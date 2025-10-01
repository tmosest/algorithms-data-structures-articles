-...
Título: LeetCode 3593. Incrementos mínimos para la igualdad de caminos de hoja -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

## 🧩 LeetCode #1525 – *Minimum Increments to Equalize Leaf Paths*
**Solutions in Java, Python & C++ + A Deep‐ Dive Blog para Ace Your Interview**

■ **Etiquetas de SEO**: LeetCode, Incrementos Mínimos para Equiparar Sendas de Hoja, árbol DP, ruta de raíz a hoja, algoritmo, solución Java, solución Python, solución C+++, prep de entrevista, instrucciones de datos, entrevista de trabajo, estructuras de datos " algoritmos

-...

### 1. El problema (en inglés claro)

Se le da un árbol con n.odos ** (`0 ... n-1`).
Cada nodo `i` tiene un costo positivo `cost[i]`.
Usted puede ** aumentar el costo de cualquier nodo** por cualquier cantidad (el aumento es *permanente* para ese nodo).

** Objetivo**: Elija los nodos *feo* para aumentar de modo que *toda la suma del camino raíz a hoja** se convierta en la misma.

■ *Ejemplo*
" costo = [2,1,3] " , bordes = `[0,1],[0,2] " → respuesta = **1** (aumento del nodo 1).

-...

### 2. Aspectos clave

Silencio Silencio Silencio Silencio
Silencio...
Silencio ✅ **Las sumas de hoja conducen todo** – el objetivo es simplemente la suma de hoja más grande. ❌ **Mis‐using a “global max”** – usted debe comparar *sub-tree* sumas de hoja, no el costo de la raíz solo. ** Profundidad de la recursión** – un DFS ingenuo recursivo puede alcanzar el límite de la pila en un árbol degenerado. Silencio
Silencio ✅ **Incremento sólo el niño que importa** – cada subárbol infantil “smaller” necesita exactamente un aumento. Silencio ❌ **Asumiendo que aumentará en el padre** – usted ** debe aumentar el nodo del niño (cuenta un nodo). Silencio **Int vs Long** – las sumas pueden rebosar enteros de 32 bits (max 105 × 109 ♥ 1014). Silencio

El corazón de la solución es un árbol ** post-orden DP** que devuelve, para cada nodo, la suma máxima de la hoja en su subárbol.
Durante la misma caminata contamos cuántos niños sub-árboles son **shorter** que el máximo y por lo tanto necesitan un aumento.

-...

### 3. El Algoritmo (Bottom‐Up DFS)

1. **Construir una lista de adyacencia** – el árbol no está dirigido pero ignoraremos al padre durante el DFS.
2. **DFS(nodo)**
* If `node` is a leaf → return `cost[node]`.
* De lo contrario:
* Por cada niño, compute `childMax = DFS(child)`.
* Let `maxChild = max(childMax)` – this is the *maximum* leaf sum under `node`.
* Para cada niño con `niñeraMax ). maxChild` → **incremento de ese niño una vez** (advertido para responder).
* Volver `maxChild + costo[nodo]` como la suma máxima de la hoja del subárbol actual.
3. La llamada raíz da la respuesta.

Debido a que sólo necesitamos añadir un solo aumento de nodos para cada niño "corto", el número total de incrementos es simplemente la suma de esos recuentos.

-...

### 4. Análisis de la complejidad

Silencio Silencio Silencio Silencio
Silencio--------------------------
tención Tiempo Silencioso **O(n)** Silencio Cada borde es visitado dos veces (una vez para construir, una vez en DFS). Silencio
Silencio Memoria Silencio **O(n)** Silencio Lista de Adjacency + pila de recursión. Silencio
Silencio Numeric tención **64-bit integers** Silencio Sum up to `n * 109 ♥ 1014`, fits in `long` / `int64`. Silencio

-...

### 5. Pitfalls comunes

Silencio Pitfall Silencio
Silencio...
Silencio **Desbordamiento de la cubierta** en un árbol similar a la línea ¦ Utilizar DFS iterante o aumentar el tamaño de la pila JVM. Silencio
Silencio **Compararing leaf sums incorrectly** tención Sólo compare las sumas de hoja *sub-tree* (`childMax`) – `cost[node]` es común a todos los niños. Silencio
Silencio **Using `int` for sums** Silencio Switch to `long` / `int64` to avoid overflow. Silencio
tención **Tratar la raíz como una hoja en un árbol de 1‐nodo** tención Regresar 0 incrementos – manejados automáticamente. Silencio

-...

### 6. Código

A continuación encontrará soluciones limpias y idiomáticas para **Java, Python y C++**.

-...

##### 6.1 Java

``java
importar java.util*;

Clase Solución {

ans privados de larga duración; // contador global

int minIncrease(int n, int[] bordes, int[] cost) {
// Construir la lista de adjacency
Lista de datos adj = nuevo ArrayList[n];
para (int i = 0; i) no; ++i) adj[i] = nuevo ArrayList fiel();
para (int[] e : bordes) {
adj[e[0].add(e[1]);
adj[e[1]].add(e[0]);
}

as = 0;
dfs(0, -1, adj, cost);
int
}

/** Post-order DFS.
* Devuelve la suma de hoja máxima en el subárbol arraigado en el nodo. */
dfs privados largos (nodo int, int parent, List made adj, int[] cost) {
boolean isLeaf = true;
maxChild = Long.MIN_VALUE;

para (incluido niño : adj[nodo]) {}
si (hijo == padre) continúan;
isLeaf = false;
long childMax = dfs(child, node, adj, cost);
(childMax > maxChild) maxChild = childMax;
}

si (esLeaf) { // hoja node
costo de devolución[nodo];
}

// Cuenta niños que son estrictamente más cortos que el mejor
para (incluido niño : adj[nodo]) {}
si (hijo == padre) continúan;
long childMax = dfs(child, node, adj, cost); // already computed
si (childMax < maxChild) ans++; // aumento de este niño
}

volver maxChild + costo[nodo];
}
}
`` `

