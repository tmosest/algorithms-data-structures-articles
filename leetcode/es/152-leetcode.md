-...
Título: LeetCode 152. Subarray de producto máximo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Mastering LeetCode 152 – “Maximum Product Subarray”
*(Java fort Python Silencio C++ implementaciones + SEO-friendly blog post)*

-...

Problema Recap

■ **Maximum Product Subarray* *
■ Dado un array entero `nums`, encontrar un sub-array **contiguo** con el producto ** más grande**, y devolver ese producto.

- 1 ≤ nums.length ≤ 2·104 `
- `-10 ≤ nums[i] ≤ 10
- La respuesta está garantizada para encajar en un entero firmado de 32 bits.

■ *Ejemplo*
[2, 3, -2, 4] → 6` (sub-array `[2,3]

-...

## 📈 Why It Matters

- **Entrevista favorita**: La mayoría de los entrevistadores piden una variación de este problema para medir su comprensión de *programación dinamica* y *adhesión por caso*.
- **El algoritmo de Krishna**: El problema de la suma de sub-array máximo clásico, pero con *multiplicación*, que introduce un giro.
- **Job‐search advantage**: Mostrando una solución limpia y idiomática en varios idiomas demuestra versatilidad a los reclutadores.

-...

## 🚀 The Idea: Keep Track of * Both* Max and Min

La multiplicación se comporta de manera diferente a la adición:

1. A *negative* times a *negative* → *positive*.
2. Un *positivo* veces un *negativo* → *negativo*.

Por lo tanto, al escanear la matriz debemos recordar **ambos** el producto máximo actual *ending* en el índice actual y el producto mínimo actual *ending* en el índice actual. El mínimo es esencial porque el próximo número negativo podría convertirlo en el nuevo máximo.

## Algorithm (Kadane-style)

`` `
max_so_far = nums[0]
current_max = nums[0]
current_min = nums[0]

para cada num en nums[1:]:
temp_max = current_max
current_max = max(num, temp_max * num, current_min * num)
current_min = min(num, temp_max * num, current_min * num)
max_so_far = max(max_so_far, current_max)

volver max_so_far
`` `

Un pase.
- **Espacio**: `O(1)` – sólo un puñado de variables.

-...

Código - Java, Python, C++

A continuación se muestran los snippets limpios y listos para la producción para cada idioma. Cada uno contiene comentarios y está listo para pegar en su editor LeetCode.

#### ## 1down⃣ Java

``java
*
* LeetCode 152 – Maximum Product Subarray
* Tiempo: O(n) Espacio: O(1)
*/
Clase Solución {
public int maxProduct(int[] nums) {
int maxSoFar = nums[0];
int currMax = nums[0];
int currMin = nums[0];

para (int i = 1; i)
int n = nums[i];
// si N es negativo, currMax y currMin cambiarán roles
Intento Max = currMax;
currMax = Math.max(n, Math.max(tempMax * n, currMin * n));
currMin = Math.min(n, Math.min(tempMax * n, currMin * n));
MaxSoFar = Math.max(maxSoFar, currMax);
}
retorno máx SoFar;
}
}
`` `

#### 2down⃣ Python

``python
# LeetCode 152 – Maximum Product Subarray
# Tiempo: O(n) Espacio: O(1)

Solución de clase:
def maxProduct(self, nums: list[int]) - Conf int:
max_so_far = curr_max = curr_min = nums[0]
para n en nums[1:]:
temp_max = curr_max
curr_max = max(n, temp_max * n, curr_min * n)
curr_min = min(n, temp_max * n, curr_min * n)
max_so_far = max(max_so_far, curr_max)
volver max_so_far
`` `

#### 3down⃣ C++

``cpp
// LeetCode 152 – Maximum Product Subarray
// Hora: O(n) Espacio: O(1)

