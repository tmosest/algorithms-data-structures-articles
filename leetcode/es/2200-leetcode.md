-...
Título: LeetCode 2200. Encuentra todos los índices de distancia en un Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Find All K‐Distant Indices in an Array
**(LeetCode 2200 – Easy)* *

■ *“El bueno, el malo y el feo” – una profunda inmersión en un problema aparentemente simple, cómo resolverlo rápido, y cómo puedes mostrarlo en una entrevista. *

-...

## 🚀 Why This Problem Matters

* * Interview‐ready** – Es una pregunta “medium-easy” frecuente sobre LeetCode y es un elemento básico en muchas entrevistas de estructura de datos.
* **Mostrar la comprensión de los trucos prefijo de dos puntos** – Una solución limpia muestra una comprensión sólida del pensamiento algoritmo.
* ** Fácil de optimizar** – La solución ingenua es \(O(n^2)\); la óptima es \(O(n)\) y espacio constante.

Si puede explicar los cambios y dar una implementación limpia en Java, Python o C++, impresionará a cualquier gerente de contratación.

-...

## 📌 Declaración de problemas (Restated)

■ Dado un conjunto entero de `nums ' , un valor `key ' que aparece en `nums ' , y un entero `k ' ,
* * lista de todos los índices " i " que existen al menos un índice " con
■[
не ный - j eterna \le k \quad\text{and}\quad nums[j] == clave
"
■
■ 1 ≤ `nums.length` ≤ 1 000
■ 1 ≤ `nums[i]
■ 1 ≤ `k` ≤ `nums.length `

-...

## Dos soluciones

TENIDO ANTERIENTE TENIDO Tiempo ANTERIENTE Espacio Por qué importa
Silencio------------------------------
TENIDO **Brute‐Force** – comprobar cada par TENIDO \(O(n^2)\) Silencio \(O(1)\) Silencio Fácil de implementar, pero lento para n Ω 1 000. Silencio
Silencio **Un paso con marcación** – **Optimal** tención **\(O(n)\)** Silencio \(O(1)\) Silencio Escanes una vez, sin bucles anidados, sólo matemáticas enteros. Silencio

Nos enfocaremos en la solución óptima y proporcionaremos el código en tres idiomas populares.

-...

## 🔍 Optimal Strategy – One‐pass Marking

1. **Traverse** el array una vez.
2. Cuando `nums[j] == key`, los índices que se vuelven **k-distant** son el rango
\[
\text{left} = \max(0, j - k) \quad\text{to}\quad \text{right} = \min(n-1, j + k)
\]
3. En lugar de añadir cada índice en esa gama **naively**, mantenga un puntero en ejecución `nextFree`.
* `nextFree` es el índice más pequeño **no** aún añadido.
* Para cada clave, solo añadimos el intervalo `[max(nextFree, left), right].
4. Después de procesar una clave, establece `nextFree = derecha + 1`.
5. Finalmente devuelve los índices recogidos.

La idea es similar a la “línea del sudor” o “interval merging” – nunca revisitamos un índice que ya se ha añadido.

-...

## 🧪 Test Cases

← Intromisión esperada
Silencio...
TENIENDO `nums=[3,4,9,1,3,9,5] ``, `key=9`, `k=1` ANTE `[1,2,3,4,5,6] Silencio
TENIDO `nums=[2,2,2,2,2,2] ``, `key=2`, `k=2` ANTE `[0,1,2,3,4] ` Silencio
TENIENDO `nums=[1,2,3,4,5]`, `key=3`, `k=0` Silencio `[2]
TENIENDO `nums=[1,3,1,3,1]`, `key=1`, `k=1` ANTE `[0,1,2,3,4] ` Silencio

-...

Código

## Java

``java
importar java.util*;

Solución de la clase pública {}
public List Noms, int key, int k) {}
Lista de datos:Integer confianza res = nuevo ArrayList correctamente();
int n = nums.length;
int nextFree = 0; // menor índice aún no añadido

para (int j = 0; j) {}
si (nums[j] == key) {}
int left = Math.max(0, j - k);
int right = Math.min(n - 1, j + k);

int start = Math.max(left, nextFree);
para (int i = start; i <= right; i++) {}
res.add(i);
}
siguienteLibro = derecho + 1; // evitar duplicados
}
}
restitución;
}

public static void main(String[] args) {
Solución s = nueva solución ();
System.out.println(s.findKDistantIndices(s)
int[]{3,4,9,1,3,9,5}, 9, 1)); // [1,2,3,4,5,6]
}
}
`` `

## Python

``python
de la importación Lista

Solución de clase:
def findKDistantIndices(self, nums: List[int], key: int, k: int) - título List[int]:
n = len(nums)
res = []
siguiente_free = 0 # primer índice que no se ha añadido

for j, val in enumerate(nums):
si vale == llave:
izquierda = max(0, j - k)
derecho = min(n - 1, j + k)

inicio = max(izquierda, siguiente_gratis)
res.extend(range(start, right + 1))
siguiente_gratis = derecha + 1

retorno

si __name_ == "__main__":
sol = Solución()
print(sol.findKDistantIndices([3,4,9,1,3,9,5], 9, 1)) # [1,2,3,4,5,6]
`` `

### C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector identificador confianza encontrarKDistantIndices(vector identificadoint hombro nums, int key, int k) {
vector res;
int n = nums.size();
int nextFree = 0; // el índice más pequeño aún no aprobado

para (int j = 0; j)
si (nums[j] == key) {}
int left = max(0, j - k);
int right = min(n - 1, j + k);

int start = max(left, nextFree);
para (int i = start; i) = right; ++i)
res.push_back(i);
siguienteGratis = derecha + 1; // saltar índices ya añadidos
}
}
restitución;
}
};

int main() {}
Solución s;
vector implicado ans = s.findKDistantIndices({3,4,9,1,3,9,5}, 9, 1);
para (int x : ans) cout se hizo x se hizo '
// Producto: 1 2 3 4 5 6
}
`` `

