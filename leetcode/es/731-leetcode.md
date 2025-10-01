-...
Título: LeetCode 731. Mi Calendario II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 731 – Mi Calendario II
**Solutions in Java, Python & C++ + un SEO-friendly interview‐blog* *

-...

## 📚 Problem Overview (LeetCode 731)

■ *Tienes que implementar un calendario que pueda reservar eventos mientras no **tres** eventos se superponen al mismo tiempo.
■ Los eventos son intervalos medio abiertos \([start, end)\). Regrese 'verdad' si el evento puede ser añadido, de lo contrario 'false'. *

■ **Constraints**
* `0 ≤ inicio > final > 10^9`
* ≤ 1000 `book()` llamadas

-...

## 🔧 Key Idea

Mantener **dos colecciones**:

1. **Todos los eventos reservados** – para detectar cualquier superposición* nueva.
2. ** Intervalos de doble libro** – intervalos que ya están cubiertos por dos eventos.
Si un nuevo evento superpone cualquiera de estos, una reserva **triple** ocurriría → rechazar.

La solución clásica de dos listas se ejecuta en **O(N)** por `book()` (N = número de eventos existentes).
Un enfoque más eficiente utiliza un *sweep-line* (`TreeMap` / `std::map`) y funciona en **O(log N)** por llamada.

A continuación se presentan tres implementaciones idiomáticas (Java, Python, C++) que utilizan la estrategia *two-list* para la claridad.

-...

## ⚙ Java Implementation

``java
importa java.util. ArrayList;
importa java.util. Lista;

clase Evento {}
int start, end;
Event(int s, int e) { start = s; end = e; }
}

clase MyCalendar Dos.

Lista final privada realizadaEvento registrar reservas = nuevo ArrayList fiel();
Lista final privada realizadaEvento relativo superposiciones = nuevo ArrayList fiel();

public MyCalendar Dos...

public boolean book(int start, int end) {
// 1) Comprobar la librería triple
para (Evento e : superposiciones) {}
si (esOverlap(e, start, end)) devolver falso;
}

// 2) Grabar nuevos libros dobles
para (Evento e : reservas) {}
si (esOverlap(e, start, end)) {}
sobrelaps.add(nuevo evento(
Math.max(e.start, start),
Math.min(e.end, end)
));
}
}

// 3) Persiste el nuevo evento
bookings.add(new Event(start, end));
retorno verdadero;
}

booleano privado isOverlap(Evento e, int s, int t) {}
devolver Math.max(e.start, s)
}
}
`` `

■ *Las complejidades*
• **Tiempo:** `O(n)` por `book()` (el escaneo lineal en el peor de los casos).
• **Espacio:** `O(n)` para las dos listas.

-...

## 🐍 Python Implementation

``python
Evento de clase:
__slots__ = ("s", "e")
def __init__(self, s, e):
auto.

clase MyCalendar Dos:
def __init__(self):
self.bookings = [] # Todos los eventos #
self.overlaps = [] # intervalos de doble reserva

def book(self, start: int, end: int) - Conf Bool:
# 1) Triple cuaderno
para ti mismo. superposiciones:
si max(e.s, start)
Retorno Falso

# 2) Construir nuevas superposiciones
para ti mismo. reservas:
si max(e.s, start)
self.overlaps.append(Event(
max(e.s, start),
min(e.e, end)
)

3) Persiste el nuevo evento
self.bookings.append(Event(start, end))
Retorno
`` `

■ *Las complejidades*
• **Hora:** `O(n)` por llamada.
• **Espacio:** `O(n)`.

-...

## C+++ Aplicación

``cpp
Incluido el título
usando std namespace;

struct Event {
int s, e;
Event(int ss, int ee) : s(ss), e(ee) {}
};

clase MyCalendar Dos.
vectores reservadosEvento usuario;
vector:Evento coincidencias;

bool isOverlap(const Evento, int s, int t) const {
volver max(e.s, s)
}
public:
MyCalendar Two() = default;

