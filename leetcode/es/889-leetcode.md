-...
Título: LeetCode 889. Construir el Árbol binario de Preorder y Postorder Traversal -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 889. Construir el Árbol binario de Preorden y Postorden Traversal
** Idiomas:** Java Silencio Python Silencio C++
**Dificultad:**
**Entrevista-ready:**

-...

#### ## 1down⃣ Java Implementation

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
public TreeNode constructDePrePost(int[] preorder, int[] postorder) {}
// Mantenemos un puntero mutable al índice actual en el preorden
int[] idx = nuevo int[]{0};
(preorden, postorder, idx, 0, postorder.length - 1);
}

privada TreeNode build(int[] pre, int[] post, int[] idx,
int postStart, int postEnd) {}
si (idx[0] pre.length ← permanecer en la vida postIniciar не postEnd) volver null;

// Root of the current subtree
TreeNode root = nuevo TreeNode(pre[idx[0]++]);

// Si este nodo es una hoja, no hay niños que apeguen
si (postStart == postEnd) raíz de retorno;

// Encontrar el índice del niño izquierdo en postorden
int leftVal = pre[idx[0];
int left Idx = postStart;
(post[leftIdx]!= izquierdaVal) izquierda Idx++;

int left Tamaño = izquierda Idx - postStart + 1;

// Recursively build left ' right subtrees
root.left = build(pre, post, idx, postStart, leftIdx);
root.right = build(pre, post, idx, leftIdx + 1, post Fin - 1);

raíz de retorno;
}
}
`` `

-...

#### 2down⃣ Python Implementation

``python
Definición para un nodo de árbol binario.
Clase TreeNode:
def __init__(self, val=0, left=None, right=None):
self.val = val
autoizquierda
self.right = right

Solución de clase:
def construct FromPrePost(self, preorder: list[int], postorder: list[int] TreeNode:
# use a list as a mutable pointer into preorder
self.idx = [0]
volver a sí mismo._build(preorden, postorder, 0, len(postorder) - 1)

def _build(self, pre, post, post_start, post_end):
si auto.idx[0] √≥= len(pre) or post_start √≥ post_end:
No.

root = TreeNode(pre[self.idx[0])
self.idx[0] += 1

# Nodo de hoja - no niños
si post_start == post_end:
raíz de retorno

left_val = pre[self.idx[0]
left_idx = post_start
mientras que post[left_idx] != left_val:
left_idx += 1

left_size = left_idx - post_start + 1

root.left = self._build(pre, post, post_start, left_idx)
root.right = self._build(pre, post, left_idx + 1, post_end - 1)

raíz de retorno
`` `

-...

### 3down⃣ C++ Aplicación

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
TreeNode* constructDesdePrePost(vector identificadoint limitada preorder, vector seleccionadointющ postorder) {}
// Índice de preordenado mutable
int idx = 0;
(preorden, postorder, idx, 0, postorder.size() - 1);
}

privado:
TreeNode* build(vector fieltro);
int postStart, int postEnd) {}
si (idx не= pre.size() ненный postStart не postEnd) devuelve nullptr;

TreeNode* root = nuevo TreeNode(pre[idx++]);

// Nodo de hoja
si (postStart == postEnd) raíz de retorno;

int left Val = pre[idx];
int left Idx = postStart;
(post[leftIdx]!= leftVal) ++leftIdx;

int left Tamaño = izquierda Idx - postStart + 1;

root- títuloleft = build(pre, post, idx, postStart, leftIdx);
root- correctamente = build(pre, post, idx, leftIdx + 1, post Fin - 1);

