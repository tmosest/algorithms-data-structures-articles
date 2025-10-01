-...
Título: LeetCode 545. Boundary of Binary Tree -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 545 – Frontera de Árbol binario
**Medium ← Árbol binario Silencioso DFS / Recursión Tiempo O(n) Silencioso Espacio O(h)**

A continuación encontrará soluciones de trabajo completo en **Java, Python y C++**.
Después del código hemos escrito un breve artículo de estilo "blog-style" que explica el algoritmo, destaca el bueno, el malo, y el feo, y está escrito con palabras clave optimizadas SEO que a los reclutadores les encanta ver en su cartera o GitHub README.

-...

### 1. Solución Java

``java
importa java.util. ArrayList;
importa java.util. Lista;

* Definición para un nodo de árbol binario. */
clase pública TreeNode {
int val;
TreeNode left;
TreeNode right;
TreeNode(int x) { val = x; }
}

Solución de la clase pública {}

public List won OfBinaryTree(TreeNode root) {
Lista de resultadosInteger título = nuevo ArrayList implicado();
si (root == null) resultado de retorno;

si (!isLeaf(root)) resultado.add(root.val);

// 1. Límite izquierdo (excluidas las hojas)
TreeNode cur = root.left;
mientras (curre!= null) {
si (!isLeaf(cur)) resultado.add(cur.val);
cur = (cur.left!= null) ? cur.left : cur.right;
}

// 2. Todas las hojas (izquierda a derecha)
addLeaves(root, result);

// 3. Límite derecho (excluidas las hojas), añadir en inversa
Lista Nombramiento:Integer derechoBoundary = nuevo ArrayList recomendado();
cur = root.right;
mientras (curre!= null) {
(!isLeaf(cur))) rightBoundary.add(cur.val);
cur = (cur.right!= null) ? cur.right : cur.left;
}
for (int i = rightBoundary.size() - 1; i > 0; --i)
result.add(rightBoundary.get(i));

Resultado de retorno;
}

vacío privado añadirLeaves(TreeNode node, Lista de productos) {
si (nodo == nulo) regresa;
si (esLeaf(nodo))) {}
out.add(node.val);
retorno;
}
addLeaves(node.left, out);
addLeaves(node.right, out);
}

booleano privado isLeaf(TreeNode node) {
Nodo de retorno. izquierda == null " Node. derecho == nulo;
}
}
`` `

-...

### 2. Solución de pitón

``python
de la importación List, Optional

Definición para un nodo de árbol binario.
Clase TreeNode:
def __init__(self, val: int = 0, left: 'TreeNode' = Ninguno, right: 'TreeNode' = Ninguno):
self.val = val
autoizquierda
self.right = right

Solución de clase:
def boundary OfBinaryTree(self, root: Optional[TreeNode]) - título List[int]:
si no raíz: retorno []

res = []

# Root (si no una hoja)
si no es uno mismo._is_leaf(root):
re.append(root.val)

# Límite izquierdo (excluyendo hojas)
nodo = root.left
mientras nodo:
si no uno mismo._es_leaf(nodo):
re.append(node.val)
nodo = nodo.izquierda si nodo. Nodo izquierdo. derecho

# Leaves
auto._add_leaves(root, res)

# Límite derecho (excluyendo las hojas) – recoger luego reverso
right_boundary = []
nodo = root.right
mientras nodo:
si no uno mismo._es_leaf(nodo):
right_boundary.append(node.val)
nodo = nodo. nodo derecho. izquierda
res.extend(reversed(right_boundary))

retorno

def _add_leaves(self, node: Optional[TreeNode], out: List[int]) - título Ninguno.
si no el nodo:
Regreso
si yo.
out.append(node.val)
Regreso
auto._add_leaves(node.left, out)
auto._add_leaves(node.right, out)

@staticmethod
def _is_leaf(nodo: TreeNode) - título bool:
Nodo de retorno. La izquierda es Ninguno y nodo. Bien.
`` `

-...

### 3. Solución C++

``cpp
Incluido el título
usando std namespace;

