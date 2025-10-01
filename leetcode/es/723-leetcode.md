-...
Título: LeetCode 723. Candy Crush -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
Código de Solución
A continuación se ** tres completas, independientes** implementaciones del solucionador Candy Crush
(LeetCode 723) en **Java**, **Python 3** y **C+**.
Cada solución sigue la misma idea algoritmo:

1. **Marca** todos los caramelos que pertenecen a una carrera horizontal o vertical de ≥ 3.
2. **Crush** los caramelos marcados → establecerlos a `0`.
3. **Drop** dulces en cada columna hasta que la tabla se estabiliza.
4. Repita hasta que no se puedan aplastar más caramelos.

Los tres códigos están listos para copiar—pasar en el editor LeetCode o cualquier IDE.

-...

## A. Java (LeetCode 723)

``java
importar java.util*;

Clase Solución {
int m privado, n;

int[][] candyCrush(int[][] board) {
m = pensión. longitud;
n = board[0].length;
mientras (!crush(board)) {}
drop(board);
}
de retorno;
}

/* Vuelva a la verdad si el tablero es estable, falso si aplastamos algo. */
trituración booleana privada(int[][] board) {
establo booleano = verdadero;
// 1. Marcar células que necesitan ser aplastadas
para (int r = 0; r)
para (int c = 0; c) {}
(board[r][c] == 0) continuar;
int val = Math.abs(board[r][c]);

booleano horizontal = falso, vertical = falso;
si (c ≤ 0 " sensible c " )
Math.abs(board[c - 1]) == val "
Math.abs(board[r][c + 1]) == val) {
horizontal = verdadero;
}
si (r √≥ 0 ' r
Math.abs(board[r - 1][c]) == val "
Math.abs(board[r + 1][c]) == val) {
vertical = verdadero;
}

si (horizontal TENIDO TENDIDO vertical) {
estable = falso;
tablero[r][c] = -Math.abs(board[r][c]); //
si (horizontal) {
[r][c - 1] = -Math.abs(board[c - 1]);
board[r][c + 1] = -Math.abs(board[r][c + 1]);
}
si (vertical) {
bordo [r - 1][c] = -Math.abs(board[r - 1][c]);
board[r + 1][c] = -Math.abs(board[r + 1][c]);
}
}
}
}

// 2. Quitar las células marcadas
para (int r = 0; r)
para (int c = 0; c) {}
si (board[r] [c] [c] [c] [c] [c] [c] = 0;
}
}
c) Retorno estable;
}

/* Tirar los caramelos para llenar las células cero */
privada void drop(int[][] board) {
para (int c = 0; c) {}
int escriba = m - 1; // siguiente posición para escribir non‐zero
para (int r = m - 1; r ñ= 0; r--) {}
(board[r][c]!= 0) {
junta[escribir][c] = junta[r][c];
[c] = 0;
escribir...
}
}
}
}
}
`` `

-...

## B. Python 3

``python
Solución de clase:
def candyCrush(self, board: List[List[int]) - No. List[List[int]]:
m, n = len(board), len(board[0])

def crush() - título Bool:
""Retorno Verdadero si el tablero es estable.""
cambiado = Falso
# Mark
para r en rango(m):
para c en el rango(n):
si la junta [r][c] == 0:
continuar
val = abs(board[r][c])
hor = Falso
ver = Falso
si 0 se hizo c - 1 y \
abs(board[r][c - 1]) == val y \
abs(board[r][c + 1]) == val:
hor = True
si 0 0 se realizó r
abs(board[r - 1][c]) == val y \
abs(board[r + 1][c]) == val:
ver = Verdadero
si hor o ver:
cambiado = Verdadero
board[r][c] = -abs(board[r][c])
Si hor:
board[r][c - 1] = -abs(board[r][c - 1])
board[r][c + 1] = -abs(board[r][c + 1])
si ver:
board[r - 1][c] = -abs(board[r - 1][c])
board[r + 1][c] = -abs(board[r + 1][c])

# Crush
para r en rango(m):
para c en el rango(n):
si la tabla [r][c] se hizo 0:
board[r][c] = 0
no cambió

def drop() - No. Ninguno.
""La columna de los caramelos de gota por columna.""
para c en el rango(n):
escribir = m - 1
para r en rango(m - 1, -1, -1):
si la junta [r][c] 0:
junta[escribir][c] = junta[r][c]
si escribe != r:
board[r][c] = 0
escribir -= 1

mientras no aplastar():
drop()
tabla de retorno
`` `

-...

## C. C++ (LeetCode 723)

