-...
Título: LeetCode 44. Wildcard Matching -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## Wildcard Matching – LeetCode 44
**Hard ⋅ 2000 ≤ Наливывывые ≤ 2000 ный DP / Greedy вы Java / Python / C+**

■ “Las mejores preguntas de entrevista son las que puedes responder con confianza y explicar claramente.” *Job‐hunt 101*

-...

### 1. Panorama general de los problemas

Silencio en el campo
Silencio...
Silencio **Nombre** Silencioso Wildcard Matching Silencio
Silencioso **LeetCode ID**
Silencio **Dificultad**
Silencio ** Entrada** Silencio Dos cuerdas `s` (texto) y `p` (pattern)
Silencio ** Salida** Silencioso `verdad ' si `p` coincide con el *entire* `s ' , `falso ' de otro modo tóxico
Silencio **Las reglas de la tarjeta de seguridad** Silencioso `?` → cualquier carácter único indicabr confianza`*` → cualquier secuencia (incluso vacía)
Silencio **Constraints** Silencio `0 ≤ s.length, p.length ≤ 2000 `` sólo minúsculas ' letras inglesas recomendadabr título`p` sólo minúsculas letras inglesas, `?`, `*`

■ Ejemplo
"Aaa" = "p = "*" → true
's = 'cb', 'p = "?a" → false `

-...

### 2. Intuición

Necesitamos saber si las dos cuerdas pueden “alinearse”** cuando sustituimos “?” y “*” con los caracteres apropiados.

El problema es un programa dinámico clásico en cuerdas:

`` `
dp[i][j] = ¿s[0.i) match p[0.j)?
`` `

* `i` is the length of the considered prefix of `s`
* `j` is the length of the considered prefix of `p`

Con esta recurrencia podemos explorar todas las posibilidades **una vez** y conseguir espacio lineal a tiempo.

-...

### 3. Cuatro maneras de resolver

Silencio Silencio Silencio
Silencio------------------------------------...
Silencio **Recursivo** Silencio Pruebe todas las opciones al encontrar `*`. Silencio O(2^n) tiempo Silencio Muy intuitivo Silencio Tiempo expositivo, apilar el sobreflujo
Silencio **Memoizado** Silencio Igual que el tiempo recursivo + caché Silencio O(n m) tiempo, O(n m) espacio Silencio rápido, todavía legible Silencio Todavía utiliza pila de recursión ←
Silencio **Tabulación** Silencio Bottom‐up DP table  durable O(n m) time, O(n m) space tención No recursion, easier to debug  durable Memory heavy for 2000 × 2000 Silencio
Silencio **Space‐Optimized DP** Silencio Mantener sólo la fila anterior Silencio O(n m) tiempo, **O(m)** espacio Silencio 4 MB en C++/Java, 2000 * 2000 ♥ 4 MB Silencio Ligeramente más lógica para la primera columna Silencio

■ **Bonus** – una solución lineal de tiempo libre y constante que escanea de izquierda a derecha y retroceder cuando es necesario.
■ En la práctica, la solución DP es lo que la mayoría de los entrevistadores esperan, pero el truco codicioso puede ser una respuesta “gotcha”.

A continuación se presentan las tres versiones de código que deseará en su curriculum vitae y en su cartera de GitHub.

-...

## 4. Implementaciones de referencia

■ **Tip** – Mantenga una copia del código DP “limpio” en su GitHub, y mencione que usted *comprendió* la recurrencia cuando se le preguntó.

-...

#### 4.1 Java – Bottom‐Up DP (2‐D)

