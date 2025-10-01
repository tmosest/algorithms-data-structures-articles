-...
Título: LeetCode 309. El mejor momento para comprar y vender Stock con Cooldown -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 309. Mejor tiempo para comprar y vender Stock con refrigeración
**Dificultad:**
**Tag:** DP, State Machine, Greedy, O(1) Space

-...

#### TL;DR
* Use un **state‐machine DP** que guarde sólo tres variables: `hold`, `sold`, and `rest`.
* Transición en *O(1)* por día → **O(n)** tiempo, **O(1)** espacio.
* La recurrencia central:

Silencioso Estado
Silencio--------------------
Silencio `hold` Silencio Mantener una acción hoy Silencioso `hold = max(hold, rest - price)` Silencio
Silencio `sold` Silencio Completo un stock hoy Silencio `sold = max(soldado, hold + price)` Silencio
Silencio `resto` Silencio En enfriamiento o no hacer nada Silencio

-...

## 1. El Código

A continuación se presentan implementaciones limpias y de producción en **Java**, **Python**, y **C+**.

-...

#### 1.1 Java

``java
Solución de la clase pública {}
public int maxProfit(int[] prices) {
int hold = Integer.MIN_VALUE; // máx beneficio al sostener un stock
int sold = 0; // ganancia máxima cuando la última acción estaba vendiendo
int rest = 0; // ganancia máxima cuando enfriamiento / ocio

por (un precio : precios) {
int prevHold = hold;
int prevSold = vendido;

sujetar = Math.max(prevHold, descanso - precio); // comprar hoy o mantener la retención
vendido = Math.max(prevSold, prevHold + precio); // vender hoy o mantener vendido
reposo = Math.max(rest, prevSold); // refrigeración o permanecer ocioso
}
retorno vendido; // la última acción debe ser una venta para realizar ganancias
}
}
`` `

-...

### 1.2 Python

``python
Solución de clase:
def maxProfit(self, prices: List[int] int:
sujetar = flotar('-inf')
vendidos
resto = 0 # refrigeración / ocioso

por precio en precios:
prev_hold, prev_sold = hold, sold
hold = max(prev_hold, restar - precio) # comprar o mantener la retención
vendido = max(prev_sold, prev_hold + precio) # vender o mantener vendido
reposo = max(rest, prev_sold) # refrigeración o ocio

Devolución vendida
`` `

-...

#### 1.3 C++

``cpp
Clase Solución {
public:
int maxProfit(vector asignadoint propietarios precios) {}
int hold = INT_MIN; // holding a stock
int sold = 0; // just sold
int rest = 0; // refrigeración / ocio

por (un precio : precios) {
int prevHold = hold, prevSold = sold;
sujetar = max(prevHold, descanso - precio); // comprar o mantener la retención
vendido = max(prevSold, prevHold + precio); // vender o mantener vendido
reposo = max(rest, prevSold); // refrigeración o ocio
}
retorno vendido; / / / mejor beneficio termina con una venta
}
};
`` `

Las tres implementaciones se ejecutan en **O(n)** tiempo y utilizan sólo **O(1)** memoria adicional – perfecta para entrevista y producción.

-...

## 2. El artículo del Blog

■ **Título:** *“Mastering LeetCode 309: Best Time to Buy and Sell Stock with Cooldown – The Good, The Bad, and The Ugly”*
■ **Meta Descripción:**
■ Aprende cómo romper LeetCode 309 en minutos. Sumérgete en la solución DP state‐machine, trampas y por qué O(1) espacio importa para entrevistas.

-...

#### 2.1 Introduction

Si has golpeado a LeetCode 309 “El mejor momento para comprar y vender stock con refrigeración”, felicitaciones!
Es un problema clásico de DP que aparece en los oleoductos de entrevistas del mundo real: ** transacciones múltiples con una refrigeración de un día**.

Este artículo descompone la solución en tres partes: el *bueno* (la idea DP limpia), el *bad* (común error y por qué fallan), y el *ugly* (tricks to make the code even shorter without losing readability).
También espolvorearemos en algunas palabras claves de **SEO** – *LeetCode, DP, trading de acciones, preguntas de entrevista, búsqueda de empleo* – por lo que el post se clasifica bien para los reclutadores que buscan candidatos que puedan resolver problemas complejos de programación dinámica.

-...

### 2.2 The Good – State‐Machine DP in O(1) Space

##### 2.2.1 Intuición

Piensa en cada día como una **máquina** que puede estar en uno de los tres estados:

1. **Hold** – tienes una acción.
2. **Sold** – acabas de vender el stock.
3. **Más** – o estás en enfriamiento (el día después de una venta) o no estás haciendo nada.

No necesitamos recordar *exactamente* cuando ocurrió la última compra; sólo necesitamos el mejor beneficio posible para cada estado hasta hoy.

##### 2.2.2 Recurrencia

Transition tóxico Fórmula Silencio
Silencio...
TENIDO `hold` → `hold` ANTE Mantener la tenencia: `hold` se mantiene igual. Silencio
Silencio `hold` → `sold` Silencio Vender hoy: `sold = hold + price`. Silencio
Silencioso `resto` → `hold` Silencio Comprar hoy: `hold = descanso - precio`. Silencio
Silencioso `vendido` → `resto`  durable Cooldown: `resto = vendido`. Silencio
Silencioso `resto` → `resto` Silencio No hagas nada: `resto` permanece igual. Silencio

Combinar la opción “no hacer nada” nos da el **max** en cada asignación:

``text
sujetar = max(hold, restar - precio)
vendido = max(soldado, hold + precio)
descanso = max(resto, vendido)
`` `

