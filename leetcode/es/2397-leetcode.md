-...
Título: LeetCode 2397. Filas máximas cubiertas por columnas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 2397. Filas máximas cubiertas por columnas – Código de 3-Way, Blog y SEO de Job‐Ready

■ **TL;DR**
■ *Problema:* Elija exactamente las columnas `numSelect` de una matriz binaria `m × n` para cubrir el número máximo de filas (una fila es *cubierta* si cada `1` en esa fila se encuentra en una columna elegida).
■ *Mensaje clave:* Las limitaciones son pequeñas (`n ≤ 12`), por lo que una solución **bitmask + backtracking** es tanto simple como rápida.
■ *Complejidad:* `O(n choose numSelect) · m · n )` tiempo, `O(1)` espacio extra.

A continuación encontrará:

1. Un blog optimizado **SEO** explicando el problema, las trampas y el algoritmo en inglés claro.
2. Tres implementaciones de trabajo – **Java**, **Python**, y **C+** – que puedes copiar-paste en LeetCode.
3. Una sección rápida “de qué hablar en una entrevista”.

-...

## The Problem (LeetCode 2397)

``text
Entrada: matriz: List[List[int]], numSelect: int
Salida: int // número máximo de filas que pueden ser cubiertas
`` `

- `matrix` is `m × n`, `0 ≤ m,n ≤ 12`, entries are `0` or `1`.
- Debes elegir, exactamente, columnas distintas.
- Una fila está cubierta* si todos* `1` en esa fila se encuentra en una columna elegida (o la fila no tiene '1's).

■ Ejemplo
[0,0,0],[1,0,1],[0,1,1],[0,0,1]], numSelect = 2 → ****

-...

## Por qué funciona la fuerza bruta (pero sigue siendo una mala idea)

Con `n ≤ 12`, el número total de subconjuntos de columna es `2^n ≤ 4096`.
Usted podría enumerar todos los subconjuntos y elegir los de tamaño `numSelect`.
Está bien **time-wise**, pero el código se pone ruidoso, y es difícil de explicar en una entrevista.

Sin embargo, el enfoque **backtracking** refleja naturalmente el árbol de decisiones:
*Pick the current column?* – *or skip it?* – y prune cuando ya has elegido `numSelect` columnas.
Esto produce código limpio y recursivo que es fácil de leer, probar y extender.

-...

## Core Idea – Bitmask + Backtracking

1. **Representar un conjunto de columnas seleccionadas como bitmask** (un `int` donde bit `j` = 1 α columna `j` seleccionada).
2. **Recursive DFS**:
* `idx` – índice de columna actual (0 ... n-1).
* " cnt " - número de columnas ya elegidas.
* `mask` - máscara de columnas elegidas.
3. **Caso base**: cuando `cnt == numSelect` → Contar filas cubiertas.
4.
* * * *Pick* columna `idx` → establecer su bit, recurse con `cnt+1`.
* * *Skip* column `idx` → leave bit 0, recurse with same `cnt`.
5. **Pruning**: si las columnas restantes son menos que las columnas todavía necesarias, deténgase temprano.

Contando filas cubiertas para una determinada `masca` es `O(m · n)` – lo suficientemente pequeña para nuestras limitaciones.

-...

## Complexity

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio Enumerating all subsets of size `k` Silencio `O(n choose k) · m · n)` Silencio `O(1)` Silencio
Silencio Contando filas para una máscara Silencioso `O(m · n)` Silencio
Silencioso en la profundidad de la recesión (además de la pila de llamadas)

Porque `(12 elegir 6) = 924` en el peor de los casos, el algoritmo funciona en mucho menos de un milisegundo en LeetCode.

-...

## 1. Java (LeetCode Style)

``java
Clase Solución {
int m privado, n, target;
int privado[][] mat;

máximo de entrada públicaMatrinas(int[][][] matriz, int numSelect) {
este.mat = matriz;
esto.m = matriz.length;
this.n = matriz[0].length;
esto. objetivo = num Seleccione;
dfs(0, 0, 0);
}

int privado dfs(int idx, int cnt, int mask) {
si (cnt == target) // hemos elegido suficientes columnas
recuento de retornoCovered(mask);

si (idx == n) // no más columnas a considerar
retorno 0;

int remaining = n - idx;
si (conservar + cnt)
retorno 0;

// Opción 1: elegir esta columna
int pick = dfs(idx + 1, cnt + 1, máscara tención (1 ненное)

// Opción 2: saltar esta columna
int skip = dfs(idx + 1, cnt, máscara);

devolver Math.max(pick, skip);
}

cuenta de entrada privada Covered(int mask) {
int covered = 0;
para (int i = 0; i)
booleano ok = verdadero;
para (int j = 0; j) {}
si (mat[i][j] == 1 " , (mask " (1 " identificado j) == 0)
ok = falso;
ruptura;
}
}
(ok) covered++;
}
retorno cubierto;
}
}
`` `

