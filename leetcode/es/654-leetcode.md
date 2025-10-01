-...
Título: LeetCode 654. Árbol binario máximo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Maximum Binary Tree – The Good, The Bad, and The Ugly
**LeetCode 654 – Una profunda inmersión en algorítmica Pensamiento* *

-...

## Tabla de contenidos

Silencio Sección Silencio Lo que aprenderás
Silencio...
Silencio | Problema Declaración Silencio Entender el desafío y las limitaciones
Silencio 🔍 Naïve Approach ← O(n2) divide‐y-conquer Silencio
Repetición clásica: clara pero lenta
TEN | Monotonic Stack ANTE O(n) solución óptima
← Tiempo > Complejidad Espacial ← Donde la parte “muy” se esconde
TEN 🧪 Casos de Edge " Pruebas de la vida Haga su código a prueba de balas
← Pitfalls comunes para evitar los errores más frecuentes
Silencio 🚀 Take‐away & Career Impact Silencio Por qué dominar este asunto para las entrevistas
Silencio 📚 Otros recursos Silencio Profundice su conocimiento Silencio

■ **SEO Palabras clave**: *Maximum Binary Tree, LeetCode 654, algoritmo, pila monotónica, construcción de árboles, preparación de entrevistas, solución Java, solución Python, solución C++, división y conquista, complejidad del tiempo, complejidad del espacio. *

-...

Declaración de problemas

■ #Maximum Binary Tree #
■ Se le da un array 'nums' de enteros distintos.
■ Construir un árbol binario utilizando las siguientes reglas:
■ 1. La raíz es el elemento máximo de " años " .
■ 2. El subárbol izquierdo es el árbol binario máximo de la sub-array izquierda del max.
■ 3. El subárbol derecho es el árbol binario máximo de la sub-array derecha del max.

Devuelve el nudo raíz del árbol construido.

■ **Constraints**
* `1 ≤ nums.length ≤ 1000`
* `0 ≤ nums[i] ≤ 1000`
* Todos los enteros en `nums` son únicos.

-...

## 2down Naïve Approach – Brute Force

La solución más directa refleja la descripción:

``text
encontrar índice de máximo en nums
crear nodo con ese valor
recursivo en la rebanada izquierda
recursivo en la rebanada derecha
`` `

### Complexity
*Encontrar el máximo* lleva `O(k)` donde `k` es la longitud de la rebanada.
En cada nivel partimos el array, por lo que el trabajo total se convierte

`` `
T(n) = T(k1) + T(k2) + O(n) - título O(n2)
`` `

Para `n = 1000`, esto todavía está bien para LeetCode, pero rápidamente se vuelve incalable y una entrevista clásica "gotcha".

-...

## 3down⃣ Divide " Conquer - Recursive O(n2) Solución

Una aplicación más limpia utiliza la recursión con un ayudante que acepta un rango de índice.

``java
Clase Solución {
public TreeNode constructMaximumBinaryTree(int[] nums) {
helper(nums, 0, nums.length - 1);
}
privada TreeNode helper(int[] nums, int l, int r) {}
si regresan nulos;
int maxIdx = l;
para (int i = l + 1; i)
si (nums[i] > nums[maxIdx]) maxIdx = i;
TreeNode node = nuevo TreeNode(nums[maxIdx]);
node.left = helper(nums, l, maxIdx - 1);
node.right = helper(nums, maxIdx + 1, r);
nodo de retorno;
}
}
`` `

■ **The Good** – *Clear, concise, y coincide perfectamente con la descripción del problema. *
■ **El malo** – *La complejidad del tiempo `O(n2)`. *
■ **El Ugly** – *Los escaneos lineales repetidos, el uso innecesario de la memoria y la profundidad de la pila pueden volar para entradas más grandes. *

-...

## 4down Sta Monotonic Stack – The Optimal `O(n)` Solución

### La vista clave

Al construir el árbol, **el orden relativo de los elementos es lo que importa**.
Cuando procesas `nums` de izquierda a derecha, solo necesitas saber el elemento más grande ** - el elemento que se convertirá en el padre del nodo actual.

Una pila decreciente **monotónica mantiene nodos cuyos valores están disminuyendo estrictamente de abajo a arriba.
Cuando llega un nuevo valor x:

1. Todos los nodos en la pila con el valor `traducido x` se convierten en el niño *izquierda* de `x`.
2. Si la pila no está vacía después de saltar, el nuevo niño *derecha* se convierte en `x`.
3. Empuje `x` en la pila.

Al final, el **abajo de la pila** es la raíz del árbol binario máximo.

### Complexity
*Cada nodo es empujado y saltado al máximo una vez* → **O(n)` tiempo**.
Espacio en estadio: **`O(n)`**.

## Java Implementation (Monotonic Stack)

``java
Clase Solución {
public TreeNode constructMaximumBinaryTree(int[] nums) {
si (nums == null 0) Retorno nulo;

Deque cumplióTreeNode confía stack = nuevo ArrayDeque indica();

para (int num : nums) {
TreeNode cur = nuevo TreeNode(num);

// Todos los nodos con menor valor se convierten en niños izquierdos
mientras (!stack.isEmpty() " bulb.peek().valo 0 observado num) {
cur.left = stack.pop();
}

// La parte superior actual (si existe) se convierte en niño derecho de Cur
si (!stack.isEmpty()) {}
stack.peek().right = cur;
}

stack.push(cur);
}

// El fondo de la pila es la raíz
volver stack.peekLast();
}
}
`` `

