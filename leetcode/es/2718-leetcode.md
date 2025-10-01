-...
Título: LeetCode 2718. Suma de matriz después de consultas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 2718 – Sum of Matrix After Queries
**TL;DR** – El truco es caminar a través de las consultas *backwards*, mantener una bandera “ver” para cada fila y columna, y añadir la contribución de cada *unique* fila / columna sólo una vez.
Complejidad: **O(queries + n)** tiempo, **O(n)** espacio.
A continuación encontrará soluciones listas para copiar en **Java, Python, y C++** (todas anotadas), seguido de un breve post de blog amigable de SEO que explica la idea, por qué funciona, y cómo se puede utilizar para impresionar a los entrevistadores.

-...

## 1. El Código

#### 1.1 Java

``java
importar java.util*;

Solución de la clase pública {}
*
* Devuelve la suma de todas las células en una matriz n x n después de aplicar
* una lista de renglón/columna sobrescribe las consultas.
*
* @param n tamaño de la matriz (n x n)
* @param lista de consultas, cada consulta = [tipo, índice, val]
* @return total sum as long
*/
matrices públicas largasSumQueries(int n, int[][ ] {
boolean[] rowSeen = nuevo boolean[n];
boolean[] colSeen = nuevo boolean[n];
int rowCount = 0, colCount = 0;
larga suma = 0;

// Proceso de última consulta a primera – “las últimas victorias”
para (int i = queries.length - 1; i >= 0; i--) {
int type = queries[i][0];
int idx = consultas[i][1];
int val = queries[i][2];

(tipo == 0) { // fila sobreescritura
si (!rowSeen[idx]) {}
suma += (long) (n - colCount) * val; // sólo columnas frescas
rowSeen[idx] = true;
fila Conteo++;
}
} más { // columna sobreescritura
si (!colSeen[idx]) {}
suma += (long) (n - rowCount) * val; // sólo filas frescas
colSeen[idx] = verdadero;
colCount++;
}
}
}
restitución;
}
}
`` `

### 1.2 Python

``python
matrices defSumQueries(n: int, queries: list[list[int]) - título int:
"
Devuelve la suma de una matriz n x n después de procesar todas las consultas.
consultas: [tipo, índice, val], ...]
"
row_seen = [False] * n
col_seen = [False] * n
row_cnt = col_cnt = 0
total = 0

para el tipo, idx, val in reversed(queries):
if typ == 0 and not row_seen[idx]:
total += (n - col_cnt) * val
row_seen[idx] = True
row_cnt += 1
elif typ == 1 y no col_seen[idx]:
total += (n - row_cnt) * val
col_seen[idx] = True
col_cnt += 1

total
`` `

#### 1.3 C++

