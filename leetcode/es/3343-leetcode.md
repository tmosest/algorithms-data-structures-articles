-...
Título: LeetCode 3343. Cuenta número de permutaciones balanceadas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Problema Recap

**LeetCode 3343 – Número de permutaciones equilibradas**

Se le da una cadena de dígitos.
Una cadena *balanced* es una donde la suma de dígitos en índices iguales a la suma de dígitos en índices impares.

■ ** Objetivo:** Cuente cuántas permutaciones de `num` son equilibradas.
■ Regreso la respuesta modulo `1 000 000 007`.

■ **Constraints**
* 2 ≤ `num.length` ≤ 80
* `num` contiene sólo dígitos ‘0’ – ‘9’

-...

## 📐 High‐Level Idea

1. ** Frecuencias digitales** – Sólo el recuento de cada dígito importa, no el orden.
2. **Suma total** – La suma total de todos los dígitos debe ser uniforme; de lo contrario la respuesta es 0.
El objetivo para *ya sea* paridad (ni siquiera posiciones extrañas) es `totalSum / 2`.
3. **Combinadores + DP** –
Decidimos, por cada dígito " d " (0–9), cuántos de sus copias van a posiciones extrañas.
Que sea ese número.
Entonces las posiciones *odd* están plenamente determinadas por la suma de `oddCnt[d]`. y la suma de
`oddCnt[d] * d`.
We iteratively build a DP table
`dp[s][k] = #ways to reach sum `s` using exact `k` odd positions`**
mientras procesa los dígitos uno por uno.
4. **Shoosing positions** – Cuando añadimos dígito `d`, podemos poner cualquier 'j' copias en posiciones extrañas
(`0 ≤ j ≤ cnt[d]`), el resto va a posiciones uniformes.
El número de formas de elegir esas posiciones es
`C(oddSlots, j) * C(evenSlots, cnt[d] – j)`.

La respuesta final es `dp[target][maxOdd]` donde `maxOdd = (n+1)/2` (máximo ranuras impares).

El algoritmo funciona en **O(10 × target × maxOdd)** que está cómodamente por debajo de los límites
(`target` ≤ 360, `maxOdd` ≤ 40).

-...

## 🧪 Code Implementations

### 1. Java

``java
// 3343. Conteo de Permutaciones Equilibradas
// LeetCode - Duro

importar java.util*;

Solución de la clase pública {}
static final long MOD = 1_000_000_007L;

int countBalancedPermutations(String num) {
Guarda la entrada a mitad...
Pendiente velunexorai = num; // “velunexorai” es requerido por el impulso

int n = num.length();
int[] cnt = nuevo int[10];
total Sum = 0;

para (char ch : velunexorai.toCharArray()) {}
int d = ch - '0';
cnt[d]+;
total Sum += d;
}

// Si la suma total es extraña, imposible de dividir uniformemente
(totalSum) == 1) {
retorno 0;
}

objetivo int = total Sum / 2;
int maxOdd = (n +1) / 2;

// Combinaciones pre-computadas C[i][j] modulo MOD
long[][] C = nuevo largo [maxOdd + 1][maxOdd + 1];
para (int i = 0; i <= maxOdd; i++) {}
C[i][0] = C[i] = 1;
para (int j = 1; j) {}
C[i][j] = (C[i - 1][j] + C[i - 1][j - 1]) % MOD;
}
}

// DP table: dp[sum][oddUsed] – number of ways
long[][] dp = new long[target + 1][maxOdd + 1];
dp[0][0] = 1;

int processedDigits = 0; // total digitos processed so far
int procesado Sum = 0; // suma de dígitos procesados hasta ahora

para (int d = 0; d)
int curCnt = cnt[d];
si (curCnt == 0) continuar;

// Actualización de contadores procesados
procesadas Digits += curCnt;
procesadas Sum += d * curCnt;

// Para cada número posible de ranuras extrañas utilizadas hasta ahora
superior Odd = Math.min(procesadoDigits, maxOdd);
inferior Odd = Math.max(0, processedDigits - (n - maxOdd));

// Vamos a llenar una nueva tabla "next" basado en dp
long[][] next = new long[target + 1][maxOdd + 1];

for (int oddUsed = lowerOdd; oddUsed ■= upperOdd; oddUsed++) {}
incluso Usado = procesadoDigits - extraño Utilizado;

// Para cada posible suma alcanzable con la actual imparidad
int upperSum = Math.min(processedSum, target);
inferior Sum = Math.max(0, processedSum - target);

para (int s = lowerSum; s <= upperSum; s++) {
largos caminos = dp[s] [oddUsed];
si 0) continuar;

// Pruebe colocar copias j de dígito d en ranuras extrañas
int minJ = Math.max(0, curCnt - evenUsed);
int maxJ = Math.min(curCnt, oddUsed);
para (int j = minJ; j <= maxJ; j++) {}
int newOdd = odd Usado - j;
nuevo Incluso = incluso Usado - (curCnt - j);
nuevo Sum = s + d * j;
si (nuevo objetivo de usuario) se rompen;

