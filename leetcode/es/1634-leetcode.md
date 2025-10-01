-...
Título: LeetCode 1634. Añadir Two Polynomials Representaed as Linked Lists -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. LeetCode 1634 – Add Two Polynomials Represented as Linked Lists

■ **Problema** – Combina dos polinomios enlazados que ya están clasificados en orden **de bajado restringido**, devolviendo un nuevo polinomio en el mismo orden.
■ **Constraints** – `0 ≤ n ≤ 104`, coeficientes en `[-109, 109]`, poderes en `[0, 109]`.
■ ** Objetivo** – Tiempo de `O(n)`, `O(1)` espacio auxiliar (la lista de salida se puede construir en su lugar).

A continuación se encuentran soluciones limpias y idiomáticas en **Java**, **Python**, y **C+** que satisfacen los requisitos.

-...

### Java Solution

``java
*
* Definición para lista ligada al canto que representa un término polinomio.
*/
clase PolyNode {
int coefficient;
poder int;
PolyNode next;
PolyNode(int coeff, int pow) { this.coefficient = coeff; this.power = pow; }
PolyNode(int coeff, int pow, PolyNode next) { this.coefficient = coeff; this.power = pow; this.next = next; }
}

Solución de la clase pública {}

*
* Añade dos polinomios representados por listas vinculadas.
* @param poly1 Head of first polynomial list
* @param poly2 Head of second polynomial list
*Retorno Head of the summed polynomial list
*/
public PolyNode addPoly(PolyNode poly1, PolyNode poly2) {
// Dummy cabeza simplifica el manejo del primer nodo
PolyNode dummy = nuevo PolyNode(0, 0);
PolyNode tail = dummy;

(poly1 != null ' poli2 != null) {
si (poly1.power > poli2.power) {}
tail.next = poly1;
poli1 = poli1.nexto;
} si (poly1.power) {}
tail.next = poly2;
poli2 = poli2.nexto;
} más { // Mismo poder – combinar coeficientes
int newCoeff = poli1.coeficient + poli2.coeficiente;
si (newCoeff!= 0) {/ Sólo mantenga términos no cero
tail.next = nuevo PolyNode (newCoeff, poli1.power);
}
poli1 = poli1.nexto;
poli2 = poli2.nexto;
}
tail = tail.next; // Mover la cola hacia adelante si un nodo fue apegado
}

// Adjuntar la cola restante (ya sea poli1 o poli2)
tail.next = (poly1 != null) ? poli1 : poli2;
Devolver el tonto.
}
}
`` `

*Por qué funciona* *

Silencio ¿Qué pasa?
...--------------------------
Silencio 1. Silencio Crear cabeza muñeca Silencioso O(1)
Silencio 2. Silencio Mientras que ambas listas no son vacías, compare poderes Silencio O(1) por iteración Silencio
Silencio 3. ← Adjuntar el mandato de mayor potencia, o fusionarse si es igual a TEN O(1) TENIDO
Silencio 4. Silencio Saltar cero resultados de coeficientes
Silencio 5. ← Apéndice la lista restante
Silencio 6. Silencio Regresar `dummy.next` Silencio O(1) Silencio

Total: **O(n)** tiempo, **O(1)** espacio auxiliar.

-...

### Python Solution

``python
de la importación Facultativo

Clase PolyNode:
def __init__(self, coefficient: int, power: int, next: Optional['PolyNode']=None):
autocoeficiente = coeficiente
poder = poder
self.next = next

def addPoly(poly1: Opcional[PolyNode], poli2: Opcional[PolyNode]) - titulado Opcional[PolyNode]:
dummy = PolyNode(0, 0)
cola = muñeco

poli1 y poli2:
si poli1.power > poli2.power:
tail.next = poly1
poli1 = poli1.
elif poly1.power - No.
tail.next = poly2
poli2 = poli2.
# Igual poder #
new_coeff = poli1.coeficient + poli2.coeficiente
si new_coeff: # skip cero term
tail.next = PolyNode(new_coeff, poly1.power)
poli1 = poli1.
poli2 = poli2.
cola = cola. siguiente si sigue. siguiente otra cola

# Attach the remaining list
tail.next = poli1 o poli2
Regresa el tonto.
`` `

*Puntos clave*

* Usa un nodo muñeco para evitar las comprobaciones de las persianas para el primer elemento.
* Mantiene escaneo lineal y memoria extra constante.
* Manejo pitónico de None y traversal de lista.

-...

### C++ Solución

``cpp
*
* Definición para nodo de lista ligada al canto que representa un término polinomio.
*/
struct PolyNode {
int coefficient;
poder int;
PolyNode *next;
PolyNode(int coeff, int pow) : coefficient(coeff), power(pow), next(nullptr) {}
PolyNode(int coeff, int pow, PolyNode *n) : coeff, power(pow), next(n) {}
};

