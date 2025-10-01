-...
Título: LeetCode 1063. Número de subarrayos válidos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1063 – Número de Subarrayos Validos
**Hard** – LeetCode

■ # Objetivo #
■ Para un array `nums`, cuente cada sub-array contiguo cuyo elemento *leftmost* es **no mayor** que cualquier otro elemento en ese sub-array.
■ (En otras palabras, el elemento más izquierdo es el mínimo de ese sub-array.)

Las restricciones (`n ≤ 5·104`) fuerzan una solución O(n) – un caso clásico para una pila *monotónica*.

A continuación encontrará una implementación limpia y lista para la producción en **Java, Python y C+**.
Después del código, un completo SEO-optimised blog post explica el algoritmo, las trampas, y por qué impresionará a los reclutadores.

-...

## 📚 Code – Three Languages

■ Los tres snippets resuelven el mismo problema en **O(n)** tiempo y **O(n)** espacio auxiliar.
■ Todos ellos siguen la misma lógica: mantienen una pila creciente de índices; cuando aparece un número más pequeño, contribuciones pop y compute.

### 1. Java

``java
importar java.util*;

Solución de la clase pública {}
*
* Cuenta el número de subarrays válidos.
*
* @param nums el array de entrada
* Retorna la cuenta de subarrays válidos
*/
public int validSubarrays(int[] nums) {
int n = nums.length;
Deque se cumplióInteger confianza stack = nuevo ArrayDeque correspondió(); // almacena índices en orden creciente
long total = 0; // use long to avoid overflow

para (int i = 0; i)
// Mientras que el elemento actual es más pequeño, la parte superior de la pila
// no puede extender más allá de i-1.
mientras (!stack.isEmpty() " nums[i] {}
int idx = stack.pop();
total += i - idx; // subarrays donde nums[idx] se deja
}
stack.push(i);
}

// Los índices restantes pueden extenderse al final de la matriz
mientras (!stack.isEmpty()) {}
int idx = stack.pop();
total += n - idx;
}

(int) total; // resultado cabe en int (≤ n*(n+1)/2)
}
}
`` `

-...

### 2. Pitón

``python
de la importación Lista

Solución de clase:
def valid Subarrays(self, nums: List[int]) - int:
pila: List[int] = [] # índices de elementos en orden creciente
total: int = 0
n: int = len(nums)

para i, val en enumerate(nums):
# pop all indices whose values are larger than the current value
mientras apilan y nums[stack[-1]] val:
idx = stack.pop()
total += i - idx # número de subarrays con nums[idx]
stack.append(i)

# Los índices restantes alcanzan el final del array
mientras que la pila:
idx = stack.pop()
total += n - idx

total
`` `

-...

### 3. C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int validSubarrays(vector fielmente unidos nums) {
int n = nums.size();
vector Nombramiento de indices
largo largo total = 0; // utilizar largo tiempo para estar seguro

para (int i = 0; i) {}
mientras (!st.empty() ' nums[st.back()] {}
int idx = st.back(); st.pop_back();
total += i - idx; // contribución de nums[idx]
}
st.push_back(i);
}

// Los índices restantes pueden extenderse al final
(!st.empty())) {}
int idx = st.back(); st.pop_back();
total += n - idx;
}

retorno estático_cast seleccionado(total)
}
};
`` `

■ **¿Por qué 'largo'/`largo'?**
■ Para `n = 5·104`, el número máximo de subarrays es `n*(n+1)/2 ♥ 1.25·109`, que se ajusta a una entrada firmada de 32 bits. Sin embargo, las adiciones intermedias pueden superar ese límite en una aplicación ingenua. Usar un acumulador de 64 bits garantiza seguridad.

-...

## 📝 Blog Post – “El Bien, el Mal, y el Ugly de LeetCode 1063”

■ **Audiencia de emergencia** – estudiantes de CS, entrevistados de ingeniería de software y reclutadores
■ **Keywords** – *Número de Subarrayos Validos*, *LeetCode 1063*, *pilación monotónica*, *entrevista de ingeniería de software*, *entrevista de algoritmo*, * algoritmo de entrevista de trabajo*, *ingeniero de software*

