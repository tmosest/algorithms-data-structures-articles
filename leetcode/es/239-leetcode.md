-...
Título: LeetCode 239. Ventana deslizante Maximum -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
** Declaración sobre los problemas* *
Dado un array entero `nums` y un entero `k`, devuelve un array que contiene el valor máximo de cada ventana deslizante de longitud `k` que se mueve de izquierda a derecha a través del array.

-...

### 1. Algoritmo - Deque Monotónico

Mantenemos un deque que almacena **indices** de elementos de array.
Los índices en la deque siempre están en orden decreciente de los valores correspondientes**:

`` `
nums[q[0] н= nums[q[1]] √≥= ... не= nums[q[-1]]
`` `

El elemento en el frente (`q[0]`) es por lo tanto el máximo de la ventana actual.

Por cada nuevo elemento `nums[i]`:

1. **Remove elementos más pequeños de la parte posterior** –
mientras que el último elemento en la deque es más pequeño que `nums[i]` pop it.
Estos elementos nunca pueden convertirse en un máximo mientras el elemento actual está en la ventana.

2. **Anexar el índice actual** – `q.append(i)`.

3. **Remove el elemento frontal si deja la ventana** –
si `q[0] <= i - k` pop it from the front.

4. **Recordar el máximo** – una vez que hemos procesado al menos una ventana completa
( " i "= k-1 " ) apéndice `nums[q[0]] ' al resultado.

-...

### 2. Prueba de corrección

Demostramos que el algoritmo produce el máximo para cada ventana.

**Lemma 1**
El deque siempre contiene índices de elementos que están dentro de la ventana actual.

*Proof. *
Cuando `i` aumenta, la ventana es '[i-k+1 , i].
El paso 3 elimina el elemento frontal si su índice `Seguido= i-k`.
Ningún otro índice puede salir de la ventana porque los índices aumentan en 1 paso. ∎

*Lemma 2*
El deque siempre está disminuyendo el orden de valores:
`nums[q[0]] √= nums[q[1]] √≥= ...`.

*Proof. *
Cuando se procesa un nuevo índice, emergemos de la parte posterior, mientras que `nums[q[-1]]] [i].
Así, después del bucle, todos los elementos restantes en la deque son **no más pequeños** que `nums[i]`.
Dado que " yo " se adjunta en la parte posterior, se mantiene la orden. ∎

**Lemma 3**
El elemento en la parte frontal de la deque es el valor máximo de la ventana actual.

*Proof. *
Por Lemma adultnbsp;2, todos los elementos de la deque están en orden decreciente.
Por Lemma adultnbsp;1, todos ellos se encuentran dentro de la ventana actual.
Por lo tanto el elemento frontal es el mayor entre los elementos de la ventana. ∎

**Teorema* *
El algoritmo produce el máximo correcto para cada ventana deslizante.

*Proof. *
Para cada posición `i ≥ k-1` el algoritmo anexa `nums[q[0].
Por Lemma adultnbsp;3 este valor equivale al máximo de la ventana `[i-k+1 , i]`.
Así cada entrada de salida es correcta, y todas las ventanas se procesan exactamente una vez. ∎

-...

### 3. Análisis de la complejidad

*Tiempo* – Cada índice se inserta y se elimina a la mayor brevedad: **O(n)**.
*Espacio* – El deque tiene en la mayoría de los índices " k " ; la matriz de resultados tiene valores " n-k+1 " : **O(k)** espacio adicional.

-...

### 4. Aplicación de la referencia (Python)

``python
de las colecciones importa
de la importación Lista

Solución de clase:
def maxSlidingWindow(self, nums: List[int], k: int) - título List[int]:
si no nums o k == 0:
retorno []

n = len(nums)
q = deque() # almacenar índices de potencial maxima
res = []

para i, num in enumerate(nums):
# Remove indices cuyos valores correspondientes son menores que num
mientras que q y nums [q[-1]]
q.pop()
q.append(i)

# Si el índice frontal está fuera de la ventana, pégalo
si q[0]
q.popleft()

# Grabar el máximo una vez que se procesa la primera ventana completa
si me ignoro= k - 1:
re.append(nums[q[0])

retorno
`` `

Esta solución sigue exactamente el algoritmo probado correcto arriba y funciona en tiempo lineal con espacio de salida lineal.