bool book(int start, int end) {
// 1) Triple guardia de reserva
para (continuo auto choza e : superposiciones)
si (esOverlap(e, start, end)) devolver falso;

// 2) Recordar nuevas superposiciones
para (continuo auto cho e : reservas)
si (esOverlap(e, start, end))
overlaps.emplace_back(
max(e.s, start),
min(e.e, end)
);

// 3) Persiste el nuevo evento
bookings.emplace_back(start, end);
retorno verdadero;
}
};
`` `

■ *Las complejidades*
• **Tiempo:** `O(n)` por `book()`.
• **Espacio:** `O(n)`.

-...

## 📝 Blog Artículo – “El Bien, el Mal, y el Ugly de Mi Calendario II”

■ **Título: *LeetCode 731 – Mi Calendario II: Una profunda inmersión en la programación intervalida, la triple reserva y su próxima entrevista de codificación*

■ **Meta Descripción:** Master LeetCode 731 con soluciones Java, Python y C++. Aprenda las ofertas de dos listas vs. barrido, optimice su algoritmo, y asee su entrevista de ingeniería de software.

-...

#### ## 1down⃣ Por qué este problema se mete

- **Real-world relevance:** Programación, sistemas de reservas y asignación de recursos.
- Profundidad algorítmica** Detección de solapamiento, conteo de eventos, elección de estructura de datos.
- ** Popularidad de interés:** Preguntas frecuentes sobre entrevistas de la compañía tecnológica (Google, Amazon, Microsoft).

-...

#### 2down⃣ El Bien - Lo que funciona

Silencio Silencio Silencioso
Silencio----------
La solución de dos listas es intuitiva: una lista para todas las reservas, otra para superposiciones. No se necesitan bibliotecas externas. Silencio
Silencio ** Complejidad Determinacional** Silencio Con ≤ 1000 reservas, un `O(n)` El análisis por llamada es lo suficientemente rápido. Silencio
Silencio **Clear Edge Cases** ← Intervalos medio abiertos evitan las trampas como `[10,20]` & `[20,30]` siendo consideradas superposición. Silencio

-...

#### 3down⃣ El malo - donde se puede deslizar

Silencio Silencio Silencio
Silencio...
Silencio **Escáneos de línea** Silencio A medida que crecen las reservas, cada `libro()` se vuelve más lento (`O(n)`). Para grandes conjuntos de datos (millones de eventos), esto es inaceptable. Silencio
Silencio **Duplicar superposiciones** Silencio El enfoque ingenuo puede almacenar el mismo segmento de doble reserva varias veces (por ejemplo, si tres pares distintos comparten la misma solapa). Todavía es correcto, pero desperdicio. Silencio
Silencio **Pedido a la razón Sobre** Silencio Debugging bucles anidados puede ser confuso para los candidatos entrevistados bajo presión del tiempo. Silencio

-...

#### 4down⃣ La Ugly – Gotchas & Misconceptions

1. **Reservar la identidad errónea**
*Muchos candidatos incorrectamente sólo comprueban 'reservas' por solapamiento, asumiendo que dos eventos nunca se superponen dos veces. Esto pierde la lista de solapamiento *double* y acepta una triple reserva. *

2. **Uso de conjuntos de intervalores**
*Un patrón común pero buggy: almacena intervalos en un `HashSet` y prueba de solapamiento por iterating. No hace caso omiso del estado “ya de doble reserva”. *

3. **Sweep‐Line Implementation Errores**
*La solución `TreeMap`/`std::map` requiere un aumento cuidadoso / lógica del deterioro. Los errores en el límite medio abierto son frecuentes. Un único desaparecido `+1` puede hacer que su algoritmo mal. *

-...

### 4 pesquisa Sweep‐Line (TreeMap / std::map) – La alternativa elegante

``java
// Boceto Java (O(log n) por llamada)
clase MyCalendar Dos.
Árbol final privadoMapa realizadaInteger, Integer icono mapa = nuevo TreeMap incorrecta();
public boolean book(int start, int end) {
map.put(start, map.getOrDefault(start, 0) + 1);
map.put(end, map.getOrDefault(end, - 1);

int concurrentes = 0;
para (int v : mapa.values()) {}
concurrent += v;
si (concurrente 2) { // triple reserva detectada
// rollback
map.put(start, map.get(start) - 1);
si (map.get(start) == 0) map.remove(start);
map.put(end, map.get(end) + 1);
si (map.get(end) == 0) map.remove(end);
devolver falso;
}
}
retorno verdadero;
}
}
`` `

