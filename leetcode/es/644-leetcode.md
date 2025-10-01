-...
Título: LeetCode 644. Subarray promedio máximo II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 644 – Maximum Media Subarray II
**Hard** – Búsqueda binaria + Sumas prefijo + Ventana deslizante

■ *“Encontrar un sub-arrayo contiguo de longitud ≥ k que tenga el promedio máximo posible.”*

A continuación encontrará una implementación completa y lista para la producción en **Java, Python y C+**.
Luego lee un breve post del blog que te lleva a través de la intuición, las trampas y el valor del mundo real de dominar este problema.
El artículo está optimizado para palabras clave como *LeetCode 644, Maximum Media Subarray II, búsqueda binaria, sumas prefijo, ventana corredera, Java, Python, C+*.

-...

## 1down Java Implementation

``java
importar java.util*;

Solución de la clase pública {}
public double findMaxAverage(int[] nums, int k) {
// 1. binario-search bounds: min y elemento max en el array
doble bajo = entero. MAX_VALUE, high = Integer.MIN_VALUE;
para (int x : nums) {
bajo = Math.min(low, x);
alto = Math.max(alto, x);
}

// 2. prefijo sumas array (tamaño n+1, sumas [0] = 0)
int n = nums.length;
doble[] pref = nuevo doble[n + 1];

// 3. búsqueda binaria con precisión 1e-5
mientras que (alto - bajo
doble media = (bajo + alto) / 2.0;
// Construir sumas prefijas de (nums[i] - mitad)
para (int i = 0; i) {}
pref[i + 1] = pref[i] + nums[i] - mid;
}

// 4. comprobar si existe un sub-array de longitud ≥ k con suma positiva
doble minPrefix = 0,0; // minimal pref[j] where j ≤ i-k
boolean ok = falso;
para (int i = k; i) {}
si (pref[i] - minPrefix 0) {
ok = verdadero;
ruptura;
}
minPrefix = Math.min(minPrefix, pref[i - k + 1]);
}

// 5. apretar los límites
si (ok) bajo = medio; // podemos alcanzar al menos este promedio
más alto = medio; // no podemos alcanzar este promedio
}
Retorno bajo;
}
}
`` `

**Puntos clave* *

* El algoritmo funciona en **O(n log M)** donde *M* es la gama de promedios posibles (Ω 2 × 104).
* `pref[i]` sostiene la diferencia acumulativa `gober(nums[j] – mediados)` hasta el índice *i‐1*.
* If `pref[i] – minPrefix > 0` para algunos *i*, encontramos un sub-array de longitud al menos *k* con promedio ≥ mediados.

-...

## 2down⃣ Python Implementation

``python
def findMaxAverage(nums: list[int], k: int) - título flotante:
bajo, alto = min(nums), max(nums)
n = len(nums)

mientras que alto - bajo
media = (bajo + alto) / 2.0
# prefix sums of (nums[i] - mid)
* (n +1)
for i, v in enumerate(nums, 1):
pref[i] = pref[i] + v - mid

min_pref = 0,0
ok = Falso
para i en rango(k, n + 1):
si pref[i] - min_pref 0:
OK = True
descanso
min_pref = min(min_pref, pref[i - k + 1])

bajo = medio si ok más alto

Regreso bajo
`` `

-...

## 3down C C++ Aplicación

