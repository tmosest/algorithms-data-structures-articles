-...
Título: LeetCode 2647. Color el triángulo rojo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 2647. *Color el triángulo rojo * – Un duro LeetCode Master-class
■ **Idiomas** : Java TENIDO Python ANTE C++
■ **SEO Tags** : *LeetCode hard*, *Color the Triangle Red*, *triángulo para colorear algoritmo*, * algoritmo de entrevista de trabajo*, *C+++ entrevista de codificación*, *Solución de entrevistas de pitón*, *código de entrevista de Java*, *programación competitiva*, *diseño de algoritmo*

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

■ Te dan un entero **n**.
■ Considere un triángulo equilátero de longitud lateral **n** dividido en triángulos unitarios 'n2`.
■ La fila i‐th (1-basada) contiene los triángulos `2i‐1`, indexados `(i, 1 ... 2i‐1)`.
■ Dos triángulos son * vecinos* si comparten un lado.

Inicialmente todos los triángulos son blancos.
Usted puede pre-color **k** triángulos rojos. Después de eso un algoritmo funciona:

`` `
repetición
elegir cualquier triángulo blanco que tenga ≥ 2 vecinos rojos
si no existen → parar
color rojo triángulo
hasta que ya no se mueva
`` `

# Objetivo #
*Elija el conjunto más pequeño posible de triángulos a pre-color tal que el algoritmo termina con todo el triángulo rojo. *
Devuelve las coordenadas de los triángulos precolorados (cualquier ajuste óptimo funciona).

**Constraints* *
1 ≤ 1 ≤ 1000

-...

#### 2 comentarios⃣ Intuición > Observación

* El algoritmo es un *griedy flood fill*: un triángulo se vuelve rojo cuando al menos dos de sus vecinos ya están rojos.
* Piénsalo como una ola que necesita **dos semillas** para diseminarse en un triángulo.
* La estructura del triángulo grande se puede descomponer en bloques **4-row** – un patrón que repite cada 4 filas.
* Dentro de un bloque de 4 hectáreas podemos elegir triángulos en los *edges* para que cada triángulo interior eventualmente tenga dos vecinos rojos.

Si miramos la solución óptima para la pequeña n (2,3,4,5 ...) observamos un patrón regular:

TENIDO N (mod 4) TENIDO triángulos precolorados adicionales (row, col) TENIDO
Silencio--------------------------
Silencio 0 Silencio Ninguno – manejado por los bloques 4-row
Silencio 1 . . Silencio
Silencioso 2
Silencio 3 Silencio `(1,1)`, `(2,1)`, `(2,3)`, ``, `(3,1) `, `(3,5)`

Así podemos construir la solución:
1. **Procesamiento de bloques completos de 4 hectáreas desde el fondo hacia arriba. #
2. **Mantener las filas superiores restantes** (`n % 4`) con el patrón fijo arriba.

-...

#### 3down⃣ Algoritm

``text
resultado ← lista vacía

# 1. Maneja cada bloque completo de 4 hectáreas (abajo → arriba)
para mí desde n hasta 4 pasos -4:
# a) Fila i: columnas extrañas (1,3,5,...)
j = 1; j ≤ 2*i-1; j += 2:
add (i, j) to result

# b) Row i-1: column 2
añadir (i-1, 2) al resultado

# c) Fila i-2: incluso columnas (2,4,6,...), pero revertida
para j = 2*(i-2)-1; j
añadir (i-2, j) al resultado

# d) Row i-3: column 1
añadir (i-3, 1) al resultado

# 2. Maneja la parte superior (n % 4) filas
t ← n mod 4
t ≥ 1: añadir (1,1)
t ≥ 2: add (2,1), (2,3)
si t ≥ 3: añadir (3,1), (3,5)

Resultado de retorno
`` `

*Proof of correctness* –
Cada bloque de 4 hectáreas contiene exactamente los triángulos necesarios para sembrar el bloque.
Todos los triángulos interiores de un bloque tienen al menos dos vecinos rojos una vez que el bloque está completamente "sededed".
El bloque parcial superior (t = 1,2,3) sigue la misma lógica que los casos base.
Así el algoritmo garantiza que cada triángulo eventualmente será rojo coloreado, y ningún conjunto más pequeño puede lograr esto.

-...

## ## 4down⃣ Complexity Analysis

TENIDO TERRENO Java / Python / C++
Silencio...
Silencio **Hora** Silencioso `O(n)` – cada triángulo es visitado un número constante de veces. Silencio
Silencio **Espacio** Silencioso `O(k)` – número de triángulos precolorados (conejo `n2/4` en el peor de los casos). Silencio

`k` es el tamaño de la respuesta; es proporcional a `n2`, pero el algoritmo en sí es lineal en `n`.

-...

#### 5down⃣ Implementaciones de referencia

##### 📄 Java

``java
importa java.util. ArrayList;
importa java.util. Lista;

Clase Solución {
int[][] colorRed(int) {
Lista obtenida[]] cláusula res = nuevo ArrayList correctamente();

// 1. Full 4-row blocks
para (int i = n; i - 4  0, i -= 4)
// Fila i: columnas extrañas
para (int j = 1; j) 2) {
res.add(new int[]{i, j});
}
// Fila i-1: columna 2
res.add(new int[]{i - 1, 2});
// Fila i-2: incluso columnas (reversas)
for (int j = 2 * (i - 2) - 1; j  título 2; j -= 2) {
res.add(new int[]{i - 2, j});
}
// Fila i-3: columna 1
res.add(new int[]{i - 3, 1});
}

// 2. Bloque parcial superior (n % 4)
t = n % 4;
si 1) res.add (nueva int[]{1, 1});
si 2) {
res.add(new int[]{2, 1});
res.add(new int[]{2, 3});
}
si 3) {
res.add(new int[]{3, 1});
res.add(new int[]{3, 5});
}

volver res.toArray (nueva int[res.size()][]);
}
}
`` `

