-...
Título: LeetCode 1706. ¿Dónde caerá la pelota?
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 1706 - ¿Dónde caerá la pelota? ”
## A Complete, SEO‐Optimized Guide (Java / Python / C++)
■ ¿Quieres empezar tu próxima entrevista de codificación? * *
■ Lea cómo resolver LeetCode 1706, entender las trampas, y aprender cómo hablar de ello en un formato de entrevista *STAR*.

-...

## 1. Recap Problema (SEO palabras clave: *LeetCode 1706*, * simulación de bola*, *problema grave*)

Se le da un 'm x n` 2‐D array `grid`.
Cada célula contiene `1` (↘️ diagonal) o `-1` (pulsar diagonal).

Una bola se cae en la parte superior de cada columna.
Mientras se mueve hacia abajo:

* Si una bola encuentra un par en forma de V** (`1` junto a `-1'), se queda atascado.
* Si una bola golpea una pared (izquierda o frontera derecha) debido a la dirección del tablero, también se queda atascado.

Devuelva un array `respuesta` de tamaño `n` donde `respuesta[i]` es la columna donde la bola cae en la parte inferior, o `-1` si se queda atascado.

-...

## 2. Intuición " Observación clave

■ **Observación** – *Una bola sólo puede pasar de la columna `c` a la columna `c+grid[row][c] si el tablero en la siguiente columna apunta en la misma dirección. *

En inglés claro:
Si una célula en `(row, c)` es `1`, la bola tratará de mover derecho a la columna `c+1`.
Pero la pelota realmente se moverá **sólo si la celda `(row, c+1)` es también `1`**.
La misma regla se aplica para `-1` (moviendo a la izquierda).

Esta regla simple nos permite simular el camino de cada bola en **O(m)** tiempo, donde `m` es el número de filas.

-...

## 3. Brute‐Force DFS vs Iterative Simulation

Silencio Silencio Silencio Pros
Silencio...
TEN DFS (recursivo) ANTE Intuitiva, natural recursión ANTERIOR Riesgo de desbordamiento de pila para grandes rejillas (m ≤ 100 → fino, pero mal estilo)
TEN simulación iterativa TEN O(1) espacio por bola, no recursion TEN Slightly more calderaplate, but clear TEN

** Usaremos la simulación iterativa** porque es más rápido, más seguro y más fácil de explicar en una entrevista.

-...

## 4. La solución – paso a paso

1. ** array de resultados** – `int[] respuesta = nuevo int[n];`.
2. **Arriba cada columna de inicio** 'comenzar'.
3. #Simulate the ball #
* `col = start Col;`
* Por cada `row` from `0` to `m-1`:
* `nextCol = col + grid[row][col];` (la dirección del tablero actual)
* **Boundary check**: if `nextCol` is outside `[0, n-1]`, the ball is locked → `answer[startCol] = -1`.
* **V-shape check**: if `grid[row][nextCol] != grid[row][col]`, the ball is locked → `answer[startCol] = -1`.
* De lo contrario, establece `col = siguienteCol` y continúe hasta la siguiente fila.
4. Si el bucle termina, la bola ha salido → `respuesta[startCol] = col`.

-...

## 5. Aplicación del Código

### 5.1 Java

``java
*
* LeetCode 1706 – Donde caerá la bola
*
* simulación iterativa – O(m * n) tiempo, O(1) espacio extra.
*/
Clase Solución {
int[] findBall(int[] grid) {
int m = grid.length; // número de filas
int n = grid[0].length; // número de columnas
int[] result = new int[n];

para (int start = 0; start < n; start++) {}
int col = inicio; // columna actual de la bola

for (int row = 0; row < m; row++) {}
siguiente Col = col + grid[row][col]; // columna de destino

// Stuck si salimos de los límites
si (siguienteCol >= 0 {}
col = -1;
ruptura;
}

// Stuck si golpeamos un V-shape
si (grid[row] [nextCol] != grid[row][col]
col = -1;
ruptura;
}

col = siguiente Col; // mover bola a la siguiente columna
}

resultado[start] = col; // columna final (o -1 si está pegada)
}
Resultado de retorno;
}
}
`` `

### 5.2 Python

``python
Solución de clase:
"
LeetCode 1706 – Donde caerá la bola
Tiempo: O(m * n)
Espacio: O(1) por bola (result array is O(n)))
"

def findBall(self, grid: List[List[int]) - No. List[int]:
m, n = len(grid), len(grid[0])
res = []

para comenzar en rango(n):
col = comienzo
para fila en rango(m):
siguiente_col = col + grid[row][col]
# Out of bounds
si next_col se hizo 0 o next_col >= n:
col = 1
descanso
# V‐shape detection
si la rejilla [row] [next_col] != grid[row][col]:
col = 1
descanso
col = next_col
re.append(col)
retorno
`` `

