-...
Título: LeetCode 1314. Matrix Block Sum -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código - Tres idiomas

A continuación se presentan implementaciones limpias, listas para la producción de **LeetCode 1314 – Matrix Block Sum** escrito en **Java, Python y C++**.
Los tres utilizan una suma de prefijo **2-D** (también llamada imagen integral) para calcular cada suma de bloque en **O(m × n)** tiempo y **O(m × n)** memoria auxiliar – la solución óptima para este problema.

■ **Consejo:** Las sumas de prefijo son un patrón clásico de entrevista. Dominarlos te da un impulso instantáneo para una amplia variedad de preguntas de “sumar suma”.

-...

## Java – Prefix‐Sum + Clean DP

``java
importa java.util. Arrays;

Solución de la clase pública {}

int[][] matrizBlockSum(int[][] mat, int k) {
int m = mat.length;
int n = mat[0].length;

/ / / 1 base prefijo suma array
int[][] pref = nuevo int[m + 1][n + 1];

para (int i = 1; i) =
para (int j = 1; j <= n; j+) {}
pref[i][j] = pref[i - 1][j] + pref[i][j - 1]
- pref[i - 1][j - 1] + mat[i - 1][j - 1];
}
}

int[][] ans = nuevo int[m][n];

para (int i = 0; i)
para (int j = 0; j) {}
int r1 = Math.max(0, i - k) + 1; // inclusive, 1-basado
int c1 = Math.max(0, j - k) + 1;
int r2 = Math.min(m, i + k + 1); // exclusiva
int c2 = Math.min(n, j + k + 1);

ans[i][j] = pref[r2][c2] - pref[r1 - 1][c2]
- pref[r2][c1 - 1] + pref[r1 - 1][c1 - 1];
}
}

devolver los ans;
}

// ---- para la prueba manual rápida...
public static void main(String[] args) {
Solución s = nueva solución ();
int[][] mat = {1,2,3},{4,5,6},{7,8,9}};
int[][] res = s.matrixBlockSum(mat, 1);
System.out.println(Arrays.deepToString(res));
}
}
`` `

-...

### Python – Fast Prefix‐Sum (NumPy-free)

``python
Solución de clase:
def matrizBlockSum(self, mat: List[List[int], k: int) - título List[List[int]]:
m, n = len(mat), len(mat[0])

# 1-based prefix sum
pref = [0] * (n + 1) para _ en rango(m + 1)]
para i en rango(1, m + 1):
row_sum = 0
para j en rango(1, n + 1):
row_sum += mat[i-1][j-1]
pref[i][j] = pref[i-1][j] + row_sum

ans = [[0] * n for _ in range(m)]
para i en rango(m):
para j en rango(n):
r1 = max(0, i - k) + 1
c1 = max(0, j - k) + 1
r2 = min(m, i + k +1)
c2 = min(n, j + k +1)
ans[i][j] = (
pref[r2][c2]
- pref[r1-1][c2]
- pref[r2][c1-1]
+ pref[r1-1][c1-1]
)
Retorno
`` `

■ **Nota:** El bucle interior está escrito deliberadamente en Python plano para la claridad. Si estás en Python 3.8+ puedes usar `itertools.accumulate` o `NumPy` para un ligero aumento de velocidad.

-...

## C++ – O(m·n) con 2-D Prefix Sum

``cpp
Incluido el título
usando std namespace;

Clase Solución {
public:
vector realizador identificadoint título de matrizBlockSum(vector identificadovector fielt int k) {
int m = mat.size(), n = mat[0].size();
vector seleccionado(n + 1, 0)

// Construir una suma prefijo basada en 1
para (int i = 1; i) {}
int rowSum = 0;
para (int j = 1; j)
rowSum += mat[i-1][j-1];
pref[i][j] = pref[i-1][j] + rowSum;
}
}

vector seleccionado(n, 0));

