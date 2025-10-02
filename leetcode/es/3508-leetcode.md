-...
Título: LeetCode 3508.
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## ✅ 3508 – Implement Router
**Solución en Java Silencio en Python
**Blog post** – El bueno, el malo, el ugly – una guía completa, amigable del SEO

-...

### 1. Recaptación de problemas

Usted está construyendo un pequeño router en memoria que debe mantener al máximo ** `memoryLimit`** paquetes.
Los paquetes tienen un *fuente*, *destinación* y *tiempo*.

Silencio Operación Silencioso Descripción
Silencio----------------------------------------
Silencio `addPacket(s,d,t)` Silencio Añadir un paquete si es **no** un duplicado. Si el router está lleno el paquete **antiguo** es desalojado primero. Silencioso
Silencioso `forwardPacket()` Silencio Retire y devuelva el paquete **antiguo** (FIFO). Silencio `[s,d,t]` o `[]
Silencio `getCount(d, start, end)` ¿Cuántos paquetes todavía están en el router que tienen `d` destino y timetamps en `[start,end]`? Silencio integer Silencio

**Constraints* *

* `2 ≤ memoriaLimit ≤ 105 `
* `1 ≤ source, destination ≤ 2·105 `
* `1 ≤ vecestamp ≤ 109 `
* llamadas `addPacket` son ** ordenadas cronológicamente** (timestamp nunca disminuye)

-...

## 2. Data‐Structure Design

Silencio necesitado Lo que usamos para sobrevivir
Silencio--------------------------
Silencio **FIFO queue** Silencio `LinkedList` / `deque` / `queue logróarray `` Silencio Almacenar los paquetes en orden de llegada para que podamos pop el más antiguo en O(1). Silencio
Silencio **Detección Duplicada** Silencio `HashSet` de una clave de 64 bits TEN O(1) insertar / buscar duplicados. Silencio
Silencio **Counto en el rango de tiempo** Silencio Para cada destino una lista ordenada de timetamps ← Tiempos de llegada en orden creciente, la lista ya está clasificada. Silencio
Silencio **Efficient range query** Silencio Binary search (`lower_bound` / `upper_bound`) en la lista de destino Silencio O(log N) por consulta. Silencio
Silencio **Mantén la pista de los timetamps eliminados** Silencio Per‐destination pointer `removedIdx` Silencio Después de que un paquete es enviado o desalojado, ya no queremos contar su timetamp. El puntero nos dice de qué índice comienzan los tiempos *activos*. Silencio

Con estas opciones cada operación se ejecuta en **O(1)** o **O(log N)** tiempo y el uso de la memoria permanece dentro del límite.

-...

## 3. Aplicación

A continuación se encuentran soluciones limpias y de producción en **Java, Python y C++**.
Los tres comparten la misma lógica – sólo la sintaxis cambia.

-...

### 3.1 Java

``java
importar java.util*;

