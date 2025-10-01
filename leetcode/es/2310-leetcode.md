-...
Título: LeetCode 2310. Suma de números con unidades Digit K -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 2310. Suma de números con unidades Digit K
**Una solución completa y lista para entrevistas en Java, Python y C++ + un blog “buen-bad-ugly”* *

■ **Keywords** – *Leetcode 2310*, *Sum of Numbers with Units Digit K*, * Solución java*, *solución pitón*, *solución C++*, entrevista de codificación*, *ingeniero de software*, *programación dinamica*, *complejidad*, *tiempo-complexidad O(1)*

-...

## 1. Declaración de problemas

■ Se les da dos enteros `num' (0 ≤ num ≤ 3000) y `k` (0 ≤ k ≤ 9).
■ Usted debe formar un conjunto de **positivos** enteros que satisfacen
* todos los números enteros terminan con el dígito `k ' (número de unidades), y
* la suma de todos los enteros equivale a `num`.
■ El conjunto puede contener números duplicados.
■ Devuelve el tamaño mínimo posible** de tal conjunto.
■ Si no existe tal conjunto, devuelve `-1`.
■ Un conjunto vacío sólo se permite cuando `num == 0` (su suma es 0).

-...

## 2. Por qué este problema es entrevista-Amén

Por qué importa
Silencio...
Silencio **Simple Math + Observation** Silencio Permite probar el razonamiento sin estructuras de datos pesadas. Silencio
Silencio **Fixed Bound (10)** Silencio Aprendes a explotar la periodicidad digital para podar la búsqueda. Silencio
Silencio **Edge‐Case Heavy** tención Entrena la programación defensiva (`k==0`, `num=0`, etc.). Silencio
Silencio **Multiple Idiomas** Silencio Showcases que puedes traducir lógica entre Java, Python, C++. Silencio

-...

## 3. High-Level Insight

Para cualquier entero que termine con el dígito `k`, se puede escribir como `10 × x + k`.
Si escogemos `i` tales enteros, su suma es 'i × k + 10 × S` para algunos enteros `S`.
Lo único que importa es el **número de unidades** de la suma: debe coincidir con el `número 10`.
Por lo tanto, sólo necesitamos comprobar por el más pequeño `i' tal que

`` `
i * k ≤ num (no podemos exceder la suma de destino)
i * k % 10 == num % 10 (units digit match)
`` `

Debido a que el dígito de unidades de 'i × k` repite cada 10 valores de 'i', nunca necesitamos
check beyond `i = 10`.
Así que todo el problema se reduce a un bucle de tiempo constante de la mayoría de 10 iteraciones.

-...

## 4. Prueba de corrección

1. **Si `num == 0`** - el conjunto vacío satisface todas las condiciones; el tamaño 0 es mínimo.
2. **Si existe una solución** con el tamaño `i`, entonces obviamente `i × k ≤ num` y los dígitos de las unidades coinciden, por lo que nuestro bucle lo encontrará (o un anterior 'i' que también funciona, dando el verdadero mínimo).
3. **Si no `i` ≤ 10 satisfies ambas condiciones**, entonces no `i` ≥ 11 puede tampoco, porque el patrón de dígitos de unidades repite cada 10 pasos. Así la respuesta es `-1`.

Por lo tanto el algoritmo devuelve el tamaño mínimo cuando existe, de lo contrario `-1`.

-...

## 5. Análisis de la complejidad

TEN TERMIN TEN ANTE SON TEN ANTE
Silencio...
Silencio ** Tiempo** Silencioso `O(1)` – a la mayoría de 10 iteraciones. Silencio
Silencio** – sólo algunas variables enteros. Silencio

-...

## 6. Casos de borde

