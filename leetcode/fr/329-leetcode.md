---
titre: LeetCode 329. Le chemin le plus long dans une matrice -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# LeetCode 329 – Le chemin le plus long d'une matrice
> **Complexité temporelle:** *O(m × n) **Complexité spatiale:** *O(m × n)*

---

Table des matières
Lien
-- -- -- -- -- --
Déclaration du problème
Intuition et observations
Deux solutions standard en or
Java
Python
C++
SEO-Friendly Blog Post

---

Déclaration de problème (Code Leet 329)

Avec une matrice entière `m × n`, retourner la longueur du chemin le plus long.
De n'importe quelle cellule, vous pouvez vous déplacer ** vers le haut, vers le bas, vers la gauche ou vers la droite** (pas de diagonales, pas d'enroulement).
Vous ne pouvez pas revisiter une cellule dans le même chemin.

> **Exemples**
> 1. `[[9,9,4],[6,6,8],[2,1,1]] → 4` (`[1,2,6,9]`)
> 2. `[[3,4,5],[3,2,6],[2,2,1]] → 4` (`[3,4,5,6]`)
> 3. "[[1]] → 1'

> **Constraints**
> - `1 ≤ m, n ≤ 200`
> - `0 ≤ matrice[i][j] ≤ 231 − 1`

---

Intuition et observations

1. **Point de vue du graphique** – Chaque cellule est un nœud. Un bord existe d'une cellule à n'importe quel voisin avec une valeur * strictement plus grande*.
2. ** Graphique acyclique dirigé (DAG)** – La relation "large" ne garantit aucun cycle.
3. **Le chemin le plus long dans DAG** – Peut être résolu par **triage topologique** ou par **DFS + mémoisation**.
4. **Mémoisation** – Conservez le chemin le plus long à partir de chaque cellule; réutiliser les sous-problèmes qui se chevauchent.

Les deux approches les plus populaires sont :

Méthode de fonctionnement
C'est pas vrai.
DFS + Mémoization Récursivement calculer le chemin le plus long de chaque cellule; résultats de cache. Simple, naturel, facile à mettre en œuvre. Risque de débordement de cheminée sur récursion profonde (utilisation itérative ou augmentation de la limite de récursion). Autres
Tri topologique (BFS) Calculer les degrés extérieurs; peler les nœuds avec zéro degré extérieur couche par couche. Aucune récursion; peut être itérative. Un peu plus de code; plus difficile à comprendre à première vue. Autres

Les deux ont *O(m × n)* temps et espace.

---

Les solutions de code

Voici des solutions entièrement commentées, prêtes à fonctionner dans **Java, Python et C++**.
N'hésitez pas à copier-coller dans votre IDE préféré ou juge en ligne.

---

C'est pas vrai. Java – DFS + mémoisation

"Java
Importation de java.util.*;

solution de classe publique {
Int privé[] dirs = La présente directive entre en vigueur le jour suivant celui de sa publication au Journal officiel de l'Union européenne.
mémo privé int[];
Int m, n;

Augmenter le plus longtempsPath(int[][] matrice) {
i (matrix) = null. 0) retour 0;
m = longueur de la matrice; n = longueur de la matrice[0];
mémo = nouvelle int[m][n];
int best = 0;
pour (int i = 0; i < m; i++) {
pour (int j = 0; j < n; j++) {
best = Math.max(best, dfs(matrix, i, j));
}
}
le meilleur retour;
}

matrice, int r, int c) {
si [memo[r][c] != 0) retour de mémo[r][c];
int le plus long = 1; // la cellule elle-même
pour (int[] d : dirs) {
int nr = r + d[0], nc = c + d[1];
si (nr >= 0 && nr < m && nc >= 0 && nc < n &&
matrice[nr][nc] > matrice[r][c] {
la plus longue = Math.max (la plus longue, 1 + dfs (matrice, nr, nc));
}
}
mémo[r][c] = plus long; // cache le résultat
retour le plus long;
}
}
«» "

---

Python – DFS + mémoisation

'`python
de taper l'importation Liste

Solution de classe:
plus longtemps AugmenterPath(self, matrice: List[List[int]]) -> Int:
si non matrice ou non matrice[0]:
retour 0

m, n = len(matrice), len(matrice[0])
mémo = [[0] * n pour _ dans l'intervalle(m)]
dirs = [(0, 1), (1, 0), (0, -1), (-1, 0)]

def dfs(r: int, c: int) -> Int:
si mémo[r][c]:
retour mémo[r][c]
meilleure = 1
pour dr, dc en dirs:
nr, nc = r + dr, c + dc
si 0 <= nr < m et 0 <= nc < n et matrice[nr][nc] > matrice[r][c]:
best = max(meilleur, 1 + dfs(nr, nc))
mémo[r][c] = meilleur
le meilleur retour

réponse = 0
pour i dans la plage (m):
pour j dans la plage(n):
réponse = max(réponse, dfs(i, j))
réponse de retour
«» "

---

####3-C++ – Tri topologique (BFS)
*(Démontre l'approche alternative de l'éditorial LeetCode.) *

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int le plus long Augmentation du Path(vecteur<vecteur<int>>& grille) {
si (grid.vide()=" grid[0].vide() retourne 0;
int m = quadrillage(), n = quadrillage[0].size();
vector<vector<int>> outdeg(m, vector<int>(n, 0));
dirs[4][2] = La présente directive entre en vigueur le jour suivant celui de sa publication au Journal officiel de l'Union européenne.

// calcul du degré externe pour chaque cellule
pour (int r = 0; r < m; ++r) {
pour (int c = 0; c < n; ++c) {
pour (auto &d : dirs) {
int nr = r + d[0], nc = c + d[1];
si (nr >= 0 && nr < m && nc >= 0 && nc < n &&
(c)
++outdeg[r][c];
}
}
}

// couche initiale – tous les nœuds avec dépassement 0
file d'attente <pair<int,int>> q;
pour (int r = 0; r < m; ++r)
pour (int c = 0; c < n; ++c)
Si (outdeg[r][c]] 0)
q. mettre en place(r, c);

hauteur int = 0; // couches traitées
pendant que (!q.vide()) {
+hauteur;
int sz = q.size();
pour (int i = 0; i < sz; ++i) {
auto [r, c] = q.front(); q.pop();
pour (auto &d : dirs) {
int nr = r + d[0], nc = c + d[1];
si (nr >= 0 && nr < m && nc >= 0 && nc < n &&
quadrillage[nr][nc] < quadrillage[r][c]) {
si [--outdeg[nr][nc]] 0)
q.emplace(nr, nc);
}
}
}
}
hauteur de retour;
}
};
«» "

