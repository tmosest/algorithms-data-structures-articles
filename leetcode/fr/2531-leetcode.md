---
titre: LeetCode 2531. Faire le nombre de caractères distincts égaux -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Réponse courte** – oui.
Vous pouvez décider de la réponse dans *O(=w1=+=w2=* en examinant uniquement
fréquence de chaque lettre (il n'y en a que 26).
L'idée clé est de suivre le *nombre de lettres uniques* dans chaque chaîne
(`c1` et `c2`) et voir ce qui arrive à ces nombres lorsque vous échangez deux
Des lettres.

---

- Oui. Pourquoi la force brute est inutile

Si nous essayions littéralement chaque paire de positions dans `w1` et `w2` nous ferions
besoin

«» "
(')
«» "

les opérations.
Parce qu'un swap ne peut affecter que le *type* des deux lettres impliquées
(`a` de `w1` et `b` de `w2`), l'effet dépend uniquement de la
*fréquence* de `a` dans les deux chaînes et de `b` dans les deux chaînes.
Il n'y a que 26 lettres possibles, nous pouvons donc essayer toutes les paires `26 × 26`
et calculer l'effet en temps constant.

---

- Oui. Ce qui change lorsque nous échangeons `a` (à partir de `w1`) avec `b` (à partir de `w2`)

Situation Répercussions sur le compte *unique-lettre* de la chaîne qu'il laisse
-- -- -- -- -- -- -- -- -------------------------------------------------- -- -- -- -- -- -- -- -- --
`a` apparaît **once** dans `w1` → il devient unique après que nous l`avons sorti → *c1–=1**
`a` ne **not** apparaissent dans `w2` → il devient une nouvelle lettre unique dans `w2` → **c2+=1**
`b` apparaît **once** dans `w2` → il devient unique après que nous l`avons sorti → **c2–=1**
`b` ne **pas** apparaissent dans `w1` → il devient une nouvelle lettre unique dans `w1` → **c1+=1**

Si `a` et `b` sont le caractère *same* les deux premières modifications annulent
Nous nous retrouvons avec les mêmes `c1` et `c2` que nous
Commencé avec, donc ce swap ne peut réussir que lorsque `c1 == c2` déjà.

Avec ces règles nous pouvons calculer le nombre *nouveau* de lettres uniques
sans toucher les cordes réelles.

---

- Oui. Implémentation Java (temps O(=w1=+=w2=), espace O(1))

"Java
Importation de java.util.*;

solution de classe publique {

boolean public isItPossible(String w1, String w2) {
// Fréquence de chaque lettre
int[] f1 = nouveau int[26];
int[] f2 = nouveau int[26];

// Compter des lettres uniques dans chaque chaîne
int uniq1 = 0, uniq2 = 0;
pour (charc : w1.toCharArray()) {
si (f1[c - 'a']++ == 0) uniq1++;
}
pour [charc : w2.àCharArray()] {
si (f2[c - 'a']++ == 0) uniq2++;
}

/* Sortie anticipée : si la différence est > 2, un swap peut changer
le nombre par au plus 2 (supprimer un char unique et/ou ajouter un
nouveau char unique). Si c'est impossible de porter les deux chefs d'accusation
à l'intérieur de 2, la réponse est définitivement fausse. */
si (Math.abs(uniq1 - uniq2) > 2) retourner faux;

/* Essayez chaque paire (a de w1, b de w2) */
pour (int a = 0; a < 26; a++) {
si (f1[a]] 0) continuer; // a doit exister en w1

// copier le compte unique pour ceci a
Int newUniq1 = uniq1;
Int newUniq2 = uniq2;

// Enlever un de w1
si (f1[a]] 1) nouveauUniq1--; // a était unique
si (f2[a]] 0) newUniq2++; // a est nouveau dans w2

pour (int b = 0; b < 26; b++) {
si (f2[b]] 0) continuer; // b doit exister en w2

int curUniq1 = nouveauUniq1;
int curUniq2 = nouveauUniq2;

// Si a == b nous échangeons la même lettre
si a) b) {
// Dans ce cas, nous avons déjà traité l'effet de
// enlevant a de w1, en l'ajoutant à w2. Pas de changement
// aux comptages uniques – nous n'avons qu'à vérifier
// si les nombres actuels sont déjà égaux.
si (curUniq1 == curUniq2) retourne vrai;
poursuivre;
}

// Ajouter b à w1
si (f1[b]] 0) curUniq1++; // b est nouveau dans w1

// Supprimer b de w2
si (f2[b]] 1) curUniq2--; // b était unique

/* Maintenant curUniq1 / curUniq2 sont les comptes uniques après
échange a avec b. S'ils correspondent, nous avons trouvé un
échange valide. */
si (curUniq1 == curUniq2) retourne vrai;
}
}
retourner faux; // aucune paire n'a réussi
}
}
«» "

- Oui. Comment ça marche – étape par étape

1. **Tableaux de fréquence de construction** – O(=w1=+=w2=).
«f1[i]» est le nombre de fois que la lettre `'a'+i` apparaît dans `w1`;
«f2[i]» fait la même chose pour "w2".

2. **Couvercle des lettres uniques** – une lettre est unique si sa fréquence
est exactement 1.
Cela nous donne `uniq1` et `uniq2`.

3. **Élagage précoce** – si `'uniq1 – uniq2=" > 2`, nous pouvons retourner `faux "
immédiatement.

4. **Énumérer les 26×26 paires** – pour chaque `a` qui apparaît dans `w1`
et chaque `b` qui apparaît dans `w2` nous calculons l'effet sur les deux
La lettre unique compte à l'aide du tableau ci-dessus.
Toutes les opérations à l'intérieur des boucles sont à temps constant, donc le total
le temps est `26 × 26 = 676`, c'est-à-dire **O(1)** par rapport à la chaîne
longueurs.

5. **Retour** – la première paire qui donne des chiffres égaux est un succès;
Si nous épuisons toutes les paires, nous retournons "faux".

---

Complexité

- **Temps** – `O(=w1=" +=w2=") pour la construction des tables de fréquence, plus
la boucle constante de 26×26 (676 étapes).
Donc le temps de fonctionnement global est linéaire dans la taille d'entrée.

- **Espace** – nous utilisons deux tableaux de longueur 26, c'est-à-dire `O(1)` supplémentaire
mémoire.

---

À emporter

Vous n'avez pas besoin d'essayer chaque position dans les cordes.
Parce que seule la matière *lettre types* pour la lettre unique compte,
vous pouvez analyser l'effet d'un swap unique en temps constant et
Essayez toutes les paires de lettres `26 × 26` possibles. Le résultat est
L'algorithme d'O(=w1=+=w2=) qui est à la fois simple à implémenter et facile à
Compris.