-...
Título: LeetCode 3346. Frecuencia máxima de un elemento después de realizar operaciones I -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Explicación de la solución**

Para cada caso de prueba

* `n` – número de amigos (`1 ≤ n ≤ 2·10^5`)
* `k` – distancia máxima que un amigo puede cambiar (`k` puede ser grande)
* `numOps` - número de operaciones que se pueden realizar
* `a[1 ... n]` – distancia del i‐th amigo de la estación

Durante una operación elegimos un amigo y cambiamos su distancia.
Después de todas las operaciones todas las distancias tienen que ser un entero.



----------------------------------------------------

##### 1. Observación – ¿qué significa “hacer un grupo”?

Todos los amigos que pertenecen a un grupo deben finalmente tener la misma distancia.
Para un grupo que se convertirá en el valor `

`` `
para cada amigo en el grupo : latitud imperoriginal – x habit ≤ k
`` `

De ahí que todas las distancias dentro del grupo deben estar dentro de un intervalo de
longitud `2k` (la diferencia entre el más pequeño y el más grande
distancia original en el grupo es a la mayoría `2k`).

Para un valor objetivo fijo `x` podemos elegir *cualquier subconjunto de amigos*
dentro de este intervalo – se nos permite dejar a algunos amigos sin cambios
y podemos cambiar sólo a los demás.

----------------------------------------------------

##### 2. Dos tipos de grupos óptimos

*1. El valor objetivo es una de las distancias iniciales*
Si el valor final ya está presente en la entrada, cada amigo cuyo
distancia difiere de este valor por lo más `k` se puede mover a él
(1 operación por amigo).
El tamaño de tal grupo es igual

`` `
número de amigos dentro [x – k , x + k] 1)
`` `

y necesitamos una operación para cada amigo que ya no es igual
x.

*2. El valor objetivo es **no** una distancia inicial*
La distancia objetivo puede ser cualquier entero.
Todos los amigos dentro de un intervalo de longitud `2k` se pueden mover a la misma
valor (1 operación por amigo que difiere de este valor).
El tamaño del grupo es

`` `
número de amigos dentro de algún intervalo de longitud 2k (2)
`` `

y podemos usar a lo más 'numOps' de estos amigos.

La respuesta final es la mayor de los mejores grupos de tipo (1) y
tipo (2).

----------------------------------------------------

##### 3. Cómo encontrar el mejor grupo de tipos (1)

Clasificar todas las distancias.
Por cada distancia distinta

`` `
cnt[v] = número de ocurrencias de v (pre-computados)
`` `

Que la matriz ordenada sea `b[0 ... n-1]`.

Para un `v' fijo necesitamos el número de elementos dentro
`[v - k , v + k]`.
Con dos punteros (una ventana corredera) podemos obtener esto en `O(n)`.

`` `
derecho – primer índice con b[right] > v + k (exclusivo)
izquierda – primer índice con b[left] ≥ v – k
total = derecha – izquierda (tamaño de la ventana)
`` `

`total - cnt[v]` amigos difieren de `v` y necesitan ser cambiados.
El tamaño máximo posible de un grupo que finalmente es igual a `v` es

`` `
cnt[v] + min(numOps , total – cnt[v] 3)
`` `

----------------------------------------------------

##### 4. Cómo encontrar el mejor grupo de tipos (2)

De nuevo con una ventana corredera buscamos el intervalo más largo
longitud 2k.
Ahora la ventana se define por

`` `
b[right] – b[left] ≤ 2k
`` `

El tamaño de la ventana es `derecha - izquierda + 1`.
El tamaño máximo de la ventana sobre todas las posiciones se almacena en
`maxWindow`.
El mejor grupo de tipo (2) tiene tamaño

`` `
min(numOps , maxWindow) (4)
`` `

----------------------------------------------------

##### 4. Prueba de corrección

Demostramos que el algoritmo descrito arriba produce el máximo
posible número de amigos que finalmente pueden tener la misma distancia.

-...

##### Lemma 1
Para una distancia fija `v` el algoritmo calcula exactamente el número de
amigos cuya distancia original se encuentra en el intervalo `[v – k , v + k]`.

Proof.

