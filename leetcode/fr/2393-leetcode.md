---
titre: LeetCode 2393. Compter strictement augmenter Subarrays -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de Leet 2393 – Compter les sous-arrachages qui augmentent strictement
- Oui. Java / Python / C++ Solutions + Un blog optimisé pour le référencement
*(Si vous vous préparez à une entrevue de codage, c'est le guide d'une page que vous voudrez garder à portée de main.) *

---

- Oui. 1. Résumé du problème

> **Don** un tableau entier "nums" (valeurs positives).
> **Retour** le nombre total de subarrays *contitueux* qui sont ** strictement en augmentation**.

> **Définition**
> *Un sous-array* est une tranche continue du tableau original.
> Un sous-barrage `nums[l ... r]` est *en augmentation stricte* si `nums[l] < nums[l+1] < ... < nums[r]`.

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
6 singletons + 3 paires + 1 triple
Chaque sous-arrachage augmente (numéro triangulaire 5·6/2)

**Contrôles* *

- Oui.
-- -- -- -- -- --
1 ≤ `nums.longueur` ≤ 10<sup>5</sup> ≤ 10<sup>6</sup>

---

- Oui. 2. Brute-Force vs Optimal

L'approche Temps L'espace Commentaires
C'est pas vrai.
Énumérer tous les sous-barrages et vérifier O(n2)= O(1)= Résolu uniquement pour les petits tableaux. Autres
**Two-pointer / sliding window** , **O(n)** , O(1) , Gardez le segment croissant courant ; ajoutez le nombre de subarrays à l'intérieur. Autres
Programmation dynamique (sommes cumulées) (O(n)) (O(n)) (O)(n)) Fonctionne mais utilise une mémoire supplémentaire inutilement. Autres

> **Bien**: O(n) col simple, espace constant.
> **Bad**: O(n2) force brute, trop lente pour 105.
> **Ugly**: DP qui stocke des valeurs intermédiaires, mémoire gaspillée.

---

- Oui. 3. La solution O(n) élégante

