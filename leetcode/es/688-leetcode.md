-...
Título: LeetCode 688. Probabilidad de Caballero en Ajedrez -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Soluciones de tres idiomas para “probabilidad de caballero en un tablero de ajedrez”

El problema de LeetCode **688 – Knight Probability in Chessboard** le pide que computar la probabilidad de que un caballero permanezca en una tabla *n × n* después de realizar exactamente *k* se mueve, empezando por la celda `(row, column)`.
El caballero elige uno de sus 8 posibles movimientos uniformemente al azar – incluso si el movimiento elegido lo desembarcaría fuera del tablero.
Cuando deja la tabla se detiene el proceso; de lo contrario continúa hasta que haya hecho *k* movimientos.

El enfoque más común y eficiente en el tiempo es la programación **dinámica** (DP).
A continuación encontrará implementaciones limpias y autocontenidas en **Java, Python y C+**.
Los tres comparten la misma idea algoritmo:

1. ** Estado del PPD** – `dp[i][j]` es la probabilidad de que el caballero esté en la plaza `(i, j)` después de un número determinado de movimientos.
2. **Transición** – para cada movimiento cuadrado y cada caballero legal, añadir `dp[prev] / 8.0` a la nueva red de probabilidad.
3. **Iteración** – repetir la transición exactamente *k* veces.
4. **Respuesta** – resume todas las probabilidades en la rejilla final (el caballero podría estar en cualquier parte de la junta después de *k* movimientos).

El tiempo de ejecución es **O(k · n2)** y el uso de la memoria es **O(n2)** – óptimo para las limitaciones dadas (n ≤ 25, k ≤ 100).

-...

#### 1.1 Java 17

``java
importar java.util*;

Solución de la clase pública {}
// Todos 8 caballeros se mueven
int final estático privado[][] MOVIMIENTOS = {
{-2, -1}, {-2, 1}, {-1, -2}, {-1, 2},
1, 2, 1
};

doble caballero públicoProbability(int n, int k, int row, int column) {}
dp = nuevo doble[n];
dp[row][column] = 1.0; // start position

para (en movimiento único = 0; movimiento) {}
doble[][] siguiente = nuevo doble[n][n];
para (int r = 0; r) {}
para (int c = 0; c) {}
si (dp[r] [c] == 0) continuar; // nada para difundir
para (int[] m : MOVES) {
int nr = r + m[0];
int nc = c + m[1];
si (es Valid(nr, nc, n)) {}
siguiente[nr][nc] += dp[r][c] / 8.0;
}
}
}
}
dp = siguiente;
}

doble total = 0,0;
para (int r = 0; r) {}
para (int c = 0; c) se realizó n; c++) total += dp[r][c];
}
Total de retorno;
}

booleano privado isValid(int r, int c, int n) {
devolver r √= 0 " pÃoblica r " identificados n " √ = 0 " pÃoblica c "
}
}
`` `

-...

### 1.2 Python 3

``python
de la importación Lista

Solución de clase:
# 8 posibles movimientos de caballeros
MOVES: List[List[int] = [
(-2, -1), (-2, 1), (-1, -2), (-1, 2),
(1, -2), (1, 2), (2, -1), (2, 1)
]

def knightProbability(self, n: int, k: int, row: int, col: int) - título flotante:
dp = [0.0] * n for _ in range(n)]
dp[row][col] = 1.0

para _ en rango(k):
siguiente_dp = [0.0] * n for _ in range(n)]
para r en rango(n):
para c en el rango(n):
si dp[r] [c] == 0:
continuar
para Dr, Dr. en sí mismo. MOVES:
nr, nc = r + dr, c + dc
si 0 0 0 0 0 0 0 0 0 0 0 0 0
next_dp[nr][nc] += dp[r][c] / 8.0
dp = next_dp

devolver suma(map(sum, dp))
`` `

-...

### 1.3 C+17

``cpp
Incluido el título
usando std namespace;

