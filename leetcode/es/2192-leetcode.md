-...
Título: LeetCode 2192. Todos los Ancestros de un Nodo en un Gráfico Acíclico Dirigido -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Todos los Ancestros de un Nodo en un Gráfico Acíclico Dirigido
**LeetCode 2192 – Medium**

■ *Problema*
■ Dado un DAG con `n` nodos (0-basado) y una lista de bordes `edges`, devuelve una lista donde
> `answer[i]` contiene *todos* antepasados de nodo `i` en orden ascendente.
■ Un nodo `u` es un ancestro de `v` si hay un camino dirigido de `u` a `v`.

-...

### 1.1 Por qué este problema importa para entrevistas

*Principales gráficos* – topológicos, DFS, BFS
*Programación Dinámica en DAG* – conjuntos de antepasado
- *O(n^2) " vs. `O(n·m) `
- Demostraciones ** codificación limpia**: listas de adyacencia, clasificación, funciones de ayudante modular

■ ** Enfoque de palabras clave de SEO**: *Solución de LeetCode 2192*, *problema de antepaso de ADAG*, entrevista de algoritmos *, ejemplo de Java Python C++*, *ejecución de tipo topológico*

-...

## 2. Intuición

El gráfico es un DAG, por lo que podemos procesar nodos en orden **topológico**.
Cuando visitamos un nodo `v`, ya conocemos los conjuntos de ancestros de todos sus predecesores.
El antepasado conjunto de `v` es la unión de:

1. El antepasado de cada predecesor
2. El propio predecesor

Almacenamos el antepasado conjunto de cada nodo como un `bitset ' (o un `Set identificadoint titulada `) para permitir la unión rápida y mantener los datos pequeños.
Finalmente, convertimos cada bitset en una lista ordenada.

-...

## 3. Algoritm (Topological‐DP)

``text
1. Construir la lista de adyacency `adj[v] = lista de niños ' .
2. Compute indegree of each node.
3. El algoritmo de Kahn → array `topo` con un orden topológico.
4. Por cada nodo `v` en `topo`:
por cada niño.
antepasados[c] ← antepasados[c]
ancestros[c] ← antepasados[c]
5. Para cada nodo `v`: convertir `ancestors[v]` en un vector ordenado.
`` `

### Complexity

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencio Construir el gráfico Silencioso `O(n + m)` Silencio
tención Topológica especie Silencioso `O(n + m)` Silencio `O(n)` Silencio
Silencio Ancestor merging Silencio `O(n2)` (worst‐case `n` antepasados per node) Silencio `O(n2)` Silencio
Silencio Conversión final Silencioso `O(n2 log n)` (relleno de cada lista) Silencio

Con los límites dados (`n ≤ 1000`, `m ≤ 2000`) esto se ejecuta fácilmente en 200 ms.

-...

## 4. Implementaciones de referencia

A continuación se encuentran soluciones limpias, comentadas y listas para pasar en **Java**, **Python**, y **C+**.

-...

#### 4.1 Java

``java
importar java.util*;

Solución de la clase pública {}
public List made(int, int[] edges) {
// 1. Construir la lista de adyacencia
Lista realizadaLista realizadaInteger confianza adj = nuevo ArrayList recomendado();
para (int i = 0; i < n; i++) adj.add(new ArrayList correctamente());
int[] indeg = nuevo int[n];
para (int[] e : bordes) {
adj.get(e[0]).add(e[1]);
indeg[e[1]]+;
}

// 2. Orden topológico vía Kahn
Búsquedas realizadasInteger título q = nuevo ArrayDeque corresponde();
para (int i = 0; i) 0) q.offer(i);
Lista Nombramiento Nombrado = nuevo ArrayList(n);
(!q.isEmpty()) {
int v = q.poll();
topo.add(v);
para (int nb : adj.get(v))
si (--indeg[nb] == 0) q.offer(nb);
}

// 3. Conjuntos de ancestro
@SuppressWarnings("unchecked")
BitSet[] anc = new BitSet[n];
para (int i = 0; i < n; i++) anc[i] = nuevo BitSet(n);

// 4. DP over topo order
para (int v : topo) {
para (int nb : adj.get(v)) {}
anc[nb].or(anc[v]); // heredar todos los antepasados
anc[nb].set(v); // add the direct ancestor
}
}

// 5. Convertir en Lista realizadaLista realizadaInteger título
Lista realizadaLista realizadaInteger título res = nuevo ArrayList recomendado();
para (int i = 0; i)
Lista realizadaInteger confianza tmp = nuevo ArrayList recomendado();
para (int j = anc[i].nextSetBit(0); j ю= 0; j = anc[i].nextSetBit(j + 1))
tmp.add(j);
res.add(tmp); // ya ordenados debido a la orden del bit
}
restitución;
}
}
`` `

