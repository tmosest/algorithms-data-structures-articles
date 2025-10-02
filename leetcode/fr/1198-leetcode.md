---
titre: LeetCode 1198. Trouver le plus petit élément commun dans toutes les lignes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Code de Leet 1198 – Trouver le plus petit élément commun dans toutes les lignes
*Solve it in Java, Python and C++ – plus un billet de blog optimisé par le SEO pour atterrir cette prochaine interview d'emploi. *

---

C'est pas vrai. Le problème (copie facile-coller pour vos notes)

«» "
Avec une matrice m × n `mat` où chaque ligne est triée dans un ordre strictement croissant,
retourner le plus petit élément commun qui apparaît dans **chaque ligne**.

Si aucun élément commun n'existe, retourner -1.

Contraintes
- Oui.
- 1 ≤ m, n ≤ 500
- 1 ≤ mat[i][j] ≤ 104
- mat[i] augmente strictement
«» "

**Exemples**

Entrée Sortie
C'est quoi ?
[[1,2,3,4],[2,4,5,8,10],[3,5,7,9,11],[1,3,5,9]"
[[1,2,3],[2,3,4],[2,3,5]

---

La feuille de route de la solution « Bonne, mauvaise et mauvaise »

Aspect du bien
- C'est quoi ?
**Complexité du temps**="O(m · n · log n)" (recherche binaire par ligne) – parfaitement adapté aux contraintes.=" Si vous vérifiez naïvement chaque élément par rapport à chaque ligne (`O(m·n2)`), vous allez TLE sur 500×500. L'utilisation d'une boucle lente nichée ou d'une fonctionnalité non optimisée spécifique à la langue peut encore atteindre des limites de temps. Autres
**Complexité spatiale** Aucun – vous pouvez le garder constant. Le stockage de toutes les lignes dans un ensemble de hachages («O(m·n)») est excessif et gaspille la mémoire. Autres
**Readability** Des solutions récursives difficiles à lire. Ugly lambda hacks qui masquent l'intention. Autres
**Spécifique à la langue**=Java, Python, C++ ont toutes des bibliothèques de recherche binaire rapide. Il est préférable d'utiliser un « bisect » intégré à Python. C++ `std::binary_search` est élégant; évitez le pointeur manuel arithmétique si vous voulez la lisibilité. Autres

---

Code – trois langues

> **NOTE:** Toutes les solutions utilisent un helper qui effectue une recherche binaire sur une ligne *triée*.
> Ils s'arrêtent dès qu'ils trouvent un élément commun – le plus petit en raison de l'ordre des lignes.

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
// O(m * n * log n) temps, espace O(1)
Plus petit élément commun(int[][] mat) {
si (mat) null (longueur du tapis) 0) retour -1;

pour (int cible : mat[0]) { // candidats de la première rangée
booléen tousRowsContient = vrai;
pour (int r = 1; r < longueur mat; r++) {
si (!binarySearch(mat[r], cible)) {
tousRowsContient = faux;
pause;
}
}
si (allRowsContient) cible de retour; // premier (le plus petit) fréquent trouvé
}
retour -1; // aucun élément commun
}

privé booléen binaireRecherche(int[] arr, int cible) {
Int gauche = 0, droite = longueur d'arrondi - 1;
pendant que (gauche <= droite) {
int milieu = gauche + (droite - gauche) / 2;
si (arr[mid] == cible) retourner vrai;
si (arr[mid] < cible) gauche = milieu + 1;
autre droite = milieu - 1;
}
retourner faux;
}
}
«» "

3.2 Python

'`python
de bisect importer bisect_left
de taper l'importation Liste

Solution de classe:
Temps, espace O(1)
def le plus petit [Liste[int]]] -> Int:
Si ce n'est pas mat: retour -1

pour la cible en mat[0]: # itérer à travers la première rangée
if all(self._in_row(row, cible) pour la ligne de mat[1:]):
Objectif de retour
retour -1

