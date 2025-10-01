-...
Título: LeetCode 432. All O`one Data Structure -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# All‐O`one` Estructura de datos – Java / Python / C++ Implementación + SEO‐Optimised Blog

■ **TL;DR**
■ *All-O`one`* es un problema difícil de LeetCode (ID 432) que pide una estructura de datos que apoye **O(1)** `inc`, `dec`, `getMaxKey`, and `getMinKey`.
■ La solución clásica es una lista de cubos de frecuencia que se vinculan con *** + ** mapas de hash**.
■ A continuación encontrará implementaciones de trabajo en **Java, Python, y C+** y un blog completo y fácil de entrevista que explica el “bueno, el malo y el feo” del diseño.

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

``text
AllOne() // inicializar la estructura de datos
inc(String key) // key+ (insertar si no está ausente)
dec(String key) // key-- (remove if cero)
getMaxKey() → Cierre // llave con frecuencia máxima
getMinKey() → Pendiente // llave con frecuencia mínima
`` `

Todas las operaciones deben funcionar en el tiempo **medio O(1)**.
Limitaciones: hasta **5 × 104 llamadas**, longitud clave ≤ 10, letras minúsculas solamente.

-...

## 2down Idea de alto nivel (el “bueno”)

1. **Bucket (Nodo)** – representa una frecuencia `f`.
* `Set Garantizar claves de confianza` - todas las teclas que actualmente tienen frecuencia `f`.
* `int freq` – el valor de frecuencia.
* `prev / next` – punteros para una lista doblemente vinculada.

2. **Sentinels** – `head` (freq 0) y `tail` (infinito).
* La lista se mantiene ** surtido por frecuencia** (aumento de `head` a `tail`).
* `head.next` es el cubo con la frecuencia **minimum**; `tail.prev` el **maximum**.

3. HashMaps
* `keyToNode: Mapa seleccionadoString, Node confianza` - encontrar rápidamente el cubo una vida clave en.
* No hay necesidad de un mapa de frecuencia a cero porque el cubo en sí sabe su frecuencia.

