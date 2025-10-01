-...
Título: LeetCode 3414. Maximum Score of Non-overlapping Intervals -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

## 1. El problema, en pocas palabras

Se nos da **N ≤ 50 000** intervalos

`` `
[li , ri , wi] (1 ≤ li ≤ 109, 1 ≤ wi ≤ 109)
`` `

y tenemos que elegir a la mayoría cuatro de ellos para que

* no dos intervalos escogidos se tocan (el extremo derecho de uno debe ser *strictamente* más pequeño que el extremo izquierdo del otro),
* el peso total es maximal, y
* si varios subconjuntos dan el mismo peso máximo devolvemos la lista **léxicográficamente más pequeña de índices originales** (los índices se basan en el orden en que aparecen los intervalos en la entrada).

La salida requerida es la lista de índices originales en orden creciente, es decir, la lista que sería obtenida simplemente clasificando los índices.

■ *Por qué “en la mayoría de cuatro” importa* – porque podemos permitirnos una tabla de programación dinámica completa con una dimensión extra **k  Iberia {0,...,4}**.
■ *Por qué la regla de límites importa* – compartir un punto final izquierdo o derecho se considera superpuesta, por lo tanto la condición *strict* `ri ' (o vice-versa) es la que debe contener.

A continuación encontrará tres soluciones de referencia, una en **Python**, una en **Java** y otra en **C+**. Los tres resuelven el problema en **O(N log N)** tiempo y **O(N)** memoria – cómodamente dentro de los límites.

-...

## 2. El algoritmo (la misma idea en los tres idiomas)

1. **Mantenga los índices originales**
Almacene el 4-tuple `(l, r, w, idx)` para cada intervalo, donde `idx` es la posición en la entrada (0-basado).

2. **Ordenar por el punto final izquierdo**
Esto nos da un orden determinista en el que exploraremos los intervalos.

3. ** Índices de precomputación "next"**
Por cada intervalo `i`necesitamos el primer intervalo que comienza * después* `ri`.
Debido a que tocar el punto final está prohibido, buscamos el más pequeño 'j  Conf' con
`lj œ ri`.
El paso de búsqueda binaria utiliza la lista ordenada de los extremos izquierdos.

4. * Programación dinámica con una dimensión extra*
`dp[i][k]` = best (weight, list of chosen indices) achievable starting from interval `i ' when we are allowed to take at most `k ' more intervals (`k`  Iberia {0,1,2,3,4}).
La recurrencia es la opción clásica “toma / salto”:

* **skip** `i` → `dp[i+1][k] `
* **take** `i` → `wi + dp[next[i] [k-1]` y append `idxi` to the indices list

Debido a que la lista está siempre ordenada y contiene a la mayoría de 4 números, fusionar / clasificar la nueva lista es trivial.

5. #Tie-breaking #
Si las dos opciones dan el mismo peso total debemos devolver la lista de índices *lexicográficamente más pequeña*.
La comparación lexicográfica de dos listas de índices ordenados es simplemente la comparación de elementos por elemento (por ejemplo, la comparación de tuples en Python o `std::lexicographical_compare` en C++).

6. **Respuesta*
Comience la recursión (o el DP inferior) de `i = 0` y `k = 4`.
La lista resultante de índices es la respuesta necesaria.

-...

## 3. Implementaciones de referencia

### 3.1 Python 3

``python
#!/usr/bin/env python3
importadores
importador bisect
desde functools import lru_cache
de la importación Lista, Tuple

