-...
Título: LeetCode 3544. Subtree Inversion Sum -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. Recaptación de problemas

■ ** Suma de inversión de subárbol** – LeetCode 3544
■
■ Le dan un árbol no dirigido arraigado en el nodo 0.
■
* `edges` – los bordes de los árboles.
■
* `nums` – valor almacenado en cada nodo.
■
* " k " – la distancia mínima que debe separar dos nodos invertidos cuando uno es un ancestro del otro.
■
■ Cuando un nodo es *invertido*, los valores de **todo nodo en su subárbol** se multiplican por −1.
■
■ Encontrar la suma **maximum posible** de todos los valores del nodo después de realizar cualquier conjunto de inversiones que obedecen la regla de distancia.

Las restricciones ( " n ≤ 5·104 " , " k ≤ 50 " ) hacen imposible una fuerza bruta ingenua.
La observación clave es que la decisión “invertir este subárbol o no” sólo interactúa con *ancesores* que son en la mayoría de los bordes de la “k–1” arriba – nada más abajo de la línea.
Eso da un DP limpio en los árboles.



----------------------------------------------------

## 2. Intuición – 3-D DP

Caminamos el árbol en una orden DFS.
Por cada nodo 'u' recordamos dos cosas:

Silencioso parameter Silencio significa Silencio
Silencio...
Silencioso `dist` (`0 ... k‐1`) TENER cuántos bordes quedan hasta que se nos permita volver a invertir **en el subárbol de 'u'.
Si 'dist > No podemos invertir. Si `dist = 0` podemos elegir invertir `u` o no. Silencio
TENIDO `sign` (`+1 / –1`) TENIENDO el signo de que los valores del subárbol arraigados en `U` actualmente llevan debido a las inversiones realizadas **above** `u`.
Si un antepasado superior fue invertido, todos sus descendientes tienen el signo opuesto. Silencio

`dp[u][dist][sign]` – la suma máxima alcanzable de todo el subárbol de `u`
bajo esas dos limitaciones.

Transiciones:

`` `
si el destilado 0 // inversión de u está prohibido
resultado = signo * nums[u] +  Elisabeth dp[child][dist-1][sign]
// dist == 0, podemos decidir
// 1) no invertir u
no Invertir = signo * nums[u] +  Elisabeth dp[child][0][sign]
// 2) invert u
invert = -signa * nums[u] +  Elisabeth dp[child][k-1][-sign]
resultado = max(notInvert, invert)
`` `

El caso base es una hoja: las mismas fórmulas todavía funcionan porque el bucle sobre los niños está vacío.



----------------------------------------------------

## 3. Prueba de corrección

Demostramos que el algoritmo devuelve la suma máxima posible.

### Lemma 1
Para cualquier nodo `u`, cualquier `dista (0≤dist madek)` y cualquier `sign`, `dp[u][dist][sign]` iguala la suma máxima que se puede lograr dentro del subárbol de `u`, respetando

* la regla de distancia para las inversiones dentro del subárbol, **y**
* el hecho de que todos los valores fuera del subárbol ya tienen el signo global `sign`.

Proof.

Inducción sobre la altura del subárbol.

*Base (leaf). *
El subárbol de una hoja contiene sólo nodo `u`.
Si `distrito0` la hoja no puede ser invertida, por lo que la única suma posible es `sign·nums[u]`.
Si `dist=0`, la hoja puede ser invertida o no - el algoritmo elige el mayor de `sign·nums[u]` y `-sign·nums[u]`.
Por lo tanto, la entrada de la tabla equivale al óptimo.

