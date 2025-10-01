-...
Título: LeetCode 2662. Costo mínimo de un camino con caminos especiales -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Solution Idea**

Para cualquier dos puntos `p1` y `p2` siempre podemos caminar por la red y el costo es su distancia de Manhattan

`` `
dist(p1,p2) = tenciónx1-x2 vidas +  sometiday1-y2
`` `

A * special road* `(a,b,c,d,w)` gives us a *directed* shortcut from `(a,b)` to `(c,d)` with cost `w`.
Si `w` no es más barato que la distancia normal de Manhattan nunca usaremos esa carretera – simplemente podemos caminar directamente.

El problema es, por lo tanto, un problema más corto en un gráfico:

* **Vertices** – todas las coordenadas distintas que aparecen:
* punto de inicio
* punto de destino
* de todos los caminos especiales

Que el número total de vértices sea `` (`N ≤ 2 + 2·k`, `k ≤ 100`).

****Edges*
* Por cada par de vértices `u , v` añadir un borde no redirigido con peso `dist(u,v)` (grid walking).
* Por cada carretera especial añadir un borde dirigido desde su comienzo hasta su final con peso `w`.

Ahora la respuesta es simplemente la longitud del camino más corto desde el vértice inicial hasta el vértice objetivo.
Debido a que el gráfico es denso (construir 'N2' bordes) podemos ejecutar **Dijkstra** directamente en él – su complejidad
`O(N2 log N)` es más que lo suficientemente rápido para 'N ≤ 202`.

-...

## Algorithm
1. *Recojan todos los vértices*
Mapa cada coordinación única a un entero id.
2. **Computar todas las distancias de Manhattan**
`mdist[i][j] = tenciónx_i-x_j sufrimiento + prehensiy_i-y_j sufrimiento`.
3. ** Listas de adyacencias de edificios**
* Por cada par " i " añadir el borde no redireccionado " (i,j) " con el peso `mdist[i][j] ' .
* Por cada carretera especial `(a,b,c,d,w)` añadir un borde dirigido de id(a,b) a id(c,d) con peso `w`.
4. **Run Dijkstra** desde el vértice inicial.
5. Devuelve la distancia encontrada al vértice objetivo.

-...

### Correctness Proof

Demostramos que el algoritmo devuelve el coste mínimo posible de viaje.

**Lemma 1**
Para cualquier dos vértices `u` y `v` el gráfico contiene un borde de peso igual al mínimo
costo posible de viajar de `u` a `v ' utilizando sólo movimientos normales de la red.

*Proof. *
Por construcción añadimos un borde sin dirección entre cada par de vértices con peso
``. Esta es exactamente la distancia de Manhattan, que es el costo mínimo
caminar entre `u ' y `v ' sin utilizar un camino especial. ∎



*Lemma 2*
Para cualquier carretera especial `(a,b)-(c,d,w)` el gráfico contiene un borde dirigido cuyo peso
equivale al costo de usar esa carretera.

*Proof. *
Añadimos un borde dirigido de id(a,b) a id(c,d) con peso `w`. ∎



**Lemma 3**
Para cualquier caminata en la declaración del problema original existe un camino en la construcción
gráfico con el mismo costo total, y vice-versa.

*Proof. *
Un paseo consiste en alternar segmentos de la red caminando y (posiblemente) carreteras especiales.
* Un segmento de andar en cuadrícula entre dos vértices consecutivos.
puede ser reemplazado por el borde `(u,v)` de Lemma limitadanbsp;1 – los costos coinciden.
* Un segmento especial está representado por el borde correspondiente dirigido
Lemma limitadanbsp;2 – los costos coinciden.
Porque insertamos bordes para *todos* par de vértices que pueden aparecer en un paseo,
todos los mapas de caminata a un camino gráfico de igual costo.
La dirección inversa es trivial: cualquier camino del gráfico se traduce de nuevo en un paseo en el
configuración original porque cada borde gráfico es realizable ya sea caminando o por una especial
carretera. ∎



