-...
Título: LeetCode 3249. Cuenta el número de buenas nodas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código – 3 idiomas

■ **Problema (LeetCode 3249 – Cuenta el número de buenas nodas)* *
■ Se le da un árbol arraigado (root = 0).
■ Un nodo es **buena** si cada subárbol arraigado en sus hijos tiene el mismo tamaño (número de nodos).
■ Devuelve el número de nodos buenos.

Las siguientes soluciones siguen la misma idea:
1. Construya una lista de adyacencia.
2. Ejecute un DFS de la raíz para calcular el tamaño del subárbol de cada nodo.
3. Para cada nodo comprobar que todos sus hijos tienen tamaños idénticos.

``cpp
// =============================================================== C++ ===============================================================

#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector asignado a la lista de productos
vector asignadoint título sz; // tamaño del subárbol

int dfs(int v, int p) {}
int cur = 1; // contar el nodo en sí
para (int nb : g[v]) {}
si (nb == p) continúan;
cur += dfs(nb, v);
}
sz[v] = cur;
Volver cur;
}

int countGoodNodes(vector seleccionadovector identificadointюще bordes) {}
int n = edges.size() + 1;
g.assign(n, {});
sz.assign(n, 0);

// construir gráfico bidireccional
para (auto &e : bordes) {}
g[e[0].push_back(e[1]);
g[e[1]].push_back(e[0]);
}

dfs(0, -1); // compute subtree size

int ans = 0;
para (int v = 0; v) {}
bool good = true;
int childSize = -1;
para (int nb : g[v]) {}
si (sz[nb] < sz[v] { // nb es un niño
si (niños tamaño == -1) ChildSize = sz[nb];
si (niños tamaño != sz[nb]) { bueno = falso; romper; }
}
}
si (bueno) ++ans;
}
devolver los ans;
}
};
`` `

``java
// =============================================================== Java ===============================================================

importar java.util*;

Solución de la clase pública {}
privada Lista hecha Gráfico;
int privado[] tamaño; // tamaño de subárbol

int privado dfs(int v, int parent) {
int cur = 1; // se cuenta
para (int nb : graph.get(v)) {}
si (nb == parent) continúan;
cur += dfs(nb, v);
}
tamaño[v] = cur;
Volver cur;
}

int countGoodNodes(int[] edges) {
int n = edges.length + 1;
gráfico = nuevo ArrayList recomendado();
para (int i = 0; i < n; i++) graph.add(new ArrayList correctamente());
tamaño = nuevo int[n];

// construir una lista de adjacency no redirigida
para (int[] e : bordes) {
graph.get(e[0]).add(e[1]);
graph.get(e[1]).add(e[0]);
}

dfs(0, -1); // compute subtree size

int ans = 0;
para (int v = 0; v) {}
bien booleano = verdadero;
int childSize = -1;
para (int nb : graph.get(v)) {}
si (tamaño[nb] [v]) { // nb es un niño
si (niños tamaño == -1) ChildSize = size[nb];
si (niños tamaño != tamaño[nb]) { bueno = falso; romper; }
}
}
si (bueno) ans+;
}
devolver los ans;
}
}
`` `

``python
# =============================================================== Python ===============================================================

de las colecciones importadas por defecto
de la importación Lista

