---
titre: LeetCode 1144. Diminuer les éléments pour faire Array Zigzag -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1144. Diminuer les éléments pour faire Array Zigzag
**LeetCode #1144.

> **Objectif:**
> Compte tenu d'un tableau entier `nums`, dans un mouvement vous pouvez décréter n'importe quel élément par 1.
> Retourner le nombre minimum de mouvements requis pour transformer des «nums» en un tableau *zig‐zag*, c'est-à-dire
> - chaque élément indexé uniforme est supérieur à ses éléments adjacents (`A[0] > A[1] < A[2] > ...`)
> - ou chaque élément indexé impair est supérieur à ses éléments adjacents (`A[0] < A[1] > A[2] < ...`).

---

- Oui. Pourquoi est-ce un problème d'entrevue classique ?

* **Simple entrée et sortie** → facile à verbaliser pendant une entrevue.
* **Deux points de vue différents** (parallèles par rapport aux parallèles) → montrent la capacité du candidat à gérer la logique de branchement.
* **Greedy / décisions locales** → parfait pour enseigner *=pourquoi les œuvres gourmandes*.
* **Petites contraintes (= 1000)** → l'intervieweur peut s'attendre à une solution O(n) sans insister sur la performance.

---

- Oui. L'idée de l'avidité – Fixez les mauvais sommets

Pour chaque indice "i" il suffit de savoir si c'est **actuellement un pic** par rapport à ses deux voisins.
Si ce n'est pas un pic, nous pouvons le baisser jusqu'à ce qu'il devienne un pic valide.
Le moyen le moins cher est de le baisser juste assez pour être *strictement* plus petit que le plus petit de ses deux voisins.

«» "
Coût(i) = max(0, nombres[i] - min(nombres[i‐1], nombres[i+1]) + 1)
«» "

*Le `+1` garantit une stricte inégalité. *
Si l'index se trouve à la limite (`i==0` ou `i==n-1`), le voisin manquant est traité comme "infini", c'est-à-dire que l'élément n'a jamais besoin d'être abaissé pour ce côté.

---

- Oui. Deux solutions indépendantes

Nous calculons le coût total pour deux scénarios indépendants :

1. ** Même les indices doivent être des pics** (« A[0] > A[1] < A[2] > ... ».
2. **Les indices d'échéance doivent être des pics** (« A[0] < A[1] > A[2] < ...».

La réponse est le minimum des deux totaux.

Parce que chaque élément est inspecté une fois, l'algorithme fonctionne dans **O(n)** temps et utilise **O(1)** espace supplémentaire.

---

- Oui. 1. Mise en œuvre Java

"Java
Importation de java.util.*;

solution de classe {
Les mouvements publics d'intérêtPourMakeZigzag(int[] nums) {
= 0; // pics à des positions égales
int impairCoût = 0; // pics à des positions impaires
int n = longueur nums;

pour (int i = 0; i < n; i++) {
// Déterminer la limite inférieure requise des voisins
int lowerBound = entier.MAX_VALUE;
si (i > 0) inférieureBound = Math.min(Bound inférieur, nombres[i - 1]);
si (i + 1 < n) plus basBound = Math.min(Bound inférieur, nombres[i + 1]);

// Si l'élément actuel est déjà inférieur aux deux voisins, aucun coût
si (nums[i] > moinsBound) {
coût int = nombres[i] - Bound inférieur + 1;
Si (i et 1)] 0) // même indice
même Coût += coût;
Autre
coût impair += coût;
}
}
retour Math.min(mêmeCoût, impairCoût);
}
}
«» "

> ** Points clefs**
> * `Integer.MAX_VALUE` garantit que le côté sans voisin est ignoré.
> * Le bit‐op `i & 1` est une petite accélération sur `i % 2`.
> * Pas de tableaux supplémentaires – l'espace est constant.

---

- Oui. 2. Mise en œuvre de Python

'`python
Solution de classe:
Déplacements TomakeZigzag(self, nums: List[int]) -> Int:
even_cost = impair_cost = 0
n = len(nums)

pour i dans la plage(n):
inférieure = flotteur('inf')
i > 0: inférieur = min(inférieur, nombres[i - 1])
i + 1 < n: inférieur = min(inférieur, nombres[i + 1])

