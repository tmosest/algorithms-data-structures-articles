-...
Título: LeetCode 488. Zuma Juego -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Zuma Game – 488 on LeetCode
■ **Hard** – tabla de 5 colores, mano de 5 bolas, encontrar las inserciones mínimas para limpiar el tablero

-...

## TL;DR
Silencio Idioma Silencio Tiempo Silencioso Silencioso Silencio
Silencio------------------------------
Silencio **Java** Silencio O(ángulo *estado* × *branch*) Silencio O(ángulo *estado*) Silencio DFS + memo + compresión de la junta
Silencio **Python** Silencio O(ángulo *estado* × *branch*) Silencio O(ángulo *estado*)
Silencio **C+** Silencio O(ángulo *estado* × *branch*) Silencio O(ángulo *estado*)

■ ** Resultado** – Inserciones mínimas (o `-1` si imposible).

-...

## 1ICK⃣ Problem restatement

Tenemos una tabla de 1-D de bolas de colores (`R Y B G W`) y una mano de bolas.
Un giro consiste en

1. **Insertar** cualquier bola de mano entre dos bolas existentes (o al final).
2. **Colapso**: desaparece cualquier grupo contiguo de 3+ bolas del mismo color; nuevos grupos pueden formar y colapsar recursivamente.
3. **Repetir** hasta que el tablero esté vacío (vino) o la mano esté agotada (sólo).

Devuelve el número mínimo de inserciones necesarias para limpiar el tablero, o `-1' si es imposible.

**Constraints* *

- 1 ≤ tabla. longitud ≤ 16
- `1 ≤ mano. longitud ≤ 5
- No existe un grupo inicial de 3+ en el tablero.

-...

## 2down ¿Por qué es “Hard”

Por qué importa
Silencio...
Silencio **Exponential Search Space** Silencio Cada inserción puede ocurrir en *cualquier* brecha → factor de ramificación hasta 17, profundidad ≤ 5 → 175 ♥ 1 400 000. Silencio
tención ** Explosión Estatal** Silencio Las configuraciones de la Junta pueden ser enormes; el DFS ingenuo revisita los mismos estados. Silencio
Silencio **Reglas de ejecución** Silencio Debemos identificar cuando un movimiento es inútil (por ejemplo, insertar un color que nunca ayuda). Silencio
Silencio **Memoization Overlap** Silencio Dos secuencias diferentes pueden producir el mismo estado de `(board, hand). Silencio
Silencio ** Variantes de lenguaje** Silencio Java: necesidad de escoria personalizada; Python: límites de recursión; C++: velocidad vs. memoria. Silencio

-...

## 3down Core Idea – DFS + Memo + Compresión de la Junta

1. ** Representación del Estado* *
- **Board** - comprimido como cuerda.
- **Hand** – una serie de tamaño 5 (`R Y B G W`) que rastrea los recuentos restantes.
- Encode state as `board#handString` (e.g., `"WWRBB#21200 ").
2. **Recursivo DFS**
- Por cada *gap* en el tablero, trate de insertar una bola del mismo color que una de las bolas vecinas (otros no es posible colapsar).
- Después de la inserción, **collapse** la tabla: repetidamente eliminar cualquier 3+ estrecas de mismo color.
- Recupere en la nueva tabla y la mano actualizada.
- Haz un seguimiento de pasos mínimos.
3. *Memoización*
- Usar un mapa de hash (`Map Garantizado,Integer conmigomo`) para encontrar la mejor respuesta para un estado dado.
- Si un estado ha sido resuelto antes, devuelve el valor caché.
4. # Corriendo #
- Si ninguna bola de mano coincide con el color de la tabla, salta.
- Si un color necesita bolas para colapsar pero la mano tiene menos, saltar.
- Salir temprano si el tablero está vacío.

La clave es que el tablero es *short* (≤16) y la mano es pequeña (≤5), por lo que podemos permitirnos un DFS compacto.

-...

## 4VIEW⃣ Code Implementations

#### 4.1 Java

``java
importar java.util*;

Solución de la clase pública {}
// 0:R 1:Y 2:B 3:G 4:W
privada static final char[] COLORS = {'R', 'Y', 'B', 'G', 'W'};
mapa privado escritoString, Integer memo = nuevo HashMap garantizado();

int findMinStep(String board, String hand) {
int[] handCnt = nuevo int[5];
para (carc : hand.toCharArray())
handCnt[charIdx(c)]++;

dfs de retorno (board, handCnt);
}

int privado dfs(String board, int[] handCnt) {}
if (board.isEmpty()) return 0;
llave de cuerda = tabla + "#" + manoCntToStr(handCnt);
si (memo.containsKey(key)) devuelve memo.get(key);

