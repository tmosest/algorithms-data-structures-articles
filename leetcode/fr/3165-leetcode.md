---
titre: LeetCode 3165. Somme maximale de la séquence avec éléments non adjacents -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Le problème**
Après chaque mise à jour `arr[p] = v` nous devons rapporter la somme maximale de
sous-réseau dans lequel deux éléments choisis ne sont pas adjacents.
Un balayage linéaire pour chaque requête (`O(n)` par requête) est beaucoup trop lent,
par conséquent une structure de données qui peut être mise à jour dans `O(log n)` et à partir de
que la réponse peut être lue dans "O(1)" est nécessaire.

---

- Oui. Pourquoi les trois premières solutions TLE

Solution: complexité: raison: TLE
- C'est pas vrai.
Pour chaque requête, nous recalculons le DP à partir de zéro. Autres
Un arbre Fenwick donne des sommes de préfixe – il ne peut pas garder le
Informations nécessaires pour le maximum
somme non adjacente.
La récursion reconstruise l'arbre entier pour chaque requête,
encore `O(n)` par mise à jour. Autres

Donc aucun des trois premiers ne résout le problème dans le besoin
"O(n+q) log n)".

---

- Oui. Comment le résoudre avec un arbre segmentaire

Pour chaque segment `[l...r]` nous conservons quatre valeurs qui décrivent la meilleure
les sommes possibles selon que le premier élément du segment est
prises ou non, et si le dernier élément du segment est pris ou non,
Pas.

«» "
0 1 (état de la limite gauche)
0 f00 f01 (meilleure somme en [l...r] lorsque la limite gauche n'est pas prise)
1 f10 f11 (meilleure somme lorsque la limite gauche est prise)
«» "

`f01` et `f10` sont égaux (symétrie) – la matrice est toujours symétrique,
Donc nous ne stockons que 4 numéros.

*Leaf*
Pour un seul élément «a»:

«» "
f00 = 0 (ne rien prendre)
f01 = f10 = a (prendre l'élément)
f11 = a
«» "

*Combinez deux enfants*

Que `L` soit la matrice de l'enfant gauche et `R` celle de l'enfant droit.
La nouvelle matrice `M` est obtenue comme suit (seulement deux combinaisons sont
possible – nous ne pouvons pas prendre un élément dans l'enfant gauche si nous prenons aussi
le premier élément de l'enfant droit:

«» "
M00 = max( L00 + R00 , L00 + R01 , L01 + R00 ) // prendre aucun à la limite
M01 = max( L00 + R01 , L00 + R11 , L01 + R01 ) // gauche non prise, prise à droite
M10 = max( L10 + R00 , L10 + R01 , L11 + R00 ) // gauche prise, droite non prise
M11 = max( L10 + R01 , L10 + R11 , L11 + R01 ) // prendre les deux limites
«» "

Les quatre nombres sont calculés avec `max`, donc l'arbre fonctionne toujours
avec "long" (la somme peut être aussi grande que `1014`).

*Mise à jour*
Pour changer un élément nous descendons l'arbre à la feuille
(`O(log n)`) et ensuite repousse les matrices sur le chemin de retour à la
racine – aussi `O(log n)`.

*Réponse*
Après une mise à jour, la réponse est simplement la meilleure somme dans tout le tableau,
c'est-à-dire le maximum des deux matrices
élément:

«» "
réponse = max( seg[0][0][1] , seg[0][1] )
«» "

La matrice racine donne la réponse instantanément, donc la complexité globale
est "O(n + q) log n)".

---

### Correction de l'implémentation Java

"Java
solution de classe {

int final statique privé[] FULL = nouveau int[] {
{0, 1},
{1, 1}
};

matrice privée longue[][] seg; // 2×2 pour chaque noeud
Int. privé n;

/* construire l'arbre **------------------------------------------------
construction privée vide(int idx, int l, int r, int[] arr) {
si (l) r) { // feuille
seg[idx][0]=0;
seg[idx][0][1] = seg[idx][1][0] = seg[idx][1][1] = arr[l];
retour;
}
Int milieu = (l + r) >> 1;
build(idx <=1, l, milieu, arr);
build(idx << 1= 2, milieu + 1, r, arr);
Tire(idx);
}

/* recalculer un nœud de ses deux enfants ----------- */
Tir à vide privé(int idx) {
int gauche = idx << 1=1, droite = idx << 1=2;
pour (int i = 0; i < 2; ++i) {
pour (int j = 0; j < 2; ++j) {
long best = Long.MIN_VALUE;
// gauche non prise (i==0) ou prise (i==1) + droite non prise (0) ou prise (1)
// nous ne pouvons pas prendre les deux extrémités adjacentes – sauter ce cas
best = Math.max(best, seg[left][i][0] + seg[right][0][j]); // skip right end
best = Math.max(best, seg[left][i][1] + seg[right][1][j]); // prendre à droite
seg[idx][i][j] = meilleur;
}
}
}

/* mise à jour du point ---------------------------------------------------- */
privé vide mise à jour(int idx, int l, int r, int pos, int val) {
si (l) r) { // feuille
seg[idx][0]=0;
seg[idx][0][1] = seg[idx][1][0] = seg[idx][1][1] = valeur;
retour;
}
Int milieu = (l + r) >> 1;
i (pos <= mi) mise à jour(idx << 1= 1, l, mi, pos, val);
autre mise à jour(idx << 1) 2, mi + 1, r, pos, val);
Tire(idx);
}

/* routine principale ---------------------------------------------------- */
public int[] maxNonAdjacent(int[] arr, int[][] requêtes) {
n = longueur normale;
seg = nouveau long[4 * n][2][2];
(0, 0, n - 1, arr);

int[] result = nouvelle int[queries.longueur];
pour (int k = 0; k < requêtes.longueur; ++k) {
int p = requêtes[k][0];
int v = requêtes[k] [1];
mise à jour(0, 0, n - 1, p, v);

// la réponse est la meilleure somme qui se termine dans le dernier élément
résultat[k] = (int) Math.max(seg[0][0][1], seg[0][1][1];
}
le résultat du retour;
}
}
«» "

---

- Oui. Pourquoi un arbre de Fenwick (BIT) ne **pas** fonctionne

Un arbre Fenwick ne peut maintenir une fonction *additive* que sur les préfixes
(par exemple la somme d'une fourchette).
La somme maximale non proportionnelle est **non** additive: la valeur DP à
la position `i` dépend de la prise ou non de `i‐1`, qui à son tour
dépend de la valeur de «i‐2».
Ces dépendances ne peuvent pas être représentées par une simple somme préfixe,
L'arbre Fenwick ne peut jamais produire la bonne réponse.

---

### En bas

* Les trois premières soumissions sont soit trop lentes, soit mal utilisées.
la structure des données.
* La solution correcte utilise un arbre de segment qui maintient les quatre DP
valeurs décrites ci-dessus et les fusionne dans `O(1)` temps par noeud.
* Après chaque mise à jour, nous lisons la réponse de la racine dans `O(1)`, et
toutes les mises à jour prennent `O(log n)` le temps, donnant un ensemble
Algorithme `O(n+q) log n)` qui passe les limites.