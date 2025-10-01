-...
Título: LeetCode 750. Número de rectángulos de esquina -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
750. Número de rectángulos de esquina – El paquete de solución completa

Silencio Idioma Silencio Tiempo Complejidad
Silencio--------------------------
Silencio **Java** Silencio O(max(M,N)·min(M,N)2) Silencio O(1) Silencio Optimizado para la rejilla escasa – dos vueltas sobre filas/cols + combinatoria. Silencio
Silencio **Python** Silencio O(max(M,N)·min(M,N)2) Silencio O(1) Silencio La misma idea, escrita idiomáticamente. Silencio
Silencio **C+** Silencio O(max(M,N)·min(M,N)2) Silencio O(1) Silencio Usa el enfoque basado en bitset/array para la velocidad. Silencio

■ **Por qué debe leer este artículo* *
■ Leetcode 750 es una clásica pregunta de entrevista “matrix + combinatoria” que se hace con frecuencia por las empresas de tecnología superior.
■ Comprender el *bueno*, el *bad*, y las partes *muy* de sus soluciones le ayudarán a impresionar a los gerentes de contratación, anotar altas en las evaluaciones de codificación, y aterrizar ese papel de ingeniería de software que ha estado observando.

-...

Declaración de problemas

■ **Given** un `m × n` matriz entero `grid` donde cada entrada es `0` o `1`, devuelve el número de * rectángulos de esquina*.
■ Un rectángulo de bellota* es un conjunto de cuatro `1`s distintos que forman un rectángulo alineado con el eje. Sólo las esquinas deben contener `1`; las células internas pueden ser `0` o `1`. Los cuatro `1`s deben ser distintos (por lo que una sola fila o columna de `1's no cuenta).

*Constraints*

- 1 ≤ m, n ≤ 200
- `grid[i] [j]  Iberia {0, 1}`
- 1 ≤ 1 ≤ 6000

-...

### 🧩 Why Es un “Medium” pero *Very* Interview‐ Problema listo

*Combinadores* – Usted necesitará pensar en “¿Cuántas maneras podemos elegir dos columnas que ambos tienen un `1` en dos filas diferentes? ”
*Sparse Matrix Awareness* – En muchos escenarios de entrevistas del mundo real, la cuadrícula es muy escasa (sólo unos pocos `1`s). Una solución ingenua `O(m2·n2)` TLE.
- **Trade-offs** – Una fuerza bruta pura es fácil de código pero lenta; un DP de fila a día o solución de bitset es rápido pero más difícil de explicar en una pizarra blanca.

-...

## ✅ The *Good* – Fast, Elegant and Easy to Reason About

La visión clave:

1. **Fix dos filas** (o dos columnas).
2. Escanee la otra dimensión para contar cuántas columnas contienen una `1` en ** ambas filas seleccionadas.
3. Si encuentras `k` tales columnas, puedes elegir cualquiera de ellos para formar un rectángulo: `C(k, 2) = k·(k‐1)/2`.

■ ¿Por qué dos filas? * *
■ Porque las esquinas del rectángulo se encuentran en dos filas distintas. Una vez fijadas las filas, las columnas se convierten en los únicos grados de libertad.

**Pseudo-code* *

`` `
Resultado = 0
para cada par de hileras (r1 <r2):
Conteo = 0
para cada columna c:
si la cuadrícula [r1][c] == 1 " cl][r2] [c] == 1:
Contador++
resultado += cuenta * (cuenta-1) / 2
Resultado de retorno
`` `

**La complejidad* *

- `O(min(M,N)2 · max(M,N)' tiempo
- `O(1)` espacio auxiliar (o `O(N2)` si desea reutilizar un array 2-D para la optimización)

-...

*Bad* – Brute‐Force O(M2·N2) y por qué no pasa

``python
# O(M^2 * N^2) – demasiado lento para 200×200 rejilla
para r1 en rango(M):
para r2 en rango(r1+1, M):
para c1 en rango(N):
para c2 en rango(c1+1, N):
if grid[r1][c1] and grid[r1][c2] and grid[r2][c1] and grid[r2][c2]:
res += 1
`` `

- Incluso con las máximas restricciones (`M = N = 200`), este bucles **1,6 billones** veces → TLE en Leetcode.
- También utiliza cuatro bucles anidados – difícil de explicar rápidamente en un tablero de entrevistas.

-...

## 😈 The *Ugly* – Memory‐Intensive DP (pero todavía eficiente)

Un punto de vista ligeramente diferente:
En lugar de contar por par de filas, mantenga un recuento de cuántos filas anteriores comparten un `1` en cada par de columnas.
Esto nos permite acumular rectángulos en **O(M·N2)** tiempo con **O(N2)** espacio, pero la matriz DP puede convertirse en un cuello de botella si `N` es grande.

■ ¿Cuándo usarlo? #
■ En los ajustes de entrevistas donde se le da una rejilla *muy escasa* y puede permitirse una matriz auxiliar de `O(N2), este método a menudo marca el tiempo de ejecución más rápido.

-...

## 📚 Full Code Implementations

### 1Ω⃣ Java (Space‐Optimized, Sparse‐Matrix Friendly)

``java
Clase Solución {
public int countCornerRectangles(int[][] grid) {
si (grid == null TEN ANTERIENTE grid.length Identifica= 1 TENIDO rejilla de vida [0]. longitud = 1) {
retorno 0;
}

filas int = grid.length;
int cols = grid[0]. longitud;

// Elija la dimensión más pequeña para iterar sobre pares
si
cuenta de retorno ByRows(grid, rows, cols);
. ♫ ... {
cuenta de retorno ByCols(grid, rows, cols);
}
}

int countByRows(int[][] grid, int rows, int cols) {}
int res = 0;
para (int r1 = 0; r1) {}
para (int r2 = r1 + 1; r2) {}
int cnt = 0;
para (int c = 0; c) {}
(grid[r1][c] " grid[r2][c]) == 1) cnt++;
}
res += cnt * (cnt - 1) / 2;
}
}
restitución;
}

