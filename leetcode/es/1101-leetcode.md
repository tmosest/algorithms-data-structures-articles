-...
Título: LeetCode 1101. El Momento más temprano cuando todos se vuelven amigos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## El Momento más temprano cuando todos se vuelven amigos – 1101 (LeetCode)

Silencio Silencio Silencio Silencio Silencio Silencio Silencio
Silencio-------------------------------Prince--
Silencio **Java** Silencio O(m log m) Silencio O(n+m) ✔
Silencio **Python** Silencio O(m log m) Silencio O(n+m)  ✔
Silencio **C+** Silencio O(m log m) Silencio O(n+m) ✔ Silencio

■ **Key Insight** – Use **Union‐Find (Disjoint‐Set Union)** para fusionar grupos de amistad en orden cronológico.
■ Cuando el tamaño del grupo que contiene cualquier miembro equivale a *n*, todo el mundo está conectado.

■ **¿Por qué Union‐Find?**
* Frenos rápidos (`α(n)` tiempo)
* Fácil de mantener la cuenta de componentes conectados
• Perfecto para “cuando toda la red se conectó” preguntas tipo

-...

Declaración de problemas

■ Hay **n** personas etiquetadas `0 ... n‐1`.
“logs[i] = [timestampi, xi, yi]” significa que en el momento `timestampi`, la gente `xi` y `yi` se vuelven amigos.
■ La amistad es transitiva, si `a` es un amigo de `b`, y `b` es un amigo de `c`, entonces `a` se conoce con `c`.
■ **Regresar el horario más temprano en el que cada persona se conoce con cada otra persona. #
■ Si eso nunca sucede, devuelve `-1`.

■ **Constraints**
* `2 ≤ n ≤ 100`
≤ 104 `
* Todos los `timestampi` son únicos y `0 ≤ vecestampi ≤ 109 `
* Cada par `(xi, yi)` aparece a la vez

-...

## ⚙ف Algorithm – Union‐Find (Disjoint Set Union)

1. **Ordenar los registros por timetamp** – necesitamos procesar las amistades cronológicamente.
2. **Initializar un ESD** con nodos.
* `parent[i] = i `
* " tamaño[i] = 1 " (número de nodos en el componente)
3. **Proceso de cada registro** en orden ordenado:
* Union the two people `x` and `y`.
* Después de una unión exitosa (es decir, estaban anteriormente en diferentes componentes), comprobar si el tamaño del nuevo componente es igual a `n`.
* Si es así, devuelva el `timestamp` actual.
4. Si el bucle termina sin alcanzar un tamaño de `n`, regrese `-1`.

-...

### Pseudocode

`` `
(logs by timestamp)
init DSU(n)
para cada [t, x, y] en troncos:
si unión(x, y):
si componenteSize(x) == n:
t
retorno -1
`` `

-...

## 📈 Complexity Analysis

Silencio Silencio Silencio Silencio
Silencio----------------
* * * *(m log m)** (`m = logs.length`) Silencio O(m)
tención Unión‐Encuentra operaciones Silencioso **O(m α(n)** (α es inverso Ackermann, prácticamente constante)
Silencio total **O(m log m)** Silencio **O(n+m)**

Con 'n ≤ 100' y `m ≤ 104`, esto funciona en unos pocos milisegundos.

-...

## ♥ Edge Cases " Pitfalls

Silencio Silencio
Silencio...
¿Amistías Duplicadas? Problema de la vida garantiza pares únicos. Silencio
Silencio ¿Ya está conectado par? Silencio `union` devuelve `false`; ningún cambio de tamaño. Silencio
Silencio ¿Todas las personas ya conectadas antes de cualquier registro? Silencio No es posible porque no hay amistades inicialmente. Silencio
Silencio ¿Tiempos muy grandes? Silencio

-...

Código – Java (Union‐Find)

``java
importa java.util. Arrays;

Clase Solución {
--------- DSU...
DSU de clase privada {}
int[] parent;
int[] size;
DSU(int n) {
padre = nuevo int[n];
tamaño = nuevo int[n];
para (int i = 0; i)
parent[i] = i;
tamaño[i] = 1;
}
}
int find(int x) {
si (parent[x] != x) parent[x] = encontrar(parent[x]); // path compresión
devolver padre[x];
}
// devuelve la verdad si la fusión sucedió
unión booleana(int a, int b) {}
int pa = find(a), pb = find(b);
si (pa == pb) devuelve falso;
// unión por tamaño
si (tamaño[pa] {}
int tmp = pa; pa = pb; pb = tmp;
}
parent[pb] = pa;
tamaño[pa] += tamaño[pb];
retorno verdadero;
}
int compSize(int x) { return size[find(x)]; }
}
--------- solución...
public int earlyAcq(int[][] logs, int n) {
// 1 / / / 1 / / / ⃣ ordenar por el temporizador
Arrays.sort(logs, (a, b) - título Integer.compare(a[0], b[0]));
DSU dsu = nuevo DSU(n);
para (int[] log : logs) {}
int t = log[0], x = log[1], y = log[2];
si (dsu.union(x, y) " dsu.compSize(x) == n) {
t; // todo el mundo conectado
}
}
retorno -1; // nunca totalmente conectado
}
}
`` `