@staticmethod
def _in_row(row: List[int], cible: int) -> C'est vrai.
"""La recherche binaire dans une rangée triée."""
i = bisect_left(ligne, cible)
retourner i < len(row) et row[i] == cible
«» "

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
// O(m * n * log n) temps, espace O(1)
int plus petitCommonElement(vecteur<vecteur<int>>& mat) {
si (mat.vide()) retour -1;
pour (int cible : mat[0]) { // candidats de la première rangée
bool commun = vrai;
pour (size_t r = 1; r < mat.size(); ++r) {
si (!binary_search(mat[r].begin(), mat[r].end(), cible)) {
fréquent = faux;
pause;
}
}
si (commun) cible de retour; // première (plus petite) cible trouvée
}
retour -1; // aucun élément commun
}
};
«» "

---

- Oui. Pourquoi ces solutions débarquent des emplois

Raison d'être
C'est pas vrai.
**L'utilisation de la recherche binaire**= montre la maîtrise des astuces algorithmiques classiques; efficace pour les données triées. Autres
**La séparation claire des préoccupations**=Le petit assistant (`binarySearch` / `_in_row`) améliore la lisibilité et la testabilité des unités. Autres
**Sensibilisation au temps et à l'espace**= Les interviews demandent souvent pourquoi c'est mieux? – vous pouvez expliquer "O(m·n·log n)" par rapport à "O(m·n2)". Autres
**Langue-spécifique Meilleures pratiques**=Java: `private` helper; Python: `bisect`; C++: `std::binary_search`. Autres

---

C'est pas vrai. Billet de blog – Le bon, le mauvais, et le mauvais de LeetCode 1198

> **Meta Description:**
> Master LeetCode 1198 en Java, Python, & C++ avec une analyse claire et correcte. Apprenez la recherche binaire, les compromis entre l'espace temporel et le code prêt à l'entrevue. Atterrissez votre prochain travail !

---

Titre

**Le bon, le mauvais et l'acharnement de LeetCode 1198 – Trouver le plus petit élément commun dans toutes les lignes *

5.2 Introduction

> LeetCode 1198 vous demande de trouver le plus petit élément qui apparaît dans **chaque ligne** d'une matrice triée.
> Sur la surface, il semble trivial, mais les pièges cachés peuvent vous mordre dans une interview.
> Dans ce post, nous allons disséquer le problème, marcher à travers une solution de recherche binaire propre, et explorer d'autres approches qui pourraient sembler attrayants à première vue mais finissent par être les options *bad* ou *ugly*.

5.3 Récapitulation des problèmes (avec contraintes)

Texte
- m, n ≤ 500
- mat[i][j] ≤ 104
- Chaque rangée augmente strictement
«» "

> *Pourquoi est-ce que l'augmentation stricte de la matière? * Il garantit que la recherche binaire ne frappera jamais les valeurs dupliquées qui pourraient fausser notre logique.

### 5.4 La recherche binaire par ligne

- Pourquoi ?
Chaque ligne est triée, donc vérifier si une cible existe est `O(log n)`.
Puisque nous devons vérifier le candidat par rapport à toutes les autres lignes, le coût total est `O(m · n · log n)` – bien dans les limites.

- **Points saillants du code (Java)* *

"Java
pour (int cible : mat[0]) {
booléen commun = vrai;
pour (int r = 1; r < longueur mat; r++) {
si (!binarySearch(mat[r], cible)) {
fréquent = faux; rupture;
}
}
si (commun) cible de retour;
}
«» "

- **Traitements clés**
1. **Source candidate** – Toujours itérer la première ligne; tout élément commun doit être là.
2. **Départ précoce** – Dès qu'une ligne échoue, casse – gagne du temps.
3. **Petite aide** – Garde la boucle externe propre.

#### 5.5 L'Intersection de Brute-Force

- C'est quoi ? **
Conservez chaque rangée dans un `HashSet`, puis entrecroisez tous les ensembles.
Temps: `O(m · n)` – linéaire, mais avec des frais généraux constants élevés.
Espace: 'O(m · n)' – peut atteindre 250 000 entiers (soit 1 Mo) *par langue*.

