-...
Título: LeetCode 930. Subarrayos binarios con sumo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 LeetCode 930 – Binary Subarrays With Sum
### 📈 How to Nail This Interview Question (Java ¦

■ ** Objetivo** – Dado un arsenal binario `nums ' y un entero `goal ' , contar todos los subarrays no vacío cuya suma equivale a `goal ' .

-...

###  pilar Datos rápidos (SEO Friendly)

Silencio Palabra clave Silencio Por qué importa Silencio
Silencio...
Silencio *LeetCode 930* Silencio partido directo para el problema número Silencio
Silencio *Subarrayos binarios con suma* ← Problema de acción
Silencio *prefix sum + hashmap* Silencio Solución más eficiente
Silencioso * ventana deslizante falla*
*O(n) time, O(n) space*
Silencio *coding interview* Silencio Buscar intención para los buscadores de empleo

-...

Problema Recap

``text
Entrada: nums = [1,0,0,1], gol = 2
Producto: 4
`` `

Los cuatro subarrays son:
`` `
[1,0,1], [1,0,1], [0,1,0,1], [1,0,1,0,1] (escrito en negrita/entendido en LeetCode)
`` `

-...

## 📦 Solution Overview

El ingenuo `O(n2)` doble bucle funciona pero es demasiado lento para 30 k elementos.
Una ventana * deslizante* funciona sólo para números **positivos**; ceros lo rompen.
La manera óptima es utilizar **prefix sums + un mapa de hash**:

1. Compute running prefix sum `currSum`.
2. Para cada índice, el número de subarrays que terminan en `i` con suma `goal` equivale
"count[curr] Sum - goal]` (cuántas veces ha aparecido la suma anterior necesaria).
3. Actualizar "count[currSum]++ " para futuros índices.

Esto funciona en **O(n)** tiempo y **O(n)** espacio auxiliar.

-...

##  Settlements Code Implementations

A continuación se muestran los snippets limpios, listos para la producción en **Java**, **Python**, y **C+**.

#### ## 1down⃣ Java

``java
importa java.util. HashMap;
importa java.util. Mapa;

Solución de la clase pública {}
*
* Cuenta el número de subarrays no vacíos de una matriz binaria con suma == gol.
*
* @param nums array binario (elementos son 0 o 1)
* gol @param Suma fija
* @return Number of eligibleing subarrays
*/
int public int numSubarraysWithSum(int[] nums, int goal) {
/ / prefijo suma - título mapa de frecuencia
Mapa seleccionadoInteger, Integer frecuentementeq = nuevo HashMap Quería();
freq.put(0, 1); // prefijo vacío

int currSum = 0;
int result = 0;

para (int num : nums) {
currSum += num;
// Subarrays terminando aquí con sum=goal
resultado += freq.getOrDefault(currSum - goal, 0);
// Grabar la suma de prefijo actual
freq.put(currSum, freq.getOrDefault(currSum, 0) + 1);
}
Resultado de retorno;
}
}
`` `

#### 2down⃣ Python

``python
de las colecciones importadas por defecto
de la importación Lista

Solución de clase:
def numSubarrays ConSum(self, nums: List[int], goal: int) - título int:
"
Cuenta subarrays de una matriz binaria cuya suma equivale a gol.
"
pref_count = defaultdict(int)
pref_count[0] = 1 # prefijo vacío
curr_sum = 0
res = 0

para n en nums:
curr_sum += n
res += pref_count[curr_sum - goal] # subarrays terminando aquí
pref_count[curr_sum] += 1

retorno
`` `

#### 3down⃣ C++

``cpp
Incluido el título
#include ■unordered_map Conf
usando std namespace;

