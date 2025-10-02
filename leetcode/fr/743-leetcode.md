---
titre: LeetCode 743. Délai réseau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Mastering LeetCode 743 – Temps de retard réseau
**Le bon, le mauvais et le mauvais – un guide complet pour les codeurs de préparation à l'entrevue**

---

Pourquoi ce problème compte

- **LeetCode Rang:** #743 (Moyen) – un favori d'entrevue classique.
- **Concepts testés :** Représentation graphique, parcours le plus court, files d'attente prioritaires, gestion du poids de bord.
- **Real-World Analog:** La propagation des signaux dans un réseau de communication ou la latence de transmission des messages dans les systèmes distribués.

Si vous voulez **déposer un rôle d'ingénierie logicielle** qui valorise les algorithmes graphiques, la résolution de ce problème vous séparera de la foule. Ci-dessous vous trouverez:

1. **Une explication claire et conviviale** de l'algorithme.
2. **Codage libre en Java, Python et C++** – prêt pour copier-coller.
3. **SEO-optimized blog content** qui sera classé haut sur les moteurs de recherche et aider les recruteurs vous trouver.

---

Réévaluation des problèmes

> **Temps de retard du réseau**
> Étant donné un graphique dirigé où `times[i] = [ui, vi, wi]` représente un bord du noeud `ui` à `vi` avec le poids `wi` (temps de déplacement), trouver le temps minimum nécessaire pour qu'un signal envoyé du noeud `k` atteigne **all** noeuds.
> Retour `-1` si un nœud n'est pas accessible.
>
> **Constraints**
> * `1 ≤ n ≤ 100`
> * `1 ≤ longueur ≤ 6000`
> * `0 ≤ wi ≤ 100`

---

Intuition – Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Représentation du graphique**= Liste d'adjacence → Espace O(E)= Oubliez de convertir 1-basé en indices 0-basés → IndexErreur== Utiliser un tableau 2-D de taille `n2` → Déchets de mémoire O(n2)=
**Shortest-Path Algorithme** , Dijkstra avec un min-heap → O(E log V) , Utiliser BFS pour les bords pondérés → Mauvaise réponse pour les poids non uniformisés , Ignorer les poids des bords (en traitant comme unité) → O(E + V) mais incorrect
**Cas d'Edge** `-1`=0 Oubliez d'initialiser la distance pour la source → Mauvaise valeur max=0 Ne pas manipuler les nœuds isolés → RuntimeError=0
**Performance**

---

Survol de l'algorithme – DijkstraS Voie

1. **Construire une liste d'assiduité**
`adj[u] = [(v, w), ...]`
Le graphique est dirigé; conservez l'orientation originale.

2. **Initialiser les distances**
`dist[i] = -- pour tous les nœuds, `dist[k] = 0`.

3. **Priority Queue (Min-Heap)* *
Chaque élément est une paire `(current_distance, noeud)`.
Pope le noeud avec la plus petite distance provisoire.

4. **Dilatation**
Pour chaque voisin `(v, w)` du noeud sauté:
«» "
si dist[u] + w < dist[v]:
dist[v] = dist[u] + w
Pousser (dist[v], v) dans le tas
«» "

5. **Réponse**
Après que le tas est vide, s'il y a un `dist[i]=#===========================================================================================================================================================================================================================================
Sinon, retourner `max(dist)` – le moment où le dernier nœud reçoit le signal.

---

Numéro de code

C'est pas vrai. Java

"Java
Importation de java.util.*;

solution de classe {
réseau public intDelayTime(int[][] times, int n, int k) {
// 1-based → 0-based conversion géré dans les boucles
Liste<List<int[]>> adj = nouvelle liste de distribution<>(n + 1);
pour (int i = 0; i <= n; i++) adj.add(new ArrayList<>());

pour (int[] t : heures) {
adj.get(t[0]).add(nouveau int[]{t[1], t[2]}); // [voix, poids]
}

int[] dist = nouvelle int[n + 1];
Arrays.fill(dist, entier. MAX_VALUE;
dist[k] = 0;

// PrioritéQuue de (distance, noeud)
PrioritéQueue<int[]> pq = nouveau PrioritéQueue<>(Comparator.comparingInt(a -> a[0]);
pq.offre(nouvelle int[]{0, k});

pendant que (!pq.isEmpty()) {
int[] cur = pq.poll();
int d = cur[0], u = cur[1];

// Sauter les entrées statiques
si (d != dist[u]) continue;

pour (int[] edge : adj.get(u)) {
int v = bord[0], w = bord[1];
si (d + w < dist[v]) {
dist[v] = d + w;
pq.offre(nouvelle int[]{dist[v], v});
}
}
}

Int ans = 0;
pour (int i = 1; i <= n; i++) {
Si (dist[i]) Integer.MAX_VALUE) retour -1;
ans = Math.max(ans, dist[i]);
}
le retour des an;
}
}
«» "

# # # # # #

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
def réseau DelayTime(self, times: List[List[int]], n: int, k: int) -> Int:
adj = [[] pour _ dans la plage (n + 1)]
pour u, v, w dans les temps:
(v, w))

dist = [float('inf')] * (n + 1)
dist[k] = 0

