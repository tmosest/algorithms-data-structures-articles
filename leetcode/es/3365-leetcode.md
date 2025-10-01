-...
Título: LeetCode 3365. Rearrange K Substrings to Form Target String -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 3365 – Rearrange K Substrings to Form Target String
## Java, Python & C+ Solutions + In‐Depth Blog Post

■ **TL;DR** –
■ *El problema pregunta si dos cadenas de anagrama pueden dividirse en piezas de `k ' de igual longitud y luego las piezas de `s` reordenadas para formar `t`. *
*A single `O(n)` pasar con un mapa de hash es suficiente: simplemente contar las piezas de `s`, luego consumirlas de `t`. *

A continuación encontrará:

Silencio Idioma Silencio Archivo Silencio
Silencio...
Silencio **Java** Silencioso `Solution.java` Silencioso |[Link](#java)
Silencio **Python** Silencio `solution.py` Silencio 🗎[Link](#python) Silencio
Silencio **C+** Silencio `solution.cpp` Silencio |[Link](#cpp)

Después de eso, un artículo completo de SEO-friendly blog que explica el algoritmo, recorre el “bueno, malo, feo”, y ofrece ideas de estilo de entrevista.

-...

## 🚀 Java Solution

``java
// Solution.java
importa java.util. HashMap;
importa java.util. Mapa;

Solución de la clase pública {}
booleano público es posibleRearrange(String s, String t, int k) {
int n = s.length(); // n == t.length()
int blockSize = n / k; // Garantizado para ser entero

// Cuenta cada k‐block de s
Mapa seleccionadoString, Integer frecuentementeq = nuevo HashMap Quería();
para (int i = 0; i < n; i += blockSize) {
Bloque de cuerda = s.substring(i, i + blockSize);
freq.merge(block, 1, Integer::sum);
}

// Abrazaderas de t
para (int i = 0; i < n; i += blockSize) {
Bloque de cuerda = t.substring(i, i + blockSize);
Integer count = freq.get(block);
si (cuenta == null 0) devolver falso;
freq.put(block, count - 1);
}
retorno verdadero;
}
}
`` `

■ **Por qué funciona* *
* `k` se fija, por lo que cada longitud de bloque es `n/k`.
* Porque `s` y `t` son anagramas, cada bloque que aparece en `t` debe aparecer también en `s`.
* El mapa del hash garantiza la búsqueda `O(1)` de cada bloque.

-...

## 🐍 Python Solution

``python
# Solución. py
def isPossibleToRearrange(s: str, t: str, k: int) Bool:
n = len(s)
bloque = n // k

freq = {}
# Contando bloques de s
para i en rango(0, n, bloque):
sub = s[i:i+block]
freq[sub] = freq.get(sub, 0) + 1

# Consume bloques de t
para i en rango(0, n, bloque):
sub = t[i:i+block]
si freq.get(sub, 0) == 0:
Retorno Falso
freq[sub] -= 1

Retorno
`` `

* Notas específicas*
* Slicing crea una nueva cuerda, pero la cabeza es insignificante para `n ≤ 2·10^5`.
* `dict.get` is `O(1)` average.

-...

## 🧩 C+ Solución

``cpp
// solution.cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
bool isPossibleToRearrange(string s, string t, int k) {
int n = s.size(); // n == t.size()
bloque de entrada = n / k; // tamaño de bloque

unordered_map detectstring, int confianza freq;

// Cuenta subestrings of s
para (int i = 0; i)
cadena sub = s.substr(i, block);
++freq[sub];
}

// Subestrings de consumo de t
para (int i = 0; i)
cadena sub = t.substr(i, block);
auto = freq.find(sub);
if (it == freq.end() TENIDO SUPERVISIÓN 0) devolver falso;
-it-jósegundo;
}
retorno verdadero;
}
};
`` `

■ **C++ notas específicas**
* " noordered_map " da operaciones medias " O(1) " .
* `substr` copia el substring, pero la longitud es en la mayoría `n/k ≤ n`.
* No se requiere gestión manual de memoria.

-...

## 📚 Blog Article – “The Good, the Bad, and the Ugly of LeetCode 3365”

■ **Keywords**: LeetCode 3365, Rearrange K Substrings, problema de codificación de entrevistas, pensamiento algoritmo, Solución Java, solución Python, solución C++, entrevista de trabajo, entrevista de codificación, estructuras de datos, mapa de hash, partición de subestring, anagramas.

-...

### 1. Introducción

Cuando se está preparando para una entrevista de ingeniería de software, problema LeetCode **3365 – Rearrange K Substrings to Form Target String** es una pregunta *gold‐mine*.
Prueba:

- ** Razones de anagrama** - las cuerdas están garantizadas para ser anagramas.
- **String partición** - debe dividir una cadena en pedazos iguales.
- ** Hash‐map contando** – seguimiento eficiente de frecuencia de bloques.
- **Edge-case vigilance** – cuidado con fuera-por-ones, copias de subestring y grandes tamaños de entrada.

