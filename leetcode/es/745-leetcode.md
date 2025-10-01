-...
Título: LeetCode 745. Prefijo y Sufijo Buscar -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
LeetCode 745 - **Prefijo y Sufijo Buscar**
■ ** Objetivo:** Encontrar el índice de una palabra que comienza con un prefijo dado ** y** termina con un sufijo dado.
■ **Idiomas:** Java TENIDO Python ANTE C++
■ *Por qué importa* Este problema es una pregunta de entrevista común que prueba el conocimiento de los intentos, la manipulación de cuerdas y el preprocesamiento para consultas rápidas. Resolver bien puede conseguir un trabajo en Google, Amazon, Microsoft, o cualquier firma de alta tecnología.

-...

##  Problema general

TEN TERRITORIO TENIDO Detalle ANTE
Silencio...
Silencio **Nombre** Silencioso Prefijo y Sufijo Buscar
Silencio **Dificultad**
Silencio ** Entrada** Silencioso `WordFilter(words)` – array de cuerdas (1 ≤ `words.length` ≤ 104, cada 1 ≤ `palabras[i].length` ≤ 7) - dos cuerdas (1 ≤ `pref.length, suff.length` ≤ ≤ 7) Silencio
tención **Output** tención Index (0-based) de la palabra **latest** que comienza con `pref` y termina con `suff`. Regreso **-1** si tal palabra no existe. Silencio
Silencio **Constraints** Silencio Hasta 104 llamadas a `f`. Todas las cadenas contienen sólo letras inglesas minúsculas. Silencio

■ *Ejemplo*
" texto
■ WordFilter wordFilter = nuevo WordFilter(["apple"]);
> palabraFilter.f("a", "e"); // → 0
" `

-...

# Idea núcleo

El reto es responder rápidamente a muchas preguntas.
Un análisis lineal ingenuo (`O(N)` por consulta) es demasiado lento.
**Pre-procesamiento** las palabras con una estructura de datos que soporta *prefix* y *suffix* en **O(1)** o **O(L)** tiempo (donde *L* ≤ 7) es la clave.

## Double Trie (Prefix + Suffix)
Construir dos intentos:

1. **Trío de prefijo** – almacena todos los prefijos de cada palabra.
2. **Suffix trie** – almacena todos los sufijos invertidos de cada palabra.

Durante una consulta, caminar ambos intenta en paralelo para reunir las palabras candidatas, luego intersectar los dos conjuntos de resultados y devolver el índice más alto.

**Pros**
* Simple de entender.
* Funciona bien cuando la longitud de la palabra es pequeña (≤ 7).

**Cons**
* Requiere dos intentos separados.
* Los conjuntos de interacción para cada consulta pueden ser costosos cuando muchas palabras comparten el mismo prefijo/suffix.

### Single Trie with “{” Separator (LeetCode‐Recommended)
Insertar para cada palabra *w* todas las cuerdas de la forma
`suffix + '{' + w` (donde `{` es un personaje lexicográficamente mayor que 'z').
Durante una consulta, construya la llave `suff + '{' + pref` y busque el trío.

**Pros**
* Sólo un triple.
* Cada nodo almacena el índice **maximum** (peso) de cualquier palabra que pasa a través de ella → respuesta es directamente el peso del nodo.
* Extremadamente rápidas consultas (`O(L)`).

**Cons**
* Lógica de inserción ligeramente más compleja.
* Usa 27 punteros por nodo (26 letras + separador).

El blog de abajo se centra en la solución **single‐trie** porque es la más eficiente y ampliamente utilizada en las entrevistas.

-...

Algoritm Walk-Through

1. **Proceso previo**
Por cada palabra:
* Por cada sufijo de `w` (incluyendo el sufijo vacío):
* Insertar la cadena `s + '{' + w` en el trie.
* Mientras se inserta, actualice el " peso " de cada nodo arrastrado a " i " .
* Insertar `"{" + w` para manejar el caso de un sufijo vacío.

