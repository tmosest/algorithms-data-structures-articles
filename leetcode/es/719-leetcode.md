-...
Título: LeetCode 719. Encontrar K-th menor distancia de par -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Encontrar K‐th Distancia más pequeña - LeetCode 719
*Hard* DistanciaPair(int[] nums, int k) `

■ ** Objetivo** – Devuelve la diferencia absoluta más pequeña entre los dos elementos en los años.
■ ** Entrada** – `nums` (length 2 ≤ n ≤ 104, 0 ≤ nums[i] ≤ 106), `k` (1 ≤ k ≤ n n‐1)/2).
■ ** Salida** – La distancia de par más pequeña.

Las secciones siguientes abarcan:

1. Resumen de problemas
2. El algoritmo óptimo (búsqueda binaria sobre distancia + ventana corredera)
3. Aplicación en **Java**, **Python 3**, **C++**
4. Casos de borde " trampas comunes
5. Bien, mal, Ugly – una lista de verificación rápida de revisión de códigos
6. SEO-friendly para los cazadores de trabajo

-...

## 1. Panorama general de los problemas

La forma bruta-fuerza generaría todas las distancias par \(\binom{n}\) , ordenarlas, y devolver el elemento \(k\)‐th.
*Time* – \(O(n^2 \log n)\) → demasiado lento para \(n=104\).
*Pace* – \(O(n^2)\) para almacenar todas las distancias → imposible.

Necesitamos una solución **\(O(n \log M)\)**, donde \(M\) es la distancia máxima posible (\(\max(nums)-\min(nums)\).
El truco es **buscar en la respuesta** (la distancia) y contar cuántos pares tienen una distancia ≤ mediados.
Si ese recuento es, necesitamos una distancia mayor; de lo contrario podemos probar uno más pequeño.

-...

## 2. Enfoque óptimo – búsqueda binaria + dos puntos

1. **Sort** el array – \(O(n \log n)\).
2. Búsqueda binaria en la distancia `d` en el rango `[0, max‐min]`.
3. Para un candidato `mid`, cuente parejas `(i, j)` con `nums[j] - nums[i] ≤ mid` utilizando una ventana deslizante (dos puntos).
* `izquierda' comienza a las 0.
* Por cada `derecha' de 0 a n-1, incremento `izquierda' mientras que el ancho de la ventana excede `mid`.
* All indices between `left` and `right-1` form valid couples with `right`. Añadir `derecha' a la cuenta.
* Esto es lineal, \(O(n)\).
4. Ajuste los límites de búsqueda binaria basados en el conteo.
5. Devuelve la distancia más pequeña cuyo conteo ≥ k.

**Por qué funciona* *
- El array está ordenados, por lo que cualquier par válido con distancia ≤ `mid` es contiguo en el orden ordenado.
- La ventana corredera cuenta cada par exactamente una vez.
- La búsqueda binaria garantiza que convergemos a la distancia mínima que satisface la condición.

-...

## 3. Aplicación del Código

### 3.1 Java

``java
importa java.util. Arrays;

Solución de la clase pública {}
público más pequeño DistanciaPair(int[] nums, int k) {
Arrays.sort(nums); // 1. sort
int bajo = 0; // mínima distancia posible
int high = nums[nums.length - 1] - nums[0]; // maximal possible distance

mientras (bajo)
int mid = low + (high - low) / 2;
cuenta larga = cuentaPairs(nums, mid); // 2. Contar pares

si (contacto) k) { // necesita mayor distancia
baja = media + 1;
} más { / / media es suficiente
alto = medio;
}
}
retorno bajo; // distancia mínima con con cuenta k
}

// cuenta lineal de dos puntos (usuarios largos para evitar el desbordamiento)
cuenta larga privadaPairs(int[] nums, int limit) {}
cnt largo = 0;
int left = 0;
para (derecho = 0; derecho) {}
mientras (nums[right] - nums[left]
izquierda++;
}
cnt += derecha - izquierda; // pares (izquierda ... derecha-1, derecha)
}
cnt de retorno;
}
}
`` `

■ ¿Por qué 64 bits? * *
■ El número de pares puede ser hasta \(\frac{10^4 \times 9999}{2} \approx 5\times10^7\), todavía encaja en `int`.
■ Utilizar `long` es una opción defensiva cuando se extiende a más grande `n`.

-...

#### 3.2 Python 3

``python
Solución de clase:
def más pequeño DistanciaPair(self, nums: list[int], k: int) - título int:
nums.sort() # 1. sorteo
bajo, alto = 0, nums[-1] - nums[0] # rango de búsqueda

mientras que bajo
media = (bajo + alto) // 2
si auto.count_pairs(nums, mid)
baja = media + 1
# Mid works
alta = media
Regreso bajo

def count_pairs(self, nums: list[int], limit: int) - título int:
""Linear cuenta de dos puntos de pares con la distancia "Directo=""
izquierda, cnt = 0, 0
por derecho, val in enumerate(nums):
val - nums[left] límite:
izquierda += 1
cnt += derecha - izquierda
retorno cnt
`` `

-...

### 3.3 C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
más pequeño DistanciaPair(vector identificadoint ánimos nums, int k) {
(nums.begin(), nums.end()); // 1. sort
int low = 0;
int high = nums.back() - nums.front(); // 2. límites de búsqueda

mientras (bajo)
int mid = low + (high - low) / 2;
cnt largo largo = cuenta Parejas(nums, mid); // 3. Contar pares

si
baja = media + 1;
. ♫ ... {
alto = medio;
}
}
retorno bajo // 4. Respuesta
}

privado:
// Conteo lineal de dos puntos
largos largos conteoPairs(cont vector conectadoint estrechos nums, límite int) {}
cnt largo = 0;
int left = 0;
para (derecho = 0; derecho)
mientras (nums[right] - nums[left]
++izquierda;
}
cnt += derecha - izquierda; // all i in [left, right-1] form a valid pair with right
}
cnt de retorno;
}
};
`` `