A continuación caminamos a través de la declaración del problema, analizamos el algoritmo, discuten los pros, los contras y las trampas, y terminamos con ideas de estilo entrevista.

-...

### 2. Reposición de problemas

■ *Given*
* Dos cuerdas `s` y `t`, ambas de longitud `n` (≤ 2·105) y **anagramas** unos de otros.
* An integer `k ' such that `n` is divisible by `k`.
■ **Pregunta**
■ ¿Puedes dividir `s` en 'k' subestrings contiguos de igual longitud, reorganizar esas subestrings arbitrariamente, y concatenarlas para obtener exactamente 't'?

Si sí → devolver `true`, otra → `false`.

-...

### 3. Naïve Approaches " Their Flaws

TENIDO Enfoque TENIDO Complejidad del tiempo TENIDO Complejidad del espacio
Silencio----------------------------------
Silencio Generar todas las permutaciones de las subestrings " k " y comparar Silencio `O(k! * n)` Silencio `O(k)` Silencio `k` puede ser hasta `n ' (el peor caso 200k) - imposible. Silencio
Silencio Revise cada posición de `t` contra cada subestring posible de `s` Silencio `O(n^2)` Silencio `O(1)` Silencio Demasiado lento para 200k. Silencio
Silencio Utilice una ventana corredera para cada bloque en `t` Silencio `O(n * k)` Silencio `O(n/k)` Silencio Todavía cuadrático cuando `k` es pequeño. Silencio

Por lo tanto, necesitamos una solución *linear*.

-...

### 4. La solución óptima – Mapa de frecuencia de bloques

###### 4.1 Observation

Porque `s` y `t` son anagramas, cada personaje en `t` existe en algún lugar en `s`.
Si dividimos ambas cadenas en bloques de longitud `len = n/k`, el problema se reduce a:

■ * ¿Se puede reorganizar el multiconjunto de bloques " k " de `s ' a igual que el multiconjunto de `k ' bloques de `t ' ? *

Así que la solución se reduce a comparar dos conjuntos de cuerdas.

#### 4.2 Algoritmo (One‐Pass Hash Map)

1. ** Longitud del bloque completo** `len = n / k`.
2. **Los bloques de `s`**:
- Por cada `i = 0 ... n-1` paso `len`, tomar subestring `s[i ... i+len)` y aumentar su cuenta en un mapa de hash.
3. **Consumo de bloques de `t`**:
- Por cada `i = 0 ... n-1' paso `len`, tomar subestring `t[i ... i+len)`.
- Si el bloque está perdido o su cuenta es cero → devolver `false`.
- De lo contrario, decremento su cuenta.
4. **Todos los bloques coinciden** → devolver `verdad ' .

**Las complejidades* *

Silencio Silencio Silencio Silencio
Silencio----------------
Subestrings → `O(n)` total Silencio `O(k)` bloques distintos Silencio
Silencio Mapa consumado Silencio `O(k)` Silencio `O(k)` Silencio
Silencioso **Overall** Silencio

Debido a que `k ≤ n`, la solución es lineal en la longitud de la cuerda y utiliza espacio extra constante relativo a `k`.

##### 4.3 Edge‐ Manejo de caso

Silencio Qué hacer para cuidar de Silencio
Silencio...
Silencio **`k == 1`** Silencio Entire string as one block tención Map will have one entry; algoritmo works unchanged. Silencio
Silencio **`k == n`** Silencio Cada personaje es un bloque tención Mapa contiene `n` entradas; todavía `O(n)` operaciones. Silencio
Silencio **Large `k`** Silencio Las copias de Substring pueden ser caras ← Use `String#substring` in Java (O(1) reference in modern JDK) or `substr` in C++/Python; still fine for 200k. Silencio
Silencio ** Longitud de bloque muy pequeña (1)** tención Mapa de búsquedas frecuentes tención Still O(1) per lookup; fine. Silencio
Silencio ** cuerda vacía** Silenciosas restricciones de problemas prohíben la vida No es necesario. Silencio

-...

### 5. El Bien, el Mal, y el Ugly

##### El Bien
- Simplicidad... El algoritmo es one‐pass y utiliza sólo un mapa de hash.
- **Tiempo de trabajo** – Maneja el tamaño máximo de entrada cómodamente.
- **Determinista** - Sin retroceso ni soplo exponencial.
- **Language‐agnostic** - Obras en Java, Python, C++, Vamos, etc.

##### El malo
- **Substring Overhead** – Cada bloque es una nueva cadena (Java) o copia (C++/Python).
- **Colisión Hash‐Map** – Mientras que la búsqueda promedio O(1), los insumos patológicos (por ejemplo, muchos bloques idénticos) pueden causar degradación del rendimiento en algunos idiomas si se utiliza una función de hash deficiente.
- ** Usage de memoria** – El peor caso `k == n` conduce a `n` teclas distintas, que es todavía `O(n)` pero puede utilizar la memoria significativa en un entorno de entrevista ajustada.

