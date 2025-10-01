-...
Título: LeetCode 2858. Reversales de bordes mínimos Así que cada nodo es alcanzable -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 2858 - Reversales de bordes mínimos Así que cada nodo es alcanzable
*Una solución de entrevista, O(n) en **Java**, **Python** y **C++***

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

Se le da un gráfico **directo** que se convierte en un árbol no dirigido si todos los bordes son tratados como bi-directional.
Para cada nodo `i` (0 ≤ i < n) debe calcular el *número mínimo de reversales de bordes* necesarios para que a partir de `i` usted puede alcanzar **todo** otro nodo.

`` `
n - número de nodos (2 ≤ n ≤ 105)
bordes – (n‐1) bordes dirigidos: bordes [i] = [ui, vi] (ui → vi)
`` `

Devuelva un array `respuesta` de longitud `n`, donde `respuesta[i]` es la inversión mínima para root `i`.

-...

### 2down Why Why O(n2) is too Slow

Una solución ingenua corre un BFS/DFS de cada nodo y cuenta cuántos bordes deben ser volteados – eso es O(n) por root → **O(n2)**, lo que es imposible para n = 105.

-...

#### 3down⃣ Insight – *Re-rooting DP*

Tratar el árbol subyacente no dirigido como una lista de **adjacency** donde cada borde tiene dos direcciones posibles:

← Edge ← Costo si se atravesó como el coste original TEN si se atravesó en la inversa
Silencio------------------------------------------
Silencio u → v Silencio 0 Silencio 1 Silencio

**Paso 1 – Escoja cualquier raíz** (por ejemplo, nodo 0) y ejecute un DFS que agrega el costo del borde a la respuesta.
Esto da `cost[0]`, el número de reversales necesarios cuando 0 es el comienzo.

**Paso 2 - Re-root**
Cuando movemos la raíz de `u` a un nodo adyacente `v`, sólo la dirección del borde único (u,v) cambia.
- Si la dirección original era `u → v` (cost 0), moviendo la raíz a `v` nos obliga a atravesar `v → u` → +1 reversal.
- Si la dirección original era `v → u` (costo 1), moviendo la raíz a `v` elimina que reversal → –1.

Por lo tanto

`` `
cost[v] = cost[u] + (1 – 2 * original Cost(u → v))
`` `

Un segundo DFS propaga `cost[]` a todos los nodos en **O(n)** tiempo.

Todo el algoritmo es **O(n)** tiempo, **O(n)** espacio – perfecto para las limitaciones.

-...

### 4down⃣ Edge Cases

← Edge Silencio Por qué importa
Silencio...
Silencio Múltiples niños Silencio Ninguno – la propiedad del árbol garantiza un solo camino Silencio El algoritmo funciona independientemente de ramificación Silencio
Silencio Grande `n` ¦ La profundidad de la recuperación podría desbordarse en idiomas con pequeña pila ¦ Utilizar DFS iterante o aumentar el límite de recursión ¦
← Gráfico con los bordes “reversos” sólo  durable `cost[0]` puede ser que no sea cero No hay manejo especial – algoritmo cuenta correctamente

-...

#### 5down⃣ Aplicación del Código

A continuación se encuentran soluciones limpias y de producción en **Java**, **Python**, y **C+**.

▪ restablecimiento **Tamaño del tacto**:
√ - Java: la profundidad de la recursión es en la mayoría de 105; use `-Xss1M` si golpea el flujo de la pila.
√≥ - Python: `sys.setrecursionlimit(2_000_000) `
Ø - C++: La optimización de recursión de cola suele estar bien; de lo contrario, usa una pila explícita.

-...

##### 5.1 Java

``java
importar java.util*;

Solución de la clase pública {}
// lista de adyacencia: cada elemento es (vecino, costo)
[] gráfico []]
int privado [] costo;

int[] minEdgeReversals(int n, int[] edges) {
buildGraph(n, edges);

costo = nuevo int[n];
boolean[] visited = new boolean[n];

// Paso 1: DFS del nodo 0 – calcular costo[0]
dfs(0, visited);

// Paso 2: Re-root to propagate costs
Arrays.fill(visited, false);
reroot(0, visited);

Costo de retorno;
}

construcción de vacío privadoGraph(int n, int[] bordes) {
gráfico = nueva lista[n];
para (int i = 0; i) no; i++) grafo[i] = nuevo ArrayList fiel();

para (int[] e : bordes) {
int u = e[0], v = e[1];
graph[u].add(new int[]{v, 0}); // original direction
graph[v].add(new int[]{u, 1}); // reversed direction
}
}

