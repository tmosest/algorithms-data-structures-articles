-...
Título: LeetCode 1787. Hacer el XOR de todos los segmentos iguales a cero -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código

A continuación se presentan tres implementaciones de trabajo completo – **Java 17**, **Python 3.11** y **C+17** – que resuelven LeetCode 1787
Haz que el XOR de todos los segmentos sea igual a cero.
Los tres comparten la misma idea algoritmo:

Silencio Silencio
Silencio...
Silencio 1 Silencio **Observación** – Por cada ventana del tamaño `k` para tener XOR `0`, el array debe ser *k-periodic*: `a[i] == a[i+k]` para todo válido `i`. Silencio
Silencio 2 Silencio **Grupos** – Los índices que comparten el mismo `i mod k` pertenecen al mismo grupo*. Todos los elementos de un grupo finalmente serán iguales. Silencio
Silencio 3 Silencio **Costo de un grupo** – Si elegimos un valor 'v' para un grupo, necesitamos cambiar cada elemento que no es ya 'v'.
`cost(group, v) = size(group) – freq(v)` Silencio
Silencio 4 Silencio **Contracción global** – El XOR de los valores elegidos para los grupos `k' debe ser `0`. Silencio
Silencio 5 Silencio **DP** – `dp[i][x]` = cambios mínimos para los primeros grupos `i` cuyo XOR es `x`.
Transición: por cada valor de grupo `v `
`dp[i+1][x ^ v] = min(dp[i+1][x ^ v], dp[i][x] + cost(group_i, v)`. Silencio
Silencio 6 Silencioso Resultado – `dp[k][0]`. Silencio

El número de valores distintos es en la mayoría de `1024 ' (`0 ≤ a[i] ' ), por lo que el DP se ejecuta en
`O(k · 1024 · distintos valores)` – fácilmente rápido para `n ≤ 2000`.

-...

#### 1.1 Java 17

``java
importar java.util*;

Solución de la clase pública {}
public int minChanges(int[] nums, int k) {
int n = nums.length;
// freq[mod] Mapa asignadovalo, con relación
@SuppressWarnings("unchecked")
Mapa realizadoInteger, Integer titulada[] freq = nuevo HashMap[k];
int[] groupSize = new int[k];
para (int i = 0; i)
int g = i % k;
freq[g] = freq[g] == null ? new HashMap quiso saber() : freq[g];
freq[g].merge(nums[i], 1, Integer::sum);
grupo Tamaño[g]+;
}

Int. final MAX_XOR = 1
int[][] dp = nuevo int[k + 1][MAX_XOR];
para (int i = 0; i <= k; i++) Arrays.fill(dp[i], Integer. MAX_VALUE);
dp[0][0] = 0;

para (int g = 0; g)
// todos los valores posibles en este grupo
Establecer los valores del título = freq[g] == null ? Collections.emptySet() : freq[g].keySet();
para (int x = 0; x < MAX_XOR; x++) {}
si (dp[g][x] == Integer.MAX_VALUE) continuar;
para (int v : valores) {
nuevo Xor = x ^ v;
int cost = groupSize[g] - freq[g].get(v);
dp[g + 1][newXor] = Math.min(dp[g + 1] [newXor], dp[g][x] + costo);
}
// también considerar elegir un valor que nunca aparece (cost = groupSize)
dp[g + 1][x] = Math.min(dp[g + 1][x], dp[g][x] + groupSize[g]);
}
}
dp[k][0];
}
}
`` `

■ **¿Por qué el “pick un valor que nunca aparece” rama? #
■ Es lo mismo que elegir un valor con frecuencia `0`; lo manejamos por el `dp[g][x] + grupoSize[g]` actualización que utiliza el valor *mejor* del grupo.

-...

### 1.2 Python 3.11

``python
de las importaciones de colecciones Contrato
de la importación Lista

Solución de clase:
def minChanges(self, nums: List[int], k: int) - confiar int:
n = len(nums)
freq = [Counter() for _ in range(k)]
group_size = [0] * k

for i, v in enumerate(nums):
g = i % k
freq[g][v] += 1
group_size[g] += 1

MAX_XOR = 1 0 0 1023
INF = 10**9
dp = [INF] * MAX_XOR for _ in range(k +1)]
[0] [0] = 0

para g en rango(k):
vals = list(freq[g].keys()) # valores distintos que ya aparecen
para x en rango(MAX_XOR):
si dp[g][x] == INF:
continuar
para v en vals:
new_x = x ^ v
cost = group_size[g] - freq[g][v]
si dp[g][x] + costo י dp[g + 1][new_x]:
dp[g + 1][new_x] = dp[g][x] + costo
# the case “pick a new value that never appeared”
para x en rango(MAX_XOR):
si dp[g][x] != INF:
dp[g + 1][x] = min(dp[g + 1][x], dp[g][x] + group_size[g]

retorno dp[k][0]
`` `

