-...
Título: LeetCode 1559. Detectar ciclos en 2D Grid -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1559. Ciclos de detección en rejilla 2D
**LeetCode – Media – Java / Python / C++ soluciones + SEO-optimized blog post**

■ **Keywords** – Detectar Ciclos en 2D Grid, LeetCode 1559, Detección del ciclo BFS DFS, Gráfico Grid, Entrevista de trabajo, Estructuras de datos, Algoritmos, Java DFS, Python DFS, C++ BFS

-...

## 1. Panorama general de los problemas

Se le da una red 2-D `grid[m][n]` de letras inglesas minúsculas.
Un **ciclo** es un camino de longitud **≥ 4** que:

* visita solamente células con el mismo carácter,
* se mueve sólo en las 4 direcciones cardinales,
* regresa a la celda inicial,
* **Nunca se mueve de nuevo a la celda de la que acabas de venir**.

Regrese `verdad ' si existe algún ciclo de ese tipo, de lo contrario `falso ' .

`` `
m, n ≤ 500 → cuadrícula puede contener hasta 250 000 células
`` `

La tarea es un problema clásico de la teoría gráfica en una cuadrícula: detectar un ciclo en un gráfico no dirigido donde los vértices son células con la misma letra.

-...

## 2. El Bien, el Mal, el Ugly

Silencio Silencio
Silencio------------Prince------
Silencio ** Algorithm** Silencio DFS (recusión) es intuitivo y fácil de implementar. BFS también trabaja con una cola de `(row, col, parentRow, parentCol)`. ← Tanto el DFS como el BFS tienen que explorar cada célula una vez; para grandes rejillas la profundidad de recursión puede alcanzar los límites en Python o Java. Un enfoque ingenuo que revisita células o no verifica la condición “parente” informará incorrectamente ciclos. Silencio
Silencio ** Complejidad del tiempo** Silencio O(m · n) – cada célula es visitada una vez. Silencio Ninguno – linear es óptimo para este problema. Algunas soluciones utilizan erróneamente `O(m · n)^2)` debido a escaneos repetidos. Silencio
Silencio **Complejidad del espacio** Silencio O(m · n) para el array visitado + pila de recursión / cola. TEN Recursive DFS puede consumir hasta marcos de pila O(m · n). Silencio Usando `HashMap` para cada célula puede soplar la memoria. Silencio
Silencio **Readability** Silencio Clear parent tracking, single `dfs` function. TEN Recursive DFS puede oscurecer la lógica padre a los recién llegados. Las implementaciones de búsquedas de unión complicadas distraen de la idea central. Silencio
Silencio **Performance** Silencio DFS en Java (`O(1)` recursión por llamada) se ejecutan 100 ms en LeetCode. Silencio Python DFS puede alcanzar límites de recursión para 500 × 500 cuadrículas. ← BFS con una clase de pareja personalizada puede ser más lento en Java debido a boxeo / buzón. Silencio

-...

## 3. Visión Algorítmica

Trate la cuadrícula como un gráfico no dirigido donde cada célula es un nodo.
Dos nodos están adyacentes si comparten un lado y contienen la misma letra.

Durante una primera traversal profunda:

* Al explorar un vecino `(nr, nc)` de la celda actual `(r, c)`,
* If the neighbour was **not visited**, recurse with `(r, c)` as its parent.
* Si el vecino **fue visitado** y no es el padre**, existe un ciclo.

El cheque “parente” garantiza que no detectamos falsamente el trivial camino de dos células hacia atrás y hacia adelante como un ciclo.

-...

## 4. Aplicación del Código

■ Todas las soluciones comparten la misma lógica; sólo la sintaxis difiere.

### 4.1 Java – DFS (Recursivo)

``java
importar java.util*;

Clase Solución {
int[] dr = {1, -1, 0, 0};
int[] dc = {0, 0, -1, 1};

booleano público contieneCycle(char[][] grid) {
int m = grid.length, n = grid[0].length;
int[][] vis = nuevo int[m][n]; // 0 = no previsto, 1 = visitado
para (int i = 0; i)
para (int j = 0; j) {}
si (vis[i] [j] == 0) {
si (dfs(grid, vis, i, j, -1, grid[i][j]))
retorno verdadero;
}
}
}
devolver falso;
}

