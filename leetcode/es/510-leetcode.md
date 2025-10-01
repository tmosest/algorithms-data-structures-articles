-...
Título: LeetCode 510. Sucesor principal en BST II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📝 Problema Recap – LeetCode 510: Sucesor Inordenado en BST II

■ **Given un nodo en un árbol de búsqueda binaria, devuelven el sucesor de ese nodo en el BST. #
■ El sucesor de un nodo es el nodo con la clave más pequeña que es mayor que el valor del nodo dado.
■ Los ganglios del árbol tienen un puntero 'parente' – usted es ** no** dada la raíz del árbol.

*Examples*

← Árbol Silencio Silencioso
Silencio--------Prince----------------
Silencioso[2,1,3]
TENIDA `[5,3,6,2,4,null,null,1]`

**Constraints* *

- 1 ≤ 104
- `-105 ≤ Nodo.val ≤ 105 `
- Todos los valores son únicos

-...

Estrategia de alto nivel

1. ¿Existe el subárbol derecho? #
Si el nodo tiene un hijo adecuado, el sucesor es el nodo *izquierda* en ese subárbol derecho.

2. **No Right Subtree**
Mueva el árbol a través del puntero padre hasta que encuentre un antepasado que sea un **izquierda** hijo de su padre.
Ese antepasado es el sucesor. Si llegas a la raíz sin encontrar tal antepasado, el nodo no tiene sucesor.

Ambos pasos son `O(h)` donde `h` es la altura del árbol, y utilizar `O(1)` espacio extra.

-...

##  Settlements

A continuación se encuentran soluciones limpias y de producción en **Java, Python y C++**.
Los tres usan el mismo algoritmo iterativo y manejan con gracia el caso `null`‐successor.

-...

## Java

``java
*
* Definición para un nodo de árbol binario con puntero padre.
*/
Clase Node {}
int val;
Nodo izquierdo, derecho, padre;
Nodo(int x) { val = x; }
}

Solución de la clase pública {}

*
* Devuelve al sucesor del nodo dado en un BST.
*
* @param node el nodo cuyo sucesor debe ser encontrado
* @return el nodo sucesor, o null si no existe
*/
público Node inorderSuccessor(Node node) {
si (nodo == nulo) vuelve nulo;

/* 1. El nodo tiene subárbol derecho – vaya a su hijo más izquierdo. */
si (node.right!= null) {
Node succ = node.right;
mientras (succ.left!= null) {
succ = succ.left;
}
retorno succ;
}

/* 2. No hay subárbol derecho - subir a través de los padres. */
Node parent = node.parent;
Nodo cur = nodo;
mientras (parente != null " cur == parent.right) {}
cur = padre;
padre = padre.
}
padre de retorno; // puede ser nulo
}
}
`` `

# El arnés de los mejores #

``java
public static void main(String[] args) {
// Árbol de construcción [2,1,3]
Node root = new Node(2);
root.left = nuevo Nodo(1);
root.right = nuevo Nodo(3);
root.left.parent = root;
root.right.parent = root;

Solución s = nueva solución ();
System.out.println(s.inorderSuccessor(root.left).val); // 2
}
`` `

-...

## Python

``python
Clase Nodo:
def __init__(self, val):
self.val = val
self.left = self.right = self.parent = none

Solución de clase:
def inorder Sucesor(yo, nodo: Nodo) - título Nodo:
"
Regrese el sucesor de 'nodo' en un BST.
"
si nodo. Bien.
succ = node.right
mientras que succ.left:
succ = succ.left
retorno succ

# No hay subárbol derecho - subir a través de los padres
padre = nodo.parente
cur = nodo
mientras padre y cura == padre. Bien.
cur = padre
padre = padre.
padre de retorno puede ser ninguno
`` `

**Uso de muestras* *

``python
root = Node(2)
root.left = Nodo(1)
root.right = Node(3)
root.left.parent = root
root.right.parent = root

sol = Solución()
print(sol.inorderSuccessor(root.left).val) # 2
`` `

-...

### C++

``cpp
#include ■iostream

/* Definición de nodo para un BST con puntero padre */
struct Node {}
int val;
Node *left, *right, *parent;
Nodo(int x) : val(x), left(nullptr), right(nullptr), parent(nullptr) {}
};