La matriz está ordenada.
`derecho ' se mueve hacia adelante mientras `b[derecha] ≤ v + k`.
Por lo tanto, cuando el bucle se detiene, `b [derecha]` es el primer elemento más grande
que `v + k`; todos los elementos anteriores pertenecen al intervalo.
Analogously `left ' is moved forward while `b[left] ' c ' ,
b [izquierda] es el primer elemento no menor que `v - k`.
All indices in `[left , right-1]` pertenecen a `[v - k , v + k]`,
ningún otro índice lo hace.
Así el tamaño de la ventana `derecha - izquierda' es exactamente el número de
amigos en ese intervalo. ∎



##### Lemma 2
Para una distancia fija `v` el valor calculado por la fórmula (3)
es el número máximo de amigos que se pueden mover a distancia `v`
en la mayoría de los años Operaciones.

Proof.

Todos los amigos dentro del intervalo `[v - k , v + k]` se puede mover a `v `
(1 operación por amigo que ya no está en `v`).
El número de tales amigos es total – cnt[v].
Podemos utilizar en la mayoría de los 'numOps' de ellos, por lo tanto el tamaño del grupo
no puede exceder el `cnt[v] + min(num Ops , total – cnt[v])`,
que es exactamente el valor (3).
Por otro lado, podemos lograr este tamaño moviéndonos
`min(numOps , total – cnt[v])` amigos a `v`.
Por lo tanto el valor (3) es óptimo para el objetivo `v`.



##### Lemma 3
`maxWindow` computed by the second sliding window is the maximum
posible número de amigos que pueden pertenecer a un grupo cuya final
distancia se encuentra dentro de un intervalo de longitud `2k`.

Proof.

Mientras el puntero derecho se mueve de izquierda a derecha,
el puntero izquierdo es siempre el índice más pequeño tal que
[b[right] – b[left] ≤ 2k`.
En consecuencia, la ventana `[izquierda, derecha]` siempre contiene todos los elementos
dentro de algún intervalo de longitud `2k` y ninguna ventana más grande terminando a
'derecho' es posible.
El algoritmo mantiene el tamaño de ventana más grande sobre todas las posiciones,
por lo tanto `maxWindow` es el número máximo de amigos que se pueden poner
en el mismo grupo utilizando una distancia final arbitraria. ∎



##### Lemma 4
El número óptimo de amigos que finalmente pueden tener la misma distancia
es `max( best_type1 , best_type2 )`,
Donde

`` `
best_type1 = max over all v of (cnt[v] + min(numOps , total(v)-cnt[v])
best_type2 = min(numOps , maxWindow)
`` `

Proof.

*Tipo (1)* grupos: por Lemma limitadanbsp;2 el mejor grupo para cada `v` es
exactamente el valor en (3).
Tomando el máximo sobre todos los rendimientos de la `v `best_type1`.

*Tipo (2)* grupos: por Lemma limitadanbsp;3 el grupo más grande posible dentro
cualquier intervalo de longitud `2k` contiene `maxWindow` amigos.
Sólo "numOps" de ellos se puede cambiar, por lo tanto el máximo alcanzable
tamaño es `min(numOps , maxWindow) = best_type2`.

Cualquier acuerdo final válido debe pertenecer a uno de los dos tipos,
por lo tanto el óptimo global es el mayor de los dos valores. ∎



################################################################################################################################################################################################################################################################ Theorem
El algoritmo produce el número máximo posible de amigos que pueden
ser movido a la misma distancia entero utilizando en la mayoría de operaciones 'numOps'.

Proof.

El algoritmo evalúa las dos expresiones derivadas en
Lemma limitadanbsp;4 y produce su máximo.
Por Lemma plaganbsp;4 este valor es exactamente el número óptimo de amigos
que puede compartir la misma distancia. ∎



----------------------------------------------------

##### 4. Análisis de la complejidad

`` `
Clasificación: O(n log n)
Dos ventanas correderas : O(n)
Consumo de memoria : O(n)
`` `

Con `n ≤ 2·10^5` el programa satisface fácilmente los límites.



----------------------------------------------------

##### 5. Aplicación de la referencia (Python 3)

``python
importadores
de las importaciones de colecciones Contrato

def solve() - título Ninguno.
data = sys.stdin.read().strip().split()
si no datos:
Regreso
iter(data)
n = int(next(it)))
k = int(next(it)))
num_ops = int(next(it))
a = [int(next(it))) for _ in range(n)]

a.sort()
cnt = Counter(a) # número de ocurrencias de cada valor

El mejor grupo con objetivo igual a una distancia inicial...
izquierda = 0
derecho = 0
mejor1 = 0
para v en set(a): # valores distintos
si la derecha se hizo a.index(v): # right is always ahead of left
derecha = a.index(v)
mientras que la derecha no se hizo y una [derecha]
derecho += 1
mientras que la izquierda no se hizo y un [izquierda]
izquierda += 1
total = derecha - número izquierdo de elementos en [v-k , v+k]
necesita = total - cnt[v] # amigos que ya no están en v
posible = cnt[v] + min(num_ops, need)
si es posible best1:
mejor1 = posible

El mejor grupo con el objetivo NO en las distancias iniciales...
izquierda = 0
max_window = 0
para derecho en rango(n):
a[right] - a[left] 2 * k:
izquierda += 1
ventana = derecha - izquierda + 1
si ventana max_window:
max_window = ventana
best2 = min(num_ops, max_window)

print(max(best1, best2))

si __name_ == "__main__":
solve()
`` `

El programa sigue exactamente el algoritmo probado correcto arriba
y se ajusta al formato de entrada/salida requerido.