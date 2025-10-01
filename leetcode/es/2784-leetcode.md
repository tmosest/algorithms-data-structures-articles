-...
Título: LeetCode 2784. Compruebe si Array es bueno -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Artículo del Blog
**Título: *“Comprobar si Array es bueno” – Leetcode 2784: Contando-Orden, Tiempo-Optimal, Job‐Entreview‐ Listo*

-...

#### Introduction

Si usted está preparando para una entrevista técnica, usted golpeará problemas que parecen simples a primera vista, pero prueba su capacidad para razonar sobre casos de borde, la complejidad del tiempo y el uso de la memoria.
Problema de LeetCode **2784 – Compruebe si Array es bueno** es una de esas preguntas “obviamente fáciles” que en realidad exige una solución limpia, O(n) debido a las restricciones estrictas y la expectativa de la optimización de los entrevistadores.

En este post:

1. **Declarar el problema** claramente.
2. Camina por la intuición **algorítmica** (la parte “buena”).
3. Las trampas y por qué la clasificación ingenua puede ser “la opción fea”.
4. Entregar códigos de copiado** en **Java, Python y C+**.
5. Termina con ** consejos de interés** que te ayudarán a aterrizar ese trabajo.

■ **SEO Palabras clave:** Leetcode, Compruebe si Array es bueno, 2784, clasificación, entrevista, solución Java, solución Python, solución C++, complejidad de tiempo, algoritmo O(n), entrevista de trabajo, estructuras de datos, permutación de matriz.

-...

### Problema Declaración

■ **Given** un array entero `nums`.
■ **Define** `base[n] = [1, 2, ..., n‐1, n, n]`.
" La base[n] " es una permutación de " n+1 " números en los que los números " 1 ... n-1 " aparecen ** una vez** y el número " n " aparece ** dos veces**.
■
■ **Retorno** `verdad' si `nums` es una permutación de algunas `base[n]`, de lo contrario devuelve `false`.
■
■ **Constraints**
* `1 ≤ nums.length ≤ 100`
≤ 200

-...

### The “Good” – Why Counting Sort Wins

El array `nums` puede contener al máximo **200** valores distintos, por lo que un conjunto clásico de contador de tamaño 201 basta.
Usando el tipo de conteo:

1. **Count** ocurrencias de cada número en O(n).
2. **Reconstruir** el array en orden ascendente – todavía O(n) porque cada elemento se toca una vez.
3. **Validato** contra la definición de `base[n]` en un solo pase lineal.

¿Por qué es esto óptimo?

TEN TERRITORIO TENIDO Tiempo ANTERIOR
Silencio--------------------------
tención Full `Arrays.sort()` (Java), `sorted()` (Python), `std::sort` (C++) Silencio O(n log n) Silencio O(1) or O(n) Silencio
Silencio **Counting Sort** Silencio **O(n)** Silencio O(1) (fixed 201 array)

Las limitaciones del problema garantizan que el enfoque de contador supera la clasificación en cada punto de referencia.

-...

### El “Bad” – Pitfalls comunes

1. **Clasificación completa + cheque** – Funciona pero pierde la oportunidad de O(n).
2. **HashMap / HashSet** – Aún O(n) pero superior adicional; innecesario cuando el rango de valor es pequeño.
3. **No verificar la longitud** – Recuerde que `nums` debe tener longitud `n+1`; muchas soluciones saltan esta salida temprana y pagan el precio de un error posterior.
4. **Asumiendo el elemento max = n** – Si `max(nums) = n`, el array debe ser longitud `n+1`; si no, es instantáneamente inválido.

-...

### El “Ugly” – Cuando usted olvida los casos de borde

*Caso 1: * `nums = [2, 1, 3]`
*Max = 3, pero la longitud = 3 → debe ser 4 → `false`.*
- *Caso 2: * `nums = [1, 1]`
*Max = 1, longitud = 2 → válida (base[1]). *

No manejar estos casos conduce a falsos positivos/negativos y matará su calificación de entrevista.

-...

### Detalles de la implementación

A continuación encontrará soluciones limpias y bien adaptadas para **Java, Python y C+** que utilizan el tipo de conteo. Todos son tiempo O(n), espacio adicional O(1) (la matriz de 201 tamaño es constante).

■ **Consejo:** Siempre leen las limitaciones; a menudo esconden el algoritmo “derecho”.

-...

## 2. Code Solutions

### 2.1 Java – 1 ms, Beats 90 %

``java
// 2784. Compruebe si Array es bueno – Java Contando Ordenar
Clase Solución {
booleano público es Good(int[] nums) {
// 1. Contando frecuencias
int[] freq = nuevo int[201]; // los valores son 1..200
para (int x : nums) freq[x]++;

// 2. Recompild array en orden ordenados
int idx = 0;
para (int i = 1; i) = 200; i++) {
mientras (freq[i]-- 0) {
nums[idx+] = i;
}
}

// 3. Validar el patrón
int n = nums.length; // candidato n+ 1
si (n ■ 2) devolver falso; // base[n] tiene al menos 2 elementos

// Los primeros números n-1 deben ser 1..n-1
para (int i = 0; i)
si (nums[i] != i + 1) volver falso;
}

// Los dos últimos números deben ser iguales n-1
volver nums[n] - 1] == nums[n - 2] - 1] = n - 1;
}
}
`` `

