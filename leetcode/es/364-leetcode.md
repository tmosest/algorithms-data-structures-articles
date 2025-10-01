-...
Título: LeetCode 364. Lista anidada Peso Sum II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
## 1. El Código

A continuación se presentan tres soluciones listas a paso que pasarán los casos oficiales de prueba LeetCode.
Cada snippet implementa la misma estrategia *un-pass BFS*:
* mientras recorremos la lista mantenemos la profundidad actual,
* acumular la suma de todos los enteros (`sumElements`) y la suma de * profundo × entero* (`sumDepthProduct`),
* rastrea la profundidad máxima (`maxDepth`).
Después del bucle podemos derivar la respuesta en O(1):

`` `
respuesta = (maxDepth + 1) * sumaElementos - sumDepthProduct
`` `

Esta fórmula sigue directamente de la definición del peso inverso.

-...

## Java (LeetCode signature)

``java
importar java.util*;

Clase Solución {
público en profundidad SumInverse(Lista realizadaNestedInteger confianza nestedList) {
Queue NoestedInteger título q = nuevo LinkedList recomendado(nestedList);

profundidad de entrada = 1;
int maxDepth = 0;
int sumElements = 0;
int sumDepthProduct = 0;

(!q.isEmpty()) {
int size = q.size();
maxDepth = Math.max(maxDepth, profundidad);

para (int i = 0; i) {}
NestedInteger cur = q.poll();

si (cur.isInteger()) {}
int val = cur.getInteger();
sumElements += val;
sumDepthProduct += val * profundidad;
. ♫ ... {
q.addAll(cur.getList());
}
}
profundidad++;
}

(maxDepth + 1) * sumaElementos - sumDepthProduct;
}
}
`` `

■ **Nota**: En el entorno LeetCode ya se suministra la interfaz `NestedInteger`.
■ Si usted prueba localmente usted puede crear un simple problema:

``java
clase NestedInteger {}
privado Valor entero;
Lista privada No incluida.

// Constructores, conserjes, y setters omitidos para brevedad
}
`` `

-...

## Python 3

``python
de las colecciones importa
de la lista de importaciones de la Unión

# LeetCode stub – no necesitas implementarlo
clase NestedInteger:
def __init__(self, value: Union[int, List] = Ninguno):
si isinstance(valor, int):
auto._int = valor
auto._list = Ninguno
más:
uno mismo.
auto._list = valor si el valor no es otro []

def isInteger(self) - título bool:
no es ninguno

def getInteger(self) - Propiedad int:
volver a sí mismo._int

def getList(self) - Propiedad List["NestedInteger"]:
volver a sí mismo.

Solución de clase:
profundidad SumInverse(self, nestedList: List[NestedInteger]) - título int:
q = deque(nestedList)

profundidad = 1
max_depth = 0
sum_elements = 0
sum_depth_product = 0

mientras q:
tamaño = len(q)
max_ profundidad = max(max_ profundidad, profundidad)

para _ en rango(tamaño):
cur = q.popleft()
si cur.isInteger():
val = cur.getInteger()
sum_elements += val
sum_depth_product += val * profundidad
más:
q.extend(cur.getList())
profundidad += 1

retorno (max_ profundidad + 1) * suma_elementos - sum_fund_product
`` `

-...

### C++ (LeetCode signature)

``cpp
Incluido el título
#include >
usando std namespace;

Clase Solución {
public:
int deepSumInverse(vector realizadoNestedInteger <nestedList) {
queue efectuadaNestedInteger confianza q;
para (auto &ni : nestedList) q.push(ni);

profundidad de entrada = 1;
int maxDepth = 0;
int sumElements = 0;
int sumDepthProduct = 0;

(!q.empty()) {
int sz = q.size();
maxDepth = max(maxDepth, deep);

para (int i = 0; i) {}
NestedInteger cur = q.front(); q.pop();

si (cur.isInteger()) {}
int val = cur.getInteger();
sumElements += val;
sumDepthProduct += val * profundidad;
. ♫ ... {
const vector efectuadoNestedInteger < = cur.getList();
q.push(x);
}
}
++a profundidad;
}

(maxDepth + 1) * sumaElementos - sumDepthProduct;
}
};
`` `

