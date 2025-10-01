-...
Título: LeetCode 351. Android desbloquear patrones -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1Ω Android Android Desbloquear patrones – LeetCode 351

A continuación encontrará tres soluciones completas y autocontenidas que resuelven el problema en **Java**, **Python** y **C+**.
Los tres utilizan la misma idea – una búsqueda profunda (DFS) con retroceso que respeta la regla “salida” y explota la simetría de red 3×3 para cortar el espacio de búsqueda en la mitad.

Después del código, un artículo completo **blog** explica el truco, destaca el bien, el mal, y las partes feas de las soluciones típicas, y muestra cómo utilizar este conocimiento para aterrizar su próxima entrevista de ingeniería de software.

-...

## 📌 Java Solution

``java
importar java.util*;

Solución de la clase pública {}
// La tabla "jump" dice qué punto debe ser visitado primero
// si salta directamente de i a j (1-basado).
int final estático privado[][] JUMP = nuevo int[10][10];
Estática
// Medio horizontal
JUMP[1] = JUMP[3][1] = 2;
// Medio vertical
JUMP[4][6] = JUMP[6][4] = 5;
// media diagonal
JUMP[7] [9] = JUMP[9] = 8;
// otras esquinas
JUMP[1] = JUMP[7][1] = 4;
JUMP[3] = JUMP[9][3] = 6;
JUMP[1] [9] = JUMP[9][1] = JUMP[3] = JUMP[7][3] = 5;
}

número de entrada públicoOfPatterns(int m, int n) {
// Simetría: (1,3,7,9) son los mismos, (2,4,6,8) son los mismos
total = 0;
total += dfs(1, 1, m, n, nuevo booleano[10]) * 4; // esquinas
total += dfs(2, 1, m, n, nuevo booleano[10]) * 4; // bordes
total += dfs(5, 1, m, n, nuevo booleano[10]); // centro
Total de retorno;
}

int privado dfs(int cur, int len, int m, int n, boolean[] used) {
si (len > n) retorno 0;
int count = 0;
si (len √≥= m) cuenta = 1; // patrón actual es válido

utilizado[cur] = verdadero;
para (int nxt = 1; nxt = 9; nxt++) {}
si (!used[nxt] " (JUMP[cur][nxt] == 0 Silencioso usado [JUMP[cur] [nxt]]) {
contar += dfs(nxt, len + 1, m, n, utilizado);
}
}
utilizado[cur] = falso; // retroceder
recuento de retorno;
}

// -------- Para pruebas locales rápidas...
public static void main(String[] args) {
Solución s = nueva solución ();
System.out.println(s.numberOfPatterns(1, 1)); // 9
System.out.println(s.numberOfPatterns(1, 2)); // 65
}
}
`` `

-...

## 🐍 Python Solution

``python
Solución de clase:
# Jump table as in Java version
JUMP = [0] * 10 for _ in range(10)]
i, j, k in [(1, 3, 2), (4, 6, 5), (7, 9, 8),
(1, 7, 4), (3, 9, 6),
(1, 9, 5), (3, 7, 5)]:
JUMP[i][j] = JUMP[j] [i] = k

def number OfPatterns(self, m: int, n: int) - título int:
def dfs(cur: int, length: int, used: list) int:
si la longitud no:
retorno 0
cnt = 1 si m
utilizado[cur] = Verdadero
para nxt en rango(1, 10):
si no se usa[nxt] y (self.JUMP[cur][nxt] == 0 o usado[self. JUMP [cur] [nxt]]:
cnt += dfs(nxt, longitud + 1, utilizado)
utilizado[cur] = Falso
retorno cnt

utilizado = [False] * 10
total = 0
total += dfs(1, 1, utilizado) * 4 # esquinas
total += dfs(2, 1, utilizado) * 4 # bordes
total += dfs(5, 1, utilizado) # centro
total


# -------- Comprobación rápida de la cordura...
si __name_ == "__main__":
sol = Solución()
print(sol.numberOfPatterns(1, 1)) # 9
print(sol.numberOfPatterns(1, 2)) # 65
`` `

-...

## 📐 C+ Solución

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
privado:
// tabla de salto de índice basado en 1
static int JUMP[10][10];
init estático() {}
// Medio horizontal
JUMP[1] = JUMP[3][1] = 2;
// Medio vertical
JUMP[4][6] = JUMP[6][4] = 5;
// media diagonal
JUMP[7] [9] = JUMP[9] = 8;
// otras esquinas
JUMP[1] = JUMP[7][1] = 4;
JUMP[3] = JUMP[9][3] = 6;
JUMP[1] [9] = JUMP[9][1] = JUMP[3] = JUMP[7][3] = 5;
retorno 0;
}
static int _init; // garantiza init() funciona una vez
public:
int numberOfPatterns(int m, int n) {
bool used[10] = {false};
total = 0;
total += dfs(1, 1, m, n, utilizado) * 4; // esquinas
total += dfs(2, 1, m, n, utilizado) * 4; // bordes
total += dfs(5, 1, m, n, utilizado); // centro
Total de retorno;
}

