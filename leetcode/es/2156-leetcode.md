-...
Título: LeetCode 2156. Encontrar Substring Con Given Hash Value -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Código - Tres idiomas

A continuación encontrará soluciones limpias y listas de producción para LeetCode **2156 – Encuentre Substring With Given Hash Value** en **Java**, **Python**, y **C++**.
Los tres usan la misma idea – un *rolling hash* computed *backwards* (derecha a izquierda) – para que puedas elegir y pegar el que coincide con tu pila.

■ **Tip** – Cuando te sometes a LeetCode siempre comprobar que usas **long** (64-bit) para el hash intermedio.
■ El producto `val * potencia` puede rebosar fácilmente una entrada de 32 bits cuando `modulo` ♥ 109.

-...

### ⚙ ️ Java – `Solution.java `

``java
Clase Solución {
public String subStrHash(String s, int power, int modulo, int k, int hashValue) {
// Caminamos desde el final de la cuerda hasta el comienzo.
long curHash = 0; // current rolling hash (modulo)
largo powerK = 1; // power^k % modulo (crecerá a medida que nos movemos a la izquierda)
int n = s.length();
int answer = 0; // index of the first matching substring

// Pre-compute power^k % modulo mientras camina
para (int i = n - 1; i 0; i--) {
// Añada el nuevo carácter ( posición actual)
curHash = (curHash * power + (s.charAt(i) - 'a' + 1)) % modulo;

// Si ya pasamos caracteres k, eliminar el más antiguo
si (i + k)
// más antiguo char = s.charAt(i + k)
largo retiro = (long)(s.charAt(i + k) - 'a' + 1) * powerK) % modulo;
curHash = (curHash - remove + modulo) % modulo; // mantenerlo positivo
}

// Una vez que golpeamos la primera ventana de k‐length, grabarla
si
// Recuerde este índice sólo si el hash coincide.
// Porque nos estamos moviendo * hacia atrás*, el último golpe es el
// primera subestring en el orden original.
si (curHash == hashValue) {
respuesta = i);
}
}

// Potencia de crecimiento K para la siguiente eliminación (la próxima iteración mueve un paso más a la izquierda)
powerK = (powerK * power) % modulo;
}

volver s.substring(respuesta, respuesta + k);
}
}
`` `

■ **¿Por qué caminar de derecha a izquierda? #
La División (por `poder ' ) es imposible bajo el modulo porque `modulo ' puede no ser coprime con `poder ' .
■ Caminando hacia atrás nos permite *multiply* en lugar de *divide*, que mantiene la matemática simple.

-...

### ## Python - `solución. py `

``python
Solución de clase:
def subStrHash(self, s: str, power: int, modulo: int,
k: int, hashValue: int) - título str:

cur_hash = 0 # actual hash (modulo)
power_k = 1 # power^k % modulo
n = len(s)
respuesta = 0

# Camina desde el final hasta el principio
para i en rango(n - 1, -1, -1):
cur_hash = (cur_hash * potencia + (ord(s[i]) - 96) % modulo

si yo + k < n:
eliminar = (ord(s[i + k]) - 96) * power_k) % modulo
cur_hash = (cur_hash - quitar) % modulo

# Recuerda *último índice que coincidió – que es la primera subestring
si cur_hash == hash Valor:
respuesta = i

power_k = (power_k * power) % modulo

retorno s[answer:answer + k]
`` `

√≥ `ord(s[i]) - 96` es una manera rápida de computar `val(s[i] (`'a'` → 1, `'b'` → 2 ...).

-...

#### ⚙י C++ – `Solution.cpp `

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
cadena subStrHash(string s, int power, int modulo,
int k, int hashValue) {
Long long curHash = 0; // current rolling hash (modulo)
largo largo de potenciaK = 1; // power^k % modulo
int n = (int)s.size();
int answer = 0; // index of the first matching substring

para (int i = n - 1; i 0; --i) {
// Agregar el nuevo personaje en la posición i
curHash = (curHash * potencia + (s[i] - 'a' + 1)) % modulo;

// Quitar el personaje que ahora está fuera de la ventana
si (i + k)
largo largo retiro = (largo largo) (s[i + k] - 'a' + 1) * powerK) % modulo;
curHash = (curHash - remove + modulo) % modulo;
}

si (curHash == hashValue) // recuerda el último golpe
respuesta = i);

powerK = (powerK * power) % modulo;
}

retorno s.substr (respuesta, k);
}
};
`` `

