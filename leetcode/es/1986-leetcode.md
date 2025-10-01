-...
Título: LeetCode 1986. Número mínimo de sesiones de trabajo para terminar las tareas -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
# Número mínimo de sesiones de trabajo para terminar las tareas

-...

Problema

Se les da un conjunto de tareas.
`taks[i]` - el número de horas requeridas para terminar la tarea *i*
Tiempo de sesión: la duración máxima de una sesión de trabajo.

Durante una sesión se puede trabajar en varias tareas una tras otra, pero **una vez que se inicia una tarea debe terminarse en la misma sesión**.
Puede comenzar una nueva tarea inmediatamente después de terminar la anterior y puede elegir cualquier orden de las tareas.

■ ** Objetivo** – encontrar el número mínimo* de sesiones que son suficientes para terminar todas las tareas.

`` `
Entrada: tareas = [1, 2, 3, 3], sessionTime = 3
Producto : 2 // un posible calendario: (3) (1+2,3)
`` `

-...

## Observations

* La respuesta es siempre entre " 1 " y " n " (en la mayoría de las tareas por sesión).
* Si sabemos que las sesiones " k " son suficientes, podemos tratar de colocar todas las tareas exactamente en " cubos de capacidad " Tiempo de sesión " .
Este es un clásico **bin-packing** problema de decisión que se puede resolver por la búsqueda de profundidad primero con poda.

-...

## Algorithm

Buscamos binariamente el menor número posible de sesiones.

`` `
ordenar tareas en orden descendente
baja = 1
alto = n
ans = n

bajo ≤ alto
media = (bajo + alto) / 2
if canPlaceAll(mid) // backtracking decision problem
ans = mitad
alta = media - 1 // tratar de encontrar un k más pequeño
más
baja = media + 1
Retorno
`` `

### `canPlaceAll(k) `

* `k` - número de sesiones que se nos permite utilizar
* `load[0...k-1]` – horas de uso actual en cada sesión

`` `
DFS(idx) // idx – índice de la próxima tarea a colocar
si idx == n // todas las tareas colocadas
retorno verdadero

tarea = tareas[idx]

para mí = 0 ... k-1
si la carga[i] + tarea Hora
continuar // la tarea no cabe en este período de sesiones

// ruptura de la simetría:
// si acabamos de empezar una nueva sesión (vacío), probar el siguiente vacío sería un duplicado
si la carga [i] == 0
vacíaStart = verdadero
más
vacíaStart = falso

carga[i] += tarea
si DFS(idx+1) // colocación exitosa de todas las tareas restantes
retorno verdadero
load[i] -= tarea

si vacStart // ya hemos intentado poner esta tarea en una sesión vacía
romper // saltar todas las demás sesiones vacías
final for

devolver falso
`` `

The recursion explores all ways of distributing the tasks among `k` sessions, but:

* **Sorting descending** asegura que las grandes tareas se coloquen primero, lo que poda muchas ramas inútiles.
* **Simetría rompiendo** (`si la carga[i]=0 break`) elimina las permutaciones de los contenedores vacíos idénticos.
* El número total de llamadas recursivas está obligado por `k^n`, pero en la práctica es mucho menos que el peor caso exponencial.

-...

## Correctness Proof

Demostramos que el algoritmo devuelve el número mínimo de sesiones.

### Lemma 1
Si `canPlaceAll(k)` devuelve `true`, entonces es posible terminar todas las tareas en la mayoría de `k` sesiones.

*Proof. *
`canPlaceAll(k)` realiza una búsqueda profunda sobre todas las tareas de `n` tareas a `k` bins, cada bin que tiene capacidad `sesión Hora.
Devuelve `verdad ' sólo cuando se ha asignado cada tarea y ningún bin excede la capacidad.
Así, la asignación encontrada utiliza exactamente sesiones de " k " (o menos, porque algunos contenedores pueden permanecer vacíos), por lo que las tareas pueden ser terminadas en las sesiones más " k " . ∎



### Lemma 2
Si es posible terminar todas las tareas en las sesiones más `k ' , `canPlaceAll(k)` devuelve `true`.

*Proof. *
Consuma un horario óptimo con sesiones 'k' ≤ k`.
Ordenar las sesiones por su tiempo usado (descendiente).
La recursión en `canPlaceAll` trata de colocar tareas en este orden: coloca la primera (más grande) tarea en el primer bin, el segundo en el primero o segundo bin, etc.
Debido a que la recursión explora *todas* asignaciones (quebrada la simetría de los maulos), eventualmente explorará la asignación que corresponde al horario óptimo y así devolverá `verdadero'. ∎



### Lemma 3
Búsqueda binaria en `k` utilizando `canPlaceAll(k)` devuelve el `k' más pequeño posible.

*Proof. *
Que `f(k)` sea el predicado "las canastas pueden ser terminadas en la mayoría de 'k' sesiones".
Por Lemma adultnbsp;1, `f(k)` es *true* cuando `canPlaceAll(k)` es `true`.
Por Lemma adultnbsp;2, `f(k)` es *false* cuando `canPlaceAll(k)` es falso.
The predicate `f(k)` is monotone non-decreasing in `k` (adding an extra session cannot hurt).
Por lo tanto, la búsqueda binaria estándar en un predicado monotone encuentra el mínimo `k` tal que `f(k)` es cierto. ∎



