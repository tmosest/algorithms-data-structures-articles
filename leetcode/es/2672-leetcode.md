-...
Título: LeetCode 2672. Número de elementos adyacentes con el mismo color -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Esquema de la solución**

Por cada consulta sólo cambiamos el color de una celda.
Después de este cambio sólo necesitamos saber si esta célula ahora forma un *pair*
con su vecino izquierdo o su vecino derecho.

El número total de pares es la respuesta para esa consulta.
Vamos.

`` `
cnt – número actual de pares adyacentes de igual color
col[i] – color actual de la célula i (0 = sin color)
`` `

Para una consulta `(pos , nuevo Color)`:

1. **Remueva los viejos pares contribuidos por `col[pos].**
Si 'col [pos] no fue cero y coincidió con el vecino izquierdo → 'cnt--`.
Si coincidía con el vecino derecho → 'cnt--`.

2. **Pinta la celda. #
`col[pos] = nuevoColour`.

3. **Agrega los nuevos pares creados por 'nuevo Color'.**
Si el vecino izquierdo no es cero y es igual a 'nueva naturaleza' → `cnt+`.
Si el vecino correcto no es cero y es igual a `nueva naturaleza' → `cnt+`.

Almacene 'cnt' después de cada consulta.
Todas las operaciones para una consulta son O(1), por lo que todo el algoritmo es O(m) donde `m` es el número de consultas.

-...

#### Python implementation

``python
de la importación Lista

Solución de clase:
def color TheArray(self, n: int, queries: List[List[int]) - No. List[int]:
colores = [0] * n # colores actuales, 0 = sin color
res = [] # respuestas para cada consulta
pares = 0 # número actual de pares de igual color

para pos, new_colour en consultas:
old_colour = colores[pos]

# Remove old pairs involving pos
si viejo_color != 0:
si pos > 0 y colores[pos-1] == old_colour:
pares -= 1
si pos + 1 < n y colores[pos+1] == old_colour:
pares -= 1

# pintura pos con el nuevo color
colores [pos] = nuevo_color

# añadir nuevos pares creados por el nuevo color
si pos Ø 0 y colores [pos-1] == new_colour:
pares += 1
si pos + 1 < n y colores[pos+1] == new_colour:
pares += 1

res.append(pairs)

retorno
`` `

### Java implementation (15-line clean code)

``java
Clase Solución {
int[] colorTheArray(int n, int[][ ] {
int[] col = nuevo int[n];
int[] ans = nuevo int[queries.length];
int cnt = 0;

para (int i = 0; i) hice consultas.length; i++) {
int pos = consultas[i][0];
int newCol = consultas[i][1];

si (col[pos]!= 0) {
si cnt...
si (pos + 1 iere n ' t ' cnt [pos+1] == col [pos])
}

col[pos] = nuevo Col;

cnt++;
si (pos + 1 ■ n " rótulos [pos+1] == newCol) cnt++;

ans[i] = cnt;
}
devolver los ans;
}
}
`` `

### C++ Implementación (compactar 15-line)

``cpp
Clase Solución {
public:
vector de instrucciones de colorTheArray(int n, vector asignadovector fieltro implicados iguales queries) {}
vector implicado col(n, 0), ans(queries.size());
int cnt = 0;
para (int i = 0; i) ++i) {
int pos = consultas[i][0], c = consultas[i][1];
si (col[pos]!= 0) {
si (pos " 0 " col[pos-1] == col [pos]) -- cnt;
si (pos + 1 י n ' t ' cnt);
}
col [pos] = c;
si (pos latitud 0 " coli[pos-1] == c) ++cnt;
si (pos + 1 0) c) ++cnt;
ans[i] = cnt;
}
devolver los ans;
}
};
`` `

-...

### Complexity

TEN TERRITOR TEN TEN ANTE
Silencio...
TENIENDO TERRENO **O(m)**, `m` = number of queries TEN
TENIDO ESPACIO TENIDO **O(n)** para la matriz de colores (plus O(m) para el resultado)

Esta solución es óptima: cada consulta se procesa en tiempo constante.