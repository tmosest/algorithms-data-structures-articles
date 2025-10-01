-...
Título: LeetCode 375.
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 375 - Adivina número superior o inferior II
**Programación Dinámica Mastery en Java / Python / C++ – Una perspectiva de trabajo Guía lista**

■ **Keywords**: LeetCode 375, Adivina número superior o inferior II, programación dinámica, codificación de entrevistas, solución Java, solución Python, solución C++, estrategia óptima, memoización DP, entrevista de trabajo

-...

## 📌 Resumen del problema (LeetCode 375)

■ Estamos jugando un juego de adivinanzas:
El oponente elige un entero "x" en `[1, n]`.
Por todas las suposiciones equivocadas, pagas dólares.
- Después de cada conjetura se le dice si `x` es superior o inferior.
■
■ ** Objetivo**: Cumplir la cantidad mínima de dinero necesaria para *guarantee* una victoria para cualquier `n ' (es decir, el peor costo de la estrategia óptima).

**Constraints* *

- 1 ≤ 200.

-...

## ♥ Why This Problem Rocks a Job Interview

* Programación Dinámica* PD clásico con una subestructura óptima (reminiscencia del problema de la gota de huevo).
- Teoría del juego Requiere razonar sobre los peores escenarios.
*Conciencia de la complejidad* Debe reconocer que una solución ingenua es `O(n3)` mientras que el DP óptimo es `O(n2)`.
- **Idioma Agnostic**: Usted puede implementarlo en cualquier idioma; los reclutadores aprecian código idiomático limpio.

-...

## Solution Overview

### 1. Recurrencia

Dejar `dp[l][r]` sea la cantidad mínima necesaria para garantizar una victoria en el intervalo `[l, r]`.
Si `l == r`, no se necesita dinero (`dp[l][l] = 0`).

Por " I " , probamos todas las posibles primeras conjeturas:

`` `
cost(k) = k + max(dp[l][k-1], dp[k+1][r])
`` `

- Pagamos dólares por primera vez.
- Si la respuesta es menor, nos quedamos con `[l, k-1]`.
- Si la respuesta es más alta, quedamos con `[k+1, r]`.

Tomamos el mínimo sobre todo 'k':

`` `
dp[l] [r] = min_{k velocidad[l,r]} cost(k)
`` `

### 2. Estrategias de aplicación

TENIDO TERRIENTE Complejidad ANTERIOR Cuando se utiliza
Silencio----------------------------
tención **Recidivante desplegable + memoización** Silencio `O(n2)` tiempo, `O(n2)` espacio TENIDO código limpio; fácil de entender. Silencio
Silencio **Bottom-up DP** Silencio `O(n2)` tiempo, `O(n2)` espacio TENIDO Ligeramente más rápido en la práctica; bueno para entrevistas que requieren DP iterativo. Silencio
Silencio **Binary Search optimization** Silencio `O(n log n)` time, `O(n2)` space (still DP) ← Overkill for `n ≤ 200`. Silencio

Proporcionaremos soluciones específicas para idiomas**:

1. **Java** – Recursive + memoización (clase `Solution`).
2. **Python** – `functools.lru_cache` decorator (clase `Solution`).
3. **C+** – `vector seleccionadovector realizador DP table (class `Solution`).

-...

## 🔧 Code Implementations

### Java (Recursive + Memoization)

``java
*
* 375. Adivina número superior o inferior II
* Tiempo: O(n^2)
* Espacio: O(n^2)
*/
Solución de la clase pública {}
int privado[][] memo;

public int getMoney Cantidad(int n) {
memo = nuevo int[n + 2][n + 2]; //
dfs(1, n);
}

int privado dfs(int low, int high) {
si (bajo >= alto) retorno 0;
si (memo[low] [high] != 0) memo de retorno[low][high];

int best = Integer.MAX_VALUE;
para (incluye = bajo; adivinar = alto; adivina ++) {}
int cost = guess + Math.max(dfs(low, guess - 1),
dfs(gues + 1, alto));
mejor = Math.min (mejor, costo);
}
memo[low] [high] = best;
devolver mejor;
}
}
`` `

■ ¿Por qué memo? #
■ Sin ella, el mismo subintervalo sería recomputado muchas veces (exponential blow-up).
■ La mesa de memo reduce la complejidad a la cuadrática.

-...

### Python (Top‐Down DP with `lru_cache`)

``python
"
375. Adivina número superior o inferior II
Hora : O(n^2)
Espacio : O(n^2) (cache)
"

desde functools import lru_cache

Solución de clase:
def getMoneyAmount(self, n: int) - int:
@lru_cache(None)
def dp(l: int, r: int) - título int:
si l >= r:
retorno 0
mejor = flotante('inf')
para adivinar en rango(l, r + 1):
costo = adivina + max(dp(l,div - 1), dp(guess + 1, r)
mejor = min(mejor, costo)
mejor

retorno dp(1, n)
`` `

