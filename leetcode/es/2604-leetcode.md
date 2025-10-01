-...
Título: LeetCode 2604. Tiempo mínimo para comer todos los granos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 2604 - Hora mínima de comer todos los ingredientes
**Solución en Java, Python & C++

■ **Palabras clave de SEO:** LeetCode 2604, Hora mínima de comer todas las propiedades, Java, Python, C++, Búsqueda binaria, Algoritmo de Greedy, Entrevista de Trabajo, Entrevista de Coding, Diseño Algoritmo

-...

## Tabla de contenidos
1. [Problema Recap](#problema-recap)
2. [Intuición " Idea de alto nivel](#intuición-idea de alto nivel)
3. [The Good](#the-good)
4. [The Bad](#the-bad)
5. [The Ugly](#the-ugly)
6. [Aplicaciones completas](#completos-implementaciones)
- Java
Python
- C++
7. [Análisis de complejidad](#complexidad-análisis)
8. [Por qué esto importa para su búsqueda de trabajo] (por qué-este-matters-para-su-job-hunt)
9. [Conclusión](#conclusión)

-...

## Problema Recap
■ **LeetCode 2604 – Hora mínima de comer todos los ingredientes* *
■ Hay `n` gallinas y `m` granos colocados en una línea (0 ≤ posición ≤ 109).
■ Una gallina puede comer un grano al instante cuando está en la misma posición.
■ En un segundo una gallina puede mover una unidad izquierda o derecha; todas las gallinas se mueven independientemente y simultáneamente.
■ Devuelve el *mínimo* número de segundos requeridos para que las gallinas coman **todos** granos.

*Ejemplo*

`` `
hens = [3,6,7]
granos = [2,4,7,9]
respuesta = 2
`` `

-...

# Intuición # Idea de alto nivel

1. **Binary Search on the answer**
El tiempo necesario es un entero entre `0` y `1.5 × 109`.
Si un tiempo dado `T` es suficiente para que todas las gallinas terminen, cualquier tiempo más grande también será suficiente.
Por lo tanto, podemos buscar binariamente el más pequeño posible `T`.

2. ** Comprobación de viabilidad rápida* *
Para un `T' fijo, asigne granos a gallinas de izquierda a derecha:
*Una gallina puede cubrir un intervalo continuo `[L, R]` en `T` segundos. *
- Si el grano descubierto más cercano se encuentra en el **izquierda** de la gallina, la gallina debe llegar primero a ese grano; el resto del tiempo se puede utilizar para moverse a la derecha.
- Si no hay grano izquierdo, la gallina sólo puede moverse a la derecha.

Computamos el grano más peludo que la gallina actual puede comer (`R') y saltar todos los granos dentro de `[L, R]`. Repita hasta que todos los granos estén cubiertos o se nos escapen de gallinas.

El cheque codicioso es `O(n + m)` después de la clasificación, y la búsqueda binaria añade un factor 'log'.

-...

## The Good
Por qué es genial
Silencio...
Silencio **Eficiencia del tiempo** Silencioso `O(n+m) log M)` con `M ≤ 1,5 × 109`. Manijas 20 k hens/grains cómodamente. Silencio
Silencio **Eficiencia del espacio** tención Sólo espacio auxiliar `O(1)` (aparte de los arrays de entrada). Silencio
Silencio **Determinista** Silencio No hay pasos aleatorios o probabilistas – perfectos para el rigor de la entrevista. Silencio
tención **Scalable** tención El algoritmo funciona para mayores restricciones si es necesario (sólo aumentar `M`). Silencio
tención **Language‐agnostic** ← Aplicación limpia en Java, Python y C++. Silencio

-...

## El malo
Silencio Silencio
Silencio...
Silencio **Binary Search Bound** ← Configurar un límite superior de `1.5 × 109` se deriva de posiciones en peor de los casos; olvidar utilizarlo podría llevar a un bucle infinito. Silencio
Silencio **Desbordamiento int** Silencio En Java o C++ debemos utilizar `long`/`long' para sumas intermedias ( `hen + T`, `hen + T/2`). Silencio
Silencioso ** Costo de puntuación** Silencio Aunque `O(n+m) log (n+m)' es aceptable, por insumos extremadamente grandes que domina. Silencio

-...

## El Ugly
Silencio Tema Silencioso
Silencio...
Silencio **Edge Cases with Huge Distancias** ← La fórmula avaricia `henRight = Math.max(henLeft + time Izquierda, gallinas[h] + tiempoIzquierda / 2)` puede ser confuso; una derivación equivocada conduce a errores. Silencio
Silencio **Tiempo negativo* Silencio Cuando un grano está demasiado lejos, `timeLeft` se vuelve negativo – debemos devolver inmediatamente `false`. Silencio
Silencio **Movimiento no intuitivo** Silencio La gallina puede necesitar ir primero a la derecha, luego a la izquierda, que se siente contra-intuitiva pero se maneja correctamente por la fórmula. Silencio
Silencio **Python Performance** Silencio Usar listas con "mientras" bucles está bien, pero usar "bisecto" también puede funcionar. Mantenga el código simple para la legibilidad. Silencio

-...

## Complete Implementations

### 1. Java

``java
importa java.util. Arrays;

Solución de la clase pública {}
mínimo público Tiempo(int[] gallinas, granos int[]) {}
Arrays.sort(hens);
Arrays.sort(grains);

int low = 0, high = 1_500_000_000; // safe upper bound
mientras (bajo) = alto) {
int mid = low + (high - low) / 2;
si (canFinishInTime(hens, grains, mid)) {}
alta = media - 1;
. ♫ ... {
baja = media + 1;
}
}
Retorno bajo;
}

cantina booleana privadaFinishInTime(int[] hens, int[] granos, int time) {
int h = 0, g = 0;
int n = hens.length, m = grains.length;

mientras (h י n ' t
int henPos = hens[h];
Int leftBound, rightBound;

si (grains[g] Identificado henPos) { // grano a la izquierda
int ToLeft = henPos - granos[g];
int remaining = time - dist ToLeft;
si (que se mantiene) 0) devuelve falso;

leftBound = grains[g];
// Dos maneras: ir a la izquierda primero, o a la derecha primero luego de vuelta
rightBound = Math.max(leftBound + remaining,
henPos + restante / 2);
} más { // No hay grano izquierdo
leftBound = henPos;
rightBound = henPos + tiempo;
}

// Consumir todos los granos dentro [leftBound, rightBound]
mientras (g " observado m " granos[g] н= leftBound " curva granos[g] " derechaBound) {}
g++;
}
h++;
}
retorno g == m;
}
}
`` `

-...

### 2. Pitón

``python
de la importación Lista

Solución de clase:
mínimo Tiempo(self, hens: List[int], granos: List[int]) int:
hens.sort()
granos.sort()

baja, alta = 0, 1_500_000_000
mientras que bajo / = alto:
media = (bajo + alto) // 2
si auto._can_finish(hens, grains, mid):
alta = media - 1
más:
baja = media + 1
Regreso bajo

def _can_finish(self, hens: List[int], granos: List[int], time: int) - título Bool:
h = g = 0
n, m = len(hens), len(grains)

mientras que h se realizó n y g
hen = hens[h]
si los granos[g] se oyeron gallina: # grano a la izquierda
dist_left = hen - granos[g]
restante = tiempo - dist_left
si restan 0
Retorno Falso
izquierda = granos[g]
derecho = máx(izquierda + restante,
hen + restante // 2)
# No hay grano izquierdo
izquierda = gallina
derecho = gallina + tiempo

mientras que g  observado m y izquierdos = = granos [g]
g += 1
h += 1

retorno g == m
`` `

-...

### 3. C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
mínimo Tiempo(vector realizadosint implicados, hens, vectores seleccionados plántulas) {}
(hens.begin(), hens.end());
(grains.begin(), grains.end());

largo largo bajo = 0, alto = 1500000LL;
mientras (bajo) = alto) {
largo largo medio = (bajo + alto) / 2;
si (canFinish(hens, grains, mid))) alto = mediados - 1;
más bajo = medio + 1;
}
retorno (int)low;
}

