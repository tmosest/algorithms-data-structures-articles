-...
Título: LeetCode 1111. Profundidad máxima de dos crianzas de padres válidas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recap del problema – 1111. Profundidad máxima de dos padres válidos

Silencio ¿Qué tan rígido?
Silencio...
Silencio ** Entrada** Silencioso `seq` - una cadena de paréntesis válida (VPS). Longitud ≤ 10 000. Silencio
Silencio ** Objetivo** Silencio Split `seq` en dos subsecuencias disjoint `A` y `B` que también son VPS. The **maximum** of ` deep(A)` and `depth(B)` must be **minimal**. Silencio
Silencio **Output** Silencio Un array entero `respuesta` de longitud `respuesta `respuesta[i] = 0` si `seq[i]` pertenece a `A`, de lo contrario `respuesta[i] = 1`. Silencio

■ ¿Por qué importa este problema? * *
■ Te enseña a usar un contador *single* (o apilar) para distribuir paréntesis entre dos cuerdas de una manera que equilibra sus profundidades. Este es un clásico LeetCode “medium” que aparece con frecuencia en entrevistas porque prueba tanto la comprensión de la profundidad y el pensamiento codicioso basado en pilas.

-...

## 2. El Greedy Insight (la parte “buena”)

Si caminamos a través de la cuerda de izquierda a derecha, podemos mantener un solo contador `a profundidad' que representa el nivel actual de anidación de la cadena original.

- Cuando vemos `', tenemos que abrir un corchete en `A` o `B`.
Lo asignamos a **uno de los dos grupos** y luego **incremento** `en profundidad ' .
El truco es alternar la asignación de grupo entre consecutivos `'(''' al mismo nivel de anidación.
Esto se logra tomando el " porcentaje 2 " .

- Cuando vemos '''''', el emparejado ''('` ya ha sido asignado a un grupo.
Para mantener los paréntesis equilibrados debemos poner este `'''' en el grupo **same** como su soporte de apertura.
Por lo tanto decrementamos ` profunda` *primero* (ya que la profundidad del par emparejado está terminada) y luego utilizamos ` profundo % 2` para decidir el grupo.

■ ¿Por qué funciona esto? #
■ La paridad de la profundidad actual nos dice si el par actual de paréntesis está en un nivel uniforme o extraño de anidación. Al girar la paridad cada vez que abrimos un soporte, difundimos el anidaje uniformemente a través de los dos grupos, asegurando que la profundidad **máximo de cada grupo es `ceil(originalDepth/2)`** – el mínimo teórico.

-...

## 3. El “Bad” – Edge Cases & Pitfalls

Silencio Pitfall Silencio
Silencio...
Silencio **Usando la profundidad después de aumentar para `'('** ANTE Increment *después de decidir el grupo, de lo contrario estaría usando el nivel de profundidad *next*. Silencio
Silencio **Usando la profundidad antes de decrementar por `')'** Silencioso Decremento *antes de decidir el grupo, porque la paréntesis de cierre pertenece al mismo par que terminó a esta profundidad. Silencio
Silencio **Asumiendo que una pila es necesaria** Silencio No es – un simple contador entero basta. Usar una pila añade espacio y tiempo innecesarios. Silencio
*Confusa “subsequencia” con “subestring”* El array de asignación no reordena caracteres; simplemente banderas pertenecientes. No se realiza re-arrangement. Silencio

-...

## 4. La lectura “Ugly” – Performance &

- ** Complejidad del tiempo**: `O(n)` - uno pasa sobre la cuerda.
- ** Complejidad del espacio**: `O(n)` para el array de respuesta (requerido por el problema).
- **Readability**: La solución contra-basada es corta y clara, pero el truco de '% 2' puede ser confuso a primera vista. La adición de comentarios o una pequeña función de ayuda ( " grupo = profundidad " ) ayuda.

-...

## 5. Implementaciones de referencia

A continuación encontrará una solución **clara, lista para la producción** en **Java**, **Python**, y **C+**. Los tres utilizan la misma lógica contra-basada.

-...

### 5.1 Java

``java
*
* 1111. Profundidad máxima de dos crianzas válidas
* Solución Greedy O(n) que utiliza un contador de profundidad único.
*/
Solución de la clase pública {}
int[] maxDepthAfterSplit(String seq) {
int n = seq.length();
int[] response = new int[n];
profundidad de entrada = 0; // profundidad de nido actual

para (int i = 0; i)
char c = seq.charAt(i);
si (c == '(') {
// Asignación basada en la profundidad actual, luego aumento
respuesta[i] = profundidad % 2;
profundidad++;
} más { // c == ') '
// Decremento primero, luego asignar
profundidad...
respuesta[i] = profundidad % 2;
}
}
respuesta de retorno;
}
}
`` `

