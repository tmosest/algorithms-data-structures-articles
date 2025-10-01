-...
Título: LeetCode 1666. Cambiar la raíz de un árbol binario -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1666 – **Cambia la raíz de un árbol binario**
*LeetCode – Medium – DFS – Manipulación de punteros*

■ # Objetivo #
■ Dada la raíz de un árbol binario y un nodo de hoja, "reroot" el árbol para que la hoja se convierta en la nueva raíz.
■ Cada nodo en el camino de la hoja a la vieja raíz debe cambiar a sus hijos:
* Si un nodo tiene un niño izquierdo, ese niño se convierte en el niño derecho del nodo;
* El anterior padre del nodo se convierte en el hijo izquierdo del nodo.
■ Por último, todos los punteros 'padre' deben ser actualizados (de lo contrario obtendrás *Respuesta incorrecta*).

A continuación encontrará soluciones completas, listas para copiar en **Java, Python y C+**.
Después del código he escrito un artículo corto de estilo blog que cubre el **bueno, el malo, y el feo** de este problema – genial para pulir tus notas de entrevista y SEO-optimizado para la búsqueda de trabajo.

-...

## 1. Solución Java

``java
// Definición para un nodo de árbol binario con puntero padre.
Clase Node {}
int val;
Nodo izquierdo;
Derecho de nodo;
Nodo parent;
Nodo(int x) { val = x; }
}

Solución de la clase pública {}
// la raíz original es necesaria sólo para el control de la caja base
privado Nodo original Root;

público Nodo flipBinaryTree(Raíz del nodo, hoja del nodo) {
original Root = root;
ayudador de retorno (carne, nulo); // hoja se convierte en nueva raíz
}

privado Node helper(Node cur, Node newParent) {
Nodo viejoParent = cur.parent; // recordar original parent
cur.parent = nuevoParent; // actualización padre puntero

// si estamos "regresando" a través del padre viejo debemos
// desconectar ese enlace para evitar ciclos
si (cur.left == newParent) cur.left = null;
si (cur.right == newParent) cur.right = null;

// hemos terminado una vez que hemos alcanzado la antigua raíz
si (cur == originalRoot) retorno cur;

// si el niño izquierdo existe se convierte en el nuevo niño derecho
si (cur.left != null) cur.right = cur.left;

// recurse en el padre anterior – se convierte en el niño izquierdo
cur.left = helper(oldParent, cur);

Volver cur;
}
}
`` `

*Por qué funciona esto: *
La recursión camina **up** el árbol de la hoja a la raíz original.
A cada paso:

1. Almacena al padre original (`oldParent`).
2. Hace `nuevoParent` el padre del nodo actual.
3. Elimina el vínculo de nuevo con el padre viejo para prevenir ciclos.
4. Swaps izquierda → derecha (si está presente).
5. Recusar, haciendo al padre el nuevo hijo izquierdo.

El caso base es cuando el nodo actual es la raíz original – la recursión se detiene y la nueva raíz se devuelve.

-...

## 2. Solución de pitón

``python
Definición para un nodo de árbol binario con puntero padre.
Clase Nodo:
def __init__(self, val: int, left=None, right=None, parent=None):
self.val = val
autoizquierda
self.right = right
self.parent = parent

Solución de clase:
def flipBinary Tree(self, root: 'Node', leaf: 'Node') 'Node':
self.original_root = root
volver a sí mismo.

def _dfs(self, cur: 'Node', new_parent: 'Node') - título 'Node':
old_parent = curro.parent
cur.parent = new_parent

# Desconectar el viejo enlace si todavía apunta a new_parent
si cur.left es nuevo_parent:
cur.left = Ninguno
si cur.right es nuevo_parent:
cur.right = Ninguno

si el cur es auto.original_root:
Retorno

si cur.left:
cur.right = cur.left

cur.left = self._dfs(old_parent, cur)
Retorno
`` `

*La misma lógica como Java, adaptada al estilo Python. *
Todos los punteros son referencias, por lo que `es` debe ser utilizado para controles de identidad.

-...

## 3. Solución C++

``cpp
Definición para un Nodo. */
Clase Node {}
public:
int val;
Nodo* izquierdo;
Nodo* derecho;
Nodo* padre;
Nodo(int _val) : val(_val), left(nullptr), right(nullptr), parent(nullptr) {}
};