-...

#### 4.2 Python

``python
de las colecciones importan deque, defaultdict
de la importación Lista

Solución de clase:
def getAncestors(self, n: int, edges: List[List[int]) - No. List[List[int]]:
1. Adjacency + indegree
adj = [[] for _ in range(n)]
indeg = [0] * n
para u, v en los bordes:
adj[u].append(v)
indeg[v] += 1

# 2. Topo order
q = deque([i for i in range(n) if indeg[i] == 0])
topo = []
mientras q:
v = q.popleft()
topo.append(v)
para nb en adj[v]:
indeg[nb] -= 1
si indeg[nb] == 0:
q.append(nb)

# 3. Conjuntos de ancestro - utilizar Python set para la claridad
anc = [set() for _ in range(n)]

4. DP
por v in topo:
para nb en adj[v]:
anc[nb].update(anc[v]) # here
anc[nb].add(v) # direct ancestor

# 5. Ordenar cada lista
retorno [ surtido(lista(s)) para s en anc]
`` `

-...

#### 4.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector realizador identificadoint título obtenerAncestros(int n, vector seleccionado, vector seleccionado, marcador implicados iguales) {}
// 1. Graph + indegree
vector realizador realizado en el título adj(n);
vector implicado(n, 0);
para (auto &e : bordes) {}
adj[e[0].push_back(e[1]);
indeg[e[1]]+;
}

// 2. Kahn
queue indicaint
para (int i = 0; i) 0) q.push(i);
vector topo;
(!q.empty()) {
int v = q.front(); q.pop();
topo.push_back(v);
para (int nb : adj[v]) {}
si (--indeg[nb] == 0) q.push(nb);
}
}

// 3. Ancestor bitsets
vector asignado bitset realizado1000 confianza anc(n); // 1000 es el máximo n

// 4. DP
para (int v : topo) {
para (int nb : adj[v]) {}
anc[nb] Silencio= anc[v];
anc[nb].set(v);
}
}

// 5. Convertir en vectores ordenados
vector realizador:
para (int i = 0; i) {}
for (int j = anc[i]._Find_first(); j ' il; j = anc[i]._Find_next(j)))
as[i].push_back(j);
}
devolver los ans;
}
};
`` `

■ **Nota:**
■ *C++* utiliza una constante compilada `1000` para el tamaño del bitset. Si prefieres el dimensionamiento dinámico, cambia a `vector realizado noordered_set fielint `` o `vector seleccionadoset fielint ``, pero ten en cuenta la sobrecabeza superior.

-...

## 5. Alternate Brute‐Force DFS (O(n·m))

Si prefieres un DFS directo que sigue la idea original de “llegar a todos los descendientes”, aquí hay una versión compacta que aún se ajusta a los límites.

## 5.1 Java (versiónDFS)

``java
Solución de la clase pública {}
public List made(int, int[] edges) {
Lista realizadaLista realizadaInteger confianza adj = nuevo ArrayList recomendado();
para (int i = 0; i < n; i++) adj.add(new ArrayList correctamente());
(int[] e : edges) adj.get(e[0]).add(e[1]);

Lista realizadaLista realizadaInteger título res = nuevo ArrayList recomendado();
para (int i = 0; i < n; i++) res.add(new ArrayList recomendado());

para (int src = 0; src) {}
boolean[] vis = new boolean[n];
dfs(src, src, adj, res, vis);
}

para (Lista) Lista de títulos: res) Colecciones.sort(lista);
restitución;
}

