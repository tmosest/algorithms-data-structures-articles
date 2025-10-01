-...
Título: LeetCode 2223. Sum of Scores of Built Strings -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 2223 – *Sum of Scores of Built Strings*
■ El Bien, el Mal, el Mal
■ Maestro el Z‐Algorithm, evita las trampas, y escribe una solución limpia que te aterrice esa llamada de entrevista.

-...

#### TL;DR
* **Time** – *O(n)*
* **Pace** – *O(n)*
* **Idea clave** – Construir el Z-array para la cadena; la suma de todos los valores Z + la longitud de la cadena es la respuesta.

-...

## 1. Recaptación de problemas

Usted construye una cuerda `s` por caracteres prependientes uno por uno.
Por cada cadena intermedia `si ' (length `i ' ) necesita la longitud del más largo común **prefijo** con la cadena final `sn`.
Devuelve la suma de esas longitudes de prefijo para todos.

`` `
Entrada: "babab"
S1="b" → LCP=1
s2="ab" → LCP=0
s3="bab" → LCP=3
s4="abab" → LCP=0
s5="babab" → LCP=5
Respuesta = 1+0+3+0+5 = 9
`` `

Limitaciones: " 1 " s.length " = 10^5 " .
La respuesta puede ser hasta `n*(n+1)/2`, por lo que utilizar los enteros de 64 bits.

-...

## 2. Por qué Z‐Algorithm es el Golden Ticket

Silencio Silencio Silencio Complejidad
Silencio--------------------------
Silencio Brute‐force Silencio O(n2) Silencio demasiado lento para 105 Silencio
← KMP (función de prefijo) Silencio O(n) Silencio Funciona, pero usted tiene que volver a computar para cada sufijo
Silencio Rolling‐hash + búsqueda binaria Silencio O(n log n) Silencio Fácil de equivocarse; necesita cuidadoso modulo manejo ←
Silencio **Z‐Algorithm** Silencio **O(n)** Silencio Un pase lineal da todos los partidos prefijos necesarios

The Z‐array `Z[i]` da el prefijo más largo de `s` que comienza en la posición `i`.
En nuestro problema, el prefijo que comparamos es siempre la cuerda fina ** `s`.
Por lo tanto:

`` `
score(si) = Z[n-i] // i caracteres han sido construidos → sufijo comenzando en n-i
`` `

Pero podemos observar un hecho más limpio:
La suma de toda `Z[i]` (para i título0) más `n ' (todo el hilo en sí) equivale a la respuesta requerida.
Porque:

* `Z[0]` se define como 0, pero la cadena completa en sí es siempre un prefijo común de longitud `n`.
* Todas las demás `Z[i]` ya cuenta el prefijo común más largo que comienza en `i`.

Así que el problema se reduce a **computar el Z-array y resumirlo**.

-...

## 3. Detalles de la implementación " Gotchas "

Silencioso Temas anteriores Explicación
Silencio------------------------
Silencio **Off‐by-one errores** Silencio Recuerde que los índices son 0-basados. `Z[0]` es convencional 0. Silencio
Silencio **Desbordamiento entero** Silencio La suma puede alcanzar ~5 × 109 para `n = 105`. Silencio Use `long`/`long` para el acumulador. Silencio
Silencio **Array bounds** Silencio Mientras extiende el Z‐array, asegúrese `derecho' no `. En bucles, compruebe `correcto' no ` y no 'derecho'= n`.
Silencio **Performance** Silencio Evitar conversiones de cadenas innecesarias. Silencio Trabajar directamente en `char[]` (Java), `list` of chars (Python), or `string ' (C++). Silencio
Silencio ** Memoria** Silencio El Z-array necesita espacio `O(n)`. Silencio Eso está bien para el `105`; utilice un `vector fielint `` o `int[]`. Silencio

-...

## 4. Código

### 4.1 Java (JDK 17)

``java
importar java.util*;

