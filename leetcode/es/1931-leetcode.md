-...
Título: LeetCode 1931. Pintura a la plancha con tres colores diferentes -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🎯 Leetcode 1931 – *Painting a Grid with Three Different Colors*
## The Good, the Bad, and the Ugly - A Job‐Entreview Friendly Blog Post

■ **SEO Palabras clave**: Leetcode 1931, cuadro con tres colores diferentes, DP, Bitmask DP, Grid Coloring, Coding Interview, Java solution, Python solution, C++ solution, entrevista prep, algoritmos, programación dinámica, desafío de codificación

-...

## 1. Panorama general de los problemas

TENIDO ANTERIOR ANTERIOR Descripción
Silencio...
confidencialidad **Título** Silencioso Pintura a la plancha con tres colores diferentes
Silencioso**
Silencio **Dificultad**
Silencioso **Constraints** Ø 1 ≤ *m* ≤ 5, 1 ≤ *n* ≤ 1000 tención
Silencio ** Objetivo** Silencio Contar cuántas formas de pintar un *m* × * n* rejilla con 3 colores (rojo, verde, azul) de tal manera que ** ninguna dos células adyacentes ortogonalmente comparten el mismo color**. Silencio
Silencio **Respuesta Mod** Silencio 109 + 7

*Por qué este problema es digno de entrevista*

* Pruebas **state‐compression DP** (bitmasking) – un elemento básico para muchas entrevistas de alto nivel.
* Te desafía a pensar en **horizontal vs. vertical adjacency** por separado.
* Escala con *n* hasta 1000, obligando a subir con una solución *O(n · K2)* donde *K* es el número de estados de columna válidos (≤ 81 para *m* = 5).

-...

## 2. Intuición " Estrategia de Alto Nivel "

1. **Treat columns as the DP dimension** – procesamos la columna de rejilla por columna.
2. **Generar todos los estados de columna válidos** (`state`) tal que no dos filas consecutivas en la misma columna comparten el mismo color. Para *m* = 5, el recuento es en la mayoría de 35 = 243, pero los conflictos verticales lo reducen a 81.
3. ** Determinar la compatibilidad entre los estados** – dos estados `A` y `B` pueden sentarse lado a lado si por cada fila `i ' , `A[i]` ل `B[i]` (no hay conflicto horizontal).
4. * Programación dinámica*
* `dp[0][s] = 1` para cada estado válido `s` (primera columna).
* Transición:
``text
dp[col][next] += dp[col‐1][prev] si prev y siguiente son compatibles
`` `
* Todos los cálculos se realizan modulo `MOD`.
4. **Respuesta** – resumir todo `dp[n‐1][s]` para la última columna.

■ **El “bien”** – El problema naturalmente se descompone en un espacio de estado *finito*; nunca es necesario sembrar sobre toda la red.
■ **El “Bad”** – Si generas ingenuamente todas las posibilidades 3n para cada célula, el tiempo explota.
■ ** El “Ugly”** – La sutileza de los conflictos *vertical* separados de los conflictos *horizontal* pueden hacer tropezar a muchas personas. La clave es codificar cada columna como un entero único (bitmask) para mantener transiciones O(K2).

-...

## 3. Algoritm detallado

### 3.1. Codificación de una columna

- Representar el color de cada fila con 2 bits (`00` = rojo, `01` = verde, `10` = azul).
- Para *m* ≤ 5, la columna encaja en un entero de 10 bits (5 × 2).
- Una columna `mask` es *válida* si para todo `row` > 0, los dos bloques de 2 bits difieren.

### 3.2. Building Compatibility List

- Para cada par de máscaras válidas `(maskA, maskB)`:
- Son **compatibles** si `(maskA " 0x3) √ (maskB " 0x3) " para la fila más baja, `(maskA  confidencial 2 " 0x3) √ (maskB но 2 " 0x3) " para la segunda fila, etc.
- Almacenar `maskB` en un vector de transiciones compatibles para `maskA`.
- Complejidad: *(K2)*, K ≤ 81.

### 3.3. DP Across Columns

`` `
dp[0][s] = 1 // primera columna
para col = 1 .. n-1:
para prev en Estados válidos:
para el próximo en las transiciones[prev]:
dp[col][next] = (dp[col] [next] + dp[col-1][prev] % MOD
`` `