- Pourquoi c'est mauvais
1. **Extra Memory** – Les intervieweurs aiment les solutions à faible espace.
2. **Insertion Overhead** – Les ensembles de construction prennent du temps; pas strictement nécessaire parce que les lignes sont déjà triées.
3. **Edge‐Cas Complexity** – Il faut traiter soigneusement les duplicatas, même si le problème garantit l'unicité.

- **Quand ça pourrait marcher* *
Si la taille de la matrice était énorme et que vous aviez une mémoire illimitée, l'approche par hachage pourrait être acceptable, mais avec les contraintes données, la méthode de recherche binaire est plus propre.

### 5.6 L'Ugly – Boucles en nid sans recherche binaire

- À quoi ça ressemble *

'`python
pour i dans la plage (m):
pour j dans la plage(n):
# O(n) balayage linéaire sur chaque ligne
«» "

- ** Pourquoi moche**
- O(m·n2) - Quadratic, sera TLE sur 500×500.
- Difficile à lire : la double nidification obscurcit l'intention.
- Aucune garantie de sortie anticipée ou d'exploitation de la propriété triée.

- ** Piège commun**
Beaucoup de nouveaux codeurs écrivent cette solution de "simple" sans réaliser l'énorme temps de pénalité. C'est un piège d'interview classique.

#### 5.7 La langue croisée Meilleures pratiques

Recommandation Autres
- C'est pas vrai.
Utiliser un assistant privé dédié pour la recherche binaire; éviter `Arrays.binarySearch` si vous voulez montrer votre propre logique. Autres
**Python**=Leverage `bisect` module – il est C-implémenté et plus rapide qu'une boucle manuelle. Autres
**C++**= Utiliser `std::binary_search`; si vous êtes à l'aise avec les itérateurs, la bibliothèque standard est concise et rapide. Autres

####5.8 Résumé de la complexité temporelle et spatiale

L'approche Temps Espace
- C'est quoi ?
Recherche binaire par ligne **O(m · n · log n)**
**O(m · n)**
* (m · n2) * **O(1)**

> **Ligne de bottom:** L'approche de recherche binaire touche le doux point de vitesse et d'utilisation minimale de la mémoire, ce qui en fait la réponse idéale pour l'entrevue.

### 5.9 Conseils pratiques d'entrevue

1. **Exposer les contraintes tôt** – Montrez que vous lisez attentivement l'énoncé du problème.
2. **Walk Through Edge Cases** – p.ex., ligne unique, colonne unique, aucun élément commun.
3. **État de votre complexité** – Les intervieweurs aiment les candidats qui peuvent expliquer pourquoi leur solution est efficace.
4. **Afficher le code propre** – fonctions d'aide de petite taille, noms de variables significatifs (`cible`, `common`).

5.10 Réflexions finales

- **LeetCode 1198** est un exemple de manuel de *mise à profit des données triées*.
- Une solution de recherche binaire bien structurée démontre à la fois des connaissances algorithmiques et des pratiques de codage propres.
- Oui. En comprenant le bien, le mauvais, et le laid, vous serez prêt à expliquer pourquoi votre approche choisie est supérieure dans une interview réelle.

> Prêt à accepter cet entretien ? Laissez un commentaire ou partagez votre propre variante de la solution. C'est ce qu'il a dit.

### 5.11 Appel à l'action

> Si vous avez trouvé cet article utile, partagez-le sur LinkedIn ou Twitter avec le hashtag **#LeetCode1198**.
> Et restez à l'écoute pour plus de messages de Deconstruction de problèmes pour aiguiser votre bord d'entrevue de codage!

---

C'est pas vrai. Fin du blog

---

> En combinant *propres solutions algorithmiques* avec *explications axées sur l'entrevue*, vous pouvez aborder avec confiance LeetCode 1198 et impressionner les gestionnaires d'embauche dans n'importe quelle pile technologique. Bon codage !