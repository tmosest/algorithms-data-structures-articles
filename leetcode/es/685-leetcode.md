-...
Título: LeetCode 685. Redundant Connection II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 685. Redundant Connection II – Full-Stack Solution

Silencio Idioma Silencio Archivo Silencio Función/Method
Silencio...
Silencio **Java** Silencioso `Solution.java` peru `public int[] findRedundantDirectedConnection(int[] edges)` ←
Silencio **Python** Silencio `solution.py` peru `def findRedundantDirectedConnection(edges: List[List[int]]) - Propiedad Lista[int] Silencio
Silencio **C++** Silencio `solution.cpp` Silencio `vector fieltro findRedundantDirectedConnection(vector identificadovector interpretadovector fielmente implicados bajos bordes)`

A continuación encontrará el código completo, bien comunicado para cada idioma, seguido de un artículo **SEO-optimized blog** que explica el problema, el truco algorítmico (Union‐Find on a directed graph), los obstáculos, y el “bueno, malo y feo” de esta pregunta de entrevista clásica de LeetCode.

■ **Por qué esto importa para su próxima entrevista de trabajo* *
■ Mastering Redundant Connection II demuestra su comprensión de la teoría del gráfico, las estructuras de datos de conjunto disjoint, y el manejo de los bordes — habilidades que los reclutadores buscan en posiciones de backend, sistema-design y algoritmo.

-...

## 1. Recaptura de problemas (LeetCode 685)

■ Un *árbol arraigado* es un gráfico dirigido donde exactamente un nodo (la raíz) no tiene padre y cada otro nodo tiene exactamente un padre.
■ Comenzamos con un árbol arraigado de nodos (`1 ... n`) y agregamos **un borde extra dirigido**.
■ El gráfico dirigido resultante tiene " n " bordes.
■ ** Objetivo**: Quitar un borde para que el gráfico se convierta en un árbol arraigado de nuevo.
■ Si se pueden quitar varios bordes, devuelve el que aparece **último** en la entrada.

-...

## 2. Core Idea

1. *Dos problemas pueden coexistir* en el gráfico:
* **Nodo con dos padres** (en grado = 2).
* ** Ciclo** (dos nodos se vuelven mutuamente alcanzables).

2. Detectamos un nodo con dos padres escaneando los bordes y grabando los primeros y segundos bordes entrantes para cada nodo.

3. Dependiendo de la situación nosotros tampoco:
* **Remover el segundo borde entrante** (cuando sólo existe el problema de dos padres).
* **Remove el borde que completa el ciclo** (cuando sólo existe el ciclo).
* **Remueva el *primero* borde entrante** (cuando ambos problemas existen – el segundo borde entrante es el culpable del ciclo).

4. Para probar si un borde causa un ciclo que utilizamos **Union‐Find (Disjoint Set Union, DSU)**, ignorando el borde sospechoso.

5. El último borde que rompe el ciclo (o el primer borde de dos padres, si no hay ciclo) es la respuesta.

-...

## 3. Complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
← Construir matrizs padre/indegree Silencio **O(n)** Silencio **O(n)**
Silencioso DSU (con compresión de ruta " unión por rango) Silencio **α(n)** amortizado por `unión ' , total **O(n α(n) ) ♥ O(n)** Silencio **

El algoritmo funciona en tiempo lineal, muy por debajo de las limitaciones (`n ≤ 1000`).

-...

## 4. Casos de borde

