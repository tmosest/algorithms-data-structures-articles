-...
Título: LeetCode 2428. Suma máxima de un reloj de reloj -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# ✅ 2428. Maximum Sum of an Hourglass – 3‐Way Solutions + SEO‐Optimized Blog

■ ** Objetivo** – Resolver el problema LeetCode *Suma Máximo de un reloj* en **Java**, **Python**, y **C+**.
■ **Bonus** – Una publicación de blog amigable de SEO que explica el “Good, Bad y Ugly” del problema, te ayuda a entrevistarte y mejora tu presencia en línea.

-...

## 1. El Código

■ **Las tres implementaciones se ejecutan en tiempo O(m × n) y O(1) espacio auxiliar** – perfecto para limitaciones de entrevista.

#### 1.1 Java

``java
// 2428. Suma máxima de un reloj de reloj – Java (O(m*n) tiempo, espacio O(1))
Clase Solución {
int public int maxSum(int[] grid) {
int m = grid.length, n = grid[0].length;
int best = 0; // Todos los valores no son negativos
para (int i = 1; i) Fila media de reloj de hora
para (int j = 1; j) Columna media
int sum = grid[i-1][j-1] + grid[i-1][j] + grid[i-1][j+1]
+ grid[i][j]
+ grid[i+1][j-1] + grid[i+1][j] + grid[i+1][j+1];
mejor = Math.max(mejor, suma);
}
}
devolver mejor;
}
}
`` `

■ *Por qué funciona*: Recorrimos cada posible “centro” de un reloj de hora (es decir, el elemento medio). El reloj de hora es siempre 3×3, por lo que la suma es un patrón fijo. No se necesitan estructuras de datos adicionales.

### 1.2 Python

``python
# 2428. Suma máxima de un reloj de reloj – Python (O(m*n) tiempo, espacio O(1))
Solución de clase:
def maxSum(self, grid: List[List[int]) - int:
m, n = len(grid), len(grid[0])
mejor = 0
para i en rango(1, m - 1):
para j en rango(1, n - 1):
s =
grid[i-1][j-1] + grid[i-1][j] + grid[i-1][j+1]
+ grid[i][j]
+ grid[i+1][j-1] + grid[i+1][j] + grid[i+1][j+1]
)
mejor = max(best, s)
mejor
`` `

■ *Pythonic tip*: Use `range(1, m-1)` para saltar las filas/collos fronterizos que no pueden albergar un reloj de arena.

#### 1.3 C++