4. *Operaciones*
* `inc `
* Encontrar el nodo actual a través de `keyToNode`.
* Quitar la llave del cubo actual.
* Mover (o crear) la clave en el cubo *next* (`freq + 1`).
* Eliminar el viejo cubo si se vuelve vacío.
* `dec` - simétrico a `inc ' (move a `freq - 1` o eliminar la clave).
* `getMaxKey` / `getMinKey` – simplemente mire a `tail.prev.keys` / `head.next.keys`.
* Todos los ajustes punteros y las operaciones establecidas son **O(1)**.

5. **¿Por qué O(1) sobre Promedio? #
* Todas las estructuras de datos están basadas en listas fijas o conectadas.
* Sin iteración sobre las colecciones de longitud variable.
* La única operación “heavy” se inserta en un “Set”, que es promedio O(1) en Java, Python, C++ (“unordered_set”.

-...

## 3down “El malo” – Cosas que hay que ver

¿Por qué duele?
Silencio------------------------
Silencio **Tipo vacío** – olvidando eliminarlo después de eliminar una clave Silencioso escapes de memoria, incorrecto min/max Silencio Después de la eliminación de la llave, si `bucket.keys.isEmpty()`, unlink el cubo. Silencio
Silencio **Nodos Duplicados** – crear accidentalmente dos nodos para el mismo freq ¦ Ordenación incorrecta, mapeo de clave incorrecto ¦ Antes de insertar, compruebe si `next.prev` o `prev.next` ya tiene el freq objetivo. Silencio
Silencio **Problemas de emergencia** – inc sobre una nueva clave, dec a 0 ← Asociación de ganglios equivocados Silencio Handle “nueva clave” y “freq 1 → eliminar” como casos especiales. Silencio
Silencio **Iterator invalidation** – using `Iterator` on a `Set` while modifying it Silencio Runtime error ← Use `iterator()` once, remove via `iterator.remove()`, or just call `set.remove(key)` directly. Silencio
Silencio **Tread safety** – no se requiere en LeetCode pero importa en la producción Silencio Carreras de datos Silencio Envolver toda la estructura en un bloque "sincronizado" o utilizar `ConcurrentHashMap` y un `ReentrantLock`. Silencio

-...

## 4down “El Ugly” – Pitfalls comunes en Codificación de Entrevista

Silencio Pitfall Silencio Consequence ← Cómo evitar
Silencio------------------------------
Silencio **Using a single `HashMap ' for freq→set and key→freq** tención Complexity becomes O(n) because you’d need to search a set to find the key ' s balde ← Mantenga dos mapas independientes ( "keyToNode " , " llave " ). Silencio
Silencio **Re-alizar cubos en cada inc/dec** Silencio Extra heap churn, posible pausa de GC ANTE Reutiliza el cubo existente si el freq adyacente ya existe. Silencio
Silencio **No usar centinelas** ← Null checks all over, bug‐prone tención Siempre tienen 'head` y 'tail` nodos muñecos. Silencio
Silencio **Retornar cualquier llave** – utilizando `set.iterator().next()` Silencio Aceptable por espectaculo pero puede ser confuso si `Set` está vacío Silencioso guardia contra vacío `head.next` / `tail.prev`. Silencio

-...

## 5down Code Walk-through

### 5.1 Java

``java
importar java.util*;

clase pública AllOne {

* Nodo de cubo – sostiene una frecuencia y un conjunto de llaves. */
Clase privada estática Nodo {}
int freq;
Establecer las teclas de acceso = nuevo HashSet correctamente();
Nodo prev, siguiente;

Nodo(int f) { this.freq = f; }
}

final privado Cabeza de nodo, cola; // centinelas
mapa final privado significa:Neding, Node confianza keyToNode = nuevo HashMap correctamente();

public AllOne() {
cabeza = nuevo Nodo(0); // freq 0 – tonto
cola = nuevo Nodo(0); // freq ∞ – dummy
head.next = tail;
tail.prev = head;
}

* Incrementar la cuenta de una llave. */
public void inc(String key) {}
Nodo cur = keyToNode.get(key);

// nueva clave – insertar en el cubo de freq 1
si (cur == null) {
Nodo primero = cabeza.next;
si (primero ==la cola Новывываный primero.freq != 1) {
Nodo nuevoNodo = nuevo Nodo 1);
newNode.keys.add(key);
insertar After(head, newNode);
keyToNode.put(key, newNode);
. ♫ ... {
primero.keys.add(key);
keyToNode.put(key, first);
}
retorno;
}

// llave existente - pasar a cubo freq+1
cur.keys.remove(key);
Nodo siguiente = cur.next;
si (siguiente == la cola Silencioso siguiente.freq != cur.freq + 1) {
Nodo nuevoNodo = nuevo Nodo(cur.freq + 1);
newNode.keys.add(key);
insertar After(cur, newNode);
keyToNode.put(key, newNode);
. ♫ ... {
siguiente.keys.add(key);
keyToNode.put(key, next);
}

// unlink cursi si está vacío
si (cur.keys.isEmpty()) unlink(cur);
}

* Decrementar la cuenta de una llave. */
public void dec(String key) {
Nodo cur = keyToNode.get(key);
si (cur == null) retorno; // clave no existe

cur.keys.remove(key);

// clave se convierte en cero – borra la asignación
si (cur.freq == 1) {
keyToNode.remove(key);
. ♫ ... {
Nodo prev = cur.prev;
si (prev == head ¦
Nodo nuevoNodo = nuevo Nodo(cur.freq - 1);
newNode.keys.add(key);
insertar After(prev, newNode);
keyToNode.put(key, newNode);
. ♫ ... {
prev.keys.add(key);
keyToNode.put(key, prev);
}
}

si (cur.keys.isEmpty()) unlink(cur);
}

/** Devuelve cualquier llave con la frecuencia máxima. */
public String getMaxKey() {}
si (tail.prev == head) regresan ";
devolver cualquierKey(tail.prev.keys);
}

/** Devuelve cualquier llave con la frecuencia mínima. */
public String getMinKey() {}
si (head.next == tail) regresan ";
devolver cualquierKey(head.next.keys);
}

--------- Métodos de ayuda...-------- */

inserción privada de vacío Después(Nodo nodo, Nodo newNode) {}
newNode.prev = node;
newNode.next = node.next;
node.next.prev = newNode;
node.next = newNode;
}

inserción privada de vacío After(Node prev, Node newNode) {}
newNode.prev = prev;
newNode.next = prev.next;
prev.next.prev = newNode;
prev.next = newNode;
}

vacío privado unlink(Nodo node) {
node.prev.next = node.next;
node.next.prev = node.prev;
// Java GC liberará el nodo una vez que ninguna referencia permanezca
}

privada String anyKey( Se establece:
Iterator se llevó a caboStringilo = s.iterator();
devolverlo.hasNext() ? it.next() : ";
}
}
`` `

