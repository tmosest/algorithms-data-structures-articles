-...
Título: LeetCode 2641. Cousins in Binary Tree II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1down Lee LeetCode 2641 – *Cousins in Binary Tree II*
** Idiomas:** Java Silencio Python Silencio C++
** Complejidad en el tiempo** O(N)
** Complejidad del espacio:** O(H) (sólo la cola para el nivel actual)

-...

Problema Recap

Dada la raíz de un árbol binario, sustitúyase el valor de cada nodo por la suma de todos los valores de sus primos.
Dos nodos son *cousinas* si están a la misma profundidad y tienen diferentes padres.
La raíz no tiene primos, así que su nuevo valor es 0.

-...

### ## TENIDO DOSSolution Idea – Level‐by‐Level BFS

1. **Root → 0** – La raíz nunca cambia.
2. Para cada nivel * excepto* la raíz:
* Compute **`sumChildren`** = sum of all children of the nodes in the current level.
* Para cada nodo en el nivel
`curChildrenSum` = suma de los propios hijos de ese nodo.
Entonces el nuevo valor de cada niño = `sumChildren – curChildrenSum` (todos los primos en el siguiente nivel).
* Empuja a los niños a la cola para la próxima iteración.
3. Para cuando no haya más nodos para procesar.

El algoritmo sólo mantiene los nodos del nivel actual en memoria – O(H) espacio extra.

-...

## 2down️ ف Code Snippets

■ *Las tres implementaciones son totalmente compatibles con la definición de LeetCode de `TreeNode`. *

-...

#### 🧰 Java

``java
*
* Definición para un nodo de árbol binario.
* clase pública TreeNode {
* int val;
* TreeNode left;
* TreeNode right;
* TreeNode(int val) { this.val = val; }
* TreeNode(int val, TreeNode left, TreeNode right) {
* this.val = val;
* this.left = left;
* this.right = right;
*
*
*/
Clase Solución {
public TreeNode replace ValueInTree(TreeNode root) {
si (root == null) vuelve nula;

root.val = 0; // root has no cousins
Queue wonTreeNode confianza queue = new LinkedList recomendado();
queue.offer(root);

(!queue.isEmpty()) {}
int size = queue.size();
Lista realizadaTreeNode confianza curLevel = nuevo ArrayList recomendado(size);
int sumChildren = 0;

// Recopilar todos los nodos a nivel actual y suma computarizada de sus hijos
para (int i = 0; i) {}
TreeNode node = queue.poll();
curLevel.add(nodo);
si (node.left != null) sumChildren += node.left.val;
si (node.right != null) sumChildren += node.right.val;
}

// Actualización de valores infantiles
para (TreeNode node : curLevel) {
int own Niños Sum = 0;
si (node.left != null) propioChildrenSum += node.left.val;
si (node.right != null) propioChildrenSum += node.right.val;

si (node.left!= null) {
node.left.val = sumChildren - ownChildrenSum;
queue.offer(node.left);
}
si (node.right!= null) {
node.right.val = sumChildren - ownChildrenSum;
queue.offer(node.right);
}
}
}
raíz de retorno;
}
}
`` `

-...

#### Python

``python
Definición para un nodo de árbol binario.
# class TreeNode:
# def __init__(self, val=0, left=None, right=None):
# self.val = val
# Yo. izquierda = izquierda
# Yo. derecho = derecho

Solución de clase:
def replace ValueIn Tree(self, root: TreeNode) - título TreeNode:
si no raíz:
No.

root.val = 0 # root has no cousins
de las colecciones importa
q = deque([root])

mientras q:
nivel_size = len(q)
nivel_nodos = []
sum_children = 0

# Recopilar nodos de nivel actual y suma de todos los niños
para _ en rango(level_size):
nodo = q.popleft()
nivel_nodes.append(nodo)
si nodo. izquierda:
sum_children += node.left.val
si nodo. Bien.
sum_children += node.right.val

# Actualizar valores de los niños
para nodo en nivel_nodos:
own_sum = 0
si nodo. izquierda:
own_sum += node.left.val
si nodo. Bien.
own_sum += node.right.val

si nodo. izquierda:
node.left.val = sum_children - ¿Sí?
q.append(node.left)
si nodo. Bien.
node.right.val = sum_children - ¿Sí?
q.append(node.right)

raíz de retorno
`` `

