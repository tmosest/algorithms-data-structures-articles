-...
Título: LeetCode 2590. Diseño de una Lista Todo -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 LeetCode 2590 – “Design a Todo List”
### A Deep‐Dive into the Problem, Solution, and Interview‐ Código listo (Java / Python / C++)

-...

#### TL;DR
* **Problema** – Implementar una clase *TodoList* que puede agregar, buscar y completar tareas para muchos usuarios.
****Key operations** – `addTask`, `getAllTasks`, `getTasksForTag`, `complete Tarea.
* **Constraints** – ≤ 100 llamadas, fechas únicas, ≤ 100 usuarios " tareas, etiquetas de hasta 100 por tarea.
* ** Objetivo** – O(1) addition, O(k log k) for fetching (k = # tasks returned).

A continuación encontrará:

Silencio Idioma Silencio Solución completa (listo para pegar en LeetCode)
Silencio--------------------
Silencio **Java** Silencioso Haga clic para ampliar
``java
importar java.util*;
importar java.util.concurrent.ConcurrentHashMap;

clase pública TodoList {
// Contrato para identificación de tareas únicas a nivel mundial
int taskCounter = 1;

// Tareas de mapas Id → Tarea
final privado Mapa seleccionadoInteger, Task confidencial taskMap = new ConcurrentHashMap fiel();

// Usuario de mapas Id → Lista de tareasIds (mantenido en orden de inserción)
mapa final privado realizadoInteger, Listo userTasks = nuevo HashMap fiel();

/** Inicia su estructura de datos aquí. */
public TodoList() {
// Nada que hacer – todos los mapas ya están instantáneos
}

* Añade una tarea y devuelve su ID. */
public int addTask(int user) Id, tarea de cuerdaDescripción, dúo int, lista seleccionadasEtiquetas inteligentes) {
int id = task Counter++;
Tareas = nuevo Task(id, taskDescription, dueDate, tags);
taskMap.put(id, task);

userTasks.computeIfAbsent(user Id, k - título nuevo ArrayList recomendado()).add(id);
retorno id;
}

* Ayudante – devolver una lista de *sin completar* Objetos de tarea para un usuario, ordenados por DueDate. */
Lista privada realizadaTask confianza getPendingTasksSorted(int user Id) {
Lista realizadaTask Confía pendiente = nuevo ArrayList correctamente();
Lista realizadaInteger títulos = usuarioTasks.getOrDefault(userId, Collections.emptyList());
para (int id : ids) {
Task t = taskMap.get(id);
si (!t.completed) pendiente.add(t);
}
(Comparador.comparingInt(t - título t.dueDate));
retorno pendiente;
}

* Obtenga todas las tareas incompletas para un usuario, ordenadas por fecha prevista. */
public List Garantizar confianza getAllTasks(int user Id) {
Lista seleccionadaString titulada res = nuevo ArrayList correctamente();
para (Task t : getPendingTasksSorted(userId)) res.add(t.description);
restitución;
}

* Obtenga todas las tareas incompletas para un usuario que contenga una etiqueta específica. */
public List made(int user) Id, String tag) {
Lista seleccionadaString titulada res = nuevo ArrayList correctamente();
para (Task t : getPendingTasksSorted(userId) {
si (t.tags.contains(tag)) res.add(t.description);
}
restitución;
}

* Marcar una tarea como terminada sólo si pertenece al usuario y sigue pendiente. */
vacío público completo Task(int user) Id, int task Id) {
si (!userTasks.containsKey(userId)) regresa;
si (!userTasks.get(userId).contains(takId))) regresan;
Task t = taskMap.get(taskId);
t.completed = true;
}

--------- Clase de tareas interna...
Clase estática privada {
int id final;
descripción final de String;
final int Fecha;
Lista final: etiquetas de referencia;
boolean completed = false;

Task(int id, String description, int dueDate, List wons) {
esto.id = id;
esto. descripción = descripción;
esto. Fecha límite Fecha;
this.tags = nuevo ArrayList fiel(tags); // copia defensiva
}
}
}
`` `
> >
Silencio **Python** Нелилилинилинаниениханиханиханиханиениханиениениханиениентентениханиениениениениениениениениениениенниениениениениениениениениениениениенниениниениениениениениениниениениениениенниениенниениениениенниеннниениеннниениениениннниенннннниениенинниенни
``python
de las colecciones importadas por defecto
de la importación Lista

