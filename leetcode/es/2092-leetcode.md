-...
Título: LeetCode 2092. Encontrar a todas las personas con secreto -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 2092 – Find All People With Secret
## Solution in **Java**, **Python**, y **C+** (Union‐Find + Batching de tiempo)
-...

#### TL;DR
El secreto se extiende sólo ** en la hora exacta de una reunión**.
Si varias reuniones suceden al mismo tiempo, todos los que ya tienen el secreto pueden transmitirlo instantáneamente a ** todos los participantes** de ese *time-batch*.
El problema se puede resolver en **O(n + m log m)** tiempo y **O(n + m)** memoria por:

1. **Sorting** reuniones a tiempo.
2. **Procesamiento** cada una de las sesiones juntas utilizando un **Union‐Find Union (DSU)** (Union‐Find).
3. Al final, todos los nodos cuyo representante es `0` (persona 0) conocen el secreto.

El ESD se reinicia después de cada lote para que las personas que hicieron **no** reciban el secreto durante ese tiempo sean aisladas de nuevo.

-...

## 1down Java Implementation

``java
importar java.util*;

Solución de la clase pública {}
// -------- Disjoint Set Union...--------
DSU de clase privada {}
int[] parent, rank;
DSU(int n) {
padre = nuevo int[n];
rango = nuevo int[n];
para (int i = 0; i)
}
int find(int x) {
(parent[x] != x) parent[x] = find(parent[x]);
devolver padre[x];
}
unión de vacío(int a, int b) {}
int pa = find(a), pb = find(b);
si (pa == pb) regresa;
[pa] = pb;
[pb] = pa;
[pb] = pa; rank[pa]++; }
}
}

public List (0)Integer confianza findAllPeople(int n, int[] meetings, int firstPerson) {}
Clasificar por el tiempo
Arrays.sort(meetings, Comparator.comparingInt(a - título a[2]));

DSU dsu = nuevo DSU(n);
dsu.union(0, firstPerson); // persona 0 da el secreto a la vez 0

int i = 0, m = meetings.length;
mientras (i
int curTime = meetings[i][2];
// mantener a todos los participantes de esta sesión de tiempo
Lista de los participantes del título = nuevo ArrayList implicado();

// 2️ Unión todos los que se reúnen en este momento
mientras (i י m ' reuniones[i][2] == curTime) {
int a = meetings[i][0];
int b = meetings[i][1];
dsu.union(a, b);
a);
a) Participantes.add b);
i++;
}

// 3️ Reset DSU para personas que no recibieron el secreto
para (int p : participantes) {}
si (dsu.find(p) != dsu.find(0)
dsu.parent[p] = p; // isolated again
}
}

// 4down Recoger a todos los que están conectados a 0
Lista de datos:Integer confianza res = nuevo ArrayList correctamente();
para (int i1 = 0; i1 = n; i1++)
si (dsu.find(i1) == dsu.find(0))) res.add(i1);

restitución;
}
}
`` `

**La complejidad* *
- `O(n + m) log m) ' time (sorting dominates)
- `O(n + m)` memoria (DSU + matriz de reuniones)

-...

## 2down⃣ Python Implementation

