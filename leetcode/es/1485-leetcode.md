-...
Título: LeetCode 1485. Árbol binario de clon con puntero aleatorio -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## Árbol binario de clon con puntero aleatorio
**LeetCode 1485 – Medium**

Silencio Idioma Silencio Código Silencio
Silencio...
Silencio **Java** Silenciosos [Ver código] (#java-code)
Silencio **Python** Silencio [Ver código] (#python-code) Silencio
Silencio **C+** Silencioso [Ver código](#cpp-code)

■ **SEO Palabras clave**: Clone Binary Tree Con Random Pointer, LeetCode 1485, copia de fondo de árbol binario, clon de puntero aleatorio, solución Java DFS, solución Python DFS, solución C++ DFS, entrevista de estructura de datos, desafío de codificación de entrevistas, problemas de codificación de entrevistas de trabajo.

-...

## 1. Resumen del problema

Se le da un árbol binario donde cada nodo contiene un puntero extra llamado `Aleatorio`.
"El azar" puede apuntar a cualquier nodo en el árbol (incluido él mismo) o ser "null".
Su tarea es crear una copia **deep** del árbol entero – es decir, cada nodo y cada uno
" la referencia aleatoria debe apuntar a un nuevo nodo que tenga el mismo valor.

El formato de entrada y salida sigue la serialización habitual de árbol binario LeetCode:
`[valor, random_index]` – `random_index` es la posición del nodo en el array
(o `null` si no hay puntero al azar).

■ **Constraints**
Número de nodos ≤ 1000
1 ≤ Nodo.val ≤ 106

-...

## 2. Core Idea – Dos– Paso DFS con un HashMap

1. **Primero Paso** – Cierra cada nodo (ignorando el enlace del `aleatorio') y almacena un
mapeo del nodo original a su clon.
2. **Paso segundo** – Traver el árbol original de nuevo; para cada nodo, establecer el
clone ' s `izquierda ' , `derecha ' , y `aleatoria ' campos buscando el correspondiente
objetos clonados en el mapa.

Porque cada nodo es visitado dos veces y utilizamos un mapa de hash para resolver punteros,
el algoritmo funciona en **O(N)** tiempo y **O(N)** espacio auxiliar.

El enfoque de dos pasos mantiene el código directo y evita complejo
Gimnasia puntero que un clon de un paso en lugar requeriría.

-...

## 3. Aplicación del Código

■ **Nota**: En los tres fragmentos el tipo de nodo *clone* es el mismo que el
" Original " . La interfaz de LeetCode `Solution` espera la misma clase
Ø para entrada y salida.

### ##  se hizo un nombre="java-code"]

``java
*
* Definición para un Nodo.
* Public class Node {}
* int val;
* Nodo izquierdo;
* Nodo right;
* Nodo aleatorio;
* Node() {}
* Node(int val) { this.val = val; }
* Node(int val, Nodo izquierdo, Nodo derecho, Nodo aleatorio) {}
* this.val = val;
* this.left = left;
* this.right = right;
* this.random = random;
*
*
*/
Clase Solución {
// Mapa original node - confianza nodo clonado
mapa final privado nodo, Node relativo mapa = nuevo HashMap fiel();

public Node clone Árbol(Raíz del nodo) {
si (root == null) vuelve nula;

// Primer paso: nodos clonados (sin niños todavía)
cloneNodes(root);

// Segundo paso: izquierdo, derecho, azar
setPointers(root);

return map.get(root);
}

// Recursive DFS que clona cada nodo una vez
clon privado vacíoNodos(nodo nodo) {
si (nodo == null TENIDO mapa.containsKey(node))) regresa;
map.put(node, new Node(node.val));
cloneNodes(node.left);
cloneNodes(node.right);
cloneNodes(node.random);
}

// Recursive DFS que conecta a niños " punteros aleatorios
set de vacío privadoPointers(Nodo nodo) {
si (nodo == nulo) regresa;
Node copy = map.get(node);
copy.left = map.get(node.left);
copy.right = map.get(node.right);
copy.random = map.get(node.random);
setPointers(node.left);
setPointers(node.right);
setPointers(node.random);
}
}
`` `

### ## ## #1 se hizo un nombre="python-code" Python – DFS con Diccionario

``python
Definición para un Nodo.
Clase Nodo:
def __init__(self, val=0, left=None, right=None, random=None):
self.val = val
autoizquierda
self.right = right
aleatorio

Solución de clase:
def clone Tree(self, root: 'Node') - título 'Node':
si no raíz:
No.

automapping = {}
self._first_pass(root)
self._second_pass(root)
Vuélvete. mapping[root]

def _first_pass(self, node):
si no no es un nodo o un nodo en sí mismo. mapeo:
Regreso
self.mapping[node] = Node(node.val)
auto._first_pass(node.left)
self._first_pass(node.right)
self._first_pass(node.random)

def _second_pass(self, node):
si no el nodo:
Regreso
clone = self.mapping[node]
clone.left = self.mapping.get(node.left)
clone.right = self.mapping.get(node.right)
clone.random = self.mapping.get(node.random)
auto._second_pass(node.left)
self._second_pass(node.right)
self._second_pass(node.random)
`` `

### ## Identificar un nombre="cpp-code"(s)

``cpp
*
* Definición para un Nodo.
* struct Node {}
* int val;
* Nodo *izquierda;
* Node *right;
* Nodo *saría;
* Nodo() : val(0), left(nullptr), right(nullptr), random(nullptr) {}
* Nodo(int _val) : val(_val), left(nullptr), right(nullptr), random(nullptr) {}
* Nodo(int _val, Nodo* _left, Nodo* _right, Nodo* _random)
* : val(_val), left(_left), right(_right), random(_random) {}
* };
*/
Clase Solución {
public:
Node* cloneTree(Node* root) {
si (!root) regresa nullptr;
unordered_map madeNode*, Node*
firstPass(root, mp);
secondPass(root, mp);
devolver mp[root];
}

privado:
vacío primero Paso(Nodo* nodo, unordered_map Node*, Node* Confundir mp) {
si (!node ¦
mp[nodo] = nuevo Node(node-conval);
firstPass(node- Confleft, mp);
firstPass(node- Confright, mp);
firstPass(node- Confrandom, mp);
}

vacio segundoPass(Nodo* nodo, unordered_map interpretadoNodo*, Node*Conducir mp) {
si (!node) regresa;
Node* clone = mp[node];
clone- confíaleft = mp.count(node- títuloleft) ? mp[node- confíaleft] : nullptr;
clone- título = mp.count(node- títuloright) ? mp[node- tituladoright] : nullptr;
clone- títulorandom = mp.count(node- títulorandom) ? mp[node- Confrandom] : nullptr;
secondPass(node- Confleft, mp);
secondPass(node- Confright, mp);
secondPass(node- Confrandom, mp);
}
};
`` `

-...

## 4. Análisis de la complejidad

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencio Primero DFS Silencio **O(N)** Silencio **O(N)** (hash map)
Silencio Segundo DFS Silencio **O(N)** Silencio **O(N)** (hash map)
Silencio **Total** Silencio**

`N` es el número de nodos en el árbol.
La profundidad de la recursión está atada por la altura del árbol (≤ N).

-...

## 5. Discusión - El Bien, el Mal, y el Ugly

Silencio Silencio
Silencio------------Prince------
Silencio **Claridad** tención Dos pasos DFS es directo a la razón. TEN Recursion puede causar apilamiento de sobreflujo en árboles muy profundos. ← Las soluciones de un paso en lugar único (los clones en el árbol original) son difíciles de depurar. Silencio
Silencio ** Memoria** Silencio O(N) mapa es aceptable para 1 000 nodos. ← Requiere espacio adicional más allá del nuevo árbol. Silencio Usar `unordered_map` en C++ puede llevar a alta sobrecarga si se producen muchas colisiones precipitadas. Silencio
Silencio **Performance** Silencio Únicamente un campo extra para establecer por nodo. Dos traversales duplican el factor constante. La manipulación compleja puntero puede introducir errores sutiles al restaurar el árbol original. Silencio
Silencio **Extensibilidad** Silencio Trabaja para cualquier estructura similar a los árboles con enlaces aleatorios. No maneja ciclos que no están cubiertos por el puntero aleatorio (no un árbol). Silencio El algoritmo no asume ciclos que no sean a través de la `saría`; de lo contrario necesitaría detección de ciclos. Silencio
Silencio ** Casos de Edge** ← Handles `null`, auto-referencia de punteros aleatorios, y apuntando a cualquier profundidad. Silencio Ninguno. Silencio Si la clase de nodos contiene campos adicionales (por ejemplo, punteros padres), deben ser manejados explícitamente. Silencio

-...

## 6. SEO‐Friendly Blog Article

■ *Título*
■ *Master LeetCode 1485: Clone Binary Tree Con Random Pointer – Java, Python, C++ Soluciones para su entrevista*

-...

### 6.1 Why This Problem Rocks Your Interview

LeetCode *Clone Binary Tree Con Random Pointer* (1485) es una entrevista clásica
problema porque combina dos queridos conceptos de estructura de datos:

1. **Traversal de árboles interiores** (DFS/BFS)
2. **Copia profunda del puntero del rayo** – una trampa oculta que puede hacer incluso sazonado
Los desarrolladores tropiezan.

Aparece en muchos repositorios de coding-interview, y los gerentes de contratación les encanta
utilizarlo porque prueba:

- Tu habilidad para pensar recursivamente
- Tu habilidad con tablas de hash (Map, `dict`, `unordered_map`)
- Tu comprensión de la semántica puntero

-...

### 6.2 ¿Por qué utilizamos un HashMap (o un mapa desordenado)

El puntero aleatorio es **no** parte de la estructura natural del árbol.
Cuando clonas un nodo, necesitas saber *que* nodo clonado corresponde al
blanco original.
Un mapa de hash le da **O(1)** tiempo de búsqueda y garantiza que cada original
mapas de nodos a un clon único.

-...

### 6.3 Step‐by‐Step Java Ejemplo

``java
público Node cloneTree(Node root) {
si (root == null) vuelve nula;
Mapa seleccionadoNodo, Node relativo mapa = nuevo HashMap fiel();
cloneNodes(root, mapa); // 1st pass
setPointers(root, mapa); // 2nd pass
return map.get(root);
}
`` `

*Primero pase* simplemente hace `map.put(node, new Node(node.val)).
*Segundo pase* alambres `izquierda ' , `derecha ' y `aleatoria ' vía `map.get(...)`.

-...

### 6.4 Enfoques alternativos que podrías ver

Silencio Silencio Silencio Pros
Silencio...
Silencio **Iterative BFS** Silencio Evita la recursión ¦ Ligeramente más código; todavía necesita una cola
Silencio **One‐pass In‐place Clone** Silencio No extra hash map Silencio Muy difícil; alto riesgo de errores Silencio
Silencio **Using Parent Pointers** Silencio A veces reduce el espacio extra Silencio No está disponible en la descripción del problema

El DFS de dos pasos es *generalmente* el enfoque recomendado para la codificación de entrevistas.

-...

### 6.5 Cómo prepararse para preguntas de entrevista similar

1. **Práctica con punteros aleatorios**
LeetCode *Copy List con Random Pointer* (versión de lista conectada) es un
Gran calentamiento.

2. **Master DFS " BFS Plantillas* *
Mantenga una plantilla reutilizable de nodo “clone con mapeo” en su cuaderno.

3. ** Casos de borde superior* *
Árbol vacío, nodo único con `alea` apuntando a sí mismo, árboles muy profundos.

4. **Tiempo de operaciones espaciales**
Prepárate para explicar por qué eligió una solución particular y cuál es su
los intercambios son.

5. **Preguntas de aclaración**
En una entrevista en vivo, confirme si se le permite utilizar memoria extra,
si el árbol puede contener ciclos a través del `arredón', etc.

-...

## 6.6 Wrap‐Up

- **Problema**: Copia profunda un árbol binario con un puntero arbitrario.
- **Solución**: Dos pasos DFS + mapa de hash (DFS, Python dict, C++ unordered_map).
- **Complejidad**: O(N) time, O(N) space.

Ya sea que se está cepillando para una entrevista de instrucciones de datos, preparándose para una
papel de ingeniería de software, o simplemente amor LeetCode desafíos, dominando este
problema te dará confianza en manejar punteros, recursión y hash
tablas – habilidades que son ** altamente buscadas** por empresas de tecnología superior.

¡Feliz codificación! 🚀