/* Definición para un nodo de árbol binario. */
struct TreeNode {
int val;
TreeNode *left;
TreeNode *right;
TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

Clase Solución {
public:
vectorial horizontal OfBinaryTree(TreeNode* root) {
vector significar uns
si (!root) devuelve ans;

si (!isLeaf(root)) ans.push_back(root- Confval);

// Límite izquierdo (excluidas las hojas)
TreeNode* cur = root-propleft;
mientras que (cur) {
si (!isLeaf(cur))) ans.push_back(cur- Confval);
cur = (cur- títuloleft) ? cur- títuloleft : cur- título;
}

// Hojas
addLeaves(root, ans);

// Límite derecho (excluyendo las hojas) – coleccionar luego reverso
vector rightB;
cur = root- tituladoright;
mientras que (cur) {
(!isLeaf(cur))) rightB.push_back(cur- Confval);
cur = (cur- título) ? cur- título: cur- títuloleft;
}
para (auto it = rightB.rbegin(); it != rightB.rend(); ++it)
ans.push_back(*it);

devolver los ans;
}

privado:
bool isLeaf(TreeNode* node) {
nodo de retorno - título == nullptr " curva node " == nullptr;
}

vacio añadirLeaves(TreeNode* nodo, vector asignadoint
si (!node) regresa;
si (esLeaf(nodo))) {}
out.push_back(node- Confval);
retorno;
}
addLeaves(node-propleft, out);
addLeaves(node-Conderight, out);
}
};
`` `

■ **Consejo:** En los tres idiomas la idea central es la misma: *FDAS con tres pases*:
■ 1. Límite izquierdo (de arriba a abajo, hojas de salto)
■ 2. Todas las hojas (izquierda a derecha)
■ 3. Límite derecho (de arriba a abajo, hojas de salto) pero añadido en orden inverso

-...

##  tuya Blog‐Style Write‐up: "Boundary of Binary Tree – Good, Bad & Ugly"

■ **Keywords**: *LeetCode 545, Boundary of Binary Árbol, traversal de árboles binarios, DFS, algoritmo de entrevista, entrevista de ingeniero de software, entrevista de codificación, complejidad del tiempo, complejidad del espacio, consejos de entrevista de trabajo. *

-...

#### ## 1down⃣ El Bien

Silencio ¿Por qué este algoritmo brilla ¦
Silencio...
La solución es sólo unos cuantos lazos y un colector de hoja recurrente. No hay máquina de estado adicional o lógica de bandera. *Clear, readable code*
Silencio **Linear Time** – Cada nodo es visitado al máximo una vez → **O(n)**. Perfecto para árboles grandes.
Silencio **Espacio auxiliar** – Sólo profundidad de recursión (`O(h)`) y algunas listas auxiliares (`O(h)`). *Espacio optimizado*
Silencio **Extensible** – Puedes conectar esta rutina a cualquier sistema de entrevista o producción que necesite una vista de “periferia del árbol”. *Programa de código reutilizable*
Silencio **No Doble Countura** – Las hojas se añaden sólo una vez, si aparecen en un límite o no. * Garantizar sin problemas*

■ **Recruiter-friendly takeaway**: *“Puedo producir limpio, O(n) código del árbol-traversal que evita trampas comunes como hojas de doble venta.”*

-...

#### 2down⃣ El malo

Silencio Puntos de dolor comunes Silencio
Silencio...
Silencio **Null root** – La declaración del problema garantiza una raíz, pero la codificación defensiva sigue siendo sabia. Silencio Check for `root == null` early. Silencio
tención **Nodos de límites individuales** – Un nodo con sólo un niño debe ser considerado parte de la frontera. Utilice el “si la izquierda existe otra derecha” (y vice-versa para el límite derecho). Silencio
*Root siendo una hoja* En ese caso el límite es simplemente `[root.val]`. tención Saltar añadir `root` cuando es una hoja. Silencio
En Python el límite de recursión puede golpear `sys.setrecursionlimit`, en C++ los controles puntero deben tener cuidado. Mantenga la profundidad de recursión en mente, o cambie a una pila iterativa si `h` podría ser enorme. Silencio

-...

#### 3down⃣ El Ugly

Silencio Cuando el código parece un monstruo de espaguetis
Silencio...
← Sobre-ingeniería con enteros “flag” (1 = izquierda, 2 = derecha, 3 = otros) y métodos de ayuda múltiple sólo para hacer un seguimiento de “donde estamos” es ** innecesario** para este problema. Hace que el código sea más difícil de leer y más error-prone. Silencio
Silencio Utilizar un `vector seleccionadoint] global y mutarlo de la recidiva profunda puede ser difícil de depurar, especialmente en C++ donde la gestión manual de memoria está involucrada. Silencio
Silencio Olvidar saltar las hojas al añadir el límite izquierdo/derecho suele llevar a duplicar los valores en la lista final. Un enfoque “simple‐first” que añade la raíz, el límite izquierdo, las hojas, el límite derecho – y luego de-duplicados – es más limpio. Silencio

