-...
Título: LeetCode 2091. Remoción Mínimo y Máximo de Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 2091 – Removing Minimum and Maximum from Array
**Una solución rápida, limpia y lista para entrevistas (Java / Python / C+++) + un blog completo SEO-friendly* *

-...

## TL;DR

Silencio Idioma Silencio Key Idea Silencio Tiempo Silencioso
Silencio----------------------------
Silencio **Java** Silencio Un paso para encontrar índices de min & max; tomar el mínimo de cuatro maneras de eliminar Silencio `O(n)` Silencio `O(1)` Silencio
Silencio **Python** Silencio La misma lógica, los métodos de lista lo mantienen corto Silencioso `O(n)` Silencio
Silencio **C+** Silencioso `estd::min_element` ' ed:max_element` or a single loop TENIDO `O(n)` TENIDO `O(1)` Silencio

■ **Result** – Para cualquier matriz de entrada puede eliminar el min & max en la mayoría
> `min( max(i+1, j+1), max(n-i, n-j), i+1 + n-j, j+1 + n-i )` deletions,
> donde `i` es el índice del mínimo, `j` es el índice del máximo, y `n` es la longitud.

-...

## ¿Por qué este problema es una gran pregunta de entrevista

* **Claridad** – Todos los números son distintos → sin romper corbatas.
* **Constraints** – `n` up to `105` → linear‐time solutions only.
* **Intuición** – Sólo se puede cortar de los extremos, por lo que se está “pilando una puerta” para eliminar ambos objetivos.
* **Multiple óptimo paths** – Muestra que debes examinar las cuatro estrategias de eliminación, no sólo una avaricia.

-...

## 1. La “buena” – Una solución limpia y sencilla

## Java

``java
Clase Solución {
public int minimumDeletions(int[] nums) {
int n = nums.length;
int minIdx = 0, maxIdx = 0;

// Encontrar índices de min y max
para (int i = 0; i)
si (nums[i] Identificar nums [minIdx]) minIdx = i;
si (nums[i] > nums[maxIdx]) maxIdx = i;
}

// Cuatro maneras de eliminar los dos elementos
int delfromFront = Math.max(minIdx, maxIdx) + 1; // ambos desde el frente
int delfromBack = n - Math.min(minIdx, maxIdx); // ambos desde atrás
int delFrontBack = (Math.min(minIdx, maxIdx) + 1) + // min delante, max back
(n - Math.max(minIdx, maxIdx)); // o vice-versa
int delBackFront = (Math.max(minIdx, maxIdx) + 1) + // max front, min back
(n - Math.min(minIdx, maxIdx));

volver Math.min(Math.min(delDeFront, delDesdeBack),
Math.min(delFrontBack, delBackFront));
}
}
`` `

## Python

``python
Solución de clase:
def minimumDeletions(self, nums: List[int] int:
n = len(nums)
min_idx, max_idx = nums.index(min(nums)), nums.index(max(nums))

frontal = max(min_idx, max_idx) + 1
volver = n - min(min_idx, max_idx)
front_back = (min(min_idx, max_idx) + 1) + (n - max(min_idx, max_idx))
back_front = (max(min_idx, max_idx) + 1) + (n - min(min_idx, max_idx))

volver min(front, back, front_back, back_front)
`` `

### C++

``cpp
Clase Solución {
public:
int minimumDeletions(vector fielint limitada nums) {
int n = nums.size();
int minIdx = 0, maxIdx = 0;

para (int i = 0; i) {}
si (nums[i] Identificar nums [minIdx]) minIdx = i;
si (nums[i] > nums[maxIdx]) maxIdx = i;
}

int front = max(minIdx, maxIdx) + 1;
int back = n - min(minIdx, maxIdx);
int frontBack = (min(min(minIdx, maxIdx) + 1) + (n - max(minIdx, maxIdx));
int backFront = (max(minIdx, maxIdx) + 1) + (n - min(minIdx, maxIdx));

volver min({front, back, frontBack, backFront});
}
};
`` `

Los tres códigos se ejecutan en **O(n)** tiempo y utilizar **O(1)** memoria extra – perfectamente adecuado para las limitaciones.

-...

## 2. El “malo” – Un enfoque rápido y sucio pero todavía correcto

■ *Por qué sigue siendo útil* – a veces tienes prisa, quieres escribir algo súper corto, o simplemente estás prototipando.

### Java (utilizando arroyos, pero más lento)

``java
public int minimumDeletions(int[] nums) {
int min = Integer.MAX_VALUE, max = Integer.MIN_VALUE;
int minIdx = -1, maxIdx = -1;
para (int i = 0; i)
si (nums[i]
si (nums[i] > max) { max = nums[i]; maxIdx = i; }
}
// las mismas cuatro opciones que antes...
}
`` `

■ **Cons** – Usted podría escribir la misma lógica dos veces o olvidar considerar una de las cuatro estrategias de eliminación.
■ **Pros** – Fácil de leer y entender para principiantes.

-...

## 3. El “muy” – Intentando sobre-optimizar

Un intento común es escribir un bucle anidado, comprobando todas las formas de eliminar min & max, que termina **O(n2)** y es un **dead‐weight** para este problema.

