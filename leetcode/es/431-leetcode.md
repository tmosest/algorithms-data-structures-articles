-...
Título: LeetCode 431. Código N-ary Tree to Binary Tree -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 Encode an N‐ary Tree to a Binary Tree (LeetCode 431) – Code + Interview‐ Listo Blog

■ **TL;DR**
• Convertir un árbol N‐ary → árbol binario usando el truco *left‐child right-sibling*.
* Decode back by traversing left→derecha hermanos.
• O(N) time, O(H) recursion stack (≤ 1000).
• Implementación limpia y apátridas, perfecta para una entrevista de LeetCode.

-...

### 1. El problema (LeetCode 431)

Dado un **N-ary árbol** (cada nodo puede tener ningún número de niños) debe:

Silencio
Silencio...
Silencio **Encode** Silencio Conviértelo en un **árbol binario** para que la estructura pueda ser almacenada o transmitida. Silencio
Silencio **Decode** Silencio Reconstruir el árbol N-ary original de la representación binaria. Silencio

■ **Constraints**
* `0 ' = node.val ' = 104`
* " 0 " = número de nodos "
* Altura ≤ 1000
* **Ningún estado global/estático** – el encoder/decoder debe ser apátrida.

La solución clásica es la cartografía de *left‐child right-sibling*:

* El niño **izquierda** de un nodo binario es el primer niño** del nodo N-ary correspondiente.
* El niño **correcto** de un nodo binario es el siguiente hermano ** de ese niño.

Esta representación es infalible: siempre se puede caminar hacia el árbol N‐ary.

-...

### 2. ¿Por qué este blog?
Los entrevistadores aman los problemas que prueban las conversiones **data‐structure** y su capacidad de pensar en **traversales de árboles** de maneras no triviales.
Este post le da:

* ** Código de trabajo** en **Java, Python y C++** – copy‐paste listo.
* Una explicación clara y amigable de SEO** que puedes mencionar en una carta de portada o portafolio.
* Un desglose de los aspectos **bueno**, **bad**, y **ugly**, para que puedas hablar de oficios durante una entrevista.

-...

## 3. El algoritmo básico

`` `
encode(root):
si root es null: volver null
binario = nuevo TreeNode(root.val)
Si root. niños no vacíos:
binario.left = código(root.children[0]) // primer niño
cur = binario. izquierda
para mí de 1 a root.children. tamaño-1: // hermanos
cur.right = código(root.children[i])
cur = cur.right
devolver binario

decode(root):
si root es null: volver null
nary = nuevo Node(root.val, [])
cur = root.left
mientras se cura!= null: // hermanos transversales
nary.children.append(decode(cur)))
cur = cur.right
Regresa Nary
`` `

* **Tiempo**: Cada nodo es visitado una vez → **O(N)**.
* **Espacio**: Profundidad de la pila de recorsión ≤ altura del árbol (≤ 1000).
* **Apátridas**: No hay variables globales; todo estado vive en la pila de llamadas.

-...

## 4. Código (Copy‐Paste Ready)

#### 4.1 Java

``java
// Definición para un nodo de árbol N-ary.
Clase Node {}
int val;
public List Node confía children;

public Node() {} {}
public Node(int _val) { val = _val; }
public Node(int _val, List GarantizadoNode confianza _children) {}
val = _val;
niños = niños;
}
}

// Definición para un nodo de árbol binario.
clase TreeNode
int val;
TreeNode izquierda, derecha;
TreeNode(int x) { val = x; }
}

Clase Codec {}

// Codificar un árbol N-ary a un árbol binario.
public TreeNode encode(Node root) {
si (root == null) vuelve nula;

TreeNode binario = nuevo TreeNode(root.val);

si (root.children != null " ventaja !root.children.isEmpty()) {}
binario.left = code(root.children.get(0)); // first child
TreeNode cur = binario. izquierda;
para (int i = 1; i) i++) { // hermanos
cur.right = código(root.children.get(i));
cur = cur.right;
}
}
retorno binario;
}

