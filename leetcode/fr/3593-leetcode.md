---
titre: LeetCode 3593. Augmentations minimales pour l'égalisation des chemins de feuilles -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

Code Leet #1525 – *Incréments mineurs pour égaliser les chemins de feuille*
**Solutions en Java, Python & C++ + A Deep‐ Plongez sur le blog pour recevoir votre entrevue**

> ** Tags du référencement**: LeetCode, Incréments minimums pour égaliser les chemins de feuilles, arbre DP, chemin root-to-leaf, algorithme, solution Java, solution Python, solution C++, prép d'entrevue, structures de données, entretien d'emploi, structures de données et algorithmes

---

- Oui. 1. Le problème (en anglais clair)

On vous donne un arbre avec des nœuds **`n`** (`0 ... n‐1`).
Chaque noeud `i` a un coût positif `cost[i]`.
Vous pouvez **augmenter le coût de n'importe quel noeud** de n'importe quel montant (l'augmentation est *permanente* pour ce noeud).

**Objectif** : Choisissez les nœuds *fewest* pour augmenter de telle sorte que la somme de la racine à la feuille soit la même.

> **Exemple**
> `coût = [2,1,3]`, bords = `[0,1],[0,2]` → réponse = **1** (nœud d'augmentation 1).

---

- Oui. 2. Principales perspectives

C'est bien, c'est mal.
C'est pas vrai.
**Les sommes de feuilles conduisent tout** – la cible est simplement la plus grande somme de feuilles. **Profondeur de récursion** – un DFS récursif naïf peut atteindre la limite de la pile sur un arbre dégénéré. Autres
**Incrément seulement l'enfant qui compte** – chaque sous-arbre d'enfant plus petit a besoin exactement d'un accroissement. C'est pas vrai. **Int vs Long** – les sommes peuvent dépasser les entiers 32 bits (max. 105 × 109 1014). Autres

Le cœur de la solution est un arbre post-commande DP** qui renvoie, pour chaque nœud, la somme maximale de feuilles dans son sous-arbre.
Au cours de la même promenade, nous comptons le nombre de sous-arbres enfants **plus court** que le maximum et avons donc besoin d'un accroissement.

---

- Oui. 3. L'algorithme (Bottom-Up DFS)

1. **Construisez une liste d'adjacence** – l'arbre n'est pas dirigé mais nous allons ignorer le parent pendant le DFS.
2. **FDS(node)**
* Si `node` est une feuille → retourner `cost[node]`.
* Sinon:
* Pour chaque enfant, calculer `childMax = DFS(child)`.
* Let `maxChild = max(childMax)` – c'est la somme *maximum* feuille sous `node`.
* Pour chaque enfant avec `childMax < maxChild` → **l`enfant une fois** (ajouter à la réponse).
* Retour `maxChild + cost[node]` comme la somme maximale des feuilles du sous-arbre actuel.
3. L'appel racine donne la réponse.

Parce que nous n'avons besoin d'ajouter qu'un seul incrément de nœud pour chaque enfant, le nombre total d'incréments est simplement la somme de ces nombres.

---

- Oui. 4. Analyse de la complexité

Aspect Calcul Raison
- C'est quoi ?
Temps **O(n)**= Chaque bord est visité deux fois (une fois à construire, une fois dans DFS). Autres
Mémoire **O(n)** Autres
Numerique **64-bit entiers**= Somme jusqu'à `n * 109 ↓ 1014`, convient à `long` / `int64`. Autres

---

- Oui. 5. Pièges communs

Piège
- Oui.
**Débordement de la pile** sur un arbre semblable à une ligne. Autres
**Comparer les montants des feuilles de façon incorrecte**=Comparer uniquement les montants des feuilles de *sous-arbre* (`childMax`) – `cost[node]` est commun à tous les enfants. Autres
**Utiliser `int` pour les sommes**= Passer à `long` / `int64` pour éviter les débordements. Autres
**Return 0 incréments – manipulés automatiquement. Autres

---

- Oui. 6. Code

Ci-dessous vous trouverez des solutions propres et idiomatiques pour **Java, Python et C++**.

---

##### 6.1 Java

"Java
Importation de java.util.*;

solution de classe {

long et privé; // compteur mondial

public int minAugmentation(int n, int[]] bords, int[] coût) {
// Créer une liste d'adjacence
Liste <entier>[] adj = nouvelle grille[n];
pour (int i = 0; i < n; ++i) adj[i] = nouvelle liste de distribution<>();
pour (int[] e : bords) {
adj[e[0]].add(e[1]);
adj[e[1]].add(e[0]);
}

ans = 0;
dfs(0, -1, adj, coût);
retour (int) ans; // réponse correspond à int
}

/** DFS post-commande.
* Renvoie la somme maximale de feuilles dans le sous-arbre enraciné au `node`. */
privé long dfs(int node, int parent, Liste<integer>[] adj, coût int) {
booléen estLeaf = vrai;
long maxChild = Long.MIN_VALUE;

pour (int enfant : adj[node]) {
si (enfant) le parent continue;
isLeaf = faux;
long childMax = dfs(enfant, noeud, adj, coût);
si (enfantMax > maxEnfant) maxEnfant = enfantMax;
}

si (estLeaf) { // noeud foliaire
coût de retour[node];
}

// Compter les enfants qui sont strictement plus courts que le meilleur
pour (int enfant : adj[node]) {
si (enfant) le parent continue;
long childMax = dfs (enfant, noeud, adj, coût); // déjà calculé
si (childMax < maxChild) ans++; // incrément cet enfant
}

retour maxChild + coût[node];
}
}
«» "

> **Pourquoi la récursion fonctionne**: La pile Javas par défaut est suffisante pour ≤ 105 profondeur sur la plupart des juges en ligne; pour le code de production, vous pouvez remplacer la récursion par une pile explicite.

---

##### 6.2 Python

'`python
importations
sys.setrecursionlimite(1 << 25) # garde sûre pour les arbres profonds

Solution de classe:
def minAugmentation(même, n: int, bords: Liste[Liste[int]], coût: Liste[int]) -> Int:
adj = [[] pour _ dans l'intervalle(n)]
pour a, b dans les bords:
adj[a].appendice(b)
adj[b].append(a)

Self.ans = 0

def dfs(node: int, parent: int) -> Int:
is_leaf = Vrai
max_child = -1
pour nxt en adj[node]:
si nxt == parent: continuer
is_leaf = Faux
child_max = dfs(nxt, noeud)
si _max enfant > _enfant max :
max_child = enfant_max

i is_leaf: # noeud de feuille
coût de retour[node]

# Compter les enfants qui sont plus courts que les meilleurs
pour nxt en adj[node]:
si nxt == parent: continuer
si dfs_cache[nxt] < max_child:
égo.ans += 1

retour max_child + coût[node]

# Utilisez la mémoisation pour éviter de recalculer les valeurs enfant
dfs_cache = {}
def dfs(node, parent):
si noeud dans dfs_cache: retourner dfs_cache[node]
is_leaf = Vrai
max_child = -1
pour nxt en adj[node]:
si nxt == parent: continuer
is_leaf = Faux
child_max = dfs(nxt, noeud)
si _max enfant > _enfant max :
max_child = enfant_max
if is_leaf :
val = coût[noeud]
Sinon:
# Compter les incréments nécessaires
pour nxt en adj[node]:
si nxt == parent: continuer
si dfs_cache[nxt] < max_child:
égo.ans += 1
val = max_child + coût[noeud]
dfs_cache[node] = valeur
retour val

dfs(0, -1)
Revenez vous-même. ans
«» "

*La limite de récursion de Python est augmentée et la mémorisation (`dfs_cache`) garantit que chaque noeud est traité une fois. *

---

*### 6.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long an = 0;

long long dfs(int u, int p, const vector<vector<int>& adj, const vector<int>& cost) {
feuille de bool = true;
longueur longue meilleure = LLONG_MIN; // somme maximale des feuilles d'enfant

pour (int v : adj[u]) {
si v == p) se poursuit;
feuille = faux;
long enfant = dfs(v, u, adj, coût);
si (l'enfant > le meilleur) meilleur = enfant;
}

Si (feuille) coût de retour[u]; // noeud de feuille

// Compter les enfants qui sont strictement plus courts que le meilleur
pour (int v : adj[u]) {
si v == p) se poursuit;
si (dfs_cache[v] < best) ans++; // incrémenter cet enfant
}

le meilleur retour + coût[u];
}

nt minAugmentation(int n, vecteur<vector<int>>& bords, vecteur<int>& coût) {
vecteur<vecteur<int>> adj(n);
pour (auto &e : bords) {
adj[e[0]].push_back(e[1]);
adj[e[1]].push_back(e[0]);
}

// Utiliser un cache pour que chaque valeur enfant ne soit calculée qu'une fois
vecteur <long> cache(n, -1);
fonction<long long(int,int)> rec = [&](int u, int p)->long long {
si (cache[u] != -1) cache de retour[u];
feuille de bool = true;
longue longue meilleure = LLONG_MIN;

pour (int v : adj[u]) {
si v == p) se poursuit;
feuille = faux;
long enfant = rec(v, u);
si (l'enfant > le meilleur) meilleur = enfant;
}

si (feuille) {
cache[u] = coût[u];
} autre {
pour (int v : adj[u]) {
si v == p) se poursuit;
si (cache[v] < best) ++ans; // incrémenter cet enfant
}
cache[u] = meilleur + coût[u];
}
retour du cache[u];
};

les points suivants sont ajoutés:
retour static_cast<int>(ans); // réponse correspond à int
}
};
«» "

---

- Oui. 7. Enveloppage

* La somme cible est **la plus grande somme de feuilles** – pas d'estimations.
* Un seul accroissement par enfant plus court** suffit.
* Le DFS ascendant donne à la fois la cible et la réponse en un seul balayage.

Grâce à ces trois solutions polies et à la panne **-Good-Bad-Ugly.**, vous êtes prêt à :

* Soumettre une réponse rapide et efficace sur LeetCode ou toute plateforme de codage. *
* Expliquez l'intuition rapidement dans une vraie interview et regardez l'intervieweur hoche la tête. *

Bonne chance – vous avez ça! C'est ce qu'il a dit