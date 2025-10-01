-...
Título: LeetCode 3004. Máximo Subtree del mismo color -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 3004 – “Maximum Subtree of the Same Color”
**Solución en Java Silencio en Python
**+ Una publicación de blog amigable de SEO que cuenta la historia del “Bueno, el Mal”* *

-...

#### TL;DR

* ** Objetivo** – Encuentra el subárbol más grande (arraigado en cualquier nodo) donde **todo nodo tiene el mismo color**.
* **Idea** – DFS + back-tracking.
* ** Complejidad** – `O(n)` tiempo, `O(n)` espacio (pilación de recusión).
* **Code** – 3 implementaciones listas para pasar (Java, Python, C++).

-...

## 1. Recaptación de problemas

■ **LeetCode 3004 – Subtree máximo del mismo color**
■ Se le da un árbol arraigado (nodo 0 es la raíz).
} `edges[i] = [u, v]` denota un borde no dirigido.
"colores" es el color del nodo i.
■ Devuelve el tamaño del subárbol más grande cuyos nodos son del mismo color.

TEN TERRITOR TEN ANTE ANTERIOR
Silencio...
[0,2], [0,3], colores = [1,1,2,3]
[0,2], [0,3]], colores = [1,1,1,1].
[0,2],[2,3], [2,4]], colores = [1,2,3,3,3].

-...

## 2. Intuition " Why DFS Works

Un subárbol es *homogéneo* sólo si cada niño subárbol es también homogéneo **y** comparte el mismo color que la raíz.
Durante el DFS podemos ** devolver dos piezas de información** para cada nodo:

1. ¿El subárbol está arraigado aquí homogéneo? * *
* Si sí → tamaño del subárbol (para respuesta potencial).
* Si no → `-1` ( significa “romper la cadena”).
2. **Maximum homogeneous subtree seen so far in the recursive call**.

Cuando un padre procesa a un niño:

* Si el subárbol del niño es homogéneo * y* el color del niño es igual al del padre, podemos combinar con seguridad sus tamaños.
* De lo contrario el subárbol de los padres se convierte en "mixed" (`-1`).

Este **back-tracking** garantiza que inspeccionamos cada nodo sólo una vez → `O(n)`.

-...

## 3. El “bueno, el malo”

**Aspecto** Silencio**
Silencio----------------------------------------------------
Silencio ** Algorithm** ← Simple DFS, intuitivo, tiempo lineal ¦ La profundidad de la Recursión puede alcanzar el límite de la pila para 5×104 nodos ← Ninguno si se implementa con la pila iterativa
Silencio **Espacio** Silencioso O(n) lista de adyacencia + O(n) pila de recursión Silencio La pila de Recursión puede volar en árboles degenerados.
Silencio ** readability del proyecto** Silencio Muy compacto, de dos valores array retorno Silencio La matriz de dos valores puede ser confusa Silencio Algunas implementaciones usan los vapores globales que hacen daño a la claridad
Silencio **Problemas de emergencia** Silencio Trabaja para un solo nodo, todo el mismo color, todo diferente Silencio Debe manejar la raíz sin niños

-...

## 4. Implementaciones de referencia

A continuación encontrará tres implementaciones pulidas.
Todos comparten la misma idea básica pero son idiomáticos a su idioma.

■ **Tip**: La lista de adyacency se construye en el tiempo `O(n).
■ El DFS se implementa recursivamente (sin tacto para convertirlo a iterativo si la profundidad de pila es una preocupación).
■ El par devuelto `[subtreeSize, maxSize]` está empacado como un array / tuple / struct.

### 4.1 Java (≤ Java 17)

``java
importar java.util*;

Solución de la clase pública {}
// método público como LeetCode espera
public int maximumSubtreeSize(int[][] edges, int[] colors) {}
int n = edges.length + 1;
Lista de datos gráfico = buildGraph(n, edges);
retorno dfs(0, -1, gráfico, colores)[1];
}

// DFS devuelve {subtreeSize, bestSize}
int privado[] dfs(int u, int parent, List Garantizado[] grafito, int[] colores
int current = 1; // size if homogeneous so far
int best = 0; // mejor visto en niños

para (int v : graph[u]) {}
si (v == padre) continúan;

int[] res = dfs(v, u, graph, colors);
int childSize = res[0];
mejor = Math.max(mejor, res[1]);

si (niños tamaño != -1 < colores[v] == colores[u] {}
actual += niño tamaño; / / / / fusión niño
. ♫ ... {
corriente = -1; // subárbol se mezcla
}
}
volver nuevo int[]{current, Math.max(current, best)};
}

Lista privada hecha Integer confianza[] buildGraph(int n, int[][] edges) {
Lista realizadaInteger() g = nuevo ArrayList[n];
para (int i = 0; i) no; i++) g[i] = nuevo ArrayList recomendado();
para (int[] e : bordes) {
g[e[0].add(e[1]);
g[e[1]].add(e[0]);
}
retorno g;
}
}
`` `

