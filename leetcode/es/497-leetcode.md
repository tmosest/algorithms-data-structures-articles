-...
Título: LeetCode 497. Random Point in Non-overlapping Rectangles -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código

A continuación se presentan implementaciones limpias y autocontenidas para **Java**, **Python** y **C+** que resuelven LeetCode 497 – *Punto de flecha en rectángulos no superpuestos*.
Las tres versiones usan la misma idea:

Silencio Silencio
Silencio...
Silencio 1 ← Pre-compute el número ** de puntos enteros** en cada rectángulo:
`area = (x2 – x1 + 1) * (y2 – y1 + 1)` Silencio
Silencio 2 ¦ Construir un **prefix‐sum array** (`puntosPrefix`) de modo que `puntosPrefix[i]` es el número total de puntos en rectángulos `0 ... i`.
Silencio 3 Silencio Escoge un entero al azar `t` en `[0, totalPuntos - 1]`. Silencio
Silencio 4 latitud binaria búsqueda `puntos Prefijo` para encontrar el rectángulo que contiene índice `t`. Silencio
Silencio 5 ← Convertir el índice local dentro de ese rectángulo en coordenadas `x` y `y`. Silencio

El punto resultante es **uniformly distributed** sobre todos los puntos enteros de todos los rectángulos.

-...

### Java (Java 17)

``java
importar java.util*;

Clase Solución {
int privado final[][] rects;
prefijo privado final int[]; // prefijo suma de puntos cuenta
final privado Random rand = nuevo Random();

(int[][] rects) {
este.rects = rects;
int n = rects.length;
prefijo = nuevo int[n];
total = 0;
para (int i = 0; i)
int[] r = rects[i];
int pts = (r[2] - r[0] + 1) * (r[3] - r[1] + 1);
total += pts;
prefijo[i] = total;
}
}

int[] pick() {}
int target = rand.nextInt(prefix[prefix.length - 1]); // [0, total-1]
int rectIdx = binarioSearch(target);
int[] r = rects[rectIdx];
ancho int = r[2] - r[0] + 1;
altura de entrada = r[3] - r[1] + 1;
int base = rectIdx == 0 ? 0 : prefix[rectIdx - 1];
int offset = target - base; // 0-based offset inside this rectangle
int x = r[0] + (ancho de apertura %);
int y = r[1] + (offset / ancho);
volver nuevo int[]{x, y};
}

int privado binarioSearch(int target) {
int lo = 0, hola = prefix.length - 1;
mientras (lo cautivado) {
int mid = (lo + hola) 1;
si (objetivo) se hacía prefijo [mid]) hola = medio;
lo = medio + 1;
}
devolver lo;
}
}
`` `

-...

Python (Python 3.10)

``python
importación al azar
importador bisect
de la importación Lista

Solución de clase:
def __init_(self, rects: List[List[int]):
self.rects = rects
autoprefijo = []
total = 0
para r en rects:
pts = (r[2] - r[0] + 1) * (r[3] - r[1] + 1)
total += pts
auto.prefix.append(total)

def pick(self) - título List[int]:
target = random.randint(0, self.prefix[-1] - 1) # inclusive
rect_idx = bisect.bisect_left(self.prefix, target)
r = self.rects[rect_idx]
ancho = r[2] - r[0] + 1
altura = r[3] - r[1] + 1
base = 0 si rect_idx == 0 más yo. prefijo[rect_idx - 1]
offset = target - base
x = r[0] + ancho de offset %
y = r[1] + offset // ancho
[x, y]
`` `

-...

### C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector realizador implicado rects;
vector realizado largamente larga ventaja; // utilizar largo tiempo para la seguridad
mt19937 rng{random_device{}()};

Solución (vector identificadovector fielint estrecho rects_) : rects(rects_) {
long long total = 0;
para (auto golpe r : rects) {
pts largos = 1LL * (r[2] - r[0] + 1) * (r[3] - r[1] + 1);
total += pts;
prefijo.push_back(total);
}
}

vector() {}
uniform_int_distribución efectuada largamente larga confianza dist(0, prefix.back() - 1);
objetivo largo largo = dist(rng); // [0, total-1]
int rectIdx = lower_bound(prefix.begin(), prefix.end(), target) - prefix.begin();

