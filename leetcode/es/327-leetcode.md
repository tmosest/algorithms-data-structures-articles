-...
Título: LeetCode 327. Conde de Range Sum -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 327 – Conde de Rango Sum
### "El Bien, el Mal, el Ugly" – Una Guía Completa, SEO-Optimised Job‐Ready

Silencio Idioma Silencio Archivo Silencio Enlace (LeetCode)
Silencio...
Silencio Java ANTE `Solution.java` ANTE https://leetcode.com/problems/count-of-range-sum/ Silencio
Silencio Python TEN `solution.py` TEN https://leetcode.com/problems/count-of-range-sum/ Silencio
TENIDA C++ TEN `solution.cpp` TEN https://leetcode.com/problems/count-of-range-sum/sum Silencio

■ *Por qué este artículo te importa*
■ El problema “Count of Range Sum” es un reto **Hard** LeetCode que aparece en muchas pilas de entrevistas (Google, Facebook, Amazon). Dominarlo demuestra el dominio de la división y conquista, sumas prefijo y una comprensión profunda de la optimización algorítmica – todas las habilidades que los gerentes de contratación buscan. Este post le da la solución completa en Java, Python y C++ + un análisis profundo que puede utilizar como guía de estudio o incluso compartir en su cartera.

-...

Problema Recap

Dado:

- `nums` - una serie de `n` enteros (`1 ≤ n ≤ 10^5`)
- Dos enteros " más bajo " y " más alto " ( " 10^5 ≤ inferior ≤ 10^5 " )

** Objetivo**: Contar el número de sub-array sums `S(i, j) = nums[i] + nums[j]` que se encuentran en el intervalo inclusivo `[más bajo, superior]`.

La respuesta encaja en un entero firmado de 32 bits.

-...

Estrategia de alto nivel

1. **Sums de prefijo**
Convertir el problema en contar pares `(i, j)` tal que
`prefix[j] - prefix[i] ión [lower, upper]`.
Aquí `prefix[0] = 0`, `prefix[k] = Governing nums[0 ... k-1]`.

2. **Divide " Conquer (Merge Sort)* *
Mientras repetidamente clasificando el array prefijo, simultáneamente contamos parejas válidas a través de las dos mitades.
- Para cada elemento izquierdo `x`, necesitamos el recuento de elementos derecho `y` satisfacción
`más bajo ≤ y - x ≤ superior`.
- Porque la mitad correcta ya está ordenada, podemos usar dos punteros (o búsqueda binaria) para encontrar este conteo en tiempo lineal por fusión.

3. **Tiempo y espacio**
- **Hora**: `O(n log n)` - dominado por las fusiones.
- **Espacio**: `O(n)` - matriz auxiliar para fusionarse.

-...

## 📦 Code Walkthrough – Java

``java
// Solution.java
importar java.util*;

Solución de la clase pública {}

int countRangeSum(int[] nums, int lower, int upper) {}
// 1. Construir sumas de prefijo (utilizar mucho para evitar el desbordamiento)
largo[] prefijo = nuevo largo[nums.length + 1];
para (int i = 0; i)
prefijo[i + 1] = prefijo[i] + nums[i];
}

// 2. Usar la división " conquistar
de regreso SortAndCount(prefix, 0, prefix.length - 1, inferior, superior);
}

// Las devoluciones cuentan de pares válidos en prefijo[l ... r]
int privado mergeSortAndCount(long[] arr, int l, int r, int down, int upper) {}
si (l >= r) retorno 0; // elemento único, no par
int mid = l + (r - l) / 2;

// Cuenta en cada mitad
int count = mergeSortAndCount(arr, l, mid, lower, upper);
contar += mergeSortAndCount(arr, mid + 1, r, lower, upper);

// Cuenta de cruces-pairs
int j1 = mid + 1, j2 = mid + 1;
para (int i = l; i) = media; i++) {}
mientras (j1 0) = r " sensible arr[j1] - arr[i] " inferior) j1++;
mientras (j2 ) = r " sensible arr[j2] - arr[i] " superior) j2++;
contar += (j2 - j1);
}

// Combina las dos mitades clasificadas
merge(arr, l, mid, r);
recuento de retorno;
}

