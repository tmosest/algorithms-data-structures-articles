-...
Título: LeetCode 809. Palabras expresivas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 809. Palabras expresivas – Solución Full‐Stack (Java / Python / C++)

A continuación encontrará una aplicación limpia y completa para **Java**, **Python**, y **C+**.
Los tres resuelven el mismo problema de LeetCode:

■ Dada una cuerda `s` y una serie de palabras de consulta, devuelve cuántas de esas palabras pueden ser estiradas en `s` ampliando repetidamente cualquier grupo de letras idénticas a ** longitud ≥ 3**.

La solución utiliza una técnica clásica de dos puntos que se ejecuta en **O(las vidas eternas + Уковоковывываковывывывывакованых)** tiempo y **O(1)** espacio extra.

-...

## Java

``java
// 809. Palabras expresivas
// Hora : O(Las vidas eternas + NOVSOPERÓVIO)
// Espacio: O(1)
Solución de la clase pública {}
public int expressive Palabras (String s, String[] words) {
int result = 0;
para (String w : palabras) {
si (estretchable(s, w)) resultado++;
}
Resultado de retorno;
}

booleano privado isStretchable(String s, String w) {
// Si w es más largo que s nunca puede coincidir
si (w.length()

int i = 0, j = 0; // i → s, j → w
mientras (i י s.length() < t > {}
si (s.charAt(i) != w.charAt(j)) devuelve falso;

char cur = s.charAt(i);

// Cuenta la longitud de ejecución en s
int sCount = 0;
mientras (i) == cur) {
sCount++; i++;
}

// Cuenta la longitud de ejecución en w
int wCount = 0;
mientras (j) == cur) {
wCount++; j++;
}

// w de ejecución no debe exceder la carrera
si (wCount > sCount) devuelve falso;

// Si la carrera es pequeña en s, debe coincidir exactamente
si (sCount) 3 ' sCount != wCount) vuelven falso;
}

// Ambas cuerdas deben consumirse completamente
devolver i == s.length() ' j == w.length();
}
}
`` `

-...

## Python

``python
# 809. Palabras expresivas
# Tiempo: O(len(s) + suma(len(w) para w en palabras))
# Espacio: O(1)

Solución de clase:
def expressive Palabras(self, s: str, words: list[str]) - int:
volver suma(self._stretchable(s, w) para w en palabras)

def _stretchable(self, s: str, w: str) Bool:
si len(w) > len(s)
Retorno Falso

I = j = 0
mientras que yo hice el len(s) y j
si s[i] w[j]:
Retorno Falso

ch = s[i]
s_cnt = 0
mientras que yo hice el len(s) y s [i] == ch:
s_cnt += 1
i += 1

w_cnt = 0
j) Len(w) y w[j] == ch:
w_cnt += 1
j += 1

si w_cnt > s_cnt: # w tiene más letras en este grupo
Retorno Falso
si s_cnt 3 y s_cnt!= w_cnt: # no se puede estirar un grupo corto
Retorno Falso

devolver i == len(s) y j == len(w)
`` `

-...

### C++

``cpp
// 809. Palabras expresivas
// Hora : O(Las vidas eternas + NOVSOPERÓVIO)
// Espacio: O(1)

Clase Solución {
public:
int expressive Words(string s, vector asignado > palabras) {}
int ans = 0;
para (auto &w : palabras)
si (es posible(s, w)) ++ans;
devolver los ans;
}

privado:
bool isStretchable(cont string &s, const string &w) {
si (w.size() > s.size()) devolver falso;

size_t i = 0, j = 0; // i - título s, j - título w
mientras (i) {}
si (s[i] != w[j]) devuelve falso;

char cur = s[i];
size_t sCnt = 0;
mientras (i)
++sCnt; ++i;
}

size_t wCnt = 0;
mientras (j.)
++w Cnt; ++j;
}

