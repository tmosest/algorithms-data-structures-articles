-...
Título: LeetCode 76. Substring de ventana mínima -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1. LeetCode 76 - Subproducción de ventana mínima
** Objetivo** – Encuentra la subestring más pequeña de `s` que contiene cada carácter de `t` (incluyendo duplicados).
*La complejidad* La solución óptima funciona en el tiempo **O (las vidas eternas + TENT)** y **O(1)** espacio auxiliar (128-tamaño para ASCII).

A continuación encontrará código completo, listo para la producción en **Java**, **Python**, y **C++** que satisface las limitaciones (las vidas eternas, tención eterna ≤ 105).
Después del código encontrarás un artículo de blog amigable de SEO que explica el problema, el clásico análisis “bueno-bad-ugly” y cómo se destaca esta solución en una entrevista de trabajo.

-...

## 2. Código de Solución

#### 2.1 Java

``java
*
* LeetCode 76 - Subproducción de ventana mínima
* O(sobrevivirles) tiempo, espacio O(1) (tamaño ASCII 128).
*/
Solución de la clase pública {}

public String minWindow(String s, String t) {
si (s == null TENIDO T == null ANTERITO TENIDO S.length() {}
devolver ";
}

// Frecuencia de cada char en t
int[] need = new int[128];
for (char c : t.toCharArray())) necesidad[c]+;

int left = 0, right = 0;
int missing = t.length(); // number of chars still needed
int minLen = Integer.MAX_VALUE;
int minStart = 0;

char[] sArr = s.toCharArray();

mientras (derecha)
char c = sArr[right++];
si (necesita[c] 0) desaparecidos--; // encontramos un char necesitado
necesidad[c]--; // consumirlo

// Cuando todos los charcos estén satisfechos, trate de reducirse de la izquierda
mientras que (perdiendo == 0) {
si (derecha - izquierda - minLen) { // Actualizar mejor ventana
minLen = derecha - izquierda;
minStart = izquierda;
}
char izquierda Char = sArr[left++];
necesidad[izquierda] Char]++; // volver
si (necesita[leftChar] 0) desaparecidos++; // perdimos un char necesitado
}
}

volver minLen == Integer.MAX_VALUE
"
: s.substring(minStart, minStart + minLen);
}
}
`` `

### 2.2 Python

``python
"
LeetCode 76 – Subestringe de ventana mínima
Tiempo: O(len(s) + len(t))
Espacio: O(1) (128 array tamaño)
"

Solución de clase:
def minWindow(self, s: str, t: str) - confía str:
si no s o no t o len(s)
"Regresa"

* 128
por ch en t:
necesidad[ord(ch)] += 1

izquierda = 0
desaparecidos = len(t)
min_len = len(s) + 1
min_start = 0

s_chars = list(s)

por derecho, ch in enumerate(s_chars, 1): # derecha es exclusiva
si es necesario[ord(ch)] 0:
desaparecidos -= 1
necesidad[ord(ch)] -= 1

mientras falta == 0:
si a la derecha - izquierda
min_len = derecha - izquierda
min_start = left
left_ch = s_chars[left]
necesidad[ord(left_ch)] += 1
si es necesario[ord(left_ch)] 0:
desaparecidos += 1
izquierda += 1

volver "" si min_len √≥ len(s) else s[min_start:min_start + min_len]
`` `

### 2.3 C++

