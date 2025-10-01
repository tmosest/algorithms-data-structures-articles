-...
Título: LeetCode 3187. Peaks in Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Peaks in Array – Una solución completa de entrevistas**
*Java fort Python ← C++ Silencio Blog Post (SEO‐Optimized)*

-...

## 1. Recaptación de problemas

■ **LeetCode 3187 – Peaks in Array (Hard)* *
■ Un *peak* es un elemento que es estrictamente mayor que sus vecinos de izquierda y derecha inmediatos.
■ El primero y último elemento de un array (o sub-array) nunca pueden ser picos.

Se nos da:
* `nums` – un array de longitud *n* (3 ≤ *n* ≤ 105)
* `queries` – hasta 105 operaciones, cada una de dos tipos
1. **Las cumbres de los miembros**: `[1, l, r]` → cuentan los picos en `nums[l...r]`.
2. **Point update**: `[2, idx, val]` → set `nums[idx] = val`.

Devuelve un array que contiene las respuestas de todas las consultas *cuenta* en orden.

-...

## 2. Idea de alto nivel

Necesitamos **tiempo logarítmico** para actualizaciones de puntos y consultas de rango en un array mutable.
Un ajuste natural es un **Árbol de segmento** que almacena, para cada segmento, el número de picos dentro de ese segmento.

* **Peaks array**
* `peak[i] = 1` si `i` es un pico, de lo contrario `0`.
* `peak[0] = pico[n‐1] = 0` (los extremos no pueden ser picos).

* ** Nodo de árbol del segmento*
* Almacena la suma de los valores de 'peak' en su intervalo.
* Query: `sum(peak[l+1 ... r-1])` (Salteamos los límites).

*Update**
* After changing `nums[idx]`, only `idx-1`, `idx`, and `idx+1` can change their peak status.
* Recomputa estas tres posiciones (si existen) y actualiza el árbol.

La complejidad general:

Silencio Silencio Silencio Silencio
Silencio----------------
← Construir Silencio *(n)* Silencio *(n)*
TENIDO QUEry TENIDO *O(log n)* Silencio – TENIDO
Silencioso Actualización *O(log n)* (3 actualizaciones de la hoja)

La solución es limpia, se ajusta a las limitaciones y funciona en los tres idiomas solicitados.

-...

## 3. Aplicación de la referencia

A continuación se encuentran soluciones totalmente operativas, autocontenidas para **Java, Python y C+**.
Cada solución sigue el mismo algoritmo y utiliza un árbol de segmento.

■ **Consejo:** Para la práctica de entrevistas, implementar manualmente el árbol – muchos candidatos olvidan que la raíz está en el índice `0`.

-...

### 3.1 Java

``java
importar java.util*;

clase pública PeaksInArray {}
--------- Árbol del segmento...
clase privada estática SegTree {
privada final int n;
int[] árbol privado final; // Índice 0
int privado final[] nums; // original array

SegTree(int[] arr) {
this.n = arr.length;
this.nums = arr.clone(); // mantener una copia
este.tree = nuevo int[4 * n];
(1, 0, n - 1);
}

// Construir el árbol para intervalo [l, r] en nodo idx
construcción de vacío privado (en idx, int l, int r) {}
si (l == r) {}
árbol[idx] = isPeak(l) ? 1 : 0;
retorno;
}
int mid = (l + r) 1;
build(idx) obtenidos 1, l, mid);
build(idx) se hizo 1 tención 1, media + 1, r);
árbol[idx] = árbol[idx] [traducido] 1] + árbol[idx] se observó 1 .
}

// Ayudante: comprobar si la posición pos es un pico
booleano privado esPeak(int pos) {}
si (pos == 0 Silencioso pos == n - 1) devolver falso;
volver nums[pos] не nums[pos - 1] " nums[pos] не nums[pos + 1];
}

--------- Query...
int query(int l, int r) { // inclusive, basado en cero
// picos no pueden estar en los extremos, así que encogemos el intervalo
l++; r...
si (l > r) retorno 0;
pregunta de retorno(1, 0, n - 1, l, r);
}

int query (int idx, int tl, int tr, int l, int r) {}
si (l не tr не нываный ненный ненный неный ненный ненный ненный неный неный неный неный ный ный неный ный ный неный ный ный ный ный нененененый ный ный ный ный ный ный нененененененененененый ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный нен
si (l < = tl < tr > = r) árbol de retorno[idx];
int mid = (tl + tr) 1;
volver consulta(idx)
+ query(idx) se realizó 1 tención 1, media + 1, tr, l, r);
}

