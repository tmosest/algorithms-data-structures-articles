-...
Título: LeetCode 1786. Número de caminos restringidos del primero al último nodo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1786. Número de caminos restringidos del primer a último nodo
*(Medium – LeetCode)*

■ ** Resumen del programa* *
■ Se le da un gráfico no dirigido, ponderado, conectado con *n* nodos (1-basado).
■ Por cada nodo *x* que `dist(x)` sea la distancia más corta de *x* a nodo *n*.
■ Un camino restringido ** del nodo 1 al nodo *n* es un camino
" [z0, z1, ... , zk] " , donde `z0 = 1 ' , `zk = n ' , y por cada ` i `
" dist(zi) " (la distancia al último nodo disminuye estrictamente).
■ Contar todos estos caminos modulo `1 000 000 007`.

-...

## ↑ Key Insight

1. **Las distancias más cortas del objetivo** – Run Dijkstra desde el nodo *n*.
2. **Graph se convierte en DAG** – Por cada borde `(u,v)` sólo la dirección 'u → v` con
`dist(u) √≥ dist(v)` puede aparecer en un camino restringido.
3. **DP on the DAG** – `ways[u] = Governing ways[v]` over all outgoing restricted edges.
4. Resultado**: "Siempre[1]".

El algoritmo funciona en la memoria `O(n+m) log n)` tiempo y `O(n+m).



-...

## 📦 Code Solutions

A continuación se presentan implementaciones idiomáticas limpias en **Java, Python y C+**.

## Java 17

``java
importar java.util*;

*
* LeetCode 1786 – Número de caminos restringidos
*/
Solución de la clase pública {}
int final estático privado MOD = 1_000_000_007;

int countRestrictedPaths(int n, int[] edges) {
// 1 / ⃣ Build adjacency list
Lista realizadaLista realizada[] título g = nuevo ArrayList recomendado(n + 1);
para (int i = 0; i <= n; i++) g.add (new ArrayList fiel());
para (int[] e : bordes) {
int u = e[0], v = e[1], w = e[2];
g.get(u).add(new int[]{v, w});
g.get(v).add(new int[]{u, w});
}

Dijkstra desde el nodo n
long[] dist = new long[n + 1];
Arrays.fill(dist, Long.MAX_VALUE);
dist[n] = 0;
PriorityQueue hacía lo largo[] confía pq = nueva PrioridadQueue decir:(Comparador.comparingLong(a - título a[1]));
pq.offer(new long[]{n, 0});

mientras (pq.isEmpty()) {
long[] cur = pq.poll();
int u = (int) cur[0];
largo d = cur[1];
si (d != dist[u]) continúan;
para (int[] nb : g.get(u) {
int v = nb[0], w = nb[1];
largo nd = d + w;
si {}
dist[v] = nd;
pq.offer(nuevo largo []{v, nd});
}
}
}

DP (memoized DFS) en el DAG
long[] dp = new long[n + 1];
Arrays.fill(dp, -1);
dfs(1, n, g, dist, dp);
}

dfs privados largos(int u, int n, Lista hecha g,
largo[] dist, long[] dp) {
si (u == n) retorno 1;
si (dp[u]!= -1) retorno dp[u];
ans largas = 0;
para (int[] nb : g.get(u) {
int v = nb[0];
si (dist[u]
as = (ans + dfs(v, n, g, dist, dp) % MOD;
}
}
dp[u] = ans;
devolver los ans;
}
}
`` `

## Python 3

``python
importación heapq
de la importación Lista

MOD = 1_000_000_007

Solución de clase:
def countRestricted Paths(self, n: int, edges: List[List[int]]) int:
# 1 Construir la lista de adjacency
g = [[] para _ en rango(n +1)]
para u, v, w en los bordes:
g[u].append(v, w))
g[v].append(u, w))

# 2️ Dijkstra from node n
(n +1)
dist[n] = 0
pq = [(0, n)] # (dist, node)
mientras pq:
d, u = heapq.heappop(pq)
si d != dist[u]:
continuar
for v, w in g[u]:
d + w
si nd , se hizo [v]:
[v] = nd
heapq.heappush(pq, (nd, v))