si (wCnt > sCnt) devuelve falso; // w más tiempo que s
si (sCnt ecto 3 " prófugo != wCnt) devuelve falso; // no puede estirar
}
devolver i == s.size() " j == w.size();
}
};
`` `

-...

Artículo del Blog – “Las palabras expresivas: lo bueno, lo malo y lo malo”

■ **SEO Palabras clave**: *Expressive Words Leetcode, solución Leetcode 809, entrevista de algoritmo de Java Python C++, cómo resolver palabras expresivas, algoritmo de entrevista de trabajo, problema de palabras estirables, preguntas de entrevista de algoritmo*

-...

Introducción

Si está preparando una entrevista de ingeniería de software, encontrará rápidamente **LeetCode 809 – Expressive Words**. Es engañosamente simple pero a menudo viaja a candidatos porque mezcla la manipulación de cuerdas con una regla de “stretch” que es fácil de malinterpretar.

En este artículo, vamos a romper los aspectos **bueno**, **bad**, y **engrandecido** del problema, caminar a través de una solución robusta en **Java**, **Python**, y **C+**, y resaltar los retiros de entrevistas.

■ *¿Por qué el título? *
■ “Bien, el Mal y el Ugly” es una referencia clásica de *El Padrino*. Señala que estamos buceando profundamente en lo que *trabaja*, qué *fails*, y qué *es fácil de equivocarnos*.

-...

### 2 comentarios sobre el problema Recap (bien)

Se te da:
- Una cuerda 's' (la cuerda de "stretchy").
- Una serie de palabras de consulta de candidatos.

Una operación **stretch** es:
1. Escoge un grupo de personajes idénticos en una palabra.
2. Añadir copias extra de ese personaje para que la longitud del grupo sea **≥ 3**.

El objetivo: Contar cuántas palabras en palabras [] se puede estirar en `s`.

¿Por qué es esto?
- **Clear constraints**: `1 ≤ s.length, words.length ≤ 100`. Así que un escaneo lineal está bien.
- **Determinista**: Sin azar ni retroceder; el enfoque codicioso funciona.

-...

#### 3down⃣ Donde el problema se encuentra

1. **Misreading the stretch rule**
Usted *no puede* estirar un grupo en `s` que ya es más pequeño que 3. Sólo grupos **≥ 3** pueden ser el objetivo de estiramiento.
*Pedazo común*: Pensando que puedes encoger el grupo de `s` para que coincida con `w`, que es falso.

2. **Off‐by-one bugs in run‐length counting**
Contando letras idénticas contiguas, olvidando aumentar ambos punteros conduce a bucles infinitos o cheques mal alineados.

3. *Desajuste por caso*
- `s` es más corto que `w`.
- `s` contiene grupos adicionales que `w` no tiene.
- `w` tiene un grupo más largo que el grupo equivalente ' s.

La parte “mala” es que una sola regla fuera por uno o malentendido puede matar su solución.

-...

#### 4down⃣ The Classic Two‐Pointer Fix (Ugly → Beautiful)

La solución “ugly” (complicada) a menudo implica bucles anidados, mapas de frecuencia de construcción, o realizar múltiples pases. La forma más limpia es el enfoque **2 puntos, carrera-length**:

1. Traverse `s` y `w` simultáneamente.
2. Cuando los caracteres actuales coinciden, cuenta cuántas veces cada uno aparece consecutivamente (longitudes de funcionamiento).
3. Aplicar las reglas del estiramiento:
- La longitud de ejecución no puede exceder la longitud de la carrera.
- Si la longitud de ejecución es ** 3**, debe igualar la longitud de ejecución exactamente.
4. Si ocurre un desajuste, aborte.

La belleza se encuentra en **O(1)** memoria extra y un solo paso sobre cada palabra.

-...

#### 5down⃣ Code Walk‐through (Java)

``java
Solución de la clase pública {}
public int expressive Palabras (String s, String[] words) {
int cnt = 0;
for (String w : words) if (isStretchable(s, w)) cnt++;
cnt de retorno;
}

booleano privado isStretchable(String s, String w) {
si (w.length()
int i = 0, j = 0;
mientras (i י s.length() < t > {}
si (s.charAt(i) != w.charAt(j)) devuelve falso;
char cur = s.charAt(i);
int sCnt = 0, wCnt = 0;
(i) == cur) { sCnt++; i+; }
mientras (j.) == cur) { wCnt++; j++; }
si (wCnt > sCnt) devuelve falso;
si (sCnt ecto 3 " prófugo != wCnt) devuelve falso;
}
devolver i == s.length() ' j == w.length();
}
}
`` `