2. ** Pregunta** f(pref, suff) "
* Construir la clave de búsqueda: `key = suff + '{' + pref`.
* Camina el trie siguiendo `key`.
* Si en cualquier momento el camino se rompe → volver **-1**.
* De lo contrario → devolver el `peso' almacenado en el último nodo.

Debido a que siempre guardamos el peso ** más alto** (índice más grande), el valor devuelto es exactamente lo que el problema pide.

-...

Análisis de la Complejidad

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencio **Constructor** Silencioso `O(N · L2)` (N = 104, L ≤ 7) – pero en la práctica ~105–106 operaciones. Silencio `O(N · L2)` – total number of trie nodes. Silencio
Silencio **Query** ( " f " ) Silencioso `O(L)` (≤ 14 traversales de carbón). Silencio

■ Con tales palabras cortas, las constantes son insignificantes, dando **sub-millisecond** por consulta en máquinas reales.

-...

Casos de bordes llenos

Silencio Caso confidencialidad Cómo lo manejamos
Silencio...
← Sufijo vacío (`suff == "''') Silencio Insertar `"{" + w` (es decir, sufijo vacío + separador + palabra). Silencio
Prefijo vacío ( " pref == " ) La clave de la consulta es `suff + '{' ' . Silencio
Silencio Ninguna palabra coincidente ← La traversal golpeará a un nodo perdido → retorno **-1**. Silencio

-...

## 📦 Implementation

A continuación se presentan implementaciones limpias y listas de producción para **Java**, **Python**, y **C+**.

■ **Consejo:** Al publicar su código en una entrevista o en su GitHub, añadir comentarios que claramente indican el propósito de cada parte (especialmente la lógica del separador).

-...

### 📌 Java Implementation (Single Trie + “{”)

``java
// Java 17
Clase WordFilter {}
privada estática final int ALPHABET_SIZE = 27; // 26 letras + '{ '

Clase privada TrieNode {}
TrieNode[] next = new TrieNode[ALPHABET_SIZE];
int weight = -1; // max index passing through this node
}

final privado TrieNode root = nuevo TrieNode();

int privado charIndex(char c) {}
c == '{'? 26 : c - 'a';
}

inserción privada de vacío (clave de llave, peso de entrada) {
TrieNode node = root;
para (char ch : key.toCharArray()) {}
int idx = charIndex(ch);
si (nodo.next[idx] == null) {
node.next[idx] = nuevo TrieNode();
}
nodo = nodo.next[idx];
nodo.weight = peso; // mantener el último índice
}
}

public WordFilter(String[] words) {
para (int i = 0; i) hice palabras.length; i++) {
Estring w = words[i];
// Todos susfijos de w
para (int start = 0; start  w w.length(); start++) {}
insert(w.substring(start) + "{" + w, i);
}
// Sufijo vacío (caso de entrada)
insert("{" + w, i);
}
}

public int f(String pref, String suff) {
llave de cuerda = suff + "{" + pref;
TrieNode node = root;
para (char ch : key.toCharArray()) {}
int idx = charIndex(ch);
si (nodo.next[idx] == null) retorno -1;
nodo = nodo.next[idx];
}
Nodo de retorno. peso;
}
}
`` `

-...

### 📌 Python Implementation (Single Trie + “{”)

``python
# Python 3.9+

Clase TrieNode:
__slots__ = ('next', 'weight')
def __init__(self):
self.next = [None] * 27 # 26 letters + '{ '
peso propio = 1


Clase WordFilter:
def __init__(self, words):
self.root = TrieNode()
para peso, palabra en enumerado(palabras):
# All suffixes of word
para i en rango(len(word)):
clave = palabra[i:] + "{" + palabra
auto._insert(key, weight)
# Empty suffix
auto._insert("{" + palabra, peso)

def _insert(self, key, weight):
nodo = self.root
para ch en clave:
idx = 26 si ch == '{' else ord(ch) - 97
si nodo.next[idx] es Ninguno:
nodo.next[idx] = TrieNode()
nodo = nodo.next[idx]
nodo. peso = peso

def f(self, pref, suff):
llave = suff + "{" + pref
nodo = self.root
para ch en clave:
idx = 26 si ch == '{' else ord(ch) - 97
si nodo.next[idx] es Ninguno:
retorno -1
nodo = nodo.next[idx]
Nodo de retorno. peso
`` `

-...

### 📌 C++ Implementación (Single Trie + “{”)

``cpp
// C+17
Clase WordFilter {}
public:
struct Node {}
int weight = -1;
std::array Nodo*, 27 hijos = {nullptr};
};
Node* root = new Node();

inserto de vacío(cont std::string curva clave, peso int) {}
Nodo* cur = raíz;
for(char c : key) {
int idx = (c == '{') ? 26 : c - 'a';
si(!cur- confíachild[idx]) cur- títulochild[idx] = nuevo Nodo();
cur = cur-jóni[idx];
r- peso = peso; // mantener el índice más grande
}
}

WordFilter(std::vector seleccionados::string confianza words) {
para(int i = 0; i < (int)words.size(); ++i) {
const string w = words[i];
para (int j = 0; j) ++j) {
insert(w.substr(j) + "{" + w, i);
}
insert("{" + w, i); // vacío suffix case
}
}

int f(estring pref, string suff) {
llave de cadena = suff + "{" + pref;
Nodo* cur = raíz;
for(char c : key) {
int idx = (c == '{') ? 26 : c - 'a';
si (!cur- confíachild[idx]) retorno -1;
cur = cur-jóni[idx];
}
Retorno de peso rizado;
}
};
`` `

-...

##  Settlement Test Cases

``text
palabras = ["apple", "apply", "applesauce", "banana"]
consultas =
f("app", "le") → 2 (applesauce)
f("ap", "ly") → 1 (apply)
f("ba", "na") → 3 (banana)
f("c", "d") → -1
`` `

Ejecute sus propias pruebas de unidad con unas cuantas mil palabras al azar para estar absolutamente confiado.

-...

##  tuya buena, mala, mala Ugly

Silencio.
Silencio... tu vida...
Silencio 1 Silencio **Hora** Silencio Pre-procesamiento `O(N·L2)` es trivial para *L* = No.
Silencio 2 Silencio **Espacio** Silencioso `O(N·L2)` nodos es aceptable (~106). Ninguno.
TEN 3 TENIDO **Readability ** TENIDO El código de doble vista es intuitivo pero más lento. TEN Ninguno. TEN La complejidad del truco del separador puede confundir a los entrevistadores si salta comentarios. Silencio
Silencio 4 Silencio **Mantenibilidad** Silencio Easier para extenderse con otras consultas de cadena. tención doble-trie duplicación de la lógica.
Silencio 5 Silencio **Interview Impact** Silencio Demonstrates solid data‐structures knowledge. Silencio Ninguno. Silencio Sobre-ingeniería (por ejemplo, usando 'unordered_map` per node) dolerá. Silencio

