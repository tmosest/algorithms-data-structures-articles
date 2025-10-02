---
Titre: LeetCode 2248. Intersection de multiples tableaux -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 2248 – Intersection de tableaux multiples
*Python de Java – 3 solutions complètes*
*Blog – Bon, mauvais et ingrat de ce problème facile (friendly SEO pour les demandeurs d'emploi)*

---

Récapitulation du problème (Code de débit 2248)

> **Intersection de tableaux multiples**
> **Difficulté :** *Facile*
> **Signature (Java):** "liste publique<integer> intersection(int[][] nombres);"

On vous donne un tableau 2-D `nums`.
Chaque `nums[i]` est un tableau non vide de ** entiers positifs distincts**.
Retourner une liste triée des entiers qui apparaissent dans **chaque** tableau de "nums".

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
Seulement 3 et 4 apparaissent dans les trois tableaux
Aucun élément commun

**Contrôles* *

* `1 ≤ longueur nominale ≤ 1000`
* `1 ≤ somme(nums[i].longueur) ≤ 1000`
* `1 ≤ nombres[i][j] ≤ 1000`
* Tous les nombres à l'intérieur d'un seul tableau sont distincts.

---

Idée de base

Comme la valeur maximale d'un élément est **1000**, un tableau *fréquence* de taille `1001` suffit.
Pour chaque nombre, nous gardons un compteur de combien de tableaux il est apparu.
Après le traitement de tous les tableaux, nous recueillons des nombres dont le compteur est égal à "nums.length".

Cela donne **O(total_elements)** temps et **O(1)** mémoire supplémentaire (1001 entiers).

Autres approches:
* ** Interconnexion d'ensemble** (HashSet) – propre mais légèrement plus lourd sur la mémoire/temps.
* **Trier** chaque tableau et effectuer une fusion multipointer – inutile pour ces contraintes.

---

Les solutions de code

Voici trois solutions autonomes en Java, Python et C++.

C'est pas vrai. Java – Array de fréquence

"Java
Importation de java.util.*;

solution de classe {
liste publique<integer> intersection(int[][] nombres) {
Liste du résultat <entier> = nouvelle liste de distribution<>();
int[] freq = nouvelle int[1001]; // indice 0 non utilisé (valeurs commençant à 1)

pour (int[] arr : nombres) {
pour (int val : arr) {
freq[val]++; // nombre d'apparence par tableau
}
}

pour (int i = 1; i <= 1000; i++) {
Si (freq[i] == longueur nums.) {
résultat.add(i);
}
}
le résultat du retour;
}
}
«» "

> **Complexité temporelle :** "
> **Complexité spatiale:** `O(1)` (fixé 1001 int)

#### 2--Python – Compteur (réseau de fréquences via liste)

'`python
de taper l'importation Liste

Solution de classe:
def intersection(self, nombres: Liste[Liste[int]]) -> Liste[int]:
freq = [0] * 1001 # valeurs 1..1000

pour les nombres:
pour la valeur en arr:
freq[val] += 1

retour [i pour i dans l'intervalle(1, 1001) si freq[i] == len(nums)]
«» "

#### $ C++ – Tableau de fréquence

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
vectorielle<int> intersection(vecteur<vector<int>>& nombres) {
vecteur<int> freq(1001, 0); // indices 0,100
pour (auto &arr : nombres) {
pour (int val : arr) freq[val]++; // nombre par tableau
}
vecteur <int> ans;
pour (int i = 1; i <= 1000; ++i)
si (freq[i] == nums.size()) ans.push_back(i);
le retour des an;
}
};
«» "

Les trois implémentations sont **O(totalElements)** et produisent une liste triée d'entiers communs.

---

Article sur le blog – C'est un problème de LeetCode

> **SEO Mots-clés:** *LeetCode Intersection of Multiple Arrays*, *Java intersection solution*, *Python intersection arrays*, *C++ intersection problem*, *job interview coding*, *algorithm interview questions*, *fréquent interview problem*, *array intersection tutorial*

---

### La bonne: Pourquoi ce problème est une Goldmine pour la préparation d'entrevue

1. **Simplicité, pourtant profonde connaissance* *
Le problème semble trivial, mais il vous force à penser à *structures de données* qui équilibrent vitesse et mémoire.
Choisir la bonne approche (tableaux de fréquences vs. jeu vs. tri) démontre la compréhension des compromis temps/espace — une compétence d'entrevue clé.

2. ** Contraintes claires vous permettent d'optimiser**
Avec `max(nums[i][j]) = 1000`, vous pouvez exploiter un tableau de fréquences délimité.
En mettant en évidence cette optimisation, vous pouvez lire les contraintes et adapter votre algorithme en conséquence.

3. **Produits déterministes**
L'exigence de la liste triée est un petit détail, mais important, qui teste votre attention au détail, une autre base d'entrevue.

4. **Cohérence linguistique* *
Avoir des solutions de travail en Java, Python et C++ démontre la capacité d'adaptation et la transférabilité de code, que les gestionnaires d'embauche aiment.

---

### Les mauvaises: pièges communs et comment les éviter

Pourquoi ça arrive ?
- Oui.
**L'utilisation d'un ensemble pour chaque tableau et l'intersecting à plusieurs reprises**= Pensée que l'intersection du jeu de caractères est toujours plus rapide== Les opérations de réglage sont `O(n)` mais avec des constantes plus grandes; plus vous attribuez de nouveaux ensembles à chaque fois. Autres
**Ignorer la garantie de "distinct"** en supposant des duplications à l'intérieur d'un seul tableau. Autres
**Il s'agit de l'ensemble du tableau de taille 1001**. Autres
**Retourner une liste non triée**= Oublier de trier ou d'utiliser un conteneur non commandé== Trier le vecteur/liste final ou l'itérer en ordre croissant (comme dans le tableau de fréquences). Autres

- Oui. L'horrible : les cas de bord qui peuvent vous faire trébucher

1. **Intersection d'étendue**
Quand aucun nombre n'apparaît dans chaque tableau, vous devez retourner une liste vide. Une mauvaise vérification du compteur (par exemple, `== longueur des nums - 1`) produirait une mauvaise réponse.

2. **Grand nombre de tableaux par rapport aux petits éléments totaux**
"nums.longueur" peut être jusqu'à 1000, mais la somme de tous les éléments est également limitée par 1000.
Une approche naïve qui construit une carte pour chaque élément pourrait encore passer, mais il est inutile. Optimisez les limites données.

3. **Formation d'entrée en différentes langues* *
En C++, vous devez être prudent avec `vector<vector<int>>& nums` vs. `vector<vector<int>> nums` pour éviter les copies.
En Java, utiliser `int[]` est très bien, mais vous devez vous rappeler que `int` est primitif; pas de boxe au-dessus.

---

### SEO–Résumé optimisé

Si vous préparez une entrevue de codage, le **LeetCode 2248 – L'intersection de plusieurs tableaux** est un problème à résoudre*.
C'est une vitrine parfaite de:

* Utilisation des tableaux **fréquence** pour les valeurs entières limitées
* Manipulation ** sortie triée** sans étapes de tri supplémentaires
* Ecrit **propre, langage-agnostique** code (Java, Python, C++)

Ces solutions vous aideront à déterrer l'entrevue sur la structure des données et l'algorithme, et vous aurez un exemple concret à nous donner lors de votre prochaine entrevue.

---

Liste de contrôle à emporter

- [ ] Utilisez un tableau de fréquences (taille 1001) pour le meilleur compromis entre l'espace temporel.
- [ ] Comptez chaque élément seulement une fois par tableau.
- [ ] Recueillir des éléments dont le nombre est égal à "nums.longueur".
- [ ] Retourner le résultat en ordre ascendant (l'ordre d'itération assure le tri).
- [ ] Cas de bord d'essai : intersection vide, tableau unique, contraintes maximales.

Bon codage, et bonne chance d'atterrir ce travail de rêve!