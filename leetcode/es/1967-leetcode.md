-...
Título: LeetCode 1967. Número de cuerdas que aparecen como subestrings en Word -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 1967 – “Número de cuerdas que aparecen como subestrings en Word”

■ **Problema** Silencio fácil Silencio 1967 Silencioso [LeetCode](https://leetcode.com/problems/number-of-strings-that-appear-as-substrings-in-word/)

■ ** Objetivo** – Dado un conjunto de cuerdas `patterns ' y una cadena `palabra ' , contar cuántas cadenas en `patterns ' ocurren como una subestring en `palabra ' .

■ *Por qué importa* – Esta es una pregunta de entrevista clásica que prueba su comprensión de la manipulación de cuerdas, el método 'contiene', y cómo mantener la solución simple pero eficiente. Dominarla aumentará sus posibilidades de romper la porción * de las entrevistas técnicas.

-...

## 📑 Declaración de problemas (formulario)

``text
Entrada: patrones: String[] (1 ≤ patrones.length ≤ 100)
palabra: cuerda (1 ≤ word.length ≤ 100)
Todos los personajes son letras inglesas minúsculas.

Producto: int – el número de patrones que aparecen como subestring contiguo en palabra.
`` `

#### Sample

pautas de confidencialidad Silencio palabra Silencio
Silencio--------------
Silencioso ["a", "abc", "bc", "d"]
Silencio ["a", "b", "c"]
Silencioso ["a", "a", "a"

-...

## 🧠 Approach – The Good, The Bad, and The Ugly

Silencio Silencio Silencio Silencio Silencio Silencio
Silencio--------------...
Silencio **Brute‐force `contains`** Silencio *(n·m)* tiempo (n patterns, m words) – perfecto para las limitaciones. No hay estructuras de datos adicionales. El escaneo repetido puede ser costoso para datos más grandes. ← N/A – demasiado simple. Silencio
Silencio **Pre-build a Suffix Trie/Automaton** Silencio Puede responder a muchas consultas en *O(1)* después del preprocesamiento. Bien por grandes 'patterns' y repetidos `palabra's. Uso de memoria pesada (~O(m2)). - No. tención Código complejo, propenso a errores. Silencio
Silencio **KMP/Two‐Pointer por patrón** tención Linear por patrón en la longitud del patrón + palabra. <br título Evita el costo de `contienes `caso peor. Silencio Todavía *O(n·m)* en general. Silencio

■ **Bottom line:** El enfoque bruto-fuerza usando 'String.contains()` de Java, Python's `in`, o C++ ́s `find()` es el más *práctico* para este problema. Le da la respuesta correcta, corre en microsegundos para los límites dados, y demuestra un estilo de codificación limpio, exactamente lo que buscan los entrevistadores.

-...

## 🛠ح Code Implementations

A continuación se presentan implementaciones limpias y listas para funcionar en **Java**, **Python**, y **C+**. Cada solución sigue la misma lógica: gira sobre cada patrón, comprueba si es una subestring de `palabra ' y aumenta un contador.

■ **Nota** – El código incluye un pequeño `main`/`if __name_ == "__main__":` bloque para pruebas rápidas. En un entorno de LeetCode sólo se necesita la clase o función de `Solution ' .

-...

### 1. Java

``java
importar java.util*;

Solución de la clase pública {}
*
* Cuenta cuántos patrones aparecen como subestrings en palabra.
*
* Patrones de @param Array of candidate patterns.
* @param word La cadena de destino.
* @return Número de patrones que son subestrings de palabra.
*/
public int numOfStrings(String[] patterns, String word) {
int count = 0;
para (String patrón : patrones) {}
si (palabra.contiene(pattern)) { // O(m) para cada patrón
contar++;
}
}
recuento de retorno;
}

Demo rápido...
public static void main(String[] args) {
Solución sol = nueva solución ();
System.out.println(sol.numOfStrings(
nuevo String[]{"a", "abc", "bc", "d"},
"abc"); // 3

System.out.println(sol.numOfStrings(
nuevo String[]{"a", "b", "c"},
"aaaaabbbbb"); // 2

System.out.println(sol.numOfStrings(
nuevo String[]{"a", "a", "a"},
"ab"); // 3
}
}
`` `

**Las complejidades* *

Silencio Silencio Silencio Silencio Silencio
Silencio...
Ø 100, m ≤ 100) Silencio **O(1)** (sin importar el tamaño de la entrada)

-...

### 2. Pitón

``python
de la importación Lista

Solución de clase:
def numOfStrings(self, patterns: List[str], word: str) int:
"
Cuenta patrones que aparecen como subestrings en palabra.

:Padres parambólicos: List[str] – cadenas de candidatos.
:param word: str – target string.
: retorno: int – cuenta de patrones de coincidencia.
"
Conteo = 0
para Pat en patrones:
si se dice: # Python's substring check
Cuenta += 1
cuenta de retorno

Demo rápido...
si __name_ == "__main__":
sol = Solución()
print(sol.numOfStrings(["a", "abc", "bc", "d"], "abc")
print(sol.numOfStrings(["a", "b", "c"], "aaaaaabbbbb") # 2
print(sol.numOfStrings(["a", "a", "a"], "ab")
`` `

**Las complejidades* *

Silencio Silencio Silencio Silencio Silencio
Silencio...
Silencio general **O(n · m)** Silencio **O(1)**

-...

### 3. C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int numOfStrings(vector identificadostring consigo patrones, palabra de cuerda) {
int count = 0;
for (const cordón palm : patterns) {}
si (pat.find(pat) != string::npos) { // O(m) por patrón
++cuenta;
}
}
recuento de retorno;
}
};

