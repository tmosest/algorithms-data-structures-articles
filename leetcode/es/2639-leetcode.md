-...
Título: LeetCode 2639. Encuentra la Ancho de Columnas de un Grid -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 📐 Encontrar la Ancho de las Columnas de un Grid - A Deep‐ Dive Blog
■ **LeetCode 2639 – Easy**
■ **SEO Palabras clave:** `LeetCode 2639`, `find column broad grid`, " Solución java " , " Solución pitón " , " Solución C++ " , " entrevista de trabajo " `

-...

Introducción

Al prepararse para entrevistas de algoritmos de estructuración de datos, a menudo encontrará problemas que suenan simples pero son un *gran* patio para la codificación limpia, el manejo de bordes y el rendimiento óptimo.
LeetCode 2639 – *Encuentra la Ancho de Columnas de un Grid* es uno de estos problemas. Está clasificado como **Easy**, pero prueba su comprensión de:

- 2-D traversal de matriz
- Manejo de enteros negativos
- Conversión de cuerda vs. dígitos matemáticos contando
- Time/Space complejidad mindset

En este artículo caminaremos a través de las partes **buena**, **bad**, y **muy** de resolver este problema, proporcionar soluciones listas para copiar en **Java**, **Python**, y **C++**, y le daremos consejos de entrevista que aumentarán su curriculum.

.
■ Para cada columna, computar la longitud máxima de sus valores (los números negativos obtienen un extra `-`).
■ Complejidad: **O(m·n)** tiempo, **O(n)** espacio.

-...

## 2down⃣ Problem Statement (Re-Worded)

Se le da una matriz 'm x n' entero `grid`.
Para cada columna `i` (0-indexed), definir el * ancho* de la columna como la representación más larga ** de cualquier entero en esa columna.
- Si el entero no es negativo, su ancho es el número de dígitos.
- Si el entero es negativo, su ancho es el número de dígitos **más uno** (para el signo menos).

Devuelva un array `ans` de longitud `n` donde `ans[i]` es el ancho de la `i`‐th columna.

**Constraints* *

Silencio parametro Silencioso
Silencio...
TENIDO `m == grid.length` ANTE `1 ≤ m ≤ 100` TENIDO
TENIDO `n == grid[0].length` ANTE `1 ≤ n ≤ 100`
Ø 109 " Silencioso "

*Examples*

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
Silencio `[[1], [22], [333]]` Silencio `[3]` Silencio El valor más amplio de la única columna es `333` (3 dígitos). Silencio
[15, 1, 3], [15, 7, 12], [5, 6, 2]] Columna 0: `-15` → 3, Columna 1: todos 1-digit, Columna 2: `12 ' y `-2` → 2.

-...

## 3down La “buena” – Solución limpia y legible

### 3.1 Concepto

1. **Initializar** un array `ans` de tamaño `n` con ceros.
2. **Iterate** sobre cada columna `j`.
3. Para cada elemento `grid[i][j]` en esa columna, computa su **Ancho**:
- Convertir en string → `len = s.length()` → Maneja el signo negativo automáticamente.
- Actualizar `max' si este 'len' es más grande.
4. Almacenar `max` en `ans[j]`.
5. Regresa.

Este enfoque es *(m·n)* en el tiempo y *O(n)* en el espacio extra.

### 3.2 Code (Java)

``java
Solución de la clase pública {}
int[] findColumnWidth(int[][] grid) {
int m = grid.length;
int n = grid[0].length;
int[] ans = nuevo int[n];

para (incluido el col = 0; col = n; col++) {}
int maxWidth = 0;
for (int row = 0; row < m; row++) {}
int len = Integer.toString(grid[row][col]).length();
si (len не máxWidth) {
maxWidth = len;
}
}
ans[col] = maxWidth;
}
devolver los ans;
}
}
`` `

### 3.3 Code (Python)

``python
Solución de clase:
def findColumnWidth(self, grid: List[List[int]) - No. List[int]:
si no cuadrícula: devolver []
m, n = len(grid), len(grid[0])
a)
para col en rango(n):
max_w = 0
para fila en rango(m):
w = len(str(grid[row][col]))
si w > máx_w:
Max_w = w
ans[col] = max_w
Retorno
`` `

### 3.4 Code (C++)

``cpp
Clase Solución {
public:
vector asignadoint contacto encontrarColumnWidth(vector identificadovector fielint sentido común grid) {
int m = grid.size();
int n = grid[0].size();
vector:

para (int col = 0; col )
int maxW = 0;
para (infiler fila = 0; hilera)
cadena s = to_string(grid[row][col]); // handles '- '
int w = s.size();
máxW = w;
}
ans[col] = maxW;
}
devolver los ans;
}
};
`` `

