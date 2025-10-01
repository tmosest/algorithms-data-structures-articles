-...
Título: LeetCode 428. Serialize and Deserialize N-ary Tree -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 428. Serialize y Deserialize N‐ary Tree
■ **LeetCode Hard ← Job‐Entreview‐ Listo.

-...

### 1. 🚀 Resumen del problema

En un árbol N-ary arraigado cada nodo puede tener un número arbitrario de niños (hasta **N**).
La tarea es **convertir todo el árbol en una cuerda** (`serialize`) y luego **reconstruir el mismo árbol exacto de esa cuerda** (`deserializar`).

- ** Entrada**: `root ' - pointer/reference to the root of an N‐ary tree (may be `null`).
- ¿Qué?
* `serialize(root)` → `String` que representa singularmente el árbol.
* `deserialize(data)` → `Nodo` que es bit‐for‐bit idéntico al árbol original.

** Limitaciones importantes**

TEN ANTERIOR ANTERIOR ANTERIOR
Silencio...
Silencioso *Nodos* Silencio
* Rango de valor* ← nodo.val ≤ 109` Silencio
Silencio *Ningún estado global/estático* Silencioso cada llamada debe ser **sin estado**. Silencio
Silencio *Hora* Silencio Linear en el número de nodos. Silencio
*Espacio* Silencioso O(número de nodos) para la cadena de salida. Silencio

-...

### 2. Por qué este problema importa

* **Interview staple** – Muchos entrevistadores de alto nivel piden un truco de “serializar/deserializar” para árboles, listas vinculadas, gráficos, etc.
* **LeetCode 428** es parte de las colecciones “Arbol Benario” y “Design” y aparece en el set “Graph/Tree”.
* Dominar este problema demuestra una comprensión sólida de la recursión, las técnicas de traversal y la cuidadosa manipulación de cuerdas, todas las habilidades básicas para los roles centrados en algoritmos (Software Engineer, Backend Engineer, Data Engineer, etc.).

-...

#### 2down⃣ Solution Strategies

A continuación se muestran los **tres patrones más comunes** que verá en las soluciones de entrevistas de producción:

Silencio Lo que hace ¦
Silencio----------------------------...
Silencio **Depth‐First Search (DFS) with child count**  durable `val childCount ■children‐DFS confianza` Silencio *Simple, no extra sentinel symbol.* ← Requiere cuidadoso manejo de índice cuando se analiza. Silencio
Silencio **Breadth‐First Search (BFS) with sentinel nulls** Silencio `val child1 child2 ... null ...` Silencioso *Iterante, fácil de entender.* Debe recordar dónde termina cada lista de niños. Silencio
* Formato personalizado con delimitadores** Silencio `1 tuviendo3 turbado2 turbado0...` Silencio *Muy compacto, no hay espacios necesarios.* Silencio Más error-prone para mayores valores; difícil de depurar. Silencio

A continuación implementamos el patrón **DFS + cuenta infantil** en **Java, Python y C+** – la manera más limpia, más rápida y segura de cumplir con las limitaciones del problema.

-...

## 💻 3‐Language Implementations

■ **Los tres códigos son apátridas, espacio auxiliar O(1) (excepto la pila de recursión), y garantizado para reconstruir el mismo árbol. #

## 3.1 Solución Java

``java
importar java.util*;

// LeetCode Node definition
Clase Node {}
int val;
public List Node confía children;

public Node() { this.children = new ArrayList fiel(); }

public Node(int val) {
este.val = val;
esto. niños = nuevo ArrayList garantizado();
}

public Node(int val, Lista de niños Node confianza) {}
este.val = val;
esto. niños = niños;
}
}

Clase Codec {}

/** Encodes an N‐ary tree to a single string. */
public String serialize(Node root) {
si (root == null) regresan "; // árbol null → cuerda vacía
StringBuilder sb = nuevo StringBuilder();
dfsEncode(root, sb);
devolver sb.toString();
}

