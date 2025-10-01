-...
Título: LeetCode 2714. Encontrar el camino más corto con K Hops -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. El problema en pocas palabras

■ **LeetCode 2714 – “Encontrar el camino más corto con K Hops”**
■ Se le da un gráfico conectado, no dirigido, ponderado con `n` vertices (0-indexed).
■ Cada borde tiene un peso positivo `w`.
■ Se suministran dos vértices distintos `s ' y `d ' , y se puede **zero-out en la mayoría de los bordes `k'** (es decir, cambiar su peso a 0).
■ ¿Cuál es el peso total mínimo posible de un camino de `s` a `d` después de que usted ha aplicado a `k` "libres de saltos"?

`` `
No se entiende por 500
edges.length
w
k
`` `

La entrada garantiza que el gráfico está conectado, no tiene acoplamientos propios, y no hay bordes duplicados.

-...

## 2. Por qué un simple Dijkstra no lo corta

Si sólo pudieras **skip** bordes pero **no** alterarlos, un Dijkstra normal encontraría el camino más bajo ponderado.
En este problema, usted puede *reemplazar* el peso de hasta 'k' bordes con `0`.
Usted debe decidir *que* bordes a cero hacia fuera y *donde* en el camino que lo hace – la elección se une al camino mismo.

Eso significa que el estado del algoritmo ya no es “justo el vértice”; también necesita recordar cuántas mangueras gratuitas ya has utilizado.
Se trata de un patrón clásico “DP + Dijkstra” (o “multi‐state Dijkstra”).

-...

## 3. La solución óptima

### 3.1 Idea

Trate a cada par
`` `
(state) = (vertex, usedHops)
`` `
como nodo en un gráfico ** más grande, virtual**.
De un estado `(u, h)` usted puede:

Silencio Acción Silencio Nuevo estado Silencio Edge cost Silencio
Silencio--------------------------------
Silencioso borde `(u, v, w)` **normalmente**
Silencioso borde `(u, v, w)` **con un hop** Silencio `(v, h+1)` Silencio `0` (sólo si `h < k`)

Ejecute Dijkstra ordinario sobre estos estados.
La primera vez que apareces un estado cuyo vértice es `d` tienes la respuesta óptima, ya que la propiedad de Dijkstra "primera vista a la destilación" tiene en este gráfico ampliado también.

#### 3.2 Correctness proof sketch

1. **Todas las vías viables están representadas** –
Cada camino en el gráfico original se puede mapear a un camino en el gráfico ampliado al decidir por cada borde si se utiliza con un tubo o no.
El número de aristas utilizados nunca supera `k` porque nunca pasamos a un estado con `h > k`.

2. **Optimality kept** –
El algoritmo de Dijkstra garantiza que la primera vez que un estado se retira de la cola prioritaria tiene el coste acumulado mínimo posible de la fuente.
Por lo tanto, cuando nos encontramos por primera vez con un estado con el vértice `d`, su costo es el mínimo posible entre *todos* caminos que respetan el límite de salto.

3. **No existe un camino más corto*
Supongamos que existió un mejor camino hacia `d`. Correspondería a un estado `(d, h')` con un menor costo que Dijkstra debería haber eliminado antes, contradiciendo la propiedad del algoritmo.

De ahí que el algoritmo devuelve la distancia más corta exacta.

#### 3.3 Complexity

`` `
Número de estados : n * (k+1) (en la mayoría de 500 * 501 Ω 250k)
Transiciones por estado : grado(u) (≤ n-1)
Bordes totales en gráfico virtual : O(k+1) * m)
`` `

Dijkstra funciona en
`` `
O(n*(k+1) + (k+1)*m) log(n*(k+1)) )
`` `
Con los límites dados esto está muy por debajo de un segundo en todos los idiomas principales.

Espacio: `O(n*(k+1))` para la distancia / tablas visitadas más el gráfico original `O(m)`.

-...

## 4. Implementaciones de referencia

A continuación se encuentran soluciones limpias y de producción en **Java**, **Python**, y **C+**.
Los tres usan el mismo patrón estatal de Dijkstra descrito anteriormente.

-...

### 4.1 Java (estilo LeetCode)

``java
importar java.util*;

*
* LeetCode 2714 – Encontrar el camino más corto con K Hops
*/
Solución de la clase pública {}

--------- Ayudante de Gráficos...
[] []] []] [construirGraph(int n, int[][] edges] {
Lista obtenida[]]] g = nuevo ArrayList[n];
para (int i = 0; i) no; ++i) g[i] = nuevo ArrayList fiel();
para (int[] e : bordes) {
int u = e[0], v = e[1], w = e[2];
g[u].add(new int[]{v, w});
g[v].add(new int[]{u, w});
}
retorno g;
}