heap = [(0, k)] # (distance, noeud)
pendant que le tas:
d, u = heapq.heappop(heap)
Si d != dist[u]:
poursuivre
pour v, w in adj[u]:
nd = d + w
si nd < dist[v]:
dist[v] = nd
heapq.heappush(heap, (nd, v))

max_time = max(dist[1:]) # saut index 0
retour -1 si max_time == float('inf') sinon max_time
«» "

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
réseau int Délai(vector<vector<int>>& times, int n, int k) {
vecteur<vector<pair<int,int>>> adj(n + 1);
pour (auto &t : heures)
adj[t[0]].push_back({t[1], t[2]}); // { voisin, poids}

const int INF = INT_MAX / 2; // Éviter les débordements
vecteur<int> dist(n + 1, INF);
dist[k] = 0;

utilisant P = paire<int,int>; // (distance, noeud)
priorité_queue<P, vecteur<P>, plus grande<P>> pq;
pq.emplace(0, k);

pendant que (!pq.vide()) {
[d, u] = pq.top(); pq.pop();
si (d != dist[u]) continue; //

pour (auto [v, w] : adj[u]) {
si (d + w < dist[v]) {
dist[v] = d + w;
pq.emplace(dist[v], v);
}
}
}

Int ans = 0;
pour (int i = 1; i <= n; ++i) {
si (dist[i] == INF) retourner -1;
as = max(ans, dist[i]);
}
le retour des an;
}
};
«» "

> **Les trois implémentations** utilisent un tas de *binaires* (`PriorityQueue` / `heapq`) et une liste d'adjacence, ce qui donne la complexité de temps optimale `O(E log V)`.

---

Analyse de complexité

Langue Heure Espace
- C'est quoi ?
Java (Log V) (opérations en lourd) (Log V) (List d'adjacence + tableau de distance)
Python "O(E log V)" "O(V + E)" Autres
"O(E log V)" Autres

Avec les limites de problème (`n ≤ 100`, `E ≤ 6000`), les trois solutions fonctionnent confortablement sous 10 ms sur du matériel moderne.

---

Les pièges communs

Comment éviter
C'est quoi ?
Autres **Introductions de tas d'étourdissement**= Vérifier `if d != dist[u]` avant de se détendre. Autres
**1-basé versus 0-basé des indices**. Autres
**Utiliser `int` pour les distances**= Poids des bords ≤ 100, `n` ≤ 100 → distance maximale possible ≤ 100 * 99 = 9900. `int` est très bien, mais utiliser `INF` assez grand. Autres
** Direction du graphique**= N'oubliez pas que les bords sont dirigés; l'échange de `u` et `v` modifie complètement le problème. Autres
Après Dijkstra, scannez le tableau `dist` pour `INF` afin de détecter les nœuds inaccessibles. Autres

---

Conseils pour l'entrevue

1. ** Expliquez le modèle graphique d'abord** – les recruteurs aiment vous voir articuler le problème avant de sauter dans le code.
2. **Discuse la complexité à l'avance** – montrez que vous connaissez les compromis entre Dijkstra, BFS et Bellman-Ford.
3. **Modalités alternatives** (p. ex. SPFA, Floyd-Warshall) et pourquoi elles sont moins adaptées à ce problème.
4. **Parler des cas d'angle** – noeuds isolés, bords de poids zéro, boucles auto.
5. **Afficher la confiance** – souligner que Dijkstra garantit l'optimalité pour les poids non négatifs.

> *Dijkstra n'est pas seulement une astuce de codage; c'est l'algorithme qui garantit une trajectoire plus courte correcte pour tout graphique dirigé avec des poids de bord non négatifs.

---

Référence Meta Mots clés

html
<title>LeetCode 743 Temps de retard réseau – Dijkstra Algorithm expliqué (Java, Python, C++)</title>
<meta name="description" content="Solve LeetCode 743 – Temps de retard réseau avec Dijkstra. Obtenez une solution Java, Python et C++ propre pour les interviews de codage.">
<meta name="keywords" content="LeetCode 743, Network Delay Time, Dijkstra algorithme, graphique chemin le plus court, interview de codage, solution Java, solution Python, solution C++, question d'entrevue, interview d'ingénieur logiciel, structures de données, algorithmes">
«» "

Ces tags, combinés avec la structure de l'article, aideront votre classement de blog pour des requêtes comme:

- LeetCode 743 Retard réseau Solution temporelle
- Entretien de l'algorithme graphique de Dijkstra
- Java Python C++ chemin le plus court
- Solution de problème d'entretien de codage

---

Réflexions finales – Déposez votre prochain travail

1. **Maîtriser l'algorithme** – savoir *pourquoi* Dijkstra fonctionne et quand l'utiliser.
2. **Livrer du code propre et prêt à la production** – tester localement, puis coller dans l'éditeur de LeetCode.
3. **Parlez à l'intervieweur** – décrivez le graphique, le tas, la relaxation et la manipulation du boîtier.

En suivant la structure ci-dessus, vous produirez une solution *robuste, optimale* qui met en évidence votre capacité à résoudre des problèmes de graphiques non triviaux – exactement l'ensemble de compétences que les recruteurs recherchent chez les ingénieurs logiciels de niveau intermédiaire.

Bonne chance, et le codage heureux! C'est ce qu'il a dit