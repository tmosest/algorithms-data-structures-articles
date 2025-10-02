---
Titre: LeetCode 1786. Nombre de chemins restreints du premier au dernier nœud -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1786. Nombre de voies réservées du premier au dernier nœud
*(Moyenne – LeetCode)*

> ** Résumé des problèmes* *
> On vous donne un graphique non dirigé, pondéré, connecté avec des nœuds *n* (1-basé).
> Pour chaque nœud *x* laisser `dist(x)` être la distance la plus courte entre *x* et *n*.
> Un sentier **restricté** du nœud 1 au nœud *n* est un sentier
> `[z0, z1, ..., zk]` où `z0 = 1`, `zk = n`, et pour chaque ` Les "
> `dist(zi) > dist(zi+1)` (la distance au dernier noeud diminue strictement).
> Compter tous ces chemins modulo `1 000 000 007`.

---

## -Le point de vue clé

1. **Short distances de la cible** – Exécuter Dijkstra du nœud *n*.
2. **Graph devient un DAG** – Pour chaque bord `(u,v)` seulement la direction `u → v` avec
`dist(u) > dist(v)` peut apparaître dans un chemin restreint.
3. **DP sur le DAG** – "ways[u] = ↓ ways[v]` sur toutes les bordures extérieures restreintes.
4. **Résultat** – «ways[1]».

L'algorithme s'exécute dans la mémoire `O(n+m) log n)` et `O(n+m)`.



---

Les solutions de code

Ci-dessous sont propres, implémentations idiomatiques dans **Java, Python, et C++**.

#### Java 17

"Java
Importation de java.util.*;

***
* Code Leet 1786 – Nombre de voies restreintes
*/
solution de classe publique {
int final statique privé MOD = 1_000_000_007;

Nombre d'intes publiquesPaths(int n, int[][] bords) {
// 1-
Liste<List<int[]>> g = nouvelle liste de distribution<>(n + 1);
pour (int i = 0; i <= n; i++) g.add(new ArrayList<>());
pour (int[] e : bords) {
u = e[0], v = e[1], w = e[2];
g.get(u).add(nouvelle int[]{v, w});
g.get(v).add(nouvelle int[]{u, w});
}

Dijkstra du noeud n
long[] dist = nouveau long[n + 1];
Arrays.fill(dist, Long.MAX_VALUE);
dist[n] = 0;
PrioritéQueue<long[]> pq = nouvelle prioritéQueue<>(Comparator.comparingLong(a -> a[1]));
pq.offre(nouvelle longue[]{n, 0});

pendant que (!pq.isEmpty()) {
long[] cur = pq.poll();
u = (int) cur[0];
long d = cur[1];
si (d != dist[u]) continue;
pour [int[] nb : g.get(u) {
int v = nb[0], w = nb[1];
long nd = d + w;
si (nd < dist[v]) {
dist[v] = nd;
pq.offre(nouvelle longue[]{v, nd});
}
}
}

Le PDD (mémorisé DFS) sur le DAG
long[] dp = nouveau long[n + 1];
les tableaux.fill(dp, -1);
retour (int) dfs(1, n, g, dist, dp);
}

privé long dfs(int u, int n, Liste<Liste<int[]>> g,
long[] dist, long[] dp) {
si u == n) retourner 1;
Si (dp[u] != -1) retour dp[u];
long ans = 0;
pour [int[] nb : g.get(u) {
int v = nb[0];
si (dist[u] > dist[v]) { // sens restreint
ans = (ans + dfs(v, n, g, dist, dp)) % MOD;
}
}
dp[u] = ans;
le retour des an;
}
}
«» "

Python 3

'`python
importation heapq
de taper l'importation Liste

MOD = 1 000 000 007

Solution de classe:
Def countRestricted Paths(self, n: int, bords: List[List[int]]) -> Int:
N° 1 Créer une liste d'adjacence
g = [[] pour _ dans la plage (n + 1)]
pour u, v, w dans les bords:
g[u].appendice(v, w))
g[v].appendice(u, w))

Dijkstra du nœud
dist = [float('inf')] * (n + 1)
dist[n] = 0
pq = [(0, n)] # (dist, noeud)
alors que pq:
d, u = heapq.heappop(pq)
Si d != dist[u]:
poursuivre
pour v, w in g[u]:
nd = d + w
si nd < dist[v]:
dist[v] = nd
(pq, (nd, v))

# 3: PDD sur le DAG (ordre topologique par dist)
ordre = trié(range(1, n + 1), clé=lambda x: dist[x])
dp = [0] * (n + 1)
dp[n] = 1
pour u dans l'ordre:
pour v, _ en g[u]:
si dist[u] > dist[v]:
dp[u] = (dp[u] + dp[v]) %

retour dp[1]
«» "

