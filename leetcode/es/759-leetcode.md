-...
Título: LeetCode 759. Empleado tiempo libre -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1. Code Solutions

A continuación se presentan tres implementaciones independientes y totalmente agregadas que resuelven **LeetCode 759 – Empleado Tiempo Libre**.
Cada aplicación sigue la misma estrategia *merge‐intervals*:

1. Aplanar todos los horarios de los empleados en una sola lista de intervalos.
2. Ordenar la lista por hora de inicio.
3. Incorpore intervalos superpuestos mientras graba las brechas entre ellos.

El resultado es la lista de intervalos libres finitos comunes a todos los empleados**.

■ **Tip** – En una entrevista, mencione que el enfoque funciona en el tiempo `O(N log N)` (dominated by the sort) y `O(1)` espacio extra más allá de la lista de resultados.

-...

## Java – Limpio e intuitivo

``java
importa java.util. ArrayList;
importa java.util. Colecciones;
importa java.util. Comparador;
importa java.util. Lista;

*
* Definición para un intervalo.
* También puede utilizar la clase Interval proporcionada de LeetCode.
*/
clase Interval {
int start, end;
Interval() { this.start = 0; this.end = 0; }
Interval(int s, int e) { this.start = s; this.end = e; }
@Override
public String toString() { return "[" + start + "," + end + "]"; }
}

Solución de la clase pública {}
public List Normativa de intervalores empleadosFreeTime(List seleccionadaList) {
Lista realizadaIntervalamento todos = nuevo ArrayList recomendado();
Lista Nombramiento Intervalado libre = nuevo ArrayList recomendado();

si (schedule == null peru schedule.isEmpty()) regresan libres;

// 1 / ⃣ Aplanar todos los intervalos
para (Lista)Intervalaño emp : horario) {}
all.addAll(emp);
}

// 2Get⃣ Sort by start time
Collections.sort(all, Comparator.comparingInt(a - confía a.start));

// 3 Cambios al tiempo que se acumulan lagunas
Interval prev = all.get(0);
para (int i = 1; i) i++) {
Cura intervalal = all.get(i);
si (cur.start > prev.end) { // espacio encontrado
free.add(new Interval(prev.end, cur.start));
prev = cur;
♪ otra vez { / / / superposición
prev.end = Math.max(prev.end, cur.end);
}
}
Retorno libre;
}
}
`` `

-...

## Python – Concise & Readable

``python
de la importación Lista

Clase Interval:
def __init__(self, start: int, end: int):
self.start = start
self.end = end
def __repr__(self):
volver f"[{self.start},{self.end}]"

Solución de clase:
def employee FreeTime(self, schedule: List[List[Interval]]) - List[Interval]:
# 1️ Flatten
intervalos = [para emp en el programa para él en emp]
# 2⃣ #
intervalos.sort(key=lambda x: x.start)

libre = []
prev = intervalos[0]
para curar en intervalos[1:]:
si cur.start > prev.end: # La brecha
free.append(Interval(prev.end, cur.start))
prev = curro
otra cosa:
prev.end = max(prev.end, cur.end)

de regreso libre
`` `

-...

## C++ – STL-powered

``cpp
Incluido el título
#include >

struct Interval {}
inicio int;
int end;
Interval() : start(0), end(0) {}
Interval(int s, int e) : start(s), end(e) {}
};

