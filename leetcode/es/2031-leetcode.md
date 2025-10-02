-...
Título: LeetCode 2031. Cuenta Subarrays Con Más Unos Que Cero -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
*Idea*

Para un sub-array `A[l ... r]` Deja

`` `
S(i) = (#ones – #zeros) en A[0 ... i)
`` `

`S(i)` es una suma prefija que puede ser **+1** (para un `1`) o **–1** (para un `0`).

The sub-array `A[l ... r]` contiene más `1's que `0`s iff

`` `
S(r) – S(l-1) ≥ 1
`` `

Así que...

`` `
S(l‐1) ≤ S(r) – 1
`` `

Para un 'r' fijo sólo necesitamos saber cuántas sumas anteriores del prefijo
son **≤ S(r)–1**.
En lugar de realizar una consulta de rango podemos mantener un contador de funcionamiento
cuántas sub-arrayas que terminan en `r` satisfacer la condición.
Cuando nos movemos de `r-1` a `r` el contador se puede actualizar en **O(1)**.

----------------------------------------------------

#### One‐pass O(n) algoritmo

`` `
suma – actual suma prefijo (ones – ceros)
cnt – número de sub-arrayos clasificatorios que terminan en el índice actual
ans – número total de sub-arrayos clasificatorios
freq – hash mapa: prefijo suma → cuántas veces ha aparecido
`` `

`` `
freq[0] = 1 // prefijo vacío
suma = 0
cnt = 0
ans = 0

para cada elemento x en nums
si x == 1
cnt += freq[sum] // sub-arrays que terminan aquí
suma += 1
x == 0
sum -= 1
cnt -= freq[sum] // sub-arrays que terminan aquí
as = (ans + cnt) mod MOD
freq[sum] += 1
`` `

*¿Por qué funciona? *

* When `x == 1` estamos agregando un `+1` a la suma de prefijo.
Cada prefijo anterior suma 'p' que es ** igual** a la corriente
`sum` crea un sub-array `A[l ... r]` con
`S(r) – S(l-1) = 1`, i.e. more `1`s than `0`s.
El número de esos prefijos es `freq[sum]`.
Después de la actualización de `sum` también incluimos el nuevo sub-array que
comienza en el índice `0`.

* When `x == 0` estamos agregando un `-1`.
Cada prefijo anterior suma que es **exactamente** igual a la *nueva*
" la suma " marcaría la diferencia " (igual número de `1 ' y `0 ' s),
que ** no satisface el requisito.
Por lo tanto restamos `freq[sum]` de `cnt`.

La variable de funcionamiento 'cnt' siempre contiene el número de clasificación
sub-arrayos que terminan en la posición actual, así que añadiéndolo a `ans `
da el número total.

----------------------------------------------------

#### Correctness Proof

Demostramos que el algoritmo devuelve el número exacto de sub-arrays
con más `1's que `0`s.

-...

##### Lemma 1
Después de procesar los primeros " elementos " ( " 0 ≤ i " ),
`freq[p]` iguala el número de índices " j " ( " 1 ≤ j " ) de tal manera que
`S(j) = p`.

Proof.

* Initialización (`i = 0`). *
Antes de que empiece el bucle, ponemos `freq[0] = 1`.
Sólo existe el prefijo vacío `S(-1)=0`, por lo que la declaración sostiene.

* Paso de inducción. *
Suponga que la lema se mantiene después del elemento " i-1 " .
Durante el procesamiento del elemento `i` aumentamos
`freq[sum]` por uno, donde `sum = S(i)`.
Todos los índices anteriores son intactos, por lo tanto después de la actualización
`freq[p]` cuenta exactamente las ocurrencias de la suma prefijo `p`
entre los índices `-1 ... i`. ∎



##### Lemma 2
Durante la iteración del índice `i` (`0 ≤ i ■ n`) la variable `cnt`
iguala el número de sub-arrayos clasificatorios que terminan en el índice `i`.

Proof.

Que `s_before` sea el valor de `sum` antes de la actualización de la corriente
elemento y `s_after` su valor después.

*Caso 1 – `x == 1`.*

`S(i) = s_after`.
Cada sub-array que termina en 'i' y comienza en 'l' (`0 ≤ l ≤ i`)
tiene diferencia

`` `
S(i) – S(l-1) = s_after – S(l-1)
`` `

Es ≥ 1 **iff** `S(l‐1) = s_before `
(porque `s_before = s_after – 1`).
`freq[s_before]` cuenta exactamente todos esos índices " 1 " .
Por lo tanto, 'cnt' se convierte en el número correcto.

*Caso 2 – `x == 0`. *

`S(i) = s_after`.
Un submarino que termina en `i' tendría la diferencia '0' si y sólo si
`S(l-1) = s_after`.
Todos estos sub-arrays deben ser contados.
`freq[s_after]` los cuenta, así que restamos esta cantidad de
'cnt'.
Después de la resta, `cnt` es exactamente el número de sub-arrays
terminar en `i' que satisfagan el requisito.

Así pues, en ambos casos se actualiza el valor correcto. ∎



##### Lemma 2
En cada paso el algoritmo añade a `ans' exactamente el número de
clasificar sub-arrayos que terminan en el índice actual.

