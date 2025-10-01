-...
Título: LeetCode 1839. Substring más larga de todas las vowels in Order -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 1839 – “Longest Beautiful Substring”
### Good, Bad & Ugly: A Deep‐Dive into Vowel‐ Subestrings de pedidos (Java / Python / C++)

■ **TL;DR** – Escanear la cadena una vez con una *gran estrategia de dos puntos*.
■ Tiempo: **O(N)**, Espacio: **O(1)**.
■ Se proporcionan tres soluciones listas a paso (Java, Python, C++).

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

■ ** Entrada** - Una palabra de cadena que contiene sólo las cinco vocales: `a, e, i, o, u`.
■ ** Objetivo** – Devuelve la longitud de la subestring más larga contigua que
■ 1. Contiene **todas** cinco vocales ** al menos una vez**.
■ 2. Aparece en orden alfabético restringido** (`a...e...o...u`).

Si no existe tal subestring, regrese `0`.

■ *Examples*
*`aeiaaioaaaeiiiiouuuooaauuaeiu`* → **13** (`aaaaaeiiiiouuu ' )
*`aeeeiiiioooauuuaeiou`* → **5** (`aeiou`)
*`a`* → **0**

-...

#### 2down⃣ "Bad" Brute‐ Enfoque de la Fuerza

La solución más intuitiva es generar *todo* subestring, comprobar las dos condiciones y mantener el más largo.
``text
para mí en [0.n-1]:
para j in [i+1..n]:
sub = word[i:j]
si esBeautiful(sub): best = max(best, len(sub))
`` `
*Por qué es malo*

TEN TERRITORIO TERRITORIO TERRITORIO
Silencio...
Subestrings O(N2) TENIDO Demasiado lento para `n = 5·105` Silencio
Silencio O(N) por cheque Silencio Todavía O(N3) en general
Silencio Alta memoria de arriba Silencio Subestring allocation ←

Incluso con optimistas no pasará los límites de tiempo de LeetCode.

-...

#### 3down⃣ La estrategia óptima “buena”

#### Core Insight
Mientras iteramos, podemos *reestablecer* cuando la orden de vocal se rompe.
Una subestring es válida **sólo** si avanza en la secuencia de vocales.
Por lo tanto, un solo escaneo lineal basta.

##### Sliding‐Window + Greedy

Silencio Variable Silencio Significado
Silencio...
Silencio `izquierda` Silencio Índice de inicio de la subestring actual candidata
Silencioso `stage` Silencio cuántas vocales distintas hemos visto en orden (1...5)
Silencio `ans` Silencio Longest beautiful substring length found so far

*Algorithm*

`` `
ans = 0
izquierda = 0
etapa = 1 // hemos visto al menos una 'a' en posición 0

para mí de 1 a n-1:
si palabra[i] cautiva palabra[i-1]: // orden roto → nueva ventana
etapa = 1
izquierda = i
si la palabra [i] не palabra[i-1]: // pisamos la siguiente vocal
etapa += 1

si etapa == 5: // hemos visto a
as = max(ans, i - izquierda + 1)

Retorno
`` `

**Por qué funciona* *

- ¿Qué? Si la vocal actual es *menos* que la anterior, la subestring no puede continuar; debemos empezar de nuevo en `i`.
-Progreso**: Si es *mayor*, nos movemos a la siguiente etapa vocal.
- **Repetición**: Los personajes iguales ( " a " → " ) no cambian el escenario; simplemente alargan la ventana actual.
- Todo listo. Cuando `stage` alcanza 5 sabemos que la ventana contiene las cinco vocales en orden, así que comparamos su longitud.

-...

### 4VIEW⃣ Code Implementations

■ **Tip** – Todas las soluciones funcionan en *O(N)* tiempo, *O(1)* espacio extra, y manejan el tamaño máximo de entrada sin esfuerzo.

#### 4.1 Java (Readable, Constant‐Space)

``java
Solución de la clase pública {}
int longestBeautifulSubstring(String word) {
int ans = 0, izquierda = 0, etapa = 1; // etapa 1 significa que ya tenemos una 'a'

para (int i = 1; i) i++) {
char prev = word.charAt(i - 1);
char curr = word.charAt(i);

si (currir)
etapa = 1;
izquierda = i;
} si (correo > prev) { // siguiente vocal
etapa++;
}
si (etapa == 5) {
as = Math.max(ans, i - izquierda + 1);
}
}
devolver los ans;
}
}
`` `

##### 4.2 Python (Elegant & Fast)

``python
Solución de clase:
def longestBeautifulSubstring(self, word: str) int:
ans = izquierda = 0
etapa = 1 # 1 - título 'a', 2 - título 'e', ... 5 - título 'u'

para i en rango(1, len(word)):
prev, cur = word[i-1], word[i]
Si se curan, se hace una rotura
etapa, izquierda = 1, i
elif cur > prev: # move to next vocal
etapa += 1

si la etapa == 5: # todas las vocales vistas
as = max(ans, i - izquierda + 1)

Retorno
`` `

