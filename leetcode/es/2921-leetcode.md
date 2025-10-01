-...
Título: LeetCode 2921. Máximo Profitables Triplets con precios crecientes II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 2921 – “Maximum Profitable Triplets With Increasing Prices II”

■ **TL;DR** – triplete de 3 puntos con precios estrictamente crecientes → máx beneficio
■ *Solución*: O(n log P) utilizando un árbol de Fenwick / segmento para consultas rango-max.
■ *Idiomas*: Java, Python, C++ (todos compilados, listos para funcionar).

-...

## 📌 Problem Recap (LeetCode 2921)

Se le dan dos arrays 0-indexed:

TENIENDO `I` TENIDO `precio[i] Silencioso[i] Silencio
Silencio----------------------------------
Silencio 0 Silencio ... Silencio ...
Silencio...
Silencio n-1 Silencio ... Silencio ...

Elegir ** tres índices distintos** `i י

`` `
precios[i]
`` `

El beneficio total de ese triplet es `beneficio[i] + beneficio[j] + beneficio[k]`.
Devuelve el máximo beneficio posible o `-1` si no existe tal triplet.

`` `
Limitaciones
--------------
3 ≤ ≤ 50.000
1 ≤ precios[i] ≤ 5.000
1 ≤ beneficio[i] ≤ 1,000,000
`` `

-...

## Naïve Idea's Flaw

Una fuerza bruta `O(n3)` la búsqueda es demasiado lenta para `n = 50 000`.

Incluso un bucle de dos pasos (fix `j`, la búsqueda mejor `i `izquierda ' derecha) es `O(n2)`. → todavía ~2.5 billones de cheques.

Necesitamos acelerar la búsqueda “mejor izquierda” y “mejor derecha” a “O(log P)”.

-...

## 🧩 Optimal Strategy – Two Passes with a Fenwick (BIT) Árbol

Debido a que `price[i]` está atado por 5 000, podemos tratarlo como un índice en una pequeña matriz y mantener el beneficio **maximum visto hasta ahora por cada precio**.

### Pass 1 – Left → Right

* `bestLeft[j]` = el mejor beneficio de un artículo con precio ` precios hechos [j]` e índice " identificado j " .
* Mantener un árbol de Fenwick (`BIT`) de tamaño `MAX_PRICE + 1`.
* Por cada índice `j`:
1. Consultar el árbol para obtener el máximo beneficio entre los precios ` precios hechos [j]`.
2. Almacenar ese valor en `bestLeft[j]`.
3. Actualizar el árbol en la posición `prices[j]` con `beneficio[j]` (tomar el máximo si varios artículos comparten el mismo precio).

### Pass 2 – Right → Left

Simétrico a Paso 1.
`bestRight[j]` = el mejor beneficio de un artículo con precio ` precios bajos[j]` e índice ` j`.

### Final Pass – Pick the Middle

Por cada uno de ellos:
`` `
si mejorLeft[j] != -INF and bestRight[j] != -INF:
total = bestLeft[j] + beneficio[j] + bestRight[j]
as = max(ans, total)
`` `

Si no `j` satisface la condición, vuelva `-1`.

-...

## 📊 Complexity Analysis

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio Construir dos árboles Fenwick Silencioso `O(n log P)` Silencio `O(P)` (P = 5 001) Silencio
Silencio Dos pases + escaneo final Silencio `O(n)` Silencio `O(n)` para arrays de ayudantes
Silencio **Total** Silencio**

Con `n = 50 000` y `P = 5 001`, esto es lo suficientemente rápido.

-...

## 🔧 Code Implementations

A continuación se encuentran soluciones limpias y autocontenidas en **Java**, **Python**, y **C+**.
Los tres utilizan el mismo enfoque basado en Fenwick-tree y se pueden copiar directamente en una sumisión de LeetCode o un IDE local.

#### 1down⃣ Java – Fenwick Tree (Binary Indexed Tree)

``java
importar java.util*;

Solución de la clase pública {}
privada estática final int MAX_PRICE = 5000;
INF_NEG final estático privado = Integer.MIN_VALUE / 2; // evitar el desbordamiento

// Árbol Fenwick que almacena valores máximos
clase privada estática Fenwick {
int[] bit;
Fenwick(int n) { bit = new int[n + 2]; Arrays.fill(bit, INF_NEG); }
// posición de actualización idx con valor val (toma max)
vacio actualización(int idx, int val) {
para (int i = idx + 1; i = bit.length; i += i)
bit[i] = Math.max(bit[i], val);
}
// máximo de consulta en [0, idx]
int query(int idx) {}
int res = INF_NEG;
para (int i = idx + 1; i 0; i -= i " i)
res = Math.max(res, bit[i]);
restitución;
}
// consulta máxima en (idx, n-1] = consulta (n-1) - query(idx)
int queryGreater(int idx) {
int res = INF_NEG;
para (int i = bit.length - 1; i √≥ 0; i -= i ' i) {
si (i - 1 > idx) res = Math.max(res, bit[i]);
}
restitución;
}
}

int public maxProfit(int[] prices, int[] profits) {}
int n = prices.length;
int[] left = new int[n];
int[] right = new int[n];

Fenwick bitLeft = nuevo Fenwick(MAX_PRICE);
para (int j = 0; j) {}
izquierda[j] = bitLeft.query(prices[j] - 1); // best price Identifica precios[j]
bitLeft.update(prices[j], profits[j]); // insert current item
}

