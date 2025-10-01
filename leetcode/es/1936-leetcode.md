-...
Título: LeetCode 1936. Añadir Número mínimo de Rungs -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1936. Añadir Número mínimo de Rungs
## The Good, the Bad, and the Ugly – A Job‐Ready LeetCode Deep‐Dive

■ **Keywords:** Leetcode 1936, añadir el número mínimo de peldaños, problema de la escalera, algoritmo codicioso, codificación de entrevistas, solución Java, solución Python, solución C++, algoritmo O(n), consejos de entrevista de codificación, estructuras de datos, diseño de algoritmos, conseguir un trabajo

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

Usted está de pie en el suelo (`altura = 0`).
Una escalera tiene un conjunto de peldaños que crecen estrictamente.
Sólo se puede dar un paso a la siguiente pista si la distancia vertical entre su posición actual y ese rancio es **≤ dist**.

Puede agregar cualquier número de nuevos peldaños a cualquier altura de entero positivo.
**Objetivo:** Encuentre el número *mínimo* de peldaños que debe ser insertado para que pueda alcanzar el más alto peldaño.

TEN SON SON SON SON SON SON SON SON SON 
Silencio----------------------------------------------------
TENIDO 1 TENIDO `[1,3,5,10]`, `dist = 2` TENIDO `2` ANTE Add rungs at heights `7` and `8`. Silencio
TENIDO 2 TENIDO `[3,6,8,10]`, `dist = 3` TENIDO `0` Silencio Ya escalable. Silencio
TENIDO 3 TENIDO `[3,4,6,7]`, `dist = 2` TENIDO `1` Silencio Añadir a rung at height `1`. Silencio

-...

#### 2down⃣ Por qué es un problema **Greedy**

Nunca necesitas mirar *ahead* para decidir si añadir un rancio.
Si la brecha entre dos peldaños consecutivos es `gap`, lo único que importa es cuántos pasos adicionales de tamaño `≤ dist` necesitas atravesar esa brecha.

- **Observación**: La manera óptima de llenar una brecha es insertar los mínimos peldaños posibles.
Lo mejor que puedes hacer es colocar siempre una rana exactamente 'dist` unidades por encima de la anterior.

Por lo tanto el problema se reduce a: *Para cada brecha, cuente cuántos “pasos adicionales” de longitud `dist` son necesarios. *

-...

#### 3down⃣ La fórmula Simple O(n)

Para una brecha `gap = siguiente - actual`:

`` `
extra_need = (gap - 1) // dist
`` `

¿Por qué?
- Si `gap > = dist ' → `gap - 1  detectado dist` → rendimientos de la división entero `0`. No hay problema extra.
- Si `gap = dist + 1` → `(dist + 1 - 1) // dist = 1` → exactamente un rang necesita, etc.

Usted simplemente resume este valor sobre todas las brechas (incluyendo la brecha desde el suelo hasta el primer peldaño).

-...

### 4️ Implementación - Código en tres idiomas

### Java (LeetCode-style)

``java
// 1936. Add Minimum Number of Rungs
// Hora: O(n)
// Espacio: O(1)
Solución de la clase pública {}
public int addRungs(int[] rungs, int dist) {
int added = 0; // response accumulator
int prev = 0; // punto de partida es el suelo

para (un peluche : peldaños) {
int diff = rung - prev;
si
añadida += (diff - 1) / dist; // división entero
}
prev = rung;
}
retorno añadido;
}
}
`` `

#### Python 3

``python
# 1936. Añadir Número mínimo de Rungs
# Hora: O(n)
# Espacio: O(1)
de la importación Lista

Solución de clase:
def addRungs(self, rungs: List[int], dist: int) - título int:
añadido = 0
prev = 0
para el peldaño en peldaños:
diff = rung - prev
si diff > dist:
añadido += (diff - 1) // dist
prev = rung
retorno añadido
`` `

###### C++

