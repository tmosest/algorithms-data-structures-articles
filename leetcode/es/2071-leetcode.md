-...
Título: LeetCode 2071. Número máximo de tareas que puede asignar -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📦 2071 – ** Número máximo de tareas que puedes asignar**
■ Dificultad**: Difícil
■ **Tags**: Salud, búsqueda binaria, dos puntos, clasificación

#### TL;DR
- Ordenar " cuadros " (ascendente) y " trabajadores " (ascendente).
- La búsqueda binaria de la respuesta (`mid` = número de tareas que estás tratando de satisfacer).
- Para cada `mid` correr un codicioso * puede-assignar* cheque:
1. Trate de satisfacer la tarea más difícil con el trabajador no arrancado más fuerte.
2. Si el trabajador no es lo suficientemente fuerte, vea si un trabajador más débil puede ser estimulado con una píldora (y todavía tenemos pastillas que quedan).
3. Si ningún trabajador (con o sin una píldora) puede manejar la tarea → `mid` es imposible.
- La más grande posible es la respuesta.

El algoritmo funciona en `O(n+m) log(min(n,m)) + n log n + m log m)` tiempo y `O(n+m)` espacio extra.



-...

## 🧪 1. Full, Idiomatic Code

### 1Ω⃣ Java (Java 17)

``java
importar java.util*;

Clase Solución {
int public int maxTaskAssign(int[] tasks, int[] workers, int pills, int strength) {}
int n = tasks.length, m = workers.length;
int lo = 0, hola = Math.min(n, m);

Arrays.sort(tasks); // ascending
Arrays.sort(trabajadores); // ascender

mientras (lo cautivado) {
int mid = (lo + hola + 1)  1; // número de tareas candidatas
si (puedeAssign(tascos, trabajadores, mediados, pastillas, fuerza)) {}
lo = medio; // mediados es factible → búsqueda superior
. ♫ ... {
hola = mediados - 1; // mediados demasiado alto → búsqueda inferior
}
}
devolver lo;
}

cana booleana privadaAssign(int[] tareas, trabajadores int[],
int taskCount, píldoras int, fuerza int) {}
int w = workers.length - 1; // index of strongest free worker
int freePills = pastillas; // pastillas izquierda

// Trabajar desde la tarea más difícil a la más fácil
para (int t = taskCount - 1; t 0; --t) {
int difficulty = tasks[t];

// 1 / ⃣ Preferir a un trabajador sin una píldora
si (w ≤= 0 " obreros[w] " ? {}
w--; // consumir este trabajador
continuar;
}

// 2Get⃣ Trate de impulsar a un trabajador más débil (si todavía tenemos pastillas)
// Buscamos al trabajador *más débil* que puede ser impulsado para satisfacer
// la tarea actual. Porque ambos arrays están ordenados ascendiendo,
// cualquier trabajador que satisfie `trabajador + fuerza >= dificultad `
// debe ser *no más fuerte* que el trabajador actual que estamos escaneando.
// Así que escaneamos hacia atrás hasta que golpeamos a un trabajador que, después del impulso,
// conoce la dificultad.
mientras (w >= 0 " obreros[w] + fuerza " dificultad) {}
// Empujar a este trabajador a una cola de trabajadores "boosted"
// (serán picados más tarde si nos quedamos sin pastillas)
// Usaremos una estructura tipo pila para mantener el orden.
// Usar una simple matriz de entrada como una pila aquí es suficiente.
si (gratisPills == 0) {
// No quedan pastillas → imposible
devolver falso;
}
// Use una pastilla para este trabajador
freePills...
// Este trabajador ahora puede manejar la tarea, así que consumirla
w...
ruptura;
}

// Si llegamos aquí, la tarea actual no puede ser satisfecha
// con cualquier combinación de trabajo/pill restante
si (w < 0 " pliegues libres == 0) {
devolver falso;
}
}

retorno verdadero;
}
}
`` `

■ **¿Por qué funciona esta versión Java? * *
■ 1. La rutina de `canAssign` es **O(taskCount)** porque caminamos una vez sobre los trabajadores más fuertes y usamos un contador simple para pastillas.
■ 2. La búsqueda binaria externa se ejecuta 'log(min(n,m))' veces, dando la complejidad general.

-...

Python (Python 3.10+)

``python
Solución de clase:
def maxTaskAssign(self, tasks: List[int], workers: List[int],
píldoras: int, fuerza: int) - título int:
tasks.sort()
trabajadores.sort()

lo, hola = 0, min(len(tasks), len(workers))

mientras que lo hizo hola:
media = (lo + hola + 1) // 2
si auto._can(tascos, trabajadores, píldoras, fuerza, mediados):
lo = mitad de las tareas son factibles
más:
hola = media - 1 mitad demasiado ambicioso
regreso

def _can(self, tasks, workers, pills, strength, task_cnt):
""Regresar Verdaderamente si podemos terminar tareas 'tak_cnt'.""
w = len(trabajadores) - 1 # trabajador más fuerte disponible
free_pills = pastillas

# Iterate de lo más difícil a lo más fácil de las tareas seleccionadas
para t en rango(task_cnt - 1, -1, -1):
necesarios = tareas[t]

1. Usar un trabajador no arrancado si tenemos uno
si 0 y los trabajadores[w] requerido:
w -= 1
continuar

# 2. Trate de encontrar un trabajador más débil que podamos impulsar
# (se puede retroceder mientras el trabajador impulsado todavía satisfaría la tarea)
mientras que w 0 y los trabajadores[w] + fuerza requerido:
w -= 1
free_pills -= 1
si free_pills
Retorno Falso

# If we ran out of workers or pills, assignment impossible
si w se realizaron 0 y free_pills 0
Retorno Falso

Retorno
`` `