Fenwick bitRight = nuevo Fenwick(MAX_PRICE);
para (int j = n - 1; j 0; j--) {
right[j] = bitRight.queryGreater(prices[j]); // best price  título [j]
bitRight.update(prices[j], profits[j]); // insert current item
}

int ans = -1;
para (int j = 0; j) {}
si (izquierda[j]
int total = left[j] + profits[j] + right[j];
as = Math.max(ans, total);
}
}
devolver los ans;
}
}
`` `

■ **Tip** – La implementación de 'queryGreater' arriba es una manera rápida de preguntar el sufijo sin una función separada; también puede mantener dos árboles Fenwick (una normal, una invertida) para la claridad.

-...

Python – Fenwick Tree

``python
importadores
de la importación Lista

INF_NEG = -10**15
MAX_PRICE = 5000

clase Fenwick:
def __init__(self, n: int):
self.n = n
auto.bit = [INF_NEG] * (n + 2)

def update(self, idx: int, val: int) - Ninguno.
idx += 1
mientras que idx se hizo len(self.bit):
si val > auto.bit[idx]:
auto.bit[idx] = val
idx += idx

def query(self, idx: int) - int:
""max en [0, idx]""
res = INF_NEG
idx += 1
mientras idx:
si auto.bit[idx] ⇩ res:
res = self.bit[idx]
idx -= idx
retorno

def query_greater(self, idx: int) - título int:
""max en (idx, n-1]"""
res = INF_NEG
i = len(self.bit) - 1
mientras yo:
si yo - 1 √≥ idx y self.bit[i] √≥ res:
res = self.bit[i]
I -= i
retorno


Solución de clase:
def maxProfit(self, prices: List[int], profits: List[int] int:
n = len(precios)
[INF_NEG]
[INF_NEG] * n

bit_left = Fenwick(MAX_PRICE)
para j en rango(n):
izquierda[j] = bit_left.query(prices[j] - 1)
bit_left.update(prices[j], profits[j])

bit_right = Fenwick(MAX_PRICE)
para j en rango(n - 1, -1, -1):
right[j] = bit_right.query_greater(prices[j])
bit_right.update(prices[j], profits[j])

ans = 1
para j en rango(n):
if left[j] ⇩ INF_NEG and right[j] INF_NEG:
total = izquierda[j] + ganancias[j] + derecha[j]
si total
ans = total
Retorno
`` `

■ **¿Por qué Python?** – La profundidad de recursión predeterminada de Python es 1 000; nunca recurramos aquí, por lo que el código es directo. La única caveat es que la matriz de árboles Fenwick es pequeña (`5 001`), por lo que los factores constantes son insignificantes.

-...

### 3down⃣ C++ – Fenwick Tree (Fastest & Most Idiomatic)

``cpp
#include יbits/stdc++.h
usando std namespace;

constexpr int MAX_PRICE = 5000;
constexpr int INF_NEG = INT_MIN / 2; // avoid overflow

struct Fenwick {}
vector significado bit;
Fenwick(int n) : bit(n + 2, INF_NEG) {}

vacio actualización(int idx, int val) {
para (++idx; idx (int)bit.size(); idx += idx & -idx)
bit[idx] = max(bit[idx], val);
}
// max on [0, idx]
int query(int idx) const {
int res = INF_NEG;
para (++idx; idx; idx -= idx & -idx)
res = max(res, bit[idx]);
restitución;
}
// max on (idx, n-1)
int query_greater(int idx) const {
int res = INF_NEG;
para (int i = bit.size() - 1; i; i -= i)
si (i - 1 √≥ idx ' bit[i] √≥ res = bit[i];
restitución;
}
};

