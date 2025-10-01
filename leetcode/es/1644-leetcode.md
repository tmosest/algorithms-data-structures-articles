-...
Título: LeetCode 1644. Ancestro común más bajo de un árbol binario II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Resumen de problemas (LeetCode 1644)

■ **Ancestro común más bajo de un árbol binario II**
■ Medium Silencio 1 k+ resuelto Silencio ⭐⭐⭐⭐

Dada la raíz de un árbol binario y dos nodos " p " y " , devuelven el ancestro común más bajo (LCA)** de " p " y " .
Si **ya sea** `p` o `q` no está presente en el árbol, vuelva `null`.
Todos los valores del nodo son únicos.

■ **Constraints**
* 1 ≤ nodos ≤ 104
* −109 ≤ nodo.val ≤ 109
* `p!= q`

■ **Seguimiento*
■ Encuentra el LCA *sin* un segundo pase que comprueba si existen los nodos.

-...

## 2. ¿Por qué 1644 es más difícil que 236?

← Feature Silencio 236 (“Lowest Common Ancestor of a Binary Tree”) Silencio 1644 (“Lowest Common Ancestor of a Binary Tree II”)
Silencio----------------------------------------------
Silencio **Guarantee** Silencio Ambos `p` y `q` son **garanteed** para estar en el árbol
Silencio ** Resultado en el nodo desaparecido** Silencio Nunca `null` Silencio Debe volver `null` si uno/muchos desaparecidos
Silencio **Early‐exit** Silencio Seguro: volver tan pronto como encuentres `p` o `q` peru Unsafe: todavía debes buscar en el resto del árbol

Debido a la falta de garantía, la solución clásica de 236 (`si (root===p TEN TENIDO root==q) raíz de retorno;`) no se puede utilizar sin modificaciones. Tenemos que hacer un seguimiento de si en realidad vimos ambos nodos mientras todavía atraviesan todo el árbol.

-...

## 3. Panorama general de la solución

Hacemos un solo **post-order DFS** y propagamos dos piezas de información:

1. **El candidato de la LCA** regresó de la llamada recurrente.
2. **Flags** indicando si se ha visto en el subárbol actual la " p " o " .

Cuando ambas banderas son 'verdaderas', el nodo actual es el verdadero LCA.
Si sólo una bandera es "verdadera", devolvemos el nodo que coincida (para que el padre pueda decidir).
Si no hay coincidencia, devolvemos `null`.

Hay dos maneras idiomáticas de almacenar las banderas:

TENCIÓN TERRITORIO ANTERIOR ANTERIOR ANTERIOR
Silencio...
Silencio **Dos campos booleanos** (`pFound`, `qFound`) Silencio Easier para leer Silencio estado Mutable; más difícil de probar en aislamiento
Silencio ** contador entero** TENIDO ÚNICO campo TENIDO Ligeramente menos expresiva pero muy compacta

Ambos tienen **O(N)** tiempo y **O(H)** espacio (apilación de llamadas recursivas).

-...

## 4. Aplicación de Java

``java
// Definición para un nodo de árbol binario.
clase TreeNode
int val;
TreeNode left;
TreeNode right;
TreeNode(int x) { val = x; }
}

Solución de la clase pública {}
----------- Método 1 : dos banderas booleanas ---------- */
Libra booleana privada;
qFound booleano privado;

public TreeNode mínimoCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {}
// banderas de reinicio para cada llamada
fúnebre = falso;
qFound = false;
TreeNode candidate = dfs(root, p, q);
// candidato de retorno sólo si ambos nodos fueron vistos
retorno (pFound " qFound) ? candidato : null;
}

árbol privadoNode dfs(TreeNode node, TreeNode p, TreeNode q) {}
si (nodo == nulo) vuelve nulo;

TreeNode left = dfs(node.left, p, q);
TreeNode right = dfs(node.right, p, q);

si (nodo == p) { libras = verdad; nodo de retorno; }
si (nodo == q) { qFound = verdadero; nodo de retorno; }

si (izquierda != null ' derecha != null) nodo de retorno; // ambos encontrados en subtrees
(izquierda!= nula) ? izquierda : derecha; // uno encontrado o ninguno
}

