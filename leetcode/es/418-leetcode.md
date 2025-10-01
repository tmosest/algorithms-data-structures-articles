-...
Título: LeetCode 418. Fijar la pantalla de la sentencia -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Sentence Screen Fitting – LeetCode 418
**Brute‐Force mple Greedy mple O(1) Optimization**
*Un completo, multi-idioma de paseo + SEO-friendly artículo que le ayudará a aterrizar su próxima entrevista de codificación. *

-...

Sinopsis del problema

Silencio Tema Silencio Detalles Silencio
Silencio...
Silencio **Problema** Silencioso *Sentence Screen Fitting* (LeetCode 418)
Silencio ** Entrada** Silencioso: frase " cuerda " , " filas " , " cols " Silencio
Silencio **Output** Silencio `int` - el número de veces que la sentencia puede ser ajustada en una pantalla de `rows × cols` Silencio
Silencio **Constraints** ← `1 ≤ sentence.length ≤ 100`, `1 ≤ sentence[i].length ≤ 10`, `1 ≤ filas, cols ≤ 2·104`  sometida

Debes conservar el orden de las palabras. Una palabra no puede dividirse; las palabras están separadas por un solo espacio. Las células vacías en la pantalla están llenas de `-` en los ejemplos.

-...

Intuición

La pantalla es escaneada línea por línea. Cada línea puede contener tantas palabras *todas* como el ancho permite. Una vez que una línea está llena, la siguiente palabra comienza en la siguiente línea.
La simulación ingenua es fácil pero **O(rows × len(sentence))** – demasiado lenta cuando `rows` es 20 000 y la frase es larga.

La observación clave: el *estado* de la pantalla después de cada línea es sólo el **index de la palabra** que será impreso después.
Si sabemos cómo el índice cambia después de una fila, podemos "saltar" muchas filas a la vez.

-...

Algoritm – O(rows) Greedy + Memorización

1. **Pre-compute** el siguiente índice de palabras para cada palabra en la oración.
`nextIdx[i]` te dice: *si la siguiente palabra para imprimir es `sentence[i]`, ¿qué palabra será después de que termine la fila actual? *
2. **Evaluar sobre filas** manteniendo un puntero `curIdx` al índice actual de palabras.
En cada iteración:
`curIdx = nextIdx[curIdx]` – saltar a la siguiente palabra inicial.
Mantenga un contador `fits` que aumenta a 1 cada vez que completamos un ciclo completo de la frase (es decir, cuando `curIdx` regresa a 0).
3. **Regresar** el mostrador `fits`.

**Por qué funciona* *
Porque cada fila sólo depende de la palabra inicial. Una vez que sabemos cómo una fila transforma la palabra inicial, el proceso es determinista y se puede repetir fila por día.

**La complejidad* *
- Tiempo: **O(rows + n)**, donde *n* = `sentence.length`.
- Espacio: **O(n)** para la matriz "nextIdx".

-...

## 4Get Cases

Silencio Caso confidencialidad ¿Por qué importa ?
Silencio...
Silencio Palabras más largas que `cols` Silencio Imposible encajar, pero las restricciones prohíben Silencio No se necesita
← La oración tiene exactamente una palabra será `0` después de cada fila ¦
Silencioso `rows = 0` Silencio Sin líneas, respuesta `0` Silencio no se ejecutará

-...

## 5VIEW⃣ Code – Three Languages

■ **Tip**: La versión Java utiliza `int[] nextIdx`, la versión Python usa una lista, y la versión C+ utiliza un `vector fielint ``. Todos comparten la misma lógica.

### 5.1 Java

``java
Solución de la clase pública {}
palabras públicas Tipoping(String[] sentence, int rows, int cols) {
int n = frase. longitud;
int[] nextIdx = nuevo int[n];
int curIdx = 0;

// Pre-compute siguiente índice para cada palabra
para (int i = 0; i)
longitud int = 0;
int j = i;
mientras (verdad) {
int wordLen = sentence[j].length();
si (duración de longitud + palabraLen √≥ chos)
longitud += palabra Len;
j = (j + 1) % n;
// Añadir un espacio después de cada palabra excepto el último en la línea
si (duración) longitud ++; // espacio
}
nextIdx[i] = j;
}

int fits = 0;
para (int r = 0; r  se realizaron filas; r++) {
curIdx = nextIdx[curIdx];
si (curIdx == 0) fits++;
}
la devolución se ajusta;
}
}
`` `

