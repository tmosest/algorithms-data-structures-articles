-...
Título: LeetCode 2673. Hacer costos de caminos iguales en un árbol binario -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Hacer costos de caminos iguales en un árbol binario – 2673 (LeetCode)

■ **Título:** Hacer los costos de los caminos iguales en un árbol binario – Java/Python/C++ Soluciones
■ **Descripción de los datos** Solve LeetCode 2673 “Hacer costes de caminos iguales en un árbol binario” en tiempo O(n). Lea nuestro tutorial DFS de fondo, los fragmentos de código para Java, Python & C+++, además de un análisis “bueno-bad-ugly” para la preparación de entrevistas.

-...

## 1. Declaración de problemas

Se le da un árbol binario perfecto con n ' n ' nodos (1-basado indexación).
La raíz es nodo `1`, y para cualquier nodo `i` el niño izquierdo es `2*i` y el niño derecho es `2*i+1`.

"cost[i] " (recurso basado en 0) tiene el costo del nodo " i+1 " .
Usted puede **incremento** el costo de cualquier nodo por `1` cualquier número de veces.
** Objetivo:** Haga que el costo total de cada camino de raíz a hoja sea igual al número mínimo de incrementos.

Devuelve ese número mínimo de incrementos.

■ *Examples*
[1,5,2,3,1]` → **6**
[5,3,3]` → **0**

■ **Constraints**
* `3 ≤ n ≤ 10^5`
* `n + 1` es un poder de 2 (árbol binario perfecto)
≤ 10^4`

-...

## 2. Intuición

Un árbol binario perfecto es *ordenado nivel*.
Si miramos cualquier nodo interno, sus dos hijos eventualmente conducen a dos caminos de hoja.
Deja:

`` `
izquierda Costo – coste total mínimo del niño izquierdo a cualquier hoja
derecho Costo – coste total mínimo del niño derecho a cualquier hoja
`` `

Para hacer los dos caminos iguales, debemos elevar el subárbol más barato para que coincida con el caro.
El costo de hacer esto es `abs(leftCost - rightCost)`.

Después de alinear a los niños, el costo mínimo del nodo actual se convierte en:
`` `
cost[nodo] + max(leftCost, rightCost)
`` `
porque elegimos al niño más pesado como base para el siguiente nivel.

Así el problema puede ser resuelto *bottom‐up* o *recursivamente* por DFS.
Ambos enfoques tienen tiempo **O(n)** y **O(1)** espacio auxiliar (ignorando la pila de recursión).

-...

## 3. Solución iterativa adicional (C+++, Java, Python)

### 3.1 Algorithm

1. Iterate desde el último nodo interno (`n/2 - 1`) hasta la raíz (`0`).
2. For node `i ' (0‐based index):
* `l = 2*i + 1` (índice inferior del niño)
* `r = 2*i + 2` (índice derecho del niño)
* `incrementos += tencióncost[l] - cost[r] `
* `cost[i] += max(cost[l], cost[r])` // update to minimal path cost from node ` i `
3. Regresen 'incrementos'.

#### 3.2 Complexity

Silencio Silencio Silencio Silencio
Silencio----------------
Silencioso sobre los nodos internos
* * * * * * * * * * * * * * * *(log n)** (a la altura del árbol) * *

### 3.3 Code Snippets

##### Java

``java
Clase Solución {
int public int minIncrementos(int n, int[] cost) {
largo res = 0; // utilizar largo para evitar el desbordamiento de grandes n
para (int i = n / 2 - 1; i 0; i--) {
int l = 2 * i + 1;
int r = 2 * i + 2;
res += Math.abs(cost[l] - cost[r]);
cost[i] += Math.max(cost[l], cost[r]); // propagar coste mínimo hacia arriba
}
retorno (int) res;
}
}
`` `

#### Python 3

``python
Solución de clase:
def minIncrementos(self, n: int, cost: List[int] int:
res = 0
para i en rango(n // 2 - 1, -1, -1):
l = 2 * i + 1
r = 2 * i + 2
res += abs(cost[l] - cost[r])
costo[i] += max(cost[l], costo[r]) # actualización al coste mínimo de la ruta
retorno
`` `

###### C++

``cpp
Clase Solución {
public:
int minIncrementos(int n, vector asignadoint
largo res = 0; // largo tiempo para evitar el desbordamiento
para (int i = n / 2 - 1; i 0; --i) {
int l = 2 * i + 1;
int r = 2 * i + 2;
res += abs(cost[l] - cost[r]);
cost[i] += max(cost[l], cost[r]); // propagar hacia arriba
}
volver estática_cast seleccionado(res)
}
};
`` `

-...

## 4. Variante DFS Recursiva

Si prefieres una aplicación recursiva * limpia*, la lógica permanece igual; la única diferencia es que computamos los costos de los niños sobre la marcha.

##### Java

``java
Clase Solución {
reses privados largos = 0;

int public int minIncrementos(int n, int[] cost) {
dfs(0, costo);
retorno (int) res;
}

int privado dfs(int i, int[] cost) {
si (i >= cost.length) retorno 0; // hoja
int left = dfs(2 * i + 1, cost);
int right = dfs(2 * i + 2, cost);
res += Math.abs(left - right);
costo de devolución[i] + Math.max(izquierda, derecha);
}
}
`` `

#### Python

