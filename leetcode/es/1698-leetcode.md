-...
Título: LeetCode 1698. Número de subestrings distintos en una cuerda -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 1698. Número de subestrings distintos en una cuerda
**Dificultad:**
** Idiomas:** Java · Pitón · C++
** Objetivo:** Contar cuántos subestrings * diferentes* contiene una determinada cadena.

■ **Por qué importa tu búsqueda de trabajo* *
■ Los entrevistadores aman los problemas que le permiten mostrar *pensamiento algorítmico*, *Maestría en estructura de datos* y *código limpio*.
■ Este problema es una “ gema oculta” clásica – se puede resolver con un conjunto simple, un Trie inteligente, o incluso un avanzado sufijo-automaton.
■ Escribir una solución clara en tres idiomas demuestra que usted está cómodo con codificación multiplataforma, un deber-tener para los roles mayores.

-...

## 1Ω⃣ The Brute‐Force / Trie Solution (O(n2))

Silencio Silencio Silencio Silencio Silencio
Silencio--------------
Silencio **Set of substrings** ← O(n2 log n) (hashing) Silencio O(n2) Silencio
Silencio **Trie (prefix‐tree)** Silencio **O(n2)** Silencio O(n2) (caso inferior)

El Trie es una versión “espacial” del conjunto: cada nueva subestring está representada por un camino único en el árbol.
Sólo añadimos un nodo cuando aparece por primera vez una nueva secuencia de caracteres, por lo que el número total de nodos equivale al número de subestrings distintos.

A continuación se presentan implementaciones limpias y de producción en **Java**, **Python** y **C+**.

-...

## 2down Java Implementation (Trie)

``java
importar java.util*;

Solución de la clase pública {}
// Trie node containing 26 children (lowercase letters)
Clase privada TrieNode {}
TrieNode[] child = new TrieNode[26];
}

público int Distinct(String s) {
TrieNode root = nuevo TrieNode();
int distinct = 0;

(int i = 0; i) s.length(); i++) {
TrieNode cur = root;
para (int j = i; j) j++) {
int idx = s.charAt(j) - 'a';
si (cur.child[idx] == null) {
cur.child[idx] = nuevo TrieNode();
diferenciada++; // Nuevo subestring distinto encontrado
}
cur = cur.child[idx];
}
}
retorno distinto;
}

