-...
Título: LeetCode 927. Tres partes iguales -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 3️ 927 – Tres partes iguales
## LeetCode – Hard TEN Java / Python / C++ TENIDO Entrevista

-...

#### TL;DR
Dada una matriz binaria, dividirla en **tres partes contiguas no vacías** cuyos valores binarios son idénticos.
Devolver los índices `[i , j]` tal que

* `arr[0 ... i]` – primera parte
* `arr[i+1 ... j-1]` – segunda parte
* `arr[j ... n-1]` – tercera parte

Si no existe tal división, devuelve `[-1, -1]`.
Los ceros principales están permitidos**.

■ **Todas las soluciones a continuación son tiempo O(n), espacio auxiliar O(1)** y están listos para pegar en su portal LeetCode/Interview.

-...

## 1. Desglose de problemas

← Insight Key Insight
Silencio------------------
Silencio El número total de 1's** debe ser divisible por 3 Silencio Cada parte debe contener el mismo número de 1's Silencio
Silencio Si el array contiene **solo 0's** podemos dividirnos en cualquier lugar ← Todas las tres partes representan el valor 0 Silencio
Silencio Encontrar el índice **primero** de cada parte saltando el primer `k` 1's TEN `k = total_ones / 3` ANTE
Silencio El **suffix** de la matriz define el valor binario que necesitamos para igualar Silencio Una vez que sabemos el comienzo de cada parte, las partes deben parecer idénticas hasta el final ¦

-...

## 2. The O(n) Solution

### Pasos

1. **Count 1's**
* If `total_ones % 3 != 0` → impossible → `[-1,-1]`.
2. ** All-zero case**
* If `total_ones == 0` → devolver `[0, 2]`.
3. **Encontrar posiciones de inicio**
* Escaneo de izquierda a derecha, manteniendo un contador de 1’s visto.
* When counter hits `k`, `2k`, and `3k`, store indices `start1`, `start2`, `start3`.
4. **Alinear las tres partes*
* Mientras los tres índices están dentro de los límites ** y** `arr[start1] == arrr[start2] == arrr[start3]`, avancen los tres simultáneamente.
* Si un desajuste ocurre → imposible.
5. **Verify that the parts are non-overlapping* *
* `start1 + len - 1 Identificar start2` y `start2 + len - 1 Identificar start3 `
* `len = n - start3` – longitud del sufijo.
6. **Retorno de la respuesta**
* `i = start1 + len - 1'
* `j = start2 + len`

### Why It Works

* Cada parte debe tener el mismo valor binario → la secuencia de 1’s y el seguimiento 0’s debe ser idéntico para cada parte.
* Al alinear el **suffix** (`start3` hacia adelante) con las dos partes anteriores garantizamos que el valor es el mismo.
* Debido a que saltamos sobre el número exacto de 1’s, las partes están garantizadas para ser no vacío y no superposición.

-...

## 3. Aplicación del Código

## Java

``java
*
* 3.927 Tres partes iguales – Java
* Tiempo: O(n) tención Espacio: O(1)
*/
Solución de la clase pública {}
int[] threeEqualParts(int[] arr) {
int n = arr.length;
int totalOnes = 0;
(int v : arr) si (v == 1) total Ones++;

// 1. el total debe ser divisible por 3
si (totalOnes % 3 != 0) devolver nuevo int[]{-1, -1};

// 2. todos los casos de ceros
si (totalOnes == 0) devolver nuevo int[]{0, 2};

int PerPart = totalOnes / 3;
int first = -1, second = -1, third = -1;
int seen = 0;
para (int i = 0; i)
si (arr[i] == 1) {
visto++;
si 1) primero = i;
si (ver == los PerPart + 1) segundo = i;
si (ver == 2 *)PerPart + 1) tercero = i;
}
}

// 3. sufijos alineados
int i = first, j = second, k = third;
mientras (k)
si (arr[i] != arrr[j] Silenciosos arr[j] != arr[k]) devuelven nuevo int[]{-1, -1};
i++; j++; k++;
}

int len = n - tercero; // longitud del patrón
int endFirst = first + len - 1;
int start Tercero = segundo + lino;

// 4. garantizar la no superposición (normalmente verdadera si se aprueban los pasos anteriores)
si (endFirst + 1 < startThird) devuelve nuevo int[]{endFirst, start Tercero;
devolver nuevo int[]{-1, -1};
}
}
`` `

-...

## Python

``python
"
3.927 Tres partes iguales – Pitón
Tiempo: O(n) TENIDO Espacio: O(1)
"

Solución de clase:
def threeEqualParts(self, arr: list[int]) - Propiedad list[int]:
n = len(arr)
total = suma (arri)

# 1. total 1's must be divisible by 3
total % 3:
[-1, -1]

# 2. todos los ceros
si total == 0:
[0, 2]

k = total // 3 # 1's per part
primero = segundo = tercero = 1
vistos = 0
para i, v en enumerate(arr):
si v:
visto += 1
si se ve == 1:
primero = i
elif seen == k + 1:
segundo = i
elif seen == 2 * k + 1:
tercero = i

# 3. comparar las tres partes
mientras que tercero
si arr [primer] != arrr[segundo] o arr[segundo] != arr[third]:
[-1, -1]
primero += 1
segundo += 1
tercero += 1

