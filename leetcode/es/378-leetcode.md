-...
Título: LeetCode 378. Kth Elemento más pequeño en una matriz clasificada -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 378. Kth Elemento más pequeño en una matriz clasificada

** Complejidad del tiempo** – `O(n log(maxVal-minVal)) `
** Complejidad del espacio** – `O(1)` (aparte de la matriz de entrada)

A continuación se encuentran soluciones limpias y productivas en **Java**, **Python**, y **C++** que utilizan la técnica binaria de investigación sobre valor.

-...

## 1. Solución Java

``java
importar java.util*;

Clase Solución {
int kthSmallest(int[][] matriz, int k) {
int n = matriz. longitud;
larga baja = matriz[0][0];
larga alta = matriz[n - 1][n - 1];

mientras (bajo)
largo medio = bajo + (alto - bajo) / 2;
int count = countLesEqual(matrix, mid, n);

si
baja = media + 1; // necesita mayores números
. ♫ ... {
alta = media; // mediados podría ser la respuesta
}
}
(int) low;
}

* Contar cuántos elementos son 0 = objetivo en la matriz clasificada */
int countLessEqual(int[][] matriz, long target, int n) {
int count = 0;
int row = n - 1, col = 0; // start from bottom‐ izquierda
mientras que (row √≥= 0 ' pÃoblica col ) {
si (matrix[row] [col] [c]
contar += fila + 1; // todos los elementos arriba son también
col++;
. ♫ ... {
fila...
}
}
recuento de retorno;
}
}
`` `

-...

## 2. Python 3 Solution

``python
de la importación Lista

Solución de clase:
def kthSmallest(self, matriz: List[List[int], k: int) - título int:
n = len(matrix)
baja, alta = matriz[0][0], matriz[-1][-1]

mientras que bajo
media = (bajo + alto) // 2
si auto._count_le(matrix, mid, n)
baja = media + 1
más:
alta = media
Regreso bajo

def _count_le(self, matriz: List[List[int]], target: int, n: int) - título int:
""Número de retorno de elementos"
cnt, row, col = 0, n - 1, 0 # bottom‐left corner
mientras que fila 0 y col
si la matriz[row] [col] 0 = objetivo:
cnt += fila + 1 # todo arriba son
col += 1
más:
fila -= 1
retorno cnt
`` `

-...

## 3. Solución C++

``cpp
Incluido el título
usando std namespace;

