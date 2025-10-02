-...
Título: LeetCode 1612. Compruebe si dos árboles de expresión son equivalente -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

# 1612. **Comprobar si dos árboles de expresión son equivalentes** – Código + SEO‐Optimized Blog

■ * Objetivo*
■ Dados dos árboles de expresión binaria que contienen sólo el operador `+` y operands (cartas menores de tiempo), deciden si evalúan a la misma expresión para *cualquier* valores de las variables.

■ ¿Por qué importa? * *
■ En el diseño del compilador, bibliotecas simbólicas de matemáticas, o codificación de entrevistas, es necesario decidir si dos expresiones algebraicas son equivalentes. Este problema de LeetCode es una pregunta de entrevista canónica que prueba su comprensión de los traversales de árboles, la conmutación, y los intercambios espacio-tiempo.

-...

## 1. Recaptación de problemas

* Cada nodo interno es un operador `+` y siempre tiene **exactamente dos** niños.
* Cada nodo de hoja es un operario (`a`‐`z`).
* Los árboles son **válidos** árboles de expresión (el número de nodos es extraño).
* **Task:** Regresar `verdad ' si los dos árboles son *mathematically equivalent* para cada posible asignación a los operandos; de lo contrario, devolver `false ' .

*Ejemplo*

`` `
root1: +
/ \
a +
/ \
b
root2: +
/ \
+ a
/ \
b

producción: verdadera
`` `

" a + (b + c) " es igual a " b + c) + a " porque " es asociativo " .

-...

## 2. Intuición

Porque `+` es *commutative* y *associative*:

1. El orden** de los operandos no importa.
2. El **sonante** de las adiciones no importa.

Así, dos árboles son equivalentes **iff** contienen el multiset ** igual** de los operandos.

Así que sólo necesitamos contar cuántas veces cada variable aparece en cada árbol y comparar los conteos.

Si cualquier operando aparece un *odd* número de veces en los conteos combinados, los dos árboles difieren (porque ese operand cancelaría en un árbol pero no el otro).

-...

## 3. Algoritm

1. Crear un array entero `cnt[26]` (una ranura para cada letra de la maleta inferior).
2. **DFS** cada árbol, incrementando `cnt [operand - 'a']` cuando se visita un nodo de operando.
3. Después de visitar ambos árboles, compruebe cada cnt[i].
* If any `cnt[i]` es extraño → los árboles no son equivalentes. *
*Else → son equivalentes. *

**La complejidad* *

TEN TERRITOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------------------
Silencioso** Silencio Cada nodo es visitado una vez. Silencio
Silencio** Únicamente una matriz de 26 elementos; la profundidad de recursión es `O(h)` donde `h` es altura de árboles. Silencio

-...

## 4. Implementaciones de referencia

■ **Nota:** Todos los fragmentos de código son autocontenidos.
■ La clase `Node` se define exactamente como en la declaración del problema LeetCode.

#### 4.1 Java

``java
// Definición para un nodo de árbol binario.
Clase Node {}
char val;
Nodo izquierdo, derecho;
Nodo() { this.val = '+'; }
Node(char val) { this.val = val; }
Node(char val, Nodo izquierdo, Nodo derecho) {
this.val = val; this.left = left; this. derecho = derecho;
}
}

Solución de la clase pública {}
public boolean checkEquivalence(Node root1, Node root2) {
int[] cnt = nuevo int[26]; // a..z

dfs(root1, cnt);
dfs(root2, cnt);

para (int c : cnt) {
si (c % 2 != 0) devolver falso;
}
retorno verdadero;
}

dfs privados (nodo, int[] cnt) {
si (nodo == nulo) regresa;
si (node.val!= '+) { //
cnt[node.val - 'a']+;
}
dfs(node.left, cnt);
dfs(node.right, cnt);
}
}
`` `

#### 4.2 Python

``python
Definición para un nodo de árbol binario.
Clase Nodo:
def __init_(self, val='+', left=None, right=None):
self.val = val
autoizquierda
self.right = right

Solución de clase:
Def check Equivalencia(self, root1: Node, root2: Node) - conveniente bool:
cnt = [0] * 26

def dfs(node):
si no el nodo:
Regreso
si node.val!= '+': # operand
cnt[ord(node.val) - ord('a')] += 1
dfs(node.left)
dfs(node.right)

dfs(root1)
dfs(root2)

devolver todo (c % 2 == 0 para cnt)
`` `

