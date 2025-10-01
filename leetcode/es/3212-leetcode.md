-...
Título: LeetCode 3212. Con la misma frecuencia de X y Y -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Problema 3212 – “Submátricos de los contingentes Con la misma frecuencia de X y Y”

* Fuente*: LeetCode 3212
* ** Entrada**: `grid[r][c]` donde cada célula contiene una de `{'X','Y',''.
* ** Objetivo**: Contar **todas las submatrices que **comenzar en la esquina superior izquierda (0, 0)** y cuyo número de células "X" equivale al número de células "Y" **y** contienen al menos una "X".
* **Constraints**: `1 ≤ r, c ≤ 1000`.

La declaración original puede sonar como un problema típico de “cuenta todos los rectángulos”, pero los ejemplos aclaran que sólo nos importan los rectángulos que comienzan en el origen.

-...

## 2. La “buena” – La idea central

El requisito de que cada rectángulo contado comience en `(0,0)` convierte todo el problema en un ejercicio prefijo-sum muy simple.

* **Prefix‐sum of X**
`preX[i+1][j+1]` = number of `X` in the rectangle `(0,0) ... (i,j)`.
* **Prefix‐sum of Y**
`preY[i+1][j+1]` = número de `Y' en el mismo rectángulo.

Si `preX[i+1][j+1] == preY[i+1][j+1]` y el valor es **positivo**, entonces el sub-matrix `(0,0) ... (i,j)` satisface ambas condiciones: igual número de `X` y `Y`, y por lo menos una `X`.

Así que sólo necesitamos un bucle anidado sobre todas las celdas, comprobando esa igualdad.

-...

## 3. El “Bad” – Pitfalls comunes

Silencio Pitfall Silencio Por qué no soporta cómo evitar
Silencio----------------------------
Silencio **Asumiendo que debemos contar todos los rectángulos** Silencio El ejemplo con `X X / X Y` tiene un sub-matrix de 2 columnas `(0,1)-(1,1) que satisfaría la igualdad, pero la respuesta es `0`. Silencio Preste mucha atención a la declaración – sólo se cuentan sub-matrices de origen. Silencio
Silencio **Usando un array 3-D o `long` para el prefijo** TEN memoria innecesaria, acceso más lento. TENIDO Utilizar arrays 2-D `int` (o arrays 1-D por fila) – `int` es suficiente porque los recuentos nunca exceden `10^6`. Silencio
Silencio **Forgetting the “at least one X” requirement** Silencio Contando todos los rectángulos igual-`X/Y` recubrirían los rectángulos que contienen solamente `.` células. 0` antes de aumentar la respuesta. Silencio
TEN **Zero‐based vs. one-based indexing errors** TEN Off‐por-one bugs that produce incorrect counts. tención Construye arrays prefijo con una fila extra/columna de ceros (`size = r+1, c+1`) para evitar cheques. Silencio

-...

## 4. El “Ugly” – Cómo hacerlo rápido” Memoria Amistad

Aunque el bucle doble ingenuo ya es `O(r·c)`, se puede apretar la memoria:

1. **Store sólo la fila actual de sumas prefijo** –
Mantenga dos arrays 1‐D `cntX[c]` y `cntY[c]` y actualice mientras escanea cada fila.
After processing row `i`, `cntX[j]` mantiene el total `X` en la columna `j` de la fila 0 a la fila i.
Un rectángulo que termina en `(i,j)` satisface la condición sif `cntX[j] == cntY[j]` **y ** 'cntX[j] .
Esto utiliza `O(c)` memoria extra en lugar de `O(r·c)`.

2. **Evitar el flujo entero** –
En la versión prefijo 2-D el recuento máximo es `1000·1000 = 106`, muy por debajo `INT_MAX`.
Si usted estaba contando todos los rectángulos (no el problema original de LeetCode), usted necesita un "long".

-...

## 5. Código Final

A continuación encontrará soluciones limpias y de producción para **Java**, **Python**, y **C+**.
Los tres comparten la misma lógica algorítmica – compute prefix sums for `X` y `Y`, a continuación, escanear la red.

-...

### 5.1. Java

``java
// LeetCode 3212 – Submatrices contables Con la misma frecuencia de X y Y
// A partir de (0,0) solamente

importar java.util*;

Clase Solución {
int numberOfSubmatrices(char[][] grid) {
filas int = grid.length;
int cols = grid[0]. longitud;

// sumas de prefijo: preX[i+1][j+1] = #X en rectángulo (0,0)-(i,j)
int[][] preX = nuevo int[rows + 1][collos + 1];
int[][] preY = nuevo int[rows + 1][collos + 1];

para (int i = 0; i) {}
para (int j = 0; j)
preX[i + 1][j + 1] = preX[i][j + 1] + preX[i + 1][j] - preX[i][j]
+ (grid[i][j] == 'X' ? 1 : 0);
preY[i + 1][j + 1] = preY[i][j + 1] + preY[i + 1][j] - preY[i][j]
+ (grid[i][j] == 'Y' ? 1 : 0);
}
}