-...

### Title
** “Número de Subarrayos Validos (LeetCode 1063): El Bien, el Mal, y el Ugly – Una Guía Monotonic‐Stack para los Coders de Job‐Ready”**

-...

##### 1. Introducción – Por qué este problema importa

- **LeetCode Hard** – aparece en muchas tuberías de contratación (Google, Amazon, Microsoft).
- ** analogía del mundo real** – encontrar “lazo más débil” en una cadena de restricciones (por ejemplo, la primera vez que un trabajo puede comenzar con los plazos).
- **Interview signal** – prueba tu comprensión de *subarray counting*, *stack tricks* y *amortized analysis*.

-...

##### 2. Recaptación de problemas

Dados `nums[0...n-1]`, cuenta el número de sub-arrayos no vacíos contiguos donde el elemento **izquierdísimo** es el más pequeño en ese sub-array.
For Formally: for a sub-array `nums[l...r]`, we require `nums[l] ≤ nums[i]` for all `I < i ≤ r`.

■ **Key Insight** – El elemento más izquierdo es el **minimo** del sub-array.

-...

##### 3. La Solución Buena - Elegante O(n)

#Monotonic Incremento de la situación* *
*Store indices of increasing values. *
Cuando aparece un elemento más pequeño, todos los índices de la pila son “congelados” – ya no pueden extenderse más allá de la posición actual.

*Contribución contable*
Para un índice " idx " apareció en la posición " i " , el número de subarrayos válidos en los que `nums[idx] " es el elemento más izquierdo igual a `i - idx`.
*¿Por qué?* All sub-arrays `[idx, k]` with `k` ranging from `idx` to `i-1` have `nums[idx]` como mínimo (porque todavía no se vio ningún elemento más pequeño).

- *El segundo paso*
Los índices restantes después de que el bucle principal puede extenderse al final de la matriz, aportando sub-arrayos 'n - idx` cada uno.

**Pseudo-code (estilo java)* *