-...

## 2. Python (3.8+)

``python
Solución de clase:
def máximo Rows(self, mat: List[List[int]], numSelect: int) - confiar int:
self.mat = mat
self.m = len(mat)
self.n = len(mat[0])
auto. objetivo = num Seleccione
volver a sí mismo._dfs(0, 0, 0)

def _dfs(self, idx: int, cnt: int, mask: int) - título int:
si cnt == uno mismo. objetivo:
volver a sí mismo._count(mask)

si idx == self.n:
retorno 0

restante = self.n - idx
si restante + cnt se hizo uno mismo. objetivo:
retorno 0

# Pick
pick = self._dfs(idx + 1, cnt + 1, mask tención (1 )
# Skip
skip = self._dfs(idx + 1, cnt, mask)
volver max(pick, skip)

def _count(self, mask: int) - título int:
cubiertos = 0
por fila en sí mismo. mat:
OK = True
for j, val in enumerate(row):
si val y no (mask " (1 iere escrito j)):
ok = Falso
descanso
Si está bien:
cubiertos += 1
retorno cubierto
`` `

-...

## 3. C++ (GNU C+17)

``cpp
Clase Solución {
public:
máximo Filas (vector realizador seleccionado) {
m = matriz.size();
n = matriz[0].size();
mat = matriz;
objetivo = num Seleccione;
dfs(0, 0, 0);
}

privado:
vector de vectores mat;
int m, n, target;

int dfs(int idx, int cnt, int mask) {
si (cnt == target) // ya se seleccionaron suficientes columnas
recuento de retornoCovered(mask);
si (idx == n) retorno 0; // corrió fuera de columnas

int remaining = n - idx;
si (conservar + cnt)
retorno 0;

// Columna actual
int pick = dfs(idx + 1, cnt + 1, máscara tención (1 ненное)

// Saltear la columna actual
int skip = dfs(idx + 1, cnt, máscara);

volver max(pick, skip);
}

int count Covered(int mask) {
int covered = 0;
para (int i = 0; i) {}
bool ok = verdadero;
para (int j = 0; j)
si (mat[i][j] == 1 " ventaja !(mask " (1 " identificado j))
ok = falso;
ruptura;
}
}
(ok) covered++;
}
retorno cubierto;
}
};
`` `

-...

## “De qué hablar en una entrevista”

1. **Declarar las limitaciones** (`n ≤ 12`) → permite algoritmos exponenciales.
2. **Explicar la representación de bitmask** – esto muestra instantáneamente que puede codificar conjuntos de columna en el espacio `O(1)`.
3. **Mostrar el árbol de recursión DFS** – “pick or skip” – y por qué la poda es segura.
4. **La complejidad** – resaltar que el algoritmo es *optimal para las limitaciones dadas*.
5. **Alternativas de mención** – un simple bucle sobre combinaciones o una solución "next_permutation" – sólo para mostrarle los cambios.
6. **Por qué es un buen problema de entrevista** – pruebas de recursión, manipulación de bits y conteo cuidadoso.

-...

## SEO Palabras clave (para páginas de búsqueda de trabajo)

- LeetCode 2397
- Maximum Rows Cubierta por Columnas
- algoritmo de retroceso
- Solución de Bitmask
- Solución Java 17 LeetCode
- Python 3 solución LeetCode
- C++ Solución LeetCode
- Preguntas de entrevista de ingenieros de software
- Preparación de la entrevista de Algorithm
- Entrevista de la estructura de datos

Incluye estas etiquetas en tu Enlace En post o blog personal para atraer reclutadores buscando candidatos que puedan resolver problemas LeetCode de manera eficiente.

-...

## Palabras finales

- El enfoque **backtracking + bitmask** le da código limpio y mantenible que es fácil de explicar.
- La complejidad del tiempo está bien dentro de los límites del problema – terminarás en milisegundos.
- Destaca el algoritmo en su próxima entrevista: “Tratamos las columnas como bits, caminamos el árbol de decisiones, y contamos filas cubiertas sólo una vez por hoja. ”

Buena suerte con la entrevista, y feliz codificación!