■ **C++ Stub**
■ En un entorno local es posible que necesite una implementación mínima de 'NestedInteger':

``cpp
clase NestedInteger {}
public:
NestedInteger() : is_int(false) {}
NestedInteger(int val) : is_int(true), integer(val) {}
bool isInteger() const { return is_int; }
int getInteger() const { integer de retorno; }
vector de const {NestedInteger >getList() const { lista de retorno; }
void add(const NestedInteger &ni) { list.push_back(ni); }
privado:
bool is_int;
int integer;
vector asignadoNestedInteger confianza list;
};
`` `

-...

## 2. El artículo del Blog

### Title
**LeetCode 364 – Lista Anidada Peso Sum II: Una Solución BFS de un solo par en Java, Python & C+**

## Meta Descripción
Aprende a resolver LeetCode 364 (Nested List Weight Sum II) de manera eficiente. Lea nuestra guía paso a paso con los fragmentos de código Java, Python y C++, además de una profunda inmersión en los cambios algoritmos.

-...

## Introduction

Si estás preparando una entrevista de ingeniería de software, problema de LeetCode **364 – Lista Anidada Peso Sum II** es un clásico.
Le pide que computar la suma ponderada de una lista anidada donde el peso de un entero es **en profundidad inversa**:

■ **peso = maxDepth – profundidad + 1**

El objetivo es regresar
`eva (integer * peso)` para todos los enteros en la lista.

Es engañosamente simple, pero prueba su capacidad para razonar sobre la recursión, la búsqueda de profundidad primero (DFS), la búsqueda de la primera (BFS), y la comprensión matemática.

En este post cubriremos:

* Problema de reinstalación " limitaciones
* Una solución BFS de paso único (el código ya se proporciona arriba)
* Un enfoque “malo” que puede causar el flujo de pila
* El truco “muy” basado en fórmulas que puede tropezar con principiantes
* Resúmenes fáciles de SEO para ayudar a su rango de artículo para preguntas de entrevista

Entremos.

-...

## El problema (reestablecido)

- Entrada: "Lista realizadaNestedInteger título anidado `
- Cada elemento es:
* un entero
* a list of other `NestedInteger`s (nested arbitrarily)
- Profundidad de un entero = número de listas que está dentro de
- `maxDepth` = profundidad de entero más profunda
- Peso de un entero = `maxDepth - profundidad + 1`
- Devuelve la suma ponderada de todos los enteros

**Constraints* *

TEN TERRITOR ANTERIOR ANTERIOR ANTERIOR
Silencio...
TENIDO 1 ≤ `SedList.length` ≤ 50
TENIDO Valor entero ANTE [-100, 100]
Silencioso `maxDepth` ≤ 50
Silencio No hay listas vacías

-...

## El “bueno” – BFS de un par

### ¿Por qué BFS?

* **Nivel por nivel**: naturalmente rastrea la profundidad sin recidiva.
* **Iterante**: ningún riesgo de apilar desbordamiento en listas profundamente anidadas.
* **Traversal individual**: podemos computar `maxDepth`, `sumElements`, y `sumDepthProduct` en un solo paso.

### Las matemáticas

Deja:

- `S = bah integer`
- `P = bah (integer × profundidad)`
- `D = maxDepth`

La suma ponderada `W` es:

`` `
W = Governing integer × (D - profundidad + 1)
= Governing integer × (D + 1) - Governing integer × profundidad
(D + 1) × S - P
`` `

Así que después del BFS acabamos de calcular `W = (D + 1) * S - P`.

### Time & Space

← Complejidad
Silencio...
Silencio **O(n)** Silencio Cada entero/lista procesado una vez que vivieron
Silencio **O(d)** Silencio `d` = profundidad máxima; el tamaño de la cola nunca supera la amplitud del nivel actual

El código para los tres idiomas ya figura en la sección anterior.

-...

## El “Bad” – Recursión profunda

Una solución estudiantil común utiliza el DFS con recidiva, pasando la profundidad actual como parámetro. Aunque elegante, tiene trampas:

* **Desbordamiento de muelles** si la profundidad de anidación se acerca al límite de recursión (~1000 en Java, ~1000 en Python, ~10 000 en C++). La limitación de profundidad de LeetCode ≤ 50 es segura, pero a los entrevistadores les encanta empujar más fuerte.
* **Dos pases**: ya sea computar `maxDepth` primero (DFS) luego recomputar la suma ponderada, o almacenar cada entero y su profundidad en una lista, luego post-proceso.

Si debe utilizar DFS, asegúrese de:

1. Almacene pares (integer, profundidad) en un vector/array.
2. Encuentre `maxDepth`.
3. Compute `(maxDepth + 1) * S - P`.

Incluso entonces, el código se vuelve más verboso y más difícil de leer.

-...

## El “Ugly” – Intentando evitar la fórmula

Algunos participantes intentan aplicar directamente pesos durante la traversal:

``pseudo
para cada entero:
peso = (maxDepth - profundidad + 1)
resultado += entero * peso
`` `

Pero `maxDepth` es * desconocido* hasta el final de la traversal!
Así terminas:

* **Storing** todos los enteros con pesos tentativos, o
* ** Actualización** pesa sobre la mosca después de descubrir nodos más profundos (que requiere recomputación o una estructura dinámica de datos).

Este back‐and‐forth es exactamente lo que la fórmula elimina: sólo necesita * profundo × entero* una vez, luego un solo-liner para la suma final.

-...

## A Quick‐Start Checklist for Interviewers

Silencio rápido Tip Silencio Lo que el candidato debe satisfacer
Silencio...
*Use BFS, no DFS* Silencio Iterante, manejo seguro de profundidad
*Track three aggregates* ANTE `S`, `P`, `D` in one loop ANTE
*Mostrar la fórmula* Silencioso `(D +1) × S – P` – demuestra el pensamiento matemático
* límites de la pila de mención* Silencio Evitar la recursión “bad”
Silencio *Explicar espacio* tención Cuidar pantalón

-...

## SEO Boosters

Silencio SEO Pillar Silencio Cómo lo utilizamos
Silencio----------------------------
Silencio **Keywords** Silencioso “LeetCode 364”, “Nested List Weight Sum II”, “Interview BFS”, “Java Python C++ Solución”
tención **Header tags** TEN H2/H3 utilizado para el problema, algoritmo, idiomas, trampas TEN
Silencio **Puntos inteligentes** viv Clear, concise, ayuda a los lectores a esquim viv
Silencio **Camaradas de combate** Silencioso `java`, `python`, `cpp` etiquetas para los motores de búsqueda para indexar
Silencio **Descripción de la información** Silencio 155‐Caracter summary for SERPs
Silencio **Enlaces internos** Silencio Sugerir leer otros posts de problemas de LeetCode (por ejemplo, 341, 341, 107)

Siéntete libre de añadir el siguiente enlace de anclaje en la parte inferior del artículo:

``html
■a href="#javascript--java--solution" ConfederJava CodeSeguido/a confiar 
■a href="#python-3-solution"
■a href="#c++-solution" Código No.
`` `

-...

Conclusión

LeetCode 364 es una buena ilustración de cómo un simple problema puede tener soluciones elegantes, eficientes y arriesgadas. El **one‐pass BFS** es el más fácil de entrevistar:

1. **Iterante** – sin límites de recursión.
2. **Tiempo de trabajo** – un escaneo de toda la lista.
3. **Mathematically concise** – una sola línea de aritmética después del bucle.

Utilice los fragmentos de código anteriores para agregar a su GitHub, cartera o repo de práctica personal.
Siéntete libre de copiar el artículo en Medium, Dev.to, o tu blog personal y míralo clasificar para *“LeetCode 364”*.

¡Feliz codificación y buena suerte en tu próxima entrevista! 🚀

-...

#### TL;DR

* **Problema** – Suma ponderada con profundidad inversa.
* **Buena solución** – Un paso BFS + `(maxDepth+1)*S – P`.
* ** Solución básica** – Recursive DFS que puede rebosar.
* **Intentamente** – Intento aplicar pesos directamente sin la fórmula.

El código Java, Python y C++ está listo para copiar y pasar y pasará cada prueba oficial de LeetCode.