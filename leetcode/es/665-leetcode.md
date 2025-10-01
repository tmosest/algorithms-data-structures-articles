-...
Título: LeetCode 665. Array no disminuyente -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🧩 665 – Non‐Decreasing Array
■ **Dificultad:**
■ **Signature:** `public boolean checkPossibility(int[] nums)`.

-...

## Problema Recap
Se le da un array entero `nums`. Puede cambiar **en la mayoría de un elemento** a cualquier valor que desee. Después del cambio, el array debe convertirse en **no-disminución** (`nums[i] ≤ nums[i+1]` para todo válido `i`).

Regresar `verdad' si es posible, de lo contrario `false`.

*Examples*

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
Silencio `[4,2,3]` Silencio `verdad '  `4` → `1`. Silencio
Silencio `[4,2,1]` Silencio `false` Silencio Ningún cambio único puede fijar ambas disminuciones. Silencio

**Constraints* *

Нены не не не ≤ ≤ 104 у
Silencioso nums[i] Silencio –105 ≤ nums[i] ≤ 105 Silencio

-...

## 🚀 Solution Overview

El array es **sólo "casi" ordenados** – en la mayoría de una violación `nums[i] se permite nums[i‐1]`.
El crux es decidir *cómo* arreglar una violación:

* **Option 1** – Bajo `nums[i-1]` a `nums[i]`.
* **Option 2** – Levantar `nums[i]` a `nums[i‐1]`.

Ambos pueden ser válidos dependiendo de los números circundantes (`nums[i‐2]` y `nums[i+1]`).
Si usted golpeó una segunda violación o una situación en la que *neither* opción mantiene la secuencia ordenada, la respuesta es `false`.

El algoritmo es un solo escaneo lineal, tiempo O(n) y espacio O(1).

-...

## 📝 Pseudocode

`` `
para mí de 1 a 1
si nums[i] encontrado una disminución
si ya vimos una disminución
devolver falso
si yo contamos1 y yo hicimos-1 y nums[i-2] ⇩ nums[i] y nums[i+1]
volver falso // ambos lados todavía estaría equivocado
marca que vimos una disminución
retorno verdadero
`` `

La condición `nums[i-2] > nums[i] ` significa que tendríamos que *raise* `nums[i]` para mantener el lado izquierdo ordenados, mientras que `nums[i+1] cautivos nums[i-1]` significa que tendríamos que *lower* `nums[i-1]` para mantener el lado derecho resuelto.
Si ambos son verdaderos, ninguna elección funciona → imposible.

-...

## 📄 Code

## Java

``java
Clase Solución {
public boolean checkPossibility(int[] nums) {
para (int i = 1, err = 0; i) i++) {
si (nums[i]
// Segunda violación
si (err++ 0) devolver falso;
// YABY situación – no puede arreglar
si (i √≥ 1 " círculo i " )
nums[i - 2] " nums[i + 1]
devolver falso;
}
}
}
retorno verdadero;
}
}
`` `

## Python 3

``python
Solución de clase:
def checkPossibility(self, nums: list[int] Bool:
err = 0
para i en rango(1, len(nums)):
si nums[i] [i - 1]:
si erres o (i √≥ 1 y i)
nums[i - 2] y nums[i + 1]
Retorno Falso
err = 1
Retorno
`` `

### C++ (C+17)

``cpp
Clase Solución {
public:
bool checkPossibility(vector fielint limitada nums) {
para (int i = 1, err = 0; i) ++i) {
si (nums[i]
si (err++ prehensivo sobre la vida eterna (i > 1 " sensible i " )
nums[i - 2] " nums[i + 1]
devolver falso;
}
}
retorno verdadero;
}
};
`` `

Las tres implementaciones se ejecutan en **O(n)** tiempo, **O(1)** espacio auxiliar, y coinciden con la estrategia avaricia descrita anteriormente.

-...

## 📚 Blog Post: "El Bien, el Mal, y el Ugly de LeetCode 665"

## Título (SEO‐Optimized)
**Cómo Crack LeetCode 665 – No Disminuir Array: El Bien, El Mal, El Ugly (Java, Python, C++)* *

## Meta Descripción
Maestro LeetCode 665 en minutos! Aprenda la solución codictiva intuitiva, trampas para evitar, y Java completo, Python, C++ código. Boost your coding interview prep and land your dream tech job.

-...

#### Introduction
* Los problemas de LeetCode “casi ordenados” son un lugar dulce para los entrevistadores.
* Problema 665 pregunta: **¿Puede un solo elemento fijar un array casi surtido? * *
* Caminaremos a través del razonamiento, las trampas del borde y una solución de producción en Java, Python y C++.

■ *Keywords:* LeetCode 665, No Disminuir Array, codificación de entrevistas, problema algorítmico, solución codictiva, codificación Java, codificación Python, codificación C++, instrucciones de datos, preparación de entrevistas.

-...

## The Good

Silencio ¿Por qué ayuda a vivir?
Silencio--------------------
Silencio **Clear Input Constraints** Silencio Fácil de razonar sobre el tiempo y los límites del espacio. Silencio
Silencio **Single Pass Greedy** Silencio Una entrevista clásica favorita – muestra que puedes pensar en el tiempo O(n). Silencio
Silencio **Elegant Edge‐Case Check** ← The `nums[i-2] ⇩ nums[i] " nums[i+1] " se entiende nums[i-1] " condition is a one-liner that captures all failure modes. Silencio
tención **Language‐agnostic** ← La misma lógica en Java, Python y C++; muestra la versatilidad del lenguaje. Silencio

