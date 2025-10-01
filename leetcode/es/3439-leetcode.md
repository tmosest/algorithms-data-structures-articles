-...
Título: LeetCode 3439. Reuniones de reprogramación para el tiempo libre máximo Yo...
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Explicación de la solución**

Por cada caso de prueba que se nos da

* " n " - número de reuniones
* " k " , el administrador tiene que eliminar las reuniones " k "
* `m` – el día tiene longitud `m` (el tiempo es `0 ... m`)
* `n` intervalos `` [l i , r i ]` - `0 ≤ l i –
una reunión ocupa el segmento medio abierto `[l i , r i )`.

Todo el día es libre excepto los intervalos que permanecen.
El administrador podrá suprimir cualquier reunión " k " .
Después de la supresión de las reuniones restantes se pueden mover (su orden puede
ser cambiado) siempre y cuando todavía no se solapan y se quedan dentro
`[0, m)`.
Tenemos que encontrar la longitud máxima posible de un libre continuo
intervalo en el calendario resultante.



----------------------------------------------------

##### 1. Observaciones

`` `
Si todas las reuniones restantes se fusionan en un bloque continuo,
el tiempo libre es la longitud de la parte vacía que está fuera de este bloque.
`` `

Porque las reuniones pueden ser reordenadas,
el horario óptimo para las reuniones restantes es siempre poner
ellos juntos en un bloque (el arreglo más “ocho”).
Todos los demás arreglos sólo pueden ampliar la parte ocupada total y
por lo tanto nunca aumentar el intervalo libre.

Para un conjunto fijo de reuniones
(que `S` contenga `t ' reuniones después de clasificarse a tiempo de inicio)

`` `
bloque = [ min l en S , max r en S ]
longitud = max r – min l (parte ocupada)

la parte libre fuera de este bloque es
( m – longitud ) – ( longitud de la brecha entre
bloque y la reunión más cercana fuera
este bloque )
`` `

Cuando eliminamos las " reuniones " , todas las reuniones restantes son contiguas
segmento en la lista ordenada – de lo contrario podríamos eliminar algunas reuniones
dentro de este segmento y agrandar la parte libre.
Por lo tanto, las reuniones restantes son exactamente una ventana corredera de tamaño
'n-k' en la lista ordenada.



----------------------------------------------------

##### 2. Precomputación

`` `
intervalos – array de pares (l, r) ordenados por l
leftGap[i] – l[i] – r[i‐1] (gap between i‐1 and i)
rightGap[i] – l[i+1] – r[i] (gap between i and i+1)
`` `

`leftGap` y `rightGap` son `0` cuando el índice correspondiente no
existen.
De ellos construimos dos arrays ayudantes

`` `
prefMax[i] – máximo de leftGap [0 ... i] (mejor parte libre a la izquierda)
suffMax[i] – máximo de rightGap[i ... n-1] (mejor parte gratuita de la derecha)
`` `

Todos ellos están construidos en el tiempo `O(n)`.



----------------------------------------------------

##### 3. Ventana deslizante

Por una ventana que comienza en la posición " p " y contiene reuniones " nk "
(`p ... p + n-k – 1`) sabemos

`` `
blockLength = r[p + n-k – 1] – l[p] (parte ocupada)
leftFree = prefMax[p‐1] (gap a la izquierda de la ventana)
rightFree = suffMax[p + n-k] (gap a la derecha de la ventana)
`` `

El tiempo libre máximo alcanzable con esta ventana es

`` `
mejor = max( izquierda) Gratis , rightFree )
`` `

deslizamos la ventana a través de todas las posiciones 'n‐k+1` y guardamos el máximo
valor – esta es la respuesta para el caso de prueba.



----------------------------------------------------

##### 4. Prueba de corrección

Demostramos que el algoritmo imprime el tiempo libre máximo requerido.

-...

##### Lemma 1
Después de suprimir " reuniones " las reuniones restantes son contiguas
serie de sesiones en el orden de todas las sesiones.

Proof.

Suponga lo contrario – existe una reunión `A` fuera del resto
segmento que está estrictamente entre dos reuniones restantes " B " y " C "
en el orden ordenado.
Suprimir " B " en lugar de " A " .
El intervalo de " B " es menor o igual al intervalo de " A " en
términos de tiempo de inicio,
por lo tanto, la brecha entre `B ' y `C ' no es menor que la brecha entre
`A` y `C`.
En consecuencia, el tiempo libre obtenido por este nuevo conjunto de restantes
las reuniones son al menos tan grandes como la contradicción original. ∎



##### Lemma 2
Para un conjunto fijo de reuniones restantes el horario óptimo es
fusionar todos ellos en un bloque continuo.

Proof.

