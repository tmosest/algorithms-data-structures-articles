---
titre: LeetCode 1976. Nombre de voies d'arrivée à destination -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solution 3 langues pour LeetCode 1976
**Problème** – *Nombre de voies d'arrivée à destination* (Moyenne)

> Compte tenu d'un graphique pondéré non dirigé, compter le nombre de plus courts
> chemins existent depuis le nœud **0** au nœud **n‐1**.
> Retourner le compte modulo **1 000 000 007**.

---

1.1 Récapitulation de l'algorithme

1. **Bâtiment de base** – liste d'adjacence
2. **Dijkstra + DP**
* `dist[u]` – distance connue la plus courte entre 0 et *u*
* `ways[u]` – nombre de chemins les plus courts vers *u*
* Quand une distance strictement plus courte vers un voisin est trouvée, mettre à jour
à la fois "dist" et "ways".
* Lorsqu'un chemin avec la distance *égale* est trouvé, ajouter le nombre de voies
du nœud actuel aux voies du voisin (modulo M).
3. Retour `ways[n-1]`.

complexité du temps : **O(E log V)* *
complexité spatiale: **O(V + E)**

---

- Oui. 2. Code

Vous trouverez ci-dessous une implémentation **propre, idiomatique** dans **Python 3**, **Java 17** et **C++17**.

> Tous les codes sont autonomes, compilent sur l'environnement LeetCode standard,
> et contiennent une méthode unique `countPaths` qui correspond à la signature du problème.

---

2.1 Python 3

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
MOD = 10 ** 9 + 7

Dénombrement Chemins(self, n: int, routes: List[List[int]]) -> Int:
# Créer une liste d'adjacence
graphique = [[] pour _ dans l'intervalle(n)]
pour u, v, w dans les routes:
graph[u].append(v, w))
graph[v].append(u, w))

dist = [float('inf')] * n
Voies = [0] * n
dist[0], voies[0] = 0, 1

pq = [(0, 0)] # (distance, nœud)

alors que pq:
d, u = heapq.heappop(pq)
Si d != dist[u]: # entrée statique
poursuivre

pour v, w dans le graphique[u]:
nd = d + w
if nd < dist[v]: # meilleure distance
dist[v] = nd
ways[v] = ways[u]
(pq, (nd, v))
elif nd == dist[v]: # un autre chemin plus court
ways[v] = (ways[v] + ways[u]) % self. MOD

retour des moyens[n - 1 % soi-même. MOD
«» "

---

#### 2.2 Java 17

"Java
Importation de java.util.*;

solution de classe {
finale statique privée longue MOD = 1_000_000_007L;

les voies publiques,
// liste d'adjacence
Liste<int[]>[] g = nouvelle liste de distribution[n];
pour (int i = 0; i < n; i++) g[i] = nouveau tableau <>();
pour (int[] e : routes) {
u = e[0], v = e[1], w = e[2];
g[u].add(nouvelle int[]{v, w});
g[v].add(nouvelle int[]{u, w});
}

long[] dist = nouveau long[n];
long[] ways = nouveau long[n];
Arrays.fill(dist, Long.MAX_VALUE);
dist[0] = 0;
Voies[0] = 1;

// min-pap (distance, noeud)
PrioritéQueue<long[]> pq = nouvelle prioritéQueue<>(Comparator.comparingLong(a -> a[0]);
pq.offre(nouvelle longue[]{0, 0});

pendant que (!pq.isEmpty()) {
long[] cur = pq.poll();
longue d = cur[0];
u = (int) cur[1];
si (d != dist[u]) continue; //

pour (int[] e : g[u]) {
int v = e[0];
longue w = e[1];
long nd = d + w;
si (nd < dist[v]) {
dist[v] = nd;
ways[v] = ways[u];
pq.offre(nouvelle longue[]{nd, v});
} sinon si (nd == dist[v]) {
ways[v] = (ways[v] + ways[u]) % MOD;
}
}
}

retour (int) (ways[n - 1] % MOD);
}
}
«» "

---

#### 2.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Constexpr statique long MOD = 1'000'000'007LL;

Int countPaths(int n, vecteur<vector<int>>& routes) {
vecteur<vector<pair<int, int>>> g(n);
pour (auto &e : routes) {
u = e[0], v = e[1], w = e[2];
g[u].push_back({v, w});
g[v].push_back({u, w});
}

vecteur <long long> dist(n, LLONG_MAX);
vecteur <long> voies(n, 0);
dist[0] = 0;
Voies[0] = 1;

utilisant P = paire <long long, int>; // (dist, noeud)
priorité_queue<P, vecteur<P>, plus grande<P>> pq;
pq.emplace(0, 0);

pendant que (!pq.vide()) {
[d, u] = pq.top(); pq.pop();
si (d != dist[u]) continue; // stale

pour (auto &[v, w] : g[u]) {
long et long = d + w;
si (nd < dist[v]) {
dist[v] = nd;
ways[v] = ways[u];
pq.emplace(nd, v);
} sinon si (nd == dist[v]) {
ways[v] = (ways[v] + ways[u]) % MOD;
}
}
}

retourner static_cast<int>(ways[n - 1] % MOD);
}
};
«» "

