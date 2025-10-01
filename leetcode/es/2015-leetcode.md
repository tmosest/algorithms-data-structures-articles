-...
Título: LeetCode 2015. Altura promedio de edificios en cada segmento -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 “Altura promedio de edificios en cada segmento” – La guía completa
*(Java / Python / C++ implementaciones + un blog SEO-friendly)*

-...

#### TL;DR

Silencio Idioma Silencio Complejidad Silencio
Silencio--------------------------
Silencio **Java** TENIDO O(n log n) time, O(n) space TEN Sweep‐line + `TreeMap` ANTE
Silencio **Python** Silencio O(n log n) time, O(n) space Silencio Sweep‐line + lista ordenada Silencio
TENIDO **C+** TENIDO O(n log n) time, O(n) space

Barremos la calle de izquierda a derecha, manteniendo la altura total *sum* y el número de edificios activos *cnt*.
En cada punto de evento (un comienzo o fin del edificio) recalculamos la altura media.
Si los cambios promedio cerramos el segmento anterior y empezamos uno nuevo.
Los segmentos sin edificios (promedio = 0) nunca se añaden.

-...

Problema Recap

Una calle es una línea número.
`buildings[i] = [start_i, end_i, height_i]` - un edificio ocupa `[start_i, end_i)` y tiene altura `height_i`.

# Objetivo #
Devuelve la lista de segmentos no superpuestos semicerrados `[izquierda, derecha)` junto con la altura promedio entero de todos los edificios que cubren ese segmento.
El promedio es "sum(heights) // count" (división entero).
Los segmentos con promedio = 0 (sin edificio) deben ser omitidos.
Los segmentos con el mismo promedio y tocándose entre sí deben ser fusionados.

El tamaño de entrada es de hasta 105 edificios, coordenadas hasta 108, alturas hasta 105.

-...

## 2down The The Core Idea – Sweep Line

1. **Eventos** – Para cada edificio crear dos eventos:
* `(start, +height, +1)` – un edificio comienza.
Un edificio termina.

2. **Ordenar** los acontecimientos por su coordinación.
Si varios eventos comparten la misma coordinación, procesarlos *juntos* – de lo contrario dividiríamos un segmento que debería permanecer continuo.

3. **Mantén el estado** mientras explora los eventos ordenados:

* `sum` – altura total de todos los edificios activos (necesidades 64-bit).
* " cnt " - número de edificios activos.
* `prevCoord` – inicio del segmento actual.
* `prevAvg` - altura media del segmento actual.

