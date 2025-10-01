-...
Título: LeetCode 2486. Personajes del Apéndice a la Cuerda para Hacer Subsequencia -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Append Caracteres to String to Make Subsequence – 2486 (LeetCode)

## TL;DR
Encuentra el prefijo más largo de **t** que ya aparece como una subsequencia en **s**.
La respuesta es simplemente `len(t) – emparejado`.
Complejidad: **O(n + m)** tiempo, **O(1)** espacio.

-...

## Problema Declaración

Se le dan dos cuerdas `s` y `t` que contienen sólo minúsculas letras inglesas.

Devuelve el número mínimo de caracteres que deben ser anexados al *end* de `s` para que `t` se convierta en una subsequencia de la nueva cadena.

■ **Subsequence** – una cuerda que puede derivarse de otra eliminando cero o más caracteres sin cambiar el orden de los caracteres restantes.

■ *Examples*

Silencio Silencio Silencio .
Silencio----------------------------------------------------------
Silencio "coaching" Silencioso "coding" Silencio 4 Silencio Apéndice "ding". Silencio
Silencio "abcde" Silencio "a" Silencio 0 Silencio Ya una subsequencia. Silencio
TENIDO "z" TENIDO "abcde" TENIDO 5 ANTETENIDO Apéndice completo "t". Silencio

**Constraints* *

- 1 ≤ s.length, t.length ≤ 105 `
- `s` y `t` consisten sólo en letras inglesas minúsculas.

-...

## The Good, the Bad, and the Ugly

TENIDO Aspecto Silencio Por qué importa TENIDO Cómo manejarlo
Silencio...
Silencio **Bueno** Silencioso *Un enfoque de dos puntos* es lineal y constante espacio. TEN Iterate una vez sobre ambas cuerdas, aumento de punteros sólo cuando se encuentra un partido. Silencio
Silencio **Bad** Silencio Muchos candidatos confunden *subsequence* con *substring* o *prefijo*. Silencio Tenga en cuenta la definición; somos personajes iguales en orden, pero pueden ser no contiguos en `s`. Silencio
Silencio **Ugly** Silencio Casos Edge donde `s` está vacío o `t` es más largo que `s`. Silencio El algoritmo naturalmente devuelve `len(t)` cuando ningún personaje coincide. No es necesario un manejo especial. Silencio

-...

Algoritmo - Dos punteros

1. **Initializar dos índices**
I ' - index in `s ' (0 ... `s.length‐1`)
j ' - index in `t ' (0 ... `t.length‐1`)

2. Traverse `s`**
Mientras que " yo " , la longitud " y " la fuerza " ,
- Si `s[i] == t[j]`, muévete *ambos** `i` y `j`.
- Si no, muévete solo.

3. Resultado**
El número de caracteres dejados en `t` es `t.length - j`.
Este es el número mínimo de caracteres que deben ser anexados a `s`.

-...

## Correctness Proof (Sketch)

Deja 'k = j' después del bucle.
All indices `0 ... k‐1` of `t` have been matched in order inside `s`.
Por construcción, ningún personaje posterior de `t` (`k ... t.length‐1`) tiene un carácter correspondiente en `s` después del prefijo emparejado, de lo contrario el bucle habría emparejado y aumentado `j`.

Appendiendo del sufijo `t[k ...]` al final de `s` crea una nueva cuerda donde los primeros `k` caracteres de `t` ya son una subsequencia (la parte emparejada) y el sufijo restante aparece verbatim al final.
Así `t` se convierte en una subsequencia de la nueva cuerda.

Ningún número menor de caracteres puede bastar porque cada personaje de 't[k ...]` no está presente en la parte igualada de `s`.
Por lo tanto, `t.length - k` es óptimo.

-...

## Complexity Analysis

TENCIÓN TERRITOR TENIDA Cálculo
Silencio----------
Silencio **Tiempo** Silencio Cada carácter de `s` es examinado al máximo una vez. `O(Las vidas eternas +  sometidat sometida)` Silencio
tención **Espacio** Silencioso Sólo dos índices enteros. `O(1)` Silencio

-...

## Implementation

A continuación se presentan soluciones limpias y idiomáticas en **Java**, **Python**, y **C+**.

### 1. Java

