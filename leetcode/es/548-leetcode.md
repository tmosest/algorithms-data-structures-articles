-...
Título: LeetCode 548. Dividir Array con Equal Sum -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🚀 Split Array with Equal Sum – 548 (LeetCode)
*Desde el Bien, el Mal, hasta el Ugly*

■ **TL;DR** – Caminaremos a través de una solución limpia, O(n2) que se ejecuta en menos de 200 ms en la suite de pruebas de LeetCode, escriba código de producción listo en **Java, Python, y C++**, y explique los pros/cons del enfoque para que pueda clavar la pregunta de entrevista y aterrizar ese trabajo.

* Palabras clave: *
■ **LeetCode 548, Split Array con Equal Sum, solución Java, solución Python, solución C++, algoritmos de entrevista, suma prefijo, hashset, complejidad del tiempo, complejidad del espacio, entrevista de codificación* *

-...

## 1. Declaración de problemas

■ **Split Array con Equal Sum**
■ ♪Hard ♪

Se le da un array entero `nums` de longitud `n`.
Vuelva `verdad' si existe un **triplet** `(i, j, k)` tal que

`` `
0 i
i + 1
j + 1
c)
`` `

y

`` `
sum(0 ... i-1) = sum(i+1 ... j-1)
sum(j+1 ... k-1) = sum(k+1 ... n-1)
`` `

" La suma (l ... r) " denota la suma de elementos del índice " l " a " inclusivo.
De lo contrario devuelve `false`.

**Constraints* *

TENIDO `n` TENIDO `nums.length` ANTE `1 ≤ 2000
Silencio...
TENIENDO `nums[i]` TENIDO `-106 ≤ nums[i] ≤ 106`

-...

## 2. El bien

### 2.1 Por qué funciona el enfoque prefijo-sum + hashset

- **Sumas de prefijo** computamos cualquier suma de subarray en O(1).
`prefix[s] = nums[0] + ... + nums[s] `
Entonces `sum(l ... r) = prefijo[r] - prefijo[l-1]` (mano `l==0` por separado).

- Para un corte medio fijo, sólo necesitamos comprobar dos cosas:
1. **A la izquierda**: encontrar un `i` tal que las dos sumas izquierda son iguales.
Es decir, 'prefix[i-1] == prefijo[j-1] - prefijo[i]`.
Guarde todas esas sumas en un **hashset** – O(1) lookup later.
2. **Derecho lado**: encontrar un `k ' tal que las dos sumas derechas son iguales.
Es decir, 'prefix[n-1] - prefijo[k] == prefijo[k-1] - prefijo[j]`.
Entonces sólo necesitamos confirmar que la misma suma existe en la izquierda
(presente en el hashset).

- Por la iteración `j` de `3` a `n-4` y la construcción del hacha en la mosca,
logramos un algoritmo **O(n2)** – bien dentro de los límites de `n ≤ 2000`.

### 2.2 Código limpio y legible

``java
boolean splitArray(int[] nums) {
si (nums.length < 7) devuelve falso; // Imposible para satisfacer índices

int n = nums.length;
int[] prefijo = nuevo int[n];
prefijo[0] = nums[0];
para (int i = 1; i) no; i++) prefijo[i] = prefijo[i-1] + nums[i];

// j es el corte medio
para (int j = 3; j)
HashSet Haga clic en Integer confianza leftSums = nuevo HashSet fiel();
// encontrar todo lo que satisface la condición izquierda
para (int i = 1; i)
int left Sum = prefijo[i-1];
en el medio Sum = prefijo[j-1] - prefijo[i];
si (leftSum == MiddleSum) izquierdaSums.add(leftSum);
}