Clase Solución {
public:
PolyNode* addPoly(PolyNode* poly1, PolyNode* poly2) {
// Dummy cabeza para simplificar el apego a los nodos
PolyNode dummy(0, 0);
PolyNode* tail = ' dommy;

(poly1 ' poli2) {}
si (poly1-propencia de títulos de propiedad poli2- título) {
tail- ratio = poli1;
poli1 = poli1-(s)next;
} si (poly1- título) {
tail-ientenext = poli2;
poli2 = poli2-tionext;
} más { // mismo poder
int newCoeff = poli1- ratio + poli2- ratio;
si (newCoeff!= 0) { // mantener sólo términos no cero
tail-iguiente = nuevo PolyNode(newCoeff, poli1-propencia);
}
poli1 = poli1-(s)next;
poli2 = poli2-tionext;
}
tail = tail-consiguiente ? tail- iconot : cola; // mover sólo si apegamos un nodo
}

// Apéndice el resto de la lista no vacía
sa-consext = poli1 ? poli1 : poli2;
Devolver el tonto.
}
};
`` `

-...

## 2. Artículo del Blog – “Agregar dos polinomios representados como listas vinculadas: el bien, el mal y el ugly”

■ **SEO Focus**: *Preguntas de entrevista de Java, Entrevista de LinkedList, soluciones Leetcode, entrevista de Python, entrevista de C++, ingeniero de software, entrevista de trabajo*

-...

#### Introduction

Al buscar “Preguntas de entrevista de Java”, “Problemas de entrevista de Python”, o “Retos de codificación C+++”, *Agregar Dos Polinomios Representados como Listas Vinculadas* es un contendiente frecuente. Combina la manipulación clásica de lista conectada con un toque de álgebra, lo que lo convierte en un favorito para evaluar la fluidez de estructura de datos y el pensamiento algoritmo.

En este post, diseccionaremos el problema, exploraremos las fortalezas y los obstáculos de las soluciones comunes y caminaremos a través de una implementación limpia y lista para la producción. Al final, usted sabrá exactamente qué entrevistadores están buscando y cómo presentar una respuesta pulida que aumenta sus posibilidades de aterrizar ese trabajo de ensueño.

-...

### El problema (LeetCode 1634)

Se le dan dos listas enlazadas, cada nodo que representa un término polinomio:

`` `
[coeficiente, poder]
`` `

Ambas listas ya están clasificadas en orden de potencia estrictamente descendente y no contienen términos de cero coeficiente.

**Task** – Combinar los dos polinomios en una lista ordenada, resumiendo coeficientes con la misma potencia y omitiendo cualquier términos que resulten en un coeficiente cero.

*Ejemplo*:
" poly1 = [2,2],[4,1],[3,0] " (2x2 + 4x + 3)
`poly2 = [[3,2],[-4,1],[-1,0] ' (3x2 – 4x – 1)

** Producto**: [[5,2],[2,0]] (5x2 + 2)

-...

### The Good – Why It's a Great Interview Question

Por qué importa
Silencio...
TEN **Alineado-list basics** Silencio Pruebas habilidad para atravesar y modificar listas vinculadas, una habilidad básica para cualquier desarrollador de backend. Silencio
Silencio **Sorting invariants** Silencio Assumes lists are pre-sorted, so candidates can focus on merging rather than sorting. Silencio
Silencio ** Casos de emergencia** Silencio Cero coeficientes, iguales poderes o listas vacías fuerzan un manejo cuidadoso de las condiciones de límites. Silencio
Silencio **Tiempo / Espacio** Silencio Solución óptima es tiempo lineal y espacio auxiliar constante: una entrevista clásica “punto del suelo”. Silencio
Silencio **Idioma agnóstico** Silencio Puedes resolverlo en Java, Python, C++ o en cualquier idioma que apoye listas vinculadas. Silencio

-...

### Los malos – saltos comunes

Pitfall Silencio Consequence Silencio
Silencio------------------------------
Silencio **Ignorando los coeficientes cero** Silencio Deja los términos `0xn` en el resultado, violando las limitaciones de problemas. ← Revise explícitamente `si (sum!= 0)` antes de subir. Silencio
Silencio **La lógica de comparación incorrecta** Silencioso Cierre los ganglios incorrectamente o causando bucles infinitos. Use `si/else if/else` o un único `si (p1- títulopower √≥ p2- título de propiedad) ... si... Silencio
Silencio **No usar un cabezal sordo** Silencio Requiere muchos casos especiales para el primer nodo. Silencio Crear un nodo muñeco y devolver `dummy.next`. Silencio
Silencio **Asignación de memoriaExtra** Silencio Fails the `O(1)` space requirement. TEN Reutilizar los nodos existentes; sólo asignar cuando se necesita un nuevo nodo para un término fusionado. Silencio
Silencio **Skipping `poly1.next` or `poly2.next`** Silencio Misaligned list after merge. Silencio

-...

### The Ugly – Over-Complicated Approaches

A veces los candidatos implementan **recursive merges** o **hash‐map aggregation**. Si bien es correcto, rompen la regla espacial `O(1)` (la pila de recursión cuenta como memoria). Además, crear nuevos nodos para cada término (incluso si el término existe en una de las listas de entrada) pierde tiempo y puede llevar a ** fugas de memoria** en idiomas como C++.

■ **Tip**: Un simple iterante, en lugar de fusión es la respuesta “limpia, magra” que impresiona a los entrevistadores.

-...

### A Clean, Idiomatic Implementation (Java as the Reference)

A continuación se encuentra la solución Java que caminaremos paso a paso. Utiliza un nodo tonto, se fusiona en un solo pase, y nunca asigna nodos innecesarios.

``java
public PolyNode addPoly(PolyNode poly1, PolyNode poly2) {
PolyNode dummy = nuevo PolyNode(0, 0);
PolyNode tail = dummy;

(poly1 != null ' poli2 != null) {
si (poly1.power > poli2.power) {}
tail.next = poly1; // Potencia más grande – mantener el nodo original
poli1 = poli1.nexto;
} si (poly1.power) {}
tail.next = poly2;
poli2 = poli2.nexto;
. ♫ ... {
int newCoeff = poli1.coeficient + poli2.coeficiente;
si (newCoeff!= 0) {/ Sólo se adjunta si el resultado no es cero
tail.next = nuevo PolyNode (newCoeff, poli1.power);
}
poli1 = poli1.nexto;
poli2 = poli2.nexto;
}
tail = tail.next; // advance if a node was attached
}

tail.next = (poly1 != null) ? poli1 : poli2; //
Devolver el tonto.
}
`` `

*Por qué es una entrevista lista: *

1. **La lógica clara** – la cadena «si/else» refleja el razonamiento matemático: «poder más grande → mantener ese término; igual poder → coeficientes de suma».
2. ** Manejo a plazo fijo** – el `si (nuevoCoeff != 0) ' guard ensures compliance with the “no cero terms” rule.
3. **O(1) espacio auxiliar** – sólo asignamos cuando se requiere un nuevo nodo fusionado; todas las demás operaciones reutilizan los nodos existentes.
4. **Escaneo de línea** – cada nodo se procesa una vez; no hay bucles anidados o clasificación de sobrecabeza.

-...

### Python & C++ Variantes

- **Python**: Use un bucle de poli1 y poli2; el nodo muñeco es un solo objeto de `PolyNode(0,0).
- **C++**: Preferir un `PolyNode dummy(0,0)` en la pila y devolver `dummy.next`.
- **Java**: La misma lógica se aplica, sólo con fuerte escritura y referencias explícitas del puntero.

-...

### Entrevista Presentación Consejos

1. **Declara tus suposiciones** – “Las dos listas están ordenadas descendiendo por el poder y no contienen coeficientes cero. ”
2. **Explicar el tiempo/espacio de intercambio** – “Nos fusionaremos en tiempo lineal, reutilizando los nodos para que permanezcamos dentro de “O(1)”. espacio extra. ”
3. **Mostrar la manipulación de la periferia** – “Si los coeficientes cancelan, simplemente saltamos el nodo; si una lista se agota, anexamos el resto. ”
4. **Write clean code** – Mantenga la lógica en un solo método; evite las funciones de ayudante anidado a menos que sea necesario.
5. **Continúe a través de un caso de prueba** – Simule `poly1 = [2,3],[1,1]]] y `poly2 = [[-2,3],[4,0]]; muestre cómo las decisiones puntero conducen a la lista final.

-...

## Pensamientos finales – Lo que los entrevistadores quieren

Los entrevistadores buscan:

Silencio Lo que refleja la vida
Silencio.
Silencio **Tiempo de iluminación** Silencio Uso eficiente de las estructuras de datos. Silencio
Silencio **Espacio constante** Silencio Manipulación en lugar y uso de memoria mental. Silencio
Silencio **Robust edge‐case handling** Silencio Atención al detalle y programación defensiva. Silencio
Silencio **Clear, comentar código** Silencio Ability to communicate complex logic to a teammate or manager. Silencio

Dominar *Añadir dos polinomios Representados como Listas Vinculadas* le da un punto de conversación versátil. Muestra tu comprensión de las listas vinculadas, clasificando invariantes y optimización algorítmica, mientras que te deja flexionar un poco de matemáticas.

Así que la próxima vez que veas esto en LeetCode, en el desafío de codificación de una empresa, o en el PDF de un reclutador, entra con confianza, mantén tu código limpio, y recuerda: las mejores respuestas son aquellas que **merge, sum, y skip**, todo en un pase de orden.

-...

#### Takeaway

- **Implement** la cabeza del muñeco, en lugar de fusionarse en su idioma preferido.
- **Explicar** la linealidad del algoritmo y el espacio constante.
- **Highlight** manipulación de la periferia (igual que poderes, cero sumas, listas vacías).

Al dominar este problema, usted no sólo asará la parte de codificación de su entrevista, sino también demostrar el estilo de codificación claro y eficiente que las compañías de tecnología valoran. ¡Feliz codificación, y que tus entrevistas de trabajo terminen con una nota alta! 🚀

-...

*No dude en comentar con su propia implementación específica del idioma o compartir donde ha encontrado este problema en una entrevista real. *