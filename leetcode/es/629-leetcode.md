-...
Título: LeetCode 629. K Inverse Pairs Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código de Solución

A continuación encontrarás implementaciones limpias y listas para copiar en **Java**, **Python** y **C+** que resuelven LeetCode 629 – *K Inverse Pairs Array*.

■ **Recapto de problemas* *
" Dados " y " , cuentan las permutaciones de " [1...n] " que contienen exactamente 'k' pares inversos.
■ Devuelve el modulo de respuesta `109+7`.

### 1.1 Java – Rolling DP (O(n k) time, O(k) space)

``java
- 629. K Parejas inversas Array
// Java – Rolling DP, O(n*k) time, O(k) space

Solución de la clase pública {}
int final estático privado MOD = 1_000_000_007;

int kInversePairs(int n, int k) {
int[] dp = nuevo int[k + 1]; // dp[j] – #ways for current i with j pairs
dp[0] = 1; // base: 0 elementos → 1 manera ( array vacío)

para (int i = 1; i) = n; i++) {
int[] next = nuevo int[k + 1];
siguiente[0] = 1; // sólo 1 permutación con 0 pares para cualquier i
para (int j = 1; j)
// dp[j] – dp[j-i] (si j-i ю= 0)
int sub = (j - i) >= 0 ? dp[j - i] : 0;
int val = (dp[j] - sub + MOD) % MOD; // temp value for this j
siguiente[j] = (next[j - 1] + val) % MOD; // prefijo sum trick
}
dp = siguiente; // pasar al siguiente i
}

// dp[k] contiene la suma de dp[0.k], subtract dp[k-1] para obtener exactamente k
int result = (dp[k] - (k ≤ 0 ? dp[k - 1] : 0) + MOD) % MOD;
Resultado de retorno;
}
}
`` `

### 1.2 Python – Rolling DP (O(n k) time, O(k) space)

``python
# 629. K Parejas inversas Array
# Python 3 – Rolling DP, O(n*k) time, O(k) space

MOD = 1_000_000_007

def k_inverse_pairs(n: int, k: int) int:
dp = [0] * (k + 1)
dp[0] = 1 caja base

para i en rango(1, n + 1):
nxt = [0] * (k + 1)
nxt[0] = 1
para j en rango(1, k + 1):
sub = dp[j - i) if j - i mento= 0 si no 0
val = (dp[j] - sub) % MOD
nxt[j] = (nxt[j - 1] + val) % MOD
dp = nxt

# exact k pairs
(dp[k] - (dp[k - 1] if k √≥ 0 else 0) % MOD
`` `

### 1.3 C++ – Rolling DP (O(n k) time, O(k) space)

``cpp
- 629. K Parejas inversas Array
// C+17 – Rolling DP, O(n*k) time, O(k) space

#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int kInversePairs(int n, int k) {
const int MOD = 1'000'007;
vector implicado dp(k + 1, 0), nxt(k + 1, 0);
dp[0] = 1; // base case

para (int i = 1; i) = n; ++i) {}
[0] = 1;
para (int j = 1; j)
int sub = (j - i >= 0) ? dp[j - i] : 0;
int val = (dp[j] - sub + MOD) % MOD; // temp value
nxt[j] = (nxt[j - 1] + val) % MOD; // prefijo suma trick
}
dp.swap(nxt); // pasar al siguiente i
}

int result = (dp[k] - (k ≤ 0 ? dp[k - 1] : 0) + MOD) % MOD;
Resultado de retorno;
}
};
`` `

Las tres implementaciones se ejecutan en el tiempo de `O(n k)` y `O(k)` espacio auxiliar, que se ajusta fácilmente a las limitaciones (`n, k ≤ 1000`).

-...

## 2. Blog Artículo – “El Bien, el Mal, y el Ugly de K‐Inverse‐Pairs”

■ **Keywords:**
" K Inverse Pairs Array " , `LeetCode 629 ' , `dinamic programming ' , `DP optimization ' , `coding interview`, `Java ' , `Python ' , `C++ ' , `algorithm interview ' , `LeetCode Hard `

