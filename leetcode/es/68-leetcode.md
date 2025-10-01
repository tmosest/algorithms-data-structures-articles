-...
Título: LeetCode 68. Justificación del texto -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 68 - Justificación de texto
**Hard – LeetCode** Silencio **Greedy** Silencio ** Tiempo O(n)** Silencio **Espacio O(1)** (ignorando la salida)

-...

## Tabla de contenidos

Silencio Sección Silencio Lo que aprenderás
Silencio...
Silencio 🎯 Problem Silencio La declaración exacta de LeetCode
TENIDO TENIENTES Ideas clave TENIDA Embalaje Greedy, distribución espacial, última línea justificada por la izquierda
Silencio 🧠 Algorithm ← Paso a paso explicación
Нели не Código ны Java, Python, C++ implementaciones Silencio
TEN 🔍 Casos de borde TENIDO Líneas de palabras individuales, división de espacio desigual, última línea de manejo TENIDO
Por qué la solución es óptima
TEN 📚 Extremidades de entrevista ← Cómo hablar de ello en una entrevista técnica
Silencio 🚀 SEO bonus Silencio Cómo este artículo te ayuda a aterrizar un trabajo

-...

Declaración de problemas

■ **Given** una serie de palabras `palabras ' y una anchura de línea máxima `maxWidth ' , formatear el texto tal que cada línea tiene **exactamente** caracteres `maxWidth` y está completamente (izquierda y derecha) justificado.
■ Empaque palabras con avidez: ponga tantas palabras como sea posible en cada línea.
■ Insertar espacios para que cada línea alcance el ancho requerido.
■ Para una línea con *k* palabras ( " k  título 1 " ), hay " k-1 " vacíos. Distribuir los espacios adicionales uniformemente: si los espacios no pueden dividirse uniformemente, los huecos más altos obtienen un espacio más**.
■ La línea **última** está justificada por la izquierda y no tiene espaciado interno adicional.
■ **Constraints**:
≤ 300.
√≠ - `1 ≤ palabras[i].length ≤ 20`
√≥ 100Â
√≥ - Cada palabra longitud ≤ `maxWidth `

-...

## Ideas clave

Silencio Por qué importa
Silencio...
Silencio **Greedy packing** Silencio Sólo tenemos que mirar la línea actual; una vez que está lleno nos movemos. Silencio
Silencio **Espacio contando** Silencio Mantener los caracteres totales de las palabras y el número de palabras. Silencio
Silencio **Inclus distribution** Silencio Integer division (`extraSpaces / gaps`) + restante (`extraSpaces % gaps`). Silencio
Silencio **Manejo especial** Silencio Última línea (left-justified), líneas con una sola palabra (también zanjada-justificada). Silencio

-...

Algoritmo (Greedy)

1. **Initializar** `idx = 0` – apuntar a la primera palabra que aún no se ha colocado.
2. Mientras que `idx' significa palabras.length` hacer:
1. **Determine line**:
- `lineLen = palabras[idx].length() `
- `último = idx + 1`
- Mientras `últimas palabras.length` y `lineLen + 1 + palabras[último].length() ≤ maxWidth `
* `lineLen += 1 + palabras[last].length() `
* `last++`
2. **Construir la línea**:
- `numWords = last - idx `
- `numSpaces = maxWidth - (lineLen - (numWords - 1))` (los espacios necesarios para alcanzar la anchura)
*Si* *las últimas palabras* # O # `numWords == 1` → *izquierda*
* Apéndice palabras con un solo espacio.
* Pad el final con espacios.
- **Else** → *full justify*
* `espaciosPerGap = numSpaces / (numWords - 1)`
* `extra = numSpaces % (numWords - 1)`
* Por cada palabra (excepto el último) Apéndice `espaciosPerGap + (i iere extra ? 1 : 0)` espacios.
3. **Advance** `idx = last`.

3. Devuelve la lista de líneas construidas.

-...

Código

A continuación se presentan soluciones limpias y idiomáticas para **Java 17**, **Python 3.10+**, y **C+17**.

## Java

``java
importar java.util*;

