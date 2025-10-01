-...
Título: LeetCode 2406. Divide Intervals Into Minimum Number of Groups -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 **Divide Intervals Into Minimum Number of Groups – 2406 (LeetCode)* *

Silencio Idioma Silencio Tiempo Silencioso
Silencio...
Silencio **Java** Silencioso `O(n log n)` Silencio
Silencioso **Python** Silencio `O(n log n)` Silencio
Silencio **C+** Silencioso `O(n log n)` Silencio

■ **Problema**:
■ Dados `intervalos[i] = [lefti, righti]` (inclusive), dividir todos los intervalos en los grupos más pocos posibles de tal manera que no se superponen dos intervalos en el mismo grupo. Devuelve el número mínimo de grupos.

-...

## 🔍 Why This Problem is a *Job‐Entreview Gold‐Mine*

1. **Core Concepts**: Clasificación, técnica de dos puntos, programación de intervalos codiciosos, línea de barrido.
2. **Idioma Agnostic**: Solvable en O(n log n) en Java, Python, o C++.
3. **Entrevista común Twist**: El intervalo *puntos son inclusivos*, por lo que `[1,5]` y `[5,8]` ## Do** overlap.
4. **Test‐Case Depth**: Grandes entradas (`n ≤ 105`) – te obliga a pensar en el tiempo y la memoria.

■ *Si haces esta pregunta, los reclutadores dirán “Comprendes la codicia + clasificación – perfecto para el diseño de sistemas y la entrevista de backend!”*

-...

## 📦 Cómo funciona el Código – “Bueno, malo,”

Silencio Silencio
Silencio------------Prince------
Silencio **Aprobación** Silencio Línea de barrido de dos puntos, O(n log n) Silencio Olvídate de la regla inclusiva → respuesta incorrecta en los casos de límite Silencio Use una prioridad-queue/heap para rastrear los tiempos finales – obras pero más pesado (O(n log n) + memoria extra)
Silencio **Complejidad** Silencio rápido y de memoria-eficiente Silencio O(n2) si comparas todos los pares Silencio O(n log n) pero sobrematar para este problema
Silencio **Readability** Silencio Separación clara de los inicios / extremos Silencio Mezclado en el lugar actualizaciones → difícil de seguir Ø Trucos de lambda obfuscados

### llevándose bien: dos puntos

1. **Sorta** todos los tiempos de inicio y todos los tiempos finales.
2. Camina por el principio.
3. Si el inicio actual es *después* el final más temprano (`start > end[endPtr]`), el intervalo puede reutilizar un grupo → move `endPtr`.
4. De lo contrario, necesitamos un nuevo grupo → aumento `grupos`.

Esta es esencialmente la misma idea que el problema clásico de “Meeting Rooms II”, pero más simple porque sólo necesitamos los intervalos concurrentes *maximum*.

### ❌ Bad: Heap/TreeSet Variant

``java
PriorityQueue se cumplióInteger confianza pq = nueva PrioridadQueueue quiso();
para (int[] intervalo : intervalos) {}
mientras (!pq.isEmpty() " pq.peek() " () " ) " )
pq.offer(interval[1]);
}
pq.size();
`` `

- Funciona, pero O(n log n) * y* un montón extra → innecesario sobrecabezamiento.

### 😱 Ugly: Over-Engineered Sweep

- Clasificar, luego escanear con un contador que se aumenta/degrada en la mosca, pero con controles de límites desordenados.
- Difícil de depurar y mantener.

-...

## 📚 Full Code (Three Languages)

■ Las tres implementaciones siguen la misma lógica:
■ *Sort comienza & extremos → barrido de dos puntos → contar intervalos máximos concurrentes. *

-...

## Python 3

``python
de la importación Lista

Solución de clase:
def minGroups(self, intervalos: List[List[int]]) int:
"
Número mínimo de grupos para dividir intervalos no superpuestos.

Tiempo : O(n log n) – clasificación
Espacio : O(n) – arrays auxiliares
"
comienza = orden(i[0] para i en intervalos)
extremos = ordenados (i[1] para i en intervalos)

end_ptr = 0 # puntos al intervalo final más temprano
grupos = 0

para s en principio:
# Si el intervalo comienza después del primer final,
# podemos reutilizar ese grupo (move end_ptr).
si el título termina[end_ptr]:
end_ptr += 1
más:
Necesito un nuevo grupo.
grupos += 1

grupos de retorno
`` `

