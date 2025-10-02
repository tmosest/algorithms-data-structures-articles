-...
Título: LeetCode 1245. Diámetro del árbol -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1245 - Diámetro del árbol
**Un “bueno, malo” Walk-through + 3‐Language Solutions + SEO‐Optimised Interview Blog**

-...

## 1. Panorama general de los problemas

■ **Diámetro del pie* *
■ Se le da un árbol *indirecto* con nodos etiquetados `0 ... n‐1`.
" Edges[i] = [ai, bi] " describe un borde entre `ai ' y ' .
■ **Regresar el diámetro** – el número de bordes en el camino más largo del árbol.

■ **Constraints**
≤ 104
* `edges.length == n‐1`
* `0 ≤ ai, bi
* `ai!= bi `

Formato típico LeetCode, perfecto para una entrevista de ingeniería **software**.

-...

## 2. Bien, mal

¿Qué es lo que está pasando?
Silencio----------------------------------------------------------------------
Silencio **Aprobación** Silencioso * Dos pasos DFS* (o BFS) es lineal, fácil de explicar. Silencio Un enfoque ingenuo de “tratar todos los pares” sería O(n2). Silencio Usar recursión para árboles profundos puede alcanzar límites de pila en algunos idiomas. Silencio
Silencioso ** Casos de Edge** Silencioso Árbol con sólo un nodo → diámetro 0. ← Olvídate de manejar hojas aisladas durante la cáscara topológica. ← Mutating la lista de adjacency en su lugar durante el DAAT (dangerous if reused). Silencio
Silencio **Performance** Silencio O(n) tiempo, O(n) espacio. Silencio DFS que rastrea la profundidad y actualiza el máximo global. Silencio BFS con una cola de tamaño n pero utilizando un 'unordered_set' para visitar cada nivel (extra overhead). Silencio
Silencio **Readability** Silencio Nombres variables claros (`maxDepth`, `diameter`). La construcción de gráficos Boilerplate puede romper la solución. ← Estructuras de datos supercomplicadas (p. ej., utilizando `Mapa realizadaSet seleccionadaInteger confianza` en Java sin ningún beneficio). Silencio
Silencio **Testing** Silencio Pruebas de la unidad para árboles pequeños, equilibrados, segados, estrella, camino. No probar el caso donde hay exactamente dos centroides. tención Prueba sólo el camino feliz (sin manejo de entrada inválido). Silencio

-...

## 3. Three Implementation Highlights

A continuación encontrará tres soluciones idiomáticas:
*Java* – clásico DFS, recursión sin pilas.
*Python* – DFS con `defaultdict(list)`.
*C+* – DFS iterativa usando una pila (sin problemas de profundidad de recursión).

Todos los fragmentos de código son auto-contenidos, comentados y listos para copiar-paste en su IDE o LeetCode.

-...

### 3.1 Java – Two‐ Paso DFS

``java
importar java.util*;

Solución de la clase pública {}
// Construir la lista de adjacency
Lista privada realizadaLista realizadaInteger confianza construyeGraph(int n, int[] edges) {
Lista realizadaLista realizadaInteger título g = nuevo ArrayList recomendado(n);
para (int i = 0; i < n; i++) g.add(nuevo ArrayList recomendado()
para (int[] e : bordes) {
g.get(e[0]).add(e[1]);
g.get(e[1]).add(e[0]);
}
retorno g;
}

// Ayudador DFS que devuelve la profundidad máxima del nodo
int privado dfs(int node, int parent, List armonizado) {}
int max1 = 0, max2 = 0; // dos niños más profundos
para (int nei : g.get(node)) {}
si (nei == padre) continúan;
int deep = dfs(nei, node, g);
si (con profundidad) máx1) { max2 = máx1; máx1 = profundidad; }
si (con profundidad) máx2 { max2 = profundidad; }
}
// Actualizar el diámetro global (pata pasa por el nodo)
diámetro = Math.max(diameter, max1 + max2);
máx1 + 1; // profundidad de subárbol
}

diámetro interior privado = 0;

