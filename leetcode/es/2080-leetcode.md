-...
Título: LeetCode 2080. Consultas de frecuencia de rango -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🚀 Range Frequency Queries (LeetCode 2080) – Java, Python & C++ Soluciones + un SEO‐Ready Blog Post

■ **TL;DR**
• **Problema**: Encuentra cuántas veces aparece un valor en un sub-array.
* **Core Idea**: Almacene las posiciones de cada número en un * surtido* lista → búsqueda binaria para el rango.
* * Complejidades**: `O(n)` preprocesamiento, `O(log n)` por consulta, `O(n)` memoria.
* **Por qué es genial para las entrevistas**: Estructura de datos simple, razonamiento claro, y usted puede hablar de intercambios (hash‐map + búsqueda binaria vs. árbol de segmento vs. Mo’s algoritmo).

-...

## 1. Declaración de problemas (LeetCode 2080)

■ **Diseño** una clase 'RangeFreqQuery' que apoya:
- `RangeFreqQuery(int[] arr)` - constructor.
⇩ - `int query(int left, int right, int value)` – devolver la frecuencia de `valor` en el sub-array `arr[left ... right]`.

Limitaciones
`` `
1 ≤ arr.length ≤ 1e5
1 ≤ arr[i], valor ≤ 1e4
0 ≤ izquierda ≤ derecha
≤ 1e5 consultas
`` `

-...

## 2. Insight Core – *Arrays of Indices*

Desde `arr[i]` ≤ `10^4`, podemos pre-allocalizar una matriz de tamaño `10001`.
Para cada posible valor `v` almacenamos la lista surtida de índices ** donde se produce `v`.

`` `
indices[v] = [i0, i1, i2, ...] (principalmente aumentando)
`` `

*¿Por qué? *
Porque realizaremos búsqueda binaria en estas listas durante las consultas.
La clasificación es inherente porque agregamos índices en orden ascendente durante la construcción.

** algoritmo de pregunta**

1. `l = lower_bound(indices[valor], izquierda)` - primer índice ≥ `izquierda.
2. `r = upper_bound(indices[valor], right)` – primer índice  'derecha'.
3. Resultado = `r - l`.

Ambos pasos son `O(log k)` donde `k` es el número de ocurrencias de 'valor'.
In the worst case `k = n`, but still `O(log n)`.

-...

## 3. Aplicación en tres idiomas

A continuación están listos para completar los snippets.
Siéntete libre de copiar-paste en tu parque infantil IDE o LeetCode.

-...

### 3.1 Java

``java
importar java.util*;

clase pública RangeFreqQuery {
// índices[v] mantiene todas las posiciones donde arr[i] == v
lista final privada realizadaInteger título[] índices;

@SuppressWarnings("unchecked")
public RangeFreqQuery(int[] arr) {
índices = nuevo ArrayList[10001]; // 0 ... 10000
para (int v = 0; v)
indices[v] = nuevo ArrayList correctamente();
}
para (int i = 0; i)
indices[i].add(i);
}
}

int query (int left, int right, int value) {}
Lista de entradas = índices [valor];
if (list.isEmpty()) return 0;

int l = lowerBound(list, left); // first ⇩= izquierda
int r = upperBound(list, right); // first ⇩
retorno r - l;
}

// Ayudantes de búsqueda binaria
int privada estática inferiorBound(Listecto:Integer título, int target) {
int lo = 0, hola = list.size();
mientras (lo cautivado) {
int mid = (lo + hola) 1;
si (list.get(mid) <) lo = medio + 1;
más hola = medio;
}
devolver lo;
}

estática privada int upperBound(Listecto:Integer ratio, int target) {
int lo = 0, hola = list.size();
mientras (lo cautivado) {
int mid = (lo + hola) 1;
si (list.get(mid) <= target) lo = mid + 1;
más hola = medio;
}
devolver lo;
}
}
`` `

**Puntos clave* *

* Usa `ArrayList` – sin copia adicional durante la construcción.
* `@SuppressWarnings("unchecked")` es seguro porque sabemos el tamaño.
* `lowerBound` / `upperBound` son los ayudantes clásicos del estilo C++.

-...

#### 3.2 Python

``python
importador bisect
de la importación Lista

