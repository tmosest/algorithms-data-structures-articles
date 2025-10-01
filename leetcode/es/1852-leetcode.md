-...
Título: LeetCode 1852. Números distintos en cada subarray -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1852 – Distinct Números en cada sub-array
**Java / Python / C++ implementaciones + un blog de entrevista “Good‐Bad‐Ugly”* *

■ **Keywords**: LeetCode 1852, números distintos, sub-array, ventana deslizante, Java, Python, C++, prep de entrevista, algoritmo, complejidad del tiempo, complejidad del espacio, entrevista de codificación, entrevista de trabajo, estructura de datos, hashmap, diccionario, vector.

-...

## 1. Recaptación de problemas

■ **Given** an integer array `nums` (length `n`) and an integer `k` (`1 ≤ k ≤ n`).
■ **Task**: Por cada ventana contigua de tamaño `k`, salida el conteo de elementos **distintos**.

`` `
Entrada: nums = [1,2,3,2,1,3], k = 3
Producto: [3,2,2,2,2,3]
`` `

La longitud de la matriz puede ser hasta `10^5`, por lo que una solución `O(n·k)` brute‐force será time‐out.

-...

## 2. Estrategia de solución – Ventana deslizante + mapa de Hash

1. **Window**: Mantenga una ventana `[izquierda, derecha)` de tamaño `k`.
2. **Hash Map**: Guarde la frecuencia de cada número dentro de la ventana.
3. #Move #
* Añadir `nums[right]` al mapa (aumento de su cuenta).
* Si el tamaño de la ventana llega a `k`, registre `map.size()` (número de llaves).
* Diapositiva la ventana: eliminar `nums[left]` (disminuir su cuenta, borrar si cero).
4. **Repetir** hasta que la derecha llegue a `n.

Esto se ejecuta en el tiempo `O(n)` y utiliza `O(k)` (en la mayoría de los " números distintos " ) espacio.

-...

## 3. Aplicación del Código

■ Todas las implementaciones siguen la misma lógica pero usan construcciones específicas para el lenguaje.

### 3.1 Java

``java
importa java.util. HashMap;
importa java.util. Mapa;

Solución de la clase pública {}
int[] distinctNumbers(int[] nums, int k) {
si (nums == null TENIDO EN LAS NUNMAS.length 0) devuelven nuevo int[0];

int n = nums.length;
int[] ans = nuevo int[n] - k + 1];
Mapa seleccionadoInteger, Integer frecuentementeq = nuevo HashMap Quería();

int left = 0, right = 0, idx = 0;

(derecho) {
freq.put(nums[right], freq.getOrDefault(nums[right], 0) + 1);
right++;

si (derecha - izquierda == k) {
ans[idx++] = freq.size();

int left Val = nums[left++];
si (--freq.get(leftVal) == 0) freq.remove(leftVal);
}
}
devolver los ans;
}
}
`` `

■ ** complejidades** – Tiempo `O(n)`, Espacio `O(k)`.

-...

#### 3.2 Python

``python
de la importación Lista
de las colecciones importadas por defecto

Solución de clase:
def distinctNumbers(self, nums: List[int], k: int) - confiar List[int]:
si no nums o len(nums)
retorno []

n = len(nums)
ans = []
freq = defaultdict(int)

izquierda = 0
por derecho, val in enumerate(nums):
freq[val] += 1

si la derecha - izquierda + 1 == k:
ans.append(len(freq))
left_val = nums[left]
freq[left_val] -= 1
si freq[left_val] == 0:
del freq[left_val]
izquierda += 1
Retorno
`` `

■ ** complejidades** – Tiempo `O(n)`, Espacio `O(k)`.

-...

### 3.3 C++

``cpp
Incluido el título
#include ■unordered_map Conf
usando std namespace;

Clase Solución {
public:
vector identificador distintosNúmeros(vector identificadoint espíritu nums, int k) {
si (nums.empty() TENIDO EN SUPERVISIÓN nums.size()

int n = nums.size();
vector significar uns
unordered_map madeint, int confianza freq;

int left = 0;
para (derecho = 0; derecho)
++freq[nums[right];

si (derecha - izquierda + 1 == k) {
ans.push_back(freq.size());

int left Val = nums[left++];
si (--freq[leftVal] == 0) freq.erase(leftVal);
}
}
devolver los ans;
}
};
`` `

■ ** complejidades** – Tiempo `O(n)`, Espacio `O(k)`.

-...

## 4. “Bueno, malo, ugly” entrevista Take-aways

