-...
Título: LeetCode 2640. Encontrar la puntuación de todos los prefijos de un Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 2640. Encontrar la puntuación de todos los prefijos de un Array
**Un blog completo, SEO-Optimized Post + Solución de 3 idiomas**

■ *LeetCode 2640 – “Encontrar la puntuación de todos los prefijos de un Array”*
■ *Java, Python, C++ implementaciones*
■ *Ya disponible, O(n) time " O(1) space solution*

-...

## 1. Recaptación de problemas

Se le da una matriz de enteros 0-indexado **nums** de longitud *n* (1 ≤ * n* ≤ 105).
Para cada prefijo `nums[0..i]` Debes:

1. Construir la matriz *conversión*
`conver[j] = nums[j] + max(nums[0.j]) `
2. Sum el array de conversión → el *score* de ese prefijo.

Devuelva un array 'ans' donde `ans[i]` es la puntuación del prefijo que termina en el índice `i`.

■ *Ejemplo*
[2,3,7,5,10]` → ans = `[4,10,24,36,56]

-...

## 2. Por qué se ve difícil (la parte “única”)

A primera vista, usted podría pensar que necesita recomputar el máximo para cada prefijo, llevando a **O(n2)**.
El giro es que **max(nums[0..j])** se puede mantener *online* como usted iterate – un solo pase es suficiente.

-...

## 3. La elegante solución “buena” – Suma prefijo + Máximo funcionamiento

Silencio Lo que mantenemos en la vida ¿Por qué funciona
...------------------------------
TENIDO 1 TENIDO `currMax` – valor máximo visto hasta ahora ANTE `max(nums[0..i])` es exactamente el máximo de funcionamiento. Silencio
Silencio 2 Silencio `ans[i]` – resumen de los valores de conversión Silencio Cada nuevo valor de conversión es `nums[i] + currMax`; añádalo al total anterior. Silencio

Eso es – **un bucle** sobre el array.

### Pseudocode

`` `
currMax = 0
total Puntuación = 0
para cada una de las numidades:
currMax = max(currMax, num)
total Puntuación += num + currMax
tienda total Puntuación en el array de respuesta
`` `

No se requiere ningún arreglo adicional para los valores de conversión – los calculamos en la mosca.
Complejidades:

Un pase.
- **Espacio**: `O(1)` – sólo unos pocos escalares más el array de salida.

-...

## 4. Full Implementations

A continuación se encuentran soluciones limpias, listas para copiar en **Java**, **Python**, y **C+**.

■ **Nota:** Los tres utilizan `long`/`long' para evitar el desbordamiento (nums[i] ≤ 109, n ≤ 105 → suma ≤ 2 × 1014).

-...

#### 4.1 Java

``java
importar java.util*;

Solución de la clase pública {}
public long[] findPrefixScore(int[] nums) {
int n = nums.length;
long[] ans = new long[n];

int currMax = 0;
total largo = 0;
para (int i = 0; i)
currMax = Math.max(currMax, nums[i]);
total += nums[i] + currMax;
as[i] = total;
}
devolver los ans;
}

// Conductor simple para pruebas rápidas
public static void main(String[] args) {
Solución s = nueva solución ();
int[] nums = {2, 3, 7, 5, 10};
System.out.println(Arrays.toString(s.findPrefixScore(nums)));
}
}
`` `

-...

#### 4.2 Python

``python
de la importación Lista

Solución de clase:
def find PrefixScore(self, nums: List[int]) - List[int]:
ans = []
curr_max = 0
total = 0
para las numidades:
curr_max = max(curr_max, num)
total += num + curr_max
ans.append(total)
Retorno

Prueba rápida
si __name_ == "__main__":
s = Solución()
print(s.findPrefixScore([2, 3, 7, 5, 10])
`` `

-...

#### 4.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector iniciado largo tiempo contacto encontrarPrefixScore(vector seleccionadoint compartir nums) {
vector realizado largamente largas ans;
ans.reserve(nums.size());

int currMax = 0;
long long total = 0;
para (int num : nums) {
currMax = max(currMax, num);
total += num + currMax;
as.push_back(total);
}
devolver los ans;
}
};

// Arnés de prueba simple
int main() {}
Solución s;
vector implicado nums = {2, 3, 7, 5, 10};
auto res = s.findPrefixScore(nums);
para (auto v : res) cout se llevó a cabo v
cout se realizó endl;
}
`` `

-...

## 5. Casos de borde " Pitfalls comunes

Silencio Caso confidencialidad ¿Qué hay que ver para Silencio
Silencio...
Silencio **Gran número** Silencio Uso 64-bit (`long` / `long long`). Silencio
Silencio **Todos los elementos iguales** Silencio `currMax` se mantiene igual; algoritmo todavía O(n). Silencio
TEN **Strictly decreasing array** Actualizaciones de ‘currMax’ sólo en el primer elemento. Silencio
Silencio ** Longitud de entrada = 1** tención Obras: ans[0] = 2 × nums[0]. Silencio
Silencio **Números negativos** (no en limitaciones) Silencio Algorithm todavía válido, pero "currMax` podría ser negativo. Silencio

-...

## 6. Por qué esta solución gana entrevistas

1. **Simplicidad** – un bucle, variables mínimas.
2. **Optimality** – pasa todos los límites del código de leetificación (105 elementos).
3. **Readability** – nombres variables claros (`currMax`, `total`).
4. **Idioma Agnostic** – la lógica es la misma en Java, Python, C++.

Los entrevistadores a menudo preguntan: *“¿Puedes evitar recomputar el máximo para cada prefijo?”* – respuesta con el truco máximo de ejecución.

-...

## 7. Mejoras adicionales (opcional)

Silencio Silencio Silencio Silencio
Silencio------------------------
← **Streaming** – si la entrada viene como un flujo, usted puede obtener puntuaciones inmediatamente. No se necesita ningún arreglo adicional. Necesita manejar el formato de salida. Silencio
Silencio **Suma prefijo Parallel** – para arrays masivos en GPU. tención de velocidad en datos grandes. Sobrematar a LeetCode. Silencio

-...

## 8. Final Takeaways

- **Fix Score** = suma acumulativa de `nums[i] + runningMax`.
- Mantener un solo `currMax` y un 'total' en funcionamiento.
- **O(n) time, O(1) auxiliar space** – la solución más limpia.
- Funciona de forma impecable en Java, Python y C++.

¡Confíe en dejar esto en su carpeta de herramientas de entrevista!

-...

## 9. SEO Tags " Palabras clave

- LeetCode 2640
- Encontrar la puntuación de todos los prefijos de un Array
- algoritmo de suma prefijo
- Solución de suma prefijo Java
- Python prefix sum solution
- Solución de suma prefijo C++
- Problemas de codificación de entrevistas
- La complejidad del tiempo
- Competencia espacial O(1)
- Correr el máximo
- Problema algorítmico resolver

¡Feliz codificación, y buena suerte aterrizando ese trabajo!