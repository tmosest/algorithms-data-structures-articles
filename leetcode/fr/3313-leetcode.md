---
titre: LeetCode 3313. Trouver les derniers nœuds marqués dans l'arbre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. Trouvez les derniers nœuds marqués dans l'arbre
> **Hard** – LeetCode

> **Mots-clés**: *Diamètre de l'arbre*, *BFS*, *DFS*, *Distance la plus courte*, *Processus de marquage*, *Codeleit 3313*, *Java*, *Python*, *C++*, *Conception de l'algorithme*, *Préparation de l'entrevue*

---

Récapitulation des problèmes

On vous donne un arbre non dirigé avec des nœuds `n` (0 ... n‐1).
Au moment `t = 0` vous marquez un seul noeud `i`.
Chaque seconde, vous marquez tous les nœuds *non marqués* qui ont au moins un voisin marqué.

Pour chaque noeud de départ `i` sortie **any** noeud qui est marqué *last*.
S'il y a deux nœuds qui sont liés pour la dernière fois, vous pouvez les retourner.

`edges` est une liste de paires `n-1` `[u, v]` décrivant l'arbre.

«» "
Entrée: bords = [0,1],[0,2]]
Produit : [2,2,1]
«» "

---

Pourquoi le diamètre de l'arbre aide

Le processus de marquage est l'équivalent d'une onde qui s'étend d'un bord par seconde à partir du nœud de départ.
Le dernier nœud à atteindre est exactement celui qui est le plus éloigné du départ.

Dans un arbre, la distance la plus éloignée de n'importe quel noeud est toujours à l'un des deux paramètres *diamètre* (les deux extrémités du chemin le plus long).
Donc, pour chaque noeud `i` nous avons seulement besoin de savoir qui des deux extrémités de diamètre est plus loin de `i`.
Cette fin est garantie d'être un nœud valide de dernière marque.

---

Bonne

Ce qu'il fait
C'est quoi ?
** Temps linéaire** ("O(n)") et espace ("O(n)"). Autres
* Fonctionne pour la contrainte maximale (`n = 105`). Autres
Aucune récursion lourde – utilise BFS/DFS itérative pour éviter le débordement de la pile. Autres
Une logique très claire : diamètre → deux tableaux de distance → réponse par noeud. Autres

---

Mauvais

Pièges potentiels
-- -- -- -- -- -- -- --
Si vous oubliez que l'arbre est *non dirigé* vous allez mal construire le graphique. Autres
En se basant sur la récursion avec la profondeur > 104 peut s'écraser sur certains systèmes. Autres
Le choix de la mauvaise solution (par exemple, « point 2 » lorsque les distances sont égales) peut encore satisfaire le problème, mais peut donner une réponse différente de celle attendue par certains harnais d'essai. Autres
L'oubli de la longueur des bords est `n‐1` pourrait entraîner une erreur de taille de tableau. Autres

---

# ### # Ugly

Les choses qui peuvent obtenir désordre
Il n'y a pas de lien entre les deux.
L'écriture de trois implémentations BFS/DFS distinctes pour Java, Python et C++ conduit à une logique dupliquée. Autres
Le mélange des indices 0 et 1 dans les commentaires ou les noms de variables peut confondre les responsables. Autres
La suringénierie de la solution (par exemple, en utilisant Dijkstra ou une file d'attente prioritaire) augmente inutilement la complexité. Autres

---

Aperçu de l'algorithme

1. **Construire la liste d'attente** (`Liste<Liste<Integer>>` en Java, `defaultdict(list)` en Python, `vector<vector<int>>` en C++).
2. **Trouver un paramètre de diamètre (`point1`)**: BFS/DFS du nœud 0 au nœud le plus éloigné.
3. **Trouver l'autre paramètre de diamètre (`point2`)**: BFS/DFS à partir de `point1`.
4. **Tableaux de distance de calcul**
* `dist1[i]` – distance entre `point1` et noeud `i`.
* `dist2[i]` – distance entre `point2` et le noeud `i`.
5. **Réponse au noeud `i`**
* Si `dist1[i] >= dist2[i]` → `point1` (années arbitrairement).
* Autre → `point2`.

Tous les parcours BFS/DFS sont linéaires, donc le temps total `O(n)`.

---

Analyse de complexité

Calcul métrique
C'est pas vrai.
**Temps**=O(n)=4 traversées de l'arbre. Autres
**Space**="O(n)` – liste d'adjacence + 2 tableaux de distance + file d'attente/pistolet. Autres

---

Liste de contrôle des cas de bord

Autres Décision Pourquoi ça compte ?
- - - - - - - - - - Non.
Un seul bord, les deux paramètres de diamètre sont les deux nœuds. BFS retourne le nœud le plus éloigné correctement. Autres
Autres Graphique stellaire (un centre, de nombreuses feuilles) Les paramètres de diamètre sont deux feuilles; les distances sont gérées correctement. Autres
Autres Arbre très profond (piste) Utilité BFS/DFS utilisée. Autres
Dupliquer les bords ou les boucles de soi-même. Pas besoin de contrôles supplémentaires. Autres

---

Extraits de mise en œuvre

Voici des solutions propres et prêtes à la production dans **Java, Python et C++**.

> **Conseil** – Tous les trois utilisent BFS itérative pour la sécurité et la clarté.
> **Aperçu** – Remplacer `ArrayDeque` par une simple file d'attente `int[]` si la mémoire devient une préoccupation.

### Java (Java 17+)

"Java
Importation de java.util.*;

solution de classe {
Int[] bfs(Liste <entier>[] graphique, démarrage int) {
int n = longueur du graphique;
int[] dist = nouvelle int[n];
les tableaux.fill(dist, -1);
ArrayDeque<entier> q = nouveau ArrayDeque<>();
q.add(démarrage);
dist[start] = 0;
alors que (!q.isEmpty()) {
int u = q.poll();
pour (int v : graph[u]) {
si (dist[v]) -1) {
dist[v] = dist[u] + 1;
q.add(v);
}
}
}
de retour;
}

intérieur statique int farthestNode(int[] dist) {
int nœud = 0, meilleur = -1;
pour (int i = 0; i < dist.longueur; i++) {
si (dist[i] > le meilleur) {
best = dist[i];
noeud = i;
}
}
noeud de retour;
}

Int[] dernierMarkedNodes[[][] bords) {
int n = bords longueur + 1;
@SuppressAvertissements("non vérifié")
Liste <entier>[] graphique = nouvelle liste[n];
pour (int i = 0; i < n; i++) graphe[i] = nouvelle liste de distribution<>();

pour (int[] e : bords) {
u = e[0], v = e[1];
graphic[u].add(v);
graphic[v].add(u);
}

// 1er paramètre
int[] dist0 = bfs(graphique, 0);
int p1 = plus loinNode(dist0);

// 2ème paramètre
int[] dist1 = bfs(graphe, p1);
int p2 = plus loinNode(dist1);

// Distances par rapport à l'autre paramètre
int[] dist2 = bfs(graphique, p2);

int[] ans = nouvelle int[n];
pour (int i = 0; i < n; i++) {
as[i] = dist1[i] >= dist2[i] ? p1 : p2;
}
le retour des an;
}
}
«» "

