-...
Título: LeetCode 2265. Conde Nodos Igual a Promedio de Subtree -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🛠中文 2265 - Conde Nodos iguales a la media de Subtree
** Código de la resolución (Java / Python / C++)**

-...

#### 1ICK⃣ El problema (LeetCode 2265)

■ **Given** un árbol binario, **cuenta** el número de nodos cuyo valor es igual al *floor* del promedio de todos los valores de nodos en su subárbol (incluyendo el nodo en sí).

- `average = ⌊(sum of values) / (number of nodes) `
- Tamaño del árbol: 1 ... 1000
- Node.val ≤ 1000

-...

## 2down Core Idea – Post-Order DFS

Por cada nodo que necesitamos:
1. **Sum** de su subárbol
2. **Counto** de los nodos en su subárbol

Un **post-order** (izquierda → derecha → nodo) traversal nos da estos dos números para los niños *antes* computándolos para el padre.
Una vez que tengamos `(sum, contar)` para un nodo, podemos comprobar:

``text
si (sum / count == node.val) →
`` `

Esto da un solo paso O(N) tiempo, O(H) pila de recursión (H = altura del árbol, ≤ N).

-...

## 3down Código

A continuación se encuentran soluciones limpias y de producción para **Java**, **Python**, y **C+**.
Todos usan la misma estrategia del DFS y están listos para pegar en LeetCode.

-...

### 3.1 Java

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
respuesta int privada = 0;

*
* Devuelve un array: [sum of subtree, node count].
*/
int privado[] dfs(TreeNode node) {
si (nodo == null) devuelve nuevo int[]{0, 0};

int[] left = dfs(node.left);
int[] right = dfs(node.right);

int sum = left[0] + right[0] + node.val;
int count = left[1] + right[1] + 1;

si (sum / count == node.val) respuesta++;

devolver nuevo int[]{sum, count};
}

en promedio De Subtree(TreeNode root) {
dfs(root);
respuesta de retorno;
}
}
`` `

-...

#### 3.2 Python

``python
Definición para un nodo de árbol binario.
# class TreeNode:
# def __init__(self, val=0, left=None, right=None):
# self.val = val
# Yo. izquierda = izquierda
# Yo. derecho = derecho

Solución de clase:
def promedio DeSubtree(self, root: TreeNode) - título int:
cuenta propia = 0

def dfs(node):
si no el nodo:
retorno 0, 0 # (sum, nodos)

left_sum, left_cnt = dfs(node.left)
right_sum, right_cnt = dfs(node.right)

total_sum = left_sum + right_sum + node.val
total_cnt = left_cnt + right_cnt + 1

si total_sum // total_cnt == node.val:
self.count += 1

total_sum, total_cnt

dfs(root)
Vuélvete. Cuenta
`` `

-...

### 3.3 C++

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
int ans = 0;

// Pareja de retorno: {sum, count}
treeNode*
si regresan {0, 0};

auto [sumL, cntL] = dfs(node- títuloleft);
auto [sumR, cntR] = dfs(node-correct);

larga duración total Sum = sumL + sumR + node- títuloval;
total Cnt = cntL + cntR + 1;

si (totalSum / totalCnt == nodo- títuloval) ++ans;

Retorno total Sum, total Cnt};
}

promedio DeSubtree(TreeNode* root) {
dfs(root);
devolver los ans;
}
};
`` `

■ **¿Por qué 'largo' en C++? #
" consuma " puede ser hasta " 1000 = 1e6 " , todavía cabe en " , pero el uso " largo " mantiene la aplicación a prueba de futuro.

-...

## 4VIEW⃣ Blog Article (SEO‐Optimized)

■ *Título*
■ **“Mastering LeetCode 2265 – Count Nodes Equal to Media of Subtree”* *
*A Deep Dive into DFS, Edge Cases, and Interview‐Ready Tricks*

■ **Meta Descripción (Ω160 chars):**
■ Solve LeetCode 2265 en Java, Python & C++ con un solo paso DFS. Entender el algoritmo, la complejidad, las trampas, y cómo llegar a esta pregunta de entrevista de árbol binario.

-...

#### 4.1 Introducción

Al romper entrevistas de codificación, los problemas de árbol binario dominan el paisaje.
LeetCode 2265 – *Count Nodes Equal to Media of Subtree* – es una estrella “médium” que mezcla técnicas de traversal con razonamiento aritmético.

