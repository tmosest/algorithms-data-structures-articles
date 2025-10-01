-...
Título: LeetCode 356. Reflexión de líneas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Code Solutions

A continuación se muestran implementaciones limpias y listas de producción en **Java**, **Python**, y **C+** que resuelven LeetCode 356 – *Line Reflection* in **O(n)** time and **O(n)** extra space.

-...

### 1.1 Java – `Solution.java `

``java
importa java.util. HashSet;
importa java.util. Set;

Solución de la clase pública {}
*
* Comproba si todos los puntos se pueden reflejar en alguna línea vertical.
*
* Puntos @param 2-D conjunto entero de puntos. 0 ≤ puntos[i].length == 2
* @return true if a vertical line of reflection exists, false otherwise
*/
booleano público esReflexed(int[][] points) {
si (puntos == null 0) Retorno verdadero;

// Encuentra las coordenadas x extremas.
int minX = Integer.MAX_VALUE;
int maxX = Integer.MIN_VALUE;
(int[] p : points) {
minX = Math.min(minX, p[0]);
maxX = Math.max(maxX, p[0]);
}

// Sum of the extreme x‐coordinates = 2 * centro de simetría
int sum = minX + maxX;

// Almacene cada punto en un set de hash para búsquedas O(1).
Conjunto de caracteres = nuevo HashSet fiel();
(int[] p : points) {
set.add(encode(p[0], p[1]));
}

// Por cada punto, su espejo también debe existir.
(int[] p : points) {
int mirroredX = sum - p[0];
llave larga = código (mirroredX, p[1]);
si (!set.contains(key)) {
volver falso; / / / socio perdido - no simétrico
}
}
retorno verdadero;
}

*
* codifica un par (x, y) en un solo largo.
* Assumes tenciónx, presiony eterna ≤ 10^8 → encaja cómodamente en 32 bits cada uno.
*/
codificador privado largo (int x, int y) {
retorno (((long) x) < 32) ^ (y < 0xffffffl);
}
}
`` `

-...

### 1.2 Python – `solution.py `

``python
de la importación Lista

Solución de clase:
def isReflected(self, points: List[List[int]]) - conviene bool:
""Return True si el conjunto de puntos es simétrico a través de una línea vertical.""
si no puntos:
Retorno

# Encontrar extremos del eje x.
min_x = min(p[0] para p en puntos)
max_x = max(p[0] para p en puntos
sum_x = min_x + max_x # 2 * centro de simetría

# Almacene todos los puntos como tuples en un set para búsquedas O(1).
point_set = {tuple(p) for p in points}

Cada punto debe tener su espejo.
para x, y en puntos:
reflejado = (sum_x - x, y)
si no reflejado en punto_set:
Retorno Falso
Retorno
`` `

-...

### 1.3 C++ – `Solution.cpp `

``cpp
Incluido el título
#include ■unordered_set
Incluido

Clase Solución {
public:
bool isReflected(std::vector seleccionadosstd:::vector seleccionadointю puntos de unión) {
si (puntos.entonces()) retornan verdaderos;

// Encontrar valores x extremos.
int minX = INT_MAX, maxX = INT_MIN;
para (continuo auto-plaza p : puntos) {}
minX = std::min(minX, p[0]);
maxX = std::max(maxX, p[0]);
}
int sumX = minX + maxX; // 2 * centro de simetría

// Codifique un punto en un entero de 64 bits.
codificador automático = [](int x, int y) - Propiedad int64_t {
retorno (static_cast seleccionadoint64_t título(x) ^ 32) ^ static_cast 0xffffffLL;
};

std::unordered_set S;
para (continuo auto-plaza p : puntos)
S.insert(encode(p[0], p[1]));

para (continuo auto-plaza p : puntos) {}
int mirroredX = sumX - p[0];
si (!S.count(encode(mirroredX, p[1])))
devolver falso;
}
retorno verdadero;
}
};
`` `

■ ¿Por qué funciona esto? * *
■ La línea de simetría debe estar a mitad de camino entre los valores más pequeños y más grandes `x'.
■ Si existe un punto `(x, y)`, el punto reflejado debe ser `(minX + maxX - x, y)`.
■ Usar un set de hash da cheques de pareja de tiempo constante, por lo que todo el algoritmo es lineal.

-...

## 2. Blog Artículo – “Line Reflection: The Good, The Bad, and The Ugly”

■ **Meta‐Description (SEO-friendly): #
■ Master LeetCode 356 – Line Reflection. Obtenga una profunda inmersión en el algoritmo, fragmentos de código en Java, Python & C+++, más información sobre casos de borde, rendimiento y consejos de entrevista. ¡Ponga su preparación de la entrevista de codificación!

#### 2.1 Introduction

Cuando te sientas para resolver LeetCode 356, *Line Reflection*, el primer pensamiento es probablemente “un truco de clasificación” o “dos punteros”. En realidad, hay una solución mucho más limpia, O(n) que incluso pasa 104 puntos con colores voladores. En este artículo diseccionaremos el problema, caminaremos por el mejor acercamiento, tocaremos las trampas (el feo), y terminaremos con códigos listos para copiar para **Java**, **Python**, y **C+**.

### 2.2 Declaración de problemas (Reestablecida)

