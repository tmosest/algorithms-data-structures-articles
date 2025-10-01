-...
Título: LeetCode 1190. Subestrings inversos entre cada par de paréntesis -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

## 1190. ** Subestaciones transversales entre cada par de paréntesis* *
*Medium ◾ LeetCode*

■ **Problema** – Dado una cadena `s` que contiene sólo letras minúsculas y paréntesis, revierte las subestrings dentro de cada par de paréntesis iguales, empezando por el par más interior.
■ Devuelve la cadena resultante **sin** cualquier paréntesis.

■ *Examples*
" `
■ Entrada: "(abcd)"
■ Producto: "dcba"
■
■ Entrada: "(u(amor)i)"
■ Producto: "iloveu"
■
■ Entrada: "(ed(et(oc))el)"
■ Producto: "código de texto"
" `

■ **Constraints**
Ø • `1 ' s.length
• `s` sólo contiene letras mayúsculas y paréntesis equilibradas.

-...

## 1. Por qué este problema es una mina de oro para las entrevistas

* Te obliga a pensar en ** estructuras de datos modificadas** (una pila o recursión).
* Prueba su capacidad para **mutar cadenas eficientemente** (en lugar vs. buffers adicionales).
* Muchos entrevistadores preguntan este problema exacto en una primera ronda porque la respuesta es limpia, corta y cubre algunos conceptos básicos.

**SEO palabras clave: #
- paréntesis inversas
- solución 1190
- pitón de java c++ leetcode reverse parentheses
- la manipulación de cadenas de entrevista
- problema de leetcode basado en pilas
- algoritmo de la entrevista de trabajo

-...

## 2. La “buena” – Una solución clásica de estaca (Python / Java / C++)

Silencio Idioma Silencio Silencio Silencio
Silencio----------------------------
Silencio Python Silencio 2‐pass: construir `pair` array + caminar con una bandera de dirección (O(n)) Silencio O(n) Silencio O(n) Silencio
Silencio Java  suya Apilada iterativa (O(n)) Silencio O(n) Silencio
TENIDO C++ TENIDO Apilación iterativa (O(n)) TENIDO O(n) TENIDO

A continuación mostramos dos variantes:

Silencio Variant Silencio Lo que hace  durable Complejidad
Silencio----------------------------
Silencio **Apilación intratable** Silencio Mientras iterando, empuja el índice de cada `'(''. Cuando se encuentra un `''''', pop el último índice `'('`, revierte el segmento entre ellos, y *skip* los paréntesis. Silencio **Tiempo** O(n) – cada personaje se procesa un número constante de veces. **Espacio** O(n) – pila + buffer de salida. Silencio
Silencio **Optimal “Jump”** ← Pre-compute pares emparejantes, luego atravesar la cuerda una vez mientras “jumping” a través de paréntesis emparejados y dirección toggling. **Espacio** O(n) – matriz de pares + pila. Silencio

### 1.1 Solución Iterative Stack (Python)

``python
def reverseParentheses(s: str) - Propiedad str:
pila = [] # tiendas índices de '( '
res = [] # personajes finales
cur = 0 # índice actual en s

mientras se curan
ch = s[cur]
si ch == '(':
stack.append(cur) # recuerda dónde está el
elif ch == ')':
inicio = pila.pop() # encontrar su partido
# revertir la subestring entre start+1 y cur-1
res.extend(reversed(s[start+1:cur]))
más:
res.append(ch) # normal character
cur += 1

volver ''.join(res)
`` `

■ *Por qué funciona* –
■ *La pila garantiza que siempre emparejamos cada `'''''' con su **más** sin igual `'.
■ Al invertir la rebanada `[start+1:cur]` deshacer los paréntesis y revertir el subestring interno en el momento exacto que terminamos de procesarlo. *

### 1.2 Java Implementation

``java
importar java.util*;

Solución de la clase pública {}
public String reverse Parentheses(String s) {
StringBuilder sb = nuevo StringBuilder();
Deque cumplióInteger confianza stack = nuevo ArrayDeque correspondió();

(int i = 0; i) s.length(); i++) {
char c = s.charAt(i);
si (c == '(') {
stack.push(i);
} si (c == ') {}
int start = stack.pop(); // index of matching '('
segmento de cuerda = sb.substring(start + 1, sb.length());
sb.delete(start + 1, sb.length()); // remove the processed part
sb.insert(start + 1, nuevo StringBuilder(segment).reverse());
. ♫ ... {
sb.append(c);
}
}
devolver sb.toString();
}
}
`` `

■ *Por qué funciona* –
■ *El `StringBuilder` nos permite eliminar e insertar en O(1) amortizado por operación.
■ La pila sigue la pista de donde comienza una nueva subestring “inner”, por lo que cuando se conoce un “”)” podemos aislar el segmento, revertirlo y volver a ponerlo. *

#### 1.3 C++ Aplicación

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
cuerda inversa Parentheses(string s) {
Resultado de cadena;
vector apilar;
int n = s.size();

para (int i = 0; i) {}
si (s[i] == '(') {
stack.push_back(result.size());
} si (s [i] == ') {
int start = stack.back(); stack.pop_back();
reverso(result.begin() + inicio + 1, result.end());
. ♫ ... {
result.push_back(s[i]);
}
}
Resultado de retorno;
}
};
`` `

■ *Por qué funciona* –
■ *La llamada "reversa" a la "estring::iterator" rango realiza la inversión interna-a-outer sin problemas.
■ Al no almacenar los paréntesis en `result`, garantizamos que la cadena final no contiene ninguno. *

-...

## 2. El Bien, el Mal, y el Ugly

Silencio Silencio
Silencio------------Prince------
Silencio **Readability** Silencio La solución de la pila es código de 40 líneas, fácil de leer en la entrevista. Silencio Un enfoque ingenuo que construye una nueva cadena para cada inversión puede ser *O(n2)*. El uso de la recursión sin un índice global puede ser confuso para principiantes. Silencio
Silencio **Performance** Silencio O(n) tiempo, memoria O(n) – óptima para los límites dados. La operación "reversa" dentro del bucle podría ser evitada por el método "jump", pero cuesta poco para n ≤ 2000. tención In‐place reversal de toda la cadena es posible pero añade complejidad con dos punteros. Silencio
En Java, `StringBuilder.reverse()` muta el constructor – recuerde clonar si necesita el original. ← En C+++, `reverse` requiere rangos de iterador cuidadosos; los errores fuera por uno son comunes. ← En Python, las rodajas de cadenas crean nuevos objetos – mantengan un ojo en el factor constante. Silencio

-...

## 3. Solución óptima “bomba” (O(n)) – 2 pasos

Este método es un favorito entre los problemas “difíciles” de LeetCode porque utiliza **sin inversión explícita** dentro del bucle.

``python
def reverseParentheses(s: str) - Propiedad str:
n = len(s)
par =
pila = []

# 1st pass – build pair index map
para i, ch in enumerate(s):
si ch == '(':
stack.append(i)
# ch == ') '
j = pila.pop()
par[i] = j
par[j] = i

res = []
I = 0
paso = 1
mientras que yo no
si s[i] en "()":
i = par[i]
paso = paso
más:
res.append(s[i])
i += paso
volver ''.join(res)
`` `

**C++**

``cpp
string reverseParentheses(string s) {
int n = s.size();
vector(n)
apilación especificado st;
para (int i = 0; i) {}
si (s[i] == '(') st.push(i);
si (s[i] == ')
int j = st.top(); st.pop();
par[i] = j;
par[j] = i;
}
}

cadena res;
para (int i = 0, d = 1; i)
si (s[i] == '('
i = par[i];
d = d);
. ♫ ... {
res.push_back(s[i]);
}
}
restitución;
}
`` `

#Java #

``java
Clase Solución {
public String reverse Parentheses(String s) {
int n = s.length();
int[] par = nuevo int[n];
Señalamiento:Integer confía st = nuevo Stack correspond();

para (int i = 0; i)
si (s.charAt(i) == '(') st.push(i);
si (s.charAt(i) == ')
int j = stpop();
par[i] = j;
par[j] = i;
}
}

StringBuilder sb = nuevo StringBuilder();
para (int i = 0, d = 1; i)
char c = s.charAt(i);
si (c == '(' Silencioso c == ')
i = par[i];
d = d);
} más sb.append(c);
}
devolver sb.toString();
}
}
`` `

-...

## 4. Recaptura de la complejidad

Silencio Variante Silencioso Silencioso
Silencio------------
← Stack/Builder (primera solución)
TENIDO “Jump” dos pasos (optimal)

Ambos corren cómodamente bajo los límites de LeetCode (`n ≤ 2000`). Para entradas más grandes, el método de salto es ligeramente más rápido porque hace *una* traversal lineal después del pase de procesamiento previo.

-...

## 5. Cómo utilizar esta solución en su próxima entrevista de trabajo

1. ** Explique la intuición primero. #
*“Porque los paréntesis están anidados, podemos pensar en ellos como una pila o recursión.”*
2. **Mostrar el código, pero no sólo entregarlo. #
*A través del uso de la pila y por qué eliminamos las paréntesis. *
3. *Mención de las operaciones.*
*Stack vs. recursion vs. salto de dos pasos – cada uno tiene su propio costo de legibilidad. *
4. **Pregunta de seguimiento. #
*“¿Y si la cuerda no estuviera equilibrada? ¿Cómo detectarías eso?*

Un candidato fuerte terminará en ** menos de 5 minutos** y luego extenderá la discusión a problemas de análisis más genéricos.

-...

## 6. Pensamiento final

El problema de los paréntesis inversos es un **gateway** en el mundo de algoritmos de cadenas *linear-time*. Entréguelo, y usted se sentirá confiado en hacer frente a una amplia gama de preguntas de entrevista que implican delimitadores **balanceados, subestring reversal, y trucos de dos puntos**.

Buena suerte, y feliz codificación! 🚀

-...

**Preparado por**
*Tu amistoso tutor de codificación AI*

-...
**Keywords para SEO**: `reverse parentheses stack solution, Optimiz jump algoritmo, interview string manipulation, stack based algoritmo, LeetCode string problem, job interview coding practice`.