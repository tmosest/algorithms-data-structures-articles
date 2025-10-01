-...
Título: LeetCode 297. Serialize and Deserialize Binary Tree -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Serializar " Deserializar " Árbol binario – Solución en tres idiomas

A continuación se presentan tres implementaciones listas a paso que pasarán LeetCode 297.
Los tres usan la estrategia *pre-orden* (DFS) – visitamos el nodo, luego el subárbol izquierdo, luego el subárbol derecho.
Los nodos 'null` se codifican como la cadena '"null" y se separan por comas.
Durante la deserialización leemos los valores de una lista (o secuencia de cadena) en el mismo orden, reconstruyendo el árbol recursivamente.

-...

#### 1.1 Java

``java
importar java.util*;

// Definición para un nodo de árbol binario.
clase TreeNode
int val;
TreeNode left;
TreeNode right;
TreeNode(int x) { val = x; }
}

clase pública Codec {}

--------- Encode...
public String serialize(TreeNode root) {
StringBuilder sb = nuevo StringBuilder();
buildString(root, sb);
devolver sb.toString();
}

construcción de vacío privadoString(TreeNodo, StringBuilder sb) {
si (nodo == nulo) {
sb.append("null",);
retorno;
}
sb.append(node.val).append(',');
buildString(node.left, sb);
buildString(node.right, sb);
}

--------- Decodificar...
public TreeNode deserialize(String data) {
si (data.isEmpty()) regresa null;
String[] vals = data.split(",");
Queue wonString confía q = new LinkedListiese(Arrays.asList(vals));
(q);
}

árbol privadoNode buildTree(Cuarta seleccionadaString confianza q) {}
String val = q.poll();
si (val.equals("null") devuelve null;
TreeNode node = nuevo TreeNode(Integer.parseInt(val));
node.left = buildTree(q);
node.right = buildTree(q);
nodo de retorno;
}
}
`` `

■ *Testing on LeetCode*
. ``java
■ Codec ser = new Codec();
■ Codec des = new Codec();
■ TreeNode root = nuevo TreeNode(1);
√≥ root.left = new TreeNode(2);
√≥ root.right = nuevo TreeNode(3);
не root.right.left = nuevo TreeNode(4);
не root.right.right = nuevo TreeNode(5);
■ Criar datos = ser.serialize (root);
■ TreeNode copy = des.deserialize(data);
ñ copia ahora representa el árbol original
" `

-...

### 1.2 Python

``python
Definición para un nodo de árbol binario.
Clase TreeNode:
def __init__(self, x):
self.val = x
self.left = Ninguno
self.right = Ninguno

class Codec:
# ------------------ Código - Sí.
def serialize(self, root: TreeNode) - título str:
""Encodes a tree to a single string.""
fuera =
self._dfs(root, out)
volver ','.join(out)

def _dfs(self, node: TreeNode, out: list):
si el nodo es Ninguno:
out.append('null')
Regreso
out.append(str(node.val)))
auto._dfs(node.left, out)
auto._dfs(node.right, out)

# ------------------ Decodificación - Sí.
def deserialize(self, data: str) - TreeNode:
""Decodifica tus datos codificados al árbol.""
si no datos:
No.
vals = data.split(',')
self.idx = 0
volver a sí mismo._build(valos)

def _build(self, vals: list) - título TreeNode:
si vals[self.idx] == 'null':
auto.idx += 1
No.
nodo = TreeNode(int(vals[self.idx]))
auto.idx += 1
node.left = self._build(vals)
node.right = self._build(vals)
Nodo de retorno
`` `

■ **Usuario**
.
√≥ codec = Codec()
árbol = árbol nodo (1)
√rbol.left = TreeNode(2)
árbol.right = TreeNode(3)
Ø serializada = codec.serialize(tree)
> deserialized = codec.deserialize(serialized)
" `

-...

#### 1.3 C++

``cpp
#include ■string
#incluye
#include >

/* Definición para un nodo de árbol binario. */
struct TreeNode {
int val;
TreeNode *left;
TreeNode *right;
TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

Clase Codec {}
public:
--------- Encode...
string serialize(TreeNode* root) {
stringstream ss;
dfs(root, ss);
retorno ss.str();
}

vacío dfs(TreeNode* nodo, stringstream &s) {}
si (!node) {
ss.
retorno;
}
ss.
dfs(node-propleft, ss);
dfs(node-ienteright, ss);
}

--------- Decodificar...
TreeNode* deserialize(resultados de cadena) {
(data.empty())) return nullptr;
queue hacía referencia q;
token de cuerda;
stringstream ss(data);
mientras (obline(ss, token, ',')) {}
q.push(token);
}
(q);
}

