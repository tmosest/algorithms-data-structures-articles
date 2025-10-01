-...
Título: LeetCode 1769. Número mínimo de operaciones para mover todas las bolas a cada caja -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. El problema en un glance

** Nombre del proyecto:** 1769. * Número mínimo de operaciones para mover todas las bolas a cada caja*
**Dificultad:**
**Enlace:** ▪ https://leetcode.com/problems/minimum-number-of-operations-to-move-all-balls-to-each-box/

■ Tienes cajas en línea.
"boxes[i]` es `'0'` si la caja *i‐th* está vacía, `'1'` si contiene una bola.
■ En una operación se puede mover **una bola** a una caja *adjacente* (` sometidai-j habit=1`).
■ Después de los movimientos usted puede tener más de una bola en una caja.
■
■ **Task:** Para cada índice `i` (0-basado) computa el número total mínimo de operaciones necesarias para reunir *todas* bolas en el cuadro `i`.
■
■ Devuelve un array `respuesta[0 ... n-1]` de tamaño `n`.

Constraints: " 1 " 0 " 0 " , " , " .

-...

## 2. La Idea Central - Prefijo de dos pasos / acumulación de sufijo

La forma bruta-fuerza sería simular mover cada bola a cada objetivo, que es `O(n2)` para cada bola y obviamente infeasible.
En cambio, podemos calcular la respuesta para cada caja en tiempo lineal con dos pases simples:

Silencio Lo que almacenamos Silencio ¿Por qué funciona
...--------------------------------
Silencio **Izquierda a derecha paso** Silencio Para cada índice `i` el número ** de bolas a la izquierda** de 'i' (`leftCnt`) y la distancia **total** esas bolas necesitan viajar para llegar a `i` (`leftOps`). Silencio Cada vez que nos movemos a la derecha, la distancia a la nueva caja aumenta en 1 para cada bola ya a la izquierda. Silencio
ANTERIOR* Pasillo izquierdo** Silencio Para cada índice `i` el número ** de bolas a la derecha** de `i` (`rightCnt`) y la distancia total** esas bolas necesitan viajar para llegar a 'i' (`rightOps`). TENIDO Symmetric al pase izquierdo, pero ahora moviéndose a la izquierda. Silencio
Silencio **Respuesta** Silencio `respuesta[i] = izquierdaOps[i] + derechaOps[i]` Silencio Todas las bolas a la izquierda más todas las bolas a la derecha – eso es exactamente el total de operaciones necesarias para llevarlas a todos a 'i'. Silencio

Ambos pases son `O(n)` y utilizan sólo espacio adicional constante.

### Proof of Correctness

Demostramos que el algoritmo es correcto por inducción sobre los dos pases.

#### Lemma 1
Después del paso izquierdo a derecha, por cada índice `i`:

- `leftCnt[i]` iguala el número de bolas en cajas `0 ... i‐1`.
- `leftOps[i]` iguala la suma de distancias que cada una de esas bolas debe viajar para llegar a la caja `i`.

*Proof by induction on `i`.*

- **Base (i=0).** No hay cajas a la izquierda.
`leftCnt[0] = 0`, `leftOps[0] = 0`. La lema sostiene.

- Paso inductivo. Supongamos que la lema contiene el índice I.
When moving to `i+1`:
* `leftCnt[i+1] = leftCnt[i] + (boxes[i]=='1'?1:0)` – añadimos la bola a `i` si existe.
* Cada bola que quedó de `i` ahora necesita un paso adicional para alcanzar `i+1`, por lo tanto `leftOps[i+1] = leftOps[i] + leftCnt[i].
Esto coincide con la definición de `leftCnt[i+1]` y `leftOps[i+1]`. ∎

#### Lemma 2
Analógicamente, después del paso derecho a izquierda, por cada índice `i`:
- `rightCnt[i]` iguala el número de bolas en cajas `i+1 ... n-1`.
- `rightOps[i] iguala la suma de distancias que cada una de esas bolas debe viajar para llegar a la caja `i`.

