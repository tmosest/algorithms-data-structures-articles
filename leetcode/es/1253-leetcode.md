-...
Título: LeetCode 1253. Reconstruir una matriz binaria de 2 puntos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Reposición de problemas
**Reconstruir una matriz binaria de 2 puntos**

Dado

* `upper` – la suma requerida de la primera (0‐th) fila
* " menor " - la suma requerida de la segunda (1a) fila
* `colsum[]` – un array de longitud *n* donde
* `colsum[i]` can be `0`, `1` or `2`
* representa el número total de `1`s que debe aparecer en la columna *i* de la matriz final de 2-row

Devuelve cualquier matriz binaria de 2 acres 'mat' que satisface todo lo anterior, o una matriz vacía si es imposible.



----------------------------------------------------

## 2. Intuición " Greedy Idea

* **`colsum[i] == 2`**
Ambas filas deben contener un `1`. Esto consume una `1` de `upper` Y uno de "más bajo".

* **`colsum[i] == 0`**
Ambas filas contienen un `0`. No se utiliza cuota.

* **`colsum[i] == 1`**
Una de las dos filas debe contener un `1`. Cualquier fila que todavía tiene cuota restante es elegida con avidez – no importa qué fila recibe el `1` mientras se respetan las cuotas totales.

La elección avaricia es segura porque las únicas columnas que **force** una colocación son las que tienen `2`.
Después de que todas esas columnas estén fijadas, los restantes `1`` columnas son " libres " , cualquier asignación que utilice exactamente los recuentos " más bajos " restantes es válida.

----------------------------------------------------

## 3. Algoritm

`` `
1. Let m = colsum.length
2. Si suma (comentario) != superior + inferior → imposible → retorno []

3. Cuenta el número de 2 en colsum, que sean dos
Si doss Ø superior o doss inferior → imposible → retorno []

4. Crear la matriz resultado res[2][m] inicializada con 0

5. Primer paso: para cada yo con colsum [i] == 2
res[0][i] = res[1] [i] = 1
arriba...

6. Segundo paso: por cada yo con colsum [i] == 1
si superior 0:
[0][i] = 1 ; superior...
más:
res[1][i] = 1 ; inferior...

7. Retorno
`` `

----------------------------------------------------

## 4. Prueba de corrección

Demostramos que el algoritmo devuelve una matriz válida si existe, y devuelve `[]` de otro modo.

-...

### Lemma 1
Si `sum(colsum) != superior + inferior`, no existe matriz válida.

Proof.
El número total de `1's en la matriz es igual
`sum(colsum)` (por definición de las sumas de la columna) y también es igual
" superior + inferior " (por definición de sumas de fila).
Si difieren, las dos igualdades no pueden mantener simultáneamente. ∎



### Lemma 2
Si el número de `2`-columns (`twos`) excede ya sea `upper ' o `lower ' , no existe matriz válida.

Proof.
Cada uno de los dos `2 `` columna requiere un `1` en * ambas filas.
Así cada columna consume una unidad de la cuota de *ambos* filas.
Si `dos' es más grande que la cuota de una fila, esa fila necesitaría más que 'upper' (o `más bajo') Es imposible. ∎



### Lemma 3
Después del primer paso, los valores restantes de " superior " y " inferior " equivalen al número exacto de " 1 " que aún deben colocarse en las filas correspondientes.

Proof.
Cada uno de los dos `2` columnas se ha llenado de dos `1`s, uno por fila, y `upper ' y `bajo ' fueron decrementados en consecuencia.
Todavía no se han colocado otros `1`s, por lo que los nuevos valores representan la cuota restante. ∎



### Lemma 4
El segundo paso coloca exactamente los restantes `1`''-columns de una manera que satisface las cuotas restantes.

Proof.
Cada uno de ellos necesita un solo `1`.
El algoritmo lo coloca en la fila superior mientras que `upper ю 0`.
Si 'upper' ya está agotado, debe colocarse en la fila inferior, y por Lemma 3 `más bajo нели 0` sostiene en ese momento.
Así, cada uno de los `1`' de columna se asigna a una fila que todavía tiene cuota disponible, y después del pase tanto 'upper' como `lower' se convierte en `0`. ∎



### Theorem
El algoritmo devuelve una matriz que satisface todas las restricciones si existe tal matriz.

Proof.

*Si el algoritmo devuelve una matriz*:
Por Lemma 1 y 2 nunca devuelve una matriz cuando las limitaciones son insaciables.
Cuando proceda, Lemmas 3 y 4 garantizan que después de los dos pases se respete cada suma de la columna y ambas sumas de la fila igualan el original 'upper' y `lower`.
Por lo tanto la matriz es válida.

*Si existe una matriz válida*:
Todas las condiciones necesarias de Lemmas 1 y 2 deben mantener, de lo contrario no puede existir matriz.
Así el algoritmo nunca rechaza una instancia factible temprano.
Con las condiciones satisfechas, la asignación codictiva en el segundo paso es siempre posible (Lema 4), por lo que el algoritmo produce una matriz. ∎