--------- Estado para la cola de prioridad...
Clase privada Estado implementa Comparable Estado {
int vertex, utilizado;
descomposición larga;

Estado(int vertex, int used, long dist) {
este.vertex = vértice;
esto.utilizado = usado;
esto.dist = dist;
}

@Override
public int compare To(State other) {
volver Long.compare (este.dist, otro.dist);
}
}

--------- Main Dijkstra --------
public int shortestPathWithHops(int n, int[] bordes, int s, int d, int k) {
Lista obtenida[]]] g = buildGraph(n, edges);

// distance[vertex][hopsUsed]
long[][] dist = new long[n][k + 1];
para (long[] fila : dist) Arrays.fill(row, Long.MAX_VALUE);

PrioridadPregunta relativa Estado titular pq = nueva PrioridadPregunta relativa();
[s] [0] = 0;
pq.offer(new State(s, 0, 0));

mientras (pq.isEmpty()) {
State cur = pq.poll();

si (cur.vertex == d) retorno (int) cur.dist; // primera llegada es óptima

si (cur.dist != dist[cur.vertex] [cur.used]) continúan; // anticuado

para (int[] e : g[cur.vertex]) {}
int nb = e[0];
int w = e[1];

// 1) transversal normalmente
si (cur.dist + w) no [nb] [cur.used]) {}
dist[nb] [cur.used] = cur.dist + w;
pq.offer(nuevo Estado(nb, cur.used, dist[nb][cur.used]));
}

// 2) utilizar un hop (si todavía tenemos hops izquierda)
si (cur.used ■ k " curva.dist " )
dist[nb] [cur.used + 1] = cur.dist;
pq.offer(new State(nb, cur.used + 1, dist[nb][cur.used + 1]));
}
}
}

// grafito está garantizado conectado, por lo que esta línea nunca llegó
retorno -1;
}
}
`` `

-...

### 4.2 Python 3 (estilo LeetCode)

``python
importación heapq
de la importación Lista

Solución de clase:
def más corto PathWithHops(
auto, n: int, edges: List[List[int],
s: int, d: int, k: int
) int:
# build adjacency list
graph = [[] for _ in range(n)]
para u, v, w en los bordes:
graph[u].append(v, w))
graph[v].append(u, w))

INF = 10**18
dist = [[INF] * (k +1) for _ in range(n)]
dist[s][0] = 0

# (dist, vertex, hopsUsed)
pq = [(0, s, 0)]
mientras pq:
cur, u, utilizado = heapq.heappop(pq)
si cur != dist[u][used]:
continuar # entrada de escalera

si U == d:
regreso cur # primera visita es óptima

for v, w in graph[u]:
Traversal normal
si cur + w se hizo dist[v] [utilizado]:
dist[v][used] = cur + w
heapq.heappush(pq, (dist[v][used], v, used))

# Hop (si está permitido)
si se utiliza не k y cur нерт [v] [utilizado + 1]:
dist[v][used + 1] = cur
heapq.heappush(pq, (cur, v, utilizado + 1))

retorno -1
`` `

-...

#### 4.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
struct Edge { int to; int w; };
struct State {}
int v, utilizado; largo tiempo dist;
(Estado const limitado o) const { return dist √ o.dist; } // min‐heap
};

más corto PathWithHops(int n, vector identificadovector identificadoint ánimo limitado bordes,
int s, int d, int k) {
vector realizador: Edge confianza g(n);
para (auto &e: edges) {}
int u = e[0], v = e[1], w = e[2];
g[u].push_back({v,w});
g[v].push_back({u,w});
}

const long INF = 4e18;
vector se llevó a cabo largo tiempo contactos dist(n, vector llevado a cabo largo tiempo(k+1, INF)
priority_queue correspondióEstado apropiado pq;

[s] [0] = 0;
pq.push({s, 0, 0});

mientras (pq.empty()) {
State cur = pq.top(); pq.pop();
si (cur.v == d) retorno (int)cur.dist; // óptimo cuando se saltó primero

si (cur.dist != dist[cur.v] [cur.used]) continúan; // stale

para (auto &e : g[cur.v]) {}
int nb = e.to, w = e.w;

// Traversal normal
si (cur.dist + w) no [nb] [cur.used]) {}
dist[nb] [cur.used] = cur.dist + w;
pq.push({nb, cur.used, dist[nb][cur.used]});
}

