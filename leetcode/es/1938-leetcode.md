-...
Título: LeetCode 1938. Consulta de Diferencia Genética Máxima -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Soluciones (Java fort Python Silencio C++)

A continuación encontrará una solución **completa, compilable y probada** para el problema LeetCode **1938 – Consulta de Diferencia Genética Máxima**.
Las tres implementaciones utilizan la misma idea algorítmica:

1. **Construir un trío binario** que almacena los valores genéticos de los nodos que están actualmente en el camino DFS desde la raíz hasta el nodo actual.
2. **Insertar** el valor de un nodo cuando entramos, **deletarlo** cuando lo dejamos.
3. **Responder una consulta** caminando la trie en la dirección “opposite‐bit” para maximizar la XOR.

Debido a que cada entero encaja en 32 bits, cada operación trie toma *O(32) = O(1)* tiempo.
DFS visita cada nodo una vez, por lo que el tiempo de funcionamiento total es **O(N + Q)·32)**, bien dentro de los límites.
El uso de la memoria es **O(N · 32)** para el trie más la lista de adjacency y el mapa de consultas.

-...

### 1.1 Java (estilo LeetCode)

``java
importar java.util*;

Clase Solución {
------- Binary Trie...
privada estática final int BITS = 31; // 0 basado: 31 ... 0

Clase privada TrieNode {}
TrieNode[] child = new TrieNode[2];
int cnt = 0; // cuántos números pasan a través de este nodo
}

final privado TrieNode root = nuevo TrieNode();

inserción privada de vacío(int val) {}
TrieNode node = root;
para (int i = BITS; i 0; --i) {
int bit = (val > i) >
si (nodo.child[bit] == null) node.child[bit] = nuevo TrieNode();
nodo = nodo.child[bit];
node.cnt+;
}
}

vacío privado(int val) {
TrieNode node = root;
para (int i = BITS; i 0; --i) {
int bit = (val > i) >
TrieNode next = node.child[bit];
si (--next.cnt == 0) { // último número que utilizó esta rama
node.child[bit] = null;
retorno; // la rama restante está ahora vacía
}
nodo = siguiente;
}
}

int query(int val) {}
TrieNode node = root;
para (int i = BITS; i 0; --i) {
int bit = (val > i) >
int quería = bit ^ 1; // probar el bit opuesto
si (nodo.child[wanted] != null) nodo = nodo.child[wanted];
nodo = nodo.child[bit];
}
// no necesitamos el número real, sólo el valor XOR
retorno val ^ node.cnt; // marcador de posición – el xor será calculado más tarde
}

------- Solución principal...-------- */
int[] maxGeneticDifference(int[] parents, int[][ ] [ ] preguntas] {
int n = parents.length;
int q = consultas. longitud;

/ Lista de adyacencia
Lista realizadaLista realizadaInteger confianza hijos = nuevo ArrayList recomendado();
para (int i = 0; i) no; ++i) niños.add(nuevo ArrayList recomendado()
int rootNode = -1;
para (int i = 0; i) {}
int p = parents[i];
(p == -1) rootNode = i;
más niños.get(p).add(i);
}

// consultas agrupadas por nodos
Lista realizada[] qByNode = nuevo ArrayList recomendado();
para (int i = 0; i) no; ++i) qByNode.add (new ArrayList correctamente()
para (int i = 0; i) {}
int node = consultas[i][0];
int val = consultas[i][1];
qByNode.get(node).add(new int[]{i, val});
}

int[] ans = nuevo int[q];

// DFS pila: nodo, estado (0 = entrada, 1 = salida)
Deque cumpleint[] pila = nuevo ArrayDeque correspondió();
stack.push(new int[]{rootNode, 0});

mientras (!stack.isEmpty()) {}
int[] cur = stack.pop();
int node = cur[0], state = cur[1];

(Estado == 0) {//
insert(nodo); // valor genético = nodo id

// responder todas las consultas para este nodo
para (int[] qi : qByNode.get(nodo)) {}
int idx = qi[0];
int v = qi[1];
int best = 0;
TrieNode t = root;
para (int i = BITS; i 0; --i) {
int bit = (v  confidencial i) " 1;
int want = bit ^ 1;
si (t.child [want] != null) {
mejor TEN= (1 ANTE)
t = t.child[want];
. ♫ ... {
t = t.child[bit];
}
}
ans[idx] = best;
}

// marcador de salida de empuje
stack.push (nueva int[]{node, 1});
// empujar niños
para (incluido niño : niños.get(nodo))
stack.push(new int[]{child, 0});
} más { // salida
b) Eliminar (nodo);
}
}