Debido a que cada variable sólo depende de su valor anterior (o el *rest* anterior), podemos iterar a través del array una vez y mantener sólo tres variables enteros – **constant extra espacio**.

-...

#### 2.2.2 Code‐Ready Implementation

Ya hemos mostrado Java, Python y C++ arriba.
Un patrón clave: **actualizar usando valores anteriores** (prevHold`, `prevSold`) para evitar la sobreescritura antes de que se computa el siguiente estado.

-...

### 2.3 The Bad – Pitfalls That Trip You Up

1. **Cerrar todo el array DP (`O(n)` memoria)** –
*Muchos candidatos comienzan con un clásico 'dp[i]` array. Funciona pero desperdicia la memoria y es a menudo marcado por los entrevistadores como “ineficiente”. *

2. ** Valores iniciales equivocados** –
Establecer `hold = 0` (en lugar de `-∞`) permite incorrectamente "comprar" el día 0 sin una venta, lo que lleva a ganancias negativas que se consideran válidas.

3. *Forgetting the cooldown* –
Algunas soluciones tratan de saltar el estado de `resto' y simplemente establecer `hold = max(hold, prices[i-2] - price)`.
Esto olvida que después de vender debe **idle** por un día, por lo que la transición debe involucrar al estado *vendido* explícitamente.

4. *Usando un bucle doble*
Una solución naïve `O(n^2)` que escanea todos los días de compra anteriores para cada día de venta pasa las pruebas pero se marca "TLE" en las grandes entradas de LeetCode.

**Fixes:**
* Siempre inicializar " mantener " con " líquido " (o "INT_MIN " ) para indicar " sin existencias todavía " .
* Mantenga la variable `rest`, incluso si nunca “hacer nada” el día 0 – mantiene la recurrencia limpia.
* Evite un bucle anidado; utilice el truco de "maxDiff" que se describe en la sección *ugly*.

-...

### 2.4 The Ugly – Shortening the Code (While Staying Readable)

← Technique Silencio Cómo Ayuda a Silencio Ejemplo Silencio
Silencio------------------------------
Silencio **Ternary update** Silencio Combinar las llamadas `max` en una línea Silencioso `hold = Math.max(hold, restar - precio);`
Silencio **Pre-compute `rest`** Silencio `rest` es siempre el mejor de sí mismo y `sold` → no separado var  durable `rest = Math.max(rest, sold);` Silencio
Silencioso **Las constantes en línea** vivieron ``` via `Integer.MIN_VALUE` or `float('-inf')` TENIDO `int hold = Integer.MIN_VALUE;`

■ **Tip for Java:**
■ Utilizar `Math.max` es preferible a ``?: porque es *tipo seguro* y autodocumentación.

-...

### 2,5 Putting It All Together – A Final Checklist

Silencio Chequeo confidencialidad ¿Por qué?
Silencio...
Silencio ** Tiempo** – `O(n)` El límite de tiempo de LeetCode es generalmente de 1 a 2 segundos. Silencio
Silencio **Espacio** – `O(1)` Silencio Programador de amor candidatos que pueden escribir código de memoria-eficiente. Silencio
Silencio **Readability** – Mantener nombres variables descriptivos (`hold`, `sold`, `rest`). tención Evite los rechazos de revisión de código. Silencio
Silencio **Edge Cases** – Empty array → return `0`. ← Handles 1-day inputs Gracefully. Silencio
Silencio **Testing** – Escribe pruebas unitarias para: matriz de 1 día, precios decrecientes, precios crecientes, mezclas aleatorias. Muestra que no puedes simplemente “escuchar” la solución. Silencio

-...

### 2.6 Cierre - Cómo esto ayuda a su búsqueda de empleo

* **Muestra en Resume** – Agregue una bala: “Solved LeetCode 309 en O(n) tiempo " O(1) espacio usando DP state-machine. ”
* **LinkedIn Post** – Compartir la solución corta snippet y los reclutadores de etiquetas.
* **Interview Prep** – Practica este patrón en otros problemas de stock de LeetCode (por ejemplo, 123, 188) – el marco *state‐machine* DP es reutilizable.

Al dominar LeetCode 309, usted demuestra:

1. **Apoyo de los fundamentos de DP** – esenciales para los roles en la ingeniería de algoritmos, fintech y equipos de productos basados en datos.
2. **Space‐time trade‐off awareness** – Los reclutadores valoran a los candidatos que pueden producir código limpio y eficiente.
3. **Mente de solución de problemas** – se puede abordar escenarios del mundo real como la programación comercial o la asignación de recursos.

-...

### 2.7 SEO‐ Palabras clave amigables " Tags

Palabras claves primarias para la vida Silencio
Silencio...
Silencio LeetCode 309 Silencioso programa dinámico Silencio
← Mejor tiempo para comprar y vender Stock Silencioso problema Silencioso
Silencio DP stock trading Silencioso entrevista preguntas
Silencioso búsqueda de empleo Silencioso coding entrevista
Silencio O(1) espacio Silencioso algoritmo entrevista

-...

### 2.8 Call to Action

■ **Listo para aterrizar su próximo papel? #
■ Añade esta solución a tu cartera, publica el código en GitHub y comparte tus propias variaciones en los comentarios.
■ Programme on Linked En el amor viendo código DP limpio junto con explicaciones reflexivas – asegúrese de que sus publicaciones están indexadas con las palabras clave correctas.

-...

### 2.9 FAQ

1. ¿Podemos ignorar la frialdad? * *
Eliminar la refrigeración convierte el problema en LeetCode 122 (mejor tiempo para comprar y vender una vez). La máquina del estado todavía funciona; simplemente establece `rest = hold` en lugar de `max(rest, sold)`.

2. **¿Y si queremos limitar el número de transacciones? * *
Agregue otra dimensión al estado: 'k' (transacciones izquierda). La recurrencia sigue siendo la misma, pero necesitarás una variedad de tamaño 'k'.

3. **¿Por qué no usar una solución codictiva? #
Greedy trabaja para la sencilla versión “no refrigeración” pero falla cuando una refrigeración te obliga a saltarte un día. El DP es la única manera de captar esa dependencia.

-...

### 2.10 Pensamientos Finales

*El Bien* Un DP conciso, O(1) que modela elegantemente los estados de “tenimiento / vendido / descanso”.
*The Bad:* Los bucles anidados, los valores iniciales incorrectos y el olvido de la refrigeración.
*The Ugly:* Ligeramente menos legible uno-liners que sacrifican claridad por brevedad.

Con este conocimiento, no sólo estás listo para as LeetCode 309, pero también estás demostrando el tipo de madurez algorítmica que los empleadores buscan en ingenieros de software y científicos de datos.

Buena suerte, y que su entrevista apile desbordamiento con “Sí, lo resolví!”

-...

### 2.11 Referencias

1. LeetCode 309 – El mejor momento para comprar y vender Stock con refrigeración
2. * Programación Dinámica – Máquina Estatal* – https://www.geeksforgeeks.org/dynamic-programming-state-machine/
3. *Entrevista Prep: LeetCode 309* – https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/

-...

**© 2024 Su nombre – Todos los derechos reservados. #

-...

### 2.12 Quick Checklist for Interviewers

* ¿El candidato explica claramente los 3 estados?
* ¿Pueden derivar la recurrencia de la declaración del problema?
* ¿Escriben el código con el espacio `O(1)`, y pueden justificar la elección?
* ¿Pueden identificar trampas comunes (como olvidar la refrigeración)?

Si responde **yes** a todo lo anterior, está listo para impresionar a cualquier gerente de contratación. ¡Feliz codificación!