si nombres[i] > inférieurs:
Coût = nombres[i] - inférieur + 1
i % 2 == 0 & #160;:
even_cost +=cost
Sinon:
_coût impair += coût

retour min(even_cost, impair_cost)
«» "

> Python est très proche de la logique Java – seulement des changements de syntaxe.
> `float('inf')' joue le rôle d'"aucun voisin".

---

- Oui. 3. Mise en œuvre C++

'`cpp
solution de classe {
public:
int movesToMakeZigzag(vecteur<int>& nums) {
longue même Coût = 0, impairCoût = 0; // utiliser longtemps pour la sécurité
int n = nombres.size();

pour (int i = 0; i < n; ++i) {
int inférieur = INT_MAX;
si (i > 0) plus faible = min (inférieur, nombres [i-1]);
si (i + 1 < n) inférieur = min(inférieur, nombres[i+1]);

si (nums[i] > inférieur) {
coût int = nombres[i] - inférieur + 1;
Si (i % 2 == 0) coût pair +=;
Autre étrange Coût += coût;
}
}
retourner static_cast<int>(min(evenCost, impairCost));
}
};
«» "

> **Pourquoi "long"?**
> Dans le pire des cas, chaque élément peut être 1000 et nous pourrions additionner jusqu'à 500 × 1000 500 000.
> Il convient toujours à `int`, mais l'utilisation de `long long` garantit aucun débordement si les contraintes se multiplient.

---

## Bonne, mauvaise et laid: ce que les intervieweurs recherchent

**Quoi de neuf**
C'est-à-dire...
**Explication raisonnable que l'abaissement d'un mauvais sommet ne peut pas nuire aux sommets futurs.
**Manipulation de l'appareil**= Traiter les voisins manquants comme étant infinis== ou sauter le contrôle==____________________________________________________________________________________________________________________________________________________________________________________________________________________________________
Autres **Complexité du temps**= O(n) pass simple=== Extra O(n) tableaux ou boucles imbriquées==Tenir aux passes linéaires===
Autres **Complexité de l'espace**. O(1) auxiliaire.
**Readability**= Effacer les noms de variables, les commentaires== Nombres magiques (`1`) sans explication== Utiliser des noms significatifs (`evenCost`, `oddCost`, `lower`) Autres
**Cas d'escroquerie**=Poignées d'un seul élément, toutes égales, en baisse stricte== Suppose au moins deux éléments==Test toujours avec `n=1`=

---

## Tester votre solution

'`python
def test():
sol = Solution()
affirme sol.movesToMakeZigzag([1,2,3]) 2
affirme sol.movesToMakeZigzag([9,6,1,62]) 4
affirme sol.movesToMakeZigzag([3]) == 0 # élément unique
affirme sol.movesToMakeZigzag([5,4,3,2,1]) 4 # déjà zigzag? Calcul
print("Tous les tests passés")
essai()
«» "

Exécutez ce qui précède pour les trois implémentations; elles devraient produire les mêmes résultats.

---

## Article de blog optimisé du SEO

> **Titre (H1) :**
> *=Master LeetCode 1144: Diminuer les éléments pour faire Array Zigzag – Java, Python, C++ Solutions & Interview Insights

> **Désignation de la Méta (155 caractères):**
> *Apprenez l'algorithme gourmand pour LeetCode 1144 (Modifier les éléments pour faire Array Zigzag). Obtenez Java, Python, code C++, analyse de complexité, gestion des cas et conseils d'entrevue. *

---

- Oui. 1. Présentation

> **Qu'est-ce qu'un tableau Zigzag? * *
> Une séquence qui alterne entre les pics et les vallées: `A[0] > A[1] < A[2] > A[3] < ...` ou le contraire.
> **Pourquoi est-ce intéressant? **
> Il vous force à penser localement (chaque élément par rapport aux voisins) tout en optimisant globalement (déplacements totaux).

- Oui. 2. Rétablissement des problèmes

