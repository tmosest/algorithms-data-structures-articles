-...
Título: LeetCode 1248.
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
1. El Código - Tres idiomas

A continuación encontrará una solución limpia, de un paso, O(n) que cuenta el número de sub-arrays “nice” (exactamente *k* números impares).
La idea es transformar el problema en * “sub-arrays con más probabilidades k”* y luego restar el recuento para *k‐1*.
Las tres implementaciones utilizan la misma rutina de ayuda `atMostK`.

Silencio Idioma Silencio Código Silencio
Silencio...
Silencio**
Silencio **Python** Silencio **
Silencio **C+** Silencio **solution.cpp**

-...

## 1.1 Java

``java
// 1248. Número de Niza Subarrays
// Sliding‐Window + Prefix‐Sum Trick (O(n) time, O(1) space)

importar java.util*;

Solución de la clase pública {}
// Cuenta sub-arrays con números impares k exactamente
Número de entrada públicoOfSubarrays(int[] nums, int k) {
volver aMostK(nums, k) - enMostK(nums, k - 1);
}

// Cuenta sub-arrays con la mayoría de los números impares k
int privado enMostK(int[] nums, int k) {
si (k 0) retorno 0; // nada puede satisfacer una cuota negativa
int left = 0, right = 0;
intrínseca Cnt = 0;
total = 0;
mientras (derecha) {
// añadir el elemento actual a la ventana
oddCnt += nums[right] % 2;
// encogimiento de la izquierda si superamos la cuota
mientras (oddCnt не k) {}
oddCnt -= nums[left] % 2;
izquierda++;
}
// todas las sub-arrayas que terminan a la derecha y comienzan en cualquier lugar
// entre izquierda y derecha son válidas
total += derecha - izquierda + 1;
right++;
}
Total de retorno;
}
}
`` `

-...

## 1.2 Python

``python
# 1248. Número de buenas subarrayas
# Sliding window approach – O(n) time, O(1) space

de la importación Lista

Solución de clase:
def number OfSubarrays(self, nums: List[int], k: int) - int:
volver auto.at_most_k(nums, k) - self.at_most_k(nums, k - 1)

def at_most_k(self, nums: List[int], k: int) - título int:
si k < 0
retorno 0
izquierda = 0
odd_cnt = 0
total = 0
por derecho, val in enumerate(nums):
odd_cnt += val > 1 # 1 if odd, 0 if even
mientras que odd_cnt
odd_cnt -= nums[left] > 1
izquierda += 1
total += derecha - izquierda + 1
total
`` `

-...

## 1.3 C++

``cpp
// 1248. Número de Niza Subarrays
// Ventana deslizante – O(n) tiempo, espacio O(1)

Incluido el título
usando std namespace;

Clase Solución {
public:
número int De Subarrays(vector asignadoint círculo nums, int k) {
volver aMostK(nums, k) - enMostK(nums, k - 1);
}

privado:
int enMostK(cont vector identificadoint círculo nums, int k) {
si (k 0) retorna 0;
int left = 0;
intrínseca Cnt = 0;
total = 0;
para (derecho = 0; derecho)
oddCnt += nums[right] & 1; // 1 if odd
mientras (oddCnt не k) {}
oddCnt -= nums[left] " 1;
++izquierda;
}
total += derecha - izquierda + 1; // sub-arrays terminando a la derecha
}
Total de retorno;
}
};
`` `

Las tres implementaciones tienen **O(n)** complejidad de tiempo, escanear el array una vez, y utilizar sólo un puñado de variables enteros – perfectamente adecuado para las limitaciones de LeetCode (hasta 50 000 elementos).

# 2. Blog Artículo – “El Bien, el Mal, y el Ugly” de Contar Niza Sub-Arrays

■ **Emergido público:** Ingenieros de software, entrevistados de codificación y reclutadores
■ ** Objetivo:** Mostrar la comprensión profunda de un problema clásico de la ventanilla deslizante, al tiempo que aumenta la SEO para las palabras clave de búsqueda de empleo.

-...

## 2.1 Title & Meta‐ Datos

TEN TERRITORIO TERRITORIO TERRITORIO TERRITORIO
Silencio...
Silencio **Título** Silencioso *Counting Nice Sub-Arrays: The Good, The Bad, and The Ugly – A Complete Sliding‐Window Walk‐through* ←
Silencio **Meta Descripción** Silencio Master LeetCode 1248 con una solución de ventanilla deslizante O(n). Aprende las trampas, las mejores prácticas y cómo llegar a la entrevista. Silencio
Silencio **Keywords** Silencioso “LeetCode 1248”, “cuenta número de subarrays agradables”, “ventana deslizante”, “dos punteros”, “cuestión de entrevista”, “Solución de Java”, “Solución de Python”, “Solución C++”, “exactly k odds”, “entrevista de algoritmo”, “prep de entrevista de trabajo”

-...

## 2.2 Introduction

■ “En las entrevistas de algoritmos, las preguntas más temidas son las que se ven sencillas pero te acercan. ”
■
■ LeetCode 1248 – **Número de Niza Subarrays** – es ese clásico. Le pide que encuentre cuántas sub-arrayas continuas contienen *exactamente* `k` números impares.
■
■ ¿El truco? Convierte el problema en una variante *prefix sum* y solucionalo en **O(n)** tiempo con **O(1)** espacio extra. A continuación, caminamos por el **bueno**, el **bad**, y el **ugly** de este desafío, con código en Java, Python, y C++.

-...

## 2.3 Problema general

TENIDO Parameter TENIDO Significado
Silencio...
Silencioso `nums` ¦ Integer array (`1 <= nums[i] Silencio
TENIDO `k` TENIDO El objetivo cuenta con números impares (`1 <= k י= nums.length`) Silencio
Silencio ** Objetivo** Silencio Contar sub-arrays con números impares exactamente 'k'

