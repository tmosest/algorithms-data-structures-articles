-...
Título: LeetCode 616. Añadir Bold Tag en String -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Add Bold Tag in String – LeetCode 616
**Java, Python & C++ + una guía de entrevista “Good‐Bad‐Ugly”**

■ **Meta-descripción** – ¿Buscas clavar tu próxima entrevista de codificación? Master LeetCode 616 – *Agregar la etiqueta Bold en String*. Sumérgete en una implementación limpia de Trie, un truco de rayos booleanos y una versión C++. Obtenga el trabajo listo con las ideas de entrevista “buena, mala y fea”.

-...

## 1. Declaración de problemas

■ Dada una cuerda `s` y una serie de cuerdas `palabras`, envuelven **todo subestring** de `s` que aparece en `palabras` con un solo par de etiquetas audaces ``. `` ... `Seguido/b ``.
* Si dos subestrings se superponen, fusionarlos en un bloque audaz.
* Si dos bloques audaces son consecutivos, fusionarlos también.

*Ejemplo*

`` `
Entrada: s = "aaabbb", palabras = ["aa", "b"]
Producto: "()
`` `

**Constraints* *

- `1 0 = s.length
- `0 0 = palabras. longitud = 100'
- `1 0 = palabras [i].length
- `s` y todas `palabras[i]` contienen sólo letras y dígitos en inglés.

El problema es una pregunta de entrevista clásica de cuerdas; también es la base para el LeetCode “Bold Words in String” (problema 758).

-...

## 2. Panorama general de la solución

El principal reto es ** encontrar eficientemente todas las ocurrencias de las palabras** en `s` y luego combinar intervalos superpuestos/adyacentes. Dos enfoques populares:

Silencio Silencio Silencio Silencio Silencio Silencio
Silencio-----------------------------Prince----
Silencio **Trie + Scan** Silencio Construye un poco de todas las palabras; en cada índice de `s` caminar el trío para encontrar el partido más largo. Marque una matriz booleana para posiciones “bold”. Silencio `O(las vidas eternas * maxLen(words))» Silencio `O(totalLength(words)) + O(las vidas eternas)` Silencio
Silencio **Boolean Array + Naïve Buscar** Silencio Por cada palabra, escanee `s` con `indexOf`; marcado rangos emparejados. Silencio `O(las palabras previas sometidas a la práctica) `O (las vidas eternas)` Silencio

Nos enfocaremos en la implementación **Trie** – es conciso, corre rápido, y demuestra una estructura de datos clásica. También mostraremos la variante **boolean array** para la integridad.

-...

## 3. 📌 Good, Bad & Ugly – Puntos de conversación de entrevistas

