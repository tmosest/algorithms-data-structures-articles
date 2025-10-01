-...
Título: LeetCode 795. Número de Subarrays con Máximo Ligero -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 795. Número de Subarrayos con Máximo Ligero
## The Good, The Bad, and The Ugly – A Complete Interview‐Ready Guide

■ **Palabras clave de montaje**: *LeetCode 795, Número de Subarrays con Bounded Maximum, preparación de entrevistas, ventana deslizante, dos punteros, solución Java, solución Python, solución C++, O(N) tiempo, entero de 32 bits*

-...

## Tabla de contenidos
1. [Restatement del Problema](restatement del Problema)
2. [Intuición > Enfoque](#intuición--aprobación)
3. [Por qué la Solución Sliding-Window gana] (por qué la ventanilla-solución-ganancias)
4. [Detalles de implementación (Java, Python, C++)](Detalles de implementación)
5. [Edge Cases ' Pitfalls](#edge-cases--pitfalls)
6. [Análisis de complejidad](#complexidad-análisis)
7. [¿Qué hace este problema "El Ugly"?](#que-makes-este-problema-el-ugly)
8. [How to Talk About It in an Interview](#how-to-talk-about-it-in-an-interview)
9. [Takeaway ' Resources](#takeaway--resources)

-...

## Problema Restatement

■ **LeetCode 795** – *Número de Subarrayos con Máximo Ligero*
■ Dado un conjunto entero de `nums ' y dos enteros `izquierda ' y `derecha ' , devolver el número de subarrays contiguos y no vacíos de tal manera que el elemento máximo en el subarray se encuentra en el rango `[izquierda, derecha].
■ Todas las respuestas encajan en un entero firmado de 32 bits.

#### Ejemplo
`` `
nums = [2,1,4,3], izquierda = 2, derecha = 3
3 (subarrayos: [2], [2,1], [3])
`` `

-...

Intuición

### 1. The “Two‐Pointer” View
Un subarray satisface la condición **iff**:

* **Ningún elemento ître derecho** – de lo contrario el máx sería correcto.
* **Al menos un elemento ≥ izquierda** – de lo contrario el máx sería indicado.

Así que un subarray es válido cuando es un *segment* de la matriz que contiene **no elementos fuera de rango** y ** contiene al menos un elemento “bueno”** (≥ izquierda).

### 2. Conteo de subarrayos válidos eficientemente
En lugar de enumerar cada subarray (O(n2)), atravesamos el array una vez manteniendo:

Silencio Variable Silencio Significado Silencio Cómo se actualiza
Silencio----------------------------------------
← `última inválida` Índice de vida del elemento **último** que es el derecho de propiedad Silencio reiniciar el índice actual cuando este elemento se ve voca
latitud 'último bien' Silencioso índice del elemento **último** que es ≥ tóxico izquierdo actualizado cada vez que un buen elemento aparece

En el índice `i`, cada subarray que termina en `i` que comienza ** después de `último Inválido' y **incluye** `último bien' es válido.
Número de tales subarrays = `último bien - último inválido ' (si `últimamente bueno не último inválido ' , si no 0).

Acumular esto sobre toda la matriz → **O(n)** tiempo, **O(1)** espacio.

-...

## Por qué gana la solución Sliding-Window

← Críterion ← Sliding‐Window ← Brute‐Force Silencio DP (resumiendo prefijo)
Silencio----------------------------------...
Silencio **Tiempo** Silencio **O(n)** Silencio O(n2) Silencio O(n) pero con más frecuencia constante
Silencio **Espacio** Silencio O(1) Silencio O(1) Silencio
Silencioso **Implementación Simplicidad** Silencio ★★★ Silencio ★ ★ Silencio
Silencio **Intuición** Silencio Fácil de explicar Silencio difícil de comprender Silencio Necesitas prueba
Silencio **Edge‐Case Handling** ← Robust ← Necesidades anidadas bucles ← Necesita índices cuidadosos

El enfoque de la ventana deslizante es *el más fácil de entrevista* – conciso, probado y fácil de probar.

-...

## Implementation Details

A continuación se presentan tres implementaciones limpias y listas de producción.
Todos son **públicos**, ** seguros**, y manejan todos los casos de borde.

■ **Consejo:** Use `long` para el acumulador sólo si usted anticipa valores cercanos a `Integer. MAX_VALUE`.
■ El problema garantiza que el resultado se ajuste en 32 bits, por lo que `int` está bien.

## Java

``java
// Java 17+ (Lombok no requerido)
Solución de la clase pública {}
*
* Cuenta subarrays cuyo máximo está en [izquierda, derecha].
*
* @param nums el array de entrada
* @param izquierda límite inferior del máximo
* @param la parte superior derecha del límite máximo
* Número de retorno de subarrays válidos
*/
tuerca públicaSubarrayBoundedMax(int[] nums, int left, int right) {
int count = 0;
int lastInvalid = -1; // último índice donde nums[i]
el último Bien = -1; // último índice en el que nums[i] izquierda

para (int i = 0; i)
si (nums[i]
últimoInvalid = i; // ventana de reajuste
}
si (nums[i]
último Bien = i; // nuevo buen elemento
}
// número de subarrays que terminan en i que son válidos
si (último inválido) {
contar += último Bien, último. Inválido;
}
}
recuento de retorno;
}
}
`` `

-...

## Python

``python
# Python 3.9+
Solución de clase:
def numSubarrayBounded Max(self, nums, left, right):
"
:tipo nums: Lista[int]
:tipo izquierda: int
:tipo derecho: int
:rtype: int
"
Conteo = 0
último_inválido = -1 # índice de último derecho
último_bueno = -1 # índice de último izquierda

para i, val en enumerate(nums):
si vale > derecho:
Last_invalid = i
si vale izquierda:
ultimo_bueno = i

si te gusta Last_invalid:
contar += last_good - last_invalid

cuenta de retorno
`` `

-...

### C++

``cpp
// C+17
Clase Solución {
public:
int numSubarrayBoundedMax(vector identificadoint limitada nums, int left, int right) {
largo plazo = 0;
int last_invalid = -1; // último índice donde nums[i]
int last_good = -1; // último índice en el que nums[i] izquierda

para (int i = 0; i) ++i) {
si (nums[i]  correctamente) last_invalid = i;
si (nums[i]

si (último_bueno)
contar += last_good - last_invalid;
}
volver estática_cast seleccionado(cuenta); // cabe en 32 bit por problema
}
};
`` `

■ **¿Por qué utilizar 'long' para 'contar' en C++?**
■ Para evitar el desbordamiento intermedio cuando la longitud de la matriz es de 105 y todos los elementos están en rango – el número de subarrays puede alcanzar ~5 × 109 temporalmente, pero la respuesta final está todavía dentro de `int`.

-...

## Edge Cases " Pitfalls

La situación actual ¿Qué hacer?
Silencio----------------------
Silencio `nums` contiene sólo los valores ître right Silencio seguirá reiniciando `lat_invalid`; `last_good` nunca actualizado → respuesta 0 TEN Código ya maneja esto – sólo asegurar no división por cero. Silencio
Silencio Todos los valores dentro de `[izquierda, derecha]` Silencio Cada subarray es válido Silencio Código se acumula correctamente: `cuenta += i - (-1)` cada iteración. Silencio
Silencio Muy grande `izquierda ' 'derecha ' (por ejemplo, 109) tención La comparación todavía está bien tención Use literales de 64 bits si escribe constantes. Silencio
¿Números negativos? Las limitaciones del problema en la vida dicen: "nums[i] ?" No se necesitan cambios. Silencio
Silencioso matriz vacía (no permitida por restricciones) Silencio Código devolvería 0 Silencio No se requiere, pero seguro guardia: `si(nums.empty()) devuelve 0;` Silencio

-...

## Complexity Analysis

TEN TERRITOR TEN TEN ANTE
Silencio...
TENIDO Tiempo TENIDO **O(n)** – un paso sobre la matriz TENIDO
← Espacio Silencioso **O(1)** – sólo algunas variables enteros

-...

## Lo que hace ¿Este problema “El Ugly”?

1. Intuición de la fuerza bruta
Muchos entrevistados piensan que deben revisar cada subarray – O(n2).
La clave es darse cuenta de que los elementos “malos” (derecho de derecho) actúan como **breakpoints**.

2. **Hidden “Two‐Pointer” Insight**
La idea de la ventana deslizante no es obvia hasta que vea la *relación* entre los elementos *invalid* y *valid*.

3. *Edge‐Case Overlook*
Olvidar reiniciar `last_invalid` o mal cálculo `last_good - last_invalid` produce errores sutiles.

4. **Testing Complexity**
Los casos de prueba pequeños se ven bien; las pruebas de estrés (por ejemplo, 105 elementos dentro del rango) exponen el flujo entero si no tienes cuidado.

-...

## How to Talk About En una entrevista

1. **Clarificar las condiciones**
*“Necesitamos subarrays donde el máximo se encuentra en [izquierda, derecha]. Eso significa: ningún elemento derecho y por lo menos un elemento ≥ izquierda.*

2. **Explicar la observación clave**
*“Indices con valores > derecha dividieron el array en segmentos independientes. Dentro de cada segmento, sólo necesitamos saber cuántos subarrays contienen un buen elemento.”*

3. **Derive the O(n) Solution**
*“Mantenga dos índices: ‘last_invalid’ (más reciente √≥n derecho) y `last_good ' (más reciente ≥ izquierda). Para cada posición, el número de subarrays válidos que terminan en i es `max(0, last_good - last_invalid)`.*

4. **Discuss Edge Cases* *
*“Si todavía no hay buen elemento (“last_good == -1`) o el último bien es antes del último inválido, agregamos 0.”*

5. ** Complejidad de la mención**
*“Visitamos cada elemento una vez, por lo que O(n) tiempo y O(1) espacio.”*

6. **Optional: Provide a Second Approach**
*“Usted también podría hacer un DP de prefijo, pero es más pesado.”*

-...

## Takeaway & Resources

* **Idea clave:** Viento deslizante con dos índices que rastrean las últimas posiciones “malas” y “buenas”.
* **Tiempo de Salvación* Sólo un pase, O(n) tiempo.
* **Interview hack:** Explicar el concepto *breakpoint* – muestra una visión profunda.

■ *Práctica*
■ 1. LeetCode 795 (Easy to Medium).
■ 2. Problemas similares: *Número de Subarrays con Sum ≤ K*, *Subarray de Máximo del tamaño K*.
■ 3. Construir un pequeño arnés de prueba de unidad en cada idioma para verificar contra datos aleatorios.

-...

### Referencias

- Página del problema LeetCode: https://leetcode.com/problems/number-of-subarrays-with-bounded-maximum/
- Principales soluciones (Java, Python, C++): https://leetcode.com/problems/number-of-subarrays-with-bounded-maximum/solutions/
- Mi propia solución de ventanilla deslizante: (Inserta tu enlace de repo GitHub si está disponible)

-...

## Final Thought

La belleza de este problema radica en el hecho de que una pregunta aparentemente “difícil” de recuento se colapsa a dos índices simples. Domine este patrón, y tendrá una poderosa herramienta para muchos problemas de entrevista que implican **max/min limitaciones** o ** "no-bad-elements"** condiciones. ¡Feliz codificación!