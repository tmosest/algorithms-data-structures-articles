-...
Título: LeetCode 1345. Juego de salto IV -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Juego de salto IV – Problema " bueno, malo, ugly "

Silencio
Silencio...
Silencio **Problema** Silencio Estás de pie en el primer índice de un array entero `arr`. En un movimiento se puede saltar a " i+1 " , " i-1 " , o cualquier índice " j " tal que `arr[i] == arr[j] " . Encuentra el número mínimo de movimientos requeridos para alcanzar el último índice. Silencio
TENIDO **Constraints** TENIDO `1 ≤ arr.length ≤ 5·104`, `-108 ≤ arr[i] ≤ 108` Silencio
Silencio **Key Observation** Silencio El problema es un problema más corto en un gráfico implícito – cada posición de matriz es un nodo, y los bordes existen entre índices consecutivos y entre índices de igual valor. Una primera búsqueda (BFS) garantiza el número mínimo de pasos. Silencio
Silencio **Bien** Silencio • BFS visita cada nodo exactamente una vez. <br confianza• O(n) time > O(n) extra space – óptimo para las limitaciones dadas. • Sencillo a razonar sobre " fácil de implementar. Silencio
Silencio **Bad** Silencio • La implementación ingenua que sigue visitando los mismos índices de igual valor una y otra vez conduce a O(n2) o peor. • Algunas personas olvidan marcar la lista del valor como “procesada” después de la primera visita, causando un error de tiempo-limitado. Silencio
Silencio **Ugly** Silencio • Usar un `HashSet` de `int[]` como claves, o convertir el array a una cadena para la piratería – ambos son innecesarios y lentos. • Reiniciar la recursión o el DFS puede causar desbordamiento de pila para grandes entradas. Silencio

-...

## 2. Soluciones

A continuación se presentan implementaciones limpias y totalmente agregadas en **Java, Python, y C++**.
Los tres comparten la misma estrategia BFS:

1. Construir un `Map realizadovale, Lista de los índices conveniente`.
2. Use una cola para BFS; almacene el índice actual y el número de movimientos tomados.
3. Cuando visite un nodo, enqueue sus índices de valor igual, " i-1 " .
4. Inmediatamente **clarar** la lista para ese valor – esto garantiza que cada lista sea procesada al máximo una vez.

#### 2.1 Java – `Solution.java `

``java
importar java.util*;

*
* 1345. Juego de salto IV
* BFS – O(n) time, O(n) space
*/
Clase Solución {
public int minJumps(int[] arr) {
int n = arr.length;
si (n ==1) retorno 0; // ya en el último índice

// 1. Construir mapa de valor a todos los índices que tengan ese valor
Mapa:Integer, Listo:Integer títuloIndices = nuevo HashMap incorrecto();
para (int i = 0; i)
valueIndices.computeIfAbsent(arr[i], k - título nuevo ArrayList recomendado()).add(i);
}

// 2. Estructuras BFS
boolean[] visited = new boolean[n];
visitado[0] = verdadero;
Búsquedas realizadasInteger título q = nuevo ArrayDeque corresponde();
q.offer(0); // comenzar desde el índice 0

int moves = 0;
(!q.isEmpty()) {
nivel intTamaño = q.size(); // nodos a la distancia actual
para (int s = 0; s) {}
int idx = q.poll();

// Compruebe los tres destinos posibles
// a) i+1
si (idx + 1 == n - 1) movimientos de retorno + 1;
si (idx + 1 < n " círculo !visited[idx + 1] {
visitado[idx + 1] = verdadero;
q.offer(idx + 1);
}

// b) i-1
si (idx - 1 == n - 1) movimientos de retorno + 1;
si (idx - 1 ≤= 0 " ventaja !visited[idx - 1] {
visitados[idx - 1] = verdadero;
q.offer(idx - 1);
}

// c) Todos los índices j donde arrr[idx] == arrr[j]
Lista realizadaInteger igualesValIdx = valorIndices.get(arr[idx]);
para (int j : sameValIdx) {
si (j == n - 1) movimientos de retorno + 1;
si (!visited[j]) {}
visitado[j] = verdadero;
q.offer(j);
}
}
// Importante: aclarar la lista para evitar revisitar estos bordes
mismoValIdx.clear();
}
moves++; // final del proceso nivel actual
}

retorno -1; // nunca debe suceder para una entrada válida
}
}
`` `

