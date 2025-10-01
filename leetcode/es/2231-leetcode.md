-...
Título: LeetCode 2231. Número más grande después de las gotas de dígito por la Paridad -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 2231. Número más grande después de las gotas de dígito por la Paridad – Código + Entrevista Listo Blog

**LeetCode ID:** 2231
*Dificultad* Fácil
**Tags:** Array, Greedy, Sorting, Priority Queue, String, Interview Question, Java, Python, C++

-...

## 📌 Problema Resumen

Se le da un entero positivo 'num'.
Puedes cambiar los dos dígitos que tengan la * misma paridad* (ambos o ambos impares).
Después de cualquier número de swaps, devuelve el ** más grande posible entero** que puedes formar.

■ *Ejemplo*
> `num = 1234 → 3412`
" año = 65875 → 87655 "

■ **Constraints**
" 1 " = num " = 10^9 "

-...

## 🧠 Key Insight

El orden relativo de los dígitos *odd* y los *even* dígitos nunca cambian – sólo puede reordenar dígitos **en cada clase de paridad**.
Así que la estrategia óptima es:

1. **Extraer** los dígitos extraños e incluso por separado.
2. **Sorta** cada lista en orden **descendiente** (así que los dígitos más grandes son los primeros).
3. **Recompilado** el número reemplazando cada dígito original por el siguiente dígito más grande de la misma paridad.

El resultado está garantizado para ser el máximo entero posible.

-...

Complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
TENIDO EXtract + sort TENIDO `O(d log d)` (d = #digits, ≤ 10) TENIDO `O(d)` Silencio
Silencio Silencio

Con 'd ≤ 10' la solución es trivial en el tiempo y la memoria.

-...

## 🎯 Code Implementations

A continuación se encuentran soluciones limpias y de producción en **Java**, **Python**, y **C+**.

■ **Tip** – Las tres soluciones convierten el número a una cadena para trabajar con dígitos, que mantiene el código legible y evita los bucles manual modulo/division.

-...

### 1Ω⃣ Java (Java 17)

``java
importar java.util*;

Clase Solución {
más grande Integer(int num) {
// Convertir en char array para facilitar el intercambio
char[] digits = String.valueOf(num).toCharArray();

// Greedy: para cada posición encontrar el mayor dígito de la misma paridad a la derecha
para (int i = 0; i) i++) {
para (int j = i + 1; j) j++) {
si (digits[j] "
(digits[j] - digitos[i]) % 2 == 0) {
// swap
char tmp = digits[i];
dígitos[i] = dígitos[j];
dígitos [j] = tmp;
}
}
}
integer.parseInt(new String(digits));
}
}
`` `

■ *Por qué funciona esto*
■ El doble bucle garantiza que cada vez que miramos hacia la derecha colocamos el mayor dígito posible de la misma paridad en la posición actual. Esto es efectivamente lo mismo que clasificar cada grupo de paridad en orden descendente.

-...

Python (Python 3.11)

``python
Solución de clase:
def mayor Integer(self, num: int) - título int:
s = list(str(num))
n = len(s)

para i en rango(n):
para j en rango(i + 1, n):
(int(s[j]) - int(s[i]) % 2 == 0:
s[i], s[j] = s[j], s[i]

volver int("".join(s))
`` `

■ *Nota pitónica*
■ El enfoque codicioso de dos vueltas es muy legible. Para entradas más grandes puede utilizar el método *sort‐byparity*, pero con la mayoría de 10 dígitos la solución simple es perfecta.

-...

### 3down⃣ C++ (C+17)

