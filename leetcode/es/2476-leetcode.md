-...
Título: LeetCode 2476. Búsquedas más cercanas en un árbol de búsqueda binaria -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 2476. Búsquedas más cercanas en un árbol de búsqueda binaria
### LeetCode ← Medium tención Entrevista Solución lista (Java ← Python Silencio C++)

-...

### 🚀 TL;DR
* **Problema** – Para cada consulta *q* encontrar:
* * *mini* = valor más grande ≤ *q* en el BST (o **‐1** si ninguno).
* * * máxi* = valor más pequeño ≥ *q* en el BST (o **‐1** si ninguno).
* **Aprobación** – Convertir el BST en un array surtido ** (en la traversal ordenada) y utilizar la búsqueda binaria (`bisect`/`lower_bound`) para cada consulta.
* Complejidad*
*Time* : **O(n + m log n)** ( *n* = #nodes, *m* = #queries)
*Espacio*: **O(n)** (para la matriz ordenada)
* **Por qué importa** – Muestra conocimiento profundo de las propiedades BST, el traversal de árboles y la búsqueda eficiente – perfecto para cualquier entrevista de ingeniería de software senior.

-...

Declaración de problemas (LeetCode 2476)

■ **Input**
* `root` – root of a binario search tree (BST).
* `queries` – lista de números enteros positivos.
■ **La salida*
■ Un array de 2-D 'respuesta' donde
> `answer[i] = [mini, maxi]` para la consulta *i*‐th.

■ *Examples*
" texto
î root = [6,2,13,1,4,9,15,null,null,null,null,null,null,null,null,14]
[2,5,16]
[2,2],[4,6],[15,-1]
" `

-...

Intuición & Diseño

TENIDO ANTERIOR ANTERIENTE ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTE ANTE
Silencio----------...
tención ** propiedad BST** – cada niño izquierdo se llevó a cabo padre o hija derecha. Silencio **Escaneo luminoso** para cada consulta es O(n · m) → TLE en 105 nodos/queries. Silencio **Ignorar los casos de borde** (no predecesor/succesor) conduce a resultados incorrectos. Silencio
TEN **In‐order traversal** da una matriz ordenada → fácil búsqueda binaria. **El almacenamiento del árbol entero** de nuevo (por ejemplo, TreeSet) es innecesario. **Búsqueda binaria incorrecta** (errores falsos por uno) identifica erróneamente los límites. Silencio
tención **`lower_bound` / `bisect`** encontrar el primer elemento ≥ target. TEN **Búsqueda binaria plegable** dentro de un lazo es más difícil de depurar. TEN **La profundidad de la recursión** puede soplar si el árbol es picado – mejor para hacer traversal iterante. Silencio

-...

## 3down Algoritm

1. **Atravesar el orden BST** → `Vals surtidos`.
2. Por cada `q ' en las ' demandas ' :
* `idx = lower_bound(sorted Vals, q)`
* `maxi = (idx < n) ? ordenadosVals[idx] : -1`
* `mini = (idx 0) ? sortVals[idx-1] : -1`
* Si `idx ' se realizó n` y `sortedVals[idx] == q` → tanto `mini ' como `maxi` = `q`.
3. Apéndice `[mini, maxi]` al resultado.

-...

## 4VIEW⃣ Complexity Analysis

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencio In‐order traversal Silencio **O(n)** Silencio **O(n)** (sorted array)
Silencio Cada consulta (búsqueda binaria) Silencio **O(log n)** Silencio – Silencio
Silencio total **O(n + m log n)** Silencio **O(n)**

* `n` = número de nodos de árboles (≤ 105)
* `m` = número de consultas (≤ 105)

Tanto el tiempo como la memoria encajan fácilmente dentro de los límites de LeetCode.

-...

## 5down Implementaciones de referencia

## 5.1 Java (Using `ArrayList` + Binary Search)

``java
importar java.util*;

// Definición para un nodo de árbol binario.
clase TreeNode
int val;
TreeNode izquierda, derecha;
TreeNode(int x) { val = x; }
TreeNode(int x, TreeNode l, TreeNode r) { val = x; left = l; right = r; }
}