``cpp
*
* LeetCode 76 - Subproducción de ventana mínima
* O(n + m) tiempo, espacio O(1) (tamaño ASCII 128).
*/
Clase Solución {
public:
hilo minWindow(string s, string t) {}
si (s.empty()
devolver ";

int need[128] = {0};
para (cara c : t) necesidad[(int)c]++;

int left = 0, right = 0;
int missing = t.size(); // chars still required
int minLen = INT_MAX;
int minStart = 0;

mientras (derecho) {}
char c = s[right++];
(necesita [(int)c] 0) desaparecidos...
necesidad [(int)c]--; // consumir

// Encoger mientras todos los charcos necesarios están en la ventana
mientras que (perdiendo == 0) {
si (derecha - izquierda - minLen) {
minLen = derecha - izquierda;
minStart = izquierda;
}
char lc = s[left++];
necesidad [(int)lc]++; //
(necesita [(int)lc] 0) desaparecidos++;
}
}

volver minLen == INT_MAX ? " : s.substr(minStart, minLen);
}
};
`` `

■ **Tip** – El array `neced` es siempre 128 elementos largos (ASCII).
■ Si necesita apoyar Unicode, reemplacelo con un `HashMap observadoCharacter, Integer confianza` y el algoritmo se mantiene igual, sólo el espacio constante se convierte en *O(presente a la vida)*.

-...

## 3. Blog Artículo – “Minimum Window Substring” (SEO-friendly)

■ *Título*
■ **Minimum Window Substring – LeetCode 76 Solución de ventana en Java, Python & C++ ← O(n) Time, O(1) Space**

■ **Descripción de los datos**:
■ Aprende el clásico LeetCode 76 Problema de Subestring de Ventana Mínima, por qué el enfoque de ventanilla deslizante es el estándar de oro, y cómo llegar a esta pregunta en una entrevista de ingeniería de software. Código en Java, Python y C++ incluidos.

-...

### 3.1 Introducción

■ El *Minimum Window Substring* (LeetCode 76) es uno de los rompecabezas de entrevista más comunes que prueba la capacidad de un candidato para aplicar la técnica **sliding‐window**.
■ Dado un texto `s` y un patrón `t`, el objetivo es encontrar la subestring más corta de `s` que contiene todos los caracteres de `t`, ** incluyendo multiplicidades**.
■
■ En una entrevista de trabajo, los entrevistadores aman este problema porque:
■ 1. Te obliga a pensar en dos puntos.
■ 2. Prueba su dominio de tablas de hash o arrays de tamaño fijo para los recuentos de frecuencia.
■ 3. Recibe una solución **O(las vidas eternas + tención eterna)** sobre una ingenua búsqueda **O(las vidas eternas2)**.

■ Palabras clave rociaremos a lo largo de este artículo: *Minimum Window Substring*, *LeetCode 76*, *sliding window*, *O(n)* algoritmo, *Java Python C+*, *entrevista de ingenieros de software*, *extremidades de entrevista de trabajo*.

-...

### 3.2 Declaración de problemas (convocar 150 palabras)

■ ** Entrada**:
> `s` - una cadena de hasta 105 caracteres.
“No” – una cadena más pequeña (también hasta 105).
■ **Output**:
■ La primera lexicografía (ya que sólo una respuesta única está garantizada) subestring más corta de `s` que contiene cada carácter de `t`.
■ Si no existe tal ventana, devuelve una cadena vacía.

■ Casos de borde:
* `s`s` or `t` empty → `'
* `Sobrevivir a la vida'

-...

### 3.3 Good – Bad – Análisis Ugly (Ω300 palabras)