DP on DAG (topological order by dist)
orden = orden(range(1, n + 1), key=lambda x: dist[x])
dp = [0] * (n +1)
dp[n] = 1
para u en orden:
for v, _ in g[u]:
si dist[u]
dp[u] = (dp[u] + dp[v] % MOD

retorno dp[1]
`` `

### C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
static const int MOD = 1'000'007;
public:
int countRestrictedPaths(int n, vector obtenidosvector fieltros iguales bordes) {}
Lista de adyacencia
vector realizador obtenidospair obtenidosint,int hilo conductor g(n + 1);
para (auto &e : bordes) {}
int u = e[0], v = e[1], w = e[2];
g[u].push_back({v, w});
g[v].push_back({u, w});
}

Dijkstra desde el nodo n
vector llevado a cabo largo plazo dist(n + 1, LLONG_MAX);
dist[n] = 0;
priority_queue hicistepair realizado largo,int
vector asignadopair llevado largo largo,int.
mayor significadopair realizado largo,int pq;
pq.push({0, n});
mientras (pq.empty()) {
auto [d, u] = pq.top(); pq.pop();
si (d != dist[u]) continúan;
para (auto [v, w] : g[u]) {}
largo largo nd = d + w;
si {}
dist[v] = nd;
pq.push({nd, v});
}
}
}

DP on DAG (topological by dist)
vector de orden(n)
iota(order.begin(), order.end(), 1);
sort(order.begin(), order.end(),
[](int a, int b){ return dist[a] [a] [b]; });

vector asignadointento dp(n + 1, 0);
dp[n] = 1;
para (int u : order) {
para (auto [v, w] : g[u]) {}
si {}
dp[u] = (dp[u] + dp[v]) % MOD;
}
}
}
dp[1];
}
};
`` `

Las tres soluciones comparten el mismo tiempo y la complejidad espacial:

- **Tiempo**: `O(n + m) log n)` (Dijkstra domina).
- **Espacio**: `O(n + m)` (lista de asistencia + array de distancia + matriz DP).

-...

Blog Artículo
*(SEO-optimizada – “LeetCode 1786, caminos restringidos, gráfico, entrevista”) *

### Title
**Mastering LeetCode 1786: Número de caminos restringidos – De la Teoría Gráfico a Job‐Ley Entrevista Prep* *

## Meta Descripción
“Aprenda la solución completa para LeetCode 1786 – caminos restringidos. Sumérgete en Dijkstra, DP en DAG y Java, Python, código C++. Boost your coding interview scores and land your dream job. ”

##### Outline

TENCIÓN TERRITORIO ANTERIOR ANTERIOR
Silencio...
Silencio 1. Sinopsis del problema tención Definición, limitaciones, ejemplos. Silencio
Silencio 2. Intuición Silencio Por qué funciona Dijkstra + DP. Silencio
Silencio 3. Restricted Edge Direction Silencio Show how `dist(u) √≥ dist(v)` convierte el gráfico en un DAG. Silencio
Silencio 4. Casos de bordes " Pitfalls " tención Cero-pesos bordes, distancias iguales, múltiples caminos más cortos. Silencio
Silencio 5. Algorithm ← Paso a paso con diagramas. Silencio
Silencio 6. Detalles de la implementación Silenciosos Códigos, estructuras de datos, memoización. Silencio
Silencio 7. Análisis de Complejidad ← Big‐O, por qué es óptimo. Silencio
Silencio 8. Bien / mal / Ugly ← Qué celebrar, qué evitar, los obstáculos del mundo real. Silencio
Silencio 9. Entrevista común Variantes Silenciosos “Patinas con reducción no limitada”, “Agregar pesos nodos”, “Versión sin ponderar”. Silencio
Silencio 10. Cómo utilizar en las entrevistas ← Temas de conversación, por qué el entrevistador lo ama. Silencio
Silencio 11. Recursos de práctica ← Más preguntas de gráfico LeetCode, libros, cursos en línea. Silencio
Silencio 12. Conclusión Silencioso, aliento. Silencio

Texto completo

-...

##### 1. Panorama general de los problemas

El problema *Número de Senderos Restrictos* se encuentra en la intersección de algoritmos de gráficos **shortest‐path** y ** programación dinamica**.
Dado un gráfico no dirigido ponderado, un camino está “restricto” si el *distance to the destination* disminuye estrictamente a cada paso.
Debemos contar todos estos caminos del nodo 1 al nodo *n*.

Las limitaciones son generosas:
- 2 ≤ 20.000
- 1 ≤ bordes. longitud ≤ 200.000
- `1 ≤ peso ≤ 106 `
- El gráfico está garantizado para estar conectado.

Estos límites hacen **O(n+m) log n)** el lugar dulce – cualquier cosa más lenta es un punto muerto en una entrevista.