clase pública {}
totalJustificar (String[] palabras, int maxWidth) {
Lista seleccionadaString titulada res = nuevo ArrayList correctamente();
int i = 0; // índice de inicio de la línea actual
mientras (i  0 palabras.duración) {}
int lineLen = words[i].length();
int last = i + 1;
// Encuentra la última palabra que encaja en la línea
mientras (último) palabras.length "
lineLen + 1 + palabras[last].length()
lineLen += 1 + palabras[last].length();
último++;
}

StringBuilder sb = nuevo StringBuilder();
int numWords = last - i;
// Número de espacios que necesitan ser distribuidos
total Espacios = maxWidth - (lineLen - (numWords - 1));

// Última línea o línea con una sola palabra = zanjado
si (último == palabras.length 1) {
para (int j = i; j) {}
sb.append(words[j]);
si (j  observado último - 1) sb.append(');
}
// Pad el final con espacios
para (int k = sb.length(); k < maxWidth; k++) sb.append(');
. ♫ ... {
// Totalmente justificado
espacios int PerGap = totalSpaces / (numWords - 1);
int extraSpaces = totalSpaces % (numWords - 1);
para (int j = i; j) {}
sb.append(words[j]);
// Las brechas más izquierdas consiguen un espacio extra
para (int s = 0; s  seleccionando espaciosPerGap + (j - i) extraSpaces ? 1 : 0); s++)
sb.append('');
}
sb.append(words[last - 1]); // última palabra, no hay espacios de seguimiento
}
res.add(sb.toString());
i = último; // pasar a la siguiente línea
}
restitución;
}
}
`` `

**Puntos clave* *
- `lineLen` rastrea la suma de longitudes de palabra **plus** un espacio entre cada palabra.
- Total Espacios` es el número crudo de blancos necesarios después de restar los espacios individuales ya presentes.
- El bucle `mientras (último) las palabras.length ' ̈ implementa el empaque codicioso.

-...

## Python

``python
de la importación Lista

Solución de clase:
def fullJustify(self, words: List[str], maxWidth: int) - Lista de contactos[str]:
res = []
I = 0
mientras que yo hice len(palabras):
# Determina cuántas palabras encajan en la línea actual.
line_len = len(words[i])
último = i + 1
mientras que el último (palabras) y line_len + 1 + len(palabras[últimas]) se realizaron= maxWidth:
line_len += 1 + len(words[último])
último += 1

num_words = last - i
total_espacios = maxWidth - (line_len - (num_words - 1))
línea = "

# Última línea o una línea con una sola palabra = título ajustado a la izquierda.
si dura == len(words) o num_words == 1:
línea = ".join(words[i:last])
línea += " * (maxWidth - len(line))
más:
# Full justification.
espacios_per_gap = total_espacios // (num_words - 1)
extra = total_espacios % (num_words - 1)
para j en rango(i, último - 1):
línea += palabras[j]
# Las brechas más izquierdas tienen un espacio extra.
línea += " * (spaces_per_gap + (j - i - se hizo extra)
línea += palabras [últimos - 1]

res.append(line)
I = last
retorno
`` `

-...

### C++

``cpp
Incluido el título
#include ■string

Clase Solución {
public:
std:::vector seleccionados::string confianza fullJustify(std::vector seleccionados:::string Pulse palabras, int maxWidth) {
std::vector seleccionado::string resultado;
size_t i = 0;
mientras (i  0 palabras.size())) {}
// 1. Encontrar el final de la línea
int lineLen = words[i].size();
size_t last = i + 1;
mientras (último)
lineLen + 1 + palabras[last].size() <= maxWidth) {
lineLen += 1 + palabras[last].size();
++último;
}

// 2. Construir la línea
td:: línea de cuerda;
int numWords = last - i;
total Espacios = maxWidth - (lineLen - (numWords - 1));

si (último == palabras.size() 1) {
// Justificado por la izquierda
para (size_t j = i; j)
línea += palabras[j];
si (j + 1 se hizo la última) línea += ' ';
}
line.append(maxWidth - line.size(), ');
. ♫ ... {
// justificación completa
espacios int PerGap = totalSpaces / (numWords - 1);
int extra = totalSpaces % (numWords - 1);
para (size_t j = i; j)
línea += palabras[j];
espacios int = espacios PerGap + (j - i) extra ? 1 : 0);
line.append(espacios, '');
}
línea += palabras [última - 1];
}