raíz de retorno;
}
};
`` `

-...

## 📄 Blog Artículo: "El Bien, el Mal, y el Ugly"
### **Construir el Árbol binario de Preorder " Postorder - Una guía completa para las entrevistas**

-...

##### 📝 Tabla de contenidos
1. [Introducción " Contexto](#introducción)
2. [Problema general](#problema vista previa)
3. [Por qué este problema importa en las entrevistas](#interview-matters)
4. [The Good: Why the Solution is Beautiful](#the-good)
5. [The Bad: Common Pitfalls > Edge‐Case Gotchas](#the-bad)
6. [The Ugly: Complex Cases & How to Tame Them](#the-ugly)
7. [Algorithm & Complexity](#complexity)
8. [Testing Strategy " Sample Unit Tests](#testing)
9. [Take‐away & Career‐Boost Tips](#takeaway)
10. [Conclusión](#conclusión)

-...

#### 1ICK⃣ Introduction > Context
■ **LeetCode 889** – *Construct Binary Tree de Preorder y Postorder Traversal* – es una piedra de las entrevistas técnicas, especialmente en las grandes empresas tecnológicas y las startups fintech.
■ Dominar este problema demuestra que usted puede **reason with recursion**, understand **tree traversal properties**, y producir soluciones limpias **O(N)** en varios idiomas.

**Keywords:** *LeetCode 889*, *Construct Binary Tree from Preorder and Postorder*, *Binary Tree Reconstruction*, *Coding Interview*, *Job Interview Prep*.

-...

## ## 2down⃣ Problem Overview

- ** Entrada:** Dos arrays enteros: `preorder` (root → left → right) y `postorder` (left → right → root).
Nodo de raíz del árbol binario que coincide con ambos traversales.
- *Constraints*
- Todos los valores de los nodos son... únicos.
- Número de nodos " n " satisfies " 1 " = n " = 30 " (pero la solución es más grande " n " ).

■ ¿Por qué es difícil? * *
■ A diferencia del postorden " preorden o inorden " , no puede mapear directamente los índices de nodos; el árbol es **no se define únicamente**. Un árbol válido todavía está garantizado porque la entrada es consistente.

-...

#### 3down⃣ Por qué este problema importa en las entrevistas

Esquía de la vida por qué se le pregunta
Silencio...
Silencio **Recursión** Silencio Muchos entrevistados luchan con la construcción de árboles recursivos. Silencio
Silencio ** Mapping Index** Silencio Demuestra la comprensión de las relaciones traversales. Silencio
Silencio ** Optimización del espacio** Silencio Muestra la capacidad de minimizar las estructuras de datos adicionales. Silencio
Silencio **Multi‐language Mastery** Silencio Los empleadores esperan que usted traduzca algoritmos entre Java, Python, C++, etc. Silencio

■ **SEO Boost** – Incluir frases como *“Solución LeetCode 889”*, *“pregunta de entrevista de árboles binarios”*, *“entrevista de codificación Java Python C++”* para clasificar más alto en los resultados de búsqueda de reclutadores que buscan resolver problemas probados.

-...

#### 4down⃣ El Bien – Lo que hace Este problema es grande

Feature Silencio Por qué Es Positivo
Silencio...
Silencio **Patrón de Recursión de cable** tención Root → dividido en izquierda/derecha basado en el siguiente valor de preorden. Silencio
Silencio **No hay mapa de Hash Extra Necesitado** Silencio Una simple búsqueda lineal en postorder mantiene el código legible. Silencio
Silencio **Linear Time Complexity** Silencio Cada nodo es visitado una vez: **O(N)**. Silencio
Silencio ** Estructura del árbol determinista** Silencio Cualquier par preorden/postorder válido produce *a* árbol correcto (no necesariamente único). Silencio
tención **Idioma Agnóstico** Silencio La misma lógica se aplica en Java, Python, C++, Vamos, etc. Silencio

**Takeaway:** Enfóquese en el ayudante recursivo* que utiliza un índice preordenado mutable y límites postorden. Es el patrón que hace la solución elegante.

-...

#### 5down⃣ Los malos – errores comunes " Edge‐ Case Quirks

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------------
Silencio **Using a HashMap for value → postorder index** tención añade espacio extra O(N); todavía está bien pero innecesario para pequeñas limitaciones. tención Realizar un escaneo lineal (`mientras post[i] != pre[idx]`) – funciona porque cada elemento es examinado al máximo dos veces. Silencio
Silencio **Incorrect postorder bounds** Silencio Off‐por-one errores producen `NullPointerException` / `None` nodes in wrong places. tención Recuerde que el último elemento del segmento postorden es la raíz actual (`postEnd`). Silencio
Silencio **Asumiendo que el árbol está lleno** Silencio Algunas soluciones erróneamente piensan que cada nodo interno debe tener dos hijos; esto falla por los árboles de punta derecha. tención Check `postStart == postEnd` para identificar hojas. Silencio
TEN **No actualizar el índice de preorden después de la recursión** ANTERIENTE Líderes para duplicar nodos o niños desaparecidos. Use un envoltorio mutable ( " idx " en Java, " idx[0] " en Python) que se incrementa una vez por nodo. Silencio
TEN **Failing to subtract 1 from postEnd for right subtree** TEN añade la raíz del subtree actual a la recursión subtree derecha. Silencio Uso `postEnd - 1` al construir el subárbol derecho. Silencio

■ **Tipo de depuración:** Visualizar con un pequeño ejemplo:
" texto
" Preorder " : [1, 2, 4, 5, 3, 6]
[4, 5, 2, 6, 3, 1]
" `
■ Paso a través de la recursión manualmente para ver dónde cambian los índices.

-...

#### 6down⃣ Casos Ugly – Árboles no únicos & Edge

