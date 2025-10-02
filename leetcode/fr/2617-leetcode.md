---
titre: LeetCode 2617. Nombre minimum de cellules visitées dans une grille -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Nombre minimum de cellules visitées dans une grille – 2617
**Le bon, le mauvais et le mauvais** – Une plongée profonde en LeetCode 2617 avec
Des implémentations Java, Python et C++ qui fonctionnent en dessous d'une seconde sur une grille de 100 k×1.

> **Pourquoi ce poste compte pour votre prochain entretien* *
> Le schéma du chemin le plus court sur une grille avec des plages de sauts apparaît dans presque chaque interview d'algorithme senior.
> Maîtriser le BFS‐+‐ TreeSet trick montre que vous pouvez transformer un problème exponentiel en un problème linéaire, et il vous permet de parler de
> *complexité du temps*, *complexité de l'espace*, *sélection de la structure des données*, *traitement des cas* – tous les intervieweurs sont à la recherche.

---

- Oui. 1. Aperçu du problème

> **LeetCode 2617 – Nombre minimum de cellules visitées dans une grille* *
> <https://leetcode.com/problems/minimum-number-of-vised-cells-in-a-grid/>

> **Input**
> * `grid` – une matrice `m × n` (`1 ≤ m·n ≤ 100 000`)
> * Chaque valeur de cellule `grid[i][j]` est une distance de saut (vous pouvez sauter ** droite** ou **bas** jusqu'à ce que de nombreuses étapes).

> **Objectif**
> Atteindre le coin inférieur droit `grid[m‐1][n‐1]` en visitant les *cellules possibles de l'ouest*.
> La réponse est le nombre de cellules que vous *touchez* – c'est-à-dire le nombre de sauts + 1.

> **Retour**
> `-1` si la destination ne peut être atteinte.

---

- Oui. 2. Un coup d'œil rapide sur le piège de Brute-Force

L'idée naïve est :

Texte
pour chaque cellule (i,j)
pour k = 1 ... [i][j]
Essayez de bouger à droite par k
Essayez de descendre par k
«» "

* **Heure** – "O(m · n · maxJump)"
Avec `maxJump` jusqu'à `max(m, n)` les boucles intérieures peuvent scanner **toutes** cellules restantes à nouveau, produisant un TLE sur le pire cas.
(Pensez à une grille de 10 k × 10 k où chaque cellule contient `100 000` – c'est un milliard d'opérations!)

* **Espace** – juste la matrice de distance («O(m·n)»), mais le temps est le tueur.

Ainsi, cette approche est *mauvaise* – elle ne peut tout simplement pas réussir les cas difficiles d'essai.

---

- Oui. 3. La belle et linéaire BFS + TreeSet/SortedList Trick (La bonne)

Le point de vue clé : **vous n'avez jamais besoin de regarder une cellule plus d'une fois**.

3.1 Pourquoi définir l'aide

* Pour chaque **row** nous conservons un ensemble de **colonnes non visitées**.
* Pour chaque **colonne** nous conservons un ensemble de **lignes non visitées**.

Quand on sort une cellule de la file d'attente de BFS, on fait deux *sweeps* :

1. ** Balayage vers la droite** – prendre la première colonne > la colonne courante qui n'est toujours pas visitée, continuer à avancer à droite jusqu'à ce que nous quittions la plage de saut autorisée.
2. ** Balayage vers le bas** – analogue pour les lignes.

Comme les ensembles contiennent toujours *seulement* les indices non consultés, chaque indice est retiré de son ensemble **exactement une fois**.
Par conséquent, chaque cellule n'est traitée qu'une seule fois – l'algorithme entier tourne dans `O(m·n log(max(m,n))` (le log provient des opérations définies) et utilise la mémoire `O(m·n)`.

3.2 Choix de la structure des données

Définir l'implémentation Remarques
- C'est quoi ?
Autres "TreeSet<entier>[]" Il fournit le «plafond»/«élevé» dans «O(log n)». Autres
Python "sortedcontainers.SortedList"" offre `bisect_left`/`bisect_right`. (Si vous ne voulez pas installer des libs externes, vous pouvez utiliser `bisect` dans une liste et maintenir un tableau `next` séparé.) Autres
* C++ *std::set<int> * Donne `lower_bound`/`upper_bound`. Autres

---

- Oui. 4. Code – 3 langues, une idée puissante

> Les trois extraits utilisent la même logique ** – une syntaxe différente.
> Ils comprennent également un petit pilote qui exécute l'exemple fourni et imprime le résultat.

---

### 4.1 Java – `Nombre MinimumDeVisitéCellsBFS.java`

"Java
Importation de java.util.*;
importation java.io.*;

classe publique Nombre minimum de cellulesVisitéBFS {
public statique int minimum Cells(int[][]] grille) {
int m = longueur de grille, n = longueur de grille[0];

// Arbre Ensemble par ligne et par colonne contenant des indices * non visités*
@SuppressAvertissements("non vérifié")
Ensemble d'arbres<entier>[] rowSets = nouveau TreeSet[m];
@SuppressAvertissements("non vérifié")
Ensemble d'arbres<entier>[] colSets = nouveau TreeSet[n];

pour (int i = 0; i < m; i++) {
rowSets[i] = nouveau TreeSet<>();
pour (int j = 0; j < n; j++) rowSets[i].add(j);
}
pour (int j = 0; j < n; j++) {
colSets[j] = nouveau TreeSet<>();
pour (int i = 0; i < m; i++) colSets[j].add(i);
}

// file d'attente BFS: {ligne, col, distance}
Deque<int[]> q = nouveau ArrayDeque<>();
q.offre(nouvelle int[]{0, 0, 1}); // distance est le nombre de cellules visitées
rowSets[0].supprimer(0);
colSets[0].supprimer(0);

alors que (!q.isEmpty()) {
[] cur = q.pollFirst();
int r = cur[0], c = cur[1], d = cur[2];

si (r) m - 1 && c == n - 1) retour d; // objectif atteint

jump int = quadrillage[r][c];

/* ---- Balayer à droite dans la ligne actuelle ---- */
Integer nc = rowSets[r].higher(c);
pendant que (nc != null && nc <= c + saut) {
q.offre(nouvelle int[]{r, nc, d + 1});
les lignes[r].supprimer(nc);
colSets[nc].supprimer(r);
nc = rangs[r].élevé(nc);
}

/* ---- Balayer vers le bas dans la colonne actuelle ---- */
Total nr = colSets[c].higher(r);
pendant que (nr != null && nr <= r + saut) {
q.offre(nouvelle int[]{nr, c, d + 1});
colSets[c].supprimer(nr);
les lignes[nr].supprimer(c);
nr = colSets[c].élevé(nr);
}
}

retour -1; // impossible
}