#### 2.1 Introduction

Si te estás preparando para una entrevista técnica o para un campo de arranque de estructuras de datos y algoritmos (DSA), te encontrarás en **LeetCode 629 – K Inverse Pairs Array** con bastante frecuencia. Es un problema *Hard* que te obliga a pensar más allá de la recursión ingenua y la fuerza bruta. En este post diseccionaremos el problema, caminaremos a través de una solución **disnamic-programming**, exploraremos las trampas comunes (el *bad*), y revelaremos un truco **optimizado lineal** (el *bueno*). Por último, hablaremos de cómo dominar este problema puede separarlo en un oleoducto de contratación.

■ **Lea el tutorial completo en el sitio oficial LeetCode:** https://leetcode.com/problems/k-inverse-pairs-array/

-...

### 2.2 Problema Recap

■ **Given** un entero 'n' y un entero 'k', devolver el número de permutaciones de `[1 ... n]` que contienen **exactamente 'k' pares inversos**.
■ Un par ** inverso** es un par `(i, j)` donde `i cauté j ' y `nums[i] не nums[j]`.
■ La respuesta debe ser devuelta modulo `1,000,000,007`.

■ *Examples*
1. `n = 3, k = 0` → `1` (sólo `[1,2,3]`)
2. `n = 3, k = 1` → `2` (`[1,3,2]`, `[2,1,3]`)

-...

### 2.3 The Brute‐Force “Bad” Approach

Un primer pensamiento es generar todas las permutaciones, contar pares inversos y filtrar. Para `n = 10' esto ya es astronómico (`3.6M` permutaciones). Incluso con la memoización, contar pares inversos para cada permutación sería `O(n2)` por permutación – claramente infeasible para las limitaciones (`n, k ≤ 1000`).

■ *Por qué falla*
- Tiempo de exposición (`O(n!)`).
√ - Soplamiento espacial debido a las permutaciones de almacenamiento.
√ - Mala escalabilidad: el algoritmo se encuentra bien antes de los casos oficiales de prueba.

Así que necesitamos un algoritmo de tiempo polinomio. Ahí es donde ** programación dinamica** pasos en.

-...

### 2.4 The DP “Good” – The Classic 2‐D Recurrence

Let `dp[i][j]` = number of permutations of the first `i` numbers (`1...i`) that have exact `j` inverse pairs.

**Transición* *

Cuando insertamos el número `i` en una permutación de `1...i-1`, el nuevo elemento puede aterrizar en cualquier posición `p` (1-basado). Creará 'p-1' nuevos pares inversos porque será más grande que todos los elementos a su izquierda. Así:

`` `
dp[i][j] = Governing_{p=1} {i} dp[i-1][j-(p-1)]
`` `

Simplifique el índice de cambio: " q = p-1 " , "  Iberia [0, i-1] " :

`` `
dp[i] [j] = Governing_{q=0}{min(i-1, j)} dp[i-1][j-q]
`` `

**Casos de base**

`` `
dp[0] [0] = 1 // permutación vacía
dp[0][j] = 0
`` `

**La complejidad* *

- Tiempo: `O(n * k * n)` → `O(n2 k)` (porque la suma interna corre hasta `i`).
- Espacio: `O(n * k)` para una mesa 2-D completa.

Si bien esto resuelve el problema, todavía es demasiado lento para `n = k = 1000`. Necesitamos una recurrencia más inteligente.

-...

### 2.5 The “Good” – Prefix Sum Optimization (O(n k))

Observe que la transición es un **convolución** de la fila anterior con una ventana corredera de ancho `i`. Podemos evitar la suma interna usando un truco **prefijo suma**:

Escribamos la recurrencia como:

`` `
dp[i][j] = dp[i][j-1] + dp[i-1][j] - dp[i-1] [j-i]
`` `

Explicación:

