-...
Título: LeetCode 1828. Consultas sobre el número de puntos dentro de un círculo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 1828 – “Preguntas sobre el número de puntos dentro de un círculo”
■ ** Objetivo:** Cuenta cuántos de los puntos dados se encuentran dentro (o en la frontera de) cada círculo de consulta.
■ **Platforms:** Java, Python, C++
■ **SEO Palabras clave:** LeetCode 1828, Consultas sobre el número de puntos dentro de un círculo, solución Java, solución Python, solución C++, entrevista de algoritmos, tiempo O(n2), consejos de entrevista de trabajo

-...

### 1. 📌 Declaración de problemas

Se les da:

Silencio Variable Silencio Significado
Silencio...
TENIDO `puntos[i] = [xi, yi]` ANTERIOR Coordenadas del punto *i*-th (0 ≤ xi, yi ≤ 500) Silencio
Silencioso `queries[j] = [xj, yj, rj]` Centro de la vida `(xj, yj)` y radio `rj` (1 ≤ rj ≤ 500)

Para cada consulta, muestre el número de puntos que satisfacen

`` `
(xi – xj)2 + (yi – yj)2 ≤ rj2
`` `

(Puntos en la frontera cuentan como dentro.)

Constraints:
`1 ≤ puntos. longitud, consultas. longitud ≤ 500`

-...

### 2. ️ Naïve Brute‐ Enfoque de la Fuerza

1. *Arriba todas las consultas. #
2. **Arriba cada punto. #
3. Compute squared distance and compare with `r2`.

■ ** Complejidad en el tiempo: ** `O(Q · P)` → en la mayoría de `500 × 500 = 250.000` controles de distancia.
■ ** Complejidad del espacio:** `O(1)` (además de la matriz de resultados).

Con los límites dados, esta solución pasa cómodamente, pero también exploraremos un método más rápido.

-...

### 3. 🧠 “Bien, Mal, Ugly” del Bruto‐Force

Silencio Silencio
Silencio------------Prince------
Silencioso **Implementación** tención Simple, one‐pass loops tención Requiere `Math.pow` o multiplicación manual ← Sobre-utilización de las matemáticas del punto flotante (`Math.pow`) puede ser lento e impreciso
Silencio **Performance** Silencio Aceptable para 500×500 Silencio Quadratic → puede llegar a ser pesado para mayores restricciones Silencio O(n2) puede llegar a límites de tiempo en pruebas más exigentes
Silencio **Readability** TEN Clear, pocas líneas TENIDO Código repetitivo TENIDO Duro de remojo para persianas (por ejemplo, rebosa si se utiliza int en grandes coordenadas) TEN
Silencio **Mantenibilidad** Silencio Fácil de entender Silencio No escala Silencio Duro de modificar para nuevas características (por ejemplo, puntos ponderados)

-...

#### 4. ffff00 Optimizando con un Sum Prefijo 2-D (Grid)

Debido a que todas las coordenadas se encuentran en `[0, 500]`, podemos pre-construir una red 2-D `cnt[x][y]` que registra cuántos puntos se sientan en cada celda. Luego computamos una suma de prefijo `pre[x][y]`. Para cualquier círculo podemos:

1. **Escribe más de x** desde `cx - r` a `cx + r`.
2. Para cada `x`, computar el `y`-range que satisface la desigualdad del círculo.
3. Utilice la suma prefijo para preguntar cuántos puntos hay entre los dos y-boundaries en *O(1)*.

Esto reduce cada consulta de `O(P)` a `O(r)` (≤ 500). Complejidad general: `O(P + Q·maxR)` → todavía bueno para los límites dados.

-...

### 5. 📚 Implementations

A continuación se encuentran soluciones limpias y de producción para **Java, Python y C++**.
Los tres utilizan el método brute-force para la claridad; la variante prefijo-sum también se muestra como un comentario para lectores avanzados.

-...

#### 5.1 Java (Java 17)

``java
// Archivo: Solution.java
importar java.util*;

Solución de la clase pública {}
public int[] countPoints(int[][] points, int[][] consultas) {
int qLen = consultas. longitud;
int[] result = new int[qLen];

para (int i = 0; i) {}
int cx = consultas[i][0];
int cy = consultas[i][1];
int r = consultas[i][2];
largo r2 = (long) r * r; // use long to avoid overflow

int cnt = 0;
(int[] p : points) {
dx largo = p[0] - cx;
long dy = p[1] - cy;
si (dx * dx + dy *
}
result[i] = cnt;
}
Resultado de retorno;
}

