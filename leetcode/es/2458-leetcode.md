-...
Título: LeetCode 2458. Altura del árbol binario después de las consultas de eliminación de subárbol -
descripción: Titular
Fecha: 2025-09-21
categorías: []
autor: muses
tags: []
HideToc: verdadero
-...
``java
Clase Solución {
int privado[] profundidad, izquierda, derecha;
int[] hojaAlturas;
hoja de entrada privada Cuenta;
int final estático privado MAX_LEAF = 50000;
int final estático privado MAX_NODES = 100001;

int[] árbolQueries(TreeNode root, int[] consultas) {}
profundidad = nuevo int[MAX_NODES];
izquierda = nuevo int[MAX_NODES];
derecho = nuevo int[MAX_NODES];
hojaAlturas = nuevo int [MAX_LEAF];
hojaCount = 0;

dfs(root, 0);

int n = leafCount;
int[] prefMax = nuevo int[n];
int[] suffMax = nuevo int[n];

para (int i = 1; i) {}
prefMax[i] = Math.max(prefMax[i - 1], leafHeights[i - 1]);
suffMax[n - i - 1] = Math.max(suffMax[n - i], leafHeights[n - i]);
}

int[] res = nuevo int[queries.length];
para (int i = 0; i) hice consultas.length; i++) {
int q = consultas[i];
int maxLeft = prefMax[left[q]];
int maxRight = suffMax[right[q];
int maxOther = Math.max(maxLeft, maxRight);
res[i] = Math.max(maxOtras, profundidad[q] - 1);
}
restitución;
}

dfs privado(TreeNode node, int d) {
profundidad[node.val] = d;
si (nodo.left == null " node.right == null) {
hojaAlturas[leafCount] = d;
left[node.val] = right[node.val] = leafCount;
hoja Conteo++;
retorno;
}
left[node.val] = leafCount;
si (node.left != null) dfs(node.left, d + 1);
si (node.right != null) dfs(node.right, d + 1);
right[node.val] = leafCount - 1;
}
}
`` `