Clase Solución {
public:
std:::vector efectuado Interval confianza employeeFreeTime(estd::vector seleccionados:::vector seleccionadoInterval involucrado Calendario) {}
std::vector realizado Intervalamento todo, libre;
si (schedule.empty()) regresan libres;

// 1/
para (autoácidos emp : horario)
all.insert(all.end(), emp.begin(), emp.end());

// 2 carreras
std::sort(all.begin(), all.end(),
[](Contigo Intervalciente a, const Interval plaga b){ devolver a.start ; b.start; });

// 3down Combinar " recoger lagunas "
Interval prev = all[0];
para (size_t i = 1; i) ++i) {
Interval cur = all[i];
si (cur.start > prev.end) { // intervalo libre
free.emplace_back(prev.end, cur.start);
prev = cur;
♪ otra vez { / / / superposición
prev.end = std::max(prev.end, cur.end);
}
}
Retorno libre;
}
};
`` `

-...

# 2. Blog Artículo – “Employee Free Time: The Good, The Bad, and The Ugly”

■ **Título:** *El tiempo libre de los empleados – El bien, el mal y el imprudente: un profesional de trabajo– Guía de amistad*
■ **Target Palabras clave:** `employee free time`, `leetcode 759`, `interval merge`, `job interview coding`, `algorithm interview`, `Python solution`, `Java solution`, `C++ solution `

-...

## Introduction

Cada ingeniero de software tiene ese problema de entrevista que se siente como un *lot* más de lo que es.
LeetCode 759 – *Employee Free Time* es uno de esos problemas de “look-simple‐pero-has-gotchas”.

En este post, pasaremos por:

1. **El Bien** – por qué el problema es una gran pregunta de entrevista.
2. **El malo** – los obstáculos comunes que tropiezan con los candidatos.
3. **El Ugly** – casos de borde y errores sutiles que pueden descarrilar una solución de otro modo perfecta.

A lo largo del camino, presentaremos soluciones limpias y idiomáticas en **Java, Python y C+** – los tres idiomas que la mayoría de los entrevistadores les encanta ver.

■ ¿Por qué importa esto? * *
■ Una fuerte comprensión de los problemas de intervalo demuestra su capacidad para pensar en *overlap*, *condiciones de límites*, y *estrategias de grano* — habilidades que son invaluables en el código de producción.

-...

## El Bien: ¿Por qué 759 es un Gold‐Mine para entrevistas

Reason Silencio Lo que muestra
Silencio----------
TEN **Simplicity** TEN La declaración es corta, la estructura de datos (intervalos) es intuitiva. Silencio
Silencio **Multiple Approaches** Silencio Merge‐intervals, barrido, cola prioritaria. Los candidatos pueden elegir uno que se adapte a su comodidad. Silencio
Silencio **Analogía del mundo real** Silencio Programación, sistemas de reservas, planificación de eventos – todos familiarizados con los desarrolladores. Silencio
Silencio **Edge‐case Rich** Silencio Infinito límites, intervalos de longitud cero, entrada sin surtido. Silencio
Silencio **Scalable** Silencio La solución se extiende naturalmente a listas de 'k' (k-way merge). Silencio

### Interviewer Takeaway

■ *“Estás cómodo con un patrón algorítmico clásico, y eres capaz de adaptarlo a las limitaciones del problema.”*

-...

## El mal: Mis pasos comunes

Silencio Pitfall Silencio Por qué Sucede
Silencio...
Silencio **Asuming Input is Fully Sorted** Silencio Sólo la lista de empleados está ordenada, no la lista combinada. Silencio Aplanado y especie *antes* de fusión. Silencio
Silencio **Ignorando las intervalaciones de la longitud cero** Silencioso `[5,5]` debe ser descartado. tención Saltar intervalos donde `start == end` o comprobar la longitud de la brecha. Silencio
Silencio **Using Incorrect Merge Condition** ← Usar ``Consejo=` en lugar de `Consejo` conduce a lagunas desaparecidas. Silencio
Silencio **No Manejo de Empty Horarios** Silencio Null o entrada vacía puede lanzar `IndexOutOfBounds`. Silencio Volver lista vacía pronto. Silencio
Silencio **Mutable vs Immutable Interval Objects** Silencio Actualizar `prev.end` en el lugar puede corromper los datos originales si se reutilizan en otro lugar. Silencio Crear un nuevo "Intervalo" para intervalos fusionados. Silencio

■ **Key Insight: *El diablo está en el paso de clasificación.* Muchos candidatos se saltan porque ven “cada horario del empleado está arreglado. ”

-...

## The Ugly: Edge Cases That Fool Incluso el más inteligente

← Caso Edge Silencioso Lo que sucede Silencioso Cómo manejar
Silencio------------------------------------------------------
Silencio ** Números muy grandes** Silenciosos `end` valores hasta `10^8` – ningún desbordamiento en la entrada de 32 bits firmados. Use `long` en idiomas que lo expongan (Java) si desea seguridad adicional. Silencio
Silencio **Todos los empleados Ocupados Todo el Tiempo** Silencio Sin brechas finitas – el resultado debe estar vacío. Después de fusionarse, si la lista resultante está vacía, devuélvala. Silencio
Silencio **Single Employee** Silencio El tiempo libre es todo vacío entre sus propios intervalos. tención Todavía funciona – el algoritmo reduce a una sola lista fusión. Silencio
[1,3]` y `[3,5]` – no hay tiempo libre. TENIDO " Comparación " , no ` > . Silencio
Silencio **Intervalos Fuera de Orden Dentro de un Empleado** Silencio Aunque la especie dice ordenada, prueba contra una entrada malformada. Una solución robusta podría cambiar la lista de cada empleado primero. Silencio

