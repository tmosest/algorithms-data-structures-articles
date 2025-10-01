-...
Título: LeetCode 1583.
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 🚀 How to Crack Leet Code #1583 – “Count Unhappy Friends”
*Java fort Python Silencio C++ – La solución completa + un blog amigable con SEO que te ayuda a conseguir un trabajo*

-...

### #1# ## ## ##

■ *Count Unhappy Friends*
■ *Medium – Código Leet 1583*

Se te da:

TENIDO ANTERIOR ANTERIOR Descripción
Silencio...
Incluso el número de amigos (`2 ≤ n ≤ 500`) Silencio
Silencioso `preferencias[i]` Silencio Una permutación de todos los amigos **excepto** `i` - ordenados de la mayoría a menos preferido Silencio
TENIDO `pairs[i] = [x, y]` ANTERIOR El único emparejamiento legal (`x` ↔ `y') Silencio

Un amigo `x` es ** inhappy** si existe un amigo 'u' tal que:

1. `x ' prefers `u ' over its own partner `y`; *y*
2. `u ' prefers `x` over its own partner `v`.

Devuelve el número de amigos infelices.

■ *Examples*
■ *Ejemplo 1* – 2 amigos infelices
■ *Ejemplo 2* – 0 amigos infelices
■ *Ejemplo 3* – los 4 son infelices

-...

#### 2down⃣ Key Insight

La condición es *no* “alguien tiene un mejor partido”.
Es una **referencia mutua**: ambas personas preferirían estar juntas.
Así que para cada persona debemos:

1. Camina por su lista de preferencias *hasta* golpeamos a su pareja.
2. Para cada candidato mejor que participante `u`, compruebe si `u` también nos prefiere sobre el socio de 'u'.

Si existe tal `u', la persona es infeliz.

Para hacer el paso 2 rápido pre-computamos una matriz **rank**:

`` `
rank[i][j] = posición de amigo j en preferencias[i] (0 = opción superior)
`` `

Entonces “ ' prefieres x over v '” es simplemente `rank[u] [x] [u] [v].

-...

### 3down⃣ Algorithm (O(n2) time, O(n2) space)

Silencio Lo que hacemos
Silencio...
Silencio 1 Silencio Construir `rank[n]` escaneando cada `preferencias[i]`. Silencio
Silencio 2 Silencio Construir `partner[n]` de `pairs`. Silencio
TENIDO 3 TENIDO Por cada amigo `x`: *partner = partner[x]* **br título Para cada `u` en `preferencias[x]` *if* `rank[u][x] [u] [partner[u]] → `` infeliz, `break`.
Silencio 4 TEN Vuelva el contador. Silencio

-...

#### 4down⃣ Código

##### Java

``java
importar java.util*;

Clase Solución {
int int infelizAmigos(int n, int[][ preferencias, int[] pares) {
// 1. matriz de rango
int[][] rank = new int[n][n];
para (int i = 0; i)
para (int pos = 0; pos " )
[i] [preferencias[i] [pos]]] = pos;
}
}

// 2. matriz de socios
int[] partner = nuevo int[n];
para (int[] p : pares) {
partner[p[0]] = p[1];
partner[p[1]] = p[0];
}

int infeliz = 0;
// 3. escanear a todos
para (int x = 0; x < n; x++) {
int y = partner[x];
para (int u : preferencias[x]) {}
si (u == y) romper; // alcanzado propio compañero → feliz
int v = partner[u]; // u socio
si (rank[u][x] [u] [v]) { // preferencia mutua
infeliz++;
ruptura;
}
}
}
el regreso infeliz;
}
}
`` `

#### Python

``python
Solución de clase:
infeliz Friends(self, n: int, preferences: List[List[int],
pares: List[List[int]) - título int:
# rank[i][j] = position of j in preferences[i]
rango = [[0] * n para _ en rango(n)]
para i, pref en enumerar(preferencias):
for pos, friend in enumerate(pref):
[i] [amigo] = pos

*
para un, b en pares:
partner[a] = b
partner[b] = a

infeliz = 0
para x en rango(n):
y = partner[x]
para u en preferencias[x]:
si u == y: romper
v = partner[u]
si el rango[u][x] [u] [v]:
infeliz += 1
descanso
Retorno infeliz
`` `

