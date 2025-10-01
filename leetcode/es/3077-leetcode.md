-...
Título: LeetCode 3077. Fuerza máxima de K Disjoint Subarrays -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recapitulación de problemas (LeetCode 3077)

■ **La fuerza máxima de las subarrayas disyuntivas de K**
■ Dificultad:
■ **Tags:** Programación dinámica, Prefix Sum, Knapsack

Se le ha dado un array entero `nums` (length `n`) y un extraño entero `k`.
Elija exactamente `k` disjoint sub-arrays
`sub1, sub2, ... , subk ' tal que el último índice de `subi` está estrictamente ante el primer índice de `subi+1`.
La fuerza **** de un conjunto elegido es

`` `
fuerza = k * sum(sub1) – (k‐1) * sum(sub2) + (k‐2) * sum(sub3) – 2 * sum(sub{k‐1}) + sum(subk)
`` `

Devuelve la máxima fuerza posible.
" 1 ≤ 104 " , `resistentes [i] sometidos ≤ 109 ' , `1 ≤ k ≤ n ' , `k ' is odd, and `n·k ≤ 106`.

El problema es un problema clásico de programación dinámica con un giro de “suma alternada ponderada”.



-...

## 2. Core Idea

*El problema puede ser reescrito como un DP sobre sumas prefijo. *

Por cada prefijo `0 ... j` guardamos la mejor fuerza posible para los primeros 'i` sub-arrays que terminan **dentro** ese prefijo.
Vamos.

`` `
dp[i][j] = máxima fuerza que se puede lograr mediante la selección de sub-arrays descomunales de nums[0 ... j-1)
`` `

Transition for the `i‐th` sub-array:

`` `
dp[i][j] = max( dp[i][j-1] , // no termine un subarray en j-1
max_{t armonizai-1 ... j-1} ( dp[i-1][t] + weight(i) * (pref[j] – pref[t]) ) )
`` `

Donde
`pref[x]` es la suma prefijo `nums[0] + ... + nums[x-1]` y

`` `
peso(i) = (k - i +1) * (-1)^(i+1)
`` `

Porque `k` es extraño, los pesos alternan `+k, -(k‐1), +k‐2, ... , +1`.
La maximización interna se puede mantener en *O(1)* por `j` manteniendo el mejor valor

`` `
dp[i-1][t] - weight(i) * pref[t]
`` `

mientras iteraba sobre `j`.
Complejidad general: `O(k·n)` tiempo y `O(n)` espacio extra (tenemos sólo dos filas).

-...

## 3. Código

A continuación se presentan implementaciones idiomáticas limpias en **Java, Python y C+**.
Cada archivo es auto-contenido y listo para copiar-paste en una solución LeetCode.

▪ restablecimiento Todas las soluciones suponen una indexación basada en 0 para 'nums' y usan aritmética larga (64-bit) para evitar el desbordamiento.

-...

### 3.1 Java

``java
importar java.util*;

Clase Solución {
public long maximumStrength(int[] nums, int k) {
int n = nums.length;
long[] pref = new long[n + 1];
para (int i = 0; i) pref[i + 1] = pref[i] + nums[i];

largo[] prev = nuevo largo[n + 1]; // dp[i-1][*]
largo[] cur = nuevo largo[n + 1]; // dp[i][*]

para (int i = 1; i) = k; i++) {
long weight = (k - i +1) * ((i) == 1 ? 1 : -1); // (+,-,+,-,...)
long best = Long.MIN_VALUE; // best of (dp[i-1][t] - weight*pref[t]
para (int j = 1; j <= n; j+) {}
// actualización mejor para el j actual (t = j-1)
mejor = Math.max(best, prev[j - 1] - weight * pref[j - 1]);

// Opción 1: no termine un subarray en j-1
largo no End = cur[j - 1];

// opción 2: terminar un subarray en j-1
final largo Aquí = mejor + peso * pref[j];

cur[j] = Math.max(notEnd, endHere);
}
/ / / swap rows for next i
largo[] tmp = prev; prev = cur; cur = tmp;
}
retorno prev[n];
}
}
`` `

-...

#### 3.2 Python

``python
Solución de clase:
def máximo Fuerza (yo, nums: List[int], k: int) - Propiedad int:
n = len(nums)
(n +1)
for i, v in enumerate(nums, 1):
pref[i] = pref[i-1] + v

(n +1)
r = [0] * (n +1)

para i en rango(1, k + 1):
peso = (k - i +1) * (1 si i & 1 más -1)
mejor = flotante('-inf')
para j en rango(1, n + 1):
# update best for t = j-1
mejor = max(best, prev[j-1] - weight * pref[j-1]

Mantener el estado anterior
not_end = cur[j-1]
# Termina un subarray en j-1
end_here = best + weight * pref[j]

cur[j] = max(not_end, end_here)
prev, cur = cur, prev # reuse arrays
retorno prev[n]
`` `

