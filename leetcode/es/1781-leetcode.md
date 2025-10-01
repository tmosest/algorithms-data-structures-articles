-...
Título: LeetCode 1781. Sum of Beauty of All Substrings -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🧩 1781. Suma de belleza de todas las subestrings – Solución Full‐Stack

■ **Keywords:** LeetCode 1781, Suma de belleza, Subestrings, Java, Python, C++, Algorithm Interview, Time Complexity, Space Complexity

-...

### 1. Recaptación de problemas

■ **Beauty of a string** = (frecuencia de carácter más común) – (frecuencia de carácter menos común que en realidad aparece).
■ **Task:** Para una determinada cadena `s` (1 ≤ Новывы ≤ 500, letras minúsculas solamente), devolver la suma de los valores de belleza para **all** posibles subestrings.

-...

### 2. Por qué este problema es un gran ejercicio de entrevista

Silencio Silencio Silencio Silencio
Silencio...
TEN **Claridad** – entrada bien definida " salida ANTERI **Nested loops** puede ser confuso para principiantes Silencio **Off‐by-one pitfalls** cuando las frecuencias informáticas ANTE
TEN **Scalability** – 500 longitud → ~125 000 subestrings →  realizadas 1 M operaciones TEN **O(n3) **Las soluciones ingenuas son innecesarias TEN **Large factores constantes** si olvidamos reutilizar el array de frecuencia TENIDO
Silencio **Multi‐language** – Java, Python, C++ → muestra el pensamiento multiplataforma Silencio **Misunderstanding of “least frequent”** (ignore cero counts) Silencio **Desbordamiento entero** (a diferencia de 500, pero vale la pena notar)

-...

### 3. Intuición de fuerza bruta

La forma más directa es enumerar cada subestring, contar la frecuencia de cada letra, luego computar `max - min`.

``text
para mí en 0 .. n-1: // índice de inicio
para j in i .. n-1: //
compute freq[26] of s[i.j]
belleza = max(freq) - min(freq confía0)
total += belleza
`` `

*Complejidad:* `O(n3)` – porque recuento los mismos caracteres muchas veces.
*Pace:* `O(1)` – sólo un array fijo de 26 puntos.

Esto es *aceptable* para `n ≤ 20`, pero para `n = 500` se vuelve demasiado lento.

-...

### 4. Solución óptima O(n2 · 26)

Podemos **reutilizar el array de frecuencia** mientras expande el subestring un personaje a la vez.

``text
para empezar en 0 .. n-1:
freq[26] = {0}
para terminar en el principio. n-1:
freq[s[end]]++ // O(1) update
maxFreq = 0
minFreq = INF
para k en 0 .. 25: // escanear 26 letras
si freq[k] 0:
maxFreq = max(maxFreq, freq[k])
minFreq = min(minFreq, freq[k])
total += maxFreq - minFreq
`` `

* Por qué funciona: *
- Al restablecer `freq` en cada nuevo índice de inicio, aseguramos que sólo consideramos la subestring actual.
- El escaneo interno de 26 letras es constante, por lo que la complejidad general se convierte en `O(n2)`.

*La complejidad:*
- **Tiempo:** `O(n2)` (Ω 125 000 × 26 ♥ 3.2 M ops for `n = 500`) – cómodamente rápido.
- **Espacio: ** `O(1)` - matriz fija de 26 puntos.

-...

### 5. Aplicación del Código

A continuación se presentan soluciones limpias y idiomáticas en **Java**, **Python**, y **C+**.
Los tres siguen la misma lógica y logran la misma complejidad óptima.

-...

##### 5.1 Java

``java
importar java.util*;

Solución de la clase pública {}
belleza int Sum(String s) {
int n = s.length();
total = 0;

para (int start = 0; start < n; start++) {}
int[] freq = nuevo int[26]; // reset para cada inicio
para (int end = start; end {}
freq[s.charAt(end) - 'a']++; // actualización de frecuencia

int maxFreq = 0;
int minFreq = Integer.MAX_VALUE;
para (int f : freq) {
si
máxFreq = f;
f) minFreq = f;
}
}
total += maxFreq - minFreq;
}
}
Total de retorno;
}