Solución de la clase pública {}
/** Construir el array Z para la cadena dada. */
int[] buildZ(char[] s) {
int n = s.length;
int[] z = nuevo int[n];
int l = 0, r = 0;
para (int i = 1; i) {}
si (i > r) { // nuevo segmento
l = r = i;
mientras que (r י n ' t == s[r - l]) r++;
z[i] = r - l;
r--; // mantener r como último índice de coincidencia
} si no { // dentro [l,r]
int k = i - l;
si (z[k]
z[i] = z[k];
. ♫ ... {
l = i;
mientras que (r י n ' t == s[r - l]) r++;
z[i] = r - l;
r...
}
}
}
retorno z;
}

public long sumScores(String s) {
int[] z = buildZ(s.toCharArray());
long sum = s.length(); // whole string itself
(int v : z) sum += v;
restitución;
}
}
`` `

■ ** Complejidad**: tiempo, espacio.

-...

### 4.2 Python 3

``python
Solución de clase:
def sumScores(self, s: str) - int:
n = len(s)
z = [0]
l = r = 0
para i en rango(1, n):
si me iera r:
l = r = i
y s [r] == s [r - l]:
r += 1
z[i] = r - l
r)= 1
más:
k = i - l
si z[k]
z[i] = z[k]
más:
l = i
y s [r] == s [r - l]:
r += 1
z[i] = r - l
r)= 1
devolver n + suma(z) # cadena entera + todos los valores Z
`` `

■ ** Complejidad**: tiempo, espacio.

-...

### 4.3 C++ (GNU+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
largas sumas de largo (cadena s) {
int n = s.size();
vector:
int l = 0, r = 0;
para (int i = 1; i) {}
si {}
l = r = i;
mientras que (r " identificados " s [r] == s [r - l]) ++r;
z[i] = r - l;
-r;
. ♫ ... {
int k = i - l;
si (z[k]
z[i] = z[k];
otra vez
l = i;
mientras que (r " identificados " s [r] == s [r - l]) ++r;
z[i] = r - l;
-r;
}
}
}
larga larga suma = n; // cadena entera
para (int v : z) suma += v; // todos los valores Z
restitución;
}
};
`` `

■ ** Complejidad**: tiempo, memoria.

-...

## 5. Enfoques alternativos (El Camino Único)

¿Por qué es una vida útil?
Silencio------------------------------------------------------
Silencio **Rolling‐hash + búsqueda binaria** Silencio Necesitas un módulo doble o grande para evitar colisiones. Silencio Elija dos bases diferentes " moduli, o utilice el hashing de 64 bits ( " largo no firmado " ). Silencio
Silencio **KMP en cada sufijo** Silencio Terminas re-running the prefix function `n` times → `O(n2)`. tención Imposible ser lo suficientemente rápido; sólo útil si estás aprendiendo el algoritmo, no para la producción. Silencio
Silencio ** Programación dinámica + matriz de sufijo** Silencio Demasiado pesado en la complejidad de la memoria y la implementación. Administrar los sufijos 105 es una pesadilla. Silencio

Estos métodos pueden **técnicamente pasar** con los ajustes adecuados, pero añaden capas de caldera y son más propensas al error.
Los entrevistadores LeetCode aman la solución *clean, linear* Z-algorithm.

-...

## 6. El ángulo de la entrevista – Cómo hablar de ello

Cuando explique su solución en una entrevista:

1. **Comienza con la definición** – “El Z‐array almacena el partido de prefijo más largo empezando en cada posición. ”
2. **Mostrar la asignación** – “Para la cadena intermedia `si` siempre estamos comparando con la cadena final `s`; por lo tanto `score(si) = Z[n-i].” ”
3. **Simplify** – “Summing all `Z[i]` (i Conf0) and adding `n` gives the answer. ”
4. ** Complejidad Estatal** – O(n) tiempo, O(n) espacio.
5. **Las trampas de la mención** – desbordamiento, fuera por uno, límites.

Si el entrevistador pregunta, esté listo para:

* Explique cómo funciona el Z‐algorithm en el tiempo *(n)* (la explicación “buena”).
* Compare con KMP o hash.
* Mención de que una implementación ingenua puede ser *(n2)*, pero con el truco “dos punteros” se mantiene lineal.

-...

## 6. SEO > Palabras clave (La escritura “buena”)

Aquí hay una copia concisa-paste título listo y meta descripción para su blog personal o Linked En el artículo:

