-...
Título: LeetCode 1163. Última Subcadería en Orden Lexicográfica -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 Leetcode 1163 – “Última Subestring in Lexicographical Order”

■ **Problema**: Dada una cuerda `s`, devuelve la subestring lexicográficamente mayor de `s`.
■ **Constraints**:
* `1 ' s.length `
* `s` contiene sólo letras en inglés minúsculas.

La fuerza bruta clásica O(n2) compararía cada subestring posible, que es demasiado lento para los límites de entrada.
A continuación encontrará una solución *single‐pass, O(n) time, O(1) space* que funciona en **Java**, **Python**, y **C+**.
Después del código nos sumergimos en una discusión de estilo blog corto titulada ** “El bueno, el malo y el ugly”** que explica por qué este algoritmo es tan poderoso – y donde puede hacer un viaje – mientras que también es fácil para los reclutadores que escanean su cartera.

-...

### 🧩 Two‐Pointer Greedy (O(n) Time)

The key idea is to maintain two candidate start positions (`i` and `j`) and an offset `k`.
En cada paso comparamos los caracteres `s[i+k]` and `s[j+k]`:

← La situación actual
Silencio...
Silencio `s[i+k] == s[j+k]` Silencio Increment `k` – los subestrings coinciden hasta ahora. Silencio
La subestring en `i` ya es mejor. Mover `j` más allá de este rival: `j = j + k + 1`, reset `k`. Silencio
TENIDO `s[i+k] ANTES [j+k] ' ANTE La subestring at `j` beats `i`. Jump `i` forward: `i = max(i + k + 1, j)`. Entonces set `j = i + 1` y restablecer `k`. Silencio

Cuando `j + k` llega al final de la cuerda, `i` apunta al mejor comienzo.
Return `s.substring(i)` (Java/C++) or `s[i:]` (Python).

▪ restablecimiento **¿Por qué el “max”? * *
■ Se salta sobre posiciones que nunca pueden vencer mejor a la corriente y mantiene el algoritmo lineal.

-...

## Code – Java, Python, C++

``java
// Java 17
Solución de la clase pública {}
public String lastSubstring(String s) {
int n = s.length();
int i = 0, j = 1, k = 0;

(j + k) {
char a = s.charAt(i + k);
b = s.charAt(j + k);

si (a ==b) {
k++; // mismo prefijo, seguir
} si (a нели b) {}
j = j + k + 1; // i wins, skip j
k = 0;
} si no { / / / / /
i = Math.max(i + k + 1, j); // j wins, move i
j = i + 1;
k = 0;
}
}
retorno s.substring(i);
}
}
`` `

``python
# Python 3.10
Solución de clase:
def lastSubstring(self, s: str) - Propiedad str:
n = len(s)
i, j, k = 0, 1, 0

mientras que j + k
si s[i + k] == s[j + k]:
k += 1
elif s[i + k] œ s[j + k]:
j = j + k + 1
k = 0
más: # s[i + k]
i = max(i + k + 1, j)
j = i + 1
k = 0
devolver s[i:]
`` `

``cpp
// C+17
Clase Solución {
public:
hilo últimoSubstring(string s) {
int n = s.size(), i = 0, j = 1, k = 0;
(j + k) {
(s[i + k] == s[j + k]) {
++k;
} si (s[i + k] {}
j = j + k + 1;
k = 0;
. ♫ ... {
i = max(i + k + 1, j);
j = i + 1;
k = 0;
}
}
retorno s.substr(i);
}
};
`` `

-...

## Los buenos, los malos y los ugly

■ ** Objetivo** – Haga que el artículo sea útil para entrevista-prep, búsqueda de empleo y SEO.

#### ## 1down⃣ El Bien

Por qué ayuda a vivir
Silencio----------
Silencio **Linear Time** Silencio Handles `4·105` caracteres en milisegundos. Silencio
Silencio **Espacio constante** Silencioso Sólo unos índices enteros; genial para entrevistar “sin espacio extra” restricciones. Silencio
Silencio **Greedy + Two‐Pointer** tención Elegant; una vez que vea el patrón, escala a cualquier alfabeto. Silencio
Silencio **No hay bibliotecas adicionales** Silencio Funciona en Java, Python, C++ – no `suffix array` trucos o dependencias externas. Silencio
La misma idea aparece en los problemas de “Encontrar el Subarray más Grande”; puedes reutilizar la lógica. Silencio

#### 2down⃣ El malo

