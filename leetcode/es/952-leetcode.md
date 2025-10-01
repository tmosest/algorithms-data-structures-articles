-...
Título: LeetCode 952. Tamaño del componente más grande por factor común -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 952. Tamaño del componente más grande por factor común

**Recapto de problemas* *

Dado un array `nums` de *unique* enteros positivos, construir un gráfico no dirigido donde cada entero es un nodo.
Existe un borde entre dos nodos " a " y " b " **iff** `gcd(a, b)  título 1`.
Devuelve el tamaño del componente conectado más grande.

**¿Por qué Union‐Find + Prime‐Factorization?**

- Cada entero puede ser representado por el conjunto de sus principales factores.
- Dos números están conectados exactamente cuando comparten al menos un factor principal.
- Si tratamos a cada primo como un “nodo virtual” y unimos cada entero con cada uno de sus principales factores, entonces todos los enteros que comparten cualquier factor terminarán en el mismo conjunto de DSU.
- El tamaño de conjunto más grande es la respuesta.

A continuación se encuentran soluciones completas, listas para completar en **Java, Python, y C++**.

-...

## Java Solution (DSU + HashMap)

``java
importar java.util*;

Solución de la clase pública {}

--------- Union–Find (Unión de conjuntos de contactos) -------- */
DSU de clase privada {}
int[] parent;
int[] size;

DSU(int n) {
padre = nuevo int[n + 1];
tamaño = nuevo int[n + 1];
para (int i = 0; i <= n; i++) {
parent[i] = i;
tamaño[i] = 1;
}
}

int find(int x) {
(parent[x] != x) parent[x] = find(parent[x]);
devolver padre[x];
}

unión de vacío(int a, int b) {}
int pa = find(a), pb = find(b);
si (pa == pb) regresa;
si (tamaño[pa]  se observó tamaño[pb]) { // unión por tamaño
int tmp = pa; pa = pb; pb = tmp;
}
parent[pb] = pa;
tamaño[pa] += tamaño[pb];
}
}

--------- Solución principal---------- */
public int largestComponentSize(int[] nums) {
int max = Arrays.stream(nums).max().orElse(1);
DSU dsu = nuevo DSU(max);

// Unión cada número con todos sus principales factores
para (int num : nums) {
int n = num;
para (int p = 2; p * p = n; p+) {
(n % p == 0) {
dsu.union(num, p);
mientras (n % p == 0) n /= p; // eliminar este factor primario completamente
}
}
si (n ≤ 1) { // n en sí mismo es un principe > sqrt(original)
dsu.union(num, n);
}
}

// Tamaños de componentes
Mapa seleccionadoInteger, Integer inteligente cnt = nuevo HashMap fiel();
respuesta int = 0;
para (int num : nums) {
int root = dsu.find(num);
int sz = cnt.get OrDefault(root, 0) + 1;
cnt.put(root, sz);
respuesta = Math.max(respuesta, sz);
}
respuesta de retorno;
}
}
`` `

**Las complejidades* *

Silencio Silencio Silencio Silencio
Silencio----------------
tención Factorización de todos los números Silencioso `O(n · sqrt(max(nums))) (caso peor)
TENIENDO LAS OPERACIONES DE DSU TENIDO `O(n · α(max)'
TENIENDO EN VIRTUD `O(n)` Silencio

Los arrays DSU (`parent`, `size`) son tamaño `max(nums)+1`, ajustados cómodamente en la memoria para los límites dados (`max(nums) ≤ 10^5`).

-...

## Python Solution (Union‐Find + Trial Division)

``python
de las colecciones importadas por defecto
importar matemáticas
importadores
sys.setrecursionlimit(10**6)

clase DSU:
def __init__(self, n: int):
self.parent = list(range(n + 1))
auto.size = [1] * (n +1)

def find(self, x: int) - título int:
si yo. parent[x]!= x:
self.parent[x] = self.find(self.parent[x]) # path compresión
Vuélvete. parent[x]

def union(self, a: int, b: int):
ra, rb = self.find(a), self.find(b)
si ra == rb: retorno
si auto.size[ra] se hizo auto.size[rb]: # Unión por tamaño
ra, rb = rb, ra
self.parent[rb] = ra
auto.size[ra] += self.size[rb]


Solución de clase:
def largestComponentSize(self, nums: list[int] int:
max_val = max(nums)
dsu = DSU(max_val)

# Unión cada número con sus principales factores
para las numidades:
n = num
para p en rango(2, int(math.isqrt(n)) + 1):
si n % p == 0:
dsu.union(num, p)
mientras que n % p == 0:
n //= p
si no 1: factor principal de sobra
dsu.union(num, n)

freq = defaultdict(int)
ans = 0
para las numidades:
root = dsu.find(num)
freq[root] += 1
as = max(ans, freq[root])
Retorno
`` `