* Beneficios:* `O(log n)` por llamada, sin solapamientos duplicados, perfecto para entrevistadores que se preocupan por la optimización asintotica.

-...

### 5downs Time " Space Trade‐offs

TENIDO ANTERIOR TENIDO Tiempo por `book()` TENIDO Espacio TENIDO Cuándo utilizar
Silencio------------------------------------------
Silencio 2‐Lista Silencio `O(n)` Silencio `O(n)` ≤ 1000 llamadas, código limpio Silencio
TENIDO Sweep‐Line TENIDO `O(log n)` tención Grandes conjuntos de datos, entrevistadores favorecen los límites asintoticos

-...

#### 6down⃣ Test- Caso Cheat Sheet

Silencio Test TENIDO Resultado esperado
Silencio...
Silencioso `book(10,20)` → `true` Silencio
Silencioso `book(50,60)` → `true` peru No overlap Silencio
Silencio `book(10,40)` → `true` Silencio superpone una existente → doble reserva Silencio
Silencio `book(5,15)` → `false` Silencio Crearía una triple reserva con `[10,20]` ' [10,40]` Silencio
Silencio `book(25,55)` → `true` ¦ Sobrelaps only `[50,60]` → doble reserva Silencio

■ *Consejo:* Siempre incluya casos de borde donde los intervalos tocan pero no se superponen (`[20,30]` después de `[10,20]`).

-...

### 7ف⃣ Interview‐Ready Checklist

1. **Explica tu algoritmo** – dos listas o barrido, cualquiera que sea el código.
2. **Tiempo de Estado & espacio** – a los entrevistadores les encanta ver la complejidad de frente.
3. ** Casos de borde de mención** – intervalos medio abiertos, eventos de espalda a vuelta.
4. **Mostrar una carrera seca** – caminar a través de un pequeño ejemplo en la pizarra.
5. **Prepárate para variaciones** - ¿Y si el límite era 10^5 reservas? Usa el barrido.

-...

#### 8down⃣ Pensamiento final – *Job‐Entreview Takeaway*

“Una solución limpia y bien comunicada que cubre los casos de borde, explica la complejidad y puede ser fácilmente porteada entre Java, Python y C++ demuestra el pensamiento algoritmo y la disciplina de codificación de un candidato, exactamente lo que buscan los reclutadores.”*

■ Si usted puede caminar a través de este problema, explicar por qué usted eligió una estructura de datos particular, y discutir oficios, impresionará a los entrevistadores en cualquier empresa de tecnología importante.

-...

## 📹 Bonus: Video Walkthrough

*(En el blog real usted había incrustado un enlace de YouTube o GIF corto)*

■ “Esperame resolver LeetCode 731 en 5 minutos. Voy a mostrar el enfoque de dos listas, una variante de barrido, y destacar los obstáculos comunes. Echa un vistazo al vídeo completo aquí: > > https://youtu.be/YourVideoID confiar > >

-...

### 📈 SEO Checklist

- **Palabras clave principales:** *LeetCode 731*, *Mi Calendario II*, *MiCalendar 2*, *programación de intervalo*, *reserva detriple*
- **Palabras clave de segundo orden:** * Solución de Java*, *solución de Pitón*, *solución C++*, *respecto de interés*, *entrevista de ingenieros de software*, preguntas de entrevista*, *preparación de entrevistas de trabajo*
- **Headings (H1, H2, H3)** con palabras clave rociando.
- **No-texto para los fragmentos de código**: *Java MyCalendar Dos actividades*
- Enlaces internos** “Lea nuestra solución de barrido” → enlace al siguiente artículo.
- **Meta tags**: Título, descripción, lista de palabras clave.

-...

#### 🚀 Wrap‐Up

- **Tres soluciones limpias** en los idiomas de entrevista más populares.
- **Un artículo completo y optimizado de SEO** que cubre la relevancia del problema, opciones de diseño y consejos de entrevista.
- **Todo listo para pegar** en un currículum, post de LinkedIn, o kit de preparación para entrevistas.

Buena suerte aterrizando ese trabajo, su maestría de *Mi Calendario II* te hará pedazos!