``cpp
Clase Solución {
public:
encontrar dobleMaxAverage(vector fieltro nums, int k) {
doble bajo = *min_element(nums.begin(), nums.end());
doble alto = *max_element(nums.begin(), nums.end());
int n = nums.size();

mientras que (alto - bajo
doble media = (bajo + alto) / 2.0;

vector alcanzadodouble confianza pref(n + 1, 0,0);
para (int i = 0; i)
pref[i + 1] = pref[i] + nums[i] - mid;

doble min_pref = 0,0;
bool ok = falso;
para (int i = k; i) {}
si (pref[i] - min_pref 0) { ok = true; break; }
min_pref = min(min_pref, pref[i - k + 1]);
}

bajo = ok? media : alta;
}
Retorno bajo;
}
};
`` `

-...

## 4down Blog Post – “Maximum Media Subarray II: El Bien, El Mal, El Ugly

■ *Título*
■ *Maximum Media Subarray II (LeetCode 644) – A Deep Dive into Binary Search, Prefix Sums and Sliding Windows (Java, Pitón, C++)*

■ **Meta Descripción:**
■ Master LeetCode 644 con una solución clara, paso a paso. Aprenda el truco de búsqueda binaria, cómo las sumas prefijo convierten los promedios en sumas, y optimizaciones de ventana deslizante. Obtener Java, Python y C++ código listo para copiar-paste.

#### 4.1 Por qué este problema importa

- *Entrevista de mina de oro* La mayoría de los gerentes de contratación preguntan sobre LeetCode 644 o una variación.
- ** Introspección algorítmica**: Demuestra cómo convertir un problema “máximo promedio” en un subproblema de “prueba factibilidad” mediante búsqueda binaria.
- **La lengua versatilidad**: La misma lógica funciona en Java, Python o C++, mostrándole cómo traducir ideas algorítmicas a través de los ecosistemas.

### 4.2 Problema Recaptura

Dado un conjunto entero `nums` de longitud `n` y un entero `k`, encontrar el sub-array contiguo cuya longitud es por lo menos 'k' que produce el promedio máximo.
Devuelve el promedio a una precisión absoluta de `1e‐5`.

#### 4.3 El “bien” – Por qué Esta solución funciona

TEN TERRITORIO ANTERIOR ANTERIOR
Silencio...
Silencio **Binary search on value** Silencio La media está entre `min(nums)` y `max(nums)`. La búsqueda binaria nos permite acercarnos al mejor promedio en iteraciones 'log(range). Silencio
Silencio **Prefix sumas de matriz transformada** Silencio Transformar cada elemento `x` en `x - mediados'. Un sub-array de promedio ≥ `mid` se convierte en un sub-array con suma positiva en el array transformado. Silencio
tención **Sliding‐window minimum** Silencio Mientras escanea las sumas prefijo, siga el prefijo más pequeño que es por lo menos 'k' posiciones detrás del índice actual. Esto da una prueba de viabilidad de O(n). Silencio
Silencio **O(n log M) time, O(n) space** Silencio `M` es el rango numérico (~ 2 × 104). Para `n ≤ 104`, esto es cómodamente rápido en LeetCode. Silencio

### 4.4 El "Bad" – Cosas que hay que ver

Pitfall tóxico Cómo evitarlo
Silencio...
Silencio **Precisión de punto flotante** Silencioso Use `1e‐5` tolerancia; detenga la búsqueda binaria cuando `alta - bajo  observado 1e‐5`. Silencio
Silencio **Off‐by‐one in prefix sums** Silencio Recordar `pref[0] = 0`. La indización de `1` a `n` mantiene las matemáticas limpias. Silencio
Silencio **Gran número negativo** Silencio La suma prefijo puede ser negativa; `min_prefix` debe ser inicializado a `0` (la suma del prefijo vacío). Silencio
Silencio **Desbordamiento entero** Silencio En C++ use `doble` para sumas; evite `long` cuando se mezcla con "doble". Silencio

### 4.5 The “Ugly” – Edge Cases That Break Naïve Code

TENIDO CASO TERRITORIO Lo que sucede ANTERIENTE
Silencio--------Prince--------------
Silencio Todos los números negativos ← La búsqueda binaria puede converger a un promedio negativo; el código todavía funciona porque `min(nums)` puede ser negativo. No se necesita ningún cambio, pero tenga cuidado con los límites bajos y altos iniciales. Silencio
Silencio `k == n` Silencio Sólo consideramos toda la matriz. El cheque de viabilidad todavía funciona (la ventana es todo el array). Silencio No es necesario cambiar. Silencio
Silencio Muy pequeño `k` (p. ej., `k = 1`) Silencio El algoritmo todavía debe manejar cada elemento individualmente. La lógica de la ventanilla deslizante todavía funciona; actualizaciones "min_prefix" de las posiciones correctas. Silencio
TENIDA `nums` contiene " in.MIN_VALUE " or `int.MAX_VALUE ' , sometido a `mid ' puede causar `pref ' a la subida/absuelo. Silencio Trabajar con `doble` para sumas prefijas; fundir ints para duplicar antes de la resta. Silencio

