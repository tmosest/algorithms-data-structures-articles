-...
Título: LeetCode 381. Insert Delete GetRandom O(1) - Duplicados permitidos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 381. Insertar Eliminar GetRandom O(1) – Duplicados Permitidos
### Solución de personal completo en **Java / Python / C+** + un post de blog amigable con SEO

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

Necesitamos una estructura de datos que apoye las siguientes operaciones en tiempo *medio* O(1):

Silencio Operación Silencioso Descripción
Silencio----------------------------------------
Silencio `insert(val)` ¦ Add `val` to the multiset. Se permiten duplicados. TENIENDO `verdad ' si `val` no estaba ya presente, de otra manera `false ' Silencio
Silencio `remove(val)` Silencio Remove one occurrence of `val` if it exists. TENIDO `verdad ' si la remoción tuvo éxito, de lo contrario `false ' Silencio
Silencioso `getRandom()` Vuelva un elemento aleatorio. La probabilidad de cada elemento es proporcional a su frecuencia en el multiset. ← Un entero al azar

■ **Constraints**
≤ 231 - 1
≤ 2 × 105 operaciones totales
* `getRandom()` nunca se llama a una colección vacía

-...

#### 2down⃣ Core Idea – “Index‐Based HashMap + Dynamic Array”

1. **Dirección Dinámica** (`ArrayList` / `vector` / `list`) mantiene cada elemento insertado.
* Acceso aleatorio (`O(1)`) → perfecto para `getRandom()`.
* El último elemento se puede eliminar en `O(1)` intercambiando con la posición que queremos eliminar.

2. **HashMap** (`Mapa realizadaInteger, Set GarantizadoInteger confianza`) mapas un valor → *all* índices donde ese valor ocurre en el array.
* Nos permite localizar rápidamente una ocurrencia arbitraria de `val`.
* El conjunto puede ser un `HashSet`, `LinkedHashSet`, o `unordered_set` (C++).

3. ** Eliminación**:
* Escoge un índice arbitrario `i` del conjunto de `val`.
* Reemplace `array[i]` with the last element `last`.
* Actualizar los conjuntos para 'val' y 'último'.
* Retire el último elemento del array.

Todas las operaciones son **amortized O(1)** – las operaciones establecidas y las operaciones vectoriales son O(1) en promedio.

-...

#### 3down⃣ Código

■ **Las tres implementaciones siguen la misma lógica** – sólo cambios de sintaxis.

-...

##### 3.1 Java

``java
importar java.util*;

clase pública Collección aleatoria {}
// Almacena todos los elementos
final privado datos;
// Valor de mapas - conjunto de índices donde el valor ocurre
Mapa final privado realizadoInteger, Establecer los índices Integer título
final privado Random rand;

public RandomizedCollection() {}
datos = nuevo ArrayList seleccionado();
indices = nuevo HashMap fiel();
rand = nuevo Random();
}

* Inserta un valor a la colección. */
public boolean insert(int val) {
// ¿La primera vez que vemos Val?
booleano es nuevo = !indices.containsKey(val);
indices.computeIfAbsent(val, k - título new HashSet correctamente()).add(data.size());
data.add(val);
El regreso es nuevo;
}

* Elimina un valor de la colección. */
public boolean remove(int val) {
Establecer:Integer título idxSet = indices.get(val);
si (idxSet == null ← idxSet.isEmpty()) retornan falsos;

// Agarra un índice arbitrario del valor para eliminar
int removeIdx = idxSet.iterator().next();
idxSet.remove(removeIdx);

int lastIdx = data.size() - 1;
int lastVal = data.get(lastIdx);

// Mueva el último elemento en el punto del elemento eliminado
data.set(removeIdx, últimoVal);
// Actualizar el índice establecido para el último Val
Establecer:Integer confianza lastIdxSet = indices.get(lastVal);
lastIdxSet.remove(lastIdx);
lastIdxSet.add(removeIdx);

// Eliminar el último elemento de la lista
data.remove(lastIdx);

// Limpiar mapa si no quedan más índices
si (idxSet.isEmpty()) indices.remove(val);
retorno verdadero;
}

* Obtenga un elemento aleatorio de la colección. */
public int getRandom() {}
data.get(rand.nextInt(data.size()));
}
}
`` `

-...

###### 3.2 Python

``python
importación al azar
de las colecciones importadas por defecto

clase RandomizedCollection:
def __init__(self):
self.data = [] # lista de todos los valores
auto.indices = defaultdict(set) # val - título de posiciones

def insert(self, val: int) - título Bool:
is_new = val no en uno mismo. índices
auto.indices[val].add(len(self.data))
self.data.append(val)
El regreso es nuevo

def remove(self, val: int) - título Bool:
si Val no en sí mismo. índices o no auto.indices[val]:
Retorno Falso

remove_idx = self.indices[val].pop()
last_idx = len(self.data) - 1
last_val = self.data[last_idx]

# Reemplazar el punto eliminado con el último elemento
self.data[remove_idx] = last_val
auto.indices[last_val].add(remove_idx)
auto.indices[last_val].discard(last_idx)

self.data.pop()

si no auto.indices[val]:
del self.indices[val]
Retorno

def getRandom(self) - Propiedad int:
volver al azar.choice(self.data)
`` `

