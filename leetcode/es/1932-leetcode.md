-...
Título: LeetCode 1932. Merge BSTs to Create Single BST -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1932 – Combinar BSTs para crear un solo BST
**Hard ← Hash‐Map ← DFS

-...

## TL;DR
- Encuentra la raíz “verdadera” – el árbol cuyo valor raíz nunca aparece como un niño en cualquier otro árbol.
- Almacene todos los árboles en un hash-map (`rootValue → TreeNode`).
- Camina con recorte de la verdadera raíz y reemplaza cualquier hoja cuyo valor coincide con una clave en el mapa con el subárbol entero correspondiente.
- Después de la caminata, si más de un árbol permanece en el mapa → **imposible**.
- Validar el árbol fusionado con una traversal en orden – los valores deben estar aumentando estrictamente.
- Si es válido, devuelve la raíz fusionada; de lo contrario, devuelve `null`.

El algoritmo funciona en **O(n)** tiempo (n = número de árboles) y utiliza **O(n)** espacio adicional para el mapa y la pila de recursión.

-...

## Full Code (Java, Pitón, C++)

■ **Consejo:** La definición de `TreeNode` es la misma en todos los tres idiomas – sólo la sintaxis cambia.

## Java

``java
*
* Definición para un nodo de árbol binario.
* clase pública TreeNode {
* int val;
* TreeNode left;
* TreeNode right;
* TreeNode() {}
* TreeNode(int val) { this.val = val; }
* TreeNode(int val, TreeNode left, TreeNode right) {
* this.val = val;
* this.left = left;
* this.right = right;
*
*
*/
Clase Solución {
public TreeNode canMerge(Lista seleccionadaTreeNode títulos) {}
si (trees.size() == 1) devolver árboles.get(0);

// 1. Construir hash‐map: root value - TreeNode
Mapa seleccionadoInteger, TreeNode titulada map = nuevo HashMap Quería();
para (TreeNode t : árboles) mapa.put(t.val, t);

// 2. Encontrar la raíz real - el cuyo valor nunca es un niño
Establecer contactoInteger hijos = nuevo HashSet correspondió();
para (TreeNode t : árboles) {}
si (t.left != null) niños.add(t.left.val);
si (t.right != null) niños.add(t.right.val);
}

TreeNode root = null;
para (TreeNode t : árboles) {}
si (!children.contains(t.val)) {}
si (root != null) devuelve null; // múltiples candidatos → imposible
raíz = t;
}
}
si (root == null) regresa null; // no root found

// 3. Combinación recursiva
merge(root, map);

// 4. Todos los árboles deben fundirse
si (map.size() 1) retorno nulo;

// 5. Validación de la propiedad BST
Lista realizadaInteger confianza inorder = nuevo ArrayList fiel();
inorderTraversal(root, inorder);
para (int i = 1; i) ++i) {
si (inorder.get(i) <= inorder.get(i - 1)) regresa null;
}

raíz de retorno;
}

merge de vacío privado(TreeNode node, Mapa seleccionadoInteger, TreeNode título) {
si (nodo == nulo) regresa;

si (node.left != null ' mapa.containsKey(node.left.val)) {}
node.left = map.remove(node.left.val);
merge(node.left, map);
}
si (node.right != null ' mapa.containsKey(node.right.val)) {}
node.right = map.remove(node.right.val);
merge(node.right, map);
}
}