4. *En cada coordenadas*
* Actualizar `sum ' y `cnt ' con *todos* eventos en esta coordinación.
* Compute `newAvg = cnt œ 0 ? suma / cnt : 0`.
* If `newAvg != prevAvg` *y* 0` → añadir `[prevCoord, coord, prevAvg]` a la respuesta.
* Set `prevCoord = coord` and `prevAvg = newAvg`.

5. **Finish** – El bucle cierra automáticamente cada segmento; nunca necesitamos un paso especial post-procesamiento.

¿Por qué se fusionan segmentos adyacentes de igual media?
Porque sólo creamos un nuevo segmento cuando el promedio cambia en realidad.
Si el promedio permanece igual en un punto de evento (por ejemplo, un edificio termina pero otro con la misma altura comienza), `prevAvg == newAvg` → no segment split.

-...

## 3down Ed Edge‐ Casos " Pitfalls

Silencio Pitfall Silencio Lo que pasó mal
Silencio...
Silencio ** Eventos obligatorios en la misma coordinación** Silencio Segmentos divididos innecesariamente Silencio Grupo sucesos por coordenadas antes de actualizar el estado
Silencio **División por cero** 0` cuando no hay edificio Silencioso Guardia: `cnt  título 0 ? sum / cnt : 0` Silencio
Silencio **Large sums** Silenciosos 105 edificios × 105 altura = 1010 → rebosamiento 32-bit tención Uso 64-bit (`long` / `int64_t`) para `sum` Silencio
Silencio ** calle vacía** Silencio Todos los segmentos promedio = 0 → salida vacía Silencio Skip segments when `prevAvg == 0. Silencio
Silencio **Requisito de la fusión** ← segmentos de la igualdad de mediación Adjacent no fusionados Silencio Sólo dividido en cambio promedio Silencio

-...

Código completo – Java

``java
importar java.util*;

Solución de la clase pública {}
int[][] promedioAlturaDeconstrucción(int[][] [edificios] {}
// Evento: [coordinado, deltaHeight, deltaCount]
Lista obtenida[] acontecimientos relativos = nuevo ArrayList correctamente(buildings.length * 2);
para (int[] b : edificios) {}
sucesos.add(new int[]{b[0], b[2], 1}); // start
sucesos.add(new int[]{b[1], -b[2], -1}); // end
}

// ordenar por coordenadas
events.sort(Comparator.comparingInt(a - título a[0]));

larga suma = 0; // altura total (64-bit)
int cnt = 0; // cuenta de edificio activo
int prev = events.get(0)[0]; // first event coordinate
int prevAvg = 0; // promedio anterior
Lista hecha[]]] > > > >

int i = 0;
mientras (i  0 eventos.size())) {}
int coord = events.get(i)[0];

// ---- procesar todos los eventos en esta coordinación...
mientras (i) se realizaron eventos.size() " afectadas events.get(i)[0] == coord) {
sum += events.get(i)[1];
cnt += events.get(i)[2];
i++;
}

int newAvg = cnt ≤ 0 ? (int)(sum / cnt) : 0;

// ---- cerrar segmento anterior si el promedio cambió...
si (newAvg != prevAvg " 0) {
ans.add(new int[]{prev, coord, prevAvg});
}

// ------ iniciar nuevo segmento--
prev = coord;
prevAvg = newAvg;
}

// ---- lista de conversión a array ----
int[][] res = nuevo int[ans.size()][];
para (int j = 0; j) j++) {
res[j] = ans.get(j);
}
restitución;
}
}
`` `

*Por qué es rápido*
*Sorting* toma `O(n log n)`; el escaneo en sí es lineal.
Memoria: un evento por edificio → `O(n)`.

-...

## 5down⃣ Full Code – Python

``python
de la importación Lista

Solución de clase:
def promedio AlturaDeconstrucción(auto, edificios: List[List[int]) - No. List[List[int]]:
sucesos = []
para s, e, h en edificios:
events.append(s, h, 1)) # start
events.append(e, -h, -1)) # end

events.sort() # sort by coordinate

sum_h = 0 # 64‐bit automáticamente en Python
cnt = 0
prev = events[0][0]
prev_avg = 0
ans = []

I = 0
n = len(events)
mientras que yo no
coord = events[i][0]
# agrega todos los eventos en esta coordinación
mientras que yo hice n y eventos[i] == coord:
sum_h += events[i][1]
cnt += eventos[i ][2]
i += 1