C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
static const int MOD = 1'000'000'007;
public:
nombre intPaths restreints(int n, vecteur<vecteur<int>>& bords) {
// Liste d'adjacence
vecteur<vector<pair<int,int>>> g(n + 1);
pour (auto &e : bords) {
u = e[0], v = e[1], w = e[2];
g[u].push_back({v, w});
g[v].push_back({u, w});
}

Dijkstra du noeud n
vecteur <long long> dist(n + 1, LLONG_MAX);
dist[n] = 0;
priority_queue<pair<long long,int>,
vecteur<pair<long long,int>>,
plus grande <pair<long long,int>>> pq;
les points suivants sont ajoutés:
pendant que (!pq.vide()) {
[d, u] = pq.top(); pq.pop();
si (d != dist[u]) continue;
pour (auto [v, w] : g[u]) {
long et long = d + w;
si (nd < dist[v]) {
dist[v] = nd;
pq.push({nd, v});
}
}
}

// 3/ PDD sur DAG (topologique par dist)
vecteur<int> ordre(n);
iota(order.degin(), order.end(), 1);
tri(order.begin(), order.end(),
[&](int a, int b){ retour dist[a] < dist[b]; });

vecteur<int> dp(n + 1, 0);
dp[n] = 1;
pour (int u : ordre) {
pour (auto [v, w] : g[u]) {
si (dist[u] > dist[v]) {
dp[u] = (dp[u] + dp[v]) % MOD;
}
}
}
retour dp[1];
}
};
«» "

Les trois solutions partagent la même complexité temporelle et spatiale :

- **Heure**: "O(n + m) log n)" (Dijkstra domine).
- **Espace**: `O(n + m)` (liste d'adjacence + tableau de distance + tableau DP).

---

Article du blog
*(SEO-optimized – Code Leet 1786, chemins restreints, graphique, interview) *

Titre
**Mastering LeetCode 1786: Nombre de chemins restreints – De la théorie des graphiques à la préparation de l'entrevue de préparation à l'emploi* *

Description de la méta
Apprendre la solution complète pour LeetCode 1786 – chemins restreints. Plongez dans Dijkstra, DP sur DAG, et le code Java, Python, C++. Boostez vos scores d'entrevue de codage et atterrissez votre travail de rêve. (en milliers de dollars)

Aperçu

Section du contenu
C'est pas vrai.
Autres 1. Aperçu du problème Autres
Autres 2. Intuition: Pourquoi Dijkstra + DP fonctionne. Autres
Autres 3. Direction des bords restreints. Afficher comment `dist(u) > dist(v)` transforme le graphique en DAG. Autres
Autres 4. Edge Cases & Pitfalls Autres
Autres 5. Algorithme Étape par étape avec diagrammes. Autres
Autres 6. Détails de la mise en œuvre. Autres
Autres 7. Analyse de complexité de Big-O, pourquoi il est optimal. Autres
Autres 8. Bon / mauvais / Quoi célébrer, quoi éviter, écueils du monde réel. Autres
Autres 9. Variantes d'entrevue communes -=Count les chemins avec une diminution non-stricte, -=Ajouter des poids de nœud, -=Version non pondérée. Autres
Autres 10. Comment utiliser dans les interviews. Autres
Autres 11. Ressources sur la pratique. Autres
Autres 12. Conclusion: Récapitulation, encouragement. Autres

Texte complet

---

C'est vrai. 1. Aperçu du problème

Le problème *Nombre de chemins restreints* se trouve à l'intersection de **algorithmes graphiques les plus courts** et **programmes dynamiques**.
Compte tenu d'un graphique non dirigé pondéré, un chemin est limité si la distance * vers la destination* diminue strictement à chaque étape.
Nous devons compter tous ces chemins du nœud 1 au nœud *n*.

Les contraintes sont généreuses:
- "2 ≤ n ≤ 20 000"
- `1 ≤ bords, longueur ≤ 200 000`
- "1 ≤ poids ≤ 106 "
- Oui. Le graphique est garanti pour être connecté.

Ces limites font **O(n+m) log n)** le spot sucré – tout est plus lent dans une entrevue.

---

C'est vrai. 2. Intuition

1. **Distance la plus courte de la cible** – Pensez à `dist(x)` comme une carte de hauteur du graphique. Node *n* est le niveau de la mer (distance 0).
2. **Les sentiers restreints doivent descendre** – Parce que `dist(zi) > dist(zi+1)` est nécessaire, chaque étape doit descendre strictement cette carte de hauteur.
3. **Edges point descente seulement** – Pour tout bord non dirigé `(u,v)`, seule la direction où le début est supérieur à la fin peut être utilisée.
4. **Le graphique devient un graphique acyclique dirigé (DAG)** – Aucun cycle ne peut exister parce que les hauteurs diminuent strictement.
5. ** Programmation dynamique sur le DAG** – Comptez les moyens d'atteindre l'évier depuis chaque nœud.

> **Traitement des clés**: *Distance courte-est → DAG → DP. *

---

C'est vrai. 3. Cas de bord et pièges communs

Pourquoi ça compte ?
C'est ce qu'on dit.
Dijkstra doit considérer le plus petit poids. Autres
Ils ne peuvent pas faire partie d'un chemin restreint. Autres
Le Dijkstra fonctionne toujours (les poids positifs sont OK) Autres
Autres Grande réponse – besoin de modulo Autres

