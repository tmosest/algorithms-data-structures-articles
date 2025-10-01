-...
Título: LeetCode 2907. Máximo Profitables Triplets con precios crecientes Yo...
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Explicación de la solución**

Por cada triplete de los índices `i

`` `
precio[j] ⇩ precio[i]
`` `

Debe esperar.
La suma que queremos maximizar es

`` `
beneficio[i] + beneficio[j] + beneficio[k]
`` `

Los arrays son a lo más `1000` largo – una solución `O(n2)` ya es rápida
Bastante.
La idea clave es pre-computar, para cada posible *izquierda* índice `i`,
el mejor beneficio posible del *right* partner `k`:

`` `
rightBest[i] = max{ profit[k] i y precio [k]
`` `

Una vez que `rightBest` se sabe, sólo tenemos que mirar un índice intermedio 'j' y
probar todos los índices izquierdos posibles `i` que satisfacen `precio[i] precio [j]`.
Si existe `rightBest[i]`, el valor candidato es

`` `
beneficio[i] + beneficio[j] + derechoBest[i]
`` `

y tenemos el máximo sobre todos esos candidatos.

----------------------------------------------------

#### Algorithm
`` `
n ← precio. longitud
derecho Mejor ← array de tamaño n, todos los valores = −∞ // no socio encontrado

// 1) computar mejor socio derecho para cada índice izquierdo i
para i = 0 ... n-1
← −
para k = i+1 ... n-1
si precio[k]
mejor ← max(best , profit[k])
rightBest[i] ← best

// 2) búsqueda del mejor índice medio j
respuesta ← −
para j = 0 ... n-1
para mí = 0 ... j-1
si el precio[i] se hacía el precio [j] y el derechoEl mejor[i]
candidato ← beneficio[i] + beneficio[j] + derechoBest[i]
respuesta ← max(respuesta , candidato)

respuesta de retorno // (integer de 64 bits)
`` `

----------------------------------------------------

#### Correctness Proof

Demostramos que el algoritmo devuelve el máximo beneficio posible.

-...

##### Lemma 1
Por cada índice `i` el valor `rightBest[i]` computed in step 1 equals
`máx{ profit[k] ¦ k  confianza i and price[k] [k] [i] }`.
Si no existe tal `k ' , `rightBest[i]` se establece a ``−∞`.

Proof.

El bucle interior del paso 1 examina todos los índices " k " con " k " i " .
Cada vez que el precio [k] se entiende por máximo el precio[i]`, `beneficio[k]`.
Así, después de que el bucle interior termine, `mejor ` iguala el beneficio máximo de
todos los índices al derecho de `i` cuyo precio es menor que `precio[i]`.
Finalmente `derecha El mejor[i] está fijado a ese máximo.
Si no existe una `k` calificada, el bucle interior nunca actualiza `mejor `,
por lo que se queda en `` — Dijo`. ∎



##### Lemma 2
Por cada índice intermedio 'j' y cada índice izquierdo 'i
" precio[i] " , si existe un socio adecuado válido,
" profit[i] + profit[j] + rightBest[i] " es el máximo beneficio de todos
triplets `(i , j , k)` que utilizan este particular `i` como el índice izquierdo
y como el índice medio.

Proof.

Arréglalo.
Por Lemma 1, `rightBest[i]` es el máximo `beneficio[k]` entre todos
indices " k " satisfaciendo " precio[k] " .
Cualquier triplet `(i , j , k)` con el pedido de precios requerido debe utilizar
exactamente un 'k'.
Así, el tercer componente más posible es `rightBest[i]`,
y el beneficio total es `beneficio[i] + beneficio[j] + derechoBest[i]. ∎



##### Lemma 3
Durante el paso 2 el algoritmo considera cada triplet válido
`(i , j , k)` que satisfies `i ' significa j ' hecho k ' y `price[j] > precio[i] ' .

Proof.

Toma cualquier triplete.
Durante el paso 2 el bucle exterior elige `j` como el índice medio.
El bucle interior se erige sobre todo 'i' con 'i 'i' significa j'.
Dado que `precio[i] ' precio [j] `, se cumple la condición en el bucle interior.
Por este `yo' también tenemos un 'k' válido con `precio[k] precio hecho [i]`; por lo tanto
por Lemma 1 `rightBest[i] י −∞`.
En consecuencia, el candidato computó para este par `(i , j)` es
exactamente el beneficio del triplete original. ∎



##### Lemma 4
Para cada par válido `(i , j)` el beneficio del mejor triplet que utiliza
'i' como la izquierda y 'j' como el medio nunca es más pequeño que el
valor candidato examinado por el algoritmo.

Proof.

Por Lemma 2 el valor candidato es el beneficio máximo alcanzable
con ese fijo `(i , j)`.
Por lo tanto, ningún otro triplete con los mismos índices izquierdo y medio puede
producir un beneficio más alto. ∎



################################################################################################################################################################################################################################################################ Theorem
El algoritmo devuelve el máximo beneficio posible sobre todos los trillizos
cumpliendo la orden de precios.

Proof.

Que `OPT' sea el beneficio óptimo.

*Existencia. *
Por Lemma 3 el algoritmo evalúa el beneficio de cada triplete válido,
por lo tanto también evalúa el triplete óptimo y obtiene un candidato
valor de al menos `OPT`.
Así que `respuesta ≥ OPT`.

*Optimality. *
El algoritmo mantiene el máximo de todos los candidatos examinados en el paso 2.
Cada candidato corresponde a un triplete válido (Lema 4).
Así, la `respuesta` no puede ser mayor que la `OPT`.
Por lo tanto `respuesta = OPT`. ∎



----------------------------------------------------

#### Complexity Analysis

`` `
Paso 1 : O(n2) tiempo , O(n) memoria adicional
Paso 2 : O(n2) tiempo , O(1) memoria extra
`` `

Con `n ≤ 1000` el programa cumple fácilmente los límites.

----------------------------------------------------

#### Aplicación de referencia (C++)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
// utilizar 64 bits entero para el cálculo, devolverlo
largo tiempo maxProfit(vector fieltint precio, vector garantizadoint ganancia) {
int n = (int)price.size();
const long long NEG_INF = LLONG_MIN / 4; // safe sentinel

/* paso 1: mejor socio derecho para cada índice izquierdo */
vector realizado largamente derecho de propiedadBest(n, NEG_INF);
para (int i = 0; i) {}
long long best = NEG_INF;
para (int k = i + 1; k)
si (price[k] ) 0 precio [i]) // valid right partner
mejor = max(best, (long long) profit[k]);
}
rightBest[i] = best;
}

/* paso 2: prueba cada índice medio */
larga respuesta = NEG_INF;
para (int j = 0; j)
para (int i = 0; i) {}
si (price[i] " ) " precio [j] " derechoBest[i] != NEG_INF) {
long cand = (long long) profit[i] + profit[j] + rightBest[i];
respuesta = max(respuesta, cand);
}
}
}
respuesta de retorno; // 64-bit resultado
}
};
`` `

La implementación sigue exactamente el algoritmo probado correcto arriba
y satisface los límites de tiempo/espacio requeridos.