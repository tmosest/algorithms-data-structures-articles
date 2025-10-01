-...
Título: LeetCode 1406. Piedra juego III -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 Stone Game III – Optimal DP Solution (Java / Python / C++)

A continuación se ** implementaciones limpias y listas de producción** para el problema LeetCode **1406. Piedra Juego III**.
Las tres soluciones funcionan en el tiempo **O(n)** y **O(1)** espacio auxiliar (la constante matriz de 3-length DP).

``java
// Java – LeetCode compatible
Clase Solución {
public String stoneGameIII(int[] stoneValue) {
int n = stoneValue.length;
// dp[i % 3] almacena la mejor ventaja neta (Alice – Bob) del índice i
int[] dp = nuevo int[3]; // automáticamente 0-inicializado

para (int i = n - 1; i 0; i--) {
int take1 = stone Valor[i] - dp[i + 1) % 3];

int take2 = Integer.MIN_VALUE;
si (i + 1 < n) tomar2 = piedra Valor[i] + piedra Valor[i + 1] - dp[i + 2) % 3];

int take3 = Integer.MIN_VALUE;
si (i + 2 < n) tomar3 = piedra Valor[i] + piedraValue[i + 1] + piedra Valor[i + 2] - dp[i + 3) % 3];

dp[i % 3] = Math.max(Math.max(take1, take2), take3);
}

int diff = dp[0]; // Alice – Bob
si 0) devolver "Alice";
si (diff 0) devuelve "Bob";
devolver "Tie";
}
}
`` `

``python
# Python – LeetCode compatible
Solución de clase:
def stone GameIII(self, stone Valor: Lista[int]) - título str:
n = len(stone) Valor)
dp = [0, 0, 0] # dp[i % 3] = la mejor ventaja de i

para i en rango(n - 1, -1, -1):
take1 = stoneValue[i] - dp[i + 1) % 3]

take2 = flotante('-inf')
si yo + 1 se hizo n:
take2 = stoneValue[i] + piedra Valor[i + 1] - dp[i + 2) % 3]

take3 = flotante('-inf')
si yo + 2 se hizo n:
toma3 = piedraValue[i] + piedraValue[i + 1] + piedra Valor[i + 2] - dp[i + 3) % 3]

dp[i % 3] = max(take1, take2, take3)

# Alice – Bob
si diff > 0: devolver "Alice"
si se apagan 0: devolver "Bob"
Regresa "Tie"
`` `

``cpp
// C++ – compatible con LeetCode
Clase Solución {
public:
string stoneGameIII(vector fieltro limitado piedraValue) {
int n = stoneValue.size();
int dp[3] = {0, 0, 0}; // dp[i % 3] = mejor ventaja de i

para (int i = n - 1; i 0; --i) {
int take1 = stone Valor[i] - dp[i + 1) % 3];

int take2 = INT_MIN;
si
take2 = stoneValue[i] + piedra Valor[i + 1] - dp[i + 2) % 3];

int take3 = INT_MIN;
si (i + 2 )
toma3 = piedraValue[i] + piedraValue[i + 1] + piedra Valor[i + 2] - dp[i + 3) % 3];

dp[i % 3] = max({take1, take2, take3});
}

