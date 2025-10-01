-...
Título: LeetCode 84. Rectángulo más grande en Histograma -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

## 1. Code Solutions

A continuación encontrará tres implementaciones de producción que resuelven **LeetCode 84 – Rectángulo más grande en Histograma**.
Los tres utilizan la técnica clásica *monotonic stack*, dando **O(n)** tiempo y **O(n)** espacio auxiliar.

■ **Problema** – Dada una matriz de alturas de barras (ancho = 1), devuelve el área del rectángulo más grande que se puede formar dentro del histograma.

Silencio Idioma Silencio Función Signature ← Complejidad
Silencio----------------------------
Silencio **Java** Silencio `public int largestRectangleArea(int[] heights)` Tiempo de vida: `O(n)` obedecióbr títuloSpace: `O(n)` Silencio
Silencio **Python** Silencio `def largest_rectangle_area(heights: List[int]) - Propiedad int` voca Time: `O(n)` wonbr confianzaSpace: `O(n)` Silencio
Silencio **C+** Silencioso `en el más grandeRectangleArea(vector fieltro puntos bajos altos)` Tiempo de vida: `O(n)` obedecióbr títuloSpace: `O(n)` Silencio

-...

#### 1.1 Java

``java
importa java.util. ArrayDeque;
importa java.util. Deque;

Solución de la clase pública {}
*
* Devuelve el área del rectángulo más grande en un histograma.
*
* @param alturas array de barra alturas
* área de rectángulo máximo de retorno
*/
int public int largestRectangleArea(int[] heights) {}
// Use un centinela -1 para simplificar el cálculo de ancho
Deque cumplióInteger confianza stack = nuevo ArrayDeque correspondió();
stack.push(-1);
int maxArea = 0;

para (int i = 0; i) las alturas.length; i++) {
// Pop hasta que la parte superior de la pila sea inferior a la altura actual
mientras (stack.peek() != -1 " alturas[i] > alturas [stack.peek()]) {}
int h = alturas[stack.pop()];
int w = i - stack.peek() - 1;
maxArea = Math.max(maxArea, h * w);
}
stack.push(i);
}

// Limpiar la pila y procesar barras restantes
(stack.peek() != -1) {
int h = alturas[stack.pop()];
int w = heights.length - stack.peek() - 1;
maxArea = Math.max(maxArea, h * w);
}

volver maxArea;
}
}
`` `

-...

### 1.2 Python

``python
de la importación Lista

Solución de clase:
def largest_rectangle_area(self, heights: List[int]) int:
"
Computa el área de rectángulo más grande en un histograma.
:Alturas del param: Lista[int] – alturas de barras
: retorno: int – área máxima
"
pila = [-1]
max_area = 0

para i, h en enumerar(alturas):
mientras que la pila [-1] -1 y h = alturas [stack [-1]:
altura = alturas[stack.pop()]
ancho = i - pila[-1] - 1
max_area = max(max_area, altura * ancho)
stack.append(i)

# Proceso restante de barras
mientras que la pila [-1] -1:
altura = alturas[stack.pop()]
ancho = len (alturas) - pila[-1] - 1
max_area = max(max_area, altura * ancho)

volver max_area
`` `

-...

#### 1.3 C++

``cpp
Incluido el título
#include >
#include >

Clase Solución {
public:
int largestRectangleArea(std::vector seleccionadoint círculos) {}
std::stack madeint confidencial st; // indices
st.push(-1); // sentinel
int maxArea = 0;

para (int i = 0; i) ++i) {
(st.top() != -1 " alturas [i] " alturas [st.top()] {}
int h = alturas[st.top()];
st.pop();
int w = i - st.top() - 1;
maxArea = std::max(maxArea, h * w);
}
st.push(i);
}

// Barritas restantes
(st.top() != -1) {
int h = alturas[st.top()];
st.pop();
int w = heights.size() - st.top() - 1;
maxArea = std::max(maxArea, h * w);
}

volver maxArea;
}
};
`` `

-...

## 2. Blog Post: “Largest Rectangle in Histogram – The Good, the Bad & the Ugly”

■ **Descripción**: Maestro LeetCode 84 en segundos. Aprenda el algoritmo basado en pilas, trampas, casos de borde, y código fácil de entrevista en Java, Python, " C++. ¡Aproveche sus habilidades de estructura de datos " aterrice su próximo trabajo!

-...

### 2.1 H1 – “Largest Rectangle in Histogram: Mastering a Classic Hard Problem”

■ Cada currículum de ingeniero senior menciona **Monotonic Stacks**. Este artículo te lleva a través del *bueno*, *bad*, y *muy* del problema del rectángulo más grande, más código limpio y de entrevista en Java, Python y C++.

-...

### 2.2 H2 – Problema Recap " Constraints

- **Input**: `heights[0...n‐1]` – alturas de barras, ancho = 1
* Salida**: área del rectángulo más grande
- Constraints**:
- 1 0 0 0 0 0 0
- `0 0 = alturas [i]

Estos límites descartan soluciones cuadráticas; necesita tiempo **O(n)**.

-...

## 2.3 H2 – El Bien: ¿Por qué una estaca monotónica?

1. **Tiempo de luz** – Cada bar es empujado/golpeado al máximo una vez.
2. * Geometría electrónica* – Al escanear de izquierda a derecha, la pila mantiene los índices de barras en orden de altura *principalmente creciente*.
3. **Computación de ancho simple** – Cuando se salta una barra `h`, el siguiente índice en la pila (`stack.top()`) da el límite izquierdo; el índice actual `i` es el límite derecho.
4. **La prueba completa de la corrección** – La pila invariante garantiza que cada rectángulo posible se considere exactamente una vez.

