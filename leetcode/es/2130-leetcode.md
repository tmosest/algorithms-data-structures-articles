-...
Título: LeetCode 2130. Suma Gemela Máxima de una Lista Relacionada -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📌 LeetCode 2130 – *Maximum Twin Sum of a Linked List*
■ **Apilación de idiomas de emergencia:** **Java, Python, C+**
■ ** Complejidad en el tiempo**
■ ** Complejidad del espacio:** `O(1)` (en lugar)

-...

### #1# ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ##### ## ## ### ## ## ## ## #### ###### ## ##### ## ##### ####################################################################################

■ *Se le da una lista con un número de nódulos ** incluso**.
■ El "twin" de nodo `i` es nodo `n‐1‐i`.
■ La suma gemela es " valor(i) + valor(n‐1‐i) " .
■ Devuelve la suma gemela **maximum**. *

Ejemplos

TEN ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio----------...
Silencio `[5,4,2,1]` Silencio `6` Silencio 5+1 = 6, 4+2 = 6 → max = 6
Silencio `[4,2,2,3]` Silencio `7` Silencio 4+3 = 7, 2+2 = 4 → max = 7 Silencio
TENIDO `[1,100000]` TENIDO `100001`

■ **Constraints**
* " 2 " = n " = 105 " (n is even)
* `1 ' = node.val ' = 105 '

-...

## ## 2down⃣ Algorithm Overview

1. **Encuentra el centro de la lista* *
*Two‐pointer (slow/fast)*: `slow` mueve un paso, `fast` dos pasos.
Cuando `rápido' llega al final, `slow` está en el nodo `n/2`.

2. **Reversa la segunda mitad* *
Invierta la lista comenzando en `slow`.
Ahora cada par gemelo está en los ganglios adyacentes: primera mitad de nodo ↔ revirtió segundo medio nodo.

3. #Vivir ambas mitades simultáneamente #
Camine desde la cabeza original y la cabeza de la segunda mitad inversa, resumiendo valores de nodo y manteniendo el máximo.

4. **(Opcional) Restaurar la lista** – no se requiere para la respuesta de LeetCode sino una buena práctica para los entrevistadores.

El truco es hacer todos los pasos *en lugar* para que el uso de la memoria permanezca `O(1)`.

-...

#### 3down⃣ Código de referencia

■ #Java #
■ Python
■ **C++**

■ Las tres implementaciones comparten la misma lógica – solo una sintaxis diferente.

``markdown
## 🔧 Java 17

``java
*
* Definición para lista enlazada.
*/
class ListNode {
int val;
ListNode next;
ListNode(int val) { this.val = val; }
}

Solución de la clase pública {}
int pairSum(ListNode head) {}
// 1 / ⃣ Encontrar el medio
ListaNodo lento = cabeza, rápido = cabeza;
mientras (fast != null " rápido.next != null) {
lento = lento.
rápido = rápido.next.next;
}

// 2down
ListNode prev = null, curr = slow;
mientras (currir != null) {
ListNode next = curr.next;
curr.next = prev;
prev = curr;
curr = siguiente;
}

// 3/50/⃣ Compute twin sums
int maxSum = 0;
ListNode p1 = head, p2 = prev;
mientras (p2 != null) { // p2 tiene n/2 nodos
maxSum = Math.max(maxSum, p1.val + p2.val);
p1 = p1.next;
p2 = p2.next;
}
retorno maxSum;
}
}
`` `

``markdown
## Python 3

``python
Definición para la lista ligada al canto.
class ListNode:
def __init__(self, val=0, next=None):
self.val = val
self.next = next

Solución de clase:
def pairSum(self, head: ListNode) - título int:
# 1 Encontrar el medio
lento = rápido = cabeza
mientras que rápido y rápido.
lento = lento.
rápido = rápido.next.next

# 2⃣ Segunda mitad inversa
Prev = Ninguno
curr = lento
mientras que curr:
nxt = curr.next
curr.next = prev
prev = curr
curr = nxt

# 3️ Compute twin sums
max_sum = 0
p1, p2 = cabeza, prev
mientras que p2: # p2 tiene n/2 nodos
max_sum = max(max_sum, p1.val + p2.val)
p1 = p1.next
p2 = p2.next
volver max_sum
`` `

``markdown
## 🔧 C+17

``cpp
*
* Definición para lista enlazada.
*/
struct ListNode {}
int val;
ListNode *next;
ListNode(int x) : val(x), next(nullptr) {}
};

