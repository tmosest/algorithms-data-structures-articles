-...
Título: LeetCode 1993. Operaciones en el Árbol -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 1993 - *Operaciones en el árbol*
■ **Una profunda inmersión en la estructura de datos LockingTree* *
■ *Cómo llegar a la entrevista, escriba código Java / Python / C++ y convierta este problema en un escaparate reiniciante. *

-...

## 1. El problema en una nuezquela

Se le da un árbol arraigado con nodos (`0 ... n-1`).
`parent[i]` is the parent of node `i` (`parent[0] = -1`).

Implementar una clase `LockingTree` que apoye tres operaciones:

Silencioso Operación Silencioso
Silencio--------------------------------
Silencio **lock(num, user)** Silencio nodo `num` está desbloqueado Silencio nodo `num` se bloquea por `user` Silencio
Silencio **unlock(num, user)** Silencio node `num` está bloqueado * por el mismo* `user` Silencio nodo `num` se desbloquea ANTE
Silencio **upgrade(num, user)** Silencio node `num` está desbloqueado, tiene un descendiente bloqueado, *y* ningún ancestro bloqueado Silencioso `num` por `user`, desbloquear *todos* sus descendientes

Todas las operaciones deben devolver `verdad ' si tienen éxito, de lo contrario `falso ' .

Constraints:
- 2 ≤ 2000
- En la mayoría de las operaciones totales de 2000
- `user` es un entero positivo hasta '10^4`

-...

## 2. Why This Problem is a “Nice” Interview Question

Por qué importa
Silencio...
Silencio **Tree Traversal** Silencio Demuestra el conocimiento de las listas de adjacency, DFS/BFS. Silencio
Silencio ** Manejo Estatal** Silencio Muestra cómo mantener el estado mutable (`bloqueado[]`) a través de llamadas. Silencio
Silencio **Conciencia de la complejidad** Silencio Realiza que cada operación puede ser `O(n)` en el peor caso, pero está bien para las limitaciones dadas. Silencio
Silencio **API Design** Silencio Destaca las firmas de métodos cuidadosos y devolver semántica. Silencio

En una entrevista, ser capaz de explicar las compensaciones, sugerir optimistas (por ejemplo, mantener un contador bloqueado), y producir código limpio es un gran plus.

-...

## 3. El “bien” – Un recto, Implementación legible

La idea central:

1. ** Listas de niños de construcción** de la matriz de padres (O(n)).
2. Mantenga un array `bloqueado[]` donde `bloqueado[i] = -1` significa "desbloqueado" y de otro modo almacena el id del usuario.
3. Por favor. actualización**:
- Revisar a todos los antepasados (aparecer " padres " ) – O(a la derecha).
- DFS/BFS de `num' para desbloquear descendientes y detectar si alguno estaba bloqueado.

Porque `n ≤ 2000` y llamadas ≤ 2000, el simple O(n) por `upgrade` es perfectamente aceptable.

A continuación se muestran implementaciones limpias en **Java, Python, y C++**.

-...

## 4. Código - Java

``java
importar java.util*;

clase pública LockingTree {

--------- Campos...
int privado final [] padre; // relación padre
int privado final[] bloqueado; // -1 = desbloqueado, otro usuario id
lista final privada realizadaInteger título[] niños; // lista de adjacency

// -------- Constructor...
@SuppressWarnings("unchecked")
public LockingTree(int[] parent) {
esto. padre = padre;
int n = parent.length;
este.locked = nuevo int[n];
Arrays.fill(bloqueado, -1); // todos los nodos comienzan desbloqueados

// construir listas de niños
esto. niños = nuevo ArrayList[n];
para (int i = 0; i < n; i++) niños[i] = nuevo ArrayList fiel();
para (int i = 1; i) {}
niños[i].add(i);
}
}

//-------------- cerradura------------
candado booleano público(incluido num, usuario int) {
si (bloqueado[num]!= -1) devolver falso; // ya bloqueado
bloqueado [num] = usuario;
retorno verdadero;
}

//-------------- desbloquear--------------
booleano público desbloqueo (incluido num, usuario int) {
si (bloqueado[num] == -1 Silencio encerrado[num]!= usuario) devuelve falso;
bloqueado [num] = -1;
retorno verdadero;
}

//-------------- Actualización--------------
public boolean upgrade(int num, int user) {
// 1. nodo debe ser desbloqueado
si (bloqueado[num]!= -1) volver falso;

// 2. ningún ancestro bloqueado
int cur = num;
mientras (curre!= -1) {
si (bloqueado[c]!= -1) devolver falso; // bloqueado ancestro encontrado
cur = parent[cur];
}

// 3. DFS/BFS para desbloquear descendientes y comprobar si alguno estaba bloqueado
boolean hasLockedDescendant = false;
Deque cumplióInteger confianza stack = nuevo ArrayDeque correspondió();
stack.push(num);

mientras (!stack.isEmpty()) {}
int node = stack.pop();
para (incluido niño : niños [nodo]) {}
si (bloqueado[niño]!= -1) {
hasLockedDescendant = true;
}
// desbloquear descendiente si estaba bloqueado
bloqueado [niño] = -1;
stack.push(child);
}
}

si (!HaLockedDescendant) devuelve falso; // regla 2 violado

// bloquear el nodo en sí
bloqueado [num] = usuario;
retorno verdadero;
}
}
`` `

