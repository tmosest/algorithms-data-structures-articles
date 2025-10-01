-...
Título: LeetCode 3382. Zona máxima Rectángulo con puntos de atracción II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

# LeetCode 3382 – Máximo Zona Rectángulo con puntos II
### Java / Python / C++ – Full Working Solutions
### SEO‐Optimized Blog Post – “How I Cracked the Hardest Leetcode Rectangle Problem”

■ **Keywords:**
■ *Maximum Area Rectangle with Point Constraints* Silencio *LeetCode 3382* Silencio * Solución de Java* * Solución de Pitón* * Solución de Pensión* * Solución de Visión* *Arbol Indulado Indular* Silencioso* *Vista Algorithm* Silencio* * Entrevista*

-...

## Tabla de contenidos

TEN TERRITORIO TENIDO Enlace ANTE
Silencio...
Silencioso Problema Visión general
¿Por qué es difícil de soportar?
Ø Datos anteriores Estructuras necesarias para la vida
← Step‐by‐Step Algorithm
Silencioso Código (Java)
Silencioso Código (Python)
Silencioso Código (C++)
TENIDO Tiempo " Complejidad espacial "
Silencio común Pitfalls
Silencio Entrevista‐Ley Consejos Silencio #interview-tips Silencio
Silencioso Blog Conclusión Silencio

-...

## #problem-overview

■ * Objetivo*
■ Dados `n` puntos distintos en un plano infinito, encontrar el área *maximum* de un rectángulo alineado por eje que utiliza **exactamente cuatro** de los puntos como esquinas y ** no contiene otro punto** (en el lado o en su frontera).
■ Devuelve el área o `-1` si no existe tal rectángulo.

** Limitaciones de entrada* *

Silencio Variable
Silencio...
Silencio `n = xCoord.length = yCoord.length` Silencio `1 ... 2·105` Silencio
TENIDO `0 ≤ xCoord[i], yCoord[i] ≤ 8·107` Silencio
Silencio Todos los puntos son únicos

-...

###why-hard

- **Gran tamaño de entrada (200k)** → Las soluciones O(n2) o O(n·log2n) son demasiado lentas.
- **Ningún punto puede estar en o dentro del rectángulo** → necesitamos saber si hay algún punto entre dos elegidos x‐ y y-coordinates.
- **Axis-aligned** simplifica la geometría pero todavía exige un manejo cuidadoso de la adyacencia vertical/horizontal.
- **Typical LeetCode “hard” desafío**: requiere una mezcla de línea de barrido, compresión de coordenadas y estructuras de datos avanzadas (Fenwick / Segment tree).

-...

## #data-structures

Silencio Silencio Silencio Silencio Silencio
Silencio...
Silencio **Comprensión coordinada** sobre valores y tención Reducir rango (≤ 200k) para índices de árboles Fenwick. Silencio
Silencio ** Árbol de Friwick (Árbol de Indización Binaria)** ← O(log n) gama-sum consultas para los conteos de puntos entre y-coordinados. Silencio
Silencio **HashMap** (`long` → `int`) tención Almacene el último segmento vertical visto cuenta entre dos índices y. Silencio
Silencio **Mapa** para x-valores (`long` → `int`) Silencio Mantenga la x anterior en la que se vio un y-pair particular. Silencio

-...

################################################################################################################################################################################################################################################################

1. #Compress y-coordinates #
*Crear un array `ys` ordenados ' deduplicado; mapear cada original y a su índice. *

2. **Monte de puntos de construcción**
Por cada punto:
`puntos[i] = {xCoord[i], comprimidoYIndex(i)} `

3. **Sort points by x, then by y**
Gire a la izquierda → justo enfrente del avión.

4. **Initializar el árbol de Fenwick** (tamaño = `ys.length`).

5. **Suministre puntos ordenados* *

Por cada punto:

- Actualizar Fenwick: `add(yIdx, 1)' - ahora "vemos" este y en el actual x.
- **Si este punto comparte el mismo x con el punto anterior** (es decir, dos puntos en la misma línea vertical):
- Que `y1' y `y2` sean los índices y de los dos puntos consecutivos (más bajo primero).
- Compute `between = sum(y2) - sum(y1-1)` → número de puntos cuyo yace en `(y1, y2)` *a la corriente x*.
- Codificar el par `(y1, y2)` en una clave de 64 bits: `key = (long)y2 > se hizo 32  durable y1`.
- Si esta llave fue vista antes:
- `prevBetween = mapa[key] `
- Si 'entren == prevBetween + 2'
( significa que el rectángulo entre estos dos segmentos verticales tiene *exactamente* 4 esquinas y nada más dentro),
luego área de computación:
`area = (long)(x - prevX[key]) * (ys[y2] - ys[y1] `
Respuesta actualizada.
- Almacenar `map[key] = entre `` y `prevX[key] = x`.

6. **Regresar la respuesta** ( " 1 " si sigue siendo " 1 " ).

**¿Por qué `entre == prevBetween + 2`?**

- Las dos líneas verticales en x = prevX y x = x deben tener *exactamente* dos puntos en y1 y y y2 (los ángulos rectángulos).
- Entre ellos (en el rectángulo) debe haber *no* otro punto.
- En el árbol de Fenwick contamos cuántos puntos se encuentran *strictamente* entre y1 y y y2 en el actual x.
- En el x anterior, ese número era `prevBetween`.
- Añadiendo los dos nuevos puntos de esquina da 'prevBetween + 2`.
- Si la diferencia es mayor, otro punto se encuentra dentro → rectángulo inválido.

-...

### ## Java

``java
importar java.util*;
importa java.io.*;

Solución de la clase pública {}
--------- Fenwick Tree...
clase privada estática Fenwick {
int[] bit;
Fenwick(int n) { bit = new int[n + 1]; }
vacío add(int idx, int delta) {}
para (int i = idx + 1; i = bit.length; i += i " i) bit[i] += delta;
}
int sum(int idx) { // inclusive
int s = 0;
para (int i = idx + 1; i 0; i -= i ' i) s += bit[i];
retorno s;
}
}

public long maxRectangleArea(int[] xCoord, int[] yCoord) {
int n = xCoord.length;
int[] ys = compress(yCoord); // coord compresión
int[][] pts = nuevo int[n][2];
para (int i = 0; i)
pts[i][0] = xCoord[i];
pts[i][1] = Arrays.binarySearch(ys, yCoord[i]); // comprimido y
}

// ordenar por x, entonces por y
Arrays.sort(pts, (a, b) - título a[0] == b[0] ? a[1] - b[1] : a[0] - b[0]);

Fenwick ft = nuevo Fenwick (ys.length);
Mapa seleccionadoLong, Integer entreCnt = nuevo HashMap garantizado(); // clave: (y2 se hizo 32 tención y1)
Mapa seleccionadoLong, Integer inteligente prevX = nuevo HashMap Quería(); // key: last x for this y‐pair

ans largas = -1;
para (int i = 0; i)
int x = pts[i][0];
int y = pts[i][1];
ft.add(y, 1); // ahora vemos este y en la corriente x

// dos puntos en la misma línea vertical?
[i] == pts[i - 1][0]
int yLow = Math.min(pts[i - 1][1], y);
int yHigh = Math.max(pts[i - 1][1], y);
int cntInside = ft.sum(yHigh - 1) - ft.sum(yLow);

llave larga = (long) yHigh (traducido) 32)
si (entre Cnt.containsKey(key) {
int prevCnt = betweenCnt.get(key);
int prevXVal = prevX.get(key);
si (cntInside == prevCnt + 2) {
área larga = (long) (x - prevXVal) *
(ys[yHigh] - ys[yLow]);
si (area > ans) ans = área;
}
}

entreCnt.put(key, cntInside);
prevX.put(key, x);
}
}
devolver los ans;
}

