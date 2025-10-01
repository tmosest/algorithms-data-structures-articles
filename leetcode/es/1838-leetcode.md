-...
Título: LeetCode 1838. Frecuencia del Elemento Más Frecuente -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📌 Problema 1838 – Frecuencia del Elemento Más Frecuente
*Dificultad* Medium tención **LeetCode URL:** https://leetcode.com/problems/frequency-of-the-most-frequent-element/

■ * Objetivo*
■ En una pregunta de entrevista de un solo paso, se le pide que maximice la frecuencia de un elemento que usted puede obtener mediante la realización de * en la mayoría* `k` operaciones de aumento en un conjunto entero `nums`.
■ (Una operación de aumento significa añadir 1 a cualquier elemento de la matriz. El valor de `k` te dice cuántas veces puedes hacer esto.)

-...

## 🏁 Why Interviewers Love This Question

Por qué importa tu próxima entrevista
Silencio...
Silencio **Array + “cambio más grave”** Silencio Shows usted puede trabajar con la idea de que sólo el elemento más pequeño en un sub-array elegido necesita ser alcanzado hasta el más grande. Silencio
TEN **Sorting + Sliding Window** Silencio Un patrón de entrevista clásico: “Sor primero, luego escanear con dos punteros”. El equipo de trabajo quiere ver que reconoce este patrón. Silencio
tención **Single‐pass logic** tención Demuestra una comprensión profunda de cómo transformar un *constreñimiento global* (`k` incrementos totales) en una condición de ventana * local*. Silencio
TEN **Time/Space trade‐off** TENIDO Una solución O(n log n) limpia que utiliza sólo O(1) espacio adicional (además del tipo) es el lugar dulce que buscan los reclutadores. Silencio

■ **SEO Palabras clave**: *Leetcode 1838, Frequency of the Most Frequent Element, escaparate deslizante, preparación de entrevistas, entrevista de codificación, solución Java, solución Python, solución C++, problema algorítmico, complejidad del tiempo, entrevista de trabajo, reclutador técnico*

-...

## 🎯 Problema general

``text
Entrada: nums = [1,2,4,5], k = 5
Producto: 4
`` `

Puede añadir a la mayoría de los elementos. Después de las operaciones, ¿cuál es la frecuencia **maximum posible** de un único valor en el array?

-...

## 🔍 Approach – The “Good” Part

1. **Sorta el array**
*¿Por qué?* Grupos de clasificación iguales o cercanos valores juntos. Una vez ordenados, lo único que importa es cuántos elementos puede elevar a un valor objetivo (el elemento más adecuado de la ventana actual).

2. **Viento deslizante en la matriz ordenada**
*Mantenga una ventana " [izquierda ... derecha] " *
* `total` = suma de todos los elementos dentro de la ventana
* Condición:
``text
nums[right] * ventanaTamaño 0 = total + k
`` `
Si el lado izquierdo es violado, encoge la ventana de la izquierda hasta que la condición se satisfaga de nuevo.

3. **Track el mejor tamaño de la ventana** – ese tamaño es la respuesta.

■ **Por qué funciona* *
■ En una ventana clasificada el *target* es siempre el valor más adecuado. Todos los demás valores en la ventana deben aumentarse a este objetivo.
■ El número de incrementos necesarios es
" texto
■ objetivo * ventana Tamaño – total
" `
■ Si este número es ≤ `k`, la ventana es factible; de lo contrario debemos soltar elementos de la izquierda.

-...

## Гливали "Bad" – Edge‐Cases ' Gotchas

Cómo evitarlo
Silencio...
tención **Desbordamiento entero** – `nums[right] * windowSize` puede exceder `int` range. ¦ Use `long`/`long ` for the product (or cast to `1LL`). Silencio
Silencio **Gran tamaño de entrada** – El 'total' también puede ser grande. Silencio Acumular `total` en un `long `/`long`. Silencio
Silencio **Estado de lazo equivocado** – Olvidar restar `nums[left]` cuando la reducción puede llevar a respuestas incorrectas. TENIDO Cuidadosamente seguir el interior mientras está abierto y siempre actualizar 'total' y `izquierda'. Silencio

-...

## 🐛 El “Ugly” – Errores comunes

← Mistake Silencio Por qué sucede Silencio
Silencio...
Silencio **Tratar la matriz como un multiconjunto de frecuencias** Silencio Muchas personas piensan que "aumento de los números más pequeños" es la respuesta. Eso sería O(n k) y falla en las pruebas más grandes. Silencio Realizar la ventana debe apuntar el número * más grande* en la ventana (`nums[right]`). Silencio
Silencio **Mis‐interpreting `k`** Silencio Pensar `k` es un límite de per-elemento en lugar de un presupuesto global. Use `total + k` como la suma *disponible* para la ventana actual. Silencio
Silencio **Off‐by-one errores en el tamaño de la ventana** TENIDO Utilizando `derecha - izquierda` en lugar de `derecha - izquierda + 1`. TENIDO Doble-ver la fórmula del tamaño de la ventana. Silencio
Silencio **No clasificar** Silencio Olvidando que la lógica depende del orden ordenado. Silencio Add `sort(nums.begin(), nums.end())` (Java: `Arrays.sort(nums)`). Silencio

-...

## 🧩 Implementación – Solución de una línea en tres idiomas

A continuación encontrará una implementación lista para la producción, completamente comentada en **Java, Python y C+**. Los tres usan el mismo O(n log n) tiempo + O(1) algoritmo espacial descrito anteriormente.

#### ## 1down⃣ Java

``java
importa java.util. Arrays;

Clase Solución {
int public maxFrequency(int[] nums, int k) {
// 1. Ordenar – O(n log n)
Arrays.sort(nums);

total largo = 0; // suma de funcionamiento dentro de la ventana
int left = 0; // puntero izquierdo de la ventana corredera
int res = 0; // mejor ventana tamaño visto hasta ahora

para (derecho = 0; derecho) {}
total += nums[right];

// Ventana de contrato mientras que necesita más incrementos de lo que tenemos (k)
(de largo) nums[derecha] * (derecha - izquierda + 1)  Confía total + k) {}
total -= nums[left];
izquierda++;
}

// Respuesta actualizada
res = Math.max(res, right - left + 1);
}
restitución;
}
}
`` `

