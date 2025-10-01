-...
Título: LeetCode 1274. Número de naves en un rectángulo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Solution Overview**

Para cada caso de prueba se nos da

`` `
topRight = [x2 , y2]
bottomLeft = [x1 , y1]
`` `

`Sea.hasShips(topRight, bottomLeft)` devuelve **True** sif el rectángulo cerrado
`[x1 ... x2] × [y1 ... y2]` contiene por lo menos una nave.

Todo el mar puede contener en la mayoría de 10 barcos, el tamaño de la cuadrícula es tan grande como
`10^9 × 10^9` y podemos llamar `hasShips` en la mayoría de 100 veces.

El objetivo es contar todos los barcos en el rectángulo dado.



----------------------------------------------------

##### 1. Observaciones

* La respuesta es a la mayoría de 10 – la función puede parar tan pronto como todos los barcos
son encontrados.
* Nunca necesitamos inspeccionar un rectángulo que no contenga naves.
* Un rectángulo con una sola célula `[x, y] × [x, y]` es un barco sif
`hasShips([x, y] , [x, y])` es `True`.

Así podemos explorar sólo rectángulos que están garantizados para contener barcos.
Debido a que el número total de barcos es pequeño, la cantidad de trabajo es muy pequeña.



----------------------------------------------------

##### 2. Recursive Quadrant Search

Para un rectángulo no vacío lo dividimos en cuatro sub-rectángulos
(bottom‐left, top-left, bottom‐right, top-right) y
recurse a los sub-rectángulos que en realidad contienen barcos.

`` `
(x2 , y2) (x2 , y2)
Silencio
+----------+------------+ +----------+------------+
Silencio Silencio .
[x1 ... xm , y1 ... ym] [xm+1 ... x2 , y1 ... ym]
Silencio Silencio .
+----------+------------+ +----------+------------+
Silencio
(xm, ym) (x2 , y2)
`` `

* `mx = (x2 + x1) // 2`
`my = (y2 + y1) // 2`

Los cuatro cuadrantes son

Silencioso silencioso Silencioso Izquierda
Silencio----------------------------
TENIDO BL TENIDO `[mx, my]` Silencio `[x1 , y1]` Silencio
TENIDO TL TENIDO `[mx , y2]` TENIDO `[x1 , my+1]` Silencio
Silencio BR TENIDO `[x2 , my]` Silencio `[mx+1 , y1] Silencio
TENIDO TR ANTE `[x2 , y2] ' Silencio `[mx+1 , my+1] `` Silencio

Sólo recurrimos a un cuadrante si 'Sea.hasShips' para ese cuadrante
devuelve `True`.
Si el rectángulo es una sola célula retornamos `1` (un barco) – la llamada
a `hasShips` garantiza que un barco realmente existe en esa celda.



----------------------------------------------------

##### 2. Algoritm

`` `
conteo(rectángulo (tr , bl)):
si bl.
retorno 0
si no es mar.tieneShips(tr, bl):
retorno 0
si tr == bl:
Regreso 1

mx = (tr[0] + bl[0]) // 2
mi = (tr[1] + bl[1]) // 2

recuento([mx, my] , bl) + # BL
recuento([mx , tr[1]] , [bl[0], my+1]) + # TL
[mx+1 , bl[1]] + # BR
# TR
`` `

The public entry point `solve_case` simply calls `count` with the
dado rectángulo.



----------------------------------------------------

##### 3. Prueba de corrección

Demostramos que el algoritmo devuelve el número exacto de barcos en el
dado rectángulo.

-...

##### Lemma 1
Si `sea.hasShips(tr, bl)` es 'False' para un rectángulo,
el algoritmo nunca cuenta una nave dentro de este rectángulo.

Proof.
El algoritmo comprueba `hasShips` en el principio de `contra`.
Si devuelve `False` la función devuelve inmediatamente `0`.
Así que ninguna nave dentro de este rectángulo contribuye a la respuesta. ∎



##### Lemma 2
Para un rectángulo que es una sola célula `[x, y] × [x, y]`,
" retornos " `1` si hay un barco en `(x, y)`.

Proof.
Cuando el rectángulo es una sola célula el algoritmo alcanza el
base case `tr == bl`.
Devuelve `sea.hasShips(tr, bl)`, que es `True`
si la célula contiene un barco.
Si es `True` la función devuelve `1`, de lo contrario `0`. ∎



##### Lemma 3
Dejar `R` ser un rectángulo que contiene al menos una nave y es **no**
una sola celda.
`contra` devuelve la suma de los números de barcos en sus cuatro sub-rectángulos.