``cpp
Clase Solución {
public:
vector realizador realizador seleccionado nombrado titular candyCrush(vector identificadovector fielint ratio) {
int m = board.size(), n = board[0].size();
mientras (!crush(board)) gota(board);
de retorno;
}

privado:
triturado bool(vector seleccionador) {
int m = board.size(), n = board[0].size();
bool estable = verdadero;

// 1. Marcar las células para aplastar
para (int r = 0; r) {}
para (int c = 0; c) {}
(board[r][c] == 0) continuar;
int val = abs(board[r][c]);

bool hor = false, ver = false;
si (c ≤ 0 "
abs(board[r][c-1])==val " pulmonar abs(board[c+1])==val) hor = true;
si (r √≥ 0 ' r
abs(board[r-1][c])==val " pulmonar abs(board[r+1][c])==val) ver = true;

si (hor TENIDO VEZ) {
estable = falso;
board[r][c] = -abs(board[r][c]);
si (hor) {
board[r][c-1] = -abs(board[r][c-1]);
board[r][c+1] = -abs(board[r][c+1]);
}
si (ver) {
bordo[r-1][c] = -abs(board[r-1][c]);
bordo[r+1][c] = -abs(board[r+1][c]);
}
}
}
}

// 2. Crush (set a 0)
para (auto &row : bordo)
para (int &x : fila)
si (x 0) x = 0;

c) Retorno estable;
}

vaciado (vector seleccionador) {
int m = board.size(), n = board[0].size();
para (int c = 0; c) {}
int escriba = m-1; // siguiente fila gratis desde el fondo
para (int r = m-1; r 0; --r) {
(board[r][c]!= 0) {
junta[escribir][c] = junta[r][c];
[c] = 0;
- Escribir;
}
}
}
}
};
`` `

-...

## 2down⃣ Blog Article – “Cracking LeetCode 723 (Candy Crush): A Java‐Python‐C++ Guía para entrevistas de trabajo”

■ *Título*
■ # Candy Crush LeetCode 723** – *A Complete Java/Python/C++ Guía para el éxito de la entrevista*

■ **SEO Palabras clave**:
■ `Candy Crush LeetCode`, `LeetCode 723 solution`, `Candy Crush algoritmo`, `Java Python C++ soluciones`, ` algoritmo de entrevista de trabajo ' , ` consejos de entrevista técnica `

-...

### 📚 Tabla de contenidos

