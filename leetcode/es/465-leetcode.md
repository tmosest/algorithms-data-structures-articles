-...
Título: LeetCode 465. Optimal Account Balancing -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Code Solutions

A continuación encontrarás **ready‐to-run** implementaciones para el problema LeetCode Hard *Optimal Account Balancing* (problema 465) en **Java 17**, **Python 3.11**, y **C+17**.
Las tres versiones utilizan la misma idea central:
1. Computa el equilibrio neto de cada persona.
2. Mantenga sólo los saldos no cero.
3. Use backtracking + memoization (bit-mask DP) para encontrar el número mínimo de asentamientos.

. *Consejo*: El DFS recurrente está garantizado para terminar en unos pocos milisegundos por las limitaciones dadas (`transactions.length ≤ 8`), por lo que es perfecto para la práctica de entrevistas.

-...

## Java 17

``java
importar java.util*;

Solución de la clase pública {}
int minTransfers(int[][] transactions) {}
// 1 / ️ Construir saldos netos
Mapa seleccionadoInteger, Integer inteligente bal = nuevo HashMap garantizado();
(int[] t : transactions) {}
bal.merge(t[0], t[2], Integer::sum);
bal.merge(t[1], -t[2], Integer::sum);
}

Mantenga sólo los saldos no cero
Lista de deudasInteger título = nuevo ArrayList correctamente();
para (int v : bal.values())
si (v!= 0) deudas.add(v);

int n = debts.size();
// 3Ω⃣ Memoization table: dp[mask] = mínimo #settlements for this subset
int[] memo = nuevo int[1]
Arrays.fill(memo, -1);
memo[0] = 0; // vacío set needs 0 transactions

retorno n - dfs(1  Se hizo n) - 1, deudas, memo);
}

// DFS con memoización
int privado dfs(inmaculada, Lista de deudas Integer, int[] memo) {
si (memo[mask] != -1) memo de retorno;

saldo no comprometido Sum = 0, best = 0;
para (int i = 0; i) i++) {
int bit = 1 < >
si (mask) != 0) {
balanceSum += debts.get(i);
mejor = Math.max(mejor, dfs(mask ^ bit, debts, memo));
}
}
// Si la suma del subconjunto es cero podemos establecerlos juntos en 1 txn
memo[mask] = mejor + (balanceSum == 0 ? 1 : 0);
devolver memo[mask];
}
}
`` `

-...

## Python 3.11

``python
de la importación Lista
desde functools import lru_cache
de las importaciones de colecciones Contrato

Solución de clase:
def minTransfers(self, transactions: List[List[int]]) int:
# 1 Equilibrio neto por persona
bal = Counter()
para frm, a, amt en las transacciones:
bal[frm] += #
bal[to] -= #

# 2⃣ Mantener sólo saldos no cero
deudas = [v para v en bal.values() si v]
n = len(debts)

@lru_cache(None)
def dfs(mask: int) - título int:
"""Retorno número máximo de grupos de suma cero podemos formar desde subconjunto `mask`.""
si máscara == 0:
retorno 0
balance_sum = 0
mejor = 0
para i en rango(n):
bit = 1
si mascara >
balance_sum += deudas[i]
mejor = max(best, dfs(mask ^ bit)
mejor rendimiento + (1 si balance_sum == 0 más 0)

# 3️ Resultado: n - maximal #zero‐sum groups
retorno n - dfs(1  obtenidos n) - 1)
`` `

-...

### C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minTransfers(vector seleccionadovector identificadoint {}
unordered_map observadoint, long long long long long escudo;
para (auto &t : transacciones) {}
bal[t] += t[2];
bal[t[1]] -= t[2];
}

deudas vectoriales largas;
para (auto &p : bal)
si (p.second) debts.push_back(p.second);

int n = debts.size();
vector implicado memo(1  se realizó n, -1);
memo[0] = 0; // vacío set needs 0 txns

función seleccionadaint(int) título dfs = [ cl](int mask) - int {
si (memo[mask] != -1) memo de retorno;
larga suma = 0;
int best = 0;
para (int i = 0; i) {}
si (mask " (1 " ) {
suma +=deudas[i];
mejor = máx(mejor, dfs(mask ^ (1  obtenidos i));
}
}
memo[mask] = mejor + (sum == 0 ? 1 : 0);
devolver memo[mask];
};