Demo rápido...
int main() {}
Sol de solución;
vector iniciador p1 = {"a", "abc", "bc", "d"};
cout se realizó el sol.numOfStrings(p1, "abc")

vector realizador titular p2 = {"a", "b", "c"};
(p2, "aaaaabbbbb")

vector realizador titular p3 = {"a", "a", "a"};
cout se realizó el sol.numOfStrings(p3, "ab")

retorno 0;
}
`` `

**Las complejidades* *

Silencio Silencio Silencio Silencio Silencio
Silencio...
Silencio general **O(n · m)** Silencio **O(1)**

-...

## 🔍 Deep Dive – Why Esto funciona

1. ** Comprobación de la substancia** ( " contenedores " / " , ya es una operación **en tiempo lineal**: explora la palabra " hasta que encuentre `pattern ' o llegue al final.
2. Desde la longitud de la palabra ≤ 100, incluso el peor escaneo de cada patrón es trivial para las CPU modernas.
3. El algoritmo es *stable* – maneja correctamente patrones duplicados (como `["a", "a","a"]) porque cada ocurrencia se cuenta por separado, coincidiendo con el requisito del problema.

-...

## 📈 Alternatives – When to Go Bigger

Silencio Escenario Silencio Estrategia recomendada
Silencio----------------------------
Silencio **Large `patterns` array** (tens of thousands) tención Build a **Trie** or **Aho‐Corasick automaton** for patterns and run a single scan of `word`. Silencio O(longitud total del patrón + longitud de la palabra)
Silencio **Muy larga `palabra'** (millones de chars) ← Utilizar un **Suffix Automaton** o **Suffix Array** para responder a las consultas de existencia subestring en *O(1)* después del preprocesamiento de O(m). TENIDO O(m) preprocesamiento, O(1) consultas TENIDO
Silencio **Preguntas relativas a la misma `palabra'** Silencio Preproceso `palabra` en un sufijo trie/automaton una vez, y luego comprueba todos los patrones en *O(1)* cada uno.

■ *Pero* para las limitaciones de LeetCode, la solución sencilla `contiene' es la más concisa y pasa cómodamente.

-...

## 📌 Takeaways for Interview Success

- **Lea las limitaciones primero.** Un pequeño tamaño de entrada a menudo permite una solución simple.
- **Explicar el tiempo de su solución / cambio de espacio.** A los entrevistadores les encanta ver que pueden justificar sus elecciones.
- Casos de borde de mención. Patrones duplicados, cuerdas vacías (si se permite), y la diferencia entre subestring y subsequence.
Mantén el código limpio y comentado. Una solución ordenada refleja el profesionalismo.

-...

Resumen optimizado

¿Buscando aterrizar un papel de ingeniería de software? Mastering LeetCode #1967 “Número de cuerdas que aparecen como subestrings en Word” es una victoria rápida. El problema prueba habilidades básicas de búsqueda de cuerdas y su capacidad de escribir código claro y eficiente. Nuestra guía ofrece:

- Imitir Java, Python y C++ implementaciones
- 📚 Razonamiento paso a paso: por qué `contiene' es suficiente
- Análisis de complejidad para discutir en entrevistas
- Consejos sobre cuándo escalar con intentos o sufijo automata

Use este artículo como su compañero de preparación de entrevistas e impresione a los reclutadores con sus chuletas de codificación y su pensamiento estratégico. ¡Feliz codificación!

-..