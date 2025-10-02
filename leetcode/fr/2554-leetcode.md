---
titre: LeetCode 2554. Nombre maximum d'entiers à choisir dans une gamme Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2554 – **Nombre maximum d'entiers à choisir dans une gamme I**
### Les bons, les mauvais et les méchants – Un guide de préparation à l'emploi

Description de la section
C'est pas vrai.
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * Autres
**Target Audience**= Ingénieurs de front / back-end, candidats à l'entretien d'algorithme, et toute personne souhaitant passer une entrevue de codage de type LeetCode. Autres
**Concepts de base** Autres
**Langues** Autres

> **SEO Mots-clés**: LeetCode 2554, Nombre maximum d'entiers à choisir A partir d'une plage, solution de tableau, Java, Python, C++, algorithme gourmand, prép d'entrevue, interview de codage, pensée algorithmique, conseils d'entrevue d'emploi.

---

- Oui. 1. Remise en état des problèmes

Vous avez reçu :
- `int[] prohibed` – une liste de numéros que vous ne pouvez pas choisir.
- `int n` – la limite supérieure de la portée `[1, n]`.
- `int maxSum` – la somme maximale que vous pouvez accumuler.

Retournez le nombre **maximum** d'entiers distincts que vous pouvez choisir qui satisfont:
- Chaque numéro choisi :
- Chaque numéro choisi est *non* dans "interdit".
- La somme des nombres choisis ≤ `maxSum`.

---

- Oui. 2. Intuition

La stratégie optimale est *greedy*:
Choisissez d'abord les plus petits numéros autorisés.
Pourquoi ?
- Oui. Les plus petits nombres consomment le moins du budget, vous permettant d'ajouter plus de nombres avant de frapper `maxSum`.
- Puisque chaque nombre peut être pris au plus une fois, il n'y a aucun avantage à sauter un petit nombre en faveur d'un plus grand.

Ainsi, nous pouvons:
1. Marquez tous les numéros interdits.
2. Il faut passer de «1» à «n» dans l'ordre croissant, sans compter les numéros interdits.
3. Gardez une somme en cours d'exécution; arrêtez dès que l'ajout du nombre suivant dépasserait "maxSum".

---

- Oui. 3. Cas de bord

Situation Résultat prévu
- Oui.
Autres Tous les numéros sont interdits.
`maxSum` est plus petit que le plus petit nombre autorisé. "0"
`maxSum` est énorme (par exemple `10^9`) et `n` est petit. Tous les numéros autorisés peuvent être pris. Autres
Le mot `banned` contient des nombres en dehors de `[1, n]`. Autres
`n` est jusqu`à `10^4`, `banned.longueur` jusqu`à `10^4`. Toujours linéaire. Autres

---

- Oui. 4. Analyse de la complexité

Opération Temps Espace
- C'est quoi ?
Marquer les numéros interdits (tableau booléen de la taille `n+1`) Autres
Numérisation de graisse
**Total****** (constante par rapport aux contraintes, ~104) Autres

Parce que `n` ≤ `104`, un simple tableau booléen est rapide et facile à raisonner. Si `n` était plus grand (p. ex. `109`), nous passerions à un ensemble de hachages de numéros interdits et n'itérerions que sur les numéros autorisés, mais cela est inutile ici.

---

- Oui. 5. Mise en œuvre du code

> **Astuce:** Utilisez `long` pour la somme de course pour éviter le débordement lorsque `maxSum` est proche de `109`.

---

##### 5.1 Java

"Java
Importation de java.util.*;

solution de classe {
Int maxCount(int[] interdit, int n, int maxSum) {
// Marquer les numéros interdits dans un tableau booléen
booléen[] interditArr = nouveau booléen[n + 1];
pour (int num : interdit) {
si (num <= n) interditArr[num] = vrai;
}

somme longue = 0;
nombre int = 0;

// Greedy: choisir les plus petits nombres autorisés
pour (int i = 1; i <= n; i++) {
si (interdictionArr[i]) continue; // saut interdit
Si (somme + i > maxSum) rupture; // budget dépassé
Montant i);
count++;
}
le nombre de retours;
}
}
«» "

