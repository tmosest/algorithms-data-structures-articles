-...
Título: LeetCode 333. Subtree -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 Largest BST Subtree – LeetCode 333
**A Deep‐Dive, O(n) Solution + Code in Java, Python & C++ + SEO‐Ready Blog Post**

-...

### 🎯 Problema Resumen

Dada la raíz de un árbol binario, encuentre el tamaño (número de nodos) del subárbol más grande ** que es también un Árbol de búsqueda binaria (BST)**.
Un subárbol debe contener a todos sus descendientes, es decir, no puede caer los nodos en el medio.

Silencio Punto clave Silencio Descripción
Silencio...
Silencio **Regla BST** Silencio Por cada nodo, todos los valores en el subárbol izquierdo node.valo Identificar todos los valores en el subárbol derecho
Silencio ** Objetivo** Silencio Regresar el *maximum* número de nodos entre todos estos subárboles BST
tención **Constraints** Silencio `0 ≤ 104`, `-104 ≤ nodo.val ≤ 104` Silencio
TENIDO **Siguiente** TENIDO Achieve O(n) time, O(n) space (recursive stack)

-...

## 📌 Optimal O(n) Approach

Recorrer el árbol una vez (post-order).
En cada nodo compute **cuatro piezas de información** para el subárbol arraigado en ese nodo:

Silencio en el campo
Silencio...
¿Este subárbol satisface las propiedades del BST? Silencio
tención `size` Silencioso Número de nodos en este subárbol (si es un BST)
Silencio `minVal` Silencio Valor mínimo en este subárbol
Silencio `maxVal` Silencio Valor máximo en este subárbol

### Recurrencia

1. **Caso de base** – Un niño vacío es considerado como un BST con tamaño 0, min = +∞, max = -∞.
2. Para un nodo `root`:
Recursively get `left` and `right`.
- `root' es un BST **iff**
`left.isBST " derecha.isBST " izquierda.maxVal " detect root.val " root.val "
- Si es un BST:
- tamaño = izquierda.size + derecha.size + 1`
- `minVal = min(root.val, left.minVal) `
- `maxVal = max(root.val, right.maxVal) `
- De lo contrario, marca `isBST = false` y mantén `size = max(left.size, right.size)` (BST más grande encontrado más profundo).

La respuesta es la mayor `tamaño' encontrada durante el traversal.

Esto se ejecuta en **O(n)** tiempo porque cada nodo es visitado una vez, y utiliza el espacio O(n) para la recidiva (o O(h) si se elimina la recursión de la cola).

-...

## 🧑 💻 Code Implementations

### 1. Java

