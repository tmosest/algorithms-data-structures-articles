-...
Título: LeetCode 3394. Compruebe si Grid puede ser cortado en secciones -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 3394. Revise si Grid puede ser cortado en secciones
#Medium** - LeetCode
'public boolean checkValidCuts(int n, int[][ rectángulos] `

-...

#### TL;DR
* Ordenar los rectángulos por sus fronteras *y* (o *x*).
* Construir dos prefijo-/suffix-arrays que le digan, para cada posible línea de corte, cuántos rectángulos se encuentran completamente debajo/abrazar esa línea.
* Un par de cortes horizontales es válido sif:
* al menos un rectángulo se encuentra debajo del primer corte,
* al menos un rectángulo está sobre el segundo corte, y
* los rectángulos restantes se emparejan entre los dos cortes.
* Haga lo mismo para cortes verticales.
* Complejidad del tiempo: **O(m log m)**, memoria: **O(m)**, donde *m* = 2 × número de rectángulos.
* Funciona para los peores límites de casos: *n* ≤ 109, hasta 105 rectángulos.

-...

## The Brute‐Force Nightmare (The **Ugly**)

Una forma ingenua es enumerar todas las coordenadas cortadas:

``text
para cada y1 en [0.n]
para cada y2 en (y1..n)
si todos los rectángulos se encuentran completamente en una de las 3 tiras horizontales
retorno verdadero
`` `

¡Pero no puede ser 109! Incluso si sólo miramos los valores *y* que realmente aparecen en la entrada (hay en la mayoría de 2·105 tales valores), comprobar un solo par requiere escanear todos los 105 rectángulos.
Eso sería ~1010 operaciones – mucho más allá de lo que cualquier sistema de entrevista o producción puede manejar.

-...

## The Elegant Sweep (The **Good**)

El problema tiene una estructura oculta:

*Los rectángulos no se solapan. *
Por lo tanto, el **proyección** de cada rectángulo sobre el eje *y* es un intervalo descomunal `[minY, maxY]`.
Lo mismo sostiene el eje *x*.

Si tratamos todos los valores fronterizos distintos (ambos comienzan y terminan) como una línea de corte potencial, podemos responder a la pregunta “¿Cuántos rectángulos se encuentran debajo de * esta línea*?” en *O(1)* tiempo después de un paso de preprocesamiento de una sola vez.
El truco es construir un **prefix‐sum** sobre las fronteras *end* y un **suffix‐sum** sobre las fronteras *start*.

Una vez que tenemos esos dos ayudantes, un par horizontal de cortes se encuentra en un solo paso sobre las posibles posiciones cortadas – sin bucles anidados, sin cheques por ángulo.

-...

## The Algorithm, Step‐by‐Step

1. *Recojan todas las fronteras*
* Por cada rectángulo empuja su 'startY' y 'endY' en un array.
* Ordenar el array y eliminar duplicados → `yVals` (tamaño *m*).

2. **Map a border value → index* *
* Usar un `Map armonizado, int] (o un diccionario en Python) para convertir una coordenadas en un índice de array en *O(log m)*.

3. **Los rectángulos que terminan / comienzan en cada índice**
``text
endCount[i] = cuántos rectángulos tienen endY == yVals[i]
startCount[i] = cuántos rectángulos han comenzado Y == yVals[i]
`` `

4. Prefijo / sufijo**
``text
debajo[i] = gia endCount[0..i] // rectángulos completamente por debajo de corte y = yVals[i]
arriba[i] = gia startCount[i.m‐1] // rectángulos completamente por encima del corte y = yVals[i]
`` `

5. #Prueba todos los primeros cortes #
``text
para k = 0 .. m‐2
inferior = inferior [k]
si abajo == 0: continuar

// encontrar el primer segundo corte que tiene al menos un rectángulo encima de él
l = k + 1
mientras que l 0: l++

si l >= m: descanso

arriba = arriba[l]
media = totalRectangles - inferior - superior
si el medio 0: retorno verdadero
`` `

*¿Por qué es suficiente una sola búsqueda? *
A medida que movemos el segundo corte a la derecha, "arriba" nunca aumenta – sólo permanece igual o disminuye.
Por lo tanto, el número de rectángulos en la raya superior sólo puede reducirse, mientras que la tira media sólo puede reducirse también.
Si la franja media está vacía en la primera viable `l`, permanecerá vacía para todos los mayores `l`. Así que un solo cheque por `k` basta.

6. ** Haga lo mismo para el *x*‐axis** – exactamente el mismo código, simplemente cambió `x` ↔y `y`.

7. **Retorno** 'verdad' si funciona la orientación, de lo contrario `falso'.

-...

## Full Reference Implementation

