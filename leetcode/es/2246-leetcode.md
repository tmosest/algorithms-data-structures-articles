-...
Título: LeetCode 2246. Sendero más largo con diferentes caracteres adyacentes -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 2246 – Camino más largo con diferentes caracteres adyacentes
*(LeetCode Hard)*

■ ** Objetivo** – En un árbol arraigado donde cada nodo tiene una letra minúscula, encontrar la longitud máxima de un camino simple tal que **no dos nodos adyacentes comparten el mismo carácter**.
■ **Introducción**: `int[] parent` (size `n`) y `String s` (length `n`).
■ ** Salida** – Longitud del camino más largo válido (1-basado).

A continuación encontrará una solución completa, lista para pasar en **Java, Python, y C+** (todo el tiempo O(n) / O(n) espacio).
Después de eso, lea el blog adjunto que explica la intuición, las trampas y cómo esta solución brilla en una entrevista de codificación.

-...

## 📌 Code

## Java

``java
importar java.util*;

Clase Solución {
int privado mejor; // longitud máxima global

int longestPath(int[] parent, String s) {
int n = parent.length;
Lista de datos niños = nuevo ArrayList[n];
para (int i = 0; i < n; i++) niños[i] = nuevo ArrayList fiel();

para (int i = 1; i < n; i++) { // construir lista de adyacencia
niños[i].add(i);
}

mejor = 1; // al menos un nodo
dfs(0, children, s);
devolver mejor;
}

/** devuelve la cadena más larga a partir del nodo 'v' que satisface la regla */
int privado dfs(int v, List Garantizado[] niños, String s) {
int first = 0, second = 0; // top dos longitudes entre los niños

para (int u : niños[v]) {}
int len = dfs(u, children, s); // cadena más larga de niño u
si (s.charAt(u) == s.charAt(v)) continúa; // no puede utilizar este niño

si (Lleno primero) {
segundo = primero;
primero = lino;
} si (len не segundo) {
segundo = lino;
}
}

mejor = Math.max(mejor, primero + segundo + 1); // camino pasa por v
volver primero + 1; // cadena más larga hacia arriba
}
}
`` `

-...

## Python 3

``python
de la importación Lista
de las colecciones importadas por defecto
importación heapq

Solución de clase:
def longestPath(self, parent: List[int], s: str) - Propiedad int:
n = len(parente)
niños = [[] for _ in range(n)]
para i en rango(1, n):
niños[i].append(i)

auto.best = 1

def dfs(v: int) - título int:
top_two = [0, 0] # mayores dos longitudes de niños

para u en niños[v]:
cur = dfs(u)
si s[u] == s[v]:
continuar
# Mantenga los dos valores más grandes
si cur > top_two[0]:
top_two[1] = top_two[0]
top_two[0] = curtido
elif cur > top_two[1]:
top_two[1] = curtido

auto.best = max(self.best, top_two[0] + top_two[1] + 1)
volver top_two[0] + 1

dfs(0)
Vuélvete. lo mejor
`` `

-...

### C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int longestPath(vector fieltro, cadena s) {
int n = parent.size();
vector asignado a los niños(n);
para (int i = 1; i)

mejor = 1;
dfs(0, children, s);
devolver mejor;
}

privado:
int best;

int dfs(int v, vector identificadovector niños, const cordón
int first = 0, second = 0; // top dos longitudes entre los niños

para (int u : niños[v]) {}
int len = dfs(u, children, s);
si (s[u] == s[v]) continúan;

si (Lleno primero) {
segundo = primero;
primero = lino;
} si (len не segundo) {
segundo = lino;
}
}