-...

## 🐍 Code – Python (Union‐Find)

``python
de la importación Lista

clase DSU:
def __init__(self, n: int):
self.parent = list(range(n))
auto.size = [1]

def find(self, x: int) - título int:
si yo. parent[x]!= x:
self.parent[x] = self.find(self.parent[x]) # path compresión
Vuélvete. parent[x]

def union(self, a: int, b: int) - Bool:
pa, pb = self.find(a), self.find(b)
si pa == pb:
Retorno Falso
si auto.size[pa] se hizo auto.size[pb]: # Unión por tamaño
pa, pb = pb, pa
self.parent[pb] = pa
auto.size[pa] += self.size[pb]
Retorno

def comp_size(self, x: int) - título int:
volver auto.size[self.find(x)]

Solución de clase:
antes Acq(self, logs: List[List[int], n: int) - título int:
logs.sort(key=lambda x: x[0]) # 1ר⃣ chronological order
dsu = DSU(n)
para t, x, y en troncos:
si dsu.union(x, y) y dsu.comp_size(x) == n:
t
retorno -1
`` `

-...

Código C++ (Union‐Find)

``cpp
Incluido el título
#include >

Clase DSU {}
public:
DSU(int n) : parent(n), sz(n, 1) {
para (int i = 0; i)
}
int find(int x) {
si (parent[x] != x) parent[x] = encontrar(parent[x]); // path compresión
devolver padre[x];
}
bool unite(int a, int b) {}
int pa = find(a), pb = find(b);
si (pa == pb) devolver falso; // ya conectado
si (sz[pa] ecto sz[pb]) std::swap(pa, pb); // unión por tamaño
parent[pb] = pa;
sz[pa] += sz[pb];
retorno verdadero;
}
int compSize(int x) const { return sz[find(x)]; }

privado:
std::vector obtenidosint titulada parent, sz;
};

Clase Solución {
public:
lo antes posible Acq(std:::vector seleccionados:::vector fielint logs, int n) {
std::sort(logs.begin(), logs.end(),
[](const std::vector fieltro a,
const std::vector fieltro b) {
devolver a [0]
}); // 1ICK⃣ ordenar por timetamp
DSU dsu(n);
para (continuo auto cho e : logs) {
int t = e[0], x = e[1], y = e[2];
si (dsu.unite(x, y) " dsu.compSize(x) == n)
t; // todos conectados
}
retorno -1; // nunca totalmente conectado
}
};
`` `

-...

## 🔀 Alternative – Depth‐First Search (DFS)

Si prefieres un enfoque más “fuerza bruta”:

1. **Construye una lista de adyacencia** de los registros mientras vas.
2. Después de cada sindicato, **corre un DFS** de cualquier miembro para contar cuántos nodos son alcanzables.
3. Cuando ese número es igual a `n`, devuelve el timetamp.

■ **¿Por qué no usar DFS? #
* Más fácil de entender para principiantes
* Complejidad del tiempo: O(m·n) en el peor de los casos - todavía bien para las limitaciones dadas
* La versión DSU es más limpia para entrevistadores y escalas a mayor `n`

-...

## 🎤 Interview Talk‐Point

- **Explicar la “transitividad”** temprano – muchos candidatos lo olvidan.
- *Mostrar el ayudante del ESD* claramente: `encontrar ' , `unir ' , ` tamaño ' .
- ** Clasificación de la mención** - un gotcha común que hace la solución O(m log m) en lugar de O(m).
- **Hablar sobre la compresión del camino y la unión por tamaño** – los entrevistadores aprecian el matiz.
- ** Explique por qué regresas después de una unión exitosa** – no todos los "unión" cambian el tamaño del componente.

■ **STAR Tip** – “*Mientras grupos de amistad fusionados, usé Union‐Find para que cada sindicato tome tiempo casi constante. Tan pronto como el tamaño del componente llega n, sé que todos están conectados. Clasifiqué los registros por timetamp para mantener el invariante cronológico.*”

-...

## 🚀 Job‐Entreview Takeaway

1. **DSU es una bala mágica** para problemas de “conectividad con el tiempo”.
2. **Mantenga el tamaño del componente** dentro del ESD; de lo contrario necesitaría un contador separado.
3. **Evite O(n2) DFS después de cada registro** – el DSU es órdenes de magnitud más rápido.
4. **Mostrar código limpio** – nombres variables como `parente`, `size`, `union`/`unite`, `find`.
5. ** Manejo del borde de la mención** (pares duplicados, par ya conectado) – demuestra robustez.

■ **Si se logra este problema, se creará el segmento de “conectividad gráfica” en casi cualquier entrevista de diseño de sistemas o instrucciones de datos.** 🎯

-...

## ⋅ Final Thought

■ El problema “momento más temprano que todos se convierten en amigos” es una pregunta de libro de texto Union‐Find.
■ Maestro el patrón DSU y estarás listo para cualquier entrevista que pregunte *“¿cuándo se conectó este gráfico?”*
■ ¿Y la mejor parte? La solución es sólo unas pocas líneas de código – perfecto para su cartera de LeetCode y su próximo trabajo-hunt! 🚀

¡Feliz codificación, y buena suerte aterrizando ese papel de tecnología de sueños!