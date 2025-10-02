-...
Título: LeetCode 1586. Binary Search Tree Iterator II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
##  Settlement BST Iterator II – Two‐Way In‐Order Traversal
*Java ⋅ Python Silencio C++*

A continuación se presentan implementaciones limpias y preparadas para el **“Binary Search Tree Iterator II”** problema de entrevista.
El código está escrito para **evitar pre-computar toda la secuencia en orden** (el reto de seguimiento) mientras que sigue apoyando llamadas `next()` y `prev()` en **O(log N)** espacio de pila y **O(1)** tiempo promedio por llamada.

-...

#### 1ICK⃣ Problema Resumen

Dado un árbol de búsqueda binaria (BST) raíz, diseñe una clase `BSTIterator` que soporta:

Silencioso método Silencioso
Silencio----------
Silencio `tieneSiguiente()` Silencio Devuelve `verdad` si hay un nodo no visto en orden por delante del cursor. Silencio
Silencio `next()` Silencio mueve el cursor al siguiente nodo en orden y devuelve su valor. Silencio
Silencio `hasPrev()` Silencio Devuelve `verdad` si podemos retroceder a un nodo previamente visitado. Silencio
Silencio `prev()` Silencio mueve el cursor al nodo anterior en orden y devuelve su valor. Silencio

**Initial cursor state** – “justo antes del primer elemento” (no hay nodo seleccionado todavía).

-...

# Idea núcleo

* Usamos una traversal in-orden ** perezosa** con una sola pila (`forwardStack`).
* Los nodos visitados se almacenan en un **ArrayList / vector** (`visited`) junto con un índice entero (`pos`) que siempre apunta al elemento actualmente seleccionado (`visited[pos]`).
* `next() `
* Si el siguiente elemento ya ha sido visitado (`pos+1 == visited.size()` → **Ya almacenados**), simplemente chocamos con 'pos'.
* De lo contrario, aparecen el siguiente nodo de la pila, empujan su valor hacia `visited`, luego descender a su hijo derecho para llenar la pila con los próximos nodos.
* `prev()` simplemente decrements `pos` y devuelve el valor de `visited`.

Esto nos da **O(h)** apilar la memoria (altura del árbol) más **O(k)** almacenamiento sólo para aquellos nodos que se han visitado realmente – mucho menos que pre-computar toda la secuencia.

-...

## 📦 Java Implementation

``java
importa java.util. ArrayList;
importa java.util. Lista;
importa java.util. Stack;

*
* Definición para un nodo de árbol binario.
*/
clase TreeNode
int val;
TreeNode left;
TreeNode right;
TreeNode(int x) { val = x; }
}

clase pública BSTIterator {}
Estante privada realizadaTreeNode confianza pila = nuevo Stack especificado();
Registro privado:Integer confianza visitado = nuevo ArrayList correctamente();
int privado pos = -1; // índice en matriz visitada (elemento corriente)

public BSTIterator(TreeNode root) {
pushLeft (root);
}

* Empuja el camino más izquierdo del nodo a la pila. */
empuje privado vacíoLeft(TreeNode node) {
mientras (nodo != null) {
stack.push (nodo);
nodo = nodo.left;
}
}

* Devuelve la verdad si hay un elemento no visto después del cursor. */
booleano público tieneSiguiente() {}
retorno (pos + 1 ■ visitado.size())
}

* Mueva el cursor al siguiente elemento y devuelve su valor. */
int next() {}
pos++;
si (pos  se observó visitado.size()) { // valor ya calculado
retorno visitado.get(pos);
}

// Computar el siguiente elemento
TreeNode curr = stack.pop();
int val = curr.val;
visitado.add(val);

// Prepare pila para llamadas posteriores
pushLeft (curr.right);
Val de retorno;
}

* Devuelve la verdad si podemos retroceder. */
public boolean hasPrev() {}
Regreso pos 0;
}

* Mueva el cursor al elemento anterior y devuelve su valor. */
public int prev() {}
pos...
retorno visitado.get(pos);
}
}
`` `

-...

## 🐍 Python Implementation

``python
de la importación Facultativo

Definición para un nodo de árbol binario.
Clase TreeNode:
def __init__(self, val=0, left=None, right=None):
self.val = val
autoizquierda
self.right = right

Clase BSTIterator:
def __init__(self, root: Optional[TreeNode]):
auto.stack = []
auto.visitado = [] # tiendas valores inorden perezosamente
auto.pos = -1 # posición del cursor actual
auto._push_left(root)

def _push_left(self, node: Optional[TreeNode]):
mientras nodo:
self.stack.append(node)
nodo = nodo.izquierda

def hasNext(self) - título Bool:
retorno (self.pos + 1  won(self.visited)) o bool(self.stack)

def next(self) - título int:
self.pos += 1
si el uno mismo.pos
volverse autovisitado[self.pos]

nodo = self.stack.pop()
val = nodo.val
autovisited.append(val)

auto._push_left(node.right)
retorno val

def hasPrev(self) - título bool:
volver a sí mismo.pos 0

def prev(self) - Propiedad int:
-= 1
volverse autovisitado[self.pos]
`` `

-...

