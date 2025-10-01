-...
Título: LeetCode 1813. Sentence Similarity III -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. El Código – LeetCode 1813 “Similitud de la Sentencia III”

A continuación encontrará ** tres implementaciones limpias y listas de producción** – una en Java, una en Python y otra en C++.
Cada aplicación sigue la misma estrategia de dos puntos de O(n) descrita en el editorial:

1. Dividir ambas frases en listas de palabras.
2. Camina de la izquierda mientras las palabras coinciden.
3. Camina de la derecha mientras las palabras coinciden.
4. Si el número de palabras coincidentes (`izquierda + derecha') es al menos el tamaño de la frase más corta, las dos frases son similares.

-...

### 1.1 Java (formato LeetCode)

``java
importar java.util*;

Solución de la clase pública {}
booleano público sonSentences Similar (String sentence1, String sentence2) {
// Dividir en palabras
Criar[] palabras1 = frase1.split(");
String[] words2 = sentence2.split(");

// Asegurar que las palabras1 son la frase más larga
si (palabras1.izquierda) {}
Criar[] tmp = palabras1; palabras1 = palabras2; palabras2 = tmp;
}

int i = 0, j = 0; // start indices
int n1 = words1.length, n2 = words2.length;

/ / / 1 / ⃣ partido desde el principio
mientras (i י n2 " plom palabras1[i].equals(words2[i])) i++;

/ / / / 2 millas ⃣ partido desde el final
mientras (j  armonizado n2 " plántulas1[n1 - j - 1].equals(words2[n2 - j - 1])) j++;

todas las palabras de la frase más corta están cubiertas
de vuelta i + j n2;
}
}
`` `

■ *Por qué funciona*
■ El único lugar que se puede insertar una nueva frase es entre el prefijo emparejado y el sufijo.
■ Si la parte media inigualable de la frase más larga encaja plenamente en esa “gap”, las dos frases pueden ser idénticas.

-...

### 1.2 Python 3 (formato LeetCode)

``python
Solución de clase:
def areSentences Similar(self, sentence1: str, sentence2: str) - Propiedad Bool:
# Split into lists of words
w1 = sentence1.split()
w2 = sentence2.split()

# Hacer w1 la lista más larga
si len(w1) se len(w2):
w1, w2 = w2, w1

i = 0 punto de partida
j = 0 # end pointer
n1, n2 = len(w1), len(w2)

# Prefix match
mientras que yo hice n2 y w1[i] == w2[i]:
i += 1

# Suffix match
j) x 2 x 1 x 1 x 1 = 1 == w2[n2 - j - 1]:
j += 1

# All words of the shorter sentence are covered
de vuelta i + j n2
`` `

-...

### 1.3 C++ (formato LeetCode)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
bool areSentences Similar (cadena frase1, cadena frase2) {
// Ayudante: dividir una frase en palabras
auto split = [](const string borde s) {
vectoriales res;
Cura de cuerda;
para (cara c : s) {}
si
(!cur.empty() { res.push_back(cur); cur.clear(); }
. ♫ ... {
cur +=c;
}
}
si (!cur.empty()) res.push_back(cur);
restitución;
};

vector asignado w1 = split(sentence1);
vector asignado w2 = split(sentence2);

// Garantizar w1 es el vector más largo
si (w1.size()  w w2.size())) swap(w1, w2);

size_t i = 0, j = 0;
size_t n1 = w1.size(), n2 = w2.size();

// Partido desde el frente
mientras (i י n2 ' p1[i] == w2[i]) ++i;

// Partido de atrás
mientras (j י n2 " sensible w1[n1 - j - 1] == w2[n2 - j - 1]) ++j;

// Todas las palabras de la frase más corta se contabilizan
de vuelta i + j n2;
}
};
`` `

-...

## 2. Blog Post – “El Bien, el Mal, y el Ugly de LeetCode 1813”

■ **Target Keywords:** *LeetCode, Sentence Similarity III, entrevista de algoritmos, entrevista de trabajo, desafío de codificación, preparación de entrevistas, Java, Python, C++ *

#### 2.1 Introduction

