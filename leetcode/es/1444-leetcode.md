-...
Título: LeetCode 1444. Número de formas de cortar una pizza -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Solving LeetCode 1444 – Número de formas de cortar una pizza
** código fuente completo en Java, Python, y C++++ + un blog SEO-friendly* *

-...

## 1. El Código

A continuación encontrará tres soluciones autocontenidas y listas para funcionar: una para **Java 17**, **Python 3.10+**, y **C+17**.
Los tres usan la misma idea óptima:

* **Matrimonio de la suma Prefix** – rápidamente nos dice cuántas manzanas hay en cualquier sub-rectángulo.
* **3-D memoized DFS** (`dp[remaningCuts][row][col]`) – cuenta las formas de cortar la pizza que comienza en la celda `(row, col)` con un número determinado de cortes a la izquierda.

``text
tiempo : O(k · filas · cols · (rows + cols)
espacio : O(k · filas · cols)
`` `

-...

### Java (Java 17)

``java
importar java.util*;

Solución de la clase pública {}
int final estático privado MOD = 1_000_000_007;

int ways (String[] pizza, int k) {
int m = pizza.length;
int n = pizza[0].length();

// Cantidad de manzanas: pre[r][c] = manzanas en submatrix (r,c) .. (m-1,n-1)
int[][] pre = nuevo int[m + 1][n + 1];
para (int r = m - 1; r  0; --r) {
para (int c = n - 1; c 0; --c) {
pre[r][c] = pre[r][c + 1] + pre[r + 1][c] - pre[r + 1][c + 1]
+ (pizza[r].charAt(c) == 'A' ? 1 : 0);
}
}

int[][][][] memo = nuevo int[k][m][n];
(int[][] a : memo)
(int[] b : a)
Arrays.fill(b, -1);

dfs(0, 0, k, pre, memo);
}

int privado dfs(int r, int c, int cuts Izquierda,
int[][] pre, int[][][] memo) {
int m = pre.length - 1, n = pre[0].length - 1;

si (pre[r][c] == 0) retorno 0; // no manzana en esta rodaja
si (cortesLeft == 1) retorno 1; // última pieza debe contener al menos una manzana

int Val = memo[cortes] Izquierda 1][c];
si (memoVal!= -1) devolver memoVal;

int ways = 0;

// Cortes horizontales
para (int nr = r + 1; nr)
si (pre[r][c] - pre[nr][c] 0) { // parte superior tiene una manzana
maneras = (siempre + dfs(nr, c, cutsLeft, pre, memo)) % MOD;
}
}

// Cortes verticales
para (int nc = c + 1; nc) {}
si (pre[r][c] - pre[r][nc] 0) { // parte izquierda tiene una manzana
maneras = (vías + dfs(r, nc, cutsLeft, pre, memo)) % MOD;
}
}

memoVal = maneras;
retorno;
}
}
`` `

-...

### Python (Python 3.10+)

``python
desde functools import lru_cache
de la importación Lista

MOD = 10**9 + 7

Solución de clase:
def ways(self, pizza: List[str], k: int) - int:
m, n = len(pizza), len(pizza[0]

# prefijo sum: pre[r][c] = manzanas en submatrix (r,c) .. (m-1,n-1)
pre = [0] * (n + 1) para _ en rango(m + 1)]
para r en rango(m - 1, -1, -1):
para c en el rango (n - 1, -1, -1):
pre[r][c] = (
pre[r][c + 1] + pre[r + 1][c] - pre[r + 1][c + 1]
+ (pizza[r][c] == 'A')
)

@lru_cache(None)
def dfs(r: int, c: int, cuts_left: int) int:
si pre[r][c] == # No hay manzana en esta pieza
retorno 0
si cuts_left == 1:
Regreso 1

res = 0
# Cortes horizontales
para nr en rango(r + 1, m):
si pre[r][c] - pre[nr][c] 0:
res = (res + dfs(nr, c, cuts_left - 1)) % MOD

# vertical cuts
para nc en rango(c + 1, n):
si pre[r][c] - pre[r][nc] 0:
res = (res + dfs(r, nc, cuts_left - 1)) % MOD

retorno

devolver dfs(0, 0, k)
`` `

-...

### C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
static constexpr int MOD = 1'000'007;

int ways(vector identificadostring tender pizz, int k) {
int m = pizza.size(), n = pizza[0].size();
vector seleccionado(n + 1, 0));

para (int r = m - 1; r  0; --r) {
para (int c = n - 1; c 0; --c) {
pre[r][c] = pre[r][c + 1] + pre[r + 1][c] - pre[r + 1][c + 1]
+ (pizza[r][c] == 'A' ? 1 : 0);
}
}

vector realizador realizador seleccionado, seleccionado(n, -1));
dfs(0, 0, k, pre, memo);
}

privado:
int dfs(int r, int c, int cuts, const vector seleccionadovector Pre,
vector seleccionador seleccionador seleccionador:
si (pre[r][c] == 0) retorno 0; // no manzana
si (cortes == 1) retorno 1; // última rebanada

intю res = memo[cuts - 1][r][c];
si (res!= -1) restitución;

res = 0;
int m = pre.size() - 1, n = pre[0].size() - 1;

// Cortes horizontales
para (int nr = r + 1; nr)
si (pre[r][c] - pre[nr][c] 0) {
res = (res + dfs(nr, c, cuts - 1, pre, memo)) % MOD;
}
}

// cortes verticales
para (int nc = c + 1; nc) {}
si (pre[r][c] - pre[r][nc] 0) {
res = (res + dfs(r, nc, cuts - 1, pre, memo)) % MOD;
}
}

restitución;
}
};
`` `

-...

## 2. El Blog – “El Bien, el Mal, el Ugly” de LeetCode 1444

■ **Desbloquear la solución lista para la entrevista para LeetCode 1444 – Número de formas de cortar una pizza* *
■ Programación dinámica maestra, sumas prefijo y memoización recursiva en **Java, Python y C+**.
■ Ideal para el prep de primera, back-end, y la entrevista completa.

-...

#### Introduction

Si te estás preparando para entrevistas de codificación, probablemente has encontrado el problema *Pizza Cutting* – LeetCode **1444**.
El objetivo es simple: cortar una pizza rectangular en piezas **k** tal que cada pieza contiene al menos una manzana (`'A'`).
Los cortes pueden ser horizontales o verticales, y contamos todas las formas distintas modulo 1 000 000 007.

¿Por qué este problema es una mina de oro para los entrevistadores?

* Combina ** programación dinámica grave** con **estatal-compresión**.
* Prueba su capacidad para manejar **memoización** y **prefix‐sum** optimizaciones.
* Te obliga a pensar en ** condiciones ilimitadas** (por ejemplo, cuando una manzana está ausente).

Vamos a romper ** el bien**, ** el malo**, y ** el feo** de resolver este problema.

-...

## The Good: Clean, Readable, and Optimized

TENIDO VALORACIÓN ANTERIOR Por qué importa
Silencio...
Silencio **Prefix‐Sum Matrix** tención O(1) consulta para manzanas en cualquier sub-rectángulo. Silencio
Silencio **3-D DP Memoization** (`dp[cuts][row][col] ' ) tención Reutiliza los resultados, previniendo el soplo exponencial. Silencio
Silencio **Largos de Corte Iterativo** TENIDO Lazos horizontales/verticales rectos; sin sobrecarga adicional. Silencio
Silencio **Modulo Arithmetic Dentro del Loop** Silencio mantiene números dentro de los límites de 32 bits, evitando el desbordamiento. Silencio
Silencio **Idioma-Independiente Lógica** Silencio El mismo enfoque funciona para Java, Python, C++. Silencio
Silencio ** Complejidad del tiempo \(O(k·rows·cols·(rows+cols))\)** Silencio Conoce las limitaciones oficiales (≤ 30 × 30 × 30). Silencio
Silencio **Complejidad del espacio \(O(k·rows·cols)\)** Silencio Aceptable para entornos modernos de entrevista. Silencio

#### Takeaway

- **Procesamiento previo rápido** (la suma prefijo) corta el espacio de búsqueda dramáticamente.
- **Memoización** transforma una recursión ingenua de `O(2^k)` a un polinomio.
- **Diseño móvil** (ayudado separado del DFS) hace que el código sea testable y sostenible.

-...

## The Bad: Naïve Brute‐Force, Redundant Recursion

❌ Pitfall Silencio Consequence
Silencio--------------------------
Silencio Comprobando cada corte *sin* sumas prefijo Silencio Cada llamada escanea un sub-matrix → **O(rows·cols)** por llamada. Silencio
Silencio Re‐computing sub-problemas Silencio Tiempo exponencial, imposible incluso para `k=3`. Silencio
Silencio Olvidar el caso base de “no manzana” tención Produce respuestas incorrectas para casos de esquina. Silencio
Silencio Usando variables globales en recursión (Python) Silencio difícil razonar sobre estado y errores. Silencio

**Bottom line** – a *pure DFS* que escanea la rejilla en cada recursión es un *slow-down* que los entrevistadores marcarán.

-...

## The Ugly: Edge‐Case Nightmares " Over-Optimized Jargon

1. **Mising Apples in the Whole Pizza**
* La pizza puede contener **0 manzanas** en algunas filas/columnas.
* Usted debe *ignore* cortes que dejarían una pieza libre de manzana; de lo contrario la respuesta será `0`.

2. **Off‐By‐One Errores en el índice de prefijo**
* Las sumas de prefijo suelen utilizar un truco de “extra fila/columna” (“pre[m][c] = 0`).
* Un único índice de tipo erróneo ( " pre[r+1][c] " vs. `pre[nr][c] " ) voltea la lógica.

3. *Large k ⇩ 30*
* Si usted asigne ingenuamente `dp[k][rows][cols]`, usted alcanzará ** límites de memoria** para entradas más grandes.
* El truco es indexar `dp` por ** cortes izquierda** (`k-1`) – se mantiene pequeño.

4. **Manejo de modulo en C++**
* Olvidar aplicar `% MOD` dentro del bucle puede desbordar `int`.
* Java’s `int` is 32‐bit; Python’s `int` is unbounded, but you still need `% MOD` for performance.

-...

## Real‐World Interview Insight

■ **Los entrevistadores suelen preguntar**: *“¿Puedes probar por qué este DP es correcto?”*
■ Explicar que cada estado `(cortes, r, c)` representa una sub-pizza **unica** (el que comienza en la celda `(r, c)` y se extiende a la parte inferior derecha).
■ Cualquier corte válido de este estado divide la sub-pizza en dos sub-rectángulos; la parte superior/izquierda debe contener al menos una manzana, garantizando la parte inferior/derecha se puede manejar recursivamente.

-...

## Step‐by‐Step Solution Walk-through

1. *Construir el Prefix‐Sum*
* Para cada celda `(r, c)`, compute apples in the **south‐east** sub-grid.
* Fórmula:
``pre[r][c] = pre[r][c+1] + pre[r+1][c] - pre[c+1] + (pizza[r] [c] == 'A'); `` `

2. **Recursive DFS + Memoization**
* Caso base 1: `pre[r][c] == 0` → retorno 0 (sin manzana).
* Caso básico 2: " cortes " Izquierda 1` → retorno 1 (la rebanada restante ya contiene una manzana).
* Memo lookup (`dp[cutsLeft-1][r][c]`).
* Pruebe todos los cortes horizontales posibles ( < nr > ) donde la rodaja **top tiene una manzana**.
* Prueba todos los cortes verticales posibles ( < nc > c > ) donde la rodaja **izquierda tiene una manzana**.
* Acumulate results modulo `1_000_000_007`.

3. **Retorno** el resultado de la llamada raíz (`dfs(0, 0, k)`).

Los fragmentos de código anteriores implementan exactamente este algoritmo.
Las versiones **Java** y **C++** utilizan arrays explícitos 3-D para la memoización, mientras que **Python** se basa en `functools.lru_cache` para la memoización transparente.

-...

## Cómo utilizar estas soluciones en entrevistas

1. **Explicar la idea primero** – hablar sobre sumas prefijas y memoización.
2. **Sketch the state** – show `dp[remainingCuts][row][col]`.
3. **Pseudocode** – escriba los bucles para cortes horizontales y verticales.
4. **Edge Cases** – pregunte al entrevistador sobre la situación de “no manzana” y cómo lo maneja.
5. **Implement** – codifica la solución en el idioma con la que más te sientes cómodo (Java, Python o C++).

-...

### Common Interview Questions Derived from 1444

Silencioso Pregunta de Habilidad Principal Testado
Silencio...
Silencio ¿Y si 'k' es más grande que el número de manzanas? TENCIÓN Boundary razonamiento " prueba de corrección. Silencio
Silencio ¿Cómo modificaría el algoritmo para cortes de 4 direcciones? tención Generalización " explotación estatal. Silencio
Silencio ¿Puede preprocesar la cuadrícula de forma diferente? estructuras de datos alternativas (BIT, árboles de segmento). Silencio
Silencio ¿Por qué el prefijo-sum está orientado a la esquina inferior derecha? ← Optimizar para las consultas “cualquier sub-rectángulo”. Silencio

-...

## The Ugly: Debugging Missteps & Performance Pitfalls

1. **Off‐by‐One in Prefix Indices** – conduce a conteos incorrectos de manzana.
2. **Missing the “no apple” base case** – cuenta rebanadas inválidas.
3. **Usar un 'int' en Python para la profundidad de recursión** – conduce a 'RecursionError'.
4. **Failing to mod after every addition** – overflows in Java/C++ and wrong results.
5. **Recuerdo excesivo** – asignar `dp[k][rows][cols]` sin el `-1` offset puede causar `StackOverflowError` en Java.

-...

## 3. Por qué este blog es su borde en la entrevista

* **Seo-friendly Headline** – “LeetCode 1444 – Número de maneras de cortar una pizza” aparece en las consultas de búsqueda de miles de buscadores de empleo.
* **Multi‐Language Showcase** – Contratar a los administradores les encanta ver a los candidatos cómodos con **Java**, **Python**, y **C+**.
* **Problem‐Solving Narrative** – La estructura “Good/Bad/Ugly” demuestra tu *meta-thinking* – un rasgo clave de entrevista.

-...

## Palabras finales

Mastering LeetCode 1444 es más que un código de escritura; se trata de construir una solución robusta, eficiente y clara que usted puede discutir con confianza con los entrevistadores.
Utilice los fragmentos arriba como su *referencia* y el blog para ensayar su *storytelling* durante las entrevistas de práctica.

¡Feliz codificación y buena suerte con tu próxima entrevista!