-...
Título: LeetCode 1906. Preguntas mínimas de diferencia absoluta -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1906. Preguntas mínimas de diferencia absoluta
## From “good” to “ugly” – a full-stack guide for the interview‐ready coder

-...

## TL;DR
- **Problema** - Para cada consulta `[l, r]` devolver la menor diferencia absoluta entre cualquier número * diferente* en el sub-array `nums[l...r]`. Si todos los números son idénticos, devuelve `-1`.
*Key Insight* – `nums[i]` está obligado por **1...100**. Este pequeño dominio nos permite construir una tabla de cuenta **prefijo** del tamaño `n × 100`.
- ** Complejidad** – `O(n + q) · 100) ' tiempo, `O(n · 100)' espacio. Funciona cómodamente para `n ≤ 1e5`, `q ≤ 2·104`.
- **Por qué importa** – Demostrar el dominio de **Sumas prefijo**, ** consultas de oficina**, y **contando rango**—todos deben conocer temas para entrevistas de instrucciones de datos.

-...

## 1. Recaptación de problemas

■ Dados `nums ' (size `n ') y `queries ' (`q ' pares `[l, r] ' ), para cada consulta encontrar
" `
[i] – nums[j] con l ≤ i ■ j ≤ r y nums[i] ل nums[j]
" `
■ Regresar `-1' si cada elemento en `[l, r]` es igual.

`n` puede ser hasta `105`, `q` hasta `2·104`.
`nums[i]` vive en `[1, 100]`.

-...

## 2. Enfoques ingenuos

Silencio Silencio Silencio Silencio Silencio Silencio
Silencio------------------------
Silencio Brute‐force double loop per query Silencio `O(q · (r-l+1)2)` Silencio `O(1)` Silencio Too slow – worst case ~ `1014`. Silencio
Silencio Ordenar el sub-array por query, luego escanear vecinos Silencio `O(q · (r-l+1) log (r-l+1))` Silencio `O(r-l+1)` Todavía demasiado lento. Silencio
Silencio Use un BST equilibrado o un multiset por consulta Silencio `O(q · (r-l+1) log (r-l+1))` Silencio `O(r-l+1)` La complejidad innecesaria. Silencio
Silencio **Conteo de prefijo + escaneo 1‐100** Silencio `O(n+q)·100)` Silencio `O(n·100)` Silencio **Fast enough** for constraints. Silencio

Debido a que el dominio *valor* es pequeño, podemos evitar clasificar o BSTs enteramente.

-...

## 3. La solución óptima – tabla de cuenta de prefijo

### 3.1 Core Idea

- Construir un array 2-D `pref[i][v]` = número de ocurrencias de valor `v` (índice 0-basado, `v  velocidad [0,99]`) en el prefijo `nums[0...i-1]`.
- Para una consulta `[l, r]` el recuento de valor `v` en el rango es
``text
count_v = pref[r+1][v] - pref[l][v]
`` `
- Camina por toda la `v` de `0` a `99` y recoge los valores que aparecen al menos una vez en el rango.
- Dado que la lista ya está clasificada por `v`, la diferencia absoluta mínima es simplemente la brecha mínima entre los valores actuales consecutivos.
- Si sólo un valor está presente → respuesta `-1`.

#### 3.2 Why This Works

**Contento de intervalos de tiempo constante**: La tabla de prefijo da `O(1)` por valor.
- **El número máximo de valores**: Siempre hacemos más de 100 números, independientes de " n " o " .
- No se necesita ninguna clasificación. Los valores se procesan en orden ascendente.

#### 3.3 Complexity

- **Tiempo**: `O(n·100 + q·100)` = `O(n+q)·100)` → about 1.2 × 107 operations for the worst case.
- **Espacio**: "O(n·100)" enteros (~ 40 MB) – aceptables en entornos de entrevista típica.

-...

## 4. Aspectos destacados de la aplicación

#### 4.1 Java

``java
Clase Solución {
int[] minDifference(int[] nums, int[][ ] {
int n = nums.length;
int[][] pref = nuevo int[n + 1][100]; // prefijo cuenta

// construir prefijo
para (int i = 0; i)
System.arraycopy(pref[i], 0, pref[i + 1], 0, 100);
pref[i + 1][nums[i] - 1]+; // cambio a 0-basado
}

int q = consultas. longitud;
int[] ans = nuevo int[q];

para (int qi = 0; qi) {}
int l = consultas[qi][0];
int r = consultas[qi][1] + 1; // exclusiva

int prev = -1, minDiff = Integer.MAX_VALUE, distinct = 0;

para (int v = 0; v)
int cnt = pref[r][v] - pref[l][v];
si (cnt √≥ 0) {
diferenciada++;
si (prev != -1) {
minDiff = Math.min(minDiff, v - prev);
}
prev = v;
}
}

ans[qi] = (distinct י= 1) ? -1 : minDiff;
}
devolver los ans;
}
}
`` `

#### 4.2 Python

``python
de la importación Lista

Solución de clase:
def minDifference(self, nums: List[int], consultas: List[List[int]) - No. List[int]:
n = len(nums)
pref = [0] * 100 for _ in range(n +1)]

para i, val in enumerate(nums, 1):
pref[i] = pref[i - 1][:] # copy previous row
pref[i][val - 1] += 1

res = []
para l, r en consultas:
r += 1
Prev = Ninguno
diferenciada = 0
min_diff = 101
para v en rango(100):
si pref[r][v] - pref[l][v]:
diferenciado += 1
si el prev no es Ninguno:
min_diff = min(min_diff, v - prev)
prev = v
re.append(-1 si se distingue <= 1 min_diff)
retorno
`` `

