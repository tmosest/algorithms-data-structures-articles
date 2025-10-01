-...
Título: LeetCode 3159. Encontrar Occurrences of an Element in an Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 3159 – Encontrar coincidencias de un elemento en un rayo
**Problema Tipo:** Medio Silencioso **Etiqueta:** Mapa de Hash ** Idiomas:** Java Silencio Python Silencio C++

-...

### 1. Resumen del problema

Te dan

TEN ANTERIOR ANTERIOR Descripción
Silencio...
TENIDO `nums` TENIENDO una serie de enteros (tamaño ≤ 105) Silencio
Silencioso `queries`  sometida a una serie de enteros (tamaño ≤ 105) Silencio
Silencioso `x`

Por cada una de las " consultas " debe devolver el índice** de la ocurrencia *k-th* de `x` en `nums`, donde `k = consultas[i].
Si `x` ocurre menos de 'k' veces, regrese `-1' para esa consulta.

■ *Ejemplo*
[1,3,1,7] ``, `queries = [1,3,2,4] ``, `x = 1` → `[0,-1,2,-1] `

-...

### 2. Enfoque directo

La observación central: sólo nos importan las posiciones de **x**.
Si podemos mapear rápidamente “k‐th ocurrencia de x” → “index in nums”, cada consulta se convierte en una búsqueda O(1).

La solución típica es:

1. **Primer paso – Construya el mapa* *
Escáner `nums`.
Cada vez que vemos `x`, aumenta un contador `cnt`.
Tienda `cnt → índice actual` en un mapa de hash.

2. **Paso Segundo – Respuestas preguntas**
Por cada `k ' en `queries ' , buscar `map[k]`.
Si no existe → `-1`.

Ambos pases son lineales, dando tiempo O(n + m) y espacio auxiliar O(n) (caso inferior cuando `x` ocurre en cada posición).

-...

### 3. Código (tres idiomas)

##### Java

``java
importar java.util*;

Solución de la clase pública {}
int[] sucesosOfElement(int[] nums, int[] consultas, int x) {
// Mapa: cuenta de ocurrencia índice
Mapa seleccionadoInteger, Integer título = nuevo HashMap fiel();
int count = 0;
para (int i = 0; i)
si (nums[i] == x) {
contar++;
map.put(count, i);
}
}

int[] ans = nuevo int[queries.length];
para (int i = 0; i) hice consultas.length; i++) {
ans[i] = map.getOrDefault(queries[i], -1);
}
devolver los ans;
}
}
`` `

#### Python

``python
def occurrencesOfElement(nums, consultas, x):
Occ = {}
cnt = 0
para idx, val en enumerate(nums):
si vale == x:
cnt += 1
occ[cnt] = idx

volver [occ.get(q, -1) para q en consultas]
`` `

###### C++

``cpp
Incluido el título
#include ■unordered_map Conf

usando std namespace;

Clase Solución {
public:
vector implicaciones de dominioDeElement(vector identificadoint limitada nums,
vector significando consultas
int x) {
unordered_map madeint, int confianza mp; // occurrence - índice
int cnt = 0;
para (int i = 0; i) ++i) {
si (nums[i] == x) {
++cnt;
mp[cnt] = i;
}
}

vector significar uns
ans.reserve(queries.size());
para (int k : consultas) {
auto = mp.find(k);
ans.push_back(it == mp.end() ? -1 : it- Confsegundo);
}
devolver los ans;
}
};
`` `

-...

### 4. Análisis de la complejidad

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencio Construir mapa Silencioso `O(n)` Silencio `O(n)` (caso inferior)
SilencioRespuestas consultas infligidas (no cuentan los arrays de salida)
Silencio **Total** Silencioso `O(n + m)` Silencio `O(n)` Silencio

- `n` - tamaño de `nums `
- " m " - tamaño de las `

Ambos pases son solo escaneos; no hay bucles anidados.

-...

### 5. Casos de borde " Pitfalls

← Situación Silencio Por qué importa
Silencio----------------
Silencio `x` nunca aparece Silencio Todas las consultas regresan `-1` Silencio Mapa permanecerá vacío - Lookup works fine Silencio
← Consultas contienen valores √° número de ocurrencias ¦ Debe devolver `-1` Silencio `getOrDefault` / `unordered_map::find` maneja it ¦
TENIDO Gran entrada (105) TENIDO Riesgo de TLE o MLE si se utiliza la recursión o O(n2) Silencio pases lineales, búsqueda constante en tiempo
Silencio `queries` unsorted Silencio No afecta la corrección Silencio No se necesita un manejo especial

-...

### 6. “Bueno, malo, feo” de esta solución

Silencio Silencio
Silencio------------Prince------
Silencio **Readability** Silencio Clear separation of concerns (build map, answer queries)
TENIDO **Performance** Silencio O(n+m) tiempo, óptimo para 105 TENIDO Utiliza un mapa de hash → O(n) espacio Silencio Si `x` ocurre en cada posición, memoria = O(n) pero todavía aceptable TEN
Silencioso **Scalability** Silencio Obras para grandes arrays Silencio Ninguno Silencio – Silencio
Silencio **Mantenibilidad** Silencio Fácil de extender (por ejemplo, índices de retorno para múltiples valores) Silencio Ninguno Silencio – Silencio
Silencio **Potential bug** Silencio Ninguno TENIDO Ninguno
Silencio **Parte del oído** Silencio Ninguno Silencioso Mapping indices correctamente

