-...
Título: LeetCode 1039. Triangulación mínima de puntuación de Polygon -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📌 LeetCode 1039 – Triangulación de puntuación mínima de Polygon
*Medium* Silencioso *Programación Dinámica* Variante*

-...

#### TL;DR
- ** Objetivo** – Dividir un polígono convexo en triángulos `n‐2` tal que la suma de
`valor[i] * valor[j] * valor[k]` para cada triángulo es mínimo.
- **Solución** – Classic **interval DP** (una variación de la multiplicación de Matrix‐Chain).
- **Las complejidades** – `O(n3)` tiempo, `O(n2) espacio.

-...

Problema Recap

Se le da un array `valores` (`3 ≤ n ≤ 50`) donde `valores[i]` es el peso del vértice `i` de un polígono convexo `n` lado.
Una triangulación es un conjunto de triángulos n-2` cuyos vértices son vértices del polígono.
La puntuación de una triangulación = suma del producto de los valores de los tres vértices de cada triángulo.

Devuelve la *mínimo* puntuación posible.

■ *Ejemplo*
■ `valores = [3,7,4,5]` → puntuación mínima = **144** (triangulación: `(3,4,5)` + `(3,4,7)`).

-...

## 🧠 Intuición – “Matrix‐Chain Multiplication” Conoce la geometría

Si usted mira un sub-polígono definido por los vértices `i ... j`, usted puede elegir un vértice `k` (`i < k ' ) como el tercer vértice de un triángulo que utiliza el borde `i-j`.

`` `
i -...
Silencio
Silencio
`` `

La puntuación de este triángulo es `valores[i] * valores[j] * [k]`.
El polígono restante se divide en dos subpolígonos independientes: `i ... k ' y `k ... j ' .
Así, la puntuación mínima para `i ... j` se puede expresar recursivamente:

`` `
dp[i][j] = min over k ( dp[i][k] + dp[k][j] + valores[i]*valores[j]*valores[k]
`` `

Cuando el subpolígono tiene sólo dos vértices (`j == i+1`), ningún triángulo se puede formar → puntuación `0`.

Esta es exactamente la recurrencia utilizada en la Multiplicación Matrix‐Chain, sólo el término “costo” es un producto de tres números en lugar de un coste de multiplicación de matriz.

-...

Diseño de Algoritm

Silencio Silencio Silencio Silencio Silencio
Silencio...
Silencio 1 TENIDO Inicializar un array de 2-D `dp[n][n]` con `-1` (o `∞` para abajo-up). Silencio
Silencio 2 Silencio Recursively compute `dp[i][j]` utilizando la memoización (top-down) o iterate over increasing sub-polygon lengths (bottom‐up). Silencio
TENIDO 3 ANTERIOR Para cada `i < k ' evalúe `score = dp[i][k] + dp[k] + valores[i]*valores[j]*valores[k]. Silencio
Silencio 4 Silencio Guardar el mínimo en `dp[i][j]`. Silencio
El resultado es `dp[0][n-1]`. Silencio

-...

## 📦 Code in Three Languages

■ **Nota:** Todas las implementaciones siguen la misma lógica – la memoización de arriba abajo.
■ El fondo se puede añadir en comentarios si prefiere una versión iterativa.

#### ## 1down⃣ Java

``java
importa java.util. Arrays;

Solución de la clase pública {}
public int minScoreTriangulation(int[] values) {}
int n = values.length;
int[][] dp = nuevo int[n][n];
for (int[] row : dp) Arrays.fill(row, -1);
dfs(valores, 0, n - 1, dp);
}

int privado dfs(int[] values, int i, int j, int[] dp) {
si (i >= j - 1) retorno 0; // menos de 3 vértices
si (dp[i] [j] != -1) retorno dp[i][j];

int best = Integer.MAX_VALUE;
para (int k = i + 1; k)
int cost = values[i] * values[j] * values[k]
+ dfs(valores, i, k, dp)
+ dfs(valores, k, j, dp);
si (costo) mejor = costo;
}
dp[i][j] = best;
devolver mejor;
}
}
`` `

#### 2down⃣ Python

``python
Solución de clase:
def minScoreTriangulation(self, values: list[int] int:
n = len(valores)
memo = [[None] * n for _ in range(n)]

def dfs(i: int, j: int) - título int:
si yo >= j - 1:
retorno 0
si memo[i][j] no es Ninguno:
memo[i][j]

mejor = flotante("inf")
para k en rango(i + 1, j):
Costo =
valores[i] * valores[j] * valores[k]
+ dfs(i, k)
+ dfs(k, j)
)
mejor = min(mejor, costo)

memo[i][j] = best
mejor

dfs(0, n - 1)
`` `