def max_weight_intervals(intervalos: List[List[int]) - No. List[int]:
"
Devuelve la lista lexicográficamente más pequeña de los índices originales
que da el peso máximo utilizando a la mayoría de 4 intervalos no superpuestos.
"
n = len(intervalos)
# Attach original indices and sort by left endpoint
ítems = [(l, r, w, idx) para idx, (l, r, w) en enumerado(intervalos)]
items.sort(key=lambda x: x[0])

comienza = [x[0] para x en ítems]
nxt = [bisect.bisect_right(starts, items[i][1]) para i in range(n)]

@lru_cache(maxsize=None)
def dfs(i: int, k: int) - título Tuple[int, Tuple[int, ...]:
""Retorno (score, tuple_of_indices) de la posición i con la mayoría de los k picks.""
si k == 0 o i == n:
0, ()
# Skip
skip_score, skip_list = dfs(i + 1, k)

# Take
take_score, take_list = dfs(nxt[i], k - 1)
take_score += ítems[i][2]
new_list = tuple(sorted(take_list + (items[i][3],))

# Elige lo mejor #
if take_score > skip_score:
volver take_score, new_list
si toma_score < skip_score:
volver skip_score, skip_list
# equal weight → lexicographic comparison
volver take_score, min(skip_list, new_list)

best_score, best_indices = dfs(0, 4)
lista de devolución (best_indices)


# -------- conductor--------------
si __name_ == "__main__":
data = sys.stdin.read().strip().splitlines()
si no datos:
sys.exit()
N = int(data[0])
intervalos = [lista(map(int, line.split()))) para línea en datos[1:N + 1]]
res = max_weight_intervals(intervalos)
print(" ".join(map(str, res)))
`` `

**Explicación**

* `@lru_cache` garantiza que cada par `(i, k)` se computa una sola vez.
* La profundidad de la recursión está atada por `N` pero el caché evita un soplo: sólo ~N × 5 estados existen.
* `tuple(sorted(...)')` garantiza que la lista está ordenada y lista para la comparación lexicográfica.

-...

#### 3.2 Java 17

``java
importa java.io.*;
importar java.util*;

clase pública Principal {}

Clase privada estática Interval {
int l, r, w, idx;
Interval(int l, int r, int w, int idx) {}
this.l = l; this.r = r; this.w = w; this.idx = idx;
}
}

Clase privada estática Resultado {
puntuación larga;
Lista de índices enteros; // ordenados
Resultado(número largo, Lista) {
esto. puntuación = puntuación;
esto.indices = índices;
}
}

public static List No se hace referenciaInteger confianza solve(List madeint[] crudo) {
int n = raw.size();
Lista de artículos Intervalentes = nuevo ArrayList correctamente(n);
para (int i = 0; i)
int[] a = raw.get(i);
ítems.add(new Interval(a[0], a[1], a[2], i));
}
items.sort(Comparator.comparingInt(o - título o.l));

int[] comienza = nuevo int[n];
para (int i = 0; i) no; i++) comienza[i] = items.get(i).l;
int[] next = new int[n];
para (int i = 0; i)
int pos = upperBound(starts, items.get(i).r);
siguiente[i] = pos;
}

long[][] bestScore = new long[n + 1][5];
@SuppressWarnings("unchecked")
Lista de datos: bestList = nueva lista[n + 1][5];
para (int k = 0; k <= 4; k++) {
bestScore[n][k] = 0;
bestList[n][k] = Collections.emptyList();
}

para (int i = n - 1; i 0; i--) {
para (int k = 0; k <= 4; k++) {
long skipScore = bestScore[i + 1][k];
Lista de datos skipList = bestList[i + 1][k];

si (k == 0) { // no queda nada por elegir
bestScore[i][k] = skipScore;
bestList[i][k] = skipList;
continuar;
}

int ni = next[i];
largo Puntuación = items.get(i).w + bestScore[ni][k - 1];
Lista realizadaInteger confianza takeList = nuevo ArrayList fiel(bestList[ni][k - 1]);
takeList.add(items.get(i).idx);
Collections.sort(takeList);

si (takeScore > skipScore) {
bestScore[i][k] = take Puntuación;
bestList[i][k] = take Lista;
} si (takeScore ) {
bestScore[i][k] = skipScore;
bestList[i][k] = skipList;
} más { // igual peso - ruptura de la corbata léxicográfica
bestScore[i][k] = take Puntuación;
bestList[i][k] = lexicographicMin(skipList, takeList);
}
}
}
devolver bestList[0][4];
}

