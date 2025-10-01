-...
Título: LeetCode 2141. Tiempo máximo de ejecución de N Computers -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 Solution Overview – LeetCode 2141: Maximum Running Time of N Computers

**Problema de declaración* *
Usted tiene 'n ' computadoras y un array 'baterías'.
`baterías[i]` es el número de minutos que una sola batería puede alimentar un ordenador.
En cualquier minuto entero puede cambiar las baterías entre ordenadores (el intercambio no lleva tiempo).
Su objetivo es ejecutar todas las computadoras "n" simultaneamente** durante tantos minutos como sea posible.
Devuelve ese número máximo de minutos.

■ **Constraints**
* `1 ≤ n ≤ baterías.length ≤ 10^5`
* `1 ≤ pilas[i] ≤ 10^9`

La visión clave:
Durante cualquier intervalo de longitud " T " , cada batería puede contribuir a la mayoría de `T ' minutos de potencia, incluso si podría funcionar más tiempo.
Por lo tanto, la contribución total de todas las baterías a una " carrera de minutos " es en la mayoría de `min(batería, T) ' para cada batería.

Presentaremos dos enfoques populares, ambos con una complejidad temporal de `O(m log m)`. donde `m = pilas.length`.
El método **sort-and‐trim** es más fácil de entender e implementar, mientras que el método ** búsqueda binaria** es un poco más "algorítmico" y muestra un ángulo diferente.

A continuación encontrará implementaciones listas para copiar en **Java**, **Python**, y **C+**.

-...

##  Detention 1ف⃣ Sort‐and‐Trim Solution (O(m log m))

La idea es mantener todas las baterías excepto las que serían "desperdiciadas" si son demasiado poderosas en comparación con el tiempo de funcionamiento promedio actual.

1. **Sorta la batería.
2. Computar el consumo total de energía.
3. Partiendo de la batería más grande, mantenga la eliminación de la consideración mientras que es más grande que el promedio actual posible `sum / (n - k)`.
*Cuando se quita una batería, reducimos la suma y la suma de uno. *
4. Después de recortar, la respuesta es simplemente `sum / n` (división entero – todo encaja perfectamente ahora).

### Why It Works

- Si la batería más fuerte tiene más potencia que el promedio (`sum / n`), se utilizaría solo para ese tiempo promedio y el resto de las baterías sería ocioso.
Retirarlo y recomponer el promedio da un límite más estrecho.
- Seguimos haciendo esto hasta que la batería más fuerte puede compartir la carga con el resto de las baterías sin perder energía.
En ese momento cada batería se puede utilizar para exactamente `sum / n` minutos, que es óptimo.

-...

## 🧪 2️ Binary Search Solution (O(m log sum))

Enfoque alternativo pero igualmente rápido:

1. Computar la energía total 'total'.
2. Set `low = 0`, `high = total / n`. (No puede exceder este límite superior.)
3. Mientras que 'bajo ≤ alto':
* Comprobar si es posible una carrera de minutos.
* Si es así, guárdalo y busque más alto; de lo contrario busque más abajo.
4. Para **ver** un candidato `mid`:
* Cada batería aporta minutos `min(battery, mid).
* Sum all contributions; if the sum is at least `n * mid`, the run is feasible.

Ambos enfoques son `O(m log m)`, pero la versión de búsqueda binaria utiliza sólo un solo paso sobre el array por iteración.

-...

## 📄 3VIEW⃣ Code Implementations

A continuación se presentan soluciones limpias y comentadas en tres idiomas.
Todos utilizan aritmética de 64 bits ( " largo " ) porque la suma total puede superar 32 bits.

## Java

``java
importa java.util. Arrays;

Solución de la clase pública {}
*
* Devuelve el número máximo de minutos todos los ordenadores pueden funcionar simultáneamente.
* @param n número de computadoras
* @param baterías matriz de tiempos de funcionamiento de la batería
* @retorno máximo tiempo de funcionamiento simultáneo (minutos)
*/
public long maxRunTime(int n, int[] pilas) {}
Arrays.sort(baterías); // O(m log m)

larga suma = 0;
para (int b : baterías) suma += b; // energía total

int idx = pilas.length - 1; // empezar desde el mayor
mientras (idx ю= 0 " pilas iguales [idx] {}
suma -= pilas[idx]; // eliminar batería demasiado potente
idx--; // reducir la matriz usable
n...
}

devolver la suma / n; // respuesta final
}
}
`` `

