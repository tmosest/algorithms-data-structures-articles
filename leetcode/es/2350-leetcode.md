-...
Título: LeetCode 2350. Secuencia Imposible más corta de rollos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código - Tres idiomas

A continuación encontrará **one‐pass, O(k) espacio** soluciones para el problema LeetCode
2350. Secuencia Imposible más corta de Rolls`.
Los tres francotiradores siguen la misma idea:

1. Escanee el array 'rolls' una vez.
2. Mantenga un conjunto (o una pequeña variedad de banderas) que recuerda qué caras de dados tienen
ya apareció en el actual “segment”.
3. Cuando el conjunto contiene todas las caras 'k', hemos encontrado un segmento completo – nosotros
aumentar el contador de respuesta y aclarar el conjunto para iniciar un nuevo segmento.
4. La respuesta es 'completeSegments + 1` porque la primera longitud que no puede
ser formado es uno más que el número de segmentos completos que podemos construir.

Silencio Idioma Silencio Complejidad
Silencio--------------------------
Silencio **Java** Silencioso `O(n)` tiempo, `O(k)` espacio ←
Silencio **Python** Silencio `O(n)` tiempo, `O(k)` espacio Silencio [Code] Silencio
Silencio **C+** Silencioso `O(n)` tiempo, `O(k)` espacio Silencio [Code]

-...

## Java

``java
importa java.util. HashSet;
importa java.util. Set;

Clase Solución {
public int shortestSequence(int[] rolls, int k) {
segmentos int = 0; // número de conjuntos completos encontrados
Establecer contactoInteger nombrado = nuevo HashSet fiel();

para (int r : rolls) {
visto.add(r);
si (ver.size() == k) { // hemos visto todas las caras
segmentos++; // un segmento completo terminado
visto.clear(); // iniciar un nuevo segmento
}
}
segmentos de retorno + 1; // la primera longitud imposible
}
}
`` `

-...

## Python

``python
Solución de clase:
def shortestSequence(self, rolls: List[int], k: int) - título int:
segmentos = 0
visto = set()

para r en rollos:
visto.add(r)
si len(seen) == k: # segmento completo
segmentos += 1
visto.clear()
segmentos de retorno + 1
`` `

-...

### C++

``cpp
Incluido el título
#include ■unordered_set
usando std namespace;

