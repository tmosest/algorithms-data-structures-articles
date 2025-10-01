-...
Título: LeetCode 3078. Partido Alphanumerical Patrón en Matriz Yo...
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 3078. Partido Alphanumerical Patrón en Matriz I
**Medio** Silencio**

-...

### 1. Recaptación de problemas

Te dan

* `board`: a `m × n` matriz de dígitos (0-9).
* `pattern`: a `p × q` matriz de caracteres - cada personaje es un dígito (`'0'```'9'`) o una letra minúscula (`'a'``''z').

A sub-matrix of `board` **matches** `pattern` si existe una asignación de cada letra distinta en `pattern` a un * dígito único* tal que después de aplicar la asignación de cada célula en la sub-matrix equivale a la célula correspondiente en `pattern`.
Los dígitos en `pattern` deben coincidir con el tablero exactamente.

Devuelve las coordenadas `[row, col]` de la esquina **upper‐left** de la sub-matrix más temprana (la fila más baja, luego la columna más baja).
Si no hay coincidencia, devuelve `[-1, -1]`.

-...

### 2. Por qué este problema es una gran pregunta de entrevista

Silencio Silencio Silencio Silencio
Silencio...
Silencio **Profundidad conceptual** – prueba tu comprensión del patrón de emparejamiento, cartografía bijeactiva y traversal 2-D. Silencio **Edge-case fatiga** – muchos errores fuera-por-uno, especialmente al mapear cartas a dígitos. Silencio ** trampa de presión del tiempo** – soluciones ingenuasivas O(m2n2) todavía pueden pasar pero arriesgarse “tiempo-limit excedido” en pruebas ocultas. Silencio

- **Bueno**: El problema es lo suficientemente pequeño (≤ 50×50) para dejar que brute‐force, sin embargo te obliga a pensar en *bijection* entre letras y dígitos.
- **Bad**: Es fácil escribir un algoritmo correcto pero obtener respuestas incorrectas en casos de esquina, como cartas repetidas, conflictos de letras digitales o patrones que tocan el límite de la junta.
- **Ugly**: Si te olvidas de reiniciar tu asignación entre diferentes posiciones de arriba a izquierda, obtendrás falsos positivos.

Preparar para este problema te hará sentir cómodo con:
* Traversal de matriz bidimensional
* Limitaciones de captura y detección de conflictos
* Condiciones de salida temprana (en cuanto se encuentre un desajuste)

Todas ellas son grapas de entrevistas de codificación de nivel superior en FAANG, Amazon, Google, etc.

-...

### 3. Panorama general de la solución

1. **Evaluar todas las posiciones de inicio posibles* *
Por cada `r' en `[0, m - p]` y `c` en `[0, n - q]` consideramos la sub-matrix cuya esquina superior-izquierda es `(r, c)`.

2. **Mantenga dos asignaciones**
* `digit → letter` (Dirección del tamaño 10, inicializada a " 1 " )
* `letter → digit ' (array of size 128 or a hashmap)

Estos dos mapas garantizan el requisito de la bijeción.

3. **Validar la sub-matrix**
Para cada celda `(i, j)` dentro del patrón:
* Si `pattern[i][j]` es un dígito, debe igualar el valor de la tabla en `(r+i, c+j)`.
* Si es una carta:
* Si ya hemos mapeado ese dígito, la letra mapeada debe ser la misma.
* Si ya hemos mapeado esa carta, el dígito mapeado debe ser el mismo.
* Si no existe ninguna asignación, establezca ambos.

4. **Retorno de las primeras coordenadas coincidentes* *
Debido a que iteramos filas primero, columnas segundo, el primer partido exitoso es automáticamente el más pequeño.

5. **Si no hay coincidencia, devuelve `[-1, -1]`. #

Complexity:
*Hora*: `O(m-p+1)(n-q+1) * p * q)` – peor caso Ω `503 = 125 000` operaciones.
*Pace*: `O(1)` – sólo arrays de tamaño fijo para los dos mapas.

-...

### 4. Implementaciones de referencia

A continuación encontrará soluciones limpias y idiomáticas en **Java, Python y C++**.
Los tres siguen la misma lógica que se describe anteriormente.

-...

###### 4.1 Java

``java
importa java.util. Arrays;

Clase Solución {
public int[] findPattern(int[][] board, String[] pattern) {}
int m = board.length, n = board[0]. longitud;
int p = pattern.length, q = pattern[0].length();

para (int r = 0; r + p <= m; r++) {
para (int c = 0; c + q י= n; c++) {
int[] digitToLetter = nuevo int[10]; // 0 significa unmapped
int[] letterToDigit = new int[128]; // -1 means unmapped
Arrays.fill(digitToLetter, 0);
Arrays.fill(letterToDigit, -1);

booleano ok = verdadero;
para (int i = 0; i) {}
para (int j = 0; j) {}
int board Val = board[r + i][c + j];
char pat = pattern[i].charAt(j);

si (Character.isDigit(pat) {
si (pat - '0' != boardVal) ok = falso;
} más { // letra
si (digitToLetter [boardVal] == 0) {
// nueva asignación
si (letterToDigit[pat] == -1) {
digitToLetter[boardVal] = pat;
letterToDigit[pat] = boardVal;
. ♫ ... {
// la misma carta mapeada a un dígito diferente
ok = falso;
}
} si (digitToLetter [boardVal] != pat) {
// dígito de la tabla ya mapeado a una carta diferente
ok = falso;
}
}
}
}

si (ok) devuelve nuevo int[]{r, c};
}
}
devolver nuevo int[]{-1, -1};
}
}
`` `

-...

###### 4.2 Python

``python
de la importación Lista

Solución de clase:
def findPattern(self, board: List[List[int]], patrón: List[str]) List[int]:
m, n = len(board), len(board[0])
p, q = len(pattern), len(pattern[0])

para r en rango(m - p + 1):
para c en rango(n - q + 1):
# digit - letra título (0 significa no numerada)
* 10
# letra - dígito de título (-1 significa sin editar)
l2d = [-1] * 128
OK = True

para i en rango(p):
si no está bien:
descanso
para j en rango(q):
num = board[r + i][c + j]
ch = patrón[i][j]

si ch.isdigit():
si int(ch) != num:
ok = Falso
descanso
más:
si d2l[num] == 0:
si l2d [ord(ch)] == -1:
d2l[num] = ch
l2d[ord(ch)] = num
más:
ok = Falso
descanso
elif d2l[num] != ch:
ok = Falso
descanso

Si está bien:
[r, c]

[-1, -1]
`` `

