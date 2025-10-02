-...
Título: LeetCode 30. Subestring with Concatenation of All Words -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 30. Subestring with Concatenation of All Words
**Hard** - Código Leet

-...

## Problema Recap
Dada una cuerda `s` y una serie de palabras `palabras` (toda la misma longitud), encuentra cada índice inicial de una subestring de `s` que es una concatenación de *toda palabra* en `palabras' exactamente una vez, en cualquier orden.

■ Ejemplo
's = "barfoothefoobarman" ``, `palabras = ["foo", "bar"] `
■ Respuesta: `[0,9]` (`barfoo` y ``foobar`)

-...

Sinopsis de la solución

Silencio Lo que hacemos _ Por qué funciona
...------------------------
Silencio 1. Silencio **Pre-proceso** – construir un mapa de hash `targetCount` que almacena cuántas veces cada palabra debe aparecer. tención Necesitada para una búsqueda rápida y para detectar uso excesivo. Silencio
Silencio 2. Silencio **Venta deslizante** – mover una ventana de tamaño `le(palabra) * k` a través de `s`. La ventana está avanzada **por longitud de palabra** así que nunca examinamos los mismos caracteres dos veces. TENIDO Garantías *O(n)* tiempo donde *n = s.length*. Silencio
Silencio 3. Silencio **Mantenga un contador de ejecución** – un mapa de hash `currentCount` que rastrea cuántas veces cada palabra aparece en la ventana actual. Mantenga una variable `utilizado' que cuenta palabras distintas que son **no sobre-utilizados**. Silencio Cuando `utilizado == k` y ninguna palabra se usa sobre-utilizado → encontramos una subestring válida. Silencio
Silencio 4. Silencio ** Desigualdad de la mandíbula** – si aparece una palabra no en `targetCount`, restablecer la ventana comenzando justo después de esta palabra. Silencio Descarta rápidamente subestrings imposibles. Silencio
Silencio 5. tención **Mandle over-usage** – cuando el tamaño de la ventana es igual a `substringSize` o tenemos una palabra sobre-utilizada, deslizar el borde izquierdo hacia adelante palabra por palabra, decrementar cuenta y `utilizado` como sea necesario. Silencio Mantiene la ventana exactamente la longitud requerida mientras preserva la corrección. Silencio

Este algoritmo funciona en **O(n)** tiempo y utiliza **O(k)** espacio adicional (para los mapas del hash), satisfaciendo las limitaciones del problema.

-...

## 2VIEW⃣ Code Implementations

A continuación encontrará implementaciones limpias y listas de producción en **Java**, **Python**, y **C+**.

▪ restablecimiento Todas las soluciones suponen que las palabras no son vacías y cada palabra tiene la misma longitud.
■ They also guard against the edge case when `s` is too short to contain a full concatenation.

-...

#### 2.1 Java

``java
importar java.util*;

Solución de la clase pública {}
public List made integer confianza findSubstring(String s, String[] words {)
Lista de resultadosInteger título = nuevo ArrayList implicado();
si (s == null Новые palabras infligidas == null 0) Resultado de retorno;

int wordLen = words[0].length();
Intento palabra Cuenta = palabras.longitud;
int totalLen = wordLen * wordCount;
si (s.length() ) 0 totalLen) resultado de retorno;

// 1. Construir mapa de frecuencia de destino
Mapa seleccionadoString, Integer ratio target = new HashMap贸();
para (String w : palabras) {
target.put(w, target.getOrDefault(w, 0) + 1);
}

// 2. Iterate sobre todas las compensaciones posibles (0 ... wordLen-1)
for (int offset = 0; offset י wordLen; offset++) {}
int left = offset, right = offset;
Mapa seleccionadoString, Integer confianza ventana = nuevo HashMap Quería();
int used = 0; // number of words that are not over-used
exceso booleano = falso; // verdadero si la ventana tiene una palabra sobre usado

mientras (derecha + palabraLen) = s.length()) {}
// Agarra la siguiente palabra
Palabras clave = s.substring(right, right + wordLen);
derecho += palabra Len;

si (!target.containsKey(word) { // 3a. mala palabra reseteo
ventana.clear();
utilizado = 0;
exceso = falso;
izquierda = derecha;
continuar;
}

// 3b. añadir la palabra a la ventana
ventana.put(palabra, ventana.get OrDefault(palabra, 0) + 1);
si (ventana.get(palabra)
utilizado++;
. ♫ ... {
exceso = verdadero; // sobreutilizado
}

// 4. Arranque la ventana si es demasiado grande o contiene exceso
mientras que (derecha - izquierda == totalLen tención exceso) {
Pendiente izquierdaWord = s.substring(left, left + wordLen);
izquierda += palabra Len;
int cnt = window.get(leftWord) - 1;
ventana.put(izquierda, cnt);

si (cnt >= target.get(leftWord)) {
// Retirada una instancia de exceso
exceso = falso;
. ♫ ... {
usados...
}
}

// 5. Encontramos una ventana válida
si (utilizado == palabraCount " sensible !excess) {
result.add(left);
}
}
}
Resultado de retorno;
}
}
`` `

-...

### 2.2 Python 3

``python
de las importaciones de colecciones Contrato, predeterminado
de la importación Lista

Solución de clase:
def findSubstring(self, s: str, words: List[str]) List[int]:
si no s o no palabras:
retorno []