para (int i = 0; i) {}
para (int j = 0; j)
int r1 = max(0, i - k) + 1;
int c1 = max(0, j - k) + 1;
int r2 = min(m, i + k + 1);
int c2 = min(n, j + k + 1);
ans[i][j] = pref[r2][c2] - pref[r1-1][c2]
- pref[r2][c1-1] + pref[r1-1][c1-1];
}
}
devolver los ans;
}
};
`` `

-...

## 2. Blog Artículo – “Matrix Block Sum: The Good, The Bad, and the Ugly”

■ **SEO Palabras clave**: Matrix Block Sum, LeetCode 1314, 2-D suma de prefijo, programación dinámica, codificación de entrevistas, Java, Python, solución C++, entrevista de codificación, entrevista de trabajo, algoritmo.

-...

### H1 – Matrix Block Sum: Mastering a Classic LeetCode Problema

■ *“Given an `m × n’ matriz y un entero `k’, compute la suma de cada bloque `k`‐radius alrededor de cada célula.”*
■ Esta tarea aparentemente simple es un elemento básico en las entrevistas de codificación. Prueba su capacidad para transformar un bucle de fuerza bruta en una solución matemáticamente inteligente.

## H2 – El problema, en inglés sencillo

- ** Entrada**: `mat` - `m × n` matriz de enteros; `k` - entero no negativo.
- ** Salida**: `ans` - matriz del mismo tamaño donde cada `ans[i][j] ' iguala la suma de todos los elementos `mat[r][c] satisfacción
`respirador - i sometida ≤ k` y `resistentesc - j sufrimiento ≤ k`.
Las fronteras están truncadas – nunca se lee fuera de la matriz.

■ *¿Por qué importa esto? *
■ Los entrevistadores a menudo piden una solución “O(m × n), lo que significa que no se puede permitir un bucle anidado ingenuo para cada célula.

## H2 – Bien: El O(m × n) Prefix‐Sum Approach

← Paso Silencioso Lo que sucede
...------------------------------
Silencio 1. **Construir una suma prefijo de 2D** Silencio `pref[i][j]` = suma de todas las células en rectángulo `(0,0)` a `(i-1,j-1)`. ← Permite las consultas de rectángulo de tiempo constante. Silencio
Silencio 2. **Convertir cada consulta en un rectángulo de prefijo** Silencio El bloque alrededor de `(i,j)` es un rectángulo `[r1,r2] × [c1,c2]`. Silencio
Silencio 3. **Computar los ans en O(1) por celda** tención Para todas las células `m × n`. tención Tiempo total = `O(m × n)`. Silencio
Silencio 4. **Memoria** Silencioso `pref` es `(m+1)×(n+1)`; `ans` is `m×n`. Silencio Aceptable para restricciones hasta 100. Silencio

■ *Resultado*: 100% correcto, velocidad óptima y código limpio.

## H2 – Bad: The Brute‐Force `O(m × n × k2)` Solución

