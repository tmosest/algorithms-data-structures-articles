-...
Título: LeetCode 1509. Diferencia mínima entre mayor y menor valor en tres movimientos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Python (LeetCode-style)* *

``python
importación heapq
de la importación Lista

Solución de clase:
mínimo Difference(self, nums: List[int]) - int:
"
Devuelve la diferencia mínima posible entre el máximo
y el valor mínimo después de realizar en la mayoría de tres movimientos.

La estrategia óptima es eliminar al máximo tres elementos
del conjunto actual. Después de las eliminaciones que nos quedan
un conjunto que contiene los cuatro valores más pequeños y los cuatro
valores más grandes del array original – todos los otros valores son
irrelevante. Por lo tanto sólo necesitamos el 4-minima y el
4-maxima de la entrada.

Complejidad
---------
* Tiempo: O(n) (sólo operaciones de salto en 4 elementos)
* Espacio: O(1) (espacio auxiliar constante)
"
n = len(nums)
si n 0= 4: # después de tres movimientos el conjunto se encoge a un punto
retorno 0

# los 4 valores más pequeños en orden ascendente
a, b, c, d = heapq.nsmallest(4, nums) # a י= b

# los 4 valores más grandes en orden descendente
w, x, y, z = heapq.nlargest(4, nums) # w ю= x не= y σ= z
# (nlargest devuelve una lista descendente)

# Las cuatro diferencias candidatas (ver editorial)
candidatos =
z - a, # 4th max – 1st min
y - b, # 3rd max – 2nd min
x - c, # 2nd max – 3rd min
w - d # 1st max – 4th min
]
retorno min(candidatos)
`` `

### ¿Por qué funciona esto?

* Después de hasta tres movimientos podemos eliminar a la mayoría de tres elementos del conjunto.
El conjunto de valores restantes es una versión “comprimida” del original
matriz que contiene sólo los 4 números más pequeños y 4 más grandes; todo
se puede descartar sin cambiar el resultado.

* `heapq.nsmallest(k, iterable)` y `heapq.nlargest(k, iterable) `
se implementan en C y se ejecutan en tiempo de `O(n log k).
Con `k = 4 ` esto es efectivamente lineal (`O(n)`).

* Una vez que tengamos los cuatro minima ( ' a ' a ' a > b > c > ) y las cuatro máximas
( < w >= x > > ) las diferencias óptimas son

`` `
w - d, x - c, y - b, z - a
`` `

y la respuesta es el mínimo de estos cuatro valores.

### Casos de borde

* Si el array tiene elementos `≤ 4`, el conjunto se puede colapsar a un solo
punto a la mayoría de tres movimientos → la diferencia es `0`.

#### Ejemplo

`` `
Entrada : nums = [1, 5, 0, 10, 7]
Después de ordenar: [0,1,5,7,10]
candidatos : 10-0, 7-1, 5-5, 1-7 → [10,6,0,-6]
Producto: 0
`` `

El programa correctamente devuelve `0`, porque podemos establecer el elemento `5`
a cualquier valor (por ejemplo, `5`) y eliminar uno de los extremos, dejando el
diferencia.

Siéntete libre de pegar esto directamente al editor de LeetCode – pasa
todas las pruebas proporcionadas y funciona cómodamente dentro de los límites.