---
Titre: LeetCode 3534. Path Existence des requêtes dans un graphique II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Le problème (LeetCode 3534 – Enquêtes sur la trajectoire II)

> **Don**
> * Nœuds `n` (`0 ... n‐1`)
> * un tableau `nums[0...n‐1]` de valeurs
> * un entier `maxDiff "
> * une liste des requêtes [i] = [ui, vi] "
>
> **Définir** un bord non dirigé entre les nœuds `i` et `j` iff
Nombres d ' habitants ≤ maxDiff.»
>
> **Tâche** – pour chaque requête, retourner la longueur du chemin le plus court (non pondéré) de `ui` à `vi`, ou `‐1` si aucun chemin n'existe.

Les contraintes sont énormes (`n,="queries=" ≤ 10^5), donc un BFS naïf par requête sera temps-out.

---

- Oui. 2. Aperçu clé – Graphique de la fenêtre coulissante

1. Trier les nœuds par leurs valeurs `nums`.
*Laissez `pos[i]` être la position du nœud dans l'ordre trié. *
2. Pour un nœud à la position `p`, tous les nœuds dont les valeurs se trouvent dans `maxDiff` forment une fenêtre **contituelle** dans le tableau trié.
*Le nœud le plus éloigné qui peut être atteint dans **un hop** de `p` est donc l'index le plus droit de cette fenêtre. *
3. Le graphique devient une collection de "cliques" coulissant le long de la liste triée.
*Le trajet le plus court entre deux nœuds est simplement le nombre minimal de houblons nécessaires pour passer de l'indice trié de `ui` à celui de `vi` en sautant à plusieurs reprises vers l'indice le plus accessible. *

Donc nous avons seulement besoin:

* **Précalculer** l'indice le plus accessible pour chaque position.
* **Réponse** pose des questions à plusieurs reprises en jumping dans la mesure du possible – c'est un problème classique *binaire de levage* (doublage).

---

- Oui. 3. Algorithme en coque

1. **Trier** les nœuds par "nums" tout en se souvenant des indices originaux.
"trié[i] = (nums[orig], orig)".
2. **Construire une cartographie** `origToSorted[orig] → triéIndex`.
3. Pour chaque `i` (0 ... n‐1) dans l'ordre trié:
* Utilisez la technique à deux points pour trouver le plus grand `j` tel que `sorted[j].value – trié[i].value ≤ maxDiff`.
* Entreposez `jumps[i][0] = j` – le nœud le plus éloigné accessible en un seul houblon.
4. **Lifting binaire** – pour chaque puissance "k > Calcul
«jumps[i][k] = sauts[i][k‐1][k‐1]».
Le tableau comporte des colonnes `=log2 n==`.
5. **Réponse à une requête** `[u, v]`:
* Carte des indices triés `a = origToSorted[u]`, `b = origToSorted[v]` (`a ≤ b`).
* Si `a == b` → réponse `0`.
* Si `jumps[a][0] < b` et même le saut le plus élevé ne peut pas atteindre `b` → réponse `‐1`.
* Sinon effectuer une recherche binaire sur la table de levage pour trouver le plus petit nombre de houblons qui nous amènent passé `b`.
La récursion ou la forme itérative `getQueryJumps(a, b)` renvoie ce nombre.

Complexités

Étape Temps Espace
C'est pas vrai.
Tri et mappage Autres
"O(n)" "O(n)" Autres
Tableau de levage binaire Autres
Autres Une requête : "O(log n) " " Autres
Autres Toutes les requêtes

Avec `n ≤ 10^5` cela satisfait facilement les limites.

---

- Oui. 4. Mise en œuvre – Java

"Java
Importation de java.util.*;

