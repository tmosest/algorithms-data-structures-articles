-...
Título: LeetCode 894. Todos los árboles binarios posibles -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
*El problema*
Para un número impar `n` debemos regresar *todo* distintos árboles binarios completos que contienen `n` nodos.
Si construimos los árboles reutilizando subárboles que ya hemos creado, los árboles que regresamos terminan compartiendo nodos (los denominados árboles *Frankenstein*).
Cuando un callador muta uno de los árboles devueltos muta silenciosamente a los otros – un comportamiento que la mayoría de los clientes no esperarían.

La única manera segura de satisfacer el contrato es ** cerrar cada subárbol antes de que se adhiera a una nueva raíz**.
Puede mantener la estructura original (compartida) en una tabla de memoización para evitar la recomputación, pero cuando realmente forma la lista que devuelve debe duplicar la estructura del árbol.

A continuación se presenta una aplicación Python concisa y plenamente documentada que hace exactamente eso.

-...

## 1. Idea

1. **Pronto números** – un árbol binario completo puede tener sólo un número extraño de nodos.
2. **Memoise** – una vez que hemos producido todos los árboles para un particular `n` almacenamos el resultado en un diccionario para que más tarde llame a la misma `n` pueda devolver la lista de caché al instante.
3. **Edificio de los sub-árboles** – por cada división extraña `i` (nodos de izquierda) y `n‐1-i` (nodos derecho) combinamos cada árbol izquierdo con cada árbol derecho creando una nueva raíz.
4. **Clone** – cada vez que combinamos un par que copiamos profundamente los subárboles izquierdo y derecho para que los árboles resultantes sean independientes.

-...

## 2. Complejidad

*Sea el número de árboles binarios llenos con nodos. *

`` `
T(1) = 1
T(n) = ega_{i odd, 1≤i maden} T(i) · T(n‐i‐1) (n odd)

`` `

La secuencia crece como los números catalanes:
`T(1)=1, T(3)=1, T(5)=2, T(7)=5, T(9)=14, ...`

* **Tiempo** – cada árbol se construye una vez y se almacena en la mesa de memoización.
El número asintotico de operaciones es Ø( T(n) · n ) Ω( 2^n ).
* **Espacio** – la mesa de memoización sostiene todos los árboles hasta el tamaño `n`.
La profundidad más profunda de la recursión es `n/2`, por lo que el espacio auxiliar es Ø(n).

-...

## 3. Código

``python
Definición para un nodo de árbol binario.
# class TreeNode:
# def __init__(self, val=0, left=None, right=None):
# self.val = val
# Yo. izquierda = izquierda
# Yo. derecho = derecho

de la importación Lista, Dict

Solución de clase:
# cache: n → lista de todos los árboles binarios llenos con n nodos
_cache: Dict[int, List['TreeNode'] = {}

def allPossibleFBT(self, n: int) - titulada List['TreeNode']:
# Árbol binario completo sólo existe para extrañar #
si n % 2 == 0:
retorno []

# Resultado memoizado
si no en uno mismo.
volver a sí mismo._cache[n]

resultado: Lista ['TreeNode'] = []

si n == 1:
# Funda base - un solo árbol de nodos
result.append(TreeNode(0))
más:
# split the remaining n‐1 nodes into two odd parts
para izquierda_cnt en rango(1, n, 2):
right_cnt = n - 1 - left_cnt
left_trees = self.allPosibleFBT(left_cnt)
right_trees = self.allPosibleFBT(right_cnt)

# combinar cada izquierda con cada derecha
para l en izquierda_trees:
para r en right_trees:
# deep‐copy both sub-trees before attaching
root = TreeNode(0, self._clone(l), self._clone(r))
result.append(root)

# Recuerda el resultado de futuras llamadas
auto._cache[n] = resultado
Resultado de retorno

# -------- helper: copia profunda de un árbol----------
def _clone(self, node: 'TreeNode') - título 'TreeNode':
""Retorna una copia profunda del subárbol arraigado en el nodo.""
si el nodo es Ninguno:
No.
# crear un nuevo nodo y clonar niños repetidamente
devolver TreeNode(0, self._clone(node.left), self._clone(node.right))
`` `

### ¿Por qué el explícitamente '_clone'?

*Si lo hiciste **no** clon*:

``python
root = TreeNode(0, l, r) # [ ]]
`` `

usted estaría adjuntando los *same* `TreeNode` objetos a muchas raíces diferentes.
Esos árboles no serían independientes; formarían una estructura de Frankenstein.

La clonación garantiza que cada llamada a 'self._clone` devuelve un nuevo subtree, por lo que el llamante puede modificar libremente cualquier árbol en la lista de resultados sin afectar a los demás.

-...

## 4. Un cheque corto de cordura

``python
sol = Solución()
árboles = sol.allPosibleFBT(5) # 2 árboles

# muta la hoja más izquierda del primer árbol
árboles[0].left.left.val = 42

# El segundo árbol no cambia - realmente hicimos clon
print(trees[1].left.val) # still 0
`` `

Si omitiste el paso de clonación, el segundo árbol mostraría el valor mutado '42', demostrando que los nodos compartidos habían sido rotos.

-...

## 5. Why LeetCode sometimes accepts non-cloned solutions

LeetCode sólo comprueba que el *forma* de los árboles devueltos coincide con el número esperado.
El arnés de prueba nunca muta ningún nodo después de que la función regrese, por lo que una solución que simplemente reutiliza los sub-árboles caché (TreeNode(0, l, r)`) pasa todas las pruebas.

Sin embargo, en el código de producción (o cuando quieres una biblioteca robusta) no puedes asumir que los calladores nunca modificarán los árboles devueltos.
La estrategia de clone-before-attach mostrada anteriormente es la forma correcta, sin efectos secundarios para implementar el contrato.