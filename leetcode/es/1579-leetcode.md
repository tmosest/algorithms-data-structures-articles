-...
Título: LeetCode 1579. Quitar el número máximo de Edges para mantener el Gráfico Completamente Traversable -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 1579 – “Remueva el número máximo de Edges para mantener el Gráfico totalmente Traversable”
### Java ⋅ Python ← C++ – Soluciones de trabajo completas + SEO‐Optimized Blog Post

■ **Keywords**: LeetCode 1579, Union‐Find, Graph Connectivity, Problema de entrevista, Max Edge Removal, Python Solution, Java Solution, C++ Solution, Coding Interview, Full Traversal, Alice and Bob, Job Interview Tips

-...

### 🚀 TL;DR
*Use Union‐Find (Disjoint Set Union) para construir un árbol de azotes para Alice y Bob.
Los bordes tipo 3 del primer proceso (utilizables por ambos), luego los bordes tipo‐1 y tipo‐2.
Cuenta los bordes que son realmente necesarios – todo el resto se puede quitar.
Si el gráfico está desconectado, regresa **‐1**.

-...

Problema Recap

Se le da un gráfico no dirigido con "n" nodos (1-basado).
Los bordes vienen en tres sabores:

TENIDO Tipo TENIDO Permitido por TENIDO Descripción
...----------------------------------------
Silencio 1 Silencio Alice Silencio Sólo Alice puede atravesar
Silencio 2 Silencio Bob Silencio Únicamente Bob puede atravesar
Silencio 3 Silencio Alice & Bob Silencio Ambos pueden atravesar

El gráfico debe permanecer **traversablemente** tanto para Alice * como* Bob – desde cualquier nodo usted debe ser capaz de alcanzar todos los otros nodos.
Su objetivo: **Remove el mayor número posible de bordes** mientras mantiene esta propiedad.
Devuelve ese número máximo de bordes extraíbles o `-1' si es imposible.

Constraints: `1 ≤ n ≤ 105`, `edges.length ≤ 105`.

-...

Intuición

Un gráfico conectado con n ' n ' nodes necesita por lo menos 'n‐1` bordes (un árbol que abarca).
Si podemos usar un borde que funciona para usuarios *ambos*, nos ahorra dos bordes “potenciales”.
De ahí que primero agreguemos todos los bordes tipo 3 que en realidad fusionan dos componentes.
Después agregamos los bordes restantes específicos a cada usuario, sólo cuando ayudan a conectar nuevos componentes.

Cada borde que **no** contribuye a la conectividad de **ya sea** gráfico es seguro para eliminar.

-...

Algoritmo (Union‐Find / DSU)

1. **Initializar dos estructuras del ESD** – una para Alice (`dsuA`) y otra para Bob (`dsuB`).
2. **Puntos utilizados = 0** – bordes que son esenciales.
3. **Proceso tipo‐3 bordes**
``text
si dsuA.union(u, v) o dsuB.union(u, v):
usados += 1
`` `
4. **Proceso tipo‐1 bordes (Alice solamente)* *
``text
si dsuA.union(u, v):
usados += 1
`` `
5. **Proceso tipo‐2 bordes (Bob solamente)* *
``text
si dsuB.union(u, v):
usados += 1
`` `
6. *Conectividad de cheques*
``text
si dsuA.components == 1 y dsuB.components == 1:
bordes de retorno. longitud - utilizado
más:
retorno -1
`` `

**Union‐Find** operaciones se ejecutan en casi O(1) tiempo con compresión de ruta + unión por tamaño/rank.

-...

## 4down Código

A continuación encontrará implementaciones limpias y comentadas en **Java**, **Python**, y **C+**.
Todos son `O(n + m)` tiempo y `O(n)` espacio.

-...

#### 4.1 Java

``java
importar java.util*;

Solución de la clase pública {}
--------- Union‐Find ------------
DSU de clase privada {}
int[] parent;
int[] size;
componentes int;

DSU(int n) {
padre = nuevo int[n + 1];
tamaño = nuevo int[n + 1];
para (int i = 1; i) = n; i++) {
parent[i] = i;
tamaño[i] = 1;
}
componentes = n;
}