// Opcional: principal para la prueba manual rápida
public static void main(String[] args) {
System.out.println(new Solution().countDistinct("aabbaba") // 21
System.out.println(new Solution().countDistinct("abcdefg"); // 28
}
}
`` `

### ¿Por qué esto es bueno? *

- No es necesario un HashSet extra; la memoria está atada por los nodos Trie.
- Fácil de leer, O(1) char lookup per node.

### ¿Qué es **bad** / **ugly**

- El tiempo cuadrático todavía; para cadenas muy largas (n √≥ 105) será demasiado lento.
- La memoria puede volar sobre insumos patológicos (por ejemplo, todos los caracteres únicos).

-...

## 3VIEW⃣ Python Implementation (Trie)

``python
Clase TrieNode:
__slots__ = ("niño",)
def __init__(self):
# 26 letras minúsculas
self.child = [None] * 26


Solución de clase:
def countDistinct(self, s: str) - int:
root = TrieNode()
diferenciada = 0

para i en rango(len(s)):
nodo = raíz
por ch en s[i:]:
idx = ord(ch) - 97 # 'a' - título 0
si node.child[idx] es Ninguno:
node.child[idx] = TrieNode()
diferenciado += 1
nodo = nodo.child[idx]
retorno distinto


Prueba rápida
si __name_ == "__main__":
sol = Solución()
print(sol.countDistinct("aabbaba") # 21
print(sol.countDistinct("abcdefg")
`` `

### Puntos de limpieza

- `_____' mantiene cada nodo ligero.
- El algoritmo es idéntico a Java’s – simplemente adaptado a la sintaxis de Python.

-...

## 4VIEW⃣ C++ Implementation (Trie)

``cpp
#include יbits/stdc++.h
usando std namespace;

struct TrieNode {}
TrieNode* child[26];
TrieNode() {
memset(child, 0, sizeof(child));
}
};

Clase Solución {
public:
int countDistinct(string s) {
TrieNode* root = nuevo TrieNode();
int distinct = 0;

para (size_t i = 0; i) ++i) {
TrieNode* cur = root;
para (size_t j = i; j) ++j) {
int idx = s[j] - 'a';
si {}
cur-tíni[idx] = nuevo TrieNode();
++distinto; // Nuevo subestring descubierto
}
cur = cur-jóni[idx];
}
}
// (Opcional) Limpiar la memoria si quieres evitar las fugas.
retorno distinto;
}
};

/ Demo
int main() {}
Sol de solución;
cout se hizo el sol.countDistinct("aabbababa")
cout se realizó el sol.countDistinct("abcdefg")
retorno 0;
}
`` `

■ **Consejo:** En entornos de codificación competitivos normalmente no se eliminan los nodos; pero para un proyecto real se implementaría un borrado recursivo o se utilizarían punteros inteligentes.

-...

## 5down El “Siguiente” – O(n) con un Sufijo Automaton

Si usted está entrevistando para un papel **Senior/Lead**, mostrando una solución O(n) demuestra un conocimiento más profundo:

``java
público int Distinct(String s) {
int n = s.length();
int[] link = nuevo int[2 * n];
int[] len = new int[2 * n];
int[][] siguiente = nuevo int[2 * n][26];
Arrays.fill(link, -1);
para (int i = 0; i) -1);

int last = 0, size = 1;
para (char ch : s.toCharArray()) {}
int cur = tamaño+;
len[cur] = len[last] + 1;
int p = último;
int c = ch - 'a'
mientras que (p!= -1 > siguiente[p] == -1) {
siguiente[p][c] = cur;
p = link[p];
}
(p == -1) {
link[cur] = 0;
. ♫ ... {
int q = next[p][c];
si (len[p] + 1 == len[q]) {}
link[cur] = q;
. ♫ ... {
int clone = size+;
len[clone] = len[p] + 1;
System.arraycopy(next[q], 0, next[clone], 0, 26);
link[clone] = link[q];
mientras (p != -1 < p > siguiente [p] == q) {
siguiente[p][c] = clon;
p = link[p];
}
link[q] = link[cur] = clon;
}
}
último = curro;
}

ans largas = 0;
para (int i = 1; i) - len[link[i];
retorno (int) ans;
}
`` `

■ ¿Por qué usarlo? #
- Manijas de hasta 106+ cómodamente.
√ - Muestra el conocimiento de la teoría de la automata – un plus en roles centrados en algoritmo.

-...

Artículo del Blog: “El Bien, el Mal y el Ugly of Distinct Substrings”

■ **Título:** De Tries a Suffix Automata: Mastering the “Number of Distinct Substrings” Problema*

### Abstract
Contar diferentes subestrings es engañosamente simple pero una pregunta de entrevista de la central eléctrica. Prueba tu comprensión de las estructuras de datos (conjuntos, intentos, árboles de sufijo/automata), la piratería y la complejidad algorítmica. Este artículo recorre las soluciones más comunes, sus oficios y cómo explicarlas a los entrevistadores como un profesional.

#### Palabras clave
`#LeetCode #CodingInterview #DistinctSubstrings #Trie #SuffixAutomaton #AlgorithmDesign #Java #Python #C++ `

-...

#### 1down⃣ El “bueno” – Un conjunto o una prueba
- **Qué**: Enumerar cada subestring, insertar en un conjunto de hash, o construir un Trie para evitar duplicados.
- **Por qué**: Simple de implementar, pasa las limitaciones de LeetCode (n ≤ 500).
- Resultado**: `O(n2)` tiempo, `O(n2) ` memoria.
*Ideal para victorias rápidas o cuando las restricciones son modestas. *

#### 2down⃣ El “Bad” – Tiempo Cuadrático con Rolling Hash
- **Qué**: Generar todas las subestrings, computar un hash rodante (por ejemplo, Rabin‐Karp), insertar en un hash set.
- **Por qué**: Las constantes ligeramente más rápidas que un conjunto de cuerdas, pero todavía `O(n2)`.
- **Resultado**: Todavía cuadrático, riesgo de colisiones precipitadas, código más complejo.
*No vale la pena extra a menos que necesite evitar la asignación de cadenas. *

#### 3down⃣ El “Ugly” – Suffix Tree (Too Heavy)
Construir un árbol de sufijo, luego contar los bordes de la hoja.
- **Por qué**: Históricamente la solución del libro de texto (`O(n)`).
- ** Resultado**: La implementación es larga (~200 líneas), difícil de depurar, rara vez requerida en LeetCode.
*El mejor evitado a menos que esté realmente preparado para probar el dominio de estructuras de datos avanzadas. *

#### 4down⃣ El “Heroic” – Suffix Automaton (O(n))
- **Qué**: Construir un DFA mínimo que reconozca todos los sufijos; el número de subestaciones distintas equivale a la suma sobre los estados de `len[state] - len[link[state].
Tiempo lineal, memoria lineal. Manijas de hasta millones de personajes.
- Resultado**: Un código conciso e inteligente que impresiona a los entrevistadores mayores.
*Si puedes explicarlo en inglés claro, eres un corte por encima del resto. *

-...

## 7 carreras Cómo hablar sobre En una entrevista

1. **Iniciar Simple* *
*“Primero implementaré un Trie porque es intuitivo y funciona para las limitaciones dadas.”*
2. **Mención del seguimiento**
*“Si tuviéramos que procesar cadenas muy largas, cambiaríamos a un autómata sufijo por tiempo lineal.”*
3. **Explicar la complejidad**
*“El Trie da tiempo O(n2); el autómata lo reduce a O(n) reutilizando sufijos ya vistos.”*
4. **Mostrar la lectura del código* *
*Use comments, `______, and clear variable names. *
5. **Relate to Real‐World* *
*“En los motores de búsqueda o secuenciación de genomas, a menudo necesitamos contar patrones distintos de manera eficiente, por lo que sufijo automata son prácticos.”*

-...

## 8VIEW⃣ SEO‐Optimized Takeaway

- **Keywords**: “LeetCode 1698”, “distinct substrings solution”, “Trie vs suffix automaton”, “O(n) distinct substrings”, “Java/Python/C++ implementation”.
- **Meta Descripción**: “Solve LeetCode 1698 (Número de Subestaciones Distintas) con código Java, Python y C++ limpio. Compare Trie, Rolling Hash, y el enfoque lineal de Suffix Automaton. ”
- ¿Qué? Epígrafes claros (`H1`, `H2`, `H3`) para aumentar la legibilidad del motor de búsqueda.

-...

## Call to Action
■ *Ready to ace your next coding interview? Agarra los fragmentos de código, practica explicándolos, y deja que el problema “Número de Subestrings Distintos” se convierta en tu arma secreta. *

-...

**End of Article**

Siéntete libre de copiar, adaptar y publicar en tu blog o Linked Para atraer reclutadores buscando expertos en algoritmos. ¡Buena suerte! 🚀

-...

**#Respuesta** – El problema se puede resolver limpiamente en los tres idiomas con un Trie. Para mayores limitaciones, muestre el sufijo O(n) autómata. El blog de arriba explica los intercambios, listos para entrevistar narración y visibilidad SEO.