Proof.

Directamente desde Lemma adultnbsp;2, `cnt` es ese número,
y el algoritmo funciona
`ans ← ans + cnt (mod MOD)`. ∎



################################################################################################################################################################################################################################################################ Theorem
`ans` devuelto por el algoritmo equivale al número de sub-arrays de
`nums` that contain strictly more `1`s than `0`s (modulo `MOD`).

Proof.

Por Lemma adultnbsp;2, durante toda la traversal cada clasificación
sub-array se añade a 'ans' exactamente una vez - es decir, cuando su derecho
endpoint es procesado.
No se añaden otras sub-arrayas, porque 'cnt' cuenta sólo las que
satisfacer la condición (por la construcción de las actualizaciones).

Por lo tanto después de la última iteración `ans` contiene el número total de
sub-arrayas clasificatorias. ∎



----------------------------------------------------

#### Complexity Analysis

TEN TERRITOR TEN TERRITOR TEN TERRITOR TEN TERRITOR TEN TERRITOR TEN TERRITOR SON TEN TERRITOR SON SON SON 
Silencio------Prince--------
Silencioso sobre la matriz Silencioso `O(n)` Silencio `O(n)` (hash mapa of at most `n+1` different prefix sums)
TENIENDO TODAS LAS OPERACIONES Silencio

Así que la complejidad general del tiempo es **O(n)** y el espacio auxiliar
es **O(n)** (hash map).

----------------------------------------------------

#### Referencia Implementación (Java)

``java
importa java.util. HashMap;
importa java.util. Mapa;

Solución de la clase pública {}
static final long MOD = 1_000_000_007L;

public long numSubarrayDóndeMásOnesThanZeros(int[] nums) {
ans largas = 0; // respuesta final
cnt largo = 0; // sub-arrayas clasificatorias terminando en i
int sum = 0; // prefijo sum (#ones – #zeros)

Mapa seleccionadoInteger, Longilo freq = nuevo HashMap garantizado();
freq.put(0, 1L); // prefijo vacío

para (int x : nums) {
(x == 1) {
// sub-arrayos que terminan aquí y satisfacen la condición
cnt = (cnt + freq.getOrDefault(sum, 0L) % MOD;
suma += 1;
} más { // x == 0
suma -= 1;
// sub-arrayos de subtracto que haría que los conteos sean iguales
cnt = (cnt - freq.getOrDefault(sum, 0L) + MOD) % MOD;
}
as = (ans + cnt) % MOD;
freq.put(sum, freq.getOrDefault(sum, 0L) + 1);
}
devolver los ans;
}

Para pruebas rápidas...
public static void main(String[] args) {
Solución s = nueva solución ();
System.out.println(s.numSubarrayDóndeMásOnesThanZeros(s)
nuevo int[]{0,0,1,0})); // 5
System.out.println(s.numSubarrayDóndeMásOnesThanZeros(s)
nuevo int[]{0,1,0,0,0,0,1,0,1}); // 18
}
}
`` `

----------------------------------------------------

#### Aplicación de referencia (C++17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
static const long MOD = 1'000'007LL;
largo largo numSubarrayDóndeMásUnoThanZeros(vector fieltro reducido nums) {
unordered_map obtenidosint, long long long long frecuenciaq;
freq[0] = 1; // prefijo vacío
larga suma = 0; // suma prefijo (#ones – #zeros)
largo cnt = 0; // sub-arrays terminando en idx actual
ans largos = 0;
para (int x : nums) {
(x == 1) {
cnt = (cnt + freq[sum]) % MOD; // sub-arrays que terminan aquí
++sum;
} más { // x == 0
-sum;
cnt = (cnt - freq[sum] + MOD) % MOD; // subtract bad ones
}
as = (ans + cnt) % MOD;
++freq[sum];
}
devolver los ans;
}
};
`` `

----------------------------------------------------

La misma lógica se puede escribir en cualquier otro idioma (Python, Go, Rust,
etc.) – la clave es la técnica de prefijo de un paso-sum + hash-map.