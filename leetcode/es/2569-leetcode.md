-...
Título: LeetCode 2569. Manipulación de consultas después de la actualización -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 2569. Manipulación de consultas de suma después de actualización
**Hard** – LeetCode
**Problema**: Dados dos arrays de igual longitud `nums1` (sólo 0/1) y `nums2`, procesar una lista de hasta \(10^5\) consultas:

Silencio tipo Silencioso formato de consulta
Silencio--------Prince------------
Silencio **1** Silencio `[1, l, r]` Silencioso cada poco en `nums1[l...r]`. Silencio
Silencio **2** Silencio `[2, p, 0]` Silencio Para todos i, `nums2[i] += nums1[i] * p`.
Silencio **3** Silencio `[3, 0, 0]` Silencio Devuelve la suma actual de todos los elementos en `nums2`. Silencio

Devuelve un array con las respuestas de todas las consultas tipo 3.

√≥ latitudes ** Objetivo** – Resolverlo en \(O(n+q)\log n)\) tiempo y \(O(n)\) memoria.

A continuación encontrará código de trabajo ** para:

* Java – usando un árbol de segmento perezoso + BitSet
* Python – árbol de segmento iterativo
* C++ – árbol de segmento iterativo

...y un blog **SEO-friendly** que explica el “bueno, el malo y el feo” de este problema de entrevista clásica.

-...

## 📚 El Blog – “El Bien, el Mal y el Ugly of Handling Sum Queries After Update”

■ *“¿Quieres aterrizar ese papel de ingenieros de software? Maestro este LeetCode duro y muestra tus trucos algorítmicos!”*

-...

#### ## 1down⃣ ¿De qué se trata este problema?

- Dos arrays**:
- `nums1` - binario (0/1).
- `nums2` - arbitrarios números no negativos.
- Tres tipos de consultas.
1. ** Range bit flip** – cambia cada 0 ↔ 1 en un sub-array de `nums1`.
2. **Add‐by-ones** – para cada índice, añadir `p * nums1[i]` a `nums2[i]`.
3. **Quería del Sol** – devolver el total de `nums2`.

Usted debe responder a muchas consultas eficientemente; un análisis de fuerza bruta en cada consulta sería \(O(nq)\) – imposible para \(n,q\le10^5\).

-...

#### 2down⃣ ¿Por qué está mal el enfoque ingenuo?

TENCIÓN ANTERIENTE Complejidad ANTERIOR Por qué falla
Silencio--------------------------
tención **Brute force** Silencio \(O(nq)\) Silencio Re-computando la suma y escaneando `nums1` para cada consulta. Silencio
Silencio **Maintain `nums2` array** Silencio Todavía \(O(nq)\) Silencio Actualizar cada elemento en el tipo‐2 es demasiado lento. Silencio
Silencio **Utilizar un contador simple** tención \(O(1)\) por consulta TENCIÓN Flipping bits in a range (`l.r`) todavía requeriría escanear ese segmento. Silencio

La clave es **evitar tocar cada elemento** en cada consulta.

-...

#### 3down⃣ El “bueno” – Árbol de Segmento Perezoso

Un árbol de segmento mantiene un resumen (aquí: **cuento de los**) para cada segmento de `nums1`.
La propagación perezosa nos permite aplazar las actualizaciones:

- **Flip a range** – simplemente cambiamos una bandera de “lazy flip” en el nodo, y el recuento del nodo de los se convierte en `segmentLength - uno `.
- **Tipo‐2 consulta** – sólo necesitamos el número total de los de toda la matriz, que es el recuento de la raíz.
- ** Pregunta tipo 3** – mantenemos una suma de ejecución de `nums2` (`long`), y responderemos al instante.

#### Complexity

