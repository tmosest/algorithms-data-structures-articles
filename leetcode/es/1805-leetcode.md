-...
Título: LeetCode 1805. Número de enteros diferentes en una cuerda -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 1805 – “Número de diferentes enteros en una cuerda”

■ ** Objetivo** – Dado una cadena mixta de letras minúsculas y dígitos, sustitúyase cada no dígitos por un espacio, divida la cadena en fichas enteros, tira de ceros líderes, y cuenta cuántos enteros *unique* existen.
■ **Escenario de entrevistas Típicas** – Una pregunta de “estring-parsing” que prueba el uso regular de la expresión, establece semántica y el manejo del borde.
■ *Por qué importan los reclutadores* Te obliga a pensar en **time-space trade‐offs**, el manejo de grandes enteros, y el estilo de código limpio – todos los traidores reclutadores buscan en un backend / ingeniero de personal completo.

A continuación encontrará una solución totalmente adaptada para la producción en **Java, Python y C+** (C++17).
Después del código, te daré una entrada de blog amigable de SEO que habla sobre los aspectos *bueno*, *bad* y *muy* de este problema y por qué dominarlo puede ayudarte a conseguir tu próximo trabajo.

-...

## 📚 Problema Resumen

`` `
Entrada: palabra – una cadena (1 ≤ tenciónword ≤ 1000) consistente en [0‐9] y [a‐z]
Producto: El número de enteros distintos después de la eliminación de no dígitos
y descartando los ceros principales.
`` `

*Ejemplo*

`` `
palabra = "a123bc34d8ef34" → fichas: 123, 34, 8, 34
enteros distintos: {123, 34, 8} → respuesta = 3
`` `

* Casos generales*

* “0000” → entero 0
* “01” y “1” son los mismos
* enteros muy largos que no encajan en tipos de 64 bits

-...

##  Settlement High-level Approach

1. **Escoja la cuerda una vez** – mantenga un puntero.
2. Cuando veas un dígito, acumula todos los dígitos consecutivos en un `StringBuilder` (o `string`).
3. Tira de ceros líderes (`replaceFirst("^0+", "").
4. Si la cadena resultante está vacía → el entero es `0`.
5. Almacene la forma canónica en un `HashSet` / `unordered_set` / `set`.
6. Devuelve el tamaño del set.

*Por qué funciona*:
* Cada número se procesa en tiempo O(duración).
* Los ceros desnudistas garantizan la forma canónica; por ejemplo, “001” → “1”.
* Utilizar un conjunto garantiza la singularidad en O(1) amortizado (basado en jash) o O(log n) (basado en árbol).

-...

Análisis de la Complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
Escaneando `palabra ' Silencio **O(n)** (n = tenciónword
Silencio Añadiendo a establecer Silencio **O(1)** amortizado (Java/C++ unordered_set) Silencio **O(k)** (k = número de enteros distintos)
Silencio general **O(n)** Silencio**

`n` ≤ 1000, por lo que el algoritmo está fácilmente dentro de los límites.

-...

## 🧑 💻 Code Solutions

■ **Tip** – Use a `BigInteger` (Java), `int` (Python’s arbitrary‐precision `int`), or `__int128`/`std::string` in C++ cuando el número puede ser de 64-bit.
■ El código a continuación se adhiere a la biblioteca estándar solamente (sin libs de terceros).

### 1. Java (Java 17)

``java
importa java.math. BigInteger;
importa java.util. HashSet;
importa java.util. Set;

Solución de la clase pública {}
public int numDifferentIntegers(String word) {
Establecer contactoString] visto = nuevo HashSet correctamente(); // store canonical string representation
int i = 0;
int n = word.length();

mientras (i
// skip non-digits
si (!Character.isDigit(word.charAt(i)))) {}
i++;
continuar;
}

// acumular dígitos
int start = i;
(i)) i++;
Crianza num = palabra.substring(start, i);

// tira de ceros líderes
Criar canónico = num.replaceFirst("^0+", "));
si (canonical.isEmpty()) canónico = "0"; // todos los ceros

visto.add (canónico);
}
retorno visto.size();
}
}
`` `

¿Por qué un set? * *
Java’s `BigInteger` es grande pero crea un objeto pesado por número.
Robar la cuerda *canónica* mantiene la memoria baja y evita el recorte de la cabeza – suficiente para `n ≤ 1000`.

-...

### 2. Python 3 (Python 3.10+)

``python
Solución de clase:
def numDifferentIntegers(self, word: str) - título int:
visto = set()
I = 0
n = len(palabra)

mientras que yo no
si no palabra[i].isdigit():
i += 1
continuar

comienza = i
mientras que yo hice n y palabra [i].isdigit():
i += 1

num = word[start:i].lstrip('0')
si num == ''
num = '0 '
visto.add(num)

len(seen)
`` `

** Nota pitónica** – `int` es una apreciación arbitraria, por lo que podría convertir `num' a un `int` si prefiere la singularidad numérica, pero la forma canónica de cuerda es más simple.

-...

### 3. C+17 (C++17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int numDifferentIntegers(string word) {
unordered_set obtenidosstring confianza visto;
int i = 0, n = word.size();

mientras (i
si (!isdigit(word[i]) { ++i; continue; }

int start = i;
(i) ++i;
string num = word.substr(start, i - start);

// tira de ceros líderes
size_t pos = num.find_first_not_of('0');
string canonical = (pos == string::npos) ? "0" : num.substr(pos);

visto.insert (canónico);
}
retorno visto.size();
}
};
`` `

