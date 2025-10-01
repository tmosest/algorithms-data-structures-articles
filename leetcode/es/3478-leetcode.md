-...
Título: LeetCode 3478. Elija elementos K Con Suma Máxima -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recaptación de problemas

**LeetCode 3478 – Elige K Elementos Con Suma Máxima**

* Entrada*
`nums1`, `nums2` – dos arrays enteros de longitud `n `
`k` - un entero positivo (`1 ≤ k ≤ n`)

*Task*
Por cada índice:

1. Encontrar todos los índices " j " de tal manera que `nums1[j] ' .
2. De esos índices eligen ** en la mayoría** valores de `nums2[j]`. que da la suma máxima posible.
3. Guarda esa suma en `respuesta[i]`.

Devuelve la matriz `respuesta`.

*Constraints*
`1 ≤ n ≤ 105`
`1 ≤ nums1[i], nums2[i] ≤ 106`

La solución clásica utiliza un **sort + min-heap** (caída de prioridad) y funciona en `O(n log n)` tiempo y `O(k)` espacio extra.

A continuación encontrará implementaciones limpias y bien agregadas en **Java, Python y C+**.

-...

## 2. Core Idea

1. ** Orden por `nums1`.**
Cuando el array se ordena cada vez más, cada elemento que ya hemos procesado tiene un valor `nums1` *strictly menor* que el actual.
El único matiz: los duplicados no deben considerarse “maller”. Lo resolvemos agrupando valores iguales.

2. **Mantenga un min-heap del mejor `k` `nums2` visto hasta ahora. #
- El montón almacena los valores *k más grandes* `nums2` encontrados.
- `sum` mantiene el total actual del contenido del montón.
- Cada vez que se inserta un nuevo valor de `nums2`, lo empujamos; si el monto crece más allá de `k`, volamos el valor más pequeño y lo restamos de `sum`.
Así, la suma es siempre la suma máxima de los elementos más `k ' que provienen de índices con un `nums1 ' más pequeño.

3. **Respuesta por un grupo de iguales `nums1`**
Para cada índice en el grupo asignamos el actual `sum`.
Sólo después de todas las respuestas para el grupo están establecidas, añadimos los valores del grupo `nums2` al montón (así que no se cuentan para sí mismos).

-...

## 3. Aplicación

### 3.1 Java

``java
importar java.util*;

*
* LeetCode 3478 – Elige K Elementos Con Suma Máxima
*/
Clase Solución {
public long[] findMaxSum(int[] nums1, int[] nums2, int k) {
int n = nums1.length;
long[] answer = new long[n];

// par cada elemento con su índice original
int[][] pares = nuevo int[n][2];
para (int i = 0; i)
pares[i][0] = nums1[i]; // valor para clasificar
pares[i][1] = i; // índice original
}

// ordenar por nums1 ascendente
Arrays.sort(pairs, Comparator.comparingInt(a - título a[0]));

// min-heap para los valores nums2 más grandes vistos hasta ahora
Prioridad Búsquedas realizadasInteger confianza heap = nueva PrioridadQueue贸 conveniente();
larga corriente Sum = 0;

int i = 0;
mientras (i
int j = i;
// encontrar el final del grupo actual (todas las nums iguales1)
[j] == pares [i] [0]) j++;

// 1 / / Respuesta para cada índice en el grupo utiliza la corriente Sum
para (int t = i; t) {}
respuesta[pairs[t][1]] = currentSum;
}

// 2️ ahora añadir los valores nums2 de este grupo al montón
para (int t = i; t) {}
int idx = pares[t][1];
int val = nums2[idx];
heap.offer(val);
corriente Sum += val;

// mantener sólo los valores más grandes k
si (heap.size() {}
corriente Sum -= heap.poll();
}
}

i = j; // pasar al siguiente grupo
}

respuesta de retorno;
}
}
`` `

#### 3.2 Python

``python
de heapq importación heappush, heappop
de la importación Lista

Solución de clase:
def findMaxSum(self, nums1: List[int], nums2: List[int], k: int List[int]:
n = len(nums1)
respuesta = [0]

# valor par con índice original
pares = ordenados ([(val, idx) para idx, val en enumerate(nums1)], key=lambda x: x[0])

* # min‐heap of best k nums2 values
current_sum = 0
I = 0
mientras que yo no
J = i
mientras j  observado n y pares [j] [0] == pares[i][0]:
j += 1

# Respuesta para este grupo
para t en rango(i, j):
respuesta[pairs[t][1] = current_sum

# Add group's nums2 to the heap
para t en rango(i, j):
idx = pares[t] [1]
val = nums2[idx]
heappush(heap, val)
current_sum += val
si len(heap)
current_sum -= heappop(heap)

I = j

respuesta
`` `

### 3.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector iniciado largo contacto encontrarMaxSum(vector identificadoint círculo nums1, vector identificadoint círculo nums2, int k) {
int n = nums1.size();
vector realizado largamente uns(n, 0);

// par {nums1 valor, índice original}
vector significado(n);
para (int i = 0; i) i; ++i) pares [i] = {nums1[i], i};

sort(pairs.begin(), pairs.end(), [](cont auto cosecha a, const auto cosecha b){
devolver a.primero
});