■ *Puntos clave*
* Use `long ' for `total` y el producto para evitar el desbordamiento.
* El interior " mientras " garantiza la ventana siempre satisface la restricción.

-...

#### 2down⃣ Python

``python
de la importación Lista

Solución de clase:
def maxFrequency(self, nums: List[int], k: int) - confiar int:
nums.sort() # O(n log n)
total = 0
izquierda = 0
res = 0

por derecho, val in enumerate(nums):
total += val

# La ventana de arrugas hasta que sea factible
mientras que val * (derecha - izquierda + 1)
total -= nums[left]
izquierda += 1

res = max(res, derecha - izquierda + 1)

retorno
`` `

■ ¿Por qué Python es genial aquí?
■ El código es extremadamente terse – sólo unas pocas líneas – sin embargo mantiene el mismo tiempo O(n log n) y las garantías del espacio O(1).

-...

#### 3down⃣ C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maxFrequency(vector fielint implicado nums, int k) {
(nums.begin(), nums.end()); // O(n log n)
long total = 0; // running sum
int left = 0, res = 0;

para (derecho = 0; derecho)
total += nums[right];

// Ventana de contrato mientras que requiere más de k aumentos
mientras (1LL * nums[derecha] * (derecha - izquierda + 1) {}
total -= nums[left];
++izquierda;
}

