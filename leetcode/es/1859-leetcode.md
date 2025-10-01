-...
Título: LeetCode 1859. Clasificación de la Sentencia -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 1859 – “Sorting the Sentence”
**Easy TENIDO 1–9 palabras TENIDO O(n) time, O(n) space**

■ *Problema*
■ Una frase deslumbrada se forma mediante la colocación de la palabra 1-indexada a cada palabra y luego permutando las palabras.
■ Dada una frase súplica `s` (no hay espacios líderes/trailing, palabras separadas por un solo espacio), reconstruir la frase original.

■ *Ejemplo*
" `
■ Entrada: "is2 frase4 Este1 a3"
■ Producto: "Esta es una frase"
" `

■ **¿Por qué es una gran pregunta de entrevista? #
* Lógica de paración sencilla
* Manipulación e indexación de cadenas
* No es necesario contar con estructuras de datos avanzadas

-...

## 📄 Solution Overview

1. **Split** la cuerda en palabras (O(n) caracteres).
2. Para cada palabra, **extract** el último personaje → la posición (1-basada).
3. **Place** la palabra (sin el dígito) en un array en `index‐1`.
4. **Entrar** el array de nuevo en una frase.

■ La restricción `1 ≤ wordCount ≤ 9` garantiza que el último personaje es siempre un dígito único.
■ Si el problema permitía más palabras, tendríamos que analizar todos los dígitos que siguen.

-...

## 🧪 Code Implementations

■ Todas las implementaciones tienen lógica idéntica; sólo la sintaxis difiere.

### 1. Java

``java
// Java 17
importar java.util*;

Solución de la clase pública {}
public String sortSentence(String s) {
Criar[] palabras = s.split(");
String[] res = nuevo String[words.length];

para (String w : palabras) {
int pos = w.charAt(w.length() - 1) - '1'; // 0 basado
res[pos] = w.substring(0, w.length() - 1);
}

volver String.join(" ", res);
}
}
`` `

■ *La complejidad*
■ *Time* – O(n) (cada palabra visitada una vez)
■ *Pace* – O(n) (result array)

-...

### 2. Pitón

``python
# Python 3
Solución de clase:
def sortSentence(self, s: str) - Propiedad str:
palabras = s.split()
res = [None] * len(words)

para w en palabras:
pos = int(w[-1]) - 1 # 0-based index
re[pos] = w[:-1]

volver '.join(res)
`` `

■ **La complejidad** - igual que Java

-...

### 3. C++

``cpp
// C+17
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
string sortSentence(string s) {
vectoriales palabras;
stringstream ss(s);
hilo w;
mientras que (ss.

vector seleccionado(words.size());
for (const string &w : words) {}
int pos = w.back() - '1'; // 0‐based
[pos] = w.substr(0, w.size() - 1);
}
Ans de cuerda;
para (size_t i = 0; i) ++i) {
si (i) ans += '
ans += res[i];
}
devolver los ans;
}
};
`` `

■ **La complejidad** – O(n) tiempo, O(n) espacio

-...

## 🚀 Cómo utilizar estas soluciones en su entrevista

1. **Explica el algoritmo** antes de bucear en código.
2. Mencione la complejidad **tiempo/espacio** y por qué son óptimos.
3. Destaca que el truco es tratar el último dígito como un índice.
4. Prepárate para discutir casos de borde (por ejemplo, frases de una sola palabra, caso mixto, etc.).

-...

## 🧩 El Bien, el Mal, y el Ugly

¿Qué es lo mejor de la vida?
Silencio--------------------------------------------...
Silencio **Bien** Silencio • O(n) tiempo " espacio, no estructuras de datos pesadas. Funciona para cualquier alfabeto (abajo/abajo).
Silencio **Bad** Silencio • Ninguno. El problema es deliberadamente fácil de superficializar las habilidades básicas de cuerda. Silencio **Mis‐parsing the digit** – olvidando convertir `char` a `int`.
Silencio **Ugly** Silencio – Silencio • Si el problema se extendió a **10+ palabras** ( posiciones multi dígitos), la lógica actual fallaría. • Necesita una rutina de persing más robusta que extrae todos los dígitos de rastreo, no sólo el último char. En el mundo real, las frases pueden contener punción o números en palabras, requiriendo una solución de regex más limpia. Silencio

-...

## 📚 Bonus: Extending to Variable‐Length Indices

Si la frase podría tener **10+ palabras**, el índice puede consistir en varios dígitos. He aquí una rápida adaptación para Python:

``python
import re

def sort_sentence_variable(s):
palabras = s.split()
res = [None] * len(words)
para w en palabras:
m = investigación(r'(\d+)$', w)
pos = int(m.group(1)) - 1
[pos] = w[:m.start()]
volver '.join(res)
`` `

Esto utiliza un regex para capturar todos los dígitos que siguen.

-...

## 🎯 SEO‐Optimized Blog Title & Meta Descripción

*Título*
■ *Sorting the Sentence (LeetCode 1859) – Java, Python, " C++ Soluciones + consejos de entrevista*

**Meta Descripción:**
■ El problema de Master LeetCode “Sorting the Sentence” con código Java, Python y C++. Aprende el algoritmo óptimo, el análisis de complejidad y la explicación de entrevista. Perfecto para la preparación de la entrevista de codificación.

-...

## 📈 Wrap‐Up

Clasificar la Sentencia es un clásico rompecabezas de entrevista de “estring manipulación + indexación”. La solución óptima es trivial cuando te das cuenta de que el último dígito es una posición explícita basada en 1.
Las implementaciones en Java, Python y C++ son concisas, eficientes y listas para entrar en su sesión de LeetCode o entrevista de codificación.

¡Feliz codificación, y que sus oraciones estén siempre en orden! 🚀