``java
// 44. Wildcard Matching – LeetCode
Solución de la clase pública {}
*
* Classic DP: dp[i][j] == true if s[0.i) match p[0.j)
* Utilizamos (n+1) x (m+1) mesa booleana, donde n = s.length(), m = p.length()
*/
booleano público esMatch(String s, String p) {
int n = s.length(), m = p.length();
booleano[][] dp = nuevo booleano[n + 1][m + 1];
dp[0][0] = verdadero; // patrón vacío coincide con cadena vacía

/* Primera fila: s está vacía – sólo liderar '* en p puede coincidir */
para (int j = 1; j)
si (p.charAt(j - 1) == '*) dp[0] [j] = dp[0][j - 1];
}

/* Rellene la tabla */
para (int i = 1; i) = n; i++) {
para (int j = 1; j)
char pc = p.charAt(j - 1);
si (pc == '*) {}
dp[i][j] = dp[i - 1][j] [j]
} si (pc == '?'
dp[i][j] = dp[i - 1][j - 1];
. ♫ ... {
dp[i][j] = false;
}
}
}
dp[n][m];
}
}
`` `

*Time*: **O(n m)**
*Espacio*: **O(n m)** – para 2000 × 2000 esto es ~4 MB, fino para LeetCode.

-...

##### 4.2 Python – Space-Optimized DP

``python
# 44. Wildcard Matching – Python 3
def is_match(s: str, p: str) - Bool:
n, m = len(s), len(p)

# prev[j] is dp[i-1][j] from the previous row
* (m + 1)
prev[0] = True

# Inicia la primera fila (vacío s)
para j en rango(1, m + 1):
si p[j - 1] == '*
prev[j] = prev[j - 1]

para i en rango(1, n + 1):
curr = [False] * (m + 1)
curr[0] = Falso # non-empty s no puede coincidir con el patrón vacío
para j en rango(1, m + 1):
si p[j - 1] == '*
curr[j] = prev[j] o curr[j - 1]
elif p[j - 1] == '?' o p[j - 1] == s[i - 1]:
curr[j] = prev[j - 1]
más:
curr[j] = Falso
prev = curr

retorno prev[m]
`` `

*Espacio*: **O(m)** (Edición 2001 booleanos ♥ 2 KB)
*Tiempo*: **O(n m)** (consumir 4 millones de operaciones – trivial para el CPython).

-...

#### 4.3 C++ – Subir DP con rayos 1-D

``cpp
// 44. Juego de tarjetas silvestres – C++17
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
bool isMatch(string s, string p) {}
int n = s.size(), m = p.size();
vector asignadobool confianza prev(m + 1, false), curr(m + 1, false);
prev[0] = verdadero; // patrón vacío coincide con cadena vacía

// Texto vacío, sólo liderar '*' puede coincidir
para (int j = 1; j)
si (p[j - 1] == '*) prev[j] = prev[j - 1];

para (int i = 1; i) = n; ++i) {}
curr[0] = falso; // texto no vacío no puede coincidir con el patrón vacío
para (int j = 1; j)
si (p[j - 1] == '*)
curr[j] = prev[j] Silencio infligido[j - 1];
si (p[j - 1] == '?' s[i - 1])
curr[j] = prev[j - 1];
más
curr[j] = falso;
}
prev.swap(curr);
}
retorno prev[m];
}
};
`` `

*Pace*: **O(m)**
*Time*: **O(n m)** – de nuevo ~4 millones de operaciones, lo suficientemente rápido incluso en una entrevista estrecha.

-...

## 4.4 Greedy Linear-Time, Constant‐Space Solution

■ ¿Por qué hablar de codicia? * *
■ En muchos paneles de entrevista, una solución *single‐pass* es un factor “wow”. El algoritmo codicioso es también la respuesta de entrevista *canónica* para este problema.

``text
Camina por s y p una vez.
Mantenga dos puntos:
i – índice actual en s
j – índice actual en p
Realizar un seguimiento de:
starIndex – el más reciente '*' en p (o -1 si no)
iAfterStar – índice en s cuando el último '* fue igualado

Si los personajes coinciden o p[j] == '?', avance ambos.
Si p[j] == '*', recuerda las posiciones y salta '*'.
Si el desajuste y tenemos un '* anterior, retroceder:
j = starIndex + 1 (reutilizar el '*)
i = iAfterStar + 1 (consumir un char más de s)
iAfterStar = i
Si el desajuste y no "*", devuelve falso.
`` `

*Time*: **O(n + m)**
*Espacio*: **O(1)**
*Bien por entrevistas*: se puede explicar el razonamiento en 3 a 5 minutos.

■ **Caveat** – Greedy sólo trabaja para esta gramática de comodín (`?` y `*`). Para otros comodines puede fallar.