*Examples*

1. `nums = [1,1,2,1,1]`, `k = 3` → `2` (`[1,1,2,1]`, `[1,2,1,1]`)
2. `nums = [2,4,6]`, `k = 1` → `0` (sin números impares)
3. `nums = [2,2,2,1,2,1,2,2,2,2,2,2]`, `k = 2` → `16`

-...

## 2.4 El Bien - ¿Por qué gana el enfoque Sliding-Window

1. **Tiempo de Luz, Espacio Extra Constante**
Cada elemento se procesa al máximo dos veces – una vez que el puntero derecho se mueve a la derecha, una vez cuando el puntero izquierdo se mueve a la derecha. No hay arrays adicionales o mapas de hash.

2. **Evites Prefix‐Sum + HashMap Overhead**
Un primer intento común es computar sumas prefijas de “oddness” y utilizar un mapa de hash para contar sumas sub-array iguales a “k”. Eso funciona pero tiene tiempo O(n) y espacio O(n). La ventana deslizante reduce el espacio a O(1).

3. Intuición absoluta
Transformar el array: extraño → 1, incluso → 0. El problema se convierte en “sub-array sum equals k”.
Entonces, *exactamente k* = *en la mayoría k* – *en la mayoría (k‐1)*. Cada llamada de ayuda cuenta cuántas ventanas contienen a la mayoría de los `k`.
Contando “a la mayoría de k” es un problema de ventanilla deslizante de libros de texto: expandirse, reducirse cuando exceda “k”.

4. *Ayudante reutilizable*
La función de ayuda `atMostK` es agnóstica del objetivo. La respuesta final es una simple resta, evitando la duplicación de códigos.

5. **Edge‐Case Friendly**
Negativo `k` en el ayudante automáticamente regresa Esto maneja perfectamente `k‐1` cuando `k = 0`.

-...

## 2.5 The Bad – Common Pitfalls and Edge Cases

Silencio Pitfall Silencio Por qué sucede  Cómo arreglar
Silencio...
Silencio **Realizar cada número como un “sub-array”** Silencio Mis-contando cuando la conversión no se realiza ─ Utilizar `num % 2` (o `num ' 1`) para detectar impares
Silencio **Off‐by-one errores en la longitud de la ventana** TENIENDO `derecha - izquierda + 1` para rangos inclusivos TENCIÓN Examinar explícitamente casos pequeños (`[1]`, `k=1`) Silencio
Silencio **Using a HashMap but missing the “k‐1” subtraction** Silencio Acumulando los recuentos exactos sólo Silencio Emplear la diferencia truco o prefijo de doble bucle sumas TEN
Silencio **Ignorando el escenario negativo `k‐1`** Silencio `k` puede ser 1 → ayudante llamado con 0 Silencio Add guard `if k  won 0: return 0. Silencio
Silencio **Using `val % 2` repeatedly inside loop** ← Rendimiento de la luz golpeada en los lazos estrechos ← Pre-compute `val ' 1` once per element
Silencio **Asumiendo que la matriz está basada en 0** Нале C++ índices vs Python lista de rebanadas ¦ Use `for right, val in enumerate(nums):` en Python, `for (int right = 0; right י n; ++right)` en C+  durable

