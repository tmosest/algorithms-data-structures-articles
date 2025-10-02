---
titre: LeetCode 2858. Le revirement minimal des bords permet d'atteindre chaque nœud -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Code Leet 2858 – Reversements de bord minimum pour que chaque nœud soit accessible
*Une solution O(n) adaptée à l'entrevue dans **Java**, **Python** et **C++***

---

Récapitulation des problèmes

Vous recevez un graphe **orienté** qui devient un arbre non dirigé si tous les bords sont traités comme bidirectionnels.
Pour chaque nœud `i` (0 ≤ i < n), vous devez calculer le nombre minimum d'inversions de bord* nécessaire pour qu'à partir de `i` vous puissiez atteindre **chaque autre noeud**.

«» "
n – nombre de nœuds (2 ≤ n ≤ 105)
bords – (n‐1) bords orientés : bords[i] = [ui, vi] (ui → vi)
«» "

Retourner un tableau `réponse` de longueur `n`, où `réponse[i]` est le renversement minimal de la racine `i`.

---

Pourquoi O(n2) est trop lent

Une solution naïve exécute un BFS/DFS à partir de chaque noeud et compte combien de bords doivent être retournés – ce qui est O(n) par racine → **O(n2)**, ce qui est impossible pour n = 105.

---

C'est vrai. Insight – *Re-rooting DP*

Traiter l'arbre non dirigé sous-jacent comme une liste ** d'adjacence** où chaque bord a deux directions possibles:

Coût si traversé comme original
- C'est pas vrai.
u → v

**Étape 1 – Choisissez n'importe quelle racine** (disons node 0) et lancez un DFS qui ajoute le coût de bord à la réponse.
Cela donne `cost[0]`, le nombre d'inversions nécessaires lorsque 0 est le début.

**Étape 2 – Re-root**
Lorsque nous déplaçons la racine de `u` à un noeud adjacent `v`, seule la direction du bord unique (u,v) change.
- Oui. Si la direction originale était `u → v` (coût 0), déplacer la racine vers `v` nous force à traverser `v → u` → +1 inversion.
- Oui. Si la direction originale était `v → u` (coût 1), déplacer la racine vers `v` supprime cette inversion → –1.

Ainsi

«» "
coût[v] = coût[u] + (1 – 2 * original Coût(u → v))
«» "

Un deuxième DFS propage `cost[]` à tous les nœuds en **O(n)** time.

L'algorithme entier est **O(n)** temps, **O(n)** espace – parfait pour les contraintes.

---

##### 4

Pourquoi ça compte Manipulation
- Oui.
Plusieurs enfants Aucune – la propriété de l'arbre garantit un seul chemin
Grande profondeur de récursion peut déborder dans les langues avec petite pile.
Graphique avec les bords de l'axe inverse seulement peut ne pas être nul Pas de manipulation spéciale – l'algorithme les compte correctement

---

C'est vrai. Mise en œuvre du code

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.

Autres **Taille de la pile**:
> - Java: la profondeur de récursion est au plus 105; utilisez `-Xss1M` si vous touchez le débordement de pile.
> - Python: `sys.setrecursionlimit(2_000_000) "
> - C++: l'optimisation de la récursion est généralement bonne; sinon, utilisez une pile explicite.

---

##### 5.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
// liste de proximité : chaque élément est (voix, coût)
graphique privé de la liste <int[]>[];
coût d'investissement privé;

int[] minEdgeReversals(int n, int[][] bords) {
construireGraph(n, bords);

coût = nouvelle int[n];
booléen[] visité = nouveau booléen[n];

// Étape 1: DSV du nœud 0 – calculer le coût[0]
dfs(0, visité);

// Étape 2: Reraciner pour propager les coûts
Arrays.fill (visité, faux);
reroot(0, visité);

les frais de retour;
}

construction privée videGraph(int n, int[][] bords) {
graphique = nouvelle liste[n];
pour (int i = 0; i < n; i++) graphe[i] = nouvelle liste de distribution<>();

pour (int[] e : bords) {
u = e[0], v = e[1];
graph[u].add(new int[]{v, 0}); // direction originale
graphic[v].add(new int[]{u, 1}); // sens inverse
}
}

// DFS qui retourne les inversions totales nécessaires pour le sous-arbre enraciné au nœud '
Int privé dfs(int node, booléen[] visité) {
visité[node] = vrai;
= 0;
pour (int[] nb : graphique[node]) {
int next = nb[0], costEdge = nb[1];
si (!visité[suivant]) {
+= coûtEdge + dfs(suivant, visité);
}
}
coût[node] = total;
le total des retours;
}

// Re-rooting DFS – mise à jour des coûts pour tous les nœuds
vide privé reroot(int node, booléen[] visité) {
visité[node] = vrai;
pour (int[] nb : graphique[node]) {
int next = nb[0], costEdge = nb[1];
si (!visité[suivant]) {
// coût[suivant] = coût[node] + 1 - 2 * coûtEdge
coût[suivant] = coût[node] + 1 - 2 * coûtEdge;
reroot(suivant, visité);
}
}
}
}
«» "

---

5.2 Python

'`python
importations
de collections importer par défautdict