--------- Versión opcional optimizada de la red --------
// Pre-compute a 2D prefix sum for O(r) query time.
// Descomiendo si quieres usarlo en lugar del bucle ingenuo.
public int[] countPointsGrid(int[] puntos, int[][] consultas) {
int final MAX = 500;
int[][] cnt = nuevo int[MAX + 1][MAX + 1];
para (int[] p : points) cnt [p[0]][p[1]]+++;

// Construir sumas prefijas
int[][] pre = nuevo int[MAX + 2][MAX + 2];
para (int x = 0; x <= MAX; ++x) {
para (int y = 0; y <= MAX; ++y) {
pre[x + 1][y + 1] = cnt[x][y] + pre[x][y + 1]
+ pre[x + 1][y] - pre[x][y];
}
}

int qLen = consultas. longitud;
int[] res = nuevo int[qLen];
para (int i = 0; i) {}
int cx = consultas[i][0];
int cy = consultas[i][1];
int r = consultas[i][2];
int minX = Math.max(0, cx - r);
int maxX = Math.min(MAX, cx + r);
total = 0;

para (int x = minX; x <= maxX; ++x) {
int dx = x - cx;
int maxDy = (int) Math.floor(Math.sqrt(r * r - dx * dx));
int minY = Math.max(0, cy - maxDy);
int maxY = Math.min(MAX, cy + maxDy);
total += queryPrefix(pre, minX, minY, maxX, maxY);
}
res[i] = total;
}
restitución;
}

int queryPrefix(int[][][] pre, int minX, int minY, int maxX, int maxY) {}
pre[maxX + 1][maxY + 1] - pre[minX][maxY + 1]
- pre[maxX + 1][minY] + pre[minX][minY];
}
---
}
`` `

**Por qué esto está listo para el trabajo* *

- Usa 'long' para evitar el flujo entero.
- Evita 'Math.pow' para la velocidad.
- Nombres variables claros ( " cx " , " , " r2 " ).
- No hay dependencias externas.

-...

#### 5.2 Python 3

``python
# File: solution. py
de la importación Lista

Solución de clase:
def countPoints(self, points: List[List[int],
consultas: List[List[int]]) - No. List[int]:
res = []
para cx, cy, r en consultas:
r2 = r
cnt = 0
para x, y en puntos:
dx = x - cx
dy = y - cy
si dx * dx + dy *
cnt += 1
re.append(cnt)
retorno

# -----
# Opcional optimización basada en la red (sumas prefijo)
# -----
# def countPointsGrid(puntos, consultas):
# MAX = 500
# cnt = [[0]*(MAX+1) for _ in range(MAX+1)]
# Para x, y en puntos:
# cnt[x][y] += 1
# pre = [0]*(MAX+2) for _ in range(MAX+2)]
# for x in range(MAX+1):
# for y in range(MAX+1):
# pre[x+1][y+1] = cnt[x][y] + pre[x][y+1] + pre[x+1][y] - pre[x][y]
# def query(minx, miny, maxx, maxy):
# return pre[maxx+1][maxy+1] - pre[minx][maxy+1] - pre[maxx+1][miny] + pre[minx][miny] [miny]
# res = []
# for cx, cy, r in queries:
# total = 0
# for x in range(max(0, cx-r), min(MAX, cx+r)+1):
# dx = x - cx
# max_dy = int(r*r - dx*dx)**0.5)
# miny = max(0, cy-max_dy)
# maxy = min(MAX, cy+max_dy)
# total += query(x, miny, x, maxy)
# res.append(total)
# Return res
`` `

**Python-friendly highlights**

- La escritura de explícito mantiene el tipo de código seguro para analizadores estáticos.
- Usa el aritmético entero para la velocidad.
- La versión opcional de la cuadrícula se comenta pero listo para copy‐paste.

-...

#### 5.3 C+17

``cpp
// Archivo: solution.cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector implicadoConteo de puntosPoints(vector seleccionadovector realizador seleccionado,
vector asignador implicados iguales consultas) {}
vector significar uns
para (auto golpe q : consultas) {
int cx = q[0], cy = q[1], r = q[2];
largo largo r2 = 1LL * r * r * r; // 64‐bit guard
int cnt = 0;
para (auto pulsa p : puntos) {}
dx largo largo = p[0] - cx;
largo largo largo dy = p[1] - cy;
si (dx * dx + dy *
}
ans.push_back(cnt);
}
devolver los ans;
}

