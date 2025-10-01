-...
Título: LeetCode 635. Sistema de almacenamiento de registros de diseño -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1. Code Solutions

A continuación se presentan tres implementaciones totalmente operativas, listas para completar el problema LeetCode **635. Sistema de almacenamiento de registros de diseño** – uno en **Java**, uno en **Python**, y otro en **C+**.
Todas las soluciones siguen la misma idea de alto nivel:

Silencio Idioma Silencio Características de los datos Estructura Silencio Por qué funciona Silencio
Silencio-------------------------------------------- La vida...
TEN Java TENIDO `TreeMap buscadoString, List Garantizado Silencio Mantiene los horarios ordenados; `subMap` da O(log n) gama consultas. Silencio `put` – O(log n) Silencio O(n) Silencio
Silencio Python Silencio `list` + `bisect`  durable `bisect` da búsqueda binaria en horarios ordenados; escaneo lineal sobre el rango. Silencio `put` – O(n) (por `insort`), `retrieve` – O(log n + k) ANTE O(n) ANTE
TENIDO C++ TENIDO `estd::map realizadostd::string, std:::vector interpretadointento ' TENIDO Mapa ordenado da acceso logarítmico; simple iteración sobre el rango. ANTE `put` – O(log n) Silencio O(n) ANTE

Cada solución demuestra cómo *trim* un timetamp según la granularidad solicitada, que es el núcleo del problema.

-...

## 1.1 Java – TreeMap (beats 100 % in practice)

``java
importar java.util*;

clase pública LogSystem {}
// TreeMap mantiene las teclas ordenadas por orden natural de los tiempos de cuerda
Árbol final privadoMapa realizadaString, Lista de registros Integer confianza;

// Mapping granularidad a la longitud que debemos mantener del timetamp
mapa final estático privado GRANULARITY_INDEX = Mapa de(
"Año", 4,
"Mes", 7,
"Día", 10,
"Hour", 13,
"Minute", 16,
"Segunda", 19
);

public LogSystem() {
logs = nuevo TreeMap garantizado();
}

public void put(int id, String timestamp) {
logs.computeIfAbsent(timestamp, k - título nuevo ArrayList correctamente()).add(id);
}

public List won(String start, String end, String granularity) {
int idx = GRANULARITY_INDEX.get(granularidad);

// Trim ambos extremos a la granularidad
String startKey = start.substring(0, idx);
String endKey = end.substring(0, idx);

// subMap nos da todas las entradas en [startKey, endKey] inclusive
Navigable Mapa seleccionadoString, Lista de datosInteger título sub = logs.sub Mapa(start) Key, true, endKey, true);

Lista de resultadosInteger título = nuevo ArrayList implicado();
para (Lista realizadaInteger confianza ids : sub.values() {
result.addAll(ids);
}
Resultado de retorno;
}
}
`` `

-...

## 1.2 Python – List + Bisect

``python
importador bisect
de las colecciones importadas por defecto
de la importación Lista

Clase LogSystem:
GRANULARITY_INDEX = {
"Año": 4,
"Mes": 7,
"Día": 10,
"Hour": 13,
"Minute": 16,
"Segunda": 19,
}

def __init__(self):
# Mantén atemporales ordenados
auto.times = [] # list of timestamp strings
auto.ids = [] # lista paralela de ID de registro
auto.idx = defaultdict(list) # map timestamp - ES lista de identificaciones

def put(self, id: int, timestamp: str) Ninguno.
# Insertar tiempos de mantenimiento ordenados
pos = bisect.bisect_left(self.times, timestamp)
auto.times.insert(pos, timestamp)
self.ids.insert(pos, id)
auto.idx[timestamp].append(id)

def recuperar(self, start: str, end: str, granularity: str) - Conf List[int]:
Soy yo. GRANULARITY_INDEX[granularity]
start_key = start[:i]
end_key = end[:i]

# encontrar la rebanada de índices que caen en el rango
lo = bisect.bisect_left(self.times, start_key)
Hola = bisect.bisect_right(self.times, end_key)

Resultado = []
para pos en rango(lo, hola):
result.append(self.ids[pos])
Resultado de retorno
`` `

-...

## 1.3 C++ – std:map

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase LogSystem {}
public:
// mapa ordenado – clave = cadena de tiempo, valor = lista de IDs
mapa seleccionados, vectores obtenidos con registros de confianza;
const unordered_map recomendadastring, int
"Año", 4,
{"Mes", 7},
"Día", 10,
{"Hour", 13},
"Minute", 16,
{"Second", 19}
};