-...

## Java (Java 17+)

``java
importa java.util. Arrays;

Clase Solución {
public int minGroups(int[][] intervalos) {
int n = intervalos. longitud;
int[] comienza = nuevo int[n];
int[] fines = nuevo int[n];

para (int i = 0; i)
[i] = intervalos[i][0];
fines[i] = intervalos[i][1];
}

Arrays.sort(starts);
Arrays.sort(ends);

int endPtr = 0, grupos = 0;
para (int s : comienza) {}
si (s не fines[endPtr]) { // intervalo puede reutilizar un grupo
final Ptr++;
♪ otra { // necesita un grupo nuevo
grupos++;
}
}
grupos de retorno;
}
}
`` `

-...

### C++ (C+17)

``cpp
Incluido el título
#include >

Clase Solución {
public:
int minGroups(std::vector seleccionadosstd:::vector fieltro intervalos de unión) {}
int n = intervalos.size();
std::vector garantizadoint empieza(n), fines(n);
para (int i = 0; i) {}
[i] = intervalos[i][0];
fines[i] = intervalos[i][1];
}
std::sort(starts.begin(), starts.end());
std::sort(ends.begin(), end.end());

int endPtr = 0, grupos = 0;
para (int s : comienza) {}
si (s √≥ fines[endPtr]) // reutilizar un grupo
++endPtr;
más
++grupos; // nuevo grupo necesario
}
grupos de retorno;
}
};
`` `

■ **Consejo**: Para **C++**, prefiera `vector fielint `sobre `vector seleccionadovectorado' cuando la entrada se lee una vez.

-...

## 📝 Blog‐Style Write‐Up (SEO Optimized)

-...

# Divide Intervals Into Minimum Number of Groups (LeetCode 2406) – Java, Python, C++ Solutions

Si te estás preparando para una entrevista de codificación, a menudo encontrarás preguntas relacionadas con intervalos. Uno de los más complicados es ** "Divide Intervals Into Minimum Number of Groups"** (LeetCode 2406). En este post, romperemos el problema, caminaremos a través de una solución O(n log n), presente código de trabajo en **Java, Python y C+**, y discutiremos las formas *buena*, *bad* y *muy* para abordarlo. Este artículo está lleno de palabras clave que los reclutadores aman: *grupos mínimos, codiciados, líneas de barrido, salas de reuniones, intervalos inclusivos, preparación de entrevistas, entrevista de codificación*, y más.

-...

Declaración de problemas

Se le da un array `intervalos` donde `intervalos[i] = [left_i, right_i]` (inclusive).

Divide los intervalos en los grupos **feo** de tal manera que **no hay dos intervalos en el mismo grupo superpuesta**. Dos intervalos superponen si comparten al menos un punto, ** incluyendo los puntos finales**. Devuelve el número mínimo de grupos requeridos.

■ *Ejemplo*
[5,10],[6,8],[1,5],[2,3],[1,10] `
■ Producto: `3`

-...

## 🧠 Why This Question Matters

- **Greedy + Sorting**: Técnica de entrevista clásica.
- ** Puntos finales inclusivos**: Muchos candidatos olvidan que `[1,5]` y `[5,8]` * do* overlap.
- **Large Constraints**: `n ≤ 105` obliga a diseñar una solución `O(n log n)`.
- **Language‐agnostic**: Funciona en Java, Python y C++.

-...

## 🛠Пле Solution Overview – Two‐Pointer Sweep Line

1. **Separar** todos los puntos de inicio y final en dos arrays.
2. **Sorta** cada matriz.
3. **Pasa a través de los inicios** mientras rastrea el final más temprano (`endPtr`).
- Si el comienzo actual `s` es ** después** `ends[endPtr]` (`s ⇩ termina[endPtr]`), podemos reutilizar ese grupo → move `endPtr`.
- De lo contrario, necesitamos un nuevo grupo** → aumento de grupos.
4. Los grupos finales son iguales al número mínimo de grupos.

