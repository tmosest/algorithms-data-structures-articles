-...
Título: LeetCode 2959. Número de posibles conjuntos de ramas de cierre -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Número de posibles conjuntos de ramas de cierre - El bueno, el malo, y el Ugly
## A Deep‐Dive LeetCode Hard Solution in Java, Python & C++

■ **SEO Palabras clave**: LeetCode, Número de posibles conjuntos de ramas de cierre, algoritmo, Floyd‐Warshall, backtracking, teoría de gráficos, Java, Python, C++, entrevista, desafío de codificación, solución

-...

Introducción

Cuando vi por primera vez a LeetCode **2959 – “Número de posibles conjuntos de ramas de cierre”**, mis ojos se ensancharon. La declaración parece simple, pero la combinación de combinación subyacente + giro más corto es un problema *hard*.

El objetivo:
■ Contar todos los subconjuntos de ramas cerradas de tal manera que cada rama restante pueda alcanzar cada uno dentro de una distancia máxima permitida (`maxDistance`).

Las restricciones (`n ≤ 10`) sugieren que una fuerza bruta sobre subconjuntos es viable, pero todavía necesitamos un cheque de cortocircuito eficiente para cada subconjunto.

A continuación caminaré por el *bueno*, el *bad*, y las partes *muy* de abordar este problema, y luego presentar código limpio y listo para la producción para **Java, Python, y C++**.

-...

Problema Recap

TENIDO ANTERIOR ANTERIOR Descripción
Silencio...
Silencio **n** Silencio Número de ramas (0-indexed). `1 ≤ n ≤ 10`.
TEN **roads** TENIDO Los bordes de peso no dirigidos. Se permiten múltiples bordes. Silencio
Silencio **maxDistance** Silencio Todas las ramas restantes deben ser ≤ esta distancia aparte. Silencio
Silencio **Retorno** Silencio Conde de *valid* conjuntos de cierre (bitmasks) que satisfacen la condición. Silencio
Silencio **Edge case** ← Empty set of active branches (all closed) is always valid. Silencio

-...

## 3down El desafío básico