int diff = dp[0]; // Alice – Bob
si 0) devolver "Alice";
si (diff 0) devuelve "Bob";
devolver "Tie";
}
};
`` `

-...

Blog Artículo: El Bien, el Mal, y el Ugly de Piedra Juego III

■ **Meta‐Description:**
■ Master LeetCode Piedra Juego III con una solución DP clara y óptima en Java, Python y C++. Aprenda el bueno, malo y feo de este problema clásico de la teoría del juego y aumentar su preparación de la entrevista.

-...

## 1. Introducción

Stone Game III es un puzzle basado en turnos de dos jugadores de clase ** que aparece en LeetCode como problema 1406. El juego obliga a los jugadores a tomar decisiones en una secuencia de pilas, y el ganador es el que tiene el mayor valor total de piedra después de que se tomen todas las pilas.

Si alguna vez has preparado para una entrevista, probablemente estés familiarizado con preguntas similares de “estrategia óptima”: *¿Cuál es el mejor movimiento que puedes hacer, asumiendo que el oponente también está jugando óptimamente? *
Stone Game III es una de esas preguntas que se pueden resolver elegantemente con ** programación dinamica** (DP). En este artículo, pasaremos por:

- ¿Por qué el problema es un DP de juego?
- La solución DP** que utiliza sólo una matriz de 3 elementos (`O(1)`). espacio)
- Fracasos de borde (valores negativos de piedra, longitudes impares, etc.)
- Las partes “buenas”, “malas”, y “muy” de la solución
- Cómo utilizar este conocimiento para impresionar a los entrevistadores

-...

## 2. Recapitulación de problemas (en sus propias palabras)

- Se le da un array `valor de piedra ` de longitud **n** (`1 ≤ n ≤ 5·104`).
- Alice comienza; Bob sigue; cada turno, un jugador puede tomar **1, 2, o 3** piedras de la pila más izquierda.
- Las puntuaciones se acumulan por jugador como la suma de los valores de las piedras tomadas.
- Ambos juegan.
- Regresar "Alice", "Bob" o "Tie" dependiendo de quién termine con la puntuación más alta.

-...

## 3. Intuición: De la teoría del juego al DP

### 3.1. El concepto “Net Advantage”

En lugar de seguir la puntuación individual de cada jugador, es más simple seguir la **diferencia** (La puntuación de Alice – La puntuación de Bob).
Si denotamos:

`` `
bestAdvantage(i) = máximo (AliceScore - BobScore) alcanzable
si el juego comienza en el índice i
`` `

entonces la respuesta es:

`` `
si mejorAdvantage(0) 0 - título Alice gana
si mejorAdvantage(0) Bob gana.
Tie
`` `

### 3.2. Relación Recursiva

Desde el índice `i` un jugador puede tomar:

1. **Una piedra** – el oponente comienza en `i+1`.
La ventaja resultante:
" Valor de piedra " - bestAdvantage(i+1)`

2. **Dos piedras** – si `i+1
`valo de piedra[i] + valor de piedra[i+1] - bestAdvantage(i+2)`

3. *Tres piedras* – si ‘i+2’
`Value[i] + stoneValue[i+1] + stoneValue[i+2] - bestAdvantage(i+3)`

El jugador elegirá el **maximum** entre estas tres opciones porque ambos juegan de forma óptima.

### 3.3. Up DP

Computamos `bestAdvantage` de derecha a izquierda (`i = n-1 ... 0`).
Cada paso depende sólo de los tres estados siguientes, por lo que podemos mantener **sólo los tres últimos valores** en lugar de un conjunto completo de 'n` tamaño.

■ **¿Por qué 3 valores? #
■ The recurrence uses `i+1`, `i+2`, and `i+3`.
■ Un búfer circular del tamaño 3 es suficiente.

Esto produce **O(n)** tiempo y **O(1)** espacio auxiliar.

-...

## 4. Código: tres idiomas

■ Cada implementación sigue la misma lógica, sólo con sintaxis específica del lenguaje y llamadas de biblioteca estándar.

*(Para consultar los bloques de código en la sección “Solutions” arriba.) *

#### 4.1. ¿Por qué? Este es el “bueno”

- **Simplicity**: Clear, one‐pass DP with only a few lines inside the loop.
- **Eficiencia**: Maneja el tamaño máximo de entrada (5·104) cómodamente.
- **Space-Optimised**: Sólo se almacenan 3 enteros, por lo que el uso de memoria es insignificante.
- **Aceptado por la Universidad**: Obras en Java, Python y C++, grandes para entrevistas de codificación donde la elección de idioma importa.

### 4.2. The “Bad”: Edge Cases " Misconceptions

¿Qué puede pasar mal? Silencio
Silencio...
Silencio ** Valores negativos** Silencio Asumiendo que todas las piedras son positivas conduce a decisiones erróneas. ← La recurrencia DP ya resta la mejor ventaja del oponente, por lo que naturalmente maneja los negativos. Silencio
Silencio **Using `int` overflow** Silencio `stoneValue[i]` hasta 1000, sum up to 3 000, but with many piles difference can reach ~5·107 → still within 32‐bit. Silencio Todavía seguro en 32-bit, pero use 64-bit si usted es paranoico. Silencio
Silencio **Indice de modulo incorrecto** TENEDAD-por-uno errores en `(i+1) % 3` vs `i % 3` puede dañar el búfer. TENIDO ATENCIÓN al patrón mostrado en el código: Resultado de la tienda en `dp[i % 3]`. Silencio
Silencio **Mis-reading the problem** Silencio Confusing “take 1, 2, o 3” con “take at most 3” (same cosa, pero algunos solvers piensan que siempre debes tomar 3). tención Revise explícitamente los límites: `si (i + 1  observado n)` etc. Silencio