Clase Solución {
public:
int maxProduct(vector identificadoint ánimos) {
int max_so_far = nums[0];
int curr_max = nums[0];
int curr_min = nums[0];

para (int i = 1; i) ++i) {
int n = nums[i];
int temp_max = curr_max;
curr_max = max({n, temp_max * n, curr_min * n});
curr_min = min({n, temp_max * n, curr_min * n});
max_so_far = max(max_so_far, curr_max);
}
volver max_so_far;
}
};
`` `

-...

##  pilas de Edge Cases " Pitfalls

Silencio # Silencio Caso Edge Silencio Por qué importa Silencio Cómo lo maneja el algoritmo
Silencio.
Silencio 1 Silencio **Todos los números negativos** Silencio El producto máximo puede ser un solo negativo si hay un recuento extraño, o un positivo si incluso. Silencio `curr_max` comienza con el primer elemento; el bucle actualiza correctamente. Silencio
Silencio 2 Silencio **Zeros en la matriz** Silencio Zero rompe la cadena del producto; un nuevo sub-array debe comenzar después de él. Silencio `max(n, ...)` incluye `n` en sí mismo, que se convierte en 0, reasentando `curr_max` y `curr_min`. Silencio
Silencioso 3 Silencioso elemento array** Silencio debe devolver ese elemento. El bucle nunca corre; `max_so_far` es devuelto. Silencio
Silencio 4 Silencio **Large negative * negativo** Silencio Puede rebosar si usa enteros de 32 bits. ← Problema garantiza que el resultado se ajuste a un int firmado de 32 bits, por lo que `int` es seguro. Silencio

-...

El bueno, el malo, el feo

### The Good
- **O(n)** tiempo y **O(1)** espacio – perfecto para las limitaciones de entrevista.
- Maneja todos los casos (negativo, cero, positivo) en un solo paso.
- Muy legible una vez que entienda la idea *max/min pair*.

### El malo
- El código puede parecer un poco mágico para un lector de primera vez; el * intercambio de roles* para números negativos no es inmediatamente obvio.
- Requiere un uso cuidadoso de variables temporales para evitar accidentalmente sobrescribir `curr_max` antes de que `curr_min` sea actualizado.

### El Ugly
- Algunas soluciones ingenuas intentan pre-computar productos prefijos o utilizar arrays de programación dinámicos de tamaño `n`, lo que resulta en **O(n)** espacio y sobrecarga adicional.
- Un error común: olvidar restablecer el min/max después de encontrar un cero, lo que lleva a resultados incorrectos.

-...

## 🎯 Quick Checklist Before Your Interview

Expliquen por qué necesitamos a ambos. Min.
- [ ] Mostrar cómo un número negativo *swaps* ellos.
- [ ] Camine a través de un ejemplo de señal mixta en la pizarra.
Mencione la actualización de "max_so_far".
- [ ] Discuta la complejidad del tiempo/espacio y por qué es óptima.

-...

## 🚀 Bonus – Solución alternativa O(n) (Prefix + Postfix)

Algunos entrevistadores podrían pedir un enfoque *two-pass*:

1. Pase adelante: computar el producto máximo finalizando en cada índice.
2. Paso posterior: calcular el producto máximo comenzando en cada índice.
3. Tome el máximo del producto de los dos pases en cada índice.

Esto también utiliza el espacio `O(n)`, pero puede ser conceptualmente más fácil de explicar.

-...

Pensamientos finales

El problema Maximum Product Subarray es un ejemplo clásico de cómo una simple declaración de problemas puede ocultar un giro sutil. Al realizar un seguimiento de los productos **maximum** y **minimum** en cada paso, manejamos elegantemente números negativos y ceros en un solo paso. Domine este patrón, y se sentirá seguro de abordar no sólo LeetCode 152 sino un conjunto de problemas de entrevista que implican *prefijos productos* o *escaneos parciales*.

-...

## Tomen acción

- **Implement** los fragmentos en tu idioma preferido y prueba en LeetCode.
- **Explicar** el algoritmo a un amigo o grabar un video corto; la enseñanza solidifica el aprendizaje.
- **Añadir** esta solución a su cartera o GitHub repo; a los reclutadores les encanta ver código limpio, multi-idioma.

¡Feliz codificación, y buena suerte aterrizando ese trabajo de sueño! 🚀

-...

### SEO Palabras clave (para el artículo):
- Subarray de producto máximo
- Solución LeetCode 152
- algoritmo de Kadane para el producto
- Problemas de entrevista de programación dinámica
- Java Python C++ entrevista codificación
- Preparación de entrevistas de trabajo
- Manejar números negativos en arrays
- O(n) time O(1) space array problems

-..