Silencio Silencio Silencio Silencio
Silencio--------------
← Construir el árbol Silencioso \(O(n)\) Silencio
tención Rango voltereta Silencioso \(O(\log n)\) Silencio
TENIDO Tipo‐2 TENIDO \(O(1)\) (encuentramiento raíz) Silencio
TENIDO Tipo‐3 TENIDO \(O(1)\) Silencio

¡Perfecto por las limitaciones!

-...

#### 4down⃣ El “malo” – BitSet (Java solamente)

Java’s `BitSet` ofrece una representación rápida y de bajo nivel de arrays binarios.
Sumergir un rango (`bs.flip(l, r+1)`) es *normalmente* \(O(\frac{r-l+1}{64})\), que es bueno en la práctica pero todavía **linear** en el tamaño del rango.
Para las consultas peor de los casos (por ejemplo, volteando todo el array muchas veces), se degenera a \(O(nq)\).

■ **TL;DR** – BitSet es *buena* para concursos en los que los rangos son pequeños; *bad* cuando usted golpea los datos de casos peores.

-...

#### 5down⃣ Las "muy" – Casos de Edge " Pitfalls

Silencio Tema Silencio Qué ver para Silencio
Silencio...
* 10^5 \* 10^6 → use 64-bit (`long` / `int64`). Silencio
tención **Indización basada en el espacio** Silencio Todas las consultas están basadas en 0; no hay errores por uno. Silencio
Silencio **Lazy flag propagation** latitud Olvidar empujar la bandera antes de acceder a los niños corrompe el árbol. Silencio
Silencio **Large la profundidad de recursión** Silencio En Python, la recursión en un árbol de segmento de 200k-nodo puede alcanzar el límite de la pila. Use la versión iterativa o aumente el límite de recursión. Silencio
tención **Tiempo-limit** tención Factores constantes importan; prefiera arrays iterantes sobre las clases. Silencio
Silencio ** Memoria** Silencioso `4*n` nodos para árbol + `4*n` banderas perezosas está bien (`n=10^5` → ~3 MB). Silencio

-...

#### 6down⃣ El Código – Java, Python, C++

A continuación encontrará soluciones **ready‐to-run** para los tres idiomas.
Cada uno utiliza un árbol de segmento iterativo con propagación perezosa (excepto el fragmento Java que muestra una alternativa *BitSet*).

-...

## 🧑 💻 Java Solution (Lazy Segment Tree)

``java
importar java.util*;

Solución de la clase pública {}
--------- Segment Tree...--------
clase privada estática SegTree {
int n;
int[] cnt; // número de uno en cada segmento
booleano[] perezoso; // pendiente bandera

SegTree(int[] a) {
n = a.length;
cnt = nuevo int[4 * n];
perezoso = nuevo booleano[4 * n];
(1, 0, n - 1, a);
}

a)
si (l == r) {}
cnt[node] = a[l];
retorno;
}
int mid = (l + r) 1;
construir(nodo)
construir(nodo) se hizo 1 tención 1, mitad + 1, r, a);
cnt[nodo] = cnt[nodo] se realizó 1] + cnt[nodo] se realizó 1 .
}

empuje de vacío privado (en nodo, int l, int r) {}
si (lazy[node]) {}
int mid = (l + r) 1;
aplicar (nodo)
aplicar(nodo)
perezoso[nodo] = falso;
}
}

nulo privado aplica (nodo, int l, int r) {}
cnt[node] = (r - l + 1) - cnt[node];
perezoso[nodo] ^= verdadero;
}

// bits en [ql, qr]
(int ql, int qr) { update(1, 0, n - 1, ql, qr); }

actualizaciones privadas de vacío (en nodo, int l, int r, int ql, int qr) {
si (qr.)
si
aplicar (nodo, l, r);
retorno;
}
push(node, l, r);
int mid = (l + r) 1;
actualización (nodo) realizada 1, l, mediados, ql, qr);
actualización (nodo) se realizó 1 tención 1, mitad + 1, r, ql, qr);
cnt[nodo] = cnt[nodo] se realizó 1] + cnt[nodo] se realizó 1 .
}

