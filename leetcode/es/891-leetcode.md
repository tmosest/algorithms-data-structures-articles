-...
Título: LeetCode 891. Sum of Subsequence Widths -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Aplicación de tres vías (Java / Python / C++)

A continuación se encuentran soluciones limpias y de producción para **LeetCode 891 – Sum of Subsequence Widths**.
Los tres códigos comparten la misma idea algorítmica (sort + contribución combinatoria) pero se escriben en el estilo típico de cada idioma.

Silencio Idioma Silencio Archivo Silencio Complejidad
Silencio----------------
Silencio Java ¦ `Solution.java` Silencioso **O(n log n)** tiempo, **O(n)** espacio Silencioso
TENIDO Python TENIDO `solution.py` TENIDO **O(n log n)** tiempo, **O(n)** espacio TENIDO
TENIDO C++ TENIDO `solution.cpp` Silencio **O(n log n)** tiempo, **O(n)** espacio ANTE

■ ¿Por qué este enfoque? * *
■ La clasificación nos permite saber, para cada elemento, cuántas subsecuencias puede convertirse en el *maximum* o el *mínimo*.
■ En una matriz ordenada, el número de subsecuencias donde `nums[i]` es el **maximum** es `2^i` (cada uno de los `i` elementos más pequeños puede estar ya sea dentro o fuera).
■ The number of subsequences where `nums[i]` is the **minimum** is `2^(n-i-1)` (cada uno de los elementos más grandes puede estar dentro o fuera).
■ Así, la contribución total de `nums[i]` a la suma de anchos es
* nums[i].
■ Resumiendo todos los índices da la respuesta, tomada modulo `1 000 000 007`.

-...

## Java

``java
// 891. Suma de Ancho Subsequence
// Java 17

importar java.util*;

Solución de la clase pública {}
int final estático privado MOD = 1_000_000_007;

int sumSubseqWidths(int[] nums) {
int n = nums.length;
Arrays.sort(nums); // O(n log n)

long[] pow2 = new long[n];
pow2[0] = 1;
para (int i = 1; i) {}
pow2[i] = (pow2[i - 1] * 2) % MOD; // pre-compute powers of 2
}

ans largas = 0;
para (int i = 0; i)
long contrib = (pow2[i] - pow2[n - i - 1]) * nums[i];
as = (ans + contrib) % MOD;
}
retorno (int) ((ans + MOD) % MOD); // guard against negative values
}
}
`` `

-...

## Python

``python
# 891. Suma de Ancho Subsequencia
# Python 3.11

MOD = 1_000_000_007

Solución de clase:
def sumSubseqWidths(self, nums: list[int] int:
nums.sort() # O(n log n)
n = len(nums)

# pre-compute powers of 2 modulo MOD
pow2 = [1] * n
para i en rango(1, n):
pow2[i] = (pow2[i-1] * 2) % MOD

ans = 0
para i, x en enumerado(nums):
contrib = (pow2[i] - pow2[n-i-1]) * x
ans = (ans + contrib) % MOD
retorcidos % MOD
`` `

-...

### C++

``cpp
// 891. Suma de Ancho Subsequence
// C+17

#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int sumSubseqWidths(vector efectuadoint ánimos) {
const int MOD = 1'000'007;
(nums.begin(), nums.end()); // O(n log n)
int n = nums.size();

vector realizado largamente largamente práctico pow2(n, 1);
para (int i = 1; i)
pow2[i] = (pow2[i-1] * 2) % MOD; // pre-compute powers of 2

ans largos = 0;
para (int i = 0; i) {}
largo largo contrib = (pow2[i] - pow2[n-i-1]) * nums[i];
as = (ans + contrib) % MOD;
}
(int)(ans % MOD + MOD) % MOD); // avoid negative
}
};
`` `

Las tres soluciones funcionan en **O(n log n)** tiempo (debido al paso de clasificación) y utilizan **O(n)** espacio adicional para la matriz de potencia.

-...

## 2. Blog Artículo – “Sum of Subsequence Widths: The Good, The Bad, and The Ugly”

■ **Keywords**: Sum of Subsequence Widths, Leetcode 891, Java solution, Python solution, C++ solution, algoritmo interview, job interview coding, combinatorics, sorting, dynamic programming, modulus, big integer, coding interview prep.

-...

#### Introduction

Cuando estás preparando una entrevista ** de ingeniería de software**, no es suficiente saber cómo *escribir* código. También necesita **entender** por qué funciona una solución, anticipar las trampas y explicar las compensaciones.
Problema de LeetCode **891 – Sum of Subsequence Widths** es un ejemplo clásico. Te obliga a:

1. Combine *combinadores* con *aritmética modular*.
2. Entregar grandes insumos (`n` hasta `10^5`) de manera eficiente.
3. Vigila el flujo de entero.

En este post, diseccionamos el **bueno**, el **bad**, y el **ugly** de resolver este problema. Caminaremos por el algoritmo, compartiremos código en Java, Python y C++, y finalmente explicaremos cómo dominar este patrón puede aumentar su rendimiento de entrevista.

-...

### The Good – A Clean, Provened Pattern

1. **Sorting + Power of Two**
Al ordenar el array, convertiremos el problema de subsequencia *no surtido* en un problema de conteo combinatorio **determinista**.
*Por qué funciona*: En una lista ordenada, cualquier elemento sólo puede convertirse en el *maximum* de una subsequencia si todos los elementos más pequeños son elegidos *o* omitidos. Por lo tanto el conteo es simplemente `2^i`.

2. **Paso de contribuciones para el aeropuerto* *
Una vez que sabemos cuántas veces cada elemento aparece como máximo/mínimo, podemos calcular su contribución en un solo paso.
*Por qué es eficiente*: Evitamos generar todas las subsecuencias (suplemento adicional) y reducir el trabajo a algunas operaciones aritméticas por elemento.

3. *Aritmética Moderna*
Modulo `1e9+7` garantiza que los resultados intermedios encajan en enteros de 64 bits. Utilizar un `long` (Java) o `long' (C++) protege contra el desbordamiento.