■ **Por qué importa:**
• Demonstrates mastery of deep‐first search (DFS).
* Muestra la capacidad de trabajar con datos agregados (sum " count).
* Prueba la atención a la división y redondeo enteros.

Vamos a romper el problema, caminar a través de una solución óptima, explorar las trampas, y terminar con el código completo en **Java, Python, C+**.

-...

### 4.2 Problema Recap (Key Points)

TENIDO ANTERIOR ANTERIOR ANTERIOR
Silencio...
Silencio ** Objetivo** Silencio Cuenta nodos donde `node.val == ⌊sum(subtree) / count(subtree)⌋`. Silencio
Ø N ≤ 1000, 0 ≤ val ≤ 1000
Silencio **Tree Size** tención Lo suficientemente pequeño para el DFS recursivo, pero lo suficientemente grande para cuidar de la profundidad de la pila. Silencio

-...

#### 4.3 “Bien” – Por qué Post-Order DFS Gana

1. **Se agrega desde el fondo hacia arriba*
- Post-order garantiza que conocemos las sumas de los niños antes de calcular las de los padres.
- No hay necesidad de estructuras auxiliares de datos (como colas).

2. **Tiempo " Complejidad espacial**
- **O(N)** tiempo - cada nodo procesado una vez.
- **O(H)** pila de recursión – H es altura (≤ N, pero en árboles equilibrados ♥ tronco N).

3. *Simlicidad*
- Una función recursiva devuelve un tuple `(sum, count)`.
- Inmediatamente utilizable para actualizar la respuesta global.

■ **Bottom line:** *Un solo pase DFS le da toda la información que necesita. *

-...

### 4.3 Step‐by‐Step Walkthrough (Pseudo Code)

`` `
DFS(nodo):
si node == null:
(sum = 0, conteo = 0)

izquierda Sum, leftCnt = DFS(node.left)
rightSum, rightCnt = DFS(node.right)

total Sum = izquierdaSum + derecha Sum + node.val
total Cuenta = izquierda Cnt + derecha Cnt + 1

totalSum // total Cuenta == nodo.val:
respuesta += 1

(totalSum, totalCount)
`` `

**Notice:** `/` (o `/` en idiomas enteros) realiza * división de suelos*, exactamente lo que el problema requiere.

-...

### 4.4 “Bad” – Pitfalls comunes Cómo evitarlos

Silencio Pitfall Silencio ¿Por qué es malo
Silencio--------------------------
Silencio **Using Pre‐Order** Silencio Necesitarías conocer las sumas de los niños primero → pases dobles o almacenamiento temporal. ← Uso post-orden DFS. Silencio
Silencio **Desbordamiento entero** Silencio Resumiendo 1000 nodos de valor 1000 → 1.000.000 (se ajusta en 32 bits), pero en entradas más grandes u otros problemas que esto puede rebosar. TENIDO Use 64-bit (`long' en C++ / `long` en Java) para seguridad. Silencio
Silencio ** División de Bronce** Silencio `sum / count` vs `sum // count`. ¦ Uso integer division **floor** – in Java `int / int` is already floor, in Python use `/`. Silencio
Silencio **Null Node Handling** ← Regresar `null` sin caso base → `NullPointerException`. Silencio Regresar `{0,0}` para los niños `null`. Silencio
Silencio **Depth de estaca** ← Árbol desequilibrado profundo (por ejemplo, lista conectada) → profundidad de la recursión ~ N. ¦ O use pila iterativa o aumente el límite de recursión en Python. Silencio

-...

### 4.5 “Ugly” – Edge Cases & Corner Scenarios

1. **Tree with all equal values* *
- El promedio de cada nodo equivale al valor del nodo → respuesta = N.
2. **Arbolado (lista enlazado)* *
- Altura = N → profundidad de recursión = N. En Python puede necesitar `sys.setrecursionlimit(2000)`; en Java/C+++ funciona bien para N = 1000.
3. ** Valor nominal 0**
- Promedio también podría ser 0 – no se necesita un manejo especial, pero asegúrese de que la división por cero nunca ocurre.
4. ** Valores más importantes* *
- Aunque 'val ≤ 1000', summing 1000 nodos todavía encaja en 32 bits, pero en pruebas personalizadas con mayores restricciones debe promover a 64 bits.

-...

### 4.6 Interview‐ Consejos listos

TENIDO TENDIDO ANTERIOR Por qué ayuda a vivir
Silencio...
Silencio **Explicar la idea post-orden** antes de bucear en código. Muestra que entiende por qué los niños son procesados primero. Silencio
Silencio **La complejidad de la mención** temprano. Silencio
Silencio **Hablar sobre la división entero**: "la división del suelo es el predeterminado en los idiomas enteros". tención Destaca el conocimiento del lenguaje. Silencio
Silencio **La profundidad de la pila de mención**: "caso inferior O(N), pero los árboles equilibrados son O(log N)". Silencio
Silencio **Probar casos de prueba** (por ejemplo, nodo único, todos los mismos valores, árbol escarpado). ← Demuestra minuciosidad. Silencio

-...

### 4.7 Full Reference Code (Java / Python / C++)

■ *Los fragmentos de código de abajo están completamente comentados y listos para copiar en LeetCode. *

##### Java

``java
Clase Solución {
respuesta int privada = 0;
int privado[] dfs(TreeNode node) {
si (nodo == null) devuelve nuevo int[]{0, 0};
int[] left = dfs(node.left);
int[] right = dfs(node.right);
int sum = left[0] + right[0] + node.val;
int count = left[1] + right[1] + 1;
si (sum / count == node.val) respuesta++;
devolver nuevo int[]{sum, count};
}
en promedio De Subtree(TreeNode root) {
dfs(root);
respuesta de retorno;
}
}
`` `

#### Python

``python
Solución de clase:
def promedio DeSubtree(self, root: TreeNode) - título int:
cuenta propia = 0
def dfs(node):
si no no nodo: retorno 0, 0
left_sum, left_cnt = dfs(node.left)
right_sum, right_cnt = dfs(node.right)
total_sum = left_sum + right_sum + node.val
total_cnt = left_cnt + right_cnt + 1
si total_sum // total_cnt == node.val:
self.count += 1
total_sum, total_cnt
dfs(root)
Vuélvete. Cuenta
`` `

###### C++

``cpp
Clase Solución {
public:
int ans = 0;
treeNode*
si regresan {0,0};
auto [sumL, cntL] = dfs(node- títuloleft);
auto [sumR, cntR] = dfs(node-correct);
larga duración total Sum = sumL + sumR + node- títuloval;
total Cnt = cntL + cntR + 1;
(totalSum / total Cnt == node-propval) ++ans;
Retorno total Sum, total Cnt};
}
promedio DeSubtree(TreeNode* root){
dfs(root);
devolver los ans;
}
};
`` `

-...

### 4.8 Testing & Validation

Silencio Test Silencioso Árbol Silencio Esperado Respuesta
Silencio...
Silencio, silencio.
Silencio **Todo igual** Silencio Árbol equilibrado de todos los `1`s soporta `N` (todos los partidos del nodo)
Silencio **Separado** Silencio cadena de tejido izquierdo 3‐2‐1 Silencio `1` (sólo los fósforos de hoja)
Silencioso **Mixed** Silencio `2, 2, 4, 5, 2` (véase el ejemplo del problema)

Ejecutar el código contra estas pruebas confirma la corrección y no revela errores ocultos.

-...

### 4.9 Pensamientos Finales

- **Bueno** – Un DFS de una línea que captura dos agregados por nodo; solución O(N) limpia.
- **Bad** – Over-engineering with extra data structures or double passs wastes time and memory.
- **Ugly** – Olvidar la división de enteros (por ejemplo, usar `doble` en lugar de `int`) dará la WA en pruebas ocultas.

Recuerde: **Los problemas de entrevista de árboles binarios son todos sobre patrones de traversal**. Mastering DFS y agregación post-orden le da una poderosa herramienta que se aplica a innumerables problemas de LeetCode (por ejemplo, “Binary Tree Level Order Traversal”, “Maximum Binary Tree” etc.).

-...

#### 5down⃣ Clausura

■ Con las soluciones anteriores, puedes enviar con confianza a LeetCode 2265 en **Java, Python, o C+**, y tus entrevistadores verán que tienes:

- Código limpio y mantenible escrito
- Casos de bordes manejados y redondeo entero correctamente
- Optimizado para el espacio de tiempo

Ahora, engranaje para su próxima entrevista de codificación —hit “Solve” en LeetCode 2265, conseguir que **✔ ↑ ↑** insignia, y dejar que los entrevistadores estén impresionados!

-...

Recursos útiles

TEN TERRITOR SON SON SON SON SON
Silencio...
TEN LeetCode 2265 – Problema TENIDO http://leetcode.com/problems/count-nodes-equal-to-average-of-subtree/ Silencio
Silencio DFS Tutorial (Java) Silencio https://www.geeksforgeeks.org/ profunda-first-search-or-dfs-for-a-graph/ Silencio
TENIDOS Básicos del Árbol Binario TENIDO https://www.tutorialspoint.com/data_structures_algorithms/binary_tree.htm Silencio
tención de entrevistas previas en https://leetcode.com/problemset/all/ Silencio

-...

¡Feliz Codificación