- `dp[i][j-1]` ya contiene todas las permutaciones donde el último elemento insertado creó ≤ `j-1` nuevos pares.
- Adding `dp[i-1][j] anexa un caso donde el último elemento crea exactamente `0` nuevos pares.
- El subtract `dp[i-1][j-i]` elimina el recuento en el que el nuevo elemento crearía más que pares ' i-1 ' (es decir, ' p ' i ' ).

Todas las operaciones se realizan modulo `M`.

#Rolling Array #

Puesto que `dp[i][*]` depende solamente de `dp[i-1][*]`, podemos mantener dos arrays 1-D:

``text
prev[j] – dp[i-1][j]
curr[j] – dp[i][j]
`` `

Y después de cada bucle exterior los cambiamos. Esto reduce el espacio a `O(k)`.

Paso final**

Después de construir hasta `i = n`, `dp[n][k]` realmente tiene el número **cumulativo** de permutaciones con ≤ `k` pares inversos debido al truco de prefijo-sum. Para obtener exactamente 'k', restar el valor anterior:

`` `
respuesta = dp[n][k] - dp[n][k-1] (mod M)
`` `

-...

### 2.6 El “Ugly” – Pitfalls comunes

Silencio Pitfall Silencio Por qué Sucede
Silencio...
Silencio ** Modulo negativo** Silencioso `dp[i-1][j] - dp[i-1][j-i]` puede ser negativo Silencio
Silencio ** Index Out‐of-Bounds** Silencio `j-i 0 ` or `j-i 0` in Python/Java  durable Guard with `if (j-i  entusiasta= 0)` Silencio
Silencio **Desbordamiento de enteros en C+** puede exceder " Silencio Uso " largo " o arrojado a " largo tiempo " antes de " Silencio "
Silencio **Límite de tiempo debido a la ingenua bucles 3-D** latitud O(n3) en Python debido a la comprensión de la lista.
Silencio ** Caso de base inquietante** Establecer todo el array a `0` luego `dp[0] = 1` TEN
Silencio **No intercambiar arrays** Silencio Después de cada `i`, `prev ' y `curr` se mezclan Silencio `prev.swap(curr)` (C++), `dp = nxt` (Java/Python) Silencio

-...

### 2.7 Takeaway: Why Solving 629 Matters

1. **Mostrar DP Mastery** – Muchos problemas de LeetCode “Hard” giran alrededor del DP. Demostrar una recurrencia correcta y una optimización inteligente indica una comprensión profunda de las transiciones estatales.
2. **Mathematical Insight** – Reconociendo la propiedad de la ventanilla deslizante y utilizando sumas prefijo destaca la intuición matemática – un rasgo apreciado para entrevistas de diseño del sistema.
3. **Performance Engineering** – Las implementaciones que evitan `O(n2 k)` son prácticas. Programador de amor a los candidatos que saben cómo **reducir tanto tiempo como espacio**.
4. **Idioma Agnostic** – Ya sea en Java, Python o C++, la idea algorítmica es la misma. Esto muestra flexibilidad – otro activo en un entorno tecnológico de movimiento rápido.

-...

#### 2.8 Conclusiones

LeetCode 629 es un problema clásico “Hard” que te enseña cómo:

1. Formular una tabla DP ( " dp[i][j] " ).
2. Encuentra una convolución y convertirla en una recurrencia prefijo-sum.
3. Implementar una matriz de rodaje para espacio lineal.
4. Manija aritmética modular correctamente.

Dominar este problema no sólo le ganará una puntuación alta en LeetCode sino que también le equipará con un conjunto de habilidad transferible: *definición del estado, simplificación de recurrencia y optimización del espacio. *

■ **Pro tip:** Después de que estés cómodo con este truco DP, intenta resolver el *“K‐th Smallest Prime Fraction”* o *“Maximum Product Subarray”* – son estructuralmente similares y siguen los mismos principios de optimización.

Feliz codificación, y que sus entrevistadores vean el *Good* y *Ugly* en su propio viaje algoritmo! 🚀

-...

■ **Para más información**
* Programación Dinámica* (MIT OCW) – https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/lecture-notes/
*El arte del DP en entrevistas* – https://www.interviewbit.com/dynamic-programming-interview-questions/
*LeetCode Discuss – 629* – https://leetcode.com/problems/k-inverse-pairs-array/discuss/
-...

¡Feliz entrevista