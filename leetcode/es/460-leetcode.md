-...
Título: LeetCode 460. LFU Cache -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. LFU Cache – O(1) implementation in three languages

El clásico problema difícil de LeetCode 460: *Menos usados con frecuencia (LFU) Cache*.
El objetivo es apoyar el `get ' y `put ' en **average O(1)** time y desalojar el
llave con la frecuencia de acceso más baja (y, en caso de lazos, la menor
utilizado uno).

A continuación encontrará una implementación completa, lista para la producción para:

Silencio Idioma Silencio Archivo Silencio Key Idea Silencio
Silencio--------------
TEN Java ANTE `LFUCache.java` ANTE Dos mapas de hash + `LinkedHashSet` Silencio
Silencio Python Silencio `lfu_cache.py` Silencio Dos diccionarios + `OrderedDict` Silencio
Silencio C++ Silencio `lfu_cache.cpp` Silencio Dos `unordered_map` + `list` + `unordered_map` de los iteradores

Las tres soluciones se ejecutan en promedio **O(1)** y manejan capacidades hasta '10^4`
y llamadas `2·10^5` - exactamente lo que la declaración del problema exige.

■ ¿Por qué dos hash-maps? * *
■ *Uno* mantiene `key → (valor, frecuencia)`.
■ *Dos* mantiene `frecuencia → list/LinkedHashSet of keys` (preservando el orden LRU para cada frecuencia).
■ La variable `minFreq` nos dice qué cubo de frecuencia contiene el candidato de desalojo.

-...

## Java (`LFUCache.java`)

``java
importar java.util*;

*
* Diseñar e implementar una estructura de datos para un caché de menor uso (LFU).
*
* Todas las operaciones funcionan en el tiempo promedio O(1).
*/
clase pública LFUCache {

// clave - título (frecuencia, valor)
final privado Mapa cerrado cache;

// frecuencia - título claves que tienen esa frecuencia (mantiene orden LRU)
final privado Mapa seleccionadoInteger, LinkedHashSet freqMap;

capacidad privada de entrada final;
int privada minFreq; // frecuencia mínima actual

--------- nodo interno...
Clase privada estática Nodo {}
clave, valor, freq;
Nodo(int k, int v, int f) { key = k; value = v; freq = f; }
}

public LFUCache(int capacity) {
esto. capacidad = capacidad;
this.cache = nuevo HashMap Quería();
este.freqMap = nuevo HashMap garantizado();
esto.minFreq = 0;
}

* Devuelve el valor de la clave si está presente, de lo contrario -1. */
public int get(int key) {}
Nodo = cache.get(key);
si (nodo == nulo) regresan -1;
// aumento de frecuencia
updateFreq(node);
Nodo de retorno. valor;
}

/** Inserta/actualiza el par clave/valor. */
public void put(int key, int value) {}
(capacidad) 0) retorno;

Nodo = cache.get(key);
si (nodo != null) { // Actualizar la clave existente
node.value = value;
updateFreq(node);
retorno;
}

(cache.size() == capacity) { // eviction required
evict();
}

// insertar nueva clave
Nodo nuevoNodo = nuevo Nodo(key, value, 1);
cache.put(key, newNode);
freqMap.computeIfAbsent(1, ignorado - nuevo título LinkedHashSet correctamente()).add(key);
minFreq = 1; // nuevo nodo tiene freq 1
}

Ayudantes...

* Mueva el nodo al cubo de frecuencia siguiente. */
actualización privada de vacío Freq(Nodo nodo) {
int oldFreq = node.freq;
LinkedHashSet se realizóInteger confianza set = freqMap.get(oldFreq);
set.remove(node.key);
si (set.isEmpty()) {}
freqMap.remove(oldFreq);
si (minFreq == oldFreq) minFreq++; // si quitamos el cubo de min
}

Nodo. freq++;
freqMap.computeIfAbsent(node.freq, ignored - nuevos LinkedHashSet correctamente()).add(node.key);
}

* Evicts the least frequently (and least recently) used key. */
privada void evict() {}
LinkedHashSet se realizóInteger confianza set = freqMap.get(minFreq);
// Enlaces HashSet preserva el orden de inserción → primer elemento es LRU
int keyToRemove = set.iterator().next();
set.remove(keyToRemove);
si (set.isEmpty()) freqMap.remove(minFreq);