■ **Por qué esta versión de Python es elegante* *
■ *No explícito multiset o montones – simplemente caminamos los dos arrays ordenados una vez. *

-...

### 3down⃣ C++ (C++20)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int maxTaskAssign(vector fielint limitada tareas, vector implicaint obreros,
píldoras int, fuerza int) {}
(tasks.begin(), tasks.end());
(trabajadores.begin(), workers.end());

int lo = 0, hola = min(tasks.size(), workers.size());

mientras (lo cautivado) {
int mid = (lo + hola + 1) / 2;
si (puedeAssign(tascos, trabajadores, mediados, pastillas, fuerza)) {}
lo = medio;
. ♫ ... {
hola = mediados - 1;
}
}
devolver lo;
}

privado:
bool canAssign(cont vectorial) tareas, const vector
int taskCnt, píldoras int, fuerza int) {}
int w = (int)workers.size() - 1; // index of strongest worker
int freePills = pastillas;

// Iterate de la tarea más difícil a más fácil entre el selecto 'takCnt`
para (int t = taskCnt - 1; t 0; --t) {
int required = tasks[t];

// Use un trabajador sin píldora si lo suficientemente fuerte
si (w ≤= 0 " trabajadores[w] requerido) {
-w;
continuar;
}

// De lo contrario debemos usar una píldora para un trabajador más débil
// Encuentra al trabajador más débil que, después de impulsar, puede hacer la tarea.
// Puesto que los trabajadores están ordenados ascendiendo, el próximo candidato es trabajadores[w].
// Buscamos hacia atrás a tal trabajador.
mientras (w >= 0 " trabajadores[w] + fuerza " se requiere) {
--w; // este trabajador ni siquiera puede ser impulsado
}
si (w Identificado 0 Silencioso librePills == 0) devolver falso; // ningún trabajador dejado

// Boost este trabajador y consumir una píldora
-w;
--freePills;
}
retorno verdadero;
}
};
`` `

■ **Por qué esta versión C++ es rápida* *
■ El cheque codicioso se ejecuta en `O(taskCnt)` y los bucles de búsqueda binaria `O(log(min(n,m)))' veces – perfectamente aceptable para `n,m ≤ 2·105`.

-...

Artículo del Blog – “De las píldoras a la productividad: Mastering LeetCode 2071”

■ **Target audience**: Ingenieros de software, entusiastas de la preparación de entrevistas, reclutadores
■ **Keywords**: LeetCode 2071, asignación de tareas, búsqueda binaria, algoritmo codicioso, entrevista de preparación, entrevista de codificación, solución de problemas, entrevista de trabajo, ingeniero de software

-...

#### ## 1down⃣ El problema en una nuezquela

■ *Se les da 'taks' (nivel de disficultividad) y 'trabajadores' (fortaleza).
■ Un trabajador puede hacer una tarea si su fuerza ≥ dificultad.
■ También tiene un número limitado de píldoras ( " píldoras " ) que añaden temporalmente " fuerza " a un trabajador.
■ ¿Cuál es el número máximo de tareas que puede completar? *

-...

#### 2down⃣ ¿Por qué es difícil este problema?

Por qué es complicado
Silencio...
Silencio **Multiple constraints** Silencio Usted debe cambiar tres variables: tareas, trabajadores, píldoras. Un simple codicioso "asignar al trabajador más fuerte a la tarea más difícil" puede fallar porque podrías desperdiciar una píldora sobre un trabajador débil cuando un trabajador más fuerte podría haber hecho el trabajo sin arranque. Silencio
Silencio **Non‐monotonic decisions** Silencio Una decisión que parece buena localmente (sobre el trabajador más débil) podría bloquear una mejor asignación global. Silencio
Silencio **Large input** Silencio `n, m ≤ 2·105`. Los enfoques de fuerza bruta que prueban todos los subconjuntos son imposibles. Silencio

-...

#### 3down⃣ El "Good Old" Naïve Approach

■ *Los trabajadores que descienden, descienden tareas de clase, luego para cada tarea, eligen al primer trabajador que puede manejarlo (a partir si es necesario). *
■ Esto falla porque usted podría consumir una píldora en un trabajador que de otra manera podría ser emparejado con una tarea posterior, mientras que un trabajador más fuerte se deja ocioso.