---

En C++ vous pouvez également utiliser DFS avec mémoisation, mais la version BFS élimine les problèmes de profondeur de récursion et est souvent favorisée dans les paramètres d'entretien de grande entrée.

---

L'article de blog du SEO

> *Titre: LeetCode 329 – Le plus long chemin croissant dans une matrice Java, Python, & C++ Solutions*
> *Mots-clés de focus: Le plus long chemin croissant, LeetCode 329, LeetCode 329, LetDFS mémoization, LetTraitement topologique, LetDfS

---

Message du blog

> **Le chemin le plus long vers une matrice – Maîtrisez la question d'entrevue graphique-DP**

---

C'est pas vrai. Pourquoi cette question se pose-t-elle pour les entrevues

- **Hard** mais soluble dans le temps linéaire – prouve que vous pouvez réduire un problème à un *DAG*.
- montre la compréhension de **graph traversal**, **mémousation**, **programmation dynamique** et **triage topologique**.
- Sur demande des entreprises de haute technologie (Google, Meta, Amazon, Netflix, etc.).
- Démontre la capacité de *raisonner les états* et de *réutiliser les sous-solutions*.

---

Intuition dans une coquille de noix

> Considérez la matrice comme un graphique acyclique * dirigé* (DAG) où chaque bord passe d'un nombre inférieur à un nombre supérieur.
> Le chemin le plus long est simplement le chemin le plus long de ce DAG.

---

#### 3-

Méthode Code Langue Complexité
C'est pas vrai.
**DFS + Mémoization**== Première recherche recursive de profondeur + caching=== **Java** (classique), **Python** (récursion claire)=== *O(m × n)* temps, *O(m × n)* espace===
**Traitement topologique (BFS)**

> *Cochez celui qui correspond à votre style*:
> - Récursion se sent naturel si vous êtes à l'aise avec la profondeur de la pile.
> - BFS est plus sûr sur de très grands réseaux (p. ex. 200 × 200).

---

#### 4-

- **Heure**:
- Chaque cellule est visitée une fois, et chaque bord examiné au plus une fois → `O(m × n) "
- **Espace**:
- Tableau de mémorisation ou matrice hors degré → `O(m × n)`
- Profondeur de récursion ≤ nombre de valeurs distinctes (= m × n) → encore linéaire.

---

#### 5--Pièges communs et comment les éviter

Pourquoi ça fait mal ?
C'est le cas.
**Trajectoires de recomputation**
**Utilisation `>=` Au lieu de `>`**' Permet des voisins égaux → des chemins invalides
Autres **Débordement de la pile (Java/Python)**= Récursion profonde sur la grille 200×200== Utiliser le système DFS itératif ou fixer une limite de récursion plus élevée==
** Erreurs hors-par-un dans les limites**=###############%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
**Cadre de direction de Wong**

---

- Oui. Pourquoi les intervieweurs aiment ce problème

1. **Graph‐DP hybride** – Affiche la structure sous-jacente du graphique et applique DP.
2. **Edge Cases** – matrice vide, ligne unique/colonne, toutes valeurs égales.
3. ** Discussion sur l'optimisation** – Les candidats peuvent parler de la profondeur de la récursion, du BFS itératif ou même de la mémorisation en place pour sauvegarder la mémoire.
4. **Codage Propreté** – Code bien commenté avec des noms de variables claires est un must.

---

#### 7.

Qu'est-ce que LeetCode 329 Teaches
-- -- -- -- -- --
DAG Le chemin le plus long du monde réel (résolution de dépendance, systèmes de construction). Autres
Mémotisation Réutiliser les sous-problèmes qui se chevauchent (modèle de PDD type). Autres
BFS Topological Sort (Traitement topologique) Traitement itératif du DAG, évitant les récursions. Autres

**Prochain problème à résoudre**: * (LeetCode 1339) – un autre graphique Le favori de l'interview du DP.

---

Enveloppe

- **Java, Python, C++** code fourni (prêt à courir).
- Deux stratégies éprouvées (FDS + mémoization vs Topological BFS).
- Un billet de blog SEO complet expliquant le problème, l'intuition, les pièges, et pourquoi il importe pour votre prochaine interview.

Bonne chance pour tuer LeetCode 329 et impressionner votre futur employeur! Les

---

> **Suivez-moi**: GitHub / Linked Dans / Twitter pour plus de contenu de préparation d'entrevue.
> **Tag:** `#LeetCode329 #LongeAugmentation Chemin #GraphDP #InterviewPrep #Java #Python #C++`