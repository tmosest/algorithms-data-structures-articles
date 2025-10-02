---
titre: LeetCode 2714. Trouvez le chemin le plus court avec K Hops -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Le problème en bref

> **LeetCode 2714 – - Trouver le chemin le plus court avec K Hops
> Vous recevez un graphique connecté, non dirigé, pondéré avec des sommets `n` (0-indexé).
> Chaque bord a un poids positif "w".
> Deux sommets distincts `s` et `d` sont fournis, et vous pouvez **zero-out au plus `k` bords** (c'est-à-dire changer leur poids à 0).
> Quel est le poids total minimum possible d'un chemin de `s` à `d` après que vous avez appliqué jusqu'à `k` sans houblon?

«» "
n <= 500
longueur <= 104
w <= 106
k <= n-1
«» "

L'entrée garantit que le graphique est connecté, qu'il n'a pas d'auto boucle et qu'il n'a pas de bords en double.

---

- Oui. 2. Pourquoi un simple Dijkstra n'a pas coupé

Si vous pouviez seulement **skip** bords mais **pas** les modifier, un Dijkstra normal trouverait le chemin le plus le plus lent.
Dans ce problème, vous pouvez *remplacer* le poids jusqu'à `k` bords avec `0`.
Vous devez décider *qui* bords à zéro dehors et *où* dans le chemin que vous faites - le choix est couplé avec le chemin lui-même.

Cela signifie que l'état de l'algorithme n'est plus juste le vertex, il doit aussi se rappeler combien de free hop vous avez déjà utilisé.
C'est un modèle classique de Dijkstra (ou Dijkstra) .

---

- Oui. 3. La solution optimale

Idée 3.1

Traiter chaque paire
«» "
(État) = (vertex, Hops usagés)
«» "
comme nœud dans un graphe virtuel plus grand**.
À partir d'un état `(u, h)` vous pouvez:

Actions Nouveau État Frais de montage
C'est pas vrai.
Bord transversal `(u, v, w)` **normalement**
* avec un houblon**

Dirigez la Dijkstra ordinaire sur ces états.
La première fois que vous pop un état dont le vertex est `d`, vous avez la réponse optimale, parce que Dijkstra=" première visite-à-destination=" propriété détient dans ce graphique élargi aussi bien.

3.2 Esquisse de preuve d'exactitude

1. **Tous les chemins possibles sont représentés** –
Chaque chemin dans le graphique original peut être cartographié sur un chemin dans le graphique élargi en décidant pour chaque bord s'il est utilisé avec un houblon ou non.
Le nombre de bords de houblon utilisés ne dépasse jamais `k` parce que nous ne sommes jamais passés à un état avec `h > k`.

2. **Optimalité préservée** –
L'algorithme de Dijkstras garantit que la première fois qu'un état est retiré de la file d'attente prioritaire, il a le coût cumulé minimum possible de la source.
Par conséquent, lorsque nous rencontrons d'abord un état avec vertex `d`, son coût est le minimum possible parmi *tous* chemins qui respectent la limite de houblon.

3. **Aucun chemin plus court n'existe** –
Supposons qu'il y ait un meilleur chemin vers "d". Il correspondrait à un état `(d, h')` avec un coût plus petit que Dijkstra aurait dû supprimer plus tôt, en contradiction avec la propriété algorithme.

D'où l'algorithme renvoie la distance la plus courte exacte.

3.3 Complexité

«» "
Nombre d'états : n * (k+1) (maximum 500 * 501 250k)
Transitions par état : degré(u) (γ n-1)
Total des bords du graphique virtuel : O((k+1) * m)
«» "

Dijkstra fonctionne dans
«» "
O( (n*(k+1) + (k+1)*m) log(n*(k+1))
«» "
Avec les limites données ceci est bien en dessous d'une seconde dans toutes les langues principales.

Espace: `O(n*(k+1))` pour la distance / les tableaux visités plus le graphique initial `O(m)`.

---

- Oui. 4. Mise en œuvre des références

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.
Tous les trois utilisent le même modèle de Dijkstra décrit ci-dessus.

---

### 4.1 Java (style LeetCode)

"Java
Importation de java.util.*;

***
* LeetCode 2714 – Trouver le chemin le plus court avec K Hops
*/
solution de classe publique {

- Oui. Aide graphique
liste privée<int[]>[] buildGraph(int n, int[][] bords) {
Liste<int[]>[] g = nouvelle liste de distribution[n];
pour (int i = 0; i < n; ++i) g[i] = nouvelle liste de distribution<>();
pour (int[] e : bords) {
u = e[0], v = e[1], w = e[2];
g[u].add(nouvelle int[]{v, w});
g[v].add(nouvelle int[]{u, w});
}
retour g;
}

- Oui. État de la file d ' attente prioritaire
la classe statique privée Comparable<État> {
int vertex, utilisé;
longue distance;

État(int vertex, int utilisé, long dist) {
ce.vertex = vertex;
ce.utilisé = utilisé;
ce.dist = dist;
}

@Override
comparaison publique Pour (indiquer autre) {
retour Long.comparer(ce.dist, autre.dist);
}
}

- Oui. Dijkstra principale -------- */
int public int le plus courtPathWithHops(int n, int[]] bords, int s, int d, int k) {
Liste<int[]>[] g = buildGraph(n, bords);

// distance[vertex][hopsutilisés]
long[][] dist = nouveau long[n][k + 1];
pour (long[] rang : dist) Arrays.fill(row, Long.MAX_VALUE);

PrioritéQueue<État> pq = nouvelle prioritéQueue<>();
dist[s][0] = 0;
pq.offre(nouveau(s, 0, 0));

pendant que (!pq.isEmpty()) {
État cur = pq.poll();

si (cur.vertex == d) retour (int) cur.dist; // première arrivée est optimale

si (cur.dist != dist[cur.vertex][cur.used]) continue; // dépassé

pour (int[] e : g[cur.vertex]) {
int nb = e[0];
int w = e[1];

// 1) traverser normalement
si (cur.dist + w < dist[nb][cur.used]) {
dist[nb][cur.utilisé] = cur.dist + w;
pq.offre(nouveau État(nb, cur.utilisé, dist[nb][cur.utilisé]);
}

// 2) utiliser un houblon (si nous avons encore du houblon)
si (cur. utilisé < k && cur.dist < dist[nb][cur. utilisé + 1]) {
dist[nb][cur.utilisée + 1] = cur.dist;
pq.offre(nouveau État(nb, cur.utilisé + 1, dist[nb][cur.utilisé + 1));
}
}
}

// graphique est garanti connecté, donc cette ligne n'a jamais atteint
retour -1;
}
}
«» "

---

4.2 Python 3 (style LeetCode)

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
def le plus court Le chemin avec les pièges(
self, n: int, bords: Liste[Liste[int]],
s: int, d: int, k: int
-> Int:
# construire une liste d'adjacence
graphique = [[] pour _ dans l'intervalle(n)]
pour u, v, w dans les bords:
graph[u].append(v, w))
graph[v].append(u, w))

INF = 10**18
dist = [[INF] * (k + 1) pour _ dans la plage (n)]
dist[s][0] = 0

# (dist, vertex, houblon utilisé)
pq = [(0, s, 0)]
alors que pq:
c, u, utilisé = heapq.heappop(pq)
si cur != dist[u][utilisé]:
Continuer # entrée dans l'impasse

Si u ==d:
retour cur # première visite est optimale

pour v, w dans le graphique[u]:
# traversée normale
si cur + w < dist[v][utilisé]:
dist[v][utilisé] = cur + w
heapq.heappush(pq, (dist[v][utilisé], v, utilisé))

# sauter (si autorisé)
si utilisé < k et cur < dist[v] [utilisé + 1]:
dist[v][utilisée + 1] = cur
heapq.heappush(pq, (cur, v, utilisé + 1))

retour -1
«» "

---

### 4.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
struct Edge { int to; int w; };
État de structure {
int v, utilisé; long dist;
opérateur de bool<(State const& o) const { return dist > o.dist; } // min-heap
};

dans la plus courte PathWithHops(int n, vector<vector<int>>& bords,
int s, int d, int k) {
vecteur<vecteur<Edge>> g(n);
pour (auto &e: bords) {
u = e[0], v = e[1], w = e[2];
g[u].push_back({v,w});
g[v].push_back({u,w});
}

Const. longue INF = 4e18;
vecteur<vector<long long>> dist(n, vecteur<long long>(k+1, INF));
priorité_queue<État> pq;

dist[s][0] = 0;
pq.push({s, 0, 0});

pendant que (!pq.vide()) {
État cur = pq.top(); pq.pop();
si (cur.v == d) retourner (int)cur.dist; // optimal lors de la première explosion

si (cur.dist != dist[cur.v][cur.used]) continue; // stale

pour (auto &e : g[cur.v]) {
int nb = e.to, w = e.w;

// traversée normale
si (cur.dist + w < dist[nb][cur.used]) {
dist[nb][cur.utilisé] = cur.dist + w;
pq.push({nb, cur.utilisé, dist[nb][cur.utilisé]});
}

// Houblon
si (cur. utilisé < k && cur.dist < dist[nb][cur. utilisé+1]) {
dist[nb][cur.used+1] = cur.dist;
pq.push({nb, cur.used+1, dist[nb][cur.used+1]});
}
}
}
retour -1; // inaccessible – le graphique est connecté, donc jamais
}
};
«» "

---

- Oui. 5. Bien, mal et mal – Ce que les intervieweurs tiennent vraiment à

Autres Phase Ce qu'un candidat ** devrait faire** Ce qu'un candidat ** ne devrait pas faire**
-- -- -- -- -- -- -- ----------------------------------------------------------------------------------
**Bon*** *Stateful Dijkstra* – concis, n'utilise qu'une seule file d'attente prioritaire, la mémoire O((k+1)n).
**Bad** C'est vrai.
**Sur-ingénierie : écrire une classe de graphes personnalisée qui fuit la mémoire, ou mélanger BFS + DFS incorrectement, ou ignorer la propriété de la première visite à la destination.

**Pourquoi ce modèle est favorable à l'entrevue* *
- Oui. Il présente une compréhension claire de **Dijkstra**, **DP** et **state compression**.
- Oui. Cela prouve que vous pouvez raisonner à propos des problèmes d'état *augmenté – un thème d'interview fréquent.
- Oui. La solution est **linéaire dans `k`**: vous pouvez facilement expliquer si `k` étaient 0 we=d juste être Dijkstra=.
- Oui. Le code est propre, utilise des conteneurs de bibliothèque standard, et est assez court pour s'adapter sur un tableau blanc.

---

- Oui. 6. Tester votre solution

Cas de bords
- C'est quoi ?
`k = 0` – pas de houblon. Autres
`k = n-1` – vous pouvez zéro sur *any* edge La réponse sera toujours la limite de poids minimum sur un chemin *any* ; Dijkstra fonctionne toujours. Autres
Autres Graphique avec un seul bord entre « s » et « d » Soit utiliser le houblon (coût 0) ou garder le poids. Autres
Dijkstra choisira automatiquement celui qui utilise le houblon le moins cher. Autres
`n = 1` est impossible car `s` et `d` doivent être distincts – la déclaration garantit `n ≥ 2`. Autres

Utilisez les exemples de tests de LeetCode plus quelques tests personnalisés:

'`python
# Extrait de python
print(Solution().pathWithHops() est le plus court
5,
[[0,15],[1,2,3],[0,2,10],[2,3,1],[3,4],
0, 4, 2
)) # Prévu : 0 (arêtes de ski 0-1 et 2-3)
«» "

