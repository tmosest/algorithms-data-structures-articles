-...
Título: LeetCode 2992. Número de permutaciones autodivisibles -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🔍 LeetCode 2992 – *Número de permutaciones autodivisibles*
** Idiomas**: Java, Python, C++
**Dificultad**: Medium
**Max n**: 12

■ **SEO Tags**:
" LeetCode 2992 " , " self divisible permutations " , " dinamic programming bitmask " , `Java solution " , `Python solution ' , `C++ solution ' , `job interview coding ' , `algorithms interview ' , `bitmask DP '

-...

### 📌 Declaración de problemas

Dado un entero `n`, cuenta cuántas permutaciones de la matriz de un índice `nums = [1, 2, ..., n]` satisfacer satisfacción
gcd(nums[i], i) == 1' por cada uno 1 ≤ ≤ n.
La longitud del array es en la mayoría **12**.

-...

### ♥ Intuition

El requisito es local: cuando decidamos el elemento que entra en la posición 'i', sólo necesitamos comprobar si es coprime con 'i'.
Esto sugiere una programación dinámica *state‐por-state* donde el estado registra los números que ya se han colocado.

Debido a que `n ≤ 12`, una máscara de 12 bits (o un entero de 64 bits en C++) puede codificar el conjunto de números usados eficientemente.
Que `mask` sea tal que bit `j‐1` es `1` si el número `j` ya se ha colocado.
Si `mask` tiene `k` bits set, entonces la siguiente posición libre es `k + 1`.

From state `mask`, we try every unused number `x` (`1 ... n`).
Si `x` es coprime con la nueva posición `k+1`, podemos colocarla y la transición a `mask ANTERITO (1 ANTE 10) ' .
The DP value `dp[mask]` es el número de formas válidas para llenar exactamente las posiciones descritas por `mask`.

-...

Algoritmo (Bitmask DP)

1. `S = 1 ' se realizó n` - número total de máscaras.
2. `dp[0] = 1` – el arreglo vacío es una manera.
3. Por cada `mask` de `0` a `S-1`:
* `k = popcount(mask)` – números ya colocados.
* `pos = k + 1` – índice de la siguiente posición para llenar.
* For each number `x` (`1 ... n`):
* if bit `x-1` is **unset ** in `mask` **and ** `gcd(x, pos) == 1
entonces `dp[mask TENIDO (1  Se hizo (x-1)] += dp[mask]`.
4. Respuesta es `dp[S-1]` – todos los números utilizados.

■ ** Complejidad del tiempo**: `O(2^n * n) `
■ ** Complejidad del espacio**: `O(2^n) `
■ Con `n ≤ 12`, esto está perfectamente bien (`2^12 * 12 Ω 49k`).

-...

## 📑 Code Implementations

A continuación encontrará soluciones limpias y listas para pasar en **Java**, **Python**, y **C+**.
Los tres comparten la misma lógica y están fuertemente comentados para la claridad.

-...

## Java 17

``java
importar java.util*;

Clase Solución {
public int selfDivisiblePermutationCount(int n) {
total Máscara = 1 > >
int[] dp = nuevo int[total] Mask];
dp[0] = 1; // permutación vacía

para (enmascarado = 0; máscara) total Máscara; máscara+) {}
si (dp[mask] == 0) continuar; // ninguna manera de llegar a este estado

int placed = Integer.bitCount(mask); // números ya utilizados
siguiente Pos = colocado + 1; // siguiente índice para llenar

para (int x = 1; x <= n; x++) {
// saltar si x ya utilizado
si (mask > (1 ) se hizo (x - 1)) != 0) continuar;

/ Coprime check
si (gcd(x, nextPos) == 1) {
int newMask = Máscara Silencioso (1  buscado (x - 1));
dp[newMask] += dp[mask];
}
}
}
retorno dp [total Máscara - 1];
}

# El algoritmo de Euclid #/
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

-...

## Python 3

``python
Solución de clase:
def selfDivisiblePermutationCount(self, n: int) - int:
total_mask = 1 = 0
* total_mask
dp[0] = 1

para máscara en rango(total_mask):
si dp[mask] == 0:
continuar

colocado = bin(mask).count("1") # números ya utilizados
pos = colocado + 1 # siguiente índice

para x en rango(1, n + 1):
si la máscara " (1 " se realizó (x - 1)):
continue # already used

si auto._gcd(x, pos) == 1:
new_mask = máscara Silencioso (1 iere escrito (x - 1))
dp[new_mask] += dp[mask]

retorno dp[total_mask - 1]

@staticmethod
def _gcd(a: int, b: int) - título int:
mientras b:
a, b = b, porcentaje b
retorno a
`` `

-...

### C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int selfDivisiblePermutationCount(int n) {
total Máscara = 1 > >
vectoriales Mask, 0);
dp[0] = 1; //