---

5.2 Python

'`python
Solution de classe:
def maxCount(self, interdit: List[int], n: int, maxSum: int) -> Int:
prohibed_set = set(banned) # O(1) look-ups
somme_val = 0
nombre = 0

pour i dans la plage(1, n + 1):
i en_set interdit :
poursuivre
si sum_val + i > max Somme :
pause
sum_val += Les
nombre += 1
Nombre de retours
«» "

> **Pourquoi un "set"?**
> Pour `n ≤ 104`, le tableau et le jeu sont tous deux bons; un jeu maintient le code simple et fonctionne si `n` grandit.

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int maxCount(vecteur<int>& interdit, int n, int maxSum) {
// Marquer les numéros interdits
vecteur<bool> interditArr(n + 1, faux);
pour (int x : interdit)
si (x <= n) interditArr[x] = vrai;

somme longue = 0;
nombre int = 0;

pour (int i = 1; i <= n; ++i) {
si (interditArr[i]) continue;
en cas de rupture (somme + i > maxSum);
Montant i);
+ nombre;
}
le nombre de retours;
}
};
«» "

---

- Oui. 6. Le bon, le mauvais, le mauvais de ce problème

Qu'est-ce qui fait le bien ?
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
*Simplicité * Facile à comprendre ; la preuve avide est simple. La formulation du problème peut être un peu verbeuse ; vous devez analyser attentivement. La solution naïve pourrait s'initier à tous les chiffres, même lorsque beaucoup sont interdits, ce qui conduirait à un travail inutile. Autres
**L'évolutivité**Le temps linéaire fonctionne pour les contraintes données (`n ≤ 104`). Pour beaucoup plus grand `n` vous'd besoin d'une structure de données plus intelligente (par exemple, arbre de segment). Oublier d'utiliser une somme de 64 bits peut causer des débordements subtils. Autres
Une poignée de cas d'angle couvrent presque tous les modes d'échec. Nécessite de traiter à la fois les nombres interdits en dehors de la gamme et les budgets extrêmes. Certains intervieweurs peuvent ajouter des contraintes cachées (p. ex., plusieurs cas de test en une seule fois). Autres
**La valeur de l'entrevue**= Démontre le raisonnement avide, la manipulation de l'ensemble/de l'arrachage, la manipulation soigneuse des cas de bord. Ce n'est pas un problème de DP ou de graphique classique ; peut être considéré comme trop facile pour les rôles seniors. La solution peut être trop courte pour les intervieweurs qui attendent une discussion plus approfondie (par exemple, pourquoi l'avidité est optimale). Autres

**Traitement des entrevues :**
Expliquez l'intuition gourmande, dessinez la preuve que le choix des plus petits nombres disponibles est optimal et discutez des compromis temps/espace. Cela démontre non seulement la compétence de codage, mais aussi la pensée algorithmique.

---

- Oui. 7. Résumé optimisé du SEO

> **LeetCode 2554** – *Nombre maximum d'entiers à choisir dans une gamme I*
> Apprenez une solution cupide propre en **Java, Python et C++**.
> Master array vs. hash-set techniques, gérer les cas de bord, et obtenir l'entrevue-prêt.
> Prêt pour votre prochain entretien de codage ? Pratiquez ce problème et ajoutez-le à votre portefeuille.

---

Référence rapide

Texte
Entrée: interdite = [1,6,5], n = 5, maxSum = 6
Sortie: 2 // choisissez 2 et 4

Entrée: interdite = [1,2,3,4,5,7], n = 8, maxSum = 1
Sortie: 0 // rien ne correspond

Entrée : interdite = [11], n = 7, maxSum = 50
Sortie: 7 // choisissez 1..7, somme=28
«» "

Bon codage, et bonne chance pour ce travail !