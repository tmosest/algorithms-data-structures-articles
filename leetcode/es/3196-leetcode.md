-...
Título: LeetCode 3196. Maximizar el coste total de las subarrayas alternantes -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 3196. Maximizar el costo total de las subarrayas supletorias
**Medium ⋅ Public Silencio LeetCode**

-...

## 🚀 TL;DR

- ** Objetivo:** Dividir el array en subarrays contiguos para que la suma de
`nums[l] – nums[l+1] + ... + nums[r] sobre cada subarray se maximiza.
- **Resultando DP:**
``text
dp[i] = max( s[i] + best Odd, -s[i] + bestEven )
`` `
donde `s[i]` es la suma de prefijo alternante y
`bestOdd = max_{j odd} (dp[j] – s[j])`,
`bestEven = max_{j even} (dp[j] + s[j])`.
- **La complejidad: *El tiempo, `O(1)` la memoria.
- Idiomas: Java, Python, C++ (todos usan enteros de 64 bits).

-...

## 📚 Declaración de problemas

Se le da un conjunto entero 'nums' de longitud `n`.

`` `
cost(l, r) = nums[l] - nums[l+1] + nums[l+2] - ... + nums[r] * (-1)^(r-l)
`` `

Dividir el array en uno o más subarrays contiguos de tal manera que el costo total se maximice.
Devuelve el coste total máximo.

-...

## 🧩 Key Insight

El costo de un subarray depende sólo de la paridad de su índice de inicio.
Al pre-computar la suma de prefijo supletoria** `s[i] = Governing_{k=0.i} nums[k] * (-1)^k`, el costo de cualquier subarray se puede expresar como:

`` `
cost(l, r) = (-1)^l * ( s[r] – s[l-1] )
`` `

Esto nos permite formular un DP 1-dimensional que sólo necesita mantener dos máximos de funcionamiento (“bestOdd’, `bestEven`) en lugar de escanear todos los puntos de división posibles.

-...

## Solution Outline

