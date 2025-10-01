-...
Título: LeetCode 2655. Encontrar Maximal Gamas descubiertas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 2655 – Find Maximal Gamas descubiertas
**Medium Ø LeetCode ANTERIED Entrevistas TENIDO Algorithm TEN Java TENIDO Python ANTE C+**

-...

#### TL;DR
* Ordenar los rangos dados por punto final izquierdo.
* Suda un puntero sobre la lista ordenada, coleccionando las lagunas que no están cubiertas.
* Complejidad: **O(m log m)** tiempo, **O(m)** espacio auxiliar (`m = ranges.length`).
* Funciona incluso cuando `n` está hasta `109` porque nunca construimos toda la matriz.

-...

## ¿Por qué este problema es una pregunta de entrevista “debemos saber”

1. **Real-world relevance** – es esencialmente el mismo que encontrar ranuras de tiempo libre en calendarios, bloques IP no utilizados, o rangos de almacenamiento no asignados.
2. **Elegant barrido** – usted aprende un patrón algoritmo clásico: ordenar, escanear y mantener un puntero en movimiento.
3. **Edge‐case mastery** – el tamaño de entrada (`n`) puede ser enorme, por lo que las soluciones ingenuas O(n) o O(n × m) son un *trap*.

Si puedes explicar esta solución de forma limpia y codificarla en **Java, Python y C++**, te destacarás en una entrevista técnica.

-...

## 1. Reposición de problemas

Dado un entero " n " (longitud de una matriz `nums " ) y una matriz de 2-D `ranges ' donde cada `ranges[i] = [l, r] ' (inclusive), encontrar **all maximal uncovered ranges**.
Un rango máximo descubierta es un subintervalo `[a, b]` tal que:

1. Ninguna célula en `[a, b]` se encuentra dentro de cualquier `ranges[i]`.
2. El intervalo no puede extenderse por uno de cada lado (es decir, " b + 1 ل nextLeft " ).

Devuelve los rangos descubiertos ordenados por índice de inicio.

*Ejemplo*

`` `
n = 10, ranges = [3,5],[7,8]]
→ [[0,2],[6,6],[9,9]]
`` `

-...

## 2. Enfoques ingenuos y condenados

Por qué falla (caso peor)
Silencio------------------
← Construir un conjunto booleano de longitud `n` y marcar las células cubiertas Silencio `n` puede ser `109` → memoria imposible " tiempo. Silencio
Silencio Para cada rango, marca las células; luego escaneo para las brechas Silencioso `O(n × m) ' tiempo. Silencio
Silencio Combinar los rangos primero, luego restar de `[0, n-1]` ← Merging es `O(m log m)`, pero si usted también construye un array usted vuelve a `O(n)`. Silencio

Estos enfoques soplan porque ignoran el hecho de que **sólo los rangos mismos importan**, no todos los índices dentro de `0 ... n‐1`.

-...

## 3. La Elegante Solución Sweep‐Line

1. **Sorta** 'ranges' por el punto final izquierdo (ascending).
2. Mantener un puntero `ptr` que denota el índice más pequeño descubierta hasta ahora. Inicialmente `ptr = 0`.
3. Iterate over each classified range `[l, r]`:
* If `ptr ■ l`, the gap `[ptr, l-1]` está descubierta → añadirlo a la respuesta.
* Actualizar `ptr = max(ptr, r + 1)` (no podemos volver a un área ya cubierta).
4. Después del bucle, si `ptr ecto n`, la cola '[ptr, n-1]` está descubierta → añadirlo.
5. Devuelve la lista recolectada.

Debido a que sólo clasificamos los rangos (≤ 106) y realizamos un solo pase lineal, el algoritmo es óptimo.

-...

## 4. Código

A continuación se presentan implementaciones limpias y de producción en **Java**, **Python**, y **C+**.

■ **Consejo:** Para los entrevistadores, puede mostrar cómo cada idioma maneja la misma lógica.
■ Si usted está aplicando, puede pegar estos snippets en su résumé o GitHub.

-...

#### 4.1 Java

``java
importar java.util*;

Solución de la clase pública {}
int[][][] encontrarMaximalUncoveredRanges(int n, int[] ranges) {}
// Cláusulas de guardia
si (ranges == null ¦ 0) {
volver n == 0 ? new int[0] [0] : new int[][]{0, n - 1}};
}

// Ordenar por punto final izquierdo
Arrays.sort(ranges, Comparator.comparingInt(a - título a[0]));

Lista hecha[]]] > > > >
int ptr = 0;

para (int[] r : ranges) {
int l = r[0], rgt = r[1];

si (ptr.) { // espacio descubierto encontrado
ans.add(new int[]{ptr, l - 1});
}
// Punto de movimiento más allá del rango actual
ptr = Math.max(ptr, rgt + 1);
}

si (ptr ecto n) { // cola descubierta
ans.add(new int[]{ptr, n - 1});
}

