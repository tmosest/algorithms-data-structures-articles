-...
Título: LeetCode 3573. Mejor tiempo para comprar y vender Stock V -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Explicación de la solución**

Porque todos los días sabemos el precio de las acciones `A[i]`.
Durante todo el período en la mayoría de las `K` *transacciones* pueden realizarse.

Una transacción puede ser

* **normal** – comprar al día `i ' y vender al día `j ' ( ' i ' i
* **Short** – vender en el día `i` y comprar de nuevo en el día `j` (`i ' i ' )

Después de una transacción todo el dinero está en efectivo de nuevo, por lo tanto un nuevo
transacción sólo puede comenzar ** después** el anterior ha terminado.
Mientras una transacción todavía está en progreso, nosotros tampoco

`` `
sosteniendo un stock comprado – hemos pagado el precio, estamos esperando a vender
sosteniendo una venta corta – recibimos el precio, estamos esperando para comprar de nuevo
`` `

----------------------------------------------------

##### 1. Estados

Por cada nivel de transacción `t ( 0 ... K ) `

`` `
res[t] – mejor beneficio total después de completar las transacciones t (cash)
comprar[t] – el mejor beneficio si actualmente estamos teniendo un stock comprado
la transacción t‐th (esperando vender)
vendido[t] – el mejor beneficio si estamos actualmente con un stock corto vendido
en la transacción t‐th (esperando comprar de nuevo)
`` `

" comprados " y " vendidos " se definen únicamente para la transacción *next*
( " comprados " / `sold[t] " pertenecen al número de transacción " ), por lo tanto,
su tamaño es `K ' (no `K+1`).

Todos los valores se mantienen como enteros firmados de 64 bits – un precio puede ser hasta
`109`, `K ≤ 100`, el resultado encaja fácilmente en un entero firmado de 64 bits.

----------------------------------------------------

##### 2. Transición por un precio a = A[i] `

