-...
Título: LeetCode 691. Stickers to Spell Word -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. LeetCode 691 – **Stickers to Spell Word**

■ **Problema statement (shortened)* *
■ Usted tiene un suministro ilimitado de *n* diferentes pegatinas.
■ Cada pegatina es una palabra Inglés minúscula.
■ Usando las letras en las pegatinas (puedes cortar cualquier letra de cualquier pegatina, reorganizarlas, y puedes reutilizar una pegatina cualquier número de veces) debes deletrear una determinada cadena *target*.
■ Regrese el *minimo* número de pegatinas requeridas, o **‐1** si es imposible.

Silencio
Silencio...
Silencioso **n** Silencio 1 ≤ n ≤ 50
TENIDO **Platadores[i] longitud** TENIDO 1 ≤ 10
Silencioso ** longitud del objetivo** latitud 1 ≤ 15
Silencio **todos los personajes** Silencio

■ *Por qué importa*
■ Las limitaciones parecen pequeñas, pero el problema es NP‐hard.
■ Los entrevistadores aman este problema porque le obliga a pensar en *representación del estado* (bitmask, string, freq array) y *search* (BFS, DFS + memoización, DP).

-...

## 2. Panorama general de la solución

El enfoque estándar “más fácil de recordar” es un **Breadth‐First Search (BFS)** sobre *mantener cadenas de destino*.

1. **Sorta** cada pegatina y el objetivo alfabéticamente.
Esto permite que la operación `filter()` se ejecute en *O( WordPresstarget eterna + tenciónsticker habit)* escaneando ambas cadenas clasificadas.
2. Ponga el objetivo fijado en una cola.
Cada nivel del BFS representa usando una pegatina más.
3. Por cada estado, prueba cada pegatina:
*Use `filter()`* – eliminar las letras que la pegatina puede cubrir.
*Si no queda nada → hemos terminado* ( profundidad corriente + 1 pegatinas).
*Otros encubrimos el nuevo estado* si no lo hemos visto antes.
4. Si la cola vacía → imposible → volver **‐1**.

El BFS garantiza que la primera vez que alcanzamos una cadena vacía usamos el mínimo número de pegatinas.

-...

## 3. Código

## 3.1 Java – BFS (la solución “Gangjig”)

``java
importar java.util*;

Clase Solución {
public int minStickers(String[] stickers, String target) {
int n = pegatinas. longitud;

// Ordenar cada pegatina y el objetivo
target = sortChars(target);
para (int i = 0; i) no; ++i) pegatinas [i] = clasificarCartas(pegantes[i]);

Búsqueda realizadaString confía q = nuevo LinkedList recomendado();
Establecer:String titulada visitado = nuevo HashSet correctamente();

q.offer(target);
int steps = 0;

(!q.isEmpty()) {
int size = q.size();
pasos++; // estamos utilizando una pegatina más
mientras (tamaño... 0) {
Cura de cuerda = q.poll();
para (String st : stickers) {}
String nxt = filtro(cur, st);
si (nxt.isEmpty())) pasos de retorno;
si (!nxt.equals(cur) " visitado.add(nxt)) {}
q.offer(nxt);
}
}
}
}
retorno -1; // imposible
}

// Quitar cartas de st de a, ambos ordenados
filtro de cuerda privado (String a, String b) {
StringBuilder sb = nuevo StringBuilder();
int j = 0; // pointer into b
for (char c : a.toCharArray())) {}
booleano encontrado = falso;
mientras (j.)
si (b.charAt(j++) == c) { // consumir esta carta
encontrado = verdadero;
ruptura;
}
}
si (!found) sb.append(c);
}
devolver sb.toString();
}

