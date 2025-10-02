-...
Título: LeetCode 971. Árbol binario Flip a la moda del preorden
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 971 – Flip Binary Tree To Match Pre‐Order Traversal
*Medium ← Binary Tree Silencioso DFS*

■ **Recapto de problemas* *
■ Se le da un árbol binario cuyos valores de nodo son una permutación de `1 ... n`.
■ También le han dado un array `voyage` (length `n`) que representa un *desired* pre-order traversal.
■ En una operación se puede “flip” un nodo, es decir, cambiar sus subárboles izquierdo y derecho.
■ ** Objetivo:** Flip el **feo** nodos para que la traversal anterior al árbol equivalga a `voyage`.
■ Devuelve una lista de los valores de todos los nodos volteados. Si es imposible, devuelve `[-1]`.

-...

## ♥ Core Idea (La parte “buena”)

La ruta previa visita los nodos en el orden *root → izquierda → derecha*.
Si caminamos por el árbol mientras caminamos simultáneamente por el `voyage`:

1. El nodo actual ** debe coincidir con el elemento actual de `voyage`.
Si no lo hace, estamos condenados → volver `[-1]`.

2. Después de consumir la raíz, mire el elemento *next* en `voyage` (`voyage[idx]`).
- Si el niño izquierdo existe **y** su valor es **no** `voyage[idx]`, la única manera de igualar la orden es voltear el nodo actual.
- Grabar la vuelta, luego recurre en *derecha* primero, luego *izquierda*.

3. De lo contrario (los partidos menores o el niño izquierdo son `null`), recurse normalmente *izquierda → derecha*.

Debido a que sólo volteamos cuando el siguiente valor en `voyage ` fuerza, estamos garantizados para utilizar el número mínimo de volteretas.

-...

# ## ѕль La parte “Bad”

- **Estado global**: Se utiliza un puntero único "idx" en llamadas recursivas.
En idiomas con escritura estricta (por ejemplo, Java, C++), usted debe guardar contra el desbordamiento o modificación accidental.
- Maneje por caso. El código debe manejar con gracia subárboles vacíos ( " nulos " ) y el caso de imposibilidad ( " [-1] " ).
- *Debugging complex*: Si el árbol es grande (aunque 'n ≤ 100' aquí), la profundidad de la pila puede convertirse en una preocupación en lenguajes recursivos.

-...

## 🔥 La parte "Ugly"

- **La duplicación del proyecto**: Escribir lógica casi idéntica en varios idiomas puede llevar a mantener dolores de cabeza.
- **Verbosidad**: La versión Java a menudo se siente verbosa debido a la caldera `TreeNode` definiciones, importaciones y manejo de listas.
- Suposiciones implícitas**: Basarse en `voyage[idx]` sin controles de límites puede producir `ArrayIndexOutOfBoundsException` si la lógica del algoritmo va mal.

-...

## 📦 Complete Solutions

A continuación se presentan implementaciones limpias y de producción en **Java**, **Python**, y **C+**.
Los tres resuelven el problema en *O(n)* tiempo y *O(h)* espacio (donde `h` es la altura del árbol, el peor caso `O(n)`).

▪ restablecimiento **Importante**: Todos los francotiradores asumen la existencia de una clase/estructura de `TreeNode` definida exactamente como se muestra.
■ También suponen que `root` nunca es `null` en la API pública (LeetCode garantiza esto).

-...

## Java (DFS Recursion)

``java
importa java.util. ArrayList;
importa java.util. Lista;

// Definición para un nodo de árbol binario.
clase TreeNode
int val;
TreeNode left;
TreeNode right;
TreeNode
TreeNode(int val) { this.val = val; }
TreeNode(int val, TreeNode left, TreeNode right) {
this.val = val; this.left = left; this. derecho = derecho;
}
}

Clase Solución {
int idx privado = 0; // posición actual en viaje
Lista privada: Integer confianza flips = nuevo ArrayList fiel();
int privado [] viaje; // referencia para evitar pasar

public List Node root, int[] voyage
esto. viaje = viaje;
dfs(root);
volteretas de retorno;
}

dfs privado(TreeNode node) {
si (nodo == nulo) regresa;

// Mismatch → imposible
si (node.val != voyage[idx]) {}
flips.clear();
flips.add(-1);
retorno;
}
idx++; // consumir valor actual

