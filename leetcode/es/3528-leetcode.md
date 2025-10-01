-...
Título: LeetCode 3528. Conversión de Unidad Yo...
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código de Solución

A continuación, ** tres soluciones totalmente operativas, listas para la producción** para LeetCode 3528 – Conversión de Unidad I.
Cada solución funciona en **O(n)** tiempo y **O(n)** memoria, manejando fácilmente los límites (`n ≤ 105`, `factor ≤ 109`).

Silencio Idioma Silencio Key Idea ← Complejidad
Silencio--------------------------
Silencio **Java** Silencio Iterative DFS on a directed tree (root 0) – product modulo *M*  **O(n)** time, **O(n)** memory ←
Silencio **Python** Silencio Iterative DFS / pila de producto modulo *M* Silencio **O(n)** tiempo, **O(n)** memoria
Silencio **C++** Silencio DFS basado en Stack – modulo de producto *M* Silencio **O(n)** tiempo, **O(n)** memoria Silencio

■ *Nota*
■ El problema garantiza que `conversiones` forman un árbol **directo arraigado en 0** (camino único de 0 a cada nodo).
■ Por lo tanto, una simple propagación de profundidad del producto es suficiente – sin necesidad de BFS o Dijkstra.

-...

### 1.1 Java – `Solution.java `

``java
importar java.util*;

Solución de la clase pública {}
int final estático privado MOD = 1_000_000_007;

int[] baseUnitConversions(int[][] conversiones) {
int n = conversiones.length + 1;
Lista hecha [] título [] gráfico = nuevo ArrayList[n];
para (int i = 0; i) no; i++) grafo[i] = nuevo ArrayList fiel();

// Construir la lista de adyacencia dirigida
para (int[] e : conversiones) {}
int src = e[0], tgt = e[1], factor = e[2];
graph[src].add(new int[]{tgt, factor});
}

long[] ans = new long[n];
ans[0] = 1L; // 1 unidad del tipo 0 equivale a 1 unidad del tipo 0
Deque cumplióInteger confianza stack = nuevo ArrayDeque correspondió();
stack.push(0);

mientras (!stack.isEmpty()) {}
int u = stack.pop();
for (int[] edge : graph[u]) {}
int v = edge[0];
largo f = borde[1];
as[v] = (ans[u] * f) % MOD;
stack.push(v);
}
}

// Convertir en array int antes de regresar
int[] result = new int[n];
para (int i = 0; i) no; i++) resultado[i] = (int) ans[i];
Resultado de retorno;
}
}
`` `

-...

### 1.2 Python – `solution.py `

``python
de la importación Lista

MOD = 10**9 + 7

Solución de clase:
def base UnitConversions(self, conversions: List[List[int]) - No. List[int]:
n = len(conversiones) + 1
g = [[] for _ in range(n)]
para src, tgt, f en conversiones:
g[src].append((tgt, f)))

a)
ans[0] = 1
pila = [0]

mientras que la pila:
u = pila.pop()
for v, f in g[u]:
as[v] = (ans[u] * f) % MOD
stack.append(v)

Retorno
`` `

-...

### 1.3 C++ – `solution.cpp `

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
static const int MOD = 1'000'007;

basal de títulos vectorialesUnitConversiones(vector seleccionadovector fielint implica conversiones) {}
int n = conversiones.size() + 1;
vector realizador designadopair realizado,largo largo título g(n);
para (auto &e : conversiones) {}
int src = e[0], tgt = e[1];
largo f = e[2];
g[src].push_back({tgt, f});
}

vector realizado largamente uns(n, 0);
ans[0] = 1;
apilación especificado st;
st.push(0);

(!st.empty())) {}
int u = st.top(); st.pop();
para (auto &p : g[u]) {}
int v = p. primero;
largo f = segundo;
as[v] = (ans[u] * f) % MOD;
st.push(v);
}
}