privada String Chars(String s) {
char[] arr = s.toCharArray();
Arrays.sort(arr);
volver nuevo String(arr);
}
}
`` `

**Las complejidades* *

Silencio
Silencio...
Silencio **Hora** Silencioso `O( 2^m * n * m )` (caso inferior, *m* = longitud del objetivo) - pero prácticamente rápido para *m* ≤ 15. Silencio
Silencio **Espacio** Silencioso `O( 2^m )` para los estados visitados (caso inferior). Silencio

-...

### 3.2 Python – Memoised DFS / DP (bit-mask)

La implementación de Python utiliza una memoización *recursiva* con un **bitmask** de los caracteres de destino restantes.
Este es el enfoque más conciso pero altamente eficiente.

``python
Solución de clase:
def minStickers(self, stickers: list[str], target: str) - Conf int:
desde functools import lru_cache

# Pegatinas de procesamiento previo en contadores de frecuencia
m = len(target)
target_letters = list(target)

# Construir una lista de máscaras de pegatina (máquina de letras que puede suministrar)
máscaras = []
para st en pegatinas:
máscara = 0
para ch en set(st):
mascarilla TENIDO= 1 TENIDO (ord(ch) - 97)
máscaras.append(mask)

@lru_cache(None)
def dfs(state: int) - título int:
si estado == 0:
retorno 0
as = flotante('inf')
Prueba cada pegatina
para máscaras en máscaras:
# If sticker does not cover any needed letter, skip
si máscara " estado == 0:
continuar
# Build new state after using this sticker
new_state = state
i, ch in enumerate(target_letters):
si el estado " (1 " se hizo i) y (mask " (1 " se hizo (ord(ch) - 97)):
new_state < =(1 >
as = min(ans, 1 + dfs(new_state)
Retorno

res = dfs(1  se hizo realidad m) - 1)
retorno -1 si res == flotante('inf')
`` `

**Las complejidades* *

Silencio
Silencio...
Silencio ** Tiempo** Silencioso `O( 2^m * n )` (m ≤ 15 → 32 768 estados)
Silencioso **Espacio** Silencioso `O( 2^m )` para la fusión + pila de recursión

-...

### 3.3 C++ – DP with Bitmask (iterative)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minStickers(vector identificados con pegatinas, objetivo de cadena) {}
int m = target.size();
int full = (1 < > > ) - 1;

/ / / Pre-compute sticker máscaras
vector máscaras;
para (auto pulsar : pegatinas) {}
int mask = 0;
para (carc : st) máscara Silencio= 1 ); Se hizo (c - 'a');
máscaras.push_back(mask);
}

INF = 1e9;
vector implicado dp(1 )
dp[0] = 0; // no se necesitan cartas → 0 stickers

para (incluido estado = 0; estado = total; + estado) {}
si (dp[state] == INF) continúan;
para (int smask : máscaras) {
int new_state = state;
// Trate de cubrir cada carta restante con esta pegatina
para (int i = 0; i) {}
si (!(Estado " 1 " ) " )) continúan; // ya cubiertos
si (smask " (1 " )
new_state &= ~(1  Se hizo i); // remove it
}
dp[new_state] = min(dp[new_state], dp[state] + 1);
}
}
dp[full] == INF ? -1 : dp[full];
}
};
`` `

**Las complejidades* *

Silencio
Silencio...
Silencio **Tiempo** Silencioso `O( 2^m * n * m )` – con *m* ≤ 15 todavía rápido
Silencio.

-...

## 4. Blog Artículo
*(SEO-optimized – “Stickers to Spell Word” + “LeetCode 691” + “Interview Prep”)*

-...

### 🚀 **Stickers to Spell Word: The Good, The Bad, and The Ugly* *

■ **Keywords** – *LeetCode 691*, *Stickers to Spell Word*, *DP bitmask*, *BFS solution*, *coding interview*, *algorithm interview questions*, *job interview tips*, *Java BFS*, *Python DP*, *C++ bitmask*.

-...

#### ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## ## #1 ¿Cuál es el problema?

Te dan un puñado de pegatinas, cada una una una palabra pequeña.
Su objetivo: ** cortar letras** de estas pegatinas (puedes cortar *cualquier letra*, reordenarlos, y utilizar pegatinas cualquier número de veces) para deletrear una palabra objetivo.

*Retorna el número mínimo de pegatinas necesarias o -1 si no se puede hacer. *

-...

##### 2down⃣ ¿Por qué es tan importante en entrevistas?

- Profundidad algorítmica**: Toca sobre *comprensión del estado*, *bitmask DP*, *BFS sobre cuerdas* – todos los conceptos básicos que los entrevistadores aman.
- ¿Por qué? Usted tiene que considerar * cartas no cubiertas*, *pegadoras duplicadas*, * cobertura superpuesta*.
- Cambio de espacio-tiempo**: Resolverlo ingenuamente puede explotar; encontrar una representación inteligente y compacta es la clave.

Si logras esta pregunta, impresionarás a los reclutadores con tanto *coding* como *design* chops.

-...

##### 3down⃣ El Bien – Intuición " Lo que funciona

1. **Ordenar simplificar la coincidencia* *
Ordenar pegatinas y el objetivo le permite correr `filter()` en tiempo lineal.
No hay bucles anidados sobre personajes – sólo dos punteros.

2. **BFS garantiza la óptimabilidad* *
Cada capa de BFS representa *utilizando una pegatina más*.
La primera vez que golpeamos una cadena de destino vacía es la respuesta.

3. ** Compresión del Estado con mascaras* *
Las soluciones DP de Python y C++ comprimen las letras restantes en un solo entero (`1 > se selecciona m`).
Sólo 2^15 = 32.768 estados – diminuto y rápido.

4. **La movilización corta la recursión**
En Python, `@lru_cache` almacena resultados para cada subproblema, convirtiendo un DFS exponencial en una búsqueda manejable.

-...

##### 4down⃣ Los malos – saltos comunes

¿Por qué no se puede arreglar la vida?
Silencio--------------------------
Silencio **Usando una fila de cuerdas** Silencio Strings puede ser largo (hasta 15 chars) y muchos duplicados – soplado de memoria. Use * strings surtidos* + a `Set` para seguir visitado. Silencio
TEN **Re-computing sticker masks each DFS call** Silencio Adds *O(n)* overhead for every recursive step. ← Pre-compute un bitmask por sticker una vez. Silencio
Silencio **Ignorando pegatinas duplicadas** Silencio Podrías perder el tiempo explorando la misma pegatina de nuevo. ← Pegatinas deduplicadas o utilizar una 'Set' de máscaras. Silencio
Silencio **Caso base equivocado en DFS** latitud Regresar 0 para estado no vacío conduce a bucles infinitos. Caso básico: `estado == 0 → 0 stickers`. Silencio
Silencio **No manejar casos imposibles** Silencio Regresar `float('inf')` directamente puede causar desbordamiento. tención después del DP, comprobar por `INF ' y regresar -1.

