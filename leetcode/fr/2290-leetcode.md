---
titre: LeetCode 2290. Suppression minimale des obstacles pour atteindre le coin - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## C'est l'élimination minimale des obstacles pour atteindre le coin – LeetCode 2290
### A Deep‐Dive, 0‐1 BFS Masterclass (Java / Python / C++)
> **SEO Mots-clés** – *LeetCode 2290*, *Minimum Obstacle Removal to Reach Corner*, *0‐1 BFS*, *job interview coding*, *Java BFS solution*, *Python Dijkstra*, *C++ grid traversal*, *software ingénierie interview*

---

### TL;DR
- **Problème**: Trouver le nombre minimum d'obstacles (`1`) que vous devez supprimer pour voyager de `(0,0)` à `(m‐1,n‐1)` dans une grille `m × n` de `0`s (gratuit) et `1`s (obstacle).
- **Solution**: 0‐1 Breadth‐First Search (Dijkstra deque-based).
- **Heure**: "O(m · n)"
- **Espace**: "O(m · n)"

---

- Oui. 1. Récapitulation des problèmes

On vous donne une grille rectangulaire où chaque cellule est vide ('0') ou contient un obstacle (`1').
Vous pouvez monter, descendre, gauche ou droite ** seulement sur les cellules vides**.
Votre tâche : *supprimer le moins d'obstacles possible* afin qu'il existe un chemin allant du coin supérieur gauche au coin inférieur droit.

> **Juge**
> • Les termes `grid[0][0]` et `grid[m-1][n-1]` sont garantis `0`.
> • La taille de la grille peut être aussi grande que les cellules `10^5` (`m * n ≤ 100 000`).
• «1 ≤ m, n ≤ 10^5».

---

- Oui. 2. Pourquoi 0-1 BFS?

La grille peut être vue comme un graphique où chaque cellule est un nœud et les bords relient les cellules adjacentes orthogonalement.
Le déménagement sur une cellule **gratuite** coûte `0` (pas d'obstacle), tandis que le déménagement sur une cellule **obstacle** coûte `1` (vous devez la supprimer).

Il s'agit d'un problème classique *edge‐weight‐`0` ou `1` le plus court chemin*.
Au lieu d'une Dijkstra complète (en attente prioritaire), une *deque* suffit:

- Oui. Si le coût du bord est `0`, poussez le noeud vers le **front** (priorité plus élevée).
- Oui. Si le coût du bord est `1`, poussez-le vers le **back** (priorité inférieure).

Cela garantit que la première fois que vous pop un noeud, vous avez déjà trouvé le nombre optimal d'éliminations d'obstacles pour cette cellule.

---

- Oui. 3. Aperçu de l'algorithme

1. **Initialisation**
* `dist[m][n]` – matrice de distance, paraphée par `.
* "dist[0]] = 0".
* Deque `dq` commence par `(0,0)`.

2. **BFS Loop**
Alors que la deque n'est pas vide:
* Pop `(x, y)`.
* Pour chacun des quatre voisins `(nx, ny)` limites intérieures:
- "newDist = dist[x]y] + quadrillage[nx][ny]".
- Si "newDist < dist[nx][ny]":
* Mettre à jour `dist[nx][ny]`.
* Poussez `(nx, ny)` vers l'avant si `grid[nx][ny]] Autre chose.

3. **Résultat**
Retour `dist[m-1][n-1]`.

---

- Oui. 4. Mise en œuvre du code

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.
Chacun utilise le modèle BFS 0-1 décrit ci-dessus.

> **Astuce**: Lors de l'écriture pour les entrevues, garder le code concis mais lisible – ajouter des commentaires seulement où la logique n'est pas évidente.

---

### 4.1 Java (Java 17)

"Java
Importer java.util. - ArrayDeque;
Importer java.util. Les tableaux;
Importer java.util. Deque;

solution de classe publique {
Int minimum public Obstacles(int[][] grille) {
int m = longueur de la grille;
int n = grille[0].longueur;
int INF = entier.MAX_VALUE / 2; // éviter le débordement

int[]] dist = nouvelle int[m][n];
pour (int[] rang : dist) Arrays.fill(row, INF);

Deque<int[]> dq = nouveau ArrayDeque<>();
dist[0][0] = 0;
dq.offreFirst(new int[]{0, 0});

int[]] dirs = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};

