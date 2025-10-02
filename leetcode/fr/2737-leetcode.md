---
titre: LeetCode 2737. Trouvez le nœud le plus rapproché -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Trouvez le noeud le plus marqué (Code de bord 2737) – Un guide complet
**Mots clés:** Trouver le nœud le plus rapproché, LeetCode 2737, Algorithme Dijkstra, chemin le plus court, graphe traversal, solution Java, solution Python, solution C++, codage d'entretien, entretien d'emploi, entretien de codage

---

Quel est le problème ?

> **Objectif:**
> Compte tenu d'un graphique pondéré ** dirigé** avec des nœuds `n` (`0 ... n‐1`) et une liste de bords `edges = [u, v, w]` (bord de `u` à `v` avec du poids `w`), un noeud de départ `s` et un tableau de noeuds **marqués**, retourner la distance **minimum** de `s` à tout noeud marqué.
> Si aucun noeud marqué n'est accessible, retourner `-1`.

Récapitulation des contraintes
Point Limites
- C'est quoi ?
2 – 500
"edges.longueur"
"Caisses [i][2]"
"marqué.longueur"
Autres Pas de boucles d'auto; des bords répétés possibles.
Autres Tous les poids sont positifs.

---

2. Pourquoi Dijkstra C'est l'ajustement naturel

* **Piste la plus courte source** – Nous avons besoin de la voie la plus courte **de `s`** à *any* noeud marqué.
* **Positive weights only** – L'algorithme de DijkstraS garantit une optimisation lorsque tous les poids de bord sont non négatifs.
* **Stop précoce** – On peut s'arrêter dès que l'on sort un nœud marqué de la file d'attente prioritaire – on est déjà au plus près.

---

- Oui. 3. Algorithme Aperçu général

