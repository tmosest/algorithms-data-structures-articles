-...
Título: LeetCode 2229. Compruebe si un Array es consecutivo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Aplicación en tres idiomas

A continuación encontrarás tres soluciones *limpias y de producción* que resuelven **LeetCode 2229 – “Comprobar si un Array es consecutivo”** en **O(n)** tiempo y **O(n)** espacio auxiliar.
Los tres usan la misma idea:

1. Escanee el array una vez para encontrar los valores mínimos y máximos y para construir un `Set` (o `HashSet` / `unordered_set`) de todos los elementos.
2. Si la longitud del array es igual a `max – min + 1` * y* el tamaño del conjunto es igual a la longitud del array, el array contiene *todo* entero en esa gama → es consecutivo.

■ **Por qué este es el enfoque “bueno”* *
* Tiempo lineal – solo toca cada elemento una vez.
• Comprobaciones de membresía de tiempo constante a través de la piratería.
* Sin clasificación, sin pases adicionales sobre los datos.

Los tres fragmentos son comentados y listos para caer en su archivo de solución.

-...

## Java – O(n) Time, O(n) Space

``java
importa java.util. HashSet;
importa java.util. Set;

Solución de la clase pública {}
*
* Comproba si el array de entrada es consecutivo.
*
* @param nums el array de entrada (1 <= nums.length 0 0 = 1e5, 0 0 0 0 nums[i] י= 1e5)
* @return true if every number in [min(nums), min(nums)+nums.length-1] is present
*/
booleano público esConsecutive(int[] nums) {
// Copia defensiva: si el array está vacío, es trivialmente consecutivo
si (nums == null 0) Retorno verdadero;

Establecer:Integer nombrado = nuevo HashSet fiel(nums.length);
Int min = Integer. MAX_VALUE;
int max = Integer.MIN_VALUE;

para (int x : nums) {
visto.add(x);
si (x.
máx = x;
}

esperada Longitud = max - min + 1;
volver nums.length == expectedLength ' ven.size() == nums.length;
}
}
`` `

-...

### Python – O(n) Time, O(n) Space

``python
Solución de clase:
def isConsecutive(self, nums: list[int] Bool:
"
Regresar Verdaderamente sif `nums` contiene cada entero de min(nums)
a min(nums)+len(nums)-1 (inclusive).
"
si no nums: # lista vacía se considera consecutiva
Retorno

min_val = min(nums)
max_val = max(nums)
expected_length = max_val - min_val + 1

# A set guarantees O(1) average lookup; its size tell us if duplicates exist
visto = set(nums)
len(nums) == expected_length and len(seen) == len(nums)
`` `

-...

## C++ – O(n) Time, O(n) Space

``cpp
Incluido el título
#include ■unordered_set
#include >
#include < > >

Clase Solución {
public:
bool isConsecutive(std::vector efectuadointющ nums) {
si (nums.empty()) retornan verdadero; // caso borde: matriz vacía

int min_val INT_MAX, max_val = INT_MIN;
std::unordered_set visto;

para (int x : nums) {
visto.insert(x);
si (x) min_val) min_val = x;
máx_val = x;
}

int expected_len = max_val - min_val + 1;
volver nums.size() == expected_len " sensible() == nums.size();
}
};
`` `

-...

## 2. Blog Artículo – “El Bien, el Mal, y el Ugly of Checking Si un Array es Consecutivo”

■ **Meta Descripción**
■ Maestro el LeetCode “Comprobar si un problema de Array es consecutivo”. Aprenda la solución de tiempo lineal *buena*, por qué el enfoque de clasificación *bad* falla, y cómo evitar las trampas *muy*. Prepárate para entrevistas en Java, Python o C++.

#### Introduction

“**Comprobar si un Array Is Consecutive**” (LeetCode #2229) se ve engañosamente simple, pero es un clásico punto de entrevista que prueba su capacidad para razonar sobre rangos, duplicados y eficiencia algorítmica. Muchos candidatos llegan a un truco de clasificación o un barrido de dos puntos, pero esos enfoques pueden ser más lentos y difíciles de justificar en una entrevista con tiempo.

En este artículo diseccionamos el problema en tres partes:

Silencio Fase actual Lo que descubrirás Silencio Por qué importa Silencio
Silencio...
Silencio **El Bien** ← Solución lineal a tiempo, basada en el conjunto TENIDO Rápido, claro y fácil de explicar
Silencio **The Bad** Silencio Ordenar o repetir el escaneo Silencio Extra O(n log n) overhead Silencio
Silencio **El Ugly** ← Casos de Edge y manipulación duplicada ← Errores sutiles que rompen su solución

-...

### El problema en una gloriencia

■ **Given** un array entero `nums`.
■ *Retorno* *confianza* contiene **todo** entero en el intervalo `[min(nums), min(nums)+len(nums)-1]`.
■ **Else** devuelve `false`.

**Constraints* *
- `1 0 = nums.length
- `0 0 0 0 0 nums[i]

-...

## The Good – Linear‐time Set Solution

### Por qué es el mejor enfoque

1. **O(n) time** – un paso para encontrar `min`, `max`, y recoger elementos en un conjunto.
2. **O(n) espacio** – el conjunto tiene cada valor distinto.
3. **Ninguna clasificación** – evita el factor adicional `n log n`.
4. ** Los dispositivos duplican naturalmente** – el tamaño del conjunto equivale a la longitud del array si no hay duplicados.

### Step‐by‐Step

1. **Encuentra los valores mínimos (`min`) y máximo (`max`). #
2. **Construir un hash-set de todos los elementos. #
3. **Computar la longitud esperada**: `expected = max - min + 1`.
4. **Retorno** `nums.length == esperado ' set.size() == nums.length`.

