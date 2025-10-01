-...
Título: LeetCode 2296. Design a Text Editor -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código – LeetCode 2296 “Design a Text Editor”

A continuación se ** tres soluciones completas y autocontenidas** – una en **Java, Python y C+** – que satisfacen las limitaciones de LeetCode y se ejecutan en **O(k)** tiempo por operación.

■ ¿Por qué esta solución? * *
* Utiliza la estructura más simple que da tiempo *O(k)*: dos objetos `Stack` (o un `StringBuilder` con un índice de cursor).
* No hay traversal de lista conectada, no hay bibliotecas pesadas – perfectas para una entrevista o código de producción.
* Todas las maletas (que van más allá del texto, eliminando más de lo disponible, cursor vacío) se manejan limpiamente.

-...

### 1.1 Java – `StringBuilder` + índice de cursor

``java
importar java.util*;

class TextEditor {}
texto privado StringBuilder; // el texto actual
int cursor privado; // posición del cursor (0 ... text.length())

public TextEditor() {
este.text = nuevo StringBuilder();
este.cursor = 0;
}

/** Apéndice `texto' en el cursor, luego mueve el cursor al extremo derecho de él. */
public void addText(String newText) {}
texto.insert(cursor, nuevoTexto); // O(newText.length())
cursor += nuevoText.length();
}

* Suprimir hasta 'k' chars a la izquierda del cursor.
* Devuelve el número de personajes realmente eliminados. */
public int deleteText(int k) {}
int remove = Math.min(k, cursor); // no se puede eliminar más allá del inicio
si 0) {
texto.delete(cursor - quitar, cursor);
cursor -= quitar;
}
Retirar la devolución;
}

* Mueva el cursor a la izquierda hasta posiciones 'k'.
* Devuelve los últimos caracteres min(10, cursor) a la izquierda del cursor. */
public String cursorLeft(int k) {
cursor = Math.max(0, cursor - k);
int start = Math.max(0, cursor - 10);
volver texto.substring(start, cursor);
}

* Mueva el cursor hasta posiciones 'k'.
* Devuelve los últimos caracteres min(10, cursor) a la izquierda del cursor. */
public String cursorRight(int k) {
cursor = Math.min(text.length(), cursor + k);
int start = Math.max(0, cursor - 10);
volver texto.substring(start, cursor);
}
}
`` `

-...

### 1.2 Python – dos pilas "deque"

``python
de las colecciones importa
de la importación Lista

class TextEditor:
def __init__(self):
# La pila izquierda contiene caracteres a la izquierda del cursor
# La pila derecha contiene caracteres a la derecha del cursor
self.left = deque()
self.right = deque()

def addText(self, text: str) - Ninguno.
para ch en texto:
self.left.append(ch) # O(1) each

def deleteText(self, k: int) - int:
Retirada = 0
mientras se quitan a ti mismo. izquierda:
self.left.pop()
Retirado += 1
Retirada

def cursorLeft(self, k: int) - título str:
movido = 0
mientras se movió a ti mismo. izquierda:
self.right.appendleft(self.left.pop())
movido += 1
# last min(10, cursor) chars to the left of cursor
volver ''.join(list(self.left)[-10:])

def cursorRight(self, k: int) - título str:
movido = 0
mientras se movió a ti mismo. Bien.
self.left.append(self.right.popleft())
movido += 1
volver ''.join(list(self.left)[-10:])

# Ejemplo de uso
# editor = TextEditor()
# editor.addText("leetcode")
`` `

*¿Por qué dos pilas? *
Nos dejan **push/pop en O(1)**, dando en general **O(k)** para cada operación, incluso para los mayores `k=40` y millones de llamadas.

-...

### 1.3 C++ – `estring` + índice de cursor

``cpp
#include ■string
#include >

class TextEditor {}
std:: texto de la cadena; // texto actual
size_t cursor; // 0 ... text.size()

public:
TextEditor() : text(""), cursor(0) {}

