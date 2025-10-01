-...
Título: LeetCode 3242. Servicio de Sum Neighbor -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Panorama general de los problemas

**Design Neighbor Sum Service** – un problema de estilo LeetCode que le pide que apoye dos consultas de tiempo constante en una red *n × n*:

Silencio **Query**
Silencio...
Silencioso `adjacentSum(valor)` tención Sum de los cuatro vecinos cardenales (top, bottom, left, right) que existen. Silencio
Silencio `diagonalSum(valor)` Silencio Sum de los cuatro vecinos diagonales (top-left, top-right, bottom-left, bottom-right) que existen. Silencio

La cuadrícula contiene **distintos** enteros, `0 ≤ valor ' se hizo n2`, y `n` satisfies `3 ≤ n ≤ 50`.
Usted recibirá hasta 2·105` consultas – el servicio debe responder a cada consulta en **O(1)** tiempo.

■ **Por qué este problema importa para la preparación de la entrevista* *
■ Muchas preguntas de la estructura de datos en intervisiones tecnológicas giran alrededor de *grid* traversal y *hash‐mapping*. Dominar este problema le da un patrón reutilizable para los problemas de “lookup por valor”, un conocimiento necesario para cualquier entrevista Java, Python o C++.

-...

## 2. Diseño: “Bien, Mal”

Silencio Silencio
Silencio------------Prince------
Silencio **Pre-procesamiento** Silencio Construir un hash‐map `valor → (row, col)`. Esto convierte una búsqueda ingenua de O(n2) por consulta en O(1). Silencio No hacer nada – cada consulta escanearía toda la red. ← Construye un gigantesco array 3-D (row, col, value) que es desperdicio. Silencio
Silencio **Memoria** Silencio Almacenar la cuadrícula como-es (`vector asignadovector fieltro `` / `int[]`) más un mapa (`unordered_map armonizado, pareado,intento ``). Silencio Asignar coordenadas temporales cada consulta. ← Revise Recursively la cuadrícula en cada llamada – apilar el riesgo de desbordamiento en cuadrículas grandes. Silencio
Silencio ** Manejo de maletas** Silenciosos Comprobaciones de límites explícitos ( < i título0 > , > ...). Silencio Olvídate de manejar las fronteras → `IndexOutOfBounds`. Ø Utilizar una indexación basada en 1 pero la cuadrícula es 0-basada → errores por uno. Silencio
Silencio **Readability** Silencio Limpiar nombres de método, comentarios, y una simple clase de datos para los pares de coordenadas. Demasiados variables globales, estado oculto. ← Recidiva o cortes de lambda que hacen daño a la mantenibilidad. Silencio

**Bottom line** – El diseño “bueno” utiliza un **hash‐map** para la búsqueda instantánea, mantiene el código limpio y maneja las fronteras con seguridad. La variante “mala” es la búsqueda de fuerza bruta; la variante “muy” mezcla lógica recursiva con estado mutable compartido, por lo que es difícil razonar.

-...

## 3. Aplicación

### 3.1 Java (O(1) Query with `HashMap`)

``java
importa java.util. HashMap;
importa java.util. Mapa;

*
* Servicio de Sum de Barrio de Diseño
* https://leetcode.com/problems/design-neighbor-sum-service
*
* Complejidad del tiempo
* Construcción: O(n2)
* Consultas: O(1)
*
* Complejidad espacial
* O(n2) para la rejilla + O(n2) para el mapa del hash
*
* Autor: [Su nombre]
* Date: 2024‐08‐31
*/
clase pública Barrio Sum {}

/** matriz original */
int final privado[][] matriz;
/** tamaño de la cuadrícula */
privada final int n;
/** valor - título (row, col) */
final privado Mapa seleccionado, int[] indexMap;

/** Constructor: cuadrícula de preproceso en O(n2) */
public NeighborSum(int[][] grid) {
esto.n = grid.length;
esto. matriz = nuevo int[n][n];
este.indexMap = nuevo HashMap garantizado(n * n);

para (int i = 0; i)
para (int j = 0; j) {}
int val = grid[i][j];
matriz[i][j] = val;
indexMap.put(val, new int[]{i, j});
}
}
}

* Suma de vecinos adyacentes (hasta, abajo, izquierda, derecha) */
int public adjacentSum(valor único) {}
int[] pos = indexMap.get(valor);
int i = pos[0], j = pos[1];
int sum = 0;

si 0) suma += matriz[i - 1][j]; // superior
si (i + 1 < n) suma += matriz[i + 1][j]; // fondo
[j - 1]; // izquierda
si (j + 1 י n) suma += matriz[i][j + 1]; // right
restitución;
}

* Suma de vecinos diagonales (4 diagonales) */
int public diagonal Sum(valor único) {}
int[] pos = indexMap.get(valor);
int i = pos[0], j = pos[1];
int sum = 0;

si (i √≥ 0 ' Ivoire 0) suma += matriz[i - 1][j - 1]; // top-left
si (i √≥ 0 ' tÃ3 j + 1 י n) suma += matriz[i - 1][j + 1]; // top‐right
si (i + 1 ) no significan 0) suma += matriz[i + 1][j - 1]; // fondo-izquierda
si (i + 1 י n ' t ' t > 1 > n) suma += matriz[i + 1][j + 1]; // bottom‐right
restitución;
}

♪♪ Demo */
public static void main(String[] args) {
int[][] grid = {
1, 2},
{3, 4, 5},
{6, 7, 8}
};
NeighborSum ns = nuevo NeighborSum(grid);

System.out.println("adjacentSum(4) = " + ns.adjacentSum(4)); // 16
System.out.println("diagonalSum(4) = " + ns.diagonalSum(4)); // 16
}
}
`` `

-...

### 3.2 Python 3 (Buscación Diccionaria)

``python
# Design Neighbor Sum Service – Python implementation
# Complejidad del tiempo: Construcción O(n2), Consultas O(1)
# Complejidad espacial: O(n2)

clase NeighborSum:
def __init__(self, grid):
"
:param grid: List[List[int] – n x n matriz de enteros distintos
"
self.n = len(grid)
self.grid = grid
# Valor de mapa - título (row, col)
self.idx = {grid[i][j]: (i, j) for i in range(self.n) for j in range(self.n)}

def adyacente Sum(self, value: int) - título int:
i, j = self.idx[value]
S = 0
si yo > 0: s += self.grid[i - 1][j] # top
si yo + 1 se hizo auto.n: s += self.grid[i + 1][j]
si j > 0: s += self.grid[i][j - 1] # left
si j + 1 se hizo auto.n: s += self.grid[i][j + 1] # right
retorno s

def diagonal Sum(self, value: int) - título int:
i, j = self.idx[value]
S = 0
si > 0 y j > 0: s += self.grid[i - 1][j - 1] # top‐left
si yo 0 y j + 1 se hizo auto.n: s += self.grid[i - 1][j + 1] # top-right
si yo + 1 se hizo a sí mismo.n y j izquierda
si yo + 1 se hizo auto.n y j + 1 se hizo auto.n: s += self.grid[i + 1][j + 1] # bottom‐right
retorno s

# Demo
si __name_ == "__main__":
grid = [[0, 1, 2], [3, 4, 5], [6, 7, 8]]
ns = VecinoSum(grid)
print(ns.adjacentSum(4)) # 16
print(ns.diagonalSum(4)) # 16
`` `

-...

### 3.3 C+17 (Vector + Unordered_map)

``cpp
/ / / Servicio de Suma de vecinos de diseño – implementación C+17
// Compilar con: g++ -std=c+17 -O2 -Wall neighbour_sum.cpp -o neighbour_sum

#include יbits/stdc++.h
usando std namespace;

clase de vecinos {}
public:
NeighborSum(cont vectorial seleccionadovector identificadoint
: n(grid.size()), matriz(grid)
{}
// Construir mapa de hash: valor - edad (row, col)
para (int i = 0; i)
para (int j = 0; j)
pos[grid[i][j] = {i, j};
}

int adyacenteSum(un valor) const {
auto [i, j] = pos.at(valor);
int sum = 0;
si 0) suma += matriz[i - 1][j]; // superior
si (i + 1 < n) suma += matriz[i + 1][j]; // fondo
[j - 1]; // izquierda
si (j + 1 י n) suma += matriz[i][j + 1]; // right
restitución;
}

int diagonal Sum(valor único) const {
auto [i, j] = pos.at(valor);
int sum = 0;
si (i √≥ 0 ' Ivoire 0) suma += matriz[i - 1][j - 1]; // top-left
si (i √≥ 0 ' tÃ3 j + 1 י n) suma += matriz[i - 1][j + 1]; // top‐right
si (i + 1 ) no significan 0) suma += matriz[i + 1][j - 1]; // fondo-izquierda
si (i + 1 י n ' t ' t > 1 > n) suma += matriz[i + 1][j + 1]; // bottom‐right
restitución;
}

privado:
int n;
vector realizador realizado en matriz de confianza;
unordered_map seleccionadaint, par observadoint,int hilo conductor pos; // valor - coordenadas de título
};

/* -------- Demo...
int main() {}
vectorial realizador realizador fieltro red = {
1, 2},
{3, 4, 5},
{6, 7, 8}
};

NeighborSum ns(grid);
cout se hizo "adjacentSum(4) = " 0 se hizo no.adjacentSum(4)  se realizó '\n'; // 16
cout se llevó a cabo "diagonalSum(4) = " 0 se realizaron no.diagonalSum(4)  se realizó '\n'; // 16
}
`` `

-...

## 4. Pitfalls comunes " Cómo evitarlos

Silencio Pitfall Silencio
Silencio...
Silencio **O(n2) escaneo por consulta** Silencio Store coordenadas en un hash‐map (`valor → (row, col)`). Silencio
Silencio **Missing boundary checks** Silencio Siempre guarde con `if (row confía0)`, `si (col observadon-1)` ... antes de acceder a `matrix[row][col]. Silencio
TEN **Off‐by-one errors** TENGA a la indexación basada en 0 para la red y el mapa. Silencio
Silencio **Mutable estado compartido en recursión** Silencio Evitar la recursión; usa el mapa para mantener la lógica iterativa y pura. Silencio

-...

## 5. Consejos de entrevista

1. **Explicar el mapa primero** – “Prepararé una tabla de búsqueda para que cada consulta sea O(1). ”
2. **Mostrar la lógica del límite** – “Nota que la fila superior no tiene un vecino ‘up’, por lo que protegemos con ‘row Conf0’. ”
3. **Hablar sobre los cambios de memoria** – “La propia red es O(n2), el mapa también es O(n2). Dado 'n ≤ 50', eso es trivial para los servidores modernos. ”
4. **Use una función limpia y testable** – escriba un pequeño `demo()` o `main()` que imprime valores esperados; los entrevistadores les encanta ver cheques de corrección rápida.
5. **Medidas de complejidad del tiempo** – “La construcción toma 2,500 pasos para una cuadrícula de 50×50; cada consulta es sólo 4 o 8 Lookups, es decir, tiempo constante. ”

-...

## 6. Final Takeaway

The *Design Neighbor Sum Service* problem is a **pattern‐builder** for interviewers and interviewees alike:

* **Pre-procesamiento + hash‐map** = búsqueda instantánea, fronteras seguras, código limpio.
* Búsqueda bruta-fuerza = demasiado lento y error-prone.
* Las soluciones Recursive “muy” duelen la legibilidad y pueden romper grandes insumos.

Al dominar la solución “buena” en **Java, Python y C++**, tendrás un kit de herramientas reutilizable para preguntas **valor por valor** que aparecen en casi todas las entrevistas tecnológicas. Buena suerte: su próxima ronda de codificación es ahora un poco más fácil de romper!