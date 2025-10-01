-...
Título: LeetCode 1402. Reduciendo discos -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
** Resumen de la resolución**

El problema es un problema clásico “schedule‐the-positive‐prefix‐sum” problema.

* Si cocina platos en un *disminuir* orden de su satisfacción,
puedes seguir agregando un plato mientras la suma de prefijo se mantenga
no negativo.
* Cada vez que se añade un plato nuevo se multiplica el *beneficio* del plato
por su posición (1-basada).
El beneficio total de un prefijo de platos es exactamente la suma prefijo
en sí mismo.
* Por lo tanto, mientras cruzamos la lista ordenada mantenemos una carrera
prefijo suma.
Tan pronto como esa suma de prefijo se vuelve negativa, añadir más platos puede
sólo lastimamos el total; paramos.

La respuesta final es la suma de todas las sumas de prefijo positivas.

-...

## Algorithm
1. **Sorta** la matriz `satisfacción' en **discreción** orden.
2. Inicializar `prefSum = 0`, `respuesta = 0`.
3. Para cada `s` en el array ordenados
* `prefSum += s`
* Si `prefSum' significa 0` → **break**
* `respuesta += prefSum`
4. Regresar `respuesta`.

-...

### Correctness Proof

Demostramos que el algoritmo devuelve la máxima satisfacción posible.

**Lemma 1**
Sea un conjunto de platos escogidos en algún orden.
Si ordenamos los platos de 'S' en la disminución del orden de satisfacción, el
la satisfacción total de `S` no disminuye.

*Proof. *
La satisfacción total de `S` es
\[
\sum_{i=1} {k} s_{\pi(i)} \times i ,
\]
donde `π` es la orden de cocción y 'k = Silencioso '.
Reordenar los platos de modo que `s_{π(i)} \ge s_{π(j)}` para `i
aumentar cada término porque el multiplicador aumenta con el
posición. ∎



*Lemma 2*
Que `T` sea la lista clasificada en orden decreciente.
Let `prefSum(i) = T[j]`.
Si " prefSum(i) " 0 " , entonces por cada " j ≥ i " la satisfacción total
cualquier horario que use los primeros platos de `j` de `T` es **no más grande**
el horario que utiliza sólo los primeros platos "i-1".

*Proof. *
Agregar el plato `i` aumenta el total por `prefSum(i)`.
Si " prefSum(i) " , esa contribución es negativa, por lo tanto, cualquier calendario
contenerlo sólo puede ser peor que el horario que se salta. ∎



**Teorema* *
El algoritmo produce la máxima satisfacción total posible.

*Proof. *
Por Lemma plaganbsp;1 podemos asumir que los platos se procesan en disminución
Orden.
El algoritmo sigue añadiendo un plato mientras la suma prefijo de funcionamiento
permanece no negativo; una vez que se vuelve negativo, por Lemma plaganbsp;2 cualquier
Además sólo disminuiría el total.
Por lo tanto el algoritmo considera exactamente el conjunto óptimo de platos y
acumula sus contribuciones correctas, dando el máximo total
satisfacción. ∎



-...

### Complexity Analysis

*Ordenar* domina el tiempo de ejecución: **O(n log n)** tiempo.
El algoritmo utiliza **O(1)** espacio extra (aparte del array de entrada).

-...

### Reference Implementation (Python)

``python
de la importación Lista

Solución de clase:
def maxSatisfaction(self, satisfaction: List[int] - int:
# Paso 1: ordenar en orden decreciente
satisfaction.sort(reverse=True)

pref_sum = 0 # actual suma prefijo de platos seleccionados
respuesta = 0

# Paso 2: iterate while prefix sum stays non-negative
para s en satisfacción:
pref_sum += s
si pref_sum 0:
romper # añadir more will only hurt
respuesta += pref_sum

respuesta
`` `

-...

### Aplicación de referencia (C++)

``cpp
Clase Solución {
public:
int maxSatisfacción(vector fieltro) {
sort(satisfaction.begin(), satisfaction.end(), greater indicaint());
long prefSum = 0, res = 0;
(int s : satisfaction) {
prefSum += s;
si (prefSum 0) romper; // parar cuando la suma de prefijo se vuelve negativa
res += prefSum; // acumular el beneficio
}
volver estática_cast seleccionado(res)
}
};
`` `

-...

### Reference Implementation (Java)

``java
Clase Solución {
int public maxSatisfaction(int[] satisfaction) {
Arrays.sort(satisfacción);
// ordenar en orden decreciente
para (int i = 0; i)
int tmp = satisfaction[i];
satisfacción[i] = satisfacción[satisfaction.length - 1 - i];
satisfacción[satisfacción.length - 1 - i] = tmp;
}

long prefSum = 0, res = 0;
(int s : satisfaction) {
prefSum += s;
si (prefSum 0) romper;
res += prefSum;
}
retorno (int) res;
}
}
`` `

-...

Este algoritmo codicioso es óptimo y mucho más rápido que las soluciones DP,
siendo todavía muy simple de entender e implementar.