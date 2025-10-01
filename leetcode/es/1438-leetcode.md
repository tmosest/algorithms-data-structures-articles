-...
Título: LeetCode 1438. Subarray Continuo Más largo con Diff Absoluto Menos Que O Igual a Límite -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1438. Subarrayo continuo más largo con Diff absoluto ≤ Límite
### LeetCode – Medium

**Problema de declaración* *

■ Dado un conjunto entero `nums ' y un " límite " entero, devuelve el tamaño del subarray más largo * no vacío* de tal manera que la diferencia absoluta entre cualquier dos elementos en ese subarray es en la mayoría de `limit ' .

`` `
Entrada : nums = [8,2,4,7] , límite = 4
Producto: 2
`` `

¿Por qué es interesante? #
La solución ingenua (ver cada subarray posible) es \(O(n^2)\) y se ajustará al tamaño máximo de entrada \(n = 10^5\).
Una solución lineal de ventanilla deslizante a tiempo usando dos deques (o una cola balanceada de BST/prioridad) corre en \(O(n)\) y es el patrón canónico de “greedy + estructura de datos” que aman los entrevistadores.

-...

## 1. Algorithm – Ventana deslizante de dos grados

1. Mantenga dos deques:
* `maxDeque` – almacena índices de elementos en **disminución** orden (el frente es el máximo actual).
* `minDeque` – almacena índices de elementos en **aumento del orden** (el frente es el mínimo actual).
2. Ampliar el extremo derecho de la ventana un paso a la vez.
* Mientras que el nuevo elemento es más pequeño que la parte posterior de `maxDeque`, pop the back – mantenemos sólo candidatos útiles para el máximo.
* Mientras que el nuevo elemento es más grande que la parte posterior de `minDeque`, pop the back – mantenemos sólo candidatos útiles para el mínimo.
* Empuja el nuevo índice en ambas deques.
3. Después de añadir el elemento, compruebe si la ventana es **válida**:
\[
nums[maxDeque.front] - nums[minDeque.front] \le limit
\]
Si es **inválido**, encoge la ventana de la izquierda (`izquierda') hasta que vuelva a ser válida, eliminando los índices que dejan la ventana desde el frente de cada deque.
4. Actualizar la respuesta con el tamaño actual de la ventana (`derecha - izquierda + 1`).

¿Por qué funciona esto? #
Debido a que las deques siempre mantienen el máximo y mínimo de la ventana actual, la diferencia se puede obtener en \(O(1)\).
Cuando la ventana se vuelve inválida, sabemos que el elemento que causó la violación debe estar en el lado izquierdo – moviendo `izquierda' hacia adelante lo elimina. Esto garantiza que cada índice se inserta y se elimina al máximo una vez → tiempo lineal.

-...

## 2. Complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
← Principal loop Silencio \(O(n)\) Silencio \(O(n)\) (deques, pero cada índice almacenado sólo una vez) ←
← Respuesta final Silencio \(O(1)\) Silencio \(O(1)\) Silencio

-...

## 3. Implementaciones de referencia

## Java

``java
importa java.util. ArrayDeque;

Solución de la clase pública {}
int public longestSubarray(int[] nums, int limit) {}
ArrayDeque se realizóInteger confianza maxQ = nuevo ArrayDeque corresponde(); // decreciente
ArrayDeque se cumplióInteger confianza minQ = nuevo ArrayDeque correspondió(); // increasing
int left = 0, ans = 0;

para (derecho = 0; derecho) {}
// mantener max deque
mientras (!maxQ.isEmpty() " nums[maxQ.peekLast()] {}
maxQ.pollLast();
}
maxQ.offerLast(right);

// mantener min deque
mientras (!minQ.isEmpty() " nums[minQ.peekLast()] {}
minQ.pollLast();
}
minQ.offerLast(right);

// ventana de contracción si es necesario
(nums[maxQ.peekFirst()] - nums[minQ.peekFirst()]
si (maxQ.peekFirst() == left) maxQ.pollFirst();
si (minQ.peekFirst() == left) minQ.pollFirst();
izquierda++;
}

ans = Math.max(ans, right - left + 1);
}
devolver los ans;
}
}
`` `

## Python

``python
de las colecciones importa
de la importación Lista

Solución de clase:
def longest Subarray(self, nums: List[int], limite: int) int:
max_q = deque() # decreciente
min_q = deque() # increasing
izquierda = 0
ans = 0

por derecho, num in enumerate(nums):
mientras max_q y nums [max_q[-1]]
max_q.pop()
max_q.append(right)

mientras min_q y nums[min_q[-1]
min_q.pop()
min_q.append(right)

nums[max_q[0] - nums[min_q[0] límite:
si max_q[0] == izquierda:
max_q.popleft()
si min_q[0] == izquierda:
min_q.popleft()
izquierda += 1

ans = max(ans, right - left +1)
Retorno
`` `

