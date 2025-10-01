-...
Título: LeetCode 45. Juego de salto II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🚀 Jump Game II – The “Go‐Fast” Greedy Solution (Java fort Python ← C++)
*LeetCode #45 – Medium*

■ “No puedo terminar la entrevista? ¡Empieza con la idea codicioso que garantiza los saltos más bajos! ”

A continuación encontrará tres soluciones pulidas y preparadas para la producción – Java, Python y C++ – que comparten la misma lógica avaricia de corte limpio.
También voy a dejar un breve **blog post** (SEO-friendly, trabajo-hunting-oriented) que usted puede copiar‐paste en Medium, Dev.to, o su propio blog.

-...

## 1. Recaptación de problemas

Se le da un array `nums` donde cada elemento `nums[i]` es el número máximo de pasos que puede saltar * hacia adelante* desde el índice `i`.
Inicio del índice `0`. Encuentra el *mínimo* número de saltos requeridos para alcanzar el último índice (`n‐1`).
La entrada garantiza que siempre es posible.

`` `
nums = [2,3,1,1,4] → respuesta = 2
^ ^ ^ ^
0 1 2 3 4
`` `

-...

## 2. Greedy Insight – “Near & Far”

La observación clave:
**Mientras estás escaneando índices que puedes alcanzar en saltos *k*, solo necesitas saber el índice más lejano que puedes alcanzar en saltos *k+1*. #

Usted no tiene que explorar cada posible salto por separado – sólo mantener el *cante corriente* (`far`) y el *proximo alcance* (`fartest`).

■ **Near** – el comienzo de la ventana actual de índices que estás considerando.
■ El final de la ventana.
■ **Farthest** – el índice más lejano puede llegar a cualquier lugar en `[cerca, lejos]`.

Cada vez que “commites” un salto, cambias la ventana a “[far+1, más lejos]”.

-...

## 3. Código - 3 idiomas

### 3.1 Java (Java 17+)

``java
// --------------- JumpGameII.java - Sí.
importar java.util*;

clase pública JumpGameII
public static int jump(int[] nums) {
int n = nums.length;
si (n י=1) retorno 0; // ya al final

saltos int = 0;
int near = 0; // start of current window
int far = 0; // extremo de la ventana actual
int farthest = 0; // farthest

(de lejos)
// Escanear todos los índices que podemos alcanzar con el número actual de saltos
para (int i = cerca; i) = lejos; i++) {}
más lejos = Math.max(más, i + nums[i]);
}

// Prepárate para el próximo salto
cerca = lejos + 1;
lejos = más lejos;
saltos++;
}

saltos de retorno;
}

// - Sí.
public static void main(String[] args) {
int[] nums = {2, 3, 1, 4};
System.out.println("Minimum saltos: " + salto(nums)); // → 2
}
}
`` `

■ **La complejidad** – O(n) tiempo, O(1) espacio extra.

-...

#### 3.2 Python 3

``python
------------- salto_game_ii.py - Sí.
def salto(nums):
n = len(nums)
si no
retorno 0

saltos, cerca, lejos, más lejos = 0, 0, 0, 0

mientras que lejos
para i en rango(cerca, lejos + 1):
más lejos = máx(más lejos, i + nums[i])

cerca = lejos + 1
lejos = más lejos
saltos += 1

saltos de retorno

# - Sí.
si __name_ == "__main__":
nums = [2, 3, 1, 4]
print(f"Minimum saltos: {jump(nums)}") # → 2
`` `

■ **La complejidad** – O(n) tiempo, O(1) espacio extra.

-...

### 3.3 C++ (C+17)

``cpp
// --------------- JumpGameII.cpp - Sí.
#include יbits/stdc++.h
usando std namespace;

int salto(cont vector consignaint círculo nums) {
int n = nums.size();
si (n 0 = 1) retorno 0;

saltos int = 0;
int near = 0, far = 0, farthest = 0;

(de lejos)
para (int i = cerca; i) = lejos; ++i) {}
más lejos = máx(más lejos, i + nums[i]);
}
cerca = lejos + 1;
lejos = más lejos;
++créditos;
}
saltos de retorno;
}

