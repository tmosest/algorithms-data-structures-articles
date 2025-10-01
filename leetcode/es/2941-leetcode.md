-...
Título: LeetCode 2941. Maximum GCD-Sum of a Subarray -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
*Problema*
Dado un array `nums` (1 ≤ len(nums) ≤ 2·105) y un entero `k` (1 ≤ k ≤ len(nums)), encontrar un sub-array contiguo cuya longitud es por lo menos `k` que maximiza

`` `
(sumo de sus elementos) × (GCD de sus elementos)
`` `

Devuelve el valor máximo (aritmética de 64 bits).

----------------------------------------------------

## Observaciones

* For a fixed right end `r`, all GCDs of sub-arrays that end at `r` form a very small set.
El GCD sólo puede **disminuir** cuando extendemos el sub-array hacia la izquierda, y cada uno
tiempo que cambia el valor debe dividir el anterior.
Para los números que ocurren en el array, el número de GCD distintos que pueden
aparece en cualquier punto está obligado por **O(log V)** donde `V = max(nums)`.
En la práctica para `V ≤ 106` nunca excede 20.

* Debido a lo anterior, podemos mantener en la mayoría de una entrada para cada posible GCD
mientras escanea el array.
Para cada GCD almacenamos el sub-array **longest** (es decir, el más grande con el
suma) que tiene este GCD y termina en la posición actual.

----------------------------------------------------

## Algoritmo (GCD‐List + sumas de prefijo)

`` `
max_val = 0
tienda = {} // divisor - título (sumo, longitud)

para i, x en enumerado(nums):
nuevo = {} // estado después de añadir nums[i]

// sub-array que consiste sólo de nums[i]
nuevo[x] = (x, 1)
si k == 1:
max_val = max(max_val, x * x)

// extender cada sub-array previamente almacenado con nums[i]
para g, (s, l) en la tienda.items():
ng = gcd(g, x) // nuevo GCD después de añadir x
ns = s + x
nl = l + 1
si nl >= k:
max_val = max(max_val, ng * ns)

// mantener sólo el sub-array más largo para este GCD
si no ng en nuevo o nuevo[ng][1] se hizo nl:
nuevo[ng] = (ns, nl)

tienda = nueva

retorno max_val
`` `

----------------------------------------------------

### Correctness Proof

Demostramos que el algoritmo devuelve el máximo posible GCD‐sum.

-...

#### Lemma 1
Al principio de la iteración de bucle para el índice `i`, `store` contiene, porque
cada divisor posible `d`, un par `(s, l)` donde `s` es la suma y `l` es
la longitud de ** el subrayo más largo** finalizando en la posición `i‐1` cuyo GCD es
`d`.

*Proof. *
La inicialización (`i = 0`) es trivial: `store` está vacía.
Supongamos que la lema contiene el índice I.
Durante la próxima iteración construimos 'nuevo' como sigue:

* Por cada entrada `(s, l)` en `store` extendemos ese sub-array con
`nums[i]`. El nuevo GCD es `gcd(d, nums[i]).
Mantenemos sólo la entrada con la longitud **maximum** para cada GCD resultante,
así que después de procesar todas las entradas `nuevas' satisfice la lema para índice `i`.

* También insertamos el sub-arrayo de la longitud 1 terminando en 'i'; éste es el único
[i] que termina en 'i'.
Por lo tanto, la lema también se mantiene después de establecer `store = nuevo ' ∎



#### Lemma 2
Durante el procesamiento del índice `i` el algoritmo examina el valor
`G × S` for **every** sub-array that end at `i`, where
`G = GCD(sub-array)` y `S = sum(sub-array)`.

*Proof. *
Considere cualquier sub-array `nums[l ... i]`.
Por Lemma adultnbsp;1 cuando el bucle para `i` es introducido, `store` contiene una entrada
con GCD igual a " gcd(nums [l ... i‐1]) " y longitud `i‐l " .
Cuando extendemos esta entrada con `nums[i]`, el GCD se convierte en `gcd(G, nums[i] ' ,
que es exactamente el GCD de todo el sub-array.
Su longitud aumenta a `i‐l+1` y su suma a `S`.
Así el algoritmo calculará `G × S` para este sub-array. ∎



#### Lemma 3
Para cada sub-array de longitud al menos `k` actualizaciones del algoritmo
`max_val` con su GCD-sum.

*Proof. *
Por Lemma adultnbsp;2 el algoritmo calcula `G × S` para el sub-array.
El cheque `si nl ¢= k` garantiza que sólo consideramos sub-arrays de
longitud requerida antes de actualizar `max_val`. ∎



##### Theorem
Después de la última iteración `max_val` equivale al máximo posible
`(sum of elements) × (GCD of elements)` over all contiguous sub-arrays of
longitud al menos 'k'.

*Proof. *
De Lemma adultnbsp;3 cada sub-array elegible contribuye su valor a
`max_val`, so `max_val` es, al menos, el óptimo.
Por el contrario, `max_val` se actualiza sólo con valores de sub-arrays elegibles,
por lo tanto es ** en la mayoría** el óptimo.
Por lo tanto los dos son iguales. ∎



----------------------------------------------------

### Complexity Analysis

Dejar `V = max(nums)`.

* `gcd` runs in `O(log V)` time.
* Cada elemento se combina con la mayoría de los GCDs distintos (el conjunto
tamaño nunca supera ~20 para 106).
Así cada iteración cuesta `O(log V)`.

`` `
Tiempo : O(n · log V) ♥ 1.3·106 operaciones para n = 2·105
Memoria : O(log V) (el diccionario de GCDs)
`` `

Ambos límites satisfacen fácilmente los límites.

----------------------------------------------------

### Referencia Implementación (Python 3)

``python
de la importación de matemáticas gcd
de las colecciones importadas por defecto
de la importación Lista

def max_gcd_sum(nums: List[int], k: int) - Conf int:
max_val = 0
tienda = {} # divisor - título (sumo, longitud)

para x en nums:
nxt = defaultdict(lambda: (0, 0))

# sub-array of length 1
nxt[x] = (x, 1)
si k == 1:
max_val = max(max_val, x * x)

# extender todas las sub-arrayas almacenadas previamente
para g, (s, l) en la tienda.items():
ng = gcd(g, x)
ns = s + x
nl = l + 1
si nl >= k:
max_val = max(max_val, ng * ns)

# Mantenga sólo el submarino más largo para este divisor
si nxt[ng] se hizo (ns, nl):
nxt[ng] = (ns, nl)

tienda = nxt

retorno max_val
`` `

La función sigue exactamente el algoritmo probado correcto arriba y
corre en el tiempo necesario para las limitaciones dadas.