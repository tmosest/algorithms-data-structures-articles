---
titre: LeetCode 2128. Supprimez toutes les lignes et colonnes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Retirez toutes les lignes et colonnes – 2128 LeetCode
> **Bien, mal et mal** – Une plongée profonde dans un problème d'interview de niveau moyen avec les solutions Java, Python & C++.

---

Table des matières

Section Lien
C'est pas vrai.
Autres Aperçu du problème
Autres #Intuition
Autres Algorithme formel #algorithme
Autres #complexité
Autres Dossiers et pièges #pièges
Code – Java
Autres Code – Python
Code – C++
#goodbad
Comment cela aide votre mémoire
Prochaines étapes

> **SEO Mots-clefs** – LeetCode 2128, Remove All Ones, Row & Column Flips, solution Java, solution Python, solution C++, entretien de codage, conception d'algorithmes, préparation d'entretien.

---

- Oui. 1. Aperçu du problème <un nom="problème"></a>

**LeetCode 2128 – Enlever toutes les lignes avec les feuillets de ligne et de colonne* *

> *On vous donne une matrice binaire `m × n` `grid`. Dans une opération, vous pouvez choisir n'importe quelle ligne ou colonne et retourner chaque valeur en elle (0→1, 1→0). Return `true` s'il est possible de retirer tous les 1=1 de la grille en utilisant n'importe quel nombre d'opérations, sinon retourner `faux`. *

**Contrôles* *

* `1 ≤ m, n ≤ 300`
* `grid[i][j] 1}'

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
[[0,1,0],[1,0],[0,1],[0,1]]""true"" Flip milieu ligne → milieu colonne"
"[1,10],[0,00],[0,00]]""""false"" Aucune séquence de flips n'éclaircit tous les "1"
"[[0]]"""true"" Déjà tous les

---

- Oui. 2. Intuition <a name="intuition"></a>

La principale perspicacité est que **une fois que nous déciderons quelles colonnes retourner, nous ne pourrons plus jamais retourner une colonne** – sinon nous annulerions nos progrès dans la première rangée.

1. **Ciblez la première rangée. **
* Si une cellule de la première rangée est `1`, nous devons retourner sa colonne.
* Après avoir retourné toutes ces colonnes, la première ligne devient toutes `0`s.

2. **Les cordes deviennent simples. **
* Pour toute ligne restante, chaque élément est soit `0` ou `1`.
* Si tous les éléments d'une ligne sont les mêmes, nous pouvons retourner la ligne (si tous `1`) ou la laisser (si tous `0`).
* Si une ligne contient à la fois `0` et `1`, aucune séquence de flips ne peut le faire tous `0`s.

Ainsi, le problème se résume à un seul balayage de la matrice:
* Flip colonnes où la première ligne a un `1`.
* Vérifiez l'homogénéité de chaque rangée.

---

- Oui. 3. Algorithme formel <un nom="algorithme"></a>

«» "
1. Let m = nombre de lignes, n = nombre de colonnes.
2. Pour chaque colonne j (0 ... n-1):
si grille[0][j]] 1 :
flip colonne j // bascule chaque cellule dans la colonne j
3. Pour chaque rangée i de 1 à m-1:
pour chaque colonne j de 1 à n-1:
si grille[i][j] != [i][j-1]:
retourner false // la ligne a des valeurs mixtes
4. Retour vrai
«» "

*Flipping a column* se contente de mélanger chaque élément : «grid[i]j] = 1 - grille[i]j]».

---

- Oui. 4. Complexité <un nom="complexité"></a>

* **Heure:**
* Étape 2 visite chaque cellule une fois → `O(mn)`
* L'étape 3 visite chaque cellule une fois → `O(mn)`
* Total : "O(mn)" (soit 90 000 opérations pour les limites indiquées).

* **Espace:**
* Modifications en place, pas de tableaux supplémentaires → `O(1)` espace auxiliaire.

---

- Oui. 5. Cas de bord et pièges communs <un nom="pièges"></a>

Pourquoi ça arrive ?
- Oui.
**En supposant que nous pouvons retourner les colonnes après les lignes**. Jamais retourner une colonne après avoir manipulé la première rangée. Autres
** Erreurs hors-par-un lors de la vérification des lignes**. Comparer chaque cellule avec son prédécesseur ou simplement vérifier `allSame(row)`. Autres
Dans des langages comme Python, réassigner la grille à l'intérieur d'une fonction d'aide peut ne pas affecter la portée extérieure. Retourner la grille modifiée ou modifier en place. Autres
**Généralités d'entrée plus grandes** Conservez les boucles itératives et les changements en place. Autres

---

- Oui. 6. Code – Java <a name="java"></a>

"Java
Importer java.util.stream.IntStream;

solution de classe publique {
// Point d'entrée principal
public booléen supprimerOnes(int[][] grille) {
int m = longueur de la grille;
int n = grille[0].longueur;

// 1. Flip colonnes où la première rangée a 1
pour (int j = 0; j < n; j++) {
si [grid[0][j]] 1) {
flipColumn(j, grille);
}
}

// 2. Toute autre rangée doit être homogène
pour (int i = 1; i < m; i++) {
Int premier Val = grille[i][0];
pour (int j = 1; j < n; j++) {
si (grid[i] [j] != firstVal) {
retourner false; // valeurs mixtes
}
}
}
retourner true; // toutes les lignes homogènes
}

// Helper: retourner une colonne entière
vide privé flipColumn(int col, int[][] grille) {
pour (int ligne = 0; ligne < quadril.longueur; ligne++) {
grille[ligne][col] = 1 - grille[ligne][col];
}
}

// ----------------------------------------------------------------------
// Optionnel: harnais d'essai rapide
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
int[[]] quadrillage1 = {{0,1,0},{1,1,1},{0,1,0}};
int[[]] grid2 = {{1,1,0},{0,00},{0,00}};
System.out.println(sol.removeOnes(grid1)); // true
System.out.println(sol.removeOnes(grid2)); // false
}
}
«» "

> **Pourquoi ça marche* *
> La première boucle garantit que la première ligne est tous zéros.
> La seconde boucle vérifie chaque ligne restante est soit tous les zéros ou tous les uns; nous pouvons retourner ces lignes si nécessaire.
> La complexité est « O(mn) » et l'algorithme est entièrement en place (espace auxiliaire « O(1) »).

---

- Oui. 7. Code – Python <a name="python"></a>

'`python
de taper l'importation Liste

