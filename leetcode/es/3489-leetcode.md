-...
Título: LeetCode 3489. Zero Array Transformation IV -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Explicación de la solución**

Por cada consulta

`` `
[I , r , v ]
`` `

Usted puede elegir *cualquier subconjunto de índices `l ... r` y disminuir cada índice elegido por `v`.
Las consultas deben ser aplicadas en el orden dado – se nos permite utilizar sólo la primera `k`
consultas y tenemos que decidir el más pequeño 'k' que puede transformar todo el array en
ceros.

----------------------------------------------------

##### 1. Observaciones

*Para un índice fijo*
sólo las consultas cuyo alcance contiene `i` son útiles.
Si miramos las primeras consultas 'k', el multiset

`` `
D(i , k) = { v de todas las consultas 0 ... k-1 que cubre i }
`` `

es el conjunto de números que se permite añadir (como subconjunto) al valor actual de
Yo.
`i` puede convertirse en cero **iff** podemos elegir un subconjunto de 'D(i , k)` cuya suma es exactamente
`nums[i]`.

*Monotonicity*
Si un determinado 'k' funciona, cada 'k' más grande ≥ k` sólo puede añadir más números a cada 'D(i,k)`,
por lo tanto también funciona.
Así que el predicado *“k` es suficiente”* es monotono – podemos buscar binariamente la primera
'k' que lo satisface.

----------------------------------------------------

##### 2. algoritmo de alto nivel

`` `
si todas las nums ya son cero → respuesta = 0

construir D(i,*) por cada vez (pre-procesamiento)
búsqueda binaria en k  Iberia [1 ... m]
si factibilidad(k) = verdadero → alto = k
baja = k + 1
si no k funciona → respuesta = -1
`` `

La parte central es la prueba ** de viabilidad** para un determinado `k`.

----------------------------------------------------

##### 2.1 Prueba de viabilidad – suma subconjunta por índice

Por cada índice `i` tenemos el vector

`` `
vals[i] = lista de todos (v , queryIndex) que cubre i
`` `

Todos los pares se almacenan en orden creciente de `queryIndex`.

Para un `k' particular, sólo guardamos los pares cuyo 'queryIndex' se hizo k`:

`` `
candidato = { v de (v,idx) en vals[i] Silencio idx
`` `

Ahora tenemos que decidir si un subconjunto de 'candidato' suma a 'nums[i].
Este es el problema clásico 0/1 knapsack (subset‐sum) y se puede resolver con un
boolean DP of size `target + 1` (`target = nums[i]`).

Debido a que el número total de valores que se pueden insertar en un DP es la longitud
" candidato " , el tiempo de funcionamiento de un cheque de viabilidad es

`` `
∑ over i ( i) × nums[i] )
`` `

`nums[i]` **10 000** (la declaración garantiza que la suma de todos
elementos de array es ≤ 10 000), por lo tanto un simple DP array de ese tamaño es lo suficientemente rápido.

----------------------------------------------------

##### 3. Prueba de corrección

Demostramos que el algoritmo devuelve el número mínimo de consultas o `-1`.

-...

##### Lemma 1
Para un índice fijo `i' y un `k` fijo,
`i` puede convertirse en cero después de aplicar las primeras consultas `k`
**iff** existe un subconjunto de `D(i , k)` cuya suma equivale a `nums[i]`.

Proof.

*Si parte:*
Supongamos que existe tal subconjunto.
Aplicar las consultas correspondientes una tras otra – cada consulta que contiene i `
se utiliza exactamente una vez en los índices elegidos, disminuyendo el valor de 'i' por los
suma del subconjunto.
Después de todas las consultas " k " se procesan, el valor de " i " es " años[i] - suma = 0`.

*Sólo si parte:*
Si después de todo `k` se pregunta el valor de `i` es cero,
cada vez que se aplicó una consulta que cubre " yo " , o hemos disminuido " por " v " o
no lo tocó en absoluto.
Así, el conjunto de todos los `v' que se utilizaron en `i` es un subconjunto de `D(i, k)` y su suma es
exactamente `nums[i]`. ∎



##### Lemma 2
Si un determinado " k " satisface la prueba de viabilidad (es decir, todos los índices pueden ser cero),
entonces cualquier 'k' не k` también lo satisface.

Proof.

Todas las consultas con índices `k ... k'-1` son *nuevos* y se añaden a cada 'D(i , k') `
como elementos adicionales.
Por lo tanto, cada subconjunto que era posible para 'k' sigue siendo posible para 'k'.
En consecuencia, la prueba de viabilidad sigue siendo verdadera. ∎



##### Lemma 3
Durante la búsqueda binaria el predicado
“las primeras consultas ‘k’ son suficientes”
es monotona.

Proof.

Consecuencia directa de Lemma adultnbsp;2. ∎



##### Lemma 4
Si la prueba de viabilidad declara que es factible,
entonces el algoritmo nunca produce un valor más pequeño que `k`.

Proof.

La búsqueda binaria sólo estrecha el intervalo `[bajo, alto]` manteniendo el
propiedad que todos los índices dentro de `[bajo, alto]` contener al menos una k `
(Lemma adultnbsp;3).
Si la prueba de `k` es verdad, el algoritmo establece `alta = k`; de lo contrario se establece
`low = k+1`.
Por consiguiente, el espacio de búsqueda es siempre una gama contigua de valores factibles " k " ,
y nunca saltará un pequeño `k` factible.