public static void main(String[] args) {
Solución sol = nueva solución ();
System.out.println(sol.beautySum("aabcb")); // 5
System.out.println(sol.beautySum("aabcbaa"); // 17
}
}
`` `

-...

#### 5.2 Python

``python
Solución de clase:
def beautySum(self, s: str) - título int:
n = len(s)
total = 0

para comenzar en rango(n):
freq = [0] * 26 # reset para cada inicio
para terminar en rango(start, n):
freq[ord(s[end]) - 97] += 1

max_f = 0
min_f = flotante('inf')
para f en freq:
si f > 0:
si f > máx_f:
max_f = f
si f
min_f = f
total += max_f - min_f

total


# Demo
si __name_ == "__main__":
sol = Solución()
print(sol.beautySum("aabcb")
print(sol.beautySum("aabcbaa")
`` `

-...

#### 5.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
belleza int Sum(string s) {
int n = s.size();
long long total = 0; // use long long for safety

para (int start = 0; start  won n; ++start) {
int freq[26] = {0}; // reset
para (int end = start; end < n; ++end) {
freq[s[end] - 'a']+;

int maxF = 0, minF = INT_MAX;
para (int f : freq) {
si
máxF = f;
f) minF = f;
}
}
total += maxF - minF;
}
}
retorno (int)total;
}
};

/ Demo
int main() {}
Sol de solución;
cout se hizo sol.beautySum("aabcb")
cout se hizo sol.beautySum("aabcbaa")
}
`` `

-...

### 6. Desglose de la complejidad

TEN TERRITOR ANTE ANTERI ANTERIOR ANTERIOR
Silencio----------------------
Silencio Loop exterior (`start`) Silencio en los tiempos Silencio O(n)
Silencio Inner loop (`end`) Silencio n - comienzo de los tiempos
← Actualización de frecuencias
Silencioso Escáneo 26 cartas Silencio 26 × (n2) Silencio O(n2)
**Total** Silencioso
Silencio Espacio adicional TENIDO freq[26]

-...

### 7. Pitfalls comunes " Cómo evitarlos

Silencio Pitfall Silencio Por qué sucede 
Silencio...
Silencio **Counting cero frecuencias as min** Silencio Algunas personas usan erróneamente `minFreq = 0` Inicialmente Silencio Skip `freq == 0` al actualizar min/max Silencio
Silencio **Off‐by‐one in loops** Silencio Olvidando que la subestring termina en `end` inclusive ¦ Silencio
Silencio **Large integer overflow** Silencio A diferencia de 500, pero "int" podría desbordarse para mayores restricciones ¦ Use `long long' (C++) o `long` (Java) si es necesario
tención **Re-alubicación de freq cada vez** ← Menor desaceleración ← Reutilizar un único array y restablecer los valores a 0 Silencio

-...

### 8. Consejos de entrevista

1. ** Explique su razonamiento** – Hable por qué escanear 26 letras es barato y cómo el algoritmo permanece `O(n2)`.
2. **Mención del caso del borde** – Cuando todos los caracteres son iguales, la belleza siempre es 0; nuestro algoritmo naturalmente lo maneja.
3. **Discuten alternativas** – Mención prefijo sumas o ventanas correderas, pero expliquen por qué son innecesarias aquí.
4. *Mostrar su código rápidamente* Incluso si escribe pseudocódigo en papel, esté listo para traducirlo en el idioma solicitado.

-...

### 9. Conclusión

■ **Sum of Beauty of All Substrings** es un problema engañosamente simple que muestra un truco limpio: **Reutilizar una pequeña tabla de frecuencias mientras se expanden subestrings**.
■ La solución óptima funciona en el espacio `O(n2)` tiempo y `O(1)`, lo que lo hace perfecto para los jueces en línea (LeetCode, HackerRank) y entrevistas de codificación en vivo.

Buena suerte – y recuerde: la * belleza* de su solución se encuentra en su **implicidad, eficiencia y claridad de lenguaje cruzado**! 🚀