-...

#### 🧰 C++

``cpp
*
* Definición para un nodo de árbol binario.
* struct TreeNode {
* int val;
* TreeNode *left;
* TreeNode *right;
* TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
* TreeNode(int x, TreeNode *l, TreeNode *r) : val(x), left(l), right(r) {}
* };
*/
Clase Solución {
public:
TreeNode* replaceValueInTree(TreeNode* root) {
si (!root) regresa nullptr;

root- iconoval = 0; // root has no cousins
std::queue correspondingTreeNode* título q;
q.push(root);

(!q.empty()) {
int sz = q.size();
std::vector seleccionadoTreeNode*
cur.reserve(sz);
larga larga sumaChildren = 0; // use long long to avoid overflow

// recoger los nodos de nivel actual y la suma de todos sus hijos
para (int i = 0; i) {}
TreeNode* node = q.front(); q.pop();
cur.push_back(nodo);
si (nodo- títuloleft) sumaNiños += nodo- títuloleft- títuloval;
si (nodo- título) sumaNiños += nodo- título-derreno- títuloval;
}

// Actualización de valores infantiles
para (TreeNode* nodo : cur) {
largo tiempo Sum = 0;
si (nodo-conferencialeft) propioSum += node- títuloleft-propioval;
si (nodo- tituladoright) propioSum += node- correctamente- títuloval;

si (nodo- títuloleft) {
node- títuloleft- títuloval = static_castint(sumChildren - ownSum);
q.push(node-consejoft);
}
si (nodo-principal) {
node- correctamente- títuloval = static_cast(sumChildren - ownSum);
q.push(node-ciendoright);
}
}
}
raíz de retorno;
}
};
`` `

-...

## 3 pescuestion Blog Article – *“Cousins in Binary Tree II: From Bugs to Brilliance (LeetCode 2641)”*

■ **SEO palabras clave:**
*Cousins in Binary Tree II*
*LeetCode 2641*
* Valor de lugar en el árbol*
* primas de árboles binarios*
*Entrevista de trabajo árbol binario*
* Pregunta de la entrevista de algoritmo*
* árbol binario BFS*

-...

# Cousins in Binary Tree II – A Job‐ Interview‐ Guía lista

### 🚀 Why This Problem Rocks

■ LeetCode 2641 es una pregunta ** "light‐bulb"** que aparece en muchas entrevistas de instrucciones de datos.
■ Resolverlo demuestra el dominio de:
(BFS)
- contabilidad de las sumas a cada profundidad
- manejo de persianas ( " niños " , nodos de un solo hijo " )

Si clavas esto, los reclutadores dirán: *“Estamos impresionados con su intuición transversal del árbol.”*

-...

## 📌 Problema Restablecido (Con un Twist)

■ Dado un árbol binario, sustitúyase el valor de cada nodo por el **sum de los valores de sus primos**.
■ La raíz siempre está fijada a 0 porque no tiene primos.

■ *Ejemplo*
" `
■ Entrada: 1
■ / \
■ 2 3
■ / \
▪ 4 5 6
■ Producto: 0
■ / \
■ 2 3
■ / \
■ 0 0
" `
■ (Aquí, los primos de 4 son 5 y 6 → 5 + 6 = 11, así que el nuevo valor de 4 es 11.)

-...

## 🧭 Step‐by‐Step Walkthrough

1. **Root → 0**
La raíz nunca participa en cálculos de primos, así que lo fijamos inmediatamente.

2. **BFS Loop**
Por cada nivel (excepto la raíz), nosotros:
- **Recoge** todos los nodos en el nivel actual ( "currentLevel " ).
- **Sum all children** of these nodes → `total ChildSum.
- Por cada nodo.
* `ownChildSum` = suma de sus propios hijos.
* El nuevo valor de cada niño = total ChildSum – propioChildSum`.

