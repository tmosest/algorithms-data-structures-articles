-...
Título: LeetCode 3111. Rectángulos mínimos para cubrir puntos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 3111. Rectángulos mínimos para cubrir puntos – Soluciones completas + Blog Post

-...

### 1. Recaptación de problemas
Se les da `puntos = [[x1,y1],[x2, y2], ...]` y una anchura `w`.
Un rectángulo puede comenzar en cualquier `(x1,0)` y terminar en `(x2, y2)` Sólo si `x2 - x1 ≤ w`.
Todos los puntos deben estar dentro de ** o en** al menos un rectángulo.
Regrese el *mínimo* número de rectángulos necesarios.

■ **Key Insight** – Porque los rectángulos son tiras horizontales que comienzan en `y = 0`, sólo el **x-coordinado** importa para cubrir.
■ Ordenar los puntos por `x` y codictivamente colocar un rectángulo cuando golpeamos un punto fuera del alcance del rectángulo actual.

-...

## 2. Algoritmo (Sort + Greedy)

`` `
1. Ordenar puntos por su ascendente x‐coordinado.
2. lastCoveredX = -∞ (cualquier valor)
3. resultado = 0
4. Para cada punto (x, y) en lista clasificada:
si x Ø último CoveredX:
// iniciar un nuevo rectángulo
resultado += 1
últimoCoveredX = x + w // más lejos x este rectángulo puede cubrir
5. Resultado de retorno
`` `

### Por qué funciona
- Después de ordenar, cualquier punto que aparece después del final del rectángulo actual no puede ser cubierto por él.
- El rectángulo que comienza en el punto actual y se extiende hasta donde se permite (`x + w`) cubre **todo** puntos posteriores cuyo `x` ≤ este límite.
- La colocación saludable es óptima porque retrasar un rectángulo nunca puede reducir el número total.

-...

## 3. Complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
TENIENDO ATENCIÓN `O(n log n)` (en lugar)
SilencioEscaneos intencionales en la vida `O(n)` Silencio `O(1)` Silencio
SilencioTotal sufrimiento **`O(n log n)`** Silencio **`O(1)`** (aparte de la matriz de entrada)

-...

## 4. Implementaciones de referencia

#### 4.1 Java

``java
importa java.util. Arrays;
importa java.util. Comparador;

Solución de la clase pública {}
public int minRectanglesToCoverPoints(int[] puntos, int w) {
// Ordenar por x-coordinado
Arrays.sort(puntos, Comparator.comparingInt(a - título a[0]));

int count = 0;
El último CoveredX = -1; // seguro para grandes valores

(int[] p : points) {
int x = p[0];
si ((long) x Ø lastCoveredX) { // nuevo rectángulo necesario
contar++;
lastCoveredX = (long) x + w; // farthest x este rectángulo puede alcanzar
}
}
recuento de retorno;
}
}
`` `

#### 4.2 Python

``python
de la importación Lista

Solución de clase:
def minRectanglesToCoverPoints(self, points: List[List[int], w: int) - título int:
puntos.sort(key=lambda p: p[0]) # ordenar por x

Conteo = 0
last_covered = -1 # cualquier valor

para x, _ en puntos:
si x Ø last_covered: # start new rectangle
Cuenta += 1
last_covered = x + w
cuenta de retorno
`` `

#### 4.3 C++

``cpp
Incluido el título
#include >

