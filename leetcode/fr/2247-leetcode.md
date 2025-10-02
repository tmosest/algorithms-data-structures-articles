---
titre: LeetCode 2247. Coût maximum du voyage avec la route K - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Coût maximum du voyage avec K Highways – Les bons, les mauvais et les méchants
**LeetCode 2247 – dur* *

> **Mots clés**: LeetCode 2247, Coût maximum du voyage, K Highways, programmation dynamique, bitmask DP, DFS+memo, Java, Python, C++, problème d'entretien, algorithmes graphiques

---

Récapitulation des problèmes

On vous donne un graphique pondéré non dirigé avec les villes `n` (`0 ... n‐1`) et une liste de `autoroutes`.
Chaque route est `[u, v, w]` – une route bidirectionnelle qui coûte `w` à conduire.

Vous voulez faire un voyage que

* ** utilise exactement les autoroutes `k`** (c ' est-à-dire traverse les bords `k`),
* ** ne visite jamais une ville deux fois** (le sentier doit être simple),
* peut partir de n'importe quelle ville.

Retournez le montant total *maximum* que vous pouvez payer lors d'un tel voyage, ou `-1` si c'est impossible.

«» "
n ≤ 15
Voies publiques ≤ 50
k ≤ 50
«» "

Les contraintes vous donnent un indice: `n` est minuscule, donc un **bitmask** est un ajustement parfait.

---

- Oui. Le bon – Pourquoi un DP bitmask fonctionne

* ** Représentation de l ' État* *
* `mask` – un entier de 15 bits où le bit `i` est `1` si la ville `i` a déjà été visitée.
* `dernier` – la ville où se termine le chemin actuel.

`dp[masque][dernier]` = coût maximal d'un sentier simple qui visite exactement les villes de `masque` et se termine par `dernier`.

* **Initialisation* *
Chaque ville peut être un point de départ.
`dp[1 << i][i] = 0` pour tous `i`.

* **Transition**
D'un État `(masque, dernier)` nous pouvons aller dans n'importe quelle ville adjacente `next` qui est *not* dans `mask`:

«» "
newMask = masque
dp[newMask][next] = max(dp[newMask][next],
dp[masque][dernier] + coût(dernier, suivant)
«» "

* **Réponse**
Nous avons besoin d'un chemin avec **exactly `k` bords**, c'est-à-dire `k+1` villes visitées.
Ainsi, parmi tous les masques avec `popcount(mask) == k+1`, prendre la valeur maximale de `dp[mask][*]`.

* **Complexité**
*Etats* – `n * 2^n` ≤ 15 × 32 768 φ 0,5 M.
* Transitions* – chaque état s'étend à tout le plus `n-1` voisins, encore minuscule.

«» "
Durée de l'opération
Mémoire O(n · 2^n) (~ 2 Mo)
«» "

Les deux sont bien dans les limites pour les cas d'essai dur.

---

- Oui. Le mauvais – Pourquoi pas DFS + Memo ou Dijkstra?

1. ** FDS + Mémo**
* Nécessite une touche `mask`, donc vous finissez par stocker `dp[vertex][mask]` – essentiellement le même DP mais mis en œuvre dans un style récursif.
La profondeur de récursion peut être jusqu'à `k` (= 50) – pas de débordement de pile, mais la table de mémo est encore grande et les facteurs constants plus élevés. *

2. ** Recherche semblable à Dijkstra**
*Si vous traitez chaque état `(mask, last)` comme un nœud dans un graphe énorme et exécutez une file d'attente prioritaire, l'algorithme est correct mais surkill.
La file d'attente contiendra des milliers d'entrées et les frais généraux des opérations de tas dominent le temps de run. *

La ligne de fond : **Plain bitmask DP est à la fois plus simple et plus rapide**.

---

- Oui. L'horrible – Cas et pièges

Comment éviter
- C'est quoi ?
"k >= n" Vous ne pouvez pas visiter plus de `n-1` bords sans revisiter une ville. Revenir immédiatement `-1`. Autres
Duplicate roads: Non autorisé par l'énoncé de problème, mais s'il est présent, il pourrait briser le DP. Construire des listes d'adjacence *sans dédoublement ou tout simplement ignorer les duplicata. Autres
Autres L'utilisation de `int` est sûre (`k*100 <= 5000`), mais si vous modifiez les contraintes, utilisez `long`. Autres
Autres Mauvais compte de population de masques. k+1`. Autres

---

C'est pas vrai. Mise en œuvre des références

Voici des solutions propres et autonomes pour **Java, Python et C++**.
Chacun suit le PDD exact décrit ci-dessus.

> *Tous les codes supposent que l'entrée est déjà analysée en variables: `int n`, `int[][]routes`, `int k`.*

---

#### 5.1 Java 17

"Java
Importation de java.util.*;

solution de classe publique {
// liste d'adjacence: liste des voisins avec des poids
classe statique privée Edge {
final int à, w;
Edge(int to, int w) { this.to = to; this.w = w; }
}

Int maximum Coût(int n, int[], int k) {
si (k >= n) retourne -1; // impossible d'avoir un chemin simple de longueur k

// Créer un graphique
Liste <Liste<Edge>> g = nouvelle liste <>(n);
pour (int i = 0; i < n; i++) g.add(new ArrayList<>());
pour (int[] e : autoroutes) {
g.get(e[0]).add(nouveaux Edge(e[1], e[2]));
g.get(e[1]).add(nouveaux Edge(e[0], e[2]);
}

états int = 1 << n;
int[][] dp = nouvelle int[états][n];
pour (int[] ligne : dp) Arrays.fill(ligne, Integer.MIN_VALUE);

// partir de chaque ville
pour (int v = 0; v < n; v++) dp[1 << v][v] = 0;

// DP sur masques
pour (int masque = 1; masque < états; masque++) {
// nombre de villes visitées = popcount(mask)
Si (Integer.bitCount(masque) > k + 1) continuer; // nous n'avons besoin que de k+1
pour (int last = 0; last < n; last++) {
int curVal = dp[masque][dernier];
si (curVal) continue;
pour [Edge e : g.get(dernier)] {
int nxt = e.to;
si ((masque et (1 < < nxt)) != 0) continuer; // déjà visité
int newMask = masque (= 1 < nxt);
dp[newMask][nxt] = Math.max(dp[newMask][nxt], curVal + e.w);
}
}
}

int best = -1;
Int cible MaskBits = k + 1;
pour (int masque = 1; masque < états; masque++) {
si (Integer.bitCount(mask) != cibleMaskBits) continue;
pour (int v = 0; v < n; v++) {
best = Math.max(best, dp[mask][v]);
}
}
le meilleur retour;
}
}
«» "

---

#### 5.2 Python 3

'`python
importations
de collections importer par défautdict

def maximum Coût(n: int, autoroutes: liste[list[int]], k: int) -> Int:
si k >= n:
retour -1

# liste d'adjacence
g = [[] pour _ dans l ' intervalle n)]
pour u, v, w dans les autoroutes:
g[u].appendice(v, w))
g[v].appendice(u, w))

États = 1 << n
# dp[masque][v] = coût maximum pour atteindre v ayant visité 'masque '
dp = [[-1] * n pour _ dans l ' intervalle (états)]
pour v dans la plage(n):
dp[1 << v][v] = 0

pour masque à portée(1, états):
si bin(mask).count('1') > k + 1 :
poursuivre
pour le dernier rang(n):
cur = dp[masque][dernier]
Si cur == -1:
poursuivre
pour nxt, w en g[last]:
si masque & (1 << nxt):
poursuivre
nouveau_masque = masque
dp[new_mask][nxt] = max(dp[new_mask][nxt], cur + w)

meilleure = -1
cible = k + 1
pour masque à portée(états):
si bin(mask).count('1') != cible:
poursuivre
pour v dans la plage(n):
best = max(best, dp[mask][v])

le meilleur retour
«» "

---

C++ 17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

struct Edge {
à l'exclusion de:
Edge(int to, int w) : to(to), w(w) {}
};

Int maximum Coût(int n, vecteur<vector<int>>& routes, int k) {
si (k >= n) retourne -1;

// liste d'adjacence
vecteur<vecteur<Edge>> g(n);
pour (auto& e : autoroutes) {
g[e[0]].push_back(Edge(e[1], e[2]));
g[e[1]].push_back(Edge(e[0], e[2]));
}

états int = 1 << n;
vector<vector<int>> dp(states, vector<int>(n, INT_MIN));

// partir de chaque ville
pour (int v = 0; v < n; ++v) dp[1 << v] v] = 0;

pour (int masque = 1; masque < états; ++masque) {
si (_constructin_popcount(masque) > k + 1) poursuivre;
pour (int last = 0; last < n; ++last) {
int cur = dp[masque][dernier];
si (cur== INT_MIN) continue;
pour (auto &e : g[last]) {
int nxt = e.to;
si (masque et (1 < < nxt)) continuent;
int newMask = masque (= 1 < nxt);
dp[newMask][nxt] = max(dp[newMask][nxt], cur + e.w);
}
}
}

int best = -1;
cible int = k + 1;
pour (int masque = 1; masque < états; ++masque) {
si (_builtin_popcount(mask) != cible) continue;
pour (int v = 0; v < n; ++v)
best = max(best, dp[mask][v]);
}
le meilleur retour;
}
«» "

---

## 6-- Tester le code

'`python
♪ Essai d ' échantillon
si __nom__ == "__main__" :
n = 4
routes = [[0, 1, 5], [1, 2, 2], [2, 3, 3], [0, 2, 4]]
k = 2
print (maximum) Coût(n, routes, k)) # → 8
«» "

