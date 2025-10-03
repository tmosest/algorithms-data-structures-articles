---
titre: LeetCode 2277. Le nœud le plus proche du sentier en arbre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Solutions de code
Voici des implémentations propres et prêtes à la production du **LeetCode 2277 – Le nœud le plus fermé vers le sentier dans l'arbre** problème dans **Java, Python et C++**.
Chaque solution suit la même logique :

1. Construire une liste d'adjacence pour l'arbre.
2. Pour chaque requête
* Trouvez les nœuds sur le chemin de `start` à `end` en utilisant DFS.
* Effectuez un BFS de `node` jusqu'à ce que le premier noeud qui se trouve sur le chemin soit atteint.

La complexité est "O(n + q·n)" (worst-cas), ce qui est plus que assez rapide pour les contraintes (`n, q ≤ 1000").

---

### Java (DFS + BFS)

"Java
Importation de java.util.*;

solution de classe publique {
// liste d'adjacence
Liste privée<Liste<entier>> graphique;

public int[] le plus procheNode(int n, int[]] bords, int[][] requête) {
construireGraph(n, bords);
int[] res = nouvelle int[query.longueur];

pour (int i = 0; i < requête.longueur; i++) {
int start = requête[i][0];
int end = requête[i][1];
int noeud = requête[i][2];

Définir le chemin <integer> = nouveau HashSet<>();
findPath(début, fin, chemin, -1); // DFS
res[i] = le plus procheOnPath(node, chemin); // BFS
}
retour rés;
}

- Oui. Méthodes d'aide

// Créer une liste d'adjacence
construction privée videGraph(int n, int[][] bords) {
graphique = nouvelle liste de répartition<>();
pour (int i = 0; i < n; ++i) graphe.add(new ArrayList<>());
pour (int[] e : bords) {
graphic.get(e[0]).add(e[1]);
graphic.get(e[1]).add(e[0]);
}
}

// DFS qui enregistre tous les nœuds sur le chemin unique de 'cur' à 'target '
booléen privé findPath(int cur, int cible, Set<integer> chemin, int parent) {
chemin.add(cur);
si (cur == cible) retour vrai;

pour (int nb : graph.get(cur)) {
si (nb) le parent continue;
si (findPath(nb, cible, chemin, cur)) retourne vrai;
}
path.remove(cur); // backtrack – pas sur le chemin
retourner faux;
}

// BFS qui retourne le premier nœud sur 'path' rencontré depuis 'start' '
Int privé le plus proche OnPath(int commencer, Définir le chemin <entier> {
Queue<integer> q = nouveau ArrayDeque<>();
booléen[] vis = nouveau booléen[graph.size()];

q.add(démarrage);
vis[start] = vrai;

alors que (!q.isEmpty()) {
int v = q.poll();
si (chemin.contient(v)) retour v;

pour (int nb : graph.get(v)) {
si (!vis[nb]) {
vis[nb] = vrai;
q.add(nb);
}
}
}
retour -1; // ne devrait jamais arriver parce que l'arbre est connecté
}
}
«» "

---

### Python (DFS + BFS)

'`python
de collections import defaultdict, deque
de taper l'importation Liste

Solution de classe:
def le plus proche Noeud(même, n: int, bords: Liste[Liste[int]],
requête : Liste[List[int]]) -> Liste[int]:
# liste d'adjacence
graphique = par défautdict(list)
pour a, b dans les bords:
graphique[a].appendice(b)
graphique[b].appendice(a)

def dfs_path(départ: int, fin: int) -> jeu & #160;:
"""Retourne tous les nœuds sur le chemin unique du début à la fin."""
chemin = set()
pile = [(démarrer, -1)]
parent = {démarrer: -1}

pendant la pile:
noeud, par = pile.pop()
parent[node] = par
si le nœud est terminé:
# retour pour construire le chemin
cur = noeud
alors que cur != - 1 :
chemin.add(cur)
cur = parent[cur]
pause
pour nb dans le graphique[node]:
si nb == par:
poursuivre
(nb, noeud)
chemin de retour

def bfs_nearest(start: int, cible_set: set) -> Int:
"""Retourne le premier nœud dans target_set trouvé pendant BFS dès le début."""
q = deque([start])
visité = {début}
alors que q:
v = q.popleft()
if v dans le_set cible :
retour v
pour nb dans le graphique[v]:
si nb n'est pas visité:
visité.add(nb)
q.annexe(nb)
retour -1

ans = []
pour début, fin, noeud dans la requête:
path_nodes = dfs_path(début, fin)
ans.append(bfs_nearest(node, path_nodes))
retour et
«» "

---

### C++ (DFS + BFS)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> le plus procheNode(int n, vector<vector<int>>& bords,
vector<vector<int>>& requête) {
// créer une liste d'adjacence
vecteur<vector<int>> g(n);
pour (auto &e : bords) {
g[e[0]].push_back(e[1]);
g[e[1]].push_back(e[0]);
}

vecteur<int> rés;
pour (auto &q : requête) {
début int = q[0], fin = q[1], noeud = q[2];

unordered_set<int> chemin = findPath(g, début, fin);
res.push_back(nearestOnPath(g, noeud, chemin));
}
retour rés;
}

