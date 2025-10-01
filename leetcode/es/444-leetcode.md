-...
Título: LeetCode 444. Reconstrucción de secuencias -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
LeetCode 444 - Reconstrucción de la Secuencia
**A Topological‐ Ordenar + Uniqueness Comprueba que funciona en Java, Python & C++**

■ **Palabras clave**: LeetCode 444, Reconstrucción de secuencias, Orden topológico único, BFS/Kahn, DFS, Teoría de Gráficos, Entrevista de codificación, Java, Python, C++.

-...

## 1. Recaptación de problemas

■ *Given*
- `nums ' - a permutation of `[1 ... n] `
:: " secuencias " , una lista de subsecuencias que aparecen en " años "

■ Retorno** **iff** `nums` es * la única* supersequencia más corta que contiene cada subsequencia en `sequences`.

El reto es decidir si el orden en los años es *determinado universalmente* por las restricciones de precedencia pares implicadas en las secuencias. Si lo es, la única supersequencia más corta válida es exactamente 'nums'; de lo contrario hay al menos una orden válida.

-...

## 2. ¿Por qué un Topological Sort?

Cada subsequence `[a, b, c]` nos dice que
`` `
a → b → c
`` `
es un borde dirigido establecido en un gráfico de nodos (los números).
El problema pregunta si ** el gráfico tiene un orden topológico único** que equivale a `nums`.

Si el orden topológico del gráfico es único, debe ser el mismo que los años.
Si no es único, existen al menos dos super-secuencias válidas y "nums" no puede ser el único más corto.

-...

## 3. Resumen del algoritmo

1. **Construir el gráfico " array indegree " *
Para cada par de elementos consecutivos en cada subsequencia, agregue un borde dirigido y actualice los indegreos.

2. **El tipo topológico de Kahn BFS con control de singularidad* *
* Mantener una cola de nodos con indegrejo 0.
* En cada paso, si la cola tiene **más de un** nodo, el pedido es *no* único → devolver `false`.
* Pop the single node, append it to `order`, and decrease indegrees of its neighbours, enqueueing any that drop to 0.

3. *Validato*
* Si la longitud final de `orden' era `n`, el gráfico era incompleto (algunos no aparecen nunca en `sequences`), devolver `false`.
* Compare `order` con `nums`. Si coinciden, `verdad`; de lo contrario `false`.

-...

## 4. Prueba de corrección

Demostramos que el algoritmo devuelve `true` **iff** `nums` es la única supersequencia más corta.

### Lemma 1
Si el algoritmo regresa `falso` porque la cola contiene ≥ 2 nodos, entonces el orden parcial definido por `sequences` admite más de un orden topológico.

*Proof. *
En ese paso, dos nodos distintos `x' y `y` tienen indegree 0, lo que significa que ninguna limitación de precedencia dicta su orden relativo. Por lo tanto ambos `[ ..., x, y, ... ]` y ` [ ..., y, x, ... ]` son extensiones válidas, dando dos super-sequences diferentes. ∎

### Lemma 2
Si el algoritmo termina con un orden único `orden`, entonces `orden` es el orden topológico * solo* del gráfico.

*Proof. *
El algoritmo de Kahn explora todos los bordes. El cheque de singularidad garantiza que en cada paso sólo un nodo es elegible, por lo que el orden relativo de cada dos nodos se fija por decisiones anteriores. Por lo tanto no existe orden alternativo. ∎

### Lemma 3
Si el orden topológico único equivale a `nums`, entonces `nums` es la única supersequencia más corta.

*Proof. *
Cualquier súper secuencia debe respetar los bordes. Una orden topológica es una super-sequencia más corta del gráfico porque contiene cada vértice exactamente una vez. Puesto que sólo hay una orden así y es igual a los `nums`, no puede existir otra supersequencia más corta. ∎

### Lemma 4
Si `nums` es la única super-sequencia más corta, entonces el algoritmo volverá 'verdad'.

*Proof. *
Suponga lo contrario: algoritmo devuelve `false`.
- Cualquier cola tenía ≥ 2 nodos ⇒ por Lemma 1 más de una supersequencia existe ⇒ contradicción.
- O la longitud del orden final ل n ⇒ un poco de vértice nunca aparece en `sequences`; entonces podríamos insertar ese vértice en cualquier lugar sin romper subsequences, dando otra super-sequencia ⇒ contradicción.
Por lo tanto, el algoritmo debe devolver `true`. ∎

Combinar Lemmas 2-4 da el *if y sólo si* declaración. ∎

-...

## 5. Análisis de la complejidad

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
← Construir el gráfico (todos los bordes) Silencio **O(durante las consecuencias [i] sufrimiento** ≤ 105 Silencio **O(n + E)** Silencio
TENIDO EL BFS de Kahn _O(n + E)** TENIDO **O(n + E)**
Silencio total **O(n + E)** Silencio **O(n + E)**

Con " n ≤ 104 " y " vidas duraderas [i] sometida ≤ 105 " , la solución encaja cómodamente dentro de los límites.

-...

## 6. Manejo de Edge‐Case

Silencio Caso confidencialidad ¿Por qué importa?
Silencio...
tención `nums` no permutation ← Problemas garantías, pero la guardia evita fallos TENENCIA Ninguno TENIDO
Silencio Un número nunca aparece en ninguna subsequencia ← Nodo de Gráfico tiene indegree 0 y outdegree 0 → algoritmo devuelve `false`  durable `if (order.size() != n) devuelve false;`
tención Empty `sequences` Silencio Sin bordes → cualquier pedido válido → algoritmo devuelve `false` Silencio Mismo guardia arriba Silencio
Los bordes Duplicados Silencio Utilizamos un `Set` por nodo o cheque antes de añadir Silencio `if (adj[u].add(v)) indeg[v]+;` Silencio

-...

## 7. Aplicación

A continuación se presentan implementaciones limpias y de producción en **Java**, **Python**, y **C+**.
Los tres usan la misma lógica y corren en el mismo tiempo asintotico.

-...

### 7.1 Java

``java
importar java.util*;

Solución de la clase pública {}
secuencia booleana públicaReconstrucción(int[] nums, Lista obtenidaLista realizadaInteger confianza secuencias) {
int n = nums.length;
Lista cumplida No se cumplióInteger título adj = nuevo ArrayList recomendado(n + 1);
int[] indeg = nuevo int[n + 1];
para (int i = 0; i <= n; i++) adj.add (new HashSet fiel());

// Gráfico de construcción
para (Lista realizadaInteger título: secuencias) {}
para (int i = 0; i + 1 seq.size(); i++) {
int u = seq.get(i);
int v = seq.get(i + 1);
si (adj.get(u).add(v)) indeg[v]+;
}
}

// Kahn con control de singularidad
Deque cumplióInteger título q = nuevo ArrayDeque correspondió();
para (int i = 1; i) = n; i++) {
si (indeg[i] == 0) q.offer(i);
}

int idx = 0;
(!q.isEmpty()) {
si (q.size() 1) devolver falso; / / / múltiples opciones - no único
int cur = q.poll();
si (cur != nums[idx]) devolver falso; // orden desajuste
idx++;
para (int nei : adj.get(cur) {
si (--indeg[nei] == 0) q.offer(nei);
}
}
retorno idx == n; // asegurar todos los nodos procesados
}
}
`` `

