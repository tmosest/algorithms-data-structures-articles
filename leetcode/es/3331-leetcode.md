-...
Título: LeetCode 3331. Encontrar tamaños de subtree después de los cambios -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📚 3331. Encontrar tamaños de subárbol después de los cambios – Código completo (Java / Python / C++) + SEO‐Optimized Blog Post

-...

#### TL;DR
- **Problema** – Aparenta cada nodo al antepasado más cercano con el mismo carácter y devuelve el tamaño de cada subárbol en el nuevo árbol.
- Solución** - Dos primeros traversales de profundidad.
1. **DFS1** – Mientras camina el árbol original mantiene el índice *último visto* para cada personaje. Si existe un índice anterior, ese nodo se convierte en el nuevo padre.
2. **DFS2** – Construir una nueva lista de adyacencia con los padres actualizados y contar tamaños de subárbol en un DFS post-orden más.
- Complejidad** - tiempo, espacio.
- **Idiomas** – Java, Python, C++ – lista para copiar-paste en tu IDE o LeetCode.

-...

## 1. El Código

■ ** Profundidad de recuperación** – La entrada puede contener hasta nodos \(10^5\).
■ En Java / C+ la pila predeterminada generalmente maneja esto, pero en Python necesita parar el límite de recursión (o utilizar un DFS iterativo).

#### 1.1 Java

``java
importar java.util*;

Clase Solución {
int[] encontrarSubtreeSizes(int[] parent, String s) {
int n = parent.length;
Lista de datos niños = nuevo ArrayList[n];
para (int i = 0; i < n; i++) niños[i] = nuevo ArrayList fiel();

// Construir la lista original de adjacency
para (int i = 1; i) no; i++) niños [parente [i].add(i);

int[] newParent = parent.clone(); // mantendrá a los padres actualizados
int[] lastSeen = nuevo int[26];
Arrays.fill(lastSeen, -1);

// DFS1 - encontrar nuevos padres
dfsParent(0, s.toCharArray(), children, lastSeen, newParent);

// Construir nueva lista de adjacency de nuevoParent
Lista de datos nuevos niños = nuevo ArrayList[n];
para (int i = 0; i < n; i++) newChildren[i] = nuevo ArrayList fiel();
para (int i = 1; i) no; i++) nuevos niños[newParent[i].add(i);

int[] response = new int[n];
dfsSize(0, newChildren, answer);
respuesta de retorno;
}

vacío privado dfsParent(int node, char[] chars, List madeInteger confianza[] niños,
int[] lastSeen, int[] newParent) {
int idx = chars [node] - 'a';
int prev = lastSeen[idx];
si (prev != -1) nuevoParent[nodo] = prev; // nuevo padre encontrado

últimoSeen[idx] = nodo; // corriente de empuje
para (incluido niño : niños [nodo]) {}
dfsParent(child, chars, children, lastSeen, newParent);
}
lastSeen[idx] = prev; // pop / restore
}

int privado dfsSize(int node, List Garantizado[] niños, int[] ans) {
int sz = 1;
para (incluido niño : niños [nodo]) {}
sz += dfsSize(hijo, niños, ans);
}
ans[nodo] = sz;
devolver sz;
}
}
`` `

-...

### 1.2 Python

``python
importadores
sys.setrecursionlimit(200000) # requerido para árboles profundos

Solución de clase:
def findSubtreeSizes(self, parent: list[int], s: str) - ratio[int]:
n = len(parente)
niños = [[] for _ in range(n)]
para i en rango(1, n):
niños[i].append(i)

new_parent = parent[:] # copy of original parents
[-1] * 26

def dfs_parent(u: int):
idx = ord(s[u]) - ord('a')
prev = last_seen[idx]
si prev != -1:
new_parent[u] = prev
last_seen[idx] = u
por v en niños[u]:
dfs_parent(v)
last_seen[idx] = prev

dfs_parent(0)

# Build new adjacency
new_children = [[] for _ in range(n)]
para i en rango(1, n):
new_children[new_parent[i].append(i)

respuesta = [0]

def dfs_size(u: int) - título int:
sz = 1
for v in new_children[u]:
sz += dfs_size(v)
respuesta[u] = sz
Regreso sz

dfs_size(0)
respuesta
`` `