TreeNode* buildTree(queue seleccionastring] {
cadena val = q.front(); q.pop();
si (val == "null") de vuelta nullptr;
TreeNode* node = nuevo TreeNode(stoi(val));
nodo- título = buildTree(q);
node-titleright = buildTree(q);
nodo de retorno;
}
};
`` `

■ *Ejemplo*
, ``cpp
■ Codec codec;
■ TreeNode *root = nuevo TreeNode(1);
√≥ root- títuloleft = new TreeNode(2);
нелительных " нелентентеле " , " , " , "
> string s = codec.serialize(root);
■ TreeNode *copy = codec.deserialize(s);
" `

-...

## 2. Artículo del Blog – “Serializar " Deserializar el árbol binario: el bien, el mal y el ugly "

■ **Meta Título**: Serialize " Deserialize " Árbol binario – LeetCode 297 Explicado (Java, Python, C++)
■ **Meta Descripción**: Master LeetCode 297 – serialize " deserialize binario tree. Lea nuestra profunda inmersión, muestras de código en Java, Python, C++ y información de entrevistas.

#### 2.1 Introduction

Al entrevistarse para un rol de ingeniería de software, **LeetCode 297 – Serializar y Deserializar el árbol binario** es una pregunta frecuente. El problema te obliga a pensar en **traversal del árbol**, **manipulación de la cuerda**, y **recusión**— habilidades básicas que los gerentes de contratación les encanta ver.

En este post, vamos a diseccionar el problema, explorar por qué la solución DFS previa es elegante, mostrar código listo a paso en **Java, Python, y C+**, y luego hablar de los aspectos **bueno**, **bad**, y **en términos generales** que los entrevistadores suelen sondear.

■ **Keywords**: serializar el árbol binario, deserializar el árbol binario, LeetCode 297, DFS, traversal pre-orden, prep entrevista, entrevista de codificación, serialización de árboles binarios, Java, Python, C++.

-...

### 2.2 Problema Recap

■ **Given** un árbol binario, *serialize* en una cuerda para que pueda ser transmitido o almacenado.
■ **Given** la cuerda, *deserializar* de nuevo en la estructura original del árbol.

**Constraints* *

* 0 ≤ nodos ≤ 104
* Valores de los nodos

La serialización canónica LeetCode usa comas y la palabra "null" para niños vacíos. Pero el problema permite explícitamente *cualquier* formato de serialización que sea invertible. Esto nos da libertad creativa.

-...

### 2.3 Why Pre‐Order DFS Works So Well

1. **Determinista** – El orden “nodo, izquierda, derecho” garantiza que durante la desintegración siempre sabemos si estamos creando un niño izquierdo o derecho.
2. **Recuperación simple** – Un único ayudante recursivo construye la cuerda; otro ayudante consume la lista para reconstruir el árbol.
3. **Linear Time & Space** – Cada nodo se procesa exactamente una vez; la longitud de cadena resultante es O(n).

##### 2.3.1 Handling `null `

Usar la señal "null" para los niños ausentes es crucial. Sin ella, el algoritmo sería ambiguo: dado `1,2,3`, es el árbol:

`` `
1
/
2
\
3
`` `

o

`` `
1
\
2
\
3
`` `

El "null" tokens break the ambiguity:

`` `
1,2,null,3,null,null,null
`` `

Ahora la estructura es única.

-...

### 2.4 El Código – Un avance rápido