■ **Por qué esto es “bueno”* *
■ *Clear variables*, *single exit points*, *no magic numbers*.

-...

Python & C++ – Comparaciones rápidas

- **Python**: Usa los bucles y 'len()' para los límites.
- **C++**: Utiliza el tamaño de los índices, el anillo y el título " .

Todos comparten el mismo flujo lógico, por lo que es fácil traducir entre idiomas.

-...

### 7ف⃣ Complexity Analysis

Silencio Silencio Silencio Silencio
Silencio----------------
Silencioso `expresivoWords` Silencio **O( sobre la vida eterna + Åmorw intimidad)** Silencio **O(1)** Silencio
TENIENDO ` isStretchable` Silencio **O(las vidas eternas +  sometidaw sometida)** Silencio **O(1)** Silencio

Con los límites dados (≤ 100 caracteres), el rendimiento es trivial, pero el algoritmo escala linealmente si las cuerdas crecen.

-...

#### 8down⃣ Qué mostrar en su resumen

- **Problema**: LeetCode 809 – Palabras expresivas
- **Skills**: Manipulación de cuerdas, codificación de longitud, algoritmos codiciosos, técnica de dos puntos
- ** Idiomas**: Java, Python, C++
** Resultado**: Solución limpia, O(n) con cobertura completa de pruebas

Mention that you **avoided** the common pitfalls of off-by‐one errors and misinterpreting stretch conditions, demonstrating attention to detail – a key interview trait.

-...

#### 9down⃣ Testing Checklist

Silencio Test confidencialidad Descripción
Silencio...
Silencioso `s = "heeellooo", palabras = ["hello", "hi", "helo"] TENIDA Producción esperada: 1 TEN
Silencioso `s = "zzzzzyyyyyyy", palabras = "zzyy", "zy", "zyy"] TENIDA Salida esperada: 3 TEN
Silencio `s = "abcd", palabras = ["abc", "abcd", "ab"] Silencio Todos los retornos 0
Silencio `s = "aaabbcc", palabras = ["aabbcc", "aaabbccc"] ← Stretch no se permite en grupos
Silencioso `s = "aaa", palabras = "aaa"] Silencio Debe devolver 0 (grupo demasiado corto) Silencio

Agregue los casos de borde para grupos de letras individuales, arrays vacíos y cadenas de longitud máxima.

-...

## ## 10VIEW⃣ Final Takeaway (El Ugly se convierte en hermoso)

■ **“Si estás atascado, recuerda que el problema es esencialmente una comparación de longitud. El método de dos puntos elimina la complejidad y protege contra errores sutiles.”* *

Durante las entrevistas, el entrevistador le pedirá que explique la regla “≥ 3”. Cuando se puede articular con claridad y presentar la solución de dos puntos, no sólo resolverá el problema sino que también mostrará ** elegancia algorítmica**.

-...

Conclusión

LeetCode 809 es más que un rompecabezas de cuerdas, es un **test de precisión**. Al dominar el enfoque de dos puntos en **Java, Python, y C++**, estás listo para impresionar a los gerentes de contratación y demostrar la mentalidad de **interview-ready** que buscan.

¡Feliz codificación, y buena suerte aterrizando esa próxima entrevista de trabajo! 🚀

-...

*End of article. *

-...

■ *Sea libre para retocar el “Testing Checklist” y añadir más persianas. La clave es demostrar minuciosidad, claridad y un algoritmo pulido. *