##### Lemma 5
Si el algoritmo produce `-1`, ningún número de consultas puede cero el array.

Proof.

El algoritmo prueba `k = m` (todas las consultas).
Si incluso eso falla, por cada índice `i` el multiset `D(i , m)` no contiene un
subset summing to `nums[i]`.
Agregar más consultas no pueden ayudar porque todas las consultas ya están presentes.
Así es imposible con cualquier número de consultas. ∎



################################################################################################################################################################################################################################################################ Theorem
El algoritmo regresa

* el número mínimo de consultas que pueden transformar 'nums' en una matriz de todos los ceros,
o
* `-1' si es imposible.

Proof.

Si todos los elementos de `nums` ya son cero el algoritmo devuelve `0`,
que obviamente es mínima.

De lo contrario, realizamos una búsqueda binaria sobre `[1 ... m]`.
Por Lemma limitadanbsp;3 el predicado es monotone, por lo que la búsqueda binaria convergerá al
más pequeña posible.
La prueba de viabilidad es correcta por Lemma plaganbsp;1.
Si incluso el máximo `k = m` es infeasible, por Lemma cosechanbsp;5 la respuesta es `-1`.

Por lo tanto el algoritmo siempre produce el valor requerido. ∎



----------------------------------------------------

##### 4. Análisis de la complejidad

Vamos.

* `n` - longitud de la matriz (`n` es pequeña, por ejemplo ≤ 100),
* `m` - número de consultas (`m` puede ser grande, por ejemplo ≤ 105),
* `S` - el valor máximo de un elemento en `nums` (`S` ≤ 10 000, como garantiza el
problem statement).

`` `
Pre-procesamiento:
Para cada consulta insertamos su valor en cada índice de su rango.
O(número total de pares) ( ≤ n · m en el peor caso, pero pequeño en la práctica )

Prueba de viabilidad para un k dado:
Por cada índice i:
construir la lista de todos los v que vienen de las consultas.
run subset‐sum DP of size nums[i]+1 using tencióncandidate valores
→ O(Principalidad _ nums[i])
Total para una prueba: O( У ыcandidate WordPress · nums[i] ) (limitado por n·k·S en el peor de los casos)

Búsqueda binaria:
Pruebas de viabilidad O( log m )

Tiempo total: O(n·k·S) · log m ) – lo suficientemente rápido para los límites
(n ≤ 50, S ≤ 10 000, m ≤ 5 000 en las pruebas oficiales).

Memoria:
Por cada índice almacenamos en la mayoría de los valores "k" (uno por consulta de cobertura).
O( n·m ) enteros en el peor caso, pero muy por debajo de 1 GB para los límites dados.
`` `

----------------------------------------------------

##### 5. Aplicación de referencia (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minZeroArray(vector fielmente unidos nums, vector asignadovector fieltro implicado {}
int n = (int)nums.size();
int m = (int)queries.size();

--------- Pre-procesamiento : valores con su índice de consulta --------- */
vector realizador obtenidospair obtenidosint,int hilo conductor valsByIndex(n); // (v , queryIndex)
para (int q = 0; q  observado m; ++q) {
int l = consultas[q][0], r = consultas[q][1], v = consultas[q][2];
para (int i = l; i) = r; ++i)
valsByIndex[i].push_back({v, q});
}

/* -------- helper : ¿podemos hacer todos los índices cero usando las primeras consultas k? ---
auto factible = [ cl](int k)-
para (int i = 0; i) {}
/ / / / recoger todo v de las consultas
vector cd;
para (auto [v, idx] : valsByIndex[i])
si (idx < k) cand.push_back(v);

int target = nums[i];
si (target == 0) continuar; // ya cero

// 0/1 knapsack (subset sum)
vector asignado título dp(target + 1, 0);
dp[0] = 1;
para (int x : cand) {
para (int t = target; t >= x; --t)
si (dp[t - x]) dp[t] = 1;
}
si (!dp[target]) devolver falso; // imposible para este índice
}
volver verdadero; // todos los índices pueden ser cero
};

--------- Búsqueda binaria en k-------- */
if (feasible(0)) return 0; // all nums already cero

int bajo = 1, alto = m;
int answer = -1;
mientras (bajo) = alto) {
int mid = low + (high - low) / 2;
si (feasible(mid)) {}
respuesta = mitad;
alta = media - 1;
. ♫ ... {
baja = media + 1;
}
}
respuesta de retorno; // será -1 si no funciona k
}
};

/* -------- Código del conductor para el juez (no necesario en la comunicación oficial) -------- */
int main() {}
Sol de solución;
vector nums = {1,2,3};
vector de vectores consultas = {0,2,2}, {1,2}, {0,0,2};
cout se realizó sol.minZeroArray(nums, consultas)
retorno 0;
}
`` `

El programa sigue exactamente el algoritmo probado correcto arriba y
se ajusta al compilador C+17. Puede ser copiado directamente en el LeetCode
editor o cualquier entorno C+17.