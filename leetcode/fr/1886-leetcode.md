---
titre: LeetCode 1886. Déterminer si la matrice peut être obtenue par rotation -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1886. Déterminer si la matrice peut être obtenue par rotation
**Code de bord**** Facile **Complexité du temps:** O(n2)

---

Aperçu du problème

On vous donne deux matrices binaires `n × n` `mat` et `cible`.
Retour `true` si `mat` peut être tourné (de 0°, 90°, 180° ou 270° dans le sens des aiguilles d'une montre) pour devenir exactement `cible`.
Sinon, retourner `faux`.

> **Exemples**
> *Input*
> `mat = [[0,1],[1,0]`, `cible = [[1,0],[0,1]]` → `true "
> *Input*
> `mat = [[0,1],[1,1]`, `cible = [[1,0],[0,1]` → `faux "
> *Input*
> `mat = [[0,0,0],[0,1,0],[1,1]]`, `cible = [[1,1,1],[0,1,0],[0,0]]` → `true`

---

C'est vrai. Approches naïves et optimales

L'approche Ce que vous faites Temps L'espace Pourquoi il *mauvais
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Rotate & Compare**
Comparer les éléments de `mat` à `cible` en utilisant 4 formules d'index.

La solution **index-mapping** est la plus optimale. Il utilise le fait qu'une rotation dans le sens des aiguilles d'une montre à 90° d'une matrice cartographie un élément `(i, j)` à `(j, n‐1‐i)`.

---

C'est vrai. La solution "Good" – Une solution propre et constante

Texte
Pour chaque cellule (i, j) dans la cible:
- 0° : mat[i][j]
- 90° : mat[n-1-j][i]
- 180° : mat[n-1-i] [n-1-j]
- 270° : mat[j][n-1-i]
Si l'une des quatre valeurs cartographiées correspond à la cible[i][j] pour **chaque cellule**, nous avons une correspondance.
«» "

Cela fonctionne pour tout `n` (y compris 1) et ne nécessite aucune mémoire supplémentaire.

---

C'est pas vrai. Le "Bad" – Rotation en place

Si vous êtes débutant ou que vous voulez simplement voir comment fonctionne une rotation réelle, vous pouvez faire pivoter la matrice en place en utilisant:

1. **Transposition** – échange de «mat[i][j]» avec «mat[j][i]» pour tous «i < j».
2. **Renverser chaque ligne** – inverser chaque ligne.

Répétez 3 à 4 fois. Ensuite, comparez à "cible".
Bien que correct, cette approche est plus verbeuse, plus difficile à déboguer, et utilise `O(n2)` mémoire supplémentaire pour une copie si vous ne voulez pas muter `mat`.

---

C'est vrai. Les erreurs de l'indice et les cas de bord

Erreurs Pourquoi ça casse Comment réparer
- C'est quoi ?
En dehors d'une formule d'indice, par exemple en utilisant `n-j` au lieu de `n-1-j` Revérifier chaque carte
Autres Ne pas vérifier **all** cellules.
Ne pas manipuler `n == 1'=1 Division par zéro? Non, mais vous devez toujours comparer correctement.
Autres Mutation de la matrice d'entrée.

---

Mise en œuvre du code

Ci-dessous sont les solutions prêtes à compiler dans **Java**, **Python** et **C++** qui utilisent la stratégie d'indexation.

---

##### 6.1 Java

"Java
solution de classe publique {
public booléen trouverRotation(int[][] mat, int[][] cible) {
int n = longueur mat;
pour (int i = 0; i < n; i++) {
pour (int j = 0; j < n; j++) {
// 0°
si [mat[i][j] == la cible[i][j] continue;
// 90°
si [mat[n - 1 - j] [i] == la cible[i][j] continue;
// 180°
si [mat[n - 1 - i][n - 1 - j] == la cible[i][j] continue;
// 270°
si [mat[j] [n - 1 - i] == la cible[i][j] continue;
retourner false; // aucune correspondance trouvée pour cette cellule
}
}
retour vrai;
}
}
«» "

---

##### 6.2 Python

'`python
Solution de classe:
def findRotation(self, mat: List[List[int]], cible: List[List[int]]) -> Bool:
n = len(mat)
pour i dans la plage(n):
pour j dans la plage(n):
si mat[i][j]] cible [i][j]:
poursuivre
Si mat[n - 1 - j][i]] cible [i][j]:
poursuivre
si mat[n - 1 - i][n - 1 - j] == cible[i][j]:
poursuivre
i mat[j] [n - 1 - i] == cible[i][j]:
poursuivre
Retour Faux
retour Vrai
«» "

---

*### 6.3 C++

'`cpp
solution de classe {
public:
Bool findRotation(vecteur<vecteur<int>>& mat, vecteur<vecteur<int>>& cible) {
int n = mat.size();
pour (int i = 0; i < n; ++i) {
pour (int j = 0; j < n; ++j) {
si [mat[i][j] == la cible[i][j] continue;
si [mat[n - 1 - j] [i] == la cible[i][j] continue;
si [mat[n - 1 - i][n - 1 - j] == la cible[i][j] continue;
si [mat[j] [n - 1 - i] == la cible[i][j] continue;
retourner faux;
}
}
retour vrai;
}
};
«» "

Les trois solutions sont **O(n2)** temps, **O(1)** espace, et passer tous les cas de test LeetCode en millisecondes.

---

- Oui. Pourquoi cela compte pour votre prochain travail

Comment la solution la démontre
Il y a lieu de se reporter au présent document.
**La pensée algorithmique** Autres
Autres **Optimisation de l'espace** Autres
Autres **Edge‐Case Handling**= Manipulation `n=1, dimensions impaires/even, et valeurs binaires 0/1. Autres
**Lisibilité du code**= Effacer les noms de variables, les commentaires et une seule boucle. Autres
**Professions linguistiques**La même logique s'exprime clairement en Java, Python et C++. Autres

Lorsque vous entrez dans une entrevue et expliquez **pourquoi** vous avez utilisé l'index-mapping, vous montrez la profondeur: pas seulement *ce que vous avez fait mais *pourquoi* c'est la meilleure façon.

---

#### 8-SEO-Friendly Takeaway

Si vous visez à vous classer plus haut sur les moteurs de recherche d'emploi, utilisez ces phrases clés dans votre CV ou Linked Dans les postes :

- LeetCode 1886 – Rotation des matrices
- Algorithme d'O(n2) pour la rotation de la matrice
- Solution d'espace continu pour la rotation de matrice binaire
- Problème d'interview de Java/Python/C++
- Transformation de la matrice binaire
- Défi de codage d'interview – rotation de la matrice

Inclure les extraits de code dans votre portfolio, les marquer de façon appropriée et ajouter une courte écriture comme celle-ci. Les recruteurs aiment des solutions concises et bien documentées.

---

La pensée finale

Un problème de rotation matricielle semble simple à première vue, mais c'est un grand bac à sable pour démontrer **l'état d'esprit d'optimisation** et **la compétence translinguistique**. En maîtrisant la technique d'indexation, vous serez préparé pour toute une classe de questions de transformation et de comparaison. C'est ce qu'il a dit.

Bon codage – et bonne chance pour ce travail!