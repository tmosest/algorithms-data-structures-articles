-...
Título: LeetCode 1776. Flota de coches II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# 1776. Flota de coches II – Master the Hard LeetCode Problema (Java ← Python tención C++)

■ **Listo para aterrizar esa tecnología-interview? * *
■ Este post le lleva a través de la solución más eficiente para LeetCode 1776 “Car Fleet II” utilizando una pila monotónica. Te mostraremos código limpio en **Java, Python, y C++**, explicar por qué es O(n), y resaltar el *bueno, el malo, y el feo* de este clásico desafío algoritmo.

-...

Problema Recap

■ **Carreras en una carretera de una calle* *
■ Hay autos que viajan en la misma dirección.
■ Cada coche `i' comienza en `posicion[i]` con velocidad[i].
■ Las posiciones están aumentando estrictamente ( " posición[i] " ).
■ Cuando un coche más rápido atrapa una más lenta, se fusionan en una sola “fleeta” que viaja a la velocidad del coche más lento.
■
■ **Retorno** un array `respuesta` donde `respuesta[i]` es el tiempo (en segundos) cuando el coche `i` primero colisiona con el coche siguiente, o `-1` si nunca choca.

■ **Constraints**
≤ 105
[i], velocidad[i] ≤ 106 `

■ **Caso de ensayo clínico* *
" texto
■ Entrada: coches = [[1,2],[2,1],[4,3],[7,2]]
[1.00000,-1.00000,3.00000,-1.00000]
" `

-...

## 🧠 The Core Idea – Monotonic Stack

La observación clave:

1. **Sólo coches más rápidos pueden alcanzar los más lentos por delante. #
2. Cuando un coche alcanza, hereda la velocidad del coche más lento (el que choca con).
3. Por lo tanto, desde el coche más derecho a la izquierda, mantenemos una pila **monotónica** de candidatos con los que el coche actual puede chocar potencialmente.
*La pila almacena índices de coches que son estrictamente más lentos que el coche debajo de ellos en la pila. *

Para cada coche (traversando de derecha a izquierda):