int countByCols(int[][] grid, int rows, int cols) {}
int res = 0;
para (int c1 = 0; c1 c1) {}
para (int c2 = c1 + 1; c2) {}
int cnt = 0;
para (int r = 0; r  se realizaron filas; r++) {
(grid[r][c1] " grid[r][c2]) == 1) cnt++;
}
res += cnt * (cnt - 1) / 2;
}
}
restitución;
}
}
`` `

-...

Python (Elegant & Easy to Read)

``python
Solución de clase:
def countCornerRectangles(self, grid: List[List[int]) - título int:
si no la cuadrícula o el len(grid)
retorno 0

m, n = len(grid), len(grid[0])
# Iterate sobre la dimensión más pequeña
si m
volver a sí mismo._by_rows(grid, m, n)
más:
volver a sí mismo._by_cols(grid, m, n)

def _by_rows(self, grid, m, n):
res = 0
para r1 en rango(m - 1):
para r2 en rango(r1 + 1, m):
cnt = 0
para c en el rango(n):
if grid[r1][c] " grid[r2][c]:
cnt += 1
res += cnt * (cnt - 1) // 2
retorno

def _by_cols(self, grid, m, n):
res = 0
para c1 en rango(n - 1):
para c2 en rango(c1 + 1, n):
cnt = 0
para r en rango(m):
if grid[r][c1] & grid[r][c2]:
cnt += 1
res += cnt * (cnt - 1) // 2
retorno
`` `

-...

### 3down⃣ C++ (Fastest, Bitset-Optimized for Leetcode)

``cpp
Clase Solución {
public:
int countCornerRectangles(vector identificadovector identificadointющ grid) {
int m = grid.size(), n = grid[0].size();
si (m <= 1 TENIDO TENIDO TENIDO ENTRE 1) retorno 0;
// Use bitset si n <= 200 (se adapta a un bitset de 200 bits)
vector realizado(m);
para (int i = 0; i)
para (int j = 0; j)
si (grid[i][j]) hileras[i].set(j);

int res = 0;
para (int i = 0; i) {}
para (int j = i + 1; j)
// intersección de dos filas
bitset =200 caracteres inter = filas[i] & filas[j];
cnt largo = inter.count();
res += cnt * (cnt - 1) / 2;
}
}
restitución;
}
};
`` `

■ ¿Por qué? * *
■ Un `bitset realizado200 ` da O(1) intersección y O(1) pop-count, convirtiendo el bucle interior en un puñado de instrucciones de la máquina. Esta es la solución más rápida para los límites de tiempo duro de Leetcode.

-...

## На Cómo explicarlo en una junta de entrevistas

1. **Dos hileras** (`r1` y `r2`).
2. **Mostrar un barrido** a través de las columnas, contando donde ambos tienen un `1`.
3. **Aplica la fórmula de combinación**.
4. **Generalizar** – “Si las columnas son menos, cambiaríamos la lógica y las columnas de par en cambio. ”

■ Mantenga su razonamiento corto: *“Estamos esencialmente contando pares de columnas que comparten un `1` en dos filas, por lo que para `k` columnas tenemos `k elegir 2` rectángulos.”*
■ Utilice la pizarra para dibujar la intersección de bitset si usted está cómodo con C++.

-...

## 🚀 Take‐away: What Hiring Managers Are Looking for

Esquía de la vida _ Por qué importa
Silencio...
tención ** Pensamiento algorítmico** Silencioso Habilidad para detectar el patrón de par-rows Silencio Brevemente describir el paso combinatoria ←
tención **Time‐Space trade‐off** Silencio Entender cuándo favorecer el tiempo sobre la duración del código ← Mención "elegimos la dimensión más pequeña para mantener el tiempo lineal" Silencio
Silencio **Uso de estructuras de datos** Silencio Reconocimiento de las matrices escasas de Leetcode Silencio Explicar la optimización de bitsets o DP array
Silencio **Comunicación** Silencio Clear, concise explanation ◾ Practica el paseo marítimo en una entrevista simulada

-...

## 🎯 Final Thoughts > Next Steps

1. **Practice** – Ejecute estas soluciones en las entradas de muestra de Leetcode, luego cree sus propios casos de borde (por ejemplo, todos los `1`s, todos `0`s, diagonal `1`s).
2. **Explicar las matemáticas** – En entrevistas, siempre verbaliza 'C(k, 2)` antes de codificación.
3. # Prepárate para adaptarte # Si el entrevistador pide “el más rápido posible” o “memory‐efficient”, pivote a la versión DP o bitset.

■ **Landing a role**: Mastering Leetcode 750 demuestra dominio de *matrix manipulación*, *combinatorics* y *algoritmic optimisation*—skills que son fundamentales para muchas posiciones de ingeniería de software (por ejemplo, backend, data‐engineering, algoritmoic trading).

Feliz codificación, y que su próxima entrevista vaya *off-the‐chart*! 🚀

-...

■ *Sígueme en GitHub para más soluciones de entrevistas, práctica de entrevistas simuladas y recursos de promoción profesional. *
[Su GitHub]** Silencio ** [Sus LinkedIn] ** [Sus Blogs]**

-...


-...


(End of article)