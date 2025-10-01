-...
Título: LeetCode 1977. Número de formas de separar números -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Explicación de la solución**

Para la cuerda `num` tenemos que dividirla en uno o más enteros.
Todos los enteros deben

* no contiene ceros principales
(`"012"` no está permitido, `"0"` solo no está permitido)
* be **non-decreasing** from left to right

Los números pueden ser arbitrariamente grandes – por ejemplo la entrada
`"123456789123456789123456789" contiene un entero de 27 dígitos que hace
no encaja en un entero de 64 bits.

----------------------------------------------------

##### 1. Comparación de dos números de longitud igual

Mientras nos dividimos a menudo tenemos que decidir si

`` `
num[i .. i+len-1] י= num[j .. j+len-1] (los dos subestrings tienen la misma longitud)
`` `

Si convertimos cada subestring a un 'BigInteger' la comparación
el costo es `O(len)` y toda la programación dinámica se convertiría en
`O(n3)` – demasiado lento para `n ≤ 500`.

En su lugar, nosotros **pre-computamos un rango para cada subestring de una longitud fija**.
El rango es un entero que es

`` `
[i][len-1] = la posición de la subestring
empezando en el i y teniendo longitud
en la lista ordenada de todas las subestrings de esa longitud
`` `

Si dos subestrings tienen la misma longitud, entonces

`` `
num[i .. i+len-1]
rango[i][len-1] [j] [len-1]
`` `

Así podemos comparar números de igual longitud en `O(1)` tiempo
después de que se haya construido la mesa.

----------------------------------------------------

##### 2. Construcción de todas las filas – clasificación de cubos

Para una longitud fija `len` sólo necesitamos ver el *len‐th* dígito
de cada posición inicial posible.
Debido a que los dígitos son sólo `0 ... 9`, podemos cubo todos empezando
posiciones por ese dígito – esto requiere trabajo por grupo.

La construcción procede longitud por longitud:

`` `
grupos = [ todas las posiciones iniciales] 0 ... n-1

para lino = 1 ... n
nuevo Grupos = lista vacía
para cada grupo en grupos
cubo[0] 9] = listas vacías
para cada posición p en grupo
idx = p + len - 1
si idx
dígito = num[idx]
cubo[digit].add(p)
apéndice todos los cubos no vacíos a nuevosGroups

// asignar filas consecutivas
rankIndex = 0
para grupo en nuevosGroups
para la posición p en grupo
[p][len-1] = rankIndex
rankIndex++

grupos = nuevosGrupos
`` `

El algoritmo visita cada par `(posición, longitud)` una vez,
por lo que es `O(n2) ` tiempo y `O(n2) ` memoria.

----------------------------------------------------

##### 3. Programación dinámica

Vamos.

`` `
dp[i][len-1] = número de divisiones válidas de
el sufijo num[i ... n-1]
donde el primer entero (que comienza en i)
tiene al menos dígitos de limón (es decir, su longitud ≥ lino)
`` `

La respuesta que finalmente necesitamos es `dp[0][1]. –
el número de divisiones de toda la cadena con el primer entero
teniendo al menos un dígito.

**Transición* *

Para un índice de inicio fijo `i' y una longitud mínima fija `len`

`` `
1) El primer entero puede ser más largo que el len.
Todas esas posibilidades se cuentan en dp[i][len] = dp[i][len+1].

2) El primer entero puede tener exactamente dígitos de lente.
Entonces el siguiente entero debe tener la misma longitud o más,
pero para la prueba de igualdad sólo comparamos la misma longitud.

j = i + len // posición del siguiente entero
si j + len י= n // el segundo entero de la misma longitud existe
si el rango[i][len-1]
dp[i][len] += dp[j][len] // segundo entero tiene la misma longitud
más
si j + lino + 1
dp[i][len] += dp[j][len+1] // segundo entero es más largo
`` `

La recurrencia utiliza sólo valores que ya están computados
(porque iteramos 'i' de derecha a izquierda), por lo tanto todo el DP
es `O(n2)`.

----------------------------------------------------

##### 4. Prueba de corrección

Demostramos que el algoritmo devuelve el número requerido de divisiones.

-...

##### Lemma 1
Para cualquier posición inicial `a, b` y longitud `len' que ambos existen,
`num[a .. a+len-1] <= num[b .. b+len-1] `
iff `rank[a][len-1] [b][len-1].

Proof.

Durante la construcción de filas para este 'le' fijo todas las subestrings
de esa longitud se dividen en cubos por el primer dígito
(`0 ... 9`).
Después de eso, los grupos son reemplazados por los cubos, por lo que el relativo
orden dentro de un cubo iguala el orden de las subestrings
con ese primer dígito.
Este proceso se repite para el segundo dígito, tercer dígito, ...
Consecuentemente, después de que todo el bucle de 'len' termine,
la concatenación de todos los cubos finales es la lista de todos
subestrings de esa longitud ordenados en orden numérico ascendente.
Por lo tanto, los números consecutivos que asignamos como rangos son exactamente
las posiciones ordenadas. ∎



##### Lemma 2
`dp[i][len]` equivale al número de divisiones válidas del sufijo
`num[i ... n-1]` donde el primer entero tiene por lo menos dígitos 'L'.

Proof.

Demostramos por inducción inversa sobre " i " (a partir de " n-1 " ).

*Base.*
Si el sufijo tiene sólo una posición (`i = n-1`),
la única división posible es el dígito único `num[i]`.
El bucle establece `dp[i][len] = 1` para el máximo `len` (`len = 1`)
y para todos los `le' más pequeños utiliza la recurrencia:
`dp[i][len] = dp[i][len+1] = 1`.
Así la lema sostiene.

