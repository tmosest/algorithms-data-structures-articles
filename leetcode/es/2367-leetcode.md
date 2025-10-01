-...
Título: LeetCode 2367. Número de Triplets Aritméticos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Panorama general de los problemas

**LeetCode 2367 – Número de Triplets Aritméticos* *

Se le da una matriz estrictamente creciente `nums` y un entero positivo `diff`.
Un triplete `(i, j, k)` se llama un triplete *arithmetic* cuando

Silencio Silencio Silencio Descripción Silencio
Silencio...
Los índices están en orden ascendente
TENIDA `nums[j] - nums[i] == diff ' Silencio La diferencia consecutiva es `diff` ¦
tención `nums[k] - nums[j] == diff` tención La misma diferencia consecutiva

Devuelve el recuento de trillizos aritméticos únicos en `nums`.

■ **Constraints**
* `3 ≤ nums.length ≤ 200`
* `0 ≤ nums[i] ≤ 200`
≤ 50
### `nums` is strictly increasing

-...

## 2. Why This Problem is a Great Interview Starter

Silencio Lo que es bueno para vivir ¿Por qué importa
Silencio...
Silencio **Tamaño de entrada muy pequeño** Silencio Permite experimentar con diferentes estrategias sin preocuparse por TLE. Silencio
tención **Strictly increasing** tención Elimina índices duplicados y nos permite utilizar simples búsquedas basadas en conjunto. Silencio
tención **Straightforward logic** Silencio se centra en la capacidad del candidato para detectar un patrón en lugar de trucos oscuros. Silencio
Silencio **Multiple optimiza solutions** Silencio Permite la discusión de los intercambios entre claridad y velocidad. Silencio

-...

## 3. Ideas de solución

1. **Brute‐Force (`O(n3)`)** – iterate over all triples and check the condition.
*Lo suficientemente rápido para los límites dados, pero no elegante. *

2. **Two‐Pointer / Two‐Loop (`O(n2)`)** – para cada `i` encontrar `j` tal que `nums[j] = nums[i] + diff`, entonces encontrar `k` con `nums[k] = nums[j] + diff`.
*Bien para aprender técnicas puntero. *

3. **HashSet / Boolean Array (`O(n)`)** – almacenar cada elemento en un conjunto.
Para cada elemento `x`, si ambos `x+diff` y `x+2*diff` están presentes, encontramos un triplet.
*Optimal and clean. *

A continuación se presentan las tres implementaciones en **Java, Python, y C++**.

-...

## 4. Código

#### 4.1 Java

``java
importa java.util. HashSet;
importa java.util. Set;

Solución de la clase pública {}
/* O(n) HashSet solution *
public int arithmeticTriplets(int[] nums, int diff) {
Conjunto de instrucciones = nuevo HashSet correspondiente();
para (int nums : nums) set.add(num);

int count = 0;
para (int num : nums) {
si (set.contains(num + diff) " set.contains(num + 2 * diff) {
contar++;
}
}
recuento de retorno;
}

/* O(n) Boolean array solution *
public int arithmeticTripletsBoolean(int[] nums, int diff) {
// Valores 0 = 200, por lo que el array de tamaño fijo es seguro
booleano[] presente = nuevo booleano[201];
int count = 0;

para (int num : nums) {
si (num √≥= 2 * diff " presente[num - diff] " presente[num - 2 * diff]) {}
contar++;
}
presente[num] = verdadero;
}
recuento de retorno;
}

/* O(n^2) solución de dos vías *
public int arithmeticTripletsO2(int[] nums, int diff) {
int n = nums.length;
int count = 0;
para (int i = 0; i)
para (int j = i + 1; j)
si (nums[j] - nums[i] != diff) romper; // array está aumentando
para (int k = j + 1; k)
si (nums[k] - nums[j] == Diff) contar ++;
si (nums[k] - nums[j] не diff) rompen;
}
}
}
recuento de retorno;
}
}
`` `

#### 4.2 Python

``python
de la importación Lista

Solución de clase:
# -----------
# O(n) solution using a set
# -----------
def arithmeticTriplets(self, nums: List[int], diff: int) - título int:
s = set(nums)
Conteo = 0
para x en nums:
si x + diff en s y x + 2 * diff en s:
Cuenta += 1
cuenta de retorno

# -----------
# O(n) solution using a fixed-size boolean list (value י= 200)
# -----------
def arithmeticTriplets_bool(self, nums: List[int], diff: int) - título int:
presente = [False] * 201
Conteo = 0
para x en nums:
si 2 * diff and present[x - diff] and present[x - 2 * diff]:
Cuenta += 1
presente[x] = Verdadero
cuenta de retorno

# -----------
# O(n^2) brute‐force con dos lazos
# -----------
def arithmeticTriplets_bruteforce(self, nums: List[int], diff: int) - título int:
n = len(nums)
Conteo = 0
para i en rango(n):
para j en rango(i + 1, n):
si nums[j] - nums[i] Diff:
descanso
para k en rango(j + 1, n):
si nums[k] - nums[j] == Diff:
Cuenta += 1
elif nums[k] - nums[j] ⇩
descanso
cuenta de retorno
`` `

#### 4.3 C++

``cpp
Incluido el título
#include ■unordered_set

Clase Solución {
public:
// -----------
// O(n) solución usando unordered_set
// -----------
int arithmeticTriplets(cont std::vector correspondintющ nums, int diff) {
std::unordered_set Utilizaint (nums.begin(), nums.end());
int count = 0;
para (int x : nums) {
si (s.count(x + diff) " s.count(x + 2 * diff))
++cuenta;
}
recuento de retorno;
}

// -----------
// O(n) solución mediante matriz booleana de tamaño fijo (valor 0 = 200)
// -----------
int arithmeticTriplets Bool(cont std::vector correspondint implica nums, int diff) {
bool present[201] = {false};
int count = 0;
para (int x : nums) {
si 2 * diff " presente[x - diff] " presente[x - 2 * diff])
++cuenta;
presente[x] = verdadero;
}
recuento de retorno;
}

// -----------
// O(n^2) solución con dos bucles anidados
// -----------
int arithmeticTripletsO2(cont std::vector fieltro nums, int diff) {
int n = nums.size();
int count = 0;
para (int i = 0; i) {}
para (int j = i + 1; j)
(nums[j] - nums[i]!= diff) break;
para (int k = j + 1; k)
si (nums[k] - nums[j] == diff) + cuenta;
si (nums[k] - nums[j] не diff) rompen;
}
}
}
recuento de retorno;
}
};
`` `