### Theorem
El algoritmo produce el número mínimo de sesiones de trabajo necesarias para terminar todas las tareas.

*Proof. *
La búsqueda binaria invoca `canPlaceAll(k)` para valores de `k`.
Por Lemma adultnbsp;3 la búsqueda binaria se detiene con el más pequeño `k` para el cual `canPlaceAll(k)` es 'true`.
Por Lemma adultnbsp;1 este `k` es suficiente, y por Lemma pactonbsp;3 ningún número menor de sesiones es suficiente.
Así, el valor devuelto es exactamente el número mínimo de sesiones. ∎



-...

## Complexity Analysis

Seamos el número de tareas.

*Sorting* – `O(n log n) `
*Binary search* – `O(log n)` iterations
*DFS en cada iteración* – el peor caso `O(k^n)` donde 'k' es la adivinación actual, pero 'k ≤ n`.
En la práctica la poda hace que el algoritmo funcione en unos pocos milisegundos por `n ≤ 20`.

La complejidad del tiempo peor: **`O(n log n · n^n)`** (exponencial),
pero para las limitaciones del problema (`n ≤ 20`) es lo suficientemente rápido.

Complejidad espacial: **`O(k)`** para el conjunto de cargas actuales más pila de recursión – en la mayoría `O(n)`.

-...

## C++17 Implementation

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minSessions(vector fielint limitada tareas, int sessionTime) {
// Ordenar tareas en orden descendente para colocar grandes tareas primero
sort(tasks.begin(), tasks.end(), mayor especificado());

int bajo = 1, alto = tasks.size(), ans = alto;

mientras (bajo) = alto) {
int mid = (low + high) / 2; // tratar de terminar en sesiones medias
vector significado carga (medio, 0); // carga actual de cada sesión

si (dfs(0, tareas, sessionTime, load) { // podemos empacar en 'mid' bins?
ans = medio;
alta = media - 1; // probar un número menor
. ♫ ... {
baja = media + 1; // necesita más sesiones
}
}
devolver los ans;
}

privado:
bool dfs(int idx, vector asignadoint
vectorial implicado cargado
si (idx == (int)tasks.size()) regresan verdadero; // todas las tareas colocadas

int curTask = tasks[idx];
// Para romper la simetría recordamos si ya hemos intentado esta tarea
// en un contenedor vacío (load[i] == 0).
bool triedEmpty = false;

para (int i = 0; i) ++i) {
si (load[i] + curTask √≥) continúan;

bool empty = (load[i] == 0);
carga[i] += curTask;
si (dfs(idx + 1, tareas, límite, carga)) retornan verdadero;
load[i] -= curTask;

si (vacío) { // ya ha intentado poner esta tarea en una sesión vacía
romper; // saltar todos los demás contenedores vacíos
}
}
devolver falso;
}
};
`` `

■ **Compile**:
" g++ " -std=c+17 -O2 -pipe -static -s -o main main.cpp`

-...

## Java 17 Implementation

``java
importar java.util*;

Clase Solución {
public int minSessions(int[] tasks, int sessionTime) {
// Ordenar en orden descendente
Arrays.sort(taks);
para (int i = 0; i)
swap(taks, i, tasks.length - 1 - i);

int bajo = 1, alto = tareas.length, ans = alto;
mientras (bajo) = alto) {
int mid = (low + high) 1;
int[] load = new int[mid];
si (dfs(0, tareas, sessionTime, load)) {}
ans = medio;
alta = media - 1;
. ♫ ... {
baja = media + 1;
}
}
devolver los ans;
}

dfs booleanos privados(int idx, int[] tareas, límite de entrada, int[] load) {
si (idx == tareas.length) regresan verdaderos;
int cur = tasks[idx];
boolean triedEmpty = false;
para (int i = 0; i)
si (load[i] + cur √≥) continúan;
(load[i] == 0) Trató a Empty = verdadero;
load[i] += cur;
si (dfs(idx + 1, tareas, límite, carga)) retornan verdadero;
load[i] -= cur;
si (tried Empty) romper; / / / / simetría romper
}
devolver falso;
}

intercambio privado de vacío(int[] a, int i, int j) {
int t = a[i]; a[i] = a[j]; a[j] = t;
}
}
`` `

Ambos francotiradores están listos para pegar en LeetCode / un IDE local y correr en unos pocos milisegundos por las limitaciones dadas.

-...

## Test Cases

Silencio # Silencioso tareas Silencioso sesión
Silencio--------------------------------
Silencio 1 Silencio [1,2,3,3]
Silencio 2 Silencio [5,5] Silencio 5 Silencio 3
Silencio 3 Silencio [1,1,1,1,1]
Silencio 4 Silencio [8,4,4,2,2]

*Ejemplo 4* – un horario con 2 sesiones:
`` `
sesión 1 : 8
sesión 2 : 4+4, 2+2 (cada ≤ 8)
`` `

-...

¡Disfruta! Si tiene alguna pregunta o quiere un enfoque diferente (por ejemplo, bit-mask DP), hágamelo saber.