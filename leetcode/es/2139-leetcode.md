-...
Título: LeetCode 2139. Movimientos mínimos para alcanzar la puntuación de la meta -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Movimientos mínimos para alcanzar la puntuación del objetivo – Un completo Guía (Java + Pitón + C++)

■ **SEO‐Optimized Título**: *LeetCode 2139 – Movimientos Mínimos para alcanzar la puntuación de Meta – Java, Python, C++ Soluciones, Algoritmo de Greedy, Complejidad del Tiempo, Prep de Entrevista*

-...

Sinopsis del problema

LeetCode #2139 – **Minimum se mueve a alcanzar la puntuación de Meta** (Medio)

■ Empiezas en el entero.
■ En un movimiento se puede:
1. `x = x + 1` (incremento) – usos ilimitados
2. `x = 2 * x` (doble) - en la mayoría de `maxDoubles` veces
■
■ ** Objetivo:** llegar a `target` con el número mínimo de movimientos.

■ **Constraints**
■ `1 ≤ blanco ≤ 109 `
■ `0 ≤ máx.

-...

## 2down Intuición: Trabajar hacia atrás

La estrategia más eficiente es pensar *desde el objetivo de vuelta a 1*.

* ¿Por qué?
* La duplicación es *poderosa* sólo cuando el número actual es *pequeño*.
* In reverse, “doubling” se convierte en “halving” (la operación más rentable).
* Quieres usar un doble como *late* como sea posible y tantas veces como puedas.

**Registro de gran intensidad ( simulación reversa)* *

TENIDO ESTADO TERRITORIO Acción Silenciosa
Silencio--------------------------
Silencioso `target` es **odd** Silencioso (`target-=1`) y luego halve (`target/=2`) Silencio
Silencioso `target` is **even** Silencio Halve (`target/=2`)
Silencio No `maxDoubles` left ← Subtract `target‐1` (sólo los incrementos permanecen)

El bucle se detiene cuando `target` se convierte en `1` o nos quedamos sin dobles oportunidades.

-...

## 3down Algoritm

``text
movimientos = 0
mientras que el objetivo 1 y máxDoubles 0:
si el objetivo es extraño:
movimientos += 2 # decremento + halve
objetivo -= 1
más:
movimientos += # Sólo halve
objetivo //= 2
maxDoubles -= 1

# restante aumentos si objetivo > 1
movimiento += objetivo - 1
Cambios de retorno
`` `

* ** Complejidad en el tiempo**: `O(objetivo de registro)` - cada uno de los lazos `target`.
* ** Complejidad del espacio**: `O(1)` – espacio auxiliar constante.

-...

## 4down Por qué funciona (el “bueno”)

* **Optimality** – En la dirección inversa la operación de halving es siempre la mejor que puedes hacer con un doble.
* **Simplicidad** – El bucle es corto, sin recidiva, sin mesa DP.
* **Scalability** – Trabaja para el más grande `target` (`109`) porque sólo se itera ` .

-...

## 5down Pi Potential Pitfalls (The “Bad”)

Silencio Silencio
Silencio...
Silencio Olvidando el decremento `maxDoubles` después de un halve  durable `maxDoubles -= 1` en cada iteración de bucles
Silencio Mezclando el “incremento” vs “decremento” en la simulación inversa TENIENTES Recuerde: un aumento adelante se convierte en un decremento atrasado
← Caso Edge `maxDoubles == 0` Silencio El bucle nunca funcionará, usted saltará directamente a `target‐1` Silencio

-...

## 6Get⃣ "Ugly" Code Anti-Patterns

1. **Recursivo DFS con memoización** – sobrematar, alta memoria.
2. **Brute‐force BFS** – espacio de estado exponencial (`109` nodos).
3. **Unnecesario manejo de grandes números** – La entrada de Python está bien, pero evitar el desbordamiento de 64 bits en C++ si usted usa `int` y cambia valores negativos.

-...

## 7فs Reference Implementations

### 7.1 Java

``java
Solución de la clase pública {}
int public int minMoves(int target, int maxDoubles) {}
int moves = 0;
mientras que (target Ø 1 " máximoDoubles " 0) {
((target) == 1) { //
movimientos += 2; // decremento + halve
objetivo -= 1;
♪ otra vez { // incluso
mudanzas += 1; // sólo halve
}
objetivo " 1° " ; // divide por 2
MaxDoubles...
}
cambio de retorno + (objetivo - 1); // aumentos restantes
}
}
`` `

## 7.2 Python

``python
Solución de clase:
def minMoves(self, target: int, maxDoubles: int) int:
movimientos = 0
mientras que el objetivo 1 y máxDoubles 0:
si objetivo % 2: # extraño
movimientos += 2 # decremento + halve
objetivo -= 1
# incluso #
movimientos += 1
objetivo //= 2
maxDoubles -= 1
movimientos de retorno + (objetivo - 1)
`` `

## 7.3 C++

``cpp
Clase Solución {
public:
int minMoves(int target, int maxDoubles) {}
int moves = 0;
mientras que (target Ø 1 " máximoDoubles " 0) {
si (target & 1) { //
movimientos += 2; // decremento + halve
objetivo -= 1;
♪ otra vez { // incluso
movimientos += 1;
}
objetivo " 1° " ; // divide por 2
--maxDoubles;
}
movidas de retorno + (objetivo a 1);
}
};
`` `

-...

Mesa de Complejidad

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Silencio Java Silencioso `O(log target)` Silencio
TENIDO Python TENIDO `O(log target)` Silencio
TENIDO C++ TENIDO `O(log target)` Silencio

-...

Preguntas frecuentes

Respuesta a la respuesta
Silencio...
Silencio **¿Puedo usar el enfoque codicioso cuando `maxDoubles` es grande?** Silencio Sí, porque cada iteración de bucle consume un doble, garantizando un uso óptimo. Silencio
Silencio *¿Qué pasa si `target` ya es 1?** Silencio La función devuelve `0` – no se necesitan movimientos. Silencio
Silencio **¿Es `int` seguro para C++?** Silencio Sí, porque `target ≤ 109` y nunca rebosamos el rango de 32 bits durante el halving. Silencio
Silencio **¿Y si 'maxDoubles' es 0?** Silencio Nos saltamos el bucle y regresamos 'target‐1' (todos los incrementos). Silencio

-...

## 🔗 Bonus: Running the Code Locally

``bash
# Python
python3 - "Seguido"
de la solución de importación
print(Solution().minMoves(19, 2)) # 7
print(Solution().minMoves(5, 0)) # 4
PY
`` `

``bash
# Java
javac Solution.java
Java Solution
`` `

``bash
# C++
g++ -std=c+17 solution.cpp -o sol
./sol
`` `

-...

Conclusión

El enfoque **reverso codicioso** ofrece una solución óptima, limpia y rápida para LeetCode 2139.
Es clave para tus entrevistas de trabajo:

1. **Piensa atrás** – a menudo reduce el tamaño del problema drásticamente.
2. **Greedy con una prueba de la optimización** – el halving es siempre la mejor estrategia de doble uso.
3. **Mantenga el código apoyado** – ninguna estructura de datos innecesaria, espacio O(1).

Comparte este post con tus pares, y siéntete libre de ajustar el código para que se ajuste a tu estilo de codificación. ¡Buena suerte aplastando la entrevista!

-...

■ **SEO Etiquetas:** LeetCode 2139, Mínimo pasos para alcanzar el objetivo Puntuación, Solución Java, solución Python, solución C++, algoritmo codicioso, pregunta de entrevista, preparación de entrevistas de codificación, análisis de algoritmos, codificación de entrevistas de trabajo.