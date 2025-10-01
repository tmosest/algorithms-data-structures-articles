-...
Título: LeetCode 1865. Encontrar parejas con un determinado sumo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📚 1865 – Encontrar parejas con cierto sumo
**Medium ⋅ LeetCode ← Data‐Structure Design**

*“Quiero mostrar a los reclutadores que puedo convertir un problema complicado en código limpio y reutilizable.”*
■ Aquí hay un paseo completo:
* Problemas "
* Solución elegante (marco de frecuencia basado en jash)
* Java / Python / C++ implementaciones
* Un artículo *blog-ready* que destaca el **bueno, el malo y el feo** – perfecto para LinkedIn, Medium, o su cartera personal.

-...

### 1. Recaptación de problemas

Silencio . .
Silencio...
Silencio **Crear una estructura de datos** que apoye dos operaciones en dos arrays enteros `nums1` y `nums2`: Silencio
1. `add(index, val)` – add `val` to `nums2[index]`. Silencio
Silencio 2. `contra(tot)` – devolver el número de pares `(i, j)` con `nums1[i] + nums2[j] == tot`. Silencio

TENIDO 📌 FORMULADA CONTRATADOS
Silencio...
Silencioso `nums1.length ≤ 1 000`
Silencioso `nums2.length ≤ 105` Silencio
TENIDO `1 ≤ nums1[i], nums2[i] ≤ 105 ` (excepto `nums1[i] puede ser hasta `109`) Silencio
Silencio `add` ' ' llamado ≤ 1 000 veces cada uno. Silencio
TENIDO `0 ≤ índice Silencio
TENIDO `1 ≤ val ≤ 105` Silencio
Ø 109 " Silencio

El objetivo es mantener cada operación rápida – idealmente *O(1)* para `add` y *O(n1)* para `contra`, donde *n1* = `nums1.length`.

-...

### 2. Intuición

1. **Static vs. Dynamic**
*`nums1`* nunca cambia – podemos iterar sobre él en cada `contra`.
*`nums2`* cambios – necesitamos una manera rápida de saber cuántas veces se produce un valor particular.

2. ** Mapa de frecuencia**
Mantenga un hash-map ( " valor → cont " ) para `nums2`.
- **add**: decrementar el recuento del antiguo valor, añadir el recuento del nuevo valor.
- **cuenta**: por cada `x` en `nums1`, mira hacia arriba `tot - x` en el mapa y añade su frecuencia.

3. *Por qué funciona*
Cada búsqueda en el hash‐map es *O(1)* en promedio.
`contra` toca cada elemento de `nums1` una vez → *O(n1)*, que está bien porque `n1 ≤ 1 000`.
`add` is *O(1)*.
Memoria: almacenar frecuencias de los más `105` números diferentes → *O(n2)*.

-...

### 3. Código - 3 idiomas

##### 3.1 Java

``java
importa java.util. HashMap;
importa java.util. Mapa;

clase pública FindSumPairs {
int privado final[] nums1;
int privado final[] nums2;
mapa final privado realizadoInteger, Integer confianza freq; // mapa de frecuencia de nums2

public FindSumPairs(int[] nums1, int[] nums2) {
este.nums1 = nums1;
este.nums2 = nums2;
este.freq = nuevo HashMap Quería();

para (int val : nums2) {
freq.put(val, freq.getOrDefault(val, 0) + 1);
}
}

* Añadir +val a nums2[index] y actualizar el mapa de frecuencia. */
public void add(int index, int val) {
int old = nums2[index];
freq.put(old, freq.get(old) - 1); // decrement old count

nums2[index] += val;
int newVal = nums2[index];
freq.put(newVal, freq.get OrDefault(newVal, 0) + 1); // incremento de cuenta nueva
}

* Devuelve el número de pares (i, j) donde nums1[i] + nums2[j] == tot. */
public int count(int tot) {}
int ans = 0;
para (int a : nums1) {}
int need = tot - a;
ans += freq.getOrDefault(necesidad, 0);
}
devolver los ans;
}
}
`` `

###### 3.2 Python

``python
de las importaciones de colecciones Contrato
de la importación Lista

class FindSumPairs:
def __init__(self, nums1: List[int], nums2: List[int]):
self.nums1 = nums1
auto.nums2 = nums2
auto.freq = Counter(nums2) # mapa de frecuencia de nums2

def add(self, index: int, val: int) - Conf Ninguno.
viejo = self.nums2[index]
self.freq[old] -= 1 # Decremento antiguo valor

auto.nums2[index] += val
new_val = self.nums2[index]
self.freq[new_val] += 1 # Aumento de nuevo valor

def count(self, tot: int) - título int:
volver suma (self.freq[tot - a] para un auto.nums1)
`` `

