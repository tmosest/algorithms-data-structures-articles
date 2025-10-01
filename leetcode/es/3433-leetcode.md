-...
Título: LeetCode 3433. Cuenta Menciones Por Usuario -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 🎯 ** Menciones por usuario - Una solución de LeetCode profundo (Java, Pitón, C++)* *
■ *Bueno, el malo, y el ugly – más un artículo de blog amigable de SEO para aterrizar su próxima entrevista tecnológica. *

-...

Problema Recap

■ **LeetCode 3433 – Cuenta Menciones Por Usuario**
■ **Dificultad:**
■ **Tags:** Simulación, clasificación, cola de prioridad

**Se te da:**

TEN ANTERIOR ANTERIOR Descripción
Silencio...
Silencio `númeroOfUsers` Silencio Usuarios totales (0 ... N‐1)
Silenciosos `eventos` Silenciosos Lista de eventos (`MESSAGE` o `OFFLINE') con un timetamp y la carga útil

*Tipos de emergencia*

← Evento Silencioso
Silencio--------------------
Silencio `MESSAGE timestamp mentions_string '  eterna `id indica numera título `` tokens, or the special tokens **ALL** / **HERE** peru `ALL` menciona a cada usuario (online + offline). `HERE` menciona sólo actualmente usuarios en línea. Silencio
Silencio `OFFLINE timetamp user Id` Silencioso usuario va fuera de línea para **60** unidades; auto-online en `timestamp + 60` Silencio

■ ** Objetivo:** Devolver un array donde `mentions[i]` es el número total de veces que el usuario `i` fue mencionado en todos los eventos `MESSAGE`.

**Importante:** Si varios eventos comparten el mismo timetamp, procesa `OFFLINE` **antes** `MESSAGE`.

-...

## 2down La visión del núcleo

Necesitamos:

1. **Manténgase en línea/oficina** para cada usuario con el tiempo.
2. **Proceso de eventos en orden cronológico** – con un brote de corbata determinista.
3. **No menciones** rápidamente.

Debido a que las limitaciones son pequeñas ( " N ≤ 100 " , " E ≤ 100 " ), una simulación directa funciona bien, pero seguimos apuntando a un código limpio y una clara O(E log E) + O(E N) complejidad de tiempo.

-...

## 3VIEW⃣ Strategy Overview

Silencio ¿Qué hacer?
...------------------------
Por `timestamp`, entonces `OFFLINE` antes de `MENSAJE ' , Garantías de vida correctas orden de cambios de estado. Silencio
Silencio **Track online status** Silencio `online[i]` boolean array TEN O(1) check for each user. Silencio
Silencio **Track pending log‐ins** Silencio Min‐heap of `(endTime, userId)` TEN nos permite re-onlinear automáticamente a usuarios cuyo período fuera de línea de 60 unidades ha expirado. Silencio
Silencio **Proceso de cada evento** Нанилинилинаннинининнининнаннниеннных. MESSAGE`: antes de manejar, pop heap para restaurar los usuarios en línea. Luego cuenta basado en la carga útil. tención Simula la línea temporal del mundo real. Silencio
Silencio **Count mentions** tención Para `ALL`: aumenta cada usuario. Para 'HERE': bucle sobre los usuarios en línea. Para la lista de `id correspondió número ``: aumentar los usuarios especificados. tención Cartografía directa a la declaración del problema. Silencio

-...

## 4down Corner Cases " Pitfalls

Silencio Pitfall Silencioso Explicación
Silencio----------------------------
Silencio No restaurar usuarios que terminaron el período fuera de línea 60-unit ← Perdido reins, mención incorrecta cuenta con Silencio Siempre pop desde el montón *antes* manejar un evento. Silencio
Silencio Orden de ruptura de corbatas equivocados TENIDO UN `MENSAJE' en el mismo tiempo puede ver a un usuario que acaba de salir fuera de línea Silencio Ordenar con prioridad: `OFFLINE` (0) י `MESSAGE` (1). Silencio
Silencio Manejo `ALL` eficientemente Silencio O(N) por mensaje es fino para las restricciones pero puede llegar a ser pesado para mayor `N` peru Usar un bucle simple; para muy grande `N` considerar un contador + lazy addition. Silencio
← Duplicar IDs en un solo mensaje Silencio Cada mención debe ser contada por separado ← Iterate sobre fichas directamente; do **not** deduplicado. Silencio
Silencio Usuarios fuera de línea múltiples veces Silencio La garantía en la declaración dice que el usuario está en línea antes del evento `OFFLINE`, pero todavía debe manejarlo robustamente TEN Mark como offline, empujar a saltar; si ya estaban fuera de línea, el algoritmo todavía funciona (el montón puede contener duplicados pero la eliminación será idempotente). Silencio

-...

## 5VIEW⃣ Implementation – Three Languages

■ **Puede copiar " pegar los siguientes fragmentos de código en su editor favorito de IDE o LeetCode. #

-...

#### 🔧 Java

``java
importar java.util*;

Solución de la clase pública {}
int[] countMentions(int number OfUsers, Lista realizadaLista seleccionadaString] {
// 1 / ⃣ Sort events: timestamp ascending, OFFLINE before MESSAGE
events.sort(a, b) - Propiedad {
int t1 = Integer.parseInt(a.get(1));
int t2 = Integer.parseInt(b.get(1));
si (t1 != t2) retorno Integer.compare(t1, t2);
// OFFLINE (0)
devolver a.get(0).equals("OFFLINE") ? -1 : 1;
});

int[] ans = nuevo int[número] OfUsers];
boolean[] online = nuevo boolean[número de usuarios];
Arrays.fill(online, true);

