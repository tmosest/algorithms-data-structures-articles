-...
Título: LeetCode 2250. Número de rectángulos que contienen cada punto -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 2250. Número de rectángulos que contienen cada punto – LeetCode Deep‐Dive
*(Java fort Python ← C++) – Un blog de amistad entre trabajo*

-...

## Tabla de contenidos
1. [Norma general](#problema vista previa)
2. [Solución ingenua " Por qué se desvanece " .
3. [Observación de clave](Observación de teclas)
4. [Optimal Algorithm](#optimal-algorithm)
5. [Análisis de complejidad](#complexidad-análisis)
6. [Edge‐Case Checklist](#edge-case-checklist)
7. [Instrucciones completas](#implementaciones)
* Java
* Python
* C++
8. [Testing the Solution](#testing)
9. [Entreview‐Ready Tips](#interview-tips)
10. [SEO‐Friendly Summary](#seo-summary)

-...

## 📌 Resumen del problema <a name="problema-overview"

Se les da:
- `rectangles`: `[l1,h1], [l2,h2], ...]` - cada rectángulo comienza en `(0,0)` y termina en `(li, hola)`.
- `puntos `: `[x1,y1], [x2, y2], ...]` - un conjunto de puntos de consulta.

Devuelva un array `contra` donde `contra[j]` es el número de rectángulos que **contiene** punto `(xj, yj)`.
Los puntos en el borde del rectángulo se consideran dentro.

**Constraints* *

Silencio parametro Silencioso
Silencio...
TENIDO `rectangles.length`, `points.length` TEN 1 ... 5 × 104 ANTE
TENIDO `1 ≤ li, xj ≤ 109` TENIDO
TENIDO `1 ≤ hola, yj ≤ 100
Silencio Todos los rectángulos / puntos son únicos

Debido a que la *altura* está cubierta a 100, podemos explotar esto para lograr una solución eficiente.

-...

## Ø Solución Naïve " Por qué Fails " seleccion "

Un bucle doble directo:

``text
para cada punto (x, y):
para cada rectángulo (l, h):
si x <= l y y  y= h: count+
`` `

*Tiempo*: O(P · R) ♥ 2.5 × 109 operaciones → ** Tiempo-out**.
*Pace*: O(1).

Necesitamos un enfoque más inteligente que reduzca el número de cheques rectángulos por punto.

-...

## 🔑 Observación de claves = nombre= "observación de teclas"

- Altura (h) ≤ 100** - un rango pequeño y fijo.
- Para una altura fija `h`, sólo los rectángulos con esa altura exacta (o mayor) pueden contener un punto con `y ≤ h`.
- Si agrupamos longitudes de rectángulo (`l`) por altura, cada grupo se puede ordenar una vez.
- Para un punto de consulta `(x, y)`, sólo necesitamos mirar grupos con altura `h ' donde `h ≥ y`.

Así, transformamos un problema de contención 2-D en una búsqueda **1-D** en la mayoría de 100 listas clasificadas.

-...

## 🚀 Algorithm Optimal se hizo un nombre="optimal-algorithm"

1. **Bucket por altura* *
- Crear un array `buckets[101]` (`0` no utilizado).
- Por cada rectángulo `(l, h)`, empuje `l` en `buckets[h]`.

2. **Córta cada cubo**
- Por cada altura que tiene rectángulos, ordenar la lista de longitudes ascendiendo.

3. **Respuestas preguntas**
Por cada punto:
``text
total = 0
para h en [y, 100]:
si los cubos no están vacíos:
// búsqueda binaria para encontrar primero l √≥= x
idx = down_bound(buckets[h], x)
total += (len(buckets[h]) - idx
contable.append(total)
`` `

La búsqueda binaria garantiza O(log k) por cubo, donde *k* es el número de rectángulos de esa altura.
Debido a que el bucle exterior itera en la mayoría de 100 veces, el trabajo total por consulta está atado.

-...

## 📈 Complejidad Análisis - nombre= "complexity-analysis"

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencio Hebilla edificio Silencioso **O(R)** Silencio **O(R)** (para guardar longitudes)
Silencio Ordenación de cubos Silencio **O(R log R)** (sum over all cubos)
Silencio Procesamiento de consultas Silencio **O(P · H · log R)** con H = 100 TEN – TEN
Silencio Total Silencio **O(R log R + P · H · log R)** Silencio **O(R)**

Con `R, P ≤ 5 × 104` y `H = 100`, esto encaja fácilmente en los límites (~5 × 106 operaciones).

-...

## ⋅ Edge‐ Lista de verificación de caso <a name="edge-case-checklist"

1. **Puntos con y ю 100** – ningún rectángulo puede contenerlos; el resultado es 0.
2. **Cubos vacíos** – saltar rápidamente (sin búsqueda binaria).
3. **Muy grande `l` (≤ 109)** – encaja en la entrada firmada de 32 bits; sin desbordamiento.
4. **Multiple rectángulos de la misma altura** – manejados por clasificación.
5. **Pintura en el borde** – `x י= l ' y `y י= h` inclusive; búsqueda binaria inferior_bound correctamente los cuenta.

-...

## 📦 Full Implementations <a name="implementations"

A continuación se encuentran soluciones limpias y de producción en **Java, Python y C++**.
Los tres siguen los mismos pasos algorítmicos y usan expresiones específicas del lenguaje.

### 1. Java (Java 17)

``java
importar java.util*;

Solución de la clase pública {}
int[] countRectangles(int[][] rectángulos, int[][] points) {
// longitudes de cubo por altura (1.100)
Lista realizadaInteger confianza[] cubos = nuevo ArrayList[101];
para (int h = 0; h <= 100; h++) cubos [h] = nuevo ArrayList fiel();

para (int[] rect : rectángulos) {}
int l = rect[0], h = rect[1];
cubos[h].add(l);
}

/ / / ordenar cada cubo
para (Lista realizadaInteger confianza cubo : cubos) {}
si (!bucket.isEmpty()) Collections.sort(bucket);
}

int[] ans = nuevo int[points.length];
para (int i = 0; i) i++) {
int x = points[i][0];
int y = puntos[i][1];

si (y > 100) { // no rectángulo puede contener este punto
as[i] = 0;
continuar;
}

total = 0;
para (int h = y; h) = 100; h++) {
Listo:Integer monedas = cubos[h];
si (bucket.isEmpty()) continúan;

// búsqueda binaria: primer índice con l x
int idx = inferior Bound(bucket, x);
total += balde.size() - idx;
}
as[i] = total;
}
devolver los ans;
}

// clásica implementación de bajo límite
int private int lowerBound(Lista seleccionadaInteger título, int target) {
int lo = 0, hola = list.size(); // hola es exclusiva
mientras (lo cautivado) {
int mid = lo + (hi - lo) / 2;
si (list.get(mid)
lo = mitad + 1;
. ♫ ... {
Hola = mitad;
}
}
devolver lo;
}
}
`` `

-...

### 2. Python 3

``python
de la importación de bisect_left
de las colecciones importadas por defecto

Solución de clase:
def ConteoRectangles(self, rectángulos, puntos):
# longitudes de cubo por altura
cubos = defaultdict(list)
para l, h en rectángulos:
cubos[h].append(l)

# ordenar cada cubo #
para h en cubos:
cubos[h].sort()

ans = []
para x, y en puntos:
si y Ø 100: # ningún rectángulo puede contener este punto
ans.append(0)
continuar

total = 0
para h en rango(y, 101):
si no en cubos:
continuar
lst = cubos[h]
idx = bisect_left(lst, x) # first l  Quiere= x
total += len(lst) - idx
ans.append(total)

Retorno
`` `

-...

### 3. C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector implicadoConteo de títulosRectangles(vector seleccionadovector seleccionadoint implicancia reducida rectángulos,
vector realizador realizado con puntos reducidos {
// longitudes de cubo por altura (1.100)
vector realizador realizado en claves(101);
para (autorrecta : rectángulos) {}
int l = rect[0], h = rect[1];
cubos[h].push_back(l);
}

/ / / ordenar cada cubo
para (auto &bucket : cubos)
(bucket.begin(), balde.end());

vector significar uns
para (auto &pt : points) {
int x = pt[0], y = pt[1];
si (y > 100) { // imposible
ans.push_back(0);
continuar;
}

total = 0;
para (int h = y; h) = 100; ++h) {
const auto "bucket = cubos[h];
si (bucket.empty()) continúan;

// down_bound: primer índice con l x
auto = inferior_bound(bucket.begin(), balde.end(), x);
total += balde.end() - it;
}
as.push_back(total);
}
devolver los ans;
}
};
`` `

-...

■ **Por qué estos son profesionales listos* *
* Separación clara de las preocupaciones (paquete → tipo → consulta).
* Cada solución utiliza las operaciones de estructura de datos más rápidas disponibles: `Collections.sort`, `bisect_left`, `std::sort`.
* Evita la sobrecarga innecesaria (por ejemplo, la creación `ArrayList` por cubo sólo una vez).

-...

## 🧪 Testing the Solution = "testing"

``python
# Test de muestra en Python
sol = Solución()
rectángulos = [4],[5,5],[5,4]]
puntos = [[3,3],[5,5],[5,1],[2,6]]
print(sol.countRectangles(rectangles, points))
# → [2, 1, 2, 0]
`` `

**Edge-case samples* *

TENIDO ANTERIOR esperada
Silencio...
tención rectángulos = `[10, 10]] ' , puntos = `[10,10]
[[1,1], [2,2]] " , puntos = `[5,5] " Silencio
tención rectángulos = `[1000000000,100] ' , puntos = `[1,100] '
tención rectángulos = `[3,10] ' , puntos = `[4] ' Silencioso `0`

Ejecute las tres implementaciones contra el mismo generador de prueba aleatorio para confirmar la paridad.

-...

## 🎯 Interview‐Ready Tips #1 Nombre= "interview-tips"

Silencioso Por qué importa
Silencio...
tención **Explicar la observación clave** – “altura ≤ 100” – puntos de victoria anticipada. Muestra que puedes detectar restricciones que simplifican el problema. Silencio
Silencio ** Complejidades espaciales del tiempo del estado** antes de bucear en código. tención Los entrevistadores aman el análisis de complejidad concisa. Silencio
Silencio **Usar ayudantes de búsqueda binaria incorporados** (`bisect_left`, `std::lower_bound`, `Collections.binarySearch`). tención Ahorra tiempo, reduce fallos. Silencio
*antes* realizar trabajos pesados. Silencio Previene cheques O(1) innecesarios. Silencio
*Proof of correctness**: Mostrar que down_bound cuenta todos los rectángulos con " l "= x " * y " h "= y " . Silencio
Silencio **Mención del límite fijo de 100 alturas** como “arma secreta”. Silencio hace que su solución se destaque. Silencio
Silencio **Hablar sobre cómo manejarías las restricciones más grandes** (por ejemplo, si `h` no estuviera tapado). tención Muestra adaptabilidad. Silencio
Silencio **Mantenga el código limpio** – evite las micro-optimizaciones que hacen daño a la legibilidad. tención Los entrevistadores valoran el código de mantenimiento. Silencio

-...

##  tuya SEO‐Friendly Summary #2 name="seo-summary"

* Número de rectángulos que contienen cada punto*
- ** Idiomas**: Java, Python, C++
- ** algoritmo operativo**: cubo por altura (≤ 100), longitudes de clase, búsqueda binaria por consulta.
- **La complejidad del tiempo**: O(R log R + P · 100 · log R) – bien inferior a 5 × 106 operaciones para límites LeetCode.
- **La complejidad del espacio**: O(R).
- **Por qué es un gran problema de entrevista**: muestra la capacidad de explotar restricciones, utilizar búsqueda binaria, y razonar sobre geometría 2-D con estructuras de datos 1-D.

■ **Ready to ace your next data‐structure interview? * *
■ Maestro el truco de cubo y prepárate para explicar *por qué* un límite de 100 alturas es un cambiador de juego.

¡Feliz codificación, y buena suerte aterrizando ese trabajo! 🚀

-...

■ **Keywords**: LeetCode, número de conteo de rectángulos que contienen cada punto, entrevista Pregunta, Java, Python, C++, Algorithm, búsqueda binaria, Complejidad del tiempo, Complejidad del espacio, estructuras de datos, consejos de entrevista de trabajo.

-..