Clase Solución {
public:
int numSubarraysWithSum(vector identificadoint compartir nums, int goal) {}
unordered_map observadoint, long long long long frecuenciaq; // use long long long for large counts
freq[0] = 1; // prefijo vacío
currSum largo = 0, ans = 0;

para (int num : nums) {
currSum += num;
auto = freq.find(currSum - goal);
if (it != freq.end()) ans += it- confíasecond;
freq[currSum]++; //
}
volver estática_cast seleccionado(ans)
}
};
`` `

■ **¿Por qué 'largo' en C++? #
> `n` puede ser de 30 k, por lo que el número de subarrays puede alcanzar ~450 M. Una entrada de 32 bits se desbordaría.

-...

## 🚀 Performance

Silencio Idioma Silencio Tiempo Complejidad
Silencio--------------------------
TEN Java TENIDO O(n) TENIDO O(n) TENIDO Usos `HashMap` TEN
Silencio Python Silencio O(n) Silencio O(n) Silencio
TENIDO C++ TENIDO O(n) ANTERIOR O(n) TENIDO `unordered_map`

Los tres pasan el límite de elementos 3 × 104 en milisegundos.

-...

## The Good, Bad, Ugly

Silencio Silencio
Silencio------------Prince------
Silencio ** Idea Algorítmica** Silencio Suma Prefix + hashmap es O(n) – *el estándar “bueno”* Silencio La ventana deslizante falla con ceros – * error de entrevista común* latitud Ninguno una vez que se conoce el enfoque correcto
Silencio ** Casos de Edge** Silenciosos Handles `goal == 0`, todos los ceros, todos los que viven Olvídate de pre-poblar `freq[0] = 1` causa off‐by‐one  permanente Respuesta grande desbordamiento si la int se utiliza (C++) Silencio
Silencio **Readability** Silencio Nombres variables claros, comentarios en línea Silencio Algunas soluciones utilizan bucles anidados → difícil de seguir Silencio Extremadamente soluciones terse sin comentarios se vuelven irreparables
Silencio **Testing** Silencio Verificar con `goal = 0` y arrays aleatorios ¦ Failing para probar con todos los ceros conduce a errores ocultos ← No usar 'long' para los conteos → silencioso rebosamiento

### Qué evitar

- **Naïve O(n2)**: todavía pasa pequeñas pruebas pero TLE en entrada máxima.
- **Venta deslizante**: Funciona sólo para números positivos; ceros rompen el invariante.
- **Over-optimization**: Removing the hash map for speed hurts correctness.

### Qué hacer hincapié en las entrevistas

- Explicar *por qué* prefijo suma ayuda: reducimos el problema de la suma de subarray a una diferencia de dos prefijos.
- Mostrar que los ceros se manejan sin problemas - cada cero aumenta la misma suma de prefijo, por lo que el mapa de hash cuenta correctamente múltiples subarrays que terminan en diferentes índices.
- Discutir el cambio: O(n) tiempo vs. O(n) memoria extra.

-...

## ❌ Entrevista‐Ready Takeaway

1. **Understand the Problem** – El array es binario, por lo que las sumas prefijo son pequeñas.
2. **Pick the Right Algorithm** – Prefix sum + hashmap = tiempo lineal, espacio lineal.
3. **Write Clean Code** – Usar nombres descriptivos, comentar la lógica y manejar casos de borde.
4. **Test Extensivamente** – `goal = 0`, todos los ceros, todos ellos, conjuntos de elementos únicos.
5. **Explicar en palabras** – Articular la solución durante la entrevista: “Mantenemos una suma en ejecución; cada vez que vemos la misma suma de nuevo, encontramos un subarray que suma a cero, etc. ”

-...

## 📄 Blog Article: “Binary Subarrays With Sum – The Interview‐Winning Solution”

■ *Título*
■ *LeetCode 930: Binary Subarrays With Sum – O(n) Solution (Java, Python, C++)*

■ **Meta Descripción**
■ Maestro LeetCode 930 en minutos! Aprenda la solución óptima de mapas prefijo-sum en Java, Python y C++. Perfeccione sus habilidades de entrevista con código claro, manejo de bordes y contenido optimizado SEO.

### 1. Introducción

■ En entrevistas de codificación, LeetCode 930 (“Subarrayos Binarios con Sum”) es un problema popular de media-dificultad. Prueba su capacidad para convertir un requisito de summación en un escaneo lineal con un mapa de hash. Este artículo te lleva a través de las partes **buena**, **bad**, y **muy** del problema, proporciona código limpio en tres idiomas principales, y ofrece explicaciones de estilo de entrevista.

### 2. Declaración de problemas

■ * Entrada*: `nums` - matriz binaria (`0` o `1`), longitud hasta 30 000.
■ * Objetivo*: Cuenta subarrays donde la suma es igual a `goal ' .
■ *El objetivo* varía de 0 a `nums.length`.
■ *Output*: Integer count of qualifieding subarrays.