para (enmascarado = 0; máscara) total Máscara; ++masca) {
si (!dp[mask]) continúan;

int placed = __ builtin_popcount(mask);
int pos = colocado + 1; // siguiente índice

para (int x = 1; x <= n; ++x) {
si (mask " (1  obtenidos (x - 1))) continúan; // ya utilizado

si (gcd(x, pos) == 1) {
int newMask = Máscara Silencioso (1  buscado (x - 1));
dp[newMask] += dp[mask];
}
}
}
retorno dp [total Máscara - 1];
}

privado:
int gcd(int a, int b) {}
b) {
t = un % b;
a = b);
b = t;
}
devolver a;
}
};
`` `

-...

## 🔍 Good, Bad & Ugly

Silencio Silencio
Silencio------------Prince------
Silencio ** Algorithm** Silencio Bitmask DP utiliza todos los estados 2n una vez → óptima para n ≤ 12 Silencio La complejidad del tiempo `O(2n·n)` crece exponencialmente, pero n es minúscula  habit Ninguno – algoritmo está limpio  sometida
Silencioso **Implementación** Silencio Simple bucle sobre máscaras + operaciones de bits TEN Necesita indexación cuidadosa (bit `x-1`) ← Olvidar la comprobación de `gcd` puede producir la respuesta incorrecta
Silencio **Backtracking Alternative** Silencio Illustrative, easy to code TEN Exponential `O(n·n!)` – mucho más lento para n=12
Silencio **Readability** Silencio Autor-documentación con comentarios Silencio Puede parecer denso a los recién llegados
Silencio **Espacio** Silencio O(2n) int array Silencio Todavía aceptable (Ω 16 KB)

-...

## 📈 Why This is a Great Interview Talking Point

1. ** Compresión estatal** – Usar un bitmask para codificar qué números se utilizan muestra dominio de DP combinatorio.
2. **Perspectiva específica del programa** – Reconociendo que la siguiente posición depende sólo de cuántos números ya se han colocado.
3. **Eficiente GCD Check** – El algoritmo de Euclid es estándar; puedes mencionar el potencial de los resultados de caché si es necesario.
4. **Discusión de la escalabilidad** – Usted puede explicar por qué este enfoque funciona hasta `n = 12`, pero se rompería para mayor `n`, y qué alternativas (por ejemplo, inclusión-exclusión) usted podría considerar.

-...

## 📚 Take‐away Checklist

- ✅ Usar un bitmask DP para las restricciones combinatorias con `n ≤ 20`.
- Contar con números usados con 'popcount' (`__construidoin_popcount`, `Integer.bitCount`, o `bin(mask).count`).
- ✅ Transición a la posición *next* (`k+1`) solamente.
- Verificar la coprimalidad con gcd.
- ✅ Return `dp [(1 seleccionado)-1].

-...

¿Listo para impresionar a los reclutadores?

Utilice los snippets anteriores Java / Python / C++ como su código "show‐off".
Explicar la intuición y hablar a través de la mesa buena/bad/ugly en una entrevista de siguiente nivel: ¡te clavarás esa pregunta de LeetCode 2992 y demostrarás el tipo de algoritmos de pensamiento que los reclutadores adoran!