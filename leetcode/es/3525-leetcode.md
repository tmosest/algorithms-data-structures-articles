-...
Título: LeetCode 3525. Encontrar valor X de Array II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

## 1. El problema (LeetCode 3525)

■ **Encuentra el valor X de Array II (Hard)* *
■ Se le da un array entero `nums`, un entero `k`, y un array 2-D `queries`.
■ Para cada consulta `[idx, val, start, x]` Debes
■ 1. Reemplace `nums[idx]` with `val`.
■ 2. Remove the prefix `nums[0 ... start‐1]`.
■ 3. From the remaining suffix `nums[start ... n‐1]` Usted puede **remove cualquier sufijo** – esto es equivalente a ** elegir cualquier prefijo no vacío de ese sufijo**.
■ Contar cuántos de estos prefijos tienen un producto que es congruente con `x (mod k)` y devolver ese número.
■ Regrese un array entero `ans` donde `ans[i]` es la respuesta para la consulta *i‐th*.
■ Constraints: `1 ≤ nums.length ≤ 105`, `1 ≤ k ≤ 5`, `1 ≤ queries.length ≤ 105`.

La observación clave es que después de que “hacia atrás” los primeros elementos de “start”, la única operación legal es *elegir un prefijo no vacío del sub-array* restante.
Así que para cada consulta necesitamos el número de prefijos del segmento `nums[start ... n‐1]` cuyo producto es `x (mod k)`.
Debemos apoyar ** actualizaciones de puntos** y **range prefix consultas** – un caso de uso clásico para un árbol de segmento.



----------------------------------------------------

## 2. La Idea Central – Árbol de Segmento de Prefix‐Remanentes

TENIDO Concepto ANTE Lo que el nodo almacena Silencio Por qué es suficiente
Silencio---------------------------------- La vida--
Silencio `prod` Silencioso producto de **todos los elementos del segmento del nodo, modulo reducido `k` Silencio Necesitamos que combine los restos cuando prepagamos a un niño izquierdo a un niño derecho. Silencio
Silencio `cnt[r]` Silencio number of **non-empty prefixes** inside the node’s segment whose product У `r (mod k)` Silencio nos da exactamente lo que necesitamos cuando fusionamos dos niños – todos los prefijos yacen por completo en el niño izquierdo o comienzan en el niño izquierdo y continúan en el niño derecho. Silencio

**Instan a dos niños ( " L " y " R " )* *

`` `
merged.prod = (L.prod * R.prod) % k

merged.cnt = L.cnt // prefijos que permanecen completamente en L
para cada r en 0 ... k- 1
si R.cnt[r] 0
new_r = (L.prod * r) % k
merged.cnt[new_r] += R.cnt[r]
`` `

Esto es `O(k)` por fusión y `k ≤ 5`, por lo que es tiempo constante.



----------------------------------------------------

## 3. Algoritm

1. **Edificio** el árbol del segmento en tiempo de `O(nk).
Leaves store `cnt[ nums[i] % k ] = 1` and `prod = nums[i] % k`.
Los ganglios internos son construidos por la regla de fusión arriba.

2. **Para cada consulta** `[idx, val, start, x]`
* ** Actualizar** la hoja en `idx` con el nuevo valor `val`.
* **Query** el árbol del segmento en `[start, n-1]` (inclusive).
* La consulta devuelve un nodo; la respuesta es node.cnt[x].

3. **Retorno** el array de respuesta.



----------------------------------------------------

## 4. Prueba de corrección

Demostramos que el algoritmo devuelve la respuesta correcta para cada consulta.

-...

### Lemma 1
For any node `v` representing the segment `S`, `v.cnt[r]` equivale al número de prefijos vacíos** de `S` cuyo producto es congruente con `r (mod k)`.

Proof.
Inducción sobre la altura del nodo.

*Base (leaf)* – una hoja contiene un único elemento `a`.
El único prefijo no vacío es el elemento mismo, cuyo producto modulo `k` es `a % k`.
Así `cnt[a % k] = 1` y todos los demás mostradores son `0`, satisfaciendo la lema.

* Paso de inducción* – asuma la lema para los dos niños `L` y `R`.
Vamos.
Todo prefijo no vacío de `S` es
* a prefix entirely inside `L` ( contributing `L.cnt[r]), or
* the whole `L` followed by a prefix of `R`.
Para el segundo caso, un prefijo de `R` con el resto `r2` se convierte en un prefijo de `S` con el resto `(L.prod * r2) % k`.
Exactamente esta lógica se utiliza en el procedimiento de fusión, por lo que el array resultante 'cnt' contiene los recuentos correctos para `S`. ∎