#### 4.3. El “Ugly”: Naïve Recursion & TLE

Un enfoque de principiante típico:

``python
def helper(i):
si me >= n: retorno 0
mejor = -inf
suma = 0
para k en rango(1,4):
si yo + k
suma += piedra Valor[i + k - 1]
mejor = max(best, sum - helper(i + k))
mejor
`` `

- ** Complejidad del tiempo**: Exponencial (`O(3^n)`) debido a la recomputación de los mismos estados.
- **Desbordamiento de estante**: Para gran `n`, profundidad de recursión 104 sopla la pila.
- Resultado**: Informes de LeetCode ** Límite de tiempo excedió** (TLE) para entradas incluso modestas.

La parte fea es la memoización **inadequate**: si solo memorizas el mejor resultado pero no la diferencia, pierdes la perspectiva del oponente y terminas con la lógica incorrecta.

-...

## 5. Una prueba rápida de la corrección

**Claim:** El DP de abajo descrito anteriormente devuelve el ganador óptimo exacto.

*Proof Sketch*

1. **Casos de base**: Para `i ≥ n`, `bestAdvantage(i) = 0` (no quedan piedras). Correcto.
2. **Inductive Step**: Assume we know `bestAdvantage(i+1)`, `bestAdvantage(i+2)`, `bestAdvantage(i+3)` properly.
Desde el índice `i`, el jugador elige entre los 3 movimientos permitidos.
Al subcontratar el `bestAdvantage' del oponente, computamos la ventaja neta para el jugador actual.
Tomar el **maximum** garantiza la optimización contra un oponente racional.
Por lo tanto, `bestAdvantage(i)` es correcto.
3. ** Terminación**: Rellenamos todos los índices hasta 0, así que `bestAdvantage(0)` es correcto.
4. ** Determinación Winner**: La señal de `bestAdvantage(0)` coincide con la puntuación más alta. ∎

-...

## 6. Cómo utilizar esto en una entrevista

1. **Explicar la idea de “ventaja neta” primero**: Demostrar que no solo estás codificación, eres *comprendido* el problema.
2. **La recurrencia en una pizarra**: Incluso si usted está escribiendo código más tarde, el visual ayuda a los entrevistadores a seguir su razonamiento.
3. *Mostrar el truco de tres elementos * Muchos entrevistadores lo aman porque demuestra conocimiento de ** optimización espacial**.
4. **Mención de la mesa del perímetro**: Una mirada rápida a la mesa revela que has pensado en las trampas.
5. **Envuélvete con “¿Y si las reglas cambiaron?”**: Por ejemplo, si pudieras tomar hasta 4 piedras, solo aumentarías el tamaño del búfer. Esta flexibilidad impresiona.

-...

## 7. Conclusiones

Stone Game III puede parecer un juego simple, pero es un ejemplo de libro de texto de programación dinámica **optimal-strategy**. La clave es pensar en términos de *score diferencia*, escribir una recurrencia limpia, e implementar un espacio optimizado DP de fondo.

**Takeaway for interviews:**

- Hablar de *ventaja de red* antes de codificación.
- Use un búfer circular para el espacio " O(1) " .
- Destaca que los negativos se manejan automáticamente.
- Evite la recursión ingenua; en cambio, explique por qué su DP es óptimo.

Siéntase confiado: puede abordar Stone Game III (y problemas similares) con una solución concisa y probada en cualquiera de los idiomas principales. Buena suerte rompiendo esa próxima entrevista de codificación! 🚀

-...

## 8. Referencias " Lectura ulterior "

- Problema de LeetCode 1406 – [Stone Game III](https://leetcode.com/problems/stone-game-iii/)
- “Programación competitiva 4” – Capítulo sobre la teoría del juego DP**
- “Programación Dinámica – Una introducción sencilla” – GeeksforGeeks
- “Entrevista Warm‐Up: DP Problems” – Plataforma de práctica libre de Pramp

-...


-...

■ **¿Hay más inmersiones profundas? #
■ Suscríbete a nuestro boletín de noticias para los desafíos semanales de entrevistas, y vamos a hacer que esas preguntas difíciles del DP juntos.