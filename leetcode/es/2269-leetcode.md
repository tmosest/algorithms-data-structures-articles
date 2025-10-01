-...
Título: LeetCode 2269. Encontrar el K-Beauty de un número -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Soluciones de 3 idiomas para **LeetCode 2269 – Encontrar la K‐Beauty de un número**

Silencio Idioma Silencio Archivo Silencio Complejidad Silencio
Silencio----------------------------------...
Silencio Java ¦ `Solution.java` Silencioso **O(n · k)** tiempo, **O(1)** extra  Utiliza el `String.substring ` + `Integer.parse Int`. Funciona cómodamente porque `n ≤ 10`. Silencio
TENIDO Python TENIDO `solution.py` TENIDO **O(n · k)** tiempo, **O(1)** extra ANTE Utiliza el corte de cuerdas y la conversión de `int(). Silencio
TENIDO C++ TENIDO `solution.cpp` Silencio **O(n · k)** tiempo, **O(1)** extra TENIDO Utiliza `substr` y `stoi`. Silencio

■ **Continuación para entrevistas** – si el número fuera mucho mayor, querrías una actualización de enteros de ventana * deslizante* en lugar de pares repetidos.
■ Aquí mantenemos el código limpio porque las limitaciones son pequeñas.

-...

## Java

``java
2269. Encontrar la K-Beauty de un número
// Problema de LeetCode #2269
// Autor: ChatGPT (adaptado del editorial oficial)

Solución de la clase pública {}
public int divisor Subestrings(int num, int k) {
// Convertir el número en una cadena una vez
String s = Integer.toString(num);
int len = s.length();
int count = 0;

para (int i = 0; i <= len - k; i++) {
// Extracto subestring de longitud k
String sub = s.substring(i, i + k);
int val = Integer.parseInt(sub); // Los ceros principales están bien

// 0 nunca es un divisor
(val!= 0 " num % val == 0) {
contar++;
}
}
recuento de retorno;
}
}
`` `

-...

## Python

``python
# 2269. Encontrar la K-Beauty de un número
# LeetCode problem #2269
# Autor: ChatGPT (adaptado del editorial oficial)

Solución de clase:
def divisorSubstrings(self, num: int, k: int) - Propiedad int:
s = str(num)
n = len(s)
Conteo = 0

para i en rango(n - k +1):
sub = s[i:i + k]
val = int(sub) # Principales ceros permitidos
si vale!= 0 y num % val == 0:
Cuenta += 1
cuenta de retorno
`` `

-...

### C++

``cpp
2269. Encontrar la K-Beauty de un número
// Problema de LeetCode #2269
// Autor: ChatGPT (adaptado del editorial oficial)

#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int divisor Subestrings(int num, int k) {
cadena s = to_string(num);
int n = s.size(), cnt = 0;

para (int i = 0; i) = n - k; ++i) {}
cadena sub = s.substr(i, k);
int val = stoi(sub); // Financiamiento de ceros
(val!= 0 " num % val == 0)
++cnt;
}
cnt de retorno;
}
};
`` `

-...

## 2. SEO‐Optimized Blog Post

■ **Título**: *Cracking LeetCode 2269: “Find the K‐Beauty of a Number” – Java, Python y C++ Soluciones + consejos de entrevista*

■ **Meta Descripción**:
■ Aprende a resolver LeetCode #2269 en Java, Python y C++. Entender el algoritmo, la complejidad, los obstáculos y cómo llegar a la pregunta en una entrevista de codificación. ¡Pon tu puntuación de la entrevista de codificación hoy!

-...

#### Introduction

El problema ** "Encontrar la belleza de un número"** es un rompecabezas clásico de LeetCode "fácil" que prueba su manipulación de cuerdas, la lógica divisor y el manejo del borde.
En este artículo:

1. ** Explique el problema** en inglés claro.
2. Camina por el algoritmo **core** y proporciona soluciones en **Java, Python y C++**.
3. Discuta los aspectos **bueno, malo y feo** – de código limpio a posibles trampas.
4. Dar ** consejos de interés** y cómo presentar la solución a los gerentes de contratación.

¡Entramos!

-...

## Problema Recap

■ **Definition**: The *k-beauty* of an integer `num` is the number of substrings of `num` ( when read as a string) that satisfy:
■ 1. La duración es igual a " k " .
■ 2. El valor entero de la subestring divide `num` uniformemente.
■ 3. `0` es **nunca** un divisor (incluso si la subestring es “00”).

**Input**
- `num`: entero positivo (`1 ≤ num ≤ 10^9`).
- `k`: entero positivo (`1 ≤ k ≤ num.length`).

**La salida*
- Cuento entero de subestrings clasificatorios.

*Examples*

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
TENIDO `num = 240`, `k = 2` TENIDO `2` ANTE ' 24 ' y " 40 " son divisores. Silencio
TENIDO `num = 430043`, `k = 2` TENIDO `2` ANTE ' 43 ' se produce dos veces; " 30 " , "00 " , "04 " son inválidos. Silencio

-...

## Core Idea