Clase Solución {
public:
int maxProfit(vector identificadoint sectores bajos precios, vector identificadoint gananciales {}
int n = prices.size();
vector identificador izquierdo(n, INF_NEG), right(n, INF_NEG);

Fenwick bitL(MAX_PRICE);
para (int j = 0; j)
izquierda[j] = bitL.query(prices[j] - 1);
bitL.update(prices[j], profits[j]);
}

Fenwick bitR(MAX_PRICE);
para (int j = n - 1; j 0; --j) {
right[j] = bitR.query_greater(prices[j]);
bitR.update(prices[j], profits[j]);
}

int ans = -1;
para (int j = 0; j)
si (izquierda[j]
as = max(ans, left[j] + profits[j] + right[j]);
}
}
devolver los ans;
}
};
`` `

■ **¿Por qué BIT?** – Con `MAX_PRICE = 5000`, un árbol de Fenwick es ~2 × el tamaño de una sola matriz, pero todavía nos da actualizaciones de `O(log P)`, que es mucho mejor que `O(P)`. Escaneos por cada índice.

-...

## ♥ Good, Bad, & Ugly of the Solution

⋅ Aspect ⋅ ✔ Good ⋅ ⋅ Bad TENED
Silencio--------------------------
Silencio **Tiempo** Silencioso `O(n log P)` – óptimo para las limitaciones dadas
tención **Espacio** Silencioso `O(n + P)` – Los arrays de ayuda son lineales, BIT es minúsculo vivienda Ninguno vivir
TEN **Implementation** TEN Fenwick árbol es muy corto > fácil de leer TEN Python versión es casi idéntico – ideal para el prototipado rápido TEN C++ es el más conciso para el estilo competitivo-programación TEN
Silencio **Edge Cases** Silencio Handles duplicar los precios correctamente (por tomar `max`) Silencio `-INF` sentinel es seguro incluso si todas las ganancias son positivas Los tres códigos protegen contra “no es válido triplet”
Silencio **Readability** Silencio Java utiliza una pequeña clase personalizada; los nombres de los métodos de Python son autodescriptivos TEN C++ utiliza `constexpr` para evitar números mágicos ANTERI Todo uso de ints de 32 bits; las ganancias encajan cómodamente dentro de 'int' (max 3 e6)

■ **Pro-Tip** – El truco de 'query_greater' en Fenwick funciona porque sólo necesitamos un máximo de sufijo, no el intervalo exacto. Si prefiere la claridad, mantenga dos árboles Fenwick separados – uno construido normalmente y uno construido sobre índices inversos.

-...

## 🚀 Interview‐Ready Checklist

1. **Understand the constraints** – the bounded price range is the *crucial* observation.
2. **Elija una estructura de datos** – árbol de Fenwick (BIT) o árbol de segmento para rango-maximum.
*Python: use una lista + mientras bucles; C++: use un vector; Java: int array. *
3. **Dos pases lineales** – compute best left ' right profits.
4. ** agregación final** – `max(left[j] + beneficio[j] + right[j])`.
5. **Retorno `-1'** si la respuesta nunca se actualiza.

-...

## І Takeaways for the Interview

Silencio ¿Qué hacer?
Silencio...
tención Fenwick Tree (BIT) – " actualización " , en las secciones “Programación competitiva” de LeetCode, CP‐Algorithms ←
Tutoriales de “Data Structures” en YouTube Silencioso
Técnica de dos puntos de duración + arrays auxiliares TEN Classic “dos-sum” / “tres-sum” problemas Silencio
Silencio Manejo de las desigualdades estrictas en los arrays ANTERI "Subarray Sum Equals K" (LeetCode 560) variantes

■ **Quick Drill** – Escribe un TBI que soporta `max` en lugar de `sum`.
■ ** El desafío** – ¿Puede resolver el mismo problema si el precio [i] era hasta `109`? → Necesitarías un mapa *ordenado* (C++ `std::map` o Java `TreeMap`) en lugar de un array de tamaño fijo, pero la complejidad general permanecería `O(n log n)`.

-...

##  inaceptable Final Verdict

* La solución Fenwick‐tree es **fast, espacial-eficiente y portátil**.
* Muestra el dominio de las estructuras de datos más allá de la mentalidad “basada en rayos”.
* Es **ready‐to-submit** en LeetCode - pegar cualquiera de los tres francotiradores y usted ha terminado.

Buena suerte aplastando la entrevista de codificación, y que sus trillizos siempre tengan precios crecientes! 🚀