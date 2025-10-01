-...
Título: LeetCode 1643. Kth Instrucciones más pequeñas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 1643 – “Kth Smallest Instruction”
*Desde los sencillos Caminos Únicos hasta un duro desafío combinatorio*

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

Usted está de pie en la esquina superior izquierda de una rejilla 'R × C`.
Sólo se puede mover **derecha** (`H`) o **abajo** (`V`).
Todas las secuencias que utilicen exactamente `V ' y `C ``s le llevarán al destino `(R,C)`.

Las secuencias se clasifican **léxicográficamente** ( ' H ' );
Dada una " k " , devuelve la secuencia más pequeña de *kth*.

`` `
destino = [2, 3], k = 1 → "HHHVV"
destino = [2, 3], k = 3 → "HHVVH"
`` `

Limitaciones
`1 ≤ R, C ≤ 15` – lo suficientemente pequeño para una mesa DP pero lo suficientemente grande que una explosión combinatoria fuerza bruta es imposible.

-...

## 2down Por qué la programación dinámica gana
*The key insight:*
En cualquier celda `(i, j)` el número de caminos restantes a la meta equivale a la suma de los caminos de la célula a la derecha `(i, j+1)` y la celda debajo `(i+1, j)` – la recurrencia clásica de los Caminos Únicos.

Con esa mesa en la mano podemos **caminar** la cuadrícula:

1. Si el camino *k*th comienza con un **derecho** movimiento, debe pertenecer al primer `dp[i][j+1]` caminos lexicográficamente más pequeños.
2. De lo contrario el camino comienza con un **down** movimiento y restamos los primeros `dp[i][j+1]` caminos de *k* y continuamos.

Esta caminata codicioso corre en `O(R+C)` tiempo una vez que se construye la tabla DP.
La memoria es `O(R*C)` – cómodamente pequeña para los límites.

-...

## 3down⃣ Implementation Highlights

Silencio Idioma Silencio Silencio
Silencio...
Silencio **Java** TENIDO Utilizar `long` para mantener los recuentos del camino (`C(30,15)` Ω 155 117 520 ANTE 231). Construir DP abajo-up, luego caminar la rejilla. Silencio
Silencio **Python** Silencio `in` no tiene límites - la misma lógica del DP. `apend()` a una lista, finalmente `'.join()`. Silencio
Silencio **C+** Silencio `unsigned long` (64-bit) basta. Use `vector asignadovector realizado no firmado largo tiempo `. Silencio

■ **Bueno** – O(R·C) tiempo, memoria O(R·C), simple de entender.
■ **Bad** – Para cuadrículas mucho más grandes esto se convertiría en memoria pesada; también `long` en Java es de 64 bits pero nos quedamos muy por debajo de la corriente.
■ **Ugly** – Un enfoque combinatorial ingenuo que intenta generar todos los caminos o utiliza fórmulas factoriales rápidamente desborda o se convierte en 'O(k)' a tiempo.

-...

## 4down S Code Snippets

#### 📜 Java
``java
importar java.util*;