Solution de classe:
def supprimer Ones(self, grille: List[List[int]]) -> bool:
m, n = len(grid), len(grid[0])

1. Flip colonnes où la première rangée a 1
pour j dans la plage(n):
si grille[0][j]] 1 :
pour i dans la plage (m):
(i) [j] ^= 1 #

2. Vérifier l'homogénéité de chaque ligne (sauf la première)
pour i à portée (1, m):
première = grille[i][0]
pour j dans la plage(1, n):
si grille[i][j] != Premièrement:
Retour Faux

retour Vrai

♪ ----------------------------------------------------------------------
si __nom__ == "__main__" :
sol = Solution()
print(sol.removeOnes([[0,1,0],[1,0,1],[0,1]]) Vrai
print(sol.supprimerOnes([[1,1,0],[0,0],[0,0]]) # Faux
«» "

> **Notes pyroniques**
> • `^= 1` est un toggle propre.
> • L'algorithme est identique à la version Java – temps linéaire, espace constant.

---

- Oui. 8. Code – C++ <a name="cpp"></a>

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
bool removeOnes(vecteur<vecteur<int>>& grille) {
int m = quadrillage(), n = quadrillage[0].size();

// 1. Flip colonnes où la première rangée a 1
pour (int j = 0; j < n; ++j) {
si [grid[0][j]] 1) {
pour (int i = 0; i < m; ++i) {
(j) ^= 1;
}
}
}

// 2. Chaque rangée restante doit être homogène
pour (int i = 1; i < m; ++i) {
int first = grille[i][0];
pour (int j = 1; j < n; ++j) {
si (grid[i] [j] != premier) retourner faux;
}
}
retour vrai;
}
};

// ----------------------------------------------------------------------
// Essai rapide
/*
#incluez <iostream>
Int main() {
Solution sol;
vecteur<vecteur<int>> g1 = {{0,1,0},{1,1,1},{0,1,0}};
vecteur<vecteur<int>> g2 = {{1,1,0},{0,00},{0,00}};
<< boolalpha << sol.supprimerOnes(g1) << endl; // true
cout << boolalpha << sol.removeOnes(g2) << endl; // false
}
*/
«» "

> **C++ Faits saillants* *
> • Utilise le XOR bitwise pour basculer.
> • Garde l'empreinte mémoire minimale ('O(1)' supplémentaire).
> • La même complexité temporelle linéaire que les autres solutions.

---

- Oui. 9. Bon / Mauvais / Ugly <a name="goodbad"></a>

Aspect du bien
- C'est quoi ?
**Clarité conceptuelle**La décomposition de la première rangée de colonnes → rangées est élégante et difficile à réaliser. Si vous décommandez des opérations, vous obtenez une logique enchevêtrée. Essayer de forcer brutalement chaque sous-ensemble de flips est insensé (exponentiel). Autres
**Mise en oeuvre**=Les boucles droites, aucune récursion, facile à lire. Les erreurs dans les limites de l'index (surtout la vérification interne de la ligne) sont fréquentes. L'utilisation incorrecte d'un état mutable (p. ex. copie de la grille) peut conduire à des bogues subtils. Autres
**Performance** Aucun – l'algorithme est déjà optimal. Toute solution qui alloue un réseau booléen supplémentaire `mn` pour les cellules visitées est un gaspillage mais fonctionne toujours. Autres
**L'espace**=Les modifications en place → `O(1)` aux.=== Aucune.= Si vous stockez tous les masques flip possibles, vous faites exploser la mémoire. Autres
**Proof** La preuve que les rangées doivent être homogènes est facile mais souvent oubliée. Sauter la preuve conduit à des réponses incorrectes qui arrivent à travailler sur des échantillons. Autres

---

- Oui. 10. Réflexions finales <un nom="final"></a>

LeetCode 3078 est un grand exercice dans la décomposition **problème**. Une fois que vous comprenez la stratégie de première rangée, le reste de la matrice se comporte presque comme une tâche de reconnaissance de motif trivial. Les trois langues — Java, Python, C++ — partagent la même empreinte minimale et le même temps d'exécution linéaire, ce qui les rend adaptées aux intervieweurs qui attendent un code propre et efficace.

Si vous préparez des entrevues techniques, n'oubliez pas : ** concentrez-vous sur l'invariant de base** (première ligne → colonnes) et évitez la suringénierie. Ce simple algorithme impressionnera aussi bien les juges humains que les juges machines.

Bon codage ! C'est ce qu'il a dit.

---

### Références & Lecture supplémentaire

1. Problème de LeetCode 3078 – Éclairer tous les bits par Flipping Rows ou Colonnes.
2. Profils communs d'entrevues : *réductions par ligne ou colonne par colonne.
3. Opérations bit-wise pour basculer: XOR ('^') est l'astuce idiomatique entre les langues.

---

> **Auteur** – Votre ami LeetCode problem‐solver.
> Suivez-moi pour des explications plus concises, un code propre et des solutions prêtes à l'entrevue.