1. [Introducción](#introducción)
2. [Resumen del proyecto](#problema-summario)
3. [Key Challenges](#key-challenges)
4. [Solution Overview](#solution-overview)
5. [Detalles de implementación](Detalles de implementación)
6. [Code Snippets](#code-snippets)
7. [Análisis de complejidad](#complexidad-análisis)
8. [Bien, Bad & Ugly](#bueno-bad-ugly)
9. [Consejos de Interview](#interview-tips)
10. [Conclusión](#conclusión)

-...

Introducción

Candy Crush (LeetCode 723) es un clásico rompecabezas de red 2-D que combina *search* y *physics*.
A menudo se pregunta en entrevistas de estructura de datos porque obliga a los candidatos a pensar en:

* Operaciones simultáneas*
- ** mutación del Estado** (marcación negativa)
- Mecánica de gravedad**

Dominar este problema demuestra la maestría de arrays, bucles y cambios de estado iterativos - todo **debe tener** para una entrevista de ingeniería de software.

-...

## ## 2down⃣ Problem Summary

Dada una matriz `board[m][n]` (cada célula contiene un entero > 0 o `0` para vacío),
**Repetir** lo siguiente hasta que no se puedan aplastar más caramelos:

1. Cualquier carrera de 3 o más caramelos **adjacent** horizontal o verticalmente debe ser aplastado.
2. Los caramelos triturados se convierten en `0` (vacío).
3. Cualquier caramelo que tenga un '0' debajo cae **down** hasta que golpea otro caramelo o el fondo.

Devuelve la tabla estable final.

Constraints:

- 1 ≤ m, n ≤ 30
- 1 ≤ tabla [i] [j] ≤ 1000` (excepto 0 para vacío)

-...

#### 3down⃣ Principales desafíos

← Reto Silencio Por qué importa ¦ Pitfalls Típicos
Silencio...
Silencio **Tribunal simultáneo** Silencio Todas las carreras deben desaparecer **a una vez**; el aplastamiento parcial da respuesta incorrecta. TEN Crushing mientras se escanea – conduce a errores de cascada. Silencio
Silencio **Marking vs. crushing** Silencio Se requieren marcas negativas para que un caramelo en una carrera no se triture dos veces. tención Olvídate de unmark → bucle infinito. Silencio
Silencio **Gravidad** Silencio Después de cada trituración, los caramelos "drop" y pueden crear nuevas carreras. Silencio Usando enfoque similar a pila incorrectamente → O(m2n) en lugar de O(mn). Silencio
Silencio **Células de edge** Silencio Las carreras no pueden envolver alrededor del tablero. TENED-por-uno errores (por ejemplo, comprobando 'c+1' en la última columna). Silencio

-...

### 4down So Solution Overview

1. *Marcos*
* Escanear toda la tabla.
* Para cada célula no cero, compruebe los vecinos de izquierda/derecha y arriba/abajo.
* Si una carrera de ≥ 3 existe horizontal o verticalmente, marque todas las células involucradas haciendolas negativas.
* Mantenga una bandera 'cambiada' – si alguna célula está marcada, necesitamos otra iteración.

2. **Crush**
* Todas las células negativas se convierten en `0`.
* Si no hay celda marcada, el tablero es *stable* → bucle de salida.

3. *Drop*
* Para cada columna, mueva todas las células no cero a la parte inferior (técnica de punta de escritura).
* Establecer las células superiores restantes a `0`.

4. **Repetir** hasta que el tablero se estabilice.

El algoritmo es **en lugar** (O(1) espacio extra) y funciona hasta que no ocurran más trituraciones.

-...

Detalles de la Implementación

Silencio Idioma Silencio
Silencio----------------------------
Silencio **Java** Silencio Usa `Math.abs` para ignorar marcas, marcación negativa, puntero de escritura para la caída. tención Evita copiar toda la tabla; O(m n) por iteración. Silencio
Silencio **Python** Silencio Usa `abs` para evitar cambios de signo, lista de comprensión para la claridad. ← Leverages La composición dinámica de Python; todavía O(m n) por iteración. Silencio
Silencio **C++** Silencio `vector realizadovector interpretadovector fielint `` + `abs`, marca negativa, simple para-loops. tención Usa el índice `escribir' para una gota eficiente. Silencio

Todas las implementaciones son compatibles con el juez en línea de LeetCode.

-...

#### 6VIEW⃣ Complexity Analysis

Let `m` = rows, `n` = columns.

* Por iteración*
* Mark + crush: **O(m n)**
* Drop: **O(m n)** (cada columna escanea una vez)

* **Número de iteraciones*
En el peor de los casos, cada iteración elimina al menos un caramelo.
Ya que en la mayoría de los dulces existen, el número de iteraciones ≤ `m n`.

*Total Time*
`O(m n * iterations)` → **O(m n)2)** en el peor caso absoluto,
pero normalmente **O(m n)** para tablas aleatorias.

****Space*
En lugar: **O(1)** auxiliar.
(LeetCode 'board' en sí se cuenta como entrada.)

-...

### 7 pesquisa buena, mala

Silencio Silencio
Silencio------------Prince------
Silencio **Bien** Silencio • Iterante, fácil de entender. • Maneja los trituradores simultáneos correctamente. • Trabaja para todos los casos de borde (que se ejecutan en las fronteras).
Silencio **Bad** Silencio Silencio • La marcación negativa puede ser no intuitiva para los entrevistadores. • Código de verbosidad puede ocultar fallos si no es cuidadosamente revisado.
Silencio **Equiposamente** Silencio Silencio Silencio • Usando arrays temporales 3-D para tener marcas. • Llamando receptivamente triturado / gota que conduce a apilar el desbordamiento en tablas grandes. No restablecer la bandera «cambiada» → bucle infinito. Silencio

■ **Pro Tip**: Siempre empezar por escribir una función de ayuda que *detectos* a ejecutar, luego *aplicar* aplastar y *aplicar* caer. Mantiene la lógica limpia y reduce los errores por uno.

-...

### 8down⃣ Interview Tips

1. **Explicar la estrategia negativa de marcación** – por qué es necesario y cómo evita el en cascada.
2. **A través de un pequeño ejemplo** sobre papel (por ejemplo, tabla 4×4).
3. ** Enfoques alternativos de mención** (por ejemplo, BFS/DFS para carreras) y por qué son menos eficientes.
4. **Mostrar pruebas de unidad**: la cubierta corre esa solapa, corre a las esquinas, y el aplastamiento de la tabla completa.
5. **Discutir la complejidad del tiempo** – mostrar que usted entiende la naturaleza iterativa.
6. **Preguntas** – si no está seguro acerca de la parte “gravedad”, haga preguntas aclaratorias.

■ *Recordar*: Los entrevistadores están más interesados en su proceso *pensamiento* que el código final.

-...

Conclusión

Candy Crush (LeetCode 723) es más que un rompecabezas – es un punto de referencia para:

** Pensamiento algorítmico* *
- Cuidado con la manipulación estatal en el lugar
- *Conciencia por caso*

El truco *negative marking*, junto con la caída del puntero, produce código limpio, eficiente y listo para entrevistas.

Al dominar este problema en **Java, Python, y C++**, estarás bien preparado para cualquier pregunta *grid‐simulation* que surja en tu próxima entrevista técnica.

-...

■ **Takeaway**:
■ *Cuando usted puede implementar una tabla estable de Candy Crush en menos de 100 líneas de código, usted ha demostrado que puede manejar simulaciones de estado - una habilidad clave para cualquier backend o ingeniero de sistemas. *

-...

■ *¿Quieres más preparación para la entrevista? Echa un vistazo a nuestra serie en **Venta deslizante en 2-D Grids**, ** Traversales Gráfico**, y ** Programación Dinámica**. *

-...

■ *Author*: **[Su nombre]** – *Entrenador de Entrevista de Ingeniero de Software de Senior*
■ *Publicado*: **Marzo 2024**
■ *Actualizado*: **Abril 2024** – Se agregó la implementación C+++.

-...

**Feliz codificación & buena suerte con sus entrevistas!** 🚀

-...

Siéntete libre de adaptar o ampliar el artículo para tu blog personal o contenido de atención tecnológica.