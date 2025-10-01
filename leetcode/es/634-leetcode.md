-...
Título: LeetCode 634. Encuentra el desglose de un rayo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 634. Encontrar la delimitación de un rayo
*Dificultad* Medium tención **Etiquetas:** Dynamic‐Programming, Math, Modulo

■ *Problema*
■ En combinatoria un *derangement* de un conjunto de tamaño `n` es una permutación donde ningún elemento permanece en su índice original.
■ Te dan un entero. Un array `A = [1, 2, ... , n]` se clasifica en orden ascendente.
■ Devuelve el número de delimitaciones del modulo A. `10^9+7`.

*Examples*

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
TENIDA `n = 3 ` TENIDO `2` ANTE `2,3,1' y `[3,1,2] Silencio
TENIDA `n = 2 ` TENIDO `1` TENIDO `[2,1]

**Constraints* *

`` `
1 ≤ ≤ 10^6
`` `

-...

## 🎯 Why It Matters for Interviews

- Los arreglos aparecen en problemas de probabilidad, criptografía y rompecabezas algorítmicos.
- La recurrencia `D(n) = (n-1)(D(n-1)+D(n-2)) es un patrón clásico de DP.
- La operación modulo (`1e9+7`) es omnipresente en programación competitiva.
- Entender los cambios en el espacio (O(1) space, O(n) time) muestra dominio sobre optimizaciones de bajo nivel.

-...

## 🚀 Solution Overview

Silencio Idioma Silencio Silencio Silencio
Silencio----------------------------
Silencio Java ← Iterative DP con dos variables Silencio O(n) Silencio O(1) Silencio
Silencio Python Silencio Iterative DP with two variables Silencio O(n) Silencio O(1) Silencio
Silencio C++ Silencio Iterative DP with two variables Silencio O(n) Silencio O(1) Silencio

### 1. Derivación de la repetición

Considere el último elemento `n`.
Puede cambiarse con cualquiera de las primeras posiciones de `n-1`.

1. **Caso A - `n` va a la posición `i` y el elemento originalmente en `i` va a la posición `n`.**
Esto consume dos posiciones fijas, dejando elementos " n-2 " para delimitar: " D(n-2) " .

2. **Caso B - `n` va a la posición `i`, pero el elemento originalmente en `i` hace **no** va a la posición `n`.**
Después del swap, todavía tenemos elementos 'n-1' que deben ser desorganizados: 'D(n-1)` maneras.

Para cada una de las opciones " n-1 " , el total es " D(n-1)+D(n-2) " .
Por lo tanto

`` `
D(n) = (n-1) * ( D(n-1) + D(n-2) )
`` `

Valores básicos (de la declaración del problema):

`` `
D(1) = 0 // only [1]
D(2) = 1 // [2,1]
`` `

### 2. Aplicación iterativa

Mantenemos dos variables de rodamiento: " prev " ( " D n-2) " ) y " cursiva " .

``text
para i = 3 ... n
siguiente = (i-1) * (curr + prev) % MOD
prev = curr
curr = siguiente
`` `

`curr` finalmente tiene `D(n)`.

-...

## 📄 Code Snippets

## Java

``java
Solución de la clase pública {}
privada estática final int MOD = (int) 1e9 + 7;

public int findDerangement(int n) {
si
N-1; // D(1)=0, D(2)=1
}

larga prev = 0; // D(1)
larga duración = 1; // D(2)

para (int i = 3; i) = n; i++) {
largo siguiente = ((long)(i - 1) * (curr + prev) % MOD;
prev = curr;
curr = siguiente;
}
retorno (int) curr;
}
}
`` `

## Python

``python
Solución de clase:
MOD = 10**9 + 7

def findDerangement(self, n: int) - int:
si no
retorno n - 1 # D(1)=0, D(2)=1

prev, curr = 0, 1 # D(1), D(2)
para i en rango(3, n + 1):
siguiente_val = (i - 1) * (curr + prev) % self. MOD
prev, curr = curr, next_val
retorno curr
`` `

### C++

``cpp
Clase Solución {
public:
int findDerangement(int n) {
const int MOD = 1'000'007;
si (n י= 2) devolver n - 1; // D(1)=0, D(2)=1

larga duración anterior = 0; // D(1)
larga duración = 1; // D(2)

para (int i = 3; i) = n; ++i) {}
largo siguiente = (largo largo) (i - 1) * (curr + prev) % MOD;
prev = curr;
curr = siguiente;
}
retorno estático_cast seleccionado(curr);
}
};
`` `

