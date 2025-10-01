-...
Título: LeetCode 2684. Número máximo de movimientos en una rejilla -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
``dart
importar 'dart:math';

vacío principal() {}

Clase Solución {
int maxMoves(Listecto)Listctoint títulos
int m final = grid.length;
final int n = grid[0].length;
final List ofgenerate(m, (_) = Lista.filled(n, 0));

para (int col = n - 2; col = 0; col--) {}
for (int row = 0; row < m; row++) {}
si (hacia el rito 0 " círculo [row] [col] [rejilla] [row - 1] [col + 1] {
dp[row][col] = max(dp[row][col], dp[row - 1][col + 1] + 1);
}
si (grid[row] [col] [llamado]
dp[row][col] = max(dp[row][col], dp[row][col + 1] + 1);
}
si (hacia cautivar m - 1 " curva[row] [col] se ha buscado cuadrícula [row + 1] [col + 1]
dp[row][col] = max(dp[row][col], dp[row + 1][col + 1] + 1);
}
}
}

int result = 0;
for (int row = 0; row < m; row++) {}
resultado = max(resultar, dp[row][0]);
}
Resultado de retorno;
}
}
`` `