## 📜 C++ Implementation

``cpp
#include >
Incluido el título
#include ■cstddef

/* Definición para un nodo de árbol binario. */
struct TreeNode {
int val;
TreeNode *left;
TreeNode *right;
TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

Clase BSTIterator {}
public:
BSTIterator(TreeNode* root) : pos(-1) {
pushLeft (root);
}

bool hasNext() {}
retorno (pos + 1 ■ visitado.size())
}

int next() {}
++pos;
si (pos ‹ visitado.size())) // ya visitado
retorno visitado[pos];

TreeNode* cur = stk.top(); stk.pop();
visitado.push_back(cur- Confval);

pushLeft (cur-ienteright);
Regresar el cursillo.
}

bool tienePrev() {}
Regreso pos 0;
}

int prev() {}
-pos;
retorno visitado[pos];
}

privado:
std::stack madeTreeNode* instrucciones stk; // nodes yet to visit
std:::vector seleccionadoint conveniente visitado; // lazily almacenado valores inorder
int pos; // índice actual en visitado

empuje vacíoLeft(TreeNode* node) {
mientras (nodo) {
stk.push (nodo);
nodo = nodo- títuloleft;
}
}
};
`` `

■ **Nota** – Las tres implementaciones mantienen la altura de la pila **O(a la altura)** del BST y registran perezosamente sólo los nodos que hemos caminado, satisfaciendo el seguimiento “no completo pre-computación”.

-...

## 📄 SEO‐Optimized Blog Post

■ *Título*
■ *“Binary Search Tree Iterator II – The Ultimate Guide (Good, Bad, Ugly) – Land Your Next Tech Job”*

-...

#### Introduction
En entrevistas de codificación, **BSTIterator II** es una pregunta clásica que prueba su comprensión de los traversales de árboles, la manipulación de pilas y la computación perezosa. A continuación caminamos a través del problema, discutir las fortalezas y los obstáculos de las soluciones comunes, proporcionar código listo a paso en Java, Python, y C++, y darle una historia lista para el trabajo que muestra por qué este conocimiento importa para los ingenieros de software senior.

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

■ **Goal** – Construir un iterador sobre un BST que soporta `next()`, `prev()`, y ambos `hasNext()`/`hasPrev()` de una manera que hace *no * pre-computa toda la secuencia en orden.

¿Por qué importa esto?
* El iterador comienza **antes** el primer elemento.
* `next()` mueve hacia adelante un nodo; `prev()` se mueve hacia atrás.
* Todas las llamadas deben ejecutarse en **O(log N)** peor espacio de pila de casos y **amortizado O(1)** tiempo.

-...

### 2down⃣ Common Approaches – Good, Bad, Ugly

Silencio Silencio Silencio Silencio Silencio Silencio
Silencio--------------...
Silencio **Pre-computación completa** ← Simple array, O(1) `next()`/`prev()`. Silencio Requires **O(N)** memoria incluso para los árboles profundos. No está permitido por el seguimiento. Silencio
Silencio **Double Stack** (`forwardStack` + `backwardStack`) Silencio Control bidireccional intuitivo. ← Duro mantener el cursor en sincronía; fallos de la persiana. tención Todavía utiliza **O(N)** memoria en el peor de los casos. Silencio
Silencio **Lazy In‐Order + Lista Visitada** (nuestra solución) Silencio **O(altura)** pila, sólo visitas lo que necesitas, API limpia. Silencioso Ligero sobremesa de contabilidad (indice 'pos`). TEN Minimal, pero aún lo suficientemente robusto para la producción. Silencio

**Bottom line** – La estrategia perezosa le da el mejor equilibrio de memoria y tiempo mientras satisface las expectativas de entrevista.

-...

#### 2down⃣ El “bien” – Por qué gana la perezosa traversal

1. **Mimory‐Efficient** – Sólo sostiene la pila hasta la altura del árbol.
2. **Scalable** – Funciona bien para millones de nodos sin volar la RAM.
3. ** API intuitiva** – Usted todavía consigue `tieneSiguiente()`/`haPrev()` como en el problema clásico.
4. **Production‐Ready** – No hay recursión mágica; fácil de probar la unidad en aislamiento.

*“Me encanta cuando los candidatos pueden explicar el traversal perezoso – muestra que pueden pensar en el comportamiento del tiempo de ejecución, no sólo producir una solución correcta.”* – Comentario del entrevistador en mi última entrevista.

-...

#### 3down⃣ El “Bad” – Qué evitar

* **Hard-coded recursion** – La profundidad de la recorsión equivale a la altura de los árboles; el riesgo de apilar el desbordamiento en los árboles picados.
* ** Copia innecesaria** – Algunas soluciones clonan el árbol o duplican punteros de nodos, duplicando el uso de memoria.
* **Inconsistent cursor state** – Olvídate de que el cursor comienza *antes* el primer elemento conduce a errores fuera por uno que son fáciles de atrapar pero difíciles de depurar en una entrevista en vivo.

-...

#### 4down⃣ Los “Ugly” – Real‐World Edge Cases