### 4.2 Python (Python 3.8+)

``python
de las colecciones importadas por defecto
de la importación Lista

Solución de clase:
def máximoSubtreeSize(self, edges: List[List[int], colors: List[int]) - título int:
n = len(colores)
g = defaultdict(list)
para u, v en los bordes:
g[u].append(v)
g[v].append(u)

def dfs(u: int, parent: int):
cur = 1 # tamaño si homogéneo
mejor = 0 # mejor visto en subtrees
for v in g[u]:
si v == padre: continuar
child_size, child_best = dfs(v, u)
mejor = max(best, child_best)

si niño_size != -1 y colores [v] == colores[u]:
cur += child_size
más:
cur = 1
volver cur, max(cur, best)

_, ans = dfs(0, -1)
Retorno
`` `

### 4.3 C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maximumSubtreeSize(vector seleccionadovector seleccionador seleccionado) {}
int n = colors.size();
vector realizador:
para (auto &e : bordes) {}
g[e[0].push_back(e[1]);
g[e[1]].push_back(e[0]);
}

función recomendadapair realizadaint,intenta(int,int)](int u, int p) {
int cur = 1; // tamaño si homogénea
int best = 0; // best in children
para (int v : g[u]) {}
si (v == p) continúan;
auto [childSize, childBest] = dfs(v, u);
mejor = max(best, childBest);

si (niños tamaño != -1 < colores[v] == colores[u]
cur += ChildSize;
más
cur = -1;
}
volver make_pair(cur, max(cur, best));
};

dfs(0, -1).second;
}
};
`` `

-...

## 5. Análisis de la complejidad

TEN ANTE TEN ANTE Java ANTERIOR Python
Silencio------------...
Silencio ** Tiempo** Silencioso `O(n)` Silencio `O(n)` Silencio `O(n)` Silencio
Silencioso **Espacio** Silencioso `O(n)` apilación de adyacencia + recursión + recursión Silencio

■ **Nota**: La profundidad de recursión es igual a la altura del árbol. En el peor de los casos (lista conectada) profundidad = `n`. Para `n ≤ 5·104` cabe en la mayoría de los entornos de tiempo de ejecución, pero si usted golpeó los límites de la pila cambiar a una pila iterativa.

-...

## 6. Variaciones " Extensiones

TENIDO Variación ANTERIOR Cómo retocar
Silencio--------------
tención **Fraígenes mínimas** ← Construir un bosque; ejecutar DFS de cada componente. Silencio
Silencio **Colores ponderados** Silencio Mantén la pista de colores como cuerdas o objetos. Silencio
Silencio **Preguntas sínmicas** Silencio Pre-compute subtree tamaños; respuesta preguntas en `O(1)`. Silencio
Silencio **Iterative DFS** ← Uso explícita de la pila & par de (nodo, estado del iterador). Silencio
Silencio **Parallel DFS** Silencio Para árboles enormes, dividir subárboles a través de hilos. Silencio

-...

## 7. SEO‐Friendly Takeaway

- **Keywords**: `LeetCode 3004`, `Maximum Subtree of the Same Color`, `Tree DFS`, `Tree DP`, `Java solution`, `Python solution`, `C++ solution`, `Job interview algoritmos`, `Graph theory`, `Data structures`, `Competitive programming`.
- **Meta Descripción** (para motores de búsqueda de blogs):
■ “Master LeetCode 3004 – Máximo Subtree del mismo color. Lea nuestra solución completa en Java, Python & C++ con explicación paso a paso, análisis de complejidad y conocimientos de entrevista. Perfecto para reclutadores y auto-estudio. ”

- ** Estructura de carga** (H1‐H3) garantiza que los motores de búsqueda vean el flujo:
`` `
# LeetCode 3004 – Maximum Subtree of the Same Color
## Problema Declaración
Intuición
## Good, Bad & Ugly
Java/Python/C++ Código
## Complexity Analysis
`` `

- ¿Qué? Compartir el artículo en LinkedIn, Reddit r/cscareerquestions, y foros de programación relevantes. Mención “listo para usar el código de entrevistas” para captar interés del reclutador.

-...

## 8. Conclusión

El crux de **LeetCode 3004** es un *simple* DFS que devuelve un par de valores.
El algoritmo es óptimo (`O(n)`) y fácil de entender, por lo que es un excelente punto de referencia en una entrevista técnica.

■ **Pro tip**: Si te estás preparando para una entrevista, recuerda a **explicar el retroceso** y por qué un subárbol homogéneo se rompe tan pronto como se encuentra un desajuste. Amo del equipo al verlo pensar en términos de *state* y *memoization* incluso en un problema “O(n)”.

¡Feliz codificación y buena suerte en tu próxima entrevista de trabajo! 🚀

-..