1. **Stringify** el entero para que podamos tomar rebanadas contiguas.
2. **Slide** una ventana de tamaño `k` a través de la cuerda.
3. Convertir cada ventana en un entero (los ceros liberados no importan).
4. Compruebe dos condiciones: `val!= 0` y `num % val == 0`.
5. Incrementar el contador en consecuencia.

Debido a que la longitud máxima de `num` es 10, el algoritmo ingenuo `O(n · k)` es más que lo suficientemente rápido.

-...

#### Solution Details " Code "

A continuación se muestra la aplicación **canónica** que verá en el editor LeetCode para los tres idiomas.

##### Java

``java
Solución de la clase pública {}
public int divisor Subestrings(int num, int k) {
String s = Integer.toString(num);
int count = 0;
para (int i = 0; i) = s.length() - k; i++) {
int val = Integer.parseInt(s.substring(i, i + k));
(val!= 0 " num % val == 0) {
contar++;
}
}
recuento de retorno;
}
}
`` `

#### Python

``python
Solución de clase:
def divisorSubstrings(self, num: int, k: int) - Propiedad int:
s = str(num)
Conteo = 0
para i en rango(len(s) - k + 1):
val = int(s[i:i + k])
si vale!= 0 y num % val == 0:
Cuenta += 1
cuenta de retorno
`` `

###### C++

``cpp
Clase Solución {
public:
int divisor Subestrings(int num, int k) {
cadena s = to_string(num);
int count = 0;
para (int i = 0; i) = s.size() - k; ++i) {}
int val = stoi(s.substr(i, k));
(val!= 0 " num % val == 0)
++cuenta;
}
recuento de retorno;
}
};
`` `

**La complejidad* *

- *Hora*: `O(n · k)` (caso inferior ~ 100 operaciones, trivial para CPUs modernas).
*Pace*: `O(1)` (ignorando la cadena de entrada, que es parte del problema).

-...

## Good, Bad, and Ugly

Silencio Silencio
Silencio------------Prince------
Silencio **Readability** Silencio Nombres variables claros (`s`, `val`, `count`). Algunas personas pueden sobre-optimizarse con actualizaciones de entero manual. Silencio
Silencio ** Casos de Edge** Silencio Manijas que llevan ceros (`int("04")` → 4). Debe protegerse contra `val == Para evitar la división por cero. Olvidar el guardia hace que el código se estrelle o da respuestas incorrectas. Silencio
Silencio **Información** Silencio Con `n ≤ 10` la solución ingenua está bien. Silencio usando `Integer.parse Int` dentro de un bucle puede sentirse pesado pero es insignificante. Silencio Para entradas más grandes, usted querría una *rolling* actualización de enteros para evitar pares repetidos. Silencio
Silencio **Scalability** Silencio Obras para 32 bits ints. Silencio Para `num` ⇩ 2^31‐1 usted necesitará `long` o `BigInteger`. Silencio Usar `long` en Java y `long` en C++ es seguro para hasta 10^9. Silencio
Silencio **Idiomas de lengua** Silencio Java usa `substring`; Python slicing; C++ `substr`. Silencio Ninguno. ← Mixing 0-based and 1-based indices incorrectly leads to off-by-one errors. Silencio

-...

### Interview Tips

1. *Explicar las limitaciones*
- `num` ≤ 10^9 → en la mayoría de 10 dígitos.
- `k` ≤ número de dígitos → tamaño de la ventana nunca excede la longitud de la cadena.

2. **A través de casos de borde* *
- ceros líderes → `int("00") = 0`.
- Regla de divisor cero.
- Subestrings duplicados (por ejemplo, “43” aparece dos veces en `430043`).

3. **Mostrar un O(n · k) limpio Aplicación**
- Mención de que una actualización de entrada de ventana deslizante podría reducir los factores constantes pero es innecesaria aquí.

4. ** Análisis del espacio*
- O(n·k) time, O(1) space.
- Por qué satisface las limitaciones del problema.

5. **Si se solicita una versión más eficiente* *
- Mostrar el enfoque de la ventana de rodamiento:
`` `
val = val % pow10(k-1) * 10 + new_digit
`` `
pero explicar por qué es demasiado para este problema.

-...

### Closing Thoughts

El desafío “Encontrar la belleza de un número” es engañosamente simple, pero muestra la importancia de la manipulación de los bordes de cuidado** (cerrar ceros, división por cero) y ** estructura de código claro**. Resolviéndolo en Java, Python o C++ demuestra el pensamiento algorítmico lingüístico-agnóstico – una habilidad de entrevista clave.

Siéntete libre de copiar los fragmentos arriba en tu editor local de IDE o LeetCode. ¡Feliz codificación, y que este problema aumente la confianza de su entrevista! 🚀

-...

## Recursos > Lectura ulterior

- [Problema LeetCode 2269](https://leetcode.com/problems/find-the-k-beauty-of-a-number/)
- [Sliding Window Technique](https://leetcode.com/discuss/general-discussion/1172340/sliding-window-solution)
- [División de Facturación por Cero](https://stackoverflow.com/q/1157228/)

-...

SEO Palabras clave:**
LeetCode 2269, Encuentra la K‐Beauty de un número, solución Java, solución Python, solución C++, entrevista de codificación, algoritmo, manipulación de cadenas, divisor, consejos de entrevista, preparación de entrevistas.