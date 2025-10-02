-...
Título: LeetCode 25. Nodos inversos en k-Group -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 Retrocede Nodos en K‐Group – Una guía completa (Java ¦

■ **Palabras clave:** Nodos inversos en K-Group, LeetCode 25, Lista enlazada, Entrevista, Java, Python, C++, O(1) space, Recursion, Iteration

-...

Introducción

Las listas vinculadas son un elemento básico de las entrevistas técnicas.
**Nodos reversos en K‐Group** (LeetCode 25) es un problema clásico “medium‐hard” que prueba su capacidad de:

* Manipular punteros cuidadosamente
* Casos de borde de mano (menos de *k* nodos izquierdos)
* Optimize for O(1) extra space

La solución es a menudo un punto de inflexión entre un candidato sólido y un “justo pasado” uno. Este artículo te lleva a través del **bueno**, el **bad**, y las partes **enormemente** del problema, y proporciona código limpio y listo para la producción en **Java, Python, y C++**.

-...

### 2down⃣ Problem Statement (Simplified)

■ Dada una lista enlazada, revierte los nodos **k** a la vez y devuelve la lista modificada.
■ *Si el número de nodos no es un múltiplo de k, los nodos restantes permanecen en orden original. *

``text
Entrada: 1 - título 2 - título 3 - título 4 - título 5, k = 2
Producto: 2 - título 1 - título 4 - título 3 - título 5
`` `

Constraints:

* 1 ≤ ≤ n ≤ 5000
* 0 ≤ Nodo.val ≤ 1000

-...

### 3VIEW⃣ Analysis ' Strategy

Silencio Silencio Silencio Silencio
Silencio...
Silencio **Bien** – El problema se reduce a *“reverse every sub‐segment of size k”*. Silencio **Bad** – Off‐by-one errores en las actualizaciones de puntero son comunes. Silencio

La operación central es **in-place reversal** de un sub-segment.
Tenemos dos patrones populares:

1. **Recursivo** – limpio e intuitivo, pero O(n) apilar espacio.
2. **Iterante con cabeza de muñeco** – O(1) memoria extra, ligeramente más verbosa pero perfecta para entrevistadores que se preocupan por el espacio.

Ambos patrones comparten un ayudante que encuentra el nodo *k‐th* desde un comienzo dado y una rutina que revierte punteros entre dos nodos.

-...

### 4down So Solution Walk-through

#### 4.1 Helper: Find k‐th Node

``text
start - título 1 - título 2 - título 3 - título 4 - título 5
k = 3
`` `

Partiendo de `start`, mueva `k` pasos.
Si alcanzamos `null` antes de tomar 'k' pasos, el segmento es demasiado corto.

##### 4.2 Revertir un segmento

Revertimos los punteros entre " cabeza " (inclusiva) y " cola " (exclusiva).
Típico enfoque de tres puntos:

`` `
prev = null
cur = cabeza
mientras se cura!= cola:
nxt = cur.next
cur.next = prev
prev = curro
cur = nxt
retorno prev // nuevo jefe de segmento inverso
`` `

##### 4.3 Algoritmo iterativo (O(1) space)

1. Crear un nodo tonto apuntando a 'cabe'.
2. `groupPrev` = dummy.
3. Si bien es cierto:
* Find `k`‐th node after `groupPrev`. Si ninguno → romper.
* `groupNext` = `kth.next`.
* Retrocede de `groupPrev.next` hasta `groupNext`.
* Reconnect:
* `groupPrev.next` = `kth` (new head)
* `oldHead.next` = `groupNext `
* Move `groupPrev` to `oldHead` ( which becomes the tail of the reversed segment).
4. Regresar `dummy.next`.

-...

#### 5down⃣ Complejidad

TEN TERRITOR TEN ANTE Recursion ANTE
Silencio--------------------------------
TENIDO Tiempo ANTERIOR O(n) ANTERIOR O(n)
TENIDO EL ESPACIO TENIDO O(n/k) (stack)

-...

### 6VIEW⃣ Code

#### 6.1 Java (Iterative)

``java
*
* Definición para lista enlazada.
* class ListNode {}
* int val;
* ListNode next;
* ListNode(int x) { val = x; }
*
*/
Solución de la clase pública {}
public ListNode reverse KGroup(ListNode head, int k) {
si (cabeza == null Silencioso k == 1) cabeza de retorno;

// Nodo tonto para manejar los cambios de cabeza
ListNode dummy = nuevo ListNode(0);
dummy.next = head;
ListNode groupPrev = dummy;

mientras (verdad) {
// Encuentra el nudo k-th
ListNode kth = getKthNode(groupPrev, k);
(kth == null) break;
ListNode groupNext = kth.next;

// Invierte este grupo
ListNode prev = kth.next;
ListNode cur = groupPrev.next;
mientras (curre != grupoSiguiente) {}
ListNode tmp = cur.next;
cur.next = prev;
prev = cur;
cur = tmp;
}

// Reconnect
ListaNodo tmp = grupoPrev.next; // la cabeza vieja se convierte en cola
grupoPrev.next = kth; // nueva cabeza
grupoPrev = tmp; // pasar al siguiente grupo
}

Devolver el tonto.
}

