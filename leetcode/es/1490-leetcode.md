-...
Título: LeetCode 1490. Clone N-ary Tree -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Clone N‐ary Tree – 1490 (LeetCode)
**Bueno, malo & ugly - una bufanda profunda de trabajo**
*Publicado 2025 – SEO-optimizada para la preparación de entrevistas y gerentes de contratación*

-...

## 1. Panorama general de los problemas

LeetCode 1490 – **Clone N‐ary Tree**
- Dificultad:
Devuelve una copia profunda de un árbol N-ary.
- ** Formato de entrada:** serialización de orden de nivel con `null` como separador de niños.
- *Constraints*
- Profundidad ≤ 1000
- Nodos totales ≤ 104

■ La tarea es esencialmente la misma que *Clone Graph* (LC 133) pero con una estructura de árboles.
■ Puede resolverlo con el espacio auxiliar DFS (recursivo o iterativo) o BFS – todo el tiempo O(N) y O(N).

-...

## 2. Por qué este problema importa

Por qué los entrevistadores se preocupan
Silencio...
Silencio **Recursive vs. Iterative** ¦ Shows mastery of stack/queue management and base‐case handling. Silencio
Silencio **HashMap / Diccionario** Silencio Demuestra el manejo de la identidad de los nodos (igualdad puntero). Silencio
Silencio **Graph vs. Tree** Silencio Proves usted puede reutilizar una solución a través de las estructuras de datos. Silencio
Silencio **Space-Time Tradeoffs** ← Highlights understanding of deep‐first vs. panth‐first traversal. Silencio

■ Resolviendo esto en *los tres idiomas principales* (Java, Python, C++) señales de que eres un codificador completo listo para cualquier pila de tecnología.

-...

## 3. El “bien” – Elegante DFS Recursivo

``java
/* Java – Recursive DFS (limpio e idiomático) */
Clase Node {}
int val;
public List Node confía children = new ArrayList correctamente();
public Node() {} {}
public Node(int _val) { val = _val; }
public Node(int _val, List Garantizado) { val = _val; children = _children; }
}

Clase Solución {
público Node clone Tree(Node root) { return dfs(root); }

privado Nodo dfs(Nodo cur) {
si (cur == null) vuelve nulo;
Node clone = nuevo Node(cur.val);
para (Niño nodo : cur.niños) {}
clone.children.add(dfs(child));
}
clon de retorno;
}
}
`` `

**Pros**
Una línea por paso, fácil de razonar.
- **Espacio** - Apilación de recidiva (H = altura del árbol).
- **Readability** - perfecto para entrevistas de codificación.

**Cons**
- La profundidad de la recuperación puede alcanzar el límite de la pila de Java si el árbol es muy profundo (≤1000 → seguro, pero todavía un riesgo en idiomas con límites más estrictos).

-...

## 4. El “Bad” – Uso de mapas ineficientes

``java
/* Java – Usando un mapa que recrea los nodos cada vez (O(N2)) */
Clase BadSolution {}
public Node clone Árbol(Raíz del nodo) {
si (root == null) vuelve nula;
Mapa seleccionadoNodo, Node relativo mapa = nuevo HashMap fiel();
clone(root, map);
return map.get(root);
}

clon de vacío privado(Node cur, Mapa Node, Node título) {
si (cur == null) regresa;
Node clone = map.computeIfAbsent(cur, n - nuevos Node(n.val));
para (Niño nodo : cur.niños) {}
clone.children.add(clone(child, map));
}
}
}
`` `

■ El truco 'computeIfAbsent` está bien, pero el código aún obliga a buscar un mapa **todo** niño, causando un factor constante O(N2) oculto en el peor de los casos.
■ **Evitar** en producción; utilizar la versión recursiva simple arriba.

-...

## 5. El “Ugly” – Manual Stack Management en Java

``java
/* Java – Apilación manual pero todavía O(N) */
clase UglySolution {}
public Node clone Árbol(Raíz del nodo) {
si (root == null) vuelve nula;
Mapa seleccionadoNodo, Node relativo mapa = nuevo HashMap fiel();
Deque node confianza stack = nuevo ArrayDeque corresponde();
stack.push (root);
map.put(root, new Node(root.val));

mientras (!stack.isEmpty()) {}
Nodo cur = pila.pop();
para (Niño nodo : cur.niños) {}
si (!map.containsKey(child) {
map.put(child, new Node(child.val));
stack.push(child);
}
map.get(cur).children.add(map.get(child));
}
}
return map.get(root);
}
}
`` `

■ Funciona bien, pero sujeta la solución. En entrevistas, se prefiere un método recursivo *single*.
■ Sólo use versiones iterativas cuando el entrevistador lo solicite explícitamente.

-...

## 6. BFS – Ropa de Nivel por Nivel (Python & C++)

## Python

``python
# Python 3 – BFS (queue) solution
de las colecciones importa
de la importación Lista

Clase Nodo:
def __init__(self, val=0, children=None):
self.val = val
niños = niños o []

Solución de clase:
def clone Tree(self, root: 'Node') - título 'Node':
si no raíz:
No.

mapeo = {root: Node(root.val)}
q = deque([root])

mientras q:
cur = q.popleft()
para niños en cura. niños:
si el niño no está en la cartografía:
mapping[child] = Node(child.val)
q.append(child)
mapping[cur].children.append(mapping[child])

mapeo de retorno[root]
`` `