``java
para (i = 0; i)
mientras (!stack.isEmpty() " nums[i] {}
idx = stack.pop();
total += i - idx;
}
stack.push(i);
}
mientras (!stack.isEmpty()) {}
idx = stack.pop();
total += n - idx;
}
`` `

** Complejidad** – Cada índice es empujado y saltado al máximo una vez → **O(n)** tiempo, **O(n)** espacio.

■ **Por qué es el “bueno”** –
■ *Simplicidad*: Un pase lineal, una pila, lógica matemática clara.
■ *Robustness*: Maneja valores iguales, aumentando estrictamente, disminuyendo estrictamente y datos aleatorios sin casos especiales.

-...

##### 4. El mal – Pitfalls comunes

Silencio Pitfall Silencio ¿Por qué rompe la vida Fijar
Silencio...
Silencio **Usando una pila de valores en lugar de índices** Silencio Perdiste la información de distancia (`i - idx`). ← Almacenar índices; buscar valores a través de 'nums[idx]`. Silencio
Silencio **Using a decreasing stack** Silencio Terminarás contando *rightmost* minima, no la izquierda. Utilizar una pila creciente (`nums[stack[top]]] [i]. Silencio
Silencio **Counting after each pop with `i - idx`** tención Fails when duplicate values appear; the condition `nums[i] debe ser *strictamente* más pequeño. Mantener `` fieltro' para duplicados o manejar duplicados en el segundo paso. Silencio
tención **No manipular la pila restante después del bucle** Н Misses sub-arrays que se extienden al extremo del array. tención bucle final: `total += n - idx`.
Silencio **Using int overflow** tención Para grandes arrays, sumas intermedias exceden de 32 bits. Silencio Use `long`/`long' para el acumulador. Silencio

■ **Por qué es “Bad”** – Estos errores son sutiles, pero hacen que una solución falla rápido en pruebas ocultas. También son fáciles de detectar si usted piensa cuidadosamente sobre los invariantes.

-...

##### 5. El Ugly – Overkill & Inefficient Solutions

1. **Brute Force** – Triple bucles anidados → **O(n3)**, imposible por `n = 50k`.
2. **Prefix‐Min + búsqueda binaria** – Todavía **O(n2)** en el peor de los casos.
3. ** Árbol de segmento / RMQ** – Sobre-ingenierado: la construcción de un árbol O(n) y la consulta O(log n) para cada sub-array → **O(n2 log n)**.
4. **Two‐Pointer Sliding Window** – Works for *sum* or *product* constraints but not for “minimum” based constraints; you'd need a deque to maintain mins → still **O(n2)** if not careful.

■ Las soluciones “muy” son a menudo las primeras que los candidatos piensan, pero son *no* competitivas. Un panel de entrevistas esperará una solución de pila O(n) limpia. Demostrar la conciencia de estos obstáculos muestra profundidad.

-...

##### 6. Real-World Takeaway

- **Estacas monotónicas** aparecen en muchos contextos: siguiente-granaje, minima de ventana deslizante, mantenimiento de casco convexo, etc.
- Maestro el patrón → lo reconocerás instantáneamente durante las entrevistas.
- Piensa siempre en términos de *“¿cuándo un elemento deja de ser relevante?”* – ese es el núcleo de los trucos amortizados de pila O(n).

-...

##### 7. Diálogo de entrevistas de muestra

■ **Entrevistador:** ¿Por qué O(n) es suficiente? ¿Podría explicar el análisis amortizado en inglés? ”
■ **Candidato:**
■ “Cada elemento puede ser empujado a la pila una vez. Después de que haya saltado, nunca se ha vuelto a ver. Así, el número total de operaciones de empuje/pop está obligado por `2n`, dando tiempo lineal. ”

■ Esta respuesta nítida muestra tanto la corrección como la comprensión del rendimiento.

-...

#### 7.1 Lista de verificación para su presentación

- [ ] Tienda **indices**, no valores.
- [ ] Use **strictamente** comparación más pequeña para saltar.
Conde 'i - idx' en pop.
- [ ] Proceso que queda pila después del bucle.
- Acumulado con `long`/`long'.
- [ ] Escriba código limpio y bien comunicado.

■ Presentar el snippet Java, pero traer la versión Python o C++ el día – muchos administradores de contratación ejecutan su solución en múltiples tiempos de ejecución.

-...

##### 7. Bono – Visualización de la dinámica de Stack

`` `
Índice: 0 1 2 3 4 5
Valor: 3 2 1 1 4 2

Evolución del estadio (top = izquierda):

i=0: stack=[0]
i=1: pop 0 (3 título2) → contrib 1, stack=[1]
i=2: pop 1 (2 prenda1) → contrib 1, stack=[2]
i=3: no pop (1==1), stack=[3,2]
i=4: no pop (4 título1), stack=[4,3,2]
i=5: pop 4 (4 título2) → contrib 1, pop 3 (1 título2? no), pop 2 (1 título2? no), stack=[5,2]
Final: pop 5→ 1, pop 2→ 4
Total = 1+1+1+4 = 8
`` `

■ Ver la pila ayuda visualmente a solidificar el razonamiento y es genial para una entrevista de pizarra blanca.

-...

##### 8. Closing – Impress

- **Hablar sobre amortizado O(n)** – los reclutadores aman “por qué esto es rápido”.
- **Mostrar el segundo paso** – muchos candidatos lo olvidan; demuestra atención al detalle.
**Explicar el manejo de la desbordación** – indica la mentalidad de código de nivel de producción.
*Mención del patrón* – “Este es un problema clásico de pila monotónica, que también se basa en el elemento siguiente, minima de ventana deslizante, etc. ”
Ellos verán instantáneamente que usted puede transferir este conocimiento a otros problemas.

-...

#### 🚀 Final Thought

LeetCode 1063 es más que un problema contable: es un portal para dominar técnicas monotónicas que dominan las entrevistas técnicas.
Con el código anterior y la profunda inmersión en este artículo, usted está totalmente equipado para convertir “lo malo y feo” en una solución limpia, **job-ready** que destacará a los reclutadores.

¡Feliz codificación y buena suerte en la próxima entrevista!

-...

*No dude en copiar, adaptar y compartir. *