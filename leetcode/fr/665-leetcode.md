---
titre: LeetCode 665. Tableau non décroissant -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
665 – Non-diminution Tableau
> **Difficulté:** Moyenne
> **Signature:** "contrôle public du booléenPossibilité(int[] nums)"

---

Récapitulation du problème
On vous donne un nombre entier. Vous pouvez changer **au plus un élément** à toute valeur que vous voulez. Après le changement, le tableau doit devenir **non-diminution** (`nums[i] ≤ nombres[i+1]` pour tous les 'i' valides).

Return `true` si c'est possible, sinon `faux`.

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
Changement `4` → `1`.
Aucun changement ne peut corriger les deux diminutions. Autres

**Contrôles* *

1 ≤ n ≤ 104
Autres

---

## Aperçu de la solution

Le tableau est **seulement -- presque - trié** – au plus une violation `nums[i] < nums[i‐1]` est autorisée.
La clé est de décider *comment* pour réparer une violation:

* **Option 1** – Bas «nums[i‐1]» à «nums[i]».
* **Option 2** – Élever «nums[i]» à «nums[i‐1]».

Les deux peuvent être valides en fonction des nombres environnants (`nums[i-2]` et `nums[i+1]`).
Si vous touchez une deuxième violation ou une situation où l'option *ni l'une ni l'autre* garde la séquence triée, la réponse est "faux".

L'algorithme est un seul balayage linéaire, le temps O(n) et l'espace O(1).

---

Code Pseudo

«» "
pour i de 1 à n-1
si nombres[i] < nombres[i-1] // trouvé une diminution
si nous avons déjà vu une diminution
retourner faux
i i>1 et i<n-1 et nums[i-2] > nums[i] et nums[i+1] < nums[i-1]
retour faux // les deux côtés seraient encore mal
marque que nous avons vu une diminution
retour vrai
«» "

La condition `nums[i-2] > nums[i]` signifie que nous devrions *relever* `nums[i]` pour garder le côté gauche trié, alors que `nums[i+1] < nums[i-1]` signifie que nous devrions *inférieur* `nums[i-1]` pour garder le côté droit trié.
Si les deux sont vrai, aucun choix ne fonctionne → impossible.

---

Code

### Java

"Java
solution de classe {
contrôle public booléenPossibilité(int[] nums) {
pour (int i = 1, err = 0; i < nombres.longueur; i++) {
si (nums[i] < nums[i - 1]) {
// Deuxième violation
si (err++ > 0) retourner faux;
// Situation YABY – ne peut pas corriger
si (i > 1 && i < nombres.longueur - 1 &&
nombres[i - 2] > nombres[i] && nombres[i + 1] < nombres[i - 1]) {
retourner faux;
}
}
}
retour vrai;
}
}
«» "

Python 3

'`python
Solution de classe:
def checkPossibilité(self, nombres: list[int]) -> C'est vrai.
erreur = 0
pour i dans la plage(1, len(nums)):
si des nombres [i] < nombres[i - 1]:
en cas d'erreur ou (i > 1 et i < len(nums) - 1 et
nombres[i - 2] > nombres[i] et nombres[i + 1] < nombres[i - 1]):
Retour Faux
erreur = 1
retour Vrai
«» "

### C++ (C++17)

'`cpp
solution de classe {
public:
Possibilité(vecteur<int>& nums) {
pour (int i = 1, err = 0; i < nums.size(); ++i) {
si (nums[i] < nums[i - 1]) {
si (err++) (i > 1 && i < nums.size() - 1 &&
nombres[i - 2] > nombres[i] && nombres[i + 1] < nombres[i - 1])
retourner faux;
}
}
retour vrai;
}
};
«» "

Les trois implémentations fonctionnent en **O(n)** temps, **O(1)** espace auxiliaire, et correspondent à la stratégie gourmande décrite ci-dessus.

---

Article de blog: Le bon, le mauvais, et le mauvais de LeetCode 665

### Titre (SEO-optimisé)
**Comment cracker LeetCode 665 – Non-décroissant Array : le bon, le mauvais, et le mauvais (Java, Python, C++)* *

Description de la méta
Maître LeetCode 665 en quelques minutes ! Apprenez la solution avide intuitive, pièges à éviter, et Java complet, Python, C++ code. Augmentez votre préparation d'entrevue de codage et atterrissez votre emploi de technologie de rêve.

---

Introduction
* LeetCode="s "Presque Trié" les problèmes sont un endroit doux pour les intervieweurs.
* Le problème 665 demande: **Un seul élément peut-il corriger un tableau presque trié? * *
* Nous allons parcourir le raisonnement, les pièges et une solution prête à la production en Java, Python et C++.

