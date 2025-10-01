-...
Título: LeetCode 3313. Encontrar los últimos nodos marcados en el árbol -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 3313. Encontrar los últimos nodos marcados en el árbol
■ **Hard** – LeetCode

■ **Keywords**: *Diámetro del panel*, *BFS*, *FDS*, *Shortest Distance*, *Proceso de marca*, *LeetCode 3313*, *Java*, *Python*, *C++*, *Diseño de algorithm*, *Entrevista Prep*

-...

Problema Recap

Se le da un árbol no dirigido con nodos (0 ... n‐1).
At time `t = 0` you mark a single node `i`.
Cada segundo se marcan todos *nodos no marcados* que tienen al menos un vecino marcado.

Para cada nodo inicial `i` salida **cualquier nodo** que se marca *último*.
Si hay dos nodos que están atados por última vez, usted puede devolver cualquiera de ellos.

`edges` es una lista de 'n-1' pares '[u, v]` describiendo el árbol.

`` `
Entrada: bordes = [[0,1],[0,2]]
Producto: [2,2,1]
`` `

-...

### 🧩 Por qué el Diámetro del Árbol ayuda

El proceso de marcado es equivalente a una “onda” que expande un borde por segundo del nodo inicial.
El último nodo a alcanzar es exactamente el que es *más lejos* desde el principio.

En un árbol, la distancia más lejana de cualquier nodo es siempre a uno de los dos *puntos de diámetro* (los dos extremos del camino más largo).
Por lo tanto, para cada nodo `i` sólo necesitamos saber cuál de los dos extremos de diámetro está más lejos de 'i'.
Ese fin está garantizado para ser un “último nodo marcado”.

-...

################################################################################################################################################################################################################################################################

TENIDO TENIDO ANTERIOR Lo que hace
Silencio...
Silencio • Silencio **Tiempo de trabajo** (`O(n)`) y espacio (`O(n)`). Silencio
Silencio • Silencio Trabaja para la máxima limitación (`n = 105`). Silencio
Silencio • Silencio No hay recursión pesada – utiliza BFS/DFS iterativa para evitar el desbordamiento de la pila. Silencio
Silencio • Silencio Muy clara lógica: diámetro → dos arrays de distancia → respuesta por nodo. Silencio

-...

### ⋅ Bad

ANTERIGEN ANTERIENTE Posibles trampas
Silencio.
Silencio • Silencio Si te olvidas de que el árbol es *indirecto* malinterpretarás el gráfico. Silencio
Silencio • Silencio Relying on recursion with deep > 104 puede estrellarse en algunos sistemas. Silencio
Silencio • Silencio Elegir el mal "tie-breaker" (por ejemplo, "punto2" cuando las distancias iguales) todavía puede satisfacer el problema, pero puede dar una respuesta diferente a la esperada por algunos arnés de prueba. Silencio
Silencio • Silencio Olvidar que la longitud de los bordes es `n‐1` podría llevar a un error fuera de cada uno en tamaños de array. Silencio

-...

#### 💥 Ugly

Silencio 💥 Silencio Cosas que pueden ser desordenadas
Silencio.
Silencio • Silencio Escribir tres implementaciones separadas de BFS/DFS para Java, Python y C++ conduce a la lógica duplicada. Silencio
Silencio • ← Mezclar índices de nodos basados en 0 y 1-basados en comentarios o nombres variables puede confundir a los usuarios. Silencio
Silencio • Silencio Sobre-ingenierar la solución (por ejemplo, usando Dijkstra o una cola prioritaria) aumenta innecesariamente la complejidad. Silencio

-...

## 📈 Algorithm Overview

1. **Construir la lista de adjacency** ( " Lista realizadaLista realizadaInteger título " en Java, `defaultdict(list) ' en Python, `vector seleccionadovector fielint ' en C++).
2. **Encontrar un punto final de diámetro (`punto1`)**: BFS/DFS del nodo 0 al nodo más lejano.
3. **Encuentra el otro punto final de diámetro (`punto2`)**: BFS/DFS desde `punto1`.
4. **Compute distance arrays**
* `dist1[i]` – distance from `point1` to node `i`.
* `dist2[i]` – distancia de `punto2` a nodo `i.
5. *Respuesta para nodo*
* If `dist1[i] √= dist2[i] → `point1` (ties arbitrarily).
* Else → `point2`.

Todas las carreras de BFS/DFS son lineales, por lo que el tiempo total `O(n)`.

-...

## 📊 Complexity Analysis

TENCIÓN TERRITOR TENIDA Cálculo
Silencio----------
Silencio **Hora** Silencioso `O(n)` – 4 traversales del árbol. Silencio
Silencio **Espacio** Silencioso `O(n)` – lista de adjacency + 2 arrays de distancia + cola/estar. Silencio

-...

## 🎯 Edge‐Case Checklist

Silencio Caso confidencialidad ¿Por qué importa?
Silencio...
Silencio `n = 2` Silencio Sólo un borde, ambos puntos de extremo de diámetro son los dos nodos. ← BFS devuelve correctamente el nodo más lejano. Silencio
Silencio Gráfico estrella (un centro, muchas hojas) Silencio Todas las hojas están a la distancia 1 del centro. Los puntos finales del diámetro son dos hojas; las distancias manejadas correctamente. Silencio
Silencio Árbol muy profundo (pata) Silencio La profundidad de la recuperación podría soplar la pila. Silencioso Ierative BFS/DFS utilizado. Silencio
← Los bordes Duplicados o auto-loops no permitidos por las restricciones del problema sino proteger contra el mal uso. No se necesitan cheques adicionales. Silencio

-...

## 🧑 💻

A continuación se encuentran soluciones limpias y de producción en **Java, Python y C++**.

■ **Tip** – Los tres usan BFS iterativa para seguridad y claridad.
**Hint** – Reemplazar `ArrayDeque` con una simple `int[]` cola si la memoria se convierte en una preocupación.

## Java (Java 17+)

``java
importar java.util*;

Clase Solución {
int estática privada[] bfs(Listecto gráfico, inicio int) {
int n = graph.length;
int[] dist = nuevo int[n];
Arrays.fill(dist, -1);
ArrayDeque se cumplióInteger confianza q = nuevo ArrayDeque corresponde();
q.add(start);
dist[start] = 0;
(!q.isEmpty()) {
int u = q.poll();
para (int v : graph[u]) {}
(dist[v] == -1) {
dist[v] = dist[u] + 1;
q.add(v);
}
}
}
de retorno;
}

privada estática int farthestNode(int[] dist) {
int node = 0, best = -1;
para (int i = 0; i)
si (dist[i]
mejor = dist[i];
nodo = i;
}
}
nodo de retorno;
}

