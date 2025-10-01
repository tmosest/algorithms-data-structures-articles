-...
Título: LeetCode 715. Módulo de rango -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 715 – **Range Module**
**Hard Silencio 104 operations Silencio 109 range* *
**LeetCode**: " ** https://leetcode.com/problems/range-module/ "

■ Un `RangeModule` rastrea un conjunto de intervalos medio abiertos \([l,r)\).
■
* `addRange(l,r)` – añadir un intervalo, fusionarse con los existentes.
* " queryRange(l,r) " - devolver `true ' si el intervalo entero está actualmente cubierto.
* `removeRange(l,r)` – eliminar el intervalo del conjunto rastreado.

A continuación encontrará tres soluciones limpias y de producción – **Java (TreeMap)**, **Python (bisect + lista clasificada)**, **C++ (std::map)** – cada uno con O(log n) tiempo por operación.
Después del código, lea el artículo de blog amigable de SEO que explica *el bueno, el malo, y el feo* de este problema, cómo se utiliza a menudo en entrevistas técnicas, y por qué dominarlo puede aumentar sus perspectivas de trabajo.

-...

## 1. Java – TreeMap (Fast, Easy to Understanding)

``java
importar java.util*;

clase pública RangeModule {}
/** clave = inicio, valor = final (exclusivo) */
Árbol final privadoMapa realizadaInteger, Integer contactos = nuevo TreeMap fiel();

public RangeModule() {}

* Add [l, r) */
public void addRange(int l, int r) {}
// Encontrar el intervalo de superposición más izquierdo
Mapa.Introducción realizadaInteger, Integer título izquierda = ranges.floorIntry(l);
si (izquierda!= null " izquierdo.getValue()  Conf= l) l = left.getKey();

// Encontrar el intervalo de superposición más adecuado
Mapa.Introducción realizadaInteger, Integer derecha = ranges.floorIntry(r);
si (derecha != null " derecha.getValue() √≥ r = right.getValue();

// Quitar todos los rangos completamente superpuestos
ranges.subMap(l, r).clear();

// Insertar el intervalo fusionado
ranges.put(l, r);
}

* Retorno verdadero si [l, r) está completamente cubierto */
public boolean queryRange(int l, int r) {}
Mapa.Introducción realizadaInteger, Integer título izquierda = ranges.floorIntry(l);
volver a la izquierda!= null " izquierda.getValue() √= r;
}

/** Remove [l, r) */
vacío público eliminar Range(int l, int r) {}
Mapa.Introducción realizadaInteger, Integer título izquierda = ranges.floorIntry(l);
si (izquierda!= null " izquierdo.getValue() √≥ l) {}
ranges.put(left.getKey(), l); // mantener el lado izquierdo
}

Mapa.Introducción realizadaInteger, Integer derecha = ranges.floorIntry(r);
si (derecha!= null " derecha.getValue()  Confía r) {}
ranges.put(r, right.getValue()); // mantener el lado derecho
}

// Borrar todos los rangos que caen dentro [l, r)
ranges.subMap(l, r).clear();
}
}
`` `

¿Por qué TreeMap?
- Mantiene intervalos ordenados por punto de partida.
- `floorEntry` da la mayor clave ≤ objetivo, haciendo cheques de solapamiento O(log n).
- `subMap` permite la eliminación masiva de todos los intervalos completamente superpuestos.

-...

## 2. Python – SortedList + bisect

``python
importador bisect
de la importación Lista

clase RangeModule:
def __init__(self):
self.starts: List[int] = [] # puntos de inicio
self.ends: List[int] = [] # end points (exclusive)

def _find_left(self, x: int) - título int:
""Indice de la mayoría i tal que comienza[i] "Según"
i = bisect.bisect_right(self.starts, x) - 1
Regreso

def addRange(self, left: int, right: int) Ninguno.
i = self._find_left(left)
si yo >= 0 y auto.ends[i] >= izquierda:
izquierda = self.starts[i]
j = self._find_left(right)
si j >= 0 y self.ends[j]
right = self.ends[j]

# Eliminar intervalos superpuestos
del self.starts[max(0, i+1):j+1]
del self.ends[max(0, i+1):j+1]

