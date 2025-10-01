-...
Título: LeetCode 1887. Operaciones de reducción para hacer iguales los elementos del rayo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
LeetCode 1887 – “Operaciones de reducción para hacer iguales los elementos del rayo”

Silencio Idioma Silencio Tiempo Complejidad Silencio
Silencio...
Silencio **Java** Silencio**
Silencio **Python** Silencio **O(n log n)** Silencio**
Silencio **C+** Silencio **O(n log n)** Silencio**

-...

### 🚀 TL;DR (Solution in One Line)

``java
Arrays.sort(nums);
int ans = 0, prev = nums[0];
para (int i = 1; i)
si (nums[i] != prev) { ans += i; prev = nums[i]; }
}
devolver los ans;
`` `

-...

## 1. Recaptación de problemas

Se le da un array entero `nums`.
Una **operación** es:

1. Encuentra el valor * más grande* (si varios, elige el más izquierdo).
2. Reduzca ese elemento al siguiente valor *smaller* más grande.
3. Repita hasta que cada elemento sea igual.

Devuelve el número total de operaciones necesarias.

-...

## 2. Intuición " Observación clave

Piense en el array ordenados ** cada vez más**:

`` `
[1, 3, 5] → ordenados: [1, 3, 5]
`` `

* Cada vez que el valor cambia, todos los elementos *a la izquierda* son estrictamente menores.
El elemento que causó el cambio se reducirá *exactamente una vez* para llegar a ser igual al valor izquierdo.

Así que para cada índice `i` donde `nums[i]!= nums[i‐1]`, agregamos `i` operaciones.
Añadiendo todos esos recuentos de “golpe” da la respuesta.

-...

## 3. Edge‐Case Pitfalls

Silencio Caso confidencialidad ¿Qué puede pasar mal? Cómo evitarlo
Silencio...
Silencio Todos los elementos iguales ¦ Podría contar incorrectamente las transiciones ¦ Skip the first element; only add when `nums[i] != nums[i‐1]` Silencio
tención Array del tamaño 1 Silencio No se necesita ninguna operación
← Valores duplicados dispersos ← Ordenar mangos orden; duplicados se vuelven contiguos tención Uso clasificación primera ¦

-...

## 4. Análisis de la complejidad

TEN TERRITORIO TERRITORIO ANTERIOR
Silencio...
Silencio Ordenar la matriz Silencio **O(n log n)**
TENIDO ÚNICO PÁRRAFO 3 Silencio
Silencio espacio extra Silencioso copia de Array (como en el lugar) → **O(1)** (Java’s `Arrays.sort` is in-place)

En general: **Hora** `O(n log n)` **Pace** `O(1)` (o `O(n)` si usted copia).

-...

## 5. Aplicación en tres idiomas

### 5.1 Java

``java
importa java.util. Arrays;

Solución de la clase pública {}
reducción de la entrada públicaOperaciones(int[] nums) {
Arrays.sort(nums); // O(n log n)
int ops = 0;
int prev = nums[0];
para (int i = 1; i)
si (nums[i] != prev) {
ops += i; // todos los elementos antes de ser más pequeños
prev = nums[i];
}
}
operaciones de retorno;
}
}
`` `

### 5.2 Python

``python
Solución de clase:
def reductionOperations(self, nums: list[int] int:
nums.sort() # O(n log n)
operaciones = 0
prev = nums[0]
para i en rango(1, len(nums)):
si nums[i] != Prev:
ops += # Todos los elementos antes de que sea más pequeño
prev = nums[i]
operaciones de retorno
`` `

### 5.3 C++

``cpp
#include >
Incluido el título

Clase Solución {
public:
int reductionOperaciones(std::vector realizadasint limitada nums) {
std::sort(nums.begin(), nums.end()); // O(n log n)
int ops = 0;
int prev = nums[0];
para (size_t i = 1; i) ++i) {
si (nums[i] != prev) {
op += static_cast
prev = nums[i];
}
}
operaciones de retorno;
}
};
`` `

-...

## 6. Vista alternativa: uso de mapa de frecuencias

Si prefiere no ordenar todo el array, puede:

1. Construir un mapa de frecuencia (`TreeMap` en Java, `SortedDict` en Python, o `std::map` en C++).
2. Traverse las teclas en orden **descendiente**, manteniendo una suma sufijo de cuentas, añadiéndola a la respuesta por cada clave excepto la más pequeña.

Esto produce el mismo tiempo `O(n log n)`, pero puede ser más claro cuando ya estás trabajando con un multiset.

-...

## 7. Por qué esto es un gran problema de entrevista

1. **Mostrar comprensión de la clasificación " Prefijo " Sums** – Muchos entrevistadores buscan la capacidad del candidato para transformar un problema en una vista de prefijo ordenada.
2. **Edge‐Case Sensitivity** – Manejar arrays con todos los elementos iguales o singletons prueba la atención al detalle.
3. **Multiple Solutions** – Usted puede discutir tanto el enfoque de “granaje surtido” y el enfoque “ mapa de frecuencia sufijo”, destacando los trade-offs.

-...

## 8. SEO‐Friendly Summary

- **Keywords**: *Leetcode 1887*, *Operaciones de reducción*, *Equipos de matriz iguales*, *Solución de Java*, * Solución de Pitón*, *Solución de C+*, *entrevista de algoritmo*, *entrevista de codificación prep*, *O(n log n)*, * array surtido*.
- *Descripción* “Aprenda a resolver LeetCode 1887 – Operaciones de reducción para hacer iguales los elementos de la raya. Ver las implementaciones Java, Python y C+++ más un blog profundo explicando el algoritmo, casos de borde y consejos de entrevista. ”

-...

#### 🎯 Final Thought

La clave para *LeetCode 1887* es reconocer que cada “jump” en la matriz ordenada nos dice exactamente cuántas reducciones se requieren. Un simple paso sencillo después de ordenar da una solución elegante y óptima que impresionará a los entrevistadores y le acercará un paso más a su trabajo de ensueño. ¡Feliz codificación!