vacio añadirText(cont std::string &s) {
text.insert(cursor, s);
cursor += s.size();
}

int deleteText(int k) {}
int remove = std::min(k, static_cast fielint(cursor));
si 0) {
text.erase(cursor - remover, remover);
cursor -= quitar;
}
Retirar la devolución;
}

std::string cursorLeft(int k) {
cursor = pt::max seleccionasize_t confianza(0, cursor - k);
size_t start = (cursor √= 10) ? cursor - 10 : 0;
devolver texto. substr(start, cursor - start);
}

std::string cursorRight(int k) {}
cursor = pt::min seleccionasize_t confianza(text.size(), cursor + k);
size_t start = (cursor √= 10) ? cursor - 10 : 0;
devolver texto. substr(start, cursor - start);
}
};
`` `

-...

## 2. Blog Artículo – “Diseñar un Editor de Textos (LeetCode 2296): El Bien, el Mal, y el Ugly

■ **Meta‐Description* *
■ Master LeetCode 2296 “Diseñar un Editor de Textos”. Explore tres implementaciones limpias en Java, Python y C++, entienda las operaciones y aprenda cómo hacer preguntas de entrevistas sobre manipulación de cadenas y simulación de cursor.

-...

#### 2.1 Introduction

¿Alguna vez has mirado el problema de LeetCode “Design a Text Editor” y te has preguntado por qué está calificado “Hard”?
La dificultad principal es que cada operación – añadir, eliminar, mover a la izquierda, mover a la derecha – debe ser **O(k)**, y la estructura de datos debe mantener el cursor en sincronía con el texto.

En este post:

- Rompe la declaración del problema y las limitaciones.
- Mostrar tres soluciones **idiomáticas** (Java, Python, C++).
- Discuss the *good*, *bad*, and *ugly* parts of each approach.
- Destacar por qué el método basado en pilas es el estándar de oro para los entrevistadores.
- Dale una hoja de trampa para impresionar a los reclutadores.

Entremos.

-...

### 2.2 Declaración de problemas

← Operación Silencioso Lo que hace
Silencio----------------------------------------
Silencio `addText(estring text)` Silencio Insertar en el cursor, el cursor se mueve a la derecha. Silencio
TENIDO `deleteText(int k)` TENIDO Suprímase hasta `k` chars left of cursor.
Silencio `cursorLeft(int k)` Silencio Move cursor izquierda `k` pasos. Silencio `string` – last min(10, cursor) chars latitud
Silencio `cursorRight(int k)` Silencio Move cursor right `k` steps. Silencio `string` – last min(10, cursor) chars latitud

*Constraints*: `text.length`, `k ≤ 40`; up to 2 × 104 calls; only lowercase letters.

-...

### 2.3 La solución “buena” – Dos pisos (o Deque)

*Por qué es genial*

Silencio Reason Silencio
Silencio...
Silencio **O(k) time** Silencio Cada operación toca a la mayoría de los caracteres 'k'. Silencio
Silencio **Constant‐space per char** Silencio Dos deques almacenan caracteres directamente, sin gimnasia puntero. Silencio
Silencio **Código simple** Silencio No hay nodos personalizados de lista conectada, no hay malabarismo de bordes más allá de los pops de pila. Silencio
Silencio **Language‐agnostic** Silencio Obras en Java (`ArrayDeque`), Python (`collections.deque`), C++ (`std::deque`). Silencio
Silencio **Perfecto para entrevistas** Silencio Entrevistadores amor simulación basada en pilas; fácil de explicar y probar. Silencio

*Core idea*

- **La pila izquierda** contiene caracteres **izquierda** del cursor.
- *La pila derecha* contiene caracteres *derecha* del cursor.
- **Inserción** → empujar a la pila izquierda.
- ** Eliminación** → pop de la pila izquierda.
- **Mueva a la izquierda** → pop desde la izquierda → empuja a la derecha.
- **Move right** → pop desde la derecha → empujar a la izquierda.
- ** cuerdas de resultados** → Mira los 10 elementos principales de la pila izquierda.

El **cursor** es implícitamente el límite entre las dos pilas.

-...

### 2.4 The “Bad” – StringBuilder + Cursor Index (Java)

**Pros**

- Usa el rápido `StringBuilder de Java para la concatenación.
- Una sola matriz (estring) – sin deques extra.

