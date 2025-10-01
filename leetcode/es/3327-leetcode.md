-...
Título: LeetCode 3327. Compruebe si las cuerdas DFS son Palindromes -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Artículo del Blog – “El Bien, el Mal, y el Ugly of **LeetCode 3327**”

#### TL;DR
LeetCode 3327 le pide que decida, por cada nodo en un árbol arraigado, si la cadena producida por un **post-order DFS** es un palindromo.
La solución “fácil” que simplemente reconstruye la cuerda para cada nodo es **O(n2)** y pasará tiempo fuera en el límite 105.
La solución más rápida aceptada utiliza ** post-order traversal + doble roll-hash** para probar palindromas en **O(n)** tiempo y **O(n)** memoria – la parte “buena”.
La parte “mala” es la sutileza de manejar el orden inverso correctamente.
¿La parte “muy”? Un par de “números mágicos” (dos primeros moduli) y la necesidad de precomputar poderes – pero esos son trucos comunes que aprenderás a amar.

■ **Palabras clave de SEO**: *Leetcode 3327, Check if DFS Strings Are Palindromes, Tree Palindrome DFS, Java solution, Python solution, C+ solution, Rolling hash, Palindrome detection, Interview prep, Algorithmic interview, Tree traversal, Post-order DFS, Complexity analysis*

-...

### 1. Panorama general de los problemas

`` `
Entrada:
parent[0...n-1] (parent[0] = -1, todos los demás padres [i]
s[0...n-1] (cartas menores)

Definición:
dfs(x):
para cada niño y de x en orden creciente
dfs(y)
append s[x] to a global string dfs Str

Tareas:
Por cada nodo i, empezar con un dfsStr vacío, llamar dfs(i), y establecer
respuesta[i] = verdadero sif el df resultante Str es un palindromo.

Limitaciones: 1 ≤ n ≤ 105
`` `

### 2. Intuición

La cadena producida por `dfs(v)` es exactamente:

`` `
S(v) = S(child1) + S(child2) + ... + S(childk) + s[v]
`` `

donde los niños son atravesados en ** orden creciente**.
Una prueba de palindromo para `S(v)` normalmente nos requeriría construir toda la cuerda para cada nodo – **O(n2)** – que es imposible para n = 105.

La observación clave:
**Podemos computar un hash delantero y un hash inverso de cada `S(v)` en un pase de abajo arriba. #
Si los dos hashes coinciden (para dos moduli diferentes), `S(v)` es un palindromo con probabilidad astronómicamente baja de colisión.

##### Adelante.
`` `
H_f(v) = (( ( H_f(child1) * P^{len(child1)} + H_f(child2) ) * P^{len(child2)} + ... ) * P + code(s[v]
`` `

##### Hacha inversa
The reverse of `S(v)` es
`` `
inverso(S(v) = s[v] + inverso(S(childk) + inverso(S(child1))
`` `
Así que debemos construir el hash en el orden del niño **reverso**:

`` `
H_r(v) = ( code(s[v]) * P^{len(childk)} + H_r(childk) ) * P^{len(childk-1)} + H_r(childk-1) ) ...
`` `

Ambos hashes también requieren la longitud exacta de la cuerda en cada nodo (`len[v]`) y poderes de la base `P`.

-...

### 3. Naïve Approach ( Why It Fails)

``python
def dfs(v):
para niños[v]:
dfs(child)
re.append(s[v])