// devuelve la lexicografía más pequeña de dos listas clasificadas
Lista estática privada realizadaInteger confianza lexicográficaMin(Listitud indicadaInteger confianza a, Lista recomendadaInteger título b) {
int i = 0;
mientras (i) {}
int va = a.get(i), vb = b.get(i);
si (va != vb) devuelve va
i++;
}
devolver a.size()
}

// superior atado en un array ordenados
estática privada int upperBound(int[] arr, int key) {
int l = 0, r = arrr.length;
mientras que (l
int m = (l + r) 1;
si (arr[m] m + 1;
r = m;
}
retorno l;
}

//----------------------------------
public static void main(String[] args) tira IOException {
BufferedReader br = nuevo BufferedReader (nueva InputStreamReader(System.in));
int n = Integer.parseInt(br.readLine().trim());
Lista hecha[]] > > > >
para (int i = 0; i)
String[] parts = br.readLine().trim().split("\s+");
raw.add(new int[]{Integer.parseInt(parts[0]),
Integer.parseInt(partes[1]),
Integer.parseInt(parts[2])});
}
Lista de datos:Integer titulado ans = solve(raw);
StringBuilder sb = nuevo StringBuilder();
para (int i = 0; i) i++) {
si (i > 0) sb.append(' ');
sb.append(ans.get(i));
}
System.out.println(sb);
}
}
`` `

**Puntos clave* *

* `@lru_cache` garantiza O(1) por estado.
* `min(skipList, newList)` utiliza la comparación de tuple – el tupla lexicográficamente más pequeño se elige automáticamente cuando el peso total es igual.

-...

### 3.3 Java 17 (bottom-up DP – no recursion)

``java
importa java.io.*;
importar java.util*;

clase pública Principal {}
Clase privada estática Interval {
int l, r, w, idx;
Interval(int l, int r, int w, int idx) {}
this.l = l; this.r = r; this.w = w; this.idx = idx;
}
}

Lista estática privada realizadaInteger confianza solve(List madeint[] crudo) {
int n = raw.size();
Lista de artículos Intervalentes = nuevo ArrayList correctamente(n);
para (int i = 0; i)
int[] a = raw.get(i);
ítems.add(new Interval(a[0], a[1], a[2], i));
}
items.sort(Comparator.comparingInt(o - título o.l));

int[] comienza = nuevo int[n];
para (int i = 0; i) no; i++) comienza[i] = items.get(i).l;
int[] next = new int[n];
para (int i = 0; i)
siguiente[i] = topBound(starts, items.get(i).r);
}

long[][] bestScore = new long[n + 1][5];
@SuppressWarnings("unchecked")
Lista de datos: bestList = nueva lista[n + 1][5];
para (int k = 0; k <= 4; k++) {
bestScore[n][k] = 0;
bestList[n][k] = Collections.emptyList();
}

para (int i = n - 1; i 0; i--) {
para (int k = 0; k <= 4; k++) {
// skip
long skipScore = bestScore[i + 1][k];
Lista de datos skipList = bestList[i + 1][k];

si (k == 0) { / // nada más que tomar
bestScore[i][k] = skipScore;
bestList[i][k] = skipList;
continuar;
}

// Toma
int ni = next[i];
largo Puntuación = items.get(i).w + bestScore[ni][k - 1];
Lista realizadaInteger confianza takeList = nuevo ArrayList fiel(bestList[ni][k - 1]);
takeList.add(items.get(i).idx);
Collections.sort(takeList);

si (takeScore > skipScore) {
bestScore[i][k] = take Puntuación;
bestList[i][k] = take Lista;
} si (takeScore ) {
bestScore[i][k] = skipScore;
bestList[i][k] = skipList;
} más { // igual peso - lexicografía min
bestScore[i][k] = take Puntuación;
bestList[i][k] = lexicographicMin(skipList, takeList);
}
}
}
devolver bestList[0][4];
}

// la parte superior en los extremos izquierdos ordenados
estática privada int upperBound(int[] arr, int key) {
int l = 0, r = arrr.length;
mientras que (l
int m = (l + r) 1;
si (arr[m] m + 1;
r = m;
}
retorno l;
}

// devuelve la lexicografía más pequeña de dos listas clasificadas
Lista estática privada realizadaInteger confianza lexicográficaMin(Listitud indicadaInteger confianza a, Lista recomendadaInteger título b) {
int i = 0;
mientras (i) {}
int va = a.get(i), vb = b.get(i);
si (va != vb) devuelve va
i++;
}
devolver a.size()
}

public static void main(String[] args) tira IOException {
BufferedReader br = nuevo BufferedReader (nueva InputStreamReader(System.in));
int n = Integer.parseInt(br.readLine().trim());
Lista hecha[]] > > > >
para (int i = 0; i)
String[] parts = br.readLine().trim().split("\s+");
raw.add(new int[]{Integer.parseInt(parts[0]),
Integer.parseInt(partes[1]),
Integer.parseInt(parts[2])});
}
Lista de datos:Integer titulado ans = solve(raw);
StringBuilder sb = nuevo StringBuilder();
para (int i = 0; i) i++) {
si (i > 0) sb.append(' ');
sb.append(ans.get(i));
}
System.out.println(sb);
}
}
`` `