cache.remove(keyToRemove);
}
}
`` `

-...

## Python (`lfu_cache.py`)

``python
de las colecciones importan defaultdict, OrderedDict

clase LFUCache:
"
Diseñar e implementar una estructura de datos para un caché de menor uso (LFU).
Todas las operaciones funcionan en el tiempo promedio O(1).
"

def __init__(self, capacity: int):
autocapacidad = capacidad
auto.size = 0
self.min_freq = 0
auto.key_to_val_freq = {} # key - titulado (valor, freq)
auto.freq_to_keys = defaultdict(OrderedDict) # freq - título Ordenado Dict{key: None}

def get(self, key: int) - título int:
si la llave no es en uno mismo.key_to_val_freq:
retorno -1
val, freq = self.key_to_val_freq[key]
auto._increase_freq(key, val, freq)
retorno val

def put(self, key: int, value: int) - Ninguno.
si yo. Capacidad 0:
Regreso

si la llave en uno mismo.key_to_val_freq:
# Valor de actualización, mantener frecuencia
_, freq = self.key_to_val_freq[key]
auto.key_to_val_freq [key] = (valor, freq)
auto._increase_freq(key, value, freq)
Regreso

si yo. tamaño == auto.capacidad:
self._evict()

# Insert new key
auto.key_to_val_freq[key] = (valor, 1)
auto.freq_to_keys[1] = Ninguno
self.min_freq = 1
auto.size += 1

# ---------- auxiliares internos --------
def _increase_freq(self, key: int, value: int, freq: int) - título Ninguno.
""La llave móvil de freq a freq+1.""
# Remove from old freq cubo
del yo. freq_to_keys [freq][key]
si no yo. freq_to_keys [freq]:
del yo. freq_to_keys[freq]
si yo. min_freq == freq:
self.min_freq += 1

# add to new freq cubo
self.freq_to_keys[freq + 1][key] = Ninguno
# update mapping
auto.key_to_val_freq[key] = (valor, freq + 1)

def _evict(self) - Propiedad Ninguno.
""Evicto la tecla LRU en el cubo con la frecuencia más baja.""
# OrderedDict preserva orden de inserción - título la primera clave es LRU
evict_key, _ = self.freq_to_keys[self.min_freq].popitem(last=False)
si no auto.freq_to_keys[self.min_freq]:
del self.freq_to_keys[self.min_freq]
del self.key_to_val_freq[evict_key]
auto.size -= 1
`` `

■ ¿Por qué `OrderedDict`?**
■ En Python 3.7+ el `dict` regular preserva el orden de inserción, pero `OrderedDict`
Aún nos da una interfaz explícita de `popitem(last=False)` que funciona en más antiguo
■ CPython versiones y garantiza O(1) para borrar.

-...

## C++ (`lfu_cache.cpp`)

``cpp
#include יbits/stdc++.h
usando std namespace;

*
* Diseñar e implementar una estructura de datos para un caché de menor uso (LFU).
* Todas las operaciones funcionan en el tiempo promedio O(1).
*/
clase LFUCache {
public:
struct Node {}
int key, val, freq;
Nodo(int k, int v, int f) : key(k), val(v), freq(f) {}
};

LFUCache(int capacity) : capacity(capacity), size(0), minFreq(0) {}

int get(int key) {}
auto = keyMap.find(key);
(it == keyMap.end()) return -1;
Nodo &node = *(it- tituladosecond);
actualización (nodo);
retorno node.val;
}

vacío put(int key, int value) {}
(capacidad) 0) retorno;

auto = keyMap.find(key);
si (it != keyMap.end()) { // clave existe
it-Consegundo-conval = valor;
actualización (*(it- título)));
retorno;
}

si (tamaño ==capacidad) desalojo();

// insertar nueva clave
Nodo *nodo = nuevo Nodo(key, value, 1);
keyMap [key] = nodo;
freqMap[1].push_back(key);
freqPos[key] = --freqMap[1].end(); // iterator a its position
minFreq = 1;
++tamaño;
}

privado:
int capacity, size, minFreq;
unordered_map madeint, Node* ClaveMap; // key - nodo*
unordered_map seleccionada, lista indicativamente usuario freqMap; // freq - lista de claves (LRU)
unordered_map madeint, list didint título::iterator confianza freqPos; // key - título iterador dentro de su lista

valid update(Node &node) {
int oldF = node.freq;
// quitar la llave del viejo cubo
freqMap[oldF].erase(freqPos[node.key]);
si (freqMap[oldF].empty()) {}
freqMap.erase(oldF);
si (minFreq == oldF) ++minFreq;
}

// añadir clave a nuevo cubo
Nodo. freq++;
freqMap[node.freq].push_back(node.key);
freqPos[node.key] = --freqMap[node.freq].end();
}

