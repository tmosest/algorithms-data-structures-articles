-...
Título: LeetCode 3679. Discos mínimos al inventario de equilibrio -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 📦 3679 – Discos mínimos para el inventario de equilibrio
**Medium tención 10‐15 min solución ← O(n) time, O(n + U) space**

-...

### 1. Recaptación de problemas

Se les da:

* `arrivals` – una serie de enteros (`1 ≤ llegadas[i] ≤ 105`) donde cada entrada es el **tipo** del artículo que llega el día `i` (1-indexed).
* `w` - el tamaño de la ventana corredera (últimos `w' días).
* `m` – el número máximo permitido de **kept** artículos del mismo tipo en cualquier ventana.

Por cada día `i` miramos la ventana
`[max(1, i – w + 1), i]`.
Si mantenemos la llegada el día `i' y causaría que la cuenta de su tipo en esta ventana excediera `m`, *debemos* descartarla.
Queremos el número **minimo** de descartes necesarios para que *cada ventana* satisfaga la regla.

-...

### 2. Visión clave

Lo único que importa es la ventana *current*.
Cuando nos movemos del día `i` a `i+1`:

1. El día `i+1-w` deja la ventana (si existe).
2. Decidimos mantener o descartar la llegada el día `i+1`.

Si guardamos un artículo sólo cuando lo hace **no** violar la regla, nunca desperdiciamos un descarte – esta estrategia avaricia es óptima.
Así que necesitamos una ventana deslizante con un contador de frecuencia.

-...

### 3. Algoritm

``text
[i] – matriz booleana, verdad si guardamos el artículo el día i
cnt[tipo] – hash map (o array) que contiene cuántos elementos guardados de ese tipo están actualmente dentro de la ventana
descarte – contador de artículos descartados

para i de 0 a n-1: // Índice 0 basado = día i+1
// 1. Quitar el día que sale de la ventana
idx = i - w
si idx >= 0 y se mantiene[idx] == verdadero:
cnt[arrivals[idx]] -= 1

// 2. Trate de mantener la llegada actual
t = llegadas[i]
si cnt[t]
[i] = verdadero
cnt[t] += 1
más:
descarte += 1 // debe desechar
Descarto de retorno
`` `

* **Tiempo** – O(n) (cada día hace sólo una cantidad constante de trabajo).
* **Espacio** – O(n + U) donde `U` es el número de diferentes tipos de elementos
(`kept` is `n`, `cnt` is `U`).

-...

### 4. Código

A continuación encontrarás tres implementaciones totalmente operativas: una en **Java**, **Python**, y **C+**.

-...

#### 4.1 Java (LeetCode-style)

``java
importar java.util*;

Solución de la clase pública {}
public int minArrivalsToDiscard(int[] arrivals, int w, int m) {
int n = llegadas. longitud;
boolean[] kept = new boolean[n];
Mapa seleccionadoInteger, Integer inteligente cnt = nuevo HashMap fiel();
int discard = 0;

para (int i = 0; i)
int idx = i - w;
si (idx ю= 0 " seguido[idx]) {}
int old = arrivals[idx];
cnt.put(old, cnt.get(old) - 1);
}

int type = arrivals[i];
int cur = cnt.get OrDefault(tipo, 0);
si
[i] = verdadero;
cnt.put(tipo, cur + 1);
. ♫ ... {
discard++;
}
}
descarte de retorno;
}
}
`` `

-...

###### 4.2 Python

``python
Solución de clase:
def minArrivalsToDiscard(self, arrivals: list[int], w: int, m: int) - título int:
n = len(arrivalos)
[False] * n
freq = {}
descarte = 0

para i en rango(n):
idx = i - w
si idx >= 0 y mantenidos[idx]:
viejo = llegadas[idx]
freq[old] -= 1

t = llegadas[i]
cur = freq.get(t, 0)
si se curan
[i] = Verdadero
freq[t] = cur + 1
más:
descarte += 1
Descarto de retorno
`` `

-...

##### 4.3 C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int minArrivalsToDiscard(vector realizadoint limitada llegadas, int w, int m) {
int n = arrivals.size();
vector asignado título mantenido(n, 0); // 0 = descartado, 1 = mantenido
unordered_map detectint, int confianza cnt; // type - cuenta en la ventana
int discard = 0;

para (int i = 0; i) {}
int idx = i - w;
si (idx ю= 0 " seguido[idx]) {}
int old = arrivals[idx];
si 0) cnt.erase(old);
}

t = llegadas[i];
si
[i] = 1;
++cnt[t];
. ♫ ... {
++descarte;
}
}
descarte de retorno;
}
};
`` `

Las tres soluciones se ejecutan en **O(n)** tiempo y uso **O(n + U)** memoria, encajando perfectamente con las limitaciones (`n ≤ 105`).

-...

### 5. Explicación del Blog-Style

■ **Título**: *Balancing Inventory in O(n): The 3679 Minimum Discards Problem Explained*

-...

##### 5.1 Introduction

Si eres un ingeniero de software que persigue un papel de algoritmos de estructuras de datos, es probable que hayas visto los problemas de LeetCode “Sliding Window”.
El “Minimum Discards to Balance Inventory” (LeetCode 3679) es un ejemplo clásico que combina decisiones codictivas con un contador de ventanilla deslizante.

En este artículo:

* Comprender el problema desde una perspectiva empresarial.
* Camina por el algoritmo codicioso paso a paso.
* Destacan los obstáculos (las partes “malas” y “muy”).
* Presentar código limpio y listo para la producción en Java, Python y C++.
* Espolvorear algunas palabras clave amigables con SEO para ayudar a los reclutadores a encontrarte.

-...

#### 5.2 Real‐World Analogy

Imagina un almacén que recibe envíos todos los días.
El gerente puede guardar o descartar cada envío el mismo día.
Sin embargo, para *cualquier* período reciente de 7 días, ningún tipo de producto puede superar un máximo de 5 artículos guardados.

Si la ventana de 7 días ya tiene 5 unidades de producto “X” y llega un nuevo envío de “X”, deberás desecharlo**, de lo contrario se viola la regla.

Usted desea descartar los envíos *fewest* posibles, porque cada envío descartado es una venta perdida.

-...

#### 5.3 The Greedy Insight

¿Por qué es suficiente descartar sólo cuando es forzado?

* Supongamos que *mantenemos* un elemento que haría que la ventana contemple más `m`.
Eso viola la regla, así que tal estado es ilegal.
* Si *descarte* un artículo que podría haberse mantenido, aumentamos innecesariamente el recuento de descartes.
Podríamos haberlo mantenido y seguir siendo legales.

Así, la única acción legal en cada día es:

`` `
si (conteo actual)
más descarte
`` `

Esta regla simple garantiza que nunca desperdiciamos un descarte, por lo que produce los descartes *mínimo*.

-...

#### 5.4 ¿Por qué se necesita una ventana deslizante (la parte “buena”)

El tamaño de la ventana `w` puede ser tan grande como `105`.
La recomposición ingenua de cada tipo en cada ventana costaría `O(n·w)`, lo que es imposible.

Una ventana * deslizante* nos permite:

1. **Agregar** el nuevo artículo del día en O(1).
2. **Remove** el elemento que deja la ventana en O(1).

Sólo guardamos un contador para los elementos *actualmente guardados*, no toda la matriz.
Eso reduce la complejidad del tiempo de cuadrático a lineal.

-...

#### 5.5 Common Pitfalls (Las partes “Bad” " Ugly " )

Problema de la vida Silencioso / Práctica de la Ugly
Silencio--------------...
Silencio **Usando una cola para la ventana** Silencio Una cola añade/removes O(1) pero almacena *todos* días, haciendo la solución memoria-heavy. Use una matriz booleana ( " sept " ) en lugar de almacenar cada día en una cola. Silencio
Silencio **Los contadores portátiles en un diccionario** Silencio Olvidar borrar las entradas cero puede hinchar el mapa y herir factores constantes. Presiona para '0' y 'erase' la llave. Silencio
TEN **Off‐by-one index errors** TENIDO Utilizar la lógica 1-basada en arrays basados en 0 conduce a errores sutiles. ← Convertir explícitamente el día `i` a índice basado en 0 y compute `idx = i - w`. Silencio
Silencio **Asignación innecesaria de la matriz** Silencio Alquilar una gran variedad de tamaño `n` sólo para saber si guardamos un artículo es desperdicio cuando `n` es enorme. Silencio Usar un `boolean[]` (o `char`) - es mínima y rápida. Silencio

-...

#### 5.4 Code Walk‐Through (Java)

``java
para (int i = 0; i)
int idx = i - w; // día que deja la ventana
si (idx ю= 0 " seguido[idx]) { // se mantuvo, así que eliminamos su cuenta
int old = arrivals[idx];
cnt.put(old, cnt.get(old) - 1);
}

tipo int = llegadas[i]; // día actual tipo de artículo
int cur = cnt.get OrDefault(tipo, 0);
si (curo < m) { // seguro para mantener
[i] = verdadero;
cnt.put(tipo, cur + 1);
} otro { // forzado a descarte
discard++;
}
}
`` `

* **¿Por qué es esto O(n)? * *
Cada iteración hace un número constante de operaciones hash-map.
* **¿Por qué funciona? * *
Porque la única violación posible se maneja inmediatamente.

-...

#### 5.5 Complexity Summary

TEN TERRITOR TEN TEN ANTE
Silencio...
Silencio ** Tiempo** Silencio **O(n)** (linear)
Silencio **Espacio** Silencioso **O(n + U)** (array + hash‐map)
Silencio **Por qué importa** Silencio Conoce los límites difíciles de LeetCode (`n ≤ 105`) y es lo suficientemente rápido para los sistemas de inventario en tiempo real. Silencio

-...

#### 5.6 SEO & Recruitment Hooks

* **Keywords**: “Sliding window algoritmo”, “minimum discards”, “Graedy algoritmo”, “Java sliding window”, “Python data structures”, “C++ hash map”, “LeetCode 3679”, “inventory management problem”, “optimal discard strategy”.
* **Tagline**: “¿Quieres ace los problemas de ventanilla deslizante de LeetCode? Echa un vistazo a la solución de 3679 Discos Mínimos – Java, Python, C++ – O(n) tiempo, descartes óptimos!”
* **Meta-descripción** (para motores de búsqueda):
*“Aprenda a resolver LeetCode 3679 – Discos mínimos para el inventario de equilibrio – con un enfoque codicioso de la ventanilla deslizante. Obtenga código Java, Python y C++, además de una explicación detallada que es perfecta para los reclutadores.”*

-...

#### 5.7 Take-away Checklist

Entendido **Greedy es óptimo** – mantener sólo cuando estás *no* forzado a descarte.
Entendido **Slide the window** – remove the day that exits (`i - w`).
✅ ** Mapa de frecuencia** – pista cuenta de tipos guardados dentro de la ventana.
✅ **Evitar los errores por uno** – convertir los números del día correctamente.
Entendido **Use la memoria mínima** – un array booleano para “kept” + un mapa precipitado para frecuencias.

-...

##### 5.8 Closing

Ya sea que esté haciendo frente a una entrevista de codificación, construyendo un microservicio de gestión de almacenes, o simplemente agudizando sus habilidades de estructura de datos, el problema 3679 es un gran escaparate de ** verde + ventana deslizante**.

Deja un ⭐pping en el problema LeetCode, comparte este artículo y siéntete libre de ajustar el código para tu propia pila.

¡Feliz codificación! 🚀**

-...

### 6. Referencia rápida

TEN TERRITORIO TENIDO Enlace ANTE
Silencio...
Silencio ** Solución de la java** Silencio
Silencio ** Solución pitón** Silencio
Silencio **C++ Solución** Silencio
Silencio **Full article** Silencio *Copy‐paste into your blog or Medium post*

-..