TENIDO TERRITORIO TÉpico ANTERIOR Qué hacer frente a las Pitfalls
Silencio--------------------------------------------------------
Silencio 1 Silencio **Clarificar el formato de entrada** Silencio ¿Está garantizada "palabras" no vacía? tención Olvídate de manejar las palabras vacías → `O(0)` TENCIÓN Check `words.length == 0 ' → return `s`s
Silencio 2 Silencio **Definir “sobrelapso” justamente** TENIDO Dos intervalos audaces `[l1, r1]` y `[l2, r2]` superposición si `l2 <= r1`. Silencio Mezclando índices inclusivos/exclusivos TENIDO Uso Índices inclusivos basados en 0
Silencio 3 Silencio ** Casos altos con audacia consecutiva** Silenciosos `[0,2]` + `[3,5]` → `[0,5]` porque `3 == 2+1` ANTE Olvídate de combinar → etiquetas colgantes Silencio Después de marcar, iterate una vez para insertar etiquetas cuando el estado cambia
Silencio 4 Silencio **La justificación de la complejidad** Silencio Mostrar cómo la trie reduce el peor de los casos de `O(n*m)` a `O(n * maxLen)` Silencio Sobre-optimización por caching partido más largo por índice ¦ Mantener un solo `maxEnd` durante la exploración Silencio
Silencio 5 Silencio **Testing** Silencio Incluir casos con palabras superpuestas, palabras anidadas, y palabras idénticas  Prueba de límite desaparecido → > > desaparecidos al final ← Final check for open tag 

■ **“Bueno”** – Una explicación limpia del algoritmo, manejo cuidadoso de los índices y una complejidad comprobada.
■ **“Bad”** – Una implementación demasiado verbosa que olvida fusionar intervalos o malinterpretar el último bloque audaz.
■ **“Ugly”** – Los bucles anidados de fuerza bruta con concatenación de cuerdas en el interior; funciona pero el tiempo fuera en el gran set de prueba.

-...

## 4. 🔧 Código Snippets

A continuación se muestran **full, ready-to-compile** soluciones en **Java**, **Python**, y **C+**. Los tres utilizan el enfoque Trie; la solución Python también incluye una variante alternativa de rayos booleanos para la comparación.

▪ restablecimiento **Todo el código se prueba en la plataforma LeetCode. #
> **Recuerda pegar el código en la sección correspondiente del idioma en LeetCode. #

-...

### 4.1 Java – Trie Implementation

``java
// Java 17

importar java.util*;

Clase Solución {

--------- Trie Node...
Clase privada TrieNode {}
Mapa seleccionadoCaracter, TrieNode confía child = new HashMap Quería();
boolean isWord = false;
}

--------- Trie...
clase privada Trie {
final privado TrieNode root = nuevo TrieNode();

vacío add(String word) {
TrieNode node = root;
para (carc : word.toCharArray()) {}
nodo = nodo.child.computeIfAbsent(c, k - título nuevo TrieNode());
}
Nodo. isWord = true;
}

/* Volver el último índice (inclusivo) de la palabra más larga
que comienza en la posición 'start' en 's'.
Si no hay ninguno, regrese -1. */
más largo Match(String s, int start) {
TrieNode node = root;
int end = -1;
(int i = start; i) s.length(); i++) {
char c = s.charAt(i);
nodo = nodo.child.get(c);
si (nodo == nulo) se rompen;
si (node.isWord) termina = i;
}
final de retorno;
}
}

public String addBoldTag(String s, String[] words) {
si (palabras == null ¦ 0) retorno s;

Trie trie = nuevo Trie();
for (String w : words) trie.add(w);

int n = s.length();
boolean[] bold = new boolean[n];
int maxEnd = -1; // la posición más cercana hasta el momento

para (int i = 0; i)
int end = trie.longest Match(s, i); // palabra más larga empezando en i
maxEnd = Math.max(maxEnd, end); // combinar con intervalo previo
bold[i] = maxEnd >= i; // posición actual es negrita
}

StringBuilder sb = nuevo StringBuilder();
boolean inBold = false;
para (int i = 0; i)
si (bold[i] " sensible !inBold) { // comenzar bold
sb.append("cantab]);
inBold = true;
} si (!bold[i] " golpe inBold) { // end bold
sb.append(" obtenidos/b título");
inBold = false;
}
sb.append(s.charAt(i));
}
si (inBold) sb.append("Seguido/b]); // cerrar al final
devolver sb.toString();
}

--------- Conductor simple para las pruebas locales-------- */
public static void main(String[] args) {
Solución sol = nueva solución ();
System.out.println(sol.addBoldTag("abcxyz123", nuevo String[]{"abc","123"})
System.out.println(sol.addBoldTag("aaabbb", nuevo String[]{"aaa","b"});
}
}
`` `

**La complejidad* *
- Tiempo: `O(las vidas eternas * maxLen(palabras)' - cada índice escanea a la palabra más larga.
- Espacio: `O(totalLength(words) + Silencios sufridos)` – trie nodes + matriz booleana.

-...

### 4.2 Python – Trie & Boolean‐Array Variant

``python
# Python 3.11

Clase TrieNode:
__slots__ = ("niño", "es_palabra")
def __init__(self):
self.child = {}
self.is_word = Falso

Clase Trie:
def __init__(self):
self.root = TrieNode()

def add(self, word: str):
nodo = self.root
para ch en palabra:
nodo = nodo.child.setdefault(ch, TrieNode())
node.is_word = Verdadero

def longest_match(self, s: str, start: int) int:
nodo = self.root
final = 1
para i en rango(start, len(s)):
nodo = nodo.child.get(s[i])
si el nodo es Ninguno:
descanso
si node.is_word:
final = i
final de retorno

Solución de clase:
def addBoldTag(self, s: str, words: list[str]) - confiar str:
si no palabras:
retorno s

trie = Trie()
para w en palabras:
trie.add(w)

n = len(s)
bold = [False] * n
max_end = -1
para i en rango(n):
end = trie.longest_match(s, i)
max_end = max(max_end, end)
bold[i] = max_end >= i

res = []
in_bold = False
para i, ch in enumerate(s):
si atrevidos[i] y no in_bold:
re.append("Seguido]
in_bold = True
Elif no bold[i] and in_bold:
re.append("Seguido/b título")
in_bold = False
re.append(ch)
si in_bold:
re.append("Seguido/b título")
volver ".join(res)

# ---------- Fuerza bruta de rayos booleanos (para comparación)--------
def addBoldTag_bruteforce(s: str, words: list[str]) - confiar str:
n = len(s)
bold = [False] * n
para w en palabras:
inicio = s.find(w)
mientras comienza!= -1:
para i en rango(start, start + len(w)):
bold[i] = True
inicio = s.find(w, start + 1)
res, in_bold = [], False
para i, ch in enumerate(s):
si atrevidos[i] y no in_bold:
re.append("Seguido]
in_bold = True
Elif no bold[i] and in_bold:
re.append("Seguido/b título")
in_bold = False
re.append(ch)
si in_bold:
re.append("Seguido/b título")
volver ".join(res)

# -------- Conductor simple...
si __name_ == "__main__":
sol = Solución()
print(sol.addBoldTag("abcxyz123", ["abc","123"])
print(sol.addBoldTag("aaabbb", ["aaa","b"])
`` `

