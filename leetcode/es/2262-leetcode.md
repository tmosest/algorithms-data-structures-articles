-...
Título: LeetCode 2262. Total Appeal of A String -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 Problem Recap – LeetCode 2262: *Total Appeal of a String*

Silencio
Silencio...
Silencio **Dificultad**
**Tipo** Silencioso String, Matemáticas, Programación Dinámica Silencio
← _Runtime Constraints** latitud `1 ≤ s.length ≤ 105` Silencio
Silencio **Apoyo de idiomas** viv Java, Python, C++

**Definición**

*The **appeal** of a string* = the number of **distinct** characters it contains.
Dada la cuerda `s`, devuelve el **sum de apelaciones** de **todo** posible subestring contiguo de `s`.

-...

Naïve Brute‐ Fuerza (y por qué es un *big no‐no*)

1. Enumerar todas las subestrings de `O(n2)`.
2. Para cada subestring, construye una 'Set' de sus personajes → `O(length)` trabajo.
3. Suma los tamaños.

**Hora** – `O(n3)` en el peor caso (por ejemplo, todos los caracteres son iguales).
**Espacio** – `O(1)` (además de conjunto temporal).

■ **Bad** – Esto explota rápidamente. Incluso 'n = 104' ya sería infesible.

-...

## 2down Insight: Contribución de un personaje

Piense en cada personaje 'c` independientemente.
¿Cuántas subestrings contienen esa ocurrencia particular de c?
Si podemos resumir estos relatos sobre todas las ocurrencias, obtenemos la respuesta.

### Observation

For an occurrence at index `i` (0‐based):

- Dejar `último[c]` ser el índice de la ocurrencia **previous** del mismo carácter.
(Si `c` no ha aparecido todavía, `último[c] = -1`.)
- Cualquier subestring que termine en el índice " i " y " comienza después de " la última frase " contendrá este `c`.

Número de subestrings
`` `
(i - last[c]) //
`` `

Así que la contribución de esta ocurrencia a la suma final es
`` `
(i - last[c]) * (n - i)
`` `
porque la subestring puede terminar en cualquier lugar de `i` a `n‐1`.

## Total Complexity

Atravesamos la cadena una vez, actualizando la última[26] y agregando la contribución para cada personaje.
Tanto **tiempo** como **espacio** son lineales/constant.

■ **Bien** – `O(n)` tiempo, `O(1)` espacio.

-...

## 3down ¿Por qué un 26-loop por personaje es *Ugly*

Una solución DP más simple mantiene un total de funcionamiento de las últimas posiciones de cada letra ( " última[26] " ) y las añade a través de un total interno " para (int k=0;k 0;k++) += i+1-last[k]`.
Eso es **`O(26 · n)`** – todavía lineal, pero el factor 26 puede dominar por muy grande `n`.
Además, el código es más difícil de leer y razonar.

-...

## 4down⃣ Final Elegant O(n) Solution (prev‐Occurrence trick)

Un punto de vista ligeramente diferente es mantener el llamamiento corriente para todas las subestrings que terminan en el índice `i`** (`cur`) y añadirlo al resultado mundial.

`` `
cur += (i + 1) - último[s] // nuevas subestrings que traen este char en el atractivo
[s[i] = i + 1 // +1 para que podamos empezar a contar a 1 en lugar de 0
res += curtido
`` `

Ambas variantes producen el mismo resultado; presentaremos ambos para la claridad.

-...

## 4VIEW⃣ Code – Three Languages

■ **Tip** – Todos los códigos están listos para funcionar en LeetCode, CodeChef, HackerRank, etc.

#### 4.1. Java 17

``java
// 2262. Llamamiento total de un String – Java
Clase Solución {
public long appeal Sum(String s) {
int n = s.length();
int[] last = nuevo int[26]; // última ocurrencia (+1). 0 significa “nunca visto”.
larga res = 0, total = 0;

para (int i = 0; i)
int idx = s.charAt(i) - 'a';
total += (i + 1) - último[idx]; // subestrings que recientemente incluyen este char
última[idx] = i + 1; // actualización a la posición actual (+1)
res += total; // todas las subestrings que terminan en i
}
restitución;
}
}
`` `

### 4.2. Python 3.10+

``python
# 2262. Llamamiento total de una cuerda – Python 3
de las colecciones importadas por defecto

Solución de clase:
def appeal Sum(self, s: str) - Propiedad int:
n = len(s)
último = defaultdict(lambda: -1)
res = 0

para i, ch in enumerate(s):
# (i - last[ch]) * (n - i) – contribución de este acontecimiento
res += (i - last[ch]) * (n - i)
último [ch] = i
retorno
`` `

