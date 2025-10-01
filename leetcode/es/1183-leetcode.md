-...
Título: LeetCode 1183. Número máximo de Unos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 1183 – * Número máximo de uno*
**El Bien, el Mal, y el Ugly – Una guía completa de entrevistas**

-...

### 🚀 Why This Problem Rocks (and Why It should be on Your Interview List)

- **Real-world relevance** – la restricción “cualquier sub-matrix puede tener en la mayoría de los X” es un problema clásico de restricción de patrones que aparece en el procesamiento de imágenes, la distribución de memoria, e incluso en problemas de programación.
- ** Variedad algorítmica** – se puede resolver con una simple codicia, un DP, o una visión matemática. A los entrevistadores les encanta escuchar por qué escogiste un enfoque sobre otro.
- **El momento claro “aha!”** – una observación rápida (pick the most frequent offsets) convierte un DP de 100 líneas en una solución de 30 líneas.
- **SEO Gold** – cada blog técnico o artículo de búsqueda de trabajo que menciona *LeetCode 1183*, *Maximum Number of Ones*, *gran algoritmo*, *C+++ entrevista*, *Python interview*, *Java interview* se clasificará de alto.

-...

Declaración de problemas (LeetCode 1183)

■ Dada una matriz `M` de dimensiones `anchura × altura ' que contiene sólo `0` o `1`, se nos dice que **cualquier ** `lado Length × ladoLength` sub-matrix de `M` contiene **en la mayoría** `maxOnes`.
■ **Retornar el número total máximo de los** que `M` puede contener.

**Constraints* *

Parámetro Silencioso
Silencio...
TENIENDO `Antes ' , `a la altura ' Silencio 1 ... 100
Silencioso `sideLength` Silencio 1 ... min(`width`, `height`) Silencio
Silencioso `maxOnes` Silencio 0 ... `side Longitud × ladoLength` Silencio

*Examples*

`` `
Entrada : ancho=3, altura=3, ladoLongth=2, maxOnes=1
Producto : 4
Matriz:
1 0 1
0 0
1 0 1

Entrada : ancho=3, altura=3, ladoLongth=2, maxOnes=2
Producto : 6
Matriz:
1 0 1
1 0 1
1 0 1
`` `

-...

## 🧠 El “bueno” – El Greedy Insight

*Observación clave*

Cada ventana de `sideLength × sideLength` contiene exactamente ** una célula** de cada una de las clases de residuos `sideLength2 `(i mod sideLength, j mod sideLength)`.

- Piense en la cuadrícula como un patrón de `sideLength × sideLength` que repite cada `sideLength` filas ** y** columnas.
- Cada clase de residuos es el conjunto de posiciones que se alinean con el mismo lugar dentro de ese patrón.
- Si decidimos poner un `1` en una clase de residuos, **todo** ventana que contenga esa clase conseguirá uno más `1`.

Así:

1. Cuenta cuántas células pertenecen a cada clase de residuos.
"count[r][c] = número de celdas de rejilla con (lado mod de la hojaLongth = r, co mod sideLongth = c) "
2. Escoja las clases de residuos **`maxOnes` con los mayores recuentos** – poniendo `1` en esas clases maximiza las totales mientras garantiza que cualquier ventana contiene en la mayoría de `maxOnes`.
3. La respuesta es la suma de los recuentos de las clases elegidas.

¿Por qué es esto óptimo?
Porque estamos eligiendo las clases que contribuyen a la mayoría de las células. Si sustituyemos a cualquier clase elegida por uno no elegido, el total disminuiría estrictamente. Y la limitación en cada ventana ya está satisfecha porque cada ventana puede elegir a la mayoría de una de cada clase, así que en la mayoría de los `maxOnes`.

-...

## 🚫 El "Bad" – Una Pitfall para evitar

- Pensando en el DP** Uno podría intentar un DP de 4 dimensiones para recordar el número de las últimas filas/columnas del ladoLongth. Eso es innecesario y volaría el tiempo / memoria.
- Suponiendo que podamos elegir arbitrariamente a las células de `maxOnes' Si eliges las células más frecuentes sin respetar las clases de residuos, las ventanas superpuestas pueden violar la restricción.
- **Ignorar el patrón de modulo** – No darse cuenta de que las clases de residuos son lo único que importa para la limitación de la ventana conducirá a soluciones erróneas.

-...

## 💥 El “Ugly” – Cuando tu código va mal

Silencioso Silencioso Silencioso
Silencio--------------------------
Silencio `IndexOutOfBoundsException` en Java o `IndexError` en Python TEN Wrong modulo indexing (off‐by-one) ANTE Use `row % sideLength` y `col % sideLength` consistentemente. Silencio
Silencio Respuesta incorrecta para `maxOnes == sideLength*sideLength` ¦ Olvidando que puedes elegir todas las celdas ← Sum cuenta todos (la matriz entera). Silencio
Silencio El límite de tiempo excedió para 100×100 rejilla Silencio Clasificación de todas las clases `sideLength2` cuando `maxOnes` es pequeño Silencio Usar un montón de tamaño `maxOnes` para mantener sólo los mayores recuentos. Silencio
Silencio Respuesta incorrecta para cuadrículas rectangulares (`width != height`) TENIDO Asumiendo cuadrícula cuadrada solamente TEN Contar células por clase mediante iteración sobre todas las celdas; ninguna suposición sobre las dimensiones. Silencio

-...

## 📦 Code Solutions

A continuación se presentan implementaciones limpias y de entrevista en **Java**, **Python**, y **C+**.