de vacío privado Traversal(TreeNode node, Listo)Integer confianza res) {
si (nodo == nulo) regresa;
inorderTraversal(node.left, res);
res.add(node.val);
inorderTraversal(node.right, res);
}
}
`` `

-...

## Python

``python
Definición para un nodo de árbol binario.
Clase TreeNode:
def __init__(self, val=0, left=None, right=None):
self.val = val
autoizquierda
self.right = right

Solución de clase:
def canMerge(self, trees: List[TreeNode]) - Propiedad opcional[TreeNode]:
si len(trees) == 1:
árboles de retorno[0]

# Map root value - título TreeNode
árbol_map = {t.val: t para t en árboles}

# Collect all child values
niños = set()
para t en los árboles:
si t.left:
niños.add(t.left.val)
Si T.right:
niños.add(t.right.val)

# Encontrar la raíz única
raíces = [t para t en árboles si t.val no en niños]
si len(roots) != 1:
No.
root = roots[0]

# Recursive merge
def merge(nodo: TreeNode):
si el nodo es Ninguno:
Regreso
si node.left y nodo. izquierda.val en árbol_map:
node.left = tree_map.pop(node.left.val)
merge(node.left)
si node.derecha y nodo. derecha.val en árbol_map:
node.right = tree_map.pop(node.right.val)
merge(node.right)

merge(root)

# Todos los árboles deben ser fusionados
si árbol_map:
No.

Validar BST por inorden
inorden = []
def dfs(nodo: TreeNode):
si el nodo es Ninguno:
Regreso
dfs(node.left)
inorder.append(node.val)
dfs(node.right)

dfs(root)
si cualquier(inorder[i] <= inorder[i-1] for i in range(1, len(inorder))):
No.

raíz de retorno
`` `

-...

### C++

``cpp
*
* Definición para un nodo de árbol binario.
* struct TreeNode {
* int val;
* TreeNode *left;
* TreeNode *right;
* TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
* };
*/
Clase Solución {
public:
TreeNode* canMerge(vector seleccionadoTreeNode* curva árboles) {}
si (trees.size() == 1) devolver árboles[0];

// Valor de la raíz de mapa - TreeNode
unordered_map madeint, TreeNode*
para (auto t : árboles) mp[t- Confval] = t;

// Recopilar valores infantiles
unordered_set obtenidos injerto;
para (auto t : árboles) {}
si (t- títuloleft) niño.insert(t- títuloleft- títuloval);
(t- tituladoright) child.insert(t- tituladoright- Confval);
}

// Encontrar la raíz única
TreeNode* root = nullptr;
para (auto t : árboles) {}
(niño.find(t- títuloval) == child.end()) {
(root) return nullptr; // more than one candidate
raíz = t;
}
}
si (!root) regresa nullptr;

// Merge Recursive
función recomendadavoid(TreeNode*) título merge = [ curva](TreeNode* node) {
si (!node) regresa;
si (nodo- confíaleft " cl.count(node- títuloleft- títuloval)) {
node- títuloleft = mp[node- títuloleft- títuloval];
mp.erase(node- Confleft-Conval);
merge(node-consejoft);
}
si (node- confíaright " ritmo mp.count(node- tituladoright- confianzaval) {
node- tituladoright = mp[node-title-
mp.erase(node- Confright-Conval);
merge(node-ienteright);
}
};
merge(root);

// Todos los árboles deben ser fusionados
si (!mp.empty()) regreso nullptr;

// Validar BST por inorden
vector inorden;
función recomendadavoid(TreeNode*) título dfs = [ cl](TreeNode* node) {
si (!node) regresa;
dfs(node-propleft);
inorder.push_back(node-conval);
dfs(node-ienteright);
};
dfs(root);

para (size_t i = 1; i) ++i)
si (inorden[i] <= inorder[i-1]) devuelve nullptr;

