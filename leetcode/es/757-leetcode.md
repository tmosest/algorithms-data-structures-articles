-...
Título: LeetCode 757. Establecer el tamaño de la intersección al menos dos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Problema reiniciado* *

Dada una serie de intervalos enteros `intervalos[i] = [li , ri] `
encontrar el tamaño mínimo de un conjunto 'S' de enteros tal que cada intervalo
contiene al menos dos números de `S`.

----------------------------------------------------

## ¿Por qué funciona una estrategia avaricia?

1. Si procesamos un intervalo que termina primero, somos libres
seleccionar puntos que se encuentran cerca del *end* de ese intervalo.
2. Los puntos elegidos cerca del final de un intervalo son los más probables
dentro de todos los intervalos **más tarde** que comienzan después del actual.
3. Por lo tanto, cuando vamos de izquierda a derecha (después de clasificarnos al final),
podemos mantener sólo los dos puntos ** más grandes** que ya han sido
elegido; cualquier intervalo que comience antes del segundo punto más grande
ya está cubierto por al menos dos de esos puntos.

----------------------------------------------------

## Algorithm

`` `
1. Si el array de entrada está vacío → volver 0.

2. Ordenar intervalos por
• extremo creciente (interval[i][1])
• si los extremos son iguales, disminuyendo el inicio (por lo tanto el intervalo más largo
viene primero). Esto garantiza que procesamos lo más corto
posibles intervalos de finalización primero.

3. Iniciar un array `ans` (o sólo dos variables) que mantendrá
los puntos añadidos al conjunto de respuestas.
Agregue los dos números más grandes del primer intervalo:
ans = [interval[0][1] - 1 , intervalo[0][1]

4. Para cada intervalo restante [l, r] en el orden
let last = ans[-1] // mayor punto añadido
segundoLast= ans[-2] // segundo punto más grande añadido

• Si l <= segundoÚltimo: // ambos puntos están dentro del intervalo
nada que hacer

• Else if l <= last: // justamente un punto dentro
añadir r a ans

• Else: // ningún punto dentro
añadir r-1 y r a ans
(El caso especial l == último es manejado por la segunda rama
porque el primer punto ya satisface el intervalo.)

5. Devuelve la longitud de `ans'.
`` `

----------------------------------------------------

## Correctness sketch

Demostramos por inducción que después de procesar el primer *k*
intervalos el conjunto `ans` contiene el número mínimo posible de
puntos.

*Base* – Después del primer intervalo debemos elegir dos puntos.
Elegir `{r-1, r}` es óptimo: cualquier conjunto que cubra el primer intervalo
debe contener dos enteros dentro de él; colocar uno al final y
el otro inmediatamente antes del final maximiza la oportunidad de que
los próximos intervalos también contienen al menos uno de estos puntos.

* Paso de inducción* – Supongamos que la reclamación tiene los primeros intervalos *k-1*
y los dos puntos más grandes son el último y el segundo último.
Para el intervalo *k*-th `[l, r]` tenemos cuatro casos:

1. ** " l " último "** Ningún punto de 'ans' está en el intervalo, así que debemos
insertar dos puntos nuevos.
Picking `{r-1, r}` es óptimo por la misma razón que en la base
caso.

2. **`l == last`** - Exactamente un punto (`último') está en el intervalo,
así que se necesita un punto más. Añadiendo `r` da dos puntos dentro
`[l, r]`.

3. ** " l " segundo Last`** – El intervalo comienza después del segundo mayor
punto pero antes o en el punto más grande.
Sólo 'último' está dentro, por lo tanto un solo punto adicional
(`r`) es suficiente.

4. ** " l " = segundoLast "** - Tanto " como " segundo last " , se encuentran dentro del
intervalo, por lo tanto ya está satisfecho y no hay nuevos puntos
requerido.

En cada caso agregamos el número **minimal** de nuevos puntos que todavía
asegura que el intervalo actual tiene al menos dos elementos de `ans`.
Así, después de procesar el intervalo *k*-th, el conjunto sigue siendo mínimo.

Por inducción el conjunto final `ans' es de tamaño mínimo posible.

----------------------------------------------------

## Complexity

Silencio Silencio Silencio Silencio
Silencio----------------
TENIDOS intervalos de clasificación TENIDO `O(n log n)` TENIDO `O(n)` (o `O(log n)` para in-place sort) ANTE
Silencio Single scan Silencio `O(n)` Silencio `O(1)` adicional (o `O(n)` si mantiene la lista de puntos)

Total: ** `O(n log n)` tiempo, `O(n)` espacio auxiliar** (la lista de la lista de
puntos seleccionados se pueden omitir, dejando sólo unas pocas variables enteros).

----------------------------------------------------

## Reference implementation (Java)

``java
Clase Solución {
intersección pública SizeTwo(int[][] intervalos) {
int n = intervalos. longitud;
// 1. ordenar por fin ascendiendo, luego por comenzar descendiendo
Arrays.sort(intervalos, (a, b) - título {
si (a[1] == b[1]) retorno b[0] - a[0];
a[1] - b[1];
});

// 2. mantener sólo los dos últimos puntos elegidos
int last = intervalos[0][1]; // largest
int secondLast = intervalos[0][1] - 1; // segundo mayor
int count = 2;

para (int i = 1; i) {}
int l = intervalos[i][0];
int r = intervalos[i][1];

si (l <= secondLast) { // ya cubierto por 2 puntos
continuar;
} si (l <= last) {/ cubierto por un punto
cuenta++; // añadir uno más
Segundo último = último;
último = r;
} más { // no hay punto dentro
contar += 2; // añadir dos puntos nuevos
segundo último = r - 1;
último = r;
}
}
recuento de retorno;
}
}
`` `

La misma lógica funciona en cualquier idioma; las ideas clave son:

* ordenar al aumentar el final derecho,
* empezar con los dos mayores números del primer intervalo,
* para cada intervalo siguiente, compare su límite izquierdo con los dos mayores
números ya elegidos y añadir 0, 1, o 2 puntos nuevos en consecuencia.

Esto da el tamaño mínimo de un conjunto que tiene al menos dos elementos
en común con cada intervalo.