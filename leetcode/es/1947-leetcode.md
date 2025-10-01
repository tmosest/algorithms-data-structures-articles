-...
Título: LeetCode 1947. Compatibilidad máxima Score Sum -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📊 Maximum Compatibility Score Sum – A Complete Guía (Java / Python / C++)

*Descripción* –
Aprende a resolver LeetCode 1947 *Maximum Compatibility Score Sum* en Java, Python y C++.
Obtenga las soluciones completas de backtracking, bit-mask DP, y húngaro-algorithm + un blog amigable de SEO que le ayudará a aterrizar su próxima entrevista tecnológica.

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

■ **Given** dos `m × n` matrices binarias `students` y `mentors`.
■ ** Objetivo:** Pare a cada estudiante con un mentor único para que se maximice la suma de los *puntos de compatibilidad* (número de respuestas iguales).

■ **Constraints**
* `1 ≤ m, n ≤ 8`
* Los elementos son sólo `0` o `1`.

Porque `m ≤ 8`, podemos enumerar todos los pares posibles (`m!` posibilidades).
El desafío es hacerlo de forma limpia, con un buen equilibrio entre legibilidad, velocidad y espacio.

-...

## ## 2down⃣ 3 Popular Approaches

Cómo funciona la Complejidad _ Por qué importa
Silencio--------------------------------------------...
Silencio **Backtracking** tención Recursive DFS + visitada matriz Silencioso `O(m! · n)` ← Super-simple, ideal para la enseñanza ¦
Silencio **Bit-mask DP** Silencio Memoise asignaciones parciales usando un bitmask Silencio `O(2^m · m · n)` ← Optimal for all `m ≤ 8` Silencio
Silencio ** Algoritmo húngaro** Silencio bipartito de coste mínimo que coincida con la vida `O(m3)` ← Tiempo lineal para más grande `m`, pero el código es pesado

■ **El “bien”** – El retroceso es fácil de leer e implementar.
■ **El "Bad"** – Se infla exponencialmente y se dará tiempo para el peor caso.
■ **El “Ugly”** – húngaro es rápido pero se siente como una caja negra y es demasiado para “m ≤ 8”.

-...

## 3VIEW⃣ Code Snippets

A continuación encontrará **tres** soluciones de trabajo completo – una por idioma – para cada uno de los tres enfoques.

■ **Consejo:** El ayudante de `compatibilidad` a continuación es idéntico en los tres códigos.
■ Copialo en tu clase/módulo una vez y llámalo donde lo necesites.

-...

### 3.1 Java

``java
----------- 3.1.1 Ayudante...
puntuación privada (int[] a, int[] b) {
int c = 0;
para (int i = 0; i) a.length; i++) si (a[i] == b) c++;
c) Retorno c;
}
`` `

#### 3.1.2 Backtracking (Easy to Understanding)

``java
Solución de la clase pública {}
int privado mejor;

public int maxCompatibilitySum(int[][] estudiantes, int[][] mentores) {
boolean[] utilizado = nuevo boolean[students.length];
backtrack(students, mentors, 0, 0, used);
devolver mejor;
}

retroceso privado vacío(int[] [] estudiantes, int[] mentores,
int pos, int curScore, boolean[] utilizado) {
si (pos == estudiantes.duración) {}
mejor = Math.max(mejor, curScore);
retorno;
}
para (int j = 0; j)
si (!used[j]) {}
utilizado[j] = verdadero;
backtrack(estudios, mentores, pos + 1,
curScore + score(students[pos], mentores[j]), utilizado);
utilizado[j] = falso;
}
}
}
}
`` `

#### 3.1.3 Bit-mask DP (Optimal for m ≤ 8)

``java
Solución de la clase pública {}
int[][] compatibilidad; // puntuaciones pre-computadas

public int maxCompatibilitySum(int[][] estudiantes, int[][] mentores) {
int m = estudiantes. longitud;
compatibilidad = nuevo int[m][m];
para (int i = 0; i)
para (int j = 0; j)
compatibilidad[i][j] = puntuación(students[i], mentores[j]);

int[] memo = nuevo int[1]
Arrays.fill(memo, -1);
dp(0, memo);
}

int privado dp(mascarada, int[] memo) {
int i = Integer.bitCount(mask); // qué estudiante asignar el siguiente
si (i == memo.length) retorno 0; // todos asignados
si (memo[mask] != -1) memo de retorno;

int best = 0;
para (int j = 0; j) {}
si (mask) == 0) {
mejor = Math.max(mejor,
compatibilidad[i][j] + dp(mask tención (1  obtenidos j), memo));
}
}
devolver memo[mask] = mejor;
}
}
`` `

-...

#### 3.2 Python

``python
#---------- 3.2.1 Ayudante--------------
def score(a, b):
volver suma(x == y para x, y en zip(a, b))
`` `

##### 3.2.2 Backtracking (Easy to Understanding)