* Paso de inducción. *
Supongamos que la lema es válida para todos los índices ``.
Para un `L' fijo, la recurrencia del DP considera

1. **Primero entero más largo que `len`.**
Todas esas divisiones se cuentan en `dp[i][len+1]`. por el
Hipótesis de inducción.

2. **Primero entero exactamente 'le' dígitos. #
El siguiente entero debe ser de longitud al menos 'le'.
* Si el siguiente entero tiene exactamente dígitos 'L',
debe ser **no menor** que el primer entero.
Por Lemma adultnbsp;1 esto equivale a
`rank[i][len-1] ' = rank[j][len-1] ' Donde `j = i+len`.
Si esto sostiene, todas las divisiones del sufijo restante comienzan
a `j` con la primera longitud de entero `len` se añaden:
`dp[j][len]`.
* De lo contrario el segundo entero es más largo,
que es contado por `dp[j][len+1]` (de nuevo por inducción).

Todas las posibilidades están desvinculadas y cubren todas las divisiones válidas de las
Sufijo.
Por lo tanto `dp[i][len]` cuenta exactamente el número requerido de divisiones.
∎



################################################################################################################################################################################################################################################################ Theorem
El algoritmo produce el número de maneras de dividir toda la cadena
no disminuir los números enteros sin ceros líderes.

Proof.

La respuesta que producimos es `dp[0][1]. –
divisiones de toda la cadena (`i = 0`) donde el primer entero
tiene al menos un dígito.
Por Lemma adultnbsp;2 este es precisamente el número de divisiones válidas.
Todas las operaciones se realizan modulo `1 000 000 007`,
por lo que el valor devuelto es el resto requerido. ∎



----------------------------------------------------

##### 4. Análisis de la complejidad

`` `
construcción de todas las filas : O(n2) tiempo, O(n2) memoria
programación dinámica : O(n2) tiempo, memoria O(n2)
`` `

Para 'n ≤ 500' esto está muy por debajo de los límites.



----------------------------------------------------

##### 5. Aplicación de las referencias (Kotlin 1.6)

``kotlin
importa java.io. BufferedReader
importa java.io. InputStreamReader
importa java.util. ArrayList
importar java.util.StringTokenizer

const privado val MOD = 1_000_000_007L

fun main() {}
val num = readLine()!.trim()
val n = num.length
intArray(n) { num[it] - '0' }

/* ---------- *
// rank[i][len-1] – position of substring i.i+len-1
val rank = Array(n) { IntArray(n - it) } // n-i entradas por fila

// cubo ordenar para todas las longitudes
var grupos: Lista hechaArrayList seleccionadaInt hilo = mutableListOf()
grupos = ArrayList(0 hasta n).toList()) // todas las posiciones de inicio

para (en 1..n) {}
val newGroups = mutableListOf madeArrayList madeIntю()
para (grupo en grupos) {
val cubos = Array(10) { ArrayList
para (p en grupo) {
val idx = p + len - 1
si
val d = dígitos[idx]
cubos[d].add(p)
}
}
para (b en cubos) si (b.isNotEmpty()) nuevoGroups.add(b)
}
var rankIndex = 0
(Grp in newGroups) {
(p en grp) rank[p][len - 1] = rankIndex
rankIndex++
}
grupos = nuevosGrupos
}

--------- programación dinámica -------
// dp[i][len-1] – número de divisiones de sufijo i.n-1
// con primer número entero que tiene al menos dígitos de lente
val dp = Array(n) { LongArray(n - it) }

para (i in n - 1 down A 0) {
si (digits[i] == 0) continuar // números no pueden comenzar con 0
val maxLen = n - i
para (lenix en maxLen - 1 downTo 0) {
val len = lenídx + 1
si (Ledx) se hizo maxLen - 1) {
var ways = dp[i][lenIdx + 1] // first integer longer
val j = i + len
si (j + len = n) { // segundo entero la misma longitud existe
si (rank[i] [lenIdx] [j] [lenIdx]
maneras += dp[j][lenIdx]
. ♫ ... {
si (j + lino + 1 0 = n) {
maneras += dp[j][lenIdx + 1]
}
}
}
dp[i][lenIdx] = maneras % MOD
} más { / / última longitud posible
dp[i][lenIdx] = 1L
}
}
}

respuesta val = dp[0][0] % MOD
println(answer.toInt())
}
`` `

El programa sigue exactamente el algoritmo probado correcto arriba
y es totalmente compatible con Kotlin 1.6.