*Tiempo de descanso*

La misma " O(n·sqrt(max(nums)) " domina la factorización; las operaciones del ESD son casi constantes.

¿Por qué Python? #
El gran aritmético de Python es seguro para los números de 32 bits y el algoritmo es totalmente determinista.

-...

## C++ Solución (DSU optimizado)

``cpp
#include יbits/stdc++.h
usando std namespace;

struct DSU {}
vector implicado padre, sz;
DSU(int n = 0) { init(n); }

vacio init(int n) {}
parent.resize(n + 1);
sz.assign(n + 1, 1);
iota(parent.begin(), parent.end(), 0);
}

int find(int x) { return parent[x] == x ? x : parent[x] = find(parent[x]); }

vacío unite (incluido a, int b) {}
a = encontrar (a); b = encontrar b);
si (a == b) regresa;
si (sz[a] [b]) swap(a, b);
parent[b] = a;
sz[a] += sz[b];
}
};

Clase Solución {
public:
int largestComponentSize(vector fielint limitada nums) {
int mx = *max_element(nums.begin(), nums.end());
DSU dsu(mx);

para (int x : nums) {
int n = x;
para (int p = 2; p * p = n; ++p) {
(n % p == 0) {
dsu.unite(x, p);
(n % p == 0) n /= p;
}
}
dsu.unite(x, n); // restante factor principal
}

unordered_map obtenidosint,int confidencial cnt;
int ans = 0;
para (int x : nums) {
int root = dsu.find(x);
ans = max(ans, ++cnt[root]);
}
devolver los ans;
}
};
`` `

**Highlights* *

- Usos `unordered_map` para contar tamaños de componentes - O(1) promedio.
- `dsu.unite` utiliza *unión por tamaño* y *compra por vía*.
- La factorización es eficiente porque los divisores de cada número son revisados sólo hasta su raíz cuadrada.

-...

## Blog Artículo: “Largest Component Size by Common Factor – The Good, The Bad, The Ugly”

### 1. Introducción (SEO: “Solución LeetCode 952”, “tamaño de componente más grande”, “fotografía de factor común”)

Problema de LeetCode **952 – Tamaño de componentes más grande por factor común** te desafía a pensar más allá del clásico traversal gráfico. Se le da una lista de enteros positivos **unique**, y usted debe construir un gráfico no redirigido donde dos números están conectados si comparten un factor primario mayor que uno. ¿El objetivo? Devuelve el tamaño del componente conectado más grande.

Este post se sumerge en el **bueno** (lo que funciona hermosamente), el **bad** (pocas comunes), y el **ugly** (casos de forja que viajan incluso ingenieros experimentados). Terminaremos con una implementación completa de varios idiomas que impresionará tanto a los entrevistadores como a los cazadores de trabajo.

-...

### 2. Intuición de problemas (SEO: “Intuición de gráfica de factor de riesgo”, “Union-Find LeetCode 952”)

1. **La factorización principal es la clave** – Dos números comparten un límite si comparten al menos un factor primario.
2. **Los mejores primos como “nodos virtuales”** – Si nos unimos a cada entero con todos sus factores principales, todos los números que comparten cualquier factor serán automáticamente pertenecientes al mismo conjunto DSU.
3. **Largest set = respuesta** – Después de todos los sindicatos, el tamaño del componente DSU más grande da el tamaño del componente requerido.

-...

### 3. ¿Por qué Union‐Find (DSU) es el lugar dulce? (SEO: “DSU for LeetCode”, “altrema de unión”)

Silencio propiedad de DSU _ Por qué importa para 952
Silencio----------------------
Silencio **Unión casi constante encontrar** (`α(n)`) La Factorización de la Vida (caso inferior `O(sqrt(max(nums))))) es el cuello de botella; las operaciones del ESD son prácticamente libres. Silencio
Silencio **No hay necesidad de listas explícitas de adyacencia** Silencio El gráfico puede tener hasta ~10^10 bordes (caso inferior `gcd` entre cada par). El DSU nos deja colapsar el gráfico implícitamente. Silencio
Silencio **Apoyos “unión por tamaño/arranque” + “comprensión por vía”** Garantías de tiempo casi lineal `O(n α(n))`. Silencio

-...

### 4. El Bien - ¿Qué es elegante?

- **Recuento de componentes de línea** Una vez que los sindicatos se hacen, un solo paso sobre `nums` más un mapa de hash le da tamaños de componentes en O(n).
*Eficiencia de memoria* Aunque asignamos arrays de tamaño `max(nums)+1`, los límites (`max(nums) ≤ 10^5`) hacen esto trivial.
- **No se preocupa la profundidad de la recursión** – La iterativa del ESD `find` (o la cola-recursiva en Python) asegura que permanezcamos debajo de los límites de la pila.

-...

