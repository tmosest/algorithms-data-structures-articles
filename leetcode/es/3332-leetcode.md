-...
Título: LeetCode 3332. Puntos máximos Turismo Can Earn -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## ✅ LeetCode 3332 – “Maximum Points Tourist Can Earn”
## ## 🚀 Java Silencio Python Silencio C++ – Todo el código que necesitas
### 📝 Blog post – The Good, The Bad, and The Ugly (SEO-friendly)

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

■ *Se te da*
* " n " - número de ciudades (grafo conectado)
* " k " - número de días (0-indexed)
* `stayScore[i][c]` – puntos ganados si usted ** permanece** en la ciudad `c` el día ` i `
[c][d] – puntos ganados si usted ** viaje** de la ciudad `c` a la ciudad `d` en cualquier día
■
■ ** Objetivo**: iniciar en cualquier ciudad, realizar una acción por día (estar o moverse), y **maximise los puntos totales** después de `k` días.

■ **Constraints**
* `1 ≤ n ≤ 200`
≤ 200
* `0 ≤ travelScore[c][d] ≤ 100`, `1 ≤ stayScore[i] [c] ≤ 100`

-...

### #2# Intuición

El problema es un clásico *time-dependiente DP*:

* El futuro del turista depende sólo de **donde** esté *y* **qué día** es.
* Podemos trabajar **hacia atrás** – después del último día el turista no gana nada, por lo que el DP para el “noche siguiente” es `0` para todas las ciudades.
* Por cada día elegimos **stay** o **move** y elija el mejor resultado.

La transición clave para la ciudad `c` el día `d` es

`` `
stay = stayScore[d][c] + dp[d+1][c]
move = max over all d' of ( travelScore[c][d'] + dp[d+1][d']
dp[d][c] = max(stay, move)
`` `

Debido a que sólo necesitamos el DP para el siguiente día, mantenemos **dos arrays 1-D** (`prev`, `curr`) en lugar de una tabla completa de 2-D → **O(n)** espacio.

-...

#### 3down⃣ Complejidad

* **Tiempo**: `O(k · n2)` – por cada día evaluamos una transición `n`‐`'n`.
* **Espacio**: `O(n)` – dos arrays 1‐D.

Con los límites (`n, k ≤ 200`) esto está bien dentro de los límites de LeetCode (Ω8 millones de iteraciones internas).

-...

#### 4down⃣ Código

##### 📌 Java

``java
importar java.util*;

Clase Solución {
int public int maxScore(int n, int k, int[][] stayScore, int[] travelScore
int[] prev = nuevo int[n]; // dp para el día siguiente (inicialmente 0)
int[] curr = nuevo int[n];

para (un día = k - 1; día 0; día--) {}
para (en la ciudad = 0; ciudad; ciudad ++) {}
// Quédate en la misma ciudad
int stay = stayScore[day][city] + prev[city];

// Muévete a cualquier otra ciudad (incluyendo el alojamiento: travelScore[city][city] == 0)
int move = Integer.MIN_VALUE;
para (int dest = 0; dest {}
int val = viaje Score[city][dest] + prev[dest];
si se mueve (val > movido) = val;
}
curr[city] = Math.max(stay, move);
}
// Swap prev & curr
int[] tmp = prev;
prev = curr;
curr = tmp;
}

// Inicio de la ciudad puede ser cualquiera, así que tome la mejor
respuesta int = 0;
para (int val : prev) {
si (respuesta de valido) respuesta = val;
}
respuesta de retorno;
}
}
`` `

-...

##### 📌 Python 3

``python
Solución de clase:
def maxScore(self, n: int, k: int, stayScore: List[List[int],
Viajes Puntuación: List[List[int]) - título int:
prev = [0] * n # dp para el día siguiente
*

para el día en rango(k - 1, -1, -1):
para la ciudad en rango(n):
estancia = estanciaScore[día][ciudad] + prev[ciudad]
# Max sobre todos los destinos
movimiento = max(travel) Score[city][dest] + prev[dest] for dest in range(n))
curr[city] = max(stay, move)
prev, curr = curr, prev # reuse arrays

volver max(prev)
`` `

-...

##### 📌 C++