* Paso de inducción. *
Supongamos que la lema tiene para todos los hijos apropiados de `u`.
Cuando `dist ratio0`, nodo dentro del subárbol de 'u' puede ser invertido (por definición de `dist`), por lo que la suma óptima es simplemente la suma de las sumas óptimas de los niños con el mismo `dist-1' y sin cambios `sign`.
Por hipótesis de inducción cada niño aporta su suma óptima, por lo que el algoritmo calcula el total óptimo.

Cuando `dist=0`, podemos dejar `u` sin cambios o invertirlo.
En ambos casos el valor óptimo para cada subárbol infantil sigue siendo el valor óptimo con el par correspondiente `(dist, sign)`:
* sin inversión: los niños obtienen `dist=0` y el mismo `sign`;
* con inversión: los niños consiguen `dist=k-1` y voltearon `sign`.
Por hipótesis de inducción cada niño aporta su valor óptimo para el par elegido, por lo que el algoritmo `max` elige el óptimo global.

Por lo tanto, la lema sostiene para `u`. ∎



### Lemma 2
`dp[0][0][+1]` equivale a la suma máxima alcanzable de todo el árbol.

Proof.

Nodo 0 es la raíz, por lo que ninguna inversión de ancestro influye en ella → global `sign = +1`.
Se permite la primera inversión posible en la raíz, por lo tanto `dist = 0`.
Por Lemma 1, `dp[0][0][+1]` es exactamente la mejor suma alcanzable para todo el árbol. ∎



### Theorem
El algoritmo devuelve la suma máxima posible después de cualquier conjunto de inversiones admisible.

Proof.

El algoritmo devuelve `dp[0][0][+1]`.
Por Lemma 2 este valor equivale al óptimo para todo el árbol. ∎



----------------------------------------------------

## 4. Análisis de la complejidad

TENIDO ANTERIOR ANTERIOR ANTERIOR
Silencio...
Silencio para construir listas de adyacency Silencio
TENIDO DP table size Silencio `n · k · 2 ` (Ω 5 × 106 para el peor de los casos)
Silencio Cada célula DP computada una vez que vivieron `O(k · 2)` por nodo (niños bucle sólo una vez)
TENIDO Tiempo total TENIDO `O(n · k)` ♥ 2.5 × 106 operaciones
TENIDA Memoria adicional TENIDO `O(n · k)` para la tabla DP + listas de adyacency TEN

Tanto el tiempo como la memoria encajan cómodamente en los límites de LeetCode.



----------------------------------------------------

## 5. Implementaciones de referencia

A continuación encontrará **Java**, **Python**, y **C++** implementaciones que siguen la misma lógica DP.
Los tres códigos exponen el mismo método público:

``java
public long subtreeInversionSum(int[][] edges, int[] nums, int k);
`` `

``python
Solución de clase:
def subtreeInversionSum(self, edges: List[List[int], nums: List[int], k: int) - título int:
`` `

``cpp
Clase Solución {
public:
long long subtreeInversionSum(vector seleccionadovector seleccionador seleccionados)
};
`` `

-...


### 5.1 Java

``java
importar java.util*;

Solución de la clase pública {}
// dp[nodo][dist][signIndex] signIndex: 0 - título +1, 1 - título -1
largo privado[][][] dp;
int k privado;
int[] nums;
lista privada indicada[] árbol;

public long subtreeInversionSum(int[][] edges, int[] nums, int k) {
int n = nums.length;
esto.k = k;
esto.nums = nums;

// construir lista de adjacency
árbol = nuevo ArrayList[n];
para (int i = 0; i) no; i++) árbol[i] = nuevo ArrayList recomendado();
para (int[] e : bordes) {
árbol[e[0].add(e[1]);
árbol[e[1]].add(e[0]);
}

// inicializar dp con un valor centinela
dp = nuevo largo[n][k][2];
para (int i = 0; i)
para (int d = 0; d)
Arrays.fill(dp[i][d], Long.MIN_VALUE);

// arrancar desde la raíz, sin inversión de ancestro, dist = 0, signo = +1
dfs(0, -1, 0, 0);
}

// dfs returns dp[node][dist][signIndex]
dfs privados largos(int u, int parent, int dist, int signIdx) {}
si (dp[u][dist] [signIdx] != Long.MIN_VALUE) {
dp[u][dist][signIdx];
}

larga señal = (signIdx == 0) ? 1L : -1L;
Nodo largo Val = signo * nums[u];

largo sin = nodeVal; // suma si no invertimos u (o no podemos)
long with = Long.MIN_VALUE; // only used when dist=0

// iterate over children
para (int v : árbol[u]) {}
si (v == padre) continúan;
si 0) {
sin += dfs(v, u, dist - 1, signIdx);
. ♫ ... {
// niño cuando NO invertimos u
sin += dfs(v, u, 0, signIdx);
}
}

// Si se permite la inversión (dist == 0), considere la inversión u
si 0) {
invertido Val = -sign * nums[u]; // valor después de la inversión
invertido Sum = invertido Val;
int opuesto SignIdx = 1 - signIdx; // flip sign

para (int v : árbol[u]) {}
si (v == padre) continúan;
invertedSum += dfs(v, u, k - 1, opuestoSignIdx);
}

sin = Math.max(sin, invertedSum);
}

