-...
Título: LeetCode 2176. Cuenta Parejas iguales y visibles en un Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**LeetCode 2176 – Conde Parejas iguales y visibles en un Array* *

■ **Task**
■ Por cada par de índices " (i , j) " ( " i " ) en `nums ' contar el par cuando
■ 1. `nums[i] == nums[j] `
■ 2. `i * j` is divisible by `k`.

Los únicos pares que necesitamos mirar son aquellos cuyos valores son los mismos.
Si dos índices apuntan a diferentes números el par nunca se puede contar, así que podemos saltar esas comparaciones.

-...

## Idea de alto nivel

1. ** Índices de crecimiento por valor** –
Escanee el array una vez, almacenando por cada valor los índices en los que aparece hasta ahora.
2. **Comprobar sólo pares dentro de cada grupo** –
Cuando encontramos el índice `i`, miramos atrás la lista de índices anteriores que contienen el mismo valor.
Para cada índice anterior `j` en esa lista, ponemos a prueba la condición de divisibilidad `i * j % k == 0`.
Si sostiene que aumentamos la respuesta.
3. **Añada el índice actual** –
Después de comprobar, empujamos `i` a la lista por su valor para que los índices futuros puedan emparejar con ella.

Esto es esencialmente el truco “hash‐map‐with‐position-lists”; convierte la ingenua `O(n2)` fuerza bruta en una construcción de un solo paso que todavía verifica cada par válido, pero nunca toca pares de valores diferentes.

-...

## Prueba de corrección

Demostramos que el algoritmo devuelve exactamente el número de pares válidos.

*Let* `pos[v]` ser la lista de índices que hemos visto hasta ahora cuyo elemento es `v`.

Cuando el bucle exterior está en el índice `i`:

* Por cada `j` en `pos[nums[i]]` comprobaremos el par `(j, i)`.
Porque " j " i " (sólo insertamos índices después de que los hayamos procesado),
esta pareja satisfice condición 2.
El algoritmo lo cuenta sif `nums[j] == nums[i]` (verdadero por construcción) y
`i * j % k == 0`, es decir, si satisface las tres condiciones.

* Todos los otros pares que podrían ser válidos son de la forma `(j, i)` donde `j  made i `
y `nums[j] == nums[i]`.
Estos son exactamente los pares enumerados en el bucle sobre `pos[nums[i].
Nunca se considera que ningún par con 'j' hechos i` y `nums[j]!= nums[i]`,
porque nunca sería insertado en `pos[nums[i].

Por lo tanto cada par contado satisface la declaración y cada par que satisface la declaración se cuenta exactamente una vez (la primera vez que se procesa su índice más grande).

∎

-...

## Complexity analysis

tención Technique TENIDO Tiempo TENIDO Espacio TENIDO Observaciones
Silencio----------------------------------------
tención Brute‐force anidado bucles TEN \(O(n^2)\) TEN \(O(1)\) TENCIÓN Comprobaciones innecesarias cuando muchos valores difieren. Silencio
TENIDO UNA BASQUE TENIDO \(O(n^2)\) peor maletín (todos los valores iguales) TENIDO \(O(n)\) ANTE En la práctica mucho más rápido porque sólo se inspeccionan los índices del mismo valor. Silencio

`n ≤ 2·105` en LeetCode, por lo que el enfoque basado en el mapa pasa cómodamente.

-...

## Aplicación de referencia (Python 3)

``python
de las colecciones importadas por defecto
de la importación Lista

Solución de clase:
def countPairs(self, nums: List[int], k: int) - título int:
# mapa del valor a la lista de índices vistos hasta ahora
pos = defaultdict(list)
ans = 0
para i, val en enumerate(nums):
# Mira hacia atrás índices anteriores con el mismo valor
para j in pos[val]:
si (i * j) % k == 0:
ans += 1
# índice de corriente récord para futuros pares
pos[val].append(i)
Retorno
`` `

El código sigue exactamente el algoritmo descrito anteriormente y se ejecuta en los límites requeridos.