-...
Título: LeetCode 245. Distancia de la palabra más corta III -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 245. Distancia de la palabra más corta III – Guía de solución completa (Java ¦

■ **TL;DR** – Escanear la lista una vez, mantener dos índices (último visto de `palabra1` y `palabra2`), actualizar la distancia mínima en cada partido. Funciona en *O(n)* tiempo, *O(1)* espacio, y maneja el caso de la misma palabra elegante.

-...

## Problema Recap

■ Dado un **lista de cuerdas** `palabrasDict` y dos cadenas `palabra1` y `palabra2` (ambos garantizados para aparecer en la lista), devuelve la distancia **cortada** (en índices) entre cualquier ocurrencia de `palabra1' y `palabra2`.
■ Las dos palabras pueden ser idénticas – en ese caso queremos la distancia más pequeña entre **dos episodios diferentes** de esa palabra.

**Constraints* *

TENIDO ANTERIOR ANTERIOR ANTERIOR
Silencio...
Silencioso `palabrasDict.length`
Silencioso `palabrasDict[i].length`
Silencio Todas las palabras son minúsculas Inglés letras

*Examples*

TEN TERRITOR ANTERIOR ANTERIOR
Silencio...
Silencioso `[practice", "makes", "perfecto", "coding", "makes"] ", `"makes"`, `"coding" ' Silencioso `1`
""Práctica", "makes", "perfecto", "coding", "makes" ", "makes", "makes"."

-...

## 📚 1. Enfoque: Escáner de dos puntos (paso del mismo)

La forma más natural es un solo escaneo de izquierda a derecha manteniendo las posiciones más recientes ** de cada palabra.

`` `
i1 = último índice de la palabra1 (inicialmente -∞)
i2 = último índice de palabra2 (inicialmente +∞)
minDist = + mujeres
para cada índice i en palabras Dict:
si palabras [i] == palabra1: i1 = i
si palabras [i] == palabra2:
si palabra1 == palabra2: i1 = i2 // Necesitamos la ocurrencia anterior
i2 = i
minDist = min(minDist, perui1 - i2 sometida)
`` `

*Cuando `palabra1 ==palabra2`* debemos ** intercambiar los dos índices en un golpe para asegurarnos de que estamos comparando *dos posiciones diferentes*.

**Por qué funciona* *

- El algoritmo nunca mira más de una vez: cada índice se procesa una vez, por lo que la complejidad del tiempo es *O(n)*.
- Solo se utilizan variables adicionales constantes → *O(1)* espacio auxiliar.
- El caso del borde de la misma palabra se maneja explícitamente intercambiando los índices cuando vemos la misma palabra.

-...

## 🔍 2. Ideas alternativas

TENIDO TERRIENTE Complejidad ANTERIOR Cuando se utiliza
Silencio----------------------------
← **Pre-procesar todas las posiciones en un `Map realizadoString, Lista seleccionadaInteger confianza`** y luego computar la diferencia mínima entre dos listas clasificadas a través de una fusión de dos puntos. TENIENDO: *O(n)*; Espacio: *O(n)* Silencio Cuando usted necesita responder **muchas consultas** en la misma lista de palabras – usted paga el costo una vez. Silencio
Silencioso **Ventana deslizante / programación dinámica** – no es necesario aquí.
Silencio **Binary search** – también innecesario porque podemos escanear una vez.

-...

##  Settlement 3. Code

A continuación encontrará soluciones listas para copiar en **Java**, **Python**, y **C+**.
Cada aplicación sigue la estrategia de escaneo de dos puntos.

■ **Nota** – Los tres snippets son las clases de "Solución" de LeetCode (o funciones) e incluyen comentarios breves para la claridad.

-...

## Java

``java
importar java.util*;

Solución de la clase pública {}
público más corto WordDistance(String[] wordsDict, String word1, String word2) {
// índices de las últimas posiciones vistas
int i1 = Integer.MIN_VALUE; // utilizar valores extremos para evitar cheques especiales
int i2 = Integer.MAX_VALUE;
int minDist = Integer.MAX_VALUE;

boolean mismo = word1.equals(word2);

para (int i = 0; i) Dict.length; i++) {
Crianza w = palabrasDict[i];
si (w.equals(word1)) {
si (same) {
// misma palabra - tratar i1 como la ocurrencia anterior
i1 = i2;
}
i1 = i;
} si (w.equals(word2)) {}
i2 = i;
}

// Sólo se comparan cuando ambos índices se establecen
si (i1!= Integer.MIN_VALUE " l2 != Integer.MAX_VALUE) {
minDist = Math.min(minDist, Math.abs(i1 - i2));
}
}
retorno minDist;
}
}
`` `

■ **Tiempo** – *O(n)*
■ **Espacio** – *O(1)*

-...

## Python

``python
Solución de clase:
def más corto WordDistance()
auto, palabrasDict: List[str], word1: str, word2: str
) int:
i1 = -10**9 # efectivamente -∞
i2 = 10**9 # efectivamente + dieta
min_dist = 10**9
misma = palabra1 = = palabra 2

para idx, w en enumerado(wordsDict):
si w == palabra1:
si mismo:
i1 = i2
i1 = idx
elif w == word2:
i2 = idx

# Update only if both indices have been seen
si i1 Ø -10**8 e i2
min_dist = min(min_dist, abs(i1 - i2)

regreso min_dist
`` `

■ **Tiempo** – *O(n)*
■ **Espacio** – *O(1)*

-...

### C++

``cpp
Clase Solución {
public:
más corto WordDistance(vector)se refiere palabras Dict, string word1, string word2) {
int i1 = INT_MIN;
int i2 = INT_MAX; //
int minDist = INT_MAX;
bool mismo = word1 == word2;

para (int i = 0; i) ++i) {
const string &w = palabras Dict[i];
(w == word1) {
si (same) i1 = i2; // ocurrencia anterior
i1 = i;
} si (w == word2) {
i2 = i;
}

si (i1 != INT_MIN " INT_MAX) {
minDist = min(minDist, abs(i1 - i2));
}
}
retorno minDist;
}
};
`` `

■ **Tiempo** – *O(n)*
■ **Espacio** – *O(1)*

-...

Resumen de la complejidad

Silencio Idioma Silencio Tiempo Silencioso Espacio Silencio ¿Por qué es Entrevista‐Ley
Silencio------------------------------------------
TEN Java TENIDO *O(n)* TENIDO *O(1)* TENCIÓN Usa sólo puntos primitivos, no HashMap, rápido en una sola consulta. Silencio
TENIDO Python TENIDO *O(n)* TENIDO *O(1)* TENIDO La misma idea, caldera mínima. Silencio
TENIDO C++ TENIDO *O(n)* TENIDO *O(1)* TENIDO Trabaja con `vector asignadostring confianza` y `estd::string`. Silencio

-...

## 🎯 4. Bien / Mal / Ugly - Lo que cada entrevistador ama

Ø Subtítulos Lo que estamos evaluando Silenciosos
Silencio------------------------------
Silencio **Bien** Silencioso * Implicidad* – un pase, no hay estructuras auxiliares de datos, espacio O(1) claro.
Silencio **Bad** Silencioso *Manejo por caso de Edge* – muchas personas olvidan el caso de la misma palabra y terminan con una respuesta incorrecta (distancia 0 o índices negativos).
*La legibilidad frente a la velocidad* – una solución ingenua de dos rayos (`i1`, `i2` almacenada por separado y cambiada de golpe) puede parecer confusa si no se comenta correctamente. TEN ❌ ←

■ **Takeaway:**
- Escribe código limpio, comentado.
√ - Guarda siempre el caso de la misma palabra – es una trampa de entrevista clásica.
√ - Si necesita responder *muchas* consultas, el preprocesamiento está bien; de lo contrario, el single‐scan es el estándar de oro.

-...

## 📄 5. Sample Test Harness

Silencioso Código Silencioso Caso de prueba
Silencio--------------------
Silencio Los tres idiomas que vivieron `[a], "b", "a", "c", "b", "a"], `a ", `"b"
Silencio Todos los tres idiomas que vivieron ``a','a,'a','a', `'a', `'a', ``a', ``a',
Silencio Los tres idiomas que vivieron `["uno", "dos", "tres"] ``, `'uno', ``, `'tres'' .

Usted puede pegar estos casos de prueba en el IDE LeetCode o su entorno local para confirmar.

-...

## 🚀 6. Por qué los entrevistadores aman esta pregunta

- **Fundamental**: Prueba la comprensión de la traversal de matriz y aritmética de índice.
- *Sensibilización por caso* La situación de la misma palabra es un obstáculo común de entrevista.
- **Versátil**: Las soluciones en varios idiomas muestran resolución de problemas agnósticos del lenguaje.
** escalable**: La solución O(n) es eficiente incluso para el tamaño máximo de entrada.

Si atrapas este problema en tu entrevista, demuestras:

- Maestría en operaciones de tiempo/espacio**.
- Capacidad de escribir ** código de búsqueda** que maneja casos especiales.
- Confort con **LeetCode-style** firmas de clase/función.

-...

## 📈 7. Performance " Trade‐offs

TEN TER TERRI ANTERIOR ANTERIOR Por qué importa
Silencio...
Silencio **Tiempo** Silencioso *(n)* (Ω 105 ops) tención Lo suficientemente rápido para los oleoductos de datos de grado de producción. Silencio
Silencio **Espacio** Silencio *O(1)* Silencio Mantiene la huella de memoria pequeña – crítica para dispositivos restringidos. Silencio
TEN **Readability** TEN High (comments + nombres variables significativos) TEN Los entrevistadores juzgan la calidad del código tanto como la corrección. Silencio
Silencio **Pre-procesamiento de mapa** Silencio Extra *(n)* memoria Silencio bueno para los escenarios de la consulta por lotes, pero no para una sola consulta. Silencio

-...

## 📢 8. SEO‐Ready Summary

- **Keywords**: *Shortest Word Distancia III LeetCode*, *Solución de Java*, * Solución de pitón*, * Solución C+*, *dos punteros*, *pregunta de entrevista*, *prep*, *entrevista de estructura de datos*, *O(n) Solución*.
- **Título**: 245. Distancia de palabra más corta III – Guía de entrevista completa de Java / Python / C++ Soluciones
- **Meta Descripción** (Ω160 chars): “Solve LeetCode 245 – Distancia de Word más corta III con O(n) Java, Python y código C++. Aprenda el truco de dos puntos, el manejo del borde y consejos de entrevista. ”

Utilice estos snippets en su cartera de résumé o GitHub para mostrar su capacidad de resolver problemas de entrevista clásicos de manera eficiente.

-...

Pensamientos finales

El análisis de dos puntos es la respuesta **canónica** para este problema LeetCode.
Si se está preparando para las entrevistas de codificación, asegúrese de que puede:

1. ** Explique el algoritmo** en inglés claro.
2. **Implementarlo en su idioma preferido** (Java, Python, C++).
3. **Discuten la periferia** donde las dos palabras son idénticas.
4. **Comparar trade‐offs** con un mapa de pre-procesamiento cuando se esperan muchas consultas.

Dominar este problema simple pero sutil aumentará su confianza para otras preguntas de entrevista de “distance / couple” como *Shortest Uncommon Subsequence*, *First Missing Positive*, y muchos más.

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