``java
Clase Solución {
public int append Personajes(String s, String t) {
int i = 0, j = 0;
int n = s.length(), m = t.length();

mientras (i י n ' t
si (s.charAt(i) == t.charAt(j) {}
j++; // coincide con un personaje de t
}
i++; // siempre moverse en s
}
volver m - j; // caracteres dejados al apéndice
}
}
`` `

■ **Por qué funciona esto* – `I` escanea `s` lineally. Cada vez que golpeamos un personaje de `t`, movemos `j`. Después del bucle `j` equivale al prefijo más largo de `t` que es una subsequencia de `s`.

### 2. Pitón

``python
Solución de clase:
def appendCharacters(self, s: str, t: str) int:
I = j = 0
mientras que yo hice el len(s) y j
si s[i] == t[j]:
j += 1
i += 1
devolver len(t) - j
`` `

### 3. C++

``cpp
Clase Solución {
public:
int appendCharacters(string s, string t) {}
int i = 0, j = 0;
mientras (i) > (int)size() > j > (int)t.size()) {}
si (s[i] == t[j] ++j;
++i;
}
t.size() - j;
}
};
`` `

Los tres francotiradores siguen el mismo patrón de dos puntos.

-...

## Unit Tests (Python example)

``python
def test():
sol = Solución()
afirma sol.appendCharacters("coaching", "coding") == 4
afirmar sol.appendCharacters("abcde", "a") == 0
afirmar sol.appendCharacters("z", "abcde") == 5
afirmar sol.appendCharacters("", "abc") == 3
afirmar sol.appendCharacters("abc", "") == 0
afirmar sol.appendCharacters("aaa", "aaab") == 1
print("Todas las pruebas pasadas.")
`` `

Ejecute `pithon -m unittest` para validar la implementación.

-...

## SEO‐Optimized Blog Post

■ **Título:** *Características del apéndice para hacer la subsequencia – 2486 peru LeetCode Solution (Java/Python/C++)*
■ **Meta Descripción:** Master LeetCode #2486 con una solución limpia de dos puntos en Java, Python y C++. Comprender las subsecuencias, los casos de borde y el tiempo de funcionamiento óptimo.

#### Introduction

LeetCode 2486, “Características de Apéndice para Estring to Make Subsequence”, es un favorito para entrevistas de manipulación de cadenas. En este post descomponemos el problema, presentamos una solución **fast** y ** amigable con memoria**, y entregamos códigos listos para copiar en Java, Python y C+++.

### El problema en una línea

■ Encuentra el número mínimo de caracteres que necesitas para anexar a `s` para que `t` se convierta en una subsequencia de la nueva cadena.

### Why It's a Classic Interview Question

- Prueba tu comprensión de **subsequence vs. subestring**.
- Requiere una solución **O(n+m)**; muchas soluciones ingenuas funcionan en tiempo cuadrático.
- Muestra tu habilidad con las técnicas **2 puntos**—un básico en entrevistas de codificación.

### Approach Overview

1. Escanear `s` con un puntero `i`.
2. Mantenga un segundo puntero " j " para `t ' .
3. Cada vez que `s[i]` equivale a `t[j]`, incremento `j`.
4. Después de la exploración, `j` indica cuántos caracteres de `t` fueron emparejados.
5. La respuesta es `len(t) – j`.

Este es **tiempo lineal** y ** espacio constante**—lo mejor que puedes esperar.

### Handling Edge Cases

- `s` vacía → respuesta = `len(t)`.
- `t` long than `s` → the same formula works.
- Cartas duplicadas – el escaneo de dos puntos todavía funciona porque sólo nos importa el orden, no la contigüidad.

### Código Snippets

*(Insert Java, Python, C++ bloques de código desde arriba.) *

### Quick‐Start Test Suite

*(Insertar código de prueba.) *

#### Summary

La solución de dos puntos es la parte **buena**: rápida, sencilla y fácil de razonar. La parte **bad** es la confusión entre subsequencia y subestring; ¡recuerda la definición! La parte **ugly** a menudo aparece en los casos de borde (cadetas vacías, muy largas 't'), pero el algoritmo maneja con gracia sin ramas adicionales.

**¿Quieres empezar tu próxima entrevista de codificación?** Practicar este problema, ajustar el código para diferentes idiomas, y explicar la idea de dos puntos claramente a tu entrevistador.

-...

## Pensamientos finales

- Mantenga la definición de subsequencia en mente. #
- La solución de dos puntos es el estándar de oro.
- La aplicación es idéntica en todos los idiomas, sólo adapte la sintaxis.

¡Buena suerte con tu práctica de LeetCode y tus próximas entrevistas! Si te gustó este artículo, no dudes en compartirlo en LinkedIn o Twitter. ¡Feliz codificación!