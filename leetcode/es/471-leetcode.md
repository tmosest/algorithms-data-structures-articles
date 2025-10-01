-...
Título: LeetCode 471. Encode String con la longitud más corta -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

# 471. **Codificación de la cuerda con la longitud más corta**
■ **Hard** – LeetCode

■ **Problema**:
■ Se le da una cuerda `s` que consiste sólo de letras minúsculas.
■ Encode it using the rule `k[encoded_string]` donde el `encoded_string` se repite exactamente 'k' veces.
■ La cadena codificada debe ser **shorter** que el original; de lo contrario, mantener el original.
■ Volver *cualquier* codificación más corta posible.

■ *Examples*

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
Silencio `'aaa'` Silencio `'aaa'`
Silencioso `'aaaaa' '' Silencio `"5[a]" Silencio `5[a]` es más corto
Silencio `'aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''' '''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

■ **Constraints**
■ `1 ≤ s.length ≤ 150`
> `s` contiene sólo minúsculas letras en inglés.

-...

## Why It Matters

- El problema es una pregunta de entrevista clásica** que prueba la programación dinámica, la manipulación de cuerdas y la creatividad en el manejo de los bordes.
- Es un buen escaparate para su capacidad de diseñar soluciones óptimas** para problemas de cuerda * no-trivial*: una habilidad esencial para los ingenieros de vanguardia/de back-end, científicos de datos y roles centrados en algoritmos.
- Una aplicación limpia y bien coordinada de este problema demuestra competencia en *Java*, *Python* y *C++*, los tres idiomas de programación más buscados mediante la contratación de administradores.

-...

## Solution Overview

La solución óptima es un DP **3-dimensional** que funciona en el tiempo `O(n3)` (con `n ≤ 150`, esto es perfectamente fino).

1. ** mesa redonda**
`dp[i][j]` = *shortest encoded string* for the substring `s[i ... j]`.

2. ** Initialización**
Para cada personaje único `dp[i][i] = s[i]`.

3. **Recurrencia**
Por cada longitud `len' de `2` a `n `
- **Split** el subestring en dos partes `s[i ... k]` y `s[k+1 ... j]`.
`dp[i][j] = min(dp[i][k] + dp[k+1][j]).
- **Comprobar la repetición**:
Que la longitud de la subestring sea 'len'.
Por cada divisor `k ' de `len ' (excluido `len ' mismo):
*Si* la subestring está hecha de repeticiones 'len / k` de sus primeros caracteres 'k', podemos codificarlo como
`cnt[k] + "[" + dp[i][i+k-1] + "]".
Mantenga el resultado más corto.

4. **Retorno** `dp[0][n-1].

**Ayudante clave** – 'findPatternLength(sub)`
Revise el período mínimo de una cadena en `O(len)` utilizando la función de prefijo KMP. Se utiliza para identificar patrones repetidos de manera eficiente.

-...

# Código #

A continuación se presentan tres soluciones limpias y totalmente adaptadas: una en **Java**, una en **Python**, y otra en **C+**.

■ **Nota**: Los tres usan la misma lógica y se pueden copiar en su IDE o caja de sumisión.

-...

#### ## 1down⃣ Java

``java
importar java.util*;

Solución de la clase pública {}
public String code(String s) {
int n = s.length();
String[][] dp = new String[n][n];

1. Cartas individuales
para (int i = 0; i < n; i++) dp[i] = String.valueOf(s.charAt(i));

// 2. DP para todas las longitudes
for (int len = 2; len = n; len++) {}
para (int i = 0; i + len - 1 < n; i++) {
int j = i + len - 1;
dp[i][j] = s.substring(i, j + 1); // initial: the raw substring

/ 2.1 Split
para (int k = i; k) {}
candidatos a la cadena = dp[i][k] + dp[k + 1][j];
si (candidate.length()
dp[i][j] = candidato;
}

2.2 Repetición
int patternLen = findPatternLen(s.substring(i, j + 1));
si (patternLen) { // sólo si encontramos una repetición
int times = len / patrón Len;
Crianza codificada = tiempos + "[" + dp[i][i + patrónLen - 1] + "]";
si (encoded.length()
dp[i][j] = codificado;
}
}
}
dp[0][n - 1];
}

// Función de prefijo KMP para encontrar el período mínimo
int findPatternLen(String sub) {
int n = sub.length();
int[] lps = nuevo int[n];
por (int i = 1, len = 0; i) {
si (sub.charAt(i) == sub.charAt(len)) {
lps[i+] = ++len;
} si (len!= 0) {
len = lps[len - 1];
. ♫ ... {
lps[i+] = 0;
}
}
int period = n - lps[n - 1];
(n % period == 0) Período : n;
}
}
`` `

-...

#### 2down⃣ Python

``python
Solución de clase:
def encode(self, s: str) - título str:
n = len(s)
dp = [["] * n for _ in range(n)]

# Single letters
para i en rango(n):
dp[i][i] = s[i]

# DP for all lengths
para longitud(2, n + 1):
para i en rango(n - longitud + 1):
j = i + longitud - 1
sub = s[i:j + 1]
dp[i][j] = subproceso en bruto

# Split
para k en rango(i, j):
cand = dp[i][k] + dp[k + 1][j]
si len(cand)
dp[i] [j] = cand

Repetición
período = auto._período(sub)
si el período se realiza longitud: # la repetición existe
tiempo = longitud // período
cand = f"{times}[{dp[i][i + period - 1]}]
si len(cand)
dp[i] [j] = cand

retorno dp[0][n] - 1]

def _period(self, s: str) - int:
""Retorno mínimo período de cadena s (utilizando KMP).""
n = len(s)
lps = [0]
para i en rango(1, n):
j = lps[i - 1]
mientras j > 0 y s[i] s[j]:
j = lps[j - 1]
si s[i] == s[j]:
j += 1
lps[i] = j
período = n - lps[-1]
período de retorno si n % período == 0 más n
`` `

-...

#### 3down⃣ C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
string encode(string s) {
int n = s.size();
vector realizador seleccionado(n));

// letras individuales
para (int i = 0; i) no; ++i) dp[i] = string(1, s[i]);

