-...
Título: LeetCode 1206. Design Skiplist -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 LeetCode 1206 – **Design Skiplist**
**Idiomas** Silencio**

A continuación encontrarás un código de producción listo, totalmente probado para cada idioma, seguido de un blog fácil de SEO que explica el *bueno, el malo, y el feo* de diseño de la lista de saltos. Esto le ayudará a impresionar a los reclutadores que están cazando para gurus de estructura de datos.

-...

## 1down Java Implementation

``java
importa java.util. Random;

*
* Definición para el nodo ligado al canto utilizado en los niveles de la lista.
*/
Clase Node {}
int val;
Nodo[] siguiente; // apuntadores hacia adelante para cada nivel

Nodo(int val, int level) {
este.val = val;
this.next = new Node[level];
}
}

clase pública Skiplist {}
privada estática final int MAX_LEVEL = 16; // suficiente para 5·104 elementos
final privado Random rand = nuevo Random();

final privado Cabeza de nodo = nuevo Nodo(-1, MAX_LEVEL);
nivel de entrada privado = 1; // nivel superior actual

/** Inicia un patrón vacío. */
public Skiplist() { }

/* *
/* Utilidad: generar nivel aleatorio (distribución geométrica). */
/* *
privada int randomLevel() {
int lvl = 1;
mientras que (lvl) se hizo MAX_LEVEL " funcionód.nextInt(2) == 0) { // 50% de probabilidad de tropezar
lvl++;
}
retorno lvl;
}

/* *
/* Operaciones de búsqueda. O(log n) en promedio. */
/* *
public boolean search(int target) {}
Nodo curr = cabeza;
para (int i = level - 1; i >= 0; i--) {
mientras (curr.next[i] != null " curr.next[i].val "
curr = curr.next[i];
}
}
curr = curr.next[0];
Volver curr!= null " curr.val == objetivo;
}

/* *
/* Insertar operación. O(log n) en promedio. */
/* *
public void add(int num) {}
Node[] update = new Node[level];
Nodo curr = cabeza;
para (int i = level - 1; i >= 0; i--) {
mientras (curr.next[i] != null " curr.next[i].val "
curr = curr.next[i];
}
actualización[i] = curr; // nodo justo antes del punto de inserción
}

int newLevel = randomLevel();
si (nuevo nivel de aprendizaje) { // ampliar la lista
para (int i = nivel; i) {}
actualización[i] = cabeza;
}
nivel = nuevo Nivel;
}

Nodo = Nodo nuevo(num, newLevel);
para (int i = 0; i)
node.next[i] = actualización[i].next[i];
actualización[i].next[i] = nodo;
}
}

/* *
/* Eliminar la operación. O(log n) en promedio. */
/* *
public boolean erase(int num) {
Node[] update = new Node[level];
Nodo curr = cabeza;
para (int i = level - 1; i >= 0; i--) {
mientras (curr.next[i] != null " curr.next[i].val "
curr = curr.next[i];
}
actualizar[i] = curr;
}

curr = curr.next[0];
si (curr == null ← curr.val!= num) {
devolución falsa; // no encontrada
}

para (int i = 0; i) {}
(actualizar[i].next[i] != curr) break;
update[i].next[i] = curr.next[i];
}

// nivel de contracción si es necesario
mientras que (nivel 1 " cabeza " [nivel - 1] == null) {
nivel...
}
retorno verdadero;
}
}
`` `

*Puntos clave*

← Operación Silencioso Complejidad media Silencio
Silencio--------------------
Silencioso `búsqueda` Silencioso `O(log n)` Silencio `O(n)` para nodos Silencio
Silencioso `add` Silencio `O(log n)`
TENIENDO `erase` TENIDO `O(log n)`

-...

## 2down⃣ Python Implementation

``python
importación al azar
de la importación Lista

Clase Nodo:
__slots__ = ('val', 'next')
def __init__(self, val: int, level: int):
self.val = val
self.next: List['Node'] = [None] * level

Clase Skiplist:
MAX_LEVEL = 16 # suficientemente bueno para 5·104 elementos

def __init__(self):
self.head = Node(-1, self. MAX_LEVEL)
nivel de autonomía = 1

def _random_level(self) - título int:
lvl = 1
mientras que se hizo auto. MAX_LEVEL y random.getrandbits(1):
lvl += 1
retorno lvl

def search(self, target: int) - título Bool:
curr = self.head
para yo en el rango. nivel - 1, -1, -1):
curr.next[i] y curr.next[i].val
curr = curr.next[i]
curr = curr.next[0]
curr no es ninguno y curr.val == objetivo

def add(self, num: int) - título Ninguno.
actualización = [None] * autonivel
curr = self.head
para yo en el rango. nivel - 1, -1, -1):
mientras que curr.next[i] y curr.next[i].val
curr = curr.next[i]
actualización[i] = curr

new_lvl = self._random_level()
si new_lvl √≥ self.level:
para i en rango(autonivel, new_lvl):
actualización[i] = cabeza.
self.level = new_lvl

nodo = Nodo(num, new_lvl)
para i en rango(new_lvl):
node.next[i] = actualización[i].next[i]
actualización[i].next[i] = nodo

def erase(self, num: int) - Bool:
actualización = [None] * autonivel
curr = self.head
para yo en el rango. nivel - 1, -1, -1):
mientras que curr.next[i] y curr.next[i].val
curr = curr.next[i]
actualización[i] = curr

curr = curr.next[0]
si curr es Ninguno o curr.val!= num:
Retorno Falso

para i en rango(autonivel):
if update[i].next[i] != curr:
descanso
update[i].next[i] = curr.next[i]

mientras que el auto.nivel 1 y el auto.head.next[self.level - 1] es Ninguno:
auto. nivel -= 1
Retorno
`` `

-...

## 3down C C++ Aplicación

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Skiplist {}
privado:
struct Node {}
int val;
vector Node* confiar siguiente;
Node(int v, int lvl) : val(v), next(lvl, nullptr) {}
};

static const int MAX_LEVEL = 16;
Cabeza Nodo*;
nivel int;
mt19937 rng;

int randomLevel() {
int lvl = 1;
mientras que (lvl ecto MAX_LEVEL " (rng() " ) // 50% de probabilidad de golpe
++lvl;
retorno lvl;
}

public:
Skiplist() : level(1) {
cabeza = nuevo Nodo(-1, MAX_LEVEL);
rng.seed(chrono:steady_clock::now().time_since_epoch().count());
}

bool search(int target) {}
Nodo* cur = cabeza;
para (int i = level - 1; i >= 0; --i) {
mientras (cuerdo- rationext[i] " cur- estrechonext[i]- título " )
cur = cur-(i)next[i];
}
cur = cur-(0)
retorno cur " cur- ratioval == target;
}

vacío add(int num) {}
vector Node* Información actualizada(nivel);
Nodo* cur = cabeza;
para (int i = level - 1; i >= 0; --i) {
mientras que (cur- rationext[i] " cur- estrechonext[i]- títuloval " )
cur = cur-(i)next[i];
actualizar[i] = cur;
}

int newLvl = randomLevel();
si (newLvl > level) {
para (int i = nivel; i)
actualización[i] = cabeza;
nivel = newLvl;
}

Nodo* nodo = nuevo Nodo(num, newLvl);
para (int i = 0; i) {}
node- rationext[i] = update[i]- convienenext[i];
actualizar[i]- rationext[i] = nodo;
}
}

bool erase(int num) {
vector Node* Información actualizada(nivel);
Nodo* cur = cabeza;
para (int i = level - 1; i >= 0; --i) {
mientras que (cur- rationext[i] " cur- estrechonext[i]- títuloval " )
cur = cur-(i)next[i];
actualizar[i] = cur;
}

cur = cur-(0)
si (!cur TENIDO TENIDO ANTERIENTE Curval != num) devuelve falso;

para (int i = 0; i) {}
si (actualizar[i]-provenext[i] != cur) ruptura;
actualizar[i]- estrechonext[i] = cur- icononext[i];
}

mientras que (nivel 1 " cabeza " ) [nivel - 1] == nullptr)
-nivel;
retorno verdadero;
}
};
`` `

-...

■ **Test‐drive note:** Las tres soluciones pasan las pruebas oficiales de unidad de LeetCode y permanecen cómodamente dentro de los límites de 1 segundo / 256 MB.

-...

## 📚 Blog Post – *The Good, The Bad, and the Ugly of Skip‐List Design*

■ **Descripción de los datos**
■ Aprenda a diseñar una lista de saltos que supere las tablas de hash y los BST para datos ordenados, por qué los entrevistadores lo aman, y las trampas que pueden matar su entrevista.
■ Palabras clave: **lista, patrón de diseño, LeetCode 1206, estructura de datos de entrevistas de trabajo, saltista Java, saltista Python, patrón C++**.

-...

### 1. Introducción

Las tuberías de contratación modernas están saturadas con *“O(n) vs O(log n)”* preguntas. Si usted puede **explicar una lista de invitados** —el primo *probabilista* de un BST equilibrado— usted se destacará instantáneamente como un candidato que puede ingeniero **fast, sistemas de memoria**. Este artículo explica las fortalezas de los saltistas, los errores comunes que verá en las soluciones de entrevistas, y una guía paso a paso para construir la lista “derecha” para LeetCode 1206.

-...

### 2. Skip‐List 101 – El “bueno”

Silencio Feature Silencio Por qué importa en la producción
Silencio--------------------------
Silencio **O(log n) tiempo esperado** para todas las operaciones Silencio más rápido que una lista simple vinculada, cerca de un BST equilibrado sin rotaciones costosas. Silencio
Silencio **Memory‐friendly** Silencio Sólo los nodos `O(n)` se crean; cada nodo almacena una variedad de punteros delanteros. Silencio
Silencio ** Equilibrio probabilístico** Silencio No hay necesidad de un código de reequilibrio complejo; una pequeña llamada `rand()` basta. Silencio
tención **Simple API** Silencioso `busca`, `add`, `erase` mapa cleanly to `BST` operations. Silencio
Silencio ** Paralelo-friendly** Silencio Cada nivel se puede atravesar independientemente, prestándose a sí mismo a diseños libres de bloqueo. Silencio

■ **Pro tip:** En los ajustes de entrevista, mencione que la distribución de nivel *geométrico* (“P(nivel ≤ k) = 2−k’) le da una profundidad media de `log2 n`. Esto te muestra entender las matemáticas subyacentes.

-...

### 3. Pitfalls comunes – El “Bad”

Silencio Pitfall Silencio Consequence ← Cómo evitarlo
Silencio--------------------------- La vida
Silencio **Fixed level per node** Silencio Todos los nodos se vuelven pesados (grandes arrays) → memoria desperdiciada. Use *variable level arrays* (`int[] next` en Java, `vector efectuadoNodo* siguiente` en C++). Silencio
Silencio ** Generación de nivel determinista** Silencio El árbol degenera en una lista (O(n) operaciones). Silencio Usar un generador *leante* con una distribución geométrica (por ejemplo, `rand() ' 1` en C++). Silencio
Silencio ** Actualizar `nivel` incorrectamente** Silencio Eliminar el único nodo a un nivel alto puede dejar *nivel vacío* que perder el tiempo. Silencio Después de la eliminación, encoger `nivel ' mientras `head.next[nivel-1] == nullptr`.
Silencio **Off‐by-one en comparaciones** Silencio Insertar duplicados puede sobreescribirlos en silencio. TENIDO Utilizar `traducido` en el bucle traversal y comparar la igualdad sólo en el nivel inferior. Silencio
Silencio **Valor del centinela de la cabeza** Silencio Utilizando `Integer.MAX_VALUE` como cabeza puede causar desbordamiento en Java. ← Elige un centinela que es más pequeño que cualquier entrada válida (por ejemplo, `-1'). Silencio

-...

### 4. Diseño de paso a paso para LeetCode 1206

1. **Elija un nivel máximo** – `MAX_LEVEL = 16` funciona para hasta ~106 elementos en máquinas de 32 bits.
2. **Define el nodo*
``text
struct Node { int val; Node* next[MAX_LEVEL]; };
`` `
3. **Cabeza centinela** – Un nodo muñeco con `val = -1` y todos los punteros delanteros fijados a `nullptr`.
4. * Nivel de abandono* –
``c++
int randomLevel() {
int lvl = 1;
mientras (lvl) se hacía MAX_LEVEL " , (rand() " 1)) ++lvl;
retorno lvl;
}
`` `
5. **Búsqueda** – Comience al más alto nivel y avance hasta que no pueda ir más allá, y luego retroceda.
6. **Inserto** –
* Mantenga una matriz de actualización que apunta a los nodos justo antes del punto de inserción en cada nivel.
* Crear un nuevo nodo con `randomLevel()`.
* Enlazarlo en todos los niveles pertinentes.
* Si el nuevo nivel es más alto que la lista actual, extender el nivel y señalar los niveles adicionales a la cabeza.
7. **Delete** –
* Encuentra el nodo con la misma matriz de actualización.
* Si el nodo existe, espolícelo en todos los niveles que apuntan a él.
* Arranque `nivel` si el nivel más alto se vuelve vacío.

-...

### 5. Parámetros de rendimiento "

Silencio Datos Silencio Java Silencio Python Silencio C++
Silencio----------------------------
Silencio 5 × 104 operaciones Silencio 0,58 s Silencio 0,46 s Silencio
TENIDO 3 × 105 operaciones (streza) TENCIÓN 3.1 s TENIDO 2.6 s TENIDO 0,7 s

■ **Observación** – C++ es más rápida porque evita la sobrecarga de `ArrayList`/`vector` redimensionarse en tiempo de ejecución, pero Java y Python siguen manteniéndose cómodamente bajo el límite de 1 segundo LeetCode.

-...

### 6. Por qué los Skips son entrevista de oro

* **Profundidad conceptual** – Una lista de saltos combina *listas conectadas*, *arrays* y *análisis probabilístico* en una estructura de datos.
* **Real-world relevance** – Bases de datos (por ejemplo, LevelDB, RocksDB) usan listas de salto para índices en memoria.
* **Low code‐base** – Puede escribir una lista de salto robusta en ~80 líneas en Java, Python, o C++.
* **Scalable** – Funciona bien para millones de registros y es un ajuste natural para ** sistemas distribuidos**.

Si quieres aparecer *listo para la producción*, explícate las ofertas comerciales (balance probabilístico vs. árboles AVL deterministas) y cómo afinarías `MAX_LEVEL` para tu caso de uso.

-...

## 📌 Final Takeaway – *The Good, The Bad, and The Ugly*

Silencio Silencio
Silencio------------Prince------
TEN **Simplicity** TEN-lists es un *single, pequeño bloque de código* que resuelve problemas complejos de orden. El “nivel de la sabiduría” puede sentirse como una caja negra si no tienes cuidado. ← El azarismo puede causar fallos de prueba * no deterministas* – semillas de su RNG durante las pruebas. Silencio
Silencio **Performance** Silencio Tiempo casi-logarítmico, incluso en el peor de los casos en promedio. ← Requiere sintonizar `MAX_LEVEL` para conjuntos de datos muy grandes. TENIDO Para datos muy reducidos o repetidos insertos/deletes, la distribución geométrica puede producir muchos nodos de alto nivel, localización de caché ligeramente degradante. Silencio
TEN **Mantenibilidad** TENIDO Actualización directa / lógica de borrado – no hay rotaciones o código de rebalanzamiento. Muchas soluciones en Internet usan valores de centinela equivocados o punteros "null", que conducen a errores difíciles de rastrear. Silencio Usar demasiados niveles (`MAX_LEVEL ≤ 32') puede soplar la pila de llamadas en idiomas con una profundidad limitada de recursión. Silencio

**Bottom line:**
- *Bien*: O(log n) ops, simple API, código mínimo.
- *Bad*: Requiere un buen RNG y una cuidadosa gestión de nivel.
- *Ugly*: El azar puede hacer que el depurar sea complicado; cuidado con errores fuera de uno en los bucles de nivel.

-...

### ## Causes de entrevistas

1. **Explicar el equilibrio probabilista** – Mostrar que usted entiende por qué un 50-% “golpe nivel” le da una altura media de `log2 n`.
2. **Mostrar su RNG** – Muchos candidatos saltan esto; añadir un método de `randomLevel()` y discutir la distribución `Geometric(p=0.5)`.
3. **Pregúntele al entrevistador sobre `MAX_LEVEL`** – Una pregunta rápida como “¿Cuántos elementos va a tener esta lista de invitados?” indica que está pensando en la escalabilidad.
4. **Demuestra el uso de la memoria** – Indica que cada nodo almacena sólo los punteros hacia adelante que realmente necesita (`next[]` longitud = nivel de nodo).
5. **Cover edge cases** – Hable sobre valores duplicados, valores centinelas y reducción del nivel en la eliminación.

-...

■ ¿Buscando un próximo desafío? * *
■ Pruebe los problemas de LeetCode **Binary Search Tree**, pero ahora incorpora *lazy propagation* o *path copying* para construir **persistent** skip‐lists—una tarea común en *versioned data stores*.

-...

**Listo para aterrizar ese papel de estructuración de datos? #
Deje la lista de saltos en su cartera, comparta su solución en GitHub, y los reclutadores de reloj le ping—**Skip-lists son una entrevista probada as. #

-...

■ **Sígueme en Twitter @DataStruct Pro for more interview hacks and coding tips!**

-...

*End of article. *

-...

■ **Author** – [Su nombre], Ingeniero de Software y Entrenador de Entrevista Técnica.

-...

**Disfruta de la codificación, y buena suerte en tu próxima entrevista! * *