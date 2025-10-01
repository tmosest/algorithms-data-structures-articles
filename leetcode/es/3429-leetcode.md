-...
Título: LeetCode 3429. Paint House IV -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 3429. **Paint House IV** – Solución completa en **Java, Python, C++** + SEO‐Optimized Blog

-...

#### TL;DR
- El problema es un DP de 2 dimensiones en pares de casas que están equidistas desde los extremos.
- Estado: `dp[i][prevL][prevR]` – costo mínimo para los primeros `i` pares, donde `prevL` es el color de la casa `i‐1` en el lado izquierdo, y `prevR` es el color de la casa `n-i` en el lado derecho.
- Recurrencia: elegir colores 'cL' y 'cR' para el par actual que respeta
* `cL != prevL` (no mismo adyacente a la izquierda)
* `cR != prevR` (no mismo adyacente a la derecha)
* `cL!= cR ' (las casas equidistas deben diferir)
Minimise `cost[i][cL] + cost[n‐1‐i][cR] + dp[i+1][cL][cR]`.
- Complejidad: **O(n · 144)** (Ω O(n)), memoria **O(n · 16)** → encaja fácilmente para `n ≤ 1e5`.

A continuación encontrará la implementación completa en los tres idiomas solicitados.

-...

## 1. Solución Java

``java
importar java.util*;

Solución de la clase pública {}
privada estática final larga INF = Long.MAX_VALUE / 4; // evitar desbordamiento

public long minCost(int n, int[][] cost) {
int half = n / 2;
// dp[i][prevL][prevR] – índices de color prev: 0,1,2 o 3 (ninguno)
long[][][] dp = new long[half + 1][4][4];
para (int i = 0; i <= half; i++) {
para (int a = 0; a) {}
Arrays.fill(dp[i][a], INF);
}
}
dp[half][3] = 0; // caso base: no más pares para pintar

por (int i = half - 1; i >= 0; i--) {
int left Idx = i;
Intento derecho Idx = n - 1 - i;
para (int prevL = 0; prevL = 4; prevL++) {}
para (int prevR = 0; prevR) {}
long best = INF;
para (int cL = 0; cL = 3; cL++) {}
si (cL == prevL) continúan; // izquierda adyacente
para (int cR = 0; cR = 3; cR++) {}
si (cR == prevR) continúan; // derecho adyacente
si (cL == cR) continúan; // equidistant
long cand = cost[leftIdx][cL] + cost[rightIdx][cR] + dp[i + 1][cL][cR];
si (candúa) mejor = cand;
}
}
dp[i][prevL] [prevR] = best;
}
}
}
dp[0][3];
}

// Para pruebas rápidas
public static void main(String[] args) {
Solución sol = nueva solución ();
int[][] cost1 = {3,5,7},{6,2,9},{4,8,1},{7,3,5}};
System.out.println(sol.minCost(4, cost1)); // 9

int[][] cost2 = {2,4,6},{5,3,8},{7,1,9},{4,6,2},{3,5,7},{8,2,4}};
System.out.println(sol.minCost(6, costo2)); // 18
}
}
`` `

-...

## 2. Solución de pitón

``python
importadores
de la importación Lista

INF = 10**18

Solución de clase:
def minCost(self, n: int, cost: List[List[int]) - título int:
media = n // 2
# dp[i][prevL][prevR]
dp = [[INF] * 4 for _ in range(4)] for _ in range(half + 1)]
dp[half][3]

para i en rango(half - 1, -1, -1):
izquierda, derecha = i, n - 1 - i
para prevL en rango(4):
para prevR en rango(4):
best = INF
para cL en rango(3):
si cL == prevL: # lo mismo que el vecino izquierdo
continuar
cR en rango(3):
si cR == prevR: # lo mismo que el vecino derecho
continuar
si cL == cR: # las casas equidistas deben diferir
continuar
cand = cost[left][cL] + costo[right][cR] + dp[i + 1][cL][cR]
si se puede hacer mejor:
mejor = cand
dp[i][prevL] [prevR] = best
retorno dp[0][3]


