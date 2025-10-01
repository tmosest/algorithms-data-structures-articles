-...
Título: LeetCode 2089. Encontrar índices de destino después de la clasificación Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Código – “Encontrar índices de destino después de ordenar el Array” (LeetCode 2089)

Silencio Idioma Silencio Código Silencio
Silencio...
Silencio **Java** Налителинилинанилиниханихинанихина.util.*; obedecióbr contactos de la clase pública Solución {нерилиного public List madeintInteger contactos(int[] nums, int target) {יbr confianza // 1 comentarios⃣ Ordenar el array – O(n log n)) obedecbr título Arrays.sort(nums); Lista realizadaInteger confía ans = nuevo ArrayList implicado(); Escaneo lineal para recopilar todos los índices de `target` – O(n) obtenidosbr confianza para (int i = 0; i ' significa nums.length; i++) { indicabr título si (nums[i] == target) ans.add(i); correspondbr título } obedecbr título devolver ans; armonizabr título } Loginbr título} indicabr título {/pre título recomendado/detalles Silencio
Silencio **Python** Нетелилинилиниханиханиханиханихиниханихиниханиханихинанихинанниханинанининияниянияниянияний ниениениениениениениениениениениениениения ниениениениениениениниениениениениениениениениениениениениениениениениениениениениениенининининиениениениениенни Ordenar la lista – O(n log n) Reúne todos los índices en los que el elemento es igual a " objetivo " – O(n) obtenidosbr título [i para i, x en enumerate(nums) si x == target]cantar título recomendado/precursos recomendados/detalles confianza Silencio
iPrincipalmente, no es posible. ++i) {cantar título si (nums[i] == target) ans.push_back(i); correspondbr título }\n devolver ans; armonizabr título } seccionóbr confianza}; se hizo un título/pre indicando/detalles incluidos Silencio

■ ¿Por qué esta solución? * *
■ *Sorting garantiza que los índices del objetivo en la matriz ordenada ya están en orden ascendente. *
■ *La complejidad del tiempo:* `O(n log n)` debido al tipo.
■ * Complejidad del espacio:* `O(m)` donde `m` es el número de ocurrencias de `target` (la lista de respuestas).
■ *Las limitaciones (`n ≤ 100`) hacen que este enfoque esté perfectamente bien, pero también puede resolverlo en `O(n)`. tiempo contando tipo si quieres mostrar optimización avanzada. *

-...

## 2. Artículo del Blog – “LeetCode 2089: Encontrar índices de destino después de ordenar Array – bueno, malo & ugly”

■ **Palabras clave de SEO**: LeetCode 2089, Encontrar índices de objetivos después de ordenar Array, entrevista de codificación, solución Java, solución Python, solución C++, complejidad del tiempo, algoritmo de clasificación, consejos de entrevista, entrevista de trabajo, entrevista de algoritmos.

-...

#### 2.1 Introduction

En el mundo de las entrevistas de ingeniería de software, los problemas de LeetCode son el *show‐stopper* que los reclutadores les encanta lanzar a los candidatos. Una de las adiciones recientes es **LeetCode 2089 – “Encontrar índices de objetivos después de clasificar Array.”** Aunque está etiquetado “Easy”, tiene un giro que lo convierte en un momento de enseñanza perfecto para * surtir*, *escaneo lineal* y *pensamiento algorítmico*.

Si te estás preparando para una entrevista de instrucciones de datos o simplemente quieres pulir tus habilidades Java/Python/C+++, este post te lleva a través del problema, te muestra código limpio en tres idiomas principales, bucea en los trade-offs (el bueno, el malo y el feo), y termina con consejos de trabajo-entrevista.

-...

### 2.2 Declaración de problemas

■ Dado un conjunto entero de `nums ' y un entero `target ' ,
■ **Regresar una lista de todos los índices en los que `target` aparece en `nums` después de que el array se ordena en orden no-disminución. #
■ La lista de respuestas debe ser clasificada en orden ascendente.
■ Si el objetivo nunca aparece, devuelve una lista vacía.

*Examples*

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
TENIDO `[1,2,5,2,3]`, `2` TENIDO `[1,2]` Silencio Clasificado → `[1,2,2,2,3,5]`; indices of `2` are 1 ' TENIDO
[1,2,5,2,3] ``, `3` Silencio `[3]` Silencio ordenado → `[1,2,2,3,5]`; índice de `3` es 3 Silencio
[1,2,5,2,3] ``, `5` Silencio `[4]` Silencio Ordenardo → `[1,2,2,3,5]`; índice de `5` es 4 Silencio

**Constraints* *

* `1 ≤ nums.length ≤ 100`
* `1 ≤ nums[i], target ≤ 100`

Debido a que el array es pequeño, cualquier algoritmo que se ejecuta en `O(n log n)` o incluso `O(n)` pasará. La solución canónica utiliza ** surtido + escaneo lineal**, que es intuitivo y fácil de explicar en una entrevista.

-...

### 2.3 The Good – What Makes Este problema es un clásico

1. **Simplicity & Clarity**
*Sorting an array and then scan for a value is a textbook pattern.* Los entrevistadores aman las preguntas donde existe un enfoque claro y canónico – le permite mostrar un estilo de codificación limpio.

2. **Apoyo lingüístico obligatorio**
*Las soluciones Java, Python y C++ son casi idénticas.* Esto demuestra el pensamiento lingüístico-agnóstico – un valor de los reclutadores de habilidad cuando su equipo utiliza pilas de poliglota.