int treeDiameter(int[] edges) {
si (edges == null ¦ 0) retorno 0;
int n = edges.length + 1;
Lista realizadaLista realizadaInteger confianza graph = buildGraph(n, edges);
dfs(0, -1, gráfico); // root at 0 (any node works)
diámetro de retorno;
}
}
`` `

*Las complejidades: *
- *Hora*
- **Espacio:** O(n) (lista de adyacencia + pila de recursión)

-...

### 3.2 Python – Recursive DFS

``python
de las colecciones importadas por defecto
de la importación Lista

Solución de clase:
def árbolDiameter(self, edges: List[List[int]]) int:
si no bordes:
retorno 0

# Build adjacency list
gráfico = defaultdict(list)
para a, b en los bordes:
graph[a].append(b)
graph[b].append(a)

autodiametro = 0

def dfs(nodo: int, parent: int) - int:
profundidades = [0, 0] # dos profundidades infantiles más largas
para nb en el gráfico [nodo]:
si nb == padre:
continuar
d = dfs(nb, node) + 1
[0]:
profundidades[1] = profundidades[0]
profundidades [0] = d
elif d ' profundidades[1]:
profundidades[1] = d
auto.diametro = max(self.diameter, deeps[0] + profundidades[1])
profundidades de retorno[0]

dfs(0, -1)
Vuélvete. diámetro
`` `

*Las complejidades: *
- *Hora*
- **Espacio:** O(n) (grafo + profundidad de recursión)

-...

### 3.3 C++ – Iterative DFS (no recursion)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
árbol intDiámetro(vector seleccionadovector seleccionador) {}
si (edges.empty()) devuelve 0;
int n = edges.size() + 1;

/ Lista de adyacencia
vector realizador:
para (auto &e : bordes) {}
g[e[0].push_back(e[1]);
g[e[1]].push_back(e[0]);
}

int diámetro = 0;
vector asignadoint -1);
vector de profundidad(n, 0);
apilación especificado st;
st.push(0); // arbitrary root

// Post-order traversal
orden de vectores:
(!st.empty())) {}
int v = sttop(); st.pop();
orden.push_back(v);
para (int nb : g[v]) si (nb != parent[v]) {}
parent[nb] = v;
st.push(nb);
}
}

// Nodos de proceso en inversa (post-orden)
para (int i = order.size() - 1; i ±= 0; --i) {
int v = order[i];
int best1 = 0, best2 = 0;
para (int nb : g[v]) si (nb != parent[v]) {}
int d = profundidad[nb] + 1;
si (d > best1) { best2 = best1; best1 = d; }
si (d √≠ best2) { best2 = d; }
}
diámetro = máx(diametro, mejor1 + mejor2);
profundidad[v] = mejor1;
}
diámetro de retorno;
}
};
`` `

*Las complejidades: *
- *Hora*
- **Espacio:** O(n) (lista de adyacencia + pila + arrays)

-...

## 4. Por qué funciona el DFS Two‐Pass (o One‐Pass)

1. **El camino más largo implica dos hojas**
El diámetro es siempre un camino entre dos nodos de hoja.
Durante el DFS rastreamos las profundidades más largas y segundas de cada nodo – la suma de estas dos profundidades es el camino más largo que pasa a través de ese nodo.

2. **Global Max Update**
Si bien desbloqueamos la recursión mantenemos una variable de `diametro' global actualizada con `max(diametro, profundidad1 + profundidad2)`.

3. *Paso de silencio*
El algoritmo visita cada borde dos veces (una vez desde cada lado), por lo que el trabajo general es lineal.

-...

## 5. Pitfalls comunes " Cómo evitarlos

Silencio Pitfall Silencioso Silencioso
Silencio------------
Silencio **Desbordamiento de la cubierta** (arboles deshuesados) Silencio RuntimeError / RecursiónError ← Utilizar DFS iterante ( ejemplo C++) o aumentar el límite de recursión en Python (`sys.setrecursionlimit`). Silencio
Silencio **Escoge incorrecta de raíz** Silencio Diámetro equivocado Silencio Cualquier obra de nodo; sólo elegir 0 o el primer nodo de `edges`. Silencio
Silencio **No Actualizar Padre** Silencio Revisiting edges TEN Mantener una matriz de 'padre' o pasar padre en DFS para evitar ciclos. Silencio
Silencio **Mis-counting Edges vs Nodes** Silencio Diámetro apagado por 1 Silencio Recordar el diámetro cuenta *edges*, así que agrega 1 cuando se mueve a un niño (`a profundidad = niñoDepth + 1`). Silencio