vacío privado dfsEncode(Nodo, StringBuilder sb) {
sb.append(node.val).append(') // valor de nodo
sb.append(node.children.size()).append(')); // number of children
para (Niño nodo: nodos.niños) {}
dfsEncode(child, sb); // recurrentemente codifica cada niño
}
}

* Decodifica tus datos codificados al árbol. */
public Node deserialize(String data) {
si (data.isEmpty()) devuelve null; // cadena vacía → árbol null
Compartir[] fichas = data.split("\s+");
int[] index = {0}; //
dfsDecode(tokens, index);
}

privado Nodo dfsDecode(String[] tokens, int[] index) {
int val = Integer.parseInt(tokens[index[0]++]); // read node value
niño Cuenta = Integer.parseInt(tokens[index[0]++]); // read child count
Nodo nodo = nuevo Nodo(val);
node.children = nuevo ArrayList recomendado();
para (int i = 0; i) {}
node.children.add(dfsDecode(tokens, index));
}
nodo de retorno;
}
}
`` `

■ *La complejidad*
■ *Tiempo*: `O(N)` – cada nodo se visita una vez durante ambos serializar " deserializar.
■ *Espacio*: `O(N)` – longitud de cadena de salida más pila de recursión.

-...

### 3.2 Python Solution

``python
# Definición de nodo (formato LeetCode)
Clase Nodo:
def __init__(self, val=None, children=None):
self.val = val
niños = niños o []

class Codec:
""Encodes an N‐ary tree to a string and decodes it back.""

def serialize(self, root: 'Node') - universidad str:
si no raíz:
Retorno '
partes = []
def dfs(node):
parts.append(str(node.val)))
partes.append(str(len(node.children))))
para niños en nodo. niños:
dfs(child)
dfs(root)
volver '.join(partes)

def deserialize(self, data: str) - 'Node':
si no datos:
No.
tokens = data.split()
idx = 0
def dfs():
idx no local
val = int(tokens[idx]); idx += 1
child_cnt = int(tokens[idx]); idx += 1
nodo = Nodo(val)
node.children = [dfs() for _ in range(child_cnt)]
Nodo de retorno
retorno dfs()
`` `

■ **La complejidad** – idéntica a la solución Java.

-...

### 3.3 C++ Solución

``cpp
#include יbits/stdc++.h
usando std namespace;

// LeetCode Node definition
struct Node {}
int val;
vector Node* niños;
Nodo(int _val) : val(_val) {}
Nodo(int _val, const vector efectuadoNode* implicado _children) : val(_val), children(_children) {}
};

Clase Codec {}
public:
// Serializar el árbol N-ary a una cuerda
string serialize(Node* root) {
si (!root) regresan ";
stringstream ss;
dfsEncode(root, ss);
retorno ss.str(); // contiene espacio de seguimiento – inofensivo
}

// Deserializar la cuerda de vuelta a un árbol N-ary
Nodo* deserialize(resultados de cadena restante) {
(data.empty())) return nullptr;
stringstream ss(data);
devolver dfsDecode(ss);
}

privado:
vacio dfsEncode(Nodo* nodo, stringstream &s) {
ss.
para (Número*: nodo-clientes)
dfsEncode(child, ss);
}

Nodo* dfsDecode(stringstream &s) {
int val, childCnt;
ss , título val ChildCnt;
Nodo* = Nodo(val);
node- títulochildren.resize(childCnt);
para (int i = 0; i)
node-clientes[i] = dfsDecode(ss);
nodo de retorno;
}
};
`` `

■ ** Complejidad** - las mismas características del espacio tiempo de `O(N).

-...

## 📚 Blog Article – “Serialize " Deserialize N‐ary Tree: The Complete Guide "

-...

### **Title (SEO‐Optimized)* *
■ **LeetCode 428 – Serialize " Deserialize " N‐ary Tree ← Solución paso a paso Consejos* *

-...

### **Meta Descripción**
■ “¿Quieres ace el duro problema de LeetCode #428? Aprende cómo serializar y deserializar un árbol N‐ary, entender los patrones DFS vs BFS, y obtener información de entrevistas de trabajo. ”

-...

### **Tabla de contenidos**

