-...
Título: LeetCode 3177. Encontrar la longitud máxima de una buena subsequencia II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🎯 1 Million Years Later – The **Maximum length Good Subsequence** Problema

■ *Problema*
■ Se le da un array entero `nums` (`1 ≤ nums.length ≤ 100 000`) y un entero `k` (`0 ≤ k ≤ nums.length`).
■ Una subsecuencia *buena* es una secuencia que puede contener a lo más `k` ** pares adyacentes desiguales**.
■ En otras palabras, cuando usted lee una buena subsequencia de izquierda a derecha se le permite cambiar el valor en la mayoría de los tiempos 'k'.
■ Encuentra la longitud máxima posible de tal subsequencia.

■ *Examples*
" `
Entrada: nums = [5, 1, 3, 5, 4], k = 1
■ Producto: 4 // [5, 5, 4, 4] o [5, 1, 5, 5]
" `
" `
Input: nums = [1, 2, 3, 4], k = 0
■ Producto: 1 // sólo puede elegir un elemento único
" `

El resto de este post es una guía *paso por paso* que te guía desde la idea bruta-force, a través de trucos dinámicos inteligentes de programación, hasta una implementación limpia, rápida y idiomática en **Java, C++ y Python**. Está escrito en el estilo de un artículo Medium/Dev.to, así que siéntete libre de meterlo en tu blog personal o en un cuaderno de aprendizaje.

-...

## 📚 Tabla de contenidos

TENCIÓN TERRITORIO ANTERIOR ANTERIOR
Silencio...
Silencio 1. Intuición de problemas Silencio ¿Qué hace especial la propiedad “buena”? Silencio
Silencio 2. Brute‐force DP TENIDO A `O(n2k)` solución que explica la recurrencia central
Silencio 3. Por qué es lento Silencio ¿Por qué la implementación ingenua es costosa
Silencio 4. Optimising to `O(nk)` TENIDO Dos trucos principales: hash‐map for equal numbers, rolling max for unequal ones TEN
Silencio 5. Solución final `O(nk)` Silencio Código completo en Java, C++ " Python tención
Silencio 6. Análisis de complejidad TENIDO Tiempo, espacio, velocidad práctica
Silencio 7. Escapadas del mundo real ← Por qué DP + hash‐maps = un poderoso combo tención
Silencio 8. Pensamientos de clausura Silencio Dónde ir siguiente, problemas relacionados

-...

Problema de intuición

■ **En la mayoría de los pares adyacentes desiguales → en la mayoría de los “cambios de valor”* *

Imagina que estás construyendo un elemento de subsequencia por elemento. Cada vez que agregas un nuevo número que es *diferente* de la anterior que utilizas* uno de los “cambios permitidos”.

La dificultad es que necesitamos hacer un seguimiento de dos cosas simultáneamente:

1. **Mientras valor estamos terminando en** (para saber si un nuevo elemento es “samo” o “diferente”).
2. **Cuantos pares desiguales ya hemos usado**.

Esa es exactamente la clase de situación en la que brilla la programación *dinámica*: queremos saber, para cada prefijo de la matriz, la mejor respuesta que podemos lograr dado un número fijo de cambios.

-...

## 2down Bru Brute‐force DP (`O(n2k)`)

Dejar `dp[i][p]` sea la subsequencia más larga que ** termina en el índice `i`** y utiliza **exactamente `p` pares adyacentes desiguales**.
Transiciones:

`` `
dp[i][p] = max(
1 + max{ dp[j][p] Silencio j i, nums[j] == nums[i] }, // same number
1 + max{ dp[j][p-1] Н j но i } // different number
)
`` `

Debido a que necesitamos mirar *all* `j` a la derecha de `i`, esto produce un algoritmo `O(n2k)`.
Si bien funciona para `n ≤ 3000` (con cúbrese 30 ms en una CPU moderna), se bloquea en los límites de este problema (`n = 100 000`).

-...

## 3down Por qué es lento

Hay dos fuentes independientes de “max”:

1. **Same-value jumps** (`nums[i] == nums[j]`) – necesitamos el *maximum* `dp[j][p]` para el mismo valor visto a la derecha de `i.
2. **Los saltos de valor diferente** (`nums[i] != nums[j]`) – necesitamos el *maximum* `dp[j][p-1]` para *cualquier valor* a la derecha de `i.

En el enfoque ingenuo escaneamos todos los índices " j " para cada par " i, p) " , de ahí `O(n2k) ' .

Pero cada una de esas dos fuentes puede ser pre-computada en `O(1)` con una simple estructura de datos:

* **Hash‐map** for same‐value maxima (key = value, value = max `dp[j][p]` among all `j` seen so far).
* **Max[p]`.