for (int len = 2; len י= n; ++len) {}
para (int i = 0; i + len - 1  won n; ++i) {}
int j = i + len - 1;
cadena sub = s.substr(i, len);
dp[i][j] = sub; // subestring crudo

/ Split
para (int k = i; k)
string cand = dp[i][k] + dp[k + 1][j];
si (cand.size()
dp[i][j] = cand;
}

// Repetición
int period = findPeriod(sub);
si (período неленных len) { // Encontramos una repetición
int times = len / period;
cadena cand = to_string(times) + "[" + dp[i][i + periodo - 1] + "]";
si (cand.size()
dp[i][j] = cand;
}
}
}
dp[0][n - 1];
}

privado:
int findPeriod(const string &s) {
int n = s.size();
vector asignadoint título lps(n, 0);
por (int i = 1, len = 0; i) {
si (s[i] == s[len]) lps[i+] = ++len;
si (le) len = lps[len - 1];
ips[i+] = 0;
}
int period = n - lps[n - 1];
(n % period == 0) Período : n;
}
};
`` `

-...

## Blog Post – “Encode String with Shortest Long: The Good, the Bad, and the Ugly”

### 1. Introducción

Al entrevistarse para un papel de ingeniería **software**, usted inevitablemente tropezará con problemas de codificación de cadenas. Uno de los más populares es **LeetCode 471 – Encode String with Shortest Long**. Le pide que comprime una cadena en su representación más corta posible utilizando una simple sintaxis «k[encoded_string]».

¿Por qué este problema es un *must‐know*?

- Mezcla ** programación dinamica** con **procesamiento**.
- Esto revela cómo se trata de casos **edge** y **optimización**.
- Muestra su capacidad para producir **clean, código mantenible** en varios idiomas—exactamente lo que los reclutadores buscan en LinkedIn y GitHub.

Este artículo camina a través del problema **bueno** (lo que funciona bien), el **bad** (pocas comunes), y el **ugly** (casos importantes que viajan incluso programadores experimentados). Al final, tendrá una solución probada por la batalla lista para cualquier entrevista de codificación.

-...

### 2. El Bien: Lo que hace Este problema se puede resolver

Por qué ayuda a vivir
Silencio...
Silencio **Deterministic Output** Silencio Siempre necesitas la cadena codificada *shortest*. Sin azar. Silencio
Silencio **Tamaño de entrada pequeña** (`≤ 150`) Solución DP sin preocupaciones de tiempo. Silencio
Silencio **Fixed Syntax** (`k[... ]`) Silencio Sin ambigüedad; usted puede dividir o codificar de forma fiable. Silencio
Silencio **Contenimiento Autónomo** Silencio La cuerda es sólo letras minúsculas – ningún personaje especial para escapar. Silencio

Estas limitaciones hacen un *abajo DP* natural:

1. **Subproblema** – codifica una subestring `s[i.j]`.
2. **Transición** – dividir el subestring o comprimirlo si es una repetición.
3. **Base** – caracteres individuales ya están codificados.

Debido a que usted puede calcular cada subestring menor primero, la tabla DP se llena de pequeños a grandes subestrings. El algoritmo resultante es intuitivo y eficiente.

-...

### 3. The Bad: Common Pitfalls " Why It Fell Apart "

confidencialidad Pitfall Silencio Lo que pasa es que no se puede esperar
Silencio...
Silencio **Using `int` for count** Silencio Si codificas “aaaaa...(1000 veces)”, convirtiendo el recuento a una cadena incorrectamente (sobreflujo) Silencio Siempre convierte el *int* a una cadena (`String.valueOf(count)` o `to_string(count)`). Silencio
Silencio ** Comprobación de repetición ingenua** Silencio Revisar cada subestring contra todos los prefijos posibles conduce a `O(n4)` tención Utilice la función *prefix (KMP)* para encontrar el período mínimo en `O(n)`. Silencio
Silencio **Ignorando ya subestrings óptimas** Silencio Si una división da la misma longitud que la subestring cruda, puede sobreescribirlo innecesariamente TEN mantener la subestring *original* como un retroceso y sólo reemplazar cuando la nueva codificación es estrictamente más corta. Silencio
Silencio ** Index off‐by‐one** Silencio Las tablas DP a menudo usan `dp[i][j]` que significa `i` inclusive, `j` exclusiva; el desajuste conduce a fallos ← Escoge una convención (inclusive-inclusive o inclusive-exclusive) y se adhieren a ella en todo. Silencio
Silencio **Recursivo con la memoización pero faltando la regla de “no codificación”** Silencio Usted puede devolver una cadena comprimida que es *no más corta*, violando la declaración del problema ¦ Compare longitudes explícitamente; si `encoded.length() √= original.length()`, mantenga el original. Silencio

-...

### 4. The Ugly: Edge Cases That Can Trip You Up

1. **Very short strings* *
`s = "a" - debe regresar 'a'.
**¿Por qué?** Una solución DP puede intentar dividirse en partes vacías. Guardia contra `i == j`.