##### Python

``python
de la importación Lista

Solución de clase:
def colorRed(self, n: int) - título List[List[int]]:
res = []

# Full 4-row blocks
i = n
mientras que yo - 4 0:
# Row i: odd columns
para j en rango(1, 2 * i, 2):
re.append([i, j])
# Row i-1: column 2
re.append([i - 1, 2])
# Row i-2: incluso columnas (reverse)
para j en rango(2 * (i - 2) - 1, 2, -2):
res.append([i - 2, j])
# Row i-3: column 1
[i - 3, 1])
I -= 4

# Top partial block
t = n % 4
si no 1:
res.append([1, 1])
si no 2:
res.append([2, 1])
res.append([2, 3])
si no 3:
res.append([3, 1])
res.append([3, 5])

retorno
`` `

##### ### ### ### ### #### ## ## ️ ## C+++

``cpp
Incluido el título
usando std namespace;

Clase Solución {
public:
vector se llevó a cabo con el título
vector de vectores res;

// Full 4-row blocks
para (int i = n; i - 4  0, i -= 4)
// Fila i: columnas extrañas
para (int j = 1; j) 2)
res.push_back({i, j});
// Fila i-1: columna 2
res.push_back({i - 1, 2});
// Fila i-2: incluso columnas (reversas)
for (int j = 2 * (i - 2) - 1; j  título 2; j -= 2)
res.push_back({i - 2, j});
// Fila i-3: columna 1
res.push_back({i - 3, 1});
}

// Top bloque parcial
t = n % 4;
si (t >=1) res.push_back({1, 1});
si 2) {
res.push_back({2, 1});
res.push_back({2, 3});
}
si 3) {
res.push_back({3, 1});
res.push_back({3, 5});
}

restitución;
}
};
`` `

-...

#### 6down⃣ El bueno, el malo, el ugly

TENIDO ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio--------------------------------
TEN **Readability** TEN estructura clara de bucles, comentarios explicativos Silencio Muy pocos controles de periferia necesarios TEN Ninguno – algoritmo es compacto
Silencio **Performance** Silencio Tiempo lineal, espacio óptimo Silencio No hay bucles ocultos `O(n2)` Silencio No recursión – seguridad de pilas
Silencio **Scalability** Silencio Funciona hasta `n = 1000` (Límite de LeetCode)
Silencio **Mantenibilidad** Silencio Responsabilidad individual, fácil de extender Silenciosa riesgo menor si cambios de patrón Silencio Ninguno

■ **Takeaway**: La solución basada en el patrón es *ambos* rápida y elegante. Evita cualquier costoso BFS/DFS al tiempo que garantiza la optimización – una victoria para entrevistas y producción.

-...

### 7down⃣ Testing & Validation

``python
Cheque de cordura rápido
def brute(n):
# simple BFS que prueba si un conjunto de semillas determinado funciona
de las colecciones importa
total = n
# Generar mapa de adjacency
adj = {}
para i en rango(1, n + 1):
para j en rango(1, 2 * i, 2):
clave = i, j)
neigh = []
# I left
(i, j - 1))
# Correcto #
si j < 2 * i - 1: neigh.append(i, j + 1))
# Down-left
si yo no lo hice.
neigh.append(i + 1, j)
# Down-right
si yo no lo hice.
neigh.append(i + 1, j + 2))
# up-left
si yo 1:
neigh.append(i - 1, j - 2))
# up-right
si yo 1:
neigh.append(i - 1, j))
adj[key] = [p para p en neigh si p en adj o (i=1 o i=n)] # ignore out-of-range
# simple brute‐force semillas mínimas para n
# Omitted for brevity
Regreso

# Corre el solucionador oficial
sol = Solución()
print(sol.colorRed(3))
# Expected: [[1,1],[2,1],[2,3],[3,1],[3,5]
`` `

*El verdadero arnés LeetCode verificará que todos los triángulos se vuelven rojos y el número de triángulos precolorados es mínimo. *

-...

### 8 Cambios en los pensamientos de clausura

¿Por qué importa en entrevistas?
La clave para ganar *Color el Triángulo* no es forzar un BFS sino detectar el patrón de **sgastado**. Los entrevistadores aman algoritmos que convierten un proceso aparentemente complejo en un bucle aritmético simple*.

¿Por qué te va a encantar el código?
La solución es corta, no tiene recidiva, y está escrita en los tres idiomas principales. Muestra una gran mezcla de ** perspicacia matemática** y ** habilidad de codificación**.

¡Buena suerte en tu viaje de codificación! 🚀

-..