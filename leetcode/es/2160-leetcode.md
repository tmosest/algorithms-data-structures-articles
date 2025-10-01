-...
Título: LeetCode 2160. Suma mínima de cuatro dígitos después de dividir dígitos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 2160 – Suma mínima de cuatro dígitos después de dividir dígitos
### Java Silencio Python Silencio C++ Silencio Algorithm tención

-...

Declaración de problemas

Se le da un entero **positivo** `num' compuesto de **exactamente cuatro dígitos** (`1000 ≤ num ≤ 9999`).
Usted debe dividir los dígitos de `num` en dos nuevos enteros `nuevo1` y `nuevo2` utilizando **todo** cuatro dígitos.
Se permiten ceros líderes.

■ * Objetivo*
■ Devuelve el valor **minimum posible** de `nuevo1 + nuevo2`.

*Ejemplo*
`num = 2932` → digitos `[2, 9, 3, 2]`
Posibles pares: `[29, 23]`, `[223, 9]`, `[2, 329]`, ...
Suma mínima = `29 + 23 = 52`.

-...

Intuición

Para mantener la suma pequeña, queremos que cada número sea lo más breve posible y utilice los dígitos más reducidos** en las posiciones de orden superior**.

Si clasificamos los dígitos en orden ascendente:

`` `
ordenados = [d0, d1, d2, d3] // d0
`` `

La suma mínima se logra por:

`` `
nuevo1 = d0 * 10 + d2 // primero y tercero más pequeño
nuevo2 = d1 * 10 + d3 // segundo y mayor
`` `

¿Por qué?
- Cada número recibe un dígito en el lugar de las decenas (el más pequeño mejor).
- El dígito restante va al lugar de las unidades.
- Este emparejamiento produce los números de dos dígitos más pequeños posibles, por lo tanto la suma más pequeña.

-...

#### 🏎{ >} Análisis de la Complejidad

TEN TERMIN TEN ANTE Complejidad
Silencio...
Silencio **Tiempo** Silencioso `O(1)` – sólo clasificamos cuatro elementos (`O(4 log 4)` ♥ constante). Silencio
Silencio** – memoria adicional constante. Silencio

-...

## 📦 Code Implementations

## Java

``java
importa java.util. Arrays;

Clase Solución {
mínimo público Sum(int num) {}
int[] dígitos = nuevo int[4];
para (int i = 0; i)
dígitos[i] = num % 10;
num /= 10;
}
Arrays.sort(digits); // ascending
int num1 = dígitos[0] * 10 + dígitos[2]; // tens + unidades
int num2 = dígitos[1] * 10 + dígitos[3];
volver num1 + num2;
}
}
`` `

## Python

``python
Solución de clase:
mínimo Sum(self, num: int) - título int:
dígitos = ordenados([int(d) para d en str(num)]) # List of four ints
num1 = dígitos[0] * 10 + dígitos[2]
num2 = dígitos[1] * 10 + dígitos[3]
volver num1 + num2
`` `

### C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minimumSum(int num) {}
dígitos vectoriales:
para (int i = 0; i) {}
dígitos. push_back (num % 10);
num /= 10;
}
(digits.begin(), digits.end()); // ascending
int num1 = digitos[0] * 10 + dígitos[2];
int num2 = dígitos[1] * 10 + dígitos[3];
volver num1 + num2;
}
};
`` `

-...

## 📚 Blog Artículo: “El Bien, el Mal, y el Ugly of Solving LeetCode 2160”

#### Introduction

Si se está preparando para entrevistas de codificación, el problema LeetCode “Minimum Sum of Four‐Digit Number After Splitting Digits” es un ejemplo perfecto de un reto **conciso, pero sutil**. Te obliga a pensar en la manipulación de dígitos, la optimización y los obstáculos de las soluciones de fuerza bruta. En este artículo, diseccionaremos el problema, caminaremos a través de la solución óptima, resaltaremos errores comunes (el “malo”) y discutiremos cómo manejar casos de borde (el “muy”).

### Por qué este problema importa

** Pensamiento Algorítmico**: Demuestra cómo se puede usar la clasificación para minimizar las sumas.
- **Constraints de tiempo y espacio**: Muestra que las soluciones de tiempo constante son alcanzables.
- **Interview Relevance**: Muchos entrevistadores preguntan variaciones de los problemas de los dígitos multiplicados.

## Problema Recap (Quick)

