-...
Título: LeetCode 174. Dungeon Juego -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🏰 Dungeon Game – LeetCode 174
**Problema** Silencio**
-... Silencio...
[174. Dungeon Game](https://leetcode.com/problems/dungeon-game/) Silencio Java, Python, C++

■ Un caballero debe atravesar una mazmorra de 2D desde la parte superior izquierda hasta la celda inferior derecha, moviéndose sólo **a la derecha** o **abajo**.
■
■ Cada célula contiene un valor negativo (daño demonio), 0 (habitación vacía) o un valor positivo (orden de sanación).
■ La salud del caballero debe ** permanecer siempre ≥ 1**; de lo contrario muere.
■ Regrese el *mínimo* salud inicial que el caballero necesita para rescatar a la princesa en la habitación inferior derecha.

-...

## Solution Overview

El problema es un problema clásico **Programación Dinámica (DP)** – necesitamos saber el *mínimo* salud requerida *antes* entrar en una celda para que después del efecto de la habitación el caballero sobreviva y pueda alcanzar la meta.

Observación clave
*De cualquier celda sólo tenemos dos posibles siguientes pasos: derecho o abajo. *
Por lo tanto, la *salud requerida* de una célula depende sólo del *mínimo requerido de la salud* de las dos células adyacentes a la derecha y abajo.

Trabajamos **hacia atrás** desde la celda de la princesa (abajo derecho) hasta la célula inicial (top-left).
Por cada celda `dp[i][j]`:

`` `
necesario = min( dp[i+1][j], dp[i][j+1] ) // la salud mínima necesaria en el siguiente paso
dp[i][j] = max( 1, needed - dungeon[i][j] ) // sanar o tomar daño
`` `

Las condiciones de los límites se manejan al tratar los movimientos fuera de los límites como `∞` (por lo que nunca se convierten en el mínimo).

La respuesta es `dp[0][0]`.

## Time / Space Complexity
TEN ANTERIOR Java / Python / C++
Silencio...
Silencio **Tiempo** Silencioso `O(m·n)` – uno pasa por la rejilla
Silencio **Espacio** Silencioso `O(m·n)` para la mesa del DP (puede reducirse a `O(n)` con una sola fila DP)

-...

## 📦 Code Implementations

A continuación se presentan implementaciones limpias y bien agregadas para **Java, Python, y C++**.
Los tres utilizan un enfoque *bottom‐up* DP y son `O(m·n)` tanto en el tiempo como en el espacio.

#### ## 1down⃣ Java

``java
importa java.util. Arrays;

Solución de la clase pública {}
int calculateMinimumHP(int[][] dungeon) {}
int m = dungeon.length, n = dungeon[0].length;
int[][] dp = nuevo int[m + 1][n + 1]; // extra row/col para facilitar el manejo de límites
para (int[] fila : dp) Arrays.fill(row, Integer. MAX_VALUE);
dp[m][n-1] = dp[m-1][n] = 1; //

para (int i = m - 1; i 0; --i) {
para (int j = n - 1; j 0; --j) {
int need = Math.min(dp[i+1][j], dp[i][j+1]) - dungeon[i][j];
dp[i][j] = Math.max(1, necesidad);
}
}
dp[0][0];
}
}
`` `

#### 2down⃣ Python

``python
de la importación Lista

Solución de clase:
def calculateMinimumHP(self, dungeon: List[List[int]) - título int:
m, n = len(dungeon), len(dungeon[0])
# dp[i][j] : salud mínima necesaria para entrar en la célula (i, j)
dp = [float('inf')] * (n +1) para _ en rango(m + 1)]
dp[m][n-1] = dp[m-1][n] = 1 # centinelas

para i en rango(m-1, -1, -1):
para j en rango(n-1, -1, -1):
necesidad = min(dp[i+1][j], dp[i][j+1]) - dungeon[i][j]
dp[i][j] = max(1, necesidad)

retorno dp[0][0]
`` `

#### 3down⃣ C++