1. *Fundación de prefijo*
``text
s[i] = s[i-1] + nums[i] * (-1)^i
`` `
2. ** Transición de los desplazados**
Para cada índice " i " (la posición final del último subarray):
``text
dp[i] = max( s[i] + best Odd, -s[i] + bestEven )
`` `
* `bestOdd` – maximum value of `dp[j] – s[j]` for odd `j` (including `j = -1`).
* `bestEven` – valor máximo de `dp[j] + s[j]` para incluso `j`.
3. ** Actualizar máximas de funcionamiento**
Después de computar `dp[i]`, actualice la paridad correspondiente:
``text
si lo soy: mejor Incluso = max(best) Incluso, dp[i] + s[i]
más: mejorOdd = max(best Odd, dp[i] - s[i]
`` `
4. **Respuesta*
`dp[n-1]` es el costo total máximo.

-...

## 📦 Code Implementations

## Java

``java
importar java.util*;

Solución de la clase pública {}
máximo público largo TotalCost(int[] nums) {
int n = nums.length;
long[] s = new long[n];
long bestOdd = 0; // dp[-1] - s[-1] = 0
mucho mejor Incluso = Long.MIN_VALUE; // no even j yet

para (int i = 0; i)
long val = nums[i];
signo largo = (i " 1) == 0 ? 1 : -1;
s[i] = (i == 0 ? 0 : s[i-1]) + signo val *;

long option1 = s[i] + bestOdd; // último subarray comienza en el índice impar
long option2 = -s[i] + bestEven; // última subarray comienza en índice
dp largo = Math.max(option1, opción2);

// Actualizar los mejores valores para futuros índices
(i) == 0) { // incluso
bestEven = Math.max(bestEven, dp + s[i]);
# Si no #
lo mejor Odd = Math.max(mejor Odd, dp - s[i]);
}
}
volver s[n-1] + bestOdd; // dp[n-1] = max( s[n-1]+bestOdd , -s[n-1]+bestEven )
}
}
`` `

## Python

``python
Solución de clase:
def máximo TotalCost(self, nums: List[int]) - int:
n = len(nums)
s = [0]
best_odd = 0 # dp[-1] - s[-1] = 0
best_even = -10**18 eficazmente -

for i, v in enumerate(nums):
señal = 1 si i % 2 == 0 más -1
s[i] = (s[i-1] si no 0) + v * signo

opt1 = s[i] + best_odd
opt2 = -s[i] + best_even
dp = max(opt1, opt2)

si I % 2 == ### even index
best_even = max(best_even, dp + s[i])
más: # índice extraño
best_odd = max(best_odd, dp - s[i])

volver s[-1] + best_odd # dp[n-1]
`` `

### C++

``cpp
Clase Solución {
public:
largo plazo máximo TotalCost(vector seleccionadoint frecuentemente reducido) {
int n = nums.size();
vector de larga duración s(n);
largo tiempo mejor Odd = 0; // dp[-1] - s[-1]
largo tiempo mejor Incluso = LLONG_MIN / 2; //

para (int i = 0; i) {}
larga señal = (i % 2 == 0) ? 1 : -1;
s[i] = (i? s[i-1] : 0) + 1LL * nums[i] * signo;

long long opt1 = s[i] + bestOdd; // comenzar con el índice impar
long long opt2 = -s[i] + best Incluso; // comenzar en índice
dp largo = max(opt1, opt2);

si (i % 2 == 0) // incluso j
bestEven = max(best Incluso, dp + s[i]);
más // extraño j
mejorOdd = max(best Odd, dp - s[i]);
}
volver s[n-1] + bestOdd; // dp[n-1]
}
};
`` `

-...

## 📈 Why This Works (Proof Sketch)

- ¿Qué?
`cost(l, r) = (-1)^l * (s[r] – s[l-1])`.
El signo `(-1)^l` sólo depende de la *paridad* de `l`.

- *Reescribir la política*
Seamos el final del último subarray.
`dp[i] = max_{j identificadoi} dp[j] + cost(j+1, i)`.
La sustitución de la expresión de costo da dos expresiones lineales separadas en `s[i]` dependiendo de la paridad de `j`.
De ahí que el máximo sobre todo " j " se reduzca al máximo de dos valores de funcionamiento ( " mejorOdd " , " mejor aún " ).

- ¿Por qué?
Las actualizaciones `bestEven = max(bestEven, dp[i] + s[i])` (even `i`) y
`bestOdd = max(best Odd, dp[i] - s[i])` (odd `i`) keep the best possible
contribuciones para futuras transiciones sin ningún bucle.

-...

## 📌 Edge Cases " Pitfalls (Good / Bad / Ugly)

← La situación actual
Silencio...
Silencio **Grandes sumas** Silenciosos `nums[i]` hasta ±1 000 000, `n` hasta 100 000 → total puede alcanzar ~1014 Silencio Uso `long` en Java, `long` en C+++, `int` está bien en Python (sin límites). Silencio
# Initial `best Incluso `** Silencio Hay *no * incluso índice `j` antes del primer elemento. tención Comienzo con `-∞` (por ejemplo, `Long.MIN_VALUE/2`). Silencio
← **La paridad de Index** Silencio En Java & C++, `-1` es extraño, por lo que `mejorOdd` comienza en 0, cubriendo el caso donde el primer subarray comienza en el índice 0. ◾ Explicitly set `bestOdd = 0` and skip `bestEven` at the start. Silencio
Silencio **Overflow in languages with fixed broad** Silencio El valor intermedio `dp[i] + s[i]` puede rebosar 32‐bit. Silencio Siempre lanzado a 64-bit (`long` / `long long`). Silencio
Silencio **Python** Silencio No hay flujo de ancho fijo; sólo tenga cuidado con la infinidad negativa (`-10**18` es seguro). TENIDO Use `-10**18` o `float('-inf')` si lo prefiere. Silencio
Silencio **Caso de Corner** Silencio No se permite la matriz vacía (`n ≥ 1`). tención Código naturalmente lo maneja porque siempre computamos `dp[0]`. Silencio

-...

## 🎯 Interview‐Ready Summary

1. **Understand parity** – el signo voltea con cada elemento, por lo que el índice *starting* decide si añadimos o restamos la suma prefija alterna.
2. **Derive an O(n) DP** – keep two running maximums; the transition becomes a simple `max` of two linear functions.
3. **Mira el tipo de datos** – Los enteros de 64 bits son obligatorios para Java/C++.
4. **Implement cleanly** – el algoritmo es sólo ~30 líneas por idioma y no utiliza ningún array adicional más allá de la suma prefijo.

-...

## 📢 SEO‐Boosted Takeaway

Si está preparando una entrevista **de codificación** o buscando una solución **LeetCode 3196**, este post cubre todo lo que necesita:

- **Keywords**: LeetCode 3196, Maximizar el coste total de las subarrayas alternantes, programación dinámica, preparación de entrevistas, Java, Python, C+++
- ** Beneficios**:
*Un paso, algoritmo de tiempo lineal* que se puede pegar en cualquier plataforma de entrevista.
La misma idea se aplica a cualquier problema cuando el costo de un segmento depende sólo de su paridad inicial.

-...

Problemas de práctica sugeridos

Problema de la vida _ Dificultad
Silencio------------
Silencio **Maximum Subarray Sum with Alternating Sign** TEN Medium TEN [LeetCode 1180](https://leetcode.com/problems/maximum-subarray-sum-with-alternating-sign/) Silencio
Silencio **Suma de Máximo de Dos Subarrayos No Sobresalientes** Silencio duro [LeetCode 689](https://leetcode.com/problems/maximum-sum-of-two-non-overlapping-subarrays/) Silencio
Silencio **Suma de Máximo de 3 Subarrayos No Desaparecidos** tención Medium [LeetCode 689](https://leetcode.com/problems/maximum-sum-of-3-non-overlapping-subarrays/) Silencio

-...

## 🔧 Final Thought

La parte “muy” de este problema es la gimnasia de signos: debe mantener un mango apretado en el que los índices son uniformes o extraños y voltear el signo en consecuencia. Una vez que dominas ese truco, el resto es un DP limpio pase con dos constantes – ** una entrevista clásica ganar**.

¡Feliz codificación! 🚀