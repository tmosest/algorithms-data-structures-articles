-...
Título: LeetCode 3310. Eliminar métodos del proyecto -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 3310 – Remove Methods From Project
**Solución en Java, Python & C++ + SEO‐Optimised Blog Post**

-...

## TL;DR (Lo que aprenderás)

Silencio Idioma Silencio Tiempo Complejidad Silencio Complejidad Espacial Silencio Key Idea Silencio
Silencio------------------------
Silencio **Java** Silencio **O(n + m)** Silencio **O(n)** Silencio DFS / BFS para recopilar métodos *sospechosos*, luego un solo escaneo para comprobar por “llamadores externos”
Silencio **Python** Silencio **O(n + m)** Silencio **O(n)** Silencio Igual que Java – utiliza `deque` y `set` Silencio
Silencio **C++** Silencio **O(n + m)** Silencio **O(n)** Silencio Usos `vector asignadoint titulado `` + `unordered_set` + `queue`  durable

*`n` = número de métodos, `m` = número de invocaciones. *

-...

## Problema Restatement (Easy‐toread)

Usted tiene `n` métodos (`0 ... n‐1`).
`invocations[i] = [a, b]` means * method `a` calls method `b`*.

One method `k` is **buggy**.
Todos los métodos llamados por " k " , directa o indirectamente, son *sospechosos*.

Usted sólo puede eliminar el grupo sospechoso si ** ningún método no sospechoso llama cualquier método dentro del grupo**.
Si esa regla es violada, usted *debe* mantener todo el proyecto (retornar todos los métodos).

Devuelve una lista de los índices de método restantes (cualquier orden).
Si nada puede ser eliminado, devuelva `0 ... n‐1`.

-...

## Intuición - ¿Por qué un problema de Gráfico?

* La lista de invocación es un gráfico **directo**.
* “Cadena de llamada” → alcanzabilidad en el gráfico.
* “Llamador externo” → un borde entrante de un nodo no sospechoso en el conjunto sospechoso.

Así que el trabajo se reduce a:

1. **Encuentra el conjunto `S'** de todos los nodos alcanzable desde `k`.
2. **Ver** si cualquier nodo fuera `S` tiene un borde en `S`.
3. Si **no** tal borde → devolver `V \ S`.
De lo contrario → devolver todos los nodos.

-...

## Avanzado detallado (bueno, malo)

### Good – Clean & Linear

* **DFS / BFS** para descubrir `S`.
* Un segundo paso sobre todos los bordes para ver si existe algún borde externo.
* Dos lazos → en general **O(n + m)**.
* No hay riesgo de desbordamiento de pila recurrente en Java/Python/C++ porque utilizamos BFS iterativa (`queue`/`deque`).

## Bad – Dirección de borde equivocado

* Algunas implementaciones ingenuas verifican “por cada borde, si `a`  Iberia S y `b` ∉ S” y luego *guarda todo el gráfico* – eso es lo contrario de lo que necesitamos.
* Es un error **common**; usted debe buscar los bordes * entrantes* **a** el conjunto sospechoso, no los bordes salientes de él.

## Ugly - Redundant Work

* Running DFS from *every node* instead of just from `k`.
* Construir una matriz de adyacencia (`n × n`) – imposible para `n = 2·105`.
* La recuperación en idiomas con una pequeña pila (Python límite de recursión predeterminado ~1k) se estrellará en cadenas de llamadas profundas.

-...

## Algorithm (Step‐by‐Step)

1. ** Lista de adyacencias de edificios** g[a]` = todo `b` que `a` llama.
2. ** Collect suspicious set** `S` by BFS starting from `k`.
3. **Scan todos los bordes**:
* if `a` ∉ `S` **and** `b`  Precio `S` → * borde externo* → abortar → devolver todos los métodos.
4. Si no hay bordes externos → devolver todo `i` tal que `i ∉ S`.

-...

# Código #

■ Todos los códigos son ** comentaron cuidadosamente** y listos para pegar en LeetCode / su propio IDE.

### 1. Java

``java
importar java.util*;

*
* 3310. Remove Methods From Project
* Solución de estilo LeetCode (Solución de clase pública)
*/
Solución de la clase pública {}
public List Normativa de Integer]Method(int n, int k, int[][] invocations) {}
// 1. Construir la lista de adyacencia
Lista realizadaLista realizadaInteger título g = nuevo ArrayList recomendado();
para (int i = 0; i < n; i++) g.add(nuevo ArrayList recomendado()
(int[] e : invocations) g.get(e[0]).add(e[1]);

// 2. BFS de k para encontrar todos los nodos sospechosos
boolean[] suspicious = new boolean[n];
Búsquedas realizadasInteger título q = nuevo ArrayDeque corresponde();
q.add(k);
sospechoso[k] = verdadero;

(!q.isEmpty()) {
int u = q.poll();
para (int v : g.get(u)) {
si (!suspicious[v]) {}
sospechoso[v] = verdadero;
q.add(v);
}
}
}

// 3. Un paso para buscar calladores externos
para (int[] e : invocaciones) {}
int a = e[0], b = e[1];
si (!suspicious[a] " sospechosa[b]) {}
// Llamador externo encontrado → no puede eliminar nada
Lista realizadaInteger confiar all = nuevo ArrayList correctamente(n);
para (int i = 0; i)
devolver todo;
}
}

// 4. Regresar el complemento del conjunto sospechoso
Lista Nombramiento Nombrado = nuevo ArrayList implicado();
para (int i = 0; i)
(!suspicious[i]) remaining.add(i);
}
retorno restante;
}
}
`` `

### 2. Python 3

``python
de las colecciones importa
de la importación Lista