3. **Queue for Next Level**
Empujamos a los niños actualizados a la cola para que la próxima iteración funcione en la siguiente profundidad.

4. * Terminación*
Cuando la cola está vacía, todo el árbol ha sido procesado.

-...

Análisis de la complejidad

TENIDO MÁSAO TENIDO Cálculo TENIDO Resultado
Silencio----------------------------
Silencio **Tiempo** Silencio Cada nodo es visitado una vez; trabajo constante por nodo
Silencio **Espacio** Silencioso La cola tiene en la mayoría de los nodos de un nivel (≤ H nodos) Silencio **O(H)** Silencio

-...

## Гливали пели Las cascadas comunes (“Bad” y “Ugly” partes)

Por qué importa confidencialidad
Silencio...
Silencio **Uso de `node.left.val` antes de que se actualice** Silencio En la conversión original de la JS, los valores infantiles fueron sobrescritos *antes* se computó el `curSum` de los padres, corrompiendo la suma para el siguiente nivel. ← Compute `sumChildren` **primero** de los valores originales, luego actualiza a los niños en un segundo paso. Silencio
Silencio **Overflow on large trees** Silencio Los valores de Nodo pueden ser hasta `10^5`; añadir muchos niños pueden superar el rango de 32 bits. ← Use `long' (C++) o `int` con restricciones cuidadosas (Java/Python manéjelo bien). Silencio
Silencio **Null checks omitted** Silencio Accessing `node.left` cuando es `null` lanza una excepción. Silencio Guarde cada niño (`si (node.left != null) { ... }`). Silencio
Silencio **Queue misuse** Silencio Los niños que empujan `null` pueden inflar el tamaño de la cola e introducir errores. ← Sólo hay niños existentes. Silencio

-...

## 🎯 فTake‐away for Interviews

- # Declarar el invariante claramente # “Todos los nodos del nivel actual comparten el mismo “totalChildSum”.
*Mostrar las matemáticas* – Nuevo valor = total ChildSum – propioChildSum`.
- **Explicar por qué la raíz es 0** – es un caso de esquina que elimina una rama especial en el bucle.
**Mención del tiempo/espacio intercambio** – BFS utiliza espacio extra O(H) contra un DFS recursivo que utiliza la pila O(H) más profundidad de recursión O(N).

-...

## 📢 فBlog Post (SEO‐Optimized)

``markdown
# Cousins in Binary Tree II (LeetCode 2641) – Reemplazar el valor en el árbol

## Tabla de contenidos
1. 📌 Resumen del problema
2. Recibir un resumen de la solución
3. Aplicación de Java
4. Aplicación de Python
5. 🧰 C++
6. Análisis de la complejidad
7. ❌ فارجم Common Mistakes > Cómo evitar Ellos
8. 🚀 ف Why You'll Nail This in Your Next Coding Interview

## 📌 Problema general
Cousins in Binary Árbol II es una pregunta clásica de LeetCode que prueba su capacidad para atravesar un árbol binario **nivel por nivel**, calcular los valores agregados y actualizar los ganglios infantiles sin perturbar las relaciones entre padres e hijos. El objetivo es sustituir el valor de cada nodo por la suma de todos los valores de sus primos.

■ **Key Terms**
*Cousins*: La misma profundidad, diferentes padres
*Reemplazar el valor en el árbol*: La operación que implementará

## ف ف Пеперись Resumen
- Establecer valor raíz a **0** (sin primos).
- Por cada nivel, calcula la suma de todos los niños**.
- Para cada nodo en ese nivel, reste la suma de los niños de ese nodo **propiado** del total.
- Actualizar el valor de cada niño a esa diferencia y empujarlo a la cola para el siguiente nivel.

Esta estrategia **BFS** funciona en tiempo lineal **O(N)** y utiliza sólo **O(H)** espacio auxiliar.

