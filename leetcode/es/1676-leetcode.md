-...
Título: LeetCode 1676. Ancestro común más bajo de un árbol binario IV -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código - Tres idiomas

A continuación encontrará una solución **single‐pass, O(N) time / O(H) space**
LeetCode 1676 – *Más bajo Ancestro Común de un Árbol binario IV*.
El código está escrito en **Java, Python, y C++** para que puedas pegarlo en el
correspondientes jueces en línea o sus propios proyectos.

■ ¿Por qué esta versión? * *
* Usa un `HashSet` (o `unordered_set`) para pruebas de membresía O(1).
* Recursivamente cuenta cuántos de los nodos de destino aparecen en cada subárbol.
* El primer nodo que contiene todos los nodos blancos en su subárbol es el LCA.
* No hay estructuras de datos adicionales (además del set) – mínima sobrecarga.

-...

## Java (LeetCode style)

``java
// Definición para un nodo de árbol binario.
clase TreeNode
int val;
TreeNode left;
TreeNode right;
TreeNode(int x) { val = x; }
}

Clase Solución {
privado TreeNode ans = null;
Conjunto privado objetivo Set;

public TreeNode lowestCommonAncestor(TreeNode root, TreeNode[] nodos) {}
si (root == null) vuelve nula;

objetivo Set = nuevo HashSet Garantizado(Arrays.asList(nodes));
dfs(root);
devolver los ans;
}

// Devuelve cuántos nodos blancos se encontraron en este subárbol
int privado dfs(TreeNode node) {
si (nodo == nulo) devuelve 0;

int count = 0;
si (targetSet.contains(node)) cuenta++;

contar += dfs(node.left);
contar += dfs(node.right);

// Si este subárbol contiene todos los nodos objetivos y aún no hemos establecido la respuesta
si (cuenta == targetSet.size() " afectadas ans == null) {
ans = nodo;
}
recuento de retorno;
}
}
`` `

-...

## Python 3

``python
Definición para un nodo de árbol binario.
Clase TreeNode:
def __init__(self, x):
self.val = x
self.left = Ninguno
self.right = Ninguno

Solución de clase:
def más bajoCommonAncestor(self, root: 'TreeNode', nodos: list['TreeNode']) - título "TreeNode"
si no raíz:
No.

target_set = set(nodos)
self.ans = Ninguno

def dfs(nodo: TreeNode) - título int:
si no el nodo:
retorno 0
cuenta = 1 si nodo en target_set 0
contar += dfs(node.left)
contar += dfs(node.right)

si cuenta == len(target_set) y auto. El culo es Ninguno:
self.ans = node
cuenta de retorno

dfs(root)
Vuélvete. ans
`` `

-...

## C++ (GNU‐C+17)

``cpp
*
* Definición para un nodo de árbol binario.
* struct TreeNode {
* int val;
* TreeNode *left;
* TreeNode *right;
* TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
* };
*/
Clase Solución {
public:
TreeNode* más bajoCommonAncestor(TreeNode* root, vector seleccionadoTreeNode* implicado nodes) {}
si (!root) regresa nullptr;
unordered_set realizadoTreeNode* Fuente(nodes.begin(), nodes.end());
ans = nullptr;
dfs(root, target);
devolver los ans;
}

privado:
TreeNode* ans = nullptr;

// devuelve cuántos nodos objetivos se encontraron en este subárbol
int dfs(TreeNode* node, unordered_set interpretadoTreeNode*⁄2⁄4e objetivo) {}
si (!node) devuelve 0;

int cnt = target.count(node) ? 1 : 0;
cnt += dfs(node- títuloleft, target);
cnt += dfs(node-principal, target);