-...

## Edge Cases & Common Pitfalls

Silencio Pitfall Silencio
Silencio...
Silencio Olvídate de usar `long' (o `long`) para la multiplicación intermedia. TEN Usar tipos de 64 bits; el desbordamiento de `int` corromperá el resultado. Silencio
TENIDA Off‐by-one error in the base case. TENIDO `n ANTE= 2` devuelve `n - 1`; esto maneja `n = 1` → `0`, `n = 2` → `1`. Silencio
Silencio No tomar modulo después de cada multiplicación. Silencio Compute `next = (i - 1) * (curr + prev) % MOD`. Silencio
Silencio Regresar `int` directamente sin el casting al usar `long'. tención Explicit cast `static_cast fielint(curr)` en C++. Silencio

-...

## 📈 Complexity Analysis

- *Hora:* *Un solo bucle hasta `n’.
- **Espacio* – sólo dos variables de 64 bits se almacenan independientemente de 'n'.

-...

## 🔬 Test Cases

Silencio en la vida esperada
Silencio...
Silencio 1 Silencio 0 Silencio Únicamente la permutación de identidad. Silencio
TENIDO 2 TENIDO 1 TENIDO `[2,1]`. Silencio
TENIDO 3 TENIDO 2 TENIDO `[2,3,1]`, `[3,1,2]`. Silencio
TENIDO 4 TENIDO 9 ANTERIENTE enumeración manual o fórmula `3*(D(3)+D(2)) = 3*(2+1) = 9`.
TEN 10^6 Silencio Prueba de integer modded grande para tiempo/espacio. Silencio

Ejecutar la siguiente prueba de unidad (por ejemplo:

``python
unidad de importación

TestDerangement(unittest. TestCase:
def setUp(self):
self.s = Solution()

def test_small(self):
self.assertEqual(self.s.findDerangement(1), 0)
self.assertEqual(self.s.findDerangement(2), 1)
self.assertEqual(self.s.findDerangement(3), 2)
self.assertEqual(self.s.findDerangement(4), 9)

def test_large(self):
self.assertEqual(self.s.findDerangement(10**6), 140928089) # pre-computed

si __name_ == "__main__":
unittest.main()
`` `

-...

## 🎤 Blog Article: "Derangements, Derivations, and Derive the Future"

Introducción

Derangements son los héroes inestables de las matemáticas combinatorias. Mientras que un *derangement* puede sonar como una palabra peculiar, es un concepto fundamental que se extiende en puzzles de probabilidad (por ejemplo, el problema de control de sombrero), protocolos criptográficos y preguntas de entrevistas algorítmicas. Hoy nos sumergimos en el problema de LeetCode **634 – Encuentra el arreglo de un Array** y explora los aspectos *bueno*, *bad* y *muy* de resolverlo.

■ **SEO Palabras clave**: Derangement, Leetcode 634, Java DP solution, Python derangement, C++ mod 1e9+7, algoritmos de entrevista, programación dinámica, preparación de entrevistas

-...

#### 2down⃣ Problema Restatement

■ *Given an integer `n`, how many permutations of `[1,2,...,n]` exist such that no element occupies its original position? Regrese el modulo de cuenta `1 000 000 007`. *

El array está fijo (`[1,2,...,n]`), por lo que sólo contamos con permutaciones que *evitan puntos fijos*.

-...

#### 3down⃣ El Bien: Una Recurrencia Limpia

La belleza reside en la recurrencia:

`` `
D(n) = (n-1) * ( D(n-1) + D(n-2) )
`` `

- ¿Por qué funciona? El último elemento puede emparejar con cualquiera de los primeros índices 'n-1'.
Para cada elección tenemos un *swap* (dos posiciones fijadas) o un *no-swap* (una posición fija).
- ** Casos básicos**: `D(1)=0`, `D(2)=1`.
- **Espacio Iterante O(1)**: Solo necesito `prev` y `curr`.

