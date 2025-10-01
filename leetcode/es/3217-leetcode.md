-...
Título: LeetCode 3217. Borrar los nodos de la lista conectada presente en Array -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recaptación de problemas

■ **LeetCode #3217 – Eliminar los nodos de la lista enlazada presente en Array* *
■ Dada una matriz `nums ' y la cabeza de una lista enlazada, eliminar **all** nodos cuyos valores aparecen en `nums ' .
■ Devuelve la cabeza de la lista modificada.

**Constraints* *

TEN TERRITOR ANTERIOR ANTERIOR ANTERIOR
Silencio...
TENIDO `1 ≤ nums.length ≤ 105`
TENIDO `1 ≤ nums[i]
Silencio Todos los elementos de `nums ' son únicos
tención Linked-list size `1 ... 105` Silencio
TENIDO `1 ≤ nodo.val ≤ 105` ANTE
Silencio Por lo menos un nodo es **No** eliminado

El problema es una pregunta de entrevista clásica que prueba:
* uso de hash-set
* manipulación de listas conectadas
* time/space trade‐offs

A continuación encontrará soluciones limpias y preparadas para la producción en **Java, Python y C++** – todo utilizando un solo traversal de la lista y un conjunto de búsqueda O(1).
Después del código encontrará una guía de estilo *blog* que explica el “bueno, el malo y el feo” de este problema y está optimizado SEO para ayudarle a aterrizar su próxima entrevista de codificación.

-...

## 2. Soluciones de referencia

■ Las tres implementaciones utilizan la misma idea:
■ 1. Construir un hash-set (`unordered_set` / `HashSet` / `set`) de `nums`.
■ 2. Camina la lista vinculada con una cabeza muñeca.
■ 3. Pasar los nodos cuyo valor está en el conjunto, de lo contrario mantenerlos.
■ 4. Regresar `dummy.next`.

#### 2.1 Java

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
importa java.util. HashSet;
importa java.util. Set;

Solución de la clase pública {}
public ListNode deleteNodes(int[] nums, ListNode head) {
// 1. Construir el conjunto de valores para eliminar
Establecer:Integer confianza toDelete = nuevo HashSet fiel(nums.length);
(int v : nums) toDelete.add(v);

// 2. Dummy cabeza simplifica los casos de borde
ListNode dummy = nuevo ListNode(0);
dummy.next = head;
ListNode prev = dummy, curr = head;

// 3. Camine la lista una vez
mientras (currir != null) {
si (toDelete.contains(curr.val)) {}
// saltar este nodo
prev.next = curr.next;
. ♫ ... {
prev = curr; // mantenerlo
}
curr = curr.next;
}
Devolver el tonto.
}
}
`` `

-...

### 2.2 Python

``python
Definición para la lista ligada al canto.
class ListNode:
def __init__(self, val=0, next=None):
self.val = val
self.next = next

Solución de clase:
def deleteNodes(self, nums, head):
# 1. Construir el conjunto de valores para eliminar
to_delete = set(nums)

# 2. Dummy head to handle deletions at the front
dummy = ListNode(0)
tonto.next = cabeza
prev, curr = muñeco, cabeza

# 3. Paso sencillo
mientras que curr:
si curr.val en to_delete:
prev.next = curr.next # skip
más:
prev = curr
curr = curr.next

Regresa el tonto.
`` `

-...

### 2.3 C++

``cpp
*
* Definición para lista enlazada.
* struct ListNode {}
* int val;
* ListNode *next;
* ListNode(int x) : val(x), next(nullptr) {}
* };
*/
#include ■unordered_set