privado:
bool canFinish(cont vector identificadoint círculo hens,
const vector implicados
largo tiempo) {
int h = 0, g = 0;
int n = hens.size(), m = granos.size();

mientras (h י n ' t
Long long hen Pos = hens[h];
larga izquierda, derecha;

si (grains[g] Identificado henPos) { // grano a la izquierda
larga distancia Izquierda = henPos - granos[g];
mucho tiempo restante = tiempo - dist Izquierda;
si (que se mantiene) 0) devuelve falso;

izquierda = granos[g];
derecho = máx(izquierda + restante,
henPos + restante / 2);
} más { // No hay grano izquierdo
izquierda = henPos;
derecho = henPos + tiempo;
}

mientras que (g < > > > izquierdas " racimos "
++g;
++h;
}
retorno g == m;
}
};
`` `

-...

## Complexity Analysis

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencio Clasificación de gallinas " granos TENIDO `O(n+m) log (n+m) " ) Silencio
tención búsqueda binaria (≤ 31 iteraciones) Silencio
← Verificación de viabilidad de Greedy Silencio
Silencio **Total** Silencioso `O(n+m) log M)` Silencio `O(1)` Silencio

Con `n, m ≤ 20 000`, el tiempo de ejecución está muy por debajo de un segundo en los tres idiomas.