nuevo_avg = (sum_h // cnt) si cnt 0 si no 0

si nuevo_avg != prev_avg y prev_avg 0:
ans.append([prev, coord, prev_avg])

prev = coord
prev_avg = new_avg

Retorno
`` `

-...

## 6down⃣ Full Code – C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vectores obtenidos mediante: {}
// evento: {coordinado, deltaAltura, deltaCount}
vector asignadotuple realizado,int,int,int
ev.reserve(buildings.size() * 2);
para (auto &b : edificios) {}
ev.emplace_back(b[0], b[2], 1); // start
ev.emplace_back(b[1], -b[2], -1); // end
}

sort(ev.begin(), ev.end(),
[](auto const " a, auto const " b){ return get did0 título(a) " )

larga suma = 0; // altura total
int cnt = 0; // cuenta de edificio activo
int prev = get won0(ev[0]); // inicio del segmento actual
int prevAvg = 0;
vector realizador:

size_t i = 0;
mientras (i) {}
int coord = get won0(ev[i]);

// Actualización con todos los eventos en esta coordenadas
mientras (i) == coord) {
la suma += conseguir realizada1(ev[i]);
cnt += conseguir obtenidos2(ev[i]);
++i;
}

int newAvg = cnt ≤ 0 ? static_cast fielint(sum / cnt) : 0;

si (newAvg != prevAvg " 0) {
ans.push_back({prev, coord, prevAvg});
}

prev = coord;
prevAvg = newAvg;
}

// convertir a vector asignado (como int[][] en Java)
vector seleccionado());
para (size_t k = 0; k) ++k)
res[k] = { ans[k][0], ans[k][1], ans[k][2] };
restitución;
}
};
`` `

-...

## 5down Bono – Por qué esta es la variante “Sweep‐Line” del problema Skyline

← Problema TENIDO Similitudes
Silencio------------------------------
Silencio **Skyline** Silencio También barremos y mantenemos alturas activas ← Skyline mantiene la altura *maximum*; aquí mantenemos **average** (sum / count)
Silencio **Average Altura** Silencio Utiliza la misma actualización basada en el evento Silencio Necesitamos una suma de 64 bits y una división entero
Silencio **Merging** Silencio Skyline nunca fusiona alturas iguales a través de un evento Silencio Nuestro algoritmo salta la creación del segmento cuando el promedio permanece en la misma vida

-...

## 6down Cómo utilizar esto en su entrevista / Resumir

1. **Tome su solución** – `@lc` “Altura promedio de edificios en cada segmento” – `Medium`.
2. **Explicar el barrido** – mostrar la lista de eventos y la actualización del estado.
3. **La complejidad de la mención** – O(n log n) time, O(n) space.
4. **Discuss pitfalls** – overflow, division by cero, grouping events.
5. **Mostrar las tres implementaciones** – probar que puedes código en Java, Python, C++.

-...

## 7Ω⃣ SEO‐Friendly Blog Post

■ *Título*
■ “Master the LeetCode Medium Problem: Media Altura de Edificios – Java, Python & C++”

■ ** Descripción de los datos* *
■ “Aprenda a resolver la ‘Altura promedio de edificios de LeetCode en cada segmento’ con un algoritmo de gran alcance. Soluciones detalladas Java, Python y C+++, análisis de complejidad y consejos de entrevista. ”

■ **Keywords**
√ LeetCode, Altura Media de Edificios, Algoritmo de Línea Sweep, Problema de Skyline, Entrevista de codificación, Java, Python, C++, Pensamiento Algorítmico, Complejidad del Tiempo, Complejidad del Espacio, Ingeniero de Software, Estructuras de Datos, Preparación de Entrevistas, Búsqueda de Trabajo, Entrevista Técnica, Problema Media.

-...

#### 📝 Blog Post

■ **Author: ** *Su nombre* – *Ingeniero de software ← Algorithm Enthusiast*
■ *Hoy*

-...

### 🚀 “Average Height of Buildings in each Segment” – What Every Software Engineer should Know

El problema LeetCode “Altura promedio de edificios en cada segmento” es un escaparate perfecto de:

- La elegancia algorítmica**: Una línea de barrido de un paso golpea fuerza bruta por un factor de 105.
- ¿Qué? Gestionar actualizaciones de eventos con una lista ordenada o “TreeMap” (Python/C++) demuestra el conocimiento de árboles equilibrados / montones.
- **Resolver la mentalidad del programa**: Reconocer la conexión con el problema clásico de Skyline y reutilizar el patrón de la línea de barrido es exactamente el tipo de entrevistadores de información buscan.

A continuación, caminaremos por el razonamiento, las trampas y las soluciones en tres idiomas. Coge un café, sumérgete y siéntete libre de copiar-paste en tu repositorio local de IDE o GitHub.

-...

#### 1⃣ Declaración de problemas (parafraseada)

■ Una calle es una línea número.
" construcciones[i] = [start_i, end_i, height_i] " - el edificio ocupa `[start_i, end_i)` con altura `height_i`.
■ Regrese una lista de segmentos no superpuestos de media cuadra `[izquierda, derecha)` con la altura media ** entero** de todos los edificios que cubren ese segmento.
■ Segmentos donde el promedio es cero (sin edificio) debe ser omitido, y se deben fusionar segmentos con el mismo promedio.

*Por qué importa: *
- **Coordinar rango**: hasta 108, por lo que no podemos discretar toda la calle.
- **Tamaño de entrada**: 105 edificios → O(n2) fuerza bruta es imposible.
- **Interview relevance**: Este es un problema clásico de “sweep‐line” que aparece en muchas entrevistas de codificación y es una pregunta común LeetCode Medium.

-...

##### 2down⃣ El Sweep‐ Estrategia de línea

1. *Acontecimientos de edificios*
Para cada edificio crear dos eventos:
``text
(start, +height, +1) # edificio entra
(fin, -height, -1) # salidas de construcción
`` `

2. **Sort by Coordinate* *
Todos los eventos ordenados de izquierda a derecha.
Si varios eventos comparten la misma coordinación los procesamos **en conjunto** para evitar divisiones de segmento artificial.

3. **Estado autónomo**
``text
suma – altura total de todos los edificios activos (64-bit)
cnt - número de edificios activos
prevCoord – inicio del segmento actual
prevAvg – altura media actual
`` `

4. *Iterate*
* Para cada coordenadas `x`:
- Actualizar `sum ' y `cnt ' con **all** eventos en `x`.
- Compute `newAvg = sum // cnt ' if `cnt ' 0`, else `0`.
- Si `nueva Avg != prevAvg` **y ** `prevAvg ' 0`, empuje `[prevCoord, x, prevAvg]` para responder lista.
- Set `prevCoord = x` y `prevAvg = newAvg`.

5. **Finish**
Convertir la lista de respuestas en un array/`vector`.

*La complejidad:*
- **Hora**: `O(n log n)` debido a la clasificación; el escaneo es lineal.
Un evento por edificio.
- **La seguridad de los flujos**: Use 64 bits para la " suma " ; Los números enteros de Python no están abundados, C++/Java necesitan `long’/`long`.

-...

#### 3down⃣ Pitfalls comunes > Cómo evitamos los

Silencio Pitfall Silencio Lo que sucede Silencioso
Silencio--------------------------
Silencio **Desbordamiento entero** Silencio `su` excede 32‐bit tención Uso 64-bit (`long` / `long'). Silencio
Silencio **División por cero** Silencio No hay edificios activos → `cnt == 0` Silencioso guardia `cnt ¢ 0` antes de dividir. Silencio
Silencio **Segmentos innecesarios** Silencio Promedio se mantiene igual en un evento, pero todavía creamos un segmento Silencio Únicamente empujar un segmento si 'nuevoAvg != prevAvg` **y** `prevAvg œ 0`. Silencio
tención **Wrong merge logic** ← Segmentos con un promedio cero no debe ser la salida en absoluto Antes de empujar. Silencio

-...

##### 4down⃣ Three Language‐Specific Implementations

#### Java (using `ArrayList` + event scan)

``java
Clase Solución {
int[][] promedioAlturaDeconstrucción(int[][] [edificios] {}
Lista obtenida[] eventos relativos = nuevo ArrayList correctamente();
para (int[] b : edificios) {}
sucesos.add(new int[]{b[0], b[2], 1});
sucesos.add(new int[]{b[1], -b[2], -1});
}
events.sort(Comparator.comparingInt(a - título a[0]));

larga suma = 0;
int cnt = 0;
int prev = events.get(0)[0];
int prevAvg = 0;
Lista hecha[]]] > > > >