-...

## Algorithm Recap – Merge‐Intervals

1. **Flatten** todos los intervalos en una sola matriz.
2. **Sort** by `start`.
3. **Tetrato** una vez, fusionando superposiciones y registrando lagunas.
4. Devuelve las brechas.

### Complexity

TENIDO ANTERIOR TERRITORIO TERRITORIO
Silencio...
Silencioso `O(N log N)` – `N` = intervalos totales, debido a la clasificación Silencioso `O(1)` extra (además de resultado)

■ **Por qué esto importa*
■ El entrevistador está a menudo más interesado en su proceso de pensamiento* que las micro-optimizaciones, pero conocer la complejidad le da un borde.

-...

## Code Show‐and‐ Dime

Silencio Idioma Silencio Silencio
Silencio...
Silencio **Java** Silencio Usos `Comparador.comparing Int; muta `prev` for brevity. Silencio
Silencio **Python** Silencio Comprensión de lista para aplanar; llave de tipo lambda. Silencio
Silencio **C+** Silencio STL `sort` con lambda; `emplace_back` para la eficiencia. Silencio

(Ver los bloques de código arriba.)

-...

## Cómo navegar la entrevista

1. **Preguntas de aclaración**
* ¿Son los intervalos inclusivos o exclusivos?
* ¿Debemos ignorar intervalos de longitud cero? (Siempre aclarado.)

2. **Habla tu proceso de pensamiento**
* “Aplanaré las listas primero porque el horario de cada empleado se ordena individualmente. ”
* Entonces me fusionaré mientras recojo las lagunas. ”
* “Finalmente, devolveré las brechas. ”

3. *Código limpio de la palabra*
* Evite fallos ocultos como `` `` cs ``.
* Use descriptive variable names (`prev`, `cur`).

4. *Casos de los mejores bordes*
* Un empleado soltero.
* Horarios completamente superpuestos.
* Intervalos adyacentes.
* Entrada vacía.

5. **Explicar la complejidad**
* “Sorting domina el tiempo de ejecución en `O(N log N)`.
* La fusión es lineal.

6. ** Extensiones de la mención**
* Si tuviéramos que apoyar límites infinitos, podríamos tratarlos como `INT_MAX` y `INT_MIN` e ignorarlos. ”

-...

Final Takeaway

LeetCode 759 es *no* una pregunta de truco; es un problema de entrevista *bien balanceado* que prueba los fundamentos del diseño del algoritmo, el manejo cuidadoso de los límites y la robustez del código.

Al dominar el **Bueno**, evitando el **Bad**, y confrontando el **Evidentemente**, te marcharás con una * solución segura y bien estructurada*, una que muestra exactamente por qué eres el candidato adecuado para un papel de producción.

Buena suerte, y recuerde: *las intervenciones son sellos de tiempo esperando su intuición codicioso. *

-...

■ **¿Quieres practicar? #
■ Trate de escribir la solución en su idioma preferido, luego ejecute contra el arnés de prueba siguiente (disponible en GitHub).

-...

¡Feliz codificación!
-...

■ *Alex “Algorithm” Johnson*
■ **Contacto** `alex.johnson@example.com `
■ **Suscribir** para más tutoriales de entrevista.
■ **Siguiente:** @AlgoMentor en Twitter.

-...

■ *Descargos* *Los fragmentos de código anteriores son para fines educativos. Adaptarlos siempre a su propio estilo de codificación. *

-...

*End of post. *

-...

**Meta‐Note (para los reclutadores / gerentes de contratación): * *
Cuando los candidatos pueden articular la historia *Good, Bad, Ugly* y proporcionar soluciones limpias a través de los principales idiomas, demuestran la mezcla de *problema-solving, comunicación, y capacidad de producción* que cada equipo moderno necesita. Este artículo es una adición ideal a su kit de herramientas de preparación de entrevista.