¿Por qué? #

* La recuperación con la memoización también podría funcionar, pero un simple DP iterativo elimina cualquier riesgo de desbordamiento de pila y es muy sencillo de entender.

-...

## 3.4 Python 3 (formulario alternativo)

``python
def solve():
importadores
data = sys.stdin.read().strip().split()
si no datos:
Regreso
iter(data)
n = int(next(it)))
raw = [(int(next(it)), int(next(it)), int(next(it))))) for _ in range(n)]
raw.sort(key=lambda x: x[0]) # sort by left endpoint

comienza = [x[0] para x en bruto]
def upper_bound(a, key):
l, r = 0, len(a)
mientras que l
m = (l + r) 1
si a[m] 1
más: r = m
Regreso

siguiente_idx = [upper_bound(starts, x[1]) para x en bruto]
dp_score = [[0]*5 for _ in range(n+1)]
dp_list = [[[]]*5 for _ in range(n+1)]
para i en rango(n-1, -1, -1):
para k en rango(5):
skip_score = dp_score[i+1][k]
skip_list = dp_list[i+1][k]
si k==0:
dp_score[i][k] = skip_score
dp_list[i][k] = skip_list
continuar
take_score = raw[i][2] + dp_score[next_idx[i]][k-1]
take_list = sort(dp_list[next_idx[i] [k-1] + [i])
if take_score > skip_score:
dp_score[i][k] = take_score; dp_list[i][k] = take_list
elif take_score
dp_score[i][k] = skip_score; dp_list[i] = skip_list
más: # igual peso
dp_score[i][k] = take_score
dp_list[i][k] = min(skip_list, take_list)
print(' '.join(map(str, dp_list[0]))
`` `

-...

### 3.5 C++ 17

``cpp
#include יbits/stdc++.h
usando std namespace;

struct Interval {}
int l, r, w, idx;
};

int upperBound(cont vector conectado int key) {}
int l = 0, r = (int)a.size();
mientras que (l
int m = (l + r) 1;
si (a[m] m + 1;
r = m;
}
retorno l;
}

int main() {}
ios::sync_with_stdio(false);
cin.tie(nullptr);
int n;
si (!(cin  título n)) devuelve 0;
vectores: Intervalencia c;
para (int i = 0; i) {}
int l, r, w; cin  confían en l ' e
v.emplace_back(l, r, w, i);
}
(v.begin(), v.end(), [](contigo Intervalciente a, const Interval plaga b){ devolver a.l.

vector significado(n)
para (int i = 0; i)
vector:
para (int i = 0; i) no; ++i) nxt[i] = upperBound(starts, v[i].r);

vector realizadora realizada largamente,5 título(n+1)
vector realizador realizador seleccionado,5 título(n+1);
para (int k = 0; k)
score[n][k] = 0;
lst[n][k] = {};
}

para (int i = n-1; i 0; --i) {
para (int k = 0; k)
saltos largos = puntuación[i+1][k];
const vector armonizado plom = lst[i+1][k];

(k == 0) {
score[i][k] = skipS;
lst[i][k] = skipL;
continuar;
}

long takeS = v[i].w + score[nxt[i] [k-1];
vector empleadoint takeL = lst[nxt[i] [k-1];
takeL.push_back(v[i].idx);
(takeL.begin(), takeL.end());

si (takeS  skip skipS) {
score[i][k] = takeS;
lst[i][k] = takeL;
} si (tomas) {
score[i][k] = skipS;
lst[i][k] = skipL;
. ♫ ... {
// igual – lexicografía min
score[i][k] = takeS;
// lexicografía min de dos vectores ordenados
const vector implicados a = skipL, &b = takeL;
vector significar res = a;
bool menos = falso;
for (size_t t = 0; t ' t > min(a.size(), b.size()); ++t) {
si (a[t] != b[t] {}
menos = a[t] > b[t];
ruptura;
}
}
si (menos) res = a;
si (a.size() √≥ b.size()) res = b;
lst[i][k] = res;
}
}
}
for (size_t i = 0; i ' i ' ilse [0][4].size(); ++i) {
si (i) cout se hizo "
cout se realizó lst[0][4][i];
}
cout se hizo 'n';
}
`` `

**Highlights* *

* Usos `vector obtenidosarray fiel `` para arrays DP (tamaño fijo 5 para 'k').
* La comparación lexicográfica se realiza manualmente con un pequeño bucle.

-...

### 3.6 C# 11

``csharp
mediante el Sistema;
usando System. Colecciones. Genérico;
usando System. OI;
usando System. Linq;

public class Program
{}
registro privado Interval(int L, int R, int W, int Id);

Registro privado Resultado(punto largo, Lista de índices relativos);

vacío estático público Principal()
{}
var input = Console.ReadLine();
si (input == null) regresa;
int n = int.Parse(input);
var raw = nueva lista hecha []
para (int i = 0; i)
{}
var parts = Console.ReadLine().Split(' ', StringSplitOptions.RemoveEmptyEntries);
crudo. Add(new int[] { int.Parse(parts[0]), int.Parse(parts[1]), int.Parse(parts[2]) });
}

var ans = Solve(raw);
Console.WriteLine(string.Join(', ans));
}

privada estática Lista efectuadaint título Solve(List seleccionadaint[]]
{}
int n = crudo. Cuenta;
var items = new List won(n);
para (int i = 0; i)
artículos. Add(new Interval(raw[i][0], raw[i][1], raw[i][i][2], i));

(a, b) = título a.L.CompareTo(b.L));

int[] comienza = items.Select(x = título x.L).ToArray();
int[] next = new int[n];
para (int i = 0; i)
siguiente[i] = UpperBound(starts, items[i].R);

long[][] bestScore = new long[n + 1][];
Lista especificada [] [] [] bestList = nueva lista efectuada [n + 1][];
para (int k = 0; k)
{}
bestScore[n] = nuevo largo[5];
bestList[n] = nueva lista especificada[5];
para (int kk = 0; kk = 4; kk+)
{}
bestScore[n][kk] = 0;
bestList[n][kk] = nueva lista hecha con título();
}
}

para (int i = n - 1; i 0; i...)
{}
para (int k = 0; k)
{}
long skipScore = bestScore[i + 1][k];
Lista especificada " patrón " = bestList[i + 1][k];

(k == 0)
{}
bestScore[i][k] = skipScore;
bestList[i][k] = skipList;
continuar;
}

largo Puntuación = artículos[i]. W + bestScore [next[i]][k - 1];
var takeList = new List garantizadoint(bestList[next[i] [k - 1]) { items[i]. Id.
takeList.Sort();

si (takeScore  skip skipScore)
{}
bestScore[i][k] = take Puntuación;
bestList[i][k] = take Lista;
}
si (takeScore )
{}
bestScore[i][k] = skipScore;
bestList[i][k] = skipList;
}
// peso igual
{}
bestScore[i][k] = take Puntuación;
// lexicografía min
bestList[i][k] = LexicographicMin(skipList, takeList);
}
}
}
devolver bestList[0][4];
}

int estática privada UpperBound(int[] a, int key)
{}
int l = 0, r = a.Length;
mientras que (l
{}
int m = (l + r) / 2;
si (a[m] m + 1;
r = m;
}
retorno l;
}

privada estática Lista efectuadaint título LexicographicMin(List madeint título a, Lista especificada b)
{}
int len = Math.Min(a.Count, b.Count);
para (int i = 0; i)
{}
si (a[i] != b[i]) devolver a [i]
}
devolver a.Count = b.Count ? a : b;
}
}
`` `

* C# 11 utiliza `record ' para la brevedad y las estructuras de datos inmutables.

-...

## 4. Explicación del Algoritmo (Programación Dinámica)

1. **Sorting**
Todos los intervalos están ordenados por el punto final izquierdo \(L_i\).
Esto garantiza que si el intervalo *j* comienza más tarde que *i* (\(L_j √≥ L_i\)), entonces en el orden ordenados *j* aparecerá después de *i*.
The property needed for the DP recurrence is:
*El intervalo más adecuado que termina antes del punto final izquierdo del intervalo actual es el predecesor. *
Debido a que los intervalos están ordenados por *L*, ese predecesor se puede encontrar con una búsqueda binaria en el array de puntos finales izquierdos.

2. * Programación Dinámica*
Por cada posición *i* (intervalo *i*) y por cada número *k* de intervalos ya elegidos (\(0\le k\le 4\)) almacenamos:
* `dp_score[i][k]` – máximo peso total alcanzable teniendo en cuenta sólo los intervalos con índices ≥ i cuando *k* intervalos ya han sido elegidos.
* `dp_list[i][k]` – la correspondiente lista de índices ordenados.

Recurrencia para intervalo *i* (índice basado en 0):

`` `
saltar: no elegir nada del intervalo i
puntuación = dp_score[i+1][k]
lista = dp_list[i+1][k]

tomar: elegir intervalo i (no debe superponerse con cualquier intervalo elegido más tarde)
let p = next_index[i] // primer intervalo que comienza después de R_i
puntuación = peso[i] + dp_score[p][k-1]
lista = ordenada( dp_list[p] [k-1]
`` `

Si las dos puntuaciones difieren, mantenemos el mayor.
Si las puntuaciones son iguales, conservamos la lista de índices *lexicográficamente más pequeña* – esto es lo que pide la declaración.

3. **Respuesta*
Después de construir la tabla DP, el peso máximo deseado es `dp_score[0][4]`.
La lista de índices asociada `dp_list[0][4]` contiene los cuatro índices de intervalo seleccionados en orden ascendente.

4. *Las complejidades*
*Sorting:* \(O(n\log n)\).
*DP loop:* Para cada intervalo se iteran más de 5 valores de *k* y se realizan en la mayoría de algunas operaciones vectoriales → \(O(n)\).
*Memoria:* 5 × (n + 1) 64 bits + 5 × (n + 1) listas – linear en *n*.

-...

## 5. Casos de borde

* **Equipos óptimos Multiple** – nuestra regla lexicográfica garantiza una respuesta única.
* **Intervalos que no superponen** – el DP selecciona automáticamente los cuatro con mayor peso.
* **Muy gran entrada** – todas las soluciones utilizan I/O rápido y funcionan en el tiempo \(O(n\log n)\).

-...

## 6. Aplicación de referencia – Java (con comentarios completos)

``java
importa java.io.*;
importar java.util*;

clase pública Principal {}

----------- estructura de datos para un intervalo --------- */
Clase privada estática Interval {
int l, r, w, idx;
Interval(int l, int r, int w, int idx) {}
this.l = l; this.r = r; this.w = w; this.idx = idx;
}
}

------------- ---
public static void main(String[] args) tira IOException {
FastScanner fs = nuevo FastScanner (System.in);
int n = fs.nextInt();
Interval[] a = nuevo Interval[n];
para (int i = 0; i)
int l = fs.nextInt();
int r = fs.nextInt();
int w = fs.nextInt();
a[i] = nuevo Interval(l, r, w, i); // los índices se basan en 0
}

/* ---------- ---
Arrays.sort(a, Comparator.comparingInt(o - título o.l));

/* ---------- compute 'next' array */
int[] lefts = new int[n];
para (int i = 0; i) no; i++) izquierdas[i] = a[i].l;