int[] lastMarkedNodes(int[][] edges) {
int n = edges.length + 1;
@SuppressWarnings("unchecked")
Lista de datos gráfico = nueva lista[n];
para (int i = 0; i) no; i++) grafo[i] = nuevo ArrayList fiel();

para (int[] e : bordes) {
int u = e[0], v = e[1];
graph[u].add(v);
graph[v].add(u);
}

// 1er punto final
int[] dist0 = bfs(graph, 0);
int p1 = farthestNode(dist0);

// 2do punto final
int[] dist1 = bfs(graph, p1);
int p2 = farthestNode(dist1);

// Distancias del otro punto final
int[] dist2 = bfs(graph, p2);

int[] ans = nuevo int[n];
para (int i = 0; i)
as[i] = dist1[i] √= dist2[i] ? p1 : p2;
}
devolver los ans;
}
}
`` `

-...

### Python 3 (3.8+)

``python
de las colecciones importa
de la importación Lista

Solución de clase:
def _bfs(self, graph: List[List[int], start: int) - título List[int]:
n = len(graph)
[-1]
q = deque([start])
dist[start] = 0
mientras q:
u = q.popleft()
for v in graph[u]:
si se dist[v] == -1:
dist[v] = dist[u] + 1
q.append(v)
Retorno

def _farthest(self, dist: List[int] - int:
volver max(range(len(dist)), key=lambda i: dist[i])

def last MarkedNodes(self, edges: List[List[int]) - No. List[int]:
n = len(edges) + 1
graph = [[] for _ in range(n)]
para u, v en los bordes:
graph[u].append(v)
graph[v].append(u)

d0 = self._bfs(graph, 0)
p1 = self._farthest(d0)

d1 = self._bfs(graph, p1)
p2 = self._farthest(d1)

d2 = self._bfs(graph, p2)

volver [p1 si d1[i] √≥= d2[i] otro p2 para i en rango(n)]
`` `

-...

### C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vectorial identificador bfs(cont vector identificadovector seleccionador seleccionado) {
int n = g.size();
vector asignadoint -1);
queue indicaint
q.push(start);
dist[start] = 0;
(!q.empty()) {
int u = q.front(); q.pop();
para (int v : g[u]) {}
(dist[v] == -1) {
dist[v] = dist[u] + 1;
q.push(v);
}
}
}
de retorno;
}

int farthest(cont vector conectado d) {
int node = 0, best = -1;
para (int i = 0; i) ++i)
si (d[i]
nodo de retorno;
}

vector implicado últimoMarkedNodes(vector seleccionadovector identificadoint implicados iguales bordes) {}
int n = edges.size() + 1;
vector realizador:
para (auto golpe e : bordes) {
int u = e[0], v = e[1];
g[u].push_back(v);
g[v].push_back(u);
}

auto d0 = bfs(g, 0);
int p1 = farthest(d0);

auto d1 = bfs(g, p1);
int p2 = farthest(d1);

auto d2 = bfs(g, p2);

vector:
para (int i = 0; i)
as[i] = (d1[i] √= d2[i]) ? p1 : p2;
devolver los ans;
}
};
`` `

-...

Testing

Ejecute el siguiente arnés mínimo de prueba en cada idioma para verificar la corrección:

``java
int[][] edges = {0,1},{0,2};
int[] result = new Solution().lastMarkedNodes(edges);
System.out.println (Arrays.toString(resultar)); // [2, 2, 1]
`` `

``python
print(Solution().lastMarkedNodes([0,1],[0,2])) # [2, 2, 1]
`` `

``cpp
vector asignado a los bordes del título = {0,1},{0,2};
Sol de solución;
auto res = sol.lastMarkedNodes(edges);
para (int x : res) cout
`` `

-...

## 🚀 Interview‐Ready Takeaway

- ¿Qué? La ola alcanza los extremos de diámetro primero.
- **Implementación**: 4 BFS/DFS pasa → `O(n)` tiempo y espacio.
- **Idiomas**: Java, Python, C++ – todos comparten la misma lógica iterativa limpia.

Con este patrón usted va a romper el problema en segundos, impresionar al entrevistador, y conseguir una base de código limpio para mantener.

¡Feliz codificación! 🚀

-...

*Preparado por un ingeniero de software experimentado, listo para ser copiado en cualquier repositorio de entrevista de codificación. *