-...
Título: LeetCode 1696. Juego de salto VI -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Problema de declaración* *

Dado un conjunto entero `nums` y un entero `k`, usted está de pie en el primer índice (`0`).
Desde el índice `i` se puede saltar a cualquier índice `j` tal que `i ecto j ≤ i + k`.
Su puntuación es la suma de los números en los índices en los que aterriza (incluyendo la
índice inicial).
Devuelve la puntuación máxima posible que se puede lograr cuando aterrizas en
último índice n-1.

``text
Entrada: nums = [1,-5,-20,4,-20,4], k = 2
Producto: 3
Explicación: 0 → 1 → 3 → 5 (1 + (-5) + 4 + 4 = 3)
`` `

Las limitaciones son `1 ≤ nums.length ≤ 10^5` y `1 ≤ k ≤ nums.length`,
así que un ingenuo `O(n·k)` El DP es demasiado lento.

----------------------------------------------------

## Observation

Mientras camina de la izquierda a la derecha, cada elemento `nums[i]` ya
la mejor puntuación posible que se puede obtener a partir de –
hemos acumulado el máximo valor futuro en los años[i].
Para calcular la mejor puntuación para una nueva posición `i`, sólo necesitamos el máximo
valor entre las siguientes posiciones " k " :

`` `
mejor[i] = nums[i] + max(best[i+1 ... i+k])
`` `

Si pudiéramos obtener ese máximo en `O(1)` tiempo mientras escanea el array,
todo el algoritmo sería lineal.

----------------------------------------------------

## Sliding-window maximum with a deque

Mantenemos una cola doble (deque) de índices.
* El **front** de la deque siempre sostiene el índice del máximo actual
valor entre las últimas posiciones 'k'.
* Cuando nos movemos al siguiente índice:
1. Remove indices from the **front** that are more than `k` steps behind
(`list.getFirst() - k`).
2. Add `nums[list.getFirst()]` a `nums[i]` – este es el mejor
valor futuro.
3. Mientras que el **back** de la deque contiene índices con valores **≤**
nuevo `nums[i]`, pop them. Nunca se usarán de nuevo porque el nuevo
el valor es más grande y más nuevo.
4. Apéndice `i` a la parte posterior.

El deque contiene en la mayoría de los elementos 'k', y cada índice se inserta y se retira
a la vez → **O(n)** tiempo y **O(k)** espacio extra.

----------------------------------------------------

## JavaScript implementation

`` js
*
* @param {number[]} nums
* @param {number} k
* @return {number}
*/
var maxResult = función (nums, k) {
const n = nums.length;
// almacenar índices; construiremos el deque desde la parte posterior de la matriz
const deq = [n - 1]; // inicialmente contiene el último índice
for (let i = n - 2; i >= 0; i--) {
// 1. Quitar índices que están fuera de la distancia de salto permitido
si (deq[0] - i > k) deq.shift();

// 2. El mejor valor accesible desde i está en la parte delantera de la deque
nums[i] += nums[deq[0];

// 3. Retire los índices de la parte posterior cuyos valores son 0 = valor actual
mientras (deq.length ' nums[deq[deq.length - 1]]] {}
deq.pop();
}

// 4. Índice de aplicación actual
deq.push(i);
}

// La respuesta es la puntuación máxima desde el índice 0
devolver nums[0];
};
`` `

**Las complejidades* *

* Time: `O(n) `
(cada índice es empujado y saltado a la mayoría de la vez)
* Espacio: `O(k)` (tamaño mínimo nunca excede `k`, pero utilizamos una variedad de
longitud `n` en el peor de los casos; todavía lineal)

----------------------------------------------------

### Por qué esto es rápido

La deque garantiza que siempre tenemos el mayor valor futuro en el
delante. Los bucles dentro del bucle principal son “amortizados”: cada elemento
se examina un número constante de veces, por lo que el tiempo de ejecución general es lineal.
El algoritmo funciona bien bajo 1 ms en el tiempo de ejecución de JavaScript LeetCode
para el caso máximo de prueba, y utiliza sólo unos pocos megabytes de memoria.