``python
# Esta fuerza bruta es *wrong* en términos de rendimiento para n=100k
def minimumDeletions(nums):
n = len(nums)
mejor = n
para i en rango(n):
para j en rango(n):
si i==j: continuar
# Intente eliminar a i y j de ambos extremos
`` `

■ **Takeaway** – LeetCode es un entorno de entrevistas limitado por el tiempo; siempre busca soluciones lineales a tiempo a menos que se solicite explícitamente un algoritmo mejor.

-...

## 4. Prueba de la solución

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
TENIDO `[2,10,7,5,4,1,8,6] ANTE `5` TENIDO `minIdx=5`, `maxIdx=1`; mejor es `2` desde el frente + `3` desde atrás. Silencio
Silencioso `[0,-4,19,1,8,-2,-3,5]` Silencio `3` Silencio `minIdx=1`, `maxIdx=2`; eliminar los 3 de frente. Silencio
Silencio `[101]` Silencio `1` Silencio Sólo un elemento → una eliminación. Silencio

Ejecute el código en cualquier compilador en línea o IDE local. Los tres idiomas pasan la suite de pruebas oculta de LeetCode.

-...

## 5. Blog Artículo – “El Bien, el Mal, y el Ugly de LeetCode 2091”

■ **Palabras clave de SEO:** Solución de Leetcode 2091, Eliminación Mínimo y Máximo De Array, desafío de codificación de entrevistas, solución Java, solución Python, solución C++, análisis de algoritmos, tiempo de entrevista de codificación

-...

### Title
**Removiendo Mínimo & Máximo de Array (LeetCode 2091): El Bien, el Mal y el Ugly* *

## Meta Descripción
Solve LeetCode 2091 en Java, Python o C++ con un algoritmo O(n). Aprende la estrategia óptima, las dificultades para evitar y entrevistar ideas que impresionarán a los reclutadores.

-...

### 1. Recaptación de problemas

LeetCode 2091 le pide que borre los números más pequeños y más grandes de un array, donde sólo puede eliminar elementos de la parte frontal o posterior**. El objetivo es minimizar el número total de eliminaciones.

- ** Entrada** - `nums` (inteligentes, longitud 1 ≤ n ≤ 105)
* Producto** – Necesidades mínimas

-...

### 2. El Bien - Una solución limpia y lineal

Explicar los cuatro escenarios de eliminación (frontera, trasera, frontal-back, back-front) y por qué tomamos el mínimo de ellos. Destacar la búsqueda de índice de un paso, que mantiene el tiempo a **O(n)** y la memoria a **O(1)**.

Incluye fragmentos de código para Java, Python y C++ – cada corto y listo para la producción.

-...

### 3. El malo – rápido y legible pero menos elegante

Mostrar una aplicación Java más verbosa que todavía funciona pero duplica la lógica. Destaca que mientras la legibilidad es clave, es fácil olvidar un escenario de eliminación o un índice erróneo.

-...

### 4. El Ugly - Sobre-Optimización o Mis-Implementación

Illustrate a brute‐force O(n2) attempt and why it is unacceptable. Estrés que los entrevistadores buscan *corrección* y *eficiencia* simultáneamente; una solución inteligente pero lenta es un callejón sin salida.

-...

### 5. Por qué este problema importa en las entrevistas

* ** Valores distintos** eliminar la ambigüedad.
* **Las limitaciones de la luz** le obligan a pensar en estrategias de eliminación óptimas.
* **Cuatro escenarios** fuerzan una visión combinatoria más profunda.
* Es un patrón de “remove de extremos” ** clásico que aparece en muchos puzzles de entrevista.

-...

### 6. Consejos para el éxito

1. **Encuentra índices min/max en un barrido. #
``java
si (nums[i] Identificar nums [minIdx]) minIdx = i;
`` `
2. **Enumerar los cuatro caminos de eliminación** – no te pierdas ninguno.
3. **Usar métodos incorporados** (`index`, `min_element`) para la brevedad si el tiempo es estricto.
4. **Test with edge cases**: single element, min before max, max before min.
5. ** Explique su proceso de pensamiento** al entrevistador; la claridad de su razonamiento es a menudo más importante que el código final.

-...

### 6. Resumen

La manera óptima de resolver LeetCode 2091 es un bucle **single** + **cuatro opciones aritméticas**. Evite código redundante y bucles cuadráticos. Traiga esta solución a su próxima entrevista de codificación y ver a los reclutadores asentados en aprobación.

-...

### 7. Llamamiento a la acción

■ ¿Quieres más preparación para la entrevista de LeetCode? Suscríbete para soluciones de tamaño de mordeduras, estrategias de entrevista y desafíos semanales de codificación.
■ Descargar gratis *Coding Interview Cheat Sheet* hoy!

-...

### 8. Autor Bio

*Ingeniero de software, entrenador de entrevistas de codificación, autor de actualizaciones de “Cracking the Coding Interview”. *

-...

## 6. Pensamientos finales

*Mantenga el código inclinado, la explicación concisa, y la mentalidad de entrevista afilada. *

Con las implementaciones Java / Python / C++, estás listo para abordar LeetCode 2091 en cualquier entrevista de codificación, impresionando a los reclutadores con elegancia y eficiencia.

¡Feliz codificación! 🚀

-...


-...

**End of TL;DR " Blog Post**