##### 4.3 C++ (Fast & Memory‐Efficient)

``cpp
Clase Solución {
public:
int longestBeautifulSubstring(string word) {
int ans = 0, izquierda = 0, etapa = 1; // etapa cuenta las vocales en orden

para (int i = 1; i) ++i) {
char prev = word[i-1];
char cur = word[i];

si (curo < prev) { // reset
etapa = 1;
izquierda = i;
} si (cuerdo > prev) { // pasar a la siguiente vocal
++etapa;
}

si (etapa == 5) {
ans = max(ans, i - left + 1);
}
}
devolver los ans;
}
};
`` `

-...

#### 5down⃣ Casos de borde & Gotchas

Silencio Caso confidencialidad ¿Por qué importa?
Silencio...
Silencioso **Single vocal** (por ejemplo, `'a'` o `'uuuuuu'''') Silencio No beautiful substring  Return `0` automatically (loop never hits `stage == 5 " )
Silencio **La ventana desactivada en el centro** Silencioso El restablecimiento de la orden también debe reajustar `stage` ¦
Silencio **Las vocales Duplicadas** Silencio No progresan `stage` Silencio Mantén `stage` sin cambios cuando `cur == prev` Silencio
Silencio **Introducción alta** Silencio Seguridad de la memoria Silencioso Usar índices, no subestring objetos

-...

Resumen de la complejidad

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Silencio en Java **O(N)** Silencio **O(1)**
TENIDO Python TENIDO **O(N)** TENIDO **O(1)**
Silencio C++ Silencio **O(N)** Silencio **O(1)**

`N` = `word.length()` (≤ 5·105)

-...

### 7П⃣ Entrevista común Pitfalls

1. **Asumiendo “contiene todas las vocales” → “contiene cada una al menos una vez”**
Sea explícito que cada vocal debe aparecer y el orden importa.

2. **Using `set` or `HashMap` for each window* *
Eso sería O(N2) en el peor caso. El escaneo codicioso es la solución prevista.

3. **Optimización con regex**
Las expresiones regulares pueden ser elegantes pero son difíciles de justificar en una entrevista.

4. **Descubriendo el caso de reajuste**
Olvídate de reajustar el escenario cuando el orden se rompe lleva a respuestas incorrectas.

-...

### 8️ Take‐aways for Your Next Coding Interview

- **Empieza con un plan de fuerza bruta** - aclara las limitaciones.
- **Busca los escaneos de tiempo lineal** – la mayoría de los problemas de cuerda con las restricciones de orden se reducen a un solo paso.
- **Las máquinas estatales importan** – `escena` es esencialmente una pequeña máquina de estado finito que rastrea el progreso a través de la secuencia vocal.
- **La legibilidad de la ley es clave** – incluso un línea en Python debe tener comentarios claros para los entrevistadores.
- **Tiempo-espacio-offs** – aquí guardamos la memoria mínima porque el tamaño de entrada es enorme.

-...

#### 9down⃣ Otros recursos

Enlace permanente Lo que ofrece
Silencio...
[LeetCode 1839](https://leetcode.com/problems/longest-substring-of-all-vowels-in-order/) Página de problemas con casos de prueba
Silencio [Java Solution – Constant Space](https://leetcode.com/problems/longest-substring-of-all-vowels-in-order/solutions/1175715/java-readable-code-constant-space-by-him-eip2/) solución original de Himanshu Chhikara Silencio
[Versión Pitón – Ventana de deslizamiento de Greedy](https://leetcode.com/problems/longest-substring-of-all-vowels-in-order/solutions/6798204/sliding-window-easy-by-vivek011299-jv7q/) Silencio Clean Python code Silencio
Silencio [C+++ Versión – O(N) Two‐Pointer](https://leetcode.com/problems/longest-substring-of-all-vowels-in-order/solutions/6622943/longest-beautiful-substring-c-solution-t/) Silencio rápido y conciso

-...

## 📌 Final Verdict

El problema de la “subordinación hermosa” es un ejemplo perfecto de cómo un escaneo codicioso simple* convierte una pesadilla O(N2) en una brisa O(N).

Copie uno de los tres fragmentos de código, envíelo, y obtendrá **AC** en LeetCode 1839 en milisegundos.

Buena suerte – y que su entrevista sea tan ordenada como una secuencia de vocales “beltas”! 🚀

-...

■ **Author** – *Stack‐Overflow " LeetCode entusiasta, convirtiendo constantemente problemas desconcertantes en código limpio y eficiente. *
■ **Contacto** – GitHub: `@codingwizard` Silencio LinkedIn: `linkedin.com/in/codingwizard `

-...

■ *Si te gustó este post, estrella el repo, compartir con amigos, y dejar un comentario si lo encontró útil! *
-...

``diff
# Fin del blog
`` `