dfs booleanos privados (char[] g, int[][] vis,
int r, int c,
int pr, int pc,
char color) {}
vis[r][c] = 1;
para (int k = 0; k)
int nr = r + dr[k], nc = c + dc[k];
si (nr < 0 Новыные ные ненный неный неный ненный ненный ненный неный неный неный неный ный ный неный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ны
continuar;
si (g[nr][nc]!= color) continuar;
si (vis[nr][nc] == 0) {
si (dfs(g, vis, nr, nc, r, c, color)) regresan verdadero;
} otro si (nr != pr  durable nc != pc) { // visitado y no padre
retorno verdadero;
}
}
devolver falso;
}
}
`` `

■ **Consejo para entrevistas de Java** – use `int[][] vis` en lugar de un `boolean[][]` para que pueda almacenar el padre coordinar indirectamente (por ejemplo, codificar `(r, c)` en un solo entero) si desea evitar pasar padre por separado.

-...

### 4.2 Python – DFS (Iterative Stack)

``python
de la importación Lista

Solución de clase:
def contains Cycle (self, grid: List[List[str]]) - Confía en bool:
m, n = len(grid), len(grid[0])
vis = [False]*n for _ in range(m)]
dirs = [(1,0), (-1,0), (0,1), (0,-1)]

para i en rango(m):
para j en rango(n):
si no se vis[i][j]:
pila = [(i, j, -1, -1)] # (r, c, parent_r, parent_c)
vis[i][j] = Verdadero
mientras que la pila:
r, c, pr, pc = stack.pop()
para dr, dc en dirs:
nr, nc = r+dr, c+dc
si 0 0 0 0 0 0 0 0 3 0 0 0 0 0 0 0 0 0 0 0 0 0 0 y cuadrícula [nr] == grid[r][c]:
si no se vis[nr][nc]:
vis[nr][nc] = True
stack.append(nr, nc, r, c))
Elif nr!= pr o nc != pc:
Retorno
Retorno Falso
`` `

■ ¿Por qué es iterativo? El límite de profundidad de la recursión de Python (por defecto 1000) se rompería para las cuadrículas grandes; una pila explícita de pasos que.

-...

### 4.3 C++ – DFS (Recursivo)

``cpp
Clase Solución {
const int dr[4] = {1, -1, 0, 0};
const int dc[4] = {0, 0, -1, 1};

public:
bool contiene Ciclo(vector seleccionador) {
int m = grid.size(), n = grid[0].size();
vector seleccionado(n, 0));

para (int i = 0; i) {}
para (int j = 0; j)
si (!vis[i][j]
si (dfs(grid, vis, i, j, -1, grid[i][j]))
retorno verdadero;
}
}
}
devolver falso;
}

