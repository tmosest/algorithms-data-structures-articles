-...
Título: LeetCode 2711. Difference of Number of Distinct Values on Diagonals -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## LeetCode 2711 – Diferencia de Número de Valores Distintos en Diagonales
### “El Bien, el Mal y el Ugly” – Un Java / Python completo / C++ Paquete de solución

■ **Por qué este artículo importa para su próxima entrevista* *
■ Mastering LeetCode 2711 muestra que puedes:
* Lea una declaración de problema no-trivial 2-D
* Piense en el traversal diagonal, los juegos y la optimización de la mascarilla
* Entregar código limpio, lingüístico-agnostico en Java, Python y C++
* Discuss time‐space trade‐offs – una entrevista imprescindible

-...

## 1. Declaración de problemas (de LeetCode)

■ **Given** a 2-D grid `grid[m][n]` (1 ≤ m, n ≤ 50, 1 ≤ grid[i][j] ≤ 50)
■ **Definir** para cada celda (r, c):
* `izquierdaAbove[r][c]` – número de valores **distintos** en la diagonal a la izquierda (excluyendo la propia célula).
* `rightBelow[r][c]` – número de valores **distintos** en la diagonal a la derecha (excluyendo la propia célula).
■ **Retorno** un `ans[m][n] Donde
[c] [c] [c] [c] [c]] [c] [c] [c] [c] [c] [c] Silencio.

Una diagonal es cualquier línea que comienza desde una célula en la fila superior o columna izquierda y mueve un paso hacia abajo a la derecha hasta que la cuadrícula termina.

-...

## 2. La Buena – Bruta‐Force Approach (Intuitive)

``java
int[][] diferenciaOfDistinctValues(int[][] grid) {
int m = grid.length, n = grid[0].length;
int[][] ans = nuevo int[m][n];
para (int i = 0; i) {}
para (int j = 0; j)
Establecer el título izquierdo = nuevo HashSet correspondió();
para (int r = i-1, c = j-1; r 0; --r, --c)
izquierda.add(grid[r][c]);

Establecer contactoInteger correctamente = nuevo HashSet correctamente();
para (int r = i+1, c = j+1; r)
right.add(grid[r][c]);

as[i][j] = Math.abs(left.size() - right.size());
}
}
devolver los ans;
}
`` `

* **Pros** – Fácil de entender, utiliza el `HashSet` de Java.
* **Cons** – Complejidad del tiempo `O(m*n*min(m,n))`, peor caso ♥ 125 000 operaciones por celda (fina para 50x50 pero lento en concursos).
* ** Memoria** – `O(min(m,n))' para los dos conjuntos temporales.

-...

## 3. El malo - ¿Por qué el Bruto-Force falla en entrevistas reales

* **Tiempo-Limit Exceed**: En entradas más grandes o en estrictos límites de competencia, la solución `O(m*n*min(m,n))' puede alcanzar 2 s de tiempo.
* **Re-computing Sets**: Cada célula recomputa las mismas diagonales repetidamente.
* **High Constant Factors**: Java `HashSet` asignación overhead per cell is expensive.

■ **Bottom line** – impresionará a su reclutador si puede reducir el algoritmo a tiempo lineal.

-...

## 4. Los Casos Ugly - Edge que rompen el código ingenuo

Silencio Caso confidencialidad ¿Por qué rompe la vida
Silencio...
TENIDO UNA Célula Única ANTE Las diagonales están vacías; establece correctamente el tamaño de la devolución 0. Silencio
Rejilla rectangular `3x5` Silencio La longitud diagonal difiere; debe guardar los límites `r confianza=0 ' y `r correspondm ' c sensiblen ' . Silencio
Silencio Valores repetidos a lo largo de un diagonal tención Sets correctamente colapsan duplicados, pero la ingenua cuenta mal. Silencio

El código de fuerza bruta maneja todos ellos, pero es frágil si modifica los lazos.

-...

## 5. La solución optimizada – Tiempo lineal con Bit‐Masks

Debido a que cada valor celular está en `[1, 50]`, podemos almacenar una máscara de 64 bits donde bit `k` (0-basado) indica que el valor `k+1` ha aparecido.
Dos máscaras por celda son suficientes:

Símbolo vocacional Significado de la Transición
Silencio----------------------
Silencio `leftMask[i][j]` Silencio Valores distintos en el diagonal izquierdo hasta `(i,j)` **excluida** Silencio `leftMask[i][j] = izquierdaMask[i-1] [j-1] Silencio (1L ANTE) Silencio
Silencio `derechaMask[i][j]` Silencio Valores distintos en el principio diagonal de bajo derecho ** después de `(i,j)` TENIDO `rightMask[i] [j] = rightMask[i+1] [j+1] TENIDO (1L] Secuestrado (grid[i+1][j+1]-1) Silencio

La respuesta para una célula es la diferencia absoluta de la cuenta pop de las dos máscaras.

### 5.1 Java Implementation

``java
Clase Solución {
int[][] diferenciaOfDistinctValues(int[][] grid) {
int m = grid.length, n = grid[0].length;
long[][] [] leftMask = new long[m][n];
long[][] rightMask = new long[m][n];
int[][] ans = nuevo int[m][n];

// Build leftMask (top‐left → bottom‐right)
para (int i = 0; i) {}
para (int j = 0; j)
si (i √≥ 0 ' Ivoire 0) {
leftMask[i][j] = leftMask[i-1][j-1]
(grid[i-1] [j-1] - 1));
}
}
}