``java
*
* Definición para un nodo de árbol binario.
* clase pública TreeNode {
* int val;
* TreeNode left;
* TreeNode right;
* TreeNode(int x) { val = x; }
*
*/
Clase Solución {
Clase privada estática Información {
boolean isBST;
tamaño de la tinta; // tamaño del BST si es BST == verdadero
int min; // min value in this subtree
int max; // valor máximo en este subtree
Info(boolean isBST, int size, int min, int max) {
this.isBST = isBST;
este.size = tamaño;
esto.min = min;
esto.max = max;
}
}

int ans privado = 0;

más grande BSTSubtree(TreeNode root) {
dfs(root);
devolver los ans;
}

información privada dfs(TreeNode node) {
si (nodo == nulo) {
// Subárbol vacío: BST válido de tamaño 0
volver nuevo Info(true, 0, Integer. MAX_VALUE, Integer.MIN_VALUE);
}

Información izquierda = dfs(node.left);
Info right = dfs(node.right);

// Compruebe la condición BST para el nodo actual
si (izquierda.esBST " derecha. isBST
" izquierda.max " node.val " curva node.val " {}
int sz = izquierda.size + derecha.size + 1;
int mn = Math.min(node.val, left.min);
int mx = Math.max(node.val, right.max);
as = Math.max(ans, sz);
volver nuevo Info(true, sz, mn, mx);
}

// No es un BST: propagar el mejor tamaño encontrado hasta ahora
as = Math.max(ans, Math.max(left.size, right.size));
volver nuevo Info(falso, 0, 0, 0); // tamaño es irrelevante aquí
}
}
`` `

-...

### 2. Pitón

``python
Definición para un nodo de árbol binario.
# class TreeNode:
# def __init__(self, val=0, left=None, right=None):
# self.val = val
# Yo. izquierda = izquierda
# Yo. derecho = derecho

Solución de clase:
def mayor BSTSubtree(self, root: TreeNode) - int:
self.ans = 0

def dfs(node):
si no el nodo:
# vacío subtree: BST of size 0
(True, 0, flotador('inf'), flotante('-inf'))

left_is_bst, left_size, left_min, left_max = dfs(node.left)
right_is_bst, right_size, right_min, right_max = dfs(node.right)

# El nodo actual forma un BST?
si la izquierda_is_bst y la derecha_is_bst y la izquierda_max node.val
sz = left_size + right_size + 1
mn = min(node.val, left_min)
mx = max(node.val, right_max)
self.ans = max(self.ans, sz)
(True, sz, mn, mx)
más:
self.ans = max(self.ans, left_size, right_size)
(False, 0, 0, 0)

dfs(root)
Vuélvete. ans
`` `

-...

### 3. C++

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
struct Info {
bool isBST;
tamaño de la tinta; // tamaño si esBST==true
int minV;
int maxV;
Info(bool b, int s, int mn, int mx) : isBST(b), size(s), minV(mn), maxV(mx) {}
};

más grande BSTSubtree(TreeNode* root) {
int ans = 0;
dfs(root, ans);
devolver los ans;
}

privado:
Info dfs(TreeNode* node, int disminuye ans) {
si (!node)
volver Info(true, 0, INT_MAX, INT_MIN); // árbol vacío

Información izquierda = dfs(node-consejoft, ans);
Información derecha = dfs(node-cedright, ans);

if (left.isBST " correctamente.isBST "
izquierda.maxV se realizó nodo- implicaval " curva node- títuloval " derecha.minV) {}

int sz = izquierda.size + derecha.size + 1;
ans = max(ans, sz);
int mn = min(node-ciendoval, left.minV);
int mx = max(node-ciendoval, right.maxV);
volver Info(true, sz, mn, mx);
}

ans = max(ans, max(left.size, right.size));
volver Info(falso, 0, 0, 0); // tamaño es irrelevante cuando no es un BST
}
};
`` `

-...

¿Qué hace esta solución?

Silencio Silencio
Silencio------------Prince------
Silencio **La complejidad del tiempo** ← O(n) – visita cada nodo una vez ← N/A TENCIÓN
Silencio **Complejidad del espacio** ← O(n) recursion stack (O(h) if tail-optimised) Silencio N/A ← Ninguno ←
Silencio **Readability** Silencio Usa un claro `Info`/tuple return; comentarios en línea Silencioso verbose en Java debido a la clase de ayuda Silencio Ninguno Silencio
Silencio **Edge Cases** Silencio Handles árbol vacío, valores negativos, valores duplicados, árboles profundos
Silencio **Pitfall** tención Olvídate de inicializar `min`/`max` para los niños null → comparación incorrecta ← Sobre-complicar con estructuras de datos adicionales Silencio Ninguno Silencio

### Common Gotchas

1. ** Valores incorrectos del centinela** – Usar `+∞` para min en niño vacío y `-∞` para máx. En Java: `Integer.MAX_VALUE / Integer.MIN_VALUE`.
2. **Wrong min/max updates** – Para un nodo BST, `min` es el menor de su propio valor y el min del subárbol izquierdo; `max` es el mayor de su propio valor y el max del subárbol derecho.
3. **Descubriendo propagar el mejor tamaño** – Incluso cuando un subárbol no es un BST, sus hijos podrían contener el mayor BST; mantener el mejor tamaño visto hasta ahora.

-...

Recursos adicionales

- **In-order traversal check** – La secuencia en orden de un BST debe estar aumentando estrictamente.
- ** Programación Dinámica en árboles** – Patrón similar utilizado para el diámetro del subárbol, mayor BST en el árbol binario, subárbol suma problemas.
- **Orden post-ordenativo** – Utilice una pila explícita para evitar el flujo de la pila de recursión para árboles extremadamente profundos.

-...

## 🎯 Interview Take‐ Away

*"Explica cómo encontraría el subárbol BST más grande en un árbol binario, y por qué utilizaría un traversal post-orden." *

Puntos de conversación clave:
- Post-order asegura que la información de los niños esté disponible antes de procesar al padre.
- El patrón Info reduce el número de pases a través del árbol.
- Discutir los valores centinela y por qué `+∞` / ``-∞` son seguros independientemente de los valores de ganglio.

-...

## ⋅ Call‐to‐Action

💬 **¿Quieres dominar más preguntas de entrevista de LeetCode? * *
- **Suscribir** para soluciones semanales Java/Python/C++.
- **Descargar** la hoja de trampolín “LeetCode 333 – más grande BST Subtree”.
- **Compartir** este post en LinkedIn o Twitter con #LeetCode333, #BST, #CodingInterview.

-...

#### 🏁 Summary

- El problema BST Subtree más grande es un problema de árbol clásico DP.
- Un DP post-orden limpio que devuelve `esBST, tamaño, min, max` produce una solución **O(n)**.
- Proporcionamos ** código de producción** para **Java, Python y C++** – copy‐paste, run, e impresiona al gerente de contratación.

¡Buena suerte con tu entrevista de codificación, y sigue resolviendo!