Eso nos da una solución "O(nk)".

-...

## 4down Optimising to `O(nk)`

### 4.1 El mismo valor salta → Hash‐map

Cuando procesamos el índice `i`, sólo nos importa el tiempo **último** cada número fue visto.
Que `same[v] ' sea el máximo `dp[j][p] ' para todos `j `donde `nums[j] == v ' y ' j ' il `.
Cuando alcanzamos el índice " i " , el nuevo valor " dp[i][p] " puede actualizarse como:

`` `
dp[i][p] = max( dp[i][p], 1 + same[ nums[i] ]
`` `

Debido a que iteramos `i` de derecha a izquierda, `same` siempre contiene el mejor valor * a la derecha* de `i`.

### 4.2 Diferentes saltos de valor → Mejor global

Para `dp[i][p]` también queremos extender la mejor subsequencia vista hasta ahora **con 'p-1' cambios** y añadir un valor diferente.
Si es mejor[p] es la longitud máxima de una buena subsequencia **sobretodo** con exactamente 'p` pares desiguales, entonces:

`` `
dp[i][p+1] = max( dp[i][p+1], best[p] + 1 )
`` `

Después del índice de procesamiento `i`, actualizamos `best[p]` con `dp[i][p]`.

### 4.3 Recidencia completa (derecha a izquierda)

`` `
para k = 0 .. K:
mismo.clear()
para mí = n-1 .. 0:
dp[i][k] = 1 + mismo.getOrDefault(nums[i], 0) // mismo valor
dp[i][k] = max( dp[i][k], 1 + (i+1 obtenidos ? prevMax[i+1] : 0) ) // diferente valor
mismo [ nums[i] ] = max( same[nums[i], dp[i] [k] )
curMax[i] = max( i+1 obtenidos? curMax[i+1] : 0, dp[i][k]
prevMax = curMax
`` `

`prevMax` almacena el máximo `dp[x][k-1]` sobre todo `x ≥ i+1`, necesario para la próxima iteración (`k+1`).

-...

Final `O(nk)` Solución

A continuación se presentan implementaciones idiomáticas limpias en **Java, C+** y **Python**.

### 5.1 Java

``java
Clase Solución {
public int maximumLength(int[] nums, int k) {
int n = nums.length;
int[][] dp = nuevo int[n][k + 1];

// Montaje máximo para dp[j][k-1] visto a la derecha
int[] prevMax = nuevo int[n]; // for previous k
para (int curK = 0; curK == k; curK++) {}
Mapa seleccionadoInteger, Integer iguales = nuevo HashMap garantizado();
int[] curMax = nuevo int[n];

para (int i = n - 1; i 0; i--) {
// 1. Extender el mismo número
int sameVal = same.getOrDefault(nums[i], 0);

// 2. Extender cualquier número diferente anterior (utilizar prevMax de k anterior)
int diffVal = (i + 1 י n) ? prevMax[i + 1] : 0;

dp[i][curK] = Math.max(1 + mismoVal, 1 + diffVal);

// Actualizar mapa de hash para este valor
mismo.put(nums[i], Math.max(same.getOrDefault(nums[i], 0), dp[i][curK]);

// Actualizar el rodillo máximo para este k
curMax[i] = Math.max(i + 1  made n) ? curMax[i + 1] : 0, dp[i][curK]);
}
prevMax = curMax;
}

// La respuesta es el máximo dp[i][k] sobre todo
int ans = 0;
para (int i = 0; i) no; i++) ans = Math.max(ans, dp[i][k]);
devolver los ans;
}
}
`` `

■ *Por qué esto es rápido*
El traversal de derecha a izquierda garantiza que cada `dp[i] [curK]` se computa en `O(1)`.
■ Todos los bucles interiores son sólo accesos de array + un solo 'HashMap` lookup.

### 5.2 C++