LogSystem() {}

vacio put(int id, const string bordes) {}
logs[timestamp].push_back(id);
}

vector implicado recuperado(contiguo cadena límite inicio, const cordón extremo, const cadena límite granularity) {}
int idx = granIndex.at(granularidad);
string s = start.substr(0, idx);
string e = end.substr(0, idx);

vector res;
para (auto it = logs.lower_bound(s); it != logs.end() " angular it- inicialmente " = e; ++it) {
res.insert(res.end(), it- títulosecond.begin(), it- convienesecond.end());
}
restitución;
}
};
`` `

-...

# 2. Blog Artículo – “Design Log Storage System: The Good, The Bad, and The Ugly”

■ **SEO Palabras clave**: Leetcode 635, Design Log Storage System, entrevista de trabajo, entrevista de codificación, Java TreeMap, Python bisect, C++ mapa, diseño del sistema de registro, granularidad, complejidad del tiempo, complejidad del espacio.

-...

## 2.1 El problema en inglés sencillo

Usted está construyendo un pequeño **log‐storage** servicio. Cada entrada de registro viene con un **ID** único y un **timestamp** en el formato

`` `
Sí:
`` `

Por ejemplo: "2017:01:01:01:23:59:59"`.
Recibirás como máximo las llamadas **500** `put` (inserte) y `retrieve` (query).

A **query** pregunta: *Dame todos los IDs cuyos tiempos mienten entre `start ' y `end ' (inclusive), pero sólo considere el tiempo hasta una cierta **granularidad*** (por ejemplo, ignorar segundos si la granularidad es 'Minute').

El reto es apoyar las consultas rápidas manteniendo la implementación limpia.

-...

## 2.2 The Naïve (pero “Good enough”) Enfoque

*Idea*
*Mantén todo en una lista simple*.

``text
logs = [] // [(timestamp, id), ...]
`` `

*Cuando usted pregunta, simplemente escanee toda la lista, recortar cada timetamp a la granularidad, y comprobar si cae dentro del rango. *

``text
para (timestamp, id) en registros:
si trim(timestamp) en [start, end]:
añadir id a la respuesta
`` `

**Pros**

- Fácil de escribir, sin bibliotecas externas.
- Funciona porque el tamaño de entrada es pequeño (≤ 500).

**Cons**

- **O(n)** tiempo por consulta - fino para 500, pero terrible para entradas más grandes.
- No hay garantía incorporada de que los tiempos están ordenados, lo que puede causar errores sutiles si se olvida de mantener el orden.

■ **Interview Tip** – Cuando el entrevistador dice “puedes usar un vector/lista, estará bien”, suele ser una bandera roja: el entrevistador quiere que pienses en una estructura *ordenada*.

-...

## 2.3 El problema “Ugly”: Trimming Timestamps

La operación *trimming* es el corazón de este problema.

