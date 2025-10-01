-...
Título: LeetCode 224. Calculadora básica -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 224. Calculadora básica – Hard – Java / Python / C+ Soluciones + SEO‐Optimized Blog Post

A continuación encontrará ** tres implementaciones completas** de LeetCode 224 – * Calculadora básica* – una en Java, Python y C+++.
Después del código encontrarás un artículo detallado de blog que cubre lo bueno, lo malo y lo feo de este problema de entrevista clásica.

-...

### 1. Java – Basado en Stack (Iterante)

``java
importa java.util. Stack;

Solución de la clase pública {}
public int calculate(String s) {
Apilación de entrada = nuevo Stack correspond();
int result = 0; // running total
int num = 0; // número actual que se construye
int sign = 1; // +1 or -1

(int i = 0; i) s.length(); i++) {
char c = s.charAt(i);

si (Character.isDigit(c)) {}
// Construir el número actual (manos multi-digit)
num = num * 10 + (c - '0');
} si (c == '+) {
resultado += signo * num;
num = 0;
señal = 1;
} si (c == '-) {}
resultado += signo * num;
num = 0;
sign = -1;
} si (c == '() {
// Empuje el estado actual en la pila
stack.push(result);
stack.push(sign);
// Reiniciar para la subexpresión
Resultado = 0;
señal = 1;
} si (c == ') {}
resultado += signo * num; // terminar el número interno
num = 0;
int prevSign = stack.pop(); // sign before '('
int prevResult = stack.pop(); // result before '('
resultado = resultado prevResult + resultado prevSign *;
} si (c == ' ) {
// saltar espacio blanco
continuar;
}
}

// Añádase el número restante
si (num!= 0) {
resultado += signo * num;
}
Resultado de retorno;
}
}
`` `

■ *Por qué funciona esto*
■ La pila almacena el *contexto* antes de cada paréntesis de apertura: el resultado acumulativo hasta ese punto y el signo que se aplica a toda la subexpresión dentro de los paréntesis. Cuando golpeamos una paréntesis de cierre, aparecen esos dos valores y los combinamos con el resultado de la subexpresión.

-...

### 2. Python – Basado en Stack (Iterative)

``python
Solución de clase:
def calculate(self, s: str) - título int:
pila = []
Resultado = 0
num = 0
sign = 1 # +1 o 1

por ch en s:
si ch.isdigit():
num = num * 10 + int(ch)
elif ch == '+':
resultado += signo * num
num = 0
señal = 1
elif ch == '-':
resultado += signo * num
num = 0
señal = 1
elif ch == '(':
stack.append(resultar)
stack.append(sign)
Resultado = 0
señal = 1
elif ch == ')':
resultado += signo * num
num = 0
prev_sign = stack.pop()
prev_result = stack.pop()
resultado = prev_result + prev_sign * resultado
# ignore espacios

si num:
resultado += signo * num
Resultado de retorno
`` `

-...

### 3. C++ – Basado en Stack (Iterative)

``cpp
#include ■string
#include >
usando std namespace;

Clase Solución {
public:
int calculate(string s) {}
apilación especificado st; // almacena resultado anterior y signo
int result = 0; // running total
int num = 0; // número actual
int sign = 1; // +1 or -1

para (cara c : s) {}
si (isdigit(c)) {}
num = num * 10 + (c - '0');
} si (c == '+) {
resultado += signo * num;
num = 0;
señal = 1;
} si (c == '-) {}
resultado += signo * num;
num = 0;
sign = -1;
} si (c == '() {
st.push(result);
st.push(sign);
Resultado = 0;
señal = 1;
} si (c == ') {}
resultado += signo * num;
num = 0;
int prevSign = st.top(); st.pop();
int prevResult = st.top(); st.pop();
resultado = resultado prevResult + resultado prevSign *;
}
// ignorar espacios
}

