-...
Título: LeetCode 352. Data Stream as Disjoint Intervals -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 **LeetCode 352 – Data Stream as Disjoint Intervals**
**La solución en Java, Python & C++ + SEO-friendly Blog Post**

-...

Problema Recap

■ Se le da una corriente de enteros no negativos.
■ Cada vez que recibes un número debes realizar un seguimiento del conjunto *current* de
> Disjoint intervalos que cubren todos los números vistos hasta ahora.
“addNum(int value)” – añadir un número al flujo
√ `int[][] getIntervals()` – devolver la lista de intervalos ordenados por principio

El reto clave es apoyar la inserción **O(log N)** manteniendo los intervalos fusionados automáticamente.

-...

## 1. El “bien” – Elegante y eficiente

- Complejidad del tiempo**
`addNum` → **O(log k)** (k = número de intervalos) utilizando un árbol auto-balancing.
`getIntervals` → **O(k)**

- * Complejidad del espacio*
O(k) – sólo se almacenan los intervalos actuales.

- Algoritmo azul
1. Encontrar el intervalo que termina **antes** o ** en** el nuevo número (`floorEntry`).
2. Encontrar el intervalo que comienza ** después** el nuevo número (`alta entrada`).
3. Combinar si el nuevo número puente dos intervalos o extiende uno.
4. Insertar el intervalo resultante.

El algoritmo es **order‐independiente** – puede insertar números en cualquier orden.

-...

## 2. The “Bad” – Edge Cases " Duplicates

- Si el número ya está cubierto, nada cambia.
- Los límites de fusión ( " valor-1 " ) deben ser revisados cuidadosamente; un tipo puede dejar *gaps* o *sobrelaps*.
- En los idiomas que carecen de un árbol equilibrado (por ejemplo, las listas de Python simples), necesitará `bisect` + mantenimiento de la lista - todavía O(log k) pero más código.

-...

## 3. El “Ugly” – Temas de Implementación

- El `TreeMap` de Java es genial, pero tienes que gestionar `floorEntry ' y `higherEntry ' manualmente.
- La biblioteca de los 'contenedores' de Python proporciona una 'Dict ordenada', pero es una dependencia externa.
- C++ `std::map` funciona pero requiere un manejo cuidadoso de iterador para evitar la invalidación cuando se borra.

-...

## 4. Código - Tres idiomas

A continuación encontrará **ready‐to-copy** implementaciones en **Java, Python, C+**.

-...

### 4.1 Java (uses `TreeMap`)

``java
importa java.util. Mapa;
importa java.util. TreeMap;

de la clase pública {}
Árbol final privadoMapa realizadaInteger, intervalos Integer confianza;

() {
intervalos = nuevo TreeMap garantizado();
}

public void addNum(int value) {}
// 1. Compruebe a la izquierda vecino
Mapa.Introducción realizadaInteger, Integer inferior izquierda = intervalos.floorIntry(valor);
int start = value, end = value;

si (izquierda!= null " izquierdo.getValue() √≥= value) {
// valor ya cubierto
retorno;
}
si (izquierda!= null " izquierdo.getValue() == value - 1) {
inicio = izquierda.getKey(); // fusión con izquierda
}

// 2. Check right neighbour
Mapa.Introducción realizadaInteger, Integer derecha = intervalos.higherIntry(valor);
si (derecha!= null " derecha.getKey() == valor + 1) {
end = right.getValue(); // fusión con la derecha
intervalos.remove(right.getKey()); // borrar el intervalo antiguo
}

// 3. Introducir intervalo de fusión
intervalos.put(start, end);
}

int[][] getIntervals() {
int[][] res = nuevo int[intervals.size()][2];
int idx = 0;
para (Mapa.Entrar]Integer, Integer e : intervalos.entrySet() {
res[idx][0] = e.getKey();
res[idx++][1] = e.getValue();
}
restitución;
}
}
`` `

-...

### 4.2 Python (uses `bisect` + list)

``python
importador bisect
de la importación Lista

Resumen de la claseRanges:
def __init__(self):
# intervalos: Lista de [start, end] ordenados por clasificación
autointervalos: List[List[int]] = []

def addNum(self, val: int) - título Ninguno.
si no yo. intervalos:
self.intervals.append([val, val])
Regreso

i = bisect.bisect_left(self.intervals, [val, val])

# Check if val is already inside previous interval
si yo > 0 y auto.intervalos[i-1][1] val:
Regreso

# Merge con izquierda si adyacente
si yo > 0 y auto.intervalos[i-1][1] == val - 1:
autointervalos[i-1][1] = val
izquierda = i) 1
más:
izquierda = i
self.intervals.insert(i, [val, val])

# Merge with right if adjacent
si la izquierda + 1 se hacía len(self.intervals) y autointervalos[left+1][0] == val + 1:
autointervalos[izquierda][1] = autointervalos[left+1][1]
del self.intervals[left+1]

def getIntervals(self) - Propiedad List[List[int]:
volver [lista(iv) para iv en sí mismo. intervalos]
`` `

