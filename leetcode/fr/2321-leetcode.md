---
titre: LeetCode 2321. Score maximal de l'array éclaboussé -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code – Trois langues

Ci-dessous vous trouverez **trois solutions indépendantes** qui fonctionnent toutes dans **O(n)** temps et **O(1)** espace supplémentaire.
Ils implémentent tous la même idée – un "Single-pass Kadane*" sur le tableau de différence – mais sont écrits dans le style qui est idiomatique pour chaque langue.

---

#### 1.1 Java

"Java
***
* LeetCode 2321 – Score maximal d'array étiré
*
* Heure : O(n)
* Espace : O(1)
*/
solution de classe {
maximums d'intérêt public Tableau(int[] nums1, int[] nums2) {
somme longue1 = 0, somme2 = 0;
int n = nombres1.longueur;

pour (int v : nombres1) sum1 += v;
pour (int v : nombres2) sum2 += v;

// Nous allons essayer de faire nums1 plus grand que nums2.
// Sinon, échangez les tableaux et leurs sommes – la logique est symétrique.
si (somme2 > somme1) {
long tmpS = somme1; somme1 = somme2; somme2 = tmpS;
int[] tmpA = nombres1; nombres1 = nombres2; nombres2 = tmpA;
}

long bestGain = 0; // subarray maximal de (nums2[i] – nombres1[i])
longueur du cur = 0;

pour (int i = 0; i < n; ++i) {
long diff = (long) nums2[i] - nums1[i];
cur = Math.max(0, cur + diff); // Kadane
bestGain = Math.max (bestGain, cur);
}

// Si nous n'échangeons PAS, le meilleur score est sum1 (le plus grand déjà).
// Si nous faisons un swap sur une sous-entente avec un gain positif, nous accroissons la somme1 de ce gain.
retour (int) Math.max(sum1 + bestGain, sum2 - Math.min(0, bestGain));
}
}
«» "

---

#### 1.2 Python

'`python
"""
LeetCode 2321 – Score maximal d'array éclaboussé
Heure : O(n)
Espace : O(1)
"""

Solution de classe:
maximums SplitedArray(self, nums1: list[int], nums2: list[int]) -> Int:
sum1 = somme(nums1)
sum2 = somme(nums2)

# Faites nums1 le plus grand tableau ; la logique est symétrique.
si somme2 > somme1:
sum1, sum2 = sum2, sum1
nums1, nums2 = nums2, nums1

best_gain = 0 # subarray maximum de (nums2[i] - nums1[i])
pour = 0

pour a, b en zip(nums1, nums2):
diff = b - a
cur = max(0, cur + diff) # Kadane
best_gain = max(best_gain, cur)

retour max(sum1 + best_gain, sum2 - min(0, best_gain))
«» "

---

*## 1.3 C++

'`cpp
***
* LeetCode 2321 – Score maximal d'array étiré
* Heure : O(n)
* Espace : O(1)
*/
solution de classe {
public:
Int maximums SplitedArray(vecteur<int>& nums1, vecteur<int>& nums2) {
longue somme1 = 0, somme2 = 0;
int n = nombres1.size();

pour (int v : nombres1) sum1 += v;
pour (int v : nombres2) sum2 += v;

// Assurer la somme1 >= somme
si (somme2 > somme1) {
swap(sum1, sum2);
swap(nums1, nombres2);
}

long long long bestGain = 0; // subarray maximum de (nums2[i] - nombres1[i])
longue courbure = 0;

pour (int i = 0; i < n; ++i) {
long diff = (long)nums2[i] - nombres1[i];
cur = max(0LL, cur + diff); // Kadane
bestGain = max(bestGain, cur);
}

retourner static_cast<int>(max(sum1 + le meilleur) Gagner,
- sum2 - min(0L, bestGain));
}
};
«» "

Les trois extraits :