■ **Por qué funciona la recursión**: La pila predeterminada de Java es suficiente para ≤ 105 profundidad en la mayoría de los jueces en línea; para el código de producción puede reemplazar la recursión con una pila explícita.

-...

##### 6.2 Python

``python
importadores
sys.setrecursionlimit(1 Identificado 25) # protector seguro para árboles profundos

Solución de clase:
def minIncrease(self, n: int, edges: List[List[int]], cost: List[int]) - título int:
adj = [[] for _ in range(n)]
para a, b en los bordes:
adj[a].append(b)
adj[b].append(a)

self.ans = 0

def dfs(nodo: int, parent: int) - int:
is_leaf = True
max_child = -1
para nxt en adj[nodo]:
si nxt == padre: continuar
is_leaf = False
child_max = dfs(nxt, node)
si niño_max √≥ max_child:
max_child = child_max

if is_leaf: # leaf node
costo de devolución[nodo]

# Contando niños que son más cortos que los mejores
para nxt en adj[nodo]:
si nxt == padre: continuar
si dfs_cache[nxt]
self.ans += 1

volver max_child + costo[nodo]

# Use memoization to avoid re-calculating child values
Dfs_cache = {}
def dfs(nodo, padre):
si nodo en dfs_cache: devolver dfs_cache[nodo]
is_leaf = True
max_child = -1
para nxt en adj[nodo]:
si nxt == padre: continuar
is_leaf = False
child_max = dfs(nxt, node)
si niño_max √≥ max_child:
max_child = child_max
si es_leaf:
val = costo[nodo]
más:
# Conde necesitaba aumentos
para nxt en adj[nodo]:
si nxt == padre: continuar
si dfs_cache[nxt]
self.ans += 1
val = max_child + costo[nodo]
dfs_cache[node] = val
retorno val

dfs(0, -1)
Vuélvete. ans
`` `

*El límite de recursión de Python aumenta, y la memoización (`dfs_cache`) garantiza que cada nodo se procesa una vez. *

-...

#### 6.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
ans largos = 0;

dfs largos(int u, int p, const vector seleccionadovector fielmente usados, const vector implicados bajos costes) {
hoja de bool = verdadero;
long long best = LLONG_MIN; // maximum child leaf sum

para (int v : adj[u]) {}
si (v == p) continúan;
hoja = falsa;
long long child = dfs(v, u, adj, cost);
si (hijo jó mejor) mejor = niño;
}

si (en hojas) costo de devolución[u]; //

// Cuenta niños que son estrictamente más cortos que el mejor
para (int v : adj[u]) {}
si (v == p) continúan;
si (dfs_cache[v] se hizo mejor) ans++; // aumentar este niño
}

devolver el mejor + costo[u];
}

int minIncrease(int n, vector asignadovector seleccionador seleccionado) {
vector realizador realizado en el título adj(n);
para (auto &e : bordes) {}
adj[e[0].push_back(e[1]);
adj[e[1]].push_back(e[0]);
}

// Use un caché para que cada valor de niño sólo se computa una vez
vector realizado largamente cache(n, -1);
función cumplida larga (int,int)
si (cache[u]!= -1) cache de retorno[u];
hoja de bool = verdadero;
largo tiempo mejor = LLONG_MIN;

para (int v : adj[u]) {}
si (v == p) continúan;
hoja = falsa;
long long child = rec(v, u);
si (hijo jó mejor) mejor = niño;
}

si (siervo) {
cache[u] = cost[u];
. ♫ ... {
para (int v : adj[u]) {}
si (v == p) continúan;
si (cache[v]  made best) ++ans; // aumento de este niño
}
cache[u] = best + cost[u];
}
cche[u];
};

rec(0, -1);
volver estática_cast seleccionado(ans); // respuesta cabe en int
}
};
`` `

-...

### 7. Wrap‐Up

* La suma de destino es **la suma de hoja más grande** – sin “trabajo”.
* Un aumento del tamaño por niño más corto** basta.
* El DFS inferior da tanto el objetivo como la respuesta en un barrido.

Con estas tres soluciones pulidas y el ** "Good-Bad-Ugly"** desglose, estás listo para:

* Presentar una respuesta rápida y eficiente en memoria en LeetCode o cualquier plataforma de codificación. *
* Explicar la intuición rápidamente en una entrevista real y ver al entrevistador filo. *

Buena suerte – ¡tienes esto! 🚀