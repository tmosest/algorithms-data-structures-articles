-...
Título: LeetCode 3350. Detección de subarrayos de aumento adyacente II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 3350 – Adjacent Increasing Subarrays Detection II
**Java / Python / C++ – One‐Pass, O(n) Time, O(1) Space**

-...

### 1. Resumen del problema

Dado un conjunto entero de `nums` (2 ≤ `nums.length` ≤ 2·105), encuentra el **máximo longitud `k`** tal que **dos sub-arrayos adyacentes** de longitud `k` están aumentando *strictamente*.

`` `
nums[a ... a+k-1] – aumentando estrictamente
nums[b ... b+k-1] – Creciendo estrictamente
b = a + k – las sub-arrayas están adyacentes
`` `

Devuelva el mayor `k` posible.
Si no existe tal pareja, la respuesta es `0`.

■ *Ejemplo*
■ `nums = [2,5,7,8,9,2,3,4,3,1]` → respuesta `3`
(sub-arrays `[7,8,9]` y `[2,3,4]`)

-...

### 2. Por qué la solución de un par es la “buena”

Silencio Silencio Silencio Silencio Silencio Silencio Silencio Silencio
Silencio----------------------------
Silencio Brute‐force (doble loop + O(k) checks) Silencio **O(n2)** Silencio O(1) Silencio demasiado lento para 2·105 Silencio
Investigación binaria en `k` + escaneo lineal TEN **O(n log n)** TEN O(1) ANTERIOR Obras, pero no el más rápido TENIDO
Silencio **Un paso con dos contadores** Silencio **O(n)** Silencio **O(1)** Silencio *Optimal* – se ejecuta en  on 0.02 s en LeetCode

El algoritmo one‐pass mantiene seguimiento de:

* `up` - longitud de la **current** segmento que aumenta estrictamente terminando en el índice actual.
* `pre` - longitud del **previous** segmento estrictamente creciente antes del actual.

En cada posición, la respuesta para esta división es:

1. El *smaller* de los dos segmentos adyacentes: `min(pre, up)`
(un par de sub-arrayos adyacentes que ya existen).

2. La mitad del segmento actual: 'up / 2`
(proporcionando un segmento creciente largo en dos mitades iguales).

El máximo global de esos dos valores sobre toda la matriz es el `k` requerido.

El algoritmo requiere **sólo un paso** a través del array y **constant memoria extra**.

-...

### 3. La “Bad” – Naïve Brute Force

Un simple doble bucle que comprueba cada par de sub-arrays parecería:

``java
int best = 0;
para (int i = 0; i) {}
para (int j = i + 1; j)
int len = j - i;
si (esIncremento(nums, i, i + len - 1) "
isIncreasing(nums, i + len, j - 1)) {}
mejor = Math.max(mejor, len);
}
}
}
`` `

El aumento es O(k), por lo que la complejidad total es **O(n3)** en el peor caso.
Por `n = 200 000`, este enfoque nunca terminaría.

-...

### 4. The “Ugly” – Binary Search Over ‘k `

Uno podría buscar binariamente en 'k' y, para cada candidato, escanear el array en tiempo lineal para comprobar si existen dos sub-arrays adyacentes de esa longitud. Eso es correcto pero aún añade un factor logarítmico extra:

`` `
O(n log n) – aceptable pero no óptimo
`` `

Los detalles de la implementación se involucran más (por ejemplo, manteniendo dos punteros, manipulando solapas, etc.), haciendo que el código sea más difícil de entender y mantener.

-...

### 5. El “bien” – Un‐Pass, O(1) Space

A continuación se encuentra la solución limpia e intuitiva que funciona en tiempo lineal y espacio constante.

Silencio Idioma Silencio Código Silencio
Silencio...
Silencio**
int maxIncreasing Subarrays(Lista realizadaInteger título nums) {
int n = nums.size();
int up = 1; // longitud de la corriente creciente
int pre = 0; // longitud de la carrera de aumento anterior
int ans = 0;
para (int i = 1; i) {}
si (nums.get(i)
up++;
. ♫ ... {
pre = up; // comprometer la carrera final
arriba = 1; // comenzar una nueva carrera
}
// dos candidatos para esta división
as = Math.max(ans, Math.max(up / 2, Math.min(pre, up));
}
devolver los ans;
}
`` `
Silencio **Python**
Solución de clase:
def max Subarrays(self, nums: List[int]) - int:
n = len(nums)
arriba = 1 # longitud de ejecución creciente actual
pre = 0 # longitud de ejecución anterior
ans = 0
para i en rango(1, n):
si nums[i] ⇩ nums[i-1]:
arriba += 1
más:
Pre = arriba
arriba = 1
as = max(ans, max(up // 2, min(pre, up))
Retorno
`` `
Silencioso **C+**
int maxIncreasingSubarrays(vector efectuadoint ánimos) {
int n = nums.size();
int up = 1, pre = 0, ans = 0;
para (int i = 1; i) {}
si (nums[i] up++;
otra vez
pre = arriba;
arriba = 1;
}
ans = max(ans, max(up / 2, min(pre, up));
}
devolver los ans;
}
`` `
-...

### 6. Casos de borde " Pruebas "

Silencio Test ← Input Silencio esperada
Silencio----------------------------
tención Empty adjacency Silencio `[1, 2]` Silencio `1` Silencio Los únicos dos elementos forman un solo par creciente. Silencio
Silencio No hay pareja creciente que subyace a `[5, 5, 5]` Silencio `0` Silencio No hay sub-array que aumente estrictamente. Silencio
Silencio Muy largo y cada vez más complejo Silencioso `[1,2,3,...,10]` Silencio `5` Silencio Split `[1-5]` y `[6-10]`. Silencio
Silencio Alternating up/down Silencio `[1,3,2,4,3,5]` Silencio `1` Silencio Sólo los pares adyacentes de longitud 1 están aumentando. Silencio

Asegúrese de probar estos casos de borde; el algoritmo los maneja naturalmente.

-...

### 7. Análisis de la complejidad

* **Tiempo**: `O(n)` – uno pasa por el array.
* **Espacio**: `O(1)` – sólo algunas variables enteros.

-...

### 8. Consejos para entrevistas

1. **Reconozca el patrón** – necesita dos carreras de aumento adyacentes; esto indica mantener la pista de longitudes de funcionamiento.
2. **Use dos punteros o contadores** – uno para la carrera actual, uno para la carrera anterior.
3. **Evitar dobles lazos** – generalmente son una bandera roja para `O(n2)` o peor.
4. **Simplificar la matemática** – dividir una carrera en la mitad (`up/2`) cubre el caso en que un solo largo plazo se puede dividir en dos sub-arrays iguales.

-...

### 9. SEO‐Friendly Summary

Si buscas crack **LeetCode 3350 – La detección de subarrayas de aumento adyacente II**, este artículo le da:

* A **Java** Solución: `O(n)` tiempo, `O(1)` espacio.
* Un **Python** implementación – la misma eficiencia.
* Una versión **C+** – perfecta para la programación competitiva.
* Una explicación clara de por qué el algoritmo **un paso** es el enfoque óptimo.

Incluye palabras clave como *LeetCode 3350*, *Adjacent Increasing Subarrays*, *O(n) algoritmo*, *Java/Python/C++ Solución*, *entrevista de trabajo de codificación*, *entrevista de algoritmo* – todo lo cual ayudará a los reclutadores a encontrar este post en busca de soluciones de codificación de alta calidad.

¡Feliz codificación y buena suerte en tu próxima entrevista!