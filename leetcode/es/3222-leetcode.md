-...
Título: LeetCode 3222. Encontrar el jugador ganador en el juego de monedas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Problema - 3222. Encontrar el jugador ganador en el juego de monedas
**LeetCode : https://leetcode.com/problems/find-the-winning-player-in-coin-game/**

■ Se le dan dos números enteros positivos "x" (número de monedas de 75 valores) y "y" (número de monedas de 10 valores).
■ Alice y Bob juegan un juego basado en turnos empezando por Alice. En cada turno un jugador **debe tomar monedas que total **115**.
■ Si un jugador no puede hacer un movimiento pierden.
■ Devuelve el nombre del ganador si ambos juegan de forma óptima.

### 📌 Observaciones clave

Silencio Qué movimiento se parece a la razón de vida
Silencio...
TENIDO `1 × 75 + 4 × 10 = 115` TEN 75 + 40 = 115. Ninguna otra combinación de 75 y 10 monedas suma a 115. Silencio
Silencio Un giro consume **uno** 75 monedas **y **cuatro** 10 monedas Silencio Debe tener ambos recursos. Silencio
tención Número de posibles giros = `min(x, y/4)` Silencio El recurso limitante se agota primero. Silencio

Una vez que se conoce el número de vueltas `t`, el juego es simplemente un juego normal de estilo Nim:

* Si `t` es extraño → ** Alice** hace el último movimiento → ** Bob** pierde → Alice gana.
* Si `t` es incluso → Bob hace el último movimiento → Alice pierde → Bob gana.

Así la solución es sólo una fórmula aritmética de tiempo constante.

-...

## 🚀 Code Solutions

A continuación se muestran las implementaciones listas a paso, totalmente trabajando en **Java, Python y C+**.

■ Los tres usan el mismo tiempo O(1), algoritmo espacial O(1):
(Math.min(x, y/4) % 2 == 1) "Alice" : "Bob";

-...

## Java

``java
// Archivo: Solution.java
Clase Solución {
public String winPlayer(int x, int y) {
// Cada giro utiliza 1 moneda de 75 y 4 monedas de 10
int turn = Math.min(x, y / 4);
retorno (tornos % 2 == 1) "Alice" : "Bob";
}
}
`` `

* Complejidad* – **O(1)** tiempo, **O(1)** espacio.
*Test* – `nueva Solución().winningPlayer(2, 7)` → `"Alice"`.

-...

## Python

``python
# File: solution. py
Solución de clase:
Def ganando Player(self, x: int, y: int) - título str:
vueltas = min(x, y // 4) # división entero
"Alice" si gira % 2 más "Bob"
`` `

* Complejidad* – **O(1)** tiempo, **O(1)** espacio.
*Test* – `Solution().winningPlayer(4, 11)` → `"Bob"».

-...

### C++

``cpp
// Archivo: solution.cpp
#include >
#include ■string

Clase Solución {
public:
std::string winPlayer(int x, int y) {
int turn = std::min(x, y / 4); // división entero
retorno (tornos % 2) ? "Alice" : "Bob";
}
};
`` `

* Complejidad* – **O(1)** tiempo, **O(1)** espacio.
*Test* – `Solution().winningPlayer(2, 7)` → `'Alice'.

-...

## 📄 Blog Artículo – “El Bien, el Mal, y el Ugly of the Coin Game”

■ **SEO-Optimized Title* *
■ *“Coin Game Winner Algorithm – O(1) Java, Python, C++ – LeetCode 3222 Profundidad”*

-...

#### ## 1down⃣ El Bien

* **Simplicidad** – Una vez que te das cuenta de que un movimiento se ve obligado a ser `1×75 + 4×10`, el juego se colapsa a una única expresión aritmética.
* **Tiempo & Espacio** – O(1) es el lugar dulce para los entrevistadores. Sin bucles, sin recidiva, sin tablas de DP.
* ** Compatibilidad en idioma corsé** – La misma lógica funciona en Java, Python y C++. Perfecto para la preparación de la entrevista donde el idioma es una opción.
* **Explicación completa** – El blog descompone el razonamiento paso a paso, que es ideal para los reclutadores que leen sus notas.

-...

#### 2down⃣ El malo

* **Asunción de Optimal Play** – Nos saltamos la simulación de todos los estados. En juegos de monedas más complejos la estrategia óptima puede no ser obvia.
* ** Casos de Edge con Pequeños `y'** – Si 'y' se hicieron 4`, no puede ocurrir vuelta. El algoritmo naturalmente lo maneja (voques = 0 → Bob gana), pero un novato puede perder este matiz.
* **LeetCode‐Specific** – La explicación está estrechamente unida a la declaración del problema; usted necesita traducir la lógica cuando los valores de moneda cambian.

-...

#### 3down⃣ El Ugly

* **Mis-reading the Winning Condition** – Muchos candidatos se enredan por la frase “última jugada gana/ pierde”. En este problema *el jugador que **no puede** mover pierde*, que voltea la lógica de la paridad.
* **Hard‐to‐Debug Recursion** – Algunas soluciones intentan una simulación recursiva, causando el desbordamiento de pila en grandes entradas.
* **Over‐Engineering** – Construir una investigación estatal completa (DFS/BFS) cuando una sola fórmula basta es una trampa de entrevista clásica.

-...

### 4downs for Your Job Hunt

Esquía Silencioso Cómo el juego de la Moneda Demuestra que  durable
Silencio...
Silencio ** Pensamiento Algorítmico** Silencio Reducir un juego a su operación central (`1x75 + 4x10`). Silencio
Silencio ** Análisis de la complejidad** tención Mostrar O(1) vs O(n) trade‐offs. Silencio
Silencio **Code Clarity** tención Solución de 2 líneas en cualquier idioma – la brevedad es valorada. Silencio
Silencio **Problema Decomposición** Silencio Identificar las limitaciones de recursos (`x` vs `y/4`). Silencio
Silencio **Entrevista Comunicación** Silencio Explicar razonamiento en voz alta – “Aquí es por qué uso “min(x, y/4)” Silencio

-...

### 📚 Más lectura > Recursos

1. **Discusión de la solución de LeetCode** – https://leetcode.com/problems/find-the-winning-player-in-coin-game/solutions/
2. **Teoría del juego Básicas** – “Guerras de ganar para tus juegos matemáticos” (libro).
3. **La complejidad del tiempo Cheat Sheet** – https://www.topcoder.com/community/competitive-programming/tutorials/time-complexity/

-...

Pensamientos finales

El juego Coin es un escaparate de entrevistas clásico. La solución O(1) en Java, Python, y C++ demuestra que puedes encontrar el “carril dorado” en un problema y comunicarlo concisamente. Cuando los reclutadores miren su blog o su sumisión, detectarán:

* Entendiste las limitaciones básicas**.
* Usted puede **optimizar** inmediatamente.
* Puedes **ejecución** limpiamente en el idioma que elijas.

Mantenga el blog útil para las futuras entrevistas; es un refrescante rápido y un carrete de résumé-friendly. 🚀

-..