■ **Given**: `n` puntos en un plano 2-D, `puntos[i] = [x_i, y_i]`.
■ **Task**: Determinar si existe una línea vertical `x = k` tal que reflejar todos los puntos en esta línea produce exactamente el mismo conjunto de puntos.

■ Se admiten puntos repetidos.

### 2.3 Intuición: La Línea Mirror está a medio camino entre extremos

Piensa en la línea como un espejo. Para cualquier punto `(x, y)`, su reflejo es `(k*2 - x, y)`. Observe que el y-coordinado permanece igual – sólo x vueltas. Por lo tanto, si conoce el **centro** de la línea, puede calcular instantáneamente a un socio.

El centro `k` es simplemente el promedio de los x-coordinates más pequeños y más grandes:

`` `
k = (minX + maxX) / 2
`` `

¿Por qué? Debido a que los puntos más izquierdos y más rectos deben ser simétricos sobre el espejo; de lo contrario, ninguna línea individual puede satisfacer todos los puntos. Esto nos da un candidato O(1) para 'k'.

### 2.4 La elegante solución O(n) (Hash Set)

1. **Encontrar extremos** – atravesar una vez para obtener `minX` y `maxX`.
2. **Suma completa** – `sumX = minX + maxX`.
* Nota*: `sumX` equivale a `2 * k`. Trabajar con `sumX` nos mantiene en números enteros y evita errores de punto flotante.
3. **Store todos los puntos** – hash cada par `(x, y)`. En Java/C++ codificamos en un solo entero de 64 bits; en Python un tuple está bien.
4. **Verify partners** – for every point `(x, y)` check whether `(sumX - x, y)` exists in the set.

Si falta algún punto a su compañero, la respuesta es falsa. De lo contrario, tenemos una simetría perfecta.

■ ¿Por qué?
Un paso para encontrar extremos → O(n).
> - Un paso para construir el conjunto → O(n).
> - Un pase para comprobar socios → O(n).
■ El hash set da una búsqueda constante a tiempo, así que el total es lineal.

### 2.5 Edge Cases (The Ugly)

← Caso Edge Silencio Por qué importa Silencio Cómo lo maneja el algoritmo
Silencio--------------------------
← Duplicar puntos Silencio Todos deben tener socios (incluso con ellos mismos). ← Hash almacena cada instancia, así que 'contra' funciona. Silencio
Silencio Todos los puntos en la misma línea vertical tención `minX = maxX` → `sumX = 2*minX`. Silencio El socio de cada punto es en sí mismo → pasa. Silencio
Silencio Coordenadas muy grandes (±108) Silencio Prevengan el desbordamiento. Silencio Encoding utiliza enteros de 64 bits (Java largo / C++ largo). Silencio
TENIDO `n = 1` TENIDO Un solo punto es trivialmente simétrico. El bucle encuentra a su propio socio. Silencio

### 2.6 Enfoques alternativos (El Bien)

- **Sorting + Dos punteros** - ordenar por x, luego para cada punto más izquierdo emparejarlo con el más derecho. Funciona en O(n log n).
*Pro*: No es necesario un set de hash.
*Con*: Factor de registro extra; código más verbose.

- **Mapa de y → Conjunto de x** – grupo por y para manejar grande n más rápido en la práctica.
*Pro*: Maneja bien conjuntos de datos enormes.
*Con*: Más complejo.

### 2.7 Why This Matters for Interviews

- ** Muestra familiaridad con las estructuras de hash** – una habilidad de entrevista de la estructura de datos núcleo.
- **Cuenta la comprensión de la geometría** - no sólo la codificación.
- **Demuestra código limpio y testable** – esencial para entrevistas de producción.

### 2.8 La palabra final (la mala)

- ** Tenga cuidado con el flujo entero** cuando summing `minX + maxX` si está usando entradas de 32 bits en idiomas como C++/Java.
- **Recuerde codificar pares**; usar una cadena `'x#y'` es fácil pero más lento.
- ** Casos de emergencia** como puntos repetidos o una sola línea de puntos puede llegar a soluciones ingenuas.

### 2.9 Code Snippets (Ready‐to‐Paste)

■ #Java #
. ``java
Solución de clase pública {
" boolean public boolean isReflected(int[] points) {
√≥ // ... (código de la sección 1.1)
.
.
" `

■ Python
.
Solución de clase:
> def isReflected(self, points: List[List[int]) - ¿Qué?
(código de la sección 1.2)
" `

■ **C++**
, ``cpp
Solución de clase {}
" Public:
 bo bool isReflected(vector seleccionadovector identificadointющ puntos) {
√≥ // ... (código de la sección 1.3)
.
};
" `

### 2.10 Wrap‐Up

LeetCode 356 es engañosamente simple pero un gran escaparate de pensamiento algoritmo y código limpio. El truco de hash-set te da un **O(n)**, **O(n)** solución espacial que pasa todos los casos de borde y está lista para entrevistarse. Usa los snippets arriba para pulir tu cartera, así la entrevista, y tal vez snag esa próxima oferta de trabajo. ¡Feliz codificación!

-...

**Keywords:** Reflexión de línea, LeetCode 356, simetría de línea vertical, algoritmo O(n), solución de hash set, Java, Python, C+++, prep de entrevista, entrevista de codificación, solución de problemas algorítmicos.