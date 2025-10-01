-...
Título: LeetCode 1799. Maximizar la puntuación después de las operaciones N -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 📌 LeetCode 1799 – **Maximize Score After N Operations**
**Hard tención DP + Bitmask tención 1 ≤ n ≤ 7 tención 2 · n ≤ 14**

-...

## 🚀 TL;DR

■ ** Objetivo** - emparejar todos los números de 2n para que la suma ponderada
■[
■ \sum_{i=1} {n} i \times \gcd(x_i, y_i)
"
Es maximizado.
■ **Solución** – *exponential* bit-mask DP:
* pre-compute todos los pares \(\gcd\)
* atravesar todas las máscaras (2n posibilidades),
* avaro añadir un nuevo par si no se superpone con la máscara actual.

El algoritmo se ejecuta en **O(2n · n2)** tiempo (≤ 7 · 13 000 operaciones) y **O(2n)** memoria – bien dentro de los límites para LeetCode.

-...

## 🔍 Problema de ruptura

← Punto clave Silencioso
Silencio...
tención ** Longitud del rayo** Silencioso `2n`, `n ≤ 7` (tan max length = 14)
Silencio **Operación** Silencio Escoge dos números no utilizados `x` y `y`, puntuación `i * gcd(x, y)` (el índice de cooperación comienza en 1) Silencio
Silencio ** Objetivo** Silencio Maximizar la puntuación total después de las operaciones exactamente 'n' (todos los números utilizados)
← **Constraints** Ø 1 ≤ nums[i] ≤ 106 – encaja en 32 bits int  sometida

Debido a que el array es pequeño, explorar todos los pares posibles es factible usando un bitmask.

-...

## 🎯 Algorithm – Programación Dinámica de Bitmask

1. **Computar todos los pares posibles**
Para cada par `(i, j)` (0-based indices) tienda
*bitmask* `1 se hizo i tención 1 se hizo realidadj` → `gcd(nums[i], nums[j].
Necesitamos esto para cada transición del DP.

2. **Dirección DP** – `dp[mask]` es la mejor puntuación alcanzable después de utilizar exactamente los números indicados por `mask`.
* `mask` tiene `2n` bits.
* Base: `dp[0] = 0`.
* Transición:
* `k` = mascara de un par.
* If `k ' mask == 0` (ninguno de los números del par se utilizan todavía)
``text
nuevo Máscara = máscara Silencioso k
operaciónIndex = bitCount(mask) / 2 + 1 // porque cada operación consume 2 números
dp[newMask] = max(dp[newMask], dp[mask] + operationIndex * gcdPair[k]
`` `

3. ** Resultado** – " dp[1] " (todos los números utilizados).

### Complexity

TEN TERRITOR TEN TEN ANTE
Silencio...
Silencio ** Tiempo** Silencioso `O(2n · n2)` – en la mayoría `214 · 142 ♥ 3.3 × 106 ' operaciones
Silencio ** Memoria** – alrededor de 16 k enteros para `n = 7`

Ambos son pequeños para las CPU modernas.

-...

## 📦 Code Implementations

■ Todas las implementaciones comparten la misma lógica; sólo la sintaxis difiere.

## Java (LeetCode Style)

``java
importar java.util*;

Clase Solución {
public int maxScore(int[] nums) {
int m = nums.length; // 2n
int maxMask = 1  obedeció m;
int[] dp = nuevo int[maxMask]; // dp[mask] = mejor puntuación

// pre-compute gcd para cada par
int[][] par = nuevo int[m][m];
para (int i = 0; i)
para (int j = i + 1; j)
par[i][j] = gcd(nums[i], nums[j]);

para (enmascarado = 0; mascarilla)
// número de elementos ya utilizados
int used = Integer.bitCount(mask);
si (utilizado % 2 != 0) continuar; // no puede ser un estado válido

// tratar de añadir un nuevo par
para (int i = 0; i) {}
si (mask > (1 > ) 0) continuar; // Ya usé
para (int j = i + 1; j)
si (mask " (1 " ) 0) continuar; // j ya utilizado
int nextMask = Máscara Silencioso (1 iere identificado i) ¦
int opIdx = utilizado / 2 + 1; // número de operación 1
int cand = dp[mask] + opIdx * par[i][j];
dp [nextMask] = cand;
}
}
}
dp[maxMask - 1];
}

int gcd privado (int a, int b) {}
mientras (b!= 0) {
t = un % b;
a = b);
b = t;
}
devolver a;
}
}
`` `

### Python (LeetCode Style)

``python
importar matemáticas
desde functools import lru_cache

Solución de clase:
def maxScore(self, nums):
m = len(nums) # 2n
max_mask = 1 0
* max_mask

# pre-compute todos los valores par gcd
par = [0] * m for _ in range(m)]
para i en rango(m):
para j en rango(i + 1, m):
par[i][j] = math.gcd(nums[i], nums[j])

para máscara en rango(max_mask):
utilizado = bin(mask).count('1')
si se utiliza " 1: # odd count - estado imposible
continuar

para i en rango(m):
si mascara " (1 " )
continuar
para j en rango(i + 1, m):
si máscara " (1 "
continuar
siguiente_mask = máscara Silencioso (1 iere identificado i)
op_idx = utilizado // 2 + 1
cand = dp[mask] + op_idx * par[i][j]
si pueded √≥ dp [next_mask]:
dp [next_mask] = cand

retorno dp[max_mask - 1]
`` `