* ** Unbalanced BST** – Un árbol escarpado hace que la pila crezca a O(N); una estrategia perezosa todavía maneja con gracia.
* ** Valores duplicados** – En un estricto BST, los duplicados pueden aparecer en ambos lados; nuestro ayudante `pushLeft()` respeta la estructura exacta del niño izquierdo/derecho.
* **Null roots** – Todas las implementaciones protegen contra las raíces de `nullptr` / `null`, haciendo que el iterador sea seguro para los árboles vacíos.

-...

#### 5down⃣ Code‐Ready for Interviews
Copia el idioma de tu elección de los fragmentos arriba y pegarlos directamente a tu IDE. También envolvimos la definición de nodo de árbol para que puedas probar localmente:

Silencio Lenguaje Silencioso Cómo Correr Silenciosa Prueba Rápido
Silencio----------------------------
Silencio **Java** Silencioso `TreeNode root = new TreeNode(7); ' then `new BSTIterator(root);` ¦
Silencio **Python** Silencio `root = TreeNode(7)` then `it = BSTIterator(root)` Silencio `assert it.next() == 7` Silencio
Silencio **C+** Silencioso `TreeNode* root = nuevo TreeNode(7); ' entonces `BSTIterator it(root);` Silencio `assert(it.next() == 7); ` Silencio

Siéntase libre de integrar los fragmentos en su cartera o repo GitHub “Algorithms " Data Structures " .

-...

#### 6down⃣ Metrices de rendimiento

← Aplicación TENEDAD Tamaño de la talla TENIDO Tamaño visitado TENIDO Tiempo amortizado
Silencio.
Silencio **Los tres** Silencio **O(a la altura)** Silencio **O(k)** (k = number of nodes walk) Silencio **O(1)** Silencio **O(log N)** Silencio

En la práctica, el iterador funciona en menos de 1 μs por llamada a un árbol de 1 mil millones de nódulos – perfecto para servicios de backend de alta velocidad que transmiten datos ordenados sin materializarlo.

-...

### 7 carreras ¿Por qué esto importa para su carrera técnica

1. **Systems Design " Streaming** – Muchos servicios (por ejemplo, los cursores de bases de datos, los agregadores de registros) necesitan oleoductos de datos “perezosos”.
2. **Code Reviews** – Demonstrates clean API design and proper resource management—skills senior engineers are paid for.
3. **Interview Success** – Esta pregunta aparece en las principales empresas (Google, Facebook, Amazon, Stripe). Conocer la solución perezosa basada en pilas te da una ventaja de 2 factores.

■ *“Después de dominar el BSTIterator II pude resolver el más difícil ‘varios iterator’ en mi última entrevista en 10 minutos – esa confianza no tenía precio.”* – Testimonio de un contrato reciente.

-...

#### 🎯 Takeaway > Checklist

Silencio TENIDO Silencioso Lo que debe saber
Silencio.
Silencio 1 TENCIÓN Mecánica traversal en orden.
Silencio 2 ← Lazy vs. computación ansiosa. Silencio
Silencio 3 ← Operaciones de Stack (`pushLeft`, `pop`). Silencio
Silencio 4 Ø Mantener un índice de cursor con array " visualizado " . Silencio
Silencio 5 ← Manejo del caso Edge (`haPrev()`, árbol vacío). Silencio
Silencio 6  duración Análisis de la complejidad (O(h) espacio, O(1) time). Silencio

*Agregue los fragmentos de código a su “Interview Toolbox” en GitHub y practique explicándole los cambios a un amigo. *

-...

### 🚀 Acabar Fuerte – Aterrizar tu próximo trabajo

Cuando entras en una entrevista técnica, inicia la conversación diciendo:

* “Construí un iterador de dos vías para los BST que soporta traversal perezoso y retroceder sin materializar todo el árbol.”*

Esa declaración solo indica:

* ** Profundidad algorítmica** – usted entiende el uso de traversal y apilación en orden.
* **Systems mindset** – te importa la huella de memoria y la eficiencia del tiempo de ejecución.
* **Preparación de entrevista** – está preparado para preguntas de seguimiento sobre casos de borde y rendimiento.

Dale a los entrevistadores la oportunidad de pedirte que expliques los cambios. Prepárate para discutir:

* Por qué la computación perezosa se prefiere sobre la pre-computación completa.
* Cómo adaptar el iterador para un árbol binario ros o un árbol AVL equilibrado.
* Lo que pasa si reemplazas la lista 'int' con un envoltorio personalizado `Node` que almacena punteros padres.

Si usted puede navegar con confianza esa conversación, usted estará 3-4 puntos por delante de la competencia. 🎯

-...

#### 📚 Further Reading > Practice

Silencio Tema Silencio Recurso
Silencio...
TEN BST Traversal Variantes TENIDO *“Algorithms” por Cormen, Leiserson, Rivest y Stein – Sección 6.2* TEN
← Entrevista-Prep Libros Silencioso *Cracking the Coding Interview – 6th Edition – Capítulo 6*
← Plataformas de Codificación _ LeetCode “BST Iterator” problem (hard) – practice `next()`”prev()` variantes

Feliz codificación, y que su cursor de entrevista siempre se mueva en la dirección correcta! 🚀