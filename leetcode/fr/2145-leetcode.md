---
titre: LeetCode 2145. Comptez les séquences cachées -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code (Java / Python / C++) – Taille des séquences cachées

Ci-dessous vous trouverez une solution **pass simple, O(n) / O(1)** pour LeetCode #2145.
Les trois versions utilisent la même astuce de préfixe qui transforme le problème en un simple nombre de gammes.

Langue
C'est pas vrai.
**Java**=Utilisez `long` pour préfixer les sommes pour éviter les débordements, puis jetez la réponse finale à `int`. Autres
**Python**=Loops droites, appels `max()`/`min()` et une seule expression arithmétique. Autres
**C++**=Utilisez `long long`, `std::max`, `std::min` et `std::max(0LL, res)` pour éviter les comptages négatifs. Autres

---

Java

"Java
solution de classe {
Nombre d'entrées publiquesOfArrays(int[] différences, int inférieur, int supérieur) {
somme longue = 0, max = 0, min = 0; // somme préfixe et ses extrémités
pour (int d : différences) {
somme += d;
max = Math.max (max, somme);
min = Math.min (min, somme);
}
// Nombre de valeurs de départ valides
long res = (long) supérieur - inférieur - max + min + 1;
retour (int) Math.max(0L, res);
}
}
«» "

---

Python

'`python
Solution de classe:
Numéro DeArrays(même, différences: Liste[int], inférieure: int, supérieure: int) -> Int:
somme_, max_, min_ = 0, 0, 0
pour d en différences:
somme_ += d
max_ = max(max_, somme_)
min_ = min(min_, somme_)

res = supérieur - inférieur - max_ + min_ + 1
retour max(0, res)
«» "

---

C++

'`cpp
solution de classe {
public:
nombre intOfArrays(vecteur<int>& diff, int inférieur, int supérieur) {
longue somme longue = 0, maxSum = 0, minSum = 0;
pour (int d : diff) {
somme += d;
maxSum = max(maxSum, somme);
minSum = min(minSum, somme);
}
long long res = (long long)upper - inférieur - maxSum + minSum + 1;
retour max(0LL, res);
}
};
«» "

---

Article du blog – Le bon, le mauvais et l'acharnement de compter les séquences cachées

> **SEO Mots-clés**: LeetCode 2145, séquences cachées, somme de préfixe, interview d'algorithme, prép d'entretien d'emploi, solution Java/Python/C++, défi de codage, structures de données, complexité temporelle, complexité spatiale.

---

2.1 Introduction

Si vous préparez une entrevue d'ingénierie logicielle, vous rencontrerez bientôt des problèmes *préfixe-sum*.
Les LeetCodes **2145 – Count the Hidden Sequences** est une illustration parfaite.
Il vous demande de compter combien de tableaux cachés satisfont à un ensemble donné de différences *et* se trouvent dans une plage numérique.
Ci-dessous on décompose le problème en **bon** (ce qui fonctionne), **mauvais** (pièges communs), et le **ugly** (pourquoi il se sent difficile).

> ** Objectif** : Équipez-vous d'une solution propre et efficace et d'une compréhension plus approfondie que vous pouvez expliquer avec confiance dans une entrevue.

---

2.2 Réévaluation des problèmes

Description de l'élément
C'est pas vrai.
"différences" "int[]" de longueur `n`. "différences[i] = caché[i+1] - caché[i]". Autres
Des limites inclusives pour chaque élément du tableau caché. Autres
*Tâche**= Compter le nombre possible de tableaux cachés de longueur `n+1` qui satisfont aux deux contraintes. Retour `0` si aucune n'existe. Autres

---

2.3 Pourquoi le préfixe s'élève à la brillance

Le tableau caché peut être exprimé en termes de valeur de départ `x`:

«» "
caché[0] = x
cache[1] = x + différences[0]
cache[2] = x + différences[0] + différences[1]
...
«» "

La somme **préfixe** de `différences` donne le décalage relatif de `x` à n'importe quel élément.
Laissez :

