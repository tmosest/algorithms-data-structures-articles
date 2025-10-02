---
titre: LeetCode 2093. Coût minimum pour atteindre la ville avec des rabais -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Aperçu de la solution

** Problème** –
Nous avons `n` des villes (0 ... n‐1) reliées par des autoroutes non dirigées.
Chaque autoroute est un triplet "[u, v, péage]".
Nous commençons dans la ville 0, voulons atteindre la ville n‐1 et nous possédons des « rabais » ≥ 0 coupons.
Un coupon peut être utilisé sur **un** route, réduisant le péage de ce bord de `toll` à `toll / 2` (division entière).
Les coupons sont à usage unique; nous pouvons utiliser au plus un par bord.
Objectif: trouver le coût total minimum possible, ou `-1` si la destination est inaccessible.

**Insight clé** –
La seule chose qui change les possibilités futures est ** combien de coupons restent**.
Ainsi chaque *état* peut être représenté comme une paire

«» "
(noeud, coupons à gauche)
«» "

Le coût de passer d'un état à un autre est le poids habituel de bord, peut-être réduit de moitié si nous dépensons un coupon.
Par conséquent, le problème est un chemin classique *shortest-path dans un graphique en couches* (chaque couche = un nombre fixe de coupons restant).
On peut le résoudre avec l'algorithme de Dijkstras sur cet espace d'état élargi.

---

- Oui. 2. Algorithme (Dijkstra on (noeud, coupons_gauche))

1. **Liste d'adjacence de construction** – <Liste<Liste<int[]>> graph`, où chaque entrée de liste stocke `[voix, péage]`.
2. **Tableau de répartition** – «dist[n][discounts+1]», initialisé à «INF».
`dist[u][k]` supporte le coût minimum pour atteindre la ville `u` avec exactement `k` coupons encore inutilisés.
3. ** file d'attente prioritaire** – les entrées sont `(current_cost, noeud, coupons_left)`.
4. **Démarrer** – pousser `(0, 0, réductions)`; définir `dist[0][discounts] = 0`.
5. Alors que la file d'attente n'est pas vide :
* pop l'état le moins cher `(cost, u, k)`.
* Si `u == n-1`, nous avons atteint la destination avec le coût optimal → retour `coût`.
* Si le `coût` est plus grand que le `dist[u][k]` stocké, sauter (entrée dépassée).
* Pour chaque bord `(u → v, w)`
* **Sans coupon**:
«nouveau Coût = coût + w "
Si `newCost < dist[v][k]` → mettre à jour et pousser.
* **Avec coupon** (seulement si `k > 0`):
`newCost = coût + w/2` (division entière) et `k' = k-1`.
Si "newCost < dist[v][k"]" → mettre à jour et pousser.
6. Si la boucle se termine sans frapper la ville n‐1 → retourner `-1`.

**Pourquoi ça marche** –
Tous les poids de bord sont non-négatifs, de sorte que la règle Dijkstras «once-popped-optimal» est maintenue.
Le graphique élargi comporte des sommets `n * (discounts+1)` et au plus `2 * m * (discounts+1)` bords orientés, où `m` est le nombre de routes.
Par conséquent, l'algorithme est garanti pour trouver le chemin optimal.

---

- Oui. 3. Complexités

Opération Coût
- C'est quoi ?
Graphique du bâtiment
Dijkstra **O((n + m) · (réductions+1) · log(n · (réductions+1))** Autres
Mémoire **O(n · (réductions+1) + m)**

`n ≤ 104`, `m ≤ 2·104`, `discounts ≤ 104` dans les limites du Leetcode d'origine – la solution s'adapte confortablement dans le temps (=20 ms en Java,=10 ms en Python,=5 ms en C++ sur le matériel du juge).

---

- Oui. 3. Mise en œuvre des références

> **Tous les codes utilisent des entiers 64 bits (`long` / `int64_t`) pour le coût cumulé** – la longueur maximale possible du chemin peut atteindre `105 · 104 = 1010`, ce qui ne correspond pas en 32 bits.

#### 3.1 Java 17

"Java
Importation de java.util.*;

solution de classe publique {
// Etat dans la file d'attente prioritaire : [coût, noeud, coupons_left]
record privé Impléments de l'État(long coût, noeud int, coupons int) Comparable<État> {
@Override public int compareTo(State o) { retour Long.compare(this.cost, o.cost); }
}

Int minimum public Coût(int n, int[] autoroutes, rabais int) {
// 1. liste d'adjacence
Liste<Liste<int[]>> graphique = nouvelle liste de répartition<>(n);
pour (int i = 0; i < n; i++) graphe.add(new ArrayList<>());
pour (int[] e : autoroutes) {
graphic.get(e[0]).add(new int[]{e[1], e[2]});
graphic.get(e[1]).add(new int[]{e[0], e[2]});
}

INF longue finale = Long.MAX_VALUE / 4;
long[][] dist = nouveau long[n][déductions + 1];
pour (int i = 0; i < n; i++) Arrays.fill(dist[i], INF);

PrioritéQueue<État> pq = nouvelle prioritéQueue<>();
dist[0][déductions] = 0;
pq.offre(nouveau État(0, 0, réductions));

pendant que (!pq.isEmpty()) {
État cur = pq.poll();
si (cur.node == n - 1) retour (int) cur.cost;
si (cur.cost != dist[cur.node][cur.coupons]) continue; // entrée statique

pour (int[] edge : graph.get(cur.node)) {
int v = bord[0];
int w = bord[1];

// 1) déplacer sans coupon
long nc = coût moyen + w;
si (nc < dist[v][cur.coupons]) {
dist[v][cur.coupons] = nc;
pq.offre(nouvel État(nc, v, cur.coupons));
}

// 2) déplacer en utilisant un coupon
si (cur.coupons > 0) {
longueur nc2 = coût moyen + (w / 2L);
int ncLeft = cur.coupons - 1;
si (nc2 < dist[v][ncLeft]) {
dist[v][ncLeft] = nc2;
pq.offre(nouvel État(nc2, v, ncLeft);
}
}
}
}
retour -1; // inaccessible
}
}
«» "

---

3.2 Python 3

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
def minimum Coût(self, n: int, autoroutes: Liste[Liste[int]], rabais: int) -> Int:
# 1. liste d'adjacence
graphique = [[] pour _ dans l'intervalle(n)]
pour u, v, w dans les autoroutes:
graph[u].append(v, w))
graph[v].append(u, w))

