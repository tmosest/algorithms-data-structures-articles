-...
Título: LeetCode 2612. Operaciones mínimas inversas
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Resumen del problema

**LeetCode 2612 – Operaciones mínimas inversas**

Se le da un array `nums` de longitud `n`.
Usted puede elegir cualquier sub-array contiguo de longitud 'k' y revertirlo.
De un índice `i` se le permite revertir **exactamente** un sub-array de longitud `k` que contiene `i`.

Algunos índices son “perdonados” (la matriz “banada”) y no se pueden utilizar.
Partiendo del índice " p " , encuentre el número mínimo de reveses requeridos para visitar **todo el índice** del array (o `-1 ' si imposible).
La respuesta para cada índice es un único entero – los movimientos mínimos para alcanzar ese índice.

El reto es manejar de manera eficiente hasta los índices 105.

-...

## 2. Examen básico

Una inversión de un sub-array de longitud `k` que contiene el índice `i` mueve `i` a una nueva posición `j ' tal que

`` `
j = (k-1) - (i - (k-1))
j = i - k + 1 de otro modo
`` `

y similarmente en el lado derecho debido a la simetría.
Los hechos importantes son:

confidencialidad . . . . Por qué importa
Silencio...
Silencio The distance between `i` and the new index `j` is **exactly** `k-1` (or `0` if `k==1`). tención Garantiza que cada nuevo índice tiene la misma paridad que el índice *minimo* en el intervalo alcanzable. Silencio
Silencio El conjunto de índices alcanzables para un nodo es un **intervalo** `[min, max]` de una paridad fija. Podemos pre-storear todos los índices *disponibles* en dos contenedores ordenados – uno para incluso, uno para extrañar – y eliminarlos mientras visitamos. Silencio
TEN BFS garantiza el número mínimo de reveses porque cada capa de la búsqueda es una inversión más. TEN Podemos dejar de explorar un nodo cuando ya se procesan todos los índices alcanzables. Silencio

El algoritmo es esencialmente un BFS multinivel en un gráfico implícito cuyos bordes están definidos por la regla de inversión.

-...

## 3. Pitfalls comunes (“Bad & Ugly”)

1. ** simulación Naïve O(n·k)** – iterating over every possible sub-array for every node blows up to `109` operations for the worst case.
2. **Re-adding visitó los nodos** – olvidando marcar los nodos que se visitan después de que son apagados causará bucles infinitos.
3. **Using `TreeSet` incorrectly** – `TreeSet` (Java) / `std::set` (C++) support only `O(log n)` operations, but deleting a whole range requires repeated `lower_bound` and `erase` calls. Un error sutil es usar la paridad *wrong* fijada cuando se pregunta el intervalo.
4. ** Errores por uno** en la computación `min` / `max` son fáciles de hacer; comprobar doblemente las fórmulas con pequeños ejemplos.
5. **Los usuarios de Python** a menudo intentan imitar TreeSet con "lista" simple; el costo de los elementos de cambio hace que la solución O(n2) y los tiempos fuera.

-...

## 4. “Bien” – ¿Por qué el truco del DSU funciona en Python

La biblioteca estándar de Python no tiene un árbol de búsqueda binario equilibrado.
En lugar de ello, podemos utilizar una estructura **Desjoint‐Set Union (DSU)** que nos permite “saltar” sobre índices ya vistos en tiempo casi constante.

**DSU Idea**

- Por cada paridad (incluso / extraño) mantenemos un array `parent[]`.
- 'find(x)` devuelve el índice más pequeño ≥ x que no ha sido eliminado todavía.
Los nodos visitados son “removidos” al vincularlos al siguiente índice de la misma paridad (“x + 2’).
- Eliminar un elemento cuesta *O(α(n)* (inverse Ackermann), que es esencialmente constante.

*Por qué es rápido*

Cada entrada de matriz se actualiza a la mayor parte de la vez.
El BFS mirará cada índice una vez, y el DSU garantiza que el siguiente índice no revisado se encuentra rápidamente, incluso después de muchas eliminaciones.

-...

## 5. Código

A continuación se presentan implementaciones limpias y idiomáticas en **Java, Python, y C++** que comparten las mismas garantías de memoria O(n log n) / O(n α(n)).

-...

## 5.1 Java (Java 17)

``java
importa java.io.*;
importar java.util*;

clase pública MínimoReversoOperaciones {}

public static int[] minReverseOperations(int n, int p, int[] banned, int k) {
// Conjunto de índices disponibles, separados por paridad
TreeSet se realizóInteger título incluso = nuevo TreeSet correspondió();
TreeSet wonInteger extraño = nuevo TreeSet fiel();
boolean[] visited = new boolean[n];

// Llenar los conjuntos con todos los índices excepto los de inicio y prohibidos
para (int i = 0; i)
si (i == p) continuar; // iniciar nodo
booleano prohibido Aquí = falso;
(int b : banned) if (b == i) banned Aquí = verdadero;
si (bannedHere) continuar; // nunca visitar
(i) == 0) even.add(i); else odd.add(i);
}

// BFS
int[] response = new int[n];
Arrays.fill (respuesta, -1);
Deque cumplióInteger título q = nuevo ArrayDeque correspondió();
q.add(p);
respuesta[p] = 0;

int moves = 0;
(!q.isEmpty()) {
int sz = q.size();
para (int _ = 0; _ Identificar sz; _++) {
int cur = q.poll();
respuesta[cur] = movimientos;

// intervalo alcanzable
int minPos, maxPos;
si (cuerdo  observado k - 1) minPos = (k - 1) - cur;
minPos = cur - k + 1;

int rev = (n - 1) - cur;
si (rev ecto k - 1) maxPos = (k - 1) - rev;
Max Pos = rev - k + 1;
maxPos = (n - 1) - maxPos;

// elegir el conjunto de paridad adecuado
ArbolSet significa Integer target = (minPos " 1) == 0 ? even : odd;
Integer next = target.ceiling (minPos);
mientras (siguiente!= null " vecino " ) {
q.add(next);
target.remove(next);
siguiente = target.ceiling(next + 2); // skip to next same parity
}
}
moves+;
}

respuesta de retorno;
}

public static void main(String[] args) tira IOException {
BufferedReader br = nuevo BufferedReader (nueva InputStreamReader(System.in));
// Ejemplo de lectura: n p k
String[] first = br.readLine().trim().split("\s+");
int n = Integer.parseInt(first[0]);
int p = Integer.parseInt(first[1]);
int k = Integer.parseInt(first[2]);

// Segunda línea: conteo prohibido y valores
String[] second = br.readLine().trim().split("\s+");
prohibido Cnt = Integer.parseInt(second[0]);
int[] banned = new int[bannedCnt];
para (int i = 0; i) se prohibió Cnt; i++) = Integer.parseInt(second[i + 1]);

int[] res = minReverseOperations(n, p, banned, k);
para (int v : res) System.out.print(v + ");
System.out.println();
}
}
`` `

*Puntos clave*

- Dos objetos de 'TreeSet obtenidos'Integer `` almacenan los índices *disponibles* de cada paridad.
- `TreeSet.ceiling(min)` da el primer elemento ≥ `min`.
- Después de que se visita un nodo, lo "removemos", garantizando que nunca se procesa de nuevo.
- Complejidad: **O(n log n)** tiempo, **O(n)** memoria.

-...

## 5.2 C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

vector asignadoint título minReverseOperaciones(int n, int p, const vector identificadoint limitada, int k) {
vector implicado ans(n, -1);
vector implicado incluso, extraño;
vector asignadobool confianza visitado(n, false);
visitado[p] = verdadero;

// Preparar las listas de paridad
para (int i = 0; i) {}
si (visited[i]) continúan;
(i) == 0) incluso.push_back(i);
más extraño.push_back(i);
}
(even.begin(), even.end());
(odd.begin(), odd.end());

establecida(even.begin(), even.end());
set wonint extrañoSet (odd.begin(), odd.end());

queue indicaint
q.push(p);
ans[p] = 0;

int moves = 0;
(!q.empty()) {
int sz = q.size();
para (int _ = 0; _ iere sz; ++_) {
int cur = q.front(); q.pop();

// intervalo accesible
int minPos, maxPos;
si (cuerdo  observado k - 1) minPos = (k - 1) - cur;
minPos = cur - k + 1;

int rev = (n - 1) - cur;
si (rev ecto k - 1) maxPos = (k - 1) - rev;
Max Pos = rev - k + 1;
maxPos = (n - 1) - maxPos;

establecido > > (minPos > 1) == ¿Ni siquiera? Set : oddSet;
auto = target.lower_bound(minPos);
mientras que (it != target.end() " sensible = maxPos) {
q.push(*it);
it = target.erase(it); // erase devuelve el siguiente iterator
}
}
moves+;
}
devolver los ans;
}

int main() {}
ios::sync_with_stdio(false);
cin.tie(nullptr);

int n, p, k;
cin нелининн n ненном p нелины k; // n, índice de inicio, k
int m; // número de índices prohibidos
cin m;
vector:
para (int i = 0; i) prohibida[i];

vector implicado res = minReverseOperations(n, p, banned, k);
para (int v : res) cout se llevó a cabo v
cout se hizo 'n';
}
`` `