Solución de la clase pública {}
public String kthSmallestPath(int[] destination, int k) {
int R = destino[0] + 1; // filas incluyendo celda de inicio
int C = destino[1] + 1; // columnas incluyendo celda de inicio
long[][] dp = new long[R][C];

// última fila y columna sólo tienen una manera de terminar
para (int i = 0; i)
para (int j = 0; j)

// llenar DP abajo-up
para (int i = R-2; i 0; i--) {
para (int j = C-2; j >= 0; j--) {
dp[i][j] = dp[i+1][j] + dp[i][j+1];
}
}

StringBuilder sb = nuevo StringBuilder();
int i = 0, j = 0;
mientras que (i ecto R-1 " p " ) {
larga derecha Paths = dp[i][j+1];
si (k <= rightPaths) { // go right
sb.append('H');
j++;
# Si no #
k -= rightPaths;
sb.append('V');
i++;
}
}
// terminar la línea recta restante
sb.append("V".repeat(R-1-i));
sb.append("H".repeat(C-1-j));
devolver sb.toString();
}
}
`` `

#### Python
``python
Solución de clase:
def kthSmallestPath(self, destination: list[int], k: int) - confiar str:
R, C = destino[0] + 1, destino[1] + 1
dp = [0] * C for _ in range(R)]

# Base cases
para i en rango(R): dp[i] [C-1] = 1
j in range(C): dp[R-1][j] = 1

# build DP bottom-up
para i en rango(R-2, -1, -1):
para j en rango(C-2, -1, -1):
dp[i][j] = dp[i+1][j] + dp[i][j+1]

# Camina la cuadrícula
I = j = 0
ruta = []
mientras que yo hice R-1 y j
[j+1]: # go right
path.append('H')
j += 1
...
k -= dp[i][j+1]
path.append('V')
i += 1

# add the final straight segment
path.append('V' * (R-1-i))
path.append('H' * (C-1-j))
volver ''.join(path)
`` `

#### 📜 C++
``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
string kthSmallestPath(vector identificadoint
int R = destino[0] + 1;
int C = destino[1] + 1;
vector realizador realizado sin firma larga larga larga larga experiencia dp(R, vector asignado largo tiempo(C, 1));

/ / última fila / columna ya 1
para (int i = R-2; i 0; --i) {
for (int j = C-2; j √= 0; --j) {
dp[i][j] = dp[i+1][j] + dp[i][j+1];
}
}

Ans de cuerda;
int i = 0, j = 0;
mientras que (i ecto R-1 " p " ) {
[j+1] { // go right
ans.push_back('H');
++j;
# Si no #
k -= dp[i][j+1];
ans.push_back('V');
++i;
}
}
as.append(R-1-i, 'V');
ans.append(C-1-j, 'H');
devolver los ans;
}
};
`` `

■ Las tres soluciones son el tiempo de `O(R*C), la memoria `O(R*C), y trabajan para el tamaño máximo de la red (`15 × 15`).

-...

## 5VIEW⃣ Complexity Analysis

Silencioso Operación Java Silencioso Python
Silencio--------------------
Silencio **Hora** Silencioso `O(R·C + R+C)` TENIDO ANTERIOR ANTERIOR ANTERIOR
Silencio **Memoria**, en la vida `O(R·C)` Silencio `O(R·C)` Silencio
Silencio **Overflow risk** Silencio negligible (`dp[30] [15] ANTE 2^63`) Silencio ninguno (`int` unbounded) Silencio seguro con `unsigned long` Silencio

-...

## 6down Ed Edge‐ Caso " Qué si " Lista de verificación

Silencioso Caso Edge Silencio
Silencio...
Silencio `k` iguala el número total de caminos ¦ Walk siempre irá derecho hasta que se vea forzado, produciendo la última cadena. Silencio
TENIDA `k` igual 1 Silencio Inmediatamente tomen siempre los movimientos correctos, dando la primera fila de 'H's seguido de todas 'V's. Silencio
Silencioso Destino `[0, 0]` Silencio `R = C = 1`, DP es una sola célula, el bucle nunca corre; anexamos una cadena vacía. Silencio
[0] El problema permanente garantiza una " k " válida; de lo contrario, haríamos una excepción. Silencio

-...

## 7Get⃣ Interview‐Ready Tips

Silencio Por qué importa
Silencio...
tención **Dynamic Programming Mastery** tención La mayoría de los gerentes de contratación les encantan las soluciones DP claras. Destacar la recurrencia, los casos de base y la construcción de fondo. Silencio
Silencio ** Optimización del espacio** tención Discuss how the DP can be reduced to `O(C)` si sólo mantiene la fila actual, pero para este problema la mesa completa está bien. Silencio
Silencio **Combinatorics vs DP** Silencio Show you understand why factorial‐based enumeration fails (overflow, time). Silencio
Silencio **Testing** tención Generar cuadrículas aleatorias (≤15) y cheque de fuerza bruta con `itertools. producto` para pequeños tamaños. Silencio
Silencio ** Estilo de codificación** TENIDO Nombres variables claros (`rightPaths`, `dp`), funciones de respuesta individual y comentarios. Silencio

■ **Entrevista de gancho**: "¿Puedes encontrar el camino kth en una rejilla 'R × C` sin enumerar todas las posibilidades?" Esta pregunta es una favorita en las entrevistas algorítmicas y aparece en LeetCode 1643. Entréguelo, y usted asará la parte DP de casi cualquier prueba de codificación.