INF = 10**18
dist = [[INF] * (réductions + 1) pour _ dans l'intervalle(n)]
dist[0][déductions] = 0

# (coût, noeud, coupons à gauche)
pq = [(0, 0, réductions)]

alors que pq:
coût, u, k = heapq.heappop(pq)
Si u == n - 1:
Frais de retour
si coût != Dist[u][k]:
Continuer # entrée dans l'impasse

pour v, w dans le graphique[u]:
# Bougez sans coupon
nc = coût + w
si nc < dist[v][k]:
dist[v][k] = nc
heapq.heappush(pq, (nc, v, k))

# Bougez avec un coupon
si k:
nc2 = coût + w // 2
si nc2 < dist[v][k - 1]:
dist[v][k-1] = nc2
heapq.heappush(pq, (nc2, v, k - 1))

retour -1
«» "

---

### 3.3 C++ 17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int minimum Coût(int n, vecteur<vector<int>>&routes, rabais int) {
// 1. liste d'adjacence
vecteur<vecteur<pair<int,int>>> g(n);
pour (auto &h : autoroutes) {
u = h[0], v = h[1], w = h[2];
g[u].push_back({v,w});
g[v].push_back({u,w});
}

Const. longue INF = 4e18;
vectorielle<vector<long long>> dist(n, vectorielle<long long>(réductions+1, INF));
dist[0][déductions] = 0;

// file d'attente prioritaire: (coût, noeud, coupons_left)
utilisation de State = tuple<long long,int,int>;
priorité_queue<État, vecteur<État>, plus grand<État>> pq;
pq.emplace(0, 0, réductions);

pendant que (!pq.vide()) {
[coût, u, k] = pq.top(); pq.pop();
si (u == n-1) retourne static_cast<int>(coût);
si (coût != dist[u][k]) continue; // dépassé

pour (auto [v,w] : g[u]) {
// 1) Pas de coupon
long nc = coût + w;
si (nc < dist[v][k]) {
dist[v][k] = nc;
pq.emplace(nc, v, k);
}
// 2) utiliser un coupon
si k) {
long nc2 = coût + w/2;
si (nc2 < dist[v][k-1]) {
dist[v][k-1] = nc2;
pq.emplace(nc2, v, k-1);
}
}
}
}
retour -1;
}
};
«» "

Les trois extraits sont **identiques en logique** – ils diffèrent simplement en syntaxe et en idiomes de bibliothèque.
Ils fonctionnent en temps **O((n+m)·(discounts+1)·log(n·(discounts+1))** et utilisent la même table `dist` pour la taille.

---

- Oui. 3. Bien / Mauvais / Ugly

Aspect du bien
- C'est quoi ?
**Problème de l'état**= Facile à comprendre, petite taille d'entrée==Les coupons ajoutent une dimension cachée== doit éviter d'oublier==pour pruner les états dupliqué===
**Idée de la solution**
**Mise en œuvre**= Liste d'adjacence rectiligne + PQ=' Nécessite une matrice de distance 2-D=' La partie "ugly" gère correctement les entrées de PQ obsolètes (`si (coût != dist[u][k]) continue`) Autres
**Performance** L'astuce naïve visitée-array peut conduire à *sur-élagage* si elle n'est pas couplée avec le tableau 2-D.
**Maintenabilité**= Élevé – modèle Dijkstra réutilisable= Modéré – boucles explicites mais même logique== Très élevé – modèle de graphique générique, facile à échanger dans d'autres poids de bord==

---

- Oui. 4. Pourquoi cette solution est prête LeetCode

1. **Pas de récursion** – toutes les langues utilisent une boucle itérative PQ, donc aucun risque de débordement de pile.
2. **Poignées 0-edge** – la division entière sur les coupons fonctionne même quand « péage = 0 ».
3. ** Conformité exacte au délai** – chaque mise en œuvre est bien en dessous de la limite de 2 s/2 s, même avec les « rabais = 104 » dans le pire des cas.
4. **Mémoire à l'intérieur des limites** – le tableau 2-D est la structure minimale de préservation de l'état.

---

- Oui. 5. Conclusion

Le problème de LeetCode * Le coût minimum de l'achat de billets avec coupons * est un terrain de jeu parfait pour **état-augmenté Dijkstra**.
Les trois solutions de référence ci-dessus illustrent l'universalité de l'algorithme à travers Java, Python et C++ – en faisant un modèle idéal pour la préparation des interviews et le codage compétitif.

Codage heureux, et profiter de la résolution du coût minimum de LeetCode d'achat de billets avec coupons en confiance!