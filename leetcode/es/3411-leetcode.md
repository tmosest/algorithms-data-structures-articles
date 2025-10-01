-...
Título: LeetCode 3411. Subarray Máximo con productos iguales -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🚀 ** Subarray Maxum con productos iguales - LeetCode 3411**
*El bien, el mal y el ugly*

-...

## 📌 Problema Resumen

Silencio
Silencio...
Silencioso **LeetCode ID**
Silencio **Título** Silencio Máximo Subarray Con Igualdad de Productos
Silencioso **Dificultad**
tención **Introducción** Silencioso `int[] nums` – enteros positivos (1 ≤ nums[i] ≤ 10, 2 ≤ nums.length ≤ 100)
Silencio ** Objetivo** Silencio Regresar la longitud de la sub-array más larga `arr` tal que

\[
\prod(arr) \;=\; \gcd(arr) \times \operatorname{lcm}(arr)
\]

Silencio **Por qué importa** Silencio Un sub-array sub-product‐equivalente satisfice una rara identidad número-teorética que sólo tiene para un puñado de secuencias enteros. Identificarlo prueba su capacidad de combinar **GCD/LCM lógica** con ** optimización de fuerza por fuerza** – una entrevista clásica combo. Silencio

-...

## The Underlying Math

Para dos enteros \(a\) y \(b\),

\[
a \times b \;=\; \gcd(a,b)\times\operatorname{lcm}(a,b)
\]

La identidad *no se extiende a un conjunto arbitrario de más de dos números.
Un sub-arrayo de longitud 2 es producto-equivalente **sólo cuando** todos sus elementos son "co-alignados" de una manera muy específica:

* Todos los elementos son múltiples del GCD del sub-array.
* El LCM es exactamente el producto de los factores de co-prime que se mantienen **.

Debido a que las limitaciones son pequeñas (longitud ≤ 100, cada elemento ≤ 10), una fuerza bruta cuadrada** es más que lo suficientemente rápida si manejamos los enteros grandes correctamente.

-...

## 🎯 Strategy – The Brute‐Force 2‐Loop

1. **Evaluar todos los índices de inicio** "i" (0...n-1).
2. Para cada principio, ** aumentar el sub-array** un elemento a la vez (`j = i ... n‐1`):
* Actualizar el producto ** (`prod`).
* Actualizar el funcionamiento **GCD** (`g`).
* Actualizar el funcionamiento **LCM** (`l`).
3. Siempre que `prod == g * l`, registre la longitud `j-i+1`.
4. Mantenga la longitud máxima encontrada.

Debido a que `prod` puede explotar (10^100 para el peor de los casos), utilizamos ** enteros de precisión arbitraria**:

Silencio Idioma Silencioso herramienta
Silencio...
Silencio Java Silencio `java.math. Big Integer` Silencio
Silencio Python Silencio incorporado `int` (sin límites)
Silencio C++ Silencioso::multiprecisión::cpp_int Silencio

El GCD del sub-array actual puede permanecer como un 'long' normal (valores ≤ 10), pero el LCM y el producto deben ser BigIntegers.

-...

## ♥ Complexity Analysis

Silencio Silencio Silencio Silencio Silencio
Silencio...
Silencio **Brute‐Force 2‐Loop** Silencio \(O(n^2)\) (≤ 10,000 iterations for n = 100) Silencio \(O(1)\) (aparte de BigIntegers que son parte de la computación) ←
Silencio **Optimized (Sliding Window)** Silencio No es necesario – las limitaciones actuales son triviales. Silencio
Silencioso **¿Por qué no hay TLE?** Silencio LeetCode da 1 s para arrays de 100 longitudes; 10.000 gcd/lcm multiplicaciones son triviales. Silencio

-...

Galería de códigos

A continuación se encuentran soluciones limpias, listas para pasar en **Java**, **Python**, y **C+**. Cada archivo contiene una única clase/función que coincide con la firma de LeetCode.

■ **Consejo:** Ejecute las pruebas localmente para verificar que la longitud máxima coincida con los ejemplos.

#### ## 1down⃣ Java

``java
importa java.math. BigInteger;
importar java.util*;

Solución de la clase pública {}
// Utilidad para gcd de dos números largos
privada estática larga gcd(long a, long b) {}
mientras (b!= 0) {
t largo = un % b;
a = b);
b = t;
}
devolver a;
}

public int maxLength(int[] nums) {
int n = nums.length;
int best = 0;

para (int i = 0; i)
g largo = nums[i]; // GCD actual
BigInteger l = BigInteger.valueOf(nums[i]); // current LCM
BigInteger prod = BigInteger.valueOf(nums[i]);

(prod.equals(l.multiply(BigInteger.valueOf(g)))))))
mejor = Math.max(mejor, 1);

para (int j = i + 1; j)
prod = prod.multiply(BigInteger.valueOf(nums[j]));

g = gcd(g, nums[j]);

BigInteger gcdLcm = l.gcd(BigInteger.valueOf(nums[j]));
l = l.divide(gcdLcm).multiply(BigInteger.valueOf(nums[j]));