si __name_ == "__main__":
sol = Solución()
print(sol.minCost(4, [3,5,7],[6,2,9],[4,8,1],[7,3,5]]) # 9
print(sol.minCost(6, [2,4,6],[5,3,8],[7,1,9],[4,6,2],[3,5,7],[8,2,4]])
`` `

-...

## 3. Solución C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
largo tiempo minCost(int n, vector asignadovector identificadoint
const long long INF = 4e18; // safe upper bound
int half = n / 2;
// dp[i][prevL][prevR] – índices de color prev: 0,1,2 o 3 (ninguno)
vectorial seleccionador seleccionador realizador dp(half + 1,
vector se llevó a cabo larga larga experiencia(4, vector llevado a cabo largo tiempo(4, INF));
dp[half][3] = 0; //

para (int i = half - 1; i >= 0; --i) {
int left = i;
int right = n - 1 - i;
para (int prevL = 0; prevL)
para (int prevR = 0; prevR)
long long best = INF;
para (int cL = 0; cL = 3; ++cL) {
si (cL == prevL) continúan; // igual que el vecino izquierdo
para (int cR = 0; cR = 3; ++cR) {
si (cR == prevR) continúan; // igual que el vecino derecho
si (cL == cR) continúan; // las casas equidistas deben diferir
c) + costo [derecho][cL] + costo[derecho][cR] + dp[i + 1][cL][cR];
mejor = min(best, cand);
}
}
dp[i][prevL] [prevR] = best;
}
}
}
dp[0][3];
}
};
`` `

-...

## 4. Artículo del Blog – “Paint House IV: El Bien, el Mal y el Ugly”

■ **Título:** Casa de pintura IV - Guía completa de la solución óptima del DP
■ **Meta Descripción:** El problema Paint House IV del Maestro LeetCode. Aprende “bueno, malo y feo” de las soluciones DP, con código en Java, Python y C++.

-...

#### Introduction

Si alguna vez has luchado con **La Casa de Pintura IV de LeetCode**, no estás solo. El desafío se siente engañosamente simple —casas pintadas con tres colores— pero las limitaciones (ninguna misma casa adyacente * y* ningún mismo color para pares equidistas) arrojan un giro que muchas soluciones de memoización de arriba abajo pierden.

En este artículo, diseccionaremos el problema desde tres ángulos:

1. **El Bien** – Qué hacer desde el principio.
2. **The Bad** – Problemas comunes que conducen a los timeouts o respuestas incorrectas.
3. **El Ugly** – Manejo avanzado del borde que a veces viaja hasta los coders experimentados.

Terminaremos con implementaciones pulidas en **Java, Python, y C++** que puedes caer directamente en tu prepa de entrevista.

-...

### The Problem (Quick Recap)

Dado un número de casas y una matriz de costes de 3 colores `cost[n][3]`, pinta cada casa de tal manera que:

1. **No dos casas adyacentes comparten el mismo color. #
2. **No hay dos casas equidistas de los extremos que comparten el mismo color. #

Devuelve el coste total de pintura **mínimo**.

-...

## The Good: A 2-Dimensional DP on Pairs

##### ¿Por qué Parejas?

Debido a que el tercero limita las casas que se sientan *simétricamente* alrededor del array. En lugar de tratar cada casa de forma independiente, tratamos **pairs**: casa `i` y casa `n‐1-i`. Pintar un par a la vez garantiza que la restricción equidistante se cumpla **una vez**.

#### State Design

`dp[i][prevL][prevR] `

- " i " - número de pares ya procesados (desde el interior más externo).
- `prevL` - el color utilizado para el vecino izquierdo de la casa izquierda actual (`i‐1`).
- `prevR` - el color utilizado para el vecino derecho de la casa derecha actual (`n-i`).
- Añadimos un índice de muñeco `3` para representar “no color anterior” (utilizado en la primera llamada).

Con 3 colores reales + 1 muñeco, sólo tenemos **4 × 4 = 16** posibles combinaciones `prevL, prevR` por par. Eso mantiene la mesa del DP minúscula.