¿Por qué es una estrategia de manejo permanente?
Silencio----------------------------------------...
Silencio **Nodos infantiles solo** Silencio Un nodo puede tener sólo un niño izquierdo (o sólo un niño derecho). En tales casos, el “tamaño del subárbol izquierdo” sigue determinado correctamente porque el niño izquierdo es el siguiente elemento en el preorden. TEN Recursion lo maneja automáticamente; no se necesitan banderas especiales. Silencio
Silencio **Tree with All Nodes in One Line (Skewed)** Silencio Preorder y postorder son idénticos (por ejemplo, `[1,2,3]` & `[3,2,1]`). El algoritmo todavía debe crear un árbol derechista válido. La condición de hoja de `postStart == postEnd ' detiene la recursión, preservando la forma asfaltada. Silencio
Silencio ** Empty Input** Silencio No se permite por limitaciones LeetCode, pero el código defensivo es trivial. Silencio Add guard `if (pre.length == 0) Retorno nulo;`. Silencio
Silencio **Large Input (n ≤ 30)** tención Los datos de entrevista real pueden ser más grandes; el uso de 'mientras' para encontrar índice en postorden podría convertirse en \(O(N^2)\) si se implementa ingenuamente. tención Construye un hashmap `valor - índice de confianza` una vez para la búsqueda O(1), alcanzando verdadero O(N). Para las limitaciones medias (≤30) el escaneo lineal está perfectamente bien. Silencio

-...

### 7Ω⃣ Time & Space Complexity

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
TEN Java TENIDO **O(N)** – Cada nodo se procesa una vez; el escaneo lineal de postorden ocurre O(1) por nivel de recursión. TEN **O(N)** – Profundidad de pila de recesión hasta `N`; no hay estructuras de datos adicionales. Silencio
Silencio Python Silencio **O(N)** Silencio **O(N)** – Profundidad de recuperación e índice mutable. Silencio
TENIDO C++ TENIDO **O(N)** Silencio **O(N)** – Profundidad de la capa; cada creación de nodos es tiempo constante. Silencio

■ **Proof of Optimality:**
√ - El aumento del índice de preorden es constante por nodo.
√ - Los escaneos de postorde paran en el niño izquierdo, que es único.
- Para los árboles escarpados, profundidad de recursión = `N`; para los árboles equilibrados = `O(log N)`.

-...

### 8️ Testing Strategy & Sample Unit Tests

``python
def inorder(root):
si no raíz: retorno []
inorder (root.left) + [root.val] + inorder(root.right)

def test_pre_post(pre, post):
root = Solution()._build(pre, post, 0, len(post)-1)
afirma inorder(root) == ordenados(pre) # no útil, sólo cheque de cordura
# Build expected tree manually for small case:
# 1
# / \
# 2 3
# / \
# 4 5
# ...
`` `

■ **Idea de prueba automatizada:**
- Generar valores únicos aleatorios.
Construir un árbol binario aleatorio.
- Computar su postorden " .
≤ - Alimentar para solucionador; luego verificar `preorder(root)` y `postorder(root)` coinciden con los originales.

■ **Por qué ayuda al programa:** Demostra la capacidad de *validar* soluciones programáticamente, una habilidad crucial en los análisis de códigos de producción.

-...

#### 9Ω⃣ Take‐away & Career‐ Consejos de Boost

1. **Traducción entre idiomas:** Mostrar reclutadores puede implementar la misma lógica en Java, Python y C++ en una sola entrevista.
2. *Explica tu recuperación* Siempre verbalice el índice *preorden* y la lógica * segmento postorden*.
3. **Emphasize Space Efficiency:** Mention that you could add a hashmap for O(1) index lookup, but opted for a simpler solution given constraints.
4. **Mostrar código de muestra en el resumen:** Añade una bala: *Implemented LeetCode 889 en Java, Python, y C++ con O(N) complejidad. *
5. **Practice Edge Cases:** Derechado, zurdo, nodos de un solo niño, y tamaños mínimos de árboles.

■ **Resume Hook:** “Implementado eficiente algoritmo de reconstrucción de árboles binarios para LeetCode 889 en Java, Python y C++, logrando tiempo lineal y complejidad espacial. ”

-...

Conclusión

Mastering **LeetCode 889** te equipa con un kit de herramientas **recursion + index-mapping** que es altamente transferible a través de entrevistas de codificación.

- **El Bien** – Recidiva limpia, tiempo lineal, lenguaje-agnóstico.
- **El malo** – Cuidado con los límites y las actualizaciones del índice que faltan.
- **El Ugly** - Manejar árboles no únicos y elegantes.

■ Al practicar el patrón anterior, no sólo resolver el problema, sino también señalar a los reclutadores que usted es cómodo **abstracting conceptos a través de idiomas**, **optimizing space**, y **debugging complex recursion**.

Tu siguiente paso: Construir una pequeña herramienta de línea de comandos que acepta dos arrays e imprime el árbol en orden de nivel; incluirlo en su sitio web de cartera o GitHub readme para mostrar su solución en vivo para contratar administradores.

-...

¡Feliz codificación!

■ *Listo para tu próxima entrevista? Sumérgete en las soluciones, ponlas en tu IDE favorito, y luego empuja tu repo a GitHub con mensajes de compromiso claros. Las soluciones de problemas visibles, bien documentadas. *

-...



-...

■ *Descargos* Los fragmentos de código anteriores son completamente compilables en sus respectivos entornos (Java 17+, Python 3.10+, C+17). Verifique siempre el problema de LeetCode para cualquier restricción oculta antes de enviar.

-..