##### El Ugly
- **Misreading the Problem** – Algunos candidatos piensan incorrectamente que necesitan *reordenar los caracteres dentro de bloques*, lo que es incorrecto. Los bloques deben permanecer intactos.
- **Off‐by-One Bugs** – Olvidar que la subestring toma la exclusiva del índice final puede causar fuera de límites.
- **Asumiendo que la 'subestring' de Java es O(n)** – En los JDK más viejos `substring` crea una copia, lo que lleva a `O(n2)` en el peor de los casos. Los JDK modernos mitigan esto, pero un enfoque seguro es utilizar `StringBuilder` si estás en un entorno donde no puedes confiar en esa garantía.

-...

### 6. Consejos para entrevistas

1. **Explicar el Anagram Constraint** – Mostrar que usted entiende que garantiza el multiconjunto total de partidos de personajes, eliminando algunas posibilidades.
2. **Preguntas de aclaración**
- ¿Está garantizado dividir 'n'? ”
- ¿Puede ser igual a 'n'? ”
- ¿Las cuerdas sólo contienen caracteres ASCII? ”
Esto demuestra atención al detalle.
3. **Tiempo-Space Trade‐Off** – Si el entrevistador pide *constant extra space*, puede notar que `k` puede ser hasta `n`, por lo que `O(k)` es inevitable a menos que utilice un algoritmo multi-pass que reutiliza la misma memoria.
4. **Testing** – Camine a través de ejemplos manualmente:
- `s = "abab" ' , `t = "bababa" ' , `k = 2` → bloques `[ab", "ab" vs `ba, "ba" → `false`.
- `s = "abcabc", `t = "bcaabc" `, `k = 3` → bloques `["abc", "abc"]` vs `[bca", "abc"] → `false`.
- `s = "abcd" ' , `t = "abcd" ' , `k = 2` → bloques `["ab, "cd"]` vs `[ab, "cd] → 'verdad'.
Mostrar las actualizaciones del mapa para cada paso.

5. ** Estructuras de datos alternativos** – Si el entrevistador pregunta, puede discutir el uso de un *multiset* (`Counter` en Python) o un * mapa surtido* si desea garantizar el orden determinista (útil cuando necesita salir del orden reordenado).

-...

### 6.1 ¿Qué pasa si” preguntas de seguimiento

¿Y si los anagramas no eran? *
**A**: Tendría que comprobar si el personaje cuenta en 's' coinciden con los de 't' antes de proceder. El mapa de frecuencia de bloques todavía sería válido, pero primero verificaría la propiedad de anagrama global.

- **Q**: *¿Podemos recuperar la permutación exacta de bloques que produce `t`? *
Sí. Mientras consumes `t`, almacena las cadenas de bloques en una lista y póngalos en el orden del consumo. El algoritmo en sí mismo ya le da la permutación.

- **Q**: *¿Cómo adaptar esta solución a un escenario de streaming en el que `s` llega por pieza? *
**A**: Actualiza el mapa de hash a medida que llegan nuevos bloques. Para `t`, todavía necesita amortiguar al menos caracteres 'blockSize' para formar un bloque.

-...

### 7. Conclusiones

LeetCode 3365 es engañosamente sencillo pero lleno de temas clásicos de entrevista:

- Razonamiento de Anagrama → asegura que el problema es solvable con la cuenta.
- Partición → te obliga a pensar en los límites de bloque, no sólo frecuencias de carácter.
- Frecuencia Hash‐map → la herramienta go‐to para comparación multiset.

Al dominar este problema, fortalecerá su *algoritmic toolbox* e impresionará a los entrevistadores con una solución limpia y lineal que escala a los límites superiores del problema.

-...

### 8. Final Interview Takeaway

■ **Recuerdan**:
■ 1. Siempre busque restricciones ocultas (anagrama, divisibilidad).
■ 2. Reducir el problema a una comparación *multiset* cada vez que vea “rearrange” o “permute”.
■ 3. Objetivo para `O(n)` a menos que pueda demostrar que el límite inferior óptimo es peor.

Si usted puede articular lo anterior en una discusión de 10 minutos, usted demostrará la habilidad principal de entrevista: *convertir las declaraciones de problemas en algoritmos concisos, provablemente eficientes. *

-...

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀

-...



-...

■ **Disfrutado del artículo? #
■ *Compártelo en LinkedIn o Twitter. Etiqueta a un amigo que se está preparando para una entrevista y vamos a conseguir que funcionen juntos! *

-...



-...

**End of Document* *


-...

> **Cómo ejecutar las soluciones* *
■ *Java* → `javac Solution.java ' pláva Solution` (con un arnés de prueba personalizado).
■ *Python* → `piathon3 solution.py` (con un arnés de prueba).
■ *C++* → `g++ -std=c+17 solution.cpp -O2 " ./a.out ' (con un arnés de prueba).

¡Feliz codificación y buena suerte en tu búsqueda de trabajo! 