privado:
bool dfs(vector identificadovector correspondía caracteres iguales g, vector asignadovector seleccionadointющ vis,
int r, int c, int pr, int pc, char col) {
vis[r][c] = 1;
para (int k = 0; k)
int nr = r + dr[k], nc = c + dc[k];
si (nr < 0 TENIDO TENIDO ENTRE SONIDO= (int)g.size() TENENCIA NO TENIDO NOCREER 0 ANTERIVADA Nc MENT= (int)g[0].size()
continuar;
si (g[nr][nc] != col) continúan;
si (!vis[nr][nc]) {}
si (dfs(g, vis, nr, nc, r, c, col))
retorno verdadero;
} otro si (nr != pr  durable nc != pc) { // visitado, no padre
retorno verdadero;
}
}
devolver falso;
}
};
`` `

■ **Nota para las entrevistas C+** – Tenga cuidado con el tamaño de la pila; use `std::vector` para la matriz 'vis' y pasar por referencia.

-...

## 5. Análisis de la complejidad

← Algorithm Silencio Silencio
Silencio----------------
Silencio DFS (todas las lenguas) Silencio **O(m · n)** Silencio **O(m · n)** – matriz visitada + pila de recursión (caso peor)
Silencio BFS (versión java) Silencio **O(m · n)** Silencio **O(m · n)** – cola + matriz visitada

Ambos son lineales y óptimas; la cuadrícula se puede visitar una vez.

-...

## 6. Artículo del Blog – “Cículos Detectos en un Grid 2-D: El Bien, El Mal, El Ugly”

■ **Meta‐Description* *
■ Master LeetCode 1559 “Ciclos de insectos en 2-D Grid” con soluciones Java, Python y C++. Aprenda la mejor estrategia de DFS, trampas y por qué este problema es un conocimiento imprescindible para su próxima entrevista de instrucciones de datos.

-...

### 6.1 Introduction

Si te preparas para entrevistas técnicas, “Ciclos Detect en 2-D Grid” es un elemento básico.
Combina traversal gráfico, seguimiento de padres y controles de límites cuidadosos, todo dentro de las limitaciones de una red de 500 × 500.

■ **Por qué importa** – Muchos entrevistadores preguntan variaciones de detección de ciclos (lista conectada, gráficos, rejillas). Dominarlo demuestra su capacidad para adaptar un algoritmo básico a diferentes modelos de datos.

-...

### 6.2 El problema revisitado

*(Inscribir la declaración formal con bloque de código.) *

-...

### 6.3 El Bien

1. **DFS es natural** – Tratar a cada célula como un nodo; dos nodos están conectados si comparten un lado * y* contienen la misma letra.
2. **Linear runtime** – O(m · n) es el más rápido que se puede conseguir.
* Datos de prueba de LeetCode* normalmente se ejecuta en 100 ms.
3. **Simple lógica de los padres** – Al pasar las coordenadas de la celda anterior, usted inmediatamente sabe si un vecino visitado es el padre.
*Una única bandera booleana en su matriz 'visitada' es insuficiente; usted debe comprobar la dirección. *

■ **Pro tip** – Escribe un ayudante `dfs(r, c, parent_r, parent_c)` que devuelve `True` tan pronto como se encuentra un ciclo. No es necesario retroceder los resultados después de explorar a todos los niños.

-...

### 6.4 El mal

Silencio Silencio Silencio Silencio
Silencio------------------------
tención Profundidad de recuperación sobre 250 000 (Python, Java) Silencio Rebosa de Stack / RuntimeError tención Use una pila explícita (Python) o levante el límite de recursión en Java (`-Xss`). Silencio
Silencio Olvídate de la condición “parente” _ False positives (p. ej., dos-cell back‐and‐forth) Silencio Compare siempre las coordenadas vecinas con el padre antes de declarar un ciclo. Silencio
tención Re-escaneamiento de la rejilla entera para cada componente TENIDO Tiempo cuadrático ANTE Utilizar una sola matriz visitada; una vez que una célula está marcada, sálvala. Silencio

-...

### 6.5 The Ugly

■ Algunos candidatos escriben código que, aunque lógicamente correcto, es **messy**:

1. **Union‐Find on a grid* *
*Over-engineered for a simple DFS problem. *
Introduce abstracciones pesadas (comprensión por vía, rango) que distraen de la lógica central.
2. ** Estructuras de datos innecesarias* *
*Using `HashSet Garantizado(int,int) =` para cada celda o un mapa clavedo por “letter”. *
Estos golpean la memoria para 250 k células.
3. **Direcciones codificadas por riesgo**
*Using separate `int` arrays for `dr` and `dc` in every function. *
Mientras que rápido, se puede ocultar detrás de bucles anidados y bucles mal indexados.

■ **Takeaway** – Mantenga su solución inclinada: una matriz visitada, un array de dirección y un cheque de padre.

-...

### 6.6 Consejos para el éxito de la entrevista

TENCIÓN TERRITORIO Estrategia TENIDO Casos Edge TENIDO
Silencio--------------------------
Silencio **Java** Silencio Use `int[][] vis` y code parent as a single integer if recursion deep is a concern. Silencio Recordar reiniciar visitado cuando termine un componente. Silencio
Silencio **Python** Silencio Preferir una pila explícita; evitar la repetición. TENIDO Aumentar el límite de recursión (`sys.setrecursionlimit`) *sólo* si confías en la profundidad de la pila. Silencio
Silencio **C++** Silencio Pase vectores por referencia; explíquese acerca de los controles de límites (`r+dr > ) tención Uso `std::vector fielint `` para `vis` en lugar de `bool` para evitar cuestiones firmadas o no firmadas. Silencio

-...

### 6.7 Real‐World Analogies

La detección del ciclo en una cuadrícula es como encontrar un bucle en un laberinto donde sólo se puede caminar a través de las paredes del mismo color.
Imagínese una cuadrícula de la ciudad donde sólo puede viajar por las calles pintadas del mismo color; un ciclo es un paseo cerrado que nunca inmediatamente retraces un paso.

-...

### 6.8 Pensamientos Finales

- **Aplicación una vez, prueba muchos** – Escribe el DFS en cualquier idioma, ejecute contra los tres ejemplos oficiales de LeetCode.
- Mira la condición de los padres... Ese es el corazón de la solución; falta es el bicho más común.
Mantenlo lineal... Cualquier intento cuadrático es una bandera roja para la evaluación de tiempo de ejecución y entrevista.

Con estos snippets Java, Python y C++ en tu toolkit, abordarás con confianza LeetCode 1559 y demostrarás el dominio de la detección del ciclo, una habilidad clave para cualquier entrevista de algoritmo.

-...

### 6.9 Call to Action

■ ¿Listo para nivelar? #
■ Marcar este post, descargar el código snippets, y añadir el problema a su “lista práctica diaria. ”
■ ¿Necesitas ayuda con otro clásico de LeetCode? Deja un comentario o envíame un correo electrónico: ¡feliz para ayudarte a prepararte para tu próxima entrevista de codificación!

-...

## 7. Conclusiones

LeetCode 1559 es directo una vez que entiendes:

* Tratar la cuadrícula como un gráfico no dirigido,
* DFS con seguimiento de padres,
* Tiempo lineal & espacio.

Las soluciones Java, Python y C++ ilustran una implementación limpia que pasará todas las pruebas oficiales e impresionará a los entrevistadores.

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀

-...

*End of article. *