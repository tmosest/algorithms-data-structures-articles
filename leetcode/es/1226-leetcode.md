-...
Título: LeetCode 1226. Los Filosofos Dining -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
-...

# The Dining Philosophers – A LeetCode Classic (1226)
■ **Problema**: Cinco filósofos se sientan alrededor de una mesa circular, cada uno con un tazón de espaguetis.
■ Entre cada par de filósofos se sienta un tenedor.
■ Un filósofo sólo puede comer cuando sostiene su tenedor izquierdo y derecho.
Ejecutar `wantsToEat()` para que ningún filósofo muera de hambre, incluso cuando el método se llama repetidamente y de múltiples hilos.

■ *Por qué importa*
■ El problema de los Filosofos Dining es el ejemplo canónico de un algoritmo concurrente de bloqueo muerto.
■ Los entrevistadores lo aman porque prueba su comprensión de **mutexes**, **semaphores**, **resource ordering**, y **fairness** en un entorno del mundo real.

■ ** Idiomas**: Java, Python, C++

-...

## 1. La Pitfall Clásico – “All Forks First”

Una solución ingenua se ve así:

``text
cerradura izquierda tenedor
Cierre el tenedor derecho
comer
abrir el tenedor derecho
abrir el tenedor izquierdo
`` `

Cuando cada filósofo toma primero el tenedor izquierdo, surge una espera circular:

`` `
P0 - título left0
P1 - título izquierda1
P2 - título izquierda2
P3 - título izquierdo3
P4 - título izquierda4
`` `

Todos los filósofos bloquean el tenedor derecho, nunca progresando → **Deadlock**.

-...

## 2. El “bueno” – Adquirir el tenedor del IID Primero

La forma más simple de evitar el estancamiento es imponer un orden global en la adquisición de tenedor.

* **Regla**: Cierre siempre el índice **Smaller** primero, luego el más grande.
* Para el filósofo i `
* Índice de tenedor izquierdo = ` i `
* índice de tenedor derecho = `(i+1) % 5`

Si el índice izquierdo de un filósofo identificó el índice derecho, elija primero a la izquierda; de lo contrario elija primero a la derecha.

**Por qué funciona* *
El pedido rompe la espera circular: cada tenedor sólo se puede solicitar en una dirección única.

*Fairness* – Todavía es posible que un filósofo muera de hambre si el programador es parcial, pero las pruebas de LeetCode rara vez muestran ese comportamiento extremo.

**Complejidad** – O(1) por llamada, sin esperar, sin tipos especiales de bloqueo.

-...

## 3. El “Bad” – Busy‐Wait y Spinning innecesario

Un error común es seguir tratando de adquirir un tenedor en un bucle apretado (`tryLock()` repetidamente).
Esto desperdicia ciclos de CPU, degrada el rendimiento, y todavía puede conducir a la inanición.

-...

## 4. El “Ugly” – Usando “sincronizado” sin equidad

`` `
sincronizado (fork[i]) {}
sincronizado (fork [(i+1)%5]) { ... }
}
`` `

"java.lang. Las cerraduras de objetos son *no-fair*. Si usted tiene muchos intentos concurrentes, algunos hilos pueden morir de hambre durante largos períodos.

-...

## 5. La solución final – Código para Java, Python, C++

A continuación se presenta una aplicación limpia y lista para cada idioma, siguiendo la regla **lower-ID‐first**.

### 5.1 Java

``java
importar java.util.concurrent.locks.Lock;
importar java.util.concurrent.locks.ReentrantLock;

clase pública DiningPhilosophers {}

// 5 cerraduras de tenedor
cerradura final privada[] tenedor = nuevo Lock Reentrant[5];

public DiningPhilosophers() {
para (int i = 0; i)
forks[i] = nuevo ReentrantLock(); // no-fair bloqueo está bien aquí
}
}

