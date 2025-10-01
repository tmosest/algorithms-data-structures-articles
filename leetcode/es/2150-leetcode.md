-...
Título: LeetCode 2150. Encontrar todos los números solitarios en el Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🧩 LeetCode 2150 – Encuentra todos los números solitarios en el Array
**Java fort Python ← C+** soluciones + un artículo de blog optimizado SEO que cubre el *bueno, el malo y el feo* de este problema – un post mortem perfecto para su próxima entrevista de codificación.

■ **Keywords:** *LeetCode 2150, Encuentra todos los números solitarios, entrevista de codificación, solución Java, solución Python, solución C++, algoritmo, complejidad del tiempo, complejidad del espacio, mapa de hash, matriz de frecuencia. *

-...

## 🎯 Problema Resumen

Se le da un array entero `nums`.
Un número `x` es ** solitario** si:

1. `x` ocurre **exactamente una vez** en el array.
2. Ni `x-1` ni `x+1` aparece en el array.

Devuelve todos los números solitarios en cualquier orden.

*Ejemplo*
`nums = [10,6,5,8] → [10,8]`
Ambos 10 y 8 aparecen una vez, y ninguno tiene números adyacentes en el array.

**Constraints* *

TEN TERRITOR ANTERIOR ANTERIOR ANTERIOR
Silencio...
TENIDO `1 ≤ nums.length ≤ 105`
TENIDO `0 ≤ nums[i] ≤ 106`

-...

## 🚀 Solution Overview

Existen tres estrategias comunes:

Silencio Silencio Silencio Silencio Silencio
Silencio--------------------------------
Silencio ** Ordenación** (en lugar) Silencio Simple pero no óptimo para las limitaciones dadas. Silencio
Silencio **HashMap / HashSet** Silencio `O(n)` Silencio `O(n)` tención Handles rangos arbitrarios fácilmente. Silencio
Silencioso **Frequency Array** Silencio más rápido si `max(nums)` es pequeño (≤ 1 e6). Silencio

El array **frecuencia** es el más rápido para este problema porque el rango de valor está ligado.
Ilustraremos que en la sección *buena* y la contrastamos con el enfoque *bad* de clasificación.

-...

## 🔧 Code Implementations

■ Los tres francotiradores siguen la estrategia **frecuencia-array** para el espacio `O(n)` tiempo y `O(max(nums)+3)`.

### 1. Java

``java
importar java.util*;

Solución de la clase pública {}
public List won(int[] nums) {
// Encontrar el valor máximo para el tamaño de la matriz de frecuencia.
int max = 0;
para (int v : nums) max = Math.max(max, v);

int[] freq = nuevo int[max + 3]; // +3 a acceso seguro v-1 y v+1

// Construir frecuencias.
para (int v : nums) {
freq[v]+; // Contando ocurrencias.
}

Lista realizadaInteger título solitario = nuevo ArrayList implicado();

// Revise cada número único.
para (int v : nums) {
si (freq[v] == 1 " frecuenciaq[v - 1] == 0 " frecuenciaq [v + 1] == 0) {
solitario.add(v);
}
}

volver solo;
}
}
`` `

■ **¿Por qué `max + 3'? #
■ La matriz necesita apoyar los índices `v-1` y `v+1`. Adding 3 ensures we never hit `ArrayIndexOutOfBoundsException` incluso para `v = max`.

-...

### 2. Pitón

``python
de la importación Lista