``cpp
Clase Solución {
public:
matriz larga largaSumQueries(int n, vector seleccionadovector seleccionadoint implicados implicados implica consultas) {}
vector asignadobool confianza rowSeen(n,false), colSeen(n,false);
int rowCnt = 0, colCnt = 0;
larga suma = 0;

// Desvío desde el final – última operación “vinos”
para (int i = (int)queries.size() - 1; i √= 0; --i) {
int type = queries[i][0];
int idx = consultas[i][1];
int val = queries[i][2];

si (tipo == 0 " Pulse " ) {}
suma += 1LL * (n - colCnt) * val;
rowSeen[idx] = true;
++row Cnt;
} si (tipo == 1 " л !colSeen[idx]) {}
suma += 1LL * (n - rowCnt) * val;
colSeen[idx] = verdadero;
++colCnt;
}
}
restitución;
}
};
`` `

■ **Las tres implementaciones se ejecutan en el tiempo O (queries + n) y O(n) memoria** – lo suficientemente rápido para los límites `n ≤ 104` y `queries ≤ 5·104`.

-...

## 2. Blog Artículo – “El Bien, el Mal, y el Ugly of Sum of Matrix After Queries”

#### 2.1 Introduction

LeetCode 2718 – *Sum of Matrix After Queries* – es un problema clásico de entrevista que prueba su capacidad para pensar en “sobreescrituras” en un espacio de 2D.
La tarea es simple de decir: comienza con una matriz all‐zero `n × n`, entonces se aplican una serie de tareas **row** o **column**. Después de todas las consultas, computar la suma total de la matriz.

¿Por qué importa esto?
* En los sistemas del mundo real a menudo *sobreescribir* filas o columnas enteras (pensar actualizaciones de hojas de cálculo, sombreadores de GPU, o operaciones a granel de bases de datos).
* Los entrevistadores aman problemas que requieren que usted evite una simulación obvia `O(n2)`, porque revelan su conciencia de la optimización algorítmica.

A continuación caminaré por el **bueno** (lo que es correcto), el **bad** (pocas comunes), y el **ugly** (las soluciones desordenadas, pero posibles).

-...

### 2.2 The Good – A Clean O(queries + n) Solución

*Key Insight*
La consulta *última* que toca una fila o columna en particular es la única que importa para la matriz final.

Por lo tanto, podemos procesar las consultas **backwards**.
Mientras se iteraba desde el final:

1. Mantenga dos arrays booleanos: `rowSeen[n]` y `colSeen[n]`.
2. Mantener los recuentos de cuántas filas o columnas distintas ya han sido “fijadas” (`rowCnt`, `colCnt`).
3. Cuando encuentres una consulta de filas `[0, r, val]` que no se ha visto:
* Toda columna que ** no haya sido aún sobrescrita contribuye `val ' a la suma.
* Esa contribución es `val * (n - colCnt)`.
4. Haga la lógica simétrica para una consulta de columna.

Debido a que cada fila o columna se cuenta **una vez** (la primera vez que lo ve en orden inverso), el algoritmo es lineal.

