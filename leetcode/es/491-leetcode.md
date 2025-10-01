-...
Título: LeetCode 491. Subsecuencias no disminuyentes -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 491. Subsecuencias no disminuyentes
■ **Medium** Silencio **Volver al inicio de la sesión* _ Time O(n · 2n)** (caso inferior)

-...

### 📌 Declaración de problemas (LeetCode)

■ **Given** un array entero `nums`, return **all** the *different* possible non-decreasing subsequences of the given array with *at least two* elements.
■ La respuesta puede estar en cualquier orden.

*Ejemplo*

TEN TERRITOR ANTERIOR ANTERIOR
Silencio...
[4],[4],[4],[4],[4],[4],[4],[4],[4],[4],[6,7],[7,[7,7]] Silencio
TENIDA `[4,4,3,2,1] ' ANTE `[4,4] ' Silencio

**Constraints* *

- `1 ≤ nums.length ≤ 15`
- `-100 ≤ nums[i] ≤ 100`

-...

## 🔧 Solution Overview

Los principales retos:

1. ** Orden no disminuyente** – una subsequencia sólo puede ser extendida si el nuevo elemento es **≥** el último elemento en el camino actual.
2. **Duplicados** – la entrada puede contener números repetidos, por lo que muchos caminos diferentes pueden producir la subsequencia *same*.
Debemos producir cada subsequencia **una vez**.

El enfoque clásico es **backtracking** (DFS) con un **`HashSet`** para evitar duplicados.

### Backtracking Steps

1. Comience con un camino vacío `cur`.
2. Por cada índice `i` de `start` a `n-1`:
- Si `cur` está vacío o `nums[i] ≥ cur.last`, podemos añadir `nums[i] a `cur`.
- Continúe recusivamente desde " i+1 " .
- Backtrack eliminando `nums[i].
3. Cada vez que la longitud de la ruta actual ≥ 2, añadir un *copia* de él a un `Set observadoList recomendado globalInteger confianza `` (para deduplicar).
4. Después de explorar todas las posibilidades, devuelve el conjunto convertido a una lista.

## Evitar Duplicados Eficientemente

- Debido a que la longitud de la matriz es mayor de 15, el número total de subsecuencias es manejable (`≤ 215 = 32,768`).
- Sin embargo, los duplicados pueden ser frecuentes (por ejemplo, `[4,4]`).
- Usando un `Set observadoLista realizadoInteger título `` automáticamente deduplica, y el sobrecabezamiento es insignificante para los límites dados.

-...

## 🧩 Code Implementations

A continuación se presentan implementaciones limpias y bien agregadas en **Java**, **Python**, y **C+**.

-...

#### ## 1down⃣ Java

``java
importar java.util*;

Solución de la clase pública {}
public List made(int[] nums) {
Establecer seleccionado()
dfs(nums, 0, nuevo ArrayList correctamente(), res);
devolver nuevo ArrayList garantizado(res);
}

dfs de vacío privado(int[] nums, int index, List GarantizadoInteger confianza cur, Conjunto recomendadoLista realizadoInteger títuloRes) {
si (cur.size() 2) {
// Almacene una *copia* para que las modificaciones posteriores no afecten la entrada del set
res.add (nuevo ArrayList garantizado(cur));
}

para (int i = index; i)
si (cur.isEmpty() Silencioso desnudos[i] √= cur.get(cur.size() - 1)) {
cur.add (nums[i]);
dfs(nums, i + 1, cur, res);
cur.remove(cur.size() - 1); // backtrack
}
}
}
}
`` `

■ ¿Por qué un HashSet?
■ Java’s `HashSet` utiliza `equals()`/`hashCode()` en las listas, por lo que se descartan automáticamente secuencias duplicadas.

-...

#### 2down⃣ Python

``python
de la importación Lista, Conjunto, Tuple

Solución de clase:
def find Subsequences(self, nums: List[int]) - Relacion[List[int]:
resultado: Set[Tuple[int, ...]] = set()
auto.backtrack(nums, 0, [], result)
[list(t) for t in result]

def backtrack(self, nums: List[int], index: int,
path: List[int], result: Set[Tuple[int, ...]) - No. Ninguno.
si len(path) 2:
result.add(tuple(path)) # tuples are hashable

para i en rango(index, len(nums)):
si no camino o nums[i] path[-1]:
path.append(nums[i])
auto.backtrack(nums, i + 1, path, result)
path.pop() # backtrack
`` `

■ ¿Por qué los tuples? #
■ El 'set' de Python sólo acepta objetos problemáticos. Convertir la lista en un tuple nos permite almacenar subsequences sin duplicados.

-...

#### 3down⃣ C++

``cpp
Incluido el título
#include >
usando std namespace;

