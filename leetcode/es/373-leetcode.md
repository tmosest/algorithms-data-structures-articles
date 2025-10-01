-...
Título: LeetCode 373. Buscar parejas K con sumos más pequeños -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

# Buscar parejas K con sumos más pequeños – 373 – LeetCode
■ **Su guía para dominar este problema de entrevista en Java, Python y C++* *

■ **Meta‐Description** – Aprende a resolver LeetCode 373 “Encuentra a los pares K con sumos más pequeños” usando un enfoque prioritario (min-heap). Prepárate para tu próxima entrevista de codificación con soluciones claras y multilingües, cobertura de bordes y un análisis de blog “bueno-bad-ugly”.

-...

## 1. Por qué este problema importa

- **High-frequency interview topic** – casi todas las entrevistas de backend senior piden los pares *k más pequeños* o una variación similar *k‐closest*.
- ** Demostrar la maestría de la estructura de datos** – colas prioritarias, juegos de hash y trucos de dos puntos.
- **Showcases time‐space trade‐offs** – necesitarás explicar por qué un min‐heap golpea una solución ingenua `O(m*n).

Si puedes clavar este problema en **Java**, **Python**, y **C++**, tendrás un punto de conversación sólido para entrevistas técnicas y campamentos de codificación.

-...

## 2. Declaración de problemas (LeetCode 373)

Se le dan dos ** surtidos** arrays enteros `nums1` y `nums2`, y un entero `k`.

A *pair* is defined as `(u, v)` where `u` comes from `nums1` and `v` comes from `nums2`.

Devuelve los pares **k** con las sumas más pequeñas.

■ *Examples*
" texto
[1, 7, 11]
[2, 4, 6]
√≥ k = 3
■ Producto: [[1, 2], [1, 4], [1, 6]]
" `
" texto
[1, 1, 2]
[1, 2, 3]
* 2
■ Producto: [[1, 1], [1, 1]]
" `

■ **Constraints**
1 ≤ nums1.length, nums2.length ≤ 105
Ø - –109 ≤ nums1[i], nums2[i] ≤ 109
≤ 104
- `k` ≤ `nums1.length` × `nums2.length`

-...

## 3. La desintegración “buena – mala”

**Aspecto** Silencio**
Silencio----------------------------------------------------
Silencio **Data Estructura** Silencio Min‐heap da la extracción `O(log k)`. viv Naïve anidado bucles = `O(m*n)` tiempo, imposible para 105 arrays de tamaño. tención Olvidar pares dedupe – duplicados pueden llevar a resultados incorrectos. Silencio
Silencio **Espacio** Silencioso `O(k)` montones + `O(k)' visitados conjunto. Silencio Usar un conjunto de objetos `Pair` en Java puede causar sobrecarga grande si no se implementa correctamente. Silencio
Silencio **Edge Cases** Silencio Handles arrays vacíos, `k` ≤ tamaño del producto, valores duplicados. tención Los límites codificados por hardware pueden fallar en números negativos o errores extremadamente grandes k. ← Off‐por-one al empujar nuevos índices sobre el montón. Silencio
Silencio **Readability** Silencio Instrucciones de ayuda claras (`IndexPair` en C++/Python). tención Sobresuelve código Java con clases internas anónimas. tención Usar indexación basada en 0 vs. 1-basada indexación en comentarios causa confusión. Silencio
Silencio **Performance** Silencio `O(k log k)` es óptimo dada la necesidad de ordenar los resultados k. Silencio `O(m + n)` El escaneo de entonces la clasificación todavía sería `O(m*n)` caso peor. Silencio Si usted empuja ambos `(i+1, j)` y `(i, j+1)` sin revisar límites, obtendrás `ArrayIndexOutOfBounds`. Silencio

-...

## 4. Enfoque óptimo – Min‐Heap + Conjunto visitado

1. **Comienza** con el par `(0, 0)` - la suma más pequeña posible.
2. **Heap** almacena tuples: `(sum, i, j)`.
3. ** Conjunto visitado** recuerda qué índices han sido empujados para evitar duplicados.
4. **Mientras que todavía necesitamos pares (`k` veces) y el montón no está vacío:
* Pop la suma más pequeña.
* Apéndice `(nums1[i], nums2[j])` al resultado.
* Push `(i+1, j)` **si** no ha sido visitada y `i+1 se hizo nums1.length`.
* Push `(i, j+1)` **si** no ha sido visitada y `j+1 ' noms2.length`.
5. **Retorno** la lista.

