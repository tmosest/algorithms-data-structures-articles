---
titre: LeetCode 3287. Trouver la valeur de séquence maximale de l'image -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3287 – Trouvez la valeur de séquence maximale de l'image
**Hard – LeetCode**

Langue Complexité Code
- C'est quoi ?
*Java * O(n · k · 32) * 2.6 M ops <details> <sommary> Java 17</résumé>... </détails>
**Python**= O(n · k · 32)= <details><sommaire>=Python 3.11</sommaire></details>=
**C++**= O(n · k · 32)= <details><sommaire>C++ 23</résumé>... </détails>

> **Pourquoi cela compte pour votre dossier d'entrevue**
> Le problème vous force à combiner **sélection de séquence** avec **bitwise OR/XOR** – deux agrafes dans les entrevues de codage.
> La maîtrise de ce modèle DP‐bitmask montre que vous pouvez raisonner sur les contraintes, l'espace d'état et une énumération efficace – une compétence incontournable pour les rôles de backend senior.

---

TL;DR

* Le but : choisir une séquence de longueur `2k` (éléments k, puis éléments k) pour maximiser
"(OU du premier k) XOR (OU du dernier k)".
* Parce que chaque `nums[i]` est `< 27`, la OU de tout groupe correspond en 5 bits → **32 possibles masques OU**.
* Utilisez deux tableaux DP :
* **préfixe DP** – index le plus précoce où une OU donnée peut être obtenue avec des éléments exactement `t`.
* **Suffix DP** – dernier index où une OU donnée peut être obtenue avec des éléments exactement "t".
* Après avoir rempli les deux tables, itérer sur toutes les paires de masques, vérifier que l'index de préfixe < suffixe, et prendre le XOR maximum.

---

## Solution complète (Java)

"Java
Importation de java.util.*;

solution de classe publique {
valeur(int[] nombres, int k) {
int n = longueur nums;
Int final MAX_MASK = 1 << 5; // 0,31 (depuis nombres[i] < 27)
Int final INF = n + 1; // marqueur d ' indice impossible

// ---- Préfixe DP: premier index pour obtenir OR==masque avec éléments t ----
int[][] pref = nouvelle int[k + 1][MAX_MASK];
pour (int t = 0; t <= k; t++)
pref[0][0] = -1; // 0 éléments avant le tableau

pour (int i = 0; i < n; i++) {
Int val = nombres[i];
// itérer t en sens inverse pour éviter de réutiliser le même élément
pour (int t = Math.min(k, i + 1); t >= 1; t--) {
pour (int masque = 0; masque < MAX_MASK; masque++) {
si (pref[t-1][masque] <= i - 1) { // nous pouvons prendre cet élément
int newMask = masque val;
pref[t][newMask] = Math.min(pref[t][newMask], i);
}
}
}
}

// enregistrer le premier index pour chaque masque OU
int[] first = nouveau int[MAX_MASK];
les tableaux.fill(premier, INF);
pour (int mask = 0; masque < MAX_MASK; mask++) premier[mask] = pref[k][mask];

// ---- Suffix DP: dernier indice pour obtenir OR==masque avec éléments t ----
int[[]] suff = nouvelle int[k + 1][MAX_MASK];
pour (int t = 0; t <= k; t++) Arrays.fill(suff[t], -INF);
suff[0][0] = n; // 0 éléments après le tableau

pour (int i = n - 1; i >= 0; i--) {
Int val = nombres[i];
pour (int t = Math.min(k, n - i); t >= 1; t--) {
pour (int masque = 0; masque < MAX_MASK; masque++) {
si (suff[t-1][masque] >= i + 1) {
int newMask = masque val;
suff[t][newMask] = Math.max(suff[t][newMask], i);
}
}
}
}

// enregistrer le dernier index pour chaque masque OU
int[] last = nouveau int[MAX_MASK];
Les tableaux.fill(dernier, -INF);
pour (int mask = 0; masque < MAX_MASK; mask++) last[mask] = suff[k][mask];

// ---- Scanner toutes les paires de masques pour obtenir le meilleur XOR ----
réponse int = 0;
pour (int m1 = 0; m1 < MAX_MASK; m1++) {
si (premier[m1] == INF) continue; // ne peut pas obtenir cette OU dans le préfixe
pour (int m2 = 0; m2 < MAX_MASK; m2++) {
si (dernier[m2] == -INF) continuer; // ne peut pas obtenir ce OU en suffixe
si (premier[m1] < dernier[m2]) // les indices ne se chevauchent pas
réponse = Math.max(réponse, m1 ^ m2);
}
}
réponse de retour;
}
}
«» "

