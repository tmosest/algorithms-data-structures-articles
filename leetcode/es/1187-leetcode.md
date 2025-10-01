-...
Título: LeetCode 1187. Hacer Array Strictly Increasing -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Hacer Array Strictly Increasing - A Complete Solution Guide

** Declaración sobre los problemas* *
Se les da dos arrays enteros `arr1` y `arr2`.
En una operación se puede elegir un índice `i` en `arr1` y un índice `j` en `arr2` y sustituir `arr1[i]` por `arr2[j]`.
`arr2` no se modifica – se puede elegir el mismo elemento de `arr2` muchas veces.
El objetivo es hacer que el " arrr1 " aumente estrictamente ( " arrr1[i+1] " , utilizando el número mínimo de operaciones.
Devuelve ese número mínimo, o `-1' si es imposible.

-...

## 1. Observaciones clave

1. **Podemos parar temprano** – si los primeros pocos elementos de `arr1` ya están aumentando estrictamente, tal vez no necesitemos tocarlos.
2. **Bound on the number of swaps** – each operation changes one element of `arr1`.
Nunca necesitamos más de operaciones de `len(arr1)` (cada elemento podría ser reemplazado una vez).
Además, si sustituyemos a más de elementos `len(arr2)`, los swaps "extra" son inútiles porque lo único que importa es el valor * que ponemos, no el índice en `arr2`.
Así la respuesta está ligada por `min(len(arr1), len(arr2))`.
3. **Elegir el valor adecuado de `arr2`** –
Si decidimos sustituir `arr1[i]`, quisiéramos poner el valor *smallest* de `arr2` que es aún mayor que el último valor del prefijo creciente.
Puesto que `arr2` no cambia, podemos ordenarlo una vez y utilizar la búsqueda binaria (`superior()`) para encontrar ese valor rápidamente.

-...

## 2. Formulación de programación dinámica

Utilizamos la siguiente tabla DP (o una versión unidimensional de ella):

`` `
dp[k] = el valor más pequeño posible del último elemento
de arrr1[0 ... cur] después de procesar los primeros elementos cur+1
y utilizado exactamente k swaps en total
`` `

" dp[k] " es " INF " si es imposible obtener un prefijo creciente con swaps exactamente " k " .

**Recurrencia** (mientras iterating over `arr1`):

*Sea el valor del último elemento del prefijo antes de la posición actual. *

1. **No cambie el elemento actual* *
Si `arr1[i] не prev`, podemos mantener `arr1[i]`.
Entonces el último valor del nuevo prefijo es `arr1[i]` y el número de swaps se mantiene `k`:

`` `
new_dp[k] = min( new_dp[k] , arr1[i] )
`` `

2. **Intercambiar el elemento actual** (sólo si `k ' 0 ' )
Necesitamos el elemento más pequeño de `arr2` que es mayor que el último valor del prefijo anterior, es decir, más grande que `dp[k-1]`. (el último valor *antes* usamos el intercambio de `k`‐th).
Utilice la búsqueda binaria en el orden `arr2` para obtener ese valor `x`.
Si existe tal `x':

`` `
new_dp[k] = min( new_dp[k] , x )
`` `

Debido a que siempre conservamos el *smallest* posible último valor, las posiciones posteriores tienen la mejor oportunidad de seguir aumentando.

-...

#### 2.1

Cuando hemos procesado sólo el primer elemento `arr1[0]`:

`` `
dp[0] = arr1[0] (sin swap)
dp[k] (k confía0) = min( arr1[0] , elemento más pequeño en arr2 )
`` `

La segunda línea dice: si ya cambiamos al menos una vez antes del primer elemento,
podemos guardar el valor original o poner el valor más pequeño posible de `arr2`.

-...

## 3. Algoritmo (DP unidimensional)

``text
especie arrr2
p = min(len(arr1), len(arr2))
INF = un número mayor que todos los valores posibles (por ejemplo, 10**18)

dp = [INF] * (p+1)
dp[0] = arr1[0]
para k en 1..p:
dp[k] = min(arr1[0], arr2[0]) # arr2 se clasifica, arr2[0] es el elemento más pequeño

para i = 1 .. len(arr1)-1: # procesar el resto de arrr1
new_dp = [INF] * (p+1)
para k = 0 .. min(i+1, p):
# 1) mantener arrr1[i] si mantiene el orden estricto
si arr1[i] > dp[k]:
new_dp[k] = arrr1[i]

# 2) reemplazar arr1[i] por el elemento arr2 más pequeño не dp[k-1]
si k > 0 y dp[k-1] != INF:
# búsqueda binaria en arr2 para el primer elemento estrictamente mayor que dp[k-1]
x = elemento más pequeño en arrr2 que es не dp[k-1]
si x existe:
new_dp[k] = min(new_dp[k], x)

dp = new_dp
`` `

