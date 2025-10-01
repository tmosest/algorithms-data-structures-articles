-...
Título: LeetCode 1474. Borrar N Nodos Después de M Nodos de una Lista Vinculada -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🎯 **LeetCode 1474 – Delete N Nodes After M Nodes of a Linked List* *
■ *Una solución limpia, en el lugar O(n) en **Java**, **Python**, y **C+** + una publicación de blog lista para entrevistas. *

-...

## Tabla de contenidos
1. [Norma general](#problema vista previa)
2. [Por qué importa](#why-it-matters)
3. [Naïve Ideas (The Bad & Ugly)](#naïve-ideas)
4. [La solución óptima (la buena)] (solución óptima)
5. [Code Walk‐through](#code-walkthrough)
* [Java](#java)
* [Python](#python)
* [C++](#c-plus-plus)
6. [Análisis de complejidad](#complejidad)
7. [Casos de Edge & Pitfalls comunes] (casas de borde)
8. [Siguiente-Up: In‐Place vs. Extra Space](#siguiente-up)
9. [Entrevista consejos " trucos](#interview-tips)
10. [lista de verificación SEO " Palabras clave](lista de verificación de datos)
11. [Conclusión " Pensamientos finales](#conclusión)

-...

## יa name="problem-overview"

■ **Delete N Nodes After M Nodes of a Linked List* *
■ **LeetCode #1474** – *Easy*

Se le ha dado una lista de **singly-linked** y dos números enteros `m` y `n`.
Partiendo de la cabeza, guarde los primeros 'm` nodos, elimine los próximos `n` nodos, luego repita hasta el final de la lista.
Devuelve la cabeza de la lista modificada.

*Ejemplo*
`` `
Input: head = [1,2,3,4,5,6,7,8,9,10,11,12,13], m = 2, n = 3
Producto: [1,2,6,7,11,12]
`` `

**Constraints* *
- 1 0 0 0 nodos
- `1 ' = val ' = 10^6`
- `1 0 = m, n

-...

## יa name="why-it-matters" #1⁄4]

- **Maestría de Listas Enlazadas** – La mayoría de las entrevistas técnicas le piden que manipule directamente a los punteros.
- ¿Qué? El problema pide explícitamente una solución **en lugar** (O(1) extra space).
- **Eficiencia del tiempo** – Un solo paso a través de la lista (O(n) tiempo) es la solución ideal.

Dominar este problema demuestra que usted entiende:
- Traversal puntero
- Manejo de caso de borde
- Estructura de código limpio (cabeza de muñeca, bucles vs recursión)

-...

## יa name="naïve-ideas" #1⁄4] Naïve Ideas (The Bad & Ugly)

Silencio Idea Silencio Por qué Es Malo Silencioso Toca
...--------------------------
Silencio **Recusión** Silencio Cada llamada utiliza espacio de pila → O(n) espacio Silencio `deleteNodes(head)` se llama dentro del bucle de eliminación, volando la pila en grandes listas
Silencio **Dos pasos** Silencio Primero pasar a contar, segundo paso a eliminar → todavía O(n) pero desperdicio vivir bucle extra, complejidad innecesaria ¦
Silencio **Conversión de Array** Silencio Convertirse en array → O(n) memoria extra ← Perder propiedades enlazadas, no “en lugar”

■ **Takeaway** – Mantenlo lineal, puntero solo, y un solo paso.

-...

## Identificar un nombre="optimal-solution" especificado/a título4] La solución óptima (el bien)

1. **Use una cabeza mutilada** – simplifica los casos de borde cuando se elimina la cabeza misma.
2. **Mantenga dos puntos**:
- `prev` - el último nodo que permanece después de una ronda de eliminación.
- `curr` - el nodo que estamos inspeccionando actualmente.
3. # Loop #
- Avance `prev ' and `curr` `m` steps (keep the nodes).
- Avance `curr `n` pasos (deletrear los nodos).
- Enlace `prev-ientenext = curr`.
4. **Parar** cuando `curr ' se convierte en `NULL ' .

Todos los pasos son **O(1) per node**, por lo que el tiempo total es **O(n)** y el espacio **O(1)**.

-...

## יa name="code-walkthrough"

A continuación se presentan implementaciones limpias y listas de producción en los tres principales idiomas de entrevista.

### ## ## ## ## #1 se hizo un nombre="java"

``java
*
* Definición para lista enlazada.
* Public class ListNode {}
* int val;
* ListNode next;
* ListNode() {}
* ListNode(int val) { this.val = val; }
* ListNode(int val, ListNode next) { this.val = val; this.next = next; }
*
*/
Clase Solución {
public ListNode deleteNodes(ListNode head, int m, int n) {
// Nodo tonto para manejar las eliminaciones en la cabeza
ListNode dummy = nuevo ListNode(0);
dummy.next = head;

ListNode prev = dummy; // último nodo que permanece
ListaNodo curr = cabeza; // nodo actual en la lista

mientras (currir != null) {
Mantener los nodos
para (int i = 0; i) null; i+) {
prev = curr;
curr = curr.next;
}

// 2 Eliminar los nodos
para (int i = 0; i < n " curr != null; i++) {
curr = curr.next;
}

// 3down Conectar la parte guardada a la siguiente parte guardada
prev.next = curr;
}

Devolver el tonto.
}
}
`` `

### ## ## ## ## ## ## Asignado="python" Python

``python
class ListNode:
def __init__(self, val=0, next=None):
self.val = val
self.next = next

def deleteNodes(head: ListNode, m: int, n: int) - título ListNode:
# Nodo tonto #
prev, curr = muñeco, cabeza

mientras que curr:
# Mantén los nudos #
para _ en rango(m):
si curr es Ninguno:
descanso
prev, curr = curr, curr.next

# Delete n nodes
para _ en rango(n):
si curr es Ninguno:
descanso
curr = curr.next

# Link
prev.next = curr

Regresa el tonto.
`` `

### ## ## ## #1 seleccion="c-plus-plus"

``cpp
*
* Definición para lista enlazada.
* struct ListNode {}
* int val;
* ListNode *next;
* ListNode(int x) : val(x), next(nullptr) {}
* };
*/
Clase Solución {
public:
ListNode* deleteNodes(ListNode* head, int m, int n) {
ListNode dummy(0);
dummy.next = head;
ListNode *prev = ' dommy, *curr = head;

mientras (curr) {
// Mantén los nudos
para (int i = 0; i) {}
prev = curr;
curr = curr-ientenext;
}

// Borrar los nodos
para (int i = 0; i) {}
curr = curr-ientenext;
}

// Connect
prev-Connext = curr;
}

Devolver el tonto.
}
};
`` `

-...

## יa name="complexity"

TEN TERRITOR TEN Java / Python / C++ ANTE ANTERIOR Explicación
Silencio--------------------------------
Silencio **Hora** Silencio **O(n)** Silencio Cada nodo es visitado un número constante de veces (en la mayoría de `m + n` pero `m + n ≤ 2000`). Silencio
Silencio **Espacio** Silencio **O(1)** Silencio Sólo unos pocos punteros + cabeza de muñeco; ningún array auxiliar o pilas de recursión. Silencio

⇩ La solución óptima satisface perfectamente el requisito “en lugar”.

-...

## יa name="edge-cases" #1⁄4]

Silencio Caso Silencio Lo que sucede Silencioso Fijar / Código Defensivo
Silencio----------------------------
Silencio No hay eliminación, sólo devuelve la lista original ← El bucle interior simplemente salta, el código todavía funciona ¦
Silencio 0** (inválido por las limitaciones) Silencio perdería la lista completa Silencio `for (int i=0; i)m; ++i)` no hace nada → `prev` se queda muñeco, lo que conduce a la lista vacía
Silencio **Lista más corto que m** Silencio Mantener todo Silencioso exterior `mientras (curr)` termina temprano; no se produce la eliminación
Silencio **Lista más corto que n después de mantener** vivir Eliminar al final Silencio Inner `for` cheques de bucle `curr != nullptr` antes de avanzar Silencio
Silencio **La eliminación toca la cabeza** Silencio Manejado por la cabeza sodomizada Silencio `prev` comienza en el muñeco, por lo que `prev.next = curr` puede saltar la cabeza original

■ **Tip** – Siempre prueba con `m = 1`, `n = 1`, `m = n = 0` (si el juez pierde las limitaciones).

-...

## יa name="seguir-up" Login/a Conf8️ Follow‐Up: In‐Place vs. Extra Space

**Pregunta:** *¿Podemos resolver esto con **O(n)** memoria extra (por ejemplo, construyendo un array o copiando nodos)? *
**Respuesta:** Absolutamente – simplemente conviértete a un array o usa un ayudante recursivo, pero pierdes el borde “en lugar” que la pregunta quiere explícitamente.
¿Por qué permanecer en el lugar? * *
- Las entrevistas a menudo prueban si puede *reutilizar* la estructura existente sin asignar nuevos nodos.
- En el código del mundo real, usted querría evitar una copia de memoria para el rendimiento y la previsibilidad.

-...

# ## יa name="interview-tips" #1⁄4]

Silencioso Pregunta  Your Talking Point Silencio Código‐Ready Respuesta
Silencio--------------... la vida...
Silencio “¿Y si ‘n’ es 0?” Silencioso “Simplemente mantenemos todos los nodos de `m`; el lazo de eliminación se salta.” Silencio Mostrar que el bloque `para (int i = 0; i) se ejecuta cero veces. Silencio
Silencio “¿Puedes hacerlo recursivamente?” Para una lista de 10 000 nodos, es un flujo de pila”. ← Ofrezca la solución iterativa primero, luego discuta la recursión sólo como una alternativa teórica. Silencio
Silencio “¿Por qué la cabeza del muñeco?” tención Mención que también garantiza 'prev- rationext' siempre es válida. Silencio
Silencioso “La complejidad?” Silencio Camina por los dos lazos anidados: cada nodo se procesa un número constante de veces. Silencio

**STAR Method** – *Situation, Task, Action, Result*
- **Situación**: “Me pidieron que eliminara todos los nodos después de mantener los nodos. ”
- **Task**: "Revisar la lista una vez y modificarla en su lugar. ”
- **Acción**: "Usó un nodo tonto, dos punteros, y dos simples lazos. ”
** Resultado**: “O(n) time, O(1) space, no extra allocations. ”

-...

♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪ ♪♪ Lista de verificación SEO

Silencio Categoría Silencio Palabra clave Por qué importa
Silencio...
Silencio **Problema Título** Silencio “LeetCode 1474 Eliminar N Nodos Después de M Nodes” Silencio Los buscadores a menudo escriben el número exacto del problema. Silencio
Silencio **Entrevista Focus** Silencio “Pregunta de entrevista de lista enlazada”, “deslección de lista en el lugar vinculado” Estas son las frases de los reclutadores tipo. Silencio
Silencio **Idiomas** Silencioso “Solucion Java”, “Solución Pitón”, “Solución C++” Silencio Permite que cada idioma aparezca en resultados de búsqueda separados. Silencio
Silencio **Complejidad** Silencio “O(n) time linked list solution”, “constant space”  WordPress Programador busca un código eficiente. Silencio
Silencio **Extras** Silencio “Java Python C++ soluciones”, “entrevista de algoritmo” Silencio Broadens el alcance. Silencio

■ **Google‐style Meta‐Tags* *
" html "
Identificar el título "LeetCode" 1474 – Eliminar los nodos después de los nodos M (Java, Python, C++)
√≥ יmeta name="description" content="Clean, in‐place O(n) solution to LeetCode 1474 – Eliminar N Nodos Después de M Nodos de una Lista Vinculada. Java, Python, y C++ de código + guía de entrevista."
" `

-...

## יa name="conclusión" Login/a título10️ Conclusion > Final Thoughts

TENIDO TENIDO ANTERIOR **Lo que aprendió**
Silencio...
Silencio 🔧 ← Manipulación de punteros Mastered en una lista de cantos. Silencio
Silencio 📦 Silencio Entregado un algoritmo **en lugar** (O (1) espacio). Silencio
TENIDO SONIDO TENIDO Achieved a single‐pass O(n) time complex. Silencio
Silencio 🗣Ω Silencio Comunicó la solución claramente en **Java**, **Python**, y **C+** – los tres idiomas que los reclutadores aman. Silencio
Нели не ный evitado recursión y trampas de dos pasos – los enfoques “malos”. Silencio

■ ** Consejo final** – Durante la entrevista, *hablar a través de la idea de la cabeza del muñeco primero*. La mayoría de los entrevistadores les encanta ver que piensa en casos de borde antes de escribir código.

¡Feliz codificación y buena suerte aplastando tu próxima entrevista! 🚀

-...

### 📌 Código de referencia rápida (Todos los idiomas)

``text
Java:
dummy → prev → curr
para m pasos: prev = curr; curr = curr.next;
para n pasos: curr = curr.next;
prev.next = curr;

Python / C++ (la misma lógica)

`` `

Siéntete libre de copiar, pegar y ejecutar estos snippets en tus propios arnés de prueba o jueces en línea. ¡Feliz piratería!