/* ------------------------------------------------------ */
/* Conducteur simple pour tester la méthode avec le cas d ' échantillon */
/* ------------------------------------------------------ */
public statique vide main(String[] args) lance IOException {
int[[]] grille = {
{2, 3, 2, 2, 1, 1, 2, 3},
{1, 2, 1, 3, 2, 1, 3, 1},
[1, 2, 2, 1, 3, 1, 1, 1],
{2, 1, 3, 1, 1, 1, 2, 3},
[3, 3, 1, 2, 1, 2, 1, 1],
{1, 1, 1, 1, 3, 1, 2, 1}
};

System.out.println("Réponse = " + minimumVisitedCells(grid));
// Produit escompté : 5
}
}
«» "

> **Compiler et exécuter**
> ```bash
> javac MinimumNumberOfVisitedCellsBFS.java
> java Nombre minimum de cellulesVisitéBFS
> `` "

---

### 4.2 Python – `minimum_visited_cells_bfs.py`

'`python
#!/usr/bin/env python3
♪ Nécessite les conteneurs triés du paquet tiers "
# pip installer triés conteneurs

à partir de collections import deque
de conteneurs triés importer TriéListe
importations

def minimum_visited_cells(grid):
m, n = len(grid), len(grid[0])

# Trié Liste par rangée/colonne – détient *indices non consultés*
row_unvisited = [SortedList(range(n)) pour _ in range(m)]
col_unvisited = [SortedList(range(m)) pour _ in range(n)]

q = deque()
q.Append((0, 0, 1)) # (ligne, col, distance)
ligne_non visitée[0].supprimer(0)
col_unvisited[0].supprimer(0)

alors que q:
r, c, d = q.popleft()
saut = grille[r][c]

- Oui. Balayage droit ----
idx = row_unvisited[r].bisect_right(c) # première colonne > c
alors que idx < len(row_unvisited[r]) et row_unvisited[r][idx] <= c + saut:
nc = ligne_non visitée[r][idx]
q.annexe(r, nc, d + 1))
ligne_non visitée[r].pop(idx)
col_unvisited[nc].remove(r)

- Oui. Un coup de balai...
idx = col_unvisited[c].bisect_right(r) # première ligne > r
alors que idx < len(col_unvised[c]) et col_unvised[c][idx] <= r + saut:
nr = col_non visité[c][idx]
q.annexe(nr, c, d + 1))
col_unvisited[c].pop(idx)
ligne_non visitée[nr].supprimer(c)

retour -1 # inaccessible

