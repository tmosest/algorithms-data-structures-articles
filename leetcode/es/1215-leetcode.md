-...
Título: LeetCode 1215. Números de paso -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
1. La solución – 3-Lenguage Code Snippets

A continuación encontrará implementaciones limpias, listas para la producción para **Java, Python y C+** que resuelven LeetCode 1215 – * Números de registro*.
Los tres utilizan la misma idea de búsqueda (BFS), bien adaptada, y se ejecutan en el tiempo anunciado y los límites del espacio.

■ **Confianza para las entrevistas** –
■ *BFS* es generalmente lo primero que la gente intenta para problemas de dígitos “construidos”.
■ Asegúrese de que puede explicar por qué la cola está atada ( " cursillo alto/10 " ), por qué tratamos `0 ' por separado, y por qué se necesita un 'sort() final (la orden BFS no está aumentando estrictamente).

----------------------------------------------------

## Java – `Solution.java `

``java
importar java.util*;

Solución de la clase pública {}
*
* Devuelve todos los números de paso en [bajo, alto], inclusivo.
*
* @param bajo límite inferior (0 ≤ bajo ≤ alto)
* @param high upper bound (low ≤ high ≤ 2·10^9)
* @return set list of stepping numbers
*/
public List made integer confianza countSteppingNumbers(int low, int high) {
Lista de resultadosInteger título = nuevo ArrayList implicado();

// Caso Edge: 0 es un número de paso si se encuentra en el rango
(bajo == 0) result.add(0);

Queue Garantizado = nueva cola LinkedList correctamente();
// iniciar BFS de cada número de un dígito (1 ... 9)
para (int d = 1; d)
queue.offer(d);
}

(!queue.isEmpty()) {}
int curr = queue.poll();

si (currir >= bajo " curr " = alto) {
result.add(curr);
}

// Si el siguiente número se desborda o excede el alto, deja de expandirse
si (currir √≥ alto / 10) continuar;

el último Digit = curr % 10;

// Apéndice último Digit+ 1
si (último dígito) {
int next = curr * 10 + (lastDigit + 1);
si (next <= high) queue.offer(next);
}

// Apend lastDigit- 1
si 0) {
int next = curr * 10 + (lastDigit - 1);
si (next <= high) queue.offer(next);
}
}

Collections.sort(result); // BFS order is not guaranteed to be classified
Resultado de retorno;
}

/* *
/* Arnés de prueba rápida – corre con “java Solution” en tu IDE. */
/* *
public static void main(String[] args) {
Solución sol = nueva solución ();
System.out.println(sol.countSteppingNumbers(0, 21)); // [0,1,2,3,4,5,6,7,8,9,10,12,21]
System.out.println(sol.countSteppingNumbers(10, 15)); // [10,12]
}
}
`` `

----------------------------------------------------

## Python – `solution.py `

``python
de las colecciones importa
de la importación Lista

Solución de clase:
def countSteppingNumbers(self, low: int, high: int) - Conf List[int]:
"
Devuelve todos los números de paso en [bajo, alto], inclusivo.
"
res = []

# 0 es un número de paso sólo si pertenece al rango
si baja == 0:
res.append(0)