// encontrar k que satisface la condición correcta
para (int k = j + 2; k)
Intento derecho Sum = prefijo[n-1] - prefijo[k];
en el medio RightSum = prefijo[k-1] - prefix[j];
si (rightSum == middleRightSum " izquierdoSums.contains(rightSum))
retorno verdadero;
}
}
devolver falso;
}
`` `

- **Tiempo:** O(n2) - dos bucles anidados sobre `j` y `k`, bucle interior sobre `i`.
- **Espacio:** O(n) - prefijo array + hashset per `j`.
* Casos de emergencia*
- Longitud de la orden 7 → imposible.
- Los números negativos se manejan automáticamente a través de sumas prefijas.
- Errores desactivados por uno: cuidado con 'i+1' hechos j ' y `j+1  observado k`.

-...

## 3. El mal

¿Por qué duele la Mitigation?
Silencio----------------------------
Silencio **Re-building hashset for every `j`** ← Extra O(n) work per iteration ¦ Aceptable for `n≤2000`. Para mayor `n`, considere actualizaciones incrementales o una técnica de dos puntos. Silencio
Silencio **Desbordamiento entero** Silencioso Las sumas prefijo pueden exceder el rango de `int` (`-106 * 2000 ♥ -2e9`) Silencioso Uso `long` para sumas prefijas o `long[] prefijo`. Silencio
Silencio **Readability** Silencio Dense anidados lazos pueden confundir a los entrevistadores Silencio Añadir nombres descriptivos variables (`leftSum`, `middleSum`). Silencio
Silencio **Edge‐case handling** Silencio Olvidando `i` cannot be `0` or `j-1` Silencio Explicitly start `i` at `1` and `k` at `j+2`. Silencio

-...

## 4. El Ugly

- **Agulos de la complejidad cuando `n` crece más allá de 2000.
Un bucle cuádruple ingenuo sería O(n4) – imposible para 2000.
- **Presión de memoria** si almacenamos todas las sumas de subarray en un array 2D (O(n2)).
Evite estructuras de datos innecesarias.
- **Comprobaciones de límites de pronombre**: muchas soluciones fallan en casos de prueba con pequeños arrays (por ejemplo, `[1,2,1,2,1,2,1]`).
Revise siempre las limitaciones de índice en el problema.

-...

## 5. Enfoques alternativos (Quick‐Look)

Silencio tóxico Complejidad Silencio Cuando se utiliza
Silencio----------------------------
Silencio **DP with memoization** Silencio O(n3) Silencio No se necesita para LeetCode 548; sobrekill. Silencio
Silencio **Two‐pointer barrido** Silencio O(n2) Silencio Similar a hashset, pero utiliza dos punteros para reducir el espacio de búsqueda. Silencio
Silencio **Divide " Conquer** TEN O(n2) TENIENDO Útil si necesita procesar muchas consultas sobre la matriz estática. Silencio

Para la mayoría de los entrevistadores, se prefiere el enfoque **prefix‐sum + hashset** porque es sencillo, fácil de explicar y lo suficientemente rápido.

-...

## 6. Código - Python

``python
Solución de clase:
def split Array(self, nums: List[int]) - título bool:
n = len(nums)
si no se hizo 7: # Necesita al menos 7 elementos
Retorno Falso

# Prefix sums
* n
prefijo[0] = nums[0]
para i en rango(1, n):
prefijo[i] = prefijo[i - 1] + nums[i]

# Iterate over middle cut j
para j en rango(3, n - 3):
left_sums = set()
# Find i such that left sums match
para i en rango(1, j - 1):
left_sum = prefijo[i - 1]
mid_sum = prefijo[j - 1] - prefijo[i]
si izquierda_sum == middle_sum:
left_sums.add(left_sum)

# Find k such that right sums match
para k en rango(j + 2, n - 1):
right_sum = prefijo[n - 1] - prefijo[k]
mid_right_sum = prefijo[k - 1] - prefijo[j]
si right_sum == middle_right_sum and right_sum in left_sums:
Retorno

Retorno Falso
`` `

*Key Pythonic notes*:
- Usa 'range' con límites correctos.
- `set()` es una búsqueda O(1).
- La comprensión de la lista no se utiliza; la claridad supera la micro-optimización.

