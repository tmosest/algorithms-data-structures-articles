-...
Título: LeetCode 968. Cámaras de árboles binarios -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Binary Tree Cameras – LeetCode 968
■ *Hard – Post-Order Greedy DFS*

Resolver el problema en **Java, Python, y C++** y leer un corto, SEO-friendly blog que explica la idea, el "bueno, el malo, y el feo", y por qué dominar este problema le ayuda a aterrizar un trabajo técnico.

-...

## 1. Código

■ **Consejo:** La solución es la misma idea en los tres idiomas:
■ *Post-order* traversal que devuelve uno de tres estados
* **-1** : el nodo es **no supervisado* *
######### #######################################################################################################################################################################################################################################################
################################################################################################################################################################################################################################################################

■ El padre utiliza estos valores para decidir si necesita una cámara.

-...

#### 1.1 Java

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
cámaras int privadas = 0;

public int minCameraCover(TreeNode root) {
// Si la raíz no es supervisada después de DFS necesitamos una cámara más.
retorno dfs(root) == -1 ? cámaras + 1 : cámaras;
}

*
* @return -1 : nodo es monitoreado
* 0 : nodo es monitoreado (sin cámara)
* 1 : nodo tiene una cámara
*/
int privado dfs(TreeNode node) {
si (nodo == nulo) retorno 0; // null se considera monitoreado

int left = dfs(node.left);
int right = dfs(node.right);

// Si un niño no es monitoreado, coloque la cámara aquí.
si (izquierda == -1 Silencioso -1) {
cámaras++;
retorno 1; // este nodo ahora tiene una cámara
}

// Si algún niño tiene una cámara, este nodo es monitoreado.
si (izquierda == 1 Silencioso 1) {
retorno 0; // monitoreado, sin cámara
}

// Ninguno de los niños tiene una cámara y todos son monitorizados.
retorno -1; // no monitoreado, padre debe ver
}
}
`` `

-...

### 1.2 Python

``python
Definición para un nodo de árbol binario.
# class TreeNode:
# def __init__(self, val=0, left=None, right=None):
# self.val = val
# Yo. izquierda = izquierda
# Yo. derecho = derecho

Solución de clase:
def minCameraCover(self, root: TreeNode) - confiar int:
autocámaras = 0

si auto.dfs(root) == -1: # root is still not monitored
Vuélvete. cámaras + 1
volver auto.cámaras

def dfs(self, node: TreeNode) - título int:
"
Regreso:
-1 : nodo es monitoreado
0 : nodo es monitoreado
1 : nodo tiene una cámara
"
si no el nodo:
retorno 0 # null is considered

izquierda = auto.dfs(node.left)
right = self.dfs(node.right)

si queda == -1 o derecha == -1:
auto. cámaras += 1
Regreso 1

si queda == 1 o derecha == 1:
retorno 0

retorno -1
`` `

-...

#### 1.3 C++

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
int minCameraCover(TreeNode* root) {
cámaras = 0;
si (dfs(root) == -1) devuelve cámaras + 1; // root not covered
devolver cámaras;
}

privado:
cámaras int = 0;