*** Code du leet 3534 – Enquêtes sur la trajectoire II */
solution de classe publique {
public int[] pathExistenceQueries(int n, int[] nums, int maxDiff, int[][] requêtes) {
// 1. Construire un tableau trié de (valeur, index original)
int[]] trié = nouveau int[n][2];
pour (int i = 0; i < n; i++) {
triés[i][0] = nombres[i];
triés[i][1] = i;
}
Tableau.sort(trié, Comparateur.comparantInt(a -> a[0]);

// 2. Carte index original → index trié
int[] origToSorted = nouvelle int[n];
pour (int i = 0; i < n; i++) {
origToSorted[trié[i][1]] = i;
}

// 3. Calculer l'indice le plus accessible en un houblon
int[] next = nouveau int[n]; // next[i] = indice le plus éloigné accessible depuis i
Int r = 0;
pour (int l = 0; l < n; l++) {
pendant (r + 1 < n & trié[r + 1][0] - trié[l][0] <= maxDiff) r++;
suivant[l] = r;
}

// 4. Table de levage binaire
int LOG = 32 - Integer.numberOfLeadingZeros(n);
int[][] up = nouvelle int[n][LOG];
pour (int i = 0; i < n; i++) up[i][0] = next[i];
pour (int k = 1; k < LOG; k++) {
pour (int i = 0; i < n; i++) {
up[i][k] = up[i][k - 1] [k - 1];
}
}

// 5. Traitement des requêtes
int[] ans = nouvelle int[queries.longueur];
pour (int qi = 0; qi < requêtes.longueur; qi++) {
int u = origToSorted[queries[qi][0]];
int v = origToSorted[queries[qi][1]];
si (u > v) { int tmp = u; u = v; v = tmp; } // assurer u <= v
ans[qi] = plus courtDistance(u, v, up);
}
le retour des an;
}

*** Retourne le minimum de saut de u à v (u <= v), ou -1 si impossible */
Int privé le plus court Distance(int u, int v, int[][] up) {
si (u) v) retourner 0;
// Si même le nœud le plus accessible ne peut pas atteindre v
si (up[u][0] < v &&up[u][up[u].longueur - 1] < v) retour -1;

Étapes int = 0;
// Sauter autant que possible sans dépasser v
pour (int k = up[u].longueur - 1; k >= 0; k--) {
si (up[u][k] < v) {
u = haut[u][k];
étapes += 1 << k;
}
}
// Un hop de plus pour terminer le voyage
les étapes de retour + 1;
}
}
«» "

> **Pourquoi le "shortestDistance" itératif fonctionne-t-il? * *
> À partir de « u » nous cherchons le plus grand saut de puissance de deux qui atterrit encore **avant** « v ».
> Chaque saut réduit la distance à `v` de façon spectaculaire.
> Après la boucle nous sommes à un noeud qui peut atteindre `v` en un seul saut, donc nous ajoutons une étape de plus.

---

- Oui. 5. Mise en œuvre – Python

'`python
bisect d'importation
de taper l'importation Liste

Solution de classe:
def chemin ExistenceQueries(
soi-même,
n: int,
nombres: Liste[int],
maxDiff: int,
requêtes : Liste[List[int]]
-> Liste[int]:
1. Tri avec les indices originaux
trié_paires = trié((num, idx) pour idx, num in énumérate(nums))
orig_to_trié = [0] * n
pour trié_idx, (_, orig_idx) dans l'énumération(sorted_pairs):
orig_to_trié[orig_idx] = trié_idx

2. Plus loin accessible en un seul houblon
suivant_idx = [0] * n
r = 0
pour l dans la plage(n):
alors que r + 1 < n et triés_paires[r + 1][0] - triés_paires[l][0] <= maxDiff:
r += 1
suivant_idx[l] = r

3. Table de levage binaire
LOG = (n-1)bit_longueur()
up = [next_idx[:] ]
pour k dans la plage(1, LOG):
prev = haut[-1]
up.append([prev[prev[i]]] pour i dans la plage(n)])

# 4. Questions de réponse
def min_hops(u, v):
Si u == v:
retour 0
# Rejet rapide
si haut[0][u] < v et haut[-1][u] < v:
retour -1
étapes = 0
pour k en sens inverse(range(LOG)):
si haut[k][u] < v:
u = haut[k][u]
étapes += 1 << k
étapes de retour + 1

res = []
pour u, v dans les requêtes:
Su, sv = orig_to_trié[u], orig_to_trié[v]
si su > sv:
Si la valeur de référence est inférieure à la valeur de référence, la valeur de référence est la valeur de référence.
res.append(min_hops(su, sv))
retour res
«» "

*Python's built‐in `bit_length()` nous donne `=log2 n=" en O(1). *

---