----------------------------------------------------

## 5. Análisis de la complejidad

*Let `n = colsum.length`.*

* Tiempo:
* Sum " count: `O(n)`
* Dos pases sobre la matriz: `O(n)`
* **Total** `O(n)`.

* Espacio:
* Matriz de resultados `2 × n`: `O(n)`.
* Variables auxiliares: `O(1)`.

----------------------------------------------------

## 6. Aplicación de las referencias

A continuación se presentan implementaciones limpias y idiomáticas en **Java**, **Python**, y **C+**.

-...

### 6.1 Java (Java 17)

``java
importar java.util*;

Solución de la clase pública {}
public List made(int, int lower, int[] colsum) {
int n = colsum.length;
total = 0;
int twos = 0;
para (int v : colsum) {
total += v;
si (v == 2) dos++;
}
si (total != superior + inferior ← anterior doss ⇩ superior tención duradera doss
devolver nuevo ArrayList recomendado(); // matriz vacía
}

int[][] res = nuevo int[2][n];

// Primer paso – columnas con 2
para (int i = 0; i)
si (colsum[i] == 2) {
[0][i] = 1;
res[1][i] = 1;
arriba...
inferior...
}
}

// Segundo paso – columnas con 1
para (int i = 0; i)
si (colsum[i] == 1) {
si 0) {
[0][i] = 1;
arriba...
. ♫ ... {
res[1][i] = 1;
inferior...
}
}
}

Lista realizadaLista realizadaInteger confianza respuesta = nuevo ArrayList recomendado();
respuesta.add(toList(res[0]));
respuesta.add(toList(res[1]));
respuesta de retorno;
}

privada Lista de datos: Integer confianza toList(int[] arr) {
Lista de títulos = nuevo ArrayList implicado(arr.length);
para (int v : arrr) list.add(v);
lista de retorno;
}
}
`` `

-...

### 6.2 Python 3

``python
de la importación Lista

Solución de clase:
def reconstruct Matriz(self, upper: int, lower: int,
colsum: List[int]) - título List[List[int]]:

n = len(colsum)
total = suma (continuación)
dos = colsum.count(2)

si total != superior + inferior o doss superior o doss inferior:
retorno []

# inicializar la matriz de 2 acres con ceros
res = [[0] * n for _ in range(2)]

# primer paso - columnas con 2
for i, v in enumerate(colsum):
si v == 2:
[0][i] = 1
[i] = 1
superior -= 1
inferior a 1

# segundo paso - columnas con 1
for i, v in enumerate(colsum):
si v == 1:
si superior 0:
[0][i] = 1
superior -= 1
más:
[i] = 1
inferior a 1

retorno
`` `

-...

### 6.3 C+17

``cpp
Incluido el título
usando std namespace;

Clase Solución {
public:
vector se llevó a cabo mediante vectores, int inferior, vector denominadoint inferior, vectorial reducido {}
int n = colsum.size();
total = 0, 2 = 0;
para (int v : colsum) {
total += v;
si (v == 2) ++dos;
}
si (total != superior + inferior tención sometida doss √≥n superior Silencioso doss √≥ inferior)
retorno {}; // matriz vacía

vector seleccionado(n, 0));

// columnas que deben contener dos 1's
para (int i = 0; i)
si (colsum[i] == 2) {
res[0][i] = res[1] = 1;
--upper; --lower;
}

// columnas que contienen exactamente 1
para (int i = 0; i)
si (colsum[i] == 1) {
si 0) {
[0][i] = 1;
-upper;
. ♫ ... {
res[1][i] = 1;
- más bajo;
}
}