Solución de clase:
def findLonely(self, nums: List[int] List[int]:
max_val = max(nums)
freq = [0] * (max_val + 3) # +3 para el acceso seguro v-1, v+1

para v en nums:
freq[v] += 1

solo = []
para v en nums:
si freq[v] == 1 y freq[v - 1] == 0 y freq[v + 1] == 0:
solitario.append(v)

regreso solitario
`` `

-...

### 3. C++

``cpp
Incluido el título
#include >

Clase Solución {
public:
std:::vector seleccionadoint confianza findLonely(std::vector correspondintющ nums) {
int maxVal = *std::max_element(nums.begin(), nums.end());
std::vector seleccionado invertir frecuenciaq(maxVal + 3, 0); // +3 para v-1 y v+1

para (int v : nums) {
freq[v]+; // Cuenta cada ocurrencia
}

std::vector realizadoint título solitario;
para (int v : nums) {
si (freq[v] == 1 " frecuenciaq[v - 1] == 0 " frecuenciaq [v + 1] == 0) {
solitario.push_back(v);
}
}

volver solo;
}
};
`` `

■ En los tres idiomas, primero construimos una tabla de frecuencias y luego escaneamos el array una vez más para elegir los números solitarios.

-...

## 📚 El Bien, el Mal, y el Ugly

Silencio Fase actual Lo que aprendimos, ¿por qué importa?
Silencio...
Silencio **El Bien** Silencioso *El array de frecuencia* da ** tiempo lineal** (`O(n)`) y una sobrecarga mínima de factores constantes. Funciona perfectamente cuando el dominio de entrada (`0‐106`) está atado. En entrevistas, mostrar conciencia de las limitaciones de entrada permite a los entrevistadores ver que usted puede adaptar soluciones. Silencio
Silencio **El mal** Silencioso* (`O(n log n)`) es sencillo pero desperdicio para este problema. También se rompe cuando los números exceden el rango " in " o cuando se le pide espacio " O(1) " . Silencio
Silencio **El Ugly** Silencio Relying on a **HashMap** or **unordered_map** funciona, pero puede olvidarse de manejar '-1` o '+1` periféricos, lo que conduce a errores fuera de límites o lógica. ← Muchos entrevistadores prueban su atención al detalle; siempre validan a los vecinos y tengan cuidado con los índices de array. Silencio

#### TL;DR

- **Preferir el array de frecuencias** cuando el rango de valor sea conocido y pequeño.
- Evite ordenar a menos que sea necesario (por ejemplo, para una orden de ruptura de corbatas).
- Doble control de las condiciones del límite: `v-1` cuando `v = 0`, y `v+1` cuando `v = max(nums)`.

-...

## 📈 Complexity Analysis

← Algorithm Silencio Silencio
Silencio----------------
Silencioso Frequency Array (nuestros) Silencioso `O(max(nums)+3) ' .
Silencio HashMap Silencio `O(n)` Silencio
Silencio Ordenación Silencioso `O(n log n)` (en lugar)

■ ** Nota práctica:**
■ Aunque la matriz de frecuencia utiliza alrededor de 4 MB para `max = 1 e6`, eso es trivial en las máquinas modernas y bien dentro de los límites de LeetCode.

-...

## 📝 Pensamientos Finales > Consejos de Entrevista

1. **Pregunta por limitaciones** temprano. Si el entrevistador menciona un rango limitado, proponga un array de frecuencia inmediatamente.
2. **Explicar la lógica** claramente: “Countar ocurrencias → comprobar vecinos → recoger números solitarios. ”
Las ayudas visuales (como una tabla simple) pueden ayudar.
3. ** Casos de edge**: matriz vacía (no permitida por restricciones), elemento único, duplicados, límites (`0` y `max`).
4. **Testing**: Ejecute una prueba de cordura rápida (`[1, 2, 3, 5, 7] → [5, 7]`).
5. **Siguiente**: "¿Deberíamos hacer mejor en el espacio?" – La respuesta: no mucho; un mapa de hash necesita espacio `O(n)`, mientras que el array ya es óptimo dado el dominio de entrada.

-...

## 🎯 SEO‐Optimized Closing

Si te estás preparando para una entrevista de ingeniería de software, masterizar *LeetCode 2150 – Encontrar todos los números solitarios en el Array* demuestra:

- Su capacidad para analizar las limitaciones de entrada y elegir una estructura de datos óptima.
- Tu competencia en Java, Python y C++.
- Su habilidad para explicar los cambios algorítmicos (bueno, malo, feo).

Mantenga este problema en su radar: es una entrevista clásica favorita que prueba tanto **frecuencia contando** como **terrestre** lógica. ¡Feliz codificación!

-...

*Fuentes: Problema oficial de LeetCode 2150, y soluciones comunitarias como las de “Subrata Jana” y “Kushal Bharadwaj”. *