■ **Por qué esto compila* *
* `insertAfter` está sobrecargado para que podamos llamarlo desde `head ' y cualquier nodo real.
* Todas las operaciones implican en la mayoría de una sola modificación `HashSet` y un intercambio de punteros constante. *

-...

### 5.2 Python

``python
de las colecciones importadas por defecto

Clase Todos Uno:
""Nodo de lista doblemente vinculado – cubo de frecuencia.""
Clase Nodo:
__slots__ = ('freq', 'keys', 'prev', 'next')
def __init__(self, freq: int):
self.freq = freq
auto.keys = set()
auto.prev = Ninguno
self.next = Ninguno

def __init__(self):
self.head = self.Node(0) # dummy
self.tail = self.Node(0) # dummy
auto.head.next = self.tail
self.tail.prev = self.head
auto.key_to_node = {} Node

def _insert_after(self, prev, node):
node.prev = prev
nodo.next = prev.next
prev.next.prev = node
prev.next = node

def _unlink(self, node):
node.prev.next = node.next
nodo.next.prev = node.prev

def inc(self, key: str) Ninguno.
cur = self.key_to_node.get(key)
si Cur es Ninguno: # nueva llave
primero = auto.head.next
si primero es uno mismo. cola o primero. freq!= 1:
nodo = yo.Nodo(1)
node.keys.add(key)
self._insert_after(self.head, node)
auto.key_to_node[key] = nodo
más:
primer.keys.add(key)
auto.key_to_node[key] = first
Regreso

# existente key
cur.keys.remove(key)
nxt = cur.next
si Nxt es uno mismo. cola o nxt. freq != cur.freq + 1:
nodo = uno mismo.Nodo(cur.freq + 1)
node.keys.add(key)
self._insert_after(cur, node)
auto.key_to_node[key] = nodo
más:
nxt.keys.add(key)
auto.key_to_node[key] = nxt

si no cur.keys:
self._unlink(cur)

def dec(self, key: str) Ninguno.
cur = self.key_to_node.get(key)
si el curro es Ninguno: regresar # nada que hacer

cur.keys.remove(key)
si cur.freq == 1:
del yo. key_to_node[key]
más:
prev = cur.prev
si el prev es uno mismo. cabeza o prev.freq != cur.freq - 1:
nodo = yo.Nodo(cur.freq - 1)
node.keys.add(key)
auto._insert_after(prev, node)
auto.key_to_node[key] = nodo
más:
prev.keys.add(key)
auto.key_to_node[key] = prev

si no cur.keys:
self._unlink(cur)

def getMaxKey(self) - título str:
si yo. La cola.prev es uno mismo. cabeza:
"Regresa"
volver siguiente(a su(auto.tail.prev.keys))

def getMinKey(self) - título str:
si yo. El siguiente es el uno mismo. cola:
"Regresa"
volver siguiente(a su(auto.head.next.keys))
`` `

■ * Nota de Python* – `self. Node` es una clase interna ligera; las operaciones `set` son O(1) en promedio.

-...

### 5.3 C++

``cpp
#include ■unordered_set
#include ■unordered_map Conf
#include ■string
#include ■iostream

clase AllOne
privado:
struct Node {}
int freq;
std::unordered_set obtenidosstd::string claves;
Nodo* prev = nullptr;
Nodo* siguiente = nullptr;
Nodo(int f) : freq(f) {}
};

Cabeza de nodo*; // cabeza de muñeco (freq 0)
Node* tail; // dummy tail (freq INF)
std::unordered_map buscado::string, Nodo* keyToNode;

/* Insertar nuevo nodo después de 'pos'.
inserción After(Node* pos, Node* node) {
node- tituladaprev = pos;
node-cliente = pos-clientenext;
" pos "
pos-amentonext = nodo;
}

/* Quitar el nodo de la lista. */
vacio unlink(Nodo* nodo) {
node- títuloprev- rationext = node- títulonext;
node-]next-proveprev = node- títuloprev;
borrar nodo; // memoria libre
}

public:
AllOne() {
head = new Node(0);
tail = new Node(0);
head-ientenext = tail;
la cola-consiguiente = cabeza;
}

~AllOne() {
// limpiar todos los nodos
Nodo* cur = cabeza;
mientras que (cur) {
Nodo* nxt = cur- rationext;
Borrar el curro;
cur = nxt;
}
}