■ **Tip** – En los tres idiomas la lógica central es idéntica:
*encuentre el intervalo alrededor de cada tecla, fusione con el intervalo ya previsto, y mantenga un puntero “next free”. *

-...

## 📈 Complexity Analysis

TEN TERMINAR ANTERIOR ANTERIOR ANTERIOR ANTERIOR Óptimo
Silencio----------------------------
Silencio ** Tiempo** Silencioso \(O(n^2)\) Silencio
Silencio **Auxiliary Space** Silencio \(O(1)\) Silencio **\(O(1)\)** (aparte de la lista de resultados)
Silencio ** Tamaño del resultado** Silencio \(O(n)\) (la matriz misma) TENIDO \(O(n)\) Silencio

Con `n ≤ 1 000`, la solución óptima terminará en milisegundos, mientras que la fuerza bruta puede tomar varios cientos milisegundos, a menudo suficiente para causar una advertencia en una entrevista temporizada.

-...

## ⋅ Common Pitfalls (El Ugly)

Silencio Pitfall Silencio
Silencio...
**Añadiendo índices dentro de la totalidad `[izquierda, derecha]` intervalo para cada tecla** – conduce a duplicados. Use el puntero "nextFree" o un "boolean[] visto. Silencio
TEN **Off‐by-one errores al actualizar `next Gratis** Silencio Recuerda: `nextFree = right + 1`. Silencio
Silencio **Ignorando los límites de los arrays** (`j-k` ) 0 o `j+k` ≥ n) Silencio Clamp con `Math.max(0, ...)` y `Math.min(n-1, ...)`. Silencio
tención **Usando un `Set` a dedupe indices** – funciona pero utiliza \(O(n)\) espacio extra y puede arruinar la reclamación del espacio \(O(1)\). Preferir el truco de puntero. Silencio

-...

## 📚 Take‐aways for Interviews

1. **Explicar la intuición** primero – hablar de “toda clave influye en un intervalo contiguo”.
2. **Discuta los cambios de complejidad** – por qué evitarás \(O(n^2)\) cuando puedas hacer \(O(n)\).
3. **Mostrar la marca de un paso** – es un patrón clásico que aparece en muchos problemas de intervalo (por ejemplo, “max consecutivos II”, “número mínimo de grifos para regar un jardín”).
4. ** Prueba de medición** – proporcionar algunos casos de esquina (k = 0, k ≥ n, todos los elementos iguales a la clave).

-...

##  tuya SEO Checklist (Si estás publicando este post)

Silencio TENIDO TENIDO Cómo optimizar los motores de búsqueda
Silencio.
Silencio **Título** – “Encontrar todos los índices K‐Distant en un Array: Solución óptima de un par” contiene la palabra clave “K‐Distant Indices” + “Optimal One‐pass”
Silencio **Meta Descripción** Silenciosa “Aprenda a resolver LeetCode 2200, encuentre todos los índices K-Distant, con un algoritmo \(O(n)\) y limpiar Java, Python y C++. Prepa de entrevista perfecta.” Silencio
Silencio **Headers** Silencio Use H1 for title, H2 for sections (Problema, Brute‐Force, Optimal, Code, Complexity), H3 for language-specific code. Silencio
Silencio ** Enlaces internos** Silencio Referencia de otros postes de entrevista en “Two‐Pointer Tricks” o “Prefix Sum for Intervals”. Silencio
Silencio ** Enlaces externos** Silencio Enlace a la página de problemas LeetCode, a su GitHub repo, a los recursos de búsqueda de empleo. Silencio
tención **Largo de contenido** tención 800–1,200 palabras; suficiente para cubrir el problema, código y análisis sin ser demasiado verbos. Silencio
tención **Imágenes** Silencio Incluye un pequeño diagrama del concepto de línea de barrido (opcional). Silencio
Silencio **Keywords** Silenciosos “indices de k-distant”, “LeetCode 2200”, “territmo de dos puntos”, “entrevista de estructura de datos”, “codificación de entrevistas de trabajo”. Silencio

-...

## 🎯 Cómo usar este artículo en tu búsqueda de empleo

1. **GitHub Gist** – Publique el código Java/Python/C++ en un repo público e incluya el enlace de reposo en su currículum.
2. **Portfolio** – Inserte el código snippet y explicación en su sitio web personal.
3. **Interview Prep** – Práctica explicando las partes “buenas” (optimal), “bad” (brute-force), y “muy” (negocias ilimitadas).
4. **Networking** – Compartir el blog en LinkedIn con un título:
■ “Acaba de romper un problema de LeetCode que muchos entrevistadores aman. #Java #Python #C++ #DataStructures #EntreviewPrep #

-...

##  Settlement Final Verdict

*El problema “Find All K‐Distant Indices” es engañosamente simple, pero esconde un patrón algoritmo limpio. Al presentar una solución clara \(O(n)\) one‐pass, usted prueba que no es sólo un códice – usted es un problema eficiente-solver que puede reducir la complejidad del tiempo sin sacrificar la claridad. *

¡Feliz codificación y buena suerte en esas entrevistas!