-...
Título: LeetCode 591. Validación de la etiqueta -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 591. Validación de la etiqueta – Soluciones completas + Blog SEO-Optimizado

A continuación encontrará tres soluciones completas, listas para la producción para LeetCode **591 – Validador de la etiqueta** escrito en **Java**, **Python** y **C+**.
Después del código encontrarás un artículo de forma larga, amigable con SEO que explica el problema, el algoritmo y las trampas “buenas, malas y feas” que querrás mencionar en una entrevista.

■ **TL;DR - Algoritmo**
* Escanee la cuerda izquierda a derecha.
* Usa una pila para mantener los nombres de las etiquetas abiertas.
> > > > > > > > > > >
[CDATA [ ... ]]]] > > se trata como texto llano.
> > Cada > > > debe coincidir con la parte superior de la pila.
* El código debe estar envuelto en una etiqueta de primer nivel.
* Todos los nombres de etiquetas deben ser 1–9 letras mayúsculas.
• Complejidad: **O(n)** tiempo, **O(n)** espacio de pila.

-...

#### ## 1down⃣ Java 17 Solución

``java
importar java.util*;

Solución de la clase pública {}
booleano público isValid(Código de la cuerda) {
// Un fragmento de código debe comenzar con una etiqueta de apertura
si (código.isEmpty() TENIDO código.charAt(0) != 'traducido') devuelve false;

Deque seleccionaString confianza stack = nuevo ArrayDeque corresponde();
int i = 0;
int n = code.length();

mientras (i
// Si vemos un '
si (código.charAt(i) == 'Hecho') {
// 1. Sección de DATOS
si (i + 9) se hizo n " límite code.startsCon(" seleccionó![CDATA[, i) {
int end = code.indexOf("]] título", i + 9);
si (fin == -1) devolver falso; // no cerrar ]]
i = final + 3; // skip CDATA
continuar;
}

// 2. Etiquetas de cierre
si (i + 1 < n " límite code.charAt(i +1) == '/') {
int j = i + 2;
int close = code.indexOf(' título', j);
si (cerrar == -1) devolver falso; // no cerrar 
String tag = code.substring(j, close);
si (!isValidTagName(tag)) devuelve falso;
si (stack.isEmpty()  durable!stack.peek().equals(tag)) devuelve falso;
stack.pop();
i = cierre + 1;
continuar;
}

// 3. Etiquetas de apertura
int j = i + 1;
int close = code.indexOf(' título', j);
si (cerrar == -1) devolver falso; // no cerrar 
String tag = code.substring(j, close);
si (!isValidTagName(tag)) devuelve falso;
stack.push(tag);
i = cierre + 1;
continuar;
}

// Cualquier otro personaje está permitido en el contenido
i++;
}

// Todo el código debe estar envuelto en una etiqueta de primer nivel
volver stack.isEmpty();
}

// Tag name rules: 1–9 uppercase letters
booleano privado isValidTagName(String s) {
si (s.length() 9) devolver falso;
para (int k = 0; k)
char c = s.charAt(k);
si (c  made 'A' TENIDO TENIDO C ENTE 'Z') devuelve falso;
}
retorno verdadero;
}
}
`` `

*Por qué funciona* *

* **Nunca** utilizar regex para validación – la declaración del problema advierte acerca de los reexes frágiles.
* La pila garantiza la correcta anidación y que cada etiqueta de apertura tiene una etiqueta de cierre coincidente.
* Las secciones de CDATA se saltan atótómicamente – nunca inspeccionamos su contenido interno.
* El cheque final `stack.isEmpty()` asegura que todo el snippet está envuelto en una sola etiqueta.

-...

## ## 2down⃣ Python 3 Solution

``python
Solución de clase:
def isValid(self, code: str) - título Bool:
si no código o código[0] != 'Seguido':
Retorno Falso

pila = []
i, n = 0, len(code)

mientras que yo no
si el código [i] == 'cantado':
Sección CDATA
si i + 9  detectado n y código.startswith(" seleccionado![CDATA[, i):
end = code.find("]] título", i + 9)
si termina == -1:
Retorno Falso
i = final + 3
continuar

# Closing tag
si yo + 1  detectado n y código[i + 1] == '/':
j = i + 2
close = code.find(' título', j)
si cierras == -1:
Retorno Falso
tag = code[j:close]
si no auto._is_valid_tag(tag):
Retorno Falso
si no apilar o apilar[-1] != etiqueta:
Retorno Falso
stack.pop()
i = cierre + 1
continuar

# Open tag
j = i + 1
close = code.find(' título', j)
si cierras == -1:
Retorno Falso
tag = code[j:close]
si no auto._is_valid_tag(tag):
Retorno Falso
stack.append(tag)
i = cierre + 1
continuar

# Ordinary character
i += 1

Regresar no pila

@staticmethod
def _is_valid_tag(name: str) - Propiedad Bool:
devolver 1 <= len(name) <= 9 y name.isupper() y name.isalpha()
`` `

