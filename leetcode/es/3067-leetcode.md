-...
Título: LeetCode 3067. Contar pares de servidores conectados en una red de árboles de peso -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1️ Solución – Contando pares de servidores conectados (LeetCode 3067)

**Recapto de problemas* *

Se le da un * árbol de peso sin raíces* con `n` servidores (vertices) numerados `0 ... n‐1`.
Por cada borde `edges[i] = [u, v, w]` la distancia entre `u` y `v` es `w`.
Un par de servidores `(a, b)` es **conectable a través de un servidor `c`** si

1. `a ' se hizo b ' y `a != c`, `b != c`,
2. `dist(c, a)` is divisible by `signal Speed`,
3. `dist(c, b)` es divisible por `signal Speed`,
4. Los dos caminos simples `c → a` y `c → b` no comparten borde.

Devuelve un array 'cnt[0 ... n‐1]` Donde `cnt[c] ' es el número de tales pares para cada servidor 'c`.

Las limitaciones son pequeñas (`n ≤ 1000`) por lo que una solución `O(n2)` está bien.



-...

## 2down # Why an `O(n2)` DFS-de cada uno de los trabajos

* Para un centro fijo `c` cada subárbol vecino de `c` es independiente - cualquier par de servidores conectados deben estar en dos subárboles * diferentes* de `c`.
* En un subárbol sólo necesitamos saber **cuántas nódulos** tienen una distancia de 'c' que es un múltiplo de `speed señal'.
* Mientras exploramos un subárbol podemos mantener la distancia actual de 'c`; si es un múltiple aumentamos un contador.
* Después de explorar un subárbol combinamos su contador con los mostradores de los subárboles ya procesados – que da a todos los pares que utilizan este nuevo subárbol.

El algoritmo es exactamente el mismo que en las soluciones aceptadas de LeetCode que aparecen en el editorial del problema.

-...

## 3VIEW⃣ Implementación en 3 idiomas

A continuación encontrará implementaciones limpias y comentadas en **Java**, **Python**, y **C+**.
Los tres comparten la misma lógica y corren en la memoria `O(n2)` tiempo, `O(n).



-...

### 3.1 Java 17

``java
importar java.util*;

Clase Solución {
// lista de adyacencia: cada elemento es { vecindad, peso}
@SuppressWarnings("unchecked")
[] []] []] [construir]Adj(int[][] edges, int n) {
Lista obtenida[]]] g = nuevo ArrayList[n];
para (int i = 0; i) no; i++) g[i] = nuevo ArrayList recomendado();
para (int[] e : bordes) {
int u = e[0], v = e[1], w = e[2];
g[u].add(new int[]{v, w});
g[v].add(new int[]{u, w});
}
retorno g;
}

// DFS que devuelve el número de nodos en el subárbol arraigado en el nodo
// cuya distancia del centro `c` es divisible por mod.
int privado dfs(int node, int parent, long dist, int mod, List wonint[] g) {
int cnt = (dist % mod == 0) ? 1 : 0; // current node
para (int[] nb : g[nodo]) {}
int nxt = nb[0], w = nb[1];
si (nxt == parent) continúan;
cnt += dfs(nxt, node, dist + w, mod, g);
}
cnt de retorno;
}

int[] countPairsOfConnectableServers(int[][] edges, int signalSpeed) {
int n = edges.length + 1;
Lista hecha [] título [] g = buildAdj(edges, n);
int[] ans = nuevo int[n];

para (int c = 0; c) {}
pares largos = 0;
int prefix = 0; // número de nodos divisibles en subárboles procesados
para (int[] nb : g[c]) {}
int child = nb[0], w = nb[1];
int subCnt = dfs(child, c, w, signal Velocidad, g);
pares += 1L * subCnt * prefijo; // pares formados con subárboles anteriores
prefijo += sub Cnt;
}
as[c] = (int) pares;
}
devolver los ans;
}
}
`` `

■ ¿Por qué 'long'?
■ Las distancias pueden ser hasta `n * 106` (Ω109), por lo que utilizamos `long` para evitar el desbordamiento.



-...

### 3.2 Python 3.9

``python
de las colecciones importadas por defecto
importadores
sys.setrecursionlimit(2000) # safe for n ≤ 1000

Solución de clase:
def build_adj(self, edges, n):
g = defaultdict(list)
para u, v, w en los bordes:
g[u].append(v, w))
g[v].append(u, w))
retorno g