-...

## 8VIEW⃣ SEO‐Optimized Blog Article

■ **Meta Descripción**
■ “Aprenda a resolver LeetCode 1643 – Kth Instrucción más pequeña – con programación dinámica. Obtenga el código en Java, Python, C++ y consejos de entrevista para la caza de empleo. ”

-...

# Kth Instrucción más pequeña - LeetCode 1643 – Un completo Guía

## 🗒 ¿Qué es “Kth Smallest Instruction”?
LeetCode 1643 es un problema de combinación de cuadrículas que te desafía a devolver la secuencia más pequeña de movimientos que conduce desde la esquina superior izquierda a un destino de cuadrícula utilizando sólo los pasos correctos (`H') y abajo (`V').

■ **Keywords**: *Kth Smallest Instruction*, *LeetCode 1643*, *grid path combinatorics*, *dinamic programming interview question*, *grid path DP*, *unique paths*

## 🎯 Why It's a Must‐Know Interview Problem
- ** Conceptos del contrato**: Relaciones de repetición, combinatoria, orden léxicográfico.
- ** Práctica de codificación**: Perfecto para practicar DP, manipulación de cuerdas y toma de decisiones codicciosas.
- **Real‐World Application**: algoritmos de navegación, planificación de movimiento robot y optimización combinatoria.

-...

## 📑 Declaración de problemas (en pocas palabras)

`` `
int[] destination = {R, C}; // R rows, C columns (1‐indexed)
int k; // 1‐indexed position in classified path list
devolver kth lexicográficamente menor secuencia de 'H' y 'V'.
`` `

Constraints: `1 ≤ R, C ≤ 15`.

-...

## 🔍 Approach: Bottom‐Up DP + Greedy Walk

1. **DP Table**:
dp[i][j] = dp[i+1][j] + dp[i][j+1]
Casos de base: última fila / columna → 1.

2. **Greedy Walk**:
En la celda " i, j) " , si `k ' es ≤ `dp[i] [j+1] ' , el siguiente movimiento es `H ' ; de lo contrario `V ' y subtract `dp[i][j+1] ' de `k ' .

3. **Finish Straight**:
Una vez que estés en la última fila o columna, anexa los `V's restantes o `H`s.

-...

## 🏁 Complexity

- **Hora**: `O(R · C)` para construir DP + `O(R + C)` para caminar = `O(R·C)`.
- **Espacio**: `O(R · C)` (≤ 256 celdas para los límites dados).

-...

## 🛠ف Full Code (Java, Python, C++)

## Java
``java
importar java.util*;

Solución de la clase pública {}
public String kthSmallestPath(int[] destination, int k) {
int R = destino[0] + 1;
int C = destino[1] + 1;
long[][] dp = new long[R][C];

para (int i = 0; i)
para (int j = 0; j)

para (int i = R-2; i 0; i--) {
para (int j = C-2; j >= 0; j--) {
dp[i][j] = dp[i+1][j] + dp[i][j+1];
}
}

StringBuilder sb = nuevo StringBuilder();
int i = 0, j = 0;
mientras que (i ecto R-1 " p " ) {
[j+1] {}
sb.append('H');
j++;
. ♫ ... {
k -= dp[i][j+1];
sb.append('V');
i++;
}
}
sb.append("V".repeat(R-1-i));
sb.append("H".repeat(C-1-j));
devolver sb.toString();
}
}
`` `

## Python
``python
Solución de clase:
def kthSmallestPath(self, destination: list[int], k: int) - confiar str:
R, C = destino[0] + 1, destino[1] + 1
dp = [[1] * C para _ en rango(R)]

para i en rango(R-2, -1, -1):
para j en rango(C-2, -1, -1):
dp[i][j] = dp[i+1][j] + dp[i][j+1]

ruta = []
I = j = 0
mientras que yo hice R-1 y j
[j+1]:
path.append('H')
j += 1
más:
k -= dp[i][j+1]
path.append('V')
i += 1

path.append('V' * (R-1-i))
path.append('H' * (C-1-j))
volver ''.join(path)
`` `

### C++
``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
string kthSmallestPath(vector identificadoint
int R = destino[0] + 1;
int C = destino[1] + 1;
vector realizador realizado sin firma larga larga larga larga experiencia dp(R, vector asignado largo tiempo(C, 1));

para (int i = R-2; i 0; --i) {
for (int j = C-2; j √= 0; --j) {
dp[i][j] = dp[i+1][j] + dp[i][j+1];
}
}

Ans de cuerda;
int i = 0, j = 0;
mientras que (i ecto R-1 " p " ) {
[j+1] {}
ans.push_back('H');
++j;
. ♫ ... {
k -= dp[i][j+1];
ans.push_back('V');
++i;
}
}
as.append(R-1-i, 'V');
ans.append(C-1-j, 'H');
devolver los ans;
}
};
`` `

-...

## 9️ Good, Bad, Ugly – What You should Tell Interviewers

TENIDO Aspecto ANTE TENIDO TENIDO ANTE ANTERIOR ANTERIOR ANTERIOR ANTERITO
Silencio------------------------------...
Silencio ** Complejidad Algorítmica** Silencioso `O(R·C)` DP + `O(R+C)` paseo – trivial para entrevistadores. tención Para rejillas, 2000 la tabla DP superaría los límites de memoria. Silencio Tratar de computar el camino kth a través de la enumeración factorial completa (`O(2^(R+C)')') es lento y propenso a rebosar. Silencio
Silencio **Implementación Detalle** Silencio Código claro, testable con comentarios; no hay números mágicos. Las suposiciones con códigos duros (por ejemplo, ignorando la " k " inválida) podrían suscitar sospechas. TEN Recursive brute‐force sin podar es apil-overflow y `O(2^(R+C))'. Silencio
Silencio **Edge‐Case Handling** Silencio Todos los casos de esquina cubiertos; algoritmo auto-checks. Silencio Si `k` está fuera de alcance, usted necesita lanzar un error. ← La 'k' no comprobada conduce a la indexación negativa o bucles infinitos. Silencio

■ **Declaración de la opinión pública* *
■ “Podemos encontrar el camino kth sin enumerar todos los caminos mediante la construcción de una tabla DP que cuenta los caminos restantes y luego caminar codicioso a través de la red, tomando decisiones basadas en el recuento restante. ”

-...

## 📢 Closing Thought

Mastering **LeetCode 1643 – Kth más pequeño La instrucción** muestra su capacidad de traducir problemas combinatorios en soluciones eficientes de programación dinámica. Los ejemplos de código limpio en Java, Python y C++ arriba le ayudarán a clavar la porción de codificación, y el comentario de entrevista asegura que usted puede discutir su proceso de pensamiento con confianza.

■ **Listo para el próximo desafío?** Siga practicando DP, manipulación de cuerdas y algoritmos codiciosos. ¡Su futuro empleador le agradecerá!

-...

■ **Keywords** repetidas para el máximo alcance: *Kth Smallest Instruction*, *LeetCode 1643*, *grid DP*, *divención de programación dinamica*, *planificación de ruta del robot*, *problema de caminos únicos*, *coding interview question*.

-...

### 🚀 Happy coding, and good luck with your job search!

-...


-...

■ **End of Blog**
■ Siéntete libre de compartir en GitHub, StackOverflow o comunidades de codificación, este conjunto de soluciones es el estándar de oro para LeetCode 1643.