-...
Título: LeetCode 2536. Submatrices de Incremento por Uno -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## LeetCode 2536 – ** Submatrices de Incremento por Uno**
## The Good, the Bad, and the Ugly

■ **Keywords**: LeetCode 2536, Submatrices de Incremento por One, 2-D suma de prefijo, matriz de diferencias, adición de rango, entrevista de codificación, análisis de algoritmos, entrevista de trabajo

-...

### 1. Recaptación de problemas

Le han dado una matriz 'n × n` cero-inicializada 'mat`.
Usted recibe una serie de consultas `queries[i] = [row1i, col1i, row2i, col2i]`.
Para cada consulta debe añadir **1** a cada elemento dentro del sub-matrix definido por los cuatro índices.
Devuelve la matriz final después de aplicar todas las consultas.

■ **Constraints**
* `1 ≤ n ≤ 500`
≤ 104 `
* `0 ≤ fila1i ≤ fila2i
* `0 ≤ col1i ≤ col2i

-...

### 2. Por qué el Bruto-Force falla (El mal)

Una implementación directa se dirige sobre cada célula afectada por una consulta:

``java
para (int[] q : consultas) {
para (int r = q[0]; r > = q[2]; r++)
para (int c = q[1]; c)
mat[r][c]++;
}
`` `

* **La complejidad del tiempo** – O(`q * n2`) en el peor caso (cada consulta cubre toda la matriz).
Con `q = 104` y `n = 500`, eso es 2,5 × 109 operaciones → TLE.
* **Espacio** – O(1) extra, pero el tiempo de funcionamiento pesado domina.

Así que necesitamos un truco de *range addition*.

-...

### 3. La Diferencia Dos Dimensionales Array (El Bien)

El truco 1-D para actualizaciones de rango es marcar el inicio y el elemento después del final, luego tomar una suma prefijo una vez al final.
En 2-D hacemos lo mismo con cuatro actualizaciones de “corner”:

Silencio
Silencio...
[c1] += 1` Silencioso inicio del rectángulo
Silencio `diff[r1][c2+1] -= 1` tención end‐right boundary Silencio
TENIDA `diff[r2+1][c1] -= 1` Silencio end‐bottom boundary Silencio
[c2+1] += 1` Silencioso

Después de procesar todas las consultas realizamos una suma de **prefijo sobre filas** luego sobre **columnas** (o vice-versa).
La matriz resultante es exactamente la matriz después de todos los incrementos.

#### Complexity

* **Time** – `O(n2 + q) `
* Cada consulta se procesa en O(1).
* Dos bucles anidados sobre la matriz para las sumas prefijo: `n2` operaciones.
* **Espacio** – `O(n2)` (la matriz de diferencias, puede reutilizar la matriz de resultados).

Con `n ≤ 500`, `n2 = 250 000`, fácilmente bajo los límites.

-...

### 4. Casos de borde " Gotchas "

La situación actual ¿Qué hacer?
Silencio...
Silencio Query touching the right/bottom edge tención `c2 + 1 == n` o `r2 + 1 == n` - no salga de los límites. Use un '(n+1) × (n+1)` array o guarde con 'si` cheques. Silencio
← Índices negativos (ninguno en este problema) Silencio No es necesario, pero recuerde la idea al extenderse a adiciones de rango general. Silencio
TENIDO Grande `n` pero pequeño `q` TENIDO Todavía O(`n2`) para las sumas del prefijo - inevitable porque la salida en sí es `n2`. Silencio
TENIDO Límites de memoria Silencio `500 × 500` enteros ♥ 1 MB - seguro en la mayoría de las plataformas. Silencio

-...

### 5. Optimizaciones alternativas (El Ugly)

TENIDO ANTERIOR ANTERIOR Cuando ayuda a vivir
Silencio--------------------------
Silencio **Diff de nivel real** – almacenar una lista de “actualizaciones” por fila, acumular un diff de 1‐D para esa fila Silencio Si tienes muchas más filas que las consultas, puedes evitar la segunda dimensión por completo. Silencio
Silencio **El prefijo perezoso** – construir sumas prefijo incrementalmente mientras se aplican las consultas ← Guarda un pase, pero más código y más difícil de razonar. Silencio
Silencioso ** Representación estable** – utilizar mapas de hash para actualizaciones muy escasas tención Útil si `n` puede ser tan grande como 106 y las consultas son pocas. Silencio

Estas variantes de la complejidad del código comercial para las ganancias de velocidad marginal y rara vez son necesarias para los límites de LeetCode.

-...

### 6. Aplicación de las referencias

A continuación se encuentran soluciones limpias y de producción en **Java, Python y C++**.
Todos usan el `(n+1) × (n+1)` truco de matriz de diferencias y dos pases de sumas de prefijo.

-...

### Java (LeetCode-style)

``java
*
* LeetCode 2536: Submatrices de Incremento por Uno
*/
Solución de la clase pública {}
public int[][] rangeAddQueries(int n, int[][] consultas) {
// diff tiene una fila extra/col para evitar controles de límites
int[][] diff = nuevo int[n + 1][n + 1];

para (int[] q : consultas) {
int r1 = q[0], c1 = q[1];
int r2 = q[2], c2 = q[3];
diff[r1][c1] += 1;
diff[r1][c2 + 1] -= 1;
diff[r2 + 1][c1] -= 1;
diff[r2 + 1][c2 + 1] += 1;
}

// Suma de prefijo sobre filas
para (int r = 0; r) {}
para (int c = 1; c) {}
diff[r][c] += diff[r][c - 1];
}
}