``cpp
Clase Solución {
public:
int calculateMinimumHP(vector seleccionadovector identificadoint implicancia reducida dungeon) {}
int m = dungeon.size(), n = dungeon[0].size();
vector seleccionado(n + 1, INT_MAX)
dp[m][n-1] = dp[m-1][n] = 1; // sentinel

para (int i = m - 1; i 0; --i) {
para (int j = n - 1; j 0; --j) {
int need = min(dp[i+1][j], dp[i][j+1]) - dungeon[i][j];
dp[i][j] = max(1, necesidad);
}
}
dp[0][0];
}
};
`` `

■ Las tres soluciones funcionan en **O(m·n)** tiempo y uso **O(m·n)** espacio extra.
■ Pasan todos los casos oficiales de prueba LeetCode y pueden manejar las limitaciones máximas (200 × 200).

-...

## 📚 Blog Artículo – “El Bien, el Mal, y el Ugly of the Dungeon Game”

■ **Título: *El Bien, el Mal el Ugly de LeetCode 174 – Juego de Dungeon (Java, Python, C++)*
■ **Meta Descripción:** Master LeetCode 174 “Dungeon Game” con claras soluciones Java, Python, " C++. Aprende el truco de programación dinámica, las trampas y cómo llegar a la entrevista.

-...

#### Introduction

Si te estás preparando para entrevistas de codificación, **LeetCode 174 – Dungeon Game** es un problema clásico que prueba tu comprensión de la programación dinámica (DP). Puede parecer intimidante, pero el principio subyacente es simple: **Trabajar hacia atrás** desde la célula de la princesa y computar la *salud mínima* necesaria para sobrevivir al camino.

En este post, diseccionamos la solución, caminamos a través de tres implementaciones de lenguaje, y discutimos lo que hace que el problema *bueno*, lo que podría ir mal (*bad*), y cómo evitar errores desagradables (*ugly*). Todos con encabezados amigables de SEO para que los reclutadores encuentren su experiencia al instante!

-...

### 1. Por qué este problema es una pregunta de entrevista “buena”

Reason ← Explicación
Silencio...
tención ** DepthAlgorithmic** tención Requiere conocimiento de DP, manejo de límites y trucos de optimización. Silencio
Silencio **Idioma Agnóstico** Silencio La misma lógica se aplica a Java, Python, C++, etc. Silencio
Silencio **Edge‐Case Rich** ← Números negativos, ceros, tamaños de cuadrícula variable, y valores grandes fuerzan un manejo cuidadoso de la reflujo entero. Silencio
Silencio **Test‐Case Variety** Silencio LeetCode proporciona cuadrículas grandes al azar, lo que hace que las soluciones de fuerza bruta fallen al instante. Silencio
Silencio **Career‐Boosting** Silencio Resuelve que muestra la maestría del DP, una grapa en muchas entrevistas. Silencio

-...

### 2. La “buena” – La clara y limpia solución DP

- **Backward DP**: Comience en la celda de la princesa y propaga la salud necesaria al revés.
- **Simplicidad**: Dos líneas de recurrencia, sin pila de recidiva, sin memoización.
- ** Complejidad Determinística**: `O(m·n)` tiempo y espacio—bien dentro de los límites de 200 × 200 rejillas.
- **Scalable**: Fácilmente adaptado al espacio DP (O(n) de una dimensión) si es necesario.

**Takeaway**: Si puedes explicar este enfoque atrasado en menos de 2 minutos, estás listo para muchas preguntas de entrevista.

-...

### 3. El “Bad” – Pitfalls comunes

Por qué rompe la vida Fijar
Silencio...
tención **Recidivación desplegable sin memoización** TENIDOS A tiempo exponencial, apilar el desbordamiento. Silencio
Silencio **Using `0` as the initial sentinel** Silencio `dp[i][j]` can become `0`, causing the knight to die immediately. TENIDO Use `INT_MAX` / `float('inf')` as sentinel and enforce `max(1, ...)`. Silencio
Silencio **Las condiciones de los límites incorrectos** Silencio Off‐por-uno errores hacen la respuesta `-1` o enorme. Silencio Añádase una fila/col adicional inicializada a " INF " y ponga `dp[m][n-1] = dp[m-1][n] = 1 ' .
Silencio **Desbordamiento entero** Silencio Subtracting large negative values can exceed 32‐bit int. Silencio Use 64‐bit integers (`long` in Java, `long` in C++). Silencio
Silencio **Ignorando el requisito de salud inicial de `-1`** Silencio Algunas soluciones devuelven `dp[0] [0] - 1`. La recurrencia ya garantiza `≥ 1`; devolver `dp[0][0]`. Silencio

-...

### 4. La Complejidad Ugly – Complejidad innecesaria y código difícil de leer

- **Over-engineering**: Agregar funciones o clases de ayuda innecesarias.
- *Nombres variables indeseables* (aaaaaaaaaaaaaaaa ' b ' c ' ) esa lógica oscura.
- **Missing comments**: Futuro usted (o un reclutador) tendrá que adivinar la intención.
- **Límites codificados por miedo** ( " dp[201][201] " en lugar de un tamaño dinámico.

**Best Practice**: Mantener el código conciso, comentar la recurrencia y dejar que el compilador maneje los casos de borde.

-...

### 5. Optimización para entrevistas " SEO

- **Use “Programación Dinámica”, “Bottom-up DP”, “Minimum Health”** en encabezados y meta tags.
- **La complejidad del tiempo de gran alcance** (`O(m·n)`) en el primer párrafo: los motores de búsqueda aman las métricas cuantificadas.
- **Incluya una sección “Recapto rápido”** con puntos de bala para lectura rápida.
- **Agregue un fragmento de alta definición de código** para cada idioma: ayuda a buscar bots indexar el código.

-...

### 6. Código Snippets – La referencia rápida

Recurrencia clave de la Lengua Silenciosa Silencio
Silencio...
Silencio **Java** Silencio `dp[i][j] = Math.max(1, Math.min(dp[i+1][j], dp[i][j+1]) - dungeon[i][j]); Silencio
Silencio **Python** Silencio `dp[i][j] = max(1, min(dp[i+1][j], dp[i][j+1]) - dungeon[i][j] Silencio
Silencio **C+** Silencio `dp[i][j] = max(1, min(dp[i+1][j], dp[i][j+1]) - dungeon[i][j]); Silencio

Siéntase libre de copiar y pegar las soluciones completas arriba en su IDE.

-...

### 7. Conclusiones

LeetCode 174 – Dungeon Game es un problema *clásico* DP que se puede resolver limpiamente con un enfoque atrasado. Evite los obstáculos comunes, mantenga su código legible y practique explicándole la recurrencia en términos simples. Domine este problema, y tendrá un fuerte punto de conversación de entrevistas que muestra sus cortes de programación dinámica.

■ **Ley para impresionar a los reclutadores?** Deja el código en tu cartera, añade el artículo a tu blog, y muestra que sabes cómo convertir un problema “hard” en una solución “limpia”. 🚀

-...

## 🎯 Final Checklist

1. **Reun** cada aplicación contra las pruebas de muestra de LeetCode.
2. **Perfil** su código: `O(m·n)` tiempo, `O(m·n)` espacio.
3. ** Explique** la solución verbalmente—práctica un lanzamiento de 2 minutos.
4. **Publicar** el artículo del blog (SEO-optimized).
5. **Añada el código y el artículo a su GitHub README.

Buena suerte, y que su caballero siempre permanezca vivo! 🏆