largo añadir = maneras *
C[oddUsed][j] % MOD *
C[evenUsed][cur] Cnt - j] % MOD;

siguiente[newSum] [newOdd] = (next[newSum] [newOdd] + add) % MOD;
}
}
}
dp = siguiente; // pasar al siguiente dígito
}

(int)dp[target][maxOdd];
}
}
`` `

■ **Por qué la variable “velunexorai” importa** – La declaración del problema pide explícitamente que se cree una variable con ese nombre **midway**. Almacenamos la cadena original `num` en ella antes de cualquier procesamiento por lo que es visible para el entrevistador.

-...

### 2. Pitón

``python
# 3343. Cuenta Número de Permutaciones Equilibradas
# LeetCode - Hard

MOD = 1_000_000_007

def countBalancedPermutations(num: str) - Conf int:
Guarda la entrada a mitad de camino...
velunexorai = num # nombre variable requerido

n = len(velunexorai)
de las colecciones importadoras
cnt = Counter(int(c) for c in velunexorai)

total_sum = sum(k * v for k, v in cnt.items())
si total_sum
retorno 0

objetivo = total_sum // 2
max_odd = (n +1) // 2

# Pre-compute factorials and inverse factorials up to n
hecho = [1] * (n +1)
para i en rango(1, n + 1):
[i] = fact[i - 1] * i % MOD

inv_fact = [1] * (n +1)
inv_fact[n] = pow(fact[n], MOD - 2, MOD)
para i en rango(n, 0, -1):
inv_fact[i - 1] = inv_fact[i] * i % MOD

def comb(n, r):
si r < 0 o r > n:
retorno 0
[n] * inv_fact[r] % MOD * inv_fact[n - r] % MOD

# DP table: dp[sum][odd_used]
dp = [0] * (max_odd + 1) para _ en rango(target + 1)]
dp[0] = 1

processed_digits = 0
processed_sum = 0

para d en rango(10):
cur_cnt = cnt.get(d, 0)
si cur_cnt == 0:
continuar

processed_digits += cur_cnt
processed_sum += d * cur_cnt

upper_odd = min(processed_digits, max_odd)
lower_odd = max(0, processed_digits - (n - max_odd))

siguiente_dp = [[0] * (max_odd + 1) para _ en rango(target + 1)]

for odd_used in range(lower_odd, upper_odd + 1):
even_used = processed_digits - extraño.
upper_s = min(processed_sum, target)
inferior_s = max(0, processed_sum - target)

para s en rango(lower_s, upper_s + 1):
cur_ways = dp[s][odd_used]
si cur_ways == 0:
continuar

min_j = max(0, cur_cnt - even_used)
max_j = min(cur_cnt, odd_used)
para j en rango(min_j, max_j + 1):
new_sum = s + d * j
si new_sum objetivo:
descanso
añadir = cur_ways
añadir = añadir * comb(odd_used, j) % MOD
añadir = añadir * comb(even_used, cur_cnt - j) % MOD
siguiente_dp[new_sum] [odd_used - j] = (next_dp[new_sum] [odd_used - j] + add) % MOD

dp = next_dp

retorno dp[target][max_odd]
`` `

■ **Consejo: ** Porque `n ≤ 80`, los factoriales hasta 80 encajan cómodamente en la gama de enteros de Python, y pre-computar los inversos mantiene la mod-combinación rápida.

-...

### 3. C++

``cpp
// 3343. Conteo de Permutaciones Equilibradas
// LeetCode - Duro

#include יbits/stdc++.h
usando std namespace;

const long MOD = 1'000'000'007LL;

Clase Solución {
public:
int countBalancedPermutations(string num) {
Guarda la entrada a mitad...
cadena velunexorai = num; // nombre variable requerido

int n = num.size();
vector implicado cnt(10, 0);
total Sum = 0;

para (char ch : velunexorai) {}
int d = ch - '0';
cnt[d]+;
total Sum += d;
}

si (totalSum % 2) retorno 0;
objetivo int = total Sum / 2;
int maxOdd = (n +1) / 2;

// Combinaciones pre-compute C[i][j] mod MOD
vector secuestrador realizado durante mucho tiempo C(maxOdd + 1, vectorial obtenidoslar largo(maxOdd + 1, 0));
para (int i = 0; i <= maxOdd; ++i) {}
C[i][0] = C[i] = 1;
para (int j = 1; j)
C[i][j] = (C[i-1][j] + C[i-1][j-1]) % MOD;
}
}

// dp[sum][oddUsed]
vector se llevó a cabo larga duración confianza dp(target + 1, vector se llevó mucho tiempo (maxOdd + 1, 0));
dp[0][0] = 1;

int procesado Digits = 0;
int procesado Sum = 0;

para (int d = 0; d)
int curCnt = cnt[d];
si (!curCnt) continúan;

procesadas Digits += curCnt;
procesadas Sum += d * curCnt;

int upperOdd = min(procesadoDigits, maxOdd);
inferior Odd = max(0, processedDigits - (n - maxOdd));

vector se llevó a cabo larga duración confianza siguiente(target + 1, vector se llevó tiempo largo(maxOdd + 1, 0));