Clase Solución {
// Construir la matriz ordenada a través de traversal en orden
inorden de vacío privado(TreeNode node, Lista de instrucciones) {
si (nodo == nulo) regresa;
inorder(node.left, list);
list.add(node.val);
inorder(node.right, list);
}

public List made más cercanaNodos(TreeNode root, Listo) {}
Lista realizadaInteger título clasificado = nuevo ArrayList implicado();
inorder(root, ordered);

Lista realizadaLista realizadaInteger título ans = nuevo ArrayList recomendado();
int n = sort.size();

para (int q : consultas) {
int lo = 0, hola = n; // hola es exclusiva
mientras (lo  hi hola) { // búsqueda binaria
int mid = lo + (hi - lo) / 2;
si (sorted.get(mid) < q) lo = mid + 1;
más hola = medio;
}
// lo es el primer índice con valor >= q (o n)
int maxi = (lo iere n) ? sort.get(lo) : -1;
int mini = (lo ≤ 0) ? sort.get(lo - 1) : -1;

si (lo ecto n " cl.get(lo) == q) { // exacta partido
mini = maxi = q;
}
ans.add (Arrays.asList(mini, maxi));
}
devolver los ans;
}
}
`` `

■ *Por qué funciona* *
■ *En orden* da una lista ascendente estrictamente porque la entrada es un BST.
> `lo` se convierte en el límite más bajo ** - el índice más pequeño con `valor ≥ q`.
■ Los casos de borde ( " lo==n " , " lo==0 " ) se manejan mediante la comprobación de límites.

-...

## 5.2 Python (Using `bisect`)

``python
de la importación de bisect_left
de la importación List, Optional

Definición para un nodo de árbol binario.
Clase TreeNode:
def __init__(self, val:int=0, left:'TreeNode'=None, right:'TreeNode'=None):
self.val = val
autoizquierda
self.right = right

Solución de clase:
def _inorder(self, node: Optional[TreeNode], arr: List[int]) - título Ninguno.
si no no nodo: retorno
self._inorder(node.left, arr)
arr.append(node.val)
self._inorder(node.right, arr)

def más cercanoNodes(self, root: TreeNode, consultas: List[int] - título List[List[int]]:
sort_vals = []
auto._inorden(root, sort_vals)
n = len(sorted_vals)
res = []

para q en consultas:
idx = bisect_left(sorted_vals, q) # first ю= q
maxi = sort_vals[idx] si idx
mini = sort_vals[idx-1] si idx Ø 0 más -1

si idx se hizo n y clasifica_vals[idx] == q: # exacta coincidencia
mini = maxi = q
re.append([mini, maxi])
retorno
`` `

> `bisect_left` implementa la misma lógica que la búsqueda binaria de Java pero en una línea única.

-...

### 5.3 C++ (Usando `vector` + `lower_bound`)

``cpp
#include יbits/stdc++.h
usando std namespace;