«» "
préfixe[0] = 0
préfixe[i] = sum_{j=0}^{i-1} différences[j]
«» "

Puis `hidden[i] = x + préfixe[i]`.
Tous les éléments restent à l'intérieur de `[inférieur, supérieur]` **iff**:

«» "
inférieur ≤ x + minPréfixe ET x + maxPréfixe ≤ supérieur
«» "

Réarrangement:

«» "
- minPréfixe ≤ x ≤ supérieure - maxPréfixe
«» "

Ainsi, *chaque entier* `x` dans cet intervalle produit un tableau caché valide.
Le compte est simplement :

«» "
max(0, (en haut - maxPrefix) - (en bas - minPrefix) + 1)
«» "

**C'est la formule magique** derrière la solution.

---

#### 2.4 Le bon – Une solution unique, O(n)

Étape Ce que nous faisons Pourquoi ça compte
- C'est quoi ?
Autres ** Calculer la somme du préfixe, min, max. Autres
**Appliquer la formule**="upper - lower - maxSum + minSum + 1`. Autres
**Guard contre les négatifs** Certains intervalles s'effondrent (par exemple, si `upper < lower - minPrefix`) → retour 0.

> **Résultat**: Les trois extraits de code ci-dessus implémentent cette logique.

---

2.5 Les mauvaises – Erreurs communes

1. **Dépassement**
- "différences" peut être ± 105 et "n" peut être 105.
- "somme" peut atteindre ±1010, ce qui dépasse "int".
- **Fix**: Utilisez `long` (Java/C++) ou `long long` (C++) / entiers Python par défaut (précision arbitraire).

2. **Mélangé min/max**
- Beaucoup de gens échangent accidentellement `minPrefix` et `maxPrefix` dans la formule finale.
- Rappelez-vous: `minPrefix` est le *plus négatif* offset, donc il **expands** la limite inférieure.
- Tester avec un petit exemple (par exemple, `différences = [1, -1]`) pour voir les nombres s'aligner.

3. ** Direction de l'intervalle de frottement**
- L'intervalle peut être vide si `upper - maxPrefix < lower - minPrefix`.
- `max(0, ...)` s`en occupe avec élégance.

4. **En supposant que la réponse corresponde à un "int"**
- Dans ce problème, `upper` et `lower` sont limités à ±105, donc le nombre maximal est ~2·105.
- Mais toujours jeter l'expression arithmétique finale à `long`/`long` avant de revenir, juste au cas où.

---

2.6 La mauvaise – Comprendre la formule

> **Pourquoi c'est contre nature**
> Lorsque vous voyez pour la première fois `upper - lower - max + min + 1`, il n'est pas évident pourquoi il faut soustraire la valeur maximum et ajouter la valeur min.

**Pourquoi les signes apparaissent comme ils le font:**

«» "
nombre = (en haut - maxPréfixe) - (en bas - minPréfixe) + 1
= supérieur - maxPréfixe - inférieur + minPréfixe + 1
= supérieur - inférieur - maxPréfixe + minPréfixe + 1
«» "

Une image mentale utile : imaginez deux murs qui pressent `x`.
Le mur *right* est `upper - maxPrefix`; le mur *left* est `lower - minPrefix`.
Si vous déplacez les deux murs vers l'intérieur, le nombre de points entiers entre eux se rétrécit.
Ce raisonnement visuel apparaît souvent dans les explications d'entrevue – soyez prêt à le dessiner rapidement.

---

2.7 Mise en oeuvre étape par étape (pour les entrevues)

Voici un croquis minimal que vous pouvez coller dans un IDE:

"Java
solution de classe {
numéro d'entrée publiqueOfArrays(int[] diff, int inférieur, int supérieur) {
somme longue = 0, maxSum = 0, minSum = 0;
pour (int d : diff) {
somme += d;
maxSum = Math.max(maxSum, somme);
minSum = Math.min(minSum, somme);
}
long res = (long) supérieur - inférieur - maxSum + minSum + 1;
retour (int) Math.max(0L, res);
}
}
«» "

- Pourquoi "long"?**
Même si les "différences" ≤ 105, une somme cumulée de 105 éléments peut atteindre ±1010, bien en dehors de la plage "int".

- **Pourquoi "max(0, ...)"?**
Un résultat négatif signifie que l'intervalle s'est effondré ; aucun tableau caché n'existe.

---

2.8 Analyse de la complexité

Valeur métrique Commentaire
C'est quoi ?
**Heure** Une seule traversée de "différences". Autres
**Espace** Seulement quelques variables « longues » ; pas de tableaux supplémentaires. Autres
**Taille de la réponse* ≤ `upper - lower + 1` ≤ 200 001. Autres

---

2.9 Cas de bord à tester

Autres Tests attendus Pourquoi ça compte
- C'est quoi ?
Autres Toutes les différences = 0, `inférieure = 5`, `upper = 5`. Autres
"différences = [5]", "inférieure = 0", "en haut = 3" "0" Impossible parce que le deuxième élément serait ≥ 5. Autres
Autres Signes mélangés, par exemple, `[-1, 3,-2]'2'2' Démontre que les préfixes négatifs fonctionnent encore. Autres
`inférieur = -105`, `upper = 105`, large `différences`= 200 001= Test de stress pour l'arithmétique du débordement. Autres