dfs de vacío privado(int src, int cur, List made adj,
Lista seleccionadaLista realizadaInteger título res, boolean[] vis) {
vis[cur] = verdadero;
para (int nxt : adj.get(cur) {
si (!vis[nxt]) {}
res.get(nxt).add(src); // src es un ancestro de nxt
dfs(src, nxt, adj, res, vis);
}
}
}
}
`` `

### 5.2 Python

``python
Solución de clase:
def getAncestors(self, n: int, edges: List[List[int]) - No. List[List[int]]:
adj = [[] for _ in range(n)]
para u, v en los bordes:
adj[u].append(v)

res = [[] for _ in range(n)]

def dfs(src, cur, visited):
visitado[cur] = Verdadero
para nb en adj[cur]:
si no es visitado[nb]:
res[nb].append(src)
dfs(src, nb, visited)

para src en rango(n):
dfs(src, src, [False] * n)

retorno [ surtido(st) para lst in res]
`` `

### 5.3 C++

``cpp
vector realizador identificadoint título obtenerAncestros(int n, vector seleccionado, vector seleccionado, marcador implicados iguales) {}
vector realizador realizado en el título adj(n);
para (auto &e : edges) adj[e[0].push_back(e[1]);

vector realizador:
para (int src = 0; src) {}
vector:
función recomendadavoid(int)] dfs = (int cur) {
vis[cur] = verdadero;
para (int nb : adj[cur]) {}
si (!vis[nb]) {}
ans[nb].push_back(src);
dfs(nb);
}
}
};
dfs(src);
}
for (auto &vec : ans) sort(vec.begin(), vec.end());
devolver los ans;
}
`` `

■ **Performance** – Estas soluciones basadas en DFS son `O(n2)` en el peor caso, pero a menudo son más rápidos en la práctica cuando el gráfico es escasa (`m` pequeño). Son geniales para mostrar *simple lógica* y *recursión* a los entrevistadores.

-...

## 6. Bien, Mal & Ugly - Qué entrevistadores Care About

Silencio Silencio
Silencio------------Prince------
Silencio **Uso de listas de adyacency** Silencio Mantiene la memoria baja y las operaciones `O(1)` por edge ❌ Utilizando la matriz de adyacency volaría la memoria ❌ Mixing 0‐based and 1‐based indices will trip you up ←
Silencio **Espección teopológica** Silencio Garantías Previas datos de predecesores está listo ❌ Olvidar indegree → bucle infinito  1000 → desbordamiento de la pila
tención **Bitset / Set merging** Silencio Fast union, low overhead ❌ Utilizando `vector fielint titulado ` for merging → `O(n3)` ❌ Gestión manual de la memoria in C++ (missing `std::unique`) Silencio
Silencio **Sorting result** Silencio Necesitado para la declaración ❌ Omitting `.sort()` → respuesta incorrecta ❌ Clasificación interna de bucles → cuadrática sobrecabezada

■ **Takeaway:**
■ La solución DP‐on‐DAG (topological + bitset) es *la más limpia* y * más rápida* para las limitaciones.
■ La versión DFS-de-each‐node es más simple de entender pero puede ser más lenta en DAGs densos.
■ **Recuerde siempre**: en la codificación de entrevistas, una solución correcta *simple* a menudo golpea a una inteligente pero buggy.

-...

## 7. “Y si...” – Casos de borde y extensiones

Silencioso Caso Edge Silencio
Silencio...
Silencio **No hay bordes** (`m == 0`) Silencio Topo orden es `[0,1,...,n‐1]`; cada lista de antepasados permanece vacía. Silencio
# Gráfico de la palabra # (`0→1→2→...`) Cada nodo acumula `O(n)` antepasados; bitset maneja unión en `O(n)` cada uno. Silencio
Silencio **Large ancestor sets** Silencio `BitSet` asegura que sólo almacenamos un solo entero por ancestro; unión es una sola palabra máquina operación por 64 ancestros. Silencio
Silencio ** Casos de prueba obligatorios** Solución de Wrap en un bucle que dice `n ' edges ' por caso. Silencio