dp[u][dist] [signIdx] = sin;
Retorno sin;
}
}
`` `

**Notas*

* `signIdx` mantiene el DP pequeño – dos posibles signos.
* El valor centinela `Long.MIN_VALUE` garantiza que siempre se recompone una célula no inicializada.
* La función devuelve un `long` – LeetCode utiliza 64 bits para la respuesta.



### 5.2 Python

``python
desde functools import lru_cache
de la importación Lista

Solución de clase:
def subtreeInversionSum(self, edges: List[List[int], nums: List[int], k: int) - título int:
n = len(nums)

# Lista de adjacency
g = [[] for _ in range(n)]
para a, b en los bordes:
g[a].append(b)
g[b].append(a)

@lru_cache(maxsize=None)
def dfs(u: int, parent: int, dist: int, sign: int) - título int:
"
señal : +1 o -1
dist : 0 .. k-1 (edges left until we may invert inside this subtree)
"
val = signo * nums[u]
si se desactivan 0: # inversion prohibited
devolver val + suma(dfs(v, u, dist - 1, sign) for v in g[u] if v != parent)

# Dist == 0 – podemos elegir invertir o no
no_invert = val
for v in g[u]:
si v == padre: continuar
no_invert += dfs(v, u, 0, sign)

inverso = -val
for v in g[u]:
si v == padre: continuar
invert += dfs(v, u, k - 1, -sign)

volver max(not_invert, invert)

dfs(0, -1, 0, 1)
`` `

**Por qué funciona " lru_cache " *

`dfs` se llama con un tuple fijo '(u, padre, dist, sign)`. - exactamente el
estados de la mesa DP.
El caché garantiza que cada estado se computa una vez, por lo que la complejidad permanece `O(n·k)`.



### 5.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
long long subtreeInversionSum(vector seleccionadovector realizador seleccionados]
vector asignadoint círculo nums
int n = nums.size();
este- título = k;
esto-nums = nums;

/ Lista de adyacencia
árbol.assign(n, {});
para (auto golpe e : bordes) {
árbol[e[0].push_back(e[1]);
árbol[e[1]].push_back(e[0]);
}

dp.assign(n, vector asignadovector realizado durante mucho tiempo!

dfs(0, -1, 0, +1);
}

privado:
vector de vectores árbol;
vectorial seleccionador seleccionador realizador dp;
int k;
vector nums;

largos dfs(int u, int parent, int dist, int sign) {
long &res = dp[u][dist][sign == -1];
si (res != LLONG_MIN) regresa res;

largo largo cur = (long long)sign * nums[u];

/ / / recoger niños primero
vector llevado a cabo largo tiempo niñoSum(k, 0); // helper no es necesario – sólo iterate

/ // si se prohíbe la inversión de
si 0) {
para (int v : árbol[u]) {}
si (v == padre) continúan;
cur += dfs(v, u, dist - 1, sign);
}
res = cur;
} más { // dist == 0 → podemos invertir o no
largo no Inversión = cura;
para (int v : árbol[u]) {}
si (v == padre) continúan;
noInvertir += dfs(v, u, 0, sign);
}

long long invert = -(long long)sign * nums[u];
para (int v : árbol[u]) {}
si (v == padre) continúan;
invert += dfs(v, u, k - 1, -sign);
}

res = max(notInvert, invert);
}