// Definición para un nodo de árbol binario.
struct TreeNode {
int val;
TreeNode *left, *right;
TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

Clase Solución {
order de vacío(TreeNode* nodo, vector identificadoint
si (!node) regresa;
inorder(node-propleft, v);
v.push_back(node-ciendoval);
inorder(node- correctamente, v);
}
public:
vector node* root, vector identificadoint confianza consultas) {
vector asignadoint título clasificado;
inorder(root, ordered);
int n = sort.size();
vector realizador:

para (int q : consultas) {
auto = inferior_bound(sorted.begin(), sort.end(), q); // first ≤
int idx = it - sort.begin();

int maxi = (it != classified.end()) ? *it : -1;
int mini = (idx > [idx-1] : -1;

if (it != classified.end() " Unidos == q) { // exact match
mini = maxi = q;
}
ans.push_back({mini, maxi});
}
devolver los ans;
}
};
`` `

Es la contraparte STL de `bisect_left`.
■ El código es *iterative* y seguro para árboles muy profundos.

-...

## 6down Ed Edge‐ Lista de verificación de casos

← Situación Silencio esperada Resultado
Silencio...
Silencio No elemento ≤ query  **‐1** ← Olvidar `idx == Mira. Silencio
Silencio Ningún elemento ≥ query Silencio **‐1** Silencio Utilizando incorrectamente `upper_bound`. Silencio
Silencio Query es igual a un valor de nodo Silencio `[q, q]` Silencio Dejar al predecesor sin cambios → incorrecto. Silencio
Silencio Árbol escarpado (degenerado) Silencio Todavía O(n) memoria ¦ Recursive traversal puede desbordar la pila – preferir iterante. Silencio
← Valores duplicados no permitidos en BST TENIDO Strictly ascending list TEN `lower_bound` todavía funciona; duplicados romperían la suposición. Silencio

-...

Consejos de entrevista

✔ Tema Tema de la vida Lo que el entrevistador se preocupa por ¦
Silencio...
Silencioso **BST fundamentals** ¿Sabes cómo un traversal en orden produce una lista ordenada? ← Dibujar un pequeño BST en papel, caminar a través del orden. Silencio
Silencio **Binary search** Silencio ¿Puede encontrar el sucesor del predecesor en el tiempo logarítmico? Silencio Aplicar `bisect_left` o `lower_bound` desde cero, a continuación, optimizar. Silencio
Silencio ** Optimización del espacio** Silencio ¿Te das cuenta de almacenar el árbol de nuevo (por ejemplo, con `TreeSet`) es desperdicio? Silencio Explicar el intercambio entre un `TreeSet` (inserción/búsqueda por tiempo fijo) vs un único array clasificado. Silencio
Silencio **Edge-case handling** Silencio ¿Devuelves **‐1** correctamente? Silencio Mostrar casos de prueba donde la consulta es más pequeña que todos los nodos o más grande que todos los nodos. Silencio
TEN **Iterative vs recursive** TEN ¿Tu solución maneja los árboles escarpados? Silencio Usa una pila o traversal iterativa si anticipas una altura de 105. Silencio

■ **Recuerde**: Las pruebas de LeetCode generalmente generan un árbol aleatorio, por lo que la profundidad de recursión puede alcanzar el límite de pila predeterminado en Java/Python. Un en orden no recursivo (utilizando una pila explícita) garantiza la estabilidad.

-...

## 8down⃣ FAQ (ficha de infidelidad)

Silencio
Silencio...
Silencio **¿Puedo usar `TreeSet` en lugar de una matriz ordenada?** Silencio Sí, pero todavía necesitarías llamar `lowerBound`/`ceil` para cada consulta – el tiempo es el mismo, pero la memoria es más alta. Silencio
Silencio **¿Es necesario 'upper_bound'?** Silencio No, `lower_bound` + `idx-1` basta para predecesor y sucesor. Silencio
Silencio **¿Qué pasa si el árbol contiene valores duplicados?** Silencio El problema garantiza un * árbol de búsqueda binario*, que por definición tiene valores distintos; de lo contrario la respuesta sería ambigua. Silencio
Silencio **¿Puedo hacer esto en tiempo O(n + m)?** Silencio Sólo si usted realiza un solo *parallel* traversal del árbol y las consultas (línea de barrido avanzada). No es necesario para 105 restricciones. Silencio
Silencio **¿Cómo construir el árbol de un array?** Silencio Utilice el ayudante habitual de LeetCode que inserta los nodos de nivel por nivel. No es parte de la lógica central. Silencio

-...

## 9️ Take‐away for the Job Interview

1. **Mostrar su comprensión de la estructura de datos** – explicar por qué en orden da una lista ordenada.
2. **Hablar de la complejidad** – “Hacemos un único traversal (O(n)), entonces cada consulta utiliza la búsqueda binaria (O(log n)). ”
3. ** Periferias de mención** – “Si el límite inferior está al principio o al final, volvemos ‐1.”
4. **Si se pide una solución más “dinámica”** – sugerir el uso de “TreeSet” o un BST equilibrado que apoye el “floor()” y el “ceiling()” en O(log n).

■ *Por qué esto te hace destacar*
■ Muestra *la capacidad de reducir una solución ingenua O(n · m) a una rápida O(n + m log n)* – un sello distintivo de un ingeniero experimentado.

-...

## 📚 Final Code Snapshot

``bash
# Java
Java -leetcode. frasco
# Python
solución python3. py
# C++
g++ -std=c+17 solution.cpp "
`` `

Los tres snippets arriba están listos para copiar-paste en el editor de LeetCode y pasar las pruebas proporcionadas.

-...

### ## ritmo Happy Coding!
Si te gustó este paseo, pulsa **👍** y **Suscribir** para más LeetCode deep‐dives – perfecto para tu próximo prep de entrevista. 🚀