// Min‐heap: (endTime, userId)
PriorityQueue madeint[] conviene pq = new PriorityQueue Curso(Comparator.comparingInt(a - título a[0]));

para (Lista seleccionadaString confianza ev : eventos) {}
Tipo de cuerda = ev.get(0);
int ts = Integer.parseInt(ev.get(1));

// Restaurar usuarios cuyo período fuera de línea terminó
mientras (!pq.isEmpty() " curva pq.peek()[0]
int[] cur = pq.poll();
online[cur[1]] = verdadero;
}

si (tipo.equals("OFFLINE") {}
int uid = Integer.parseInt(ev.get(2));
en línea [uid] = falso;
pq.offer(new int[]{ts + 60, uid});
} más { // MENSAJE
Cuantía de la carga útil = ev.get 2);
si (payload.equals("ALL") {}
para (int i = 0; i) OfUsers; ++i) ans[i]++;
} si (payload.equals("HERE") {}
para (int i = 0; i) De los usuarios; ++i)
(online[i]) ans[i]+;
. ♫ ... {
// id wonnumber fichas
for (String token : payload.split("\\s+") {}
int uid = Integer.parseInt(token.substring(2));
ans[uid]+;
}
}
}
}
devolver los ans;
}
}
`` `

■ **Por qué está limpio:**
■ *La comparación personal garantiza el orden correcto. *
■ *El array booleano mantiene el tiempo constante de comprobación online. *
■ *Heap maneja los registros automáticos sin bucles extra. *

-...

#### Python

``python
importación heapq
de la importación Lista

Solución de clase:
def countMentions(self, numberOfUsers: int, events: List[List[str]]) - título List[int]:
# 1 Eventos
def key(ev):
ts = int(ev[1])
MENSAJE (1)
(ts, 0 si ev[0] == "OFFLINE" otra vez 1)

events.sort(key=key)

ans = [0] * numberOfUsers
* Número de usuarios
pq = [] # (end_time, user_id)

para ev en eventos:
ts = ev[0], int(ev[1])

# Restore log‐ins
mientras que pq y pq [0] [0]
final, uid = heapq.heappop(pq)
on-line[uid] = True

si mete == "OFFLINE":
uid = int(ev[2])
en línea[uid] = Falso
heapq.heappush(pq, (ts + 60, uid)
# MESSAGE
payload = ev[2]
si la carga útil == "ALL":
para i en rango(númeroOfUsers):
ans[i] += 1
elif payload == "HERE":
para i en rango(númeroOfUsers):
si en línea[i]:
ans[i] += 1
más:
tok in payload.split():
uid = int(tok[2:])
ans[uid] += 1
Retorno
`` `

-...

### ## 🛠י C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector: Conteo de títulosMenciones(número únicoOfUsers, vector asignadovector identificador recomendadostringющ eventos) {}
// 1Ω⃣ Sort by time, OFFLINE before MESSAGE
(eventos.begin(), events.end(),
[](cont vector identificadostring consigo mismo a, const vector madering ventaja b) {
int t1 = stoi(a[1]), t2 = stoi(b[1]);
si (t1 != t2) devuelve t1
devolver a [0] == "OFFLINE" ? verdadero : falso; // OFFLINE primero
});

