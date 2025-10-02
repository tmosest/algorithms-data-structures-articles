-...
Título: LeetCode 2201. Conde Artifacts que pueden ser extraídos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Solución de 3 idiomas a LeetCode 2201
■ **Problema**: *Artículos de los contingentes que pueden ser extraídos*
■ **Dificultad**: Medium

A continuación encontrará una implementación limpia y lista para la producción en **Java, Python y C+**.
Los tres utilizan el mismo enfoque O(n2) peor, pero se ejecutan en O(n2) tiempo y O(n2) espacio, que está perfectamente bien dadas las limitaciones (`n ≤ 1000`).

-...

#### 1.1 Java – `HashSet` + `Map`

``java
importar java.util*;

Clase Solución {
int digArtifacts(int n, int[][] artifacts, int[][] dig) {
// Mapa cada célula que ha sido cavada al artefacto id que lo ocupa.
Mapa seleccionadoInteger, Integer confianza cellToArtifact = new HashMap correspond();
para (int id = 0; id > artifacts.length; id+) {}
int[] a = artefactos[id];
para (int r = a[0]; r > = a[2]; r++) {
para (int c = a[1]; c)
cellToArtifact.put(r * n + c, id);
}
}
}

// Cuenta cuántas células de cada artefacto han sido cavadas.
int[] uncovered = nuevo int[artifacts.length];
int extracted = 0;
(int[] d : dig) {
int key = d[0] * n + d[1];
Integer id = cellToArtifact.get(key);
si (id != null) {
si (++ no descubierto [id] == ConteoCells(artifacts[id], n) {
extraído+;
}
}
}
Retorno extraído;
}

int countCells(int[] a, int n) {
// (r2 - r1 + 1) * (c2 - c1 + 1) es en la mayoría 4 por declaración de problema
(a[2] - a[0] + 1) * (a[3] - a[1] + 1);
}
}
`` `

-...

### 1.2 Python – `set` + diccionario

``python
de la importación Lista

Solución de clase:
def digArtifacts(
auto, n: int, artifacts: List[List[int], dig: List[List[int]]
) int:
# Celda de mapa - índice de artefactos
cell_to_id = {}
para idx, (r1, c1, r2, c2) en enumerado (artifactos):
para r en rango(r1, r2 + 1):
para c en rango(c1, c2 + 1):
cell_to_id [(r, c)] = idx

descubierta = [0] * len(artifactos)
extraído = 0
para r, c en cava:
idx = cell_to_id.get(r, c))
si idx no es Ninguno:
descubierta[idx] += 1
si se descubre[idx] == (artifactos[idx][2] - artifacts[idx][0] + 1) * (
artifacts[idx][3] - artifacts[idx][1] + 1
):
extraído += 1
Regreso extraído
`` `

-...

