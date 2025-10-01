-...
Título: LeetCode 3351. Sum of Good Subsequences -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 3351 – *Sum of Good Subsequences*
### “El bien, el mal, el ugly” – Un paseo práctico DP (Java Silencioso Python Silencio C++)

■ **TL;DR** –
■ *Una buena subsequencia* es una subsequencia donde la diferencia absoluta entre cada par de elementos consecutivos equivale a **1**.
■ Queremos la suma de todos los elementos sobre todas las subsecuencias buenas.
■ La solución clásica es una programación **dinámica** que funciona en **O(n)** tiempo y **O(max(nums))** memoria.

■ **Keywords:**
■ *LeetCode 3351* Silencioso *Sum of Good Subsequences* Silencio *Programación Dinámica* Silencio *DP with arrays* Silencio *Java* Silencio *Python* Silencio *C++* Silencio* *Entrevista Prep*  durable *Job Interview*

-...

Problema Recap

``text
Entrada : nums = [1, 2, 1]
Producto: 14
`` `

Buenas subsecuencias (tamaño ≥ 1):
- [1] → suma = 1
- [2] → suma = 2
- [1] → suma = 1
- [1,2]→ suma = 3
- [2,1]→ suma = 3
- [1,2,1]→ suma = 4
Total = 14

Limitaciones
- 1 ≤ nums.length ≤ 10^5`
- `0 ≤ nums[i] ≤ 10^5`
- Respuesta modulo `10^9 + 7`

-...

## 2down ¿Por qué Programación Dinámica?

- Cada subsequencia buena que termina con el valor `x` sólo puede ser extendida por elementos `x-1` o `x+1`.
- Esta propiedad “local” nos permite procesar el array una vez, acumulando cuentas y sumas totales por valor.
- Sin DP, tendríamos que enumerar todas las subsecuencias → `O(2^n)`.

-...

## 3down The DP Idea

Vamos.
- `cnt[v]` = **number** of good subsequences that end with value `v`.
- `sum[v]` = **Suma total de elementos** sobre todas las subsecuencias buenas que terminan con el valor `v`.

Cuando leemos un nuevo elemento:

Silencio Acción Silencioso Descripción Silencio Actualizar fórmula Silencio
Silencio...
Silencio Inicio de una nueva subsequencia `[a]` Silencio 1 subsequence ← 1o de abril de 1994
Silencio Ampliar subsequence terminando con `a-1` Silencio Cada da nueva subsequence `...,(a-1),a` Silencio `cnt[a] += cnt[a-1] ` Silencio
Silencioso Extensión finalizada con `a+1` Silencio Mismo ANTE `cnt[a] += cnt[a+1] Silencio
Silencio Resúmenes de actualización para cada nueva subsequencia agregamos la suma de la antigua subsequencia + el nuevo elemento `a` Silencio
`sum[a] += sum[a-1] + sum[a+1] + a * (cnt[a-1] + cnt[a+1] + 1) Silencio

Todas las operaciones se realizan modulo `M = 1 000 000 007`.

La respuesta es la suma de todos los valores de la suma [v]` después de la exploración.

-...

## 4Get Cases " The Ugly "

Problema permanente ¿Qué puede pasar mal? Cómo proteger Silencio
Silencio----------------------------
Silencio Indice fuera de los límites Silencio `cnt[a-1]` o `cnt[a+1]` cuando `a` es 0 o `MAX_VAL` Silencio Use array size `MAX_VAL + 3` y siempre acceda `cnt[a+1]`, `cnt[a+2]`. Silencio
Silencio Integer overflow ← `cnt ' y `sum ' puede exceder `int`  durable Use `long` (`int64`) en todas partes. Silencio
tención Modulo después de cada adición tención Failing to mod puede rebosar tención Mod después de cada asignación. Silencio
← Números Duplicados Silencio Cada ocurrencia del mismo número debe ser tratada independientemente tención DP naturalmente lo maneja porque procesamos secuencialmente. Silencio

-...

## 5down El Código

A continuación se **tres** implementaciones que siguen la misma lógica:

*Los tres comparten la misma complejidad: `O(n + max(nums)' tiempo, `O(max(nums))' memoria. *

■ **Consejo:** Use `int[]` for the input; all heavy lifting is done in `long` arrays.

### 5.1 Java

``java
importar java.util*;

clase pública SumOfGoodSubsequences {}
static final long MOD = 1_000_000_007L;
privada estática final int MAX_VAL = 100_000; // determinada limitación

int sumOfGoodSubsequences(int[] nums) {
largo[] cnt = nuevo largo [MAX_VAL + 3]; // +3 para evitar controles de límites
long[] sum = new long[MAX_VAL + 3];

para (int a : nums) {
int idx = a + 1; // cambio por +1 para mantener 0-index seguro

cntPrev largo = cnt[idx - 1]; // a-1
cntNext = cnt[idx + 1]; // a+1

larga sumaPrev = sum[idx - 1];
suma largaSiguiente = suma[idx + 1];

nuevo Cnt = (cntPrev + cntSiguiente + 1) % MOD;
long newSum = (sumPrev + sumNext + a * newCnt) % MOD;

cnt[idx] = (cnt[idx] + newCnt) % MOD;
sum[idx] = (sum[idx] + newSum) % MOD;
}

resultado largo = 0;
para (int i = 0; i)
resultado = (resultar + suma [i]) % MOD;
}
Resultado de retorno (int)
}