### C++

``cpp
// C+17 – solución BFS (queue)
Incluido el título
#include >
#include ■unordered_map Conf

usando std namespace;

struct Node {}
int val;
vector Node* niños;
Nodo(int _val = 0) : val(_val) {}
};

Clase Solución {
public:
Node* cloneTree(Node* root) {
si (!root) regresa nullptr;
unordered_map madeNode*, Node*
mp[root] = nuevo Node(root- Confval);
queue hacía Node*
q.push(root);

(!q.empty()) {
Nodo* cur = q.front(); q.pop();
for (Node* child : cur- ratiochildren) {}
si (!mp.count(child)) {
mp[child] = new Node(child- Confval);
q.push(child);
}
mp[cur]- confíachildren.push_back(mp[child]);
}
}
devolver mp[root];
}
};
`` `

*Key Takeaways*

Silencio Idioma Silencio Preferente Traversal
Silencio----------------------------
TEN Java TENIDO Recursive DFS (por defecto) TENIDO O(N) tiempo, O(H) stack ANTE
TENIDO Python TENIDO BFS (queue) es más claro TENIDO O(N) tiempo, O(N) cola ANTE
TENIDO C++ TENIDO BFS o DFS, ambos OK TENIDO O(N) tiempo, memoria O(N)

-...

## 7. Seguimiento: De Árboles a Gráficos

Si la entrada era un gráfico **directo** en lugar de un árbol, el mismo patrón funciona:

- **Mantenga un `map armonizado, clone]** para evitar revisiting nodes.
- Traverse con DFS/BFS como siempre.
- La única diferencia es que **debemos revisar el mapa antes de que se repita/copiar para manejar ciclos.

■ **Entrevista Trick:**
*“Voy a copiar la lógica del árbol pero añadir un conjunto visitado. Eso también funciona para gráficos.”*
■ Mostrar al entrevistador que usted entiende *identidad vs. valor*.

-...

## 8. Time & Space Complexity Recap

Silencio Silencio Silencio Silencio Silencio
Silencio--------------
← Recursive DFS Silencio **O(N)** Silencio O(H)
Silencio Iterative DFS Silencio **O(N)** Silencio O(H) pila Silencio
TENIDO BFS TENIDO **O(N)** Silencio O(N) cola (anchura de caso inferior)

■ Para un árbol equilibrado, H ♥ log N → uso casi lineal de la pila.
■ Para un árbol degenerado (linked-list), H ♥ N → sigue siendo aceptable para las limitaciones dadas.

-...

## 9. SEO‐Friendly Closing: “Por qué este blog ayuda a su búsqueda de trabajo”

1. **Keyword Rich** – “Clone N‐ary Tree”, “LeetCode 1490”, “DFS”, “BFS”, “Java Python C++”.
2. **Entreview‐Ready** – Cubre * todos* estilos de traversal, el uso del mapa y la extensión del gráfico.
3. **Job‐Specific** – Demuestra que puedes resolver un problema de entrevista canónica *a través de idiomas*.
4. **Problema‐Solving Insight** – Explica por qué ciertos enfoques son “buenos” o “malos”, a los reclutadores de habilidades les encanta.

■ **Takeaway:** Dominar este problema demuestra que puede *deep‐clone*, *traverse*, y *reuse* lógica a través de las estructuras de datos, un sello distintivo de un ingeniero de backend senior.

-...

## 10. Código completo

■ Utilice los siguientes snippets como referencia rápida o para copiar-paste en su IDE.

## Java (Recursive DFS)

``java
clase Nodo igual que en la sección 3
Clase Solución {...} // código DFS recurrente
`` `

## Java (Iterative DFS)

``java
clase Solución { ... } / / / / iterative DFS code (sección 4)
`` `

## Java (BFS)

``java
clase Solución {...} // Código BFS (sección 4)
`` `

### Python (BFS)

``python
clase Nodo: ...
Clase Solución: ...
`` `

### C++ (BFS)

``cpp
struct Node {... };
Clase Solución {... };
`` `

-...

## 11. Lista de verificación de inicio rápido

Silencio TENIDO ANTERIOR ANTERIOR
Silencio...
✔ Cambios en la vida Escribe la definición `Node` en tu idioma.
Ω ✔ Cambios en la vida Elige *DFS* para entrevistas rápidas (Java/Python) o *BFS* para claridad (Python/C++).
← ✔ Cambio tóxico Utiliza un solo `mapa/Diccionario` para almacenar el clon original →.
Ω ✔ Cambio de imagen Demostrar la extensión del gráfico si se le pregunta.
← ✔ Cambio de vida con árboles degenerados ( profundidad = 1000) para confirmar la seguridad.

-...

**Feliz codificación - y buena suerte en su próxima entrevista! * *
*(Sea libre de marcar esta página o compartirla con tus compañeros candidatos.) *