Int ans = Integer. MAX_VALUE;
// Para cada posición de brecha
para (int i = 0; i <= board.length(); i++) {
char left = (i == 0) ? 'X' : board.charAt(i - 1);
char right = (i == board.length()) ? 'X' : board.charAt(i);
// Sólo inserta una pelota que coincida al menos con un vecino
para (int color = 0; color = 5; color++) {}
(handCnt[color] == 0) continuar;
char c = COLORS[color];
si (c != izquierda " c != derecha) continúan;

handCnt [color]--;
Cierre después = colapso (board.substring(0, i) + c + tabla.substring(i));
int res = dfs(after, handCnt);
si (res!= -1) ans = Math.min(ans, res + 1);
handCnt[color]+; // backtrack
}
}

memo.put(key, ans == Integer. MAX_VALUE ? -1 : ans);
devolver memo.get(key);
}

privada desplome de la cuerda (String s) {
StringBuilder sb = nuevo StringBuilder(s);
booleano cambiado = verdadero;
mientras (cambiado) {
cambiado = falso;
int n = sb.length();
int i = 0;
mientras (i
int j = i + 1;
mientras (j.) == sb.charAt(i)) j++;
si 3) { // eliminar la racha
sb.delete(i, j);
cambiado = verdadero;
n = sb.length();
i = Math.max(0, i - 1); // volver a comprobar la posición anterior
. ♫ ... {
i = j);
}
}
}
devolver sb.toString();
}

int privado charIdx(char c) {}
c) {
caso 'R': retorno 0;
caso 'Y': retorno 1;
caso 'B': retorno 2;
caso 'G': retorno 3;
caso 'W': retorno 4;
default: lanzar nuevo IlegalArgumentException();
}
}

privada String handCntToStr(int[] cnt) {
volver String.format("%d%d%d%d", cnt[0], cnt[1], cnt[2], cnt[3], cnt[4]);
}
}
`` `

##### Por qué funciona

- **Memoización** garantiza que cada uno de los pares únicos se procesa una vez.
- **El filtrado de la pila** (atrapar a un vecino) corta ramas inútiles.
- **Colapso** se realiza iterativamente hasta que esté estable, asegurando que el tablero sea siempre canónico para la clave del memo.

-...

#### 4.2 Python

``python
desde functools import lru_cache
de las importaciones de colecciones Contrato

Solución de clase:
COLORS = 'RYBGW'

def find MinStep(self, board: str, hand: str) - Conf int:
hand_cnt = [hand.count(c) for c in self. COLORS

@lru_cache(maxsize=None)
def dfs(b: str, h: str) int:
si no b:
retorno 0
hand_cnt = [int(h[i]) for i in range(5)]
mejor = flotante('inf')

# Escanear cada punto de inserción
para i en rango(len(b) + 1):
izquierda = b[i-1] si yo si no 'X '
derecha = b[i] si yo ecto len(b) otra 'X'

para ti mismo. COLORS:
si Hand_cnt[self. COLORS.index(c)] == 0:
continuar
si c!= izquierda y c!= Bien.
continuar

# Insertar
new_board = b[:i] + c + b[i:]
new_board = colapso(new_board)

Hand_cnt[self. COLORS.index(c)] -= 1
res = dfs(new_board, ''.join(map(str, hand_cnt))))
Hand_cnt[self. COLORS.index(c)] += 1

si res!= -1:
mejor = min(mejor, res + 1)

retorno -1 si mejor == flotante('inf') mejor

dfs(board, ''.join(map(str, hand_cnt)))

def collapse(s: str) - Propiedad str:
""Repetidamente quita las rayas de 3+ mismo color.""
pila = []
I = 0
n = len(s)
mientras que yo no
j = i + 1
mientras j < n y s[j] == s[i]:
j += 1
si j - i √≥= 3:
i = j) saltar este bloque
más:
stack.append(s[i:j])
I = j
new_s = ''.join(stack)
retorno colapso (new_s) si new_s != s else new_s
`` `

■ **Consejo:** La profundidad de la recursión del pitón no es un problema aquí porque la profundidad ≤ 5 (tamaño de la mano). La función " colapso " es recursiva a la cola; es segura y rápida.

-...

#### 4.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
const string COLORS = "RYBGW";
unordered_map detectstring, int

// Tabla de colapsar después de la inserción
desplome de cadenas (la cadena restante) {
hilo cur = s;
bool cambiado = verdadero;
mientras (cambiado) {
cambiado = falso;
int n = cur.size();
cuerda siguiente;
por (int i = 0; i)
int j = i + 1;
mientras (j.) j++;
si 3) {
cambiado = verdadero; // quitar este bloque
. ♫ ... {
siguiente += cur.substr(i, j - i);
}
i = j);
}
cur.swap(next);
}
Volver cur;
}

int dfs(punto de cuerda, vector asignadoint
si (board.empty()) devuelve 0;
llave de cadena = tabla + "#" + toKey(hand);
si (memo.count(key))) devuelve memo[key];