Silencio Idioma TENIDO Pasos principales Silencio Silencio
Silencio----------------------------
Silencio **Java** Silencioso `StringBuilder` + recursión para `serialize`; `Cuestión recomendadaString titulada` for `deserialize` TEN Usa una cola para consumir valores en orden. Silencio
Silencio **Python** tención Lista y puntero índice para `serializar`; recursive `deserialize` ← Elegant index-tracking without external library. Silencio
Silencio **C++** Silencioso `estringstream` para la construcción de cuerdas; `queue correspondióstring confianza` para la práctica de la memoria 'eficiente con 'std::queue`. Silencio

Las tres implementaciones comparten el mismo esqueleto algorítmico, asegurando una complejidad constante del tiempo/espacio:

* **Tiempo**: O(n) – cada nodo visitó una vez.
* **Espacio**: O(n) – cadena de salida + pila de recursión o cola.

-...

### 2.5 The Good – Why Esta solución es entrevista- Amistad

1. **Claridad** – Recursión refleja la declaración del problema; un candidato puede explicar cada línea.
2. **Robustness** – Trabaja para árboles equilibrados o asados; maneja hasta 104 nodos sin desbordamiento de la pila (profundidad de la recusión Ω 104 está bien para Java/Python; C++ puede necesitar recursión o DFS iterativa si la profundidad de la pila es una preocupación).
3. **Scalability** – El algoritmo se extiende naturalmente a los árboles * n-ary* si cambiamos el separador.
4. **Readability** – Métodos de ayuda limpia (`compildString` / `_dfs`) lógica aislatada.

-...

### 2.6 The Bad – Trade‐Offs and Gotchas

Silencio Tema Silencio Lo que pasa
Silencio...
Silencioso **Tamaño de cuerda** Silencio Para un árbol binario completo, la cadena serializada contiene 2n + 1 `"null"` tokens, que puede ser ~20 KB para n = 104. Silencio Pregunte: ¿Podrías comprimir la salida? Silencio
Silencio **Repeated Parsing** Silencio Splitting the string (`data.split(',')`) crea una lista de tamaño n. Silencio Los entrevistadores pueden pedir un decodificador basado en flujo *en lugar*. Silencio
Silencio **Estadio recursivo** Silencio Los árboles profundamente desequilibrados pueden llegar a los límites de profundidad de recursión en Python o causar el desbordamiento de pila en C++. Silencio
Silencio **La conversión del entero se produce para cada nodo. No es significativo para 104 nodos, pero vale la pena señalar para micro-optimizaciones. Silencio

*Consejo para entrevistadores* Si desea mostrar *advanced* habilidad, puede implementar un pre-orden iterativo basado en **queue** para eliminar la recursión enteramente, la complejidad del código comercial para la seguridad de la pila.

-...

## 2.7 The Ugly – Hidden Edge Cases & Common Mistakes

1. *Comma de tren*
*Java/Python/C++* termina la cadena con un coma extra (`"1,2,null",`). Algunos entrevistadores prueban si usted maneja esto con gracia.
**Fix** – Desenmascarar la coma final antes de regresar, o ignorarla durante la persiana (`getline` producirá una señal vacía que es inofensiva).

2. **Empty Input String**
El arnés de prueba de LeetCode a veces llama `deserializar(""). Su código debe devolver `nullptr`/`None` con gracia.

3. *Los números principales*
La cadena token `"null"` nunca debe confundirse con un valor negativo. Compruebe siempre la igualdad antes de convertir a `int`.

4. **Separadores No-Comma**
Si decide utilizar espacios o nuevas líneas en lugar de comas, asegúrese de que el encoder/decoder use *exactamente* el mismo delimitador.

5. **Líderes de memoria (C++)**
En la versión C++, asignamos nuevos `TreeNode`s pero nunca los liberamos. En un entorno de entrevista real usted pondría la propiedad a la persona que llamó o escribiría un ayudante de 'deleteTree'.

-...

### 2.8 Interview‐Specific Takeaways

Silencio Tema Silencioso Pregunta que podría escuchar
Silencio...
¿Cuál es la complejidad del tiempo? ¿Podrías hacerlo mejor? Silencio
¿Por qué elegiste el pre-orden? ¿Podrías usar el orden de nivel? Silencio
¿Cómo maneja tu código un árbol vacío o un árbol asado? Silencio
¿Qué pasa si el árbol contiene sólo un nodo? ¿Sólo dejaron niños? Silencio
Silencio ** Manejo de memoria** Silencioso “Explica cómo manejas la cadena y la pila de recursión”. Silencio

-...

### 2.9 Conclusiones

LeetCode 297 es un problema de entrevista *canónica* que prueba tu comprensión de los traversales de árboles y la recursión.
La solución **pre-order DFS** es:

* **Eficiente** – tiempo lineal y espacio.
* **Simple** – un par de pequeños ayudantes recursivos.
* **Reliable** – Reconstrucción determinista gracias a los marcadores "null".

Al estudiar los aspectos **bueno**, **bad**, y **amplio**, usted será capaz de explicar *por qué* el algoritmo funciona y *cómo* para defenderlo contra las preguntas del caso de borde, todo lo cual impresiona a los gerentes de contratación.

■ **Practice tip** – Escriba el código en una pizarra, luego copiarlo en su IDE y ejecutar las pruebas oficiales de LeetCode.
■ **Compartir** – Si encontró esto útil, suelte un comentario o tweet `@YourHandle` y déjale saber a su red que ha conquistado LeetCode 297!

-...

## 3. Lista de verificación de salida (Entreview‐Ready)

 ✔ Cambios en la vida ↑ ❌
Silencio...
← Serializar con DFS pre-orden Silencio 1-liner recursión en Java/Python/C++
Silencio Uso `"null"` fichas para los niños ausentes Silencioso Tenga cuidado de no confundir `null` con valores numéricos
Silencio La deserialización consume la lista para vivir la cuerda vacía Handle (`"") con gracia ←
TENIDO O(n) tiempo " espacio TENIDO ANTES esté listo para explicar la pila vs. el uso de la cola
← Código listo para pasar en 3 idiomas Silencio Silencio

¡Feliz codificación y feliz entrevista!