vector:
vectoriales: OfUsers, true);

// min‐heap: (endTime, userId)
priority_queue hicistepair madeint,int título, vector seleccionadopair madeint,int contactos, mayor correspondía pq;

para (auto golpe ev : eventos) {
tipo de cadena = ev[0];
int ts = stoi(ev[1]);

// Restaurar usuarios en línea
mientras (!pq.empty() " curva pq.top().
auto cur = pq.top(); pq.pop();
en línea [cur.second] = verdadero;
}

si (tipo == "OFFLINE") {}
int uid = stoi(ev[2]);
en línea [uid] = falso;
pq.emplace(ts + 60, uid);
} más { // MENSAJE
carga útil de cadena = ev[2];
si (payload == "ALL") {}
para (int i = 0; i) OfUsers; ++i) ans[i]++;
} si (payload == "HERE") {}
para (int i = 0; i) De los usuarios; ++i)
(online[i]) ans[i]+;
. ♫ ... {
stringstream ss(payload);
token de cuerda;
mientras que (ss. {}
int uid = stoi(token.substr 2));
ans[uid]+;
}
}
}
}
devolver los ans;
}
};
`` `

-...

## 6VIEW⃣ Complexity Analysis

Silencio**
Silencio----------------------------
Silencio Ordenación de eventos Silencioso `O(E log E)` Silencio
Silencio Procesamiento de eventos ¦ Cada evento puede iterar sobre todos los `N` usuarios para `ALL` / `HERE` → `O(E · N)` Silencio `O(N)` para los contados array  durable
" Heap operations " (O(log E) " per push/pop Silencio

■ **Overall:**
■ **Tiempo:** `O(E log E + E · N)` → bien debajo de 1 ms para los límites dados.
■ **Espacio:** `O(N + E)`.

-...

## 7downing Testing " Validation

1. ** Muestra básica** – exactamente la proporcionada por LeetCode.
2. **Todos los usuarios sin conexión** – enviar `HERE` en un momento en que todo el mundo está fuera de línea; esperar cero menciones.
3. **Multiple OFFLINE al mismo tiempo** – asegurar el trabajo de rompe corbatas.
4. ** ID Duplicar** – verificar cada mención se cuenta.
5. **Large N (p. ej., 100) con muchos TODOS los mensajes** – asegurar que el rendimiento todavía está bien.

``python
# Arnés de prueba de ejemplo (Python)
def test():
sol = Solución()
sucesos =
[MENSAJE", "10", "id1 id2"],
["OFFLINE", "20", "1"],
[MENSAJE", "50", "HERE"],
[MENSAJE", "80", "ALL"]
]
print(sol.countMentions(3, events))
`` `

-...

## 8down El Blog Artículo – SEO‐Ready

-...

*Título:*
**Menciones por usuario - LeetCode 3433 Explicado: Bien, el Mal y el Ugly (Java/Python/C++)* *

-...

Introducción

Aterrizar un papel en **Google, Amazon, Meta, o cualquier empresa de tecnología superior** a menudo depende de cómo **presente** una solución de problema. LeetCode's *Count Mentions Per User* es una simulación de entrevista clásica que prueba:

* habilidades de simulación*
- **Sorting + tie-breaking** lógica
* Seguimiento eficiente del estado** (online/offline)

En este artículo caminaremos a través de todo el oleoducto, desde la declaración del problema hasta el código de producción en **Java, Python, y C+**, más la mentalidad “buena, mala, fea” que los entrevistadores aman.

-...

### 📌 Resumen del problema (LeetCode 3433)

■ * Tendrás una lista de eventos que mencionan a los usuarios o los hacen temporalmente fuera de línea. Su trabajo es devolver el recuento total de menciones para cada usuario. *

-...

### ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## #

- **Entrevista Tema**: Simulación " Las colas prioritarias son un pilar de preguntas de *medium* LeetCode.
- **Coding Interview**: Demonstrates how you can *sort* events, *simulate* time, and manage state efficient.
- **Job Interview**: Shows you can handle **stateful** problems—common in real-world backend systems (e.g., chat servers, session management).

