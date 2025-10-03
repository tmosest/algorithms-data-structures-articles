---
titre: LeetCode 1102. Chemin avec la valeur minimale maximale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1102. Chemin avec la valeur minimale maximale – Un guide complet
*(Java, Python, C++ – Dijkstras Max-Heap + 4-direction BFS)*

---

Table des matières
1. Résumé du problème
2. Pourquoi Dijkstra + Max-Heap fonctionne
3. Mise en œuvre des langues (Java / Python / C++)
4. Description de la complexité du temps et de l'espace
5. Pièges communs (Les parties "Bad" et "Ugly")
6. Variantes et extensions
7. Conseils à emporter et conseils pour stimuler la carrière
8. Autres lectures et ressources

> **SEO Mots-clés**: Path With Maximum Minimum Value, LeetCode 1102, Algorithme Dijkstra, problème de chemin de grille, Java BFS, Python priority file, C++ priority file, problème de codage d'entretien, préparation d'entretien, entretien d'ingénierie logicielle, conseils d'entretien de codage, blog d'algorithme, entretien de structure de données, pensée algorithmique.

---

- Oui. 1. Résumé du problème

**LeetCode #1102 – Chemin avec la valeur minimale maximale* *

> *Avec une grille entière `m × n` `grid`, trouvez un chemin de la cellule supérieure gauche `(0,0)` vers la cellule inférieure droite `(m‐1,n‐1)` qui maximise la valeur **minimum** rencontrée le long du chemin. *

Le sentier ne peut se déplacer que dans les quatre directions cardinales (en haut, en bas, à gauche, à droite).
La réponse est le *score* du meilleur chemin – la plus grande valeur possible de l'entrée **le plus petit** de la grille sur ce chemin.

Exemples

Entrée Sortie Explication
C'est pas vrai.
[[5,4],[1,2,6],[7,4,6]] `4`- Le chemin surligné donne min = 4.
[[2,2,1,2,2,2],[1,2,2,1,2]
[[3,4,6,3,4],[0,2,1,1,7],[8,8,3,2,7],[3,2,4,9,8],[4,1,2,0,0],[4,6,5,4,3]

> **Constraints**
> 1 ≤ m, n ≤ 100, 0 ≤ grille[i][j] ≤ 109

---

- Oui. 2. Pourquoi Dijkstra + Max-Heap fonctionne

Le problème est une *maximisation d'un minimum* le long d'un chemin.
Pensez à chaque cellule comme un nœud avec le poids `grid[i][j]`.
Lorsque nous nous déplaçons vers un voisin, le score de chemin devient `min(current_score, voisin_value)`.
Nous voulons le meilleur score pour chaque nœud – le **maximum** possible tel score.

C'est exactement ce que fait l'algorithme de Dijkstras si nous interprétons le coût du bord comme --négatif ou si nous utilisons un *max-heap* au lieu d'un min-heap.
À chaque étape, nous prenons le nœud qui a actuellement le score le plus élevé, puis détendons ses voisins.

*Pourquoi max-heap? *
La file d'attente prioritaire stocke les tuples `(score, x, y)` triés par **descendant** score.
Lorsque nous pop un noeud, son score est garanti être le plus grand possible parmi tous les nœuds non atteints - la même propriété gourmande qui sous-tend Dijkstra.

**Invariant clé**

> La première fois que nous pop la cellule de destination, le score que nous pop est le score minimum maximum de n'importe quel chemin de `(0,0)` à cette cellule.

La preuve est identique à la preuve Dijkstra classique, juste avec `max` au lieu de `min` dans la comparaison.

---

3. Mise en œuvre de la 3e langue

> Les trois solutions suivent la même logique :
> *Initialiser une matrice `score` (`-1` = non atteint).
> Pousser `(grid[0][0], 0, 0)` dans une file d'attente prioritaire.
> Alors que la file d'attente n'est pas vide, pop la cellule avec le plus grand score, détendre ses quatre voisins, et mettre à jour leurs scores si nous avons trouvé un meilleur. *

> **Important:**
> *Évitez de visiter un nœud deux fois avec un score inférieur. *
> Il n'incite un voisin que si le nouveau score est strictement supérieur au score enregistré pour cette cellule.

#### 3.1 Java (JDK 17+)

"Java
Importation de java.util.*;

solution de classe publique {
finale statique privée [] DIRS = {{0,1},{1,0},{0,1},{1,0},{1,0}};

Int maximumMinimumPath(int[][] grille) {
int m = longueur de grille, n = longueur de grille[0];
int[][]meilleur = nouveau int[m][n];
pour (int[] range : best) Arrays.fill(row, -1);
meilleure[0][0] = grille[0][0];

// max-heap commandé par score
PrioritéQueue<int[]> pq = nouvelle prioritéQueue<>((a,b) -> Integer.compare(b[2], a[2]));
pq.offre(nouvelle int[]{0, 0, grille[0][0]}); // {x, y, score}

pendant que (!pq.isEmpty()) {
int[] cur = pq.poll();
int x = cur[0], y = cur[1], score = cur[2];

si (x == m-1 && y == n-1) retourne le score;

pour (int[]d : DIRS) {
int nx = x + d[0], ny = y + d[1];
si (nx < 0) ny < 0) nx >= m) continuer;

int newScore = Math.min(score, grille[nx][ny]);
si (NewScore > best[nx][ny]) {
best[nx][ny] = nouveau score;
pq.offre(nouvelle int[]{nx, ny, newScore});
}
}
}
retour -1; // inaccessible (ne se produit jamais sur une entrée valide)
}

// --- Pilote pour des tests locaux rapides
public statique vide principal(String[] args) {
[] g = {{5,4,5},{1,2,6},{7,6}};
System.out.println(nouvelle solution().maximumPath(g)); // 4
}
}
«» "

