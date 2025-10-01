-...
Título: LeetCode 1891. Cintas de corte -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1891. Cintas de corte – El último problema de la entrevista de búsqueda binaria
*(LeetCode #1891)*

Silencio Idioma Silencio Código Silencio
Silencio...
Silencio **Java** Silencioso Haga clic para ampliar el texto correspondiente
*
* 1891. Cintas cortantes
* LeetCode – Medium
*
* Complejidad del tiempo : O(n · log(max(ribbons)))
* Complejidad espacial: O(1)
*/
Clase Solución {
int public maxLength(int[] cintas, int k) {
// 1. Encontrar la longitud máxima posible en el array
int maxLen = 0;
para (int r : cintas) maxLen = Math.max(max, r);

// 2. Búsqueda binaria en respuesta
int bajo = 1, alto = maxLen, mejor = 0;
mientras (bajo) = alto) {
int mid = bajo + (alto - bajo) / 2; // longitud del candidato

cnt largo = 0; // cuántas piezas podemos conseguir
para (int r : cintas) cnt += r / media; // división entero

si (cnt >= k) { // podemos producir al menos piezas k
mejor = mitad; // mediados es un candidato
bajo = medio + 1; // tratar de aumentar la longitud
. ♫ ... {
alta = media - 1; // necesita una longitud más pequeña
}
}
devolver mejor;
}
}
`` ' escrito/detalles titulado Silencio
Silencio **Python** Нелилилинилинаниениханиханиханиханниханиханихананиханиенинаниеннтентениханиянанияниенниенанананиянниянинниянияния нанниениянтиенанниенних ннниханиенниеннннниенаниеннниенаниениеннниениениениениенниеннннннниениенниениениенаннннннниенниенниеннннниени
"
1891. Cintas de corte – LeetCode
Complejidad del tiempo : O(n * log(max(ribbons)))
Complejidad espacial: O(1)
"

def maxLength(ribbons: list[int], k: int) - Conf int:
# Encontrar la longitud máxima de la cinta
max_len = max(ribbons)

# Búsqueda binaria en la respuesta
bajo, alto = 1, max_len
mejor = 0
mientras que bajo / = alto:
media = (bajo + alto) // 2

# Cuento cuántas piezas de longitud 'mid' podemos obtener
piezas = suma(r // mediados para r en cintas)

si piezas >= k:
mejor = mediados # mitad es una respuesta válida, tratar de aumentar
baja = media + 1
más:
alta = media - 1 # demasiadas piezas, longitud demasiado grande

mejor
`` `
`` ' escrito/detalles titulado Silencio
tención **C+** Silencioso Haga clic para ampliarlo
*
* 1891. Cintas cortantes – LeetCode
* Complejidad del tiempo : O(n · log(max(ribbons)))
* Complejidad espacial: O(1)
*/

#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maxLength(vector fielint círculo ribbons, int k) {
int maxLen = *max_element(ribbons.begin(), ribbons.end());

int bajo = 1, alto = maxLen, mejor = 0;
mientras (bajo) = alto) {
int mid = low + (high - low) / 2;

piezas largas = 0;
para (int r : cintas)
piezas += r / media;

si (piezas >= k) { // puede producir al menos piezas k
mejor = mitad;
baja = media + 1; // probar longitud más grande
. ♫ ... {
alta = media - 1; // necesita menor longitud
}
}
devolver mejor;
}
};
`` ' escrito/detalles titulado Silencio

-...

# 📝 Blog Post – “Cutting Ribbons: The Good, The Bad, and The Ugly”

■ **SEO Título**: Cutting Ribbons LeetCode 1891 – Estrategia de búsqueda binaria, Java/Python/C+++ Soluciones y consejos de entrevista
■ **Meta Descripción**: Master LeetCode 1891 (Cutting Ribbons) con una solución binaria clara en Java, Python y C++. Aprenda las trampas, trucos de rendimiento y cómo enfrentar este problema en su próxima entrevista de ingeniería de software.

-...

## 1. Introducción

**Cutting Ribbons** (LeetCode #1891) es un problema clásico *maximum‐value binaria-search* que prueba su capacidad de combinar dos conceptos fundamentales de CS:

1. **Greedy contando** – “Dada una longitud de la cinta `L`, ¿cuántas piezas podemos cortar? ”
2. **Binary search on answer** – “Find the largest `L` that satisfies the condition. ”

Si te estás preparando para una entrevista de ingeniería de software **, este problema es un problema básico. A menudo se le pregunta en *Google*, *Amazon*, y *Microsoft* entrevistas. Entender los enfoques buenos, malos y feos le ayudará **score high** en la ronda de codificación.

-...

## 2. Declaración de problemas (implificada)

Se te da:

- Un array entero `ribbons` donde `ribbons[i]` es la longitud de la cinta i‐th.
- Un entero.

Usted puede cortar cada cinta en cualquier número de segmentos *positivos enteros* (o dejarlo intacto). Descender las sobras.

** Objetivo**: Encontrar el entero máximo `x` tal que se puede cortar por lo menos `k` pedazos de longitud `x`.
Si no existe tal `x', regrese `0`.

-...

## 3. El Bien – Búsqueda binaria eficiente (O(n log m))

### 3.1. Intuición

- Si una longitud `x` funciona (puedes cortar 'k' pedazos), entonces cada longitud más pequeña también funciona.
- Si una longitud 'x' falla, cada longitud mayor falla también.

Así la función de viabilidad es *monotonic*: `true → true → ... → false → false`.
Este es un escenario de libro de texto para la búsqueda binaria en la respuesta.

### 3.2. Comprobación de viabilidad

``text
conteoPieces(L) = eva (ribbon / L) para todas las cintas
`` `

- `/` es la división entero → descarte automáticamente los restos.
- Inclina el número de piezas de longitud `L' de todas las cintas.

Si 'contraPieces(L) k` → `L` is *feasible*.
`` `

### 3.3. Procedimiento de búsqueda

1. **Espacio de búsqueda**: `[1, max(ribbons)]`.
(`max(ribbons)` es la respuesta más grande posible).
2. **Mid-point**: `mid = low + (high - low) / 2` (evita el desbordamiento).
3. **Actualizar punteros**:
- Si es factible → respuesta de la tienda, derecho de búsqueda (`bajo = medio + 1`).
- Else → búsqueda izquierda (`alta = media - 1`).

### 3.3. Complejidad

- **Tiempo**: Cada prueba de viabilidad es `O(n)`.
Búsqueda binaria necesita `O(log max(ribbons))' iterations → `O(n log m)`.
- **Espacio**: Sólo unas pocas variables enteros → `O(1)`.

### 3.4. Edge‐ Manejo de caso

- **k œ sum(ribbons)**: impossible → return `0`.
La búsqueda binaria producirá naturalmente `0` porque ninguna longitud puede producir suficientes piezas.
- Large `k'**: Use `long ́ / `long` para evitar el desbordamiento al resumir piezas.

-...

## 4. El mal – Naïve Linear o DP Solutions

TENIDO ANTERIOR TENIDO Tiempo TENIDO Espacio Por qué es malo
Silencio--------------------------------------
Silencio Brute force enumeration of all lengths (1...max) TEN O(n · max) TEN O(1) ANTE `max` can be `10^5`. Peor que `O(n log m)` para gran entrada. Silencio
tención Programación dinámica en longitudes de cinta ← O(n · max) Silencio O(max) Silencio DP es innecesario y añade memoria extra. Silencio
TENED ventana deslizante de dos puntos TENIDO O(n) TENIDO O(1) TENCIÓN No se aplica – el problema no se trata de sub-arrays. Silencio

Estos enfoques ingenuos *mejorar la propiedad monotónica del problema* y dar **90-plus por ciento** soluciones más lentas que el método de búsqueda binaria. En un entorno de entrevista, el entrevistador notará inmediatamente la ineficiencia.

-...

## 5. El Ugly - Recursión incorrecta / Optimización excesiva

Algunos candidatos escriben un “divide‐and-conquer” recurrente que *tries* para cortar cintas y retrocesos en el fracaso. Aunque interesante, es:

- **Afloja la recidiva profunda** (`k` up to `10^9` → stack overflow).
- ** Tiene el peor caso exponencial* si no se memoiza cuidadosamente.
- **Es difícil leer** – entrevistas recompensa * código limpio y legible*.

■ **Bottom line**: Póngase en el bucle de investigación codicioso y binario limpio. No hay necesidad de recursión o memoización elegante.

-...

## 6. Pitfalls comunes " Cómo evitarlos

Silencioso tóxico tóxico
Silencio------------
Silencio Usando `int` para resumir piezas → rebosadero Silencioso respuesta para gran `k`  durable Use `long long`/`long` para el contador. Silencio
← Errores desactivados por uno en los límites de búsqueda binaria ← Devoluciones `maxLen+1` o `0` incorrectamente ANTERITO Use `low <= high` y actualice `best` sólo sobre viabilidad. Silencio
Silencio No manejo `k √≥ totalLength` Retorno `maxLen` en lugar de `0` ← Verificación anticipada: si `k ' sum(ribbons)` → retorno `0`. Silencio
Silencio Recomputing `maxLen` en cada bucle ANTE SUPER `O(n)` por iteración TENIDO Compute una vez antes de la búsqueda binaria. Silencio

-...

## 7. Variación " Extensión de ideas

1. **Different Cut Cost** – Cada corte cuesta tiempo; minimizar el costo total manteniendo al menos piezas `k'. → Utilice *búsqueda binaria* + *función de coste*.
2. **Largo Piece No‐Integer** – Permitir longitudes fraccionadas → búsqueda binaria todavía pero utilizar *punto flotante* prueba de viabilidad.
3. **Multiple Queries** – Pre-compute prefix sumas para responder a varios valores de 'k' en O(log m) cada uno.

Saber adaptar el algoritmo del núcleo te da *flexibilidad* en entrevistas.

-...

## 8. Soluciones de muestra (Java / Python / C++)

(Ver la tabla de códigos arriba).
Cada solución sigue la misma estructura limpia:

``pseudo
maxLen = max(ribbons)
mejor = 0
mientras que bajo / = alto:
media = (bajo + alto) // 2
piezas = suma(ribbon // mid)
si piezas >= k:
mejor = mitad
baja = media + 1
más:
alta = media - 1
mejor
`` `

-...

## 9. Lista de verificación de la entrada

- [ ] Comprender *viabilidad monotónica* → búsqueda binaria.
- [ ] Use integer division (`/` in Python, `/` in Java/C++).
- [ ] Mantenga el contador en un tipo de 64 bits para evitar el desbordamiento.
- [ ] Computar el espacio de búsqueda 'alto' una vez (`max(ribbons)`).
Preferir 'mientras baja' = alta' sobre 'mientras baja' significaba alta' para claridad.
- [ ] Añádase el regreso anticipado `0` si `k ' totalPieces(1)` (opcional pero ordenado).

-...

## 10. Pensamientos finales

Cutting Ribbons es un **micro‐ecosystem** de las ideas de CS: codicia, monotónica, búsqueda binaria.
- **Bueno**: Investigación binaria en respuesta, viabilidad lineal de tiempo → rápido y escalable.
- **Bad**: Fuerza bruta lineal o exponencial → demasiado lento para pruebas grandes.
- **Ugly**: Recidiva ingenua → difícil de leer y mantener.

Maestro el patrón *bueno*, evita el *bad*, y mantén el *muy* lejos. Estarás listo para resolver este problema en cualquier entrevista de codificación y para impresionar a los gerentes de contratación que se preocupan por soluciones limpias y eficientes.

-...

■ **¿Quieres hacer más preguntas de entrevista de LeetCode? * *
■ Suscríbete a nuestro boletín semanal de desafío de codificación para problemas curados, preguntas de entrevistas y vídeos. 🚀

-..