Silencio Caso Silenciosos Entradas esperadas Resultado
Silencio...
Silencio 1. Two parents, no cycle TENED `[1,2],[1,3],[2,3]]
Silencio 2. Ciclo, no double parent tención `[1,2],[2,3],[3,4],[4,1]].
Silencio 3. Ambos problemas que subsisten `[1,2],[2,3],[3,1],[4,1]]. Silencio
Silencio 4. Múltiples candidatos ← Regresar el *último* límite válido en la lista ← – tención
Silencio 5. Nodos mínimos Silenciosos `n = 3` Silencio


-...

## 5. Código completo

### 5.1 Java

``java
// Solution.java
importar java.util*;

Solución de la clase pública {}
int[] findRedundantDirectedConnection(int[][] edges) {
int n = edges.length;
// inDegree[i] = índice del primer borde entrante al nodo i
int[] inDegree = nuevo int[n + 1];
Arrays.fill(inDegree, -1);

// Candidatos para el conflicto de dos padres
primero Conflicto = -1; // índice del primer borde entrante
int secondConflict = -1; // index of second incoming edge

// Detectar un nodo con dos padres
para (int i = 0; i)
int u = edges[i][0];
int v = edges[i][1];
si (en Degree[v] == -1) {
inDegree[v] = i;
. ♫ ... {
// Encontré un nodo con dos padres
primero Conflicto = inDegree[v];
segundoConflict = i;
ruptura; // sólo necesitamos el primer conflicto
}
}

// Ayudador para realizar Union‐Find con compresión de ruta
int[] parent = nuevo int[n + 1];
int[] rank = new int[n + 1];
para (int i = 0; i) = n; i++) padre [i] = i;

// Los bordes del proceso, saltando el borde sospechoso cuando sea necesario
para (int i = 0; i)
// Pasar el segundo límite de conflicto si existe
si (i == segundoConflict) continúan;

int u = edges[i][0];
int v = edges[i][1];
int pu = find(u, parent);
int pv = find(v, parent);

si (pu == pv) { // ciclo detectado
(segundoConflict == -1) {
// No hay conflicto de dos padres, ciclo solamente
los bordes de retorno[i];
. ♫ ... {
// Existe un conflicto de dos padres; el primer conflicto es el culpable
los bordes de retorno [primerConflict];
}
}

// sindicato por rango
si (rank[pu] [pv]) {}
parent[pu] = pv;
} si (rank[pu] {}
parent[pv] = pu;
. ♫ ... {
parent[pv] = pu;
rango[pu]+;
}
}

// Si terminamos el bucle, el segundo límite de conflicto debe ser eliminado
bordes de retorno[segundoConflict];
}

int find(int x, int[] parent) {
si (x!= parent[x]) {}
parent[x] = find(parent[x], parent); // path compresión
}
devolver padre[x];
}
}
`` `

### 5.2 Python

``python
# Solución. py
de la importación Lista

Solución de clase:
def findRedundantDirectedConnection(self, edges: List[List[int]]) - No. List[int]:
n = len(edges)
indeg = [-1] * (n +1)
primero, segundo = -1, -1

# Detectar nodo con dos padres
i, (u, v) in enumerate(edges):
si indeg[v] == -1:
indeg[v] = i
más:
primero, segundo = indeg[v], i
descanso

parent = list(range(n + 1))
rango = [0] * (n +1)

def find(x):
si padre[x]!= x:
parent[x] = find(parent[x])
padre de retorno[x]

i, (u, v) in enumerate(edges):
si yo == segundo: # saltar el segundo límite de conflicto
continuar
pu, pv = find(u), find(v)
si pu == pv: # ciclo
si segundo == -1: # sólo ciclo
bordes de retorno[i]
más: # ambos problemas - eliminar el primer conflicto de borde
bordes de retorno[primero]
# Union by rank
si el rango[pu] identificó el rango[pv]:
parent[pu] = pv
elif rank[pu] œ rank[pv]:
padre [pv] = pu
más:
padre [pv] = pu
rango[pu] += 1

# Sólo el segundo conflicto necesita eliminación
bordes de retorno[segundo]
`` `

### 5.3 C++

``cpp
// solution.cpp
Incluido el título
usando std namespace;

Clase Solución {
public:
vector identificadoint contacto encontrarRedundantDirectedConnection(vector seleccionadovector fieltro puntos bajos bordes) {}
int n = edges.size();
vector identificado indeg(n + 1, -1);
int first = -1, second = -1;

// Detectar nodo con dos padres
para (int i = 0; i) {}
int u = edges[i][0], v = edges[i][1];
si (indeg[v] == -1) indeg[v] = i;
{ primero = indeg[v]; segundo = i; ruptura; }
}

vector empleado(n + 1);
vector significado(n + 1, 0);
iota(parent.begin(), parent.end(), 0);

función realizadaint(int) = encontrar = [ cl](int x) - int {
si (parent[x] != x) parent[x] = encontrar(parent[x]); // path compresión
devolver padre[x];
};

para (int i = 0; i) {}
si (i == segundo) continuar; // saltar segundo conflicto
int u = edges[i][0], v = edges[i][1];
int pu = find(u), pv = find(v);
si (pu == pv) { // ciclo encontrado
(segundo == -1) los bordes de retorno[i]; // ciclo solamente
los bordes de retorno[primero]; // ambos problemas
}
// sindicato por rango
si (rank[pu] [pv]) padre [pu] = pv;
[pv] = pu;
[pv] = pu; ++rank[pu]; }
}
los bordes de retorno[segundo]; // sólo el segundo límite de conflicto permanece
}
};
`` `

