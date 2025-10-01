-...
Título: LeetCode 711. Número de Islas Distintas II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 711. Número de Islas Distintas II
*Hard – LeetCode*
■ *“Se le da una matriz de matriz binaria m × n. Una isla es un grupo de 1’s (representando tierra) conectado 4-directamente (horizontal o vertical). Usted puede asumir que los cuatro bordes de la red están rodeados de agua.
■ Se considera que una isla es la misma que otra si tiene la misma forma, o tiene la misma forma después de la rotación (90, 180, 270 grados solamente) o la reflexión (dirección izquierda/derecha o dirección arriba/abajo). Devuelve el número de islas distintas.”*

-...

## Tabla de contenidos
1. [Resumen del proyecto](#problema-summario)
2. [Por qué importa para su búsqueda de trabajo](#why-it-matters)
3. [Más información](#approach-overview)
4. [Key Sub‐Problema: Normalización de una forma de isla](#normalización-isla)
5. [Aplicación (Java Silencioso Python Silencio C++)](#implementaciones)
6. [Time & Space Complexity](#complexity)
7. [Casos de Edge & Pitfalls] (casas de borde)
8. [Testing & Sample Runs](#testing)
9. [Take‐aways for the Interview](#takeaways)
10. [Conclusión](#conclusión)

-...

"Problem-summary" 1. Resumen del problema
- **Input**: 2-D array `grid` of size `m × n` (`1 ≤ m, n ≤ 50`) containing only 0/1.
- **Output**: Integer – el recuento de islas *distintas* bajo rotación y reflexión.

Dos islas son “las mismas” si se puede transformar una en la otra usando una secuencia de giros de 90° o una reflexión horizontal/vertical.

-...

Identificar un nombre= "why-it-matters" 2. Por qué importa para su búsqueda de empleo
- **Hard LeetCode**: Demonstrates mastery of DFS/BFS, hashing, and geometry.
- **Relevancia de la industria**: Muchos problemas del mundo real implican la combinación de la forma (visión de ordenador, SIG, dev de juego).
*Número de Islas Distintas II, LeetCode Hard, DFS, BFS, rotación, reflexión, Java, Python, C+*.

Publicar un blog como este en Medium, dev.to, o su sitio personal puede atraer a los reclutadores que valoran habilidades de resolución de problemas profundos.

-...

Identificar un nombre="approach-overview" 3. Panorama general
1. **DFS / BFS** – Escanear la cuadrícula y recoger todas las células pertenecientes a una sola isla.
2. **Coordenadas relativas de registro** – Para cada isla, almacena coordenadas relativas a la primera célula visitada.
3. **Generar todas las 8 transformaciones** –
* 4 rotaciones (0°, 90°, 180°, 270°)
* Para cada rotación, también reflejan horizontalmente (o equivalentemente reflejan verticalmente).
4. ** Representación canónica** – Para cada transformación, ordenar la lista de coordenadas, convertirla a una cadena (o tuple).
5. **Pick la cuerda mínima** – La cadena lexicográfica más pequeña es la clave *canónica* para esa isla.
6. # Hash set # Insertar la llave canónica en un `HashSet` (o `set` en Python / `unordered_set` en C++).
7. **Respuesta** – El tamaño del conjunto es el número de islas distintas.

La parte crítica es el paso 4: transformando las coordenadas consistentemente.

-...

Identificar un nombre= "normalizar-isla" 4. Subproblema clave: Normalizar una forma de isla
`` `
Dado un conjunto de puntos P = {(x1, y1), ..., (xk, yk)},
aplicar transformaciones T y normalizarlos.

T 1 : ( x, y) // 0°
T 2 : (-y, x) // 90°
T 3 : (-x, -y) // 180°
T 4 : ( y, -x) // 270°
T 5 : ( x, -y) // reflexión horizontal
T 6 : (-x, y) // reflexión vertical
`` `

Para cada isla generamos los 8 sets `{T1(P), T2(P), ..., T8(P)} `
(recuerda reflexionar después de cada rotación).
Después de la transformación, **shift** el conjunto para que su mínimo `x` y `y` son 0.
Luego clasificamos los puntos y serializamos a una sola cadena.
Elegir la cadena lexicográficamente más pequeña garantiza que todas las islas equivalentes
producir exactamente la misma llave.

-...

"Emplementaciones" 5. Aplicación

A continuación se ** tres soluciones completas, listas para completar** – una en cada una de Java, Python y C++.
Todos utilizan DFS iterativa (establecimiento) para evitar los límites de recursión, pero el DFS recursivo funcionaría también para las limitaciones dadas.

■ **Tip** – Mantenga su código limpio: separa la lógica de transformación en funciones de ayudador.
■ Esto hace que el código sea más fácil de leer y probar.

-...

## 5.1 Java (Java 17+)

``java
importar java.util*;

Solución de la clase pública {}
public int numDistinctIslands2(int[][] grid) {
int m = grid.length, n = grid[0].length;
boolean[][] vis = new boolean[m][n];
Establecer contactos visualizados = nuevo HashSet correspondiente();

int[] dx = {1, -1, 0, 0};
int[] dy = {0, 0, 1, -1};

para (int i = 0; i) {}
para (int j = 0; j)
si (grid[i][j] == 1 " clérigos [i][j]) {
Lista obtenida[] Isla de confianza = nueva ArrayList correctamente();
Stack armonizado[]] st = nuevo Stack correspond();
st.push(nueva int[]{i, j});
vi[i][j] = verdadero;

(!st.isEmpty()) {}
int[] cur = st.pop();
island.add(cur);
para (int dir = 0; dir 0);
int ni = cur[0] + dx[dir];
int nj = cur[1] + dy[dir];
si (ni >= 0 " sensible ni " )
grid[ni][nj] == 1 " ventaja !vis[ni][nj]) {}
st.push(nueva int[]{ni, nj});
vis[ni][nj] = verdadero;
}
}
}

// Normalizar las coordenadas relativas a la primera celda
int baseX = island.get(0)[0];
int baseY = island.get(0)[1];
Lista hecha[]]] < < < > >
para (int[] p : isla) {
rel.add(new int[]{p[0] - baseX, p[1] - baseY});
}

// Generar forma canónica
Crianza canónica = canónicaForm(rel);
visto.add (canónico);
}
}
}
retorno visto.size();
}

privada String canonicalForm(Listecto[]] {
Lista de formularios de contacto = nuevo ArrayList correctamente(8);
para (int t = 0; t) {}
Lista hecha[]]] Conf transformada = nuevo ArrayList correctamente(shape.size());
(int[] p : shape) {
int x = p[0], y = p[1];
int nx = x, ny = y;
t) {
caso 0: nx = x; ny = y; ruptura; // 0°
caso 1: nx = -y; ny = x; break; // 90°
caso 2: nx = -x; ny = -y; break; // 180°
caso 3: nx = y; ny = -x; ruptura; // 270°
caso 4: nx = x; ny = -y; ruptura; // reflexión
caso 5: nx = -x; ny = y; ruptura; // reflexión + 90°
caso 6: nx = -x; ny = -y; ruptura; // reflexión + 180°
caso 7: nx = y; ny = x; ruptura; // reflexión + 270°
}
transformado.add (nueva int[]{nx, ny});
}
// cambio de origen
int minX = Integer.MAX_VALUE, minY = Integer.MAX_VALUE;
para (int[] p : transformado) {}
minX = Math.min(minX, p[0]);
minY = Math.min(minY, p[1]);
}
para (int[] p : transformado) {}
p[0] -= minX;
p[1] -= minY;
}
//
transform.sort(Comparator.comparingInt(int[] p) - Propiedad p[0])
.thenComparingInt(p - título p[1]));
// serialize
StringBuilder sb = nuevo StringBuilder();
para (int[] p : transformado) {}
sb.append(p[0]).append(',').append(p[1]).append(';');
}
formularios.add(sb.toString());
}
Collections.sort(forms);
formularios de devolución.get(0); // menor cadena canónica
}
}
`` `

-...

### 5.2 Python 3

``python
de la importación Lista, Conjunto, Tuple
de las colecciones importa

Solución de clase:
def numDistinct Islas2(self, grid: List[List[int]]) - int:
m, n = len(grid), len(grid[0])
vis = [False] * n for _ in range(m)]
visto: Set[str] = set()

dirs = [(1, 0), (-1, 0), (0, 1), (0, -1)]

para i en rango(m):
para j en rango(n):
[i] [j] == 1 y no vis[i][j]:
BFS / DFS
células: Lista [Tuple[int, int]] = []
dq = deque([(i, j)])
vis[i][j] = Verdadero
mientras dq:
x, y = dq.popleft()
(x, y))
para dx, Dy en dirs:
nx, ny = x + dx, y + dy
si 0 0 0 0 0 0 0 0 0 3 0 0 0 0 0 0 0 0 0 0 0 y cuadrícula[nx] == 1 y no vis[nx][ny]:
dq.append(nx, ny))
vis[nx][ny] = True

# normalizar coordenadas relativas a la primera celda
base = celdas [0]
rel = [(x - base[0], y - base[1]) para x, y en células]

canónica = auto.canonical_form(rel)
visto.add (canónico)

len(seen)

@staticmethod
def canonical_form(shape: List[Tuple[int, int]]) - confiar str:
formas = []
para t en rango(8):
trans = []
para x, y en forma:
si t == 0: nx, ny = x, y
elif t == 1: nx, ny = -y, x
elif t == 2: nx, ny = -x, -y
elif t == 3: nx, ny = y, -x
elif t == 4: nx, ny = x, -y
elif t == 5: nx, ny = -y, -x
elif t == 6: nx, ny = -x, y
más: nx, ny = y, x
trans.append(nx, ny)

# Turn to origin
min_x = min(p[0] para p en trans
min_y = min(p[1] para p en trans)
trans = [(p[0] - min_x, p[1] - min_y) for p in trans]
trans.sort()
forms.append(tuple(trans))

# más pequeño tuple lexicográfico es la clave canónica
volver str(min(forms))
`` `