Clase Solución {
public:
doble caballeroProbability(int n, int k, int row, int column) {}
const int moves[8][2] = {
{-2, -1}, {-2, 1}, {-1, -2}, {-1, 2},
1, 2, 1
};

vector se llevó a cabo el doble título dp(n, vector se hizo doble(n, 0,0)
dp[row][column] = 1.0;

para (incluido paso = 0; paso) {}
vector realizador realizado(n, vectores seleccionados(n, 0,0)
para (int r = 0; r) {}
para (int c = 0; c) {}
si (dp[r] [c] == 0) continuar;
para (auto &m : movimientos) {
int nr = r + m[0];
int nc = c + m[1];
si (nr не= 0 " sensible nr " )
siguiente[nr][nc] += dp[r][c] / 8.0;
}
}
}
}
dp.swap(next);
}

doble resultado = 0,0;
para (auto &row : dp)
por (doble v : fila) resultado += v;
Resultado de retorno;
}
};
`` `

-...

## 2. Artículo del Blog: *Probabilidad de la noche en un tablero de ajedrez – El bueno, el malo y el ugly*

### 2.1 ¿Por qué este problema choca (y por qué es un tema de gran entrevista)

- Flair matemático... Combina la combinatoria, la probabilidad y la teoría del gráfico de manera tangible y visual.
- **Multiple Solution Paths** – Brute‐force recursion, memoization, iterative DP, e incluso matriz exponentiation.
- Constraints escalables La solución debe ser eficiente pero legible; un parque infantil perfecto para demostrar cambios algorítmicos.

Si usted está solicitando roles de ingeniería de software que enfatizan el pensamiento algoritmo (Google, Amazon, Facebook, etc.), dominar este problema muestra que usted puede:

- Traducir una descripción de lenguaje natural en estados formales.
- Optimize nested laops.
- Equilibrio de tiempo-espacio.

### 2.2 The Good – The Classic DP Solution

Lo que hace:
El array DP mantiene un seguimiento de *cuántas maneras* (o equivalentemente, *qué probabilidad*) el caballero puede llegar a cada celda después de un cierto número de movimientos.

**Por qué es bueno:**

TEN TERRITORIO ANTERIOR ANTERIOR
Silencio...
Silencio ** Complejidad del tiempo** Silencioso `O(k · n2)` – lineal en el número de movimientos y células de la junta. Silencio
Silencioso ** Complejidad del espacio** Silencioso `O(n2)` – sólo se necesitan dos `n × n` cuadrículas. Silencio
Silencio **La simbolidad** Silencio La transición estatal clara; fácil de depurar. Silencio
Silencio **Extensibilidad** Silencio Añadir más movimientos (por ejemplo, un “super caballero”) es un cambio trivial. Silencio

** Código de muestra (Java)** – ver arriba.

-...

### 2.3 The Bad – A Naïve Recursive Approach

Lo que parece:
Una búsqueda profunda-primera explorando todas las secuencias de movimiento posibles 8n, podando cuando un movimiento sale del tablero.

**Por qué es malo:**

- **Exponential Blow-up** – Incluso para `k = 10`, hay 810 Ω 1,073,741,824 caminos.
- **Trabajamiento residual** – Muchas subproblemas se recomiendan (por ejemplo, alcanzar la misma celda después del mismo número de movimientos).
- **Stack Overflow Risk** – La recursión profunda puede alcanzar el límite de llamada para mayor *k*.

**Mitigation:**
Utilice la memoización para almacenar la probabilidad de llegar a una célula en un paso dado. Eso esencialmente convierte la recursión en DP.

-...

### 2.4 The Ugly – Over-Optimizing with a 3‐D Array or Matrix Power

Si bien puede pre-computar las probabilidades de transición utilizando un array 3-D o tratar el tablero como un gráfico y utilizar la exponentiación de matriz (`Ak`), este nivel de optimización “superior” raramente se necesita en entrevistas:

- **3-D DP** (`dp[step][i][j]`) da una formulación limpia pero aumenta la memoria a `O(k · n2) ` (no es grande para `k = 100`).
- **Matrix Exponentiation** reduce el tiempo de ejecución a `O(log k · (n2)3)`, pero requiere un montón de código caldera y una comprensión profunda del álgebra lineal.
- **Readability Hit** – Los entrevistadores a menudo penalizan soluciones que parecen inteligentes pero son difíciles de seguir.

Usa estos trucos avanzados sólo si estás escribiendo una biblioteca de grado de producción o tocando un seguimiento *teórico*.

-...

### 2.5 SEO Tips – Haz que tu blog se destaque

Silencio SEO Element Silencio Cómo Ayuda a vivir
Silencio------------------
Silencio **Título** – *“La probabilidad de caballero en un tablero de ajedrez: DP, Recursion, " Matrix Power Explained”* Silencio Captura la palabra clave “Probabilidad de la noche” + “DP” TEN
Silencio **Meta Descripción** – 155-character snippet que contiene el ID de la pregunta y términos clave. ← Mejora la velocidad de clic a través de los resultados de búsqueda. Silencio
**Headers** – H1, H2, H3 con palabras clave. Los motores de búsqueda analizan la jerarquía de contenidos. Silencio
Silencio **Code Snippets** – Cada idioma envuelto en `` etiquetas. Silencio Easier para los lectores (y bots) para parse. Silencio
Silencio **Anchor Links** – "#the-good", "#the-bad", "#the-ugly" Silencio Mejora la navegación y SEO. Silencio
Enlaces internos/externos** – Enlace a la página LeetCode, problemas similares (por ejemplo, “Super Jumping Game”). tención significa relevancia. Silencio

-...

### 2.6 Putting It All Together – A Job‐Ready Narrative

Cuando estés en una entrevista, describe el problema como:

1. **Definición del Estado** – “Vamos a rastrear la probabilidad de que el caballero esté en cada celda después de que *t* se mueva. ”
2. **Caso de base** – “Inicialmente, la probabilidad es 1.0 en la celda de inicio y 0 en otros lugares. ”
3. **Transición** – Cada movimiento distribuye la probabilidad actual a los 8 destinos, dividido por 8. ”
4. **Iteración** – “Repetir la transición *k* tiempos. ”
5. Resultado** – “Sum the final grid. ”

Agregue un cheque de cordura rápido (por ejemplo, `n=8, k=1, fila=0, col=0` → probabilidad ♥ 0.125).
Esto demuestra tanto la corrección como la profundidad del pensamiento.

-...

### 2.7 Take‐away for Job Seekers

1. **Mostrar las matemáticas, luego el código** – Explicar la lógica DP antes de sumergirse en la implementación.
2. **Highlight Trade-offs** – Mention why brute force fails and how DP solves it.
3. **Mantenlo limpio** – Use constantes para movimientos, cláusulas de guardia y nombres variables claros.
4. **Talk About Variants** – Mención de que el mismo marco DP puede resolver *Super Knight* (10‐move) o *Hexa‐Knight* (5‐move) variantes.
5. **Link Volver a su cartera** – Si tiene su código en GitHub, incluya un enlace (por ejemplo: https://github.com/your‐repo/knight-probability).

**Resultado:** Los entrevistadores verán que pueden:

- **Interpret** la declaración del problema,
- **Escoge un algoritmo apropiado,
- **Implement** en varios idiomas,
- **Explicar** el razonamiento—exactamente el conjunto de habilidades que están cazando.

-...

## 3. Lista de verificación rápida para su entrevista

TENIDO ANTERIOR ESTADO ANTERIOR Por qué importa
Silencio...
TENIDO TENIDO Entender la tabla como un gráfico TENIDO Ayudas en el modelado estatal
Silencio TENIENDO Maestro de los movimientos de 8 caballeros ANTERIOR de la transición DP
Silencio TENIDO Escribir iterante DP ANTE La solución más entrevistada
Silencio TENIENDO Mention memoization vs brute force ANTE Shows awareness of redundancy TEN
TENIDO ✅ Discuss time/space trade‐offs ← Demonstrates optimization mindset
Silencio ✅ Opcional: Matrix exponentiation ← Bonus para funciones teóricas

¡Feliz codificación y buena suerte en tu próxima entrevista de algoritmos! 🚀