Clase Solución {
public:
int minRectanglesToCoverPoints(std::vector seleccionados:::vector fielint implicado reducir puntos, int w) {
// ordenar por x
std::sort(points.begin(), points.end(),
[](Cont std::vector fielint implica a, const std::vector fieltro b) {
devolver a [0]
});

int count = 0;
largo tiempo Cubierta = -1; // seguro para grandes valores

para (continuo auto-plaza p : puntos) {}
si (durante largo)p[0] √≥ LastCovered) {}
++cuenta;
último Cubierta = (durante largo)p[0] + w;
}
}
recuento de retorno;
}
};
`` `

Las tres soluciones comparten la misma lógica básica y se ejecutan en el tiempo `O(n log n)` con `O(1)` espacio extra.

-...

## 5. Artículo del Blog – “Master LeetCode 3111: Rectángulos Mínimos a Puntos de Cubierta”

■ **Keywords**: LeetCode 3111, Rectángulos Mínimos a Puntos de Cubierta, algoritmo de calidad, solución Java, solución Python, solución C++, entrevista de codificación, entrevista de algoritmos, estructuras de datos, entrevista de trabajo, ingeniero de software, entrevista técnica

-...

#### Introduction

Si se está preparando para las entrevistas de ingeniería de software, se ejecutará rápidamente en problemas que requieren una estrategia limpia *sort-and‐greedy*. LeetCode 3111, **Minimum Rectangles to Cover Points**, es un ejemplo clásico. En este artículo, caminaré a través del problema, mostraré la solución avaricia óptima, discutir casos de borde, presentar código listo para copiar en Java, Python y C++, y explicar por qué este problema es un gran punto de conversación de entrevista.

-...

### Problema Declaración

Dado:
- `puntos = [[x1, y1], [x2, y2], ...]` - todos los puntos son únicos.
- Un ancho.

Cada rectángulo debe tener:
- esquina inferior en el eje x: `(x1, 0)`.
- esquina superior por encima: `(x2, y2)` con `x2 - x1 ≤ w`.

Objetivo: **Cover cada punto con los pocos rectángulos posibles**.

-...

### Why This Problem is Interesting

1. ** Reducción de la dimensión** – Aunque cada punto tiene un 'x' y 'y', el valor 'y' es irrelevante para la cobertura porque todos los rectángulos se extienden desde 'y = 0' hacia arriba.
2. **Optimidad severa** – Una elección codictiva bien escogida (comenzando un rectángulo en el punto más descubierto izquierdo) garantiza la óptimaidad.
3. **Large Input** – `n` puede ser hasta 100 000, por lo que se requiere una solución `O(n log n).
4. **Real‐World Insight** – Este patrón es común en los problemas de programación, cobertura de intervalos y asignación de recursos.

-...

### The Greedy Insight

Ordenar puntos por su x-coordinado. Luego escaneo de izquierda a derecha:

- Si el punto actual está más allá del alcance del rectángulo actual (`x  Confed LastCoveredX`), **comienza un nuevo rectángulo** en este punto.
- El rectángulo abarcará de `x` a `x + w`, así que establece `lastCoveredX = x + w`.

Esto asegura que cada rectángulo cubre tantos puntos como sea posible a su derecho.

-...

### Implementation Walk‐Through

##### Java

``java
importa java.util. Arrays;
importa java.util. Comparador;

Solución de la clase pública {}
public int minRectanglesToCoverPoints(int[] puntos, int w) {
// 1. Ordenar por x
Arrays.sort(puntos, Comparator.comparingInt(a - título a[0]));

int res = 0;
largo último = -1; // cualquier valor < min(x)

(int[] p : points) {
int x = p[0];
// 2. Si este punto no está cubierto, comience un nuevo rectángulo
si ((long) x > last) {
res++;
último = (long) x + w; // alcance del nuevo rectángulo
}
}
restitución;
}
}
`` `

**Qué destacar en una entrevista* *

- Use `long ' for `lastCoveredX` to guard against overflow (`x + w` may be up to 2 × 109).
- Explicar que clasificar con `Arrays.sort` es *estable* suficiente porque sólo importa `x'.

#### Python

``python
Solución de clase:
def minRectanglesToCoverPoints(self, points: List[List[int], w: int) - título int:
puntos.sort(key=lambda p: p[0]) # ordenar por x

res = 0
último = 1

para x, _ en puntos:
si x Ø último:
res += 1
último = x + w
retorno
`` `