---

- Oui. 7. Article de blog convivial pour le référencement

Vous trouverez ci-dessous un article complet que vous pouvez copier dans un article moyen, Dev.to, ou votre propre blog.
N'hésitez pas à modifier le titre, à ajouter votre propre voix ou à laisser tomber les balises `#` qui fonctionnent avec la plupart des plateformes de blogs.

---

### ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> **Mots-clés**: *LeetCode 2714*, *Trouver le chemin le plus court avec K Hops*, *interview de l'algorithme graphique*, *Dijkstra stateful*, *entretien de l'ingénieur logiciel prep*, *algorithme libre de l'algorithme du houblon*, *programmation dynamique + Dijkstra*, *optimisation de la latence du réseau*, *mise à zéro des bords*, *structures de données de la théorie graphique*

---

C'est vrai. 1. Pourquoi ce problème est une « mine d'or » pour les intervieweurs

- **Graphiques fondamentaux** – bords, poids, connectivité.
- **Dijkstra** avancé – relaxation multi-états, file d'attente prioritaire.
- **La programmation dynamique sur le graphique** – la dimension "usedHops".
- **Analyse de la complexité** – Log-based runtime, utilisation de mémoire serrée.
- **La pensée d'Edge-case** – Et si vous atteigniez la limite de saut? Et si tous les bords sont zéro ?