si (num!= 0) resultado += signo * num;
Resultado de retorno;
}
};
`` `

-...

Blog Post – “El bueno, el malo y el ugly de LeetCode 224: Calculadora básica”

### 1. Introducción

■ **LeetCode 224 - Calculadora básica (Hard)**
■ El problema le pide que evalúe una simple expresión aritmética que contiene enteros no negativos, `+`, `-`, paréntesis y espacios.
■ **Por qué importa:**
* Es una pregunta clásica de entrevista *stack* que prueba su capacidad de manejar la precedencia del operador y estructuras anidadas.
* Muchas compañías tecnológicas (Google, Amazon, Microsoft, Meta, etc.) utilizan variantes de este problema para medir el conocimiento de la estructura de datos de los candidatos y la velocidad de matemáticas mentales.
• Escribir una solución limpia y eficiente demuestra el dominio de la lógica iterativa, la recursión y el manejo de errores, cualidades muy apreciadas en su currículum.

### 2. Declaración de problemas (Palabras clave de la SEO)

* Calculadora básica* – LeetCode 224
- **Hard** - desafío de entrevista de codificación
- ** Solución basada en datos**
- **Java, Python, C+** - código específico del idioma
- **Evaluación de la expresión anímica** - no `eval() `

■ Entrada: `s = "1 + 1" → Producto: `2`
■ Entrada: `s = "(1+(4+5+2)-3)+(6+8)" → Producto: `23`

### 3. Limitaciones

TEN TERRITORIO ANTERIOR ANTERIOR
Silencio...
TENIDO `1 ANTE = s.length = 3 * 10^5` ANTE Maneja grandes expresiones
TENIDO `s` contiene sólo dígitos, `+`, ``, ``, `(`, `)`, y espacio TENIDO Gramática simple TENIDO
Silencio No unary `+` Silencio Clarifies que `+1` es inválido
TENIENDO UNAry `` permitido ANTERIENTE Manchas expresiones como `-1` o `-(2+3)` Silencio
Silencio No consecutivas operadoras Silencio Garantiza una sintaxis válida
tención 32‐bit integer firmado encaja Silencio No hay reflujo de preocupaciones

### 4. El Bien - Lo que hace este problema Elegante

* Gramática definitiva* Ningún operador ambiguo precedencia más allá de los paréntesis y binario `+`/`-`.
- **Stack Suitability:** Cada par de paréntesis mapas naturales a un empuje/pop, manteniendo el algoritmo O(n).
- *Paso de silencio* Podemos resolver el problema en un escaneo lineal, que es una gran victoria para los entrevistadores.
- ¿Qué? Funciona para entradas enormes (`3*10^5` chars) sin problemas de profundidad de recursión.
- Agnóstico en idioma: La lógica de la pila es idéntica en Java, Python, C++.

### 5. Los malos – las caídas comunes y los errores

Silencio Pitfall Silencio Cómo evitar
Silencio...
Silencio **Olvidó añadir el último número** Silencio Después del bucle, añadir `sign * num` si `num` no es cero. Silencio
Silencio **Mis-ordering stack push/pop** Silencio Push *result* primero, luego *sign*. Al saltar, revierta el orden. Silencio
Silencio **Asumiendo números de un dígito** Silencio Construir números por `num = num*10 + (c - '0')`. Silencio
Silencio **Using recursion for `()** ¦ La profundidad de la Recursión puede golpear el flujo de pila para paréntesis profundamente anidados. Silencio
Silencio **Tratar de espacios incorrectamente** Silencio Skip `' caracteres, no los trate como operadores. Silencio

### 6. Los Casos Ugly – Edge que los candidatos de viaje

1. Unry minus at the start**: `'-1+2'`
- El algoritmo debe tratar el líder `-` como señal para el primer número.
2. **Padres negativos**: `'- (1+2)'`
- El espacio después de `` es inofensivo, pero el algoritmo todavía debe empujar el signo correcto en la pila.
3. **Ministerios anidados: "(1+2)+(3+4)"
- Asegurar que la pila nunca se desborde; cada `(` debe tener una coincidencia ')`.
4. **Números principales**: `123456789+987654321'
- Use `int` (32‐bit) pero tenga cuidado de que las sumas intermedias permanezcan dentro de límites (lo hacen, según las limitaciones).

### 7. Algorithm Walkthrough (Stack‐Based)

1. **Initializar**: `resultar = 0`, `num = 0`, `sign = 1`, vaciado.
2. **Escoge cada personaje**:
- **Digit** → construir `num`.
- **`+` / `-`** → aplicar `sign * num` a `result`, reset `num`, set new `sign`.
- **`(`** → push current `result` and `sign`, reset them (`result = 0`, `sign = 1`).
- **`)** → terminar el número interno, multiplicarse por el signo saltado de la pila, luego añadir al resultado externo.
3. **Después del bucle**: Agregue cualquier número restante a `resultar`.

Este algoritmo funciona en **O(n)** tiempo y utiliza **O(n)** espacio de apilación en el peor caso (padres anidados completamente). El factor constante es muy pequeño, sólo un puñado de variables enteros y operaciones de pila.

### 8. Muestras de Código

* Código fuente completo para Java, Python y C++ se proporciona arriba. *
Los tres comparten la misma lógica; sólo la sintaxis cambia.

### 9. Análisis de la complejidad

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Silencio Java Silencio `O(n)` Silencio `O(n)` Silencio
Silencio Python Silencio `O(n)` Silencio
TENIDO C++ TENIDO `O(n)` Silencio

■ ¿Por qué es aceptable? * *
■ Los entrevistadores buscan algoritmos lineales para problemas difíciles. Recursión habría añadido una llamada extra arriba y riesgo de apilación de flujo.

#### 10. Cómo brillar en su Résumé

- **Agregue una placa de “Entrevista de codificación”** junto al problema de Calculadora Básica en su blog GitHub o personal.
- **Solución de pila de alto nivel “O(n)”** en su proyecto README o LinkedIn posts.
- ** Implementaciones de varios idiomas de la mención** (Java, Python, C++) para mostrar adaptabilidad.
- **Proporcione un snippet de tiempo** para demostrar que su solución funciona bajo 1 ms por `3*10^5` caracteres en hardware típico.

#### 10. Final Takeaway

■ El problema “Cálculo básico” es un ejemplo *beautiful* de cómo un problema complejo de pares se puede destilar en simples operaciones de pila.
■ Al dominar el enfoque basado en pilas y anticipar casos de borde, no sólo clava esta pregunta de LeetCode sino que también demuestra una profundidad de entendimiento que los reclutadores buscan en ingenieros de software senior.

¡Buena suerte en tu próxima entrevista!

-...

** Nota de datos**: El contenido anterior del blog puede ser utilizado literal en blogs personales, Medium, dev.to, o incluso en publicaciones de LinkedIn. Está lleno de encabezados fáciles de SEO, párrafos ricos en palabras clave y fragmentos de código práctico, perfecto para aumentar su visibilidad y atraer a los reclutadores.