---
titre: LeetCode 3604. Temps minimum pour atteindre la destination dans le graphique dirigé -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Aperçu de la solution

** Problème** –
Avec un graphique dirigé avec des nœuds `n` (0 ... n‐1).
Un bord est défini par `[u, v, début, fin]` et ne peut être traversé qu'à un temps entier "t" tel que "démarrage ≤ t ≤ fin".
Vous commencez par le noeud `0` au moment `0`.
Dans une unité de temps, vous pouvez soit attendre sur le nœud actuel ou traverser un bord sortant valide.
Trouvez le plus tôt possible pour atteindre le nœud `n‐1`.
Retour `-1` si c'est impossible.

---

Pourquoi Dijkstra Travaux Ici.

La principale observation est que le coût du déplacement d'un noeud `u` à l'époque `t` à un noeud `v` est **toujours exactement une unité de temps** (l'acte de traverser le bord).
La seule torsion supplémentaire est que vous pourriez devoir *attendre* jusqu'à ce que le bord soit disponible, c'est-à-dire jusqu'à `max(start, t)`.

Pour un nœud `u` que nous atteignons à l'époque `t`:

«» "
si t ≤ fin:
départ_temps = max(start, t) // attendre si nécessaire
arrive_time = départ_time + 1 // edge traversal prend 1 unité
«» "

L'heure d'arrivée est une fonction monotonique de l'heure de départ, donc l'heure d'arrivée à tout noeud est toujours meilleure que toute arrivée ultérieure.
Par conséquent, nous pouvons considérer le graphique comme un graphique pondéré où le poids de `u` à `v` dépend de l'heure actuelle, mais l'optimalité reste – nous avons juste besoin d'une **priority‐queue** (min-heap) qui étend toujours le nœud qui peut être atteint le plus tôt.

C'est exactement l'algorithme de Dijkstras avec une étape de relaxation dépendante du temps.

---

1.2 Étapes de l'algorithme

Description des étapes Autres
- C'est quoi ?
Autres 1=Construisez une liste d'adjacence `G[u]` contenant des tuples `(v, début, fin)` pour chaque bord sortant de `u`. Autres
"Dist[i]" – première heure d'arrivée connue au nœud "i". Initialisez tous les éléments à l ' exception de l ' expression < < dist > > [0] = 0 > .
Autres Utilisation d'un stockage min-heap `(temps, noeud)`. Push `(0, 0)` initialement. Autres
Autres Bien que le tas ne soit pas vide:
* Pop `(t, u)` – le noeud qui peut être atteint le plus tôt. Autres
* Si nous avons déjà un temps mieux connu pour `u` (`t > dist[u]`), sauter. Autres
* Si `u == n-1`, nous avons fini - retour `t`. Autres
* Pour chaque bord `(v, s, e)` de `u`: Autres
* Si `t > e` → le bord est déjà fermé, ignorez. Autres
* `départ = max(s, t)` (attendez si nécessaire). Autres
* `arrivée = départ + 1`. Autres
* Si `arrival < dist[v]`, mettez à jour `dist[v]` et appuyez `(arrival, v)` sur le tas. Autres
Autres Si la boucle se termine sans atteindre le nœud `n-1`, retourner `-1`. Autres

---

1.3 Esquisse de preuve de l'exactitude

Nous prouvons que l'algorithme renvoie l'heure d'arrivée minimale possible au nœud `n-1`.

**Lemme 1 (Monotonicité)* *
Si un nœud `u` peut être atteint au moment `t1` et `t1 < t2`, alors tout chemin commençant à `u` au moment `t1` ne peut pas arriver plus tard à une destination qu'un chemin commençant au moment `t2`.

*Proof.* La seule opération qui peut retarder les progrès est l'attente. Attendre plus ne peut que pousser l'heure de départ du prochain bord vers l'avant, jamais plus tôt. Par conséquent, la première arrivée à partir d'une heure de départ ultérieure est ≥ la première arrivée à partir d'une heure de départ antérieure. *

**Lemme 2 (Sous-structure optimale)* *
Laissez `π` être un chemin optimal du nœud `0` au noeud `n-1`. Le préfixe `π` jusqu'à tout noeud intermédiaire `u` est également un chemin optimal de `0` à `u`.

*Proof.* Supposons le contraire – qu'il existe un meilleur chemin vers 'u'. Concaténer ce meilleur préfixe avec le suffixe de `π` de `u` à `n-1` donnerait un meilleur chemin global, en contradiction avec l'optimalité de `π`.

** Théorème (exactitude algorithmique)* *
Lorsque l'algorithme extrait un noeud `u` de la file d'attente prioritaire avec le temps `t`, `t` équivaut au minimum possible temps d'arrivée à `u`.

*Proof par induction sur le nombre de nœuds extraits. *

- **Base**: Le premier noeud extrait est `(0,0)`. Clairement `0` est minimal pour le noeud `0`.
- **Étape d'introduction**: Supposons que la déclaration soit conservée pour tous les nœuds extraits avant « u ».
Supposons, pour contradiction, qu'il existe un chemin vers `u` qui arrive au moment `t' < t`.
Laissez `p` être le prédécesseur de `u` sur ce chemin optimal, arrivant à l'heure `t_p`.
Par hypothèse d'induction, `t_p` est minimal, donc quand `p` a été extrait, l'algorithme considéré comme le bord `p → u`.
Il aurait calculé `arrivée = max(start, t_p) + 1 ≤ t'` et inséré `(arrivée, u)` dans le tas.
Puisque `arrivée ≤ t' < t`, le tas aurait surgi `(arrivée, u)` avant `(t, u)`, en contradiction avec l'hypothèse que `(t,u)` aurait été extrait ensuite. *

Enfin, la première fois que l'algorithme extrait le noeud `n-1`, l'heure est l'heure d'arrivée optimale. Si le tas se vide avant cela, aucun chemin n'existe. *

---

1.4 Analyse de la complexité

Opération Heure Explication
C'est quoi ?
Construire une liste d'adjacence. **O(E)**
Chaque noeud peut être inséré plusieurs fois, mais au plus une fois par relaxation qui améliore le «dist». Chaque coût d'insertion/extraction **O(log V)**. Dans le pire des cas, nous traitons chaque bord une fois → **O(V+E) log V)** Autres
Temps total Autres
Espace **O(V + E)** pour liste d'adjacence, tableau de distance, tas et drapeaux visités. Autres

Avec des contraintes `n ≤ 10^5` et `edges.longueur ≤ 10^5`, cela correspond confortablement aux limites de temps et de mémoire.

---

- Oui. 2. Mise en œuvre du code

Voici des solutions concises, prêtes à la production dans **Java**, **Python** et **C++**.

> **Astuce** – Pour la pratique de l'entrevue, implémentez l'algorithme à partir de zéro (pas de raccourcis de bibliothèque) pour démontrer la compréhension.

### 2.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
public int minTime(int n, int[][] bords) {
// liste d'adjacence: noeud -> liste de {à, début, fin}
Liste<Liste<int[]>> graphique = nouvelle liste de répartition<>(n);
pour (int i = 0; i < n; ++i) graphe.add(new ArrayList<>());

pour (int[] e : bords) {
graphic.get(e[0]).add(new int[]{e[1], e[2], e[3]});
}

// les premières heures d'arrivée connues
long[] dist = nouveau long[n];
Arrays.fill(dist, Long.MAX_VALUE);
dist[0] = 0;

// min-pap de (temps, noeud)
PrioritéQueue<long[]> pq = nouvelle prioritéQueue<>(Comparator.comparingLong(a -> a[0]);
pq.offre(nouvelle longue[]{0, 0});

pendant que (!pq.isEmpty()) {
long[] cur = pq.poll();
longue t = cur[0];
u = (int) cur[1];

si (t != dist[u]) continue; //
si (u == n - 1) retour (int) t; // destination atteinte

pour (int[] e : graph.get(u)) {
int v = e[0], s = e[1], eEnd = e[2];
si (t > eEnd) continuer; // bord déjà fermé
long départ = Math.max(s, t);
longue arrivée = départ + 1;
i (arrivée < dist[v]) {
dist[v] = arrive;
pq.offre(nouvelle longue[]{arrivée, v});
}
}
}
retour -1; // inaccessible
}
}
«» "

---

2.2 Python

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
def minTime(self, n: int, bords: List[List[int]]) -> Int:
graphique = [[] pour _ dans l'intervalle(n)]
pour u, v, s, e dans les bords:
(v, s, e))

INF = 10**20
dist = [INF] * n
dist[0] = 0

pq = [(0, 0)] # (temps, noeud)
alors que pq:
t, u = heapq.heappop(pq)
Si t != dist[u]:
poursuivre
Si u == n - 1:
retour t

pour v, s, e_end dans graph[u]:
si t > e_end :
poursuivre
départ = max(s, t)
arrivée = départ + 1
si vous arrivez < dist[v]:
dist[v] = arrivée
heapq.heappush(pq, (arrivée, v))

retour -1
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minTime(int n, vecteur<vector<int>>& bords) {
vecteur<vector<array<int, 3>>> g(n);
pour (auto& e : bords) { // {à, début, fin}
g[e[0]].push_back({e[1], e[2], e[3]});
}

Const. longue INF = 4e18;
vecteur <long long> dist(n, INF);
dist[0] = 0;

utilisant P = paire <long long, int>; // (temps, noeud)
priorité_queue<P, vecteur<P>, plus grande<P>> pq;
pq.push({0, 0});

pendant que (!pq.vide()) {
[t, u] = pq.top(); pq.pop();
si (t != dist[u]) continue; // stale
si (u) n - 1) retourner (int)t;

pour (auto& e : g[u]) {
int v = e[0], s = e[1], eEnd = e[2];
si (t > eFin) continue;
long départ = max<long long>(s, t);
longue arrivée longue = départ + 1;
i (arrivée < dist[v]) {
dist[v] = arrive;
pq.push({arrivé, v});
}
}
}
retour -1;
}
};
«» "

