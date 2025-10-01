-...
Título: LeetCode 2387. Mediana de una matriz clasificada de alambre de fila -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Panorama general de los problemas
**LeetCode 2387 – Mediana de una matriz clasificada en fila* *
■ *Given an odd-sized `m × n` matriz (`m` y `n` son ambos raros) donde cada fila se clasifica en orden no-disminución, devuelve la mediana de todos los elementos `m·n`. *

■ ** Objetivo** – encontrar la mediana en **O(m·log n · log V)** tiempo, donde `V` es la gama de valores (≤ 106), es decir, mucho mejor que la ingenua exploración `O(m·n).

-...

## 2. ¿Por qué una búsqueda binaria en el espacio *valor*?
* Cada fila está clasificada → podemos contar “cuántos números son ≤ X” en O(log n) con búsqueda binaria.
* La mediana es el menor número `X` tal que al menos la mitad de los elementos son ≤ X.
* Si podemos responder rápidamente “¿Cuántos elementos ≤ X?” podemos realizar una investigación binaria sobre el espacio *valor* (del mínimo global al máximo global).

Esta estrategia es la búsqueda *binaria clásica sobre el patrón de respuesta*.

-...

## 3. Algoritmo (High‐Level)

1. **Determine search bounds* *
* `low` = elemento más pequeño en la matriz (primer elemento de cada fila).
* `alta ` = elemento más grande en la matriz (último elemento de cada fila).

2. **Binary search on values**
Mientras 'bajo' se hizo alto ':
* `mid = (bajo + alto) / 2`
* < cnt = cuenta de la egaRow(row, mid)` - número de elementos en la matriz ≤ mediados.
* Si `cnt ecto (m·n +1)/2` → median es ** más grande ** conjunto `low = mid + 1`.
* Else → mediana es **≤** mediados → conjunto `alta = medio `.

3. Regresar 'bajo' (o 'alto') - la mediana.

**countRow(row, mid)** es una búsqueda binaria estándar (`upper_bound`) devolver el primer índice donde el elemento > mid. El índice devuelto equivale al número de elementos ≤ a mediados de esa fila.

-...

## 4. Prueba de corrección

Demostramos que el algoritmo devuelve la verdadera mediana.

### Lemma 1
Para cualquier integer `x`, `cnt(x) = gia_i upper_bound(row_i, x)` equivale al número de elementos de matriz ≤ x.

*Proof. *
Porque cada fila está ordenada, 'upper_bound' devuelve el índice del primer elemento estrictamente mayor que `x`. Todos los elementos antes de ese índice son ≤ x. Resumiendo en filas cuenta todos los elementos de la matriz ≤ x. ∎

### Lemma 2
Dejar `k = (m·n + 1)/2 ' (la posición de la mediana en orden ordenado).
Si `cnt(mid) < k`, entonces el median √ mid; si `cnt(mid) ≥ k`, entonces el median ≤ medio.

*Proof. *
`cnt(mid)` cuenta cuántos elementos son ≤ mediados.
* Si menos de los elementos 'k' son ≤ mediados, entonces el elemento `k`‐th (el medio) debe ser más grande que `mid`.
* Si al menos los elementos 'k' son ≤ mediados, entonces el elemento 'k`‐th no puede ser más grande que 'mid'.

### Lemma 3
Durante la búsqueda binaria el invariante
`bajo' es siempre ≤ mediana y 'alto' es siempre ≥ mediana sostiene.

* Prueba por inducción. *
*Base*: Inicialmente, `bajo ' es el mínimo global y `alto' el máximo global; la mediana se encuentra entre.
*Paso*:
- Si 'cnt(mid)' se hizo k` → por Lemma 2 median mediados de → establecemos `bajo = medio +1`. Desde la mediana, "bajo" queda ≤ mediana.
- Else (`cnt(mid) ≥ k`) → mediana ≤ mediados → nos fijamos `alto = medio `. Desde `mid ≥ median ' , `alta ' permanece ≥ median. ∎

### Theorem
Cuando el bucle termina (`low == high`), el valor devuelto equivale a la mediana matriz.

*Proof. *
Por Lemma 3 el intervalo de búsqueda siempre contiene la mediana. La cancelación sólo ocurre cuando el intervalo se contrae a un solo valor. Ese valor único debe ser la mediana porque ningún valor menor puede satisfacer la condición mediana ( " cnt " ) y ningún valor mayor puede satisfacer " cnt ≥ k " . ∎

-...

## 5. Análisis de la complejidad

*Seamos el número de filas, `n` el número de columnas. *