-...

## 7.2 Python

``python
de las colecciones importan defaultdict, deque
de la importación Lista

Solución de clase:
def sequenceReconstruction(self, nums: List[int], sequences: List[List[int]) - ¿Qué?
n = len(nums)
adj = defaultdict(set)
(n +1)

# Build graph
para seq en secuencias:
for u, v in zip(seq, seq[1:]):
si no en adj[u]:
adj[u].add(v)
indeg[v] += 1

# Kahn con control de singularidad
q = deque([i for i in range(1, n +1) if indeg[i] == 0])
idx = 0

mientras q:
si len(q) 1:
Regreso False # non-unique ordering
cur = q.popleft()
si cur != nums[idx]:
regreso Falso # orden desajuste
idx += 1
para nei en adj[cur]:
indeg[nei] -= 1
si indeg[nei] == 0:
q.append(nei)

retorno idx == n
`` `

-...

## 7.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
secuencia de boolReconstrucción(vector fielint círculo nums, vector asignadovector fieltrente secuencias reducidas) {}
int n = nums.size();
vector realizado noordered_set didint confianza adj(n + 1);
vector implicado(n + 1, 0);

// Gráfico de construcción
para (auto &seq : secuencias) {}
para (size_t i = 0; i + 1 seq.size(); ++i) {
int u = seq[i], v = seq[i + 1];
si (adj[u].insert(v).second) // insertado correctamente
++indeg[v];
}
}

// Kahn con control de singularidad
queue indicaint
para (int i = 1; i) = n; ++i)
si (indeg[i] == 0) q.push(i);

int idx = 0;
(!q.empty()) {
si (q.size() 1) volver falso; / / / múltiples candidatos
int cur = q.front(); q.pop();
si (cur != nums[idx]) devolver falso; // orden desajuste
++idx;
para (int nei : adj[cur]) {}
si (--indeg[nei] == 0) q.push(nei);
}
}
devolver idx == n;
}
};
`` `

-...

## 8. Bien, mal,

Silencio Silencio
Silencio------------Prince------
Silencio **Tiempo** Silencio Linear in `n + E` Silencio Ninguno
Silencioso **Espacio** Silencioso `O(n + E)`
Silencio **Readability** Silencio Clear separation of graph build " Kahn  durable Slight verbosity in Java (sets, arrays) TENNING Ninguno ANTE
Silencio **Edge‐Case Handling** Silencio Explicit guard for `order.size() != n` 
Silencio **Common Pitfall** Silencio Olvídate de comparar con `nums` durante BFS Silencio Con vistas a la verificación de la singularidad ( ' q.size() ≤ 1`)

-...

## 9. Por qué esto importa en las entrevistas

- Los fundamentos del gráfico**: Comprensión de bordes dirigidos, indecisos, topológicos.
- Comprobación de la unidad**: Un giro sutil más allá de un tipo topológico.
- **La complejidad**: Los datos del mundo real pueden llegar a 105 bordes; usted debe permanecer lineal.
- **Destrezas de codificación**: Las implementaciones Java/Python/C++ muestran dominio de las características del lenguaje (sets, deques, unordered_set).

Muestra esta solución en tu portafolio o durante una entrevista técnica para demostrar tanto la información algorítmica como la habilidad práctica de codificación.

-...

## 10. SEO‐Optimized Wrap‐ Arriba

Si estás preparando una entrevista de codificación, dominar **LeetCode 444 – Sequence Reconstruction** te ofrece una ventaja **unica**.
- **Java** amantes: ver una lista de adyacencia basada en la Seta.
- **Python** pros: a one-liner `deque` plus `defaultdict`.
- **C+** gurus: `unordered_set` y `queue` hacen la lógica nítida.

Recuerde el proceso de dos pasos**:
1. **Construir un gráfico dirigido de subsecuencias**.
2. **Aplica el algoritmo de Kahn con un guardia de singularidad**.

Su respuesta final será rápida, eficiente en memoria y robusta contra todos los casos de borde.
Añada esto a su currículum, GitHub repo, o notas de entrevista—*sequence* su camino al éxito!

¡Feliz codificación! 🚀

-...

*End of solution. *