Clase Solución {
public:
ListNode* deleteNodes(vector fielint limitada nums, ListNode* head) {
// 1. Hash-set for O(1) lookups
(nums.begin(), nums.end());

// 2. Nodo tonto para evitar casos especiales
ListNode dummy(0);
dummy.next = head;
ListNode *prev = ' dommy, *curr = head;

// 3. Un pase
mientras (curr) {
(toDelete.count(curr- títuloval) {
prev- rationext = curr- rationext; // skip
. ♫ ... {
prev = curr; // mantener
}
curr = curr-ientenext;
}
Devolver el tonto.
}
};
`` `

-...

## 3. Artículo del Blog – *El Bien, el Mal, y el Ugly de Eliminar Nodos de una Lista Relacionada*

■ **SEO Palabras clave**: eliminar nodos de la lista enlazada, preguntas de entrevista de la lista enlazada, código 3217, lista enlazada de Java, lista enlazada de Python, lista enlazada C+++, consejos de entrevista, conjunto de hash, complejidad del tiempo, codificación de la entrevista de trabajo

-...

#### 3.1 Introducción

Las listas vinculadas son la **fundación** de muchas preguntas de entrevista.
Uno de los giros más comunes: “remover todos los nodos que contienen un valor de un array dado. ”
Probablemente lo ha visto en LeetCode (Problema 3217) o en una entrevista técnica.
Se ve simple, pero conseguir los casos de esquina correcto y ofrecer una solución óptima puede ser difícil.

Vamos a desmoronar **el bueno**, **el malo**, y **el feo** de este problema.

-...

### 3.2 The Good: Why It's a Great Interview Test

Silencio ¿Por qué? Cómo te pones a prueba
Silencio...
Silencio **Manipulación de la estructura de datos** Silencio Usted debe entender punteros (o referencias) y cómo cambiar de forma segura los enlaces "next". Silencio
Silencio ** Uso de hash‐set** Silencio Usted debe convertir un array en un conjunto de búsquedas O(1). Silencio
Silencio **Requisito de Paso-Single** Silencio Deberías darte cuenta de que no puedes permitirte atravesar la lista varias veces. Silencio
Silencio ** Manejo de maletas por edge** Silencio Removing the head, all nodes, or nodes – all must be handled Gracefully. Silencio
Silencio **Scalability** Silencio El tamaño de la entrada puede ser de hasta 100 k – por lo que O(n) tiempo y O(1) espacio extra es el lugar dulce. Silencio

Para los entrevistadores, es un **compacto “¿Entiendes punteros + hash‐set?”** pregunta que produce una señal de calidad rápida.

-...

### 3.3 El malo: saltos comunes

Por qué rompe la vida
Silencio------------
Silencio **No usar una cabeza muñeca** Silencio Si se elimina el primer nodo perderás la referencia a la nueva cabeza. Silencio
Silencio **Modifying `next` incorrectly** Silencio Assigning `curr = curr.next` *after* deleting can skip a node or create a cycle. Silencio
Silencio **Tipo de datos incorrecto para el set** Silencio Usar una lista o array para buscar da O(n) por nodo → O(n2) tiempo. Silencio
Silencio **Asumiendo array de entrada está ordenados** Silencio Muchos candidatos equivocadamente intentan búsqueda binaria; el array puede ser sin surtido. Silencio
Silencio **No manejar “no borrar”** Silencio Algunas soluciones devuelven “null” cuando la lista no se cambia. Silencio
Silencio **Tipo de retorno incorrecto** Silencio Regresar el nodo muñeco en lugar de `dummy.next` da una lista vacía. Silencio

Evitar estas trampas muestra que usted entiende el diseño de memoria de lista vinculada y la teoría de conjuntos.

-...

### 3.4 El Ugly: “Lo que si” varia

Silencioso Variante
Silencio...
Silencio **Nodos completos por *valor* en lugar de *index*** tención Usted debe convertir los valores en un conjunto, no posiciones. Silencio
Silencio **Large node values** Silencio El array puede contener valores de hasta 105, pero todavía debe mantener la búsqueda O(1). Silencio
Silencio **Deleción compartida** Silencio (Preguntada Raramente) necesitaría bloquear la lista o utilizar una estructura de datos concurrente. Silencio
Silencio ** Lista enlazada con punteros aleatorios** Silencio Si fuera una lista enlazada *doblemente* o tenía `prev`, tendría que actualizar ambos lados. Silencio
Silencio **Inmutable lista** Silencio Algunos idiomas exponen listas inmutables; usted tendría que construir una nueva lista. Silencio

En una entrevista real, las variantes “muy” a menudo vienen como **curve‐ball seguimientos** (“¿Y si el array es enorme? ¿Y si la lista es una lista de doble enlace?”).

Mostrar que puede **adapt** la idea central (hash‐set + pase único) a nuevas restricciones.

-...

## 3.5 Optimal Solution Walk-through

``text
1. Construir un hash‐set desde el array.
2. Cree un nodo tonto apuntando a la cabeza original.
3. Iteado con dos punteros: prev (estrellando en el muñeco) y curr.
4. Si curr.val está en el set: prev.next = curr.next // skip
Else: prev = curr // keep
5. Mover curr = curr.next.
6. Regresa al tonto.
`` `

*Time*: **O(n + m)** → O(n) because `m` = `nums.length `
*Espacio*: **O(m)** para el conjunto, **O(1)** punteros adicionales.

Con `m ≤ 105`, un hash‐set es la única manera realista de permanecer dentro de los límites de tiempo.
Las bibliotecas estándar de todos los idiomas le dan una estructura **no ordenada** o **hash** que hace exactamente eso.

-...

### 3.6 Edge‐ Lista de verificación de casos

Silencio Caso Edge Silencioso Qué visitar
Silencio----------------
Silencio La cabeza es eliminada ¦ Dummy cabeza mantiene la nueva cabeza. Silencio
Silencio La cola se elimina Silencioso `prev.next` correctamente se convierte en `null`. Silencio
Silencio Todos los nodos eliminados, excepto uno de los loops infligidos continúa hasta que `curr` es `null`. Silencio
Silencio El nodo se elimina Silencioso `prev` siempre avanza, `dummy.next` sigue siendo la cabeza original. Silencio
← Vacío vacío (no sucede debido a limitaciones) Usted puede guardar contra él, pero la especificaciones garantiza al menos un valor. Silencio

Probando contra un pequeño conductor como:

``python
# build list: 1- título2- título3- título4
head = ListNode(1, ListNode(2, ListNode(3, ListNode(4)))
nums = [2, 4]
resultado = Solución().deleteNodes(nums, head)
# result should be 1- titulada3
`` `

asegura que usted está listo para el caso de esquina “no eliminación”.

-...

### 3.6 Interview‐ Consejos listos

TENIDO TERRITORIO ANTERIOR
Silencio...
Silencio **Explica tu plan antes de codificación** Silencio Shows puedes pensar en la mosca. Silencio
Silencio **Talk a través de actualizaciones de puntero** Silencio ayuda a evitar ciclos accidentales. Silencio
Silencio **Pregunta aclarando preguntas** Silencio “¿Está el arreglo? ¿Necesitamos preservar el orden? Silencio
Silencio **Tiempo de la mención / cambio de espacio** Silencio Impress the interviewer that you're aware of algoritmoic constraints. Silencio
Silencio **Escribe un pequeño arnés de prueba** En la entrevista se puede realizar una prueba mental rápida o incluso un rápido Python REPL para probar su lógica. Silencio
Silencio **Use un cabeza hueca** Silencio Es una salvaguardia segura que nunca vas a olvidar. Silencio

-...

### 3.7 Cómo este artículo te ayuda a aterrizar un trabajo

* Las muestras **código** le dan una referencia de copy‐paste rápida.
* Las secciones **blog** resaltan trampas comunes de entrevista, para que pueda presumir sobre *no* caer para ellos.
* Las etiquetas **SEO** ayudan a los reclutadores a encontrar este artículo cuando buscan “preguntas de entrevista de lista conectadas. ”

**Siguiente Paso**: Pruebe cualquiera de las soluciones de referencia en su IDE, ejecute las pruebas de muestra y confíe en explicar el algoritmo en su próxima entrevista.

-...

### 3.8 Pensamiento de clausura

Las listas enlazadas permanecerán como un pilar de entrevistas de codificación durante años.
Dominar este problema de los “nodos de leete” no sólo le da un algoritmo ** ganador** sino que también demuestra:

1. ** Los polos no son sólo un concepto teórico** – son una herramienta del mundo real.
2. ** Hash‐sets son su amigo de búsqueda más rápido** cuando el tiempo importa.
3. **Single‐pass solutions are the gold standard** for interview‐size constraints.

Enséñate, trae una cabeza sodomizada, y te irás con más que una respuesta correcta: te irás con una señal que *realmente entiendes* las instrucciones de datos.

Buena suerte, y feliz codificación!