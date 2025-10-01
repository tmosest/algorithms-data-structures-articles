-...
Título: LeetCode 3410. Maximizar el Suma de Subarray Después de eliminar todas las probabilidades de un elemento -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Respuesta – 12 minutos ( Entendido 750 palabras)* *

-...

## Lo que el problema realmente pregunta

Por cada valor distinto `v` en el array podemos *remove all occurrences* of `v`.
El array que queda es sólo el array original con esas posiciones eliminadas, y
la tarea es reportar el *maximum sub-array sum* de esa nueva matriz.

`` `
original : 1 2 3 3 4
eliminar 3 : 1 2 4 → sub-array máximo = 1+2+4 = 7
`` `

Debido a que los elementos eliminados son simplemente **skipped**, un sub-array en el nuevo array
corresponde a una secuencia de índices en el array original que contiene **no**
`v` - pero puede saltarse sobre las posiciones eliminadas.
Así que no podemos confiar en la propiedad “contigua en la matriz original”.

-...

## 1. The “skip‐over‐v” Kadane

La forma más simple de calcular la respuesta por un valor particular `v` es:

`` `
current_sum = 0
respuesta =
para cada elemento x en el array:
si x == v: # elemento se elimina → nada para añadir
continuar
current_sum = max(current_sum + x, x)
respuesta = max(respuesta, current_sum)
`` `

El bucle nunca se reinicia `current_sum` en un elemento eliminado – simplemente *skip*
Es. El algoritmo es un solo pase (O(n)) para ese `v`.
Repetirlo por cada valor distinto produce una solución O(n · U)
(`U` = número de valores distintos).
Esto está perfectamente bien para los datos pequeños pero se vuelve demasiado lento cuando el array
contiene 100 000 números distintos (operaciones de Silvestre).

-...

## 2. Una solución casi óptima O(n log n)

El editorial oficial muestra que podemos construir un árbol **segment** que
tiendas, por cada intervalo:

* " suma " - suma total del intervalo
* `pref` – el mejor prefijo suma
* `suff` – best suffix sum
* `best` – la mejor suma de sub-array dentro del intervalo

Combinar dos nodos infantiles es la fórmula clásica

`` `
suma = izquierda.sum + derecha.sum
pref = max(left.pref, left.sum + right.pref)
suff = max(right.suff, right.sum + left.suff)
mejor = max(left.best, right.best, left.suff + right.pref)
`` `

Una vez construido el árbol (O(n)), podemos * cambiar temporalmente* cada ocurrencia de
" v " a " (es decir, eliminarlo) mediante actualizaciones de puntos.
Después de todas las actualizaciones de ese valor, el campo "mejor" de la raíz ya contiene
el sub-array máximo de la matriz con todo `v` eliminado.
Luego revertimos los cambios – cada elemento se actualiza *exactamente una vez** sobre
toda la carrera, así que el trabajo total es

`` `
edificio : O(n)
actualizaciones : O(n log n) (cada elemento actualizado registro n veces)
consultas: O(1) por valor
`` `

Complejidad general: **O(n log n)**, que cumple fácilmente los límites.

-...

## 3. Aplicación de pitón (árbol de segmento)

``python
importadores
de las colecciones importadas por defecto

# ----------... árbol del segmento...------------
Clase Nodo:
__slots__ = ('sum', 'pref', 'suff', 'best')
def __init__(self, val=0):
self.sum = self.pref = self.suff = self.best = val

def merge(a: Node, b: Node) - título Nodo:
res = Nodo()
res.sum = a.sum + b.sum
res.pref = max(a.pref, a.sum + b.pref)
res.suff = max(b.suff, b.sum + a.suff)
res.best = max(a.best, b.best, a.suff + b.pref)
retorno

def build(arr):
n = len(arr)
tamaño = 1
mientras que tamaño n: tamaño
seg = [Nodo() para _ en rango(2 * tamaño)]
♪ hojas
para i, v en enumerate(arr):
seg[size + i] = Node(v)
# Nodos internos
para i en rango(tamaño - 1, 0, -1):
seg[i] = merge(seg[2 * i], seg[2 * i + 1])
seg de retorno, tamaño

def point_update(seg, size, pos, val):
i = tamaño + pos
seg[i] = Nodo(val)
i 1
mientras yo:
seg[i] = merge(seg[2 * i], seg[2 * i + 1])
i 1
# --------------fin del árbol----------