def dfs(self, node, parent, dist, mod, g):
""Retorna cuántos nodos en el subárbol arraigados en el nodo
tienen distancia del centro un múltiplo de mod.""
cnt = 1 si dist % mod == 0 si no 0
para nxt, w en g[node]:
si nxt == padre:
continuar
cnt += self.dfs(nxt, node, dist + w, mod, g)
retorno cnt

def countPairsOfConnectableServers(self, edges, signalSpeed):
n = len(edges) + 1
g = self.build_adj(edges, n)
[0]

para c en el rango(n):
pares = 0
pref = 0
para nxt, w en g[c]:
sub = self.dfs(nxt, c, w, signalSpeed, g)
pares += sub * pref
pref += sub
res[c] = pares
retorno
`` `

■ **Consejo para entrevistadores** – mantener la profundidad de recursión baja al elevar `sys.setrecursionlimit` si no estás seguro de la pila.



-...

### 3.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
vector realizador designadopair observadoint,intenta confiar título g; // { vecindad, peso}

// DFS que cuenta nodos cuya distancia del centro es múltiple de mod
int dfs(int node, int parent, long dist, int mod) {
int cnt = (dist % mod == 0) 1 : 0;
para (auto [nxt, w] : g[node]) {}
si (nxt == parent) continúan;
cnt += dfs(nxt, node, dist + w, mod);
}
cnt de retorno;
}

public:
vector asignadoint confía countPairsOfConnectableServers(vector seleccionadovector fielmente usado, int signalSpeed) {
int n = edges.size() + 1;
g.assign(n, {});
para (auto &e : bordes) {}
int u = e[0], v = e[1], w = e[2];
g[u].push_back({v, w});
g[v].push_back({u, w});
}

vector:
para (int c = 0; c) {}
pares largos = 0;
int pref = 0;
(auto [child, w] : g[c]) {}
int subCnt = dfs(child, c, w, signalSpeed);
pares += 1LL * sub Cnt * pref;
pref += sub Cnt;
}
ans[c] = static_cast correctamenteint(pairs);
}
devolver los ans;
}
};
`` `

■ ¿Por qué 'largo'?
■ La misma protección de flujo que se aplica a Java.



-...

## 4down Pruebas del Código