1. Scannez le tableau une fois.
2. Maintenir la longueur "len" du segment *current* en pleine augmentation.
3. Lorsque le segment se termine (c.-à-d. `nums[i] <= nums[i‐1]`), ajouter
\[
\text{segment\_count} = \frac{len \times (len+1)} {2}
\]
à la réponse (nombre de sous-tribus dans ce segment).
4. Réinitialiser `len = 1` (démarrer un nouveau segment à l'élément actuel).
5. Après la boucle, ajoutez la contribution finale du segment.

La formule `len * (len+1) / 2` est le nombre triangulaire – exactement le nombre de subarrays à l'intérieur d'un tour de longueur strictement croissant `len`.

---

- Oui. 4. Mise en œuvre du code

#### 4.1 Java

"Java
solution de classe publique {
compte long publicSubarrays(int[] nums) {
long total = 0L;
int len = 1; // courant augmentant la longueur du segment

pour (int i = 1; i < nombres de longueur; i++) {
si (nums[i] > nombres[i - 1]) {
len++; // toujours en augmentation
} autre {
total += (long) len * (len + 1) / 2;
len = 1; // lancer un nouveau segment
}
}

// ajouter le dernier segment
total += (long) len * (len + 1) / 2;
le total des retours;
}
}
«» "

4.2 Python

'`python
Solution de classe:
def countSubarrays(self, nombres: List[int]) -> Int:
Total = 0
longueur = 1 # courant augmentant la longueur d'exécution

pour i dans la plage(1, len(nums)):
si nombres[i] > nombres[i - 1]:
longueur += 1
Sinon:
Total += longueur * (longueur + 1) // 2
longueur = 1

Total += longueur * (longueur + 1) // 2
retour total
«» "

### 4.3 C++

'`cpp
solution de classe {
public:
long long compteSubarrays(vector<int>& nums) {
long total = 0;
longueur longue len = 1; // longueur du courant

pour (size_t i = 1; i < nums.size(); ++i) {
si (nums[i] > nombres[i - 1]) {
++len;
} autre {
Total += len * (len + 1) / 2;
len = 1;
}
}
Total += len * (len + 1) / 2; // segment final
le total des retours;
}
};
«» "

Les trois solutions fonctionnent dans **O(n)** temps, utiliser **O(1)** espace supplémentaire, et gérer la taille d'entrée maximale confortablement.

---

- Oui. 5. SEO-Optimized Blog Post

> **Titre**: Code Leet 2393 – Compter des sous-arrachages qui augmentent strictement (Java/Python/C++) Guide de préparation de l'entrevue

> **Meta Description**: LeetCode Master 2393 en minutes. Découvrez la solution O(n) optimale avec le code Java, Python et C++, ainsi que les idées d'entrevue. Boostez votre score d'entrevue de codage!

> **Mots-clés**: LeetCode 2393, Count Strictly Augmenting Subarrays, solution Java, solution Python, solution C++, problème d'entrevue, interview algorithmique, deux-pointer, fenêtre coulissante, conseils d'entrevue d'emploi.

---

Article du blog

---

Quel est le problème ?

LeetCode 2393 vous demande de compter combien de subarrays contigus d'un nombre entier positif sont ** augmentation stricte**. Le tableau peut être aussi long que 100 000 éléments, de sorte qu'un algorithme de force brute O(n2) n'a pas coupé. Les intervieweurs aiment les problèmes qui peuvent être résolus en temps linéaire avec une simple idée de fenêtre coulissante – exactement ce que celui-ci offre.

---

Pourquoi faut-il apprendre ?

- ** Glissement classique Fenêtre**: Montre la maîtrise des techniques *deux-pointeurs*.
- **Nombres triangulaires** : Démontre la capacité de connecter les combinatoires au traitement des tableaux.
- **Time & Space Efficiency**: Une vitrine parfaite pour les intervieweurs qui recherchent un code optimal.

---

Solution étape par étape (O(n) Temps, O(1) Espace)

1. **Démarrer** avec `len = 1` (un seul élément augmente toujours).
2. **Loop** du deuxième élément à la fin :
- Si `nums[i] > nums[i-1]`, incrément `len`.
- Sinon, le segment croissant se termine.
* Ajouter `len * (len + 1) / 2` à la réponse.
* Réinitialiser `len = 1`.
3. Après la boucle, ajoutez la dernière contribution du segment.
4. **Retour** le total.

La principale perspicacité : **Chaque longueur croissante contiguë `len` contribue exactement `len*(len+1)/2` subarrays** – la somme des premiers `len` nombres naturels.

---

Extraits de code

Code complet
C'est pas vrai.
**Java**
[Voir le code](#)
[Voir le code](#)

*(Insérer les blocs de code de la section 4 ici.) *

---

### -Les pièges communs et comment les éviter

Une erreur Pourquoi ça fait défaut
- C'est quoi ?
Autres Oublier le dernier segment après la boucle.La dernière course croissante ne sera jamais comptée.
En utilisant `int` pour la réponse. Autres
Vérification `>=` au lieu de `>` L ' égalité rompt la rigueur Autres

---

Les bons, les mauvais, les méchants

Catégorie Exemple Que faire
- C'est quoi ?
**Bon**Sliding-window + formule triangulaire
**Modalité **Modalités Doubles boucles imbriquées (O(n2) temps, impossible pour 105 éléments)
**Ugly**=++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

---

Pourquoi ce problème impressionne les intervieweurs

- **Profondeur algorithmique**: Il teste la compréhension du nombre de *subarray* et de *combinatoires*.
- **Optimisation** : vous pouvez passer d'une force brute évidente à une solution O(n) élégante.
- **Qualité du code**: Votre mise en œuvre devrait être claire, éviter le débordement, et gérer les cas bord gracieusement.

---

Autres lectures et ressources

- [LeetCode 2393 sur la plateforme](https://leetcode.com/problèmes/count-strictly-crowing-subarrays/)
(https://www.interviewbit.com/blog/two-pointer-technique/)
- **Nombres triangulaires**: [Wikipedia] (https://en.wikipedia.org/wiki/Triangular_number)

---

À emporter

LeetCode 2393 est un micro-classique : une prémisse simple mais une aire de jeux parfaite pour pratiquer les fenêtres coulissantes, le comptage combinatoire et la manipulation soigneuse des débordements entiers. Maîtrisez-le, et vous aurez un point de discussion solide dans toute entrevue de codage. Bonne chance ! C'est ce qu'il a dit.

---

**Mots clés**: LeetCode 2393, Count Strictly Augmenting Subarrays, solution Java, solution Python, solution C++, prép d'entrevue, fenêtre coulissante, bi-pointer, interview algorithme, complexité temporelle, complexité spatiale, entretien d'emploi.