-...
Título: LeetCode 336. Parejas de condromo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## Palindrome Pairs - LeetCode 336
### El problema duro, la mejor solución, y por qué importa en las entrevistas

■ **Keyword-rich intro** – *“Palindrome Pairs, LeetCode 336, problema de entrevista dura, solución O(N), Java, Python, C+++, Trie, detección de palindrome”*

-...

#### TL;DR

* ** Objetivo** – Encontrar todos los pares índice `(i, j)` tal que `palabras[i] + palabras[j]` es un palindrome.
* **Constraints** – `1 ≤ words.length ≤ 5 000`, cada palabra hasta 300 chars.
* ** Complejidad requerida** – `O(longitud total de todas las palabras)` (Equipo O(exploración vivacitaria)
* **Optimal Approach** – Build a **Trie of reversed words** and keep a list of word IDs that can form a palindrome with the remaining prefix.
* **Idiomas** – Implementación en **Java, Python y C++**.

A continuación se muestra el código completo para cada idioma, seguido de un artículo detallado del blog que pasa por el algoritmo, sus compensaciones, y cómo muestra sus cortes de estructura de datos en una entrevista de contratación.

-...

## 1. Aplicación de Java (O(explotación subversiva))

``java
importar java.util*;

*
* LeetCode 336 – Parejas de Palindrome
* Tiempo de ejecución: O(explorar vidas subversivas), Memoria: O(firmar vidas eternas)
*/
Solución de la clase pública {}

* Trie node sosteniendo el índice de la palabra que termina aquí y
* una lista de índices cuyo sufijo forma un palindrome con el
* resto de la palabra. */
Clase privada TrieNode {}
int wordIndex = -1; // -1 → ninguna palabra termina aquí
Mapa seleccionadoCaracter, TrieNode confiar siguiente = nuevo HashMap garantizado();
Lista realizadaInteger título palindromeSuffix = nuevo ArrayList recomendado();
}

* Compruebe si la subestring s [i ... final] es palindrome. */
booleano privado esPalindrome (String s, int i) {
int l = i, r = s.length() - 1;
mientras que (l
si (s.charAt(l) != s.charAt(r)) devuelve falso;
l++; r...
}
retorno verdadero;
}

public List made(String[] words) {
TrieNode root = nuevo TrieNode();

--------- Construye el trie de palabras inversas...------ */
para (int id = 0; id = palabras.length; id+) {}
Estring w = words[id];
String rev = nuevo StringBuilder(w).reverse().toString();
TrieNode node = root;

para (int j = 0; j) j++) {
/* Si el sufijo restante de rev es un palindromo,
* entonces el prefijo original de w puede emparejar con cualquier
* Palabra que termina en este nodo. Tienda id. */
si (esPalindrome(rev, j))
node.palindromeSuffix.add(id);

char c = rev.charAt(j);
nodo = nodo.next.computeIfAbsent(c, k - título nuevo TrieNode());
}
nodo.wordIndex = id; // marca final de una palabra
}

--------- Encuentra todos los pares de palindrome...------
Lista realizadaLista realizadaInteger confianza result = nuevo ArrayList recomendado();

para (int id = 0; id = palabras.length; id+) {}
Estring w = words[id];
TrieNode node = root;

para (int j = 0; j) j++) {
/* Caso 3: el nodo actual termina una palabra y el resto
* of w is palindrome → (id, node.wordIndex) */
si (nodo.wordIndex!= -1 " node.wordIndex!= id ' id
isPalindrome(w, j))
result.add (Arrays.asList(id, node.wordIndex));

/* Muévete por el trie */
nodo = nodo.next.get(w.charAt(j));
si (nodo == nulo) se rompen;
}
si (nodo == nulo) continúan;

/* Caso 1: partido completo (palabra termina aquí) */
si (nodo.wordIndex != -1 > nodo.wordIndex != id)
result.add (Arrays.asList(id, node.wordIndex));

/* Caso 2: palabras que tienen un sufijo palindrome con el resto
* of w (stored during trie construction). */
for (int other : node.palindromeSuffix)
result.add (Arrays.asList(id, other));
}