Clase Solución {
public:
vector identificadovector fieltro encontradaSubsequences(vector fieltro nums) {
marcador seleccionado res;
vector:
dfs(nums, 0, cur, res);
vector de retorno seleccionado(res.begin(), res.end());
}

privado:
vacío dfs(cont vector identificadoint círculo nums, int idx,
vector significando:
si (cur.size() 2) res.insert(cur);

para (int i = idx; i) ++i) {
si (cur.empty() {}
cur.push_back (nums[i]);
dfs(nums, i + 1, cur, res);
cur.pop_back(); // backtrack
}
}
}
};
`` `

■ **C++ `set`** ordena automáticamente y deduplica las subsecuencias.

-...

## 📊 Complexity Analysis

Silencio Silencio Silencio Silencio
Silencio----------------
← exploración de DFS Silencio **O(n · 2n)** (caso inferior) – cada subconjunto puede ser visitado Silencio **O(n)** profundidad de recidiva
Silencio Establecer inserción Silencio **O(k log k)** por inserción, donde *k* es el número de subsecuencias únicas (≤ 2n) Silencio **O(k · n)** total para todas las subsecuencias almacenadas

Dado `n ≤ 15`, el algoritmo encaja cómodamente dentro de los límites de tiempo.

-...

## 🎯 Interview‐Ready Tips

Silencio Silencio Silencio Silencio
Silencio...
TENIDO TENIDO Utilizar backtracking para generar subsequences incrementalmente. TEN ❌ Do *not* sort the array – order matters! Silencio ❌ Evite `String` concatenation for each path; it blows up memory. Silencio
TENIDO TENIDO Los resultados de la tienda en un `Set` (o `unordered_set` / `HashSet`) para dedupe de forma automática. TEN ❌ Olvídate de convertir el camino a una *copia* antes de añadir al conjunto; posteriores retroceder entradas corruptas. ❌ Ignorando el *al menos dos* limitación; añadir todas las subsecuencias de la longitud 1 conduce a la respuesta incorrecta. Silencio
Silencio TENIDO Explicar la complejidad del tiempo/espacio claramente. TENIDO ❌ Falta para discutir por qué aparecen los duplicados (números repetidos). ← ❌ No manejar números negativos – asegurar que la comparación sea ``. Silencio

-...

## 📝 Blog Article: “The Good, the Bad, and the Ugly of LeetCode’s Non-Decreasing Subsequences”

■ **Meta‐Title: ** *Master LeetCode 491: Subsecuencias no disminuyentes – El bien, el mal y el ugly (Java, Python, C++)*
■ **Meta‐Description:** *Descubre la solución paso a paso de LeetCode 491. Aprenda las trampas, código en Java/Python/C++ y as su entrevista de codificación. ¡Pon tu curriculum vitae hoy! *

-...

#### ## 1down⃣ Lo que hace Este problema “Medium”
- Tamaño de entrada pequeño (`n ≤ 15`) pero una explosión combinatoria de posibles subsecuencias.
- Requiere un manejo cuidadoso de **duplicados** – una trampa de entrevista común.
- Debe respetar el límite **no disminuyendo** al generar todos los subconjuntos válidos.

-...

#### 2down⃣ El Bien: Elegante Backtracking + HashSet

- **Backtracking** da una estructura recursiva natural: en cada índice decide si *incluya* o *apagado* el elemento actual.
- **HashSet** (o `set` in C++ / `Set` in Java) elimina la carga de los cheques duplicados manuales.
- Código limpio y legible que se puede adaptar a muchas variantes de “subsecuencia”.

-...

#### 3down⃣ El malo: Pitfalls comunes

Silencio Pitfall Silencio Por qué Sucede
Silencio...
Silencio *No copiar el camino antes de insertar en el set* Silencio La misma instancia de `Lista' se muta más tarde. Silencio Crear un nuevo `ArrayList fiel(path)` (o `tuple(path)` en Python). Silencio
*Agregar subsecuencias de longitud 1* Silencio Estados Problemas *al menos dos* elementos. ← Check `path.size() 2` antes de añadir. Silencio
*Usar una lista global en lugar de un set* Silencio Duplicates sobreviven porque la igualdad de lista no se utiliza automáticamente. Silencio Use un contenedor de `Set`. Silencio

-...

#### 4down⃣ The Ugly: Performance Jitters

- **Tiempo**: En el peor de los casos (por ejemplo, todos los elementos iguales) la recursión explora sendas `2n`. Para `n=15`, es alrededor de 32k, que está bien.
- **Espacio**: Robar cada subsequencia única podría volar si el array contiene muchos valores distintos. Sin embargo, las limitaciones mantienen esto manejable.
- **Evitar**: Concatenación excesiva de cuerdas, recidiva profunda más allá de `n` (pero aquí `n ≤ 15`).

-...

### 5down⃣ Code in Three Languages – One for Every Stack

■ *Véase las implementaciones anteriores. *
■ Elige el idioma con el que estés más cómodo, o muestra los tres en tu GitHub.

-...

### 6 comentarios SE SEO‐Friendly Takeaways for Job Seekers

- **Keywords**: “LeetCode 491 solución”, “No disminuir subsequences”, “Entrevista de backtracking”, “Java Python C++”, “Consultores de entrevista”.
- **Headers**: Use H1 para el título, H2 para secciones como “Good”, “Bad”, “Ugly”, y H3 para sub-puntos.
- **Meta Tags**: Incluya el número de problema y los términos clave en la meta-descripción.
- **Enlace Building**: Consulte el problema oficial LeetCode, soluciones similares, y su propio GitHub repo.
**Engagement**: Agregue un breve párrafo “Lo que aprendí” para fomentar los comentarios.

-...

Lista final antes de enviar

- Acreditar los ejemplos proporcionados.
- ✅ Agregar los casos de borde: todos los números negativos, único elemento repetido, estrictamente creciente array.
- ✅ Asegúrese de que la profundidad de recursión no exceda los límites de la pila.
- ✅ Ejecutar las pruebas de tiempo y memoria (secciones “Runtime” y “Memory” de LeetCode).

-...

## 🚀 Takeaway

LeetCode 491 es un rompecabezas de entrevista *clásico* que prueba tanto el pensamiento algoritmo como la atención al detalle. Al dominar el patrón de retroceso y el truco de deduplicación, no sólo resolverá este problema sino que también ganará un kit de herramientas reutilizable para una amplia gama de preguntas de “subsequencia”.

Ahora adelante, pulir su solución, y compartirla en su cartera. ¡Buena suerte aterrizando ese trabajo de ensueño!