-...
Título: LeetCode 948. Bolsa de Tokens -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## Bag of Tokens – Optimal Greedy Solution

**Problema* *
Empiezas con `poder = P` y `score = 0`.
Usted tiene una lista 'tokens' donde 'tokens[i]` es el "gasto de poder" de token *i*.
Usted puede jugar cualquier ficha a la vez, en cualquier orden, en una de dos maneras

Silencioso de acción
Silencio--------------------------
TENIENDO TENIDO `poder ≥ tokens[i] `` soporta `poder -= tokens[i], `score += 1o de abril de 1994
TENIDO ANTERIOR TENIDO `score ≥ 1` TENIDO `poder += tokens[i], `score -= 1` ANTE

Devuelve la puntuación máxima que puedes alcanzar.

----------------------------------------------------

### ¿Por qué funciona una estrategia codicioso de dos puntos

* **Arranque el token más barato para ganar un punto* *
Cuando usted tiene suficiente poder para jugar un token face‐up, siempre es mejor utilizar el *smallest* token disponible. Cualquier token más grande desperdiciaría más potencia para el mismo punto +1.

* **Use un punto para ganar la mayor potencia*
Cuando usted no puede jugar cualquier token face‐up, usted puede convertir un punto en el poder. Es óptimo utilizar el token * más grande* que permanece para esto, porque da la máxima potencia posible para un solo punto -1.

Si aplicamos repetidamente estas dos reglas,

1. crecer la puntuación siempre que la potencia permite (utilizando las fichas más baratas);
2. si nos quedamos sin poder pero aún tenemos puntos, recuperamos el poder con el token más caro (perdiendo un punto);
3. Parar cuando ninguno de los movimientos es posible.

Durante el proceso realizamos un seguimiento de la puntuación máxima vista – esa es la respuesta.

----------------------------------------------------

## Algorithm (dos puntos codiciosos)

`` `
# O(n log n)
l = 0 # token no utilizado más izquierda
r = len(tokens)-1 # rightmost unused token
puntuación = 0
maxScore = 0

mientras que l
si tokens[l] <= potencia: # puede jugar boca arriba
power -= tokens[l]
l += 1
puntuación += 1
maxScore = max(maxScore, score)
elif marcador 0: # necesidad de jugar boca abajo
potencia += tokens[r]
r)= 1
puntuación:= 1
# No puedo jugar más
descanso

volver maxScore
`` `

----------------------------------------------------

### Correctness Proof

Demostramos que el algoritmo devuelve la puntuación máxima alcanzable.

-...

#### Lemma 1
Si un token puede ser tocado boca arriba, usando el *smallest* que queda token nunca es peor que usar cualquier otro token.

Proof.
Jugar cualquier token face‐up consume su valor del poder y da +1 punto.
Dejar `x ≤ y` ser dos fichas restantes.
Después de jugar `x` tenemos al menos tanto poder dejado como después de jugar `y' (`P - x ≥ P - y`).
Ambas acciones dan el mismo punto +1, por lo que el uso de 'x' sólo puede dejarnos con más poder, que sólo puede ayudar en futuros movimientos. ∎



#### Lemma 2
Si tenemos que jugar un token face-down (es decir, no tenemos poder para cualquier juego de face-up pero al menos un punto), el uso de la * mayor* token no es peor.

Proof.
Token face-down da '+tokens[i]` power at the cost of `-1` point.
Dejar `x ≤ y` ser dos fichas restantes.
Después de jugar `y` tenemos al menos tanto poder como después de jugar `x` (`P + y ≥ P + x`).
Ambas acciones pierden exactamente un punto, por lo que el uso de 'y' sólo puede dejarnos con más poder, que sólo puede ayudar más tarde. ∎



#### Lemma 3
Durante la ejecución del algoritmo, a cada paso el conjunto de fichas que han **no** sido utilizados es un sufijo de la matriz ordenada.

Proof.
Inicialmente no se usan tokens.
El algoritmo sólo elimina las fichas de dos maneras:

* `tokens[l]` se retira moviendo `I` hacia adelante.
* `tokens[r]` se retira moviendo hacia atrás.

Así las fichas eliminadas son siempre contiguas desde el principio o desde el final, dejando un sufijo sin tocar `tokens[l ... r]`. ∎



#### Lemma 4
El algoritmo nunca pierde una secuencia óptima de movimientos.

Proof.
Asume una secuencia óptima `S` que produce la puntuación máxima.
Considere el primer paso donde `S` difiere del algoritmo codicioso.

*Si `S` juega un token boca arriba mientras que codicioso no*:
Greedy tiene suficiente poder (también jugaría) o no.
Si el codicioso no puede jugar ningún token facial, entonces el token en `S` debe ser *más caro* que `tokens[l]`. (por Lemma 1).
Replacing that token in `S` with the cheaper `tokens[l]` cannot reduce the score and only increases remaining power, contradicting optimizaity.

*Si `S` juega un token boca abajo mientras que codicioso no*:
Greedy sólo falla en jugar boca abajo cuando `score == 0`.
Cualquier movimiento boca abajo reduce la puntuación a negativo, que nunca es útil para alcanzar una puntuación final más alta, por lo que una solución óptima nunca jugaría un token boca abajo en esa situación.

Por lo tanto, a cada paso la elección codictiva es al menos tan buena como cualquier otra, y ninguna solución óptima puede lograr una puntuación más alta que el algoritmo codicioso. ∎



##### Theorem
`maxScore` devuelto por el algoritmo equivale a la puntuación máxima posible.

Proof.
Por Lemma 4 el algoritmo codicioso se puede transformar en una secuencia óptima que produce la misma o mayor puntuación.
El algoritmo registra la puntuación más grande vista durante la transformación, por lo que `maxScore` es al menos la puntuación óptima.
Por el contrario, el algoritmo nunca excede el verdadero óptimo porque cada paso es consistente con las reglas del problema.
Por lo tanto, la salida del algoritmo equivale a la óptima. ∎



----------------------------------------------------

### Complexity Analysis

*Sorting* – `O(n log n)` time, `O(n)` space (Python’s kind uses Timsort).
*Greedy loop* – cada ficha se procesa a la vez, `O(n)` tiempo, `O(1)` espacio adicional.

Total: **Time `O(n log n)`, Space `O(1)`** (ignoring input storage).

----------------------------------------------------

### Referencia Implementación (Python 3)

``python
de la importación Lista

Solución de clase:
bolsa de defOfTokens Score(self, tokens: List[int], power: int) - int:
tokens.sort() # ascending order
l, r = 0, len(tokens) - 1 # dos punteros
puntuación, mejor = 0, 0

mientras que l
si tokens[l] <= power: # play face‐up
power -= tokens[l]
l += 1
puntuación += 1
mejor = máximo (mejor, puntuación)
elif marcador 0: # play face-down
potencia += tokens[r]
r)= 1
puntuación:= 1
# No se quedan movimientos
descanso

mejor
`` `

La misma lógica se puede escribir en C++/Java con estructura idéntica de dos puntos; el código anterior sigue el algoritmo literal y contiene comentarios explicativos.

----------------------------------------------------

** Resultado**
La solución es óptima, simple de implementar, y funciona en el tiempo mínimo posible dada la necesidad de ordenar la entrada.