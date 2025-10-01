-...
Título: LeetCode 2809. Tiempo mínimo para hacer Sum Array en la mayoría x -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
*Problema*

Se le dan dos arrays de la misma longitud

`` `
nums1[0 ... n-1] – valores actuales
nums2[0 ... n-1] – “crecimiento” valores
`` `

En cada segundo `t` toda la matriz `nums1` crece por su
valores correspondientes de `nums2 ' , es decir, en el momento `t `

`` `
valor[i] = nums1[i] + t * nums2[i]
`` `

Durante cualquier segundo usted puede **pick un índice y establecer `nums1[i] a `0`**.
Una vez que es cero el crecimiento todavía sucede, pero el valor es siempre
`0 + (t-chosen_time) * nums2[i]`.

Su objetivo es encontrar el menor número de segundos `t`
(`0 ≤ t ≤ n`) tal que después de aplicar en la mayoría `t` cero-operaciones los
suma de todos los valores es ≤ `x`.
Si esto es imposible volver `-1`.

----------------------------------------------------

##### 1. Observaciones

* Ceroando un elemento con un **grande** debe ser hecho **late**,
porque cuanto antes lo cero más veces su crecimiento se añade
a la suma.
Por lo tanto, primero clasificamos los pares `(nums1[i], nums2[i]) `
aumentando los años 2.

* Para un número fijo de operaciones no nos gustaría saber
# ¿Cuánto podemos reducir la suma** en comparación con el caso en que lo hacemos
nada.

* Si ya hemos considerado los primeros 'i‐1' pares y todavía queremos
para utilizar las operaciones " j " , podemos:

1. **Ignore** el par `i`‐th – la reducción es `dp[i‐1][j]`.
2. **Use** una operación en el par `i`‐th – entonces usamos
`j‐1` operaciones en los primeros `i‐1` pares y pasar el último
operación en este par.
La reducción aportada por este par es

`` `
nums1[i] // hemos cero su valor inicial
+ nums2[i] * j // hemos eliminado j futuros crecimientos
`` `

* Estas dos opciones dan un clásico DP 2-dimensional.

----------------------------------------------------

##### 2. Formulación del DP

Vamos.

`` `
dp[i][j] – máxima reducción posible en la suma
si utilizamos en la mayoría j cero-operaciones
entre los primeros pares (después de ordenar).
`` `

`dp[0][*] = 0` – sin pares no podemos reducir nada.

Recurrence for `1 ≤ i ≤ n` and `1 ≤ j ≤ i` :

`` `
sin_i = dp[i-1][j] // no somos pareja cero
con_i = dp[i-1][j-1] + nums1[i] + nums2[i] * j // we cero pair i
dp[i][j] = max( without_i, with_i )
`` `

¿Por qué `nums2[i] * j`?
Si cero este par a la vez `j`, su valor en ese momento tendría
ha aumentado `j` veces por `nums2[i]`.
Cero que elimina todos esos futuros aumentos **más** su
valor original `nums1[i]`.

Después de llenar la tabla, `dp[n][t]` nos dice la reducción *maximum*
podemos lograr si se nos permite exactamente "no" operaciones.

----------------------------------------------------

##### 3. Encontrar la respuesta

La suma de todos los elementos después de `t` segundos **sin**
operaciones

`` `
S(t) = sum(nums1) + sum(nums2) * t
`` `

Si utilizamos las mejores reducciones dadas por `dp[n][t]`, la suma real es

`` `
sum_after_t = S(t) – dp[n][t]
`` `

Necesitamos el más pequeño `t ' tal que `sum_after_t ≤ x`.
Si no existe tal " no " (es decir, incluso con " t = n " , todavía es " x " ) nosotros
Regrese `-1`.

----------------------------------------------------

##### 4. Optimización de memoria

El DP utiliza sólo la fila anterior, por lo que podemos mantener un solo
array 1-dimensional y actualizarlo de vuelta a frente:

`` `
int[] dp = nuevo int[n+1]; // dp[j] = dp[i] [j] después de terminar par i

para (int i = 1; i) = n; ++i) {}
para (int j = i; j ' il= 1; --j) {
dp[j] = Math.max(dp[j], dp[j-1] + nums1[i] + nums2[i]*j);
}
}
`` `

----------------------------------------------------

##### 4. Complejo

*Sorting* : `O(n log n) `
*DP*: `O(n2)` time, `O(n)` memory
*Finding t*: `O(n)` tiempo

----------------------------------------------------

##### 5. Aplicación de las referencias

A continuación se muestra una aplicación Java concisa que sigue lo anterior
procedimiento.
(Es equivalente a la solución clásica para LeetCode 2781,
pero escrito desde cero para la claridad.)

``java
importar java.util*;

Solución de la clase pública {}
public int minimumSeconds(int[] nums1, int[] nums2, int x) {
int n = nums1.length;

// 1. clasificar índices aumentando nums2
Integer[] idx = nuevo Integer[n];
para (int i = 0; i)
Arrays.sort(idx, (a, b) - título Integer.compare(nums2[a], nums2[b]));

// 2. sumas prefijo de los arrays originales
long sum1 = 0, sum2 = 0;
para (int i = 0; i)
suma1 += nums1[i];
sum2 += nums2[i];
}

// caso trivial
si (sum 1 <= x) retorno 0;

PD
int[] dp = nuevo int[n + 1]; // dp[j] – mejor reducción con j ops
para (int id = 0; id י n; id++) {}
int a = nums1[idx[id];
int b = nums2[idx[id];
// actualización de alta j a baja j para evitar sobreescritura
para (int j = id + 1; j ю= 1; j--) {
int with = dp[j - 1] + a + b * j;
int without = dp[j];
dp[j] = Math.max(con, sin);
}
}

// 4. encontrar mínimo t
para (int t = 0; t <= n; t++) {}
largo cur = suma1 + suma2 * t - dp[t];
si (curo 0= x) devuelve t;
}
retorno -1; // incluso con todas las operaciones n no es suficiente
}
}
`` `

----------------------------------------------------

##### 4. Por qué funciona esto

*Sorting garantiza que cada vez que decidimos cero un par a la vez
`j`, todos los pares con mayores `nums2` serán considerados más adelante en el DP
y por lo tanto se nos permite pasar la operación en ellos a
más tarde segundo, que siempre es óptimo. *

*El DP considera todas las posibles opciones de operaciones cero
(“skip” vs “use”) para cada par, por lo que “dp[n][t]” es el verdadero máximo
reducción obtenida con operaciones " t " . *

*Finalmente simplemente revisamos las sumas resultantes para `t = 0 ... n`; el primero
tiempo que podemos alcanzar `x` es el número mínimo requerido de segundos. *

----------------------------------------------------

##### 5. Nota final

*Si prefieres una versión de ahorro de memoria puedes guardar sólo la
array 1-dimensional como se muestra anteriormente – todavía necesita `O(n2)` tiempo
porque cada elemento debe ser procesado por cada `t`.
El algoritmo es fácilmente portado a Python o C++ también; la clave
La recurrencia permanece igual. *

¡Feliz codificación!