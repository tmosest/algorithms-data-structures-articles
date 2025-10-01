-...
Título: LeetCode 2420. Encontrar todos los buenos índices -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. LeetCode 2420 – Encontrar todos los índices buenos
** Idiomas:** Java Silencio Python Silencio C++
*La complejidad* **Tiempo** O(n) **Espacio** O(n) (puede reducirse a O(1) con un truco de ventana deslizante)

-...

#### 1.1 Problema de recuperación

Dado un array `nums` (size `n`) y un entero `k`, un índice `i` is **good**

* `k ≤ i
* Los " elementos k " antes* " están en orden no creciente**
* The `k` elements *after* `i` are in **non-decreasing**

Devuelve todos los índices buenos en orden ascendente.

■ *Ejemplo*
■ `nums = [2,1,1,3,4,1], k = 2 → [2,3]`

-...

#### 1.2 Intuición

La forma ingenua compararía cada ventana de longitud 'k' alrededor de cada candidato 'i' - que es O(n k) y TLE.
La clave es **pre-computación** cuánto tiempo una carrera de monotona se extiende desde cada posición:

Silencio lado izquierdo Silencio lado derecho
Silencio...
Silencio Por cada índice `I` store `decLeft[i]` – ¿Cuántos elementos consecutivos que no aumentan terminan en “i” (incluyendo “i”.). Silencio
TENIDO Por cada índice `I` tienda `incRight[i]` – ¿Cuántos elementos consecutivos que no disminuyen comienzan en “i” (incluyendo “i”.). Silencio

Una vez que tengamos esos dos arrays, el índice `i` es buen iff
`decLeft[i-1] ≥ k` **y** `incRight[i+1] ≥ k`.

Ambos arrays se construyen en un escaneo lineal cada → O(n) tiempo, O(n) memoria.
El cheque para cada candidato es O(1), por lo que todo el algoritmo es tiempo O(n), memoria O(n).

-...

#### 1.3 Implementation

A continuación se muestran implementaciones limpias y comentadas en **Java, Python y C+**.

-...

##### 1.3.1 Java

``java
importar java.util*;

Solución de la clase pública {}
public List (0)Integer correctamenteIndices(int[] nums, int k) {
int n = nums.length;
Lista de datos:Integer confianza res = nuevo ArrayList correctamente();

// 1. matriz de prefijo: longitud de la carrera no creciente final en i
int[] decLeft = nuevo int[n];
decLeft[0] = 1; //
para (int i = 1; i) {}
decLeft[i] = (nums[i - 1] ⇩= nums[i]) ? decLeft[i - 1] + 1 : 1;
}

// 2. matriz de sufijo: longitud de la carrera no disminuyendo a partir de i
int[] incRight = new int[n];
incRight[n] - 1] = 1;
para (int i = n - 2; i 0; i--) {
incRight[i] = (nums[i] י= nums[i + 1]) ? incRight[i + 1] + 1 : 1;
}

// 3. comprobar cada centro posible
para (int i = k; i) = n - k - 1; i++) {
(decLeft[i) - 1] k " aplique incRight[i + 1] √= k) {}
res.add(i);
}
}

restitución;
}
}
`` `

-...

##### 1.3.2 Python

``python
de la importación Lista

Solución de clase:
def goodIndices(self, nums: List[int], k: int) - List[int]:
n = len(nums)

# prefijo: más larga carrera no creciente terminando en i
dec_left
dec_left[0] = 1
para i en rango(1, n):
dec_left[i] = dec_left[i - 1] + 1 si nums[i - 1]

# Sufijo: la carrera más larga no disminuyendo comienza en i
inc_right = [0]
inc_right[-1] = 1
para i en rango(n - 2, -1, -1):
inc_right[i] = inc_right[i + 1] + 1 si nums[i] 1]