# Insert merged interval
pos = bisect.bisect_left(self.starts, left)
self.starts.insert(pos, left)
self.ends.insert(pos, right)

def queryRange(self, left: int, right: int) Bool:
i = self._find_left(left)
devolver i >= 0 y self.ends[i] >= derecho

def quitar Range(self, left: int, right: int) - Ninguno.
i = self._find_left(left)
si yo >= 0 y auto.ends[i] √≥n dejado:
self.ends[i] = left # truncate left part

j = self._find_left(right)
si j >= 0 y self.ends[j]
# Insertar un nuevo intervalo para la parte correcta
pos = bisect.bisect_left(self.starts, right)
self.starts.insert(pos, right)
self.ends.insert(pos, self.ends[j])
self.ends[j] = right

# Eliminar intervalos completamente superpuestos
del self.starts[max(0, i+1):j+1]
del self.ends[max(0, i+1):j+1]
`` `

**¿Por qué galletas + listas? * *
- El 'bisecto' de Python da O(log n) búsqueda.
- Dos listas paralelas mantienen pares de inicio/fin, haciendo la huella de memoria pequeña.
- Todas las modificaciones permanecen O(log n) más O(k) para eliminar los intervalos de superposición de 'k' (k ≤ n).

-...

## 3. C++ – `std::map` (contenedor asociativo ordenado)

``cpp
#include >

clase RangeModule {}
std::map madeint, int confianza mp; // key = start, value = end (exclusive)

public:
RangeModule() {}

vacío addRange(int left, int right) {
auto = mp.lower_bound(left);
si (lo != mp.begin()) {}
auto prev = std::prev(it);
si (prev-jósegundo >= izquierda) izquierda = prev- primero;
}
mientras (¡eso!= mp.end() " clérigo- primero " ) {
derecha = std::max(derecha, it-Consegundo);
it = mp.erase(it);
}
mp.emplace(izquierda, derecha);
}

bool queryRange(int left, int right) {
auto = mp.upper_bound(left);
si (it == mp.begin()) devuelve falso;
-it;
devolverlo. derecho;
}

vacío Rango(int left, int right) {
auto = mp.lower_bound(left);
si (lo != mp.begin()) {}
auto prev = std::prev(it);
si (prev- confíasecond > left) {
int old_end = prev- tituladosecond;
prev-tio segundo = izquierda;
si (old_end ≤ derecho) {
mp.emplace(right, old_end);
}
}
}
mientras (¡eso!= mp.end() " clérigo- primero " ) {
si (es decir, segundo y derecho) {
mp.emplace(derecho, it-Consegundo);
}
it = mp.erase(it);
}
}
};
`` `

¿Por qué?
- Inserción logarítmica, eliminación y búsqueda.
- Sintaxis clara para la lógica de división / fusión.
- Funciona bien en entornos de programación competitivos.

-...

## 4. El Bien, el Mal, el Ugly

¿Qué es lo bueno que hay en la vida?
Silencio------------------------------------------------------------
Silencio ** Estructura de datos** Silencio Mapas ordenados mantienen intervalos ordenados → O(log n) operaciones Silencio Si utiliza una *lista* o *vector*, las operaciones se convierten en O(n) Silencio Evite los escaneos lineales ingenuos después de cada actualización.
tención **Merge logic** tención El enfoque simple “expand left/right” fusiona todos los rangos superpuestos en un solo paso Silencioso para manejar intervalos *adyacentes* (por ejemplo, `[1,3)` y `[3,5)`) → puede dejar las lagunas Silencio Siempre tratar los intervalos como *half‐open*
Silencio **Supresión** Silencio Split partes izquierda/derecha si existen → no datos perdidos ← Eliminar o olvidarse de mantener el fragmento correcto  Mantener la pista del final del intervalo original antes de borrar ←
Silencio **Memoria** Silencio Las tiendas de mapas sólo *disjoint* intervalos TEN Repetidas añadir/remove pueden fragmentar el mapa → muchas pequeñas gamas ¦ Merge agresivamente en `addRange` para mantener el tamaño mínimo
Silencio **La complejidad** Silencio Cada operación es *logarítmica* En el peor de los casos, la eliminación de muchos intervalos pequeños → O(k log n)
Silencio **Language quirks** Silencio Java TreeMap, C++ mapa, Python bisect TEN Java’s `subMap` devuelve una vista – debe llamar `clarar()`; La lista de Python rebanada de eliminación es O(k) Silencio Presta atención a las condiciones de límite (derecha exclusiva)