La prueba es simétrica a Lemma limitadanbsp;1.

##### Theorem
Por cada índice `i`, `answer[i] = leftOps[i] + rightOps[i] es el número mínimo de operaciones para recoger todas las bolas en el cuadro `i`.

*Proof. *
Todas las bolas a la izquierda de `i` contribuyen exactamente `leftOps[i]` se mueve (por Lemma 1) para traerlas a `i`.
Todas las bolas a la derecha de " yo " contribuyen exactamente a los movimientos `derecha[i] " (por Lemma 2).
Dado que los movimientos para las bolas izquierda y derecha son independientes (nunca interfieren), el costo mínimo total es la suma de los dos, es decir, `respuesta[i]`. ∎

-...

## 3. Aplicación en tres idiomas

A continuación se muestran implementaciones limpias y comentadas para **Java**, **Python**, y **C+**.
Cada versión sigue la misma lógica de dos pasos descrita anteriormente.

-...

### 3.1 Java

``java
*
* LeetCode 1769 – Número mínimo de operaciones para mover todas las bolas a cada caja
*
* Complejidad del tiempo: O(n)
* Complejidad espacial: O(1) (aparte de la matriz de salida)
*/
Solución de la clase pública {}
public int[] minOperations(String boxes) {
int n = box.length();
int[] response = new int[n];

// --- - Izquierda al Paso Derecha ---
int left Cnt = 0; // bolas izquierdas del índice actual
int left Ops = 0; // operaciones necesarias para llevar bolas izquierdas al índice actual
para (int i = 0; i)
respuesta[i] = izquierdaOps; // contribución izquierda hasta el momento
si (boxes.charAt(i) == '1'
izquierda Cnt++; // nueva bola aparece en i
}
izquierda Ops += leftCnt; // cada bola izquierda mueve un paso más para alcanzar i+ 1
}

// ----- Derecha a Paso Izquierdo ---
Intento derecho Cnt = 0;
Intento derecho Ops = 0;
para (int i = n - 1; i 0; i--) {
respuesta[i] += rightOps; // add right contribution
si (boxes.charAt(i) == '1'
derecho Cnt++;
}
derecho Ops += rightCnt; // cada bola derecha mueve un paso más para alcanzar i-1
}

respuesta de retorno;
}
}
`` `

-...

#### 3.2 Python

``python
# LeetCode 1769 – Número mínimo de operaciones para mover todas las bolas a cada caja
# Hora: O(n)
# Espacio: O(1) excluyendo la lista de resultados

def minOperaciones(boxes: str) - Lista de contactos[int]:
n = len(boxes)
respuesta = [0]

Izquierda a la derecha
left_cnt = 0 # número de bolas a la izquierda de i
left_ops = 0 # distancia total para esas bolas para llegar i
para i, ch in enumerate(boxes):
respuesta[i] = left_ops
si ch == '1':
left_cnt += 1
left_ops += left_cnt

# Right to left
right_cnt = 0
right_ops = 0
para i en rango(n - 1, -1, -1):
respuesta[i] += right_ops
si cajas [i] == '1':
right_cnt += 1
right_ops += right_cnt

respuesta
`` `

-...

### 3.3 C++

``cpp
*
* LeetCode 1769 – Número mínimo de operaciones para mover todas las bolas a cada caja
*
* Complejidad: O(n) tiempo, O(1) espacio extra (además del vector de salida)
*/
Incluido el título
#include ■string