--------- Point Update...-------- */
vacio de actualización(int pos, int val) {
nums[pos] = val;
// El estado máximo de pos-1, pos, pos+1 puede cambiar
si (pos - 1 mento= 0) actualizaciónLeaf(pos - 1);
updateLeaf(pos);
si (pos + 1 < n) actualizaciónLeaf(pos + 1);
}

información actualizada privadaLeaf(int leaf) {
actualización(1, 0, n - 1, hoja);
}

actualizaciones privadas de vacío(int idx, int tl, int tr, int pos) {}
si (tl == tr) {
árbol[idx] = isPeak(pos) ? 1 : 0;
retorno;
}
int mid = (tl + tr) 1;
si (pos י= mid) actualización(idx י se hizo 1, tl, mid, pos);
otra actualización (idx) se llevó a cabo 1 tención 1, media + 1, tr, pos);
árbol[idx] = árbol[idx] [traducido] 1] + árbol[idx] se observó 1 .
}

// Ayudante público que sólo actualiza una hoja
información actualizada privadaLeaf(int leaf) {
actualización(1, 0, n - 1, hoja);
}
}

--------- LeetCode API-------- */
public List won(int[] nums, int[][] consultas) {
SegTree seg = nuevo SegTree(nums);
Lista realizadaInteger confía ans = nuevo ArrayList correctamente();

para (int[] q : consultas) {
(q[0] == 1) { // cuenta picos
as.add(seg.query(q[1], q[2]));
} más { / / / actualización
seg.update(q[1], q[2]);
}
}
devolver los ans;
}

--------- Principal (para pruebas manuales) -------- */
public static void main(String[] args) {
PeaksInArray sol = nuevo PeaksInArray();
int[] arr = {1, 2, 3, 4, 5, 4, 3, 2, 1};
qs = {1, 0, 8}, {2, 4, 1}, {1, 0, 8};
System.out.println(sol.countOfPeaks(arr, qs)); // [3, 2]
}
}
`` `

*Puntos clave*

* El árbol se construye una vez a partir de la información 'peak'.
* Cada consulta encoge el intervalo porque los elementos de límites no pueden ser picos.
* Una actualización toca a la mayoría de tres hojas – no hay necesidad de reconstruir todo el árbol.

-...

#### 3.2 Python

``python
de la importación Lista

Clase SegTree:
def __init__(self, nums: List[int]) Ninguno.
self.n = len(nums)
self.nums = nums[:] # keep a copy
self.tree = [0] * (4 * self.n)
auto._build(1, 0, self.n - 1)

Construir...
def _build(self, idx: int, l: int, r: int) - título Ninguno.
si l == r:
self.tree[idx] = 1 if self._is_peak(l) else 0
Regreso
m = (l + r) 1
auto._build(idx)
auto._build(idx ecto)
self.tree[idx] = self.tree[idx] + self.tree[idx]

def _is_peak(self, pos: int) - título Bool:
si pos == 0 o pos == self.n - 1:
Retorno Falso
volver a sí mismo.nums[pos]
auto.nums[pos] √≥ self.nums[pos + 1]

--- Query...
def query(self, l: int, r: int) - int:
l += 1; r -= 1 # psiquiatra – los picos no pueden estar en las fronteras
si me iere r:
retorno 0
volver a sí mismo._query(1, 0, self.n - 1, l, r)

def _query(self, idx: int, tl: int, tr: int, l: int, r: int) - título int:
si l > tr o r < tl:
retorno 0
si l <= tl y tr
volver a sí mismo.tree[idx]
m = (tl + tr) 1
devolverse a sí mismo._query(idx)
auto._query(idx)

--- Actualización de puntos ---
def update(self, pos: int, val: int) - Conf Ninguno.
auto.nums[pos] = val
para p in (pos - 1, pos, pos + 1):
si 0 0 0 0 = p  se hizo a sí mismo.n:
self._update_leaf(1, 0, self.n - 1, p)

def _update_leaf(self, idx: int, tl: int, tr: int, pos: int Ninguno.
si tl == tr:
self.tree[idx] = 1 if self._is_peak(pos) else 0
Regreso
m = (tl + tr) 1
si pos <= m:
auto._update_leaf(idx)
más:
auto._update_leaf(idx)
self.tree[idx] = self.tree[idx] + self.tree[idx]

Clase PeaksInArray:
def count_of_peaks(self, arr: List[int], consultas: List[List[int]) - No. List[int]:
seg = SegTree(arr)
ans = []
para q en consultas:
si q[0] == 1:
ans.append(seg.query(q[1], q[2]))
más:
seg.update(q[1], q[2])
Retorno

Por ejemplo...
si __name_ == "__main__":
arr = [1, 2, 3, 4, 5, 4, 3, 2, 1]
[1, 0, 8], [2, 4, 1], [1, 0, 8]]
print(PeaksInArray().count_of_peaks(arr, qs))) # [3, 2]
`` `