``cpp
// 1936. Add Minimum Number of Rungs
// Hora: O(n)
// Espacio: O(1)
int addRungs(vector fielint círculo rungs, int dist) {
int added = 0;
int prev = 0;
para (un peluche : peldaños) {
int diff = rung - prev;
si
añadido += (diff - 1) / dist;
}
prev = rung;
}
retorno añadido;
}
`` `

-...

#### 5down⃣ Análisis de la complejidad

TEN ANTE TEN ANTE Java ANTERIOR Python
Silencio------------...
Silencio ** Tiempo** Silencioso `O(n)` Silencio `O(n)` Silencio `O(n)` Silencio
Silencio** Silencio

n` = número de peldaños existentes (≤ 105).
El algoritmo sólo escanea el array una vez y hace una cantidad constante de trabajo por elemento.

-...

### 6walks comunes (El "Bad")

Silencio Pitfall Silencio Por qué no funciona
Silencio--------------------------
Silencio **Añadiendo peldaños uno por uno** (simular cada paso) TENIENDO PÁRRAFO: `O(n · dist) `caso peor, imposible para `dista` hasta 109. Usa la fórmula de división anterior. Silencio
Silencio **Off‐by-one errors** TENIDO Utilizando `gap / dist` en lugar de `(gap - 1) / dist` da recuentos incorrectos cuando `gap` es un múltiplo de `dist`. Silencio
Silencio **Ignorando la brecha terrestre a primera** Silencio Failing para contar la distancia del primer rancio del suelo. Silencio Inicio `prev = 0`. Silencio
Silencio **Large integer overflow** Silencio En idiomas con tamaño entero fijo, `gap` podría ser de hasta 109. Silencio Usar tipos de 64 bits si es necesario (por ejemplo, 'long' en Java, `int64_t` en C++). Silencio

-...

### 7 carreras Alternativas " Variantes "

1. **Venta deslizante** – Sobrematar; el enfoque codicioso ya produce la optimización.
2. **Recursivo DP** – Cabeza innecesaria; la subestructura óptima es lineal, no combinatoria.
3. **Binary Search on Answer** – Se puede utilizar para los problemas de “medios mínimos” pero añade complejidad.
4. **Simulate Adding Rungs** – Works only for small constraints; will TLE on LeetCode.

**Bottom line:** La fórmula de división es *ambos* limpia y óptima.

-...

### 8️ Quick Test Harness (Python)

``python
si __name_ == "__main__":
sol = Solución()
print(sol.addRungs([1,3,5,10], 2)) # 2
print(sol.addRungs([3,6,8,10], 3)) # 0
print(sol.addRungs([3,4,6,7], 2)) # 1
`` `

-...

#### 9️ Take‐away for Interviews

- **Lea la declaración cuidadosamente.** El “gap” es entre posiciones *consecutivas*, no sólo el último rand.
- Una prueba genial. La colocación óptima de nuevos peldaños es siempre `dist` unidades separadas.
Si saltas un punto potencial, necesitarás al menos tantos peldaños más tarde.
- **La complejidad importa.** Los problemas de LeetCode con los insumos de `105` requieren soluciones lineales.
- Muestra las matemáticas. Derive `(gap - 1) // dist` explícitamente; entrevistadores les encanta ver el razonamiento.
- Código limpio. Agregar comentarios, use descriptive variable names (`prev`, `gap`, `added`).
- Los mejores casos de borde.
- Muy pequeño `dist` (1) → Usted puede necesitar muchos peldaños.
- Muy grande `dist` → respuesta es 0.
- Grandes brechas (hasta 109) → no garantizan el desbordamiento.

-...

#### 🔑 Final Thought

Este problema es un ejemplo de libro de texto de un algoritmo codicioso que es *forward*, *eficiente* y *idiomática* a través de idiomas. Dominarlo demuestra que usted puede:

- Traducir una limitación del mundo real en una expresión matemática limpia.
- Evite las trampas comunes que conducen a TLE o respuestas incorrectas.
- Escribir código listo para la producción que pasa todos los casos de borde.

Estas son exactamente las habilidades que los reclutadores buscan cuando le piden que resuelva “Añadir número mínimo de Rungs” en una entrevista de codificación. Buena suerte aterrizando ese próximo trabajo!