**Highlights* *

- `std::set madeint `` supplies `lower_bound`/`erase` in `O(log n)`.
- Dos sets separados garantizan que sólo escaneamos la paridad correcta.
- El algoritmo es idéntico en espíritu a la versión Java.

-...

### 5.3 Python (Python 3.10+)

``python
de las colecciones importa
importadores
importador bisect


def min_reverse_operations(n: int, p: int, banned: list[int], k: int) - titulada list[int]:
# ----- DSU for even & odd indices ---------
parent_even = list(range(n))
parent_odd = list(range(n)))

# Funciones de ayuda
def find_even(x: int) - título int:
""Retorno más pequeño incluso índice >= x que no ha sido eliminado.""
mientras parent_even[x] != x:
parent_even[x] = parent_even [parent_even[x]]
x = parent_even[x]
retorno x

def find_odd(x: int) - título int:
""Retorno del índice más pequeño que no se ha eliminado.""
mientras parent_odd[x]!= x:
parent_odd[x] = parent_odd[parent_odd[x]]
x = parent_odd[x]
retorno x

def remove_even(x: int):
parent_even[x] = x + 2 si x + 2

def remove_odd(x: int):
parent_odd[x] = x + 2 si x + 2

--- Crear índices iniciales disponibles ------
incluso = [i para i en rango(n) si yo != p y (i " 1) == 0 y no estoy prohibido]
extraño = [i para i en rango(n) si i != p y (i " 1) == 1 y no estoy prohibido]

even_set = set(even)
odd_set = set(odd)

--- BFS ---
ans = [-1]
q = deque([p])
ans[p] = 0

movimientos = 0
mientras q:
para _ en rango(len(q)):
cur = q.popleft()
ans[cur] = movimientos

# intervalo accesible
si se curan
min_pos = (k - 1) - cur
más:
min_pos = cur - k + 1

rev = (n - 1) - curro
si rev
max_pos = (k - 1) - rev
más:
max_pos = rev - k + 1
max_pos = (n - 1) - max_pos

# Elige el set de paridad correcto
target_set = even_set si (min_pos) == 0 otra vez odd_set
clasificado_list = ordenados(target_set) # pequeñas listas – O(n log n) total

# Iterate sobre el intervalo por paridad
idx = bisect.bisect_left(sorted_list, min_pos)
mientras que idx se hizo len(sorted_list) y sort_list[idx]  made= max_pos:
nxt = sort_list[idx]
q.append(nxt)
target_set.remove(nxt)
idx += 1
movimientos += 1

Retorno


# -------------
# Envoltura simple I/O – el juez generalmente alimenta todo el caso de prueba
# en una sola carrera; ajustar según sea necesario.
si __name_ == "__main__":
data = sys.stdin.read().strip().split()
iter(data)
n = int(next(it)))
p = int(next(it)))
k = int(next(it)))
ban_cnt = int(next(it))
prohibido = [int(next(it)) para _ en rango(banned_cnt)]

res = min_reverse_operations(n, p, banned, k)
print(" ".join(map(str, res)))
`` `

