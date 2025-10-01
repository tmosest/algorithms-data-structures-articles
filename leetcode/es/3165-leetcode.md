-...
Título: LeetCode 3165. Suma máxima de subsecuencia con elementos no adyacentes -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
*El problema*
Después de cada actualización `arr[p] = v` tenemos que reportar la suma máxima de un
sub-array en el que no hay dos elementos elegidos adyacentes.
Un escaneo lineal para cada consulta (`O(n)` por consulta) es demasiado lento,
por lo tanto, una estructura de datos que puede actualizarse en `O(log n)` y desde
que la respuesta puede leerse en `O(1)` es necesaria.

-...

### Por qué las tres primeras soluciones TLE

soluciÃ3n permanente complejidad Silencio para TLE
Silencio------------------------
TENIDO 1 TENIDO `O(n2)` Silencio Por cada consulta recomputamos el DP desde cero. Silencio
Silencio 2 Silencio `O(n)` (wrong) Silencio Un árbol Fenwick da sumas de prefijo – no puede mantener el
“tomar / saltar” información que se necesita para el máximo
suma no adyacente.
La recursión reconstruye todo el árbol para cada consulta,
de nuevo `O(n)` por actualización. Silencio

Así que ninguno de los tres primeros resuelve el problema en el requerido
`O(n+q) log n)` tiempo.

-...

### Cómo resolverlo con un árbol de segmento

Para cada segmento `[l...r]` guardamos cuatro valores que describen lo mejor
sumas posibles dependiendo de si el primer elemento del segmento es
y si se toma o no el último elemento del segmento
No.

`` `
0 1 (estado del límite izquierdo)
0 f00 f01 (mejor suma en [l...r] cuando el límite izquierdo no se toma)
1 f10 f11 (mejor suma cuando se toma el límite izquierdo)
`` `

`f01` y `f10` son iguales (simetría) - la matriz siempre es simétrica,
Así que realmente almacenamos sólo 4 números.

*Leaf*
Para un único elemento:

`` `
f00 = 0 (toma nada)
f01 = f10 = a (tomar el elemento)
f11 = a
`` `

*Combina dos niños*

Seamos la matriz del niño izquierdo y la del niño derecho.
La nueva matriz `M` se obtiene de la siguiente manera (sólo dos combinaciones son
posible – no podemos tomar un elemento en el niño izquierdo si también tomamos
el primer elemento del niño adecuado:

`` `
M00 = max( L00 + R00 , L00 + R01 , L01 + R00 ) // no tomar ninguno en el límite
M01 = max( L00 + R01 , L00 + R11 , L01 + R01 ) // no tomada, derecha tomada
M10 = max( L10 + R00 , L10 + R01 , L11 + R00 ) // izquierda tomada, derecha no tomada
M11 = max( L10 + R01 , L10 + R11 , L11 + R01 ) // tomar ambos límites
`` `

Los cuatro números están computados con `max`, por lo que el árbol todavía funciona
con `long` (la suma puede ser tan grande como `1014`).

*Actualizar*
Para cambiar un elemento bajamos por el árbol a la hoja
(`O(log n)`) y luego repullar las matrices en el camino de regreso a la
root – también `O(log n)`.

*Respuesta*
Después de una actualización la respuesta es simplemente la mejor suma en todo el array,
i.e. el máximo de las dos matrices que implican tomar el último
elemento:

`` `
respuesta = max( seg[0][0][1], seg[0][1]
`` `

La matriz raíz da la respuesta al instante, por lo que la complejidad general
es `O(n + q) log n)`.

-...

## Correct Java implementation

``java
Clase Solución {

privada estática final int[][] FULL = nuevo int[][] {}
{0, 1},
{1, 1}
};

largo privado[][][] seg; // 2×2 matriz para cada nodo
privada int n;

/* construir el árbol ---
construcción de vacío privado (en idx, int l, int r, int[] arr) {
si (l == r) { // hoja
seg[idx][0] = 0;
seg[idx][0][1] = seg[idx][1][0] = seg[idx][1][1] = arr[l];
retorno;
}
int mid = (l + r) 1;
build(idx) se hizo 1 TENIDO 1, l, mid, arr);
build(idx) se hizo 1 TENIDO 2, mediados + 1, r, arrr);
pull(idx);
}

/* recomputar un nodo de sus dos hijos ----------------------------
vacio privado (int idx) {}
int left = idx Identificado 1 tención 1, derecha = idx = 1 Ø 2
para (int i = 0; i) {}
para (int j = 0; j)
mucho mejor = Long.MIN_VALUE;
// no tomada (i==0) o tomada (i==1) + derecha no tomada (0) o tomada (1)
// no podemos tomar ambos extremos adyacentes - saltar ese caso
mejor = Math.max(best, seg[left][i][0] + seg[right][j]); // skip right end
mejor = Math.max(best, seg[left][i][1] + seg[right][1][j]); // take right end
seg[idx][i][j] = best;
}
}
}

/* actualización de puntos -...
actualizaciones privadas de vacío(int idx, int l, int r, int pos, int val) {
si (l == r) { // hoja
seg[idx][0] = 0;
seg[idx][0][1] = seg[idx][1][0] = seg[idx][1] = val;
retorno;
}
int mid = (l + r) 1;
si (pos י= mid) update(idx 贸 segnsitivo 1 TEN 1, l, mid, pos, val);
otra actualización (idx) se llevó a cabo 1 tención 2, media + 1, r, pos, val);
pull(idx);
}

/* rutina principal -...
int[] maxNonAdjacent(int[] arr, int[][] consultas) {
n = arrr.length;
seg = nuevo largo[4 * n][2][2];
(0, 0, n - 1, arrr);

int[] result = nuevo int[queries.length];
para (int k = 0; k) se realizaron consultas.length; ++k) {
int p = consultas[k][0];
int v = consultas[k] [1];
actualización(0, 0, n - 1, p, v);

// respuesta es la mejor suma que termina en el último elemento
resultado[k] = (int) Math.max(seg[0][0][1], seg[0][1][1][1]);
}
Resultado de retorno;
}
}
`` `

-...

### ¿Por qué un árbol de Fenwick (BIT) no funciona?

Un árbol de Fenwick sólo puede mantener una función *aditiva* en prefijos
(por ejemplo, la suma de un rango).
La suma máxima no adyacente es **no** aditivo: el valor DP al
la posición " I " depende de que se haya tomado o no " , que a su vez
depende del valor de `i‐2`.
Estas dependencias no pueden ser representadas por una simple suma prefija, por lo que
El árbol de Fenwick nunca puede producir la respuesta correcta.

-...

#### Bottom line

* Las tres primeras presentaciones son demasiado lentas o usan el mal
estructura de datos.
* La solución correcta utiliza un árbol de segmento que mantiene los cuatro DP
valores descritos anteriormente y los fusiona en `O(1)` tiempo por nodo.
* Después de cada actualización leemos la respuesta de la raíz en `O(1)`, y
todas las actualizaciones tardan `O(log n)` tiempo, dando un total
`O(n+q) log n)` algoritmo que pasa los límites.