Clase TodoList:
def __init__(self):
auto._task_id = 1
auto. tareas = {} Tareas
self.user_tasks = defaultdict(list) # user_id - ratio de tarea ids

def addTask(self, userId: int, taskDescripción: str,
dueFecha: int, etiquetas: List[str]) - int:
Tid = self._task_id
auto._task_id += 1
self.tasks[tid] = {
"desc": taskDescription,
"due": dueDate,
"tags": set(tags),
"completo": Falso
}
self.user_tasks[userId].append(tid)
Vuelva la marea

def _pending_sorted(self, userId: int):
pendiente = [self.tasks[tid] para el tid en self.user_tasks.get(userId, [])
si no auto.taks[tid] ["completo"]]
volver ordenados (pendiendo, key=lambda t: t ["due"])

def getAllTasks(self, userId: int) - titulada List[str]:
volver [t["desc"] para t en uno mismo._pendiendo_ surtido(userId)]

def getTasks ForTag(self, userId: int, tag: str) - Propiedad Lista[str]:
volver [t["desc"] para t en uno mismo._pendiendo_ surtido(userId) si etiqueta en t["tags"]]

def complete Task(self, userId: int, taskId: int) - Ninguno.
si la tarea No estaba en sí mismo. tareas:
Regreso
si taskId no en auto.user_tasks.get(userId, []):
Regreso
si no auto.taks[taskId] ["completo"]:
self.tasks[taskId] ["completed"] = True
`` `
> >
tención **C+** Silencioso Haga clic para ampliar
``cpp
#include יbits/stdc++.h
usando std namespace;

clase TodoList
public:
TodoList() : taskCounter(1) {}

int addTask(int user Id, tarea de cadenaDescripción,
int dueDate, vector asignados etiquetas confianzas) {
int id = task Counter++;
Tarea t{id, taskDescription, dueDate, tags, false};
tareas[id] = t;
userTasks[userId].push_back(id);
retorno id;
}

vectores asignados confiar getAllTasks(un usuario) Id) {
vectoriales res;
para (auto &t : getPendingSorted(userId))
res.push_back(t.description);
restitución;
}

vector de instrucciones clave conseguirTasksForTag(int user Id, string tag) {
vectoriales res;
para (auto &t : getPendingSorted(userId))
si (t.tags.find(tag) != t.tags.end())
res.push_back(t.description);
restitución;
}

vacío completo Task(int user) Id, int task Id) {
auto = usuarioTasks.find(userId);
si (it == usuarioTasks.end()) regresa;
si (find(it-¢nd.begin(), it- títulosecond.end(), taskId) == it- Confend()))
retorno;
auto &t = tasks[taskId];
t.completed = true;
}

privado:
struct Task {
int id;
descripción de la cadena;
int due;
noordered_set obtenidosstring etiquetas de título;
bool completed = false;
Task(int i, string d, int du, vector identificadostring confianza tg)
: id(i), description(d), due(du), tags(tg.begin(), tg.end()) {}
};

int taskCounter; // siguiente ID de tarea global
unordered_map obtenidos, Tarea tareas; Id → Tarea
unordered_map madeint, vector usuarioTasks; // usuario Id → lista de tareas Ids

// Devolución de tareas pendientes por fecha prevista
vector asignadoTask confianza getPendingSorted(int user) Id) {
vector iniciado;
auto = usuarioTasks.find(userId);
si (it == userTasks.end()) regresan pendientes;
para (int id : it- Confsegundo) {
auto &t = tasks[id];
si (!t.completed) pendiente.push_back(t);
}
(pendiendo.begin(), pending.end(),
[](Cont Task ' , const Task &b){ devolver a.due = b.due; });
retorno pendiente;
}
};
`` `
> >
Silencio **C+** (estilo LeetCode-style) Haga clic para ampliar
``cpp
#include יbits/stdc++.h
usando std namespace;

clase TodoList
public:
TodoList() : nextId(1) {}