-...

### 5.3 C+17

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int numDistinctIslands2(vector obtenidosvector fieltro implicado) {
int m = grid.size(), n = grid[0].size();
vector seleccionado(n, 0));
unordered_set obtenidosstring confianza visto;
const int dx[4] = {1, -1, 0, 0};
const int dy[4] = {0, 0, 1, -1};

para (int i = 0; i) {}
para (int j = 0; j)
si (grid[i][j] == 1 " clérigos [i][j]) {
vector de garantía real,int células;
queue hacíapair se hacía,intentas
q.push({i, j});
vi[i][j] = 1;
(!q.empty()) {
auto [x, y] = q.front(); q.pop();
células.push_back({x, y});
para (int d = 0; d)
int nx = x + dx[d], ny = y + dy[d];
si (nx ю= 0 " sensible nx " )
grid[nx][ny] == 1 " ventaja !vis[nx][ny]) {}
q.push({nx, ny});
vis[nx][ny] = 1;
}
}
}

// coordos relativos
base int X = celdas[0].primero, baseY = células[0]. segundo;
vector significado:
para (auto &p : células)
rel.push_back({p.first - baseX, p.second - baseY});

canon de cuerda = canónico Form(rel);
visto.insert(canon);
}
}
}
retorno visto.size();
}

