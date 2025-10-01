-...
Título: LeetCode 1764. Form Array by Concatenating Subarrays of Another Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recapitulación de problemas (LeetCode 1764)

■ **Form Array by Concatenating Subarrays of Another Array* *
■ Dado un conjunto de 2-D `grupos` y un array `nums`, ¿puedes elegir `n` *disjoint* sub-arrays de `nums` para que el sub-array *i-th* iguale `grupos[i]` y el orden se conserva?
■ Volver **verdad** si es posible, de lo contrario **falso**.

* `1 ≤ groups.length ≤ 103`
* `1 ≤ groups[i].length, sum(groups[i].length) ≤ 103 `
* `1 ≤ nums.length ≤ 103`
* Elementos encajan en un entero firmado de 32 bits.

-...

## 2. Core Idea

Necesitamos escanear `nums` una vez e intentar localizar a cada grupo en orden.
Una simple ventana corredera de 2 puntos* basta:

1. Mantenga un índice 'pos' apuntando al siguiente elemento no comprobado en 'nums'.
2. Para el actual `grupo` tratar de coincidir con él carácter‐por-character:
* Si el elemento actual coincide, avance ambos punteros.
* Si se produce un desajuste, vuelva a rodar `pos` al siguiente elemento después del inicio original de esta ventana y reinicie coincidiendo con el grupo actual.
3. Si logramos coincidir con un grupo, `pos` se convierte en el índice sólo ** después de** el sub-array emparejado.
Continúe con el próximo grupo.

Si en cualquier momento un grupo no puede ser encontrado, devolvemos `false`.
De lo contrario, si todos los grupos están emparejados, devuelve `verdad ' .

El algoritmo se ejecuta en `O (las vidas eternas sometidas a la práctica de los subgrupos tiempo (caso peor cuando cada grupo es largo y coincide casi por todas partes) pero con los límites dados es lo suficientemente rápido.
El uso de memoria es `O(1)` más allá de los arrays de entrada.

-...

## 3. Implementaciones de referencia

## 3.1 Java – Ventana deslizante

``java
importar java.util*;

Solución de la clase pública {}

// Devuelve el índice en nums justo después del grupo emparejado.
// Si no se encuentra, regrese -1.
int particularGroup(int[] group, int[] nums, int start) {
int n = nums.length;
int m = group.length;
int i = start, j = 0;

mientras (i
(nums[i] == group[j]) {}
i++; j++;
si (j == m) regreso i; // grupo completamente emparejado
. ♫ ... {
// volver al elemento después del inicio original
i = i - j + 1;
j = 0;
}
}
retorno -1; // grupo no encontrado
}

public boolean canChoose(int[][] grupos, int[] nums) {
int pos = 0;
para (int[] grupo : grupos) {}
pos = findGroup(grupo, nums, pos);
(pos == -1) volver falso;
}
retorno verdadero;
}

// --- principal para la comprobación rápida de la cordura ---
public static void main(String[] args) {
Solución s = nueva solución ();
int[][] groups1 = {1,-1,-1},{3,-2,0};
int[] nums1 = {1,-1,0,1,-1,-1,3,-2,0};
System.out.println(s.can Elija (grupos1, nums1)); // verdadero
}
}
`` `

### 3.2 Python – Ventana deslizante

``python
Solución de clase:
def canChoose(self, groups: List[List[int]], nums: List[int]) - título bool:
pos = 0 # siguiente índice gratis en nums
para grupo en grupos:
pos = self._find_group(group, nums, pos)
si pos == -1:
Retorno Falso
Retorno

def _find_group(self, group: List[int], nums: List[int], start: int) - título int:
n, m = len(nums), len(group)
i, j = start, 0
mientras que yo no
si nums[i] == group[j]:
i += 1
j += 1
si j == m:
Regreso
más:
i = i - j + 1 vuelta atrás
J = 0
retorno -1
`` `

### 3.3 C++ – Ventana deslizante