### C++

``cpp
Incluido el título
#include >
#include >

Clase Solución {
public:
más largo Subarray(std::vector fieltro nums, int limit) {}
ptd::deque correspondía máxQ; // decreciente
std::deque correspondintios minQ; // increasing
int left = 0, ans = 0;

para (derecho = 0; derecho)
mientras (!maxQ.empty() ' nums[maxQ.back()]
maxQ.pop_back();
maxQ.push_back(right);

mientras (!minQ.empty() " nums[minQ.back()]
minQ.pop_back();
minQ.push_back(right);

(nums[maxQ.front()] - nums[minQ.front()]
si (maxQ.front() == izquierda) maxQ.pop_front();
si (minQ.front() == left) minQ.pop_front();
++izquierda;
}
ans = std::max(ans, right - left + 1);
}
devolver los ans;
}
};
`` `

-...

## 4. Artículo del Blog – *El bueno, el malo y el ingenio de soluciones de ventanilla deslizante*

#### Introduction

Cuando usted ve un problema de LeetCode titulado “Longest Continuous Subarray ...”, su mente corre inmediatamente a * ventana deslizante*. Las ventanas deslizantes son el pan-y-butter de la preparación de la entrevista: son rápidas, intuitivas, y a menudo la única solución aceptable para grandes limitaciones de entrada.

En este post caminaremos a través de los **bueno**, **bad**, y **ugly** aspectos de soluciones de ventanilla deslizante para LeetCode 1438, *Longest Subarray continuo con Absolute Diff ≤ Limit*. Derribaré el algoritmo, mostraré código Java/Python/C++ y le daré consejos fáciles de SEO que le ayudarán a brillar en una entrevista técnica o en un blog de búsqueda de trabajo.

■ **Seo titular**: “Master LeetCode 1438: Sliding‐Window Deques to Pass in O(n) – Java, Python & C++”

-...

### The Good

TENIDO TENIDO ANTERIOR ANTERIOR Por qué importa
Silencio...
tención **Tiempo de iluminación** Silencio \(O(n)\) Silencio Escalas a \(n = 10^5\) en
TEN **O(1) actualizaciones amortizadas de la ventana** Silencio Deques mantener max/min TEN Evita ordenar o saltar operaciones. Silencio
Silencio **Readability** Silencio Dos preguntas + punteros Silencio fácil de explicar en una entrevista. Silencio
Silencio **Memoria amigable** Silencio Cada índice almacenado una vez TENIDO Extra \(O(n)\) peor, pero las deques son minúsculas. Silencio

El *good* es obvio: el algoritmo es óptimo para las limitaciones del problema y utiliza un patrón de estructura de datos limpio que los entrevistadores aman.

-...

### El malo

Silencio Silencio Silencio Silencio Silencio Silencio
La vida... la vida...
Silencio **Edge-case la complejidad** Silencio Manejando las deques vacías cuando se encogía TENIDO Comprobando cuidadosamente `front()` antes de saltar. Silencio
Silencio **Language quirks** ⋅ Java’s `ArrayDeque` vs. `LinkedList` TENIDO Use `ArrayDeque` for O(1) ops. Silencio
Silencio **Large integer values** Silencio `int` vs. `long` Silencio En Java, utilice `int` porque los límites de problemas encajan, pero observe si extiende la lógica. Silencio
tención **Las dificultades de legibilidad** ← Sobre-commenting vs. over-abstracting Silencio Mantener un equilibrio: comentar sólo las partes no obvias. Silencio

Estas son molestias menores que aparecen si se copiara una plantilla sin entender el matiz de la aplicación de cada idioma.

-...

### El Ugly

Silencio 👹 Silencio Pitfall Silencio
Silencio...
Silencio **Off‐by-one bugs** Silencio El bucle de riego puede dejar la ventana inválida tención Verifique después del bucle con una prueba de aserción o unidad. Silencio
Silencio **O(n2) en casos malos** Silencio Deques incorrectos que no pop back Silencio Asegurar `mientras (maxQ.back י new)` lógica es correcta. Silencio
Silencio **Desbordamiento de datos sobre la recursión** Silencio Ninguno en este problema ← Pero tenga en cuenta el uso de pilas en soluciones recursivas. Silencio
Silencio **El límite de tiempo excede en gran entrada** ← Extra `Math.max` dentro del bucle Silencio Mover fuera si usted puede, pero aquí es barato. Silencio

La parte *ugly* nos recuerda que la ventana corredera es poderosa **solo** si se implementa correctamente. Un solo tipo en la lógica deque puede convertir una solución óptima \(O(n)\) en una lenta.

-...

## 5. Cómo mostrar esto en su blog o resumen

1. **Título** – Hacerlo keyword-rich: “Longest Continuous Subarray (LeetCode 1438) – Sliding Window Deques in Java, Python, C++”.
2. **Intro** – Brevemente indicar el problema y el desafío de la gran entrada.
3. ** Sección Algorithm** – Use pseudo-código y diagrame sus deques.
4. ** Análisis de la complejidad** – Nota de Big‐O con explicaciones.
5. **Code snippets** – Include the three language implementations. Mención que deques son el linchín.
6. **Discusión** – Bien, malo, feo – muestra que no solo estás copiando; entiendes los cambios.
7. **Link** – Proporcionar la URL de LeetCode y un enlace a un repo GitHub con la solución completa.
8. ** Etiquetas de la SEO** – “LeetCode 1438”, “Sliding Window”, “Java Deque”, “Python Deque”, “C++ Deque”, “O(n) solution”, “Entrevista técnica”.

Añadiendo una pequeña sección de pruebas unitarias o un punto de referencia de rendimiento (por ejemplo, `timeit` en Python) le da al lector confianza extra.

-...

## 6. Lista de verificación para el retiro

- Conseguir el uso **dos deques**: uno para máx, uno para min.
- ✅ Maintain deques in **monotonic** order.
- Límpiate la ventana hasta la diferencia ≤ límite.
- Recibir la respuesta de actualización después de cada expansión.
- TENIDO Evite errores por cada prueba con casos de borde.

-...

#### TL;DR

- Problema: El subarray más largo con tenciónmax‐min permanente ≤ límite.
- Solución: Ventana deslizante + dos deques (queues monotónicas).
- Complejidad: \(O(n)\), espacio \(O(n)\).
- Código listo para Java, Python, C++.

■ **Pro tip**: Cuando le explicas esto a un entrevistador, comienza con “Mantengo el máximo y mínimo de la ventana actual en deques para que pueda saber la diferencia en O(1). Luego deslizaré la ventana hasta que la diferencia sea ≤ límite. Ese es un "campo de ascensor" de 10 segundos que instantáneamente muestra que conoce el patrón.

¡Feliz codificación y buena suerte aterrizando ese trabajo!