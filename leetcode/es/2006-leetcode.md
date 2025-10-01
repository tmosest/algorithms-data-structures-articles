-...
Título: LeetCode 2006. Número de pares con diferencia absoluta K -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código

A continuación se presentan tres soluciones idiomáticas que se ejecutan en **O(n)** tiempo y **O(1)** espacio adicional (una tabla de frecuencias de tamaño constante o un mapa de hash).

Silencio Idioma Silencioso
Silencio...
Silencio **Java** Silencioso `Solution.java` Silencio
Silencioso **Python**
Silencio **C+**

-...

### 1.1 Java – `Solution.java `

``java
importa java.util. HashMap;
importa java.util. Mapa;

Solución de la clase pública {}
int countKDifference(int[] nums, int k) {
// Mapa de frecuencia: número - título su cuenta en nums
Mapa seleccionadoInteger, Integer frecuentementeq = nuevo HashMap Quería();

para (int num : nums) {
freq.put(num, freq.getOrDefault(num, 0) + 1);
}

int count = 0;
para (int num : nums) {
// Sólo busque num + k (el par i < j garantiza que no tenemos doble cuenta)
int target = num + k;
Integer tCnt = freq.get(target);
si (tCnt != null) {
Cuenta += tCnt;
}
}
recuento de retorno;
}
}
`` `

-...

### 1.2 Python – `solution.py `

``python
de las importaciones de colecciones Contrato
de la importación Lista

def countKDifference(nums: List[int], k: int) - título int:
freq = Counter(nums) # O(n) time, O(1) extra space (max 100 teclas distintas)
Conteo = 0
para las numidades:
contar += freq.get(num + k, 0)
cuenta de retorno
`` `

-...

### 1.3 C++ – `solution.cpp `

``cpp
Incluido el título
#include ■unordered_map Conf

Clase Solución {
public:
int countKDifference(std::vector efectuadoint ánimos, int k) {
std::unordered_map armonizado, int confianza freq;
for (int nums : nums) freq[num]++; // build freq mapa

int ans = 0;
para (int num : nums) {
auto = freq.find(num + k);
if (it != freq.end()) ans += it- confíasecond;
}
devolver los ans;
}
};
`` `

■ *Por qué funciona* *
■ Contamos cada elemento *una vez* y agregamos el número de ocurrencias del valor que es exactamente 'k' más grande. Debido a que sólo esperamos hacia adelante (`num + k`) el par `(i, j)` con `i ' se cuenta exactamente una vez, sin doble cuenta y sin bucles anidados.

-...

## 2. Artículo del Blog

*Título*
**“Número de pares con diferencia absoluta K – el bien, el mal y el ugly (Java/Python/C++)”* *

**Descripción de los datos (SEO):* *
Master LeetCode 2006 en Java, Python y C++ con una solución O(n). Aprenda las trampas, el manejo de los bordes, y cómo llegar a esta pregunta de entrevista. Perfecto para los ingenieros de software buscando empleos.

-...

#### 2.1 Introduction

Has conseguido una entrevista de codificación y el entrevistador pregunta:
*“Dé un array `nums ' y un entero `k`, contar los pares (i, j) donde yo cauté j y Silencionums[i] – nums[j] eterna == k.”*

Este es LeetCode 2006 – un problema aparentemente simple “difference‐k” que esconde algunas trampas sutiles. En este post diseccionamos el **bueno**, el **bad**, y los enfoques **ugly**, y entregamos una solución limpia y lista para la producción en **Java, Python y C+**.

-...

### 2.2 Declaración de problemas (Clear " Concise)

- ** Entrada*
- `nums`: array entero, longitud 1 ≤ n ≤ 200
- `k`: 1 ≤ k ≤ 99
- `1 ≤ nums[i] ≤ 100`

- ¡Fuera!
- El recuento de los pares de índices `(i, j)` donde `i ' escritos j ' y `persnums[i] - nums[j] viven == k`.

- *Examples*

Silencios en la vida
...------------------
Silencio [1,2,2,1] Silencio 1 Silencio 4 Silencio cada 1‐2 par Silencio
TENIDO [1,3] TENIDO 3 ANTERIOR 0 Silencio no par ANTE
Silencio [3,2,1,5,4] Silencio 2 Silencio 3 Silencio (3,1),(5,3),(4,2)

-...

### 2.3 The Good – O(n) Solution

**Idea** – Use una tabla de frecuencias (o mapa de hash) para recordar cuántas veces aparece cada número. Para cada elemento `x`, el único socio que puede formar un par válido es `x + k` (porque aplicamos `i  j j`). Al añadir `freq[x + k]` a la respuesta para cada 'x' obtenemos el recuento total en tiempo lineal.

#### Why It's Good

Silencio .
Silencio...
Silencio **Hora** Silencioso `O(n)` – dos pases lineales, sin bucles anidados
Silencio **Espacio** Silencioso `O(1)` – array de tamaño fijo (100 valores) o `O(1)` para mapa de hash (max 100 teclas) Silencio
Silencio **claritud** Silencio directo: contar frecuencias → escanear una vez más
Silencio **Scalability** Silencio Trabaja para 'n` hasta millones (todavía linear) Silencio
Silencio **Estabilidad** Silencio Fácil de probar con pequeños ayudantes

#### Edge Cases Handled