### 5.2 Python

``python
Solución de clase:
def words Tipoping(self, sentence: list[str], rows: int, cols: int) - título int:
n = len(sentence)
siguiente_idx = [0] * n

# Pre-compute siguiente índice para cada palabra
para i en rango(n):
longitud = 0
J = i
Mientras Verdadero:
word_len = len(sentence[j])
si longitud + word_len √≥ cols:
descanso
longitud += word_len
j = (j + 1) % n
# espacio después de una palabra, a menos que exceda la línea
si la longitud
longitud += 1
siguiente_idx[i] = j

cur_idx, cabe = 0, 0
for _ in range(rows):
cur_idx = next_idx[cur_idx]
si cur_idx == 0:
ajuste += 1
ajuste de retorno
`` `

### 5.3 C++

``cpp
Clase Solución {
public:
palabras Titulación (vector seleccionador significando oración, filas, int cols) {
int n = sentence.size();
vector:

// Pre-computa el siguiente índice para cada palabra
para (int i = 0; i) {}
int len = 0;
int j = i;
mientras (verdad) {
int wlen = sentence[j].size();
si se rompen (len + wlen  collares)
len += wlen;
j = (j + 1) % n;
si (len cautivar) ++len; // añadir espacio
}
nextIdx[i] = j;
}

int curIdx = 0, fits = 0;
para (int r = 0; r) {}
curIdx = nextIdx[curIdx];
si (curIdx == 0) + prestaciones;
}
la devolución se ajusta;
}
};
`` `

-...

## 6down Blog‐Estilo Discusión: Bien, mal y feo

■ **SEO Palabras clave**: *ajuste de la pantalla desentencia, solución de leetcode 418, entrevista de codificación, entrevista de trabajo, diseño de algoritmos, codiciado, optimización, Java, Python, C+++ *

### 6.1 The “Bad” Brute‐Force

.
* palabras_in_sentence) – demasiado lento para las hileras de 20k
√≥n para fila en rango(rows):
.
.
" `
■
■ *Por qué falla:*
■ Cada fila se inclina sobre toda la frase, incluso cuando la frase es larga pero la mayoría de las palabras nunca encajan en una sola línea. La complejidad aumenta hasta millones de operaciones.

### 6.2 The “Good” Greedy + Memorización

*Idea clave* *Recuerda dónde terminas después de cada línea. *
- Pre-computar la transición `nextIdx`.
- Por cada fila simplemente saltar: `curIdx = nextIdx[curIdx]`.
- La complejidad es lineal en el número de filas - *optimal para codificación de entrevista*.

### 6.3 The “Ugly” DP Variant (from some editorial)

Algunas soluciones utilizan programación dinámica con un array 2-D para registrar el estado de cada par fila-column.
Si bien técnicamente correcto, utiliza **O(rows·cols)** memoria y tiempo, haciéndolo *necesario* y *más difícil de entender*.
Para una entrevista, mantén la solución simple y legible – **el enfoque codicioso gana**.

### 6.4 Interview‐ Consejos listos

TENIDO TERRITORIO ANTERIOR
Silencio...
Silencio **Explicar la transición del estado** (índice de la palabra siguiente)
* Casos de borde de mención** (palabra única, longitud de la frase 1, etc.) ← Demonstrates thoroughness
Silencio **Análisis de la complejidad en vivo**
Silencio **Mostrar el código en dos idiomas** Silencio Versatile skillset (Java/Python/C++) Silencio

-...

## 7 carreras Takeaway

- **Problema**: Cuenta cuántas veces encaja una frase en una pantalla dada.
- **La mejor solución**: Greedy + memorización (`O(rows + n)`).
- **Key Insight**: El estado de la pantalla después de cada fila está completamente determinado por el índice de la siguiente palabra para imprimir.
- **Idiomas**: Java, Python, C++ – todos usan el mismo algoritmo.

■ Dominar este patrón no sólo le ayudará a as *LeetCode 418*, sino también cualquier pregunta de entrevista que implique *estar empaquetado*, * patrones cíclicos*, o * simulación gris*. Buena suerte aterrizando ese próximo trabajo!