// - Sí.
int main() {}
vector implicado nums = {2, 3, 1, 4};
cout se llevó a cabo "Minimum saltos: " se realizó el salto(nums) se hizo '\n'; // → 2
retorno 0;
}
`` `

■ **La complejidad** – O(n) tiempo, espacio O(1).

-...

## 4. Blog Post – “El Bien, el Mal y el Ugly of Jump Game II”

■ **Target audience**: Front-end / desarrolladores de personal completo que quieren ace entrevistas técnicas.
■ **Palabras clave de SEO**: Jump Game II, LeetCode 45, entrevista problema de codificación, algoritmo codicioso, soluciones de entrevista de codificación, Java, Python, C++.

-...

### Title
**Juego del juego II – El bien, el mal y el ugly: una guía de 5 minutos para el dominio LeetCode 45**

-...

## Meta Descripción
■ Crack LeetCode 45 minutos! Descubre la avaricia estrategia “Near & Far”, compara las soluciones Java/Python/C++ y aprende por qué este problema es imprescindible para tu próxima entrevista de codificación.

-...

### 1. TL;DR
Juego de salto II es un clásico rompecabezas de entrevistas que se reduce a un algoritmo codicioso de pasar * single*.
- **Bien**: O(n) time, O(1) space – perfecto para entrevistas.
- **Bad**: Pobre DP o fuerza bruta intenta perder tiempo y apilar profundidad.
- **Ugly**: Los controles de límites excesivos o incorrectos pueden provocar errores fuera de lugar por uno.

Coge los fragmentos de código a continuación, elija su idioma, y está listo para la entrevista.

-...

### 2. ¿Por qué es tan popular este problema?

- Fácil de decir, difícil de pensar demasiado - una declaración de problema limpio con trampas ocultas.
- **Tema común de entrevista** – muchas empresas piden una variante en entrevistas in situ.
- **Illustrates codiciay vs. DP** – un gran momento de enseñanza para los entrevistadores.

-...

### 3. La “buena” – La solución de salud

El ambicioso enfoque “Tierra” funciona porque:
1. Cualquier índice que se puede alcanzar en los saltos *k* sólo puede mejorar el alcance más lejano para los saltos *k+1*.
2. Nunca es necesario revisitar una ventana anterior – una vez que usted comete un salto, ya ha considerado todas las posibilidades dentro de esa ventana.

*Paso por paso*
Silencio Variable Silencio Significado Silencioso Actualización Regla
Silencio----------------------------------
Silencio `cerca' Silencioso Inicio de la ventana actual
TENIDO `far` TENIDO FIN DE LA ventana actual
Silencio `farthest` Silencio Índice máximo accesible desde la ventana actual ← `farthest = max(farthest, i + nums[i])` Silencio
Silencioso `saltos ' Silencio Número de saltos hechos ¦

■ **Hora**: O(n) – inspeccionamos cada índice al máximo una vez.
■ **Espacio**: O(1) – sólo un puñado de contadores enteros.

-...

### 4. El “Bad” – Lo que debe evitar

Por qué es malo
Silencio.
Silencio **Brute‐Force DFS** Silencio Recusarse en cada posible salto → O(2n) tiempo, apilar el riesgo de desbordamiento. Silencio
Silencio ** Programación Dinámica** (abajo) Silencio Obras, pero O(n2) tiempo y O(n) espacio – no un lugar dulce para los entrevistadores. Silencio
Silencio **Bounds Integer sin límites** TENIDO Utilizando `Integer.MAX_VALUE`/`INT_MAX` y luego añadiendo índices puede desbordarse. Use un centinela como `más lejos = 0` y computar sólo cuando sea necesario. Silencio

-...

### 5. El “Ugly” – Casos de borde y errores comunes

Silencio Pitfall Silencio
Silencio...
Silencio **`mientras (a lo lejos) no 1)` vs. `mientras (a lo más lejos se hizo n-1)`** Silencio El bucle debe parar * después* usted compromete un salto que garantiza que está en o más allá del último índice. Silencio
Silencio **Off‐by-one en el bucle interior** (`for (int i = near; i י= far; ++i)`) Silencio Asegúrate de que `far` es inclusivo; la ventana es `[cerca, lejos]`. Silencio
Silencio **Large values of `nums[i]** Silencio No desborde en Java/C++ porque `i + nums[i]` se ajusta en `int` para las restricciones LeetCode. Silencio
Silencio **El rayo de longitud 1** Silencio Regresar `0` inmediatamente – ya estás en el blanco. Silencio

-...

### 6. Los 3 idiomas – Java, Python, C++

*(Insert code snippets from Section 3.1‐3.3 here. Use bloques de código con el resaltado de sintaxis adecuado.) *

■ *Consejo*: Mantenga los mismos nombres variables (cerca de " , " lejos " , " .
■ *Consejo*: Escribe un pequeño `main()`/`_main_` para probar la entrada de la muestra, que muestra que puedes ejecutar la solución localmente, un impulsor de confianza para la entrevista.

-...

### 7. Cómo hablar de este problema en una entrevista

1. **Clarificar la cuestión**: ¿Podemos saltar *exactamente* `k` pasos o en la mayoría `k`? ”
2. **Explicar el fundamento codicioso** antes de escribir código.
3. ** Comprobaciones de los límites de la mención**: “¿Y si el array tiene la longitud 1? ”
4. **Camina a través de un simple ejemplo** en la pizarra (manejar los turnos de la ventana).
5. **Afinar con el código** – resaltar que está utilizando el espacio O(1) y un paso.

-...

### 8. Job‐Hunting Angle – Why Esto importa

■ *Las entrevistas no son sólo sobre la respuesta; se trata de la narrativa que presenta. *
- Mostrar que puedes pensar **verde** y **eficientemente**.
√ - Destacar su *código de calidad* – variables concisas, bien conocidas, y comentarios.
- Compartir su solución en GitHub o una cartera; a los reclutadores les encanta ver código limpio y comentado.

**Resume Bullet* *
• Implementó un algoritmo codicioso de tiempo lineal para resolver LeetCode 45 “Juego II”, logrando O(n) tiempo de funcionamiento y O(1) uso de memoria en Java, Python y C++.

-...

### 9. Final Takeaway

*La codiciada solución de Near-Far es un problema perfecto para su próxima entrevista técnica. Domina la lógica, posee el código en al menos un idioma, y convertirás un desafío de 45 segundos en una entrevista de confianza. *

Buena suerte, y que su próximo reclutador te vea como el candidato *fast-moving* que ya *jumps* pasado la competencia! 🚀

-...

■ *No dude en adaptar las palabras clave de SEO arriba en las etiquetas de su blog. Agregue una imagen corta del diagrama de ventana deslizante, y tendrá un artículo digno de compartir que los reclutadores amarán. *