``cpp
Clase Solución {
public:
más grande Integer(int num) {
cadena s = to_string(num);
int n = s.size();

para (int i = 0; i) {}
para (int j = i + 1; j)
si (s[j] √≥ s[i] " (s[j] - s[i]) % 2 == 0)
swap(s[i], s[j]);
}
}
}
devolver stoi(s);
}
};
`` `

■ **C++ 17** – Usa `std::to_string`, `std::stoi`, and `std::swap`.
■ El modulo trick `(s[j] - s[i] % 2` funciona porque los caracteres `'0'`-`'9'` difieren por la misma cantidad que sus valores numéricos.

-...

## 📚 Blog Article – “Largest Number After Digit Swaps by Parity: The Good, The Bad, and the Ugly”

### Title

■ **Largest Number After Digit Swaps by Parity – Master the Interview Problem (Java, Python, C++)* *

## Meta Descripción

■ Solve LeetCode 2231 – Mayor número después de los desvíos por Parity – con soluciones Java, Python y C++. Entender la estrategia avaricia, las trampas y los consejos de entrevista. ¡Anota tu puntuación de la entrevista de codificación!

-...

#### Introduction

Si estás buscando un problema de entrevista *real-world* que prueba tus habilidades ** de manipulación de rayos** y tu intuición **algorítmica**, no busques más que LeetCode 2231: ** Número mayor después de las gotas de dígito por Paridad**. Es un problema “fácil” en la plataforma, pero esconde matices sutiles que pueden tropezar incluso programadores experimentados.

En este artículo, nos sumergimos profundamente en:

- La estrategia codictiva básica que garantiza el número máximo.
- Errores comunes (el “malo” y el “muy”).
- Tres soluciones de producción (Java, Python, C++).
- Cómo explicar la solución en un entorno de entrevista.

¡Vamos a romperlo!

-...

### The Good – Why It's Elegant

Por qué funciona
Silencio----------
Silencio **Greedy** Silencio Cada swap es local: siempre ponemos el mayor dígito posible (de la misma paridad) al lugar más disponible. Silencio
Silencio **Parity Preservation** TEN La restricción de paridad mantiene el problema solvable con un simple enfoque de tipo por grupo. Silencio
Silencio **O(d log d)** Silencio Con 'd ≤ 10' dígitos, el algoritmo es esencialmente constante-tiempo. Silencio
Silencio **No se necesita un gran entero** Silencio El resultado final encaja dentro de un entero firmado de 32 bits (`≤ 10^9`). Silencio

La elegancia reside en reconocer que cambiar dígitos de la misma paridad es equivalente a clasificar independientemente los dígitos extraños e incluso en orden descendente y luego volver a montarlos de acuerdo con el patrón de paridad original.

-...

### The Bad – Pitfalls You should avoid

1. *Asumiendo que puedes cambiar cualquier cosa*
❌ Swapping a `1` (odd) with a `4` (even) is illegal – many startner solutions wrongnly do this.

2. **Using Integer Arithmetic En lugar de String**
❌ Trabajar directamente con dígitos enteros (`num % 10`) puede llevar a errores cuando intenta cambiar dígitos en su lugar.

3. *Ignorando ceros principales*
Si bien el problema garantiza `num ю= 1`, usted podría pensar en los números que comienzan con `0`. Un algoritmo codicioso que sólo reordena dígitos puede crear inadvertidamente un cero líder si no tienes cuidado.

4. **Optimizing for Larger Numbers**
Debido a que `num' está capped en '10^9`, no hay necesidad de un montón o un tipo de conteo. La ingeniería excesiva puede hacer que su solución sea más difícil de entender.

-...

### Las trampas de la complejidad

- **Recursivo/Backtracking**
Algunos enfoques ingenuos intentan explorar cada permutación de swaps extraños/inclusos, lo que lleva a tiempo exponencial (`O(d!)`). Esto es *terrible* para incluso `d = 10`.

- Usando BigInteger
Un error común es analizar la cadena final de nuevo en "BigInteger" para evitar el desbordamiento, pero las limitaciones lo hacen innecesario, y "BigInteger" es más lento.

* Comprobación de paridad rota* *
Utilizando `(digit1 + digit2) % 2 == 0` es *incorrecto* para la comparación de paridad. La prueba correcta es `(digit1 - digit2) % 2 == 0` o `digit1 % 2 == digit2 % 2`.

-...

### Interview‐Ready Explanation

■ **“Primero se separan los dígitos en dos listas—dedos e inclusos. Luego ordeno cada lista descendiendo para que los dígitos más grandes estén en la parte delantera. Finalmente, paso por el número original, reemplazando cada dígito por el siguiente dígito más grande de la misma paridad de la lista correspondiente. El resultado es el entero más grande posible.”* *

Explique que el algoritmo es *verde* porque en cada paso escogemos la opción localmente óptima (el mayor dígito de paridad a la izquierda), y debido a los grupos de paridad independientes este óptimo local es también global.

-...

## Code Walkthrough

##### Java

``java
char[] digits = String.valueOf(num).toCharArray();
para (int i = 0; i) i++)
para (int j = i + 1; j) j++)
si (digits[j] "
(digits[j] - digitos[i]) % 2 == 0) {
t = dígitos[i];
dígitos[i] = dígitos[j];
dígitos [j] = t;
}
integer.parseInt(new String(digits));
`` `

* Por qué está limpio:* Dos bucles anidados, un simple cheque de paridad, y un intercambio en el lugar.

#### Python

``python
s = list(str(num))
para i en rango(len(s)):
para j en rango(i+1, len(s)):
(int(s[j]) - int(s[i]) % 2 == 0:
s[i], s[j] = s[j], s[i]
volver int("".join(s))
`` `

*Retorno pitónico:* Utilizando la sintaxis s[i], s[j] = s[j], s[i].

###### C++

``cpp
cadena s = to_string(num);
para (int i = 0; i) ++i)
para (int j = i+1; j) ++j)
si (s[j] √≥ s[i] " (s[j] - s[i]) % 2 == 0)
swap(s[i], s[j]);
devolver stoi(s);
`` `

*Highlights:* `std::swap` mantiene el código conciso.

-...

### Bono: Sort‐by‐Parity Approach (Alternative)

Si quieres enfatizar * surtido* en lugar de los dos bucles codiciosos, puedes hacer:

``java
Lista seleccionadaCaracterística propiedad impares = nuevo ArrayList recomendado();
Lista seleccionadaCaracterística uniformes = nuevo ArrayList implicado();

para (carc : dígitos) {
(c - '0') % 2 == 0) evens.add(c);
(c);
}
odds.sort(Collections.reverseOrder());
evens.sort(Collections.reverseOrder());

int o = 0, e = 0;
para (int i = 0; i) i++) {
si (digits[i] - '0') % 2 == 0) dígitos[i] = evens.get(e++);
dígitos[i] = odds.get(o++);
}
`` `

■ *Por qué sigue siendo “bueno”* Es un poco más largo pero hace que la *independencia de grupos de paridad* sea clara. En una entrevista, podría impresionar al entrevistador mostrando que ha considerado múltiples vías de solución.

-...

#### 🚀 Final Takeaway

LeetCode 2231 es un problema de entrevista *golden*. Dominar te da:

- Limitaciones de manejo de confianza y casos de esquina.
- Experiencia explicando claramente la lógica codictiva.
- Un patrón reutilizable (grupo → ordenar → reconstruir) que aparece en muchos problemas de matriz.

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀

-...

## Recursos > Lectura ulterior

- [LeetCode 2231 - Declaración de problemas](https://leetcode.com/problems/largest-number-after-digit-swaps-by-parity/)
- [Greedy Algorithms – Coursera](https://www.coursera.org/learn/greedy-algorithms)
- [Parity in Programming – Stack Overflow Q juntosA](https://stackoverflow.com/questions/ what-is-parity)

-...

### 📈 SEO Boost

- **Keywords**: “LeetCode 2231”, “Largest Number After Digit Swaps by Parity”, “Java solution”, “Python solution”, “C++ solution”, “greedy algoritmo”, “coding interview tips”, “array manipulation”, “parity restraint”, “algorithmic intuition”.
- **Caracteres**: Usar " armonizado " , " armonizado " , " armonizado " y " armonizado " para estructurar el contenido de los motores de lectura y búsqueda.
- **Imágenes**: Incluye un pequeño diagrama de “grupos o incluso grupos” y un diagrama de flujo del algoritmo.
- **Backlinks**: Repositorios oficiales de referencia LeetCode, Medium y GitHub para mayor exploración.

Con el código y la guía de entrevistas arriba, usted está listo para as LeetCode 2231 y mostrar su problema solución de problemas en cualquier entrevista técnica. ¡Feliz codificación!