### 3. Pitfalls comunes

Por qué no soporta el ejemplo
Silencio----------------------------
Silencio Usando una ventana deslizante Silencio Zeros rompe la propiedad "principalmente creciente" de la ventana suma Silencioso `[0,0,1]`, gol = 1 → fallas
Silencio O(n2) fuerza bruta ← Time Limit Exceed on large input TEN 30 k elements → 450 M iterations ANTE

### 4. El enfoque óptimo: Suma prefijo + mapa de Hash

- **Idea**: Que `prefix[i]` sea la suma de los primeros 'i' elementos.
- **Observación**: Un subarray `(l, r]` suma a `goal` iff `prefix[r] - prefijo[l] = gol`.
- **Implementación**: Para cada `prefijo[r]`, mira cuántas veces `prefijo[r] - meta` ha aparecido antes.

■ **Tiempo**: O(n)
■ **Espacio**:

### 5. Code Walkthrough (Java)

``java
int public int numSubarraysWithSum(int[] nums, int goal) {
Mapa seleccionadoInteger, Integer frecuentementeq = nuevo HashMap Quería();
freq.put(0, 1); // prefijo vacío

int sum = 0, ans = 0;
para (int n : nums) {
suma += n;
ans += freq.get OrDefault(sum - goal, 0);
freq.put(sum, freq.getOrDefault(sum, 0) + 1);
}
devolver los ans;
}
`` `

* Puntos clave*:
- `freq[0] = 1` maneja subarrays que comienzan en el índice `0`.
- `sum - gol` es el *prefijo objetivo* que necesitamos haber visto antes.

### 6. Python & C++ Variantes

■ (Mostrar el anterior proporcionado snippets.)

### 7. Lista de verificación Edge‐Case

Silencio Test ← Esperado Silencio ¿Por qué importa
Silencio...
Silencio `goal = 0`, todos los ceros  durable `n*(n+1)/2` Silencio Cero resume muchos subarrays  durable
Silencio `goal = 0`, mixto Silencio Cuentas subarrays de sólo ceros Silencio No debe contar subarrays con los que permanecen
Silencioso `goal = n`, todos los que están en la vida 1
Silencio Elemento único tención 1 si es igual a la meta 0 ← Entrada mínima sanidad

### 8. Entrevista - Puntos

1. *Explicar* la intuición prefijo-sum.
2. *Mención* la necesidad del primer `freq[0] = 1`.
3. *Discuss* time/space trade‐offs.
4. *Mostrar* la solución en su idioma preferido.

### 9. Conclusión

■ LeetCode 930 es un ejemplo clásico donde un uso inteligente de estructuras de datos convierte un problema de otro modo cuadrático en lineal. Dominar este patrón no sólo le da un algoritmo listo para el trabajo, sino que también demuestra a los entrevistadores que usted puede pensar críticamente bajo restricciones.

-...

## 🎯 Final Checklist for Your Job Hunt

- ✅ Incluya el código en su cartera (Java, Python, C++).
- ✅ Escribe un breve blog (como el anterior) y lo acoge en Medium/Dev.to.
- ✅ Añadir el artículo a tu GitHub README con etiquetas: `#leetcode #930 #binary-subarrays`.
- ✅ Practice explicando la solución en voz alta (entrevista de memoria).
- ✅ Optimize for SEO: add keywords, meta tags, backlinks.

Buena suerte: sus entrevistadores apreciarán la solución limpia y eficiente y las explicaciones claras!