### 5.3 C++

``cpp
*
* LeetCode 1706 – Donde caerá la bola
*
* Tiempo: O(m * n)
* Espacio: O(1) espacio extra
*/
Clase Solución {
public:
vector identificador gráfico encontrarBall(vector seleccionador) {
int m = grid.size();
int n = grid[0].size();
vector(n)

para (int start = 0; start  won n; ++start) {
int col = inicio; // columna actual de la bola

para (infiler fila = 0; hilera)
siguiente Col = col + grid[row][col];

// La pelota se atasca en la pared
si (siguienteCol >= 0 {}
col = -1;
ruptura;
}

// La pelota se atasca en una forma de V
si (grid[row] [nextCol] != grid[row][col]
col = -1;
ruptura;
}

col = siguiente Col; // avance a la siguiente columna
}

respuesta[start] = col; // columna final o -1
}

respuesta de retorno;
}
};
`` `

-...

## 6. Análisis de la complejidad

**Operación**
Silencio------------------------------...
Silencio Simulación de una bola Silencioso `O(m)` Silencio
TENIENDO `n` bolas TENIDO `O(m * n)` TENIDO `O(n)` para el array de salida

Dada las limitaciones (`1 ≤ m, n ≤ 100`), esta solución funciona en milisegundos y está bien dentro de los límites.

-...

## 7. Casos de borde para discutir en entrevistas

1. **Single row / single column** – asegura que la bola siempre sale o se queda atascada inmediatamente.
2. **Todas las `1` o todas las `-1` rejillas** – la bola simplemente se mueve a la derecha o a la izquierda hasta la pared.
3. ** Patrón alternativo `1,-1,1,-1...'** - cada bola se queda atascada debido a las formas V.
4. **Segmentos consecutivos `1` o `-1`** – la bola puede mover muchas columnas en una fila; el cheque de próxima celda garantiza la corrección.

Mostrar el caso de prueba en el artículo para reforzar que el código maneja todos ellos.

-...

## 8. “Bueno / malo / ugly” – Discusión final

← Subtítulos Lo que haría
Silencio...
Silencio ** Bien** Silencioso** La simulación es una línea única en cada idioma. No recursión** – Evita el desbordamiento de la pila. * Memoria predictible** – O(1) por bola, fácil de explicar. Silencio
Silencio **Bad** Silencio • **Quadratic if coded poorly** – Algunas personas intentan simular cada célula para cada bola, lo que lleva a `O(m*n^2)` (al igual que con `m, n≤100`, pero todavía un mal patrón). Silencio
Silencio **Ugly** Silencio • ** Recidencia de las FDI** – Funciona pero se siente “mágico” y puede chocar con entradas mucho más grandes. **Over-optimization** – Tratar de usar trucos bit-mask o matemáticas de lujo puede hacer que la solución sea imposible de leer. Silencio

■ **Tip de Interview** – Si un candidato propone una solución DFS, pídale que explique el uso de la pila y por qué es preferible un enfoque iterativo.

-...

## 8. Talking About the Problem in an Interview (STAR Format)