- Los coches pop de la pila que:
- Son más rápidos que el coche actual (sin colisión), **o**
- Collide **después**, el coche saltado ya ha chocado con otra persona (de ahí sus cambios de velocidad “eficaces”.

- El primer coche que queda en la pila que satisface la condición de colisión es el que el coche actual chocará primero.
- Si no queda ese coche, la respuesta es `-1`.

Este algoritmo funciona en **O(n)** tiempo porque cada coche es empujado y saltado a la mayoría de la vez.

-...

## 💻 Code Snippets

A continuación se presentan implementaciones limpias y listas de producción en **Java, Python y C++**. Cada uno sigue la misma lógica monotónica.

-...

### 1. Java (Clean, O(n) Monotonic Stack)

``java
importar java.util*;

Solución de la clase pública {}
public double[] getCollisionTimes(int[][] coches) {
int n = coches.length;
doble[] ans = nuevo doble[n];
Arrays.fill(ans, -1.0);

Deque cumplióInteger confianza stack = nuevo ArrayDeque correspondió();

para (int i = n - 1; i 0; i--) {
int posI = coches[i][0], spdI = coches[i][1];

mientras (!stack.isEmpty()) {}
int j = stack.peekLast();
int posJ = cars[j][0], spdJ = cars[j][1];

// Si el coche actual es más lento o igual, nunca atrapará j
si se rompe (spdI) = spdJ;

doble t = (doble) (posJ - posI) / (spdI - spdJ);

// Si J nunca colisiona, o la colisión sucede antes de la colisión de j
si (ans[j] == -1.0 TENIDO ANTERITO T ANTE= ans[j] {
as[i] = t;
ruptura;
. ♫ ... {
// j cambiará la velocidad antes de que lo pille → descarte j
stack.pollLast();
}
}
stack.offerLast(i);
}
devolver los ans;
}
}
`` `

-...

### 2. Python (3.9+)

``python
de la importación Lista

Solución de clase:
def getCollision Times(self, cars: List[List[int]) - No. List[float]:
n = len(carros)
ans = [-1.0]
pila: List[int] = [] # índices de coches candidatos

para i en rango(n - 1, -1, -1):
pos_i, spd_i = coches[i]
mientras que la pila:
j = pila[-1]
pos_j, spd_j = coches[j]

si spd_i 0 0 = spd_j: # no puede ponerse al día
descanso

t = (pos_j - pos_i) / (spd_i - spd_j)

si ans[j] == -1.0 o t == ans[j]:
ans[i] = t
descanso
más:
pila.pop() # j cambia velocidad antes de que lo pille

stack.append(i)
Retorno
`` `

-...

### 3. C++ (GNU+17)

``cpp
Clase Solución {
public:
vector asignadosdouble título getCollisionTimes(vector seleccionadovector fielint implicando automóviles) {
int n = coches.size();
vector alcanzadodouble título ans(n, -1.0);
vector Nombramiento de indices

para (int i = n - 1; i 0; --i) {
int pos_i = cars[i][0], spd_i = cars[i][1];
(!st.empty())) {}
int j = st.back();
int pos_j = cars[j][0], spd_j = cars[j][1];

si (spd_i <= spd_j) romper; // no puede atrapar

doble t = doble(pos_j - pos_i) / (spd_i - spd_j);

si (ans[j] ■ 0 TENIDO TENIDO ANTE= ans[j] {
as[i] = t;
ruptura;
. ♫ ... {
st.pop_back(); // j cambiará la velocidad primero
}
}
st.push_back(i);
}
devolver los ans;
}
};
`` `

-...

## 📈 Complexity Analysis

Silencio Silencio Silencio Silencio
Silencio----------------
Silencio Principal bucle (traversing `n` cars) Silencio `O(n)` Silencio `O(n)` (stack + array de respuesta)
Silencio Cada coche empujado / picado una vez

*Overall:* **Time O(n), Space O(n)** – óptimo para `n ≤ 105`.

-...

Bien, mal, feo.

Silencio Silencio
Silencio------------Prince------
Silencio **Concepto** ← Elegante pila monotónica; tiempo lineal ← Requiere cuidadoso manejo de “coliciones de futuro”
Silencio **Aplicación** Silencioso Compacto; fácil de depurar Silencio Debe mantener correctamente `mientras `condiciones Silencio Off‐por-uno errores, división por cero si las velocidades son iguales
Silencio **Readability** Silencio Nombres variables claros (`ans`, `st`) ← La lógica de Stack puede confundir a los principiantes ← Sobre-ingeniería (por ejemplo, almacenar datos adicionales)
Silencio **Edge Cases** Silencio Handles all `-1` cases ¦Necesidad de comprobar `spd_i= spd_j` para evitar la división por cero TENIDO Olvidar comparar contra `ans[j]` conduce a resultados incorrectos

■ **Consejo:** Siempre caminar a través de la pila con un pequeño ejemplo. Visualizar los estados de la pila ayuda a prevenir errores.

-...

## 🎯 Interview‐Ready Tips

1. **Declarar la observación primero.** Explique que un coche más rápido sólo puede coger uno más lento y que después de la captura, la flota se mueve a la velocidad más lenta.
2. **Describa la pila monotónica.** Ponga de relieve que la pila tiene “potential colliders” y por qué pasamos de derecha a izquierda.
3. *Espera un caso de prueba.* Mostrar cómo evoluciona la pila paso a paso.
4. **Complexity discussion.** Highlight `O(n)` time ' `O(n)` space, and why no `O(n2)` nest loops are needed.
5. Manejo de edge. Mention the check `spd_i ANTE= spd_j` and the comparison with `ans[j]`.

-...

## 📌 SEO‐Optimized Meta Data

``html
< > > > > > > > > > > >
Contenido de "Descripción" = "Master the LeetCode hard problem Car Fleet II. Obtenga soluciones Java, Python y C++ con un enfoque monotónico de pila. Aprende el algoritmo, la complejidad y los consejos de entrevista."
"LeetCode 1776, Car Fleet" II, solución Java, solución Python, solución C++, pila monotónica, entrevista de algoritmos, entrevista de codificación, problema de flota de autos"
`` `

-...

## ⋅ Conclusion

Car Fleet II es un ejemplo de libro de texto de **utilizando una pila monotónica para transformar un problema aparentemente cuadrático en uno lineal**. El truco radica en darse cuenta de que después de una colisión, la velocidad "bloquea" al coche más lento, y que cualquier coche más rápido detrás debe primero limpiar todos los coches más rápidos antes de considerar colisiones.

Con los fragmentos de código arriba y las ideas en este post, usted está listo para:

- **Solve el problema de manera eficiente** en tu idioma elegido.
- Explique el algoritmo convenciendo a un entrevistador.
- **Mostrar su codificación-limpieza** utilizando implementaciones claras y libres de errores.

Buena suerte, y que las flotas estén siempre a su favor! 🚀