// -1: NO monitoreado, 0: monitoreado, 1: tiene cámara
int dfs(TreeNode* node) {
si (!node) retorno 0; // null es monitoreado

int left = dfs(node- confíaleft);
int right = dfs(node-cedright);

si (izquierda == -1 Silencioso -1) { // niño sin vigilancia
++cámaras;
vuelta 1; // cámara de lugar aquí
}

si (izquierda == 1 Silencioso 1) { // niño tiene cámara
retorno 0; // monitoreado
}

retorno -1; // still not monitored
}
};
`` `

-...

## 2. Artículo del Blog

■ **Título:** *Cámaras de árboles hinchables – LeetCode 968 Resuelto en Java, Python & C++ *
■ **Keywords:** cámaras de árboles binarios, LeetCode 968, problema duro, algoritmo de entrevista, DFS post-orden, codiciado, entrevista de trabajo, reclutador técnico

-...

#### 2.1 Introduction

Si te estás preparando para una entrevista de ingeniería **software**, te encontrarás enfrentando problemas difíciles que empujan tu comprensión de los árboles, la programación dinámica y las estrategias avaricias.
LeetCode 968 – **Binary Tree Cameras** – es uno de esos problemas de firma.

■ *Por qué importa*
* Prueba tu habilidad para razonar con los estados del árbol.
• Requiere una solución DP limpia e inferior.
* Muestra a los reclutadores que puede escribir código eficiente y legible en varios idiomas.

En este artículo caminamos a través del **bueno**, el **bad**, y el **junto** de este problema, compartimos una solución **grande post-orden**, y mostrar cómo se puede implementar en **Java, Python, y C++**.

-...

### 2.2 Declaración de problemas

■ **Given** un árbol binario, puede colocar una cámara en cualquier nodo.
■ Una cámara puede controlar a su padre, a sí mismo y a sus hijos inmediatos.
■ **Retorna el número mínimo de cámaras necesarias para monitorear cada nodo** del árbol.

*Constraints: *
- 1 ≤ número de nodos ≤ 1000
- Los valores de los ganglios son todos 0 (el valor es irrelevante).

-...

### 2.3 The Good – Why the Greedy Idea Works

- **Bottom-up reasoning:** El estado de un nodo está plenamente determinado por los estados de sus hijos.
- **Sólo 3 estados necesarios** (sin vigilancia, monitorización, cámara) – mantiene al DP pequeño.
- **Tiempo de trabajo** (O(n)) y **O(h)** pila auxiliar (profundidad de recuperación).
- **Elegant code**: just one `dfs` function and a counter.

**Esquema de Estado**

Silencio Silencio Silencio Silencio
Silencio--------
Silencio -1 (sin vigilancia) Silencio * Silencio **camera** (lugar aquí)
Silencio 1 (cámara) Silencio * Silencio monitoreado
Silencio 0 (monitored) Silencio 0 Silencio unmonitored (necesita a su padre para ver)

-...

### 2.4 El malo – Pitfalls comunes

Silencio Pitfall Silencio Por qué duele Silencio
Silencio--------------------------
Silencio **Treat null as unmonitored** Silencio Causas Cámaras infinitas en los árboles de hoja solamente Silencio Regresar 0 para null (considerado monitorizado)
Silencio **Retorno valor mal uso** ← Confusing `-1` with `0` ints primitivos de Java Silencio Mantener un comentario claro o enum Silencio
Silencio **Profundidad recursiva** Silencio Rebosa de apilamiento para árboles de abeto profundo de 1000 n odo Silencio Usar orden post-orden iterativo o aumentar el límite de apilación (Java: `-Xs256m`) Silencio
Silencio **No comprobando la raíz después de DFS** Silencio Puede perder la cámara en la raíz cuando todo el árbol no supervisado Silencio Add `if (dfs(root) == -1) cámaras++` Silencio

-...

### 2.5 The Ugly - When Things Go Wrong

- Ordenación de las condiciones* Colocar la cámara antes de comprobar los niños conduce a recuentos subóptimos.
- **Over-complicated DP**: Tratar de almacenar una lista de posiciones de cámara o utilizar BFS en lugar de DFS convierte la solución elegante en un desastre.
- *Agujación del árbol* Algunas soluciones pre-computan la profundidad, luego ejecutan otro bucle – innecesario.

-...

## 2.6 Solución completa – Post-Order Greedy DFS

1. Devuelve el estado del nodo.
2. Si un niño es ** no supervisado** (`-1`), coloque la cámara en el nodo actual (`cámaras++`) y regrese ** cámara** (`1`).
3. Si algún niño tiene un **cámara** (`1`), el nodo es ** supervisado** (`0`).
4. De lo contrario, el nodo es **unmonitored** (`-1`).
5. Después de DFS, si el **root** no está vigilado, agregue una cámara más.

■ **Tiempo**: O(n) – cada nodo visitó una vez.
■ **Espacio**: O(h) - apilación de recursión, donde `h` es altura de los árboles.

-...

### 2.7 Muestras de Código

*(Ver la sección de código anterior para Java, Python, C++ implementaciones.) *

-...

### 2.8 Cómo esto te ayuda a conseguir un trabajo

1. **Demonstrates Tree DP** – Muchos entrevistadores preguntan “¿Cuál es el estado?” y “¿por qué fondo? ”
2. **Shows Coding Limpieza** – Tres idiomas, lógica idéntica → gran portafolio snippet.
3. **Highlights Problem‐Solving Mindset** – Reconocer la propiedad avaricia reduce dramáticamente la complejidad.
4. **Preparaciones para las variaciones** – Si preguntan “¿qué pasa si las cámaras cuestan diferente?”, usted puede extender el DP.

Añadir este problema a tu lista **LeetCode Top 100 Hard**, publicar las soluciones en GitHub, y discutir los cambios en tu entrevista.

-...

### 2.9 Quick Reference Cheat‐ Sheet

Silencio Idioma Silencioso contra Silencio Silencio
Silencio------------------------------
TEN Java TERRITORIO `int cameras` ANTE `int dfs(TreeNode node)` Silencio
TENIDO Python TENIDO `self.cameras` TENIDO `def dfs(self, node)` Silencio
TENIDO C++ TENIDO `int cameras` TENIDO `int dfs(TreeNode* node)` Silencio

-...

### 2.10 Takeaway

■ *Binary Tree Cameras* le enseña cómo **modelizar un problema con una pequeña máquina de estado** y resolverlo con un pase de DFS de sonido **.
■ Maestro esto, y estará listo para abordar cualquier problema duro relacionado con los árboles en el piso de la entrevista.

¡Buena suerte! 🚀

-...

■ ** Recursos:**
• LeetCode 968: https://leetcode.com/problems/binary-tree-cameras/
• Discuss on Reddit /r/cscareerquestions.
Repositorio GitHub para soluciones multi-lang.

-...

■ *Descargos* El código está escrito con Java 17, Python 3.10, y C++17 en mente.
■ Las adaptaciones pueden ser necesarias para su compilador particular o entorno de tiempo de ejecución.

-...


■ **End of Article**



-...

■ **Nota a los lectores:**
■ Si desea una inmersión más profunda en el árbol DP o necesita ayuda con otro problema difícil de LeetCode, deje un comentario o envíenos un correo electrónico a `interviewguru@example.com`. ¡Feliz codificación!