*
* 3508. Router de ejecución
*/
clase pública Router {
memoria de entrada privadaLimit;
final privado queue; // FIFO cola
Conjunto final privado ajustado a los duplicados de Long confianza; // para detección duplicada
mapa final privado realizadoInteger, Lista de resultadosInteger confianza destTs; // dest - lista de precios
mapa final privado realizadoInteger, Integer confianza removedIdx; // dest #removed

public Router(int memoryLimit) {
este.memoryLimit = memoriaLimit;
este.queue = nuevo ArrayDeque quiere decir();
este.duplicados = nuevo HashSet fiel();
este.destTs = nuevo HashMap correctamente();
este.removedIdx = nuevo HashMap incorrecto();
}

/** Construir una llave única de 64 bits para un paquete */
fabricante privado largoKey(en fuente, destino int, int timestamp) {
// origen > destino >
((long) source) ANTERIEDAD 40) TENIDO (((long) destino)
}

public boolean addPacket(int source, int destination, int timestamp) {
tecla larga = hacer Key(source, destination, timestamp);
si (duplicados.contains(key)) devolver falso; // duplicado

// si el router está lleno, desaloje el paquete más antiguo primero
si (queue.size() == memoriaLimit) {
int[] evicted = queue.pollFirst();
duplicates.remove(makeKey(evicted[0], evicted[1], evicted[2]));
removedIdxFor(evicted[1])++; // marca ts como eliminado
}

// enqueue el nuevo paquete
int[] pkt = nuevo int[]{source, destination, timestamp};
queue.addLast(pkt);
duplicates.add(key);

// mantener el horario para el destino
destTs.computeIfAbsent(destinación, k - título nuevo ArrayList recomendado()).add(timestamp);
retorno verdadero;
}

int[] forwardPacket() {
si (queue.isEmpty()) devuelve nuevo int[0];
int[] pkt = queue.pollFirst();
duplicates.remove(makeKey(pkt[0], pkt[1], pkt[2]));
removedIdxFor(pkt[1])++; // paquete ya no está activo
retorno pkt;
}

public int getCount(int destination, int startTime, int endTime) {
Lista de títulos = destTs.get(destinación);
si (lista == null) devuelve 0;

int startIdx = removedIdxFor(destinación);
// búsqueda binaria en el sufijo activo de la lista
int l = lowerBound(list, startIdx, startTime);
int r = upperBound(list, startIdx, endTime);
retorno r - l;
}

Ayudantes...

/** búsqueda binaria para el primer índice valor */
int private int lowerBound(Lista seleccionadaInteger título, int offset, int value) {
int lo = offset, hi = list.size();
mientras (lo cautivado) {
int mid = (lo + hola) 1;
si (list.get(mid) valuado) lo = medio + 1;
más hola = medio;
}
devolver lo;
}

/** búsqueda binaria del primer índice valor */
int privado superiorBound(Lista seleccionadaInteger título, int offset, int value) {
int lo = offset, hi = list.size();
mientras (lo cautivado) {
int mid = (lo + hola) 1;
si (list.get(mid) <= valor) lo = medio + 1;
más hola = medio;
}
devolver lo;
}

/** obtener o inicializar índice eliminado para un destino */
int private int removedIdxFor(int destination) {
volver removedIdx.computeIfAbsent(destinación, k - 0);
}

mapa final privado realizadoInteger, Integer confianza removedIdx = nuevo HashMap fiel();
}
`` `

■ *Por qué esto es genial* *
* Todas las búsquedas/inserciones son **O(1)**.
* `getCount` is **O(log N)** gracias a la búsqueda binaria.
* Usa sólo clases JDK estándar – no se necesitan bibliotecas externas.

-...

#### 3.2 Python 3

``python
#!/usr/bin/env python3
"
3508. Implement Router
"

de las colecciones importa
de la importación de bisect_left, bisect_right
de la importación Listo, Deque, Set, Dict

clase Router:
def __init__(self, memoryLimit: int):
auto.memory_limit = memoriaLimit
autor.queue: Deque[List[int]] = deque() # FIFO
auto.duplicados: Set[int] = set() # 64‐bit key
auto.dest_ts: Dict[int, List[int] = {} # dest - título timetamps
auto.removido: Dict [int, int] = {} # dest - #removed

def _key(self, s: int, d: int, t: int) int:
# source > 2^18, dest > 2^18, t > 2^30 → encaja en 64 bits
retorno (s.

def addPacket(self, source: int, destination: int, timestamp: int) Bool:
key = self._key(source, destination, timestamp)
si la llave en uno mismo. duplicados:
Retorno Falso

si len(self.queue) == self.memory_limit:
desalojado = auto.queue.popleft()
ev_key = self._key(*evicted)
auto.duplicados.remove(ev_key)
self.removed[evicted[1]] = self.removed.get(evicted[1], 0) + 1

self.queue.append([source, destination, timestamp])
auto.duplicados.add(key)
auto.dest_ts.setdefault(destinación, []).append(timestamp)
Retorno

def forwardPacket(self) - Propiedad List[int]:
si no yo. cola:
retorno []
pkt = self.queue.popleft()
auto.duplicates.remove(self._key(*pkt))
auto.removed[pkt[1]] = self.removed.get(pkt[1], 0) + 1
retorno pkt

def getCount(self, destination: int, startTime: int, endTime: int) - título int:
si destino no en sí mismo. Dest_ts:
retorno 0
ts = self.dest_ts[destination]
start_idx = self.removed.get(destinación, 0)
izquierda = bisect_left(ts, startTime, lo=start_idx)
derecha = bisect_right(ts, endTime, lo=start_idx)
retorno a la derecha - izquierda
`` `

■ * Notas de pitón*
* Usa `deque` para O(1) pop desde la izquierda.
* `bisect` da búsqueda binaria en la rebanada *activa* de la lista de timetamp.

-...

### 3.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

