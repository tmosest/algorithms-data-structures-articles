-...
Título: LeetCode 3387. Maximizar la cantidad después de dos días de conversiones -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📦 1. Code Solutions

A continuación encontrará tres soluciones completas para el problema **LeetCode** **“3387. Maximizar Cantidad después de dos días de conversiones** – uno cada uno en **Java**, **Python**, y **C+**.
Los tres usan la misma idea *BFS basado*:
1. Construye un gráfico bidireccional ponderado para el Día 1.
2. Ejecute BFS para calcular la cantidad máxima alcanzable desde la moneda inicial.
3. Reaccionar BFS el día 2, comenzando con las cantidades del día 1.
4. Devuelve la cantidad final de la moneda original.

■ ¿Por qué BFS? #
■ Con ≤ 10 bordes por día el gráfico es diminuto – BFS garantiza que visitamos cada nodo sólo cuando encontramos una cantidad mejor.
■ Es más fácil de entender, más rápido en la práctica para estas limitaciones, y evita el riesgo de flujos de puntos flotantes que pueden venir con DFS o DP exhaustivos.

-...

### 1.1 Java (LeetCode-style)

``java
importar java.util*;

Clase Solución {

public double maxAmount(String initialCurrency,
Lista realizadaLista realizadaString confianza pares1, doble[] tasas1,
Lista realizadaLista realizadaString confianza pares2, doble[] tasas2) {

// Día 1 gráfico
Mapa seleccionadoString, Mapa seleccionadoString, Double confidencial g1 = buildGraph(pairs1, rates1);
// Día 2 grafito
Mapa seleccionadoString, Mapa seleccionadoString, Double confidencial g2 = buildGraph(pairs2, rates2);

// Cantidades máximas después del día 1
Mapa seleccionadoString, Double confidencial day1 = bfs(inicialCurrency, g1, null);

// Cantidades máximas después del día 2 – empezar con resultados de día-1
Mapa seleccionadoString, Double confidencial day2 = bfs(inicialCurrency, g2, day1);

volver día2.getOrDefault(inicialCurrency, 1.0);
}

* Construir un gráfico bidireccional ponderado */
mapa privado seleccionadoString, Mapa seleccionadoString
Lista seleccionadaLista realizadaString confianza pares, doble[] tarifas {

Mapa seleccionadoString, Mapa seleccionadoString, Double confidencial graph = nuevo HashMap Quería();

para (int i = 0; i) ++i) {
Criar a = pares.get(i).get(0);
Crianza b = pares.get(i).get(1);
doble r = tasas[i];

graph.computeIfAbsent(a, k - título new HashMap quiso()).put(b, r);
graph.computeIfAbsent(b, k - título new HashMap quiso()).put(a, 1.0 / r);
}
Gráfico de retorno;
}

*
* BFS que mantiene la mejor cantidad vista hasta ahora.
* Si la entrada no es nula sembramos la cola con todas las llaves de la entrada.
*/
mapa privado(s)String, Double confidencial bfs(
Empieza String,
Mapa seleccionadoString, Mapa seleccionadoString Gráfico,
Mapa seleccionadoString, Double Propiedad init) {

Mapa seleccionadoString, Doble contacto mejor = nuevo HashMap garantizado();
si (init != null) {
best.putAll(init);
. ♫ ... {
best.put(start, 1.0);
}

Queue wonString] q = nuevo LinkedList recomendado(best.keySet());

(!q.isEmpty()) {
Cura de cuerda = q.poll();
doble curAmt = best.get(cur);

para (Map.Entrar)
graph.getOrDefault(cur, Collections.emptyMap()).entrySet()) {}

String nxt = e.getKey();
doble nuevo Amt = curAmt * e.getValue();

si (newAmt > best.getOrDefault(nxt, 0.0) {
best.put(nxt, newAmt);
q.offer(nxt);
}
}
}
devolver mejor;
}
}
`` `

-...

### 1.2 Python 3

``python
de las colecciones importan defaultdict, deque
de la importación Lista

Solución de clase:
def maxAmount(
auto,
inicialCurrency: str,
pares1: List[List[str],
Tasas1: Lista[flot],
pares2: List[List[str],
Tasas2: Lista[flot]
) - flotador de confianza:

g1 = self.build_graph(pairs1, rates1)
g2 = self.build_graph(pairs2, rates2)

day1 = self.bfs(initialCurrency, g1, None)
day2 = self.bfs(initialCurrency, g2, day1)

retorno día2.get(inicialCurrency, 1.0)

def build_graph
auto, pares: List[List[str]], tarifas: List[float]
) defaultdict:
g = defaultdict(dict)
para (a, b), r en zip(paires, tarifas):
g[a][b] = r
g[b][a] = 1.0 / r
retorno g

def bfs(
auto,
empezar:
gráfico: defaultdict,
init: dict tención Ninguno,
) dict:
mejor = init.copy() si init else {start: 1.0}
q = deque(best.keys())

mientras q:
cur = q.popleft()
cur_amt = best[cur]
para nxt, tasa en graph.get(cur, {}).items():
new_amt = cur_amt * rate
si new_amt > best.get(nxt, 0.0):
mejor[nxt] = new_amt
q.append(nxt)
mejor
`` `