1. **Subset Explosion** – `2n ' possible close‐sets (`n ≤ 10` → 1024).
2. ** Gráfico Dinámico** – cada subconjunto elimina algunos vértices y bordes de incidentes.
3. **Shortest Path** – debemos conocer las distancias de todos los pares en el gráfico *Remanente* rápidamente.

La fuerza bruta más directa ejecutaría el subconjunto Dijkstra o Floyd‐Warshall *per*, costando `O(2n * (n3))` – todavía bien para `n=10`, pero podemos hacerlo mejor pre-computando distancias de todos los puntos una vez en el gráfico completo y luego *filtering* distancias para cada subconjunto.

-...

## 4VIEW⃣ Approach 1 – Full Floyd‐Warshall + Subset Check (Easy but Clear)

1. **Compute full all-pairs shortest distances** (`dist[i][j]`) en el gráfico completo utilizando Floyd‐Warshall.
* Complejidad: `O(n3)` con `n ≤ 10`.
2. **Tetrato sobre todos los subconjuntos** (bitmask).
* Para cada subconjunto, sólo necesitamos asegurar que *para cada par de nodos activos* `i` y `j`, `dist[i][j] ≤ maxDistance`.
3. Cuenta los subconjuntos que satisfacen la condición.
* El subconjunto vacío (todos los nodos cerrados) pasa automáticamente.

### Por qué funciona

Debido a que la eliminación de vértices *no puede* crear un camino más corto que el ya computado en el gráfico completo. Si un par está dentro de `maxDistance` en el gráfico completo, permanece dentro de esa distancia cuando cerramos otras ramas (a menos que cierremos uno de los puntos finales). Por el contrario, si un par es *ya* más lejos que `maxDistance`, el subconjunto es inválido independientemente de qué más cerramos.

Por lo tanto, no necesitamos recomputar distancias para cada subconjunto, sólo filtro.

-...

## 5VIEW⃣ Complexity Analysis

TEN TERRITORIO TEN TERRITORIDAD
Silencio...
Silencio Floyd‐Warshall on full graph Silencio `O(n3)` (`≤ 1000` operations for `n=10`) Silencio
← Subconjuntos de Enumerate Silencioso `O(2n)` (`≤ 1024`) Silencio
Silencio Ver todos los pares en el subconjunto Silencioso `O(n2)` por subconjunto → `O(2n * n2)`
Silencio **Total** Silencioso `O(n3 + 2n * n2)` → efectivamente ` tratar 1.3e6` ops for worst case. Silencio

Memoria: `O(n2)` para la matriz de distancia.

-...

## 6VIEW⃣ Implementation

A continuación se presentan implementaciones limpias y comentadas en **Java**, **Python**, y **C+** que siguen el enfoque anterior. Cada uno utiliza una matriz de distancia única y enumeración de bitmask.

■ **Confianza para las entrevistas** – Cuando explicas la solución, destaca la *observación*: cerrar los vértices no puede acortar ningún camino más corto, por lo que pre-computar todos los pares una vez es seguro. A menudo los entrevistadores clave buscan información.

-...

### 6.1 Java

``java
importar java.util*;

Clase Solución {
int public int numberOfSets(int n, int maxDistance, int[][] roads) {
int INF final = (int)1e9;
int[][] dist = new int[n][n];

// inicializar distancias
para (int i = 0; i) {}
Arrays.fill(dist[i], INF);
dist[i][i] = 0;
}

// construir bordes gráficos
para (int[] e : carreteras) {
int u = e[0], v = e[1], w = e[2];
si (w  won dist[u] [v]) {
dist[u][v] = dist[v] [u] = w;
}
}

// Floyd‐Warshall en el gráfico completo
para (int k = 0; k)
para (int i = 0; i)
para (int j = 0; j)
si (dist[i][k] + dist[k] [j] [j] [i] [j])
dist[i][j] = dist[i][k] + dist[k][j];

total Máscaras = 1 > >
respuesta int = 0;

// iterate all subsets of *closed* nodes
para (enmascarado = 0; máscara) total Máscaras; ++masca) {
booleano ok = verdadero;
para (int i = 0; i)
para (int j = i + 1; j)
si ((mask нелили i) " 1) == 0 " перен (mask ненно j) " ) == 0) {
si (dist[i][j] не maxDistance) ok = falso;
}
si (ok) respuesta+;
}
respuesta de retorno;
}
}
`` `

-...

### 6.2 Python

``python
Solución de clase:
def numberOfSets(self, n: int, maxDistance: int, roads: List[List[int]) - título int:
INF = 10**9
[INF] * n for _ in range(n)]
para i en rango(n):
dist[i][i] = 0

para u, v, w en carreteras:
[v]:
dist[u][v] = dist[v] [u] = w

Floyd-Warshall
para k en rango(n):
para i en rango(n):
para j en rango(n):
si dist[i][k] + dist[k][j] se entiende dist[i][j]:
dist[i][j] = dist[i][k] + dist[k][j]

respuesta = 0
para máscaras en el rango(1)
OK = True
para i en rango(n):
si mascara # Nodo I closed
continuar
para j en rango(i + 1, n):
si mascarilla √Īan j > 1 nodo j cerrado
continuar
si dist[i][j] > maxDistance:
ok = Falso
descanso
si no está bien:
descanso
Si está bien:
respuesta += 1
respuesta
`` `

-...

### 6.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
número de intOfSets(int n, int maxDistance, vector seleccionado, identificador implicados iguales) {
INF = 1e9;
vector seleccionado(n, INF));

para (int i = 0; i) no; ++i) dist[i] = 0;

para (auto &e : carreteras) {
int u = e[0], v = e[1], w = e[2];
[v] [v] = dist[v] = w;
}

// Floyd‐Warshall en el gráfico completo
para (int k = 0; k)
para (int i = 0; i)
para (int j = 0; j)
dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j]);

int total = 1 > 0 >

para (enmascarado = 0; mascarilla) {
bool ok = verdadero;
para (int i = 0; i)
para (int j = i + 1; j)
si ((mask нелили i) " 1) == 0 " перен (mask ненно j) " ) == 0)
si (dist[i][j] не maxDistance) ok = falso;
si (ok) ++ans;
}
devolver los ans;
}
};
`` `