-...

#### 1.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector implicado encontrarSubtreeSizes(vector realizadointющ parent, string s) {
int n = parent.size();
vector asignado a los niños(n);
para (int i = 1; i)

vector nuevoParent = padre; // copiar
vector contratado(26, -1);

función recomendadavoid(int) = dfsParent = [ cl](int u) {
int idx = s[u] - 'a';
int prev = lastSeen[idx];
si (prev != -1) nuevoParent[u] = prev;
lastSeen[idx] = u;
dfsParent(v);
últimoSeen[idx] = prev; // restaurar
};
dfsParent(0);

// Construya nueva lista de adjacency
vector realizador implicado nuevoNiños(n);
para (int i = 1; i) no; ++i) nuevos niños[newParent[i].push_back(i);

vector(n)

función seleccionadaint(int)? dfsSize = [ cl](int u) int {
int sz = 1;
for (int v : newChildren[u]) sz += dfsSize(v);
respuesta[u] = sz;
devolver sz;
};
dfsSize(0);
respuesta de retorno;
}
};
`` `

-...

## 2. The Blog Post – *Haga que su entrevista Resultado Explote! *

■ *Este post está escrito para los candidatos que quieren dominar los problemas de árboles de LeetCode, clavar su próxima entrevista, y conseguir un trabajo en una empresa de tecnología superior. *
■ Utilice el epígrafe “**Encontrar tamaños de subárbol después de los cambios**” y la palabra clave “LeetCode 3331” en su buscador de la visibilidad instantánea.

-...

#### 2.1 Title
■ **“LeetCode 3331 – Encontrar tamaños de subtree después de los cambios: Master the DFS Tree Problem”* *

### 2.2 Meta‐Descripción (SEO)
■ **“Aprenda a resolver LeetCode 3331 – Encontrar tamaños de subárbol después de los cambios – con soluciones Java, Python y C+++, más una explicación detallada de DFS, reparente de árboles y cálculo de tamaño.”* *

#### 2.3 Artículo completo

■ **Keywords**: LeetCode 3331, encontrar tamaños de subárbol después de cambios, problemas de árbol, DFS, matriz de padres, Java, Python, C+++, entrevista de codificación, diseño de algoritmos, estructuras de datos, entrevista de trabajo, entrevista de ingeniería de software, preguntas de entrevista, desafío de codificación.

-...

## 📄 3331 – ¿Qué pregunta el problema en realidad?

Se le da un árbol arraigado como una matriz de padres** `parent[i]` (root tiene `-1') y una cadena `s` donde `s[i]` es el carácter del nodo `i`.
Para cada nodo `x` (excepto la raíz) debe **re-parent** al antepasado **más cercano** que tiene el mismo carácter.
Después de que todos los nodos se hayan movido, devuelves un array 'ans' donde `ans[i]` iguala el número de nodos en el subárbol arraigado en el nodo `i` ** en el nuevo árbol**.

-...

### 🔍 Observaciones clave

1. **La estructura del árbol es conocida por un array padre. #
Convertirlo en una lista de adyacencia ( " hijos " ) es trivial: por cada " i " , añadir " i " a " hijos[i] " .

2. **Encontrar el antepasado “más cercano” con el mismo personaje es un clásico truco DFS. #
Mientras exploras el árbol que guardas, para cada personaje, el nodo *último* que has visitado (`últimoSeen`).
Cuando llegues a un nodo `u`, si `último visto[char] != -1` significa que hay un ancestro *previoso* con el mismo char, y *porque estamos haciendo un paseo por la profundidad*, que el índice anterior es automáticamente el más cercano.