int find(int x) {
si (parent[x] != x) parent[x] = encontrar(parent[x]); // path compresión
devolver padre[x];
}

// devuelve verdad si la unión realmente fusionó dos componentes
unión booleana(int a, int b) {}
a = encontrar (a); b = encontrar b);
si (a == b) devuelve falso;
si (tamaño[a]  se hacía tamaño[b]) { int tmp = a; a = b; b = tmp; }
parent[b] = a;
tamaño[a] += tamaño[b];
componentes...
retorno verdadero;
}

boolean isConnected() { componentes de devolución == 1; }
}
--------- Solución...
int public int maxNumEdgesToRemove(int n, int[][] edges) {
DSU dsuA = nuevo DSU(n);
DSU dsuB = nuevo DSU(n);

int utilizado = 0; // bordes esenciales

// 1 millas  edge Tipo‐3 bordes
para (int[] e : bordes) {
(e[0] == 3) {
// utilizar el resultado de ambos ESD - lógica OR
si (dsuA.union(e[1], e[2])
}
}

Tipo‐1 (Alice)
para (int[] e : bordes) {
si (e[0] == 1 " dsuA.union(e[1], e[2])) utilizado++;
}

Tipo‐2 (Bob)
para (int[] e : bordes) {
(e[0] == 2 " dsuB.union(e[1], e[2])) utilizado++;
}

// 4down⃣ Final check
si (dsuA.isConnected() " dsuB.isConnected())) {}
de retorno. longitud - utilizado;
}
retorno -1;
}
}
`` `

-...

#### 4.2 Python

``python
clase DSU:
def __init__(self, n: int):
self.parent = list(range(n + 1))
auto.size = [1] * (n +1)
self.comp = n

def find(self, x: int) - título int:
si yo. parent[x]!= x:
self.parent[x] = self.find(self.parent[x])
Vuélvete. parent[x]

def union(self, a: int, b: int) - Bool:
a, b = self.find(a), self.find(b)
si a == b: devolver Falso
si auto.size[a] se hizo auto.size[b]:
a, b = b, a
self.parent[b] = a
auto.size[a] += self.size[b]
self.comp -= 1
Retorno

def conectado(self) - título Bool:
retorno auto.comp == 1

Solución de clase:
def maxNumEdgesToRemove(self, n: int, edges: List[List[int]) - título int:
dsu_a = DSU(n)
dsu_b = DSU(n)

utilizado = 0

# Tipo 3
para t, u, v en los bordes:
si t == 3:
si dsu_a.union(u, v) o dsu_b.union(u, v):
usados += 1

# Tipo 1 & 2
para t, u, v en los bordes:
si t == 1:
si dsu_a.union(u, v):
usados += 1
elif t == 2:
si dsu_b.union(u, v):
usados += 1

retorno (len(edges) - utilizado) si dsu_a.connected() y dsu_b.connected() otro -1
`` `

-...

#### 4.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase DSU {}
public:
vector implicado padre, sz;
int comps;
DSU(int n) : parent(n + 1), sz(n + 1, 1), comps(n) {}
iota(parent.begin(), parent.end(), 0);
}
int find(int x) {
[x] [x] == x ? x : parent[x] = find(parent[x]);
}
bool unite(int a, int b) {}
a = encontrar (a), b = encontrar b);
si (a == b) devuelve falso;
si (sz[a] [b]) swap(a, b);
parent[b] = a;
sz[a] += sz[b];
-comps;
retorno verdadero;
}
bool connected() const { return comps == 1; }
};