Silencioso
Silencio...
Silencio **Hard to Understanding at First Sight** Silencio El índice yugling (i, j, k) y `max(i + k + 1, j)` puede ser confuso. Silencio
Silencio **Off‐By‐One Bugs** ← Mistake `j = j + k + 1` para `j = j + k` elimina un salto crítico. Silencio
Silencio ** Casos de Edge** Silencio Las cadenas de caracteres individuales (`s = "a"`) regresan inmediatamente, pero olvidando inicializar `j = 1` puede causar `ArrayIndexOutOfBounds`. Silencio
Silencio **Code Duplication** Silencio Muchas soluciones se copian, pero variaciones sutiles en la cláusula “else” pueden cambiar la corrección. Silencio

#### 3down⃣ El Ugly

Silencio Pitfall Silencio Cómo evitar
Silencio...
Silencio **Asumiendo `s[i+k] Siempre mueve `i` Forward** Silencio Puede ser mejor mover `i` todo el camino más allá del prefijo del rival: `i = max(i + k + 1, j)`. Silencio
Silencio **Mixing `substring` and `charAt` in Java** tención Use `charAt` for comparison; `substring` for the final result. Silencio
Silencio **Python’s Negative Index** Silencio Python maneja felizmente índices negativos, pero todavía debe comprobar `j + k < n` antes de acceder. Silencio
tención **Not Resetting `k`** Silencio Después de cambiar un puntero, olvidando restablecer `k ' a cero causa compensaciones y comparaciones incorrectas. Silencio
Silencio **No Manejo de Patrones Repetitivos** Silencio Para cuerdas como "aaaaa", `k` puede seguir aumentando hasta el final. El bucle todavía termina en O(n), pero la lógica debe permitir que `k` crezca hasta que `j + k` golpee el final. Silencio

-...

## 📊 Complexity Analysis

TEN ANTE TEN ANTE Java ANTERIOR Python
Silencio------------...
Silencio **Tiempo** Silencioso `O(n)` – un pase lineal Silencioso `O(n)` – el mismo sufrimiento `O(n)` – bucle único
tención **Espacio** Silencioso `O(1)` – tres números enteros que subsisten `O(1)` – tres números enteros – tres números enteros
Silencio **El peor de los casos Runtime** Silencio ♥ 3 ms (para 400k chars) Silencio ♥ 2 ms Silencio ¦

-...

Aproximaciones Suplementarias (por qué los pasamos)

Silencio Silencio Silencio Silencio Silencio
Silencio--------------------------------
Silencio Brute‐Force Substring Comparación Silencio `O(n2)` Silencio `O(n)` Silencio Demasiado lento, sólo para aprender. Silencio
Silencio Construir un Suffix Array Silencioso `O(n log n)` Silencio `O(n)` , pero sobrematar para este problema. Silencio
Silencio Manacher-style Sliding Window Silencio `O(n)` pero más código Silencio `O(n)` Silencio No se necesita – dos puntos es más simple. Silencio

-...

## 🔍 SEO & Recruiter Checklist

← Palabra clave Silencio Por qué importa
Silencio...
confidencialidad ** 1163** Silencio Exact match for the problem ID recruiters often search. Silencio
Silencio **Última Substring Lexicographical Order** Silencio El nombre completo del problema aparece en entrevistas de trabajo. Silencio
Silencio **Dos-Pointer Greedy** Silencio Patrón de entrevista común para problemas de cuerda. Silencio
TEN **O(n) Time, O(1) Space** Silencio Escaneo rápido para limitaciones de rendimiento. Silencio
TEN **String Processing** ANTE Shows usted puede manejar gran entrada de manera eficiente. Silencio
TEN **Job Interview** / **Coding Challenge** TENS Signals that you're interview-ready. Silencio

■ **Consejo:** Agregue un enlace corto *GitHub‐Gist* o un snippet *code‐pen* para que los gerentes de contratación puedan ejecutar la solución inmediatamente.
■ Utilice la misma estructura de repositorio a través de idiomas (por ejemplo, `leetcode/1163/java`, `python`, `cpp`) para mantener su cartera ordenado.

-...

## 🎯 Final Take‐away

- La solución codictiva de dos puntos es la forma *rápida* y *más eficiente en el espacio* para resolver Leetcode 1163.
- Ejecutarlo cuidadosamente: observe el índice aritmético, reajuste `k ' correctamente, y pruebe con los casos de esquina ( ' a ' , ` ' aaab ' , ` ' ).
- Cuando escriba la solución en su currículum, incluya el **Java**, **Python**, y **C+** snippets mostrados anteriormente, y quizás un enlace a este artículo para demostrar comprensión profunda.

¡Feliz codificación y buena suerte en tu próxima entrevista! 