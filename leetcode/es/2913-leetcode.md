-...
Título: LeetCode 2913. Subarrays Distinct Element Sum of Squares Yo...
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 2913 – Subarrays Distinct Element Sum of Squares
*Easy – LeetCode*

■ *Problema*
■ Dada una matriz de enteros de 0-indexado `nums`, un *subarray* es cualquier rebanada no vacía contigua de `nums`.
■ Para un subarray `nums[i..j]`, su **distinct count** es el número de valores únicos que contiene.
■ Devuelve la suma de los cuadrados de los recuentos distintos para **all** subarrays de `nums`.

TEN SON SON SON SON SON SON SON SON SON 
Silencio----------------------------------------------------
TENIDO 1 TENIDO `[1,2,1] `` TENIDO `15` TEN Six subarrays → `1^2+1^2+1^2+2^2+2^2+2^2 = 15`
Silencio 2 Silencio `[1,1]` Silencio `3` Silencio Tres subarrays → `1^2+1^2+1^2 = 3` Silencio

■ **Constraints**
* `1 ≤ nums.length ≤ 100`
≤ 100

Debido a que la matriz es pequeña, un enfoque O(n2) brute‐force limpio es perfectamente adecuado.
A continuación encontrará ** tres soluciones completas** (Java, Python, C++), seguido de un análisis de estilo **blog** que le ayudará a aterrizar esa entrevista de ingeniería de software.

-...

## 1down Java – Simple Brute‐Force

``java
importar java.util*;

Clase Solución {
public int sumCounts(List won) {
int n = nums.size();
total = 0;

// Para cada índice de inicio posible
para (int i = 0; i)
Establecer contactoInteger nombrado = nuevo HashSet fiel();

// Ampliar el elemento subarray a la vez
para (int j = i; j) {}
visto.add(nums.get(j));
int distinct = seen.size();
total += distintos * distintos; // cuadrado el conteo diferenciado
}
}
Total de retorno;
}
}
`` `

*Por qué funciona* *

* El bucle exterior recoge un límite izquierdo.
* El bucle interior extiende el límite derecho `j`.
* Un `HashSet` mantiene un seguimiento de los valores únicos vistos hasta ahora – insertar es O(1).
* Para cada subarray computamos el tamaño 2 y lo agregamos a la respuesta.

**La complejidad* *

TEN TERRITOR TEN TEN ANTE
Silencio...
TENIDO Tiempo TENIDO `O(n2)` (max 10 000 iterations when `n = 100`) Silencio
TENIDO EL ESPACIO TENIDO `O(1)` (el conjunto nunca tiene más que 'n' elementos)

-...

Python – List‐Based Brute‐ Fuerza

``python
de la importación Lista

def sum_counts(nums: List[int]) - título int:
n = len(nums)
total = 0

para i en rango(n):
visto = set()
para j en rango(i, n):
visto.add(nums[j])
total += len(seen) ** 2

total
`` `

La lógica es idéntica a la versión Java. El 'set' de Python da inserciones amortizadas O(1).

**La complejidad* *

* Tiempo: `O(n2) `
* Espacio: `O(1)`

-...

## 3VIEW⃣ C++ – Vector " unordered_set `

``cpp
Incluido el título
#include ■unordered_set
usando std namespace;