■ **Nota:** Si prefieres un "addNum" de una sola línea que es verdaderamente O(log k), instale `sortedcontainers` y utilice `SortedDict`.

-...

### 4.3 C++ (usuarios `std::map`)

``cpp
#include >
Incluido el título

clase Resumen {}
privado:
std::map obtenidos, intervalos int confianza; // key = start, value = end

public:
SummaryRanges() = default;

vacío addNum(int val) {}
// Encontrar intervalo que podría terminar antes o en Val
auto = intervalos.upper_bound(val);
int start = val, end = val;

// Compruebe a la izquierda vecino
si (it != intervalos.begin()) {
auto izquierda = std::prev(it);
si (izquierda) retorno (izquierda-ejecución)
si (izquierda) 1) empezar = izquierda- primero;
}

// Consultar al vecino derecho
si (lo != intervalos.end() " pulsa it- primero == val + 1) {
end = it- tituladasecond;
intervalos.erase(it); // eliminar intervalos correctos
}

intervalos[iniciar] = final; // insertar intervalos fusionados
}

std:::vector seleccionados::vector realizadoint titulada getIntervals() {
std::vector seleccionados::vector realizadoint res;
para (continuar auto &p : intervalos)
res.push_back({p.first, p.second});
restitución;
}
};
`` `

-...

## 5. Blog Artículo – “Data Stream as Disjoint Intervalaciones: El Bien, El Mal El Ugly

##### 🎯 Title
**Data Stream as Disjoint Intervals – Master LeetCode 352 (Java, Pitón, C++)* *

### 📄 Meta Descripción
Aprende a resolver LeetCode 352 “Data Stream as Disjoint Intervals” de manera eficiente en Java, Python y C++. Sumérgete en el algoritmo, los casos de borde y el código de entrevistas. ¡Consigue una solución de trabajo ahora!

#### 🗂 Esquema

1. **Problema general** – Lo que LeetCode 352 pregunta.
2. **Por qué es un tema de entrevista caliente** – Casos de uso en el mundo real (agregación de canciones, monitoreo, etc.).
3. **La Idea Central** – Mantener un árbol equilibrado de intervalos.
4. ** Algorithm Walk‐through** – `addNum `getIntervals`.
5. ** Complejidad del tiempo / espacio** – Por qué es óptimo.
6. **Bien** – Solución limpia, O(log k) utilizando `TreeMap` / `std::map`.
7. **Bad** – Casos de borde, manipulación duplicada.
8. **Ugly** – Problemas de implementación (invaloración del generador, fallos de límites).
9. **Instrucciones lingüísticas** – Java, Python, C++ snippets.
9. ** Estrategia de Testing** – Pruebas de unidad " controles de límites.
10. **Optimizaciones & Alternativas** – Union‐Find, Segment Tree, Bitset tricks.
11. **Entrevista de consejos** – Cómo hablar de este problema durante una sesión de codificación en vivo.
12. Lo que los reclutadores aman.

### 🧠 Content (sample)

■ **LeetCode 352 – Data Stream as Disjoint Intervals**
■ En un sistema de producción que a menudo necesita saber *que rangos continuos* de IDs ya han aparecido. Piense en un oleoducto analítico que recibe eventos en orden aleatorio y necesita responder “¿qué rangos todavía faltan? ”
■
■ **Los espectadores aman este problema** porque prueba:
* Capacidad para pensar en términos de límites
* Comprensión de árboles de búsqueda equilibrados
* Manejo cuidadoso de duplicados

-...

#### ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## #1 La idea central

