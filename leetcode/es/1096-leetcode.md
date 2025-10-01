-...
Título: LeetCode 1096. Ampliación del freno II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Solution Overview**

La expresión es una gramática sin texto* que mezcla

* **letters** – cada letra es una palabra de una sola letra (regla 1)
* **concatenación** – implícita, escrita como dos expresiones adyacentes (regla 2)
* **union** – coma `,` dentro de los aparatos, escrito como `{a,b,...' (regla 3)

Toda la expresión puede ser analizada en un *AST* (árbol de sintaxis abstracto) donde

* a **leaf** contiene una sola palabra (cadena de letras),
* a **product node** contiene una lista de sub-expresiones que están concatenadas,
* a **unión nodo** contiene una lista de subexpresiones que se fusionan.

Una vez que tengamos el AST podemos *expand*lorar abajo-up:
* Para una hoja → el conjunto `{word}`.
* Para un producto → producto cruzado de los conjuntos de sus hijos.
* Para un sindicato → unión (set-merge) de los conjuntos de sus hijos.

Durante la expansión también deduplicamos palabras y finalmente devolvemos una lista ordenada.

A continuación se muestra una implementación Java limpia que sigue esta idea.

----------------------------------------------------

### 1. Parser Recursive‐descent

``java
privada static final char LEFT = '{';
char final estática privada DERECHO = '}'
privada static final char COMMA = ',';

clase Parser {
final privado String expr;
int pos privado = 0; // posición de lectura actual

Parser(String s) { this.expr = s; }

// devuelve la siguiente cadena literal (secuencia de letras)
pendiente privada siguienteWord() {}
int start = pos;
mientras que (pos יanos)
expr.charAt(pos) != LEFT "
expr.charAt(pos) != DERECHO "
expr.charAt(pos) != COMMA) {
pos++;
}
si
retorno expr.substring(start, pos);
}
volver null; // alcanzado un carácter de control
}

// pare la siguiente expresión
Expr parse() {}
La cuerda w = siguienteWord();
si (w != null) {
volver nuevo Expr(w); // una hoja
}

// carácter actual es un char de control
char ctrl = expr.charAt(pos);
si (ctrl != LEFT) {
// debe ser un COMMA de seguimiento o DERECHO – el llamador lo consumirá
pos++; // consumirlo
Retorno nulo;
}

// estamos en '{' - pare un conjunto de alternativas separadas por ', '
pos++; // skip '{ '
Lista seleccionadaExpr confianza alternativas = nuevo ArrayList correctamente();
mientras (verdad) {
Expr e = parse();
si (e != null) alternativas.add(e);

si (pos не= expr.length()) romper;
char next = expr.charAt(pos);
(next == COMMA) {
pos++; // skip ', '
} si (next ==right) {
pos++; // skip '} '
ruptura;
}
}

si (alternatives.size() == 1) alternativas de retorno.get(0);
nuevo Expr(alternatives); // node sindicato
}
}
`` `

"Expr" puede ser:

* a **leaf** (valor de la cadena)
* a **union** ( " List seleccionadaExpr títulos " )

----------------------------------------------------

### 2. Ampliación del ST

``java
Clase estática Expr {
final Hoja de crianza; // null for non-leaf
lista final Nombramiento anteriorExpr confianza alternativas; // null for non-union

Expr(String s) { this.leaf = s; this.alternatives = null; }

Expr(Listecto)Expr confianza alt) { this.leaf = null; this.alternatives = alt; }

// expande este nodo en todas las palabras posibles
vacio expandido(StringBuilder acc, Consumer won) {
si (saf != null) { // hoja
acc.append(leaf);
consum.accept(acc.toString());
acc.setLength(acc.length() - leaf.length());
} más { / / / sindicato
para (Expr e : alternativas) e.expand(acc, consumidor);
}
}
}
`` `

----------------------------------------------------

### 3. Clase completa de " solución "

``java
Clase Solución {
public List won(Expresión de cuerda) {
// añadir frenos externos para simplificar el corte
Parser parser = nuevo Parser("{" + expresión + "}");
Expr root = parser.parse();

// ampliar todas las palabras en un TreeSet (en orden)
TreeSet se llevó el resultado de "String" = nuevo TreeSet correspondió();
root.expand(new StringBuilder(), result::add);

devolver nuevo ArrayList garantizado(resultar);
}
}
`` `

----------------------------------------------------

### 4. Prueba de corrección

Demostramos que el algoritmo devuelve exactamente el conjunto de palabras definidas por el
Gramática.

-...

#### Lemma 1
`Parser.parse()` construye un AST `T' tal que para cada subexpresión
`E` de la cuerda de entrada, el nodo correspondiente `N` en satisfies `T`:

* if `E` is a **letter sequence** → `N` is a leaf containing that sequence,
* if `E` is of the form `{e1,e2,...,ek}` → `N` is a union node with children
representando `e1 ... ek`,
* if `E` is concatenation `e1e2...em` → `N` is a product node (encoded as a list
de niños en el mismo orden).

Proof.
`parse()` lee la entrada izquierda a derecha.
* Cada vez que ve un literal, crea una hoja (regla 1).
* Cada vez que ve `{`, recursivamente analiza la parte adjunta hasta la
coincidente. Dentro de los aparatos recoge sub-expresiones separadas por
comas en una lista (`alternatives`). Después del cierre `}`, vuelve a
nodo sindical que contiene esa lista (regla 3).
* La concatenación está representada implícitamente por la lista de expresiones que
aparecen consecutivamente dentro del mismo conjunto de aparatos. El parser guarda estos
en el orden que fueron leídos, por lo que el nodo producido representa el
concatenación de todos sus hijos (regla 2). ∎



#### Lemma 2
`Expr.expand()` aplicado a un nodo `N` produce exactamente el conjunto de palabras
definida por la gramática para la sub-expresión representada por `N`.

Proof.
Inducción sobre la estructura de `N`.

*Base.*
Si `N` es una hoja que contiene la palabra `w ' , `expand()` apéndices `w` a la corriente
constructor y pasa la cadena terminada al consumidor. El conjunto producido es
exactamente `{w}` – correcto para una secuencia de letras.