1. **Construisez une liste d'adjacence** à partir de la liste des bords.
`adj[u]` → liste des paires `(v, w)`.
2. **Maintenir un minimum (en attente prioritaire)** de "(distance, nœud)".
3. **Gardez un tableau `dist[]`** (initialement `=) et un tableau `visité[]`.
4. **Push** `(0, s)` dans la file d'attente, définir `dist[s] = 0`.
5. Alors que la file d'attente n'est pas vide :
* Pop le plus petit noeud de distance `u`.
* Si `u` est déjà visité, sauter.
* Marquez `u` comme visité.
* **Si `u` est un nœud marqué → retourner `dist[u]`.**
* Relax tous les bords sortants `u → v`:
Texte
si dist[u] + w < dist[v]:
dist[v] = dist[u] + w
Pousser (dist[v], v)
«» "
6. Si la boucle se termine sans frapper un noeud marqué → retourner `-1`.

L'algorithme fonctionne dans **O(n + m) log n)** time et **O(n + m)** space (avec `m = bords.longueur`).

---

C'est pas vrai. 4. Le bien, le mal et le mal

Aspect du bien
- C'est quoi ?
**Sonorité algorithmique**=Dijkstra garantit une optimisation avec des poids positifs.=== Ne convient pas pour les poids négatifs – aurait besoin Bellman-Ford ou SPFA.==== Les bords répétés pourraient gonfler inutilement le tas, mais avec `m ≤ 104` il est négligeable. Autres
**Early exit** . . S'arrête dès que le noeud marqué le plus proche est réglé, en économisant du temps. . Nécessite une vérification minutieuse de visite – si omis vous pouvez retourner une distance sous-optimale. . Un tableau de buggy visité (par exemple, "dist" seulement) peut causer de mauvais résultats. Autres
Pour les graphes très denses, le tas peut se grossir. Autres

---

5. Mise en œuvre du code

Ci-dessous sont propres, des extraits de production prêts pour **Java**, **Python** et **C++**. Tous utilisent la même approche décrite ci-dessus.

> **Astuce:** Dans toutes les solutions, la sortie anticipée ('si marquéeSet.contient(node)') garantit que nous retournons toujours la distance minimale à tout noeud marqué.

#### 5.1 Java (Java 11+)

"Java
Importation de java.util.*;

solution de classe publique {
Int minimum public Distance(int n, Liste<Liste<entier>> bords, int s, int[] marqué) {
// 1. Jeu de nœuds marqués pour la recherche O(1)
Définir <Intégrer> marquéeSet = nouveau HashSet<>();
pour (int node : marquée) marquée Set.add(node);

// 2. Liste des dépendances
Liste<Liste<int[]>> adj = nouvelle liste de distribution<>();
pour (int i = 0; i < n; i++) adj.add(new ArrayList<>());
pour (Liste <entier> e : bords) {
u = e.get(0), v = e.get(1), w = e.get(2);
adj.get(u).add(new int[]{v, w});
}

// 3. Distances + visites
int[] dist = nouvelle int[n];
booléen[] visité = nouveau booléen[n];
Arrays.fill(dist, entier. MAX_VALUE;
dist[s] = 0;

// 4. La file d'attente prioritaire de la taille minimale
PrioritéQueue<int[]> pq = nouveau PrioritéQueue<>(Comparator.comparingInt(a -> a[0]);
pq.offre(nouvelle int[]{0, s});

// 5. Dijkstra avec sortie anticipée
pendant que (!pq.isEmpty()) {
int[] cur = pq.poll();
int d = cur[0], u = cur[1];
si (visité[u]) continue;
visité[u] = vrai;
si (markedSet.contient(u)) retour dist[u];
pour (int[] nb : adj.get(u)) {
int v = nb[0], w = nb[1];
si (dist[u] + w < dist[v]) {
dist[v] = dist[u] + w;
pq.offre(nouvelle int[]{dist[v], v});
}
}
}
retour -1; // aucun nœud marqué accessible
}
}
«» "

#### 5.2 Python 3

'`python
importation heapq
de taper l'importation Liste, Tuple

Solution de classe:
def minimum Distance (self, n: int, bords: List[List[int]],
s: int, marquée: Liste[int]) -> Int:
adj = [[] pour _ dans l'intervalle(n)]
pour u, v, w dans les bords:
(v, w))

marked_set = set(marqué)
dist = [float('inf')] * n
visité = [Faux] * n
dist[s] = 0
heap = [(0, s)]

pendant que le tas:
d, u = heapq.heappop(heap)
si visité[u]:
poursuivre
visité[u] = Vrai
si u dans la_set marquée:
retour dist[u]
pour v, w in adj[u]:
si dist[u] + w < dist[v]:
dist[v] = dist[u] + w
heapq.heappush(heap, (dist[v], v))
retour -1
«» "

Numéro 5.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int minimum Distance(int n, vecteur<vector<int>>& bords,
int s, vecteur <int>& marqué) {
// Créer une liste d'adjacence
vecteur<vecteur<pair<int,int>>> adj(n);
pour (auto& e : bords)
adj[e[0]].emplace_back(e[1], e[2]);

unordered_set<int>markSet(marked.begin(), balisé.end());

vecteur <long long> dist(n, LLONG_MAX);
vecteur<bool> visité(n, false);
dist[s] = 0;

utiliser P = paire <long long,int>;
priorité_queue<P, vecteur<P>, plus grande<P>> pq;
pq.emplace(0, s);

pendant que (!pq.vide()) {
[d, u] = pq.top(); pq.pop();
si (visité[u]) continue;
visité[u] = vrai;
si (markSet.count(u)) retourne dist[u];

pour (auto [v,w] : adj[u]) {
si (dist[u] + w < dist[v]) {
dist[v] = dist[u] + w;
pq.emplace(dist[v], v);
}
}
}
retour -1;
}
};
«» "

---

6. Analyse de la complexité