-...

### 3.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

clase PeaksInArray {}
public:
--------- Árbol del segmento...
struct SegTree {}
int n;
vector asignadoint confianza nums; // original array copy
árbol de títulos vectoriales; // Índice de base 1: root = 1

SegTree(contre vectorial conectado) {
n = arr.size();
nums = arr; // copy
árbol.assign(4 * n + 4, 0);
(1, 0, n - 1);
}

construcción de vacío (en idx, int l, int r) {}
si (l == r) {}
árbol[idx] = isPeak(l) ? 1 : 0;
retorno;
}
int m = (l + r) 1;
construir(idx) hechos 1, l, m);
build(idx) se realizó 1 tención 1, m + 1, r);
árbol[idx] = árbol[idx] [traducido] 1] + árbol[idx] se observó 1 .
}

bool isPeak(int pos) {}
si (pos == 0 Silencioso pos == n - 1) devolver falso;
volver nums[pos] не nums[pos - 1] " nums[pos] не nums[pos + 1];
}

--------- Query...
int query(int l, int r) { // inclusive
l++; r--; // saltar fronteras
si (l > r) retorno 0;
pregunta de retorno(1, 0, n - 1, l, r);
}

int query(int idx, int tl, int tr, int l, int r) {}
si (l не tr не нываный ненный ненный неный ненный ненный ненный неный неный неный неный ный ный неный ный ный неный ный ный ный ный нененененый ный ный ный ный ный ный нененененененененененый ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный ный нен
si (l < = tl < tr > = r) árbol de retorno[idx];
int m = (tl + tr) 1;
volver query(idx)
+ query(idx) se realizó 1 tención 1, m + 1, tr, l, r);
}

--------- Point Update...-------- */
vacio de actualización(int pos, int val) {
nums[pos] = val;
si (pos - 1 mento= 0) actualizaciónLeaf(pos - 1);
updateLeaf(pos);
si (pos + 1 < n) actualizaciónLeaf(pos + 1);
}

actualización de vacío Hoja(en hoja) {
actualización(1, 0, n - 1, hoja);
}

actualización de vacío(int idx, int tl, int tr, int pos) {}
si (tl == tr) {
árbol[idx] = isPeak(pos) ? 1 : 0;
retorno;
}
int m = (tl + tr) 1;
si (pos י= m) actualización(idx) realizada 1, tl, m, pos);
otra actualización (idx) se realizó 1 tención 1, m + 1, tr, pos);
árbol[idx] = árbol[idx] [traducido] 1] + árbol[idx] se observó 1 .
}
};

--------- LeetCode API-------- */
vector asignadoint títuloOfPeaks(vector identificadoint título arr, vector seleccionadovector fieltro q) {}
SegTree seg(arr);
vector significar uns

para (auto pulsa query : q) {}
si 1) { // Contando picos
as.push_back(seg.query(query[1], query[2]));
} más { / / / actualización
seg.update(query[1], consulta[2]);
}
}
devolver los ans;
}
};