---

- Oui. 3. Article de blog – Le bon, le mauvais, et le lamentable de compter les chemins les plus courts

> **Audience cible:** Candidats à l'entrevue de conception de système, passionnés de la structure des données et demandeurs d'emploi à la recherche d'une solution LeetCode.

> **SEO Mots-clés:** LeetCode 1976, comptage des chemins les plus courts, Dijkstra DP, interview algorithmique, Python LeetCode solutions, problèmes d'entrevue Java, algorithme C++, comptage des routes les plus courtes, codage des entretiens d'emploi

---

### 3.1 Titre et méta

Contenu du champ
C'est quoi ?
Le bon, le mauvais, et le mauvais de compter les chemins les plus courts – LeetCode 1976
**Meta Description**= Master LeetCode 1976 avec une solution Dijkstra‐DP propre en Python, Java et C++. Apprenez les compromis, les pièges et le code d'entrevue qui impressionneront les gestionnaires d'embauche. Autres
LeetCode 1976, chemin le plus court, Dijkstra, programmation dynamique, codage d'entretien, itinéraires de comptage, solution Python, solution Java, solution C++

---

3.2 Aperçu

1. **Introduction** – pourquoi ce problème est important
2. **Le bon** – brillance algorithmique de Dijkstra + DP
3. **Le mauvais** – cas et pièges difficiles
4. **Les Ugly** – erreurs courantes dans les paramètres d'entrevue
5. **Code Walkthrough** – étape par étape pour Python Java, C++
6. ** Liste de contrôle du rendement** – que vérifient les gestionnaires d'embauche
7. **Take‐away** – comment en parler dans une entrevue
8. **Bonus** – approches alternatives et quand les utiliser

---

3.3 Organe de l'article

> *Sentez-vous libre de copier-coller ce balisage sur votre plateforme de blog. *

```markdown
# Le bon, le mauvais et le laid de compter les chemins les plus courts – LeetCode 1976

Quand vous voyez un problème qui demande *=Combien de façons puis-je atteindre une destination dans le moins de temps?=== l'instinct est de penser Dijkstra ou Floyd–Warshall.
Mais la torsion ? **Vous devez compter les chemins, pas seulement trouver la distance. **
Ci-dessous, nous disséquons le problème, découvrons les pièges cachés, et présentons des solutions propres et prêtes à l'interview dans **Python, Java et C++**.

- Oui. 1. Pourquoi ce problème est une médaille d'or pour les entrevues

- **Graphiques fondamentaux** – nœuds, bords, poids
- **Algorithme de chemin le plus court** – Cas d'utilisation classique de Dijkstra
- **Programmation dynamique sur graphiques** – comptage avec mémoisation
- **Modulo arithmétique** – gestion de grands nombres
- ** Sensibilité au boîtier** – gros poids, graphes denses, bords déconnectés (mais le problème garantit la connectivité)

Si vous clouez ceci, vous démontrez la maîtrise de tous les concepts CS de base que les recruteurs aiment.

- Oui. 2. Le bon – l'algorithme qui gagne

> **Idée**: Courez Dijkstra une fois, *simultanément* gardez un compteur du nombre de chemins les plus courts qui atteignent chaque nœud.

Étape Explication Pourquoi ça marche
C'est pas vrai.
**Liste d'adjacence de construction**
**Initialize**=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1
**Traitement prioritaire** Les garanties nous font toujours apparaître le nœud le plus court du monde
**Dilatation**= Si une nouvelle distance `< dist[v]` → mettre à jour `dist[v]` et `ways[v]` = `ways[u]` Amélioration classique de Dijkstra Autres
**Caisse d'égalité** → `ways[v] += ways[u]` Chaque route la plus courte jusqu ' à " u " s ' étend jusqu ' à une nouvelle route la plus courte jusqu ' à " v " Autres

Cette approche **one-pass** s'exécute dans `O(E log V)'—optimale pour les graphiques clairsemés.