para (int i = 0; i) {}
int x = events.get(i)[0];
mientras (i) se realizaron eventos.size() " afectadas events.get(i)[0] == x) {
sum += events.get(i)[1];
cnt += events.get(i)[2];
i++;
}
int newAvg = cnt ≤ 0 ? (int)(sum / cnt) : 0;
si (newAvg != prevAvg " 0)
ans.add(new int[]{prev, x, prevAvg});
prev = x;
prevAvg = newAvg;
}

volver ans.toArray(nueva int[0][0]);
}
}
`` `

##### Python (lista directa/trabajo)

``python
Solución de clase:
def promedio AlturaDeconstrucción(auto, edificios: List[List[int]) - No. List[List[int]]:
sucesos = []
para s, e, h en edificios:
events.append(s, h, 1))
events.append(e, -h, -1))
events.sort()
sum_h, cnt = 0, 0
prev, prev_avg = events[0][0], 0
ans = []
I = 0
mientras que yo hice len(eventos):
x = sucesos[i][0]
mientras que yo hice len(eventos) y eventos[i][0] == x:
sum_h += events[i][1]
cnt += eventos[i ][2]
i += 1
new_avg = sum_h // cnt if cnt else 0
si nuevo_avg != prev_avg y prev_avg 0:
ans.append([prev, x, prev_avg])
prev, prev_avg = x, new_avg
Retorno
`` `