mejor = max(best, first + second + 1);
retorno primero + 1;
}
};
`` `

-...

## 📚 Blog Post – *The Good, The Bad, and The Ugly of DFS on Trees*

■ **Keywords**: LeetCode 2246, Sendero más largo con diferentes caracteres adyacentes, DFS, árbol DP, codificación de entrevistas, diseño de algoritmos, casos de borde.

### 1. Introducción

Cuando un reclutador le da la mano **LeetCode 2246 – “Pase más largo con diferentes caracteres adyacentes”**, usted está mirando un árbol clásico‐ Problema del DP. El desafío no es sólo encontrar el camino más largo; es hacerlo mientras obedece una regla de compatibilidad con carácter.
Una búsqueda clara y recurrente de profundidad (DFS) que rastrea las dos mejores cadenas de cada niño es la solución más elegante y fácil de entrevistar.

-...

### 2. Reposición de problemas

Dado un árbol arraigado con `n` nodos (`0 ≤ n ≤ 105`), donde cada nodo `i` tiene una letra `s[i]`, computar la longitud del camino más largo (no se repite el nodo) tal que ** cada par de nodos consecutivos en el camino tiene diferentes letras**.
Porque `n` es grande, necesitamos un algoritmo **O(n)**.

-...

### 3. La intuición – ¿Por qué dos cadenas?

Piense en un camino que pasa por un nodo 'v' y ramas en dos sub-árboles diferentes.
Si ya conocemos la cadena *longest* a partir de cada niño que termina en ese niño, podemos

1. **Utilice al niño sólo si su carta difiere de `v`.**
2. Mantén las dos cadenas usables más largas. #
3. **Añadir 1 para el nodo 'v' mismo** para conseguir un camino candidato.

La respuesta mundial es el máximo de todos esos candidatos. Esta es una computación *post-order*: los niños son procesados antes de su padre.

-...

### 3. Por qué DFS + “top-two” es la Buena elección

Reason ← Detalle de la vida
Silencio...
TEN **Simplicity** TENENCIA Una función recursiva, ninguna estructura de datos elegante. Silencio
Silencio **Predictable Runtime** Silencio Cada nodo visitó una vez → **O(n)**. Silencio
Silencio **Memory Friendly** Silencio Lista de Adjacency + pila de recursión → **O(n)** peor maletín. Silencio
Silencio **Entreview‐Ready** Silencio Explica la transición del estado claramente, fácil de depurar en el lugar. Silencio
tención **Scalability** Silencio Maneja los máximos nodos `105` cómodamente. Silencio

La clave es que un camino válido **nunca revisita un nodo**, por lo que sólo necesitamos considerar *child → parent → otro niño* patrones. Rastrear dos cadenas máximas basta porque un camino puede tener en la mayoría de dos ramas en un nodo.

-...

### 3. El mal – Pitfalls comunes

1. *Ignorar la condición de la raíz*
Algunas implementaciones olvidan que la raíz podría ser una hoja y volver 0 en lugar de 1. Siempre inicialice lo mejor global a 1 (un único camino de nodo).

2. **Mixing Up “Length of Path” vs “Number of Nodes”* *
En DFS, el valor de retorno representa el más largo *cadena* que puede ampliarse hacia arriba. Recuerde añadir 1 para el nodo actual al regresar.

3. **O(n2) Error con Naïve Pairing* *
Parecer a cada niño con cada otro niño (`O(k2)` por nodo) rápidamente sopla en un árbol en forma de estrella. El truco “mantener dos más grandes” mantiene la complejidad lineal.

4. **Desbordamiento de la tensión en la recuperación**
Con 'n = 105', la recursión profunda puede alcanzar el límite de la pila en algunos idiomas. En Java o C+ puede necesitar elevar el límite de recursión o utilizar un apilador iter. Python 3 soluciones generalmente pasan porque el límite de recursión predeterminado de CPython es mayor; de lo contrario, use `sys.setrecursionlimit`.

-...

### 4. Los casos Ugly - Edge que rompe su código

← Caso Edge Silencioso Lo que pasa si lo extrañas Es permanente
Silencio------------------------------------...
Silencio **Todas las Nodes Mismo Carta** Silencio La longitud del camino es siempre 1. Si olvida actualizar `mejor = 1` al principio, puede volver 0. Silencio Inicializar `mejor = 1`. Silencio
Silencio **Large Star Tree** Silencio O(n2) si parejas a niños ingenuamente. Mantenga sólo las dos cadenas utilizables más grandes. Silencio
Silencio **Single Node Tree** tención Algunos códigos recursivos pueden devolver 0 para nodos de hoja. TENIDO Vuelta 1 para una hoja (una cadena de longitud 1). Silencio
Silencio ** Lista de niños empleados** Silenciosos `niños[v]` podrían estar vacíos; el bucle debe manejarlo con gracia. Use una lista vacía, no es necesario un caso especial. Silencio
Silencio **Non‐Rooted Input** Silencio LeetCode garantiza `parent[0] == 0`. Si usted asume incorrectamente un árbol no dirigido, usted cuenta doble. tención Construya una lista de adyacencia dirigida desde la raíz a los niños. Silencio

-...

### 5. Paso a paso

Caminemos a través de un pequeño ejemplo:

`` `
padres = [0, 0, 1, 2, 2]
s = "abacbd"
`` `

1. Construir la lista de adyacency:
`0 → {1, 2}`
`1 → {3, 4}`
2 → {5}`

