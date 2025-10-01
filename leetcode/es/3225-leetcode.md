-...
Título: LeetCode 3225. Máximo puntaje de las operaciones de la red -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

# **Apoyo Máximo de Operaciones de Grid (LeetCode 3225) - Un profundo-Dive**

■ *Hard – 5 – 100 × 100 rejilla – DP + recursión – O(n3) tiempo, O(n3) espacio*

■ **Keywords** – LeetCode, Programación Dinámica, Java, Python, C++, Entrevista, Operaciones Grid, Entrevista de Coding, Resolución de Problemas, Entrevista de Trabajo, Análisis de Algoritmo

-...

## 1. Declaración de problemas

Se le da una matriz `n × n` `grid`.
Todas las células son inicialmente **blancas**.

*Operación*
Elija cualquier celda `(i , j)` y pintar **negro** cada celda en la columna `j` de la fila `0` hasta la fila `i` (inclusive).

**Score**
Para cada célula *blanca* que tiene una célula negra **horizontalmente adyacente** (a su izquierda o derecha) ganas `grid[i][j]`.
La puntuación de toda la red es la suma de todos los valores obtenidos.

■ ** Objetivo** – Realizar cualquier número de operaciones para maximizar la puntuación.

-...

## 2. ¿Por qué es difícil?

Silencio Lo que hace que sea difícil
Silencio...
Silencio **Large value range** Silencio `grid[i][j]` puede ser hasta `109`, por lo que la respuesta no encaja en un entero de 32 bits. Silencio
Silencio **Estado complejo** Silencio Cada columna puede ser parcialmente pintada; el impacto futuro depende de *cuántas filas* ya estaban pintadas en columnas anteriores. Silencio
Silencio ** Interdependencia entre columnas** Silencio Pintura de una celda en la columna `j` puede afectar la posibilidad de pintar células en la columna `j+1` (porque una célula negra bloquea una blanca). Silencio
Silencio **Exponential naïve search** Silencio Cada columna tiene 'n+1` posibilidades (pintura 0 ... n filas). La fuerza bruta sería `O(n+1)^n)` – imposible para `n = 100`. Silencio

La solución aceptada utiliza la programación **dinámica** con un estado tridimensional que captura exactamente la información necesaria para subproblemas óptimos.

-...

## 3. Intuición " Diseño del Estado "

Veamos las columnas de **izquierda a derecha**.

Cuando estamos en la columna 'c', ya sabemos:

1. **`último1`** - el número de filas pintadas **por columna `c-1`**.
Esto nos dice qué filas ya son negras en el *start* de la columna `c`.

2. ** `último2`** - el número de filas pintadas ** por columna `c-2`**.
Esto importa porque una célula negra en la columna 'c-2' puede bloquear una célula blanca en la columna 'c-1', que a su vez puede bloquear una célula blanca en la columna 'c`.

Con estos dos números podemos calcular la contribución de la columna 'c' para cualquier elección que hagamos en esta columna:

* **Caso I – No pintar nada en la columna `c`**
Sólo guardamos las filas que ya eran negras de `last2`.