-...

#### 3.3 C++ (GNU+17)

``cpp
Incluido el título
#include ■unordered_map Conf
#include ■unordered_set
#Incluye #

clase aleatoria Colección {}
public:
RandomizedCollection() : gen(rd()), dis(0, 0) {}

bool insert(int val) {
bool isNew = mp.find(val) == mp.end();
mp[val].insert(data.size());
data.push_back(val);
El regreso es nuevo;
}

bool remove(int val) {
auto = mp.find(val);
si (it == mp.end() TENIDO SUPERVISIÓN-Consejo.empty()) retornan falsos;

// índice para eliminar
int idx = *it- convienesecond.begin();
it- título.erase(idx);

int lastVal = data.back();
int lastIdx = data.size() - 1;

// Mueva el último elemento en idx
data[idx] = last Val;
mp[lastVal].insert(idx);
mp[lastVal].erase(lastIdx);

data.pop_back();

si (es decir, segundo.empty()) mp.erase(it);
retorno verdadero;
}

int getRandom() {}
dis = std::uniform_int_distribución obtenidaint(0, data.size() - 1);
datos de devolución [dis(gen)];
}

privado:
std::vector obtenidosint datos del usuario;
std::unordered_map armonizado, std::unordered_set mp;
std::random_device rd;
std::mt19937 gen;
std::uniform_int_distribución hechaint dis;
};
`` `

-...

### 4 comentarios ⃣ Blog Artículo – “El Bien, el Mal, el Ugly of RandomizedCollection”

■ **SEO Palabras clave**: `LeetCode 381`, `RandomizedCollection`, `O(1) insert delete random`, `multiset data structure`, `hashmap vector trick`, `duplicate elements`, `data structures interview`, `python c+ java`, `job interview coding `

-...

##### 4.1 Introducción

Cuando los reclutadores piden “ejecutar una estructura de datos que soporta insertar, eliminar y getRandom en tiempo constante”, no solo están probando su conocimiento de arrays o tablas de hash – están probando su capacidad para **combine** estructuras de datos creativamente.
LeetCode 381 – *Inserto Eliminar GetRandom O(1) – Duplicados permitidos* es un clásico favorito de entrevista que muestra este conjunto de habilidades exactas.

En este artículo vamos a diseccionar el **bueno**, el **bad**, y el **ugly** de resolver este problema. Ya sea que se esté preparando para una entrevista de codificación, mirando a su próximo papel, o simplemente agudizando su caja de herramientas algorítmica, esta guía le dará ideas accionables y fragmentos de código en Java, Python y C++.

-...

#### 4.2 The Good: Why the HashMap‐Vector Trick is a Game‐Changer

1. **Simplicity + Power** –
*Un array para acceso aleatorio, un hashmap para contabilidad de índice* – toda la solución encaja en menos de 100 líneas de código.
* Cada operación es *amortizada* O(1) – perfecta para preguntas de entrevista de alto volumen.

2. **Robustness with Duplicates** –
El hashmap almacena *sets* de índices, para que puedas rastrear fácilmente cuántas copias de un valor existen.
Esto elimina la necesidad de listas vinculadas o árboles que pueden degradar a O(log n).

3. **Patrón de lengua agnóstica** –
La misma lógica se traduce en Java ( " ArrayList + HashMap cumplimentado " ), Python ( "list + defaultdict(set) " ) y C++ ( " vencedor + unordered_map " ).
La habilidad demostrante en varios idiomas puede ser un fuerte diferenciador en funciones *full‐stack* o *backend*.

-...

#### 4.3 The Bad: Hidden Pitfalls That Trip Candidatos

Silencio Pitfall Silencio Lo que pasa es cómo evitarlo
Silencio----------------------------
Silencio **O(n) en el peor de los casos** Silencio Usar una lista y un conjunto que rehashes frecuentemente puede causar un pico de tiempo lineal. Silencio Rely on `HashSet`/`unordered_set` – they’re O(1) amortized, not worst‐case. Silencio
TEN **Off‐by‐One errors** TEN Wrong index update during swap (forgetting to update the set for the moved element). tención Escribe un método de ayudador `swapAndUpdate(int i, int lastIdx)` o comenta meticulosamente. Silencio
Silencio **Memoria fuga en Java** Silencio No quitar la llave del mapa cuando su conjunto se vuelve vacío → O(n) espacio. ← Limpiar con "si (set.isEmpty()) indices.remove(val);`. Silencio
Silencio **Iniciación del generador de comandos** Silencio En C++ crear la distribución en cada llamada puede ser caro. Silencio Mantenga vivo un generador::mt19937` y sólo reconstruya la distribución cuando el tamaño cambie. Silencio
Silencio **Python `defaultdict` misuse** Silencio Guardando accidentalmente conjuntos vacíos que mantienen la clave viva. TENIDOS Eliminar la llave cuando el conjunto se vacía (`del auto.indices[val]`). Silencio

-...

#### 4.4 The Ugly: Edge Cases & Debugging Tricks

1. **Swap‐and‐Remove Bug**
* Error común*: olvidando eliminar el último índice del conjunto del valor movido.
**Debug tip**: después de cada `remove()`, imprime el hashmap para el valor eliminado y el último valor para asegurar que los conjuntos sean consistentes.

2. **Empty Collection on `getRandom()**
El problema garantiza que esto no sucederá, pero la codificación defensiva paga en APIs del mundo real.
``java
si (data.isEmpty()) lanzar nuevo NoSuchElementException();
`` `

3. *Los números principales*
Al usar arrays, los valores negativos no importan – son sólo claves en el hashmap.
Pero en C++ `unordered_map observadoint, ... `` está bien; sólo tenga cuidado con `size_t` vs `int` conversiones.

