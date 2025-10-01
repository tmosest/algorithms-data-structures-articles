-...
Título: LeetCode 533. Pixel solitario II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. 533. Pixel II solitario – Soluciones multi-idioma

A continuación se presentan implementaciones limpias y de producción en **Java**, **Python**, y **C+**.
Los tres siguen la misma estrategia espacial O(m·n), O(m + n.

``text
Entrada: imagen = ["W", "B", "W", "B", "B", "W"],
["W", "B", "W", "B", "B", "W"],
["W", "B", "W", "B", "B", "W"],
["W", "W", "B", "W", "B", "W"] ],
objetivo = 3
Producto: 6
`` `

-...

## Java

``java
importar java.util*;

clase pública LonelyPixelII {
public int findBlackPixel(char[][] imagen, int target) {
int m = picture.length, n = picture[0].length;
int[] rowCnt = nuevo int[m];
int[] colCnt = nuevo int[n];
Mapa seleccionadoString, Integer confianza rowMap = nuevo HashMap garantizado();

// 1. El conde B está en cada fila, columna y cadena de la fila de la tienda
para (int i = 0; i)
StringBuilder sb = nuevo StringBuilder();
para (int j = 0; j) {}
char ch = picture[i][j];
sb.append(ch);
si (ch == 'B') {
fila Cnt[i]+;
colCnt[j]+;
}
}
String rowStr = sb.toString();
si (rowCnt[i] == target) { // sólo filas con materia de destino exacta
rowMap.put(rowStr, rowMap.getOrDefault(rowStr, 0) + 1);
}
}

// 2. Para cada columna, si contiene el objetivo B y todas las filas con B
// en esta columna tiene el mismo patrón, añadir el objetivo a la respuesta
int ans = 0;
para (int j = 0; j) {}
si (colCnt[j] != target) continuar; // columna también debe tener objetivo B's

// recoger todas las filas que tienen una B en la columna j
Criar primeroRow = null;
booleano mismo = verdadero;
para (int i = 0; i)
si (foto[i] [j] == 'B') {
String rowStr = nuevo String(picture[i]); // row as string
si (primer Raw == null) primero Fila = fila Str;
si (!rowStr.equals(firstRow)) { same = false; break; }
}
}
si (same ' primerosRow != null) {
// todas las filas con B en esta columna son idénticas
ans += blanco; // cada uno de esos B es un pixel solitario
}
}
devolver los ans;
}
}
`` `

■ **Nota**: 'nuevas String(picture[i])'' funciona porque 'picture[i]` es un `char[]`.
■ Para las matrices muy grandes es posible que desee mantener el `rowStr` del primer lazo en lugar de reconstruirlo.

-...

## Python

``python
Solución de clase:
def findBlackPixel(self, picture: List[List[str]], target: int) - título int:
m, n = len(picture), len(picture[0])
row_cnt = [0] * m
col_cnt = [0] * n
row_map = {}

# 1. Conde B's y construir cuerdas de fila
para i en rango(m):
row_str = ".join(picture[i])
cnt = row_str.count('B')
row_cnt[i] = cnt
si cnt == objetivo:
row_map[row_str] = row_map.get(row_str, 0) + 1

j, ch in enumerate(picture[i]):
si ch == 'B':
col_cnt[j] += 1

# 2. Columnas de exploración
ans = 0
para j en rango(n):
si col_cnt[j]!= objetivo:
continuar

primera_row = Ninguno
mismo = verdadero
para i en rango(m):
si la imagen [i] [j] == B:
r = ".join(picture[i])
si primero_row es Ninguno:
first_row = r
elif r!= first_row:
mismo = Falso
descanso
si lo mismo y lo primero:
ans += objetivo
Retorno
`` `

-...

### C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int findBlackPixel(vector seleccionadovector) imagen, meta int) {}
int m = picture.size(), n = picture[0].size();
vector implicado(m, 0), colCnt(n, 0);
unordered_map buscadostring, int confianza rowMap;