-...

### 4. Trade-offs – Good, Bad, Ugly

Silencio Silencio
Silencio------------Prince------
Silencio **Readability** ← La memoización Recursiva es más simple la tabla de DP de la vida puede ser enorme ← Greedy necesita cuidadosos punteros juggling
Silencio **Performance** Silencio Greedy es lineal Silencio DP utiliza memoria O(n m) (Ω 4 MB) Silencio La recursión exponencial puede apilar sobre el flujo ←
Silencio **Edge-cases** Silencio Todo `*` en patrón → coincide con la cuerda vacía Silencio Necesita manejar las cuerdas vacías por separado ← Off‐por-uno los errores son comunes en el manual DP ←
Silencio **Entrevista percepción** Silencio DP muestra comprensión de la cuerda DP ← Greedy demuestra la creatividad algorítmica tención Recursive se puede ver como "perezosa" y no óptima

■ **Key Takeaway** – *Siempre empezar con la solución de trabajo más simple (recursiva), luego “acelerar” a un DP listo para la producción. En las entrevistas, el paso de actualización (memoización de la cama o tabulación) demuestra habilidades de solución de problemas. *

-...

### 5. Lista de verificación para entrevistas

1. **Clarificar el “sentido real”** – patrón debe cubrir *todo* de `s.
2. **Explicar semántica de tarjetas silvestres** – escríbalas explícitamente.
3. **Pregunte sobre las limitaciones de tiempo/espacio** – confirme 2000×2000 encaja en la memoria.
4. **Mostrar la recurrencia DP** – dibujar la rejilla 'dp[i][j].
5. ** Código de la palabra en el idioma de la entrevista** – use Java/Python/C++ como se solicite.
6. **La mención del truco codicioso** – a veces los entrevistadores quieren que pienses fuera del DP.
7. **Espera un ejemplo no-trivial** – por ejemplo, `s="abbcd", p="*b?d" para demostrar las transiciones estatales.
8. **Preguntar preguntas aclaratorias** – por ejemplo, “¿Qué hay de patrones con múltiples “*” consecutivos?” – para mostrar un profundo entendimiento.
9. ** Casos de borde de discusión** – cuerdas vacías, todo `*`, o patrón comienza con `*`.
10. **La complejidad del espacio-tiempo** – siempre esclarece y compara.

-...

### 6. Pensamientos finales

Wildcard Matching es uno de esos problemas “Hard” que ** cambia de fuerza bruta a DP elegante. Dominar te da:

- Una comprensión sólida de **estring DP** que se aplica a muchos problemas de LeetCode (por ejemplo, “Regular Expression Matching”, “Decode Ways”).
- Una plantilla DP** optimizada para el espacio puede entrar en cualquier entrevista.
- La capacidad de lanzar una solución **grande** cuando usted necesita impresionar.

Agregue las implementaciones de referencia a su cartera, escriba un artículo de blog rápido o un vídeo corto que explique el algoritmo, y estará bien posicionado para marcar alto tanto en pantallas técnicas como en pruebas de codificación.

Buena suerte con su viaje de codificación y la próxima entrevista!

-...

## 7. Bibliografía " Lectura ulterior "

- Problema de LeetCode 44** – [Wildcard Matching](https://leetcode.com/problems/wildcard-matching/)
- **Cracking the Coding Interview – String DP** – Chapters on “Dynamic Programming” and “Regular Expressions”.
- **GeeksforGeeks – Wildcard Matching** – proporciona el camino codicioso.

-...

**Meta-note** – Si usted está preparando un video o blog post, incrustar el código snippets con resaltado de sintaxis. A los clientes les encanta ver una solución limpia y bien adaptada.

¡Feliz codificación! 🚀

-...

SEO Palabras clave**: LeetCode 44 Wildcard Matching, Java DP solution, Python wildcard regex, C++ 1D array DP, algoritmo codicioso para Wildcard, consejos de entrevista, programación dinámica de cadenas, complejidad del tiempo, optimización del espacio.

-...

*(End of reference guide – no dude en adaptarse o extenderse con pruebas unitarias o JUnit en Java.) *