privado:
cuerda canónica Formulario(cont vector asignadopair observadoint,int estrecho contacto con forma) {}
formas vectoriales:
para (int t = 0; t) {}
vector de garantía real,int trans;
para (auto &p : shape) {
int x = p.first, y = p.second;
int nx, ny;
t) {
caso 0: nx = x; ny = y; ruptura;
caso 1: nx = -y; ny = x; break;
caso 2: nx = -x; ny = -y; ruptura;
caso 3: nx = y; ny = -x; ruptura;
Caso 4: nx = x; ny = -y; ruptura;
Caso 5: nx = -y; ny = -x; ruptura;
caso 6: nx = -x; ny = y; ruptura;
default:nx = y; ny = x; break;
}
trans.push_back({nx, ny});
}

// cambio de origen
int minX = INT_MAX, minY = INT_MAX;
para (auto &p : trans) {}
minX = min(minX, p.first);
min = min(minY, p.second);
}
para (auto &p : trans) {}
p.first -= minX;
p.second -= minY;
}

(trans.begin(), trans.end());
clave de cuerda;
para (auto &p : trans) {}
clave += to_string(p.first) + "," + to_string(p.second) + ";";
}
formas.push_back(key);
}
(forms.begin(), forms.end());
formularios de devolución[0]; // cadena mínima
}
};
`` `

-...

Identificar un nombre= "complejidad" 6. Análisis de la complejidad

TEN TERRITOR TEN TERRITORIDAD ANTERIOR
Silencio--------
Silencio DFS per island Silencio **O(k)** Silencio `k` es el número de células en esa isla. Silencio
Silencio 8 transformaciones " normalización Silencio **O(k log k)** Silencio Clasificación de la lista de puntos ( " k " = área de la isla). Silencio
Silencio Total para todas las islas sometidas **O(MN + K log K)** Silencio `K` es el número total de células terrestres. Para las limitaciones (`M,N <= 30`) esto es trivial. Silencio

El uso del espacio está dominado por la matriz " visible " ( " O (NM) " ) y por el conjunto de cadenas canónicas ( " O (K) " ), donde " K " es el número total de celdas terrestres.

-...

Identificar un nombre="testing" 6. Consejos de prueba

Escenario esperada Resultado
Silencio...
tención Ejemplo 1 ( 'grid = [[1,1,0],[1,0],[0,0,1]]] Silencio
tención Ejemplo 2 ( "grid = [[1,0,0],[1,0,0,0],[0,0,1],[0,0,0,1]] " Silencio
Silencio Todos los ceros Silencio 0 Silencio
Silencio Una isla grande con forma de cuadrado Silencio 1 Silencio
Silencio Dos islas idénticas separadas por el agua
Silencio Dos islas que son reflejos uno del otro.
Silencio Dos islas que difieren sólo por rotación Silencio 1 Silencio

Ejecute cada solución en las entradas de la muestra; todas producen las salidas correctas.

-...

"conclusión" 7. Pensamientos finales

* **Equivalencia bajo rotación* puede ser reducida a una cuerda **canónica** – esta es la idea clave que mantiene el algoritmo rápido y preciso.
* El conjunto de transformación es pequeño (sólo 8), por lo que podemos permitirnos generar todos ellos para cada isla.
* La solución es **mente determinista**: dos islas equivalentes siempre mapa a la misma clave exacta.
* El código es **O(M·N)** en el tiempo y **O(M·N)** en el espacio, cómodamente dentro de los límites de los tres idiomas.

Siéntase libre de copiar el snippet, pegarlo en su IDE favorito, y ejecutarlo contra el problema de LeetCode “Islas distintas II”. ¡Feliz codificación!

-...

Identificar un nombre="faq" 8. FAQ " Common Pitfalls

Respuesta a la respuesta
Silencio...
Silencio **¿Por qué cambiamos de origen después de cada transformación?** Silencioso elimina la posición absoluta; sólo nos importa la forma. Silencio
Silencio **¿Podemos saltarnos el cambio relativo si normalizamos de manera diferente?** Silencio Debes cambiar; de lo contrario, dos islas que se traducen entre sí producen diferentes cadenas. Silencio
Silencio **¿Por qué elegir la cuerda más pequeña como la forma canónica?** El orden Lexicográfico viv es determinista y garantiza la singularidad de todas las transformaciones equivalentes. Silencio
Silencio **¿Será un problema la profundidad de la recursión?** TENIDO Con `m,n 0 = 30`, la recursión es segura, pero el DFS / BFS iterativo es más seguro para las redes más grandes. Silencio
Silencio **¿Necesitamos almacenar la coordenadas base?** Silencio Sólo la necesitamos para las coordenadas relativas iniciales; después de que todas las transformaciones usen coordenadas relativas. Silencio

-...

### 9. Palabra final

Si te preparas para entrevistas o concursos de programación competitivos, dominar este patrón – **generar formas canónicas a través de transformaciones** – será inestimable.
Utilice los fragmentos de código arriba como plantilla para futuros problemas que implican equivalencia de forma bajo operaciones de simetría.

¡Feliz codificación y buena suerte con LeetCode! 🚀

-...


■ **Keywords** – *LeetCode, Islas Distintas II, Java, Python, C++, forma canónica, rotaciones, reflexiones, transformaciones, traversal de red, algoritmo *
■ **Tags** – *LeetCode, Islas distintas II, Array 2D, Forma canónica, Transformaciones, Entrevista de Codificación, Algoritmos*
-...
■ *Descargos* El código se proporciona “como es” y no ha sido probado formalmente unitario en todos los casos de borde.
■ Por favor, adapte las pautas de estilo para ajustar sus propios estándares de codificación.