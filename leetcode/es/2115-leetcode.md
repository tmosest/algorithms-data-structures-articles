-...
Título: LeetCode 2115. Encontrar todas las recetas posibles de los suministros dados -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Explicación de la solución**

El problema es un problema clásico *dependencia gráfica*.
Cada ingrediente o receta puede considerarse un nodo.
Si una receta necesita un ingrediente dibujamos una flecha **del ingrediente a la receta**.

`` `
zanahoria - sopa
sal - título sopa
soup - titulado guiso
`` `

Los únicos nodos libres son los suministros dados – podemos pensar en ellos como ya preparados
ingredientes.
Una receta se puede cocinar tan pronto como **all** de sus bordes entrantes (ingredientes) están disponibles.
Después de una receta se cocina se puede utilizar como un suministro para otras recetas.

Esto es exactamente lo que una especie *topológica* (El algoritmo de Karen) hace:
empezar con todos los nodos libres (supplies), eliminar repetidamente un nodo, y
disminuir el grado de sus vecinos salientes.
Cada vez que el indegrejo de un vecino se convierte en cero sabemos que todos sus ingredientes
ya están disponibles – la receta se puede cocinar.

El algoritmo funciona naturalmente en *cualquier* orden en el que se cumplen los requisitos, que
es todo el problema que pide.



----------------------------------------------------

#### Algorithm
`` `
1. Construir dos mapas:
indegree[recipe] = número de ingredientes necesarios
gráfico[ingrediente] = lista de recetas que requieren este ingrediente

2. Pon todo el suministro en una cola.
También mantenga un conjunto 'disponible' que inicialmente contiene todos los suministros.

3. Mientras que la cola no está vacía
cur = cola.pop()
// Si cur es una receta que acabamos de hacer, ya está en 'disponible'.
Por cada receta siguiente que depende de cura
indegree[next]--
indegree[next] == 0
// todos sus ingredientes están disponibles
result.push_back(next)
queue.push(next) // esta receta se convierte en un nuevo suministro
disponible.insert(next)

4. El vector 'result' ahora contiene todas las recetas que se pueden cocinar.
`` `

----------------------------------------------------

#### Correctness Proof

Demostramos que el algoritmo devuelve exactamente el conjunto de recetas que se pueden cocinar.

-...

##### Lemma 1
Cuando una receta `r` se inserta en la cola (y en consecuencia en el vector resultado),
todos sus ingredientes necesarios están disponibles en ese momento.

Proof.
`r` se inserta sólo cuando su `indegree[r]` se convierte en cero.
`indegree[r]` sólo se disminuye cuando uno de sus ingredientes necesarios (o una receta que
lo usa) se elimina de la cola.
Así pues, por cada ingrediente necesario `x` de `r` había un momento en que `x` fue quitado
de la cola y `indegree[r]` fue decrementado por uno.
Puesto que el indegrejo final es cero, cada ingrediente requerido fue eliminado de la cola
exactamente una vez, lo que significa que estaba disponible cuando fue procesado. ∎



##### Lemma 2
Si una receta `r` se puede cocinar utilizando los suministros dados, entonces el algoritmo
insértese en la cola.

Proof.
Utilizamos la inducción sobre la longitud de la derivación más corta de `r`.

*Base:*
Si `r` utiliza sólo los suministros originales, todos sus ingredientes están inicialmente en la cola.
Cuando el algoritmo procesa el primero de esos suministros, se decrementará
`indegree[r]` en consecuencia.
Después de que el último suministro requerido haya sido procesado, `indegree[r]` se convierte en cero y
" r " se inserta.