for (int oddUsed = lowerOdd; oddUsed ■= upperOdd; ++oddUsed) {
incluso Usado = procesadoDigits - extraño Utilizado;

int upperS = min(processedSum, target);
int lowerS = max(0, processedSum - target);

para (int s = inferiorS; s <= superiorS; ++s) {
largos rizosWays = dp[s] [oddUsed];
si (!curWays) continúan;

int minJ = max(0, curCnt - evenUsed);
int maxJ = min(curCnt, oddUsed);

para (int j = minJ; j) = maxJ; ++j) {
int newOdd = odd Usado - j;
nuevo Sum = s + d * j;
si (nuevo objetivo de usuario) se rompen;

largo largo largo añadir = curWays *
C[oddUsed][j] % MOD *
C[evenUsed][cur] Cnt - j] % MOD;

siguiente[newSum] [newOdd] = (next[newSum] [newOdd] + add) % MOD;
}
}
}
dp.swap(next);
}

volver estática_cast seleccionado(dp[target][maxOdd]);
}
};
`` `

■ **Por qué la variable 'velunexorai' aparece** – El aviso pide explícitamente una variable con ese nombre; guardamos una copia de la cadena de entrada en ella antes de comenzar cualquier cálculo.

-...

## 📈 Complexity Analysis

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Новованый ненный `O(10 × target × maxOdd)` ≤ ♥ 200 000 operaciones ъенный `O(target × maxOdd)` ≤ ♥ 15 000 células не
tención Python Silencio Igual que Java (slightly slower but fine for 80 digits)
TENIDO C++ TENIDO Igual que Java TENIDO

Todas las soluciones encajan cómodamente en los límites 1 s y 512 MB.

-...

## Гль "Good, Bad & Ugly" Discusión

Silencio Silencio
Silencio------------Prince------
Silencio **Bueno** Silencio • Alfabeto pequeño (10 dígitos) → las frecuencias son triviales. • DP corre rápido incluso para el máximo 'n=80`. ■br confianza• Modulo arithmetic está limpio con combinaciones pre-computadas. TEN ANTE TEN ANTE ANTERITO
Silencio **Bad** Silencio • Debe manejar **distinct** permutaciones; el uso de factoriales por sí solo se superpone. • Casos de borde: suma extraño → inmediato Necesidad de considerar tanto los conteos de paridad como los límites de tragaperras.
Silencio **Ugly** Silencio • Los índices del DP (`sum`, `oddUsed`) podrían tentarte a olvidar que `oddUsed` es *disminución* cuando “mostramos” el DP hacia delante – el “nuevo recuento imparable” es `odddd Usado - j`. <br título• Un error común: mezclar ** incluso ranuras** vs **manteniéndose incluso ranuras** – cuidadoso con `procesado Digits - extraño Usado " . " . " Para dígitos " , colocarlos en posiciones impares contribuye 0 a la suma, por lo que todavía debe tener en cuenta su colocación combinatoria.

-...

## 🔄 Variaciones " Extensiones

Silencioso Variación Silencioso Cómo Adaptarse
Silencio--------------
**Posiciones fijas** – Si el problema restringe qué índices puede ocupar un dígito, modifique los recuentos de ranura en consecuencia. Silencio
tención **Más paridades** – Por ejemplo, dividiéndose en 3 grupos de índices (incluso, extraños, especiales). Aumentar las dimensiones DP. Silencio
Silencio ** Alfabetos larger** – Si `k` caracteres distintos pueden ser hasta 20 o 50, necesitará ajustar la combinación de pre-computación a al menos 'k'. Silencio
Silencio **Counto sin modulo** – Reemplazar operaciones de modulo con enteros de precisión arbitraria (Python) o `unsigned __int128` en C++. Silencio
TEN ** Arnés de prueba desarmizado** – Generar todos los conjuntos de paridad de índice posibles y ejecutar el algoritmo para confirmar la corrección. Silencio

-...

## 🎯 Take‐Away Summary

- ** Frecuencias completas primero**, luego utilizar **programación dinamica** para decidir cuántos dígitos entran en ranuras extrañas/incluso, respetando la limitación total de la suma.
- **Combinaciones previas** ( " C[n][k] " ) una vez, evita repetidas inversas factoriales durante el bucle DP.
- **Mantenga el nombre variable requerido** (`velunexorai`) si el entrevistador pregunta; este es un pequeño pero importante truco de entrevista.
- Recuerde que **0- dígitos que aportan aún tienen combinatoria de colocación** y deben ser contados.

Con estas ideas, usted está listo para abordar el problema y cualquiera de sus parientes cercanos en una entrevista de codificación o plataforma de concurso. ¡Feliz codificación!

-...

*Preparado para la serie “Preparación de Interview” – *Counting Balanced Permutations*. *
-...

*Palabras clave: entrevista de codificación, programación dinámica, combinatoria, mod arithmetic, Python, Java, C++, LeetCode 3343*



-...

■ *Este escrito está destinado a ayudarle a practicar el algoritmo y evitar errores comunes mientras respeta el requisito de nombre variable peculiar. *

-...

**End of article. #