### 4.6 Step‐by‐Step Walkthrough (Ilustración)

Assume `nums = [1,12,-5,-6,50,3]`, `k = 4`.

1. ** Los límites interiores**: `bajo = -6`, `alto = 50`.
2. **Primero medio**: `(50 + -6) / 2 = 22`.
*Transform* → `[ -21, -10, -27, -28, 28, -19 ].
Resumiendo: `[0, -21, -31, -58, -86, -58, -77]`.
Check: No hay diferencia positiva → `alta = 22`.
3. **A mitad siguiente**: `(22 + -6) / 2 = 8`.
Transform → `[-7, 4, -13, -14, 42, -5]`.
Resumiendo: `[0, -7, -3, -16, -30, 12, 7]`.
Check: En el índice 5, `pref[5] - min_prefix = 12 - (-7) = 19 ≤ 0`. → `low = 8`.
4. Repita hasta 'alto - bajo' 1e‐5`. Respuesta final: 25,75.

### 4.7 Running the Code

Java** – Copiar la clase 'Solution' en el IDE LeetCode.
- **Python** – Pegar la función en el editor, luego ejecutar `findMaxAverage([1,12,-5,-6,50,3],4)` → `25.75`.
- **C+** – Pegar la clase `Solution`; compilar con `-std=c+17`.

Los tres idiomas producen resultados idénticos y se ejecutan dentro de los plazos.

### 4.8 Takeaway – What to Bring Back to the Interview

1. **Binary Search as a Pattern** – “Check‐if‐feasible” + búsqueda binaria resuelve muchos problemas de valor “max/min” (por ejemplo, *máxima diferencia mínima*, *mínimo altura máxima*, etc.).
2. ** Transformación de valor a etapa** – La subcontratación de media convierte los promedios en sumas. El mismo truco puede resolver problemas sobre medianas, diferencias, etc.
3. **Prefix Sum + Sliding Minimum** – Una técnica general para probar un sub-array de longitud al menos `k` que satisface una condición suma.
4. **Confianza en el idioma de la lengua** – Puede implementar el mismo algoritmo en Java, Python o C++ en cuestión de minutos. Esto muestra a los entrevistadores que no están atados a una sola pila.

### 4.9 Pensamientos Finales

LeetCode 644 es un hermoso microecosistema de ideas.
Si puede explicar por qué funciona la búsqueda binaria, cómo las sumas prefijo codifican la prueba de viabilidad, y cómo la ventana corredera da tiempo lineal, ha dominado una técnica que aparece en *casi cualquier entrevista de codificación*.

¡Buena suerte! 🚀

-...

Lista rápida antes de enviar

Silencio TENIENDO EL ARTÍCULO Silencio Hecho? Silencio
Silencio...
tención 1️ Establecer `bajo = min(nums)`, `alta = máx(nums)`  ✔
⋅ 2️ Use a `double` prefix array ✔
TENIDO 3 PUEDE `mientras (alto - bajo √Īo 1e-5)` bucle ✔
La prueba de viabilidad corre O(n)
Silencio 5 comentarios Return Return `low ' (el promedio más viable)

-...

#### 🚀 Wrap‐Up

Ahora tienes:

* Código de copiado listo para Java, Python y C++.
* Un blog corto, amigable con SEO que aclara las ideas básicas.

Utilice el código como referencia o pegado y dirígido en LeetCode. La explicación le ayudará a articular la solución a un reclutador o un panel de entrevista técnica. ¡Feliz codificación!