int addTask(int user Id, tarea de cadenaDescripción,
int dueDate, vector asignados etiquetas confianzas) {
int id = siguiente Id++;
tareas[id] = {taskDescription, dueDate, tags, false};
userTasks[userId].push_back(id);
retorno id;
}

vectores asignados confiar getAllTasks(un usuario) Id) {
auto v = pendingSorted(userId);
vectoriales res;
(auto &t : v) res.push_back(t.description);
restitución;
}

vector de instrucciones clave conseguirTasksForTag(int user Id, string tag) {
auto v = pendingSorted(userId);
vectoriales res;
para (auto &t : v) si (t.tags.count(tag)) res.push_back(t.description);
restitución;
}

vacío completo Task(int user) Id, int task Id) {
si (!userTasks.count(userId)) regresa;
si (!tasks.count(taskId)) regresa;
si (!userTasks [userId].count(taskId)) regresa;
si (!tasks[taskId].completed) tareas[taskId].completed = true;
}

privado:
struct Task {
descripción de la cadena;
int due;
noordered_set obtenidosstring etiquetas de título;
bool completed;
Task(string d, int du, vector identificadostring confianza tg)
: descripción(d), due(du), tags(tg.begin(), tg.end()), completed(false) {}
};

siguiente Id;
unordered_map obtenidos, Tarea tareas; Id → Tarea
unordered_map Utilizar Tareas; // usuario Id → conjunto de tareas Ids

// vector de retorno de tareas pendientes ordenados por fecha
vector asignadoTask confianza pendienteSorted(int user Id) {
vector asignadoTask confidencial v;
if (!userTasks.count(userId)) return v;
para (int id : userTasks[userId]) {}
Task &t = tasks[id];
si (!t.completed) v.push_back(t);
}
sort(v.begin(), v.end(), [](const Task &a, const Task &b) {
devolver a.due
});
retorno v;
}
};
`` `
> >

-...

## 📚 ¿Qué significa "Diseñar una lista de todo" realmente quiere?
A primera vista parece un simple problema de estructura de datos de estilo CRUD.
Pero en una entrevista usted está siendo probado en:

1. **Diseño orientado hacia objetos** – cómo modelas *taks*, *usuarios*, y la lista misma.
2. ** Escalabilidad & complejidad** – aunque LeetCode limite las llamadas a 100, todavía debe apuntar a **O(1) add** y **log‐linear fetches**.
3. **Manejo por caso electrónico** – etiquetas, IDs de usuario duplicados, identificadores de tareas inexistentes, etc.
4. ** readability del código** – entrevistadores buscan código limpio y comentado.

### Good, Bad & Ugly: A Quick Checklist
Silencio Silencio Silencio Silencio
Silencio...
Silencio TENIENDO clara separación de responsabilidades (TodoList vs. Task). Silencio ❌ Ordenar por cada lote puede ser desperdicio si usted tiene muchas tareas. Ø ❌ Utilizar campos estáticos globales para contadores puede romperse en un entorno multi-tele. Silencio
Silencio Uso de copias defensivas (tags, strings). ← ❌ Las estructuras mutables (`lista de taskIds) pueden ocultar fallos cuando se eliminan las tareas. ❌ Over-engineering: a whole new DB layer or a micro-service for a LeetCode problem. Silencio
Silencio ↓ O(1) `addTask` gracias a hash maps. ❌ `complete Task` debe comprobar la membresía del usuario – un escaneo lineal si mantiene un vector. Ø ❌ Failing to mark `completed` puede llevar a resultados duplicados. Silencio
Silencio ✅ `getAllTasks` / `getTasksForTag` compartir un ayudante común – sin duplicación de códigos. Silencio ❌ Clasificar cada vez está bien para 100 operaciones pero no para la producción. Silencio ❌ Utilizar `static` or global counters without `volatile` in Java leads to race conditions. Silencio

-...

## 📌 Design Overview

### 1. Data‐Model