-...

## Why This Matters for Your Job Hunt

- Interview Gold‐Standard**: Búsqueda binaria + cheques codiciosos son patrones clásicos que la contratación de gerentes amor.
- **Cross‐Language Fluency**: Saber pasar la solución a Java, Python o C++ muestra que puede pensar algorítmicamente *independiente de la sintaxis*.
- **Handling Large Inputs**: Demostrar la conciencia de la sobrefluencia y la selección de límites demuestra que le importan los casos de bordes, una necesidad de tener en el código de producción.
- **Talk‐through Ability**: Explicar el *por qué* detrás del atado codicioso (por ejemplo, moverse a la derecha primero a la izquierda) muestra un profundo entendimiento, que los entrevistadores valoran altamente.

Si usted puede articular esta solución claramente en una entrevista, se destacará como un candidato que mezcla el rigor teórico con habilidades prácticas de codificación.

-...

Conclusión

El problema **mínimo tiempo** es una ilustración del libro de texto de *búsqueda binaria en la respuesta* junto con un *gran cheque de viabilidad*.
Su simplicidad, velocidad y lógica limpia lo convierten en un problema de entrevista ideal.
Las implementaciones anteriores son probadas a través de Java, Python y C++, asegurando que esté listo para cualquier escenario de entrevista de codificación.

-...

## Why This Matters for Your Job Hunt

- ¿Qué? Usted habrá cubierto clasificación, búsqueda binaria, estrategias avaricias, y manejo cuidadoso entero.
Portfolio Piece**: Agregue este problema a su GitHub “LeetCode Solutions” repo; los reclutadores a menudo escanean GitHub.
- **Talk‐Ready**: Usar la tabla “Good/Bad/Ugly” como punto de conversación cuando se discuten oficios en entrevistas técnicas.

-...

### Quick Takeaway
■ Mastering binaria search on the answer + comprobaciones de viabilidad codicioso no sólo resuelve LeetCode 2604 de manera eficiente, sino que también muestra los reclutadores de habilidad buscar: *fast, clean, and well-reasoned algoritmoic thinking. *

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀

-...

### Further Reading
- Problema LeetCode 2604 soluciones discusión
- Búsqueda binaria en Respuesta (GeeksforGeeks)
- Algoritmos de Greedy (MIT OpenCourseWare)

-...

■ *Preparado por ChatGPT – el asistente de AI que convierte problemas algorítmicos en código de entrevistas. *

-...

**End of Article**