def solve() - título Ninguno.
it = iter(sys.stdin.read().strip())
n = int(next(it)))
a = [int(next(it))) for _ in range(n)]

# trivial case - todos los números negativos
si todo(x) se hizo 0 para x en a):
print(max(a)))
Regreso

# posiciones de cada valor
pos = defaultdict(list)
para i, v in enumerate(a):
pos[v].append(i)

seg, size = build(a)
respuesta = max(a) # siempre podemos tomar un solo elemento

para val, idxs en pos.items():
1. eliminar temporalmente este valor
para mí en idxs:
point_update(seg, size, i, 0)

respuesta = max(respuesta, seg[1].best)

# 2. restaurar los valores originales
para mí en idxs:
point_update(seg, size, i, a[i])

print(respuesta)

si __name_ == "__main__":
solve()
`` `

**Explicación de las partes clave**

Silencio Parte privada Por qué es necesario
Silencio...
Silencio `Node` tención Almacena los cuatro parámetros; `______' mantiene el uso de la memoria bajo. Silencio
Silencio `merge` Silencio Combina a dos niños; idéntico a la fórmula en el editorial. Silencio
Silencio `construye el árbol en tiempo lineal. Silencio
TENIDO `point_update` Silencio Usado dos veces por elemento – una vez para establecerlo a `0`, una vez para restaurarlo. Silencio
Silencio `pos` Silencioso Diccionario `valor → lista de índices` – iterating over this diccionario
garantiza que cada elemento se actualiza exactamente una vez para todo el algoritmo. Silencio

-...

## 4. Aplicación C++ (árbol de segmento)

``cpp
#include יbits/stdc++.h
usando std namespace;

struct Node {}
larga larga suma, pref, suff, best;
Nodo(long long v = 0) : sum(v), pref(v), suff(v), best(v) {}
};

Node merge(const Node &l, const Node &r) {
Res;
res.sum = l.sum + r.sum;
res.pref = max(l.pref, l.sum + r.pref);
res.suff = max(r.suff, r.sum + l.suff);
res.best = max({l.best, r.best, l.suff + r.pref});
restitución;
}

int main() {}
ios::sync_with_stdio(false);
cin.tie(nullptr);
int n;
si (!(cin  título n)) devuelve 0;
vector realizado largamente a(n);
para (auto &x : a) cin >

si (*max_element(a.begin(), a.end())
cout se llevó a cabo *max_element(a.begin(), a.end()))
retorno 0;
}

unordered_map hacía largo, vector pos;
para (int i = 0; i)

int sz = 1;
mientras (sz identificó n) sz
vector node confianza seg(2 * sz, Node());

para (int i = 0; i) seg[sz + i) = Nodo(a[i]);
for (int i = sz - 1; i √≥ 0; --i) seg[i] = merge(seg[2 * i], seg[2 * i + 1]);

auto point_update = [ю](int p, long long val) {
p += sz;
seg[p] = Nodo(val);
para (p нель = 1; p; p; p > 1)
seg[p] = merge(seg[2 * p], seg[2 * p + 1]);
};

larga respuesta = *max_element(a.begin(), a.end());
para (auto " [val, idxs] : pos) {
para (int idx : idxs) point_update(idx, 0);
respuesta = max(respuesta, seg[1].best);
para (int idx : idxs) point_update(idx, a[idx]);
}

cout se hizo la respuesta
retorno 0;
}
`` `

El código C++ sigue la misma lógica que la versión Python – una versión inferior
árbol de segmento y un diccionario de posiciones. Todas las actualizaciones se realizan en
`O(log n)` tiempo, y cada elemento array se actualiza exactamente dos veces sobre el
Toda la ejecución.

-...

## 5. Aplicación de Java (árbol de segmento)

``java
importa java.io.*;
importar java.util*;

clase pública Principal {}
Clase privada estática Nodo {}
larga suma, pref, suff, best;
Nodo(long v) { sum = pref = suff = best = v; }
}

estática privada Node merge(Node l, Node r) {}
Nodo res = nuevo Nodo(0);
res.sum = l.sum + r.sum;
res.pref = Math.max(l.pref, l.sum + r.pref);
res.suff = Math.max(r.suff, r.sum + l.suff);
res.best = Math.max(Math.max(l.best, r.best), l.suff + r.pref);
restitución;
}