``python
de las colecciones importadas por defecto
importadores
sys.setrecursionlimit(1

clase DSU:
def __init__(self, n):
self.par = list(range(n))
* n

def find(self, x):
si auto.par[x]!= x:
self.par[x] = self.find(self.par[x])
volver a sí mismo.par[x]

def union(self, a, b):
pa, pb = self.find(a), self.find(b)
si pa == pb: retorno
si auto.rnk[pa] se auto.rnk[pb]:
self.par[pa] = pb
elif self.rnk[pb] se hizo auto.rnk[pa]:
self.par[pb] = pa
más:
self.par[pb] = pa
self.rnk[pa] += 1

def findAllPeople(n: int, meetings: list[list[int], firstPerson: int) - ratio[int]:
meetings.sort(key=lambda x: x[2]) # sort by time
dsu = DSU(n)
dsu.union(0, firstPerson) # transferencia secreta inicial

I = 0
mientras que yo hice el len(meetings):
cur_time = reuniones[i ][2]
participantes

# sindicato de todas las reuniones que suceden al mismo tiempo
mientras que yo hice la mención y las reuniones [i][2] == cur_time:
a, b, _ = reuniones[i]
dsu.union(a, b)
participantes.extend([a, b])
i += 1

# resetea los nodos que no recibieron el secreto durante este lote
para p en participantes:
si dsu.find(p) != dsu.find(0):
dsu.par[p] = p

retorno [i para i en el rango(n) si dsu.find(i) == dsu.find(0)]

# --------------------------------------------------
# Uso de ejemplo (descomunal para probar)
# N = 6
# meetings = [[1,2,5],[2,3,8],[1,5,10]]
# print(findAllPeople(n, meetings,1)) # - título [0, 1, 2, 3, 5]
`` `

**La complejidad** – idéntica a la solución Java.

-...

## 3down C C++ Aplicación

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase DSU {}
public:
DSU(int n): parent(n), rank(n), 0) {
iota(parent.begin(), parent.end(), 0);
}
int find(int x) {
volver padre[x]=x ? x : parent[x]=find(parent[x]);
}
vacío unite (incluido a, int b) {}
int pa=find(a), pb=find(b);
si (pa==pb) regresa;
[pa]=pb) padre [pa]=pb;
[pb]=pa;
[pb]=pa; rank[pa]++; }
}
privado:
vector:
};

Clase Solución {
public:
vector asignadoint círculo encontrarTodas las personas(int n, vector asignadovector identificadointющ reuniones, int firstPerson) {}
sort(meetings.begin(), meetings.end(),
[](cont auto ' , const auto &b){ devolver a [2]  obtenidos b[2]; });

DSU dsu(n);
dsu.unite(0, firstPerson); // secret starts at person 0

int i = 0;
mientras(i) {}
int cur = meetings[i][2];
vector implicado; // participantes en este tiempo-batch

mientras(i) se hacía (int)meetings.size() " reuniones individuales[i][2] == cur) {
int a = meetings[i][0];
int b = meetings[i][1];
dsu.unite(a, b);
part.push_back(a);
part.push_back(b);
++i;
}

para(int p : part) // reajustar a los que no recibieron secretos
if(dsu.find(p) != dsu.find(0)
dsu.unite(p, p); // set parent to itself
}

vector significar uns
para (int j=0;j obtenidos;+j)
if(dsu.find(j) == dsu.find(0))
ans.push_back(j);
devolver los ans;
}
};
`` `

. **Tip**: En C++ se puede saltar el paso "reset" usando un *stack* de nodos que cambian a los padres durante un lote, pero lo anterior es más fácil de leer.

-...

## 📚 Blog Article – “The Secret Spread: A Deep Dive into LeetCode 2092”

### Title
**“El mensaje secreto: 2092 – De BFS a Union‐Find – El bueno, el malo, el ugly”* *

## Meta Descripción
Aprende cómo romper LeetCode 2092 en tiempo O(n+m log m). Lea la profunda inmersión en estrategias BFS, DSU y de reducción de tiempo. Perfecto para la preparación de entrevistas, entrevistas de codificación y ingenieros de búsqueda de empleo.

-...

#### Introduction

■ **Recapto de problemas* *
■ Se les da `n` personas, una lista de reuniones `(x, y, tiempo)`, y una `primera persona`. Persona `0` tiene un secreto a la vez `0` y lo pasa a 'primera persona'. Cada vez que se celebra una reunión, cualquiera que ya sepa el secreto lo comparte instantáneamente con el otro asistente.
■ ** Objetivo** – devolver a todas las personas que conocen el secreto después de todas las reuniones.

■ *Por qué importa* –
■ 1. **Concurrencia** – múltiples reuniones al mismo tiempo.
■ 2. **La propagación del gráfico** – un problema clásico de “reachabilidad”, pero con un giro: la propagación ocurre *sólo* en determinados momentos.
■ 3. **Interview challenge** – requiere un pensamiento cuidadoso sobre *cuando* puedes difundir el secreto, no sólo *quien* puede.

-...

### The Naïve View: Breadth‐First Search (BFS)

Un primer instinto es tratar cada reunión como un borde en un gráfico y ejecutar un BFS de la fuente `(0, primera persona)`.

``text
tiempo 0: 0 - Propiedad first Persona
t: BFS de todos los que conocen el secreto en este momento
`` `

**Problema** – BFS asume un gráfico *estático*. En nuestro problema, los bordes sólo llegan a ser relevantes ** una vez** en el tiempo de reunión, y pueden ser "apagados" si el secreto nunca llegó a ese borde. Ejecutar BFS una vez por cada sello de tiempo llevaría a un algoritmo **O(n · m)** – demasiado lento para las restricciones (`m` up to `2·105`).

-...

### The Good – Union‐Find + Time‐Batching

#### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## #

Ordenar todas las reuniones por `tiempo`. Todas las reuniones que comparten el mismo tiempo forman un *batch*.

##### 2downSU DSU within a Batch

Durante un lote, si **cualquier participante** conoce el secreto, el secreto se propaga a **todo** componente conectado de ese lote instantáneamente.
Union‐Find nos permite *merge* todos los participantes de un lote en tiempo amortizado casi constante.

##### 3down⃣ Reiniciar Después del Batch

Después de procesar el lote, debemos aislar a los que hicieron **no** el secreto.
En código esto parece:

``pseudo
para cada participante p en este lote:
si encuentra(p) != find(0):
parent[p] = p // resetear a sí mismo
`` `

Este truco garantiza que la próxima vez-batch comienza de cero para todos los que no recibieron el secreto.

-...

### El malo - ¿Por qué BFS es un final muerto

TENIDO TENIDO Complejidad ANTERIOR Por qué Fails ANTE
Silencio--------------------------
Silencio Puro BFS Silencio `O(n · m)` Silencio Demasiado lento cuando `m` es enorme. Silencio
Silencio BFS + Sorting Silencio `O(m log m + n)` Silencio Todavía `O(n·m)` porque necesitamos recomputar la posibilidad de llegar desde cero para cada vez más. Silencio

En resumen, BFS ignora la dimensión *time* y por lo tanto no puede manejar las reuniones simultáneas de manera eficiente.

-...

### The Ugly – Edge Cases that Break Simple Code

El caso Edge tóxico tóxico Problema
Silencio-----------------------Prince--
tención **Reunión de padres con el mismo par en diferentes momentos** Silencio DSU puede recordar incorrectamente los sindicatos pasados. Silencio
tención **Tamaño de entrada alto** ← Profundidad de la recuperación en los desbordamientos de DSU en Java/Python. Use compresión de ruta y bucles iterativos o levante límites de recursión. Silencio
Silencio **Multiple visits to the same person in one batch** Silencio Añadir el mismo participante dos veces puede inflar la lista de los participantes innecesariamente. ← Mantener un `std::unordered_set interpretadoint `` (o `HashSet`) por lote para almacenar nodos únicos. Silencio

-...

### Complexity Breakdown

Silencio Silencio Silencio Silencio Silencio Silencio
Silencio--------------------
Silencio Clasificar reuniones Silencio `m log m` Silencio Dominant Silencio
Silenciosas operaciones de la DAA TENIDO `α(n)` amortizado por unión ANTE `O(n + m)` Silencio
Silencioso Reiniciar los bucles Silencio en la mayoría de `2 · m` por lote Silencioso `O(n + m)`
Silencio Final scan Silencio `n` finds Silencio `O(n)` Silencio

■ Resultado** – `O(n+m) log m)` tiempo, `O(n+m)` espacio.

-...

### Consejos para entrevistas

1. **Explicar la idea de tiempo-batch primero.** Los entrevistadores les encanta ver que entendieron por qué “las reuniones simultáneas” son especiales.
2. **Mostrar el truco de reajuste del ESD** – es el * huevo este* que convierte una solución ingenua del ESD en el óptimo.
3. **Alternativas de mención** (BFS con una cola de eventos atemporales, o un gráfico por timetamp). Esto demuestra que usted es consciente del paisaje.
4. **Discusa la optimización del espacio** – por ejemplo, reutilizando el vector de reuniones, o usando un vector de “nodos cambiados” en lugar de reiniciar toda la matriz de padres.
5. **Práctica sobre problemas similares** – por ejemplo, *BFS con limitaciones*, *Union‐Find with time windows*.

-...

### Conclusión

LeetCode 2092 te enseña a mezclar dos conceptos clásicos:

- **BFS** (reachability)
- **Union‐Find** (compuestos conectados)

...y combinarlos con un truco de reducción de tiempo ** que respeta las reglas de coincidencia del problema.
Dominar este patrón le dará confianza para las preguntas sobre *redes temporales*, *propulsión impulsada por elevento*, y *conectividad dinamica* en entrevistas técnicas.

-...

### Referencias > Lectura posterior

- [Union‐Find (DSU) – Wikipedia](https://en.wikipedia.org/wiki/Disjoint-set_data_structure)
- [BFS on graphs – LeetCode](https://leetcode.com/problems/breadth-firstsearch/)
- [Problemas de gráficos basados en el tiempo - Codeforces EDU](https://codeforces.com/blog/entry/11978)

¡Feliz codificación! 🚀