class RangeFreqQuery:
def __init_(self, arrr: List[int]):
# indices[v] = lista ordenada de posiciones
auto.indices = [[] para _ en rango(10001)]
para i, v en enumerate(arr):
self.indices[v].append(i)

def query(self, left: int, right: int, value: int) int:
lst = self.indices[value]
si no lst:
retorno 0
l = bisect.bisect_left(lst, left) # first ю= izquierda
r = bisect.bisect_right(lst, right)
retorno r - l
`` `

*El `bisecto`* de Pitón ya es una implementación C rápida, por lo que no necesita escribir su propia búsqueda binaria.

-...

### 3.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

clase RangeFreqQuery {
privado:
vectores seleccionados:

public:
RangeFreqQuery(vector fielint >arr) {
indices.assign(10001, {});
para (int i = 0; i) ++i) {
indices[arr].push_back(i); // indices are appended in order
}
}

int query(int left, int right, int value) {}
const vector armonizado "vec = indices [valor];
si (vec.empty()) devuelve 0;

auto l = lower_bound(vec.begin(), vec.end(), left);
auto r = upper_bound(vec.begin(), vec.end(), right);
retorno r - l;
}
};
`` `

El código C++ utiliza la lógica de STL `lower_bound` / `upper_bound` – idéntica como Java.

-...

## 4. Análisis de la complejidad

TEN TERRITOR TERRITOR TEN TERRITOR TEN TERRITOR TEN TERRITOR SON TERRITOR SON SON SON TEN SON SON SON 
Silencio------Prince--------
Silencio **Preprocesamiento** Silencio `O(n)` – cada elemento es empujado una vez en su cubo. TENIDA `O(n)` – la longitud total de todos los cubos equivale a `n`. Silencio
tención **Single query** Silencioso `O(log k)` ≤ `O(log n)` Silencio `O(1)` por consulta (aparte de la búsqueda del cubo). Silencio
Silencio **El peor de los casos** en general

¿Por qué no? *
Si todos los elementos son iguales ( " valor " = 1), el cubo correspondiente tiene tamaño " n " .
La búsqueda binaria en `n` elementos sigue siendo logarítmica.

-...

## 5. Alternativas – Cuándo elegir qué

Silencioso aproximación Silencio Pros
Silencio----------------------------
tención **Array of indices + búsqueda binaria** (nuestra solución) Silencio • O(1) lookup + O(log n) por consulta. • Muy fácil de explicar. No hay placa de caldera de estructura de datos pesados. • Si `arr[i]` puede ser grande ( > 1e5 ), no podemos pre-allocar un cubo por valor. tención Entrevista preguntas donde las restricciones permiten un pequeño dominio. Silencio
Silencio ** algoritmo de Mo** (preguntas de línea) Silencio • O(n + q) √n) – bueno cuando las consultas son conocidas de antemano. Silencio • Más difícil de código; necesita descomposición de bloque. No "online". Los problemas de entrevistas de “Batch” o “offline” rondas de entrevista. Silencio
Silencio ** Árbol de segmento / TBI de HashMaps** Silencio • Consulta de tiempo para *cualquier* valor, no sólo pequeño dominio. Silencio • Espacio: O(n log n) debido a la fusión del mapa. • Complejidad de implementación alta. ← Entrevistadores que piden explícitamente una solución * árbol de segmento*. Silencio
Silencio ** Árbol de agua** Silencio • Maneja los grandes valores de `arr[i]`. tención Entrevista avanzada o pista de “data‐estructuras”. Silencio

■ **Bueno**: El método de índices-bucket es perfecto para *online* consultas y dominio pequeño.
■ **Bad**: Es desperdicio si el rango de valor fuera enorme (`1e9`).
■ **Ugly**: Si no manejas los cubos vacíos correctamente, obtendrás respuestas incorrectas o `IndexOutOfBoundsException`.

-...

## 6. “Bueno, malo & ugly” – Un desarrollador-Entreview Lens