Silencio Silencio Silencioso
Silencio...
TENIDO `k = 0` ANTE Las restricciones del problema prohíben `k = 0` (k ≥ 1), por lo que no se requiere un manejo especial. Silencio
← Duplicar valores Silencio Frecuencia mapa cuenta automáticamente la multiplicidad. Silencio
Silencio Negativo `k` Silencio No está permitido, pero si está presente, la fórmula todavía funcionaría porque la diferencia absoluta es simétrica. Silencio
Ø Elemento Max 100 ¦ Frequency array de tamaño 101 es suficiente. Silencio

-...

## 2.4 The Bad – Quadratic Brute Force

Un enfoque común pero ingenuo:

``python
def bad(nums, k):
Conteo = 0
para i en rango(len(nums)):
para j en rango(i + 1, len(nums)):
si abs(nums[i] - nums[j]) == k:
Cuenta += 1
cuenta de retorno
`` `

##### Por qué es malo

- **O(n2)** – Para 'n = 200', todavía bien, pero para los escenarios de entrevista puede enfrentar arrays hasta 105.
- **Hard to Optimize** – Dos bucles anidados dan poco espacio para la salida temprana a menos que agregue la poda compleja.
- **Readability** – La intención es obvia, pero la ineficiencia muestra falta de pensamiento algorítmico.

-...

### 2.5 The Ugly – Frequency Array Misuse

A veces la gente usa un array de frecuencias pero olvida dar cuenta de ** pares duplicados** o de la restricción **i âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa o âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa âTMa

``java
int[] freq = nuevo int[101];
para (int x : nums) freq[x]++;

int ans = 0;
para (int x : nums) {
si (x + k) = 100) ans += freq[x + k]; // incorrecto si también contamos freq[x] antes
}
`` `

Resultado** – cuenta cada par dos veces. The fix is to **only add** once per occurrence of `x`. Es por eso que nosotros tampoco:
- Iterate sobre el * mapa de frecuencia* mismo: `para (int x : freq) ans += freq[x] * freq[x + k]` (y dividir por 2 si k = 0).
- O mantener el bucle original, pero confíe en `i ' identificado j ' implícitamente (escuchando el array original y mirando sólo `x + k`).

-...

### 2.6 Full Walk‐through – Java Code Explained

``java
int countKDifference(int[] nums, int k) {
// Tabla de frecuencia de construcción
int[] freq = nuevo int[101]; // índices 1..100
para (int n : nums) freq[n]++;

int ans = 0;
// Para cada elemento, cuenta con socios que son k más grandes
para (int n : nums) {
int target = n + k;
si (objetivo 0 = 100) ans += freq[target];
}
devolver los ans;
}
`` `

* Puntos clave: *

1. **Dirección de tamaño fijo** – evita el hash overhead, gracias a los límites `nums[i] ≤ 100`.
2. **Single pasa a poblar** – O(n) operaciones de memoria.
3. ** Segundo paso** – sólo esperamos (`n + k`), por lo que cada par válido contribuye exactamente una vez.

-...

### 2.7 Complexity Analysis (All Languages)

TENIDO MEDIDAS FORMULADAS O(n) Solución
Silencio----------------------------------------------
TENIDO ANTERIOR ANTERIENTE **O(n2)**
TENIDO EL ESPACIO SUPERVISIÓN **O(1)**
Silencio Persona más grande

Debido a que las limitaciones son pequeñas, todos los idiomas golpean la misma complejidad asintotica. Pero para un conjunto de datos más grande o entrevista, la solución lineal es la única práctica.

-...

### 2.8 Consejos comunes

Silencio Pitfall Silencio
Silencio...
Silencio **Cuento doble** Silencio Sólo cuenta `x + k`, no `x - k`. Silencio
Silencio **Off‐by‐one en array** Silencio Al utilizar un array fijo, asegúrese de que los índices cubren todo el rango (1–100). Silencio
Silencio **Assuming k ≥ 0** Silencio El problema garantiza `k ≥ 1`, pero en general necesitará manejar k negativo o `k == 0`. Silencio
Silencio **Ignorando límites de entrada** Silencio Un mapa de hash es más seguro cuando los valores pueden ser grandes; pero si los límites son pequeños, un array de frecuencia es más rápido. Silencio
Silencio **No maneje k = 0** Silencio Si se permite, utilice `freq[x] * (freq[x] - 1) / 2` para evitar la doble contabilización. Silencio

-...

### 2.9 Take‐ Away

- Use un mapa de frecuencia ** (o array) para reducir el problema de verificación de pares a un solo escaneo lineal.
- La condición **i > i > se aplica naturalmente buscando el `num + k`.
- Mantenga su solución **compact** y **bien documentado** – los entrevistadores valoran el razonamiento claro tanto como el código correcto.

-...

## 2.10 SEO‐Friendly Keywords

- LeetCode 2006
- Número de pares con diferencia absoluta K
- Solución Java LeetCode 2006
- Solución pitón LeetCode 2006
- Solución C++ LeetCode 2006
- O(n) par contando algoritmo
- interrogantes de codificación
- problema algorítmico resolver
- preguntas de entrevista de la estructura de datos
- algoritmo de mesa de frecuencia

-...

### 2.11 Conclusión

El problema “Número de parejas con diferencia absoluta K” es un rompecabezas clásico de entrevistas que prueba su comprensión de **conteo de frecuencia**, ** mapas de hash**, y ** eficiencia algorítmica**. Mediante la entrega de una solución O(n) limpia en Java, Python y C++, no sólo resolver el problema, sino también mostrar la capacidad de detectar y corregir los patrones malos y feos comunes. Buena suerte aterrizando ese trabajo, y feliz codificación!