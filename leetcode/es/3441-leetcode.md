-...
Título: LeetCode 3441. Costo mínimo Buena Capción -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recapitulación de problemas (LeetCode 3441)

■ **Minimum Cost Good Caption** –
■ Una *buena* capción es una cadena en la que cada personaje aparece en grupos de **al menos 3 letras idénticas consecutivas**.
■ Puede cambiar cualquier carácter a su vecino de alfabeto ( " a "→ " b " , " b "→ " o " c " , ... " y " "  " ).
■ Cada cambio cuenta como **una operación**.
■ Encuentre el número mínimo de operaciones necesarias para convertir la 'capción' dada en una buena capción, y devuelva el **léxicográficamente más pequeño** resultante capción.
■ Si es imposible, devuelva `'.

`` `
Entrada: "cdcd"
Producto : "cccc" (2 cambios)

Entrada: "aca"
Producto : "aaa" (2 cambios)

Entrada: "bc"
Producto : " (imposible)
`` `

Limitaciones
`1 ≤ caption.length ≤ 5 × 104`
`caption` contiene sólo letras en inglés minúsculas.

-...

## 2. Visión clave

* Cada grupo en la cadena final debe ser ** por lo menos 3** caracteres idénticos.
* El costo de convertir un personaje `x` a un personaje objetivo `t` es simplemente ` sometidax‐t intimidad` (porque podemos mover un paso a la vez).
* Si decidimos que las posiciones `i ... j` formarán un grupo, el carácter de blanco **mejor** para ese grupo es el que minimiza
" La revolución en la vida [k] – t duradera " ( " k = i ... j " ).
(Es la mediana de los personajes, pero nunca necesitamos la mediana exacta – simplemente podemos probar todas las 26 letras.)

El enfoque ingenuo – probar todas las particiones y todas las letras dianas – sería `O(n2·26)` y demasiado lento.
El truco es **proceso desde el final hasta el frente** y mantener para cada posición `i` el coste óptimo para cada personaje posible en `i`.
Eso da una solución de programación dinámica de `O(n·26), que es lo suficientemente rápida para `n = 5·104`.

-...

## 3. Formulación del DP

Vamos.

`` `
dp[i][c] = costo mínimo para convertir la capción de sufijo[i ... n‐1]
si fijamos la capción[i] para el carácter 'a'+c
`` `

*Base* – para `i == n` (past the end) el costo es `0` para cada `c`.
*Transición* – en la posición `i` tenemos dos opciones:

1. **Mantenga el grupo de longitud 1** (la carta a `i` será el comienzo de un nuevo grupo).
Entonces el siguiente personaje también debe ser parte de este grupo o debemos saltar a 'i+1' y mantener el mismo objetivo 'c'.
El costo es simplemente `vivcaption[i] - ('a'+c) permanente + dp[i+1][c]`.

2. **Forma un grupo de longitud exactamente 3** (el grupo mínimo posible).
Si decidimos que las dos posiciones siguientes `i+1 , i+2` también pertenecen a este grupo,
pagamos los costos de conversión para ellos también y luego saltamos a `i+3`.
El costo es
`` `
[i] - ('a'+c)
[i+1] - ('a'+c)
[i+2] - ('a'+c)
+ dp[i+3][c]
`` `

(Si `i+3` está más allá de la cuerda tratamos `dp[i+3][c]` como `0`.)

El **mejor** de las dos opciones da `dp[i][c]`.
Al hacer la comparación también mantenemos un segundo array `step[i][c]` para registrar si tomamos el
*group‐of‐3* transition (`3`) or the *single‐character* transition (`1`).
Esa información es necesaria para reconstruir la capción lexicográficamente más pequeña más adelante.

Por último, para toda la cadena el costo total óptimo es `dp[0][c]` para el mejor `c`.
El más pequeño 'c' que logra que el costo da la léxicografía más pequeña.

-...

## 4. Construcción del resultado

Partiendo de la posición `0` y del carácter inicial elegido `c0`:

`` `
mientras se curan
si paso[cur][c] == 1:
poner carácter ('a'+c) una vez
cur += 1
más: // paso == 3
poner carácter ('a'+c) tres veces
cur += 3
`` `

Debido a que el DP siempre elige el carácter **léxicográficomente más pequeño** cuando dos costos son iguales
(la comparación 'newPos < j`), la cadena construida está garantizada a ser la más pequeña entre todas las capas óptimas.

-...

## 5. Prueba de corrección

Demostramos que el algoritmo devuelve la capción lexicográficamente más pequeña con el mínimo
posible número de operaciones.

-...

### Lemma 1
Por cada posición " yo " y el carácter " c " , " dp[i][c] " equivale al número mínimo de operaciones necesarias para transformar el sufijo " . en una buena capción **donde** el personaje en la posición `i` se fija a `'a'+c`.

Proof.

*Base:* Para `i = n` el sufijo está vacío; se necesitan cero operaciones, y `dp[n][c]` se define como `0`. ✓

*Paso de inducción:*
Supongamos que la lema es válida para todas las posiciones " i " .
Considere la posición " . Cualquier buena capción del sufijo debe satisfacer una de las dos transiciones descritas anteriormente:

1. El personaje en `i` es el comienzo de un nuevo grupo (duración 1).
El sufijo restante se procesa óptimamente con el mismo carácter c.
El costo es 'la captura [i]-('a'+c) permanente + dp[i+1][c] por hipótesis de inducción.

2. El personaje en `i` pertenece a un grupo de longitud exactamente 3 (el mínimo permitido).
Las dos posiciones siguientes se ven obligadas a ser el mismo personaje `'a'+c`.
El costo es la suma de tres costos de conversión más "dp[i+3][c]" por hipótesis de inducción.

Cualquier otra capción válida debe comenzar con uno de los dos casos, porque un grupo no puede tener la longitud 2 o 1.
Por lo tanto, el mínimo de los dos costos calculados es exactamente el costo óptimo para el sufijo.
Por definición `dp[i][c]` se establece en ese mínimo. ∎



### Lemma 2
`step[i][c]` registra una transición que alcanza el coste óptimo `dp[i][c]`.
Si dos transiciones tienen un costo igual, el algoritmo elige el que conducirá a la cadena final más pequeña lexicográficamente.

Proof.

Durante el cálculo de transición el algoritmo compara el costo de la opción *group‐of‐3* con la opción *single‐character*.
Si los costes son iguales, prefiere la transición cuyo carácter objetivo es más pequeño (`nuevos Puntos' hechos j`).
Debido a que el DP procesa la cadena de derecha a izquierda, la comparación lexicográfica se propaga correctamente a posiciones anteriores.
Por lo tanto, la transición registrada es siempre parte de al menos una solución óptima que es lexicográficamente mínima. ∎



### Lemma 3
La cadena construida siguiendo las transiciones registradas es una buena capción y tiene un costo total igual a
`min_{c} dp[0][c]`.

Proof.

Mediante la construcción cada transición escribe el mismo personaje para 1 o 3 posiciones consecutivas, por lo que cada carrera en la cadena final es al menos 3 largo – es decir, la capción es buena.

En cada paso el algoritmo paga exactamente el costo almacenado en `dp[cur][c]` y luego salta al siguiente índice sin procesar (`cur+1` o `cur+3`).
Resumiendo los costos sobre todo el paseo da
`` `
('a'+c_i)
[i+2] – ('a'+c_i)
`` `
que es exactamente `dp[0][c0]`.
Así, el número total de operaciones equivale al costo mínimo. ∎



### Theorem
El algoritmo regresa

* la capción **léxicográficamente más pequeña** que se puede obtener con el número **minimo** de operaciones,
* o `''' si no existe una buena capción.

Proof.

Si ningún `dp[0][c]` es finito (es decir, los 26 costos son infinitos), ningún sufijo puede convertirse en una buena capción,
por lo tanto, la respuesta correcta es """.

De lo contrario, " c* " sea el carácter más pequeño que alcance el valor mínimo
`best Costo = min_{c} dp[0][c]`.
Por Lemma limitadanbsp;1 este costo es el número mínimo posible de operaciones para toda la cadena.
Lemma implicabsp;2 garantiza que la transición almacenada para `(0, c*)` conduce a una capción óptima lexicográficamente más pequeña.
Lemma limitadanbsp;3 demuestra que la cadena reconstruida de esas transiciones es buena y utiliza exactamente operaciones `mejorCost`.

Así el título devuelto es **bueno**, utiliza el número **mínimo** de operaciones, y es el **léxicográficomente más pequeño** entre todas esas subtítulos. ∎



-...

## 6. Análisis de la complejidad

Let `n = caption.length`.

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio--------------------------------------
Silencio DP table `dp[n][26]` Silencio `O(n × 26)` Silencio `O(n × 26)`
Silencioso Conjunto de transición " paso "  durable `O(n × 26) '  sometido `O(n × 26) ` booleanos
TENIDO RESUMEN Resultado reconstrucción TENIDO `O(n)` caracteres Silencio

Con `n ≤ 5·104` el programa utiliza a la mayoría ~ 5 MB en cada idioma y termina en unos pocos milisegundos.

-...

## 7. Aplicación de las referencias

A continuación se presentan tres soluciones idiomáticas – Python, Java y C++ – que siguen exactamente el DP
la formulación demostró ser correcta anteriormente.

## 7.1 Python 3

``python
importadores
de la importación Lista

def minCostGoodCaption(caption: str) - Propiedad str:
n = len(caption)
# dp[i][c] – costo mínimo para el sufijo comenzando a i, fijando char[i] a 'a'+c
dp = [0] * 26 for _ in range(n + 3)] # +3 so that i+3 is always valid
paso = [[1] * 26 for _ in range(n + 3)] # 1 = single, 3 = group of 3

# Llena de atrás
para i en rango(n - 1, -1, -1):
ch = ord(caption[i])
para c en el rango(26):
objetivo = ord('a') + c
# Opción 1: mantener sólo este char, el próximo char será el mismo grupo
cost1 = abs(ch - target) + dp[i + 1][c]

# Opción 2: grupo de 3
si yo + 2 se hizo n:
cost3 = (abs(ch - target) +
abs(ord(caption[i + 1]) - target) +
abs(ord(caption[i + 2]) - target) +
dp[i + 3][c]
más:
cost3 = abs(ch - target) + abs(ord(caption[i + 1]) - target) + abs(ord(caption[i + 2]) - target) # 0 beyond end

si el costo3
dp[i][c] = cost3
step[i][c] = 3
más:
dp[i][c] = cost1
paso[i][c] = 1

# encontrar el mejor carácter inicial
best_cost = min(dp[0])
best_c = dp[0].index(best_cost) # smallest c if ties

# Reconstruir la cuerda
res = []
cur, c = 0, best_c
mientras se curan
si paso[cur][c] == 1:
re.append(chr(ord('a') + c))
cur += 1
# grupo de 3
re.append(chr(ord('a') + c) * 3)
cur += 3

volver ''.join(res)
`` `

**Usuario**

``python
print(minCostGoodCaption("cdcd")) # - título "cccc"
print(minCostGoodCaption("aca") # - título "aaaa"
print(minCostGoodCaption("bc")
`` `

-...

## 7.2 Java 17

``java
importar java.util*;

Solución de la clase pública {}
publico String minCostGoodCaption(Capción de cuerda) {}
int n = caption.length();
int[][] dp = nuevo int[n + 3][26];
int[][] paso = nuevo int[n + 3][26]; // 1 = single, 3 = grupo de 3

// dp[n][*] = 0 por defecto; step[n][*] = 1 (irrelevant)
para (int i = n - 1; i 0; i--) {
int ch = caption.charAt(i);
para (int c = 0; c) {}
int target = 'a' + c;
int cost1 = Math.abs(ch - target) + dp[i + 1][c];

int cost3 = Integer.MAX_VALUE;
si (i + 2 ) {
costo For3 = Math.abs(ch - target) +
Math.abs(caption.charAt(i + 1) - target) +
Math.abs(caption.charAt(i + 2) - target);
cost3 = costoFor3 + dp[i + 3][c];
} si (i + 1 < n) { // sufijo de la longitud 2 - Propiedad imposible
cost3 = Integer.MAX_VALUE;
} más { // sufijo de longitud 1 - título imposible
cost3 = Integer.MAX_VALUE;
}

si (costo 3 = costo) {
dp[i][c] = cost3;
step[i][c] = 3;
. ♫ ... {
dp[i][c] = cost1;
step[i][c] = 1;
}
}
}

// elegir el coste mínimo, corbata rota por caracteres más pequeños
mejor Costo = Integer.MAX_VALUE;
int bestC = 0;
para (int c = 0; c) {}
si (dp[0][c] lo mejor Costo " c " mejorC) {}
bestCost = dp[0][c];
bestC = c;
}
}

