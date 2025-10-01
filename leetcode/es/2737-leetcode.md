-...
Título: LeetCode 2737. Encontrar el Nodo marcado más cercano -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Find the Closest Marked Node (LeetCode 2737) – A Complete Guide
**Keywords:** Encuentra el Nodo marcado más cercano, LeetCode 2737, algoritmo Dijkstra, ruta más corta, traversal de gráficos, solución Java, solución Python, solución C++, codificación de entrevistas, entrevista de trabajo, entrevista de codificación

-...

## 🚀 1. Lo que el problema es preguntar

■ * Objetivo*
■ Dado un gráfico con peso directo ** con n ' nodos (`0 ... n‐1`) y una lista de bordes `edges = [u, v, w] ' (edge from `u` to `v` with weight `w '), un nodo de inicio `s ' y una serie de nódos ** marcados**, devuelve la distancia **minimo** de `s` a cualquier nodo marcado.
■ Si no hay un nodo marcado es alcanzable, devuelve `-1`.

### Constraints Recap
TENIDO ANTERIOR TERRITORIOS TENIDO
Silencio...
TENIDA `n` Silencio 2 - 500 ANTE
TENIDA `edges.length` ANTERIOR 1 - 104
TENIDA `edges[i][2]
Silencio `marked.length` Silencio 1 – n‐1
Silencio No auto-ops; los bordes repetidos posibles
Silencio Todos los pesos son positivos

-...

Por qué Dijkstra Es la Fit Natural

* **Single‐source shortest path** – Necesitamos el camino más corto **de `s`** a *cualquier nodo marcado.
* **Positive weights only** – El algoritmo de Dijkstra garantiza la óptimabilidad cuando todos los pesos del borde son no negativos.
* Early-stop** – Podemos parar tan pronto como nos encontramos con un nodo marcado de la cola de prioridad – ya estamos en el *closest*.

-...

## 🏗 3. Algoritm Sinopsis

1. **Construir una lista de adyacencia** de la lista de bordes.
`adj[u]` → lista de `(v, w)` pares.
2. **Mantenga un min-heap (cuarta de prioridad)** de `(distancia, nodo)`.
3. **Mantenga un 'dist[]` array** (inicialmente `∞') y un 'visited[]` array.
4. **Push** `(0, s)` en la cola, establece `dist[s] = 0`.
5. Mientras que la cola no está vacía:
* Pop the smallest distance node `u`.
* If `u` is already visited, skip.
* Mark `u` como fue visitado.
* **Si `u` es un nodo marcado → retorno `dist[u].**
* Relajar todos los bordes salientes `u → v`:
``text
si dist[u] + w >
dist[v] = dist[u] + w
push (dist[v], v)
`` `
6. Si el bucle termina sin golpear un nodo marcado → retorno `-1`.

El algoritmo funciona en **O(n + m) log n)** tiempo y **O(n + m)** espacio (con `m = edges.length`).

-...

## ⚙ 4. El Bien, el Mal, y el Ugly

Silencio Silencio
Silencio------------Prince------
Silencio ** Sonido algorítmico** Silencio TENIENDO Dijkstra garantiza la optimización con pesos positivos. TEN ❌ No es adecuado para pesos negativos – necesitaría Bellman‐Ford o SPFA. Silencio  Los bordes repetidos pueden inflar el montón innecesariamente, pero con `m ≤ 104` es insignificante. Silencio
Silencio **Early exit** Silencio ف Stops tan pronto como se resuelve el nodo marcado más cercano, ahorro de tiempo. ❌ Requires careful visited check – if omitted you may return a sub-optimal distance. Silencio 😠 Un buggy visitado array (por ejemplo, `dist` solamente) puede causar resultados incorrectos. Silencio
Silencio ** Pieza de memoria** Silencio TENIDO Sólo tiendas adjacency list, distance and visited arrays. TEN ❌ Para gráficos muy densos el montón puede crecer grande. TEN  Sobre-engineering a binario heap wrapper when the STL/collections library is enough. Silencio

-...

## 📚 5. Implementaciones de código

A continuación se muestran francos limpios, listos para la producción para **Java**, **Python**, y **C+**. Todos utilizan el mismo enfoque descrito anteriormente.

■ **Consejo:** En todas las soluciones la salida temprana (`si marcadaSet.contains(node)`) garantiza que siempre devolvemos la distancia mínima a cualquier nodo marcado.

### 5.1 Java (Java 11+)

``java
importar java.util*;

Solución de la clase pública {}
mínimo público Distancia (int n, Lista) bordes, int s, int[] marcados) {
// 1. Conjunto de nodos marcados para la búsqueda O(1)
Establecer:Integer título marcadoSet = nuevo HashSet fiel();
for (int node : marked) markedSet.add(node);

// 2. Lista de adyacencia
Lista realizadaLista realizada[]] > adj = nuevo ArrayList recomendado();
para (int i = 0; i < n; i++) adj.add(new ArrayList correctamente());
para (Lista realizadaInteger título e : bordes) {
int u = e.get(0), v = e.get(1), w = e.get(2);
adj.get(u).add(new int[]{v, w});
}