> **Pourquoi cette version Java est géniale* *
> *Explicité `int[][]Matrice du meilleur` → Mémoire O(mn). *
> *Comparateur max-heap avec `Integer.compare(b[2], a[2])' – pas d'objets d'emballage. *
> * Séparation claire de la logique de relaxation. *

3.2 Python (3,9+)

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
DIRS = [(0, 1), (1, 0), (0, -1), (-1, 0)]

def maximumMinimumPath(self, grille: List[List[int]]) -> Int:
m, n = len(grid), len(grid[0])
best = [[-1] * n pour _ dans la plage(m)]
meilleur[0][0] = grille[0][0]

# max-heap: stocker (-score, x, y) parce que le heapq est un min-heap
masse = [(-grid[0]], 0, 0)]

pendant que le tas:
neg_score, x, y = heapq.heappop(heap)
score = -neg_score

Si x == m - 1 et y == n - 1:
retour

pour dx, dy inself. - Oui.
nx, ny = x + dx, y + dy
si 0 <= nx < m et 0 <= ny < n:
nouvelle_score = min(score, grille[nx][ny])
si new_score > best[nx][ny]:
best[nx][ny] = nouveau_score
heapq.heappush(heap, (-nouvelle_score, nx, ny))
retour -1 # inaccessible – ne se produit jamais pour les entrées valides

# test de santé rapide
si __nom__ == "__main__" :
sol = Solution()
print(sol.maximumPath([[5,4,5],[1,2,6],[7,4,6]]) # 4
«» "

> **Pourquoi cette version Python est géniale* *
> *Aucune dépendance externe – seule la bibliothèque standard. *
> *`-score` astuce transforme le min-heap en un max-heap, gardant le code minimal. *
> *L'utilisation du « meilleur » comme table de mémotisation empêche de revoir les cellules avec des scores inférieurs. *

### 3.3 C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maximumMinimumPath(vecteur<vecteur<int>>& grille) {
int m = quadrillage(), n = quadrillage[0].size();
vecteur<vector<int>> meilleur(m, vecteur<int>(n, -1));
meilleure[0][0] = grille[0][0];

utilisant T = tuple<int,int,int>; // (score, x, y)
priority_queue<T> pq; // max‐heap par défaut
pq.emplace(grid[0][0], 0, 0);

dirs[4][2] = La présente directive entre en vigueur le jour suivant celui de sa publication au Journal officiel de l'Union européenne.
pendant que (!pq.vide()) {
auto [score, x, y] = pq.top(); pq.pop();

si (x == m-1 && y == n-1) retourne le score;

pour (auto& d : dirs) {
int nx = x + d[0], ny = y + d[1];
si (nx < 0) ny < 0) nx >= m) continuer;

int newScore = min(score, grille[nx][ny]);
si (NewScore > best[nx][ny]) {
best[nx][ny] = nouveau score;
pq.emplace(nouveau Score, nx, ny);
}
}
}
retour -1; // inaccessible (ne se produit pas)
}
};
«» "

> **Pourquoi cette version C++ est géniale* *
> * file d'attente prioritaire Zero-overhead – le "tuple" est emballé dans le tas. *
> *Le tableau explicite `dirs` rend la manipulation de direction cristal. *
> *L'utilisation de `min` et `max` maintient l'algorithme concis. *

---

La complexité temporelle et spatiale

Langue Complexité Remarques
C'est quoi, ça ?
Autres **Java / Python / C++** , **O(m · n log(m · n))** , Chaque cellule peut être poussée dans le tas jusqu'à 4 fois (worst-case). Autres
Mémoire **O(m · n)** Autres

Le facteur log vient des opérations de tas.
Avec `m, n ≤ 100', c'est assez rapide (4 000 logs 4 000 48 000 opérations).