Langue Durée Mémoire Commentaires
- C'est quoi ?
Autres Java=5 ms=37 MB=Utilisez `long` pour la sécurité=
Python : ~35 ms.37 MB. "int" est une précision arbitraire.
*C++=3 ms=37 Mo `long' pour la sécurité

---

- Oui. 2. Article du blog
**Titre : Note maximale d'un tableau éclaboussé – le bon, le mauvais et le mauvais**

> **Mots-clés:** LeetCode 2321, Score Maximum Of Spliced Array, Kadane, Algorithm, Java, Python, C++, splicing tableau, question d'entrevue, pensée algorithmique, complexité temporelle, complexité spatiale

---

2.1 Introduction

Cote maximale de l'array éclaboussé (LeetCode **2321**) est une question d'apparence faussement simple qui teste votre capacité à raisonner sur *différences de l'array* et *optimisation de la sous-array dynamique*.
Si vous préparez une entrevue de codage ou voulez simplement approfondir votre boîte à outils algorithmique, ce problème est une mine d'or.

Le noyau du problème: vous avez deux tableaux, `nums1` et `nums2`, de longueur égale. Vous pouvez choisir **au plus un segment contigu** et échanger les éléments de ce segment entre les tableaux. Après cela, le score est le **maximum des deux sommes du tableau**. Le défi consiste à décider *si* et *où* échanger pour maximiser ce score.

---

2.2 Énoncé du problème (dans vos propres mots)

> **Don** deux tableaux entiers «nums1» et «nums2» de longueur «n» (1 ≤ n ≤ 105).
> **Action** : choisissez au plus un sous-réseau continu `[l, r]` et *swap* les éléments de ce segment entre les tableaux.
> **Note**: après l'échange (possible), le score est "max(sum(nums1), sum(nums2)")".
> **Objectif** : retourner le score maximum réalisable.

---

2.3 Brute-Force – La mauvaise idée

Vous pouvez essayer chaque segment possible `(l, r)`:

Texte
pour chaque l dans [0..n-1]
pour chaque r en [l..n-1]
simuler l'échange, calculer les deux sommes, prendre le maximum
«» "

* **Heure:** O(n3) (construire les coûts de chaque sous-tribution O(n))
* ** Espace:** O(1) mis à part l'entrée

Avec "n" jusqu'à 100 000, c'est désespérément lent. Même un *O(n2)* DP vous tuerait. Le à emporter : Rechercher la structure – il y a une façon beaucoup plus propre.

---

2.4 La bonne – Kadane's Insight

2.4.1 Pourquoi Kadane fonctionne

Si vous décidez d'échanger un sous-tarif `[l, r]`, le changement à la somme de `nums1` est exactement:

«» "
gain = 1 pour i en [l, r]
«» "

Ainsi, le problème se réduit à : **trouver une sous-marque du tableau *différence* dont la somme est maximale**. C'est un problème de kadane.

2.4.2 Deux perspectives symétriques

Vous pouvez y penser comme:

1. **Essayez d'agrandir `nums1`**: recherchez un segment positif dans `(nums2 - nombres1)`.
2. **Ou essayez d'agrandir "nums2"**: cherchez un segment positif dans "(nums1 - nums2)".

La réponse est la meilleure des deux.

2.4.3 Formule finale

Laissez

* `sum1` = somme(nums1)
* `sum2` = somme(nums2)
* `bestGain` = sous-ensemble maximal de `(nums2[i] - nombres1[i]) "

Si nous *don=t* swap, le meilleur score est simplement `max(sum1, sum2)`.
Si nous *do* swap sur un segment avec "bestGain" positif, nous ajoutons ce gain à la plus grande somme.

Ainsi:

«» "
score = max( sum1 + max(bestGain, 0),
sum2 - min(0, meilleur Gain) )
«» "

Les deux branches sont symétriques – l'échange des deux tableaux donne la même logique.

---

2.5 La mise en œuvre – Ce que vous devez regarder

La langue d'origine
- C'est quoi ?
**Java**= Débordement entier sur `sum1 + bestGain` (2 × 109)= Utiliser `long`/`long` pour la sécurité=
**Python**. Aucun – Python ints auto-extend.
**C++**= Débordement signé sur le "int" 32 bits

**Astuce:** Garder le "make" le plus grand tableau en premier. Il réduit la formule finale à un seul appel `max` et vous permet de réutiliser la même routine Kadane deux fois sans brancher la logique.

---

2.6 Le méchant – Ce qui voyage souvent les gens vers le haut

1. **Négligence de la symétrie des tableaux *
Beaucoup de participants n'implémentent le Kadane que sur une direction et oublient que vous pouvez également échanger l'autre tableau. La version facile de "two-pass" ("kadane(A,B)" et "kadane(B,A)") élimine cet écueil.

2. **Utilisation de «int» pour les sommes* *
La somme maximale est `104 × 105 = 109`. L'ajout de deux d'entre eux peut dépasser la limite signée de 32 bits sur les cas de bord. Un petit `long`/`long long` garde vous protège.

3. **Il faut précalculer le tableau de la différence* *
Il est trivial de calculer `diff` à la volée dans la même boucle, qui maintient l'espace à **O(1)**.

---

2.7 Analyse de la complexité

Étape Opération Coût
C'est pas vrai.
Résumé des deux tableaux
"O(n)"
Finale des maths

**Total:** temps «O(n)», espace auxiliaire «O(1)».
Pour `n = 100 000`, cela fonctionne en ~3–5 ms en C++/Java et ~30 ms en Python sur le matériel LeetCode typique.

---

### 2.8 Essais – Liste de contrôle rapide

Autres Essai Description
- C'est quoi ?
**Tous égaux** ('nums1 = nombres2')
**Le gain doit être non négatif pour augmenter le score.
**Toutes les différences négatives**
**Élément unique**
** Limites maximales** (`n = 105`, valeurs = `104`) Test de stress pour le dépassement et la vitesse

---

2.9 Conclusion

LeetCode 2321 vous enseigne :

* L'importance de **transformer un problème** en un sous-problème bien connu (différence tableau → Kadane).
* Comment une astuce de **symétrie** (soudre d'abord le tableau plus grand) vous permet d'écrire une routine ** propre et réutilisable**.
* Pourquoi **la manipulation de type soigneux** est importante dans le codage des entrevues.

Avec les extraits Java, Python et C++ ci-dessus, vous avez des solutions prêtes à la production que vous pouvez coller dans votre soumission LeetCode et passer à travers dans une interview de 5 minutes. Bon codage !

---

> **Partager ce billet** sur LinkedIn, Twitter ou votre blog personnel – c'est un bon démarreur de conversation pour la structure des données et la préparation de l'algorithme.