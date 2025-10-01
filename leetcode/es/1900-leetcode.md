-...
Título: LeetCode 1900. Las rondas más antiguas y más recientes donde los jugadores compiten -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Explicación de la solución**

Por cada caso de prueba que se nos da

* `N` - número de participantes en la ronda actual
* `P1 , P2` – posiciones de los dos jugadores en la ronda actual
(las posiciones son `1 ... N`, el jugador más izquierdo tiene la posición `1`)

En una ronda sucede lo siguiente

`` `
jugador 1 vs jugador N
jugador 2 vs jugador N-1
jugador 3 vs jugador N-2
...
`` `

El ganador de cada par (o el jugador medio único cuando `N` es extraño)
continúa hasta la siguiente ronda.
Los ganadores se colocan en una línea ** surtido por sus posiciones** (izquierda)
a la derecha) – el orden es completamente determinista, no depende de
que gana dentro de un par.

La tarea es determinar después de cuántas rondas se reúnen los dos jugadores
(primera vez).
La respuesta es la misma para lo mejor posible y para lo peor posible
situación – se define únicamente por los datos iniciales.



----------------------------------------------------

#### Observación 1
En una ronda los dos jugadores se reúnen **iff**

`` `
P1 + P2 = N + 1
`` `

porque el jugador en la posición `i` conoce al jugador en la posición `N-i+1`.

----------------------------------------------------

##### Observación 2
Después de una ronda las posiciones de los dos jugadores en la siguiente ronda pueden
ser computado **sin saber quién ganó**.

Dejar `M = (N + 1) / 2` - número de ganadores (división entero).

Para cualquier jugador en posición `x` en la ronda actual de la nueva posición en
la próxima ronda es

`` `
newPos = ceil(x / 2)
`` `

`ceil` se puede expresar con aritmética entero como

`` `
newPos = (x + 1) / 2 // división entero
`` `

Prueba de boceto:

* Para la parte izquierda del campo (`x ≤ N/2`) el ganador es el
`x`‐th ganador, por lo tanto su nuevo índice es `ceil(x/2)`.
* Para la parte derecha del campo (`x √≥ N/2`) el ganador es el
'N-x+1'-est ganador, pero después de ordenar a los ganadores el orden relativo
de los dos ganadores que vienen del mismo par se conserva,
por lo tanto el nuevo índice es también `ceil(x/2)`.
* Para el jugador medio cuando `N` es extraño (`x = (N+1)/2`) el mismo
fórmula da el nuevo índice correcto – termina en medio de
la próxima ronda.

Así las nuevas posiciones están completamente determinadas por la corriente
y el número actual de participantes.

----------------------------------------------------

#### Algorithm
Para cada caso de prueba

`` `
ronda = 1
mientras que cierto
si P1 + P2 == N + 1 // los dos jugadores se reúnen
respuesta = ronda
descanso
// de lo contrario ambos sobreviven a la siguiente ronda
P1 = (P1 + 1) / 2
P2 = (P2 + 1) / 2
N = (N + 1) / 2
round++
respuesta de salida
`` `

El bucle funciona en la mayoría de `log2(N)` tiempos, así que la complejidad es
`O(log N)` por caso de prueba.

----------------------------------------------------

#### Correctness Proof

Demostramos que el algoritmo produce la ronda en la que los dos jugadores
primera reunión.

-...

##### Lemma 1
Durante cada iteración del bucle las variables `P1` y `P2`
son las verdaderas posiciones de los dos jugadores en la ronda actual.

Proof.

* Inicialmente son las posiciones dadas – verdad.
* Supongamos que son correctos antes de una iteración.
Si no se conocieron, ambos sobrevivieron a la siguiente ronda.
Mediante observación limitadabsp;2 los actualizamos a
`P1 = (P1 + 1) / 2` y `P2 = (P2 + 1) / 2`.
Por la observación estos son exactamente sus posiciones en la siguiente
ronda.
Por lo tanto el invariante sostiene para la próxima iteración. ∎



##### Lemma 2
Cuando el bucle termina, el valor `respuesta` equivale a la primera ronda en
que los dos jugadores se encuentran.

Proof.

El bucle sólo se detiene cuando la condición `P1 + P2 == N + 1` sostiene.
Esta condición es equivalente a los dos jugadores
reunión en esa ronda.
Porque el bucle corre en orden creciente de `redo',
la primera vez que la condición se hace realidad es la primera ronda de reunión.
Así `respuesta' es el valor deseado. ∎



################################################################################################################################################################################################################################################################ Theorem
Para cada caso de prueba el algoritmo produce el número de rondas después
que los dos jugadores dados se encuentran por primera vez.

Proof.

Por Lemma adultnbsp;1 el bucle se detiene exactamente cuando los dos jugadores se reúnen.
Por Lemma adultnbsp;2 el número redondo registrado equivale a la primera reunión
ronda.
Por lo tanto, el número impreso es correcto. ∎



----------------------------------------------------

#### Complexity Analysis
Seamos el número inicial de participantes.

* Cada iteración reduce `N` al menos por un factor de dos
(`N ← (N+1)/2`), por lo que el bucle funciona `⌈log2 N⌉` veces.
* Todas las operaciones dentro del bucle son `O(1)`.

Por lo tanto

`` `
Hora : O(log N) por caso de prueba
Memoria: O(1)
`` `

----------------------------------------------------

#### Referencia Implementación (Go 1.17)

``go
paquete principal

importación (importación)
"bufio"
"Fmt"
"os"
)

func main() {}
en := bufio.NewReader(os.Stdin)
var T int
si _, err := fmt.Fscan(in, &T); err != Nil
Regreso
}
escritor := bufio.NewWriter(os.Stdout)
for ; T ⇩ 0; T-- {
var N, P1, P2 int64
si _, err := fmt.Fscan(in, &N, &P1, &P2); err != Nil
Regreso
}
round := int64(1)
por
si P1+P2 == N+1 {
fmt.Fprintln(writer, round)
descanso
}
// avance a la siguiente ronda
P1 = (P1 + 1) / 2
P2 = (P2 + 1) / 2
N = (N + 1) / 2
round++
}
}
escritor. Flush()
}
`` `

El programa sigue exactamente el algoritmo probado correcto arriba y
se ajusta a Go 1.17.