##### 3.3 C++

``cpp
Incluido el título
#include ■unordered_map Conf

class FindSumPairs {
public:
FindSumPairs(std::vector efectuadoint título nums1, std::vector fielint nums2)
: nums1(std::move(nums1)), nums2(std::move(nums2)) {
para (int v : este- rationums2) freq[v]++; // construir mapa de frecuencia
}

vacio añadir(indice, int val) {
int old = nums2[index];
--freq[old]; // decremento viejo cuenta

nums2[index] += val;
int newVal = nums2[index];
++freq[newVal]; // aumento de cuenta nueva
}

int count(int tot) {}
int ans = 0;
para (int a : nums1) {}
int need = tot - a;
auto = freq.find(neced);
if (it != freq.end()) ans += it- confíasecond;
}
devolver los ans;
}

privado:
std::vector obtenidosint titulada nums1;
std::vector seleccionado noms2
std::unordered_map seleccionadaint, int confianza freq; // value → count
};
`` `

Las tres soluciones comparten el mismo O(1) *add* y O(`nums1.length`) *contra* tiempo, haciéndolos ideales para los límites de LeetCode.

-...

### 4. Blog Artículo – “El bien, el mal”

■ **Target audience**: reclutadores, entrevistadores y compañeros en LinkedIn/Medium.
■ **Palabras clave amigables de SEO**: *LeetCode 1865*, *FindSumPairs*, *data‐structure interview*, *hash map solution*, *O(1) add*, *job interview coding*, *Python Counter*, *C++ unordered_map*, *Java HashMap*.

-...

##### 4.1 Title > Meta

`` `
Identificar el título 1865 – Design a Frequency‐Based FindSumPairs Data Structure
Contenido "Master LeetCode 1865 (FindSumPairs). Aprende un Java limpio, Python, solución C++, análisis de complejidad y consejos de entrevista. Perfecto para entrevistas de codificación y escaparate de cartera."
`` `

#### 4.2 Tabla de contenidos (para legibilidad)

1. [El problema](El problema)
2. [Por qué el truco Hash-Map es la salsa secreta] (#hash-map-sauce)
3. [Algorithm & Complexity](#complexity)
4. [Código Completo](#code)
5. [The Good, The Bad & The Ugly](#pros-cons-ugly)
6. [Consejos de Interview](#interview-tips)
7. [Conclusión " Siguientes pasos](#conclusión)

-...

##### 4.3 El Bien

TENIDO TENIDO ANTERIOR Lo que amaba
Silencio...
TEN **Simplicidad** – un mapa de frecuencia + dos lazos directos. Silencio
Silencio **Información** – *O(1)* `add`, *O(n1)* `contra`. Silencio
tención **Idioma Agnostic** – la misma idea funciona en Java, Python, C++, Rust, Vamos, etc. Silencio
← **Mómory Footprint** – sólo cuenta de 'nums2` se almacenan, no todo el array. Silencio
TEN **Reusabilidad** – se puede adaptar a otros problemas de “frecuencia dinamica + radio estática”. Silencio

##### 4.4 The Bad