---

C'est vrai. 4. Algorithme détaillé

1. **Run Dijkstra de noeud *n***
- Complexité: `O(n+m) log n) "
- Conservez `dist[1...n]` (long/64-bit pour éviter le débordement).

2. **Construire le DAG**
- Pour chaque bord non dirigé `(u,v,w)`:
*Si `dist[u] > dist[v]` → ajouter le bord dirigé `u → v`*
*Si `dist[v] > dist[u]` → ajouter le bord dirigé `v → u`*
*Si `dist[u] == dist[v]` → aucun bord dirigé (ne peut pas être utilisé). *

3. **DP sur le DAG**
- "ways[n] = 1".
- Procéder à des nœuds dans l ' ordre croissant de " dist "** (ordre topologique).
- Pour le nœud u:
`ways[u] = ↓ ways[v]` sur toutes les bordures extérieures restreintes.
- Retour "ways[1]".

Le DAG s'assure que lorsque nous traitons un nœud, tous les nœuds qu'il pointe ont déjà été traités.

---

C'est vrai. 5. Production— Code prêt (Java, Python, C++)

(Voir la section du code ci-dessus – copier-coller prêt, commenté et testé.)

> *Conseil pour les intervieweurs*: Afficher la logique d'abord, puis présenter le squelette de code. Il démontre à la fois la compréhension et une mise en œuvre propre.

---

C'est vrai. 6. Analyse de la complexité

Opération Coût
- C'est quoi ?
(n+m) log n)» Autres
Bâtiment DAG Autres
PDD traversant le territoire Autres
**Total**="O((n+m) log n)=" temps, "O(n+m)=" mémoire

Pour `n = 20 000` et `m = 200 000`, cela correspond confortablement aux limites de temps de LeetCode et à toute plateforme d'entretien.

---

C'est vrai. 7. Bon / mauvais / Méchant

Autres Qu'est-ce que c'est ?
- C'est quoi ?
• Séparation claire des préoccupations (Dijkstra + DP).<br>• Réutiliser la liste d'adjacence pour les deux passes.
**La profondeur de récursion peut atteindre les limites de récursion dans Python.
**Ugly**) • Certaines solutions tentent d'effectuer le DFS sans mémorisation sur le DAG, ce qui conduit à un temps exponentiel. • Éviter. Autres

---

C'est vrai. 8. Variations et extensions

Comment s'adapter
C'est quoi ?
*Trouver des chemins où `dist(zi) >= dist(zi+1)`*= Supprimer la stricte inégalité; toujours un DAG. Autres
*Le graphique est dirigé à l'origine. Autres
*Les poids peuvent être négatifs mais pas de cycles négatifs. *Dijkstra ne fonctionne plus. La complexité devient "O(nm)". Autres
*Large `n` jusqu`à 105, `m` jusqu`à 5·105*.

---

C'est vrai. 9. Stratégie d'entrevue

1. **Clarifier l'exigence de « réduction stricte »** – Certains candidats l'interprètent mal comme « non-augmentation ». (en milliers de dollars)
2. **Exposer la formation du DAG** – Visualiser la carte de hauteur.
3. **La complexité du temps de mention en amont** – Montrez que vous avez considéré les limites.
4. **Discuss mémoization vs topological DP** – Mettre en évidence les compromis.
5. **Parler de l'arithmétique modulaire** – De nombreux intervieweurs testent des erreurs de manipulation modulo.

---

10 ans. Ressources pratiques

- **LeetCode**: 1786 – chemins restreints, 1785 – Nombre de bonnes voies, 1237 – Sous-îles du comte.
- **Livres**: *Éléments des entrevues de programmation – Graphique* *Introduction à l'algorithme (CLRS) – chemins les plus courts et DP.
- **Cours**: **Graphique Algorithmes* sur Coursera, ** Programmation Dynamique* sur Udemy.
- ** Entretiens de masse**: LeetCode Gym, Interviewing.io, Prêle.

---

Dernier départ

> La meilleure façon d'aser un problème de graphe LeetCode est de le diviser en un sous-problème classique de chemin le plus court suivi d'un DP DAG.

Avec les extraits de code ci-dessus, vous pouvez :

- **Expliquer clairement la solution** lors d'une entrevue de codage en direct.
- ** Démontrer des connaissances prêtes à la production** en présentant un code propre et bien commenté en Java, Python ou C++.
- **Afficher la profondeur de la compréhension** en discutant des cas de pointe, de la complexité et des stratégies d'entrevue.

Bonne chance – vous êtes un pas de plus vers l'atterrissage de ce *travail de rêve*! C'est ce qu'il a dit.

---

Mots clés

`LeetCode 1786`, `Number of Restricted Paths`, `graph algorithme`, `Dijkstra`, `dynamique programmation`, `coding interview`, `software engineer interview`, `Java solution`, `Python solution`, `C++ solution`, `job interview preparation`, `algorithme analyse`.