// hop
si (cur.used ■ k " curva.dist " )
dist[nb][cur.used+1] = cur.dist;
pq.push({nb, cur.used+1, dist[nb][cur.used+1]});
}
}
}
retorno -1; // no alcanzable – el gráfico está conectado, así que nunca sucede
}
};
`` `

-...

## 5. “Bueno, malo” – Lo que los entrevistadores realmente se preocupan

Silencio Fase actual ¿Qué candidato debería hacer? Lo que un candidato **should not** hace Silencio
Silencio...
Silencio **Bueno** Silencio *Declarante Dijkstra* – conciso, utiliza sólo una sola cola de prioridad, O(k+1)n memoria. Silencio Silencio
Silencio **Bad** Silencio BFS o DP que iterates over all `k`‐combinations of edges (exponential). Silencio
Silencio **Ingeniería instantánea: escribir una clase de gráfica personalizada que filtra la memoria, o mezclar BFS + DFS incorrectamente, o ignorar la propiedad “primero-visit‐to-destinación”.

**Por qué este patrón es de entrevista amigable* *
- Muestra una comprensión clara de **Dijkstra**, **DP**, y ** compresión del estado**.
- Prueba que puede razonar sobre * problemas de estado aumentado* – un tema de entrevista frecuente.
- La solución es **linear en `k`**: se puede explicar fácilmente “si `k ' fueron 0 sólo sería Dijkstra”.
- El código está limpio, utiliza contenedores de biblioteca estándar, y es lo suficientemente corto para caber en una pizarra.

-...

## 6. Prueba tu solución

Silencio Casos pendientes Silencio conducta esperada
Silencio...
TENIDO `k = 0` – no pasatiempos TENIDO Sendero más corto. Silencio
Silencio `k = n-1` – usted puede cero hacia fuera *cualquier borde La respuesta siempre será el límite mínimo de peso en un camino *cualquier*; Dijkstra todavía funciona. Silencio
Silencio Gráfico con un solo borde entre `s ' y `d` ANTE O utilice el tubo (costo 0) o mantenga el peso. Silencio
TEN Múltiples trayectorias de igual peso TEN Dijkstra elegirá automáticamente la que tiene el uso más barato de la manguera. Silencio
Silencio `n = 1` es imposible porque `s` y `d` deben ser distintos - la declaración garantiza `n ≥ 2`. Silencio

Use las pruebas de muestra de LeetCode más algunas personalizadas:

``python
# Python snippet
print(Solution().shortestPathWithHops()
5,
[[0,1,5],[1,2,3],[0,2,10],[2,3,1],[3,4,4]],
0, 4, 2
) # Esperado: 0 (puntos 0-1 y 2-3)
`` `

-...

## 7. artículo de blog amigable SEO

A continuación se muestra un artículo de longitud completa que puede copiar‐paste en un correo mediano, Dev.to, o su propio blog.
Siéntase libre de retocar el título, agregue su propia voz, o suelte las etiquetas `#` que funcionan con la mayoría de las plataformas de blogging.

-...

### 🔍 “Find Shortest Path with K Hops” – A LeetCode 2714 Deep Dive (Graph + DP)

■ **Keywords**: *LeetCode 2714*, *Find Shortest Path with K Hops*, *graph algoritmo interview*, *Dijkstra stateful*, *software engineer interview prep*, *free hops algoritmo*, *diseños de programación dinamica + Dijkstra*, *network latency optimization*, *edge Zeroing*, *graph theory data structures*

-...

##### 1. Por qué este problema es una “gold‐mine” para los entrevistadores

- ** Fundamentos gráficos** - bordes, pesos, conectividad.
**Advanced Dijkstra** – relajación multiestado, cola prioritaria.
- Programación Dinámica en el gráfico** - la dimensión de "Hops usados".
- ** Análisis de complejidad** – tiempo de funcionamiento basado en registros, uso de memoria ajustado.
- ¿Qué pasa si golpeas el límite de la manguera? ¿Y si todos los bordes son cero?

Estos temas surgen en entrevistas *software‐engineer* en Google, Microsoft, Amazon, y muchos equipos de información-ciencia.

-...

##### 2. Recaptación de problemas (de LeetCode)

■ Dado un gráfico ponderado, dos vértices distintos `s` y `d`, y un entero `k`, cero-out * en la mayoría* `k` bordes.
■ Cumplir el peso total mínimo de cualquier camino de `s` a `d` después de la operación.

Constraints garantiza un gráfico denso con hasta 10 000 bordes y 500 vértices – un lugar dulce para Dijkstra.

-...

##### 3. “Bien” – El estado limpio Dijkstra

1. **State = (vertex, hopsUsed)* *
Cada estado es un nodo en un gráfico virtual.
2. **Dos relajacións** – borde normal vs borde de salto (costo 0).
3. **La cola de la prioridad** – `min-heap` ordenado por la distancia acumulada.
4. **Early exit** – la primera vez que aparece un estado cuyo vértice es `d` es la respuesta óptima.

*Por qué es bueno*