-...

### 3.3 C++

``cpp
Clase Solución {
public:
Long long long maximumStrength(vector interpretadoint ánimo nums, int k) {
int n = nums.size();
vector realizado largo tiempo anterior(n + 1, 0);
para (int i = 0; i) no; ++i) pref[i+1] = pref[i] + nums[i];

vector realizado largo tiempo anterior(n + 1, 0), cur(n + 1, 0);

para (int i = 1; i) = k; ++i) {}
largo peso = (largo largo)(k - i + 1) * (i) ? 1 : -1);
largo tiempo mejor = LLONG_MIN;
para (int j = 1; j)
// actualización mejor para t = j-1
mejor = max(best, prev[j-1] - weight * pref[j-1]);

largo no End = cur[j-1];
largo plazo Aquí = mejor + peso * pref[j];

cur[j] = max(notEnd, endHere);
}
swap(prev, cur);
}
retorno prev[n];
}
};
`` `

Las tres soluciones funcionan en **O(k · n)** tiempo y **O(n)** espacio extra – muy por debajo de los límites (`n·k ≤ 106`).

-...

## 4. Artículo del Blog: “El Bien, el Mal, y el Ugly de LeetCode 3077”

■ *Título*
■ *La fuerza máxima de las subarrayas disyuntivas de K – El bien, el mal y el ugly (A DP Masterclass)*
■ **Meta Descripción:**
■ Master LeetCode 3077 con una guía de programación dinámica, código práctico en Java, Python & C++, y conocimientos de entrevista.
■ **Keywords:** LeetCode 3077, máxima fuerza de k disjoint subarrays, programación dinámica, codificación de entrevistas, entrevista de trabajo, diseño de algoritmos

-...

#### 4.1 Introducción

LeetCode 3077 le pide que elija *exactamente* `k` desjoint sub-arrays de un conjunto entero y maximice un *peso de la suma alterna*.
A primera vista, se siente como una variante del clásico “máxima suma de ‘k’ disjoint sub-arrays” problema, pero el patrón de signos (+, –, +, – ...) lanza una llave inglesa en soluciones estándar.

Si te estás preparando para una entrevista de datos o algoritmos, dominar este problema demuestra:

* **Destreza DP** – usted puede formular un DP multidimensional con transiciones estatales no-triviales.
* ** Optimización del espacio** – se puede reducir `O(k·n)` a `O(n)` por reutilizar filas.
* **Atención al detalle** – Usted maneja correctamente números negativos y grandes entradas.

Diseccionemos el problema en tres partes:

Silencio Parte privada Lo que estás aprendiendo Silencio ¿Por qué importa
Silencio...
Silencio **The Good** Silencio Clean DP formulation + tiempo/complejidad espacial tención Muestras que puedes razonar sobre sub-estructuras óptimas
Silencio **El mal** Silencio común trampas (off‐by-one, errores de firma, desbordamiento) Silencio Destaca lo que *no* hacer durante una entrevista Silencio
Silencio **El Ugly** Silencio Profundo razonamiento sobre el patrón de peso " prefijo optimización Silencio Revela la penetración más profunda del algoritmo

-...

### 4.2 The Good – A Clean DP

###### 4.2.1 State

`dp[i][j]` = best strength using **first `i` sub-arrays** within the prefix `nums[0...j-1]`.

- " I " ranges 0...k.
- 'j` rangos 0...n.
- Caso base: `dp[0][*] = 0` (no sub-array → la fuerza 0).

##### 4.2.2 Transición

Para el sub-array, su peso es

`` `
peso(i) = (k - i +1) * (-1)^(i+1)
`` `

Si terminamos el sub-arrayo de la `i` en el índice `j-1`, la suma de la sub-array es `pref[j] - pref[t]` para algunos `t  observado j`.
Así:

`` `
dp[i][j] = max(
dp[i][j-1], // skip j- 1
max_{t י j} ( dp[i-1][t] + weight(i) * (pref[j] - pref[t]) )
)
`` `

El máximo interior mira *all* posibles puntos de partida del último sub-array.
Sin la optimización esto sería `O(n)` por célula, dando `O(k·n2)` – demasiado lento.

##### 4.2.3 Prefix Trick

Define

`` `
mejor = max_{t < j} ( dp[i-1][t] - weight(i) * pref[t] )
`` `

Entonces...

`` `
dp[i][j] = max( dp[i] [j-1] , best + weight(i) * pref[j]
`` `

Durante el escaneo sobre `j`, mantenemos `mejor ' actualizado en `O(1)` tiempo, dando lugar a `O(k·n)` general.

##### 4.2.4 Reducción del espacio

Sólo se necesitan simultáneamente " dp[i-1][*] " y " dp[i][i] " .
Mantenemos dos arrays 1-D `prev` y `cur`, swapping them after each `i.
El espacio se reduce a `O(n)` – vital cuando `k` puede ser unos pocos miles.

