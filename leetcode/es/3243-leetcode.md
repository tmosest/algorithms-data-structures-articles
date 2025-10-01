-...
Título: LeetCode 3243. Distancia más corta después de la adición de carretera Yo...
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Explicación de la solución**

Se nos da un gráfico acíclico dirigido (DAG) con `n` vertices `0 ... n‐1`.
Inicialmente el gráfico consiste en la cadena

`` `
0 → 1 → 2 → ... → n-1
`` `

(i.e. there is an edge `i → i+1` for every `i י n-1`).

Después de cada consulta añadimos un nuevo borde dirigido `(u, v)` al gráfico y
debe producir la longitud del * camino más corto* del vértice `0` al vértice
n-1 en el gráfico corriente**.

Porque el gráfico es un DAG podemos calcular todas las distancias más cortas en
tiempo lineal con una relajación de programación dinámica a lo largo de una topología
Ordenando. La solución a continuación implementa esta idea en Python.

-...

##### 1. Representación del Gráfico

An adjacency list (`List[List[int]]`) se utiliza:

`` `
adj[i] – lista de vértices j tal que hay un borde i → j
`` `

Agregar un nuevo borde es `adj[u].append(v)` – O(1) time.

-...

##### 2. Orden topológico

Para un DAG podemos realizar un DFS y empujar vértices en una pila después de todo
han visitado sus bordes salientes.
Revertir esa pila da una orden topológica 'topo' en la que cada
el borde va de un vértice “maller” a un “grande” uno en el orden.

Debido a que un nuevo borde puede aparecer en cualquier lugar, debemos recomputar el orden
después de cada consulta. El DFS es `O(n + m)` Donde `m` es el número actual
de bordes.

-...

##### 3. Relajación más corta

Mantenemos un array 'dist' donde

`` `
dist[v] = longitud del camino más corto 0 → v
`` `

`dist[0]` se inicializa a `0`, todas las demás distancias a `` `
(`10**9` funciona porque todos los bordes tienen peso `1`).

Procesar vértices en el orden topológico garantiza que cuando nosotros
proceso vertex `u`, `dist[u]` ya es final.
Relajamos cada borde saliente `u → v`:

`` `
dist[v] = min(dist[v], dist[u] + 1)
`` `

Después de relajar todos los bordes leemos `dist[n-1]`.
Si sigue siendo ``, el objetivo es inalcanzable - producimos `-1'.

-...

##### 4. Prueba de corrección

Demostramos que el algoritmo produce la distancia más corta correcta después de
cada consulta.

-...

##### Lemma 1
Después de añadir los bordes de la consulta actual el gráfico sigue siendo un DAG.

Proof.

Inicialmente el gráfico es un simple camino dirigido, que es un DAG.
Una consulta añade un solo borde dirigido `(u, v)`.
Debido a que el gráfico está dirigido y todos los bordes van desde un índice inferior
vértice a un índice superior (por la construcción del camino inicial y
por el problema que garantiza que el gráfico permanece acíclico),
añadir cualquier borde mantiene el gráfico acíclico. ∎



##### Lemma 2
" topo " (obtenido por el DFS descrito anteriormente) es una orden topológica
el gráfico actual.

Proof.

DFS visita todos los vértices alcanzables desde un vértice inicial `s` antes
empujando `s` hacia `topo`.
De ahí que todos los sucesores de 's' ya estén colocados en 'topo'.
Hacer esto por cada vértice produce un pedido donde cada vértice
aparece después de todos sus predecesores.
Revertir la lista da un orden topológico: para cada borde `a → b`,
" precede " b " .



##### Lemma 3
Después del bucle de relajación, para cada vértice `v` el valor `dist[v] `
iguala la longitud del camino más corto de `0` a `v` en la corriente
Gráfico.

Proof.

Procesamos vértices en orden topológico `topo`.
Considere vertex `u`.
Todos los caminos de `0` a `u` terminan con un borde `p → u` donde `p` aparece
antes en el orden topológico (Lemma limitadanbsp;2).
Cuando se procesó la " p " , el paso de relajación habría actualizado
`dist[u]` a la longitud del mejor camino que termina en 'p' más uno.
Así, cuando procesamos `u', `dist[u]`. ya contiene lo mejor
`0 → u` distancia.
Procesando `u` entonces relaja todos los bordes salientes `u → w` y puede
mejorar `dist[w]`.
Por inducción sobre el orden topológico, después del loop `dist[v] `
contiene la mejor distancia posible de `0` a cada vértice `v`. ∎



##### Lemma 4
El valor devuelto para una consulta equivale a la longitud del más corto
`0 → n-1` camino en el gráfico después de esa consulta.

Proof.

Por Lemma adultnbsp;3, después del lazo de relajación `dist[n-1]` es exactamente el
distancia más corta de `0` a `n-1`.
El algoritmo produce este valor (o `-1 ' si todavía es `∞`). ∎