Silencio Silencio Silencio Silencio Silencio Silencio
Silencio--------------------
TENIDO Encontrar `low '/`high ' TENIDO Scan first ' last elements of each row TENIDO `O(m)` Silencio
TENIDO Cada iteración de búsqueda binaria ANTERIOR Para cada una de las filas de `m` realizan `upper_bound` (`O(log n)`) Silencio `O(m·log n)` Silencio
tención Número de iteraciones donde `range ≤ 106` → ≤ 20 (Ω log2(106) Silencioso `O(log V)`

Tiempo total: `O(m·log n·log V)` ♥ `O(m·log n)` para las limitaciones dadas.
Espacio: `O(1)` – sólo algunas variables entero.

-...

## 6. Aplicación de las referencias

A continuación encontrará **ready‐to‐copy** código en **Java, Python, y C+**. Cada aplicación sigue el algoritmo descrito anteriormente y contiene comentarios en línea para la claridad.

### 6.1 Java (LeetCode-compatible)

``java
importar java.util*;

Clase Solución {
int public int matrizMedian(int[] grid) {
int m = grid.length, n = grid[0].length;

// 1. Encuentra min global y máx
Int bajo = Integer. MAX_VALUE;
int high = Integer.MIN_VALUE;
para (int[] fila : rejilla) {
bajo = Math.min(bajo, fila[0]); // primer elemento de una fila ordenada
alta = Math.max(alto, fila[n - 1]); // último elemento
}

int target = (m * n + 1) / 2; // k-th elemento en orden

// 2. Búsqueda binaria en el rango de valor
mientras (bajo)
int mid = low + (high - low) / 2;

int count = 0;
para (int[] fila : rejilla) {
cuenta += superiorBound(row, mid); // #elements ≤ mediados de esta fila
}

si (cuenta)
baja = media + 1; // mediana es mayor
. ♫ ... {
alta = mediana; // mediana es ≤ mediados
}
}
baja de retorno; // baja == alta
}

/** devuelve el primer índice de destino de usuario (es decir, conteo de elementos ≤ objetivo) */
int privado superiorBound(int[] arr, int target) {}
int lo = 0, hola = arr.length; // hola es exclusiva
mientras (lo cautivado) {
int mid = (lo + hola) 1;
si (arr[mid] <= target) lo = mid + 1;
más hola = medio;
}
devolver lo;
}
}
`` `

-...

### 6.2 Python

``python
de la importación de bisect_right
de la importación Lista

Solución de clase:
matriz de defMedian(self, grid: List[List[int]] int:
m, n = len(grid), len(grid[0])

# Global bounds
bajo = min(row[0] for row in grid)
alto = max(row[-1] for row in grid)

objetivo = (m * n + 1) // 2

mientras que bajo
media = (bajo + alto) // 2
cuenta = sum(bisect_right(row, mid) for row in grid)

si se cuenta el objetivo:
baja = media + 1
más:
alta = media

Regreso bajo
`` `

-...

### 6.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int matricidadMedian(vector identificadovector identificadoint
int m = grid.size(), n = grid[0].size();

int low = INT_MAX, high = INT_MIN;
para (contigo auto-plaza fila : rejilla) {
bajo = min(bajo, row.front());
alto = máximo (alto, fila.back());
}

int target = (m * n +1) / 2;

mientras (bajo)
int mid = low + (high - low) / 2;
int count = 0;
para (contigo auto-plaza fila : rejilla) {
contar += superior_bound(row.begin(), row.end(), mid) - row.begin();
}

si (cuenta de blanco) bajo = medio + 1;
más alto = medio;
}
Retorno bajo;
}
};
`` `

-...

## 7. Blog Post – * “El Bien, el Mal, y el Ugly of Finding the Median in a Row‐Wise Sorted Matrix”*

## 7.1 Why This Problem Matters (SEO keywords: *algorithm interview, binaria search, matriz median, coding interview, LeetCode 2387*)

Cuando los reclutadores preguntan "¿Cómo encontrarías la mediana de una matriz clasificada?" realmente están probando tres competencias básicas:

1. ** Pensamiento Algorítmico** – ¿Puede usted encontrar la oportunidad de búsqueda binaria en *valores* en lugar de índices?
2. ** Conciencia de la complejidad** – ¿Conoces el tiempo/espacio de compensación frente a búsqueda?
3. **Implementation Skill** – ¿Puede traducir una idea concisa en código de producción?

Una respuesta bien hecha a este problema demuestra los tres y gana puntos brownie en su próxima entrevista de instrucciones de datos.

-...

## 7.2 El Bien - Lo que hace que este problema sea una Goldmine

Por qué es bueno
Silencio----------
Silencio **Asunado por cable** Silencio Permite *log‐n* búsquedas por fila. Silencio
Silencio **Odd dimensions** Silencio Garantiza un medio único (no se necesitan reglas para romper corbatas). Silencio
Silencio **Cantidad mínima de valor (≤ 106)** tención Permite la búsqueda binaria en el rango de valor en un número constante de iteraciones. Silencio
tención **Scalable** tención Funciona para 500×500 matrices (elementos de 250k) en menos de un milisegundo. Silencio
Silencio **Reusable** Silencio El patrón de “búsqueda binaria en respuesta” se aplica a muchas preguntas de entrevista (kth mayor, matriz dividida, etc.). Silencio

-...

### 7.3 Los malos – saltos comunes

Silencio Pitfall Silencio Cómo evitarlo
Silencio...
Silencio **Usar el escaneo lineal** Silencio `O(m·n)` es demasiado lento; asegúrese de que no está iterando sobre cada elemento al contar. Silencio
Silencio **Using `mid = (low + high) / 2` sin guardia de desbordamiento** tención Para grandes rangos, prefiera `low + (high - low) / 2`. Silencio
Silencio **Misinterpreting the median position** Silencio Con `m·n` odd, target = `(m*n +1)/2`. Los errores desactivados por uno producen respuestas incorrectas. Silencio
Silencio **Ignorando que cada fila está clasificada** Silencio Si tratas de combinar filas ingenuamente, pierdes el beneficio 'log n`. Silencio
Silencio **No use `upper_bound` correctamente** Debe devolver el conteo de elementos ≤ mediados, no se realizó a mediados. Silencio