- Oui. 3. Les cas de mauvais – bord qui brisent l'esprit

Ce qui arrive
- C'est quoi ?
Autres **Introductions d'un tas d'étalons** avant d'explorer
Autres **Poids très grands (1e6)**= Les distances peuvent déborder de 32 bits nombre d'ints.
**Modulo après l'ajout seulement**= Vous pourriez oublier de mod après chaque ajout== `ways[v] = (ways[v] + ways[u]) % MOD`=
**Graph avec des bords parallèles**=Le problème indique un graphique simple, mais si non, vous devez toujours garder tous les bords, Dijkstra le gère.

Être vigilant à cela assure que votre solution ne s'écrase pas sur des tests cachés.

- Oui. 4. L'Ugly – Entretien

1. **Utiliser `dist` comme un tableau de booléen visité* *
- Confuse la logique de la distance la plus courte; vous manquerez plusieurs chemins plus courts.
2. **Oubliant les entrées de tas d'impasse**
- Causes d'explosion "O(V^2)" dans le pire des cas.
3. **Modding seulement à la toute fin* *
- Débordement entier ou résultat modulo incorrect.
4. **Codage dur `int` pour les distances* *
- Fonctionne pour les petits poids mais échoue sur `w=10^6` et de nombreux bords.

Si vous voyez un de ces dans votre propre code, vous risquez un 0 dans une interview.

- Oui. 5. Passage du code – trois langues

> Ci-dessous vous pouvez copier l'implémentation directement dans votre IDE ou LeetCode.

Python 3

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
MOD = 10 ** 9 + 7
Dénombrement Chemins(self, n: int, routes: List[List[int]]) -> Int:
# liste d'adjacence
graphique = [[] pour _ dans l'intervalle(n)]
pour u, v, w dans les routes:
graph[u].append(v, w))
graph[v].append(u, w))

dist = [float('inf')] * n
Voies = [0] * n
dist[0], voies[0] = 0, 1
pq = [(0, 0)]

alors que pq:
d, u = heapq.heappop(pq)
Si d != [u]: # Tente
poursuivre
pour v, w dans le graphique[u]:
nd = d + w
si nd < dist[v]:
dist[v] = nd
ways[v] = ways[u]
(pq, (nd, v))
elif nd == dist[v]:
ways[v] = (ways[v] + ways[u]) % self. MOD

return ways[n-1] % self. MOD
«» "

*Pourquoi c'est propre: *
- Un "si" par voisin – pas de boucles cachées.
- Tous les états sont mis à jour ensemble – pas de laissez-passer DP séparé.

#### Java 17

* (voir le code dans la section 2.2 ci-dessus)*

C++17

* (voir le code à la section 2.3 ci-dessus)*

- Oui. 6. Liste de contrôle du rendement – Ce que les recruteurs remarqueront

Liste de contrôle Comment répondre
C'est quoi ?
**Complexité du temps**
Autres **Complexité spatiale**
**Poids importants**= Utiliser `long`/`long long` ou `float('inf')`– éviter le débordement
Remarquez que nous prenons du modulo
* Expliquez le garde-corps

- Oui. 7. Points d'entrevue prêts à parler