// Construir derecho Máscara (bottom‐right → top-left)
para (int i = m-1; i 0; --i) {
para (int j = n-1; j 0; --j) {
si
rightMask[i][j] = rightMask[i+1][j+1]
(grid[i+1] [j+1] - 1));
}
}
}

// Respuesta completa
para (int i = 0; i) {}
para (int j = 0; j)
int left Cuenta = Long.bitCount (leftMask[i][j]);
Intento derecho Cuenta = Long.bitCount (rightMask[i][j]);
as[i][j] = Math.abs(leftCount - rightCount);
}
}
devolver los ans;
}
}
`` `

### 5.2 Python Implementation

``python
Solución de clase:
def diferencia OfDistinctValues(self, grid: List[List[int]) - No. List[List[int]]:
m, n = len(grid), len(grid[0])
left_mask = [[0] * n for _ in range(m)]
right_mask = [[0] * n for _ in range(m)]

# leftMask: top‐left - título inferior derecho
para i en rango(m):
para j en rango(n):
si yo me convengo 0 y j
left_mask[i][j] = left_mask[i-1][j-1] ANTE (1 ANTE)

# rightMask: bottom‐right - titulado top-left
para i en rango(m-1, -1, -1):
para j en rango(n-1, -1, -1):
si yo hice lo primero y lo primero fue:
right_mask[i][j] = right_mask[i+1][j+1] ANTE (1 ANTE)

ans = [[0] * n for _ in range(m)]
para i en rango(m):
para j en rango(n):
left_cnt = left_mask[i][j].bit_count()
right_cnt = right_mask[i][j].bit_count()
ans[i][j] = abs(left_cnt - right_cnt)
Retorno
`` `

### 5.3 C++ Aplicación

``cpp
Clase Solución {
public:
vector realizador identificadoint confianza diferencialOfDistinctValues(vector seleccionadovector identificadovector fieltro unido grid) {
int m = grid.size(), n = grid[0].size();
vector realizador realizado no firmado largo tiempo largo título leftMask(m, vector asignado largo(n, 0)
vector realizador realizado no firmado largo tiempo de confianza derechaMask(m, vector asignado largo(n, 0)
vector seleccionado(n, 0));

//izquierda Máscara: superior izquierda a inferior derecha
para (int i = 0; i)
para (int j = 0; j)
si (i ' Ivoire j)
leftMask[i][j] = leftMask[i-1][j-1]
(grid[i-1] [j-1] - 1));

// rightMask: inferior derecha a superior izquierda
para (int i = m-1; i 0; i)
for (int j = n-1; j √= 0; --j)
si
rightMask[i][j] = rightMask[i+1][j+1]
(grid[i+1] [j+1] - 1));

// Respuesta final
para (int i = 0; i)
para (int j = 0; j)
int left Cnt = __constructionin_popcountll(leftMask[i][j]);
Intento derecho Cnt = __constructionin_popcountll(rightMask[i][j]);
as[i][j] = abs(leftCnt - rightCnt);
}
devolver los ans;
}
};
`` `

-...

## 6. Análisis de la complejidad

TENIDO ANTERIENTE TENIDO Tiempo ANTERIENTE Espacio Por qué importa
Silencio------------------------------
Silencio Brute‐Force (HashSet) Silencio **O(m × n × min(m,n)** Silencio `O(min(m,n))' por célula ← Intuitiva pero lenta 
Silencio Optimised (Bit‐Mask) Silencio **O(m × n)** Silencio `O(m × n)` para dos máscaras de 64 bits TEN Linear, pasa todos los casos de prueba de LeetCode y concursos Silencio

*Constant‐Factor Ganar**:
* Java: `Long.bitCount` es una única instrucción de CPU.
* Python: `int.bit_count()` también es altamente optimista en el CPython 3.10+.
* C++: `__construido_popcountll` es una única instrucción de máquina.

Debido a que los valores de la red están ligados a 50, una máscara de 64 bits es un ajuste perfecto.
Si el rango de valor fuera más grande, revertirás a `HashSet` o usarás un `HashMap realizadovalor, contágalo ` para cada prefijo diagonal.

-...

## 7. Consejos para entrevistas

1. **Explicar el problema en sus propias palabras** – “Para cada célula sólo miramos la diagonal que va arriba-izquierda y la que va directamente. ”
2. **Preguntas aclaratorias** – por ejemplo, “¿La longitud diagonal es siempre la misma? ”
3. **Mostrar la fuerza bruta primero** – da al entrevistador una base de referencia.
4. **Introducir el truco bit-mask** – “Porque los valores son ≤ 50, podemos tratarlos como bits. ”
5. **Discuss pop-count** – muchos entrevistadores te aman cuando mencionas `_construidoin_popcountll` / `Long.bitCount`.
6. **Edge‐Case check** – resaltar cómo su código maneja una cuadrícula de células individuales o matrices no cuadradas.

-...

## 8. Conclusión – Su próxima entrevista Edge

LeetCode 2711 es más que un problema diagonal – es un escaparate de:

* **Teoría de asiento** (elementos distintos en diagonal)
* **Dinamic-programming aroma** (mascaras prefijo)
* ** Optimización de nivel superior** (mascaras de 64 bits)
* **Language‐agnostic implementation** (Java, Pitón, C++)

Dejar la versión brute-force para impresionar, mantener la fuerza bruta en tus notas para depurar rápidamente, y estar siempre listo para explicar la solución bit-mask `O(m*n)` en la sala de entrevistas. Buena suerte – ahora estás un paso más cerca de aterrizar ese papel de ingeniería de software!