---

### Python 3 (3.8+)

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
def _bfs(self, graph: List[List[int]], start: int) -> Liste[int]:
n = len(graphe)
dist = [-1] * n
q = deque([start])
dist[démarrer] = 0
alors que q:
u = q.popleft()
pour v dans le graphique[u]:
si dist[v] == - 1 :
dist[v] = dist[u] + 1
q.appendice v)
retour

def _farthest(self, dist: List[int]) -> Int:
retour max(range(len(dist)), clé=lambda i: dist[i])

dernière MarkedNodes(même, bords: Liste[Liste[int]]) -> Liste[int]:
n = len(edges) + 1
graphique = [[] pour _ dans l'intervalle(n)]
pour u, v dans les bords:
graphic[u].append(v)
graphic[v].append(u)

d0 = auto._bfs(graphique, 0)
p1 = self._farthest(d0)

d1 = auto._bfs(graphe, p1)
p2 = self._farthest(d1)

d2 = auto._bfs(graphique, p2)

retourner [p1 si d1[i] >= d2[i] sinon p2 pour i dans l'intervalle(n)]
«» "

---

C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> bfs(const vector<vector<int>>&g, int start) {
int n = g.size();
vecteur<int> dist(n, -1);
file d'attente <int> q;
q.push(démarrage);
dist[start] = 0;
pendant que (!q.vide()) {
i) u = q.front();
pour (int v : g[u]) {
si (dist[v]) -1) {
dist[v] = dist[u] + 1;
q.push(v);
}
}
}
de retour;
}

int farthest(const vector<int>& d) {
int nœud = 0, meilleur = -1;
pour (int i = 0; i < (int)d.size(); ++i)
si (d[i] > meilleur) { meilleur = d[i]; noeud = i; }
noeud de retour;
}

vector<int> lastMarkedNodes(vecteur<vecteur<int>>& bords) {
int n = bords.taille() + 1;
vecteur<vector<int>> g(n);
pour (auto& e : bords) {
u = e[0], v = e[1];
g[u].push_back(v);
g[v].push_back(u);
}

d0 = bfs(g, 0);
int p1 = plus loin(d0);

auto d1 = bfs(g, p1);
int p2 = plus loin(d1);

auto d2 = bfs(g, p2);

vecteur <int> ans(n);
pour (int i = 0; i < n; ++i)
ans[i] = (d1[i] >= d2[i]) ? p1 : p2;
le retour des an;
}
};
«» "

---

Essais

Exécuter le harnais d'essai minimal suivant dans chaque langue pour vérifier l'exactitude:

"Java
les bords int[] = {{0,1},{0,2}};
int[] result = new Solution().lastMarkedNodes(edges);
Système.out.println(Arrays.toString(result)); // [2, 2, 1]
«» "

'`python
print(Solution().lastMarkedNodes([[0,1],[0,2])) # [2, 2, 1]
«» "

'`cpp
vecteur<vector<int>> bords = {{0,1},{0,2}};
Solution sol;
auto res = sol.lastMarkedNodes(edges);
pour (int x : res) cout << x << '; // 2 2 1
«» "

---

## C'est l'interview-Ready à emporter

- **Point de vue principal**: La vague atteint le diamètre se termine en premier.
- **Mise en œuvre**: 4 BFS/DFS passent → "O(n)" temps et espace.
- **Langues**: Java, Python, C++ – tous partagent la même logique itérative propre.

Avec ce modèle, vous allez casser le problème en quelques secondes, impressionner l'intervieweur, et obtenir une base de code propre à maintenir.

Bon codage ! C'est ce qu'il a dit.

---

*Préparé par un ingénieur logiciel chevronné, prêt à être copié dans n'importe quel dépôt d'entrevue de codage. *