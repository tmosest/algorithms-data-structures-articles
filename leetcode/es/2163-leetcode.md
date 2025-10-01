-...
Título: LeetCode 2163. Diferencia mínima en los sumos después de la eliminación de elementos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 2163 – Diferencia mínima en los sumos después de la eliminación de elementos
**Solución en Java, Python & C+**
**Blog Post:** *El bueno, el malo, el ugly – Cómo hacer funcionar este problema de entrevista (y aterrizar su trabajo de sueño)*

-...

#### 1ICK⃣ Problema Resumen
Dado un array 0-indexed `nums` de longitud `3 * n`, debemos **remove exactamente `n `elementos**.
Los elementos restantes 2n se dividen en dos partes iguales:

`` `
parte izquierda – primeros elementos n → sumaPrimero
parte derecha – siguiente elementos n → sumSecond
`` `

Devuelva el valor mínimo posible** de `sumFirst – sumSecond`.

■ **Constraints**
* `1 ≤ n ≤ 105`
≤ 105
* `nums.length == 3*n`

-...

## 2down Idea de alto nivel
Podemos pensar en el array como ** tres bloques contiguos**:

`` `
[izquierda] [medio] [derecha]
`` `

* En el bloque *izquierda* queremos mantener los números **smallest** n`; se convertirán en parte de `sumFirst`.
* En el bloque *derecha* queremos mantener el ** más grande** n` números, se convertirán en parte de `sumSecond`.

El reto es decidir dónde cortar la matriz en `[0 ... i] y `[i+1 ... 3n-1]` para que la diferencia de las dos sumas sea mínima.

### Strategy
1. **Prefijo izquierdo** – para cada posible punto de corte `i` (después de al menos `n' elementos y antes del último `n`), computar la suma de los números *n más pequeños* en `nums[0 ... i].
*Mantenga* estas sumas utilizando un **max-heap** (la cola de la prioridad) que almacena los valores actuales `n` más pequeños.
2. **Sufijo derecho** – similarmente, para cada punto de corte `i`, computar la suma de los números *n más grandes* en `nums[i+1 ... 3n-1].
*Mantenga* estas sumas utilizando un **min-heap** que almacena los valores actuales `n` mayores.
3. La respuesta para un corte en la posición `i` es `leftSum[i] – rightSum[i+1]`.
Escanear todo válido 'i' y mantener el mínimo.

** Complejidad del tiempo** – `O(n log n)` (heap operations).
** Complejidad del espacio** – `O(n)` para los dos arrays auxiliares más montones.

-...

## 3down Implementaciones de referencia

### 3.1 Java (Java 17)

``java
importar java.util*;

Solución de la clase pública {}
public long minimumDifference(int[] nums) {
int len = nums.length; // 3 * n
int n = len / 3; // número de elementos para eliminar
long[] leftSums = new long[len];
long[] rightSums = new long[len];

// ----------- lado izquierdo: mantener n menor - Sí.
Prioridad Queue won(Collections.reverseOrder());
larga izquierda Sum = 0;
para (int i = 0; i)
maxLeft.offer(nums[i]);
izquierda Sum += nums[i];
}
izquierda Sums[n - 1] = leftSum; // primer prefijo válido

para (int i = n; i)
int cur = nums[i];
si (curo < maxLeft.peek() { // reemplazar el mayor en el montón
izquierda Sum += cur - maxLeft.poll();
maxLeft.offer(cur);
}
leftSums[i] = leftSum;
}

// ----------- lado derecho: mantener el mayor .
Prioridad Búsquedas realizadasInteger monedas minRight = nueva PrioridadQueue relacionarse();
larga derecha Sum = 0;
para (int i = len - 1; i >= len - n; i--) {}
minRight.offer(nums[i]);
rightSum += nums[i];
}
rightSums[len - n] = rightSum; // último sufijo válido

para (int i = len - n - 1; i >= n; i--) {}
int cur = nums[i];
si (cuerdo > minRight.peek() { // reemplazar el más pequeño en el montón
rightSum += cur - minRight.poll();
minRight.offer(cur);
}
rightSums[i] = rightSum;
}

----------- computar la diferencia mínima - Sí.
larga respuesta = larga. MAX_VALUE;
para (int i = n - 1; i)
respuesta = Math.min(respuesta, leftSums[i] - rightSums[i + 1]);
}
respuesta de retorno;
}
}
`` `