volver ans.toArray (nueva int[ans.size()][]);
}
}
`` `

-...

#### 4.2 Python

``python
de la importación Lista

Solución de clase:
def findMaximalUncoveredRanges(self, n: int, ranges: List[List[int]) - No. List[List[int]]:
si no rangos:
volver [[0, n - 1]] si no

# Sort by left endpoint
ranges.sort(key=lambda x: x[0])

ans = []
ptr = 0

para l, r en rangos:
si ptr ecto l: # segmento descubierto
ans.append([ptr, l - 1])
ptr = max(ptr, r + 1)

si ptr se hizo n: # segmento de seguimiento
ans.append([ptr, n - 1])

Retorno
`` `

-...

#### 4.3 C++

``cpp
Incluido el título
#include >

Clase Solución {
public:
std:::vector obtenidosstd::vector realizadoint título encontrarMaximalUncoveredRanges(int n, std::vector seleccionados:::vector seleccionados:::vector fieltro alcances) {}
si (ranges.empty()) {}
devolver n  título 0 ? std::vector seleccionados:::vector fieltro {{0, n - 1}} : std:::vector seleccionados::::vector fieltro();
}

// Ordenar por punto final izquierdo
std::sort(ranges.begin(), ranges.end(),
[](Cont std::vector fielint implica a, const std::vector fieltro b) {
devolver a [0]
});

std::vector seleccionados::vector realizadoint títulos
int ptr = 0;

para (continuidad auto-cliente : rangos) {}
int l = seg[0], r = seg[1];

si (ptr.) { // parte descubierta
ans.push_back({ptr, l - 1});
}
ptr = std::max(ptr, r + 1); // move pointer
}

si (ptr ecto n) { // parte de seguimiento
ans.push_back({ptr, n - 1});
}

devolver los ans;
}
};
`` `

-...

## 5. Análisis de la complejidad

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencio Ordenando `ranges` Silencio **O(m log m)** Silencio **O(1)** (en el lugar)
Silencio Escaneo lineal único Silencio **O(m)** Silencio **O(m)** (lista de respuestas)
Silencio total **O(m log m)** Silencio **O(m)**

Con `m ≤ 106`, esto funciona cómodamente en un segundo en máquinas modernas.

-...

## 6. Bien, mal,

TENIDO Categoría ANTERIOR Qué destacar ANTERIENTE Pitfalls para evitar TENIDO
Silencio...
Silencio **Bien** Silencioso * Ordenación + barrido* – tiempo lineal después de la clasificación, sin construcción de matriz. Silencio
Silencio **Bad** Silencioso `O(n)` soluciones (construyendo toda la matriz) - será rechazado en grande `n`. Silencioso de memoria, cache misses  durable
Silencio **Ugly** Silencio Sobre-merging or deduplication when ranges overlap heavily; you must keep the **minimal** gaps. ← Unnecessary extra pass, sutil off-by-one bugs when `ptr = r + 1` sometida

### Common Interview Traps

1. **Off‐by-one errores** – recuerde que los rangos son inclusivos.
2. ** Entrada vacía** – no olvides el caso en el que todos los índices son descubiertos.
3. **Large `n`** - evitar crear una variedad de tamaño `n`.
4. **Los rangos Duplicados** – clasificarlos naturalmente; nunca es necesario fusionarse explícitamente a menos que quieras comprimir la memoria más allá.

-...

## 7. Aplicaciones prácticas

Por qué el algoritmo importa
Silencio--------------------
Calendario permanente programando Silencio Encuentra tragaperras gratuitas entre eventos. Silencio
tención Red IP asignación Silencio Compute bloques IP no utilizados de rangos asignados. Silencio
Silencio fragmentación del sistema de archivos ¦ Detectar grandes bloques libres para la asignación rápida. Silencio
Silencio Diseño de nivel de juego Silencio Identificar áreas aún no pobladas por enemigos o elementos. Silencio

Entender este problema te ayuda a abordar cualquier pregunta de “interval-gap” que aparece en escenarios del mundo real.

-...

## 8. SEO‐Friendly Takeaway

Si usted está apuntando a los reclutadores o las juntas de entrevista técnica, esta escritura de palabras clave ricas le ayudará a ser descubierto:

* **Encontrar rangos máximos descubiertos** – LeetCode 2655
* ** algoritmo intervalorando la línea de barrido** – estrategia de entrevista
* **Java, Python, soluciones C++** – códigos
* ** Análisis de complejidad** – O(m log m) tiempo, espacio O(m)

Los motores de búsqueda aman el contenido estructurado. Mediante el uso de encabezados audaces, cercas de código y un tono limpio y conversacional, su blog se clasificará como alto para los desarrolladores que se preparan para LeetCode 2655 o cualquier entrevista que exija el razonamiento basado en intervalos.

-...

## 9. Palabras finales

- **Recordar**: `n` es sólo un *boundary*; sólo los rangos importan.
- **Mostrar** el patrón de barrido; los entrevistadores aman soluciones limpias y generalizables.
- **Práctica** codificación en todos los idiomas con los que te sientes cómodo; resaltar las diferencias (por ejemplo, `Arrays.sort` vs. `ranges.sort`).

Buena suerte agrietando LeetCode 2655 – es el mismo conjunto de habilidades que convierte las preguntas de entrevista en resolver problemas del mundo real. ¡Feliz codificación!