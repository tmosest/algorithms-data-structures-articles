-...
Título: LeetCode 3240. Número mínimo de Flips para hacer la Palindromica Parcial Grid II -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
**Respuesta*

Para una matriz binaria uniforme el problema se divide en grupos independientes de 4 celdas.
Vamos.

`` `
(i , j) – esquina superior izquierda del grupo
(i , m-1-j) – esquina superior derecha
(n-1-i , j) – esquina inferior izquierda
(n-1-i , m-1-j) – esquina inferior derecha
`` `

(Aquí `n` es el número de filas y `m` el número de columnas.)

Para cada grupo podemos hacer las cuatro células 0 o las cuatro células 1 –
ambas opciones garantizan que cada submatrix 2×2 tiene un número uniforme de 1’s.
El costo de las dos opciones es

`` `
cnt = suma de las cuatro células
costAllZero = cnt // flip all 1→0
costAllOne = 4 - cnt // flip all 0→1
`` `

Por lo tanto, el costo mínimo para ese grupo es `min(cnt, 4-cnt)`.
Añadiendo los costos sobre todos los grupos da el óptimo global porque el
grupos son descomunales e independientes.

``java
Clase Solución {
int public minFlips(int[] grid) {
int n = grid.length, m = grid[0].length;
int ans = 0;
para (int i = 0; i) {}
para (int j = 0; j)
int cnt = grid[i][j] + grid[i][m-1-j]
+ grid[n-1-i][j] + grid[n-1-i][m-1-j];
ans += Math.min(cnt, 4 - cnt);
}
}
devolver los ans;
}
}
`` `

Por lo tanto, ** el número mínimo de vueltas equivale a la suma de `min(cnt, 4-cnt)`. sobre todo
Grupos de 4 celdas**.
Esta solución funciona en **O(n · m)** tiempo y utiliza **O(1)** espacio extra.