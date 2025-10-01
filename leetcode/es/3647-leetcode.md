-...
Título: LeetCode 3647. Peso máximo en dos bolsas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código de Solución

A continuación se presentan tres soluciones **ready‐to-run** – una cada una en Java, Python y C++ – que resuelven LeetCode 3647 “Maximum Weight in Two Bags”.
Los tres utilizan la misma idea de programación dinámica: tratar las dos bolsas como dos dimensiones de knapsack independientes e iterar sobre los elementos una vez.

Silencio Idioma Silencio Complejidad Silencio
Silencio--------------------------
tiempo, `O(w1 · w2) ` espacio TENIDO Iterative DP, no recursion ANTE
TENIDO Python TENIDO `O(n · w1 · w2) ` tiempo, `O(w1 · w2) ` espacio TENIDO MUNDO DP, utiliza una lista de listas TENIDO
TENIDO C++ TENIDO `O(n · w1 · w2) ' tiempo, `O(w1 · w2) ` espacio TENIDO Usos `vector seleccionadovector fielint Silencio

-...

#### 1.1 Java

``java
// Archivo: Solution.java
importar java.util*;

Solución de la clase pública {}
int public maxPeso(int[] pesos, int w1, int w2) {
// Tabla DP: dp[a][b] = peso máximo que se puede llevar
// con capacidad a en bolsa1 y capacidad b en bolsa2
int[][] dp = nuevo int[w1 + 1][w2 + 1];

para (peso único : pesos) {}
// iterate backs to avoid re-using the same item
para (int a = w1; a ±= 0; a) {
para (int b = w2; b 0; b) {
int cur = dp[a][b];
si (a ± = peso) {
cur = Math.max(cur, dp[a - weight][b] + weight);
}
si (b >= peso) {
cur = Math.max(cur, dp[a][b - weight] + weight);
}
dp[a][b] = cur;
}
}
}
dp[w1][w2];
}

--------- Demo Main (opcional) ----------
public static void main(String[] args) {
Solución s = nueva solución ();
System.out.println(s.maxWeight(new int[]{1, 4, 3, 2}, 5, 4)); // 9
System.out.println(s.maxWeight(new int[]{3, 6, 4, 8}, 9, 7)); // 15
System.out.println(s.maxWeight(new int[]{5, 7}, 2, 3)); // 0
}
}
`` `

-...

### 1.2 Python

``python
# File: solution. py
de la importación Lista

Solución de clase:
def maxPeso(self, weights: List[int], w1: int, w2: int) - título int:
# dp[a][b] = peso máximo alcanzable con capacidades a, b
dp = [0] * (w2 + 1) para _ en rango(w1 + 1)]

para peso en pesos:
para un rango(w1, -1, -1):
para b en rango(w2, -1, -1):
cur = dp[a][b]
si un peso >=:
r = max(cur, dp[a - weight][b] + weight)
si b Peso:
r = max(cur, dp[a][b - weight] + weight)
dp[a][b] = cur
retorno dp[w1][w2]

# -------- Demo...
si __name_ == "__main__":
s = Solución()
print(s.maxWeight([1, 4, 3, 2], 5, 4)) # 9
print(s.maxWeight([3, 6, 4, 8], 9, 7) # 15
print(s.maxWeight([5, 7], 2, 3)) # 0
`` `

-...

#### 1.3 C++

``cpp
// Archivo: solution.cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maxPeso(vector asignadoint pesos iguales, int w1, int w2) {
vector seleccionado(w2 + 1, 0)

para (peso único : pesos) {}
para (int a = w1; a ±= 0; --a) {
para (int b = w2; b 0; --b) {
int cur = dp[a][b];
si (a ± peso=)
r = max(cur, dp[a - weight][b] + weight);
si (b >= peso)
r = max(cur, dp[a][b - weight] + weight);
dp[a][b] = cur;
}
}
}
dp[w1][w2];
}
};

