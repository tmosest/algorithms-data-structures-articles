-...
Título: LeetCode 493. Parejas inversas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Parejas inversas (LeetCode 493) – Código & Guía del Blog

A continuación encontrarás implementaciones preparadas para la producción* **Java, Python y C+** para el problema *Reverse Pairs*.
Después del código leerás un artículo de estilo *blog* que explica el problema, los aspectos “buenos, malos y feos” de las soluciones típicas, y por qué este problema es un gran punto de conversación para los roles de ingeniería de software.

■ **SEO Palabras clave**: *LeetCode Parejas inversas, Solución de Parejas inversas, Merge Sort, división-y-conquer, pregunta de entrevista, Java, Python, entrevista de codificación C++, consejos de entrevista de trabajo, entrevista de algoritmo*

-...

## 1. Recaptura de problemas (LeetCode 493)

■ ** Parejas reversas* *
■ *Given an integer array `nums`, devolver el número de pares inversos en el array. *
■ Un par reversivo es un par `(i, j)` donde `0 ≤ i ' significa j ' nums.length ' y `nums[i] œ 2 * nums[j]`.

TEN SON SON SON SON SON SON SON SON SON 
Silencio----------------------------------------------------
Silencio 1 Silencio `[1,3,2,3,1] ' Silencio `2` Silencio `(1,4)` y `(3,4)` Silencio
TENIDO 2 TENIDO `[2,4,3,5,1] ' ANTE `3` TENIDO `(1,4)`, `(2,4)`, `(3,4)` Silencio

**Constraints* *

* `1 ≤ nums.length ≤ 5 × 104`
* `-231 ≤ nums[i] ≤ 231 − 1`

-...

## 2. Why the Naïve O(n2) Approach Fails

El doble bucle de fuerza bruta comprueba cada par:

``text
para mí en 0 .. n-1:
para j en i+1 .. n-1:
si nums[i] √≥ 2 * nums[j]:
Contador++
`` `

* **Tiempo**: `O(n2)` – inaceptable para ' n = 50.000 ' (consumir 2.5 billones de operaciones).
* **Espacio**: `O(1)` - Bien, pero la velocidad lo mata.

-...

## 3. El “bien” – Divide " Conquer with Merge Sort

La solución óptima utiliza el mismo truco contable que subyace a *conteo de inversión*.
Mientras realizamos un merge-sort estándar, **contamos** cuántos elementos en la mitad derecha satisfacen la condición de pago inverso para cada elemento en la mitad izquierda.

### 3.1 Algorithm Sketch

`` `
función de fusión SortAndCount(nums, left, right):
si la izquierda >= derecha: retorno 0

media = (izquierda + derecha) / 2
cuenta = mergeSortAndCount(nums, left, mid)
+ mergeSortAndCount(nums, mid+1, right)

// Cuenta pares inversos cruzando las mitades
j = mitad + 1
para mí de izquierda a mitad:
j < = derecho y nums[i] 2 * nums[j]:
j++
contar += j - (medio + 1)

// Combina las dos mitades clasificadas
merge(nums, left, mid, right)
cuenta de retorno
`` `

****Key Insight*
*Mientras las dos mitades están ordenadas, podemos caminar por ellas linealmente para contar todos los cruces en O(n). *

#### 3.2 Why It Works

* Cada llamada recursiva garantiza que su segmento se ordene después de regresar.
* El paseo de dos puntos ( " i " a la izquierda, " a la derecha " ) cuenta todos los pares " i, j) " con `i ' en la mitad izquierda y `j ' en la mitad derecha.
* Merge step mantiene la orden orden ordenada para el siguiente nivel.

#### 3.3 Complexity

* **Tiempo**: `O(n log n)` - cada nivel de los procesos de recursión todos los elementos de una vez.
* **Espacio**: `O(n)` - matriz auxiliar para fusionarse (puede hacerse en lugar con trucos adicionales pero `O(n)` es más simple).

-...

## 4. El “Bad” – Pitfalls comunes

Silencio Pitfall Silencio Por qué Sucede
Silencio...
Silencio **Desbordamiento entero** cuando se computan `2 * nums[j] ' ¦ puede ser tan grande como `231−1`. Multiplying by 2 overflows 32‐bit int. ← Use 64-bit (`long`/`long') para el producto. Silencio
Silencio **Using `int` for count** Silencio El recuento máximo puede ser `n(n-1)/2`, hasta ~1.25 billion for `n=50k`. ← Uso `long ` for the counter in Java/C++; `int` in Python is unbounded. Silencio
Silencio **Wrong merge boundaries** Silencio Off‐por-one errores (`mid` vs `mid-1`) romper el orden invariante. ← Pruebe a fondo con pruebas de unidad; utilice el esqueleto de combinación estándar. Silencio
TEN **Re-alizar arrays cada fusión** TEN Causes alta constante overhead. TEN Reuse a single temporary array (pass it down or create once). Silencio

-...

## 5. El “Ugly” – Enfoques alternativos

