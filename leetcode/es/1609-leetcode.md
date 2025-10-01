-...
Título: LeetCode 1609. Incluso Árbol Extraño -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1609. Incluso Árbol extraño
**Medium ← Breadth‐First Search Silencio O(N) time Silencio O(N) space**

■ Un árbol binario se llama **Even‐Odd** cuando:
■ 1. Los niveles se numeran a partir de 0 (root = nivel 0).
■ 2. Los niveles incluso indexados contienen valores **odd** que aumentan estrictamente** de izquierda a derecha.
■ 3. Los niveles odd-indexed contienen **even** valores que están **disminuyendo estrictamente** de izquierda a derecha.

Regresa 'verdad' si el árbol satisface las tres reglas, de lo contrario 'falso'.

-...

## 🚀 Why This Problem Matters for Job Interviews

- **La primera traversal es un elemento básico para preguntas binarias.
- Las pruebas de tarea **traversal de estado** (mantenimiento de la paridad de nivel).
- Requiere una lógica de salida** –una vez que se encuentra una violación, todo el algoritmo se detiene.
- Los candidatos deben pensar en **time/space trade-offs** e implementar limpiamente los cheques de monotonicidad.

Ser capaz de discutir este problema (y sus variaciones) en una entrevista muestra que usted entiende los traversales de árboles, el manejo de los bordes y la complejidad algorítmica.

-...

## 🔍 Problem Recap (Short Version)

``text
Entrada : TreeNode root
Producto : booleano

Regla 1 : Nivel 0, 2, 4... - Números impares del título, aumentando estrictamente
Regla 2 : Nivel 1, 3, 5... - E incluso números, disminuyendo estrictamente
`` `

-...

## 🧠 Core Idea – Level Order with Parity Checks

1. **BFS** (queue) para visitar los nodos de nivel por nivel.
2. Mantenga una bandera " esEvenLevel " ( " verdadero " por niveles).
3. Para cada nivel:
* **Incluso nivel**: el valor debe ser extraño y `valor ' prev`.
* **Nivel extraño**: el valor debe ser uniforme y `valor  observado prev`.
4. Actualizar `prev` después de comprobar el nodo.
5. Aprenda a los niños de izquierda y derecha para el siguiente nivel.
6. Flip la bandera de nivel después de terminar un nivel.

Debido a que podemos devolver `falso' tan pronto como una regla se rompe, el algoritmo es lineal en el número de nodos.

-...

Aplicación

A continuación se encuentran soluciones limpias, listas para pasar en **Java**, **Python**, y **C+**.

■ **Nota**: Las tres soluciones utilizan la misma lógica BFS; las únicas diferencias son sintaxis y estructuras de datos específicas para cada idioma.

-...

## Java

``java
importar java.util.LinkedList;
importa java.util. Queue;

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
booleano público esEvenOddTree(TreeNode root) {
si (root == null) regresan verdaderos;

Queue wonTreeNode confiar q = new LinkedList recomendado();
q.offer(root);
boolean isEvenLevel = true; // nivel 0 es incluso
int prev = isEvenLevel ? Integer.MIN_VALUE : Integer. MAX_VALUE;

(!q.isEmpty()) {
int size = q.size();
nivel Prev = prev; // reset prev para cada nivel

para (int i = 0; i) {}
TreeNode node = q.poll();

// Revisar la regla de paridad
si (esEvenLevel) {
si (node.val % 2 == 0 TENIDO NODE.val <= nivelPrev) devuelve falso;
. ♫ ... {
si (node.val % 2 == 1 TENIDO Node.val √≥= levelPrev) devuelve falso;
}

nivelPrev = node.val;

// Agregar niños para el siguiente nivel
si (node.left != null) q.offer(node.left);
si (node.right!= null) q.offer(node.right);
}

// Paridad de nivel Flip para la siguiente capa
isEvenLevel = !isEvenLevel;
}
retorno verdadero;
}
}
`` `

-...

## Python

``python
Definición para un nodo de árbol binario.
# class TreeNode:
# def __init__(self, val=0, left=None, right=None):
# self.val = val
# Yo. izquierda = izquierda
# Yo. derecho = derecho

de las colecciones importa

Solución de clase:
def isEvenOddTree(self, root: TreeNode) - conveniente bool:
si no raíz:
Retorno

q = deque([root])
is_even_level = True # level 0 is even
prev = flotante('-inf') si es_even_nivel más flotante('inf')

mientras q:
tamaño = len(q)
nivel_prev = prev

para _ en rango(tamaño):
nodo = q.popleft()

# Parity and monotonicity check
si es_even_nivel:
si nodo.val % 2 == 0 o nodo.val
Retorno Falso
más:
si nodo.val % 2 == 1 o nodo.val  nivel_prev:
Retorno Falso

nivel_prev = node.val

si nodo. izquierda:
q.append(node.left)
si nodo. Bien.
q.append(node.right)

# Toggle level parity
is_even_level = not is_even_level