*Lemma 4*
El algoritmo de Dijkstra devuelve la longitud del camino más corto en el gráfico desde el principio
al objetivo.

*Proof. *
Todos los pesos del borde son no negativo, por lo que se aplica el argumento de corrección estándar para Dijkstra. ∎



**Teorema* *
El algoritmo produce el coste mínimo posible de viaje desde el punto de inicio hasta el
punto de destino.

*Proof. *
Por Lemma adultnbsp;3 el conjunto de caminatas factibles en el problema original está en uno a uno
correspondencia con el conjunto de caminos en el gráfico construido, preservando coste total.
Por Lemma adultnbsp;4 Dijkstra encuentra la ruta de coste mínimo en el gráfico.
Por lo tanto, el costo devuelto por el algoritmo equivale al óptimo en el problema original. ∎



-...

### Complexity Analysis

Seamos el número de carreteras especiales ( " k ≤ 100 " ).
Número de vértices `N = 2 + 2·k ≤ 202`.

* Distancias anteriores a Manhattan: `O(N2)` tiempo, `O(N2)` memoria.
* Listas de adyacencia de edificios: también bordes `O(N2)`.
* Dijkstra: `O(E log V)` with `E = Ø(N2) → `O(N2 log N)` time.
* Consumo de memoria: listas de adjacency + array de distancia → `O(N2)`.

Con `N ≤ 202` esto está muy por debajo de los límites para un límite de tiempo de 2 s.

-...

### Referencia Implementación (Python 3)

``python
importadores
importación heapq

def solve() - título Ninguno.
data = sys.stdin.read().strip().split()
si no datos:
Regreso
iter(data)
sx, sy, tx, ty = map(int, (next(it), next(it), next(it), next(it))))
k = int(next(it)))

# Recopilar todas las coordenadas distintas
coord_to_id = {}
coords = []

def get_id(x, y):
si (x, y) no en coord_to_id:
coord_to_id [(x, y)] = len(coords)
coords.append(x, y))
devolver coord_to_id[(x, y)]

start_id = get_id(sx, sy)
target_id = get_id(tx, ty)

special_edges = [] # (u_id, v_id, weight)
para _ en rango(k):
a, b, c, d, w = map(int, (next(it), next(it), next(it), next(it), next(it), next(it)))
b - d): # carretera útil sólo
u = get_id(a, b)
v = get_id(c, d)
special_edges.append(u, v, w))

n = len(coords) # número de vértices

# pre-compute Manhattan distances
mdist = [[0] * n for _ in range(n)]
para i en rango(n):
xi, yi = coords[i]
para j en rango(i + 1, n):
xj, yj = coords[j]
d = abs(xi - xj) + abs(yi - yj)
mdist[i][j] = mdist[j][i] = d

# build adjacency lists
adj = [[] for _ in range(n)]
# grid walking edges (undirected)
para i en rango(n):
para j en rango(i + 1, n):
w = mdist[i][j]
adj[i].append(j, w))
adj[j].append(i, w))
# special road edges (directed)
para u, v, w en special_edges:
adj[u].append(v, w))

# Dijkstra
INF = 10**18
[INF]
dist[start_id] = 0
pq = [(0, start_id)]

mientras pq:
d, u = heapq.heappop(pq)
si d != dist[u]:
continuar
si u == target_id:
descanso
for v, w in adj[u]:
d + w
si nd , se hizo [v]:
[v] = nd
heapq.heappush(pq, (nd, v))

print(dist[target_id])

si __name_ == "__main__":
solve()
`` `

** Formato de entrada* *

`` `
sx sy tx ty
k
a1 b1 c1 d1 w1
...
ak bk ck dk wk
`` `

**La salida*

`` `
minimum_cost
`` `

El programa sigue exactamente el algoritmo probado correcto arriba y funciona cómodamente
dentro de los límites.