-...
Título: LeetCode 2914. Número mínimo de cambios para hacer la cuerda binaria hermosa -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código – LeetCode 2914 “Número mínimo de cambios para hacer hermosa la cuerda binaria”

El problema se reduce a correcciones **pair-wise**.
Para una cadena binaria de longitud uniforme `s = s0 s1 ... s(n-1)` podemos dividirlo en
subestrings of length 2:
`(s0,s1) Silencio (s2,s3) Silencio ...`.
Cada par debe convertirse en todo-cero o todo-uno.
Cambiar un personaje en un par arregla todo el par, por lo que la estrategia óptima
es:

`` `
respuesta = número de pares adyacentes (si,si+1) donde si != si+ 1
`` `

Ese es el número mínimo de vueltas requeridas.

A continuación se muestran soluciones limpias, O(N) en **Java**, **Python** y **C+**.

-...

## Java

``java
// LeetCode 2914 – Número mínimo de cambios para hacer hermosa la cuerda binaria
Clase Solución {
public int minChanges(String s) {
cambios de entrada = 0;
// iterate por pasos de 2 – mira cada par
(int i = 0; i) s.length(); i += 2) {
// si los dos caracteres difieren necesitamos una vuelta
si (s.charAt(i) != s.charAt(i +1) {
cambios++;
}
}
cambios de retorno;
}
}
`` `

-...

## Python

``python
# LeetCode 2914 – Número mínimo de cambios para hacer hermosa la cuerda binaria
Solución de clase:
def minCambios(self, s: str) - int:
cambios = 0
para i en rango(0, len(s), 2):
si s[i] s[i + 1]:
cambios += 1
Cambios de retorno
`` `

-...

### C++

``cpp
// LeetCode 2914 – Número mínimo de cambios para hacer hermosa la cuerda binaria
Clase Solución {
public:
int minChanges(string s) {
cambios de entrada = 0;
para (int i = 0; i) i += 2) {
si (s[i]!= s[i + 1]) ++cambios;
}
cambios de retorno;
}
};
`` `

Las tres soluciones funcionan en tiempo **O(n)**, uso **O(1)** espacio adicional, y
conforme a la firma esperada de LeetCode.

-...

## 2. Blog Artículo – “LeetCode 2914: The Beautiful Binary String – Good, Bad, & Ugly”

■ **SEO Palabras clave**: *LeetCode 2914, cambios mínimos, hermosa cadena binaria, entrevista de codificación, solución de algoritmo, solución Java, solución Python, solución C++, algoritmo codicioso, corrección de pareja, prep de entrevista*

-...

################################################################################################################################################################################################################################################################ ¿Cuál es el problema?

En LeetCode “Minimum Number of Changes to Make Binary String Beautiful”
(Problema 2914) se le da una cadena binaria de longitud uniforme `s`.
Una cuerda es hermosa si puedes dividirla en subestrings, cada uno:

* Incluso longitud (así que la división siempre estará en pares de dos caracteres)
* All‐zero o todo uno.

Puede cambiar cualquier personaje.
Regrese las volteretas *mínimo* necesarias para que toda la cuerda sea hermosa.

-...

### 🧠 Intuition – The Pair‐Wise Greedy

Debido a que cada subestring debe tener incluso longitud, la división natural está en * pares adyacentes*:

`` `
s0 s1 Silencio s2 s3 Silencio ... Silencio s(n-2) s(n-1)
`` `

Si un par ya contiene dos partes iguales (00 o 11), estamos bien.
Si no (01 o 10), *debemos girar* **exactamente uno** de los dos pedazos para hacer el par hermoso.
Las vueltas en diferentes pares no interfieren entre sí, por lo que el óptimo
La estrategia es simplemente:

■ Cuente cuántos pares han desajustado bits; eso cuenta es la respuesta.

No hay DP, no hay retroceder, no se necesita ninguna codicioso “mirar a la cabeza”.
Es por eso que este problema tiene una solución puramente codictiva**.

-...

#### 📈 Complexity Analysis

Silencio Silencio Silencio Silencio Silencio
Silencio...
Solución vocalada **O(n)** – un paso sobre la cuerda voca **O(1)** – sólo una contrarrespuesta
Silencio Donde `n = s.length()` Silencio

Con 'n ≤ 105', esto funciona en microsegundos en todos los idiomas principales.

-...

#### 🛠ف Implementation – “Good” Code

A continuación se presenta la aplicación *limpio y listo para la producción* en tres idiomas.

*Java*

``java
Clase Solución {
public int minChanges(String s) {
cambios de entrada = 0;
(int i = 0; i) s.length(); i += 2) {
si (s.charAt(i) != s.charAt(i + 1)) cambia++;
}
cambios de retorno;
}
}
`` `

