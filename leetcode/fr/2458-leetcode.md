---
titre: LeetCode 2458. Hauteur de l'arbre binaire après la suppression des sous-arbres -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
"Java
solution de classe {
profondeur privée, gauche, droite;
Int privé[] hauteurs des feuilles;
feuille d'inte privée Compte;
MAX_LEAF = 50000;
MAX_NODES = 100001;

public int[] treeQueries(Rope TreeNode, inter[] requêtes) {
profondeur = nouvelle int[MAX_NODES];
gauche = nouvelle int[MAX_NODES];
droite = nouveau int[MAX_NODES];
heights = nouvelle int[MAX_LEAF];
nombre de feuilles = 0;

dfs(racine, 0);

int n = feuilleCoupe;
int[] prefMax = nouvelle int[n];
int[] suffMax = nouvelle int[n];

pour (int i = 1; i < n; i++) {
prefMax[i] = Math.max(prefMax[i - 1], feuilleHauteur[i - 1]);
suffMax[n - i - 1] = Math.max(suffMax[n - i], feuilleHauteurs[n - i]);
}

int[] res = nouvelle int[queries.longueur];
pour (int i = 0; i < requêtes.longueur; i++) {
int q = requêtes[i];
int maxLeft = prefMax[left[q]];
int maxRight = suffMax[right[q]];
int maxAutre = Math.max(maxLeft, maxRight);
res[i] = Math.max(maxAutre, profondeur[q] - 1);
}
retour rés;
}

vide privé dfs(nœud TreeNode, int d) {
profondeur[node.val] = d;
Si (noeud.left) null && node.right == null) {
hauteurs des feuilles[colte des feuilles] = d;
gauche[node.val] = droite[node.val] = feuilleCoupe;
feuille Nombre++;
retour;
}
gauche[node.val] = feuilleCoupe;
si (node.left != null) dfs(node.left, d + 1);
si (node.right != null) dfs(node.right, d + 1);
droite[node.val] = feuilleCount - 1;
}
}
«» "