Retorno
`` `

-...

### C++

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
#include >
usando std namespace;

Clase Solución {
public:
bool isEvenOddTree(TreeNode* root) {
si (!root) regresan verdaderos;

queue realizaronTreeNode* titulada q;
q.push(root);
bool isEvenLevel = true; // nivel 0 es incluso
int prev = isEvenLevel ? INT_MIN: INT_MAX;

(!q.empty()) {
int sz = q.size();
nivel Prev = prev; // reseteo para este nivel

para (int i = 0; i) {}
TreeNode* cur = q.front(); q.pop();

si (esEvenLevel) { // incluso nivel: valores extraños, aumentando
si (cuerdo- títuloval % 2 == 0 vocante cur- títuloval iere= nivelPrev) devuelve falso;
} otro { // nivel extraño: incluso valores, disminuyendo
si (cuerdo- títuloval % 2 == 1 ← permanente cur- confianzaval ≤ nivelPrev) devuelve falso;
}

nivelPrev = cur- títuloval;

q.push(cur-ing- títuloleft);
q.push(cur- tituladoright);
}

isEvenLevel = !isEvenLevel; // flip for next level
}
retorno verdadero;
}
};
`` `

-...

Paso a paso ( Ejemplo Java)

1. **Pregunta inicialización** – empezar con la raíz.
2. ** Tamaño de la distancia** – `tamaño = q.size()` dice cuántos nodos pertenecen al nivel actual.
3. ** Valor Prev** – `prev` se inicializa a `INT_MIN` en niveles incluso (cualquier valor extraño será mayor) y a `INT_MAX` en niveles impares (cualquier valor incluso será menor).
4. **Node Check** –
* Incluso nivel: `node.val % 2 == 1 `Y `node.val ¢prev`.
* Nivel de riesgo: `node.val % 2 == 0 `Y `node.val' se hizo prev`.
5. **Early Failure** – devolver `false` inmediatamente si se viola una regla.
6. **Aprenda a los niños** – izquierda y derecha, preservando el orden izquierdo a derecho.
7. **Level Flip** – ` isEvenLevel = !isEvenLevel`.

-...

## ⋅ Common Pitfalls

Silencio Pitfall Silencio
Silencio...
Silencio **Using `prev = Integer.MIN_VALUE` on both levels** tención Reset `prev` per level; use `INT_MIN` only on even levels, `INT_MAX` on odd levels. Silencio
Silencio **Mixing left/right order** Silencio Encuue children in the order `left` then `right`. El BFS garantiza un orden de nivel correcto. Silencio
Silencio **Ignorando a los niños pequeños** Silencio No encargues `null`; de lo contrario la cola crecerá innecesariamente. Silencio
Silencio **No voltear la bandera después de cada nivel** Silencio Si te olvidas de mover `isEvenLevel`, todos los niveles serán tratados como incluso. Silencio

-...

## 📊 Complexity Analysis

TEN TERMIN TEN ANTE Complejidad
Silencio...
Silencio **Hora** Silencioso `O(N)` – cada nodo es visitado exactamente una vez. Silencio
Silencio **Espacio** Silencioso `O(N)` – la peor cola de casos mantiene todos los nodos en el nivel más profundo (coge la mitad del árbol). Silencio

-...

## 🔁 Alternative Approaches

1. **Recursive DFS with Level Tracking** – pasa el número de nivel a cada llamada recursiva, pero todavía necesita seguir el valor anterior por nivel.
2. **DFS alternativo con Stack** - complejidad similar pero más engorroso para mantener el orden.
3. **Divide‐and‐Conquer** – proceso de subárboles izquierdos y derechas, luego fusionar resultados; sobrecarga innecesaria.

BFS sigue siendo la solución más simple y legible para este problema.

-...

## 📈 SEO‐Friendly Highlights

- **Título**: “Even‐Odd Tree LeetCode Solution – Java, Python, C++ Explained”
- **Keywords**: *Incluso Árbol extraño, LeetCode 1646, Árbol binario BFS, Traversal de órdenes de nivel, Preparación de entrevistas, Estructuras de datos, Complejidad del tiempo, Complejidad del espacio, Algoritmo de salida temprana, Comprobación de paridad del árbol*
- **Meta Descripción**: “Master el problema Even‐Odd Tree en LeetCode con soluciones BFS paso a paso en Java, Python y C++. Comprender las reglas de paridad, complejidad y estrategias de entrevista. ”

-...

## Causeaway

El Even‐Odd El problema del árbol es un escaparate conciso de:

1. **La primera traversal con una cola.
2. ** Paridad estatal** manejo.
3. **Monotonicity and parity checks** con salida temprana.
4. **Tiempo de trabajo** y espacio óptimo**.

Siéntase libre de ajustar las soluciones para las variaciones (por ejemplo, el estricto vs. no-strict ordering) o de manejar árboles grandes en los ajustes de entrevista. Buena suerte, ¡muestra a esos entrevistadores que tienes traversales de árboles bajo tu cinturón! 🚀

-..