el vacío estático público principal (String[] args) lanza Excepción {
BufferedReader br = nuevo BufferedReader (nueva InputStreamReader(System.in));
int n = Integer.parseInt(br.readLine().trim());
StringTokenizer st = nuevo StringTokenizer(br.readLine());
long[] a = new long[n];
para (int i = 0; i < n; i++) a[i] = Long.parseLong(st.nextToken());

si (Arrays.stream(a) allMatch(x - título x 0) {
System.out.println(Arrays.stream(a).max().getAsLong());
retorno;
}

Mapa seleccionadoLong, Lista Nombrado:Integer título pos = nuevo HashMap fiel();
para (int i = 0; i)
pos.computeIfAbsent(a[i], k - título nuevo ArrayList correctamente()).add(i);
}

int size = 1;
mientras (tamaño cautivado n) tamaño
Nodo[] seg = nuevo Nodo[2 * tamaño];
para (int i = 0; i) seg[i] = nuevo Nodo(0);

para (int i = 0; i) seg[size + i] = nuevo Nodo(a[i]);
for (int i = size - 1; i √≥ 0; --i) seg[i] = merge(seg[2 * i], seg[2 * i + 1]);

respuesta larga = Arrays.stream(a).max().getAsLong();

para (Map.Entry madeLong, Listo)Integer confianza e : pos.entrySet() {
Lista de índices enteros = e.getValue();
for (int idx : indices) pointUpdate(seg, size, idx, 0);
respuesta = Math.max(respuesta, seg[1].best);
for (int idx : indices) pointUpdate(seg, size, idx, a[idx]);
}

System.out.println(answer);
}

punto de vacío estático privadoUpdate(Nodo[] seg, int size, int pos, long val) {
int p = tamaño + pos;
seg[p] = nuevo Nodo(val);
para (p √Ī= 1; p √≥ 0; p } 1)
seg[p] = merge(seg[p] obtenidos 1], seg[p] seg [p] seg [p] seg [p] seg [p]
}
}
`` `

El código Java es esencialmente la misma idea que el C++, pero utiliza un
"Clase de Nodo" y una serie de 'Nodo's para el árbol del segmento.

-...

## 6. Cómo decidir qué aplicación utilizar

Silencio Silencio Silencio Silencio Silencio
Silencio----------------------------------------------------
Silencio Muy pequeños arrays (≤ 2000) ← Naïve Kadane para cada `v` TEN O(n · U) TENIDO Simple, sin estructura de datos sobre arriba TEN
TENIDO Grandes arrays (≥ 104) TENIDO Árbol de Segmento (O(n log n))
← Necesita una solución **Python** ← Árbol de segmento con la implementación iterativa ← Mismo O(n log n) Silencio Python es más lento por operación.
tención Necesita una solución **C++** o **Java** ← Árbol de segmento Recursivo o iterativo Silencio Mismo O(n log n) Silencio La profundidad de la recesión es ≤ log n (Ω 17), seguro

-...

## 7. Dificultades comunes

1. **Usando ints de 32 bits en C++/Java** – las sumas pueden llegar a 104 · 109, por lo que
use `long' / `long`.
2. *Actualizando el nodo equivocado* – recuerde que en un árbol de abajo arriba el
hoja está en el índice `size + pos`, no `pos`.
3. ** Iniciación incorrecta para el árbol vacío** – las hojas para índices no utilizados deben
ser `-∞` si usted está buscando el subarray máximo sobre toda la matriz; aquí nosotros
simplemente mantenerlos en `0` porque nunca son alcanzados (indices más allá
`n` nunca se preguntan).
4. **Desbordamiento entero** – en C++ y Java usan `long' / `long`.
5. **Introducción de lectura rápida** – especialmente en C++/Java, use I/O amortiguado; in
Python, lee todo el archivo inmediatamente.

-...

## 7. Observaciones finales

El problema se reduce a “por cada valor distinto, computar el subarray máximo
suma después de eliminar todas sus ocurrencias”. La visión crucial es que nosotros
puede realizar la remoción estableciendo temporalmente las posiciones correspondientes
a `0` en un árbol de segmento, consulta la respuesta, y luego restaurar el original
valores. Debido a que cada índice pertenece exactamente a un valor, cada elemento es
actualizado sólo dos veces, garantizando el plazo `O(n log n)`. El código
ejemplos anteriores implementan esta estrategia en tres idiomas populares.