■ **Takeaway:** Usa el truco de una sola pista: es el más rápido y el que los entrevistadores realmente esperan de ti.

-...

## 📌 Take‐Away Checklist (Job‐Ready)

- [ ] ✅ Comprender *trie* básicos (niños array, peso del nodo).
- [ ] Saber por qué `{` es seguro como separador.
- [ ] ✅ Implementar *insert* que actualiza el peso del nodo.
- [ ] ✅ Construir llave `suffix + '{' + prefijo` en consultas.
- [ ] ✅ Handle vacío sufijo insertando `"{" + palabra`.
- [ ] TENIENDO la complejidad del disco: 'O(N·L2) 'construir, 'O(L)` consulta.
- [ ] ↑ Ver pruebas de unidad.
- [ ] Prepárate para explicar *bueno* (velocidad), *bad* (complejidad), *muy* (juego de codificación) partes.

-...

## 📚 SEO‐Friendly Blog Sections

A continuación se muestra un blog completo que puede pegar en Medium, Dev.to, o su blog personal. Contiene todas las palabras clave que los reclutadores están buscando.

-...

# LeetCode 745 – Master Prefix & Suffix Buscar en Java, Python & C++

■ **Keywords**: LeetCode 745, Prefix y Suffix Search, WordFilter, trie, Java, Python, C++, entrevista, estructuras de datos, OOP, desafío de codificación, entrevista de ingeniero de software

## 1. ¿Qué es LeetCode 745?

LeetCode 745 te desafía a construir un **WordFilter** que apoye las consultas de la forma:

``text
f(prefijo, sufijo) → mayor índice de una palabra que comienza con prefijo y termina con sufijo
`` `

Este es un problema de cuerda clásico que cada entrevista de ingeniero *software* debe dominar.

## 2. The Separator Trick: Why `{` Obras

Cuando veas `palabra + '{' + sufijo' en una solución, piensa en:

- **No hay colisiones**: `{` no es una carta, por lo que no puede aparecer en las palabras de entrada.
- **Traversal persistente**: Cada tienda " Nodo " de la mayoría de 27 niños (26 letras + " ).

## 3. Construyendo el Trie – O(N·L2) Tiempo, Rápido en la práctica

Aunque el tiempo de construcción teórico es cuadrático de longitud de palabra, con *L* ≤ 7 el tiempo del mundo real es un puñado de milisegundos.

### Java Code

``java
clase WordFilter { /* ... */ }
`` `

### Python Code

``python
Clase WordFilter: /* ... */
`` `

### C++ Código

``cpp
clase WordFilter { /* ... */ };
`` `

## 4. Querying in O(L) Time – Sub‐Millisecond Answers

Todas las consultas involucran el traversing a la mayoría de 14 nodos (prefijo + sufijo ≤ 7 cada uno). Es por eso que las soluciones pasan 104 consultas más en un ordenador portátil.

## 5. Casos de borde y consejos prácticos

- ** Sufijo vacío** → insertar `"{" + word`.
- ** Prefijo vacío** → clave es sólo `suffix + '{'`.
- **No coincide** → devolver `-1`.
Verifica con miles de palabras al azar.

## 6. Secretos de entrevista: Explique el Bien, el Mal

- **Bien**: Consultas rápidas de relámpago, actualizaciones de peso de nodo limpias.
- **Bad**: Over-engineering with hash maps per node.
Olvidar comentar la lógica del separador.

## 7. Lista de verificación para el programa

- Conocimiento de estructura de datos (tries).
- Eficiencia Algorítmica (O(N·L2), O(L) consulta).
- Código limpio en Java, Python, C++.
- Pruebas de unidad completas.
- Capacidad para explicar los cambios.

-...

## 🎯 Palabras finales

Si ace LeetCode 745 con la aplicación **single trie + “{”**, estás mostrando reclutadores que:

- Puede implementar estructuras de datos sofisticadas.
- Comprender por qué ciertos trucos (como el separador) son necesarios.
- Entrega código rápido y mantenible.

Adelante, publica el código en GitHub, escribe un blog, y sigue practicando! 🚀

-...

¡Feliz codificación y buena suerte con tus entrevistas!