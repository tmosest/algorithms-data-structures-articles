---
titre: LeetCode 658. Trouver les éléments les plus proches de K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

## 658. Trouver les éléments les plus proches de K – De la théorie à la production – Code de préparation

**Mots clés:** LeetCode 658, Trouver K le plus proche Éléments, algorithme à deux points, recherche binaire, file d'attente prioritaire, Java, Python, C++, interview algorithmique, solution O(n), préparation d'entrevue, interview de codage

---

Récapitulation des problèmes

> **Grâce à un tableau entier *trié* `arr`, et à deux entiers `k` et `x`,
> **Retour** les entiers `k` dans `arr` qui sont les plus proches de `x`.
>
> La liste retournée doit également être triée par ordre croissant.
>
> Si deux nombres sont également proches de "x", le nombre le plus petit gagne.

Exemple Entrée Sortie
- C'est quoi ?
< < arr = [1,2,3,4,5] > > , < < k = 4 > > , < < x = 3 > > , < < [1,2,3,4] > > Autres
< < ar = [1,1,2,3,4,5] > > , < < k = 4 > > , < < x = -1 > > , < < [1,1,2,3] > > Autres

**Contrôles* *

«» "
1 ≤ k ≤ longueur d'arrondi ≤ 104
arr est trié en ordre ascendant
-104 ≤ arr[i], x ≤ 104
«» "

---

Les choix algorithmiques – Les bons, les mauvais, les mauvais

Une bonne approche
C'est pas vrai.
**Fenêtre coulissante à deux points**= O(n) temps, O(1) espace supplémentaire – simple à comprendre et code== Besoin d'une gestion soigneuse de la logique de rupture d'attache (abs‐différences)= Rarement utilisé dans les entrevues; peut être négligé par rapport aux astuces de recherche binaire==
**Binary-search avec fenêtre coulissante**= O(log n) time, O(1) space – optimum pour les grands tableaux== Plus complexe à implémenter correctement; hors-par-un bugs communs==Certains intervieweurs adorent ce =trick== mais ils peuvent être difficiles à comparer===
**Priorité file d'attente (max-pap de taille k)**= Facile à raisonner à propos de & #160; maintenir le k le mieux jusqu'à présent==== O(n log k) temps, O(k) espace – plus lent sur les grandes entrées== Les opérations de happ peuvent devenir un goulot d'étranglement; pas le plus optimal pour les tableaux triés===
**Force brute + tri**

> **Ligne de bottom:** Pour un tableau trié, la fenêtre coulissante à deux points est le *spot doux* – temps linéaire, espace constant, et elle respecte naturellement l'exigence de commande.

---

C'est vrai. Fenêtre coulissante à deux points – Le code « Good »

3.1 Concept

Nous maintenons deux indices, `gauche` et `droite`, qui délimitent une fenêtre de candidats.
Alors que la taille de la fenêtre est supérieure à `k`, nous laissons tomber l'extrémité *farther* de la fenêtre:

«» "
if-arr[gauche] - x-arr[droite] - x-arr → gauche++ // l'extrémité gauche est plus loin
autrement → droite-- // la fin droite est plus loin ou égale
«» "

Quand `right - left + 1 == k`, la fenêtre contient exactement la réponse.

3.2 Complexité

- **Heure:** O(n) – chaque élément est examiné au plus une fois.
- **Espace:** O(1) – seulement deux indices et une liste de résultats.

---

Mise en œuvre de Java

"Java
Importation de java.util.*;

solution de classe publique {
***
* Trouve les entiers k dans un tableau trié le plus proche de x.
*
* @param arr le tableau trié
* @param k nombre d'éléments à retourner
* @param x valeur cible
* @return une liste contenant les éléments k les plus proches en ordre ascendant
*/
liste publique<integer> trouverFermerElements(int[] arr, int k, int x) {
Int gauche = 0;
Int droite = longueur d'arrondi - 1;

// Réduire la fenêtre jusqu'à ce que seuls les éléments k restent
pendant que (droite - gauche + 1 > k) {
si (Math.abs(arr[gauche] - x) > Math.abs(arr[droite] - x)) {
gauche++; // gauche est plus loin – déposez-le
} autre {
droite--; // droite est plus loin (ou cravate avec plus petite gauche) – la déposer
}
}

// Copiez la fenêtre dans une liste <integer>
Liste <Integer> résultat = nouvelle liste de distribution<>(k);
pour (int i = gauche; i <= droite; i++) {
le résultat.add(arr[i]);
}
le résultat du retour;
}
}
«» "