#### Transition

Para cada par `(i, n‐1-i)` elegir colores `cL` y `cR` tal que

`` `
cL != prevL // vecino izquierdo
cR != prevR // vecino derecho
cL != cR // casas equidistas difieren
`` `

El costo añadido es `cost[i][cL] + costo[n‐1‐i][cR]`.
Agregue el costo de la solución óptima para el par *next*: `dp[i+1][cL][cR]`.

``text
dp[i][prevL] [prevR] = min {
cost[i][cL] + costo[n‐1‐i][cR] + dp[i+1][cL][cR]
para todos los cL válidos, cR
}
`` `

#### Complexity

- Lazos internos iteran más de 3 × 3 opciones de color para cada estado.
- Con 16 estados por par → **144 operaciones por par**.
- Para 'n = 100.000' esto es < 15 millones de operaciones primitivas → bien bajo el límite de 1 segundo.

-...

## The Bad: Why Naïve DP Fails

### 1. Ignorar el Estrecho Equidista

Muchas soluciones de primera vez solo comprueban casas adyacentes.
Felizmente pintarán 'i' y 'n‐1' el mismo color, causando un **incorrecto límite inferior**.

### 2. Usando sólo un DP 1-Dimensional

Tratar el problema como una clásica “casas pintadas en una línea” ignora la *simetría*.
The resulting DP would be **O(n3)** and impossible for the given constraints.

### 3. Recursión con Memoización 1‐D

Un memo de arriba abajo que almacena sólo la casa actual y el último color de ese lado olvida el último color del lado derecho*, dando lugar a repetidos estados ilegales.

-...

## The Ugly: Edge Cases that Trip You Up

← Caso Edge Silencioso Lo que puede ir mal
Silencio----------------------
* Índice holandés* (`3`) Silencio Olvídate de inicializar `dp[half][3] = 0`. Silencio Añadir el caso base explícitamente. Silencio
Silencio **Overflow** Silencio Summing two `int` costs plus `INF` may overflow `int`. Silencio Use `long ' / `long` every and a safe `INF`. Silencio
Silencio **Array bounds** Silencio Usando `n-1-i` cuando `i` llegue al centro para extrañar `n` (pero el problema garantiza incluso). ANTERIOR Asegurar " n % 2 == 0` antes de proceder, o simplemente confiar en la entrada. Silencio
tención **Tiempo límite** tención Anidado 3×3 bucles dentro de 4×4 estados → 144 operaciones por par. Para 100k casas son 14,4 millones de operaciones. Algunos idiomas de alto nivel pueden alcanzar el límite de 2 segundos. Usar DP de fondo iterativo, evitar la sobrecarga de recidiva, y precomputar los índices de costes. Silencio

-...

## Final Thoughts

La belleza de Paint House IV se encuentra en el **pair-wise DP**: una vez que te das cuenta de que la tercera restricción es una condición de “mirror”, el problema se desploma a un pequeño espacio estatal.

Para los entrevistadores, la clave es el razonamiento **state‐transition**:

1. “¿Qué información anterior necesito?” → colores de los dos vecinos adyacentes.
2. “¿Qué limitaciones adicionales existen?” → las casas equidistas deben diferir.
3. ¿Cuántos estados? → 4 × 4 por par.

Si usted puede explicar este razonamiento, usted clavará el problema en cualquier entrevista.

-...

### Listo para Código?

Copie la solución de su idioma favorito de la sección “Solución” de arriba, ejecute contra los casos de muestra, y confíe en que ha clavado Paint House IV!

¡Feliz codificación! 🚀

-...

**Tags:** `LeetCode`, `DP`, `Dynamic Programming`, `Java`, `Python`, `C++`, `Algorithm`, `Interview Preparation `
**Author: ** *Su nombre – Algorithm Enthusiast & Software Engineer*
**Fecha:**

-...

*Para explicaciones más detalladas, no dude en ping me en Twitter @YourHandle o suelte un comentario en el artículo. *