int[] next = new int[n];
para (int i = 0; i)
siguiente[i] = topBound(izquierda, a[i].r); // primer intervalo con L  título R_i
}

--------- DP ----------------------------------------
long[][] dpScore = nuevo largo[n + 1][5]; // dpScore[i][k]
int[][][] dp Lista = nuevo int[n + 1][5][]; // dpList[i] [k] - título int[] de índices

para (int i = n; i 0; i--) { // desde n-1 hasta 0
para (int k = 0; k <= 4; k++) {
si (i == n) { // base: más allá del último intervalo
dpScore[i][k] = 0;
dpList[i][k] = nuevo int[0];
continuar;
}

/* ----- opción: saltar intervalo actual --- */
long skipScore = dpScore[i + 1][k];
int[] skipList = dpList[i + 1][k];

/* ----- opción: tomar intervalo actual --- */
largo Puntuación = a[i].w;
int[] take Lista = nula;
si (k > 0) { /// podemos tomar sólo si todavía necesitamos intervalos
Toma. Score += dpScore[next[i]][k - 1];
int[] tmp = dpList[next[i] [k - 1];
Toma. Lista = Arrays.copyOf(tmp, tmp.length + 1);
takeList[takeList.length - 1] = a[i].idx; // Apend current index
Arrays.sort(takeList);
. ♫ ... {
// no se puede tomar cuando k=0 (no se necesitan más intervalos)
Toma. Puntuación = Long.MIN_VALUE;
Toma. Lista = nuevo int[0];
}

/* ----- Elija una mejor opción (corte léxicográfico) --- */
si (takeScore > skipScore) {
dpScore[i][k] = take Puntuación;
dpList[i][k] = takeList;
} si (takeScore ) {
dpScore[i][k] = skipScore;
dpList[i][k] = skipList;
} más { // igual puntuación - elegir la lista lexicográficamente más pequeña
dpScore[i][k] = take Resultado; // mismo valor
dpList[i][k] = lexicographicMin(skipList, takeList);
}
}
}

/* ---------- */
int[] respuesta = dpList[0][4]; // índices de intervalos elegidos
StringBuilder out = nuevo StringBuilder();
para (int i = 0; i)
si (i > 0) fuera.append(')
out.append(answer[i]);
}
System.out.println(out.toString());
}

/* ---------- búsqueda binaria: primer índice con valor llave...
estática privada int upperBound(int[] arr, int key) {
int l = 0, r = arrr.length;
mientras que (l
int m = (l + r) 1;
si (arr[m] m + 1;
r = m;
}
retorno l;
}

/* ---------- lexicográficamente más pequeño de dos conjuntos de int ordenados */
int[] lexicographicMin(int[] a, int[] b) {
int minLen = Math.min(a.length, b.length);
para (int i = 0; i) {}
si (a[i] != b[i]) devolver a [i]
}
devolver a.length
}

Escáner rápido para entrada de entrada --------------------------
Clase privada estática FastScanner {}
InputStream final privado;
byte final privado[] buffer = nuevo byte[1]
int ptr privado = 0, len = 0;
FastScanner(InputStream in) { this.in = in; }
int privada read() lanza IOException {
si
len = in.read(buffer);
ptr = 0;
si (len len= 0) retorno -1;
}
búfer de retorno[ptr+];
}
int nextInt() lanza IOException {
int c, sign = 1, val = 0;
do c = read(); while (c <= ' ' -1);
(c == '-') { sign = -1; c = read(); }
mientras (c > '') { val = val * 10 + (c - '0'); c = read(); }
retorno val * signo;
}
}
}
`` `

*El programa sigue exactamente el algoritmo explicado anteriormente y es compatible con Java 17. *

-...

Fin del Tutorial.