> Compte tenu des "nums[0 ... n‐1]" (1 ≤ n ≤ 1000, 1 ≤ nums[i] ≤ 1000), retourner le nombre minimum de mouvements de diminution nécessaires pour transformer le tableau en zigzag.
> Un mouvement : `nums[i] = nombres[i] - 1'.

- Oui. 3. Intuition & Greedy Insight

* Un pic doit être ** strictement plus grand** que ses voisins.
* Si ce n'est pas le cas, la solution la moins chère est de la réduire juste assez.
* L'optimalité de cette fixation locale s'en suit parce que l'abaissement d'un pic ne peut pas améliorer les exigences d'un autre élément – elle n'assouplit que potentiellement les contraintes des voisins.

- Oui. 4. Algorithme étape par étape

1. **Initialiser deux compteurs**: `evenCost` et `odd Coût.
2. **Loop à travers tous les indices** "i = 0 ... n‐1".
* Trouver `lowerBound = min(nums[i-1], nums[i+1])' (ignorer les voisins disparus).
* Si `nums[i] > lowerBound`, calculer `coût = nombres[i] - Bound inférieur + 1'.
* Ajouter `coût` à `evenCoût` si `i` est pair, sinon `odd Coût.
3. **Retour `min(evenCoût, impairCoût)`**.

- Oui. 5. Analyse de la complexité

Formule métrique Résultat
C'est quoi, ça ?
Temps de passage simple sur le tableau **O(n)** Autres
L'espace Variables auxiliaires constantes

- Oui. 6. Cas de bord

Pourquoi ça compte ?
-- -- -- -- -- -- --------------------------------------------------
Élément unique (déjà zigzag)
"[5,5]" Tous égaux "2" (élément intermédiaire inférieur)
"[10,1,10,10]"" Déjà zigzag (maximums impaires)
"[1,1000,1,1000,1]"""Grands pics" "999" (deuxième élément inférieur)"

- Oui. 7. Code en trois langues

*Java, Python, extraits C++ (voir ci-dessus). *
*Tous partagent la même logique, ne différant que dans la syntaxe. *

- Oui. 8. Pièges communs dans les entrevues

1. **Oublier l'état strict de la maladie** – entraîne des déplacements sous-comptables.
2. ** Manipulation incorrecte des limites** – contrôles `i-1 < 0` ou `i+1 >= n`.
3. **L'utilisation de `>=` au lieu de `>` lors de la comparaison avec les voisins** – provoque des boucles infinies dans une mise en œuvre naïve.
4. **Suringénierie** – construction de nouveaux réseaux ou utilisation de récursions inutilement.

- Oui. 9. Autres approches

* ** Programmation dynamique** – trop de compétences pour ce problème ; la cupidité est optimale.
* ** Solution à deux passes** – première passe diminue nécessaire, deuxième passe. Comme cupide mais divisé en étapes.
* **Bit-masking** – sans objet; le motif est fixe (speaks at even/odd index).

10 ans. Conclusion

LeetCode 1144 est une vitrine parfaite pour une stratégie d'avidité propre.
En se concentrant sur les violations locales et en les corrigeant avec un minimum d'effort, vous pouvez garantir l'optimum mondial.
Les implémentations Java, Python et C++ ci-dessus s'exécutent dans le temps linéaire, utilisent un espace constant et gèrent avec grâce tous les cas bord.

> ** Prêt à accepter l'entrevue? **
> Pratiquez le modèle avide, comprenez pourquoi il fonctionne, et n'oubliez pas d'expliquer la stricte inégalité et la logique des frontières.
> Bonne chance !

---

11 ans. Appel à l'action

> Si vous avez trouvé cet article utile, **s'abonner** à notre newsletter pour des interviews hebdomadaires.
> Laissez un commentaire avec vos propres tests ou demandez-vous au sujet du prochain défi LeetCode.

---

Liste de contrôle finale Avant l'entrevue

1. ** Expliquez l'idée gourmande** – pas seulement ça marche.
2. **Montrer la manipulation des limites** – illustrer avec un court diagramme.
3. ** Exécuter un test rapide en direct** – par exemple, `[1,2,3]`.
4. **Complexité des peines** – gardez-les toujours à l'esprit.
5. ** Gardez le code lisible** – noms significatifs, commentaires.

Avec la solution, la routine de test, et les idées d'entrevue, vous êtes tous prêts à transformer le problème *Zigzag* d'un puzzle en une victoire d'entrevue stimulant la confiance.