----------- Método 2 : contador entero (opcional) ------------ */
// int count privado = 0;
// public TreeNode lowestCommonAncestorCounter(TreeNode root, TreeNode p, TreeNode q) {}
// conteo = 0;
// TreeNode candidate = dfsCounter(root, p, q);
// retorno (cuenta == 2) ? candidato : null;
// }
//
// privado TreeNode dfsCounter(TreeNode node, TreeNode p, TreeNode q) {}
// si (nodo == null) vuelve nulo;
// TreeNode left = dfsCounter(node.left, p, q);
// TreeNode right = dfsCounter(node.right, p, q);
// si (nodo == p  vidas eternas node == q) { count++; nodo de retorno; }
// si (izquierda!= null ' derecha != null) nodo de retorno;
// retorno (izquierda!= null) ? izquierda : derecha;
// }
}
`` `

*Explicación*
- El DFS es post-orden: inspeccionamos a los niños antes de decidir sobre el nodo actual.
- `dfs` devuelve el nodo que es `p`, `q`, o el LCA de ellos en el subárbol.
- Las banderas (`pFound ' , `qFound ' ) se fijan sólo cuando el nodo exacto se combina.
- Después del traversal completo, devolvemos al candidato sólo si ambas banderas son "verdaderas".

-...

## 5. Aplicación de los pitones

``python
Definición para un nodo de árbol binario.
Clase TreeNode:
def __init__(self, val=0, left=None, right=None):
self.val = val
autoizquierda
self.right = right

Solución de clase:
def más bajoCommonAncestor(self, root: TreeNode, p: TreeNode, q: TreeNode) - confiar TreeNode confidencialidad Ninguno:
# dos banderas booleanas
self.p_found = False
self.q_found = False

candidato = auto._dfs(root, p, q)
candidato de retorno si mismo. P_fundo y auto. q_found else Ninguno

def _dfs(self, node: TreeNode, p: TreeNode, q: TreeNode) - título TreeNode confidencialidad Ninguno:
si no el nodo:
No.

izquierda = auto._dfs(node.left, p, q)
derecho = uno mismo._dfs(node.right, p, q)

si el nodo es p:
self.p_found = True
Nodo de retorno
si el nodo es q:
self.q_found = True
Nodo de retorno

si izquierda y derecha:
Nodo de retorno
vuelta izquierda o derecha # un lado encontrado o ninguno
`` `

*Tips for Python*
- Use `es` para comparar objetos de nodo, no `=`, porque los valores de nodo son únicos pero necesitamos confirmar la identidad.
- La solución funciona en un solo DFS; no se necesita un segundo pase de “existencia”.

-...

## 6. Aplicación C++

``cpp
* Definición para un nodo de árbol binario. **
struct TreeNode {
int val;
TreeNode *left;
TreeNode *right;
TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

Clase Solución {
bool pFound, qFound; // dos banderas booleanas

TreeNode* dfs(TreeNode* node, TreeNode* p, TreeNode* q) {}
si regresan nullptr;

TreeNode* izquierda = dfs(node- títuloleft, p, q);
TreeNode* right = dfs(node- títuloright, p, q);

si (nodo == p) { libras = verdad; nodo de retorno; }
si (nodo == q) { qFound = verdadero; nodo de retorno; }

si (izquierda " derecha " ) nodo de retorno; // ambos encontrados en subárboles
¿Regresar a la izquierda? izquierda : derecha; // uno o ninguno
}

public:
TreeNode* más bajoCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {}
qFound = falso;
TreeNode* candidate = dfs(root, p, q);
retorno (pFound " qFound) ? candidato : nullptr;
}
};
`` `

El código C++ es casi idéntico a Java – las únicas diferencias son la sintaxis y el uso de punteros crudos.

-...

## 6. Análisis de la complejidad (Todos los idiomas)

Silencio Silencio Silencio Silencio
Silencio----------------
TENIDO DFS traversal TENIDO **O(N)** (cada nodo visitado una vez) Silencio **O(H)** (apilado de llamadas, `H` = altura de los árboles)
Silencio Actualizaciones de la bandera Silencio constante per node Silencio constante per node
Silencio total **O(N)** Silencio **O(H)**

-...

## 7. Casos de borde " Pitfalls comunes