int ans = 0;
para (int i = 0; i) {}
para (int j = 0; j)
int xCnt = preX[i + 1][j + 1];
int yCnt = preY[i + 1][j + 1];
si
ans++;
}
}
}
devolver los ans;
}
}
`` `

-...

### 5.2. Python 3

``python
# LeetCode 3212 – Conde Submatrices Con la misma frecuencia de X y Y
# Comenzando en (0,0) sólo

def number_of_submatrices(grid: list[list[str]]) int:
filas, cols = len(grid), len(grid[0])

# prefijo sumas para X y Y
pre_x = [0] * (collos + 1) para _ en rango(rows + 1)]
pre_y = [[0] * (collos + 1) para _ en rango(rows + 1)]

para i en rango(rows):
para j in range(cols):
pre_x[i + 1][j + 1] =
pre_x[i][j + 1] + pre_x[i + 1][j] - pre_x[i][j]
+ (1 si la rejilla [i] [j] == 'X' else 0)
)
pre_y[i + 1][j + 1] =
pre_y[i][j + 1] + pre_y[i + 1][j] - pre_y[i][j]
+ (1 si la rejilla [i] [j] == 'Y' else 0)
)

ans = 0
para i en rango(rows):
para j in range(cols):
si pre_x[i + 1][j + 1] ≤ 0 y pre_x[i + 1][j + 1] == pre_y[i + 1][j + 1]:
ans += 1
Retorno
`` `

-...

### 5.3. C++

``cpp
// LeetCode 3212 – Submatrices contables Con la misma frecuencia de X y Y
// A partir de (0,0) solamente

Incluido el título
#include ■string

Clase Solución {
public:
número intOfSubmatrices(cont std::vector obtenidosstd::string ventaja) {
int R = grid.size();
int C = grid[0].size();

// Sumas de prefijo: preX[i+1][j+1] sostiene #X en rectángulo (0,0)-(i,j)
std:::vector obtenidosstd::vector efectuadoint confianza preX(R + 1, std:::vector fielint(C + 1, 0));
std:::vector obtenidosstd::vector efectuadoint confianza preY(R + 1, std:::vector fielint(C + 1, 0));

para (int i = 0; i) {}
para (int j = 0; j)
preX[i + 1][j + 1] =
preX[i][j + 1] + preX[i + 1][j] - preX[i][j]
+ (grid[i][j] == 'X' ? 1 : 0);
preY[i + 1][j + 1] =
preY[i][j + 1] + preY[i + 1][j] - preY[i][j]
+ (grid[i][j] == 'Y' ? 1 : 0);
}
}

int ans = 0;
para (int i = 0; i) {}
para (int j = 0; j)
int xCnt = preX[i + 1][j + 1];
int yCnt = preY[i + 1][j + 1];
si (xCnt ≤ 0 " sensible xCnt == yCnt) ++ans;
}
}
devolver los ans;
}
};
`` `

-...

## 6. Análisis de la complejidad

Silencioso de la aplicación Silenciosos Tiempo Silencioso
Silencio.
Silencio Prefijo 2D (Java, Python, C++) Silencio `O(r · c)` (conducir 106 operaciones para el peor de los casos) enteros – ~ 8 MB para una red de 1000×1000
Silencio 1‐D "row‐by-row" variante (Java & C++) Silencio `O(r · c)` Silencio `O(c)` enteros – ~ 4 kB para una cuadrícula de 1000 columnas

Ambos cumplen con los plazos de LeetCode cómodamente.

-...

## 7. Probando su solución

``python
si __name_ == "__main__":
muestra =
['.', 'X', 'X'],
['X', 'X', 'Y'],
['.', '.', 'Y']
]
print(number_of_submatrices(sample)) # Esperado: 4
`` `

Por el otro ejemplo que demuestra el requisito “origin‐only”:

``python
muestra2 =
['X', 'X'],
['X', 'Y']
]
print(number_of_submatrices(sample2)) Esperado: 0
`` `

-...

## 8. Take-away

*Recuerda*: En LeetCode 3212 los rectángulos que contamos **siempre comienzan en (0, 0)**.
* La solución se reduce a una traversal prefijo-sum bidimensional.
* La cláusula " por lo menos una " se aplica por un solo " Mira.
* Para ahorros de memoria adicionales se puede mantener sólo un recuento de funcionamiento único por columna.

Con los fragmentos de código arriba usted puede abordar con confianza el problema en **Java, Python, o C+** y enviar una solución limpia y lista para la producción a LeetCode. ¡Feliz codificación!