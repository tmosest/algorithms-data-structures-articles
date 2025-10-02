---
titre: LeetCode 2639. Trouvez la largeur des colonnes d'une grille -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
La largeur des colonnes d'une grille – Une profondeur Dive Blog
> **LeetCode 2639 – Facile**
> ** Mots-clés de référence:** `LeetCode 2639`, `find colonne width grid`, `Java solution`, `Python solution`, `C++ solution`, `algorithme interview`, `emploi interview prep "

---

Présentation

Lorsque vous vous préparez à des entretiens de structure de données et d'algorithmes, vous rencontrez souvent des problèmes qui semblent simples, mais qui sont un terrain de jeu *grand* pour un codage propre, un traitement des cas de bord et une performance optimale.
LeetCode 2639 – *Trouver la Largeur des Colonnes d'une Grille* est un tel problème. Il est classé ** facile**, mais il teste votre compréhension de:

- Traversée du réseau 2-D
- Manipulation des entiers négatifs
- Conversion des chaînes par rapport au comptage des chiffres mathématiques
- L'état d'esprit de complexité du temps et de l'espace

Dans cet article, nous allons passer par les parties **good**, **bad** et **ugly** de résoudre ce problème, fournir des solutions prêtes à la copie dans **Java**, **Python** et **C++**, et vous donner des conseils prêts à l'entrevue qui stimuleront votre CV.

* * * * * *
> Pour chaque colonne, calculez la longueur maximale de chaîne de ses valeurs (les nombres négatifs obtiennent un `-` supplémentaire).
> Complexité: **O(m·n)** temps, **O(n)** espace.

---

## 2--Déclaration du problème (re-mot)

Vous recevez une matrice entière `m x n` `grid`.
Pour chaque colonne `i` (0-indexé), définir la *largeur* de la colonne comme la plus longue **représentation de chaîne** de tout entier dans cette colonne.
- Oui. Si l'entier est non négatif, sa largeur est le nombre de chiffres.
- Oui. Si l'entier est négatif, sa largeur est le nombre de chiffres **plus un** (pour le signe moins).

Retourner un tableau `ans` de longueur `n` où `ans[i]` est la largeur de la colonne `i`-th.

**Contrôles* *

Valeur du paramètre
C'est quoi ?
< 1 ≤ m ≤ 100 >
= = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =
< 109 ≤ grille[r][c] ≤ 109 '

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
La plus grande valeur dans la seule colonne est `333` (3 chiffres). Autres
[[−15, 1, 3], [15, 7, 12], [5, 6, −2] Colonne 0: `-15` → 3, Colonne 1: tous à 1 chiffre, Colonne 2: `12` et `-2` → 2.

---

- Oui. La bonne solution – une solution propre et lisible

### 3.1 Concept

1. **Initialiser** un tableau `ans` de taille `n` avec des zéros.
2. **Itérer** sur chaque colonne "j".
3. Pour chaque élément `grid[i][j]` dans cette colonne, calculer **largeur**:
- Convertir en chaîne → `len = s.length()` → Poigne le signe négatif automatiquement.
- Mettre à jour `max` si ce `len` est plus grand.
4. Entreposer `max` dans `ans[j]`.
5. Retour «ans».

Cette approche est *O(m·n* dans le temps et *O(n* dans l'espace supplémentaire.

Code (Java)

"Java
solution de classe publique {
public int[] findColumnWidth(int[][]) {
int m = longueur de la grille;
int n = grille[0].longueur;
int[] ans = nouvelle int[n];

pour (int col = 0; col < n; col++) {
int maxWidth = 0;
pour (int rang = 0; rang < m; rang++) {
int len = entier.toString(grid[row][col]).longueur();
si (lent > maxWidth) {
maxWidth = len;
}
}
ans[col] = maxWidth;
}
le retour des an;
}
}
«» "

Code 3.3 (Python)

'`python
Solution de classe:
def findColumnWidth(self, grid: List[List[int]]) -> Liste[int]:
si non grille: retourner []
m, n = len(grid), len(grid[0])
ans = [0] * n
pour le col dans la plage(n):
max_w = 0
pour la ligne de range(m):
w = len(str(grid[row][col])
si w > max_w:
max_w = w
[col] = max_w
retour et
«» "

Code 3.4 (C++)

'`cpp
solution de classe {
public:
vector<int> findColumnWidth(vecteur<vecteur<int>>& grille) {
int m = quadrillage.size();
int n = grille[0].taille();
vecteur<int> ans(n, 0);

pour (int col = 0; col < n; ++col) {
= 0;
pour (int rang = 0; rang < m; ++row) {
chaîne s = to_string(grid[row][col]); // poignées '- '
int w = s.size();
si (w > maxW) maxW = w;
}
[col] = maxW;
}
le retour des an;
}
};
«» "

Autres *Pourquoi c'est bon: *
> - **Relevable**: Effacer les noms de variables, un liner pour le calcul de la largeur.
**Idiomatique**: Utilise des fonctions de conversion de chaînes spécifiques au langage.
> - **Performance**: Pas d'opérations inutiles; seulement des traversées "O(m·n).

---

- Oui. Ce que vous devriez éviter

Mauvaise pratique
C'est pas vrai.
Utiliser `StringBuilder` ou `String` à plusieurs reprises dans les boucles serrées (Java)
En casting à `long` puis à `String` inutilement. Autres
Reliant sur `Math.log10()` ou division pour compter les chiffres.
Impossible de gérer l'entrée vide (rare, mais défensive) Erreur d'exécution sur les cas de test LeetCode. Autres

---

C'est pas vrai. Le «Ugly» – Sur-optimisé mais difficile à lire

Certains intervieweurs aiment un ** monoligne** ou un style **fonctionnel**:

"Java
public int[] findColumnWidth(int[][]) {
retour IntStream.range(0, grille[0].longueur)
.map(j -> IntStream.of(grid).map(row -> Integer.toString(row[j]).longueur()).max().getAsInt()
.à Array();
}
«» "

Bien que concis, il sacrifie:

- **Clarité** – Une personne qui lit le code peut ne pas comprendre immédiatement l'intention.
- **Debuggability** – Plus difficile à franchir.
- **Performance** – L'API de flux peut avoir caché les frais généraux.

Autres *Éviter les entretiens réels* à moins que l'intervieweur ne demande explicitement une solution fonctionnelle.

---

C'est pas vrai. Liste de contrôle des cas

Autres Décision Pourquoi il importe de savoir comment notre solution le gère
Il n'y a pas de lien entre les deux.
**Tous les nombres négatifs**=Il faut compter le signe `-` `Integer.toString()` comprend "-".
**Zero**. `0` a la longueur 1. Autres
**Maximum/minimum entier** (`±109`)= Pas de trop-plein dans la conversion de la chaîne=" ToString` poignées 32-bit ints en toute sécurité. Autres
**Ligne unique/colonne unique**=S'assurer que les limites des boucles sont correctes=Loops sur `grid.length` et `grid[0].length`. Autres
**Grande grille (100x100)**= Test de performance=O(104) opérations → temps trivial. Autres

---

Autres approches

#### 7.1 Compte des chiffres basés sur les mathématiques (Éviter les chaînes)

Si vous voulez éviter la conversion des chaînes :

"Java
nombres int(int x) {
Si (x) 0) retour 1;
Int len = 0;
si (x < 0) {
len++; // pour '- '
x = -x;
}
pendant que (x > 0) {
x/= 10;
len++;
}
retour len;
}
«» "

Cela fonctionne, mais l'approche de conversion des chaînes est *propre* et moins sujette à erreur pour la plupart des contextes d'entrevue.

#### 7.2 Utilisation d'un précalcul Largeurs

Vous pouvez pré-calculer un tableau 2-D `largeurs` de la même forme que `grid`, puis prendre la colonne maxima. Cela ajoute une mémoire inutile ('O(m·n)' supplémentaire), de sorte que cela ne vaut pas la peine pour un problème facile.

---

Analyse de complexité

L'approche Temps Espace
- C'est quoi ?
C'est une chaîne de caractères propre.
Basé sur les mathématiques
Un seul cours d'eau

Les deux approches répondent facilement aux contraintes.

---

## 9=1 Conseils d'entrevue & Points saillants

1. ** Expliquer l'idée centrale d'abord** – Nous itérer sur les colonnes et suivre la largeur maximale en utilisant la conversion de chaîne. (en milliers de dollars)
2. **Cas du bord de la Mention** – nombres négatifs, zéro, ints min/max.
3. **Parler de la complexité** – Ceci fonctionne dans le temps linéaire par rapport au nombre d'éléments. (en milliers de dollars)
4. **Afficher le code** – Fournir un extrait propre (comme ci-dessus) et demander à l'intervieweur s'il préfère une langue différente.
5. **Optionnel** – Si nous devions éviter la conversion des chaînes, nous pourrions utiliser une routine de comptage numérique. Cela démontre la profondeur.

Autres * Reprendre la balle :*
> • Conçu et mis en œuvre un algorithme O(m·n) efficace pour calculer la largeur des colonnes dans les grilles entières 2-D, gérer les valeurs négatives et les cas de bord, ce qui donne un code clair et durable à travers Java, Python et C++.

---

Conclusion

LeetCode 2639 est un problème trompeur simple qui offre une plate-forme solide pour démontrer un codage propre, une couverture complète des cas de bord et des compétences en communication par entrevue. En se concentrant sur la lisibilité et la manipulation correcte des négatifs et zéro, vous pouvez répondre à cette question dans une entrevue de codage et mettre en valeur un ensemble de compétences poli sur votre CV.

Bon codage, et bonne chance d'obtenir ce travail! C'est ce qu'il a dit.

---