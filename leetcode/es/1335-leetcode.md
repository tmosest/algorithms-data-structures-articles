-...
Título: LeetCode 1335. Dificultad mínima de un horario de trabajo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 1335 – Dificultad mínima de un horario de trabajo
■ **Hard Silencio DP Silencio Recursion + Memoization ← O(n·d) Time Silencio O(n·d) Space**

## Tabla de contenidos
1. [Restatement del Problema](restatement del Problema)
2. [Por qué es difícil](#why-its-hard)
3. [Brute‐Force Idea (The Ugly)](#brute-force-idea-the-ugly)
4. [Optimal DP Solution (The Good)](#optimal-dp-solution-the-good)
5. [Edge Cases & Common Pitfalls (The Bad)] (#edge-cases--common-pitfalls-the-bad)
6. [Java / Python / C++ Código](#code)
* Java
* Python
* C++
7. [Análisis de complejidad](#complexidad-análisis)
8. [SEO‐Friendly Takeaway](#seo-friendly-takeaway)

-...

## Problema Restatement

Se le da un array `jobDifficulty` donde `jobDifficulty[i]` es la dificultad del trabajo *i*‐th, y un entero `d` - el número de días que tiene que terminar todos los trabajos.

- Los trabajos deben completarse en orden**.
- Cada día debes terminar con un trabajo.
- La dificultad de un día = la dificultad **maximum** entre los trabajos completados ese día.
- La dificultad total de un horario = suma de las dificultades diarias.

** Objetivo:** Minimizar la dificultad total.
Si no puedes terminar todos los trabajos en exactamente `d ' días (es decir, `jobDifficulty.length ' ), devolver `-1`.

-...

## Why It's Hard

1. **Partición** – necesitas dividir el array en segmentos contiguos.
2. **Exponential search space** – el punto de división de cada día es una opción.
3. **Objetivo no lineal** – el costo de un segmento es su máximo, no una suma.
4. **Pequeña `d` pero grande `n`** - `n` puede ser 300 mientras `d` ≤ 10, que significa un algoritmo que es `O(n2·d)` está bien, pero cualquier cosa peor comienza a morder.

-...

# Brute‐ Fuerza Idea (El Ugly)

Una recursión ingenua intenta cada punto de división por cada día:

``text
helper(idx, daysLeft):
días Izquierda
volver max(jobDifficulty[idx..end])
mejor = JUEGO
maxDay = - hígado
para mí en idx ... final - días Izquierda + 1: // elegir división después de que yo
maxDay = max(maxDay, jobDifficulty[i])
mejor = min(mejor, maxDay + helper(i+1, díasLeft-1)
mejor
`` `

*Problemas*

- Plazo exponencial (`O(2^n)`caso peor).
- Los subproblemas repetidos causan una recomputación masiva.
- La profundidad de las pilas puede llegar a " n " (riesgo de la sobrefluencia de las pilas en grandes entradas).
- Difícil de leer y mantener.

■ *La parte “muy”:* este es el primer código que escribirás; muestra el *concepto*, pero falla en pruebas más grandes.

-...

## Optimal DP Solution (The Good)

### 1. DP State

`dp[i][k]` = mínima dificultad para terminar **primer `i` puestos de trabajo** en **exactamente `k ' días**.

- " I " ranges from `1 ... n "
- " k " ranges from `1 ... d `

### 2. Transición

Para el último día (día `k`) escogemos un punto de división `t` (`k-1 ≤ t ' )

`` `
dp[i][k] = min over t ( dp[t][k-1] + max(jobDifficulty[t+1 ... i]) )
`` `

Durante el bucle interior mantenemos el máximo de funcionamiento para que la computación
`max(jobDifficulty[t+1 ... i])` es `O(1)` para cada `t`.

### 3. Iniciación

- `dp[i][1] = `max(jobDifficulty[1 ... i])`
(Todos los trabajos del día 1 están fijos – no se puede dividir más.)

### 4. Resultado

" dp[n][d] " (primer `n ' empleo en ' días " ).
Si `n ecto d` → `-1` inmediatamente.

### 5. Por qué funciona

La partición del array está codificada implícitamente en la elección de `t`.
Desde `d ≤ 10`, los bucles de 3 etapas (`n·d·n`) son en la mayoría de las operaciones `300·10·300 ♥ 9×105` – cómodamente rápido.

### 6. Consejos de aplicación

Silencio .
Silencio...
TEN **Iterative DP** Silencio Evita los problemas de profundidad de la recidiva. Silencio
Silencio **Hacia atrás máx** Silencio Actualizaciones `maxDay` dentro del bucle interior - no extra `max()` llamadas.
tención **Sentinel row** TENIDO Una fila de señales `-1` o `∞` "no computadas". Silencio

-...

## Edge Cases & Common Pitfalls (The Bad)

← Mala práctica ← Qué puede ir mal
Silencio...
Silencio Utilizando `dp[0][*]` como 0 voca El problema garantiza *al menos un* trabajo por día; `dp[0][k] ` debe ser ``rígido' por 'k' 0`. Silencio
tención Off‐by-one errores en índices tención Recordar índices de array en Java/Python/C++ iniciar en 0, pero `dp` utiliza '1-basado' para legibilidad. Silencio
Silencio Olvídate de las pruebas de `n ' comprobada ' tención LeetCode incluyen este caso; debe volver `-1` inmediatamente. Silencio
Silencio Sobre-optimizing with `O(n2·d)` → `O(n·d)` via prefix maxima? Silencio Aquí no es necesario; mantenerlo sencillo y claro. Silencio

-...

# Código #
A continuación se ** tres implementaciones** – una en cada idioma – con comentarios extensos para que pueda copiar, pegar y ejecutar en sus propios casos de prueba.

■ **Todos los códigos utilizan la formulación DP descrita anteriormente. #
■ Corren en **O(n·d·n)** tiempo y **O(n·d)** memoria, que es óptima para los límites de LeetCode.

## Java

``java
importa java.util. Arrays;

Solución de la clase pública {}
public int minDifficulty(int[] jobDifficulty, int d) {
int n = trabajoDifficulty.length;
si (n י d) retorno -1; // no suficientes trabajos

// dp[i][k] : mínima dificultad para los primeros trabajos en k días
int[][] dp = nuevo int[n + 1][d + 1];
para (int[] fila : dp) Arrays.fill(row, Integer. MAX_VALUE);

// caso base: un día - título tomar el máximo del segmento
para (int i = 1; i) = n; i++) {
int max = 0;
para (int j = 1; j <= i; j++) max = Math.max(max, jobDifficulty[j - 1]);
dp[i][1] = max;
}

// rellenar la tabla DP
para (int k = 2; k <= d; k++) {/d
para (int i = k; i <= n; i++) { //
int maxDay = 0;
// probar todos los puntos de división t (último día termina en i)
para (int t = i - 1; t >= k - 1; t--) {}
maxDay = Math.max(maxDay, jobDifficulty[t]); // trabajo t
int candidate = dp[t][k - 1] + maxDay;
dp[i][k] = Math.min(dp[i][k], candidate);
}
}
}

dp[n][d];
}

// Simple principal para comprobar la cordura rápida
public static void main(String[] args) {
int[] jobs = {6, 5, 4, 3, 2, 1};
System.out.println(new Solution().minDifficulty(jobs, 2)); // 7
}
}
`` `

■ **Por qué esto es bueno* *
■ *Clean, iterative DP, single‐pass over splits, no recursion. *

-...

## Python

``python
de la importación Lista

Solución de clase:
def minDifficulty(self, jobDifficulty: List[int], d: int) - título int:
n = len(jobDifficulty)
si no se hace d:
retorno -1

# dp[i][k] mínima dificultad para los primeros trabajos en k días
dp = [float('inf')] * (d +1) para _ en rango(n + 1)]

# Base: un día
para i en rango(1, n + 1):
dp[i][1] = max(jobDifficulty[:i])

# DP transition
para k en rango(2, d + 1):
para i en rango(k, n + 1):
max_day = 0
# split before i: last job index t
para t en rango(i - 1, k - 2, -1):
max_day = max(max_day, jobDifficulty[t])
dp[i][k] = min(dp[i][k], dp[t][k - 1] + max_day)

dp[n][d]

Prueba rápida
si __name_ == "__main__":
sol = Solución()
print(sol.minDifficulty([6,5,4,3,2,1], 2)) # 7
`` `

-...

### C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minDifficulty(vector fieltro implicado trabajarDifficulty, int d) {
int n = trabajoDifficulty.size();
si (n) d) regresan -1;

vector seleccionado(d + 1, INT_MAX)

// Funda base: un día
para (int i = 1; i) = n; ++i) {}
int mx = 0;
para (int j = 0; j) i; ++j) mx = max(mx, jobDifficulty[j]);
dp[i][1] = mx;
}

// DP
para (int k = 2; k)
para (int i = k; i) {}
int mx = 0;
// el último día termina en i, división después de t
para (int t = i - 1; t
mx = max(mx, jobDifficulty[t]);
dp[i][k] = min(dp[i][k], dp[t][k - 1] + mx);
}
}
}
dp[n][d];
}
};

int main() {}
Solución s;
vector asignados empleos profesionales = {6,5,3,2,1};
cout se realizó s.minDifficulty(jobs, 2)
}
`` `

-...

## Complexity Analysis

TEN TERRITORIO TENIDO Tiempo ANTERIENTE
Silencio----------Prince------
Silencio Brute‐Force Recursion ANTE Exponential (`O(2^n)`) Silencio `O(n)` recursion deep ←
Silencio DP (iterative) Silencio **O(n2 · d)** ≤ 9 × 105 Silencio **O(n·d)**
Silencio DP (recusión + memoización) Silencio **O(n2 · d)** Silencio **O(n·d)** + pila de recursión Silencio

Dado `n ≤ 300` y `d ≤ 10`, el DP es cómodamente rápido en LeetCode.

-...

## SEO‐Friendly Takeaway

- **Keywords a la meta:** *LeetCode 1335*, *Minimum Dificultad de un horario de trabajo*, *Hard LeetCode problem*, *Java DP solution*, *Python DP solution*, *C++ DP solution*, *job scheduling algoritmo*, *entrevista de programación dinamica*, *disparo*.
- Use encabezados descriptivos (`#`, `#`) que contengan esas palabras clave: Google los ama.
- Añádase un breve párrafo resumido al principio:
``markdown
## LeetCode 1335 – Dificultad mínima de un horario de trabajo
Solución de DP duro en Java, Python y C++ que funciona en tiempo O(n·d).
Resolver el problema de programación de trabajo duro con particiones contiguas y máximos de segmento.
`` `
- Mantener el artículo bajo 1.200 palabras, espolvorear las palabras clave naturalmente, y terminar con una “call‐to-action” (por ejemplo, “Pruébalo en LeetCode y etiqueta tu solución con #Leetcode1335”).

-...

## Palabras finales

- **Bueno** – La solución DP es limpia, rápida y pasa todas las pruebas.
- **Bad** – Olvídate de la comprobación o mezcla de índices basados en 0-basados/1-basará la solución.
- **Ugly** – La primera recursión ingenua es fácil de escribir pero poco práctico; utilizarlo sólo como una herramienta de aprendizaje.

¡Feliz codificación, y buena suerte clavando esa entrevista!