### Pseudocode

`` `
función isConsecutive(nums):
si nums vacías: devolver verdadero
minVal = + dieta
maxVal = -∞
set = hash vacío

para cada x en nums:
set.add(x)
minVal = min(minVal, x)
maxVal = max(maxVal, x)

expectedLen = maxVal - minVal + 1
len(nums) == expectedLen and len(set) == len(nums)
`` `

### Java / Python / C++ Snippets

* (Véase la sección 1 supra para comentar completamente el código en cada idioma.) *

### Interview Tip

Explique que el conjunto no garantiza duplicados. Si el tamaño del conjunto difiere de la longitud del array, usted sabe que hay un duplicado y el array no puede ser consecutivo.

-...

## El malo – clasificación o doble escaneo

### Common Pitfall

Muchos candidatos ordenarán el array primero:

``java
Arrays.sort(nums);
int min = nums[0];
para (int i = 1; i)
si (nums[i] != min + i) devuelve falso; // detectar brecha o duplicado
}
`` `

### ¿Por qué es suboptimal

- **O(n log n)** tiempo debido a la clasificación, que es innecesario dada la solución lineal-time existe.
- La clasificación destruye el orden original, que podría ser un requisito en otros contextos.
- Requiere un pase adicional para validar brechas y duplicados, agregando factores constantes ocultos.

## When It might be Acceptable

Si usted está seguro de que el entrevistador sólo se preocupa por la *corrección* y no la optimización, o si `n` es extremadamente pequeño, un enfoque de clasificación puede estar bien. Pero para una matriz de 10^5, la parte superior es medible.

-...

## The Ugly – Edge Cases & Duplicate Handling

### Duplicate Numbers

La declaración del problema permite duplicados (por ejemplo, `1,1,2,3]`), pero un array consecutivo válido debe contener *todo* entero exactamente una vez.
*Código de errores*
``python
si len(set(nums)) == len(nums) y max(nums) - min(nums) + 1 == len(nums):
Retorno
`` `
Este código funciona, pero si olvidas el cheque de tamaño establecido, devuelves incorrectamente `True` para `[1,2,2,3]`.

### Empty Array

Las limitaciones garantizan por lo menos un elemento, pero una aplicación defensiva debe manejar `[]`.
**Buena práctica**: `si las nums.empty() vuelven verdaderas;` (o `falso' si lo prefieres).

## Números grandes > Desbordamiento

Con " valores in " hasta " 10^5 " , la expresión " máximo - min + 1 " no rebosará en enteros de 32 bits.
Sin embargo, si las restricciones eran más grandes, use un entero de 64 bits ( " largo " en Java, " largo " en C++).

### Performance Testing

Si no estás seguro de la linealidad, ejecute una micromarca de banco:

``java
int[] big = new int[100_000];
para (int i = 0; i) 100_000; i++) grande[i] = i;
nueva Solución().isConsecutive(big); // debe ser verdad
`` `

-...

## Take- Lista de verificación

Silencio TENIDO ANTERIOR ANTERIOR
Silencio...
TENIDO TENIENDO TENIDO Utilizar un hash-set para garantizar la búsqueda O(1) y la detección duplicada. Silencio
TENIDO TENIDO ANTERIOR Compute `min` y `max` en el mismo paso que la inserción del conjunto. Silencio
TENIDO TENIENDO ANTE Validate `nums.length == (max - min +1)` y `set.size() == nums.length`. Silencio
Silencio ❌ Silencio Evite ordenar a menos que tenga una buena razón. Silencio
Silencio ❌ Silencio No te olvides de manejar duplicados. Silencio
Silencio ❌ ¦ No asuma que el array no es vacío a menos que las restricciones lo garanticen. Silencio

-...

## Closing Thoughts

El problema “Check if an Array Is Consecutive” es un micro-tratamiento de *range logic* y *set-based uniqueness*. Al dominar la solución lineal usted no sólo marca puntos en LeetCode pero también demuestra a los entrevistadores que usted:

- **Conozca la complejidad** – puede elegir O(n) sobre O(n log n) cuando sea apropiado.
- **Understand data structures** – sets de hash de apalancamiento para cheques de membresía.
- **Código limpio, testable** - cada parte del algoritmo es aislado y fácil de razonar.

Buena suerte aplastando sus entrevistas de codificación, y seguir practicando – cada caso de borde que maneja ahora pagará dividendos más tarde!

-...

**Keywords:** LeetCode 2229, Compruebe si un Array es consecutivo, pregunta de entrevista, algoritmo, Java, Python, C++, O(n), hash set, clasificación de trampas, consejos de entrevista de codificación, entrevista de trabajo, ingeniería de software, estructuras de datos, complejidad del tiempo.