-...

## 7down Good Good, Bad & Ugly in the Solution Space

**Aspecto** Silencio**
Silencio----------------------------------------------------
*Key* – los nodos de cierre no pueden acortar ningún camino más corto. Silencio difícil de detectar sin pensar en la contracción de gráficos. Silencio Los entrevistadores suelen preguntar *por qué* distancias pre-computadoras es segura. Silencio
TEN ** Simplicidad Algorítmica** TENIDO Clear `O(n3)` pre-computación + filtro de bitmask. Podría parecer “demasiados bucles” para principiantes. El Floyd‐Warshall triplicado puede sentirse pesado en otros contextos. Silencio
Silencio **Scalability** Silencio Obras para `n ≤ 10`. Silencio Para mayor `n`, el factor `2n ' se vuelve imposible. Silencio Si `n` eran 20+, necesitamos una estrategia diferente (por ejemplo, DP + BFS). Silencio
TEN **Implementation Readability** TEN Cada versión del idioma es ~50 líneas. TEN Demasiados arrays temporales si recomputa distancias por subset. ← Usar listas de adyacencia para cada subconjunto (fuerza bruta) conduce a código que es difícil de depurar. Silencio
tención **Memory Footprint** Silencioso `O(n2)` distancias, trivial. La vida misma.

-...

## 8️ Common Pitfalls & Edge Cases

Silencio Pitfall Silencio
Silencio...
Silencio **Aristas múltiples** – mantener el peso *mínimo*. En el paso inicial, siempre `min(w, dist[u][v]). Silencio
← **Disjoint Graph** – Algunos pares pueden nunca conectarse (`INF`). Silencioso Treat `INF ' ¢ `maxDistance` como inválido; el subconjunto será rechazado. Silencio
Silencio ** Todos los nodos cerrados** Asegúrate de contar este subconjunto. En el bucle del subconjunto, si *no existe un nodo activo*, `ok ' permanece `True`. Silencio
Silencio **Large `maxDistance`** – ю 1e9 – asegúrese de que su `INF ' es más grande. TENIDO Use `1e9` o `Long.MAX_VALUE` en consecuencia. Silencio

-...

Consejos de entrevista

1. **Empieza con la observación**: “Los vértices perdidos no pueden acortar un camino más corto. ”
2. **Pre-computación de la mención**: una Floyd‐Warshall en el gráfico completo.
3. **Mostrar la lógica bitmask** – iterar todos los subconjuntos, filtrar distancias pares.
4. **Discuss Complexity** – `n` es pequeña, por lo que 1024 subsets están bien.
5. **Preguntar preguntas aclaratorias** – por ejemplo, “¿El conjunto activo vacío es considerado válido?” – entrevistadores aprecian la precisión.

-...

Conclusión

LeetCode 2959 es una hermosa mezcla de combinatoria y teoría de gráficos.
- La parte *buena* es la elegante percepción de que una matriz pre-computada de todos los puntos basta.
- La parte *bad* es que es fácil pasar por alto la imposibilidad de “shortening-path” y terminar recomputando distancias para cada subconjunto.
- La parte *ugly* se ocupa de múltiples bordes y garantiza que el valor " INF " sea suficientemente alto.

Con los fragmentos de código arriba, usted está listo para enviar o entregar una solución limpia en **Java, Python, o C+**. Buena suerte en su próxima entrevista de codificación – este problema es un gran escaparate de cómo una pequeña observación puede convertir un desafío aparentemente difícil en una solución perfectamente manejable.