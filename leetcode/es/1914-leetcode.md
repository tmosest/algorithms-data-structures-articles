-...
Título: LeetCode 1914. Cicclicamente Rotating a Grid -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recapitulación del problema – LeetCode 1914

**Problema* *
■ Dada una matriz uniforme `grid ' (m × n) y un entero `k ' ,
" rotar cada " (o capa) de la matriz a la derecha por posiciones " .
Puede ser tan grande como 109, por lo que la rotación debe realizarse en **O(1)** por elemento.

A *shell* es el conjunto de células que comparten la misma distancia de Manhattan desde la frontera exterior.
La cáscara más externa contiene todas las celdas fronterizas, la siguiente es la
frontera de la sub-matrix que permanece después de pelar la capa exterior, etc.

■ **Regresar la rejilla después de que todas las conchas hayan sido rotadas. #

**Constraints* *

TEN TERRITOR ANTERIOR ANTERIOR ANTERIOR
Silencio...
TENIDO `grid.length == m` TENIDO 2 ≤ m ≤ 30
TENIDA `grid[0].length == n` ANTE 2 ≤ n ≤ 30
'm, n` even Silencio sí Silencio
TENIDO `0 ≤ grid[i] [j] ≤ 1000` ANTERIOR sí TENIDO
Ø ≤ ≤ 109` Silencio

El objetivo es una solución de tiempo **O(m·n)** que utiliza sólo **O(m·n)** memoria extra (o incluso menos).

-...

## 2. Algoritmo de alto nivel

1. *Peel each shell*
* Mover en sentido de reloj / en sentido contrario a lo largo de los cuatro bordes (top → izquierda → fondo → derecha) y recoger los elementos en un array de 1‐D `shell[]`.
2. *Rotar el array 1‐D*
* Porque `k` puede ser enorme, girar sólo `k % shell.length` veces.
* Una rotación izquierda por `r` se puede hacer en su lugar con un truco *reverso* (o por corte).
3. **Escribe la cáscara rota*
* Tetrato sobre los mismos cuatro bordes en el mismo orden y sobreescribir la matriz original con los valores rotativos.
4. *Repetir por cada caparazón*
* Comience con la cáscara exterior (`top = 0`, `left = 0`, `bottom = m-1`, `right = n-1`) y encoge las fronteras hasta `top ît= bottom` o `left не= right`.

-...

## 2. Aplicación del Código

A continuación encontrará tres soluciones independientes, una en cada uno de los tres idiomas de entrevista más comunes.

■ **Consejo:** En cada aplicación de las entrevistas usamos `k %= shellLen` inmediatamente después de que se extraiga la cáscara, por lo que nunca llegamos a más de lo necesario.

-...

### 2.1 Java (O(m·n) time, O(m·n) extra space)

``java
importar java.util*;

Clase Solución {
int[][] rotateGrid(int[][] grid, int k) {
int m = grid.length, n = grid[0].length;
int top = 0, left = 0, bottom = m - 1, right = n - 1;

mientras que (de arriba)
// 1. Extraiga la cáscara actual en un array 1-D
int len = 2 * (bottom - top + derecha - izquierda);
int[] shell = new int[len];
int idx = 0;

para (incluido r = superior; r = inferior); r++) // columna izquierda (top→bottom)
shell[idx++] = grid[r][left];
para (int c = izquierda; c < right; c++) // bottom row (left→right)
shell[idx++] = grid[bottom][c];
for (int r = bottom; r  título superior; r--) // right column (bottom→top)
shell[idx+] = grid[r] [right];
para (int c = derecha; c > left; c--) // top row (right→left)
shell[idx++] = grid[top][c];

// 2. Rotar la cáscara
int shift = k % len;
si 0) {
int[] rotated = new int[len];
para (int i = 0; i) {}
girado[i] = concha [i + turno) % len];
}
shell = rotated;
}

// 3. Escriba la cáscara rota
idx = 0;
para (incluido r = superior; r)
grid[r][left] = shell[idx++];
para (int c = izquierda; c)
grid[bottom][c] = shell[idx++];
para (incluido r = inferior; r > top; r--) // columna derecha
grid[r][right] = shell[idx++];
para (int c = derecha; c > izquierdo; c--) // fila superior
grid[top][c] = shell[idx++];

// encoger el rectángulo para el siguiente shell
top++; bottom--; left++; right--;
}
rejilla de retorno;
}
}
`` `