-...

### 1.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
doble maxAmount(estring initial Moneda
vectorial identificadovector identificadostring confianza ambos pares1, vector asignados
vectorial identificadovector identificadostring persuadido ambos pares2, vector asignados

auto g1 = buildGraph(pairs1, rates1);
auto g2 = buildGraph(pairs2, rates2);

unordered_map detectstring, double ratio day1 = bfs(initialCurrency, g1, {});
unordered_map detectstring, double ratio day2 = bfs(initialCurrency, g2, day1);

volver día2.count(initialCurrency) ? day2[initialCurrency] : 1.0;
}

privado:
// Gráfico: nodo - lista de {neighbor, peso}
vector noordered_map buscadostring, doble título
vector const vector llevado a cabo, constring vector implicado pares, const vector armonizado
unordered_map buscadostring, unordered_map adj;
para (size_t i = 0; i) ++i) {
cadena a = pares[i][0];
cadena b = pares[i][1];
doble r = tasas[i];
adj[a][b] = r;
adj[b][a] = 1.0 / r;
}

// Convertir en forma vectorial para más fácil BFS
vector noordered_map buscadostring,double confianza g;
para (cont auto cho [nodo, vecinos] : adj)
g.emplace_back (vecinos);
retorno g;
}

unordered_map buscadostring,double título bfs(
const cordón
const vector se llevó a cabo unordered_map Gráfico,
const unordered_map recomendadastring,double título* init) {

unordered_map detectstring,double título best;
queue hacía referencia q;

si (inito) {
mejor = *init; // semilla con resultados de día a 1
para (continuidad auto-cliente [k, v] : *init) q.push(k);
. ♫ ... {
best[start] = 1.0;
q.push(start);
}

(!q.empty()) {
string cur = q.front(); q.pop();
doble curAmt = mejor[cur];
para (auto it = graph[cur].cbegin(); it != graph[cur].cend(); ++it) {
const string limitado nxt = it-
doble tasa = it-jósegundo;
doble nuevo Amt = curro * Tasa de ajuste;
si (newAmt > best[nxt]) {}
mejor[nxt] = newAmt;
q.push(nxt);
}
}
}
devolver mejor;
}
};
`` `

■ **Nota**: La versión C++ mantiene el gráfico en un vector de mapas para la velocidad. Con los pequeños tamaños de entrada, la representación "vector realizadaunordered_map贸" es más que lo suficientemente rápida.

-...

## 📘 2. Blog Artículo – “El Bien, el Mal” el Ugly de Conversiones de Moneda de dos días”

■ *Título*
■ **Maximizar la cantidad después de dos días de conversiones – una profunda cala (Java fort Python TEN C++)* *

-...

## Tabla de contenidos

1. **Problema general**
2. **Por qué este problema es un Gold‐Mine para los algoritmos de Gráfico* *
3. **La Estrategia BFS – El Bien* *
3.1 Construcción del Gráfico Bidireccional
3.2 First‐ Día BFS
- 3.3 Segundo Día BFS
4. ** Enfoques alternativos – El mal de la ugly**
- 4.1 DFS agotador
- 4.2 Programación dinámica en secuencias de bordes
- 4.3 Bellman‐Ford " Floyd‐ Warshall (overkill here)
5. ** Análisis de la complejidad**
6. **Casos Corner y Pitfalls**
7. #Code Walk-through (Java, Pitón, C++)* *
8. **Toke‐away < Final Thoughts* *

-...

#### 2.1 Resumen de problemas

Se le dan dos tipos de cambio *independientes*: uno para **Día 1** y otro para **Día 2**.
A partir de **1 unidad** de la `ciudad inicial', usted puede:

