-...
Título: LeetCode 3488. Consultas más cercanas de igualdad de elementos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código de Solución

A continuación se ** tres implementaciones limpias y listas de producción** – una para cada uno de los idiomas de entrevista más populares.

■ Los tres usan el mismo tiempo de O(n), espacio de O(n) “dos pasos sobre una técnica de doble array”.
■ Son cortas, completamente comentadas, y han sido comprobadas unitariamente contra los casos de muestra.

Silencio Idioma Silencio Función Signature Silencio Código
Silencio----------------------
tención **Java** Silencioso `public List GarantizadoInteger confianza solveQueries(int[] nums, int[] queries)` Silencio > Haga clic para ampliar

``java
importar java.util*;

Solución de la clase pública {}

*
* Encuentra la distancia circular mínima a otro elemento igual para cada consulta.
*
* @param nums La matriz circular de enteros.
* consultas @param Índices cuyas respuestas necesitamos.
*Retorno Una lista de distancias mínimas (o -1 si no existe duplicado).
*/
public List Noms, int[] consultas {}
int n = nums.length;
// distancia[i] = distancia circular mínima de i a otro elemento igual
int[] dist = nuevo int[n];
Arrays.fill(dist, Integer. MAX_VALUE);

// lastSeen maps a value - confiar el último índice (en el doble traversal) donde apareció
Mapa seleccionadoInteger, Integer confiar lastSeen = nuevo HashMap garantizado();

// Traverse dos veces (direjado doble) para contabilizar la circularidad
para (int i = 0; i)
int val = nums[i % n];
int curIdx = i % n;

Integer prev = lastSeen.get(val);
si (prev != null) {
int prevIdx = prev % n;
int d = i - prev; // distancia a lo largo de la matriz doble
dist[curIdx] = Math.min(dist[curIdx], d);
dist[prevIdx] = Math.min(dist[prevIdx], d);
}
lastSeen.put(val, i);
}

Lista de resultadosInteger título = nuevo ArrayList implicado(queries.length);
para (int q : consultas) {
result.add(dist[q] >= n ? -1 : dist[q]); // if >= n, it means no duplicate
}
Resultado de retorno;
}
}
`` `

> >
Silencio **Python** Silencio `def solveQueries(nums: List[int], consultas: List[int]) - titulado List[int] < > > Silencio > > > Haga clic para ampliar

``python
de la importación Lista
de las colecciones importadas por defecto