particulier:
// DFS qui recueille tous les nœuds sur le chemin de 'cur' à 'cible '
unordered_set<int> findPath(const vector<vector<int>>& g,
Int cur, cible int) {
chemin non ordonné_set<int>;
vecteur<int> parent(g.size(), -1);
Pile <int> m;
s.push(cur);
parent[cur] = -2; // marque telle que visitée

pendant que (!st.vide()) {
Int v = st.top(); st.pop();
si (v) la cible est brisée;
pour (int nb : g[v]) {
si (parent[nb]] -1) {
parent[nb] = v;
b) Poussées st.
}
}
}

// retour pour construire le chemin
pour (int v = cible; v != -2; v = parent[v])
path.insert(v);
le chemin de retour;
}

// BFS depuis 'start' jusqu'à ce qu'un nœud dans 'cible_set' soit trouvé
Int le plus proche OnPath(vecteur const<vector<int>>&g, démarrage int,
Const unordered_set<int>& cible_set) {
file d'attente <int> q;
vecteur<bool> vis(g.size(), faux);
q.push(démarrage);
vis[start] = vrai;

pendant que (!q.vide()) {
l'entrée v = q.front(); q.pop();
si (target_set.count(v)) retourne v;
pour (int nb : g[v]) {
si (!vis[nb]) {
vis[nb] = vrai;
q.push(nb);
}
}
}
retour -1; // jamais atteint parce que l'arbre est connecté
}
};
«» "

---

Article du blog
### Les bons, les mauvais, et le lamentable de résoudre le LeetCode 2277
C'est vrai. *Le nœud le plus près du sentier dans l'arbre – De la tempête à la production‐ Code prêt*

---

C'est vrai. 1. Récapitulation des problèmes
> **LeetCode 2277 – Le nœud le plus proche du sentier dans l'arbre* *
> Vu un arbre avec des nœuds `n` (0-basé), répondez aux requêtes `m`. Chaque requête `[démarrer, terminer, noeud]` demande: * quel noeud sur le chemin de `start` à `end` est le plus proche de `node`? *

Les contraintes sont petites (`n, m ≤ 1000`), mais le problème teste votre capacité à combiner la traversée du graphique, l'extraction du chemin, et le calcul de la distance.

---

C'est vrai. 2. La bonne – l'intuition directe

1. ** Propriété de chemin unique**
Dans un arbre, il y a exactement un chemin simple entre deux nœuds. Cela signifie qu'une fois que nous connaissons ce chemin, tout ce dont nous avons besoin est le point le plus proche.

2. **Découplage des tâches**
* **Trouver le chemin** – Un DFS (ou BFS) qui s'arrête dès que la destination est atteinte.
* **Trouver le noeud le plus proche sur ce chemin** – Un BFS à partir de `node` qui s'arrête quand il atterrit sur n'importe quel noeud du chemin défini.

3. **Pourquoi ça marche**
* Le DFS visite chaque bord au plus deux fois → `O(n)`.
* Le BFS explore les nœuds jusqu'à ce que le premier match → pire cas `O(n)` à nouveau.
* Total par requête: `O(n)` → `O(n·m)` global, ce qui est acceptable pour les limites données.

4. **Simplicité du code**
L'algorithme est propre, lisible et facile à tester. Vous pouvez l'écrire en **Java**, **Python** ou **C++** avec une poignée de fonctions d'aide.

---

C'est vrai. 3. Les mauvaises – pièges communs

Pourquoi ça se brise
- C'est quoi ?
**En supposant que le premier noeud trouvé est le plus proche** , BFS sur un arbre non dirigé peut atteindre un noeud plus loin d'abord si pas prudent avec le calcul de la distance. Utilisez un tableau de distance ou arrêtez le BFS **exactement** sur le premier nœud de chemin. Autres
**Utiliser la récursion sans garde des parents** Passez l'index parent dans DFS/BFS ou gardez un tableau visité. Autres
Autres **En stockant le chemin comme une liste et en effectuant des scans linéaires** → frais généraux supplémentaires. Enregistrer le chemin dans un `HashSet` / `unordered_set` pour les vérifications d'adhésion O(1). Autres
**Ignorer la garantie de chemin unique** Faites confiance à la propriété de l'arbre; vous n'avez jamais besoin de Dijkstra. Autres

---

C'est vrai. 4. L'indulgence – Quand les cas de bord ont mal

