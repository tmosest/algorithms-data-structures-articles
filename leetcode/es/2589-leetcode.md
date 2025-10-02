-...
Título: LeetCode 2589. Tiempo mínimo para completar todas las tareas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# LeetCode 2589 – Tiempo mínimo para completar todas las tareas
**Solutions in Java Silencio Python ← C++**
**SEO guía optimizada** que cubre el *bueno, el malo, y el feo* de este problema, perfecto para la preparación de entrevistas y la caza de trabajo.

-...

Problema Recap

- ** Entrada**: 'taks[i] = [start_i, end_i, duration_i] `
*La tarea debe ejecutarse para los segundos `duration_i` (no necesariamente continuo) dentro de la ventana inclusiva `[start_i, end_i]`. *
- **Computer**: puede ejecutar un número ilimitado de tareas al mismo tiempo.
- ** Objetivo**: Encontrar los segundos totales ** el ordenador tiene que ser encendido para terminar *todas las tareas*.

■ **Constraints**
* 1 ≤ tareas. longitud ≤ 2000
* 1 ≤ start_i ≤ end_i ≤ 2000
* 1 ≤ duración_i ≤ end_i − start_i + 1

-...

## ✅ The “Good” – Why Esta Solución Rocks

Silencio Idioma Silencio Tiempo Complejidad Silencio Complejidad Espacial Por qué funciona
Silencio--------------------------
Silencio **Java** Silencioso `O(n * w)` (caso peor) → `O(n * 2000)` ♥ `O(n)` Silencio `O(2000)`  Greedy + matriz booleana
Silencio **Python** Silencio Igual que Java Silencio Igual que Java
Silencio **C++** Silencio Igual que Java TENIDO Igual que Java TENIDO

- **Greedy on the right-endpoint** garantiza que cada intervalo ya ha “controlado” todas las superposiciones posibles con los intervalos que terminan antes.
- The Boolean/bit array (`used[1..2000]`) marca cada segundo el ordenador está “en”.
- Nosotros ** primero** consumimos cualquier segundo ya marcado dentro de la ventana de la tarea, luego **add los segundos restantes** a partir del "fino" del intervalo y moviendo a la izquierda.
- La respuesta final es simplemente la cuenta de segundos marcados.

-...

El código