> J'utilise un Dijkstra* modifié où je garde un tableau auxiliaire "ways[]".
> Chaque fois que nous découvrons une nouvelle distance la plus courte à un vertex, nous écraseons son
> `ways[]`; si nous trouvons un chemin alternatif de longueur égale, nous accumulons
> chemins du nœud actuel.
> Cela garantit que lorsque nous avons finalement le nœud cible, `ways[n-1]`
> contient déjà le nombre total de chemins les plus courts. (en milliers de dollars)

Si l'intervieweur demande *= pourquoi ne pas exécuter BFS après Dijkstra?===*, expliquer que BFS serait `O(V+E)` par niveau et aurait encore besoin du tableau de distance; il ne donne pas un avantage de performance ici.

- Oui. 8. A emporter

- **Afficher le double rôle** de Dijkstra (distance) + DP (compte).
- **Mention modulo** tôt – les recruteurs vont clin d'œil à vos compétences en arithmétique.
- ** Expliquez pourquoi un log V est nécessaire** – O(E log V) bat O(E V) pour des graphiques clairs.

Avec les extraits de code ci-dessus, vous disposez d'une solution prête à être copiée, *interview-friendly* qui couvre l'ensemble du spectre, des fondamentaux du graphique aux manipulations grand entier.

Joyeux codage – et heureux entretien!

«» "

---

3.4 Liste de contrôle des performances

Cible
C'est quoi ?
**Temps** ≤ 0,3 s sur le LeetCode (Python) / ≤ 0,5 s (Java, C++) pour le graphe le plus dense
**Mémorie**= < 64 Mo – la liste d'adjacence est le choix préféré
**Clarté du code**= Pas de fonctions d'aide inutiles; pass simple, boucle unique
**Commentaires**

---

- Oui. 4. Pensées finales

Compter des chemins plus courts est plus qu'un jouet ; c'est un *signal* que vous pouvez **combiner des algorithmes classiques avec DP**.
Présentez la solution, passez à travers le code, et vous laisserez les intervieweurs avec confiance que vous pouvez gérer ** tout défi graph-théorie**.

---
«» "

---

- Oui. 4. Ce qu'il faut souligner au cours d'une entrevue

Thème Point de discussion
- Oui.
**Pourquoi Dijkstra fonctionne**
**Comptabilité simultanée**
**Entrées discontinues**
*Modulo**= Constante `1_000_000_007` – pourquoi nous en avons besoin (débordement de l'int, énormes nombres)=
**Complexité**

---

- Oui. 5. Conclusion

Vous possédez maintenant :

- **Compréhension théorique** d'un algorithme *hybride*
- **Code pratiquement vérifié** en trois langues principales
- **Narratif d'entrevue** qui met en évidence les forces, évite les pièges et fait preuve de confiance

Utilisez ces connaissances pour ace LeetCode 1976 et *n'importe quelle question d'entrevue qui suit.

> Bonne chance – que vos chemins soient toujours les plus courts et vos comptes toujours corrects! C'est ce qu'il a dit.
«» "

---

4.1 Discussion facultative: Solutions de rechange

Démarcher Quand utiliser
- C'est quoi ?
**Bellman–Ford + DP**= Le graphique peut contenir des bords négatifs (pas dans ce problème)= Plus simple à coder, fonctionne avec des poids négatifs== O(VE) – plus lent sur les grands graphiques==
**DP + Floyd–Warshall**
**Contribution avec BFS après Dijkstra**= Vous connaissez déjà les distances, vous n'avez besoin que de comptes.

Dans la plupart des contextes d'entretien, **Dijkstra + DP** reste la norme d'or.

---

- Oui. 5. Note finale

N'hésitez pas à adapter l'article pour votre portfolio personnel ou comme guide de référence pour les autres personnes interrogées. La combinaison d'un algorithme solide, d'un code propre et d'une explication réfléchie vous aidera à vous démarquer dans le monde concurrentiel de l'embauche technique. Bon codage !
«» "

---

> **Bon entretien!** Si vous avez des questions au sujet du code ou de l'article, laissez un commentaire ou contactez LinkedIn – laissez résoudre d'autres problèmes ensemble. C'est ce qu'il a dit.
«» "

---

> **Bonne chance,** et que tous vos chemins soient les plus courts!