*Python*

``python
Solución de clase:
def minCambios(self, s: str) - int:
cambios = 0
para i en rango(0, len(s), 2):
si s[i] s[i+1]:
cambios += 1
Cambios de retorno
`` `

*C++*

``cpp
Clase Solución {
public:
int minChanges(string s) {
cambios de entrada = 0;
para (int i = 0; i) i += 2)
si (s[i] != s[i+1]) ++cambios;
cambios de retorno;
}
};
`` `

Cada versión:

* Maneja la garantía de longitud uniforme con seguridad
* Usa un simple "para" bucle que pasos por dos
* Realiza un solo cheque por par

-...

### ## Гливали "Bad" Pitfalls to avoid

Silencio Pitfall Silencio ¿Por qué es malo
Silencio...
Silencio **Iterating over every character** (`i+` en lugar de `i+=2`) Silencio Parejas de doble cuenta y añadir comparaciones innecesarias. Silencioso Uso `i += 2 ` por lo que cada par es inspeccionado sólo una vez. Silencio
Silencio **Flipping the wrong bit** (e.g., always change the first bit) Silencio Un único `si` cheque es suficiente; no hay necesidad de decidir *que* bit to flip. Silencio
Silencio **Asumiendo que la cadena puede ser de extraña longitud** Silencio LeetCode garantiza incluso la longitud, pero un cheque adicional podría costar O(1) tiempo extra sin ningún beneficio. Silencio Confía en las limitaciones del problema; evita la validación extra. Silencio
TEN **Usando una cadena mutable o array innecesariamente** TEN En Java/C++ esto podría asignar nueva memoria cada bucle. Trabajar con `charAt` / indexación de matriz; mantener la huella de memoria constante. Silencio

-...

### 🤡 "Ugly" Anti-Patterns

Silencio Anti‐Pattern Silencio Por qué es feo TENIDO Ejemplo TENIDO
Silencio...
Silencio **Recusión con el uso de pilas pesadas** Silencio Una solución recursiva ingenua podría golpear el desbordamiento de la pila para `n = 105`. Rec (String s, int idx)` que se llama por cada par. Silencio
Silencio **Using regex or string splits** Silencio Splitting the string into pairs and then check each pair is overkill. Silencioso `s.split(...)") o `Pattern.compile("(? made=.)(?=.)" etc. Silencio
Silencio **Copiar la cuerda en cada iteración** Silencio `s = s.replace(...)` dentro de un bucle crea nuevas cuerdas cada vez. Mantener la cuerda original intacta; sólo contar con desajustes. Silencio
Silencioso ** Índices de codificación de riesgo** Silencioso `si (s[0] != s[1]) ... ` luego repetir para todos los pares manualmente. Use un bucle para generalizar. Silencio

-...

### 🚀 Take‐aways for Interviewees

1. **Reconozca el patrón** – “Hasta la longitud → dividido en pares” sugiere inmediatamente un escaneo lineal.
2. **Gran corrección** – Cada par es independiente; una fijación local es globalmente óptima.
3. **Tiempo/Espacio** – O(n)/O(1) es más que suficiente; no hay necesidad de estructuras de datos elegantes.
4. **Edge Cases** – La cadena siempre es uniforme; el algoritmo naturalmente maneja “todos los ceros” o “todos” con cero cambios.
5. *Testing** – Cover:
* Todos los pares iguales → 0 cambios
* Todos los pares diferentes → n/2 cambios
* Alternating 0101... → N/2 cambios
* Mezclas aleatorias → computar manualmente

-...

#### 📚 Más lectura

* ** Algoritmos de granedía** – Entender cuando las opciones locales conducen a un óptimo global.
* ** Programación Dinámica** – Para problemas de partición más complejos; aquí el DP sería exagerado.
* **LeetCode Discuss – Problema 2914** – Muchos contribuyentes comparten variaciones y pruebas alternativas.

-...

Veredicto final

*Bien*: Un paso a un lado, un contador a dos es la solución óptima.
*Bad*: Sobre-ingeniería, bucles innecesarios o copias mutables pierden tiempo y espacio.
*Ugly*: Recursión, regex o índices codificados duros hacen que el código sea difícil de leer y mantener.

Con los fragmentos de código arriba, usted puede enviar con confianza a LeetCode, as the interview, y mostrar su capacidad para detectar la elegante solución avaricia. ¡Feliz codificación!