##### C+17 (usando 'tuple' para claridad)

``cpp
Clase Solución {
public:
vectores obtenidos mediante: {}
vector asignadotuple realizado,int,int,int
para (auto &b : edificios) {}
ev.emplace_back(b[0], b[2], 1);
ev.emplace_back(b[1], -b[2], -1);
}
sort(ev.begin(), ev.end(),
[](auto const " a, auto const " b){ return get did0 título(a) " )

larga suma = 0; int cnt = 0;
int prev = get won0(ev[0]), prevAvg = 0;
vector realizador:
para (size_t i = 0; i)
int x = get won0(ev[i]);
mientras (i)
la suma += conseguir realizada1(ev[i]);
cnt += conseguir obtenidos2(ev[i]);
++i;
}
int newAvg = cnt ? static_castint título(sum / cnt) : 0;
si (newAvg != prevAvg " 0) ans.push_back({prev, x, prevAvg});
prev = x; prevAvg = newAvg;
}

vector seleccionado());
para (size_t k = 0; k) ++k)
res[k] = { ans[k][0], ans[k][1], ans[k][2] };
restitución;
}
};
`` `

-...

##### 3down⃣ ¿Por qué? Esta es una gran pregunta de entrevista

1. **Reusabilidad** – La técnica de barrido se utiliza para “Número mínimo de arcos para cubrir un punto”, “Cubierta Interval” y el problema clásico “Skyline”.
2. **Edge‐Case Handling** – Mostrando que usted sabe manejar grandes sumas y división por cero es una manera rápida de impresionar a los reclutadores.
3. **Tiempo/Space Trade-offs** – Discutir por qué no se puede discretar toda la calle pero todavía puede procesar eventos de manera eficiente demuestra una fuerte comprensión de las restricciones algorítmicas.

-...

##### 4down⃣ Consejos para entrevistas

- Diagrama Estatal**: Sketch el tiempo del evento y los cambios del estado; ayuda a aclarar la lógica.
- **Testing**: Ejecutar los casos de esquina – un solo edificio, intervalos superpuestos, sin solapamiento, edificios que cubren el mismo segmento con diferentes alturas.
- **Explain Complexity**: `O(n log n)` es óptimo para este problema; no se puede superar la clasificación.
** Flexibilidad en idioma**: Mostrar las tres implementaciones para demostrar versatilidad.

-...

#### Гельные Takeaway

Dominar este problema significa que puedes:

- Aplicar **sweep‐line** a problemas que implican promedios, minima, maxima o sumas a intervalos.
- Evite errores comunes como desbordamiento o eventos no agrupados.
- Comunicar una solución algoritmoica limpia en varios idiomas.

Añádalo a su cartera, practique con variaciones (por ejemplo, “Maximum Media Altura”), y tendrá un sólido, listo para la entrevista LeetCode Medium problema en su toolkit. ¡Feliz codificación!

-...

##### 📌 Referencias > Leer más

- *Algorithms on Trees and Graphs* – Cormen et al. (Sección sobre los árboles de búsqueda binaria equilibrada).
- *LeetCode 1504: Maximum Media Subarray II* – otro problema de intervalo medio.
- *Cracking the Coding Interview* – capítulo sobre algoritmos Sweep Line.

-...

**End of Blog Post**

-...

Pensamientos finales

- **Tome su solución** en su plataforma de codificación o repositorio.
- **Mención del patrón algoritmo** – barrido, lista de eventos, actualización del estado.
*Mostrar los tres fragmentos de lenguaje* – esta es una señal fuerte de fluidez de codificación.
**Mantenga la discusión sobre las trampas** – desbordamiento, división por cero, agrupación de eventos.

Buena suerte en su próxima entrevista, y disfrutar de codificación! 🚀

-...

*No dude en comentar a continuación si tiene alguna pregunta o quiere discutir variaciones más profundas de este problema. *