const auto recurrente r = rects[rectIdx];
ancho largo largo = r[2] - r[0] + 1;
larga altura = r[3] - r[1] + 1;
larga base larga = rectIdx == 0 ? 0 : prefix[rectIdx - 1];
offset largo = objetivo - base; // 0 basado en rectángulo interior

int x = r[0] + int(offset % ancho);
int y = r[1] + int(offset / ancho);
vuélvete.
}
};
`` `

Las tres soluciones se ejecutan en **O(log n)** tiempo por `pick()` (búsqueda binaria en la mayoría de 100 rectángulos) y **O(n)** tiempo para la inicialización.

-...

## 2. Artículo del Blog

■ *Título*
■ “LeetCode 497 – Random Point in Non-overlapping Rectángulos: Java, Python " C++ Soluciones (El Bien, el Mal, " ).

-...

#### Introduction

Si se está preparando para una entrevista de codificación, encontrará rápidamente que **la aleatoria** puede ser un tema sorprendentemente complicado. LeetCode *Random Point in Non-overlapping Rectangles* (Problem 497) es un ejemplo clásico que prueba no sólo el conocimiento de sus datos, sino también su capacidad para razonar sobre la probabilidad y la eficiencia.

En este artículo:

1. Recapitula la declaración del problema.
2. Discuta las dificultades que pueden convertir una gran idea en una aplicación *bug‐prone*.
3. Presentar una solución de consulta limpia **O(n)** pre-procesamiento + **O(log n)**.
4. Mostrar código en **Java, Python, y C+**.
5. Explore “los aspectos buenos, malos y feos” del problema y sus soluciones.
6. Ofrezca información de entrevista y posibles preguntas de seguimiento.

Entremos.

-...

### 1. Reposición de problemas

Se le da un array 'rects' de rectángulos no superpuestos, axis-alignados.
Cada rectángulo es `[x1, y1, x2, y2]` donde `(x1, y1)` es la esquina inferior izquierda y `(x2, y2) ` la esquina superior derecha (tanto inclusiva).

■ **Task** – Diseñar una clase que:
* Inicialmente con `rects`.
* Devuelve un punto entero al azar `[x, y]` que se encuentra dentro *cualquier* de los rectángulos, con cada punto entero siendo igualmente probable.

Constraints:
* `1 ≤ rects.length ≤ 100`
* `-10^9 ≤ x1 se hizo x2, y1 se hizo y2 ≤ 10^9`
* `x2 – x1 ≤ 2000`, `y2 – y1 ≤ 2000`
* Todos los rectángulos están descompuestos.
* Hasta `10^5` llama a 'pick()` en un caso de prueba.

-...

### 2. Las Pitfalls – *Por qué la azarización es dura*