■ Las tres soluciones tienen la misma complejidad de tiempo/espacio:
■ **Hora**: \(O(n \log n + n \log M)\)
■ **Espacio**: \(O(1)\) además del array de entrada (el tipo está en el lugar).

-...

## 4. Casos de borde " Pitfalls comunes

Silencioso Qué hacer para comprobar Silencio Por qué importa
Silencio----------------------------- La vida eterna
← Números Duplicados Silencio `low` comienza a 0; ConteoPairs devolverá muchos pares de cero distancia. El algoritmo todavía encuentra la distancia no negativo más pequeña. Silencio
Silencio Muy grande `k` (cerca a \(n(n-1)/2\) Silencio La búsqueda binaria termina con `bajo == alto == máx-min`. Silencio Asegurar no off-by‐one: `cuenta ' hecho k` → `low = mid + 1`. Silencio
Silencio Array ya ordenados Silencio Ordenar es obligatorio; de lo contrario la lógica de la ventana deslizante falla. tención Recuerde llamar `Arrays.sort` / `sort(nums)` antes de la búsqueda binaria. Silencio
Silencio Overflow in pair count tención Uso `long` / `long ́ para el conteo. Silencio `n(n-1)/2` puede exceder `int` cuando n = 104. Silencio
¿Números negativos? El problema de la vida garantiza no negativo, pero si se extiende a los negativos, `nums[right] - nums[left]` todavía funciona porque la matriz está ordenada. No es necesario cambiar. Silencio

-...

## 5. Bueno, malo, ugly – Quick Code‐Review Checklist

Silencio Silencio
Silencio------------Prince------
Silencio **Sorting** Silencio Usos incorporados eficientemente (`Arrays.sort` / `sort`) Silencio Olvidando ordenar rompe el algoritmo Silencio Sobre-ordenando una enorme corriente de datos (por ejemplo, utilizando `Collections.sort` en una lista de objetos) Silencioso
Silencio **Binary search bounds** ← Correct `low = 0`, `high = max‐min` ¦ Usando `high = max(nums)` en lugar de `max‐min` infla el espacio de búsqueda  Off‐by: `int mid = (low + high)/2` sin prevenir el desbordamiento  durable
Silencio **Count function** tención Linear two-pointer, no extra memory ← Mis-incrementing `left` orOlvidting `right-left` ANTE Solución pares dos veces o pares desaparecidos (por ejemplo, utilizando `right-left+1`) Silencio
tención **Retorno de valor** Silencio `bajo ' después del bucle - distancia mínima con conteo ≥ k  duración Devolviendo `alta ' incorrectamente  durable Devolviendo `mid ' dentro del bucle (stops too early)
Silencio **Tipo de seguridad** Silencio Uso `long`/`long' para cuenta de pares TENIDO Asumiendo que `int` es suficiente → rebosa de enteros ANTE Conversiones innecesarias `no firmadas ` (en el código C++)

-...

## 6. Alternativas & Por qué se escoge este

Silencio tóxico Complejidad
Silencio--------------------------...
Silencio **K‐th order statistic + min‐heap** Silencio \(O(n^2 \log k)\) Silencio Obras para pequeños `n` Silencio Todavía cuadrático
TEN **FFT + matriz de frecuencia** TENED \(O(M \log M)\) TENSIÓN Puede manejar muy grande `n` si los valores están vinculados ANTE Requiere bibliotecas de convolución, memoria pesada TEN
Silencio **Binary search + binaria search per element** Silencio \(O(n \log n \log M)\) Silencio Simpler para el código para entrevistadores Silencio ligeramente más lento que el recuento lineal

Para LeetCode 719 el método binario‐search‐over‐answer es la solución *de facto*.

-...

## 7. SEO‐Friendly Take‐Away – What Hiring Managers Love

**Keyword**: *K‐th Smallest Pair Distancia LeetCode 719*
- **Descripción** (conjunto155 chars)
■ “Hard LeetCode 719 solución – búsqueda binaria a distancia + ventana corredera de dos puntos. O(n log M) código en Java, Python, C++. Entrevista prep y guía de búsqueda de trabajo. ”
- *Headers*
- `# Encontrar K-th menor distancia de par – LeetCode 719`
- ## Algoritmo óptimo: Búsqueda binaria + Ventana deslizante
- ## Java / Python / C++ Código `
- ## Bien, mal, ugly – Lista de verificación del código de entrevista `

■ **Por qué importa** – Búsqueda de “LeetCode 719” en busca de candidatos que puedan resolver problemas difíciles de procesar.
■ Incluya las palabras clave anteriores en su título de blog, primer párrafo, y meta-descripción para clasificar más alto en consultas de búsqueda de empleo.

-...

### 🎯 Palabras finales

- El patrón de búsqueda **binaria sobre la respuesta** es una poderosa herramienta para los problemas "find‐kth-smallest".
- Mantenga su **count** función lineal; la ventana corredera es tanto *fast* como *clean*.
- No te olvides de usar **`long`** para la cuenta de pareja.
- El algoritmo funciona cómodamente para las máximas restricciones (104 elementos).

¡Suelta este post en su cartera, retoque los comentarios para su estilo y golpee “Publicar”! Buena suerte en el piso de la entrevista.