-...

## 2.6 El Ugly – Deep‐Dive into Optimization & “Nice” Variantes

1. *Desbordamiento de enteros*
En Java, la suma de las ventanas puede llegar a `n * n / 2` ( Entendido 1.25 mil millones para n=50k). `int` es seguro en Java y C++, pero en idiomas con tipos enteros más pequeños podría necesitar 'long'.

2. **Bit-wise vs Modulo**
El uso de `val ' 1 ' (bit-wise AND) es marginalmente más rápido que `val % 2`. Los compiladores modernos optimizan ambos, pero los micromarcadores en grandes entradas muestran un aumento de velocidad de ~5–10% para bit-wise.

3. **Cuando k es muy grande (k = n)**
`atMostK` nunca reducirá la ventana; todo el array es una sola ventana. El ayudante todavía funciona: `total = n * (n +1) / 2`.

4. #Handling Empty Array #
El problema garantiza "nums.length "= 1 " , pero la programación defensiva todavía verifica por " k " 0 " .

5. *Potential “Ugly” Recursion**
Un “atMostK” recurrente es una ruta fácil a un flujo de pila para elementos de 50 k. Mantenga la rutina iterativa.

6. ** Estrategia de Testing**
Escribe pruebas que cubren: todas las probabilidades, todos los uniformes, `k = 1`, `k = n`, alternando patrones extraños/incluso.

-...

## 2.7 Cómo aparecer en la búsqueda de un reclutador

Silencioso Acción Silencioso
Silencio...
Silencio **Incluya múltiples soluciones de idiomas** Silencio Programador en busca de “Solución Java LeetCode 1248” o “Solución Pitón” hará clic en ←
Silencio **Utilice los nombres de funciones claros (`atMostK`)** Silencio Ayuda a los algoritmos de búsqueda a recoger en terminología algorítmica
tención **Agregar tiempos y análisis de complejidad** viv Signals professionalism to both ATS and hiring managers tención
Silencio **Proporción de los diagramas visuales** ← Mejora la legibilidad, lo que aumenta el tiempo de vida – un factor clave de clasificación ←
Silencio **Embed code snippets in `rectificante especificado tags** Silencio Permite a los motores de búsqueda indexar el código para búsquedas a nivel de consultas TEN

-...

## 2.8 Cierre – Convertir la pregunta en una pieza de Portfolio

■ *“No se trata sólo de obtener la respuesta correcta; se trata de demostrar que usted entiende por qué funciona la respuesta, cómo protegerse contra errores comunes, y cómo explicar el algoritmo concisamente.”*
■
■ Al dominar LeetCode 1248 con el enfoque de la ventana deslizante, usted demuestra:
- Competencia con técnicas de dos puntos
:: Capacidad para transformar los problemas en subproblemas más simples
:: Utilización eficiente del tiempo " espacio
√≥ - Código limpio, mantenible en Java, Python y C++

■ Implemente este artículo en su blog, LinkedIn, o Medium con las palabras clave anteriores, y atraerá reclutadores que están buscando activamente candidatos listos para la entrevista. Buena suerte, y recuerde: cada fallo “muy” que evitas es un paso más cerca de la próxima llamada de entrevista.

-...

## 2.9 Quick Checklist for the Interview

- [ ] **Lea cuidadosamente la declaración del problema** – note que 'k' es "exactamente".
- [ ] **Convertir probabilidades a 1, incluso a 0** – modulo simple o truco bit-wise.
- [ ] **Implement `atMostK` escaparate corredera** - expandir → reducir → añadir `right-left+1`.
- [ ] ** Retorno `atMostK(k) - enMostK(k-1)`** - maneja todos los casos de borde automáticamente.
- [ ] **Prueba ejemplos + casos de borde** – los tres idiomas deben pasar.

¡Feliz codificación, y que su próxima entrevista sea una “nave”!