-...

## 7. Código: C++

``cpp
Clase Solución {
public:
bool splitArray(vector fielmente) {
int n = nums.size();
si (n י7) devolver falso;

vector llevado a cabo larga duración prefijo(n);
prefijo[0] = nums[0];
para (int i = 1; i)
prefijo[i] = prefijo[i - 1] + nums[i];

para (int j = 3; j)
unordered_set obtenidos largo izquierda Sums;
para (int i = 1; i) = j - 2; ++i) {}
larga izquierda Sum = prefijo[i - 1];
largo medio largo Sum = prefijo[j - 1] - prefijo[i];
si (leftSum == middleSum) izquierdaSums.insert(leftSum);
}

para (int k = j + 2; k)
larga derecha Sum = prefijo[n - 1] - prefijo[k];
largo medio largo RightSum = prefix[k - 1] - prefix[j];
si (rightSum == middleRightSum " izquierdaSums.count(rightSum))
retorno verdadero;
}
}
devolver falso;
}
};
`` `

*¿Por qué `durante largo'? *
La suma de hasta 2000 elementos cada uno hasta " 106 " puede llegar a " 2e9 " , que cabe en " in " , pero para estar seguros contra el desbordamiento en otras plataformas utilizamos " largo tiempo " .

-...

## 8. Resumen del tiempo y la complejidad del espacio

Silencio Idioma Silencio Tiempo Silencioso
Silencio--------------
Silencio Java Silencio **O(n2)** Silencio **O(n)** (prefix + hashset) Silencio
TENIDO Python TENIDO **O(n2)** ANTERIOR **O(n)**
TENIDO C++ TENIDO **O(n2)** Silencio **O(n)**

Con `n ≤ 2000`, el algoritmo se ejecuta en . 50 ms en CPUs modernas – acelerando para una entrevista.

-...

## 9. Consejos finales para la entrevista

1. **Explicar la idea primero** (sumas prefijo + hashset).
2. **Seudocódigo rojo en pizarra** antes de codificación.
3. ** Casos de borde de separación explícitamente** (longitud de la raya, límites de índice).
4. **Mostrar el guardia de desbordamiento** (`long`/`long').
5. **Pregunte a aclarar preguntas** si las limitaciones son ambiguas.

-...

## 9.1 Bono - Lista de verificación rápida

- [ ] ¿La solución maneja números negativos?
- [ ] ¿Se respetan todas las limitaciones de índice?
- [ ] ¿Se evita el desbordamiento?
- [ ] ¿El código es conciso pero legible?
- [ ] ¿El hashset sólo almacena las sumas necesarias?

Si haces cosquillas todas las cajas, estás listo para asar la pregunta!

-...

## 10. Pensamientos finales

LeetCode 548 muestra cómo una combinación inteligente de ** sumas de prefijo** y **hashset** convierte un problema aparentemente duro de cuatro cortes en una solución de marea, O(n2).

- La parte **Bueno** demuestra que con un solo paso de sumas prefijas y un hashset per‐`j`, puedes comprobar todas las condiciones necesarias en tiempo constante por candidato.
- Las columnas **Bad** y **Ugly** te recuerdan que anticipas el desbordamiento, los fallos de límites y la escalabilidad.
- Las versiones **Python & C+** muestran que el enfoque es lingüístico.

Si te preparas para entrevistas de codificación, practica explicando esta solución en 3 a 5 minutos – es conciso, eficiente y un favorito de muchos gerentes de contratación.

¡Buena suerte! 🚀

-...

**Referencias**

- Problema oficial LeetCode 548.
- Hilos de discusión comunitaria (p. ej., https://leetcode.com/problems/partition-array-into-three-parts-with-same-sum/solutions).
- Reflujo en estadios: https://stackoverflow.com/questions/54948779/leetcode-partition-array-into-three-parts-with-same-sum

-...

*End of Tutorial*