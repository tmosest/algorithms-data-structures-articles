-...
Título: LeetCode 3235. Compruebe si el Rectangle Corner es accesible -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
### Union‐Find (Disjoint‐Set Union, DSU)

Union‐Find es una estructura de datos muy rápida que mantiene un seguimiento de una partición de un conjunto en subconjuntos **disjoint (no superposición)**.
Puedes

1. **Encontrar** a qué subconjunto pertenece un elemento.
2. **Unión** (merge) dos subconjuntos en uno.

Es la columna vertebral de muchos algoritmos: MST de Kruskal, detección de ciclos en gráficos, conectividad de red, procesamiento de imágenes, etc.

-...

## 1. Lo que la estructura almacena

Silencio Silencio
Silencio...
Por cada elemento `i`, el padre de 'i' en un bosque. Si `i` es una raíz de un árbol, `parent[i] == i. Silencio
Silencio `rank[i]` (o `size[i]`) TENIENDO Aproximadamente la altura (o tamaño) del árbol cuya raíz es `i`. Solía mantener los árboles poco profundos. Silencio

Inicialmente, cada elemento es su propio conjunto:

``text
padre [i] = i
rango[i] = 0 (o tamaño[i] = 1)
`` `

Todos los conjuntos están representados como un bosque de árboles.

-...

## 2. Operaciones

### `find(x)` – localizar el conjunto que contiene `

``pseudo
función find(x):
si padre[x]!= x:
parent[x] = find(parent[x]) // Compresión del camino
padre de retorno[x]
`` `

*Recursivamente camina hasta la raíz. *
Durante el paseo, **comprimir el camino**: cada nodo visitado apunta directamente a la raíz.
Después de un 'encuentro', la profundidad del árbol se convierte en la mayoría de 1 para los nodos visitados.

### `union(x, y)` – fusionar los conjuntos que contienen `x' y `y `

``pseudo
función union(x, y):
rootX = find(x)
rootY = find(y)
si rootX == rootY: retorno // ya en el mismo conjunto

// Unión por rango (o por tamaño)
si el rango[rootX] identificó el rango [rootY]:
parent[rootX] = rootY
si el rango[rootX] > rank[rootY]:
parent[rootY] = rootX
más:
parent[rootY] = rootX
rank[rootX] += 1
`` `

Si las filas son iguales, elegimos arbitrariamente una como nueva raíz y aumentamos su rango.

-...

## 3. Por qué es rápido

- Cada 'find' hace la compresión del camino → el árbol se convierte en un solo nivel en las próximas visitas.
- Cada "unión" sujeta el árbol más pequeño bajo el más grande (por rango) → la profundidad del árbol permanece baja.

El tiempo amortizado por operación es **inverso Ackermann**:
`α(n) ♥ 4` para todo práctico `n`. En resumen, es esencialmente *O(1)* para todos los insumos realistas.

-...

## 4. Ejemplo rápido

Supongamos que tenemos elementos 0...5. Haremos sindicatos:

`` `
sindical(0,1) // sets: {0,1} {3} {4} {5}
sindical(2,3) // sets: {0,1} {2,3} {4} {5}
union(1,2) // fusionar los dos conjuntos
`` `

Después de esas operaciones:

`` `
encontrar(0) → root r
encontrar(5) → root 5 (diferente)
`` `

La estructura después de la compresión puede parecer:

`` `
padres = [r, r, r, r, 4, 5]
rango = [1, 0, 0, 0, 0, 0, 0]
`` `

Todos los nodos en el conjunto fusionado ahora apuntan directamente a `r`.

-...

## 5. Maleta de uso común: Árbol mínimo de esparcimiento de Kruskal

``pseudo
bordes clasificados por peso
para cada borde (u,v) en orden:
si encuentra(u) != find(v):
añadir borde al MST
union(u,v)
`` `

Debido a que `find` rápidamente dice si añadir un borde crearía un ciclo, podemos construir un MST en `O(E log V)` tiempo.

-...

## 6. C++/Python snippets

### C++ (compactar)

``cpp
struct DSU {}
vector:
DSU(int n=0) { init(n); }

init(int n){
parent.resize(n);
rank.assign(n,0);
iota(parent.begin(), parent.end(), 0);
}

int find(int x){
volver padre[x]=x ? x : parent[x]=find(parent[x]); // path compresión
}

vacío unite(int a, int b){
a=find(a); b=find(b);
si (a==b) regresa;
si (arranque[a]) swap(a,b);
parent[b]=a;
si (rank[a]==rank[b]) rango[a]+;
}
};
`` `

## Python (clear)

``python
clase DSU:
def __init__(self, n):
self.parent = list(range(n))
self.rank = [0]*n

def find(self, x):
si yo. parent[x]!= x:
self.parent[x] = self.find(self.parent[x]) # path compresión
Vuélvete. parent[x]

def union(self, a, b):
a, b = self.find(a), self.find(b)
si a ==b: retorno
si auto.rank[a] se auto.rank[b]:
a, b = b, a
self.parent[b] = a
si yo. rango[a] == self.rank[b]:
self.rank[a] += 1
`` `

-...

## 7. Take-away

*Union‐Find* es una estructura casi constante para mantener una partición de elementos bajo operaciones sindicales.
Con la compresión **path** y **union por rango/tamaño** garantiza amortizado `O(α(n)' por operación, que es prácticamente *O(1)*.
Su sencillez y velocidad lo hacen indispensable en algoritmos gráficos y muchas otras aplicaciones.