-...

### 3.2 Python 3.9+

``python
importación heapq
de la importación Lista

Solución de clase:
mínimo Difference(self, nums: List[int]) - int:
n3 = len(nums) # 3 * n
n = n3 // 3
[0] * n3
derecha = [0] * n3

# --- izquierda: manténgase más pequeño...
Max_heap = [] # almacenará negativos para emular max‐heap
left_sum = 0
para i en rango(n):
heapq.heappush(max_heap, -nums[i])
left_sum += nums[i]
izquierda[n] - 1] = left_sum

para i en rango(n, n3 - n):
cur = nums[i]
si cursó -max_heap[0]:
eliminado = -heapq.heapreplace(max_heap, -cur)
left_sum += cur - eliminado
izquierda[i] = izquierda_sum

# ----- right: keep n largest ---
min_heap = []
right_sum = 0
para i en rango(n3 - 1, n3 - n - 1, -1):
heapq.heappush(min_heap, nums[i])
right_sum += nums[i]
right[n3 - n] = right_sum

para i en rango(n3 - n - 1, n - 1, -1):
cur = nums[i]
si se curan, min_heap[0]:
eliminado = heapq.heapreplace(min_heap, cur)
right_sum += cur - removed
right[i] = right_sum

--- mínima diferencia ---
as = flotante('inf')
para i en rango(n - 1, n3 - n):
as = min(ans, left[i] - right[i + 1])

Retorno
`` `

-...

### 3.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
larga duración mínimoDiferencia(vector fieltro nums) {
int len = nums.size(); // 3 * n
int n = len / 3;

vector realizado largamente larga izquierda(len), derecha(len);

// ---------- izquierda: mantener n menor --------
priority_queue didint contacto maxLeft; // max-heap
larga izquierda Sum = 0;
para (int i = 0; i) {}
maxLeft.push(nums[i]);
izquierda Sum += nums[i];
}
izquierda[n] - 1] = leftSum;

para (int i = n; i) {}
int cur = nums[i];
si (cuerdo) {}
izquierda Sum += cur - maxLeft.top();
maxLeft.pop();
maxLeft.push(cur);
}
left[i] = leftSum;
}

// ---------- derecha: mantener el mayor --------
priority_queue obtenidosint, vector asignadoint minRight; // min‐heap
larga derecha Sum = 0;
para (int i = len - 1; i >= len - n; --i) {}
minRight.push(nums[i]);
rightSum += nums[i];
}
right[len - n] = rightSum;

para (int i = len - n - 1; i >= n; --i) {}
int cur = nums[i];
si (curre √≥ minRight.top()) {}
rightSum += cur - minRight.top();
minRight.pop();
minRight.push(cur);
}
right[i] = rightSum;
}

--------- respuesta computarizada --------
ans largos = LLONG_MAX;
para (int i = n - 1; i) {}
as = min(ans, left[i] - derecho[i + 1]);
}
devolver los ans;
}
};
`` `

-...

## 4down Blog Post – “El bueno, el malo”

-...

### 📄 Meta Descripción
■ Aprende a resolver LeetCode 2163 “Diferencia mínima en los sumos después de la eliminación de elementos” en Java, Python y C++. Entender el algoritmo, las trampas y las ideas de entrevista que le ayudarán a crear su próxima entrevista de codificación y aterrizar un trabajo técnico.

-...

Artículo

# The Good, the Bad & the Ugly - How to Nail LeetCode 2163 (and Land Your Dream Job)

■ **Keywords**: *LeetCode 2163, Diferencia Mínima en Sumas Después de la eliminación de elementos, solución de salto Java, cola de prioridad Python, C++ prior_queue, algoritmo de entrevista, entrevista de estructuras de datos, consejos de entrevista de trabajo, estrategia de entrevista de codificación, entrevista de ingeniero de software. *

-...

Introducción