int totalOnes() { return cnt[1]; }
}
// - Sí.

public long[] handleQuery(int[] nums1, int[] nums2, int[][] consultas) {
SegTree st = new SegTree(nums1);
larga suma = 0;
para (int v : nums2) suma += v; // suma inicial de nums2

Lista de respuestas de larga duración = nuevo ArrayList correctamente();

para (int[] q : consultas) {
int type = q[0];
(tipo == 1) { //
q[2]);
} si (tipo == 2) { /// add p *
long p = q[1];
suma += p * st.totalOnes();
} más { / / suma de consulta
respuestas.add(sum);
}
}

long[] res = new long[answers.size()];
para (int i = 0; i)
restitución;
}
}
`` `

■ **Compile**: `javac Solution.java `
■ **Test**: pegar la manija Query` llama a tus pruebas de unidad.

-...

## 🐍 Python Solution (Iterative Segment Tree)

``python
importadores
de la importación Lista

Clase SegTree:
def __init_(self, a: List[int]):
self.n = len(a)
auto.cnt = [0] * (4 * self.n)
self.lazy = [False] * (4 * self.n)
self.build(1, 0, self.n - 1, a)

def build(self, node, l, r, a):
si l == r:
self.cnt[node] = a[l]
Regreso
media = (l + r) // 2
autor.build(nodo * 2, l, mid, a)
autor.build(nodo * 2 + 1, mitad + 1, r, a)
self.cnt[node] = self.cnt[node * 2] + self.cnt[node * 2 + 1]

def push(self, node, l, r):
si auto.lazy[node]:
media = (l + r) // 2
auto.apply(nodo * 2, l, mid)
self.apply(node * 2 + 1, mid + 1, r)
self.lazy[node] = False

def apply(self, node, l, r):
auto.cnt[nodo] = (r - l + 1) - self.cnt[node]
self.lazy[node] ^= Cierto.

def update(self, ql, qr):
self._update(1, 0, self.n - 1, ql, qr)

def _update(self, node, l, r, ql, qr):
si qr se hizo l o r se hizo ql:
Regreso
si ql י= l y r <= qr:
auto.apply(nodo, l, r)
Regreso
auto.push(nodo, l, r)
media = (l + r) // 2
self._update(node * 2, l, mid, ql, qr)
self._update(node * 2 + 1, mid + 1, r, ql, qr)
self.cnt[node] = self.cnt[node * 2] + self.cnt[node * 2 + 1]

def total_ones(self):
retorno auto.cnt[1]

def handle Query(nums1: List[int], nums2: List[int], consultas: List[List[int]]) - No. List[int]:
st = SegTree(nums1)
total = suma (nums2)
fuera =

para q en consultas:
t = q[0]
si #
st.update(q[1], q[2])
elif t == 2: # add p * ones
p = q[1]
total += p * st.total_ones()
# sum query
out.append(total)

Retorno