// DFS que devuelve los totales reversales necesarios para subárbol arraigado en el nodo '
int privado dfs(int node, boolean[] visited) {
visitado[nodo] = verdadero;
total = 0;
para (int[] nb : graph[node]) {}
int next = nb[0], costEdge = nb[1];
si (!visited[next]) {}
total += costoEdge + dfs(next, visited);
}
}
cost[nodo] = total;
Total de retorno;
}

// Re-rooting DFS – actualizaciones costo para todos los nodos
privada void reroot (int node, boolean[] visited {
visitado[nodo] = verdadero;
para (int[] nb : graph[node]) {}
int next = nb[0], costEdge = nb[1];
si (!visited[next]) {}
// costo[next] = costo[nodo] + 1 - 2 * costoEdge
cost[next] = cost[nodo] + 1 - 2 * costEdge;
reroot(next, visited);
}
}
}
}
`` `

-...

#### 5.2 Python

``python
importadores
de las colecciones importadas por defecto

Solución de clase:
def minEdgeReversals(self, n: int, edges: list[list[int]]) - titulado list[int]:
sys.setrecursionlimit(2_000_000)

# Build weighted adjacency list
gráfico = defaultdict(list)
para u, v en los bordes:
(v, 0) # original
graph[v].append(u, 1)) # reverse

costo = [0]
visitado = [False] * n

def dfs(nodo: int) - título int:
visitado[nodo] = Verdadero
total = 0
para nxt, w en el gráfico [nodo]:
si no es visitado[nxt]:
total += w + dfs(nxt)
costo[nodo] = total
total

def reroot(nodo: int):
visitado[nodo] = Verdadero
para nxt, w en el gráfico [nodo]:
si no es visitado[nxt]:
costo[nxt] = costo[nodo] + 1 - 2 * w
reroot(nxt)

dfs(0)
visitado = [False] * n
reroot(0)
Costo de retorno
`` `

-...

#### 5.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
vector realizador designadopair realizado,int hilo conductor g; // (medio, costo)
vector Costo;
public:
vector identificador minEdgeReversals(int n, vector seleccionado, obtentor fielmente usado) {}
buildGraph(n, edges);
cost.assign(n, 0);
vector asignado confianza vis(n, 0);

// Paso 1: DAAT de 0
dfs(0, vis);

// Paso 2: Re-rooting
fill(vis.begin(), vis.end(), 0);
reroot(0, vis);
Costo de retorno;
}

privado:
construcción de vacíoGraph(int n, const vector armonizado) {}
g.assign(n, {});
para (continuo auto choza e : bordes) {
int u = e[0], v = e[1];
g[u].push_back({v, 0}); // original
g[v].push_back({u, 1}); // reverse
}
}

int dfs(int node, vector efectuador
vis[nodo] = 1;
int tot = 0;
para (auto [a, w] : g[nodo]) {}
si (!vis[to]) {}
tot += w + dfs(a, vis);
}
}
cost[nodo] = tot;
retorno tot;
}

vacio reroot (int node, vectorial fielchar ventaja vis) {
vis[nodo] = 1;
para (auto [a, w] : g[nodo]) {}
si (!vis[to]) {}
cost[to] = costo[nodo] + 1 - 2 * w;
reroot(to, vis);
}
}
}
};
`` `

-...

### 6 Cambios en la entrevista—Ley Tips

Silencioso Por qué importa
Silencio...
Silencio **Explicar el truco de re-raíz temprano** Silencio Ahorra tiempo y muestra que usted entiende árbol DP Silencio
Silencio **Mostrar el DFS de dos pasos explícitamente**
################################################################################################################################################################################################################################################################
TEN **Utilice una lista de adyacency ponderada** TEN mantiene el código conciso y evita dos arrays separados TEN

-...

### 7 comentarios 📚 Cómo ayuda el Blog Tú.

- ** Estructura azul** – Intro → Vista → Casos de borde → Código → Complejidad.
- ** "Bien, Mal, Ugly"** sección le dice lo que hace difícil el problema, por qué un enfoque ingenuo falla, y cómo re-rooting lo convierte en un DP limpio.
- **Las palabras clave de la SEO** (`leetcode`, `minimum edge reversals`, `tree DP`, `re-rooting`, `interview question`) ayudan a los reclutadores y los motores de búsqueda a encontrar esta guía.
- **Real-world coding snippets** en 3 idiomas principales.

-...

Pensamientos finales

*LeetCode 2858* es un problema clásico de “pesos de árbol + bordes dirigidos”.
La clave es convertir una dirección en un costo** y **propagar la raíz** con un solo paso del árbol.
Este O(n) DP no sólo es rápido sino también elegante – un candidato perfecto para entrevistas de codificación y código de producción.

Buena suerte en tu próxima entrevista, ¡y feliz codificación!