def solve():
ans = [False]* n
para v en el rango(n):
res.clear()
dfs(v)
ans[v] = res == res[:-1] # reconstruir & reverse
`` `

*Tiempo*: `O(explotación permanenteS(v)
*Memoria*: O(n) por llamada – la recursión de pila explotará en Java o C++.

** Resultado**: TLE en pruebas duras medias.
Así que debemos hacer algo más inteligente.

-...

### 4. Enfoque optimizado - O(n) con malla de doble rollo

Silencio Qué computar Silencio Por qué
Silencio...
← Construir la lista de adyacency Silenciosos listas de niños Silencio Necesitado para la traversal
Silencio Post-order DFS (bottom-up)
Silencio Compare hashes (mod1 > mod2) Silencioso `respuesta[v] `` examen de Palindrome

#### Pre-computation

`` `
P1 = 911382323, MOD1 = 1_000_000_007
P2 = 972663749, MOD2 = 1_000_000_009
pow1[i] = P1^i (mod MOD1)
pow2[i] = P2^i (mod MOD2)
`` `

Pre-compute potencias hasta n para que la combinación de la hash de un niño sólo necesita una sola multiplicación y adición.

#### Fórmula de fondo (para adelante)

`` `
val = 0
para niños[v] # Aumentando el orden
val = (val * pow1[len[child]] + H_f[child] % MOD1
val = (val * pow2[len[child]] + H_f[child] % MOD2

val = (val * P1 + code(s[v]) % MOD1
val = (val * P2 + code(s[v]) % MOD2

H_f[v] = val
`` `

#### Bottom‐up formula (reverse)

`` `
val = 0
val = (código(s[v]) * 1) % MOD1
val = (código(s[v]) * 1) % MOD2

para niños invertidos(niños[v]): # orden inverso
val = (val * pow1[len[child]] + H_r[child] % MOD1
val = (val * pow2[len[child]] + H_r[child] % MOD2

H_r[v] = val
`` `

* Nota*: `código(ch)` es simplemente `ord(ch) - ord('a') + 1`.

#### Palindrome check

`` `
respuesta[v] = (H_f[v] == H_r[v]) # ambos pares modulo deben coincidir
`` `

-...

### 5. Detalles de la aplicación

A continuación se muestran **ready‐to‐paste** soluciones en **Java, Python, y C++**.
Todos utilizan el mismo esqueleto algoritmo: construir el árbol, poderes pre-compute, realizar un *iterative* post-order DFS, luego comparar los dos hashes.

■ **Importante** – usamos moduli *dos* para mantener la probabilidad de colisión insignificante.
■ El código está fuertemente comentado para que puedas entender cada paso sin la necesidad de “ingeniero reverso” más adelante.

-...

#### 5.1 Java (Java 17)

``java
importa java.io.*;
importar java.util*;

Solución de la clase pública {}
static final long MOD1 = 1_000_000_007L;
static final long MOD2 = 1_000_000_009L;
privada estática final larga BASE1 = 9113823L; // cualquier prima al azar
privada estática final larga BASE2 = 972663749L; // cualquier prima al azar

public static void main(String[] args) tira IOException {
FastScanner fs = nuevo FastScanner (System.in);
int n = fs.nextInt();
int[] parent = nuevo int[n];
para (int i = 0; i) no; i++) padre [i] = fs.nextInt();
char[] s = fs.next().toCharArray();

// 1. Construir listas de niños
Lista realizadaInteger() g = nuevo ArrayList[n];
para (int i = 0; i) no; i++) g[i] = nuevo ArrayList recomendado();
para (int i = 1; i) no; i++) g [parente [i].add(i);
para (int i = 0; i) Collections.sort(g[i]);

// 2. Pre-compute powers
long[] pow1 = new long[n + 1];
long[] pow2 = new long[n + 1];
pow1[0] = pow2[0] = 1;
para (int i = 1; i) = n; i++) {
pow1[i] = (pow1[i - 1] * BASE1) % MOD1;
pow2[i] = (pow2[i - 1] * BASE2) % MOD2;
}

// 3. Suboficial iterante
int[] len = new int[n];
long[] hf1 = new long[n], hf2 = new long[n];
long[] hr1 = new long[n], hr2 = new long[n];
boolean[] visited = new boolean[n];
Deque cumplióInteger confianza stack = nuevo ArrayDeque correspondió();
stack.push(0);

mientras (!stack.isEmpty()) {}
int v = stack.peek();
si (!visited[v]) {}
visitado[v] = verdadero;
para (incluido niño : g[v]) stack.push(niño);
. ♫ ... {
stack.pop();
// longitud de computación
int total = 1;
para (incluido niño : g) total += len[child];
len[v] = total;

// forward hash
f1 = 0, f2 = 0;
para (incluido niño : g[v]) {}
f1 = (f1 * pow1[len[child]] + hf1[child]) % MOD1;
f2 = (f2 * pow2[len[child]] + hf2[child]) % MOD2;
}
f1 = (f1 * BASE1 + (s[v] - 'a' + 1)) % MOD1;
f2 = (f2 * BASE2 + (s[v] - 'a' + 1)) % MOD2;
hf1[v] = f1; hf2[v] = f2;

// reversa
largo r1 = (s[v] - 'a' + 1) % MOD1;
largo r2 = (s[v] - 'a' + 1) % MOD2;
para (int i = g[v].size() - 1; i ю= 0; i--) {
int child = g[v].get(i);
r1 = (r1 * pow1[len[child]] + hr1[child]) % MOD1;
r2 = (r2 * pow2[len[child]] + hr2[child]) % MOD2;
}
hr1[v] = r1; hr2[v] = r2;
}
}

// 4. Construir respuesta
StringBuilder out = nuevo StringBuilder();
para (int i = 0; i)
boolean ok = (hf1[i] == hr1[i]) " sensible (hf2[i] == hr2[i]);
fuera.append(ok? "verdad" : "falso");
si (i + 1 0) fuera.append('');
}
System.out.println(out);
}

Escáner rápido...
Clase privada estática FastScanner {}
InputStream final privado;
byte final privado[] buffer = nuevo byte[1]
int ptr privado = 0, len = 0;
FastScanner(InputStream in) { this.in = in; }
int readByte() lanza IOException {
si
len = in.read(buffer);
ptr = 0;
si (len len= 0) retorno -1;
}
búfer de retorno[ptr+];
}
int nextInt() lanza IOException {
int c, sign = 1, val = 0;
mientras ((c = readByte())) se hacía= ' '') si (c == -1) retorno -1;
(c == '-') { sign = -1; c = readByte(); }
mientras (c > '') { val = val * 10 + c - '0'; c = readByte(); }
retorno val * signo;
}
La cuerda siguiente() lanza IOException {
StringBuilder sb = nuevo StringBuilder();
int c;
mientras ((c = readByte())) se hacía= ' '') si (c == -1) volver nulo;
c) { sb.append(char) c); c = readByte(); }
devolver sb.toString();
}
}
}
`` `

-...

#### 5.2 Python

``python
importadores
de las colecciones importan defaultdict, deque

MOD1 = 1_000_000_007
MOD2 = 1_000_000_009
BASE1 = 911382323
BASE2 = 972663749

def solve():
data = sys.stdin.read().strip().split()
iter(data)
n = int(next(it)))
parent = [int(next(it))) for _ in range(n)]
s = list(next(it)))

# Build tree
g = [[] for _ in range(n)]
para i en rango(1, n):
g[parent[i]].append(i)
para lst en g:
lst.sort()

# Pre-compute powers
pow1 = [1]*(n+1)
pow2 = [1]* (n+1)
para i en rango(1, n+1):
pow1[i] = (pow1[i-1] * BASE1) % MOD1
pow2[i] = (pow2[i-1] * BASE2) % MOD2

# Bottom‐up DFS
lenv = [0]*n
hf1 = [0]*n; hf2 = [0]*n
hr1 = [0]*n; hr2 = [0]*n
visitados = [False]*n
pila = [0]
mientras que la pila:
v = pila[-1]
si no es visitado[v]:
visitado[v] = Verdadero
para c en g[v]: stack.append(c)
más:
stack.pop()
total = 1
para c en g[v]: total += lenv[c]
lenv[v] = total

# forward hash
f1, f2 = 0, 0
para c en g [v]:
f1 = (f1 * pow1[lenv[c] + hf1[c] % MOD1
f2 = (f2 * pow2[lenv[c] + hf2[c] % MOD2
f1 = (f1 * BASE1 + (ord(s[v]) - 96) % MOD1
f2 = (f2 * BASE2 + (ord(s[v]) - 96) % MOD2
hf1[v], hf2[v] = f1, f2

# Inverso hash
r1, r2 = (ord(s[v]) - 96) % MOD1, (ord(s[v]) - 96) % MOD2
para c invertida(g[v]):
r1 = (r1 * pow1[lenv[c] + hr1[c] % MOD1
r2 = (r2 * pow2[lenv[c] + hr2[c] % MOD2
hr1[v], hr2[v] = r1, r2

ans = [ (hf1[i]==hr1[i] y hf2[i]==hr2[i]) para i in range(n) ]
print(' '.join('true' if x else 'false' for x in ans))

si __name_ == "__main__":
solve()
`` `

-...

#### 5.3 C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

const long long MOD1 = 1'000'007LL;
const long long MOD2 = 1'000'000'009LL;
const long long BASE1 = 9113823LL; // random prime
const long long long BASE2 = 972663749LL; // random prime

int main() {}
ios::sync_with_stdio(false);
cin.tie(nullptr);

int n;
si (!(cin  título n)) devuelve 0;
vector:
para (int i = 0; i) parent[i];
string str; cin нелими str;
vector significación de caracteres (str.begin(), str.end());

// Lista de niños
vector realizador:
para (int i = 1; i)
para (int i = 0; i) no; ++i) sort(g[i].begin(), g[i].end());

// Potencias precomputadas
vector obtenidos largamente largas puw1(n + 1, 1), pow2(n + 1, 1);
para (int i = 1; i) = n; ++i) {}
pow1[i] = (pow1[i-1] * BASE1) % MOD1;
pow2[i] = (pow2[i-1] * BASE2) % MOD2;
}

// Subtítulo iterativo DFS
vector:
vector realizado largamente hf1(n), hf2(n), hr1(n), hr2(n);
vector:
vector identificador pila = {0};

mientras (!stack.empty()) {}
int v = stack.back();
si (!vis[v]) {}
vis[v] = verdadero;
for (int child : g[v]) stack.push_back(child);
. ♫ ... {
stack.pop_back();
int total = 1;
para (incluido niño : g) total += len[child];
len[v] = total;

// forward hash
f1 largo = 0, f2 = 0;
para (incluido niño : g[v]) {}
f1 = (f1 * pow1[len[child]] + hf1[child]) % MOD1;
f2 = (f2 * pow2[len[child]] + hf2[child]) % MOD2;
}
f1 = (f1 * BASE1 + (s[v] - 'a' + 1)) % MOD1;
f2 = (f2 * BASE2 + (s[v] - 'a' + 1)) % MOD2;
hf1[v] = f1; hf2[v] = f2;

// reversa
largo largo r1 = (s[v] - 'a' + 1) % MOD1;
largo largo r2 = (s[v] - 'a' + 1) % MOD2;
for (int i = (int)g[v].size() - 1; i √≥= 0; --i) {
int child = g[v][i];
r1 = (r1 * pow1[len[child]] + hr1[child]) % MOD1;
r2 = (r2 * pow2[len[child]] + hr2[child]) % MOD2;
}
hr1[v] = r1; hr2[v] = r2;
}
}

// Producto
para (int i = 0; i) {}
bool ok = (hf1[i] == hr1[i]) " sensible (hf2[i] == hr2[i]);
cout se hizo (ok ? "true" : "false")
}
}
`` `

-...

### 6. Análisis de la complejidad

Silencioso Operación Silencioso Complejidad del tiempo Silencio
Silencio----------------
TENIDO Árbol de construcción TENIDO `O(n)` Silencio
Silencioso poder pre-calc Silencio
Silencio Iterative post-order DFS Silencio `O(n)` Silencio `O(n)` (arrays)
Silencio Respuesta final Silencio

En general: **`O(n)` tiempo, `O(n)` memoria** – bien dentro de los límites de 105 nodos.

-...

### 7. Resumen

- **Problema**: Determinar si la cadena DFS de cada nodo es un palindrome.
- **Naïve**: O(n2) – falla.
- **Optimized**: Use *double rolling hash* with *bottom‐up* traversal, computing forward and reverse hashes in correct child orders.
- ** Complejidad**: tiempo, memoria.
- **Todos los idiomas**: La misma lógica, con comentarios claros y rápido I/O.

Con esta solución puede abordar con confianza cualquier prueba de medio/difícil en LeetCode **Postorder DFS Palindrome** o problemas similares de piratería de árboles. Buena suerte, y feliz codificación!