2. **Definir soluciones óptimas* *
"aaaaaaaaaaaaa" puede ser codificada como "10[a]" ", `"9[a]a" `, `"a9[a]".
¿Por qué? El DP sólo necesita *cualquier* más corto, pero su implementación podría devolver involuntariamente una cadena codificada más larga si la comparación no es estricta ( < < = > > > ).

3. **Large repetition counts**
"bababababab..." repetida 50 veces – el conteo se convierte en 50.
¿Por qué? Convertir el entero en una cadena puede tomar varios dígitos, haciendo la cadena codificada más tiempo que la subestring cruda. Compara siempre las longitudes completas.

4. **Codificación de objetos desnudos**
"aaaaaaaa" → "6[a]" es óptimo, pero "3[2]" es también 6 caracteres.
**¿Por qué?** El DP debe considerar los patrones anidados correctamente. La detección de periodos mínimos lo maneja automáticamente.

5. ** Longitudes no visibles**
"abcabras" no es una repetición completa.
**¿Por qué?** La detección de periodos debe devolver la longitud original; de lo contrario, podrías codificarla incorrectamente como `1[abcab]`.

-...

### 5. The DP Walk‐through

``text
dp[i][j] – menor codificación para s[i...j]
`` `

1. **Initialización**
dp[i] [i] = s[i] `

2. **Length loop** (`len` from 2 to n)

Por cada `i', set `j = i + len - 1'

