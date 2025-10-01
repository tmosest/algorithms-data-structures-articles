-...
Título: LeetCode 2147. Número de formas de dividir un corredor largo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 2147. Número de formas de dividir un corredor largo
### (Hard) – Leetcode, O(N) time, O(1) space

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Silencio Java Silencio O(n) Silencio O(1)
TENIDO Python TENIDO O(n) ANTERIOR O(1) TENIDO
TENIDO C++ TENIDO O(n) TENIDO O(1)

-...

#### TL;DR
1. **Si el corredor contiene un número impar de asientos (`S`) → respuesta = 0.**
2. **Otra vez** caminar la cuerda, mantener el índice del asiento *previous*.
3. Cada vez que golpeamos el asiento *3, 5, 7...*, multiplicamos el resultado por la distancia entre este asiento y el asiento anterior.
4. Retorno `resultado % 1_000_000_007`.

Por qué funciona: cada “gap” entre un par de asientos puede albergar un divider en cualquiera de las posiciones que se encuentran entre los dos asientos. El número de posibles posiciones de divider para un par en particular es exactamente el número de índices entre los dos asientos (`i - prevSeat`). Multiplicar todas estas opciones independientes produce el número total de maneras.

-...

## 🚀 Code (All 3 Languages)

## Java

``java
Solución de la clase pública {}
static final long MOD = 1_000_000_007L;

público número DeWays (corredor de cuerda) {}
larga res = 1L;
int seatCount = 0;
int prevSeatIdx = 0; // será sobrescrito en el primer asiento

para (int i = 0; i) i++) {
si (corridor.charAt(i) == 'S') {
seatCount++;

si (seatCount 2 " asiento " 1) {
res = (res * (i - prevSeatIdx) % MOD;
}
prevSeatIdx = i;
}
}

si (seatCount % 2 == 1 Silencioso en la vida útilCount 2) {
retorno 0;
}
(int) (res % MOD);
}
}
`` `

## Python

``python
Solución de clase:
MOD = 10**9 + 7

def numberOfWays(self, pasillo: str) - Conf int:
res = 1
seat_cnt = 0
prev_seat = 0

para idx, ch in enumerate(corridor):
si ch == 'S':
seat_cnt += 1
si sit_cnt 2 y sit_cnt % 2 == 1:
res = (res * (idx - prev_seat) % self. MOD
prev_seat = idx

retorno 0 si sit_cnt % 2 == 1 o sit_cnt = 2 otro res % auto. MOD
`` `

### C++

