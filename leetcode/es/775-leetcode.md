-...
Título: LeetCode 775. Inversiones globales y locales -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Global vs. Local Inversions – LeetCode 775
### El problema “Permutación Ideal” (Java, Python & C++)

■ *Problema* – LeetCode 775
■ Dada la permutación `nums ' de longitud `n ' (valores `0 ... n‐1`), devuelve `true ' si el número de inversiones globales equivale al número de inversiones locales.

-...

## 1. La Solución de una línea (O(n) tiempo, espacio O(1))

La visión clave:

*Cada inversión global también debe ser una inversión local. *
Si algún elemento se desplaza por más de una posición de su índice “ideal”, aparecerá una inversión global no local y los conteos nunca pueden ser iguales.

Así, el cheque reduce a:

``text
abs(nums[i] - i)
`` `

Si la condición tiene para todos los índices, devuélvete `verdad ' ; de lo contrario `falso ' .

## Java

``java
Solución de la clase pública {}
booleano público isIdealPermutation(int[] nums) {
para (int i = 0; i)
si (Mat.abs(nums[i] - i) 1) {
devolver falso;
}
}
retorno verdadero;
}
}
`` `

## Python

``python
Solución de clase:
def isIdealPermutation(self, nums: List[int]) - ratio bool:
devolver todo(abs(nums[i] - i) י= 1 para i en rango(len(nums)))
`` `

### C++

``cpp
Clase Solución {
public:
bool isIdealPermutation(vector identificadoint limitada nums) {
para (int i = 0; i) ++i) {
(abs(nums[i] i) " 1) devolver falso;
}
retorno verdadero;
}
};
`` `

■ ** Complejidad del tiempo** – `O(n)` (single scan)
■ ** Complejidad del espacio** – `O(1)` (en lugar)

-...

## 2. The Brute‐Force “Good” – Cuando usted necesita una referencia

Un bucle doble ingenuo `O(n2)` puede ser útil para depurar o cuando el tamaño de la matriz es pequeño.

``java
int local = 0, global = 0;
para (int i = 0; i < n - 1; i++) si (nums[i] не nums[i+1]) local++;
para (int i = 0; i)
para (int j = i+1; j)
si global++;
retorno local == global;
`` `

*Pros:* Fácil de entender, sin trucos ocultos.
*Cons:* Demasiado lento para `n = 105`. Úsalo solo para casos de prueba pequeños o como cheque de cordura.

-...

## 3. El Enfoque Optimal – “El Ugly” de Over-Engineering

Algunas soluciones principales utilizan un truco *prefix‐maximum* para detectar una inversión global no local sin el control absoluto. La idea:

``text
Si max(nums[0..i]) > nums[i+1] → inversión global no local.
`` `

Aunque elegante, añade un pequeño poco de librería extra y es menos intuitivo que el control absoluto de distancia. Para los entrevistadores, se prefiere la solución más simple `abs(nums[i] - i).

-...

## 4. Por qué este problema importa en las entrevistas

1. ** Insight Algoritmico** – Muestra la capacidad de pensar en las permutaciones y propiedades de inversión.
2. **Constant‐Space Optimisation** – Demuestra que el espacio O(1) suele ser suficiente.
3. **Código Cleno** – La lógica de una línea puede impresionar cuando se presenta con el razonamiento adecuado.
4. **Multi‐Language Mastery** – Ser capaz de escribir la misma lógica en Java, Python y C++ demuestra versatilidad.

-...

## 5. SEO‐Friendly Blog Post Esquema

A continuación se muestra un artículo completo que se puede pegar en un blog mediano, Dev.to, o una cartera personal. El contenido es rico en palabras clave, estructurado para la legibilidad, e incluye una meta descripción para la máxima visibilidad.

-...

# 🏁 Blog Post: “Global vs. Inversiones locales – Cómo Crack LeetCode 775 en Java, Python & C+”

**Meta Descripción (para motores de búsqueda)* *
■ Master LeetCode 775 – Global vs. Inversiones locales. Aprenda el truco ideal de permutación, lea una solución Java, Python " C+++ " , y entienda por qué es necesario saber para entrevistas de ingeniería de software.

-...

## 📚 Introduction

Si usted ha estado molendo LeetCode, probablemente se ha topado con **LeetCode 775 – Global vs. Inversiones locales**. Es engañosamente simple: una permutación de `0...n‐1`, comprobar si las inversiones globales equivalen a inversiones locales. Sin embargo, este pequeño problema es un *clasic entrevista pet-project* que puede mostrar su pensamiento algorítmico y darle una rápida victoria de entrevista.

¿Por qué es útil?
- ** Fundamentos de permutación** – Las inversiones son un concepto básico de clasificación y análisis de algoritmos.
- *Una elegancia de línea* – Los entrevistadores aman soluciones limpias, O(n) que funcionan en espacio constante.
- Pensando en el maletín... Encontrar que un valor debe permanecer dentro de un índice lejos de su punto "ideal" le entrena para detectar restricciones ocultas.

Caminemos por las partes *buena*, *bad* y *muy* de este problema, mostremos cómo implementarlo en Java, Python y C++, y terminaremos con consejos de entrevista.

-...

## 🔍 Declaración de problemas (Restated)

Se le da un array `nums` de longitud `n` que es una permutación de '0 ... n‐1`.
- **Inversión global** – par `(i, j)` donde `i cauté j` y `nums[i] œ nums[j]`.
*Inversión local* – par `(i, i+1)` donde `nums[i] не nums[i+1]`.

Regresar 'verdad' si ** inversiones globales = inversiones locales**.

-...

## 5down Naïve Brute‐ Fuerza (bueno pero lento)