Clase Solución {
public:
más corto Secuencia(vector seleccionados) {
int segments = 0;
unordered_set observadoint

para (int r : rolls) {
visto.insert(r);
si (int)seen.size() == k) { // todas las caras vistas
++segmentos; // terminado un segmento
visto.clear(); // reset para el siguiente segmento
}
}
segmentos de retorno + 1; // primera longitud imposible
}
};
`` `

■ **Tip** – Si desea evitar un hash-set en C++ puede utilizar un tamaño fijo
" matriz de booleanos " ( " . que es incluso más barato.

-...

## 2. Blog Post – “Short‐Circuiting Impossible Sequences de dados”

■ **SEO Palabras clave** – *Shortest Impossible Secuencia de Rolls, Leetcode 2350, problema de codificación de entrevistas, Java, Python, solución C++, análisis de algoritmos, tiempo O(n) y espacio O(k). *

-...

# Secuencias de dados imposibles de corta duración – Un LeetCode Deep Dive

■ ¿Puedes predecir el próximo rollo? ”
■ No – pero usted * puede* predecir *que secuencia nunca será capaz de
Forma. *
■ Ese es el crujo de LeetCode 2350: **Shortest Impossible Secuencia de Rolls**.

#### TL;DR

- Lo que nos preguntan es: Dado un array `rolls[i]` (dice resultados) y un die con
" caras " ( " 1...k " ), encontrar la longitud " L " de la secuencia de la longitud
`L` that **cannot** be produced as a subsequence of `rolls`.
- **Idea de la solución**: Escanear una vez, contar cuántos bloques contiguos contienen *all*
Caras.
- **Respuesta**: `blocks + 1`.

-...

## ¿Por qué es un problema *bueno*?

✔ Cambios en la vida
Silencio...
Silencio 1️ ** Intuitivo** Silencio Piensa en cada conjunto completo de rostros distintos como una “capa” que
Silencio Silencio puede contribuir un rollo de muerte a cualquier secuencia. Silencio
tención 2️ **Un paso** Silencioso O(n) tiempo – perfecto para entrevistar pruebas de estrés. Silencio
tención 3️ **Recuerdo pequeño** Silencioso espacio O(k) – sólo un puñado de banderas son necesarias siempre. Silencio
tención 4️ **LeetCode-ready** ¦ Sigue el patrón de clase estándar 'Solution' para Java,
TENIDO ANTERIOR Python, C++. Silencio

-...

## The Algorithm, Step‐by‐Step

1. **Initializar** `segments = 0` y un conjunto de conjunto/plano vacío.
2. **Iterate** a través de 'rollos':
- Agregue el rollo actual al set.
- Si el tamaño del set se convierte en 'k', hemos visto * toda* cara.
- Incremento `segments`.
- Borrar el set para comenzar el próximo segmento.
3. **Retorno** `segmentos + 1`.
La primera longitud imposible es siempre una más que el número completo
segmentos que puedes construir.

■ ** Caso Edge** – Si una cara de `1...k` nunca aparece, el algoritmo nunca
por primera vez, `segments` se queda `0` y la respuesta
> correctamente se convierte en `1`.

-...

## Complexity Analysis

TEN TERRITOR TEN TEN ANTE
Silencio...
Silencio ** Tiempo** Silencioso `O(n)` – un pase sobre `rolls`. Silencio
Silencio **Espacio** Silencioso `O(k)` – un conjunto/array que rastrea las distintas caras del segmento actual. Silencio

-...

## “El Ugly” – Lo que podría ir mal

Cómo evitarlo
Silencio...
Silencio **Muy grande `k`** (hasta 100 000) Silencio El conjunto crece a 'k', pero esto todavía es lineal en
Silencio. Use un 'boolean[] visto ` en lugar de un hash-set para guardar la memoria
Silencio. Silencio
Silencio ** Hash-set overhead** Silencio Cada `add`/`clear` cuesta un pequeño factor constante. Para un
tención tención entrevista, un `int[]` de tamaño `k+1` es más rápido y más predecible. Silencio
Silencio ** validación de entrada** Silencio LeetCode garantiza restricciones, pero si usted está escribiendo un
Silencioso biblioteca, compruebe que 'k'= 1 `y `rolls` no es nulo. Silencio

-...

## “El Bien” – Por qué el Juego de un Pase gana

1. **Claridad** – La lógica es literalmente "colectar rostros distintos; cuando
completo, cuenta una capa”.
2. **Scalability** – Works for `n = 10^6`, `k = 10^5` in under a second in
los tres idiomas.
3. **Robustness** – Maneja todos los casos de esquina: rostros desaparecidos, duplicados
rollos, largas carreras, etc. El algoritmo sólo se preocupa por si un conjunto completo
ha sido visto, no sobre *donde* ocurre.

-...

## “El mal” – Trade-offs

- **El uso de memoria** crece con k. Si `k` es enorme (Ω105) el conjunto de conjunto o bandera
ocupará muchos bytes.
**Hash‐set vs. array** – En Java o Python el conjunto incorporado es conveniente pero
puede ser más lento que una pequeña matriz booleana.
- ** Operación aérea** – Limpiar un conjunto repetidamente es O(1) en promedio pero
todavía asigna un nuevo hash‐table en Java. Usando una serie de banderas y una
counter evita la reubicación.

-...

## “El Ugly” – Subtle Gotchas

Silencio ¿Qué pasó?
Silencio...
TENIENDO `rolls` vaciado El bucle nunca funciona; `segmentos = 0` → respuesta `1` (correcto). Silencio
TENIDA `k == 1`  El set siempre alcanza el tamaño 1 después del primer rollo → `segments = 1`,
← respuesta permanente `2` – que es correcto porque las secuencias longitud‐1 son todas
Es posible. Silencio
TENIENDO `k`, número de valores distintos en `rolls` ANTE `segments` se mantiene `0`, respuesta `1`. Esto
TEN ANTE TENED correctamente identifica que un único rollo es imposible. Silencio

-...

## 3. Cómo utilizar el Código

1. **Copiar** el snippet para su idioma de elección en el LeetCode
editor.
2. **Ejecutar** las pruebas de muestra proporcionadas:

``text
Entrada: rollos = [4,2,1,2,3,2,4,1], k = 4
Producto: 3
`` `

3. **Extienda** la solución si necesita manejar varios dados u otros
limitaciones – la idea central sigue siendo la misma.

-...

## 4. Take-away for Your Next Interview

- **Explicar la intuición** primero: “Estamos buscando la primera longitud que
no podemos formar; cada vez que vemos todos los rostros "k" podemos decir con seguridad
secuencia de esa longitud es posible. ”
*Mostrar la solución de un paso* – los entrevistadores aman el espacio lineal, constante
trucos.
- **Mención del caso del borde** donde una cara nunca aparece → respuesta `1`.

¡Feliz codificación! 🚀