// -------- Demo...
int main() {}
Solución s;
cout se realizó s.maxWeight({1, 4, 3, 2}, 5, 4) Identificado endl; // 9
cout se realizó s.maxWeight({3, 6, 4, 8}, 9, 7)
cout se realizó s.maxWeight({5, 7}, 2, 3)
retorno 0;
}
`` `

-...

## 2. Artículo del Blog – “Peso máximo en dos bolsas: el bueno, el malo, el ugly”

■ *“Si usted puede resolver un problema que parece un 0‐1 Knapsack, usted es básicamente un programador.”* – *Comunidad de LeetCode*

## Tabla de contenidos
1. [Norma general](#problema vista previa)
2. [Nive Approaches](#naïve-approaches)
3. [Programación Dinámica – The Sweet Spot](#dynamic-programming-the-sweet-spot)
4. [The Good, The Bad, The Ugly] (#the-good-the-bad-the-ugly)
5. [Time & Space Complexity](#time-space-complexity)
6. [Por qué esto importa en las entrevistas](por qué-esto-matters-en-interviews)
7. [Final Takeaway](#final-takeaway)

-...

### Problema Resúmenes ## #### Nombre="problema-supervisión"

■ ** Peso máximo en dos bolsas* *
■ *LeetCode 3647 – Medium*

Se le da un array `pesos' de enteros positivos y dos enteros `w1`, `w2` que representan los límites de capacidad de dos bolsas. Cada artículo puede entrar en ** en la mayoría de una bolsa** (o no ser utilizado). El objetivo es **maximise el peso total** que termina en ambas bolsas.

*Constraints*
- 1 ≤ pesos. longitud ≤ 100`
- 1 ≤ pesos [i] ≤ 100 `
- 1 ≤ w1, w2 ≤ 300

Debido a que las capacidades son relativamente pequeñas (≤ 300), una solución de programación dinámica con `O(w1 · w2) ` espacio estatal es perfectamente factible.

-...

### Naïve Approaches #1 name="naïve-approaches"

1. **Brute‐Force Backtracking* *
Enumere cada asignación de cada artículo a bolsa 1, bolsa 2, o “no utilizado. ”
*Complejidad*: `3^n` – completamente infeasible incluso para `n = 20`.

2. **Recursive Top-Down with Memoization* *
Recidiva típica de 0‐1 knapsack con una dimensión extra para la segunda bolsa.
*Pros*: Fácil de entender.
*Cons*: matriz de memoización tridimensional puede volverse voluminosa; riesgo de desbordamiento de pila para la recidiva profunda.

Ambos métodos ingenuos golpearon rápidamente la pared en escenarios de entrevistas reales – son demasiado lentos y difíciles de explicar en menos de un minuto.

-...

### Dynamic Programming – The Sweet Spot = "dynamic-programming-the-sweet-spot"

##### 1. Knapsack dos dimensiones

La idea central: tratar las dos capacidades como un *grid* de estados.
`dp[a][b]` = peso total máximo que se puede lograr con * en la mayoría* `a` capacidad en el bolso 1 y `b` capacidad en el bolso 2.

##### 2. Transición del Estado

Por cada peso:

`` `
para un de w1 hasta 0
para b desde w2 hasta 0
cur = dp[a][b]
si un >= x: cur = max(cur, dp[a - x][b] + x)
si b >= x: cur = max(cur, dp[a][b - x] + x)
dp[a][b] = cur
`` `

*¿Por qué los bucles inversos? *
Actualizamos de alta a baja capacidad para que cada artículo se utilice al máximo una vez. El orden inverso garantiza que nunca leamos un estado que ya incluye el artículo actual.

##### 3. Respuesta final

`dp[w1][w2]` mantiene el peso total óptimo.

-...

### The Good, The Bad, " The Ugly " se hizo un nombre= "el bueno-el-bad-the-ugly"