Clase Solución {
public:
Nodo* flipBinaryTree(Nodo* root, Node* leaf) {
original Root = root;
dfs (página, nullptr); // hoja se convierte en nueva raíz
}

privado:
Nodo* originalRoot;

Nodo* dfs(Nodo* cur, Nodo* newParent) {
Nodo* viejoParent = cur-ñuelo;
cur- patrono = nuevoParent;

// Desconectar el enlace de regreso a los padres viejos
si (cur- títuloleft == newParent) cur- títuloleft = nullptr;
si (cur-correcto == nuevoParent) cur- correctamente = nullptr;

si (cur == originalRoot) retorno cur;

si (cur- títuloleft) cur-ienteright = cur- títuloleft; // izquierda se convierte a la derecha

cur- título = dfs(oldParent, cur); // padre viejo se convierte en niño izquierdo
Volver cur;
}
};
`` `

C++ utiliza punteros crudos; se aplica la misma lógica puntero-manipulación.

-...

## 4. Artículo del Blog: *El Bien, el Mal, y el Ugly of “Change the Root of a Binary Tree”*

■ **SEO palabras clave:** Cambiar la raíz de un árbol binario, LeetCode 1666, rerooting de árboles binarios, manipulación puntero, DFS, consejos de entrevista, entrevista de trabajo, Java, Python, C++

-...

### 1. Introducción

Los árboles binarios son el pan-y-butter de muchas preguntas de entrevista, pero el problema *rerooting* (LeetCode 1666) lanza un giro: usted debe **cambiar la raíz** de un árbol **en lugar**, actualizando tanto los vínculos de los niños como los punteros 'padre'. Es una prueba perfecta de:

- Comprensión de la traversal de árboles
- Capacidad para razonar sobre manipulación puntero
- Diseño recursivo limpio

Ya sea que se esté preparando para una entrevista de codificación o puliendo su caja de herramientas algorítmica, este problema es una mina de oro.

-...

### 2. Recaptación de problemas

Se le da un nodo raíz `root ' y un nodo hoja `leaf`. El árbol tiene el habitual `val ' , `izquierda ' , `derecha ' campos ** más** un `padre ' puntero.
Objetivo: Realizar la nueva raíz y ajustar todos los nodos en el camino desde la hoja hasta la vieja raíz para que:

- El niño izquierdo (si existe) se convierte en el niño derecho.
- El padre original se convierte en el hijo izquierdo.
- Todos los punteros " padres " se actualizan en consecuencia.

Si se olvida de ajustar un enlace padre, el árbol contendrá un ciclo y obtendrá “Respuesta incorrecta”.

-...

### 3. El “bien” – Por qué Este es un problema hermoso

Por qué es genial
Silencio...
Silencio **Código mínimo, gran impacto** Silencio Un ayudante recursivo de ~20 líneas mueve todo el árbol. Silencio
Silencio **Clear Base‐Caso** Silencio La recursión se detiene naturalmente cuando se alcanza la raíz original. Silencio
Silencio **No hay espacio extra** Silencio Todos los cambios están en su lugar; no se requieren estructuras auxiliares de datos. Silencio
tención **Language‐agnostic** TEN La lógica central es idéntica en Java, Python y C++. Silencio
Silencio **Insight into Parent Pointers** Silencio Muestra cómo los enlaces “parentes” pueden ser tratados como el siguiente puntero de una lista enlazada, dando una nueva perspectiva sobre la traversal de árboles. Silencio

-...

### 4. El “Bad” – Pitfalls comunes

Pitfall tóxico Cómo evitarlo
Silencio...
Silencio ** Formación Ciclo** Silencio Siempre ** Desconectar** al padre anterior antes de asignarlo como nuevo niño (`si (cur.left == newParent) cur.left = null;`). Silencio
Silencio **Caso de base incorrecto** Silencio Si te detienes en la hoja en lugar de la raíz original, perderás la parte superior del árbol. Silencio
Silencioso **Mising `parent` Actualizaciones** latitud Olvidar establecer `cur.parent = newParent` dejará punteros colgantes. Silencio
Silencio ** Comparaciones de valor** Silencio En los idiomas con referencias de objetos, compare por identidad (`es` en Python, `=` para punteros en C++). Silencio
Silencio **Desbordamiento de los árboles profundos** Silencio Con hasta 100 nodos esto no es un problema real, pero siempre sea consciente de la profundidad de recursión para mayores insumos. Silencio

-...

### 5. Los escenarios “Ugly” – menos estrechos