**Situación** Silencio**
Silencio----------------------------------------------------------
Silencio “Teníamos una rejilla de diagonales “m x n”. “Necesitamos saber dónde sale una pelota o si se quedaría atascada”. "Yo simulaba la bola para cada columna, comprobando hacia fuera de límites y formas V - un algoritmo de 'O(m*n)'." Silencio "El algoritmo terminó en 1 ms, pasó todos los casos de borde, y expliqué la complejidad claramente." Silencio

Estar listo para responder preguntas de seguimiento tales como:

* * * Why do we check `grid[row][nextCol] != grid[row][col]?* – Debido a que una bola sólo se mueve si el siguiente tablero apunta en la misma dirección; de lo contrario golpeamos una forma V.
* * *¿Y si tuviéramos 105 hileras?* – Discuss using **amortized O(m)** simulation per ball and how you’d pre-compute reachable columns with DP or memoization.
* *¿Podemos hacer mejor que O(m*n)?* – No, cada bola debe examinar cada hilera al menos una vez; sólo puede guardar el array de salida 'O(n)`.

-...

## 9. Lista de verificación de preguntas

1. **Leer el problema con cuidado** – prestar atención a las condiciones de “estuck”.
2. **Explicar la observación clave** – la dirección de la junta debe coincidir con la siguiente célula.
3. **Mostrar la simulación iterativa** – escribir pseudo-código en la pizarra.
4. ** Código de la palabra en un idioma** (Java, Python, o C++) – hacerlo limpio, comentado y basado en pruebas.
5. **Análisis de la complejidad** – `O(m*n)` tiempo, `O(n)` espacio.
6. **Talk through edge cases** – paredes, formas V, rejillas de una sola fila.
7. **Respuestas de seguimiento** – apilar seguridad, enfoques alternativos.

-...

## 10. Cómo este problema te ayuda a aterrizar un trabajo

* **Data‐Structure Skills** – Usted demuestra manipulación de arrays y indexación bidimensional.
* Pensamiento Algorítmico* Mostrar observación → simulación → implementación.
* **Coding Style** – Clean, iterative code is a hallmark of a senior engineer.
* **Interview Conversation** – Puede utilizar este problema como punto de conversación para *System Design* (visualizar la rejilla) y *Data Structures* (manejo de arrays 2-D).

■ **Pro tip:** Cuando tu entrevistador dice *“¿Podrías resolver esto recursivamente?”*, comienza con DFS, luego gira con gracia al método iterativo, explicando por qué el iterativo es superior.

-...

## 11. Conclusión – Final Takeaways

* **LeetCode 1706** es un problema clásico de simulación *grid‐ball* que prueba su capacidad de razonar sobre la dirección, los límites y las condiciones de fracaso.
* La simulación **iterative** es la solución más robusta, eficiente y amigable para entrevistas.
* Al comprender los aspectos *bueno* (implicidad), *bad* (pecamientos de recusión), y *en términos generales* (sobre ingeniería), podrás explicar el problema con confianza durante tu próxima entrevista de codificación.

-...

### Bono: Referencia rápida Cheat‐ Sheet

Silencio Idioma Silencio Tiempo Silencioso Silencioso Código
Silencio--------------------------------------
TEN Java TENIDO `O(m*n)` TENIDO `O(n)` ANTERIED Mostrar el código identificado/summary confiadoJava code block above identificado/details Silencio
TENIDO Python TENIDO `O(m*n)` TENIDO `O(n)` Mostrar código identificado/summary Bloque de código Python arriba identificado/detalles Silencio
TENIDO C++ TENIDO `O(m*n)` Silencio `O(n)` Mostrar el código identificado/summary ConfC++ bloque de código arriba Silencio

-...

### Final Word

Mastering **LeetCode 1706 Donde la caída de la bola** muestra que puede:

* Traducir una descripción real del mundo físico en código limpio y eficiente.
* Elija la estrategia algoritmo derecha (simulación sobre DFS).
* Comunicar la complejidad y los casos de borde a los entrevistadores.

¡Ahora practica! Añade este problema a tu lista de verificación de preparación de entrevistas, y entrarás en tu próxima entrevista técnica con confianza.

¡Feliz codificación! 🚀