" Substr " es equivalente a " subestring " en Java, ambos toman índices * basados en cero*.

-...

## 2down Blog Blog Post – SEO‐Optimised & Job-Entreview Friendly

■ **Título (H1)* *
■ **“LeetCode 2156 – Encontrar Substring Con Given Hash Value: Rolling‐Hash + Sliding‐Window Solutions (Java, Python, C++)* *

-...

### 📚 Problema Resumen

En el **2156** de LeetCode, se le da una cuerda `s`, un entero `poder`, un entero grande `moulo`, una longitud de la ventana `k`, y un valor hash target `hashValue`.
Necesitas devolver la subestring **primera** de longitud `k` cuyo *hash* (definido a continuación) equivale a `hashValue`.

**Definición hach**

`` `
hash(s[i ... i + k – 1], power, modulo) =
( val(s[i]) * power^0
+ val(s[i+1]) * power^1
+ ... + val(s[i+k-1]) * power^(k-1) ) % modulo
`` `

`val(c)` = (`a'` → 1, `'b'` → 2 ...).

-...

¿Por qué un Rolling Hash?

Silencio TENIDO **Pros** Silencio ❌ **Cons**
Silencio----------------
Silencio • **O(n)** tiempo – sólo un paso sobre `s` (≤ 105) Silencio • Requiere cuidadoso manejo de ** aritmética modular**; valores negativos después de la subtracción
Silencio • **O(1)** espacio auxiliar (sólo unas cuantas largas) Si usted computa de izquierda a derecha necesita un inverso modular de 'poder', que es caro/complicado
Silencio • Funciona para *cualquier* `modulo`, incluso no-coprime con `poder` Silencio • Riesgo de desbordamiento si utiliza ints de 32 bits para productos intermedios

-...

### 🚀 The Backward‐to-Left Technique

1. **Pre-compute** `power^k modulo` mientras camina a la izquierda.
Este valor (`powerK`) le permite *subtract* el carácter que deja la ventana en O(1).

2. Empieza desde el final de la cuerda.
Para cada personaje " c = s " :
* `curHash = (curHash * power + val(c) % modulo` –‐ añadir el nuevo personaje.
* Si ya hemos procesado al menos caracteres 'k', resta el *antiguo*:
`remove = val(s[i+k] * powerK % modulo `
`curHash = (curHash - remove + modulo) % modulo` (add `modulo` before `%` to keep it positive).

3. **Registre el último índice** donde `curHash == hashValue`.
Debido a que caminamos desde la derecha, el *último* golpe en este pase es el *primer* subestring en orden de avance.

-...

#### 📈 Complexity

- **Tiempo**: `O(n)` - uno pasa por `s`.
- **Espacio** : `O(1)` - un puñado de variables largas.

-...

### ## 🛠ف Common Pitfalls & Fixes

Silencio Silencio
Silencio...
Silencio **Overflow** (`val * power`) Silencio Uso `long` (64-bit). `(long)val * power) % modulo`. Silencio
Silencioso ** Modulo negativo** después de la resta Silencio Añadir `modulo` antes `%` : `(curHash - remove + modulo) % modulo`. Silencio
Silencio **Off‐by-one** en subestring indices TENIENDO ACUERDO `respuesta` es el *start* de la ventana; `s.substr(respuesta, k)` (C++/Python) o `s.substring(respuesta, respuesta + k)` (Java). Silencio
Silencio **Large `modulo` ♥ 109** Silencio Asegúrese de que no vuelva a lanzar el producto a `int` antes `% modulo`. Silencio

-...

Caso de prueba de muestras

Silencio input Silencio `s ' Silencio `poder ' Silencio `k` Silencio `hashValue` Silencio
Silencio----------------------------------------------------------------------
Silencio `'abcd'` Silencio 1 Silencio 100 Silencio 3 Silencio 2 Silencio 4 Silencio `"ab"
Silencioso `'abcd'` Silencio 2 Silencio 1000 Silencio 3 Silencio 2 Silencio 2 Silencio `"bc"
Silencio `'a' Silencio 1 Silencio 1 Silencio 1 Silencio 1 Silencio 1 Silencio `'a' Silencio