public static void main(String[] args) {
SumOfGoodSubsequences solver = nuevo SumOfGoodSubsequences();
System.out.println(solver.sumOfGoodSubsequences(new int[]{1, 2, 1})); // 14
System.out.println(solver.sumOfGoodSubsequences(new int[]{3, 4, 5})); // 40
}
}
`` `

### 5.2 Python

``python
de las colecciones importadas por defecto
de la importación Lista

MOD = 10 ** 9 + 7

Solución de clase:
def sumOfGoodSubsequences(self, nums: List[int]) int:
cnt = defaultdict(int)
total = defaultdict(int)

para una en las numidades:
c_left, c_right = cnt[a - 1], cnt[a + 1]
t_left, t_right = total[a - 1], total[a + 1]

new_cnt = (c_left + c_right + 1) % MOD
new_sum = (t_left + t_right + a * new_cnt) % MOD

cnt[a] = (cnt[a] + new_cnt) % MOD
total[a] = (total[a] + new_sum) % MOD

(total.values()) % MOD

# Demo
si __name_ == "__main__":
sol = Solución()
print(sol.sumOfGoodSubsequences([1, 2, 1])) # 14
print(sol.sumOfGoodSubsequences([3, 4, 5])) # 40
`` `

### 5.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int sumOfGoodSubsequences(vector seleccionadoint implicados nums) {
const int MOD = 1'000'007;
const int MAX_VAL = 100000;
vector realizado largamente larga cnt(MAX_VAL + 3, 0);
vector realizado largamente larga suma (MAX_VAL + 3, 0);

para (int a : nums) {
int idx = a + 1; // cambio por +1
c_left largo = cnt[idx - 1]; // a-1
c_right largo = cnt[idx + 1]; // a+1
t_left largo = sum[idx - 1];
t_right largo = sum[idx + 1];

largo tiempo nuevo Cnt = (c_left + c_right + 1) % MOD;
long long long newSum = (t_left + t_right + 1LL * a * newCnt) % MOD;

cnt[idx] = (cnt[idx] + newCnt) % MOD;
sum[idx] = (sum[idx] + newSum) % MOD;
}

ans largos = 0;
(auto v : suma) ans = (ans + v) % MOD;
retorno (int)ans;
}
};

/ Demo
int main() {}
Sol de solución;
cout se realizó el sol.sumOfGoodSubsequences({1, 2, 1})
cout se hizo el sol.sumOfGoodSubsequences({3, 4, 5})
}
`` `

-...

## 6VIEW⃣ Complexity Analysis

TEN ANTE TEN ANTE Java ANTERIOR Python
Silencio------------...
TENIDO EL TIEMPO TENIDO `O(n + MAX_VAL)` Silencio `O(n + MAX_VAL)` Silencio
Silencioso de memoria (arrayos de 100k) Silencioso `O(MAX_VAL)` (hash-maps pero efectivamente el tamaño de la matriz) Silencio
Silencio ¿Por qué `MAX_VAL`? Valores actuales hasta `10^5`; asignamos ranuras `100003`. El uso de `defaultdict` mantiene la memoria proporcional a valores distintos. Igual que Java. Silencio

Todos corren cómodamente dentro de 1 s y 512 MB límites.

-...

## 7ف⃣ SEO‐Ready Blog: “Sum of Good Subsequences – The Good, The Bad & The Ugly”

■ *Si te estás preparando para una entrevista de ingeniería de software, LeetCode 3351 es un problema **must‐solve**. A continuación se muestra un profundo-dive que descompone el truco DP, muestra código Java/Python/C++ y explica cada trampa que podría enfrentar. *

### 7.1 Intro

■ “Hoy, estamos abordando **LeetCode 3351: Sum of Good Subsequences** – un problema que pone a prueba su comprensión de la programación dinámica, la aritmética modular y el manejo del borde. ”

### 7.2 El “bueno”

- **Simplicidad** – El DP con arrays es **forward** y escala linealmente.
- Modularidad... El algoritmo naturalmente maneja valores repetidos y los valores del borde de `0`/`MAX`.
- **Reusabilidad** – El mismo patrón ( " cnt " + " ) se aplica a muchos problemas de subsequencia “adyacentes” (por ejemplo, subsecuencias al estilo Fibonacci).

### 7.3 El "Bad"

- **Index Off‐by‐One** - Olvidar el cambio por `+1` conduce a `ArrayIndexOutOfBounds` en Java/C++ o un `KeyError` en Python.
- **Overflow** – Usar `int` en lugar de `long` en Java o `int` en C++ causa flujos silenciosos.
- **Modulo Mis-placement** – Añadiendo grandes números antes de tomar modulo puede exceder `64-bit` y dar respuestas incorrectas.

### 7.4 El "Ugly"

- **Boundaries** – Cuando `a` es `0` o `100000`, el DP ingenuo intentaría acceder a `cnt[-1]` o `cnt[100001]`.
- **Hash‐Map Overhead** – Python `defaultdict` se ve elegante pero puede desperdiciar la memoria si muchos valores distintos.
- **Readability vs. Performance** – Demasiadas declaraciones de `% MOD` pueden romper el código, pero son esenciales.

### 7.5 Final Takeaway

■ “LeetCode 3351 no es sólo un juguete. Es un microcosmos de problemas de entrevistas del mundo real donde una sola línea de DP puede convertir una pesadilla exponencial en un algoritmo lineal. Domine este patrón y usted ace muchas preguntas basadas en subsequence. ”

-...

## 8️ Pensamientos de clausura

- El DP arriba es la solución **canónica**; si lo presentas claramente en una entrevista, mostrarás una comprensión profunda de *definición del estado*, *transición* y *aritmética modular*.
- Variaciones de la práctica: cambiar " cnt " a " suma " a " larga " o utilizar " noordened_map " para obtener datos escasos.
- Tenga en cuenta el truco “shift by +1”; es un salvavidas para la seguridad de límites en todos los idiomas.

¡Buena suerte con tu entrevista, y que las buenas sucesivas* estén siempre a tu favor! 🚀

-...

¡Feliz codificación! *