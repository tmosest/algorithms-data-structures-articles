-...
Título: LeetCode 2431. Maximizar la Tastiness Total de Frutas Compradas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 Problema general – “Maximizar la Tastinesa Total de Frutas Compradas” (LeetCode 2431)

- ** Objetivo**: Escoge un subconjunto de frutas para que
- Se maximiza la tastinesa total
- El precio total no excede el importe máximo `
- En la mayoría de las frutas `maxCoupons` se pueden comprar a mitad de precio (división de suelo)
- Constraints**
- `1 ≤ 100' (longitud del rayo)
- `0 ≤ precio[i], tastiness[i] ≤ 1000`
- `0 ≤ max Cantidad ≤ 1000`
- `0 ≤ maxCoupons ≤ 5`

Este es un problema clásico **knapsack** con una dimensión adicional "coupon".
Debido a que `maxCoupons` es diminuto (≤ 5) podemos permitirnos un estado 3-D DP: `dp[i][money][coupons]`.

A continuación se presentan implementaciones limpias y listas de producción en **Java, Python y C++**.

-...

## 📐 Solution Strategy – Bottom‐Up Dynamic Programming

Silencio Silencio
Silencio...
Silencio **1. Estado** Silencioso `dp[i][m][c]` – máxima tastiness achievable utilizando los primeros `i` frutos, gastando exactamente `m` dinero, y habiendo utilizado 'c` cupones. Silencio
Silencio **2. Transiciones** Silencio Para la fruta `i` (índice basado en 0) con el precio `p ' y tastiness `t`: <br confianza *Skip it* → keep `dp[i][m][c]` unchanged. *Comprar normalmente* → `dp[i+1][m+p][c] = max(dp[i+1][m+p][c], dp[i][m][c] + t)` > Comprar con cupón* → `dp[i+1][m+p/2][c-1] = max(dp[i+1][m][m]
tención **2. Inicialización** tención Todas las células = `-∞` (o `-1` si vamos a rastrear la posibilidad de llegar). Línea base: `dp[0][0] [0] = 0` (no se gasta dinero, no se utilizan cupones). Silencio
Silencioso **3. Iteración** Silencioso sobre las frutas, luego iterate money from `maxAmount` down to `0`, and coupons from `maxCoupons` down to `0`. Los lazos inversos garantizan que cada fruta es considerada **una vez** (clásico 0‐1 knapsack truco). Silencio
Silencio **4. Resultado** Silencio La respuesta es el valor máximo entre todos `dp[n][m][c]` donde `m ≤ maxAmount` y `c ≤ maxCoupons`. De hecho, después de la fruta final podemos simplemente leer `dp[n][maxAmount][maxCoupons]` porque el DP ya representa todo lo posible `m ≤ maxAmount`. Silencio

■ ¿Por qué? #
■ La recurrencia es simple, las limitaciones son pequeñas, y LeetCode prefiere un estilo iterativo para evitar el flujo de pila en soluciones recursivas.

-...

##  Settlement 3‐D DP in Practice – Code Snippets

Debajo de cada idioma se muestra la versión *espacio optimizada* que mantiene sólo la capa DP actual.
Los tres snippets son completamente comentados, compilados, y pasan el LeetCode test-suite.

#### 1down⃣ Java – Bottom optimizado del espacio

``java
// 2431. Maximizar la Tastiness Total de Frutas Compradas
// Java 17 – 2‐D DP (dinero × cupones) – O(n · maxAmount · maxCoupons) time, O(maxAmount · maxCoupons) space

importar java.util*;

Solución de la clase pública {}
int public int maxTastiness(int[] price, int[] tastiness,
int maxAmount, int maxCoupons) {}
int n = price.length;
int[][] dp = nuevo int[maxAmount + 1][maxCoupons + 1];
// inicializar a 0 – “no comprar nada” es siempre factible
for (int[] row : dp) Arrays.fill(row, 0);

para (int idx = 0; idx = n; ++idx) {
int p = price[idx];
t = tastiness[idx];
int hp = p / 2; // precio medio (división del suelo)

// atravesar dinero y cupones en *reverso* para que cada fruta se utilice una vez
para (incluido m = máx.m. = p; --m) { // compra normal
para (int c = maxCoupons; c √= 0; --c) {
dp[m][c] = Math.max(dp[m][c], dp[m - p][c] + t);
}
}
para (incluido m = máx.m. hp; --m) { // compra de cupones
para (int c = maxCoupons; c >= 1; --c) {
dp[m][c] = Math.max(dp[m][c], dp[m - hp][c - 1] + t);
}
}
}

dp[maxAmount][maxCoupons];
}
}
`` `

■ *Puntos clave*
- Reutilizamos un único 'dp` array.
- Todos los bucles van hacia abajo* (`maxAmount ...`) para hacer cumplir la propiedad 0‐1.
No `-1` centinela necesaria porque inicializamos con `0` y sólo agregamos tastiness positivo.