" , titulado " *Por qué es bueno: *
- **Readable**: Nombres variables claros, una línea para el cálculo de ancho.
*Idiomática*: Utiliza funciones de conversión de cadenas específicas para cada idioma.
√≥ - **Performance**: No hay operaciones innecesarias; sólo traversales `O(m·n).

-...

## 4down El “Bad” – Lo que debe evitar

¿Por qué es malo arreglar la vida?
Silencio--------------------------------...
TENIDO Utilizando `StringBuilder` o `String` repetidamente en lazos estrechos (Java) Silencio Memory churn, GC pressure TEN Use `Integer.toString()` que es optimizado internamente TEN
Silencio Casting to `long` then to `String` unnecessarily TEN Adds overhead TEN Direct `toString` or `std:to_string` Silencio
TENIENDO EN VIRTUD DEL `Math.log10()` o división para contar dígitos ¦ Casos Edge (`0`) + inexactitudes de punto flotante Silencio Conversión String maneja todos los números enteros limpiamente
Silencio No manipular entrada vacía (rare, pero defensiva) Silencio Correr error en casos de prueba LeetCode Silencio Añadir guardia `if (!grid) return {};` Silencio

-...

## 5down El “Ugly” – Sobre-Optimizado pero difícil de leer

Algunos entrevistadores aman un **single-liner** o un estilo **funcional**:

``java
int[] findColumnWidth(int[][] grid) {
intStream.range(0, grid[0].length)
.map(j - Propiedad IntStream.of(grid).map(row - instrucciones Integer.toString(row[j]).length()).max().getAsInt())
.toArray();
}
`` `

Mientras conciso, sacrifica:

Alguien que lea el código puede no entender inmediatamente la intención.
- Debuggability** - Más difícil de superar.
- **Performance** – La API de flujo puede haber ocultado sobrecabezamiento.

▪ restablecimiento *Evite en entrevistas reales* a menos que el entrevistador solicite explícitamente una solución funcional.

-...

## 6down Ed Edge‐ Lista de verificación de casos

Silencio Caso confidencialidad ¿Por qué importa?¿Cómo lo maneja nuestra solución?
Silencio--------
Silencio **Todos los números negativos** Silencio Necesita la señal de `` contada Silencio `Integer.toString()` incluye " .
Silencio **Zero** Silencio `0` tiene longitud 1 ¦ La conversión de String devuelve `"0". Silencio
Silencio **Maximum/minimum integer** (`±109`) Silencio No hay desbordamiento en la conversión de cuerdas Silencioso `toString` maneja ints de 32 bits de forma segura. Silencio
tención **Single row / single column** Silencio Asegurar que los lazos del lazo sean correctos TENCIÓN Los lazos sobre `grid.length` y `grid[0].length`. Silencio
tención **Large grid (100x100)** Silencioso Prueba de rendimiento Silencioso O(104) operaciones → tiempo trivial. Silencio

-...

## 7VIEW⃣ Alternative Approaches

## 7.1 Math‐Based Digit Counting (Avoiding Strings)

Si desea evitar la conversión de cadena:

``java
int digits(int x) {
(x == 0) retorno 1;
int len = 0;
si
len++; // for '- '
x = -x;
}
(x 0) {
x /= 10;
len++;
}
Len de retorno;
}
`` `

Esto funciona, pero el enfoque de conversión de cadena es *cleaner* y menos error-prone para la mayoría de los contextos de entrevista.

### 7.2 Usando Pre-Calculado Ancho

Usted podría pre-computar un array 2-D ` anchos` de la misma forma que `grid` y luego tomar la columna máxima. Esto añade memoria innecesaria (`O(m·n)` extra), por lo que no vale la pena para un problema fácil.

-...

## 8VIEW⃣ Complexity Analysis

Silencio Silencio Silencio Silencio Silencio
Silencio--------------
TENIDO LLEGADO TENIDO **O(m·n)** Silencio **O(n)** (fuerzo de salida)
Silencio basado en las matemáticas **O(m·n)**
Silencio, transmisión de una línea de duración **O(m·n)**

Ambos enfoques satisfacen fácilmente las limitaciones.

-...

## 9️ Entrevista Consejos " Resume Highlights

1. *Explicar la idea principal* “Logramos sobre columnas y rastreamos el ancho máximo mediante la conversión de cadenas. ”
2. ** Casos de borde de fusión** – números negativos, cero, min/max.
3. **Hablar de la complejidad** – “Esto funciona en tiempo lineal con respecto al número de elementos. ”
4. **Mostrar el código** – Proporcionar un snippet limpio (como arriba) y preguntar al entrevistador si prefiere un idioma diferente.
5. **Opcional** – “Si tuviéramos que evitar la conversión de cuerdas, podríamos usar una rutina de contabilidad de dígitos”. Esto demuestra profundidad.

> *Resume bullet:*
• Diseñada e implementada un algoritmo O(m·n) eficiente para los anchos de columna de computación en cuadrículas de enteros 2-D, manejando valores negativos y casos de borde, resultando en código claro, mantenible en Java, Python y C++.

-...

Conclusión

LeetCode 2639 es un problema engañosamente sencillo que ofrece una plataforma sólida para demostrar una codificación limpia, una cobertura minuciosa y habilidades de comunicación de entrevista. Al enfocarse en la legibilidad y el correcto manejo de los negativos y cero, puede llegar a esta pregunta en una entrevista de codificación y mostrar una habilidad pulida en su currículum.

¡Feliz codificación, y buena suerte aterrizando ese trabajo! 🚀

-..