**Por qué funciona* *
Debido a que ambos arrays están ordenados, las próximas sumas más pequeñas están siempre adyacentes al par más pequeño actual. Al empujar sólo a los dos candidatos “next” nunca extrañamos a un candidato mientras guardamos el tamaño del montón ≤ k.

**La complejidad* *
- Hora: `O(k log k)` (cada pop/push es `log k`)
- Espacio: `O(k)` (heap + visited set)

-...

## 5. Aplicación del Código

A continuación se muestran las implementaciones ** limpias, listas de producción** en **Java**, **Python**, y **C+**.
Los tres usan la misma idea algoritmo y manejan todos los casos de borde.

### 5.1 Java

``java
importar java.util*;

Solución de la clase pública {}
public List won(int[] nums1, int[] nums2, int k) {
Lista realizadaLista realizadaInteger confianza result = nuevo ArrayList recomendado();
si (nums1.length == 0 Silencioso desnudos2.length == 0 ← 0) Resultado de retorno;

// Min-heap ordering by sum
PriorityQueue madeint[] Confía minHeap = new PriorityQueue conveniente(Comparator.comparingInt(a - título a[0]));
Conjunto realizadoLong confiado visitado = nuevo HashSet fiel(); // store (i iere seleccionado 32)

minHeap.offer(new int[]{nums1[0] + nums2[0], 0, 0});
visitado.add(encode(0, 0));

mientras (k-- > 0 " sensible !minHeap.isEmpty()) {}
int[] cur = minHeap.poll();
int sum = cur[0];
int i = cur[1];
int j = cur[2];

result.add (Arrays.asList(nums1[i], nums2[j]));

si (i + 1) se hizo nums1.length) {}
llave larga = código(i + 1, j);
si (visited.add(key)) {
minHeap.offer(new int[]{nums1[i + 1] + nums2[j], i + 1, j});
}
}
si (j + 1 se hizo nums2.length) {
llave larga = codifica (i, j + 1);
si (visited.add(key)) {
minHeap.offer(new int[]{nums1[i] + nums2[j + 1], i, j + 1});
}
}
}
Resultado de retorno;
}

// Codifique dos índices en un solo largo para evitar objetos de Pareja
codificador privado largo(int i, int j) {
retorno (((long) i) < 32) Silencio (j < 0xffffffL);
}
}
`` `

**Puntos clave* *

- Usar una llave de 'long' en lugar de una clase de 'Pair' personalizado mantiene la memoria baja.
- La comparación es simple: ordenar por la suma precompuesta.
- Los casos de borde se manejan por adelantado (`k == 0`, arrays vacíos).

-...

### 5.2 Python 3

``python
importación heapq
de la importación Lista, Tuple

Solución de clase:
def kSmallestPairs(self, nums1: List[int], nums2: List[int], k: int) - título List[List[int]]:
si no nums1 o no nums2 o k == 0:
retorno []

result: List[List[int] = []
min_heap: List[Tuple[int, int, int]] = [] # (sum, i, j)
visitado = set() # store (i, j) tuples

heapq.heappush(min_heap, (nums1[0] + nums2[0], 0, 0)
(0, 0))

mientras k y min_heap:
s, i, j = heapq.heappop(min_heap)
result.append([nums1[i], nums2[j])
k -= 1

si i + 1 י len(nums1) y (i + 1, j) no visitados:
heapq.heappush(min_heap, (nums1[i + 1] + nums2[j], i + 1, j)
(i + 1, j))

si j + 1 se hizo len(nums2) y (i, j + 1) no se visitó:
heapq.heappush(min_heap, (nums1[i] + nums2[j + 1], i, j + 1))
visitado.add(i, j + 1))

Resultado de retorno
`` `

**Highlights* *

- `heapq` da un montón binario eficiente de la caja.
- El conjunto "visitado" evita empujar pares de índice duplicados.
- Las insinuaciones de tipo hacen que la función sea autodocumentada.

-...

### 5.3 C++

``cpp
Incluido el título
#include >
#include ■unordered_set
*incluye el título funcional

