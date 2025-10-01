-...
Título: LeetCode 568. Días máximos de vacaciones -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 568. Días máximos de vacaciones – Código, Análisis " Blog SEO‐Ready

■ ** Fuente del programa:** LeetCode Hard
■ **Conceptos clave:** Programación dinámica, Compresión Estatal, Traversal Gráfico
■ *Ideal para:* Entrevistas de software para mejorar (Java/Python/C++)

-...

#### TL;DR

Mantenemos una tabla del DP `dp[city]`. que almacena los días de vacaciones *maximum* alcanzables **de la semana actual al final** si estamos en 'ciudad' al comienzo de esa semana.
Iteramos semanas **hacia atrás** (de la semana `k-1` a la semana `0`).
Para cada ciudad consideramos:

1. **Stay** – tomar los días de vacaciones de esa ciudad en la semana actual.
2. **Fly** – elegir una ciudad que podamos alcanzar a través de un vuelo directo, tomar sus días de vacaciones para la semana actual y añadir el mejor valor futuro (`dp[dest]`).

La respuesta final es `dp[0]`. porque empezamos en la ciudad `0` el lunes.

Complexity:
- **Tiempo: ** `O(k * n2)` (k ≤ 100, n ≤ 100 → ~1 000 000 ops)
- **Espacio:** `O(n)` para el array DP (dos arrays de longitud `n`).

-...

Problema Recap

Estás en un mundo de **n ciudades** y **k semanas**.
- Los vuelos se dirigen (matrix `flights[n]` – 1 = vuelo disponible, 0 = ninguno).
- Cada semana se puede *fly* *una vez* – sólo el lunes por la mañana.
- `días[n][k]` da los días máximos de vacaciones que puede tomar en la ciudad `i ` durante la semana `j`.
- Usted puede permanecer más tiempo que los días permitidos, pero sólo los días permitidos cuentan.
- Ciudad inicial: `0` el lunes de la semana 0.

** Objetivo:** Maximizar los días de vacaciones totales durante todas las semanas.

-...

## 🔧 Solution (Bottom‐Up DP)

A continuación se muestra una implementación concisa y lista para la producción en **Java, Python, y C++**.
Todas las versiones comparten la misma lógica, sólo la sintaxis difiere.

### 1. Java

``java
importar java.util*;

Solución de la clase pública {}
int public int maxVacationDays(int[][], int[] days) {
si (días == null tención días infligidos. longitud == 0) retorno 0;
int n = días. longitud;
int k = días[0]. longitud;

// dp[city] = días máximos de vacaciones de la semana actual a fin si estamos en la ciudad '
int[] dp = nuevo int[n];
// Iterate semanas de las últimas a las primeras
para (una semana = k - 1; semana 0; --week) {
int[] next = new int[n];
para (int cur = 0; cur < n; ++cur) {
// Opción 1: estancia en la ciudad actual
siguiente[cur] = días[cur] [semana] + dp[cur];

// Opción 2: volar a una ciudad accesible
para (int dest = 0; dest {}
si (vuelos[cur] [dest] == 1) {
siguiente[cur] = Math.max(next[cur],
días[dest][week] + dp[dest]);
}
}
}
dp = siguiente;
}
volver dp[0]; // comenzar en la ciudad 0
}
}
`` `

### 2. Pitón

``python
Solución de clase:
def maxVacation Días(auto, vuelos: List[List[int],
días: List[List[int]] int:
si no días:
retorno 0
n, k = len(días), len(días[0])
*
durante la semana invertida(range(k)):
nxt = [0]
para curar en rango(n):
Quédate
nxt[cur] = días[cur][semana] + dp[cur]
# Volar #
para el dest en rango(n):
si los vuelos [curen][se]:
nxt[cur] = max(nxt[cur],
días[dest][semana] + dp[dest]
dp = nxt
retorno dp[0]
`` `

### 3. C++

``cpp
Incluido el título
#include >