■ Esta es la misma lógica utilizada para **Meeting Rooms II**, pero el punto final incluyente cambia la comparación de ``=` a ` ``conejo`.

################################################################################################################################################################################################################################################################
- **Tiempo**: `O(n log n)` (sorting dominates).
- **Espacio**: `O(n)` (dos arrays auxiliares).
Dos bucles, un solo puntero, directo.

#### ❌ Bad
- **Heap / Priority‐Queue** variante - todavía `O(n log n)` pero añade salto innecesario sobre la cabeza.

#### 😱 Ugly
- Un barrido con contadores y actualizaciones en el lugar que son difíciles de razonar.

-...

## 📦 Code Snippets

■ Cada aplicación del lenguaje sigue los mismos pasos algorítmicos.

## Python 3

``python
de la importación Lista

Solución de clase:
def minGroups(self, intervalos: List[List[int]]) int:
comienza = orden(i[0] para i en intervalos)
extremos = ordenados (i[1] para i en intervalos)

end_ptr = 0
grupos = 0

para s en principio:
si el título termina[end_ptr]:
end_ptr += 1
más:
grupos += 1

grupos de retorno
`` `

## Java (Java 17+)

``java
importa java.util. Arrays;

Clase Solución {
public int minGroups(int[][] intervalos) {
int n = intervalos. longitud;
int[] comienza = nuevo int[n];
int[] fines = nuevo int[n];

para (int i = 0; i)
[i] = intervalos[i][0];
fines[i] = intervalos[i][1];
}

Arrays.sort(starts);
Arrays.sort(ends);

int endPtr = 0, grupos = 0;
para (int s : comienza) {}
si (s √≥ fines[endPtr]) endPtr++;
más grupos++;
}
grupos de retorno;
}
}
`` `

### C++ (C+17)

``cpp
Incluido el título
#include >

Clase Solución {
public:
int minGroups(std::vector seleccionadosstd:::vector fieltro intervalos de unión) {}
int n = intervalos.size();
std::vector garantizadoint empieza(n), fines(n);
para (int i = 0; i) {}
[i] = intervalos[i][0];
fines[i] = intervalos[i][1];
}
std::sort(starts.begin(), starts.end());
std::sort(ends.begin(), end.end());

int endPtr = 0, grupos = 0;
para (int s : comienza) {}
si (s ю termina[endPtr]) ++endPtr;
más ++grupos;
}
grupos de retorno;
}
};
`` `

-...

## 📈 Complexity Analysis

Silencio Idioma Silencio Tiempo Silencioso
Silencio...
TENIDO Python TENIDO `O(n log n)` Silencio
Silencio Java Silencio `O(n log n)` Silencio `O(n)` Silencio
TENIDO C++ TENIDO `O(n log n)` Silencio

■ El tiempo de ejecución está dominado por la clasificación. El barrido es lineal (`O(n)`).

-...

## 🎯 Interview Tips

1. **Clarificar puntos finales inclusivos** antes de la codificación.
2. **Explicar el barrido** al entrevistador – mostrar que está contando el número máximo de intervalos simultáneos.
3. **Test edge cases**:
- `[1,5], [5,10]` → 2 grupos.
- `[1,2], [3,4]` → 1 grupo.
4. **Mención** la relación con las Salas de Reuniones II, como demuestra su amplitud de conocimiento.

-...

## 🔗 Más lectura

*Salas de reuniones II* – LeetCode 253
- # Intervalos no relacionados # - LeetCode 435
*Cracking the Coding Interview*
*Algoritmos (Cormen, Leiserson, Rivest, Stein)*

-...

## 🚀 Takeaway

El **Divide Intervals Into Minimum Número de grupos** problema es una mina de oro para los entrevistadores para probar su dominio de clasificación codicioso, manejo de límites y eficiencia algorítmica. La solución limpia de línea de barrido de dos puntos es eficiente, fácil de implementar, y lenguaje-agnóstico. Al compartir este post, también estás mostrando la capacidad de escribir código limpio en Java, Python y C++, exactamente lo que buscan los reclutadores.

¡Feliz codificación y buena suerte con tu próxima entrevista!

-...

## ♥ Final Note

■ Si encontró útil este artículo, compártelo en LinkedIn o Twitter y etiqueta a tus reclutadores con #codinginterview #leetcode2406 #minGroups.

-...

**Palabras clave usadas:** `Divide Intervals Into Minimum Number of Groups, LeetCode 2406, grupos mínimos, algoritmo codicioso, línea de barrido, salas de reuniones II, puntos finales inclusivos, entrevista de codificación, solución Java, solución Python, solución C++, preparación de entrevistas, complejidad algorítmica.