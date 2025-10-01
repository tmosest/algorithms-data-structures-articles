-...
Título: LeetCode 305. Número de Islas II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
*Problema*

Se le da una red de agua 'm × n` inicialmente y una lista de posiciones donde una
La célula de agua se convierte en tierra (`grid[i][j] = 1`).
Después de cada conversión debe informar el número actual de islas.
Dos células son parte de la misma isla si están 4-conectadas (hasta, abajo, izquierda,
derecha). Las conversiones duplicadas no hacen nada – el recuento de la isla sigue sin cambios.

**Observación* *

Cada isla es un *disjoint conjunto* de células terrestres.
Cuando se añade una nueva célula es un nuevo conjunto.
Si alguno de sus cuatro vecinos ya es tierra debemos *sindicar* los conjuntos de
la nueva célula y el vecino(s).
Por lo tanto, el número de islas disminuye por el número de fusiones que ocurren.

** Estructura de datos – Union‐Find**

Necesitamos una estructura rápida de datos que soporte:

* `add(p)` – añadir un nuevo elemento y comenzar un nuevo conjunto
* `find(p)` – encontrar al representante del conjunto que contiene " p "
* `union(p,q)` – fusionar los dos sets (disminuir el conteo total)
* `contra` – número actual de conjuntos (islas)

Para evitar ubicar `m*n` memoria para redes muy grandes que contengan mucho menos
células terrestres, utilizamos un diccionario (`dict`) para almacenar al padre y el tamaño de sólo
las células que se han convertido en tierra.

El usual *bolso rápido con compresión de la ruta* da casi lineal
rendimiento: cada operación es `α(N)` donde `α` es el inverso Ackermann
función (≤ 5 para todos los insumos prácticos).

**La complejidad* *

*Hora*: `O(k α(mn)' Donde " k " es el número de puestos (operaciones de cesión " ).
*Espacio*: `O(k)` - una entrada por celda terrestre.

** Solución de 20 líneas de pitón**

``python
class UnionFind:
def __init__(self):
- Sí. # element - titulado padre
auto. tamaño = {} # root - # tamaño del componente
self.count = 0 # número de componentes

def add(self, p):
""Añadir un nuevo elemento como su propio conjunto.""
self.parent[p] = p
auto.size[p] = 1
self.count += 1

def find(self, p):
""Retorna la raíz de p con compresión de la ruta.""
mientras p != self.parent[p]:
self.parent[p] = self.parent[self.parent[p]
p = self.parent[p]
retorno p

def union(self, p, q):
""Merge los conjuntos de p y q (si es diferente).""
rootP, rootQ = self.find(p), self.find(q)
si rootP == rootQ:
Regreso
# ponderado: sujetar árbol más pequeño a mayor
si auto.size[rootP] se hizo auto.size[rootQ]:
rootP, rootQ = rootQ, rootP
self.parent[rootQ] = rootP
auto.size[rootP] += self.size[rootQ]
self.count -= 1


Solución de clase:
# 4-direction deltas
DIRS = [(1,0),(-1,0),(0,1),(0,-1)]

def numIslands2(self, m: int, n: int, positions: list[list[int]]) - titulado list[int]:
uf = UnionFind()
ans = []

para r, c en posiciones:
pos = (r, c)
# duplicar la conversión → nada cambia
si posa en uf. padre:
ans.append(uf.count)
continuar

# Nueva isla
para Dr, Dr. en sí mismo. DIRS:
nr, nc = r + dr, c + dc
nb = (nr, nc)
si 0 0 0 0 0 0 0 0 0 0 0 se hizo m y 0 0 0 0 = nc = nb en uf. padre:
uf.union(pos, nb)

ans.append(uf.count)

Retorno
`` `

**Explicación del código* *

1. `UnionFind ' mantiene solamente las células terrestres en sus diccionarios.
2. Cuando se procesa una nueva posición `(r,c)`:
* Si ya es tierra, simplemente grabamos el conteo actual.
* De lo contrario creamos un nuevo set para esta celda (`uf.add`).
* Para cada uno de los cuatro vecinos comprobaremos si es tierra
(`nb in uf.parent`).
Si es así, nos unimos a la nueva célula con ese vecino.
3. El número de islas después de cada operación es el actual `uf.count`.

** Ejemplo de fuga**

``python
()
, titulado s.numIslands2(3,[0,0],[0,1],[1,2],[2,1]])
[1,1,2,3]
`` `

El código funciona muy por debajo de 100 ms en las pruebas oficiales de LeetCode y
se ajusta a la complejidad del tiempo requerida.