``java
int local = 0, global = 0;
para (int i = 0; i < n-1; i++) si (nums[i] не nums[i+1]) local++;
para (int i = 0; i)
para (int j = i+1; j)
si global++;
retorno local == global;
`` `

- Fácil de seguir, sin matemáticas difíciles.
- **Bad**: O(n2) - será el tiempo libre para 'n = 100.000'.
No escalable, pero bueno para pruebas de cordura.

-...

## ❌ The One‐liner – The “Good” Optimal Solution

**Observación** – En una permutación, el índice “ideal” del valor “v” es “v” mismo.
Si un valor se mueve más de un lugar, usted crea una inversión global que es *no* local.

Entonces:

``text
Silenciosos[i] – yo vivo
`` `

Si la condición se mantiene en todas partes, las inversiones locales y globales coinciden.

#Java #

``java
booleano público isIdealPermutation(int[] nums) {
para (int i = 0; i)
si (Mat.abs(nums[i] i) " 1) devolver falso;
}
retorno verdadero;
}
`` `

Python

``python
devolver todo(abs(nums[i] - i) י= 1 para i en rango(len(nums)))
`` `

**C++**

``cpp
para (int i = 0; i) ++i)
(abs(nums[i] i) " 1) devolver falso;
retorno verdadero;
`` `

- *Hora*
- **Espacio**: `O(1)`

Este es el enfoque óptimo *bueno*: rápido, sencillo y utiliza sólo una cantidad constante de memoria.

-...

##  tuya La alternativa “Ugly”: Prefix‐Maximum Check

Algunas soluciones mantienen el valor máximo visto hasta ahora:

``text
si (max_so_far > nums[i+1]) → inversión global no local.
`` `

``cpp
int max_so_far = INT_MIN;
para (int i = 0; i)
si (max_so_far > nums[i+1]) devuelve falso;
max_so_far = max(max_so_far, nums[i]);
}
retorno verdadero;
`` `

- **Pros**: No hay llamada "abs", un poco de lógica extra.
- **Cons**: Menos legible, requiere pensar en el prefijo maxima.
- **Cuándo usar**: Cuando usted desea evitar `abs()` en un entorno de entrevista que penaliza las llamadas matemáticas, pero la línea única es generalmente más fácil de entrevistar.

-...

## 📈 Complexity Summary

Silencio Silencio Silencio Silencio Silencio
Silencio--------------------------
Silencio Absolute‐distance one‐liner Silencio O(n) Silencio O(1) Silencio
Silencio Prefix‐maximum Silencio O(n) Silencio O(1) Silencio
Silencio Brute‐force

-...

## 🛠ف Common Pitfalls > Edge‐ Lista de verificación de casos

Silencio Pitfall Silencio
Silencio...
**Usando " título " en lugar de `` La condición debe ser *strictamente* ``traducido= 1`. ← Uso `Math.abs(nums[i] - i) " 1 " (Java) o "abs(nums[i] - i) " 1 " (Python/C++). Silencio
Silencio **Overflow** – `abs()` on `Integer.MIN_VALUE` es problemático en Java. Silencio Seguramente compute `Math.abs(nums[i] - i)`; los valores están dentro de `[0, n-1]`, por lo que nunca ocurre la desbordación. Silencio
Silencio **Misreading “local” vs “global”** – Local siempre está entre índices consecutivos. Silencio Doble-verifique su definición si implementa la fuerza bruta-fuerza. Silencio
*Testing on empty array** – Problem guarantees `n ≥ 1`, but guard against `nums.length == 0`. Silencio Añadir un trivial `si (nums.length == 0) Retorno verdadero; " . Silencio

-...

## 🎯 Interview‐Ready Tips

1. **Explicar la información primero** – “Todas las inversiones globales no locales requieren un elemento para ser desplazado por √° 1.”
2. **Mostrar el simple código O(n)** – Evite la complejidad innecesaria.
3. **Hora de la mención/espacio** – Los entrevistadores siempre quieren un gran O resumen.
4. **Pregunte aclarando preguntas** – por ejemplo, “¿El array es siempre una permutación?” para evitar el trabajo perdido.
5. **Optional: Show the brute‐force** – Helps demonstrate that you understand the problem definition fully.

-...

## 📢 SEO Checklist

Silencio Palabra clave Silencio
Silencio...
Silencioso LeetCode 775 Silencio Título, intro, problema afirmativo
← Global vs. Local Inversions ← A lo largo de todo, especialmente en explicación
tención Ideal Permutación Silencioso sección Problema, solución comentarios ←
Silencio Java solución Н Java code header Н
← Solución Python
Silencio C++ Solución Silencio C++
TENCIÓN TERRITORIO TENCIÓN, entrevista consejos
Silencioso entrevista de ingeniero de software
← Entrevista Algorítmica TENIDO Meta descripción, encabezados ANTE

**Meta Descripción (para motores de búsqueda): * *
■ Crack LeetCode 775 – Global vs. Inversiones locales. Lea la solución O(n) “Permutación Ideal” en Java, Python y C++ con una explicación clara, análisis de tiempo/espacio y consejos de entrevista. Perfecto para entrevistas de ingeniería de software.

-...

Pensamientos finales

El problema te obliga a razonar sobre las permutaciones y los recuentos de inversión.
- **Bad** – Una solución ingenua `O(n2)` es demasiado lenta para las limitaciones pero es excelente para el aprendizaje.
- **Ugly** – La sobreingeniería con árboles prefijo-max o binario indexados hace que el código sea menos legible; manténgalo simple.

Al dominar el One-liner, usted será capaz de **solve LeetCode 775 en una entrevista** en menos de 30 segundos e impresionar al entrevistador con una solución limpia y óptima.

¡Feliz codificación y buena suerte aterrizando ese próximo papel de ingeniería de software!