// 1. El Conde B está en filas y columnas, recuerde cadenas de filas
para (int i = 0; i) {}
cuerda Str;
rowStr.reserve(n);
para (int j = 0; j)
char ch = picture[i][j];
rowStr.push_back(ch);
si (ch == 'B') {
++rowCnt[i];
++colCnt[j];
}
}
si (rowCnt[i] == target)
++rowMap[rowStr];
}

// 2. Inspección de cada columna
int ans = 0;
para (int j = 0; j)
si (colCnt[j] != target) continúan;

cuerda primero Row = ";
bool mismo = verdadero;
para (int i = 0; i) {}
si (foto[i] [j] == 'B') {
string curRow(picture[i].begin(), picture[i].end());
si (primeroRow.empty())
primero Row = curRow;
si (curRow != firstRow) {
mismo = falso;
ruptura;
}
}
}
si (same " Unidos " )
ans += objetivo; // cada coincidencia B es solitario
}
devolver los ans;
}
};
`` `

-...

## 2. Artículo del Blog
#### *Cracking LeetCode 533 – Lonely Pixel II: El Bien, el Mal, y el Ugly*

■ **Keywords**: LeetCode, 533, Lonely Pixel II, codificación de entrevistas, Java, Python, C++, algoritmo, ingeniería de software, entrevista de trabajo, estructuras de datos, complejidad del tiempo, complejidad espacial.

-...

### 1. Panorama general de los problemas

LeetCode 533 *Solo Pixel II* te pide contar **Pixeles solitarios negros** en una imagen binaria.
Un pixel `'B' en la posición `(r, c)` es solitario si:

1. Row `r` contiene exactamente **`target`** píxeles negros.
2. Columna `c` contiene exactamente **`target`** píxeles negros.
3. Cada fila que tiene un píxel negro en la columna `c` es **identical** para remar `r`.

La imagen es un `m × n` grid (`1 ≤ m, n ≤ 200`).
La tarea es devolver el número de píxeles solitarios.

-...

### 2. Por qué es una gran pregunta de entrevista

* Profundidad conceptual* Prueba la comprensión de 2‐D array traversal, mapas de hash y la manipulación de cuerdas.
- ¿Qué? Requiere cuidadoso contar para permanecer dentro de O(m·n) tiempo y O(m + n) espacio.
- **La lengua versatilidad**: Solvable en Java, Python, C++, o cualquier idioma que soporta mapas de hash y el manejo de cuerdas.

-...

### 3. La “buena” – La estrategia óptima

#### 3.1 High-Level Idea

1. **Píxeles negros por fila y por columna**.
*Las flechas* se almacenan como cuerdas; si una fila tiene exactamente 'target` píxeles negros, guardamos su cadena en un mapa de hash.

2. ** Columnas validadas**:
Para cada columna que contiene exactamente 'target` píxeles negros, compruebe que **todas las filas que tienen una ''B' en esta columna son **identical**.
Si lo son, cada "B" en esa columna es un pixel solitario.