*
* 3508. Router de ejecución
*/
clase Router {
public:
Router(int memoryLimit) : MemoryLimit(memoryLimit) {}

bool addPacket(int source, int destination, int timestamp) {
tecla larga largo = hacer Key(source, destination, timestamp);
si (dup.count(key)) devolver falso; // duplicado

si (int)q.size() == MemoryLimit) { // evict older
auto ev = q.front(); q.pop();
dup.erase (makeKey(ev[0], ev[1], ev[2]);
[ev[1]]+;
}

int pkt[3] = {source, destination, timestamp};
q.emplace(pkt[0], pkt[1], pkt[2]);
dup.insert(key);
destTs[destination].push_back(timestamp);
retorno verdadero;
}

vector asignado injerto() {
(q.empty()) return {};
auto pkt = q.front(); q.pop();
dup.erase(makeKey(pkt[0], pkt[1], pkt[2]));
[pkt[1]]++;
devolver {pkt[0], pkt[1], pkt[2]};
}

int getCount(un destino, int startTime, int endTime) {
auto = destTs.find(destinación);
si (it == destTs.end()) devuelve 0;

const vector identificadointento &vec = it- segundos;
int start Idx = eliminado[destinación]; // primera ts activa
auto izquierda = inferior_bound(vec.begin() + startIdx, vec.end(), startTime);
auto derecho = superior_bound(vec.begin() + startIdx, vec.end(), endTime);
volver estática_cast seleccionado(derecha - izquierda);
}

privado:
memoria int Límite;
queue realizaronarrayo realizado, 3 títulos q; // FIFO
unordered_set obtenidos largamente larga confianza dup; // duplicar teclas
unordered_map madeint, vector autorizadoint títulos destTs; // dest timetamps
unordered_map madeint, int confianza removed; // dest - confianza #removed

hace mucho tiempo Key(int s, int d, int t) const {
retorno (static_cast seleccionado largo(s)
(static_cast seleccionado largo(d)
static_cast realizado largo largo(t);
}
};
`` `

■ ** Notas C++**
> > > > mantiene un paquete de tamaño fijo en la cola.
* "lower_bound "/ "upper_bound " en un "vector fielint " , dar el mismo desempeño O(log N) que la versión Python.

-...

## 4. Análisis de la complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio `addPacket` Silencio **O(1)** (hash‐set lookup + possible pop) Silencio O(1) extra por paquete Silencio
Silencioso `forwardPacket` Silencio **O(1)** Silencio O(1)
Silencio `getCount` Silencio **O(log M)** donde *M* es el número de paquetes *activos* para ese destino

El consumo total de memoria es lineal en el número de paquetes en el router (limitado por `memoryLimit`).

-...

## 5. Las partes “buenas” y “malas” – Una mirada rápida

- Bien.
* Uso de memoria lineal determinista – sin fugas accidentales.
* Todas las estructuras de datos se construyen desde la biblioteca estándar.
* La búsqueda binaria en los tiempos ignora elegantemente los paquetes desalojados a través de `removedIdx`.
* La llave única de 64 bits garantiza no colisión de hash (con probabilidad 1).

- *Potential pitfalls*
* Si usas un hash-set de 32 bits en Python/Java y olvidas empacar la llave, las colisiones pueden causar falsos negativos.
* Las listas de timetamp guardan *todas* timetamps, incluso eliminadas – en casos patológicos puede tener una lista muy grande pero `removed` mantiene la rebanada correcta; esto está bien, pero debe recordar recortarlas si desea liberar la memoria (no es necesario para las restricciones del problema).
* El enfoque asume las limitaciones (fuente, dest, time) encajan en 64 bits – que sostienen para la declaración del problema.

-...

## 5. “El Bien” y “El Mal” – Un resumen rápido

Silencio **Lo que es bueno ** Por qué importa**
Silencio.
Silencio O(1) `addPacket`/`forwardPacket` Silencio Hace la solución rápida incluso para 105 operaciones. Silencio
Silencio O(log N) `getCount` Silencio Escalas a muchos destinos distintos. Silencio
Silencio No hay bibliotecas externas ← Easier para enviar a LeetCode / plataformas de entrevista. Silencio
TEN 64‐bit clave codificación ANTE Garantías única identificación de paquetes con un simple truco bit-shift. Silencio

¿Qué hay que cuidar?
Silencio...
Silencio Desahuciando accidentalmente el paquete equivocado Silencio Mantener la generación clave consistente en todas partes. Silencio
Silencio Olvídate de actualizar `removido` después del desalojo tención Siempre aumenta `removed[destination]` cuando un paquete se vuelve inactivo. Silencio
← Malusing bisect offsets in Python ← Utilizar el argumento `lo=` para restringir la búsqueda al sufijo activo. Silencio

-...

## 6. Tomado para su próxima entrevista

- **Bit-shift encoding** es un poderoso truco para generar un identificador único de múltiples pequeños enteros.
- ** Hash‐sets** le dan cheques duplicados de tiempo constante.
- **Deques** (o `ArrayDeque` / `ArrayDeque` en Java) le dan operaciones de cola eficientes.
- **Binary search on sections** (via `bisect` or `lower_bound`) le permite preguntar una lista ordenada mientras ignora los elementos "inactivos".
- **Mapping per-destination data** mantiene `getCount` eficiente incluso cuando el router contiene muchos paquetes.

Esta solución demuestra código limpio, estructuras de datos eficientes y un manejo cuidadoso de casos de borde – exactamente lo que buscan los reclutadores en una entrevista de algoritmo.

-...

## 5.1 Final Checklist

- ✅ Todas las funciones son públicas (LeetCode signature).
- ✅ Usa sólo contenedores de biblioteca estándar.
- ✅ Maneja la lógica "evict on full" correctamente.
- TENIENDO Marcar correctamente los horarios como removidos cuando los paquetes salen del router.
- ✅ `getCount` trabaja en el sufijo *activo* de la lista de timetamp.
- TENIENDO 64 bit generación clave evita colisiones dadas las entradas.

¡Feliz codificación y buena suerte en LeetCode y futuras entrevistas!