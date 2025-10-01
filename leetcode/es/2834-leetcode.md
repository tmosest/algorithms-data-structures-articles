-...
Título: LeetCode 2834. Encuentra el Suma Mínimo Posible de un Hermoso Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Explicación de la solución**

Por cada número 'x' el par que da la suma 'target' es
`(x, target‐x)`.

`` `
1 + (target-1)
2 + (target-2)
...
⌊target/2⌋ + (target-⌊target/2⌋)
`` `

Si ya usamos todos los números '1 ... ⌊target/2⌋` no podemos utilizar ningún
número en el rango `⌊target/2⌋+1 ... target-1` - cada uno de ellos tiene
a partner that is already taken and together would sum to `target`.

Por lo tanto

* Todos los números `objetivo `` que podemos utilizar son exactamente `1 ... ⌊target/2⌋`.
Forman una secuencia aritmética.
* Cada número de `≥` es seguro - la suma con cualquier entero positivo
es más grande que `target`.
Forman la segunda secuencia aritmética comenzando en `target`.

El objetivo es elegir los números más pequeños que satisfacen lo anterior
restricción, es decir, tomar todos los números pequeños posibles primero y luego
continue from `target` if more numbers are still needed.

Las dos secuencias son

`` `
baja : 1 ... mitad (half = objetivo/2)
alto : objetivo ... objetivo + mantener 1
`` `

Donde

`` `
restantes = n - min(n, half)
`` `

Ambas sumas pueden ser calculadas por la fórmula conocida

`` `
suma(1 ... k) = k*(k+1)/2
`` `

y la suma de un rango general `[a ... b]` es

`` `
suma(1 ... b) – sum(1 ... a-1)
`` `

Todos los cálculos se realizan modulo `MOD = 1 000 000 007`.

----------------------------------------------------

#### Algorithm
`` `
mitad = objetivo / 2
lowCount = min(n, half) // cuántos números de la primera parte
lowSum = lowCount*(lowCount+1)/2 (mod MOD)

restantes = n - bajo
si queda 0
HighStart = objetivo
alto Final = objetivo + restante - 1
highSum = (highEnd*(highEnd+1)/2
- (highStart-1)*highStart/2) (mod MOD)
más
alto Sum = 0

respuesta = (lowSum + HighSum) mod MOD
`` `

----------------------------------------------------

#### Correctness Proof

Demostramos que el algoritmo devuelve la suma mínima posible de una
anti-dos-sum array of length `n`.

-...

##### Lemma 1
Si un número de `x` satisfies `x ' identificado target` y `x ≤ target/2`, entonces
cualquier número `y' con `target/2 י y لم target` tiene la propiedad
x + y = blanco y por lo tanto no puede ser elegido junto con `x`.

Proof.

`y` está en el intervalo `(target/2 , target)` que implica `target-y`
pertenece a `(0 , target/2]`.
Porque `x ≤ target/2`, tenemos `target-y ≥ target-x ≥ 0`.
Así `x + y = blanco ' ∎



##### Lemma 2
Cualquier entero `z ≥ target` puede ser elegido junto con todos los números
" 1 ... objetivo-1 " (es decir, con cualquier número menor que " objetivo " ).

Proof.

Para cada `x ' identificado objetivo ' tenemos `x + z ≥ target + 1 >
Por lo tanto la suma nunca puede igualar `target`. ∎



##### Lemma 3
El más pequeño posible conjunto anti-dos-sum de tamaño `n` consiste en

* the first `k = min(n, ⌊target/2⌋)` numbers `1 ... k`
* if `n œ k`, the next `n-k` successive numbers starting from `target `

Proof.

De Lemma adultnbsp;1 el conjunto `{1,...,⌊target/2⌋}` contiene el más pequeño
elementos posibles.
Ningún elemento en `(⌊target/2⌋+1 , target-1)` se puede añadir,
de lo contrario, se combinaría con un elemento elegido para resumir `target`.
Por lo tanto, cada elemento del conjunto final debe ser en la primera parte
o al menos `target`.
Lemma implicabsp;2 muestra que todos los enteros `≥ target` son válidos.
Tomar los números disponibles más pequeños produce la suma mínima mundial,
y esta es exactamente la construcción descrita. ∎



##### Lemma 4
`bajo Sum` computed by the algoritmo equals the sum of the first `k`
enteros (`k = min(n, ⌊target/2⌋)`).

Proof.

Por la fórmula de la serie aritmética

`` `
suma(1 ... k) = k(k+1)/2
`` `
El algoritmo aplica este modulo de fórmula `MOD`. ∎



##### Lemma 5
'highSum' computado por el algoritmo equivale a la suma de la consecutiva
integers `target ... target+remaining-1`, where `remaining = n-k`.

Proof.

La suma de un rango " [a ... b] " equivale a

`` `
suma(1 ... b) – sum(1 ... a-1)
= b(b+1)/2 – (a-1)a/2
`` `

El algoritmo calcula exactamente esta expresión (modulo `MOD`).
Así, `highSum` es la suma correcta de los números requeridos. ∎



################################################################################################################################################################################################################################################################ Theorem
El algoritmo devuelve la suma mínima posible de un conjunto de longitud
`n` que evite cualquier par de elementos que summing a `target`.

Proof.

Que `S` sea el conjunto elegido por el algoritmo.
Por Lemma plaganbsp;3 `S` es exactamente el conjunto óptimo de `n` más pequeño
elementos que respetan la limitación.
`lowSum ' y `highSum` son, por Lemma contaminanbsp;4 y Lemma tronbsp;5, el
sumas de las dos partes de `S`.
Por lo tanto el algoritmo produce `sum(S)` (modulo `MOD`), que es el
suma mínima requerida. ∎



----------------------------------------------------

#### Complexity Analysis

Todas las operaciones son simples aritméticas; no se utilizan bucles ni recursión.

`` `
Hora: O(1)
Memoria: O(1)
`` `

----------------------------------------------------

#### Referencia Implementación (Java 17)

``java
importa java.io.*;

clase pública Principal {}
static final int MOD = 1_000_000_007;

public static int minimumPossibleSum(int n, int target) {}
int half = target / 2;
int lowCount = Math.min(n, half); // números tomados de 1 ... mitad

// suma de los primeros números positivos bajosCount
long lowSum = (long) lowCount * (lowCount + 1) / 2) % MOD;

int remaining = n - lowCount; // números todavía necesarios
largo alto Sum = 0;
si (continúo siendo) 0) {
inicio largo = objetivo; // primer número del lado alto
final largo = objetivo + restante - 1; // último número necesario

// suma de 1 ... final
long sumEnd = end * (end +1) / 2;
// suma de 1 ... (start-1)
long sumStartMinus1 = (start - 1) * start / 2;

highSum = (sumEnd % MOD - sumStartMinus1 % MOD + MOD) % MOD;
}

(int) ((lowSum + highSum) % MOD);
}

/* ----------------------------------------------------------------------------

public static void main(String[] args) tira IOException {
BufferedReader br = nuevo BufferedReader (nueva InputStreamReader(System.in));
StringTokenizer st = nuevo StringTokenizer(br.readLine());
int n = Integer.parseInt(st.nextToken());
int target = Integer.parseInt(st.nextToken());
System.out.println(minimumPossibleSum(n, target));
}
}
`` `

El programa sigue exactamente el algoritmo probado correcto arriba y
se ajusta a Java 17.