-...

### 2.2 Python – `solution.py `

``python
de las colecciones importan defaultdict, deque
de la importación Lista

Solución de clase:
def minJumps(self, arr: List[int] int:
n = len(arr)
si n == 1:
retorno 0

# Valor de construcción → índices cartografía
val_to_idx = defaultdict(list)
para i, v en enumerate(arr):
val_to_idx[v].append(i)

visitado = [False] * n
visitado[0] = Verdadero
q = deque([0]) # La cola BFS contiene índices

movimientos = 0
mientras q:
para _ en rango(len(q)):
idx = q.popleft()

# Jump to idx+1
si idx + 1 == n - 1:
movimientos de retorno + 1
si idx + 1 < n y no visitados[idx + 1]:
visitado[idx + 1] = Verdadero
q.append(idx + 1)

# Jump to idx-1
si idx - 1 == n - 1:
movimientos de retorno + 1
si idx - 1 mento= 0 y no visitados[idx - 1]:
visitados[idx - 1]
q.append(idx - 1)

# Jump to all equal-value indices
para j en val_to_idx[arr[idx]:
si j == n - 1:
movimientos de retorno + 1
si no es visitado[j]:
visitado[j] = Verdadero
q.append(j)

# Importante: nunca volver a ver este valor de nuevo
val_to_idx[arr[idx]].clear()

movimientos += 1

retorno -1
`` `

-...

### 2.3 C++ – `Solution.cpp `

``cpp
#include יbits/stdc++.h
usando std namespace;

/*
* 1345. Juego de salto IV
* BFS – O(n) time, O(n) space
*/
Clase Solución {
public:
int minJumps(vector fieltro arr) {
int n = arr.size();
(n == 1) retorno 0;

// 1. Mapa del valor a la lista de índices
unordered_map madeint, vector mp;
para (int i = 0; i)
mp[arr[i]].push_back(i);

vector asignadobool confianza visitado(n, false);
queue indicaint
q.push(0);
visitado[0] = verdadero;

int moves = 0;
(!q.empty()) {
int sz = q.size();
para (int _ = 0; _ iere sz; ++_) {
int idx = q.front(); q.pop();

// idx+1
si (idx + 1 == n - 1) movimientos de retorno + 1;
si (idx + 1 < n " círculo !visited[idx + 1] {
visitado[idx + 1] = verdadero;
q.push(idx + 1);
}

// idx-1
si (idx - 1 == n - 1) movimientos de retorno + 1;
si (idx - 1 ≤= 0 " ventaja !visited[idx - 1] {
visitados[idx - 1] = verdadero;
q.push(idx - 1);
}

// Todos los índices de valor igual
auto &vec = mp[arr[idx];
para (int j : vec) {
si (j == n - 1) movimientos de retorno + 1;
si (!visited[j]) {}
visitado[j] = verdadero;
q.push(j);
}
}
vec.clear(); // procesado una vez
}
++moves;
}
retorno -1; // inalcanzable - nunca se activa para una entrada válida
}
};
`` `

-...

## 3. Artículo del Blog – “Juego IV: Mastering BFS for LeetCode Interviews”

■ *Título*
■ **Juego del juego IV – código Leet 1345**: Optimal Java / Python / C++ Solución BFS

■ **Meta Descripción**:
■ Descubra la solución BFS más rápida de LeetCode *Jump Game IV*. Aprenda Java, Python y C++ implementaciones, trucos de optimización y conocimientos de entrevista.

-...

#### 3.1 Introducción

Si te estás preparando para una entrevista técnica o tocando el “Juego IV” de LeetCode (problema #1345), te darás cuenta rápidamente de que el ingenuo enfoque “juego a cada valor igual” sopla en el tiempo. El secreto es tratar el array como un gráfico y utilizar **Breadth‐First Search (BFS)** para encontrar el camino más corto. En este artículo caminamos a través del algoritmo, ilustramos por qué funciona, y proporcionamos código limpio en **Java, Python, y C+**.

■ **Keywords**: `Jump Game IV`, `Leetcode 1345`, `BFS`, `minimum jumps`, `array jumps`, `Java solution`, `Python solution`, `C++ solution`, `competitive programming`, `interview coding`.

-...

### 3.2 Declaración de problemas (Reescrita para la claridad)

Se le da una matriz unidimensional de enteros `arr`.
Usted comienza en el índice `0` y desea alcanzar el último índice (`arr.length-1`).
En un solo paso puedes:

1. Saltar a " i + 1 " (si existe).
2. Salta a " i - 1 " (si existe).
3. Saltar a cualquier índice `j` tal que `arr[i] == arr[j]`.

Regrese el número mínimo de pasos** requerido para alcanzar el último índice.
Si la longitud del array es `1`, la respuesta es `0` (ya estás allí).

-...

### 3.3 Ejemplo Walk-through

Silencioso `arr` Silencio `i` Silencio `i-1` Silencioso `i+1` Silencio igual indices Silencioso
Silencio------------------------------------------------------------------
[100, -23, -23, 404, 100, 23, 23] " Silencio 0 Silencio – Silencio 1 Silencio 4 Silencio Saltar desde 0 → 4 en un paso (valor igual). Silencio
Silencio De 4, puede ir a 5 o cualquier índice con el valor 100. Silencio 4 Silencio 3 Silencio 5 Silencio 0 Silencio, etc.

El camino óptimo para este array es: `0 → 4 → 5 → 6 → 7` → **4 pasos**.

-...

### 3.4 Algorithm Design

1. ** Modelo Gráfico* *
- Nodos: índices de array No.
- Edges:
* `i ↔ i+1` (si está dentro de los límites).
* `i ↔ j ' cuando `arr[i] == arr[j]`.

Este gráfico es **sin peso**, por lo que BFS da la longitud más corta del camino.

2. **Procesamiento previo**
Construir un mapa de hash: `valor → lista de todos los índices que tienen ese valor`.
Complejidad: `O(n)`.

3. **BFS Execution**
* Mantener un `queue observadoint] (o `deque' en Python/C++).
* Mantenga una matriz 'visitada[n]` para evitar revisiting nodes.
* Por cada índice de popped `i`, enqueue:
* " i-1 " (si es válida y no visitada).
* " i+1 " (si es válida y no visitada).
* Cada índice " j " en " índices[arr[i] " (excepto " i " ).
* **Clear** `valorIndices[arr[i]]` después de la primera visita - esto garantiza que cada lista de bordes de igual valor se procesa una vez.

4. *Cuento de viaje*
Seguimiento de cuántos niveles hemos ampliado (`moves`).
Cuando encubrimos un destino que es el último índice, devuelve `moves+1`.

4. * Terminación*
Dado que todos los bordes se procesan, el algoritmo siempre termina con una respuesta.

-...

### 3.5 ¿Por qué “Clear Después de la Primera Visita” es crítico

Sin aclarar la lista de índices iguales, cada nodo intentaría saltar a todos los nódulos iguales en cada visita, lo que llevaría a un golpe de `O(n^2).
Al despejar después de la primera vez que atraviesamos un valor particular, cortamos el número de bordes que exploramos a ** en la mayoría `n`**.
Esta es la optimización principal que convierte una solución brute-force en un algoritmo rápido `O(n)`.

-...

### 3.6 Complexity Analysis

TEN TERRITORIO TEN TERRITORIDAD
Silencio...
Silencio Edificio hash mapa Silencioso `O(n)` Silencio
← BFS traversal Silencio Cada nodo visitado una vez, cada borde examinado a la vez → `O(n)` Silencio
TENIDO TODO TENIDO **`O(n)` time** y **`O(n)` espacio**

Esto satisface los requisitos para las limitaciones de nivel de entrevista.

-...

### 3.7 Aspectos destacados de la implementación

##### Java
- Usa `ArrayDeque` (más tarde que `LinkedList` para cola).
- `ArrayList` para la cartografía; `clear()` se llama para evitar el procesamiento.

#### Python
- `defaultdict(list)` almacena índices.
- `deque ' for O(1) pop/append operations.
- List clearing with `clear()`.

###### C++
- " noordered_map armonizado, vector asignadoint título " da un promedio de búsquedas O(1).
- `vector asignadobool `` para banderas visitadas.
- `queue hacíaint] (o `std::deque` si lo prefieres) para BFS.

-...

### 3.8 Pitfalls comunes & Fixes

Silencio Pitfall Silencio
Silencio...
Silencio **Republicación de los bordes del mismo valor en repetidas ocasiones** Silencio Después de visitar el índice `i`, llame `mp[arr[i].clear()` o `val_to_idx[arr[i].clear()`. Silencio
Silencio **Missing bounds checks** tención Siempre cheque `i-1 √= 0 ' y ' i+1 " se hicieron " antes de empujar. Silencio
Silencio **No usar array visitado** Silencio Usar un array booleano para saltar nodos ya procesados; de lo contrario obtendrás bucles infinitos. Silencio
Silencio **Regresar antes de aumentar el nivel** Silencio En BFS, devolver `moves+1` *después de procesar el nivel, no inmediatamente después de saltar, a menos que haya encontrado el objetivo. Silencio

-...

### 3.9 Recibido para Entrevistas

* Treat arrays como gráficos.
* Problemas cortos sin peso → BFS.
* Pre-proceso para colapsar múltiples bordes (claro después de la primera visita).
* Mantener banderas visitadas para evitar la reexploración.
* Mantenga el nivel contrario a la distancia calculada.

Dominar este patrón le ayudará a resolver otros problemas de LeetCode como “Juego de Bombas” (problemas 55, 1302) y puzzles basados en gráficos.

-...

### 3.10 Pensamientos Finales

La solución BFS a *Jump Game IV* es elegante y funciona en tiempo lineal, lo que hace que sea eficiente y fácil de explicar durante una entrevista técnica. Ya sea que estés en codificación en Java, Python o C++, la idea clave sigue siendo: **Proceso de bordes de igual valor sólo una vez**.
Siéntase libre de copiar los fragmentos de código arriba en su editor local, realizar pruebas, y tweak según sea necesario. ¡Buena suerte cortando tus puntuaciones de LeetCode!

-...

### 3.11 Más lectura

- [LeetCode 1345 – Jump Game IV on Discuss] (https://leetcode.com/problems/jump-game-iv/)
- [Apoyo BFS en Depth - Serie de YouTube por "The Coding Train"]
- [Teoría Gráfico en Programación - Libro de Mark Allen Weiss]

-...

### 3.12 Finalidad del artículo

-...

■ **End of Blog**
■ (No dude en compartir sus propias soluciones, añadir comentarios o hacer preguntas. ¡Feliz codificación!)

-...

**Aquí lo tienes**: un completo, entrevistado a través y código para LeetCode *Jump Game IV*. La estrategia BFS no sólo garantiza un rendimiento óptimo, sino que también demuestra un patrón poderoso aplicable a muchos otros desafíos más cortos. ¡Feliz codificación!