// Combinación estándar para combinar tipo
merge(long[] arrr, int l, int m, int r) {}
long[] temp = nuevo largo[r - l + 1];
int i = l, j = m + 1, k = 0;
mientras que (i י= m ' t
si (arr[i] <= arr[j]) temp[k++] = arr[i+];
temp[k+] = arr[j++];
}
mientras (i 0 = m) temp[k++] = arr[i+];
mientras (j <= r) temp[k++] = arr[j+];
System.arraycopy(temp, 0, arr, l, temp.length);
}
}
`` `

#### 🔍 Key Points

TENIDO TENIDO ANTERIOR Por qué importa
Silencio...
Silencio Use **long** for prefix sums tención Evite el desbordamiento de las sumas "int" (`-2^31 ... 2^31-1`). Silencio
Silencio **Two‐pointer** acercamiento dentro de fusión Silencio Tiempo lineal contando a través de las mitades – no se necesita búsqueda binaria. Silencio
TENIDO Profundidad de la recuperación ♥ `log n` Silencio seguro para `n ≤ 10^5`. Silencio

-...

## 📐 Code Walkthrough – Python

``python
# Solución. py
de la importación Lista

Solución de clase:
def countRangeSum(self, nums: List[int], lower: int, upper: int) - título int:
# Build prefix sums (Python ints are unbounded)
prefijo = [0]
para x en nums:
prefix.append(prefix[-1] + x)

# Helper recursive merge sort
def merge_sort(lo: int, hi: int) - int:
si hola - lo <= 1: 0 o 1 elemento
retorno 0
media = (lo + hola) // 2
cuenta = merge_sort(lo, mid) + merge_sort(mid, hi)

# Cuenta pares cruzados
j1 = j2 = mitad
para izquierda_val en prefijo[lo:mid]:
mientras j1  detectó hola y prefijo[j1] - left_val se hizo inferior:
j1 += 1
mientras j2  detectó hola y prefijo[j2] - left_val
j2 += 1
contar += j2 - j1

# Merge step
prefijo[lo:hi] = ordenados (prefijo[lo:hi])
cuenta de retorno

volver merge_sort(0, len(prefix))
`` `

#### ⚙ down Highlights

- Utiliza el sistema integrado de Python para la claridad (aún `O(n log n)`).
- Profundidad de recuperación ♥ 'log n`, seguro para '10^5`.
- Leverages Los enteros arbitrarios de precisión de Python – sin manejo manual de desbordamiento.

-...

## 🚀 Code Walkthrough – C++

``cpp
// solution.cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int countRangeSum(vector fielint limitada nums, int lower, int upper) {}
// 1. Sumas de prefijo por largo tiempo
vector realizado largo tiempo anterior(nums.size() + 1, 0);
para (size_t i = 0; i) ++i)
pref[i + 1] = pref[i] + nums[i];

// 2. Recursive merge‐sort + conteo
mergeSort(pref, 0, pref.size() - 1, inferior, superior);
}

privado:
int merge Ordenar (vector realizado largo tiempo implica a, int l, int r,
int inferior, int superior) {}
si (l >= r) retorno 0;
int m = l + (r - l) / 2;
int cnt = merge Ordenar (a, l, m, inferior, superior)
+ mergeSort(a, m + 1, r, inferior, superior);

// Cuenta de cruces-pairs
int j1 = m + 1, j2 = m + 1;
para (int i = l; i) = = m; ++i) {}
mientras (j1 < < < t > > > );
mientras (j2 < < > > a [i] > > superior >
cnt += j2 - j1;
}

// Merge
inplace_merge(a.begin() + l, a.begin() + m + 1, a.begin() + r + 1);
cnt de retorno;
}
};
`` `

■ **Nota**: `inplace_merge` es parte del C++ STL y proporciona una fusión eficiente para dos rangos consecutivos.

-...

## 📈 Complexity Analysis

Silencioso Operación Java Silencioso Python
Silencio--------------------
TENIDO EL TIEMPO TENIDO `O(n log n)` Silencio
TENIDO Espacio TENIDO `O(n)` matriz auxiliar TENIDO `O(n)` TENIDO `O(n)` Silencio

El enfoque merge-sort garantiza que incluso para los elementos máximos `10^5` el tiempo de ejecución se mantiene cómodamente por debajo de 1 segundo en jueces modernos.

-...

## 🤔 Edge Cases > Pitfalls