Silencio Silencio Silencio Pros
Silencio...
Silencio **Arbol Indizado Indizado Indicio (Fenwick)** Silencio Maneja actualizaciones dinámicas, útiles en variaciones. ← Requiere coordinar la compresión, O(n+logV) log n). Silencio
Silencioso ** Árbol del segmento** Silencioso Similar al TBI pero más flexible. Más memoria, mayor factor constante. Silencio
Silencio **Divide‐and‐Conquer (igual que Merge Sort)** tención Optimal O(n log n). La complejidad de la implementación para los novatos. Silencio

Para este problema exacto, *Merge Sort* sigue siendo la solución más sencilla, limpia y fácil de entrevista.

-...

## 6. Aplicación – 3 idiomas

### 6.1 Java

``java
importar java.util*;

Solución de la clase pública {}
int reversePairs(int[] nums) {
si (nums == null 0) retorno 0;
int[] temp = nuevo int[nums.length];
(int) merge SortAndCount(nums, temp, 0, nums.length - 1);
}

// Las devoluciones cuentan tanto como para evitar el desbordamiento
mergeSortAndCount(int[] nums, int[] temp,
int left, int right) {
si (izquierda derecha) devuelve 0;
int mid = left + (right - left) / 2;
larga cuenta = mergeSortAndCount(nums, temp, left, mid)
+ mergeSortAndCount(nums, temp, mid + 1, right);

// Cuenta pares cruzados
int j = mid + 1;
para (int i = izquierda; i = media; i++) {
mientras (j " = derecho " (long) nums[i] ю 2L * nums[j]) {}
j++;
}
contar += j - (mid + 1);
}

// Paso de fusión
int i = izquierda, k = izquierda;
mientras que (i י= mid ' ritmo j
si (nums[i] temp[k++] = nums[i+];
temp[k+] = nums[j++];
}
mientras (i 0= mediados) temp[k++] = nums[i+];
mientras (j < = derecho) temp[k++] = nums[j+];
System.arraycopy(temp, left, nums, left, right - left + 1);
recuento de retorno;
}
}
`` `

### 6.2 Python

``python
def reversePairs(nums):
si no nums:
retorno 0

def merge_sort_and_count(arr, left, right):
si se deja Bien.
retorno 0
media = (izquierda + derecha) // 2
cuenta = merge_sort_and_count(arr, left, mid) + \
merge_sort_and_count(arr, mid + 1, right)

# Cuenta pares inversos
j = mitad + 1
para i en rango(izquierda, media + 1):
j > j > derecho y arrr[i]
j += 1
contar += j - (medio + 1)

# Merge lobos ordenados #
merged = []
i, j = izquierda, mitad + 1
Mientras que yo hice el medio y el derecho:
merged.append(arr[i] if arrr[i]
si arrr[i]
i += 1
más:
j += 1
mientras que yo me apunté a mitad:
merged.append(arr[i]); i += 1
mientras que j
merged.append(arr[j]); j += 1
arrr[left:right+1] = merged
cuenta de retorno

regreso merge_sort_and_count(nums, 0, len(nums) - 1)
`` `

### 6.3 C++

``cpp
Incluido el título
#include >

Clase Solución {
public:
int reversePairs(std::vector seleccionadoint limitada nums) {
(nums.empty()) return 0;
std::vector obtenidosint ánimo temp(nums.size());
long res = mergeSortAndCount(nums, temp, 0, nums.size() - 1);
volver estática_cast seleccionado(res); // cuenta cabe en 32 bits para este problema
}

privado:
largo largo largo de fusiónSortAndCount(std::vector correspondint implicancia nums,
std::vector obtenidosint
int left, int right) {
si (izquierda derecha) devuelve 0;
int mid = left + (right - left) / 2;
largo largo conteo = mergeSortAndCount(nums, temp, left, mid) +
mergeSortAndCount(nums, temp, mid + 1, right);

// Cuenta pares cruzados
int j = mid + 1;
para (int i = izquierda; i) {}
mientras (j <= right ' static_cast seleccionadolong largo(nums[i]) {}
++j;
}
contar += j - (mid + 1);
}

// Merge
int i = izquierda, k = izquierda;
mientras que (i י= mid ' ritmo j
si (nums[i] temp[k++] = nums[i+];
temp[k+] = nums[j++];
}
mientras (i 0= mediados) temp[k++] = nums[i+];
mientras (j < = derecho) temp[k++] = nums[j+];
std::copy(temp.begin() + izquierda, temp.begin() + derecha + 1,
nums.begin() + left);
recuento de retorno;
}
};
`` `

■ **Nota en C++**
■ *El tipo de largo es obligatorio para `2 * nums[j]`.
■ El elenco final a `int` es seguro porque la respuesta es siempre ≤ 1 250 000 000 para `n ≤ 50 000`. *

-...

## 7. Artículo del Blog – “Pases Reversos” (Entrevista-Ley)

■ **Título**: Parejas inversas (LeetCode 493) – El reto de codificación de la última entrevista
■ **Author**: *Tu amigo Algorithm Enthusiast*

-...

### 7.1 Introduction

Los pares inversos parecen engañosamente simples: *“cuenta cuántas veces un elemento es más del doble que aparece más adelante en el array.”*
En realidad es un ejemplo de libro de texto de un algoritmo **divide‐and‐conquer** que prueba la capacidad de un candidato para

* Razón sobre sub-arrays ordenados
* Use traversal de dos puntos
* Evitar los flujos de enteros
* Escriba código limpio, reutilizable

> *Por qué a los reclutadores les encanta* Cubre **time-complexity thinking**, **array manipulation**, y **edge-case handling** – todas las cosas que buscan en un programador de software.

-...

## 7.2 Declaración de problemas (reescrito)

■ **Given** una lista de enteros firmados de 32 bits,
■ **Encuentra** el número de pares índice `(i, j)` tales que `i ' significa j ' y `nums[i] √≥ 2 × nums[j]`.