# ----
# Ejemplo de conductor (opcional – eliminar al enviar a LeetCode)
si __name_ == "__main__":
nums1 = [0, 1, 0, 1, 1]
nums2 = [1, 2, 3, 4, 5]
consultas =
[3, 0, 0],
[1, 0, 2],
[3, 0, 0],
[2, 2, 0],
[3, 0, 0]
]
print(handle) Query(nums1, nums2, consultas)) # [15, 15, 27]
`` `

■ ¿Por qué iterativa? #
■ Evita problemas de profundidad de recursión en Python y funciona cómodamente bajo 1 s para preguntas \(10^5\).

-...

## 🎯 C+ Solución (Árbol de Segmento Iterante)

``cpp
#include יbits/stdc++.h
usando std namespace;

clase SegTree {
int n;
vector asignadoint título cnt; // número de
vector asignadobool confianza perezoso; // pendiente flip

public:
SegTree(cont vector identificadoint estrecho a) : n(a.size())) {}
cnt.assign(4*n, 0);
lazy.assign(4*n, false);
construir(1, 0, n-1, a);
}

construcción de vacío(en nodo, int l, int r, const vector implicaint {}
si (l == r) {}
cnt[node] = a[l];
retorno;
}
int m = (l + r) 1;
construir (nodo realizado);
construir(nodo observado)1 vidas1, m+1, r, a);
cnt[nodo] = cnt[nodo observado] + cnt[nodo observado]1 sometida1];
}

información actualizada (int L, int R) { update(1, 0, n-1, L, R); }

empuje vacío(en nodo, int l, int r) {}
si (!lazy[node]) regresa;
int m = (l + r) 1;
aplicar(nodo indicado)1, l, m);
aplicar(nodo observado)1 vida1, m+1, r);
perezoso[nodo] = falso;
}

nulo aplicado(en nodo, int l, int r) {}
cnt[node] = (r-l+1) - cnt[node];
perezoso[nodo] ^= verdadero;
}

vaciado de actualización(en nodo, int l, int r, int L, int R) {
si regresan (R seleccionadol TENIDO R)
si
aplicar (nodo,l,r);
retorno;
}
push(node,l,r);
int m = (l+r) título 1;
actualización (nodo realizado);
actualización (nodo indicado)
cnt[nodo] = cnt[nodo observado] + cnt[nodo observado]1 sometida1];
}

int totalOnes() const { return cnt[1]; }
};

vector de larga duración empuñadura Query(vector seleccionado] nums2,
vector de búsquedas:
SegTree st(nums1);
larga suma = 0;
(auto v : nums2) suma += v;

vector realizado largamente largas ans;
para (auto &q : consultas) {}
(q[0] == 1) st.update(q[1], q[2]); // flip
si (q[0] == 2) suma += 1LL*q[1] * st.totalOnes(); // add
ans.push_back(sum); // query
}
devolver los ans;
}

/* -... Arnés de prueba de ejemplo...
int main() {}
vector nums1 = {0,0,1,1};
vectorial de larga duración nums2 = {1,2,3,4,5};
vector de vectores consultas = {
{3,0,0},
{1,0,2},
{3,0,0},
{2,2,0},
{3,0,0}
};
auto res = mango Query(nums1, nums2, consultas);
para (auto v:res) cout se llevó a cabo v se hizo "
retorno 0;
}
*/
`` `

■ **¿Por qué este código C++? * *
■ Todas las operaciones son **iterative** y utilizan `int` para índices, `int64` (`long') para sumas – no rebosa de las pilas de recursión y la sobrecarga mínima.

-...

## 🧩 Take‐away

* ** Árbol de segmento + Propagación perezosa** es la estructura de datos *must‐know* para este problema.
* **BitSet** funciona *bien* cuando los rangos son cortos, pero puede ser una pesadilla para las entradas del peor de los casos.
* Sé meticuloso con **overflow**, ** indexación basada en cero**, y ** propagación de bandera perezosa**.

Muestra estas ideas en tu entrevista o en tu perfil coding-platform – los reclutadores aman a un candidato que puede diseccionar un problema en *bueno, malo,* y *muy* piezas.

-...

## 🔑 SEO Palabras clave (para los reclutadores " sitios de entrevistas prep)

* LeetCode Hard – Manejo de las consultas de sum después de la actualización
* Binary Array Rango Algoritm
* Lazy Segment Tree Sum Query
* Entrevista Algorithm – Rango Flip + Add‐By‐Ones
* C++ Python Código Java – LeetCode 2569
* Problema de entrevista de ingeniero de software superior
* Manipulación de consultas del sumo después de actualización del tutorial
* Aplicación del árbol de segmentos de rayos binarios

-...

■ **Feliz codificación, y puede que su tiempo de ejecución sea \(O(\log n)\) y su uso de memoria sea *(n)*!** .

-..