3. **Después de actualizar a todos los padres se puede tratar el nuevo árbol como cualquier otro árbol. #
Construya una nueva lista de adyacency ( " newChildren " ) de la matriz actualizada de `newParent ' y realice un DFS post-orden para contar tamaños de subtree.

-...

### 📐 The Two‐DFS Algorithm

Silencio ¿Por qué funciona?
...------------------------------
Silencio **DFS1** Silencioso `dfsParent(node)` ' יbr confianza *Maintain* `lastSeen[26]` (index of most recent node for each character). *Si* existe un índice anterior, establece `nuevoParent[node] = lastSeen[char]`. ¦ La naturaleza apilada de DFS garantiza que `la últimaSeen[char]` es el antepasado más cercano con ese personaje. Silencio
Silencio ** Árbol de la construcción** Silencio Para cada niño `i не 0`, insértese `i ' en `niños[newParent[i]. Silencio nos da una lista de adyacencia adecuada para las nuevas relaciones entre padres. Silencio
Silencio **DFS2** Silencioso `dfsSize(node)` – DFS post-orden que devuelve el tamaño de subtree. Silencio Classic post-order trick: size of node = 1 + suma de tamaños de sus hijos. Silencio

-...

Por qué Esto es eficiente

TEN TERMIN TEN ANTE SON TEN ANTE
Silencio...
tención **Tiempo** Silencio Cada nodo es visitado dos veces – una vez en DFS1 y una vez en DFS2. \(O(n)\). Silencio
Silencio **Espacio** Silencioso listas de Adjacency, matriz de padres, `últimoSeen`, y `ans` - all \(O(n)\). Silencio
Silencio **Constantes** Silencio El algoritmo sólo necesita un entero único por personaje (“últimoSeen[26]”. No hay estructuras de datos pesadas. Silencio

-...

## 3. Cómo utilizar esto en una entrevista

Cómo la respuesta ayuda a vivir
Silencio...
Silencio “Explicar su solución en 2 min.” Silencio **DFS + pila de último visto** – dos pases, datos auxiliares de tamaño constante. Silencio
Silencio “¿Cuál es el peor momento?” Silencio **Linear** – incluso para una cadena degenerada de nodos \(10^5\). Silencio
Silencio ¿Podrías escribir esto en Python? tención Proporcionar el código Python arriba y mencionar el límite de recursión. Silencio
Silencio “¿Qué hay de DFS iterante?” Silencio Usted puede reemplazar la recursión con una pila explícita si lo prefiere. Silencio

-...

## 4. Lista de verificación de inicio rápido

1. **Copiar** el bloque de idiomas que coincide con su entorno.
2. **Paste** en el editor de LeetCode o tu IDE local.
3. **Run** en las pruebas de la muestra.
4. **Añada** sus propios casos personalizados (cadenas profundas, árboles equilibrados, caracteres todos iguales, caracteres diferentes).
5. **Enviar** – ¡Te aceptarán en la primera vez!

-...

## 5. SEO‐Optimized Blog Wrap‐ Arriba

■ **Título:** *LeetCode 3331 – Encontrar tamaños de subárbol después de los cambios: DFS Tree Re‐Parenting en Java, Python & C++ *
■ **Meta‐Description:** *Master LeetCode 3331 (Encontrar tamaños de subárbol después de los cambios) con soluciones completas Java, Python y C++, una explicación paso a paso del DFS, y las ideas de entrevista. *

### 📌 Why Reading This Helps You Land a Job

La mayoría de las entrevistas prueban el traversal de árboles. Este problema demuestra cómo mantener el estado (`últimoSeen`) mientras camina un árbol.
- **Parent‐Array to Adjacency** – Convertir entre representaciones es un truco común de entrevista.
- **Análisis de Complejidad Azul** – Demostrar el espacio/tiempo \(O(n)\) muestra que puede razonar sobre asintotica en la mosca.
- ** Flexibilidad lingüística** – Conocer el mismo algoritmo en tres idiomas señales a entrevistadores que usted entiende *concepto* sobre *sintaxis*.

-...

#### 🎯 Takeaway

Si alguna vez has mirado el array de padres, no te sientes seguro de cómo atravesar el árbol, o preocupado por los límites de la recursión, el código anterior y la explicación te dan un **bullet-proof blueprint**.

Úsalo, pruébalo y explícalo en tu próxima entrevista. Usted demostrará:

Pensamiento algorítmico** – dos pases, memoria extra mínima.
- **Disciplina de codificación** – separación limpia de preocupaciones (actualización de los padres vs. cálculo del tamaño).
- ** Fluencia lingüística** – Java, Python y C++ muestran adaptabilidad.

¡Feliz codificación, y buena suerte aterrizando ese trabajo de sueño! 🚀