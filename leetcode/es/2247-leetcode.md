-...
Título: LeetCode 2247. Precio máximo de viaje con autopistas K -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🏆 Precio máximo del viaje con las autopistas K - El bueno, el malo, y el Ugly
**LeetCode 2247 – Hard* *

■ **Keywords**: LeetCode 2247, Maximum Cost of Trip, K Highways, dynamic programming, bitmask DP, DFS+memo, Java, Python, C++, problema de entrevista, algoritmos gráficos

-...

Problema Recap

Se le da un gráfico de peso no dirigido con `n` ciudades (`0 ... n‐1`) y una lista de `altades`.
Cada carretera es `[u, v, w]` – una carretera bidireccional que cuesta `w` para conducir.

Quieres hacer un viaje que

* **Exactamente utiliza `k` autopistas** (es decir, cruces `k` edges),
* **Nunca visita una ciudad dos veces* (el camino debe ser simple),
* puede empezar desde cualquier ciudad.

Devuelve el *máximo total de peaje* puedes pagar en tal viaje, o `-1` si es imposible.

`` `
n ≤ 15
Ø Ø 50
k ≤ 50
`` `

Las limitaciones le dan una pista: `n` es pequeña, por lo que un **bitmask** es un ajuste perfecto.

-...

## 2down El Bien - ¿Por qué funciona un Bitmask DP

* Representación del Estado* *
* `mask` – a 15-bit integer where bit `i` is `1` if city `i` has already been visited.
* `última' - la ciudad donde termina el camino actual.

`dp[mask][last]` = coste máximo de un camino simple que visita exactamente las ciudades en `mask` y termina en `último `.

* **Initialización* *
Cada ciudad puede ser un punto de partida.
" dp[1 " se hizo i] [i] = 0 " para todos " .

* Traición*
De un estado `(mask, last)` podemos ir a cualquier ciudad adyacente que sea *no* en `mask`:

`` `
nuevoMask = máscara Silencioso (1 Identificado siguiente)
dp[newMask] [next] = max(dp[newMask] [next],
dp[mask][último] + costo(último, siguiente)
`` `

*Respuesta*
Necesitamos un camino con **exactamente 'k' edges**, es decir, `k+1` ciudades visitadas.
Así que entre todas las máscaras con `popcount(mask) == k+1`, tome el valor máximo de `dp[mask][*]`.

* Complejidad*
*Estados* – `n * 2^n` ≤ 15 × 32 768 ♥ 0,5 M.
*Transiciones* – cada estado se expande a la mayoría de los vecinos `n-1`, todavía pequeños.

`` `
Tiempo O(n^2 · 2^n) (~ pocos millones de operaciones)
Memoria O(n · 2^n) (~ 2 MB)
`` `

Ambos están bien dentro de los límites para los casos de prueba dura.

-...

## 3down El malo - ¿Por qué no DFS + Memo o Dijkstra?

1. **DFS + Memo**
*Requiere una llave de máscara, por lo que terminas almacenando `dp[vertex][mask]` – esencialmente el mismo DP pero implementado en un estilo recursivo.
La profundidad de la recursión puede ser de hasta 'k' (≤ 50) – no hay desbordamiento de la pila, pero la memola es todavía grande y los factores constantes superiores. *

2. **Dijkstra‐like Search**
*Si tratas a cada estado `(mask, last)` como nodo en un gráfico enorme y ejecutas una cola de prioridad, el algoritmo es correcto pero exagerado.
La cola contendrá miles de entradas y la parte superior de las operaciones del montón domina el tiempo de ejecución. *

La línea inferior: **plain bitmask DP es tanto más simple como más rápido**.

-...

## 4down Los Ugly – Edge Cases " Pitfalls

Silencio Pitfall Silencio Lo que pasa es mentira Cómo evitar
Silencio------------------------
Silencio No se puede visitar más de 'n-1' bordes sin volver a visitar una ciudad. Silencio Regreso inmediatamente `-1`. Silencio
Las carreteras Duplicadas no están permitidas por la declaración del problema, pero si están presentes podría romper el DP. ← Construir listas de adjacency *sin* deduplicación o simplemente ignorar duplicados. Silencio
Silencio Valores de peaje grandes TENIDO Utilizar " in " es seguro ( " k*100 " = 5000 " ), pero si cambias las restricciones utilizan " largo " . Silencio
Silencio Conteo de población de máscaras incorrectas ¦ Olvidar comprobar `popcount(mask) == k+1`. Silencioso Uso `Integer.bitCount(mask)` (Java), `bin(mask).count('1')` (Python), `_construidoin_popcount` (C++). Silencio

-...

## 5down Implementaciones de referencia

A continuación se encuentran soluciones limpias y autocontenidas para **Java, Python y C++**.
Cada uno sigue el DP exacto descrito anteriormente.

■ *Todos los códigos asumen que la entrada ya está analizada en variables: `int n`, `int[] autopistas`, `int k`.*

-...

### 5.1 Java 17

``java
importar java.util*;

Solución de la clase pública {}
// lista de adjacency: lista de vecinos con pesos
Clase privada estática Edge {}
final int to, w;
Edge(int to, int w) { this.to = to; this.w = w; }
}

máximo Cost(int n, int[] autopistas, int k) {
si (k >= n) retorno -1; // imposible tener un camino simple de longitud k

// gráfico de construcción
Lista realizadaEdge confía g = nuevo ArrayList recomendado(n);
para (int i = 0; i < n; i++) g.add(nuevo ArrayList recomendado()
para (int[] e : carreteras) {}
g.get(e[0]).add(new Edge(e[1], e[2]));
g.get(e[1]).add(new Edge(e[0], e[2]));
}

int states = 1 < >
int[][] dp = int[states][n];
para (int[] fila : dp) Arrays.fill(row, Integer.MIN_VALUE);

// empezar desde cada ciudad
para (int v = 0; v) dp [1] [v] = 0;

// DP sobre máscaras
para (enmascarado = 1; máscaras) {}
// número de ciudades visitadas = cuenta(masca)
si (Integer.bitCount(mask) 1) continuar; // sólo necesitamos hasta k+1
para (incluido el último = 0; último se hizo n; último++) {}
int curVal = dp[mask][last];
si (curVal == Integer.MIN_VALUE) continúan;
para (Edge e : g.get(last) {
int nxt = e.to;
si (mask & nxt) != 0) continuar; // ya visitado
int newMask = Máscara Silencioso (1 ■ nxt);
dp[newMask][nxt] = Math.max(dp[newMask][nxt], curVal + e.w);
}
}
}

int best = -1;
int target MaskBits = k + 1;
para (enmascarado = 1; máscaras) {}
si (Integer.bitCount(mask) != targetMaskBits) continúan;
para (int v = 0; v) {}
mejor = Math.max(best, dp[mask][v]);
}
}
devolver mejor;
}
}
`` `

-...

### 5.2 Python 3

``python
importadores
de las colecciones importadas por defecto

def máximo Cost(n: int, highways: list[list[int], k: int) - título int:
si k >= n:
retorno -1

# Lista de adjacency
g = [[] for _ in range(n)]
para u, v, w en carreteras:
g[u].append(v, w))
g[v].append(u, w))