Ejecute el código en LeetCode o su IDE favorito para verificar.

-...

## 3Ω⃣ Blog – “Mastering LeetCode 2156: A Rolling‐Hash Interview Cheat Sheet”

■ **Keywords** – `LeetCode 2156`, `Find Substring With Given Hash Value`, `rolling hash`, `sliding window`, `Java solution`, `Python solution`, `C++ solution`, `hash function`, `job interview algoritmo`, `coding interview practice`.

-...

#### } Introducción

■ *“Lo hash up, deslizalo hacia adelante – el desafío LeetCode 2156 es un caso de libro de texto de hash rodante y ventana corredera. Entréguelo, y se dará un nuevo conjunto de preguntas de entrevista.”*

Si se está preparando para una entrevista de instrucciones de datos o un papel *software engineering*, este problema es un escaparate perfecto de su capacidad para manejar ** aritmética modular** y ** procesamiento eficiente de cadena**. El siguiente artículo te lleva a través de las partes **bueno**, **bad**, y **muy** de la resolución 2156, te da el código completo en tres idiomas, y explica por qué es un gran escaparate de entrevistas.

-...

Problema Recap

■ **Input**
≤ - `s` - una cadena de letras minúsculas (`1 ≤  sometidas sometidas ≤ 105`)
- `poder' - base del hash (`2 ≤ potencia ≤ 106`)
■ - `modulo` - modulo (`2 ≤ modulo ≤ 109`)
√≥ - `k` - longitud de la ventana de subestring (`1 ≤ k ≤ ¦
≤ hashValue - `hashValue` – target hash value (`0 ≤ hashValue י modulo`)

■ **Task**
■ Encontrar el **primer** subestring de longitud `k` cuyo hash iguala `hashValue`, según la fórmula anterior.
■ Si no existe tal subestring, devuelve una cuerda vacía.

-...

### 🎯 ¿Por qué es 2156 una "Must‐Know" Entrevista Pregunta?

1. **String Hashing** – Muestras que puedes convertir una cuerda en una huella numérica, una técnica común en *diseño de algoritmo* (por ejemplo, Rabin‐Karp).
2. ** Aritmética Moderna** – Trabajar con grandes moduli es una habilidad sutil que muchos candidatos pasan por alto.
3. **Venta deslizante** – Destaca su comprensión de *O(1)* actualizaciones de la ventana, esencial para muchos problemas *real-time*.
4. ** Elegancia Algorítmica** – El retroceso elimina la necesidad de inversos modulares, haciendo la solución tanto **limpio** como **fast**.

-...

### llevándose el “bueno” – Lo que funciona tan bien

1. **Linear Time** – `O(n)` asegura que incluso las cuerdas permitidas más largas terminen en milisegundos.
2. **Espacio constante** – Sólo algunas variables largas; no hay arrays adicionales o tablas de hash.
3. **No Modulo Inverse** – Evita las matemáticas pesadas; en lugar de multiplicarse, que es trivial bajo el módulo.
4. ** Técnica reutilizable** – El mismo patrón (volver a rodar + subtracción Power^k) se aplica a *Rabin‐Karp* patrón de coincidencia y *prefix‐hash* consultas.

-...

### ❌ The “Bad” – What Traps Beginners