part_len = n - tercera longitud del sufijo
i = primero - part_len # end of first part
j = segundo - part_len # start of third part

[i, j]
`` `

-...

### C++

``cpp
*
* 3.927 Tres partes iguales – C++
* Tiempo: O(n) tención Espacio: O(1)
*/
Clase Solución {
public:
vector tresEqualParts(vector fieltro arr) {
int n = arr.size();
int total = acumulación(arr.begin(), arr.end(), 0);
si (total % 3 != 0) retorno {-1, -1};
(total == 0) devolver {0, 2};

int k = total / 3;
int first = -1, second = -1, third = -1;
int seen = 0;
para (int i = 0; i) {}
si (arr[i] == 1) {
++;
si 1) primero = i;
si (ver == k +1) segundo = i;
si (ver == 2 * k + 1) tercero = i;
}
}

// Alinear las tres partes
int i = first, j = second, kIdx = third;
mientras (kIdx) {
si (arr[i] != arrr[j] Silenciosos arr[j] != arrr[kIdx]) regresa {-1, -1};
++i; ++j; ++kIdx;
}

int partLen = n - third;
int endFirst = first + partLen - 1;
int start Tercero = segundo + parte Len;

si (endFirst + 1 < startThird) regresa {endFirst, startThird};
retorno {-1, -1};
}
};
`` `

-...

## 4. Artículo del Blog – “El Bien, el Mal, y el Ugly de LeetCode 927”

■ *Título*
■ *Tres partes iguales – El bien, el mal y el ugly (Java, Python, C++)*

■ **Descripción de los datos* *
■ Maestro LeetCode 927 en minutos. Lea la solución completa, entienda las trampas, y consiga una respuesta de entrevista lista para el trabajo. Incluye código Java, Python, C++.

■ **Keywords**
■ `Three Equal Parts Leetcode`, `Java solution`, `Python solution`, `C++ solution`, `binary array split`, `job interview coding`, `binary number comparison`, `O(n) algoritmo`, `array partición `

-...

#### ## 1down⃣ El Bien: ¿Por qué este problema se mete?

* ** Vibe del mundo real** – Piensa en paquetes de datos que deben dividirse en segmentos iguales.
* **Pure desafío algoritmo** – No hay matemáticas pesadas, sólo manipulación inteligente puntero.
* ** Prueba de entrevista perfecta* Muestra tu comprensión de *array traversal*, *casos de forja*, y *time‐space trade‐offs*.

#### 2down⃣ El malo: Pitfalls comunes

Por qué rompe la vida
Silencio...
El valor binario de `[0,1,1]` es el mismo que `[1,1]`. Silencio
Silencio *Asumiendo cualquier obra dividida cuando todos los ceros* Silencio Todavía debes regresar `[0,2]` – la respuesta más simple válida. Silencio
*Using a hash map of prefixes* Silencio O(n) space for a problem that can be done in O(1). Silencio
*Verificar sólo el número de 1’s* Silencio Dos arrays pueden tener el mismo patrón de 1 cuenta pero diferente. Silencio

#### 3down⃣ Casos de borde oculto

1. **Todos los ceros** – Su algoritmo todavía debe devolver una división válida.
2. **Trailing ceros after the last part** – Deben contarse en la alineación del sufijo.
3. **Very short arrays** – E.g., `[1,0,1]` → imposible.
4. **Introducciones altas** – `arr.length == 30000` – asegúrese de hacer *not* crear arrays adicionales o utilizar la recursión.

-...

## 5. SEO‐Optimized Quick‐ Comience la hoja de Cheat

Silencio Idioma Silencio Código de inicio rápido
Silencio...
Silencio **Java** Silencioso ``java\npublic int[] threeEqualParts(int[] arr) { /* code */ }\n``` Silencio
*Python* Solución:\n def threeEqualParts(self, arr: List[int]) - título List[int]:\n # code\n``` Silencio
Silencio **C++** Silencio ``cpp\nclass Solution {\npublic:\n vector asignadoint 3EqualParts(vector fieltro arr) {\n // code\n }\n}\n``` Silencio

**Consejo: ** Cuando usted pega en LeetCode, sólo reemplazar el esqueleto con el código anterior y ejecutar.

-...

## 6. Pensamientos de clausura

* **Practice** – Ejecute el código con arrays aleatorios para ver casos de borde en acción.
* **Explicar** – En entrevistas, caminar a través de *los totales*, *indices de arranque*, *alineación de suffix*, *no superposición*.
* **Portfolio** – Añadir esta solución a tu GitHub repo, etiqueta con `#LeetCode927`. Amo del programa ver código limpio, bien comunicado.

■ *Ready to land that next coding interview?* 🚀
■ ¡Suelta la solución en tu IDE, pruébala y explícale la lógica, estás listo!

-...

*Feliz codificación y buena suerte! *

-...

■ *Author** – Entrevista de Coding Ninja
■ **Siguiente** para más información de LeetCode: LinkedIn, Twitter, Medium
■ **Suscribir** a nuestro boletín: plan de preparación de entrevistas de 30 días.

-...

### End of Article

-...

Con este artículo, los lectores no sólo aprenden el algoritmo, sino que también entienden *por qué* es digno de entrevista, lo que aumenta la confianza y el rendimiento de entrevista — clave para aterrizar ese papel de ingeniería de software de sueño.