retorno n - dfs(1 ' escrito n) - 1);
}
};
`` `

-...

## 2. Artículo del Blog – “Cobertura de la cuenta óptima: el bien, el mal y el ugly”

■ **SEO Palabras clave**: LeetCode 465, Optimal Account Balancing, hard algoritmo, backtracking, DFS, bitmask DP, preparación de entrevistas, entrevista de ingeniero de software, solución Java, solución Python, solución C++, consejos de entrevista de trabajo.

-...

#### Introduction

Cuando golpeaste a LeetCode 465 – *Optimal Account Balancing* – estás mirando un problema clásico **minimum‐transaction** que se siente engañosamente simple pero es en realidad un problema **Hard**. En una entrevista real tendrás que explicar *por qué* funciona un enfoque de retroceso, cómo podas el espacio de búsqueda, y por qué la solución es lo suficientemente eficiente para las limitaciones.

A continuación caminamos por el **bueno** (por qué el problema es un gran tema de la entrevista), el **bad** (qué obstáculos a menudo tropiezan con los candidatos), y el **ugly** (el código ingenuo que va a salir de tiempo). Terminaremos con una solución pulida y lista para la producción en **Java**, **Python**, y **C+**.

-...

### The Good: Why This Problem Matters

Por qué es útil
Silencio...
Silencio **Graph of Debt** Silencio El problema se puede visualizar como un gráfico dirigido ponderado. Prueba la comprensión de los conceptos de flujo *net*. Silencio
Silencio **Backtracking + Memoization** tención Demonstrates mastery of recursion, pruning, and DP on subsets – core skills for any senior role. Silencio
Silencio **Pequeña entrada, Búsqueda Exponencial** Silencio muestra que *time-complexity* importa más que *espacio*; el entrevistado debe reconocer la naturaleza y el optimismo de O(2^n). Silencio
Silencio **Language‐agnostic** Silencio Puedes resolverlo en Java, Python, C++, Rust... la lógica sigue siendo la misma, demostrando el pensamiento algorítmico sobre la fluidez del lenguaje. Silencio
Silencio **Job‐Search Edge** Silencio Resolver este problema de forma limpia es un punto de referencia común de entrevistas para las startups fintech, y cualquier papel inteligente. Una solución pulida se nota en tu GitHub. Silencio

-...

### The Bad: Common Pitfalls

Pitfall Silencio Por qué Fails Silencio
Silencio...
Silencio **Tratar a cada persona como un nodo** Silencio Contando `de` y `a` por separado puede conducir a 12 nodos, pero el número de *eficacia* personas es ≤ 8. Olvidar colapsar el gráfico añade un trabajo inútil. Silencio
Silencio **No Pruning** Silencio Un ingenuo DFS que intenta cada par de personas en cada paso explora las posibilidades 'n!' – inaceptable para 'n = 8`. Silencio
Silencio **Using Maps for Memoization** Silencio Usando `Map Haga clic enInteger, Integer `` con una * llave de montaje* para subconjuntos conduce a la piratería en la cabeza; un array de bitmask es más rápido. Silencio
Silencio **Retorno del valor equivocado** Silencio Mezclando las “transacciones mínimas” contra “grupos máximos de suma cero” – la respuesta correcta es `n - maxZeroGroups`. Silencio
Silencio **Over‐Recursion** Silencio Para la gran `n`, la profundidad de recursión puede alcanzar el límite de pila de Java o el límite de recursión de Python. Un enfoque recursivo o iterativo es más seguro. Silencio

-...

### The Ugly: A Naïve, Time-Out Code

``python
# Ugly, O(n!) Python
def minTransfers(transacciones):
saldos = contado()
for f, t, amt in transactions:
saldos[f] += #
balances[t] -= amt
deudas = [v para v en balances.values() si v]
n = len(debts)
mejor = n
def dfs(i, cur):
no local mejor
si yo == n:
mejor = min(mejor, cur)
Regreso
dfs(i+1, cur+1) # tratar de resolver esta persona solo
para j en rango(i+1, n):
si deudas[i] + deudas [j] == 0:
dfs(i+1, cur) # conformar i with j together
dfs(0, 0)
mejor
`` `

Este código intenta cada posible agrupación de personas. Con `n = 8` puede hacer **40320** llamadas recursivas, y con una pesada contra/ropa de arriba superará el 2 segundo límite en LeetCode. Es *muy* porque parece limpio pero falla en la práctica.

-...

### The Clean, Polished Solution

Los tres idiomas siguientes siguen la *same* estrategia óptima:

1. **Recuperar los saldos** (`de` + `amt`, `a `` - `amt`).
2. **Mantenga solamente deudas no cero** – en la mayoría de `n ≤ 8`.
3. **Bit-mask DP** (`dp[mask]`) almacena el número máximo de grupos de suma cero que podemos colapsar para un subconjunto dado.
4. La respuesta final es " n - dp [1 se hizo]-1] " .

##### Por qué funciona esto

*Todo acuerdo que lleve la suma de un subconjunto a **0** puede resolverse con una sola transacción. Al *maximizar* el número de tales grupos de suma cero, minimizamos las transacciones requeridas. *

La complejidad es **O(2^n · n)** – por `n = 8` que es sólo **512** estados veces un pequeño bucle interno, que es < 1 ms en Java y < 0,5 ms en Python en hardware moderno.

-...

### Complexity Analysis

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Silencio **Java** Silencio **O(2^n · n)** (`n ≤ 8`) Silencio **O(2^n)** para la mesa de memo + `O(n)` la pila de recursión
**Python** Silencio **O(2^n · n)** (cached) Silencio **O(2^n)** para LRU cache Silencio
Silencio **C++** Silencio **O(2^n · n)** (array DP) Silencio **O(2^n)** para vector asignadoint

Debido a que `n` está cubierta a las 8, la solución es prácticamente *instant*.

-...

### Conclusión " Escapadas "

* Cuenta Optimal Balancing es un problema **must‐solve** para cualquier persona que se aplique a los roles de datos o fintech.
* Evite los errores comunes: derrumbe el gráfico, prune agresivamente, utilice la memoización de bitmask y regrese `n - maxZeroGroups`.
* Los tres fragmentos de código anteriores son **clean, testable y lingüístico-agnóstico** – perfecto para agregar a su cartera.

> **Job‐Search Sugerencia**: Pon tus soluciones Java, Python y C++ en un solo repo en GitHub, etiquetalas `leetcode-465`, y añade un pequeño README explicando el algoritmo. El equipo de trabajo ama una solución clara y bien agregada.

Codificación feliz - y que sus entrevistados siempre salgan arriba!