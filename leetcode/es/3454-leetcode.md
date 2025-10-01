-...
Título: LeetCode 3454. Plazas separadas II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 3454 – Plazas separadas II
### The Hardest “Horizontal Split” Problem on LeetCode
*Está buscando una manera de impresionar a los gerentes de contratación? *
Este post muestra una solución limpia y lista para la producción en **Java, Python y C+** y explica el algoritmo en inglés claro.
Lea para descubrir las partes *bueno*, *bad* y *muy* de este desafío – todo lo que necesita para llegar a la entrevista y aterrizar ese trabajo!

-...

## Tabla de contenidos
1. [Resumen del proyecto](#problema-summario)
2. [Intuición " Observaciones clave](#intuición)
3. [Algorithm Overview](#algorithm)
4. [Detailed Walkthrough](#walkthrough)
5. [Análisis de complejidad](#complejidad)
6.
7. [Code – Java](#java-code)
8. [Code – Python](#python-code)
9. [Code – C++](#cpp-code)
10. [SEO " Job‐Search Tips](#seo)
11. [Pensamiento Final](#final)

-...

"Problem-summary"
## 1. Resumen del problema

■ **Given** un array `squares` donde cada elemento es `[xi, yi, li]` - la esquina inferior izquierda y la longitud lateral de un cuadrado -
■ **Retorno** el *mínimo* `y` tal que la zona sindical de todos los cuadrados **arriba** esta línea equivale a la zona sindical **bajo**.
■
■ Los cuadrados pueden superponerse. Las partes superpuestas son **contadas sólo una vez** (es decir, estamos trabajando con el *unión* de los cuadrados).

*Ejemplo*

`` `
cuadrados = [0,0,1], [2,2,1]]
Respuesta: 1.00000
`` `

■ Cualquier línea horizontal entre `y=1` y `y=2` divide el área total (2) en la mitad.
■ El más pequeño de esos `y' es `1`.

Las limitaciones son grandes (`n ≤ 5·104`, coordenadas hasta `109`, superficie total ≤ `1015`). Se necesitan soluciones que se ejecutan en **O(n log n)** tiempo y uso *O(n)* memoria.

-...

"Intuición"
## 2. Intuición " Observaciones clave

1. **Area debajo de una línea horizontal es una función lineal, monotónica de y**
– Cada cuadrado aporta una tira rectangular `[x, x+l] × [y, y+l]`.
– Al barrer `y` hacia arriba, el lapso horizontal de cuadrados activos (el *unión de x-intervalos*) cambia sólo en la parte inferior o superior de un cuadrado.

2. **La unión de x-intervalos es fácil de mantener con un árbol de segmento* *
– Comprendemos las coordenadas "x" (hay en los bordes más '2n' distintos).
– Cada evento (inicio o final de un cuadrado) actualiza un rango en el árbol: `+1` al entrar, `-1` al salir.
– El árbol mantiene la longitud total cubierta en el tiempo `O(log n).

3. **El área acumulativa entre dos eventos consecutivos es**
`cubierta Longitud × (y2 – y1)`.
– Mientras barremos podemos acumular este valor y detectar cuando el área acumulada alcanza ** la mitad** del área total de unión.

4. **El barrido de dos pasos es más simple* *
– Primer paso: computar el área total.
– Segundo paso: barrer de nuevo, parar cuando el área acumulada ≥ la mitad; interpolar dentro de la placa actual para encontrar el 'y' exacto.

-...

"algorithm"
## 3. Resumen del algoritmo

`` `
1. Construir dos listas de eventos: (y, x1, x2, delta)
delta = +1 en la parte inferior de la plaza, -1 en la parte superior de la plaza.

2. Compre todas las coordenadas x → xs[0 ... m-1] ordenados & únicos.

3. Segmento Árbol sobre xs:
- Contando. cuántos intervalos cubren este nodo
- longitud [nodo] : total x longitud cubierta por intervalo de nodo

4. Primer paso (para calcular el área total):
- Más o menos eventos.
- prevY = eventos[0]. Sí.
- área = 0
- Para cada evento e:
cubiertos = segTree.totalCovered()
área += cubierta * (e.y - prevY)
segTree.update(range x1→x2, delta)
prevY = e.y
- totalArea = área
- mitad = totalArea / 2

4. Segundo paso (para localizar la línea dividida):
- Reinicializar el árbol del segmento, barrer de nuevo.
- cum = 0
- Para cada evento e:
cubiertos = segTree.totalCovered()
slabHeight = e.y - prevY
si está cubierto 0 y cum + recubierto * placaAltura mitad:
// y miente dentro de esta tabla
necesitado = mitad - cum
ySplit = prevY + necesario / cubierto
devolver ySplit
cum += cubierta * placaAltura
segTree.update(range x1→x2, delta)
prevY = e.y

// Si nunca cruzamos la mitad (por ejemplo, toda la zona concentrada en un solo y),
// simplemente devolver el último evento's y (caso principal).
`` `

*Por qué funciona la interpolación*
Dentro de una losa la longitud cubierta es constante.
La zona aumenta linealmente con `y`.
Si necesitamos `need` más área, la altura extra es `neced / coveredLength`.

-...

Identificar un nombre="walkthrough"
## 4. Recorrido detallado

Silencio Lo que está pasando Silencio ¿Por qué importa
Silencio...
Silencio **Evento la creación** Silencio Por cada cuadrado `(x, y, l)` añadir: `(y, x, x+l, +1)` y `(y+l, x, x+l, -1)` Los eventos permanentes indican cuando una plaza se vuelve activa o inactiva. Silencio
Silencio **X-coordinate compresión** Silencio Todo distinto `x` y `x+l` ordenados → `xs`. Silencio El árbol del segmento funciona en índices, no coordenadas crudas. Silencio
tención ** Interiores de árboles de sedimento**
`tree[v]` – longitud total cubierta en el intervalo del nodo
«cnt[v]` – cuántos intervalos activos cubren este nodo ANTERIOR Cuando `cnt[v] ître 0`, el nodo está completamente cubierto; de lo contrario sumamos niños. Silencio
Silencio **Primero paso – área total** Silencio Sumérgete de la más pequeña `y` a la más grande, actualizando el árbol y agregando `cubierta × Δy` a `rea`. Silencio da 'totalArea'. Silencio
Silencio ** Segundo paso – encontrar división** Silencio Reinicializar el árbol, repetir barrido.
Cuando el área acumulativa `cum` satisfies `cum + covered × Δy ≥ half`, compute exact `y`. ← Stops early – no need to store all slabs. Silencio
Silencio **Interpolación** Silencio `y = prevY + (half - cum) / covered`. Silencio Exact `y` dentro de la losa; garantiza la precisión hasta 1e‐5. Silencio

-...

"Nombre="complejidad"
## 4. Análisis de la complejidad

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio Generación de eventos en `O(n)` Silencio
Silencioso X‐compresión Silencioso `O(n log n)` Silencio
← Actualizaciones de los árboles de Segment Silencioso `O(log n)` cada  durable `O(n)` (array of size `4·m`) Silencio
Silencio Primer barrido: `O(n log n)` extra confidencialidad
Silencio Segundo barrido Silencioso `O(n log n)` extra confidencialidad

*Total*
`Time : O(n log n) `
`Pace: O(n)`

Con `n = 5·104` esto encaja cómodamente con los límites de LeetCode.

-...

"Nombre="pitfalls"
## 5. Pitfalls comunes

Silencio Pitfall Silencio Cómo evitar
Silencio...
Silencio **Using `int` for coordinates/lengths** Silencio Coordinates up to `109`; their sum can be `2·109`. Use `long` (Java) or `int64_t` (C++). Silencio
Silencio **No manejo de la duración no cubierta** En una losa sin plazas activas, `coveredLength = 0`. Skip interpolation and continue to next event. Silencio
Silencio **Overflow during area computation** tención Use `long` for lengths, cast to `double` only when multiplicaing by height. `doble` puede representar hasta `1e308`. Silencio
Silencio **Wrong range update semantics** Silencio La actualización del árbol del segmento debe ser *half‐open* `[l, r)`; el intervalo de hoja es entre `xs[i]` y `xs[i+1]`. Silencio
Silencio **Precisión de punto flotante** Silencio La respuesta debe ser exacta a `1e‐5`. La fórmula de interpolación utiliza la división doble, segura para la precisión necesaria. Silencio

-...

Identificar un nombre= "java-code"
## 6. Código - Java

``java
importar java.util*;
importa java.io.*;

Clase Solución {
// Evento: cambio de cobertura en un y dado
Clase privada estática Evento {}
long y, x1, x2;
int delta; // +1 al entrar, -1 al salir

Event(long y, long x1, long x2, int delta) {}
esto.y = y;
esto.x1 = x1;
esto.x2 = x2;
esto. delta = delta;
}
}

// Árbol de segmento que mantiene total cubierta x‐length
Clase estática privada SegmentTree {
final largo[] xs; // comprimidas x coordenadas
int n final; // número de xs
final int[] cnt; // cobertura contador
longitud final[] len; // longitud cubierta

SegmentTree(long[] xs) {
esto.xs = xs;
esto.n = xs.length;
int size = 4 * n;
cnt = nuevo int[size];
len = nuevo largo [tamaño];
}

// update [l, r) by delta
vaciado (nodo, int l, int r, int ql, int qr, int delta) {}
si regresan (qr <= l vivienda ql не= r)
si
cnt[nodo] += delta;
. ♫ ... {
int mid = (l + r) 1;
actualización (nodo) realizada 1, l, mediados, ql, qr, delta);
actualización (nodo) se llevó a cabo 1 tención 1, mitad, r, ql, qr, delta);
}
si (cnt[node] 0) {
len[node] = xs[r] - xs[l];
} si (r - l == 1) {
len[node] = 0;
. ♫ ... {
len[nodo] = len[nodo] = 1] + len[nodo] se indica 1 .
}
}

total Covered() {}
len de retorno[1];
}
}

public double separateSquares(int[] [] squares) {
int n = cuadrados. longitud;
// Construir eventos
Lista seleccionadaEvento relativo ev = nuevo ArrayList implicado(2 * n);
long[] xsRaw = new long[2 * n];
int idx = 0;
para (int[] sq : cuadrados) {}
x largo = sq[0];
long y = sq[1];
long l = sq[2];
x1 largo = x;
x2 largo = x + l;
ev.add(nuevo evento(y, x1, x2, +1));
ev.add (new Event(y + l, x1, x2, -1));
xsRaw[idx++] = x1;
xsRaw[idx++] = x2;
}

// Compresora x
largo[] xs = compress(xsRaw);

// Primer barrido – área total de carga
doble totalArea = computeArea(ev, xs, n);

doble media = totalArea / 2.0;

// Segundo barrido: encontrar la línea de división
respuesta doble = findSplit(ev, xs, half, n);
respuesta de retorno;
}

static long[] compresss(long[] raw) {
Arrays.sort(raw);
int m = 0;
para (int i = 0; i)
si [i]!= crudo [i - 1]
crudo[m+] = crudo[i];
}
}
devolver Arrays.copyOf(raw, m);
}

computación doble estática privadaArea(Listitud seleccionadaEventilo ev, long[] xs, int n) {
ev.sort(Comparator.comparingLong(a - título a.y));
Segmento Tree st = nuevo SegmentTree(xs);
largo prevY = ev.get(0).y;
zona doble = 0,0;

para (Evento e : ev) {
largo cury = e.y;
Long coveredLen = st.totalCovered();
area += coveredLen * (double) (curY - prevY);

st.update(1, 0, xs.length - 1,
Arrays.binarySearch(xs, e.x1),
Arrays.binarySearch(xs, e.x2),
e.delta);
PrevY = cury;
}
zona de retorno;
}

encontrar doble estática privadaSplit(List wonEvencio ev, long[] xs,
doble mitad, int n) {
ev.sort(Comparator.comparingLong(a - título a.y));
Segmento Tree st = nuevo SegmentTree(xs);
largo prevY = ev.get(0).y;
doble cum = 0,0;

para (Evento e : ev) {
largo cury = e.y;
Long coveredLen = st.totalCovered();
larga delta Y = cury - prevY;
si (cubiertoLen 0) {
doble necesidad = mitad - cum;
si (necesitado) {
retorno prevY + necesidad / cubierto Len;
}
cum += coveredLen * (double) delta Y;
}

st.update(1, 0, xs.length - 1,
Arrays.binarySearch(xs, e.x1),
Arrays.binarySearch(xs, e.x2),
e.delta);
PrevY = cury;
}
// Todo el área en una sola línea horizontal – retorno último y
ev.get(ev.size() - 1).y;
}

// Ayudante: encontrar índice de un valor en xs comprimidos
privada estática int idx(long[] xs, long val) {
devolver Arrays.binarySearch(xs, val);
}
}
`` `

**Explicación de partes clave**

- `computeArea` utiliza la misma lista de eventos para evitar la reconstrucción; simplemente re-ordenarlo.
- `Arrays.binarySearch(xs, value)` devuelve el índice comprimido de una coordenadas crudas.
- El árbol del segmento utiliza rangos medio abiertos; la raíz cubre `[0, xs.length-1)` (es decir, entre la primera y última coordenadas comprimidas).

-...

Identificar un nombre="cxx-code"
## 7. Código: C++

``cpp
#include יbits/stdc++.h
usando std namespace;

struct Event {
largo y, x1, x2;
int delta; // +1 al entrar, -1 al salir
Evento(largo y, largo largo x1, largo x2, int delta)
: y(y), x1(x1), x2(x2), delta(delta) {}
};

struct SegTree {
vector de const obtenidos largo tiempo &xs; // coordenadas comprimidas
int n; // número de xs
vector asignadoint título cnt; // cobertura contador
vector de longitud larga duración del título; // longitud cubierta

SegTree(cont vector consignalong long &xs) : xs(xs) {
n = xs.size();
int sz = 4 * n;
cnt.assign(sz, 0);
len.assign(sz, 0);
}

actualización de vacío(en nodo, int l, int r,
int ql, int qr, int delta) {}
si regresan (qr <= l vivienda ql не= r)
si
cnt[nodo] += delta;
. ♫ ... {
int mid = (l + r) 1;
actualización (nodo) realizada 1, l, mediados, ql, qr, delta);
actualización (nodo) se llevó a cabo 1 tención 1, mitad, r, ql, qr, delta);
}
si (cnt[node] 0) {
len[node] = xs[r] - xs[l];
} si (r - l == 1) {
len[node] = 0;
. ♫ ... {
len[nodo] = len[nodo] = 1] + len[nodo] se indica 1 .
}
}

larga duración total Covered() const { return len[1]; }
};

vector realizado largamente compresss(vector realizado largo tiempo gris) {
(raw.begin(), raw.end());
raw.erase(unique(raw.begin(), raw.end()), raw.end());
retorno crudo;
}

doble computación Area(vector seleccionadoEventilo ev, const vector obtenidos largamente largamente >
sort(ev.begin(), ev.end(), [](const Event &a, const Event &b){
devolver a.y
});

SegTree st(xs);
largo tiempo antes = ev[0].y;
zona doble = 0,0;

para (continuo automático : ev) {
largo largo cury = e.y;
largo tiempo cubierto = st.totalCovered();
área += cubierta * doble(curY - prevY);

int l = lower_bound(xs.begin(), xs.end(), e.x1) - xs.begin();
int r = lower_bound(xs.begin(), xs.end(), e.x2) - xs.begin();
st.update(1, 0, xs.size() - 1, l, r, e.delta);
PrevY = cury;
}
zona de retorno;
}

encontrar dobleSplit(vector seleccionadoEvent confianza ev,
const vector se llevó mucho tiempo xs,
doble mitad) {}
sort(ev.begin(), ev.end(), [](const Event &a, const Event &b){
devolver a.y
});

SegTree st(xs);
largo tiempo antes = ev[0].y;
doble cum = 0,0;

para (continuo automático : ev) {
largo largo cury = e.y;
largo tiempo cubierto = st.totalCovered();
delta larga Y = cury - prevY;
si (cubierto √≥ 0 ' qum + cubierto * doble(deltaY) mitad) {
doble necesidad = mitad - cum;
volver prevY + necesidad / cubierta;
}
cum += cubierto * doble(deltaY);

int l = lower_bound(xs.begin(), xs.end(), e.x1) - xs.begin();
int r = lower_bound(xs.begin(), xs.end(), e.x2) - xs.begin();
st.update(1, 0, xs.size() - 1, l, r, e.delta);
PrevY = cury;
}
// Caso de borde: toda la zona concentrada en un solo y
ev.back().y;
}
`` `

**Puntos clave* *

- `lower_bound` obtiene el índice comprimido.
- `SegTree` utiliza `xs.size() - 1` como el índice más adecuado porque cada hoja representa `[xs[i], xs[i+1])`.

-...

Identificar un nombre="cxx-code"
## 8. Código: C++

``cpp
#include יbits/stdc++.h
usando std namespace;

// -------- Evento...
struct Event {
largo y, x1, x2;
int delta; // +1 entrando, -1 saliendo
Evento(largo y, largo largo x1, largo x2, int delta)
: y(y), x1(x1), x2(x2), delta(delta) {}
};

// -------- Segment Tree...--------
struct SegTree {
vector de const obtenidos largo tiempo &xs; // comprimido x
vector asignadoint confianza cnt; // cobertura con
vector de longitud larga duración del título; // longitud cubierta

SegTree(cont vector consignalong long &xs) : xs(xs) {
int sz = 4 * xs.size();
cnt.assign(sz, 0);
len.assign(sz, 0);
}

vaciado (en nodo, int l, int r, int ql, int qr, int delta) {}
si regresan (qr <= l vivienda ql не= r)
si
cnt[nodo] += delta;
. ♫ ... {
int mid = (l + r) 1;
upd(node Identificado 1, l, mid, ql, qr, delta);
upd(node Identificado) 1 tención 1, mid, r, ql, qr, delta);
}
si (cnt[node] 0) {
len[node] = xs[r] - xs[l];
} si (r - l == 1) {
len[node] = 0;
. ♫ ... {
len[nodo] = len[nodo] = 1] + len[nodo] se indica 1 .
}
}

long long covered() const { return len[1]; }
};

// Ayudantes...
vector realizado largamente compresss(vector realizado largo tiempo gris) {
(raw.begin(), raw.end());
raw.erase(unique(raw.begin(), raw.end()), raw.end());
retorno crudo;
}

doble compute_area(vector seleccionadoEvento confianza ev, const vector obtenidoslong prendas de vestir) {
sort(ev.begin(), ev.end(), [](const Event &a, const Event &b){
devolver a.y
});

SegTree st(xs);
largo tiempo prevY = ev.front().y;
zona doble = 0,0;

para (continuo automático : ev) {
largo largo cury = e.y;
long long cov = st.covered();
area += cov * double(curY - prevY);

int l = lower_bound(xs.begin(), xs.end(), e.x1) - xs.begin();
int r = lower_bound(xs.begin(), xs.end(), e.x2) - xs.begin();
st.upd(1, 0, xs.size() - 1, l, r, e.delta);
PrevY = cury;
}
zona de retorno;
}

doble find_split(vector seleccionadoEvent confianza ev, const vector xs,
doble mitad) {}
sort(ev.begin(), ev.end(), [](const Event &a, const Event &b){
devolver a.y
});

SegTree st(xs);
largo tiempo prevY = ev.front().y;
doble cum = 0,0;

para (continuo automático : ev) {
largo largo cury = e.y;
long long cov = st.covered();
delta larga Y = cury - prevY;

si (cov ≤ 0 " sensible + cov " doble(deltaY) mitad) {
doble necesidad = mitad - cum;
volver prevY + necesidad / cov;
}
cum += cov * double(deltaY);

int l = lower_bound(xs.begin(), xs.end(), e.x1) - xs.begin();
int r = lower_bound(xs.begin(), xs.end(), e.x2) - xs.begin();
st.upd(1, 0, xs.size() - 1, l, r, e.delta);
PrevY = cury;
}
retorno ev.back().y; // borde caso
}

// -------- Principal...
int main() {}
ios::sync_with_stdio(false);
cin.tie(nullptr);

int N; // número de rectángulos
si (!(cin ≤ N)) devuelve 0;
vector:
vector de larga duración crudo;
para (int i = 0; i)
largo x1,y1,x2,y2;
cin √≥ contactos x1 √≥ título y1 нелили x2 y2;
ev.emplace_back(y1, x1, x2, +1);
ev.emplace_back(y2, x1, x2, -1);
raw.push_back(x1);
raw.push_back(x2);
}

vector realizado largo tiempo xs = compress(raw);
doble total = compute_area(ev, xs);
doble media = total / 2.0;
respuesta doble = find_split(ev, xs, half);

cout.setf(ios::fixed); cout se hizo la precisión establecida(6)
retorno 0;
}
`` `

Compile**

`` `
g++ -std=c+17 -O2 -Wall main.cpp -o main
`` `

-...

### 9. Análisis de la complejidad

- **Sorting events**: \(O(N \log N)\)
- **Arbol de segmento de construcción**: \(O(N)\) (una vez por barrido)
- **Suerte**: cada evento activa una actualización del árbol - \(O(\log N)\)
- **Total**: \(O(N \log N)\) time, \(O(N)\)

Con \(N \le 10^5\), esto satisface fácilmente los límites.

-...

#### 10. Observaciones finales

- La técnica de barrido de línea gira un geométrico aparentemente bidimensional
problema en una secuencia de actualizaciones 1-dimensionales, permitiendo un
\(O(N\log N)\) solución.
- Usando un array de *diferencia* para el cubículo x simplifica el
aplicación y garantiza la memoria lineal.
- La solución funciona para cualquier coordenadas entero dentro de los límites
\([0,10^9]\) y es robusto contra casos degenerados donde todo el área es
concentrado en una sola línea horizontal.