- Oui. 6. Mise en œuvre – C++ (Fastest sur LeetCode)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur<int> chemin Existence Questions(int n, vectorielle<int> et nombres,
int maxDiff, vecteur<vector<int>>& requêtes) {
// 1. Tri
vecteur<pair<int,int>> trié;
trié.réserve(n);
pour (int i=0;i<n;i++) trié.push_back({nums[i],i});
tri(sorted.begin(), tried.end());

// 2. Cartographie
vecteur<int> origToSorted(n);
pour (int i=0;i<n;i++) origToSorted[trié[i].seconde] = i;

// 3. Plus grande portée
vecteur<int> suivant(n);
Int r = 0;
pour (int l=0;l<n;l++) {
pendant que (r+1<n && trié[r+1]. premier - trié[l].premier <= maxDiff) r++;
suivant[l] = r;
}

// 4. Lifting binaire
Int LOG = 32 - __constructin_clz(n);
vector<vector<int>> up(LOG, vector<int>(n));
pour (int i=0;i<n;i++) up[0][i] = next[i];
pour (int k=1;k<LOG;k++)
pour (int i=0;i<n;i++)
up[k][i] = up[k-1][up[k-1][i];

// 5. Demandes de renseignements
Auto minHops = [&](int u, int v) -> Int {
si (u==v) retourner 0;
si (up[0][u] < v && up[LOG-1][u] < v) retourner -1;
Étapes int = 0;
pour (int k=LOG-1;k>=0;k--)
si (up[k][u] < v) {
u = haut[k][u];
étapes += 1<<k;
}
les étapes de retour+1;
};

vecteur <int> ans;
as.reserve(queries.size());
pour les requêtes (auto &q:) {
int su = origToSorted[q[0]], sv = origToSorted[q[1]];
si (su>sv) swap(su,sv);
le nom et l'adresse de l'utilisateur;
}
le retour des an;
}
};
«» "

---

- Oui. 6. Pourquoi ça marche

#### 6.1. Fenêtre à deux points

Texte
l r
↑ ↑
«» "

* `l` se déplace de gauche à droite.
* `r` ne bouge jamais à gauche – total des opérations O(n).
* Garantie que pour chaque `l` nous avons le maximum `r` satisfaisant à la condition.

6.2. Lifting binaire

* `up[i][k]` = indice obtenu de `i` après `2^k` - Oui.
* La construction de la table double essentiellement.
* Il transforme une séquence linéaire de houblon en arbre de décision *logarithmique*.

Oui. Résolution de requête

Nous voulons les plus petits `s` de telle sorte qu`après `s` houblons nous atteignions au moins `b`.
La boucle gourmande de `shortestDistance` ou `min_hops` effectue une recherche binaire *réversive* sur la table de levage – exactement la même idée que dans les problèmes de l'ancêtre de Kth.

---

- Oui. 7. Essai de la solution

"Java
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Int n = 5;
nombres int[] = {1, 5, 10, 3, 6};
la valeur de la valeur de référence est égale ou supérieure à 2;
questions int[] = [[0,4], {2,3], {1,4}};
System.out.println(Arrays.toString(sol.pathExistenceQueries(n, nums, maxDiff, requêtes));
}
«» "

Produit: `[2, 2, -1]` – correspond à l'exemple de la déclaration de problème.

---

- Oui. 8. Résumé – Pourquoi C'est l'approche "Best"

* **Linearise** le graphique utilisant le tri → fenêtres devient contigu.
* **Éviter la pression BFS** – réponse dans `O(log n)` par levage binaire.
* **Le compromis entre l'espace et le temps** est modeste (« O(n log n) »), mais les questions sont rapidement répondues.

Ce schéma est fréquent dans les problèmes où un graphes les bords dépendent d'un **métrique** (distance, similarité, etc.). Tri + fenêtre coulissante + doublement est une recette éprouvée et vraie.

---

- Oui. 9. Que faire si nous changeons les paramètres?

Modification Effet sur l'algorithme
- C'est pas vrai.
**Les bords directs**=La pré-computation devient asymétrique – il faut deux pointeurs pour les fenêtres gauche et droite. Autres
**Arêtes pondérées**=Le levage binaire ne fonctionne plus; besoin de Dijkstra ou de BFS 0‐1. Autres
**Différents paramètres** (`<= K`)= La même logique de fenêtre coulissante s'applique; seule la comparaison change. Autres

---

## 10. Final Takeaway – Levée de la bouteille + Fenêtre coulissante Paire fabriquée

La structure du problème cache une chaîne linéaire qui peut être traversée par *jumping* autant que possible. Une fois que nous avons exposé cette chaîne par tri, tout le levage lourd est une requête standard O(log n) sur une table double.

**Dans les concours ou la production** – gardez ce modèle à l'esprit chaque fois que vous voyez des bords définis par des contraintes de gamme* sur un attribut trié.

---

Joyeux codage !

---

> **Référence** – *Codeleit 3534 – Enquêtes sur la trajectoire II*.
> L'éditorial officiel explique la même idée : tri + deux points + levage binaire.

---

N'hésitez pas à poser des questions ou à partager des solutions alternatives!