/* ---
// Aplicación opcional de la rejilla optimizada (resumo prefijo)
---
vector identificadoint títuloPointsGrid(vector identificadovector fielint implica puntos
vector asignador implicados iguales consultas) {}
const int MAX = 500;
vector seleccionado(MAX+1)
cnt [p[0]] [p[1]]++;

// 2‐D sumas de prefijo
vector identificadovector interpretadoint confianza pre(MAX+2, vector asignadoint confianza(MAX+2, 0)
para (int x=0; x ==MAX; ++x)
para (int y=0; y consigna=MAX; ++y)
pre[x+1][y+1] = cnt[x][y] + pre[x][y+1] + pre[x+1][y] - pre[x][y];

auto query = [ afectada](int minx, int miny, int maxx, int maxy) {
pre[maxx+1][maxy+1] - pre[minx][maxy+1]
- pre[maxx+1][miny] + pre[minx][miny];
};

vector res;
para (auto golpe q : consultas) {
int cx = q[0], cy = q[1], r = q[2];
total = 0;
para (int x = max(0, cx-r); x <= min(MAX, cx+r); ++x) {
dx largo largo = x - cx;
int maxdy = static_cast fielint(sqrt(r*r - dx*dx));
int miny = max(0, cy-maxdy);
int maxy = min(MAX, cy+maxdy);
total += query(minx=min(0, cx-r), miny, maxx=max(0, cx+r), maxy);
}
res.push_back(total);
}
restitución;
}
-...
};
`` `

*Características inteligentes para el trabajo*

- Evita `pow()` mediante la multiplicación de enteros.
- " largo " garantiza la seguridad contra el desbordamiento.
- Estándar `traducidos/stdc++.h header mantiene el archivo mínimo.

-...

### 6. Recaptura de la complejidad

Silencioso en la aplicación
Silencio.
tención Brute‐force Silencioso `O(Q · P)` (≤ 2,5 × 105 operaciones) Silencio
Silencio Grid‐prefix (opcional) Silencio `O(P + Q·maxR)` (≤ 2,5 × 105 + 500·500) Silencio `O(1)` más `O(MAX2)` memoria de rejilla (Ω 250k ints)

Ambos enfoques son **bien dentro del límite de 1 segundo** en LeetCode. La variante de rejilla brilla cuando crecen las restricciones (por ejemplo, 10.000 puntos o 10.000 consultas).

-...

### 7. 🧪 Caso de prueba de muestras

``text
puntos = [1, 1], [2, 2], [3, 3], [4, 4]
[2, 2, 2], [1, 1, 1], [0, 0, 10]]
`` `

Silencio Silencio Silencio
Silencio...
TENIDO (2, 2, 2) TENIDO 3 (puntos a (1,1), (2,2), (3,3) están dentro)
Silencio (1, 1, 1) Silencio 1 (sólo (1,1)) Silencio
Silencio (0, 0, 10) 4 (todos los puntos dentro de un gran círculo)

La ejecución de cualquiera de las tres implementaciones sobre esta entrada devuelve `[3, 1, 4]`.

-...

#### 8. Гле Edge‐Case Checklist

Silencio tóxico Qué ver
Silencio...
Silencio **Large radius** (`r = 500`) Silencio `dx2 + dy2` puede llegar a `2.5 × 105` → se ajusta en `int` pero usa `long`/`long` para estar seguro. Silencio
[0, 0, ...]`. Silencio
Silencio **Puntos Duplicados** Silencio Cada duplicado contribuye por separado – el algoritmo cuenta todos ellos. Silencio
Silencio **Todos los puntos en la frontera** Silencio Todavía deben ser contados; la desigualdad es `≤`. Silencio
Silencio **Overflow** Silencio Use 64-bit (`long`/`long`) para el cálculo de distancia. Silencio

-...

### 9. 🏁 Pensamientos finales

- **Para los entrevistadores**: La solución O(Q·P) directa es una base sólida. Muestra el dominio de los lazos básicos, las fórmulas de distancia y el manejo cuidadoso del tipo.
- Para los reclutadores**: Su código debe ser **compactado, correcto y seguro**—el ejemplo Java arriba cumple con esos criterios.
- Para el autoaprendizaje. Pruebe el bucle ingenuo para la versión prefijo de la red. Enseña sumas de prefijo 2-D, que aparecen en muchas preguntas de algoritmo avanzado (resultas de rango, distancia de Manhattan, etc.).

-...

### 10. 🎯 Take‐away for the Next Job Interview

1. Empieza a ser simple. Muestra que puedes resolver el problema con lógica clara antes de bucear en optimizaciones.
2. ** Explique sus compensaciones.** Los entrevistadores aman cuando se habla del “bueno, malo, feo” de su solución.
3. **Mantenga el código limpio:**
- Evitar llamadas de función innecesarias (`Math.pow`).
- Usar enteros de 64 bits donde el desbordamiento es un riesgo.
- Nombrar variables descriptivas.
4. **Más rigurosamente**: Incluya los casos de esquina en sus pruebas de unidad.
5. # Hablando de escalar # Mencione cómo se podría mejorar la solución si las limitaciones crecieron (sumas de prefijo grave, indexación espacial, etc.).

Al seguir estos pasos no sólo ace LeetCode 1828, sino también demostrar la mentalidad de ingeniería que buscan los reclutadores.

¡Feliz codificación! ▪

-..