# Recopilar buenos índices
ans = []
para i en rango(k, n - k):
si dec_left[i - 1] k and inc_right[i + 1] √= k:
ans.append(i)
Retorno
`` `

-...

#### 1.3.3 C++ (C+17)

``cpp
Incluido el título
#include ■string
usando std namespace;

Clase Solución {
public:
vector identificador buenoIndices(vector fieltro nums, int k) {
int n = nums.size();
vector implicado decLeft(n), incRight(n);

// prefijo
decLeft[0] = 1;
para (int i = 1; i) {}
decLeft[i] = (nums[i-1] н= nums[i]) ? decLeft[i-1] + 1 : 1;
}

/ Sufijo
incRight[n-1] = 1;
para (int i = n-2; i 0; --i) {
incRight[i] = (nums[i] 0 = nums[i+1]) ? incRight[i+1] + 1 : 1;
}

vector significar uns
para (int i = k; i) = n-k-1; ++i) {
si (decLeft[i-1] k " aplique incRight[i+1] k)
as.push_back(i);
}
devolver los ans;
}
};
`` `

-...

## 2. Blog Artículo – “El Bien, el Mal, y el Ugly de LeetCode 2420”

■ **Título**: *“LeetCode 2420 – Encuentra todos los índices buenos: el bien, el mal y el ugly”*
■ **Target Palabras clave**: LeetCode 2420, Encontrar todos los índices buenos, entrevista de algoritmos, solución Java, solución Python, solución C++, codificación de entrevistas de trabajo

-...

#### 2.1 Introduction

Si estás buscando un papel de ingeniería de software, probablemente has mirado los mismos problemas de LeetCode una y otra vez. Una de esas preguntas de nivel medio es **2420. Encontrar todos los buenos índices**. Aunque la declaración es directa, las soluciones ingenuas pueden ser engañosamente lentas.

En este artículo pasaremos por:

1. **Lo que hace que este problema sea “bueno”** – por qué es una gran pregunta de entrevista.
2. **La buena solución** – un enfoque limpio de DP/prefix‐suffix (Java/Python/C++).
3. **Los malos enfoques** – trampas comunes que conducen a TLE o MLE.
4. **El feo** – casos de borde y cómo manejarlos sin exageración.
5. **Recogidas prácticas** para su próxima entrevista.

-...

### 2.2 ¿Por qué este problema es el estudio profundo

Por qué importa una entrevista
Silencio...
Silencio **Array + Dos Pointer DP** Silencio Demuestra que puede transformar una “O(n·k)” fuerza bruta ingenua en una solución O(n). Silencio
Silencio **Monotonic Runs** Silencio muestra comprensión de las técnicas de prefijo/suffix – un elemento básico en muchos problemas de entrevista. Silencio
Silencio **Space/Time Trade‐offs** Silencioso oportunidad para discutir la reducción de la memoria O(n) a O(1) con una ventana deslizante. Silencio
Silencio **Edge‐case Awareness** Silencio `k = 1`, array de todos los números iguales, array con picos alternantes – bueno para la discusión. Silencio

-...

### 2.3 La Buena Solución – Prefijo + Sufijo DP

*Core Idea*
*Pre-compute, para cada índice, hasta qué punto la propiedad monotona se extiende en ambos lados. *