■ **Take‐away**: *Escribe el DFS más simple que satisface las reglas del límite. Evite banderas ocultas o máquinas estatales a menos que la entrevista los requiera explícitamente. *

-...

Resumen optimizado

Si usted está construyendo un GitHub README, una página de portafolio, o preparando un conjunto de soluciones **LeetCode** para impresionar a los gerentes de contratación, utilice los siguientes meta-tags, encabezados y oraciones de keyword-dense:

- `#LeetCode545`, `#BoundaryOfBinaryTree`, `#BinaryTreeTraversal`, `#DFS`, `#Recursion`, `#Entreview Algorithm`, `#SoftwareEngineer`, `#CodingInterview`, `#JobInterview`, `# AlgorithmDesign`, `#TimeComplexity`, `#SpaceComplexity `

# Sample README snippet #

``markdown
# Boundary of Binary Tree – LeetCode 545

- **Problema**: Computar el límite de un árbol binario (izquierda, hojas, límite derecho) en tiempo O(n).
- ** Idiomas**: Java, Python, C++.
- ** complejidades**: `O(n)` tiempo, `O(h)` espacio auxiliar (`h` = altura de los árboles).
- **Por qué importa**: Demuestra la búsqueda de profundidad, el manejo de los bordes y el código limpio – habilidades clave para una entrevista de ingeniero de software.
`` `

■ **Por qué esto importa para su búsqueda de trabajo* *
■ Búsqueda de reclutadores para candidatos que pueden **solver problemas de árboles clásicos** rápidamente y con código limpio. Añadiendo este problema (LeetCode 545) a tu repo público y escribiendo un blog que explica * buenas, malas, feas* ideas, muestras:
* habilidades de solución de problemas
* Responsabilidad del código "
* Comprensión del tiempo " intercambio espacial
* Capacidad para comunicar ideas complejas en un formato digestible

-...

#### 5down⃣ Harness de prueba rápida (Opcional)

``java
public static void main(String[] args) {
/* Construir el siguiente árbol
1
/ \
2 3
/ \ \ \
4 5 7
*/
TreeNode root = nuevo TreeNode(1);
root.left = nuevo TreeNode(2);
root.right = nuevo TreeNode(3);
root.left.left = nuevo TreeNode(4);
root.left.right = nuevo TreeNode(5);
root.right.right = new TreeNode(7);

Solución sol = nueva solución ();
System.out.println(sol.boundaryOfBinaryTree(root)); // - título [1, 2, 4, 5, 7, 3]
}
`` `

-...

### 🎯 Cómo utilizar estas soluciones en su cartera de entrevistas

1. ** Subir los tres archivos fuente** (`Solution.java`, `solution.py`, `solution.cpp`) a un gitHub repo.
2. Añada el artículo **blog** como `README.md` o un archivo separado `blog.md`.
3. En su página de LinkedIn o portafolio, enlace con el repo y mención *“Solved LeetCode 545 – Frontera de Árbol binario con O(n) DFS”*.
4. Cuando se aplique, agregue el siguiente fragmento a su carta de portada o LinkedIn:

■ * Durante mi reciente preparación para la entrevista, me enfrenté a LeetCode 545 – Boundary of Binary Tree, implementando una solución limpia y lineal en Java, Python y C++. El algoritmo muestra mi capacidad de realizar DFS en árboles binarios, gestionar la lógica de la periferia, y producir código de producción listo.”*

-...

**Feliz codificación " la mejor suerte de aterrizaje que el próximo papel de ingeniería de software!** 🚀