Silencio Caso Edge Silencio Qué ver para Silencio
Silencio...
Silencio **Root es `null`** Silencio Inmediatamente regresa `null`. Silencio
Silencio **`p` o `q` es el mismo que root** Silencio Todavía necesita confirmar que el otro nodo existe en el subárbol. Silencio
Silencio **Arbol escalonado profundo** Silencio Profundidad de la Recursión `H` puede alcanzar `104`; en idiomas con pila limitada puede necesitar una solución iterativa. Silencio
Silencio **Using mutable global state** Silencioso para restablecer banderas entre casos de prueba → respuesta incorrecta. Silencio
Silencio **Comparando por el valor en lugar de la identidad** Silencio En LeetCode los nodos son objetos distintos; comparar `node.val == p.val` puede dar falsos positivos si el árbol tiene valores duplicados (no permitido aquí pero buena práctica). Silencio

-...

## 8. Desglose “Good‐Bad‐Ugly”

Silencio Silencio
Silencio------------Prince------
Silencio **Bien** Silencio • Paso único DFS con clara propagación de banderas. <br título• Código mínimo, O(N) tiempo.
Silencio **Bad** Silencio • Si copia‐pasa la solución 236 (`if(root===p vidas eternaroot==q)return root;`) te perderás el control de existencias. • El acceso temprano en medio de un DFS puede devolver un LCA equivocado si falta un nodo. Silencio • Olvidar restablecer banderas globales en cada caso de prueba. • Usando `==` en valores de nodo en lugar de identidad de nodo. Silencio
Silencio **Ugly** Silencio • Manejando el caso donde sólo uno de los nodos está presente (por ejemplo, `p` es ancestro de `q`, pero `q` está ausente). El DFS arriba devuelve automáticamente `null` en ese escenario, por lo que no se necesita traversal extra. Silencio • Algunos entrevistadores esperan que usted implemente una solución *two‐pass*: primero DFS para LCA, luego BFS/DFS de nuevo para confirmar ambos nodos existen. • Tratar de utilizar un apilador iterante mientras que también mantener dos banderas puede convertirse en verbosa y error-prone. Silencio

-...

## 9. Cómo utilizar esto para una entrevista de trabajo

1. **Explicar la diferencia con 236** – muestra que usted entiende el matiz.
2. **Walk through the DFS** – resalta cómo propagas las banderas.
3. **Mostrar la manipulación de la periferia** – “si un nodo está perdido, vuelva nulo”.
4. **Tiempo/espacio de la mención** – a los entrevistadores les encanta ver O-notación.
5. **Optional: provide the counter-based implementation** – demonstrates you know multiple idioms.

-...

## 10. Paquete de código completo

A continuación encontrará las tres soluciones completas que puede pegar en el editor LeetCode o su propio repositorio.

Silencio Idioma Silencio Archivo Silencio
Silencio...
Silencio **Java** Silencioso `Solution.java` Silencio
Silencioso **Python**
Silencio **C+**

-...

### 10.1 Java (`Solution.java`)

``java
clase TreeNode
int val;
TreeNode izquierda, derecha;
TreeNode(int x) { val = x; }
}

Solución de la clase pública {}
Libra booleana privada;
qFound booleano privado;

public TreeNode mínimoCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {}
qFound = false; qFound = false;
TreeNode candidate = dfs(root, p, q);
retorno (pFound " qFound) ? candidato : null;
}

árbol privadoNode dfs(TreeNode node, TreeNode p, TreeNode q) {}
si (nodo == nulo) vuelve nulo;
TreeNode left = dfs(node.left, p, q);
TreeNode right = dfs(node.right, p, q);

si (nodo == p) { libras = verdad; nodo de retorno; }
si (nodo == q) { qFound = verdadero; nodo de retorno; }

si (izquierda!= null ' derecha != null) nodo de retorno;
(izquierda!= nula) ? izquierda : derecha;
}
}
`` `

### 10.2 Python (`solution.py`)

``python
Clase TreeNode:
def __init__(self, val=0, left=None, right=None):
self.val = val
autoizquierda
self.right = right

Solución de clase:
def más bajoCommonAncestor(self, root, p, q):
self.p_found = False
self.q_found = False
candidato = auto._dfs(root, p, q)
candidato de retorno si mismo. P_fundo y auto. q_found else Ninguno

def _dfs(self, node, p, q):
si no no el nodo: devolver Ninguno
izquierda = auto._dfs(node.left, p, q)
derecho = uno mismo._dfs(node.right, p, q)

si el nodo es p: uno mismo. p_found = Verdadero; nodo de retorno
si el nodo es q: uno mismo. q_found = Verdadero; nodo de retorno

si izquierda y derecha: nodo de retorno
retorno izquierda o derecha
`` `