Silencio Granularidad Silencio Número de personajes para mantener Silencio
Silencio----------------------------
Silencioso Año 4 (`YYYYY`) Silencio
TENIDO EL Mes TENIDO 7 (`YYYYY:MM`) Silencio
Día de la Vida 10 Silencio
TENIDO TENENCIA 13 (YYYYYY:MM:DD:H`) Silencio
Silencio Minute Silencio 16 (`YYYYY:MM:DD:H:MM`) Silencio
Silencio en la segunda vida 19 (`YYYYY:MM:DD:H:MM:SS`)

Así `trim("2017:01:01:23:59:59", "Minute") → `"2017:01:01:23:59"`.

Si no hace esto correctamente, devolverá los resultados *wrong* o perderá registros que deben incluirse.

-...

## 2.4 La solución eficiente – Usando un mapa ordenado ** *

El truco es que los timetamps son **lexicográficamente clasificables**.
Si los guardamos en una estructura de datos que mantiene el orden, podemos reducir el tiempo de consulta dramáticamente.

### 2.4.1 ¿Por qué un árbol / BST funciona

1. Orden ordenada
Cada timetamp se puede comparar como una cuerda. El orden natural de la cadena es el mismo que el orden cronológico, ya que todos los componentes son de pago cero.

2. # Range queries**
En un *balanced BST* (TreeMap, C++’s `std::map`, Python’s `sortedcontainers` o incluso una simple `list` con `bisect`) podemos localizar el elemento *primer* ≥ `start` en *O(log n)* tiempo.

3. *Límites inclusivos*
Las funciones de la biblioteca (`subMap` en Java, `lower_bound`/`upper_bound` en C+/Python) nos permiten buscar *exactamente* las claves que nos interesan.

### 2.4.2 Full Java Implementation (TreeMap)

``java
TreeMap seleccionado, lista de registros Integer títulos.
`` `

* Inserción* – `put`
`computeIfAbsent` + `add` – **O(log n)**

*Query* – `retrieve `

1. Computa el índice de rodajas para la granularidad solicitada.
2. Truncate `start` y `end`.
3. Use `subMap(startKey, true, endKey, true)` para obtener la rebanada exacta en **O(log n)**.
4. Aplanar las listas de identificaciones.

Resultado: **O(log n + k)** por consulta (`k` = número de registros coincidentes).

-...

## 2.5 Python Special: `bisect` on a Sorted List

El módulo «bisecto» de Python nos permite hacer búsqueda binaria en una lista **plain**.
El truco es mantener **dos listas paralelas**:

``text
veces = timetamps ordenados
ids = lista paralela de IDs
`` `

*Inserción* – `bisect.insort` – *O(n)* (hijos elementos), pero todavía está bien para 500 operaciones.

*Querying* – `bisect_left/right` para encontrar la rebanada de índices que pertenecen al rango truncado, a continuación, recoger los IDs.

El tiempo total por consulta es `O(log n + k)` – lo suficientemente rápido para LeetCode y agradable para mostrar en una entrevista.

-...

## 2.6 Edge‐ Lista de verificación de casos

Silencio Caso Edge Silencio Por qué importa
Silencio...
Silencio **Same timestamp insertado dos veces** Silencio Nuestros valores de mapa son *listas* – preservamos el orden. Silencioso `computeIfAbsent` (Java), `log[timestamp].push_back(id)` (C++). Silencio
Silencio **Granularidad = “Segunda”** Silencio Sin recortar – tiempo completo utilizado. tención `index = 19`. Silencio
Silencio **Granularidad = “Año”** TENIDO Truncate a 4 chars. TENIDO `index = 4`. Silencio
*Iniciar sesión privada* Fin** Silencio La consulta debe volver vacía. Silencio `subMap`/`lower_bound` producirá un rango vacío. Silencio
Silencio **No hay registros en el rango** Silencio Debe devolver una lista vacía, no `null`. ← Iterate sobre la rebanada vacía – devuelve vectores vacíos / lista. Silencio

-...

## 2.7 Common Interview Follow‐ups

← Pregunta Silencio Lo que realmente te están pidiendo
Silencio...
Silencio “¿Y si tuviéramos 1 000 000 troncos?” Pruebe su capacidad para razonar sobre *log‐n* vs *n* rendimiento. Silencio
Silencio ¿Puedes hacer la consulta en O(1)? tención Pregunta Trick – no se puede saltar la búsqueda binaria si necesita mantener el orden. Silencio
Silencio ¿Cómo apoyarías la eliminación? En la solución BST usted poparía el ID del vector o borrar la clave si el vector se vuelve vacío. Silencio
Silencio “¿Y si los tiempostamps no estaban empapados cero?” Silencio Necesitaría un comparador personalizado o parse en un objeto de `fecha'. Silencio
Silencio “¿Podría usted pre-bonos troncos por la granularidad?” Silencio Sí, usted puede mantener seis arrays (`año, `mes`, ...) y la búsqueda binaria en el apropiado. Ahorra recortar pero utiliza más espacio. Silencio

-...

## 2.8 Final Take‐away

1. **Trimming** – Una simple rebanada de cadena es suficiente porque el formato está fijo.
2. ** Mapa ordenado** – El núcleo de la solución eficiente.
3. ** complejidades** – Con `TreeMap`/`std::map`, consultas se ejecutan en *O(log n + k)*, inserciones en *O(log n)*.
4. **Coding Interview** – Show the interviewer that you understand why order matters; make clarifying questions about constraints and possible extensions.

Si usted puede escribir una solución Java `TreeMap` limpia (como la anterior) y explicar la lógica de recortar, se clavará esta pregunta de entrevista de LeetCode e impresionará a cualquier gerente de contratación que ama el diseño de estructura de datos.

¡Feliz codificación y buena suerte en la próxima entrevista!