Silencioso Element Silencio Representación
Silencio...
Silencio **Task** Silencioso Objeto con campos: `id`, `description`, `dueDate`, `tags` ( " Setificaron " ), " completado " (bool). tención mantiene todos los atributos de tarea juntos y soporta actualizaciones O(1). Silencio
Silencio **User → Tareas** Silencio `Mapa realizadauserId, Lista realizadataskId confianza `` (o `unordered_map identificado, vector asignadoint título ` en C++). tención simple & rápida búsqueda de la lista de tareas de un usuario. Silencio
Silencio ** ID Global** Silencioso `int counter` (Java), `int _task_id` (Python), `int next Id` (C++). tención Garantiza IDs de tarea únicas a nivel mundial. Silencio

■ **¿Por qué no un TreeSet por usuario? * *
■ Con fechas únicas podríamos mantener un 'TreeMap observadodueDate, taskId titulado` por usuario. Eso daría *O(log k)* buscar sin ordenar.
■ Sin embargo, el problema garantiza **≤ 100 llamadas** y tamaños de datos pequeños, por lo que un simple escaneo lineal + `sort` es *más que suficiente* y mucho más fácil de implementar.

### 2. Desglose de la operación

TEN TERRITORIO TERRITORIO ANTERIOR
Silencio----------------------
Silencio `addTask` Silencio **O(1)** Silencio Insertar en dos mapas de hash. Silencio
Silencio `getAllTasks` Silencio **O(k log k)** Silencio Filtrar tareas incompletas, ordenar por dueFecha. Silencio
Silencio `getTasksForTag` Silencio **O(k log k)** Silencio Igual que arriba más un filtro `tag`. Silencio
Silencio `completeTask` Silencio **O(1)** Silencio Lookup Direct hash + un cheque de membresía rápido. Silencio

### 3. Thread‐Safety (Optional Bonus)
La solución Java proporcionada utiliza `ConcurrentHashMap` y mantiene el `takCounter` como un simple `int`.
Si se le pidió una aplicación * seguro*, usted:

* Envuelve el aumento del contador en un bloque sincronizado o usa `AtomicInteger`.
* Keep `userTasks` as `Concurrent HashMap Haga clic enInteger, CopyOnWriteArrayList recomendadoInteger confianza`.
* Mark `completed` using `AtomicBoolean`.

Para LeetCode esto es exagerado, pero mostrar conocimiento de concurrencia puede impresionar a los gerentes de contratación.

-...

## Corriendo la Muestra

``plaintext
Entrada:
["TodoList", "addTask", "getAllTasks", "getTasksForTag", "completeTask", "getAllTasks"]
[[],[1, "leche de compra",3, ["creceries"]],[1],[1,"creceries"],[1,1],[1]]

Producto:
[null,1, ["buy leche"], ["buy leche"],null,[]]
`` `

1. Cree una nueva lista.
2. Añadir una sola tarea → ID `1`.
3. `getAllTasks` devuelve `["buy milk"].
4. `getTasksForTag` (tag = `'groceries'') devuelve lo mismo.
5. `completeTask(1,1)` se hace.
6. Final `getAllTasks` produce una lista vacía.

Todos los idiomas proporcionados manejan esto exactamente como se esperaba.

-...

## What to Practice Next

Esquía permanente práctica Idea Silencio
Silencio...
Silencio ** Hash‐map tricks** Silencio Implementar un caché que invalida después de *n* golpes. Silencio
Silencio **Set vs. List** Silencio Construir un pequeño caché LRU para decidir entre O(1) deletion vs. O(log n) busca. Silencio
Silencio **Concurrencia** Silencio Escribir un `Singleton` con un 'volatil' contador y prueba con múltiples hilos. Silencio
Silencio **Testing** Silencio Crear pruebas de unidad que cubren: usuario inexistente, etiquetas duplicadas, marcando ya completado. Silencio

-...

Veredicto final
Usted acaba de resolver un problema de LeetCode que * no es sólo sobre algoritmos*, sino sobre el diseño.
La clave despega: **modelo bien el problema**, mantenga su código limpio, y esté listo para discutir *por qué* usted eligió una estructura de datos particular.

Eso, amigos, es el sello distintivo de un ingeniero de alto nivel, ambos para entrevistas y proyectos del mundo real. 🚀

-...


**Keywords para reclutadores**: diseño orientado al objeto, mapa de hash, operaciones O(1), copia defensiva, concurrencia, código limpio, LeetCode, habilidades de entrevista.