// run() ejecutará el Runnable suministrado
vacío público quiereToEat(int filósofo,
PickLeftFork ejecutable,
PickRightFork ejecutable,
Comer corriendo,
Runnable putLeft Fork,
Puso ejecutableRightFork) lanza InterruptedException {

int left = filósofo; // index of left fork
int right = (philosopher + 1) % 5; // index of right fork

// elegir el índice inferior primero para evitar la espera circular
int first = Math.min(left, right);
int second = Math.max(left, right);

// adquirir cerraduras
forks[first].lock(); // bloqueará hasta que el bloqueo esté disponible
♪
forks[second].lock();
♪
/ / / recoger las horquillas
si (primero == izquierda) PickLeftFork.run(); si no escogeRightFork.run();
si (segundo == derecho) elijaRightFork.run(); de lo contrario, elijaLeftFork.run();

// comer
comer.run();

/ / / bajado de horquillas
si (primero == izquierda) putLeftFork.run(); si no se poneRightFork.run();
if (second == right) putRightFork.run(); else putLeftFork.run();
Por fin
tenedor[segundo].unlock(); // liberación segundo tenedor
}
Por fin
forks[first].unlock(); // release first fork
}
}
}
`` `

**Test arnés (minimal)* *

``java
vacío estático público principal (cadena[] args) lanza InterruptedException {
DiningPhilosophers dp = nuevo DiningPhilosophers();
PickL ejecutable = () - No. System.out.println(Thread.currentThread().getName()+" elige a la izquierda");
PickR ejecutable = () - No. System.out.println(Thread.currentThread().getName()+" elige derecho");
Comida ejecutable = () - No. System.out.println(Thread.currentThread().getName()+" come");
PutL ejecutable = () - No. System.out.println(Thread.currentThread().getName()+" pone a la izquierda");
PutR ejecutable = () - No. System.out.println(Thread.currentThread().getName()+" pone derecho");

int n = 3; // cuántas veces cada filósofo intentará comer

para (int i = 0; i)
int p = i;
nuevo thread(() - título {
probar { for (int j = 0; j < n; j++) dp.wantsToEat(p, pickL, pickR, eat, putL, putR); }
(InterruptedException e) { e.printStackTrace(); }
}, "Philosopher-"+i).start();
}
}
`` `

-...

### 5.2 Python

``python
importan rosca
de la importación Callable

Clase DiningPhilosophers:
def __init__(self):
self.forks = [threading.Lock() for _ in range(5)]

Def quiere comer (a ti mismo,
filósofo: int,
pickLeftFork: Callable[[], Ninguno],
pickRightFork: Callable[[], Ninguno],
come: Callable[], Ninguno],
putLeftFork: Callable[[], Ninguno],
putRightFork: Callable[[], Ninguno] Ninguno.

izquierda = filósofo
derecho = (filosofía + 1) % 5

# orden locks by id
primero = min (izquierda, derecha)
segundo = máximo (izquierda, derecha)

con auto.forks[primer]:
con uno mismo. forks[segundo]:
# Pick forks
si primero == izquierda:
pickLeftFork()
más:
pickRightFork()

si segundo == derecha:
pickRightFork()
más:
pickLeftFork()

# Come #
comer()

# Bajen horquillas #
si primero == izquierda:
putLeftFork()
más:
putRightFork()

si segundo == derecha:
putRightFork()
más:
putLeftFork()
`` `

** Prueba simple (utilizar 5 hilos)* *

``python
tiempo de importación

def main():
dp = DiningPhilosophers()

def pickL(): print(f"{threading.current_thread().name} picks left")
def pickR(): print(f"{threading.current_thread().name} picks right")
def eat(): print(f"{threading.current_thread().name} comes")
def putL(): print(f"{threading.current_thread().name} puts left")
def putR(): print(f"{threading.current_thread().name} puts right")

def filósofo(id):
para _ en rango(3):
dp.wantsToEat(id, pickL, pickR, eat, putL, putR)
time.sleep(0.01) # dar otros hilos una oportunidad

hilos = [la lectura. Thread(target=philosopher, args=(i,), name=f"P{i}") para i en rango(5)]
para t en hilos: t.start()
para t en hilos: t.join()

si __name_ == "__main__":
principal()
`` `

■ **Nota**: El GIL de Python todavía protege las cerraduras, pero el algoritmo es el mismo que en Java.

-...

### 5.3 C++

``cpp
#include ■iostream
#Incluye #
Incluido el título
#include ■mutex

Clase DiningPhilosophers {}
public:
DiningPhilosophers() {
para (int i = 0; i) {}
forks[i] = std::make_unique seleccionados::mutex Conf();
}
}

vacío quiereToEat(int filósofo,
const std::function garantizadavoid() Elige. LeftFork,
const std::function garantizadavoid() PickRight Fork,
const std::function garantizadavoid() Come,
const std::function garantizadavoid() putLeftFork,
const std::function garantizadavoid() putRightFork) {

int left = filósofo;
int right = (philosopher + 1) % 5;

int first = std::min(left, right);
int second = std::max(left, right);

// bloqueo en orden global
std::unique_lock obtenidos:::mutex confianza lk1(*forks[first]);
std::unique_lock obtenidos:::mutex confianza lk2(*forks[second]);

// recoger
si (primero == izquierda) PickLeftFork();
elijaRightFork();
si (segundo == derecha)PickRightFork();
más pickLeftFork();

// comer
comer ();

//
si (primero ==izquierda) putLeftFork();
más puestoRightFork();
si (segundo == derecho)putRightFork();
más putLeftFork();
}