* Notas de pitón*

* `str.find()` se utiliza en lugar de regex – lo mantiene rápido y simple.
* `stack` es una lista; `append`/`pop` give amortized **O(1)** operations.
* El ayudante '_is_valid_tag` mantiene el control de reglas aislado.

-...

### 3down⃣ C+17 Solution

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
bool isValid(código de la cadena) {
si (código.vacío() Silencioso código[0] != 'Seguido') devuelve falso;

vector asignado st;
int i = 0, n = code.size();

mientras (i
si (código[i] == 'cantado') {
/ Sección CDATA
si (i + 9 ecto n " límite code.compare(i, 9, "hecho hecho![CDATA] == 0) {
int end = code.find("]] título", i + 9);
si (end == string::npos) devuelve falso;
i = final + 3;
continuar;
}

// Etiquetas de cierre
si (i + 1 < n " límite code[i + 1] == '/') {
int j = i + 2;
int close = code.find(' inteligente', j);
si (cerrar == hilo::npos) devuelve falso;
string tag = code.substr(j, close - j);
si (!isValidTag(tag)) devuelve falso;
si (st.empty() TENIDO SUPERVISIÓN st.back() != tag) devuelve falso;
st.pop_back();
i = cierre + 1;
continuar;
}

// Etiquetas de apertura
int j = i + 1;
int close = code.find(' inteligente', j);
si (cerrar == hilo::npos) devuelve falso;
string tag = code.substr(j, close - j);
si (!isValidTag(tag)) devuelve falso;
st.push_back(tag);
i = cierre + 1;
continuar;
}

++i; // carácter normal
}

()
}

privado:
bool isValidTag(const string &s) {
si (s.empty() 9) devolver falso;
para (cara c : s)
si (c  made 'A' TENIDO TENIDO C ENTE 'Z') devuelve falso;
retorno verdadero;
}
};
`` `

**C++ trucos* *

* `estring::compare` da un cheque de tiempo constante para el prefijo CDATA.
* `vector asignadostring `` se utiliza como una pila; es lo suficientemente rápido para el límite de 10 000 caracteres.
* Todos los bucles funcionan en **O(n)** – sin recidiva, sin reex.

-...

## 📝 Blog Article – “Tag Validator Leetcode 591” (SEO‐Optimized)

■ **Keywords**: *Tag Validator, LeetCode 591, entrevista de análisis XML, algoritmo de pila, codificación de entrevistas de trabajo, entrevista de ingeniero de software, preguntas de entrevistas de codificación, patrones de entrevista de programación*

### Tag Validator - LeetCode 591 Explained

Imagínate que eres un ingeniero **backend** trabajando en un pequeño motor de marcación tipo XML.
LeetCode **591 – Tag Validator** le pide que decida si una cadena dada es un fragmento de código válido siguiendo *strict* reglas de estilo XML:

← Regla Silencioso Descripción Silencio
Silencio...
Silencio **Debe empezar con una etiqueta de apertura** Silencio Todo el snippet está envuelto en una sola etiqueta de primer nivel. Silencio
Silencio **Etiqueta de nombre** Silencio 1–9 caracteres alfabéticos mayúsculas solamente. Silencio
tención **Nesting** tención Las etiquetas deben ser anidas correctamente; cada `traducido/TAG titulado` debe cerrar la etiqueta más reciente. Silencio
Silencio **No estrado `seguido `` o ``** Silencio Todos los soportes de ángulo pertenecen a etiquetas o CDATA. Silencio
Silencio ** DATOS** Silencioso `¡traducido![CDATA[ ... ]]] `` se trata como texto crudo; su contenido es ignorado. Silencio

Se le ha dado un único " código de la cadena " (≤ 10 000 chars) y debe devolver `verdad ' si sigue todas las reglas, de lo contrario `false ' .

### The “Good” Part – Why a Stack is the Right Tool

* ** Representación natural de estructuras anidadas** – cada etiqueta abierta empuja su nombre en la pila; una etiqueta cercana debe coincidir con la parte superior de la pila.
* **Tiempo de trabajo** – sólo escanea una vez, cada personaje examinó un número constante de veces.
* **Memoria atada por la profundidad del anidamiento** – peor caso `O(n)` pero generalmente mucho menos.
* **Comportamiento predecible** – no sorpresas de los quirks del motor regex o retroceder.

### La parte “Bad” – Pitfalls comunes

1. *Usando regex*
Muchas soluciones ingenuas intentan un regex grande para validar etiquetas, pero la especificación advierte que tales patrones son *fragile* y difícil de mantener.
*Por qué regex falla*: No puede hacer cumplir el anidamiento sensible al contexto (por ejemplo, garantizar que `directo/A título ' coincida con la correcta ` > > ).