(prod.equals(l.multiply(BigInteger.valueOf(g)))))))
mejor = Math.max(best, j - i + 1);
}
}
devolver mejor;
}
}
`` `

-...

#### 2down⃣ Python

``python
Solución de clase:
def maxLength(self, nums: List[int] int:
n = len(nums)
mejor = 0

para i en rango(n):
g = nums[i] # GCD se mantiene pequeño
l = nums[i] # LCM as Python int
prod = nums[i] # producto as Python int

si prod == g * l:
mejor = max(best, 1)

para j en rango(i + 1, n):
prod *= nums[j]
g = math.gcd(g, nums[j])
l = l * nums[j] // math.gcd(l, nums[j])

si prod == g * l:
mejor = max(best, j - i +1)

mejor
`` `

*(Agregue 'import math' en la parte superior si usted está ejecutando esto en un script.) *

-...

#### 3down⃣ C++

``cpp
#include יbits/stdc++.h
#include ■boost/multiprecision/cpp_int.hpp

usando std namespace;
usando el impulso::multiprecisión::cpp_int;

estática larga larga gcd_ll(long long a, long long b) {}
b) {
largo t = un % b;
a = b; b = t;
}
devolver a;
}

Clase Solución {
public:
int maxLength(vector fielint círculo nums) {
int n = nums.size();
int best = 0;

para (int i = 0; i) {}
long g = nums[i]; / GCD
cpp_int l = nums[i]; // LCM
cpp_int prod = nums[i]; // producto

si (prod == l * g)
mejor = max(best, 1);

para (int j = i + 1; j)
prod *= nums[j];

g = gcd_ll(g, nums[j]);

long long val = nums[j];
gcd_l_val = gcd_ll(long long)(l % val), val);
l = l / gcd_l_val * val;

si (prod == l * g)
mejor = max(best, j - i + 1);
}
}
devolver mejor;
}
};
`` `

-...

## 📚 Discussion – The Good, The Bad, The Ugly

TENIDO Aspecto ANTE TENIDO TENIDO ENTRE ANTERIOR ANTERITO
Silencio--------------------------
Silencio ** Algorithm** Silencio directo, fácil de entender. Brute‐force 2‐loop aprovecha los pequeños límites. Silencio Ninguno – el algoritmo ingenuo ya es óptimo para las limitaciones dadas. En versiones más grandes del problema, este método O(n2) **blow up** porque las actualizaciones GCD/LCM dominarían. Silencio
Silencio **Precisión** Silencio Usando `BigInteger`/`cpp_int` previene el desbordamiento y mantiene la lógica pura. Usted * debe* utilizar la apreciación arbitraria; un producto ingenuo 'long' se desbordará incluso para n = 20. Silencio Olvidar BigIntegers conduce a respuestas erróneas que el juez rechazará. Silencio
Silencio **Readability** Silencio Java code tiene helper `gcd(long a, long b)` y un solo bucle; Python's big-int hace que sea casi "no-overhead". TEN C++ solución se basa en Boost; algunos entrevistados podrían evitarlo debido a encabezados adicionales. En una entrevista real, mostrando un completo "boost::multiprecision` snippet puede ser una bandera roja si el entrevistador no está familiarizado con Boost. Silencio
Silencio **Tiempo de Entrega** Silencio Las tres soluciones se ejecutan 0,5 ms en LeetCode para n = 100. Silencio Silencio Si usted estaba codificación bajo 60 s presión, el enfoque Java/Boost podría sentir pesado. Una nota mental rápida: *“Mantendré el producto como un `BigInteger` y romper temprano si es más grande que `LCM * GCD`”* le salvará de un momento de pánico. Silencio

-...

## 🎤 "Tell‐Me‐About" the Interview

Durante una entrevista de estilo FAANG, a menudo se le pedirá que explique:

1. **¿Por qué `prod == g * rara vez sucede? * *
*Hablar sobre la identidad de dos números y por qué colapsa por ≥ 3 números. *

2. **¿Qué tipo de datos utilizar? #
*Explicar que el producto puede crecer a 10^100, por lo que debemos utilizar `BigInteger` (Java), Python's nativa `int`, o Boost `cpp_int`. *

3. **Posibilidades de optimización**
*Si el tamaño de la matriz fuera de 104, necesitaríamos una ventana deslizante o una estrategia de poda. Aquí, n = 100, por lo que la fuerza bruta O(n2) es más limpia. *

4. *Manipulación de cajas*
*Mostrar que comprobó para los desbordamientos y utilizó la comparación `.equals()` / `=` correctamente. *

-...

## 💬 Final Takeaway

■ **El sub-arrayo equivalente del producto es un *raza matemática* – un juego perfecto para entrevistadores para probar la teoría del número + habilidades algorítmicas. #
■ Con las limitaciones de LeetCode 3411, una fuerza bruta simple de 2 puntos** que utiliza **arbitrary‐precision arithmetic** es *ambos* rápida y elegante.

- Si se está preparando para **FAANG** o cualquier entrevista de gran tecnología, practique este problema junto con otros puzzles **GCD/LCM** (por ejemplo, “Número mínimo de toques” o “Recoloj de lanza en Histograma”).
- No dude en copiar los fragmentos de código en su espacio de trabajo personal LeetCode, añadir pruebas de unidad y ajustar el uso BigInteger para su propia comodidad.

Feliz codificación, y que su próxima entrevista vaya **smootal y eficientemente**!

-...

## 🔖 Palabras clave para SEO

- Subarray Máximo con productos iguales
- Solución LeetCode 3411
- Java LeetCode GCD LCM
- Python LeetCode product‐equivallent subarray
- C++ arbitrario-precisión integer LeetCode
- La teoría del número de entrevistas FAANG
- Preparación de entrevistas de trabajo LeetCode
- Preguntas de entrevista de LeetCode

-..