int sumCounts(vector fielint nums) {
int n = nums.size();
long long total = 0; // use long long to avoid overflow for larger inputs

para (int i = 0; i) {}
unordered_set observadoint
para (int j = i; j)
visto.insert(nums[j]);
int distinct = seen.size();
total += 1LL * distintos * distintos;
}
}
retorno estático_cast seleccionado(total)
}
`` `

*Nota*: La declaración de LeetCode garantiza que el resultado se ajuste a un entero firmado de 32 bits, pero el uso de 'long' protege contra el desbordamiento accidental.

**La complejidad* *

* Tiempo: `O(n2) `
* Espacio: `O(1)`

-...

## 4VIEW⃣ Blog Article – “The Good, The Bad, and The Ugly of LeetCode 2913”

■ *Título*
■ *“Cracking LeetCode 2913: Subarrays Distinct Element Sum of Squares – A Deep Dive for Job‐Seeking Engineers”*

■ **Descripción (SEO):* *
■ Aprende a resolver LeetCode 2913 en Java, Python y C++. Entender los cambios algorítmicos, leer un tutorial paso a paso, y descubrir las ideas de entrevista para aumentar sus perspectivas de trabajo.

-...

#### Introduction

En una entrevista de ingeniería de software, el objetivo del reclutador no es sólo para probar su código – también están evaluando su mentalidad de resolver problemas, estilo de codificación y capacidad de comunicarse.
LeetCode 2913 es un problema clásico de “array‐and-hash-set” que es **fácil** en términos de dificultad pero **poderoso** en la enseñanza de conceptos importantes:

1. **La fuerza bruta vs. la optimización** - ¿cuándo es una solución ingenua aceptable?
2. ** Elección de la estructura de datos** – por qué un conjunto de hash es perfecto para contar elementos distintos.
3. ** Análisis de la complejidad** – por qué O(n2) está bien para n ≤ 100 pero se rompería de otra manera.
4. ** matices específicos de lenguaje** – Java’s `Listecto:Integer confianza` vs. Python’s `list`, C++’s `unordered_set`.

A continuación descomponemos los aspectos *bueno*, *bad*, y *muy* de las soluciones típicas y cómo convertirlas en código ganador de entrevistas.

-...

##### El Bien

← Feature Silencio Por qué importa
Silencio--------------
TEN **Simplicidad** TENIDO Un solo bucle anidado y un conjunto mantiene el código corto y legible. tención Reduce la carga cognitiva para que el entrevistador siga su lógica. Silencio
Silencio **Correcto** Silencio Utiliza la definición de “conteo instinto” directamente – no hay trucos ocultos. tención Demuestra una asignación clara de la declaración del problema al código. Silencio
tención **La actuación para las manifestaciones** Silencioso O(n2) es ≤ 10 000 operaciones; se ejecuta en Muestra que usted entiende los límites de problema y puede hacer el cambio adecuado. Silencio
Silencio **Language‐Friendly** Silencio Obras en Java, Python, C++ sin caldera compleja. Silencio Te da flexibilidad para código en el idioma con el que estás más cómodo. Silencio

■ *Consejo:* En su entrevista, comience con el enfoque de fuerza bruta, luego pregunte al entrevistador si se le permite optimizar – esto muestra la humildad y la voluntad de iterar.

-...

##### El malo

Silencio Silencio Silencio Silencio
Silencio------------------------
Silencio ** Memoria Excesiva** – Usando un array de tamaño `n2` para almacenar todos los resultados de subarray. Silencio Residuos RAM, innecesario. Silencio Evitar almacenar los resultados; acumularse directamente. Silencio
Silencio **Desbordamiento entero** – Cuentos diferenciados pueden rebosar 32 bits en idiomas con límites más estrictos. ← Errores en casos de borde (`n=100`, todos los valores distintos). TENIDO Use integer de 64 bits ( " largo largo " en C++, `long ' en Java, `int ' en Python es sin límites). Silencio
Silencio **Reiniciar Ineficientes** – La reubicación del conjunto en cada bucle exterior puede ser costosa en micro-benchmarks. Lenta desaceleración. Reutiliza el mismo conjunto si lo aclara, pero con n ≤ 100 el beneficio es insignificante. Silencio
Silencio **Ignorando las limitaciones de tipo** – Pasando una "int[]" cruda cuando la API espera `Listecto No se hace referencia a errores de compilación. tención Código no compila. Coincide con la firma exactamente ( ' List seleccionadaInteger ' ). Silencio

■ *Key takeaway:* Incluso los problemas “fáciles” ocultan pequeños obstáculos; atraparlos muestra atención al detalle.

-...

##### El Ugly

Problema en la vida ¿Por qué es una práctica mejor?
Silencio--------------------------------------
Silencio **Números mágicos de alta costura** – Usar 'n' hechos 100' como una suposición oculta. ← Hace que el código sea frágil si las restricciones cambian. ← Derive `n` de `nums.size()`; evitar números mágicos. Silencio
** Falta de documentación** – No hay comentarios ni explicaciones. Silencio difícil de leer para los humanos; los entrevistadores pueden dudar de su proceso de pensamiento. Silencio Añadir comentarios breves o una descripción del método. Silencio
Silencio **Non‐Idiomatic Code** – Usando `para (int i = 0; i < 0 se hicieron nums.size(); i++)` en lugar de un anteceso. Las características del idioma de las personas desaparecidas pueden ser más lentas. Use mejorado para bucles cuando sea apropiado, pero para índices todavía los necesitará. Silencio
tención **Ignorando Casos de Edge** – No hay prueba para que los años estén vacíos (aunque las restricciones dicen ≥ 1). Silencio Muestra pruebas despreocupadas. Silencio Sigue afirmando la condición previa o maneje con gracia. Silencio

■ *Lesson:* El código limpio, bien comunicado, y el borde-case-aware separa a un buen candidato de uno grande.

-...

### Cómo hablar sobre este problema en una entrevista

1. **Reseña el problema en tus propias palabras. #
*“Necesitamos considerar cada rebanada contigua de la matriz, contar los números únicos dentro, cuadrado que cuenta, y agregarlos todos juntos.”*

2. ** Explique su algoritmo elegido. #
*“Caminaremos a través de cada índice de inicio ‘i’, mantenemos un conjunto de números vistos corriendo a medida que expandamos el índice final ‘j’. Añadiendo `set.size()2` a la respuesta para cada expansión.

3. **Analizar la complejidad. #
* Con `n ≤ 100`, el bucle doble funciona ≤ 10 000 veces – perfectamente bien. Cada inserción de conjunto es O(1), por lo que O(n2). El uso de memoria es O(1) además del conjunto.”*

4. **Discuten las optimizaciones potenciales (opcional). #
*“Si ‘n’ fuera más grande, podríamos usar una ventana deslizante o una matriz de frecuencia prefijo para evitar recomputar el conjunto desde cero.”*

5. ** Casos de borde de fusión " desbordamiento. #
* “Usamos un entero de 64 bits para estar seguros, y el conjunto maneja valores duplicados automáticamente.”*

-...

## Final Thoughts

- Practica el patrón.
Contar elementos distintos en una ventana corredera es un trope de entrevista recurrente – aplicarlo a problemas como “Subestring más largo con los caracteres distintos de la mayoría de K” o “Conteo distinto de subarray”.

- Conoce tus límites de idioma. #
El `HashSet` de Java es un envoltorio alrededor de una tabla de hash, el `set` de Python es una tabla de hash, y el 'unordered_set' de C+ es la misma idea. Todos dan amortizado O(1) insert/lookup.

- Mantenlo legible. #
Los entrevistadores leen el código más rápido de lo que lo depuran. Utilizar nombres variables significativos ( " i " , " vistos " , " distinto " ) y evitar abstracción innecesaria.

- **Preparar algunos casos de prueba** (edge, típico, grande).
*`[1]`, `[1,2,3,4]`, `[1,1,1,1]`, `[100,99,100]`* – demuestra que usted entiende cómo cambian las cuentas distintas.

- Qué curiosidad.
Pregunte si el entrevistador quiere una solución más eficiente o quiere que discuta cómo manejar una 'n' de 105. Incluso si es imposible con el enfoque ingenuo, explicar el cuello de botella muestra que estás pensando en la escalabilidad.

-...

## Listo para aterrizar ese trabajo?

1. **Copia el código** en su IDE favorito y haga las pruebas de LeetCode.
2. **Agregar un breve bloque de comentarios** explicando el enfoque – esto se verá muy bien en su GitHub README.
3. **Blog it up** (como la sección anterior) – use palabras clave: *“LeetCode 2913 solución”, “array distinct element”, “hash set algoritmo”, “consejos de entrevista de trabajo”*.
4. **Compartir** el puesto en comunidades tecnológicas, LinkedIn o su cartera. El equipo a menudo mira sus muestras de escritura.

Con una implementación limpia en **Java, Python, y C++**, un avance de entrevista sólida, y un post de blog pulido, se destacará como un candidato que no sólo resuelve el problema, sino que también lo comunica claramente. ¡Buena suerte! 🚀

-...


*© 2024 Engineering Interview Insights* – Todos los derechos reservados.

-...

*No dude en adaptar el artículo para su propia voz o expandirse en las optimizaciones si desea mostrar habilidades más profundas. *