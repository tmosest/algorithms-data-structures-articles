-...
Título: LeetCode 1301. Número de caminos con Max Score -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

# LeetCode 1301 – **Número de caminos con Max Score**
*Dificultad* Duro de vida **Tags:** DP, BFS, Grid, Modulo, Top-Down

-...

#### 1ICK⃣ Problema Resumen

Se le da un 'n × n` bordo (`2 ≤ n ≤ 100').
Cada célula contiene uno de los siguientes caracteres:

Personaje permanente
Silencio...
Silencioso `S` Silencio Inicio (a la derecha del fondo)
TENIDO `E` TENIDO FIN (corriente superior izquierda)
Silencio `1`-`9` Silencio Valor numérico que puede ser recogido
Silencioso `X` Silencioso Obstáculo - no se puede entrar

Usted puede mover **up**, **left**, o **up‐left** (diagonalmente) sólo si la célula objetivo no es un obstáculo.
Su objetivo es:

1. **Maximizar** la suma de dígitos recogidos a lo largo de un camino de `S` a `E`.
2. Cuenta cuántos caminos distintos alcanzan esta puntuación máxima.
El recuento debe ser devuelto modulo `1 000 000 007`.

Si no hay camino, devuelve `[0, 0]`.

-...

#### 2down⃣ Idea de solución de alto nivel

Debido a que cada movimiento permitido disminuye el índice de fila y/o columna, el gráfico es **acíclico** – nunca volver a una célula que ya ha visitado.
Esta propiedad nos permite utilizar un simple **programación dinamica** que procesa la tabla ** desde el principio (abajo derecho)** hacia la meta (a la izquierda).

Por cada celda `(i, j)` almacenamos dos valores:

Silencio `maxScore[i][j]` Silencio Suma más grande que se puede lograr cuando *arrive* en `(i, j)`. Silencio
Silencio...
TENIDO `ways[i][j]` TENIDO Número de formas de obtener ese `maxScore[i][j].

Iniciamos la celda de inicio con la puntuación `0` y `1` de manera, luego se iteran todas las celdas en orden reversa-por-row.
Para cada célula propagamos su puntuación a las tres posibles células "next" (up, izquierda, arriba).
Cuando nos propagamos

* **Reemplazar** la puntuación de la célula de destino si la nueva puntuación es mayor.
* **Añadir** a las formas de la célula de destino si la nueva puntuación es igual al máximo actual.

Debido a que cada transición es monotone (sólo “upwards”), nunca necesitamos volver a revisar una célula después de que haya sido procesada.

-...

Algoritmo (Pseudo‐Code)

`` `
MOD = 1_000_000_007
n = pensión. longitud
maxScore[n] [n] =
maneras[n][n] = 0

// Empieza en la parte inferior derecha
maxScore[n-1][n-1] = 0
maneras[n-1][n-1] = 1