// Decodificar un árbol binario de vuelta a un árbol N-ary.
público Nodo decode(TreeNode root) {
si (root == null) vuelve nula;

Node nary = nuevo Node(root.val, nuevo ArrayList recomendado());
TreeNode cur = root.left;
mientras (cur != null) { // hermanos transversales
nary.children.add(decode(cur));
cur = cur.right;
}
devolver nary;
}
}
`` `

#### 4.2 Python

``python
Definición para un nodo de árbol N-ary.
Clase Nodo:
def __init__(self, val=None, children=None):
self.val = val
niños = niños o []

Definición para un nodo de árbol binario.
Clase TreeNode:
def __init__(self, val=0, left=None, right=None):
self.val = val
autoizquierda
self.right = right

class Codec:
# Encodes an N-ary tree to a binario tree.
def encode(self, root: 'Node') - título "TreeNode"
si no raíz:
No.

nodo = TreeNode(root.val)
Si root. niños:
node.left = self.encode(root.children[0]) # first child
Cur = nodo. izquierda
para niños en la raíz. niños[1:]:
cur.right = self.encode(child) # hermanos
cur = cur.right
Nodo de retorno

# Decodifica un árbol binario de vuelta a un árbol N-ary.
def decode(self, root: 'TreeNode') 'Node':
si no raíz:
No.

nary = Node(root.val, [])
cur = root.left
mientras se cura:
nary.children.append(self.decode(cur)))
cur = cur.right
Regresa Nary
`` `

#### 4.3 C++

``cpp
Incluido el título
usando std namespace;

// Definición para un nodo de árbol N-ary.
struct Node {}
int val;
vector Node* niños;
Nodo() : val(0) {}
Nodo(int _val) : val(_val) {}
Nodo(int _val, vector efectuadoNode*=niños)
: val(_val), children(_children) {}
};

// Definición para un nodo de árbol binario.
struct TreeNode {
int val;
TreeNode *left, *right;
TreeNode(int _val) : val(_val), left(nullptr), right(nullptr) {}
};

Clase Codec {}
public:
// Codificar un árbol N-ary a un árbol binario.
TreeNode* encode(Node* root) {
si (!root) regresa nullptr;

TreeNode* node = nuevo TreeNode(root-Conval);
si (!root- confíachildren.empty()) {}
node- títuloleft = code(root- títulochildren[0]); // first child
TreeNode* cur = nodo- títuloleft;
para (size_t i = 1; i) ++i) {
cur- tituladoright = código (root- espíritun[i]); // hermanos
cur = cur-iente derecho;
}
}
nodo de retorno;
}

// Decodificar un árbol binario de vuelta a un árbol N-ary.
Nodo* decode(TreeNode* root) {
si (!root) regresa nullptr;

Node* nary = nuevo Node(root- Confval);
TreeNode* cur = root-propleft;
mientras que (cur) {
(decode(cur));
cur = cur-iente derecho;
}
devolver nary;
}
};
`` `

■ **Tip** – En todos los idiomas, nunca olvides la guardia `si (!root)`; de lo contrario golpearás un error 'NullPointerException`/`NoneType`.

-...

## 5. El Bien, el Mal, y el Ugly

Silencio Silencio
Silencio------------Prince------
Silencio **Espacio** Silencio No hay estructuras de datos adicionales; sólo pila de recursión. La profundidad de la Recursión fílmica podría alcanzar 1000 – seguro en Java/Python pero ver la pila de desbordamiento en árboles más profundos. TENN Ninguno; el algoritmo es naturalmente reacio a la cola en la lista de hermanos, pero todavía asigna nuevos objetos `TreeNode`/`Node`. Silencio
Silencio **Hora** Silencio Linear, O(N). tención Ninguno; el algoritmo es óptimo.
Silencio ** Implicidad** Silencio Clear left‐child/right-sibling mapping – fácil de explicar. La lista de niños* es " null " o vacía → cheques extra `null`. Silencio En C++ debe `derezar` nodos después; olvidar que puede causar fugas de memoria. Silencio
Silencio **Perdida** Silencio Perfect bijection. Silencio Ninguno. Silencio Si cambias erróneamente `izquierda/`derecha' durante la codificación, la decodificación fallará silenciosamente. Silencio
Silencio **Desacato** Silencio Meets interview requirement. Debe evitar los globales – puede ser una trampa para los principiantes. Silencio.
Silencio **Testing** Silencio Fácil de escribir pruebas de unidad por ronda. ← Edge‐case `root = null`. ← Los arnés de prueba demasiado complicados pueden ocultar errores. Silencio