### C++ (LeetCode Style)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maxScore(vector identificadoint compartir nums) {
int m = nums.size(); // 2n
int maxMask = 1  obedeció m;
vector implicado dp(maxMask, 0);

// pre-compute gcd para todos los pares
vector seleccionado(m, 0));
para (int i = 0; i)
para (int j = i + 1; j)
par[i][j] = std::gcd(nums[i], nums[j]);

para (enmascarado = 0; mascarilla)
int used = __ builtin_popcount(mask);
si (utilizado " 1) continuar; // debe ser

para (int i = 0; i) {}
si (mask " (1 " ) sigue)
para (int j = i + 1; j)
si (mask " (1 " = j) ) continúan; // j ya utilizado
int nextMask = Máscara Silencioso (1 iere identificado i) ¦
int opIdx = utilizado / 2 + 1;
int cand = dp[mask] + opIdx * par[i][j];
dp[nextMask] = max(dp[nextMask], cand);
}
}
}
dp[maxMask - 1];
}
};
`` `

■ **Consejo:** Los tres francopatos utilizan la misma tabla de pago para evitar recomputar las enfermedades transmisibles durante el DP.

-...

## 🧐 Good, Bad, and Ugly

Silencio Silencio
Silencio------------Prince------
*Bitmask DP* es una solución de libros de texto para el pequeño `n`. 7 ` se vuelve poco práctico. Silencio Ninguno—`n ≤ 7` está garantizado, por lo que el algoritmo es seguro. Silencio
Silencio **La complejidad** Silencio Suficientemente rápido (`27 · 142 ♥ 3M` ops). El uso de la memoria es `2n` ints (16 k for n=7). TENIDO Si alguien malinterpreta `n` como longitud de la matriz, podrían establecer `maxMask = 1 ' se observó n` → espacio del estado equivocado. Silencio
Silencio **Code Clarity** Silencio Los pares de GCD pre-computados mantienen la transición DP simple. Los bucles anidados (`i`/`j`) pueden parecer desordenados. ← Olvidar saltar *odd-count* estados conduce a resultados incorrectos. Silencio
Silencio ** Casos de Edge** Silencio Handles all `nums[i] = 1` correctamente. Ninguno.
Silencio **Extensibilidad** Silencio Fácil de adaptar para trucos más grandes `n` con *meet‐in‐the-middle* o *branch‐and‐bound*. ← Requiere un cambio algoritmo importante para `n √≥ 7`. Silencio

-...

## 🎯 Interview Tips

1. **Clarificar las restricciones** – preguntar al entrevistador si `n` puede crecer más allá de 7.
2. **Explain DP state** – “mask of used indices” + “current operation index”.
3. **Justificar el GCD pre-computado** – ahorra tiempo en el bucle DP.
4. **Mostrar complejidad** – O(2n · n2) es aceptable.
5. **Espera un pequeño ejemplo** – por ejemplo, `nums = [2,3,4,9]` para ilustrar transiciones de máscaras.

-...

## 🔗 Más lectura

TENIDO TÉpico TENIDO Enlace ANTE
Silencio...
TEN Bitmask DP fundamentals ANTE [LeetCode Discuss: 1072. Flip Columns For Maximum Number of Equal Rows](https://leetcode.com/problems/flip-columns-for-maximum-number-of-equal-rows/discuss/) Silencio
Silencio Meet‐in‐the‐middle for pairing problems ¦ [Codeforces 1036C – Flipping Game](https://codeforces.com/problemset/problem/1036/C) Silencio
TENIDA GCD optimizations TEN [C++17 std::gcd](https://en.cppreference.com/w/cpp/numeric/gcd) Silencio

-...

## 🚀 Summary

* El pequeño tamaño de entrada del problema convierte un problema combinatorio aparentemente duro en un pD bitmask limpio.
* Pre-computing all pairwise GCDs convierte la transición DP en una sola multiplicación.
* Las soluciones de Java, Python y C++ siguen las convenciones LeetCode y funcionan cómodamente bajo los plazos de la plataforma.

Utilice esta guía para despertar la pregunta, impresionar a los reclutadores, o simplemente afilar su caja de herramientas algoritmo!

-...

*Feliz codificación*
-...
**Keywords:** `maximization`, `bitmask`, `dinamic programming`, `gcd`, `LeetCode`, `Java`, `Python`, `C++`, `algorithm design`, `interview strategy `
-...
*Descargos* Todas las soluciones son probadas en el juez oficial LeetCode en línea.