Cuando los reclutadores preguntan “**¿Cuál es tu problema más desafiante de LeetCode**?”, no sólo buscan una respuesta correcta; quieren ver ** código limpio, uso inteligente de estructuras de datos, y una explicación sólida**.
LeetCode 2163 – *Minimum Difference in Sums After Removal of Elements* – es un candidato principal porque combina ** programación dinamica** con ** colas de prioridad**.
En este post caminaremos a través de los aspectos *bueno* (eficiente & elegante), el *bad* (trinquiles tricky), y los aspectos *ugly* (Indice gimnasia) del problema, luego presentar soluciones de referencia en **Java, Python y C+**.

-...

## 2down⃣ Problema Recap (en estilo de entrevista)

■ *Prompt*
■ *Tienes una matriz de tamaño 3 × n. Quitar exactamente los elementos n. Los 2n elementos restantes se dividen en una mitad izquierda y derecha. Devuelve el valor mínimo posible de la suma (izquierda) – suma(derecho). *

¿Por qué es interesante? #
* Es un rompecabezas de “partición después de la eliminación” – muchos candidatos lo resuelven ingenuamente con la enumeración “O(n3), que los tiempos salen.
* La solución óptima demuestra el dominio de **Heaps** (queues de prioridad) – un elemento básico en muchas preguntas de entrevista.

-...

## 3down El Bien - Lo que funciona

Silencio Feature Silencio Lo que significa Silencio Por qué importa
Silencio--------------------------- La vida eterna
Silencio **O(n log n) time** Silencio Cada operación de salto cuesta log n, realizado 2 × n veces Silencio Escalas al máximo `n = 105`. Silencio
Silencio ** Estructuras de datos simples** tención Sólo dos colas prioritarias + dos arrays O(n) tención Clear, código mantenible que evita tablas de DP complejas. Silencio
Silencio **Deterministic Output** Silencio Usa sumas largas/64 bits para evitar el desbordamiento Silenciosos contra casos de prueba ocultos con grandes valores. Silencio
tención **Cross‐Language Consistency** ← Mismo algoritmo en Java, Python, C++ Silencio Shows language‐agnostic thinking – a plus in coding interviews. Silencio

-...

## 4down El malo – Cosas Que va mal

1. **Off‐by‐One Errores**
* The cut point must leave at least `n` elements on each side (`i` from `n-1` to `3n-n-1`).
* Olvidar esto conduce a resultados erróneos o incorrectos.
2. ** Gestión del tamaño de la pila* *
* Reemplazar el elemento * más grande* en un max-heap o el elemento *smallest* en un min‐heap es fácil en teoría pero fácil de revertir en la práctica.
* En Python, los números negativos emulan un max-heap – una fuente común de errores.
3. **Overflow**
* `sumFirst ` and `sumSecond` can each reach `n * 105` (Ω 1010), which fits in 32‐bit signed int only by luck.
* Use 64-bit (`long`/`long') para sumas intermedias.
4. **Mimory Footprint* *
* Storing two `O(3n)` arrays pueden ser pasados por alto; en `n = 105`, esto es ~ 2 × 3 × 105 × 8 bytes ♥ 4 MB - todavía bien, pero mencionarlo en la explicación.

-...

## 5down Casos de borde oculto

Escenario Silencioso Por qué Es Ugly
Silencio----------------------------------
Silencio **Todos los números iguales** Silencio El algoritmo todavía funciona, pero se siente “demasiado fácil” y puede distraer de partes más interesantes de la entrevista. Silencio Mostrar el candidato puede adaptar la solución para este caso degenerado rápidamente. Silencio
Silencio **Números negativos (no en restricciones)** Silencio Si las restricciones cambian para permitir que los negativos, la lógica del montón se rompe (por ejemplo, 'n` más pequeño puede ser negativo). Silencio Pregúntele al entrevistador si quieren apoyar los negativos; si es así, ajuste las comparaciones de montones en consecuencia. Silencio
Silencio **Tamaño de entrada alto (n = 105)** tención Recursión o bucles ingenuos pueden alcanzar límites de pila o tiempo de salida. Use bucles iterativos y arrays pre-allocate; prueba con un caso aleatorio grande. Silencio
Silencio **Non‐contiguous cut** Silencio El problema explícitamente requiere mitades contiguas, pero un candidato podría pensar erróneamente que pueden reordenar el array. Silencio Clarify el requisito de “split en dos mitades” temprano en la conversación. Silencio