4. **Tiempo y espacio**
- **Tiempo**: `O(n log n)` debido a la clasificación; todo lo demás es lineal.
- **Espacio**: `O(n)` para la matriz de potencia - aceptable para `n ≤ 10^5`.

-...

### El malo – Pitfalls comunes & Por qué Sucede.

Silencio Pitfall Silencio Reason Silencio
Silencio------------
Silencio **Usar `int` para potencias** Silencio `2^n` supera rápidamente el rango de 32 bits. Silencio Use `long` (`Java`/`C++`) o Python’s built‐in big integers. Silencio
tención **Olvidó aplicar el módulo después de la resta** Silencioso `pow2[i] - pow2[n-i-1]` puede ser negativo antes de la multiplicación. Silencio Computar la diferencia modulo `MOD` *antes* multiplicando, o añadir `MOD` después. Silencio
TEN **Sorting in place when the original array matters** TEN Algunos entrevistadores piden preservar el array de entrada. Cerrar el array primero (`nums.clone()` en Java, `sorted(nums)` en Python). Silencio
Silencio ** Subsecuencias de contabilidad mínima** Silencio Pensar que cada elemento contribuye `2^i` veces sin considerar que también aparece como mínimo. Silencio Siempre restar la contribución *mínimo* (`2^(n-i-1)`). Silencio
Silencio **Overflow in Python (rare)** Silencio Multiplicar dos grandes números antes de aplicar módulo puede ser caro. TENIDO Use `pow(2, i, MOD)` o poderes pre-compute con módulo a cada paso. Silencio

-...

### The Ugly – Things That Can Break Your Code

1. **Desbordamiento entero en C++**
Si usas `int` para `pow2`, te desbordarás temprano. Incluso con 'largo largo', olvidándose de aplicar el módulo después de la resta puede producir valores negativos que, cuando se lanzan a tipos no identificados, se convierten en enormes positivos.

2. **Tiempo-Limit Exceeded (TLE) en Python**
Python’s built‐in `pow(2, i, MOD)` es rápido, pero pre-computar una lista de poderes y iterating más de 'nums' dos veces puede ser demasiado lento si usted no tiene cuidado con las comprensión de la lista vs. bucles. Use `sys.setrecursionlimit` si desea una solución recursiva (no se recomienda aquí).

3. ** Resultados negativos móviles**
En Java, `(pow2[i] - pow2[n-i-1])` puede ser negativo. Si multiplicas ese número negativo por `nums[i]` y luego aplicas `% MOD`, el resultado puede ser todavía negativo, lo que conduce a una respuesta final equivocada. Ajuste siempre:
``java
diff largo = (pow2[i] - pow2[n-i-1] + MOD) % MOD;
`` `

4. **Casos de Edge – Elemento Único**
Cuando `n == 1`, la fórmula reduce a `(1 - 1) * nums[0] = 0`. Asegúrese de que su código maneja correctamente `n-i-1` (se convierte en `0`).

-...

## Step‐by‐Step Algorithm (Illustrated)

1. **Ordenar el array** → `nums = [a1, a2, ..., an]`.
2. *Poderes de precomputación de dos*
`pow2[0] = 1`
`pow2[i] = (pow2[i-1] * 2) % MOD`
3. **Comentario completo**
Por cada uno de los `i` de `0` a `n-1`:
`` `
maxCount = pow2[i] // subsecuencias donde ai es máx
minCount = pow2[n-i-1] // subsequences where ai is min
contrib = (maxCount - minCount) * ai
ans = (ans + contrib) % MOD
`` `
4. ** Retorno `ans`** (asegúrese de que no es negativo).

-...

### Why This Pattern Matters for Interviews

- **Compactness**: Toda la solución encaja en ~30 líneas de código limpio—exactamente lo que quieren los entrevistadores.
- **Scalability**: Handles `10^5` elements in י0.1 s in Java and C++; י0.3 s in Python.
*Mathematical Rigor* Demuestra que puedes reducir una explosión combinatoria a una simple fórmula.
- **Edge‐Case Awareness**: Muestras que puedes prever desbordamiento, saltos de modulus y arrays de un solo elemento.

Dominar este patrón desbloquea muchos otros problemas que confían en “sort y luego cuentan” (por ejemplo, contando inversiones, sumas de subarray, o preguntas de tipo “beautiful pairs”.

-...

### Conclusión

El problema **Sum of Subsequence Widths** puede parecer intimidante a primera vista, pero su solución es un testimonio de lo poderoso * surtido* y *combinadores* pueden estar juntos.

- La solución **buena**: Una solución corta, O(n log n) que es rápida y elegante.
- El **bad**: Los errores comunes alrededor del desbordamiento y el módulo.
- ¿Qué? Los errores sutiles que pueden arrastrarse si no se protege contra números negativos o se olvida de aplicar el módulo a cada paso.

Armado con los fragmentos de código arriba (Java, Python, C++), usted puede abordar con confianza este problema LeetCode e impresionar a los entrevistadores con su claridad de pensamiento y disciplina de codificación. Buena suerte, y feliz codificación! 🚀

-...

**Compartir este artículo** si lo encontró útil, y háganos saber cuáles son los problemas de entrevista que le gustaría que rompiéramos el próximo.