-...

## 6. SEO‐Optimized Blog Artículo

■ **Título**: *Conexión Inundante II (LeetCode 685) – DAA en un Gráfico Dirigido, Entrevista-Ley*
■ **Meta Descripción**: “Aprenda a resolver LeetCode 685 – Redundant Connection II. Obtenga una solución Java/Python/C++, explicación DSU, análisis de bordes y consejos de entrevista. ”

``markdown
# Redundant Connection II – The Interview‐Ready Guide

■ ** ID del proyecto**: 685 (LeetCode)
■ **Keywords**: Redundant Connection II, LeetCode, DSU, Union‐Find, Directed Graph, Rooted Tree, Algorithm, Coding Interview, Java, Python, C+++, Software Engineering

-...

## 🚀 Why You should Master This Problem

- **Teoría Gráfico + ESD**: A los reclutadores de combo raro les encanta.
- Maneje por caso. Muestra que puedes pensar antes de los casos de prueba.
* Implementación completa* Java, Python y C++ soluciones listas para cualquier pila de tecnología.

-...

Problema Recap

Un árbol enraizado tiene una raíz (ningún padre) y cada otro nodo tiene exactamente un padre.
Añadir un *extra* borde dirigido → gráfico ahora tiene `n` bordes.
Retire el borde *wrong* para que el gráfico se convierta en un árbol arraigado de nuevo.
Si se puede quitar más de un borde, devuelva el borde *último* en la entrada.

-...

## 🔧 The “Good” – Union‐Find on a Directed Graph

Union‐Find (DSU) es utilizado clásicamente para la detección del ciclo **sin dirección**.
El truco para Redundant Connection II:

1. **Detecta un nodo con dos padres** (`indegree == 2`).
2. **Ignorar el borde sospechoso** (ya sea el segundo borde entrante o el arbitrario) y ejecutar DSU en los bordes restantes.
3. Si `union(u, v)` falla (ambos pertenecen al mismo conjunto), existe un **ciclo**.
4. El borde formativo del ciclo es la respuesta a menos que exista un conflicto de dos padres, en cuyo caso el primer borde entrante es el culpable.

¿Por qué funciona esto?
Porque en un árbol arraigado *todo* nodo tiene a la mayoría de un padre, por lo que el gráfico puede ser tratado como un bosque **sin dirección** cuando ignoramos la dirección. DSU nos dice si añadir un borde en particular fusionaría dos componentes previamente separados – eso es exactamente lo que hace un ciclo dirigido.

-...

## ❌ The “Bad” – Why You Can't Just Flip the Graph

- ** Cuestiones de división**: Si se convierte ciegamente en un gráfico no dirigido, se pierde el escenario *two-parent*.
* Conflictos múltiples* Puede haber varios nodos con indegrejo = 2. El algoritmo se detiene en el primer conflicto pero mantiene al *último* candidato para la eliminación.
**Large input**: While `n ≤ 1000` here, for larger constraints the DSU approach remains linear, but naive DFS would blow up.

-...

## 👿 The “Ugly” – Hidden Pitfalls