Métrique Temps Espace
- Oui.
**Best-cas** (noeud marqué est un voisin direct de `s`)
**Cas le plus défavorable** (aucun noeud marqué n'est accessible)
**Pratique** (sous réserve des contraintes)

---

- Oui. Tranche Liste de contrôle des cas

Qu'est-ce qu'il faut regarder
-- -- -- -- -- -- -- -- --
**Les bords sont multiples entre les mêmes nœuds**.Tous les bords sont détendus – les duplicatas sont fins; la taille du tas peut augmenter légèrement. Autres
**Le noeud de démarrage `s` est déjà marqué**L'algorithme va immédiatement pop `(0, s)` et retourner `0`. Autres
Autres **Pas de nœud visible**La file d'attente sera vide; retourner `-1`. Autres
**Poids importants (jusqu'à 106)**= Utiliser `long long` en C++ ou `long` en Java pour éviter les débordements. Autres
**Graph déconnecté** Autres

---

7. Variations et extensions

Démarche
- Oui.
**Tous les bords non dirigés**= Construire une liste d'adjacence dans les deux directions – Dijkstra s'applique toujours. Autres
**Poids négatifs autorisés**= Passer à **Bellman-Ford** ou **SPFA**; sortie anticipée possible mais plus lente. Autres
**Multiple source nœuds**= Exécutez Dijkstra de chaque source ou utilisation **multi-source Dijkstra** en insérant toutes les sources avec la distance 0 dans le tas. Autres
**Le graphique de pondération avec des bords de poids zéro** Autres
**Objectif : somme des distances à tous les nœuds marqués**= Après avoir réglé tous les nœuds, somme `dist[node]` pour tous les `node` dans un ensemble marqué. Autres

---

8. Pourquoi maîtriser ce problème aide votre recherche d'emploi

1. **Showcases graph–theoretic thought** – Les intervieweurs aiment vous voir appliquer le bon algorithme (Dijkstra vs Floyd-Warshall vs BFS).
2. **Fait ressortir l'optimisation des départs** – Indique que vous pouvez penser à la taille et aux performances.
3. ** Démontre un style de codage propre** – Les trois extraits de langue utilisent des structures de données idiomatiques concises (`PriorityQueue`, `heapq`, `std::priority_queue`).
4. **Versatilité** – Vous pouvez pivoter depuis Java → Python → C++ dans la même interview, prouvant l'agnosticisme du langage.
5. **Exemple de LeetCode réel** – 2737 apparaît sur l'ensemble de difficultés de "Graph" ; la résolution indique la disponibilité pour les problèmes de "Graph" dans les interviews de codage.

---

9. Dernier départ

2737. Trouver le nœud marqué le plus proche est un problème *classique* de chemin le plus court qui cartographie parfaitement l'algorithme de Dijkstras avec une sortie précoce. Maîtriser cette solution :

* Vous donne un modèle **réutilisable** pour toute question d'entrevue sur le trajet le plus court.
* Vous montre comment **optimiser** en vous arrêtant au premier nœud marqué.
* Construit la confiance dans la manipulation ** cas de pointe** comme des bords répétés, des cibles inaccessibles, et de gros poids.

La prochaine fois que vous avez touché un problème de LeetCode, rappelez-vous l'astuce de Dijkstra – c'est votre ticket pour nettoyer, efficace et le code de niveau d'entrevue.

---

Dix. Méta‐ Données (facultatif pour l'hébergement de blog)

html
<title>Trouver le nœud le plus marqué – LeetCode 2737.
<meta name="description" content="Solve LeetCode 2737: Trouvez le noeud le plus marqué avec Dijkstra. Lire les solutions Java, Python & C++, la complexité du temps et de l'espace, et les conseils d'entrevue.">
<meta name="keywords" content="Trouver le nœud le plus rapproché, LeetCode 2737, Algorithme Dijkstra, graphe traversal, solution Java, solution Python, solution C++, chemin le plus court, code d'entretien d'emploi">
«» "

Bon codage, et bonne chance d'obtenir cette interview technique!