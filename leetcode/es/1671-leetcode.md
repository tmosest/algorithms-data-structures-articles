-...
Título: LeetCode 1671. Número mínimo de absorciones para hacer la raya de montaña -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🔍 1671 – Mínimo número de extracciones para hacer el rayo de montaña
### La solución completa “buena, mala y fea”
*(Java fort Python Silencio C++)*

■ **TL;DR** –
■ 1. Encuentra la Subsecuencia de Incremento más largo (LIS) terminando en cada índice.
■ 2. Encuentre la subsecuencia de disminución más larga (LDS) comenzando en cada índice.
■ 3. Por cada índice que puede ser un pico ( " LIS[i] √≥ 1 " √≥ LDS[i] √° 1 " )
"mountainLen = LIS[i] + LDS[i] - 1`.
■ 4. `respuesta = n - max(mountainLen)` - las absorciones mínimas.
■
■ Complejidad: **O(n2)** tiempo, **O(n)** espacio (n ≤ 1000).

-...

## 🏔 Por qué este problema importa para las entrevistas

- **Mountain Array** – un patrón clásico de entrevista: “recientemente aumentando y disminuyendo estrictamente”.
- Requiere *programación dinamica* (LIS/LDS) y una comprensión clara de los problemas de subsecuencia.
- Prueba su capacidad para manejar los casos de borde (`n = 3`, todos los números iguales, etc.).
- Perfecto para mostrar su estilo de codificación y enfoque de solución de problemas en una entrevista de trabajo.

-...

## 📚 Walk‐Through detallado

### #1# Define a Mountain Array

Un array de montaña `arr` satisfies:

1. `arr.length >= 3
2. ∃ index ' i ' ( " 0 " )
`arr[0] ' ecto ... **y** `arr[i] } `

El pico es único porque ambos lados son estrictamente monotónicos.

#### 2down⃣ Observación

Si sabemos por cada índice:
- ¿Cuánto tiempo termina una subsecuencia estrictamente creciente en ese índice (`LIS[i]`).
- ¿Cuánto tiempo comienza una subsequencia estrictamente decreciente en ese índice (`LDS[i]`).

Entonces, un índice puede ser un pico **iff** `LIS[i] > 1 " LDS[i] > 1 `.
La longitud total de la montaña que utiliza `i` como el pico es `LIS[i] + LDS[i] - 1` (el pico se cuenta dos veces).

DP for LIS and LDS

Porque `n' 0 = 1000`, un `O(n2)` El DP está perfectamente bien.

- **LIS**
`` `
LIS[i] = 1
para j
si nums[i] не nums[j]: LIS[i] = max(LIS[i], LIS[j] + 1)
`` `

- **LDS** - iterate backs
`` `
LDS[i] = 1
para j i)
si nums[i] не nums[j]: LDS[i] = max(LDS[i], LDS[j] + 1)
`` `

#### 4down⃣ Encuentra la montaña más larga

`` `
MaxLen = 0
para mí en 1 ... n-2:
si LIS[i] ≤ 1 y LDS[i]
maxLen = max(maxLen, LIS[i] + LDS[i] - 1)
`` `

#### 5down⃣ Respuesta final

`` `
retorno n - maxLen
`` `

-...

## 📦 Code Snippets

## Java (LeetCode-friendly)

``java
Clase Solución {
public int minimumMountainRemovals(int[] nums) {
int n = nums.length;
int[] lis = nuevo int[n];
int[] lds = nuevo int[n];

// LIS (para adelante)
para (int i = 0; i)
lis[i] = 1;
para (int j = 0; j) {}
si {}
lis[i] = Math.max(lis[i], lis[j] + 1);
}
}
}

// LDS (backward)
para (int i = n - 1; i 0; i--) {
i) = 1;
para (int j = n - 1; j i; j) {}
si {}
lds[i] = Math.max(lds[i], lds[j] + 1);
}
}
}

int best = 0;
para (int i = 1; i)
si (lis[i] 1) {
mejor = Math.max(best, lis[i] + lds[i] - 1);
}
}
retorno n - mejor;
}
}
`` `

## Python 3

``python
Solución de clase:
def minimumMountainRemovals(self, nums: List[int]) - título int:
n = len(nums)
lis = [1] * n
lds = [1] * n

# LIS
para i en rango(n):
para j en rango(i):
si nums[i] √≥ nums[j]:
lis[i] = max(lis[i], lis[j] + 1)

# LDS
para i en rango(n - 1, -1, -1):
para j en rango(n - 1, i, -1):
si nums[i] √≥ nums[j]:
lds[i] = max(lds[i], lds[j] + 1)

mejor = 0
para i en rango(1, n - 1):
si lis[i] ≤ 1 y lds[i] 1:
mejor = max(best, lis[i] + lds[i] - 1)

retorno n - mejor
`` `

## C++ (GNU‐C+17)

``cpp
Clase Solución {
public:
mínimo intMountainRemovals(vector efectuadoint ánimo nums) {
int n = nums.size();
vector:

// LIS
para (int i = 0; i) {}
para (int j = 0; j)
si
lis[i] = max(lis[i], lis[j] + 1);
}

/ LDS
para (int i = n - 1; i 0; --i) {
para (int j = n - 1; j i; --j)
si
lds[i] = max(lds[i], lds[j] + 1);
}

int best = 0;
para (int i = 1; i) {}
si (lis[i] 1)
mejor = max(best, lis[i] + lds[i] - 1);
}