### 1.3 C++ – `unordered_map` + vector

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int digArtifacts(int n, vector obtenidosvector seleccionador implicados iguales artifacts, vector armonizadovector fieltro estrecho) {
unordered_map se llevó mucho tiempo, ent confianza cellToId;
auto key = [n](int r, int c) { return (long long)r * n + c; };

para (int id = 0; id > artifacts.size(); ++id) {
a = artefactos[id];
para (int r = a[0]; r > = a[2]; ++r)
para (int c = a[1]; c
cellToId[key(r, c)] = id;
}

vector implicado no descubierto(artifacts.size(), 0);
int extracted = 0;

para (auto golpe d : dig) {
long long k = key(d[0], d[1]);
auto = cellToId.find(k);
si (lo != cellToId.end()) {
int id = it- segundos;
si (++ no descubierto[id] == ConteoCells(artifacts[id], n))
++extracted;
}
}
Retorno extraído;
}

privado:
int countCells(cont vector identificadoint
(a[2] - a[0] + 1) * (a[3] - a[1] + 1); // ≤ 4 por declaración
}
};
`` `

■ ** Complejidad del tiempo**: `O(n2)` en el peor caso (cuando todas las células son parte de los artefactos).
■ ** Complejidad del espacio**: `O(n2)` para el mapa del hash que contiene hasta 'n2' entradas.

-...

## 2. Artículo del Blog – “Mastering LeetCode 2201: The Good, The Bad, and The Ugly”

* Título SEO*
■ **Artífactos de bolsillo que pueden ser extraídos – Java, Python, C++ Soluciones + Entrevista Consejos**
■ *Meta Descripción: *
■ Aprende a resolver LeetCode 2201 con código claro y listo para la producción en Java, Python y C++. Comprender el problema, las trampas y las estrategias de entrevista. ¡Anota tu puntuación de la entrevista de codificación!

-...

#### 2.1 Introduction

Cuando usted consigue una entrevista de ingeniería de software, los problemas de LeetCode *Medium* son el lugar dulce: son lo suficientemente desafiantes para mostrar la profundidad pero todavía solvable con fundamentos sólidos. Uno de estos problemas es **2201 – Conde Artifacts que pueden ser extraídos**. Se siente como un rompecabezas, dado un conjunto de artefactos rectangulares y una serie de excavaciones, cuenta cuántos artefactos están completamente descubiertos.

En este artículo caminaremos por el **bueno** (por qué el problema es una gran pregunta de entrevista), el **bad** (pocas comunes y por qué fallan las soluciones ingenuas), y el **ugly** (menos optimistas pero todavía correctos enfoques). También presentaremos tres soluciones limpias, lingüísticas-agnósticas en Java, Python y C++, listos para pegar en su preparación de entrevistas o repositorio de aplicaciones de trabajo.

-...

### 2.2 Problema Recap

- **Grid**: `n × n` (0-indexed).
- **Artifacts**: Hasta `105` rectángulos, cada uno cubriendo a la mayoría de 4 células. No se superponen dos artefactos.
- **Digs**: Hasta 105 coordenadas celulares únicas.
- ** Objetivo**: Devuelve cuántos artefactos tienen *todas* sus células excavadas.

■ **Por qué importa:**
√ - Manijas * espaciamiento espacial* (célula → artefacto).
- Trabaja con *sparse* entrada (los artefactos y las excavaciones son mucho menos que `n2`).
√ - Tests habilidad para mapear coordenadas 2D a claves 1‐D.

-...

### 2.3 The Good – What Makes This Problem Great

¦ Feature Silencio Por qué Es Beneficial Silencio
Silencio...
Silencio **Tamaño pequeño del artefacto** Silencio Limita los lazos interiores; usted puede iterar con seguridad sobre las células de cada artefacto. Silencio
Silencio **No solapamiento** tención simplifica el mapeo: cada célula pertenece a la mayoría de un artefacto. Silencio
TEN **Sparse digs** TEN Alienta el uso de conjuntos de hash/maps en lugar de densos arrays para la eficiencia. Silencio
Silencio ** Dificultad media** Silencio Muestra que estás cómodo con mapas de hash, conversión 2D a 1D y contando. Silencio

### 2.4 El mal – Errores comunes

TENIDO ANTERIOR ANTERIOR CONSECUENCIA
Silencio...
Silencio **O(n2) simulación de rejilla completa** Silencio Con `n = 1000`, eso es 1 000 000 células; aceptable, pero innecesario si los artefactos son pocos. Silencio
Silencio **Escaneo luminoso para cada excavación** Silencio `dig.length * artifacts.length` puede llegar a las operaciones `10`. Silencio
Silencio **Uso de arrays 2D para todas las células** Silencioso de memoria: 1 000 000 booleans está bien, pero si usted tuvo que almacenar ids de artefacto por célula, se vuelve caro. Silencio
tención **Ignorando la garantía “en la mayoría de las 4 celdas”** ← Leads to over-engineering (por ejemplo, usando árboles de intervalos). Silencio

## 2.5 The Ugly – Naïve Brute‐ Enfoque de la Fuerza

``python
# O(artifacts * dig) ~ 10^10
def feo_solution(n, artifacts, dig):
extraído = 0
para un en artefactos:
all_exposed = True
para r en rango(a[0], a[2] + 1):
para c en rango(a[1], a[3] + 1):
si [r, c] no en cava:
all_exposed = False
descanso
si no todo_expuesto:
descanso
si all_expuesto:
extraído += 1
Regreso extraído
`` `