### 10.3 C++ (`solution.cpp`)

``cpp
* Definición para un nodo de árbol binario. **
struct TreeNode {
int val;
TreeNode *left;
TreeNode *right;
TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

Clase Solución {
qFound;

TreeNode* dfs(TreeNode* node, TreeNode* p, TreeNode* q) {}
si regresan nullptr;

TreeNode* izquierda = dfs(node- títuloleft, p, q);
TreeNode* right = dfs(node- títuloright, p, q);

si (nodo == p) { libras = verdad; nodo de retorno; }
si (nodo == q) { qFound = verdadero; nodo de retorno; }

si (izquierda " derecha " ) nodo de retorno; // LCA encontrado
¿Regresar a la izquierda? izquierda : derecha; // propagar partido
}

public:
TreeNode* más bajoCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {}
qFound = falso;
TreeNode* cand = dfs(root, p, q);
retorno (pFound " qFound) ? cand : nullptr;
}
};
`` `

-...

## 11. Blog Post – “Lowest Common Ancestor of a Binary Tree II: Good, Bad, Ugly (y por qué es una gran pregunta de entrevista)”

■ **SEO Palabras clave**: LeetCode 1644, Ancestro Común Menor, Árbol binario, Entrevista de trabajo, Entrevista de codificación, Estructuras de datos, Recursión, Contrarretro, Bandera, O(N) Solución, Árbol de búsqueda binaria, DFS, BFS, Pensamiento Algorítmico

-...

#### 11.1 Introduction

Si se está preparando para una entrevista de ingeniería de software, se encontrará rápidamente con problemas *“Lowest Common Ancestor (LCA). La variante clásica —*encontrar el LCA en un árbol binario de búsqueda*— es común, pero *LeetCode 1644* empuja el sobre pidiendo el LCA **en cualquier árbol binario**, y **sólo si ambos nodos existen**. Es la combinación perfecta de la maestría en estructura de datos, el pensamiento recursivo y el manejo de los bordes.

Este post camina por lo que hace que el problema “Bueno”, las trampas que lo hacen “Bad”, y el matizado escenario “Ugly” que puede hacer frente a usted. Terminaremos con una lista de verificación práctica para responder esto en una entrevista, para que puedas entrar en la siguiente sala de entrevistas con confianza.

-...

### 11.2 El “bien” – ¿Por qué un solo paso es elegante

1. *Simlicidad*
Un único DFS que lleva dos banderas booleanas (`pFound`, `qFound`) es todo lo que necesitas.
No hay bucles adicionales o estructuras de datos complejas.

2. Tiempo óptimo
Cada nodo es visitado una vez → **O(N)**.
Los entrevistadores les encanta ver una prueba lineal en la sección *análisis*.

3. **Uniform para todos los árboles**
Trabaja para árboles equilibrados, segados o degenerados.
La profundidad de la recuperación es la altura del árbol (`H`), dando **O(H)** espacio.

4. **Muchas maletas de borde Internamente**
Si los nodos de destino son iguales a la raíz, uno falta, o uno es un ancestro, las banderas deciden automáticamente si debemos devolver `null' o el LCA real.

-...

### 11.3 El “Bad” – Mispasos comunes (y cómo evitarlos)

