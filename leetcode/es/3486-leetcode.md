-...
Título: LeetCode 3486. Sendero Especial más largo II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Explicación de la solución**

Por cada caso de prueba que se nos da

* `n` - número de nudos de un árbol
* `n` enteros - el valor almacenado en cada nodo (no son necesarios para el
tarea, pero son parte del formato de entrada)
* " n-1 " líneas: cada línea contiene dos índices de nodos " , v " y
entero positivo `w` - el peso del borde entre `u` y `v`.

El árbol está conectado y no tiene ciclos.
La tarea es producir la longitud ** del camino más largo en el árbol** medido
por la suma de los pesos del borde.
(Si el árbol es ponderado la definición natural de su diámetro es esta suma.)

----------------------------------------------------

#### Observaciones

* Un árbol tiene exactamente un camino sencillo entre dos vértices.
* El camino más largo se llama el **diámetro** del árbol.
* En un árbol ponderado la longitud de un camino es la suma de los pesos de todos
bordes pertenecientes al camino.
* Para cualquier árbol podemos encontrar un punto final de un diámetro realizando un
profunda búsqueda (DFS) (o primera búsqueda, BFS) de un arbitrario
vertex y mantener el vértice que está más lejos.
* A partir de ese punto final y correr un segundo DFS de nuevo da el otro
punto final del diámetro y la longitud del diámetro.

----------------------------------------------------

#### Algorithm
`` `
lee n
leer los valores de n nodo e ignorarlos

construir la lista de adyacency g[0 ... n-1]
para cada uno de los bordes n-1:
u, v, w
añadir (v,w) a g[u] y (u,w) a g [v]

función más lejos(start):
// Devoluciones (versión, distancia) que es más lejos de empezar
dist[0 ... n-1] = -1
S
empuje comenzar a S
dist[start] = 0
Mientras que S no está vacío:
U = pop S
para cada (v,w) en g [u]:
si se dist[v] == -1:
dist[v] = dist[u] + w
empujar v hacia S
// encontrar el vértice con la máxima distancia
mejor = principio, mejor Dist = 0
para i = 0 ... n-1:
si dist[i] Dist:
bestDist = dist[i]
mejor = i
(mejor, mejorDist)

(firstEndpoint, _) = farthest(0)
(_, diámetro) = más lejano (primer punto)

diámetro de salida
`` `

----------------------------------------------------

#### Correctness Proof

Demostramos que el algoritmo produce la longitud del diámetro del
dado árbol ponderado.

-...

##### Lemma 1
`lo más lejano(start)` devuelve un vértice que está más lejos de `start ' y
distancia a ese vértice.

Proof.

La función realiza un DFS desde `start`.
`dist[v]` se establece exactamente una vez, a la distancia del único camino simple
desde `start` a `v`.
Debido a que el árbol no contiene ciclos, esta es la única distancia posible.
Después del DFS todos los vértices son accesibles, por lo tanto todas las distancias son conocidas.

La función escanea todos los vértices y mantiene el uno con el máximo
"dist".
Por lo tanto el vértice devuelto es exactamente el más lejano de `start`,
y la distancia devuelta es la distancia correspondiente. ∎



##### Lemma 2
Seamos un vértice arbitrario y el vértice devuelto por
`farthest(x)`.
Entonces `y` es un punto final de un diámetro del árbol.

Proof.

Suponga lo contrario: que 'y' no es un punto final de un diámetro.
Seamos los dos puntos finales de un diámetro con longitud `D`
(`dist(u,v)=D`).

De Lemma plaganbsp;1 `dist(x,y)` es la distancia máxima de `x`.
Porque no es un punto final de un diámetro,
`dist(x,u)` and `dist(x,v)` must both be **strictly smaller** than
`dist(x,y)`; de lo contrario el camino de 'x' al punto final más lejano
tendría longitud 'dist(x,y)' y sería al menos tanto como el
Diámetro, una contradicción.

Pero el diámetro de un árbol es un camino sencillo más largo.
Si ni `u' ni `v` está más lejos de `x`, el camino más largo que
no es un diámetro, contradiciendo el hecho de que
camino más largo en un árbol que comienza desde un vértice arbitrario debe ser un
punto final del diámetro.
Por lo tanto, la suposición es falsa y `y` es en realidad un punto final de un
Diámetro. ∎