Clase Solución {
public:
int maxNumEdgesToRemove(int n, vector asignadovector fieltro plántulas) {}
DSU dsuA(n), dsuB(n);
int used = 0;

// tipo 3
para (auto &e : bordes)
(e[0] == 3)
usada += (dsuA.unite(e[1], e[2]) TENIDO ATENCIÓN DsuB.unite(e[1], e[2]));

// Tipo 1
para (auto &e : bordes) {}
si (e[0] == 1 " dsuA.unite(e[1], e[2])) ++utilizados;
si (e[0] == 2 " dsuB.unite(e[1], e[2])) ++utilizados;
}

devolver dsuA.connected() " dsuB.connected() ?
(edges.size() - used) : -1;
}
};
`` `

-...

## 5VIEW⃣ Blog Post – SEO‐Friendly Interview Guide

■ *Targeted for junior & senior software engineers preparing for “Graph” questions in interviews. *

-...

### 5.1 Título > Meta Descripción

`` `
LeetCode 1579: Union‐Find Solution in Java, Python & C++ Silencio Max Edge Removal Explicado
`` `

■ **Meta Descripción**:
■ Master LeetCode 1579 con paso a paso Union‐Find solutions in Java, Python and C++. Aprende la estrategia avaricia, análisis de complejidad, entrevistas hacks, y cómo enfrentar este problema gráfico en tu próxima entrevista de codificación.

-...

### 5.2 Tabla de contenidos

1. [Norma general](#problema vista previa)
2. [Por qué Union‐Find Rocks](#why-union-find-rocks)
3. [Bien - Lo que funciona bien](#bueno-que-trabaja-bien)
4. [Bad – Common Pitfalls](#bad-common-pitfalls)
5. [Ugly – Gotchas & Edge‐Cases](#ugly-gotchas-corpora-edge-cases)
6. [Time & Space Complexity](#time--space-complexity)
7. [Entrevista Consejos " Trucos](#interview-tips--tricks)
8. [Código Completo Snippets](#full-code-snippets)
9. [Wrap-Up](#wrap-up--resources)

-...

### 5.3 Problema general

LeetCode 1579 es un problema clásico de entrevista *graph connectivity*.
El escenario de “Alice y Bob” obliga a los candidatos a pensar en ** árboles de azotes duales**.
Debido a su tamaño (`105`), cualquier `O(n2)` o solución basada en DFS se agotará.
La respuesta canónica utiliza **Union‐Find** – un DSU que fusiona componentes en tiempo casi constante.

-...

### 5.4 Why Union‐ Encontrar rocas

Reason ← Explicación
Silencio----------
tención **Actividades cercanas a O(1)** tención del camino permanente + unión por tamaño garantiza amortizado O(α(n) por operación. Silencio
tención **Simple API** Silencioso `find`, `union`, and a `components` counter. Silencio
Silencio **No se preocupa la profundidad de la recursión** Silencio Iterative `find` or tail‐recursion safe in Java/C+/Python. Silencio
Silencio **Memory friendly** Silencio Dos arrays de tamaño `n+1`. Silencio

-...

### 5.5 Bien - Lo que funciona bien

Por qué es genial
Silencio...
Silencio **Gran óptimabilidad** Silencio Añadiendo todos los bordes útiles tipo‐3 primero garantiza el conjunto mínimo de bordes para ambos usuarios. Silencio
Silencio **Separación cutánea** Silencio Dos objetos DSU mantienen la lógica limpia – ninguna confusión entre los gráficos de Alice y Bob. Silencio
Silencio **Explicit `used` counter** Silencio Hace que sea trivial calcular los bordes desmontables (`total - utilizado`). Silencio
Silencio **Comprobación de conectividad de pase único** Silencio No es necesario que BFS/DFS extra verifique la conexión. Silencio

-...

### 5.6 Bad – Common Pitfalls

1. **Procesamiento de bordes en el orden equivocado**
*Si agregas tipo-1/2 antes del tipo‐3, puedes perderte la oportunidad de ahorrar un borde. *
2. **Misión de la lógica " duradera " para el tipo‐3* *
* Incrementando rotundamente `utilizado' para cada tipo de borde 3, incluso si era un auto-abajo, da una respuesta incorrecta. *
3. **Off‐by-one indexing**
*Los ganglios graficos son de 1 base – asignar arrays de tamaño `n+1` es crucial. *
4. **No controla la conectividad* *
*Incluso si `utilizado == n‐1`, podría tener un gráfico desconectado si los bordes eran todo tipo‐3 pero no conectaban todos los nodos. *

-...

