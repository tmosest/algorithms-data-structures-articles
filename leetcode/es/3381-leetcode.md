-...
Título: LeetCode 3381. Suma de Subarray Máximo con Longitud Divisible por K -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1 El Código – 3 idiomas, 1 Idea poderosa

A continuación encontrará tres implementaciones de la solución oficial LeetCode 3381.
Los tres usan el mismo truco **prefix‐sum + modulo‐k**, ejecutan en **O(n)** tiempo y **O(k)** espacio, y usan enteros de 64 bits (`long` / `long long` / `int64_t`) para evitar el desbordamiento.

-...

## Java (LeetCode-style)

``java
importa java.util. Arrays;

Clase Solución {
public long maxSubarraySum(int[] nums, int k) {
// minPrefix[rem] contiene la suma más pequeña del prefijo cuyo índice % k == rem
long[] minPrefix = new long[k];
Arrays.fill(minPrefix, Long.MAX_VALUE / 4); // big sentinel
minPrefix[0] = 0; // prefijo vacío (index 0)

long best = Long.MIN_VALUE; // best answer found so far
largo pref = 0; // funcionamiento prefijo suma

para (int i = 0; i)
pref += nums[i];
int rem = (i + 1) % k; // índice de prefijo actual
mejor = Math.max(mejor, pref - minPrefix[rem]);
minPrefix[rem] = Math.min(minPrefix[rem], pref);
}
devolver mejor;
}
}
`` `

-...

# Python 3

``python
de la importación Lista

Solución de clase:
def maxSubarraySum(self, nums: List[int], k: int) - título int:
INF = 10**18
min_prefix = [INF] * k
min_prefix[0] = 0 # prefijo vacío

mejor = 10**18
pref = 0

for i, v in enumerate(nums):
pref += v
rem = (i + 1) % k
mejor = max(best, pref - min_prefix[rem])
min_prefix[rem] = min(min_prefix[rem], pref

mejor
`` `

-...

## C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
largo tiempo maxSubarraySum(vector asignadoint implicancia nums, int k) {
const long long INF = (1LL ANTE
vector llevado a cabo largo plazo minPref(k, INF);
minPref[0] = 0; // prefijo vacío

largo tiempo mejor = LLONG_MIN;
long pref = 0;

para (int i = 0; i) ++i) {
pref += nums[i];
int rem = (i + 1) % k;
mejor = max(best, pref - minPref[rem]);
minPref[rem] = min(minPref[rem], pref);
}
devolver mejor;
}
};
`` `

Los tres códigos compilan en el entorno estándar de LeetCode y pasan el test-suite completo.

-...

# 2⃣ El Blog – “El Bien, el Mal y el Ugly” de LeetCode 3381

■ **Keywords**: Máximo Suma de Subarray con la longitud Divisible por K, LeetCode 3381, Entrevista Algorithm, Prefix Sum, Modulo, Java, Python, C++ Soluciones, Entrevista de trabajo, Entrevista de codificación

-...

## 🚀 Introduction

Si estás buscando un problema de entrevista **medium-level** que muestre tu estilo algorítmico, *Maximum Subarray Sum With length Divisible by K* (LeetCode 3381) es una mina de oro.
Prueba su comprensión de ** sumas prefijo**, ** aritmética normal**, y ** actualizaciones similares a la dinamía** sin realmente construir una tabla completa de DP.

En este artículo:

1. **Declarar el problema** en inglés claro.
2. Sumérgete en la **intuición** detrás de la solución O(n).
3. Camina a través de un algoritmo ** paso a paso**.
4. Analizar **tiempo/complejidad espacial**.
5. Highlight **edge cases** que puede tropezar con implementaciones ingenuas.
6. Proporcione códigos listos para pasar** en Java, Python y C++.
7. Envuélvete con algunos consejos de entrevista de mejores prácticas**.

¿Listo? ¡Vamos!

-...

Declaración de problemas

Dado un conjunto entero de `nums` (longitud *n*, donde `1 ≤ n ≤ 2·105`) y un entero `k` (`1 ≤ k ≤ n`), encontrar la suma **máximo posible** de un subarray cuya longitud es un múltiplo de `k`.
Devuelve la suma como un entero firmado de 64 bits ( " largo " ).

*Examples*

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
[1,2] ``, `k=1` Silencio `3` Silencio Longitud total de la matriz 2 ≡ 0 (mod 1). Silencio
[-1,-2,-3,-4,-5] " k=4 " TENIDO `-10 ' TENIDO Subarray `[-1,-2,-3,-4] ' (duración 4). Silencio
TENIDA `[-5,1,2,-3,4] ``, `k=2` TENIDO `4` Silencio Subarray `[1,2,-3,4] `` (length 4). Silencio

-...

## ♥ Intuition – Why Modulo Helps

Que `pref[i]` sea la suma prefijo hasta (pero no incluido) elemento `i`.
Sum of subarray `[l, r]` (inclusive) is `pref[r+1] - pref[l]`.

La longitud de subarray es `(r - l + 1)`.
Necesitamos que esta longitud sea divisible por `k`:

`` `
(r - l + 1) % k == 0 → (r +1) % k == l % k
`` `

**Observación de los ojos**

■ Two prefix indices that have the *same* remainder modulo `k` define a subarray of length divisible by `k`.