*Paso de inducción:*
Insértese cada receta que se puede cocinar en la mayoría de los pasos 'k' se inserta.
Seamos una receta que requiere una receta 'p' que es en sí misma cocinable en 'k' pasos.
Mediante la hipótesis de la inducción, `p` se insertará en la cola.
Cuando " p " se procesa, `indegree[r] ' es decrementado.
Todos los demás ingredientes necesarios de `r` son ya sea suministros originales o recetas
cocinable en la mayoría de los " pasos " , así también insertado antes de " r " se considera.
Consecuentemente, después de que el último ingrediente se procesa, `indegree[r]` se convierte en cero
y `r` se inserta. ∎



##### Lemma 3
Ninguna receta que no se puede cocinar se inserta en la cola.

Proof.
Una receta se inserta sólo cuando su indegree llega a cero (Lemma budnbsp;1).
Indegree cero significa que todos los ingredientes necesarios ya han sido eliminados de la cola,
Es decir, están disponibles.
Si una receta no era cocinable, al menos un ingrediente requerido nunca está disponible,
por lo tanto su indegree nunca puede convertirse en cero, y la receta nunca se inserta. ∎



################################################################################################################################################################################################################################################################ Theorem
El vector de salida `result` contiene exactamente todas las recetas que se pueden cocinar desde el
dados suministros.

Proof.

*Soundness* – cada receta en `result` se puede cocinar:
Por Lemma plaganbsp;1, cada receta insertada tiene todos sus ingredientes disponibles, por lo que es
cocinable.

* Completeness* – cada receta cocinable aparece en `resultado`:
Por Lemma adultnbsp;2 cada receta cocinable será insertada en la cola, y
por la construcción el algoritmo empuja cada receta insertada en `result`. ∎



----------------------------------------------------

#### Complexity Analysis

Vamos.

* `n` - número de recetas
* `m` – número total de ocurrencias de ingredientes (sumo de todas las longitudes de la lista de ingredientes)

Construir los dos mapas es `O(n + m)`.
Cada extracción de ingredientes de la cola activa un procesamiento constante de todos
bordes salientes, que en general toca cada borde una vez – `O(m)`.
Las propias operaciones de la cola también son `O(n + m)`.
Por lo tanto, el tiempo de funcionamiento total es `O(n + m)` y el consumo de memoria es
`O(n + m)`.



----------------------------------------------------

#### Aplicación de referencia (C++)

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
vector identificador confianza encontrarAllRecipes(vector seleccionadostring consigo recetas,
vector identificador seleccionador obteniendo ingredientes
vectores asignados a suministros
unordered_map seleccionadastring, vector seleccionadosstring confianza graph; // ingrediente - título recetas que lo necesitan
unordered_map logradostring, intilo indegree; // receta - número de ingredientes faltantes
unordered_set obtenidosstring confianza disponible; // todos los ingredientes que actualmente son libres
vectoriales resultado;

// 1. Construir el mapa gráfico e indegree
para (size_t i = 0; i) ++i) {
const string límite receta = recetas[i];
indegree[recipe] = ingredientes[i].size();
para (contiguo cadena ing : ingredientes[i]) {}
graph[ing].push_back(recipe);
}
}

// 2. Queue all original supplies
queue hacía referencia q;
para (contiguo cadena reducida s : suministros) {}
si (disponible.insert(s).second) { // insertar sólo una vez
q.push(s);
}
}

// 3. El algoritmo de Kahn
(!q.empty()) {
const string cur = q.front(); q.pop();

// Para cada receta que depende de 'cur', reducir su indegree
(graph.find(cur) != graph.end()) {
para (continuado cadena nxt : graph[cur]) {}
--indegree[nxt];
si (indegree[nxt] == 0) {
// todos los ingredientes de 'nxt' ya están disponibles
result.push_back(nxt);
disponible.insert(nxt);
q.push(nxt); // 'nxt' se convierte en un nuevo suministro
}
}
}
}

Resultado de retorno;
}
};
`` `

*El código sigue exactamente el algoritmo;*
Los comentarios dentro de la implementación reflejan los pasos descritos anteriormente.

----------------------------------------------------

#### Implementaciones alternativas
Si prefiere una solución basada en DFS o el enfoque BFS de fuerza bruta, también son
disponible, pero el método basado en Kahn es el más eficiente (tiempo lineal) y es
exactamente lo que el problema espera.