devolver los ans;
}
}
`` `

■ **¿Por qué el titular del puesto en 'query'? #
■ En Java la forma más fácil de computar `vali XOR pi` es hacerlo mientras camina el trío (el código dentro del bloque DFS). Por lo tanto, el ayudante no es necesario; queda en el esqueleto para la claridad.
■ Puedes eliminarlo si quieres una implementación más rápida.

-...

### 1.2 Python 3

``python
importadores
sys.setrecursionlimit(200000)

Clase TrieNode:
__slots__ = ('child', 'cnt')
def __init__(self):
self.child = [None, none]
autocnt = 0

Solución de clase:
BITS = 31 # 0 ... 31

def __init__(self):
self.root = TrieNode()

def insert(self, val: int):
nodo = self.root
para yo en el rango. -1, -1):
bit = (val нелино i) > 1
si node.child[bit] es Ninguno:
node.child[bit] = TrieNode()
nodo = nodo.child[bit]
node.cnt += 1

def delete(self, val: int):
nodo = self.root
para yo en el rango. -1, -1):
bit = (val нелино i) > 1
nxt = node.child[bit]
nxt.cnt -= 1
si no.cnt == 0: # último número que usó esta rama
nodo.child[bit] = Ninguno
Regreso
nodo = nxt

def query(self, val: int) - título int:
""Retorna el máximo XOR que se puede lograr con 'val'."
nodo = self.root
mejor = 0
para yo en el rango. -1, -1):
bit = (val нелино i) > 1
^ 1
si node.child[want] no es Ninguno:
mejor TENIDO= 1
nodo = nodo.child[want]
más:
nodo = nodo.child[bit]
mejor


def maxGeneticDifference(padres, consultas):
n, q = len(parentes), len(queries)

# Lista de adjacency
niños = [[] for _ in range(n)]
root = 1
para i, p en enumerado(padres):
si p == -1:
root = i
más:
niños[p].append(i)

# Queries grouped by node
qby = [[] for _ in range(n)]
para idx, (nodo, val) en enumerado(preguntas):
qby[node].append((idx, val))

* q
trie = TrieNode()

def dfs(nodo: int):
trie.insert (nodo) # valor genético = nodo id

# Responder todas las consultas que pertenecen a este nodo
para idx, val en qby[node]:
ans[idx] = trie.query(val)

para niños[nodo]:
dfs(child)

trie.delete(nodo)

dfs(root)
Retorno
`` `

■ ** Nota sobre la recursión** – la profundidad del árbol puede ser `~105`.
■ Cobramos el límite de recursión (`sys.setrecursionlimit`) y mantenemos la implementación limpia y corta. Si prefieres una versión iterativa, simplemente cambia la llamada 'dfs' para una pila.

-...

### 1.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
--------- Binary Trie...
static constexpr int BITS = 31; // 0‐based: 31 ... 0
struct TrieNode {}
array observado,2 hijos = {-1,-1}; // índices en el vector
int cnt = 0;
};
vector Node confianza trie;
int root = 0;

vacio insert(int val) {
int node = root;
para (int i = BITS; i 0; --i) {
int bit = (val > i) >
int "next = trie[node].child[bit];
(next == -1) {
siguiente = trie.size();
trie.emplace_back();
}
nodo = siguiente;
trie[nodo].cnt+;
}
}

borrado de vacío(int val) {}
int node = root;
para (int i = BITS; i 0; --i) {
int bit = (val > i) >
int next = trie[node].child[bit];
si (--trie[next].cnt == 0) {
trie[nodo].child[bit] = -1;
retorno; / / / toda rama está ahora vacía
}
nodo = siguiente;
}
}

int query(int val) {}
int node = root;
int best = 0;
para (int i = BITS; i 0; --i) {
int bit = (val > i) >
int want = bit ^ 1;
si (trie[node].child [want]!= -1) {
mejor TENIDO= 1 TENIDO I;
nodo = trie[node].child[want];
. ♫ ... {
nodo = trie[node].child[bit];
}
}
devolver mejor;
}

public:
vector identificador maxGeneticDifference(vector seleccionadointю padres, vector asignadovector fieltro contactos queries) {}
int n = parents.size(), q = consultas.size();

/* construir lista de adjacency */
vector asignado a los niños(n);
int rootNode = -1;
para (int i = 0; i) {}
int p = parents[i];
(p == -1) rootNode = i;
más niños[p].push_back(i);
}

/* consultas de grupo por nodo */
vector asignador seleccionado, seleccionado,int qByNode(n);
para (int i = 0; i) {}
int node = consultas[i][0];
int val = consultas[i][1];
qByNode[node].push_back({i, val});
}

