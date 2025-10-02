-...
Título: LeetCode 115. -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1Ω⃣ LeetCode 115 – Distinct Subsequences
**Hard Silencio Dynamic Programming* *

Silencio Idioma Silencio Código Silencio
Silencio...
Silencio**
Silencio **Python** Silencio **
Silencio **C+** Silencio **solution.cpp**

■ Las tres soluciones se ejecutan en **O(n · m)** tiempo y uso **O(min(n, m))** memoria (la tabla 2-D es opcional – un array de rodamiento 1‐D se muestra en la implementación de Java).
■ La respuesta está garantizada para encajar en un entero firmado de 32 bits.

-...

### 1. Java – 1‐D DP (O(1) extra space)

``java
// Solution.java
Solución de la clase pública {}
*
* Cuentan subsecuencias distintas de la misma t.
* @param s cadena fuente
* @param t cadena de destino
* @return number of distinct subsequences
*/
public int numDistinct(String s, String t) {
int n = s.length(), m = t.length();

// Si t es más largo que s, imposible de formar t
si (m > n) retorno 0;

// dp[j] mantendrá el número de formas de formar t[0.j-1]
// del prefijo procesado de s
int[] dp = nuevo int[m + 1];
dp[0] = 1; // vacío t

para (int i = 1; i <= n; i++) { // iterate over s
char sc = s.charAt(i - 1);
// iterate backs so that dp[j-1] refers to the previous row
para (int j = m; j
(sc == t.charAt(j - 1)) {
dp[j] += dp[j - 1];
}
}
}
dp[m];
}

public static void main(String[] args) {
Solución sol = nueva solución ();
System.out.println(sol.numDistinct("rabbbit", "rabbit"); // 3
System.out.println(sol.numDistinct("babgbag", "bag")); // 5
}
}
`` `

¿Por qué funciona 1‐D? #
The transition `dp[j] = dp[j] + dp[j‐1] utiliza el valor de la fila anterior (`dp[j]` antes de la actualización) y el valor de la columna anterior (`dp[j‐1]`).
Al buclear `j` desde `m` hasta `1`, el valor de la “rengla anterior” sigue intacto cuando es necesario, por lo que un único array basta.

-...

### 2. Python – 1-D DP (compacto " legible)

``python
# Solución. py
Solución de clase:
def numDistinct(self, s: str, t: str) - Propiedad int:
n, m = len(s), len(t)
si m # Early exit
retorno 0

dp = [0] * (m + 1)
dp[0] = 1

para sc en s:
para j en rango(m, 0, -1):
si sc == t[j - 1]:
dp[j] += dp[j - 1]
retorno dp[m]

si __name_ == "__main__":
sol = Solución()
print(sol.numDistinct("rabbbit", "rabbit") # 3
print(sol.numDistinct("babgbag", "bag") # 5
`` `

Python 'range(m, 0, -1)` da un iterador inverso, manteniendo la lógica idéntica a Java.

-...

### 3. C++ – 1-D DP (fast & type-safe)

``cpp
// solution.cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int numDistinct(string s, string t) {}
int n = s.size(), m = t.size();
si (m > n) retorno 0;

vector implicado dp(m + 1, 0);
dp[0] = 1; // vacío t

para (char sc : s) {}
para (int j = m; j
si (sc == t[j - 1]) {
dp[j] += dp[j - 1];
}
}
}
dp[m];
}
};

int main() {}
ios::sync_with_stdio(false);
cin.tie(nullptr);

Sol de solución;
cout se realizó el sol.numDistinct("rabbbit", "rabbit")
cout se realizó el sol.numDistinct("babgbag", "bag")
retorno 0;
}
`` `

Los bucles de estilo aritmético y `range` mantienen el código mínimo.

-...

## 2VIEW⃣ Blog Article – “Cracking LeetCode 115: Distinct Subsequences – The Good, the Bad, and the Ugly”

■ *Audiencia de emergencia*
* Solicitantes de entrevistas de ingeniería de software*
* Programador que busca conocimiento sólido DP*
* Estudiantes que pulen su coding-interview toolkit*

■ **SEO Palabras clave:**
" Distinct Subsequences " , " Leetcode 115 " , `diseñación dinamica " , " entrevista de trabajo " , " Solución de Java " , " Solución de Palestina " , " Solución de problemas algorítmicos " , " , " , " , " , " , " , " , " , " , " , " , " , " , " , " , " , " , " , " , " , " , " , " , " , " , " , " , " , " , " , " , " , &

-...

# Cracking LeetCode 115: Distinct Subsequences – The Good, the Bad, and the Ugly

■ * Programación Dinámica (DP) × Manipulación de cuerdas*
■ *Por qué importa tu próxima entrevista de codificación*

-...

## 📌 ¿Qué es “Subsecuencias Distintas”?

En este clásico problema de LeetCode se le dan dos cuerdas:
* **`s`** - la cadena fuente,
* **`t`** - la cadena de destino.