``python
para i en rango(m):
para j en rango(n):
total = 0
para r en rango(max(0, i-k), min(m, i+k+1):
para c en rango(max(0, j-k), min(n, j+k+1)):
total += mat[r][c]
ans[i][j] = total
`` `

- **Tiempo**: `O(m × n × k2)` → 106 × k2 operaciones.
Con 'k' hasta 100, esto puede volar hasta 1010 – demasiado lento.
- **Espacio**: Lo mismo que un esfuerzo óptimo, pero desperdiciado.

■ *¿Por qué es malo? *
■ Los entrevistadores esperan que pienses más allá de los obvios bucles anidados. La fuerza bruta es una bandera roja clásica.

## H2 – Ugly: Edge‐ Case Mishandling " Off‐ Por-Uno Trampas

1. **Off‐by-one in prefix indices**
- `pref` es 1-basado, pero muchos novatos olvidan el +1 offset, produciendo resultados incorrectos.
2. **Aprincipio literario**
- Olvidar a `max(0, ...)` o `min(m, ...)` conduce a errores array-out‐of-bounds.
3. *Desbordamiento del número entero*
- En lenguajes como Java o C++, las sumas acumulativas pueden exceder de 'int'. Use `long ' o `long long` si `mat[i][j]` puede ser grande.
4. **Nombre variable inconsistente**
- Mixing `r1`/`c1` for inclusive vs exclusive bounds confunde lectores.

■ *Evitando Ugly*:
■ 1. Funciones de ayuda de escritura `int clamp(int val, int low, int high)`;
■ 2. Tenga en cuenta la matriz de prefijo basada en 1;
■ 3. Prueba primero sobre las pequeñas matrices (`[[1]]`, `[1,2],[3,4]] ' .

## H2 – Algorithm Deep Dive: 2-D Prefix Sum Mechanics

Un prefijo 2D suma `pref[i][j]` se define como:

`` `
pref[i][j] = Governing_{r i, c י} mat[c]
`` `

La suma de cualquier sub-matrix `[r1, r2] × [c1, c2]` (inclusive) es:

`` `
S = pref[r2+1][c2+1]
- pref[r1][c2+1]
- pref[r2+1][c1]
+ pref[r1][c1]
`` `

Porque cada término añade o resta regiones superpuestas exactamente una vez.

■ *¿Por qué basado en 1? *
■ Los +1 turnos permiten que el “vacío” fila/column (“pref[0][*] = 0`) actúe como los casos de límite cero, simplificando los bordes.

### H2 – Consejos de implementación para la entrevista de trabajo

Silencio Lengua Silenciosa Silenciosa
Silencio--------------------
Silencio **Java** Silencio Use `long` for prefix sums; cast at output to `int` if problem guarantees no overflow. Silencio
Silencio **Python** Silencio Escribe el bucle prefijo en una sola línea, pero mantén `row_sum` para claridad. Muéstrale que conoce la fórmula de consulta "O(1)". Silencio
Silencio **C+** Silencio Preferir `vector seleccionadovector fielint sobre matrizs primas; evitar variables globales a menos que se especifique. Silencio
Silencio **Todo** Silencio **Explica tu idea primero**: Establezca el concepto prefijo-sum verbalmente antes de la codificación. Esto demuestra un pensamiento algorítmico. Silencio

### H2 – Resumen de complejidad (tablado)

TEN TERRIENTE TENIDO Tiempo TENIDO Espacio ANTERIENTE
Silencio--------------------------------------
TENIDO Brute‐Force TENIDO `O(m × n × k2) `` TENIDO `O(m × n)` TENIDO Sólo si `k` es diminuto (`k ANTE 5`). Silencio
tención Prefix‐Sum Silencioso `O(m × n)` Silencioso `O(m × n)` Silencio Mejor para todas las restricciones. Silencio
Silencioso Ventana (Alternativa) Silencioso `O(m × n)` (dos pases) Silencio `O(m × n)` Silencio Obras si usted puede mantener una suma rodante por fila. Silencio

■ *Pro Tip*:
■ Mostrar tanto el código como un diagrama **mental** de la consulta del rectángulo. Ayudas visuales impresionan a los entrevistadores.

### H2 – Pensamientos Finales: De Problema a Portfolio

*Matrix Block Sum* es más que un rompecabezas de codificación, es un microecosistema para programación dinamizada**, ** sumas de prefijo**, y ** manipulación de límites**.
Dominar te da:

- Confianza en transformar bucles anidados en fórmulas matemáticas.
- Un patrón reutilizable para futuros problemas de entrevistas que implican sumas acumulativas 2-D.
- Una insignia de honor: “Puedo resolver problemas de O(m × n) en segundos. ”

■ *Ready to ace your next coding interview? *
■ Practica la solución prefijo-sum en Java, Python y C++. Explíquelo en una entrevista de mock con tiempo, y observe a los reclutadores tomar nota.

### H3 – Llamada a la acción

■ **Compartir** su aplicación favorita en los comentarios.
■ **Descargar** los fragmentos de código completo arriba.
■ **Suscribir** para más “El Bien, el Mal y el Ugly” descompone los problemas de LeetCode.

-...

### H3 – Sobre el autor

■ Un ingeniero de software experimentado que ha limpiado entrevistas técnicas en Google, Amazon y Microsoft.
■ Pasionar sobre algoritmos limpios y mentorear la próxima generación de códecs.
■ Siga en LinkedIn: [@YourName](#) Silencio Blog: [yourblog.com](#)

-...

*End of article. *