Ces sujets se retrouvent dans les interviews *logiciels-ingénieurs* de Google, Microsoft, Amazon et de nombreuses équipes de data-sciences.

---

C'est vrai. 2. Récapitulation du problème (à partir de LeetCode)

> Avec un graphique pondéré, deux sommets distincts `s` et `d`, et un entier `k`, zéro-out *au plus* `k`.
> Calculer le poids total minimal de tout chemin de `s` à `d` après l'opération.

Les contraintes garantissent un graphe dense avec jusqu'à 10 000 bords et 500 sommets – un endroit doux pour Dijkstra.

---

C'est vrai. 3. Bien – L'état propre Dijkstra

1. **État = (vertex, houblon utilisé)* *
Chaque état est un nœud dans un graphique virtuel.
2. **Deux relaxations** – bord normal vs bord houblon (coût 0).
3. ** file d'attente prioritaire** – 'min-heap' commandé par distance accumulée.
4. **Début de sortie** – la première fois que nous pop un état dont le vertex est `d` est la réponse optimale.

**Pourquoi c'est bon**

- **Time‐optimal**: «O((k+1)·(n+m) log(n(k+1))»
- **Efficacité spatiale**: matrice de distance "O(n(k+1)".
- **Facile à comprendre** sur un tableau blanc: -Nous venons d'ajouter une dimension de plus.

---

C'est vrai. 4. Pourquoi les solutions naïves échouent

Pourquoi il est lent ou mal
Ce n'est pas le cas.
**FDS + force brute** – essayez chaque combinaison de "k` houblon (choisir les bords de `k` sur `m`) Temps exponentiel, impossible pour `m = 104`. Autres
**DP sur la liste des bords** – calculez la meilleure distance pour chaque vertex et chaque nombre de houblons dans une boucle imbriquée. Autres
**BFS sur le graphique élargi mais sans file d'attente prioritaire**BFS assume des poids unitaires; ici les coûts de bord varient considérablement ('w` jusqu'à 106). Autres

---

#### 5. – Ce que vous devez éviter

- ** Fuites de mémoire** : attribution de «vecteur<vecteur<int>>» dans une boucle, oubliant de se réinitialiser.
- **La file d'attente de priorité personnalisée** qui fausse l'ordre des éléments (par exemple, en utilisant un « max-heap » par accident).
- **Mixer les structures de données** (FDS pile + Dijkstra PQ) en une seule solution – conduit à la confusion des raisonnements sur le tableau.
- **Imprimer chaque état** pour déboguer – ralentit l'entrevue et montre un manque de concentration.

À emporter : restez simple. Utilisez des conteneurs standard de langage; ne sur-optimisez pas avant de connaître la structure du problème.

---

C'est vrai. 6. Passage de code (exemple de python)

'`python
Solution de classe:
def le plus court PathWithHops(self, n, bords, s, d, k):
graphique = [[] pour _ dans l'intervalle(n)]
pour u, v, w dans les bords:
graph[u].append(v, w))
graph[v].append(u, w))

