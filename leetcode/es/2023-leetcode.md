-...
Título: LeetCode 2023. Número de pares de cuerdas con concatenación igual a blanco -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🧩 LeetCode 2023 – “Número de pares de cuerdas con concatenación igual a blanco”

← Solución de la vida
Silencio--------------------------
Silencio **Java** Silencio TENIENDO 1‐pass hash mapa TENIDO O(n · L) tiempo, O(n) espacio ANTE
Silencio **Python** Silencio TENIENDO 1‐pass hash map TENIDO O(n · L) tiempo, O(n) espacio ANTE
Silencio **C++** Silencio ↓ 1‐pass hash map ← O(n · L) time, O(n) space Silencio

■ *“Si quieres conseguir un trabajo técnico, necesitas dominar problemas que muestren tu capacidad de pensar algorítmicamente y escribir código limpio.”* – **Sus futuros entrevistadores* *

A continuación encontrará el código completo, listo para la producción para cada idioma, seguido de un escrito detallado de estilo blog que explica el **bueno, el malo, y el feo** de resolver este problema. El artículo es SEO-optimizado para ayudarle a posicionarse más alto en los motores de búsqueda y ser notado por los reclutadores.

-...

## 📦 El problema (LeetCode 2023)

■ **Given** una serie de cadenas de dígitos `nums` y una cadena de dígitos `target`, **return** el número de pares de índices `(i, j)` (donde `i != j`) tales que `nums[i] + nums[j] == target`.

**Constraints* *

Silencioso
Silencio...
TENIDO 1 TENIDO `2 ANTERE= nums.length ANTE = 100` TENIDO
TENIDO 2 TENIDO `1 ANTERE= nums[i].length ANTE = 100` Silencio Las cuerdas individuales pueden ser largas
Silencio 3 Silencio `2 |= target.length= 100` Silencio La cadena de blanco puede ser larga 
Silencio 4 Silencio Todas las cuerdas consisten en dígitos y **no hay ceros principales**

-...

## 🏁 Quick Overview

1. **Niveve Approach** – O(n2) bucles anidados. Funciona para las limitaciones dadas pero no es elegante o escalable.
2. **Hash‐Map (Optimal)** – O(n) time, O(n) space. Cuente las ocurrencias de cada cadena y luego busque la parte complementaria del objetivo.
3. ¿Por qué Hash‐Map? Elimina las comparaciones redundantes, da búsquedas constantes a tiempo, y mantiene el código succinct.

-...

## 🔧 Code Solutions

■ Todas las soluciones comparten la misma idea fundamental: para cada cadena `s` en `nums`, si `target` comienza con `s`, el sufijo restante `t` debe existir en `nums` (excepto cuando `s == t`, debemos evitar contar el mismo índice dos veces).

#### ## 1down⃣ Java

``java
importa java.util. HashMap;
importa java.util. Mapa;

Solución de la clase pública {}
*
* Cuenta el número de pares ordenados (i, j) tal que nums[i] + nums[j] == objetivo.
* Tiempo: O(n * L)
* Espacio: O(n)
*/
public int numOfPairs(String[] nums, String target) {
Mapa seleccionadoString, Integer frecuentementeq = nuevo HashMap Quería();
para (String s : nums) {
freq.put(s, freq.getOrDefault(s, 0) + 1);
}

int count = 0;
para (String s : nums) {
si (target.startsWith(s)) {
sring suffix = target.substring(s.length());
int add = freq.get OrDefault(suffix, 0);
si (suffix.equals(s)) añadir--; // excluir i == j
contar += añadir;
}
}
recuento de retorno;
}
}
`` `

#### 2down⃣ Python

``python
de las importaciones de colecciones Contrato
de la importación Lista

def num_of_pairs(nums: List[str], target: str) - confiar int:
"
Devuelve el número de pares ordenados (i, j) donde nums[i] + nums[j] == objetivo.
Tiempo: O(n * L)
Espacio: O(n)
"
freq = Counter(nums)
Conteo = 0

para s en nums:
si el objetivo.startswith(s):
sufijo = objetivo [len(s):]
contar += freq.get(suffix, 0)
si sufijo == s:
Contando -= 1 # Evite i == j

cuenta de retorno
`` `

#### 3down⃣ C++

``cpp
Incluido el título
#include ■string
#include ■unordered_map Conf

