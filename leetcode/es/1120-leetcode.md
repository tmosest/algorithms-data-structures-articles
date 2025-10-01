-...
Título: LeetCode 1120. Maximum Media Subtree -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Maximum Media Subtree – LeetCode 1120
**El Bien, el Mal y el Ugly - Una Guía de Trabajo-Entrevista-Ley (Java, Pitón, C++)* *

■ **Keywords:**
■ *Maximum Media Subtree*, *LeetCode 1120*, *Binary Tree*, *DFS*, *Recursive*, *Java*, *Python*, *C++*, *Algorithm*, *Problemas de Interrevisión*, *Job Interview*, *Coding*

-...

## 1. Declaración de problemas

Dada la raíz de un árbol binario, devuelve el valor promedio máximo de un subárbol de ese árbol.
Un *subtree* es cualquier nodo más todos sus descendientes.
El valor promedio de un árbol es la suma de sus valores de nodo divididos por el número de nodos.
Las respuestas dentro de 10-5 de la respuesta real serán aceptadas.

**Constraints* *

TEN ANTERIOR ANTERIOR ANTERIOR
Silencio...
TENIDO Número de nodos TENIDO 1 ≤ n ≤ 104 Silencio
← Node.val

-...

## 2. Por qué este problema importa

- **Teree traversal mastery** – a los entrevistadores les encanta ver si puede hacer un DFS post-orden correctamente.
- **Precisión de punto flotante** - el manejo de promedios exige un uso cuidadoso de 'doble'.
- **Space vs. time trade-offs** – el enfoque ingenuo puede llegar a los límites de recursión o desbordamiento.

-...

## 3. El Bien - Una solución Recursiva Limpia

La visión central: **procesa cada subárbol una vez** y propaga dos valores hacia arriba:

1. **sum** – total de todos los valores de nodos en el subárbol
2. **cuenta** – número de nodos en el subárbol

Con estos, el promedio de ese subárbol es simplemente `sum / count`.
Mientras viajamos, mantenemos un máximo global.

### Complexity

Silencio Silencio Silencio Silencio Silencio
Silencio...
Silencio `O(n)` Silencio Cada nodo visitó una vez. Silencio `O(h)` – profundidad de recursión (caso inferior `h = n` para un árbol escarpado). Silencio

-...

## 4. El mal – Pitfalls que debe evitar

Por qué es un problema
Silencio...
Silencio **Modifying node values** in‐place tención Efectos secundarios si el árbol es reutilizado; puede conducir a sumas erróneas. ← Compute sumas por separado. Silencio
Silencio **Usando `int` for sum** Silencio Max sum could be `n * 105 = 109` → todavía cabe, pero más seguro para utilizar `long`. ¦ Utiliza `long` o `long long`. Silencio
Silencio **Profundidad recursiva límite de recursión** Silencio Python puede alcanzar un límite de recursión (por defecto ~1000). Silencio Use DFS iterativa o aumente el límite de recursión (`sys.setrecursionlimit`). Silencio
TEN ** Errores de punto flotante** Silencio Dividir por `int` puede perder la precisión. Difundido a "doble" antes de la división. Silencio
tención **Insectos del estado global** ← Reiniciar la variable global entre los casos de prueba. tención Pass `maxAverage` por referencia o utilizar un campo que se reinicia. Silencio

-...

## 5. Los Casos Ugly - Manejo de Edge

← Edge Case Silencioso Silencioso Cómo lo manejamos
Silencio...
Silencio **Todos los nodos tienen el mismo valor** Silencio Cada subárbol tiene un promedio idéntico; el algoritmo todavía funciona. No es necesario un manejo especial. Silencio
tención **Tree with a single node** Silencio Promedio es que el valor del nodo; la recursión debe regresar correctamente. El caso base devuelve `sum = val`, `count = 1`. Silencio
Silencio ** Árbol profundo muy profundo** Silencio El riesgo de desbordamiento de Stack. Use optimización de recursión (no disponible en Java/Python) o pila iterativa. Silencio
Silencio **Gran número de nodos** Silencioso El límite del tiempo excedió si no lineal. El DFS lineal está garantizado. Silencio