Silencio Silencio
Silencio------------Prince------
Silencio **Concept** Silencio Extensión clásica 0‐1 knapsack – directamente para explicar. ← Requiere *dos* dimensiones; puede ser confuso para los principiantes. Un ingenuo DP tridimensional es a menudo la solución "muy" que la gente intenta primero y se atasca. Silencio
Silencio **Implementación** Silencio Bucles anidados compactos – fácil de leer y depurar. huella de memoria 'O(w1 · w2) puede ser grande si las capacidades son cerca de 300. TEN Recursion con un array 3-D puede desbordar la pila o golpear Java 'StackOverflowError`. Silencio
Silencio **Hora** Silencioso `O(n · w1 · w2)` – suficientemente rápido para límites dados. Si accidentalmente te alejas de `0` hacia arriba en lugar de hacia abajo, contarás artículos varias veces. ← Backtracking (`3^n`) es infeasible más allá de casos de prueba muy pequeños. Silencio
Silencio **Espacio** Silencioso 2D array sólo – no hay pila de recursión extra. TENIDO Para muy grande `w1` o `w2` usted se quedaría sin memoria. ← La memoización superior puede utilizar un mapa 3-D que es menos amigable. Silencio
Silencio **Interview Impact** Silencio Muestra la maestría del DP y la optimización espacial. Silencio Demonstrates cuidadosa atención a las condiciones de límites. tención Muestra la capacidad de reconocer y evitar el soplo exponencial. Silencio

-...

### Tiempo & Complejidad Espacial > = "time-space-complexity"

Silencio Silencio Silencio Silencio Silencio
Silencio--------------
Silencio Brute‐Force Silencioso `O(3^n)` Silencio
Silencio Top‐Down DP Silencio `O(n · w1 · w2) `` Silencio
TENIENDO 2-D DP TENIDO **`O(n · w1 · w2)`** Silencio **`O(w1 · w2)`** Silencio

Para las limitaciones dadas (`n ≤ 100`, `w1,w2 ≤ 300`) el DP inferior utiliza en la mayoría de los enteros `301 × 301 ♥ 90 601`, bien dentro de cualquier pila moderna.

-...

### ¿Por qué esto importa en las entrevistas?

**Muestra DP Mastery**: La mayoría de los entrevistadores les encanta ver que resuelven una variación del problema de Knapsack. Prueba que puedes manejar la optimización combinatoria.
- **Explicar los lazos inversos**: Una parte sutil pero esencial de la transición; perderla puede llevar a respuestas erróneas. Prueba su capacidad para pensar en estados “utilizados” vs “no utilizados”.
- ** Optimización del espacio**: Reducir de 3-D a 2-D demuestra que piensa en la memoria de runtime y la localidad de cache.
- Evitar las trampas de Stack La solución recursiva suele causar desbordamientos de pila. Si reconoce esto y cambia a una versión iterativa, impresionará.
- ¿Qué? Terminarás dentro de la ventana de entrevistas (aprobar 30 minutos) y tendrás tiempo para aclarar preguntas.

-...

## Final Takeaway > ## Final Takeaway > ## Final Takeaway > sign=final-takeaway

■ “Si puedes resolver esto con un DP 2-D, estás listo para abordar *cualquier* problema de empaquetado combinatorio. ”

El problema *Maximum Weight in Two Bags* es un “safe‐harbor” en los apilamientos de entrevistas: es lo suficientemente complejo para probar su profundidad algorítmica pero lo suficientemente simple como para ser explicado en menos de un minuto.
Utilice el enfoque **bottom‐up 2‐D DP** – es la solución “buena” que evita las trampas “malas” de una mesa de memo 3-D y pasa de lado el retroceso exponencial “muy”.

¡Feliz codificación! 🚀

-...

### SEO > Palabras clave

- LeetCode 3647
- Peso máximo en dos bolsas solución
- Preguntas de entrevista de programación dinámica
- 0‐1 Knapsack dos bolsas
- Problemas de medio LeetCode
- Entrevista optimización del espacio DP
- Knapsack bidimensional
- Entrevista de programación mejores prácticas

*(Sea libre de copiar/pasar los fragmentos de código arriba, ejecutarlos en su IDE, y ajustar la demo principal para probar más casos de borde.) *

-...

■ **¿Quieres más artículos “el bueno, el malo”?** Suscríbete a mi newsletter y consigue el *más común de las dificultades de entrevista* resuelto, *paso a paso*.

-...

**Author**: *[Su nombre]* – Ingeniero de personal completo, colaborador de código abierto y evangelista LeetCode.
LinkedIn: " https://linkedin.com/in/yourprofile "
GitHub: ■ https://github.com/yourgithub
Blog: ■ https://yourblog.com

-...


-...

■ *Si utiliza este artículo para un sitio web personal, recuerde acreditar a LeetCode y la descripción oficial del problema. *