res = max(res, right - left + 1);
}
restitución;
}
};
`` `

■ ** Consejos C++**
* Use `1LL` para que el producto mantenga todo en 64 bits.
* `std::sort` es `O(n log n)` pero se puede realizar en el lugar (sólo se utiliza la pila de recursión).

-...

## 📑 Blog: "Cracking Leetcode 1838 – Frecuencia del Elemento Más Frecuente: Una Masterclass Sliding-Window”

-...

### #1# ## ## ##

■ **LeetCode 1838 – Frecuencia del Elemento Más Frecuente**
■ Se le da un array entero `nums` y un entero no negativo `k`.
■ Usted puede realizar en la mayoría de las operaciones de aumento " k " en cualquier elemento (add 1 cada vez).
■ ** Objetivo:** devolver la mayor frecuencia de un solo valor alcanzable después de todas las operaciones.

-...

#### 2down⃣ ¿Por qué esta pregunta es un *Golden Ticket* para entrevistas

← Recruiter Concern Silencio Candidate Skill Demonstrated Silencio
Silencio...
Silencio **Manipulación del rayo** Silencio Habilidad para pensar en términos de rangos y conteos
Silencio **Optimization mindset** latitud Reconocimiento de la necesidad de clasificar y pasar un solo paso
Silencio **Conciencia sobre el proyecto** Silencio ventana deslizante después de la clasificación es un patrón conocido de LeetCode
tención **Language versatility** Silencio Mostrando soluciones en Java, Python y C++ demuestra fluidez multiplataforma ¦

Si logras este problema, tendrás un punto de conversación sólido para cualquier entrevista de ingeniería de software, especialmente en empresas que valoran el pulido algorítmico* (Google, Facebook, Amazon, etc.).

-...

#### 3down⃣ El “bueno” – ¿Por qué nuestra aproximación de rocas

Silencio Por qué es “bueno”
Silencio...
TEN **Sorting first** TEN Grupos valores para que el valor más grande de cualquier sub-array esté en el límite correcto. Esto reduce la limitación global a la local. Silencio
Silencio **Two‐pointer escaparate** Silencio Un pase (O(n)) después del tipo → rápido, simple y probado patrón. Silencio
Silencio **Resumen (`total`)** Silencio Permite comprobar la viabilidad a tiempo constante para la ventana actual. Silencio
Silencio ** Actualizando la respuesta en cada iteración** ← Garantizas que nunca extrañamos una ventana más grande. Silencio

■ Resultado** – Un tiempo O(n log n) limpio, solución espacial O(1) que es rápida y fácil de razonar.

-...

#### 4down⃣ El “Bad” – Edge‐Case Conciencia

■ *Grandes productos → desbordamiento. *
■ *Acumular sumas en enteros de 64 bits. *
■ *Asegúrese de que el tamaño de la ventana es `derecha - izquierda + 1`, no `derecha - izquierda`. *

Los candidatos que prevengan estos obstáculos respetan a los candidatos. Añade un comentario en tu código: “Usando matemáticas de 64 bits para evitar el desbordamiento” y obtendrás puntos extras.

-...

#### 5down⃣ El “Ugly” – Cómo convertir errores comunes en ganancias

1. **Mis‐using `k` as a per-element budget* *
*Fix:* Use `total + k` como la suma *disponible* dentro de la ventana.
2. **Tocando el puntero izquierdo incorrectamente**
*Fix:* Actualizar `total` cada vez que elimina un elemento.
3. *Olvídalo*
*Fix:* Añadir la línea de clasificación antes del bucle – es la piedra angular de toda la lógica.

Convertir una solución ingenua en una estrategia de ventana * deslizante* es la prueba definitiva de *problema‐pattern recognition* — un rasgo fundamental entrevistable.

-...

#### 6down⃣ Cómo explicar la lógica de la ventana deslizante en la mosca

■ Después de ordenar, cualquier ventana `[izquierda...derecha]`. tiene un objetivo natural: el elemento más adecuado `nums[right]`. Todos los demás elementos de la ventana deben aumentarse a este objetivo.
■ El número de incrementos requeridos equivale a `target * windowSize – total`. Si ese valor es ≤ k, la ventana es válida; de lo contrario nos encogemos de la izquierda hasta que sea. ”

Al explicar, enfatizar la distinción **local vs global**: la viabilidad de la ventana es un cheque *local* (`k` es un presupuesto *global*).

-...

### 7ف⃣ Summary – What Draft should Take Home

* **Reconocimiento de Patrones** – “Sort + Ventana Sliding” es una estrategia básica de LeetCode.
* **Overflow Awareness** – Usar matemáticas de 64 bits le muestra el cuidado del código de producción listo.
* **Cross‐Language Implementation** – Demostrar soluciones Java, Python y C++ demuestra que eres un pensador algorítmico completo.
* **Problema‐Solving Clarity** – Una explicación concisa (como la tabla anterior) es perfecta para entrevistas técnicas.

■ **Takeaway**: “Lo he arreglado, luego he deslizado una ventana, luego he mantenido el mejor tamaño de la ventana – eso es todo lo que necesitas para resolver LeetCode 1838. ”

-...

#### 8down⃣ Palabra final

■ “Si puedes articular por qué ordenar la ventanilla deslizante resuelve el problema *y* proporciona Java limpio, Python y código C++, acabas de entregar una obra maestra de entrevista completa.
■ Este es el tipo de pregunta que muestra *claridad, velocidad y profundidad* – la combinación exacta que buscan los reclutadores.

-...

**Feliz codificación, y la mejor suerte con su próxima entrevista!

-...

■ *Recuerde probar su solución con las pruebas ocultas de LeetCode – cubren casos de borde como `k = 0`, todos los elementos ya iguales, o muy grandes `k`. Una solución de grado de producción pasará a todos ellos. *

-...

*Feliz codificación, futuro candidato estrella!* .
-...

**(Si tienes preguntas o quieres profundizar en las matemáticas detrás del producto-check, deja un comentario a continuación o abre un problema en el GitHub repo.)* *
-...

*Mantén la curiosidad. Sigue codificando. Sigue entrevistando. *

-...

**End of Blog* *
-...

-...

*Ahora tienes:
* Una base de código pulida y lista para la producción en tres idiomas.
* Un blog listo para publicar para impresionar a los reclutadores y entrevistadores por igual.
* Una comprensión clara del patrón, los obstáculos y cómo explicarlo. *

¡Buena suerte! 🏆

-...

**[Descargar la hoja de trampa PDF](#)** (incluye los fragmentos de código + explicación de referencia rápida).

-...

*Avísame si te gustaría una inmersión más profunda en las matemáticas, un videoconferencia, o una sesión de entrevista mock. *



-...

**TL;DR** – *Sorta, diapositiva, encoge, pista*. Todo en `O(n log n)` tiempo, `O(1)` espacio, y unas docenas de líneas de código. Este es el problema de la entrevista que quieres en tu curriculum vitae.
-...

*Buena suerte, y disfrutar de su viaje al siguiente nivel! *

-...



-...



-...

-...

-...

-...

-...

-...



-...

-...

-...

-...

-...

-...



-...

-...

-...



-...

-...

-...



-...

-...

-...



-...

-...

-...



-...



-...



-...

-...



-...

-...



-...

-...



-...

-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-...



-..