3. **Conciencia de la complejidad del tiempo**
*Te obligan a hablar sobre `O(n log n)` para clasificar vs. `O(n)` si usas el tipo de cuenta.* Los entrevistadores a menudo buscan esta conciencia.

4. *Manipulación de cajas*
* Resultado vacío, valores duplicados, objetivo fuera de rango.* Este problema te obliga a pensar en casos de borde y a escribir código defensivo.

-...

### 2.4 The Bad – Donde puedes perder puntos

Silencio Pitfall Silencio Por qué Es malo
Silencio--------------------------
Silencio **Asumiendo que `target` está siempre presente** Silencio Devolviendo una lista vacía cuando no lo es te hará perder puntos. Después de ordenar, simplemente devuelva la lista vacía 'ans' si no se encuentra nada. Silencio
Silencio **No ordenar** Silencio Saltar el paso del tipo produce índices incorrectos porque el array no está surtido. Silencio Explicablemente (`Arrays.sort(nums)`, `nums.sort()`, o `std::sort`). Silencio
Silencio **Using O(n2) fuerza bruta** Silencio En un set de prueba más grande, esto sería un tiempo libre. TENCIÓN Póngase en el tipo canónico + enfoque de escaneo. Silencio
Silencio **Ignorando el requisito de “orden surtido”** Silencio Si usted devuelve índices del orden original del array, usted fallará pruebas ocultas. Silencio Asegúrese de que está iterando sobre el array * surtido*. Silencio

-...

### 2.5 The Ugly – Optimizing for Speed & Space

Mientras que `O(n log n)` es aceptable, usted puede afeitar el paso de clasificación completamente:

1. **Counting Sort** –
Desde `nums[i] ≤ 100`, puede crear una matriz de frecuencia de tamaño 101.
Luego, mientras atraviesa los recuentos, mantenga un puntero índice en ejecución para saber dónde aterrizará el objetivo después de ordenar.

2. ** Terminación total** –
Si la matriz ordenada comienza con números más grandes que `target`, usted puede romper temprano.

3. **Respuesta eficiente de la memoria**
En lugar de construir toda la matriz ordenada, puede calcular los índices de inicio y final de 'target` directamente desde la matriz de frecuencia.

■ *¿Por qué hacer esto en una entrevista? *
■ Muestra que estás pensando en * optimización algorítmica* y *problemas*. Pero, si el entrevistador no está buscando micro-optimizaciones, se adhieren al enfoque limpio-y-escan – la claridad gana.

-...

### 2.6 Code Walkthrough (Python)

``python
Solución de clase:
def targetIndices(self, nums: List[int], target: int) - título List[int]:
# 1 Ordenar el array (O(n log n))
nums.sort()
# 2⃣ Reunir índices del objetivo (O(n))
retorno [i para i, x en enumerate(nums) si x == target]
`` `

*Line 3:* La clasificación se hace en su lugar.
*Line 5:* La comprensión de la lista da una respuesta concisa.

-...

### 2.7 Complexity Analysis

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio Ordenación Silencioso `O(n log n)` (en lugar para Python/C++/Java)
Silencio Escáner lineal Silencioso `O(n)` Silencio `O(m)` (lista de respuesta; `m` ≤ `n`) Silencio
Silencio **Total** Silencioso `O(n log n)` Silencio `O(m)` Silencio

Con 'n ≤ 100', el tiempo de ejecución es insignificante, pero la complejidad es la *derecha* que se menciona en una entrevista.

-...

### 2.8 Interview Tips

Silencioso Qué decir Silencio Por qué importa
Silencio--------------------------- La vida eterna
Silencio **Iniciar** Silencio “Yo ordenaré el array primero, y luego analizaré el objetivo”. tención Muestra que está utilizando un patrón estándar. Silencio
Silencio **La complejidad** Silencioso “La ordenación toma tiempo, pero sólo escaneamos una vez”. ← Demonstrates conciencia algorítmica. Silencio
"Si el objetivo no está presente, devuelvo una lista vacía". ← Cubre pruebas ocultas. Silencio
"Porque todos los números son ≤ 100, podríamos usar la forma de contar para obtener 'O(n)`." ← Destaca el conocimiento de las técnicas avanzadas. Silencio
Silencio **Testing** Silencioso “Pruebaré con objetivos duplicados, arrays de un solo elemento y arrays diferentes”. Silencio Muestra minuciosidad. Silencio

-...

### 2.9 Conclusiones

LeetCode 2089 es engañosamente simple, pero empaca una gran lección en * surtido*, *traversal lineal*, y *casos de borde de manipulación*. La solución canónica es un patrón “sort-and‐scan” que es fácil de código y fácil de explicar. Para una entrevista de trabajo, el **bueno** está mostrando código limpio y legible; el **bad** está pasando por alto la necesidad de ordenar; el **engrandecido** está exagerando la solución cuando un enfoque directo es suficiente.

■ **Ley para aterrizar esa entrevista de instrucciones de datos? * *
■ Practique este problema en Java, Python y C++, escriba su propia suite de prueba, y ensaye el “por qué” detrás de cada paso. Los empleadores aman a los candidatos que pueden *explicar* su solución tan claramente como lo codifican.

¡Feliz codificación, y que los dioses de la entrevista estén siempre a su favor!