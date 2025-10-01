-...
Título: LeetCode 2386. Encuentra el K-Sum de un Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

## 1. Recaptación de problemas
**LeetCode 2386 – Encuentra el K‐Sum de un Array* *

■ *Dado un array entero `nums` y un entero positivo `k`, usted puede elegir cualquier subsequence de la matriz y sumar todos sus elementos.
■ El **K‐Sum** es la suma de subsecuencia más grande ** (las sumas de subsecuencia son ** no** necesarias para ser distintas).
■ Devuelve el K‐Sum del array. *

*Subsequence* = mantener el orden original, eliminar cero o más elementos.
La subsequencia vacía cuenta y tiene una suma de `0`.
`1 ≤ n ≤ 105`, `-109 ≤ nums[i] ≤ 109`, `1 ≤ k ≤ min(2000, 2n)`.

-...

## 2. Visión clave

Vamos.

`` `
P = suma de todos los elementos positivos en las monjas
`` `

Si **flip** cada elemento a su valor absoluto, el array se convierte en no negativo.
Para un array no negativo la suma de subsequencia **k‐th más pequeña** es fácil de generar con un min-heap (el problema clásico de la “k‐th menor subset sum”).

¿Por qué ayuda esto?

* La mayor suma de subsequencia de la matriz original es `P` – sólo toma cada elemento positivo.
* Cada subsequence de la matriz original puede ser representado como
`P – (suma de elementos que *excluimos* de P)`.
Excluir elementos es equivalente a *adding* los valores absolutos correspondientes a un array no negativo.
* Por lo tanto la suma **k‐th más grande** del array original es
`P – (la suma de subsecuencia más pequeña de la matriz de valor absoluto)`.

Así que el problema se reduce a: ** encontrar la suma de subsecuencia más pequeña k‐th de un array no negativo**.

-...

## 3. Algoritmo (Heap + Two‐Pointer Trick)

1. **Proceso previo**
* `P` ← suma de números positivos.
* `abs[i] = Silencionums[i].
Cada vez más.

2. Min-heap
Cada elemento de salto almacena
* `sum` - la suma de subsecuencia actual.
* `idx` – el índice del último elemento incluido en esta suma.
El montón es ordenado por `sum` (ascending).

*Comienza* con `(abs[0], 0)` – la suma no vacía más pequeña posible.

3. **Generate k‐th smallest* *
Repita 'k-1' veces:
* Pop the smallest pair `(sum, idx)` → `cur`.
* Los dos siguientes candidatos que pueden derivarse de " vale " son:

* **Exclude** the last element: `cur.sum - abs[idx]` (esto ya está representado por `cur` después del primer pop, por lo que sólo lo guardamos para el siguiente paso).
* **Incluya** el siguiente elemento: `cur.sum - abs[idx] + abs[idx+1]`.
* Empujar ambos hacia el montón (si 'idx+1' se hizo n`).
* Mantenga el último popped `cur.sum` – esta será la suma más pequeña k después de que el bucle termine.

4. **Respuesta*
`ans = P - cur.sum`.

-...

### Complexity Analysis

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencio Ordenación Silencioso `O(n log n)` Silencio
Silencio Heap operations Silencio `O(k log k)` Silencio `O(k)` Silencio

Con `k ≤ 2000`, el algoritmo cumple fácilmente los límites incluso para `n = 105`.

-...

## 4. Aplicación del Código

#### 4.1 Java

``java
importa java.util. Arrays;
importa java.util. Comparador;
importa java.util. Prioridad Queue;

Solución de la clase pública {}
kSum(int[] nums, int k) {
long posSum = 0;
int n = nums.length;
int[] abs = nuevo int[n];
para (int i = 0; i)
si (nums[i] 0) posSum += nums[i];
abs[i] = Math.abs(nums[i]);
}
Arrays.sort(abs); // O(n log n)

// Elemento de salto: [suma actual, último índice]
PriorityQueue hacía lo largo[] confía pq = nueva PrioridadQueue decir correctamente(Comparador.comparingLong(o - título o[0]));
pq.offer(new long[]{abs[0], 0});