para mí de n-1 a 0:
para j desde n-1 hasta 0:
si maxScore[i][j] == -∞: continue // unreachable
para cada (di, dj) en {( -1, 0), (0, -1), (-1, -1)}:
ni = i + di; nj = j + dj
si no se hizo 0 o nj 0
si la junta [ni][nj] == 'X': continuar
añadir = 0
si la tabla[ni][nj] es dígito:
añadir = int(board[ni][nj])
newScore = maxScore[i][j] + añadir
si newScore > maxScore[ni][nj]:
maxScore[ni][nj] = newScore
maneras[ni][nj] = maneras[i][j]
si no es nuevoScore == maxScore[ni][nj]:
maneras[ni][nj] = (ways[ni][nj] + ways[i][j] % MOD

respuesta = [maxScore[0][0], ways[0][0]]
si respuesta[0] == -∞: respuesta = [0, 0]
respuesta
`` `

**La complejidad* *

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencio, muerte, muerte, muerte, muerte, muerte, Silencio

Con 'n ≤ 100' esto satisface fácilmente los límites.

-...

#### 4down⃣ Implementaciones de referencia

A continuación se presentan soluciones limpias y idiomáticas para **Java, Python y C++**.

-...

##### 4.1 Java 17

``java
importar java.util*;

Solución de la clase pública {}
int final estático privado MOD = 1_000_000_007;

int[] pathsWithMaxScore(List won) {String confianza board) {
int n = board.size();
char[][] grid = new char[n][n];
para (int i = 0; i)
grid[i] = board.get(i).toCharArray();

int[][] maxScore = nuevo int[n][n];
int[][] ways = new int[n][n];
para (int[] fila : maxScore) Arrays.fill(row, Integer.MIN_VALUE);

// celda de inicio (abajo derecho)
maxScore[n - 1][n - 1] = 0;
maneras[n] [n] - 1] = 1;

int[] dx = {-1, 0, -1};
int[] dy = {0, -1, -1};

para (int i = n - 1; i 0; i--) {
para (int j = n - 1; j 0; j--) {
si (maxScore[i] [j] == Integer.MIN_VALUE) continuar; // inalcanzable
para (int dir = 0; dir 3; dir++) {}
int ni = i + dx[dir];
int nj = j + dy[dir];
si continúan (ni 0 ANTE TENIDO TENIDO NJ 0)
char ch = grid[ni][nj];
si (ch == 'X') continúan;

int add = (ch не= '1' ' де ch = '9') ? ch - '0' : 0;
int newScore = maxScore[i][j] + add;

si (newScore > maxScore[ni][nj] {}
maxScore[ni][nj] = newScore;
maneras[ni][nj] = maneras[i][j];
} si (newScore == maxScore[ni][nj]
[ni][nj] = (ways[ni][nj] + ways[i][j]) % MOD;
}
}
}
}

int final Puntuación = maxScore[0][0];
int final Ways = ways[0][0];
si (finalScore == Integer.MIN_VALUE) devuelve nuevo int[]{0, 0};
nuevo int[]{final Puntuación final Ways};
}
}
`` `

-...

##### 4.2 Python 3.10+

``python
de la importación Lista

MOD = 1_000_000_007

Solución de clase:
def paths ConMaxScore(self, board: List[str]) - List[int]:
n = len(board)
grid = [list(row) for row in board]

max_score = [[-10**9] * n for _ in range(n)]
maneras = [[0] * n para _ en rango(n)]

max_score[n-1][n-1] = 0
maneras[n-1][n-1] = 1

dirs = [(-1, 0), (0, -1), (-1, -1)]

para i en rango(n-1, -1, -1):
para j en rango(n-1, -1, -1):
si max_score[i][j] == -10**9:
continuar
para di, dj en dirs:
ni, nj = i + di, j + dj
si no se hizo 0 o nj 0
continuar
ch = grid[ni][nj]
si ch == 'X':
continuar
añadir = int(ch) si ch.isdigit() otro 0
nuevo = max_score[i][j] + añadir

si nuevo > max_score[ni][nj]:
max_score[ni][nj] = new
maneras[ni][nj] = maneras[i][j]
elif new == max_score[ni][nj]:
maneras[ni][nj] = (ways[ni][nj] + ways[i][j] % MOD

si max_score[0] [0] == -10**9:
[0, 0]
[max_score[0][0], ways[0][0]]
`` `

-...

##### 4.3 C++ 17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
const int MOD = 1'000'007;

vector significando caminos de confianzaConMaxScore(vector seleccionadostring ventaja) {
int n = board.size();
vector seleccionado(n, vector)
vector seleccionado(n, vector)

// celda inferior derecha
score[n-1][n-1] = 0;
maneras[n-1][n-1] = 1;

const int dx[3] = {-1, 0,1};
const int dy[3] = { 0,-1,-1};

para (int i = n-1; i 0; --i) {
para (int j = n-1; j 0; --j) {
si (score[i][j] == INT_MIN) continúan; //
para (int dir = 0; dir 3); ++dir) {
int ni = i + dx[dir], nj = j + dy[dir];
si continúan (ni 0 ANTE TENIDO TENIDO NJ 0)
char ch = board[ni][nj];
si (ch == 'X') continúan;

int add = (ch не= '1' ' де ch = '9') ? ch - '0' : 0;
int newScore = score[i][j] + add;

si (newScore > score[ni][nj]) {}
score[ni][nj] = newScore;
maneras[ni][nj] = maneras[i][j];
} si (newScore == score[ni][nj]) {}
[ni][nj] = (ways[ni][nj] + ways[i][j]) % MOD;
}
}
}
}

si (score[0] [0] == INT_MIN) regresa {0, 0};
[0] [0], way[0][0]};
}
};
`` `

-...

#### 5down⃣ “Good‐and‐Bad” Insight – The **Good‐Path** vs. **Bad‐Path**

Silencio Silencio Silencio Silencio Silencio Silencio
Silencio...
Silencio **Complejidad** Silencio `O(n2)` Silencio Requiere recursión de arriba hacia abajo + memoización → todavía `O(n2)` pero más pesado
Silencioso **Implementation Effort** Silencio 30 min Silencio 30 min Silencio 30 min Silencio
Silencio **Mimory Footprint** Silencio `O(n2)` Silencio `O(n2)` Silencio
Silencio **Readability** Silencio Muy alta Silencio Muy alta Silencio Muy alta
Silencio **Por qué funciona** tención Graph es un DAG – no ciclos → linear DP TENIDO Mismo razonamiento TENIDO

■ **Bottom‐Line:** Un solo pase DP es el “buen camino” que gana en el tiempo y la memoria.

-...

#### 6down⃣ The Good‐Path vs. The Bad‐Path (Common Mistakes)

TENIDO MÁS INVESTIGACIÓN ANTERIOR Por qué sucede ANTERIENTE Cómo arreglar 
Silencio...
tención **1️ Añadiendo el valor de la celda de inicio** Silencio `S` es *no* un dígito – no debe ser contado. Tréate `S` como puntaje `0` solamente. Silencio
Silencio Olvidar los obstáculos** tención Sendero puede "pasar" a una célula "X" y estrellar el programa. Silencioso Explicit `if (ch == 'X') continue;`
tención **3 ride Using Utilizando `int` para puntuar en una tabla de 32 bits** TEN La puntuación máxima posible es `9 × (n2‐2)` – todavía encaja en `int`, pero cuando usas `Integer. MIN_VALUE` como "inalcanzable" debe tener cuidado de no desbordarse. Silencio Use un centinela (`-INF` o `-109`) que está muy por debajo de cualquier puntaje real. Silencio
tención **4Ω⃣ Modulo en cada adición** Silencio Sólo 'siempre' necesita modulo. Las puntuaciones no. Mantener puntuaciones como `int`/`long`; aplicar `% MOD` sólo en `ways`. Silencio
[0], maneras[0][0] cuando el objetivo es inalcanzable produce un puntaje de basura. Después del bucle DP, si `maxScore[0][0]` es todavía `-INF`, retorno `[0, 0]`. Silencio

-...

### 7down⃣ Testing Your Own Board

``python
Python – prueba rápida de cordura
si __name_ == "__main__":
sol = Solución()
Tablero =
"S123",
"X1X1",
"2X2E",
"121X"
]
print(sol.pathsWithMaxScore(board)) #  Usa [max_score, ways]
`` `

Siéntete libre de ajustar la tabla y ver cómo se comporta el algoritmo.

-...

## 🎯 Why This Matters for Your Interview Prep

Silencio . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 
Silencio...
Silencio ** Ciclos de Manchas Con Gracia** Silencio El tablero es un DAG, por lo que un único barrido DP es suficiente. Silencio
tención **Definición del estado claro** Silencioso `maxScore` + `ways` es un par de DP de libro de texto. Silencio
Silencio **Conteo Moderno** Silencio El truco del modulo es un elemento básico en problemas de la red. Silencio
Silencio ** Fácil de Traducir** Silencio El mismo patrón funciona en *cualquier idioma* (Java, Python, C++). Silencio

-...

## 🔍 Search‐Friendly Summary

* LeetCode 1301 – Número de caminos con Max Score
* Acyclic grid DP – `O(n2)` time, `O(n2)` espacio
* Estado bidimensional: `maxScore` ' (mod `1e9+7`)
* Código de referencia: **Java, Python, C+**

-...

#### 📚 Más lectura

TENIDO TÉpico TENIDO Enlace ANTE
Silencio...
Silencio Grid DP Patterns ANTE https://leetcode.com/explore/learn/card/advanced-dynamic-programming/ Silencio
← Aritmética Modular en DP Silencio https://cp-algorithms.com/algebra/modular-arithmetic.html Silencio
Silencio Top‐down vs. Bottom‐up DP Silencio https://www.geeksforgeeks.org/dynamic-programming/ Silencio

Feliz codificación, y que sus puntuaciones siempre sean *maximum*! 🚀