``cpp
Clase Solución {
public:
int findGroup(cont vector identificadoint círculo, const vector implicaint limitada nums, int start) {
int n = nums.size(), m = group.size();
int i = start, j = 0;
mientras (i
(nums[i] == group[j]) {}
++i; ++j;
si (j == m) regreso i; // partido completamente
. ♫ ... {
i = i - j + 1; // rollback
j = 0;
}
}
retorno -1; // no encontrado
}

bool canChoose(vector seleccionadovector identificadointю grupos, vector identificadoint compartir nums) {
int pos = 0;
para (auto &g : grupos) {}
pos = findGroup(g, nums, pos);
(pos == -1) volver falso;
}
retorno verdadero;
}
};
`` `

-...

## 4. Alternativa: KMP (O(n + m) por grupo)

■ **Cuando necesitas velocidad absoluta** (por ejemplo, `nums.length` hasta `105`), reemplaza el escaneo lineal interno con el algoritmo Knuth-Morris-Pratt:
■ 1. Construir el prefijo *Longest Proper que es también Suffix* (LPS) array para `grupo`.
■ 2. Scan `nums` from `pos` using the standard KMP search.
■ 3. Regresar el índice después del partido o `-1`.

KMP garantiza que cada elemento de `nums ' es examinado a la mayoría de dos veces por grupo, lo que hace que la complejidad total `O (las vidas eternas vivas * #grupos)` todavía, pero con una constante muy pequeña.
La solución de ventanilla deslizante es a menudo más simple de leer y ya suficientemente rápida para las limitaciones de este problema de LeetCode.

-...

## 5. Artículo del Blog – “Mastering LeetCode 1764: El Bien, el Mal y el Ugly”

■ **Keywords**: LeetCode 1764, matriz de forma mediante subarrays concatenantes, técnica de dos puntos, algoritmo KMP, prep de entrevista, entrevista de codificación, explicación de algoritmo, solución Python, solución Java, solución C+++, disjoint subarrays, complejidad del tiempo, complejidad del espacio

-...

### 5.1 Introduction

■ En el mundo de las entrevistas de codificación, los problemas que prueban su *manipulación de rayos* y * habilidades que coinciden con sub-array* son una visión común. Uno de esos desafíos es **LeetCode 1764 – “Form Array by Concatenating Subarrays of Another Array.”* *
■ Hoy diseccionaremos este problema, caminaremos a través de una elegante solución de ventanilla deslizante, tocaremos una variante KMP más óptima, y descubriremos los obstáculos ocultos que pueden tropezar hasta desarrolladores experimentados.

-...

### 5.2 Declaración de problemas (en inglés sencillo)

Se te da:

* `grupos` – una lista de *n* pequeños arrays.
* `nums` – un array más largo.

Usted debe decidir si usted puede **pick `n` segmentos no superpuestos de 'nums'** tales que:

1. El segmento *i‐th* es *exactamente* `grupos[i]`.
2. Los segmentos aparecen en el mismo orden que los grupos.

Si usted puede hacer eso, vuelva `verdad ' ; de lo contrario, `false`.

-...

### 5.3 Constraints " Why They Matter

TENIDO Parameter TENIDO Límites
Silencio...
TENIDA `groups.length` ANTERIOR 1 ... 1 000 ANTE
TENIDO `grupos[i].length` TENIDO 1 ... 1 000 TENIDO
TENIDO `sum(groups[i].length)` Ø 1 000 TENIDO
TENIDO `nums.length` TENIDO 1 ... 1 000 ANTE

Estos números nos dicen:

* Todo el problema es **pequeño suficiente** para que una solución \(O(n^2)\) pase cómodamente.
* Los arrays de entrada encajan en la memoria con ** espacio auxiliar constante**.
* Sin embargo, una entrevista puede pedirle a *escala* el algoritmo, por lo que es bueno saber la opción KMP más eficiente.

-...

### 5.4 La “buena” – Una solución de deslizamiento limpio–Window

La idea central: **se puede una vez, avariciosamente coincidir cada grupo, luego seguir adelante. #

#### 5.4.1 Step‐by‐Step

1. Mantenga un puntero 'pos` en 'nums' - el primer elemento no comprobado.
2. Por cada grupo:
* Intento coincidir con él empezando en 'pos'.
* Si un personaje coincide, mueva ambos punteros.
* Si un desajuste, *rollback* `pos` al elemento justo después del inicio original de este grupo y reiniciar.
* Si llegas al final del grupo, `pos` ahora apunta * después de* el segmento emparejado.
3. Si cualquier grupo no puede ser igualado, devuelve inmediatamente `false`.

Debido a que **nunca retrocedemos** a través de grupos ya emparejados, el algoritmo es lineal en 'nums' para cada grupo. Con casi 1 000 grupos, el trabajo total se mantiene pequeño.

#### 5.4.2 Code (Java)

*(ver la implementación de Java arriba)*

#### 5.4.3 Time & Space

* **Tiempo**: \(O(las personas que viven en la vida eterna)\) en el peor de los casos, pero encuadrado por `1 000 * 1 000` ♥ 1 millón de operaciones – bien bajo el límite de 1 segundo.
* **Espacio**: \(O(1)\) extra (sólo unos pocos índices).

-...

### 5.5 El "Bad" – Errores comunes

