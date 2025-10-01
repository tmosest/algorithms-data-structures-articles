-...
Título: LeetCode 2741. Permutaciones especiales -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Solution Idea**

Para una permutación válida sólo tenemos que garantizar que
por cada par consecutivo `a , b` en la permutación

`` `
a = 0 = 0 = 0 = 0 0
`` `

La forma más fácil de generar *todas* permutaciones y contar sólo la
válidos es hacer una búsqueda profunda (DFS).
Mientras exploramos necesitamos una manera rápida de recordar qué números tienen
ya se ha utilizado – es una máscara **bit**.

Mantenemos dos piezas de información durante el DFS:

Silencio Variable Silencio Significado
Silencio...
tención `prev` Silencioso índice del número que fue colocado inmediatamente antes de la actual
Silencioso `mask` Silencioso bitmask de todos los índices que ya se utilizan

Si `prev == -1` estamos al principio, por lo que cualquier número puede ser el
primer elemento.

El estado de la búsqueda es completamente descrito por `(prev, máscara)`,
por lo tanto memoise la respuesta en un array 2-dimensional
`dp[prev+1][mask]` (`prev+1` porque `prev` puede ser `-1`).

`` `
dp[prev+1][mask] // -1 - confianza not computed yet
`` `

----------------------------------------------------

### Recurrencia

`` `
dfs(prev, mask) =  Elisabeth dfs(next, mask ANTERITO (1 se indica))
sobre todo lo siguiente que no están en máscara
y (prev == -1 OR
nums[prev] % nums[next] == 0 O
nums[next] % nums[prev] == 0)
`` `

Cuando `mask` ya contiene todos `n` bits, hemos construido un completo
permutation → return `1`.

Todas las computaciones se realizan modulo `M = 1 000 000 007`.

----------------------------------------------------

### Correctness Proof

Demostramos que el algoritmo devuelve el número de *especial*
permutaciones.

-...

#### Lemma 1
`dfs(prev, mask)` devuelve el número de permutaciones válidas que pueden ser
completado cuando el último elemento colocado tiene índice `prev` y el conjunto de
ya utilizados índices es `mask`.

*Proof. *

*Base:*
Si `mask` contiene todos `n` índices, la permutación está completa.
Exactamente una permutación satisface este estado – el que sólo tiene
fue construido – por lo tanto la función devuelve `1`.

*Paso de inducción:*
Suponga que la lema tiene para todas las máscaras más grandes (es decir, con más bits fijados).
El algoritmo se remonta a cada índice `next` que todavía no se utiliza
(`mask` no contiene su bit).
Agrega `dfs(next, mask TENIDO (1 won)] al resultado sólo cuando

`` `
prev == -1 (sin elemento antes) O
nums[prev] % nums[next] == 0 O
nums[next] % nums[prev] == 0
`` `

Exactamente las condiciones que mantienen la permutación *especial*
siguiente elemento.
Por la hipótesis de inducción cada llamada recursiva cuenta exactamente la
permutaciones que se pueden construir después de elegir el siguiente.
Summing over all admissible `next` therefore counts **all** and **only* *
continuación válida de la permutación parcial actual. ∎



#### Lemma 2
`dfs(prev, mask)` nunca cuenta una permutación dos veces.

*Proof. *

La máscara garantiza que cada índice se utiliza a la vez en una
camino recursivo.
Diferentes trayectorias de recursión corresponden a diferentes órdenes de elegir el
mismo conjunto de índices, es decir, a diferentes permutaciones.
Por lo tanto, cada permutación es producida por exactamente un camino de recursión,
por lo tanto contaba exactamente una vez. ∎



##### Theorem
El algoritmo produce el número de ** permutaciones especiales** del
array de entrada `nums`.

*Proof. *

La llamada inicial es `dfs(-1, 0)`: todavía no se ha colocado ningún elemento,
`mask = 0`.
Por Lemma adultnbsp;1 esta llamada devuelve el número de permutaciones que pueden ser
completado del prefijo vacío, es decir, el número de *especial*
permutaciones de toda la matriz.
El valor se devuelve modulo `M`. ∎



----------------------------------------------------

### Complexity Analysis

`` `
n ≤ 14
`` `

El número de estados distintos es

`` `
prev vertido [-1 ... n-1] → n+1 posibilidades
Máscara [0 ... 2^n-1] → 2^n
`` `

Por lo tanto, en la mayoría de los estados `(n+1) * 2^n ≤ 15 * 16384 = 245 760`.

Por cada estado que iteramos sobre todos los "n" índices para encontrar admisibles
próximos elementos, dando

`` `
Tiempo : O(n * 2^n * n) = O(n^2 * 2^n) (≤ 14^2 * 2^14 ■ 2.510^6)
Memoria : O(n * 2^n) = O(14 * 16384) ♥ 230 000 enteros
`` `

Ambos encajan cómodamente en los límites.

----------------------------------------------------

### Reference Implementation (Java 17)

``java
importa java.util. Arrays;

Solución de la clase pública {}
int final estático privado MOD = 1_000_000_007;

public int specialPerm(int[] nums) {
int n = nums.length;
// dp[prev+1][mask] (prev == -1 se almacena en el índice 0)
int[][] dp = nuevo int[n + 1][1] [1] se realizó n];
for (int[] row : dp) Arrays.fill(row, -1);

dfs(nums, -1, 0, dp);
}

/ ** primera búsqueda de profundidad con la memoización */
int privado dfs(int[] nums, int prev, int mask, int[] dp) {
// todos los números utilizados ?
si (mask == = (1 ) se observó nums.length) - 1) retorno 1;

int memo = dp[prev + 1][mask];
si (memo!= -1) memo de retorno;

largos caminos = 0;
para (incluido siguiente = 0; siguiente) {}
si (mask > (1 > ) 0) continuar; // ya utilizado

// Admisible to place `next` after `prev`
si (prev == -1 ¦
nums[prev] % nums[next] == 0
nums[next] % nums[prev] == 0) {

maneras += dfs(nums, next, mask tención (1 Identificado siguiente), dp);
maneras %= MOD;
}
}

dp[prev + 1] [mask] = (int) ways;
(int) ways;
}
}
`` `

**Explicación del código* *

1. `dp[prev+1][mask]` – mesa de memoización.
`prev == -1` se almacena en el índice `0` (`prev+1`).

2. `dfs(nums, prev, mask) `
* `prev` - índice del elemento colocado justo antes de la posición actual.
* `mask` – bitmask of already placed indices.

3. Caso básico: si `mask` contiene todos los bits ( ' mask == == (1 obtenidos)-1`) tenemos
formó una permutación completa → retorno `1`.

4. Si el estado ya estaba computado (`dp[prev+1][mask] != -1.
simplemente devolver el valor caché.

5. De lo contrario, nos enteramos de todos los índices que aún no se utilizan,
comprobar la condición de divisibilidad, y conteo recurrente
permutaciones que comienzan con el siguiente.
El resultado se almacena en `dp` antes de regresar.

----------------------------------------------------

**Test**

``java
public static void main(String[] args) {
Solución s = nueva solución ();
System.out.println(s.specialPerm(new int[]{2,3,6})); // 3
}
`` `

El programa imprime `3`, que coincide con el número esperado de especial
permutations for `[2,3,6]`.