long curSum = 0;
para (int t = 0; t {}
long[] cur = pq.poll(); // O(log k)
curSum = cur[0];
int idx = (int) cur[1];
si (idx + 1 ) {
// incluir el siguiente elemento
largo incluye = curSum - abs[idx] + abs[idx + 1];
// excluir el elemento actual (sólo mantener la curva)
pq.offer(new long[]{include, idx + 1});
pq.offer(cur);
}
}
retorno posSum - curSum; // respuesta final
}
}
`` `

#### 4.2 Python

``python
importación heapq
de la importación Lista

Solución de clase:
def kSum(self, nums: List[int], k: int) - título int:
pos_sum = sum(x para x en nums si x > 0)
abs_vals = ordenados(abs(x) por x en nums)

# heap element: (current_sum, last_index)
heap = [(abs_vals[0], 0)]
cur_sum = 0

para _ en rango(k):
cur_sum, idx = heapq.heappop(heap)
si idx + 1 < len(abs_vals):
incluye = cur_sum - abs_vals[idx] + abs_vals[idx + 1]
heapq.heappush(heap, (include, idx + 1))
heapq.heappush(heap, (cur_sum, idx))

retorno pos_sum - cur_sum
`` `

#### 4.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
largo largo largo kSum(vector interpretadoint círculo nums, int k) {
larga posada Sum = 0;
int n = nums.size();
vector llevado a cabo largo plazo abstenVals(n);
para (int i = 0; i) {}
si (nums[i] 0) posSum += nums[i];
absVals[i] = llabs(nums[i]);
}
(absVals.begin(), absVals.end()); // O(n log n)

// min-heap de pares {current_sum, last_index}
usando P = par realizado largo, int
priority_queue obtenidosP, vector asignadoP título, mayor especificadoP título
pq.emplace(absVals[0], 0);