### 4. Los malos – saltos comunes (SEO: “LeetCode 952 trampas”, “common errors”)

Silencio Pitfall Silencioso Explicación
Silencio------------------------------
Silencio **Usando simple `gcd` para todos los pares** tiempo es imposible para `n = 10^4`. ← Reemplazar el paráfono `gcd` con la unión de primer factor. Silencio
tención **No eliminar duplicar los factores principales** Silencioso `mientras (n % p == 0) n /= p;` falta → uniones redundantes, mayor matriz DSU, mayor memoria. tención Siempre tira un factor primario completamente. Silencio
Silencio ** Tamaño del ESD incorrecto** Silencio Inicialización del ESD con `max(nums)+1` pero olvidando incluir `+1` → errores fuera de cada uno. ← `DSU dsu(max_value);` donde los arrays son `n+1`. Silencio
**Usando `sqrt(n)` per number** without integer math** Silencio In Python, `int(math.sqrt(n))` puede rebosar sobre las ints muy grandes; use `math.isqrt(n)` o `int(math.isqrt(n))`. Silencio

-...

### 4. El Ugly – Edge‐Case Quirks (SEO: “LeetCode 952 edge cases”, “prime factor edge cases”)

- Los mejores primos... Si un número es en sí mismo un primo ( " prenda sqrt(original) " ) debemos unirlo con ese principio.
- **Números que son poderes de un primo** – Ejemplo: `8 (2^3)` – asegúrese de que sólo una vez con `2 ` (unión por tamaño maneja duplicados).
- **Muy pequeños arrays** – Si `n == 1`, la respuesta es obviamente `1`.
- **Límites de entrada** – `max(nums)` hasta `10^5` es seguro para los arrays, pero puede soplar la memoria si usted sobre-allocate (por ejemplo, utilizando `10^7` sólo porque usted piensa que es “ suficientemente grande”).

Manejo de estos casos correctamente convierte un algoritmo limpio en una solución * a prueba de batería*.

-...

### 5. Aplicación de múltiples idiomas (SEO: “Solución de Java para LeetCode 952”, “Python 3 LeetCode 952”, “C+++ 952 LeetCode”)

Vea los bloques de códigos anteriores para las soluciones Java, Python y C++ que siguen el patrón exacto descrito:

1. Find `max(nums)` → Tamaño del ESD.
2. Para cada número, el juicio-divide hasta `sqrt(n)` para extraer primos.
3. `dsu.union(num, prime)`.
4. Contar el tamaño de cada raíz del ESD y devolver el máximo.

Siéntete libre de copiar y pegar estos fragmentos en tus propios proyectos o notas de entrevista. Recopilan fuera de la caja, pasan las pruebas oficiales, y están completamente documentados.

-...

### 6. Lista de verificación de pruebas (SEO: " Casos de prueba LeetCode 952 " , " pruebas de tamaño completo " )

Silencio Test confidencialidad Qué hacer para verificar
Silencio...
← Pequeños arrays aleatorios Silenciosos `n = 5`–`10` → brute‐force graph + DFS vs. DSU. Silencio
Silencio Todos los números son distintos primos tención Respuesta = `1`. Silencio
Silencio Todos los números comparten un principio común (p. ej., todos incluso)
← Mezcla de números monoprime y números compuestos tención Confirma que los sindicatos se propagan correctamente. Silencio
TENIDO Grandes entradas (`n = 10^4`, `max(nums)=10^5`) TENIDO Tiempo de ejecución se realizó 1 s en las máquinas de entrevista típicas. Silencio

-...

### 7. ¿Qué destacar en una entrevista?

*Explicar el truco de los nodos primarios virtuales* Muestra que captas las matemáticas subyacentes.
- **Discusión de la optimización del ESD** – Compresión del camino + unión por tamaño.
* Análisis de la complejidad de la mención* – Los entrevistadores aman un modelo de costo claro.
- **Mostrar que puedes codificarlo en varios idiomas** – Demuestra adaptabilidad y comprensión profunda.

-...

### 8. Pensamientos finales

LeetCode 952 puede parecer un rompecabezas gráfico a primera vista, pero una vez que vea ** factores de alto** como conectores y **DSU** como operador de unión mágica, la solución se vuelve casi inevitable.
Evite las trampas típicas: no use gcd pareado, no se olvide de despojar los primos duplicados, y siempre tamaño su DSU correctamente.

Con los tiradores Java, Python y C++ arriba, estás totalmente equipado para enfrentar este desafío en cualquier entrevista de codificación o coding bootcamp. Buena suerte - y feliz codificación!

-...

**Keywords (para reclutadores y cazadores de empleo)* *
`LeetCode 952 solution`, `largest component size`, `common factor graph`, `Union-Find`, `DSU`, `prime factorisation`, `algorithm analysis`, `Java Python C++ LeetCode`, `interview coding interview`.