Clase Solución {
public:
Nodo* inorderSuccesor(nodo*) {
si regresan nullptr;

* Caso 1: subárbol derecho*
si (nodo-principal) {
Node* succ = node-cedright;
(succ- títuloleft)
succ = succ- títuloleft;
retorno succ;
}

/* Caso 2: sin subárbol derecho - subir hasta que el nodo sea un niño izquierdo */
Node* parent = node-consejoparent;
Nodo* cur = nodo;
mientras (padre " curva " == padre- título) {
cur = padre;
padre = padre y padre;
}
padre de retorno; // puede ser nullptr
}
};
`` `

Demo**

``cpp
int main() {}
Node* root = new Node(2);
root- iconoleft = nuevo Nodo(1);
root- título = nuevo nodo(3);
root- iconoleft-ñuelo = root;
root- tituladaright- tituladaparent = root;

Solución s;
Node* succ = s.inorderSuccessor(root- confíaleft);
si (succ) std::cout se hizo succ- títuloval
otro std:::cout se hizo "Ningún sucesor";
}
`` `

-...

## Нели Complexity Analysis

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio Right‐subtree traversal Silencio `O(h)` Silencio `O(1)` Silencio
Silencio Escalada por los padres Silencio
Silencio** Silencio

`h` es la altura del BST (≤ `log n` para equilibrado, `n` para esquemado).

-...

El bueno, el malo y el feo

Silencio Silencio
Silencio------------Prince------
tención **Algorithm sencillez** TEN Iterative, no recursion TEN Requires parent pointers TEN Ninguno – straightforward TEN
Silencio **Uso del espacio** Silencioso (`O(1)`) Silencio Todavía necesita enlaces de padres
Silencio **Uso del tiempo** Silencio Linear en altura Silencioso-caso `O(n)` para árbol escarpado Silencio
Silencio ** Casos de emergencia** Silencio Handled (sin sucesor → `null`) Silencio .
Silencio **Reto de seguimiento** Silencio Resuelto a través de la traversal de padres Silencio

**Takeaway**: El puntero padre es el arma secreta; se convierte en una búsqueda de otra manera `O(n)` en un `O(h)` caminar.

-...

## 📌 Interview‐Ready Tips

1. **Explicar los dos casos** – subárbol derecho vs. subir.
2. **Mención del puntero padre** – es por eso que el “seguimiento” (sin búsqueda de valor) es trivial.
3. **Tiempo/Espacio** – resaltar `O(h)` tiempo, `O(1)` espacio.
4. ** Manejo de edge** – si el nodo es el elemento máximo, devuelve `null`.
5. **Prueba su solución** con árboles equilibrados y segados.

-...

## 📚 Bonus – Follow-Up: “Sin mirar los valores de cualquier nodo”

Cuando sólo se le permite inspeccionar punteros de nodo (no sus valores), el mismo algoritmo funciona porque:

- Nunca comparas los valores – solo navegas `izquierda, 'derecha', y `padre'.
- El sucesor es siempre el primer antepasado** que es un niño **izquierda** de su padre (o el nodo más izquierdo en el subárbol derecho).

Así, la solución iterativa anterior ya es óptima para el seguimiento.

-...

## 📢 SEO > Job‐Boosting Wrap‐Up

- **Título**: Mastering LeetCode 510: Sucesor Inorder en BST II – Java, Python, C++ Soluciones " Entrevista Insights
- **Meta Descripción**: Obtenga la respuesta lista para LeetCode 510. Aprenda el algoritmo sucesor en orden, vea Java limpio, Python y C++ código, y as su entrevista de instrucciones de datos.
- **Keywords**: LeetCode 510, Sucesor Inorder en BST II, sucesor BST, árbol de búsqueda binaria, puntero padre, pregunta de entrevista, solución Java, solución Python, solución C++, tiempo O(h), espacio O(1), entrevista de algoritmo, prep de entrevista técnica.

■ **Ley para impresionar a los reclutadores?** Deje este artículo en su cartera o publicaciones de LinkedIn, y vea a los entrevistadores notar su comprensión profunda de BSTs y lógica puntero.

¡Feliz codificación y buena suerte en la próxima entrevista! 🚀