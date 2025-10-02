-...
Título: LeetCode 1567. Longitud máxima de subarray con producto positivo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1567. Longitud máxima de subarray con producto positivo
## Java, Python & C+ Soluciones + SEO-Optimized Blog Post

-...

## 📄 Problema general
Dado un conjunto entero `nums`, encontrar la longitud **maximum** de un **subarray contiguo** cuyo producto es **positivo**.
Un subarray es una rebanada consecutiva del array; puede contener cualquier número de elementos (incluyendo cero).

### Constraints
Silencio
Silencio...
TENIDO `1 ≤ nums.length ≤ 105` TENIDO `-109 ≤ nums[i] ≤ 109`

### Por qué este problema se mete
**Real-world relevance**: Similar a encontrar el tramo más largo de los datos “buenos” en las series temporales o las finanzas.
- *Entrevista de mina de oro* Muchos entrevistadores piden variaciones de esto para probar la comprensión de **DP**, **greedy** y **edge‐case handling**.
- LeetCode 1567**: Alto tráfico, dificultad media – perfecta para construir una cartera.

-...

## 🔍 Solution Insight – One‐Pass O(n), O(1) Space

### Observaciones clave

1. **Zero es un reset** – el producto se convierte en 0, así que empezamos a contar desde el siguiente elemento.
2. **Los números negativos cambian la paridad** – cada vez que vemos un negativo, un producto positivo se vuelve negativo y viceversa.
3. **Mantenga dos longitudes**
- `posLen` - longitud del subarray más largo que termina en el índice actual con un producto ** positivo**.
- `negLen` - longitud del extremo de subarray más largo en el índice actual con un producto **negativo**.

Actualizarlos depende de la señal del elemento actual.

#### Transition Rules

TENIDO Valor actual TENIDO Efecto sobre `posLen` Efecto involuntario en `negLen`
Silencio...
Silencioso `0` Silencioso para `0` Silencioso para `0`
Silencio positivo 1` Silencio `negLen = negligencia 0 negLen + 1 : 0` Silencio
Silencio Negativo Silencioso swap `posLen` ' negLen ' (después de añadir `1` a cada uno)

La respuesta es el máximo `posLen` visto durante el escaneo.

### Complexity

- **Tiempo**: `O(n)` - pase único sobre el array.
- **Espacio**: `O(1)` – sólo un puñado de variables enteros.

-...

## 📦 Code Implementations

### 1Ω⃣ Java (LeetCode-style)

``java
Clase Solución {
public int getMaxLen(int[] nums) {
int posLen = 0; // longitud del producto positivo subarray
int negLen = 0; // longitud del producto negativo subarray
int best = 0; // global best

para (int x : nums) {
(x == 0) {
posLen = 0;
negLen = 0;
} si (x 0) {
pos Len++;
negLen = negLen 0 ? negLen + 1 : 0;
} más { // x } 0
int oldPos = pos Len;
posLen = negLen 0 ? negLen + 1 : 0;
negLen = oldPos + 1;
}
mejor = Math.max(mejor, posLen);
}
devolver mejor;
}
}
`` `

### 2down⃣ Python (LeetCode-style)