Silencio Silencio Silencio Silencio Silencio Silencio
Silencio----------Prince------
Silencio **Concepto** Silencio Intuición de “buscar en una lista de posiciones” – muy explicable. Silencio Ninguno. Silencio Si usted elige un * árbol del segmento* o el algoritmo de *Mo* sin explicar primero la matriz más simple de índices, los entrevistadores pensarán que usted está sobre-configurado. Silencio
Silencio **Pre-procesamiento** Silencioso O(n) tiempo; sólo un solo paso. Silencio Ninguno. Silencio Olvidar pre-allocalizar el tamaño de la matriz de cubo puede llevar a 'ArrayIndexOutOfBoundsException`. Silencio
TEN **Query** Silencio O(log n) por consulta; utiliza la búsqueda binaria estándar. Silencio Ninguno. Silencio Relying on Java’s `Arrays.binarySearch` y malinterpretar su valor de retorno (índices negativos) chocará su código. Silencio
Silencio ** Memoria** Silencio O(n) total, bien dentro de los límites. Silencio Ninguno. Silencio Guardar todo el array en un `HashMap observadoInteger, Integer `` por cada valor (tamaño 1e4) soplará la memoria – **evitar** eso. Silencio
Silencio **Testing** Silencio Fácil de escribir pruebas de unidad – sólo brute‐force un array al azar. Silencio Ninguno. Silencio Failing to handle the case where the value does not exist (empty balde) → `0` vs `r-l` negative bug. Silencio

-...

## 7. FAQ – Pitfalls comunes " Gotchas

Respuesta a la respuesta
Silencio...
Silencio ¿Y si el valor es 0? Las restricciones del problema de la vida dicen `arr[i]` ≥ 1, pero todavía puede apoyar 0 asignando `tamaño 10001`. Ten cuidado de que tu cubo es lo suficientemente grande. Silencio
Silencio **Will `upperBound` ever return `-1`?** Silencio No, `upperBound` devuelve el *index* del primer elemento mayor que el objetivo. Si todos los elementos son ≤ `derecha', devuelve `list.size()`. Silencio
Silencio **¿Por qué no utilizar `Collections.binarySearch`?** Silencio Devuelve el *index del elemento exacto* o `-(insertionPoint) - 1`. Convertir eso en `lowerBound` / `upperBound` es más propensa a error que escribir los dos pequeños ayudantes. Silencio
Silencio **¿Cómo me adapto si `arr[i] puede ser 10^9?** Silencio Usar un `HashMap observadoInteger, Lista hecha en lugar de una serie de listas; el enfoque sigue siendo el mismo. Silencio

-...

## 8. Consejos para entrevistas

1. **Comienza con la solución más simple** – explica la idea de “arrayos de índices”; luego pregunta si el entrevistador quiere un enfoque más sofisticado (árbol de segmento, algoritmo de Mo, etc.).
2. **Hablar sobre los cambios** – mencionar que el enfoque de cubo es espacio lineal pero rápido, mientras que un árbol de segmento utiliza más memoria pero trabaja para cualquier valor `arr[i]`.
3. **Mostrar su estilo de codificación** – utilizar el nombre apropiado (`indices`, `lowerBound`, `upperBound`) y comentar su código.
4. ** Casos del borde de la mención** – cubo vacío, valor no presente, izquierda √° derecho (no debe suceder por limitaciones pero todavía comprobar).
5. ** Pruebas de unidad de Proveedor** – escribir una pequeña función principal o método `@Test` que afirma salidas conocidas.
6. **Mostrar familiaridad con C++ STL y Python bisect** – a muchos entrevistadores les encanta ver que conocen los lenguajes específicos.

-...

## 9. Wrap‐Up & Final Pensamientos

* La solución “arrayos de índices” es **la respuesta canónica** para LeetCode 2080.
* Corre en `O(n)` tiempo de preprocesamiento, `O(log n)` por consulta, y `O(n)` memoria, perfecto para las limitaciones dadas.
* Si te preparas para una entrevista **coding** o un trabajo **data‐estructuras**, puedes hablar con confianza sobre esta solución, sus fortalezas, y por qué la elegirías sobre un árbol de segmento a menos que la entrevista lo exija explícitamente.

Feliz codificación, y que su próxima entrevista sea tan suave como una búsqueda binaria en una lista ordenada! ▪

-...

*Keywords para SEO*: **Range Frequency Queries LeetCode 2080, RangeFreqQuery implementation, Java Python C++ solution, interview data structure, job interview coding, binario search, arrays of indices, segment tree alternative**.