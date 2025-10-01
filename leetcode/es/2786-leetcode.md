-...
Título: LeetCode 2786. Visitar las posiciones de la raya para maximizar la puntuación -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 2786 – * Visit Array Posiciones para maximizar la puntuación*
## The Good, The Bad, and The Ugly
■ ¿Quieres empezar tu próxima entrevista? * *
■ Aprende el truco DP más eficiente, véalo en **Java, Python, y C++**, y consigue un post de blog listo para copiar que puedes publicar en LinkedIn, Medium o tu portfolio personal.

-...

#### TL;DR

Silencio Idioma Silencio Tiempo Silencioso
Silencio----------------------------
Silencio **Java** Silencio **O(n)** Silencio **O(1)** Silencio `public long maxScore(int[] nums, int x)` Silencio
Silencio **Python** Silencio **O(n)** Silencio **O(1)** Silencio `def maxScore(self, nums: List[int], x: int) - propiedad int`  durable
Silencio **C+** Silencio **O(n)** Silencio **O(1)** TENIDO `long long maxScore(vector fieltro limitado nums, int x)` Silencio

El algoritmo mantiene **dos puntajes de funcionamiento** – uno para el mejor total si el último número visitado es ** incluso** y uno para **odd**.
En cada posición decidimos si viene de la misma paridad (sin penalidad) o de la paridad opuesta (pago `x`).
La clave es la simple recurrencia:

`` `
dp[paridad] = max(
dp[paridad] + nums[i], // misma paridad
dp[parity^1] - x + nums[i] // paridad opuesta
)
`` `

Porque sólo guardamos dos números, el costo del espacio es constante.

-...

Problema Recap

■ **Estás de pie en el índice 0 de un array `nums`.**
■ Usted puede saltar hacia adelante a cualquier índice " j " i " .
■ Índice de visita `i` añade `nums[i]` a tu puntuación.
■ Si saltas de `i` a `j` y `nums[i] y `nums[j]` tienen diferentes paridades, pierdes puntos "x".
■ ** Objetivo:** maximizar la puntuación total después de cualquier número de saltos (incluyendo permanecer al principio).

-...

## 🤔 Why DP Works

La decisión en el índice " sólo depende de:

1. The **maximum score** achievable end with an even number before `i.
2. The **maximum score** achievable end with an odd number before `i.

Todos los movimientos futuros son independientes de los índices exactos visitados, sólo de la paridad del último número.
Por lo tanto, un DP de dos estados es suficiente.

-...

## 🧩 Algorithm Walk-through

Silencio Lo que almacenamos ← Actualizar la regla Silencio Por qué funciona
Silencio----------------------------------------------------------
Silencio ** Initial** Silencio `dp[0] = dp[1] = -x` Silencio `dp[nums[0] limit1] = nums[0]` Silencio Empezamos en el índice 0. La otra paridad es imposible todavía, así que ponla en un valor muy pequeño (`-x`). Silencio
Silencio **Iterate i = 1 ... n-1** Silencio Para el número actual `cur = nums[i]` Silencio `dp[cur reducido1] = max(dp[cur limitado1], dp[cur1^1] - x) + cur` Silencio Dos opciones: vienen de la misma paridad (sin penal) o de la paridad opuesta (subtract `x`). Mejor. Silencio
Silencio **Result** Silencio `max(dp[0], dp[1])` Silencio La mejor puntuación independientemente de la paridad del último elemento visitado. Silencio

■ **Nota:** Todas las operaciones son `O(1)` por elemento, dando un algoritmo general de tiempo lineal.

-...

## 📌 Code in Three Languages

#### ## 1down⃣ Java

``java
Clase Solución {
public long maxScore(int[] nums, int x) {
long[] dp = new long[]{-x, -x}; // dp[0] = even, dp[1] = odd
dp[nums[0] & 1] = nums[0]; // start at index 0
para (int i = 1; i)
int parity = nums[i] " 1;
dp[parity] = Math.max(dp[parity], dp[parity ^ 1] - x) + nums[i];
}
devolver Math.max(dp[0], dp[1]);
}
}
`` `

#### 2down⃣ Python