``cpp
// 2428. Suma máxima de un reloj de reloj – C++ (O(m*n) tiempo, espacio O(1))
Clase Solución {
public:
int maxSum(vector seleccionadovector fielint ánimo limitado) {
int m = grid.size(), n = grid[0].size();
int best = 0; // todos los elementos 0
para (int i = 1; i)
para (int j = 1; j)
int sum =
grid[i-1][j-1] + grid[i-1][j] + grid[i-1][j+1]
grid[i][j] +
grid[i+1][j-1] + grid[i+1][j] + grid[i+1][j+1];
mejor = max(best, sum);
}
}
devolver mejor;
}
};
`` `

■ *Por qué es rápido*: No hay asignación de memoria dinámica, sólo aritmética simple entero.

-...

## 2. SEO‐Optimized Blog Artículo

■ **Título**: El Bien, el Mal, y el Ugly of Solving LeetCode 2428 – *Suma Máximo de un reloj de arena*
■ **Meta‐Description**: Maestro el problema de LeetCode 2428 horas de vidrio en Java, Python y C++. Aprenda mejores prácticas, trampas comunes y estrategias de entrevista para aterrizar su próximo rol de ingeniería de software.
■ **Keywords**: LeetCode 2428, Maximum Sum of an Hourglass, entrevista de codificación, entrevista de trabajo, algoritmo, Java, Python, C++, entrevista de codificación, estructura de datos, complejidad del tiempo, complejidad del espacio.

-...

#### 📌 Problema general

LeetCode 2428 le pide que computar la suma máxima de un 3×3 "horaglass"** en una matriz *m × n*:

`` `
ab
d
e f
`` `

* Un reloj de arena no se puede girar.
* Debe encajar completamente dentro de la matriz.
* Todos los valores son no negativo (0 ≤ grid[i][j] ≤ 106).

**Constraints* *
3 ≤ m, n ≤ 150 → ≤ 22500 celdas → los bucles simples anidados son lo suficientemente rápido.

-...

### ش The Good – A Clean, Interview‐Ready Approach

1. ** Índices de bucle intuitivos**
* Iterate over the *center* `(i, j)` of every hourglass: `i  Iberia [1, m-2]`, `j  Iberia [1, n-2]`.
* Esto excluye automáticamente las células fronterizas que no pueden albergar un reloj completo.

2. **Cálculo de la suma dividida* *
* Computar explícitamente las 7 celdas; no hay estructuras de datos adicionales.
* `sum = top Fila + media + inferior Row`.

3. **Espacio auxiliar constante**
* Sólo unas pocas variables enteros ( " mejor " , " ).
* Perfecto para entrevistadores que buscan código espacial eficiente.

4. *Edge-case safety*
* Debido a que todos los valores no son negativos, inicializando obras `mejores = 0`.
* Si se permitían los negativos, establece `mejor = INT_MIN` / `-inf`.

5. *La complejidad del tiempo*
* `O(m × n)` – cada célula se considera un número constante de veces.
* Con *m, n* ≤ 150, el peor es 22 500 iteraciones – trivial.

-...

## ## Глали los malos – saltos comunes

¿Por qué no se puede arreglar la vida?
Silencio--------------------------
Silencio ** Inclusión de las celdas fronterizas** Silencio tratando de acceder a `grid[i-1][j-1]` cuando `i=0` o `j=0` → `ArrayIndexOutOfBounds`. Silencio `i` from `1` to `m-2`; `j` from `1` to `n-2`. Silencio
Silencio **Asumiendo valores negativos** Silencio Iniciando `best = 0` da respuesta incorrecta si todos los números son negativos. Silencio Inicializarse para `inf` o `INT_MIN`. Silencio
Silencio **Using O(n2) space** Silencio Pre-computing prefix sums or a DP table for no benefit; wastes Memory. Mantener el espacio constante. Silencio
En Java/C++, el `int` podría desbordarse si los valores eran mayores. Use `long` si usted anticipa sumas > 231‐1 (no es necesario aquí). Silencio

-...

### 🐞 The Ugly – Over-Optimization Traps

1. Prefix Sum Overkill**
* Algunas soluciones pre-computan una suma de prefijo 2D y luego deslizan una ventana.
* Mientras funciona, añade espacio *(m × n)* y un bucle de 2 niveles para cada reloj de arena – innecesario.

2. **Bolte-Force recursivo**
* Repetidamente recurriendo a la cuadrícula para elegir 7 células es lenta y apilada.
* Los entrevistadores esperarán un bucle **plain**.

3. **Micro-optimizing Inner Loop**
* Usando arrays temporales para mantener rebanadas de fila.
* Complica el código sin una ganancia de velocidad mensurable en este tamaño.

**Bottom line:** La simplicidad gana. Los entrevistadores valoran código limpio y legible que resuelve el problema dentro de las limitaciones.

-...

### 🎯 Takeaways for the Job Interview

TENCIÓN ANTERIOR Por qué importa
Silencio...
Silencio **Explicar los límites del bucle** Silencio Muestra comprensión de índices de matriz. Silencio
Silencio ** Tiempo de mención/complejidad espacial** Silencio Demuestra el pensamiento algoritmo. Silencio
tención **Mostrar la conciencia de los casos de bordes** ← Destaca la robustez. Silencio
Silencio **Discúlpese por qué eligió esta solución** Silencio Revela las decisiones de diseño. Silencio
tención **Hablar sobre pruebas** tención Casos de esquina Mención: matriz 3×3, todos los ceros, números mixtos. Silencio

**Consejo:** Después de escribir la solución, caminar a través de un ejemplo rápido con una pequeña matriz. Los entrevistadores les encanta ver el código en acción.

-...

Recursos adicionales

- [Problema de LeetCode 2428 - Suma máxima de un reloj de arena](https://leetcode.com/problems/maximum-sum-of-an-hourglass/)
- [Los panes de debate (Java/Python/C+++)](https://leetcode.com/problems/maximum-sum-of-an-hourglass/solutions/)
- [Entreview Warm‐Up: 2‐D Array Problems](https://www.educative.io/courses/leetcode-interview-preparation/4)

-...

## 🚀 Palabras finales

Resolver *Maximum Sum of an Hourglass* es una victoria rápida para su kit de herramientas de entrevista.
- **Java**: Mostrar maestría de arrays y bucles.
- **Python**: Destacar la sintaxis concisa y la legibilidad.
- **C+**: Demostrar la conciencia de rendimiento y el uso de STL.

Utilice esta solución, hable a través de la “buena, mala, fea”, y impresionará a cualquier entrevistador, ya sea que esté aplicando en una startup o una compañía Fortune 500.

¡Feliz codificación y buena suerte en tu próxima búsqueda de trabajo! 