vaciado() {}
int key = freqMap[minFreq].front();
freqMap[minFreq].pop_front();
si (freqMap[minFreq].empty()) freqMap.erase(minFreq);
eliminar keyMap[key];
keyMap.erase(key);
- tamaño;
}
};
`` `

■ **¿Por qué `list` + mapa iterador? * *
> `list` nos da la eliminación constante a tiempo dado un iterador.
■ El mapa de `freqPos` recuerda el iterador de cada llave dentro de su cubo de frecuencia,
± nos permite eliminarlo en O(1).

-...

## 2. The Good, The Bad & The Ugly – Un blog SEO‐Ready Post

■ **Target audience**: ingenieros de software que se preparan para entrevistas de diseño del sistema, personal directivos que buscan habilidades de estructura de datos, y cualquier persona curiosa sobre cómo funciona LFU bajo la capucha.

-...

### The Good: Why LFU Matters

* **Real-world caching** – Bases de datos, servidores de bordes CDN y página de OS–reemplazamiento
todas las políticas utilizan LFU (o variantes).
La maestría demostrante de LFU le muestra entender *el desalojo basado en frecuencia*,
no sólo *tiempo basado* (LRU) o *de tamaño* (FIFO).

* **Interview buzz‐word** – Problema de LeetCode 460 es un problema básico en el nivel superior
entrevistas. Resolverlo correctamente y de manera eficiente es una bandera verde para contratar
gerentes.

* **O(1) complejidad** – Probando que puede diseñar estructuras de datos que se reúnen
tiempo-espacio estricto garantiza el conocimiento profundo de las tablas de hash, vinculadas
listas y análisis amortizado.

-...

### The Bad: Common Pitfalls

Silencio Pitfall Silencioso Silencioso
Silencio------------
Silencio **No mantener el orden LRU por frecuencia** Silencio Evicts the most recently used key → wrong answer Silencio Use `LinkedHashSet` (Java), `OrderedDict` (Python), o `list` with iterators (C++) to preserve order inside each cubo. Silencio
Silencio **Actualización de la frecuencia puesta pero no en get** Silencio candidato de desalojo Wrong TEN siempre golpe la frecuencia para 'get' y para una actualización sólo 'put`. Silencio
Silencio **Missing `minFreq` actualización después de la eliminación de cubos** Silencio `evict()` tira de un cubo vacío → `KeyError` / `IndexError` Silencio Después de quitar la última llave de un cubo de frecuencia, aumentar `minFreq` ** sólo si** ese cubo era el mínimo. Silencio
Silencio ** Las filtraciones de memoria en C+** Silencio `nueva Noda` nunca suprimió la memoria del nodo desalojado en `evict()` o utilizar punteros inteligentes (`unique_ptr`). Silencio

-...

### Casos de borde que rompen su código

1. ** Capacidad cero** – Tu caché no debe hacer nada con gracia.
2. **Duplicar `put`** – Actualizar una clave existente debe *no* restablecer su frecuencia.
3. ** Frecuencias altas** – Las frecuencias pueden crecer sin límites; el mapa del cubo debe
asignar dinámicamente nuevos cubos y soltar viejos.
4. **Desahucios simultáneos** Cuando se alcanza la 'capacidad', siempre debes
*Exactamente una* clave. Una implementación de buggy podría tratar de desalojar dos
llaves en una llamada.

-...

## 3. Poner todo junto – Lo que busca

* **System‐design fluency** – Usted puede explicar *por qué* el patrón de dos-hash‐map
resuelve el problema en O(1).
* **Código limpio* Ningún estado mutable mundial, todos los métodos son " públicos " / " privados "
cuando sea apropiado, y la memoria se limpia (por ejemplo C++ elimina los nodos).
* **Testabilidad** – Cada implementación se puede comprobar unitariamente con la
`TestCase` de LeetCode, y usted puede añadir su propio 'si __name_== "_main__" arnés de prueba.
* **Documentación** – Comentarios claros y una breve sección “por qué” ayudan a contratar
gerentes y tu futuro yo.

■ **Pro tip:** Cuando usted está en una entrevista, caminar el entrevistador a través del
diagrama de estructura de datos, nombre cada componente ( " cache " , "freqMap " ,
" minFreq " ), y explicar los invariantes *O(1)*.

-...

## 4. Cómo utilizar el blog en su resumen / Enlace In

1. **Blog Título** – *“La caché deLFU – El bueno, el malo”*
Términos de búsqueda: “LFU cache”, “LeetCode 460”, “entrevista de diseño del sistema”.
2. **Añada un enlace** – “Lea el artículo completo con el código: https://your‐blog.com/lfu‐cache‐blog”.
3. **Caso de exposición** – En la sección *Proyectos*, mencione:
*Aplicado un caché LFU de producción en Java, Python y C++ con operaciones O(1); resuelto LeetCode 460*.
4. **Keywords** – “O(1) time complexity”, “hash map”, “LinkedHashSet”, “OrderedDict”, “frequency‐based eviction”, “system design interview”.
5. **Carta Cover** – Destaca que usted abordó un problema *hard* LeetCode y que la solución es reutilizable en escenarios de caché en el mundo real (CDN, DB en memoria, etc.).

-...

#### TL;DR

Silencio Idioma Silencio Complejidad clave Silencio Cómo mostrarlo en una entrevista
Silencio...
TEN Java TENIDO `O(1)` Silencio Habla sobre los dos hash‐maps, `minFreq`, y desalojo a través de `LinkedHashSet`. Silencio
TENIDA Python Mención "defaultdict(OrderedDict)" y cómo mantiene orden LRU. Silencio
TENIDO C++ TENIDO `O(1)` TENIDO Uso `unordered_map` + `list` + mapa de iterador para eliminaciones O(1). Silencio

Implementarlo, agregue el código a su GitHub repo, y lo refiera en su
Sección LeetCode “Discuss” o “Interview Notes”.
Cuando los reclutadores detectan que usted ha dominado un caché O(1) LFU en varios idiomas, pensarán: *“Este ingeniero conoce tablas de hash, listas vinculadas y puede optimizar la producción”*