- **Time‐optimal**: `O((k+1)·(n+m) log(n(k+1)) ' .
- **Espacio-eficiente**: `O(n(k+1))' matriz de distancia.
- ** Fácil de entender** en una pizarra: “Acabamos de añadir una dimensión más”.

-...

##### 4. “Bad” – Por qué fallan las soluciones ingenuas

Por qué es lento o incorrecto
Silencio----------------
tención **DFS + fuerza bruta** – probar todas las combinaciones de 'k' hops (elegir 'k' bordes fuera de `m`) Tiempo exponencial, imposible para `m = 104`. Silencio
TEN **DP en lista de bordes** – computar la mejor distancia para cada vértice y cada aro cuenta en un bucle anidado TEN todavía `O(n2k)` que está bien, pero no puede garantizar que usted está explorando bordes con el costo más barato primero; el algoritmo puede volver a ver estados innecesariamente. Silencio
Silencio **BFS en el gráfico ampliado pero sin cola prioritaria** Silencio BFS asume pesos unitarios; aquí los costos del borde varían ampliamente (`w` hasta 106). Silencio

-...

##### 5. “Ugly” – Lo que debes evitar*

- filtraciones de memoria**: asignación de `vector identificadovectorado dentro de un bucle, olvidando reasentarse.
- **Custom priority queue** that mis-orders elements (e.g., using a `max‐heap` by accident).
- **Mixing data structures** (DFS stack + Dijkstra PQ) en una solución – conduce a un razonamiento confuso en el tablero.
- **Principar a cada estado** para depurar – retrasa la entrevista y muestra falta de enfoque.

El viaje: mantenlo sencillo. Use contenedores estándar de lenguaje; no sobre-optimice antes de conocer la estructura del problema.

-...

##### 6. Caminata de código (por ejemplo, Python)

``python
Solución de clase:
def más corto PathWithHops(self, n, edges, s, d, k):
graph = [[] for _ in range(n)]
para u, v, w en los bordes:
graph[u].append(v, w))
graph[v].append(u, w))

INF = 10**18
dist = [[INF]*(k+1) for _ in range(n)]
dist[s][0] = 0
pq = [(0, s, 0)] # (dist, vertex, hops)

mientras pq:
cur, u, utilizado = heapq.heappop(pq)
si cur != dist[u][used]:
continuar
si U == d:
Retorno
for v, w in graph[u]:
# Normal
si cur + w se hizo dist[v] [utilizado]:
dist[v][used] = cur + w
heapq.heappush(pq, (dist[v][used], v, used))
# Hop
si se utiliza не k y cur нерит [v] [utilizado+1]:
dist[v][used+1] = cur
heapq.heappush(pq, (cur, v, used+1))
retorno -1
`` `

Siéntase libre de pegar esto en su IDE y ejecutarlo en las pruebas de muestra de LeetCode.

-...

##### 6. Despliegue " paralelos del mundo real "

Zero‐ing an edge is akin to **caching** or **reducing latency** in a network: you're free to “bypass” certain costly links.
El patrón del algoritmo es útil para:

- **Optimizing routing tables** in distributed systems.
- ** Simulation budgeted upgrades** in infrastructure (e.g., ¿cuántos cables puede actualizar para reducir la latencia total?).

-...

##### 7. Takeaway

- ** El Estado Dijkstra** es una solución concisa y poderosa.
- **Lista de teclado**: explicar la dimensión añadida y las dos relajacións.
- **Entrevistas**: hablar de por qué no puede utilizar BFS y por qué la cola prioritaria garantiza la óptimaidad.
- **Mostrar el análisis**: tiempo de ejecución basado en registros y cómo lo derivaste.

Dale una oportunidad en tu próxima entrevista – impresionarás con *corrección* y *claridad*.

-...

##### 📚 Más lectura

- *Introducción a Algoritmos* – algoritmo de Dijkstra.
- *Algorithms (CLRS)* – DP en gráficos, compresión estatal.
- * Programación competitiva 3* – trucos avanzados de cortocircuito.

¡Feliz codificación, y que tus caminos sean siempre los más cortos! 🚀

-...

### 🎤 Bonus: Agregar un toque personal

- Agregue una anécdota corta de su propia experiencia abordando un problema del gráfico LeetCode.
- Comparta una captura de su código en una pizarra.
- Fin con una llamada a acción: ¿Tienes un truco para un problema similar? ¡Tíralo en los comentarios! ”

-...

**Disfrute de su blog,** y la mejor suerte con esas entrevistas de codificación! 🚀

-...

Eso es todo – una explicación lista para compartir, entrevista-ready de LeetCode 2714 “Find Shortest Path with K Hops”, junto con código limpio en pseudocode estilo Java (Java omitted for brevity), y un artículo completo para mostrar su experiencia a los administradores de contratación. ¡Feliz codificación!