CurSum largo = 0;
para (incluido paso = 0; paso) {}
auto [sum, idx] = pq.top(); pq.pop();
curSum = sum;
si (idx + 1 ) {
largo tiempo incluyen = suma - absVals[idx] + absVals[idx + 1];
pq.emplace(include, idx + 1);
pq.emplace(sum, idx);
}
}
retorno posSum - curSum;
}
};
`` `

-...

## 5. Blog Article (SEO‐Optimized)

■ *Título*
√ _LeetCode 2386 – Encuentra el K‐Sum de un Array: Java / Python / C+ Soluciones & Insightful Guide_

■ **Meta Descripción**
■ Master LeetCode 2386 con soluciones Java, Python y C++. Aprende el algoritmo basado en el montón, el análisis del espacio-tiempo, y consejos prácticos para crear este problema difícil en las entrevistas.

■ **Keywords**
√ LeetCode 2386, K‐Sum, subsequence sum, heap algoritmo, Java solution, Python solution, C++ solution, interview preparation, algoritmo analysis

-...

#### Introduction

LeetCode **2386 – Encuentra el K‐Sum de un Array** es un problema *hard* que prueba tu comprensión de las subsecuencias, montones y trucos de reducción inteligentes. Si se está preparando para entrevistas técnicas, resolver este problema mostrará su capacidad de manipular sumas, utilizar colas prioritarias y pensar fuera de la caja.

En este artículo, pasamos por:

1. La visión matemática que convierte una pregunta “k‐th mayor” en una “k-th más pequeña”.
2. Un algoritmo basado en heap que funciona en **O(n log n + k log k)** tiempo.
3. Código limpio, listo para la producción en **Java, Python, y C++**.
4. Lo bueno, lo malo y lo feo de la solución – qué amar, qué cuidar y cómo mejorar.

Entremos.

-...

## 6. The Core Insight – Positive vs. Non-Negative

### ¿Por qué voltear a no negativo?

- La suma de subsecuencia **maximum** de cualquier matriz es simplemente la suma de todos los números positivos.
*Si agregas algún número negativo, solo reduces la suma. *

- Para un array ** no negativo**, las sumas de subsequencia más pequeñas son fáciles de enumerar con un min-heap.
Cada subsequence puede ser representado como un camino en un árbol binario donde el niño izquierdo excluye el siguiente elemento y el niño derecho lo incluye.

Así, la suma **k‐th más grande** del array *original* es igual:

`` `
(máxima suma positiva) – (máxima suma de abs(nums)
`` `

-...

## 7. Generación basada en el montón de k‐th Sum más pequeño

El problema clásico de “k‐th menor subset sum” se puede resolver en **O(k log k)** utilizando un min‐heap.

### Pasos

1. **Proceso previo**
* Compute `P = sum of positives`.
* Reemplazar cada elemento por su valor y tipo absolutos.

2. **Initializar el montón**
Empujar `(abs[0], 0)` – la suma no vacía más pequeña posible.

3. **Iterate**
Pop el par más pequeño `(sum, idx)`.
Generar dos niños:
* Incluya el siguiente elemento → `(sum - abs[idx] + abs[idx+1], idx+1)`.
* Mantenga la misma suma → `(sum, idx)` (para la próxima iteración).

4. Después del bucle, el último saltó `sum` es el más pequeño **k‐th**.
Sumételo de `P` para obtener la respuesta.

-...

## 8. Muestras de código completo

*(ver las secciones del código anterior – Java, Python, C++)*

■ **Tip** – En Java, usa `long` para todas las sumas para evitar el desbordamiento.
■ En C++, 'long' es tu amigo.
■ El "int" de Python está sin límites, así que estás a salvo.

-...

## 9. Bien, malo y feo

### The Good

- **Intuition-driven** – Reduce una pregunta “más grande” difícil a un problema de montón conocido.
- **Fast** – `k ≤ 2000` asegura que las operaciones de los montones son triviales incluso para la gran 'n'.
- ** Luz de memoria** - Sólo espacio auxiliar de `O(k).

### El malo

- **Pre-procesamiento** requiere ordenar toda la matriz - `O(n log n)`.
Si el array ya está clasificado, puede saltarse este paso.

* Casos de emergencia* Si todos los números son negativos, `P = 0`.
El algoritmo todavía funciona porque estamos restando la suma *smallest* de `0`.

### El Ugly

*Sumas duplicadas* – El montón podría generar la misma suma varias veces (por ejemplo, excluyendo el mismo elemento).
En nuestra sencilla implementación ignoramos duplicados; una solución más óptima utiliza un hash set para deduplicar antes de empujar.

Large k** Si una pregunta de entrevista empuja `k ' cerca de `n ' (por ejemplo `k = 105 ' ), el algoritmo actual se volvería infeasible.
Para tales escenarios, necesitaría un enfoque de división y conquista o DP.

-...

## 9. Takeaways for Interviews

1. **Explicar la reducción**: a los entrevistadores les encanta escuchar el “por qué” detrás de su algoritmo.
2. **Discuss time‐space**: mostrar que puede analizar la complejidad en el contexto de las limitaciones (`k ≤ 2000`).
3. **Manejo de bordes de altura**: mencione cómo evitas el desbordamiento y aseguras que el montón nunca se agote de los candidatos.
4. **Offer an optimization**: si el tiempo lo permite, muestre cómo saltar duplicados o usar un truco de dos puntos para evitar re-pushing el mismo elemento.

-...

## 10. Pensamientos finales

LeetCode 2386 es un hermoso ejemplo de cómo una reducción inteligente convierte un problema intimidante en uno manejable. El truco del montón es limpio, eficiente y portátil en los principales idiomas.

Ahora es el momento de practicar. Ejecutar el código, ajustar la entrada, y sentir la intuición solidificar. ¡Buena suerte en tu viaje de entrevista! 🚀

-...

## Call to Action

- **Al igual que ** Compartir** si te resultó útil.
- Subscríbete** para más avances de problemas difíciles de LeetCode.
- **Comentario** sus propias optimizaciones o preguntas – mantengamos la discusión en marcha.

-...

■ ¡Feliz codificación!
* Tu mentor de algoritmo amigable*

-...

Eso completa la solución completa: el algoritmo, el código y un blog listo para la entrevista. ¡Feliz entrevista!