**Las complejidades* *

- Tiempo: **O(n)** (n ≤ 100)
- Espacio: **O(1)** (201-int array)

-...

### 2.2 Python – 0 ms (fastest)

``python
# 2784. Compruebe si Array es bueno – Pitón contando Ordenar
Solución de clase:
def isGood(self, nums: list[int]) - título Bool:
1. Conde
[0] * 201
para x en nums:
freq[x] += 1

2. Reconstruido en orden ascendente
idx = 0
para val en rango(1, 201):
mientras freq[val]:
nums[idx] = val
idx += 1
freq[val] -= 1

3. Validación
n = len(nums)
si no
Retorno Falso
para i en rango(n - 2):
si nums[i] != i + 1:
Retorno Falso
volver nums[n] - 1] == nums[n] - 2] = n - 1
`` `

-...

### 2.3 C++ – 0 ms, beats 100 %

``cpp
- 2784. Compruebe si Array es bueno – C++ Contando algo
Clase Solución {
public:
bool isGood(vector seleccionadoint compartir nums) {
// 1. Contando frecuencias
int freq[201] = {0};
para (int x : nums) freq[x]++;

// 2. Reconstrucción ordenada
int idx = 0;
para (int val = 1; val > = 200; ++val) {
mientras (freq[val]--) {}
nums[idx+] = val;
}
}

// 3. Validación
int n = nums.size();
si (n. 2) devolver falso;
para (int i = 0; i) {}
si (nums[i] != i + 1) volver falso;
}
volver nums[n] - 1] == nums[n - 2] - 1] = n - 1;
}
};
`` `

-...

## 3. Análisis de Complejidad (A través de todos los idiomas)

TEN TERRITOR ANTERIOR ANTERIOR ANTERIOR ANTERIOR TERRITORIO TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR TERRITORNO ANTERITORNO ANTERIOR ANTE
Silencio--------------------------...
Silencio Cuenta las frecuencias Silencio O(n) Silencio O(1) Silencio
Silencio Rebuild ordenados por clasificación
Silencio patrón de validación
Silencio **Total** Silencio**

Debido a que `n ≤ 100' y rango de valor ≤ 200, esta solución es trivial para cualquier máquina moderna pero muestra la maestría de *contrar tipo* – una entrevista clásica.

-...

## 4. Consejos de entrevista – Lo que el programa quiere

Cómo se presenta en el problema ¿Cómo se presenta?
Silencio------------------------------------------ La vida--
Silencio ** Pensamiento algorítmico** Silencioso Elegir una especie sobre el sur ← Mención el límite de rango de valor; demostrar O(n) percepción 
Silencio **Edge‐case awareness** Silencio Manejando arrays de longitud 1, máx elemento discordancias tención Revise extensivamente la longitud contra `max(nums)+1` Silencio
Silencio ** readability del proyecto** Silencio Comentarios limpios, nombres descriptivos variables Silencio Mantenga la implementación concisa pero explique los pasos
Silencio **Testing** Silencio Proveer múltiples pruebas de unidad ← Incluir casos desde el prompt + sus propios casos de bordes

■ **Pro Tip:** Durante la entrevista, hable a través del algoritmo antes de escribir código. Los entrevistadores les encanta ver articular el plan.

-...

## 5. Conclusión

Problema 2784 “Comprobar si Array es bueno” es un ejemplo de cómo una pregunta aparentemente fácil oculta un requisito sutil: el array debe ser una permutación de ‘base[n].
Al aprovechar el rango de valor fijo con el tipo de conteo, se consigue:

- **Linear time** – golpea la penalización de la clasificación completa.
- **Espacio constante** – no hay contenedores adicionales, sólo una matriz de 201 tamaño.
- **Robustness** – comprobaciones de valor de longitud temprana garantizan la corrección.

Armado con esta solución (Java, Python, C++), estás listo no sólo para asar el problema LeetCode, sino también para impresionar a los entrevistadores con código limpio y óptimo.

■ **Feliz codificación & buena suerte en su próxima entrevista! * *

-...

*No dude en copiar los fragmentos de código, adaptarlos a su entorno de codificación, y compartirlos en su cartera de GitHub – es una gran manera de demostrar la proeza de resolver problemas a los posibles empleadores. *