-...

##### 5down⃣ El Ugly – Cuando la complejidad se mueve salvaje

Si intentas generar **todas las combinaciones** de pegatinas, crearás *exponential* árboles de búsqueda:

- Cada estado de cadena puede ramificarse en *n* pegatinas → `O(n^m)` caminos.
- Sin una máscara inteligente o un truco de cadena ordenados, usted va a tiempo fuera en objetivos más grandes.

**Solución**:
Mantenga su *representación del estado* apretado (mascara de bits o cadenas ordenadas) y evite el trabajo duplicado.
Esa es la salsa secreta para convertir “muy” en “eficiente”.

-...

##### 6down⃣ Quick‐ Inicio: ¿Qué idioma prefieres?

Silencio Lengua Silencio Lo que usted aprenderá Silencio Código snippet
Silencio----------------------------
Silencio **Java (BFS)** Silencio La cadena de dos puntos coincide con la búsqueda de colas en silencio. Silencio
Silencio **Python (DP)** Silencio Recursion + bitmask + `lru_cache` Silencio `[Python code]` Silencio
Silencio **C++ (iterative DP)**

Escoge el que coincide con tu pila de entrevistas.

-...

##### 6down⃣ Final Pensamiento: Mostrar *Diseño* No solo *Aplicación*

Al responder en una entrevista en vivo:

1. *Explicar la representación del estado* (¿por qué bitmask? ¿Por qué las cuerdas clasificadas?)
2. **Walk through BFS layers** – enfatiza la optimización.
3. **Mention pruning " memoisation** – show you know the time‐space trade‐off.
4. ** Casos de borde de separación** – prueba escenarios “imposibles” y “single‐letter”.

Usted convertirá esta pregunta de codificación en una narrativa **diseñada** que los reclutadores aman.

-...

##### 🎯 **Takeaway**

- LeetCode 691 es *una de las mejores* preguntas de entrevista para * buscadores de empleo*.
- Usar **BFS** con cadenas clasificadas * o * ** bitmask DP** con memoización.
Mantenga el código limpio, los estados pequeños y los casos de base correctos.

-...

■ **Listo para practicar? #
■ Cerrar el repo, ejecutar las soluciones Java, Python y C++, y probar contra los casos oficiales de prueba LeetCode.
■ Cuando estés cómodo, agrega un paso *deduplicación* e intenta reducir la memoria más allá – así es como vas de *bueno* a *grande*.

¡Feliz codificación! ▪

-...

*(End of article)*

-...

## 5. Conclusión

- Cubrimos tres soluciones idiomáticas: Java BFS, Python memoised DFS, C+++ iterative DP.
- La implementación de Java es un favorito de entrevistas “real”, concisa, rápida y fácil de explicar.
- Los fragmentos Python y C++ muestran el poder de la compresión del estado de bitmask* – el truco algoritmo "último" para LeetCode 691.
- El artículo del blog explica por qué el problema importa, cómo evitar las trampas, y cómo enmarcar su respuesta para los reclutadores.

Happy interviewing, and may your job offers come *in just the right number of stickers*