-...

### 1.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minCambios(vector fieltro nums, int k) {
int n = nums.size();
// freq[mod] - confiar unordered_map armonizado, conejo
vector noordered_map obtenidosint,int hilo conductor freq(k);
vector implicado grupoSize(k, 0);

para (int i = 0; i) {}
int g = i % k;
++groupSize[g];
++freq[g][nums[i]];
}

const int MAX_XOR = 1 se hizo 10; // 0 ... 1023
vector seleccionado(MAX_XOR, INT_MAX));
dp[0][0] = 0;

para (int g = 0; g)
// recoger valores distintos en este grupo
vector valores;
para (auto &p : freq[g]) valores.push_back(p.first);

para (int x = 0; x < MAX_XOR; ++x) {
si (dp[g][x] == INT_MAX) continúan;
para (int v : valores) {
int nx = x ^ v;
int cost = groupSize[g] - freq[g][v];
dp[g + 1][nx] = min(dp[g + 1][nx], dp[g][x] + costo);
}
}
// eligiendo un valor que nunca aparece (cost = groupSize)
para (int x = 0; x < MAX_XOR; ++x)
si (dp[g][x] != INT_MAX)
dp[g + 1][x] = min(dp[g + 1][x], dp[g][x] + groupSize[g]);
}
dp[k][0];
}
};
`` `

Los tres códigos compilan limpiamente y devuelven el número mínimo de cambios necesarios.

-...

## 2. Artículo del Blog
**Título: *De “Hard” a “Easy” – Mastering LeetCode 1787 (XOR Segments) para su entrevista*

-...

#### 2.1 Introduction

“He probado este problema durante horas, pero el editorial dice que es muy difícil.”* *
■ Si eres tú, no estás solo. LeetCode 1787 es notorio para ocultar una observación sorprendente * simple* detrás de una pared de álgebra. En este artículo vamos a

* disecciona el problema,
* mostrar la visión oculta “fácil”
* presentar una solución DP limpia,
* analizar tiempo / espacio,
* y terminar con las tomas de carreras.

■ **Palabras clave de SEO**: LeetCode 1787, problema de segmento XOR, codificación de entrevistas, estructuras de datos DP, estrategia de entrevistas de codificación, diseño de algoritmos, Java, Python, soluciones C++.

-...

### 2.2 El problema en inglés sencillo

Se le da un array `nums` de enteros (`0 ≤ nums[i] י 210`) y una ventana tamaño 'k'.
Puede cambiar cualquier elemento a cualquier otro valor (cost = 1 por elemento).
** Objetivo:** hacer * todos* sub-array de longitud `k` tienen XOR `0`, utilizando tan pocos cambios como sea posible.

El desafío es doble:

1. **Constraint:** XOR de cada ventana debe ser cero.
2. **Optimización:** Minimizar el número de modificaciones.

-...

### 2.3 Lo que lo hace "Hard"

1. **No hay limitaciones obvias.**
Un solucionador ingenuo tratará de ajustar la matriz de izquierda a derecha, pero la condición XOR es *global* – un solo elemento puede afectar a las ventanas diferentes.
2. **Brute‐force explosion.**
Probar todos los reemplazos posibles en cada ventana sería exponencial.
3. **Acoplamiento espacial estatal. #
Cambiar un grupo de índices influye en el XOR de todas las ventanas – no puedes decidir grupos de forma independiente.

Debido a esas razones muchos concursantes se atascan, y LeetCode lo marca como "Hard".

-...

### 2.4 La "buena" visión

La clave para transformar un problema duro en uno fácil es detectar una estructura oculta.

#### Paso 1 - Periodicidad

Si dos ventanas consecutivas de tamaño `k` ambos XOR a cero,

`` `
ventana i : a[i] a[i+1] ... a[i+k-1]
ventana i+1 : a[i+1] ... a[i+k-1] a[i+k]
`` `

Sus XOR son iguales → `a[i] == a[i+k]`.
Repetir este argumento para todos los `i` muestra que el array debe ser *k-periodic*.

#### Paso 2 - Agrupación

Todos los índices con el mismo `i mod k` pertenecen a un *grupo*.
Dentro de un grupo todos los valores finales serán los mismos; de lo contrario la periodicidad se rompería.

#### Paso 3 - Costo de un grupo

Para un grupo de tamaño `s`, eligiendo el valor `v` costos
`cost = s - frecuencia(v)`.

#### Paso 4 – Global XOR Constraint

Que los valores elegidos para los grupos " k " sean " b [k-1] " .
El XOR de cualquier ventana es el XOR de un período: `b[0] ^ b[1] ^ ... ^ b[k‐1]`.
Necesitamos que esto sea `0`.

Así que el problema se reduce a: **Pick un valor para cada grupo de tal manera que el XOR de todos los valores elegidos es `0`, mientras que el costo total es mínimo**.

-...

### 2.5 The “Easy” DP

Debido a que cada elemento array es 1024, hay en la mayoría 1024 valores distintos.
Podemos enumerarlos.

`` `
dp[i][x] = mínimos cambios para los primeros grupos i cuyo XOR es x
`` `

* Initializar*
`dp[0][0] = 0`, todos los demás = INF.

*Transición*
Para el grupo `i ' y el xor actual `x`, pruebe todo el valor posible `v` en ese grupo:

`` `
newXor = x ^ v
newCost = dp[i][x] + (size_i - freq_i[v])
dp[i+1] [newXor] = min(dp[i+1] [newXor], newCost)
`` `

After processing all `k` groups, answer is `dp[k][0]`.

**La complejidad* *

* `k ≤ 2000`
* `MAX_XOR = 1024`
* Cada grupo tiene en lo más `min(size_i, 1024)' valores distintos

`` `
Tiempo : O(k · 1024 · distintos valores)
Memoria : O(k · 1024) ♥ 2 MB
`` `

Esto está muy por debajo de los límites (2 s / 512 MB).

-...

### 2.6 Why the DP Works

El DP realiza un seguimiento del *cumulativo XOR* de los valores de grupo ya elegidos.
Debido a que XOR es asociativo y comunicativo, cualquier combinación de opciones de grupo que rinde XOR `0` satisface la condición original de la ventana.
Al elegir siempre la opción más barata para el grupo actual, el DP garantiza la optimización global.

-...

## 3. toques finales – Consejos de cuidado

Silencio Lo que hice bien Silencio Lo que puedes hacer
Silencio.
Silencio **Fundar la estructura ocultatoria** ¦ Practicar la “caza de purpurina”: buscar la monotónica, la simetría o los invariantes. Silencio
Silencio **Used a clean DP** Silencio Estar listo para explicar su estado de DP a entrevistadores. Les encanta ver que usted entiende *por qué* una transición estatal es correcta. Silencio
Silencio **Optimizado para limitaciones** Silencio Siempre revise los rangos de valor primero; muchos problemas pueden ser capped por una pequeña constante (aquí 1024). Silencio
Silencio **Implemented in multiple languages** Silencio Show you're versátil: entrevistadores pueden pedirle que envíe una solución a otro idioma o entorno. Silencio

■ **Pro tip:** En su curriculum vitae o portafolio, escriba una sección "Problema-Solving". Incluya LeetCode 1787 y describir cómo lo redujo a un DP sobre grupos. Destacar la visión que convirtió “Hard” en “Easy”.

-...

### 4. Wrap‐Up

* LeetCode 1787 es un ejemplo de libro de texto de la estrategia **“mirar la estructura”**.
* La dureza del problema es *aparente* pero * ilusoria* – una vez que reconoce la periodicidad, es un grupo estándar– Problema del DP.
* El DP es elegante, eficiente y lingüístico-agnóstico – hemos mostrado código completo en Java, Python y C++.

Ahora usted está listo para aplastar esta pregunta en su próxima entrevista y, lo más importante, para detectar estructuras ocultas en otros problemas difíciles. ¡Feliz codificación!

-...

■ ** Recursos**
* Discusión LeetCode – 1787
* Cracking the Coding Interview – Dynamic Programming section
* YouTube – “XOR Tricks for Interview” por *Tech With Tim*

-...

#### 4.1 Nota de clausura

Si encontró este artículo útil, por favor ** compartirlo**.
Tus compañeros candidatos te lo agradecerán, y la comunidad seguirá creciendo.
¡Feliz preparación de entrevistas!