``cpp
Clase Solución {
public:
int maxScore(int n, int k, vector stayScore,
vector realizador realizador realizador fielmente limitado viajeScore
vector implicado prev(n, 0), curr(n, 0);

para (un día = k - 1; día 0; --day) {
para (en la ciudad = 0; ciudad, no; + ciudad) {
int stay = stayScore[day][city] + prev[city];
int move = INT_MIN;
para (int dest = 0; dest {}
int val = viaje Score[city][dest] + prev[dest];
movimiento = máx (move, val);
}
curr[city] = max(stay, move);
}
swap(prev, curr); // reutilizar los dos arrays
}
retorno *max_element(prev.begin(), prev.end());
}
};
`` `

-...

#### 5down⃣ Blog Artículo – “El Bien, el Mal y el Ugly”

-...

##### Title
■ **Maximum Puntos Turísticos Can Earn - LeetCode 3332**
■ **Java / Python / C++ DP Solution

### Meta Description (SEO)
■ Aprenda el enfoque óptimo de programación dinámica para LeetCode 3332 “Puntos Máximos Turístico Can Earn”. Soluciones completas en Java, Python y C++. Prepa de entrevista perfecta para trabajos de ingeniería de software.

-...

## Introduction

Cuando el reclutador pregunta, “¿Puede resolver un problema de DP que implica ciudades, puntajes de viaje, y mantener puntuaciones?”, el primer instinto es pensar en una búsqueda de fuerza bruta.
Pero **LeetCode 3332** es un clásico *time‐dependiente de programación dinámica* desafío que prueba tanto su visión matemática como estilo de codificación.

En este post:

1. Rompe el problema.
2. Camina por el truco de DP **bueno.
3. Muéstrame dónde están las trampas.
4. Enfrente a los periféricos **enormes**.
5. Compartir código limpio, listo para la producción en Java, Python y C++.

-...

## 1down El Bien – O(k · n2) DP con Dos Arrays

* **Backward DP**: Al partir del último día y al retroceder, sólo necesitamos los valores del “exto día”.
* **Dos arrays 1-D** (prev`, `curr`): reduce la memoria de `O(k·n)` a `O(n)`.
Este es el truco “clean-up” que mantiene el código legible y rápido.
* **Explicit stay/move transitions**:
``text
estancia = estanciaScore[día][ciudad] + prev[ciudad]
movimiento = max( viajes) Score[city][dest] + prev[dest] )
curr[city] = max(stay, move)
`` `
fórmulas simples, sin bucles ocultos.

Porque `n, k ≤ 200`, el bucle interno 'n2` funciona a la mayoría de 40 000 veces al día – perfectamente bien para LeetCode.

-...

## 2down El malo – Cuando las cosas van mal

Por qué es malo arreglar la vida
Silencio--------------------------------...
Silencio **Storing the whole `dp[k][n]` table** Silencio Usa la memoria `O(k·n)`, innecesaria y puede alcanzar límites para mayores limitaciones. Silencio Mantenga sólo dos filas (prev`, `curr`). Silencio
Silencio **Re-computing `move` desde cero cada vez** Silencio Todavía `O(n2)` por día, pero usted puede pre-compute el max interno si usted tiene muchas consultas (no es necesario aquí). ← Compute `move` dentro del bucle interior como se muestra; simple y rápido. Silencio
Silencio **Using recursion + memoization** tención Riesgo de desbordamiento de pila en Java/C++ y sobrecarga adicional. Silencio Iterative DP (bottom‐up) es más seguro. Silencio

-...

## 3down The Ugly – Edge Cases ' Subtle Bugs

Silenciosamente en la situación actual
Silencio.
TENIDO `travelScore[city] [city] == Es tentador saltar `dest == ciudad`, pero saltar puede ocultar una transición válida si quedarse es el mejor movimiento. Silencio Mantenga el bucle de destino como es; el peso `0` es inofensivo. Silencio
Silencio **Large values near `int` limits** tención Los puntos totales máximos pueden alcanzar `100 * 200 + 100 * 200 = 40 000`. Sigue siendo seguro para `int`. Si las limitaciones cambiaron, use `long`. Silencio
Silencio **Todas las ciudades atadas** Silencio La respuesta es el máximo durante el primer día; olvidando tomar `max(prev)` conduce a un error fuera de-por-uno. Silencio Después del swap final, use `max_element(prev)` (C++), `max(prev)` (Python), o un simple bucle (Java). Silencio

-...

## 3VIEW⃣ Full Solutions – Clean Code in Every Language

Ya hemos publicado los **Java**, **Python**, y **C+** implementaciones anteriores.
Cada versión sigue la misma estructura, utiliza nombres variables claros (prev`, `curr`), e incluye comentarios que explican la transición.

-...

## 6down Takeaway for the Interview

* ** Explique el DP**: Hable sobre la iteración atrasada, la optimización de dos filas y la fórmula de estadía/move.
“Yo compute `dp[d][c]` mirando al día siguiente, así que solo necesito dos arrays. ”
* **Tiempo de mención/espacio**: Mostrar que puedes manejar `n, k = 200` cómodamente.
* **Mostrar código**: Ofrece un snippet limpio y compilable en el idioma de elección.
– Programador de amor conciso código que funciona en milisegundos.

■ ** Resultado**: Demostrará la maestría con DP dependiente del tiempo, la optimización de la memoria y la codificación limpia, todos los rasgos dorados para una entrevista de ingeniería del software.

-...

## 🔗 Más lectura

* [Programación Dinámica – Biblioteca Algorithm de Entrevista] (https://www.interviewbit.com/dynamic-programming/)
* [Space‐Optimised DP – LeetCode Tips](https://leetcode.com/articles/dynamic-programming-tutorial/)
* [C++ `swap()` vs `memcpy()` for DP arrays](https://stackoverflow.com/questions/1137481/why-swap-is-faster-than-copys)

-...

#### 🚀 Final Thought

LeetCode 3332 no es sólo un rompecabezas DP; es una prueba de estilo *coding*.
Si puede:

1. **Explicar la transición** rápidamente.
2. **Write iterative bottom-up code** con dos filas.
3. **Conoce las trampas** (grandes tablas, pila de recursión, etc.).

brillará en cualquier entrevista de codificación y destacará a los gerentes de contratación.

¡Feliz codificación! ▪

-..