■ Las tres implementaciones asumen el entorno LeetCode: un único método/función llamado 'findMinimumTime' (o la clase Python `Solution').

-...

##### Java (Java 17+)

``java
importa java.util. Arrays;
importa java.util. Comparador;

Solución de la clase pública {}
*
* LeetCode 2589 – Tiempo mínimo para completar todas las tareas
* Grisía + matriz booleana (índice máximo 2000)
*/
int findMinimumTime(int[][] tareas) {
// Ordenar por el punto final derecho
Arrays.sort(taks, Comparator.comparingInt(a - título a[1]));

// Segundos marcados: índice 1..2000
booleano[] utilizado = nuevo booleano[2001];

para (int[] t : tareas) {
int start = t[0];
int end = t[1];
int dur = t[2];

// 1 / ⃣ Contar cuántos segundos ya utilizados en esta ventana
para (int i = start; i <= end " dur " 0; i++) {
(utilizado[i]) {}
dur...; // este segundo cuenta para la tarea
}
}

Rellene los segundos necesarios a la derecha
para (int i = end; dur √≥ 0 " clâ i " start; i--) {
si (!used[i]) {}
utilizado[i] = verdadero; // encender el ordenador en este segundo
dur--; // consumir un segundo de la tarea
}
}
}

// Suma de todos los segundos marcados es la respuesta
int ans = 0;
for (boolean b : used) if (b) ans++;
devolver los ans;
}
}
`` `

-...

#### Python (Python 3.8+)

``python
de la importación Lista

Solución de clase:
def find Mínimo(auto, tareas: List[List[int]]) - int:
"
LeetCode 2589 – Tiempo mínimo para completar todas las tareas
Greedy + Boolean array (tamaño 2001)
"
# Ordenar por el final del intervalo
tasks.sort(key=lambda x: x[1])

utilizado = [0] * 2001 # index 1..2000

para comenzar, terminar, duración en tareas:
# 1 Consumo ya marcado segundos dentro de la ventana
para i en rango(start, end + 1):
si se usa[i]:
duración -= 1
si la duración == 0:
descanso

# 2⃣ Añadir los segundos perdidos a la derecha a la izquierda
i
mientras dure 0:
si se usa[i] == 0:
utilizados[i] = 1
duración -= 1
I -= 1

retorcimiento (utilizado)
`` `

-...

#### C++ (C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int findMinimumTime(vector asignadovector identificadoint tareas) {
// Ordenar por el punto final derecho
(tasks.begin(), tasks.end(),
[](cont vector identificadoint ánimo a, const vector identificadoint círculo b) {
devolver a[1]
});

vector empleado(2001, 0); // index 1..2000

para (auto golpe t : tareas) {
int l = t[0], r = t[1], dur = t[2];

// 1 / ⃣ Conteo ya usado segundos en esta ventana
para (int i = l; i) {}
si (utilizado[i]) dur...
}

// 2down Añadir segundos perdidos a la derecha
para (int i = r; i l ' dur; --i) {
si (!used[i]) {}
utilizado[i] = 1;
dur...
}
}
}

// Suma de todos los segundos marcados
retorno acumulado(utilizado.begin(), utilizado.end(), 0);
}
};
`` `

-...

## 📝 El Blog: “El Bien, el Mal, y el Ugly of Solving LeetCode 2589”

■ **Descripción de los datos (SEO):* *
■ *Aprenda a romper LeetCode 2589 – Tiempo mínimo para completar todas las tareas. Obtenga soluciones Java, Python y C++, intuición algorítmica, complejidad del tiempo y consejos de entrevista. *

-...

#### ## 1down⃣ Lo que el problema quiere (bueno)

Por qué ayuda a vivir
Silencio...
Silencio **Intervalos + Duración** Silencio Clásico sabor “intervalo de programación”. Silencio
Silencio **Paralelismo ilimitado** Silencio Hace el problema sobre *coverage* en lugar de la programación clásica. Silencio
Silencio **Tiempo pequeño (≤2000)** Silencio nos permite utilizar un simple O(2000) "línea de tiempo" array. Silencio

La parte **buena** es que las limitaciones son generosas: puedes marcar cada segundo explícitamente. Eso elimina la necesidad de estructuras de datos complejas como árboles de segmentos o árboles indizados binarios.

-...

#### 2down⃣ La intuición (bueno)

1. *La onda es libre*
*Si dos tareas comparten un segundo, el ordenador ya está encendido para ese segundo; sin costo adicional. *
2. **Greedy from the Right**
*Para cualquier tarea, tratamos de terminar tantos segundos como sea posible en los últimos segundos de su intervalo. *
3. **Sort by `end`**
*Cuando los intervalos se clasifican por su fin derecho, ya se han considerado todas las superposiciones posibles con intervalos previamente procesados. *

■ **Por qué la clasificación por `start` falla* *
■ Si usted ordena por el punto final izquierdo, una tarea que comienza temprano puede "establecer" un segundo de una tarea posterior que necesita ese segundo, causando que el algoritmo para anular el ordenador encendido.

-...

#### 3down⃣ El algoritmo básico (bueno)

`` `
ordenar tareas por tiempo final
utilizado[1..2000] = 0 // Boolean array: 1 si la computadora está en ese segundo
para cada tarea [l, r, d] en orden ordenado:
// 1 / ⃣ Conteo ya usado segundos dentro [l, r]
para mí
si se usa[i]: d -= 1
si d == 0

// 2down Añadir los segundos restantes a la derecha
i
mientras que d 0:
si !used[i]:
utilizados[i] = 1
d-= 1
I -= 1

respuesta = suma (utilizado)
`` `

- *Hora*
*El peor de los casos*: cada tarea escanea todo su intervalo → `O(n * 2000)` ♥ `O(n)` porque 2000 es una constante.
- **Espacio**: `O(2000)` para la matriz booleana → constante.

-...

#### 4down⃣ Los Pitfalls (Bad)

Silencio Pitfall Silencioso Silencioso
Silencio------------
Silencio **Wrong sort key** TEN Respuesta incorrecta o TLE TENIDO Siempre ordenar por `end` (`taks[i][1]`). Silencio
Silencio **Off‐by-one en la matriz booleana** Silencio Índice Array 0 o 2000 desaparecidos Silencio Allocate tamaño `2001` (o `2005` para la seguridad). Silencio
Silencio **Ignorando ya usados segundos** Silencio Sobre-contando turnos en Silencio Subtract `used[i]` de `duration` antes de añadir nuevos segundos. Silencio
Silencio **Using a `Set Garantizado'** Silencio Trabaja pero más lento (`O(log n)` per insert) Silencio Usar una matriz booleana/bit – tiempo constante. Silencio
Silencio **Procesamiento de tareas en orden de entrada** Silencio Resultado equivocado para tareas superpuestas Silencio antes de procesar. Silencio

-...

#### 5down⃣ El “Ugly” – Cuando las cosas se complican

1. **Si `duration_i` fuera mayor que la longitud del intervalo* *
La estrategia avaricia todavía funciona porque la tarea puede dividirse arbitrariamente, pero debe asegurarse de que no salga de los límites mientras se llena de la derecha.
*Solución*: aprieta el bucle a `i √≥= l ' y para una vez `duration ' se convierte en 0.

2. **Amplio rango de entrada (con relación 2000)**
En una variante hipotética con `start_i, end_i` hasta 109, la matriz booleana es imposible.
*Suplente*: utilice un **`TreeSet` o `HashSet`** para almacenar segundos usados y un ** árbol de segmento** o ** árbol indizado binario** para consultas de gama.
El enfoque de línea de tiempo ya no es “bueno” pero se convierte en “muy” – más código, más errores.

3. **Minucios tareas que requieren exactamente el mismo segundo* *
Si muchas tareas tienen ventanas idénticas, el algoritmo todavía cuenta cada segundo una vez, pero no debe contar doblemente.
*Insight*: el primer bucle del algoritmo ya consume todos los segundos superpuestos, por lo que el segundo bucle solo añade nuevos segundos únicos.

-...

### 6 Cambios en la entrevista Consejos (Ready‐to‐Use)

- **Explicar la idea "línea"** antes de bucear en código.
- **Mostrar la prueba clave** que clasificar por 'end' es óptima: cualquier intervalo posterior no puede beneficiarse de segundos anteriores no utilizados.
- **Mention the constant‐time Boolean array** – es un gran truco para evitar la estructura de datos en las entrevistas de codificación.
- **Preparación para preguntas de seguimiento**: “¿Y si el horizonte era enorme?” – estar listo para discutir árboles de segmento o coordinar la compresión.

-...

#### 6down⃣ Pensamiento final

Cracking LeetCode 2589 es sobre **coverage**. Una vez que te das cuenta de que la superposición no cuesta nada y que el horizonte temporal es pequeño, el problema se reduce a un simple barrido codicioso.
El código Java, Python y C++ ilustra la misma idea elegante, dejándote centrarte en la visión **algorítmica** en lugar de combatir los detalles de la implementación.

Buena suerte en su viaje de codificación y su próxima entrevista técnica! 🚀

-...

■ *No dude en copiar/pasar los fragmentos de código o todo el blog en sus notas. ¡Feliz codificación! *

-...



-...
**Disfrute del código “bueno”, evite las trampas “malas” y prepárese para abordar los casos “muy” de borde si el problema cambia. #

-...

■ **TL;DR**: Sort by `end`, use a Boolean array, consuma ya usado segundos, agregue rápidamente segundos perdidos de la derecha, resumiendo segundos marcados. Las tres implementaciones lingüísticas ofrecen la misma solución espacial " O " y " O(1) " .

-...

¡Feliz codificación! ▪