Solution de classe:
def minEdgeReversals(self, n: int, bords: list[list[int]]) -> list[int]:
(en milliers)

# Créer une liste d'adjacence pondérée
graphique = par défautdict(list)
pour u, v dans les bords:
graphic[u].append(v, 0) # original
graph[v].append(u, 1)) # inverse

Coût = [0] * n
visité = [Faux] * n

def dfs(node: int) -> Int:
visité[noeud] = Vrai
Total = 0
pour nxt, w dans le graphique[node]:
si elle n'est pas visitée[nxt]:
Total += w + dfs(nxt)
coût[noeud] = total
retour total

def reroot(node: int):
visité[noeud] = Vrai
pour nxt, w dans le graphique[node]:
si elle n'est pas visitée[nxt]:
coût[nxt] = coût[node] + 1 - 2 * w
reroot(nxt)

dfs(0)
visité = [Faux] * n
reroot(0)
Frais de retour
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
vectorielle<vector<pair<int,int>>> g; // (voix, coût)
vecteur<int> coût;
public:
vector<int> minEdgeReversals(int n, vector<vector<int>& bords) {
construireGraph(n, bords);
l'attribution du coût(n, 0);
vecteur <char> vis(n, 0);

// Étape 1: DFS à partir de 0
dfs(0, vis);

// Étape 2: Réenracinement
fill(vis.begin(), vis.end(), 0);
reroot(0, vis);
les frais de retour;
}

particulier:
vide buildGraph(int n, vecteur const<vector<int>>& bords) {
g. attribuer(n, {});
pour (const auto& e : bords) {
u = e[0], v = e[1];
g[u].push_back({v, 0}); // original
g[v].push_back({u, 1}); // inverse
}
}

int dfs(int node, vecteur <char>& vis) {
vis[node] = 1;
la valeur de l'élément est égale à 0;
pour (auto [à, w] : g[node]) {
si (!vis[to]) {
tot += w + dfs(à, vis);
}
}
coût[node] = tot;
retour à domicile;
}

vide reroot(inint node, vector<char>& vis) {
vis[node] = 1;
pour (auto [à, w] : g[node]) {
si (!vis[to]) {
coût[à] = coût[node] + 1 - 2 * w;
reroot(vers, vis);
}
}
}
};
«» "

---

#### 6.

Conseil Pourquoi c'est important
-- -- -- -- --
**Expliquez l'astuce de re-rooting tôt**
Autres **Afficher explicitement le DFS à deux passes**
**Les limites de la pile de Mention**
**Utiliser une liste d'adjacence pondérée**

---

Comment le blog aide Toi

- **Structure claire** – Intro → Insight → Edge Cases → Code → Complexité.
La section Bon, Mauvais, Ugly** vous explique ce qui rend le problème difficile, pourquoi une approche naïve échoue, et comment le re-rooting le transforme en un DP propre.
- **Mots-clés de référence** (`leetcode`, `minimum ledge inversions`, `tree DP`, `re-rooting`, `interview question`) aident les recruteurs et les moteurs de recherche à trouver ce guide.
- **Les extraits de code du monde réel** en trois langues principales.

---

Les pensées finales

*LeetCode 2858* est un problème classique de poids d'arbre + bord dirigé.
La clé est de ** transformer une direction en un coût** et **propager la racine** avec un seul passage de l'arbre.
Ce O(n) DP est non seulement rapide mais aussi élégant – un candidat parfait pour les interviews de codage et le code de production.

Bonne chance pour votre prochaine interview, et le codage heureux!