Escenario Silencioso Por qué se pone Ugly
Silencio...
Silencio **Tree with Multiple Leaves** Silencio Debes asegurarte de que hayas pasado la hoja *exact* que tienes la intención de hacer la nueva raíz. Silencio
Silencio ** Ciclos preexistentes** Silencio Si el árbol de entrada está malformado (al igual que en LeetCode), el algoritmo todavía atravesará hasta que golpee un lazo. Silencio
Silencio **Memory‐Leak in C+** Silencio Si los nodos se asignan en el montón y usted no maneja la propiedad, usted podría filtrar la memoria. Silencio
Silencio ** Árboles desequilibrados** Silencio En árboles muy segados, la profundidad de recursión es igual a la altura del árbol; todavía aceptable aquí pero vale la pena notar. Silencio
Silencio **Puntos de Padre No Establecer Inicialmente** Silencio Algunos problemas pueden omitir 'padre'. En ese caso, usted necesitaría pre-computar los punteros padres antes de rerooting. Silencio

-...

### 6. Step‐by‐Step Walk‐Through

Vamos a rastrear el algoritmo en un pequeño ejemplo:

`` `
3
/ \
5 1
/ \ / \
6 2 0 8
\ /
7 4
`` `

" Ho = 7 " .
Comenzamos en 7 → padre viejo 2 → nuevo padre `null` (ya que 7 es nueva raíz).

- 7's `parent` = `null`.
- El niño izquierdo de 7 es nulo, el niño derecho es nulo.
- 7's left stays `null`.
- 7’s right stays `null`.

Recuperar hasta 2:

- El padre de 2 = 5, nuevo padre = 7.
- El niño izquierdo de 2 se convierte en el niño izquierdo de 5? No: 2’s izquierda es 4 → se convierte en niño derecho.
- 2 se convierte en resultado de recursión (`7`).
- Actualizar punteros en consecuencia.

Continuar hasta 3. El árbol final coincide con la salida LeetCode.

-...

### 7. Análisis de la complejidad

TEN TERMIN TENIDO Tiempo ANTERIENTE Espacio ANTE
Silencio----------Prince------
Silencio **Hora** Silencioso `O(n)` – cada nodo en el camino de la hoja a la raíz se visita una vez. TEN ANTE
Silencio **Auxiliary Space** Silencioso `O(1)` – actualizaciones en el lugar. Silencio
Silencio **Estadio recursivo** Silencioso `O(h)` – altura del árbol (≤ 100 para este problema). Silencio

-...

### 8. Entrevista-Consejos amigos

1. **Explica tu intuición primero** – tratar el camino de la hoja a la raíz como una lista vinculada donde el puntero 'parente' es el enlace "nexto".
2. **Sketch the pointer changes** on a whiteboard or paper; many candidates skip the step that disconnects the old parent, leading to sutil bugs.
3. **Mostrar el caso base** claramente: cuando golpeó la raíz original, deje de repetirse.
4. ** Casos del borde de la mención** tales como árboles escarpados o una hoja que es la raíz misma (aunque LeetCode garantiza al menos dos nodos).
5. **Declara la complejidad** en el frente; los entrevistadores aprecian un gran conciso O explicación.

-...

### 9. Conclusión

LeetCode 1666 es engañosamente simple pero rico con oportunidades de aprendizaje.
Al dominar la manipulación de punteros en árboles, no solo estás resolviendo un solo problema, estás afilando un conjunto de habilidades que se aplica a:

- algoritmos basados en el camino (por ejemplo, el Ancestro Común más bajo con punteros padres)
- Tareas de reestructuración de árboles en el código de producción
- Implementación de estructuras de datos avanzadas como Link‐ Árboles cortados

Utilice las soluciones de Java, Python y C++ como referencia de aplicación para ir a la aplicación, y mantenga la lista de verificación “Good, Bad, Ugly” útil para futuras entrevistas.

Buena suerte, y feliz codificación!

-...

■ *Ready to ace your next coding interview? *
■ Practique LeetCode 1666 y agréguelo a su conjunto de habilidades de “manipulación de árboles en el lugar”. El problema puede ser pequeño en tamaño, pero los conceptos que aprendes son enormes.

-...

*End of article. *

-...

Esto completa la respuesta completa y lista para la producción: código en tres idiomas, una explicación sólida y un artículo fácil de entrevista. ¡Feliz entrevista!