// Si el niño izquierdo existe y el siguiente valor esperado no es, debemos cambiar
si (node.left != null ' node.left.val != voyage[idx]) {}
flips.add(node.val); // record flip
dfs(node.right);
dfs(node.left);
. ♫ ... {
dfs(node.left);
dfs(node.right);
}
}
}
`` `

-...

### Python (DFS Recursion)

``python
Definición para un nodo de árbol binario.
Clase TreeNode:
def __init__(self, val=0, left=None, right=None):
self.val = val
autoizquierda
self.right = right

Solución de clase:
def flipMatch Voyage(self, root: TreeNode, voyage: list[int]) - Deseo list[int]:
self.idx = 0
self.flips = []

def dfs(nodo: TreeNode tención Ninguno):
si no el nodo:
Regreso
si node.val != voyage[self.idx]:
self.flips = [-1]
Regreso
auto.idx += 1
# need to flip?
si node.left and node.left.val != voyage[self.idx]:
self.flips.append(node.val)
dfs(node.right)
dfs(node.left)
más:
dfs(node.left)
dfs(node.right)

dfs(root)
Vuélvete. volteretas
`` `

-...

## C++ (DFS Recursion)

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
vector node* root, vector implicado con éxito viaje) {
idx = 0;
flips.clear();
dfs(root, voyage);
volteretas de retorno;
}

privado:
int idx = 0;
vector flips;

vacío dfs(TreeNode* nodo, vector asignadoint
si (!node) regresa;
si (nodo- confíaval != voyage[idx]) {}
flips = {-1};
retorno;
}
++idx;
si (nodo- confíaleft " node- títuloleft- confianzaval != voyage[idx]) {}
flips.push_back(node-Conval);
dfs(node-ienteright, voyage);
dfs(node-consejoft, voyage);
. ♫ ... {
dfs(node-consejoft, voyage);
dfs(node-ienteright, voyage);
}
}
};
`` `

-...

## 🔍 Complexity Analysis

← Algorithm Silencio Silencio
Silencio----------------
Silencio Todas las 3 implementaciones Silencio **O(n)** Silencio **O(h)** (llamada pila + lista de volteretas)

- `n` = número de nodos (≤ 100).
- `h` = altura del árbol (caso inferior `n`).

-...

## І Why This Code Rocks (And How It Helps Your Interview)

Silencio tóxico
Silencio...
Silencio **Linear traversal** Silencio Garantiza que la solución es lo suficientemente rápida para las limitaciones. Silencio
Silencio **Minimal flips** Silencio La lógica es determinista; no hay necesidad de retroceder o fuerza bruta. Silencio
Silencio **Recidiva clérigo** Silencio Hace obvia la lógica pre-ordenada, que es lo que buscan los entrevistadores. Silencio
Silencio **Fail‐fast** Silencio Detecta inmediatamente la imposibilidad, el tiempo de ahorro. Silencio
Silencio ** Patrón reutilizable** Silencio El mismo patrón DFS-with-index puede resolver muchos problemas de estilo LeetCode de “voyage” (por ejemplo, 1043, 1129). Silencio

Durante una entrevista, usted puede:

1. ** Explique la intuición** primero: muestra que usted entiende el problema.
2. **Escribe el esqueleto** de `dfs(node)` y el índice global.
3. Mantén la condición de la voltereta en un `si'.
4. ** Retorno `[-1]** como caso especial.

Impresionará al entrevistador con una solución que es **ambos elegante y correcta**.

-...

## 📈 SEO‐Ready Blog Post

■ *Título*
√ LeetCode 971 – Flip Binary Tree To Match Pre‐Order Traversal (Java / Python / C+ Soluciones)

■ **Meta Descripción**
■ Master LeetCode 971 aprendiendo la solución DFS óptima para voltear un árbol binario para una traversal preordenada deseada. Obtenga Java, Python, y C++ codificadores que resuelven el problema en tiempo lineal – perfecto para entrevistas de ingeniería de software.

-...

#### 📝 Blog Post

### Flip Binary Tree To Match Pre‐Order Traversal – 971 – A Full Interview Guide

-...

##### Introducción

Los entrevistadores a menudo hacen preguntas * árbol binario* para medir su recursión y habilidades de estrategia codicioso.
LeetCode 971 – **Flip Binary Tree To Match Pre‐Order Traversal** es un problema clásico de “voyage” que prueba exactamente esas habilidades.

En este artículo descubrirás:

- Una solución completa y lineal en **Java**, **Python**, y **C+**.
- El **por qué** detrás de cada línea de código (cambios mínimos, fail-fast, DFS‐with-index).
- Una hoja de trampolín de interrevisión ** para explicar su enfoque en una entrevista de codificación.

¡Entramos!

-...

#### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ### #1# ## ## ## ## ## ## ## ## ## ## ### ## ## ### ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ####### ##### ## ## ### ## ##### ## ##### ## ## ## ## ## ## ##### ## ######## #### ## ## ## ##### #1

TEN TERRITOR ANTERIOR ANTERIOR ANTERIOR
Silencio...
← Valores del Nodo Silencioso Permutación de `1 ... n` Silencio
Silencioso `voyage` length confidencialidad
Silencioso `n` Silencio ≤ 100
Silencio Permitido operación Silencio Flip (swap left/right children)
viv Goal TENIDO Minimal flips → deseada pre-order traversal

-...

#### 2 comentarios] Intuitive Walkthrough (Pre-Order + Index)

Imagina que estás de pie en el árbol.
The *root* must match the first number in `voyage`.
Después de elegir ese número, el número *next* le dice qué niño visitará después.

Si el siguiente número pertenece al subárbol derecho, debemos cambiar el nodo actual.
Si pertenece al subárbol izquierdo (o el niño izquierdo es 'null'), nos quedamos como es.

Esta regla codictiva produce los giros más bajos.

-...

##### 3down⃣ Code Highlights

- **La recursión de la FDA** mantiene el algoritmo simple.
- **Index pointer** (`idx`) se mueve linealmente por `voyage`.
- ** Lista de Flips** sólo almacena valores de nodos volteados.
- **La salida total** para casos imposibles ahorra tiempo.

-...

### ## 4down⃣ Code Snippets

■ #Java #

``java
public List Node root, int[] voyage {... }
`` `