*Empieza con la subestring* *
`dp[i][j] = s[i...j] `
♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪
`cand = dp[i][k] + dp[k+1][j] `
Si `cand` shorter → `dp[i][j] = cand `
- *Comproba la repetición*
`período = mínimoPeriod(s[i...j]) `
Si existe "período"
`cand = count + '[' + dp[i][i+perod-1] + ']
Reemplazar si es estrictamente más corto.

3. Resultado**: `dp[0][n-1]

El *período* se encuentra utilizando KMP en `O(len)`. Así, la complejidad general es `O(n3)` (longitud × splits) con un cheque adicional `O(n)` de repetición dentro de cada iteración.

-...

### 6. Lenguaje múltiple Mastery

Los clientes suelen preguntar: *“¿Cuál es tu idioma preferido para una entrevista de codificación?”*
Un candidato fuerte demuestra competencia al menos:

- **Java** (o Kotlin) - pila de empresas
*Python* – prototipado rápido, ciencia de datos
- **C+** – programación de sistemas, concursos de algoritmos

Las soluciones presentadas anteriormente son casi idénticas en todos los idiomas, destacando:

- **Reusabilidad** - la misma lógica, sólo cambios de sintaxis del lenguaje.
- **Readability** – nombres variables claros, índices de DP consistentes.
- **Modularidad** – funciones de ayuda para la detección del período KMP y la conversión de cadenas.

Cuando presente estas soluciones en GitHub o durante una entrevista, mostrará que puede *adapt* en lugar de *copy‐paste*.

-...

### 6. Lista de verificación para el retiro

- [ ] ** Caso básico**: " dp[i] = s [i] `
- [ ] **Siempre mantenga el subestring crudo** si no se encuentra nada más corto.
[ ] **Use KMP** (función de prefijo) para encontrar el período mínimo.
- [ ] **Comparar longitudes** después de generar un candidato codificado.
- [ ] **Evitar el flujo de entero** – convertir el recuento a cadena antes de comparar.
- [ ] **Test edge cases**: single char, nested patterns, high digit counts.

Ejecute su implementación contra los casos de prueba *de código duro* de LeetCode y unos pocos casos de borde *costo* para estar seguro.

-...

### 7. Palabras finales

LeetCode 471 es más que un rompecabezas divertido; es una prueba de Limus para tu pensamiento algoritmo. Maestro, y usted:

- Earn **Top Interviewer** insignias en plataformas como LeetCode.
- Tenga una solución **listo-para-pasar** para su próxima ronda de codificación.
- Los reclutadores de Impress buscan “programación dinamica + manipulación de cadenas” en LinkedIn.

Feliz codificación, y que su próxima entrevista sea como *short* y *optimal* como su codificación!

-...

### 8. Recursos relacionados

- [Dynamic Programming Primer](https://leetcode.com/discuss/interview-question/12620/DP-in-10-minutes)
- [KMP Algorithm Explained](https://www.geeksforgeeks.org/knuth-morris-pratt-algorithm/)
- [LeetCode 472 – Concatenated Words](https://leetcode.com/problems/concatenated-words/)
- [LeetCode 451 - Caracteres Clasicos By Frequency](https://leetcode.com/problems/sort-characters-by-frequency/)

-...

### 9. Call to Action

¿Tienes tu propia implementación? **Compartirlo en GitHub, etiquetarlo con `#leetcode471`, y avisar a la comunidad. ¿Quieres practicar más problemas de cuerda? **Únete a nuestro desafío de entrevistas de 30 días** y comienza con éste hoy!

-...

#### 10. Referencias

- Problema LeetCode 471
- Algoritmo KMP en GeeksforGeeks
- Programación dinámica – *Introducción a los algoritmos* (CLRS)

-...

■ *Recuerde: en entrevistas de codificación, **claridad** golpea * claridad*. The DP approach above is a testament to that. ¡Buena suerte! *

-...

## 6. Conclusión

Ahora tienes:

- Una solución comprobada ** en Java, Python y C++.
- Una hoja de ruta para evitar los obstáculos habituales.
- Una publicación **blog** que muestra su comprensión profunda – perfecta para Linked En o su cartera.

Cuando los reclutadores buscan la codificación de cadenas de programación dinamica, encontrarán su código, su versatilidad del lenguaje y su explicación de problema pulida. Eso es exactamente lo que hace un candidato *stand out*.

¡Feliz entrevista!

-...

*No dude en comentar, compartir o falsificar el código. ¡Mantengamos la conversación! *