``python
# Arnés de prueba rápida (Python)
bordes = [0,1,1],[1,2,2],[2,3,3]]
señal = 2
print(Solution().countPairsOfConnectableServers(edges, signal)))
# Producción esperada: [1, 1, 0, 0]
`` `

Puede realizar pruebas analógicas en Java o C++ copiando el código en un compilador en línea o en un IDE local.



-...

## 5down Bueno, malo - Lo que debe discutir en una entrevista

TENIDO ANTERIOR ANTERIENTE ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTE ANTE
Silencio------------...
*La lógica intuitiva* El algoritmo refleja exactamente la declaración del problema. Silencio **Tiempo cuadrático** – Por `n = 1000` todavía está bien, pero en árboles más grandes explotaría. tención ** Código Duplicado** – Cada idioma necesita su propio ayudante del DFS; la idea central es la misma pero la sintaxis repite. Silencio
Silencio **Recuerdo luminoso** – `O(n)` lista de adyacencia + pila de recursión. Silencio ** Profundidad de la recursión** – Python/C++ puede alcanzar un límite para árboles muy profundos (aunque 1000 es seguro). Silencio ** Riesgo de flujo** – Utilizar `int` para las distancias puede romper en pesos pesados; utilizar `long` / `long`. Silencio
Silencio ** modularidad de vuelo** – Separar `build_adj`, `dfs`, y el bucle principal. **Ninguna poda** – Cada DAAT visita de nuevo todo el árbol. Silencio **Pedido extender** – Si usted necesita apoyar muchas consultas (diferente `signalSpeed`), usted rehacer todo el trabajo. Silencio

■ **Cómo hablar de esto en una entrevista* *
*“Usé un enfoque `O(n2)` que hace un DFS de cada centro para contar cuántos nodos en cada subárbol infantil tienen una distancia que es un múltiplo de la velocidad dada. Debido a que cada par de servidores conectados debe venir de dos subárboles diferentes del centro, combinar los conteos usando una suma prefijo.”*
■ Esto demuestra su comprensión de la descomposición de árboles y aritmética modular.



-...

## 6VIEW⃣ Potential Improvements (La sección “Por qué sigo entrevistando”)

Si un gerente de contratación pregunta "¿puedes hacerlo mejor?" puedes mencionar:

1. **Descomposición central** – Reduce el número total de DFS va desde `O(n2)` a `O(n log n)` dividiendo el árbol alrededor de su centroide.
2. ** Programación Dinámica en el Árbol** – Si `signalSpeed` está fijado para todo el caso de prueba, puede propagar los contadores de modulo de abajo en un solo DFS.
3. **Bitset / BFS** – Cuando los pesos son pequeños puede pre-computar los restos en O(n) por centro.

Estas optimizaciones no son estrictamente necesarias para las limitaciones dadas, pero conocerlas muestra que estás * consciente* de los cambios de rendimiento – exactamente lo que los entrevistadores aman.



-...

## 7 carreras Take-away: Cómo hacer Nail el LeetCode 3067 Entrevista

Silencio Lo que demostrarás Silencio Por qué importa Silencio
Silencio...
Silencio **Traversal de torres** – DFS/BFS, recursion, stack, adjacency lists TEN Los árboles son un elemento básico en las preguntas de entrevista (binario, n-ary, ponderado). Silencio
Silencio **Aritmética Moderna** – Contando nodos cuya distancia es un múltiplo de un valor tención Muestras que puede aplicar el razonamiento matemático a una estructura de datos. Silencio
Silencio **Combinar sub-soluciones** – prefijo suma truco Silencio Pantallas que puedes pensar en *partes* y *todo* simultáneamente. Silencio
Silencio **Análisis de complejidad** Silencio Entrevistadores esperan que usted discuta `O(n2)` vs. `O(n log n)`. Silencio
tención **Language versatility** Silencio Coding en Java, Python, C++ muestra que puede traducir conceptos a través de las pilas. Silencio

■ Si te estás preparando para una entrevista de codificación, practica escribir el ayudante de `dfs` una vez, luego reutilizarlo para la lógica "combine‐with‐previous‐subtree". Comenta bien tu código – eso es lo que buscan los reclutadores.



-...

## 8️ FAQ (Del POV del entrevistador)

**Q1. ¿Por qué no necesitamos preocuparnos por " a " b " ? #
El algoritmo cuenta con pares sin orden una vez por centro, y la declaración del problema sólo requiere que cada par es contado para el centro 'c' que satisface las condiciones. La condición " a " b " es sólo allí para evitar la doble contabilización en todo el conjunto de servidores, no para el conteo específico del centro.

**Q2. ¿Es suficiente para distancias? * *
Los pesos del borde son hasta `106` y la profundidad del árbol puede ser `n-1`. La distancia máxima es `Ω109`, que *se ajusta en un entero firmado de 32 bits, pero la suma de muchas de estas distancias puede superarlo, por lo que es más seguro utilizar `long`/`long`.

**Q3. ¿Cómo aceleraría esto por 'n = 105'? * *
Usted cambiaría a un centroide descomposición o enfoque de descomposición de luz pesada que se ejecuta en `O(n log n)` o incluso `O(n)` en algunos casos.



-...

Conclusión

- Un `O(n2)` El algoritmo DFS-a partir de cada cero es limpio, directo y pasa los límites de LeetCode.
- Los tres fragmentos de lenguaje de arriba utilizan la misma idea elegante: *cuenta los nodos divisibles en cada subárbol infantil, luego combina los recuentos en los subárboles*.
- Discutir el algoritmo en una entrevista muestra que entiende **la independencia del árbol**, **aritmética modular**, y **contando el papel** – todos los conceptos clásicos de entrevista.

¡Feliz codificación, y buena suerte aterrizando ese papel de ingeniería de software! 🚀



-...



## 10Ω⃣ SEO‐Friendly Headings (Utilice estos en su blog)

* `#LeetCode 3067 – Contando pares de servidores conectados – Solución Java `
* `#Python 3 DFS - Problema del árbol de peso `
*#C+17 – Entrevista-Ley Tree Traversal `
* `#Tree Algorithms – Job Interview Prep`
* `#Weighted Tree Network – Algorithm Design `
* Solución#DFS – Contando pares de servidores conectados `



-...



## 11Get⃣ Bonus – A Quick One‐Liner for Competitive Programmers

Si usted está absolutamente seguro de que `signalSpeed` divide todos los pesos de borde, el contador DFS simplifica para *cuentar todos los nodos* en el subárbol, que convierte toda la solución en un solo paso `O(n)`. Ese es un truco que puedes mencionar durante una entrevista para mostrar ideas más profundas.