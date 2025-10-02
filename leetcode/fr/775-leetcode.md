---
Titre: LeetCode 775. Inversions globales et locales -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Inversions globales contre inversions locales – LeetCode 775
- Oui. Le problème de la permutation (Java, Python et C++)

> **Problème** – LeetCode 775
> Compte tenu de la permutation de la longueur `n` (valeurs `0 ... n‐1`), retourner `true` si le nombre d'inversions globales est égal au nombre d'inversions locales.

---

- Oui. 1. La solution monoligne (temps O(n), espace O(1))

Le point de vue clé :

*Toute inversion globale doit également être une inversion locale. *
Si un élément est déplacé par plus d'une position à partir de son indice de l'idéal, une inversion globale non locale apparaîtra et les nombres ne pourront jamais être égaux.

Ainsi la vérification se réduit à:

Texte
abs(nums[i] - i) <= 1 pour chaque i
«» "

Si la condition est remplie pour tous les indices, retourner `true`; sinon `faux`.

### Java

"Java
solution de classe publique {
public booléen isIdealPermutation(int[] nums) {
pour (int i = 0; i < nombres de longueur; i++) {
si (Math.abs(nums[i] - i) > 1) {
retourner faux;
}
}
retour vrai;
}
}
«» "

Python

'`python
Solution de classe:
def isIdealPermutation(self, nombres: List[int]) -> bool:
retourner all(abs(nums[i] - i) <= 1 pour i dans l'intervalle(len(nums)))
«» "

C++

'`cpp
solution de classe {
public:
Bool isIdealPermutation(vector<int>& nums) {
pour (int i = 0; i < nums.size(); ++i) {
Si (abs(nums[i) - i) > 1) retourner faux;
}
retour vrai;
}
};
«» "

> **Complexité temporelle** – `O(n)` (analyse unique)
> **Complexité spatiale** – « O(1) » (en place)

---

- Oui. 2. La Force Brute – Quand vous avez besoin d'une référence

Une double boucle `O(n2)` naïve peut être utile pour le débogage ou lorsque la taille du tableau est minuscule.

"Java
int local = 0, global = 0;
pour (int i = 0; i < n - 1; i++) si (nums[i] > nombres[i+1]) local++;
pour (int i = 0; i < n; i++)
pour (int j = i+1; j < n; j++)
si (nombres[i] > nombres[j]) global++;
retour local == global;
«» "

*Pros:* Facile à comprendre, pas de tours cachés.
*Cons:* Trop lent pour `n = 105'. Utilisez seulement pour les petits cas d'essai ou comme un contrôle de la santé mentale.

---

- Oui. 3. L'approche optimale – l'hommage de la sur-ingénierie

Certaines solutions de pointe utilisent un astuce *prefix-maximum* pour détecter une inversion globale non locale sans vérification absolue. L'idée :

Texte
Si max(nums[0..i]) > nombres[i+1] → inversion globale non locale.
«» "

Bien qu'élégant, il ajoute un petit peu de comptabilité supplémentaire et est moins intuitif que le contrôle de distance absolu. Pour les intervieweurs, la solution plus simple `abs(nums[i] - i)` est préférée.

---

- Oui. 4. Pourquoi ce problème compte dans les entrevues

1. **Insight algorithmique** – Affiche la capacité de penser aux permutations et aux propriétés d'inversion.
2. ** Optimisation de l'espace continu** – Démontre que l'espace O(1) est souvent suffisant.
3. **Clean Code** – Une logique monoligne peut impressionner lorsqu'elle est présentée avec un raisonnement approprié.
4. **Maîtrise multi-langue** – Être capable d'écrire la même logique en Java, Python et C++ prouve sa polyvalence.

---

- Oui. 5. Aperçu de l'article sur le blog

Vous trouverez ci-dessous un article prêt à coller dans un blog Medium, Dev.to ou un portfolio personnel. Le contenu est riche en mots clés, structuré pour la lisibilité, et comprend une méta description pour une visibilité maximale.

---

Billet de blog : Inversions globales et locales – Comment cracker le LeetCode 775 en Java, Python & C++

**Meta Description (pour les moteurs de recherche)* *
> Master LeetCode 775 – Inversions globales et locales. Apprenez l'astuce de permutation idéale, lisez une solution Java, Python & C++ et comprenez pourquoi elle est incontournable pour les entretiens d'ingénierie logicielle.

---

Introduction

Si vous avez broyé LeetCode, vous avez probablement rencontré **LeetCode 775 – Global vs. Inversions locales**. C'est faussement simple : une permutation de "0...n‐1", vérifiez si les inversions globales sont égales aux inversions locales. Pourtant, ce petit problème est un projet *classique d'interview pour animaux de compagnie* qui peut mettre en valeur votre pensée algorithmique et vous donner une victoire d'interview rapide.

Pourquoi est-ce utile ?
- **Les fondamentaux de la permutation** – Les inversions sont un concept central dans le tri et l'analyse par algorithme.
- **Élégance d'un liner** – Les intervieweurs aiment les solutions propres, O(n) qui fonctionnent dans un espace constant.
- ** Pensée de cas** – Spotting qu'une valeur doit rester à l'intérieur d'un indice à l'écart de son spot idéal de train vous pour repérer des contraintes cachées.

Laissez passer les parties *good*, *bad* et *ugly* de ce problème, montrez comment le mettre en œuvre en Java, Python et C++, et terminez avec des conseils prêts à l'entrevue.

---

## -Déclaration du problème (reformulé)

Vous êtes donné un tableau `nums` de longueur `n` qui est une permutation de `0 ... n‐1`.
- **Inversion mondiale** – paire `(i, j)` où `i < j` et `nums[i] > nums[j]`.
- **Inversion locale** – paire `(i, i+1)` où `nums[i] > nums[i+1]`.

Retourner `true` si **inversions globales = inversions locales**.

---

C'est pas vrai. Naïve Brute Force (bon mais lent)

"Java
int local = 0, global = 0;
pour (int i = 0; i < n-1; i++) si (nums[i] > nombres[i+1]) local++;
pour (int i = 0; i < n; i++)
pour (int j = i+1; j < n; j++)
si (nombres[i] > nombres[j]) global++;
retour local == global;
«» "

- **Bien**: Facile à suivre, pas de maths difficiles.
- **Bad**: O(n2) – sera temps-out pour `n = 100 000`.
- **Ugly**: Pas évolutive, mais bon pour les tests de santé mentale.

---

La solution optimale – La solution idéale

**Observation** – Dans une permutation, l'indice de la valeur `v` est `v` lui-même.
Si une valeur déplace plus d'un endroit, vous créez une inversion globale qui est *pas* locale.

Donc :

Texte
<= 1 pour tous
«» "

Si la condition se maintient partout, les inversions locales et mondiales correspondent.

**Java**

"Java
public booléen isIdealPermutation(int[] nums) {
pour (int i = 0; i < nombres de longueur; i++) {
si (Math.abs(nums[i] - i) > 1) retourner faux;
}
retour vrai;
}
«» "

**Python**

'`python
retourner all(abs(nums[i] - i) <= 1 pour i dans l'intervalle(len(nums)))
«» "

**C++**

'`cpp
pour (int i = 0; i < nums.size(); ++i)
Si (abs(nums[i) - i) > 1) retourner faux;
retour vrai;
«» "

- **Heure**: "O(n)"
- **Espace**: "O(1)"

C'est l'approche *bonne* optimale : rapide, simple, et n'utilise qu'une quantité constante de mémoire.

---

L'alternative "Ugly" : préfixe-maximum Vérification

Certaines solutions maintiennent la valeur maximale vue jusqu'à présent:

Texte
si (max_so_far > nums[i+1]) → inversion globale non locale.
«» "

'`cpp
int max_so_far = INT_MIN;
pour (int i = 0; i < nums.size()-1; ++i) {
si (max_so_far > nums[i+1]) retourner faux;
max_so_far = max(max_so_far, nombres[i]);
}
retour vrai;
«» "

- **Pros**: Pas d'appel `abs()`, un peu de logique supplémentaire.
- **Cons**: Moins lisible, nécessite de penser au préfixe maxima.
- **Quand utiliser**: Lorsque vous voulez éviter `abs()` dans un cadre d'entrevue qui pénalise les appels de maths, mais le liner unique est généralement plus facile à interviewer.

---

Résumé de la complexité

L'approche Temps Espace
- C'est quoi ?
À une distance absolue
Préfixe maximal O(n) O(1)
Défaut de force

---

## -Pièges et bords communs Liste de contrôle des cas

Piège
- Oui.
**Utilisation `>` au lieu de `>=`** – La condition doit être *strictement* `<= 1''.- Utiliser `Math.abs(nums[i] i) > 1 ' (Java) ou `abs(nums[i] - i) > 1' (Python/C++). Autres
**Overflow** – `abs()` sur `Integer.MIN_VALUE` est problématique en Java. Autres
**Misreading -local --global -local est toujours entre indices consécutifs. Double-vérifiez votre définition si vous mettez en œuvre la force brute. Autres
**Test sur tableau vide** – Garantie de problème `n ≥ 1`, mais garde contre `nums.longueur== Ajouter un "si" trivial (longueur en chiffres) 0) retourner vrai;». Autres

---

Conseils pour l'entrevue

1. ** Expliquez d'abord le point de vue** – Toutes les inversions globales non locales nécessitent qu'un élément soit déplacé par > 1.
2. **Afficher le simple code O(n)** – Éviter toute complexité inutile.
3. ** Temps/espace** – Les intervieweurs veulent toujours un grand O résumé.
4. **Demander des éclaircissements** – par exemple, le tableau est-il toujours une permutation?
5. **Optionnel: Afficher la force brute** – Aide à démontrer que vous comprenez parfaitement la définition du problème.

---

Liste de contrôle du référencement

Mot-clé
C'est quoi, ça ?
Titre, introduction, énoncé de problème
Global vs. Inversions locales
Section du problème, commentaires de la solution
Autres En-tête du code Java
Solution Python En-tête de code Python
Solution C++
Conclusion, conseils d'entrevue
Entretien de l'ingénieur logiciel
Interview algorithmique

**Meta Description (pour les moteurs de recherche): * *
> Crack LeetCode 775 – Inversions globales et locales. Lisez la solution de permutation idéale O(n) en Java, Python et C++ avec une explication claire, une analyse du temps/de l'espace et des conseils prêts à l'entrevue. Parfait pour les entrevues d'ingénierie logicielle.

---

Les pensées finales

- **Bon** – Le problème vous oblige à raisonner sur les permutations et les comptes d'inversion.
- **Bad** – Une solution "O(n2)" naïve est trop lente pour les contraintes mais excellente pour l'apprentissage.
- **Ugly** – La sur-ingénierie avec préfixe-max ou les arbres indexés binaires rend le code moins lisible; gardez-le simple.

En maîtrisant le monoligneur, vous pourrez ** résoudre le LeetCode 775 dans une interview** en moins de 30 secondes et impressionner l'intervieweur avec une solution propre et optimale.

Bon codage – et bonne chance pour ce prochain rôle d'ingénierie logicielle!