Solución de clase:
def restantes Métodos(
int, k: int, invocations: List[List[int]]
) List[int]:
1. Construir la lista de adyacencia
g = [[] for _ in range(n)]
para a, b en invocaciones:
g[a].append(b)

# 2. BFS para recoger todos los nodos alcanzables desde k
sospechosos
q = deque([k])
[k] = Verdadero
mientras q:
u = q.popleft()
for v in g[u]:
si no sospecha [v]:
sospechoso[v] = Verdadero
q.append(v)

# 3. Escanear todos los bordes para los calladores externos
para a, b en invocaciones:
si no sospecha [a] y sospecha[b]:
lista de retorno(range(n)) # no puede eliminar

4. Retorno de los métodos restantes
retorno [i para i en rango(n) si no sospecha [i]
`` `

### 3. C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector asignadoint título restanteMétodos(int n, int k, vector asignadovector fieltro pluripartido) {}
// 1. Construir la lista de adyacencia
vector realizador:
for (auto &e : invocations) g[e[0]].push_back(e[1]);

// 2. BFS de k
vector:
queue indicaint
q.push(k);
sospechoso[k] = verdadero;

(!q.empty()) {
int u = q.front(); q.pop();
para (int v : g [u]) si (!suspicious[v]) {}
sospechoso[v] = verdadero;
q.push(v);
}
}

// 3. Buscador externo
para (auto &e : invocaciones) {}
int a = e[0], b = e[1];
si (!suspicious[a] " sospechosa[b]) {}
// no puede eliminar
vector:
iota(all.begin(), all.end(), 0);
devolver todo;
}
}

// 4. Retorno de los métodos restantes
vector asignadoint título restante;
para (int i = 0; i)
si (!suspicious[i]) restante.push_back(i);
retorno restante;
}
};
`` `

-...

## Why This Solution is “Job‐Ready”

Ø Punto Silencio Por qué el Programador Love It Silencio
Silencio...
Silencio **Escaneo de iluminación** Silencio Muestras que puedes manejar datos grandes (`n`, `m` hasta 2 × 105). Silencio
Silencio **Pensaje gráfico** Silencio Muchos entrevistadores preguntan acerca de la posibilidad de alcanzar, orden topológico, detección de ciclos. Silencio
Silencio **Separación total de preocupaciones** Silencio Discovery of suspicious set vs. validity check – easy to unit‐test. Silencio
Silencio **Ninguna magia-número trucos** Silencio Usa contenedores de biblioteca estándar – mantenibles y portátiles. Silencio
Silencioso **Espacio-eficiente** memoria extra – buena para equipos integrados / con recursos. Silencio

■ Si usted puede explicar *por qué* usted elige BFS sobre DFS para el paso de la capacidad de acceso, los reclutadores sabrán que usted está consciente de los trade-offs de pila vs. cola.

-...

## SEO‐Friendly Meta‐ Datos

- **Título**: “3310 – Quitar Métodos Del Proyecto: Solución de Gráficos en Java, Python & C+”
- **Keywords**: LeetCode 3310, Remove Methods From Project, graph algoritmos, DFS, BFS, preparación de entrevistas, soluciones de entrevistas de codificación, entrevista de ingeniero de software, preguntas de codificación de entrevistas de trabajo.
- **Descripción**: "Descubre cómo resolver el problema de LeetCode 3310 – Eliminar los métodos del proyecto – en Java, Python y C++. Lea nuestra solución limpia y lineal, completa con código, explicaciones y ideas de entrevista. ”

-...

## Sample Test Harness (Comprobación rápida de la cordura)

``java
public static void main(String[] args) {
Solución sol = nueva solución ();
System.out.println(sol.remainingMethods(4, 1, new int[]{0,1},{1,2},{2,3}) [0]
System.out.println(sol.remainingMethods(3, 1, new int[]{0,1},{1,2}})); // [0,1,2]
}
`` `

``python
sol = Solución()
print(sol.remainingMethods(4,1,[0,1],[1,2],[2,3]]) # [0]
print(sol.remainingMethods(3,1,[0,1],[1,2]])
`` `

``cpp
Sol de solución;
auto r = sol.remainingMethods(4,1,{0,1},{1,2},{2,3});
para (incluido x: r) cout obtenidos se hizo "
`` `

-...

## Pitfalls comunes para evitar

TEN TERRITOR ANTERIOR ANTERIOR ANTERIOR
Silencio...
Silencio Usando **DFS de cada nodo** en lugar de simplemente de `k` peru Construir el conjunto alcanzable una vez - es O(n + m) no O(n × m). Silencio
Silencio Comprobando *outgoing* bordes de nodos sospechosos en lugar de *incoming* edges tención Recuerde que debemos prohibir *llamadores externos* → escanear para bordes `a ∉ S, b  Iberia S`. Silencio
Ø Errores de profundidad de Recursión en Python / Java TEN Preferir iterative BFS/DFS o aumentar el límite de recursión. Silencio
Silencio Regresar `S` en lugar del complemento Silencio El problema pide *mantener* métodos. Silencio

-...

## Closing Thoughts

- Los algoritmos de Gráficos son el pan-y-butter de la mayoría de las entrevistas de codificación.
- Una solución limpia de dos pasos (reachability + edge-validation) demuestra **problema descomposición** y ** eficiencia algorítmica**.
- Mediante la implementación de la misma lógica en **Java, Python & C+**, se muestra que se pueden traducir ideas de alto nivel a través de los ecosistemas – una habilidad altamente valorada en una pila de multilingüe.

¡Feliz codificación, y buena suerte aterrizando esa entrevista de ingeniería de software! 🚀