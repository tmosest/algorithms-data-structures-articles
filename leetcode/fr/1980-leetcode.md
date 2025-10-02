---
titre: LeetCode 1980. Trouver une chaîne binaire unique -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Leetcode 1980 – Trouver une chaîne binaire unique
**(Java / Python / C++ Solutions + SEO-Optimized Blog Post)**

---

- Oui. 1. Code (toutes langues)

C'est vrai. Java

"Java
***
* Leetcode 1980 – Trouver une chaîne binaire unique
* Heure: O(n)
* Espace : O(1) (signalisation de la chaîne de sortie)
*/
solution de classe {
public Chaîne trouverDifferentBinaryString(String[] nums) {
int n = longueur nums;
StringBuilder sb = nouveau StringBuilder(n);
pour (int i = 0; i < n; i++) {
// Dépliez le bit en position i (diagonale du canon)
sb.append(nums[i].charAt(i) == '0' ? '1' : '0');
}
retour sb.toString();
}
}
«» "

Python

'`python
Solution de classe:
"""
Leetcode 1980 – Trouver une chaîne binaire unique
Heure: O(n)
Espace : O(1) (signalisation de la chaîne de sortie)
"""
def findDifferentBinaryString(self, nums: List[str]) -> str:
n = len(nums)
# Construire la chaîne diagonale en tournant chaque bit
retourner ''.join('1' si nombres[i][i]== '0' autre '0' pour i dans l'intervalle(n))
«» "

C++

'`cpp
***
* Leetcode 1980 – Trouver une chaîne binaire unique
* Heure: O(n)
* Espace : O(1) (signalisation de la chaîne de sortie)
*/
solution de classe {
public:
string findDifferentBinaryString(vector<string>& nums) {
int n = nombres.size();
la chaîne rés;
res.reserve(n);
pour (int i = 0; i < n; ++i) {
res.push_back(nums[i][i] == '0' ? '1' : '0');
}
retour rés;
}
};
«» "

---

- Oui. 2. Article de blog – Le Bon, le Mauvais, et l'Ugly de Leetcode 1980

#### Titre (Référencement ami)
Leetcode 1980 – Trouver une chaîne binaire unique: Java, Python, C++ Solutions + Interview-Ready Guide

Description de la méta
*Master Leetcode 1980 avec code Java, Python et C++. Apprenez l'astuce de diagonalisation optimale, les pièges à éviter, et comment répondre à cette question d'entrevue. *

---

Présentation

Lors d'un entretien pour un rôle d'ingénierie de logiciel, vous allez rencontrer des problèmes classiques de trouver un élément manquant. Leetcode **1980 – Find Unique Binary String** est un tel puzzle qui teste votre raisonnement sur les cordes, la manipulation de bits et l'élégance algorithmique. Dans cet article, nous allons:

1. ** Expliquez le problème** en anglais.
2. Marchez à travers **Naïve vs Optimal** solutions, en mettant en évidence ce qui est bon,,,,, et, et ,ugly. (en milliers de dollars)
3. Fournir **Les implémentations Java, Python et C++** qui fonctionnent dans le temps linéaire.
4. Discutez des cas de pointe, de la complexité et des conseils d'entrevue.

Laissez plonger !

---

## Énoncé de problème (reformulé)

Vous êtes donné un tableau `nums` de `n` ** chaînes binaires uniques**, chacune de la longueur `n`. Votre tâche : produire toute chaîne binaire de longueur `n` qui **ne figure pas** dans `nums`.

> **Constraints**
> - `1 ≤ n ≤ 16`
> - Chaque chaîne se compose uniquement de `'0'` et `'1'`.
> - Toutes les chaînes dans `nums` sont distinctes.

---

## Le bon: Cantor=S Diagonal Trick

Le problème est une application de manuel de la diagonalisation **Cantors**. Considérez `nums` comme une matrice de bits `n × n`. En tournant les bits diagonaux, vous garantissez une nouvelle chaîne qui diffère de chaque ligne.

Pourquoi ça marche ?

- La ligne `i` a bit `nums[i][i]`.
- Notre nouvelle chaîne `i`-th bit est l'opposite** de ce bit diagonal.
- Par conséquent, la chaîne `i` ne peut pas correspondre à notre nouvelle chaîne à la position `i`, de sorte qu'elle ne peut être identique à aucune ligne.

**Résultat:** Algorithme linéaire, espace constant (ignorer la sortie).

---

- Oui. Les mauvais : Brute- Énumération des forces

Une solution naïve générerait toutes les chaînes binaires possibles de longueur `n` (il y a des possibilités `2^n`) et vérifierait si elles sont dans `nums`. Voici :

- **Complexité temporelle :** `O(2^n)` – impossible même pour `n = 16` (65 536 vérifications).
- **Espace-Complexité:** Potentiellement grand si vous stockez tous les candidats.

Alors que cela passe sur Leetcode en raison de petit `n`, il est un manuel **O(2^n) goulot** et semble mauvais pour les intervieweurs.

---

- Oui. L'horrible : trop compliqué Hachage

Une autre route de "over-engineering" utilise un `HashSet` pour stocker toutes les chaînes et ensuite il retourne automatiquement des bits pour trouver un manquant. Ça marche, mais :

- Vous attribuez un `HashSet` de taille `n`, ce qui est inutile.
- Vous ajoutez de la complexité sans aucun gain dans la lisibilité ou la performance.
- Oui. L'algorithme peut apparaître comme un problème si simple.

À emporter

Stick à l'astuce diagonale – il est court, clair et mathématiquement garanti.

---

Code à suivre

On trouvera ci-dessous des solutions concises et idiomatiques dans les trois principaux langages d'entrevue.

- Oui. 1. Java

"Java
solution de classe {
public Chaîne trouverDifferentBinaryString(String[] nums) {
int n = longueur nums;
StringBuilder sb = nouveau StringBuilder(n);
pour (int i = 0; i < n; i++) {
sb.append(nums[i].charAt(i) == '0' ? '1' : '0');
}
retour sb.toString();
}
}
«» "

*Pourquoi c'est bon: *
- Utilise `StringBuilder` pour la construction de cordes O(n).
- Oui. Pas de structures de données supplémentaires.

- Oui. 2. Python

'`python
Solution de classe:
def findDifferentBinaryString(self, nums: List[str]) -> str:
n = len(nums)
retourner ''.join('1' si nombres[i][i]== '0' autre '0' pour i dans l'intervalle(n))
«» "

*Flacon pyronique: *
- List‐comprehension transforme la boucle en une seule expression.

- Oui. 3. C++

'`cpp
solution de classe {
public:
string findDifferentBinaryString(vector<string>& nums) {
int n = nombres.size();
la chaîne rés;
res.reserve(n);
pour (int i = 0; i < n; ++i) {
res.push_back(nums[i][i] == '0' ? '1' : '0');
}
retour rés;
}
};
«» "

*Spécifications C++:*
- "réserve(n)" évite les réaffectations.
- L'opérateur terne le garde compact.

---

Analyse de complexité

L'approche Temps Espace
- C'est quoi ?
Cantor Diagonal (hors sortie)
(Excepté)
Énumération de HashSet

La solution optimale bat les alternatives par un facteur de "2n" et ne nécessite aucun stockage auxiliaire.

---

## Cas de bord et essais

1. ** Taille minimale (`n = 1`)**
- `nums = ["0"]` → Sortie: `"1"`.
- `nums = ["1"]` → Sortie: `"0"`.

2. **Tous les bits zéro**
- `nums = ["00", "01"]` → Sortie: `"11"`.

3. ** Tous les bits**
- `nums = ["11", "10"]` → Sortie: `"00"`.

4. ** Mélange de rando**
- Tester avec des chaînes binaires aléatoires de longueur `n`.
- Valider que le résultat n'est pas en "nums".

---

## Conseils d'entrevue

Motif
- Oui.
**La diagonalisation des Cantors explicites** Autres
**Linéarité de Mention** Autres
**Éviter les structures de données inutiles** Autres
**Montrer la manipulation de l'étui** Autres
**Commentaires brièvement** Autres

---

Conclusion

Leetcode 1980 est trompeurment simple une fois que vous reconnaissez le motif sous-jacent: un flip diagonal garantit une chaîne manquante. L'astuce diagonale est votre solution « good » – rapide, propre et mathématiquement saine. Évitez la force brute ou les solutions de hachage sur-moteurs – ils sont les façons de distraire les intervieweurs.

En maîtrisant ce problème, vous obtiendrez non seulement la bonne réponse en une fraction de seconde, mais également impressionner les gestionnaires d'embauche avec votre élégance algorithmique et votre discipline de codage.

Bon codage, et bonne chance d'atterrissage ce rôle d'ingénierie de logiciels!

---

Faits saillants du référencement

- **Mots-clés:** Leetcode 1980, Find Unique Binary String, solution Java, solution Python, solution C++, entretien de codage, entretien d'algorithme, diagonalisation de Cantor, codage d'entretien d'emploi, entretien d'ingénierie logicielle.
- **Meta Tags:** `find-unique-binary-string, leetcode-1980, interview-questions, codage-entrevue, algorithme, recherche d'emploi, Java, Python, C++`.

N'hésitez pas à copier les extraits de code, à adapter la structure du blog et à modifier les méta tags pour correspondre à votre marque personnelle ou site de portefeuille. Bonne chance !