priority_queue obtenidosint, vector asignadoint minHeap;
CurSum largo = 0;
int i = 0;
mientras (i
int j = i;
mientras (j י n " pares[j].first == pairs[i].first) ++j; // grupo de nums iguales1

// 1 / ⃣ dar respuesta para todo el grupo
para (int t = i; t)
ans[pairs[t].second] = curSum;

// 2️ add group's nums2 into the heap
para (int t = i; t) {}
int idx = pares[t].second;
int val = nums2[idx];
minHeap.push(val);
curSum += val;
si (int)minHeap.size() {}
curSum -= minHeap.top();
minHeap.pop();
}
}

i = j);
}
devolver los ans;
}
};
`` `

Las tres soluciones funcionan en el tiempo de `O(n log n)` y utilizan `O(k)` espacio extra, que se ajusta cómodamente a las limitaciones (`n ≤ 105`).

-...

## 4. Blog Post – “Elige K Elementos Con Suma Máxima: El Bien, El Mal”

■ **SEO Palabras clave**: LeetCode 3478, Choose K Elements Con Maximum Sum, salto de tipo, cola de prioridad, diseño de algoritmos, complejidad del espacio-tiempo, Java, Python, soluciones C++

-...

#### 4.1 Introducción

Si estás haciendo preguntas de entrevista basadas en array, probablemente hayas visto *“pick the best k”* problemas todo el tiempo.
LeetCode 3478 te pide que hagas eso – pero con un giro añadido: los índices de los que puedes elegir son **restricted by a comparison on a second array**.
En este post caminamos a través de la solución **buena**, señalamos las trampas **bad** que a menudo tropiezan con la gente hacia arriba, y expongan los males **ugly** que hacen que este problema sea sutil.

-...

### 4.2 El “bien” – Por qué Este enfoque es elegante

1. **La ordenación da una orden lineal para “maller”* *
Una vez que el array se ordena por `nums1`, todos los elementos anteriores satisfacen `nums1[j] Identificado nums1[i]` automáticamente – no se necesitan escaneos caros.

2. **Min‐heap guarda sólo los mejores números k**
Debido a que el montón es un montón *min*, podemos mantener exactamente `k` números en `O(log k)` por inserción.
El "sum" que se ejecuta le da la respuesta al instante – sin reescanning o recomputación.

3. **Group‐by‐equal-value logic**
Duplicados de otra manera daría una relación “smaller” equivocada. Agruparlos garantiza la rigidez y mantiene el algoritmo lineal después del tipo inicial.

-...

### 4.3 El "Bad" – Errores comunes

Por qué rompe la vida Fijar
Silencio-----------------------------Prince--
tención **Usando una " comparación= "** para duplicados ANTERIED Los índices con el mismo valor de `nums1 ' se consideran “smaller” y terminan añadiéndose al montón. tención Grupo iguales valores y respuesta **antes** insertar el grupo. Silencio
Silencio **Poner cada elemento individualmente antes de asignar respuestas** ← Elementos en el índice actual se cuentan en su propia suma. Silencio Assign respuestas para todo el grupo primero, luego empujar el grupo en el montón. Silencio
Silencio **Usando un array en lugar de un montón** Silencio Tendrías que ordenar cada vez que necesitas el top‐k, convirtiendo el algoritmo en `O(nk)` o peor. Silencio Usar un `PriorityQueue`/`heapq`/`min-heap`. Silencio
Silencio **Assuming k iguala n** Silencio El montón mantendría todos los valores, pero el algoritmo todavía funciona; sin embargo, el uso de un montón en ese caso es exagerado. Silencio Si desea un caso de borde súper rápido, puede simplemente clasificar `nums2` y tomar la suma superior-k, pero la solución genérica permanece limpia. Silencio

-...

### 4.4 El “Ugly” – Edge Cases & Extensiones

1. *Muy grande*
Cuando `k` está cerca de `n`, el montón crecerá a ese tamaño; todavía bien, pero se puede saltar el mantenimiento del montón enteramente tomando la suma de los primeros `k ' clasificado `nums2` valores.
*Complexity*: `O(n log n)` still.

2. ** Números negativos en `nums2`**
La declaración del problema garantiza números enteros positivos, pero si lo relajas, la regla “a la mayoría de k” se vuelve esencial: es posible que elijas menos de los elementos “k” si añadir un valor negativo reduce el total.

3. #Updating `k` on the fly #
Si el entrevistador quiere una versión dinámica donde 'k' cambia por consulta, necesitarás un BST equilibrado o un truco de dos saltos – una discusión completamente diferente.

4. **Vista de ahorro de espacio* *
En lugar de un montón se puede mantener un conjunto de los mejores valores de 'k' (`std::multiset` en C++ o `SortedList` en Python).
La complejidad del tiempo sigue siendo `O(n log k)`, pero las constantes son un poco más grandes.

-...

### 4.5 Complexity Recap

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------------------
Silencio Java Silencio `O(n log n)` Silencio `O(k)` Silencio
TENIDO Python TENIDO `O(n log n)` Silencio
TENIDO C++ TENIDO `O(n log n)` Silencio

Con 'n ≤ 100.000', cada solución funciona bien bajo un segundo en hardware típico.

-...

### 4.6 Final Thoughts

LeetCode 3478 es una gran ilustración de cómo ** surtir + una cola de prioridad** convierte un problema aparentemente costoso “pick el mejor k” en una solución limpia y lineal.
Al manipular cuidadosamente los duplicados, evitamos la trampa más común y conservamos la estricta relación “sección”.

Siéntase libre de copiar los fragmentos de código en su IDE local, ejecute los casos de prueba y practique tweaking el algoritmo para variaciones (por ejemplo, “pick the best k *greater*” en lugar de “smaller”). ¡Feliz codificación!