#### 4.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector implicado menosDifference(vector interpretadoint estrecho contacto nums, vector seleccionadovector fieltro implica consultas) {}
int n = nums.size();
vector realizador realizado, 100 títulos pref(n + 1);
para (int i = 1; i) = n; ++i) {}
pref[i] = pref[i - 1]; // copy
pref[i][nums[i - 1] - 1]++; // cambio a 0
}

vector significar uns
ans.reserve(queries.size());

para (auto &q : consultas) {}
int l = q[0], r = q[1] + 1; // make r exclusive
int prev = -1, minDiff = 101, distinct = 0;

(int v = 0; v) 100; + v) {}
si (pref[r][v] - pref[l][v]) {
++distinto;
si (prev != -1) minDiff = min(minDiff, v - prev);
prev = v;
}
}
ans.push_back(distinct י= 1 ? -1 : minDiff);
}
devolver los ans;
}
};
`` `

-...

## 5. Casos de borde " Pitfalls

Silencio Pitfall Silencio Por qué duele Silencio
Silencio--------------------------
Silencio Olvídate de hacer `r` exclusiva al usar sumas prefix ← Off‐por-one error → conteos incorrectos tención Use `r + 1` al indexar el array prefijo. Silencio
TENIDO Utilizar `int[][]` en Java sin copiar filas TENER `System.arraycopy` es necesario para evitar referencias compartidas ANTE Copiar cada fila o utilizar 'Arrays.copy Of`. Silencio
Silencio Asumiendo que el dominio puede cambiar TEN si `nums[i]` √ 100, el algoritmo rompe TENCIÓN Para mayores rangos, utilice 'TreeSet`/segment tree or compresss values. Silencio
Silencio No manejar el caso `-1` ANTE Vuelta `0` cuando todos los elementos son iguales Silencio Número de pista de valores distintos y volver `-1` si ≤ 1. Silencio
TENIDO Utilizando `int[][]` para prefijo en Python ANTE Las listas de listas son mutables; copia por fila necesaria ANTE Use `pref[i] = pref[i-1][:` dentro del bucle. Silencio

-...

## 6. Variaciones del problema

← Variante Silencio Sugerida Solución Silencio
Silencio...
Silencio ** Unbounded `nums[i]** (e.g., `1...106`) Silencio Compresa los valores, luego construye una tabla de prefijo 2-D o utiliza un **BIT / Fenwick** en los índices comprimidos. Silencio
Silencio **Large query count** (`q ♥ 1e6`) ← La '100`''' aún funciona, pero podrías llegar a los límites de memoria Silencio Usar un **bitset** (`std::bitset Utilizado101 ``) por prefijo para cortar espacio. Silencio
Silencio **Solicitar consultas en línea** Silencio Necesitar una estructura de datos que apoye la inserción/borto en la mosca Silencio BST equilibrado (`TreeMap`) por prefijo, o mantener un multiset para la ventana deslizante. Silencio
Silencio ** Actualizaciones Dinámicas a `nums`** ¦ La tabla Prefix se vuelve estancada Silencio Recompilado después de cada actualización, o utilizar un ** árbol de segmento** que soporta actualizaciones de puntos. Silencio

-...

## 6. Por qué esta solución parece “buena” en entrevistas

1. **Shows Problem‐Solving Skills** – Usted vio el límite en `nums[i]` y lo apalancó.
2. **Usuarios Classic Data‐Structures** – Las sumas de prefijo son una grapa; los convertiste en una tabla de conteo de rango 2-D.
3. **Dispone de grandes entradas con gracia** – El tiempo y la memoria permanecen lineales en `n` y `q`.
4. ** Lectura en idioma cuadrado** – Suministramos código limpio y idiomático en Java, Python y C++.
5. **Extensible** – El mismo patrón (prefijo tabla + escaneo de dominio fijo) funciona para muchos problemas de estilo “range‐min‐diff”.

-...

## 6. Lista de verificación para entrevistadores

- [ ] Construya correctamente una tabla de 'pref' (copia filas, valores de cambio).
- [ ] Convertir query `[l, r]` a `[l, r+1)` antes de subcontratar prefijos.
Escáner `v` de `0` a `99` - ninguna clasificación adicional necesaria.
- [ ] Regresar `-1` cuando `distinct <= 1`.
Verificar con casos de esquina:
- Consultas de elementos individuales.
- Todos valores iguales.
- Consulta completa.

-...

## 6. Pensamientos de clausura

El rango de valor **tiny** transforma un problema de búsqueda de rango aparentemente pesado en un algoritmo simple y lineal.
Dominar este patrón demuestra:

- ** Uso creativo de las restricciones** – convertir un problema que parece que necesita un árbol de segmento en un problema de conteo de `O(1)`.
- **Procesamiento sin conexión eficiente** – construir estructuras de datos una vez y volver a utilizarlas para muchas consultas.
- **Clear, código mantenible** - sin necesidad de hacks oscuros, sólo una mesa de prefijo limpio y un solo paso sobre 100 valores.

■ *Si puedes explicar esta solución en una entrevista y escribir el código Java/Python/C++ en el lugar, pasarás la pregunta de estructura de datos “hard” con colores voladores. *

-...

## SEO & Social Tags

- **Descripción de los datos**: “Solve LeetCode 1906 – Mínima Diferencia Absoluta Consultas en O(n+q)·100). Tabla de cuenta de prefijo, soluciones Java/Python/C++, consejos de entrevista, casos de borde. ”
- **Keywords**: `minimum absolute difference queries`, `prefix sums`, `range counting`, `LeetCode 1906`, `data structure interview`, `segment tree`, `Mo's algoritmo`, `C++ solution`, " Solución java " , " Solución pitón " , " consultas oficiosas " .

¡Feliz codificación y buena suerte en tu próxima entrevista!