- Oui. Pourquoi ça marche

* ** État** – "pref[t][masque]` stocke *le plus petit indice* où nous pouvons choisir des éléments `t` jusqu'à ce point dont OU égale `masque`.
S'il est toujours `INF`, que OU est inaccessible avec exactement `t` éléments.
* Transition – inclure l'élément actuel «nums[i]»: `newMask = oldMask" nums[i]`.
Nous conservons l'indice le plus ancien car nous le comparerons plus tard avec l'indice de suffixe *dernier*.
* Le suffixe DP est symétrique – nous stockons l'indice *dernier*, donc nous itérés à l'envers.

La réponse finale est le maximum sur toutes les paires de masques qui respectent la contrainte d'ordre (`pref[m1] < last[m2]`).

---

Solution complète (Python)

'`python
de taper l'importation Liste

Solution de classe:
def maxValue(self, nombres: List[int], k: int) -> Int:
n = len(nums)
MAX_MASK = 1 << 5 # 0..31
INF = n + 1 # marqueur impossible

# ---- préfixe dp : premier indice ----
pref = [[INF] * MAX_MASK pour _ dans la plage (k + 1)]
pref[0][0] = -1 # avant le premier élément

pour i, val dans l'énumération(nombres):
pour t dans la plage (min(k, i + 1), 0, -1):
pour masque de portée(MAX_MASK):
si pref[t - 1][masque] <= i - 1: # peut utiliser cet élément
nouvelle_masque = masque val
pref[t][new_mask] = min(pref[t][new_mask], i)

d'abord = [pref[k][m] pour m dans la plage (MAX_MASK)]

# ---- suffixe dp : dernier indice ----
suff = [[-INF] * MAX_MASK pour _ dans la plage (k + 1)]
suff[0]] = n # après le dernier élément

pour i dans la fourchette(n - 1, -1, -1):
val = nombres[i]
pour t dans la plage (min(k, n - i), 0, -1):
pour masque de portée(MAX_MASK):
si suff[t - 1][masque] >= i + 1:
nouvelle_masque = masque val
suff[t][new_mask] = max(suff[t][new_mask], i)

dernière = [suff[k][m] pour m dans la plage (MAX_MASK)]

- Oui. Scanner toutes les paires de masques ----
ans = 0
pour m1 dans la gamme (MAX_MASK):
si première[m1]] INF: continuer
pour m2 dans la gamme (MAX_MASK):
Si last[m2] == -INF: continuer
si première[m1] < dernière[m2]:
ans = max(ans, m1 ^ m2)
retour et
«» "

---

## Solution complète (C++)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int maxValue(vector<int> nums, int k) {
const int n = nombres.size();
const int MAX_MASK = 1 << 5; // 32 masques en raison des nombres[i] < 27
INF = n + 1; // indice impossible

/* préfixe DP : premier index pour OR==masque avec éléments t */
vecteur <array<int, 32>> pref(k + 1);
pour (int t = 0; t <= k; ++t) pref[t].fill(INF);
pref[0][0] = -1; // 0 éléments avant le tableau