**Por qué es “bueno”* *
* Tiempo lineal, espacio lineal – bien dentro de los límites de LeetCode.
* Intuitivo una vez que entiendas “las últimas victorias”.
* Obras para las limitaciones máximas ( " n = 104 " , " , " = 5·104 " ).

-...

### 2.3 The Bad – Naïve Approaches That Die

TENCIÓN TENIDO Tiempo TENIDO Espacio ANTERIOR ¿Por qué falla
Silencio--------------------------------------
Silencio ** simulación de matriz completa** Silencio O(n2 · q) Silencio O(n2) Silencio `n2` puede ser 108 células – imposible. Silencio
Silencio **Track per-cell last writer** ← O(n2) Silencio O(n2) Silencio Mismo problema – demasiadas células. Silencio
Silencio **Análisis anticipada con set** Silencio O(q · n) Silencio Todavía cuadrático en el peor de los casos porque usted recomputa cada fila / columna muchas veces. Silencio
Silencio **Ignorando las consultas duplicadas** Silencio O(q · n) Silencio Todavía demasiado lento; usted está haciendo 5×104 × 104 ♥ 5×108 operaciones – línea fronteriza o más. Silencio

Los entrevistadores a menudo dan la solución de la matriz completa como un ejemplo de lo que *no* hacer.
Incluso una implementación de Python que escribe ingenuamente a la célula matriz por célula TLE en las pruebas más grandes.

-...

### 2.4 Las Variedades Ugly Messy que funcionan pero son difíciles de explicar

1. *Usando `unordered_map` para grabar el último tiempo de escribir** –
*Prueba para cada fila/columna el sello *time* de su última asignación y luego reconstruya la matriz. *
* Aún requiere `O(n2)` para la suma final a menos que haga un truco de matemáticas inteligente.

2. ** Compresión de inicio + BFS** –
*Utilice un bitset para marcar filas / columnas vistas y BFS para propagar valores. *
* Funciona, pero el código se convierte en un laberinto de pequeñas manipulaciones que son difíciles de depurar.

Estas soluciones son técnicamente correctas pero traen **verbosidad** y ** fallos escondidos** (por ejemplo, errores fuera por uno en el multiplicador `(n - colCnt)`).

■ **Bottom line:** Si usted puede terminar la solución de selección inversa en 2 minutos, usted ha superado los “malos” por un amplio margen.

-...

### 2.4 ¿Por qué funciona el truco inverso (Proof by Induction)

Vamos a probar que el escaneo atrasado funciona:

- Caso básico: La última consulta en la lista toca una fila. En la simulación posterior, después de esta asignación todas las celdas `(r, c)` para todos `c` se convierten en 'val'. Dado que ninguna consulta posterior sobrescribe `r`, el valor final de la fila `r` es exactamente 'val'.

- Paso inductivo: Supongamos que para cada fila/columna procesada hasta ahora (desde el final) la suma aportada por *unique* filas/columns es correcta.
Cuando a continuación golpeamos una nueva fila " , cada columna " c " aún no procesada* (es decir, no vista al revés) sigue siendo su valor original " anterior " .
Así, añadiendo `val * (n - colCnt)`. captura exactamente las células frescas que hieren `r` serán propias en la matriz final.

Por inducción, cada fila / columna único contribuye correctamente, y se ignoran los duplicados.

-...

## 2.5 Variaciones Podrías escuchar en una entrevista

Ø Variant tención Estrategia
Silencio...
Silencio **Preguntas que añaden a una fila/columna en lugar de sobreescritura** Silencio Mantener *cumulativas* sumas para filas/columnes, aplicarlas en orden, utilizar prefijo-sums para calcular los valores finales. Silencio
← **Matrimonio de la parrilla (n es enorme pero pocas filas/columnas activas)** Silencio Sólo mantener los diccionarios para filas/columnes que realmente aparecen; la complejidad se reduce a O (preguntas). Silencio
Silencioso **Tamaño de matriz Dinámica** Silencio Uso * mapas de hash* para banderas vistas; todavía tiempo O(q), O(#distinct filas/cols). Silencio

Si usted puede explicar cómo la idea de la composición inversa se adapta a cualquiera de estos, usted será un candidato estrella.

-...

### 2.6 Cómo usar esta solución en una entrevista

1. **Explicar la propiedad “última consulta gana”** – demuestra que no solo estás escribiendo código, estás razonando sobre el problema.
2. **Mostrar la complejidad O(n + q)** – preguntar al entrevistador si eso es aceptable para las limitaciones.
3. **Pasa por la entrada de la muestra** – paso a paso (por ejemplo, `[0,1,5]`, `[1,3,2]`, ...) – para mostrar cómo funciona el multiplicador.
4. ** Casos de borde de fusión** – por ejemplo, consultas duplicadas, todas las filas entonces todas las columnas, matriz de células individuales.
5. **Bonus:** Ofrezca un Python o un snippet Java en el lugar.

■ Los entrevistadores suelen buscar *explicabilidad* más que *velocidad*, así que mantenga la explicación concisa pero completa.

-...

### 2.7 Conclusión – Un viaje para tu próximo trabajo

LeetCode 2718 es un gran problema “algorithm‐plus‐story”.
- **Bueno** – La solución de la composición inversa es un algoritmo O(queries + n) del libro de texto.
- **Bad** – No caigas en la trampa de simulación de matriz ingenua.
- **Ugly** – Hay muchas maneras desordenadas de hackear el problema, pero rara vez son necesarios.

Cuando aterrice en este problema, apunte a la solución limpia y atrasada, mencione sus garantías lineales, y no sólo obtendrá la respuesta correcta, sino que también impresione al gerente de contratación con su capacidad mental de eficiencia.

■ **SEO Palabras clave* *
■ Sum of Matrix After Queries ← LeetCode 2718 Silencio Java solución ← Solución Python Silencio C++ Solución Silencio inversa iteración Silencio O(n) tiempo la complejidad Silencioso entrevista técnica

Feliz codificación, y que sus futuras entrevistas se *llenen con soluciones limpias y eficientes!* 🎯