#### 4.3. C+17

``cpp
// 2262. Llamamiento total de una cuerda – C+17
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
larga apelación Sum(string s) {}
int n = s.size();
vector implicado último(26, -1);
largas res = 0;
para (int i = 0; i) {}
int idx = s[i] - 'a';
res += 1LL * (i - last[idx]) * (n - i);
último[idx] = i;
}
restitución;
}
};
`` `

Los tres códigos funcionan en tiempo **O(n)**, **O(1)** memoria auxiliar.

-...

## 4down Edge‐ Lista de verificación de casos

TENIDO ANTERIENTE TENIDO Resultado esperado Por qué importa
Silencio...
Silencio Todas las mismas letras, por ejemplo, "aaaa" TENIDA `4*5/2 = 10` subestrings, each appeal `1` → suma `10` Silencio asegura que tratamos los duplicados correctamente TEN
Silencio Todo distinto, por ejemplo, `"abcd"` Silencio Llamamiento de cada subestring iguala su longitud tención prueba el *max* escenario de apelación Silencio
cuerda vacía – no permitida por las restricciones Silencio N/A TEN ANTE
Silencio Individual character, e.g. `"z" ' Silencioso de apelación `1`
Silencio Max longitud `105` cuerda al azar Silencio Debe terminar 0 0,5 s en LeetCode  durable stress‐test

-...

## 5down⃣ Quick Test Harness (Python)

``python
def brute(s):
n = len(s)
ans = 0
para i en rango(n):
visto = set()
para j en rango(i, n):
visto.add(s[j])
ans += len(seen)
Retorno

def test():
importación al azar, cadena
para n en rango(1, 50):
para _ en rango(100):
s = ''.join(random.choice('abc') for _ in range(n))
si brute(s) != Solución().appealSum(s):
print('Mismatch', s, brute(s), Solution().appealSum(s))
Regreso
print('Todas las pruebas pasadas!')

si __name_ == "__main__":
test()
`` `

-...

Conclusión - Lo que los entrevistadores quieren

- **Tiempo ineficiente**: `O(n)` soluciona el problema en la segunda vez incluso para 'n=105`.
- **Space‐light**: sólo un array de 26 o diccionario.
- **La elegancia matemática**: la contribución del personaje-por-character evita el desordenado DP o bucles.

■ **Bueno** – Sencillo, lineal, fácil de razonar.
■ **Bad** – Naïve set-based or DP with a 26‐loop per character – both are unnecessary.
■ **Ugly** – Super-ingenierar la solución o olvidar el truco +1 puede llevar a fuera-por-ones.

-...

## 📄 SEO‐Optimized Blog Article

### Title
■ **Master LeetCode 2262 – Total Appeal of a String peru Java, Python, C++ O(n) Solution**

## Meta Descripción
■ Solve LeetCode 2262 *Total Appeal of a String* in linear time. Aprende el truco de contribución de carácter con código Java, Python y C++. ¡Perfecto para la preparación de la entrevista!

-...

## 🚀 Blog Post

#### Introduction
Entrevistas amor problemas que disfrazan un patrón simple detrás de una etiqueta “Hard” deslumbrante. *Total Appeal of a String* es uno de esos clásicos. A pesar de su etiqueta 'Hard', la solución más eficiente es un algoritmo de un solo paso `O(n)` con memoria `O(1)`. Este post te recorre:

- Restablecimiento de problemas
- Ingenuas trampas
- La solución lineal **buena**
- La fuerza bruta cuadrática y cúbica
- La versión **ugly ** DP con 26-loop
- Códigos limpios (Java, Pitón, C++)
- Análisis de la complejidad
- Discusión por caso.
- Arnés de prueba rápido

-...

Declaración de problemas

■ **Aplicación** = número de caracteres distintos en una cuerda.
■ Por cada subestring contiguo de `s`, computar su apelación y resumir todos ellos.

Ejemplo: `s = "aba"
Subestrings → ``a', ``ab'`, ``aba', ``b', ``ba'`, ``a'`
Apelaciones → 1, 2, 1, 2, 1, 2, 1 → **Total = 9**.

-...

#### 2down⃣ Naïve Approach – The Big No‐No

``text
por cada uno en [0,n]
por cada j en [i,n]
construir conjunto de s[i.j]
ans += tamaño(set)
`` `