alors que (!dq.isEmpty()) {
[] cur = dq.pollFirst();
int x = cur[0], y = cur[1];

pour (int[] d : dirs) {
int nx = x + d[0], ny = y + d[1];
si (nx < 0) nx >= m) ny < 0) ny >= n) continue;

int newDist = dist[x][y] + grid[nx][ny];
si (newDist < dist[nx][ny]) {
dist[nx][ny] = nouveauDist;
Si [grid[nx][ny]] 0) {
dq.offreFirst(nouvelle int[]{nx, ny});
} autre {
dq.offreDernière(nouvelle int[]{nx, ny});
}
}
}
}
retour [m - 1] [n - 1];
}
}
«» "

---

#### 4.2 Python (Python 3.10+)

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
def minimum Obstacles(même, grille: Liste[Liste[int]]) -> Int:
m, n = len(grid), len(grid[0])
INF = 10**9
dist = [[INF] * n pour _ dans la plage (m)]

dq = deque()
dist[0][0] = 0
Annexe((0, 0))

dirs = [(1, 0), (-1, 0), (0, 1), (0, -1)]

alors que dq:
x, y = dq.popleft()
pour dx, dy en dirs:
nx, ny = x + dx, y + dy
si 0 <= nx < m et 0 <= ny < n:
nouveau = dist[x][y] + grille[nx][ny]
si nouveau < dist[nx][ny]:
dist[nx][ny] = nouveau
si grille[nx][ny]] 0:
(nx, ny)
Sinon:
(nx, ny)
retour [m - 1] [n - 1]
«» "

---

### 4.3 C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int minimum Obstacles(vecteur<vecteur<int>>& grille) {
int m = quadrillage(), n = quadrillage[0].size();
const int INF = INT_MAX / 2;

vecteur<vector<int>> dist(m, vector<int>(n, INF)
deque<pair<int,int>> dq;

dist[0][0] = 0;
dq.emplace_front(0, 0);

dirs[4][2] = {1,0},{1,0},{0,1},{0,1},{0,1}};

pendant que (!dq.vide()) {
[x, y] = dq.front();
dq.pop_front();

pour (auto& d : dirs) {
int nx = x + d[0], ny = y + d[1];
si (nx < 0) nx >= m) ny < 0) ny >= n) continue;

int nd = dist[x][y] + grille[nx][ny];
si (nd < dist[nx][ny]) {
dist[nx][ny] = nd;
Si [grid[nx][ny]] 0)
dq.emplace_front(nx, ny);
Autre
dq.emplace_back(nx, ny);
}
}
}
retour dist[m-1][n-1];
}
};
«» "

---

- Oui. 5. Analyse de la complexité

Métrique
- C'est quoi ?
**Heure**=O(m · n)==O(m · n)===O(m · n)==
* Espace * * O(m · n) * O(m · n) *
**Pourquoi c'est rapide** Chaque cellule est sautée au plus une fois de l'avant; pousser vers l'avant/arrière est `O(1)`. Même raisonnement avec "deque". Autres

---

- Oui. 6. Manipulation de cas et gotchas