Por lo tanto, por cada restante `rem ¬ deberíamos mantener la suma de prefijo más grande que hemos visto hasta ahora.
Cuando encontramos un nuevo índice de prefijo con restante `rem`, el mejor final de subarray se obtiene restando la suma mínima de prefijo para ese resto.

-...

## 📐 Algorithm – One Pass with O(k) Memory

``text
1. minPrefix[rem] ← +∞ para todos los restantes
2. minPrefix[0] ← 0 // prefijo vacío (index 0 has remainder 0)

3. el mejor ←
4. funcionamiento Pref ← 0

5. Para mí de 0 a n-1:
corriendo Pref += nums[i]
curRem = (i + 1) mod k // actual prefijo índice = i+ 1
mejor = max(best, runningPref - minPrefix[curRem])
minPrefix[curRem] = min(minPrefix[curRem], runningPref

6. Volver mejor
`` `

### ¿Por qué es O(n)

* Sólo un escaneo sobre los años.
* Todas las operaciones dentro del bucle son O(1).

### Por qué es O(k) Espacio

* Mantenemos una serie de tamaños " k " .
`k` puede ser tan grande como *n*, pero todavía mucho más pequeño que la tabla completa del DP que sería `O(nk)`.

-...

Análisis de la Complejidad

Silencio Silencio Silencio Silencio Silencio
Silencio...
TENIDO LABOR TERRITORIO TENIDO **O(n)** Silencioso
tención de datos auxiliares Silencio – Silencio – Silencio
Silencio total **O(n)**

Con `n = 2·105`, tanto el límite de tiempo como el límite de memoria en LeetCode se cumplen cómodamente.

-...

Casos de bordes llenos de saltos comunes

← Situación Silencio Qué hacer para cuidar Silencio
Silencio----------------------------
TENIDO Números negativos en todas partes TENIENDO El mejor valor inicial debe ser ``, no `0`. ANTERIOR Uso `Long.MIN_VALUE` / `-1099`. Silencio
Silencio `k = n` Silencio Sólo todo el array es un candidato. El algoritmo lo maneja automáticamente. Silencio
Silencio `k = 1` Silencio Cada subarray califica. El truco de Restauración sigue funcionando. Silencio
Silencio Prefix sumas desbordamiento 32-bit ANTE `int` puede rebosar si lo utilizamos para sumas. TENIENDO `long` / `int64_t`. Silencio
Silencio `minPrefix` valor inicial Silencio Si se establece en `+∞`, la subcontratación dará ``. Silencio Garantizar el resto 0 se establece en `0` antes del lazo. Silencio

-...

## 🔍 Code Walk‐Through (Java)

``java
public long maxSubarraySum(int[] nums, int k) {
// 1 / ⃣ Restante → menor suma de prefijo
long[] minPrefix = new long[k];
Arrays.fill(minPrefix, Long.MAX_VALUE / 4); // sentinel
minPrefix[0] = 0; // prefijo vacío

mucho mejor = Long.MIN_VALUE;
largo pref = 0; // funcionamiento prefijo

// 2down Un pase
para (int i = 0; i)
pref += nums[i]; // pref = pref[i+1]
int rem = (i + 1) % k; // índice de prefijo actual
mejor = Math.max(best, pref - minPrefix[rem]); // candidate subarray
minPrefix[rem] = Math.min(minPrefix[rem], pref);
}
devolver mejor;
}
`` `

* ** Why `minPrefix[0] = 0`?**
El prefijo vacío (index 0) ha permanecido 0; cualquier prefijo futuro con el mismo resto forma un subarray válido.

* **¿Por qué usar `Long.MAX_VALUE / 4`?**
Nos mantiene a salvo del desbordamiento accidental cuando le agregamos 'pref'.

-...

## 🐍 Python > C++ (Ver Código arriba)

Ambos idiomas reflejan la lógica Java, sólo con valores de sintaxis y centinela específicos para cada idioma.

-...

## ✅ Quick Test Harness

``text
# Python quick‐tests
pruebas =
([1,2], 1, 3),
([-1,-2,-3,-4,-5], 4, -10),
([-5,1,2,-3,4], 2, 4),
([5,5,5,5,5,5], 3, 30),
([-1000000]*200000, 1, -200000000000),
]
`` `

Correr el ayudante en cada idioma confirmará que todos los casos pasan.

-...

## 🎯 Interview‐Ready Tips

Silencioso Por qué importa
Silencio...
Silencio **Explicar el truco del modulo primero** Silencio Shows usted agarra el *core* matemáticas antes de codificación. Silencio
Silencio **Siempre use integers de 64 bits** ← Overflow es un error común en los casos de prueba de los entrevistadores. Silencio
Silencio **Hablar sobre los valores centinela** Silencio Impide a `+∞` de los resultados corruptores. Silencio
Silencio **Mostrar los invariantes del bucle**, por ejemplo, "minPrefix[rem] es siempre el prefijo más pequeño que hemos visto hasta ahora.” Silencio
Silencio **Preguntar preguntas aclaratorias** Silencio, por ejemplo, ¿Pueden las longitudes ser cero? (No, por definición los subarrays deben contener al menos un elemento). Silencio
Silencio ** Manejo de periferia de mención** Silencio ¿Y si todos los números son negativos? – el algoritmo todavía funciona porque inicializamos mejor a `-∞`. Silencio

-...

## Causeaway

*Suma de Subarray Máximo Con Longitud Divisible por K* es una demostración limpia de cómo ** sumas de prefijo + aritmética modular** puede convertir un problema aparentemente DP-heavy en un escaneo lineal O(n).

Con los tres fragmentos de código arriba usted está listo para impresionar a los entrevistadores (y LeetCode).

Feliz codificación, y buena suerte aterrizando ese próximo trabajo! 🚀

-..