-...

### 3down⃣1 Real-World Analogy

Piensa en un equipo de software.
Usted tiene un conjunto de ** características** (tascos) y un conjunto de **desarrolladores** (trabajadores).
Usted tiene un número limitado de horas de **mentorship** (`pills`) que pueden impulsar temporalmente el conocimiento de un desarrollador junior (`strength`).
Si usted asigna la mentoría al desarrollador menos experimentado en una característica que un senior podría haber hecho, usted pierde tiempo de mentoría escaso, potencialmente desaparecido en proyectos más grandes.

-...

#### 4down⃣ La solución elegante: búsqueda binaria + cheque de cortesía

##### 4.1 Panorama conceptual

1. **Sorta** ambos arrays – esto nos da orden para decisiones codictivas.
2. **Binary search** la respuesta: Si usted puede terminar `mid` tareas, pruebe más; si no, pruebe menos.
3. **Comprobación de viabilidad inteligente** – para cada tarea (más difícil → más fácil), elegir el trabajador más fuerte que puede hacerlo. Si no, busque un trabajador más débil que pueda ser impulsado.
4. **Para cuando** golpeaste una tarea que no puede ser satisfecha → `mid` es imposible.

##### 4.2 El Greedy Can‐Assign

■ ¿Por qué funciona?
■ Procesamos tareas para disminuir la dificultad; esto garantiza que cuando consideramos una tarea, cualquier trabajador quede después del bucle sea *demasiado débil* o *ya asignado*.
■ Al elegir siempre el *fuerte* trabajador no arrancado primero, evitamos “sobre-boosting”.
■ Si tenemos que usar una píldora, escogemos al trabajador *más débil* que se puede impulsar – esta conserva pastillas para tareas posteriores.

##### 4.3 Análisis de complejidad

TEN TERRITOR SON TEN ANTERIOR ANTERIOR ANTERIOR TERRITORIO ANTERIOR ANTERIOR ANTERIOR ANTERIOR
Silencio------Prince--------
Silencio Ordenando `taks ' , `trabajadores ' Silencio `O(n log n + m log m)` Silencio `O(1)` Silencio
tención binaria búsqueda Silenciosa `O(log(min(n,m)))' Silencio
Silencio Greedy Check Silencioso `O(taskCnt)` por iteración Silencio `O(1)` Silencio

Total: `O(n+m) log(min(n,m))) ' time, `O(n+m)` space.

-...

#### 5down⃣ Pitfalls to avoid

1. **Misreading the monotonicity** – suponiendo que impulsar al trabajador más débil siempre es mejor.
2. **Usar un montón para el multiset cuando no es necesario** – aumenta los factores constantes.
3. **Off‐by-one errores** – recuerde la búsqueda binaria utiliza `(lo + hola + 1) / 2` para evitar bucles infinitos.

-...

#### 6down⃣ Key Takeaways for the Interview

Silencioso Tip Silencioso Explicación
Silencio...
Silencio **Explicar su intuición** Silencio Empieza describiendo por qué un ingenuo codicioso falla; luego explica cómo la búsqueda binaria + codicioso resuelve el problema. Silencio
Silencio **Discúlpese la complejidad frente a frente** Silencio Los argumentos de la complejidad concisa. Silencio
Silencio **Mostrar la equivalencia** ← Demostrar que el cheque codicioso puede ser implementado en varios idiomas (Java, Python, C++). Silencio
Silencio **Relatar a escenarios del mundo real** Silencio Dibujar paralelos a la gestión de productos, asignación de recursos, o incluso optimización de dosis de drogas. Silencio

-...

### 7ف⃣ Practice, Practice, Practice

**LeetCode**: 2071 – *Task Assignment with Pills*
- **Hard** – pero solvable con una estrategia de búsqueda binaria + codicioso**.
- **Tips**: Escribir casos de borde, ejecutar un rastro de mano, y luego traducir su razonamiento en código limpio.

-...

#### 8down⃣ Palabras finales

■ *LeetCode 2071 es más que un reto de codificación; es una lección de optimización de recursos.
■ Dominarla no sólo le da confianza para las entrevistas, sino que también agudiza su pensamiento para los problemas de ingeniería del mundo real donde debe equilibrar recursos limitados contra las cargas de trabajo exigentes. *

Buena suerte, y que sus pastillas siempre sean usadas sabiamente! 🚀



-...



## 🔚 Wrap‐Up

* Ahora tiene tres soluciones de producción (Java, Python, C++).
* El artículo explica por qué el problema es difícil y cómo articular la solución en un entorno de entrevista.
* Listo para impresionar a los reclutadores? ¡Muéstrales el truco de la “producción arrancada por pilas”! ▪

-...



-...

■ *Si quieres más información o una inmersión más profunda en la estrategia avaricia-vs-binary-search, deja un comentario o DM me. ¡Feliz codificación! *