Clase Solución {
public:
std::vector seleccionados::vector realizadoint kSmallestPairs(
const std::vector garantizadoint
const std::vector correspondint
int k) {

std::vector seleccionados::vector realizadoint res;
si (nums1.empty() ← permanecen desnudos2.empty() 0) restitución;

// Min-heap: {sum, i, j}
usando HeapNode = std::tuple obtenidos, int, int
auto cmp = [](const HeapNode pulmonar a, const HeapNode pulmonar b) {
retorno std::get made0(a) √≥ std::get fiel0(b); // reverse for min‐heap
};
std::priority_queue madeHeapNode, std::vector madeHeapNode confianza, decltype(cmp) confianza pq(cmp);
std::unordered_setSe realizó larga experiencia visitada; // encode (i,j) - título largo

codificador automático = [](int i, int j) largo
retorno (static_cast realizado largo largo(i)
};

pq.emplace(nums1[0] + nums2[0], 0, 0);
(0, 0));

mientras (k √≥ 0 ' pq.empty() {
auto [s, i, j] = pq.top(); pq.pop();
res.push_back({nums1[i], nums2[j]});
k;

si (i + 1  observado nums1.size() " paciente visited.insert(encode(i + 1, j)).second) {
pq.emplace(nums1[i + 1] + nums2[j], i + 1, j);
}
si (j + 1  observado nums2.size() " paciente visited.insert(encode(i, j + 1)).second) {
pq.emplace(nums1[i] + nums2[j + 1], i, j + 1);
}
}
restitución;
}
};
`` `

**Por qué esto es rápido en C++**

- `std::tuple observadoint, int, int `` es ligero.
- Codificar índices en un único largo mantiene el sistema visitado inclinado.
- El comparador de lambda mantiene el código conciso.

-...

## 6. Pruebas " Edge‐ Cobertura de casos

Silencio **Escenario** Silencioso ** Qué probar
Silencio...
Silencioso ** arrays vacíos** Silencioso `nums1 = []`, `nums2 = [1, 2]` → `[]
Silencio **Números negativos** Silenciosos `nums1 = [-5, -1] `, `nums2 = [0, 3] ` → pares correctos
Silencio ** Valores duplicados** Silenciosos `nums1 = [1, 1]`, `nums2 = [1, 1]` → duplicados se permiten " contados
Silencio **k más grande que el producto** Silencio `k = 10`, arrays de longitud 2 → devolver todos los 4 pares
Silencio **k = 0** Silencio Debería devolver `[]` inmediatamente
Silencio **Ambos arrays longitud 1** ← Prueba simple 1‐pair

Use pruebas de unidad que cubren cada uno de estos escenarios – muestra a los entrevistadores que no sólo está hackeando una solución sino pensando en la robustez de producción.

-...

## 7. Cuando usted *No* Necesita el Conjunto Visitado?

Si estás absolutamente seguro de que los dos arrays tienen valores **unique** y sabes que `k` ≤ `nums1.length` + `nums2.length`, puedes **drop** el conjunto visitado y empujar tanto `(i+1, j)` como `(i, j+1)` incondicionalmente.
Pero para las restricciones generales de LeetCode, el conjunto visitado es obligatorio – de lo contrario empujarás el mismo par varias veces, volarás el montón y producirás respuestas erróneas.

-...

## 8. Entrevista rápida Resumen

- **Algorithm**: Min-heap of `(sum, i, j)` + hash set of visited indices.
- ** Complejidad**: `O(k log k)` tiempo, `O(k)` espacio.
- **Por qué es óptimo**: La entrada ordenada garantiza las siguientes sumas más pequeñas son vecinos.
- **Idiomas**: Listo a paso Java, Python, y C++ código arriba.

Si puedes explicar esto en **5 minutos**, estás a mitad de camino a través de una entrevista estelar.

-...

## 9. Siguientes pasos – Práctica " Entrevista Prep

1. **Ejecute el código** contra las pruebas ocultas de LeetCode.
2. **Hora usted mismo** – una solución `Java` debe terminar bajo 1 s en una entrada de 105 tamaño con `k = 104`.
3. **Explicar las compensaciones**: ¿Por qué un montón es necesario, qué pasa si saltas el conjunto visitado, etc.
4. **Entrevista móvil**: Reúnete con un amigo y practica la discusión “bueno-bad-ugly” – es un inicio de conversación perfecto.

-...

## 10. Call to Action

**Lista a su próxima entrevista de codificación? * *
- **Descargar** las soluciones multilingües (copy-paste)
- **Run** tus propias pruebas en GitHub o un IDE local
- **Compartir** este artículo con pares – es SEO-friendly y listo para su Enlace En post.

> **Reserva una entrevista de mock conmigo** o **Únete a nuestro desafío semanal LeetCode** – ¡hagamos que la práctica se convierta en rendimiento!

¡Feliz codificación!