> *Mots clés:* LeetCode 665, Non-Decreasing Array, codage d'entrevue, problème algorithmique, solution gourmande, codage Java, codage Python, codage C++, structures de données, préparation d'entrevue.

---

Les bons

Autres Ce qui est grand Pourquoi il aide
C'est quoi ?
**Contraintes d'entrée claires**= Facile à raisonner sur les limites de temps et d'espace. Autres
Autres **Single Pass Greedy**= Un favori d'interview classique – montre que vous pouvez penser en temps O(n). Autres
Autres **Élégant contrôle de l'Edge-Case** . La condition `nums[i-2] > nums[i] && nums[i+1] < nums[i-1]` est un seul liner qui capture tous les modes de défaillance. Autres
**Language-agnostic** ► Même logique en Java, Python et C++; montre la polyvalence du langage. Autres

À emporter
Une solution propre et cupide d'O(n) est souvent la *la plus facile à interviewer* car elle démontre :

* Une pensée efficace
* Attention aux détails avec les cas bord
* Capacité d'écrire un code concis, sans bug

---

Les mauvais

Comment le corriger ?
C'est quoi ?
**Misreading -modify au plus un élément**- Il n'est pas -swap deux éléments; vous pouvez changer à n'importe quelle valeur. Oublier cela conduit à de mauvaises solutions qui essaient de *swap* au lieu de *set*. Autres
**Sur-optimiste. ou l'élévation de «nums[i]» peut encore casser la paire suivante. Vérifiez toujours `nums[i-2]` et `nums[i+1]`. Autres
**Compenser les violations incorrectement**=Certains débutants utilisent `i++` incorrectement et finissent par manquer la deuxième violation. Autres
**Complexe des modifications dans la place** Préférez une valeur prev *virtuelle* ou gardez simplement un compteur. Autres

** Exemple de piège commun**

'`python
♪ Mauvaise approche : toujours définir nombres[i-1] = nombres[i]
pour i dans la plage(1, len(nums)):
si des nombres [i] < nombres[i-1]:
nombres[i-1] = nombres[i]
retour Vrai
«» "

Cela échoue sur `[3,4,2,3]`. Le côté gauche devient `[3,4,2]` → toujours en baisse.

---

# # # Les affreux

1. **Misinterprétation de "non-diminution" par rapport à "progression stricte"* *
*La non-diminution* permet l'égalité (‘. Un bug subtil : utiliser `<` partout rejettera incorrectement les tableaux comme `[1,1]`.

2. **Délai sur les gros intrants**
Si vous écrivez une boucle imbriquée O(n2) (p. ex., en essayant toutes les modifications possibles), la solution frappera la limite de 2 s de LeetCode sur les tableaux 104 éléments.

3. **Utilisation inutile de l'espace**
Créer une copie du tableau pour chaque tentative d'édition double l'utilisation de la mémoire et ralentit en raison de caches manquants.

4. ** Lire la mauvaise réponse de la communauté* *
De nombreux billets de blog prétendent changer de "nums[i]` en "nums[i-1]" aveuglément. Cela n'est correct que lorsque «nums[i-2] ≤ nums[i]».
La situation "YABY" est la laid *réelle* – les deux côtés sont toujours brisés si vous choisissez le mauvais côté.

---

Conseils d'entrevue

Conseil Pourquoi ça compte
-- -- -- -- --
**Démarrer avec une définition claire de la violation. Prévient la confusion sur les «nums[i] < nums[i-1]». Autres
Autres **Utilisez un seul compteur (`modifié` / `err`).**=Cette règle est explicite. Autres
Autres **Pensez aux voisins (`i-2`, `i+1`).**.La décision dépend de ces deux éléments. Autres
Autres **Les cas de bords d'essai d'abord. Autres
**Les intervieweurs apprécient les processus de pensée clairs. Autres
**Pratiquez la version du tableau sans modifier la version du tableau** Autres

---

Résumé

LeetCode 665 est un problème classique d'avidité qui récompense:

* ** Pensée linéaire* *
* **Manipulation des bords méticuleuse* *
* **Clarté du langage brut* *

La solution gourmande ci-dessus est le code minimal-overhead, prêt à la production qui fonctionne en Java, Python et C++. Maîtrisez-le, ajoutez-le à votre portfolio, et vous serez prêt à répondre à n'importe quelle question d'entrevue de lecture!

---

** Bon codage !**
* Sentez-vous libre de laisser tomber vos propres prises dans les commentaires, ou faites-moi savoir si vous aimeriez plonger plus profondément dans des variantes de programmation dynamique. *