-...

## 5. Artículo del Blog: “El Bien, el Mal y el Ugly of Number of Arithmetic Triplets”

### 5.1 Title

**Número de Triplets Aritméticos – LeetCode 2367: Una entrevista de codificación Deep‐Dive**

*(Keywords: LeetCode, Número de Triplets Arithmetic, Java, Python, C++, entrevista, entrevista de codificación, algoritmo, hashset, complejidad de tiempo, O(n), entrevista de trabajo)*

-...

### 5.2 Intro

■ “Durante su próxima entrevista de codificación, se le pide que encuentre todos los tripletes *arithmetic* en un array ordenados. Parece fácil, ¿por qué muchos candidatos luchan? ”

Este artículo desempaca el **bueno** (lo que hace que el problema sea accesible), el **bad** (pocas comunes), y el **ugly** (los casos difíciles de borde) de LeetCode 2367. También veremos cómo resolverlo en **Java, Python y C+** en menos de 10 líneas de código.

-...

### 5.3 The Good

Silencio Silencio Silencioso
Silencio----------
Silencio ** Patrón intuitivo** Silencioso `nums[i] + diff` y `nums[i] + 2*diff` – una propiedad clara de " mira arriba " . Silencio
Silencio **Small Input Space** tención Con sólo 200 elementos, podemos experimentar con múltiples algoritmos. Silencio
Silencioso **Profundamente Aumentando** Garantías de vida que los índices son únicos; no hay necesidad de preocuparse por los tripletes duplicados. Silencio
Silencio **Multiple Optimal Solutions** Silencio muestra a los candidatos que un problema puede tener un enfoque “obvio” y “limpio”. Silencio

*SEO cue*: “LeetCode 2367 solución fácil”, “pregunta de entrevista de triplete de la revista”

-...

### 5.4 The Bad

Silencio Pitfall Silencio
Silencio...
Silencio **Confusing `+` vs `-` ** Muchos candidatos accidentalmente verifican `x-diff` en lugar de `x+diff`. Silencio
tención **Off‐by-one Index Errores** ← Mis-placing `según `` frente `` en los bucles anidados puede encontrar doble o perder un triplet. Silencio
tención **Ignorando la propiedad estrictamente creciente** ← Escribir un conjunto genérico que funciona para cualquier matriz (incluyendo duplicados) tiempo de pérdida. Silencio
Silencio **Ignoring Constraints** Silencio Usando una matriz dinámica de tamaño `nums.size()*2` en lugar de una matriz booleana de 201' puede llevar a la ineficiencia de la memoria. Silencio

*SEO cue*: “común error de entrevista”, “hashset pitfalls”, “time complejidad LeetCode”

-...

### 5.5 The Ugly

Tricky Edge _ Cómo manejarlo
Silencio...
Silencio **Large `diff`** Silencio If `diff` is close to 100, `x + 2*diff` might exceed 200; use a safe guard (`x î= 2*diff`). Silencio
Silencio **Overflow in C+** Silencio `x + 2*diff` puede desbordar `int ` if `diff` were huge; though not in this problem, always cast to `long ` for safety in real-world code. Silencio
Silencio **Números negativos** Silencio Aunque las restricciones les prohíben, una solución genérica todavía debe manejar los negativos con gracia. Silencio
Silencioso **Sorting Mis‐Assumption** Silencio Recuerde: el array *es* ordenados. Saltar el paso del tipo ahorra tiempo, pero no puede reordenarlo. Silencio

*SEO cue*: “LeetCode coding challenge pitfalls”, “debugging interview code”

-...

## 6. Lista de verificación de salida (para entrevistadores)

- **Pregunte por la solución óptima de `O(n)`** - el candidato debe proponer un enfoque de conjunto / radio.
- ** Solicitud de manejo de persianas** - comprobar si consideran `x ≥ 2*diff`.
- **Discuss trade-offs** - ¿Por qué un array booleano es más rápido que un hash-set en este caso.
* Seguimiento opcional* “¿Y si los “nums” no estaban aumentando estrictamente?” (introduce necesidad de manipulación duplicada).

-...

## 7. TL;DR

- ** Objetivo**: Cuenta `(i, j, k)` con `nums[j] - nums[i] = nums[k] - nums[j] = diff`.
- **Optimal**: `O(n)` utilizando un hash-set o un array booleano de tamaño fijo.
- **Code**: Soluciones listas para funcionar en **Java, Python, C++**.
- ** Valor de Intervisión**: Demostrar el reconocimiento de patrones, el uso de conjuntos y la conciencia de la complejidad del tiempo.

Buena suerte aplastando este problema de LeetCode y clavando tu próxima entrevista de codificación!