## Python

``python
def maxRunTime(n: int, pilas: list[int] int:
"
Devuelve el número máximo de minutos, todos los ordenadores pueden funcionar simultáneamente.
"
baterías.sort() # O(m log m)

total = sumas
i = len(baterías) - 1 # índice de batería más grande

# Trim pilas que se desperdiciarán
mientras que i >= 0 y pilas[i] √ total // n:
total -= pilas[i]
I -= 1
n -= 1

total de retorno // n
`` `

### C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
largo tiempo maxRunTime(int n, vector asignadoint {}
(baterías.begin(), pilas.end()); // O(m log m)

larga suma = 0;
para (int b : baterías) suma += b; // energía total

int idx = pilas.size() - 1;
mientras (idx ю= 0 " pilas iguales [idx] {}
suma -= pilas[idx]; // eliminar demasiado potente
idx...
n...
}
devolver la suma / n;
}
};
`` `

-...

## 📚 4️ Blog Artículo – “El Bien, el Mal, y el Ugly de LeetCode 2141”

■ **Título**: 2141 – Tiempo máximo de ejecución de N Computers*
■ **Meta‐Description**: Descubra la solución óptima, las trampas y las ideas de entrevista para LeetCode 2141. Lea la guía completa en Java, Python y C++.

-...

### 1. Introducción

LeetCode 2141 le pide que maximice el tiempo de funcionamiento simultáneo de un conjunto de computadoras utilizando una piscina de baterías.
Es un problema clásico *resource‐allocation* que aparece con frecuencia en entrevistas técnicas.
¿Por qué? Debido a que te obliga a pensar en **Planificación de capacidad**, **Recortar enormemente**, y ** búsqueda binaria** – todas las habilidades que son altamente valiosas para el diseño de datos y los roles de backend.

### 2. Recaptación de problemas

Tienes:
- No computadoras.
- Baterias de longitud.
- `baterías[i]` = tiempo de funcionamiento de la batería `i ' (minutos).

Puede cambiar las baterías entre ordenadores en cualquier momento (el intercambio es instantáneo).
Objetivo: encontrar el número máximo de minutos todas las computadoras pueden funcionar *simultaneamente**.

### 3. Intuición " Observaciones clave

TENCIÓN ANTERIOR Por qué importa
Silencio...
TEN **O(1) Swap** Silencio Permite volver a equilibrar al instante; la única limitación real es la capacidad de la batería. Silencio
Silencio **La batería no puede exceder T** Silencio Durante un intervalo de `T`-minuto, una batería contribuye a la mayoría de `T` minutos. Silencio
Silencio **Feasible Total** Silencio Una carrera de longitud `T` es factible sif `explotar min(batería, T) ≥ n * T`.

La última observación nos da una función **decisión** – un candidato perfecto para la búsqueda binaria.

### 4. El Bien - Sort-and-Trim

##### Lo que hace

1. Ordenar baterías ascendiendo.
2. Mantenga el recortar la batería más fuerte si de otro modo sería “idle”.
3. Las baterías restantes se pueden utilizar para exactamente `sum / n` minutos.

#### Why It's Good

Perfecto para una entrevista.
- **Fast** - un `O(m log m)` tipo + un solo escaneo lineal.
- **Determinista** – sin factores aleatorios; siempre la misma respuesta para la misma entrada.

#### Code‐Snippet (Java)

``java
Arrays.sort(batteries);
Mientras que (baterías[idx]
`` `

### 5. El malo – las caídas de búsqueda binaria

La búsqueda binaria es elegante pero sutil:

- **Atado superior equivocado** → bucle infinito.
Uso siempre `alto = total / n`, no `total` en sí mismo.
- **División de enteros** – `mid = (bajo + alto) / 2` puede desbordarse; use `bajo + (alto - bajo) / 2`.
- ** Función de viabilidad** – usted debe resumir `min(batería, mediados)`; olvidarse de cap en `mid` dará resultados incorrectos.

#### Interview‐Ready Tip
Si se le pide que justifique la búsqueda binaria, resalta que `mid` es un **guess** para el tiempo de ejecución objetivo, y la prueba de viabilidad es esencialmente un *knapsack* con pesos atados.

### 6. Casos Ugly – Common Traps & Edge

Silencio Silencio Silencio Silencio Silencio
Silencio...
Silencio **Desbordamiento de 32 bits** Silencio `sum` de 10^5 baterías cada 10^9 = 10^14 Silencio Uso `long` / `long long`. Silencio
Silencio ** Lista de baterías vacías** Silencioso `m ' Silencioso El problema garantiza `m ≥ n`; todavía, guardia contra la división por cero. Silencio
Silencio **Todas las Baterías Igual** Silencioso `baterías = [5,5]` Silencio Después de clase, el lazo de recortar no funciona; la respuesta es `15/3 = 5`. Silencio
Silencio **Very Strong Battery** Silencioso `[1000,1,1]`, `n=2` peru Trim 1000 → `sum=2`, `n=2`, respuesta `1`. Silencio

### 7. Análisis de la complejidad

Silencio Silencio Silencio Silencio Silencio
Silencio--------------
Silencio Trim Silencio `O(m log m)` Silencio `O(1)` extra confidencialidad
tención binaria búsqueda Silencioso `O(m log (total / n))' extra confidencialidad

Con `m ≤ 10^5`, ambos están bien dentro de los límites de LeetCode.

### 8. Consejos de entrevista

- **Explicar la función de decisión** antes de codificación; a los entrevistadores les encanta ver su proceso de pensamiento.
- **Mostrar la manipulación de la caja del borde** – por ejemplo, cuando todas las baterías son iguales, o una batería es astronómicamente mayor.
- ** alternativas de la mención** – por ejemplo, cola de prioridad, DP – para demostrar la amplitud del conocimiento, incluso si te asientas en un obstáculo para la brevedad.
- **Hora su solución** en una pizarra blanca – asegúrese de que no exceda la ventana asignada de 30 minutos.

### 9. Conclusión

LeetCode 2141 es una buena ilustración de **gran trimming + razonamiento aritmético**.
Al dominar este problema, usted mostrará un pensamiento algoritmo fuerte, una comprensión sólida de la aritmética entero, y la capacidad de optimizar tanto para *time* como *space*—exactamente los reclutadores de habilidades buscan en backend, ingeniería de datos, y funciones de personal completo.

-...

## 🔑 5down Por qué este blog te ayuda a aterrizar tu próximo trabajo

- ¿Qué? El artículo pasa por el conducto de razonamiento completo.
- *Multi‐language* Java, Python, C++ muestran una competencia multiplataforma.
- **SEO-friendly**: Palabras clave como *Maximum Running Time of N Computers*, *LeetCode 2141*, *búsqueda binaria*, *entrevista de codificación*, *Java*, *Python*, *C++* asegurar la visibilidad en los motores de búsqueda de empleo.
- ** Estructura del plano**: Los encabezados, tablas y bloques de código hacen que el artículo sea fácil de esquiar, un gran plus para los reclutadores escaneando rápidamente.

-...

#### 📌 Takeaway

■ **Sort‐and‐Trim** le da una solución limpia y óptima que es fácil de explicar en una entrevista.
■ **Binary Search** ofrece una perspectiva más algorítmica y demuestra el mismo resultado con una lente diferente.
■ Sea cual sea el presente, esté listo para discutir casos de borde y justificar el cheque de viabilidad —estos son los momentos de entrevista “buenos” que dejan una impresión duradera.

Buena suerte, y feliz codificación!