INF = 10**18
dist = [[INF]*(k+1) pour _ dans la plage(n)]
dist[s][0] = 0
pq = [(0, s, 0)] # (dist, vertex, houblon)

alors que pq:
c, u, utilisé = heapq.heappop(pq)
si cur != dist[u][utilisé]:
poursuivre
Si u ==d:
retour cur
pour v, w dans le graphique[u]:
# normale
si cur + w < dist[v][utilisé]:
dist[v][utilisé] = cur + w
heapq.heappush(pq, (dist[v][utilisé], v, utilisé))
♪ sauter
si utilisé < k et cur < dist[v][utilisé+1]:
dist[v][utilisé+1] = cur
heapq.heappush(pq, (cur, v, used+1))
retour -1
«» "

N'hésitez pas à le coller dans votre IDE et à l'exécuter sur les tests de LeetCode.

---

C'est vrai. 6. Déploiement et parallèles du monde réel

Zero-ing un bord est semblable à **caching** ou **réduction de la latence** dans un réseau: vous êtes libre à "bypass" certains liens coûteux.
L'algorithme est utile pour :

- **Optimiser les tables de routage** dans les systèmes distribués.
- **Simuler les mises à niveau budgétaires** dans l'infrastructure (p. ex., combien de câbles pouvez-vous mettre à niveau pour réduire la latence totale?).

---

C'est vrai. 7. A emporter

- **Dijkstra** est une solution concise et puissante.
- **Données en blanc**: expliquer la dimension ajoutée et les deux relaxations.
- **Interviews**: expliquez pourquoi vous ne pouvez pas utiliser BFS et pourquoi la file d'attente prioritaire garantit l'optimalité.
- **Afficher l'analyse**: log-based runtime et comment vous l'avez dérivé.

Donnez-lui une chance sur votre prochaine interview – vous impressionnerez avec *correctitude* et *clarité*.

---

Autres lectures

- *Introduction aux algorithmes* – Algorithmes Dijkstra.
- * Algorithmes (CLRS)* – DP sur les graphiques, état de compression.
- * Programmation concurrente 3* – astuces avancées sur le chemin le plus court.

Bon codage, et que vos chemins soient toujours les plus courts! C'est ce qu'il a dit.

---

Bonus : Ajout d'une touche personnelle

- Ajoutez une courte anecdote de votre propre expérience en abordant un problème de graphique LeetCode.
- Partagez une capture d'écran de votre code sur un tableau blanc.
- Terminer par un appel à l'action : Vous avez un truc pour un problème similaire ? Laissez tomber les commentaires! (en milliers de dollars)

---

**Profitez de votre billet de blog,** et bonne chance avec ces interviews de codage! C'est ce qu'il a dit.

---

C'est tout – une explication prête à partager, prête à l'entrevue du LeetCode 2714, ainsi qu'un code propre dans le pseudocode Java (Java omis pour la brièveté), et un article complet pour mettre en valeur votre expertise auprès des gestionnaires d'embauche. Bon codage !