1. Convertir a lo largo de cualquier cadena de intercambios el día 1.
2. Mantenga las monedas resultantes durante la noche.
3. Convertir de nuevo en Día 2 utilizando las tarifas de ese día.

Su objetivo: ** devolver la cantidad máxima posible de la moneda original después de los dos días**.

* Limitaciones*:
- 2 ≤ Наливывывывые 10 por día.
- Los tipos de cambio son números reales 0.
- Los Gráficos son totalmente bidireccionales (siempre puedes invertir un comercio).

-...

### 2.2 ¿Por qué Algoritmos de Gráficos?

A primera vista, el problema se parece a un rompecabezas dinámico de programación o “knapsack-style”, pero es, de hecho, un problema con la posibilidad de alcanzar gráficas ** ponderadas**:

- **Nodos** - monedas.
- **Edges** – tipos de cambio directos, peso = multiplicador.
- ** Objetivo** – maximizar el producto de pesos a lo largo de un camino.

Porque puedes revertir cualquier cambio, cada borde es bidireccional.
Con sólo 10 bordes por día, el gráfico tiene a la mayoría de 11 nodos, haciendo ** primera búsqueda (BFS)** un ajuste ideal.

-...

### 2.3 The BFS Strategy – The Good

Silencio Lo que hacemos _ Por qué funciona
...------------------------
Silencio **Construir el gráfico** Silencio Para cada tasa `a → b` añadir `b → a` con peso `1/r`. Silencio Mantiene el gráfico simétrico; nunca faltamos una conversión inversa. Silencio
Silencio **Día 1 BFS** Silencio Inicio en `inicialCurrency` con cantidad = 1. Silencio Cada vez que encontramos un mejor producto para un vecino lo empujamos a la cola. Silencio
Silencio **Día 2 BFS** Silencio Seed la cola con **todas** sumas del día 1. Silencio Por la noche puede empezar desde cualquier divisa que posea. Silencio
Silencio** Resultado** después del día 2. Silencio El producto del mejor Día 1 cantidad con el mejor Día 2 multiplicador. Silencio

##### ¿Por qué BFS es *bueno*

- **Simplicidad** - sin recidiva, sin problemas de profundidad de pila.
- **Optimality** – cada vez que vemos un producto más grande lo propagamos inmediatamente.
- **Hablado** – Con ≤ 10 bordes por día, BFS termina en microsegundos.
* Seguridad nuclear* – Evitamos la recidiva profunda que podría llevar a un punto flotante bajo/desbordamiento.

-...

### 2.4 Enfoques alternativos – El mal

TENCIÓN ANTERIOR Cuando *might* sea útil ANTERIENTE SONIDOS POR este problema
Silencio----------------------------------------
Silencio **Exhaustivo DFS** Silencio Profundidad pequeña, todas las permutaciones posibles Silencioso exponencial, muchos cálculos repetidos, apilar el riesgo de desbordamiento. Silencio
Silencio ** Programación Dinámica** (DP sobre los bordes) Silencio Gráficos más grandes, necesidad de rastrear *estados* ← Requiere la memoria `O(n^2)` para todos los estados intermedios posibles – sobrematar para ≤ 10 bordes. Silencio
Silencio **Bellman–Ford** Silencio Detecta ciclos negativos (en el espacio de bitácora) Silencioso; sobrecarga algorítmica de `O(VE)` para pequeños gráficos. Silencio
Silencio **Floyd-Warshall** Silencio All‐pairs reachability Silencio `O(V^3)` – innecesario con tan pocos nodos. Silencio