retorno n - mejor;
}
};
`` `

-...

"Bueno" - Lo que funciona bien

TENIDO VALORAR LA FACILIDAD ANTERIOR Por qué Es bueno
Silencio----------------------------
confidencialidad **Simple O(n2) DP** Ø Fácil de entender, no se necesitan estructuras de datos avanzadas. Silencio
Silencioso **Separación de vuelo** Silencioso LIS y LDS computed independently, making debugging trivial. Silencio
Silencio **Deterministic Peak Check** Silencio `LIS[i] ≤ 1 " LDS[i] 1` garantiza una montaña válida. Silencio
tención **Scalable** Silencioso `n = 1000` → en la mayoría de 1.000.000 operaciones → bien debajo de 1 ms. Silencio
tención **Portable** Silencio Obras en Java, Python y C++ con cambios mínimos. Silencio

-...

"Bad" – Potential Pain Points

Н нели вали Edición ный Mitigation
Silencio...
Silencio **O(n2) puede sentirse pesado** Silencio Para `n = 105` fracasaría, pero las limitaciones son `≤ 1000`. Silencio
¿Todos los números iguales? `LIS` y `LDS` se quedarán 1 → sin pico; el problema garantiza la soledad, pero todavía bueno para manejar explícitamente. Silencio
Silencio ** Memoria** Silencioso `O(n)` arrays son minúsculas, pero si necesita `O(n log n)` para mayores restricciones, utilice la búsqueda binaria LIS. Silencio

-...

## 🧙 ️ "Ugly" – Gotchas & Advanced Molinos

1. **Prontamente Aumentar / Disminuir** – Asegúrese de que se utilice la comparación *strict* (` ``).
2. **Peak debe tener ambos lados** – Nunca considerar `i = 0` o `i = n-1` como un pico.
3. **Off‐by‐One en Longitud Cálculo** – Recuerde restar 1 al resumir LIS + LDS porque el pico se cuenta dos veces.
4. ** Enfoque alternativo** – Una solución más rápida `O(n log n)` se puede construir con LIS+reverse‐LIS + búsqueda binaria, pero para la claridad de la entrevista se prefiere el DP cuadrático.
5. **Testing** – Incluir casos como `[1, 2, 3]` (sin disminuir el lado) y `[3, 2, 1]` (sin aumentar el lado) para confirmar el algoritmo sólo recoge los picos válidos.

-...

## 📈 SEO‐Optimized Blog Draft

■ *Título*
■ *Master LeetCode 1671 – Número mínimo de extracciones para hacer Array de Montaña (Java/Python/C++)”*
■
■ **Meta Descripción:**
■ Aprende a resolver LeetCode 1671 en Java, Python y C++ usando programación dinámica. Entender LIS & LDS, selección de picos y análisis de complejidad para su próxima entrevista de codificación.

### Intro Paragraph
■ Si usted está preparando una entrevista técnica, a menudo golpeará problemas de subsecuencia. Uno de los más complicados pero más esclarecedores es LeetCode 1671: *Minimum Number of Removals to Make Mountain Array*. Este post te lleva a través de la solución completa, rompiéndola en las partes “buenas, malas y feas”. Coge los fragmentos de código para Java, Python y C++, así que puedes practicar en LeetCode o prepararte para tu próxima entrevista de trabajo.

### Body Sections
1. **Por qué los rayos de montaña son entrevistas oro**
2. ** Definición de problemas " Limitaciones " *
3. **Dynamic Programming Insight – LIS LDS**
4. **Step‐by‐Step Implementation** (Java, Pitón, C++)
5. ** Análisis de complejidades y casos de borde**
6. **“Bueno / malo / ugly” Resumen**
7. ** Variantes avanzadas y lectura ulterior**
8. **Practice Tips & Sample Test Cases**

■ **Keywords:**
√ LeetCode 1671, Eliminaciones de Montaña Mínima, LIS, LDS, Programación Dinámica, Solución Java, solución Python, solución C++, patrones de codificación de entrevistas, consejos de entrevista de codificación, desafío de codificación.

## Call‐to‐Action

■ *“¿Quieres más soluciones LeetCode? ¡Suscríbete a nuestro boletín y consigue retos semanales de codificación entregados directamente a tu buzón de entrada!”*

-...

## 🚀 Cómo usar este artículo en tu búsqueda de empleo

1. **Mostrar el Código** – Pegar el fragmento específico del idioma en su perfil de GitHub o un blog personal.
2. **Explicar el enfoque** – En una entrevista, comience con la definición de montaña → LIS/LDS → pico check.
3. **Discuten las partes “Bad”* “Ugly”** – Limitaciones de mención, por qué las comparaciones estrictas importan, y cómo manejar casos de borde.
4. **Mención de la alternativa** – Nota breve la opción 'O(n log n)`; se puede decir que eligió el DP cuadrático para la claridad.
5. **Envolver** – Resumir la respuesta y la complejidad para reforzar su comprensión.

-...

##  inaceptable Final Takeaway

LeetCode 1671 es un showcase *disnamic-programming* disfrazado como un rompecabezas subsequence. Mediante la computación de LIS y LDS y la validación de picos, puede terminar con el número mínimo de eliminaciones de una manera limpia, de entrevista. Utilice el código anterior, probarlo a fondo, e impresionará a los reclutadores con su profundidad técnica y claridad de pensamiento.

¡Feliz codificación! 🚀

-...

**Nota:** Todos los fragmentos de código compilan en el entorno estándar de LeetCode. Siéntete libre de copiar y probar. ¡Feliz entrevista!