---

- Oui. 4. Pièges communs (Les parties "Bad" et "Ugly")

Problème Réparer / Bonnes pratiques Autres
- C'est quoi ?
**Utiliser un min‐heap**= `priority_queue<pair<int,int>> pq;` // wrong order==Switcher vers max‐heap: `priority_queue<pair<int,int>> pq;` ou pousser des valeurs négatives. Autres
**Ignorer de meilleurs scores** Autres
**Off‐by‐one erreurs dans les limites**= Oublier `x+dx < 0` check== Toujours valider `0 ≤ nx < m` et `0 ≤ ny < n` avant d'accéder à la grille. Autres
Autres **Mutable matrix as "visited"**="grid[nx][ny]= -1`="Utilisez une matrice `meilleure` séparée ou un tableau booléen `visited`; modifier l'entrée peut être surprenant. Autres
**Utilisation de la récursion / DFS** 104. N'est pas sécuritaire pour les grandes grilles; utilisez BFS itérative. Autres

---

- Oui. 5. Variantes et extensions

Variante Comment s'adapter
C'est quoi ?
Autres **Binary Search + Union‐Find**= Recherche du seuil maximal `t` tel que les cellules ≥ `t` soient connectées. Autres
Autres Pour chaque seuil, lancez un DFS pour vérifier la connectivité; log-time *O(log(maxValue) · m·n*. Autres
**Minimum Effort Path (LeetCode 1631)**. Autres
**Arêtes pondéreuses (poids non cellulaires) **Dijkstra avec coûts de bord au lieu de coûts de nœud. Autres

---

- Oui. 6. Conseils à emporter et conseils pour stimuler la carrière

1. **Afficher l'invariant** – Dans les interviews, articulez que le max-heap vous garantit toujours de choisir le meilleur score possible jusqu'à présent.
2. **Exposer le interrupteur de la valeur maximale par rapport à la valeur minimale** – Mettre en évidence comment l'échange de la comparaison transforme un Dijkstra standard en la solution exacte.
3. **Éviter de muter l'entrée** – Gardez la grille intacte; utilisez une matrice `meilleure` pour la clarté.
4. ** Garder le code en ordre** – Utilisez des constantes d'aide ('DIRS') et des variables locales de courte durée.
5. **Benchmark mentalement** – Même si le problème est petit, discutez de la complexité asymptotique; cela montre une conscience algorithmique.

La maîtrise de ce problème démontre sa compétence en algorithmes graphiques, en structures de données et en codage minutieux, une vitrine parfaite pour les interviews techniques ou les blogs techniques.

---

### Mots clés pour référencement et base de connaissances

- "Piste minimale maximale "
- `Code de débit 1091 "
- 'Dijkstra max-heap "
- La file d ' attente prioritaire de Java "
- 'Python heapq max-heap "
- 'C++ priority_queue tuple "
- `Recherche binaire de connectivité graphique "
- Code de Leet "
- Le chemin de l'effort minimal "

N'hésitez pas à adapter l'un des extraits à votre IDE préféré ou juge en ligne. Bon codage !