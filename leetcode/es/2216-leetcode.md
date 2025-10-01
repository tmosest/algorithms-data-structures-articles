-...
Título: LeetCode 2216. Eliminaciones mínimas para hacer el Array hermosa -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🧩 2216 – Deleciones Mínimas para Hacer Hermoso Array
**Solución en Java, Python & C+**

-...

### 1. Recaptación de problemas

■ # Hermoso array #
* `nums.length` Incluso
* Por cada índice, `i`, `nums[i]!= nums[i+1] `

Podemos eliminar cualquier número de elementos (los elementos restantes mantienen su orden relativo).
Regrese las eliminaciones necesarias.

`` `
Entrada: nums = [1,1,2,3,5]
Producto: 1 // eliminar uno de los dos 1s
`` `

-...

### 2. Observación clave

Cuando construimos la matriz “hermosa” de izquierda a derecha sólo necesitamos saber:

* **El último elemento de un índice es** (pre`).
- Si el siguiente número es igual a `pre`, debemos eliminarlo (otros `nums[i] == nums[i+1]`).
- Si difiere, podemos mantenerlo y *reiniciar* el marcador “incluso índice” (la siguiente ranura es extraña).

El algoritmo nunca necesita mirar más adelante – una decisión codictiva es óptima.

-...

### 3. Greedy, O(1) Space Algorithm

TEN TERRITORIO ANTERIOR ANTERIOR ANTERIOR
Silencio------------------------------
TENIENDO TENIDO `res = 0` (conteo de eliminación), `pre = -1` (sin elemento de índice aún) TENIDO ANTE
← Iterate sobre cada elemento `a` Silencio *Si `a == pre` → borrarlo (`res++`).* Selección* → set `pre = (pre 0 ? a : -1)` Silencio Cuando mantenemos un número en una posición que “reconectamos” `pre` a `-1` para que el siguiente elemento pueda ser colocado en la posición impar. Silencio
Silencio Después del bucle Silencio Si `pre >= 0` (la longitud de la matriz es extraña) → `res+` (deletrear el último elemento) Silencio Una hermosa matriz debe ser uniformemente grande. Silencio

-...

### 4. Prueba de corrección (Sketch)

*Probamos por inducción que el algoritmo produce una hermosa matriz válida con el número mínimo de eliminaciones. *

1. **Base**: Antes de procesar cualquier elemento, la matriz vacía es hermosa.
2. ** Paso de inducción**:
*Asumir el prefijo procesado (después de `k` iterations) es el **shortest** hermosa subsequencia de los primeros 'k' números. *
* For the `k+1`‐th number `a`:
*Si `a == pre`*: mantener `a` violaría la regla de la adyacencia en un índice uniforme → cualquier subsequencia hermosa debe eliminar `a`. El algoritmo lo elimina, manteniendo la propiedad mínima.
* If `a != pre`*:
- Si `pre` es negativo, `a` puede ocupar con seguridad la ranura actual incluso → el algoritmo lo mantiene.
- Si `pre` no es negativo, eso significa que el elemento anterior fue colocado en una ranura extraña, por lo que `a` puede ocupar con seguridad la siguiente ranura incluso, reasentando `pre`.
En ambos casos el algoritmo mantiene `a` cuando no duele la viabilidad, preservando las eliminaciones mínimas.

3. **Procesamiento de postes**: Si `pre √= 0` después del lazo, la longitud actual es extraña. Cualquier hermoso array debe ser incluso tamaño, por lo que el último elemento debe ser eliminado. El algoritmo lo elimina, aún es mínimo.

Así el algoritmo produce la solución óptima.

-...

### 5. Análisis de la complejidad

TEN ANTE TEN ANTE Java ANTERIOR Python
Silencio------------...
TENIDO EL TIEMPO ANTERIENTE **O(n)** TENIENTES **O(n)**
Silenciosos en el espacio **O(1)**

`n` ≤ 105, por lo que el escaneo lineal es lo suficientemente rápido.

-...

### 6. Aplicación de las referencias

■ **Nota**: Las tres versiones siguen la misma lógica codictiva y pueden copiarse en LeetCode.

#### 6.1 Java (LeetCode signature)

``java
Clase Solución {
public int minDeletion(int[] nums) {
int deletions = 0; // response so far
int pre = -1; // último elemento en un índice uniforme (-1 significa ninguno)

para (int a : nums) {
si (a == pre) { // rompería la regla de belleza
supresiones++;
. ♫ ... {
// mantener un
pre = (pre 0) ? a : -1; // si acabamos de colocar un elemento uniforme, resetea
}
}

// Si terminamos con un extraño array de longitud, eliminar el último elemento
si 0) {
supresiones++;
}
supresiones de retorno;
}
}
`` `

#### 6.2 Python 3

``python
Solución de clase:
def minDeletion(self, nums: List[int] int:
supresiones = 0
pre = -1 # último elemento de índice

para una en las numidades:
si a == pre:
supresiones += 1
más:
pre = a if pre -1 Guardar o restablecer

si pre- 0: # longitud extraña al final
supresiones += 1
devoluciones
`` `

#### 6.3 C+17

``cpp
Clase Solución {
public:
int minDeletion(vector fielint círculo nums) {
supresiones int = 0;
int pre = -1; // último elemento de índice

para (int a : nums) {
si (a == pre) {}
++deleciones; // debe eliminar
. ♫ ... {
pre = (pre 0) ? a : -1; // mantener o restablecer
}
}

si 0) { // longitud impar
++deleciones;
}
supresiones de retorno;
}
};
`` `

-...

### 7. “Bueno, malo y feo” – ¿Qué hay que ver para

Silencio Silencio
Silencio------------Prince------
Silencio **Logic** Silencio Puro avaricioso, sin DP o pila requerida TENIDO MIS-pensando la bandera de “reset” → infinito bucle TENIDO Olvídate de manejar el extraño caso final de longitud (common bug)
Silencio **Edge Cases** ← Empty array → 0 deletions  sometida Single element → 1 deletion (debe eliminar) Silencio Muy largo de igual número → todo pero uno debe ser borrado
Silencio **Testing** Silencio ``, ``, `[1,1]`, `[1,2]`, `[1,1,1,1]` Silencio Motivos mixtos iguales / desiguales Silencio Aleatoria gran entrada para confirmar `O(n)` velocidad

-...

### 8. Consejos para entrevistas

1. ** Explique el invariante**: "pre` tiene el valor que, si se repite, rompería la regla de belleza. ”
2. **Mostrar la prueba**: Utilice la inducción o un pequeño argumento contra-ejemplo.
3. **Hablar sobre el espacio**: O(1) es un punto de venta fuerte.
4. ** Manejo del borde de la fusión**: La eliminación definitiva de la longitud es la sutileza que a menudo viaja a los candidatos.
5. **Mostrar la muestra funciona**: Camina por `[1,1,2,2,3,3]` y destaca donde se produce cada eliminación.

-...

### 9. Final Take-away

La solución avaricia, O(1) para **LeetCode 2216** es limpia, rápida y perfecta para una entrevista de codificación.
Su elegancia reside en reconocer que *sólo el último elemento incluso indexado importa* y que la paridad del array decide si se necesita una eliminación adicional al final.

¡Feliz codificación! 🚀

-...

**Keywords**: LeetCode 2216, Eliminaciones Mínimas para Hacer Hermoso Array, O(1) Greedy, Solución Java, solución Python, solución C++, prep de entrevista, belleza de array, complejidad del tiempo, complejidad del espacio.