restitución;
}
};
`` `

----------------------------------------------------

## 6. Blog Post – “Subtree Inversion Sum: The Good, the Bad, the Ugly”

■ ** [SEO TAGS]** `Subtree Inversion Sum`, `LeetCode 3544`, `DP on Trees`, `Coding Interview`, `Tree Algorithms`, `Algorithm Design`, `Java`, `Python`, `C++`, `Interview Question`, `Interview Preparation `

-...

### 6.1 Hook – ¿Por qué esta pregunta se mete

En una típica entrevista de codificación el entrevistador ama *trees* porque son una estructura de datos “mundo real” – los ves en sistemas de archivos, en árboles DOM, e incluso en cartas organizativas.
El “Suma de Inversión Subtree” añade un giro: se puede cambiar el signo de toda una rama, pero sólo si se mantiene una distancia mínima de un ancestro flip.
Es una gran mezcla de la teoría **graph**, **recursion**, y ** programación dinamística** – exactamente el tipo de problema que convierte a un candidato de “medio” a “estrella” en una llamada de contratación.

-...

### 6.2 The Good – A Clean 3-D DP

* **Máquina estatal intuitiva** – el contador "dista" recuerda “hasta donde estamos prohibidos de invertir”, mientras que el estado "sign" mantiene un seguimiento de la paridad global de las inversiones por encima del nodo actual.
* **Linear time** – `O(n·k)` es sólo alrededor de 2,5 millones de operaciones para la entrada peor de los casos, que es una brisa para cualquier CPU moderna.
* **No trucos ad‐hoc** – el algoritmo no depende de la heurística o aleatorización; se deriva de una formulación DP rigurosa.

Debido a que la elección de cada nodo sólo depende del estado de su padre, el DP es *exactamente* un árbol‐ DP. Es por eso que la solución es directa una vez que reconoces el hecho de "mirar-ahead sólo hasta 'k-1' bordes".

-...

### 6.3 The Bad – A Flawed Brute‐Force

Un enfoque ingenuo podría intentar:

1. Enumere cada subconjunto de nodos (2n posibilidades) y aplique inversiones.
2. Para cada subconjunto, compruebe la regla de distancia caminando cada par de ancestro.

Ambos pasos explotan exponencialmente. Incluso con la poda, la explosión combinatoria de “invertir cualquier subárbol” es intratable para `n = 5·104`.
La gente a veces piensa que debido a los “señales de la inversión”, uno puede simplemente *verdemente* voltear los nodos de valor negativo – pero esa regla codictiva falla porque cambiar a un padre niega un subárbol *entire** y puede destruir muchos pequeños valores positivos.

-...

### 6.4 El Ugly – Señales de Manejo & Distancias

La implementación correcta del DP no es “trivial”, pero es *manageable*:

* **Sign bookkeeping** – necesitas recordar si un antepasado fue invertido. Una manera limpia es codificar el signo como `0 → +1` y `1 → –1`.
* **Distance counter** – mantener un contador que decrementos mientras vas más profundo. Reiniciarlo a `k-1` después de una inversión.
* **Cache / Memoisation** – porque cada nodo puede ser visitado para muchos `(dist, sign)` pares, una mesa de memoización o un `@lru_cache` en Python es esencial; de lo contrario, usted recomputaría millones de subsubproblemas.

Las fórmulas centrales del algoritmo ocultan un montón de detalles algebraicos:
`sign * nums[u]` vs. `-sign * nums[u]` y las dos llamadas infantiles diferentes.
Obtener los índices y el orden de repetición equivocado es una fuente común de errores.

-...

### 6.5 Takeaway – Master the State

Cuando te sientas en una entrevista y veas “Subtree Inversion Sum”, tu primer instinto debe ser hacer preguntas aclaratorias:

* ¿Está garantizado que sea pequeño? Puede ser hasta `n`, pero sólo nos importa 'k-1`.
¿Qué hace una inversión a los descendientes de un nodo? Da la vuelta a la señal de cada descendiente exactamente una vez.

Desde allí se puede definir los estados DP, probar que el valor óptimo de cada nodo depende sólo del estado de su padre, y luego escribir la función recursiva.
Al entrevistador le encantará el hecho de que usted ha convertido una norma aparentemente confusa establecida en un DP ** matemáticamente sonido**.

-...

### 6.6 Pensamiento Final – Escribe, Prueba, Repita

* Escribe primero el ayudante recursivo (sin memo todavía).
* Agregue la mesa de memoización o `@lru_cache`.
* Prueba en casos artesanales pequeños (`n=4, k=2`) para asegurar el trabajo de las flips de señal.
* Escalar y verificar contra la solución oficial LeetCode.

Una vez que hayas hecho esto, no solo resolverás el problema, sino que también demostrarás una comprensión ** profunda de la programación dinámica en los árboles** – una habilidad que es valiosa en muchos dominios: desde los servicios de backend a los árboles de decisión AI.

-...

■ ¿Quieres impresionar a los reclutadores? * *
■ Añadir “Subtree Inversion Sum” a su cartera y practicar el enfoque DP limpio en Java, Python, o C++.
■ Recuerde: buenos algoritmos *look clean* – y algoritmos limpios *look great* en su currículum.

-...

**End of Blog Post**

-...

## 7. Clausura

El problema “Subtree Inversion Sum” es un ejemplo de una pregunta de entrevista bien diseñada.
Una solución DP limpia es tanto **eficiente** como **conceptualmente elegante**.
Ya sea que lo codificas en Java, Python o C++, la misma máquina estatal sustenta la lógica – la diferencia está en los detalles de implementación y los trucos de memoización específicos del lenguaje.

¡Feliz codificación!