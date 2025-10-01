-...
Título: LeetCode 2110. Número de Períodos de Descendencia Smooth de una Stock -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1down⃣ Problem Overview – LeetCode 2110
**Número de periodos de descendencia de un stock* *
- Dificultad:
- **Idea clave:** Cuenta cada sub-array contiguo cuyos elementos consecutivos caen por **exactamente 1**.
- ** Entrada: ** `int[] precios` - precios de las acciones diarias (1 ≤ n ≤ 105).
- **Resultado:** 'long' - el número total de periodos de bajada suave.

■ Un período de longitud 1 es siempre válido; períodos más largos deben satisfacer
" precios [i‐1] - precios [i] == 1` para todos `i' dentro del período.

-...

## 2down Por qué este problema importa
- ** Insight Algoritmico:** Reconocimiento de un problema clásico de “run” o “segment”.
- **Entreview Context:** Aparece en LeetCode, y es un favorito de muchos equipos de contratación para la estructura de datos + pensamiento codicioso.
- Analogía del mundo real. Detectar secuencias decrecientes estrictamente en datos de series temporales (por ejemplo, caídas de stock, caídas de temperatura).

-...

## 3down La “buena” – Ventana de deslizamiento simple / Ejecución de longitud
- **O(n) tiempo, O(1) espacio extra. #
- Mantenga un contador 'len' para la carrera consecutiva "drop‐by-1".
- Cuando la carrera se rompe, añadir el número de sub-arrays contribuido por esa carrera:
\[
\text{add} = \frac{\text{len} \times (\text{len}+1)}{2}
\]
- Después del bucle, agregue la contribución de la última ejecución.

### ¿Por qué funciona esto?
Cada sub-array que se encuentra completamente dentro de una carrera de longitud `len` es un período de descenso válido.
La fórmula anterior cuenta todos **contiguos** sub-arrayos de una secuencia de longitud 'len' - exactamente lo que necesitamos.

-...

## 4down El “Bad” – Fuerza bruta O(n2)
Ábrete todos los índices de inicio, extiende hasta que la regla se rompa, y cuenta cada sub-array válido.
- Tiempo: \(O(n^2)\) – inaceptable para \(n = 10^5\).
- Espacio: \(O(1)\) - pero el costo del tiempo lo mata.

-...

## 5down Los “Ugly” – DP / Segment Trees
Algunas soluciones intentan la programación dinámica o los árboles de segmento, añadiendo complejidad innecesaria.
- **Over-engineering:** DP rastrearía la carrera más larga final en cada posición, pero la ventana deslizante ya hace esto en espacio constante.
- Oído leer: Más líneas de código, mayor probabilidad de errores.
- **Performance:** Todavía \(O(n)\) pero con factores constantes más pesados.

-...

## 6down La solución limpia (Venta deslizante)
A continuación encontrará implementaciones completamente recomendadas, de producción en **Java, Python y C+**. Todos usan la misma idea descrita anteriormente.

Silencio Idioma Silencio Función Silencioso Tipo de retorno
Silencio----------------------------------------------------------
TEN Java TENIDO `public long getDescentPeriods(int[] prices)` Silencio `long` ANTE Utiliza `long` para evitar el desbordamiento ANTE
Silencio Python Silencio `def get_descent_periods(prices: List[int]) - confiar int:` Silencio `int` Silencio La int de Python es intrínseca
TENIDO C++ TENIDO 'long getDescentPeriods(vector asignadoint tendría precios reducidos)` TEN `long' TENIDO 64‐bit firmado ANTERI

-...

### 6.1 Java

``java
importar java.util*;

Solución de la clase pública {}
*
* Cuenta períodos de descenso suaves en una variedad de precios de stock.
*
* @param precios array de precios diarios
* @retorno número de periodos de descenso suave (longo para evitar el desbordamiento)
*/
public long getDescentPeriods(int[] prices) {}
int n = prices.length;
si (n == 0) retorno 0; // defensiva (problemas garantías n ю= 1)

total largo = 0;
int runLen = 1; // longitud actual de gota por-1 consecutivo

para (int i = 1; i) {}
(precios[i) - 1] - precios [i] == 1) {
runLen++; // continuar la carrera
. ♫ ... {
total += (long) runLen * (runLen +1) / 2; // añadir contribución
runLen = 1; // resetea para la próxima carrera
}
}

// añadir la última carrera
total += (long) runLen * (runLen +1) / 2;
Total de retorno;
}