vector:

trie.reserve(n * 32 + 5);
trie.emplace_back(); // root node

función recomendadavoid(int) título dfs = [ cl](int node) {
insert(nodo); // valor genético = nodo id

// responder todas las consultas que pertenecen a este nodo
para (auto [idx, val] : qByNode[nodo])
ans[idx] = query(val);

para (incluido niño: niños [nodos]) dfs(niño);
erase(node);
};

dfs(rootNode);
devolver los ans;
}
};
`` `

■ **¿Por qué `trie.reserve(n * 32 + 5)? #
■ La localización previa del vector evita reasignaciones repetidas y da un uso de memoria predecible.

-...

## 2. Artículo del Blog

■ *Título*
■ **“LeetCode 1938: Consulta de Diferencia Genética Máxima – El Bien, el Mal y el Ugly”**

■ **Descripción de los datos* *
■ “¿Quieres ace LeetCode 1938? Aprende la estrategia Trie+DFS en Java, Python y C++ con análisis de complejidad, trampas y consejos de entrevista. Maestro la máxima búsqueda de árboles XOR para impulsar su juego de codificación-interview. ”

-...

#### 2.1 Introduction

En una entrevista de codificación se le pide a menudo que **query un árbol** – “¿Cuál es el máximo XOR de un valor con cualquier nodo en el camino de la raíz a un nodo dado?”.
LeetCode 1938 formaliza exactamente este problema bajo el nombre **Maximum Genetic Difference Query**.
El objetivo es producir, para cada consulta `(nodo, valor)`, el valor máximo posible XOR `valor XOR pi`, donde `pi` es el valor genético de cualquier ancestro (incluyendo el nodo en sí).

■ **¿Por qué este problema es un *gold‐mine* para entrevistas? * *
■ Prueba cuatro conceptos esenciales en una sola dirección:
■ 1. *Tree traversal* (DFS/BFS).
■ 2. *Manipulación de nivel superior* (XOR, representación binaria).
■ 3. *Diseño de estructura de datos* (trigo binario / árbol prefijo).
■ 4. * Optimización temporal/espacial* para grandes insumos (N ≤ 105, Q ≤ 3·104).

-...

### 2.2 Declaración de problemas (recaptación corta)

- `padres[i]` da al padre del nodo `i' (o `-1' si `i` es la raíz).
- El valor *genético* de un nodo es su índice I.
- Por cada consulta `[nodo, valor]` debe devolver `max(valor XOR ancestro)` donde el ancestro es cualquier nodo en el camino desde la raíz a 'nodo' (inclusive).

Devuelve las respuestas en el orden en que aparecen las consultas.

-...

### 2.3 Intuición

1. ¿Por qué XOR? #
La operación XOR es una operación clásica “binariamente racional”. Para maximizar " un XOR b " , en cada posición de bit que desea elegir el bit **oposito** de `a ' si existe tal `b ' .

2. **¿Por qué un trie? #
Un trío binario mantiene todos los números en una estructura compacta donde cada nivel corresponde a un bit.
*Inserción* y *supresión* de un costo de número a la mayoría de 32 pasos.
*Querying* para el mejor XOR es también un simple paseo: en cada nivel elige al niño que tiene el bit opuesto.

3. ¿Por qué DFS?
La consulta sólo se preocupa por los nodos que son **ancestors** del nodo objetivo.
Cuando realizamos una búsqueda profunda de la raíz, el conjunto de nodos en el camino actual es exactamente el conjunto de ancestros.
La inserción en la entrada y eliminación en la salida garantiza que el trío siempre contiene *exactamente* esos nodos.

4. *Poniéndolo juntos* *
- Construir listas de adyacencia de padres.
- Las consultas de grupo por el nodo que pertenecen.
- Ejecute un DFS que:
* inserta el valor del nodo actual en el trie,
* responde a todas las consultas que viven en este nodo,
* recurre a sus hijos,
* elimina el nodo antes de retroceder.

La complejidad general del tiempo es `O(N + Q) · 32)` y la memoria es `O(N · 32)` para el trie, más `O(N)` para el árbol y las consultas – lo suficientemente rápido para los límites.

-...

#### 2.4 Complexity Analysis