pour (int i = 0; i < n; ++i) {
Int val = nombres[i];
pour (int t = min(k, i + 1); t >= 1; --t) {
pour (int mask = 0; masque < MAX_MASK; ++ mask) {
si (pref[t-1][masque] <= i-1) { // peut choisir cet élément
int newMask = masque val;
pref[t][newMask] = min(pref[t][newMask], i);
}
}
}
}
vecteur<int> premier(MAX_MASK, INF);
pour (int mask = 0; masque < MAX_MASK; ++ mask) d'abord[mask] = pref[k][mask];

/* suffixe DP : dernier index pour OR==masque avec éléments t */
vecteur<array<int, 32>> suff(k + 1);
pour (int t = 0; t <= k; ++t) suff[t].fill(-INF);
suff[0][0] = n; // 0 éléments après le tableau

pour (int i = n - 1; i >= 0; --i) {
Int val = nombres[i];
pour (int t = min(k, n - i); t >= 1; --t) {
pour (int mask = 0; masque < MAX_MASK; ++ mask) {
si (suff[t-1][masque] >= i + 1) {
int newMask = masque val;
suff[t][newMask] = max(suff[t][newMask], i);
}
}
}
}
vecteur<int> dernier(MAX_MASK, -INF);
pour (int mask = 0; masque < MAX_MASK; ++mask) last[mask] = suff[k][mask];

/* Scanner toutes les paires de masques pour trouver le meilleur XOR */
Int ans = 0;
pour (int m1 = 0; m1 < MAX_MASK; ++m1) {
si (premier [m1] == INF) continuer;
pour (int m2 = 0; m2 < MAX_MASK; ++m2) {
Si (dernier [m2] == -INF) continuer;
si (premier[m1] < dernier[m2)) ans = max(ans, m1 ^ m2);
}
}
le retour des an;
}
};
«» "

---

## Bonne, mauvaise et laid du modèle DP-Bitmask

Aspect Ce que nous avons appris Comment il montre la compétence
Il y a un problème.
**Bon**• **Tiny state space** (32 masques) – montre que vous pouvez réduire le problème par des contraintes.<br>• **PDD linéaire** sur les positions – facile à mettre en œuvre, à déboguer et à tester. Démontre l'optimisation de la vitesse* – transformer une idée exponentielle en routine linéaire. Autres
**Bad** La déclaration parle de *subséquences* (pas subséquences) – de nombreux codeurs naïfs vont essayer une combinaison de force brute d'indices (O(n2·k2)).<br>• La taille du masque OR est *pas évidente*; vous devez remarquer l'astuce < 27. Révèle *attention au détail* : attraper une contrainte cachée et la transformer en une énorme accélération. Autres
La gestion des tableaux DP 2 dimensions (`t × masque`) peut être maladroite dans les langues qui ne prennent pas en charge les grands tableaux multidimensionnels hors de la boîte.<br>• Certaines solutions gardent la table DP complète même si nous n'avons besoin que de la ligne «k»‐th. Afficher *conservabilité du code*: comment vous refactorez un DP dense en deux tableaux unidimensionnels (`first` & `last`) pour plus de clarté. Autres

---

## A emporter pour l'interview

* **Afficher votre état d'esprit sous contrainte** – identifier que `nums[i] < 27` signifie seulement 32 valeurs OU possibles.
* ** Expliquez le DP** – ce que signifie chaque dimension, pourquoi nous conservons les indices les plus rapides* par rapport aux indices les plus récents* et pourquoi le balayage final fournit la réponse optimale.
* **Parler de cas de bord** – préfixes/suffixes de longueur zéro, manipulation de l'infini négatif, et la façon dont le marqueur impossible est choisi.

Ce problème est un exemple parfait pour illustrer qu'une personne interrogée peut traduire une description combinatoire en un algorithme propre et efficace qui fonctionne en *temps linéaire*. La maîtrise du modèle DP‐Bitmask est un signal fort de la maturité algorithmique* et de l'intuition de résolution de problèmes* – des traits très prisés par les embaucheurs à la recherche d'ingénieurs logiciels de premier plan.