def solveQueries(nums: List[int], queries: List[int] List[int]:
"
Devuelve la distancia circular mínima de cada índice queried a otro
índice que tiene el mismo valor. Si no existe tal índice, retorno -1.
"
n = len(nums)
INF = n + 5 # cualquier valor n será tratado como "no duplicado"
dist = [INF] * n # distancia mínima para cada posición
last_seen = {} # value - titulado último índice en traversal doble

# Traverse el array dos veces para modelar la circularidad
para i en rango(2 * n):
val = nums[i % n]
cur = i % n
si val en last_seen:
prev = last_seen[val]
d = i - prev # distancia positiva
dist[cur] = min(dist[cur], d)
dist[prev % n] = min(dist[prev % n], d)
last_seen[val] = i

# Construir respuestas para las consultas
volver [d si d ecto n otro -1 para d in dist[i] para mí en consultas]
`` `

> >
Silencio **C++** Silencio `vector efectuadoint títulos solveQueries(vector fielmente situado cerca de nums, vector implicados iguales queries)` Нелелилиниханиминениминиениханиханихиниханиеных. Haga clic para ampliar

``cpp
Incluido el título
#include ■unordered_map Conf
#include >

usando std namespace;

*
* @brief Encuentra distancia circular mínima a otro elemento igual para cada consulta.
*
* @param nums Conjunto circular de enteros.
* consultas @param Índices para los cuales necesitamos la respuesta.
* @return vector Distancias mínimas (o -1 si no existe duplicado).
*/
vector implicados en la resoluciónQueries(vector fieltro nums, vector implicados en modales) {}
int n = nums.size();
const int INF = n + 5; // any value n será tratado como "no duplicado"
vector asignadoint título dist(n, INF);

unordered_map detectint, int confianza lastSeen; // value - título último in doubled traversal

para (int i = 0; i) {}
int val = nums[i % n];
int cur = i % n;
aut it = lastSeen.find(val);
si (lo != lastSeen.end()) {
int prev = it- segundos;
int d = i - prev; // distancia positiva
dist[cur] = min(dist[cur], d);
dist[prev % n] = min(dist[prev % n], d);
}
lastSeen[val] = i;
}

vector significar uns
ans.reserve(queries.size());
para (int q : consultas) {
ans.push_back(dist[q] [q]] no ? dist[q] : -1);
}
devolver los ans;
}
`` `

> >

Los tres códigos:

Silencio Idioma Silencio Tiempo Complejidad Silencio
Silencio...
Silencio en Java**
TENIDO Python TENIDO **O(n)** ANTERIOR **O(n)**
TENIDO C++ TENIDO **O(n)** Silencio **O(n)**

----------------------------------------------------

## 2. Artículo del Blog

■ *Título*
■ *“Mastering LeetCode 3488: Closest Equal Element Queries – The Good, The Bad, and The Ugly”*

■ **Meta Descripción**
■ Aprenda una slick O(n) solución a LeetCode 3488, completa con Java, Python y código C++, fallos en el borde, consejos de entrevista, y cómo este problema puede conseguir un papel FAANG.

-...

## Tabla de contenidos
1. [Norma general](#problema vista previa)
2. [Por qué LeetCode 3488 es una Gem de Entrevista Oculta](#why-leetcode-3488-is-a-hidden-interview-gem)
3. [Aprobación: El Dos Pass Hashmap Trick] (#approach-the-two-pass-hashmap-trick)
4. [Detalles de implementación en Java, Python & C++](#implementation-details-in-java-python--c)
5. [Time & Space Complexity](#time--space-complexity)
6. [Common Edge Cases & Pitfalls](#common-edge-cases--pitfalls)
7. [La "Ugly" – Cosas que Meten Su Solución] (#the-ugly---things-that-up-your-solution)
8. [Interview Strategy: Turning the Problem into a Talk‐about-Project](#interview-strategy--turning-the-problem-into-a-talk-about-project)
9. [Conclusión > Siguientes pasos](#conclusión--siguiente-pasos)

-...

### Problema Resúmenes ## #### Nombre="problema-supervisión"

**Closest Equal Element Queries** (LeetCode 3488) te pide que tomes un array **circular** `nums` y, por cada índice `i` dado en `queries`, devuelva la distancia mínima *circular* a *otro* índice que contiene el valor *same* como `nums[i]`. Si `nums[i]` es único, devuelve `-1`.

¿Por qué es un problema de entrevistas? * *

Reason ← Explicación
Silencio----------
Silencio **Circularidad** Silencio Añade un giro que hace que los trucos estándar de dos puntos o de ventana deslizante parezcan sospechosos. Silencio
Silencio **Hash‐map heavy** Silencio Testa su comodidad con `Map/HashTable` – una estructura de datos básica en cada entrevista FAANG. Silencio
Silencio **Dos-pass elegancia** Silencio Showcases a *single pass over a doubled array* – un patrón que a menudo aparece en otros problemas de rayos circulares. Silencio
Silencio **Large constraints** Silencio `n` hasta 105 obliga a pensar en **O(n)** tiempo en lugar de fuerza bruta. Silencio

-...

### The Good, se hizo un nombre= "el bueno"

1. **Tiempo de luz, Espacio lineal** – El algoritmo elegido funciona en **O(n)** tiempo y **O(n)** espacio, manejando fácilmente las máximas limitaciones.
2. **Determinista y Simple** – Sólo se utilizan un mapa de hash y dos arrays enteros; no hay búsqueda binaria o DP multidimensional.
3. **Extensible** – El mismo patrón resuelve otros problemas como *El Duplicado Más cercano en un Array Circular*, *Shortest Distancia al Personaje*, o *Pasos mínimos de Array Circular*.

-...

### The Bad > ## The Bad >

Silencio ¿Qué puede pasar mal?
Silencio...
Silencio ** Distancia ininicializada** Silencio Failing to set `dist` to a value larger than `n` leads to wrong “no duplicate” checks. Use un centinela `INF = n + 5` (o `INT_MAX` si agregue una ``guarda' explícita. Silencio
Silencio **Single pass only** Silencio Revisar sólo la ocurrencia anterior inmediata extraña el camino circular *shortest* cuando los duplicados están muy separados. Silencio
Silencio **Off‐by-one en operaciones mod** tención Mis-calculating `prevIdx = prev % n` puede producir índices negativos. tención Siempre use `(prev % n + n) % n` si usted no está seguro de la señal. Silencio
Silencio ** Condiciones de devolución incorrectas** directamente incluso si `dist[i] == INF`. Silencio Compare contra `n` (la longitud de la matriz) para decidir “-1”. Silencio

-...

### The Ugly ## ## The Ugly ## ## ## The Ugly ## ## ## ## ### ## The Ugly ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ### ## #### ## # The Ugly # The Ugly # The Ugly âTMa Name=a Name='a name=the-the-the-the-the-the-the-the-the-the-the-ugly #################################################################################################### #The Ugly #The Ugly ##

**Putas de rendimiento en producción- Código de grado**

*Ataques de colisión HashMap*
Si estás en una plataforma que utiliza datos de prueba contradictorios, el estándar `HashMap` en Java o `unordered_map` en C++ puede degradar a O(n2).
**Fix**: Use `Int2IntOpenHashMap` (FastUtil) or `std::unordered_mapsectoint, int confianza` with a custom `hash` that mixes bits (e.g., `valor ^= value √≥ título 16;`).

*Memory Over‐head of Wrapper Objects*
En Java, `ArrayList seleccionadaInteger ` crea objetos boxeados `Integer`. Para las entradas a escala de entrevistas esto está bien, pero en un sistema de producción de alto volumen que utilizaría `int[]` para la velocidad.

**Ineficiente Modulus* *
Utilizar `%` dentro de un bucle ajustado puede ser caro en C++. Usar un pre-computado `n2 = 2 * n` y cambiar el índice manualmente:
``cpp
int idx = i < n ? i : i - n; / // alternativa rápida al i % n cuando yo
`` `

-...

### Implementación Caminata a través de un nombre= "implementation-details"

1. ** Estructuras de datos**
- `dist[i]` – distancia circular mínima del índice `i` a otro elemento igual.
- `últimoSeen` - mapa de hash desde un valor hasta el índice *último* (en el traversal doble) donde apareció ese valor.

2. **¿Por qué doblar el Array? #
Una matriz circular significa que después del índice `n‐1` se envuelve a `0`.
Al iterar a través de índices `0 ... 2*n-1` y utilizando `i % n`, **simular** que envuelven alrededor mientras todavía mantiene el traversal lineal.

3. ** Actualizaciones de distancia**
Cuando vemos un valor que ya se vio en el índice `prev`, la distancia **exacta a lo largo de la matriz doble** es `i - prev`.
Esta distancia es una distancia circular *valida* para *ambos* posiciones:
``text
i : ocurrencia actual
prev : ocurrencia anterior
d = i - prev (integer positivo)
`` `
Actualizar tanto `dist[cur]` como `dist[prev % n]` garantiza que cada par duplicado influye en la distancia mínima de ambos índices involucrados.

4. **Respuestas finales**
Cualquier `dist[i] ¢ n` significa que la distancia del par excede la longitud original del array - en otras palabras, no existió duplicado.
Sustitúyase esas entradas por " 1.

-...

### Tiempo & Complejidad Espacial > = "time-space-complexity"

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Silencio en Java**
TENIDO Python TENIDO **O(n)** ANTERIOR **O(n)**
TENIDO C++ TENIDO **O(n)** Silencio **O(n)**

El algoritmo realiza **2 × n** operaciones simples – perfectas para los límites de tiempo LeetCode.

-...

### Entrevista Consejos: "nombre="interview-tips"

TENIDO TENDIDO ANTERIOR Por qué importa
Silencio...
Silencio **Explicar la circularidad temprano** ¦ Shows usted entiende el matiz del problema antes de bucear en código. Silencio
Silencio **Mención del “gato doble”** Silencio Es un patrón comúnmente esperado para problemas de rayos circulares (por ejemplo, “Pasos mínimos en un Array circular”). Silencio
Silencio **Hablar sobre casos de borde** – ocurrencias individuales, array de longitud 1, duplicado en extremos – los entrevistadores les encanta ver que cubren. Silencio
Silencio ** Optimización espacial de la mención** – si el entrevistador es estricto sobre la memoria, explique cómo almacenar distancias en 'nums' mismo después de la pre-computación (en lugar). Silencio
Silencio **El uso de hash‐map de Highlight** – demuestra que puede mapear valores a índices de manera eficiente y manejar conjuntos de datos grandes. Silencio
TEN **Mostrar cómo probar** – escribir pruebas rápidas de unidad (o un método principal) para verificar contra las entradas de muestra. Silencio

-...

### Conclusión #1 nombre="conclusión"

*LeetCode 3488 – Closest Equal Element Queries* es una magnífica muestra de un simple truco de tiempo lineal** que maneja la circularidad, los duplicados y las distancias a la vez.

Al dominar los dos pasos sobre una matriz doble, puede responder el problema en el tiempo O(n) y el espacio O(n) – una solución que se siente limpia y poderosa.

Las implementaciones en **Java, Python y C+** demuestran que estás listo para cualquiera de las pilas de tecnología más importantes.

Tome esta solución, agregue un par de pruebas de unidad, y compartala en su GitHub. Ese es un punto de referencia sólido** para tu próxima entrevista de FAANG, porque podrás discutir:

1. *Por qué los arrays circulares son difíciles. *
2. *Cómo un simple hash‐map puede convertir un problema aparentemente cuadrático en tiempo lineal. *
3. *La importancia del cálculo de distancia cuidadoso y los valores centinela. *

Feliz codificación, y buena suerte en su viaje de entrevista! 🚀

-...

**Keywords para SEO:**
- LeetCode 3488
- Consultas más cercanas de igualdad de elementos
- distancia circular
- Solución O(n)
- algoritmo de mapa de hash
- Solución de entrevista de Java
- Python entrevista codificación
- C++ Problema de LeetCode
- Consejos de entrevista de FAANG
- tabla de datos

Siéntase libre de ajustar los encabezados de artículo o meta etiquetas para que coincida con su marca personal o con el papel específico que está apuntando.