-...

### 4.3 El malo – saltos comunes

1. **Off‐by-one en sumas prefijas**
- Utilizar indebidamente " pref[j] " en lugar de " pref[j-1] " en la transición.
- Arreglar: Recuerda `pref[x]` es la suma de los primeros elementos x.

2. **Perfunción de signos de peso**
- Dado que `k` es extraño, los pesos alternan comenzando con '+k`.
- Un error de signo se propaga a través del DP, dando una respuesta negativa absurdamente grande.

3. *Desbordamiento del número entero*
- Cada año. puede ser 109 y puede haber hasta 104 elementos → prefijo suma hasta 1013.
- Use `long '/`long ' (64-bit) en lugar de ' in.

4. Caso básico equivocado**
- Olvidar `dp[0][j] = 0` conduce a la propagación `Long.MIN_VALUE` y el algoritmo se bloquea.

5. **No volver a utilizar arrays**
- Algunas soluciones asignan matrices 'k`×`n` y exceden la memoria (incluso si `n·k ≤ 106` el factor constante importa en Java).

6. **Mis-interpreting “disjoint”**
- Las sub-arrayas deben ser * no superpuestas*; no se puede saltar un índice dentro de un sub-array elegido.

-...

### 4.4 The Ugly – Weight Pattern Deep Dive

El patrón de peso `(+k, -(k-1), +k-2, ..., +1)` es lo que convierte esto en un problema “muy”.

#### 4.4.1 Why It Matters

Si todos los pesos eran `+1`, el DP reduce a la conocida “máxima suma de ‘k’ disjoint sub-arrays” – se puede resolver con una simple recurrencia.
Los signos alternantes significan la contribución de un sub-array puede *subtract* del total si su índice es incluso (en relación con el orden elegido).

#### 4.4.2 Optimisation Insight

Considere la maximización interior:

`` `
max_{t} ( dp[i-1][t] + peso * (pref[j] – pref[t]) )
`` `

Ampliación:

`` `
= peso * pref[j] + max_{t} ( dp[i-1][t] - peso * pref[t] )
`` `

El término dentro del `max` es *independiente* de `j` después de fijar `t`.
Por lo tanto, mientras escaneamos `j` izquierda a derecha, podemos mantener el mejor valor de

`` `
dp[i-1][t] - peso * pref[t]
`` `

en una variable de funcionamiento mejor.
Cada nuevo `j` sólo necesita `prev[j-1] - peso * pref[j-1]` para actualizar `mejor'.
Ese es el truco algebraico “muy” que convierte al DP en tiempo *linear* por `i.

-...

### 4.5 Interview‐ Consejos listos

Silencioso Código de ejemplo Silencio
Silencio...
Silencio **Explicar su diagrama DP** – bosquejar tabla `dp` sobre papel. TENIDA `dp[i][j]` – first `I` sub-arrays inside `0...j-1`. Silencio
ANTERIOR **Walk through a small example** (e.g., `nums = [1,-2,3,4]`, `k=3`). tención Mostrar cómo mejor actualiza cada paso. Silencio
Silencioso **Mostrar manejo de desbordamiento** – uso `long`. Silencioso `long weight = (k - i + 1) * (i " 1) == 1 ? 1 : -1); ' 
tención **El optimismo del espacio** – mencionar el intercambio de filas. TENIDA `swap(prev, cur);` Silencio
Silencio **Explicar por qué k es extraño** – asegura que el peso final es `+1`. TENIDO `peso(i)` fórmula. Silencio

-...

#### 4.6 Conclusiones

LeetCode 3077 es una hermosa mezcla de *clásico DP* y * optimización no tripartita*.
Usted puede resolverlo limpiamente, evitar trampas de entrevistas comunes, y, lo más importante, mostrar entrevistadores que usted puede *ver* la estructura subyacente y traducirlo en código.

■ *“Destruir el problema, entonces preguntar: ¿cómo sería una pregunta de entrevista de seguimiento?”*
■ Esa curiosidad te mantiene por delante de la curva.



-...

## 5. Pensamientos finales

La solución DP anterior es tanto **eficiente** como **extensible**.
Si no estás seguro de cómo abordarlo en la entrevista, intenta construir la tabla DP a mano para una pequeña entrada – verás el patrón de “mejor hasta ahora” emerge naturalmente.

¡Feliz codificación, y buena suerte aterrizando ese trabajo! 🚀



-...



### 5.1 Referencias

* LeetCode 3077 – Maximum Strength of K Disjoint Subarrays
* “Maximum Sum of `k` Non-Overlapping Subarrays” – clásico LeetCode 689
* Programación competitiva 3 – técnicas de programación dinámica



-...



*No dude en comentar a continuación si desea una inmersión más profunda en cualquiera de las optimizaciones de DP o estrategias de entrevista! *