Resultado de retorno;
}
}
`` `

■ **Por qué esta es una gran respuesta de entrevista* *
■ 1. ** Tiempo-optimal** – escaneamos cada personaje al máximo dos veces.
■ 2. **Espacio-optimal** – las tiendas de trie sólo necesitaban bordes.
■ 3. **Readability** – separación clara de las fases de búsqueda de edificios.

-...

## 2. Implementación de Python (O(durante palabra eterna))

``python
de la importación Lista, Dict

Clase TrieNode:
__slots__ = ('idx', 'children', 'pal_suffix')

def __init__(self):
self.idx = -1 # -1 → ninguna palabra termina aquí
Dict[str, 'TrieNode'] = {}
auto.pal_suffix: List[int] = [] # índices de palabras cuyo sufijo es palindrome

Solución de clase:
def is_pal(self, s: str, start: int) Bool:
retorno s[start:] == s[start:][:-1]

def palindrome Pares(self, words: List[str]) -(List[int]:
root = TrieNode()

# ---------- Construir un trie de palabras inversas...------
para i, w en enumerado(palabras):
rev = w[:-1]
nodo = raíz
for j, ch in enumerate(rev):
si auto.is_pal(rev, j):
node.pal_suffix.append(i)
nodo = nodo.children.setdefault(ch, TrieNode())
node.idx = i

# ---------- Encontrar pares de palindrome --------
res = []

para i, w en enumerado(palabras):
nodo = raíz
for j, ch in enumerate(w):
Caso 3
si node.idx != -1 y node.idx != i y self.is_pal(w, j):
re.append([i, node.idx])
nodo = nodo.children.get(ch)
si no el nodo:
descanso
más:
# El nodo no es ninguno
Caso 1
si node.idx != -1 y node.idx != i:
re.append([i, node.idx])
# Case 2
para otro en nodo.pal_suffix:
re.append([i, other])

retorno
`` `

* Notas específicas*
* Use `______` para reducir la sobrecarga de memoria de los nodos de trie.
* El ayudante es_pal se llama sólo unas cuantas veces por palabra.

-...

## 3. C++ Implementación (O(firmo permanente palabra))

``cpp
Incluido el título
#include ■string
#include ■unordered_map Conf

usando std namespace;

clase TrieNode
public:
int wordIdx = -1; // -1 → ninguna palabra termina aquí
unordered_map determinadachar, TrieNode* Niño;
vector implicado fielSuffix; // índices de palabras cuyo sufijo es palindrome

~TrieNode() {
para (auto &p : niño) eliminar p.second;
}
};

Clase Solución {
// helper: comprobar si s[pos .. end] es palindrome
bool isPal(const string &s, int pos) {}
para (int l = pos, r = (int)s.size() - 1; l ' identificado r; ++l, --r)
si (s[l] != s [r]) devuelve falso;
retorno verdadero;
}

public:
vector realizador identificadoint confianza palindromePairs(vector asignadostring títulos) {}
TrieNode *root = nuevo TrieNode();

--------- Construir trie de palabras inversas...------ */
para (int id = 0; id > (int)words.size(); ++id) {
const string &w = words[id];
cadena rev = string(w.rbegin(), w.rend());
TrieNode *node = root;

para (int j = 0; j) ++j) {
si (isPal(rev, j))
node-propiospaloSuffix.push_back(id);
char c = rev[j];
si
node-(c) = new TrieNode();
nodo = nodo-cliente[c];
}
nodo-ContextIdx = id;
}

--------- Encontrar pares de palindrome...------
vector realizador:
para (int id = 0; id > (int)words.size(); ++id) {
const string &w = words[id];
TrieNode *node = root;
para (int j = 0; j) ++j) {
// Caso 3
si (nodo-contextIdx!= -1 " node- `wordIdx!= id ' id
isPal(w, j))
ans.push_back({id, node-jerowordIdx});

char c = w[j];
si (!node-jerochild.count(c))) romper;
nodo = nodo-cliente[c];
}
si (!node) continúan;

Caso 1
si (nodo- confíawordIdx != -1 " sinde- confianzaIdx != id)
ans.push_back({id, node-jerowordIdx});

// Caso 2
para (incluidos otros: node-propiospapix)
ans.push_back({id, other});
}

eliminar raíz; // destructor de TrieNode liberará a los niños
devolver los ans;
}
};
`` `

■ ** Observaciones específicas de C++**
* `unordered_map` da un promedio de búsqueda de borde O(1).
* Explicit `delete root;` limpia los nudos trie asignados.

-...

## 4. Artículo del Blog – “El bueno, el malo, y el Ugly de Parejas de Palindrome”

### 4.1 The Good: Why the Trie Idea Wins

1. **Escáneo de línea** – Cada carácter de cada palabra es visitado un número constante de veces (una vez que se inserta, una vez que se pregunta).
2. **No hay colisiones de Hash** – El trío es determinista; cada camino representa un sufijo de una palabra inversa.
3. **Built‐in Palindrome Check** – Al grabar *sufijos palindromicos* durante la construcción evitamos reescanear los mismos subestrings durante la búsqueda.
4. **Extensible** – La misma estructura se puede reutilizar para *anagramas*, *prefix‐suffix* problemas, o *reverse‐lookup* tareas.
5. **Interviewer‐Friendly** – Te muestra entender:
* Construcción trie
* Detección de palindrome en O(length)
* Cambios en el espacio/tiempo

■ **Key entrevista Takeaway** – “Construí una estructura de datos que me permite responder *cualquier consulta de palindrome‐concatenación en tiempo lineal. ”

-...

### 4.2 The Bad: Edge Cases & Memory Footprint

¿Por qué es “Bad” la Mitigation
Silencio...
Silencioso ** cuerda vacía** Silencioso `" es un palindrome; se combina con cada palabra que en sí mismo es un palindrome. ← Maneja explícitamente `"" como un caso separado o almacena su índice en el trie. Silencio
Silencio **Duplicar palabras** Silencio El problema garantiza que todas las palabras son únicas, pero los datos reales podrían no ser. ← Deduplicar antes de construir, o almacenar múltiples índices si se permiten duplicados. Silencio
Silencio **Elevar alfabeto** Silencio Un trie con un alfabeto enorme (por ejemplo, Unicode) podría soplar la memoria. Restrict to ASCII/UTF‐8 for LeetCode constraints. Silencio
Silencio **Memory overhead** Silencio Cada nodo almacena un `HashMap` / `unordered_map`. Con 5 000 palabras × 300 chars, el peor de los casos ~1.5 millones de nodos. Silencio