■ **Constraints**
■ * Longitud del rayo ≤ 50 000*
■ * Los nómeros están en el rango completo de 32 bits firmado. *

-...

### 7.3 "El Bien"

**Merge-sort contando** es la solución canónica:

1. **Sorta** el array por recursión (divide el rango en las mitades).
2. **Mientras que se fusionan**, caminar una vez a través de las mitades izquierda y derecha y contar cuántos pasajes cruzados satisfacen la condición.
3. **Retorno** la suma de los recuentos de todos los niveles recursivos.

■ **Por qué es *bueno*** –
■ *Runs en O(n log n)*, que es el mejor que puede hacer para un array estático.
■ *La implementación es corta ( tómese 70 líneas en la mayoría de los idiomas) y fácil de razonar. *

-...

### 7.4 "The Bad"

Errores comunes que convierten la solución elegante en una implementación de buggy:

* **Overflow**: `2 * nums[j]` debe ser evaluado como 64-bit.
* **Tipo de datos incorrecto para el contador**: La respuesta puede ser de ~1.25 mil millones.
* ** Errores benéficos en el paso de fusión**: Los insectos destruyen la orden.
* **Repetida asignación de amortiguadores temporales**: Tiempo de desperdicio.

-...

### 7.5 “El Ugly” – Cuando tienes que pensar fuera de la caja

1. **Binary Indexed Tree (Fenwick)** – Coordinate‐compress the values, then iterate from right to left inserting into the BIT and querying how many earlier numbers are > 2×current.
2. ** Árbol de segmento** – Similar al TBI pero con más flexibilidad para las consultas de rango.
3. **Divideo recursivo " Conquer (igual que Merge‐Sort)** – Ligero pero más verboso.

Todos ellos alcanzan el tiempo *O(n log n)* o *O(n log n + n log V)*, pero **merge‐sort** es todavía el más *interview‐ready* porque sólo necesita recordar el patrón clásico *inversion‐count*.

-...

## 7.6 ¿Por qué este problema es un tema de gran entrevista

TENIDO Entrevista Focus ANTERIOR Lo que muestra
Silencio.
Silencio ** Pensamiento Algorítmico** Silencio Candidato puede detectar el truco de recuento cruzado. Silencio
La habilidad para escribir una rutina recursiva correcta y una fusión en el lugar. Silencio
Silencio **Edge‐Case Awareness** Silencio Detecta el desbordamiento, gran cuenta, números negativos. Silencio
Silencio **Maestría en Idiomas** Silencio Idiomas diferentes (Java/Python/C++) exigen un manejo diferente de enteros largos. Silencio
Silencio **Tiempo/Space Trade‐offs** Silencioso Discusión sobre `O(n)` array temporal vs. realmente en lugar se fusiona. Silencio

-...

## 7.7 Quick‐ Pruebas de unidad de verificación (para los tres idiomas)

``text
[1, 3, 2, 3, 1] → 2
[2, 4, 3, 5, 1] → 3
[0, 0, 0, 0] → 0
[2147483647, -2147483648] → 1 (comprueba el manejo de desbordamiento)
`` `

■ **Tip for interviewers**: Pida al candidato que pase por la parte *cross‐pair contando* con una pequeña matriz dibujada a mano; expone su modelo mental.

-...

### 7.8 Conclusion " Job‐ Entrevista Takeaway

* **Reverse Pairs** es un problema clásico *(n log n)* divide‐and‐conquer que combina array clasificando con un giro contable.
* Aplicarla correctamente demuestra dominio del pensamiento algorítmico, manejo cuidadoso de los tipos de datos y estilo de código limpio, exactamente lo que los gerentes de contratación están buscando.
* Maestro este patrón, escriba los fragmentos de tres idiomas arriba, y usted estará listo para llegar a la etapa de entrevista de codificación de su próxima búsqueda de trabajo de ingeniería de software.

-...

■ ** Nota de Pro-Recruiter** – “Me di cuenta de que resolvió * Parejas Reversas* eficientemente.” →
■ *Respuesta*: “Usé un enfoque de conteo basado en combinación, evitando cuidadosamente el desbordamiento utilizando enteros de 64 bits. Corre en el tiempo `O(n log n)`, que es esencial para grandes insumos. ”
■ Esto le dice al reclutador que entiende tanto la optimización algorítmica como las persianas prácticas.

¡Feliz codificación y buena suerte en tu próxima entrevista!