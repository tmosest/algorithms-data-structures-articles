-...
Título: LeetCode 2970. Cuenta el número de Subarrayos Increíbles I -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recapitulación de problemas – LeetCode 2970
**Cuenten el número de Subarrayos Increíbles I**

Se le da una matriz 0-indexada de números enteros positivos `nums`.
A **subarray** `[i ... j]` (contiguo, no vacío) se llama *incremable* si la eliminación hace la matriz restante **principalmente aumentando**.
Devuelve el número total de subarrays increibles.

*Ejemplos*

TENIDO `nums` Respuesta involuntaria
Silencio------------
Silencio `[1,2,3,4]` Silencio 10 Silencio cada subarray es increible
Silencio `[6,5,7,8]` Silencio 7 Silencio sólo el trabajo de 7 subarrays en la lista
[8,7,6,6] Silencio

*Constraints*

`` `
1 ≤ nums.longth ≤ 50
1 ≤ nums[i] ≤ 50
`` `

Debido a que el array es diminuto (≤ 50), una solución simple O(n3) brute‐force funciona en unos pocos microsegundos y es aceptable para un entorno de entrevista.
A continuación encontrará tres implementaciones limpias – **Java**, **Python**, y **C+** – todos usando la misma lógica O(n3).
También mostraremos una breve optimización O(n2) que vale la pena tener en cuenta para mayores insumos.

-...

## 2. The Brute‐Force Idea (O(n3))

1. **Pick a subarray** `[i ... j]`.
2. **Skip all elements inside ** `[i ... j]` and traverse the remaining elements from left to right.
3. Compruebe que cada elemento visitado es **strictamente mayor** que el visitado anteriormente.
4. Si el cheque pasa, el subarray es inamovible → aumentar el contador.

El algoritmo sólo necesita unas variables enteros (`i`, `j`, `k`, `último `, `ok`) – espacio extra constante.

### Why It Works

La eliminación de un subarray equivale a concatenar el prefijo (`0 ... i‐1`) y sufijo (`j+1 ... n‐1`).
La matriz concatenada aumenta estrictamente si cada elemento del sufijo es mayor que el último elemento del prefijo, y todos los elementos dentro de cada segmento ya están aumentando.
El algoritmo imita esta prueba escaneando el array una vez por candidato subarray.

-...

## 3. Detalles de la aplicación

Silencio Idioma Silencio Código Silencio
Silencio...
Silencio **Java** Silencio Utiliza 'in` arrays, un 'long` counter para evitar el desbordamiento (no necesario para n=50, pero seguro). Silencio
La simplicidad de Python brilla para esta pequeña n. Silencio
Silencio **C+** Silencio Usos `vector realizadoint título`, `long long` mostrador, y `bool ok` bandera. Silencio

A continuación están los snippets exactos.

### 3.1 Java (Java 17)

``java
Solución de la clase pública {}
public long incremovableSubarrayCount(int[] nums) {
int n = nums.length;
ans largas = 0;

// Índice de inicio
para (int i = 0; i)
// Índice final
para (int j = i; j) {}
booleano ok = verdadero;
int last = Integer.MIN_VALUE; // centinela: no elemento anterior

// escanear toda la matriz
para (int k = 0; k)
si (k не= i ' qu ' significa= j) { /// inside subarray – skip
continuar;
}
si (último ю= nums[k]) { // no aumenta estrictamente
ok = falso;
ruptura; // no es necesario seguir comprobando
}
último = nums[k];
}
si (ok) ans+;
}
}
devolver los ans;
}
}
`` `

### 3.2 Python (Python 3.11)