// Devuelve el nudo k-th desde el principio, o null si no son suficientes nodos
nodo getKthNode(ListNode start, int k) {
(start!= null " 0) {
start = start.next;
k...
}
Inicio de retorno;
}
}
`` `

#### 6.2 Python (Iterative)

``python
Definición para la lista ligada al canto.
class ListNode:
def __init__(self, val=0, next=None):
self.val = val
self.next = next

Solución de clase:
def reverse KGroup(self, head: ListNode, k: int) - ListNode:
si no cabeza o k == 1:
cabeza de retorno

dummy = ListNode(0, head)
group_prev = dummy

Mientras Verdadero:
kth = self.get_kth_node(group_prev, k)
si no kth:
descanso
group_next = kth.next

# Grupo inverso
prev, cur = kth.next, group_prev.next
mientras se cura!= group_next:
nxt = cur.next
cur.next = prev
prev = curro
cur = nxt

# Reconnect
tmp = group_prev.next
group_prev.next = kth
group_prev = tmp

Regresa el tonto.

def get_kth_node(self, start: ListNode, k: int) - título ListNode:
mientras comienza y k:
start = start.next
k -= 1
Inicio de retorno
`` `

#### 6.3 C++ (Iterante)

``cpp
/* Definición para lista enlazada. */
struct ListNode {}
int val;
ListNode *next;
ListNode(int x) : val(x), next(nullptr) {}
};

Clase Solución {
public:
ListNode* reverseKGroup(ListNode* head, int k) {
si 1) cabeza de retorno;
ListNode dummy(0);
dummy.next = head;
ListNode* groupPrev = >

mientras (verdad) {
ListNode* kth = getKthNode(groupPrev, k);
si (kth) romper;
ListaNodo* grupoSiguiente = kth- rationext;

// Inversión
ListaNodo* prev = grupoSiguiente;
ListNode* cur = groupPrev- rationext;
mientras (curre != grupoSiguiente) {}
ListNode* nxt = cur- rationext;
cur-ientenext = prev;
prev = cur;
cur = nxt;
}

// Reconnect
ListaNodo* tmp = grupoPrev- rationext; // cabeza vieja
grupoPrev- rationext = kth; // nueva cabeza
grupoPrev = tmp; // pasar al siguiente grupo
}
Devolver el tonto.
}

privado:
ListNode* getKthNode(ListNode* start, int k) {
(start ' k) {
start = start-ientanext;
k;
}
Inicio de retorno;
}
};
`` `

-...

### 7down⃣ Common Pitfalls > Cómo evitarlos

Silencio Pitfall Silencio Por qué Sucede
Silencio...
Silencio **Off‐by-one** cuando se encuentra el nodo kth ← Moving k times from `group Prev` puede devolver `null` incluso si el segmento es válido. Usar un bucle *dummy* y **strict** (`mientras (k-- 0)`) para asegurar la cuenta correcta. Silencio
Silencio **Dangling pointer** después de reversal tención Olvidando establecer `groupPrev.next` antes del bucle. TEN siempre volver a conectar el grupo después de la inversión; utilizar variables temporales. Silencio
Silencio **Profundidad de la recusión** Silencio k = 1 ⇒ cada llamada procesa un nodo → n llamadas. TEN Preferir solución iterativa si los entrevistadores mencionan espacio O(1). Silencio
Silencio **Modificación de la lista de entrada fuera de la función** tención accidentalmente devolver un nodo que todavía apunta a un segmento inverso. Silencio Regresar `dummy.next` (o la cabeza original si no hay reversión). Silencio
Silencio **Null pointer dereference** Silencio Calling `kth.next` when `kth` is `null`. Silencio Check `kth == null` **before** using it. Silencio

-...

### 8 comentarios⃣ Interview‐Friendly Tips

1. *Empieza con un tonto* Elimina el manejo especial para la cabeza.
2. **Escribe un ayudante para `getKthNode`** – Mantiene el bucle principal limpio.
3. **Use una inversión de tres puntos** – Demuestra la maestría sobre la manipulación de punteros.
4. **Explica tu lógica de reconexión** – Los entrevistadores les encanta ver articular por qué 'grupo Prev` se traslada a la cola del segmento inverso.
5. **Mostrar complejidad** – Mención O(1) espacio y por qué la versión iterativa es preferible para listas grandes.

-...

## ## 9Ω⃣ Variantes & Extensiones

Silencio Qué cambios Silencio Cómo adaptar Silencio
Silencio----------------------------
Silencio **Reversa en orden inverso (k = n)** Silencio Lista completa invertida Silencio Mismo algoritmo con k = duración de la lista
TEN **Reversal de arranque con variable k** TENK puede cambiar por segmento TEN Store k por segmento o pasar un array TEN
Silencio **Doubly linked list** Silencio Usted puede utilizar `.prev` para simplificar la inversión en el Swap `.next` y los punteros `.prev` en el bucle

-...

Conclusión

*Nodos reversos en K‐Group* no es sólo un ejercicio puntero – es un **diagnóstico** de cómo piensa en estructuras de datos, casos de borde y gestión de memoria.
Al dominar la solución espacial iterativa O(1) (shown above) y estar listo para discutir la alternativa recursiva, usted demostrará tanto ** código limpio** como ** conciencia de ingeniería** – exactamente lo que los gerentes de contratación buscan.

**Siguiente arriba:** Otros LeetCode Linked‐ Los desafíos de lista como *“Remove Nth Node From End of List”* (25) y *“Merge k Sorted Lists”* (23) se basan en los mismos fundamentos. ¡Sigue practicando!

-...

#### 🔗 Referencias

* Problema de LeetCode 25: " : " https://leetcode.com/problems/reverse-nodes-in-k-group/ titulado
* Tutorial de YouTube por el OP (bueno, malo, feo):
* Definiciones oficiales Java/Python/C++ – Identificadashttps://leetcode.com/problems/reverse-nodes-in-k-group/solutions/

-...

**Feliz codificación y buena suerte en su próxima entrevista! * *