Clase Solución {
public:
int pairSum(ListNode* head) {
// 1 / ⃣ Encontrar el medio
ListNodo *slow = cabeza, *fast = cabeza;
mientras (fast " rápido " ) {}
lento = lento-conexto;
rápido = rápido- ration-propinto
}

// 2down
ListNode *prev = nullptr, *curr = slow;
mientras (curr) {
ListNode *nxt = curr- rationext;
curr-ientenext = prev;
prev = curr;
curr = nxt;
}

// 3/50/⃣ Compute twin sums
int maxSum = 0;
ListNode *p1 = head, *p2 = prev;
(p2) { // p2 tiene n/2 nodos
maxSum = std::max(maxSum, p1- Confval + p2-Conval);
p1 = p1- títulonext;
p2 = p2- títulonext;
}
retorno maxSum;
}
};
`` `

-...

#### 4down⃣ El Bien, el Mal, y el Ugly

Silencio Silencio
Silencio------------Prince------
Silencio **Tiempo** Silencio O(n) – pase único para encontrar el centro + reverso + computación Silencio Ninguno ←
TEN **Espacio** TEN O(1) – in-place reversal TENCIÓN Iluminar el uso temporal de la pila si la recursión es elegida.
TEN **Readability** TEN Clear separation: find middle → reverse → compute TEN complejo pointer gimnasia puede ser confuso ANTE No revertir (utilizando un array) utiliza el espacio O(n) – “el más fácil pero no el mejor”
Silencio **Edge Cases** tención Handles n = 2 (single twin pair) TEN Ninguno TENIDO Medio mal cuando la longitud de la lista no es ni siquiera (pero el problema garantiza incluso)
Silencio **Interview Tactics** Silencio Mostrar la conciencia de la técnica de dos puntos Silencio Solicitar alternativa (stack, array) – discutir trade-offs Silencio Estar listo para restaurar la lista original si se le pide latitud

-...

#### 5down⃣ ¿Por qué esta solución Rocks for Interviews

1. **Muestra maestría de dos puntos** – un patrón de entrevista clásico.
2. **In-place reversal** demuestra cuidadosa manipulación de punteros y conciencia de memoria.
3. **Paso único (después del revés)** muestra eficiencia algorítmica.
4. **Código limpio** – fácil de entender, testable y escalable.

-...

### 6 comentarios ## Testing & Edge‐ Lista de verificación de casos

Silencio Test ← Input Silencio esperada
Silencio----------------------------
Silencio Incluso la longitud, grande Silencioso `[1,2,3,4,5,6] Silencio `11` Silencio 1+6, 2+5, 3+4 → max 11 Silencio
Silencio Minimal length TENIDO `[2,3]` Silencio `5` TENIDO Únicamente un par de gemelos
Silencio Todos los mismos valores Silencioso `8` Silencio 4+4 pares
Silencio Altos valores que subsisten `[100000,1,1.100000]` Silencio `200000` TEN 100000+100000
Silencio Orden aleatoria Silencio `[7,8,2,9,3,6] Silencio `15` Silencio 7+6, 8+3, 2+9 Silencio

Utilice estos como pruebas de unidad en su IDE o editor en línea.

-...

### 7Ω⃣ SEO‐Optimized Takeaway

- **Título** – “Maximum Twin Sum of a Linked List – LeetCode 2130 Silencio Java / Python / C++ Soluciones”
- **Meta Descripción** – “Aprenda a resolver LeetCode 2130 (Maximum Twin Sum of a Linked List) en Java, Python y C+++. Maestro de dos puntos, inversión en el lugar, y código de entrevista amigable!”
- **Keywords** – LeetCode 2130, Maximum Twin Sum, Linked List problema, dos puntos, lista de enlace inversa, pregunta de entrevista, solución Java, solución Python, solución C++.
- **Headers** - Use `H1` for title, `H2` for sections, `H3` for sub-topics.
- ** Enlaces internos** – Enlace a otros problemas de LeetCode (por ejemplo, “Reverse Linked List”, “Two Sum”) para mejorar la rastreabilidad.
- ** Call‐to-Action** – “Descargar el código, practicar y compartir sus propias soluciones en GitHub para mostrar sus chuletas de codificación!”

-...

#### 8down⃣ Pensamientos finales

- **Mantenga la orden de código** - funciones de ayuda separadas si es necesario.
- **Explicar su enfoque** – hablar de los cambios de tiempo/espacio.
- **Mostrar la conciencia de los obstáculos** – por ejemplo, no manejar la longitud extraña (aunque el problema lo garantiza).
- **Prepárate para retocar** – si se le pide que preserve la lista, puedes revertir la segunda mitad antes de regresar.

¡Buena suerte en tu próxima entrevista! 🚀

¡Feliz codificación!