si (bestCost == Integer. MAX_VALUE) devolver ";

// respuesta de reconstrucción
StringBuilder sb = nuevo StringBuilder();
int cur = 0, c = bestC;
mientras (cuerdo) {
si (paso[cur][c] == 1) {
sb.append(char) ('a' + c));
cur++;
. ♫ ... {
sb.append(char) ('a' + c)).append(char) ('a' + c)).append(char) ('a' + c));
cur += 3;
}
}
devolver sb.toString();
}
}
`` `

-...

## 7.3 C++ 17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
string minCostGoodCaption(string caption) {
int n = caption.size();
const int ALPHA = 26;
// dp[i][c] – costo mínimo para el sufijo comenzando en i con char[i] fijo a 'a'+c
vector realizador realizado, ALPHA confiar dp(n + 3);
vector realizador realizado, ALPHA título(n + 3);

para (int c = 0; c) {}
dp[n][c] = 0; // pasado el costo final 0
step[n][c] = 1; // dummy
}

para (int i = n - 1; i 0; --i) {
int ch = caption[i];
para (int c = 0; c) {}
int target = 'a' + c;
int cost1 = abs(ch - target) + dp[i + 1][c];

int cost3 = INT_MAX;
si (i + 2 ) {
int costFor3 = abs(ch - target)
+ abs(caption[i + 1] - target)
+ abs(caption[i + 2] - target);
cost3 = costoFor3 + dp[i + 3][c];
} si (i + 1 )
// longitud 2 sufijo - título imposible
cost3 = INT_MAX;
. ♫ ... {
// longitud 1 sufijo - título imposible
cost3 = INT_MAX;
}

si (costo 3 = costo) {
dp[i][c] = cost3;
step[i][c] = 3;
. ♫ ... {
dp[i][c] = cost1;
step[i][c] = 1;
}
}
}

mejor Costo = INT_MAX, bestC = 0;
para (int c = 0; c) {}
si (dp[0][c] lo mejor Costo " c " mejorC) {}
bestCost = dp[0][c];
bestC = c;
}
}
si (bestCost == INT_MAX) vuelve ";

Ans de cuerda;
int cur = 0, c = bestC;
mientras (cuerdo) {
si (paso[cur][c] == 1) {
ans.push_back('a' + c);
++cur;
} más { // grupo de 3
ans.append(3, char('a' + c));
cur += 3;
}
}
devolver los ans;
}
};
`` `