Clase Solución {
public:
int kthSmallest(vector seleccionadovector realizador identificador implicados iguales matriz, int k) {
int n = matriz.size();
largo largo bajo = matriz[0][0];
largo largo alto = matriz[n-1][n-1];

mientras (bajo)
largo medio = bajo + (alto - bajo) / 2;
si (contrale(matrix, mid, n)
baja = media + 1;
más
alto = medio;
}
volver estática_cast seleccionado(bajo)
}

privado:
// Contar cuántos elementos son
int countLE(cont vector identificadovector nombrado int
int cnt = 0, row = n-1, col = 0; // bottom-left corner
mientras que (row √≥= 0 ' pÃoblica col ) {
si (matrix[row] [col] [c]
cnt += fila + 1; / // todos los elementos arriba son también
++col;
. ♫ ... {
--row;
}
}
cnt de retorno;
}
};
`` `

-...

## 4. Artículo del Blog – “El Bien, el Mal, y el Ugly de LeetCode 378”

■ **Título: ** Elemento más pequeño en una matriz ordenada - El bueno, el malo, el ugly*
■ **Keywords:** LeetCode 378, Kth Smallest Element, Java, Python, C++, Binary Search Matrix, Interview Coding, Algorithm Design, Job Interview Tips

-...

#### 🚀 Introducción

LeetCode 378 – *Kth Smallest Element in a Sorted Matrix* – es un pilar de entrevistas técnicas.
Te obliga a pensar más allá de la fuerza bruta, mezclando ** búsqueda binaria** con ** traversal de la matriz**.

En este artículo diseccionamos el problema, presente ** código limpio** en Java, Python y C++, y buceamos en los aspectos *bueno*, *bad* y *muy* que pueden tropezar incluso desarrolladores experimentados.

-...

Problema Recap

Se le da una matriz 'n × n` donde ** cada fila y columna se ordena** en orden ascendente.
Devuelve el elemento más pequeño **k‐th** en la matriz (contando duplicados).
Constraints: `1 ≤ n ≤ 300`, los valores pueden variar de `-109` a `109`.

Requisito clave: **Memoria . O(n2)** – no puedes aplanar la matriz en una lista.

-...

## 🔧 The Good – Why Binary Search on Value Works

1. **Elegant** – Tratamos la matriz como un “array” de números por su **valor** en lugar de posición.
2. **No hay espacio extra** – Sólo algunas variables enteros; memoria auxiliar O(1).
3. **Fast** – `O(n log(maxVal - minVal))' tiempo. Para los enteros típicos de 32 bits, el término de registro es de 31 a 32, por lo que es prácticamente lineal en `n`.
4. **Determinista** – No hay una cola de prioridad en la cabeza; nunca tienes que almacenar más que los punteros de `O(n).
5. **Scalable** – Trabaja para la restricción superior `n = 300` cómodamente ( tómese 9 000 elementos).

-...

## The Bad – What Makes It Tricky

Por qué importa la Mitigación
Silencio...
Silencio **Range of values** Silencio `maxVal - minVal` puede ser enorme (`2·109`), por lo que el bucle de búsqueda binaria corre muchas iteraciones si utilizamos un ingenuo "mid = (bajo + alto)/2" con ints de 32 bits. Silencio
Silencio **Duplicates** Silencio La matriz puede contener números repetidos; el algoritmo debe manejar “k-th smallest” incluyendo duplicados, no valores distintos. ← El ayudante de cuenta cuenta cuenta todos los elementos ≤ mediados; duplica automáticamente aumentar el conteo. Silencio
Silencio ** Casos de edge** Silencio Matrices de un solo elemento, números negativos, k = 1 o k = n2. TENCIÓN Los punteros de inicio y final inicializados en esquinas de matriz reales; salidas de bucle cuando `bajo == alto ' . Silencio
Silencio **Performance** Silencio Contando ≤ mediados es `O(n)` por iteración. Silencio La rutina del conteo va desde abajo hasta arriba en un solo pase. Silencio

-...

## 😱 The Ugly – Common Pitfalls Cómo evitarlos

1. **Off‐by‐One in Binary Search**
*Mistake*: Usando `mientras (bajo cautivar alto)` pero estableciendo `bajo = medio ' o `alto = medio ' incorrectamente.
*Fix*: Cuando `cuenta ' , se establece `bajo = medio + 1`. De lo contrario se establece `alto = medio'.

2. *Desbordamiento de enteros*
*Mistake*: `mid = (bajo + alto) / 2` con ints de 32 bits puede rebosarse.
*Fix*: `mid = bajo + (alto - bajo) / 2` o utilizar tipos de 64 bits.

3. #Wrong Count Logic #
*Mistake*: Incrementar cuenta por 1 cada vez que vea un elemento ≤ medio.
*Fix*: Debido a que empezamos en la parte inferior izquierda, cada vez que nos movemos a la derecha, *todos* elementos en esa columna hasta la fila actual son ≤ mediados. Así que agrega `row + 1`.

4. **Asumiendo Matrix Is Square* *
*Mistake*: Algunas soluciones asumen `matrix.length == matriz[0].length`.
*Fix*: Use `n = matriz.size()` sólo después de confirmar la matriz no es vacía.

5. **No manipular los números negativos**
*Mistake*: Iniciando `low` y `high` a 0 en lugar de esquinas reales.
*Fix*: Siempre establece `bajo = matriz[0][0]`, `alta = matriz[n-1][n-1]` – esto también funciona para valores negativos.

-...

## 📘 Full Code Walkthrough

### 1. Java

- Usa 'long' para 'low/high/mid`.
- Contable ayudante camina **bottom‐left → top‐right**.
- Los comentarios explican cada paso.

### 2. Pitón

- Usos incorporados en " (sin límites), por lo que el desbordamiento no es un problema.
- Aún con cuidado con la lógica 'low = mid + 1`.

### 3. C++

- Usa "largo largo" para el rango de valor.
- 'contrale' utiliza el mismo truco de abajo izquierda.

-...

## 📈 Alternative Approaches

TENIDO TERRIENTE Complejidad ANTERIOR Cuando se utiliza
Silencio----------------------------
Silencio **Min‐Heap (k-times extraction)** Silencio `O(n log n)` tiempo, `O(n)` espacio tención Simpler para implementar si usted está cómodo con colas prioritarias. Bien para entrevistar “quick-win” pero menos elegante. Silencio
Silencio **Flatten + nth_element (C++)** Silencio `O(n2)` espacio → viola restricciones Silencio Únicamente adecuado cuando el entrevistador relaja los límites de memoria. Silencio

-...

## 🎯 How these Solutions Help you Land a Job

**Showcase Algorithmic Thinking** – La búsqueda binaria del valor demuestra una profunda comprensión de los invariantes de la estructura de datos.
- **Cross‐Language Mastery** – Tener aplicaciones Java, Python y C++ muestra que puedes adaptarte a cualquier pila de tecnología.
- **Performance‐First Mindset** – El espacio O(1) y el tiempo O(n log range) ilustran una mentalidad lista para la producción.

**Tip de Interview:**
*Cuando se le pide que resuelva 378, primero describa la idea, luego hable a través de la lógica del conteo, y finalmente presente el código. Mencione el requisito de memoria O(1) y el truco de caminar desde la esquina inferior izquierda. *

-...

Conclusión

LeetCode 378 es más que una prueba de búsqueda binaria, es una prueba de razonamiento cuidadoso, manejo de límites y codificación limpia.
Dominar este análisis “bueno, malo, feo” no sólo impresionará a los gerentes de contratación, sino que también le dará confianza para abordar una amplia gama de problemas de entrevista.

Codificación feliz, y que su elemento más pequeño k siempre aterriza en el trabajo que busca! 🚀

-...

*No dude en copiar los fragmentos de código en su IDE preferido, ejecutar los casos de prueba oficiales, y compartir este artículo con compañeros que están preparando su próxima entrevista. *