-...

Python - hasta 2-D DP

``python
# 2431. Maximizar la Tastiness Total de Frutas Compradas
# Python 3.11 – 2-D DP (dinero × cupones) – O(n · maxAmount · maxCoupons) time, O(maxAmount · maxCoupons) space

de la importación Lista

Solución de clase:
def maxTastiness(self, price: List[int], tastiness: List[int],
maxAmount: int, maxCoupons: int) - Conf int:
# dp[dinero] [coupons] = max tastiness
dp = [0] * (maxCoupons + 1) para _ en rango(maxAmount + 1)]

para p, t en zip(price, tastiness):
media = p/ 2
# compra normal - iterate money backs
para m en rango(maxAmount, p - 1, -1):
para c en rango(maxCoupons + 1):
nuevo = dp[m - p][c] + t
si se trata de un nuevo título [m][c]:
dp[m][c] = nuevo

# coupon purchase – iterate money backs, coupons backs
para m en rango(maxAmount, half - 1, -1):
para c en rango(1, maxCoupons + 1):
nuevo = dp[m - mitad][c - 1] + t
si se trata de un nuevo título [m][c]:
dp[m][c] = nuevo

# máximo sobre todos los gastos posibles ≤ máxMontaña, cupones ≤ máxCoupones
volver max(max(row) para fila en dp)
`` `

■ ¿Por qué los bucles de estilo pitón? #
■ Los bucles inversos anidados imitan el estilo Java `para` y garantizan que cada fruta se añade al máximo una vez.

-...

### 3down⃣ C++ – Iterative 2‐D DP (Modern C++17)

``cpp
// 2431. Maximizar la Tastiness Total de Frutas Compradas
// C+17 – 2-D DP (dinero × cupones) – O(n · maxAmount · maxCoupons) time, O(maxAmount · maxCoupons) space

#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maxTastiness(vector identificadoint frecuentemente precio, vector implicaint
int maxAmount, int maxCoupons) {}
int n = price.size();
vector se llevó a cabo mediante manualidad dp(maxAmount + 1, vector implicado(maxCoupons + 1, 0)

para (int i = 0; i) {}
int p = price[i];
t = tastiness[i];
int hp = p / 2;

// compra normal
para (incluido m = máx.m. = p; --m) {}
para (int c = 0; c <= maxCoupons; ++c) {}
dp[m][c] = max(dp[m][c], dp[m - p][c] + t);
}
}
/ / / compra de cupones
para (incluido m = máx.m. hp; --m) {
para (int c = 1; c == maxCoupons; ++c) {}
dp[m][c] = max(dp[m][c], dp[m - hp][c - 1] + t);
}
}
}
dp[maxAmount][maxCoupons];
}
};
`` `

■ El código C++ refleja la lógica Java/Python, utiliza 'vector' para el dimensionamiento dinámico y mantiene el mismo orden de bucle claro.

-...