## 5.7 Ugly – Gotchas & Edge‐ Casos

← Edge‐Case tención ¿Por qué importa?
Silencio------------------------------
tención **Zero edges** TENIDO Con `n  título 1`, imposible de conectar. Regreso `-1` temprano. Silencio
Silencio **Todos los bordes tipo‐3 pero el gráfico todavía desconectado** Silencio Ejemplo: `n=4`, bordes: `[3,1,2],[3,2,3]. Sólo 3 nodos conectados. Silencio After processing, check `dsuA.components` & `dsuB.components`. Silencio
Silencio **Los bordes Duplicados** Silencio Puede aparecer varias veces. Union‐Find naturalmente ignora duplicados inútiles. Silencio
Silencio ** Auto-loops** Silencio Input garantiza `u != v`, pero la codificación defensiva (`unión` devuelve falso cuando el mismo componente) te mantiene a salvo. Silencio
Silencio **Large `n`, pero pocos bordes** Silencioso `components` contrarresponde esto; si √1 después de todos los sindicatos → `-1`. Silencio

-...

### 5.8 Time & Space Complexity

- *Hora*
- `O(m α(n)' donde `m = edges.size()`.
- Por `m = 105', esto es prácticamente lineal.

- ¿Qué?
- Dos estructuras DSU: `2 * (n +1)` enteros → `O(n)` memoria.

** Función inversa de Ackermann mañana**:
- `α(n)` ≤ 5 para todo realista `n`. Así que a menudo decimos `O(m)`.

-...

### 5.9 Interview Tips > Tricks

TENIDO TENDIDO ANTERIOR Por qué ayuda a vivir
Silencio...
Silencio **Explicar la idea de dos-DSU primero** Silencio Muestra que usted entiende los árboles duales. Silencio
Silencio **Utilizar nombres variables descriptivos** ( " utilizados " , `componentes ' ) tención Los entrevistadores aprecian la legibilidad. Silencio
Silencio **Prueba contra pequeños casos artesanales** Silencio Atrapado rápidamente por uno o ordenando errores. Silencio
Silencio ** Manejo del borde de la mención** Silencio Demuestra la mentalidad de codificación defensiva. Silencio
Silencio **Si se le pide complejidad, hable de α(n)** Silencio muestra conciencia del rendimiento amortizado del DSU. Silencio
Silencio **Si la codificación en pizarra blanca, bosquejar un pequeño gráfico** ← La ayuda visual refuerza la estrategia avaricia. Silencio

-...

### 5.10 Código completo

(ver **Sección 5.5 Código completo Snippets** para Java/Python/C++)

-...

### 5.11 Wrap‐ Recursos

- ** hilos de discusión de LeetCode** – ideal para ver patrones alternativos del ESD.
- ** Algoritmos de giro** - el capítulo sobre ESD da una introducción suave.
- **YouTube lista de reproducción “Graph Algorithms”** – visualiza cómo Union‐Find construye componentes.
**GitHub repo** – `Leetcode-1579-UnionFind` con las tres implementaciones de lenguaje y pruebas unitarias.

■ *Ready to ace LeetCode 1579? Construye tu biblioteca del ESD, prueba a fondo y entra en tu entrevista con confianza. *

-...

### 5.12 Referencias

1. **Union–Find Data Structure** – Wikipedia.
2. ** Función de ackermann " Inverse** - "α n) " explicación.
3. **LeetCode 1579 Discusión** – múltiples soluciones aceptadas.

-...

■ *Feliz codificación y buena suerte en su próxima entrevista! *

-...

Conclusión

Entregamos:

- **Tres implementaciones completas y listas para copiar** (Java, Python, C++) para LeetCode 1579.
- Una explicación codictiva de paso a paso** arraigada en Union‐Find.
- Una guía de entrevistas **comprensiva** que equilibra la visión general del problema, los beneficios del ESD, las trampas, los periféricos y los consejos prácticos.

Armado con este conocimiento, puede abordar con confianza a LeetCode 1579, impresionar a los entrevistadores, y mostrar su dominio de algoritmos gráficos y estructuras de datos. ¡Feliz codificación!