### Lemma 2
Para cualquier segmento `[l, r]`, la rutina de la consulta devuelve un nodo cuya matriz 'cnt' equivale al número de prefijos de `nums[l ... r]` con cada resto, y cuyo `prod` iguala el producto de todo el modulo de segmento `k`.

Proof.
La rutina de consulta agrega nodos de izquierda a derecha utilizando la misma regla de fusión como el paso de construcción.
Debido a que la fusión es asociativa (probado por Lemma 1), el nodo final fusionado representa exactamente la concatenación de todos los sub-segmentos que cubren `[l, r]`.
Por lo tanto, su array 'cnt' contiene los recuentos deseados y su `prod` es correcto. ∎



### Theorem
Por cada consulta `[idx, val, start, x]` el algoritmo produce el número de maneras de eliminar un sufijo del sub-array `nums[start ... n-1]` después de reemplazar `nums[idx] `` por `val ' tal que el prefijo restante tiene el producto 'x (mod k)`.

Proof.
Después de la actualización, el árbol del segmento refleja correctamente el nuevo array de Lemma 1.
La consulta sobre `[start, n-1]` da, por Lemma 2, los recuentos de todos los prefijos de ese sufijo.
Elegir un prefijo de longitud `l` es equivalente a la eliminación de un sufijo de longitud `n - principio - l`.
Así cada operación permitida corresponde exactamente a un prefijo contado, y vice-versa.
Por lo tanto, la respuesta es `node.cnt[x]`, que es lo que el algoritmo regresa. ∎



----------------------------------------------------

## 5. Análisis de la complejidad

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
← Construir Silencioso `O(n · k)` Silencio `O(n · k)` (cada nodo almacena una variedad de tamaño `k`) Silencio
← Actualización de Puntos Silenciosos `O(k · log n)` extra confidencialidad
TENCIÓN DE LA CAMPAÑA TENIDA `O(k · log n)` extra confidencialidad

Con `k ≤ 5`, la constante oculta es pequeña – la solución satisface fácilmente los límites difíciles de LeetCode.



----------------------------------------------------

## 6. Aplicación de las referencias

A continuación encontrará código de trabajo completo para Java, Python y C++ que coincide con la API LeetCode.

■ **Nota** – En los entornos Java y C++ de LeetCode, la clase debe llamarse `Solution` y el método público.
■ En Python la función `resultArray` debe ser miembro de la clase `Solution`.

-...

## 6.1 C++ (GNU C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
int k, n, size; // k ≤ 5
vector asignadoint título prod; // prod en cada nodo de árbol
vector realizador realizado, 6 títulos cnt; // cnt[rem] en cada nodo (index 0...k-1 utilizado)

// fusionar dos nodos infantiles en las posiciones l, r en padres p
vacuno fusión (int p, int l, int r) {}
prod[p] = (prod[l] * prod[r]) % k;
para (int i = 0; i) k; ++i) cnt[p] = cnt[l][i];
para (int rem = 0; rem < k; ++rem) {}
si (cnt[r][rem]) {
int newRem = (prod[l] * rem) % k;
cnt[p][newRem] += cnt[r][rem];
}
}
}

public:
vector identificador ResultadoArray(vector fieltro nums, int k_, vector asignadovector fieltro implicado viviendo consultas) {}
k = k_;
n = nums.size();
tamaño = 1;
mientras (tamaño < n) tamaño n

prod.assign(2 * size, 0);
cnt.assign(2 * tamaño, array observadoint, 6 título{0});

// ------- construir hojas ---
para (int i = 0; i) {}
int pos = tamaño + i;
prod[pos] = nums[i] % k;
cnt[pos] [prod[pos]] = 1;
}

// ------- construir nodos internos ---
for (int i = size - 1; i √≥= 1; --i) merge(i, i, i ' se hizo 1, i ' se cumplió 1 ← 1);

vector significar uns
ans.reserve(queries.size());

// ----- consultas de proceso ---
para (auto &q : consultas) {}
int idx = q[0];
int val = q[1];
int start = q[2];
int x = q[3];

// hoja de actualización
int pos = tamaño + idx;
prod[pos] = val % k;
cnt[pos].fill(0);
cnt[pos] [prod[pos]] = 1;
// actualización padres
para (pos нель = 1; pos; pos > 1) merge(pos, pos, pos) se realizaron 1, pos se hicieron 1

// consulta en [start, n-1]
int l = inicio + tamaño, r = (n - 1) + tamaño;
int resProd = 1; // será sobrescrito
array madeint, 6 confidenciales resCnt{};
bool first = true;

// consultas iterativas (dos pilas – izquierda y derecha)
auto pull = [ cl](int &p) {
si (primero) {
resProd = prod[p];
resCnt = cnt[p];
primero = falso;
. ♫ ... {
tmpProd = res Prod;
int tmpCnt[6];
memcpy(tmpCnt, resCnt.data(), sizeof(int)*6);
// fusión tmpCnt (izquierda) con cnt[p] (derecha)
int newProd = (tmpProd * prod[p]) % k;
array 6 nuevos claves = tmpCnt;
para (int rem = 0; rem < k; ++rem) {}
si (cnt[p][rem]) {
int newRem = (tmpProd * rem) % k;
newCnt[newRem] += cnt[p][rem];
}
}
res Prod = newProd;
res Cnt = newCnt;
}
};

mientras (l <= r) {
(l) pull(l++);
si (!(r)) pull(r--);
l ' título= 1;
r 1;
}

ans.push_back(resCnt[x]);
}
devolver los ans;
}
};
`` `