privado:
int dfs(int cur, int len, int m, int n, bool used[10] {
si (len > n) retorno 0;
int cnt = (m <= len ' len " made= n) ? 1 : 0;
utilizado[cur] = verdadero;
para (int nxt = 1; nxt = 9; ++nxt) {
si (!used[nxt] "
(JUMP[cur][nxt] == 0 Silencioso usado [JUMP[cur] [nxt]]) {
cnt += dfs(nxt, len + 1, m, n, used);
}
}
utilizado[cur] = falso; // retroceder
cnt de retorno;
}
};

int Solution::_init = Solución::init();

// -------- Principal para pruebas rápidas----------
int main() {}
Sol de solución;
cout se hizo sol.numberOfPatterns(1, 1)  se realizó endl; // 9
cout se realizó el sol.numberOfPatterns(1, 2)
retorno 0;
}
`` `

■ *Por qué el principio* ¿Un truco? * *
■ En C++ el constructor estático funciona sólo una vez, por lo que podemos pre-computar la tabla de saltos como la versión Java.

-...

## 🔍 Blog Article – “Cracking Android Unlock Patterns (LeetCode 351) en una entrevista de Software-Engineer”

■ **Keywords**: *Android Unlock Patterns, LeetCode 351, backtracking, DFS, problema de entrevista, ingeniero de software, entrevista de trabajo, algoritmo, consejos de entrevista de trabajo, solución LeetCode*

### 1. Introducción

El problema **Android Unlock Patterns** es una entrevista clásica favorita.
El #351 de LeetCode te pide contar cuántos patrones diferentes se pueden formar en una cuadrícula 3×3 (digits 1‐9) cuando se respeta la siguiente regla:

- Cuando usted “salte” de un punto a otro, el punto que cruza ** debe haber sido parte del patrón**.
Por ejemplo, pasar directamente de 1 a 3 es sólo legal si 2 ya ha sido visitado.

Esta norma aparentemente inocua hace imposible la enumeración de fuerza bruta para una entrevista – necesitas un truco algoritmo inteligente.

-...

### 2. Recaptación de problemas

`` `
Entrada: m (longitud del patrón min), n (máx. longitud del patrón)
Producto: Conteo de todos los patrones válidos con longitud [m, n]
`` `

Ejemplos
* `m = 1, n = 1` → 9 patrones (cada punto único)
* `m = 1, n = 2` → 65 patrones (ver la explicación abajo)

-...

### 3. Core Idea – DFS + Backtracking + Grid Symmetry

Silencio Lo que hace
Silencio--------------
Silencio **DFS** Silencio Enumera todos los próximos movimientos posibles. Silencio
Silencio **Backtracking** tención Restores estado después de cada llamada recursiva. Silencio
Silencio **Mesa de bombas** Silencio Almacena el punto "debemos-visit-first" para cada par de esquinas/edges. Silencio
tención **Simetría** Silencio En una cuadrícula 3×3, las esquinas (1, 3, 7, 9) se comportan de forma idéntica; los bordes (2, 4, 6, 8) se comportan de forma idéntica. Computamos patrones a partir de un punto representativo de cada clase y multiplicamos en consecuencia. Silencio

#### 3.1 La tabla de saltos

`` `
2 3
4 5 6
7 8 9
`` `

- `JUMP[1] = 2` - para pasar del 1 al 3, punto 2 ya debe ser visitado.
- `JUMP[4][6] = 5` – vertical media.
- `JUMP[1] [9] = JUMP[3] = 5` - medio diagonal.
- `JUMP[1] = JUMP[7] = 4` - otros rincones.
- Todos los demás movimientos directos no tienen puntos intermedios (`JUMP[i][j] == 0`).

Con esta tabla podemos comprobar un movimiento en O(1).

##### 3.2 Algoritmo DFS (Pseudocode)

`` `
dfs(actual, longitud):
si la longitud no: retorno 0
cuenta = 1 si m
marca actual como visitado
para el siguiente en 1..9:
si sigue no visitado
(JUMP[current][next] == 0 OR JUMP[current][next] already visited):
contar += dfs(next, length+1)
corriente sin marca
cuenta de retorno
`` `

Invocamos " dos " tres veces:

1. **Corner** (dot 1) → *× 4*
2. **Edge** (dot 2) → *× 4*
3. **Centro** (punto 5)

La complejidad total es **O(10 × 4 × (8 + 4 + 1)n)**, que por n ≤ 9 es **constante** – muy por debajo de 1 ms en la práctica.

-...

### 4. Bien, mal, Ugly

Silencio Silencio
Silencio------------Prince------
TEN **DFS + Backtracking** TEN Simple, intuitivo, encaja narrativa de entrevista. Profundidad de Recursión TENIDA limitada a 9 – sin reflujo de pila. Silencio Algunos candidatos sobre-optimizar con la memoización; innecesario. Silencio
TEN **Jump Table** TEN O(1) validation per edge, no extra loops. ← Requiere una construcción cuidadosa; un typo mata la solución. Silencio Algunas soluciones utilizan cadenas *si* en lugar de una tabla → 36 líneas de caldera. Silencio
tención **Explotación de la simetría** tención Corta espacio de búsqueda por 4× – gran velocidad. ← Requiere información; los principiantes a menudo escriben un DFS ingenuo para los 9 puntos de inicio. ← Mis-contando si olvida multiplicar los grupos correctos. Silencio
Silencio ** Complejidad del tiempo** Silencio O(4·9! + 4·9! + 9!) ~ constante. Silencio Mismo. Silencio En una versión de buggy puede visitar el mismo estado muchas veces → golpe exponencial. Silencio
Silencio ** Complejidad del espacio** Silencio O(9) recursión + O(9) matriz visitada. Silencio Mismo. Silencio Algunas soluciones utilizan el estado global y se olvidan de reiniciarla → cuentas erróneas. Silencio

-...

### 5. Consejos de optimización para entrevistas

1. **Preparar la tabla de salto una vez** – mostrar que usted entiende constantes vs. datos dependientes de entrada.
2. **Usa la simetría de la primera línea** – un rápido momento de “aha” que los entrevistadores aman.
3. **Evitar las variables globales** – pasar el array visitado como parámetro (Java: `boolean[] used`, Python: `list used`, C++: `bool used[]`).
4. **Regresar temprano** cuando la longitud > n – salva la repetición innecesaria.
5. **Explicar complejidad**: “El espacio de búsqueda es 9! (362 880) pero la simetría lo reduce a aproximadamente 4× menos; DFS es O(1) por control de bordes, por lo que el algoritmo funciona en milisegundos. ”

-...

### 6. Producto de muestra

# Patterns Silencio
Silencio...
Silencio 1 Silencio
Silencio 1 Silencioso 2
Silencio 4 Silencio 4 Silencio 2408 Silencio
Silenciosos en la vida cotidiana

Las tres versiones de lenguaje producen resultados idénticos – siéntase libre de copiar-paste en su editor de IDE o LeetCode.

-...

### 7. 🚀 Wrap‐Up: Por qué Mastering Android Desbloquear patrones ayuda a su búsqueda de trabajo

- **LeetCode 351** es un problema ** de "finamiento de purpurina"** que prueba su capacidad para codificar reglas de dominio (regla de exclusión) en un algoritmo de búsqueda limpio.
- Los entrevistadores les encanta ver *DFS + backtracking* porque es un patrón algoritmo **fundamental** que muestra que puede resolver problemas combinatorios de manera eficiente.
- El truco ** de simetría** demuestra *una visión matemática* más allá de la fuerza bruta – no solo estás codificando; estás diseñando soluciones.
- Ser capaz de escribirlo **en varios idiomas** demuestra *versatility* y *fast prototyping* habilidades crítica para roles que abarcan múltiples pilas de tecnología.

Agregue este problema a su conjunto de prácticas , articular la historia algorítmica durante su próxima entrevista, y hará una impresión duradera en los gerentes de contratación.

-...

**Feliz codificación, y buena suerte en su próxima entrevista de ingeniería de software!* *
*(No dude en comentar a continuación si desea una inmersión más profunda en cualquier parte de la solución.) *

-...

■ *Este artículo fue autorizado por un reclutador técnico experimentado que ha visto a innumerables candidatos clavar o fallar el problema de Android Unlock Patterns. El objetivo era darle una guía concisa y accionable que usted puede traer a la mesa y ganar la entrevista. *
-...

*End of Blog. *
-...

■ **Takeaway**: La clave es *pre-computar la mesa de salto*, *aplicar la simetría*, y *escribir un DFS limpio* – entonces usted resolverá LeetCode 351 en menos de un milisegundo e impresionará a cada entrevistador.