■ **Bottom line**: *BFS* alcanza el equilibrio perfecto de claridad, rendimiento y bajo uso de memoria para los límites dados.

-...

### 2.5 Complexity Analysis

Silencio Fase de las operaciones infligidas
Silencio------------------------
← Construir grafito (Día 1) Silencio O(n) bordes Silencio **O(n)** Silencio
← Construir el gráfico (Día 2) Silencio O(m) los bordes Silencio **O(m)**
Silencio BFS Día 1 Silencio O(V + E) por actualización **O(V + E)** (≤ 11 + 10)
TENIDO BFS Día 2 TENIDO MUNDO TENIDO **O(V + E)**
Silencio **Total** Silencio **O(n + m)** Silencio **~O(20)** – tiempo prácticamente constante. Silencio

El uso de la memoria también es insignificante – sólo un puñado de mapas que contienen a la mayoría de 11 teclas.

-...

### 2.6 Common Pitfalls

Silencio Pitfall Silencio
Silencio...
Silencio Olvidando añadir el borde *reverso* (`1/r`) Silencio `graph.putIfAbsent(b, new HashMap Quería()); graph.get(b).put(a, 1.0 / r);` Silencio
Silencio Devolviendo 0.0 para monedas que no pueden ser alcanzadas Silencio Default a `1.0` (número original) si clave falta Silencio
Silencio Usando la recursión en un gráfico cíclico TEN Prefer BFS/queue o DFS iterativa para evitar el desbordamiento de pila ANTE

-...

### 2.7 Test Harness (Optional)

``java
public static void main(String[] args) {
Solución s = nueva solución ();
Lista de(s)
List.of("USD", "EUR"),
Lista.de("EUR", "JPY")
);
doble[] r1 = {0.9, 120};

Lista realizadaLista realizada p2 = Lista de(
List.of("USD", "GBP"),
Lista.de("GBP", "JPY")
);
doble[] r2 = {0.8, 150};

System.out.println(s.maxAmount("USD", p1, r1, p2, r2));
}
`` `

Lo anterior imprimirá la cantidad máxima de **USD** que puede terminar después de los dos días.

-...

## 📚 2. Blog Artículo – SEO‐Optimized Guide

■ **Maximizar la cantidad después de dos días de conversiones – Resolver el problema LeetCode en Java, Python & C+* *

-...

#### 2.1 Introduction

LeetCode **3387 – “Maximize Amount After Two Days of Conversions”** es un clásico rompecabezas *graph* que combina la financiación del mundo real con el pensamiento algoritmo. La tarea: empezar con una unidad de una moneda, cambiarlo por otros durante **dos días**, y terminar con la cantidad ** más grande posible** de su moneda original.

A continuación diseccionamos el problema, caminar a través de la solución más eficiente (BFS), y proporcionar código completo en **Java, Python, y C+**. Si usted es un prepper de entrevista de codificación, un programador competitivo, o sólo un códice curioso, este artículo es su manual de inicio rápido.

-...

### 2.2 Captura de problemas

- ** Entrada*
- 'inicialCurrency' - una cadena como ''USD'.
- `pairsDay1` - lista de intercambios directos para el Día 1.
- `ratesDay1` - multiplicadores correspondientes ( 0).
- `pairsDay2` Day2` - el mismo día 2.

*Operación*
1. Convertir a lo largo de cualquier camino en el Día 1.
2. La noche a la mañana puede *tener* cualquier moneda con la que termine.
3. Convertir de nuevo en Día 2 utilizando las tarifas de ese día.

- ** Objetivo** – retorno **maximum** cantidad de `inicialCurrency` después de ambos días.

**Por qué importa*: El problema pone a prueba su capacidad de modelar un sistema financiero como gráfico, manejar los bordes bidireccionales y maximizar un producto de números reales – una perfecta intersección de matemáticas y codificación.

-...

### 2.3 La “buena” – Primera búsqueda de la pantemia

Trataremos cada día como un gráfico dirigido separado** (aristas bidireccionales). BFS naturalmente encaja porque:

- **Pequeño gráfico**: ≤ 11 nodos, ≤ 10 bordes por día.
- **No recursión**: elimina el riesgo de desbordamiento.
- **La propagación inmediata**: un producto mejor es empujado de inmediato.

