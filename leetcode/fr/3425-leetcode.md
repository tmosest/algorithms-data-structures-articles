---
titre: LeetCode 3425. Voie spéciale la plus longue -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
3425 – Voie spéciale la plus longue
*LeetCode – solution «Job‐Interview‐Ready» dans **Java**, **Python** & **C++***

---

Pourquoi ce post va vous poser un appel d'entrevue de codage

Mot-clé Pourquoi ça compte
C'est-à-dire
**LeetCode Le problème exact que vous verrez sur votre prochain forum d'entrevue. Autres
**Pathe spécial le plus long**= Titre concis et digne de buzz que recherchent les recruteurs. Autres
**Tree DP**=Les signaux vous permettent de résoudre des problèmes de théorie graphique avec la programmation dynamique. Autres
**Fenêtre coulissante C'est un tour intelligent et linéaire qui impressionne les intervieweurs. Autres
Autres **Java / Python / C++**= Montre la polyvalence du langage – parfait pour les rôles -tech-stack-agnostic. Autres

> **TL;DR** – Construisez l'arbre, précalculez les distances de la racine, et lancez une première recherche *simple* de profondeur tout en maintenant une fenêtre coulissante sur le chemin root-to-node actuel. L'algorithme fonctionne en temps **O(n)** et en mémoire **O(n)**.

---

Récapitulation des problèmes

On vous donne un arbre non dirigé (raciné au nœud 0) avec des nœuds `n`.
«edges[i] = [ui, vi, leni]» décrit un bord non dirigé de poids "leni".
«nums[i]» est la valeur stockée dans le noeud `i`.

Un chemin spécial** est un chemin * vers le bas* (d'un noeud à l'un de ses descendants) où toutes les valeurs de nœuds sur le chemin sont distinctes.
La longueur d'un chemin est la somme des poids de bord; un seul noeud a la longueur 0.

**Retour** où
* `maxLength` – la plus grande longueur possible d'un sentier spécial,
* `minNodes` – les plus petits nœuds qui atteignent cette longueur (le chemin peut être un seul noeud).

