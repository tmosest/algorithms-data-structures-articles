-...
Título: LeetCode 1973. Conde Nodos Igual a Sum de Descendientes -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. LeetCode 1973 – Conde Nodos Igual a Sum de Descendientes
** Objetivo:** Devuelve el número de nodos en un árbol binario cuyo valor equivale a la suma de todos los valores en su subárbol descendente.

■ *Un descendiente es cualquier nodo que se encuentra en un camino desde el nodo actual a una hoja.
■ La suma de los descendientes para una hoja se define como 0. *

La solución óptima funciona en **O(n)** tiempo y **O(h)** espacio, donde *n* es el número de nodos y *h* la altura del árbol (pila de recursión).

A continuación se presentan implementaciones limpias y de producción en **Java**, **Python** y **C+**.

-...

### 1.1 Java – Post-order DFS (Recursivo)

``java
*
* Definición para un nodo de árbol binario.
* clase pública TreeNode {
* int val;
* TreeNode left;
* TreeNode right;
* TreeNode() {}
* TreeNode(int val) { this.val = val; }
* TreeNode(int val, TreeNode left, TreeNode right) {
* this.val = val;
* this.left = left;
* this.right = right;
*
*
*/
Clase Solución {
int count privado = 0;

int equalToDescendants(TreeNode root) {
dfs(root);
recuento de retorno;
}

*
* Devuelve la suma de todo el subárbol arraigado en el nodo.
* Mientras desenrollamos la recursión comparamos el valor del nodo
* con la suma de sus descendientes (izquierda + derecha).
*/
int privado dfs(TreeNode node) {
si (nodo == nulo) devuelve 0;

int left Sum = dfs(node.left);
Intento derecho Sum = dfs(node.right);
niño Sum = izquierda Sum + derecha Sum;

si (node.val == childSum) cuenta++;

// Regresar suma incluyendo este nodo para su padre.
retorno node.val + childSum;
}
}
`` `

-...

### 1.2 Python – Post-order DFS (Recursivo)

``python
Definición para un nodo de árbol binario.
# class TreeNode:
# def __init__(self, val=0, left=None, right=None):
# self.val = val
# Yo. izquierda = izquierda
# Yo. derecho = derecho

Solución de clase:
def equal ToDescendants(self, root: TreeNode) - int:
cuenta propia = 0

def dfs(nodo: TreeNode) - título int:
si no el nodo:
retorno 0
izquierda = dfs(node.left)
derecho = dfs(node.right)
child_sum = izquierda + derecha
si node.val == child_sum:
self.count += 1
retorno node.val + child_sum

dfs(root)
Vuélvete. Cuenta
`` `

-...

### 1.3 C++ – Post-order DFS (Recursivo)

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
int count = 0;

int equalToDescendants(TreeNode* root) {
dfs(root);
recuento de retorno;
}

privado:
int dfs(TreeNode* node) {
si (!node) devuelve 0;
int left = dfs(node- confíaleft);
int right = dfs(node-cedright);
int child_sum = izquierda + derecha;
si (nodo- títuloval == child_sum) ++cuenta;
nodo de retorno-conval + child_sum;
}
};
`` `

-...

## 2. Artículo del Blog – “El Bien, el Mal y el Ugly of Counting Nodes Equal to the Sum of Descendants”

### Title
**Mastering LeetCode 1973: Count Nodes Equal to Sum of Descendants – A Deep Dive into Good, Bad & Ugly Patterns* *

## Meta Descripción
Aprende a resolver LeetCode 1973 en Java, Python y C++ con un enfoque DFS post-orden limpio. Descubre las mejores prácticas, las trampas comunes y los consejos de entrevista que impresionarán a los reclutadores.

#### Palabras clave
LeetCode 1973, Conde Nodes Equal to Sum of Descendants, Binary Tree DFS, Post-order Traversal, Java LeetCode, Python LeetCode, C+ LeetCode, Tree Traversal, Interview Question, Technical Interview, Backend Engineer

-...

Introducción

Los problemas de los árboles binarios son el pan y la mantequilla de las entrevistas de codificación.
LeetCode **1973 – Conde Nodes Equal to Sum of Descendants** es un gran ejemplo: te obliga a combinar un clásico traversal de árboles con un sutil cheque aritmético.

En este post, vamos a:
1. Rompe el problema en tres partes – *El Bien*, *El Mal* y *El Ugly*.
2. Proporcionar una solución lista para la producción en **Java**, **Python**, y **C+**.
3. Discuti los casos de borde, la profundidad de recursión, y por qué este patrón es un conocimiento imprescindible para cualquier ingeniero de backend.

-...

#### 2down⃣ El bueno – un elegante post-order DFS

Por qué es buena vida
Silencio----------
Silencio **Post-order traversal** ANTE Garantías que conocemos las sumas descendientes *antes* evaluando el nodo actual. Silencio
Silencioso **Paso único** Silencioso O(n) tiempo – cada nodo visitado una vez. Silencio
Silencio **Espacio de la pila de luz** Silencioso O(h) espacio – la profundidad de la recursión equivale a la altura del árbol, mucho mejor que el O(n) de BFS. Silencio
tención ** legible " mantenible** vivir clara separación de la " suma completa " y " comprobar la igualdad " . Silencio
Silencio **No hay efectos secundarios globales** Silencio Usar un campo de clase/instance (`count`) mantiene al ayudante puro. Silencio

■ *Key Insight*
■ Si `sum(left) + sum(right) == node.val`, aumenta el contador.
■ Volver `node.val + sum(left) + sum(right)` a los nodos padres.

Este patrón es reutilizable para muchos problemas “subtree agregado” (sum, promedio, altura, etc.).

-...

#### 3down⃣ Los malos – saltos comunes

Pitfall Silencio Consequence Silencio
Silencio----------------------------
Silencio **Usar variables globales** Silencio difícil para probar una unidad, riesgo de estado de estancamiento a través de llamadas. TEN Store estado en un campo de clase o devolver un tuple. Silencio
Silencio **Brute‐force BFS/DFS** ← Re-computing sums from scratch for each node → O(n2). tención Computa una vez en un pase post-orden. Silencio
Silencio **Apilador alternativo con seguimiento manual de sumas** Silencio Bug‐prone, verbose. TEN Preferir la recursión a menos que la altura del árbol Ω 105 (riesgo de desbordamiento de la pila). Silencio
Silencio **Ignorando la definición del nodo de hoja** ← Mis-count cuando el nodo no tiene hijos. La suma descendente de la hoja Treat como 0. Silencio
Silencio **Desbordamiento entero** Silencioso Valores hasta 105, pero la suma de muchos nodos podría exceder `int`. Silencio Uso `long` en Java/C++ o los enteros ilimitados de Python. Silencio

-...

#### 4down⃣ Soluciones Ugly – Ineficientes o incorrectas

1. **Recuperación ingenua (O(n2)* *
``java
int count = 0;
int sumDescendants(TreeNode node) { ... } // O(n)
vacio transversal(TreeNode node) {}
si (nodo == nulo) regresa;
int sum = sumDescendants(node);
si (nodo.val == suma) cuenta++;
(node.left);
Traverse(node.right);
}
`` `
¿Por qué Ugly? Cada nodo activa toda una suma de subárbol, dando lugar al tiempo cuadrático.

2. **Using a `HashMap` to store subtree sums* *
``java
Mapa seleccionadoTreeNode, Integer título memo = nuevo HashMap correctamente();
int getSum(TreeNode node) {
si (nodo == nulo) devuelve 0;
devolver memo.computeIfAbsent(node, n - título n.val + getSum(n.left) + getSum(n.right));
}
`` `
¿Por qué Ugly? Añade espacio extra y complejidad; no es necesario para este problema.

3. ** DAIterative con una pila y dos pases* *
- Primer paso para empujar nodos.
- Segundo paso a las sumas pop y compute.
¿Por qué Ugly? Doble trabajo y código frágil.

Evite estos patrones a menos que la entrevista solicite específicamente una alternativa (por ejemplo, DP de abajo arriba, árboles de segmento).

-...

#### 5down⃣ Casos de borde " Robustness "

Silencio ¿Qué hay que ver para Silencio
Silencio...
Silencio ** Árbol vacío (`root == null`)** Silencio Regresar 0 – nodos a contar. Silencio
TENIDO **Arbol muy desequilibrado** TENIDO Altura Ô n → la recursión puede desbordarse. Use una pila explícita o una " recidiva de cola " (según se permite). Silencio
Silencio **Grandes sumas descendientes** Silenciosos Reflujo potencial en ints de 32 bits. Silencio Uso `long` (Java/C++) o la int.
Silencio **Todos los nodos iguales a 0** Silencio Todos los partidos no sordos porque la suma descendente es 0. Silencio mostrado será 'n - number_of_leaves`. Silencio

Pruebas con estos casos de borde garantizan una presentación a prueba de balas.

-...

### 6 comentarios⃣ Interview‐Ready Talking Points

1. **Declarar el Enfoque Primero** – “Haré un DFS post-orden porque necesito las sumas descendientes antes de que pueda comprobar la igualdad. ”
2. **Explicar la complejidad** – Un pase, O(n) tiempo, O(h) pila. ”
3. **Desbordamiento de la mención** – “Todos los valores de entrada son ≤ 105, pero la suma puede exceder de 32 bits; Voy a utilizar `long’.”
4. **Mostrar el Código** – Proporcionar un snippet limpio en el idioma de su elección.
5. **Optional – Discuss a Brute‐Force Baseline** – “Si fuéramos a fuerza bruta, terminaríamos con O(n2), que es poco práctico. ”
6. **Pregunta por Variaciones** – “¿Y si quisiéramos devolver los nodos reales en lugar de contar?” – conduce a un pequeño refactor.

-...

Conclusión

LeetCode 1973 no es sólo una prueba de recursión; es un micro-curso sobre la agregación de árboles ** eficiente**.
La solución “post-order DFS” es el estándar de oro:
* Traversal individual, espacio lineal, lógica clara. *

Evite los patrones malos y feos, porque los reclutadores están buscando códigos limpios, *interview-friendly* que escala.

-...

### 7ف⃣ Takeaway Checklist

- [ ] Use ** Post-order DFS** para agregados de subárbol.
- [ ] Mantenga contadores en un campo de clase/instancia; evite la estática global.
- [ ] Tratar hojas como tener 0 suma descendente.
- [ ] Guardia contra el desbordamiento ( " largo " / " BigInteger " ).
- [ ] Maneja el árbol vacío como base.
- [ ] Prepárate para explicar la profundidad de recursión y el uso de pilas.

Dominar estos principios le dará una posición sólida para ** entrevistas de ingeniería de backend** donde la lógica de los árboles es común.

-...

## 3down Pensamientos finales

Los árboles binarios están en todas partes, desde la perspicacia de árboles de expresión en los compiladores hasta la organización de una estructura de directorios en los sistemas de archivos.
El patrón que demostramos hoy se extenderá en muchos otros problemas: “Sum of left subtree”, “Maximum path sum”, “Largest BST en un árbol binario”, etc.

La próxima vez que veas un problema de árbol de LeetCode, piensa:

■ *Computa una vez → tienda una vez → propagar hacia arriba. *

¡Feliz codificación y buena suerte impresionando a su próximo reclutador!