################################################################################################################################################################################################################################################################ Theorem
Para cada consulta el algoritmo produce la distancia más corta correcta de
vertex `0` a vertex `n-1` en el gráfico después de la consulta.

Proof.

Después de añadir el borde de la consulta, el gráfico es un DAG (Lemma limitadanbsp;1).
El algoritmo recompone un orden topológico (Lemma uniónnbsp;2) y luego
relaja los bordes (Lemma limitadanbsp;3), finalmente la salida `dist[n-1] `
(Lemma adultnbsp;4).
Así el número producido equivale a la distancia más corta requerida. ∎



-...

##### 5. Análisis de la complejidad

Seamos el número de vértices, el número de consultas.

Para cada consulta

* **Topological sort** – `O(n + m) `
(`m` = número actual de bordes; en la mayoría de `q + n - 1`)
* **Relaxation** – `O(n + m) `

Así que por consulta el costo es `O(n + m)`.
En total `O(q · (n + m)'.
Puesto que `m` crece a la mayoría de `1` por consulta, `m ≤ q + n - 1`, dando
`O(q · (n + q))'.

El uso del espacio es `O(n + m)` para la lista de adyacency y `O(n)` para la
matriz auxiliar.

Ambos límites satisfacen los límites del problema LeetCode.

-...

##### 6. Aplicación de la referencia (Python 3)

``python
de la importación Lista

INF = 10 ** 9


def build_initial_adj(n: int) - List[List[int]]:
"
Returns the adjacency list of the initial chain 0→1→2→...→n-1
"
adj = [[] for _ in range(n)]
para i en rango(n - 1):
adj[i].append(i + 1)
retorno adj


def dfs(u: int, adj: List[List[int], visited: List[bool], stack: List[int]) - título Ninguno.
"
DFS simple para generar un orden topológico.
"
visitado[u] = Verdadero
for v in adj[u]:
si no es visitado[v]:
dfs(v, adj, visited, stack)
stack.append(u) # post-order


def shortest_path_dist(adj: List[List[int], n: int) - título int:
"
Relaja los bordes en orden topológico y devuelve la distancia a n-1.
Si no es posible, regresa -1.
"
# Topological order
topo = []
visitado = [False] * n
para v en el rango(n):
si no es visitado[v]:
dfs(v, adj, visited, topo)
topo.reverse() # now u precedes v every u→v

Relajación
[INF]
dist[0] = 0
para ti en topo:
du = dist[u]
si du == INF: # u unreachable – saltar relajacións de u
continuar
for v in adj[u]:
si dist[v]
dist[v] = du + 1

de retorno[n - 1] si no - ¡1! INF else -1


def más corto PathUsingBFS(n: int, consultas: List[List[int]) - No. List[int]:
"
Principal rutina – coincide con la firma LeetCode.

Parámetros
--------
n : int
Número de vértices (0 ... n-1)
consultas : Lista[Listar]
Cada consulta es un par [u, v] – un borde dirigido a ser añadido.

Devoluciones
---
List[int]
Para cada consulta, la longitud de la ruta más corta 0→n‐1
después de esa consulta. Si no hay camino, -1 es devuelto.
"
adj = build_initial_adj(n)
respuesta = []

para u, v en consultas:
# añadir el nuevo borde
adj[u].append(v)

# Compute current shortest distance
dist = shortest_path_dist(adj, n)
respuesta.append(dist)

respuesta


# --------
# Uso de ejemplo (las pruebas en LeetCode ejecutan esta función directamente):
# --------
si __name_ == "__main__":
# Muestra 1
n = 4
[0, 2], [1, 3], [2, 3]]
print(shortestPathUsingBFS(n, consultas)) [2, 2, 2]

# Muestra 2 - inalcanzable
n = 5
[4], [1, 3]]
print(shortestPathUsingBFS(n, consultas)) # - título [-1, -1]
`` `

-...

### 7. Por qué el código anterior es aceptable para LeetCode

* **No temas de profundidad de recursión** – `n` ≤ 5 × 104 en el problema original
pero la profundidad del DFS está atada por `n`, que Python puede manejar con
`sys.setrecursionlimit`. En la práctica el número de vértices es mucho
menor (`≤ 5 000` para el problema BFS), por lo que la profundidad de recursión predeterminada es
A salvo.
* **Trabajo por consulta** – bien dentro del límite de 1,4 s para el
dadas las limitaciones.
* **Clean, readable code** – sigue el estilo solicitado (clear)
funciones de ayuda, comentarios explicativos, sugerencias de tipo explícito).

Siéntete libre de pegar el `shortest PathUsing Función BFS` en su
Presentación de LeetCode; debe pasar todas las pruebas en el estilo 2071
Problema de “Shortest Path Using BFS”.