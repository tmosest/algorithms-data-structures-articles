-...
Título: LeetCode 782. Transformar a Chessboard -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

# 🏰 Transformar en Ajedrez – LeetCode 782
### The Good, the Bad, and the Ugly – A Complete, SEO‐Optimized Guide

■ **TL;DR** – En una sola línea puede convertir una tabla binaria en un tablero de ajedrez intercambiando filas y columnas. El truco es validar el patrón, contar desajustes, fijar la paridad y dividir por dos.
■
■ Complejidad: **O(n2)** tiempo, **O(1)** espacio auxiliar.
■
■ Código: **Java, Python, C+** – comentó completamente, listo para la entrevista.

-...

## Tabla de contenidos

1. [Declaración sobre el proyecto] (declaración sobre el problema)
2. [Por qué es difícil](#why-its-hard)
3. [Solution Overview](#solution-overview)
* Comprobación de validez de 1 paso
* ✅ Contando swaps para columnas de filas
* ✅ Manipulación impar vs incluso tamaños
* ✅ Respuesta final = (rowSwaps + colSwaps) / 2
4. [Detailed Algorithm](#detailed-algorithm)
5. [Proof of Correctness](#proof-of-correctness)
6. [Análisis de complejidad](#complexidad-análisis)
7. [Edge Cases ' Pitfalls](#edge-cases--pitfalls)
8. [Java Implementation](#java-implementation)
9. [Python Implementation](#python-implementation)
10. [C+++](#c-implementation)
11. [Testing & Sample Runs](#testing--sample-runs)
12. [Takeaway & Interview Tips](#takeaway--interview-tips)
13. [SEO Palabras clave " Metadatos](#seo-keys)

-...

## 1. Declaración de problemas

■ **LeetCode 782 – Transformar en Ajedrez* *
■ Dificultad**: Difícil
■
■ Dado un `n × n` cuadrícula binaria `board`, puede cambiar cualquier dos filas o cualquier dos columnas cualquier número de veces.
■ Regrese el número mínimo de movimientos** requerido para transformar el tablero en un **cheboard** (es decir, no dos células adyacentes comparten el mismo valor). Si es imposible, devuelve `-1`.

-...

## 2. Por qué es difícil

* **Constraint: ** `n` ≤ 30 - lo suficientemente pequeño para un algoritmo `O(n2)`, pero todavía necesita un truco de validación *linear-time*.
* ** Problema de la paridad:** Incluso vs. el tamaño del tablero extraño cambia el número óptimo de swaps.
* **Simetría de Raíz/Columno:** Las filas y columnas son independientes pero deben cumplir las mismas reglas de viabilidad.
* **Counting Swaps Efficiently:** No puedes simular cada swap; necesitas una fórmula basada en desajustes.

-...

## 3. Panorama general de la solución

1. ** Comprobación de viabilidad* *
* Cada célula debe satisfacer
`board[r][c] == board[0] [0] ^ board[r] [0] ^ board[0][c].
* Si alguna célula viola esto, el tablero no puede ser transformado → retorno `-1`.

2. **Count Row ' Column Mismatches* *
* Para filas: cuenta cuántas filas coinciden con el patrón `[0,1,0,1,...]`.
* Para columnas: cuenta cuántas columnas coinciden con el patrón `[0,1,0,1,...]`.
* También compute `rowSwap` = número de filas que ya comienzan con la paridad correcta (es decir, `board[r][0] == r % 2`).
* Análogamente para `colSwap`.

3. ** Frecuencias de valor**
* El recuento de `1`s en cualquier fila o columna debe ser `n/2⌋` o `n/2⌉`.
* Si no, la transformación es imposible.

4. **Compute Minimal Swaps**
*Even n.*
* `rowSwaps = min(rowSwap, n - rowSwap)`
* `colSwaps = min(colSwap, n - colSwap)`
################################################################################################################################################################################################################################################################
* La paridad inicial debe coincidir con la mayoría.
* If `rowSwap` is odd → `rowSwap = n - rowSwap`
* Del mismo modo para `colSwap`.

5. **Respuesta*
* Cada swap fija dos posiciones, por lo que el total se mueve = `(rowSwaps + colSwaps) / 2`.

-...

## 4. Algoritmo detallado (Step‐by‐Step)

`` `
n = pensión. longitud
rowSum = colSum = 0
rowSwap = colSwap = 0

// 1. Verificación de viabilidad
para r en 0.n-1:
para c en 0.n-1:
(board[0] [0] ^ board[r][0] ^ board[0][c] ^ board[r][c]) == 1:
retorno -1

// 2. Contar filas/collos que son “buenos” y desajustes
para mí en 0.n-1:
rowSum += board[0][i] // número de 1s en primera fila
colSum +=board[i][0] // número de 1s en la primera columna
rowSwap += (board[i] == # 1 : 0
colSwap += (board[0][i] == # 1 : 0

// 3. Validar 1-cuentas
si rowSum no en [n/2, (n+1)/2] o colSum no en [n/2, (n+1)/2]:
retorno -1

// 4. Cambios ajustados basados en la paridad
si n % 2 == 1: // tamaño de la tabla
si rowSwap % 2 == 1: rowSwap = n - rowSwap
si colSwap % 2 == 1: colSwap = n - colSwap
más: // incluso tamaño de la tabla
rowSwap = min(rowSwap, n - rowSwap)
colSwap = min(colSwap, n - colSwap)

// 5. Regresar movimientos mínimos
retorno (rowSwap + colSwap) / 2
`` `

-...

## 5. Prueba de la corrección

1. ** Estado de viabilidad**
* Para cualquier dos filas `r1, r2` y dos columnas `c1, c2`, las cuatro celdas `(r1,c1),(r1,c2),(r2,c1),(r2,c2) ` debe formar un patrón de tablero de control.
* Algebraicamente, esto es equivalente a la condición XOR arriba.
* Si el tablero falla esto, ninguna secuencia de swaps puede fijar el patrón.

2. **Cuento de la cintura o el algodón**
* Las hileras que ya están en el patrón deseado con aquellas que no reducen los desajustes por exactamente uno cada uno.
* El número mínimo de swaps para hacer que todas las filas se alternan es `min(rowSwap, n-rowSwap)` para incluso `n`; para extraño `n`, la paridad fuerza una orientación exacta.

3. **División por Dos**
* Un solo intercambio de dos filas corrige dos posiciones (las dos filas).
* Igualmente para columnas.
* Así, el número total de movimientos equivale a la mitad de los desajustes totales.

El algoritmo sigue los pasos lógicos anteriores, garantizando movimientos mínimos si el tablero es transformado.

-...

## 6. Análisis de la complejidad

****Time:**
* Comprobación de viabilidad: `O(n2)`
* Contando bucles: `O(n)` (realmente `O(n)` para cada uno de los dos pases, todavía `O(n)`)
* Total: **O(n2)** (dominante por comprobación de viabilidad)

* **Espacio*
* Sólo un puñado de contadores enteros → **O(1)** espacio auxiliar.

Con 'n ≤ 30', esto funciona en microsegundos en cualquier máquina moderna.

-...

## 7. Casos de borde " Pitfalls

Silencio Caso tóxico Qué ver para Silencio
Silencio...
La Paridad de `rowSwap '/`colSwap` debe ser incluso. Silencio
Silencio **Cuento de propiedad/col** Silencio Número de 1s debe ser `n/2 ' o `(n+1)/2 ' . Silencio
Silencio **Todas las ceros o todas las demás** ← La feasibilidad falla inmediatamente. El cheque de la XOR permanente lo atrapa. Silencio
Silencio **Large n (30)** Silencio Todavía O(n2) – seguro. ← No se necesita optimización. Silencio
Silencio **Cambiando la misma fila dos veces** No es necesario, la formula lo maneja. Silencio

-...

## 8. Aplicación de Java

``java
*
* 782. Transformar en Ajedrez
*
* Solución Java que funciona en tiempo O(n^2) y espacio O(1).
* Implementa la estrategia de recuento óptima explicada anteriormente.
*/
Clase Solución {
public int movesToChessboard(int[][] board) {
int n = tabla. longitud;
int rowSum = 0, colSum = 0; // número de 1s en primera fila/column
int rowSwap = 0, colSwap = 0; // filas/cols ya en la paridad correcta

--------- 1. Verificación de la viabilidad ---------- */
para (int r = 0; r) {}
para (int c = 0; c) {}
// board[r][c][0][0] ^ board[r][0] ^ board[c]
if ((board[0][0] ^ board[r][0] ^ board[c] [c] ^ board[c]) " 1) == 1) {
retorno -1;
}
}
}

--------- 2. Contando filas/collos que encajan...--------
para (int i = 0; i)
rowSum += board[0][i]; // 1s en primera fila
colSum += board[i][0]; // 1s en primera columna
si (board[i][0] == (i & 1)) filaSwap++; // fila comienza con la paridad correcta
si (board[0][i] == (i " 1)) colSwap++; // columna comienza con la paridad correcta
}

--------- 3. Validar 1 cuenta...------
si (rowSum ) no se realizó / 2 Silencioso filaSum  Conf (n + 1) / 2) retorno -1;
si (colSum) se realizó n / 2 Silenciosos en secreto (n +1) / 2) retorno -1;

--------- 4. Cambios ajustados basados en la paridad--------
(n) == 1) { // tamaño de tabla impar
((rowSwap) == 1) rowSwap = n - rowSwap;
(colSwap) == 1) colSwap = n - colSwap;
} más { // incluso tamaño de la tabla
rowSwap = Math.min(rowSwap, n - rowSwap);
colSwap = Math.min(colSwap, n - colSwap);
}

--------- 5. Respuesta final...
retorno (rowSwap + colSwap) / 2;
}
}
`` `

-...

## 9. Aplicación de los pitones

``python
"
LeetCode 782 - Transformar a Chessboard
Python 3 solución – O(n^2) tiempo, O(1) espacio
"

Solución de clase:
def movesToChessboard(self, board: list[list[int]) - título int:
n = len(board)
row_sum = col_sum = 0
row_swap = col_swap = 0

1. Verificación de viabilidad
para r en rango(n):
para c en el rango(n):
si (board[0][0] ^ board[r][0] ^ board[c] [c] ^ board[r][c]) " 1:
retorno -1

# 2. Contando filas/collos que encajan
para i en rango(n):
row_sum += board[0][i]
col_sum += board[i][0]
if board[i][0] == (i " 1): row_swap += 1
si la tabla [0][i] == (i " 1): col_swap += 1

# 3. Validar 1 cuenta
si no (n//2 <= row_sum )= (n+1)//2): retorno -1
si no (n//2 <= col_sum )= (n+1)//2): retorno -1

# 4. Ajustar los intercambios basados en la paridad
si n % 2:
si row_swap % 2: row_swap = n - row_swap
si col_swap % 2: col_swap = n - col_swap
más:
row_swap = min(row_swap, n - row_swap)
col_swap = min(col_swap, n - col_swap)

# 5. Regresar movimientos mínimos
(row_swap + col_swap) // 2
`` `

-...

## 10. C++ Implementación

``cpp
*
* 782. Transformar en Ajedrez
*
* Solución C++: O(n^2) tiempo, espacio O(1).
* Usa la misma estrategia de conteo óptima.
*/
Clase Solución {
public:
int movesToChessboard(vector seleccionadovector identificadointющ board) {
int n = board.size();
int rowSum = 0, colSum = 0; // número de 1s en primera fila/column
int rowSwap = 0, colSwap = 0; // filas/cols ya en la paridad correcta

--------- 1. Verificación de la viabilidad ---------- */
para (int r = 0; r) {}
para (int c = 0; c) {}
(board[0] [0] ^ board[r][0] ^ board[0][c] ^ board[r][c]) "
retorno -1;
}
}
}

--------- 2. Contando filas/collos que encajan...--------
para (int i = 0; i) {}
rowSum += board[0][i];
colSum += board[i][0];
si (board[i] [0] == (i " 1)) ++rowSwap;
(board[0][i] == (i ' 1)) ++colSwap;
}

--------- 3. Validar 1 cuenta...------
si (rowSum > n/2 ¦
si (colSum י n/2 TENIDO TENIDO ColSum √≥ (n+1)/2) regreso -1;

--------- 4. Cambios ajustados basados en la paridad--------
(n " 1) { //
si (rowSwap " 1) rowSwap = n - rowSwap;
si (colSwap " 1) colSwap = n - colSwap;
♪ otra vez { // incluso
rowSwap = min(rowSwap, n - rowSwap);
colSwap = min(colSwap, n - colSwap);
}

--------- 5. Respuesta final...
retorno (rowSwap + colSwap) / 2;
}
};
`` `

-...

## 11. C Aplicación

`` c
*
* 782. Transformar en Ajedrez
*
* Solución C – O(n^2) tiempo, espacio O(1).
* Escrito en plan C para la máxima portabilidad.
*/
int movesToChessboard(int** bordo, int n) {
int rowSum = 0, colSum = 0;
int rowSwap = 0, colSwap = 0;

--------- 1. Verificación de la viabilidad ---------- */
para (int r = 0; r) {}
para (int c = 0; c) {}
if (board[0][0] ^ board[r][0] ^ board[c] [c] ^ board[r][c]]
retorno -1;
}
}

--------- 2. Contando filas/collos que encajan...--------
para (int i = 0; i)
rowSum += board[0][i];
colSum += board[i][0];
(board[i][0] == (i " 1)) rowSwap++;
(board[0][i] == (i " 1)) colSwap+++;
}

--------- 3. Validar 1 cuenta...------
si (rowSum > n/2 ¦
si (colSum י n/2 TENIDO TENIDO ColSum √≥ (n+1)/2) regreso -1;

--------- 4. Cambios ajustados basados en la paridad--------
(n " 1) { //
si (rowSwap " 1) rowSwap = n - rowSwap;
si (colSwap " 1) colSwap = n - colSwap;
♪ otra vez { // incluso
rowSwap = rowSwap rowSwap : n-rowSwap;
colSwap = colSwap colSwap : n-colSwap;
}

--------- 5. Respuesta final...
retorno (rowSwap + colSwap) / 2;
}
`` `

■ **Nota:** En C, se supone que la tabla 'int** es un array cuadrado 2-D.

-...

## 12. Recap & Takeaway

* **Optimality** – el algoritmo produce el *fewest* swaps posible.
* **Simplicidad** – sólo unos contadores enteros; no hay estructuras de datos pesadas.
* **Robustness** – maneja tamaños impares, cheques de frecuencia, ajustes de paridad.
* **Performance** – `O(n2)` es trivial para `n ≤ 30`, pero escala agradable para entradas más grandes.

Esta solución es un favorito en mi repertorio de entrevista y ha demostrado ser tanto *fast* como *clean*.

-...

Pensamientos finales

Transformar una tabla en un tablero de control no es sólo sobre el intercambio; se trata de entender las limitaciones algebraicas subyacentes y el aprovechamiento de la paridad. Al tratar filas y columnas simétricamente y contar desajustes inteligentemente, podemos calcular el número mínimo de movimientos con un solo paso sobre la matriz.

¡Feliz codificación y buena suerte aplastando la entrevista de LeetCode! 🚀

-...


■ *Si te gustó esta inmersión profunda, echa un vistazo a mis otras explicaciones de algoritmo: [160. Intersección de Dos Arrays II](https://leetcode.com/problems/intersection-of-two-arrays-ii/), [1729. Swapping Nodes in a Linked List](https://leetcode.com/problems/swapping-nodes-in-a-linked*)