-...

##### 2. Intuición

1. **La distancia más corta del objetivo** – Piense en 'dist(x)` como un "mapa de la altura" del gráfico. Nodo *n* es el nivel del mar (distancia 0).
2. **Los caminos restringidos deben ir cuesta abajo** – Debido a que se requiere `dist(zi) œ dist(zi+1)`, cada paso debe descender estrictamente este mapa de altura.
3. **Los edges apuntan cuesta abajo sólo** – Para cualquier borde no redirigido `(u,v)`, sólo la dirección donde el comienzo es más alto que el extremo puede ser utilizado.
4. **El gráfico se convierte en un Gráfico Acíclico Directo (DAG)** – Ningún ciclo puede existir porque las alturas disminuyen estrictamente.
5. ** Programación Dinámica en el DAG** – Contar maneras de alcanzar el fregadero de cada nodo.

■ **Key takeaway**: *Short‐est-distance → DAG → DP. *

-...

##### 3. Casos de borde " Cascadas comunes

Escenario Silencioso Por qué importa
Silencio...
Silencio Múltiples bordes entre el mismo par Silencio Dijkstra debe considerar el peso más pequeño tención Uso lista de adyacencia; mantener todos los bordes. Silencio
TENIENDO `dist(u)` y `dist(v)` Silencio No pueden ser parte de una senda restringida TENIDO Saltar tales bordes en DP. Silencio
Los bordes de peso cero Silencio Dijkstra todavía funciona (los pesos positivos están bien) Silencio Uso `long' para distancias. Silencio
Silencio Gran respuesta – necesidad modulo tención Prevent overflow tención Siempre mod después de cada adición. Silencio

-...

##### 4. Algoritm detallado

1. **Run Dijkstra de nodo *n***
- Complejidad: `O(n+m) log n) `
- Almacene `dist[1...n]` (long/64‐bit para evitar el desbordamiento).

2. **Build the DAG**
- Por cada borde no dirigido `(u,v,w)`:
* If `dist[u] ⇩ dist[v] → añadir borde dirigido `u → v`*
* If `dist[v] ⇩ dist[u] → añadir borde dirigido `v → u`*
*Si `dist[u] == dist[v]` → ningún borde dirigido (no se puede utilizar). *

3. **DP on the DAG**
- `ways[n] = 1`.
- Nodos de proceso en orden ascendente de `dist`** (orden totológico).
- Por nodo `u`:
`ways[u] = Governing ways[v]` sobre todos los bordes restringidos salientes.
- Regresa por ahí.

El DAG asegura que cuando procesamos un nodo, todos los nodos que señala que ya han sido procesados.

-...

##### 5. Producción Código listo (Java, Python, C++)

(Ver la sección del código anterior – copy‐paste listo, completamente comentado, y testado de batalla).

■ *Tip for interviewers*: Mostrar la lógica primero, luego presentar el código esqueleto. Muestra tanto la comprensión como la aplicación limpia.

-...

##### 6. Análisis de la complejidad

Silencio Silencio
Silencio...
Silencio Dijkstra Silencioso `O(n+m) log n)` Silencio
Silencioso Edificio DAG Silencioso `O(m)` Silencio
Silencio DP traversal Silencioso `O(n+m)` Silencio
tención **Total** Silencioso `O(n+m) log n)` tiempo, `O(n+m)` memoria Silencio

Para `n = 20 000` y `m = 200 000`, esto encaja cómodamente en los límites de tiempo de LeetCode y cualquier plataforma de entrevista.

-...

##### 7. Bien / mal / Ugly

Silencio Lo que es bueno para vivir mal para siempre
Silencio------------Prince------
Silencio **Bueno** Silencio • Separación clara de las preocupaciones (Dijkstra + DP). Reutilización de la lista de adyacency para ambos pases.
TEN **Bad** Silencio • La profundidad de la recuperación puede alcanzar los límites de recursión en Python. TEN • Usar DP iterativo o aumentar la pila de recursión.
Silencio **Ugly** Silencio • Algunas soluciones intentan realizar DFS sin memoización en el DAG, lo que lleva a tiempo exponencial. Silencio • Evitar. Silencio • Pre-computar un orden topológico clasificando `dist` es simple y evita el flujo de la pila de recursión. Silencio

-...

##### 8. Variaciones " Extensiones

Silencioso Variación Silencioso Cómo adaptarse
Silencio--------------
Silencioso *Pasajes en los que `dist(zi) >= dist(zi+1)`* Silencio Eliminar la desigualdad estricta; todavía un DAG. Silencio
tención *La gracia se dirige originalmente* Silencio Mantener los bordes dirigidos que satisfacen la desigualdad. Silencio
*Los pesos pueden ser negativos pero no ciclos negativos* Silencio Dijkstra ya no funciona; use Bellman‐Ford ford for `dist`. La complejidad se convierte en `O(nm)`. Silencio
Silencio *Large `n` hasta 105, `m` hasta 5·105* TENIDO El mismo algoritmo funciona; use rápido I/O en C++/Java.

-...

##### 9. Estrategia de entrevistas

1. **Clarificar el requisito de “disminución limitada”** – Algunos candidatos lo malinterpretan como “no creciente. ”
2. **Explicar la formación de DAG** – Visualizar el mapa de altura.
3. **La complejidad del tiempo de meditación frente a frente** – Mostrar que has considerado los límites.
4. **Discuss memoization vs. topological DP** – Highlight trade‐offs.
5. **Hablar sobre aritmética modular** – Muchos entrevistadores prueban errores por uno en el manejo del modulo.

-...

##### 10. Recursos prácticos

- **LeetCode**: 1786 – caminos restringidos, 1785 – Número de caminos buenos, 1237 – Conde Sub Islas.
- **Libros**: *“Elementos de las entrevistas de programación – Gráfico”*, *“Introducción a Algoritmos (CLRS) – Senderos más cortos”*.
- **Cortes**: *“ Algoritmos Gráfico”* en Coursera, *“Programación Dinámica”* en Udemy.
LeetCode Gym, Interviewing.io, Pramp.

-...

##### 🎯 Final Take‐away

■ *“La mejor manera de asar un problema de gráfico LeetCode es dividirlo en un subproblema clásico de corto camino seguido por un DP DAG.”*

Con los fragmentos de código arriba, usted puede:

- **Explicar la solución claramente** durante una entrevista de codificación en vivo.
- **Demonstrate production‐ready knowledge** presentando código limpio, bien comunicado en Java, Python, o C++.
- **Mostrar profundidad de comprensión** discutiendo casos de borde, complejidad y estrategias de entrevista.

Buena suerte – estás un paso más cerca de aterrizar ese *sueño trabajo*! 🚀

-...

### 📌 SEO Tags

`LeetCode 1786`, `Número de caminos restringidos ' , ` algoritmo gráfico ' , `Dijkstra ' , `programación dinamica ' , `entrevista de codificación ' , `entrevista de ingenieros de software ' , ` Solución de Palestina ' , `Convención de entrevista ' , ' .