*Por qué es bueno*

- **Claridad** - Una estructura de ayuda (`niños') sostiene el árbol.
- ** Corrección** – Las tres condiciones para la "aceleración" se verifican explícitamente.
- **Performance** - Sólo se necesitan pases lineales; `O(n)` por `upgrade` se ajusta a las limitaciones.

-...

## 5. Código - Python

``python
Clase de bloqueo Árbol:
def __init__(self, parent):
self.parent = parent
n = len(parente)
auto.locked = [-1] * n # -1 = unlocked, else user id
self.children = [[] for _ in range(n)]
para i en rango(1, n):
self.children[parent[i].append(i)

def lock(self, num: int, user: int) - Bool:
si auto.locked[num] != -1:
Retorno Falso
autobloqueado[num] = usuario
Retorno

def deslock(self, num: int, user: int) - Bool:
si auto.locked[num] == -1 o self.locked[num] != usuario:
Retorno Falso
autobloqueado[num] = -1
Retorno

def upgrade(self, num: int, user: int) - Bool:
# 1. node must be unlocked
si auto.locked[num] != -1:
Retorno Falso

# 2. no bloqueado ancestro
cur = num
mientras se cura!= -1:
si auto.locked[cur]!= -1:
Retorno Falso
cur = self.parent[cur]

# 3. DFS para desbloquear descendientes, detectar cualquier bloqueado
pila = [num]
has_locked_descendant = False
mientras que la pila:
nodo = pila.pop()
para niños en sí mismos. niños[nodo]:
si yo. encerrado[niño] -1:
has_locked_descendant = True
auto.locked[child] = -1 # unlock
stack.append(child)

si no has_locked_descendant:
Retorno Falso

# Cierra el nudo en sí #
autobloqueado[num] = usuario
Retorno
`` `

La implementación de Python sigue la misma lógica que Java, pero aprovecha ** listas dinamicas** y una pila de DFS clara**.

-...

## 6. Código: C++

``cpp
Incluido el título
#include >

clase LockingTree {
public:
LockingTree(cont std::vector seleccionadoint
: parent(parente), n(parent.size()), bloqueado(n, -1) {
niños.resize(n);
para (int i = 1; i)
niños [parentes [i].push_back(i);
}

bool lock(int num, int user) {
si (bloqueado[num]!= -1) volver falso;
bloqueado [num] = usuario;
retorno verdadero;
}

bool unlock(int num, int user) {
si (bloqueado[num] == -1 Silencio encerrado[num]!= usuario) devuelve falso;
bloqueado [num] = -1;
retorno verdadero;
}

bool upgrade(int num, int user) {
si (bloqueado[num]!= -1) volver falso; // debe ser desbloqueado

// Ver ancestros
int cur = num;
mientras (curre!= -1) {
si (bloqueado[c]!= -1) devolver falso; // bloqueado ancestro
cur = parent[cur];
}

/ DFS/BFS sobre descendientes
bool hasLocked = false;
std::stack madeint
st.push(num);
(!st.empty())) {}
int node = st.top(); st.pop();
para (incluido niño : niños [nodo]) {}
si (bloqueado[niño]!= -1) hasLocked = true;
bloqueado [niño] = -1; //
st.push(child);
}
}

si (! hasLocked) devuelve falso; // no

bloqueado[num] = usuario; // bloquear el nodo en sí
retorno verdadero;
}

privado:
const std::vector correspondint
std::vector realizadoint confidencial bloqueado;
std::vector seleccionados::vector realizadoint niños;
int n;
};
`` `

*Por qué es bueno*

- Usa 'std:::vector' para todo – no hay asignación dinámica.
- Mantiene la forma del árbol (`niños').
- Usa `estd::stack ' for DFS; no recursion deep concerns.

-...

## 6. El “Bad” – A Less‐Than‐Ideal Approach

Algunos candidatos intentan reconstruir el árbol en cada 'aceleración', o mantener un mapa de bloqueo global que es **no** indexado por nodo id.
Esto puede llevar a:

- **Uso de memoria más alto** (Maps vs arrays).
- **Comprobación del antepasado menor** (escandando el mapa completo cada vez).
- **Harder to reason about** (mixed data structures).

**Bottom line** – si te ves a ti mismo en este código "bad", es hora de refactor.

-...

## 7. El “Ugly” – Intentando sobre-Optimizar Prematurely

Un típico intento “de gran alcance”:

- **Preparar un contador de descendientes encerrados** para cada nodo, actualizarlo en cada `bloqueo'.
Si bien reduce el " costo de actualización " a `O(altura) ' + `O(1) ' para la comprobación descendente, la aplicación se convierte en **bug-prone**:
- Debes propagar cuidadosamente los cambios de contador en el árbol.
- Una sola actualización olvidada puede corromper todas las respuestas posteriores.