■ **El Bien** – *Runs en tiempo lineal y es fácil de entender una vez que la idea de apilar supera. *
■ **El malo** – * curva de aprendizaje interior; manipulación de pila puede ser propensa al error. *
■ **El Ugly** – *En idiomas sin tipos de pila incorporados (por ejemplo, C) tienes que administrar los punteros manualmente. *

### Python Implementation (Monotonic Stack)

``python
de la importación List, Optional

Clase TreeNode:
def __init__(self, val: int = 0, left: 'TreeNode' = Ninguno, right: 'TreeNode' = Ninguno):
self.val = val
autoizquierda
self.right = right

Solución de clase:
def constructMaximumBinary Tree(self, nums: List[int]) - Propiedad Opcional[TreeNode]:
pila = []
para las numidades:
nodo = TreeNode(num)
mientras que la pila y la pila[-1].val
node.left = stack.pop()
si la pila:
[-1].right = nodo
stack.append(node)
la pila de retorno[0] si la pila de otra
`` `

## C++ Implementación (Monotonic Stack)

``cpp
struct TreeNode {
int val;
TreeNode *left, *right;
TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

Clase Solución {
public:
TreeNode* constructMaximumBinaryTree(vector fieltro nums) {
vector realizadoTreeNode*
para (int num : nums) {
TreeNode* node = nuevo TreeNode(num);
mientras (!st.empty() " st.back()- Confval " significa num) {
nodo- título = st.back();
st.pop_back();
}
si (!st.empty())
st.back()- correctamente = nodo;
st.push_back(nodo);
}
volver st.empty() ? nullptr : st.front();
}
};
`` `

-...

## 5down⃣ Edge Cases " Testing

Silencio Test Silencio Descripción
Silencio--------------------------------
Silencioso `[]’
TENIDO `[7]` TENIDO Único elemento TENIDO `TreeNode(7)` Silencio
Silencio `[1,2,3,4,5]` Silencio Resucitando estrictamente la vida `TreeNode(5)` con todos los niños de la izquierda
Silencioso `[5,4,3,2,1]` . .
Silencio `[3,2,1,6,0,5]` Silencio Mixed Silencio `TreeNode(6)` con subárboles por ejemplo

**Tip**: Usa un ayudante para atravesar el árbol y serializarlo en un array (orden nivel) para compararlo con la salida esperada de LeetCode.

-...

## 6walks comunes

Silencio Pitfall Silencio Por qué no funciona
Silencio--------------------------
Silencio **Acondicionamiento de la pila incorrecta** ( " = " ) Los valores Duplicados no están permitidos, pero el uso de ```' puede aparecer demasiados nodos.
Silencio **No establecer `izquierda` después de saltar** Silencio El nodo saltado se convierte en el niño *derecha* incorrectamente. Silencioso Assign `cur.left = popppedNode` dentro del bucle. Silencio
Silencio **Regresar el elemento de pila incorrecto** latitud Regresar `stack.peek()` da el nodo más reciente, no la raíz. Silencio Regresar `stack.peekLast()` (abajo de la pila). Silencio
Silencio **Memoria fugas en C+** Silencio Olvídate de los nodos de 'delete'. Use punteros inteligentes (`std:unique_ptr`) o un destructor. Silencio
Silencio **Desbordamiento de profundidad de recursión** Silencio Solución Recursiva utiliza la profundidad de pila `O(n)`. Silencio

-...

## 7 carreras Por qué Mastering Esto importa

* ** Mentalidad Algorítmica** – Convertir una descripción en un patrón eficiente de estructura de datos es una habilidad de entrevista básica.
* ** Fluencia de estructura de datos** – Los árboles binarios y las pilas monotónicas son temas de entrevista frecuentes.
* **Tiempo-espacio-offs** – Ser capaz de detectar la parte cuadrática “muy” y mejorarla demuestra la profundidad de solución de problemas.
* **La versatilidad en el idioma crusario** – Impresionará a los reclutadores si puede resolver el mismo problema en **Java, Python y C+** (o cualquier otro idioma que ame).

■ **Career Take-away**:
■ *LeetCode 654 es un problema “mostrar” – se ve fácil, pero la solución óptima esconde un patrón sutil.
■ Resolviéndolo elegantemente le dará un impulso de confianza para entrevistas de estructura de datos y le ayudará a colocar roles que valoren código limpio y eficiente. *

-...

Otros recursos

1. **Monotonic Stack Pattern** – *LeetCode discusión hilo*
2. **Recursive Tree Construction** – *CS‐Academy’s “Build Tree from Pre-order ' In-order”*
3. ** Gestión de memorias en C+** – *“Unique_ptr and Smart Pointers” en GeeksforGeeks*
4. **Entreview Prep Books** – *“Cracking the Coding Interview” – Capítulo on Binary Trees & Stack*
5. **YouTube Walk‐through** – * La lista de reproducción “Monotonic Stack” de Ben Awad (Python + JavaScript)*

-...

## 🎯 Final Take‐away

■ *El Árbol binario Máximo es un problema engañosamente simple que recompensa una visión más profunda del algoritmo. *
■ Al pasar de un escaneo de fuerza bruta a una pila **monotónica**, conviertes una solución `O(n2)` en una `O(n)` limpia que destacará en entrevistas.

Sigue practicando el patrón – aparece en otros problemas de LeetCode como ** “El rectángulo Largest en Histograma”** y ** “Maximum Sum Rectangular Subarray”**. Dominar esta idea es un pequeño paso que puede elevar todo su conjunto de habilidades de coding-interview.

Buena suerte, y feliz codificación! 🚀