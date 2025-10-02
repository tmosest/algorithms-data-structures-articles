---
titre: LeetCode 378. Kth plus petit élément dans une matrice triée -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 378. Kth plus petit élément dans une matrice triée

**Complexité temporelle** – 'O(n log(max Val-minVal) "
**Complexité spatiale** – « O(1) » (hors matrice d'entrée)

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++** qui utilisent la technique binaire de recherche sur valeur.

---

- Oui. 1. Solution Java

"Java
Importation de java.util.*;

solution de classe {
public int kthSmallest(int[][] matrice, int k) {
int n = matrice. longueur;
long bas = matrice[0][0];
longueur élevée = matrice[n - 1][n - 1];

pendant que (faible < haut) {
long milieu = faible + (élevé - faible) / 2;
nombre int = nombreLessEqual(matrix, milieu, n);

si (compte < k) {
faible = milieu + 1; // besoin de plus grands nombres
} autre {
haute = moyenne; // moyenne pourrait être la réponse
}
}
retour (int) faible;
}

*** Compter le nombre d'éléments <= cible dans la matrice triée */
Int privé countLessEqual[][] matrice, cible longue, int n) {
nombre int = 0;
ligne int = n - 1, col = 0; // commencer par le bas– gauche
pendant que (ligne >= 0 && col < n) {
si (matrix[ligne][col] <= cible) {
nombre += ligne + 1; // tous les éléments ci-dessus sont également <= cible
col++;
} autre {
ligne...
}
}
le nombre de retours;
}
}
«» "

---

- Oui. 2. Solution Python 3

'`python
de taper l'importation Liste

Solution de classe:
def kthSmallest(self, matrix: List[List[int]], k: int) -> Int:
n = len(matrix)
faible, élevé = matrice[0][0], matrice[-1][-1]

alors que faible < élevé:
milieu = (faible + élevé) // 2
si self._count_le(matrix, mi, n) < k:
faible = milieu + 1
Sinon:
haute = moyenne
retour faible

def _count_le(self, matrix: List[List[int]], cible: int, n: int) -> Int:
"""Nombre de retours d'éléments <= cible."""
cnt, rang, col = 0, n - 1, 0 # coin inférieur gauche
pendant la ligne >= 0 et col < n:
si matrix[row][col] <= cible:
cnt += ligne + 1 # tous les ci-dessus sont <= cible
+= 1
Sinon:
ligne -= 1
retour cnt
«» "

---

- Oui. 3. Solution C++

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
int kthSmallest(vecteur<vecteur<int>>& matrice, int k) {
int n = matrice.size();
long long bas = matrice[0][0];
longue longue haute = matrice[n-1][n-1];

pendant que (faible < haut) {
long moyen = faible + (élevé - faible) / 2;
si (compteLE(matrice, milieu, n) < k)
faible = milieu + 1;
Autre
haute = moyenne;
}
retourner static_cast<int>(faible);
}

particulier:
// Nombre d'éléments <= cible
int countLE(const vector<vector<int>>& matrix, longue cible, int n) {
int cnt = 0, ligne = n-1, col = 0; // coin inférieur gauche
pendant que (ligne >= 0 && col < n) {
si (matrix[ligne][col] <= cible) {
cnt += ligne + 1; // tous les éléments ci-dessus sont également <= cible
+col;
} autre {
--row;
}
}
retour cnt;
}
};
«» "

---

- Oui. 4. Article de blog – Le bon, le mauvais, et l'atroce de LeetCode 378

> **Titre:** *Le plus petit élément d'une matrice triée – le bon, le mauvais et le mauvais*
> **Mots clés:** LeetCode 378, Kth plus petit élément, Java, Python, C++, Matrice de recherche binaire, Codage d'entrevue, Algorithme Design, Conseils d'entrevue

---

Introduction

LeetCode 378 – *L'élément le plus petit d'une matrice triée* – est une base d'entrevues techniques.
Il vous force à penser au-delà de la force brute, mélangeant ** recherche binaire** avec **matrix traversal**.

Dans cet article, nous disséquons le problème, présentons **clean code** en Java, Python et C++, et plongeons dans les aspects *good*, *bad* et *ugly* qui peuvent voyager même les développeurs chevronnés.

---

Récapitulation des problèmes

On vous donne une matrice `n × n` où **chaque ligne et colonne est triée** en ordre ascendant.
Retourner l'élément **k‐th le plus petit** dans la matrice (compter les duplicatas).
Contraintes: `1 ≤ n ≤ 300`, les valeurs peuvent varier de `-109` à `109`.

Principale exigence: **Mémorie < O(n2)** – vous ne pouvez pas aplatir la matrice dans une liste.

---

## Le bon – Pourquoi la recherche binaire sur la valeur fonctionne

1. **Élégant** – Nous traitons la matrice comme un ... ..trié de nombres par leur **valeur** plutôt que de position.
2. **Pas d'espace supplémentaire** – Seulement quelques variables entières; O(1) mémoire auxiliaire.
3. **Fast** – temps "O(n log(maxVal - minVal)". Pour les entiers 32 bits typiques, le terme log est d'environ 31–32, donc il est pratiquement linéaire dans `n`.
4. **Déterministe** – Pas de file d'attente prioritaire; vous n'avez jamais à stocker plus de pointeurs `O(n)`.
5. **Évoluable** – Fonctionne pour la contrainte supérieure `n = 300` confortablement (soit 9 000 éléments).

