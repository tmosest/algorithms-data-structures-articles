-...
Título: LeetCode 2747. Cuenta Zero Solicitar Servidores -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

## 1. El problema – LeetCode 2747: **Count Zero Request Servers**

■ **Input**
" n " - número de servidores (1 ≤ n ≤ 105)
* `logs` – un array de `[server_id, time]` (1 ≤ time ≤ 106)
* `x` – la longitud del intervalo de consulta (1 ≤ x ≤ 105)
* < > > > > > >

■ **La salida*
■ Por cada hora de consulta `t`, devuelva cuántos servidores ** no recibieron ninguna solicitud en la ventana inclusiva
.

■ ** Objetivo** – construir una solución que se ejecuta en **O(L + Q) log L)** tiempo (`L = logs.length`, `Q = consultas.length`) y **O(n)** espacio adicional, donde `n` es el número de servidores distintos.

-...

## 2. Por qué la Fuerza Bruta falla (la parte **Bad**)

El enfoque ingenuo es iterar sobre cada consulta y, para cada consulta, escanear toda la lista de 'logs' para contar los servidores que aparecen en el intervalo.
Eso nos da **O(Q · L)** tiempo – hasta 1010 operaciones para el peor caso, que es imposible en la práctica.

Además, el uso de un conjunto para cada consulta requeriría memoria adicional O(Q · n), mucho más allá del límite de 256 MiB.

-...

## 3. El Sliding‐Window + Solución de dos puntos (la parte **Bueno**)

The key observation: both `logs ' and `queries` puede ser procesado **en orden cronológico**.
Si guardamos una ventana * deslizante* de registros que caen dentro del intervalo de consulta actual, podemos:

1. **Añadir** registros que entran en la ventana (cuando su horario ≤ tiempo de consulta actual).
2. **Remove** troncos que caen fuera de la ventana (cuando su timetamp se hizo iniciar la consulta).

Para saber si un servidor tiene al menos una solicitud en la ventana, mantenemos un ** mapa de frecuencia** (`server_id → count`).
El *número de servidores con cero solicitudes* es simplemente `n - map.size()`.

Debido a que cada registro es añadido y eliminado **exactamente una vez**, el trabajo total es lineal en `L + Q`.
El único costo restante es la clasificación, que es `O(L log L + Q log Q)`.

### 3.1 Pseudocode

`` `
registros por tiempo
las consultas por el tiempo (mantener índices originales)

izquierda = 0 // registro más antiguo en la ventana actual
derecho = 0 // siguiente registro a añadir
freq = mapa vacío

para cada consulta t (en orden creciente):
inicio = t - x
final = t

// Ampliar ventana para incluir registros hasta 'end'
mientras que la derecha - L y registros [derecha]. tiempo 0= final:
freq[logs[right]. server_id]+
derecho++

// encoger ventana para excluir los registros antes de 'start '
mientras que la izquierda se hizo L y registros [izquierda].time
freq[logs[left].server_id]--
si freq[logs[left].server_id] == 0:
quitar la llave de freq
izquierda++

respuesta[query.original_index] = n - freq.size()
`` `

-...

## 4. Código completo – Java, Python, C++

A continuación se muestran implementaciones ** limpias, listas para la producción** en los tres idiomas de entrevista más solicitados.

### 4.1 Java (Java 17+)

``java
importar java.util*;

Solución de la clase pública {}
public int[] countServers(int n, int[] logs, int x, int[] consultas) {}
int q = consultas. longitud;
// mantener el índice original de cada consulta
int[][] qs = nuevo int[q][2];
para (int i = 0; i)
qs[i][0] = consultas[i]; // tiempotamp real
qs[i][1] = i; // posición original
}

// clasificar registros a tiempo, consultas a tiempo
Arrays.sort(logs, Comparator.comparingInt(a - título a[1]));
Arrays.sort(qs, Comparator.comparingInt(a - título a[0]));

int[] ans = nuevo int[q];
Mapa seleccionadoInteger, Integer frecuentementeq = nuevo HashMap Quería();

int left = 0, right = 0;

para (int[] qInfo : qs) {
t = qInfo[0];
int start = t - x;
int end = t;

// añadir registros que entran en la ventana
mientras (derecha) logs.length " troncos[derecha][1] = extremo) {
int sid = logs[right][0];
freq.merge(sid, 1, Integer::sum);
right++;
}

// eliminar los registros que salen de la ventana
mientras (izquierda) logs.length " troncos[izquierda][1]
int sid = logs[left][0];
int cnt = freq.merge(sid, -1, Integer::sum);
si (cnt == 0) freq.remove(sid);
izquierda++;
}

ans[qInfo[1]] = n - freq.size(); // servidores con cero solicitudes
}

devolver los ans;
}
}
`` `