Se le da un entero de 4 dígitos 'num'. Dividir sus dígitos en dos nuevos números usando **all** dígitos, permitiendo ceros líderes, y devolver la suma **minimo** posible.

### The “Good” – Elegante y Optimal

##### 1. Ordenar los dígitos

Al ordenar, inmediatamente sabemos qué dígitos son más pequeños y más grandes.
Ordenar cuatro números es trivial (`O(1)` tiempo).

##### 2. Pare el más pequeño con el siguiente más pequeño

Forma `nueva1' utilizando los dígitos más pequeños (`d0`) y tercero más pequeños (`d2`),
y `nueva2` utilizando el segundo más pequeño (`d1`) y el más grande (`d3`).

¿Por qué esta pareja?
- Garantiza que cada nuevo número es **dos dígitos** largos (excepto cuando aparecen ceros).
- Coloca los dígitos más pequeños en el lugar **tens**, que tiene el peso más alto.

##### 3. Regrese el Suma

Agregue los dos números; esa es la respuesta.

Esta solución es **extremada**, ** legible**, y ** optimista**.

### El “Bad” – Pitfalls comunes

Por qué es malo arreglar la vida
Silencio--------------------------
Silencio **Brute‐force all permutations** Hay 4! = 24 maneras, pero todavía aceptable. Sin embargo, la generación de todas las particiones 2^4 es exagerada y aumenta el tiempo. Usar la clasificación + pares codiciosos. Silencio
Silencio ** Orden de extracción de dígitos incorrectos** Silencio Tomar dígitos de izquierda a derecha vs derecha a izquierda puede llevar a índices incorrectos. Silencio Consistentemente pop desde el final o convertir a cadena. Silencio
Silencio **Ignorando los ceros principales** Silencio Algunas personas piensan que deben evitar ceros; pero el problema explícitamente les permite. Tener ceros como cualquier otro dígito. Silencio
Silencio **Asumiendo que cada número debe ser de 2 dígitos** Silencio Caso Edge `num=4009` → división óptima es `[4,9]` (números de dígitos). Silencio El algoritmo naturalmente maneja esto, ya que los ceros no contribuyen nada. Silencio

### El “Ugly” – Edge Cases & Tricky Inputs

← Input Silencio esperada salida ¿Por qué puede viajar hasta arriba
Silencio......
TENIDO `num = 1000` TENIDO `1` (split `[1, 0]` y `[0, 0]`) TENIDO Dos ceros en un número, pero el algoritmo todavía funciona. Silencio
Silencio `num = 9999` Silencio `99 + 99 = 198` Silencio Todos los dígitos son iguales – la suma es sólo dos veces el número de dos dígitos. Silencio
TENIDO `num = 4009` TENIDO `13` TENIDO Los ceros principales aparecen cuando se forman `[4, 9]`. Asegúrese de que su código no deja accidentalmente ceros del frente. Silencio

## Código Snippets (Todos los idiomas)

-Java** – ver arriba.
- **Python** – ver arriba.
- **C+** - ver arriba.

### Qué proyector busca

Una explicación concisa del algoritmo.
- **Eficiencia**: Saber que existen soluciones de tiempo constante.
- **Edge‐Case Awareness**: Manejo de entradas con ceros o dígitos repetidos.

## Final Takeaway

LeetCode 2160 es engañosamente simple pero revela una estrategia clásica avaricia: * surtido, luego par más pequeño con el tercero más pequeño, más grande con el segundo más pequeño.* Dominar este problema demuestra su capacidad de pensar algorítmicamente, escribir código limpio, y anticipar casos de borde, todas las habilidades clave para una entrevista de ingeniería de software.

### ¿Quieres más?

- Explore otros problemas de “manipulación de dígitos” en LeetCode (por ejemplo, **2164. Cuenta el número de subsecuencias palindromicas**).
- Practicar algoritmos codiciosos en entrevistas (por ejemplo, **Greedy Gift Givers**, **Maximum Subarray**).
- Construir una cartera personal de soluciones en GitHub; los reclutadores aman código limpio y bien documentado.

Codificación feliz, y que sus puntuaciones de entrevista reflejen esta solución elegante! 🚀

-...

**SEO Tags**: LeetCode 2160, Suma mínima de cuatro dígitos, Algorithm Interview Question, Java Solution, Python Solution, C++ Solution, Greedy Algorithm, Interview Preparation, Coding Interview, Software Engineer Interview, Job Interview Tips.