raíz de retorno;
}
};
`` `

-...

## Blog Post (SEO‐Optimized)

■ **Título:** *De “Merge” a “Master” – Solving LeetCode 1932 (Merge BSTs) y Boosting Your Data‐Structure Skills*

-...

### 1. Introducción

Cuando se está preparando para una entrevista de ingeniería de software senior, es raro que se le pida que resuelva un problema que combina *hash-maps*, *repetición de árbol* y * validación de BST* de inmediato. LeetCode **1932 – Merge BSTs to Create a Single BST** es una de esas gemas ocultas. Es marcado “Hard” por una razón: las limitaciones (5 × 104 árboles, cada uno con ≤ 3 nodos) exigen una solución lineal que también es fácil de razonar.

En este post caminaremos:

Silencio Palabra clave Silencio Por qué importa Silencio
Silencio...
Silencio `merge bst` ← Concepto básico del problema
Silencio `hash mapa` Silencio O(1) lookup is critical Silencio
Silencioso `dfs` ¦ Depth‐first traversal to pega arboles
Silencio `validación inordenada` Silencio Forma rápida de probar la propiedad BST
Silencio `tiempo complejidad O(n)` Silencio Los entrevistadores aman soluciones lineales

-...

### 2. Sinopsis de problemas

■ ** Objetivo**: Combine una lista de pequeños árboles binarios en **uno** árbol de búsqueda binaria (BST), o determine que es imposible.

**Input**
- `trees`: lista de punteros TreeNode.
- El valor raíz de cada árbol es único.
- Cada árbol tiene como máximo 3 nodos (raíz + 0/1/2 niños).

**Operaciones permitidas* *
- Escoge un árbol como la raíz verdadera (la que nunca aparece como un niño).
- Si el valor de una hoja coincide con el valor raíz de otro árbol, sustituya esa hoja con el subárbol *entire*.
- Cada árbol se puede utilizar al máximo una vez.

Retorno**
- La raíz fusionada si se puede formar un solo BST válido, de lo contrario `null` (o `None` / `nullptr`).

-...

### 3. Principales desafíos

← Reto Silencio Por qué es complicado
Silencio...
Silencio Identificar la raíz *real* tención Un enfoque ingenuo podría mal-pick un subárbol como la raíz. Silencio
← Evitar “doble-merge” Silencio Una hoja podría coincidir con varios subárboles si la entrada es malformada. Silencio
← Examinar eficientemente ← Repetidamente buscar el valor de un niño en un array sería O(n2). Silencio
Silencio Validación de la propiedad BST después de fusionarse Silencio Un árbol podría verse bien estructuralmente pero violar la regla del pedido. Silencio

-...

### 4. Enfoque (Step‐by‐Step)

1. **Hash‐Map Construction**
Mapa de cada valor raíz a su TreeNode (`rootValue → node`).
*¿Por qué?* Permite que el tiempo constante “es un subárbol?” cheques durante la fusión.

2. **Encontrar la raíz verdadera**
- Reunir todos los valores infantiles en un conjunto.
- Escanear todos los árboles; el que cuyo valor raíz es *no* en el conjunto del niño es la raíz real.
- Si hay más de un candidato o ninguno, fusionarse es imposible.

3. **Recursive Merge* *
Partiendo de la verdadera raíz, atraviesa el árbol.
Cada vez que encuentres una hoja cuyo valor existe en el mapa, reemplaza esa hoja con el subárbol mapeado y retira la entrada del mapa.
Recusarse en el subárbol recién insertado.

4. # Comprobación completa #
Después de la traversal, el mapa debe contener sólo la verdadera raíz. Si algún árbol permanece → imposible.

5. *Validar BST*
Realizar un traversal en orden para recoger valores de nodo.
Si la lista no aumenta estrictamente → el árbol fusionado viola las reglas BST → devolver `null`.

-...

### 5. Aspectos destacados de la aplicación

Silencio Idioma Silencio Notas Especiales
Silencio...
Silencio **Java** Silencio Usos `Lista realizadoTreeNode confianza` de LeetCode; la profundidad de recursión es segura (≤ 3 × 5 000). Silencio
Silencio **Python** Silencio Usos diccionario (`{}`) y conjunto (`set()`) - rápido O(1) operaciones. Silencio
Silencio **C+** Silencio Usos `unordered_map` y `unordered_set`; recursión de lambda con `std::function`. Silencio

-...

### 6. Complejidad del tiempo y el espacio

TEN TER TER TER ANTE Fórmula ANTERI ANTE
Silencio--------------------------------
Silencio **Hora** Silencio **O(n)** Silencio Cada árbol se procesa un número constante de veces (construcción, detección de raíces, fusión, validación). Silencio
Silencio **Espacio** Silencio **O(n)** Silencio El hash‐map almacena una entrada por árbol; profundidad de la pila de recursión ≤ 3. Silencio

-...

### 7. Casos de borde cubiertos

- **Multiple verdaderas raíces** → imposible.
- **Ninguna verdadera raíz** → imposible.
- ** Árboles inmersos dejados** → imposible.
- **En orden no aumenta estrictamente** → inválido BST.
- **Introducción del árbol del sonido** → trivialmente devuelto.

-...

### 8. “Bueno, malo” – Pitfallas comunes

Silencio Fase ANTE ANTE ANTE ANTERIOR ANTERIOR ANTERIOR
Silencio----------Prince------
Silencio **Error/NullPointer Silencio Usar una lista y una búsqueda lineal → O(n2) Silencioso
Silencio **Detección de la raíz** Silencio Conjunto de paso único de niños ← Múltiples candidatos → aceptar silencio (bug) Silencio Contemplando que la raíz podría ser *leaf* sólo (árbol vacío)
Silencio **Merging** tención Recuperar ligeramente pop de mapa ← No eliminar las teclas usadas → recursión infinita Silencio Modificar la estructura original de los árboles de entrada en su lugar (side-effects)
Silencio **Validación** Silencio In‐order traversal Silencio Comparando los valores iguales incorrectamente ( ``conejo=` en lugar de `conejo`) Silencioso Olvidar atravesar *todos* nodos (despertando a un niño nulo)