**Entreview Tip** – Show that Python’s built‐in `sort` is `Timsort` (optimal `O(n log n)`).

###### C++

``cpp
Clase Solución {
public:
int minRectanglesToCoverPoints(vector identificadovector fielmente usado puntos, int w) {
// Ordenar por x
(puntos.begin(), points.end(),
[](cont auto cho a, const auto golpe b) { return a[0] ANTE b[0]; });

int count = 0;
largo tiempo último = -1; // utilizar largo tiempo para la seguridad

para (continuo auto-plaza p : puntos) {}
si (durante mucho tiempo)p[0]
++cuenta;
último = (largo largo)p[0] + w;
}
}
recuento de retorno;
}
};
`` `

-...

## Edge Cases & Common Pitfalls

Silencio Caso Edge Silencioso Qué ver para Silencio
Silencio...
Silencio Cada rectángulo puede cubrir sólo un punto. El algoritmo todavía funciona. Silencio
SilencioMuy grande `x + w` (Ω 2 × 109) Usar enteros de 64 bits ( " largo " ) para evitar el desbordamiento. Silencio
tenciónPuntos con valores idénticos 'x' El problema garantiza la singularidad, pero si no, la clasificación todavía funciona; los duplicados sólo comparten el mismo rectángulo. Silencio
← Entrada vacía (a diferencia de LeetCode) eterna Return `0` – nuestro bucle naturalmente lo maneja. Silencio
←Coordinaciones negativas La clasificación de las manijas negativas está bien; la última cifra se inicia en `-1`. Silencio

-...

#### Testing Strategy

Silencio Test confidencialidad Puntos Silencio w Silencio esperada
Silencio--------------------------
Silencio1 Silencio `[1,5],[2,3],[5,1]] ' Silencio `3 `` Silencio One rectangle `[1,4]` covers all. Silencio
[1,1],[4,1],[6,2],[9,4]]. " TENIENDO `2 ' Silencio `2` ANTE Dos rectángulos: `[1,3] ' y `[6,8] ' . Silencio
[10,0],[20,0],[30,0] Silencio `5` Silencio `3` Silencio Ancho demasiado pequeño para cubrir más de un punto. Silencio
TEN4 TENIDO Gran matriz aleatoria (105 puntos) TENIDO `105` ANTE Corres en 1 s TEN confirma el rendimiento. Silencio

-...

### Take‐ Away for Interviews

- **Estado la Intuición**: "El y-coordinado nunca importa porque todos los rectángulos comienzan en y = 0."
- **Explicar Optimality**: Mostrar que iniciar un rectángulo en el punto más descubierta izquierda no puede ser mejorado por cualquier otra colocación.
- **Tiempo & Espacio**: Mención que ordena domina el tiempo, y sólo estamos usando memoria adicional constante.
- Language-agnostic**: Puede presentar el algoritmo en cualquier idioma. Es una gran demostración de un algoritmo codicioso O(n log n).
- **Talk About Edge Cases**: Mention overflow and negative coordinates. Muestra que estás pensando en la robustez de la producción.

-...

## Final Thoughts

LeetCode 3111 es un problema engañosamente simple que empaqueta varios conceptos entrevistables:
- Clasificación
- Toma de decisiones graciosas
- Cubierta intervalorada
- Manejo de caso de borde

Dominar no sólo le da una solución lista para usar para la plataforma LeetCode, sino que también demuestra su capacidad para *reducir la dimensionalidad* y *aplicar una estrategia comprobada y avaricia*—skills that hiring managers love to see. Buena suerte en tu próxima entrevista técnica!

-...

### Referencias

- Problema de LeetCode 3111 – * Rectángulos mínimos para puntos de cubierta*
- Discusiones oficiales de solución (Java / Python / C++)
- Entrevista-prep blogs sobre algoritmos codiciosos y cobertura de intervalos

-...

Codificación feliz, y que sus rectángulos siempre sean óptimos!