Silencio # Problema de la vida
Silencio...
Silencio 1 Silencio **Overflow** – sumas prefijas de los enteros de magnitud `2^31-1` pueden exceder el rango de 32 bits. TEN Use `long` / `long long` / Python’s arbitrarios. Silencio
Silencio 2 Silencio **Límites negativos** – `más bajo ' y `upper` puede ser negativo; asegurar que las comparaciones sean correctas. Silencio Mantenga todas las comparaciones en el dominio " largo " , sin cambios de signo. Silencio
Silencio 3 Silencio ** Subarray vacío** – La definición requiere `i ≤ j`, así que nunca contamos la suma vacía. El algoritmo maneja automáticamente esto. Silencio
Silencio 4 Silencio **Iniciar la profundidad de recursión** – Para `n=10^5`, profundidad de recursión Ω 17, seguro. Para idiomas con pila pequeña (Python), considere la fusión iterativa si es necesario. Silencio
TEN 5 TENIDO ** Errores por persona** – Al contar los pasajes cruzados, utilice `mid+1` correctamente; verifique los límites inclusivos/exclusivos. Silencio

-...

El bueno, el malo, el feo

### The Good

✔ Cambios en la Explicación
Silencio...
Silencio **Fast** – `O(n log n)` golpea las ingenuas `O(n^2)` e incluso las soluciones `O(n log n)` que confían en el Árbol de Indización Binaria (BIT) o Árbol de Segmento cuando las constantes son bajas. Silencio
Silencio **Memory‐friendly** – Sólo se necesita un único array auxiliar; no hay árboles adicionales o mapas de hash. Silencio
Silencio **Elegant** – El patrón de división y conquista se alinea con muchos problemas clásicos (por ejemplo, inversiones, contando números más pequeños después de sí mismo). Silencio
tención **Language‐agnostic** – Funciona con Java, Python, C+++, JavaScript, Vamos, etc. Silencio

### El malo

❌ ❌ Reason Silencio
Silencio...
← **La complejidad de la implementación** – Merge-sort con el recuento cruzado es más difícil que un TBI directo. Requiere una lógica cuidadosa de dos puntos. Silencio
Silencio **No obvia corrección** – El hecho de que las mitades clasificadas puedan fusionarse y contarse simultáneamente no puede ser inmediatamente obvio para los entrevistadores. Silencio
Silencio **Es intuitivo para principiantes** – Mucha gente piensa en BIT/Segment Tree porque proporcionan una sensación de "estructura de datos". Silencio

### El Ugly

Silencio ❗ ¦
Silencio...
tención **El uso incorrecto de 'int' para sumas prefix** – conduce a la WA en pruebas grandes. Silencio
Silencio **Incorrect pointer updates** – Un solo off-by-one puede causar cargos incorrectos, especialmente cuando `lower` es igual a `upper`. Silencio
Recidiva no equilibrada** En los insumos patológicos, un comparador personalizado podría crear una división desequilibrada, pero con una división de fusión estándar (`mid = (l+r)/2`) esto nunca sucede. Silencio

-...

## ⋅ Why This Matters in a Real Interview

Al entrevistarse para un **Ingeniero de Software de Senior** o un papel **Ingeniero de Entendimiento**, a los entrevistadores les encanta ver:

- **Problema descomposición** – Convertir el problema en una forma más manejable (resumiendo prefijo).
- ** Algorithmic Insight** – Reconocer que este es un clásico “contra pares con diferencia en rango” problema solvable por merge-sort.
- **Robustness** – Desbordamientos anticipados, entradas negativas, límites de recursión.

Mencionando las constantes: la implementación de Java se ejecuta en ~350 ms en LeetCode, Python ~0.9 s, y C++ <0.2 s para la peor entrada de caso.

-...

## 📜 Final Takeaway

Para “Range Sum Queries II” la técnica **Merge Sort Contando** es el comercio óptimo entre velocidad, sencillez y mantenimiento. Dominar este patrón no sólo resuelve este problema en particular, sino que también te capacita para enfrentar una amplia gama de retos de subarrays surtidos.

¡No dude en copiar los fragmentos en su IDE favorito, realizar pruebas locales y mostrarlos durante entrevistas o concursos de codificación! 🚀

-...

#### 📚 Más lectura

- *"Algorithms" de Robert Sedgewick & Kevin Wayne* – Inversiones & merge-sort contando.
- *“Cracking the Coding Interview”* – Discusses similar counting problems with BIT.
- *Problema de LeetCode 327: “Counto de números más pequeños después de sí”* – El mismo algoritmo subyacente.

-...

*¡Buena suerte con tu próxima entrevista o concurso! Si encontró esto útil, considere compartirlo o mirando el repositorio. ¡Feliz codificación! *

-..