**Pseudocode**:

`` `
buildGraph(pairs, rates):
para cada (a, b, r):
añadir borde a- peso r
añadir el borde b- títuloa peso 1/r

BFS(startNode):
queue = [(startNode, 1.0)]
mejor = {startNode: 1.0}
mientras que la cola no está vacía:
nodo, amt = cola.pop()
para cada vecino, w en el gráfico [nodo]:
nuevo Amt = amt * w
si nuevoAmt > mejor[neighbour]:
best[neighbour] = newAmt
queue.push (vecino, nuevoAmt))
mejor
`` `

Aplicar " BFS " dos veces: una vez por el Día 1 (comenzando desde `inicialCurrency ' ), una vez por el Día 2 (comenzando desde *todas las* monedas que posee después del Día 1). La respuesta es simplemente `mejor[inicialCurrency]` después del segundo BFS.

-...

### 2.4 ¿Por qué no DFS o DP?

TENIDO TÉCNICA ANTERIOR ANTERIOR ANTERIOR POR QUÉ No es ideal para Day‐ Cierre tóxico
Silencio...------------------------
Silencio **DFS** Silencio Búsqueda de caminos minúsculas y exhaustivas en tiempo exponencial, trabajo redundante, riesgo de recidiva profunda. Silencio
Silencio ** Programación Dinámica** Silencio Espacio de Estado grande Silencio Requiere `O(V^2)` memoria – innecesaria para ≤ 10 bordes. Silencio
Silencio **Bellman‐Ford** Silencio Detección de ciclos en log‐space tención Añade complejidad; no hay ciclos para detectar. Silencio
Silencio **Floyd–Warshall** tención All‐pairs distances  `O(V^3)` – overkill for this small graph. Silencio

El método BFS es *lighter*, *faster* y *clearer* – exactamente lo que buscan los entrevistadores.

-...

### 2.5 Code Walk-through

A continuación encontrará las implementaciones completas y anotadas en **Java**, **Python**, y **C+**. Cada uno sigue el mismo plano:

1. **Construir el gráfico** (bidirectional).
2. ** Día 1 BFS** para poblar `AmountDay1`.
3. **Día de Rin 2 BFS** semillas con `AmountDay1`.
4. **Retorno** `amountDay2[initialCurrency]`.

■ *Véase la sección “Test Harness” para un ejemplo ejecutable. *

-...

### 2.6 Edge Cases " Numerical Safety

- ** Monedas no alcanzables** - por defecto a la cantidad original (`1.0`).
- división cero** - nunca sucede porque todas las tarifas 0.
- **Precisión** – El uso de dobles/floats está bien; el producto de ≤ 20 multiplicadores se mantiene dentro del alcance.

-...

### 2.7 Final Take-away

LeetCode 3387 es un problema *gráfico disfrazado de rompecabezas financiero*. La solución óptima y amigable del entrevistador es un BFS **iterative** que respeta la naturaleza bidireccional de los comercios.

Ya sea que lo escribas en **Java** con `HashMap`, **Python** con diccionarios, o **C+** con `unordered_map`, la lógica subyacente sigue siendo idéntica. Los fragmentos de código de arriba ilustran el *exacto* mismo algoritmo, adaptado a las expresiones del lenguaje.

¡Feliz codificación!

-...

### 2.8 Referencias > Lectura posterior

- Problema LeetCode 3387 – [Link](https://leetcode.com/problems/maximize-amount-after-two-days-of-conversions/)
- Graph Traversal: BFS vs DFS – [GeeksforGeeks](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)
- Bellman‐Ford Algorithm – [Wikipedia](https://en.wikipedia.org/wiki/Bellman%E2%80%93Ford_algorithm)
- Floyd-Warshall All‐Pairs Shortest Path – [Coursera](https://www.coursera.org/lecture/algorithms-ongraphs/floyd-warshall-shortest-paths-5B6g8)

-...

■ *Al dominar la estrategia BFS para LeetCode 3387, estarás listo para enfrentar cualquier problema de cambio basado en gráficos que llegue a tu manera. *

-...

¡Feliz Solving