Clase Solución {
public:
std:::vector obtenidosint confianza minOperations(cont std::string curvas cajas) {
int n = box.size();
std::vector garantizadoint edad answer(n, 0);

// Izquierda a derecha
int left Cnt = 0; // bolas izquierdas del índice actual
int left Ops = 0; // distancia suma para esas bolas al índice actual
para (int i = 0; i) {}
respuesta[i] = izquierda Ops;
(boxes[i] == '1') izquierda Cnt++;
izquierda Opciones += izquierda Cnt;
}

// Derecho a la izquierda
Intento derecho Cnt = 0;
Intento derecho Ops = 0;
para (int i = n - 1; i 0; --i) {
respuesta[i] += derecho Ops;
(boxes[i] == '1'. Cnt++;
derecho Ops += rightCnt;
}

respuesta de retorno;
}
};
`` `

-...

## 4. Artículo del Blog – “El Bien, el Mal y el Ugly” de Moving Balls a Boxes

#### 4.1 Introducción

“Una entrevista de trabajo no es sólo sobre su código, es sobre cómo piensas.”*
■ En entrevistas técnicas, problemas como **1769 – Número mínimo de operaciones para mover todas las bolas a cada caja** son comunes. Prueban su capacidad para convertir un rompecabezas aparentemente combinatorio en un algoritmo de tiempo lineal.
■ A continuación, diseccionamos el problema, exploramos sus fortalezas y trampas, y presentamos una solución limpia y lista para la producción en Java, Python y C++.
■ Al final, podrás entrar en una entrevista, explicar tu razonamiento y codificar la respuesta en minutos.

-...

### 4.2 The Good – Why Este problema es una pregunta de la entrevista de estrellas

1. **Claridad del objetivo* *
El objetivo – *move todas las bolas a una caja de destino* – es cristalino. No hay truco oculto; sólo tienes que contar distancias.

2. ** Subestructura óptima**
El problema naturalmente se descompone en mitades *izquierda* y *derecha*. Eso revela una solución DP/prefix‐sum limpia.

3. ** Posibilidad de tiempo libre* *
Con un enfoque de dos pasos, la solución se ejecuta en `O(n)`, cumpliendo las limitaciones (`n ≤ 2000`) fácilmente.

4. **Hands‐On Practice* *
Te obliga a pensar en *sumas prefijos* y *operaciones acumulativas*, conceptos que aparecen en muchas entrevistas (por ejemplo, "Suspiraciones mínimas para agrupar todos los 1's Together", "Operaciones mínimas para reducir un número").

5. **Relevancia en idioma corsé* *
El algoritmo es lenguaje-agnóstico. Usted puede demostrarlo en Java, Python, C++, o incluso JavaScript – una gran manera de mostrar versatilidad.

-...

### 4.3 El malo – Pitfalls comunes y malentendidos

Silencio Pitfall Silencio Lo que sucede Silencioso
Silencio--------------------------
Silencio **Retirar “move one ball” como “teleportation”** Silencio Resumiendo incorrectamente distancias sin tener en cuenta el costo incremental. Use sumas prefijas para acumular *distancia* por bola, no sólo contar. Silencio
Silencio **O(n2) Simulación** Silencio Mover cada bola individualmente a cada objetivo conduce a 2 millones de operaciones para 'n=2000`. tención Reconoce que las distancias añaden linealmente; usa dos pases en su lugar. Silencio
Silencio **Off‐by‐One Errores** ← Errores de error 0‐basado frente a índices 1-basados cuando computar los índices izquierdo/derecho. Silencio Mantenga un contador de funcionamiento que comienza en 0 y actualizaciones ** después de procesar el índice actual. Silencio
Silencio **Space Mis-estimation** tención Usando un array extra por pase (leftCnt, leftOps) y olvidando fusionarlos. Silencio Sólo mantén el array de respuesta final; los contadores intermedios son escalares. Silencio

-...

### 4.4 The Ugly – Edge Cases You might Overlook

1. *Todos los Cero* – Si no existen bolas, cada `respuesta[i]`. debería ser `0`. El algoritmo maneja esto con gracia porque los contadores permanecen en 0.

