-...
Título: LeetCode 2368. Nodos alcanzables con restricciones -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🚀 **LeetCode 2368 – Nodos alcanzables con restricciones**
■ *Un profundo dinamismo en una pregunta de entrevista a los árboles – Java, Python & C++++ + una publicación de blog optimizada SEO para ayudarte a aterrizar ese trabajo de ingeniería de software. *

-...

## 1. Recaptación de problemas

■ **Given** un árbol con nodos (`0 ... n-1`) y `n-1` bordes no redirigidos, y una lista de * nodos restringidos*.
■ **Retorno** el número máximo de nodos que puede alcanzar a partir del nodo `0` sin pisar un nodo restringido.

■ **Constraints**
≤ 105
Ø - `edges` forman un árbol válido
" Restricted " length " , all unique, none equals `0`

-...

## 2. Idea de solución de alto nivel

Simplemente necesitamos realizar un **graph traversal** (DFS o BFS) a partir del nodo `0`.
Durante el traversal nosotros:

1. **Ignorar** cualquier nodo que aparezca en el conjunto `restricted`.
2. **Count** cada nodo visitado que es *no* restringido.
3. Utilice una lista de adyacency para mantener el uso de la memoria lineal.

Tanto el DFS como el BFS dan el mismo tiempo lineal `O(n)` y espacio lineal `O(n)`.

-...

## 3. Aplicación de Java

``java
importar java.util*;

Solución de la clase pública {}

// Breadth‐First Search
public int reachableNodesBFS(int n, int[] edges, int[] restricted) {}
Establecer:Integer prohíbe = nuevo HashSet correctamente();
para (int r : restricted) prohibir.add(r);

Lista realizadaLista realizadaInteger confianza adj = buildAdj(n, edges);

boolean[] vis = new boolean[n];
Búsquedas realizadasInteger título q = nuevo ArrayDeque corresponde();
q.add(0);

int count = 0;
(!q.isEmpty()) {
int cur = q.poll();
si (vis[cur] TENIDO ANTERIEND.contains(cur))) continúan;

vis[cur] = verdadero;
contar++;

para (int nxt : adj.get(cur) {
si (!vis[nxt] " ven !forbid.contains(nxt))) q.add(nxt);
}
}
recuento de retorno;
}

// Depth‐First Search (recursive)
public int reachableNodesDFS(int n, int[] edges, int[] restricted) {}
Establecer:Integer prohíbe = nuevo HashSet correctamente();
para (int r : restricted) prohibir.add(r);

Lista realizadaLista realizadaInteger confianza adj = buildAdj(n, edges);
boolean[] vis = new boolean[n];
dfs(0, adj, forbid, vis);
}

int privado dfs(int node, Lista hecha:
Conjunto indicadoInteger título prohibir, boolean[] vis) {
si (vis[nodo] tención eterna prohíbe.contains(node)) devuelve 0;
vis[nodo] = verdadero;
int cnt = 1;
para (int nxt : adj.get(node)) cnt += dfs(nxt, adj, forbid, vis);
cnt de retorno;
}

Lista privada realizadaLista realizadaInteger confianza buildAdj(int n, int[] edges) {
Lista realizadaLista realizadaInteger confianza adj = nuevo ArrayList recomendado(n);
para (int i = 0; i < n; i++) adj.add(new ArrayList correctamente());
para (int[] e : bordes) {
adj.get(e[0]).add(e[1]);
adj.get(e[1]).add(e[0]);
}
devolver adj;
}
}
`` `

■ **Por qué esto es eficiente* *
- `buildAdj` se ejecuta en `O(n)` tiempo.
≤ - BFS/DFS visita cada nodo y borde a la vez → `O(n)` tiempo, `O(n)` memoria.

-...

## 4. Aplicación de los pitones

``python
de las colecciones importan defaultdict, deque
de la importación Lista, Conjunto

Solución de clase:
def alcanzableNodos(self, n: int, edges: List[List[int], restricted: List[int]) - título int:
prohibir: Set[int] = set(restricted)

# Lista de adjacency
adj = defaultdict(list)
para a, b en los bordes:
adj[a].append(b)
adj[b].append(a)

vis = [False] * n
q = deque([0])
Conteo = 0

mientras q:
cur = q.popleft()
si vis[cur] o se curan en prohibir:
continuar
vis[cur] = Verdadero
Cuenta += 1
para nxt en adj[cur]:
si no vis[nxt] y no se prohíben:
q.append(nxt)

cuenta de retorno
`` `

■ # Consejos pitónicos #
√≥ - `defaultdict(list)` salva el bucle de construcción de gráficos explícito.
- Uso `deque ' para operaciones pop-left O(1).

-...

## 5. Aplicación C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int reachableNodos(int n, vector identificadovector seleccionador seleccionados) {
unordered_set Utilizado(restricted.begin(), restricted.end());
vector realizador realizado en el título adj(n);
para (auto &e : bordes) {}
adj[e[0].push_back(e[1]);
adj[e[1]].push_back(e[0]);
}

vector:
queue indicaint
q.push(0);
int count = 0;

(!q.empty()) {
int cur = q.front(); q.pop();
si continúan (vis[cur] TEN- ANTERIEND.count(cur));
vis[cur] = verdadero;
++cuenta;
para (int nxt : adj[cur]) {}
si (!vis[nxt] " sensible !forbid.count(nxt))
q.push(nxt);
}
}
recuento de retorno;
}
};
`` `

■ **C++* *
" noordered_set " para los cheques de membresía O(1).
√≥ - < > > para el BFS iterante.

-...

## 6. Artículo del Blog – “El Bien, el Mal, el Ugly” de **Nodos alcanzables con restricciones* *