#### Takeaway
Una solución limpia, O(n) codicioso es a menudo el *más fácil de entrevista* porque demuestra:

* Pensamiento eficiente
* Atención al detalle con casos de borde
* Capacidad para escribir código conciso, sin errores

-...

## The Bad

← Cómo arreglarlo
Silencio...
Silencio **Misreading “modify at most one element”** Silencio No es “swap two elements”; puedes cambiar a cualquier valor. Olvidar esto conduce a soluciones erróneas que intentan *swap* en lugar de *set*. Silencio
Silencio **Over-optimistic “fix left or right”** Silencio Simplemente bajando `nums[i-1] o levantar `nums[i]` todavía puede romper el siguiente par. Siempre comprueba `nums[i-2]` y `nums[i+1]`. Silencio
Silencio **Counting violations incorrectly** Silencio Algunos novatos usan incorrectamente `i+` y terminan perdiendo la segunda violación. Silencio
Silencio ** Modificaciones complejas “en lugar”** tención Cambiar el array mientras iterating puede ocultar la lógica. Preferir un valor prev *virtual* o simplemente mantener un contador. Silencio

** Ejemplo de cascada común**

``python
# Enfoque equivocado: siempre se establecen nums[i-1] = nums[i]
para i en rango(1, len(nums)):
si nums[i] [i-1]:
nums[i-1] = nums[i]
Retorno
`` `

This fails on `[3,4,2,3]`. El lado izquierdo se convierte en `[3,4,2]`. → todavía disminuyendo.

-...

## The Ugly

1. **Misinterpreting “non-decreasing” vs “strictly increasing”* *
*No disminuir* permite la igualdad (`≤`). Un error sutil: el uso de `` `` en todas partes rechazará incorrectamente arrays como `[1,1,1]`.

2. **Tiempo de salida en grandes entradas**
Si escribes un bucle anidado O(n2) (por ejemplo, probando todas las ediciones individuales posibles), la solución alcanzará el límite de 2 s de LeetCode en los arrays 104‐element.

3. ** Uso innecesario del espacio**
Crear una copia de la matriz para cada intento de edición duplica el uso de memoria y disminuye debido a faltas de caché.

4. **Leer la “respuesta” equivocada de la comunidad* *
Muchos artículos del blog dicen “cambiar “nums[i]” a “nums[i-1]” ciegamente. Eso es correcto cuando `nums[i-2] ≤ nums[i]`.
La situación “YABY” es la *real* fea – ambos lados aún se rompen si eliges el lado equivocado.

-...

## 🎯 Interview Tips

Silencioso Por qué importa
Silencio...
Silencio **Empieza con una definición clara de “violación”.** Silencio Previene confusión sobre `nums[i] > nums[i-1] ' . Silencio
Silencio **Use un solo contador ( " modificado " / `err " ). Silencio
Silencio **Piensa en los vecinos (`i-2`, `i+1`).** Silencio La decisión fija se centra en estos dos elementos. Silencio
Silencio **Primeros casos de filo.** Silencioso ``, `[1,1]`, `[2,1]`, `[3,2,1]` son cheques de cordura rápidos. Silencio
Silencio **Explica tu lógica en inglés claro antes de codificación.** Silencio Entrevistadores aprecian procesos de pensamiento claros. Silencio
Silencio **Práctica la versión “sin modificar la matriz”. ** Silencio Shows puedes mantener intacta la matriz – un sutil amor de los entrevistadores de habilidad. Silencio

-...

## ❌ Resumen

LeetCode 665 es un problema codicioso clásico que recompensa:

* **Linear‐time thinking* *
* **Meticulous edge-case handling* *
* **Cross‐language clarity* *

La solución avaricia anterior es el código de producción, que funciona en Java, Python y C++. Entréguelo, agréguelo a su cartera, y estará listo para llegar a cualquier pregunta de entrevista de “array‐smoothing”!

-...

¡Feliz codificación!
*Tenga la libertad de dejar sus propias tomas en los comentarios, o hágame saber si le gustaría una inmersión más profunda en las variantes de programación dinámica. *