**La complejidad* *

Silencio
Silencio...
Silencio ** Tiempo** Silencioso `O(m·n)` – cada elemento se lee y escribe una vez por concha
Silencio **Espacio** Silencioso `O(m·n)` en el peor caso (el proyectil exterior) - se puede reducir a `O(min(m,n))'' por re-utilizar un único array

-...

## 2.2 Python 3 (O(m·n) time, O(m·n) extra space)

``python
Solución de clase:
def rotateGrid(self, grid: List[List[int], k: int) - título List[List[int]]:
m, n = len(grid), len(grid[0])
arriba, izquierda, inferior derecha = 0, 0, m - 1, n - 1

mientras que la parte superior de abajo y izquierda
# 1. Extraiga la actual cáscara
shell = []

para r en rango(top, fondo): # La columna izquierda
shell.append(grid[r][left])

para c en rango(izquierda, derecha): # La fila inferior
shell.append(grid[bottom][c])

para r en rango(abajo, arriba, -1): # columna derecha
shell.append(grid[r][right])

para c en rango (derecha, izquierda, -1): # fila superior
shell.append(grid[top][c])

# 2. Girar a la izquierda por k % len(shell)
cambio = k % len(shell)
si cambio:
shell = shell[shift:] + shell[:shift]

# 3. Escribe de nuevo
idx = 0
para r en rango(top, fondo): # La columna izquierda
grid[r][left] = shell[idx]; idx += 1

para c en rango(izquierda, derecha): # La fila inferior
grid[bottom][c] = shell[idx]; idx += 1

para r en rango(abajo, arriba, -1): # columna derecha
grid[r][right] = shell[idx]; idx += 1

para c en rango (derecha, izquierda, -1): # fila superior
grid[top][c] = shell[idx]; idx += 1

top, bottom, left, right = top + 1, bottom - 1, left + 1, right - 1

Cuadrícula de retorno
`` `

**La complejidad* *

Silencio
Silencio...
Silencio ** Tiempo** Silencioso `O(m·n)` Silencio
Silencio **Espacio** Silencioso `O(min(m, n))` – la matriz de shell temporal ←

-...

### 2.3 C+ (O(m·n) time, O(m·n) extra space)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector seleccionador seleccionador: No, no.
int m = grid.size(), n = grid[0].size();
int top = 0, bottom = m - 1, left = 0, right = n - 1;

mientras que (de arriba)
// 1. Extract shell
vector cáscara;
para (int r = top; r)
shell.push_back(grid[r][left]);

para (int c = izquierda; c)
shell.push_back(grid[bottom][c]);

para (incluido r = inferior; r > top; --r) // columna derecha
shell.push_back(grid[r] [right]);

para (int c = derecha; c > left; --c) // top row
shell.push_back(grid[top][c]);

// 2. Girar a la izquierda por k % shell.size()
int shift = k % shell.size();
si
girar(shell.begin(), shell.begin() + cambio, shell.end());
}

// 3. Escriba de nuevo
int idx = 0;
para (int r = top; r)
grid[r][left] = shell[idx++];

para (int c = izquierda; c)
grid[bottom][c] = shell[idx++];

for (int r = bottom; r > top; --r)
grid[r][right] = shell[idx++];

para (int c = derecha; c > left; --c)
grid[top][c] = shell[idx++];