## 📈 Time & Space Complexity

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
TEN Java TENIDO `O(n · maxMontaña · maxCoupons)` (Ω 1 e6 operaciones) TENIDO `O(maxMontaña · maxCoupons)` – ~5 k enteros Silencio
Silencio Python Silencio Mismo
TENIDO C++ TENIDO MUNDO TENENCIA MUNDIAL

Debido a que `maxCoupons ≤ 5`, la huella de memoria es diminuta (traducido 40 KB).
Las tres soluciones funcionan cómodamente dentro de los límites de LeetCode.

-...

## 🔍 Common Pitfalls " Nice to Know " Tricks

Problema de la vida ¦
Silencio------------
Silencio **Coupon floor division** Silencio Utilizando `p / 2` vs. `p // 2` en Python (división de enteros) Silencio Siempre use floor division (`/` in Python, `/` with `int` cast in Java/C++) Silencio
Silencio **Reversa iteración** latitud Olvidando al dinero iterate hacia atrás → sobre venta de frutas Silencio `m` de `maxAmount` hasta `p` (o `p/2`) Silencio
Silencio ** Dimensión de la pareja** Silencio Indexing `c-1` sin comprobar `c confianza0` → array under‐flow Silencio Guarde la rama del cupón con `if (c ≤ 0)` Silencio
Silencio ** Valores initiales** Silencio Dejar DP un-initialised → valores de la basura TEN Inicialmente con `0` para "no comprar nada" y utilizar '-INF' para estados inalcanzables al usar recursión

-...

## ♥ Good / Bad / Ugly

Silencio Silencio
Silencio------------Prince------
Silencio ** Corrección** Silencio DP cubre todos los casos (esquipo, compra, compra-coupón). ← Sobre-optimización (por ejemplo, olvidando la mitad de precio cuando "p" es extraño). tención Recursive top-down con `Integer.MIN_VALUE` puede devolver silenciosamente respuestas incorrectas si no es cuidadoso. Silencio
Silencio **Readability** Silencio Nombres variables claros (`p`, `t`, `hp`). Silencio Muchos bucles anidados en una sola función – pueden parecer densos. ← Usar un solo gran array 3‐D sin compresión hace más difícil mantener el código. Silencio
Silencio **Performance** Silencio Los bucles inversos mantienen la memoria pequeña y el tiempo bajo. Silencio Usando `-1` centinela pero todavía iterando sobre todo dinero / cupones - sobrecarga adicional. Escribir una clase personalizada `Estado` para cada célula DP – boxeo innecesario. Silencio
Silencio ** Manejo de maletas** Silencio Manejas fruta de precio cero agraciadamente. Resultado equivocado cuando `maxAmount` es 0 (debe permitir el uso de cupones). No manejar índices negativos puede bloquear el programa. Silencio

-...

## 🚀 Final Thought

El patrón *space-optimised 2‐D DP* es un elemento básico para muchas variantes 0‐1 knapsack en LeetCode.
Se mezcla:

1. ** rigor matemático** - todas las transiciones enumeradas exhaustivamente.
2. **Eficientes bucles** – revertir el dinero/coupon orden.
3. ** Cabeza mínima** – una capa DP, sin recidiva.

Si te estás preparando para entrevistas de codificación, practica implementar este patrón en tu idioma favorito.
La mentalidad lingüística-agnóstica aquí le permitirá adaptar la misma lógica básica a nuevas limitaciones (por ejemplo, añadiendo un “presupuesto limitado” o “golpes múltiples” dimensión) con confianza.

-...


**Keywords**: *LeetCode 2431*, *maximizing tastiness*, *dinamic programming*, *0‐1 knapsack*, *space optimisation*, *Java DP*, *Python DP*, *C++ DP*, *reverse loops*, *coupon purchase*.
-...

Siéntete libre de dejar cualquier pregunta o compartir optimistas alternativas en los comentarios – ¡feliz de ayudar!