Le test ci-dessus correspond à un chemin `0 → 2 → 3` (coût 4 + 3 = 7) ou `1 → 0 → 2` (5 + 4 = 9) – le maximum est `9`.
Vous pouvez ajuster l'exemple pour voir l'algorithme en action.

---

C'est pas vrai. Pourquoi cette solution obtient-elle la réponse dans votre entrevue

* **Graph + DP + Bitmask** – modèles d'entrevue classiques que les recruteurs aiment.
* **Time & Memory** – répond aux contraintes de hard avec des couleurs volantes.
* **Clean Code** – pas de bibliothèques supplémentaires, juste une seule boucle sur `mask` et `dernier`.
* **Language-agnostique** – vous pouvez écrire la même idée en Java, Python ou C++ en une minute.

N'hésitez pas à coller les extraits dans votre IDE préféré, modifier l'analyse d'entrée, ou même ajouter un petit programme de pilote à lire à partir de `stdin`.

---

Liste de contrôle à emporter pour les entrevues

1. **Lisez attentivement la déclaration** – remarquez les bords *exactement* `k` et *pas de revisite*.
2. **Spot le petit `n`** – il indique à bitmask DP.
3. **Définir l'état du PDD** – "masque" + "dernier".
4. **Initialiser, transition et réponse** – comme indiqué.
5. **Boîtes à bord** (`k >= n`, routes vides, etc.).
6. ** Expliquez votre complexité** – les recruteurs aiment quand vous parlez de `O(n^2·2^n)' et d'utilisation de la mémoire.

Bonne chance, et profitez d'écraser LeetCode 2247! C'est ce qu'il a dit