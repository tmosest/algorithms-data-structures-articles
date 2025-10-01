-...
Título: LeetCode 3555. Subarray más pequeño para ordenar en cada ventana deslizante -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Python – Extremada solución “sort-and-compare”* *
*La complejidad del tiempo:* `O(n−k+1) · k log k) `
* Complejidad del espacio:* `O(k)`

La idea es simple:

1. Por cada ventana corredera de longitud `k` tomar el sub-array `sub`.
2. Ordenar una copia de esa sub-array (`sorted_sub`).
3. Escanee los dos arrays simultáneamente.
*Si un elemento de `sub` es diferente del elemento en el mismo índice
`sorted_sub`, esa posición es “fuera de lugar”. *
El bloque contiguo más pequeño que contiene todas las posiciones fuera de lugar
es exactamente el bloque que debe ser arreglado para hacer la ventana entera ordenada.

La longitud de ese bloque es `derecha - izquierda + 1`.
Si la ventana ya está ordenada, `izquierda ' nunca se mueve de ``∞` y regresamos `0`.

``python
de la importación Lista

Solución de clase:
def minSubarray Ordenar (self, nums: List[int], k: int) - List[int]:
n = len(nums)
ans = []

# deslizarse sobre todas las ventanas de longitud k
para i en rango(n - k +1):
sub = nums[i:i + k]
ordenados_sub = ordenados(sub) # su versión ordenada

izquierda, derecha = k, -1 # almacenar min y max índices desajustados

# encontrar las posiciones más izquierdas y más desajustadas
para j en rango(k):
si sub[j]!= [j]:
izquierda = min (izquierda, j)
derecha = max(right, j)

# Si no se encontraron desajustes, la ventana ya está ordenada
si es correcto -1: No hay desajustes
ans.append(0)
más:
ans.append(derecha - izquierda + 1)

Retorno
`` `

### Cómo funciona
* Para cada ventana tenemos el orden “currente” (`sub`) y el orden “desirado”
(`sorted_sub`).
* Cada índice donde difieren es un lugar que no está en lo correcto
posición relativa en la ventana.
* El subrayo más pequeño que contiene todos estos índices es precisamente el
segmento que tiene que ser resuelto.
Su longitud es `derecha - izquierda + 1`.
Si la ventana ya está ordenada, no hay índices diferentes, y volvemos `0`.

La solución es fácil de entender, implementa la idea central directamente,
y es lo suficientemente rápido para las limitaciones típicas de LeetCode.