vector asignadoint título res(n);
para (int i = 0; i) no; ++i) res[i] = static_cast fielint(ans[i]);
restitución;
}
};
`` `

Las tres implementaciones utilizan **iterative DFS** (stack) para evitar el desbordamiento de pilas para árboles profundos (hasta 100 000 nodos).
Difunden el producto de factores de conversión de la raíz (unidad 0) a cualquier otro nodo, tomando el modulo `1 000 000 007` según sea necesario.

-...

## 2. Blog Artículo – “Unit Conversion I on LeetCode: The Good, The Bad, and The Ugly”

■ **SEO Palabras clave: *LeetCode 3528*, *Unit Conversion*, *Java solution*, *Python solution*, *C++ solution*, *DFS*, *BFS*, *graph tree*, *coding interview*, *job interview*, *algorithm analysis*, *software engineer interview*, *coding interview questions*

-...

#### 2.1 Introduction

Cuando estás preparando una entrevista de ingeniería de software, el juego de problemas LeetCode es tu patio de juegos. Entre los muchos desafíos “medium”, **Unit Conversion I (LeetCode 3528)** destaca: prueba traversal gráfico, aritmética modular y la capacidad de detectar estructura oculta en la entrada.

En este post diseccionaremos el problema, caminaremos a través de las soluciones más elegantes en **Java, Python y C+**, y discutiremos:

* **El Bien * – por qué el problema es una gran pregunta de entrevista
* **The Bad** – trampas comunes que tropiezan con candidatos
* **El Ugly** – matices del borde que pueden romper silenciosamente su código

Al final tendrás una solución lista para la producción y una narrativa clara para compartir con los entrevistadores.

-...

### 2.2 Problema Recap

Se le da `n` tipos de unidad (0 ... n‐1) y un array `conversiones` de longitud `n-1`.
Cada elemento `conversiones[i] = [fuente, objetivo, factor] ' significa *1 unidad de `fuente ' equivale a unidades `factor ' de `target '*.

** Objetivo:** Para cada unidad tipo `i`, computa cuántas unidades de tipo `i` son equivalentes a * una unidad de tipo `0`. Regresar el modulo de resultados `1 000 000 007`.

**Constraints* *

* `2 ≤ n ≤ 105`
* `1 ≤ factor ≤ 109 `
* El gráfico es un árbol **directo arraigado en 0** (camino único de 0 a cualquier nodo).
* La respuesta puede ser enorme, por lo que el modulo `MOD = 1 000 000 007` es obligatorio.

-...

### 2.3 Spotting the Hidden Structure – The Good

El problema parece un problema genérico de “grafo ponderado”, pero la línea extra de las restricciones es un *golden ticket*:

■ *Se garantiza que la unidad 0 se puede convertir en cualquier otra unidad a través de una combinación única de conversiones. *

Eso significa que la entrada es en realidad un árbol **directo** (sin ciclos, sin ramificar de la raíz de vuelta a sí mismo). En la teoría del gráfico, los árboles son las estructuras conectadas más simples. Una vez que reconoces esto, todo el problema se reduce a un único DFS/BFS que multiplica los pesos del borde a lo largo del camino único.

¿Por qué es una buena idea de entrevista?

1. **Ahorros de tiempo** – evitas algoritmos genéricos de cortocircuito (Dijkstra, Bellman‐Ford) que de otro modo serían exagerados.
2. **Claridad** – una clara declaración de problemas → una estrategia de solución clara → un entrevistado confiado.
3. **Optimización** – usted puede implementar un algoritmo *(n)* que encaja cómodamente en 1 s límite de tiempo.

-...

### 2.4 El Algoritmo – Propagación DFS

*Core idea*
Partiendo de la raíz (unidad 0), atraviesa el árbol.
Por cada borde `u → v` con peso `w`, propagar

`` `
valor[v] = valor[u] * w mod MOD
`` `

Debido a que el camino de 0 a cualquier nodo es único, no hay necesidad de "mejor camino" lógica o colas prioritarias.

**Detalles de aplicación**

Silencio Qué hacer Silencio ¿Por qué importa
Silencio...
← Construir la lista de adyacencia Silencioso `Lista realizadaint[] g = nuevo ArrayList[n];` Silencioso búsqueda de vecino rápido (`O(1)` por borde). Silencio
Silencio Utilice una pila iterativa/cuue Silencio `Deque Haga clic enInteger stack = nuevo ArrayDeque quiere decir:();` Silencio Evita los límites de profundidad de recursión (100 000 nodos). Silencio
tención Mantener " valores intermedios largos " TENIDO `long val = ans[u] * w % MOD; " TENIDO " puede ser hasta " 109 " ; el producto puede rebosar " . Silencio
Silencio Retorno `int[]` Silencio Convertir el `long[] ans` a `int[]` antes de regresar a la firma de LeetCode requiere `int[]. Silencio

■ **BFS vs. DFS**
■ Ambos están bien. DFS (stack) es un poco más amigable para los árboles porque sólo necesita almacenar los valores de los padres. BFS (cuue) haría lo mismo con esencialmente la misma sobrecarga.

-...

## 2.5 Code Walkthrough – The Ugly Edge Cases