``python
Solución de clase:
def maxCompatibilitySum(self, students: List[List[int]], mentores: List[List[int]]) - título int:
self.best = 0
utilizado = [False] * len(students)
auto.dfs(estudiantes, mentores, 0, 0, utilizados)
Vuélvete. lo mejor

def dfs(self, students, mentores, pos, cur, used):
si pos == len(students):
auto.best = max(self.best, cur)
Regreso
para j en rango(len(mentors)):
si no se usa[j]:
utilizado[j] = Verdadero
auto.dfs(estudiantes, mentores, pos+1,
cur + puntuación(students[pos], mentores[j]), utilizado)
utilizado[j] = Falso
`` `

##### 3.2.3 Bit-mask DP (Optimal)

``python
Solución de clase:
def maxCompatibilitySum(self, students: List[List[int]], mentores: List[List[int]]) - título int:
n = len(students)
compat = [[score(s, m) for m in mentors] for s in students]

@lru_cache(None)
def dfs(mask):
i = bin(mask).count('1') # siguiente estudiante
si yo == n: retorno 0
mejor = 0
para j en rango(n):
si no (mask >
mejor = max(best, compat[i][j] + dfs(mask TENIDO (1 ANTE)
mejor

devolver dfs(0)
`` `

-...

### 3.3 C++

``cpp
--------- 3.3.1 Ayudante...
int score(cont vector seleccionado), const vector conectado
int c = 0;
para (int i = 0; i) b[i]) + c;
c) Retorno c;
}
`` `

##### 3.3.2 Backtracking

``cpp
Clase Solución {
public:
int maxCompatibilidadSum(vector seleccionadovector seleccionador)
vectores seleccionados:
m = estudiantes.size();
mejor = 0;
us.assign(m, false);
backtrack(estudios, mentores, 0, 0);
devolver mejor;
}

privado:
int m, best;
vector utilizado;

retroceso de vacío(cont vectorial)vector s,
const vector identificadovector seleccionado,
int pos, int cur) {
(pos == m) { best = max(best, cur); return; }
para (int j = 0; j)
si (!used[j]) {}
utilizado[j] = verdadero;
backtrack(s, mnt, pos+1, cur + score(s[pos], mnt[j]);
utilizado[j] = falso;
}
}
}
};
`` `

#### 3.3.3 Bit-mask DP

``cpp
Clase Solución {
public:
int maxCompatibilidadSum(vector seleccionadovector seleccionador)
vectores seleccionados:
n = estudiantes.size();
compat.assign(n, vector implicaint(n));
para (int i = 0; i)
para (int j = 0; j)
compat[i][j] = score(students[i], mentores[j]);

dp.assign(1) se realizó n, -1);
(0);
}

privado:
int n;
vector de vectores compás;
vector dp;

int solve(int mask) {
int i = __constructionin_popcount(unsigned)mask); // next student
si (i == n) retorno 0;
si (dp[mask] != -1) retorno dp[mask];

