-...
Título: LeetCode 2979. El artículo más caro que no se puede comprar -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 Resumen del problema: “La mayoría de los artículos costosos que no se pueden comprar”

Silencioso LeetCode ID Silencio 2979
Silencio...
Dificultad para vivir Medio tiempo
Tag tóxico Matemáticas, Teoría del Número Silencio

**Declaración* *
Te han dado dos números principales distintos 'primeOne' y 'prime Dos.
Usted tiene una cantidad infinita de monedas en esas dos denominaciones.
Por cada entero positivo `x` hay un artículo que cuesta `x`.
Devuelve el precio más alto de un artículo que **no puede** ser pagado exactamente con cualquier
combinación de las dos monedas.

*Examples*

Silencioso `primeOne` Silencio `primeTwo` Silencioso
Silencio------------------------------------------------------------------
Silencio 2 Silencio 5 Silencio 3 Silencio Precios incomprensibles: {1,3}. Todos >3 son comprables. Silencio
Silencio 5 Silencio 7 Silencio 23 Silencio Precios incomprensibles: {1,2,3,4,6,8,9,11,13,16,18,23}. Todos >23 son comprables. Silencio

**Constraints* *

* 1 " PRIOne " , " PRITwo " , 104
* `primeOne ' y `prime Dos son primos
* `primeOne` × `primeTwo`

-...

## 🔑 Insight – Chicken McNugget Theorem

Cuando usted tiene dos enteros positivos coprime `a` y `b`, el entero más grande que no se puede expresar como
`a * x + b * y` con enteros no negativos `x, y` es

`` `
maxNoRepresentable = a * b - a - b
`` `

Ambos primos son distintos, así que son automáticamente coprime.
Por lo tanto la respuesta es simplemente

`` `
primo Uno... Dos - primo Uno - primo Dos.
`` `

No se necesitan bucles ni DP – la solución se ejecuta en **O(1)** tiempo y **O(1)** espacio.

-...

## 🧑 💻 Implementación - Tres idiomas

#### ## 1down⃣ Java

``java
- 2979. Lo más caro que no se puede comprar
Clase Solución {
public int mostExpensive Item(int primeOne, int primeTwo) {
// Teorema de pollo McNugget para primos coprime
de regreso Uno... Dos - primo Uno - primo Dos;
}
}
`` `

#### 2down⃣ Python

``python
# 2979. Lo más caro que no se puede comprar
Solución de clase:
def mostExpensive Artículo(self, primeOne: int, primeTwo: int) - int:
# O(1) formula: a*b - a - b
de regreso Uno... Dos - primo Uno - primo Dos.
`` `

#### 3down⃣ C++

``cpp
- 2979. Lo más caro que no se puede comprar
Clase Solución {
public:
int mostExpensive Item(int primeOne, int primeTwo) {
// Teorema de pollo McNugget para primos coprime
de regreso Uno... Dos - primo Uno - primo Dos;
}
};
`` `

Los tres snippets están listos para caer en el botón "Enviar" de LeetCode y pasar cada caso de prueba al instante.

-...

## 📚 Blog Article – “The Good, the Bad, and the Ugly of the Chicken McNugget Problem”

■ *Título*
■ “Cómo Crack LeetCode 2979 en 10 segundos: The Chicken McNugget Theorem Explained”

■ **Meta Descripción**:
■ “Aprenda a resolver LeetCode 2979 en el tiempo O(1) con el Teorema de Chicken McNugget. Obtenga soluciones Java, Python y C++, además de un blog detallado en las matemáticas detrás de ella. ”

■ **Keywords**:
■ LeetCode 2979, artículo más caro que no se puede comprar, teorema de pollo, problema de monedas, teoría de números, entrevista de codificación, solución Java, solución Python, solución C++, algoritmo O(1), DP vs matemáticas.

-...

#### Introduction

Cuando vi por primera vez *LeetCode 2979 – Lo más caro que no puede ser comprado*, asumí que un enfoque dinámico de programación (DP) era inevitable: “Tenemos dos denominaciones de monedas, ¿podemos calcular todas las cantidades representables? ”
Pero las limitaciones eran pequeñas (`primeOne * primeTwo ' ) y los casos de prueba eran simples.
¿El verdadero secreto? Un resultado número-teoría clásico llamado **Chicken McNugget Theorem**.

-...

### The Good – Why the Formula Works

1. *Coprime Primes* – Cualquier dos primos distintos son coprime, es decir, gcd(primeOne, primeTwo) == 1`.
Esta es la condición exacta que el teorema requiere.

2. **Largest Inttainable Sum** – El teorema nos dice el entero más grande que **no puede ser escrito como
" PRI Uno * x + primo Dos * y’ (x, y ≥ 0)
" PRI Uno... Dos – primo Uno – primo Dos.

3. **Constant‐Time Answer** – Una vez que conoces la fórmula, la respuesta es una única operación aritmética.
Es por eso que las tres soluciones funcionan en el tiempo *O(1)*.

-...

### Los malos – saltos comunes

Silencio Pitfall Silencio Por qué Sucede
Silencio...
Silencio **Off‐by‐One Errores** Silencio Olvidando que el teorema se aplica a *positivos* enteros 0. Uno... Dos - primo Uno, primo Dos.
Silencio **Overflow (Java)** Silencioso la multiplicación podría rebosar para grandes primos (pero las restricciones lo mantienen a salvo). Todavía seguro porque `prime Uno de los dos primeros fue 105. Silencio
Silencio **Misinterpreting “Distinct”** Silencio Algunas personas suponen que los primos podrían ser iguales, lo que rompería la condición coprime. El problema de la vida garantiza que son distintos. Silencio

-...

### The Ugly – When You Don't Know the Theorem

Si estás atascado y no has oído hablar del teorema, podrías:

1. **Escribe un DP** que explora todas las sumas hasta 'prime Uno.
Tiempo: `O(n2)` en el peor caso (n ~ 105) → ~109 operaciones → demasiado lento.

2. **Implement a BFS/DP with a Queue** that keep adding `primeOne ' and `prime Dos.
Todavía termina explorando ~105 estados, pero es innecesario.

3. **Enumeración de Trial y Error** hasta que note el patrón.
Esto desperdicia tiempo y conduce a soluciones que pueden fallar las pruebas ocultas.

-...

## Final Takeaway

El problema LeetCode 2979 es un ejemplo de libro de texto de cómo un poco de matemáticas puede convertir un problema DP aparentemente difícil en un solo teléfono.
Recuerda:

`` `
respuesta = primario Uno... Dos - primo Uno - primo Dos.
`` `

¡Añada esto a su kit de herramientas de entrevista, e impresionará a los entrevistadores con su codificación y los grupos matemáticos!

-...

### SEO Checklist

- **Título** > **Meta** contiene la palabra clave principal (LeetCode 2979).
- **Intro** conecta a los lectores con una historia (primer encuentro).
- **Las cuentas** (`#`, `#`, `###') rompen el contenido para la legibilidad > SEO.
- **Los bloques del código** son específicos para cada idioma y están listos para copiar.
- **Las listas de errores hacen que el artículo sea hábil.
- **Keywords** espolvoreado naturalmente.

-...

**Feliz codificación, y que su entrevista sea tan suave como esa única línea!* *