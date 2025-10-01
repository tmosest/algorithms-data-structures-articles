-...
Título: LeetCode 3145. Buscar Productos de Elementos de Gran Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Explicación de la solución**

Para una consulta `l , r , m` tenemos que salida

`` `
big_nums[l] · big_nums[l+1] · ... · big_nums[r] (mod m)
`` `

`big_nums` es la lista de todos los números naturales escritos en orden creciente

`` `
big_nums[0] = 1, big_nums[1] = 2, big_nums[2] = 3, ...
big_nums[i] = i + 1
`` `

así que el producto requerido es el producto de todos los enteros de `l+1` a `r+1`
(inclusive) tomada modulo `m`.

----------------------------------------------------

##### 1. Observaciones

* `m` is at most `10^5`.
En cualquier secuencia de `m` enteros consecutivos hay un múltiple de `m`
(principio del agujero de Pigeon).
Por lo tanto, si la longitud del intervalo `r - l + 1` es **≥ m** el producto es un
múltiple de `m` y la respuesta es `0`.

* Cuando la longitud del intervalo es menor que `m` el producto contiene a
la mayoría de los factores `m‐1 (≤ 10^5)`.
Podemos calcular el producto directamente, cada factor modulo `m`, porque
el tamaño del bucle es en la mayoría de `10^5`.

----------------------------------------------------

##### 2. Algoritm
Para cada caso de prueba

`` `
len = r - l + 1
si len m → respuesta = 0
más
prod = 1 (mod m)
para mí de 0 a Len... 1
prod = prod * ((l + 1 + i) mod m) (mod m)
respuesta = prod
respuesta de salida
`` `

----------------------------------------------------

##### 3. Prueba de corrección

Demostramos que el algoritmo produce el valor correcto para cada consulta.

-...

##### Lemma 1
Si `len = r – l + 1 ≥ m` entonces
'big_nums[l] · big_nums[r] es divisible por `m`.

Proof.
`big_nums[i] = i + 1`.
El conjunto `{l+1, l+2, ..., r+1}` contiene `m` enteros consecutivos.
Entre los enteros consecutivos hay exactamente uno que es un múltiple
de `m`.
Por lo tanto el producto contiene este múltiple y es un múltiple de `m`,
por lo tanto congruente con el modulo `m`.



##### Lemma 2
Si 'len' m `' el algoritmo compute el bucle

`` `
prod = (l+1) · (l+2) · ... · (r+1) ) (mod m)
`` `

Proof.
El bucle se abre sobre `i = 0 ... len-1`.
En la iteración 'i' multiplica el producto actual por
`(l+1+i) mod m`.
Todas las operaciones se realizan modulo `m`, así que después de la última iteración
`prod` iguala el producto de todos los números de `l+1` a `r+1` tomado modulo
`m`. ∎



################################################################################################################################################################################################################################################################ Theorem
Para cada consulta `l , r , m` el algoritmo salidas

`` `
big_nums[l] · big_nums[l+1] · ... · big_nums[r] (mod m)
`` `

Proof.

* If `len ≥ m`*:
Por Lemma adultnbsp;1 el producto es un múltiple de `m`; el algoritmo produce
`0`, que equivale al modulo de valor deseado `m`.

*Si ‘len’
Por Lemma adultnbsp;2 el bucle calcula exactamente el producto de todos los factores
de `l+1` a `r+1` modulo `m`.
Este es el valor requerido. ∎



----------------------------------------------------

##### 4. Análisis de la complejidad

Para una consulta

* Si `len ≥ m` la respuesta se calcula en `O(1)`.
* De lo contrario, se realizan multiplicaciones `m-1 ≤ 10^5`,
cada `O(1)`.

Por lo tanto el tiempo por consulta es `O(min(len, m)) ≤ O(10^5)` y la memoria
el consumo es `O(1)`.

----------------------------------------------------

##### 5. Aplicación de la referencia (Python 3)

``python
importadores

def solve() - título Ninguno.
data = list(map(int, sys.stdin.read().split())))
t = data[0]
fuera =
p = 1
para _ en rango(t):
l, r, m = data[p:p+3]
p += 3
si m == # Todo es 0 modulo 1
out.append(0)
continuar

longitud = r - l + 1
si longitud >= m: # un múltiplo de m ocurre
out.append(0)
continuar

prod = 1 % m
inicio = l + 1
para i en rango(longitud):
prod = (prod * (estrella + i) % m) % m
out.append(prod)

sys.stdout.write("\n"join(map(str, out)))

si __name_ == "__main__":
solve()
`` `

El programa sigue exactamente el algoritmo probado correcto arriba y
se ajusta al formato de entrada / salida requerido.