--- Opcional principal para la prueba manual rápida -----
public static void main(String[] args) {
Solución sol = nueva solución ();
System.out.println(sol.getDescentPeriods(new int[]{3, 2, 1, 4})); // 7
System.out.println(sol.getDescentPeriods(new int[]{8, 6, 7, 7})); // 4
System.out.println(sol.getDescentPeriods(new int[]{1})); // 1
}
}
`` `

-...

### 6.2 Python

``python
de la importación Lista

def get_descent_períodos(precios: List[int]) - int:
"
Cuenta los períodos de descenso suave en una lista de precios.

Parámetros
--------
precios : List[int]
Precios diarios de las acciones, 1 0 = len(precios)

Devoluciones
---
int
Número total de períodos de descenso suave.
"
n = len(precios)
si n == 0:
retorno 0

total = 0
run_len = 1 # longitud de ejecución actual

para i en rango(1, n):
si precios[i - 1] - precios [i] == 1:
run_len += 1
más:
total += run_len * (run_len +1) // 2
run_len = 1

total += run_len * (run_len +1) // 2
total

# ---- La prueba rápida opcional...
si __name_ == "__main__":
print(get_descent_períodos([3, 2, 1, 4])) # 7
print(get_descent_períodos([8, 6, 7, 7])) # 4
print(get_descent_períodos([1]) # 1
`` `

-...

### 6.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
*
* @param precios vectorial de precios de stock diario
* @retorno número de periodos de bajada suaves mientras largo
*/
long getDescentPeriods(vector efectuadoint ánimos bajos precios) {
int n = prices.size();
si (n == 0) retorno 0; // guardia de seguridad

long long total = 0;
int runLen = 1; // longitud de ejecución actual

para (int i = 1; i) {}
if (prices[i-1] - prices[i] == 1) {
++runLen; // extender la carrera
. ♫ ... {
total += 1LL * runLen * (runLen +1) / 2; // añadir contribución
runLen = 1; // comenzar nueva carrera
}
}

total += 1LL * runLen * (runLen +1) / 2; // última ejecución
Total de retorno;
}
};

// --- Opcional principal para pruebas rápidas ---
int main() {}
Sol de solución;
cout se realizó el sol.getDescentPeriods({3,2,1,4})
({8,6,7,7})
cout se realizó el sol.getDescentPeriods({1})
retorno 0;
}
`` `

-...

Artículo del Blog – “El Bien, el Mal, y el Ugly de LeetCode 2110”

### Title
**LeetCode 2110 – Número de periodos de olor de una acción: el bien, el mal de la ugly**

*SEO Etiquetas:*
■ `Número de periodos de descenso de la nieve de un stock ' , `LeetCode 2110 ' , `períodos de descenso de la nieve ' , ` algoritmo de precio real ' , `DP vs ventana deslizante ' , `Java Python C++ soluciones ' , `data‐structure interview questions`.

-...

### 7.1 Introduction

Si has estado practicando en LeetCode, te toparás con **Problema 2110 – “Número de Períodos de Descendencia de Smooth de una Stock”**. A primera vista parece un simple problema de “contras submarinos”, pero en realidad enseña un truco limpio que aparece en muchas preguntas de entrevista: *contando longitud*. En este post, diseccionaremos el problema, discutiremos las trampas comunes y presentaremos una solución limpia y lista para la producción que funciona en Java, Python y C++.

-...

### 7.2 Declaración de problemas (Restated)

■ Se le da un array `prices` de longitud *n* (1 ≤ *n* ≤ 105).
■ Un ** período de descenso del sol** es un sub-array contiguo donde el precio de cada día es **exactamente 1 menos** que el precio del día anterior.
■ Sub-arrayos de la longitud 1 siempre califican.
■ Devuelve el número total de periodos de descenso suaves.

-...

### 7.3 Ejemplo Walk-through

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
TENIDO `[3, 2, 1, 4] `` TENIDO `7` ANTE 1 día (4 de ellos) + 2 días de duración `[3,2]`, `[2,1]` + 3 días de duración `[3,2,1]` Silencio
Silencio `[8, 6, 7, 7]` Silencio `4` Silencio Sólo días porque `[8,6] falla la regla de “diferencia = 1”
Silencioso `[1] Silencioso `1`

-...

## 7.4 El Bien - Ventana Sliding / Codificación Run‐Length