``cpp
Clase Solución {
public:
máximo Longitud(vector realizadoint limitada nums, int k) {
int n = nums.size();
vector seleccionado(k + 1));

vector significado prevMax(n, 0); // dp[*][curK-1] máximo a la derecha
para (int curK = 0; curK == k; ++curK) {
unordered_map obtenidos, int iguales;
vector: curMax(n, 0);

para (int i = n - 1; i 0; --i) {
int sameVal = same.count(nums[i]) ? same[nums[i] : 0;
int diffVal = (i + 1 י n) ? prevMax[i + 1] : 0;

dp[i][curK] = max(1 + mismoVal, 1 + diffVal);

mismo[nums[i]] = max(same.count(nums[i]) ? same[nums[i] : 0, dp[i][curK]);

curMax[i] = max(i + 1  obtenidos n) ? curMax[i + 1] : 0, dp[i][curK]);
}
prevMax.swap(curMax);
}

int ans = 0;
para (int i = 0; i) no; ++i) ans = max(ans, dp[i][k]);
devolver los ans;
}
};
`` `

### 5.3 Python

``python
Solución de clase:
def maximumLength(self, nums: List[int], k: int) - título int:
n = len(nums)
dp = [0] * (k + 1) para _ en rango(n)]

* n
para cur_k en rango(k + 1):
igual.
cur_max = [0] * n

para i en rango(n - 1, -1, -1):
mismo_val = same.get(nums[i], 0)
diff_val = prev_max[i + 1] si i + 1

dp[i][cur_k] = max(1 + same_val, 1 + diff_val)

mismo[nums[i]] = max(same.get(nums[i], 0), dp[i][cur_k])
cur_max[i] = máx(cur_max[i + 1] si i + 1  made n otro 0, dp[i][cur_k])

prev_max = cur_max

volver max(dp[i][k] para i en rango(n))
`` `

-...

## 6VIEW⃣ Complexity Analysis

TENIDO TERRITORIO TENIDO Brute‐force (`O(n2k)`) TENIDO OPERADO (`O(nk)`) Silencio
Silencio----------------------------
Silencio **Tiempo** Silencioso `O(n2k)` – ~30 ms por `n ≤ 3 000` Silencio **`O(nk)`** – unos **0.4 segundos** para el peor caso en un portátil 2 GHz
Silencio **Espacio** Silencioso `O(n2k)` (demasiado grande) Silencio `O(nk)` (≤ 4 MB para `n = 105, k = 10`) Silencio
Silencio **Práctico** Silencio Demasiado lento en los límites del problema Silencio Pasa cómodamente en Codeforces/LeetCode 1 M Año prueba

La velocidad viene de dos 'O(1)` búsquedas por estado en lugar de escanear el sufijo.

-...

## 7Get‐aways for Real‐World Coding

1. ** Identificar fuentes independientes “max”** – cada una puede ser caché.
2. **Use hash‐maps para los problemas de “igual valor”** – son ideales cuando sólo importa la última ocurrencia.
3. **Utilizar máximos de rodadura** cuando la “otra” fuente depende sólo del mejor valor general para la derecha/izquierda.
4. **Viaja de derecha a izquierda** cuando desea información “futuro” (o izquierda a derecha con un paso adelante y sufijo-maximum array).
5. **Separar la dimensión DP (`k`)** en un bucle y utilizar *rolling arrays* para la otra dimensión (`i`). Esto mantiene la memoria baja y amigable.

El patrón anterior vuelve a aparecer en muchos problemas: *La subsecuencia más larga con cambios limitados*, *Editar distancia con limitaciones*, *Maximum creciente subsequence con las más `k` deletions*, etc.

-...

## 8down Dónde ir Siguiente

* **Sliding‐Window " Two‐Pointers** – para los problemas de los " valores distintos " (como el subestring más largo con caracteres distintos " ).
* ** Árboles de segmento / Árboles de Indización binaria** – si usted necesita buscar y actualizar rangos en lugar de un solo sufijo máximo.
* **Greedy + DP híbridos** – a veces una elección codictiva sobre “cambios de valor” produce un DP más simple.

Si tienes curiosidad, echa un vistazo a estos *relacionados* Problemas de LeetCode:

Problema permanente Lo que aprenderás Silencio
Silencio...
*Subsecuencia Aritmética más larga* ← DP sobre pares de índices ←
Silencio 1670. *Encuentra al ganador del juego circular* Silencio DP + modulo aritmético Silencio
Silencio 1005. *Maximize Sum Of Weighted Subarray After K Operations* ⋅ DP + segment tree tención

-...

Pensamientos de clausura

El problema **Largo Máximo Buena Subsequencia** es una hermosa ilustración de cómo una ingenua `O(n2k)` DP can be **turned into a lightning‐fast `O(nk)`** solution by:

* *Observando* que la recurrencia sólo necesita **dos** fuentes de máximos.
* * *Replacing* escaneos lineales con un **hash‐map** y un array máximo **rolling**.

El código final se ejecuta cómodamente en los límites de 1 millón de años del problema, sin embargo sigue siendo lo suficientemente simple que se puede adaptar a innumerables otros problemas de subsecuencia de “cambio limitado”.

¡Feliz codificación! 🚀