**Notas*

- `__slots_' reduce la sobrecarga de memoria para el trie.
- La variante de fuerza bruta es `O(len(words) * len(s))` y debe evitarse en la producción.

-...

### 4.3 C++ – Trie Implementation

``cpp
// C+17 (GNU+17)

#include יbits/stdc++.h
usando std namespace;

struct TrieNode {}
matriz realizadaTrieNode*, 62 hijos de confianza; // 0-9, A-Z, a-z
bool isWord;
TrieNode() : child{nullptr}, isWord(false) {}
};

clase Trie
TrieNode* root = nuevo TrieNode();
public:
vacio add(cont cadena reducida word) {
TrieNode* node = root;
por (char ch : word) {
int idx = charIndex(ch);
si (!node- confíachild[idx]) node-(idx] = nuevo TrieNode();
nodo = nodo-(idx);
}
node- títuloisWord = true;
}

/* Regresar el último índice del partido más largo empezando por 'start'.
Regresa -1 si no hay coincidencia. */
más largo Match(const cordón plaga s, int start) const {
TrieNode* node = root;
int end = -1;
para (int i = start; i) ++i) {
int idx = charIndex(s[i]);
nodo = nodo-(idx);
si (nodo) romper;
si (nodo-clienteisWord) final = i;
}
final de retorno;
}

privado:
// Mapa: '0'-'9' - título 0-9, 'A'-'Z' - título 10-35, 'a'-z' - título 36-61
static int charIndex(char c) {}
si ('0'' 0' 0') devuelto c " &= " ;
si ('A') se entiende= c " círculo c " = 'Z') devuelve 10 + (c - 'A');
retorno 36 + (c - 'a');
}
};

Clase Solución {
public:
string addBoldTag(string s, vector seleccionadostring confianza words) {
si (palabras.empty()) devuelve s;

Trie trie;
para (continuo auto-cliente w : palabras) trie.add(w);

int n = s.size();
vector:
int maxEnd = -1;
para (int i = 0; i) {}
int end = trie.longest Partidos, i);
maxEnd = max(maxEnd, end);
bold[i] = (maxEnd >= i);
}

cadena res;
bool inBold = false;
para (int i = 0; i) {}
si (bold[i] " sensible !inBold) { res += " implicab confianza"; inBold = true; }
si (!bold[i] " sensible inBold " ) { res += " obtenidos/b confidencial"; inBold = false; }
res += s[i];
}
si (inBold) res += "traducido/b confidencial";
restitución;
}
};
`` `

**La complejidad** – idéntica a la versión Java.

En C++ se puede optimizar el trie con un array de 62 niños (10+26+26).

-...

## 5. 🎯 Takeaway for the Interview

- **Explicar el algoritmo paso a paso** (compilar, escanear, marcar, combinar).
- ** Casos de bordes validados** (palabras vacías, palabras de caracteres individuales, intervalos superpuestos).
- **Descubre el O(explorando palabras vivas)** espacio/tiempo de intercambio de la trie.
- **Mostrar un controlador mínimo** o 'mantener' función si usted está codificación fuera de LeetCode; demuestra confianza.

Recuerde, los contadores de LeetCode **runtime** y **memory** son estrictos. Una solución que fusiona intervalos perezosos (sobre la marcha) y **insertas etiquetas en un solo pase** pasará todas las pruebas.

-...

## 6. 🚀 Pensamiento final

■ **Bold Words in String** es la entrevista “estring-matching” equivalente al problema de la mejor práctica* de una entrevista de codificación. Dominar el escaneo trie + el patrón de fusión de intervalos no sólo te lleva a través de LeetCode, sino que también demuestra tu capacidad de manejar el preprocesamiento de cadenas, la búsqueda eficiente y la lógica de límites cuidadosos — mata a cada ingeniero de software senior debe poseer.

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀

-...

** ¿Tienes preguntas? * *
- ¿Quieres una solución Rust?
- Curioso sobre Aho-Corasick para el emparejamiento multi-pattern?

Avísame en los comentarios – Actualizaré el repo con más idiomas!