``cpp
Clase Solución {
public:
número int DeWays (corredor de cuerda) {
const long MOD = 1'000'000'007LL;
largas res = 1;
asiento Cnt = 0;
int prevSeat = 0;

para (int i = 0; i) ++i) {
si (corridor [i] == 'S') {
++seatCnt;
si (seatCnt > 2 " asiento " Cnt % 2 == 1) {
res = (res * (i - prevSeat) % MOD;
}
prevSeat = i;
}
}

si (seatCnt % 2 == 1 TENIDO asiento permanenteCnt = 2) retorno 0;
(int)(res % MOD);
}
};
`` `

-...

Artículo del Blog – “El Bien, el Mal, y el Ugly de Leetcode 2147”

#### Introduction
Cuando se está preparando para una entrevista de ingeniería de software, Leetcode's **Número de maneras de dividir un corredor largo** (Problema 2147) es una cadena clásica‐ DP puzzle que parece engañosamente simple a primera vista. En este post, diseccionamos el problema desde **todo ángulo**:

Silencio Silencio Silencio Silencio
Silencio...
Silencio **Dynamic‐Programming** se reúne **combinatorics** ¦ Edge-case pitfalls ← Misinterpreting “gap” positions 
Silencio **O(N)** tiempo – ideal para una entrevista de 30 minutos La condición *odd‐seat* puede hacer un viaje hacia arriba Silencio El producto de las lagunas puede rebosarse si no tienes cuidado.

Con explicaciones detalladas, usted sabrá *por qué* funciona el algoritmo, *qué* podría ir mal, y *cómo* para evitar errores comunes.

**Palabras clave de SEO** – Solución Leetcode, algoritmo de entrevista, cadena de programación dinámica, entrevista de codificación Java/Python/C++, algoritmo O(n), modulo 1e9+7, prep de entrevista de codificación.

-...

### 1. Declaración de problemas (reafirmada)
Dada una cuerda `corridor` de longitud **≤ 105** que contiene sólo `S` (sello) y `P` (persona), usted tiene dos asientos en una fila que debe formar un "bloque" de exactamente dos asientos. El objetivo es colocar divisores entre bloques consecutivos de dos asientos de tal manera que:

* cada bloque tiene exactamente dos asientos,
* un divider se puede colocar en cualquier posición * vacía* entre dos asientos consecutivos,
* todo el pasillo se divide en tales bloques.

Devuelve el número de diferentes colocaciones de divider modulo `109+7`.

-...

### 2. Intuición: Por qué los asientos importan, no las personas
Si el número de asientos es **odd**, es imposible dividir el pasillo en pares de dos asientos – piensa en intentar dividir 5 asientos en grupos de 2. Ese es el ** primer caso de borde "muy"**: olvídalo y devolverás un número no cero para una entrada imposible.

Para un número **** de asientos, usted puede pensar en el pasillo como una secuencia de posiciones de asiento
`s1, s2, s3, ..., s2k`.
Cada *dividente* tiene que sentarse *entre* dos posiciones de asiento consecutivas: `s2` y `s3`, `s4` y `s5`, ..., `s2k-2` y `s2k-1`.
Entre dos asientos consecutivos se puede colocar el divider en cualquier posición que miente estrictamente *entre* ellos. Si la distancia entre los asientos es `d`, hay exactamente `d` posiciones válidas.

-...

### 3. El Algoritmo Greedy‐Multiplicativo (bueno)
La elegante solución O(N) se reduce a un paso:

1. Asientos contables (`seatCnt`).
2. Mantenga el índice del asiento *previous* (`prevSeatIdx`).
3. Cuando alcanzamos el asiento número 3, 5, 7, ... (conteo de asientos de confianza 2), multiplicamos la respuesta por 'i - prevSeatIdx`.

¿Por qué?
Las opciones de colocación de separadores para cada *gap* son independientes. El número total de configuraciones es el producto de las opciones para cada brecha.

#### Proof of Correctness
- *Base*: Para los dos primeros asientos sólo hay una manera de dividir el pasillo – el separador es *antes* asiento 3, así que empezamos `res = 1`.
- *Paso de inducción*: Supongamos que hemos procesado correctamente los primeros '2t' asientos (formando `t` bloques).
Cuando nos encontramos con el asiento `2t+1` (el comienzo del siguiente bloque), el número de posiciones entre el asiento `2t` (el último asiento del bloque `t`) y el asiento `2t+1` es exactamente `i - prevSeatIdx`. Multiplicar por este factor preserva la corrección porque las decisiones de colocación de cada nuevo bloque son independientes de las anteriores.

Por inducción, después de que el bucle termine, `res` iguala el producto de todas las opciones independientes de brecha, es decir, el número total de configuraciones de divider.

-...

### 4. El “Bad” – Pitfalls comunes