Cuando te cruzas **LeetCode 1813 – “Sentence Similarity III”** en tu preparación de entrevistas, lo primero que te golpea es que es un problema de “medio”. Sin embargo, su solución es *remarcablemente simple* una vez que vea el ángulo recto.
En este post caminaremos a través del algoritmo, diseccionamos lo que lo hace grande, expongamos los obstáculos ocultos, y le mostraremos los casos de borde “muy” que podrían subir. También te daremos una aplicación **ready‐to‐paste** en Java, Python y C++ para que puedas presumir de tus habilidades en tu próxima entrevista.

■ *Por qué esto importa para tu búsqueda de trabajo* –
■ Los entrevistadores aman los problemas que le obligan a pensar en términos de *prefix/suffix* y * 2 puntos* trucos. Demostrar el dominio de este patrón muestra que puede traducir una declaración de problema en una solución eficiente y sostenible. Además, conocer las trampas te mantiene desde ese momento de "gotcha" cuando un caso de prueba falla inesperadamente.

-...

### 2.2 Problema Recap

■ ** Objetivo**: Determinar si dos oraciones pueden llegar a ser idénticas insertando *cualquier* frase contigua única (posiblemente vacía) en una de ellas.

- Las oraciones son palabras separadas por el espacio.
- No hay espacios líderes/trailing.
- Las palabras contienen sólo letras (por debajo/por menor).

*Examples*

Silencio en la vida 1 2 TEN ANTE ANTE ANTE ANTE
Silencio--------------------------...
Silencio “Mi nombre es Haley”
Silencioso “de” Silencioso “Muchas palabras”
"Comer ahora mismo" Silencioso "Comer"

-...

### 2.3 The Good – 2‐Pointer Power

Por qué es genial
Silencio...
Silencio **O(n) Tiempo** Silencio Escaneamos cada palabra al máximo dos veces (una vez desde el principio, una vez desde el final). No hay bucles anidados. Silencio
Silencio **O(n) Espacio** Silencio Sólo almacena listas de palabras; no hay estructuras de datos auxiliares pesadas. Silencio
Silencio **Intuitivo** Silencio Los prefijos y sufijos coincidentes es un patrón que aparece en muchos problemas de cuerda (palindromes, prefijo común más largo, etc.). Silencio
tención **Language‐agnostic** Silencio Funciona igual en Java, Python, C++ – sólo dividir cadenas y comparar índices. Silencio
Silencio **La lógica de 2 puntos es a menudo más corta y más clara que la recursión o la programación dinámica para este problema. Silencio

■ **Takeaway** – Un enfoque conciso de dos puntos demuestra que usted puede extraer la esencia de un problema y resolverlo en tiempo lineal.

-...

### 2.4 El mal – Costos ocultos