si (cnt == target.size() " afectadas !ans) ans = nodo;
cnt de retorno;
}
};
`` `

-...

## 2. Blog Artículo – *El Bien, el Mal, y el Ugly of LCA (Nodos Multiple)*

### Title
**Más bajo Ancestro Común de Múltiples Nodos en un Árbol binario – Una profunda cueva para las entrevistas* *

## Meta‐Descripción
Desbloquear la solución LeetCode 1676: aprender el mejor algoritmo, comparar las implementaciones Java/Python/C++ y dominar la entrevista “bueno, malo, feo”. Perfecto para los ingenieros de software que preparan para preguntas de estructura de datos.

-...

### 1. Introducción

Cuando piensas en *Lowest Common Ancestor* (LCA) en árboles binarios, el problema de la entrevista clásica es *dos* nodos. LeetCode 1676 lanza un giro: **Dada una serie de nodos, encontrar el LCA de todos ellos**.
Suena trivial, pero las soluciones ingenuas que ves en Internet a menudo ignoran los casos de esquina, explotan la memoria o pierden la garantía *O(N)*.

En este artículo pasaremos por:

Silencio **Aspecto** Silencio **Lo que usted aprenderá**
Silencio...
Silencio Good TENIDO El algoritmo O(N) que funciona para cualquier número de nodos
Silencio ¿Por qué el enfoque de “busca cada par” falla
TENCIÓN Ugly ANTERIÓ trampas ocultas: profundidad de recursión, identidad vs. valor, y fugas de memoria

-...

### 2. Reposición de problemas

■ **Input** –
* `root` – puntero/referencia a la raíz de un árbol binario (los valores son únicos).
* `nodes[]` – un conjunto de objetos **TreeNode** que existen en el árbol.
■
■ **Output** – el TreeNode que es el antepasado común más bajo de *todo* nodo en `nodos[].

■ **Constraints**
1 ≤ N ≤ 104 (número de nodos en el árbol).
* Todos los valores del nodo son únicos.
* Todos los nodos en los nodos son distintos y presentes en el árbol.

-...

### 3. Naïve Approaches (The Bad)

Por qué es problemático
Silencio------------------------------
Silencio **Pairwise LCA** – Compute LCA para cada par, luego fusionarse Silencio O(k2 · h) Silencio k = Silencionodes vidas pueden ser hasta 104; soplo cuadrático. Silencio
tención **Mark " Sweep** – DFS cada nodo objetivo, almacenar ancestros, intersect TEN O(k·h + N) ANTE Requiere memoria O(k·h) para listas de ancestros. Silencio
Silencio **Brute DFS with Set at every node** – Para cada nodo, recopilar todos los objetivos en su subtree Silencio O(N2) ← Re-counts the same subtrees many times. Silencio

Estos patrones son comunes en soluciones “primero-draft” que verá en blogs o foros de discusión. Trabajan para datos pequeños, pero no en las limitaciones.

-...

### 4. Estrategia óptima (el bien)

##### 4.1 Core Idea

Durante una única traversal de profundidad mantenemos un seguimiento de **cuántas de los nodos blancos** aparecen en el subárbol actual.
* Si un subárbol contiene *todas* metas, entonces el nodo actual es el LCA.
* Devolvemos la cuenta al padre para que el antepasado sepa si su propio subárbol es un candidato.

Esto nos da:

* **Tiempo** – Cada nodo es visitado una vez → **
* **Espacio** – Profundidad de la pila de recorsión → **O(H)** donde H es la altura del árbol (≤ N)

##### 4.2 Detalles de la implementación

Silencio Idioma Silencio Notas Especiales
Silencio--------------------------
Silencio **Java** Silencio Usar un `HashSet observadoTreeNode confianza` para O(1) `contains()` cheques. Mantenga un campo mutable `ans` que almacena el primer nodo que satisface la condición del conteo. Silencio
Silencio **Python** Silencio Usar un `set(nodos)`; la recursión devuelve un recuento entero. Use `ans no locales' o un atributo de clase. Silencio
Silencio **C++** Silencio `noordered_set observadoTreeNode* Destino(nodes.begin(), nodes.end());` Recursion devuelve el conteo. Almacene 'ans' como miembro privado. Silencio

##### 4.3 Why It Works

Dejar `k = nodes.length`.
Cuando visitamos un nodo `x`, contamos cuántos de los objetivos 'k' están en sus subárboles izquierdo y derecho, añada 1 si `x` es un objetivo.
* Si la suma es igual a " k " , entonces cada objetivo se encuentra en el subárbol arraigado en `x ' .
* Debido a que pasamos de las hojas hacia arriba, el **primero** tal nodo encontrado es el *oeste*.
* Una vez que se establece que simplemente propagamos el conteo hacia arriba; nunca exageramos.