Por qué Fails
Silencio--------------------
Silencio ** Multiplicación directa** Silencio Sin inverso modular, estás atascado; la base `poder' puede compartir factores con `modulo`. Silencio
Silencio **Ignorando los resultados negativos** Silencio Subtracting the leaving character can produce a negative number; El uso de `%` en un largo negativo en C++/Python lo deja negativo, rompiendo el control de igualdad. Silencio
Silencio **Usando ints de 32 bits** Silencio El producto `val * power` puede exceder `231`; el compilador puede envolver silenciosamente alrededor, dando a los hashes equivocados. Silencio
Silencio ** confusión index** Silencio Recuerde que el subestring de Java utiliza índices *end-exclusive*; C++’s `substr` tarda mucho. Un común de los cultivos de error al convertir entre idiomas. Silencio

-...

### 😖 The “Ugly” – Edge‐Case Traps

Silencioso Caso Edge Silencioso Consequence
Silencio------------------
Silencio `k` iguala toda la cuerda Silencio Tu ventana nunca se mueve; todavía tienes que manejar el primer golpe correctamente. Silencio Trate de la cadena completa como una ventana; el algoritmo naturalmente cae de vuelta. Silencio
TENIDA `modulo` igual `1` voca All hashes become cero; but `hashValue` may still be non-zero. Asegurar que el algoritmo no se divide por cero; el producto `(powerK * power) % modulo` permanecerá cero. Silencio
Silencio " poder " muy grande " , muy pequeño `moulo " (Sujeto) 2) tención Frecuente desbordamiento, pero todavía manejable con 'long'. tención Uso 64 bits enteros; modulo reduce el valor rápidamente, evitando el crecimiento de fuga. Silencio

-...

### 📦 Código completo Snippets (Tres idiomas)

El artículo anterior enumera las implementaciones **Java**, **Python**, y **C++** en un solo lugar. Copiar / pegarlos en LeetCode, probar en su máquina local, o ejecutarlos en un compilador en línea. La lógica central – la resta atrasada traversal + `powerK` – sigue siendo la misma, sólo cambios de sintaxis.

-...

### ## ❌ Why 2156 is a **Show‐case** Problema

*Demonstrates modular arithmetic*: Muchos entrevistadores preguntan sobre “hashing” o “Rabin‐Karp”. Muestras que sabes cómo manejar correctamente `%`, incluyendo la maleta de la esquina de la resta.
- **Las luces correderas-ventana**: Las ventanas deslizantes son un punto de partida para *resultas de rango* y *problemas de intervalo*. Si clavas 2156, ya estás cómodo con este patrón.
- **Scales**: La solución `O(n)` muestra que puede resolver problemas con grandes limitaciones (105 caracteres) de manera eficiente, un software de alto rendimiento.
- Language-agnostic**: Tener soluciones listas para usar en Java, Python y C++ muestra que puedes cambiar contextos dependiendo de la pila de tecnología del trabajo.

-...

### 🚀 Cómo usar esta hoja de Cheat

1. **Practice** – Ejecutar las tres implementaciones en todos los casos oficiales de prueba en LeetCode; ajustar el código para la claridad o añadir comentarios.
2. **Explicar** – En una entrevista, caminar por el enfoque atrasado, enfatizando por qué nos multiplicamos en lugar de dividir.
3. **Mostrar Variedades** – Preguntar: “¿Qué pasa si el poder era 1? ¿Y si `modulo` era 1? Muestra que puedes razonar sobre casos de esquina.
4. **Mention Trade-offs** – Brevemente declara que izquierda a derecha necesitaría un inverso modular y por lo tanto es menos eficiente.

-...

#### Гельные Takeaway

■ *Si puedes explicarle a LeetCode 2156 en una habitación llena de ingenieros, demostrarás maestría de dos pilares de diseño de algoritmos. *

■ Ya sea que usted está apuntando a un **desarrollador de software** papel, una posición **data‐engineer**, o una carrera de programación **competitiva**, la técnica de rodaje que usted aprende aquí pagará dividendos por los próximos meses.

-...

#### 📚 Más lectura

- *Rabin–Karp algoritmo* – el enfoque clásico de hash rodante para la búsqueda de subestring.
- *Venta deslizante* – un patrón que aparece en problemas como “Suma de Subarray Máximo de Tamaño K”.
- * Inverso móvil* – cuándo y cómo computarlo (útil para otros problemas).
- *Big O Notation* – seguir practicando para detectar rápidamente si un algoritmo pasará grandes entradas.

-...

#### 🏁 Closing

■ “Lo hash, deslizarlo, resolverlo – ese es el mantra de LeetCode 2156. Código la solución, entender las matemáticas, y traerla en su próxima entrevista. ”

Feliz codificación, y que sus hashes siempre sean *derecha*!

-...

**End of blog. #
(Sea libre de publicar en Medium, Dev.to, o su sitio de cartera personal – la estructura asegura que se clasificará bien para las palabras clave apuntadas.)