estados = 1
# dp[mask][v] = coste máximo para alcanzar v habiendo visitado 'mask '
dp = [-1] * n for _ in range(states)]
para v en el rango(n):
dp[1] [v] = 0

para máscara en rango(1, estados):
si bin(mask).count('1') 1:
continuar
por último en rango(n):
cur = dp[mask][last]
si cur == -1:
continuar
para nxt, w en g [last]:
si máscara " (1 " )
continuar
new_mask = máscara Silencioso (1 )
dp[new_mask][nxt] = max(dp[new_mask][nxt], cur + w)

mejor = 1
objetivo = k + 1
para máscara en rango(estados):
si bin(mask).count('1') != objetivo:
continuar
para v en el rango(n):
mejor = max(best, dp[mask][v])

mejor
`` `

-...

### 5.3 C++ 17

``cpp
#include יbits/stdc++.h
usando std namespace;

struct Edge {}
int to, w;
Edge(int to, int w) : to(to), w(w) {}
};

máximo Cost(int n, vector asignadovector correspondint carreteras, int k) {
si regresan -1;

/ Lista de adyacencia
vector realizador: Edge confianza g(n);
para (auto golpe e : autopistas) {}
g[e[0].push_back(Edge(e[1], e[2]));
g[e[1]].push_back(Edge(e[0], e[2]));
}

int states = 1 < >
vector se llevó a cabo mediante:

// empezar desde cada ciudad
para (int v = 0; v)

para (enmascarado = 1; mascarilla) {
si (__construido_popcount(mask) 1) continuar;
para (incluido el último = 0; último se hizo n; + posterior) {
int cur = dp[mask][last];
si (cur == INT_MIN) continúan;
para (auto &e : g[last]) {}
int nxt = e.to;
si continúan (mask " (1 " )
int newMask = Máscara Silencioso (1 ■ nxt);
dp[newMask][nxt] = max(dp[newMask][nxt], cur + e.w);
}
}
}

int best = -1;
int target = k + 1;
para (enmascarado = 1; mascarilla) {
si (__construido_popcount(mask) != target) continúan;
para (int v = 0; v)
mejor = max(best, dp[mask][v]);
}
devolver mejor;
}
`` `

-...

## 6 Cambios en el Código

``python
# Prueba de muestra
si __name_ == "__main__":
n = 4
carreteras = [0, 1, 5], [1, 2, 2], [2, 3, 3], [0, 2, 4]]]
k = 2
print(maximum Cost(n, highways, k))) # → 8
`` `

La prueba anterior corresponde a un camino `0 → 2 → 3` (costo 4 + 3 = 7) o `1 → 0 → 2` (5 + 4 = 9) – el máximo es `9`.
Puede ajustar el ejemplo para ver el algoritmo en acción.

-...

## 7 carreras ¿Por qué esta solución obtiene el ⭐ en su entrevista

* **Graph + DP + Bitmask** – patrones clásicos de entrevista que los reclutadores aman.
* **Tiempo & Memoria** – cumple con las restricciones “hard” con colores voladores.
* **Código Clean** – no hay bibliotecas adicionales, sólo un solo bucle sobre `mask ' y `last ' .
* **Language‐agnostic** – puedes escribir a mano la misma idea en Java, Python o C++ en un minuto.

Siéntete libre de pegar los snippets en tu IDE favorito, retocar el pergamino de entrada, o incluso añadir un pequeño programa de controlador para leer de 'stdin'.

-...

## 8️ Take‐away Checklist for Interviews

1. **Lea atentamente la declaración** – observe los bordes *exactamente* y *no revisits*.
2. **Ponte el diminuto `n`** - que insinúa a bitmask DP.
3. **Define the DP state** – `mask` + `last`.
4. **Initializar, transición y respuesta** – como se muestra.
5. ** Casos de borde huelguístico** ( " k " , carreteras vacías, etc.).
6. **Explica tu complejidad** – los reclutadores aman cuando hablas de `O(n^2·2^n)` y el uso de la memoria.

Buena suerte, y disfrutar de aplastar a LeetCode 2247! 🚀