4. *Mareos*
Algunos entrevistadores prueban la verdadera uniformidad. Use un *sistema RNG* (`Random` en Java, `random.choice` en Python, `mt19937` en C++) y **re-seed** si está escribiendo un servicio de larga duración.

-...

#### 4.5 How This Wins Interviewers

* **Showcases Data‐Structure Fusion** – Combinar array y hashmap es un sello distintivo de la ingeniería inteligente.
* **Highlights Edge‐Case Handling** – Duplicados, eliminaciones de valores perdidos y lógica de limpieza demuestran la atención al detalle.
* **Demonstrates Language Proficiency** – Proporcionar soluciones Java, Python y C++ muestra que estás listo para cualquier pila.
* **Habla a Real‐World Use** – `RandomizedCollection` es esencialmente un *multiset* con muestreo aleatorio rápido – un patrón utilizado en caches, balanceadores de carga y motores de juego.

-...

#### 4.6 Quick Checklist Antes de la entrevista

Silencio TENIDO ANTERIOR ANTERIOR
Silencio...
Silencio **Entender el problema** – se permiten duplicados. Silencio
Silencio **Conoce las estructuras de datos** – matriz dinámica + hashmap de conjuntos de índices. Silencio
TEN **Planea el borrador** – intercambia con el último elemento, actualiza índices. Silencio
Silencio ** Funciones de ayuda de palabras** – para mantener el código legible. Silencio
Silencio **Más a fondo** – insertar, eliminar, getRandom, casos de borde. Silencio
*Explicar su diseño* – grande– O, por qué utilizamos un conjunto, por qué es tiempo constante. Silencio
Silencio **Mention trade‐offs** – memoria overhead, potencial peor-case, específico del lenguaje. Silencio

-...

#### 4.7 Palabras finales

LeetCode 381 puede parecer engañosamente simple, pero es una prueba *code-generación* de comprensión profunda.
El **bueno** es la elegancia del patrón array-hashmap.
El **bad** es los errores sutiles que se esconden en la lógica del swap‐and-remove.
El **ugly** es los casos de borde que viajan incluso programadores experimentados.

Mostrando una implementación limpia y bien comunicada – como hemos hecho anteriormente – te permitirá entrar en la habitación de un reclutador y decir:
■ “Puedo construir un **multiset** que se comporta como una bolsa y todavía elegir un artículo aleatorio en O(1) – todo en Java, Python y C++. ”

¡Buena suerte aterrizando ese trabajo! 🚀

-...

■ *Si has encontrado este artículo útil, dale un 👍, compártelo en LinkedIn, o deja un comentario abajo – vamos a ayudar a la próxima generación de ingenieros a romper LeetCode 381 y aterrizar sus roles de sueño. *

-...

■ *Copyright © 2023 “Coding Interviews Demystified” – Todos los derechos reservados. *

-...

### 📚 Referencias > Leer más

1. [LeetCode 381 – Insert Delete GetRandom O(1) – Duplicates allowed](https://leetcode.com/problems/insert-delete-getrandom-o1-duplicates-allowed/)
2. [GeeksforGeeks – Randomized Set " Multiset](https://www.geeksforgeeks.org/design-a-data-structure-that-supports-insert-delete-getrandom-in-constant-time/)
3. [EntreviewBit – Constant Time Operations](https://www.interviewbit.com/question/insert-delete-get-random-o1/)

-...

¡Feliz codificación! 💻🔥