Tome cualquier calendario de las reuniones restantes que no sea un solo bloque.
Mueva las reuniones a la izquierda hasta que una reunión toque a su izquierda
vecino. La parte ocupada no crece, por lo tanto la parte libre
no encoger.
Repetir este paso para todas las reuniones produce exactamente un bloque,
por lo tanto un horario con por lo menos tan grande un intervalo libre. ∎



##### Lemma 3
Que las reuniones restantes formen una ventana `W` de longitud `t = n‐k`.
Que `lmin` y `rmax` sean respectivamente el comienzo más pequeño y el
mayor final entre todas las reuniones en `W`.
Que `gapL' sea la mayor brecha a la izquierda de `W`
(prefMax[p‐1]` en el algoritmo) y `gapR` la mayor brecha a la
derecho de `W` (`suffMax[p+t]`).
Entonces el intervalo máximo libre obtenible con esta ventana es igual
`max(gapL , gapR)`.

Proof.

El bloque que contiene todas las reuniones en `W` ocupa el segmento
`[lmin , rmax)` de longitud `len = rmax - lmin`.
El bloque puede ser desplazado dentro de las dos lagunas vecinas.
*Si el bloque comienza en la frontera izquierda de la brecha izquierda*,
la parte libre en su lado izquierdo es 'gapL'.
*Si termina en la frontera derecha de la brecha derecha*,
la parte libre en su lado derecho es 'gapR`.
Ninguna otra colocación puede aumentar a ambos lados, porque el bloque
no puede cruzar una reunión vecina.
Por lo tanto, el mejor tiempo libre posible para esta ventana es
`max(gapL , gapR)`. ∎



##### Lemma 4
Durante el paso de la ventana deslizante el algoritmo calcula
`max(gapL , gapR)` correctamente por cada ventana.

Proof.

Por una ventana que comienza en la posición `p`

`` `
prefMax[p‐1] = gapL (por definición de prefMax)
suffMax[p+t] = diferenciaR (por definición de suffMax)
`` `

El algoritmo evalúa `max(prefMax[p‐1], suffMax[p+t])`,
por lo tanto obtiene exactamente `max(gapL , gapR)` para esta ventana. ∎



################################################################################################################################################################################################################################################################ Theorem
Para cada caso de prueba el algoritmo produce la longitud máxima posible
of a continuous free interval after deleting `k` meetings.

Proof.

Por Lemma limitadanbsp;1 las reuniones restantes son una ventana contigua de
longitud `n-k` en la lista ordenada.
Por Lemma adultnbsp;2 podemos fusionarlos en un bloque.
Lemma curvanbsp;3 da el mejor intervalo libre para esa ventana en particular
y Lemma limitadanbsp;4 muestra que el algoritmo evalúa este valor.
Tomando el máximo sobre todas las ventanas posibles, el algoritmo
devuelve exactamente el óptimo. ∎



----------------------------------------------------

##### 5. Análisis de la complejidad

`` `
Intervalos de clasificación : O(n log n)
Edificio prefijo / matrizs de sufijo : O(n)
Ventana deslizante sobre todas las ventanas: O(n)
`` `

Por lo tanto, el tiempo de funcionamiento total para un caso de prueba es `O(n log n)`
y el consumo de memoria es `O(n)`.



----------------------------------------------------

##### 6. Aplicación de la referencia (Python 3)

``python
importadores
importador bisect

# -----------

def solve_one(n, k, m, intervalos):
# 1. ordenar por hora de inicio
intervalos.sort() # by l, r automaticamente
l = [iv[0] para iv en intervalos]
r = [iv[1] para iv en intervalos]

# 2. brechas prefijo - mayor brecha que termina en i
* n
para i en rango(1, n):
brecha = l[i] - r[i-1]
pref[i] = max(pref[i-1], gap)

# 3. brechas de sufijo - mayor brecha que comienza en i
* n
para i en rango(n-2, -1, -1):
brecha = l[i+1] - r[i]
suff[i] = max(suff[i+1], gap)

# 3. ventana corredera (remanente de reuniones)
t = n - k # número de reuniones que permanecen
mejor = 0
para p en rango(0, t + 1):
left_g = pref[p-1] if p  0 si no 0
right_g = suff[p + t] si p + t
mejor = max(best, left_g, right_g)
mejor

# -----------
def solve() - título Ninguno.
it = iter(sys.stdin.read().strip())
out_lines = []
Mientras Verdadero:
n = int(next(it)))
k = int(next(it)))
m = int(next(it)))
si n == 0 y k == 0 y m == 0:
descanso
intervalos = [(int(next(it)), int(next(it)))) para _ en rango(n)]
out_lines.append(str(solve_one(n, k, m, intervalos)))
sys.stdout.write("\n"join(out_lines))

# -----------
si __name_ == "__main__":
solve()
`` `

El programa sigue exactamente el algoritmo probado correcto arriba y
se ajusta al formato de entrada / salida requerido.