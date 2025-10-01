-...
Título: LeetCode 3418. Cantidad máxima de dinero Robot puede Ganar -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📌 Problema Recap – LeetCode 3418: *Maximum Cantidad de dinero Robot Can Earn*

# Objetivo #
Un robot comienza en `(0,0)` y sólo se mueve **right** o **down** para alcanzar `(m‐1, n-1)` in an `m × n` grid `coins`.
* `coins[i][j] ≥ 0` → the robot **gains** that many coins.
* `coins[i][j] [j] 0 ` → a robber steals `prehensicoins[i][j].
El robot puede neutralizar a los ladrones en ** en la mayoría de las dos células** en su camino, evitando esos robos.

Devuelve las monedas totales **maximum** que el robot puede recoger (el total puede ser negativo).

■ **Constraints**
■ `1 ≤ m, n ≤ 500`
[j] ≤ 1000

-...

## 🔍 Why this problem is a “Must‐Know” for job interviews

* **DP on 2‐D grid** – un patrón clásico de entrevista.
* **Recurso reducido (2 neutralizaciones)** – muestra cómo agregar una dimensión adicional al DP.
* **Large input** (`500×500`) – prueba tu capacidad de gestionar el tiempo y la memoria.

Si usted puede explicar esta solución claramente en una entrevista, usted mostrará la maestría de programación dinámica y solución de problemas - un gran plus para cualquier papel de ingeniería de software.

-...

##  Settlement Solution Overview

1. **Estado**
`dp[i][j][k]` – monedas máximas que se pueden recoger cuando el robot está en la celda `(i,j)` habiendo utilizado exactamente `k` neutralizaciones (`k = 0, 1, 2`).

2. **Transición**
From `(i-1,j)` or `(i,j-1)` podemos
* **Move sin usar** un neutralizador:
`dp[i][j][k] = max(dp[i][j][k], dp[prev][k] + coins[i][j]
* **Move and use** one neutraliser on the current cell (if `k ≤ 0`):
`dp[i][j][k] = max(dp[i][j][k], dp[prev][k-1] + (coins[i][j] √= 0 ? coins[i][j] : 0)`
(cuando neutralizamos, un valor negativo se trata como `0`).

3. * Initialización*
`dp[0][0] [0] = coins[0][0]`
Si `coins[0] [0] [0] [0] [0]], también fijamos `dp[0][0][1] = 0` (neutralizar el primer ladrón).

4. **Respuesta*
`max(dp[m-1][n-1][0], dp[m-1][n-1][1], dp[m-1][n-1][2] `

5. *Las complejidades*
*Tiempo* – `O(m × n × 3)` ♥ `O(mn)` (Ω 3 × 250 000 = 750 k) – rápido para 500×500.
*Pace* – `O(m × n × 3)` ♥ `O(mn)` (~ 4 MB).
También podemos reducir a 2 filas (`O(2 × n × 3)`), pero la matriz 3-D completa mantiene el código simple.

-...

## 🧩 Code Implementations

A continuación se presentan implementaciones limpias y bien agregadas en **Java, Python, y C++**.
Siéntete libre de copiarlas en tu IDE y haz tus propias pruebas.

### 1Ω Java Java (estilo LeetCode)

``java
Clase Solución {
máximo Cantidad(int[][] coins) {
int m = coins.length, n = coins[0].length;
int final NEG = Integer.MIN_VALUE / 4; // seguro negativo centinela

// dp[i][j][k] : max coins at (i,j) after using k neutralisations
int[][][] dp = nuevo int[m][n][3];
para (int i = 0; i)
para (int j = 0; j)
para (int k = 0; k)
dp[i][j][k] = NEG;

// celda de inicio
dp[0][0][0] = coins[0][0];
si (coins[0][0] 0) dp[0][1] = 0; // neutralizar el primer ladrón

para (int i = 0; i)
para (int j = 0; j) {}
si (i == 0 " 0) continuar; // ya inicializado

para (int k = 0; k)
// desde arriba
si 0) {
// 1. moverse sin neutralizar
dp[i][j][k] = Math.max(dp[i][j][k],
dp[i-1][j][k] + coins[i][j]);

// 2. mover y neutralizar esta célula
si 0) {
int val = dp[i-1][j][k-1];
val += (coins[i][j] >= 0) monedas[i][j] : 0;
dp[i][j][k] = Math.max(dp[i][j][k], val);
}
}

// desde la izquierda
si (j  contactos 0) {
dp[i][j][k] = Math.max(dp[i][j][k],
dp[i][j-1][k] + coins[i][j]);

si 0) {
int val = dp[i][j-1][k-1];
val += (coins[i][j] >= 0) monedas[i][j] : 0;
dp[i][j][k] = Math.max(dp[i][j][k], val);
}
}
}
}
}

devolver Math.max(dp[m-1][n-1][0],
Math.max(dp[m-1][n-1][1], dp[m-1][n-1][2]);
}
}
`` `

-...

#### 2down⃣ Python 3

``python
Solución de clase:
def máximo Cantidad (self, coins: List[List[int]) - int:
m, n = len(coins), len(coins[0])
NEG = 10**15

dp = [[NEG] * 3 for _ in range(n)] for _ in range(m)]

# Start cell
dp[0][0] [0] = coins[0][0][0]
si las monedas [0] [0]
dp[0][0][1] = 0 # neutralise first robber

para i en rango(m):
para j en rango(n):
si == 0 y j == 0:
continuar

para k en rango(3):
# desde arriba
si yo 0:
dp[i][j][k] = max(dp[i][j][k],
dp[i-1][j][k] + coins[i][j])
si k > 0:
val = dp[i-1][j][k-1] + \
(coins[i][j] if coins[i][j] }= 0 más 0)
dp[i][j][k] = max(dp[i][j][k], val)

# desde la izquierda
si j > 0:
dp[i][j][k] = max(dp[i][j][k],
dp[i][j-1][k] + coins[i][j])
si k > 0:
val = dp[i][j-1][k-1] + \
(coins[i][j] if coins[i][j] }= 0 más 0)
dp[i][j][k] = max(dp[i][j][k], val)