``python
Solución de clase:
def maxScore(self, nums: List[int], x: int) - Conf int:
dp = [-x, -x]
dp[nums[0] & 1] = nums[0]
de nums[1:]:
p = num
dp[p] = max(dp[p], dp[p ^ 1] - x) + num
volver max(dp)
`` `

#### 3down⃣ C++

``cpp
Clase Solución {
public:
largo tiempo maxScore(vector asignadoint círculo nums, int x) {
dp[2] = {-x, -x}; // dp[0] even, dp[1] odd
dp[nums[0] & 1] = nums[0]; // start
para (int i = 1; i) ++i) {
int p = nums[i] " 1
dp[p] = max(dp[p], dp[p ^ 1] - x) + nums[i];
}
volver max(dp[0], dp[1]);
}
};
`` `

-...

## 📈 Complexity Analysis

Silencioso Complejidad
Silencio--------------------------
Silencio **Hora** Silencioso `O(n)` – uno pasa a través de la matriz. Silencio
Silencio** – sólo dos enteros largos. Silencio

Incluso para `n = 10^5` esto funciona cómodamente bajo 0.1 s en los tres idiomas.

-...

## ♥ Why This Beats Brute‐Force

Un enfoque ingenuo probaría todos los subconjuntos o todas las secuencias de salto – tiempo exponencial (`O(2^n)`).
Incluso una programación dinámica que almacena la puntuación máxima para cada índice ( " dp[i] " ) tendría que considerar todos los índices anteriores, dando lugar a un tiempo " O(n^2).

Nuestro DP de dos estados colapsa las posibilidades exponenciales en dos números porque la paridad es el único estado que importa para futuras transiciones. Este es el momento “aha” que convierte un problema de entrevista dura en una solución limpia y óptima.

-...

## 🎯 SEO‐Optimized Blog Structure

A continuación se muestra un esqueleto que puede copiar-pasar en Medium, Dev.to o LinkedIn. Añadir imágenes o capturas de pantalla de código para un mejor compromiso.

``markdown
# Visitar las posiciones de Array para maximizar la puntuación – LeetCode 2786

Resumen del problema

...

## 📊 Key Takeaways

- Dos estados DP (even/odd) reduce la complejidad de O(n2) a O(n).
- El espacio se puede bajar a O(1) manteniendo sólo las últimas puntuaciones.
- La recurrencia es simple: `dp[p] = max(dp[p], dp[p^1] - x) + cur`.

## ✅ Java / Python / C++ Código

## Java
``java
// bloque de código
`` `

## Python
``python
# code block
`` `

### C++
``cpp
// bloque de código
`` `

## 🚀 Performance

Silencio Idioma Silencio Tiempo (ms) Silencio Memoria (MB)
Silencio--------------------------------
Silencio Java Silencio 5 Silencio 12 Silencio
Silencio Python
Silencio C++

## 💬 Entrevista común Pitfalls

1. Olvidando inicializar la paridad imposible con un número muy negativo.
2. Mezclando operaciones de paridad bitwise.
3. Pensar un 'dp[i]` array es necesario – no lo es.

## Cómo dominar problemas similares

- Enfóquese en la compresión del estado*: busque un conjunto mínimo de variables que capten decisiones futuras.
- Practicar la paridad y la manipulación de bits – muchos problemas de DP se colgan en ellos.

##  abstract Conclusión

[Sus comentarios de clausura aquí. Anime a los lectores a probar el problema, compartir sus soluciones o hacer preguntas.]

`` `

-...

##  inaceptable Bonus: Visual Explanation (Optional)

Puede agregar un diagrama simple:

`` `
Índice 0 (even/odd) −► Índice 1 (even) −► Índice 2 (odd) −► ...
Silencio
" Pena de paz " , sin penalización " .

`` `

Marque los dos puntajes de funcionamiento y muestre cómo la transición toma el máximo de las dos opciones.

-...

#### 🎯 Final Note

Esta solución está lista para entrevistas de grado de producción** – pegarla en su cuaderno, practicar explicarlo en una entrevista de mock, y ver el guiño del entrevistador.

Buena suerte, y feliz codificación!