**Aspecto** Silencio**
Silencio----------------------------------------------------
Silencio **Concept** Silencio Ventana deslizante + mapa de frecuencia – clásico, amigable para entrevistas. Silencio Ninguno (fácil de implementar). Silencio.
Silencio ** Complejidad del tiempo** Silencio `O(n)` – óptimo para `n = 10^5`. Silencio ❌ Brute‐force `O(n·k)` no tiene una gran entrada. Silencio
Silencio ** Complejidad del espacio** Silencio `O(k)` – sólo necesita contar para la ventana actual. ❌ Storing all prefix sums or pre-computed distinct sets consume `O(n·k)`. Silencio ❌ Utilizando an array of size `max(nums)+1` (`10^5`) when only `k` distinct needed – wasted Memory. Silencio
Silencio **Edge Cases** Silencio Handles `k = 1`, `k = n`, números repetidos. Silencio ❌ Olvídate de eliminar la clave cuando el recuento va a cero → inflamado conteo distintivo. Silencio
Silencio **Language Nuances** Silencioso Java’s `HashMap.getOrDefault`, Python’s `defaultdict`, C++’s `unordered_map`. ❌ En Java: using `Map` instead of `HashMap` may cause unnecessary overhead. ❌ In C+++: using `map` (red-bla). Silencio

■ **Key Take‐away**: Usar una estructura de hash * no ordenada*, la actualización cuenta en `O(1)` por paso, y siempre eliminar entradas cuando el conteo alcanza cero para mantener el tamaño del mapa exacto.

-...

## 5. Pruebas " Edge‐ Lista de verificación de casos

Silencio Test Silencio Descripción Silencio Esperado
Silencio------------------------
TENIDO `nums = [1,1,1], k = 1` TENIDO Todas las ventanas del tamaño 1 TENIDO `[1,1] `` Silencio
TENIENDO `nums = [1,2,3,4], k = 4` TENIDO Entire array Silencio `[4]
TENIDO `nums = [5], k = 1` TENIDO Elemento único
TENIENDO `nums = [2,2,2,2,2,2,2], k = 3` TENIDO Todos los duplicados ANTE `[1,1]`
TENIENDO `nums = [1,2,1,2,1,2,1,2], k = 2 ` TENIDO ANTERIOR TENIDO `[2,2,2,2,2,2,2,2] Silencio

Ejecute el código proporcionado con un arnés de prueba de unidad o método 'main` para validar.

-...

## 6. Consejos de desempeño

1. **Evitar la creación de objetos innecesarios** – volver a utilizar el mismo mapa/dict; claro sólo cuando sea necesario.
2. **Prefer `unordered_map` over `map` in C+** for `O(1)` average lookups.
3. ** En Java, utilice `HashMap` con capacidad inicial** `k` para reducir el reajuste (`nuevo HashMap garantizado(k)`).
4. **Vuelve brevemente** para casos de filo ( " k " , `nums == null " ) para ahorrar tiempo.

-...

## 7. Historia de la entrevista – “La ventana deslizante Saga”

*“Una vez me enfrenté a una pregunta de código de leetcóticos pidiendo cuentas distintas en cada subarray. Mi primer instinto fue un bucle anidado; después de unos minutos de desbordamiento de la pila, recordé el truco de la ventana deslizante. Codifiqué un mapa de hash para mantener frecuencias y deslizar la ventana en tiempo lineal. El entrevistador quedó impresionado por la complejidad `O(n)` y la eliminación limpia de llaves cuando los conteos cayeron a cero. Ese pequeño detalle sobre la eliminación de teclas de cuenta cero salvó mi solución de estar equivocado en casos de prueba con muchas repeticiones.”*

-...

## 8. Pensamientos finales

¿Por qué esto importa para una entrevista de trabajo?
* Demuestra el dominio de dos estructuras de datos centrales: tablas de hash y ventanas correderas.
* Muestra la conciencia de los intercambios entre tiempo y espacio.
* Indica cuidadoso manejo de casos de borde y gestión de memoria.

- **Siguientes pasos**:
* Variaciones de práctica – “Countar valores distintos en un rango” (preguntas de línea).
* Explorar estructuras de datos más avanzadas: `Arbol de Kenwick’ o `Arbol de segmento’ para actualizaciones dinámicas.
* Construir un repo personal de soluciones de ventanas correderas para recordar rápidamente durante entrevistas.

-...

#### 🎯 SEO Meta Descripción

■ "Solve LeetCode 1852 – Distinto Números en cada subarray. Aprenda Java, Python y C++ soluciones de ventanilla deslizante, análisis de tiempo y espacio y consejos de entrevista. Boost your coding interview prep and land your dream job. ”

-...

¡Feliz codificación, y que la cuenta distinta sea siempre a su favor!