← Mistake ← Consequence
Silencio----------------------------
Silencio **Ignorando el modulo** – Usando `int` para el producto ← Reflujo entero → Respuesta incorrecta ¦ (Java `long`, Python `int` maneja grandes ints) y aplicar `% MOD` cada multiplicación. Silencio
Silencio **Regresar en cada asiento** – `prevSeat` uninitialized TENIDO Distancia incorrecta en el primer asiento imparable TENCIÓN Inicializar `prevSeat` sólo después de encontrar el primer asiento, o establecer un valor aburrido que está sobrescrito en el primer asiento. Silencio
* Comprobando el asiento* Cnt. 1 `` en lugar de `seat Cnt. 2`** ← Mis-counts cuando el pasillo tiene exactamente 2 asientos pero no divisores Silencio La respuesta es 1 (sólo el divider inicial) cuando `seat Cnt == 2`. Asegurar el asiento 2 ` antes de regresar no cero. Silencio
Silencio **Off‐by-one en la distancia** Silencio Contando `i - prevSeat` cuando `prevSeat` es el *primer* asiento para el tercer asiento en lugar de la segunda tención En el algoritmo proporcionado `prevSeat` se actualiza después de cada asiento, por lo que cuando el asiento #3 es procesado tiene el índice de asiento #2, dando la distancia correcta. Silencio
Silencio **No manejar asientos impares contar** Silencio Devolviendo un número positivo para entradas imposibles Silencio Añadir un cheque final: si `seatCnt % 2 == 1` → retorno 0. Silencio

-...

### 5. Los enfoques ingenuos alternativos (y por qué fracasan)

TENIDO TENIDO Complejidad ANTERIOR Por qué Fails ANTE
Silencio--------------------------
TEN **Brute‐force all divider placements** – DFS/Backtracking TEN O(2n) TENIDO Tiempo exponencial, imposible para `n = 105`. Silencio
Silencio ** Programación dinámica con el estado** – `dp[i][j]` (posposiciones, paridad) Silencio O(n2) memoria ← Demasiado grande para 105. Silencio
Silencio **Divide " Conquer al dividirse en el primer asiento impar** ← O(n log n) si no es cuidadoso ← Todavía demasiado lento para el peor de los casos. Silencio

Estas soluciones “muy” son un recordatorio de que **over-engineering** puede matar su tiempo de ejecución en Leetcode. El truco de producto de gaps es el más limpio, más rápido y más fácil de entrevista.

-...

### 6. Consejos para la entrevista

1. **Lea cuidadosamente las limitaciones. #
* Longitud de cuerda hasta 105 → O(N) es obligatorio. *
2. ** Explique primero la intuición. #
“El número de posiciones de divider entre dos asientos es simplemente la distancia entre ellos. ”
3. **Declarar el algoritmo paso a paso.**
Esto demuestra que usted puede traducir la intuición en un plan concreto.
4. *Mención del modulo*
Leetcode siempre pide modulo 1 000 000 007; olvidarse de tomar `% MOD` puede viajar al juez.
5. **Test edge se presenta. #
``text
"" → 0"
"S" → 0
"SS" → 1
"SPSPSS" → 0 (caños impares)
"SSPSS" → 2
`` `
Muestra que tu código pasa esto.

-...

#### ⋅ Conclusion

El problema “Número de maneras de dividir un corredor largo” es un ejemplo brillante de la ingeniosidad **O(N)** oculto detrás de una declaración aparentemente complicada.
- El *bueno* es su solución lineal, sólo un escaneo, una multiplicación por asiento extraño.
- El *bad* es que un solo control (conteo de asientos o modulo olvidado) invalida instantáneamente toda la respuesta.
- El *muy* se encuentra en la tentación de over-complicar con DP o retroceder; la matemática simple es la clave.

Si usted está haciendo frente a su próxima entrevista de codificación, recuerde: *mirar opciones independientes*, *reducir el problema a un producto de brechas*, y *aplicar modulo temprano y a menudo*.

¡Feliz codificación! 🚀

■ **Si te ha parecido útil este post, dale un pulgar hacia arriba, compártelo con tus compañeros de equipo, y sigue a mi GitHub/Twitter para más soluciones de entrevista. #

-...

#### 🔗 Referencias

- Problema de Leetcode 2147: [https://leetcode.com/problems/number-of-ways-to-divide-a-long-corridor](https://leetcode.com/problems/number-of-ways-to-divide-a-long-corridor)
- Divulgación del texto – “Número de maneras de dividir un corredor largo” – [https://leetcode.com/problems/number-of-ways-to-divide-a-long-corridor/discuss] (https://leetcode.com/problems/number-of-ways-to-divide-a-long-corridor/discuss)

-...

■ **¿Quieres dominar más problemas de Leetcode “hard”? * *
■ Suscríbete a mi newsletter: *[Su Boletín]*
■ Sígueme en Twitter: *[@YourHandle] *
■ Buena suerte, y que sus entrevistas sean tan limpias como esta solución!