-...

### 5. Code Walk‐Through (Java Ejemplo)

``java
privado TreeNode ans = null; // almacena el LCA una vez encontrado
set privado seleccionadoTreeNode confianza targetSet; // prueba de membresía rápida

public TreeNode lowestCommonAncestor(TreeNode root, TreeNode[] nodos) {}
si (root == null) vuelve nula;
objetivo Set = nuevo HashSet Garantizado(Arrays.asList(nodes));
dfs(root); // single DFS pass
devolver los ans;
}

int privado dfs(TreeNode node) {
si (nodo == nulo) devuelve 0;
int count = targetSet.contains(node) ? 1 : 0;
contar += dfs(node.left);
contar += dfs(node.right);

si (cuenta == targetSet.size() " afectadas ans == null) {
as = nodo; // primer nodo que cubre todos los objetivos
}
recuento de retorno;
}
`` `

* `dfs` devuelve el número de objetivos encontrados en el subárbol de `nodo`.
* Tan pronto como se establece `ans' dejemos de buscar un candidato más profundo.

-...

### 6. Casos de borde " Pitfalls "

Problema de la vida _ Cómo encontrarlo Silencioso
Silencio...
Silencio *Sólo un nodo objetivo* *Viva LCA debería ser ese nodo en sí mismo* El algoritmo naturalmente maneja esto: `contra == 1`. Silencio
Silencio **Identidad del nodo vs. valor** Silencio Dos nodos pueden tener el mismo `val` pero son diferentes objetos TEN siempre utilizar la *identidad del objeto* ( ' referencia del nodo) en el conjunto, no el valor entero. Silencio
Silencio **Recidiva profunda** Silencio Altura del árbol cerca de N (104) → Apilar el desbordamiento en Java/Python TEN Utilizar DFS iterante o aumentar el límite de recursión (`sys.setrecursionlimit`). Silencio
Silencio **Memoria fuga en C+** Silencio Olvídate de eliminar local `unordered_set` si lo asignas dentro de un helper ¦ Allocate una vez en el método público; el ayudante lo recibe por referencia. Silencio
Silencio **Null pointer checks** tención LeetCode garantiza `root != null`, pero los `dfs' locales todavía deben proteger contra los `null` niños Silencio Todos los tres snippets comienzan con `if (node == null) retorno 0;`. Silencio

-...

### 7. Entrevista Aways

Respuesta a la respuesta
Silencio...
*¿Cuál es la complejidad del tiempo de su solución?* Silencio **O(N)** – una visita DFS por nodo. Silencio
*¿Por qué necesitamos un HashSet?* Silencio **O(1)** pruebas de membresía; sin él estaríamos haciendo O(N2). Silencio
*¿Cómo garantizas que estás devolviendo el antepasado más bajo?* El primer nodo cuyo subárbol cuenta iguala `k` es el más bajo porque nos estamos moviendo de hojas a raíz. Silencio
*¿Qué hay del uso del espacio?* Sólo pila de recursión – **O(H)**, no O(N) a menos que el árbol sea degenerado. Silencio

-...

### 7. Resumen

Silencio**
Silencio--------------------------
Silencio Un paso DFS, O(N) tiempo, O(H) espacio Ø Quadratic pairwise LCA, O(k2·h) Silencio Identidad vs. errores de valor, límites de profundidad de recursión
Silencio Usa un `HashSet` para la membresía de tiempo constante ← Requiere múltiples traversales ← Uninitialized `ans` puede llevar a respuestas incorrectas Silencio

Con las tres implementaciones listas para copiar arriba usted puede golpear con confianza el *“LeetCode 1676 – Lowest Common Ancestor of a Binary Tree IV”* en cualquier plataforma y clavo que entrevista la pregunta.

-...

### 8. Pensamiento final

■ **Práctica, práctica, práctica. #
■ Intente escribir el DFS usted mismo desde cero en cada idioma.
■ Luego, cambie el árbol (skewed, balanceado, aleatorio) y realice las mismas pruebas – verá el escalado lineal que importa.

¡Feliz codificación y buena suerte en tu próxima entrevista!