-...

##### 4.3 C++

``cpp
Incluido el título
#include ■string
usando std namespace;

Clase Solución {
public:
vector identificador encontrarPattern(vector seleccionadovector seleccionador seleccionado) {}
int m = board.size(), n = board[0].size();
int p = pattern.size(), q = pattern[0].size();

para (int r = 0; r + p <= m; ++r) {}
para (int c = 0; c + q י= n; ++c) {
int d2l[10] = {0}; // dígito - letra título (0 significa no incluido)
int l2d[128];
fill(begin(l2d), end(l2d), -1); // letter - título dígito

bool ok = verdadero;
para (int i = 0; i) {}
para (int j = 0; j)
int num = board[r + i][c + j];
char ch = pattern[i][j];

si {}
si (ch - '0' != num) ok = falso;
} más { // letra
si (d2l[num] == 0) {
si (l2d [(int)ch] == -1) {
d2l [num] = ch;
l2d [(int)ch] = num;
. ♫ ... {
ok = falso;
}
} si (d2l [num] != ch) {
ok = falso;
}
}
}
}

si (ok) regreso {r, c};
}
}
retorno {-1, -1};
}
};
`` `

-...

### 5. Testing " Edge Cases

Silencio Test ← Reason
Silencio...
Silencio `board = [[0]]`, `pattern = ["a"]` Silencio celda individual, asignación de cartas. Silencio
Silencioso `board = [5,5],[5,5]]`, `pattern = ["aaa", "aaa"]` Silencio Todos los mismos dígitos – cartografía debe ser consistente. Silencio
TENIDO `board = [1,2],[3,4]]`, `pattern = ["a1","2b"] ' ANTE Mixed digit/letter desajusttch. Silencio
Silencio `board ' o `pattern` en la frontera Silencio Asegúrese de que nunca leamos fuera de límites. Silencio
Silencio `pattern` que contiene cartas repetidas con diferentes dígitos Silencio Debe fallar. Silencio

Ejecutar las implementaciones proporcionadas contra los casos anteriores (y las pruebas de muestra de LeetCode) todos producen los productos esperados.

-...

### 6. Consejos de entrevista

1. **Clarificar la bijeción** – preguntar al entrevistador si diferentes letras deben mapear a diferentes dígitos.
2. **Habla a través de tus arrays de mapeo** – explica por qué necesitas dos mapas y cómo haces cumplir la singularidad.
3. **La complejidad del debate** – señala que la fuerza bruta está bien para las limitaciones, pero puede ser optimizada si el tablero es grande.
4. ** Pensamiento por caso ** – mencionar errores fuera de uno y cómo sus bucles aseguran que permanezcamos dentro del tablero.
5. **Return ordering** – enfatizar que las hileras iterantes garantizan primero las coordenadas más pequeñas.

-...

### 7. SEO-Optimized Takeaway

■ Maestro **LeetCode 2384** (Board Pattern Matching) – un clásico desafío de doble patrón que enseña mapa bijetivo, traversal bidimensional y estrategias de salida temprana. Sumérgete en soluciones limpias **Java, Python, y C++**, casos de borde de prueba, y camina entrevistadores a través de su razonamiento para aterrizar ese rol de nivel superior en Google, Amazon, o cualquier empresa de tecnología superior.

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀

-...

*Preparado por [Su nombre], Senior Software Engineer " Coding Interview Coach. *