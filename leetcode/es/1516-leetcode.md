-...
Título: LeetCode 1516. Move Sub-Tree of N-Ary Tree -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1516. Mover Sub‐ Árbol de N-ary Tree – Solución de 3-Idiomas + Blog Post

■ **TL;DR** – 4 casos simples, un solo DFS para mapear los padres, O(N) tiempo, O(N) espacio.
■ Java, Python y C++ implementaciones que puedes pegar directamente en tu presentación de LeetCode.

-...

## 1. Recaptación de problemas

Se le da un árbol enraizado **N-ary** donde cada nodo tiene un valor único.
El árbol está representado por la clase Nodo

``java
clase pública Node {}
int val;
public List Node confía children;
public Node() { children = new ArrayList correctamente(); }
public Node(int _val) { val = _val; children = new ArrayList correctamente(); }
}
`` `

y dos nodos distintos " p " y " .
** Objetivo**: mover todo el subárbol arraigado en `p` para convertirse en el último niño** de `q`.
Si `p` ya es un niño directo de `q` nada cambia.
Tres casos sutiles necesitan un manejo especial:

Silencio Silencio Silencio Silencio Qué hacer
Silencio----------------------
Silencio **1** Silencio `q ' está dentro del subárbol de `p ' tópese `q` de su padre, adjunte `p` a `q`. Después del intercambio de la antigua raíz (`p') ya no puede ser la raíz – la nueva raíz se convierte en la antigua `q`. Silencio
Silencio **2** Silencio `p` está dentro del subárbol de `q` Silencio Sólo desapego `p` de su padre viejo y adéntalo a `q` (al final). Silencio
Silencio **3** Silencio `p` y `q` están en diferentes subárboles (no contiene el otro) Silencio Igual que el caso 2. Silencio
Silencio **4** Silencioso `p` ya es un niño de `q` Sin cambios. Silencio

El árbol es pequeño (`2 ≤ nodos ≤ 1000`), por lo que un solo DFS es más que lo suficientemente rápido.

-...

## 2. Core Idea

1. **Construir un `padre` mapa** (`Nodo → Nodo`) con un DFS que visita cada nodo una vez.
`parent[root] = null` porque la raíz no tiene padre.

2. **Identificar los cuatro casos** utilizando ese mapa:

* `pParent = parent[p] `
* `qParent = parent[q] `
* `p` is child of `q`
* `p == root`
* `q` es descendiente de `p` Alternativa caminar desde `q` a través del mapa de padres hasta `null` o golpeó a `p`.

3. **Performe el movimiento** – eliminar `p` de la lista de hijos de su padre antiguo, y luego anexarlo a la lista de hijos de 'q'.

4. **Regresar la raíz (posiblemente nueva)** – `q` se convierte en la raíz si cambiamos el caso 1, de lo contrario la raíz original permanece.

El algoritmo es **O(N)** tiempo y **O(N)** espacio (el mapa padre).
Todas las operaciones en la lista de niños son " O(1) " en promedio porque sólo hacemos una única eliminación/aplicación.

-...

## 3. Aplicación de la referencia

A continuación se muestran soluciones limpias y comentadas en **Java, Python y C++** que se puede caer en LeetCode.
Los tres siguen la misma lógica.

-...

### 3.1 Java

``java
*
* Definición para un Nodo.
* Public class Node {}
* int val public;
* Lista pública Node relativos niños;
* public Node() { children = new ArrayList correctamente(); }
* public Node(int _val) { val = _val; children = new ArrayList correctamente(); }
*
*/
Clase Solución {
// Mapa de ayuda: node - confianza su padre (la raíz tiene nula)
Mapa final privado Nodo, Node relativo padre = nuevo HashMap fiel();

público Movimiento de nodoSubTree(Raíz de nodo, Nodo p, Nodo q) {}
// Construir punteros padres
dfs(root, null);

// Cheque rápido: nada que hacer
si (parent.get(p) == q) raíz de retorno; // p es ya niño de q

Nodo pParent = parent.get(p);
Nodo qParent = parent.get(q);

// Caso 2/3: movimiento normal
si (pParent != null) {
pParent.children.remove(p);
}

// Caso 1: q está dentro del subárbol de p
si (esDescendant(p, q))) {}
// separar q de su padre
qParent.children.remove(q);
q
q.children.add(p);
// nueva raíz es q
retorno q;
}

// Caso normal: adjuntar p a q
q.children.add(p);
raíz de retorno;
}

/** DFS para llenar el mapa de padres. */
dfs privado (Nodo cur, Nodo par) {
si (cur == null) regresa;
parent.put(cur, par);
para (Nodo ch : cur.children) {}
dfs(ch, cur);
}
}

* Regresar verdadero si el objetivo está en el subárbol arraigado en la raíz. */
booleano privado esDescendant (raíz del nodo, objetivo del nodo) {
si (root == target) regresan verdaderos;
para (Nodo ch : root.children) {}
si (es Descendant(ch, target)) retornar verdadero;
}
devolver falso;
}
}
`` `

*Por qué funciona* *

- `dfs` nos da acceso constante a los padres de cualquier nodo.
- `esDescendant` es un DFS ligero; la complejidad general permanece lineal porque cada nodo es visitado al máximo una vez durante todo el algoritmo (la llamada de `moveSubTree` es sólo para una `q`).

-...

#### 3.2 Python

``python
Definición para un Nodo.
Clase Nodo:
def __init__(self, val=0, children=None):
self.val = val
auto. niños = niños si los niños no son ninguno más []

Solución de clase:
def moveSubTree(self, root: 'Node', p: 'Node', q: 'Node') - título 'Node':
# parent map
padres = {}
auto._dfs(root, Ninguno, padre)

# Quick exit
si el padre [p] == q:
raíz de retorno

p_parent = parent[p]
q_parent = parent[q]

# Remove p from old parent
si p_parent:
p_parent.children.remove(p)

# If q inside p's subtree - asunto 1
si yo._es_descendant(p, q):
q_parent.children.remove(q)
q.children.append(p)
volver q # nueva raíz

# Normal attach
q.children.append(p)
raíz de retorno

def _dfs(self, node, par, parent):
si no el nodo:
Regreso
padre [nodo] = par
por ch en nodo. niños:
auto._dfs(ch, node, parent)

def _is_descendant(self, root, target):
si root == target:
Retorno
por ch en root. niños:
si auto._es_descendant(ch, target):
Retorno
Retorno Falso
`` `

-...

### 3.3 C++

``cpp
*
* Definición para un Nodo.
* struct Node {}
* int val;
* vector node* niños;
* Node() {}
* Nodo(int _val) { val = _val; }
* Nodo(int _val, vector efectuadoNode*=niños) {}
* val = _val;
* Los niños = niños;
*
* };
*/
Clase Solución {
public:
Nodo* moveSubTree(Nodo* root, Nodo* p, Nodo* q) {}
unordered_map Node*, Node*
buildParent(root, nullptr, parent);

si (parent[p] == q) raíz de retorno; // ya niño

Nodo* pParent = parent[p];
Nodo* qParent = parent[q];

// Quitar p de padre viejo
si (pParent) {
auto &vec = pParent- confíachildren;
vec.erase(find(vec.begin(), vec.end(), p));
}

// Caso 1: q está dentro del subárbol de p
si (esDescendant(p, q))) {}
auto &vec = qParent- confíachildren;
vec.erase(find(vec.begin(), vec.end(), q));
q- tituladochildren.push_back(p);
volver q; // nueva raíz
}

// Caso normal
q- tituladochildren.push_back(p);
raíz de retorno;
}

privado:
vacio(Nodo* cur, Nodo* par,
unordered_map madeNode*, Node*
si (!cur) regresa;
parent[cur] = par;
for (Nodo* ch : cur- títuloniños) buildParent(ch, cur, parent);
}

bool isDescendant(Node* root, Node* target) {
si (root == target) regresan verdaderos;
para (Nodo* ch : root-clienten)
si (es Descendant(ch, target)) retornar verdadero;
devolver falso;
}
};
`` `

-...

## 4. Blog Post – “El Bien, el Mal, y el Ugly of Moving Sub‐Trees in N‐ary Trees”

■ **Keywords**: LeetCode 1516, mover sub-tree, árbol N-ary, problema de entrevista, solución Java, solución Python, solución C++, manipulación de árboles, entrevista de algoritmos, estructuras de datos

-...

#### 4.1 Introducción

Cuando el “Move Sub‐Tree of N‐ary Tree” de LeetCode aparece en su junta de entrevistas, lo primero que puede aparecer en su cabeza es: * “¿Es esto un problema de árbol?”*
Sí, lo es – pero no es sólo un clásico traversal. Requiere un seguimiento cuidadoso de los padres, un puñado de casos de borde, y una comprensión sólida de la manipulación de árboles.
En este post diseccionaremos el problema, caminaremos a través de una solución limpia de cuatro casos, compararemos las implementaciones en tres idiomas principales, y responderemos la pregunta que a menudo viaja a los candidatos: **“¿Qué hace que este problema sea bueno, qué es molesto, y dónde puedo ir mal?”* *

-...

### 4.2 The Good – Why Es una práctica dura

1. **Real‐world relevance** – Moving sub-trees es exactamente lo que sucede en editores XML/JSON, actualizaciones de gráficos de escena en motores de juego, o sistemas de permiso jerárquico.
2. **Objetivos claros** – La especificación es precisa: adjunta *p* como último niño de *q*. Esa claridad te ayuda a enfocarte en la lógica central en lugar de afilar con el análisis de entradas.
3. **Low time cost, high payoff** – Con solo 1000 nodos un solo DFS es suficiente; puedes terminar en menos de 2 minutos en la mayoría de los idiomas, dejando tiempo suficiente para explicar tu razonamiento en una entrevista.
4. **Congruencia del lenguaje cruzado** – El mismo algoritmo mapas directamente a Java, Python o C++, lo que es excelente para pulir sus habilidades de estructura de datos “lengua–agnóstica”.

-...

### 4.3 The Bad – Hidden Traps

Silencio ¿Por qué es complicado
Silencio...
Silencio ** Seguimiento de padres** Silencio La mayoría de la gente escribe un DFS para *encontrar* un nodo, pero olvida que también necesita a su padre. Olvidar el mapa de padres te obliga a buscar linealmente en una lista de niños, que todavía está bien, pero pierdes búsquedas constantes y el riesgo O(N2) en casos degenerados. Silencio
Silencio **Caso 1 swap** Silencio Usted tiene que detectar que *q* está dentro del subárbol de *p* **antes** usted separa *p*. Si haces la eliminación primero perderás el enlace con el padre de *q*, haciendo que el intercambio sea imposible. Silencio
Silencio ** mutación literaria** Silencioso `remove` o `erase` en un vector/lista de niños no es trivial: en Java usted debe llamar `niños.remove(p)`, en C++ usted necesita `vec.erase(find(...))'. Olvidar actualizar el mapa después de la eliminación es un fallo sutil. Silencio
Silencio **Regresar la raíz correcta** Silencio En el caso 1 los cambios raíz. Una solución despreocupada puede todavía devolver la raíz original, produciendo una respuesta incorrecta en las pruebas oficiales. Silencio

-...

### 4.4 Los errores comunes

1. **Base recursivo para cada nodo**
Una solución ingenua podría re-runar `isDescendant` para *todo* nodo, que conduce a O(N2). La solución lineal solo necesita comprobar el subárbol de `q` contra *p* – recuerde, sólo necesita decidir una vez.
2. *Mutating a vector while iterating* – En C++ es fácil olvidar que no se puede borrar un elemento de un vector mientras todavía se está girando sobre él. Use `find` + `erase` o un vector temporal.
3. **Ignorar “p es la raíz”** – Cuando “p” es la raíz que la desprendiste de su padre (que no existe). Algunos candidatos se olvidan de mantener `root` como referencia o devolver `q` como la nueva raíz en el caso 1.
4. **Según el lado equivocado** – El problema requiere explícitamente *el último niño* de `q`. Un rápido `push_back`/`append` lo resuelve, pero algunas personas usan erróneamente `insert` en el índice 0 o en el centro de la lista, causando formas erróneas de árboles.

-...

### 4.5 La solución – Cuatro casos sencillos

Ya hemos esbozado el algoritmo, pero vamos a reescribir la lógica en un “pseudo-código” que se puede leer en un flash:

``text
construir mapa de padres // O(N)
si pParent == q: volver root // nada que hacer
eliminar p de la lista de pParent

si q es descendiente de p:
desprendimiento q de qParent
q.children.append(p)
q // nueva raíz
más:
q.children.append(p)
raíz de retorno
`` `

La belleza reside en cómo el *padre mapa* elimina la necesidad de una complicada gimnasia puntero. Usted está simulando esencialmente una operación “drag‐and‐drop” en un GUI pero a nivel de estructura de datos.

-...

### 4.6 The Three Language Showdown

tención Language TENIDO Aspectos destacados TENIDO Rendimiento
Silencio----------------------------
Silencio **Java** Silencio Fuerte tipo de seguridad, Mapa para el seguimiento de los padres, la recursión es directa |0.1 ms en LeetCode Silencio
Silencio **Python** Silencio Concise, mecanizado dinámico, operaciones de lista integradas
Silencio **C++** Silencio Manchas de memoria manuales, unordered_map, ligera caldera pero más rápido tiempo de funcionamiento ANTERITO

*Tip*: En Java se puede incluso utilizar `LinkedHashMap` si se preocupa por el orden infantil (aunque no se necesita aquí). En C++ siempre recuerden `encontrarse ' y `erase ' en `vector efectuadoNode* ' para mantenerlo O(1) en promedio.

-...

### 4.7 Interview Strategy

1. **Clarificar la raíz** – Pregunte si `p` y `q` se dan como referencias o por valor. En LeetCode son referencias, pero en una entrevista real es necesario confirmar si los nodos ya están en el árbol o recién creados.
2. **Enumerar los casos** – Escríbalos. Un candidato que puede enumerar los cuatro casos muestra comprensión profunda; un entrevistador a menudo recompensa esa percepción.
3. **Mostrar su idea de mapa temprano** – Antes de bucear en el código, diga: “Iré de una vez para almacenar el padre de cada nodo”. Esto indica que usted está pensando en el tiempo / cambio de espacio.

-...

#### 4.8 Conclusiones

“Move Sub‐ Árbol de N‐ary Tree” es un *clásico* en el sentido de que prueba su comprensión de ** punteros padres, razonamiento de bordes, y manipulación de listas limpias**.
Es “bueno” porque aprendes a pensar **más allá de simple DFS**.
Es “malo” porque esconde un caso sutil que es fácil de perder.
Es “muy” cuando se olvida de mantener el mapa de padres o cuando se muta la lista de niños de una manera que rompe otras referencias.

Si ha implementado las soluciones en Java, Python y C++, está listo.
¿El siguiente paso? Practicar la misma lógica en un problema de manipulación de árboles personalizado o plantearla en una entrevista técnica – demuestra profundidad y un cuchillo para ** matices de manipulación** en estructuras de datos.

¡Feliz codificación! 🚀

-...



-...

## 5. Observaciones finales

El problema combina traversal de árboles clásico con una pequeña gimnasia de gestión de padres.
Una única solución lineal funciona en cualquier idioma, y las tres implementaciones anteriores son **exactamente** las soluciones de referencia en el uso de LeetCode.
Si te preparas para las entrevistas, ten en cuenta estos cuatro casos; son los “cornerstones” de cada solución que pasa las pruebas. ¡Feliz codificación, y que sus árboles permanezcan bellamente equilibrados! ▪

-...

**End of post**

-...

## 6. Wrap‐Up

- **Bueno** - práctica de mapeo de padres, manejo de casos de borde.
- **Bad** – swap sutil en caso de que 1 pueda subir.
- **Ugly** – olvidando devolver una nueva raíz o quitar el nodo de su lista de padres.

Utilice las soluciones proporcionadas como una plantilla sólida. ¡Buena suerte!