Silencio Idioma Silencio Comune error Silencio
Silencio...
Silencio **Java** Silencio Retornando `long[]` directamente Silencio LeetCode espera `int[]`. La conversión final es obligatoria. Silencio
Silencio **Python** Silencio Usando `stack = [0]` y `stack.pop()` tención Funciona, pero un `deque` da un rendimiento ligeramente mejor para la grande n. Silencio
Silencio **C++** Silencio Usando `int` para pesas Silencio Convertirse en `long' antes de la multiplicación. Silencio

##### Edge‐ Caso 1: Modulo “Zero”
Cuando `factor` es un múltiple de `MOD`, `factor % MOD` se convierte en 0 y propaga ceros río abajo. Eso es *correcto* porque el modulo aritmético se comporta de esa manera. Asegúrese de aplicar el modulo ** después** cada multiplicación, no sólo al final.

##### Edge‐ Caso 2: Desbordamiento de enteros de 32 bits
`1 000 007 × 109` supera el rango de enteros firmados de 32 bits ( ' ♥ 2.1×109`).
Utilizando `long` (64-bit) para el producto intermedio y luego tomando `mod` garantiza la corrección.

##### Edge‐ Caso 3: Tamaño de la talla en la recuperación
Un DFS recursivo ingenuo puede soplar la pila de llamadas JVM/CPython/C++ en un árbol profundo. Usar una pila explícita (`ArrayDeque` / `std::stack`) es un *must*.

-...

### 2.5 Complexity Analysis

← Algorithm Silencio Silencio
Silencio----------------
Silencio Iterative DFS Silencio **O(n)** (todo el filo del nodo visitado una vez) Silencio **O(n)** (graph + answer array)
TENIDO BFS / cola TENIDO Igual que DFS
Silencio Genérico Dijkstra (si usted ignora la propiedad de los árboles)

La solución óptima es la más simple y rápida, dándole una ventaja **10 puntos** en una entrevista.

-...

### 2.6 Interview‐ Consejos listos

1. ** Explique primero la propiedad del árbol** – pregunte al entrevistador si el gráfico está garantizado a ser un árbol. Muestra que estás buscando restricciones ocultas.
2. **Clarificar la operación modulo** – asegúrate de que el entrevistador sepa que tomarás `mod` en *toda multiplicación*, no sólo la respuesta final.
3. **Discuss stack vs recursion** – mencionar por qué un enfoque iterativo es más seguro para el límite 100 000 de LeetCode.
4. **Mostrar el código en varios idiomas** – se puede decir “Tengo un DFS limpio, O(n) en Java/Python/C+” y dejar los snippets como una mano.

-...

### 2.7 Lo que el Contratista notará

* **Reconocimiento de Patrón** – observar la estructura de árboles es un sello distintivo de un códice experimentado.
* **Atención a Detalle** – manejar correctamente el modulo, utilizando `long` para evitar el desbordamiento, y elegir un traversal iterativo todos demuestran la codificación de producción.
* **Comunicación** – caminar a través del algoritmo paso a paso muestra que usted puede explicar ideas complejas simplemente – una habilidad crítica suave para los roles mayores.

-...

### 2.8 Bono: Cómo utilizar este problema para un Pitch “Real‐World”

Si usted está solicitando un **Ingeniero de batería** o **Ingeniero de sistemas** papel, puede enmarcar su solución como un “motor de conversión modular”.
* “Construí un sistema de propagación basado en árboles ligeros que puede extenderse a gráficos arbitrarios dirigidos. ”
* “El patrón aritmético modular que usé aquí es exactamente lo que empleamos en controles de acceso basados en token. ”

Estas conexiones le ayudan a convertir un problema de codificación en un **story sobre arquitectura** que los administradores de contratación aman.

-...

### 2.9 Pensamiento Final

Conversión de unidad Soy engañosamente simple una vez que leas cuidadosamente las limitaciones.
Un DFS/BFS limpio que multiplica pesos a lo largo de un árbol es la estrategia *optimal*.
Con las tres muestras de código anteriores, usted está listo para impresionar a cualquier entrevistador - si piden **Java**, **Python**, o **C+**.

■ **Siguientes pasos**
■ 1. Ejecute las soluciones en el arnés de prueba de LeetCode.
■ 2. Añádalos a su “ficha de entrevista personal”. ”
■ 3. Práctica explicando la propiedad de los árboles y el algoritmo de propagación – la pregunta más frecuente será *“¿Por qué eligió DFS sobre Dijkstra?”*

Buena suerte, y que su entrevista sea tan suave como un árbol perfectamente equilibrado!

-...

### 2.10 TL;DR

Silencio Lo que aprenderás | Quién ayuda a vivir
Silencio...
Silencio Reconocimiento de árboles en problemas de gráficos Silencio **Entrevistadores** – muestra la percepción
Silencio O(n) DFS propagation with modulo tención **Candidates** – fácil de código, rápido
← Código Java/Python/C++ para la producción _ All** – copy‐paste into your IDE ←

Deja estos fragmentos en tu cartera, ponlos en contra de las pruebas de LeetCode y trae el **story** de "el árbol oculto" a tu próxima entrevista. Buena suerte, y disfrute de la conversión de unidades de tiempo en entrevista gana!