q = deque(range(1, 10) # comienza con 1..9

mientras q:
cur = q.popleft()

si baja <= cur <= alta:
res.append(cur)

# No hay necesidad de crecer más si el próximo número se desborda
si cur > alta // 10:
continuar

último = cur % 10

# Append last+1
si la última se hizo 9:
nxt = cur * 10 + último + 1
si nxt 0 = alto:
q.append(nxt)

# Append last-1
si es el último 0:
nxt = cur * 10 + último - 1
si nxt 0 = alto:
q.append(nxt)

de vuelta ordenados (res)


# --------------------------------------------------
Prueba manual rápida
# --------------------------------------------------
si __name_ == "__main__":
sol = Solución()
print(sol.countSteppingNumbers(0, 21)) # [0,1,2,3,4,5,6,7,8,9,10,12,21]
print(sol.countSteppingNumbers(10, 15)) # [10,12]
`` `

----------------------------------------------------

## C++ – `solution.cpp `

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector significado conteoSteppingNúmeros(incluidos bajos, int altos) {
vector res;

// 0 es un número de paso solamente si se encuentra dentro del rango
(bajo == 0) res.push_back(0);

queue indicaint
para (int d = 1; d) = 9; ++d) q.push(d); // start BFS from 1..9

(!q.empty()) {
int cur = q.front(); q.pop();

si (cuerdo = bajo " curva " = alto)
res.push_back(cur);

// Si el siguiente número supera el alto, deja de expandirse
si (cuerdo √° alto / 10) continuar;

int last = cur % 10;

// Apéndice último+ 1
si (último)
largo largo nxt = 1LL * cur * 10 + (último + 1);
si (nxt <= high) q.push(static_cast fielint(nxt));
}

// Apéndice final-1
si 0) {
nxt largo largo = 1LL * cur * 10 + (último - 1);
si (nxt <= high) q.push(static_cast fielint(nxt));
}
}

(res.begin(), res.end());
restitución;
}
};

/* --------------------------------------------------
* Arnés de prueba rápida – compilar con
* g++ -std=c+17 solution.cpp -o solution " sensible ./solution
*
int main() {}
Sol de solución;
auto v1 = sol.countSteppingNumbers(0, 21);
para (int x : v1) cout se hizo x se hizo "
cout se realizó endl;

auto v2 = sol.countSteppingNumbers(10, 15);
para (int x : v2) cout se hizo x se hizo "
cout se realizó endl;
}
`` `

----------------------------------------------------

# 2. Blog Artículo – “El Bien, el Mal, y el Ugly de LeetCode 1215 (Números de Paso)”

■ **Keywords** – LeetCode 1215, números de paso, BFS, preparación de entrevistas, diseño de algoritmos, Java, Python, C++, entrevista de trabajo

-...

## Introduction

Cuando los reclutadores comienzan a preguntar “¿Puede resolver el problema de los números de paso?”, usted está en el medio de una entrevista** o preparándose para uno.
LeetCode 1215 es engañosamente simple: *encontra todos los enteros en un rango donde los dígitos adyacentes difieren por 1*. Sin embargo, sus limitaciones (hasta 2 × 109) y el requisito de devolver los números en orden surtido** dan lugar a trampas sutiles.

En este post caminaremos por el **bueno** (lo que lo hace elegante), el **bad** (los errores comunes), y el **ugly** (la gimnasia de caso entero). Terminaremos con una lista de verificación práctica de búsqueda de trabajo: cómo discutir el problema en una entrevista, y cómo mostrar su código.

-...

## The Problem, Restated

■ **Número de registro** – Un entero *x* donde cada par de dígitos adyacentes tiene una diferencia absoluta de exactamente 1.
■ **Task** – Dados números enteros *low* y *high* (0 ≤ bajo ≤ alto ≤ 2 × 109), devuelve una lista ordenada de todos los números de paso en el rango inclusivo [*low*, *high*].

El desafío no es encontrar los números sino en **generarlos eficientemente** sin iterar sobre cada entero en el rango.

-...

## The Good: Why BFS is the Natural Choice

1. *Tree‐like Growth*
Cada número de paso puede ser expandido por un dígito que está ±1 lejos de su último dígito. Esto forma un **trie** (árbol prefijo) de números válidos.

2. **Bounded Depth**
El número de paso más largo inferior al 2 × 109 tiene a la mayoría de 10 dígitos. Por lo tanto, el árbol BFS tiene una profundidad ≤ 10, garantizando que la cola nunca explote.

3. **No Re-Computaciones**
BFS visita cada número **exactamente una vez**. En cambio, un DFS ingenuo puede generar el mismo número a través de diferentes caminos si no es cuidadoso.

4. #Prueba natural #
Antes de encubrir a un niño, podemos comprobar si el nuevo número superaría *alto*. Si es así, dejamos de explorar esa rama inmediatamente.

5. *Simlicidad*
El algoritmo del núcleo se reduce a un puñado de líneas (más la caldera de cola habitual). Los entrevistadores aman el código que es *correcto, conciso y claramente anotado*.

-...

## The Bad: Common Mistakes That Kill Your Solution

TENIDO ANTERIOR ANTERIOR ANTERIOR Por qué sucede
Silencio...
Silencio **Over Looking the 0 case** Silencio 0 es un número de paso, pero BFS que comienza a partir de 1-9 nunca lo genera. Agregue un cheque especial: si `low == 0`, empuje 0 en la lista de resultados. Silencio
Silencio **Utilizando el desbordamiento de la int en C+** Digit` puede exceder 2 × 109 (todavía se ajusta en 32 bits firmados), pero la multiplicación podría desbordarse si `cur` es grande. Use `long' para los cálculos intermedios, devolver a `int` sólo después de la comprobación `traducido= alto'. Silencio
Silencio **No podar con `alto / 10`** Silencio La cola puede crecer indefinidamente si mantiene dígitos pendientes incluso cuando el siguiente número se desbordará *alto*. Silencio Add `if (cur ю / 10) continue;` antes de generar niños. Silencio
Silencio **Asumiendo que la orden BFS está ordenada** Silencio BFS visita los nodos de nivel por nivel, pero nodos a la misma profundidad no están garantizados para estar en orden ascendente. Silencio Ordenar el resultado final o utilizar un `PriorityQueue` para mantener el orden durante la traversal (cosa). Silencio
Silencio **Ignorando 32-bit vs 64-bit bounds** Silencio En Java, `int` es 32-bit, por lo que 2 × 109 es seguro. En Python, no hay problema; en C++ utilizar 'long' para la seguridad. Mantenga siempre el tipo de datos consistente con los límites. Silencio

-...

## The Ugly: Edge‐Case Tactics " Final Sorting

1. **Manejo de dígitos de edge* *
* Cuando el último dígito es `9`, no puedes anexar `10`.
* Cuando es `0`, no puedes anexar `-1`.
Estas son manejadas por las condiciones 'últimoDigit' realizadas 9` y 'último Digit.

2. ** Prevención Duplicada**
El árbol BFS puede producir el mismo número de diferentes padres si no tienes cuidado.
Con el límite de profundidad ( "cur " alto / 10 " ) y las restricciones de dígitos, los duplicados no ocurren en este problema. Pero en variantes más complejas necesitarás un `HashSet` para dedupe.

3. *Clasificación final*
A pesar de que cada número generado es único, orden BFS es **no** que aumenta estrictamente. La solución más simple es `Collections.sort(resultar)` (Java), `sorted(res)` (Python), or `sort(res.begin(), res.end())` (C++).
Alternativamente, utilice un `PriorityQueue` durante la traversal – pero el factor de registro adicional generalmente supera los beneficios.

-...

## Complexity Analysis

TENCIÓN TENIDO Tiempo ANTERIENTE Espacio ANTERIOR
Silencio------------------------
Silencio BFS (nuestra solución) Silencio **O( N )** donde N es el recuento de los números de paso ≤ alto (≤ 2 × 109) Silencio **O( N )** para la cola + lista de resultados Silencio N está obligado por unos pocos miles; por lo tanto prácticamente lineal Silencio
← DFS (recursivo) Silencio Igual que BFS TENIDO Mismo, además de la profundidad de la pila de recidiva (≤ 10) TENIDO Ligeramente más código, más difícil prune Early TEN
Silencio Brute‐Force  **O( high – low )** Silencio **O(1)** Silencio Impractical for 2 × 109 Silencio

Porque `alto' puede ser tan grande como 2 × 109, *(alto – bajo)* es completamente infeasible. BFS garantiza un tiempo de ejecución que depende sólo del tamaño **output**.

-...

## How to Talk About En una entrevista

1. **Declarar claramente el problema** – Reestablecer la definición de un número de paso y el formato de salida requerido.
2. **Elija BFS** – Mencione la propiedad del árbol: desde un número válido sólo puede anexar `último+1` o `último-1`.
3. **Explicar el Libra de la Cuidad** – Mostrar que si `cur √° alta / 10`, cualquier expansión adicional se desborda, para que pueda parar.
4. ** Casos de Edge** – No olvides los límites de 0 y dígitos (`0` y `9`).
5. **Sorting** – Clarify que ordenará al final; BFS no produce números ordenados por defecto.
6. **Simplicidad del código** – Mantener la solución corta, bien adaptada, y discutir cualquier preocupación tipo de datos (Java `int` vs C++ `long long').
7. **Pregunte por la retroalimentación** – Si el entrevistador sugiere una alternativa (por ejemplo, usando una cola prioritaria), discuta los intercambios.

-...

## Checklist for Job‐Seekers

Silencio Silencio Silencio Silencio Silencio Silencio Silencio
Silencio--------Prince--------
TEN Write **multi‐language solutions** Silencio Show proficiency in Java, Python, C++ Silencio El programa de trabajo agradece la experiencia en lenguaje cruzado
Silencio Add **unit tests** Silencio Usar los rangos de ejemplo proporcionados Silencio Demuestra confiabilidad y confianza Silencio
← Benchmark contra un probador **randomizado** TEN Generar pares bajos/alto aleatorios, comparar su salida con una fuerza bruta para pequeñas gamas TEN inculca confianza TEN
Silencio Documento **tiempo/complejidad espacial** En una pizarra blanca o README Silencio Refleja la madurez algorítmica
← Preparar ** Puntos de charla** – Buena/Bad/Ugly ANTE Summarize in bullet form Silencio Hace la conversación nítida

-...

Conclusión

LeetCode 1215 (Stepping Numbers) es un **micro-gem** de entrevistas algorítmicas.
*Bien*: BFS aprovecha la propiedad de expansión natural y la profundidad atada.
*Bad*: Errores como ignorar `0`, faltando cheques de desbordamiento, o asumiendo orden ordenados puede descarrilar incluso una idea perfecta.
*Evidentemente*: La gimnasia de Edge-case y la clasificación final pueden parecer mundanas, pero son esenciales para la corrección.

Su arsenal de búsqueda de trabajo está listo: puede **código** en Java, Python, o C+++, y puede **explicar** el razonamiento, las trampas y las optimizaciones.

Buena suerte - la próxima entrevista puede estar justo a la vuelta de la esquina, y usted va a dar un paso al éxito! 🚀

-...

■ *No dude en compartir este artículo en LinkedIn o Twitter con el hashtag #LeetCode1215 para ayudar a otros a prepararse para su próxima entrevista. *

-...

¡Feliz codificación! *



-...

**
-...


■ *Este artículo fue escrito originalmente para la temporada de entrevistas 2024. Todo el código es de código abierto bajo la licencia MIT (ver el enlace de repositorio arriba). *



-...

¡Feliz trabajo de caza!