> Contraintes
> * `1 ≤ n ≤ 5 × 104`
> * `1 ≤ nombres[i] ≤ 5 × 104`
> * `1 ≤ leni ≤ 106 "

---

Aperçu de l'approche

1. **Distance du nœud vers le noeud** – Précalculez la distance entre la racine (node 0) et chaque noeud.
2. **Fenêtre coulissante sur le chemin root-to-node** – Pendant le DFSing, gardez une pile du chemin root-to-node actuel.
3. **Dernier tableau d'occurrence** – `last[value]` se souvient du noeud le plus profond du chemin courant qui a la valeur donnée.
4. ** Pointeur de départ du vent** – Lorsque nous rencontrons une valeur répétée, déplacez la fenêtre de démarrage après l'événement précédent.
5. **Réponse à jour** – Pour chaque nœud visité, le segment `[démarrer ... courant]` est un chemin spécial valide. Calculez sa longueur et son nombre de nœuds, puis mettez à jour la réponse globale.

La clé est que la fenêtre *sliding* n'est jamais plus grande que la pile DFS actuelle, de sorte que chaque noeud est poussé et sauté exactement une fois → **temps linéaire**.

---

Détails de la mise en œuvre

Voici trois implémentations de référence : **Java**, **Python** et **C++**.
Tous partagent le même squelette algorithmique mais ne diffèrent que par syntaxe.

> **Conseil:**
> *Ne jamais utiliser de DFS de force brute de chaque noeud – ce serait "O(n2)" et TLE sur les 5 000 nœuds.

---

Mise en œuvre Java

"Java
Importation de java.util.*;

solution de classe {
Int[] le plus longSpecialPath(int[][] bords, int[] nombres) {
int n = longueur nums;
// Créer une liste d'adjacence
Liste <Liste<int[]>> g = nouvelle liste <>();
Int max Val = entier.MIN_VALUE;
pour (int i = 0; i < n; ++i) {
g.add(nouveau tableau<>());
maxVal = Math.max(maxVal, nombres[i]);
}
pour (int[] e : bords) {
g.get(e[0]).add(nouvelle int[]{e[1], e[2]});
g.get(e[1]).add(nouvelle int[]{e[0], e[2]});
}

// Distance de la racine (node 0) – nous avons besoin de cela pour calculer la longueur du chemin
int[] dist = nouvelle int[n];
dfsDist(0, -1, 0, g, dist);

// Dernier tableau d'occurrence pour les valeurs des nœuds
int[] dernière = nouvelle int[max Val + 1];
les tableaux.fill(dernier, -1);

// Stack qui tient le chemin de racine à noeud actuel
Liste<entier> chemin = nouvelle liste d'array<>();
int start = 0; // fin gauche de la fenêtre
int maxLen = 0; // meilleure longueur vue jusqu'à présent
minNodes = 1; // min pour cette longueur

// DFS qui exécute la fenêtre coulissante
dfsWindow(0, -1, 0, g, nombres, dist, last, path, start, maxLen, minNodes);

retour de nouveau int[]{maxLen, minNodes};
}

vide privé Dist(int v, int p, int d,
Liste<Liste<int[]>> g, int[] dist {
dist[v] = d;
pour (int[] e : g.get(v)) {
u = e[0];
si (u == p) continue;
dfsDist(u, v, d + e[1], g, dist);
}
}

vide privé Fenêtre(int v, int p, int profondeur,
Liste <Liste<int[]>> g, nombres int[], nombre int[]
int[] last, List<Integer> chemin,
début int, int maxLen, int minNodes) {
int curIdx = path.size(); // position nous sommes sur le point de pousser
int oldLast = last[nums[v]]; // rappelez-vous l'ancienne position de cette valeur
int oldStart = start; // rappelez-vous l'ancien pointeur de démarrage

// Déplacer la fenêtre de démarrage si cette valeur est déjà dans la fenêtre
if (oldLast != -1 && oldLast >= start) start = oldLast + 1;

// Pousser le nœud actuel et mettre à jour la dernière occurrence
le chemin.add(v);
last[nums[v]] = curIdx;

// Calculer la longueur de la fenêtre actuelle
int curLen = dist[v];
si (démarrer > 0) curLen -= dist[path.get(start)];

curNodes = curIdx - début + 1;
si (curLen > maxLen) {
maxLen = curLen;
minNodes = curNodes;
} sinon si (curLen) maxLen && curNodes < minNodes) {
minNodes = curNodes;
}

// Récursions sur les enfants
pour (int[] e : g.get(v)) {
u = e[0];
si (u == p) continue;
dfsWindow(u, v, profondeur + e[1], g, nombres, dist,
dernier, chemin, départ, maxLen, minNodes);
}

// Backtrack : restaurer l'état précédent
last[nums[v]] = oldDernier;
path.size() - 1);
début = ancien Démarrer;
}
}
«» "

**Pourquoi ça marche* *

* Le tableau `last` stocke le noeud **deepest** avec chaque valeur sur le chemin courant root‐to‐node.
* Lorsque nous rencontrons un duplicata, nous décalons la limite gauche de la fenêtre au-delà de l'événement précédent – c'est-à-dire l'astuce classique *sliding-window*.
* Parce que l'arbre n'est traversé qu'une seule fois et que chaque nœud est poussé/poussé exactement une fois, l'algorithme entier est linéaire.

---

Mise en œuvre de Python

'`python
importations
sys.setcursionlimit(200000) # sûr pour n = 5e4

Solution de classe:
plus longtemps Path spécial (soi, bords, nombres):
n = len(nums)

# Créer une liste d'adjacence
adj = [[] pour _ dans l'intervalle(n)]
pour u, v, w dans les bords:
(v, w))
adj[v].append(u, w))

# Distance précalculée de la racine
dist = [0] * n
def dfs_dist(v, p, d):
dist[v] = d
pour u, w dans adj[v]:
Si u != p:
dfs_dist(u, v, d + w)
dfs_dist(0, -1, 0)

max_len = 0
_nœuds min = 1

pile = [] # stocke les indices des nœuds de la racine courante→ chemin des nœuds
dernière = {} # valeur -> position la plus profonde dans la pile
start = 0 # fin gauche de la fenêtre coulissante

def dfs(v, p):
non local max_len, min_nodes, début

idx = len(stack) # profondeur du courant dans la pile
old_last = last.get(nums[v], -1)
old_start = début

# Déplacer la fenêtre de démarrage si le duplicata est trouvé dans la fenêtre actuelle
if old_last != -1 et old_last >= début:
début = old_last + 1

pile.append(v)
last[nums[v]] = idx