1. [Problema instantánea](#problema-snapshot)
2. [Por qué importa](#why-it-matters)
3. [Key Constraints & Edge Cases](#key-constraints)
4. [Solution Overview](#solution-overview)
5. [DFS + Child Count – The Classic Pattern](#dfs-child-count)
6. [BFS + Null Sentinel – An Alternative](#bfs-sentinel)
7. [Code Walk‐Through (Java / Python / C++)](#code-walk-through)
8. [Complexity " Pitfalls](#complexity-pitfalls)
9. [Entreview‐Ready Tips](#interview-tips)
10. [Pensamientos Finales > Pasos Siguientes] (Pensamientos finales)

-...

##### **1vers⃣ Problem Snapshot** Se hizo un nombre="problema-snapshot"

■ **LeetCode #428 – Serialize and Deserialize N‐ary Tree**
■ Dificultad: **Hard**
■ Plazo: 1 s viv límite de memoria: 512 MB

■ *Dada una referencia a la raíz de un árbol N‐ary, escriba dos funciones que: *

Silencio Silencio .
Silencio...
Silencio `serialize(root)` Silencio Convierte todo el árbol en una cuerda. Silencio
Silencio `deserializar(data)` Silencio Recrear el árbol original de esa cuerda. Silencio

■ *La salida de `deserialize(serialize(root)' debe ser **bit‐for‐bit idéntica** al árbol original. *

-...

##### **2vides⃣ ¿Por qué importa ? ? ?

- **Core Data‐Structure Skill** – Los árboles son ubiquitos (sistemas de ficheros, pares JSON, organigramas).
- **Entrevista Gold‐mine** – Muchas entrevistas de alto nivel piden “serializar/deserializar” para probar la recursión, el traversal y la gestión estatal.
**Real‐World Relevance** – Las bases de datos de gráficos y los sistemas distribuidos necesitan una serialización eficiente para el transporte de redes o la persistencia.

-...

### **3️ Key Constraints " Edge Cases** sa name= "key-constraints"

Silencio Caso Edge Silencioso Qué ver para Silencio
Silencio...
Árbol vacío (`root == null`) Vuelva una cuerda vacía. Silencio
Silencio Árbol de nodo único ← Debe serializarse como `valor 0 ` (0 niños). Silencio
Silencio Árbol profundo ( profundidad = 104) Silencio Profundidad de recuperación → considerar la recursión de la cola o BFS iterativa si los límites de la pila de lenguaje son una preocupación. Silencio
Silencio Grandes valores de nodo (`≤ 109`) tención Evite delimitadores de caracteres individuales que podrían chocar con dígitos. Use espacios o un separador no numérico. Silencio

■ *Recordar: No hay variables globales/estáticas – cada llamada debe ser autocontenida. *

-...

#### **3flexiones sobre la Solución Resumen**

■ **Dos patrones limpios** – DFS (recursivo) y BFS (iterante).

√≥ **DFS + Child Count**
⇩ - codificar como: nodo Val childCnt child1 ... niñoK` recursivamente.
- Muy fácil de analizar usando un puntero índice.

**BFS + Null Sentinel**
√≥n - Codigo nivel por nivel, insertando un centinela (`null`) para marcar el final de una lista de niños.
> - Iterative, no index pointer needed, pero usted tiene que “conocer” cuando cada sub-lista termina.

■ Ambos patrones logran tiempo lineal y espacio.

-...

############468⃣ Solution Overview**

■ **FDAS + Cuento de Niños** es el ** más común** y recomendado debido a:

1. **Formación mínima** – ningún delimitador especial, solo espacios.
2. **Separación determinística** – siempre se lee un valor, luego el número de niños.
3. **Compact** – la longitud de la cuerda es aproximadamente `2 * number_of_nodes + sum_of_child_counts`.

-...

#### **5️ DFS + Cuento de Niños – El Patrón Clásico** - "dfs-child-count"

#### Algorithm

1. **Serializar (DFS)* *
- Visita al nodo.
- Apéndice `node.val` y `node.children.size()` separados por un espacio.
- Recupere a cada niño.
2. **Deserialize (DFS)* *
- Dividir la cuerda por los espacios → array `tokens`.
- Mantener un índice mutable ( " idx " o una lista de pitones).
- Read `tokens[idx++]` → `val`.
- Lea el siguiente token → `childCount`.
- Crear nodo con 'val'.
- Recusar los tiempos del niño para construir niños.
- Nodo de retorno.

■ *Por qué funciona* El formato es *prefijo* (nodo primero) y cada nodo declara explícitamente cuántos niños siguen, por lo que el analizador nunca identifica los límites.

-...

#### **6vers⃣ BFS + Null Sentinel – An Alternative** ■a name="bfs-sentinel"

Si prefieres una solución **iterative**, puedes codificar nivel por nivel, insertando un 'null' centinela después de cada lista de niños.

``text
[ rootVal, rootChildCnt, child1, child2, ..., null, ... ]
`` `

- Cada uno de ellos le dice al deserializador que la lista de niños actual ha terminado.
√ - Aún es tiempo lineal, pero necesita mantener una cola y seguir posiciones centinelas.
Es ligeramente más verbosa que DFS + cuenta para niños.

-...

### **7️ Code Walk‐Through** ▪ a name="code-walk-through" Login

Hemos proporcionado ** tres implementaciones completas** antes (Java, Python, C++).
Puntos clave para destacar durante una presentación:

* Utilizar **espacios** como delimitadores – sobreviven `split`/`istringstream` parsing.
* Siempre maneje ** árboles vacíos** temprano (retorna o pare una cuerda vacía).
* La profundidad de la recuperación está naturalmente atada por la altura del árbol; porque los árboles muy profundos consideran una versión recursiva de la cola o BFS.

-...

### **8️ Complejidad " Pitfalls** " se hizo un nombre= "complexity-pitfalls"

TENCIÓN DE LA Operación TENIDO Tiempo TENIDO Espacio ANTERIENTE Errores comunes
Silencio...
Silencio `serialize` Silencio `O(N)` Silencio `O(N)` cuerda Silencio Olvidando un espacio después del recuento de niños → parser mis-aligned. Silencio
Silencio `deserializar` Silencio `O(N)` Silencio `O(N)` recursión pila Silencio Usando variables globales (viola la apatridia). Silencio
Silencio Manejando grandes `val`  vidas `O(1)` per node Silencio `O(1)` Silencioso desbordamiento si usted almacena como 'car'. Usa cuerda para evitar. Silencio

■ #Pitfall 1** – ** Index Out-of-Bounds** – Siempre verifique que el array token tiene suficientes elementos antes de acceder.
■ #Pitfall 2** – ** Espacios de navegación** – Algunos idiomas los tratan como fichas vacías; sean consistentes.
■ #Pitfall 3** – **Recursive Stack Overflow** – Para árboles extremadamente arrugados (de profundidad = 104) podrías alcanzar límites de pila en Java/Python; considera aumentar el tamaño de la pila o utilizar BFS.

-...

##### **9️ Interview‐Ready Tips** "trabaja un nombre="interview-tips"

1. **Explicar su formato al frente** – “Voy a usar el DFS con recuento infantil porque...”.
2. **Mostrar los casos de borde** – Árbol vacío, nodo único, grandes valores.
3. **Discusión Complejidad** – Tiempo lineal " espacio; justificar la pila de recursión.
4. **Mención No Global State** – “Cada llamada utiliza sólo variables locales / pila de recursión. ”
5. **Opcional: Agregue Tests de Unidad** – Prueba de ida y vuelta serialización/deserialización rápidamente.

-...

#### **10️ Pensamientos Finales > Próximos Pasos** Se hizo un nombre= "final-thoughts"

* Mastering LeetCode #428 te equipa con una técnica de traversal de árboles ** inversatiles** y muestra tu capacidad de ** estado de código** en una cadena compacta.
* Practicar extendiendo la solución a **N-ary graphs** o ** formatos de serialización de átomos**.
* Añade pruebas de unidad en tu idioma preferido para simular escenarios del mundo real.
* Sigue explorando los problemas de LeetCode *Design* (por ejemplo, `Serialize/Deserialize Binary Search Tree`, `Design Twitter`, etc.) – se aplican los mismos patrones.

-...

■ **Happy Coding** y **Good Luck** en su próxima entrevista de algoritmos! 🚀

-...

### ** Call to Action**

*Si te gustó este post, pulsa el botón **Suscribir**, comenta a continuación con tus propias soluciones o preguntas, y comparte en LinkedIn o Twitter con el hashtag `#LeetCode428`. *

-...

Siguiente Paso Recursos

1. Conjunto de problemas LeetCode: “Árbol interior – serialización”
2. “Recursive vs Iterative Tree Traversal” – Coursera / Udacity.
3. “Serialización de Gráficos” – G4G y Hackerrank desafíos.

-...

■ **End of Article**

-...

#### 📦 4י⃣ Final Wrap‐ Arriba

Ahora tienes:

1. ** Código totalmente funcional y apátridas** en tres idiomas.
2. Un **conciso, explicación de entrevista** de por qué el problema importa.
3. Un **completo blog** que usted puede publicar en Medium, dev.to, o su sitio de cartera personal para demostrar dominio.

Buena suerte aplastando a LeetCode 428 e impresionando a los gerentes de contratación! 🚀