* **Caso II - Pintar algunas filas en la columna 'c' y **block** c+1**
Si pintamos filas a partir de `último1` a `i`, debemos establecer `último1` para la siguiente columna a `i+1` y `last2` a `0` (porque las filas de `último1` serán negras y ya no estarán disponibles para la columna 'c+1`).

* **Caso III – Pintar filas en la columna `c` pero **no bloquee la columna** c+1**
Guardamos las filas de 'último2' y pintamos todas las filas de 'último2` hacia abajo.
Para la siguiente columna, `último1` se convierte en `0` y `último2` se convierte en el nuevo recuento pintado.

This leads to the DP recurrence:

`` `
dp[col][last1][last2] = puntuación máxima desde el col de columna
`` `

La transición enumera todas las opciones posibles para la columna actual (Caso I, II, III) y recurre a la siguiente columna, manteniendo la pista del nuevo `último1 ' y `último2 ' .

-...

## 4. Complejidad

****Time** – `O(n3)`
Por cada columna ( " n " ) nos dirigimos sobre " last1 " y " last2 " ( " ≤ n " ). En el interior volvemos a buclear sobre filas (`≤ n`).
* **Espacio** – `O(n3)` para la memoización (puede reducirse a `O(n2)` si usted guarda sólo dos capas, pero la simple tabla 3dimensional es más fácil de entender).
* ** Tamaño de la respuesta** - Usar enteros de 64 bits (`long`/`int64_t`/`int` en Python).

-...

## 5. Implementaciones de referencia

A continuación se presentan implementaciones limpias y bien agregadas en **Java**, **Python**, y **C+**.

-...

## 5.1 Java (Recursive DP with Memoization)

``java
importar java.util*;

Solución de la clase pública {}
/ Tabla de memoización
privada Long[][][] memo;
int privado[][] grid;
privada int n;

máximo público largo Score(int[][] grid) {
esto. rejilla = rejilla;
esto.n = grid.length;
// +1 porque el último1 / último2 puede ser igual a n (pintar todas las filas)
memo = nuevo largo[n + 1][n + 1][n + 1];
dfs(0, 0, 0);
}

/** @param col actual columna (0-basada)
* @param última1 filas pintadas por columna col‐1
* @param último2 filas pintadas por columna col‐2
*/
dfs privados largos(int col, int last1, int last2) {
si (col == n) retorno 0; // terminado todas las columnas
si (memo[col][last1][last2] != null)
memo [col][last1][last2];

long best = 0;

/* ---- Caso I : no pintar esta columna ---- */
long fromLast2 = 0;
para (int r = 0; r ' seg último2; r++) de Last2 += grid[r][col];
mejor = Math.max(mejor,
de last2 + dfs(col + 1, 0, last1));

/* ---- Caso II : pintar algunas filas, bloquear la siguiente columna ---- */
larga suma = 0;
si (col + 1 0) {
para (int r = last1; r ' n; r++) {}
sum += grid[r][col];
mejor = Math.max(mejor,
suma + dfs(col + 1, r + 1, 0));
}
}

/* ---- Caso III : filas de pintura pero no bloquee la siguiente columna ---- */
tiempo largo = 0;
para (int r = 0; r) {}
[r] [col];
mejor = Math.max(mejor,
temp + dfs(col + 1, 0, r + 1));
}

memo[col][last1][last2] = best;
devolver mejor;
}

public static void main(String[] args) {
Solución s = nueva solución ();
int[][] g = {
{0,0,0,0},
{0,0,3,0,0},
{0,1,0,0,0},
{5,0,0,3,0},
{0,0,0,0,2}
};
System.out.println(s.maximumScore(g)); // 11
}
}
`` `

-...

## 5.2 Python (Recursion + `functools.lru_cache`)

``python
desde functools import lru_cache
de la importación Lista

Solución de clase:
def máximo Score(self, grid: List[List[int]]) - int:
n = len(grid)

@lru_cache(maxsize=None)
def dfs(col: int, last1: int, last2: int) - título int:
si col == n:
retorno 0

# --- Caso I: saltar esta columna
desde_last2 = sum(grid[r][col] for r in range(last2))
mejor = from_last2 + dfs(col + 1, 0, last1)

# --- Caso II: filas de pintura, bloque siguiente columna
sum_ = 0
si colo + 1 se hizo n:
para r en rango(last1, n):
sum_ += grid[r][col]
mejor = max(best, sum_ + dfs(col + 1, r + 1, 0)

# --- Caso III: filas de pintura, pero mantenga la siguiente columna abierta
temp = 0
para r en rango(n):
si R se hizo el último2:
temp -= grid[r][col]
mejor = max(best, temp + dfs(col + 1, 0, r + 1))

mejor

devolver dfs(0, 0, 0)

# Prueba de muestra
si __name_ == "__main__":
s = Solución()
g)
[0,0,0,0],
[0,0,3,0,0],
[0,1,0,0,0],
[5,0,0,3,0],
[0,0,0,2]
]
print(s.maximumScore(g)) # 11
`` `

-...

## 5.3 C++ (Top‐Down DP with Memoization)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
largo plazo máximo Puntaje(vector seleccionador) {
n = grid.size();
este- título = &grid;
memo.assign(n + 1, vector identificadovector realizador realizado largamente largo título(n + 1, vector obtenidoslong tiempo(n + 1, LLONG_MIN));
dfs(0, 0, 0);
}

privado:
int n;
vector realizador:
vectorial seleccionador seleccionador realizador memo;

largos dfs(int col, int last1, int last2) {
si (col == n) retorno 0;
si (memo[col][last1][last2] != LLONG_MIN) return memo[col][last1][last2];

long long best = 0;

// Caso I: columna de salto
largo tiempo desdeLast2 = 0;
para (int r = 0; r ' se hizo el último2; ++r) de Last2 += (*grid)[r][col];
mejor = max(best, fromLast2 + dfs(col + 1, 0, last1));

// Caso II: filas de pintura, bloque siguiente columna
larga suma = 0;
si (col + 1 0) {
para (int r = last1; r > n; ++r) {}
suma += (*grid)[r][col];
mejor = max(best, sum + dfs(col + 1, r + 1, 0));
}
}

// Caso III: filas de pintura, mantener la siguiente columna abierta
tiempo largo = 0;
para (int r = 0; r) {}
[r] [col];
mejor = max(best, temp + dfs(col + 1, 0, r + 1));
}

memo[col][last1][last2] = best;
devolver mejor;
}
};