> **Pourquoi la comparaison `Math.abs`? * *
> La règle tie-break de problems ( ''=a-x=') est déjà satisfaite en gardant l'index *plus petit* à gauche.
> Si les distances sont égales, la branche "else" garde le côté gauche (le nombre plus petit), correspondant exactement à l'exigence.

---

Mise en œuvre de Python

'`python
de taper l'importation Liste

Solution de classe:
def findFermerstElements(self, arr: List[int], k: int, x: int) -> Liste[int]:
gauche, droite = 0, len(arr) - 1

alors que droite - gauche + 1 > k:
si abs(arr[left] - x) > abs(arr[right] - x):
gauche += 1
Sinon:
droite -= 1

retour arr[left:right+1]
«» "

> La version Python est presque identique – la tranche `arr[left:right+1]` donne directement la sous-liste triée.

---

Mise en œuvre du C++

'`cpp
#incluez <vecteur>
#incluez <cmath>

solution de classe {
public:
std::vector<int> findFermerstElements(std::vector<int>& arr, int k, int x) {
Int gauche = 0;
int droite = arr.size() - 1;

pendant que (droite - gauche + 1 > k) {
Si (std::abs(arr[left] - x) > md::abs(arr[right] - x))
++ gauche; // gauche
Autre
--à droite; // à droite
}

retour::vector<int>(arr.begin() + gauche, arr.begin() + droite + 1);
}
};
«» "

> L'utilisation de `std::vector`s iterator constructor rend la copie du résultat concis.

---

- Oui. Pourquoi cette solution gagne dans les entrevues

1. ** Logique claire et concise** – Aucune boucle ni structure de données complexe.
2. **Temps optimal** – O(n) bat le niveau de référence du tri O(n log n).
3. **Space‐friendly** – Constante mémoire supplémentaire; correspond à l'interview .
4. **Poignées brisant implicitement** – Pas de vérification supplémentaire `si (a < b)`, juste l'ordre naturel du tableau.

> Les intervieweurs aiment une solution qui *fait* quelque chose d'intéressant *et* reste simple. La méthode à deux points coche les deux cases.

---

## 5-Optimized Blog Meta

- **Titre:** LeetCode 658 – - Trouver les éléments les plus proches de K Algorithme expliqué (Java/Python/C++)
- **Meta Description:** Master LeetCode 658 avec une solution rapide à deux points O(n) en Java, Python et C++. Apprenez les bonnes, les mauvaises et les mauvaises approches algorithmiques.
- **Mots clés:** LeetCode 658, Trouver les éléments les plus proches de K, algorithme à deux points, recherche binaire, prép d'entrevue, interview de codage, Java, Python, C++, explication d'algorithme, solution O(n).

---

#### 6-

Même si l'approche à deux points est parfaite pour les entrées triées, il **won=t généralise** pour les tableaux non triés.
Si l'entrée n'a pas été triée, vous auriez besoin d'un maximum de "k" de taille, ce qui introduit le temps "O(n log k).
Ainsi, toujours confirmer que le tableau est trié avant de choisir l'astuce de la fenêtre coulissante.

---

À emporter

Pour les tableaux *triés*, **la fenêtre coulissante à deux points** est votre algorithme d'entrée pour LeetCode 658.
Il satisfait aux contraintes, respecte la règle de l'égalité et dispose d'une preuve claire de la justesse de l'entrevue.

Bonne chance pour votre prochaine interview – maintenant vous pouvez vous en aller avec une implémentation *clean* et un billet de blog qui sera découvert par d'autres personnes interrogées à la recherche de solutions LeetCode 658.