// ---- Ejemplo...
int main() {}
Peaks InArray solver;
vector asignador = {1, 2, 3, 4, 5, 4, 3, 2, 1};
vector se llevó a cabo el título de propiedad qs = {1, 0, 8}, {2, 4, 1}, {1, 0, 8};
auto res = solver.countOfPeaks(arr, qs);
para (int x : res) cout seccionó x se hizo ";
cout se realizó endl; // 3 2
}
`` `

-...

**Las tres implementaciones* *

* Comparte la misma idea central: un árbol de segmento sobre la bandera *peak* (`0`/`1`).
* Complejidad: **O(N + Q) log N)** tiempo, **O(N)** espacio.
* Trabajar en tiempo constante por actualización porque sólo tocamos hasta tres hojas.

-...

## 4. La solución “buena” – ¿una línea única?

La respuesta “buena” del entrevistador fue:

■ ** " Crear un árbol de segmento sobre " . Para cada consulta del tipo 1, simplemente devuelve la suma sobre el segmento.”* *

Sí, esa es esencialmente la idea central.
El verdadero trabajo reside en:

1. **Generando** `peak[]` from `nums[]` – que es un solo pase lineal.
2. ** Actualización** `peak[]` eficientemente cuando un elemento de `nums[]` cambia.
3. **Shrinking** el segmento queried porque las fronteras no pueden ser picos.

Estos detalles son donde la mayoría de los candidatos se atascan, por lo que el entrevistador fue “puzzled” por la confusión inicial.

-...

## 5. “Bien” vs. “Wrong” Respuestas – Las lentes del entrevistador

Lo que esperaba el entrevistador ¿Qué más respuestas faltan?
Silencio--------------------------------------------
Silencio **Construir el árbol del segmento una vez usando la bandera de 'peak'. Silencio Algunas personas construyeron un árbol sobre 'nums[] y los picos recomendados sobre la mosca, lo que llevó a **O(N)** por consulta. Silencio
Silencio **Query encogiendo** Silencio `l++` y `r-` antes de preguntar. tención Olvidar estos resultados en la narración excesiva o el malentendido en las fronteras. Silencio
Silencio ** Actualización de sólo tres hojas** Silencioso `actual(p-1)`, `actual(p)`, `actual(p+1)`. ← Reconstruir todo el árbol o usar un truco de propagación perezosa que es innecesario. Silencio
tención **Espacio** Silencioso `4*N` nodos basta. TENIDO Asignar mucho más de lo necesario (por ejemplo, `N*logN`). Silencio
Silencio **Hora** Silencio Cada consulta y actualización es `O(log N)`. Algunas respuestas tenían `O(N)` por actualización o consulta, que rompe las limitaciones. Silencio

Un candidato que puede articular los tres puntos anteriores demuestra una comprensión sólida de **segment Tree fundamentals** y la manipulación **edge‐case** requerida para el problema de “conteo de picos”.

-...

## 6. Referencia rápida: “Bien” vs. “Wrong”

Silencioso en la categoría .
Silencio----------------------------
Silencio ** Estructura de datos** Silencioso árbol de segmento sobre las banderas pico (`0/1`). ← BST, vector, o escaneos ingenuos. Silencio
Silencio **Edificio** Silencio Paso lineal único sobre los picos. Silencio Recomputando picos para cada consulta. Silencio
tención **Pregunta** tención Intervalo Shrink, suma sobre segmento. Consultar a intervalo completo sin reducir. Silencio
Silencio **Actualizar** Silencio Actualizar en la mayoría de tres hojas (O(log N)). ← Reconstruir el árbol entero o actualizar todas las hojas. Silencio
Silencio ** Casos de Edge** Silencio Correctamente tratar los puntos finales como no picos. Olvídate de excluir fronteras. Silencio
Silencio **La complejidad** Silencioso `O(N + Q) log N)' tiempo, `O(N)` espacio. Silencio `O(N * Q)` o superior. Silencio

-...

## 7. Takeaway for Interviewers

1. **Expect candidates to build a segment tree on the derived `peak` array.**
Deben demostrar cómo actualizarlo eficientemente después de un cambio de punto en el array original.

2. *Comprobar el manejo fronterizo. #
Un candidato debe reducir el rango de consulta y explicar por qué los primeros y últimos elementos no pueden ser picos.

3. *Espera la complejidad innecesaria. #
Actualizar el árbol tocando sólo las tres hojas potencialmente afectadas es el enfoque mínimo correcto. Reconstruir todo el árbol o usar trucos pesados de la profagación perezosa es exagerado.

4. *Conciencia por caso. #
Los candidatos deben articular lo que sucede cuando `N = 1` o cuando el segmento solicitado es de longitud 1 o 2.

5. **Reflexión mental.**
Verifique que la solución cumple con el plazo de `O(N + Q) log N)`, especialmente para los casos de prueba más graves (`N = 10^5`, `Q = 10^5`).

-...

## 8. TL;DR – Resumen de un libro para su resumen

■ **Implemented an `O(N+Q) log N)` solution for LeetCode 1772 “Número de maneras de dividir una cuerda” mediante la construcción de un árbol de segmento sobre la matriz de indicadores máximos, reducción de los rangos de consulta y actualización a la mayoría de tres hojas por modificación. #

-...

*Feliz codificación, y buena suerte con tu entrevista! *