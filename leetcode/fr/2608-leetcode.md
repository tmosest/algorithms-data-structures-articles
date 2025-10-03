---
titre: LeetCode 2608. Le cycle le plus court dans un graphique -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2608 – Cycle le plus court d'un graphique
> Le bon, le mauvais et l'hugly – Un guide complet (Java-Python C++) + un billet de blog SEO optimisé

---

- Oui. 1. Récapitulation des problèmes
> **Don** un graphique non dirigé * bidirectionnel* avec "n` sommets (`0 ... n-1`) et "edges" (`[ui, vi]`).
> **Retour** longueur du cycle *le plus court*.
> Si le graphique est acyclique, retourner `-1`.

Contraintes (Code Leet):
«» "
2 ≤ n ≤ 1000
1 ≤ longueur des bords ≤ 1000
0 ≤ ui, vi < n
ui vi
Pas de bords parallèles
«» "

---

- Oui. 2. Pourquoi ce problème est une *mine d'or* pour les entrevues

Raison
- Oui.
Il vous force à penser à la traversée du graphique, au suivi de distance et à la détection du cycle en un seul balayage. Autres
Discutable – DFS vs BFS, compromis temps/espace, représentations graphiques. Autres
Solvable en O(n·(n+m)) avec simple BFS – parfait pour une entrevue de codage de 5 minutes. Autres
Vous pouvez présenter votre maîtrise de BFS, des files d'attente et des modèles de code propres. Autres

---

- Oui. 3. La solution "Good" – une solution propre basée sur BFS

3.1 Intuition

1. **Rot le BFS à chaque vertex**.
2. Gardez deux tableaux :
* `dist[v]` – distance de la racine à `v`.
* `parent[v]` – le nœud d'où nous avons découvert pour la première fois «v».
3. Tout en explorant un bord «u – v»:
* Si `v` est non visité → définir sa distance et parent.
* Si `v` est déjà visité **et** `parent[u] != v` → un cycle est détecté.
La longueur du cycle est "dist[u] + dist[v] + 1".

Parce que BFS explore les sommets en augmentant la distance de la racine, la première fois que nous trouvons un voisin non-parent nous sommes garantis d'avoir le cycle *le plus court* qui passe par la racine. La répétition pour toutes les racines donne le minimum global.

3.2 Complexité

Temps Espace
C'est pas vrai.
Autres Pour un seul BFS. Autres
Autres Pour toutes les racines (réutilisé par BFS)

Avec `n, m ≤ 1000`, c'est confortablement rapide.

---

- Oui. 4. Les pièges communs

Pièges
C'est pas vrai.
Oubliez de marquer les nœuds visités avant de faire la demande. Utilisez un tableau `dist` initialisé à `-1` et vérifiez avant de faire une demande. Autres
Autres **Longueur du cycle d'essai**= Mélanger la vérification des parents (`dist[u] <= dist[v]` v `parent[u] != v`).== Comparaison explicite des parents; ou, si l'on utilise uniquement `dist`, conserver l'invariant `dist[u] <= dist[v]` lorsqu'on trouve un cycle. Autres
Utiliser une matrice d'adjacence naïve pour `n=1000`. Autres
**Manipulation incorrecte des composants déconnectés** Il s'agit d'un point d'ancrage. Autres

---

- Oui. 5. Le "Ugly" – Quand vous allez par-dessus bord

- Mélanger le code DFS et BFS dans la même fonction – mène à une logique difficile à lire.
- L'utilisation de la récursion pour BFS (queue stockée dans une liste) peut être source de confusion.
- Codage dur, infini, comme un nombre magique («1e9») au lieu d'une constante claire.
- Ecrire des classes d'aide séparées pour les trois langues sans un seul modèle de conception partagée.

*Leçon:* Tenir la mise en œuvre *simple* et *documenté*. Un BFS propre basé sur la file d'attente est la solution la plus durable.

---

- Oui. 6. Mise en œuvre des références

Ci-dessous vous trouverez **trois** solutions entièrement commentées.
Tous les trois suivent la même stratégie BFS, juste adaptée aux idiomes Java, Python et C++.

> **Astuce:** Pour votre portfolio ou GitHub, copiez la langue avec laquelle vous êtes le plus à l'aise et ajoutez-la à un dossier .

---

#### 6.1 Java 17