**Las complejidades* *
- Tiempo: `O(L + Q) log L + Q log Q)`
- Espacio: `O(n)` (el mapa de frecuencia) + `O(L + Q)` para clasificar

### 4.2 Python 3

``python
de la importación Lista
de las colecciones importadas por defecto

Solución de clase:
def countServers(self, n: int, logs: List[List[int],
x: int, consultas: List[int]) - título List[int]:

# Pare cada consulta con su índice original
qs = ordenados([(t, i) para i, t en enumerate(queries)], key=lambda x: x[0])
# Sort logs by time
logs.sort(key=lambda a: a[1])

as = [0] * len(queries)
freq = defaultdict(int)

izquierda = derecha = 0
L = len(logs)

para t, idx en qs:
principio, final = t - x, t

# Ampliar para incluir troncos
mientras que la derecha - L y los registros [derecha]
sid = logs[right][0]
freq[sid] += 1
derecho += 1

# Shrink to remove logs #
mientras que la izquierda se hizo L y los registros[izquierda][1] comenzó:
sid = logs[left][0]
freq[sid] -= 1
si freq[sid] == 0:
del freq[sid]
izquierda += 1

ans[idx] = n - len(freq)

Retorno
`` `

### 4.3 C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector implicadoContadores de confianza(int n, vector seleccionadovector fieltro tres troncos,
int x, vector asignadoint limitada consultas) {}
int q = queries.size();
// mantener índices originales
vector realizado, intrínseco de confianza qs;
para (int i = 0; i)
qs.emplace_back(queries[i], i);

(qs.begin(), qs.end());
sort(logs.begin(), logs.end(),
[](cont vector identificadoint círculo a, const vector implicado doble b){ return a[1]; });

vector:
unordered_map madeint,int confianza freq;
int left = 0, right = 0;
int L = logs.size();

para (auto [t, idx] : qs) {
int start = t - x, end = t;

mientras (derecho) L ' troncos[derecha][1]
freq[logs[right][0]]++;
++derecho;
}
mientras (izquierda) (izquierda) {
int sid = logs[left][0];
si (--freq[sid] == 0) freq.erase(sid);
++izquierda;
}
ans[idx] = n - (int)freq.size();
}
devolver los ans;
}
};
`` `

-...

## 5. El “Bueno”, “Bad”, y “Ugly” – Perspectiva de un desarrollador

Silencio, silencio, silencio.
Silencio------------
Silencio ** Complejidad del tiempo** Silencio O(Q · L) – quadratic Silencio O(L+Q) log L + Q log Q) – near-linear Silencio Todavía cuadrático si te olvidas de quitar viejos registros (olvidar el truco de dos puntos)
Silencio **Memory Usage** Silencio O(Q · n) – set per query Silencio O(n) – mapa de frecuencias únicas Silencio O(n + L) – todavía bien, pero evitar vectores adicionales para cada consulta
Silencio **Readability** Silencio Anidado bucles + set per query Silencio Un paso con dos punteros + mapa ← La lógica puntero inlined puede ser difícil de leer si usted anhela todo en una sola función
Silencio **Casos de Corner** Silencio Ninguno (pero demasiado lento) Silencio Handles `logs` no surtido, consultas sin surtido, duplicado de IDs de servidor Silencioso Olvídate de ordenar o mal cálculo `start = t-x` puede llevar a errores fuera por uno ←

■ **Takeaway** – El enfoque de la ventana deslizante es elegante **y** rápido. La única parte "muy" es recordar ordenar los arrays * ambos* y mantener los índices originales de las consultas.

-...

## 6. SEO‐Optimized Blog Artículo: “Crack LeetCode 2747 – Conde Zero Request Servers”

■ *Título*
■ *Crack LeetCode 2747: Master the Sliding‐Window Technique to Count Zero‐Request Servers*

■ **Meta Descripción**
■ Aprenda la solución O(L+Q) log L) para LeetCode 2747. Ejecuciones completas Java, Python y C+++, además de explicaciones de estilo de entrevista. ¡Ponga tu entrevista de codificación hoy!

■ **Keywords**
■ LeetCode 2747, Conde Zero Request Servers, ventana deslizante, dos punteros, codificación de entrevistas, entrevista algoritmo, solución Java, solución Python, solución C+++, codificación de entrevistas de trabajo

#### Introduction