privado:
std::vector obtenidosstd::unique_ptr se realizó::mutex confianza forks{5};
};
`` `

Prueba rápida

``cpp
int main() {}
DiningPhilosophers dp;
auto pickL = [](){ std::cout Identificado std:::this_thread:::get_id() se hizo "elementos izquierda\n"; };
auto pickR = [](){ std::cout Identificado std:: this_thread:::get_id() se hizo " selecciona right\n"; };
auto comer = [](){ std::cout = seg:: this_thread:::get_id() = " comes\n"; };
auto putL = [](){ std::cout Identificado std:::this_thread:::get_id()
auto putR = [](){ std::cout Identificado std:::this_thread:::get_id()

std::vector seleccionado::thread ths;
para (int i = 0; i) {}
ths.emplace_back([ limitdp,i,pickL,pickR,eat,putL,putR] {}
para (int j=0;j obtenidos3;+j)
dp.wantsToEat(i,pickL,pickR,eat,putL,putR);
});
}
t.join();
}
`` `

-...

## 6. Cómo la solución cumple con los requisitos de LeetCode

* El **API** es exactamente el único suministro de LeetCode – ninguna función principal necesaria para el juez.
* Cada método adquiere **exactamente dos** bloqueos y los libera inmediatamente después de comer.
* Sin esperar, sin inanición de rosca (a propósito de las pruebas).
* Funciona bajo una carga de trabajo altamente concurrente, cada llamada sólo bloquea los dos tenedores necesarios.

-...

## 7. Qué reclutadores quieren ver

1. **Clear callejón sin salida razonando** – “Todos los filósofos que agarran a la izquierda primero → espera circular”
2. **Resource ordering** – “Acquire el tenedor inferior-ID primero. ”
3. **Código de seguridad del pan** - Use `Lock`/`Mutex`/`Semaphore` correctamente.
4. **Mezcla conducida por el mejor** – Mostrar un pequeño arnés de prueba o pruebas de unidad.
5. **Explicación** – Por qué funciona el algoritmo, no sólo código.

-...

## 8. SEO‐Friendly Summary (para el desarrollador de búsqueda de empleo)

Tito**: 1226 – El problema de los filósofos del comedor en Java, Python & C++ *
- **Descripción de los datos**: “Aprenda a resolver el problema de LeetCode Dining Philosophers (1226) con código limpio y libre de bloqueo en Java, Python y C++. Ingrese su preparación de entrevistas y aterrice su próximo trabajo. ”
- **Las palabras clave principales**:
- "Filosofos Dining `
- `LeetCode 1226`
- " cuestión de entrevistas concurrentes `
- Evitación del bloqueo `
- `Java hiloing `
- Multiprocesamiento de pitón `
- 'C++ mutex `
- Entrevista de trabajo `

-...

## 9. Final Takeaway

Silencio Silencio
Silencio...----------------------------------------
Silencio ** Algorithm** Silencio Ordenación de recursos (más bajo-ID primero)
Silencio **Uso de la CPU** TEN O(1) bloqueo de bloqueo de bloqueos TEN alta CPU spin TENIDO Contexto innecesario conmutación TEN
tención **Fairness** tención Mostly fair (pero todavía puede morir de hambre) ← Starvation potencial ← Inanimación del mundo real debido al sesgo programador
Silencio **Readability** Silencio Comentarios claros, cerradura única por tenedor Silencio difícil de leer los lazos ¦ Nested `synchronized` bloques ←

-...

### ¿Quieres clavar tu próxima entrevista?

- *Explica el punto muerto* Mostrar el diagrama de espera circular.
- *Mostrar la solución* Ordenación de recursos o una sola semafora para todos los tenedores.
*La justicia de la mención* “Usando una semafora de la `fair ' si quieres un estricto comportamiento de la roba redonda. ”
- **Hablar sobre la escalabilidad**: El algoritmo funciona en tiempo constante, independiente del número de filósofos.

Deja este artículo en tu blog personal o LinkedIn, y mira a los reclutadores notar que puedes **pensar críticamente acerca de la concurrencia**, **escribir código limpio** en varios idiomas, y **solver puzzles de entrevista clásica**. ¡Buena suerte!