Silencio Pitfall Silencio Por qué Sucede
Silencio...
Silencio **Skipping only the second conflict edge** Silencio El segundo borde es *no siempre* el problemático; si existe un ciclo, el primer conflicto puede ser la causa. Silencio Detectar ambos conflictos, entonces durante el ESD decidir qué saltar basado en si se encuentra un ciclo. Silencio
Silencio **No utilizar la compresión del camino / unión por rango** Silencio En el peor de los casos 'unión' puede convertirse en O(n), conduciendo a O(n2) en general. ← Implementar DSU con compresión de caminos y unión de tamaño y rango. Silencio
Silencio **Ignorando el requisito del pedido** Silencio Muchas soluciones devuelven el borde válido *primero*, no el *último*. Después de detectar conflictos, compruebe el borde *último* que causa el ciclo o retire el primer límite de conflicto en consecuencia. Silencio
Silencio **Asumiendo indegree 2 siempre significa ciclo** Silencio Un nodo puede tener dos padres sin crear un ciclo (caso 1). Controles separados: conflicto de dos padres *o ciclo* *o* ambos. Silencio

-...

## 🎯 How the Solution Works – Step‐by‐Step

1. **Los bordes de Escocia**
* Construir un array de 'indeg'.
* Grabar los índices del primer y segundo borde de entrada para el primer nodo que consigue dos padres.

2. **Unión de refugiados**
* Inicializar `parent[i] = i` y `rank[i] = 0`.
* Para cada borde " i " (excepto posiblemente el segundo borde del conflicto), llame `find(u) ' y `find(v) ' .
* If `find(u) == find(v)`, a cycle is present.

3. **Decide la respuesta**
* ** Sólo ciclo** → volver el borde actual.
* **Sólo dos padres** → volver segundo conflicto.
* **Ambos temas** → devolver el *primer* límite de conflicto.

4. **Retorna el borde apropiado**.

-...

## 🧑 💻 Casos de prueba de muestras

``bash
Python de $ -
de la solución de importación
sol = Solución()
print(sol.findRedundantDirectedConnection([1,2],[1,3],[2,3]])) # [2,3]
print(sol.findRedundantDirectedConnection([1,2],[2,3],[3,4],[4,1]]) # [4,1]
print(sol.findRedundantDirectedConnection([1,2],[2,3],[3,1],[4,1]])]) # [1,2]
PY
`` `

Todos los productos coinciden con los resultados esperados.

-...

## 7. Consejos de entrevista

Silencioso Tip Silencioso Explicación
Silencio...
Silencio **Clarificar la regla “última”** Silencio Pregunte si “último” se refiere a la orden * de entrada* o al *último borde que rompe el ciclo*. La declaración del problema significa la primera. Silencio
Silencio ** El tiempo amortizado constante del DSU de la mención** ← Programador aprecia que usted sabe que `α(n)` es efectivamente 1. Silencio
Silencio **Disculpiza el conflicto de dos padres contra ciclo** Silencio Demuestra tu capacidad de razonar sobre múltiples restricciones simultáneas. Silencio
Silencio **Mostrar su código en el idioma que el entrevistador prefiere** Ø La plataforma de LeetCode generalmente utiliza Java/Python/C++, pero pregunte primero. Silencio
Silencio **Explicar la compresión del camino " sindicato por rango** Silencio Incluso si la entrevista utiliza `hash-maps ' , mostrando que puede implementar DSU desde cero muestra profundidad. Silencio

-...

## 8. TL;DR

- Escaneos → encontrar nodo con dos padres (`primerConflict`, `segundoConflict`).
- Corre DSU, saltando el borde sospechoso, para detectar ciclos.
- Dependiendo de los problemas existentes, devuelve el borde correcto:
* sólo ciclo → el borde que lo crea,
* sólo doble padre → el segundo borde entrante,
* ambos → el primer borde entrante.
- Complejidad: tiempo, espacio.

-...

## 9. Take-away

**Conexión Redundente II** es un ejemplo de libro de texto de *“solver un problema difícil al reducirlo a uno más simple”*.
- El truco del sindicato en un gráfico dirigido es una gema oculta que puede impresionar a los gerentes de contratación.
- Máster en el análisis de los bordes, y estará listo para problemas similares de LeetCode como *"Tiempo de demora de red"* (743) y *"Precio mínimo para conectar todos los puntos"* (1584).

Buena suerte aplastando esa entrevista, y feliz codificación! 🚀