-...
Título: LeetCode 1861. Rotating the Box -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1down Java, Python & C++ Soluciones para **LeetCode 1861 – Rotating the Box**

A continuación encontrará implementaciones limpias, listas para la producción para los tres idiomas de entrevista más populares.
Todas las soluciones siguen la misma idea:

1. **Aplicar la gravedad** – por cada fila, deslizar cada piedra (`#`) en la medida en que puede ir respetando los obstáculos (`*`).
2. **Rotación** – transponer la matriz y voltearlo horizontalmente (o utilizar el algoritmo clásico “rotate 90° en sentido de reloj”).

La complejidad del tiempo es **O(m × n)** y la complejidad del espacio es **O(1)** extra (la matriz de salida es el valor de retorno requerido).

-...

### 📄 Java (LeetCode-style)

``java
importa java.util. Arrays;

Solución de la clase pública {}

public char[][] rotaTheBox(char[] [] cuadro) {
int m = box.length; // filas originales
int n = box[0].length; // cols originales

/* 1 ride⃣ Aplicar gravedad – cada fila independientemente */
para (int i = 0; i)
int empty = n - 1; // farthest right empty spot
para (int j = n - 1; j 0; j--) {
si (box[i][j] == '*) { // obstáculo
vacío = j - 1; // siguiente lugar libre queda de él
} si (box[i] [j] == '#) { // stone
si (j != vacío) {
box[i][empty] = '#';
box[i][j] = '.
}
vacía...
}
}
}

/* 2 vídeos Ro girar 90° en sentido de reloj */
char[][] rotated = new char[n][m];
para (int i = 0; i)
para (int j = 0; j) {}
[j] [m - 1 - i] = box[i][j];
}
}
Retorno rotativo;
}

/* Arnés de prueba simple – eliminar para la presentación de LeetCode */
public static void main(String[] args) {
Solución s = nueva solución ();
char[][] input = {
'', '', '', ''
};
char[][] out = s.rotateTheBox(input);
para (char[] fila : fuera) System.out.println (Arrays.toString(row));
}
}
`` `

-...

### 🐍 Python (Python 3.9+)

``python
Solución de clase:
def rotate TheBox(self, box: list[list[str]]) - titulado[list[str]]:
m, n = len(box), len(box[0])

# 1 Aplicar la gravedad – cada fila independientemente
para i en rango(m):
vacío = n - 1
para j en rango(n - 1, -1, -1):
si box[i][j] == '*':
vacío = j) 1
elif box[i][j] == '#':
si j!= vacía:
box[i][empty] = '# '
box[i][j] = '. '
vacías 1

# 2 Cambio # girar 90° en el reloj
[[box[i][j] for i in range(m)][:-1] for j in range(n)]

# Ejemplo
si __name_ == "__main__":
s = Solución()
cuadrícula = [["#", ", "#"]
print(s.rotateTheBox(grid))
`` `

-...

### 🏗י C++ (C+17)

``cpp
Incluido el título
usando std namespace;

Clase Solución {
public:
vector de vectores: box) {
int m = box.size();
int n = box[0].size();

/* 1 ride⃣ Aplicar gravedad – cada fila independientemente */
para (int i = 0; i) {}
int empty = n - 1;
para (int j = n - 1; j 0; --j) {
si (box[i] [j] == '*) {
vacío = j - 1; // obstáculo bloquea el camino
} si (box [i] [j] == '#) {
si (j != vacío) {
box[i][empty] = '#';
box[i][j] = '.
}
-vacío; // siguiente piedra debe aterrizar a la izquierda
}
}
}

/* 2 vídeos Ro girar 90° en sentido de reloj */
vector seleccionado(n, vector asignado(m));
para (int i = 0; i)
para (int j = 0; j)
[j] [m - 1 - i] = box[i][j];

Retorno rotativo;
}
};
`` `

-...

## 2down⃣ Blog Article – "Rotating the Box: The Good, The Bad, and The Ugly"

■ **Título:** Rotating the Box (LeetCode 1861) – Una profundidad profunda, solución completa y consejos de entrevista
■ **Meta‐Description:** Master LeetCode 1861 “Rotating the Box” con paso a paso, código Java/Python/C++, análisis de complejidad, manejo de los bordes y explicaciones de entrevista. ¡Anota tu puntuación de la entrevista de codificación!
■ **Keywords:** rotando la caja, leetcode 1861, rotación de matriz, simulación de gravedad, prep de entrevista, entrevista de codificación, problema algorítmico, solución Java, solución Python, solución C++

-...

### #1# ## ## ##

En LeetCode se le da una cuadrícula 2-D que representa una vista frontal ** de una caja rectangular.
Las células pueden ser:

Personaje permanente
Silencio...
Silencio
Silencioso `*
Silencioso `.`

La caja está rota **90° de ancho de reloj**.
Las piedras caen directamente debajo de la gravedad, parando en un obstáculo, otra piedra o la parte inferior de la caja.
Los obstáculos nunca se mueven, y las piedras mantienen su posición horizontal durante la rotación.

Su tarea es devolver la rejilla después de la rotación.

■ ¿Por qué importa esto? * *
■ Prueba su capacidad para manipular los arrays 2-D, entender la simulación de gravedad y realizar la rotación de matriz, todos los temas comunes en las entrevistas de codificación.

-...

#### 2down⃣ El Bien: Lo que funciona

1. #Dos Pointer Gravity # Al escanear cada hilera de derecha a izquierda y mantener el “punto siguiente libre” (`vacío') podemos deslizar piedras en **O(n)** por hilera.
2. ** Rotación determinista** – Un único bucle anidado gira la matriz sin memoria adicional más allá de la red de resultados.
3. **Simplicity " Readability** – La solución utiliza sólo operaciones primitivas; no bibliotecas de lujo ni estructuras de datos complejas.
4. **Linear Complexity** – Con `m × n ≤ 250 000`, el algoritmo encaja cómodamente dentro de los límites de tiempo de LeetCode.