``python
Solución de clase:
def incremable SubarrayCount(self, nums: list[int] - int:
n = len(nums)
ans = 0
para i en rango(n): # Start
para j en rango(i, n): # extremo
OK = True
último = flotante('-inf')
para k en rango(n):
si lo hice, lo hice.
continuar
si el rito= nums[k]:
ok = Falso
descanso
último = nums[k]
Si está bien:
ans += 1
Retorno
`` `

### 3.3 C++ (C+17)

``cpp
Clase Solución {
public:
long long incremovableSubarrayCount(vector seleccionadoint limitada nums) {
int n = nums.size();
ans largos = 0;

para (int i = 0; i)
para (int j = i; j)
bool ok = verdadero;
int last = INT_MIN; // sentinel

para (int k = 0; k)
si (k не= i ' qu ' = j) continúan; // skip subarray
si (último ю= nums[k]) { // no aumenta estrictamente
ok = falso;
ruptura;
}
último = nums[k];
}
si (ok) ++ans;
}
}
devolver los ans;
}
};
`` `

-...

## 4. Más optimizado (O(n2)) Ver

Aunque la fuerza bruta pasa cómodamente, se puede reducir el bucle interior por pre-computación:

- `izquierda[i]` - es el prefijo 'nums[0...i]` ¿Se está incrementando estrictamente?
- `rightInc[i]` - ¿Está aumentando estrictamente el sufijo 'nums[i...n-1]?

Entonces por cada `[i...j]` sólo tienes que comprobar:

1. `leftInc[i-1]` (si `i título0`) - asegura el prefijo antes de `i` está bien.
2. `rightInc[j+1]` (si `j+1 obtenidos ' ) – asegura sufijo después de que `j` esté bien.
3. `nums[i-1]  realizadas nums[j+1]` (si existen ambas partes) – garantiza que el punto de unión está aumentando.

Con estos arrays la decisión de un subarray se convierte en **O(1)**, convirtiendo todo el algoritmo en **O(n2)**.
Para las limitaciones dadas es sobre-ingeniería, pero es un truco excelente recordar para las preguntas de entrevista donde 'n' podría estar hasta '105'.

-...

## 5. Casos de borde " Pruebas "

Silencio Test ← Input Silencio esperada
Silencio----------------------------
Silencio 1 Silencio `[1] Silencio `1` Únicamente subarray `[1] es válido. Silencio
TENIDO 2 TENIDO `[2,1]` TENIDO `2` Silencio `[2] ' y `` ambos dejan un único conjunto de elementos, que está aumentando estrictamente. Silencio
TENIDO 3 TENIDO `[1,1]` TENIDO `1` Únicamente `[1,1]` deja una matriz vacía. Silencio
TENIDO 4 TENIDO `[3,2,1]` TENIDO `3` TENIDO `[3]`, ``[2]`, `` Cada uno produce `[2,1]`, ``, `[3,2]` - todo estrictamente disminuyendo, por lo que sólo funciona el subarray completo `[3,2,1]`. Silencio
TENIDO 5 TENIDO `[1,2,3,4]` TENIDO `10` TENIDO Todos los subarrays funcionan. Silencio

Ejecute estas pruebas en cualquier idioma; las tres soluciones deben coincidir.

-...

## 6. El Bien, el Mal, el Ugly

Silencio Silencio
Silencio------------Prince------
TEN **Simplicidad** Silencio fácil de leer, no hay estructuras auxiliares de datos. La fuerza bruta puede parecer lenta a primera vista. Los bucles triples anidados pueden intimidar a los recién llegados. Silencio
Silencio **Performance** Silencio Corres ■ 1 ms para n ≤ 50. Silencio Todavía O(n3), no puede escalar más allá de los elementos ~2000. El cheque interno "si (k не= i ' qu ' t = j)` se repite muchas veces. Silencio
Silencio **Extensibilidad** Silencio Directo para adaptarse a otros problemas de “removal”. Silencio difícil de reutilizar para mayores limitaciones. La lógica no es reutilizable para secuencias que no aumentan estrictamente. Silencio
Silencio **Entrevista de apelación** Silencio muestra comprensión del razonamiento “prefijo + sufijo”. Podría levantar una bandera roja sobre la complejidad del tiempo. Silencio Muestra la capacidad de escribir bucles limpios, pero la falta de discusión de optimización puede doler. Silencio

■ **Takeaway** – Para las restricciones de estilo de entrevista, *la legibilidad* a menudo supera la *optimidad*.
■ Si el entrevistador pide explícitamente una solución más rápida, el método O(n2) arriba es un paso siguiente rápido.

-...

## 7. Resumen – Por qué vas a tener puntos de puntuación

- El problema es un clásico truco de “remove un segmento → check monotonicity”.
- Un enfoque de fuerza bruta es perfecto para los límites dados.
- Los snippets Java/Python/C+ comparten el mismo esqueleto lógico, demostrando que la solución es *language‐agnostic*.
- Siempre puedes mencionar la optimización O(n2) para demostrar conciencia de patrones más eficientes.
- El código está listo para pegar en una plataforma de coding-interview, y usted puede explicar con confianza cada bucle al entrevistador.

Buena suerte aterrizando esa llamada de coding-interview! 🚀