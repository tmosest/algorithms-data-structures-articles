-...
Título: LeetCode 2055. Placas entre velas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Solution Idea – O(n + q)**

Por cada consulta `(l, r)` necesitamos

* la primera `vida' en o después de 'I' – llámalo **L**
* el último `vivir' en o antes de 'r' – llamarlo **R**
* the number of `*` between **L** and **R**.

Si tal par de tuberías no existe (no hay `vivir' a la izquierda de `r` o no `vivir' a la derecha de `l') la respuesta es `0`.

Toda la información que necesitamos se puede obtener en un solo escaneo de la cadena:

Silencio variable Silencio descripción Silenciosos construcción Silencio
Silencio----------------------------------
Silencioso `nextPipe[i]` distancia de `i` a la **soportada `a la derecha** (incluido ella misma). '-1' si ninguno. Escaneo permanente de derecha a izquierda. Silencio
Silencioso `prevPipe[i]` distancia de `i` a la **soportada `a la izquierda** (incluido ella misma). '-1' si ninguno. Escaneo permanente de izquierda a derecha. Silencio
Silencioso `starPref[i] tención número de `* **strictly before** posición `i ' (i.e. in `[0 , i)`). Silencioso prefijo estándar suma. Silencio

Con estos tres arrays cada consulta es contestada en O(1).

-...

#### Pre-procesamiento (O(n))

``cpp
int n = s.size();
vector asignadoint espíritu estrellaPref(n + 1, 0); // starPref[0] = 0
vector implicado siguientePipe(n, -1); // distancia a la siguiente ' '
vector implicado prevPipe(n, -1); // distancia a la anterior ' '

int lastPipe = -1; // la distancia a la "última" más cercana a la izquierda
para (int i = 0; i) {}
si (s[i] == '*)
starPref[i + 1] = starPref[i] + 1;
más
starPref[i + 1] = starPref[i];

si (s[i] == 'vivir') últimoPipe = 0; // la posición actual es una tubería
si no (la última foto!= -1) ++lastPipe;
prevPipe[i] = lastPipe; // la distancia a la 'última' más cercana a la izquierda
}
`` `

``cpp
int nextPipeDist = -1;
para (int i = n - 1; i 0; --i) {
si (s[i] == 'vivir') siguientePipeDist = 0;
si no (nextPipeDist != -1) ++nextPipeDist;
siguientePipe[i] = siguientePipeDist; // distancia a la 'última' más cercana a la derecha
}
`` `

Ahora

* index of the first pipe after position `l` → `l + nextPipe[l]` (if `nextPipe[l] == -1` → sin tubería
* index of the last pipe before position `r` → `r - prevPipe[r] (if `prevPipe[r] == -1` → sin tubería

-...

##### Respuesta a una consulta (O(1))

``cpp
int left = queries[i][0];
int right = queries[i][1];

int afterL = (nextPipe[left] == -1) ? -1 : izquierda + siguientePipe[izquierda];
int beforeR = (prevPipe[right] == -1) ? -1 : derecha - prevPipe[right];

si (después de L == -1 Silencioso antesR == -1 Silencioso después deL нел ненный derecho ный habito antes deR нерентентентентентентентентентентеный izquierdo) {
ans[i] = 0; // no válido par de tuberías
. ♫ ... {
ans[i] = starPref[beforeR] - starPref[afterL];
}
`` `

La matriz 'starPref` se define de modo que `starPref[x]` equivale al número de `* **principalmente antes de la posición `x`.
Por lo tanto `starPref[beforeR] - starPref[afterL]` cuenta exactamente el `*` entre las dos tuberías.

-...

#### Complexity

*Time* : `O(n + q)` – un pase lineal para el preprocesamiento y uno para las consultas.
*Pace*: `O(n)` – tres conjuntos enteros de longitud `n`.

-...

#### Full C+++ implementation

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
placas vectoriales EntreCandles(cadenamiento s, vector asignadovector identificadoint sentido común implica consultas) {}
int n = (int)s.size();

--------- preprocesamiento...
vector implicado estrellaPref(n + 1, 0); // starPref[i] = # of '*' in [0, i)
vector implicado siguientePipe(n, -1); // distancia a la siguiente ' '
vector implicado prevPipe(n, -1); // distancia a la anterior ' '

int dist = -1; // la distancia a la "última" más cercana a la izquierda
para (int i = 0; i) {}
si (s[i] == '*)
starPref[i + 1] = starPref[i] + 1;
más
starPref[i + 1] = starPref[i];

si (s[i] == 'vivir') dist = 0;
si (dist!= -1) ++dista;
prevPipe[i] = dist; // distancia a la tubería más cercana en la izquierda
}

dist = -1; // ahora de derecha a izquierda
para (int i = n - 1; i 0; --i) {
si (s[i] == 'vivir') dist = 0;
si (dist!= -1) ++dista;
siguientePipe[i] = dist; // distancia a la tubería más cercana a la derecha
}

/* ---------- Respondiendo preguntas----------
vector implicado(queries.size(), 0);
para (int i = 0; i) ++i) {
int l = consultas[i][0];
int r = consultas[i][1];

int afterL = (nextPipe[l] == -1) ? -1 : l + nextPipe[l];
int beforeR = (prevPipe[r] == -1) ? -1 : r - prevPipe[r];

si (después de L == -1 Silenciosos antesR == -1 Silenciosos después deL нер нующе ный habit antes deR нелент l)
as[i] = 0;
más
ans[i] = starPref[beforeR] - starPref[afterL];
}
devolver los ans;
}
};
`` `

El código sigue el algoritmo descrito anteriormente y funciona en el espacio requerido `O(n + q)` tiempo y `O(n)`.