int best = INT_MAX;
int len = board.size();

para (int i = 0; i) {}
char left = (i == 0) ? '?' : board[i-1];
char right = (i == len) ? '?' : board[i];

para (int c = 0; c) {}
si (!hand[c]) continúan;
char color = COLORS[c];
si (color != izquierda " color != derecha) continúan;

[c]--
cadena siguiente = colapso (board.substr(0, i) + color + tabla.substr(i));
int res = dfs(next, hand);
[c]+;

si (res!= -1) mejor = min(best, res + 1);
}
}

memo [key] = (mejor == INT_MAX) ? -1 : mejor;
devolver memo[key];
}

string toKey(const vector identificadoint confianza &hand) {
string k;
para (int v : hand) k += char('0' + v);
retorno k;
}

public:
int find MinStep(tabla de cuerda, mano de cuerda) {}
vector significado cnt(5, 0);
cnt [COLORS.find(c)]++;
dfs (board, cnt);
}
};
`` `

-...

## 5down ¿Qué era correcto? (El Bien)

Silencio TENIDO ANTERIOR ANTERIOR
Silencio...
Silencio **Estado Compacto** Silencio Board + mano cuenta capturar completamente el estado del juego. Silencio
Silencio **Memoización** Silencio Evita el soplo exponencial – cada estado visitado una vez. Silencio
Silencio **Gap Filtrar** Silencio Sólo insertar colores que pueden desencadenar un colapso → menos ramas. Silencio
Silencio ** Collapso alternativo** Silencio Junta se vuelve canónica; la misma configuración siempre tiene la misma clave. Silencio
tención **Language‐Specific Optimizations** TEN Java: custom hash key; Python: `lru_cache`; C++: `unordered_map` with string key. Silencio

-...

## 6down ¿Dónde podría ser más inteligente? (El Mal)

Silencio Silencio Silencio Silencio
Silencio...
Silencio **Recomputación de clave innecesaria** Silencio Construyendo una nueva clave de cuerda cada llamada de recursión puede ser pesada. tención Pre-compute llave cadena para la mano una vez, reutilizarlo. Silencio
Silencio **Colapso Complejidad** Silencio Mientras el tablero es corto, el colapso se ejecuta en O(N2) si se hace ingenuamente. Utilice el enfoque de dos puntos de pila de O(N). Silencio
Silencio **Large Hand** Silencio La poda actual asume la mano ≤ 5. Si la mano crece, el algoritmo puede necesitar más poda (por ejemplo, contando las bolas necesarias para cada color). Silencio
Silencio **Thread‐Safety** Silencio El mapa de Memo no es seguro de hilo. En concursos, el hilo único está bien. Silencio

-...

## 6walks comunes & Edge Cases

¿Por qué sucede?
Silencio...
Silencio ** Mano vacía** Silencio Si la mano tiene cero tarjetas para todos los colores que aparecen a bordo, DFS devuelve `-1` inmediatamente. Silencio Comprueben temprano y regresen `-1`. Silencio
Silencio **Circular Collapse** Silencio La eliminación de un bloque puede crear otro del mismo color en el límite. El bucle de colapso iterativo (Bandera cambiada) asegura que todas las cascadas se manejan. Silencio
Silencio **Las teclas Duplicadas** Silencio Las diferencias menores en el orden de mano pueden producir el mismo estado. tención La llave de mano es una cadena de 5 dígitos; el orden es fijado por COLORS. Silencio
tención **Python Recursion Depth** ← Depth está atado por el tamaño de la mano (≤5), tan seguro. Si el tamaño de la mano creció, considere DFS iterativa o aumente el límite de recursión. Silencio

-...

## 6VIEW⃣ Summary " Takeaways

- **La puesta en marcha en operaciones clave** (insertar en la brecha + colapso) reduce el problema a un pequeño DAAT.
- **La representación canónica** (tabla colapsada estable) permite que la memoización sea eficaz.
- ** Complejidad del tiempo**: \(O(3^{H} \times 5^{H})\) ♥ \(O(10^3)\) para el peor caso, gracias al memo.
- **Complejidad del espacio**: dominado por el mapa del memo – en la mayoría de unos pocos miles de entradas.

-...

Pensamientos finales

Ya sea que usted está codificación en **Java**, **Python**, o **C++**, la idea central sigue siendo la misma: tratar el juego como un problema de investigación estatal y utilizar la memoización para prune. El juego Zuma-like en LeetCode 488 es un gran ejercicio en * compresión del estado*, *programación dinamica* y *revolvimiento recursivo*.

¡Feliz codificación! 🚀

-...

**Keywords:** Zuma juego, LeetCode 488, encontrarMinStep, DFS, memoización, colapso del tablero, cuenta de mano, Java LRU cache, Python lru_cache, C++ unordered_map, algoritmo de diseño.