word_len, word_count = len(words[0]), len(words)
total_len = word_len * word_count
si len(s)
retorno []

target = Counter(words)
res = []

para offset in range(word_len):
izquierda = offset
derecho = compensación
ventana = defaultdict(int)
utilizado = 0
exceso = Falso

mientras que la derecha + word_len
palabra = s[right:right+word_len]
derecho += word_len

si palabra no en blanco:
# resetea la mala palabra
ventana.clear()
utilizado = 0
exceso = Falso
izquierda = derecha
continuar

# Add word
ventana[palabra] += 1
si ventana[palabra] 0 0 objetivo [palabra]:
usados += 1
más:
exceso = verdadero

# Encoge si es necesario
mientras que la derecha - izquierda == total_len o exceso:
left_word = s[left:left+word_len]
izquierda += word_len
ventana[left_word] -= 1

si ventana[left_word] target[left_word]:
exceso = Falso
más:
utilizado -= 1

si se usa == word_count y no exceso:
re.append(izquierda)

retorno
`` `

-...

### 2.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector asignadoint contacto encontrarSubstring(string s, vector asignado palabras clave) {
vector res;
si (s.empty()

int wordLen = words[0].size();
Intento palabra Cuenta = palabras.size();
int totalLen = wordLen * wordCount;
si (s.size() י totalLen) devolver res;

/ Mapa de frecuencia de destino
unordered_map detectstring, int contacto target;
para (continuar cadena w : palabras)
++target[w];

for (int offset = 0; offset י wordLen; ++offset) {}
int left = offset, right = offset;
unordered_map detectstring, int
int used = 0;
exceso de bool = falso;

mientras (derecha + palabraLen )= (int)s.size() {}
string word = s.substr (right, wordLen);
derecho += palabra Len;

si (!target.count(word)) { // mala palabra – reset
ventana.clear();
utilizado = 0;
exceso = falso;
izquierda = derecha;
continuar;
}

// añadir a la ventana
++ventana[palabra];
si (ventana [palabra]
++utilizados;
más
exceso = verdadero;

// encoger si ventana demasiado grande o exceso
mientras que (derecha - izquierda == totalLen tención exceso) {
string lWord = s.substr(left, wordLen);
izquierda += palabra Len;
-ventana[lWord];

si (ventana[lWord]
exceso = falso;
más
-utilizados;
}

si (utilizado == wordCount " sensible !excess)
res.push_back (izquierda);
}
}
restitución;
}
};
`` `

-...

## 3down El bueno, el malo, el ugly

Нели вы не вы вы вы вы вы вы вы вы не не ны вы не не не ны не не не ны не ны не ны не не ны не ны ны ны ны ны ны ны ны ны не ны ны ны ны ны ны ны ны ны ны ны ны ны не ны ны ны ны ны у ны ны ны ны ны ны не ны ны ны ны ны ны ны ны ны ны ны ны ны ны ны ны у 
Silencio--------------------------
Silencioso **La complejidad** Silencio Tiempo lineal, pequeña memoria
tención **Scalability** tención Handles 105‐length strings easily TEN ANTE TENIDO
Silencio **Readability** Silencio Comentarios claros, variables autoexplicativas
Silencio **Edge‐Case Safety** Silencio Manejas entradas vacías > cuerdas cortas TEN ANTE TENIDO
Silencio **Características del lenguajediomático** Silencio Java `Map`, Python `Counter`, C++ `unordered_map` ANTE ANTE TEN ANTE 
tención **Potential Pitfalls** Silencio fuera de lugar por uno bugs, olvidando restablecer en la mala palabra Silencio Evitar por pruebas rigurosas
Silencio **Debugging Aid** ← Iniciar sesión cada ventana encogimiento paso ← Ayuda a rastrear fallas

### Qué mantener en una entrevista de trabajo

* **Mostrar el *why*** – no solo suelte el código. Camine por la lógica de la ventana deslizante y por qué alcanza *O(n)*.
* **Hablar sobre casos de borde** – preguntar al entrevistador si las palabras pueden estar vacías o palabras de diferente longitud; mostrar cómo protegerías contra ella.
* **Explicar su elección de estructuras de datos** – por qué un mapa de hash, no un array.
* **Mención del bucle offset** – este es el truco que garantiza que no se pierda ninguna posición de inicio válida.

-...

## 4Ω⃣ SEO‐Optimized Title & Meta Description

### Title
■ ** Código de hoja #30: Eficiente “Subestring with Concatenation of All Words” – Java, Python & C++ Soluciones**

## Meta Descripción
■ Descubra una solución rápida y corredera para el código Leet #30. Lea el código Java detallado, Python y C++, pasee por el algoritmo, y aprenda cómo crear este problema “hard” en su próxima entrevista técnica.

-...

Pensamientos de clausura

La parte “buena” es la solución *linear* que mezcla elegantemente hash‐map seguimiento de frecuencia con una ventana deslizante avanzada por longitud de palabra.
La parte “mala” es la tentación de deslizar un personaje a la vez – que volaría hasta *O(n·wordLen)*.
La parte “muy” se encuentra en la gestión de palabras sobreutilizadas dentro de la ventana; es sutil, pero el bucle de frescura lo fija limpiamente.

Con estas implementaciones y la explicación adjunta, usted está listo para caer en una entrevista de trabajo y hablar con confianza a través del problema Leet Code 30. ¡Feliz codificación