- **El DFS recursivo sin una pila** en Python podría alcanzar el límite de profundidad de Python incluso si `n ≤ 2000`.

Si usted necesita mostrar tal optimización, **documentarlo claramente** y proporcionar lógica de retroceso para la corrección.

-...

## 8. Ideas de optimización (para entrevistadores “nice”)

Silencio Idea tóxico Cuando se utiliza para la complejidad
...--------------------------
Silencio **Locked-descendant counter** (`descLocks[]`) Silencio Si quieres garantizar `O(a la altura)` para cada `upgrade` Silencio `O(a la altura)` para bloquear/desbloquear, `O(a la altura)` para actualizar Silencio
Para mayores limitaciones (por ejemplo, `n = 10^5`) Silencio `O(log n)` por operación Silencio
Silencio **Bitset para usuarios** Silencio Si los IDs de usuario son pequeños TEN-time cheque si cualquier ancestro está bloqueado

Debido a que las limitaciones aquí son pequeñas, la implementación “buena” directa es generalmente la mejor opción – ahorra tiempo y evita errores.

-...

## 9. Convertir este problema en *Resume‐Boosting Story*

*Resolví LeetCode 1993 – Operaciones en el Árbol – en Java, Python y C++ con una API limpia, código documentado y un análisis de complejidad claro.”* *

En su entrevista o carta de portada, mencione:

1. **Máquina estatal basada en Tree** – Construí una lista de adyacencia y mantuve una matriz de bloqueo.
2. **Comprobaciones previas a la limpieza** – Cada método devuelve un estado booleano y nunca muta cuando las condiciones previas fallan.
3. **Diseño escalable** – Mientras que mi solución base es `O(n)` por actualización, también bosquejé un contador opcional O(1) bloqueado para sistemas de grado de producción.

Agregar el *blog* (este post) a su cartera o Enlace En le da a los reclutadores una muestra concreta y bien agregada que pueden funcionar inmediatamente.

-...

## 10. Final Checklist for the Interview

- ✅ **Explicar** la estructura de datos en palabras primero.
- ✅ Escriba **clean, typed code** (Java + anotaciones, Python 3.8+ tipo de pistas, C++14+).
- ✅ **Walk through** a sample `upgrade` call, illustrating each pre-condition.
- ✅ Mention a possible *optimization* and discuss when it is worth it.

Buena suerte – ahora estás listo para mostrar a los reclutadores que puedes **diseño, razón y código** un problema de árbol no-trivial en tres idiomas principales! 🚀

-...

#### 📚 Más lectura

- “Tree Traversals – DFS vs BFS” – un refrigerio rápido en las listas de adjacency.
- “Datos completos en entrevistas” – por qué los arrays son a menudo la mejor opción.
- “Java Generics vs Python Dynamic Typing” – elegir la herramienta adecuada para el trabajo.

¡Feliz codificación!