Por qué Fails
Silencio--------------------------
TENIDO Utilizando los bucles sintonizados* que se reinician desde el comienzo de los `nums` para cada grupo TENIDO O(n2) con grandes `nums`, pero lo más importante es ignorar el requisito *order*. Mantener un puntero en movimiento (`pos`) y nunca volver a empezar en `0`. Silencio
← Los grupos de Assuming son únicos o que todo el array puede ser particionado ANTE Grupos pueden superponerse en valores, y puede seleccionar un sub-array que contiene múltiples grupos (como en el ejemplo). ← Tratar a cada grupo de forma independiente; el algoritmo asegura automáticamente la descomunión. Silencio
Silencio No manejando el **edge** cuando un grupo está al final de `nums` Usted puede indexar fuera de límites. Mientras el bucle comprueba `i < n`; en el desajuste que voltea, nunca supera los límites de array. Silencio

-...

### 5.6 The “Ugly” – Edge Cases That Survive Even the Good Solution

Silencioso Escenario Silencioso Lo que sucede Silencioso Qué ver
Silencio--------------------------------------------------------------
Silencioso `grupos` contiene un *sub-array que es en sí mismo una concatenación de dos grupos más pequeños* El enfoque codicioso puede agarrar todo para el primer grupo, sin dejar nada para el segundo. Silencio Como el algoritmo coincide con los grupos **exactamente**, no los fusionará inadvertidamente. Silencio
Silencio `nums` se llena con un patrón de repetición (por ejemplo, todos los 1’s) Silencio El emparejamiento interno seguirá rodando de nuevo mucho, lo que podría conducir al peor caso \(O(n \times m)\). Aceptar que esto sigue siendo rápido para las restricciones, pero si te empujan a datos más grandes, cambia a KMP. Silencio
TENIDO Utilizando `String` concatenation o convirtiendo arrays a strings TEN Esto introduce una enorme sobrecarga y puede llevar a comparaciones erróneas debido al formato de números (cerrar ceros, signos negativos). ← Operar en los arrays enteros directamente. Silencio

-...

### 5.7 Cuando la velocidad es la pregunta – KMP

Si usted está entrevistando para un papel que exige una cadena de tiempo fijo ** (por ejemplo, *buscando un motivo de ADN en un genoma*), el algoritmo **Knuth–Morris–Pratt** es un conocimiento imprescindible.

* Construir un array LPS para cada grupo una vez – \(O(responderatura)\).
* Ejecute la búsqueda clásica de KMP sobre `nums` a partir de `pos`.
* Aún tocarás cada elemento de 'nums' un puñado de veces.

¿Por qué sigue siendo lineal? Debido a que la limitación *orden* le permite tratar a cada grupo como un patrón separado; la complejidad general sigue siendo \(O(las vidas eternanums sometidas \times #groups)\) pero con una constante mucho menor que el análisis ingenuo.

*(El código Pseudo para KMP se omite por brevedad pero está disponible fácilmente en las páginas de discusión de LeetCode.) *

-...

### 5.7 Bottom‐ Line Takeaway

* **Sliding‐window** es la solución *go‐to* para LeetCode 1764.
* **KMP** es la actualización * escalable* para entrevistadores que aman grandes tamaños de entrada.
* Evite reiniciar los escaneos desde el principio, seguir siempre la posición actual, y recuerde que *order* + *disjointness* son los dos pilares del problema.

-...

### 5.8 Problemas de práctica

1. **LeetCode 1448 – “Count Good Ways to Choose a Line of Students”** – similar array partición con restricciones.
2. **LeetCode 438 – “Encontrar todos los anagramas en una cuerda”** – un híbrido clásico KMP/Kadane.
3. **LeetCode 1048 – “Shortest Path with Alternating Colors”** – práctica manteniendo múltiples punteros a través de traversales de gráficos.

-...

Conclusión

■ Mastering LeetCode 1764 es más que resolver un solo problema; se trata de **bajo la forma en que los punteros de matriz se comportan**, reconociendo las trampas, y apreciando el poder de los algoritmos clásicos de mezcla de cuerdas.
■ Al combinar una solución de ventanilla deslizante limpia con el giro opcional KMP, usted estará listo para abordar el problema en cualquier configuración de entrevista – desde un conjunto de datos de 1 000-element a un conjunto de datos del mundo real masivo.

¡Feliz codificación, y sigue resolviendo!

-...

## 6. Notas de clausura

* No dude en adaptar el código de referencia a su idioma preferido.
* Para la preparación de entrevistas reales, practicar el rastreo a través del algoritmo en papel – esto ayuda a captar la lógica de rodaje-back.
* Mantenga la discusión de KMP útil – demuestra su conocimiento de *time-optimal patrón que coincide* y puede ganar puntos adicionales en una entrevista técnica.

-...

■ **End of Blog**.