1. **Prefijo izquierdo** – `decLeft[i]`: longitud del subarray no creciente más largo que termina en `i.
``text
decLeft[i] = (nums[i-1] н= nums[i]) ? decLeft[i-1] + 1 : 1
`` `
2. **Sufijo derecho** – `incRight[i]`: longitud del subarray no disminuyente más largo que comienza en `i.
``text
incRight[i] = (nums[i] 0 = nums[i+1]) IncRight[i+1] + 1 : 1
`` `
3. *Comprobar a cada candidato* – para ‘k ≤ i’
``text
si decLeft[i-1] ≥ k e incRight[i+1] ≥ k → i is good
`` `

**Por qué funciona* *
El lado izquierdo de un buen índice debe contener " k " elementos consecutivos que nunca suben. Eso significa exactamente que la carrera que termina en 'i-1' es al menos 'k'. La misma lógica se aplica al lado derecho.

**Las complejidades* *
- **Hora**: `O(n)` (dos escaneos lineales + un cheque lineal)
- **Espacio**: `O(n)` para los dos arrays auxiliares (puede ser recortado a O(1) si prefiere la versión de ventanilla deslizante).

*Code snippets*
*(ver las implementaciones Java, Python y C++ arriba)*

-...

### 2.4 Los malos enfoques – saltos comunes

Por qué no soporta
Silencio------------
Silencio **La fuerza bruta anida los bucles** – para cada `i` escaneo izquierda `k ' elementos y derecha `k ' elementos Silencio O(n·k) → TLE cuando `n` = 105 y `k ' Ô n/2 Silencio
Silencio **Using `ArrayListecto:Integer confianza` para prefijos sin pre-alubicación** Silencioso extra, pero no catastrófico. Silencio
tención **Incorrect index bounds** – errores fuera de uno al acceder a `decLeft[i-1]` o `incRight[i+1]` Silencio conduce a `ArrayIndexOutOfBoundsException`. Silencio
Silencio **Misinterpretar “no aumentar” vs “no disminuir”** vivir los signos de comparación rompe la lógica. Silencio

**Takeaway:**
Siempre las condiciones de doble control de límites; el problema restringe explícitamente " a " k ≤ i " identificado n-k " .

-...

### 2.5 The Ugly – Edge Cases & Corner Conditions

Silencio Caso Edge Silencio Qué ver para Silencio
Silencio------------------
Silencio `k = 1` Silencio El requisito de la longitud de ejecución se vuelve trivial; todavía hay que asegurarnos de que no acceda a índices fuera de límites. Mantenga los bucles como 'k ≤ i' = n-k-1`. Silencio
tención Array de números iguales Silencio Cada lado satisfies monotonicidad; respuesta es todos los índices en rango. Las fórmulas DP manejan correctamente las comparaciones de ` ' y ` ' realizadas= ' . Silencio
TENIENTES TERRITORALES ( " 1 3 2 4 3 5 ... " ) Los arrays DP serán `1`; algoritmo devuelve la lista vacía como se esperaba. Silencio
tención longitud exactamente `2·k + 1` Silencio Sólo un candidato `i = k`. Silencio El bucle sigue funcionando; asegúrese de que no se pierda el último valid `i`. Silencio
Silencio Grande `n` pero pequeño límite de memoria (por ejemplo, 256 MB) Silencio Dos arrays enteros podrían consumir ~8 MB cada → todavía bien. ← Si está ajustado, implemente la ventana deslizante O(1): mantenga sólo las longitudes actuales de `k`-run mientras se escanea. Silencio

-...

### 2.6 Consejos prácticos para su entrevista

1. ** Explique su plan primero** – escriba los dos pases de DP en la pizarra antes de codificación.
2. ** Destacar la optimización O(n)** – los entrevistadores les encanta escuchar “Evité los bucles anidados. ”
3. ** Optimización espacial de la mención** – mostrar conciencia de la variante O(1).
4. ** Pruebas de debate** – pida al entrevistador que ayude a pensar en casos de esquina.
5. **Mantenga su código legible** – incluso en una entrevista, nombres de variables limpios (`decLeft`, `incRight`) y ayuda lógica concisa.

-...

### 2.7 Conclusiones

LeetCode 2420 es un problema de “medio” que esconde un truco de DP limpio. La solución **buena** es un enfoque prefijo de libro de texto que funciona en tiempo lineal. Los enfoques **bad** te enseñan a cuidar de TLE y de los bichos. Los casos de borde **ugly** nos recuerdan que incluso un algoritmo limpio puede fallar si te pierdes un solo límite.

Dominar este problema te da un patrón reutilizable – prefijo/suffix para las restricciones monotónicas – y demuestra que estás listo para asumir retos de entrevistas en el mundo real. ¡Feliz codificación y buena suerte en tu próxima entrevista técnica!

-...

### 2.8 Recursos > Leer más

- LeetCode Discusión sobre el problema 2420
- “Algoritmic Toolbox” – Prefix & Suffix Techniques
- “Cracking the Coding Interview” – Two‐Pointer DP ejemplos
- GitHub Gist con las tres soluciones de idiomas (Java, Python, C++)

-...

*Author*: *Su nombre*, *Software Engineer " Tech Recruiter*
*Publicado en*: *2024‐04‐27*

-...

■ **Meta‐Note**: El artículo está estructurado para proporcionar valor a los lectores que podrían estar en la valla sobre la dificultad del problema, y termina con estrategias de entrevistas factibles. Al incorporar las palabras clave de destino naturalmente en los encabezados, texto corporal y comentarios de código, el artículo es SEO-friendly y listo para clasificar en motores de búsqueda para las etiquetas especificadas.