■ **Bottom line:** El enfoque hash‐map es *la forma más limpia y rápida de resolver este problema. Evitar estructuras de datos adicionales (por ejemplo, listas vinculadas) mantiene el código inclinado y fácil de entrevista.

-...

### 7. SEO‐Optimized Blog Post

-...

##### Title
#Crack LeetCode 3159 – Encontrar coincidencias de un elemento en un Array (Java, Python, C++)* *

#### Meta Descripción
Maestro LeetCode 3159 en segundos. Aprenda la solución hash‐map, vea código Java/Python/C+++, entienda el tiempo-espacio-offs y obtenga entrevistas. Perfecto para los ingenieros de software que preparan para las entrevistas de codificación.

-...

##### Introducción

Si estás cazando para un *nivel medio* Problema LeetCode que es perfecto para agudizar tus habilidades hash‐map, no busques más allá de **3159. Encontrar Occurrences of an Element in an Array**. Este problema prueba su capacidad de mapear ocurrencias a índices y responder preguntas en tiempo lineal – un escenario clásico de entrevista.

En este artículo:
- Rompe la declaración del problema en inglés.
- Presentar una solución limpia, O(n+m) con código Java, Python y C++.
- Discuta el “bueno, malo, feo” de este enfoque.
- Destacar por qué esta solución brilla en entrevistas de codificación del mundo real.

-...

#### Problema Recap

Dado:
- `nums` - una serie de enteros (hasta 100 000 elementos).
- `queries` - una serie de enteros donde cada valor es un rango (k-th ocurre).
- "x" - el valor objetivo.

Devuelve un array donde cada elemento es el índice de la ocurrencia k‐th de `x` en `nums`, o `-1` si no existe.

-...

##### ¿Por qué un mapa de Hash es la clave

La idea directa es caminar a través de 'nums' una vez y recordar cada posición donde 'x' aparece.
Una vez que tenemos ese mapeo “occurrence → index”, cada consulta es una búsqueda de diccionario constante.

Esta estrategia da:
- **Linear time** – sólo dos escaneos (`O(n+m)`).
- **Constant‐time consultas** – sin bucles anidados, sin búsqueda binaria sobre una lista de posiciones.
**Uso espacial escalable** – en la mayoría de una entrada por ocurrencia de `x`.

-...

#### Step‐by‐Step Walkthrough

1. *Construir el mapa*
``text
Conteo = 0
para mí en 0 ... nums.length-1:
si nums[i] == x:
Cuenta += 1
map[count] = i
`` `

2. *Responde a cada consulta*
``text
ans[i] = map.getOrDefault(queries[i], -1)
`` `

Eso es todo. Sin arrays adicionales, sin estructuras de datos complejas.

-...

#### Código Muestras

■ Ver las implementaciones *Java*, *Python* y *C++* en la sección “Code” arriba. Cada snippet es sólo unas pocas líneas de largo, lo que hace que la entrevista sea fácil y fácil de recordar.

-...

##### Bien, mal, Ugly

← Feature ← Buenas vidas
Silencio------------...
tención **Readability** Silencio claro, conciso lógica tención Ninguno ←
Silencio **Hablar** Silencio O(n+m) – óptimo para 105 Silencio Ninguno Silencio – Silencio
Silencio **Espacio** Silencioso O(n) el peor de los casos – todavía está bien para 105 Silencioso mapa de Hash sobre la cabeza – Silencio
Silencio **Mantenibilidad** tención Fácil de retocar para las variaciones
Silencio **Entreview‐fit** Silencio No hay caldera, comentarios limpios

■ **Tip de Interview:** Hable a través de la idea de mapeo antes de escribir código. Muestra al entrevistador que usted entiende la estructura de datos subyacente, no sólo el truco "código-it-up".

-...

#### Common Gotchas to avoid

- **Missing `x` en `nums`** - el mapa permanece vacío, pero las apariencias todavía vuelven `-1`.
- **Las preguntas más grandes que la ocurrencia real cuentan** – use `getOrDefault` / `unordered_map::find` para proteger.
- **Soplado de memoria** - si `x` aparece en cada elemento, el mapa tiene 100 000 entradas; todavía bien dentro de las limitaciones típicas de la entrevista.

-...

###### Takeaway

La solución hash‐map es la respuesta *canónica* a LeetCode 3159. Es conciso, rápido y demuestra el dominio de las búsquedas de diccionarios – exactamente lo que los entrevistadores quieren ver.
Practique hasta que pueda escribirlo en una línea (Java/Python) o dos bucles (C+++), entonces estará listo para as esto y muchas otras preguntas de hash-map de nivel medio.

-...

#### ¿Quieres aprovechar tus habilidades de entrevista?

- Construir un parque infantil **LeetCode** y practicar 5-10 problemas al día.
- Programa de pares con un amigo o usa una plataforma como **EntreviewBit** para entrevistas de mock.
- Compartir esta solución en LinkedIn - la comunidad ama el código limpio!

¡Feliz codificación, y que sus índices siempre apuntan al éxito! 🚀

-...

*No dude en dejar un comentario si tiene preguntas o quiere discutir otras estrategias de LeetCode! *