int best = 0;
para (int j = 0; j)
si (!(mask " (1 iere escrito j)))
mejor = max(best, compat[i][j] + solve(mask TENIDO (1  Se hizo referencia j));
dp[mask] = mejor;
}
};
`` `

-...

## 4VIEW⃣ Complexity Analysis

Silencio Silencio Silencio Silencio Silencio
Silencio--------------------------------
Silencioso Backtracking Silencio `O(m! · n)` Silencio `O(m)` (recursion stack) Silencio rápido para minúscula `m`, poco práctico para 8! = 40320 Silencio
← Bit‐mask DP Silencio `O(2^m · m · n)` Silencio `O(2^m)` Silencio Con `m = 8` → `256 · 8 · 8 = 16k` ops
Silencio en Hungría TENIDO Scales a `m = 500` fácilmente pero sobrematizado aquí TENIDO

Porque `m ≤ 8`, **Bit-mask DP** es el lugar dulce: es rápido, utiliza poca memoria, y todavía es legible.

-...

## 5down El bueno, el malo, el ugly

### The Good
* **Backtracking** es *instantaneamente comprensible*—usted literalmente intenta cada asignación.
* Es perfecto para *entrevistas educativas* donde el entrevistador quiere ver su lógica primero.

### El malo
* Soplamiento exponencial: incluso en `m = 8`, la recursión explora 40320 ramas.
* Para más *estrés-test* o casos de prueba ocultos, el DFS puede *timeout*.

### El Ugly
* **Hungríano** se siente como un “buttón mágico”: el algoritmo funciona, pero la implementación es un laberinto **10-línea**.
* Para los entrevistadores que ven la “notación de estrellas algorítmicas”, puede *evaluar las cejas* y *matar su puntaje de legibilidad*.

### The Ugly‐but‐Fast
* Cuando `m` salta más allá de 10, **Bit-mask DP** comienza a convertirse en memoria-hungry (`2^10 = 1024` todavía bien, pero `2^20 = 1.048,576` comienza a estirarse).
* Usted cambiaría a *Hungariano* o *Min‐Cost Max‐Flow* en esos casos, pero esas bibliotecas vienen con * costos de configuración más altos* (incluyendo un buen contenedor C++ STL o una biblioteca de terceros).

-...

## 6down Consejos de uso del mundo real

1. ** Partituras de pre-compute** – `compatibilidad[i][j]` una vez, utilizar en todas partes.
2. **Memoización con bitmask** – `dp[mask]` en Java/C++ o `lru_cache` en Python.
3. **Iterate sobre bits** – `for (int j = 0; j ' no; ++j) si (!(mask " (1 " identificado j)))) " en C++; use `itertools.combinations ' or bit tricks in Python.
4. **Edge Cases** – El código ya los maneja: `m = 1`, `n = 1`, etc.

-...

## 7Ω⃣ Interview‐Ready Checklist

1. **Entender el problema** – articular que estás emparejando gráficos bipartitos con una matriz de costes.
2. **Elige el algoritmo adecuado** – explica por qué Bit-mask DP es preferible para `m ≤ 8`.
3. **Write clean code** – use helper functions, comment your loops, and keep variable names expressive.
4. **Prueba la muestra**, por ejemplo.
``python
s = [[0,1],[1,0]
m = [[1,0],[0,1]]
print(Solution().maxCompatibilidadSum(s, m)) # → 4
`` `
5. **Explicar complejidad** – mostrar el cálculo de back-of-the-envelope para convencer al entrevistador.

-...

## 8down Bono: Una aplicación húngara de peso ligero (opcional)

Si usted está interesado en ver una rápida implementación húngara (trabajos para todos `m`), el siguiente Python snippet es conciso y completamente escrito:

``python
clase Húngaro:
def __init__(self, cost): # cost[i][j] es la pena (más alto es peor)
self.n = len(cost)
self.u = [0] * (self.n+1)
self.v = [0] * (self.n+1)
self.p = [0] * (self.n+1)
auto.way = [0] * (self.n+1)
auto.cost = costo

def min_cost(self):
para i en rango(1, auto.n+1):
self.p[0] = i
minv = [float('inf')] * (self.n+1)
utilizado = [False] * (self.n+1)
J0 = 0
Mientras Verdadero:
utilizado[j0] = Verdadero
i0 = self.p[j0]
delta, j1 = carro('inf'), 0
para j en rango(1, auto.n+1):
si no se usa[j]:
cur = self.cost[i0-1][j-1] - self.u[i0] - self.v[j]
si se curan los minv[j]:
minv[j], self.way[j] = cur, j0
si minv[j]
delta, j1 = minv[j], j
para j en rango(self.n+1):
si se usa[j]:
auto.u [self.p[j] += delta
self.v[j] -= delta
más:
minv[j] -= delta
j0 = j1
si auto.p [j0] == 0:
descanso
Mientras Verdadero:
j1 = self.way[j0]
self.p[j0] = self.p[j1]
j0 = j1
si j0 == 0:
descanso
# Resultado
match = [-1]*self.n
para j en rango(1, auto.n+1):
si auto.p[j] != 0:
match[self.p[j]-1] = j-1
total = sum(self.cost[i][match[i]] para i in range(self.n))
total
`` `

■ **Pero** para `m ≤ 8` esto es *necesario*.

-...

## 6down W Wrap‐Up & Next Steps

1. Elija **Bit-mask DP** para la solución de entrevista final.
2. Mantenga la 'compatibilidad' pre-computación; es lo mismo para todos los idiomas.
3. Prepárate para *explicar* por qué eligió DP sobre DFS.
4. Casos de borde de práctica (por ejemplo, todos los ceros, todos ellos, `m = n = 8`).

-...

### Bonus Resources

← Recurso Silencio Idioma Silencio Lo que aprenderás
Silencio------------------------------
Silencio [LeetCode 1772 Discusión – Bit-mask DP](https://leetcode.com/problems/maximize-compatibility-score/discuss/2514872/JavaC%2BPython-Backtracking-Bitmask-DP) Silencio Todo TEN Clean DP code, 3-minute explanation TEN
Silencio [GeeksForGeeks – Húngaro Algorithm](https://www.geeksforgeeks.org/hungarian-algorithm-for-assignments-problem/) TEN TO TO TO TO TO TO TO TO TO TO TODO TEN tutorial completo con matricidad paso a paso

-...

## 7 carreras Final Takeaway

- Para LeetCode **1772** (o cualquier bipartito que coincida con `m ≤ 8`), **Bit-mask DP** es la solución ganadora.
- Mantenga el código **clean** – partituras pre-compute una vez, mezclar con 'int[]`/`lru_cache`.
- En una entrevista, *explicar* su elección: * “Usamos DP con una máscara de 8 bits porque 28 = 256 estados; es tanto rápido como fácil de entender.”*

¡Buena suerte! 🚀
Siéntete libre de dejar las preguntas en los comentarios o en tu foro elegido. ¡Feliz codificación! 👩 💻👨

-...


-...

*End of article*
-...
Esto completa la guía completa.