TENIDO ANTERIOR ANTERIOR ANTERIOR Por qué sucede
Silencio...
← Copiar 236 solución LCA Silencio Asumiendo 1644 es idéntico a 236 Silencio Añadir existencia banderas o segundo paso Silencio
Silencio Temprano de salida mediados-DFS Silencio Creyendo que se puede romper una vez que golpeó `p` o `q` No salgas temprano; propagar banderas hacia arriba
Silencio Olvídate de reiniciar banderas Silencio Correr múltiples casos de prueba en el mismo tiempo de ejecución Silencio Reset `pFound ' y `qFound ' en el comienzo de cada llamada
TENIDO Utilizando la igualdad de valor (==`) en lugar de identidad TENIDO Confusión entre el valor de nodo y el objeto de nodo TENIDO Utilizar `es` en Python, `==` sólo para primitivos, `nodo == p` en Java/C++ para la identidad de objeto

-...

### 11.4 El "Emocionado" – El Edge‐Case donde se pierde un nodo

■ **Escenario**: `p` es el antepasado de `q`, pero `q` no existe en realidad en el árbol.
■
■ **¿Qué es Ugly? #
■ Si usted implementa ingenuamente la bandera de un solo paso, usted podría pensar que todavía devolverá el LCA correcto. Pero volverá `null` porque `qFound ' permanece `false ' . Eso es *exactamente* el comportamiento esperado para este problema. La “superficie” proviene de soluciones antiguas que hacen un enfoque *two-pass*: primero encuentra el LCA, luego un BFS/DFS separado para confirmar que ambos nodos existen. Esta traversal extra puede hacer la solución más difícil de razonar y propenso a los errores.

**Por qué gana el Flag‐DFS* *
Las banderas `pFound` y `qFound` son *propagadas* todo el camino hasta la pila de recursión. Si un nodo nunca aparece, la bandera correspondiente permanece `false`. Por lo tanto, el final `si (pFound ' qFound)` te asegura devolver `null` si el segundo nodo está desaparecido. No hay bucles extras, no hay contabilidad desordenada, sólo un traversal limpio.

-...

### 11.5 Interview Talk-Track

1. **Comienza con la definición del problema** – enfatiza que estamos tratando con *objetos*, no sólo valores enteros.
2. **Explicar la diferencia con el clásico LCA (BST)** – la variante BST explota el pedido, pero 1644 requiere una solución estructural pura.
3. En la pizarra. Marca donde se establecen las banderas y cómo viajan.
4. **Mostrar el pseudocódigo** (similar al código Java) y señalar las dos líneas clave: `si(nodo == p) { libras = verdadero; nodo de retorno; }`.
5. **Discuss edge‐case**: Si `root == p`, todavía necesitamos confirmar `q` está en el subárbol. Las banderas lo resuelven automáticamente.
6. **Mención de la solución opcional basada en contra** – “en lugar de booleanos, podría haber usado un contador entero. Ambos son idiomáticos; elegiré lo que el entrevistador prefiere. ”
7. **Tiempo & Espacio** – escribir rápidamente el grande O fórmulas.
8. **Envolver** – “Así que 1644 es una gran pregunta de entrevista porque prueba la comprensión de la recursión, las banderas, el manejo de los bordes y la complejidad algorítmica en un solo problema. ”

-...

### 11.6 Pensamientos Finales

- *LeetCode 1644* es más que un rompecabezas de codificación; es un examen micro de cómo se manejan las restricciones que cambian un problema clásico.
- Dominar el DFS de un solo paso con banderas; estará listo para jueces en línea y entrevistas en persona.
- Mantenga su código limpio, anota sus pensamientos, y esté listo para responder preguntas de seguimiento como “¿Qué pasa si el árbol era un BST?” o “¿Puede resolver esto iterativamente? ”

-...

### 11.7 Takeaway

Ya sea que esté resolviendo esto en una pizarra o un portátil, recuerde: **entendiendo la declaración del problema profundamente** (el “bueno”), **evitando las trampas** (el “malo”) y ** manejar los casos más difíciles de borde** (el “muy”) es lo que distingue a los mejores intérpretes. LeetCode 1644 es un ejemplo de este camino.

Buena suerte, y feliz codificación! 🚀

-...

*No dude en reservar este post y compartirlo con su grupo de estudio de codificación. ¡Si lo encuentras útil, deja un comentario o una estrella en el repositorio! *

-...

■ **Author**: *Su nombre* – *Data‐Structures Enthusiast, Ingeniero de Software, Entrenador de Entrevista*
■ **Fecha**: *2024-07-12*
■ **Comentarios**: *¡Abre para la discusión! *

-...

Esto completa la explicación completa, el código y el análisis de entrevistas para **LeetCode 1644 – Ancestro Común Lo más bajo de un Árbol binario II**. ¡Feliz entrevista!