// Suma de prefijo sobre columnas
para (int r = 1; r) {}
para (int c = 0; c) {}
diff[r][c] += diff[r] [c];
}
}

// Trim la fila extra/col y regreso
int[][] res = nuevo int[n][n];
para (int r = 0; r) {}
System.arraycopy(diff[r], 0, res[r], 0, n);
}
restitución;
}
}
`` `

-...

#### Python 3

``python
"
LeetCode 2536: Submatrices de Incremento por Uno
"
Solución de clase:
def range AddQueries(self, n: int, queries: List[List[int]) - No. List[List[int]]:
# +1 para realizar actualizaciones de esquina de forma segura
diff = [0] * (n + 1) para _ en rango(n +1)]

para r1, c1, r2, c2 en consultas:
diff[r1][c1] += 1
diff[r1][c2 + 1] –= 1
diff[r2 + 1][c1] -= 1
diff[r2 + 1][c2 + 1] += 1

# Prefix over rows
para r en rango(n):
para c en el rango(1, n):
diff[r][c] += diff[r][c - 1]

# Prefijo sobre columnas
para r en rango(1, n):
para c en el rango(n):
diff[r][c] += diff[r] [c]

# Devuelva la matriz recortada
[row[:n] for row in diff[:n]
`` `

-...

#### C++ (GNU C+17)

``cpp
*
* LeetCode 2536: Submatrices de Incremento por Uno
*/
Clase Solución {
public:
vector de vectores rangeAddQueries(int n, vector identificadovector identificadoint {}
// diff tiene una fila adicional / frío para la seguridad
vector seleccionado(n + 1, 0)

para (continuo auto cho q : consultas) {}
int r1 = q[0], c1 = q[1];
int r2 = q[2], c2 = q[3];
diff[r1][c1] += 1;
diff[r1][c2 + 1] -= 1;
diff[r2 + 1][c1] -= 1;
diff[r2 + 1][c2 + 1] += 1;
}

// Suma de prefijo sobre filas
para (int r = 0; r)
para (int c = 1; c)
diff[r][c] += diff[r][c - 1];

// Suma de prefijo sobre columnas
para (int r = 1; r)
para (int c = 0; c)
diff[r][c] += diff[r] [c];

// Trim la matriz a n x n
vector seleccionado(n));
para (int r = 0; r)
para (int c = 0; c)
[r][c] = diff[r][c];

restitución;
}
};
`` `

-...

### 7. Pruebas " validación "

Silencio Test confidencialidad esperada
Silencio...
TENIDO `n = 1`, one query `[0,0,0,0]` TENIDO `[[1]] Silencio
Silencio `n = 3`, consultas que cubren sub-matrices descomunales ¦
TENIDO `n = 500`, cada consulta cubre toda la matriz TENIDO Matriz llena de `q ' (por ejemplo, 10 000) ANTE
← Consultas que tocan la frontera No hay desbordamiento; resultado es correcto

Ejecute las implementaciones proporcionadas contra estos casos – todos pasan instantáneamente en el arnés de prueba de LeetCode.

-...

### 8. Qué están buscando los entrevistadores

1. **Apoyo de las sumas de prefijo 2-D** – muestra que puede generalizar el truco de actualización de rango 1-D.
2. **Manejo de edge** – tratar correctamente con los límites de `+1` es una fuente común de errores.
3. ** Análisis de complejidad** – poder explicar `O(n2 + q)` es crucial.
4. **Código completo** – comentarios legibles y nombres de variables adecuados ayudan al evaluador a leer su solución rápidamente.

Si usted está apuntando a una entrevista de ingeniería de software, explicar el concepto *difference array* e incluso dibujar el algoritmo en una pizarra blanca. Eso demuestra pensamiento claro y fundamentos algoritmoicos sólidos.

-...

### 9. Preguntas frecuentes

Respuesta a la respuesta
Silencio...
Silencio **¿Puedo usar un diff array de 1‐D solamente?** No – un único array 1‐D no puede capturar dos dimensiones independientes de un rectángulo. Silencio
Silencio **¿Y si el valor a añadir no es 1? ** TENIDO La misma idea, simplemente agregue el valor en lugar de `1`. Silencio
Silencio **¿Puedo usar `int64` para evitar el desbordamiento?** Silencio Para este problema el valor máximo es `104`, por lo que `int` está bien. Para problemas generalizados puede cambiar a 'long'. Silencio
Silencio **¿Hay un algoritmo mejor que O(n2)?** Silencio No para salidas densas. Si usted podría saltar la salida de la matriz, un barrido en línea o un escaso diff podría ayudar. Silencio

-...

#### 10. Final Take‐ Away

■ * Submatrices de Incremento por One* es un ejemplo de libro de texto de cómo un simple array de diferencia de 2-D convierte un tiempo de ejecución imposible en una solución elegante `O(n2 + q)`.
■ Domine este patrón, y estará preparado para muchas preguntas de entrevista “range-update” que aparecen en rondas de diseño y estructura de datos.

Buena suerte, y que sus entrevistadores amen su código Java/Python/C++ limpio!