Qu'est-ce que regarder ?
- C'est quoi ?
**Grande grille** (`m*n = 10^5`)= La distance `int` 32 bits peut déborder si vous ajoutez beaucoup `1`s.= Utilisez `INF = INT_MAX/2` (C++/Java) ou `10**9` (Python). Autres
**Les bords de coût zéro pourraient créer des boucles. Le tableau de distance permet de ne jamais revisiter un noeud avec une distance inférieure. Autres
**Les limites du voisinage**Les erreurs hors-par-un sont fréquentes. Précalculer `m, n` une fois; utiliser `si (nx < 0) nx >= m=" ny < 0=" ny >= n) continuer;`"

---

- Oui. 7. Bon / mauvais / Ugly de l'entrevue

Aspect du bien
- C'est quoi ?
**Intuition** Oublier que vous ne pouvez pas marcher sur `0`s → mauvais BFS. Essayer de sur-enginer avec Dijkstra complet lorsque 0‐1 BFS est plus simple. Autres
**Le choix de l'algorithme**=0-1 BFS = optimal + concis.=L'utilisation d'un tas ralentit les facteurs constants. L'application aveugle de BFS sans frais de manutention → O(n^2) runtime. Autres
**Mise en œuvre**=Codage propre et simple.=Le surcommentage rend la solution bruyante.= Oublier de réinitialiser `INF` avant chaque test (état des fuites). Autres
**Tests** Exclure les cas de bord : tous les `0`, tous les `1` (sauf les coins), grille clairsemée, grande grille clairsemée. Seul le test sur l'échantillon – risque de manque de cas de bord. Pas d'instructions `assert`, donc les bogues glissent dans la production. Autres
**Readability**= Commentaires seulement lorsque la logique n'est pas triviale. En ligne lambda pour laque push → obscurcit l'intention. C++ mixte `utilisant l'espace de noms std;` vs explicite `std:` utilisation. Autres

---

- Oui. 8. Pourquoi cette solution est-elle pour votre prochain travail

1. **Afficher la profondeur algorithmique** – 0‐1 BFS est un modèle d'entrevue classique.
2. ** Démontre la discipline de codage** – structures de données propres, pas de nombres magiques, contrôle des limites appropriées.
3. **Prouve l'efficacité** – gère la limite de cellules `100 000` confortablement.

> **Le directeur de l'hébergement* *
> *= Pouvez-vous trouver le chemin le plus court sur une grille avec coût 0/1 dans le temps linéaire?
Oui, avec 0-1 BFS.
Autres Voici mon implémentation Java – prête à coller dans l'IDE.

---

- Oui. 9. Appel à l'action pour le codeur ambitieux

Si vous avez cloué ce problème:

1. **Posez-le sur LinkedIn** avec le titre « My LeetCode 2290 Solution – 0-1 BFS in Java / Python / C++.
2. **Tag recruteurs** dans l'espace technologique – recruteurs recherchent souvent des solutions *LeetCode 2290*.
3. **Ajouter le code** à votre repo GitHub sous un dossier `leetcode/2290_min_obstacle_removal`.

Autres **Vous voulez décrocher un rôle de génie logiciel? * *
> 1=Créer un portefeuille personnel avec des solutions bien commentées.
> Partager votre billet de blog sur Medium, dev.to et Hacker News.
> Appliquez aux entreprises qui aiment les défis algorithmiques – Amazon, Google, Stripe, Shopify, etc.

---

10. Pensées finales

Le problème *Minimum Obstacle Removal to Reach Corner* est une vitrine parfaite** de :

- Modélisation graphique d'une grille
- 0-1 BFS – une variante concise Dijkstra
- Manipulation des bords réfléchis

Maîtrisez ce modèle, et vous allez non seulement ace LeetCode 2290 mais impressionner également les recruteurs qui apprécient le code propre et efficace.

> **Votre prochaine grande question d'entrevue pourrait être un problème de grille – rappelez-vous simplement le tour de laque! **

Joyeux codage, et que l'algorithme soit toujours en votre faveur!

---

**Suivez-moi** sur Twitter @YourCodingJourney pour plus de prép d'entrevue, d'algorithmes et de conseils d'avancement professionnel.