-...

## 8. Cómo utilizar estas soluciones para *Job Interview* Prep

1. **Lea cuidadosamente el problema** – Comprender la definición de un antepasado.
2. **Echa un orden topológico** – Escríbelo en papel; esto te ayudará a verificar el paso DP.
3. ** Código de la palabra en su idioma preferido** – Utilice los fragmentos arriba como plantilla.
4. **Pruebas locales** – Use el gráfico de la cadena de muestra " casos sin linaje.
5. **Explica tu lógica* En una entrevista, pasee por el algoritmo, no sólo el código.
5. **Destaque la eficiencia** – Mostrar cómo usar una lista de bitset o adjacency ahorra tiempo & espacio.

*Practice:* Intente implementar una variación en la que también necesita producir el *carril más largo* que utiliza sólo los bordes del antepasado.
> *Entrevista móvil:* Programa de par con un amigo y explique cada paso en inglés.

-...

## 9. Lectura adicional " Recursos "

Silencio Recurso _ Por qué Ayuda a vivir
Silencio------------
[LeetCode 1736 - 1736. Find in Mountain Array](https://leetcode.com/problemset/problem/1736) tención Práctica búsqueda binaria + DP en arrays. Silencio
[GFG – “Topological Sort”] (https://www.geeksforgeeks.org/topological-sorting/) ← explicación clásica del algoritmo de Kahn. Silencio
[cppreference – `std::bitset`](https://en.cppreference.com/w/cpp/utility/bitset) ← Inmersión profunda en operaciones de bitset. Silencio
TEN [Stack Overflow – “Memory efficient graph representation”](https://stackoverflow.com/questions/1045924/graph-representation-in-c) Silencio Discusses adjacency lists vs matrices. Silencio
Silencio [YouTube – “Algorithms: DP on DAGs”](https://www.youtube.com/watch?v=YzZgZt9qGvA) Silencio

-...

## 9. TL;DR – Resumen de una condena

*La solución más rápida y eficiente en memoria para LeetCode 1736 es realizar un tipo topológico, utilizar un bitset/`std::bitset` para combinar el ancestro se establece en tiempo lineal, y luego salida listas clasificadas; la variante DFS-de-cada-nodo es más simple pero puede ser más lento en gráficos densos. *

-...

### 10. introducir palabras finales

*Ahora estás equipado con las formas *optimal* y *simple* para resolver LeetCode 1736.
Recuerde: la clave para las entrevistas de codificación es un algoritmo **claro, correcto** y *explain‐your-thoughts* que demuestra que usted realmente entiende el dominio del problema. *

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀

-...



-...

### 11. FAQ

**Q1: ¿Por qué no utilizar una estructura de datos de identificación sindical? * *
A1: Union‐find es ideal para * componentes conectados*, no para las relaciones de ancestro dirigidas. El enfoque DP‐on‐DAG es el ajuste natural para gráficos acíclicos dirigidos.

**Q2: ¿Se recopilará el código de bitset C++ con '-std=c+17`?**
A2: Sí, pero debe definir el tamaño en el tiempo de compilación (por ejemplo, `bitset asignado1000 título ``). Para la dinámica " n " , considere " , " , " , " .

**Q3: ¿Y si la entrada utiliza índices basados en 1? #
A3: Convertir todos los vértices en 0-basado antes de construir el gráfico, o ajustar el resultado en consecuencia (por ejemplo, añadir 1 a cada índice en la salida).

**Q4: ¿Hay un algoritmo codicioso? * *
A4: Ningún algoritmo codicioso producirá los conjuntos correctos del antepasado porque usted debe considerar todos los caminos. El enfoque DP es la solución codictiva en el sentido de “tomar a todos los antepasados que ya han sido tomados. ”

-...

## 12. Pensamiento de clausura

■ ** En algoritmos gráficos, siempre piensa en un orden topológico. Una vez que lo tienes, muchos problemas se vuelven embarazosamente simples.”* *

¡Feliz codificación y disfrutar de romper el rompecabezas del antepasado de DAG! 🧩💻

-..