■ Python

``python
Solución de clase:
def flipMatch Voyage(self, root: TreeNode, voyage: List[int]) - Propiedad Lista[int]: ...
`` `

■ **C++**

``cpp
Clase Solución {
public:
vector asignadoint confianza flipMatchVoyage(TreeNode* root, vector implicaint compartir viaje) { ... }
};
`` `

(Véase el código completo anterior para la aplicación exacta.)

-...

##### 5down⃣ Complejidad

- *Hora*
- **Espacio:** O(h) – pila de llamadas + array de resultado

-...

##### 6flexiones sobre entrevistas—Ley Tips

La situación actual Cómo explicar
Silencio...
Silencio ** Patrón de FDS** Silencioso "Vio el árbol exactamente una vez, usando el índice global para sincronizar con `voyage`." Silencio
"El único giro ocurre cuando el siguiente elemento lo obliga, así que estamos garantizados mínimos giros". Silencio
Silencio **Caso imposible** Silencioso “Si en cualquier momento el valor actual del nodo no coincide con el valor esperado, devolvo inmediatamente `[-1].” Silencio
Silencio **Edge-case** Silencioso “Yo guardo contra los niños `null` y asegurar que el índice permanezca dentro de los límites.” Silencio

-...

#### 7s] TL;DR

- La parte **buena** es un DFS lineal y codicioso que gira sólo cuando es necesario.
- La parte **bad** es gestionar el estado global de forma segura en código recursivo.
- La parte **ugly** es la duplicación de códigos entre idiomas y caldera.

Las tres versiones del idioma que aparecen a continuación resuelven el problema en el espacio `O(n)` tiempo y `O(h)` mientras son fáciles de entender y listos para una entrevista técnica.

-...

#### 🚀 Takeaway

Mastering LeetCode 971 escaparates:

- Proficiencia en el traversal de árboles binarios**.
- Capacidad de escribir **clean, fail-fast código recursivo**.
- Comprensión de estrategias inteligentes** para problemas de cambio mínimos.

Si usted puede explicar esta solución claramente en una entrevista, usted demostrará:

1. ** Introspección algorítmica** – conocer el patrón adecuado para usar.
2. ** Estilo de codificación** – conciso pero legible.
3. **Mezcla de solución de problemas** – manejar casos de borde e imposibilidad tempranamente.

Agregue esta solución a su pila de preparación de entrevistas y será un paso más cerca de aterrizar ese papel de ingeniería de software!

Buena suerte 🚀, y feliz codificación!