2. **Single Box** – Con `n=1`, el resultado es `[0]`. Los pases corren una vez y no añaden nada.

3. **La longitud máxima** – `n=2000` sigue siendo trivial para `O(n)`, pero debe probar con cadenas grandes al azar para asegurar que no se desborde (utilizar `int` – la suma máxima es `2000 * 2000 = 4,000,000`, con seguridad dentro de 32 bits).

4. **No-ASCII caracteres** – La declaración del problema garantiza sólo `'0'` o `'1'. Sin embargo, validar la entrada defensivamente en el código de producción es una buena práctica.

-...

### 4.5 Código Final – Listo para la Producción

A continuación encontrará las implementaciones finales, comentadas en **Java**, **Python**, y **C+**. Cada versión:

- Corre en el tiempo `O(n)`, `O(1)` espacio adicional.
- Maneja todos los casos de borde.
- Está autocontenido y listo para copiar en un entorno de entrevista.

``java
// Java
Solución de la clase pública {}
public int[] minOperations(String boxes) {
int n = box.length();
int[] ans = nuevo int[n];
int leftCnt = 0, left Ops = 0;
para (int i = 0; i)
ans[i] = izquierda Ops;
si (boxes.charAt(i) == '1') izquierda Cnt++;
izquierda Opciones += izquierda Cnt;
}
int rightCnt = 0, rightOps = 0;
para (int i = n - 1; i 0; i--) {
ans[i] += derecho Ops;
si (boxes.charAt(i) == '1'. Cnt++;
derecho Ops += rightCnt;
}
devolver los ans;
}
}
`` `

``python
# Python
def minOperaciones(boxes: str) - Lista de contactos[int]:
n = len(boxes)
a)
left_cnt = left_ops = 0
para i, ch in enumerate(boxes):
ans[i] = left_ops
si ch == '1': left_cnt += 1
left_ops += left_cnt
right_cnt = right_ops = 0
para i en rango(n-1, -1, -1):
ans[i] += right_ops
si cajas [i] == '1': right_cnt += 1
right_ops += right_cnt
Retorno
`` `

``cpp
// C++
Clase Solución {
public:
vector asignadoint confianza minOperations(cont cordones iguales) {
int n = box.size();
vector:
int leftCnt = 0, left Ops = 0;
para (int i = 0; i) {}
ans[i] = izquierda Ops;
(boxes[i] == '1') ++leftCnt;
izquierda Opciones += izquierda Cnt;
}
int rightCnt = 0, rightOps = 0;
para (int i = n - 1; i 0; --i) {
ans[i] += derecho Ops;
(boxes[i] == '1') + + derecho Cnt;
derecho Ops += rightCnt;
}
devolver los ans;
}
};
`` `

-...

### 4.6 Takeaway

- **Explicar la intuición** – sumas prefijo + dos pases.
- **Demuestra el algoritmo** – escribe código lineal y limpio en el idioma con el que estás cómodo.
- **Mostrar confianza con los casos de borde** – mencionar “todos los ceros” o “single box” explícitamente.

■ *“Cuando conviertes un problema en un simple truco de matemáticas, no solo estás resolviendo el problema; estás mostrando maestría.”*
■ Buena suerte: ¡las cajas estarán listas para aceptar tu solución en segundos!

-...

### 5. Pensamientos de clausura

Problemas de masterización como **1769** es más que una codificación; se trata de *architecting* una solución que es:

- Correcta** - probada por teoremas y lemas.
- **Eficiente** – `O(n)` corre cómodamente bajo cualquier límite de tiempo de entrevista.
- **Elegant** – una estrategia prefijo de dos pasos que se puede escribir en menos de 30 líneas de código.

Al estudiar lo bueno, reconociendo lo malo, y preparándose para lo feo, puede convertir cada entrevista en una oportunidad para mostrar tanto su perspicacia algorítmica como su fluidez de codificación. ¡Feliz codificación!