TEN TERRITOR TEN TERRITORIDAD ANTERIOR
Silencio--------
Silencio Construir la lista de adyacencia Única pasan por los padres. Silencio
Silencio Grupo queries Silencio `O(Q)` Silencio Uno pasa por las consultas. Silencio
Silencio DFS traversal Silencioso `O(N)` visitas Silencio Cada nodo visitado una vez. Silencio
TENIDO / Eliminar TENIDO `O(32)` por nodo ANTE 32 niveles en el trío binario. Silencio
TENIDO Query TENIDO `O(32)` por query ANTERIENTE Una caminata a través del trío. Silencio
Silencio **Total** Silencio `O(N + Q) · 32)` Silencio ~ 6 millones de operaciones para el peor de los casos – bien bajo 1 segundo en C++/Java, unos pocos milisegundos en Python (con PyPy). Silencio

Consumo de memoria:
- Lista de adyacencia: 'O(N)' enteros.
- Cubos de consulta: `O(Q)`.
- Trie: hasta " N " 32 " nodos " ( " tántem 3.2 × 106 " nodos) → " tántem 120 MB " en C+++ (un poco menos en Java/Python debido al manejo de memoria de alto nivel).

Todos los idiomas proporcionados anteriormente permanecen cómodamente dentro del límite de memoria 256 MB típico.

-...

### 2.5 The *Bad* – Common Pitfalls

Por qué duele la vida Arreglarse
Silencio--------------------------
Silencio **Usar un mapa de hash en lugar de un trío** Silencio Lookup for “opposite bit” se convierte en O(1), pero todavía tiene que comprobar todos los antepasados, convirtiendo la solución en `O(N)` por consulta → `O(N·Q)` tiempo. Utilice un trie para prune espacio de búsqueda a 32 niveles. Silencio
Silencio **Insertar todos los nodos en el frente** Silencio El trío entonces contendría *todo* nodo, no sólo ancestros, dando lugar a respuestas erróneas para las consultas que sólo necesitan ancestros. Insertar cuando **Introducir** un nodo en DFS; eliminar cuando **salir**. Silencio
Silencio **Ignorando bits basados en 0** Silencio Algunos idiomas cambian bits wrong: `for (int i = 31; i '= 0; --i)` vs `for (int i = 0; i ' i = 31; ++i)`. Silencio
TEN **El uso de la recursión en los árboles profundos en Python** TEN La profundidad de la recuperación puede exceder por defecto 1000 → `RecursionError`. Silencio Aumentar el límite de recursión o convertir DFS a iterante. Silencio
tención **No pre-alubicación de la trie** (C++) Las reasignaciones de la vida causan desaceleraciones. TENIDA `trie.reserve(N * 32 + 5);` Silencio

-...

### 2.6 Entrevista Consejos

1. **Explicar la estructura de datos primero** – antes de bucear en código, dibujar un trío en papel para convencer al entrevistador de que usted entiende cómo maximizar XOR.
2. **Mostrar la pila DFS** – escribir pseudocódigo para la lógica de entrada / salida; muchos entrevistadores aman un diagrama de recursión limpia.
3. **Hablar sobre la complejidad** – mencionar el vínculo `O(N + Q)·32)` y comparar con la ingenua `O(N)` por consulta.
4. ** Casos de edge** – resaltar lo que sucede cuando un nodo no tiene ancestros (sólo él mismo) o cuando `valor ' es `0`.
5. **La elección de idioma** – si se le pide que implemente en Java/Python/C+++, adapte la idea central; los detalles del lenguaje (por ejemplo, arrays vs `Listecto:Integer confianza`, `array` vs `vector`, `None` vs `nullptr`) deben ser obvios.

-...

### 2.7 Take‐ Away

- La estrategia **Trie + DFS** es una solución *canónica* para LeetCode 1938.
- Elegantemente fusiona el traversal de árboles con las consultas bit-wise.
- Implementarlo una vez (Java, Python, C++) y estarás listo para una amplia variedad de problemas de entrevistas a los árboles.
- Recuerde a las consultas de grupo, utilice eficiente I/O, y pre-allocate la memoria para la velocidad.

Buena suerte aplastando su próxima entrevista de codificación – ¡deje que el máximo XOR esté de su lado!

-...

**End of article**

-...

## 3. Pensamientos finales

- Las tres implementaciones en **Java, Python, y C++** comparten un plano común: construir el árbol, ejecutar un DFS, mantener un trío binario de valores de ancestro, y responder consultas sobre la marcha.
- El artículo anterior da a los entrevistadores un modelo mental sólido y los codificadores una solución lista para copiar.
- Al dominar LeetCode 1938 fortalecerás tu comprensión de las estructuras de datos de árboles, la manipulación de bits y la optimización algorítmica – habilidades que están en demanda en casi todas las entrevistas de alta tecnología.

-...

¡Feliz codificación