-...

## 6. Código Snippets

A continuación se ** tres implementaciones idiomáticas** que compilan en LeetCode y la mayoría de las plataformas de entrevista.

### 6.1 Java

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
Doble maxAverage privado = Doble. NEGATIVE_INFINITY;

doble máximo público Promedio Subtree(TreeNode root) {
dfs(root);
retorno maxAverage;
}

// Devoluciones {sum, count}
long[] dfs(TreeNode node) {
si (nodo == null) devuelve nuevo largo []{0, 0};

long[] left = dfs(node.left);
long[] right = dfs(node.right);

long sum = left[0] + right[0] + node.val;
cuenta larga = izquierda[1] + derecha[1] + 1;

doble avg = (doble) suma / cuenta;
maxAverage = Math.max(maxAverage, avg);

devolver nuevo largo[]{sum, count};
}
}
`` `

### 6.2 Python

``python
Definición para un nodo de árbol binario.
# class TreeNode:
# def __init__(self, val=0, left=None, right=None):
# self.val = val
# Yo. izquierda = izquierda
# Yo. derecho = derecho

Solución de clase:
def máximo MediaSubtree(self, root: TreeNode) - título flotante:
auto.max_avg = flotante('-inf')
self.dfs(root)
volver a sí mismo.max_avg

def dfs(self, node: TreeNode):
si no el nodo:
0, 0 # suma, cuenta

left_sum, left_cnt = self.dfs(node.left)
right_sum, right_cnt = self.dfs(node.right)

total_sum = left_sum + right_sum + node.val
total_cnt = left_cnt + right_cnt + 1

auto.max_avg = max(self.max_avg, total_sum / total_cnt)
total_sum, total_cnt
`` `

### 6.3 C++

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
doble máximo Promedio Subtree(TreeNode* root) {
maxAvg = -std::numeric_limits obtenidosdouble confianza::infinity();
dfs(root);
volver maxAvg;
}

privado:
doble maxAvg;

// devoluciones par realizado, con relación
std::pair obtenidos durante mucho tiempo, intilo dfs(TreeNode* node) {
si regresan {0, 0};

auto izquierda = dfs(node-consejoft);
derecho automático = dfs(node-Conderight);

larga suma = izquierda. primera + derecha.primero + nodo- títuloval;
Int count = izquierda. segundo + derecho. segundo + 1;

maxAvg = std::max(maxAvg, static_cast seleccionadodouble(sum) / count);
volver {sum, count};
}
};
`` `

-...

## 7. Cómo podrían preguntarse los entrevistadores

← Pregunta sobre lo que realmente están probando
Silencio...
Silencio ¿Puedes explicar cómo evitas recomputar las sumas del subárbol? Silencio espera DFS con la memoización de la suma " cuenta. Silencio
Silencio ¿Y si el árbol es cortado? ¿La recursión explotará? ← Conocer la profundidad de recursión = altura, discutir alternativas iterativas. Silencio
¿Por qué usaste `doble` en lugar de 'float'? Precisión permanente " tolerancia LeetCode. Silencio
Silencio ¿Cómo adaptarías esto para encontrar el subárbol con el promedio mínimo? La lógica del espejo con `min`. Silencio

-...

## 8. Cierre optimizado de SEO

Si te estás preparando para tu próxima entrevista de ingeniería de software **, dominando el **Maximum Media Subtree** problema muestra que puedes:

1. **Arboles binarios transversales** eficientemente (DFS, post-order).
2. **Precisión numérica múltiple* con cuidado.
3. **Código limpio, mantenible** en Java, Python y C++.

Siéntete libre de copiar los snippets arriba, ejecutelos en LeetCode, y tweak ellos para la velocidad.
Recuerde explicar la intuición, la complejidad y los casos de borde durante su entrevista—estos son los *buenos* partes que impresionan a los gerentes de contratación.

Feliz codificación, y la mejor suerte de aterrizar ese trabajo de ensueño! 🚀

-..