// 3. Distancias + visitadas
int[] dist = nuevo int[n];
boolean[] visited = new boolean[n];
Arrays.fill(dist, Integer. MAX_VALUE);
dist[s] = 0;

// 4. Lugar de prioridad de los minutos
PriorityQueue madeint[] conviene pq = new PriorityQueue Curso(Comparator.comparingInt(a - título a[0]));
pq.offer(new int[]{0, s});

// 5. Dijkstra con salida temprana
mientras (pq.isEmpty()) {
int[] cur = pq.poll();
int d = cur[0], u = cur[1];
si (visited[u]) continúan;
visitado[u] = verdadero;
si (marcadoSet.contains(u)) devuelve dist[u];
para (int[] nb : adj.get(u) {
int v = nb[0], w = nb[1];
si (dist[u] + w ' ) {}
dist[v] = dist[u] + w;
pq.offer(new int[]{dist[v], v});
}
}
}
retorno -1; // no marcado nodo alcanzable
}
}
`` `

### 5.2 Python 3

``python
importación heapq
de la importación Lista, Tuple

Solución de clase:
mínimo Distancia (auto, n: int, edges: List[List[int],
s: int, marked: List[int] int:
adj = [[] for _ in range(n)]
para u, v, w en los bordes:
adj[u].append(v, w))

marked_set = set(marked)
* n
visitado = [False] * n
dist[s] = 0
[(0, s)]

Mientras salta:
d, u = heapq.heappop(heap)
si es visitado[u]:
continuar
visitado[u] = Verdadero
si u en mark_set:
Retorno[u]
for v, w in adj[u]:
si dist[u] + w >
dist[v] = dist[u] + w
heapq.heappush(heap, (dist[v], v)
retorno -1
`` `

### 5.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
mínimo Distancia(inc. n, vector asignadovector identificadoint
int s, vector identificadoint
// Construir la lista de adjacency
vector realizador obtenidospair obtenidosint,int títulos
para (auto pulsa e : bordes)
adj[e[0].emplace_back(e[1], e[2]);

unordered_setSet(marked.begin(), marked.end());

vector llevado a cabo largo tiempo dist(n, LLONG_MAX);
vector asignadobool confianza visitado(n, false);
dist[s] = 0;

usando P = par realizado largo, injerto;
priority_queue obtenidosP, vector asignadoP título, mayor especificadoP título
pq.emplace(0, s);

mientras (pq.empty()) {
auto [d, u] = pq.top(); pq.pop();
si (visited[u]) continúan;
visitado[u] = verdadero;
si (markSet.count(u)) devuelve dist[u];

para (auto [v,w] : adj[u]) {}
si (dist[u] + w ' ) {}
dist[v] = dist[u] + w;
pq.emplace(dist[v], v);
}
}
}
retorno -1;
}
};
`` `

-...

## 📈 6. Análisis de complejidad

TEN TERMIN TENIDO Tiempo ANTERIENTE Espacio ANTE
Silencio----------Prince------
Silencio **El mejor maletín** (nodo marcado es un vecino directo de `s`) Silencio O(1) – pop `s ' e inmediatamente la salida Silencio O(n + m)
Silencio **El peor maletín** (no marcado node alcanzable) Silencio O(n + m) log n) Silencio O(n + m) Silencio
Silencio **Práctico** (disposiciones dadas) TENIDO Lo suficientemente rápido para todos los casos de prueba TENIDO Única lista de adyacencia + montón ANTE