Después del bucle la respuesta es el más pequeño `k` tal que `dp[k] != INF`.
Si no existe tal `k ' , regrese `-1`.

-...

## 4. Análisis de la complejidad

Vamos.

* `m = len(arr1)`
* `n = len(arr2)`
* `p = min(m, n)` - la respuesta máxima que necesitamos considerar

TEN TERRITORIO TERRITORIO ANTERIOR
Silencio...
Silencio Ordenando `arr2` Silencioso `O(n log n)` Silencio
Silencio DP loop Silencioso `O(m * log n)` - para cada una de las `m` posiciones iterate up to `p` swap counts, and each swap needs a binario search (`log n`). Silencio
TENIDO Memoria TENIDO `O(p)` – matriz DP unidimensional. Silencio

Con `m` y `n` hasta `5·104`, esto funciona cómodamente dentro de los límites.

-...

## 5. Aplicación de la referencia (Python 3)

``python
importador bisect
de la importación Lista

INF = 10**18

Solución de clase:
def make ArrayIncreasing(self, arr1: List[int], arr2: List[int]) - título int:
arr2.sort() # sólo necesitamos una lista ordenada
m, n = len(arr1), len(arr2)
p = min(m, n)

# dp[k] = mínimo último valor del prefijo después de usar exactamente k swaps
dp = [INF] * (p + 1)
dp[0] = arr1[0] # no swap on the first element

# También podemos usar un intercambio en el primer elemento (cualquier valor arr2)
si no > 0:
dp[1] = min(arr1[0], arr2[0])

para i en rango(1, m):
new_dp = [INF] * (p + 1)
para k en rango(0, min(i + 1, p) + 1):
# 1. keep arrr1[i]
si arr1[i] > dp[k]:
new_dp[k] = arrr1[i]

# 2. reemplazar arrr1[i] si tenemos al menos un swap izquierdo
si k > 0 y dp[k - 1] != INF:
# encontrar el elemento arrr2 más pequeño dp[k-1]
idx = bisect.bisect_right(arr2, dp[k - 1])
si idx se hizo n:
new_dp[k] = min(new_dp[k], arr2[idx])

dp = new_dp

# Responder es el k más pequeño con un valor factible
para k en rango(p + 1):
si dp[k]!= INF:
de vuelta k
retorno -1
`` `

-...

## 6. Alternativa: Java Implementation (Space‐Optimised)

``java
importar java.util*;

Solución de la clase pública {}
public int makeArrayIncreasing(int[] arr1, int[] arr2) {
int m = arr1.length, n = arr2.length;
int p = Math.min(m, n);
final long INF = Long.MAX_VALUE / 4;

Arrays.sort(arr2);

long[] dp = new long[p + 1];
Arrays.fill(dp, INF);
dp[0] = arr1[0];
si (n ≤ 0) dp[1] = Math.min(arr1[0], arr2[0]);

para (int i = 1; i)
long[] newDp = new long[p + 1];
Arrays.fill(newDp, INF);
para (int k = 0; k <= Math.min(i + 1, p); k++) {
// 1. mantener arrr1[i]
si (arr1[i] > dp[k]) newDp[k] = arr1[i];

// 2. reemplazar arrr1[i]
si (k ⇩ 0 " dp[k - 1] INF) {
int idx = upperBound(arr2, dp[k - 1]); // first ⇩ dp[k-1]
si (idx י n) newDp[k] = Math.min(newDp[k], arr2[idx]);
}
}
dp = newDp;
}

para (int k = 0; k <= p; k++) si (dp[k] != INF) return k;
retorno -1;
}

// búsqueda binaria para el primer elemento objetivo
int privado superiorBound(int[] a, long target) {}
int l = 0, r = a.length;
mientras que (l
int m = (l + r) 1;
si (a[m] ]= target) l = m + 1;
r = m;
}
retorno l;
}
}
`` `

-...

## 7. Cheque rápido “Qué-si”

¿Scenario permanente? ¿Swaps mínimos? Silencio
Silencio...
TENIDA `arr1 = [1,2,3] ' (ya en aumento)
TENIDA `arr1 = [3,1,2] ``, `arr2 = [4,5]` tención `2 ' (swap 3→4, 1→5)
Silencio `arr1 = [5,4,3] ``, `arr2 = [1,2]` Silencio `-1 ` (no puede hacerlo aumentar)

-...

#### Summary

Una vez.
* Use DP where `dp[k]` stores the minimal possible last value after `k` swaps.
* Transición: mantener el elemento actual si mantiene el orden, o reemplazarlo con el elemento más pequeño `arr2` que es aún mayor que el valor anterior del prefijo.
* La respuesta es la más pequeña 'k' para la que existe una solución.

El algoritmo se ejecuta en la memoria `O(m · min(m,n) · log n)` tiempo y `O(min(m,n)', ajustando plenamente los límites del problema.