---

- Oui. 3. Et si? – Cas de bord et pièges communs

Situation Comment l'algorithme le gère Pourquoi il est sûr
- C'est quoi ?
**Les bords sont multiples entre la même paire**. L'algorithme choisit l'arrivée possible la plus rapide. Les distances ne sont mises à jour que si elles sont strictement meilleures. Autres
Autres **Démarrage d'Edge > fin**. Pas de frais supplémentaires. Autres
Autres **Fenêtres de temps très volumineuses **= `dist` utilise `long` / `int64` si le débordement ne peut pas se produire. Même une fenêtre de `10^9` est bonne. Autres
Autres **Les entrées de tas distants**= La vérification `if t != dist[u]` les rejette. Il garantit l'exactitude et garde le tas petit. Autres
**En attente d'une longue période**"depart = max(start, t)" va pousser l'entrée de tas loin dans le futur – c'est exactement ce que signifie "en attente". L'algorithme est toujours linéaire dans le nombre de relaxations. Autres

---

- Oui. 4. Pourquoi certaines approches naïves échouent

1. **BFS seulement** – BFS suppose que chaque bord est toujours disponible.
La contrainte temporelle signifie que vous pouvez arriver à un nœud *later* via un chemin différent qui attend un meilleur bord.
BFS ne saurait jamais attendre, de sorte qu'il peut retourner une réponse *sur-optimiste* ou manquer un chemin possible.