-...

#### 3down⃣ The Bad: Edge Cases " Gotchas

Silencioso Temas anteriores Explicación
...------------------------------
Silencio **Obstáculos adyacentes a las piedras** Silencio Una piedra justo al lado de un obstáculo no debe pasarla. La lógica de dos puntos establece `vacío = j - 1` cuando se encuentra `*`, asegurando las tierras de piedra que quedan de ella. Silencio
Silencio **Stonas ya en la columna más derecha** Silencio Deben permanecer puestos. Silencio Si `j == vacío`, el `si (j != vacío)` guardia salta movimientos innecesarios. Silencio
Silencio **Large grids** Silencio Demasiados bucles anidados podrían golpear el límite de recursión de Python? Evitamos la recursión; todos los lazos son iterativos. Silencio
Silencio **Non‐rectangular input** Silencio LeetCode garantiza un rectángulo, pero una solución robusta debe protegerse contra `box[i] == null`. Silencio

-...

#### 4down⃣ El Ugly: ¿Qué hay que ver

1. ** Índices Confusos** – Recuerde que después de la rotación, la fila original se convierte en una columna. La fórmula `rotated[j][m - 1 - i] = box[i][j]` puede tropezarte.
2. ** Entrada Mutable** – El algoritmo muta la caja original. Si necesitas el original para depurar, guarda una copia.
3. **Language‐Specific Pitfalls** –
* **Java**: Use `char[][]` (not `String[]`) to avoid immutable strings.
* **Python**: `list[list[str]]` se recomienda mantener la mutabilidad de la fila.
* **C++**: Evite fuera de límites con `vector asignadovector fieltro ``.

-...

#### 5down⃣ Code Walk-through (Java Edition)

``java
// 1 / ⃣ Aplicar la gravedad en cada fila
para (int i = 0; i)
int vaciado = n - 1; // celda libre más derecha
para (int j = n - 1; j ю= 0; j--) { // escaneado de derecha a izquierda
si (box[i][j] == '*) { // obstáculo – bloque piedras adicionales
vacías = j - 1;
} si (box[i] [j] == '#) { // stone
si (j != vacio) { // mover sólo si desplazados
box[i][empty] = '#';
box[i][j] = '.
}
vacía...
}
}
}
`` `

*¿Por qué funciona esto? *
Debido a que las piedras sólo pueden moverse a la izquierda en la rejilla **pre-rotación** (que se volverá “abajo” después de la rotación).
El puntero vacío siempre apunta al lugar vacío más cercano donde una piedra podría establecerse.
Cuando golpeamos un obstáculo, encogemos el área alcanzable moviendo `vacío' una célula izquierda.

-...

#### 6VIEW⃣ Complexity Analysis

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silenciosa gravedad por hilera **O(n)**
Silencio Todas las hileras Silencio **O(m × n)** Silencio **O(1)**
Silencioso Rotation Silencio **O(m × n)** Silencio **O(m × n)** ( matriz de salida)
Silencio **Total** Silencio**

-...

### 7down⃣ Quick Test (Python)

``python
s = Solución()
Rejilla =
["#", ", "*", "
["#", "#", "*", "
]
print(s.rotateTheBox(grid))
# Se prevé:
[['#', '.'],
['#', '#'],
# ['*', '*],
['.', '.']
`` `

-...

### 8down⃣ Interview Tips

- **Preguntar preguntas aclaratorias**: por ejemplo: ¿Las piedras mantienen posiciones horizontales después de la rotación? ”
- **Explicar su enfoque en voz alta**: caminar a través de la simulación de gravedad y rotación por separado.
- **Casos de bordes altos**: obstáculos junto a piedras, piedras en el límite, cuadrículas vacías.
- **La complejidad del tiempo es importante**: tranquilizar al entrevistador que no está usando bucles anidados que se iteran sobre toda la matriz más de dos veces.

-...

#### 9Ω⃣ SEO & Career Impact

- **Keywords**: *Rotating the Box, LeetCode 1861, rotación de matriz, simulación de gravedad, prep de entrevista, problema algoritmo, solución Java, solución Python, solución C+*
- **Meta Descripción**: *Master LeetCode 1861 “Rotating the Box” con paso a paso, solución completa en Java, Python y C++, análisis de complejidad y explicaciones de entrevista. *
- **Blog Post Hook**: “¿Quieres comenzar la pregunta de manipulación de matriz en tu próxima entrevista de codificación? Lea cómo resolver Rotating the Box en 30 segundos. ”

Mediante la publicación de este artículo en una plataforma que se clasifica para la solución “LeetCode 1861”, atraerás a gerentes de contratación que buscan activamente candidatos que puedan resolver problemas de entrevista rápida y limpiamente. Utilice un tono atractivo, fragmentos de código, y una sección "revisual" para mostrar su mentalidad de solución de problemas - exactamente lo que los reclutadores quieren.

-...

#### 🔟 Wrap‐Up

Rotating the Box puede parecer intimidante al principio, pero una vez que divide el problema en **gravity** y **rotación**, la solución es sencilla y elegante.
Con el código proporcionado en su idioma preferido y la explicación amigable de la entrevista anterior, usted estará listo para impresionar a cualquier reclutador haciendo frente a este clásico desafío de entrevista de codificación. ¡Buena suerte!

-...

¡Feliz codificación!
-...

■ *Author note: Siéntete libre de adaptar el artículo a tu propia voz o añade tus propios ejemplos “real-world”. Cuanto más contexto dé, más alto serán los reclutadores de probabilidades que lo vean como un activo valioso. *