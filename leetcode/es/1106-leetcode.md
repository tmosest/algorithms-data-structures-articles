-...
Título: LeetCode 1106. Parsing A Boolean Expression -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📚 Parsing a Boolean Expression – 1106 – Stack‐Based Mastery (Java / Python / C++)
Un guía práctico para tu próxima entrevista de codificación. *

-...

#### TL;DR
- **Problema**: Evaluar una expresión booleana totalmente paréntesis con `t`, `f`, ``! `, ``, ``, `` sometida ' y comas.
- ** Solución óptima**: algoritmo de pila de espacio lineal de tiempo lineal que *rompea temprano* cuando se conoce el resultado.
- **Idiomas**: Soluciones listas para aprobar **Java**, **Python**, y **C+**.
- **Se centra el blog**: Por qué el enfoque de pila gana, saltos comunes, y cómo discutirlo en una entrevista de trabajo.

■ **Listo para añadir esto a su cartera? #
■ Copia el código, póngalo en contra de LeetCode y suelte el artículo en su GitHub README.

-...

## 1. Recaptura de problemas (LeetCode 1106)

■ ** Entrada** - Una cadena `expresión` (longitud ≤ 20 000) que sigue la gramática:
" `
"('' expr')" "(' expr ')" "(' expr ')" "(' expr' '(' expr (',' expr)* ")" "(' expr (',' expr)* '
" `
■ **Output** – El valor booleano (`true` / `false`) que la expresión evalúa.

*Examples*

Silencioso expresión Silencioso respuesta
Silencio...
Silencioso `"
TENIDO `"Vida(f,t,f)"
Silencioso.

-...

## 2. Por qué una estaca es la elección natural

1. **Depth‐first nature** – Cada operador se aplica a la sub-expresión *next*, reflejando la orden push/pop de la pila.
2. **Ninguna pila de recursión** – La recuperación en una cadena de 20 000 caracteres puede alcanzar los límites de recursión JVM / Python.
3. **Erradicación total** – Para ``pobla` podemos parar tan pronto como veamos ' f ' ; porque `vivir ' tan pronto como veamos `t ' .

■ **Key insight**: *Solo necesitas mantener los operadores “activos” y operar valores en la pila. *

-...

## 3. El Algoritmo de Stack optimizado (O(n) tiempo, espacio O(n))

`` `
para cada char c en expresión
si c == ',' o c == '(' → ignore
si c en { 't', 'f', '!', 'cada', 'vida' } → push(c)
si c == ') → evaluar sub-expresión
`` `

**Evaluar la subexpresión* *

``text
hasTrue = false
hasFalse = false
mientras que la parte superior de la pila es 't' o 'f'
pop - titulado val
tiene Verdadero tención= (val == 't')
hasFalse Silencio= (val ==f)

op = pop() // operador ahora está en la parte superior

si op == '!':
push('t' if not hasTrue else 'f') // !x: true only if x is false
elif op == 'cl':
push('f' if hasFalse else 't') // & : false if any operand is false
más: // op == ' '
push('t' if hasTrue else 'f') // Silencio : verdadero si cualquier operando es verdadero
`` `

El valor final en la pila es la respuesta.

■ ¿Por qué temprano? * *
Para ``, tan pronto como `haFalse` se convierte en 'verdad' podríamos saltar el resto de los valores, pero el simple bucle ya hace eso en algunas operaciones más.
" Para la vida " , se aplica la misma idea. La ganancia es marginal en comparación con la complejidad extra de código, así que la mantenemos sencilla.

-...

## 4. Código

A continuación se muestran los fragmentos completos y compilables para Java, Python y C++. Cada uno sigue la lógica exacta descrita anteriormente.

#### 4.1 Java

``java
importa java.util. ArrayDeque;
importa java.util. Deque;

Solución de la clase pública {}
boolean parseBoolExpr (expresión de cuerda) {
Deque se realizóCaracterística pila = nuevo ArrayDeque correspondió();

para (carc : expression.toCharArray() {)
si (c == '',' TENIDO TENIDO C == '(') continúan;
si (c == 't' Silencioso c == 'f' Silencioso c == '!'
stack.push(c);
} si (c == ') {}
Boolean tiene Verdadero = falso;
boolean hasFalse = false;
mientras (stack.peek() != '!' ' stack.peek() != ' sensible' ' plom.peek() != 'Prince') {
char val = stack.pop();
si (val == 't') tieneTrue = verdadero;
si (val == 'f') hasFalse = verdadero;
}
char op = stack.pop(); // operator
char res;
si (op == '!') {}
res = hasTrue ? 'f' : 't'; // !x
} si (op == 'cl') {}
res = hasFalse ? 'f' : 't'; // &x
} más { // ' '
res = hasTrue ? 't' : 'f'; //  sometidax
}
stack.push(res);
}
}
volver stack.peek() == 't';
}
}
`` `

#### 4.2 Python

``python
de las colecciones importa

Solución de clase:
def parseBoolExpr(self, expression: str) - Bool:
st = deque()
para ch en expresión:
si ch en ',(':
continuar
si entras ('t', 'f', '!', 'du', 'pretensión'):
st.append(ch)
elif ch == ')':
has_true = has_false = False
mientras que st[-1] no en ('!', 'cl', 'persevera'):
val = st.pop()
si vale == 't':
has_true = True
# Val == 'f '
has_false = True
op = st.pop()
si op == '!':
st.append('t' if not has_true else 'f')
elif op == 'cl':
st.append('f' if has_false else 't')
otra cosa:
st.append('t' if has_true else 'f')
volver st[-1] == 't'
`` `

#### 4.3 C++

``cpp
Clase Solución {
public:
bool parseBoolExpr (expresión de la cuerda) {
vectorial asignado fieltro st; // utilizar vector como pila para velocidad
para (cara c : expresión) {
si (c == '',' TENIDO TENIDO C == '(') continúan;
si (c == 't' Silencioso c == 'f' Silencioso c == '!' Неный ненный неннный неный ный ный ный неный неный неный ный ный неный ный ный ный ный ный ный ный ный неный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный 
st.push_back(c);
si (c == ')') {}
bool hasTrue = false, hasFalse = false;
mientras (!st.empty() " sensible st.back() != '!' " sensible st.back() != ' paciencia') {
char val = st.back(); st.pop_back();
si (val == 't') tieneTrue = verdadero;
tiene más Falso = verdadero;
}
char op = st.back(); st.pop_back();
char res;
si (op == '!') res = hasTrue ? 'f' : 't';
si (op == 'cl') res = hasFalse ? 'f' : 't';
más res = hasTrue ? 't' : 'f'; // ' '
st.push_back(res);
}
}
volver st.back() == 't';
}
};
`` `

Las tres soluciones funcionan en tiempo **O(n)** (un paso) y **O(n)** espacio auxiliar (la pila).

-...

## 5. El Bien, El Mal, El Mal

Silencio Silencio
Silencio------------Prince------
Silencio **Correcto** Silencio Funciona para todos los insumos válidos, pase lineal. TEN Ninguno – algoritmo es simple y robusto. ← Olvidar saltar comas o paréntesis → apilar corrupción. Silencio
Silencio **La complejidad** Silencioso `O(n)` tiempo, `O(n)` espacio – óptimo para 20 k longitud. Silencio Ninguno. ← Una implementación de DFS recursiva corre el riesgo de desbordamiento de la pila para el anidamiento profundo. Silencio
Silencio **Readability** Silencio Clear push/pop, one logical block. Silencio Minor: use of boolean flags (`hasTrue`, `hasFalse`) might look unfamiliar. La solución basada en Stack puede ser más difícil de entender para los novatos; la recursión es más intuitiva. Silencio
Silencio ** Casos Edge** Silencio Handles single `t`/`f`, cualquier número de subexpresiones. Silencio Ninguno. Silencio Expresiones como '"!(t)" → necesidad de tratar `!` como no está bien. Silencio
Silencio **Entrevista Talk** Silencio Explicar la metafora temprana, por qué ignoramos las comas. tención Evite sobre-optimizar los bucles de ruptura temprana; puede confundir al entrevistador. Do **not** menciones `ArrayDeque` en Java 8 entrevista; use `Stack` o `ArrayList` para claridad. Silencio
Silencio **Producción Listo** Silencio Limpio, probado y compilable. Silencio Ninguno. ← Agregar registros de depuración o la pila de impresión después de cada operación puede hinchar tiempo de ejecución. Silencio

-...

## 6. Alternativa: Recursive Descent (Less Optimal for Interviews)

Una recursión ingenua:

``python
def parse(expr, i):
si expr[i] en 'tf':
retorno expr[i] == 't', i+1
op = expr[i]
i += 2 # skip '( '
resultados = []
Mientras Verdadero:
val, i = parse(expr, i)
resultados.append(val)
si expr[i] == ')':
i += 1
descanso
i += 1 # skip ', '
si op == '!':
volver no resultados[0], i
elif op == 'cl':
devolver todo(resultados), i
otra cosa:
devolver cualquier(resultados), i
`` `

■ ¿Por qué evitarlo? #
- Complejidad oculta en profundidad de recursión (`O(n)` en el peor de los casos.
- Más difícil de ilustrar a primera hora.
> - Para idiomas como Java/Python, profundidad de recursión > 10 000 puede chocar.

-...

## 7. Puntos de conversación para su entrevista de trabajo

1. **Encuadre de problemas**: reiniciar la gramática, aclarar el caso de una sola `t`/`f`.
2. **¿Por qué linear?** – Big‐O: una traversal, ninguna estructura de datos extra más allá de una pila.
3. **Stack analogy** – mostrar cómo cada `(` empuja contexto, cada `)` pops contexto.
4. **Early-termination** – resaltar " , frente a " perpetua " .
5. ** Prueba de complejidad** – mencionar que cada personaje se procesa una vez.
6. **Testing** – dar ejemplos de pruebas de límites ( " t " , " t) " .
7. **Scalability** – 20 k caracteres → la recursión puede fallar, la pila es segura.

■ **Consejo:** Practicar el "caminar hacia adelante" con una pizarra blanca o un depurador de IDE, para que puedas mostrar visualmente la pila evolucionando.

-...

## 7. Wrap‐Up

- ¿Qué? La solución más rápida, segura y fácil de entrevista para LeetCode 1106.
- **Code**: Proporcionado para **Java**, **Python**, **C+** – copiar, pegar y correr.
- **Artículo**: Este artículo de blog es fácil de SEO para “LeetCode 1106”, “expresión booleana”, “Territmo de tacto”, “O(n)”, “Discusión de perspectiva”.

> # Toma acción # Publique el código a su repositorio, agregue el artículo a su README y compartalo en LinkedIn o Twitter.

Buena suerte, y que su pila permanezca equilibrada!

-...

### Referencias

1. Problema de LeetCode 1106 – *“Expresión booleana”*.
2. G. H. Cormen et al., *Algorithms*, 3rd ed., Chapter 6 (Stacks and Queues).

-...

*Si encontró este artículo útil, protagonice el repo, comparta un comentario a continuación, o llegue a Twitter. ¡Feliz codificación! *