-...

## 2.4 H2 – Lo malo: saltos comunes

Silencio Pitfall Silencio Por qué Sucede
Silencio...
Silencio **Off‐by‐One errors** Silencio Mis‐counting ancho (`i - stack.peek() - 1` vs `i - stack.peek()`) Silencio Usar un centinela `-1` para evitar los anchos negativos
Silencio ** Comprobación de la pila de vacío** ← Olvidar manejar el centinela cuando salta la pila inicial con `-1` o comprobar `stack.empty()` Silencio
Silencio **Large Input** Silencio Usando la recursión o los lazos ingenuos O(n2) Silencio Stick to iterative stack approach ←
Silencio **Overflow** Silencio Altura multiplying * Ancho para 105 bares TENIDO Use `long` en idiomas donde el flujo de entrada es posible (C++, Java) ANTE

-...

## 2.5 H2 – The Ugly: Edge Cases & Performance Trampas

Silencioso Caso Silencioso
Silencio--------------------------------
Silencio **Todos los ceros** TENIDO Altura = 0 → área = 0 TENIDO Stack aparecerá todo inmediatamente; máx se queda 0 Silencio
Silencio **Monotonically increasing** tención Stack crece a tamaño en Silencio Todavía O(n) porque no pops hasta el final ←
Silencio **Monotonically decreasing** Silencio Stack se encoge cada paso Silencio Todavía O(n) debido a un solo paso
Silencio **Large equal heights** ← Consecutive equal bars TEN La condición `traducido=` garantiza que usted pop *all* igual alturas para evitar los rectángulos perdidos
Silencio **Memory limits** Silencio n = 100 000 → tamaño de la pila ♥ n ¦ Aceptable en todos los idiomas (Ω 0,8 MB)

-...

## 2.6 H2 – El Algoritmo (Step‐by‐Step)

1. **Initializar** una pila con centinela `-1`.
2. **Iterate** sobre cada índice:
- Mientras la altura actual `h` ≤ altura en la parte superior de la pila:
- Índice Pop `idx`.
- Altura = `alturas[idx]`.
- Ancho = 'i - stack.top() - 1.
- Actualización `maxArea`.
- Empuja a la pila.
3. **Clean up** restantes índices después del lazo (similar lógica pop con `n` como límite derecho).
4. **Retorno** `maxArea`.

-...

## 2.7 H2 – Código Snippets (Todos los idiomas)

■ *Java*
. ``java
> int public int largestRectangleArea(int[] heights) { ... }
" `

■ *Python*
.
> def largest_rectangle_area(self, heights: List[int]) - confiar int: ...
" `

■ *C++*
, ``cpp
ît int largestRectangleArea(vector identificadoint propietarios altos) { ... }
" `

*(Código completo arriba - ver Sección 1.)*

-...

## 2.8 H2 – Time & Space Complexity

- **Tiempo**: `O(n)` - cada índice es empujado/robado una vez.
- **Espacio**: `O(n)` - la pila puede crecer a `n` en el peor de los casos.
- **Los factores constantes** son pequeños: unas pocas operaciones por iteración.

-...

### 2.9 H2 – Consejos de Entrevista

1. **Explicar la pila invariante**: “La pila contiene índices de alturas crecientes; esto garantiza que conocemos el límite izquierdo para cualquier barra picada. ”
2. **A través de un pequeño ejemplo**: `[2,1,5,6,2,3]` - mostrar empujes/pops y cálculos de área.
3. ** Casos de borde de fusión** que probaste – todos los ceros, aumentando, disminuyendo.
4. **Preguntar preguntas aclaratorias**: por ejemplo, ¿Hay alturas garantizadas no negativas? – muestra a los entrevistadores que se preocupan por las limitaciones.
5. ** Optimizaciones de mención**: evitar bucles adicionales; utilizar centinela para simplificar el cálculo de ancho.

-...

## 2.10 H2 – Takeaways

- **Las pilas monotónicas** son una herramienta poderosa para los problemas de histograma 1-D.
- Evitar errores comunes con un centinela.
- Incluso en un problema “Hard”, una pila de un solo paso da la solución óptima.
- El mismo patrón se aplica a otros desafíos de LeetCode: *Largest Rectangle in a Grid*, *Largest Rectangle of 1s*, etc.

-...

### 2.11 H2 – Call to Action

■ **Listo para asar su próxima entrevista? * *
- Practica esta solución en LeetCode, HackerRank y tus propios proyectos.
≤ - Comparta sus soluciones en GitHub con la etiqueta `#largest-rectangle-histogram`.
⇩ - Suscribirse para obtener más paseantes de entrevista y explicaciones de vídeo.

■ **¡Código, entrevista y tierra que sueño trabajo juntos!* *

-...

### 2.12 H2 – Referencias & Lectura ulterior

1. LeetCode: [Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)
2. YouTube: [Explicación de vídeo – Niits38862Jun 27, 2024](https://www.youtube.com/watch?v=...)
3. Blog Post: *Monotonic Stack – A Deep Dive* (https://example.com/monotonic-stack)
4. GitHub Repo: https://github.com/yourhandle/leetcode-84` – Realizaciones completas " pruebas

-...

■ **SEO Palabras clave**: “Largest Rectangle in Histogram”, “LeetCode 84 solution”, “monotonic stack algoritmo”, “O(n) histogram rectangle”, “Java Python C++ entrevista”, “data structure interview prep”, “get a job coding interview”, “how to solve hard problems”

-...

¡Feliz codificación! 🚀