Analizamos los días de izquierda a derecha, procesando el precio `a` una vez.
Por cada nivel de transacción " j " (que va hacia atrás** de `K ' a `1 ' ) nosotros
actualizar los tres arrays:

`` `
1) Terminar una transacción ahora

res[j] puede permanecer sin cambios,
o podemos terminar una transacción normal:
comprar[j-1] + a
o terminar una transacción corta:
sold[j-1] - a

res[j] = max( res[j], comprar[j-1] + a, sold[j-1] - a )

2) Iniciar una nueva transacción (normal) en este día
podemos abrir una posición "traída" para la transacción j

comprar[j-1] = max( comprar[j-1], res[j-1] - a )

3) Iniciar una nueva transacción (corte) en este día
podemos abrir una posición "short sold" para la transacción j

[j-1] = max( vendido[j-1], res[j-1] + a )
`` `

Los bucles se ejecutan hacia atrás (`j` decreciente) porque
`bought[j-1]` y `sold[j-1]` en el lado derecho todavía pertenecen al
nivel de transacción anterior " j-1 " .
Si usamos un bucle de avance vamos a sobreescribir valores que todavía están
necesaria en la misma iteración.

----------------------------------------------------

##### 3. Prueba de corrección

Demostramos que el algoritmo devuelve el máximo beneficio posible.

-...

##### Lemma 1
Después de procesar los primeros " precios " ,
`res[j]` equivale al máximo beneficio total alcanzable después de la mayoría de `j `
operaciones completas (normales o cortas) utilizando sólo estos " i+1 " días.

Proof.

Inducción sobre 'i'.

*Base `i = 0`*
Antes del primer día `res[0] = 0` (sin dinero gastado, sin transacción
completado).
Por consiguiente, no se puede terminar ninguna transacción.
`res[j] = 0` que es óptimo. La lema sostiene.

*Paso de introducción*
Supongamos que la lema se mantiene después del día `i-1`.
Durante la iteración del día `i` el algoritmo considera todas las formas de
*finish* a transaction on day `i` (case 1).
Todas las posibilidades que terminan una transacción el día `i` utilizar el óptimo
beneficio del día anterior (`res[j-1]`), el beneficio óptimo mientras
posesión de una posición comprada o corta ( " comprada [j-1] " /
`sold[j-1]`), y luego el nuevo precio `a`.
Así el máximo sobre estas tres posibilidades es exactamente el mejor
beneficio después de completar las transacciones " j " en los primeros " días " .
`res[j]` no se puede mejorar de ninguna otra manera porque todos los demás estados
o mantener una transacción ya terminada ( " , " sin cambios) o
realizar una transacción inacabada (encabezada en los otros dos arrays). ∎



##### Lemma 2
Después de procesar los primeros precios,
[J] equivale al máximo beneficio que se puede lograr
después de terminar en la mayoría de las transacciones de " j " ** y**, que todavía tienen
compran acciones que se compraron en la transacción `j+1` el día `i+1`.

Proof.

Inducción sobre 'i'.
La actualización en paso limitadonbsp;2 utiliza el beneficio óptimo `res[j-1]` de la
nivel de transacción anterior y resta el precio actual.
Por lo tanto `hijo[j]` es exactamente el beneficio óptimo para un normal abierto
transacción del nivel `j+1`.
Ninguna otra actualización cambia `hijo[j]`, por lo tanto la lema sostiene. ∎



##### Lemma 3
Después de procesar los primeros precios,
`sold[j]` equivale al máximo beneficio que se puede alcanzar después de completar
en la mayoría de las transacciones " j " , y aún manteniendo un stock corto de venta
transacción `j+1` el día `i+1`.

Proof.

Analogous to Lemma plaganbsp;2, using step limitadonbsp;3 of the transition. ∎



##### Lemma 4
During the update for a fixed price `a` and transaction level `j`,
las asignaciones

`` `
res[j] = max(res[j], bought[j-1] + a, sold[j-1] - a)
comprar[j-1] = max(bought[j-1], res[j-1] - a)
[j-1] = max(sold[j-1], res[j-1] + a)
`` `

mantener el invariante de Lemma sensiblenbsp;1, Lemma sensiblenbsp;2, y Lemma implicanbsp;3 para
todos los índices " realizados j " sin cambios, y actualizar correctamente las entradas para " j `
y `j-1`.

Proof.

*Caso 1 – finalizando una transacción. *
El algoritmo considera las tres posibilidades que terminan una transacción
en este día y mantiene el máximo; ninguna otra estrategia puede producir un
mayor ganancia para `res[j]`.

*Caso 2 – iniciando una nueva transacción normal. *
`hijo[j-1]` sólo se utiliza si después una transacción se termina en esto
día o día siguiente.
Tomando el máximo de su valor actual y el beneficio de una nueva compra
(`res[j-1] - a`) da el valor óptimo para una posición abierta comprada.

*Caso 3 – iniciando una nueva transacción corta. *
Mismo razonamiento para `sold[j-1]`.

El orden atrasado de `j` garantiza que los valores en la mano derecha
lado todavía pertenece al nivel de transacción anterior, por lo que las actualizaciones
son correctos. ∎



##### Lemma 5
Después de que todos los precios sean procesados, `res[K]` equivale al máximo beneficio total
alcanzable después de la mayoría de las transacciones de `K`.

Proof.

Por Lemma adultnbsp;1 después del último día (`i = N-1`) el array `res` contiene
el beneficio óptimo para cada transacción cuenta `0...K`.
Más transacciones nunca pueden disminuir el beneficio,
por lo tanto la entrada para 'K' es el mejor beneficio alcanzable con *at
la mayoría de las transacciones* ∎



################################################################################################################################################################################################################################################################ Theorem
El algoritmo produce el máximo beneficio total que se puede obtener por
en la mayoría de las transacciones normales o cortas
Siempre manteniendo a la mayoría de una unidad de acción.

Proof.

El valor devuelto por el algoritmo es el óptimo
beneficio. Por lo tanto el algoritmo es correcto. ∎



----------------------------------------------------

##### 4. Análisis de la complejidad

`` `
Dejar N = Налики , ≤ 100
`` `

El bucle exterior corre `N` veces, el bucle interior corre 'K' veces.

`` `
Tiempo : O(N · K) ≤ 5·104 · 100 = 5·106 operaciones
Memoria : O(K) ≤ 100 enteros de 64 bits
`` `

Ambos límites están muy por debajo de las limitaciones de problemas.

----------------------------------------------------

##### 5. Aplicación de referencia (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
larga duración máximaProfit(vector fieltro A, int K) {
int N = (int)A.size();
(K == 0 Silencioso N == 0) retorno 0;

const long long INF_NEG = -(1LL Identificado 60); // large negative number

vector realizado largamente confianza res(K + 1, 0); // res[0] = 0
vector realizado largamente comprado(K, INF_NEG); // comprado[t] - transacción de confianza t+1
vector realizado largamente vendido(K, INF_NEG); // vendido[t] - transacción de confianza t+1

para (int a : A) { // días de exploración de izquierda a derecha
(int j = K; j ' ilse= 1; --j) {
// 1) terminar una transacción ahora
acabado largoNormal = comprado[j - 1] + a; // comprado[j-1] puede ser -INF
acabado largo Short = sold[j - 1] - a; // sold[j-1] may be -INF
res[j] = max(res[j], max(finishNormal, endShort));

// 2) iniciar una transacción normal en este día
comprar[j - 1] = max(bought[j - 1], res[j - 1] - a);

// 3) iniciar una transacción corta en este día
[j - 1] = max(sold[j - 1], res[j - 1] + a);
}
}
devolver res[K];
}
};
`` `

El programa sigue exactamente el algoritmo probado correcto arriba y
se ajusta a los límites de tiempo y memoria del problema.