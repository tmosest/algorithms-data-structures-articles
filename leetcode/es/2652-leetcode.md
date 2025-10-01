-...
Título: LeetCode 2652. Sum Multiples -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 2652 - **Sum Multiples**
**Su guía para Java, Python & C+++++ + un artículo de blog optimizado SEO* *

■ *“Sum all integers from 1 to n that are divisible by 3, 5, or 7.”*
■ *Dificultad*

-...

## TL;DR

Silencio Idioma Silencio O(1) Math Formula Silencio O(n)
Silencio----------------------------
Silencio **Java** Silencio ✔ `sumOfMultiples(n)` – utiliza la serie aritmética
Silencio **Python** ✔ ✔ `sum_of_multiples(n)` – utiliza la serie aritmética
Silencio **C+** Silencio ✔ `sumOfMultiples(n)` – utiliza la serie aritmética

■ **Escoge la solución de matemáticas** para pasar grandes pruebas en * 1 ms* y impresionar a los entrevistadores.

-...

## Blog Article – “The Good, The Bad, and The Ugly of Sum Multiples”

■ **SEO Palabras clave**: *LeetCode Sum Multiples, Java suma de múltiples, Python sum of multiples, C++ suma de múltiples, entrevista desafío de codificación, solución O(1), serie aritmética, algoritmo entrevista prep*

### #1# ## ## ##

LeetCode 2652 le pide que computa la suma de cada entero entre 1 y n (inclusive) que es un múltiple de 3, 5 o 7.
Las limitaciones son pequeñas (`1 ≤ n ≤ 10^3`) – pero un *single pass* sobre el rango todavía le muestra un enfoque O(n) eficiente. La verdadera pregunta de estilo entrevista es: ¿puedes hacerlo *O(1)* con un truco matemático?

■ **Por qué importa*: A los entrevistadores les encanta ver que usan *inclusión-exclusión* y *seriearitmética* – muestra que usted está cómodo con el análisis de matemáticas y complejidad.

-...

#### 2down⃣ El enfoque de Naïve - O(n) Loop

``java
int sum = 0;
para (int i = 1; i) = n; i++) {
si (i % 3 == 0 Silencioso i % 5 == 0 0) {
suma += i)
}
}
`` `

**Pros**
- Simple de entender
- Funciona para cualquier n

**Cons**
- Tiempo lineal → innecesario para pequeños escenarios de entrevistas en el mundo real
- No demuestra un pensamiento algoritmo más profundo

■ **Bottom line**: buena para una solución rápida, mala para una entrevista de codificación *real*.

-...

### 3 comentarios La elegante solución matemática O(1)

Utilizamos la fórmula para la suma de una serie aritmética:

\[
S_k = k + 2k + 3k + \dots + mk = k \times \frac{m(m+1)}{2}
\]
Donde `m = ⌊n/k⌋`.

**Principio de inclusión* *

- Suma de múltiplos de 3 + múltiplos de 5 + múltiplos de 7
- Extractos múltiples de 15 (3×5), 21 (3×7), 35 (5×7) (una vez contados dos veces)
- Añada varios de 105 (3×5×7) de vuelta (desde entonces restados tres veces)

**Formula* *

`` `
S = sumMultiples(3) + sumMultiples(5) + sumMultiples(7)
- sumMultiples(15) - sumMultiples(21) - sumMultiples(35)
+ sumaMultiples(105)
`` `

Where `sumMultiples(k)` is computed in O(1) as:

`` `
m = n / k
k * m * (m +1) / 2
`` `

** Beneficios**

- **Hora**: O(1) - no bucles
- **Espacio**: O(1)
- **Readability**: Muestra el dominio del diseño de matemáticas y algoritmos
- **Performance**: Pasa millones de casos de prueba al instante

-...

### 4down⃣ Code Snippets – Listo para copiar

#### 4.1 Java (O(1) Math)

``java
Clase Solución {
int sumOfMultiples(int n) {
(int) (sum(n, 3) + sum(n, 5) + sum(n, 7)
- sum(n, 15) - sum(n, 21) - sum(n, 35)
+ suma n, 105);
}

privada larga suma (int n, int k) {
largo m = n / k;
retorno (long) k * m * (m +1) / 2;
}
}
`` `