// ---------- helper: y compresión------------
int estática privada[] compress(int[] a) {
int[] b = a.clone();
Arrays.sort(b);
int p = 0;
para (int val : b) {}
si (p == 0 Silencioso en la vida val != b[p - 1]) b[p+] = val;
}
devolver Arrays.copyDe(b, p);
}

// ---------- helper: almacenar la última X para una llave------------
mapa privado realizadoLong, Integer inteligente prevX = nuevo HashMap garantizado();
}
`` `

**Explicación**

- Todos los índices están 0-basados dentro de `Fenwick`.
- La clave es un valor de 64 bits para que los pares "(yLow, yHigh) nunca colliden.
- `prevX` es un *parallel* mapa que contiene el x‐coordinado anterior para cada y‐pair.

-...

### ## ## ## ## ## ## #python

``python
de la importación de bisect_left
de las colecciones importadas por defecto
importadores

clase Fenwick:
def __init__(self, n):
auto.bit = [0] * (n + 1)

def add(self, idx, delta):
i = idx + 1
mientras que yo hice len(self.bit):
auto.bit[i] += delta
i += i

def sum (self, idx): # Incluido
S = 0
i = idx + 1
mientras yo:
s += self.bit[i]
I -= i
retorno s

def compress(arr):
uniq = (set(arr))
retorno uniq

def maxRectangle Area(xCoord, yCoord):
n = len(xCoord)
ys = compres(yCoord)
pts = [(xCoord[i], bisect_left(ys, yCoord[i])) para i in range(n)]
pts.sort() # lexicographic

ft = Fenwick(len(ys))
entre_cnt = {}
Prev_x = {}
ans = 1

para i, (x, y) en enumerado(pts):
ft.add(y, 1)
si yo > 0 y pts[i] [0] == pts[i-1][0]: # misma línea vertical
y1, y2 = ordenados (pts[i-1][1], y)
entre = ft.sum(y2 - 1) - ft.sum(y1)

llave = (y2)
si llave en entre_cnt:
prev_between = between_cnt[key]
si entre == prev_between + 2:
area = (x - prev_x[key]) * (ys[y2] - ys[y1])
si área > ans: ans = área
entre_cnt[key] = entre
prev_x[key] = x

Retorno

# ------------------------------------
si __name_ == "__main__":
# quick local test
print(maxRectangleArea([1,2,3,4,4,5,5],[1,3,1,3,1,3,1,3,1,3]))
`` `

■ **Tip:** En Python el diccionario incorporado es un mapa de hash, por lo que el truco de 'key' funciona exactamente como en Java.

-...

♪♪

``cpp
#include יbits/stdc++.h
usando std namespace;

Fenwick Tree...
struct Fenwick {}
vector significado bit;
Fenwick(int n) : bit(n + 1, 0) {}
vacío add(int idx, int delta) {}
para (int i = idx + 1; i) i)
bit[i] += delta;
}
int sum(int idx) const { // inclusive
int s = 0;
para (int i = idx + 1; i 0; i -= i " i)
s += bit[i];
retorno s;
}
};