// Uso del ejemplo
int main() {}
Solución s;
vector de vectores obtenidos {}
{0,0,0,0},
{0,0,3,0,0},
{0,1,0,0,0},
{5,0,0,3,0},
{0,0,0,0,2}
};
cout se realizó s.maximumScore(g)
}
`` `

-...

## 6. Soluciones “bien” vs “Bad” – Lista de verificación

¿Por qué vivir?
Silencio...
Silencio **Respuesta de 64 bits?** Silencio TENIENDO TENIDO `long` en Java, `long' en C++, `int` en Python. Silencio
Silencio ** ¿Se encuentra dentro del tiempo en n=100?** Silencio TENIENDO TENIDO `O(n3)` pasa en 2 s para jueces típicos. Silencio
Silencio **Memoiza correctamente?** Silencio TENIENDO TENIDO mesa 3-dimensional o `lru_cache`. Silencio
Silencio **Evite el desbordamiento de enteros?** Silencio TENIENDO TENIDO 64 bits tipos, `LLONG_MIN` sentinel. Silencio
TENIDO **Siguiente la recurrencia DP limpiamente?** TENIENDO ANTERIOR Caso I/II/III. Silencio
Silencio **¿El código está bien recomendado?** Silencio TENIENDO TENIDO Los comentarios en línea ayudan a la legibilidad. Silencio

Si alguno de los anteriores falta, la solución puede ser **bad** (por ejemplo, utilizando `int` en Java, o la memoización perdida que conduce a tiempo exponencial).

-...

## 7. Testing " Edge Cases

Silencio Rejilla Tamaño Silencio Caso Edge Silencio esperada Comportamiento
Silencio--------------------------- La vida--
Silencio `1x1` TENIDO Minimal grid ANTE Respuesta igual a la rejilla[0][0]
TENIDO `100x100` TENIDO Todos los ceros ANTERIENTE Resultado `0`
Silencio `100x100` Silencio Todos los 1s Silenciosos Resultado igual a la suma total de todas las celdas
Silencio `n = 100` con valores aleatorios ← Rendimiento Silencio Debe terminar en ~1‐2 segundos en Java/ C++ Silencio
tención `n = 50` pero valores cercanos a `109` tención Sobre el riesgo Silencio 64‐bit debe ser utilizado

Prueba estos con pequeños scripts para garantizar la corrección antes de enviar.

-...

## 8. ¿Qué hace una *buena* solución?

Una solución **buena** DP para este problema:

1. **Encapsular el estado exacto** necesario para subproblemas óptimos (aquí: `col, last1, last2`).
2. **Enumerar todas las opciones válidas** (Caso I/II/III) sin duplicación.
3. **Memoizar** resultados para evitar la recomputación.
4. **Mantener números grandes** utilizando enteros de 64 bits.
5. **Manténgase dentro de los límites del tiempo/espacio** (`O(n3)`).
6. **Sea fácil de leer** – use nombres y comentarios variables descriptivos.

-...

## 9. Lecciones prácticas

* **3-dimensional DP** puede parecer pesado, pero es a menudo la forma *derecha* de codificar dependencias que abarcan más de un paso (aquí, `último1 ' y `último2 ' ).
* **Memoización** se puede aplicar en muchos idiomas: recursión + `lru_cache` en Python, `@lru_cache` o tablas manuales en Java/C++.
* ** Análisis de la complejidad**: Siempre confirma que la recurrencia DP reduce el tamaño del problema.
* **Code clarity**: Una implementación limpia (como se muestra anteriormente) es más valiosa en entrevistas y en sistemas de producción que una versión altamente optimizada pero opaca.

-...

## 10. Palabras finales

La programación dinámica es una técnica *poderosa* que convierte una explosión combinatoria intrínseca en una solución polinomio-tiempo.
Al estudiar cuidadosamente la interacción entre las columnas en este problema, hemos creado un DP tridimensional que captura exactamente la información necesaria para decisiones óptimas.

Si te preparas para entrevistas técnicas, dominar este tipo de diseño de estado te ayudará a abordar muchos problemas de “painting grave” o “blocking” que aparecen en concursos o sistemas del mundo real.

¡Feliz codificación! 🚀

-...

**Búsqueda de etiquetas**: #Java #Python #C++ #DynamicProgramming #LeetCode #InterviewQuestion #DPStateDesign #64bitInteger #Memoization
-...
*Posted on 2024‐03‐18 by “CodingMentor”*
-...
*Si te gustó este post, considera suscribirte para tutoriales más limpios de DP y algoritmo. *
-...
*No dude en abrir problemas si detecta errores o desea optimizaciones. *