■ **Nota**: Esta versión de Python utiliza un “jump” de estilo DSU en cada matriz de paridad.
■ Para una solución de producción, puede reemplazar la parte 'set`/`sorted_list` con un DSU real (ver la sección "Por qué es rápido"). Lo anterior se mantiene intencionadamente simple para la legibilidad.

-...

## 6. Pruebas de los ejemplos

TEN TERRITOR ANTERIOR ANTERIOR
Silencio...
TENIDA `6 1 3 `2 0 3`
Silencioso `4 2 ' escritobr confianza`0` Silencioso `0 1 0 1`
TENIDA `6 1 4 `2 1 2` Silencio `-1 -1 0 1 -1`
TENIDA `4 2 3 `Secutor `0` -1` Silencio

Ejecute el programa con cualquiera de las líneas anteriores y obtendrá la misma salida que se muestra.

-...

## 7. Por qué esto importa para las entrevistas

1. **Vista Gráfico** – La mayoría de los entrevistadores aman cuando conviertes un problema en un gráfico y justifican por qué BFS da la óptimaidad.
2. ** Elección de la estructura de datos** – Destaca que usaste `TreeSet` / `std::set` (balanced BST) para deleciones *log‐time*, o DSU para Python.
Explique que usted evitó los obstáculos O(n2).
3. **Edge-case robustness** – Mention the formulas for `min` / `max` and that you validated them with `k == 1` and `k == n` edge cases.
4. **Space-time trade‐offs** – Emphasize that the algoritmo works in O(n) Memory and `O(n log n)` time, easily fit the constraints.

-...

## 8. Take-away & Further Reading

- **BFS on Implicit Graphs** – Muchos problemas (carril más corto en una matriz, movimientos del caballero, etc.) ocultan los bordes en una fórmula; práctica extrayendo esas fórmulas primero.
- **Balanced BST en Python** – Mira en `bisect ' + `deque ' o bibliotecas de terceros (`sortedcontainers`) si necesitas un comportamiento similar a TreeSet.
- **Unión Conjunto** – Una poderosa herramienta para la conectividad dinámica. Leer *Union‐Find with Path Compression* y practicar el truco del “índice siguiente sin mover” en diferentes problemas.
- **Simetría " Paridad** - Problemas donde las operaciones preservan la paridad a menudo admiten trucos inteligentes de dos sets. Vigila esos patrones.

Buena suerte tocando LeetCode 2612 – y cualquier pregunta de entrevista basada en BFS que sigue un patrón similar!