ANTE NOVEDAD ANTE LAS POTENCIAS Potenciales
Silencio.
Silencio **Large Frequency Map** – si el `nums2` contiene muchos valores únicos, el unordered_map/Counter puede utilizar hasta ~200 KB por entrada única, que todavía está bien para los números '105' pero vale la pena notar para entradas realmente masivas. Silencio
Silencio **Zero‐Count Keys** – decremos cuenta pero nunca eliminamos las claves cuando el conteo alcanza cero. En un sistema del mundo real es posible que desee prune para mantener el mapa inclinado, pero la sobrecarga extra es insignificante dadas las limitaciones. Silencio
Silencio **Repetición Llamadas** – iterating over `nums1` en cada llamada es *O(n1)*. Si `nums1` fuera más grande, usted necesitaría pre-computar algo más (por ejemplo, una suma prefijo 2-D). Los límites del problema lo mantienen aceptable, pero el entrevistado debe mencionar este intercambio. Silencio

#### 4.5 The Ugly

Silencio 👿 Silencio Casos Edge > Gotchas ocultas
Silencio.
Silencio **Desbordamiento entero** – `t` puede ser hasta `109`. La adición de dos ints en C++/Java puede rebosar si utilizas tipos firmados de 32 bits; el uso de 'long' o 'long' para la suma intermedia es más seguro en idiomas que no tienen ints de precisión arbitraria (JavaScript, C). En este problema las sumas permanecen dentro de 32 bits, pero siempre vigilan los límites. Silencio
tención **Multiple Updates to the Same Index** – Si `add` se llama repetidamente en el mismo índice, asegúrese de que el mapa de frecuencia permanezca en sincronía con el array subyacente. Un error común es olvidar actualizar el array después de decrementar el antiguo conteo. Silencio
¿Números negativos?** – Las restricciones oficiales prohíben los valores negativos, pero si se ajusta el problema para permitirlos, el algoritmo todavía funciona porque el hash‐map puede almacenar claves negativas. Sólo recuerda usar un tipo de entero *signed*. Silencio

-...

#### 4.6 Interview‐Ready Pseudocode

``text
class FindSumPairs:
freq = mapa de los valores nums2

init(nums1, nums2):
construir freq de nums2

add(idx, val):
freq[nums2[idx]...
nums2[idx] += val
freq[nums2[idx]]++

Contando.
res = 0
para x en nums1:
res += freq[tot - x]
retorno
`` `

■ **Por qué es un “show‐off” para los reclutadores* *
* El entrevistador puede ver al instante que utilizó un *hash mapa* para convertir un array dinámico en una mesa de búsqueda estática.
* Usted explicó la *amortizada* *O(1)* actualización, la consulta *O(n1)* y el intercambio espacial.
* Usted mostró métodos limpios y testables, listos para una API de grado de producción.

-...

### 5. Poniéndolo en su cartera

1. **Embed the Code** – copy the Java, Python, and C++ snippets into a README or a GitHub Gist.
2. **Agregue un README** que incluya:
- Declaración de problemas (copia de LeetCode)
- Arnés de prueba (pruebas individuales para los tres idiomas)
- “Pon esto para ver la salida esperada” bloque.
3. **Link It** – en tu enlace In article or on your personal site, add a link: `https://github.com/yourusername/leetcode-1865-findsumpairs`.
4. **Compartir en Medium** – publicar el blog con los encabezados arriba. Tag with `#LeetCode`, `#CodingInterview`, `#DataStructures`, `#AlgorithmDesign`.

-...

### 6. Conclusión

- **LeetCode 1865** es un problema clásico de “design‐a‐data‐structure” que prueba su capacidad de equilibrar **time-complexity** y **memory‐efficiency**.
- El truco de frecuencia **hash‐map** es la solución canónica: actualizaciones O(1), consultas O(n1).
- Las implementaciones en **Java, Python, y C+** son directas y demuestran competencia en lenguaje cruzado.
- The **blog article** above is SEO‐optimized and ready to share—complete with keywords that recruiters love (`LeetCode 1865`, `FindSumPairs`, `Java HashMap`, `Python Counter`, `C++ unordered_map`, `job interview coding`).

 **Siguiente paso:**
Añade tus propias pruebas de unidad, empuja el repo a GitHub y comienza un post de LinkedIn: *“Solved LeetCode 1865 en Java, Python y C++ – aprende cómo diseñé una estructura de datos eficiente”*

Feliz codificación, y la mejor suerte de aterrizar en la próxima entrevista! 🚀