TEN TERRITORIO TERRITORIO TERRITORIO
Silencio...
Silencio **String splitting overhead** Silencio En un entorno de entrevista ajustada se espera que mantenga el código inclinado. `split(" ")` (Java), `split()` (Python) o tokenization manual (C++) todos asignan nuevas cadenas. Para grandes insumos esto puede convertirse en una sobrecarga mensurable. Silencio
Silencio **Sección sensible a local** Silencio Algunos idiomas tratan los espacios como espacio blanco locale-dependiente. Siempre dividido en el carácter literal del espacio (`'), no en el regex predeterminado, para evitar sorpresas. Silencio
Silencio **Tamaño de entrada más alto** Silencio Aunque el algoritmo es O(n), puede alcanzar el rendimiento de Java 'String.split` O(n2) si utiliza un reex que compila cada vez. Preferir `StringTokenizer` o pareado manual en Java para código de producción. Silencio
Silencio **Edge case “empty sentence”** Silencio La declaración del problema permite insertar una frase *entonces*. Su código debe manejar correctamente frases de cero longitud. Silencio
tención **Desajustes de maletas/bajos** Silenciosos Las palabras son sensibles a casos. Asegúrese de utilizar `equals` (Java) o `==` después de `split()` (Python) – no `=` en Java que compara referencias de objetos. Silencio

-...

### 2.5 The Ugly – "Gotcha" Edge Cases

Silencioso Caso Edge ¿Por qué viajan personas?
Silencio------------------------------------
Silencio **La frase más corta ya es un sufijo del más largo** Silencio `izquierda + derecha' puede ser igual a `n2` sólo si el sufijo emparejado es ** no superposición** con el prefijo. TENIDO Asegurar que los bucles utilizados se utilizaran " no " " " . Silencio
Silencio **Ambos frases idénticas** Silencio Algunos pueden regresar prematuramente a la verdad después del lazo prefijo. La condición final `izquierda + derecha > n2` es el cheque definitivo. Silencio
Silencio **Todas las palabras coinciden pero el orden difiere** Silencio Ejemplo: “Hola Mundo” vs “World Hello” Silencio El método de dos puntos volverá falso porque ni el prefijo ni el sufijo coinciden completamente. Silencio
Silencio **Inserción vacía** Silencio “Hola” vs “Hola” → no hay palabras para insertar, pero el algoritmo todavía debe volver a la verdad. El cheque ``=` maneja el caso medio vacío. Silencio
Silencio **Segmento medio muy largo** Silencioso “a b c ... z” vs “a ... z” Tus arrays divididos deben manejar listas largas. Utilice el persing eficiente en Java (por ejemplo, 'StringTokenizer') si usted está preocupado por el rendimiento. Silencio

■ **Debugging tip** – Después de los bucles de dos puntos, imprimir `i`, `j`, `n2` y asegurar `i + j` nunca excede `n2`. Si lo hace, usted ha cubierto toda la frase más corta.

-...

### 2.6 Pseudocode

``text
dividir la frase1 en palabras1
dividir frase2 en palabras2
si len(palabras1)  le len(palabras2) swap ellos // palabras1 es siempre más largo

izquierda = 0
derecho = 0
n1 = len(words1), n2 = len(words2)

mientras que la izquierda no 2 y palabras1[izquierda] == palabras2[izquierda]:
izquierda += 1

y las palabras1[n1 - right - 1] == palabras2[n2 - right - 1]:
derecho += 1

regreso a la izquierda + derecha n2
`` `

-...

### 2.7 Complexity Summary

Silencioso Complejidad
Silencio--------------------------
Silencio ** Tiempo** Silencioso `O(n)` – cada palabra es examinada al máximo dos veces. Silencio
tención **Espacio** Silencioso `O(n)` – los dos vectores palabra. Silencio
Silencio **Mejor/Mejor** Silencio No hay comportamiento cuadrático oculto. Silencio
Silencio **Scalability** Silencio Funciona cómodamente hasta millones de caracteres (Los casos de prueba de LeetCode son mucho más pequeños). Silencio

-...

### 2.8 Real‐World Interview Checklist

Silencio TENIDO ANTERIOR ANTERIOR
Silencio...
TENIDO TENIENDO TENIDO Utilizar un simple bucle de dos puntos – no recursión o DP. Silencio
TENIDO TENIENDO TENIDO Siempre swap así que la primera lista es la más larga. Silencio
TENIDO ANTERIOR Comparar palabras con `equals` (Java), `==` después `split()` (Python), o `= ' en objetos de `cadena ' (C++). Silencio
TENIDO TENIENDO TENIDO Probar su código en los siguientes casos de borde:
Silencio Silencio 1. “a” vs “a”
Silencio Silencio 2. “a b” vs “b a”
Silencio Silencio 3. “a b c d” vs “a d”
"a" vs "" (la sentencia vacía es **no** permitido por la declaración, pero bueno para comprobar). Silencio

-...

### 2.9 Final Takeaway

- **Mostrar el patrón** – Prefix/suffix matching es una técnica de fuego rápido que impresiona a los entrevistadores.
- Evitar las gotas - Preste atención a la división de cuerdas y los límites punteros.
- **Ready‐to-paste** – Utilice los fragmentos de código arriba en el idioma de su elección.

**Ahora puede entrar en cualquier entrevista de codificación armada con una solución limpia y eficiente a “Sentence Similarity III” y una publicación de blog que le muestra entender el problema a *todo* nivel. Buena suerte aterrizando ese próximo trabajo! #

-..