2. **Missing CDATA handling* *
Tratar los CDATA como texto ordinario conduce a falsos negativos (por ejemplo, un estrado ` ` ` `` dentro de CDATA).
*Solución*: Pasar el bloque CDATA completo una vez que detecte su marcador de apertura.

3. * Comprobación de envoltura de nivel superior*
Olvidar exigir que todo el snippet está envuelto en una sola etiqueta causa errores sutiles.
*Fix*: Después del escaneo, la pila debe estar vacía – cualquier etiqueta sobrante significa que el snippet no estaba completamente cerrado.

### The “Ugly” Part – Edge Cases That Trip People Up

← Caso Edge Silencioso Por qué Es Ugly ← Cómo Manejar
Silencio----------------------------------------------------------
La gente olvida a menudo que toda la cadena debe ser envuelta; devolver 'verdad' para un contenido vacío dentro de una etiqueta es fácil de perder. Mantenga el control de la pila `stack.empty()` después del bucle. Silencio
Silencio Longitud del nombre de la etiqueta 10 o caso mixto tención Sustituya errores por uno al contar caracteres o verificar caso. Silencio Encapsular la regla en un ayudante (`isValidTagName`). Silencio
Silencio No cerrar `` o `']] Los cálculos del Índice tóxico se vuelven negativos, conduciendo a 'StringIndexOutOfBounds`. TEN siempre verificar el índice se encuentra antes de cortar. Silencio
tención `` en el medio del contenido Si no es seguido por una etiqueta válida o CDATA, es un carácter ilegal. tención Trate a cualquier otro `tratado `` como inválido y devolver `falso`. Silencio
TENIDO cuerda vacía o primer char no `` ANTE Algunas personas olvidan este rápido pre-check y permiten que el algoritmo funcione hasta el final, devolviendo incorrectamente 'verdad'. TEN Vuelva `false` inmediatamente si la cuerda está vacía o no comienza con 'aplicado'. Silencio

## Step‐by‐Step Algorithm Walk-through

1. **Pre-check** – El snippet debe comenzar con ``aplicado'.
2. **Initializar una pila vacía** – Mantener los nombres de las etiquetas abiertas.
3. **Scan left → right* *
* Cuando golpeaste un `traducido':
* **CDATA** (`¡traducido![CDATA[`) – Encuentra el siguiente `]]]] título y salta sobre él.
* **Etiqueta de cierre** ( < > > ) - Extraer el nombre de la etiqueta, validarlo y abrir la pila. Regrese `false` si no coincide con la parte superior.
* **Etiqueta de apertura** ( < = > ) – Extraiga el nombre de la etiqueta, lo valide y empuje hacia la pila.
* Cualquier otro personaje está permitido en el contenido – simplemente siga adelante.
4. **Revista final** – La pila debe estar vacía, lo que significa que cada etiqueta abierta fue cerrada y todo el código está envuelto en una etiqueta de primer nivel.

### Complexity Analysis

TENCIÓN TERRITOR TENIDA Cálculo
Silencio----------
Silencio **Hora** Silencio Cada personaje es inspeccionado un número constante de veces → **O(n)** Silencio
Silencio **Espacio** Silencio Las tiendas de la pila en la mayoría de los nombres de las etiquetas `n/2` → **O(n)** en el peor caso (nidificación profunda). Silencio

### Interview Tips

* **Explica tu pila invariante* La parte superior de la pila siempre representa la etiqueta más reciente que aún no ha sido cerrada.
* **Mostrar que entiende CDATA* No se analiza; es simplemente un bloque de texto crudo.
* **Mención del nombre de la etiqueta regla** – 1–9 caracteres alfabéticos mayúsculas.
* **Evite regex** – La mayoría de los entrevistadores esperan que usted navegue el analizador.
* ** Casos de error de detección temprano** – Si encuentras una etiqueta perdida `` o desajustada, salga inmediatamente.

## Final Thoughts

- **Bueno** – El enfoque de la pila es limpio, O(n) y fácil de razonar.
- **Bad** – Un complejo reex es tentador pero frágil; evitelo.
- **Ugly** – Recuerde las condiciones de límites sutiles: la primera `` debe ser una etiqueta de apertura, la última debe ser su etiqueta de cierre concordante, y las secciones de CDATA deben ser saltadas atómicamente.

Si usted puede explicar este algoritmo, caminar a través de un par de casos de prueba, y mostrar una de las tres soluciones anteriores, usted tendrá una respuesta sólida para **LeetCode 591 – Tag Validator** que impresiona tanto a nivel automatizado como a los entrevistadores.

Buena suerte en su entrevista de codificación y su próximo papel de ingeniería de software! 🚀

-...

### 📌 Quick Copy‐Paste for Hiring Interviews

``java
// Java 17 – Tag Validator
clase pública Solución { ... } // ver código arriba
`` `

``python
# Python 3 - Tag Validator
Clase Solución: ... # ver el código arriba
`` `

``cpp
// C+17 - Validador de la etiqueta
clase Solución { ... } // ver el código arriba
`` `

¡Feliz codificación!