**Cons**

- `insert` y `delete` son **O(n)** en el peor caso porque `StringBuilder` debe cambiar caracteres.
Para las limitaciones dadas (`k ≤ 40` y operaciones totales ≤ 20 k) está bien, pero la complejidad teórica es más débil.
- El código debe gestionar cuidadosamente los límites índices; un pequeño fallo puede causar `IndexOutOfBoundsException`.
- No es ideal para entrevistadores que esperan soluciones *pura* o deque.

■ ¿Cuándo usarlo? #
■ Si está codificando un prototipo a pequeña escala o una sumisión de LeetCode, esto funciona perfectamente. Para una entrevista, traiga el enfoque de la pila.

-...

### 2.5 La “Ugly” – Classic Singly-Linked List

Algunas personas implementan el editor con una lista de enlaces personalizada **Node-based**:

- Cada nodo almacena un personaje y un puntero "next".
- El cursor es un puntero a un nodo.
- Inserción / eliminación / movimiento son todos O(k) atravesando los nodos 'k'.

*Por qué es feo*

Silencioso
Silencio...
Silencio **Pointer complejidad** Silencio Debe mantener 'prev` punteros para el movimiento izquierdo. Silencio
Silencio **Memory overhead** Silencio Cada nodo es un objeto – 8 bytes (puntero) + encabezado de objeto ♥ 32 bytes por char. Silencio
Silencio **Asesino a depurar** Silencio fuera de lugar por uno errores son comunes. Silencio
tención **Entrevistar el riesgo** tención Los entrevistadores a menudo rechazan el código puntero de bajo nivel a menos que se le pida explícitamente que implemente una lista vinculada. Silencio

Si necesita una lista doblemente conectada *real*, debe utilizar la biblioteca estándar ( < LinkedList seleccionadoCharacter confidencial > ) en lugar de escribir la suya propia.

-...

### 2.5 El “Seguimiento” – ¿Por qué se vinculan– La lista no es necesaria

El pequeño `k` (≤ 40) del problema permite *cualquier* solución que toque a la mayoría de `k` caracteres a pasar.
Sin embargo, los entrevistadores también prueban *pensando sobre la complejidad*.
Una solución basada en pilas le muestra entender cómo mantener operaciones *amortizadas* O(1), que es más impresionante que un ingenuo `StringBuilder` hack.

-...

## 2.6 Casos de bordes que debes probar

Silencio Qué hacer para comprobar Silencio
Silencio...
Silencio Muévete a la izquierda antes de comenzar Silencio `cursorLeft(100)` → cursor se queda a 0. Silencio
Silencio Muévete justo después de la finalización Silencio `cursorRight(100)` → cursor se detiene en `text.length()`. Silencio
Silencio Suprímase más de lo que está disponible Silencio `deleteText(10)` cuando sólo 3 chars left → returns 3. Silencio
 Curso permanenter en cadena vacía Silencio Todas las operaciones deben funcionar, devolviendo cadenas vacías para movimientos de cursor. Silencio
Silencio Añadiendo una cuerda vacía Silencio No hay cambio, el cursor se queda. Silencio
TENIDO Querying when cursor ANTE 10 ANTE Vuelva todos los charcos izquierdos. Silencio

Siempre ejecute un script rápido para verificar estos en su idioma de elección.

-...

### 2.7 Complexity Analysis