##### Lemma 3
La segunda llamada de `más lejos' comenzó desde un punto final de un diámetro
devuelve el otro punto final y la longitud del diámetro.

Proof.

Seamos un punto final de un diámetro, y el otro punto final.
Por Lemma adultnbsp;2, la primera llamada `farthest(0)` devuelve algún punto final de un
diámetro; llámalo `e`.
Considere ahora la segunda llamada " más lejos " .
Todas las distancias de `e` se calculan correctamente de nuevo
(Lemma limitadanbsp;1).
El vértice más lejano de `e` debe ser el otro punto final de *algunos*
Diámetro.
Porque un árbol tiene un único camino sencillo entre cualquier dos vértices,
el camino más largo que comienza de 'e' es exactamente el diámetro, y su
Otro punto final es " b " .
Así la distancia devuelta por la segunda llamada equivale al diámetro
longitud.



################################################################################################################################################################################################################################################################ Theorem
El algoritmo produce la longitud del diámetro de la entrada ponderada
árbol.

Proof.

La primera llamada " más lejos " produce un vértice `a` que es un punto final de un
diámetro (Lemma limitadanbsp;2).
La segunda llamada " más lejos " cede el punto final opuesto " b " y
distancia entre ellos – por Lemma plaganbsp;3 esta distancia es exactamente la
longitud del diámetro.
El algoritmo produce esta distancia, por lo tanto produce el diámetro
longitud.



----------------------------------------------------

#### Complexity Analysis

Seamos el número de vértices.

* Building the adjacency list: `O(n)`
* Cada DFS visita cada vértice y borde una vez: `O(n)`
* Two DFS runs: `O(n)`
Complejidad del tiempo total: **`O(n)`**

La lista de adyacency almacena '2·(n-1) ' entradas de borde, cada entrada mantiene un
vértice id y peso (`largo largo').
El consumo de memoria es `O(n)`.



----------------------------------------------------

#### Aplicación de referencia (GNU‐C+17)

``cpp
#include יbits/stdc++.h
usando std namespace;

int main() {}
ios::sync_with_stdio(false);
cin.tie(nullptr);

int n;
si (!(cin нелиную n)) retorno 0; // no entrada

/* read node values – que son parte del formato de entrada pero no utilizado */
vector realizado largo tiempo nodeValue(n);
para (int i = 0; i) nodeValue[i];

/* construir lista de adjacency con pesos */
vector realizador designadopair realizado,largo largo título g(n);
para (int i = 0; i) {}
int u, v; long w;
cin " título " u " confianza c "
g[u].push_back({v, w});
g[v].push_back({u, w});
}

/* -------------
auto farthest = [ cl](int start) - usuario pair madeint,long long {}
vector de larga duración -1);
apilación especificado st;
st.push(start);
dist[start] = 0;

(!st.empty())) {}
int u = st.top(); st.pop();
para (auto [v,w] : g[u]) {}
(dist[v] == -1) {
dist[v] = dist[u] + w;
st.push(v);
}
}
}

int best = start; long long best Dist = 0;
para (int i = 0; i) {}
si (dist[i]
bestDist = dist[i];
mejor = i;
}
}
volver {best, best Dist};
};
/* -------------

auto [firstEndpoint, _] = farthest(0);
auto [_, diámetro] = más lejano (primer punto);

cout se realizó el diámetro hecho 'n'
retorno 0;
}
`` `

El programa sigue exactamente el algoritmo probado correcto arriba
y se ajusta al compilador GNU+17.