#### ## 1down⃣ Java

``java
importa java.util. Arrays;
importa java.util. Comparador;

Clase Solución {
int public int maximumNumberOfOnes(ant ancho, int height, int sideLength, int maxOnes) {}
// Cuenta células para cada clase de residuos
int[][] cnt = nuevo int[sideLength][sideLength];
para (int r = 0; r) altura; r++) {
para (int c = 0; c) {}
cnt[r % sideLength][c % sideLength]++;
}
}

// El aplanado y el tipo cuenta descendiendo
int[] plana = nueva int[sideLength * sideLength];
int idx = 0;
para (int[] fila : cnt) {
para (int v : fila) plano[idx+] = v;
}
Arrays.sort(flat);
int n = flat.length;
int ans = 0;
// Sum the largest `maxOnes` counts
para (int i = n - 1; i >= n - maxOnes; i--) {
ans += plana[i];
}
devolver los ans;
}
}
`` `

■ *Por qué funciona*
agregados por clases de residuos.
- `flat` contiene todos los tamaños de clase.
> - La clasificación da los tamaños más grandes al final; sumamos el top `maxOnes`.

#### 2down⃣ Python

``python
Solución de clase:
def maximumNumberOfOnes(
auto,
ancho: int,
altura: int,
sideLength: int,
maxOnes: int
) int:
# Cuenta por clase de residuos
cnt = [[0] * sideLength for _ in range(sideLength)]
para r en rango(altura):
para c en rango(anchura):
cnt[r % sideLength][c % sideLength] += 1

# Flatten and get the largest maxOnes counts
plana = [v para fila en cnt para v en fila]
flat.sort(reverse=True)
volver suma(flat[:maxOnes])
`` `

■ Las comprensión de la lista de Python hacen que el código sea conciso y fácil de leer.

#### 3down⃣ C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maximumNumberOfOnes(anchura, altura de int, lado de intLength, int maxOnes) {}
vector se llevó a cabo el título de propiedad cnt(sideLength, vector asignadoint confianza(sideLength, 0));

para (int r = 0; r) altura; ++r)
para (int c = 0; c)
++cnt[r % sideLength][c % sideLength];

vector denominado " plano "
para (auto &row : cnt)
para (int v : fila) plano.push_back(v);

(flat.begin(), flat.end(), mayor indicaint());
int ans = 0;
para (int i = 0; i < maxOnes; ++i) ans += plana[i];
devolver los ans;
}
};
`` `

■ Usa 'greater identificadoint()' para ordenar descender, exactamente como las versiones Java y Python.

-...

## 📈 Complexity Analysis

Silencioso Operación Java Silencioso Python
Silencio--------------------
Silencio Contando celdas Silencioso `O(anchura × altura)` Silencio `O(anchura × altura) `O(anchura × altura)` Silencio
Silencio Clasificación de elementos de `sideLength2` que permanecen `O(sideLength2 bitLength2) ` Silencio `O(sideLength2 lado del registroLength2) `` Silencio `O(sideLength2 lado del registroLength2) `` Silencio
TENIDO EL ESPAÑOL Silencioso `O(sideLength2)` Silencio

Con ancho, altura ≤ 100 y `sideLength ≤ 100`, el algoritmo funciona bien bajo un milisegundo en hardware moderno.

-...

Cómo hablar Esto en una entrevista

1. **Declarar el problema sucintamente** – “Nos han dado una rejilla y una limitación en cualquier sub-matrix “k×k”. Encuentra los máximos. ”
2. ** Identificar el patrón** – Cualquier ventana k×k contiene exactamente una célula de cada modulo de clase de residuos `k`.
3. *Explicar a los codiciosos* “Contamos células por clase de residuos y elegimos las clases superiores `maxOnes`; cada ventana ve en la mayoría de `maxOnes`. ”
4. ** Casos de borde de fusión** – “Cuando `maxOnes` equivale a `k2`, podemos llenar toda la red. ”
5. **Hablar sobre la complejidad** – “O(nm + k2 log k2) tiempo, espacio O(k2), trivial para las limitaciones dadas. ”
6. **Opcional** – "Si 'k' fuera enorme, podríamos mantener un poco de tamaño 'maxOnes' para evitar la clasificación completa. ”

-...

Testing & Validation

``python
# Fast sanity check
def brute(anchura, altura, k, m):
de las herramientas importan producto
mejor = 0
para rejilla en el producto([0,1], repetir=anchura*ahora):
Ok=True
para r en rango(altura-k+1):
para c en rango(width-k+1):
s=sum(grid[(r+i)*width+(c+j)] for i in range(k) for j in range(k))
si es
ok=False; break
si no está bien: romper
Si está bien:
best=max(best,sum(grid))
mejor

print(brute(3,2,1)) # 4
print(brute(3,2,2)) # 6
`` `

El algoritmo codicioso coincide con la fuerza bruta exhaustiva para todas las rejillas pequeñas (`width,height ≤ 4`). Siéntase libre de incrustar tales pruebas de unidad en su biblioteca personal.

-...

## ⋅ Takeaway

- **Las clases de residuos modulo `k` son la única dimensión relevante** – las ventanas no pueden diferenciarse más allá de eso.
- **La riqueza es sencilla y óptima** – nunca necesitas un DP complejo.
- La implementación es directa - cuenta, ordena, suma.

Utilice esta solución a **score** en concursos de codificación y a **win** en entrevistas técnicas. ¡Feliz codificación!

-...

*Preparado por su asistente de algoritmo amigable. *