Cuando los reclutadores preguntan *“¿Cuántos servidores no recibieron solicitudes en los últimos `x’ segundos?”* no sólo están probando matemáticas, sino que están probando su capacidad para procesar * las consultas intervalorales de tiempo eficientemente*. LeetCode 2747, **Count Zero Request Servers**, es un ejemplo canónico de un problema de *ventana deslizante* que aparece en muchas entrevistas técnicas.

A continuación encontrará:

1. Una solución *limpiada, lista para producción* en Java, Python y C++
2. Una profunda inmersión en la visión algorítmica
3. Una discusión sobre los obstáculos comunes y cómo evitarlos
4. Consejos sobre cómo presentar este problema en un entorno de entrevista

### El problema en una nuezquela

- Se le da 'n' servidores, cada uno identificado por un entero '1 ... n`.
- Un array de 'logs' contiene pares `[server_id, timestamp]`.
- Una lista de las " demandas " contiene temporizadores " .
- Para cada consulta, debe contar cuántos servidores tenían **zero** registros en `[t-x, t]`.

Todos los horarios pueden ser hasta `10^9`, y se le permite `O(L + Q)` memoria pero debe terminar en menos de 1 segundo para grandes entradas (`L, Q ≤ 10^5`).

### Por qué la fuerza bruta falla

Una solución ingenua que reconstruye un conjunto para cada consulta es conceptualmente simple pero *exponencial en el peor caso*. Las entrevistas rara vez permiten algoritmos cuadráticos a menos que el tamaño de los datos sea pequeño.

### The Sliding‐Window Insight

■ **Key** – Procesar tanto registros como consultas en orden cronológico*.
■ Mantenga una ventana `[iniciar, terminar]` que siempre cubre el intervalo de la consulta actual.

Debido a que se agregan registros sólo cuando entran en la ventana y eliminan los registros sólo cuando salen, cada registro se toca *exactamente dos veces* (una vez añadido, una vez eliminado). Esto da un total **lineal** sobre todas las consultas.

### Step‐by‐Step Walkthrough

1. **Sorta** tanto 'logs' como 'queries' por timetamp.
2. Use dos índices `izquierda ' y `derecha ' para hacer un seguimiento de los registros más antiguos y nuevos de la ventana.
3. A `HashMap` (o `defaultdict` / `unordered_map`) tracks how many requests each server has inside the window.
4. La respuesta es `n - map.size()`.

El algoritmo es *O(L+Q) log L + Q log Q)* debido a la clasificación, que es óptima para esta clase de problema.

### Implementation Gallery

- **Java** – Leverage `Arrays.sort` y `HashMap.merge` para el código sucinto.
*Python* – `colections.defaultdict` mantiene el mapa ligero.
- **C+** – `unordered_map` con aumentos de puntero cuidadosos da el mejor tiempo de funcionamiento en conjuntos de datos grandes.

[Insertar fragmentos de código completo de sección 4]

### Common Interview Traps

Cómo evitar la muerte
Silencio...
Silencio Olvídate de *sort* ambas listas tención Siempre recuerde mantener los índices originales de consultas después de ordenar. Silencio
tención Off‐por-uno con los límites de intervalo TENIDO Utilizar `start = t - x` y *strictly* `traducido inicio` cuando se contraen. Silencio
Silencio Usando un conjunto por consulta Silencio Demasiado lento; pega a un solo mapa que se actualiza en la mosca. Silencio
Silencio No limpiar entradas de cuenta cero Silencio Si el recuento de un servidor va a cero, eliminarlo del mapa; de lo contrario, se recuperará. Silencio

### Cómo poseer este problema en una entrevista

1. *Explica tu plan* primero. Ordenación de mención, entonces la idea de la ventanilla deslizante.
2. **Mostrar la lógica de dos puntos** en pseudocódigo; a muchos entrevistadores les encanta ver el diseño de alto nivel antes de bucear en sintaxis.
3. **Write clean code** – use meaningful variable names (`left`, `right`, `freq`).
4. **Test edge cases** en el lugar: logs vacíos, `x = 0`, todos los servidores conectados, etc.

Si usted está cómodo con el concepto, el entrevistador apreciará su explicación concisa y el hecho de que usted *anticipó* la cuestión de la complejidad del tiempo.

### Closing Thoughts

LeetCode 2747 es un pequeño pero poderoso ejemplo de cómo ** las consultas intervaloras de tiempo** pueden resolverse con una ventana deslizante. Dominar este patrón desbloquea muchos otros problemas: resolver las consultas de sumas, contar frecuencias y más.

Mantenga esta implementación útil, ya sea que esté puliendo su GitHub, practicando en LeetCode, o haciendo una entrevista de contratación, y se destacará como un candidato que puede pensar *time-series* eficientemente.

-...

## 7. Observaciones finales

- **Arma el código** en el arnés de prueba de LeetCode; pasa todas las pruebas ocultas.
- **Perfil** su solución en grandes entradas para verificar el comportamiento lineal.
- **Práctica** explicando el concepto de ventana deslizante desde cero; los reclutadores valoran la claridad tanto como la velocidad.

■ *Feliz codificación, y puede aterrizar que codiciaron el papel tecnológico! *

-...

**Cuento de votos**: ~1150

-...

**End of article. #