result.push_back(line);
i = último; // Mover a la siguiente línea
}
Resultado de retorno;
}
};
`` `

-...

## 🔍 Edge Cases " Common Pitfalls

Silencio Caso confidencialidad ¿Por qué importa?¿Cómo se maneja la solución?
Silencio--------
Silencio **Single word per line** Silencio No hay espacios internos para distribuir. TENIDA `numWords == 1` → camino justificado por la izquierda. Silencio
Silencio **Última línea** Silencio Debe ser justificado a la izquierda independientemente del recuento de palabras. TENCIÓN `último == palabras.size()` desencadena el camino justificado a la izquierda. Silencio
Silencio **Distribución espacial desigual** Silencio Las brechas más izquierdas reciben un espacio extra. Silencio `extra = totalEspacios % (numWords - 1)` y añadir a las lagunas izquierdas. Silencio
Silencio ** Orada exactamente igual a `maxWidth`** Silencio No hay espacios entre palabras. El bucle codicioso se detiene antes de añadir otra palabra; la línea se vuelve justificada a la izquierda. Silencio
Silencio **Muy larga línea de palabras cortas** tención Se pueden necesitar múltiples espacios. TENIDO Cálculos correctamente manejan grandes 'totalSpaces'.

-...

## 📈 Complexity Analysis

TENCIÓN TERRITOR TENIDA Cálculo TENIDO ANTE
Silencio--------------------------
Silencio **Tiempo** Silencio Cada palabra es examinada una vez → `O(n)` Silencio `O(n)` donde `n = palabras.length` Silencio
Silencio **Espacio** Silencio Sólo unas pocas variables enteros + lista de salida Silencio `O(1)` espacio auxiliar (excluyendo la salida) Silencio

La solución es lineal, la más rápida posible porque cada palabra debe ser visitada al menos una vez.

-...

## 📚 Interview Tips

1. **Explicar la decisión avara**: “Seguimos agregando palabras hasta que no podemos encajar en la siguiente. ”
2. **Mostrar su razonamiento para la distribución del espacio**: hablar de división entero y resto.
3. **Manejo del borde de alta luz**: líneas de una sola palabra, última línea, espacios desiguales.
4. **La complejidad**: “Tiempo de trabajo, espacio auxiliar constante. ”
5. **Mostrar un boceto rápido** (líneas, vacíos, espacios) – demuestra una comunicación clara.

-...

## 🚀 SEO Bonus – Landing a Job with This Article

* **Keywords**: LeetCode Text Justification, Greedy Algorithm, Java Interview Question, Python Text Justification, C++ Text Justification, Full Justification, Interview Prep, Coding Interview, Technical Interview, Algorithm Design.
* **Meta description**: “Solve LeetCode’s Text Justification (Hard) en Java, Python y C++. Aprenda un algoritmo codicioso, manejo de los bordes y explicaciones de entrevista. ¡Aterrice su próximo trabajo tecnológico!”
* **Headers**: Use H1 para el título, H2 para secciones, H3 para sub-secciones – Google ama la estructura semántica.
****Code snippets* Los bloques de código visible ayudan a los motores de búsqueda a reconocer el contenido es un tutorial.
* **Readability**: Puntos de bala, párrafos cortos y código destacado mantienen a los usuarios comprometidos → menor tasa de recompensa.

Al publicar este artículo, compartirlo en los blogs de codificación, o agregarlo a su README GitHub, no solo estás practicando la codificación, sino que también estás mostrando tu capacidad de escribir soluciones limpias y de entrevista en varios idiomas.

-...

**Takeaway**: Un algoritmo codicioso conciso, matemáticas del espacio cuidadosa y un manejo robusto del borde hacen que este problema de Hard LeetCode sea un escaparate perfecto tanto para sus cortes de codificación como para sus habilidades de comunicación de entrevista. ¡Feliz codificación y buena suerte en la próxima entrevista de trabajo!