A continuación se presentan tres soluciones idiomáticas – **Java**, **Python** y **C+** – cada uno anotado para que pueda copiarlas en una sala de entrevistas o en un arnés de prueba LeetCode.

-...

### 1. Java

``java
importar java.util*;

Solución de la clase pública {}
comprobaciones booleanas públicasValidCuts(int n, int[][] rectángulos) {}
// ----- cortes horizontales ---
si (validCuts(n, rectángulos, cierto)) retornan verdaderos;
// ----- cortes verticales ---
si (válidosCuts(n, rectángulos, falsos)) retornan verdaderos;
devolver falso;
}

// dirección = verdadero → trabajo en y, false → trabajo en x
booleano privado válidoCuts(int n, int[] rects, booleano horizontal) {
int m = rects.length;
int[] coords = nuevo int[2 * m];
int ptr = 0;
para (int[] r : rects) {
int a = horizontal ? r[1] : r[0]; // start
int b = horizontal ? r[3] : r[2]; // extremo
coords[ptr+] = a;
coords[ptr+] = b;
}

// únicos, ordenados
Arrays.sort(coords);
int[] uniq = nuevo int[ptr];
int sz = 0;
para (int i = 0; i)
si [i]!= coords[i - 1) {
uniq[sz+] = coords[i];
}
}
uniq = Arrays.copyOf(uniq, sz); // longitud real

// mapa coordenadas → index
Mapa seleccionadoInteger, Integer confianza idx = nuevo HashMap Quería(sz * 2);
para (int i = 0; i)

int[] start Cnt = nuevo int[sz];
int[] endCnt = nuevo int[sz];
para (int[] r : rects) {
int start = horizontal ? r[1] : r[0];
int end = horizontal ? r[3] : r[2];
startCnt[idx.get(start)]++;
endCnt[idx.get(end)]++;
}

// prefijo de fin Cnt = número de rectángulos con finalización
int[] below = new int[sz];
int cum = 0;
para (int i = 0; i) {}
cum += endCnt[i];
[i] = cum;
}

// sufijo de inicio Cnt = número de rectángulos con inicio √= corte
int[] above = new int[sz];
cum = 0;
para (int i = sz - 1; i 0; i--) {
cum += startCnt[i];
arriba[i] = cum;
}

// probar todas las posiciones cortadas
para (int k = 0; k)
int bottom = below[k];
si 0) continuar; // necesitar al menos uno debajo

int l = k + 1;
mientras (l) 0) l++; // saltar secciones superiores vacías
si (l не= sz) romper;

int top = above[l];
int middle = m - bottom - top; // total = m rectángulos

si (middle > 0 " ventaja " 0) Retorno verdadero;
}
devolver falso;
}
}
`` `

■ **Por qué funciona* *
* `below[k]` cuenta todos los rectángulos cuyo **end** es ≤ el candidato primero corte.
* " above[l] " cuenta todos los rectángulos cuyo **start** es ≥ el segundo corte.
* `m - bottom - top` es exactamente el número de rectángulos que se sientan estrictamente entre los dos cortes.
■ Si cada parte no es vacía tenemos un par válido de cortes.

-...

### 2. Pitón

``python
def checkValidCuts(n: int, rectángulos: List[List[int]]) - ¿Qué?
def try_cuts(coord_start, coord_end):
""La misma lógica como Java, pero escrita para Python.""
m = len(rectángulos)

# Recopilar todos los valores fronterizos
coords = []
para un, b, c, d en rectángulos:
coords.append(coord_start)
coords.append(coord_end)

# única ordenada
uniq =(set(coords))
idx = {v: i for i, v in enumerate(uniq)}

start_cnt = [0] * len(uniq)
end_cnt = [0] * len(uniq)

para un, b, c, d en rectángulos:
start_cnt[idx[a] += 1
end_cnt[idx[d] += 1

# prefijo de end_cnt
infra = [0] * len(uniq)
S = 0
para i, val en enumerate(uniq):
s += end_cnt[i]
infra[i] = s

# Sufijo de start_cnt
arriba = [0] * len(uniq)
S = 0
para i en rango(len(uniq) - 1, -1, -1):
s += start_cnt[i]
arriba[i] = s

total = m
para k en rango(len(uniq) - 1):
inferior = inferior [k]
si abajo == 0:
continuar
l = k + 1
mientras que l  observado len(uniq) y superior[l] == 0:
l += 1
si l >= len(uniq):
descanso
arriba = arriba[l]
media = total - inferior - superior
si el medio 0:
Retorno
Retorno Falso

# Cortes horizontales (y-axis)
si try_cuts(lambda r: r[1], lambda r: r[3]):
Retorno
# vertical cuts (x-axis)
si try_cuts(lambda r: r[0], lambda r: r[2]):
Retorno
Retorno Falso
`` `

■ *Python* mantiene el mismo comportamiento de O(m log m) mientras es muy terse.