-...

## 7.4 The Ugly – Edge Cases That Trip You Up

Silencioso Caso Edge ¿Por qué es complicado ← Quick Fix
Silencio------------------------------
Silencio **Todas las hileras idénticas** tención La búsqueda binaria todavía funciona, pero muchos valores medios darán el mismo recuento. Silencio No se necesita ningún cambio – el algoritmo converge correctamente. Silencio
Silencio **Matrix con muy pequeña gama (por ejemplo, todos los números son 1) ** Silencio El bucle sigue funcionando ~20 veces pero siempre encuentra la respuesta rápidamente. Silencio Mantenga el mismo 'log V' atado. Silencio
Silencio **Large integers close to `int` max/min** tención Overflow in `mid` calculation or `target` multiplication. Uso `largo' (C++/Java) o seguro aritmético (`(bajo + alto) 1`). Silencio
Silencio **Matrimonio cuadrado (m ل n)** Silencio Las personas a veces usan erróneamente `n` para ambas dimensiones. TENIDA Computar explícitamente `target = (m*n +1)/2`. Silencio
Silencio ** Valores negativos** tención El rango de valor podría ser negativo; garantizar negativos de captura bajos y altos. El algoritmo maneja los negativos automáticamente porque el rango está definido por elementos de primera / última. Silencio

-...

### 7.5 How to Nail It in Your Interview

1. **Explicar la *búsqueda binaria en la respuesta* idea** antes de escribir cualquier código. Mostrar el invariante que el intervalo de búsqueda siempre contiene la mediana.
2. **A través de un pequeño ejemplo** en la pizarra (por ejemplo, una matriz 3×3). Mostrar cómo cambia el intervalo y cómo se contrae.
3. **Conducir la implementación** (pick one of the reference solutions above). Mencione las funciones clave (`upper_bound`, `bisect_right`) y por qué son O(log n).
4. **Mención de la complejidad del tiempo/espacio** sucintamente: `O(m·log n)` tiempo, `O(1)` espacio.
5. **Agregue una pequeña optimización** – en Java/C++ puede pre-storear los primeros y últimos elementos de cada fila para evitar escanear toda la fila al encontrar límites.

-...

## 7.6 Pensamiento Final - ¿Por qué Mastering Esto te da un borde competitivo

*LeetCode Mastery*: Solving LeetCode 2387 eficientemente te pone en el percentil superior de problemas de matriz.
- Interview Confidence**: Usted sabrá cómo pivotar de la clasificación ingenua a una solución logarítmica.
- **Problema‐Solving Reputation**: El equipo recordará su elegante utilización de la búsqueda binaria en un rango de valor – un patrón que recordarán en futuras entrevistas.

-...

## 7.7 Call‐to‐Action (SEO: *coding interview preparation, median algoritmo, binaria search matriz, interview tips*)

■ ¿Quieres ver cómo esta solución se acumula contra el enfoque “Merge‐K-sorted‐arrays”? Sumérgete en el repositorio **GitHub** conectado a continuación, donde cada versión de idioma viene con un arnés de prueba y métricas de rendimiento.

**GitHub**: https://github.com/yourusername/matrix-median-impl

-...

## 8. Nota de clausura

Dominar el problema de mediana en matrix es un *show‐stopper* en entrevistas técnicas. Con la **búsqueda binaria en la estrategia de respuesta**, usted puede resolverlo en el tiempo sub-cuadratico y demostrar comprensión profunda de patrones algorítmicos. Utilice el código de referencia anterior para practicar, establecer puntos de referencia y luego explicar la solución claramente a cualquier panel de entrevistas. ¡Buena suerte!

-...

*No dude en adaptar el blog a su estilo o añadir secciones adicionales como “Alternative Solutions (heap, divide‐and‐conquer)” si lo desea. ¡Feliz codificación! *

-...

■ *Si te gustó este post, considera suscribir para más guías de entrevistas de algoritmo, tutoriales de codificación y contenido de preparación de entrevistas. *

-...

**End of Documentation* *