## 🧰 Java Implementation
``java
Clase Solución {
public TreeNode replace ValueInTree(TreeNode root) {
si (root == null) vuelve nula;
root.val = 0;
Queue wonTreeNode confiar q = new LinkedList recomendado();
q.offer(root);
(!q.isEmpty()) {
int size = q.size();
Lista realizadaTreeNode título = nuevo ArrayList interpretado();
int sumChildren = 0;
para (int i = 0; i) {}
TreeNode node = q.poll();
nivel.add(nodo);
si (node.left != null) sumChildren += node.left.val;
si (node.right != null) sumChildren += node.right.val;
}
para (TreeNode node : nivel) {
int own Sum = 0;
si (node.left != null) propioSum += node.left.val;
si (node.right != null) propioSum += node.right.val;
si (node.left!= null) {
node.left.val = sumChildren - ownSum;
q.offer(node.left);
}
si (node.right!= null) {
node.right.val = sumChildren - ownSum;
q.offer(node.right);
}
}
}
raíz de retorno;
}
}
`` `

## 🧰 Python Implementation
``python
Solución de clase:
def replace ValueIn Tree(self, root: TreeNode) - título TreeNode:
si no raíz:
No.
root.val = 0
de las colecciones importa
q = deque([root])
mientras q:
sz = len(q)
nivel = []
sum_children = 0
para _ en rango(sz):
nodo = q.popleft()
nivel.append(nodo)
si node.left: sum_children += node.left.val
if node.right: sum_children += node.right.val
para nodos en el nivel:
propio = 0
si node.left: propio += node.left.val
si node.right: propio += node.right.val
si nodo. izquierda:
node.left.val = sum_children - own
q.append(node.left)
si nodo. Bien.
node.right.val = sum_children - own
q.append(node.right)
raíz de retorno
`` `

## 🧰 C++ Implementation
``cpp
Clase Solución {
public:
TreeNode* replaceValueInTree(TreeNode* root) {
si (!root) regresa nullptr;
root-Conval = 0;
queue realizaronTreeNode* titulada q;
q.push(root);
(!q.empty()) {
int sz = q.size();
vector:TreeNode* nivel;
larga suma Niños = 0;
para (int i = 0; i) {}
TreeNode* node = q.front(); q.pop();
nivel.push_back(nodo);
si (nodo- títuloleft) sumaNiños += nodo- títuloleft- títuloval;
si (nodo- título) sumaNiños += nodo- título-derreno- títuloval;
}
para (TreeNode* nodo : nivel) {
largo tiempo Sum = 0;
si (nodo-conferencialeft) propioSum += node- títuloleft-propioval;
si (nodo- tituladoright) propioSum += node- correctamente- títuloval;
si (nodo- títuloleft) {
node- títuloleft- títuloval = static_castint(sumChildren - ownSum);
q.push(node-consejoft);
}
si (nodo-principal) {
node- correctamente- títuloval = static_cast(sumChildren - ownSum);
q.push(node-ciendoright);
}
}
}
raíz de retorno;
}
};
`` `

Análisis de la complejidad
Silencio **La complejidad**
Silencio.
tención Tiempo **O(N)** Silencio Cada nodo es visitado una vez. Silencio
TENIDO Espacio **O(H)** Silencio Sólo un nivel de nodos vive en la cola a la vez. Silencio

## ❌ فارج Common Mistakes > Cómo evitar Ellos
- ** Actualizar niños antes de computar `sumChildren`** - conduce a totales incorrectos.
- **Dereferencia del puntero nulo** - siempre comprobar 'si (node.left)` antes de acceder a '.val'.
- **Overflow on huge trees** – use integers de 64 bits en idiomas que lo apoyen.

## 🚀 ف Why You'll Nail This in Your Next Coding Interview
- El problema combina **primera búsqueda** con ** razonamiento numérico** – un lugar dulce para los aficionados a la estructura de datos.
- Demuestra que puedes manejar **edge-cases** como nodos de un solo niño y punteros nulos con gracia.
- Muestra que eres cómodo escribiendo limpio, **O(H)** Código BFS que es fácilmente translatable entre Java, Python, y C++.

■ **Llévate a casa**: Maestro esto, y los reclutadores te verán como un gurú de árbol-traversal* listo para los desafíos algorítmicos más difíciles.

`` `

-...

**No dude en adaptar, publicar y compartir su maestría de Cousins en el Árbol binario II!**