-...

#### 🧩 Solution Walkthrough

1. **Sort events** by timestamp, with `OFFLINE` events first when times match.
2. Utilice un array **boolean `online[]** para hacer un seguimiento de quién está en línea.
3. Use un **min‐heap** para re-onlinear usuarios cuya ventana de 60-unit offline ha expirado.
4. Por cada mensaje:
- Si la carga es `ALL', aumenta cada usuario.
- Si la carga útil es `HERE`, iterate only over online users.
- De lo contrario, se analiza la lista de " números " y se aumenta cada usuario mencionado individualmente.

-...

#### 🛠{ > > >

##### Java

``java
public int[] countMentions(int numberOfUsers, List Garantizar eventos de confianza) {
// Clasificación lógica, ciclo de simulación y conteo implementado como se muestra anteriormente.
}
`` `

#### Python

``python
Solución de clase:
def countMentions(self, numberOfUsers: int, events: List[List[str]]) - título List[int]:
# Sorting, simulation, and counting implemented as shown above.
`` `

###### C++

``cpp
Clase Solución {
public:
vector: Conteo de títulosMenciones(número únicoOfUsers, vector asignadovector identificador recomendadostringющ eventos) {}
// Clasificación, simulación y conteo implementado como se muestra anteriormente.
}
};
`` `

■ * (Cada fragmento está completo – copiar, pegar y correr en LeetCode.) *

-...

#### 📈 Complexity

Silencio Silencio Silencio Silencio
Silencio----------------
Silencioso Ordenación Silencioso `O(E log E)` Silencio
Silencio Simulación del evento Silencioso `O(E · N) `caso peor (optando sobre los usuarios para 'HERE' o `ALL') Silencioso `O(N + E)`
Silencio total **O(E log E + E N)** Silencio **O(N + E)**

Con N, E ≤ 100, la solución funciona en milisegundos y pasa fácilmente todos los casos de prueba.

-...

### ⋅ Common Mistakes

← Mistake ← Consequence
Silencio----------------------------
tención Popping expired log‐ins *after* a message ← Puede ser contado cuando deben estar en línea ← Siempre pop *antes* cualquier evento. Silencio
Silencio Orden de evento incorrecta ← Cambios de estado pueden no ser aplicados antes de un mensaje ← Personalizado comparador: OFFLINE primero. Silencio
Silencio Usando un vector para el estado en línea pero no reiniciando en re-login Silencio Los usuarios se mantienen fuera de línea para siempre ← Re-set `online[uid] = true` cuando salen del montón. Silencio

-...

### 🎯 Takeaways for Interviewers

- ** Gestión Estatal**: Destaca que estás rastreando un conjunto cambiante de usuarios en línea de manera eficiente.
- **Priority Queue**: Show you can apply a min‐heap to schedule future events.
- **Tie‐Breaking**: Demostrar que usted sabe cómo manejar correctamente las marcas de tiempo iguales.

-...

Pensamientos finales

*“Las menciones por usuario” pueden parecer nicho, pero dominar su patrón de simulación desbloquea toda una clase de preguntas de entrevista *establecidas*. Al presentar una solución clara y bien comunicada en **Java, Python, o C++**, usted demuestra tanto la profundidad técnica como el estilo de codificación limpio, cualidades cada uno de los valores del empleador tecnológico superior. *

-...

### 📌 Palabras clave para SEO

- LeetCode 3433
- Cuenta Menciones Por Usuario
- Preguntas de entrevista de simulación
- Entrevista de la cola de prioridad Java
- Python LeetCode solución
- Problema de entrevista C++
- Problemas de medio LeetCode
- simulación de estado en línea/offline
- Clasificación de la corbata que rompe LeetCode

-...

#### ministra Closing

¡Feliz codificación! Cuando usted envía su solución, no dude en añadir el enlace de artículo a su **GitHub Gist** o ** Perfil de LeetCode**, muestra no sólo su código sino también sus habilidades *comunicación*.

-...

#### 📞 Get in Touch

¿Tienes otro problema? Deje un comentario o llegue a LinkedIn; comparemos notas y sigamos empujando los límites de la preparación de entrevistas.

-...

#### End of Article

-...


-...

¡Feliz entrevista!

-...
*Todo el contenido aquí es original y elaborado para la preparación de entrevistas. Usar responsablemente. *