``python
Solución de clase:
def getMaxLen(self, nums: List[int] int:
pos_len = 0
neg_len = 0
mejor = 0

para x en nums:
si x == 0:
pos_len, neg_len = 0, 0
elif x Ø 0:
pos_len += 1
neg_len = neg_len + 1 si neg_len 0 si no 0
# Negativo
pos_len, neg_len = (neg_len + 1 si neg_len œ 0 else 0), pos_len + 1
mejor = max(best, pos_len)

mejor
`` `

### 3down⃣ C++ (LeetCode-style)

``cpp
Clase Solución {
public:
int getMaxLen(vector fielint limitada nums) {
int posLen = 0, negLen = 0, best = 0;

para (int x : nums) {
(x == 0) {
pos Len = negLen = 0;
} si (x 0) {
posLen += 1;
negLen = negLen 0 ? negLen + 1 : 0;
} más { // negativo
int oldPos = pos Len;
posLen = negLen 0 ? negLen + 1 : 0;
negLen = oldPos + 1;
}
mejor = max(best, posLen);
}
devolver mejor;
}
};
`` `

Los tres snippets se ejecutan en **O(n)** tiempo y **O(1)** espacio, coincidiendo con la solución óptima en LeetCode.

-...

##  gradualmente Blog Post – “El Bien, el Mal, y el Ugly de 1567”

## Título (SEO‐Optimized)
**“Mastering LeetCode 1567 – El bueno, malo & ugly del subarray de la longitud máxima con producto positivo”* *

■ *Keywords*: LeetCode 1567, subarray de longitud máxima, producto positivo, prep de entrevista, solución Java Python C++, DP, algoritmo codicioso, entrevista de trabajo.

-...

#### Introduction

Si estás buscando ese “proxito gran problema de entrevista” para crack, no busques más que **LeetCode 1567**. Es un clásico *array + parity* puzzle que prueba tanto *time‐complexity awareness* como *edge‐case thinking*. En este post descifraremos el problema, exploraremos los pros y contras de enfoques comunes, y finalmente entregaremos ** tres implementaciones limpias y listas para la producción**.

-...

### The Good – Why Este problema es una Goldmine

TENIDO VALORACIÓN ANTERIOR ANTERIOR
Silencio...
Silencio **Simple Input** tención Sólo una sola matriz – ninguna estructura anidada. Silencio
Silencio **Clear Goal** Silencio Subarray más largo con un producto positivo – un objetivo fácil de establecer. Silencio
Silencio **Multiple Solution Paths** Silencio Puedes resolverlo con DP, codicioso, o incluso dividir–y conquistar – gran para mostrar amplitud. Silencio
Silencio ** Alto Relevancia** Silencio La lógica del “reset on cero” y “flip on negative” aparece en muchos escenarios del mundo real (procesamiento de firmas, análisis de stock, etc.). Silencio
Silencio **LeetCode Traffic** Silencio Alto volumen de búsqueda → perfecto para mostrar en su cartera o GitHub. Silencio

-...

### Los malos – saltos comunes

1. **Misunderstanding the Product Sign**
*Muchos principiantes erróneamente piensan que un número negativo gira *ambos* longitudes. *
2. *Ignorando Cero*
*Skipping the reset leads to incorrect subarray lengths. *
3. ** Complejidad espacial extraordinaria**
*Some DP solutions use two arrays (`dpPos`, `dpNeg`) – unnecessary when a single pass suffices. *
4. ** Casos de emergencia**
*Número total negativo, todos los ceros o la longitud de la matriz 1 – prueba siempre estos antes de enviar. *

-...

### Los enfoques Ugly – Ineficientes o de mayor intensidad

Por qué es Ugly
Silencio...
Silencio **Brute‐Force O(n2)** Silencio Enumerating all subarrays, recomputing product each time – far too slow for `105` length. Silencio
Silencio **Full DP Tables** Silencio `dpPos[i]`, `dpNeg[i]` arrays → O(n) space that can be avoided. Silencio
Silencio **Recursive Backtracking** Silencio La recursión profunda puede alcanzar límites de pila en grandes entradas. Silencio
Silencio **Mis‐Typed Sign Check** tención Usando `abs(x) % 2` en lugar de `x  realizadas 0` puede llevar a la desbordación cuando `x = -109`. Silencio

-...

### Step‐by‐Step Walkthrough (Dry Run)

Considerar `nums = [1, -2, -3, 4]`:

Silencio idx tóxico valor Silencio pos Len  negLen
Silencio...
Silencio 0 Silencio 1 Silencio 1 Silencio 0 Silencio
Silencio 1 Silencio -2 Silencio 0 Silencio 2 Silencio
Silencio 2 Silencio -3 Silencio 3 Silencio 0 Silencio 3
Silencio 3 Silencio 4 Silencio 4 Silencio 0 Silencio 4

La longitud máxima positiva del producto subarray es **4** – toda la matriz.

-...

## Código-Ley Implementaciones

*(Proporcionado anteriormente en este documento)*
■ Cada solución utiliza un solo pase, mantiene sólo tres enteros, y funciona en tiempo lineal.

-...

### SEO Take-away

- **Use Headers with Palabras Clave**: “LeetCode 1567”, “maximum length subarray”, “producto positivo”.
- **Insert Code Snippets**: Search engines love code-rich content.
- **Añadir Meta Descripción**: "Solve LeetCode 1567 en Java, Python, y C++ con un algoritmo codicioso O(n). Lea el artículo completo para dominar DP y trucos codiciosos para entrevistas de trabajo. ”
- Link Back**: Insertar un enlace al problema LeetCode y a tu repositorio GitHub.

-...

### Closing Thoughts

Mastering **LeetCode 1567** demuestra:

- Capacidad para *detectar y explotar patrones* (señales volteretas, reajustes).
- *Intuición de intercambio a tiempo parcial* (O(1) vs O(n)).
- Versatilidad entre idiomas (Java, Python, C++).

Comparte estas implementaciones en tu portafolio, discute los cambios en tu entrevista, y te destacarás como un pensador algorítmico muy completo** listo para el próximo trabajo tecnológico.

Feliz codificación, y buena suerte en su viaje de entrevista! 🚀

-..