#### 4.3 C++

``cpp
Incluido el título
usando std namespace;

// Definición para un nodo de árbol binario.
struct Node {}
char val;
Nodo* izquierdo;
Nodo* derecho;
Node(char v='+', Node* l=nullptr, Node* r=nullptr)
: val(v), left(l), right(r) {}
};

Clase Solución {
public:
bool checkEquivalence(Node* root1, Node* root2) {
vector implicado cnt(26, 0);
dfs(root1, cnt);
dfs(root2, cnt);
para (int c : cnt)
si (c % 2 != 0) devolver falso;
retorno verdadero;
}

privado:
vacío dfs(Nodo* nodo, vector asignadoint
si (!node) regresa;
si (nodo-convalido!= '+)
++cnt[node-ciendoval - 'a'];
dfs(node-propleft, cnt);
dfs(node-ienteright, cnt);
}
};
`` `

-...

## 5. Seguimiento: Añadiendo el Operador

Si el árbol también puede contener `-`, el problema de equivalencia se hace más difícil:

* `` is **not** commutative: `a - b` ل `b - a`.
* `` is also **not** associative: `(a - b) - c`  maduro `a - (b - c)`.

Una estrategia común:

1. **Canonicalizar** cada expresión convirtiéndola en una cadena *totalmente paréntesis* (o otra forma normal).
2. Compare las cuerdas canónicas.

En la práctica, se puede realizar una traversal post-orden que construye una cuerda:

``java
String expr(Node n) {
si (n.val!= '+') devolver String.valueOf(n.val);
devolver "(" + expr(n.left) + n.val + expr(n.right) + ")";
}
`` `

Para la resta simplemente usas `-`.
Dos árboles son equivalentes sif `expr(root1).equals(expr(root2))`.

-...

## 6. Artículo del Blog: “El Bien, el Mal, y el Ugly of Expression‐Tree Equivalence”

■ **Audiencia:** Ingenieros de software, entrevistados, reclutadores, y cualquier persona que desee conseguir un rol desarrollador senior.

-...

### 6.1 Title (SEO‐Optimized)

**“Comprobar si dos árboles de expresión son equivalentes – Java/Python/C++ Solución + consejos de entrevista”**

¿Por qué? La palabra clave “expresión de la equivalencia de árboles” es buscada por entrevistadores, reclutadores y estudiantes. Combinarlo con “Java/Python/C++” señales de conocimientos multilingües, potenciando SEO.

-...

### 6.2 Meta Descripción

■ *“Aprenda a resolver LeetCode 1612 en Java, Python y C++. Entender las matemáticas detrás de los árboles comunicativos, ver el código completo, y descubrir trucos de seguimiento para la resta. Perfecto para su próxima entrevista de codificación.”*

-...

### 6.3 Esquema

TENCIÓN TERRITORIO ANTERIOR ANTERIOR
Silencio...
¿Qué es un árbol de expresión? Silencio
Silencio **Problema Declaración**
tención **Bien** TENIDO Simplicidad, O(n) tiempo, O(1) espacio TENIDO
tención **Bad** Silencioso Casos de Edge, sólo `+` apoyado Silencio
tención **Intensivamente** Silencio Extensivo a ``, potenciales trampas
Silencioso ** Código completo** viv Java, Python, C++
Silencio **Siguiente** Silencio Sutracción de manipulación, formas canónicas
Silencio **Entrevista Consejos** Silencio Cómo lanzar su solución
Silencio **Conclusión** Silencio Recap + llamada a la acción

-...

### 6.4 Full Blog Post

■ *(El post del blog se formatea en Markdown; copy‐paste en su plataforma de blogging o GitHub README.) *

``markdown
# Compruebe si dos árboles de expresión son equivalentes – Java/Python/C++ Solución + consejos de entrevista

## 1. Why This Problem Rocks Your Interview

Los árboles de expresión son la columna vertebral de los compiladores, motores de matemáticas simbólicos e incluso la comunidad **LeetCode**. Ser capaz de probar dos árboles son equivalentes demuestra dominio sobre:

- Traversales de trineo** (DFS/BFS)
- ** Propiedades algebraicas** (commutatividad)
- ** Optimización algorítmica** (tiempo lineal, espacio constante)

Si usted puede clavar este problema, los reclutadores verán que puede mezclar estructuras de datos con la visión matemática.

## 2. Recaptación de problemas

Se le dan dos árboles binarios que representan expresiones aritméticas con sólo el operador y los operados de minúsculas. Regrese 'verdad' si las expresiones son equivalentes para *todo* posible asignación a las variables.

*Examples*

Silencioso `root1` Silencio `root2` Silencioso
Silencio--------------------------------------------------------
Silencio `[x]` Silencio `[x]` Silencio `true`
TENIDO `[+,a,+,null,null,b,c]` TENIDO `[+,+,a,b,c]` ANTE `verdad` ANTE `a + (b + c) `(b + c)
TENIDO `[+,a,+,null,null,b,c]` TENIDO `[+,+,a,b,d]` TENIDO `false` ANTE Different operand (`c` vs `d`) Silencio

## 3. El Bien

Cada nodo es visitado una vez.
- **O(1) Extra Space** – Sólo una matriz de 26 elementos (constant para letras minúsculas).
- Intuitivo** - Contando operandos, compara la paridad.
- **Extensible** - Funciona para cualquier número de variables.

## 4. El mal

- Sólo ``** La solución se centra en la comunicatividad y la asociatividad. Si la resta aparece, estás fuera de suerte.
- Large Alphabets... Si usted soporta `A-Z` o Unicode, el tamaño de la matriz crece, aunque todavía manejable.

## 5. El Ugly

- Sutracción (`-`)** - No comercial, no asociativa. Un contador simple falla.
- **Parentheses / Precedencia Operadora** – Si se extiende a `*` o `/`, necesita un parser completo o normalizador de expresión.
- **Efectos secundarios** - Si los operandos no son independientes (por ejemplo, funciones con efectos secundarios), la equivalencia matemática ya no es suficiente.

### 5.1 How to Tackle `- `

Un enfoque confiable es **canonicalizar** cada expresión:

1. **Traversal Post-order**: construir una cadena `("(" + izquierda + op + derecha + ")").
2. Compare las cuerdas canónicas.

Esto garantiza que se preserve la estructura (y el orden). Es tiempo de O(n) y espacio O(n), pero eso es aceptable para escenarios de entrevista.

## 6. Code Walkthrough

A continuación se encuentran soluciones limpias y de producción en tres idiomas.

### 6.1 Java

``java
Clase Node {}
char val;
Nodo izquierdo, derecho;
Nodo() { this.val = '+'; }
Node(char val) { this.val = val; }
Node(char val, Nodo izquierdo, Nodo derecho) {
this.val = val; this.left = left; this. derecho = derecho;
}
}

Solución de la clase pública {}
public boolean checkEquivalence(Node root1, Node root2) {
int[] cnt = nuevo int[26];
dfs(root1, cnt);
dfs(root2, cnt);
para (int c : cnt) si (c % 2 != 0) devolver falso;
retorno verdadero;
}

dfs privados (nodo, int[] cnt) {
si (nodo == nulo) regresa;
si (node.val!= '+') cnt[node.val - 'a']+;
dfs(node.left, cnt);
dfs(node.right, cnt);
}
}
`` `

### 6.2 Python

``python
Clase Nodo:
def __init_(self, val='+', left=None, right=None):
self.val = val
autoizquierda
self.right = right

Solución de clase:
Def check Equivalencia(self, root1: Node, root2: Node) - conveniente bool:
cnt = [0] * 26

def dfs(node):
si no no nodo: retorno
si node.val!= '+':
cnt[ord(node.val) - ord('a')] += 1
dfs(node.left)
dfs(node.right)

dfs(root1)
dfs(root2)
devolver todo (c % 2 == 0 para cnt)
`` `

### 6.3 C++

``cpp
struct Node {}
char val;
Nodo* izquierdo;
Nodo* derecho;
Node(char v='+', Node* l=nullptr, Node* r=nullptr)
: val(v), left(l), right(r) {}
};

Clase Solución {
public:
bool checkEquivalence(Node* root1, Node* root2) {
vector implicado cnt(26, 0);
dfs(root1, cnt);
dfs(root2, cnt);
para (int c : cnt) si (c % 2 != 0) devolver falso;
retorno verdadero;
}

privado:
vacío dfs(Nodo* nodo, vector asignadoint
si (!node) regresa;
si (nodo-convalido != '+') ++cnt[node-consejoval - 'a'];
dfs(node-propleft, cnt);
dfs(node-ienteright, cnt);
}
};
`` `

## 7. Puntos de entrevista

1. **Explicar la matemática** – Porque `+` es conmutativa, sólo la paridad de cada variable importa. ”
2. **Mostrar el código** – Comparta primero la solución basada en el contador; luego pregunte si puede extenderse a `-`.
3. ** Casos de borde de alta luz** – Niños nulos, árboles de un solo nodo.
4. **Preguntas aclaratorias** – Si el entrevistador permite la resta u otros operadores, pivote a la canonicalización temprano.

## 8. Takeaway

- **Master el truco del contador** para árboles puros.
- **Prepárate para canonicalizar** cuando las limitaciones del problema cambien.
- **Práctica** escribiendo la solución desde cero en cada idioma. Esta fluidez de lenguaje cruzado es un gran imán de reclutador.

■ **Lista a su próxima entrevista de codificación?** Practique este problema en LeetCode, agréguelo a su cartera, y vea las puertas de la entrevista abierta.

`` `

`` `

-...

### 6.5 Call to Action

**Repositorio de GitHub** – Almacene las soluciones y los casos de prueba.
- **LeetCode Profile** – Mostrar sus etiquetas de solución (`DFS`, `Hashing`, `Algorithms`).
- Enlazado en... Publique un corto snippet con la etiqueta `#ExpressionTreeEquivalence`.
- **Recruiter Outreach** – Mencione el problema al discutir su experiencia de entrevista técnica.

-...

## 7. Pensamientos finales

Solving LeetCode 1612 es una victoria **quick** que demuestra una elegancia algorítmica. Al proporcionar código completo en Java, Python y C++, usted muestra la versatilidad del lenguaje. La sección “Siguiente-Up” enseña a los reclutadores que está pensando por delante, listos para manejar conjuntos de operadores más complejos.

*Ahora ve código, as the interview, and land that senior dev position! *

`` `

-...

## 7.1 Publicación Lista de verificación

- Llámanos por titulo > meta
- Límites de idioma
- Conseguir bloques de código completo con resaltado de sintaxis
- Consejos de seguimiento y entrevista
- ✅ CTA (“Descargar el repo GitHub” o “Programar una llamada”)

-...

## 7.2 Final Word

Este problema es un *gold‐mine* para su cartera de entrevistas. Maestro el truco de contador de tiempo lineal, entender las limitaciones, y estar listo para pivotar a formas canónicas para la resta. Con los fragmentos de código multi-idioma arriba, no solo estás resolviendo un desafío de LeetCode: estás entregando un paquete de entrevistas **completo** que a los reclutadores les encantará. ¡Feliz codificación!
`` `

-...

## 7. Observaciones finales

Ahora tienes:

1. ** Código de trabajo** en tres idiomas populares.
2. Una comprensión clara de **cuando** la solución funciona y **por qué**.
3. Un artículo **blog** listo para su sitio web personal, LinkedIn, o un puesto de Media, con título optimizado SEO y meta descripción.
4. Explicaciones de entrevista que muestran a los reclutadores que puede **explicar**, **justificar**, y **extender** la solución.

**Siguientes pasos:**
- Ejecute las soluciones contra una batería de pruebas de unidad.
- Construir un GitHub repo titulado `leetcode-1612-expr-tree` que contiene el código, las pruebas, y el blog Markdown.
- Publicar el artículo.

Buena suerte, ¡y que el operador sea siempre a su favor!