Solución de clase:
def count GoodNodes(self, edges: List[List[int]) - título int:
n = len(edges) + 1
g = defaultdict(list)
tamaño = [0]

# Build adjacency list
para a, b en los bordes:
g[a].append(b)
g[b].append(a)

# DFS to compute subtree size
def dfs(v: int, p: int) - int:
Cur = 1
para nb en g [v]:
si nb == p:
continuar
cur += dfs(nb, v)
tamaño[v] = curtido
Retorno

dfs(0, -1)

# Cuenta buenos nodos
ans = 0
para v en el rango(n):
Bien = Verdadero
child_size = 1
para nb en g [v]:
si el tamaño[nb]
si el niño_size == -1:
child_size = size[nb]
elif child_size != size[nb]:
bueno = Falso
descanso
si es bueno:
ans += 1
Retorno
`` `

Los tres códigos se ejecutan en **O(n)** tiempo y **O(n)** memoria (n = #nodes).

-...

## 2. Blog Artículo – “Countar el número de buenos ganglios en un árbol: el bueno, el malo y el ugly”

■ **Meta‐Título**: Maestro LeetCode 3249 – Cuenta el número de buenos nodos
■ **Meta‐Descripción**: Solución paso a paso en C++, Java y Python. Aprende el truco de DFS, análisis de complejidad y consejos de entrevista para “Buenas nodos en un árbol”.

#### Introduction

Si usted está cazando para un trabajo de entrevista de estructura de datos, problemas de LeetCode que combinan la teoría **graph** con la programación **dinámica** son oro.
LeetCode 3249 – *Comentar el número de buenos nodos* es uno de estos problemas.
Prueba su capacidad para atravesar un árbol, calcular tamaños de subárbol y razonar sobre “congruencia infantil”.

En este artículo, diseccionaremos el enfoque **bueno** (fácil de entender), el **bad** (pocas comunes) y el **ugly** (trampas de portafolios). Terminaremos con una solución limpia y lista para la producción en **C+**, Java**, y Python**.

-...

## Problema Recap

Dado un árbol arraigado (root = 0) representado por un array `edges`, cuente los nodos que satisfacen:

■ **Buen Nodo** – Todos los subárboles arraigados en sus hijos tienen el mismo tamaño (número de nodos).

■ **Constraints**
≤ 105
* `edges` es un árbol válido (n-1 bordes, sin ciclos)

-...

### 1. El “bien” – Por qué funciona un DFS simple

Una idea ingenua es forzar cada nodo, contar sus descendientes y comparar los tamaños de los niños.
Pero hacer esto por cada nodo llevaría a O(n2) tiempo.

La visión: **Si conocemos el tamaño de cada subárbol una vez, podemos comprobar la “buena” de cada nodo en O(1)**.

**Steps:**

1. ** Lista de Adjacency** – Construir un gráfico bidireccional de `edges`.
2. **DFS (Depth‐First Search)** – Recursively compute el tamaño del subtree de cada nodo.
3. **Niños de tamaño Comprobación** – Para el nodo `v`, todos los vecinos `u` tal que `size[u] [u] = tamaño[v]` son niños.
Si todos estos niños comparten el mismo tamaño[u]`, entonces `v` es bueno.

El DFS funciona una vez, dando **O(n)** tiempo y **O(n)** memoria.

-...

### 2. El “Bad” – Errores comunes

¿Por qué no se puede arreglar la vida?
Silencio--------------------------
Silencio **Usando la lista de adyacency pero olvidando al padre** Silencio Usted va a doble cuenta el padre como un niño, tamaños de coser. Pase "Padre" en DFS y salta. Silencio
Silencio **Comparar los tamaños de los niños al tamaño del nodo** ← El tamaño de los niños es siempre menos que el tamaño del padre; la igualdad nunca es verdadera. tención Compare a los niños entre sí, no con los padres. Silencio
Silencio **Assuming root has no children** Silencio Una raíz todavía puede ser buena si todos sus sub-subtrees son iguales. ¦ Treat root igual que cualquier otro nodo. Silencio
TEN **El uso de la recursión sin optimización de la recursión de la cola** TENIDO Para n = 105 árboles profundos, la profundidad de recursión puede soplar la pila en algunos idiomas. TEN En C++/Java, aumentar el tamaño de la pila o convertir a DFS iterante. Python: use `sys.setrecursionlimit` o iter stackative. Silencio

-...

### 3. Los “Ugly” – Casos de borde y Pitfalls

Silencio Caso Edge Silencio ¿Qué puede pasar mal?
Silencio----------------------------
Silencio **Arbol de estrellas** (raíz conectada a todas las hojas) Silencio Todas las hojas son niños con tamaño 1, hijos de raíz todos iguales → raíz es buena. Sin manejo especial; algoritmo naturalmente maneja. Silencio
Silencio ** Árbol blanco** (pata) Silencio Cada nodo tiene un niño → trivialmente bueno. tención Funciona, pero ten cuidado al computar `niñez = -1`. Silencio
Silencio ** Árbol profundo muy profundo** (a fondo ♥ n) Silencio Profundidad de la Recursión. Silencio Aumentar la profundidad de recursión o utilizar la pila iterativa. Silencio
Silencio **Introducción alta** (n = 105) Silencio Usar listas de Python para la adyacencia puede causar problemas de memoria si no se pre-alentado. Silencio Pre-allocalizar listas o utilizar `defaultdict(list)` y confiar en el administrador de memoria de CPython. Silencio

-...

### 4. Solución completa – avance del código

A continuación se encuentra la implementación más limpia que jamás verás. Es la misma lógica, pero escrita una vez para **C+**, Java**, y Python**.

■ **¿Por qué es una solución de producción? #
* Un DFS, un pase para contar buenos nodos.
* Usa sólo listas de adyacency – no estructuras de datos adicionales.
* Maneja todos los casos de borde.
* Nombres variables claros: `graph`, `size`, `good`.

Vea la sección de código en la parte superior de esta página. Siéntete libre de copiar-paste en tu caja de arena LeetCode.

-...

### 5. Análisis de la complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio Construir la lista de adyacencia Silencio **O(n)** Silencio **O(n)**
Silencio DFS subtree sizes Silencio **O(n)** Silencio **O(n)** (call stack)
Silencio Contar buenos nodos Silencio **O(n)** Silencio **O(1)**

Total: **Hora O(n)**, **Pace O(n)**.
La complejidad del tiempo lineal satisface la restricción estrecha `n ≤ 105`.

-...

### 6. Consejos de entrevista – Cómo hacer realidad esta pregunta

1. ** Explique el DAAT en una frase**: “Computamos tamaños de subárbol en un solo DFS, luego comparamos los tamaños de los niños. ”
2. **Mención del cheque de padre** – a los entrevistadores les encanta ver el parámetro 'padre'.
3. **Mostrar su proceso de pensamiento**: "¿Por qué no O(n2)? ¿Cómo reducirlo? ”
4. ** Casos de bordes de alta luz** – pregunte al entrevistador si quieren que se ocupe de la recidiva profunda.
5. **Un truco opcional** – si el entrevistador lo quiere, puede modificar el DFS para devolver también el “niñez” y evitar un segundo bucle.

-...

### 6.1 Bono – Prueba tu entendimiento

Agregue una prueba rápida de cordura a su entorno:

``python
# Prueba de árbol de estrellas
bordes = [0, i] para i en rango(1, 100000)]
print(Solution().countGoodNodes(edges))) # debe devolver 100000
`` `

Si te sientes cómodo con este snippet, estás listo para la pregunta de entrevista de “Buenas nodos en un árbol”.

-...

### 6. Pensamientos finales

LeetCode 3249 es más que una pregunta de truco – es un micro-exámen de traversal gráfico, DP, y un razonamiento cuidadoso.
Al dominar el patrón de consistencia **DFS + tamaño infantil**, ganarás confianza para abordar una serie de problemas de estilo “contar los buenos nodos”.

Buena suerte en su próxima entrevista, y no olvides practicar más árbol‐ ¡Problemas DP!

-...

## Call‐to‐Action

* Inténtalo ahora* Copia el código C++, Java o Python en LeetCode y resuelve 3249 en minutos.
* **Compartir** este artículo con amigos preparando entrevistas.
* **Suscribir** para inmersiones más profundas en la teoría del gráfico y DP en LeetCode.

-...

**Author**: [Su nombre] – Aficionado a la estructura de datos, colaborador de código abierto y entrenador de entrevista de codificación.
**Contacto**: `remail@example.com `
**Siguiente**: @YourHandle on Twitter, GitHub, Linked In

-...

¡Feliz codificación!

-...

### End of Article

-...

Este artículo debe darle un ** camino de aprendizaje claro**: captar el concepto, evitar las trampas, manejar los casos de borde, e implementar una solución rápida.
Pásalo con los snippets de código listos para usar arriba, y estás listo para la pregunta de entrevista de “buenos nodos” – ¡sin sorpresas “muy”!

-...

¡Buena suerte en tus entrevistas de codificación! *

-...

**Nota**: Todas las URL, etiquetas y metadatos son titulares de lugares; sustitúyalos por su cuenta si está publicando en un blog personal o en un sitio web de búsqueda de empleo.