-...

## 6.2 Python 3 (PyPy 3.7)

``python
Clase Nodo:
__slots__ = ('cnt', 'prod')
def __init__(self, k):
autocnt = [0] * k
autoprod = 0


Segmento de clase Árbol:
def __init__(self, nums, k):
self.k = k
self.n = len(nums)
auto. tamaño = 1
mientras yo. tamaño  se auto.n:
auto.size
self.tree = [Node(k) for _ in range(2 * self.size)]
auto.build(nums)

def build(self, nums):
♪ hojas
para mí en rango(self.n):
nodo = self.tree[self.size + i]
val = nums[i] % self.k
node.prod = val
node.cnt[val] = 1
# Nodos internos
para i in range(self.size - 1, 0, -1):
self.pull(i)

def pull(self, i):
izquierda, derecha = auto.tree[i]
nodo = self.tree[i]
node.prod = (left.prod * right.prod) % self.k
node.cnt = left.cnt[:] # Copia
para r en rango(self.k):
Si es cierto. cnt[r]:
new_r = (left.prod * r) % self.k
node.cnt[new_r] += right.cnt[r]

def update(self, pos, val):
i = auto.size + pos
nodo = self.tree[i]
node.prod = val % self.k
node.cnt = [0] * self.k
node.cnt[node.prod] = 1
i 1
mientras yo:
self.pull(i)
i 1

def query(self, l, r):
l += auto.size
r += auto.size
left_node = Ninguno
right_node = Ninguno
mientras que l
si l ' 1:
si left_node es Ninguno:
left_node = self.tree[l]
más:
left_node = self._merge(left_node, self.tree[l])
l += 1
si no R:
si right_node es Ninguno:
right_node = self.tree[r]
más:
right_node = self._merge(self.tree[r], right_node)
r)= 1
l ' título= 1
r 1
si left_node es Ninguno:
retorno right_node
si right_node es Ninguno:
retorno izquierda_nodo
volver a sí mismo._merge(left_node, right_node)

def _merge(self, left, right):
nodo = Nodo(self.k)
node.prod = (left.prod * right.prod) % self.k
node.cnt = left.cnt[:]
para r en rango(self.k):
Si es cierto. cnt[r]:
new_r = (left.prod * r) % self.k
node.cnt[new_r] += right.cnt[r]
Nodo de retorno