Clase Solución {
public:
int maxVacationDays(std::vector seleccionado:::vector seleccionadoint implicancia reducida vuelos,
std:::vector seleccionados::vector realizado injertado!
si (días.empty()) devuelve 0;
int n = days.size();
int k = days[0].size();
std::vector obtenidosint titulada dp(n, 0);

para (una semana = k - 1; semana 0; --week) {
std::vector garantizadoint siguiente(n, 0);
para (int cur = 0; cur < n; ++cur) {
// Permanecer en la ciudad actual
siguiente[cur] = días[cur] [semana] + dp[cur];
// Volar a las ciudades accesibles
para (int dest = 0; dest {}
si (vuelos[cur] [dest] == 1) {
siguiente[cur] = std::max(next[cur],
días[dest][week] + dp[dest]);
}
}
}
dp.swap(next);
}
dp[0];
}
};
`` `

-...

## 🎯 Why This Works (Intuition)

1. **Definición estatal** – `dp[city]` tiene el valor futuro óptimo de una ciudad determinada.
Esto evita la recomputación y captura la dependencia entre semanas.

2. **Recipiente iteración** – A partir de la última semana asegura que cuando computamos la semana `w`, todas las semanas futuras (`w+1...k-1`) ya son óptimas.

3. **Dos opciones por semana** – O quedarse o volar.
Debido a que los vuelos son sólo el lunes, la única decisión que importa para la próxima semana es *donde terminas* después del vuelo del lunes.

4. Traversal Gráfico** El bucle interior sobre `dest` explora todos los vuelos salientes desde `cur`.
La complejidad sigue siendo aceptable porque `n ≤ 100`.

-...

## 📊 Complexity Table

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Silencio Java Silencioso `O(k * n2)` Silencio
Silencio Python Silencio `O(k * n2)` Silencio
Silencio C++ Silencioso `O(k * n2)` Silencio

-...

## 🧰 Tips for Interviewers > Candidatos

✔ Buenas noticias sobre la vida
Silencio------------
Silencio **Bien** Silencio Utilizar nombres variables claros (`dp`, `next`). tención Evite los tamaños de array de codificación dura. tención Olvídate de manejar casos de bordes (`días` vacíos). Silencio
Silencio **Bueno** Silencio Explicar el estado del DP y por qué iteramos hacia atrás. Silencio Escribir pruebas unitarias para casos de esquina (sin vuelos, todos los vuelos). Silencio Skip the proof that stay in the same city is always considered. Silencio
Silencio **Bien** Silencio Show how to transform the recurrence into code. Silencio Sobre el cumplimiento de cada línea. Silencio Use recursión sin memoización → apilación desbordamiento. Silencio
Silencio **Bueno** Silencio Mención que la solución puede ser optimizada para `O(k * n + k * m)` donde `m` es número de bordes si las listas de adyacency se utilizan. No optimizar más el espacio cuando `n` puede ser grande. ← Misinterpret "luz sólo el lunes" que conduce a la recurrencia errónea DP. Silencio

-...

## 📚 SEO‐Optimized Blog Article

■ **Título:** Master LeetCode 568: Maximum Vacation Days – Java, Python, C++ Solutions & Interview Tips
■ **Meta Descripción:** Aprende a resolver LeetCode Hard #568 “Maximum Vacation Days” con código Java claro, Python y C++. Entender el enfoque DP, analizar la complejidad y obtener consejos de entrevista.

-...

### 1. Introducción

LeetCode **Maximum Vacation Days** es un problema clásico de programación dinámica que prueba su capacidad de manejar las transiciones estatales en un gráfico. Con **n cities** y **k weeks**, usted debe planificar vuelos y vacaciones para maximizar los días de descanso total. En este artículo, diseccionamos el problema, presentamos soluciones Java limpias, Python y C+++, y discutimos las dificultades para evitar durante las entrevistas.

-...

### 2. Sinopsis de problemas

- **Flights**: `flights[i][j] = 1` significa un vuelo directo de la ciudad `i` a `j`.
- ** Límites de conversión**: `days[i][w]` es el máximo de días de vacaciones que se puede tomar en la ciudad `i` durante la semana `w`.
- Rulas.
- Empiezas en la ciudad '0' la semana 0 Lunes.
- Los vuelos sólo se toman una vez por semana, el lunes.
- Un día de vuelo cuenta con los días de vacaciones de la ciudad de destino.

Su objetivo: **Máximas vacaciones totales** durante semanas.

-...

### 3. Intuición " DP Formulation "

Tratamos cada semana como una transición del estado**.
Dejar `dp[city]` denota los días máximos de vacaciones alcanzables desde la *actual* semana hasta el final si estás en `ciudad' al comienzo de esa semana.

Transición (por semana `w`):
- **Stay**: `days[city][w] + dp[city] `
- **Fly**: Por todos los `dest`, `días[dest][w] + dp[dest] `

Lo mejor de estos dos da el nuevo valor para 'ciudad' en la semana anterior.
Iteramos semanas atrás para que todas las semanas futuras (`w+1...k-1`) ya sean óptimas.

-...

### 4. Code Walkthrough

##### Java

[Fuente total mostrada en la sección "Solución" arriba.]

#### Python

[Fuente total mostrada anteriormente.]

###### C++

[Fuente total mostrada anteriormente.]

-...

### 4. Análisis de la complejidad

Con 'n ≤ 100' y 'k ≤ 100':

- **Tiempo**: `O(k * n2)` – hasta 1.000 000 operaciones, fácilmente dentro de los límites.
- **Espacio**: `O(n)` - dos tipos de DP de longitud `n`.

-...

### 5. Entrevista Pitfalls

Silencio ¿Qué pasa con **Evite**
Silencio...
Silencio No iterating weeks backs ← Leads to incorrect future value use. Silencio
Silencio Ignorar la limitación de “luz el lunes” Causa una recurrencia inválida. Silencio
Silencio Utilizando la recursión sencilla sin la memoización TEN resultados en tiempo exponencial y posible desbordamiento de pila. Silencio
Silencio Over-optimizing with adjacency lists without need ¦ Adds unnecessary complejidad for a simple grid problem. Silencio

-...

### 6. Ir más allá

Si quieres apretar el rendimiento más adelante:
- Guardar el gráfico como una lista de adyacencia ** (vector de vectores) para saltar vuelos imposibles.
- Reducir el bucle interior a `O(m)` Donde `m` es el número de bordes, en lugar de `n2`.
- Esto da tiempo de `O(k * (n + m)) - todavía trivial para las limitaciones.

-...

### 7. Pensamientos finales

LeetCode 568 es un problema *state‐compression* DP que combina traversal gráfico con tabulación.
Al definir correctamente la `dp[city]` y iterando semanas atrás, transformamos un potencialmente desordenado "graph‐DP" en un algoritmo limpio, O(k · n2).

**¿Quieres brillar en tu próxima entrevista? * *
- Práctica explicando el estado del DP y la recurrencia.
- Escribe código conciso en tu idioma elegido.
- Casos de borde de prueba (sin vuelos, todos los vuelos).
- Mantenga una nota mental de los cambios de tiempo/espacio.

¡Feliz codificación, y que tus días de vacaciones siempre sean maximizados! 🌴🛫

-...

Si quieres discutir las variaciones de este problema o necesitas ayuda para pulir las respuestas de tu entrevista. ¡Feliz entrevista!