``python
Solución de clase:
def minIncrementos(self, n: int, cost: List[int] int:
autos = 0
def dfs(i):
si >= len(cost): retorno 0
l, r = dfs(2 * i + 1), dfs(2 * i + 2)
auto.res += abs(l - r)
costo de devolución[i] + max(l, r)
dfs(0)
Vuélvete. res
`` `

###### C++

``cpp
Clase Solución {
public:
ans largos = 0;
int dfs(int i, vector identificadoint
si (i >= cost.size()) retorno 0;
int left = dfs(2 * i + 1, cost);
int right = dfs(2 * i + 2, cost);
ans += abs(left - right);
costo de devolución[i] + máx(izquierda, derecha);
}

int minIncrementos(int n, vector asignadoint
dfs(0, costo);
volver estática_cast seleccionado(ans)
}
};
`` `

-...

## 5. “Bueno – malo – ugly” Entrevista Análisis

← Fase actual Lo que usted debe mostrar a la vida Lo que puede ir mal ¿Cómo evitarlo
Silencio------------------------------
tención **Bueno** Silencio • Tiempo lineal (O(n)) algoritmo. Incrementos mínimos derivados de la alineación de subárboles. Bottom‐up o DFS ambos simples de código.
Silencio **Bad** Silencio • malinterpretar el árbol como * no-perfecto* lleva a errores de índice.• Usar `int` para la respuesta puede desbordarse cuando `n` ♥ 105. Silencio • Utilizar siempre entero de 64 bits (`long`/`long long'). Validar que existen índices de niños ( < l, r < n > )
Silencio **Ugly** Silencio • Tratando de ejecutar brute‐force todos los patrones posibles de aumento (exponencial). Recursively recomputing child costs from scratch at every node (O(n log n) if you don't cache). Silencio • Nunca revisit a node’s cost; propagarlo una vez.

### ¿Por qué el patrón de subida es una estrella en entrevistas

1. **Claridad** – El algoritmo lee como un simple bucle; los entrevistadores pueden ver la lógica inmediatamente.
2. **Proof-of-Correctness** – El invariante costo[i] almacena el mínimo costo de la ruta del nodo `i` a cualquier hoja ” se mantiene en cada iteración.
3. **Memoria** – Las actualizaciones en el lugar evitan los arrays adicionales; si se utiliza la recursión, la profundidad de la pila es sólo 'log n` para un árbol binario perfecto.
4. **Extensibilidad** – El mismo patrón funciona para la variante de seguimiento donde se puede *decremento* también, simplemente reemplazando `abs` por `max(0, leftCost - rightCost)`.

-...

## 6. Lista de verificación Edge‐Case

Silencio Caso Edge Silencio Por qué importa
Silencio...
Silencio `n` es sólo el mínimo (3) Silencio Sólo un nodo interno (root) Silencioso Loop lo maneja correctamente (`n/2 - 1 == 0`). Silencio
Silencio Todos los costos ya iguales Silenciosos estancias No se necesita ningún caso especial. Silencio
Silencio Muy grande `n` (Ω105) Silencio Potential 32‐bit overflow tención Use 64-bit (`long`/`long `) for `res`. Silencio

-...

## 7. Variante: aumento **o Decremento*

Si la declaración del problema se cambió para permitir tanto incrementos como decrementos, la estrategia óptima cambia ligeramente:

* Levantaríamos el subárbol más barato **hasta** el más pesado, *y* podríamos opcionalmente bajar el más pesado si eso conduce a un menor número de incrementos totales.
* Esto reduce a ** haciendo ambos subárboles iguales al máximo de sus costos mínimos de ruta**, lo que produce el mismo costo de `abs(leftCost - rightCost)`.
* El resto de la lógica permanece igual; sólo la interpretación de la operación cambia.

-...

## 8. Tomado para su próxima entrevista de codificación

* **LeetCode 2673** es un problema del árbol de la clase media que prueba:
1. Traversal de árboles (DFS o fondo).
2. Trabajando con montones implícitos/representaciones de los árboles.
3. Pensando en términos de *subproblemas invariantes* y *propagación*.

* Dominar este patrón demuestra:
* **Clean, código libre de errores** (la lógica básica de 3 líneas).
* **Uso eficiente del espacio** (actualizaciones en el lugar).
* ** Razonamiento matemático** (alineación de costos, diferencias absolutas).

* **Use it in your interview prep**:
* Escribe la versión iterativa primero – es fácil de explicar.
* Mención la versión recursiva – los entrevistadores les encanta ver perspectivas iterativas y recursivas.
* Destacar el tiempo O(n) " espacio auxiliar O(1) para impresionar la eficiencia.

-...

## 9. Repositorio completo del código

Las tres implementaciones lingüísticas están disponibles en este GitHub repo:

``text
https://github.com/tu-username/leetcode-2673-cost-path
`` `

Siéntete libre de copiar, adaptar y añadir pruebas de unidad.

-...

## 10. Clausura

Resolver **LeetCode 2673** con un DFS de fondo no sólo le gana una puntuación perfecta en la plataforma, sino que también muestra su capacidad de:

* Traducir un problema en un invariante limpio.
* Optimize for both time and space.
* Escriba código conciso, listo para la producción en Java, Python o C++.

Añada este problema a su lista de reproducción de preguntas, y estará bien preparado para cualquier ronda de instrucciones de datos que implique ** árboles binarios** y **ajuste de costos** lógica.

Buena suerte, y feliz codificación!