volver max(dp[m-1][n-1])
`` `

-...

### 3down⃣ C++ (LeetCode style)

``cpp
Clase Solución {
public:
máximo Amount(vector seleccionadovector asignadoint implicados iguales monedas) {
int m = coins.size(), n = coins[0].size();
const int NEG = -1e9; // safe negative sentinel

// dp[i][j][k] – max coins at (i,j) after using k neutralisations
vector realizador realizador seleccionado,3 títulos, dp(m, vector seleccionadoarray identificado,3 contactos(n, {NEG,NEG,NEG})

dp[0][0][0] = coins[0][0];
si (coins[0][0] 0) dp[0][0][1] = 0; // neutralizar el inicio

para (int i = 0; i) {}
para (int j = 0; j)
si (i == 0 " 0) continuar; // ya init

para (int k = 0; k)
// desde arriba
si 0) {
dp[i][j][k] = max(dp[i][j][k],
dp[i-1][j][k] + coins[i][j]);

si 0) {
int val = dp[i-1][j][k-1];
val += (coins[i][j] >= 0 ? coins[i][j] : 0);
dp[i][j][k] = max(dp[i][j][k], val);
}
}

// desde la izquierda
si (j  contactos 0) {
dp[i][j][k] = max(dp[i][j][k],
dp[i][j-1][k] + coins[i][j]);

si 0) {
int val = dp[i][j-1][k-1];
val += (coins[i][j] >= 0 ? coins[i][j] : 0);
dp[i][j][k] = max(dp[i][j][k], val);
}
}
}
}
}

volver max({dp[m-1][n-1][0], dp[m-1][n-1][1], dp[m-1][n-1][2]});
}
};
`` `

■ **Tip** – Si quieres afeitar la memoria, sustitúyase `dp` con dos filas (`dp[2][n][3]') y ruede los índices.

-...

## 🎯 Lo que hace que esta solución sea “buena” (la parte * Acepto*)

Silencio Silencio Silencio Silencio ❌ Silencio ❌
Silencio...
Silencio** El DP cubre *todos* posibles usos de neutralizadores. Silencio ❌ Una recursión ingenua que intenta cada camino explota exponencialmente (`O(2^mn)`). Silencio
Silencio **Tiempo Eficiencia** ✔ ~ 750 k operations for 500×500 – easily under 0.1 s on LeetCode. Silencio ❌ Brute‐force `O(3^mn)` or `O(mn2)` solutions hit the TL. Silencio
Silencio **Memory‐Footprint** Silencio ✔ ~ 4 MB (full 3‐D array) – bien debajo del límite de 256 MB de LeetCode. ❌ Recidiva o memoización sin podar utiliza demasiado pila y memoria. Silencio
Silencio** El DP puede reducirse a **dos filas** (`O(2×n×3)`) para entornos conmovedores de memoria extremos. ❌ Tratar de optimizar el coste de legibilidad puede hacer difícil la explicación de la entrevista. Silencio

-...

##  tuya Las partes "Ugly" – Pitfalls comunes para evitar

1. **Repetición profunda sin memoización** – obtiene un *RuntimeError* o *Time Limit Exceeded* en Python/LeetCode.
2. ** almacenar cuatro enteros por celda** (`k=0,1,2`) en un gigantesco vector 3-D y nunca podar conduce a ~ 1 GB de memoria (en idiomas con alta sobrecabeza).
3. **Olvidándose de neutralizar una célula negativa** – perderás el presupuesto de dos neutralizaciones y devolverás una respuesta sub-optimal.

**Bottom line:** Adherirse al DP 3D descrito anteriormente; es simple, rápido y demuestra lógica clara a un entrevistador.

-...

##  inaceptable Bonus: A Test Harness (Python)

``python
si __name_ == "__main__":
s = Solución()
print(s.maximumAmount([0, 1], [-2, -3])) # → 1
print(s.maximumAmount([1, -5], [0, 2])) # → 3
# ¡Añada sus propias redes aquí!
`` `

-...

## 🚀 Listo para clavar la entrevista?

* Camina por la definición **estatal** ( " dp[i][j][k] " ).
* Explicar la lógica **transición** – especialmente el caso “utilizar un neutralizador”.
* Destaca el truco **inicialización** para la primera celda.
* Mencione el intercambio de tiempo/espacio** y la posible optimización de 2 puntos.
* Mostrar uno de los fragmentos de código limpio y estar preparado para **debug** en el lugar.

Si puede hacerlo, ha demostrado que entiende la programación dinámica, las limitaciones de recursos y el manejo de insumos a gran escala – todas las habilidades que los reclutadores están buscando en un ingeniero de software senior. 🚀

¡Feliz codificación! ▪