-...

### 5.2 Python

``python
Solución de clase:
def maxDepthAfterSplit(self, seq: str) - Conf List[int]:
profundidad = 0
respuesta = []

para ch en seq:
si ch == '(':
respuesta.append(en profundidad % 2)
profundidad += 1
# ch == ') '
profundidad -= 1
respuesta.append(en profundidad % 2)

respuesta
`` `

-...

### 5.3 C++

``cpp
Clase Solución {
public:
vector asignado injerto maxDepthAfterSplit(string seq) {
vector respuesta;
respuesta.reserve(seq.size());
profundidad de entrada = 0; // profundidad de nido actual

para (cara c : seq) {
si (c == '(') {
respuesta.push_back( profundidad) 1); // igual que la profundidad % 2
++a profundidad;
} más { // c == ') '
- En profundidad;
respuesta.push_back(a fondo)
}
}
respuesta de retorno;
}
};
`` `

■ **¿Por qué `en profundidad ' en lugar de `% 2`? #
■ Poco a poco Y es una pequeña victoria de rendimiento (y también demuestra el truco de paridad). Es totalmente equivalente a los enteros no negativos.

-...

## 6. Artículo del Blog – “El Bien, el Mal, y el Ugly de LeetCode 1111”

■ **Título**: *Mastering LeetCode 1111: A Deep Dive into the “Maximum Nesting Depth” Puzzle*
■ **Meta Descripción**: Aprenda la solución O(n) óptima para LeetCode 1111 en Java, Python y C++. Comprender la estrategia avaricia, las trampas y las ideas de entrevista.

-...

### 6.1 Introduction

Si usted está cazando un papel de ingeniería de software, probablemente se ha enfrentado a una pregunta de entrevista que se ve simple a primera vista pero esconde un truco inteligente. LeetCode 1111 – *Maximum Nesting Depth of Two Valid Parentheses Strings* – es una gema de este tipo. Prueba no sólo sus cortes de codificación sino también su capacidad de pensar en *balance* y *distribución* en un solo paso.

En este artículo derribaremos:

1. La idea **core** (el bien).
2. Common **missteps** (el malo).
3. Trucos de rendimiento y consejos de legibilidad (el feo).
4. Implementaciones completas de lenguaje cruzado.

¿Listo? Vamos a bucear.

-...

### 6.2 Problema de reestablecimiento

Se le da una cadena 'seq' que es una cadena de paréntesis válida (VPS). Usted debe dividirlo en dos subsecuencias disyuntivas `A` y `B` tales que ambos son VPS. Su objetivo: **minimizar** `max(a), profundidad(B)'. Devuélvete una matriz que dice a qué grupo cada personaje va (`0` para `A`, `1` para `B`).

-...

### 6.3 The Greedy Insight – The Good

Piense en la cuerda como una serie de *niveles profundos*:

`` `
0 1 2 3 2 1 0
(()()()) → aumentos de profundidad y disminuciones
`` `

Si siempre dividimos entre corchetes en ** profundidades alternantes**, el par más profundo será compartido lo más uniformemente posible. Formalmente:

- Para una apertura `'('' en profundidad `d`, póngalo en el grupo `d % 2`.
- Para el cierre concordante '')', después de disminuir la profundidad, ponerlo en grupo `d % 2` también.

¿La belleza? Un contador entero ( ' profundidad " ) basta; ningún mapa de pila o hash necesario. La profundidad máxima de ambos grupos se convierte en `ceil(originalDepth / 2)`, que es el mínimo teórico.

-...

### 6.4 Los Pitfalls – El Mal

← Mistake ← Consequence
Silencio----------------------------
¦ Incremento `de profundidad ' *antes* asignando `'('’ Silencio Usa la paridad incorrecta para la apertura actual Silencio Assign primero, luego `de profundidad++` peru
Silencio Decrement ` profunda` *after* assigning `''''' Silencio Cierre de paréntesis consigue el grupo equivocado Silencio Decrement primero, luego asigne Silencio
Silencio Asumiendo que se requiere una pila ← Memoria extra, código más lento ← Utilizar un contador
← Misreading “subsequence” como “substring” Respuesta incorrecta si usted reordena ¦ Mantener el orden original; sólo la membresía de la bandera

-...

### 6.5 Performance " Readability – The Ugly

Un pase lineal.
- **Espacio**: O(n) – array de respuesta (debe ser devuelto).
**Readability**: 2 " o " . La adición de un ayudante ( " grupo único = profundidad " 1 " ) o comentarios aclara la intención.

-...

### 6.6 Muestras de código completo

■ Las tres implementaciones siguen el mismo algoritmo.
■ Elige el idioma que coincida con la pila de entrevistas de trabajo.

##### Java

``java
Solución de la clase pública {}
int[] maxDepthAfterSplit(String seq) {
int n = seq.length();
int[] response = new int[n];
profundidad de entrada = 0;

para (int i = 0; i)
char c = seq.charAt(i);
si (c == '(') {
respuesta[i] = profundidad % 2;
profundidad++;
. ♫ ... {
profundidad...
respuesta[i] = profundidad % 2;
}
}
respuesta de retorno;
}
}
`` `

#### Python

``python
Solución de clase:
def maxDepthAfterSplit(self, seq: str) - Conf List[int]:
profundidad = 0
ans = []

para ch en seq:
si ch == '(':
ans.append(en profundidad % 2)
profundidad += 1
más: '
profundidad -= 1
ans.append(en profundidad % 2)
Retorno
`` `

###### C++

``cpp
Clase Solución {
public:
vector asignado injerto maxDepthAfterSplit(string seq) {
vector significar uns
ans.reserve(seq.size());
profundidad de entrada = 0;

para (cara c : seq) {
si (c == '(') {
as.push_back(a fondo)
++a profundidad;
} más { // ') '
- En profundidad;
as.push_back(a fondo)
}
}
devolver los ans;
}
};
`` `

-...

### 6.7 Take‐ Away for the Interviewer

- ¿Por qué esta entrevista está lista? La solución demuestra tiempo O(n), espacio auxiliar O(1) y un enfoque codicioso limpio.
- **Por qué importa la contratación**: Usted será capaz de explicar *por qué* paridad de obras de profundidad, anticipar las trampas, y escribir código conciso.
- ¿Qué hacer después? Pruebe el problema “Split Array con Máximo Sum”; también utiliza particionamiento codicioso.

-...

### 6.8 Pensamientos Finales

LeetCode 1111 puede parecer intimidante debido a su requisito de “dos cuerdas”, pero la lógica subyacente es un ejemplo de libro de texto de * paridad alterna* para equilibrar las estructuras anidadas. Al dominar este problema, ganarás confianza en:

- Traducir limitaciones de problemas en contadores simples.
- Reconociendo cuando una pila es exagerada.
- Escribir código limpio, idiomático en Java, Python y C++.

Buena suerte, y que tus paréntesis siempre permanezcan equilibrados!