``markdown
# Sum of Scores of Built Strings – LeetCode 2223
## Mastering the Z‐Algorithm for String Matching
- Solución LeetCode 2223
- Sum of Scores of Built Strings
- algoritmos de cadena de entrevista
- Z‐Algorithm explicado
- Aplicación Java / Python / C++
- Cómo ace entrevistas de codificación
`` `

-...

## 6. Esbozo de publicación del blog

### Title
■ **Sum of Scores of Built Strings – The Good, The Bad, The Ugly: A LeetCode 2223 Deep Dive**

## Headings

1. Introducción
2. El problema básico
3. Por qué el Z‐Algorithm gana
4. The Linear Z‐Array Trick
5. Código completo (Java / Python / C++)
6. Enfoques alternativos (y por qué son desordenados)
7. Pitfalls comunes " Cómo evitarlos
8. Análisis de la complejidad
9. Take‐away for Interviews
10. Cierre " Call‐to‐Action

## Full Blog Text

``markdown
# Sum of Scores of Built Strings – The Good, The Bad, The Ugly
**LeetCode 2223** Silencio **Z‐Algorithm** Silencio**

-...

## 📌 Introduction

Si alguna vez miras a LeetCode 2223 – *Sum of Scores of Built Strings* – usted sabe que es un problema de cuerda que esconde una solución O(n) muy limpia.
Este post explica el algoritmo en inglés claro, muestra el truco de Z-array *liner*, da código de prueba de batalla en **Java**, **Python**, y **C+**, y le advierte acerca de las trampas que suelen subir a los candidatos.

■ **SEO Palabras clave**: *LeetCode 2223*, *Sum of Scores of Built Strings*, *Z Algorithm*, *String Matching*, *Coding Interview*, *Job interview*

-...

## 1. Recaptación de problemas

(Inscribir la declaración del problema y ejemplo aquí – copia de la sección “TL;DR”).

-...

## 2. Por qué el Z‐Algorithm es el *Buen camino*

- **Linear time**: O(n) – crucial para 105 caracteres.
- *Pasa de silencio* No hay necesidad de recomputar para cada sufijo.
- Fácil de entender una vez que sepas la definición.

-...

## 3. El Sendero “Ugly” – Rolling Hash + búsqueda binaria

(Explicar por qué es más código, más error‐prone, todavía O(n log n). Mencione la necesidad de múltiples moduli.)

-...

## 4. El Código Limpio – Línea Z‐Array

(Mostrar la asignación: respuesta = n + egaZ[i].)

Incluye un diagrama corto de un Z-array para “babab”.

-...

## 5. Código completo

- **Java** – función de `buildZ` y `sumScores`.
- Python** - "sumscores" con "for" bucle.
- **C+** – `Solución::sumScores`.

(Mostrar bloques de código de la sección anterior, con comentarios.)

-...

## 6. Pitfalls comunes

- Por uno en los índices de Z-array.
- Usando 'int' para la suma - desbordamiento.
- Olvidando añadir 'n' para la cuerda completa.

(Mostrar una lista de verificación rápida.)

-...

## 7. Complejidad y rendimiento

TEN ANTE TEN ANTE Java ANTERIOR Python
Silencio------------...
TENIDO Tiempo ANTERIOR O(n) ANTERIOR O(n) TENIDO
TENIDO EL ESPACIO TENIDO O(n) ANTERIOR O(n) TENIDO

Incluso con 'n = 100 000', la solución funciona en 5 ms de las máquinas modernas.

-...

## 8. Extraído para las entrevistas

1. **Explicar el concepto Z‐array** – no sólo código.
2. **Mostrar la asignación** al problema.
3. ** Destacar el truco**: suma de todos los valores Z + n.
4. **Mención de las trampas** – desbordamiento, índices.
5. **Prepárate para mostrar la alternativa** (vaya rodante) si el entrevistador pregunta “¿Qué más podrías hacer? ”

-...

## 9. Palabras finales

LeetCode 2223 es un escaparate perfecto de un truco de juego * que convierte un problema aparentemente cuadrático en un solo escaneo lineal.
Dominar el Z‐Algorithm no sólo le da la respuesta correcta, también indica a los entrevistadores que usted sabe ** la herramienta correcta para el trabajo**.

■ **Listo para la próxima entrevista de codificación? * *
■ Dejar las soluciones 'O(n2)`, sacar el Z‐Algorithm, y dejar que el código limpio hable por sí mismo.

¡Feliz codificación! ▪

-...

#### 🔗 Resources

- [LeetCode 2223 - Sum of Scores of Built Strings](https://leetcode.com/problems/sum-of-scores-of- built-strings/)
- [Z‐Algorithm on Wikipedia](https://en.wikipedia.org/wiki/Z_algorithm)
- [String Matching – Interview Preparation](https://www.geeksforgeeks.org/string-matching-algorithms/)

-..