-...

## 6. Entrevista " Valor de resumen "

* ** Estructuras de datos:** Gráfico, lista de adyacencia, recursión/stack.
* **Algorithms:** Primera búsqueda, programación dinámica en los árboles.
* ** Análisis de la complejidad* Tiempo lineal & espacio – crucial para entrevistas de rendimiento.
* **Testing " Edge‐Case Handling:** Demuestra la atención al detalle.

Al escribir su currículum:

`` `
- Solved LeetCode #1245 “Diámetro de Tree” – implementada eficiente solución O(n) DFS en Java, Python y C++.
- Capacidad demostrada para analizar el tiempo/espacio de intercambio y manejar la recursión profunda a través de enfoques iterativos.
- Muestra una fuerte comprensión de la programación traversal gráfica y dinámica en los árboles.
`` `

-...

## 7. SEO‐Optimized Blog Article (For Job Seekers)

### Title
*Cracking LeetCode* 1245 – Diámetro del árbol: Java, Python, " C++ Soluciones " Consejos de entrevista "* *

## Meta Descripción
■ Master LeetCode “Tree Diameter” (1245) con código Java, Python y C++. Aprenda el algoritmo, el manejo de los bordes y las explicaciones de entrevista para aterrizar su próximo trabajo de ingeniería de software.

## Headings > Content

Silencio encabezamiento Silencioso Silencio Palabras clave
Silencio----------------------
Silencio **¿Qué es el Diámetro del Árbol? ** Silencioso diámetro de los árboles, LeetCode 1245
Silencio **¿Por qué es un problema de entrevista clásica?** Silencio Discuss relevancia algorítmica. entrevista de software, estructuras de datos
tención **Dos-Pass DFS Explicado** ← Algoritmo básico. TENIENDO DFS, algoritmos de árboles, O(n)
Silencio **Java Implementation** Silencio Código completo + explicación. Java DFS, LeetCode Java Silencio
Silencio **Python Implementation** Silencio Código completo + explicación. Python DFS, LeetCode Python Silencio
Silencio **C++ Implementación** Silencio Código completo + explicación. ← C++ DFS, LeetCode C++
Silencio ** Errores comunes de depuración** ¦ Pitfalls.
tención **Performance & Complexity** tención Tiempo/espacio. Silencioso análisis de algoritmos, O(n)
Silencio **Entrevista Take-aways** Silencio Cómo discutir la solución. Extremidades de entrevista en tóxico, charla de algoritmos
Silencio **Añadir a su resumen** Silencio Cómo frase. Consejos de reanudación de la vida, entrevista de codificación

### Intro Párrafo
El problema del Diámetro del Árbol (LeetCode #1245) es un elemento básico para entrevistas de ingeniería de software. Prueba tu comprensión de la traversal gráfica, la recursión y la programación dinámica en los árboles. En este post caminaremos a través de la solución O(n) óptima, le mostraremos limpiar Java, Python y C++ implementaciones, y le daremos puntos de conversación listos para entrevistas que impresionarán a los gerentes de contratación.”*

### Closing CTA
■ “Prueba el código de LeetCode, añádelo a tu GitHub, y mentítalo en tu próxima entrevista. ¿Quieres más preparación para entrevistas? Suscríbete a nuestro boletín para pasarelas semanales. ”

-...

## 8. Lista final para entrevistadores

- ** Explique el algoritmo** en términos simples.
- **Mostrar el código** y resaltar dónde se actualiza el diámetro.
- ** Casos de borde de debate** (grafo vacío, nodo único).
- **Hablar sobre la complejidad** y los posibles límites de pila.
- ** Comercio de mención** (recursivo contra iterativo).

Buena suerte aterrizando ese papel – acabas de resolver un problema clásico en tres idiomas principales! 🚀

-...

¡Feliz codificación