-...
Título: LeetCode 330. Array Patching -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 330. Array de Patching – Una entrevista completa Guía lista
*(Java fort Python Silencio C++ Implementación + un blog profundo-dive post)*

-...

#### TL;DR

Silencio Idioma TENIDO Parches mínimos TENIDO truco clave TENIDO
Silencio----------------------------
Silencio **Java** Silencioso `O(log n + m)` Silencio Usar un `long` para evitar el desbordamiento; parche codicioso
Silencio **Python** Silencio `O(log n + m)` La misma lógica es que "in" no tiene límites
Silencio **C+** Silencioso `O(log n + m)` Silencio 64‐bit arithmetic (`long long') Silencio

■ **Lo que cubriremos* *
■ 1. Declaración de problemas " ejemplos
■ 2. Información graciosa + prueba formal
■ 3. algoritmo paso a paso
■ 4. Casos de borde " obstáculos
■ 5. Análisis del tiempo / espacio
■ 6. Snippets de código completo (Java, Python, C++)
■ 7. SEO amistoso “el bueno, el malo, el feo” artículo del blog

-...

## 1. Declaración de problemas

■ **Given**:
* `nums`: a **sorted** array of positive integers (length ≤ 1000).
< < < : integer (1 ≤ n ≤ 231 −1).
■ **Task**: Añada el **feo** nuevos números (patches) a `nums` para que cada número entero en `[1, n]` pueda ser representado como una suma de **algunos** elementos de la matriz * aumentada*.
■ **Regresar** el número mínimo de parches.

■ *Examples*
1. `nums = [1, 3]`, `n = 6` → response = 1 (patch `2`).
■ 2. `nums = [1, 5, 10]`, `n = 20` → response = 2 (patch `2, 4`).
■ 3. `nums = [1, 2, 2]`, `n = 5` → response = 0 (ya cubre todas las sumas).

-...

## 2. Why Greedy Works

Mantenemos una variable `miss` que representa el entero más pequeño **no** actualmente representable por el array que hemos visto hasta ahora (incluyendo los parches que hemos añadido). Inicialmente `miss = 1`.

- Si el siguiente elemento en `nums` (`nums[i]`) es **≤ miss**, significa que podemos ampliar el rango representable:
`miss += nums[i]` (todas las sumas hasta el nuevo `miso - 1` llegan a ser alcanzables).
- De lo contrario, tenemos que hacer un parche.
Añadiendo `miss` duplica el rango alcanzable: `miss += miss`.

¿Por qué remiendo `miso' óptimo?
Debido a que cualquier número " hecho " ya es representable, y cualquier número ≥ " miss " pero " dañados + nums[i] " se puede hacer accesible sólo añadiendo un número ≤ `miss`. El número más pequeño es exactamente " inadmisible " . Por lo tanto, el parche codicioso `miss` es la única manera de cerrar la brecha con un solo parche.

El proceso se detiene una vez. En ese momento, todo entero hasta `n` es representable.

-...

## 3. Algoritmo (código Pseudo)

`` `
minPatches(nums, n):
parches = 0
I = 0
miss = 1 // menor suma no representativo

mientras se pierden
si yo hice len(nums) y nums[i]
miss += nums[i]
i += 1
más:
// parche falta
miss += miss
parches += 1

parches de retorno
`` `

*Importante*: Use integers de 64 bits ( " largo " ) para `miso ' porque `mis ' puede duplicar muchas veces y puede exceder los límites de 32 bits.

-...

## 4. Casos de borde " Gotchas "

Silencio Caso confidencialidad ¿Por qué importa?
Silencio...
TENIDA `nums` contiene `1` Silencio Si el array comienza a 1 de inmediato ampliamos el rango ANTE La rama `si` lo maneja. Silencio
Silencioso `nums[i]`. `mis `mis` Silencio Gap - necesitamos un parche Silencio Los parches de la rama `else `miss`. Silencio
TENIENDO `n` muy grande (`Ω231 − 1`) TENIDO `miss` puede exceder 32-bit ANTE Utilizar enteros de 64 bits. Silencio
Silencio `nums` ya cubre todas las sumas Silencio No hay parches necesarios Silencio Las salidas de Loop cuando `miss ≤ n`. Silencio

-...

## 5. Análisis de la complejidad

TENIDO TERRENO Java / Python / C++
Silencio...
TENIDO Tiempo TENIDO **O(log n + m)** (cada parche en la mayoría de los dobles `miss`, por lo que en la mayoría de los parches 'log2 n`; cada elemento array procesado una vez). Silencio
← Espacio Silencioso **O(1)** (sólo unas pocas variables). Silencio

-...

## 6. Código completo

## Java

``java
Solución de la clase pública {}
public int minPatches(int[] nums, int n) {
parches int = 0;
int i = 0;
larga falta = 1; // uso largo para evitar el desbordamiento

mientras que (miso <= n) {
si (i) se hizo nums.length " nums[i] י= miss) {
miss += nums[i+];
. ♫ ... {
miss += miss; // parche miss
parches++;
}
}
parches de retorno;
}
}
`` `

## Python

``python
Solución de clase:
def minPatches(self, nums: List[int], n: int) - título int:
parches = 0
I = 0
falta = 1 # Python ints are unbounded

mientras se pierden
si yo hice len(nums) y nums[i]
miss += nums[i]
i += 1
más:
miss += miss
parches += 1
parches de retorno
`` `

### C++

``cpp
Clase Solución {
public:
int minPatches(vector fielint círculo nums, int n) {
parches int = 0, i = 0;
larga falta = 1; // 64-bit para evitar el desbordamiento

mientras que (miso <= n) {
si (i) se hizo nums.size() " nums[i]
miss += nums[i+];
. ♫ ... {
miss += miss; // parche miss
++patches;
}
}
parches de retorno;
}
};
`` `

-...

## 7. Artículo del Blog – “El Bien, el Mal y el Ugly”

■ **Título**: *Patching Array – The Ultimate Interview Cheat Sheet (Good, Bad, & Ugly)*
■ **Descripción**: “Aprenda a romper el problema de Patching Array de LeetCode en 5 minutos. Entender el algoritmo codicioso, los casos de borde y prepararse para su próxima entrevista de trabajo. ”

### 7.1 The Good
****Simplicity** – Un bucle, dos ramas, aritmética de 64 bits.
* **Optimality** – Provenida estrategia codictiva garantiza el número mínimo de parches.
* **Especiado** – O(log n) parches; trabaja en milisegundos para las máximas limitaciones.

### 7.2 The Bad
* **Pestaca de flujo* En idiomas con límites de 32 bits ( " in " en Java/C++ " ), " puede desbordarse antes de darse cuenta de ello.
* **Misreading the problem** – Muchos candidatos piensan “patch the smallest missing number” pero olvidan duplicar “miss” después de parchear.
* **Puntos ciegos de emergencia** – Olvídate de que los 'nums' ya podrían cubrir toda la gama o que `n` podría ser 1.

## 7.3 The Ugly
* **Prueba compleja** – Algunas soluciones intentan un DP o una recursión que explota tanto en el tiempo como en el espacio.
* ** Variables innecesarias** – Superar la solución (por ejemplo, construir un conjunto de todas las sumas alcanzables) conduce a TLE.
* **Datotipo incorrecto** – Utilizar `int` for `miss` en Java/C++ resulta en errores ocultos que solo tienen una superficie grande `n`.

### 7.4 How to Nail En una entrevista

1. **Explicar la intuición primero** – Hablar de 'miser' y por qué parcharla es óptima.
2. **Mostrar el algoritmo en papel** – Escribe el pseudo-código, y luego lo mapea al idioma elegido.
3. **Desbordamiento de la tensión** – Mención con `long`/`long' y por qué importa.
4. **Corre a través de los casos de borde** – `n=1`, `nums=[1]`, `nums=[2]`, `n` enorme.
5. **La complejidad** – 1‐2 frases en el tiempo/espacio.

### 7.5 SEO Checklist

Silencio Element Silencio Por qué importa Silencio Cómo lo satisfacemos
Silencio...
Silencio **Keyword** Silencio “patching array” Silencio Incluido en título, encabezados y a lo largo del texto. Silencio
Silencio **Meta description** Silencio Short, compelling Silencio Proporcionado en la parte superior del artículo. Silencio
Silencio **Headers (H1, H2, H3)** tención Mejora la legibilidad " SEO tención Jerarquía estructurada con títulos descriptivos. Silencio
Silencio **Camaradas de frío** Silencio Muestra código claramente Silencio Cada idioma envuelto en vallas adecuadas (````java`, etc.). Silencio
Silencio **Imagen alt text** Silencio Si las imágenes agregadas ← Use texto descriptivo alt como “Esquema de parche verde”. Silencio
Silencio ** Enlaces internos** Silencio Mantiene a los usuarios en el sitio ← Sugerido “Related: LeetCode 1527” o “Top interview problems”. Silencio
Silencio **Referencias externas** tención Autoridad Silencio Enlaces a LeetCode y puestos de discusión. Silencio
Silencio ** Párrafos legibles** Silencio La calidad del contenido de Google Silencio párrafos cortos, puntos de bala. Silencio

## 7.6 Takeaway

El problema **Patching Array** es un reto codicioso clásico que prueba la capacidad de un candidato para pensar en la cobertura del rango y el crecimiento incremental. Dominar te da:

* Confianza en estrategias codictivas.
* Un buen punto de entrevista.
* Un fragmento de código que funciona en Java, Python y C++.

-...

**Feliz codificación - y que sus parches siempre sean mínimos! * *