Silencio Pitfall Silencio Por qué importa
Silencio...
Silencio **Inclusive vs. límites exclusivos** Silencio Muchas personas olvidan que los ángulos rectángulos son *inclusivos*. Si los tratas como exclusivos, los puntos de cuenta inferior. Silencio `(x2 - x1) * (y2 - y1) `` en lugar de `(x2 - x1 + 1) * (y2 - y1 +1) `
Silencio **Overflow** Silencio `x2 – x1 + 1` puede ser hasta 2001. Squared da ~4 M. 100 rectángulos → ~400 Puntos M. Todavía cabe en `int`, pero el uso de un entero firmado de 32 bits puede ser inseguro en algunos idiomas (por ejemplo, el `int` de Java es de 32 bits, pero `long` es más seguro). Utilizar `int` en todas partes en Java puede llevar a errores sutiles si los datos de prueba empujan el límite superior. Silencio
Silencio ** Rango de amortiguación fuera por uno** Silencio `Random.nextInt(n)` devuelve `[0, n‐1]`. Olvidar el extremo inclusivo conduce a una distribución **biased**. TENIDA Mixing `nextInt(n)` with `nextInt(n) + 1` or `randrange(n+1)` incorrectly. Silencio
Silencio **Linear search per query** Silencio Con hasta 100 rectángulos, una búsqueda lineal está bien, pero sigue siendo *O(n)* por `pick()`. En una entrevista querrá mostrar un paso logarítmico (búsqueda binaria) si puede. No usar `bisect`/`lower_bound`, o escanear cada rectángulo para cada selección. Silencio
La clase debe mantener las sumas prefijadas; si las recomputas cada llamada, perderás la ventaja O(1). Silencio Re-building prefix sums inside `pick()` → TLE en casos de prueba pesados. Silencio

-...

### 3. La elegante solución

**Core idea** – Piensa en todos los puntos enteros como un *single linear array* de longitud `totalPoints`.
Si pudiéramos mapear un índice aleatorio en esta matriz a un punto concreto `(x, y)`, tendríamos una distribución uniforme automáticamente.

1. **Point Count per Rectangle* *
Cada rectángulo contiene
``text
pts = (x2 - x1 + 1) * (y2 - y1 + 1)
`` `
(el `+1' hace que las esquinas sean inclusivas).

2. **Prefix Sum Array** – `puntosPrefix[i]` = número total de puntos en rectángulos `0 ... i`.
*Construir una vez en O(n). *

3. **Objetivo de flecha**: escoge un entero en `[0, totalPoints-1].
Cada valor de 't' corresponde a un punto único en la matriz lineal global.

4. **Binary Search** – encontrar el más pequeño `i ' tal que `puntos Prefix[i] не t`.
Ese rectángulo contiene el punto con offset local `t - anteriorPrefix`.

5. **Translate Offset → Coordenadas**
Dentro del rectángulo elegido, `Ancho = x2 - x1 + 1`.
``text
localX = x1 + (anchura %)
localY = y1 + (offset / ancho)
`` `

Debido a que cada punto entero tiene una representación *identical* en el array lineal, el punto resultante es uniformemente aleatorio.

■ **¿Por qué búsqueda binaria? * *
"puntosPrefix " se ordena (aumento monotonal). Un estándar `lower_bound`/`bisect_left` nos da el rectángulo en **O(log n)** tiempo – bien dentro de los límites del problema (100 rectángulos) y expectativas de entrevista.

-...

### 4. Code Walkthrough (Java)

``java
Solución de la clase pública {}
int privado final[][] rects;
prefijo final privado[];
final privado Random rand = nuevo Random();

(int[][] rects) {
este.rects = rects;
int n = rects.length;
prefijo = nuevo int[n];
total = 0;
para (int i = 0; i)
int[] r = rects[i];
int pts = (r[2] - r[0] + 1) * (r[3] - r[1] + 1);
total += pts;
prefijo[i] = total;
}
}

int[] pick() {}
int target = rand.nextInt(prefix[prefix.length - 1]); // [0,total-1]
int idx = binarioSearch(target);
int[] r = rects[idx];
ancho int = r[2] - r[0] + 1;
altura de entrada = r[3] - r[1] + 1;
int base = idx == 0 ? 0 : prefix[idx - 1];
int offset = target - base;
int x = r[0] + (ancho de apertura %);
int y = r[1] + (offset / ancho);
volver nuevo int[]{x, y};
}

int privado binarioSearch(int target) {
int lo = 0, hola = prefix.length - 1;
mientras (lo cautivado) {
int mid = (lo + hola) 1;
si (objetivo) se hacía prefijo [mid]) hola = medio;
lo = medio + 1;
}
devolver lo;
}
}
`` `

**Take‐away** – la clase es apátrida después de la construcción; `pick()` es puro y rápido.

-...

### 5. El Bien, el Mal, y el Ugly

La buena vida es la mala vida
Silencio------------------------------------...
Silencio ** La elegancia algorítmica** Silencio Usar una suma prefijo + búsqueda binaria es un patrón de “transform‐then‐search”. Silencio El fracaso para tratar los límites conduce inclusivamente a resultados parciales. Silencio Intentar utilizar un ingenuo “punto aleatorio general en la caja atada y rechazar” enfoque resulta en tiempo exponencial cuando los rectángulos son pequeños o escasos. Silencio
Silencio **Correctomidad** Silencioso `nextInt(total)` + conversión offset garantiza uniformidad sin procesamiento post-procesamiento. ¦ Mis‐calculando el offset (por ejemplo, olvidando el `+1` en ancho) sesgada la distribución. Silencio Volver a un punto basado en `Math.random()` (float) y luego redondear puede introducir sesgo oculto porque la resolución de flotador no es uniforme sobre el rango entero. Silencio
Silencio **Performance** Silencio Pre-procesamiento es lineal en `n` (≤ 100). La consulta es logarítmica. El uso de una búsqueda lineal por `pick()` sigue siendo aceptable aquí, pero una entrevista podría esperar `O(log n)` si `n` puede crecer. TEN Generar números aleatorios en el espacio de 64 bits sin un módulo adecuado puede rebosar o submuestrar. Silencio
Silencio **Language quirks** Silencio Java’s `Random.nextInt()` es **inclusive‐exclusive** – Tenga cuidado con off-by-one. El `random.randint(a, b)` de Python’ es incluyente en ambos extremos; ajustar en consecuencia. La `uniform_int_distribución' de tención C++ requiere ** límites inclusivos** – utilizar `dist(rng)` adecuadamente. Silencio
¿Qué pasa si los rectángulos se superponen? – necesitaría un enfoque diferente (por ejemplo, intervalos aleatorios ponderados). ¿Y si las coordenadas eran punto flotante? – la misma idea funciona, pero usted necesita elegir de un rango continuo. “¿Y si tuviésemos que apoyar la inserción dinámica/delete de rectángulos?” – necesitarías un árbol de segmentos o un árbol de Fenwick. Silencio