---

2.10 Comment expliquer Dans une interview

1. **Énoncer l'observation* *
Si nous choisissons une valeur de départ `x`, chaque élément est `x` plus une somme de préfixe. (en milliers de dollars)

2. **Introduire le tableau de préfixes**
Afficher la dérivation de «préfixe[i]».

3. **Les limites**
Ecrivez les inégalités pour `inférieur` et `upper` en termes de `x` et `préfixe`.

4. **Simplifier à un intervalle**
Les valeurs de départ valides sont les entiers entre `inférieur - minPrefix` et `upper - maxPrefix`.

5. ** Compter les points**
Expliquez l'arithmétique pour compter les entiers inclus.

6. **Afficher l'algorithme à un passage* *
Soulignez l'optimalité *temps* et *espace*

7. **Cas de bord des peines**
Nous serrerons à zéro si l'intervalle est vide. (en milliers de dollars)

---

### 2.11 Prise- Des conseils pour s'éloigner

Conseil Pourquoi
- Oui.
Autres **Gardez une somme de préfixe en cours d'exécution. Autres
**Track min/max pendant la même boucle** Autres
**Utilisez toujours l'arithmétique 64-bit**Évitez les débordements subtils qui peuvent briser votre réponse. Autres
**Visualisez l'intervalle pour `x`**=Ceci rend la formule "magique" intuitive. Autres
Autres **Vérifiez le cas zéro** Une surveillance commune; rappelez-vous `max(0, ...)` à la fin. Autres

---

2.12 Conclusion

LeetCode #2145 est un test concis et élégant de deux compétences de base :

1. **Le raisonnement préfixe** – transformer une contrainte apparemment complexe en un problème de portée simple.
2. **Clean code** – un seul passage avec l'espace O(1) que vous pouvez expliquer en quelques minutes.

La maîtrise de ce modèle renforce votre confiance en *la programmation dynamique*, *la manipulation de l'arrachage* et *le comptage de l'échelle* — des compétences que les recruteurs recherchent dans les rôles de conception de systèmes et d'ensemble.

** Prêt à décrocher ce travail ? **
- **Ajouter cette solution à votre GitHub** et inclure un bref README expliquant l'algorithme.
- **Pratique expliquant la dérivation** à voix haute; cela vous aidera à articuler votre processus de pensée lors d'une entrevue en direct.
- **Paire-programme avec un ami** ou utiliser un juge en ligne pour répéter sous pression temporelle.

Bon codage – et que votre prochaine entrevue se déroule aussi bien que ce balayage préfixe-somme! C'est ce qu'il a dit.

---