---

Le mauvais – ce qui le rend difficile

Sujet Pourquoi cela importe
- C'est quoi ?
Autres **La portée des valeurs**= `maxVal - minVal` peut être énorme (`2·109`), de sorte que la boucle de recherche binaire exécute beaucoup d'itérations si nous utilisons un arithmétique naïf = (faible + élevé)/2= avec des ints 32 bits.==Utilisez 64 bits (`long`/`long`) pour éviter le débordement. Autres
**Duplicats**La matrice peut contenir des nombres répétés; l'algorithme doit gérer -k‐th plus petit, y compris des duplicatas, et non des valeurs distinctes. L'aide au comptage compte tous les éléments ≤ mi; des duplications augmentent automatiquement le nombre. Autres
**Cas d'Edge**=Les matrices à éléments uniques, les nombres négatifs, k = 1 ou k = n2.==Les pointeurs de départ et d'extrémité initialisés aux angles de matrice réels; la boucle s'éteint lorsqu'elle est "faible". Autres
**Performance**Le calcul ≤ milieu est la peritération "O(n)". La routine de comptage va du bas à gauche au haut à droite en un seul passage. Autres

---

## - Le lamentable – Pièges communs et comment les éviter

1. **Off‐par‐un dans la recherche binaire**
*Mostake*: Utiliser `tandis (faible < élevé)` mais régler `faible = milieu` ou `haut = milieu` incorrectement.
*Fix*: Quand `compte < k`, définir `faible = milieu + 1`. Dans le cas contraire, définir `haut = milieu`.

2. **Excédent total**
*Mission*: `mid = (faible + élevé) / 2` avec des ints 32 bits peuvent déborder.
*Fix*: `mid = faible + (élevé - faible) / 2` ou utiliser des types 64-bit.

3. **Logique du compte d'erreur**
*Mostake*: Augmentation du nombre par 1 chaque fois que vous voyez un élément ≤ milieu.
*Fix*: Parce que nous commençons à gauche en bas, chaque fois que nous déplaçons à droite, *tous les éléments de cette colonne jusqu'à la ligne actuelle sont ≤ milieu. Alors ajoutez `row + 1`.

4. **En supposant que la matrice est carrée* *
*Mistake*: Certaines solutions supposent `matrix.longueur= matrice[0].longueur`.
*Fix*: Utilisez `n = matrix.size()` seulement après avoir confirmé que la matrice n'est pas vide.

5. **Non-traitement des nombres négatifs**
* Mission*: Initialisation `bas` et `haut` à 0 au lieu des coins réels.
*Fix*: Toujours définir `low = matrix[0][0]`, `high = matrix[n-1][n-1]` – cela fonctionne aussi pour des valeurs négatives.

---

Code complet

- Oui. 1. Java

- Utiliser `long` pour `faible/élevé/milieu`.
- Compter les marches des aides **bottom‐gauche → haut à droite**.
- Les commentaires expliquent chaque étape.

- Oui. 2. Python

- Utilisations intégrées `int` (non limitées), donc le débordement n'est pas un problème.
- Toujours prudent avec la logique `faible = milieu + 1`.

- Oui. 3. C++

- Utilise "long long" pour la plage de valeurs.
- `countLE` utilise le même tour de fond gauche.

---

Autres approches

L'approche La complexité Quand utiliser
C'est pas vrai.
**Min-Heap (extraction de k-times)**="O(n log n)` time, `O(n)` space=" Simple à mettre en œuvre si vous êtes à l'aise avec les files d'attente prioritaires. Bon pour l'interview, mais moins élégant. Autres
**Flatten + nth_element (C++)**= L`espace `O(n2)` → viole les contraintes== uniquement lorsque l`intervieweur détend les limites de mémoire. Autres

---

Comment ces solutions vous aident à trouver un emploi

- **Showcase Algorithmic Thinking** – La recherche binaire sur la valeur démontre une compréhension profonde de la structure des données invariantes.
- **Cross‐Language Mastery** – Les implémentations Java, Python et C++ montrent que vous pouvez vous adapter à n'importe quelle pile technologique.
- **Performance-First Mindset** – L'espace O(1) et le temps O(n log) illustrent un état d'esprit prêt à la production.

**Conseil d'entrevue :**
Quand on lui a demandé de résoudre 378, d'abord décrire l'idée, puis parler à travers la logique du compte, et enfin présenter le code. Mentionnez l'exigence de mémoire O(1) et l'astuce de marcher du coin inférieur gauche. *

---

Conclusion

LeetCode 378 est plus qu'un test de recherche binaire, c'est un test de raisonnement prudent, de manipulation des frontières et de codage propre.
Maîtriser cette bonne, mauvaise, laid (analyse) n'impressionnera pas seulement les gestionnaires d'embauche, mais vous donnera également confiance pour aborder un large éventail de problèmes d'entrevue.

Joyeux codage, et que votre k-th plus petit élément atterrisse toujours sur le travail que vous êtes après! C'est ce qu'il a dit.

---

*Sentez libre de copier les extraits de code dans votre IDE préféré, exécutez les cas de test officiel, et partagez cet article avec des pairs qui préparent leur prochaine entrevue. *