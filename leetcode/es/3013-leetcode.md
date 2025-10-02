-...
Título: LeetCode 3013. Divide un Array Into Subarrays con coste mínimo II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
#include יbits/stdc++.h
usando std namespace;

larga resolución (cont vectorial) largo tiempo ventaja a, largo k, largo largo d) {}
int n = (int)a.size();
si (k <=1) devolver a [0]; // sólo un subarray necesario
int need = (int)k - 1; // number of subarrays to choose
long long best = LLONG_MAX;
suma larga = 0; // suma actual de elementos seleccionados

setיpair obtenidos larga,intentas no utilizados; // elementos aún no en la ventana actual
setיpair observadolong long,int contacto estrecho; // elementos de ventana actuales (mantenido ordenados)

int r = 0; // último índice que se ha añadido a
para (int l = 1; l ' = n-1; ++l) {
// añadir índice l si aún no se ha añadido
si
mientras (r)
++r;
unused.insert ({a[r], r});
}
}

int target = (int)min(long)l + d, (long long)n - 1);
mientras que (r) objetivo) {
++r;
unused.insert ({a[r], r});
}

// mover los elementos más pequeños de los no utilizados para curar hasta que los elementos "necesitados"
mientras ((int)cur.size() {}
auto = no utilizado.begin(); // elemento más pequeño
cur.insert(*it);
sumSel += it-jófirst;
unused.erase(it);
}

// mantener los elementos más pequeños 'necesitados' en curtido
mientras (!cur.empty() " sensible !unused.empty() "
cur.rbegin()- primero не noused.begin()- primero) {
auto itCur = prev(cur.end());
sumSel -= itCur-propfirst;
unused.insert(*itCur);
cur.erase(itCur);

aut itUn = unused.begin();
cur.insert(*itUn);
sumSel += itUn- confíafirst;
unused.erase(itUn);
}

si (int)cur.size() ==necesidad)
mejor = min(mejor, sumSel);

// eliminar elemento en la posición l antes de la próxima iteración
auto itCurL = cur.find({a[l], l});
(itCurL != cur.end()) {
cur.erase (itCurL);
sumSel -= a[l];
. ♫ ... {
unused.erase({a[l], l});
}
}

devolver el mejor + a[0];
}