3. ** Resultado**:
Cada columna válida contribuye a los píxeles solitarios "target" (uno por fila que tiene un `'B'' en esa columna).

##### 3.2 Why It Works

- **Acondicionamiento real**: El mapa garantiza que sólo se consideran filas con píxeles negros `target`.
- Condicion de colon**: El bucle de columna asegura que las columnas también tienen píxeles negros 'target`.
- ¿Qué? Al comparar cadenas de filas confirmamos que todas las filas que comparten la columna son idénticas.

El algoritmo funciona en `O(m·n)` porque atraviesamos la matriz un número constante de veces, y las operaciones del mapa son `O(1)` en promedio.

-...

### 4. El “Bad” – Pitfalls comunes

Silencio Pitfall Silencio Lo que pasa
Silencio...
Silencio **Using `picture[i].toString()`** Silencio Devuelve la referencia del array, no el contenido de la fila. Silencio Convierta la fila en una cuerda: 'nueva cuerda (fotografía[i])' o '" "join(row)` en Python. Silencio
Silencio **Ignorando las filas duplicadas** Silencio Contando cada fila idéntica por separado conduce a doble contabilización. Mantenga un mapa de frecuencia de cuerdas de fila y multiplíquese sólo una vez por fila. Silencio
Silencio **No validar el recuento de columna** Silencio Algunas columnas pueden tener más o menos `'B'' que `target`. i) Subir las columnas donde `colCnt[j]!= target`. Silencio
Silencio **Compararing rows incorrectly** Silencio Usando la identidad de objeto (`==`) en Java/Python en lugar de la igualdad de contenido. ← Use `equals()` en Java, `==` on strings in Python (estrings are interned), or `=` on C++ `std:string`. Silencio
Silencio **Iniciar cadenas intermedias** Silencio Construyendo cuerdas repetidamente puede alcanzar límites de tiempo. ← Construir una vez durante el primer paso; reutilizar en el control de columna. Silencio

-...

### 5. Los “Ugly” – Edge Cases y Gotchas

- Toda la foto blanca. Ninguna fila o columnas satisfacen la condición de `target` → retorno 0.
- **Single row/column**: `m == 1` o `n == 1` todavía funciona; algoritmo degenera a un escáner 1‐D.
- **El grupo es igual 1**: Sólo los `'B'' aislados pueden sentirse solos; las columnas con más de un `'B' deben ser descartadas.
* Limitaciones de memoria* Para la matriz de 200×200 maximal, el mapa de cadena es diminuto (traducido 4 kB), por lo que no hay problema.

-...

### 6. Aplicación en tres idiomas

A continuación se limpian, los snippets de producción (Java, Python, C++).
Los tres siguen la estrategia óptima descrita anteriormente.

- **Java**: Usa `HashMap escritoString, Integer confianza` para almacenar recuentos.
- **Python**: Usa `dict` y concatenación de cuerdas.
- **C+**: Utiliza las conversiones `noordered_map realizadasstring, int confianza` y `std::string`.

■ **Consejo**: Cuando se presenta en LeetCode, asegúrese de que la firma de la función coincida con el requisito de la plataforma (findBlackPixel` en Java, `Solution.findBlackPixel` en Python, etc.).

-...

### 7. Entrevista-Ley de asesoramiento

1. **Declara tu plan**: Establezca los dos pases y por qué cada condición importa.
2. **Explicar la complejidad**: `O(m·n)` tiempo, `O(m + n)` espacio auxiliar.
3. **Edge-case sanity checks**: Mostrar que consideraba filas individuales, columnas, matrices blancas.
4. **Trade-offs**: Si la memoria fuera más ajustada, usted podría evitar almacenar cadenas de filas por la piratería de las filas.
5. **Testing**: Mostrar algunos casos de prueba rápida, incluyendo los ejemplos del aviso.

■ **Por qué esto importa para un trabajo**: Los entrevistadores no se preocupan sólo por la respuesta correcta sino por cómo *pensar*. Demostrar una solución clara y optimizada indica habilidades fuertes para resolver problemas que se traducen en ingeniería del mundo real.

-...

### 8. Take-away

- **Solo Pixel II** es un problema *medium* LeetCode que empaca varios conceptos clave de CS: 2-D array traversal, mapas de hash, igualdad de cadenas, y cuenta cuidadosa.
- La solución óptima es simple una vez que se separa la fila‐, columna- y controles de identidad.
- Ser capaz de implementarlo limpiamente en Java, Python o C++ muestra versatilidad, un atractivo rasgo para los roles de ingeniería de software.

-...

##### Final Thought

Si puede convertir una declaración de problema confusa en un algoritmo elegante y eficiente, acaba de ganar un boleto de oro para su próxima entrevista de codificación. ¡Feliz codificación y buena suerte en tu búsqueda de trabajo!