Proof.
Para tal `R' el algoritmo

1. computes the mid coordinates `mx, my`,
2. comprueba cada uno de los cuatro cuadrantes con `hasShips`.
Por Lemma adultnbsp;1 se ignoran los cuadrantes que no contienen nave.
3. Recursivamente llama 'cuenta' en cada cuadrante que contiene un barco.

Así cada nave en 'R' se encuentra en exactamente uno de los cuadrantes, y el
Las llamadas recursivas cuentan exactamente una vez.
Añadiendo los cuatro resultados recurrentes da el número total de barcos en
`R`.



################################################################################################################################################################################################################################################################ Theorem
Para cada caso de prueba el algoritmo devuelve el número exacto de barcos
dentro del rectángulo dado.

Proof.
Probamos por inducción sobre la profundidad de la recursión.

*Base:*
La recursión se detiene cuando el rectángulo es una sola célula.
Por Lemma adultnbsp;2 el valor devuelto es exactamente el número de barcos
en esa celda.

*Paso de inducción:*
Supongamos que para todos los rectángulos a la profundidad ` se hizo d` el algoritmo devuelve el
cuenta de la nave exacta.
Considere un rectángulo `R` a profundidad `d`.
Si `haships` es `False ' , por Lemma adultnbsp;1 la respuesta es `0`, que es
Correcto.
De lo contrario `R` contiene al menos una nave.
Si `R` es una sola célula estamos en el caso base.
De lo contrario nos dividimos 'R' en los cuatro cuadrantes y, por
El número total de barcos en `R` es la suma de los números
en los cuadrantes.
Cada cuadrante tiene profundidad " realizada " , por lo tanto por la hipótesis de inducción la
Las llamadas recursivas devuelven los recuentos correctos.
Añadiéndolos da la respuesta correcta para 'R'.

Por inducción el algoritmo es correcto para todos los rectángulos, incluyendo
la inicial. ∎



----------------------------------------------------

##### 4. Análisis de la complejidad

Que `k` sea el número de barcos que el algoritmo realmente visita
(`k ≤ 10`).

* Cada nave en el mar crea como máximo **4** llamadas recursivas
(uno para cada nivel de la división) hasta que se aísla a una sola célula.
Por lo tanto, el número de llamadas "Sea.hasShips" es
`≤ 4 * k + 1 ≤ 4 * 10 + 1 = 41`, que está muy por debajo del
permitido 100 llamadas.
* Cada llamada realiza una cantidad constante de trabajo (unas pocas entradas)
operaciones y una prueba de membresía en el set de barcos).
* La profundidad de recursión es en la mayoría de `⌈log2 109⌉ ♥ 30`, por lo que la recursión de Python
El límite no es un problema.

`` `
Tiempo : O(k) ≤ 40 operaciones por caso de prueba
Memoria : O(1) (sólo unos pocos enteros locales por nivel de recursión)
`` `

----------------------------------------------------

##### 5. Aplicación de la referencia (Python 3)

``python
importadores
de la importación Lista, Tuple

# ---------- Mar --------
Clase Mar:
"
El objeto del Mar simplemente mantiene un conjunto de posiciones de barco.
hasShips(tr, bl) returns Verdadero si alguna nave se encuentra en el rectángulo cerrado
definido por el fondo Izquierda 0 = coordenadas 0 = superior derecha.
"
def __init_(self, vessels: List[Tuple[int, int]):
# Los barcos se dan como una lista de tuples (x, y)
auto.ships = set(ships)

def hasShips(self, topRight: List[int], bottomLeft: List[int]) - título bool:
x2, y2 = superior Bien.
x1, y1 = fondo Izquierda
Para Sx, sígueme. barcos:
si x1 0 0 0 0 0 0 0 0 0 x2 y y 1 0 0 0 0 0 0 0 = 2
Retorno
Retorno Falso


# -------- Solver...
def count_ships_in_rectangle(sea: Sea,
topRight: List[int],
bottomLeft: List[int]) - Propiedad int:
"
Se divide el rectángulo en cuatro cuadrantes y cuenta barcos.
La función se detiene tan pronto como se encuentren todos los barcos.
"

def helper(tr: List[int], bl: List[int] int:
# vacío rectángulo
si bl[0] не tr[0] o bl[1].
retorno 0

# No hay nave en este rectángulo
si no es mar.tieneShips(tr, bl):
retorno 0

# Single cell
si tr == bl:
Regreso 1

# split into four sub-rectangles
mx = (tr[0] + bl[0]) // 2
mi = (tr[1] + bl[1]) // 2

# bottom‐left
cnt = helper([mx, my], bl)

# Top-left
cnt += helper([mx, tr[1]], [bl[0], my + 1])

# bottom-right
cnt += helper([tr[0], my], [mx + 1, bl[1]])

# Top-right
cnt += helper(tr, [mx + 1, my + 1])

retorno cnt

helper(topRight, bottomLeft)


# -------- Conductor principal...
def main() - título Ninguno.
data = list(map(int, sys.stdin.read().strip().split()))
si no datos:
Regreso
iter(data)
t = siguiente(it) # número de casos de prueba
out_lines = []

for case_no in range(1, t + 1):
x1 = next(it); y1 = next(it); x2 = next(it); y2 = next(it)
ship_x = next(it); ship_y = next(it)

# Generar la lista de naves según la especificación de entrada
# Cada posición de la nave es un solo punto (ship_x, ship_y)
mar = mar([(ship_x, ship_y)])

as = count_ships_in_rectangle(sea,
topRight=[x2, y2],
bottomLeft=[x1, y1])

out_lines.append(f)Case #{case_no}: {ans})

sys.stdout.write("\n"join(out_lines))


si __name_ == "__main__":
principal()
`` `

El programa sigue exactamente el algoritmo probado correcto arriba
y se ajusta al formato de entrada / salida requerido.