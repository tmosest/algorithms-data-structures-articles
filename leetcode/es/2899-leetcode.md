-...
Título: LeetCode 2899. Últimas entradas visitadas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 2899 – **Últimos enteros visitados**
## Easy – Java tención Python ← C++ Soluciones + In‐Depth Blog Post

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

Se le da un array entero `nums`.
- Un entero positivo** representa un “visit” y debe ser recordado.
- `-1` es una pregunta: usted tiene que devolver el *k‐th* más recientemente recordado entero, donde `k` es el número de consecutivos `-1`s visto hasta ahora (incluyendo el actual).
- Si `k` es más grande que el número de números recordados, regrese `-1`.

La salida es una lista de enteros producidos por todas las consultas `-1`.

**Constraints* *
- `1 ≤ nums.length ≤ 100`
- `nums[i] == -1` o `1 ≤ nums[i] ≤ 100`

-...

## 🔧 2ف⃣ Optimal Solution (O(n) time, O(n) space)

La visión clave:

Silencio Lo que hacemos .
Silencio----------------------
Silencio **Push** Silencio Almacene cada entero positivo en un *stack* (último, primero). Silencio Siempre necesitamos las visitas más recientes. Silencio
Silencio **Reset** Silencio Cuando nos encontramos con un número positivo, reajuste el contador consecutivo-`-1`. Silencio `k` sólo cuenta con consecutivos `-1`s. Silencio
Silencio **Query** Silencio En `-1`, aumentar el contador. Si el contador ≤ tamaño de la pila, devuelva el elemento en `stack.size() - counter`; de lo contrario devuelva `-1`. Silencio `stack.size() - contra` apunta al entero más reciente *k‐th*. Silencio

Esto da un algoritmo limpio de un paso.

-...

## 📦 3VIEW⃣ Code Implementations

■ **Nota:** Los tres fragmentos compilan y corren en la plataforma LeetCode.

### 3.1 Java

``java
importa java.util. ArrayList;
importa java.util. Lista;

Solución de la clase pública {}
public List won(int[] nums) {
Lista realizadaInteger confía ans = nuevo ArrayList correctamente();
Lista Nombramiento de entrada = nuevo ArrayList correctamente(); // actúa como una pila

int consec = 0; // consecutivo -1 contador

para (int num : nums) {
(num == -1) {
consec++; // another -1 in a row
si (consec <= stack.size()) {}
// k-th más reciente - título stack.size() - k
as.add(stack.get(stack.size() - consec));
. ♫ ... {
ans.add(-1);
}
. ♫ ... {
stack.add(num); // push new visit
consag = 0; // restablecer contador consecutivo
}
}
devolver los ans;
}
}
`` `

#### 3.2 Python

``python
de la importación Lista

Solución de clase:
def last Visitadas Integers(self, nums: List[int]) - List[int]:
ans = []
pila = [] # visitas recientes
consiguiente = 0 # consecutivo -1 contador

para las numidades:
si num == -1:
consiguiente += 1
si consiguiente = len(stack):
ans.append(stack[-consec]) # kth most recent
más:
ans.append(-1)
más:
stack.append(num)
consag = 0
Retorno
`` `

### 3.3 C++

``cpp
Incluido el título
usando std namespace;

