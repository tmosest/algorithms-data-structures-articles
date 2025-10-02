---
titre: LeetCode 3486. Voie spéciale II la plus longue -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Explication de la solution**

Pour chaque cas de test nous sommes donnés

* `n` – nombre de nœuds d'un arbre
* `n` entiers - la valeur stockée dans chaque noeud (ils ne sont pas nécessaires pour le
tâche, mais font partie du format d'entrée)
* lignes `n-1` – chaque ligne contient deux indices de nœud `u , v` et a
entier positif `w` – le poids du bord entre `u` et `v`.

L'arbre est connecté et n'a pas de cycles.
La tâche consiste à afficher la longueur ** du chemin le plus long de l'arbre** mesuré
par la somme des poids de bord.
(Si l'arbre est pondéré, la définition naturelle de son diamètre est cette somme.)

-----------------------------------------------------------------------------------

Observations

* Un arbre a exactement un chemin simple entre deux sommets.
* Le plus long chemin est appelé le **diamètre** de l'arbre.
* Dans un arbre pondéré la longueur d'un chemin est la somme des poids de tous
les bords du sentier.
* Pour n'importe quel arbre, nous pouvons trouver un point final d'un diamètre en exécutant un
recherche de profondeur (DFS) (ou recherche de largeur, BFS) à partir d'une recherche arbitraire
vertex et garder le vertex qui est le plus loin.
* En commençant par ce paramètre et en exécutant une seconde DFS donne à nouveau l'autre
le diamètre et la longueur du diamètre.

-----------------------------------------------------------------------------------

Algorithme
«» "
lire n
lire les valeurs du nœud n et les ignorer

build adjacency list g[0 ... n-1]
pour chacun des bords n-1:
lire u, v, w
ajouter (v,w) à g[u] et (u,w) à g[v]

fonction la plus lointaine(début):
// retourne (vertex, distance) qui est le plus éloigné du début
dist[0 ... n-1] = -1
pile S
pousser le démarrage sur S
dist[démarrer] = 0
alors que S n'est pas vide:
u = pop S
pour chaque (v,w) en g[u]:
si dist[v] == - 1 :
dist[v] = dist[u] + w
Pousser v sur S
// trouver vertex avec la distance maximale
meilleur = début, meilleur Dist = 0
pour i = 0 ... n-1:
si dist[i] > meilleur Dist :
bestDist = dist[i]
meilleure = i
retour (meilleur, meilleurdiste)

(premier point, _) = plus loin(0)
(_, diamètre) = plus loin (premier point)

diamètre de sortie
«» "

-----------------------------------------------------------------------------------

Preuve d'exactitude

Nous prouvons que l'algorithme produit la longueur du diamètre du
l'arbre pondéré.

---

Lemma 1
`farthest(start)` retourne un vertex qui est le plus loin de `start` et le
distance jusqu'à ce vertex.

**Prof.**

La fonction effectue un DFS à partir de `start`.
"dist[v]" est réglé exactement une fois, à la distance du chemin simple unique
de `start` à `v`.
Parce que l'arbre ne contient aucun cycle, c'est la seule distance possible.
Après le DFS tous les sommets sont accessibles, donc toutes les distances sont connues.

La fonction scanne tous les sommets et garde celui avec le maximum
"dist".
Par conséquent, le vertex retourné est exactement le plus loin de "départ",
et la distance retournée est la distance correspondante. *



Lemma 2
Laissez `x` être un vertex arbitraire et `y` le vertex retourné par
"plus loin(x)".
Puis `y` est un point final d'un diamètre de l'arbre.

**Prof.**

Supposons le contraire – que `y` n'est pas un point final d'un diamètre.
Que `u` et `v` soient les deux paramètres d`un diamètre avec la longueur `D`
(`dist(u,v)=D`).

De Lemma 1 `dist(x,y)` est la distance maximale de `x`.
Parce que `y` n'est pas un point final d'un diamètre,
`dist(x,u)` et `dist(x,v)` doivent tous deux être ** strictement plus petits** que
`dist(x,y)`; sinon, le chemin de `x` vers le paramètre le plus éloigné
aurait la longueur `dist(x,y)` et serait au moins aussi longtemps que le
diamètre, une contradiction.

Mais un arbre de diamètre est un chemin simple le plus long.
Si ni `u` ni `v` ne sont les plus éloignés de `x`, le chemin le plus long
commence à partir de "x" n'est pas un diamètre, en contradiction avec le fait que
le plus long chemin dans un arbre qui part d'un vertex arbitraire doit être un
diamètre du point final.
Par conséquent, l'hypothèse est fausse et `y` est en effet un paramètre de
diamètre. *



Lemma 3
Le deuxième appel de "plus loin" a commencé à partir d'un point final d'un diamètre
renvoie l'autre paramètre et la longueur du diamètre.

**Prof.**

Que `a` soit un point final d'un diamètre, et `b` l'autre point final.
Par Lemma 2, le premier appel `farthest(0)` renvoie un certain point final d'un
diamètre; l'appeler "e".
Considérez maintenant le deuxième appel `farthest(e)`.
Toutes les distances de `e` sont à nouveau correctement calculées
(Lemma 1).
Le sommet le plus éloigné de `e` doit être l'autre paramètre de *certains*
diamètre.
Parce qu'un arbre a un chemin simple unique entre deux sommets,
le chemin le plus long qui commence par `e` est exactement le diamètre, et son
un autre paramètre est "b".
Ainsi la distance retournée par le second appel est égale au diamètre
longueur.



C'est vrai. Théorème
L'algorithme produit la longueur du diamètre de l'entrée pondérée
arbre.

**Prof.**

Le premier appel `à distance(0)` donne un vertex `a` qui est un point final d'un
diamètre (Lemma 2).
Le deuxième appel est le plus éloigné. donne le paramètre inverse `b` et le
distance entre eux – par Lemma 3 cette distance est exactement la
diamètre de longueur.
L'algorithme produit cette distance, donc il produit le diamètre
longueur.



-----------------------------------------------------------------------------------

Analyse de complexité

Que `n` soit le nombre de sommets.

* Bâtir la liste d'assiduité: `O(n)`
* Chaque DFS visite chaque vertex et bord une fois: `O(n)`
* Deux tours de DFS: `O(n)`
complexité du temps total: **'O(n)'**

La liste d'adjacence stocke les entrées de bord "2·(n-1"), chaque entrée conserve une
vertex id et un poids ( "long long").
La consommation de mémoire est `O(n)`.



-----------------------------------------------------------------------------------

#### Mise en œuvre de la référence (GNU‐C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

Int main() {
ios::sync_with_stdio(faux);
cin.tie (nullptr);

l'élément n;
si (!(cin >> n)) retourner 0; // aucune entrée

/* lire les valeurs des nœuds – elles font partie du format d'entrée mais ne sont pas utilisées */
vecteur <long long> nodeValue(n);
pour (int i = 0; i < n; ++i) cin >> nodeValue[i];

/* construire une liste d'adjacence avec des poids */
vecteur<vector<pair<int,long>>> g(n);
pour (int i = 0; i < n - 1; ++i) {
u, v; longue w;
cin >> u >> v >> w;
g[u].push_back({v, w});
g[v].push_back({u, w});
}

/* */
auto farthest = [&](int start) -> paire<int, long> {
vecteur <long long> dist(n, -1);
Pile <int> m;
s.push (départ);
dist[start] = 0;

pendant que (!st.vide()) {
u = st.top(); st.pop();
pour (auto [v,w] : g[u]) {
si (dist[v]) -1) {
dist[v] = dist[u] + w;
le point v) est remplacé par le texte suivant:
}
}
}

int best = début; long long best Dist = 0;
pour (int i = 0; i < n; ++i) {
si (dist[i] > bestDist) {
bestDist = dist[i];
best = i;
}
}
retour {meilleur, meilleur Dist};
};
/* */

auto [premier point, _] = plus loin(0);
auto [_, diamètre] = le plus éloigné (premier point);

cout << diamètre << '\n';
retour 0;
}
«» "

Le programme suit exactement l'algorithme prouvé correct ci-dessus
et se conforme au compilateur GNU++17.