TENIDO Scenario ANTERIOR Lo que sucede
Silencio------------
TENIDA `num == 0` Silencio devuelve `0`. Silencio
TENIDA `k == Sólo múltiples de 10 son alcanzables. El bucle todavía funciona; devuelve `1` si `num % 10 == 0`, de lo contrario `-1`. Silencio
TENIDO `num ANTERIENTE ANTERIOR La condición del lazo `i * k ANTE = num` falla inmediatamente; respuesta `-1`. Silencio
No se permite por limitaciones. Silencio
TENIDA `k == 5` y `num == 5` ANTERIOR Funciona; devuelve `1`. Silencio
TENIDO `k == 3`, `num == No hay solución → `-1`. Silencio

-...

## 7. Código (Java, Python, C++)

## Java

``java
Clase Solución {
public int minimumNumbers(int num, int k) {
(num == 0) retorno 0; // Conjunto de vacío
para (int i = 1; i * k <= num ' ю = 10; i+) {
(k * i) % 10 == num % 10) {
regreso i; // Más pequeño que funciona
}
}
retorno -1; // No existe un conjunto válido
}
}
`` `

## Python

``python
Solución de clase:
def minimumNumbers(self, num: int, k: int) int:
si num == 0:
retorno 0
para mí en el rango(1, 11): # 1..10
si k * i % 10 == num % 10 y i * k <= num:
Regreso
retorno -1
`` `

### C++

``cpp
Clase Solución {
public:
int minimumNumbers(int num, int k) {}
(num == 0) retorno 0;
para (int i = 1; i * k <= num " ю = 10; ++i) {}
si (k * i) % 10 == num % 10) devuelve i;
}
retorno -1;
}
};
`` `

-...

## 8. “El Bien, el Mal, el Mal”

Silencio Silencio
Silencio------------Prince------
tención ** Simplicidad Algorítmica** ← O(1) loop, no DP, no estructuras de datos TENIDO Podría parecer trivial, pero faltando la experiencia del dígito sutil puede llevar a una solución O(num)
Silencio **Edge‐Case Coverage** ← Handles `num == 0`, `k == 0`, y todos los desajustes de dígitos ¦ Common pitfall: assumed `k == 0` siempre funciona cuando `num % 10 == 0` Silencio No comprobando `i * k <= num` puede producir respuestas incorrectas (sobre-suming) Silencio
Silencio **Readability** Silencio Nombres variables claros (`i`, `k`, `num`) y comentarios Silencio Sobre-commenting puede desordenar el código Silencio Escribir una sola línea `if (k*i%10===num%10 " Pulse i*k =num) devolver i;` parece inteligente pero oculta la intención
TEN **Language-specific quirks** TENCIÓN La integer overflow de Java es imposible aquí TEN Python 'range(1, 11)` es inclusiva de 10 TEN C++ falta de cheque por `num==0` se puede perder si copy‐pasted TEN

-...

## 9. Consejos de entrevista

1. **Explicar la periodicidad** – decir por qué 10 es suficiente.
2. ** Casos de borde de discusión primero** – `num == 0`, `k == 0`.
3. **Tiempo/espacio de la mención** explícitamente – entrevistador ama las reclamaciones O(1).
4. **Mostrar alternativa** – un DP rápido o un enfoque codicioso (sólo para mostrar profundidad).
5. **Hablar sobre pruebas** – dar ejemplos de `num=58,k=9`, `num=37,k=2`, `num=0,k=7`.

-...

## 10. Conclusión

Este problema de Leetcode demuestra cómo una pregunta de “sumo” aparentemente abierta puede resolverse en tiempo constante explotando la naturaleza periódica de los dígitos de unidades decimales.
La llave despega: **siempre buscan patrones ocultos** que pueden encoger un espacio de búsqueda potencialmente grande a un pequeño bucle fijo.
Dominar este truco no sólo le da una solución correcta, sino que también muestra a los entrevistadores que usted puede detectar atajos elegantes, un rasgo de todos los covets ingeniero senior.

¡Feliz codificación, y que su próxima entrevista sea tan suave como este bucle de 10 letras!