Silencio Silencio
Silencio------------Prince------
Silencio ** Complejidad del tiempo** Silencio La solución **O(n+m)** utiliza dos punteros y tablas de frecuencias de tamaño constante. Silencio Tratando de construir un autómata sufijo o un árbol de sufijo generalizado - sobrematar y difícil de explicar. Silencio
Silencio **Space Usage** tención Constant 128‐size array – ideal para entrevistas. Silencio `HashMap` con muchas entradas si Unicode – todavía lineal pero no constante. ← Mesa de programación dinámica del tamaño `sobrevivirs × sobrevivir’ – espacio cuadrático, imposible para 105. Silencio
La lógica de dos puntos es limpia y fácil de leer. Mantener dos mapas de frecuencia separados para “necesidad” y “ventana” hace el código verbose. TEN Utilizar la recursión o el estilo funcional (map/reduce) hace que la intención sea difícil de seguir para un gerente de contratación. Silencio
Silencio **Portabilidad** Silencio El algoritmo es idéntico en Java, Python, C++ – solo cambios de sintaxis. ← Errores específicos del lenguaje (por ejemplo, la lista mutable de Python vs. rebanada). Silencio Usando características de lenguaje que no son bien conocidos (por ejemplo, flujos Java para mutación). Silencio

■ **Bottom line** – En una entrevista desea presentar el *good* (ventana deslizante, O(n), código claro) y evitar el *ugly* (estructuras de datos poco claras y sobre ingeniería). El *bad* – una solución ligeramente menos eficiente – todavía puede pasar al juez pero puede costar puntos de entrevista.

-...

### 3.4 ¿Por qué esta solución brota en una entrevista de trabajo

1. **Time‐optimal** – `O(las vidas eternas + tención eterna)` golpea a la fuerza bruta `O(las vidas eternas2)` por órdenes de magnitud.
2. **Espacio-eficiente** – Sólo un array de frecuencia de 128-elementos; no mapas de hash, no vectores adicionales.
3. # Dos puntos de claridad # El algoritmo se puede explicar en una frase: *expandir hasta que tengamos todos los caracteres requeridos, luego contraer con avidez de la izquierda*.
4. **Language agnostic** – La misma lógica se traduce en **Java, Python, y C++**, para que puedas mostrar competencia en el idioma que tu entrevista requiere.
5. **Scalable** – Maneja los tamaños máximos de entrada cómodamente; se puede demostrar tiempo de ejecución mediante la ejecución de la solución 'python3.py.

-...

### 3.5 Lista de verificación lista de entrevistas

vocablo pregunta vocablo Qué hacer
Silencio...
Silencio ¿Cómo manejas personajes fuera de ASCII? Silencio Uso `HashMap` o un array de 256 tamaño para ASCII extendido; para Unicode use a `HashMap madeCharacter,Integer confianza` en Java/Python. Silencio
Silencio ¿Por qué decrementamos “necesitamos[c]” después de consumir? Mantiene seguimiento de cuántas veces *todavía* necesitamos ese carácter; valores negativos significan que tenemos más que suficiente de ese char en la ventana. Silencio
Silencio ¿Puede probar que la lógica de contracción de ventanas es correcta? Cuando `missing == 0`, el personaje más izquierdista se elimina sólo si su conteo es > 0; de lo contrario es necesario para una ventana válida. Silencio
Silencio ¿Qué pasa si `t` contiene caracteres repetidos? La matriz 'necesita' comienza con la multiplicidad exacta, por lo que el algoritmo requiere automáticamente cada repetición. Silencio

-...

### 3.6 Conclusión (Aplausos100 palabras)

■ El problema de la subestring de ventana mínima es un ejercicio de ventanilla deslizante por excelencia.
■ Mediante el uso de un array de frecuencia **fixed‐size** y **dos punteros**, logramos tiempo lineal y espacio auxiliar constante, exactamente lo que busca un gestor de contratación.
■ Presentar la solución en **Java, Python, o C++** demuestra su versatilidad a través de las pilas.
■ Recuerde: centrarse en la claridad, explicar el paso en contracción, y resaltar la complejidad de O(n) —estos son las señales de entrevista que usted está listo para un rol de ingeniería de software a tiempo completo.

-...

## 4. SEO‐Optimized Blog Post (Markdown)

``markdown
# Substring de ventana mínima – LeetCode 76
## Sliding‐Window Solution in Java, Python & C++ (O(n) Time, O(1) Space)

■ **Descripción de los datos**: Maestro el problema de la subestring de la ventana mínima (LeetCode 76).
■ Encuentra la subestring más corta que contiene todos los caracteres del patrón usando el enfoque de la ventana deslizante.
■ Obtener código en Java, Python, y C+++ más consejos para entrevista.

-...

## Tabla de contenidos
- [Problema general](#problema vista previa)
- [Sliding‐Window Technique](#sliding-window-technique)
- [Explicación de la Complejidad del Tiempo] (explicado por la complejidad del tiempo)
- [Java Implementation](#java-implementation)
- [Python Implementation] (#python-implementation)
- [C++](#cpp-implementation)
- [Entrevista Consejos " Lista de verificación](#interview-tips-and-checklist)
- [Por qué esta solución se pone de manifiesto] (por qué-esta-solución-resiste)
- [Conclusión](#conclusión)

-...

## Problema general
LeetCode 76, titulado *Minimum Window Substring*, le pide que encuentre la subestring más pequeña contiguo de una determinada cadena `s` que contiene todos los caracteres de otra cadena `t`.
Este problema prueba:
Lógica deslizante de dos puntos.
- **Frecuencia contando** con tablas de hash o arrays fijos.
- Capacidad para optimizar la complejidad **time** de O(n2) a O(n).

-...

## Sliding‐Window Technique
1. **Expand** el puntero derecho hasta que la ventana actual cubra todos los caracteres requeridos.
2. **Contratar** el puntero izquierdo para encoger la ventana mientras que sigue siendo válida.
3. Realice un seguimiento de la mejor ventana (shortest) encontrada.

El truco: utilizar un * array de frecuencia* del tamaño 128 (ASCII) o un `HashMap` para Unicode para contar los caracteres necesarios.
Esto produce un algoritmo **O(sobre las vidas eternas + TENT)**.

-...

## Time Complexity Explained
- Ampliar la ventana toca a cada personaje al máximo una vez → **O(sobrevivir)**.
- Contratante también toca cada personaje a la mayor parte de una vez → **O(sobrevivir)**.
- Total: **O(Las vidas eternas + TENT)**, lo que es óptimo para una longitud de entrada de hasta 105.

-...

## Java Implementation
``java
Solución de la clase pública {}
public String minWindow(String s, String t) {
si (s.isEmpty()
devolver ";
int[] need = new int[128];
for (char c : t.toCharArray())) necesidad[c]+;
int left = 0, right = 0, missing = t.length();
int minLen = Integer.MAX_VALUE, minStart = 0;
mientras (derecho) {}
char c = s.charAt(right++);
si (necesita[c] 0) desaparecidos...
necesita [c]...
mientras que (perdiendo == 0) {
si (derecha - izquierda - minLen) {
minLen = derecha - izquierda;
minStart = izquierda;
}
char lc = s.charAt(left++);
necesidad[lc]+;
si (necesita[lc] 0) desaparecidos++;
}
}
volver minLen == Integer.MAX_VALUE ? "" : s.substring(minStart, minStart + minLen);
}
}
`` `

