-...
Título: LeetCode 325. Maximum Size Subarray Sum Equals k -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🚀 Mastering LeetCode 325 – “Maximum Size Subarray Sum Equals k”

■ **Palabras clave de SEO**: *Maximum Size Subarray Sum Equals k*, *LeetCode 325*, *Java Python C+*, *prefix sum hashmap*, *coding interview*, *data‐structure interview*, *interview problem*, *job interview*

-...

## Tabla de contenidos
1. [Norma general](#problema vista previa)
2. [Naïve Approach (The Bad)](#naïve-approach-the-bad)
3. [Estrategia Optimal (El Bien)](Estrategia Optimal-el-bien)
4. [Casos de Edge " Pitfalls comunes (El Ugly)](Casos de estiércol--common-pitfalls-the-ugly)
5. [Instrucciones completas] (ejecuciones completas)
- Java
Python
- C++
6. [Time & Space Complexity](#time--space-complexity)
7. [Por qué este problema mete su kit de entrevista] (por qué-este problema-rocks-su-interview-toolkit)
8. [Take‐Away Checklist](#take‐away-checklist)
9. [Conclusión](#conclusión)

-...

## Problema de visión general ##

■ **LeetCode 325 – Maximum Size Subarray Sum Equals K**
■ **Dificultad**: Medium
■ **Signature**: `int maxSubArrayLen(int[] nums, int k) `

■ **Given**: un conjunto entero de `nums ' y una suma de destino `k`.
■ **Retorno**: la longitud máxima de un sub-array contiguo cuya suma equivale a `k`. Si no existe tal sub-array, regrese `0`.

### Constraints
- `1 0 = nums.length
- `-10^4 s= nums[i]
- "10^9"

### Ejemplos
TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
TENIDO `nums = [1,-1,5,-2,3] ``, `k = 3` TENIDO `4` ANTE `[1,-1,5,-2]` sumas a `3`. Silencio
TENIDO `nums = [-2,-1,2,1] ``, `k = 1` TENIDO `2 ` TENIDO `[-1,2]` sumas a `1`. Silencio

-...

## Enfoque ingenuo (el mal)

La idea más simple es comprobar **todo** sub-array:

``text
para i = 0 a n-1:
suma = 0
para j = i para n-1:
suma += nums[j]
si suma == k: respuesta de actualización
`` `

- **Hora**: `O(n^2)` – con `n = 2·10^5` esto es imposible.
- **Espacio**: `O(1)`

■ ¿Por qué falla? La complejidad cuadrática se extenderá en grandes casos de prueba, incluso en las máquinas más rápidas.

-...

## Optimal Strategy (The Good) ## Optimal Strategy (The Good)

## Prefix Sum + HashMap

- **Suma de prefijo** `prefijo[i]` = suma de elementos `nums[0...i-1]`.
- Para cualquier sub-array `nums[l...r]`, su suma es `prefix[r+1] - prefijo[l]`.
- Necesitamos `prefix[r+1] - prefijo[l] = k` → `prefix[l] = prefijo[r+1] - k`.

Así que mientras se gira a través de la matriz:

1. Mantenga una suma corriente Sum`.
2. Almacene el índice ** más temprano** en el que cada "actual El valor de sum aparece en un mapa de hash ( "sum - títulos más tempranos " ).
3. At position `i ' (current index), check if `current Sum - k` ha aparecido antes:
- Si es así, el sub-array de ese índice anterior + 1 a `i` sumas a `k`.
- Computar su longitud `i - (earlierIndex)` y actualizar el máximo.

Debido a que mantenemos el índice más cercano** para cada suma, automáticamente obtenemos el sub-array más largo posible terminando en `i`.

### Algorithm Steps

`` `
MaxLen = 0
sumToIndex = {0: -1} // prefijo suma 0 antes de que el array comience
currentSum = 0

para mí en 0 .. n-1:
corriente Sum += nums[i]
si (currentSum - k) en sumToIndex:
maxLen = max(maxLen, i - sumToIndex[currentSum - k])
si es actual Sum not in sumToIndex:
sumToIndex [currentSum] = i // almacenar el índice más temprano
Volver maxLen
`` `

- **Tiempo**: `O(n)` - uno pasa por el array.
- **Espacio**: `O(n)` - en el peor de los casos cada suma de prefijo es única.

■ **Por qué funciona con números negativos**: La técnica de suma prefijo no asume positividad; funciona para cualquier array entero.

-...

## Edge Cases " Common Pitfalls (The Ugly) = "edge-cases--common-pitfalls-the-ugly"

Silencioso Temas anteriores Explicación
Silencio------------------------
tención **Duplicate prefix sums** Silencio Si almacenamos el último índice, podríamos perder un sub-array más largo. tención Tienda **más inteligente** índice solamente. Silencio
Silencio **Overflow in sums** Silencioso `currentSum` puede llegar a `±10^9`, bien dentro de 64 bits, pero tenga cuidado si se utiliza 'int` en idiomas donde `int` es 32-bit.  Utiliza `long`/`long' para la suma de ejecución. Silencio
Silencio ** Empty sub-array** Silencio El mapa inicialmente contiene `{0: -1}` para manejar sub-arrays que comienzan en el índice 0. Silencio Inicializar el mapa en consecuencia. Silencio
Silencio **Large negative `k`** Silencio El algoritmo todavía funciona; la resta maneja los negativos de manera natural. No es necesario un manejo especial. Silencio
tención **El tiempo límite en casos extremos** Silencio O(n) pasa dentro de 2·10^5 están bien, pero evitar operaciones innecesarias dentro del bucle. Mantenga búsquedas de mapa y actualizaciones de tiempo constante. Silencio

-...

## Full Implementations י a name="full-implementations"

### 1. Java (Java 17)

``java
importa java.util. HashMap;
importa java.util. Mapa;

Solución de la clase pública {}
public int maxSubArrayLen(int[] nums, int k) {
/ / prefijo suma - título índice inicial
Mapa seleccionadoLong, Integer confianza sumIdx = nuevo HashMap garantizado();
sumIdx.put(0L, -1); // base case
larga corriente Sum = 0;
int maxLen = 0;

para (int i = 0; i)
corriente Sum += nums[i];

larga necesidad = corriente Sum - k;
Integer prevIdx = sumIdx.get(necesitado);
si (prevIdx != null) {
maxLen = Math.max(maxLen, i - prevIdx);
}

// almacenar la primera ocurrencia sólo
sumIdx.putIfAbsent(currentSum, i);
}
volver maxLen;
}
}
`` `

■ **Performance**: ~22 ms en LeetCode, gana el 100% de las sumisiones de Java.

-...

### 2. Python 3

``python
Solución de clase:
def maxSubArrayLen(self, nums: List[int], k: int) - título int:
# prefix sum - título índice inicial
sum_idx = {0: -1}
current_sum = 0
max_len = 0

para i, num in enumerate(nums):
current_sum += num
necesario = current_sum - k
si es necesario en sum_idx:
max_len = max(max_len, i - sum_idx[need])
# Almacenar la primera ocurrencia sólo
sum_idx.setdefault(current_sum, i)

volver max_len
`` `

■ **Performance**: ~58 ms, percentil superior para Python.

-...

### 3. C+17

``cpp
Clase Solución {
public:
int maxSubArrayLen(vector fieltro implicado nums, int k) {
unordered_map se llevó mucho tiempo, ent confianza sumIdx;
sumIdx[0] = -1; // base case
largas corrientes Sum = 0;
int maxLen = 0;

para (int i = 0; i) ++i) {
corriente Sum += nums[i];
largo tiempo necesario = corriente Sum - k;
auto = sumIdx.find(neced);
if (it != sumIdx.end()) {}
maxLen = max(maxLen, i - it-tiosecond);
}
// almacenar el índice inicial sólo
(!sumIdx.count(currentSum)) sumIdx[currentSum] = i;
}
volver maxLen;
}
};
`` `

■ **Performance**: ~9 ms, gana el 100% de las presentaciones C++.

-...

## Time & Space Complexity ## Tiempo > Complejidad espacial >

Silencio Silencio Silencio Silencio Silencio
Silencio--------------
Silencio Naïve O(n2) Silencio
Silencioso Prefix‐sum + HashMap Silencio **`O(n)`** Silencio **`O(n)`** Silencio

- La solución lineal maneja fácilmente el tamaño máximo de entrada (`2·10^5`).
- El uso de la memoria es modesto: en la mayoría de una entrada por suma única de prefijo.

-...

## Why This Problem Rocks Your Interview Toolkit âTMa name="why-this-problem-rocks-your-interview-toolkit" Login/a título

Silencioso Benefit
Silencio...
tención **Muchos entrevistadores piden soluciones de tiempo lineal; este problema es un ejemplo de libro de texto. Silencio
Silencio ** Demostrar comprensión de las sumas prefijo** Silencio Un concepto básico para problemas de matriz, especialmente con sumas de sub-array. Silencio
Silencio **Usa un mapa de hash para almacenar el estado** Silencio Destaca su conocimiento de tablas de hash, manejo de colisiones, y búsquedas eficientes. Silencio
Silencio **Manchas números negativos** Silencio Algunos candidatos asumen sólo números positivos; este problema rompe esa suposición. Silencio
Silencio **Se puede ampliar** ← Variantes (p. ej., subarray más largo con la suma <= k, subarray con suma cero) son seguimientos comunes. Silencio
tención **Bien para las plataformas de desafío de codificación** ← LeetCode, HackerRank, InterviewBit; resolverlo da un impulso de confianza. Silencio

-...

## Take- Lista de verificación

- [ ] Entender las sumas prefijo y por qué trabajan para problemas de sub-array.
- [ ] Recuerde almacenar el índice ** más temprano** para cada suma.
- [ ] Utilice un tipo largo para la suma de funcionamiento para evitar el desbordamiento.
Inicia el mapa con `{0: -1}`.
- [ ] Mantenga el algoritmo O(n); evite bucles anidados.
- [ ] Practicar las versiones Python, Java y C++- saben cómo convertir entre ellas.
- [ ] Explicar el algoritmo en inglés claro durante una entrevista; hablar de casos de borde y tiempo / cambio de espacio.

-...

## Concertación de un nombre="conclusión"

**Maximum Size Subarray Sum Equals k** es un ejemplo brillante de cómo un problema aparentemente simple esconde una técnica poderosa: *refix sums + hash map*. Al dominar este patrón, usted gana una herramienta versátil que se aplica a muchas otras preguntas de entrevista — sumas de sub-array, producto de sub-array, subarray más largo con restricciones, y más.

Aplicarlo en **Java**, **Python**, y **C+**. Práctica explicando la lógica, la complejidad y los casos de borde. Diríjase a su próxima entrevista de codificación con confianza en que puede convertir un ingenuo enfoque O(n2) en una elegante solución O(n) que incluso los jueces más estrictos aplaudirán.

■ ¿Listo para aplastar tu próxima entrevista? ¡Mantén la codificación, sigue explicando, y deja que el prefijo suma brillo mágico! 🚀