← Operación Silenciosos Tiempo Silenciosos
Silencio------------------------
Silencio `addText` Silencio **O(k)** Silencio O(k) para los nuevos personajes
Silencio `deleteText` Silencio **O(k)** Silencio O(k) eliminados caracteres Silencio
Silencio `cursorLeft` Silencio **O(k)** Silencio O(1) – sólo mover elementos entre las pilas
Silencioso `cursorRight` Silencio **O(k)**

El uso de la memoria es lineal en el número de caracteres almacenados (Equipo 2 × `n` bytes para dos pilas).

-...

### 2.8 Quick‐Reference Code Snippets

Silencio Idioma Silencio Key Data Structure Silencio One‐liner for `deleteText(k)` Silencio
Silencio...
Silencio **Java** Silencioso `StringBuilder text; int cursor;` ¦ Silencio
Silencio **Python** Silencio `deque left, right;` TENIDO ` while removed  removed k and self.left: self.left.pop();` Silencio
Silencio **C++** Silencioso `estring text; size_t cursor;` Silencioso `int remove = min(k, (int)cursor);` Silencio

■ *Tip*: Mantenga la pila **izquierda** como la “historia” del editor. Esto hace que la cadena de resultado sea trivial: sólo mire los últimos 10 elementos.

-...

### 2.9 How to Ace the Interview

1. **Explica la idea de la pila primero. #
Mostrar los dos límites y cómo cada operación mapas para apilar operaciones.
2. **Mostrar complejidad sobre papel** – O(k) para los cuatro métodos.
3. **Escribe el código** – manténgalo corto; agrega comentarios para explicar cada línea.
4. **Más rápido** – escribir algunas afirmaciones que cubren la muestra de la declaración del problema.
5. **Mención del seguimiento** – ¿Y si K podría ser hasta 105? → todavía estarías en territorio O(k).

Programador de amor candidatos que pueden *abstract* un problema (cursor + texto) en una estructura de datos limpia (dos pilas). Ese es el truco.

-...

### 2.10 Call to Action

- **Prueba el código de LeetCode** – copie los fragmentos en el editor y ejecute la prueba de muestra.
- ** Ponga su solución a GitHub** con un README claro; los reclutadores a menudo revisan su GitHub.
- **Aplicar posiciones de entrevistas de codificación** que requieran habilidades de *estring manipulation*, por ejemplo, Backend Engineer, Mobile Developer o DevOps.
- **Programa una entrevista de mock** con un amigo; utilice este problema como el ejercicio *core*.

■ *Su próxima pregunta de entrevista podría ser: “¿Puede implementar un editor de texto basado en cursor en su idioma preferido?” – ¡Ven preparado con la solución de pila arriba! *

-...

### 2.11 Pensamientos Finales

El problema LeetCode “Design a Text Editor” no se trata de algoritmos mágicos; es un rompecabezas **simulation** que prueba:

- Comprensión del tiempo *amortizado*.
- Maestría en estructuras básicas de datos (tapas, deques).
- Código limpio y libre de errores.

La solución de dos puestos es el estándar **oro** para entrevistas. El enfoque StringBuilder es limpio en Java, mientras que C++ ofrece un patrón muy similar de 'string + cursor'.

Elige el idioma con el que estés más cómodo, ejecuta el código contra el juez LeetCode, y entrarás en tu próxima entrevista con confianza.

■ **Listo para enfrentar el próximo desafío “Hard” LeetCode? * *
■ Manténgase afinado para obtener más soluciones de entrevistas de tamaño murciélago - dejar un comentario o DM me si necesita ayuda para preparar su próxima entrevista de codificación!

-...

### 2.12 Etiquetas > Palabras clave

- `Design a Text Editor `
- `LeetCode 2296 `
- `Java StringBuilder `
- `Python deque `
- 'C++ dos pilas `
- Entrevista de manipulación. `
- Movimiento de los precursores `
- Entrevista de trabajo `
- `O(k) time complexity `
- " Coding interview prep "

-...

■ **Feliz codificación - y buena suerte aterrizar ese trabajo de tecnología de sueños! * *