Por último, `respuesta = bah dp[n-1][s]` para todos `s`.

-...

## 4. Análisis de la complejidad

TEN ANTE TEN ANTE Fórmula TENIDO Para *m* = 5 TENIDO Explicación
Silencio--------------------------------------------------------------
Silencio **K (estados)** Silencio 3m – conflictos verticales Ø 81 Silencio Todas las 35 posibilidades menos aquellas con iguales colores consecutivos. Silencio
Silencio **Hora** Silencioso `O(n · K2)` Silencio ~ 1000 · 812 ♥ 6.5 M ops Silencio Dominated by the transition laops. Silencio
Silencio **Espacio** Silencio `O(K)` Silencio ~ 81 enteros por columna Silencio Sólo podemos mantener los arrays actuales y anteriores de la columna DP. Silencio

-...

## 5. Aplicación del Código

■ **Tip for interviews**: Mostrar un solo pase de DP con *O(K)* espacio, pero mantener el código legible.

### 5.1. Java 17 (Fastest readable)

``java
importar java.util*;

Solución de la clase pública {}
int final estático privado MOD = 1_000_000_007;

int colorTheGrid(int m, int n) {
Lista Nombramiento NombradoInteger = nuevo ArrayList implicado();
// Generar todas las máscaras de columna válidas
para (enmascarado = 0; máscaras) {}
si (esValidColumn(mask, m)) estados.add(mask);
}

/ / Pre-compute compatibility
Lista realizadaLista realizadaInteger título = nuevo ArrayList recomendado();
para (int i = 0; i) i++) {
Lista de títulos = nuevo ArrayList implicado();
para (int j = 0; j) determinados estados.size(); j++) {
si (esCompatible(states.get(i), states.get(j), m))
list.add(states.get(j));
}
compat.add(list);
}

// DP
long[] prev = new long[states.size()];
Arrays.fill(prev, 1); // primera columna

para (incluido el col = 1; col) {}
long[] next = new long[states.size()];
para (int i = 0; i) i++) {
largos caminos = prev[i];
si 0) continuar;
para (int nb : compat.get(i)) {}
int idx = states.indexOf(nb);
siguiente[idx] = (next[idx] + maneras) % MOD;
}
}
prev = siguiente;
}

// Sum
ans largas = 0;
(long v : prev) ans = (ans + v) % MOD;
retorno (int) ans;
}

booleano privado esValidColumn(inta máscara, int m) {
int prev = -1;
para (int r = 0; r)
int color = (mask ≤ = (2 * r)) " 3; // 0=red,1=green,2=blue
si (color == prev) devuelve falso;
prev = color;
}
retorno verdadero;
}

booleano privado esCompatible(int a, int b, int m) {}
para (int r = 0; r)
int ca = (a нелиме (2 * r)) " 3;
int cb = (b < > > >
si (ca == cb) devuelve falso;
}
retorno verdadero;
}
}
`` `

■ **Por qué este código Java gana**
* Usos primitivos `int` bitmask – sin boxeo sobrehead.
* Mantiene la huella de memoria mínima (`states.size()` ≤ 81).
* Demuestra la separación limpia de *generación* (`isValidColumn`) y *transición* (`isCompatible`).

-...

### 5.2. Python 3 (Clean & Pythonic)

``python
MOD = 1_000_000_007

Solución de clase:
def color TheGrid(self, m: int, n: int) - int:
# 1 Generar todas las máscaras de columna válidas
def gen(row, prev, mask):
si fila == m:
estados.append(mask)
Regreso
para col en rango(3): # 0,1,2 para R,G,B
si hilera  título 0 y (mask  títulos) (2*(row-1))) " 3 == col:
continuar
gen(row+1, col, mask TENED (col ANTE)

estados = []
gen(0, -1, 0)

# 2⃣ Transiciones pre-computadas
comp = {s: [] for s in states}
para un en estados:
para b en estados:
si todo(((a не (2*i)) " 3) != ((b  título título(s) (2*i)) " ) para i en rango(m)):
comp[a].append(b)

# 3️ DP across columns
dp = {s: 1 para s en estados} # primera columna
para _ en rango(1, n):
nuevo
para prev, maneras en dp.items():
para nxt en comp[prev]:
nuevo[nxt] = (new.get(nxt, 0) + maneras) % MOD
dp = nuevo

# 4️ Respuesta de su madre
(dp.values()) % MOD
`` `