###### C++

``cpp
#include יbits/stdc++.h
usando std namespace;

Clase Solución {
public:
int infelizAmigos(int n, vector asignadovector identificadoint modales,
vector asignador implicados iguales {
// rank[i][j]
vector seleccionado(n));
para (int i = 0; i) {}
para (int pos = 0; pos " )
[i] [preferencias[i] [pos]]] = pos;
}
}

vector asignadoint socio(n);
para (auto &p : pares) {
partner[p[0]] = p[1];
partner[p[1]] = p[0];
}

int infeliz = 0;
para (int x = 0; x < n; ++x) {
int y = partner[x];
para (int u : preferencias[x]) {}
(u == y) romper;
int v = partner[u];
si (rank[u][x] [u] [v] {}
++sinhappy;
ruptura;
}
}
}
el regreso infeliz;
}
};
`` `

-...

#### 5down⃣ Análisis de la complejidad

TENIDO TERRENO Java / Python / C++
Silencio...
← Tiempo Silencioso **O(n2)** – visitamos la lista de preferencias de cada amigo una vez. Silencio
TENIDO Espacio TENIDO **O(n2)** – la matriz de `rank ';; `parner ' y los arrays auxiliares son O(n). Silencio

Con 'n ≤ 500', esto pasa fácilmente los límites del Código Leet.

-...

### 6down⃣ Common Pitfalls (“El malo”)

Silencio Pitfall Silencio Por qué no funciona
Silencio--------------------------
Silencio Usando un * mapa de hash* para el rango en lugar de un array de 2-D habit Demasiado lento (`O(n2)` las apariencias se convierten en `O(1)` pero con una alta constante) Usar una matriz de int simple – rápido cache friendly
Silencio Rompiendo sólo después de encontrar *cualquier* mejor amigo También debemos asegurarnos de que *ese amigo* nos prefiera en la vida Revise la segunda condición (`rank[u][x] [u] [partner[u]]] Silencio
Silencio Skipping the partner in the internal loop by `if(u===y) continue` Silencio Contaría incorrectamente a algunas personas infelices Silencio `romper` cuando se llega a un socio - estamos garantizados para ser felices más allá de ese punto tención
Silencio Contando tanto `x' como `y` como infeliz para el mismo par TEN El algoritmo cuenta cada persona de forma independiente, pero la condición es simétrica; sin doble recuento de problema TEN Ningún cambio necesario – cada persona es evaluada una vez ANTE

-...

### 7 carreras ¿Por qué este blog te ayuda a conseguir un trabajo

1. **SEO‐Optimized Palabras clave** – “Count Unhappy Friends”, “Leet Code 1583”, “Java interview question”, “Python algoritmo”, “C++” Solución”, “O(n2) time”, “space complexity”, “mutual preference algoritmo”, “unhappy friends logic”.
2. **Código de cable** – Soluciones listas para copiar para Java, Python, C++ – esperan los tres entrevistadores de idiomas más comunes.
3. **Deep Dive** – Understanding *why* the algoritmo works gives you the confidence to explain it in an interview.
4. **Pitfalls** – Errores comunes que puedes mencionar como “cosas que aprendí” para demostrar que has pensado en casos de borde.
5. **Time & Space Analysis** – Muestra tu capacidad de evaluar la complejidad – una habilidad de entrevista obligada.

-...

#### 8down⃣ Quick Takeaway

- Construir una matriz **rank** para las consultas de preferencia O(1).
- Mapa del socio de cada amigo en un array.
- Para cada amigo, iterate preferencias hasta que golpees al socio; si cualquier candidato mejor que el compañero también prefiere, eres infeliz.
- Complejidad: **O(n2)** tiempo, **O(n2)** espacio – perfectamente bien para `n ≤ 500`.

¡Suelta el código en tu editor, ejecuta las pruebas del Código Leet y estarás listo para crear este problema e impresiona a los gerentes de contratación! 🚀

-...

Feliz codificación, y la mejor suerte de aterrizar ese trabajo de ensueño!