Clase Solución {
public:
vector implicado por última vez VisitadoIntegers(vector realizadoint limitada nums) {
vector significar uns
vector asignadoint edad pila; // visitas recientes
int consec = 0; // consecutivo -1 contador

para (int num : nums) {
(num == -1) {
++consec;
si (consiguiente)
ans.push_back(stack[stack.size() - consec]); // k-th most recent
más
ans.push_back(-1);
. ♫ ... {
stack.push_back(num);
consag = 0;
}
}
devolver los ans;
}
};
`` `

-...

##  Mensaje del Blog – “El Bien, el Mal y el Ugly” de los últimos números visitados

#### 🏁 Introducción

Al prepararse para una entrevista de ingeniería *software*, es común encontrar problemas de “estatalización”. *LeetCode 2899 – Últimas entradas visitadas* es uno de esos problemas que prueba su capacidad para mantener una historia dinámica mientras se manejan las consultas. En este artículo, vamos a diseccionar el problema, caminar a través de una solución limpia, resaltar el bien, los malos, y los aspectos feos, y terminar con las ideas amigables de SEO para ayudarle a aterrizar esa llamada de entrevista.

-...

### llevándose el bien - ¿Por qué Este problema importa

¦ Feature Silencio Por qué es útil
Silencio...
tención **Administración Estatal** ← Aplicaciones del mundo real (por ejemplo, navegación, pilas de deshacer) necesitan recordar acciones pasadas. Silencio
Silencio **One‐Pass Algorithm** Silencio Demuestra cómo resolver requisitos complejos con el tiempo O(n). Silencio
Silencio **Edge‐Case Handling** Silencio te enseña a pensar en restablecimientos, consultas consecutivas y estados vacíos. Silencio
tención **Cross‐Language Implementation** Silencio Showcases adaptability in Java, Python, and C++. Silencio

Dominar este problema demuestra que puede diseñar estructuras de datos eficientes y manejar habilidades de estado mutable—cruciales para cualquier rol de backend o sistemas.

-...

## ## Глали los malos – saltos comunes

1. **Indización confusa** – Recuerde que el “k‐th más reciente” es *stack.size() – k* (no *k - 1*). Los errores fuera por uno son la razón principal para una respuesta incorrecta.
2. **Forgetting Reset** – El contador consecutivo `-1` debe reasentarse cuando aparezca un número positivo. Descubriendo que esto produce resultados incorrectos para insumos como `[1, -1, 2, -1]`.
3. **Using `pop()` for Queries** – Muchos principiantes accidentalmente aparecen la pila en cada '-1', destruyendo la historia. La pila debe ser sólo para preguntas.
4. **Ignorando a los Estados Vacíos** – Si usted ve `-1' antes de cualquier número positivo, debe regresar `-1` en lugar de acceder a un índice inválido.

-...

### 👿 The Ugly – Suboptimal Approaches

TENCIÓN ANTERIOR Lo que es incorrecto
Silencio------------
Silencio **Dos-D Array of All Queries** Silencio O(n2) memoria, innecesaria. Silencio
Silencio **Reconstrucción de la historia en cada consulta** Silencio O(n2) tiempo; usted atraviesa el array de nuevo por cada `-1`. Silencio
Silencio ** Lista enlazada con la inserción de la cabeza** Silencio Obras pero añade sobrecabeza puntero adicional; no tan limpio como vector/ArrayList. Silencio
Silencio **Using Recursion for Queries** Silencio El riesgo de desbordamiento de Stack sobre grandes insumos; sobrekill for a simple linear scan. Silencio

Estos patrones son tentadores si usted está apuntando a "quick fixes", pero rompen la escalabilidad y la legibilidad—calidades que los entrevistadores odian.

-...

#### 📈 Complexity Analysis

Silencioso Complejidad
Silencio--------------------------
Silencio **Hora** Silencio O(n) – pase único sobre el array. Silencio
Silencio **Espacio** Silencioso O(n) – el peor de los casos todos los números son positivos, así que los almacenamos todos. Silencio

Esta solución lineal golpea la tabla líder en LeetCode (≤ 1 ms en Java, Python, C++ en hardware estándar).

-...

Consejos prácticos para la entrevista

1. **Explicar su estructura de datos** – Mención de que una pila mantiene visitas recientes, y una pista de contrapeso consultas consecutivas.
2. **Edge Cases** – Discuss scenarios like leading `-1`s, trailing `-1`s, and alternating positive/negative patterns.
3. **Por qué no `pop()`** – Aclarar que las consultas se leen solamente, preservando la historia para futuras consultas.
4. **Proceso de Pensamiento en Idiomas** – Mostrar cómo el mismo algoritmo se adapta a Java, Python y C++ (array/vector vs. list vs. std::vector).
5. **Tiempo-Space Trade‐Off** – Si el entrevistador pide optimización, señala que O(n) es óptimo; no puedes mejorarlo porque debes examinar cada elemento al menos una vez.

-...

### 🎯 SEO Lista de verificación (Para los entrenadores profesionales)

*LeetCode 2899, Last Visited Integers, problema de seguimiento estatal, algoritmo de paso único, pregunta de entrevista, solución Java, solución Python, solución C+*
- **Meta Descripción**: “Solve LeetCode 2899 – Últimas entradas visitadas en Java, Python y C++. Algoritmo de paso único con lógica de pila clara. Lea el blog completo para las trampas y consejos de entrevista. ”
- **Header Tags**: H1 (`LeetCode 2899 – Last Visited Integers`), H2 (`Problem Recap`, `Optimal Solution`, `Code Implementations`, ``Blog Post - The Good, The Bad, and The Ugly`), H3 (`Java ' , `Python`, `C+++ ' ), H4 (Análisis complejo ' ).

Estas etiquetas ayudan a los motores de búsqueda indexar el post y coincidir con las consultas relacionadas con entrevista.

-...

#### 🎯 Closing Thought

Si se puede articular por qué una simple pila + contador es la solución *derecha* y cómo se evitan las trampas típicas, se demostrará una maestría de estructuras de datos **estatales** — un sello distintivo de un desarrollador de alto nivel. Este problema es pequeño en LeetCode, pero los conceptos que prueba son enormes en el mundo real.

¡Buena suerte en tu próxima entrevista! Si encontró útil este artículo, compartalo en LinkedIn o Twitter y etiqueta **@YourCompany** para que los reclutadores vean su experiencia en acción. 🚀

-..