■ **Python-specific highlights**
* Generador Recursivo es pequeño – no hay bibliotecas externas.
* Usa el diccionario para DP; todavía O(K2) transiciones.
* Mantiene el uso de la memoria pequeña – sólo dos diccionarios a la vez.

-...

### 5.3. C+17 (Lo más posible)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
static constexpr int MOD = 1'000'007;

color int TheGrid(int m, int n) {
--------- 1. Construir todos los estados de columna válidos --------
vectoriales indicativos;
para (incluido máscara = 0; mascarilla) = (1 > ) {
si (validColumn(mask, m)) estados.push_back(mask);
}

--------- 2. Compatibilidad pre-compute ----------
vector seleccionado());
para (int i = 0; i) ++i) {
para (int j = 0; j ' ilse (int)states.size(); ++j) {
si (compatible(estados[i], estados[j], m)
trans[i].push_back(j);
}
}

--------- 3. DP a través de las columnas--------
vector implicado dp(states.size(), 1), ndp(states.size(), 0);
para (int col = 1; col)
fill(ndp.begin(), ndp.end(), 0);
para (int i = 0; i) ++i) {
si (!dp[i]) continúan;
para (int j : trans[i]) {}
ndp[j] = (ndp[j] + dp[i]) % MOD;
}
}
dp.swap(ndp);
}

--------- 4. Sum up ----------
int ans = 0;
para (int x : dp) ans = (ans + x) % MOD;
devolver los ans;
}

privado:
bool válido Columna(enmascarado, int m) const {
int prev = -1;
para (int r = 0; r) {}
int col = (mask  confidencial (2 * r)) " 3;
si (col == prev) vuelve falso;
prev = col;
}
retorno verdadero;
}

bool compatible(int a, int b, int m) const {
para (int r = 0; r) {}
int ca = (a нелиме (2 * r)) " 3;
int cb = (b < > > >
si (ca == cb) devuelve falso;
}
retorno verdadero;
}
};
`` `

■ **Por qué esta solución C++ supera**
* Usos `vector fielint `` – memoria contigua, amigable con cache.
* `trans` as adjacency list → O(K2) but only integer indices.
* Constante `MOD` – operación inline mod es muy barato.

-...

## 6. Qué hacer hincapié en las entrevistas

1. ** Reducción del espacio estatal** – Mostrar cómo la codificación de una columna en un bitmask reduce el problema a los estados 'K'.
2. **Transition Pre-computation** – Clarify that compatibility is independent of column index, enabling reuse across all `n` columns.
3. ** Optimización del espacio** – Mantenga sólo dos filas de DP (prev`, `next`) en lugar de `n` matrices completas.
4. ** Aritmética Modular** – Todas las sumas deben ser modulo `MOD` (caso importante de borde).
5. ** Casos Edge** - ¿Cuándo `n == 0`? (aunque las limitaciones dicen `n ≥ 1`).
6. **Testing** – Verificar en casos de muestra, por ejemplo, `m=2, n=3 → 18`.

-...

## 7. Pensamientos finales

■ **En resumen**:
■ *Aprobar el espacio pequeño del estado, codificar columnas con bitmasks, precomputar transiciones compatibles, y ejecutar un DP simple. *

■ ** Estrategia de Intervisión* *
* Habla primero a través de la descomposición del problema.
* Mostrar la generación del estado y la lógica de compatibilidad.
* Entonces explique la transición del DP.
* Fin con la suma final.

Con esta estructura, usted demuestra tanto un **conceptual** captación y **practical** implementación – la combinación ganadora para cualquier entrevista de codificación.

-...

### 8. Lectura adicional " Problemas similares

- **"Número de maneras de llenar un rayo con K Integers"** (LeetCode 1106) – similar state-based DP.
- ** "Colorful Stones"** - programación dinámica sobre pechugas.
- **" Coloración árida con retratos"** – combinatoria avanzada con DP.

■ ¡Feliz codificación!

-...

■ *Si quieres caminar paso a paso a través de las conversiones bit-mask, no dudes en preguntar. ¡Feliz entrevista! *

-...
**Keywords**: `LeetCode 1106`, `Grid coloring`, `Bitmask DP`, `Java`, `Python`, `C++`, `Dynamic Programming`, `Combinatorics`.