La observación clave: **Si tienes una carrera contigua de longitud `L` donde cada par de elementos consecutivos difiere en 1, entonces cada sub-array dentro de esta carrera es válido**.
- Número de sub-arrays en una carrera de longitud `L` es \(\frac{L(L+1)}{2}\).
- Sólo tenemos que encontrar cada carrera máxima y añadir el resultado de la fórmula.

** Pasos del Algoritmo**

1. Inicializar `runLen = 1` y `total = 0`.
2. Tetrato del segundo elemento al final.
3. If `prices[i-1] - prices[i] == 1`, increase `runLen`.
4. Else (run broken):
- Add `runLen * (runLen +1) / 2` to `total`.
- Reiniciar `runLen = 1`.
5. Después del bucle, agregue la contribución de la última ejecución.

¿Por qué es esto? * *
Sólo escaneamos el array una vez; cada operación dentro del bucle es O(1).

¿Espacio?
Sólo algunas variables enteros – O(1).

-...

## 7.5 The Bad – Brute Force O(n2)

Un enfoque ingenuo comprueba cada sub-array posible y verifica la regla de descenso. Mientras que funciona para pequeñas entradas, rápidamente se vuelve infeasible para *n* = 105:

- **Hora:** ~5 × 109 operaciones → minutos o horas.
- **Espacio:** Todavía O(1), pero el costo de tiempo más puro lo mata.

-...

## 7.6 The Ugly – Over-engineering (DP / Segment Trees)

Algunas soluciones implementan la programación dinámica o un árbol de segmentos para hacer un seguimiento de la carrera de descenso más larga finalizada en cada índice.
- **Pros:** Aún O(n).
- **Cons:** Agrega ~20 líneas adicionales de código, dolores de cabeza más depurantes, y un factor constante más grande.
- **Resultado:** Más difícil de mantener, más difícil de leer, y no ofrece ninguna ventaja sobre la ventana deslizante.

-...

## 7.7 Final Clean Code (Java / Python / C++)

(Mostrar las implementaciones enumeradas en la sección 6 supra.)

*Consejo:* En Java y C++ utilizan enteros de 64 bits ( " largo " ) para protegerse contra el desbordamiento; los enteros de Python son una apreciación arbitraria, así que estás a salvo.

-...

## 7.7 What to Practice Next

Una vez que domina el Problema 2110, prueba estas variaciones:

- LeetCode 1576 – Encontrar Min Arrow Speed to Hit Targets** (también conteo de longitud).
- **Subsecuencia Aritmética más larga** (genera la regla “diferencia = 1”).
- **Nombra “buenas sub-arrayas” donde el producto es divisible por un número** (DP o dos puntos).

-...

### 7.8 Take-away Checklist

Silencio ↑ ✔ ✔ ❌ Silencio
Silencio...
Silencio Use un solo escaneo para detectar carreras. Mantenga `runLen` y agregue \(\frac{L(L+1)}{2}\) para cada carrera. Silencio
Retorno `long` (Java/C++) o `int` (Python). Aritmética de 64 bits para prevenir el desbordamiento. TEN sobre el motor con DP o árboles de segmentos. Silencio

-...

### 7.9 Clausura

LeetCode 2110 es un micro-lesson en *conteo eficiente*. El enfoque de la ventana corredera es elegante, rápido y fácil de implementar en cualquier idioma principal. Si te estás preparando para entrevistas técnicas, dominar este patrón te ahorrará tiempo e impresionará a los entrevistadores.

■ **¿Quieres más consejos de entrevistas?** Suscríbete a mi newsletter para pasarelas semanales de desafío de codificación en Java, Python y C++.

-...

## 7.10 Call to Action

■ ¡Prueba el código!
■ Copie la implementación para su idioma preferido, ejecute las muestras y luego pruebe los arrays aleatorios para ver la diferencia de rendimiento.
■ ¡Feliz codificación!

-...

## 8down Palabras finales

- **LeetCode 2110** es un problema clásico de recuento “de longitud”.
- La solución **sliding ventana** es la más limpia, más rápida y más sostenible.
- La ingeniería excesiva con DP o árboles es innecesaria; la fórmula de matemáticas simple ya le da la respuesta.

Si encuentra este artículo útil, compartalo en LinkedIn o Twitter y etiqueta tus compañeros de código. ¡Buena suerte en tu próxima entrevista! 🚀

-...

*Author:* [Su nombre] – Senior Software Engineer " Code Mentor.
*Contacto:* `you@example.com` en Twitter

-...

*Sea libre para ajustar el tono o la estructura del artículo para adaptarse a su marca personal. La parte más importante: las ideas algorítmicas permanecen igual. *