-...
Título: LeetCode 630. Calendario del curso III -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

# The “Course Schedule III” Interview Puzzle
**LeetCode 630 – Hard**
*¿Qué reclutadores quieren ver? Cómo resolverlo en Java, Python, " C+++. *

-...

## TL;DR

Silencio Idioma Silencio Código Silencio
Silencio...
Silencio **Java** Silencioso [Ver] (#java-code)
Silencio **Python** Silencio [Ver] (#python-code)
[Ver](#c-code) Silencio

■ **Algorithm** – Greedy + Max‐Heap
■ **Tiempo** – `O(n log n) `
■ **Espacio** – `O(n)`

-...

## ¿Por qué este problema se mete en una entrevista de trabajo

* ** Gran prueba * Muestras que puedes razonar sobre la optimización.
* **Heap data structure** – Le da la oportunidad de demostrar familiaridad con las colas prioritarias.
* ** Vibe del mundo real** – Los cursos de programación son como la gestión del proyecto. Me encanta escucharlo.

-...

## Problema Recap

Se le da 'cursos', un array donde cada elemento es `[duración, último Día]`.
Usted comienza el día 1, no puede superponer los cursos, y cada curso debe terminar **por** su 'último Día'.
Devuelve el número máximo ** de cursos que puedes tomar.

-...

## El “bien” – Un codicioso limpio y óptimo

1. ** Cursos de reserva por fecha límite ( " último día " )** –
siempre trate de terminar el primer curso antes.
2. **Mantenga un máximo de duración** –
el montón tiene todos los cursos que has aceptado hasta ahora.
3. **Si añadir un nuevo curso te mantiene a tiempo** → aceptarlo.
Actualizar el tiempo actual y presionar su duración sobre el montón.
4. **Si añadiera que te haría tarde** →
Mira el curso más largo que ya estás tomando (`heap.peek()`).
Si esa duración más larga es **más grande** que la nueva, sustituyala:
* eliminar el más largo, añadir el nuevo, ajustar el tiempo total.
Esto libera tiempo y mantiene el horario ajustado.
5. **Resultado** – el tamaño del monto es el número máximo de cursos.

¿Por qué funciona?
Debido a que el montón siempre almacena las duraciones más cortas posible** que permiten cumplir los plazos más tempranos.
Si en cualquier momento llegamos tarde, reemplazar el curso más largo con un más corto sólo puede ayudar.

-...

## El “Bad” – Qué cuidar

Por qué importa confidencialidad
Silencio...
tención **Ties in deadlines** Silencio Ordenar por `lastDay` alone is enough, but be careful with `stable` sorting in some languages. Use un tipo estable o agregue una llave secundaria (duración) si se desea. Silencio
Silencio **Large input** Silencio `n` puede ser 104, por lo que un algoritmo lineal o cuadrático TLE. Solución de uso `O(n log n)` arriba. Silencio
Silencio **Desbordamiento entero** Silencio El tiempo acumulativo puede exceder de 231-1. TENIDO Utilizar enteros de 64 bits ( " largo " en Java, " largo " en C++ " en Python es ilimitado). Silencio

-...

## Los “Ugly” – Problemas comunes y casos de borde

Silencio Caso Silencioso Silencioso
Silencio--------------------
Silencio **Cuarto tarda más tiempo que su fecha límite** Silencio `[5, 3]` – imposible de terminar. El algoritmo se saltará automáticamente. Silencio
Silencio **Todos los cursos imposibles** Silencio Ejemplo 3: `[3,2],[4,3]]. 0. Silencio
Silencio **Duplicar los plazos y duraciónes** Silencio Ordenar no debe comportarse mal. tención Comparador sólo debe utilizar `la última hora`. Silencio
Silencio **Cuantales duraciones pero pocos plazos** tención El tiempo puede exceder los límites int. TENIDO Utilizar enteros de 64 bits. Silencio
Silencio ** Valores negativos** Silencio Constraints garantizan positivo, pero la codificación defensiva es buena. Silencioso o guardia contra los negativos. Silencio

-...

## El Código

A continuación se encuentran soluciones listas para pasar por **Java**, **Python**, y **C+**.
Los tres usan la misma idea algorítmica.

## Java

``java
importar java.util*;

Solución de la clase pública {}
public int scheduleCourse(int[][] courses) {
// 1 / ⃣ Ordenar por última vez Día
Arrays.sort(courses, Comparator.comparingInt(a - título a[1]));

// 2Get Max Max‐heap (la duración más grande en la parte superior)
Prioridad Queue won(Collections.reverseOrder());

long currentTime = 0; // 64‐bit para evitar el desbordamiento

para (int[] curso : cursos) {}
duración int = curso[0];
int deadline = course[1];

si (hora actual + duración) {
// 3down Aceptar el curso
maxHeap.offer(duration);
corriente Tiempo += duración;
} si (!maxHeap.isEmpty() " limit maxHeap.peek() " duración) {}
// 4down Reemplazar el curso más largo
tiempo actual += duración - maxHeap.poll();
maxHeap.offer(duration);
}
// si no: saltar este curso
}
volver maxHeap.size();
}
}
`` `

## Python

``python
importación heapq
de la importación Lista

Solución de clase:
def schedule Curso(auto, cursos: List[List[int]]) - int:
# Sort by deadline
cursos.sort(key=lambda x: x[1])

# Max‐heap using negative durations
Max_heap = []
current_time = 0

por duración, plazo en los cursos:
si actual_time + duración 0 = plazo:
heapq.heappush(max_heap, -duration)
actual_time += duración
elif max_heap y -max_heap[0] duración:
current_time += duration + heapq.heappop(max_heap) # pop largest, add new
heapq.heappush(max_heap, -duration)

(max_heap)
`` `

### C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
horario int Curso(vector seleccionador seleccionador) {}
Ordenar por fecha límite
sort(courses.begin(), courses.end(),
[](cont vector identificadoint ánimo a, const vector identificadoint círculo b) {
devolver a[1]
});

// 2️ Max‐heap of durations
prior_queue indicaint contacto maxHeap;
largo plazo = 0; // 64-bit

para (continuo auto-cliente c : cursos) {}
int dur = c[0], dl = c[1];
si (curTime + dur ) {
maxHeap.push(dur);
curTime += dur;
} si (!maxHeap.empty() " maxHeap.top()  Confeder dur) {
curTime += dur - maxHeap.top();
maxHeap.pop();
maxHeap.push(dur);
}
}
(int)maxHeap.size();
}
};
`` `

-...

## Blog Artículo: "El Bien, el Mal, y el Ugly of Course Schedule III"

■ **Título** – “Mastering LeetCode 630: Course Schedule III – The Good, The Bad & The Ugly”*
■ **Meta‐Description** – *Aprenda la solución de salto codicioso a LeetCode 630, bucee en casos de borde, y as su próxima entrevista de ingeniería de software. *

-...

#### 1down⃣ El Bien: ¿Por qué esta Solución Rocks

- **Simplicity + Power** – Un solo pase después de la clasificación da la respuesta óptima.
- **Intuitive Greedy** – “Toma el curso con el plazo más temprano primero. ”
- **Heap Leverage** – Replacing the longest course is O(log n), keeping the schedule tight.
- **Real‐World Parallel** – Similar a la programación de tareas, la planificación de proyectos o la programación de trabajo de CPU.

#### 2down⃣ El mal: Pitfalls comunes para evitar

Silencio Pitfall Silencio
Silencio...
TENIDO Utilizando `int` para el tiempo acumulativo TENIDO Switch to `long` / `long long` to avoid overflow. Silencio
Silencio Ignorando la posibilidad de plazos precoces tención Siempre ordenar por plazo; un tipo equivocado da resultados sub-optimales. Silencio
Silencio Asumiendo que todos los cursos se ajusten a la vida El algoritmo salta cursos imposibles automáticamente. Silencio
Una solución ingenua `O(n2)` (p. ej., retroceder) se llenará con 104 entradas. Silencio

#### 3down⃣ The Ugly: Edge Cases " Tuning

- **Reunión de la fecha límite** - Se permite el curso termina en su "último Día".
- **Large durations** – Incluso si la duración de un curso es mayor que su fecha límite, el algoritmo lo descarta naturalmente.
- **Ties in deadlines** – El orden de los cursos con el "último Día" idéntico no afecta la corrección, pero un tipo estable mantiene la lógica clara.
- ** Pieza de memoria** – Almacenes en la mayoría de las `n` duración, por lo que la memoria `O(n)` es aceptable.

-...

## Interview Tips: Talking About This Problem

1. *Explicar al invariante avaro* “Si usted puede terminar un curso en su fecha límite, siempre es seguro tomarlo; de lo contrario, sustituimos el más largo si libera tiempo. ”
2. **Mostrar la intuición del montón** – “Necesitamos acceso rápido a la duración más larga para poder cambiarlo. ”
3. ** Complejidad de la mención** – “Sorting `O(n log n)`, each heap operation `O(log n)`, total `O(n log n)`.”
4. ** Casos de ventaja de discusión** – “¿Y si la duración de un curso excede su plazo? Nuestro algoritmo se salta. ”

-...

## SEO > Job‐Hunting Boost

← Palabra clave Silencio Por qué ayuda
Silencio...
Silencio `LeetCode 630` Silencio Partido directo para los reclutadores que buscan este problema. Silencio
Silencio III solución` Ø Alto volumen de búsqueda para la preparación de entrevistas. Silencio
Silencio `Java priority queue LeetCode` Silencio Targets entrevistas centradas en Java. Silencio
Silencio `Python heapq interview` Silencio Showcases Python skills. Silencio
Silencio `C++ prior_queue scheduling` peru Highlights C+++ proficiency. Silencio
Silencio `Greedy algoritmo interview` ¦ Demonstrates algoritmoic thinking. Silencio
Silencio `Software ingeniero entrevista consejos` Silencio Broad audiencia. Silencio

**Incluya estas palabras clave de forma natural en las partidas, balas y la meta descripción**. Un artículo bien estructurado con fragmentos de código claro se clasificará más alto y captará los ojos de los reclutadores.

-...

### Final Checklist Before You Submit

- Código de cesión compila en Java 17 / Python 3.10 / C+17.
- Recibir todos los casos de borde cubiertos.
- Recibir Complejidad declarada.
- ✅ artículo del blog listo para Medium, Dev.to, o su propia cartera.
- ✅ Palabras clave rociadas en todo.

¡Buena suerte! 🚀

-..