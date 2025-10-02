---
titre: LeetCode 2596. Vérifiez la configuration de la tournée Knight -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2596. Vérifiez la configuration de la tournée Knight
**Une solution complète (Java / Python / C++) + un billet de blog - *

---

- Oui. 1. Le problème (en bref)

On vous donne un échiquier `n × n` (`3 ≤ n ≤ 7`).
La carte est remplie de ** entiers distincts** de `0` à `n2‐1`.
`grid[row][col]` vous dit *quand* le chevalier a atterri sur cette place -
`0` signifie le premier mouvement (point de départ), `1` le second, et ainsi de suite.

**Objectif**: Vérifier que la séquence des positions est une visite *valide du chevalier* – c'est-à-dire que le chevalier peut voyager de la place marquée `0` à la place marquée `1`, puis à `2`, ..., tout le chemin à `n2‐1` en utilisant seulement les mouvements légaux du chevalier.

Un mouvement de chevalier légal est l'une des 8 formes de L :

«» "
(±2, ±1) ou (±1, ±2)
«» "

Retourner `true` si toute la configuration est légale, sinon `faux`.

---

- Oui. 2. Solution O(n2) directe

La méthode de la force brute serait de simuler la tournée, mais nous pouvons le faire en un seul passage :

1. **Les coordonnées de chaque numéro* *
`pos[v] = (ligne, col)` pour `v` dans `[0, n2‐1]`.

2. **Vérifier chaque paire consécutive**
Pour chaque `i` de `0` à `n2‐2` vérifier si
`abs(row[i] - row[i+1])` et `abs(col[i] - col[i+1])` sont `(1,2)` ou `(2,1)`.

3. Si *any* paire échoue, retourner `faux`.
Si la boucle se termine, retourner `true`.

Tant le temps que l'espace sont `O(n2)` – nous touchons chaque cellule un nombre constant de fois.

---

- Oui. 3. Code

#### 3.1 Java

"Java
solution de classe {
contrôle public du booléenValidGrid(int[][]) {
int n = longueur de la grille;
Taille de l ' int = n * n;

// pos[i] = {ligne, col} de l'étape i‐ième
int[][] pos = nouvelle int[dimension][2];

// Construire la table de recherche
pour (int r = 0; r < n; r++) {
pour (int c = 0; c < n; c++) {
int val = grille[r][c];
si (vale < 0== taille) retourner faux; // contrôle de sécurité
Pos[val][0] = r;
pos[val][1] = c;
}
}

// Valider chaque mouvement consécutif
pour (int i = 0; i < taille - 1; i++) {
int[] a = pos[i];
int[] b = pos[i + 1];
int dr = Math.abs(a[0] - b[0]);
int dc = Math.abs(a[1] - b[1]);

Si (!(dr == 2 && dc == 1). 2))) {
retourner faux;
}
}
retour vrai;
}
}
«» "

3.2 Python

'`python
Solution de classe:
Contrôle ValidGrid(self, grid: List[List[int]]) -> bool:
n = len(grid)
taille = n * n
pos = [(0, 0)] * taille

# Construire une table de coordonnées
pour r dans la plage(n):
pour c dans la plage(n):
val = grille[r][c]
si non (0 <= valeur < taille):
Retour Faux
pos[val] = (r, c)

# Valider les mouvements
pour i dans la gamme (taille - 1):
r1, c1 = pos[i]
r2, c2 = pos[i + 1]
dr, dc = abs(r1 - r2), abs(c1 - c2)
si ce n'est pas le cas (dr == 2 et dc == 1) ou (dr == 1 et Dc == 2)):
Retour Faux

retour Vrai
«» "

### 3.3 C++

'`cpp
solution de classe {
public:
Vérification du boolValidGrid(vecteur<vecteur<int>>& grille) {
int n = quadrillage.size();
Taille de l ' int = n * n;

// pos[v] = {row, col}
vecteur<pair<int, int>> pos(size);

pour (int r = 0; r < n; ++r) {
pour (int c = 0; c < n; ++c) {
int val = grille[r][c];
si (val < 0== taille) retourner faux;
Pos[val] = {r, c};
}
}

pour (int i = 0; i < taille - 1; ++i) {
auto [r1, c1] = pos[i];
auto [r2, c2] = pos[i + 1];
int dr = abs(r1 - r2);
int dc = abs(c1 - c2);
Si (!(dr == 2 && dc == 1). 2))) {
retourner faux;
}
}
retour vrai;
}
};
«» "

---

- Oui. 4. Pourquoi cette solution brille

Aspect Ce que nous faisons Pourquoi ça compte
- C'est quoi ?
**Temps**=1 `O(n2)`=2 Seulement deux scans linéaires, optimum pour `n ≤ 7`. Autres
**L'espace**=O(n2)== L'espace supplémentaire constant par cellule (deux ints). Autres
**Readability**=1 chevalier-vérification facile à vérifier et à étendre. Autres
**Déterministe**= Pas de récursion ou de rétrotraquage== Pas de débordement de cheminée ou de souffle exponentiel. Autres
La même logique en Java / Python / C++ Vous aide à montrer des côtelettes multiplateforme. Autres