■ **Tip**: Use `@lru_cache` para evitar mesas de memo manuales – mantiene el código corto y pitónico.

-...

## C++ (Bottom‐Up DP)

``cpp
*
* 375. Adivina número superior o inferior II
* Tiempo: O(n^2)
* Espacio: O(n^2)
*/
Clase Solución {
public:
int getMoney Cantidad(int n) {
vector seleccionado(n + 2, 0)

para (int len = 2; len = n; ++len) { // longitud de intervalo
para (int l = 1; l + len - 1 י= n; ++l) {
int r = l + len - 1;
int best = INT_MAX;
para (int k = l; k)
int cost = k + max(dp[l][k - 1], dp[k + 1][r]);
mejor = min (mejor, costo);
}
dp[l][r] = best;
}
}
dp[1][n];
}
};
`` `

■ ¿Por qué? #
■ El bucle exterior construye intervalos de pequeño a grande, garantizando que todas las subintervalaciones ya se resuelven cuando sea necesario.

-...

## 🧪 Test Cases

TENIDA `n` Silencio esperada
Silencio--------------------------------
Silencio 1 Silencio 0 Silencio Sólo un número – sin costo. Silencio
Silencio 2 Silencio 1 Silencio Adivina 1 → costo 1 si es incorrecto. Silencio
Silencio 3 Silencio 2 Silencio Optimal primera conjetura 2: costo 2 + max(0,0) = 2. Silencio
Silencio 10 Silencio 16 Silencio Proporcionado en la declaración. Silencio
Silencio 200 Silencio 1079 Silencio Cálculo rápido - todavía rápido ( Entendido 0.01 s). Silencio

■ Ejecutar `python -m unittest` o similar a validar.

-...

El bueno, el malo, el feo

Silencio Silencio
Silencio------------Prince------
Silencio **Caso de base** ← Correctamente maneje `l √= r` → 0 costo TENIDO Olvídate de manejar `l == r` → respuesta incorrecta o bucle infinito ANTE Regresar un número negativo o grande para intervalos vacíos ANTE
Silencio **La complejidad** Silencioso `O(n2)` DP Silencio `O(n3)` recursión ingenua (exponencial) Silencio OOM o apilar el desbordamiento con recidiva profunda (no memo)
Silencio **Memoización** Silencio Usos 2‐D array o `lru_cache` Silencio Usando `HashMap` con el formato clave incorrecto ← Memo key collisions or missing entries Н
Silencio **Iterative vs Recursive** Silencio Bottom‐up da control explícito del orden de intervalo Silencio Top-down puede exceder la profundidad de recursión en otros idiomas Silencio Usar el estado mutable global incorrectamente

■ **Takeaway**:
■ *Siempre* identificar la recurrencia DP, implementar la memoización y probar con pequeños valores antes de escalar.

-...

## 📈 Complexity Analysis

Silencio Silencio Silencio Silencio Silencio
Silencio--------------
Silencio Top-down (Java / Python)
Silencio en el fondo (C++) Silencio

■ Con 'n ≤ 200', ambos enfoques funcionan en microsegundos.

-...

## 🎯 Interview Tips

1. ** Explique la recurrencia** antes de la codificación. Programador de amor para verlo razonar a través de sub-estructuras.
2. **Declarar el caso base** claramente (`l == r → 0`).
3. **Mención del tiempo / cambio de espacio** – usted puede discutir tanto recursión + memo o DP iterativo.
4. **Mostrar un ejemplo** (por ejemplo, `n = 10`) para ilustrar por qué funciona la fórmula.
5. **Optional**: talk about possible optimizations (e.g., binaria search to reduce internal loop to `O(log n)`), even if you don't implement them.

-...

## 🚀 Wrap‐Up

- El problema es un clásico rompecabezas de programación dinámica que prueba la recursión, la memoización y el razonamiento peor de caso.
- La solución óptima es **quadratic** en `n` y funciona hermosamente para `n ≤ 200`.
- Los snippets de Java, Python y C++ están listos para pegar a su editor o al juez en línea de LeetCode.
- Dominar este problema le da una base sólida para muchas preguntas de entrevista que implican ** estrategia óptima** o ** DP termorético del juego**.

¡Buena suerte en tu próxima entrevista de codificación!

-...

■ **Compartir** este artículo sobre Enlace En o GitHub para ayudar a otros y mostrar a los reclutadores que tiene bajo control este desafío dinámico de programación.