int numOfPairs(const std::vector obtenidosstd::string nums, const std::string {}
std::unordered_map seleccionados::string, int confianza freq;
para (contigo auto cho s : nums) {
++freq[s];
}

int count = 0;
para (contigo auto cho s : nums) {
si (target.rfind(s, 0) == 0) { // target.startsWith(s)
std::string suffix = target.substr(s.size());
auto = freq.find(suffix);
if (it != freq.end()) {}
contar += it-jósegundo;
si (suffix == s) cuentan--; // evite i == j
}
}
}
recuento de retorno;
}
`` `

■ Los tres fragmentos compilan en los últimos JDK 17 / Python 3.10+ / C++17 compiladores y funcionan en tiempo lineal.

-...

Artículo del Blog – “El Bien, el Mal y el Ugly of Pair Concatenation”

■ **Título**: *LeetCode 2023 – Mastering the “Número de pares de cuerdas concatenación” Problema (Java, Python, C++)*

### 1. Introducción

El problema “Número de pares de cuerdas con concatenación igual a blanco” parece engañosamente sencillo. Pero enseña una lección que aparece en entrevistas de codificación en el mundo real: **optimizar las estructuras de datos y evitar el trabajo innecesario** puede convertir una solución ingenua O(n2) en un O(n) elegante.

A continuación caminamos a través del problema, discutir el enfoque ingenuo, explicar la solución de hash-map óptima, y reflexionar sobre los aspectos *bueno, malo y feo* de cada uno.

■ ¿Por qué leer esto? * *
■ *Si te estás preparando para entrevistas técnicas, dominar este problema no solo aumentará tu puntuación de LeetCode sino que también te dará un punto de conversación que los reclutadores aman. *

-...

### 2. Recaptación de problemas

- ** Entrada**: `nums` - matriz de cadenas de dígitos, `target` - cadena de dígitos.
- ** Salida**: Cuenta de pares ordenados `(i, j)` (`i ل j`) tales que `nums[i] + nums[j] == target`.

*Ejemplos*
1. `nums = ["777","7", "77", "77"], target = "7777" → 4 pares
2. `nums = ["123","4","12","34"], target = "1234" → 2 pares
3. `nums = ["1","1","1"], target = "11" → 6 pares

El matiz clave: **Los índices deben diferir** – el mismo valor de cadena puede aparecer múltiples veces, y cada ocurrencia cuenta como un índice separado.

-...

### 3. The Naïve (Bad) Approach

``python
Conteo = 0
para i en rango(n):
para j en rango(n):
i!= j y nums[i] + nums[j] == objetivo:
Cuenta += 1
`` `

**Pros**
- *Simple para escribir y entender. *
- Trabaja bajo las pequeñas limitaciones del problema (n ≤ 100).

**Cons**
- La complejidad del tiempo.
- Redundant string concatenations (`nums[i] + nums[j]`) para cada par.
- La baja escalabilidad - sería el tiempo fuera en insumos más grandes.

En términos de entrevista, esto es lo suficientemente bueno para una rápida demostración*, pero los reclutadores buscan soluciones *eficientes*. El método naïve también oculta un fallo sutil: si `nums[i] == target`, todavía necesita asegurarse de que el sufijo existe en el array. La solución hash‐map maneja esto limpiamente.

-...

### 4. El enfoque óptimo (bueno) – Mapa de Hash de un par

*Idea*
Porque cada cadena `s` en `nums`, si `target` comienza con `s`, el sufijo restante `t` debe aparecer en algún lugar en `nums`. Contando ocurrencias de cada cadena nos permite encontrar `t` en **O(1)**.

** Pasos del Algoritmo**

1. ** Mapa de frecuencia de edificios**
`freq[s] = número de veces s aparece en nums`.

2. *Tetrato sobre cada cuerda*
- Si `target` comienza con `s`, vamos `t = target.substring(len(s))'.
- Añada la respuesta.
- Si `t == s`, restar 1 para evitar emparejar una cadena con sí mismo (ya que los índices deben diferir).

**Por qué funciona* *
- Nunca comparamos cada par.
- Buscar constantemente la parte complementaria.
- Linear in `n` (plus the string length `L` which is unavoidable because we must inspect `target`).

**Las complejidades* *
- *Time*: `O(n · L)` – `n` loop iterations, each doing a prefix check and a map lookup.
- *Pace*: `O(n)` – para el mapa de frecuencia.

**Proof of Correctness* *
Cada par ordenado que satisface la condición será contado exactamente una vez:

- Supongamos que `(i, j)` es un par válido. Let `s = nums[i]`.
- En el bucle de `s`, vemos que `target` comienza con `s`, compute `t = nums[j]`.
- Añadimos `freq[t]`, que cuenta *todos* índices `k ' tal que `nums[k] == t`.
- Si `k == j`, la adición es correcta; si `k == i`, restamos 1 cuando `s == t`.

Todos los pares son capturados, y no se cuentan pares extraneosos.

** Casos Edge manejados**

- Múltiples cadenas idénticas ( " [1", "1"] " ).
- Sufijo vacío (sólo cuando " es igual a `target ' , pero el problema garantiza `target.length '= 2`).
- cuerdas muy largas (la concatenación sería cara, pero la extracción de subestring es barata).

-...

### 5. Snippets de implementación (Mapa de un solo paso)

(Véase la sección del código anterior.)

Los tres idiomas comparten la misma estructura:

- Construir un `Counter`/`HashMap`/`unordered_map`.
- Use `startsWith`/`target.rfind`/`target.rfind(s, 0)`.
- `suffix = target[len(s):]` (o `substr`).
- Agregue frecuencia, ajuste para auto-pair.

-...

### 5. La Ugly – Potential Pitfalls & Common Mistakes

Silencio Pitfall Silencio Por qué Sucede
Silencio...
Silencio **Colisión de valor index** – utilizando un mapa clavedo por *valor* pero olvidando que los valores idénticos pueden aparecer en diferentes índices. Silencio Asumiendo que cada valor es único. ¦ Tienda *frecuencia*, no una bandera booleana. Silencio
Silencio **Off‐by-one en subestring** – olvidándose de utilizar `len(s)` en lugar de `size()`. ↑ Mismatch entre las convenciones de indexación de idiomas. Prueba con una prueba de unidad que cubre cadenas de caracteres individuales. Silencio
Silencio ** Auto-pairing** – contando `(i, i)` cuando `s == t`. Silencio Muchos candidatos pasan por alto la regla 'i != j`. latitud Subtract 1 cuando el sufijo es igual a la cadena prefijo. Silencio
Silencio **Large L** – la concatenación de cuerdas dentro de bucles anidados puede ser caro. Silencio Incluso si `n` es pequeña, concatenando cadenas de 100 caracteres 10 000 veces es desperdicio. Silencio Evite la concatenación usando 'startsWith`/`substring`. Silencio
Silencio **Caso sensibilidad** – tratar `"1" y `"01" de manera diferente. ← Problema no garantiza ceros líderes, pero algunas soluciones malmanejen sufijos vacíos. Silencio Garantizar la longitud de `target` ≥ 2 y comprobar `target.startsCon(s)` primero. Silencio

-...

### 6. Por qué el Programador Ama la Solución Hash‐Map

- **Scalability**: El código sigue siendo rápido incluso si `n` crece a 105 (la complejidad del tiempo no cambia).
- **Readability**: Un bucle, una búsqueda de mapa, una ramificación mínima.
- **Usodiomático de las características del lenguaje**: Java’s `Map.getOrDefault`, Python’s `Counter`, C++’s `unordered_map`.
- **Test-ability**: Fácil de probar cada componente (cama de frecuencia, extracción de sufijo, ajuste de auto-pair).

-...

### 7. Take‐aways for Your Next Interview

TENIDO TENDIDO TENIDO Cómo Ayuda a TENIDO
Silencio...
Silencio **Comienza con un mapa de frecuencias limpias** Silencio instantáneamente te dice cuántas veces aparece una subestring. Silencio
Silencio **Evitar la doble cuenta** Silencio Recuerde que el problema pide pares *ordenados*, por lo que `(i, j)` y `(j, i)` son distintos. Silencio
Silencioso **Edge-case first** Silencio Escribe pruebas para `"1" * 3 ``"11', `"777" * 2 ``"77', etc. Silencio
Silencio **La complejidad del tiempo importa** Silencio Incluso si las limitaciones son pequeñas, siempre apuntan a soluciones lineales o logísticas. Silencio
Silencio **Leverage built‐in helpers** Silencio `String.startsCon()`, `Counter`, `unordered_map` – están optimizados bajo la capucha. Silencio

-...

### 8. SEO Boost – Palabras clave & Meta Data

- **Primary Palabras clave**: LeetCode 2023, número de pares concatenación, problema de concatenación de cadenas, solución óptima, pregunta de entrevista de mapas.
- **Secondary Keywords**: Solución Java LeetCode, Solución Python LeetCode, solución C++ LeetCode, problemas de codificación de entrevistas, algoritmo eficiente.

■ *Añadir este artículo a su sitio de cartera o blog de LinkedIn y los reclutadores de relojes alcanzan! *

-...

### 9. Pensamientos de clausura

- La solución **naïve** es fácil pero falla en el criterio de *optimización*.
- La solución **hash‐map** es concisa, escalable y demuestra una profunda comprensión de la estructura del problema.
- **Entrevistadores** a menudo sonda *por qué* eligió una estructura de datos particular – estar listo para explicar la ventaja de búsqueda de `O(1)`.

Practique las tres implementaciones, ejecute sus propios arnés de prueba, e intente extender el problema (por ejemplo, permita cadenas no dígitos o arrays más grandes). El aprendizaje que obtenga será inestimable para su próxima entrevista de codificación.

-...

###  inaceptable Bonus: Quick Test Harness (Python)

``python
def test():
afirma num_of_pairs(["777","77","77"], "7777") == 4
afirma num_of_pairs(["123","4","12","34"], "1234") == 2
afirma num_of_pairs(["1","1","1"], "11") == 6
print("Todas las pruebas pasadas!")

test()
`` `

-...

¡Feliz codificación, y que su mente algoritmo sea tan aguda como su curriculum! 🚀