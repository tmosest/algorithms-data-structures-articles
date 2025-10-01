-...
Título: LeetCode 2912. Número de maneras de llegar Destino en la Grid -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📌 LeetCode 2912 – *Número de maneras de llegar Destino en la red*
### El bueno, el malo, y el feo
*Dynamic‐Programming, Grid, Counting, Interview Prep, Java / Python / C+*

-...

### 1. Recaptación de problemas

Se le da una red **1-indexada** del tamaño `n × m` ( `2 ≤ n,m ≤ 109` ), una célula fuente `fuente = [x1, y1]` y una célula de destino `dest = [x2, y2]`.
En un movimiento se puede saltar de la celda `[x1, y1]` a `[x2, y2]` **iff** las dos células comparten el mismo **row** o el mismo **column** (pero no la misma célula).

** Objetivo:** Contar el número de secuencias distintas de movimientos exactamente 'k' que terminan en `dest`.
Devuelve el modulo de respuesta `1 000 000 007`.
`1 ≤ ≤ 105`.

■ **Por qué esto importa para entrevistas* *
■ 1. DP clásico en una red con movimientos *restricted*.
■ 2. Requiere la compresión del estado inteligente – un único conjunto DP de tamaño 4 obras.
■ 3. Demostra el manejo de grandes dimensiones de la red (sólo las fórmulas algebraicas importan).

-...

### 2. El bien

Silencio TENIDO ANTERIOR
Silencio...
Silencio **Tiempo de iluminación** – `O(k)` – 100 000 iteraciones es trivial. Silencio
TEN **O (1) memoria** – sólo se necesitan 4 contadores. Silencio
TEN **Mathematically clean** – matriz de transición se deriva una vez. Silencio
tención **Language‐agnostic** – el mismo DP funciona en Java, Python, C++. Silencio
Silencio **No hay necesidad de la exponencia de la matriz** – porque `k` es en la mayoría de 105. Silencio

-...

### 3. El mal

Silencio Silencio Silencio Silencio
Silencio...
Silencio `n` y `m` pueden ser tan grandes como `109`, por lo que debe utilizar aritmética de 64 bits antes de tomar el modulo. Silencio
Silencio `k = 1` es un caso *especial* – no puedes quedarte en la misma celda. Silencio
Los errores en los recuentos de transición (por ejemplo, `n-1` vs `n‐2`) son fáciles de hacer. Silencio
tención Sobreflujo en la multiplicación intermedia (`long * long` en Java / `int * int` en C++). Silencio

-...

### 4. El Ugly

Silencio 👿 Silencioso Silencioso
Silencio...
Silencio **Mantenerse en la misma celda** Silencio Permitido por la regla de la misma fila / misma columna sólo si usted *move* en algún otro lugar. La transición de “en dest” a “en dest” debe ser “0”. Silencio
Silencio **Counting “out” cells** Silencio `m+n-4` es el número de celdas que comparten **Ni filas** ni columna con `dest`. ¦ Derive cuidadosamente: células totales en dest-row ' dest-col (`m + n - 2`) menos las dos células “especiales” (las que están en la misma fila o columna como dest pero no dest mismo). Silencio
Silencio **Desbordamiento de la multiplicación de modulo** Silencio En Java/C++ `int * int` desborda antes de que podamos aplicar `% MOD`. Silencio
Silencio ** Valores intermedios negativos** tención Sustracciones como `m-2` pueden convertirse en `-1` si `m=2`. Silencio `m ≥ 2`, por lo que `m-2` es siempre no negativo. Silencio
Silencio **Edge case `k = 1`** Silencio El DP inicializado con la fuente informaría incorrectamente `1` cuando `source == dest`. ¦ Handle `k = 1` explícitamente: answer is `1` iff `source` and `dest` compartir una fila o columna **y** no son la misma celda. Silencio

-...

### 5. El Ugly-ish - Qué cuidar mientras que codificación

Silencio 😱 Silencio Lo que puede ir mal
Silencio.
Silencio **La transición incorrecta cuenta** – doble narración o falta de un camino conduce a la respuesta equivocada. Silencio
Silencio **Desbordamiento entero antes del modulo** – especialmente en Java (`int` is 32‐bit). Silencio
Silencio **El estado inicial equivocado** – la clasificación errónea de la fuente como “fuera” cuando está realmente en la misma fila. Silencio
Silencio **El rendimiento de los bucles anidados** – 4×4×k está bien, pero el uso de un bucle anidado ingenuo para cada paso 'k' puede ser más lento en Python si no está escrito eficientemente. Silencio
Silencio **Olvidó manejar `k = 1`** – muchos concursantes salen 1 para `source == dest`. Silencio

-...

## 3. Core Insight – 4 “Cell-Types”

En lugar de pensar en *toda* célula en la cuadrícula, sólo nos importa su *relación* al destino:

Silencio Tipo Silencioso Estado Silencio
Silencio--------------------
**Out** – shares **neither** row nor column with `dest` ¦ *y*
Silencio** – la misma fila que `dest ' , la columna diferente  durable `x = x2` *y*
Silencio **Col** - la misma columna que `dest ' , la otra fila  durable `y = y2` *y*
Silencio **En** – exactamente el destino Silencio `x = x2` *y*

Sólo **cuatro** mostradores son necesarios: 'cntOut, cntRow, cntCol, cntAt`.
Después de cada movimiento todos los contadores se actualizan simultáneamente utilizando una matriz de transición fija.

-...

### 4. Matriz de transición

Dejar `MOD = 1 000 000 007`.
Seamos el estado actual, el siguiente estado.

Silencio De\Para Silencio Sobre Silencio Relájate
Silencio---------------Prince----
Silencioso**
Silencio**
Silencio**
Silencio ** At** Silencioso `0` Silencio `m-1` Silencio `n-1`

¿Por qué estos números? #

* Desde una celda *fuera* de la fila/col de dest puede:
* saltar a cualquier otra célula “fuera” – hay `(m-1)+(n-1)-2 = n+m-4` tales células,
* saltar a la única celda en la misma fila que el dest – **1**,
* saltar a la única celda en la misma columna que el dest – **1**.
* Desde una celda *en la misma fila* como dest:
* saltar a cualquier otra célula en esa fila - 'n-1' células "fuera",
* permanecer en la misma fila pero evitar el dest – `m-2` células,
* saltar directamente a la dest – **1**.
* Los dos casos restantes son simétricos.
* Desde el destino sólo se puede salir – no hay transición “establecer”.

Todos los números son **derived algebraically** de `n` y `m` y son seguros para computar con enteros de 64 bits incluso para `n,m = 109`.

-...

### 5. DP Iteration

`` `
dp[i] – número de maneras de estar en estado i después del número actual de movimientos
siguiente[i] – el mismo pero después de un movimiento adicional
`` `

`` `
para el paso = 1 ... k-1
siguiente[0...3] = 0
para mí en 0.3
para j en 0.3
siguiente[j] = (next[j] + dp[i] * T[i][j]) mod MOD
dp = siguiente
respuesta = dp[At] // número de maneras que terminan en dest después de k movimientos
`` `

*Time* : `O(4·4·k) ♥ O(k) `
*Memory*: `O(4)` counters → `O(1)`

-...

### 6. Manejo especial para `k = 1`

Cuando `k == 1`No podemos quedarnos en la misma celda.
Los únicos caminos válidos son los saltos directos que comparten una fila **o** una columna:

``text
respuesta = 1 si (fuente[0] == dest[0] y fuente[1] != dest[1] // misma fila
o (fuente[0] != dest[0] y fuente[1] == dest[1] // misma columna
0
`` `

-...

## 7. Aplicación de las referencias

A continuación se presentan soluciones totalmente adaptadas para **Java, Python y C++** que siguen la misma lógica DP.

-...

## 7.1 Java 17

``java
Solución de la clase pública {}
static final long MOD = 1_000_000_007L;

// índices estatales
privada estática final int OUT = 0, ROW = 1, COL = 2, AT = 3;

público número DeWays (int n, int m, int k, int[] source, int[] dest) {
------------- 1. Caso especial k == 1o
(k == 1) {
boolean sameRow = source[0] == dest[0] " ventaja[1]!= dest[1];
booleano mismoCol = source[1] == dest[1] " ventaja[0]!= dest[0];
regreso (sameRow tención eterna mismoCol) ? 1 : 0;
}

------------- 2. Matrícula de transición ---
long[][] T = nuevo largo[4][4];

// Desde afuera
T[OUT] [OUT] = n + m - 4;
T[OUT] [ROW] = 1;
T[OUT][COL] = 1;
// T[OUT][AT] se queda 0

// Desde ROW
T[ROW] [OUT] = n - 1;
T[ROW] [ROW] = m - 2;
T[ROW][AT] = 1;

// Desde COL
T[COL] [OUT] = m - 1;
T[COL][COL] = n - 2;
T[COL][AT] = 1;

// De AT (destinación)
T[AT] [ROW] = m - 1;
T[AT][COL] = n - 1;
// T[AT][AT] se queda 0

------------- 3. vector inicial del DP ---
long[] dp = new long[4];
si (fuente[0] == dest[0] " víctima fuente[1] == dest[1]) {
dp[AT] = 1;
} si (fuente [0] == dest[0] {
dp [ROW] = 1;
} si (fuente[1] == dest[1]) {
dp[COL] = 1;
. ♫ ... {
dp [OUT] = 1;
}

------------- 4. Iteraciones del DP -----
para (en un paso = 1; paso)
largo[] siguiente = nuevo largo[4];
para (int i = 0; i)
para (int j = 0; j) {}
si (T[i] [j] == 0) continuar; // saltar cero entradas
siguiente[j] = (next[j] + dp[i] * T[i][j]) % MOD;
}
}
dp = siguiente;
}

------------- 5. Resultado */
dp[AT];
}
}
`` `

-...

## 7.2 Python 3.10

``python
Solución de clase:
MOD = 10**9 + 7
Fuera, ROW, COL, AT = 0, 1, 2, 3

def number DeWays(self, n: int, m: int, k: int,
fuente: List[int], dest: List[int]) - int:
# -------- k == 1 manipulación especial --------
si k == 1:
misma_row = source[0] == dest[0] y source[1] != dest[1]
mismo_col = fuente[1] == dest[1] y fuente[0]!= dest[0]
int(same_row o same_col)

# ---------- Matriz de transición --------
T = [[0] * 4 for _ in range(4)]

# From OUT
T[self.OUT] [self.OUT] = n + m - 4
T[self.OUT] [self.ROW] = 1
T[self.OUT] [self.COL] = 1

# From ROW
T[self.ROW][self. OUT] = n - 1
T[self.ROW] [self.ROW] = m - 2
T[self.ROW] [self.AT] = 1

# From COL
T[self.COL][self. #### = m - 1
T[self.COL] [self.COL] = n - 2
T[self.COL] [self.AT] = 1

De AT
T[self.AT] [self.ROW] = m - 1
T[self.AT] [self.COL] = n - 1

# ---------- Primer vector...
* 4
si fuente[0] == dest[0] y fuente[1] == dest[1]:
dp[self. AT] = 1
elif source[0] == dest[0]:
dp[self. ROW] = 1
elif source[1] == dest[1]:
dp[self. COL] = 1
más:
dp[self. EXTRATO = 1

# ---------- Las iteraciones del DP----------
para _ en rango(1, k): # ya manejamos el paso 1
nxt = [0] * 4
para i en rango(4):
si dp[i] == 0:
continuar
para j en rango(4):
si T[i] [j] == 0:
continuar
nxt[j] = (nxt[j] + dp[i] * T[i][j]) % self. MOD
dp = nxt

int(dp[self.AT])
`` `

-...

## 7.3 C++20

``cpp
Clase Solución {
public:
static constexpr long MOD = 1'000'007LL;
// índices estatales
static constexpr int OUT = 0, ROW = 1, COL = 2, AT = 3;

número int OfWays(int n, int m, int k, vector implicaint limitada source, vector armonizado convenientemente) {
/* -------- k == 1 caso especial...
(k == 1) {
bool sameRow = source[0] == dest[0] " ventaja[1]!= dest[1];
bool sameCol = source[1] == dest[1] < fuente[0]!= dest[0];
regreso (sameRow tención eterna mismoCol) ? 1 : 0;
}

--------- matriz de transición-------- */
T[4][4] = {}; // cero-inicializado
T[OUT] [OUT] = (long long)n + m - 4;
T[OUT] [ROW] = 1;
T[OUT][COL] = 1;

T[ROW] [OUT] = n - 1;
T[ROW] [ROW] = (long long)m - 2;
T[ROW][AT] = 1;

T[COL] [OUT] = m - 1;
T[COL][COL] = n - 2;
T[COL][AT] = 1;

T[AT] [ROW] = (long long)m - 1;
T[AT][COL] = (long long)n - 1;

/* -------------- inicial DP vector----------
dp[4] = {0,0,0};
si (fuente[0] == dest[0] " fuente del paciente[1] == dest[1]) dp[AT] = 1;
si (fuente[0] == dest[0]) dp [ROW] = 1;
si (fuente[1] == dest[1]) dp[COL] = 1;
dp [OUT] = 1;

--------- Las iteraciones del DP-------- */
para (en un paso = 1; paso) {}
long nxt[4] = {0,0,0};
para (int i = 0; i) {}
si (dp[i] == 0) continuar;
para (int j = 0; j)
si (T[i] [j] == 0) continuar;
nxt[j] = (nxt[j] + dp[i] * T[i][j]) % MOD;
}
}
memcpy(dp, nxt, sizeof(dp));
}
(int)dp[AT];
}
};
`` `

-...

## 8. Pensamientos finales

* La solución se reduce a **cuatro contadores** y una matriz de transición **fixed**.
* Todos los recuentos del camino se expresan como simples funciones algebraicas de `n` y `m`.
* Manejo cuidadoso de k = 1 y promoción a 64 bits garantiza la corrección.

Con este entendimiento, usted puede implementar la solución en cualquier idioma sin caer en los obstáculos típicos. ¡Feliz codificación!

-...

### 9. Lectura adicional (opcional)

* ** Programación Dinámica en Gráficos** – por qué la reducción del estado funciona.
* **Conteo algebraico de caminos** – ver interpretaciones combinatorias de los conteos de transición.
* ** Aritmética Moderna en 64 bits** – trampas en idiomas como Java/C++/Python.

-...

*Happy Problem Solving! *