#### 3down⃣ C++

``cpp
Incluido el título
#include >
#include < > >

Clase Solución {
public:
int minScoreTriangulation(std::vector seleccionadoint compartir valores) {}
int n = values.size();
std::vector obtenidosstd::vector realizadoint titulado dp(n, std::vector fielint(n, -1));
dfs(valores, 0, n - 1, dp);
}

privado:
int dfs(const std::vector efectuadoint tendrían éxito v, int i, int j, std::vector seleccionadostd:::vector interpretadoint
si (i >= j - 1) retorno 0; // menos de 3 vértices
si (dp[i] [j] != -1) retorno dp[i][j];

int best = INT_MAX;
para (int k = i + 1; k)
int cost = v[i] * v[j] * v[k]
+ dfs(v, i, k, dp)
+ dfs(v, k, j, dp);
best = std::min(best, cost);
}
dp[i][j] = best;
devolver mejor;
}
};
`` `

-...

## 📈 Complexity Analysis

TEN SON TERRIENTE TENIDO Tiempo ANTERIENTE
Silencio----------------
← Memoización de arriba abajo (todos los 3 códigos) Silencio **O(n3)** – `O(n2)` subproblemas, cada escaneamiento `O(n)` divide. Silencio **O(n2)** – Tabla DP + pila de recursión (`O(n)` profundidad). Silencio
← Subtítulo (no se muestra)

Con `n ≤ 50`, el algoritmo se ajusta fácilmente a los límites (Ω125 000 iteraciones).

-...

## 📜 "El Bien, el Mal, y el Ugly"

TENIDO TERRITORIO DE LA CONVENCIÓN
Silencio...
Silencio **Bueno** Silencio • Recidiva intuitiva – fácil de entender. • Requiere sólo la memoria `O(n2)`. Silencio
Silencio **Bad** Silencio • El tiempo es cúbico; por muy grande `n` se volvería pesado (aunque `n=50` está bien). * valores[j] * valores[k] podría desbordar la entrada de 32 bits en casos extremos (si los valores eran mayores). En los límites del problema oficial (`≤100`) es seguro. Silencio
Silencioso **Ugly** Silencio • La recurrencia DP es *no* obvia a los novicios; pueden pensar la multiplicación de la matriz y confundirse. • La memoización necesita cuidadoso manejo de minúsculas ( < i > j-1 > ). Un tipopo allí conduce a apilar el desbordamiento o respuestas incorrectas. En idiomas con pequeños rangos de int (por ejemplo, JavaScript), debe utilizar BigInt. Silencio

**Equipamiento:** Enfóquese en un caso de base claro, utilice enteros largos donde sea necesario y casos de borde de prueba (`n=3`, todos los valores iguales, arrays ascendentes/descendientes).

-...

## 📈 SEO‐Optimized Blog Title & Meta Descripción

*Título*
■ “Minimum Score Triangulation of Polygon – LeetCode 1039 tención Java, Python, C++ Solutions

**Meta Descripción:**
■ “Aprenda a resolver LeetCode 1039 (Minimum Score Triangulation of Polygon) con la memoización superior. Java completo, Python y código C++, análisis de complejidad y una profunda inmersión en las soluciones buenas, malas y feas de DP. ”

-...

Pensamientos finales

- ¿Por qué DP? Debido a que la triangulación óptima de un subpolígono depende sólo de sus puntos finales, un ajuste perfecto para el intervalo DP.
¿Por qué memoización? La recuperación mantiene el código limpio, y el tamaño del problema (`n ≤ 50`) no garantiza problemas de pila.
- ¿Cuándo cambiar al fondo? Si necesita evitar la recursión para límites de recursión muy profundos o desea pre-alubicar la tabla DP explícitamente.

Con los fragmentos de código y la explicación anterior, usted puede abordar con confianza **LeetCode 1039** en entrevistas, entradas de blog, o concursos de codificación. ¡Feliz codificación