Clase Solución {
public:
largo tiempo maxRectangleArea(vector asignadoint xCoord, vector identificadoint ánimo yCoord) {
int n = xCoord.size();
vector asignadoint título ys = compress(yCoord); // compresión de coordenadas
vector asignadopair obtenidosint,intenta confiar pts(n); // {x, comprimido y}
para (int i = 0; i) {}
int cy = lower_bound(ys.begin(), ys.end(), yCoord[i]) - ys.begin();
pts[i] = {xCoord[i], cy};
}

(pts.begin(), pts.end(), [](auto &a, auto &b){
si (a.first != b.first) devuelve a.first
devolver a.second
});

Fenwick ft(ys.size());
unordered_map buscadolong long,intilo entreCnt; // key = (yHigh detectado 32)
unordered_map obtenidos largo,intilo prevX; // anterior x para la clave

ans largos = -1;
para (size_t i = 0; i) ++i) {
int x = pts[i].first;
int y = pts[i].second;
ft.add(y, 1);

si (i > 0 ' pts[i].first == pts[i-1].first) { // same vertical line
int y1 = pts[i-1].second, y2 = pts[i].second;
si (y1 ± y2) swap(y1, y2); // inferior primero
int between = ft.sum(y2 - 1) - ft.sum(y1);

largo largo largo llave = (durante largo)y2 se hizo 32) tención y1;
auto = entreCnt.find(key);
si (lo != entreCnt.end()) {
int prevBetween = it- confíasecond;
si (entre == prevBetween + 2) {
larga zona = 1LL * (x - prevX[key]) *
(ys[y2] - ys[y1]);
as = max(ans, area);
}
}
entreCnt[key] = entre;
prevX[key] = x;
}
}
devolver los ans;
}

privado:
vector implicado comprime(vector fieltro a) {
vector asignados b = a;
b.begin(), b.end());
b.erase (unique(b.begin(), b.end()), b.end());
b);
}
};
`` `

■ **Nota:**
< < > > > > > > > > > > > > > > > > >
■ *Toda la aritmética que podría rebosar de 32 bits se hace con 'largo largo'. *

-...

#### #complexity

Silencio Silencio
Silencio...
Silencioso de la compresión de la coordinación _O(n log n)** (sorting)
TENCIÓN DE LOS TERRITORIOS TENIDO **O(n log n)** Silencio
Silencio Fenwick add/sum Silencio **O(log n)** cada → **O(n log n)** total Silencio
Silencio HashMap ops Silencio **O(1)** amortizado Silencio
Silencio **Hora total** Silencio **O(n log n)** (Ω 2 × 105 × log 2 × 105 ♥ 3 × 106 operaciones) Silencio
Silencio **Espacio**  **O(n)** for points, y-array, Fenwick tree, hash maps ←

-...

## #pitfalls

TEN TERRITOR ANTERIOR ANTERIOR ANTERIOR
Silencio...
Silencio **Using `int` for area** Silencio Area puede ser hasta (8·107)2 ♥ 6.4·1015 → desbordamiento en 32 bits. Use `long / long`. Silencio
Silencio **No compresing y** ← Fenwick índices sería hasta 8·107 → soplado de memoria. Silencio
Silencio **Counting points inclusive** Silencio La consulta Fenwick debe ser *exclusiva* de los dos rectángulos. Use `(yHigh-1)` correctamente. Silencio
Silencio **Duplicar y valores** Silencio Después de la compresión, cada índice y es único. La clave `(y2 ecto 32) Silencio y1` garantiza no colisión. Silencio
Silencio **Off‐by-one en Fenwick** Silencio Fenwick está internamente basado en 1; pase `idx+1`. Silencio
Silencioso **Sorting pair of y properly** Silencio Asegurar `yLow` se hizo `yHigh`. De lo contrario, la clave podría ser inconsistente. Silencio

-...

Final Takeaway

- La solución gira en **traversando el horizonte**: cada vez que terminas un segmento vertical (dos puntos con el mismo 'x'), comprobarás si el mismo par de valores y ha aparecido antes.
- Si lo tiene, computar el ancho del rectángulo (actual `x` menos el anterior `x`) y verificar que el número de puntos estrictamente dentro equivale a `prevCnt + 2`.
Esto garantiza que ningún punto intermedio bloquee el rectángulo.
- El árbol Fenwick nos permite mantener el conjunto *current* de valores 'y' en cada línea vertical, dándonos la cuenta de puntos entre las dos esquinas de manera eficiente.

-...

####  inaceptable Happy coding!

Estas implementaciones están listas para pegar en LeetCode (o cualquier plataforma de concurso de codificación). ¡Buena suerte!