-...

### 4.3 The Ugly: Common Pitfalls Cómo evitarlos

Silencio Pitfall Silencio Típico Insensato
Silencio----------------------------
Silencio **Null‐pointer during search** Silencio Olvidar `continue` cuando una rama de trie no existe. Usar un guardia (¡si (¡nodo) romper; " ) y una cláusula de `else ' después del lazo en C+/Java, o `romper ' lógica ' en Python. Silencio
Silencio ** Auto-pairing** Silencio Paring a word with itself (`i == j`) when the word is a palindrome. ← Revise explícitamente `node.idx != id`. Silencio
TEN **Comprobación incorrecta de palindrome** TENIDO Utilizando `s[start:] == s[:-1]` que revierte la cadena *total* cada llamada. Silencio Compruebe sólo la subestring `s[start:]` contra su revés. Silencio
Silencio **Duplicar resultados** Silencio Agregar el mismo par dos veces (una vez durante la búsqueda, una vez durante la construcción trie). Silencio O deduplicar la lista de resultados con un `set`, o diseñar el algoritmo por lo que cada par se añade sólo una vez (como se muestra). Silencio

-...

## 5. SEO‐Friendly Wrap‐Up – Land That Job

■ **Descripción de los datos** “Aprenda la solución de Trie lineal para LeetCode 336 – Parejas de Palindrome, con Java, Python y código C++, además de un artículo de entrevista que muestra que es un asistente de estructura de datos. ”

1. **Mostrar el algoritmo** – Los fragmentos de código anteriores son copy‐paste‐ready; imprimen a un gerente de contratación que comprueba su presentación contra la suite de pruebas LeetCode.
2. **Agregar un post de LinkedIn** – Publicar un breve escrito de la solución con un enlace a tu repo GitHub; usar etiquetas como `#Leetcode336 #PalindromePairs #DataStructures #Java #Python #C++ #EntreviewPrep`.
3. **Construir una página de cartera** – Alojar el artículo del blog en Medium o su sitio personal con el título *“Palindrome Pairs – LeetCode 336 (Java/Python/C++)”* e incrustar los bloques de código.
4. **Explicar las compensaciones** – En una entrevista en vivo, esté listo para discutir *time vs. space*, la importancia de manejar la cadena vacía, y cómo la solución escala a alfabetos más grandes.

-...

### 6. Take- Lista de verificación de la entrevista

TENIDO ANTERIOR TENIDO ANTERIOR POR QUÉ Ayuda a vivir
La vida... la vida...
← ✔ Cambios en la vida Explicar el concepto de palabras inversas* primero. ← Establece el contexto rápidamente. Silencio
Ω ✔ Cambio de imagen Los tres casos (completo partido, prefijo palindrome, sufijo palindrome). ← Demuestra problemas sistemáticos. Silencio
✔ ✔ Cambio a través de un pequeño ejemplo (por ejemplo, `["bat","tab", "cat"]). Silencio muestra comprensión del flujo de algoritmo. Silencio
← ✔ Cambio de la mención en el borde de la manipulación (`"', duplicados). Silencio Muestra robustez. Silencio
Ω ✔ Cambios en la vida Destacar la garantía `O(longitud total)`. ← Conoce la complejidad requerida de LeetCode. Silencio
Mantenga el código limpio, comentado y dividido en fases *compilado* + *búsqueda*. TENIDO El punto de orgullo de un codificador. Silencio

-...

### 7. Pensamiento final

Mastering *Palindrome Pairs* demuestra que puede hacer malabares **manipulación de cuerda**, ** lógica de condromo**, y ** diseño eficiente de estructura de datos**—todos los temas básicos en entrevistas de codificación de nivel superior. Las soluciones Java, Python y C++ arriba están listas para pasar, linear-time, y listas para impresionar a los reclutadores buscando un fuerte fondo algorítmico.

Feliz codificación, y buena suerte aterrizando ese próximo papel de ingeniería de software!