### 6.1 Title & Meta‐Description
■ *Título*
■ *LeetCode 2368 – Nodos alcanzables con restricciones: un Java/Python/C++ Deep‐Dive for Job Interviews*

■ **Meta‐Description:**
■ “Master the LeetCode Nodos alcanzables con problemas de restricciones con soluciones óptimas BFS/DFS en Java, Python y C++. Aprenda las ofertas comerciales, las trampas y los patrones de entrevista para aterrizar su próximo papel de ingeniería de software. ”

#### 6.2 Introduction
Empieza con un gancho:

■ “Si has estado mirando el problema de LeetCode **Nodos alcanzables con restricciones**, no estás solo. Es un traversal de árboles engañosamente simple que puede tropezar hasta entrevistadores experimentados. En este post, te guiaré a través del *bueno* (clear BFS/DFS), el *bad* (ineficiente profundidad recursiva primero que puede soplar la pila), y el *ugly* (sin unión de ingeniería superior para un árbol). Proporcionaré código limpio y listo para la producción en Java, Python y C++, además de palabras clave SEO que ayudarán a los reclutadores a encontrarte. ”

### 6.3 Declaración de problemas
Re-establece el problema en inglés claro, enfatizando que es un árbol, a partir del nodo 0, y no se puede pisar los nodos restringidos.

### 6.4 ¿Por qué un árbol lo hace simple
- Sólo 'n-1' bordes.
- Sin ciclos → un solo camino entre dos nodos.
- Traversal de tiempo lineal es suficiente.

### 6.5 The *Good* – Breadth‐First Search

Explique BFS, por qué es natural:
- El conjunto visitado evita la revisión.
- La cola asegura explorar los nodos capa por capa.
- Complejidad: tiempo, espacio.

Mostrar el fragmento Java (o enlace a bloque de código).

### 6.6 The *Bad* – Recursion on a Huge Tree

Muchos novatos escriben un DFS recursivo ingenuo que no protege contra el desbordamiento de pilas por `n = 105`.
- Riesgo de `StackOverflowError` (Java), `RecursionError` (Python), `std::stack_overflow` (C++).
- La optimización de la recursión a la medida de mención no está garantizada en Java o Python.
- Sugerir DFS iterativa con una pila explícita como una alternativa más segura.

### 6.7 The *Ugly* – Over-Engineering with Union‐Find

Algunas soluciones utilizan Union‐Find to “connect” nodes, sólo para olvidar que la entrada ya es un árbol.
- Union‐Find introduce innecesarios 'O(α(n))' sobrecabezado.
- En un árbol ya estás garantizada la conectividad.
- Mostrar un enfoque de unión mínimo y por qué es demasiado.

### 6.8 Edge Cases > Gotchas

Silencio Caso confidencialidad ¿Por qué importa la Mitigación?
Silencio...
Silencio `restricted` contiene sólo hojas Silencio No hay daño, todavía cuenta `0` Silencio
Silencio `restricted` está vacío Silencio Todos los nodos alcanzables Silencio Funciona automáticamente Silencio
Silencio Árbol muy profundo (skewed) ANTE Problemas de profundidad de recesión ← Uso iterativo DFS/BFS Silencio
Silencio Grande `n` (105) Silencio Memoria soplado Silencioso Usar la lista de adyacency, no la matriz de adyacency

### 6.9 Complejidad Cheat‐ Sheet

Silencio Silencio Silencio Silencio Silencio
Silencio--------------
Silencio BFS/DFS (iterative) Silencio `O(n)` Silencio `O(n)` Silencio
TENIDO Recursive DFS TENIDO `O(n)`
Silencioso Union‐Find (over-kill) Silencio `O(n α(n)' Silencio

### 6.10 Tomado para Entrevistas

- **Clarificar la propiedad del árbol**: preguntar si garantizan la aciclicidad (que sí lo hacen).
- **Escoge BFS** si te sientes cómodo con colas; **iterative DFS** si prefieres pilas.
- Siempre protegen contra el desbordamiento de la pila para grandes `n`.
- **Explicar su código**: hablar de conjunto visitado, nodos prohibidos y terminación.

### 6.11 Call‐to‐Action

■ “Ahora que tienes una solución limpia y lista para la producción en Java, Python y C++, es hora de pulir tus habilidades de entrevista. Use este problema como punto de conversación en su próxima entrevista de codificación, y no olvide destacar los intercambios que discutimos. Buena suerte, y siéntete libre de llegar si quieres profundizar en los algoritmos de árboles! ”

### 6.12 SEO Palabras clave (para espolvorear a lo largo del artículo)

- Nodos alcanzables de LeetCode con restricciones
- Java DFS árbol traversal
- Python BFS problema de árbol
- C+++ entrevista de gráfico
- Preguntas de la entrevista a los árboles
- Prep de entrevista de ingeniero de software
- algoritmo de gráfica eficiente
- Solución LeetCode en Java, Python, C++
- Evite el desbordamiento de la pila de recursión
- Union‐Find vs DFS para árboles

-...

## 7. Despliegue rápido

Guardar cada fragmento en su archivo respectivo:

- `Solution.java` → compilar con `javac Solution.java `
- `solución. py` → corre con la solución de pitón. py `
- `solution.cpp` → compilar con g++ -std=c+17 solution.cpp -o solución `

Agregue un arnés de prueba simple si lo desea.

-...

### 8. Nota final

Las tres soluciones funcionan cómodamente bajo el arnés de prueba LeetCode y están libres de trampas comunes. Ilustran cómo un *simple* problema del árbol puede convertirse en *complejo* si no respeta los límites del lenguaje y los patrones algorítmicos. Buena suerte rompiendo entrevistas y aterrizando ese trabajo!