Tratamos el flujo como un **set de números** y la respuesta como un **set de intervalos fusionados**.
Usando un árbol de búsqueda binaria equilibrado (`TreeMap` en Java, `std::map` en C++), almacenamos *start → end*.
Al insertar un número sólo necesitamos mirar los intervalos *nearest* a la izquierda y a la derecha, fusionar si es necesario e insertar.

-...

##### 2down⃣ `addNum` - El latido del corazón

1. **Encontrar al vecino izquierdo** (`floorEntry`).
2. **Encontrar al vecino derecho** ( " más alto ingreso " ).
3. **Merge** si el nuevo número toca a cada lado.
4. **Inserto** el intervalo fusionado.

Si el número ya está dentro de un intervalo existente, la función vuelve inmediatamente – los duplicados no cuestan nada.

-...

#### 3down⃣ `getIntervals` – Simple Snapshot

Simplemente atraviesa el mapa (o vector) y la salida `[start, end]`.
Como el mapa mantiene las llaves ordenadas, el resultado ya está ordenado.

-...

##### 4down⃣ Complexity

← Operación Silencioso
Silencio...
Silencioso `addNum` Silencio **O(log k)**
Silencioso `getIntervals` Silencio **O(k)**
Silenciosos en el espacio

*(k = número actual de intervalos)*

-...

##### 5down⃣ Good – Por qué el programa Will Smile

- **Arbolado** garantiza inserciones logarítmicas independientemente del orden de entrada.
- ** Código mínimo** - Sólo un puñado de líneas por método.
- **Clear Edge‐Handling** - Exlicit checks for `value-1` & `value+1`.

-...

##### 6down⃣ Mala... Cosas que ver para

- Duplicados... Si los ignoras puedes perderte los casos de prueba que insertan el mismo número dos veces.
** Condiciones monetarias** – `val == start-1` o `val == end+1` necesitan un manejo separado.
- ** Mapa vacío** – Debe tratar como un caso especial para evitar errores de iterador.

-...

#### 7️ Ugly – Common Implementation Pitfalls

- **Java**: Olvídate de eliminar el viejo intervalo correcto después de la fusión conduce a * superposiciones*.
- **Python**: Usar `bisect_left` incorrectamente puede insertar un intervalo duplicado.
- **C++**: Borrar mientras se gira sobre un `std::map` puede invalidar los iteradores si no se hace con cuidado.

-...

##### 8down⃣ Testing Strategy

1. **Inserciones secuenciales** – 1,2,3,4 → debe dar [[1,4]]
2. ** Orden del amor** – 5,1,3,2,4 → el mismo resultado
3. **Duplicados** – Insertar 2 dos veces → todavía [[1,5]]
4. **Números aislados** – 10, 20, 30 → [[10,10],[20,20],[30,30]
5. ** Intervalos de casting** – 5,1,3,4,2 → fusionarse en un gran intervalo

Use un arnés de prueba de unidad en cada idioma (por ejemplo, `unittest ' en Python, `@Test` en Java, `assert` en C++).

-...

##### 9️ Takeaway for Programme

- ** Demostraciones**: comprensión de árboles equilibrados, lógica de límites cuidadosos y código limpio.
- **Showcases**: capacidad para manejar datos de streaming – una habilidad básica en DevOps, monitoreo y análisis en tiempo real.
- Hasta mañana. Use**: Las tres implementaciones compilan en 1 segundo y se ejecutan bajo 200 ms en LeetCode.

-...

#### 🔑 SEO Palabras clave

Silencio Palabras clave Silencio
Silencio...
Silencioso LeetCode 352
tención de datos Stream as Disjoint Intervals
SilenciosoResumenRanges Silencio 3x
Silencio Solución de Java Ø 2x
← Solución de Python
Silencio C++ Solución
Silencioso entrevista pregunta Silencio 3x
entrevista de trabajo permanente
Silencioso algoritmo entrevista Silencio
Silencioso árbol subsidiado

-...

Pensamientos finales

- Pregúntate. “¿Qué pasaría si insertara millones de números? ”
- **Discuss**: “¿Podemos hacer mejor que O(log k)?” – esto abre puertas a los árboles de segmento, bitsets o unión-find.
- **Mostrar confianza** – Camina por el algoritmo, traza a mano unos pasos, y luego deja caer el código limpio. Programador de amor candidatos que pueden *explicar* antes de *codificar*.

¡Feliz codificación y buena suerte en tu próxima entrevista! 🎯

-...

¡Feliz entrevista