*Hora* → imposible para `n=105`.
- **Espacio** (ignorando el conjunto temporal).

Este es el clásico *exponential golpe-up* que debe evitar en entrevistas.

-...

#### 3down⃣ La visión “buena”: contribución de carácter

Considere cada ocurrencia de un personaje por separado.

1. `último[26]` contiene el índice de la última ocurrencia de cada carta (`-1` si no hay ninguna).
2. For the occurrence at index `i` of character `c`:
- Subestrings that **start after ** `last[c]` y **Adelante o después** `I` contiene este `c`.
- Número de comienzos: 'i - last[c]`.
- Número de extremos: `n - i`.
3. Contribución: `(i - last[c]) * (n - i)`.

Añadir esto por cada índice.

Resultado:** Escaneo lineal, espacio auxiliar constante.

■ **Por qué es *Good*** – No hay bucles anidados, no juegos caros, sólo aritmética entero.

-...

#### 4down⃣ El DP “Ugly” con un 26-loop

Un patrón común de DP:

``text
total = 0
para cada personaje:
total += i - última[c]
último[c] = i
`` `

Entonces, en cada iteración, suma todos los valores "últimos" a través de un "para" interno (k=0;k obtenidos26;k++) total += último[k]; `
Esto es **`O(26 · n)`**, todavía lineal pero el factor constante duele la legibilidad y el rendimiento.

■ **Ugly** – Añade bucles innecesarios y hace que la lógica sea más difícil de mantener.

-...

### 5down⃣ Full Code Snippets

Silencio Idioma Silencio Código Silencio
Silencio...
Silencioso **Java** Silencioso Haga clic para ver seleccionado/summary tituladapre clases Solución { indicabr título public long appeal Sum(String s) { indicabr título int n = s.length(); obtenidosbr confianza int[] last = new int[26]; identificadobr confianza long res = 0; armonizado para (int i = 0; i i i) se hizo n; ++i) {egr confianza int idx = s.charAt(i) - 'a'; Silencio
Silencio **Python** Нателенильныменниханиминыминыменниминамименными (s: ch: str) - > > > > > Silencio
tención **C+** Silencioso Click to view/summary contactospre clases Solution { didbr títulopúblico: Nombramiento largo de larga duraciónSum(string s) { no = s.size(); identificadobr título vector identificador último(26, -1); identificador de larga data = 0; identificador de última generación para (int i = 0; i Silencio

Todos los códigos compilan en LeetCode, CodeChef y otros jueces en línea.

-...

#### 6down⃣ Complexity Recap

- **Tiempo**: `O(n)` (paso único).
- **Espacio**: `O(1)` (diario o array de 26 centavos).
- ** Operaciones numéricas**: `1 × 106` multiplicaciones y agrega para 'n=105` – trivial en las CPU modernas.

-...

### 7 comentarios - Quick Python Script

``python
def brute(s):
# O(n^3) fuerza bruta para pequeñas cuerdas
...

def test():
importación al azar, cadena
para n en rango(1, 100):
para _ en rango(200):
s = ''.join(random.choice('abcd') for _ in range(n))
si brute(s) != Solución().appealSum(s):
print('Fail', s, brute(s), Solution().appealSum(s))
Regreso
print('All good!')

test()
`` `

Ejecute este script localmente para validar su implementación antes de enviar.

-...

#### 8down⃣ Final Takeaway

*Total Appeal of a String* te enseña que muchos problemas de “Hard” se reducen a un truco lineal oculto. Domine el patrón de distribución de caracteres, y responderá con confianza en Java, Python o C++ durante las entrevistas de codificación. Recuerde: buscar siempre una solución aritmética de paso único antes de recurrir a conjuntos o bucles anidados.

-...

#### 📚 Más lectura

- “Cracking the Coding Interview” – Carácter contando trucos
- “Problemas Duros LeetCode” – Capítulo de Reconocimiento Pattern
- “Coding Interview Prep” – O(n) tricks collection

¡Feliz codificación! 🚀

-...

El Pensamiento Final

Ya sea que esté haciendo frente a los desafíos de codificación o a las entrevistas técnicas, la lección de *Total Appeal of a String* es clara: busque el patrón aritmético **simple** detrás de un problema complejo, mantenga sus bucles apretados, y siempre busque el tiempo lineal. ¡Feliz entrevista!