-...

## 🛠ר 6. Edge‐ Lista de verificación de casos

Silencio Caso Edge Silencioso Qué ver para Silencio
Silencio...
Silencio **Finalidades mínimas entre los mismos nodos** Silencio Todos los bordes están relajados – los duplicados están bien; el tamaño del salto puede aumentar ligeramente. Silencio
Silencio **El nodo inicial `s` ya está marcado** Silencio El algoritmo estallará inmediatamente `(0, s)` y devolverá `0`. Silencio
Silencio **Ningún nodo marcado alcanzable** Silencio La cola vaciará; devuelve `-1`. Silencio
Silencio **Pesas altas (hasta 106)** Silencio Uso `long' en C++ o `long` en Java para evitar el desbordamiento. Silencio
Silencio **Graph desconectado** Silencio La salida temprana no activará; asegurar el retorno final `-1`. Silencio

-...

## 🔄 7. Variaciones " Extensiones

Silencioso Variación
Silencio...
Silencio **Todos los bordes no dirigidos** Silencio Construir la lista de adyacencia en ambas direcciones – Dijkstra todavía se aplica. Silencio
Silencio **Pesas negativas permitidas** tención Switch to **Bellman‐Ford** or **SPFA**; salida temprana posible pero más lenta. Silencio
Silencio **Nodos de origen múltiple** Silencio Run Dijkstra de cada fuente o uso **multi‐source Dijkstra** insertando todas las fuentes con distancia 0 en el montón. Silencio
Silencio ** Gráfico ponderado con bordes de peso cero** Silencio Dijkstra funciona bien mientras no existan ciclos negativos. Silencio
Silencio ** Objetivo: suma de distancias a todos los nodos marcados** Silencio Después de resolver todos los nodos, suma `dist[node]` para todo `nodo` en marcado conjunto. Silencio

-...

## 🎯 8. Por qué dominar este problema ayuda a su búsqueda de empleo

1. **Muestra pensamiento gráfico-teorético** – Los entrevistadores les encanta ver aplicar el algoritmo adecuado (Dijkstra vs. Floyd‐Warshall vs. BFS).
2. **Highlights early‐exit optimization** – Indica que puedes pensar en poda y rendimiento.
3. **Demuestra estilo de codificación limpio** – Los tres fragmentos de lenguaje utilizan estructuras de datos concisas y idiomáticas (PrioridadQueue`, `heapq`, `std::priority_queue`).
4. **Versatilidad** – Usted puede pivotar desde Java → Python → C++ en la misma entrevista, demostrando el agnosticismo del lenguaje.
5. ** Ejemplo real LeetCode** – 2737 aparece en el conjunto de dificultades “Graph”; resolverlo indica la disponibilidad para los problemas “Graph” en las entrevistas de codificación.

-...

## 📢 9. Final Takeaway

2737. Encuentra el Nodo más cercano marcado es un problema *clásico* de un solo código que mapea perfectamente al algoritmo de Dijkstra con una salida temprana. Dominar esta solución:

* Te da una plantilla **reutilizable** para cualquier pregunta de entrevista más corta.
* Te muestra cómo **optimizar** parando en el primer nodo marcado.
* Construye la confianza en el manejo de casos **edge** como bordes repetidos, objetivos inalcanzables y pesos grandes.

La próxima vez que golpeó un problema de LeetCode “Graph” en una entrevista, recuerde el truco de Dijkstra temprano – es su boleto para limpiar, eficiente y código de entrevista.

-...

## 📄 10. SEO Meta‐ Datos (Opcional para hospedaje de blogs)

``html
< > > > > > > > >
"Solve LeetCode 2737: Encuentra el Nodo marcado más cercano con Dijkstra. Lea Java, Python & C++ soluciones, tiempo & complejidad del espacio, y consejos de entrevista.
Identificar el nombre="palabras clave" contenido="Encuentra el Nodo marcado más cercano, LeetCode 2737, algoritmo Dijkstra, traversal gráfico, solución Java, solución Python, solución C+++, camino más corto, codificación de entrevistas de trabajo"
`` `

¡Feliz codificación y buena suerte aterrizando esa entrevista tecnológica!