2. DFS(0):
* niño 1 devuelve cadena `2` (b → a → c)
* niño 2 devuelve la cadena `1` c) pero `s[2]==s[0]`? No → utilizable.
* `first=2`, `second=1` → best candidate `2+1+1 = 4`.

3. La recursión devuelve `primero+1 = 3` al nodo 0.
4. Global `best = 4`. Camino: `b → a → c → d`.

Todas las operaciones son `O(1)` por niño; en general `O(n)`.

-...

### 6. Análisis de la complejidad

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
TEN Java TENIDO **O(n)** Silencio **O(n)** (lista de adyacencia + pila de recursión)
TENIDO Python TENIDO **O(n)** ANTERIOR **O(n)**
TENIDO C++ TENIDO **O(n)** Silencio **O(n)**

El único factor de constante extra es el costo de comparar caracteres y actualizar dos máximos – insignificante.

-...

### 7. Variaciones " Extensiones

Silencioso Variación Silencioso Cómo Adaptarse
Silencio--------------
Silencio **Multiple Allowed Letters** Silencio En lugar de un solo personaje, mantén un poco de letras permitidas. Silencio
Silencio **Edanzas ponderadas** Silencio Regresar el peso de la cadena en lugar de contar los nodos. Silencio
Silencio ** Árbol Desarraigado** TENIDO Rotar el árbol arbitrariamente (por ejemplo, nodo 0) – el algoritmo es agnóstico a la raíz porque la regla sólo se refiere a los nodos adyacentes. Silencio

-...

### 8. Estrategia de examen

Silencio Test confidencialidad Descripción
Silencio...
Silencio `n=1` Silencio Nodo único → respuesta = 1. 
Silencio Todas las mismas letras Silencio Respuesta = 1. Silencio
Silencio Cartas supletorias (por ejemplo, “ababa”)
Silencio Árbol de estrellas con un niño diferente Respuesta = 2.
tención Árbol grande aleatorio (105 nodos) Silencio Verificar que el tiempo de ejecución se queda ANTE 1 s. Silencio

Utilice las pruebas de unidad LeetCode, además de sus propios generadores aleatorios para probar el estrés.

-...

### 9. Conclusión

LeetCode 2246 es un problema **pure‐DFS árbol DP** que recompensa el pensamiento claro y una solución mínima y lineal.
El patrón de “mantener las dos cadenas superiores” es un patrón reutilizable para muchas preguntas de entrevista sobre los caminos más largos, subsecuencias crecientes más largas en los árboles, o problemas de conjunto máximo independiente.

■ *Takeaway*: Siempre **Piensa en el fondo**. Al resumir la contribución de cada niño en un pequeño par de números enteros, puede resolver todo el problema en un solo paso.

-...

#### 10. Pensamiento final

Si se está preparando para una entrevista técnica, practique este patrón exacto hasta que pueda escribirlo sin mirar una referencia. La maestría del DFS en los árboles abre la puerta a muchos problemas duros de LeetCode e impresiona a los gerentes de contratación que valoran algoritmos limpios y eficientes.

-...

¡Feliz codificación! 🚀