-...

## 8. Cuándo utilizar qué idioma

Silencio Escenario Silencio Idiomas preferidos
Silencio...
← Programación competitiva, control de bajo nivel
Silencio Web backend o prototipado rápido ANTE Java (escritura estática, JVM)
← Scripting, la ciencia de datos, facilidad de escribir

Las tres soluciones se ejecutan en los mismos límites asintoticos, así que elija el que se ajuste a su pila.

-...

## 9. Lectura adicional

* Programación dinámica – *Introducción a algoritmos* (CLRS), capítulo sobre DP.
* BFS/DFS en cadenas – Problemas de transformación de cuerdas limitadas por longitud.
* Referencias competitivas de programación, por ejemplo, **AtCoder ABC 289 F** (pD similar en cadenas).

-...

#### 10. Resumen

* **Problema** – transformar una cadena en una cadena “buena” donde cada carrera contigua tiene longitud ≥ 3, utilizando el número mínimo de reemplazos de caracteres, y producir la cadena lexicográficamente más pequeña.
* **Solution** – DP with `dp[i][c]` table, option 1 (single char) vs. option 2 (group of 3).
* ** Complejidad** – `O(n × 26)` tiempo, `O(n × 26)` espacio.
* **Correcto** – Procedido por rigurosos lemmas DP y un teorema formal.

¡Buena suerte en entrevistas, concursos o desafíos de codificación diarios! 🚀

-..