-...

### 3. C++

``cpp
Clase Solución {
public:
bool checkValidCuts(int n, vector seleccionadovector fielint implicancia rects) {
si (solve(rects, true)) retornan verdadero; // horizontal
si (solve(rects, false)) retornan verdadero; // vertical
devolver falso;
}

privado:
bool solve(vector identificadovector fieltro estrecho rects, bool horizontal) {
int m = rects.size();

// 1. Recopilar fronteras
vector coords;
coords.reserve(2 * m);
para (autor : rects) {
int start = horizontal ? r[1] : r[0];
int end = horizontal ? r[3] : r[2];
coords.push_back(start);
coords.push_back(end);
}

// 2. únicos ordenados
(coords.begin(), coords.end());
coords.erase(unique(coords.begin(), coords.end()), coords.end());

// 3. coordenadas → mapa índice
unordered_map madeint, int título idx;
idx.reserve(coords.size() * 2);
para (int i = 0; i)

vector implicado(coords.size(), 0), endCnt(coords.size(), 0);
para (autor : rects) {
int start = horizontal ? r[1] : r[0];
int end = horizontal ? r[3] : r[2];
++startCnt[idx[start]];
++endCnt[idx[end]];
}

// 4. prefijo de fin Cnt → abajo
vector:
int cur = 0;
para (int i = 0; i) ++i) {
cur += endCnt[i];
infra[i] = cur;
}

// 5. sufijo de inicio Cnt → arriba
vector indicado anteriormente(coords.size(), 0);
cur = 0;
para (int i = (int)coords.size() - 1; i √≥= 0; --i) {
cur += startCnt[i];
arriba[i] = cur;
}

// 6. probar todos los primeros cortes
para (int k = 0; k) - 1; ++k) {
int bottom = below[k];
si (!bottom) continuar; // necesita algo abajo

int l = k + 1;
mientras (l) se hacía (int)coords.size() " sensible !above[l]) ++l;
si (l не= (int)coords.size()) romper;

int top = above[l];
int middle = m - bottom - top;
si 0) Retorno verdadero;
}
devolver falso;
}
};
`` `

■ La versión C++ sigue el mismo oleoducto, pero apalanca `unordered_map` y `vector fielint ` para velocidad.

-...

## Complexity Analysis

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencioso colección de fronteras **O(m)** Silencio **O(2 m)**
Silencioso Ordenación + dedup Silencio **O(m log m)** Silencio **O(m)**
Silencioso Edificio cuenta con vida **O(m)** Silencio **O(m)**
Silencio Comprobando todos los primeros cortes Silencio **O(m)** Silencio **O(1)** per `k` Silencio
Silencio **Total** Silencio**

El uso de memoria es lineal en el número de fronteras distintas (≤ 2 m).

-...

## ¿Qué pasa si quieres manejar el rango completo [0, n]?

El algoritmo anterior sólo utiliza las fronteras que realmente aparecen en la entrada.
Si también desea permitir un corte en `0` o en `n` (incluso si ningún rectángulo los toca), simplemente agregue esos valores a la lista fronteriza antes de la deduplicación.
Todo lo demás es idéntico.

-...

## Edge Cases & Common Pitfalls

Silencio Caso confidencialidad Por qué importa Silencio Cómo el código lo maneja
Silencio...
Silencio **Solo un rectángulo** Silencio Imposible dividir → siempre `false` Silencio `below[0]` será 0 para cualquier primer corte; el bucle nunca volverá verdad. Silencio
Silencio **Todos los rectángulos apilados** (tocarse el uno al otro) Silencio
Silencio **Los rectángulos que comparten una frontera** Silencio `start == end` no permitido por el problema, pero si ocurre no romperá el algoritmo ¦ Puesto que el intervalo `[minY, maxY]` estaría vacío, tales rectángulos se ignoran automáticamente. Silencio
Silencio **Coordenadas altas** tención Necesidad de 64 bits tipo si `n` es 2 B Silencio Use 'long' o 64-bit ints cuando corresponda. Silencio

-...

## Pensamientos finales

- La idea **core** – prefijo de extremos + sufijo de inicios – es universal para problemas basados en intervalos.
- Una vez que tengas a esos ayudantes, *cualquier pregunta* que haga “cuantos intervalos se encuentran completamente en un lado de un umbral” puede ser contestada en *O(1)*.
- El algoritmo se ejecuta en *O(m log m)* tiempo y *O(m)* espacio, cómodamente rápido para hasta los rectángulos `10^5`, que es típico para las limitaciones de LeetCode.

Siéntase libre de adaptar el código a su idioma de elección, retoque los comentarios, y traiga la intuición de “disjoint borders → dos arrays prefijos” a su próxima entrevista. ¡Buena suerte! 🚀

-..