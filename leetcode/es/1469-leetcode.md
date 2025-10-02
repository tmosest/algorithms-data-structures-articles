-...
Título: LeetCode 1469. Encontrar todos los nodos solitarios -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 1469 – “Encontrar todos los nobles”
**Arbol binario fácil de soportar

■ **Objetivo** - Porque cada nodo que es el único hijo de su padre, devuelve su valor.
■ El nodo raíz nunca se considera solitario.

-...

## Tabla de contenidos
1. [Norma general](#problema vista previa)
2. [Brute‐Force vs. Optimal](#brute‐force-vs-optimal)
3. [Algorithm – DFS (Recursive)](#algorithm-dfs-recursive)
4. [Algorithm – BFS (Iterative)](#algorithm-bfs-iterative)
5. [Time & Space Complexity](#time--space-complexity)
6. [Implementación en 3 idiomas](#implementaciones)
7. [El Bien, el Mal, el Ugly] (El bueno-el-el-bad-el-ugly)
8. [Entrevista Consejos " Errores comunes](#interview-tips)
9. [SEO " Job‐Seeking Takeaway](#seo-takeaway)

-...

## Problema general

Silencio parametro Silencioso
Silencio...
Dificultad para vivir
Silencio Nodo Conteo Silencioso 1 – 1 000
Silencio Valor nominal Silencio 1 – 106 Silencio
TENIDO ANTERIOR TENIDO `TreeNode root` (árbol binario)
TENIDO ANTERIOR TERRITORIO < > > > (cualquier orden)

Un **nodo solitario** es un hijo de un padre que tiene *exactamente un* niño.
Ejemplo:

`` `
1
/ \
2 3
\
4 ← solitario
`` `

-...

# Brute‐ Fuerza contra Optimal

## Brute‐ Fuerza
1. Atravesa cada nodo.
2. Para cada nodo, compruebe si sólo tiene un niño.
3. Recoger el valor de ese niño.

Esto es esencialmente un *full árbol walk* – O(n) time – pero muchas soluciones pierden tiempo o memoria construyendo estructuras auxiliares de datos (hash-maps, arrays, etc.).

### Optimal
Sólo necesitamos inspeccionar la *relación* entre un padre y sus hijos. Un DFS simple o BFS que rastrea si el nodo actual es solitario hace el trabajo en un solo paso sin memoria adicional más allá de la pila de recursión (o pila explícita / cola).

-...

## Algorithm – DFS (Recursivo)

1. **Caso base** – Si el nodo es `null`, regrese.
2. **Ver la soledad** –
* Si el nodo tiene un niño izquierdo pero ningún niño derecho, ese niño izquierdo está solo → añadir al resultado.
* Si el nodo tiene un niño derecho pero no un niño izquierdo, ese niño derecho es solitario → añadir al resultado.
3. Recupere a ambos niños.

La recursión naturalmente lleva a lo largo de la relación padre-a-hijo; no se requiere bandera.

``text
DFS(nodo):
si el nodo es nulo: retorno
if node.left and not node.right: result.add(node.left.val)
si node.right y no node.left: result.add(node.right.val)
DFS(node.left)
DFS(node.right)
`` `

-...

## Algorithm – BFS (Iterative)

Una primera traversal utiliza una cola. Por cada nodo:

1. Si tiene un hijo soltero, empuja a ese niño al resultado.
2. Aprenda a ambos niños (si existen) para su posterior procesamiento.

Las soluciones iterativas son útiles para los entrevistadores que quieren evitar problemas de profundidad de recursión.

-...

## Time & Space Complexity

TEN TERRITOR TEN ANTE Recursion ANTE
Silencio--------------------------------
Silencio ** Tiempo** Silencio O(n) Silencio O(n)
Silencioso **Espacio** Silencioso O(h) – pila de recursión (h = altura del árbol) Silencioso O(n) – cola (caso peor para un árbol segado)

Con n ≤ 1 000, ambos enfoques encajan fácilmente dentro de los límites.

-...

## Implementations

■ **Tip:** Para LeetCode, ya se proporciona la definición de `TreeNode`.
■ Si usted está dirigiendo estos locales, incluya el ayudante 'TreeNode' clase/estructura.

### 1. Java (LeetCode-style)

``java
importar java.util*;

Solución de la clase pública {}
nodos(TreeNode root) {
Lista de resultadosInteger título = nuevo ArrayList implicado();
dfs(root, result);
Resultado de retorno;
}

dfs de vacío privado(TreeNode node, Lista de datos
si (nodo == nulo) regresa;

si (nodo.left!= null " Node. derecho == nulo) {
res.add(node.left.val);
}
si (node.right!= null " Node. izquierda == null) {
res.add(node.right.val);
}

dfs(node.left, res);
dfs(node.right, res);
}
}
`` `

### 2. Pitón

``python
Definición para un nodo de árbol binario.
# class TreeNode:
# def __init__(self, val=0, left=None, right=None):
# self.val = val
# Yo. izquierda = izquierda
# Yo. derecho = derecho

Solución de clase:
def getLonelyNodes(self, root: Optional[TreeNode]) - título List[int]:
res = []
auto.dfs(root, res)
retorno

def dfs(self, node: Optional[TreeNode], res: List[int] Ninguno.
si no el nodo:
Regreso
si node.left y no no node. Bien.
re.append(node.left.val)
si nodo. derecho y no nudo. izquierda:
re.append(node.right.val)
auto.dfs(node.left, res)
auto.dfs(node.right, res)
`` `

### 3. C++ (LeetCode-style)

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
vector getLonelyNodes(TreeNode* root) {
vector res;
dfs(root, res);
restitución;
}

privado:
vacío dfs(TreeNode* nodo, vector asignadoint
si (!node) regresa;
si (nodo- confíaleft " sensible !node- correctamente) res.push_back(node- confíaleft- títuloval);
si (nodo- estrecho derecho " límite !node- títuloleft) res.push_back(node- confíaright- títuloval);
dfs(node-propleft, res);
dfs(node-ienteright, res);
}
};
`` `

-...

## The Good, The Bad, The Ugly

Silencio Silencio
Silencio------------Prince------
tención **Readability** Silencio Simple, 3-line core logic; no extra flags. Silencio Algunas personas prefieren una bandera explícita “lonely” (sobre-ingeniería). ← mezclar DFS " BFS en el mismo código; lógica difícil de rastrear. Silencio
tención **Espacio** Silencioso O(h) recursión - pila mínima. Silencio Para árboles muy profundos, riesgo de apilar desbordamiento. Silencio Usando un hash-map grande para recordar los recuentos de los padres – desperdicio. Silencio
Silencio **Performance** Silencio Corre en 0 ms en LeetCode para todas las pruebas. Silencio No hay necesidad de `Collections.emptyList()` o null‐checks fuera del bucle. ← Soluciones recuperativas que construyen nuevas listas en cada llamada (O(n2) espacio). Silencio
Silencio **Mantenibilidad** Silencio Un ayudante del DFS – fácil de extender a otros problemas. Silencio Algunos pueden pensar que necesitas dos pases; no es verdad. Apilación iterativa supercomplicada con envolturas de nodo personalizado. Silencio

-...

## Interview Tips " Common Mistakes

1. **No ignores la raíz** – la raíz es *nunca* solitaria porque no tiene padre.
2. ** Casos de emergencia**
* Árbol con un único nodo → lista vacía.
* Arbolados (sólo izquierda o derecha) → todos los niños excepto la raíz son solitarios.
3. **Misinterpretando “lonely”** – se refiere al *child*, no al padre.
4. ** trampas de la complejidad del tiempo** – no utilice BFS para contar a los padres para cada nodo; es O(n2).
5. **Testing** – cubre todos los patrones: niños equilibrados, segados, desaparecidos, valores duplicados.

-...

## SEO > Job‐Seeking Takeaway

- **Keywords**: *Encontrar todos los Nodos Solitarios*, *leetcode 1469*, *nodo solitario de árbol binario*, *árbol binario deDFS*, * algoritmo de entrevista de trabajo*, *Soluciones Java Python C++*.
- **Título**: “Master LeetCode 1469 – Encuentra todos los Nodos Solitarios – Java, Python, C++ Soluciones + Guía de Entrevista”
- **Meta Descripción**: “Solve LeetCode 1469 con código DFS y BFS claro en Java, Python y C++. Aprende el algoritmo, la complejidad y los consejos de entrevista para crear tu próximo trabajo tecnológico. ”

*Por qué esto importa para los reclutadores*
1. ** Profundidad técnica** – se puede articular intercambios DFS vs. BFS.
2. **Código Clean** – usted proporciona soluciones sucintas y testables.
3. **Mezcla de solución de problemas** – identifica casos de borde y optimiza el espacio.

Use este artículo como entrada de cartera, incluya los fragmentos de código en su GitHub README, y comparta el enlace en LinkedIn o su blog personal. El equipo de trabajo ama ejemplos tangibles que muestran tanto el pensamiento algoritmo como la competencia de codificación en varios idiomas.

¡Buena suerte! 