*¿Por qué es feo? *
- Escaneo lineal sobre 'dig' para cada célula en cada artefacto.
- La complejidad del tiempo explota incluso para entradas moderadas.
- Difícil de leer y depurar.

### 2.6 El código limpio – Solución eficiente

La idea clave: **hash every dug cell** once, and **map each cell to its owning artifact**. Entonces, para cada excavación, sólo aumenta un contador para ese artefacto. Cuando el contador es igual al tamaño del artefacto, lo hemos descubierto completamente.

#### 2.6.1 2-D → 1-D Key Trick

Una coordenadas 2-D `(r, c)` se puede convertir en un solo número:

`` `
llave = r * n + c // obras porque 0 ≤ r, c
`` `

Esto funciona para mapas de hash en los tres idiomas.

#### 2.6.2 Pseudocode

`` `
crear celda de mapasToArtifact
para cada artefacto id, rect:
para r de rect.r1 a rect.r2:
para c del rect.c1 al rect.c2:
cellToArtifact[key(r,c)] = id

uncoveredCount = array[artifactCount] = 0
extraído = 0

para cada excavación (r,c):
si llave(r,c) en la celdaToArtifact:
id = cellToArtifact[key(r,c)]
uncoveredCount[id] += 1
si no se encuentraCount[id] == size_of(artifact[id]):
extraído += 1

Regreso extraído
`` `

#### 2.6.3 Complexity Analysis

TEN TERRITORIO TEN TERRITORIDAD
Silencio...
TENIDO `cellToArtifact` ANTE `O(total_cells)` ≤ `4 * artifacts.length` ≤ 4 × 105 ANTE
Silencio Procesando excavaciones Silencioso `O(dig.length)` ≤ 105
Silencio Total Silencio **O(total_cells + dig.length)** → lineal en tamaño de entrada. Silencio
Silencio espacio adicional Silencio **O(total_cells)** para el mapa de hash + contadores. Silencio

-...

### 2.7 Código de Producción-Ley Snippets

*(ver soluciones de 3 idiomas arriba)*

Los tres comparten el mismo esqueleto algorítmico, adaptado a las expresiones lingüísticas. Siéntase libre de copiar-paste en su repositorio, anota con comentarios, o utilizarlos como referencia de estudio.

-...

### 2.8 Interview Tips " Takeaways

1. **Explicar su diseño primero** – hablar del mapa de “celular → artefacto”.
2. **Mención de la tecla 2-D a 1-D** – es un truco clásico en la mente de los entrevistadores.
3. **Hablar sobre el tamaño del artefacto atado** – muestra que usted entiende las restricciones del problema.
4. **Edge cases**: cero artefactos, cero excavaciones, o excavaciones que extrañan todos los artefactos, los cubren en pruebas unitarias.

■ *“Cuando esté en duda, pregunte al entrevistador qué considera el mejor enfoque de estructura de datos.”*
■ Esto indica la colaboración y mantiene la conversación dinámica.

-...

### 2.8 Wrap‐Up

LeetCode 2201 es un pequeño problema de conteo espacial bien entrenado que prueba un puñado de habilidades de estructura de datos básicos. La solución eficiente es conceptualmente simple pero elegante: hah todas las celdas de excavación, células de mapa a artefactos, y cuentan exposiciones. Las implementaciones Java, Python y C++ arriba están listas para usar, probadas en batalla, y pueden ser agregadas a cualquier base de código “listo para visión”.

■ **Siguiente paso**: Agregue pruebas de unidad, ejecute casos aleatorios grandes y practique explicándole verbalmente el algoritmo.
■ **Bonus tip**: Empuja tu repositorio a GitHub, y añade un "README" que lista el problema, las restricciones y las soluciones: tu propio compañero de entrevista.

¡Feliz codificación y buena suerte en la próxima entrevista!

-...

*© 2024 Su nombre – Todos los derechos reservados. *

-...

■ *Descargos*
■ Las muestras de código se proporcionan con fines educativos y no están vinculadas a ninguna aplicación laboral específica. Siempre siga los estándares de codificación y las directrices de estilo de su organización durante una entrevista.