-...

### 6. Análisis de la complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio **Construcción** Silencioso `O(n)` – pase único para construir sumas prefijo. Silencio `O(n)` – almacenar los rectángulos y la matriz prefijo. Silencio
Silencio **pick()** Silencio `O(log n)` – búsqueda binaria en el array prefijo (`n ≤ 100`). Silencio `O(1)` – memoria extra constante. Silencio

Debido a que `n` está ligada por 100, esto es esencialmente * tiempo constante* por consulta en la práctica, pero las garantías asintoticas hacen que la solución sea robusta para mayores insumos.

-...

### 7. Entrevista-Ley Insights

* **¿Por qué añadimos `+1` a anchura ' altura? * *
Las coordenadas del rectángulo son inclusivas. Contar los puntos a lo largo de un eje debe incluir ambos puntos finales.

* **¿Y si se permite que los rectángulos se superpongan? * *
La técnica de suma prefijo todavía funciona, pero debe asegurarse de que no está superponiendo las regiones. Un truco común es **scanline** el avión para construir un conjunto de sub-rectángulos descomunales primero.

* **¿Y si necesitábamos *puntos continuos* aleatorios? * *
Sustitúyase el cálculo del offset entero con un punto flotante generado uniformemente en `[0, ancho)` y `[0, altura]`. La lógica de búsqueda binaria se mantiene igual.

* **¿Podríamos hacerlo mejor? #
Para una `n ' muy grande, usted podría utilizar un ** árbol del segmento** o ** Árbol de Frankwick** para lograr `O(log n)` pre-procesamiento y `O(log n)` consultas. Pero con 'n ≤ 100' la matriz simple es preferible para su claridad.

-...

### 8. Preguntas de seguimiento para el entrevistador

1. ** Limitaciones de memoria** – *¿Y si tuviéramos rectángulos 10^5? *
Discuta cómo escala el array prefijo y si necesita una estructura de datos más sofisticada (Árbol de Fenwick/segment).

2. **Actualizaciones sínmicas** – *¿Pueden insertarse o eliminarse rectángulos después de la construcción? *
Hable sobre equilibrar la actualización vs. el rendimiento de la consulta.

3. **Manejo del espejo** – *¿Y si el generador al azar es débil o sesgado? *
Insistir en utilizar funciones de biblioteca comprobadas y evitar PRNGs personalizados a menos que se especifique.

4. ** Casos de edge** – *¿Qué pasa cuando un rectángulo tiene cero área? *
El recuento de puntos se convierte en 0; el algoritmo debe manejar esto con gracia (esquipar tales rectángulos).

5. **Precisión** – * Suponga que las coordenadas son números reales con hasta 6 lugares decimales. *
Mostrar cómo adaptar el cálculo offset a los puntos flotantes preservando la uniformidad.

-...

### Resumen

- El problema es un clásico *mapping índice aleatorio → punto* pregunta.
- Una suma prefijo de puntos cuenta + búsqueda binaria produce una solución **exactamente uniforme**.
- Tenga cuidado con la inclusividad, el desbordamiento y los límites de rango aleatorio.
- El código Java presentado, junto con sus contrapartes Python/C+++, muestra una implementación limpia, eficiente y de lenguaje.

Buena suerte con tu entrevista – ahora tienes tanto la información algorítmica como el código para respaldarlo!