-...

### 9. Estrategia de prueba

1. ** Casos de éxito básico**
- Dos árboles donde uno es un niño directo.
- Tres árboles formando un BST perfecto.

2. **Failure due to multiple roots**
- Dos árboles independientes (sin vínculo infantil).

3. **Failure due to leftover trees**
- Una hoja que no coincide con ninguna otra raíz.

4. **Failure due to BST violation* *
- Merge produce un árbol donde el hijo izquierdo padre.

5. **Large input**
- 5 × 104 árboles, cada uno con 3 nodos – verificar tiempo de ejecución 1 s.

-...

### 10. SEO & Career Advice

Silencio Palabra clave Silencio
Silencio...
TENIDO “Merge BSTs” TENIDO Título, primer párrafo, H2 encabezados TENIDO
← “LeetCode 1932” Silencio Meta descripción, primera línea
TENIDO “Hard BST problem” TENIDO H3 headings ANTE
Silencio “Entrevista de datos‐estructuración”
← “Solución Java/Python/C++”

**Por qué esto importa para su carrera:**
- Mastering hash‐maps and tree recursion demonstrates deep data‐structure knowledge – a hallmark of senior‐level roles.
- Los problemas “difíciles” de LeetCode son la fuente de interés tecnológico en Google, Amazon y las compañías de nivel FAANG.
- Una solución limpia y bien comunicada muestra profesionalidad y legibilidad de códigos.

-...

Conclusión

Solución **LeetCode 1932 – Combinar BSTs para Crear un BST Único** es una gran manera de afilar su intuición hash‐map, practicar DFS y reforzar técnicas de validación BST. El algoritmo lineal anterior es elegante y eficiente, lo que lo convierte en un punto de conversación sólido en su próxima entrevista.

Si usted ya ha clavado este problema, considere la práctica de problemas relacionados:
- 2105. Reemplazar todos los dígitos con el Suma de los subconjuntos de dígitos** (la fusión de árboles similares).
**1307. Verbal Arithmetic Puzzle** (hash‐map + backtracking).

¡Feliz codificación y buena suerte en su viaje de entrevista!