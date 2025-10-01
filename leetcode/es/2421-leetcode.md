-...
Título: LeetCode 2421. Número de buenos caminos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Python – Union‐Find solution for “Number of Good Paths”* *

El objetivo es contar el número de caminos *bueno* en un gráfico no dirigido.

* Un buen camino es un camino simple (no repetido vértice) cuyos puntos finales tienen el mismo valor, y el valor máximo en todo el camino equivale a ese valor de punto final.
* Cada vértice es un buen camino trivial – que contribuye uno a la respuesta.

La solución clásica funciona
`O(n + m) · α(n) )` tiempo (`α` = función inversa de Ackermann) y
`O(n + m)` memoria, donde `n` es el número de nodos y `m` el número de bordes.

-...

### 1. Idea

1. ** Lista de adyacencia** – almacenar el gráfico como una lista de vecinos para cada nodo.
2. **Value → nodos mapa** – para cada valor distinto del nodo mantener una lista de nodos que tienen ese valor.
3. ** Valores del proceso en orden ascendente** –
Para un valor actual `v` sólo necesitamos fusionar los nodos que pueden conectarse por un camino que no ** contiene un valor mayor que `v`.
Esto significa que podemos unir con seguridad un nodo con un vecino *iff* el valor del vecino ≤ `v`.
4. **Conteo completo** – después de que todos los sindicatos por el valor actual se hagan, miren sólo los nodos que realmente tienen valor `v`.
Cuenta cuántos de ellos pertenecen a cada componente conectado (root).
Si un componente contiene `k` tales nodos, todos los pares sin orden de ellos dan un `k·(k‐1)/2` buenos caminos.
Añada eso a la respuesta.
5. **Respuesta interior** – cada nodo solo contribuye un buen camino.
Así que comenzamos con `ans = n` y agregamos el par cuenta mientras vamos.

-...

### 2. Código

``python
de las colecciones importadas por defecto
de la importación Lista

# ---------- Union‐Find (Disjoint Set Union) ------------
clase DSU:
"
DSU clásico con compresión de ruta y unión por tamaño.
parent[x] == x → x es una raíz
tamaño[root] → número de nodos en el componente
"
def __init__(self, n: int):
self.parent = list(range(n))
auto.size = [1]

def find(self, x: int) - título int:
""Retorna la raíz de x con compresión de ruta.""
mientras yo. parent[x]!= x:
self.parent[x] = self.parent[self.parent[x]
x = self.parent[x]
retorno x

def union(self, a: int, b: int) - Ninguno.
""Merge los componentes que contienen a y b.""
ra, rb = self.find(a), self.find(b)
si ra == rb:
Regreso
# unión por tamaño - adjuntar el árbol más pequeño a la mayor
si auto.size[ra] se hizo auto.size[rb]:
ra, rb = rb, ra
self.parent[rb] = ra
auto.size[ra] += self.size[rb]

# ---------- Solución principal...----------
def number_good_paths(vals: List[int], edges: List[List[int]]) - título int:
"
Contar todos los buenos caminos en un gráfico no dirigido.

Parámetros
--------
vals : List[int]
Valores de nodos. Nodo tengo valor vals[i].
bordes : List[List[int]]
Los bordes no dirigidos, cada borde es [u, v] (índices basados en 0).

Devoluciones
---
int
El número total de buenos caminos.
"
n = len(vals)
1. Construir la lista de adyacencia
adj = defaultdict(list)
para u, v en los bordes:
adj[u].append(v)
adj[v].append(u)

# 2. Valor de mapa → lista de nodos que tienen ese valor
val_to_nodes = defaultdict(list)
for node, val in enumerate(vals):
val_to_nodes[val].append(node)

# 3. Prepare DSU
dsu = DSU(n)

4. Respuesta inicial: cada uno de los nodos es un buen camino
ans = n

# 5. Valores de proceso en orden ascendente
para val en orden(val_to_nodes):
nodos = val_to_nodes[val]

a) Combinar nodos con vecinos de valor
para nodos en nodos:
para nb en adj[nodo]:
si vals[nb]
dsu.union(nodo, nb)

# b) Cuenta los nodos de este valor dentro de cada componente
comp_cnt = defaultdict(int)
para nodos en nodos:
root = dsu.find(node)
comp_cnt[root] += 1

# c) Cada par sin orden de tales nodos forma un buen camino
para cnt en comp_cnt.values():
si cnt
ans += cnt * (cnt - 1) // 2

Retorno
`` `

-...

### 3. Cómo funciona – un paseo rápido

* **Sorting the values** garantiza que cuando procesamos un valor `v`, cada nodo que puede permanecer en un buen camino hacia otro nodo de valor `v` ya se ha fusionado con todos los valores estrictamente menores.
* **Unión sólo con vecinos de valor ≤ v** preserva la condición de que el máximo en el camino es `v`.
Cualquier vecino con valor ` ' contravendría la regla del buen camino y, por lo tanto, no debe fusionarse para este paso.
* **Counting pairs per component** – una vez que los sindicatos se hacen, todos los nodos de valor `v` que comparten la misma raíz pertenecen a un único componente conectado que contiene sólo nodos ≤ `v`.
Cada par de ellos se puede conectar por un buen camino, por lo tanto el coeficiente binomial.

-...

### 4. Análisis de la complejidad

*Edificio de la lista de adyacencia* – `O(n + m)`
*Sorting unique values* – `O(k log k)`, where `k` ≤ `n `
*Procesando cada nodo una vez por cada uno de sus vecinos* – sindicatos `O(m), cada `α(n)` amortizado
*Conteo completo* – `O(n)` sobre todos los valores

Tiempo total: **O(n + m) · α(n))** (esencialmente lineal).
Consumo de memoria: **`O(n + m)`**.

-...

### 5. Ejemplo

``python
si __name_ == "__main__":
vals = [1, 3, 2, 1, 3]
bordes = [[0,1], [1,2], [2,3], [2,4]]
print(number_of_good_paths(vals, edges)) # Output: 6
`` `

Los 6 buenos caminos son:

1. `[0]` (valor 1)
2. `[1] ' (valor 3)
3. `[2]` (valor 2)
4. `[3] (valor 1)
5. `[4]` (valor 3)
6. `[1, 2, 4]` – endpoints ambos 3, nodo intermedio 2 tiene valor 2 ≤ 3.

-...

Siéntase libre de dejar caer la función en su propia base de código o utilizarla como referencia para implementar el problema *Número de caminos buenos* en cualquier entorno pitón.