-...

## Python Implementation
``python
Solución de clase:
def minWindow(self, s: str, t: str) - confía str:
si no s o no t o len(s)
"Regresa"
* 128
por ch en t:
necesidad[ord(ch)] += 1
izquierda, desaparecida, min_len, min_start = 0, len(t), len(s)+1, 0
por derecho, cap en enumerado(s, 1):
si es necesario[ord(ch)] 0:
desaparecidos -= 1
necesidad[ord(ch)] -= 1
mientras falta == 0:
si a la derecha - izquierda
min_len = derecha - izquierda
min_start = left
left_ch = s[left]
necesidad[ord(left_ch)] += 1
si es necesario[ord(left_ch)] 0:
desaparecidos += 1
izquierda += 1
volver "" si min_len √≥ len(s) else s[min_start:min_start+min_len]
`` `

-...

## C++ Aplicación
``cpp
Clase Solución {
public:
hilo minWindow(string s, string t) {}
si (s.empty()
devolver ";
int need[128] = {0};
para (cara c : t) necesidad[(int)c]++;
int left = 0, missing = t.size(), min_len = INT_MAX, min_start = 0;
para (derecho = 0; derecho) {}
char c = s[right];
(necesita [(int)c] 0) desaparecidos...
necesita [int)c]...
mientras que (perdiendo == 0) {
si (derecha - izquierda + 1 se indica min_len) {}
min_len = derecha - izquierda + 1;
min_start = izquierda;
}
char lc = s[left++];
necesidad [(int)lc]++;
(necesita [(int)lc] 0) desaparecidos++;
}
}
volver min_len == INT_MAX ? " : s.substr(min_start, min_len);
}
};
`` `

-...

## Interview Tips
- **Explicar la ventana corredera**: "Expande hasta que tengamos todos los caracteres requeridos, luego contrate de la izquierda."
- **Highlight O(n) time**: Esta es una entrevista clave métrica.
*Mostrar portabilidad* Mención se puede adaptar a Java, Python o C++.
- ** Casos erguidos**: `las vidas eternas ' ), cuerdas vacías, no ASCII caracteres.

-...

## Por qué la subestring de ventana mínima es un clásico
- Prueba técnica de dos puntos.
- Forza la comprensión de las tablas de frecuencias.
- Recibe la optimización: **O(n)** vs. **O(n2)**.

-...

Conclusión
Dominar el problema de la subestring de la ventana mínima demuestra que puede resolver los desafíos de procesamiento de cadenas en el mundo real de manera eficiente y limpia.
Mantenga esta solución de ventana deslizante en su caja de herramientas de entrevista y impresionará a los gerentes de contratación buscando un ingeniero de software experto.

-...

#MinimumWindow Substring #LeetCode76 #SlidingWindow #O(n) #Java #Python #C++ #SoftwareEngineer #EntreviewTips
`` `

■ El formato de Markdown arriba se puede copiar a cualquier plataforma de contenido (WordPress, Jekyll, Hugo) y rendirá bellamente con la sintaxis adecuada destacando para bloques de código.

-...

■ ** Nota final** – Utilizar este artículo como publicación de LinkedIn o artículo medio; los encabezados estructurados, los fragmentos de código y los párrafos de keyword-dense ayudarán a tu rango de contenido para *Minimum Window Substring* consultas mientras muestra tus cortes de codificación.

-...

■ ¡Hecho!