##### 4.2 Python (O(1) Math)

``python
Solución de clase:
def sumOfMultiples(self, n: int) - int:
def s(k: int) - Propiedad int:
m = n // k
k * m * (m +1) // 2

(Retorno)
s(3) + s(5) + s(7)
- s(15) - s(21) - s(35)
+ s(105)
)
`` `

##### 4.3 C++ (O(1) Math)

``cpp
Clase Solución {
public:
int sumOfMultiples(int n) {
auto sum = [ cl](int k) - título largo
largo m = n / k;
retorno 1LL * k * m * (m +1) / 2;
};
retorno estático_cast
suma(3) + suma(5) + suma(7)
- sum(15) - sum(21) - sum(35)
+ suma(105)
);
}
};
`` `

■ **Tip**: Use `long’ para los productos intermedios para evitar el desbordamiento, aunque la respuesta final se ajuste en `int`.

-...

### 5down⃣ Edge Cases " Common Pitfalls

Silencio Silencio
Silencio...
tención Integer desbordamiento en Java/C++ Utilizar `long`/`long' para cálculos intermedios
← Olvidar la inclusión–exclusión Silencio Verify that each multiple set is added/subtracted properly ←
tención Off‐by-one errores (n inclusive) Silencio Uso `n / k` para contar cuántos múltiples existen hasta `n` Silencio
Silencio Pruebas sólo pequeñas n ← Ejecutar pruebas de estrés hasta 10^9 para confirmar las obras de fórmula

-...

Desglose de la complejidad

Silencio Silencio Silencio Silencio Silencio
Silencio--------------
O(n) Loop Silencio **O(n)** Silencio **O(1)**
Silencio O(1) Matemáticas infligidas **O(1)**

■ **Takeaway**: En entrevistas, prefiere la solución O(1) – muestra que sabes cómo optimizar y utilizar las matemáticas para reducir el tiempo de ejecución.

-...

### 7down⃣ Interview Takeaways

1. **Siempre piden restricciones** – le guían a la correcta complejidad.
2. ** Explique su proceso de pensamiento** – hable de inclusión, exclusión, serie aritmética y por qué eligió O(1).
3. ** Casos del borde de la mención** – desbordamiento, grande `n`, y cómo se protege contra ellos.
4. **Estar listo para implementar** – dar código limpio y bien comunicado (ver los fragmentos arriba).

-...

### 8️ Practice, Practice, Practice

- **LeetCode**: 2652 - Sum Multiples
- **GeeksforGeeks**: “Arithmetic Series Sum” – refresca la fórmula
- **HackerRank**: "Inclusión-Exclusión" problemas de práctica

-...

## ## 9Ω⃣ Palabras finales

El problema Sum Multiples es un *clásico* para aprender cómo convertir un simple bucle en una solución matemáticamente elegante. Al dominar la inclusión-exclusión y la serie aritmética, usted:

- Reducir la complejidad del tiempo de linear a constante
- Show interviewers you think beyond brute force
- Aumentar la confianza para problemas más difíciles (por ejemplo, contar coprimes, función mobius)

■ **Pro tip**: Cuando termine, escriba una suite de prueba de unidad rápida (JUnit/pytest/GoogleTest) para cubrir casos de borde. Muestra profesionalidad y atención al detalle.

-...

## 📚 Referencias > Leer más

- LeetCode 2652 – [Sum Multiples](https://leetcode.com/problems/sum-multiples/)
- GeeksforGeeks – [Arithmetic Progression Sum](https://www.geeksforgeeks.org/arithmetic-progressions/)
- Brillante.org – [Principio de inclusión-exclusión] (https://brilliant.org/wiki/inclusion-principle/)

-...

## 🚀 Get Your Job

¿Quieres aterrizar ese papel de ingeniería de software?
# Sigue # nuestro canal para más avances de LeetCode #
*Descargar* la lista de verificación gratuita de la entrevista
- **Reach out** para el entrenamiento personalizado

¡Feliz codificación