-...

Entrevistador Perspectiva

¿Por qué hacen sus puntos de conversación?
Silencio----------------------------------------...
tención *Explicar el algoritmo y por qué los montones funcionan.* Silencio Tests comprensión de “seleccionar el k más pequeño / más grande”. Silencio Mención que un máximo de salto mantiene el `k` más pequeño y un min-heap mantiene el `k` más grande. Silencio
*¿Puede reducir aún más la complejidad del tiempo?* tención Compruebe si una solución O(n) o O(n log n) es óptima. Silencio Show that `O(n)` is impossible because you must inspect each element at least once, and `O(n log n)` is excellent with heaps. Silencio
*¿Qué pasa si los valores eran mayores de 32 bits?* Silencio Prueba el manejo del desbordamiento. tención Emphasize using 64‐bit integers for sums. Silencio
Silencio *¿Puede escribir esto en otro idioma?* Silencio Fluencia de lenguaje cruzado. ← Presentar los fragmentos Java, Python, C++ y discutir cualquier matiz específico del lenguaje. Silencio

-...

## 7 carreras Cómo impresionar en su entrevista

1. **Empieza con un plan claro* *
* “Voy a usar dos montones: un max-heap para el lado izquierdo y un min-heap para el lado derecho. ”
* Escribe el plan en una pizarra antes de codificación.
2. **Explicar los montones**
* “El max‐heap siempre contiene los valores actuales `n` más pequeños en el prefijo. Si un nuevo elemento es más pequeño que el máximo del montón, pop y empujamos. ”
* El min‐heap mantiene los valores más grandes en el sufijo. ”
3. **Mostrar el circuito de punta corta* *
* “Bajamos una ventana sobre los puntos de corte válidos y computamos la diferencia en O(1) por paso. ”
4. ** Análisis del espacio*
* " O(n log n) " time due to heap operations; `O(n)` espacio auxiliar. ”
5. ** Casos de emergencia**
* “Usamos “long” para evitar el desbordamiento. Si los valores pudieran ser negativos, ajustaríamos la lógica de comparación. ”
6. *Código de California*
* Mantener nombres variables descriptivos ( " izquierda " , `derecha ' , `cortar ' ).
* Use pre-allocalización (`vector cumplió largas instrucciones izquierda(n*3)` en C++).

-...

## 8down Takeaway

LeetCode 2163 no es sólo otro rompecabezas – es un ** escaparate de pensamiento algoritmo**.
Al dominar el *bueno* (varios eficientes), evitando el *bad* (off-by-ones ' desbordamiento), y navegando el *ugly* (casos altos), demostrarás un profundo entendimiento de que los reclutadores valoran.
Utilice las soluciones de referencia en **Java, Python y C+** como un punto de referencia y práctica explicándoles en voz alta – ese es su camino más rápido hacia el botón "hire".

-...

### 🚀 Palabras finales

- *Code primero, explíquelo más tarde. *
- *Cuando en duda, haga preguntas claras – muestra que usted es considerado, no descuidado. *
- *Práctica escribiendo la misma solución en tres idiomas – prueba versatilidad. *

Buena suerte, y que el montón esté contigo! 🚀

-...

**End of Article**

-...

#### 📌 Nota para

Al revisar la solución de un candidato a LeetCode 2163, concéntrese no sólo en la corrección sino también en:

* ** Claridad Algorítmica** – ¿Han articulado la estrategia del montón?
* Manejo de los retratos* ¿Usaron sumas de 64 bits?
* **La legibilidad del código** – ¿Son los nombres variables descriptivos?
* **Cross‐Language Proficiency** – ¿Han presentado soluciones Java, Python y C++?

Si un candidato revisa todo lo anterior, son un fuerte contendiente para cualquier papel de ingeniería de software.