### El lado “Ugly”

- Casos de emergencia**:
- Añadiendo un rango que toque el final de uno existente.
- La eliminación de un rango que superpone parcialmente múltiples intervalos.
- Querying an empty set or range outside all intervals.

- Off-by-One
Puesto que los intervalos son *half‐open*, un rango `[10, 20)` incluye 10 pero excluye 20.
El tratamiento erróneo como cerrado puede llevar a errores sutiles.

- ¿Por qué?
Las implementaciones dadas son *no * seguros de rosca.
En un entorno multi-teleada necesitará cerraduras externas o un mapa concurrente.

-...

## 5. Por qué el módulo de control de distancia ayuda a su carrera

1. ** Frecuencia de Intervisión**
- *Range Module* es un elemento básico de las plataformas de contratación técnica (LeetCode, HackerRank, InterviewBit).
- Examina su capacidad para mantener un conjunto *dinámico* de intervalos – un problema clásico de estructura de datos.

2. *Templo conceptual*
- Practicarás:
* Mapas ordenados / BSTs balanceados* → conocimiento de estructura de datos básicos.
*Aritmética intervalida* → matemática + manutención del borde.
*Set operations (unión, intersección, diferencia)* → fundamental para muchos sistemas.

3. **Showcasing Problem‐Solving**
- Escribe una implementación clara y libre de errores en el idioma con el que estás cómodo.
- Explicar los cambios de tiempo en el espacio durante una entrevista; muestra profundidad de comprensión.

4. **Relevancia de producción**
- Muchos servicios del mundo real (p. ej., motores de características, sistemas de programación, reglas de cortafuegos de red) mantienen rangos de tiempos o bloques IP.
- Conocer este patrón le da confianza para contribuir inmediatamente a tales sistemas.

-...

## 5. SEO‐Friendly Blog Title " Esquema

*Título*
■ “Range Module – The Interview Power‐Up: 715 LeetCode Explained (Good, Bad & Ugly)”

**Meta Descripción**
■ Sumérgete en el problema “Range Module” (LeetCode #715). Aprenda tres soluciones de O(log n) en Java, Python y C+++, además de información de entrevistas sobre el manejo de las maletas y por qué dominar este problema puede conseguir un papel de ingeniería de software.

**Suggested Headings* *

1. **¿Cuál es el módulo de rango?** – Declaración de problemas " intervalos medio abiertos.
2. **Por qué este problema se plantea para las entrevistas** – Conjunto dinámico de intervalos, intervalos de tiempo-espacio.
3. **Tres implementaciones de producción-Ley** – Java, Python, C++ (bloqueos de código).
4. **El Bien** – Mapas ordenados, operaciones logarítmicas, lógica clara de separación.
5. **El mal** – Casos de borde, errores fuera por uno, fragmentación.
6. **El Ugly** – Intervalos adyacentes, seguridad de los hilos, fragmentación a gran escala.
7. ** Errores comunes para evitar** – Lista de verificación Pseudocode, pruebas de límites.
8. **Más allá del problema** – Aplicar lógica de intervalos para programar, caching, reglas de cortafuegos.
9. **Entrevisar consejos de éxito** – Cómo explicar su solución, discusiones de intercambio, manejo de preguntas de seguimiento.
10. **Conclusión > Siguientes pasos** – Otros problemas (Merge Intervals, 315 – Conde de números más pequeños, 720 – Word más larga en Diccionario) y recursos.

-...

#### Takeaway

Mastering **Range Module** significa que puede:

- Escriba código eficiente y libre de errores para problemas de intervalo dinámico.
- Distinciones de articulado entre diferentes idiomas y estructuras de datos.
- Resolver un problema clásico de entrevista que prueba tanto el conocimiento de la estructura de datos como el razonamiento cuidadoso sobre casos de borde.

Dar a las soluciones un intento, correr a través de un puñado de pruebas al azar, y sentir la confianza que viene de ser *pro-fesional* en los rangos de gestión. ¡Feliz codificación y buena suerte en tu próxima entrevista!