"Java
Importation de java.util.*;

solution de classe publique {
// Infinité sentinelle – plus grande que toute longueur de cycle possible
Inf = 1_000_000_000;

public int findShortestCycle(int n, int[][] bords) {
// Créer une liste d'adjacence
Liste <liste<entier>> graphique = nouvelle liste <>(n);
pour (int i = 0; i < n; ++i) graphe.add(new ArrayList<>());
pour (int[] e : bords) {
graphic.get(e[0]).add(e[1]);
graphic.get(e[1]).add(e[0]);
}

int best = INF;

// Exécuter BFS de chaque vertex comme racine
pour (int root = 0; racine < n; ++root) {
best = Math.min(best, bfs(root, graph, n));
}

meilleur retour == INF ? -1 : meilleur;
}

/** BFS de racine, retourne le cycle le plus court qui passe par racine, ou INF si aucun. */
Int privé bfs(int root, List<Liste<Intéger>> graphe, int n) {
int[] dist = nouvelle int[n];
Arrays.fill(dist, -1); // -1 → non visité
Queue<integer> q = nouveau ArrayDeque<>();
q.offre(root);
dist[root] = 0;

alors que (!q.isEmpty()) {
int u = q.poll();
pour (int v : graph.get(u)) {
si (dist[v]) -1) { // première visite v
dist[v] = dist[u] + 1;
q.offre(v);
} sinon si (dist[u] <= dist[v]) { // visité et non parent
// Nous avons trouvé un cycle: u → ... → v → u
retour dist[u] + dist[v] + 1;
}
}
}
retour INF; // aucun cycle impliquant la racine
}
}
«» "

---

#### 6.2 Python 3

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
INF = 10 ** 9

def trouver Plus court Cycle(self, n: int, bords: List[List[int]]) -> Int:
# liste d'adjacence
g = [[] pour _ dans l ' intervalle n)]
pour u, v dans les bords:
g[u].appendice(v)
g[v].append(u)

mieux = soi. INF

pour la racine dans la plage(n):
best = min(meilleur, self._bfs(root, g, n))

retour -1 s'il y a lieu. INF autrement mieux

def _bfs(self, root: int, g: List[List[int]], n: int) -> Int:
dist = [-1] * n
q = deque([root])
dist[root] = 0

alors que q:
u = q.popleft()
pour v en g[u]:
si dist[v] == -1: # première visite
dist[v] = dist[u] + 1
q.appendice v)
elif dist[u] <= dist[v]: # visité et non parent
retour dist[u] + dist[v] + 1
Revenez vous-même. INF
«» "

---

Numéro 6,3 C++ (ISO C++20)

'`cpp
#incluez <vecteur>
#incluez <queue>
#incluez <algorithme>
#incluez <cstring>

solution de classe {
INF = 1'000'000'000;

public:
int findShortestCycle(int n, std::vector<std::vector<int>& bords) {
// Créer une liste d'adjacence
À l'annexe I, le paragraphe 2 est remplacé par le texte suivant:
pour (const auto &e : bords) {
g[e[0]].push_back(e[1]);
g[e[1]].push_back(e[0]);
}

int best = INF;

pour (int root = 0; racine < n; ++root)
best = md::min(meilleure, bfs(root, g, n));

meilleur retour == INF ? -1 : meilleur;
}

particulier:
int bfs(int root, const std::vector<std::vector<int>>& g, int n) {
à:vecteur<int> dist(n, -1);
à:queue<int> q;
q.push(root);
dist[root] = 0;

pendant que (!q.vide()) {
i) u = q.front();
pour (int v : g[u]) {
si (dist[v]) -1) { // première visite
dist[v] = dist[u] + 1;
q.push(v);
} sinon si (dist[u] <= dist[v]) { // visité, non parent
retour dist[u] + dist[v] + 1; // longueur du cycle
}
}
}
retour INF; // aucun cycle impliquant la racine
}
};
«» "

---

- Oui. 7. Écrire un billet de blog prêt à travailler**

Ci-dessous est un article entièrement structuré que vous pouvez copier-coller dans un blog balisage (Pages GitHub, Dev.to, Medium, etc.).
Les titres, la densité des mots clés et l'appel à l'action en font **facile à la recherche** pour les recruteurs à la recherche de talents d'algorithme graphique.

---