### 5.1 Common Gotchas

1. **Null Children List**
*Java* – `root.children` can be `null`. Compruebe `root.children != null` antes de acceder.
*Python* – `niños o []` asegura que una lista esté siempre presente.

2. **Líderes de memoria en C++**
Cada `nueva' debe eventualmente ser emparejado con `delete`. En entrevistas reales se le pide generalmente que *ignore* esto, pero si usted está construyendo una biblioteca, escriba un destructor o utilice punteros inteligentes.

3. ** Límites de velocidad de recusión**
*Python* límite de recursión predeterminado es 1000. Si eres desafortunado y la altura del árbol es igual a ese límite, obtendrás una `RecursionError`.
Java & C++ tienen pilas más grandes, pero sigue siendo una buena idea probar con una profunda cadena de niños.

4. **Inversión de hermanos/niños/derecho**
El intercambio de 'izquierda' y 'derecha' en el encoder romperá el decodificador. Revise siempre el diagrama de mapeo antes de codificación.

-...

## 6. Cómo navegar esta entrevista

1. *Sketch the Mapping*
Dibuja un pequeño nodo N-ary con 3 niños → árbol binario. Muestre el diagrama de la derecha del niño izquierdo.
Las ayudas visuales ganan puntos.

2. **Explicar la recuperación**
* Código* – “Primer niño → izquierda, hermanos → cadena de derechos. ”
*Decode* – “Walk left, then right until `nullptr`. ”

3. **Tiempo & Espacio** – La mención O(N) y O(H) apilan, y aseguran que H ≤ 1000.

4. ** Casos de emergencia**
* Árbol vacío.
* Nodo sin hijos.
* Árboles anchos vs. árboles profundos.

5. Pregunta**
* “¿Prefieres una implementación iterativa para evitar la repetición? ”
* “¿Cómo manejarías un árbol con 105 nodos? ”

Demostrar que usted puede anticipar las compensaciones demuestra una profunda comprensión estructural —exactamente lo que buscan los entrevistadores.

-...

## 6. Bono – Harness de prueba rápida (Python)

``python
def tree_to_list(root):
si no raíz: devuelve Ninguno
volver [root.val] + [tree_to_list(child) para niño en la raíz. niños]

codec = Codec()

# Ejemplo de árbol N-ary:
# 1
# / latitud \
# 2 3 4
# Silencio
# 5
root = Nodo(1, [Nodo 2), Nodo(3, [Nodo(5)]), Nodo(4)])
binario = codec.encode(root)
decodificado = codec.decode(binario)

afirmar árbol_to_list(root) == tree_to_list(decoded)
print("Round‐trip sucedió!")
`` `

Ejecute el snippet arriba en un nuevo intérprete de Python para ver el algoritmo en acción.

-...

## 7. Final Takeaway

"La representación de la derecha del niño izquierdo convierte un árbol de grado arbitrario en un binario sin perder ninguna estructura, y es tan simple como un solo paso recursivo". * *

Ahora tienes:

* **Verified, multi-language solutions** que puedes pegar en cualquier plataforma de codificación.
* A **structured interview answer** explaining the *good*, *bad*, and *ugly* trade‐offs.
* **Keywords** listos para su currículum: * Código N‐ary Tree to Binary Tree*, *LeetCode 431*, *conversión de árboles*, *entrevista de datos sobre la estructura*, *left‐child right-sibling*, *O(N) algoritmo*.

Siéntase seguro de que impresionará a su próximo gerente de contratación con código y estrategia. ¡Feliz codificación! 💻