Solución de clase:
def result Array(self, nums: List[int], k: int,
consultas: List[List[int]]) - No. List[int]:
st = SegmentTree(nums, k)
ans = []
para idx, val, start, x en consultas:
st.update(idx, val)
nodo = st.query(start, len(nums) - 1)
ans.append(node.cnt[x])
Retorno
`` `

-...

### 6.3 Java (Java 17)

``java
importar java.util*;

Clase Solución {
Nodo de clase estática {}
int prod;
int[] cnt;
Nodo(int k) { cnt = nuevo int[k]; }
}

clase estática SegTree {
int n, k, size;
Nodo[] árbol; // 1 base, tamaño 2*size

SegTree(int[] nums, int k) {
esto.k = k;
esto.n = nums.length;
tamaño = 1;
mientras (tamaño cautivado n) tamaño
árbol = nuevo Nodo[2 * tamaño];
para (int i = 0; i)
build(nums);
}

vacuno(int[] nums) {
// hojas
para (int i = 0; i)
int pos = tamaño + i;
int val = nums[i] % k;
árbol[pos].prod = val;
árbol[pos].cnt[val] = 1;
}
// nodos internos
para (int i = size - 1; i)= 1; --i) pull(i);
}

vaciado (en idx) {
Nodo izquierdo = árbol [idx] obtenidos 1];
Nodo derecho = árbol[idx] se realizó 1 tención 1];
Cura de nodo = árbol[idx];
cur.prod = (left.prod * right.prod) % k;
Arrays.fill(cur.cnt, 0);
System.arraycopy(left.cnt, 0, cur.cnt, 0, k);
para (int r = 0; r)
si (right.cnt[r] 0) {
int newR = (left.prod * r) % k;
cur.cnt[newR] += right.cnt[r];
}
}
}

vacio de actualización(int pos, int val) {
pos = tamaño + pos;
árbol. prod = val % k;
Arrays.fill(tree[pos].cnt, 0);
árbol[pos].cnt [tree[pos].prod] = 1;
pos " 1;
mientras que (pos >= 1) { pull(pos); pos > 1; }
}

Nodo query(int l, int r) { // inclusive
l += tamaño; r += tamaño;
Nodo izquierdo Res = nula, derecha Res = null;
mientras (l <= r) {
(I) == 1) {
izquierda Res = (izquierda == nula) ? árbol[l] : merge(leftRes, tree[l]);
l++;
}
(r) == 0) {
rightRes = (rightRes == null) ? árbol[r] : merge(tree[r], rightRes);
r...
}
l < < > > 1;
}
si (leftRes == null) devuelve derechoRes;
si (derechaRes == null) regresa a la izquierda Res.
retorno merge(leftRes, rightRes);
}

Node merge(Node left, Node right) {
Nodo res = nuevo Nodo(k);
res.prod = (left.prod * right.prod) % k;
res.cnt = left.cnt.clone();
para (int r = 0; r)
si (right.cnt[r] 0) {
int newR = (left.prod * r) % k;
res.cnt[newR] += right.cnt[r];
}
}
restitución;
}
}

public List Garantizado(int[] nums, int k,
Lista seleccionadaLista realizadaInteger confianza consultas) {
SegTree st = new SegTree(nums, k);
Lista realizadaInteger confía ans = nuevo ArrayList recomendado(queries.size());
para (Lista seleccionadaInteger título q : consultas) {}
int idx = q.get(0), val = q.get(1);
int start = q.get(2), x = q.get(3);
st.update(idx, val);
nodo = st.query(start, nums.length - 1);
ans.add(node.cnt[x]);
}
devolver los ans;
}
}
`` `

-...

## 7. Conclusiones

- La solución utiliza un **segment‐tree** que almacena, para cada nodo,
- el producto del modulo de segmento `k`,
- y por cada resto '0 ... k‐1`, cuántos prefijos del segmento dan ese resto.
- Cada operación ( " actualizada " o " ) es " O(log N) " ; con las actualizaciones y consultas más " 2 × 105 " el algoritmo satisface cómodamente el límite de 2 segundos.
- La aplicación está disponible en **Python (PyPy)**, **Java**, y **C+**, y puede ejecutarse en los respectivos jueces en línea.

Esta respuesta muestra una técnica **rápida, eficiente en memoria** para manejar las consultas dinámicas del producto-modulo contando – un patrón común en programación competitiva y entrevistas técnicas.