1. ** Grande profondeur (arbre cousu)* *
La profondeur de récursion DFS peut atteindre 1000, ce qui est très bien dans la plupart des langues, mais peut causer un débordement de pile dans certains environnements d'entrevue.
*Solution :* Utilisez une pile explicite (DFS implicite) ou augmentez les limites de récursion en Python.

2. **Demandes en double**
La mise en œuvre naïve recalcule le même chemin pour le même `[départ, fin]`.
*Solution:* Cache path set par paire `(start, fin)` si vous anticipez de nombreuses répétitions.

3. **Ordre de visite incorrect**
Si BFS de `node` n'est pas ordonné de niveau, vous pouvez retourner un noeud de distance non minimal.
*Solution:* Utilisez une file d'attente (`deque` dans Python, `std::queue` dans C++) – elle garantit l'ordre des niveaux.

---

C'est vrai. 5. Coup d'oeil sur la complexité

Opération Complexe Remarques
C'est quoi, ça ?
Construire le graphique Une seule passe sur les « bords ». Autres
DFS par requête Visite de chaque bord une fois (sortie précoce). Autres
BFS par requête Arrête au premier match. Autres
Total **'O(n · m)'**' ≤ 1 000 000 opérations dans le pire des cas – trivial pour les CPU modernes. Autres

Mémoire : `O(n)` pour la liste d'adjacence et quelques tableaux auxiliaires par requête.

---

C'est vrai. 6. Faits saillants de la mise en œuvre

* **Java** – Utilise `List<List<Integer>>` pour la liste d'adjacence et un tableau booléen pour les nœuds visités.
* **Python** – Utilise `defaultdict(list)` pour l'adjacence, `deque` pour BFS, et une pile manuelle pour DFS.
* **C++** – Utilise `vector<vector<int>>`, `unordered_set` et `queue`.

Les trois versions exposent la même structure : build → find path → BFS pour le nœud le plus proche.

---

C'est vrai. 7. Comment faire face à cette question dans une entrevue

1. **Demander des précisions**
* Est-ce que `start`, `end` et `node` garantis pour être distincts? (en milliers de dollars)
* Est-il acceptable de faire `O(n)` par requête? (en milliers de dollars)

2. **Afficher la stratégie découplée* *
Esquisse l'idée sur le papier : "FDS" pour obtenir le chemin, BFS pour trouver la première intersection. (en milliers de dollars)
Mentionnez la propriété *unique chemin* en amont – elle démontre une compréhension profonde.

3. **Cas de bord des peines* *
* Arbres très profonds (chaîne).
* Interroge où `node` se trouve sur le chemin.
* Requêtes répétées (optimisation possible par mémoisation).

4. **Le commerce de l'espace-temps Arrêt**
* Si l'intervieweur pousse pour mieux que "O(n·m)", discutez de pré-calculer toutes les distances par paire ("O(n^2)") ou en utilisant LCA + levée binaire pour répondre dans `O(log n)` par requête.
* Pour les contraintes données, le simple DFS+BFS est l'étalon d'or : correct, durable et rapide.

5. **Tests**
* Construisez votre propre harnais de test avec des arbres aléatoires et des requêtes.
* Vérifiez que la réponse correspond à un vérificateur de force brute qui calcule explicitement les distances.

---

C'est vrai. 8. Dernier départ

> **En cas de doute, briser le problème en petites parties indépendantes. **
> Pour le LeetCode 2277, la garantie d'un seul sentier de l'arbre signifie que vous pouvez séparer en toute sécurité le chemin de finition du noeud le plus proche. (en milliers de dollars)
> Une solution DFS + BFS propre, écrite en **Java**, **Python** ou **C++**, passera tous les tests et impressionnera les intervieweurs avec sa clarté et sa justesse.

---

C'est vrai. 9. Mots clés du référencement

Mot-clé Pourquoi ça compte
C'est-à-dire
Terme de recherche de base
Le nœud le plus proche du sentier dans l'arbre
Autres Demandes d'arbres
Autres Solution DFS Java Langue + algorithme Autres
Solution Python BFS Langue + algorithme Autres
C++ code de l'interview Autres
Les algorithmes d'entretien d'emploi

Utilisez ces balises lors du partage de votre solution sur LinkedIn, Medium ou un blog personnel pour joindre les recruteurs et les autres personnes interrogées.

---

Ligne de fond
- **Bien**: La propriété de chemin unique de l'arbre rend le problème conceptuellement simple.
- **Bad**: Les erreurs en ordre de passage ou les vérifications visitées peuvent produire silencieusement de mauvaises réponses.
- **Ugly**: Ignorer les limites de profondeur ou de mise en cache peut causer des débordements de cheminée et TLE en plus grandes contraintes.

S'en tenir au modèle **DFS + BFS**, garder votre code propre, et vous allez résoudre LeetCode 2277 en un rien de temps – et vous serez prêt à présenter ce modèle exact dans une entrevue de codage!