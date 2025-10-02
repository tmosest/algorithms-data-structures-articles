---
titre: LeetCode 2240. Nombre de moyens d'acheter des stylos et des crayons -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
N° 1 Le Code (Java-Python-C++)

> **Problème** – Code de Leet 2240 Nombre de façons d'acheter des stylos et des crayons
> **Objectif** – Comptez le nombre de paires distinctes *(pens, crayons)* que vous pouvez acheter avec le plus `total` dollars.

Voici des solutions propres et prêtes à la production dans trois langues d'entrevue populaires.
Tous les trois courent dans **O(total / min(coût1, coût2)** temps et **O(1)** espace supplémentaire.

---

## 1.1 Java

"Java
***
* LeetCode 2240 – Nombre de moyens d'acheter des stylos et des crayons
*
* Temps: O(total / min(coût1, coût2))
* Espace: O(1)
*/
solution de classe publique {
Voies publiques de longue durée AcheterPensPencils(int total, coût int1, coût int2) {
longueur = 0;

// itérer sur la quantité de l'article plus cher pour garder la boucle courte
int maxPens = total / Math.min(coût1, coût2);

// si le coût1 est moins cher, itérer les stylos; sinon, itérer les crayons.
Voie booléenne Stylos = coût1 <= coût2;

pour (int i = 0; i <= maxPens; i++) {
de longue durée;
Int restant;

si (usePens) { // boucle sur les stylos
dépenses = (long) i * coût1;
restant = (int) (total - dépensé);
} autre { // boucle sur crayons
dépenses = (long) i * coût2;
restant = (int) (total - dépensé);
}

// nombre maximal de l'autre article qui peut encore être acheté
int maxAutre = restant / (usePens ? coût2 : coût1);

// +1 pour l'autre article
Voies += maxAutres + 1;
}

les voies de retour;
}
}
«» "

---

## 1.2 Python

'`python
"""
LeetCode 2240 – Nombre de moyens d'acheter des stylos et des crayons
"""

def ways To BuyPensPencils(total: int, coût1: int, coût2: int) -> Int:
# Itérer sur l'article moins cher pour réduire le nombre d'itérations
si coût1 <= coût2:
max_first = total // coût1
premier_coût, deuxième_coût = coût1, coût2
Sinon:
max_first = total // coût2
premier_coût, deuxième_coût = coût2, coût1

Voies = 0
pour i dans la plage (max_first + 1):
restant = total - i * premier coût
max_second = restant // second_coût
+= max_seconde + 1 # +1 pour acheter 0 du second article
retour
«» "

---

C++

'`cpp
***
* LeetCode 2240 – Nombre de moyens d'acheter des stylos et des crayons
*
* Temps: O(total / min(coût1, coût2))
* Espace: O(1)
*/
solution de classe {
public:
long chemin AcheterPensPencils(int total, coût int1, coût int2) {
longueurs longues = 0;

// itérer sur l'article moins cher
Voie orale Stylos = coût1 <= coût2;
int maxFirst = total / (usePens ? coût1 : coût2);

pour (int i = 0; i <= maxFirst; ++i) {
i * (utilisationPens ? coût1 : coût2);
Int restant = total - dépensé;
int maxSecond = restant / (usePens ? coût2 : coût1);
+= maxSecond + 1; // +1 pour acheter 0 du deuxième article
}
les voies de retour;
}
};
«» "

> **Pourquoi c'est rapide** – La boucle tourne `total / min(coût1, coût2)` temps, qui est au plus `106` dans le pire des cas.
> **Pourquoi c'est sûr** – Tous les produits intermédiaires sont moulés à "long`/`long` pour éviter le débordement.
> **Pourquoi c'est convivial pour l'entrevue** – La logique est simple, le code est compact, et vous pouvez discuter de l'astuce "cheaper-item-first" dans une entrevue.

---

Article du blog – Le bon, le mauvais, et le lamentable d'acheter des stylos et des crayons

> **Description détaillée**
> Plongez profondément dans le LeetCode 2240: Nombre de façons d'acheter des stylos et des crayons. Apprenez les maths, les extraits de code en Java, Python et C++, les pièges d'entrevue, et comment maîtriser ce problème peut stimuler votre score d'entrevue de codage.

---

2.1 Introduction

Dans un monde où votre CV est la première impression, cracher un problème moyen LeetCode peut être la différence entre un callback et un rejet. L'un de ces problèmes est le nombre de façons d'acheter des stylos et des crayons** (LeetCode 2240). Bien que cela puisse ressembler à un exercice arithmétique trivial, les nuances cachées en font une grande vitrine d'entrevue:

- **Compréhension solide des boucles et des maths* *
- **Attention aux débordements entiers**
- **Choisir la variable d'itération optimale* *

Laissez passer le bon, le mauvais et le mauvais.

---

## 2.2 Récapitulation des problèmes

Vous avez ` total` dollars et deux éléments:

Poste Coût
- Oui.
Unité
Crayon

Vous pouvez acheter toute quantité entière non négative de chacun, à condition que le montant total des dépenses ne dépasse pas le «total».
**Objectif:** Comptez le nombre de paires distinctes *(pens, crayons)* que vous pouvez acheter.

> **Exemple**
> `total = 20, coût1 = 10, coût2 = 5` → 9 façons (comme indiqué dans l'énoncé du problème).

---

2.3 Le bon – un droit En avant, solution pour l'avidité

La solution la plus courante itère sur le nombre de stylos (ou crayons) que vous pouvez acheter et, pour chaque, calcule le maximum de crayons restants.

- Oui. Pourquoi ça marche

Si vous décidez des stylos `p`, le reste de l'argent est `total – p * coût1`.
Le plus grand nombre de crayons que vous pouvez encore acheter est `=remaining / cost2==`.
Pour chaque `p`, le nombre d'options de crayon est `=remaining / cost2=2 + 1` (le +1 compte pour l'achat de crayons zéro).

Complexité

- **Heure**: "O(total / coût1)"
- **Espace**: "O(1)"

Ceci est optimal pour les contraintes (total ≤ 106).

Faits saillants de la mise en oeuvre

Mots clés Autres
C'est pas vrai.
Utiliser `long` pour les produits intermédiaires pour éviter les débordements. Autres
**Python** Autres
**C++**="long long" protège du débordement. Autres

---

2.4 Le mauvais – les variantes inefficaces ou buggy

Pourquoi ça va mal
C'est quoi ?
**Le nombre de boucles devient "total / max(cost1, cost2)", ce qui peut être 1 000 000, même si l'élément le moins cher permet beaucoup moins d'itérations. Toujours acceptable, mais pas optimal. Autres
**Éviter l'affaire 0.**Éviter d'ajouter `+1` pour chaque boucle entraîne une erreur hors-par-un. Autres
**L'utilisation de `int` pour les produits**="total * cost1` peut déborder `int` (par exemple, `106 * 106`). Autres
**Sur-complication avec la récursion** Autres
**Ignorer les cas de bord**= Lorsque les deux coûts dépassent le « total », la réponse doit toujours être 1 (ne rien acheter). Autres

---

## 2.5 L'Ugly – Complexité excessive et inutile

Certains codeurs essaient d'appliquer une programmation dynamique ou des formules combinatoires. Bien que mathématiquement élégants, ils peuvent masquer la simple logique gourmande et rendre les réponses d'entrevue plus difficiles à expliquer.

- **DP**
`dp[i] = dp[i-cost1] + dp[i-cost2] "
Pourquoi moche ? Il nécessite un tableau de taille `total + 1` et est surqualifié pour un problème de comptage.

- **Formulaire fermée**
Certaines solutions dérivent `=total/coût1= *=(total - coût1)/coût2=‘ mais oublient l'effet cumulatif. Il est sujet à erreur et difficile à justifier lors d'une entrevue.

**Ligne de bottom:** La simplicité gagne. Une boucle claire + explication mathématique est la plus facile d'entrevue.

---

2.6 Conseils d'entrevue

1. **Énoncer clairement le problème** – Nous voulons compter les solutions entières non négatives à `p * coût1 + q * coût2 ≤ total`.
2. ** Expliquez l'approche de la graisse** – Fix stylos, calculer le reste, puis compter les crayons. (en milliers de dollars)
3. **Edge Cases** – Si les deux coûts sont plus grands que le total, la seule possibilité est de 0 stylos, 0 crayons. (en milliers de dollars)
4. **Conversation de complexité** – Nous tournons jusqu'à "total / min(coût1, coût2)". Pour 106, ça va. (en milliers de dollars)
5. **Manipulation de l'excès de flux** – Utiliser des entiers 64 bits en Java/C++. (en milliers de dollars)

---

## 2.7 Extraits de code – Prêt pour votre portefeuille

> **Java** – `Solution.java "
> **Python** – `solution.py "
> **C++** – `solution.cpp "

*(Voir la section 1 pour le code complet prêt à copier.) *

---

## 2.8 SEO Boost: Mots-clés et phrases

Primaire Secondaire
C'est quoi, ça ?
Code Leet 2240 Nombre de moyens d'acheter des stylos et des crayons
Codage interview
Entretien de codage Java
Un problème algorithmique
Algorithme cupide
complexité temporelle
Conseils d'entrevue Questions d'entrevue

---

2.9 Réflexions finales

Maîtrise **LeetCode 2240** démontre:

- ** intuition mathématique** – transformer un nombre combinatoire en une simple boucle.
- ** Agilité linguistique** – implémenter la même logique en Java, Python et C++.
- **Interview finesse** – expliquer la solution de façon concise, couvrir les cas de bord et traiter les problèmes de performance.

Ajoutez ce problème (et sa solution propre) à votre portfolio GitHub, incluez-le dans votre blog technique, et vous vous démarquez des recruteurs à la recherche de solutions de problèmes. Bonne chance pour votre prochain entretien !

---