# Longueur de la fenêtre actuelle
cur_len = dist[v]
si début > 0:
cur_len -= dist[stack[start]]

cur_nodes = idx - début + 1
si cur_len > max_len:
max_len = cur_len
min_nodes = cur_nodes
elif cur_len == max_len et cur_nodes < min_nodes:
min_nodes = cur_nodes

# Récursez
pour u, _ dans adj[v]:
Si u != p:
dfs(u, v)

# Retour
Pile.pop()
si old_last == -1:
del last[nums[v]]
Sinon:
last[nums[v]] = old_last
start = old_start

dfs(0, -1)
retour [max_len, min_nodes]
«» "

---

Mise en œuvre du C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> le plus longSpecialPath(vector<vector<int>>& bords, vector<int>& nums) {
int n = nombres.size();

// Créer une liste d'adjacence
vecteur<vecteur<pair<int,int>>> adj(n);
= 0;
pour (auto& e : bords) {
u = e[0], v = e[1], w = e[2];
adj[u].push_back({v, w});
adj[v].push_back({u, w});
maxVal = max(maxVal, max(nums[u], nums[v]);
}

// Distance de la racine
vecteur<int> dist(n, 0);
fonction<vit(int,int,int)> dfsDist = [&](int v, int p, int d) {
dist[v] = d;
pour (auto [u, w] : adj[v])
si (u != p) dfsDist(u, v, d + w);
};
dfsDist(0, -1, 0);

vecteur<int> dernier(maxVal + 1, -1);
int maxLen = 0, minNodes = 1;
vectorielle<int> chemin; // pile racine à noeud
début int = 0;

fonction<vit(int,int)> dfsWin = [&](int v, int p) {
int idx = chemin.size();
Int oldLast = last[nums[v]];
int oldStart = début;

if (oldLast != -1 && oldLast >= start) start = oldLast + 1;

path.push_back(v);
last[nums[v]] = idx;

int curLen = dist[v];
si (démarrer > 0) curLen -= dist[path[start]];

Int curNodes = idx - démarrage + 1;
si (curLen > maxLen) { maxLen = curLen; minNodes = curNodes; }
sinon si (curLen) maxLen && curNodes < minNodes) minNodes = curNodes;

pour (auto [u, w] : adj[v]) si (u != p)
dfsWin(u, v);

// arrière-cours
last[nums[v]] = oldDernier;
chemin.pop_back();
début = ancien Démarrer;
};

dfsWin(0,1);
retour {maxLen, minNodes};
}
};
«» "

---

Résumé de la complexité

Heure de mise en œuvre Mémoire
- C'est quoi ?
Java **O(n)**
Python **O(n)**
* * * * * * * *

Comme chaque noeud n'est visité qu'une seule fois et que chaque bord est traité une seule fois, l'exécution est bien inférieure à 1 s, même pour la limite supérieure.

---

C'est vrai. Ce que les recruteurs remarqueront

* **Fenêtre coulissante linéaire** – un tour non évident qui coupe la complexité algorithmique.
* ** Flexibilité de la langue** – Même solution en trois langues principales → vous pouvez intégrer presque n'importe quelle équipe.
* **Pré-computation + DFS** – montre une compréhension des nuances de la traversée du graphique.

---

À emporter pour la prochaine interview

1. **Demander au sujet de l'enracinement des arbres** – Clarify que le terme « vers le bas » signifie d'un noeud à ses descendants.
2. **Exposer la précomputation** – C'est le moyen le plus rapide pour obtenir des longueurs de chemin à la volée.
3. **Afficher la logique de la fenêtre coulissante** – Parler à travers le tableau `last` et le pointeur `start`.
4. **Linéarité de l'image** – Chaque noeud est poussé/poncé exactement une fois, de sorte que vous pouvez gérer l'ensemble de contrainte confortablement.

Avec ces solutions de référence dans votre GitHub ou votre repo de codage personnel, vous allez entrer dans une interview avec confiance, prêt à écrire la réponse optimale sur le tableau blanc ou sur un ordinateur portable en quelques minutes.

Bonne chance – votre prochain appel au travail est juste un "print("Bonjour, monde!")` loin!

---

> **Suivez-moi** pour plus de solutions *fast-track* LeetCode, des articles de préparation d'entrevues et des informations sur la culture du codage.

---

Codage heureux ! (en milliers de dollars)