vacio inc(cont std::string curva key) {
auto = keyToNode.find(key);
if (it == keyToNode.end()) { // new key
Nodo* primero = cabeza- rationext;
si (primero ==la cola TENIDO ANTERIENDA EN LA PRIMERA 1) {
Nodo* nuevoNodo = nuevo Nodo 1);
newNode- confíakeys.insert(key);
insertar After(head, newNode);
keyToNode[key] = newNode;
. ♫ ... {
primer- títulokeys.insert(key);
keyToNode[key] = primero;
}
retorno;
}

Nodo* cur = it- segundos;
cur- títulokeys.erase(key);
Nodo* nxt = cur- rationext;
si (nxt == tail  durable nxt-jerofreq != cur-юfreq + 1) {
Nodo* nuevoNodo = nuevo Nodo(cur- títulofreq + 1);
newNode- confíakeys.insert(key);
insertar After(cur, newNode);
keyToNode[key] = newNode;
. ♫ ... {
nxt- títulokeys.insert(key);
keyToNode[key] = nxt;
}

si (cuarto-keys.empty()) unlink(cur);
}

vacio dec(cont std::string curva clave) {
auto = keyToNode.find(key);
si (it == keyToNode.end()) regresa; // falta clave

Nodo* cur = it- segundos;
cur- títulokeys.erase(key);

si (cuando- 1) {
keyToNode.erase(it); // key removed completely
. ♫ ... {
Nodo* prev = cur-propiv;
si (prev == head ← anterior prev- confianzafreq != cur-propfreq - 1) {
Nodo* nuevoNodo = nuevo Nodo(cur- títulofreq - 1);
newNode- confíakeys.insert(key);
insertar After(prev, newNode);
keyToNode[key] = newNode;
. ♫ ... {
prev- tituladokeys.insert(key);
keyToNode[key] = prev;
}
}

si (cuarto-keys.empty()) unlink(cur);
}

std::string getMaxKey() const {
si (alcista-prev == cabeza) regresan ";
volver *tail- Confprev- títulokeys.begin();
}

std::string getMinKey() const {
si (cabeza- ratio == cola) regresan ";
volver *head- Confnext- títulokeys.begin();
}
};
`` `

■ **C++ Nota** – `unordered_set` garantiza un promedio de búsqueda/insert/delete O(1).
■ La memoria se recupera inmediatamente a través de 'delete' cuando un cubo se vacía.

-...

## 6. Resumen de la complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio `inc` Silencio **O(1)** Silencio Nodo adicional sólo cuando es necesario
Silencioso:
Silencio `getMaxKey` / `getMinKey` Silencio **O(1)** Silencio Siempre constante (pick any element from the set)

■ *Todas las estructuras auxiliares de datos (`HashSet` / `unordered_set`) tienen un costo constante esperado.
■ *La lista vinculada garantiza que siempre conocemos los extremos sin traversal. *

-...

## 7. Por qué Esta es la Solución “Optimal”

1. **Un Paso, Operaciones Constantes** – Cada método toca un único cubo, realiza en la mayoría de un conjunto de operaciones, y cambia un número constante de punteros.
2. **Sin clasificación o montones** – Evitamos estructuras de datos costosas (heaps, BSTs) que degradarían a O(log n) por operación.
3. **Espacio-Eficiente** – Cada clave se almacena sólo una vez en el diccionario más una referencia a su cubo. Los cubos solo se crean cuando son necesarios y liberados inmediatamente cuando están vacíos.
4. **Scalability** – Adecuado para millones de claves y actualizaciones por segundo, como se requiere a menudo en sistemas de caché o contadores de frecuencia en servicios web de alto tráfico.

-...

## 8. Take‐ Away

- ** Lista de frecuencia rota** es la información clave: mantener un nodo por cuenta distinta.
- **Las actualizaciones constantes** se logran mediante la manipulación de punteros y las operaciones de conjunto basadas en hash.
- **Regresar cualquier llave** está satisfecha por simplemente recuperar un elemento arbitrario del cubo de la cabeza o la cola.

■ Este patrón es ampliamente utilizado en *LFU/LRU cache* implementaciones, *word-frequency* trackers, y muchos otros sistemas del mundo real que requieren estadísticas de frecuencia O(1).

Siéntase libre de copiar, probar y adaptar los fragmentos de código arriba en sus propios proyectos o de someterse como solución al problema LeetCode “**432. Todos Estructura de datos**”. ¡Feliz codificación!