Su tarea es contar **Cuantas formas distintas** puede eliminar caracteres de **`s`** para que la cadena restante sea igual **`t`**.
Cada posición en `s` puede ser utilizada** (si coincide con el carácter actual en `t ') o **pagado**. El orden de los personajes en `t` debe ser preservado, pero no necesitan ser contiguos en `s`.

-...

♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪

Vamos.

`dp[i][j]` = number of ways to form the first **`j`** characters of `t` using the first **`i`** characters of `s`.

Transición:

* If `s[i‐1] == t[j‐1]`:
dp[i][j] = dp[i‐1][j‐1] (Pick this char)
[j] (Esquítalo)
* Else:
dp[i][j] = dp[i‐1][j] (no puede elegir)

Casos de base:

Silencio `j == 0` Silencio → `dp[i] [0] = 1` (vacío `t` can always be formed by taking nothing)
Silencio `i == 0` Silencio → `dp[0][j] = 0` for `j ≥ 1` (non-empty `t` cannot be formed from an empty `s`) Silencio

Respuesta: ** " dp[n][m]** Donde " n " las vidas infligidas " y " m = удельных " .

-...

## 🧮 Complexity

TEN TERRITORIO TENIDO Tiempo ANTERIOR
Silencio--------------------------
Silencio 2‐D DP (completa mesa) Silencio **O(n · m)** Silencio **O(n · m)** Silencio
Silencio 1‐D roll array Silencio **O(n · m)** Silencio **O(min(n, m)** Silencio

■ En todos los casos, el algoritmo es lineal en el producto de longitudes de cadena y utiliza sólo enteros de 32 bits porque el problema garantiza la respuesta se ajusta en un `int` firmado.

-...

## 🚀 Why This Problem is a **Must‐Know** Interview Question

1. **String DP mastery** – Los entrevistadores a menudo preguntan variaciones: “Número de formas de formar una cadena de otro?” o “Copiar un sistema de archivos. ”
2. ** Optimización del espacio** – La solución 1‐D muestra un clásico truco DP (reverse iteration) que mantiene la memoria baja.
3. **Edge‐case awareness** – La salida temprana si `vivt intimidad √≠s vidas eterna` muestra una cuidadosa comprobación de límites, un traidor entrevistador busca.
4. **Agnosticismo lingüístico** – Usted puede ofrecer la solución en **Java, Python, o C++** – los tres idiomas se utilizan con frecuencia en entrevistas técnicas.

-...

## 🎯 Cómo utilizar estas soluciones en su entrevista

Silencio Qué hacer para mostrar
Silencio...
Silencio **Explicar la tabla DP** Silencio Show `dp[i][j]` y la recurrencia. Silencio
Silencio **Mostrar la optimización 1‐D** Silencio Explicar por qué iterar hacia atrás preserva los valores de la “rema anticipada”. Silencio
Silencio ** Análisis de tiempo-espacia** ¦ O notación y discutir por qué 32 bits encaja. Silencio
* Casos de borde de mención* *vigilantes cuerdas vacías, " más largo que " . Silencio
Silencio **Hablar sobre pruebas** Silencio Proporcionar pruebas de muestra (`rabbbit → conejo` y `babgbag → bag`). Silencio
Silencio **Opcional** Silencio Comparte una pequeña prueba de unidad o rutina de `mantener' para cada idioma. Silencio

-...

##  inaceptable The Good, The Bad, and The Ugly of the DP Approach

Silencio Silencio
Silencio------------Prince------
Silencio **Claridad** Silencio Transition `dp[j] += dp[j-1]` es intuitivo una vez que piensas en "pick" vs "skip." ← La mesa 2‐D parece limpia pero puede ocultar la optimización 1-D. TENIDO Olvidar al iterate `j` hacia atrás conduce a **wrong** respuestas—este error sutil es a menudo el culpable por fallar la prueba. Silencio
Silencio **Información** Silencio O(n · m) es óptimo; no hay sobrecarga cuadrática oculta. Silencio Ninguno – el algoritmo se ha demostrado óptimo para este problema. En idiomas con acceso lento a cadenas (por ejemplo, viejo C), es posible que necesite cache `s ' y `t` chars para evitar la indexación repetida. Silencio
Silencio ** Memoria** Silencio 1‐D utiliza **O(min(n, m))** memoria – ideal para las limitaciones de entrevista. TEN 2‐D es más fácil de leer pero duplica el uso de memoria. ← Utilizar enteros de 64 bits cuando no es necesario puede desperdiciar espacio; pero seguro si la respuesta puede exceder de 32 bits. Silencio
Silencio **Edge-cases** Silencio Empty `t` siempre rinde 1, vacío `s` rendimientos 0 para no vacío `t`. Silencio Salida temprana para `m не n` acelera casos triviales. tención Olvidar establecer `dp[0] = 1` conduce a cero conteos. Silencio
Silencio **Readability** Silencio Nombres variables `dp`, `sc` son claros; comentarios explican la dirección del bucle. El "range" de Python(m, 0, -1) ` esconde el bucle inverso. ← C+++ `vector fielint ` garantiza la seguridad tipo pero necesita `#parar los bits/stdc++.h] para la brevedad. Silencio

-...

## 📢 SEO‐Friendly Take-away

■ *Si está preparando una entrevista de ingeniería de software, “Distinct Subsequences” es un problema que casi seguro encontrará. Dominarlo demuestra su comprensión de programación dinámica, manipulación de cadenas y optimización espacial. Utilice los fragmentos Java, Python y C++ como referencia en su práctica, y recuerde resaltar la información algorítmica cuando se lo explica a los entrevistadores. *

-...

## 🔗 Más lectura

- [LeetCode 115 – Distinct Subsequences](https://leetcode.com/problems/distinct-subsequences/)
- [Programación Dinámica: de la teoría a la práctica] (https://www.geeksforgeeks.org/dynamic-programming/)
- [Preguntas de Interview You must Master for 2024](https://example.com/interview-prep-2024)

■ ¡Buena suerte en tu viaje de codificación!

-..