++top; --bottom; ++izquierda; --right;
}
rejilla de retorno;
}
};
`` `

**La complejidad* *

Silencio
Silencio...
Silencio ** Tiempo** Silencioso `O(m·n)` Silencio
Silencio **Espacio** Silencioso `O(min(m,n)'' – el array de shell

■ **¿Por qué hacemos `k % shell.size()`? #
■ Rotating a shell of length `L` by `L` or `2·L` positions is the identity.
■ Usando el modulo elimina el trabajo innecesario cuando `k` es enorme.

-...

## 3. “Bien” vs. “Bad” Código: Lo que los entrevistadores buscan

Silencio
Silencio...
Silencio **Bien** Silencio Clear separation of **shell extraction**, **rotation**, **write-back**. ←
Silencio Silencio Usos `k % shellLen` justo después de la extracción. Silencio
TENIDO ANTERIENTE Arranca los límites en una sola línea (`++top; --bottom; ...`). Silencio
TEN ANTERIOR Comentarios explican *por qué* no *cómo* (por ejemplo, “rotación anticipada por turno izquierdo”). Silencio
TEN **Bad** TEN Recomputes shell length multiple times; does not use modulo; writes back without using the rotated array directly. Silencio
← Los bucles anidados con controles de límites redundantes. Silencio
Silencio Silencio No hay comentarios ni explicación de la rotación inversa. Silencio

-...

## 4. “Bien” vs. “Bad” Código – Una mini guía

Feature ← Buenas vidas
Silencio...
Silencio **Claridad** Silencioso `extractShell()`, `rotateArray()`, `writeBack()` helpers Silencio Todo enredado en un solo bucle ←
Silencio ** Sensibilización de la complejidad** Silencio `k %= shellLen` para evitar iteraciones inútiles Silencio iterando directamente 'k' veces incluso cuando `k > shellLen`
Silencio **Encogimiento de la frontera** ← Encoger la línea única (`++top; --bottom; ...`) tención Múltiples variables cambiaron en líneas separadas, haciendo que los fallos sean fáciles
Silencio **Documentación** Silencio Comentarios explicando cada paso Silencio No hay comentarios, just code tención
Silencio **Testing** Silencio Manijas vacías / 1-células matrices (caso de borde) Silencio Sólo pruebas para el caso típico

-...

## 5. Por qué esto importa para las entrevistas

1. **La complejidad del tiempo es la primera señal** – los reclutadores piden la mejor complejidad posible.
`O(m·n)` es el tiempo mínimo; cualquier cosa más lento será rechazado instantáneamente.
2. **La complejidad del espacio muestra la conciencia** – utilizando `O(min(m,n))` en lugar de `O(m·n)` revela que usted sabe que la longitud de la cáscara está atada por la dimensión más pequeña.
3. **El truco modulo para el enorme `k'** - demuestra el conocimiento de que 'k' puede rebosar y que las rotaciones son cíclicas.
4. **Código legible, autocontenido** – entrevistadores valoran el código que pueden leer, probar y explicar en menos de un minuto.

-...

## 6. “Bien” vs. “Bad” Code – Una lista final de verificación

- [ ] *Extracción de casco* hecha una vez por concha.
- [ ] **Rotación** utiliza `k % shellLen` inmediatamente.
- [ ] **Write‐back** sigue el mismo orden que la extracción.
- [ ] ** Variables** para los límites del rectángulo se actualizan atómicamente.
- [ ] **Comentarios** explican por qué hacemos cada paso.
- [ ] **No hay límites codificados duros** – la solución escala con tamaño de entrada.

-...

## 7. TL;DR para entrevistadores

■ *Se pela una cáscara, gira su representación de 1-D por 'k % longitud', y escribe de nuevo. Repita hasta que se hagan todos los proyectiles. Implementar esto en tiempo O(m·n) y O(min(m,n)) espacio. *

-...

## 8. Takeaway

■ Las soluciones presentadas son **perfectas para entrevistas técnicas**:
* Ellos resuelven el problema dentro de las limitaciones.
* Muestran información algorítmica (conchas de pelaje, truco de rotación inversa).
* Están escritos en **Java, Python, y C+**, cubriendo la mayoría de los apilados de entrevista.

Buena suerte con la preparación de la entrevista, y recuerde: una solución limpia y bien alimentada es mucho más impresionante que una rápida, imparable. ¡Feliz codificación!

-...

#### Preguntas frecuentes

* **¿Podemos resolver esto con O(1) espacio extra? #
Sí – puede girar la cáscara en su lugar con intercambio de cuatro vías. Es un poco más involucrado, pero todavía O(m·n) tiempo.
* **¿Por qué la rotación izquierda por `r` trabaja para el movimiento anti-horario? * *
Debido a que recogimos la concha en orden *auricular*, una rotación izquierda por `r` coloca el elemento que estaba `r` pasos adelante en la posición actual, que equivale a una rotación antiauricular en la matriz 2-D.
* **¿Necesitamos manejar dimensiones extrañas? #
El problema garantiza incluso dimensiones, por lo que el rectángulo interior siempre se encoge uniformemente.

-...

¡Feliz entrevista-preparación! Si tienes alguna pregunta o quieres una inmersión más profunda en el truco de rotación inversa, házmelo saber.