2. **DP par heure (DP[t][u])** –
Si vous essayez de précalculer toutes les fois possibles jusqu'à la fin maximale, vous aurez besoin d'une table de taille `O(max_time * n)` qui est astronomiquement grande (`max_time` peut être `10^9`).
C'est pourquoi l'approche Dijkstra est la seule façon pratique.

---

- Oui. 5. Bonne à savoir – Pourquoi Ce problème est une question d'entrevue classique

Pourquoi ça compte ?
C'est-à-dire
**Arrêtes dépendantes du temps**= Affiche que vous pouvez étendre les algorithmes classiques pour gérer les contraintes dynamiques. Autres
Autres **Grande entrée (10^5)**.Vous forcez à utiliser des structures de données efficaces (`heap`, liste d'adjacence) au lieu de récursions ou matrices naïves. Autres
**Exacte entier traversal**=Conserve le problème discret – utile pour apprendre à gérer les problèmes de graphique. Autres
**Retour -1** Vous forcez à penser à *reachability* et aux entrées inexistantes. Autres

Un candidat fort :

* Expliquez l'argument de la monotonicité.
* Remettre en œuvre l'étape de relaxation.
* Discutez de la manipulation de l'étui (arêtes fermées, entrées d'étau).
* Être capable de prouver l'exactitude en quelques phrases.

---

- Oui. 6. Essais rapides

Vous pouvez copier-coller n'importe laquelle des trois implémentations dans l'éditeur de LeetCodes et exécuter les tests suivants :

"Java
Int n = 4;
[]] bords = {
{0, 1, 0, 5},
{1, 3, 4, 6},
{0, 2, 4},
{2, 3, 5, 7}
};
affirme la nouvelle solution().minTime(n, bords) == 5; // Réponse attendue
«» "

'`python
sol = Solution()
affirme sol.minTime(4, [[0,1,0,5],[1,3,4,6],[0,2,2,4],[2,3,5,7]) 5
«» "

'`cpp
Solution s;
int ans = s.minTime(4, {{0,1,0,5},{1,3,4,6},{0,2,2,4},{2,3,5,7}});
assertion(ans == 5);
«» "

---

- Oui. 7. Pensées finales

- **Pourquoi Dijkstra fonctionne toujours** – L'étape d'attente est monotonique, donc plus tôt est toujours mieux.
- **Pourquoi c'est une bonne question d'entrevue** – Il mélange la logique classique du trajet le plus court avec une subtile torsion dépendante du temps, exigeant une explication claire de la monotonicité et de la sous-structure optimale.
- ** Erreurs communes** – Oubliant d'utiliser `Long.MAX_VALUE` / `10**20` pour les valeurs initiales `dist`, ou poussant les entrées de tas stalles (qui peuvent augmenter considérablement le temps d'exécution).

Bon codage, et bonne chance pour votre prochaine interview!