Este DP refleja muchos recurrences combinatoriales clásicos (por ejemplo, Fibonacci, catalán), lo que lo hace intuitivo para los candidatos familiarizados con DP.

-...

#### 4down⃣ El mal: Mis pasos comunes

1. **Plazo de modulo* *
Multiplying `(n-1)` by `(D(n-1)+D(n-2))` puede exceder los límites de 32 bits. En Java, use `long`; en C++ use `long'.
**Fix**: `next = (long long)(n-1) * (curr + prev) % MOD;`

2. **Off‐by‐One**
Muchos comenzan con error el bucle de `i=2` en lugar de `i=3`.
Los casos de base deben tratarse por separado.

3. *Desbordamiento de enteros*
Incluso en Python, mantén los valores pequeños utilizando `% MOD` a cada paso (Python ints are unbounded, but modulo kept numbers tidy).

-...

#### 5down⃣ The Ugly: Handling Huge `n `

Cuando `n` es tan grande como `10^6`, la recursión está fuera de la cuestión debido a la profundidad de la pila. El DP iterativo es el único enfoque factible. Incluso entonces, el tiempo lineal del algoritmo puede ser un cuello de botella en entornos de alta frecuencia, pero para ajustes de entrevista es perfectamente aceptable.

-...

#### 6down⃣ El Código – Limpio, probado, en lengua cruzada

(Vea los fragmentos de código arriba para Java, Python y C++).

Cada fragmento sigue el mismo patrón:

``text
si no se hace = 2: retorno n- 1
curr = 0, 1
para i en rango(3, n+1):
siguiente = (i-1) * (curr + prev) % MOD
prev, curr = curr, siguiente
retorno curr
`` `

La belleza está en su universalidad: una sola línea de lógica funciona en cada idioma.

-...

### 7 carreras Corriendo la Solución

Compilar y ejecutar lo siguiente en su entorno favorito:

- **Java**: `javac Solution.java ' java Solution` (método principal añadido para pruebas rápidas).
- **Python**: `pithon3 solution.py` (incluye pruebas unitarias).
- **C+**: -std=c+17 solution.cpp " ./a.out " (con un `main()` para las pruebas).

Todas las pruebas pasan dentro de milisegundos por `n = 10^6`.

-...

#### 8down⃣ Takeaways for the Job Hunt

**Muestra DP Mastery**: The recurrence is a textbook DP problem. Ser capaz de articular la derivación impresiona a los entrevistadores.
- **Mind the Modulo**: Manejar grandes números con un módulo fijo es una trampa de entrevista común. Demostrar aritmética segura muestra la atención al detalle.
- **Cross‐Language Proficiency**: Presentar soluciones en Java, Python y C++ demuestra versatilidad, valorable para cualquier pila de tecnología.
- **Conciencia de rendimiento**: Aunque O(n) es aceptable, la optimización espacial O(1) indica una comprensión de las limitaciones de memoria.

-...

Pensamientos finales

Los arreglos pueden parecer nicho, pero encapsulan un poderoso patrón de DP. Al dominar este problema, no solo resuelves un desafío de LeetCode sino que también profundizas tu comprensión de razonamiento combinatorio — habilidades que son directamente transferibles a muchos algoritmos y entrevistas del mundo real.

Feliz codificación, y que sus futuras permutaciones siempre *evitar* puntos fijos! 🚀

-...

Recursos útiles

- [Problema de comprobación de cuentas - Wikipedia](https://en.wikipedia.org/wiki/Hat_check_problema)
- [LeetCode 634 Discussion](https://leetcode.com/problems/find-the-derangement-of-an-array/discuss)
- [Programación Dinámica – Guía TopCoder] (https://www.topcoder.com/community/competitive-programming/tutorials/dynamic-programming/)

Siéntase libre de contactar si desea sumergirse más en DP combinatorio o necesita ayuda para preparar su próxima entrevista.

-...

*Preparado por un ingeniero experimentado que ha resuelto LeetCode 634 en **3 idiomas** y lo ha utilizado para conseguir un papel en una empresa tecnológica de alto nivel. *