restitución;
}
};
`` `

----------------------------------------------------

## 7. SEO‐Optimised Blog Post – “How to Nail a Data‐Structures Interview *and* Land Your Next Tech Job”

■ **Keywords** – *reconstruir una matriz binaria de 2 acres*, *LeetCode 1739*, * algoritmo de entrevista de trabajo*, * algoritmo importante*, *entrevista de codificación Java Python C++*, *extremidades de entrevista de ingenieros de software*, *disposiciones de datos entrevista preguntas*, *pensamiento algoritmico*, *evoces de contratación*

-...

## 7.1 Title & Meta‐Description

← Elemento Silencioso
Silencio...
Silencio **Título** Silencioso Reconstruir una matriz binaria de 2-Row – LeetCode 1739 (Java, Pitón, C++) Silencio
Silencio **Meta‐Descripción** ← Maestro el problema LeetCode “Reconstruir una matriz binaria de 2-Row” Paso a paso algoritmo codicioso, prueba, complejidad y soluciones Java, Python, C++. Perfecto para el prep de entrevista de software-motor. Silencio

-...

### 7.2 Introduction

■ *Preguntas sobre la estructura y el algoritmo son la piedra angular de cada entrevista de ingeniería de software. Uno de los patrones más solicitados implica reconstruir una matriz de las sumas de fila y columna – un problema engañosamente simple pero sorprendentemente complicado. En este artículo, caminamos a través de la “Reconstruir una matriz binaria de 2 acres” LeetCode desafío (ID 1739) y proporcionar soluciones de producción en Java, Python y C+++. *

-...

### 7.3 Por qué este problema importa en las entrevistas

1. **Demuestra comprensión de la contabilidad básica** – Debe realizar un seguimiento de las sumas de fila y columna simultáneamente.
2. **Highlights Greedy Decision‐Making** – Elegir dónde colocar un `1` en columnas “libres” es una trampa codictiva clásica; resolver correctamente muestra la madurez algorítmica.
3. **Mostrar Edge‐Case Rigor** – El rechazo temprano de los insumos imposibles prueba su capacidad para detectar las condiciones necesarias antes de hacer un trabajo pesado.
4. **Scales Across Languages** – Una solución sólida en tres idiomas populares demuestra el pensamiento agnóstico del lenguaje – un activo valioso para posiciones de personal completo o sistemas.

-...

## 7.4 Step‐by‐Step Algorithm (in Plain English)

1. **Validar la viabilidad* *
* Total number of `1`s must equal the sum of the two row quotas.
* Cada columna con `2` fuerza una colocación; su cuenta no puede exceder ninguna cuota.

2. **Fill Forced Columns** ( " Colsum[i] == 2 " ) – ambas filas consiguen `1 ' y reducimos ambas cuotas.

3. **Allocate “Free” Columnas** (“colsum[i] == 1`) – codicioso poner el `1` en la fila que todavía necesita uno. Después de esto, ambas cuotas alcanzan cero.

4. **Retorna la matriz** o una lista vacía si algún cheque falla.

-...

### 7.5 Code Overview

Silencio Idioma Silencio Key Implementation Details
Silencio--------------------------
Silencio **Java** Silencio Usos `List observadoList madeInteger inteligente` para que coincida con el tipo de retorno de LeetCode; helper `toList()` para legibilidad. Silencio
Silencio **Python** tención Lista-comprensiones para la creación de matriz concisa; retorno temprano sobre la imposibilidad. Silencio
tención **C++** TENIDO 2-dimensional `vector armonizado: > salida temprana con `{}`. Silencio

-...

### 7.6 Complexity & Performance

* **Tiempo** – `O(n)` donde *n* es el número de columnas.
* **Espacio** – `O(n)` para la matriz resultante.

Estos límites ajustados son óptimos; ningún algoritmo puede ser asintoticamente mejor porque debemos inspeccionar cada columna al menos una vez.

-...

## 7.7 Edge‐ Lista de verificación de casos

Escenario esperada Resultado
Silencio...
Silencioso `sum(colsum) != superior + inferior`
demasiados `2 ' columns  durable `[]
Silencio Todas las columnas son `0` matriz de vida de todos los ceros
Silencio Todas las columnas son `2` y `upper == inferior == n/2` matriz de vida con todos los que están bajo

-...

### 7.8 Final Takeaway

*El algoritmo codicioso anterior es ** probablemente correcto** y funciona en tiempo lineal.
Implementarlo en varios idiomas demuestra tanto el pensamiento algorítmico como la artesanía específica del lenguaje – exactamente el tipo de habilidades que buscan los reclutadores. *

-...

## 8. Cómo este Blog pone en marcha su carrera técnica

Cómo el artículo ayuda a vivir
Silencio...
Silencio **Keyword Visibilidad** Silencio Palabras clave como “Reconstruir una matriz binaria de 2-Row”, “Solución de LeetCode 1739”, “Entrevista de Java Python C++” aparecen naturalmente a lo largo del post, lo que hace que sea descubierta cuando los reclutadores o los gerentes de contratación buscan problemas comunes de entrevista. Silencio
Silencio **Exámenes Problema–Solving Skills** ← El artículo camina a través de la manipulación de pruebas, complejidades y periferias —signales a los reclutadores que usted puede razonar rigurosamente sobre algoritmos. Silencio
Silencio **Demonstrates Multilingual Expertise** Silencio Al proporcionar soluciones claras y idiomáticas en tres idiomas principales, ilustra la capacidad de adaptarse a la pila tecnológica de una empresa. Silencio
Silencio **Añadir valor a su Portafolio** Silencio Usted puede incrustar los fragmentos de código en su GitHub README o sitio web personal, y la explicación sirve como una referencia rápida para futuras entrevistas. Silencio
Silencio **Engages Programador con Contenido Estructurado** Silencio El uso de tablas, listas de balas y bloques de código coincide con los reclutadores de formato apreciar al esquiar los blogs candidatos o perfiles técnicos. Silencio

**Acción:**
*Pon este artículo en Medium, Dev.to, o tu blog personal. *
*Añadir un enlace a su repositorio GitHub que contiene los archivos de solución completa. *
*Use como punto de conversación en las próximas entrevistas—explicar la intuición, caminar a través de la prueba, y mostrar las implementaciones limpias. *

¡Feliz codificación y feliz entrevista! 🚀