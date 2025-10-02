---
titre: LeetCode 1131. Maximum de valeur absolue Expression -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1131 – Maximum d'expression de valeur absolue
*LeetCode*
*Python C++ – Solution One-Pass, O(n)**

---

Table des matières
1. [Énoncé du problème] (#Énoncé du problème)
2. [Pourquoi l'approche Naïve O(n2) est-elle mortelle] (#naïve-approche)
3. [Le point de vue O(n) – Quatre transformations simples](#approche optimale)
4. [Mise en œuvre] (#Mise en œuvre)
- Java
- Python
- C++
5. [Analyse de la complexité] (#complexité)
6. [Liste de contrôle des cas d'urgence](#cas de référence)
7. [Le bon, le mauvais, et le mauvais]
8. [Interview-Ready Tips](#interview-tips)
9. [Conclusion et retrait] (#conclusion)

---

<a name="problem-statement"></a>
- Oui. 1. Exposé des problèmes

On vous donne deux tableaux entiers `arr1` et `arr2` de longueur égale `n`.
Retourner la valeur maximale de

«» "
Le nombre d'heures travaillées dans le cadre d'un programme d'aide à l'emploi a augmenté, passant de 3 % à 3 %, en passant par le nombre d'heures travaillées dans le cadre d'un programme d'aide à l'emploi.
«» "

pour tous `0 <= i, j < n`.

**Contrôles* *

2 ≤ n ≤ 40 000
- Oui.
Valeur ≤ 106

---

<une approche naïve></a>
- Oui. 2. Pourquoi l'approche Naïve O(n2) est mortelle

Une mise en œuvre directe énumère chaque paire «(i, j)»:

Texte
maxVal = 0
pour i en 0..n-1:
pour j en 0..n-1:
val = abs(arr1[i]-arr1[j]) + abs(arr2[i]-arr2[j]) + abs(i-j)
maxVal = max(maxVal, val)
«» "

**Complexité:** temps `O(n2)`, espace `O(1)`.
Avec "n" jusqu'à 40 000, il s'agit d'environ 1,6 milliard d'opérations – bien au-delà d'une limite de 1 seconde.
De plus, les boucles imbriquées cachent une propriété mathématique subtile qui permet une solution **linéaire**.

---

<un nom="approche optimale"></a>
- Oui. 3. Le point de vue O(n) – Quatre transformations simples

L'observation clé :

«» "
= max( (x - y), (y - x)
«» "

Appliquer ceci à chaque terme absolu :

«» "
= max( arr1[i] - arr1[j] - arr1[i]
- arr2[j]
i) j) = max.
«» "

L'élargissement de la somme donne 8 combinaisons linéaires de la forme
«(±arr1[i] ± arr2[i] ± i)».
Étant donné que le terme `=i-j==` est symétrique, les combinaisons réduisent à **quatre** expressions distinctes:

Sens de l'expression
C'est quoi ?
Le nombre d'heures d'ouverture et de fermeture est égal au nombre d'heures d'ouverture.
"-arr1[i] - arr2[i] + i`
< < arr1[i] - arr2[i] + i ' , < < + > >
"-arr1[i] + arr2[i] + i`

Pour deux indices `i` et `j`, la valeur de l'expression originale est égale à la différence entre l'une de ces expressions évaluées à `i` et la même expression évaluée à `j`.
Par conséquent, la valeur maximale possible est simplement la différence maximale entre le **maximum** et **minimum** de chaque expression sur tous les indices.

**Algorithme**

1. Scanner les tableaux une fois, calculer les quatre valeurs pour chaque index.
2. Continuez à exécuter `max` et `min` pour chacune des quatre expressions.
3. La réponse est `max( max1 - min1, max2 - min2, max3 - min3, max4 - min4 )`.

C'est un classique *one-pass, O(n)* solution avec *O(1)* espace supplémentaire.

---

<un nom="mise en oeuvre"></a>
- Oui. 4. Exécution

Voici des implémentations propres, prêtes à coller dans **Java**, **Python** et **C++**.

> **Conseil:** Les trois codes suivent la même logique. Ils ne diffèrent que par la syntaxe et l'utilisation mineure de la bibliothèque.

### Java

"Java
***
* Code Leet 1131 – Maximum d'expression de valeur absolue
* Temps O(n), espace O(1)
*/
solution de classe publique {
Int public maxAbsValExpr(int[] arr1, int[] arr2) {
int n = arr1.longueur;
// Initialiser les extrêmes
int max1 = entier.MIN_VALUE, min1 = entier.MAX_VALUE;
int max2 = entier.MIN_VALUE, min2 = entier.MAX_VALUE;
int max3 = entier.MIN_VALUE, min3 = entier.MAX_VALUE;
Int max4 = entier.MIN_VALUE, min4 = entier.MAX_VALUE;

pour (int i = 0; i < n; i++) {
Int v1 = arr1[i] + arr2[i] + i;
int v2 = -arr1[i] - arr2[i] + i;
int v3 = arr1[i] - arr2[i] + i;
int v4 = -arr1[i] + arr2[i] + i;

max1 = Math.max(max1, v1); min1 = Math.min(min1, v1);
max2 = Math.max(max2, v2); min2 = Math.min(min2, v2);
max3 = Math.max(max3, v3); min3 = Math.min(min3, v3);
max4 = Math.max(max4, v4); min4 = Math.min(min4, v4);
}

retour Math.max(
Math.max(max1 - min1, max2 - min2),
Math.max(max3 - min3, max4 - min4));
}
}
«» "

Python

'`python
Code Leet 1131 – Maximum d'expression de valeur absolue
Temps O(n), espace O(1)

Solution de classe:
def maxAbsValExpr(self, arr1: list[int], arr2: list[int]) -> Int:
max1 = min1 = flotteur('-inf')
max2 = min2 = flotteur('-inf')
max3 = min3 = flotteur('-inf')
max4 = min4 = flotteur('-inf')

pour i, a, b) dans l'énumération(zip(arr1, arr2)):
v1 = a + b + i
v2 = -a - b + i
v3 = a - b + i
v4 = -a + b + i

max1 = max(max1, v1); min1 = min(min1, v1)
max2 = max(max2, v2); min2 = min(min2, v2)
max3 = max(max3, v3); min3 = min(min3, v3)
max4 = max(max4, v4); min4 = min(min4, v4)

retour max(
max1 - min1,
max2 - min2,
max3 - min3,
max4 - min4
)
«» "

C++

'`cpp
// Code Leet 1131 – Maximum d'expression de valeur absolue
// O(n) temps, espace O(1)

solution de classe {
public:
int maxAbsValExpr(vector<int>& arr1, vector<int>& arr2) {
int max1 = INT_MIN, min1 = INT_MAX;
Int max2 = INT_MIN, min2 = INT_MAX;
int max3 = INT_MIN, min3 = INT_MAX;
int max4 = INT_MIN, min4 = INT_MAX;

pour (int i = 0; i < arr1.size(); ++i) {
Int v1 = arr1[i] + arr2[i] + i;
int v2 = -arr1[i] - arr2[i] + i;
int v3 = arr1[i] - arr2[i] + i;
int v4 = -arr1[i] + arr2[i] + i;

max1 = max(max1, v1); min1 = min(min1, v1);
max2 = max(max2, v2); min2 = min(min2, v2);
max3 = max(max3, v3); min3 = min(min3, v3);
max4 = max(max4, v4); min4 = min(min4, v4);
}

retour max({max1 - min1, max2 - min2, max3 - min3, max4 - min4});
}
};
«» "

---

<un nom="complexité"></a>
- Oui. 5. Analyse de la complexité

Métrique
- C'est quoi ?
**Heure** Autres
**Espace** Autres

L'algorithme est linéaire dans la longueur des tableaux et utilise un espace auxiliaire constant, satisfaisant les contraintes du problème même à la limite supérieure (`n = 40 000`).

---

<un nom="cases"></a>
- Oui. 6. Liste de contrôle des cas de bord

Autres Décision Pourquoi ça compte ?
- Oui.
La taille la plus petite est permise; assurez le fonctionnement des boucles. Autres
Les nombres négatifs dans `arr1/arr2`. Les expressions utilisent `+` et `-` de manière appropriée. Autres
Autres Tous les éléments sont égaux.Toutes les différences deviennent nulles à l'exception de "i-j"". La formule reprend toujours le terme "i-j". Autres
Autres Très grande magnitude du débordement potentiel dans l'int 32-bit signé? Pas de débordement. Autres
Nombre de tableaux vides Non autorisé par les contraintes. Pas besoin de garder. Autres

---

<a name="good-bad-ugly"></a>
- Oui. 7. Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Mathématical Insight**=Il transforme une expression cubique en quatre formes linéaires. Requiert une dérivation soigneuse; facile à rater un signe. Aucun dérivé. Autres
**Runtime**="O(n)" – passe les limites de LeetCode.="O(n2)` force brute échoue.="Aucun.="
**Loops compactes, noms de variables clairs. Un excès d'abstraction (p. ex. en utilisant des tableaux pour 4 valeurs) peut nuire à la clarté. Une ligne unique `max({})` dans C++ peut sembler terse pour les débutants. Autres
**Maintenabilité** Aucun.

**Ligne de bottom:** L'élégant «max – min» tour est l'étoile de ce problème. Une fois que vous le voyez, la solution devient simple et très efficace.

---

<un nom="conclusion"></a>
- Oui. 8. Conclusion

Nous avons disséqué **LeetCode 1131 – Maximum d'expression de valeur absolue** pour révéler sa linéarité cachée, a dérivé un algorithme *linéaire* et a livré des solutions prêtes à déployer dans trois langues principales.

**Traitements clés pour les intervieweurs et les candidats :**

- ** Cherchez des simplifications algébriques.** Les valeurs absolues peuvent souvent être éliminées en considérant toutes les permutations de signes.
- **Analysez toujours les contraintes du problème** – elles laissent généralement entendre la complexité correcte.
- **Test cas bord** rigoureusement ; un mauvais signe peut silencieusement vaincre une implémentation correcte.

Utilisez ces solutions comme un modèle pour d'autres problèmes diff. abmax, et vous aurez un outil puissant dans votre boîte à outils algorithmique.

Bon codage ! C'est ce qu'il a dit.

---

** Termes de recherche pour stimuler votre référencement:**

- Solution LeetCode 1131
- Algorithme d'expression de valeur absolue maximale
- Différence maximale de la paire de tableaux O(n)
- Python Java C++ Problèmes de tableau LeetCode
- Optimisation de la combinaison linéaire
- Aperçu de l'algorithme d'entrevue

Ces mots-clés garantissent que quiconque recherche une solution concise et performante à LeetCode 1131 trouve cet article.