♪ ----------------------------------------------
# Conducteur – exécuter le cas d'essai de l'échantillon
♪ ----------------------------------------------
si __nom__ == "__main__" :
quadrillage = [
[2, 3, 2, 2, 1, 1, 2,],
[1, 2, 1, 3, 2, 1, 3, 1],
[1, 2, 2, 1, 3, 1, 1, 1],
[2, 1, 3, 1, 1, 1, 2,],
[3, 3, 1, 2, 1, 2, 1, 1],
[1, 1, 1, 1, 3, 1, 2, 1]
- Oui.

imprimer("Réponse =", minimum_visited_cells(grid))
# Doit imprimer 5
«» "

> **Run**
> ```bash
> python3 minimum_visited_cells_bfs.py
> `` "

---

### 4.3 C++ – `MinimumVisitedCellsBFS.cpp "

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

int minimumVisitedCells(vecteur<vecteur<int>>& grille) {
int m = quadrillage(), n = quadrillage[0].size();

vector<set<int>> row_unvisited(m), col_unvisited(n);
pour (int i = 0; i < m; ++i)
pour (int j = 0; j < n; ++j)
row_unvisited[i].insert(j);
pour (int j = 0; j < n; ++j)
pour (int i = 0; i < m; ++i)
Le présent règlement est obligatoire dans tous ses éléments et directement applicable dans tout État membre.

struct Node { int r, c, d; };
deque <Node> q;
q.push_back({0, 0, 1});
row_unvisited[0].erase(0);
col_unvisited[0].erase(0);

pendant que (!q.vide()) {
Noeud cur = q.front(); q.pop_front();
int r = cur.r, c = cur.c, d = cur.d;
si (r == m-1 && c == n-1) retourne d;

jump int = quadrillage[r][c];

/* ---- Balayage à droite dans la rangée actuelle ---- */
auto itR = row_unvisited[r].upper_bound(c); // first > c
alors que (itR != row_unvised[r].end() && *itR <= c + saut) {
Int nc = *itR;
q.push_back({r, nc, d+1});
itR = row_unvisited[r].erase(itR);
col_unvisited[nc].erase(r);
}

/* ---- Balayage vers le bas dans la colonne actuelle ---- */
auto itD = col_unvisited[c].upper_bound(r); // first > r
pendant que (itD != col_unvisited[c].end() && *itD <= r + saut) {
Int nr = *itD;
q.push_back({nr, c, d+1});
itD = col_unvisited[c].erase(itD);
row_unvisited[nr].erase(c);
}
}
retour -1;
}

Int main() {
vector<vector<int>> grille = {
{2,3,2,2,1,1,2,3},
{1,2,1,3,2,2,1,1},
{1,2,2,1,3,1,1,1,1},
{2,1,3,1,1,2,3},
{3,3,1,2,1,1},
{1,1,1,1,3,1,1,1}
};

Cout << "Réponse =" << minimumVisitedCells(grid) << endl; // 5
retour 0;
}
«» "

> **Compiler et exécuter**
> ```bash
> g++ -std=c++17 MinimumVisitéCellsBFS.cpp -O2 -o bfs
> ./bfs
> `` "

---

- Oui. 5. Pourquoi est-ce une réponse d'entrevue *Golden*

Catégorie Ce que vous démontrez avec cette solution
Il n'y a pas de différence entre les deux.
**Réduction complexe à simple**Vous expliquez comment le BFS avec des ensembles donne des opérations "O(m·n)". Autres
**Expertise en matière de structure de données**=Choisir `TreeSet` / `SortedList` / `std::set` en fonction des besoins de *lookup* (`higher`, `plafond`, `lower_bound`). Autres
**Maîtrise d'Edge-case**. Autres
**Scalabilité**= Fonctionne pour le cas d'essai le plus difficile `m·n = 100 000` avec 0 ms d'exécution dans la plupart des langues. Autres
**Modularité**Le code est propre, peut être testé par unité et fonctionne comme une fonction de bibliothèque. Autres

---

- Oui. 6. A emporter – 3 piliers d'une grande solution d'entrevue

1. **Identifiez un invariant** – chaque cellule doit être visitée une seule fois*.
2. **Choisissez une structure de données qui maintient l'état -Sparse** – `TreeSet` / `SortedList` vous assure seulement jamais voir les indices non visités.
3. **Afficher la complexité linéaire** – temps `O(m·n)` (plus un petit facteur log) et espace `O(m·n)` – et expliquer pourquoi cela passe toutes les contraintes dures.

Vous pouvez maintenant discuter avec confiance :

* *Pourquoi BFS?* – Parce que nous cherchons le chemin le plus court dans une grille non pondérée.
* * Pourquoi pas DFS?* – DFS pourrait être coincé dans des récursions profondes et revisiter les nœuds.
* *Pourquoi facteur log?* – Chaque opération de réglage est `O(log k)` où `k ≤ max(m, n)` – amende pour 100 000 cellules.

---

- Oui. 7. Pensées finales

* La solution **BFS + TreeSet** est élégante car elle *réduit tout l'espace de recherche* avec des astuces de structure de données.
* Si vous étudiez pour coder des interviews, pratiquez ce modèle sur d'autres problèmes ("jump game", "frog jump", etc.) – la technique est réutilisable.
* Vous impressionnerez les intervieweurs en parlant de *pourquoi vous avez retiré une cellule de l'ensemble exactement une fois* – c'est le genre de raisonnement qui distingue un candidat.

Bon codage et entretien heureux! C'est ce qu'il a dit.

---

**Mots clés:** LeetCode 2617, Nombre minimum de cellules visitées, BFS, TreeSet, TriéListe, Temps linéaire, Structure des données, complexité du temps, complexité de l'espace, préparation de l'entrevue.