Le bon, le mauvais et l'acharnement de trouver le cycle le plus court dans un graphique

```markdown
# Le bon, le mauvais, et l'ennui de trouver le cycle le plus court dans un graphique

> **LeetCode 2608 – Cycle le plus court d'un graphique**
> Une plongée profonde dans les modèles de codage BFS, DFS et prêts à l'entrevue

---

Pourquoi cette question vous fait réfléchir

- **Graph Traversal Mastery** – montre que vous pouvez manipuler les files d'attente, les listes d'adjacence et les matrices de distance.
- ** Discussion commerciale** – DFS vs BFS, complexité temporelle, complexité spatiale.
- **Réponse courte et longue** – parfait pour des entrevues de 5 minutes ou des séances de codage.

---

La bonne – une solution que tout le monde aime

L'approche BFS est le moyen le plus propre de détecter les cycles tout en calculant simultanément les chemins les plus courts.

1. **Root la recherche** à chaque vertex (`0 ... n-1`).
2. **Track** `dist[]` (distance de la racine) et implicitement le parent via l'ordre BFS.
3. **Détecter** un cycle lorsque vous rencontrez un noeud déjà visité qui est *pas* le parent.
4. ** Calculer** la longueur du cycle comme étant "dist[u] + dist[v] + 1".

"Java
// Extrait de Java (voir rubrique 6.1 ci-dessus)
«» "

'`python
# Extrait de python (voir rubrique 6.2 ci-dessus)
«» "

'`cpp
// Extrait C++ (voir section 6.3 ci-dessus)
«» "

**Heure**: «O(n(n + m)» – assez rapide pour «n, m ≤ 1000».
**Espace**: `O(n)` – tableau de distance réutilisé pour chaque BFS.

---

## Les mauvaises – Quoi éviter

Pourquoi ça se brise
- C'est quoi ?
Autres Ne pas marquer les nœuds visités avant de pousser à la file d'attente. Contrôle
Autres Utilisation d'un tableau parent qui devient écrasé.
Utiliser les listes d'adjacence
Suppression des composants déconnectés

---

La suringénierie qui éveille la lisibilité

- Mélanger la logique DFS & BFS en une seule méthode.
- Ecrire un BFS récursif qui utilise une liste comme file d'attente.
- Codage dur valeurs infinites au lieu de constantes nommées.
- Ajout de classes d'aide non liées qui encombrent le dépôt.

> **Conseil pro :** Gardez votre code *à usage unique* et *auto-documenté*.

---

Comment l'utiliser dans votre prochaine entrevue

1. ** Commencez par un croquis rapide** de l'idée BFS.
2. **Afficher votre code** dans une langue avec laquelle vous êtes à l'aise.
3. **Discuss** cas de bord (composants déconnectés, pas de cycles).
4. **Comparer** BFS vs. DFS – mettre en évidence la garantie de BFS du cycle le plus court.
5. **Mention** optimisations possibles (BFS bidirectionnelle, sortie anticipée) – même si vous ne les implémentez pas.

---

La pensée finale

Le problème *Shortest Cycle* est un *show-case* pour vos côtelettes graphi-algorithmiques.
Une solution BFS propre comme celle ci-dessus démontre :

- **Compréhension des structures de données** (listes de contiguïté, files d'attente).
- ** Pensée algorithmique** – suivi de distance + contrôles parent.
- ** Style de codage** – constantes claires, fonctions d'aide modulaire.

Ajoutez l'extrait de code à votre GitHub, engagez-le dans un dossier "Graph Algorithms" et ajoutez un commentaire expliquant l'approche. Les recruteurs aiment voir non seulement une solution de travail, mais aussi le *pourquoi* derrière vos choix.

---

Mots clés pour épurer

- cycle le plus court dans un graphique
- LeetCode 2608 solution
- entretien avec un algorithme graphique
- Détection du cycle BFS
- questions d'entretien avec un ingénieur logiciel
- algorithmes graphe traversants
- problème de graphique d'entretien d'emploi
- Algorithme graphique C++
- Algorithme du graphique Python

Ajoutez-les à votre blog méta tags, rubriques, et naturellement dans le contenu – il stimulera la découverte pour les recruteurs de chasse pour les ingénieurs graph‐savvy.

---

Bon codage, et que votre pile d'entrevue soit sans bugs! Les