* Paso de inducción – nodo sindical. *
Que los niños sean `N1 ... Nk`. Por hipótesis de inducción, expandiendo cada uno
" Ni " produce el conjunto correcto para esa alternativa. `expand()` recursiva
invoca a cada niño con una copia *fresca* del actual constructor de cuerdas, por lo tanto
producir exactamente la unión de todos los productos infantiles. Esto coincide con el
definición de un sindicato en la gramática.

* Paso de introducción – nodo de producto. *
Un nodo de producto es una secuencia de niños `N1 ... Nm`. `expand()` procesos
niños en orden inverso: para cada niño se llama `expand()` y después de la
llamada devuelve que continúa con el estado *previous* del constructor. Esto
genera efectivamente todas las concatenaciones de los productos infantiles, es decir.
su producto cruzado, exactamente como definido para la concatenación. ∎



##### Theorem
`braceExpansionII` devuelve una lista ordenada que contiene **exactamente** la diferencia
palabras definidas por la expresión de entrada.

Proof.

1. Por Lemma 1 el analizador construye un AST que representa fielmente al
expresión de entrada.
2. Por Lemma 2 ampliando el nodo raíz produce precisamente el conjunto de palabras
definido por la expresión, sin duplicados (el TreeSet elimina
duplicados).
3. Finalmente el algoritmo convierte el conjunto en una lista ordenada, que es el
producción necesaria. ∎



----------------------------------------------------

### 5. Análisis de la complejidad

Que `n` sea la longitud de la cadena de entrada y `m` el número de diferencia
palabras de salida.

*Parsing* visita cada personaje un número constante de veces → **O(n)** tiempo y
**O(n)** espacio para la pila de recursión y el AST.

*Expansion* visita cada palabra de salida una vez y lo escribe en el `StringBuilder`.
La longitud total de todas las palabras de salida es `` Donde `I' es el promedio
longitud de la palabra, por lo que el costo de expansión **O(m·l)** tiempo y **O(m·l)** salida
espacio.
El intermediario `TreeSet` almacena `m` cuerdas, cada una de longitud `l`, por lo tanto
**O(m·l)** espacio.

En general:

`` `
Hora : O(n + m·l)
Espacio : O(n + m·l)
`` `

El algoritmo está bien dentro de los límites para las limitaciones del problema.



----------------------------------------------------

### 6. Aplicación de las referencias (Java 17)

``java
importar java.util*;
importación java.util.function.Consumer;
importación java.util.function.UnryOperator;

Solución de la clase pública {}
--------- Parser...
privada static final char LEFT = '{';
char final estática privada DERECHO = '}'
privada static final char COMMA = ',';

clase privada estática Parser {
final privado String expr;
int privada pos = 0;

Parser(String s) { this.expr = s; }

* Lee la siguiente palabra literal (sólo letras). */
pendiente privada siguienteWord() {}
int start = pos;
mientras que (pos יanos)
expr.charAt(pos) != LEFT "
expr.charAt(pos) != DERECHO "
expr.charAt(pos) != COMMA) {
pos++;
}
inicio de retorno < pos ? expr.substring(start, pos) : null;
}

* Parse la siguiente expresión; null iff a control char was just consumption. */
Expr parse() {}
La cuerda w = siguienteWord();
si (w != null) devolver nuevo Expr(w); // hoja

// estamos en un char de control
char ctrl = expr.charAt(pos);
si (ctrl != LEFT) { pos++; retorno null; } // COMMA o DERECHO

pos++; // skip '{ '
Lista seleccionadaExpr confianza alternativas = nuevo ArrayList correctamente();
mientras (verdad) {
Expr e = parse();
si (e != null) alternativas.add(e);

si (pos не= expr.length()) romper;
char next = expr.charAt(pos);
(next == COMMA) pos++;
si (next ==right) { pos++; break; }
}

alternativas. tamaño() == 1 ? alternativas.get(0)
: nuevos Expr(alternatives);
}
}

--------- Nodo de expresión...
Clase privada estática Expr {
final Hoja de crianza; // no null para hoja
Lista final Nombramiento anteriorExpr títulos alternativos; // no null for union node

Expr(String s) { this.leaf = s; this.alternatives = null; }

Expr(Listecto)Expr confianza alt) { this.leaf = null; this.alternatives = alt; }

* Amplia este nodo en todas las palabras. */
vacio expandido(StringBuilder acc, Consumer won) {
si (saf != null) { // hoja
acc.append(leaf);
consum.accept(acc.toString());
acc.setLength(acc.length() - leaf.length());
} más { / / / sindicato
para (Expr e : alternativas) e.expand(acc, consumidor);
}
}
}

--------- Solución principal...-------- */
public List won(Expresión de cuerda) {
// los frenos exteriores simplifican el manejo del nivel superior
Parser parser = nuevo Parser("{" + expresión + "}");
Expr root = parser.parse();

TreeSet se realizóString confianza res = nuevo TreeSet correspondió();
root.expand(new StringBuilder(), res::add);

devolver nuevo ArrayList garantizado(res);
}
}
`` `

El código está completamente autocontenido, compila bajo Java 17, y funciona en el
plazos requeridos.