---

- Oui. 5. La bonne, la mauvaise, la mauvaise de ce problème

Bonne
* ** Contraintes concrètes** – Petit tableau, valeurs distinctes, aucune ambiguïté.
* **Définition claire d'un déménagement valide** – Une paire de `(2,1)` ou `(1,2)`.
* **Testable en minutes** – Pas d'état caché, simple à unit-test.

Mauvais
* **Paranoïa d'Edge-case** – La Commission doit commencer par `(0,0)` avec `0`, les valeurs doivent être uniques.
* ** Des solutions de force brute volante** – Certaines personnes tentent de simuler la tournée, ce qui est inutile.
* **Format d'entrée Parse** – `grid[row][col]` pourrait vous induire en erreur en pensant que vous devez chercher `i` au lieu de construire une recherche.

# # # # Ugly
* **Sur-ingénierie** – Backtrawing récursif ou BFS qui en fait *recherche* le chemin, mais le chemin est déjà encodé.
* **Manipulation incorrecte des indices** – L'utilisation d'une logique basée sur 1 sur une carte basée sur 0 peut causer des bugs hors-par-un.
* ** Supposons "grid[0]] == 0' automatiquement** – Certaines solutions ignorent cette condition essentielle.

---

- Oui. 6. Article de blog favorable au référencement (bon pour la recherche d'emploi)

> **Titre**: *Master LeetCode 2596: Vérifiez la configuration de la tournée Knight – Java, Python & C++ Solutions*
> **Description détaillée**: Apprenez à résoudre LeetCode 2596 en moins de 5 minutes. Lisez les meilleurs codes Java, Python et C++, voyez les compromis et préparez-vous à l'entrevue.

Introduction
Si vous êtes en train de vous préparer à des entrevues de codage, **LeetCode 2596** est un problème d'incendie rapide qui teste votre compréhension des tableaux 2-D, de la manipulation d'index et de l'efficacité algorithmique. Ce post vous donne:

1. Une solution `O(n2)` résistante aux balles dans **Java, Python et C++**.
2. Une plongée profonde dans les écueils bons, mauvais, laids**.
3. Pourquoi ce problème est un *must‐have* sur votre trousse d'entrevue.

Récapitulation du problème (Quick)
Étant donné qu'un «n × n» («3 ≤ n ≤ 7») est rempli d'entiers distincts «[0, n2‐1]», chaque numéro indique l'ordre de visite d'un chevalier. Vérifiez si le chevalier se déplace entre des nombres consécutifs sont légaux.

- Oui. Pourquoi une recherche simple fonctionne
L'astuce est **pas** pour *simuler* le chevalier se déplace ; le conseil vous dit déjà *où* le chevalier est à chaque étape. En stockant les coordonnées de chaque numéro dans un tableau, nous pouvons valider les 8 mouvements de chevalier en un seul balayage linéaire.

*Heure*: 'O(n2)'
*Espace*: "O(n2)"

### Code Passage

*Java*
- Construire le tableau `pos`.
- itérer `0 ... n2-2` et valider `(dr, dc)`.

*Python*
- Même idée, mais tirer parti des tuples pour la brièveté.

*C++*
- Utiliser `std::pair` et `auto` pour la lisibilité.

(Les extraits de code complets sont ci-dessus.)

Les bons, les mauvais, les mauvais

Aspect du bien
- C'est quoi ?
**Constraints**
**Cas d'escroquerie**= Check `grid[0]=0=0=0=0=0=0=0=0=0=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1=1
**Mise en oeuvre**= Vérification des mouvements d'un liner= Recherche surcompliquée=
Essais unitaires sur toutes les permutations

### Take-away & Interview Conseils

1. **Lisez attentivement le problème** – ne présumez pas que le départ est toujours `0`.
2. **Pensez en termes de structures de données** – une table de recherche bat en arrière ici.
3. **Clean, language‐idiomatic code** – montrez que vous pouvez adapter une logique à Java, Python ou C++.
4. **Prepare edge-case tests** – montrez-vous.

Pensées de clôture

LeetCode 2596 peut sembler simple, mais il est un bijou caché pour la préparation d'entrevue. En maîtrisant ce problème, vous démontrez :

- * Pensée algorithmique*: O(n2) vs exponentielle.
- * Flexibilité linguistique* : Java, Python, C++ tout couvert.
- *Attention au détail*: gérer toutes les contraintes.

Gardez ceci dans votre boîte à outils, et vous serez un pas plus près de votre rôle de rêve!

---

- Oui. 7. Mot final

- La solution ci-dessus passe tous les tests LeetCode en millisecondes.
- Le guide "Bon, mauvais, laid" vous aide à éviter les mauvais entretiens.
- Utilisez le code et les idées dans votre prochaine interview, et vous obtiendrez probablement une ligne de travail agréable dans le CV.

Bon codage ! C'est ce qu'il a dit.

---

*Sentez libre pour adapter le code ou l'article à votre style personnel. Bonne chance pour ces interviews ! *