**¿Por qué `noordened_set asignados'? * *
El mismo razonamiento que Java: cadena canónica salva la memoria y pasa a un lado la necesidad de «boost::multiprecision» o «__int128».

-...

## 📑 Blog Artículo: “El Bien, el Mal, el Ugly de LeetCode 1805”

■ *Palabras clave de SEO: LeetCode 1805, Número de diferentes enteros en una solución String, Java, solución Python, solución C++, entrevista de codificación, entrevista de trabajo, análisis de algoritmos, análisis de cadenas. *

-...

Introducción

Cuando los reclutadores recubren su currículum, a menudo buscan **recognición de pattern** y **set-theory** problemas—dos pilares básicos de código limpio y listo para la producción.
Problema de LeetCode **1805 – “Número de diferentes enteros en una cuerda”** es una joya así.
Te obliga a:

* Convertir una cadena desordenada en fichas significativas
* Tratar con casos de borde que pueden parecer triviales a primera vista
* Decide la mejor estructura de datos para la singularidad
* Discuss performance trade‐offs

Mastering 1805 muestra que puede manejar datos del mundo real analizando con confianza – una habilidad que resuena en backend, Data-engineering y roles de personal completo.

-...

#### 2down⃣ El Bien

Silencio TENIENDO Feature Silencio Por qué es una fuerza
Silencio...
Silencio **Escáneo de línea** Silencio Únicamente **O(n)** tiempo; los reclutadores aman soluciones lineales de tiempo para pequeños tamaños de entrada. Silencio
Silencio ** Canonical String** Silencio Evita los flujos numéricos; almacenar `"0" vs `"0000"` es trivial. Silencio
Silencio **Set Semantics** Silencio Garantiza la singularidad en tiempo constante; destaca el conocimiento de tablas de hash. Silencio
tención **La Portabilidad del lenguaje-Cross** Silencio Las soluciones en Java, Python y C++ son cortas, limpias y fáciles de explicar en una pizarra. Silencio
Silencio **Clear Edge‐Case Handling** Silencio Demuestra la codificación defensiva (todos los ceros → 0). Silencio

Estas cualidades “buenas” hacen de 1805 una pieza de entrevista **stand-alone**: un ejemplo perfecto “hablar–sobre–su experiencia” en su próxima ronda de codificación.

-...

#### 3down⃣ El malo

Silencio ❌ Problem ← Repercusión permanente
Silencio------------------------
tención **Potential Integer Overflow** Silencio Tokens muy largas (por ejemplo, 100 dígitos) pueden exceder los límites de 64 bits. Use canonicalización de cadenas o bibliotecas de grandes números (Java `BigInteger`, Python’s `int`, C++ `boost::multiprecision`). Silencio
Silencio **Memory Overhead of BigInteger** ← Crear un `BigInteger` para cada número puede ser pesado en Java. ← Guarde la cadena *canónica*; parse solamente si se requiere comparación numérica. Silencio
Silencio **Performance of Regex** Silencio Algunas personas lo resuelven con un regex como `re.findall(r'\d+', word)` luego `int(s)`. Silencio Mientras que rápido para pequeños insumos, regex puede ocultar la lógica y hace más difícil explicar los cambios algoritmos. Silencio

Los reclutadores aprecian a los candidatos que pueden detectar estos obstáculos y explicar por qué un enfoque simple y claro es a menudo preferible.

-...

#### 4down⃣ El Ugly

Silencio 😱 Ugly Pattern
Silencio.
Silencio **Over‐Complicated Regex** Silencio `re.sub(r'[^0-9]', '', word).split()` seguido de un bucle que tira ceros. El regex esconde el análisis *O(n)* y hace difícil ver que el algoritmo es lineal. Silencio
Silencio **Formación Canónica de Bronce** Silencio Añadiendo `"0" al conjunto directamente en lugar de despojar los principales ceros → duplicados (`"01"`, `"1"`). tención conduce a respuestas erróneas; muestra una falta de atención al detalle. Silencio
Silencio **Conversiones de BigInteger Unnecesario** ← Convertir cada ficha en `BigInteger` incluso cuando se ajusta en 32 bits. Añade ciclos innecesarios de CPU y presión de memoria. Silencio

Estos patrones “muy” son trampas comunes para los candidatos que se apresuran a utilizar funciones integradas sin entender la semántica subyacente.

-...

#### 5down⃣ Por qué Solving 1805 ayuda a su búsqueda de trabajo

1. **La manipulación de cuerdas es en todas partes** – Desde los analizadores de registros hasta la enrutación de URL, el análisis de datos mixtos es una tarea diaria.
2. **Set Usage Demonstrates Data‐Structure Awareness** – Programador de amor para ver que usted sabe cuando una tabla de hash vs. conjunto de árboles es apropiado.
3. **Pensando en Edge-Case Shows Maturity** – Handling “0000” vs. “0” es un problema del mundo real en tuberías de limpieza de datos.
4. **Cross‐Language Confidence** – Ser capaz de producir código limpio y idiomático en Java, Python y C++ muestra que puedes trabajar en cualquier pila.
5. **Performance‐First Mindset** – Impresionará a los entrevistadores al explicar que la solución es O(n) y O(k) y por qué eso importa para los sistemas de producción.

-...

#### 6down⃣ Final Takeaway

LeetCode 1805 es *no* un teaser cerebral; es un ejercicio **code-craft** que revela su estilo de codificación pragmática.
Al dominar el patrón **canonical-string + set** usted:

* Evite los obstáculos de desbordamiento
* Mantenga el uso de la memoria bajo
* Entregar código limpio y testable
* Prepárate para discutir *por qué* eligió una estructura de datos sobre otra en una entrevista

Añada los fragmentos Java, Python y C++ arriba a su portafolio GitHub, y deja que los reclutadores vean las partes *buena*, *bad* y *muy* de este problema resueltas con elegancia. Buena suerte en tu próxima entrevista de codificación – ¡estás un paso más cerca de aterrizar ese trabajo de ensueño! 🚀