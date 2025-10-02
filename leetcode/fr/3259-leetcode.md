---
titre: LeetCode 3259. Boost maximum d'énergie de deux boissons -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de démarrage rapide (Java / Python / C++)

"Java
/* Java 17 */
solution de classe publique {
public long maxEnergyBoost(int[] energyDrinkA, int[] energyDrinkB) {
long a = 0, b = 0; // meilleur total si nous terminons sur A / B
pour (int i = 0; i < énergieDrinkA.longueur; i++) {
long nouveauA = Math.max(a + énergieDrinkA[i], b);
long nouveauB = Math.max(b + énergieDrinkB[i], a);
a = nouveauA; b = nouveauB;
}
retour Math.max(a, b);
}
}
«» "

'`python
# Python 3.10
def max_energy_boost(energyDrinkA: list[int], energyDrinkB: list[int]) -> Int:
a, b = 0, 0 # meilleure somme se terminant par A / B
pour a_val, b_val dans zip(énergieDrinkA, énergieDrinkB):
new_a = max(a + a_val, b)
nouveau_b = max(b + b_val, a)
a, b = nouveau_a, nouveau_b
retour max(a, b)
«» "

'`cpp
// C++17
solution de classe {
public:
long maxEnergyBoost(vector<int>&energyDrinkA,
vecteur<int>&énergieDrinkB) {
long a = 0, b = 0;
pour (size_t i = 0; i < energyDrinkA.size(); ++i) {
long newA = max(a + énergieDrinkA[i], b);
long long nouveauB = max(b + énergieDrinkB[i], a);
a = nouveauA; b = nouveauB;
}
retour max(a, b);
}
};
«» "

Les trois solutions fonctionnent dans **O(n)** temps et utilisent **O(1)** espace supplémentaire (en plus des tableaux d'entrée).

---

2. Guide d'entrevue de style blog

Titre
**Le LeetCode #1662: Boost maximum d'énergie à partir de deux boissons – Tutoriel d'espace DP‐in‐O(1) (Java, Python, C++)* *

Pourquoi ça compte pour ton prochain entretien
- **LeetCode** problèmes comme *Maxim Energy Boost from Two Drinks* sont un point de départ dans les interviews de codage.
- Démontrer une solution propre et optimale montre que vous comprenez **Programmation dynamique**, **échanges temps/espace**, et pouvez écrire du code prêt à la production en **Java, Python ou C++**.
- Oui. L'article est optimisé pour les recruteurs à la recherche de questions d'interview de programmation dynamique, de solutions LeetCode, d'interview Python DP, etc.

---

Récapitulation des problèmes

> Vous avez deux tableaux `A` et `B` de longueur égale `n`.
> A chaque heure vous pouvez ** boire** une des deux boissons.
> Si vous changez le type de boisson (de A à B ou vice-versa), vous devez **skiper l'heure suivante** (c.-à-d. que vous buvez à l'heure *i*, puis prendre une pause à *i+1*, et peut boire l'autre type à *i+2*).
> Maximiser l'énergie totale gagnée.

---

2.1 Ce qui fait le problème

Description Autres
C'est pas vrai.
**Linear input**.Un seul passage sur les tableaux est nécessaire. Autres
**Claire avide Vous pouvez penser que c'est une décision d'entretien à chaque heure. Autres
** Facile à implémenter** La version d'espace O(1) utilise seulement deux totaux en cours d'exécution. Autres

---

2.2 Pièges communs

C'est pas vrai. Pourquoi il échoue
C'est pas vrai.
**O(n2) force brute**=L'essai de chaque sous-ensemble d'heures est exponentiel. Autres
**O(n) DP, mais utilisant un tableau 2-D complet**. Autres
**Ignorer la règle de "skip" d'une heure** de nombreuses solutions naïves traitent la décision comme "boire A vs boire B" seulement, manquant le repos obligatoire après un interrupteur. Autres
**L'utilisation d'un int 32 bits pour le résultat**. Utilisez `long`/`int64`. Autres

---

2.3 Le bon Algorithme – O(1)

Nous maintenons deux variables :

Sens de la variable
C'est pas vrai.
"a" : énergie maximale qui peut être recueillie ** si nous terminons l'heure actuelle en buvant A**. Autres
Même mais fini sur B. Autres

Lorsque nous regardons l'heure `i`, il ya deux possibilités pour chaque boisson:

Nouvelle valeur
C'est pas vrai.
Autres **Conserver la même boisson**= Ajouter la valeur de l'heure actuelle au total de la même boisson (`a + A[i]` ou `b + B[i]`). Autres
**Traitez les *autres* boissons (qui inclut déjà le repos obligatoire) et ajoutez 0 (parce que nous buvons ** à l'heure i** mais nous **l'heure de ski i‐1**). Dans la pratique, cela se traduit par `max(a + A[i], b)` pour la finition sur A et `max(b + B[i], a)` pour la finition sur B. Autres

La récurrence est:

«» "
newA = max(a + A[i], b)
newB = max(b + B[i], a)
«» "

Après mise à jour `a` et `b` pour chaque heure, la réponse est `max(a, b)`.

Cette formulation est une version classique de la description et est **optimale**:

- **Complexité temporelle :** `O(n)` – un passage sur les tableaux.
- **Complexité spatiale :** "O(1)" – seulement deux compteurs 64 bits.

---

2.4 Pourquoi la récurrence fonctionne

Considérez la stratégie optimale jusqu'à l'heure "i".

* Si nous buvons A à l'heure `i`:*
- Soit nous **obtenu** buvant A à l'heure précédente – total `a + A[i]`.
- Oui. Ou nous **switched** de B à l'heure `i-1` (qui nous oblige à nous reposer à `i-1`) – total `b` (le meilleur se terminant sur B jusqu'à l'heure `i-1`).

Le maximum de ces deux donne "newA".
La même logique s'applique au «nouveauB».
Parce que chaque état ne dépend que des deux états précédents (`a` et `b`), nous pouvons jeter les valeurs plus anciennes – c'est la propriété de l'espace constant.

---

2.5 Edge- Liste de contrôle des cas

Qu'est-ce qu'il faut faire attention Comment notre code le gère
Il y a un problème.
Un seul verre peut être pris. La boucle tourne une fois; `newA = max(0 + A[0], 0) = A[0]». Autres
"A[i] = B[i]"" Cas symétrique – toute stratégie est bonne. L'algorithme maintient naturellement les deux totaux égaux. Autres
Nombres importants (`106` × `105`) Toutes les solutions utilisent 64 bits (`long` en Java, `int` en Python 3, `long` en C++). Autres
Autres Tous les zéros Résultat zéro. L'algorithme produit 0.

---

2.6 Variations que vous pourriez entendre dans les entrevues

1. **Plusieurs types de boissons** – étendre le DP aux états « k ».
2. **Coût pour la commutation** – ajouter une pénalité au lieu d'un repos obligatoire.
3. **Calendrier circulaire** – première et dernière heure sont adjacentes.

Dans tous les cas, l'idée de base est la même : **=Conserver la même boisson== vs===Switch drink===**, stocké dans une petite table roulante.

---

3. SEO-friendly Blog Article

Titre
*Comment cracker le code Leet 1662 – Augmentation maximale d'énergie de deux boissons (Java, Python, C++)* *

Description de la méta
> Découvrez la solution O(n) DP optimale pour LeetCode 1662 -Profit énergétique maximal de deux boissons. Voir les implémentations Java, Python et C++, l'analyse du temps et de l'espace, les pièges d'entrevue, et comment maîtriser ce problème peut augmenter vos performances d'entrevue de codage.

Table des matières

1. [Présentation du problème](#problème-aperçu)
2. [Intuitive Insight] (#intuitive-insight)
3. [Formulation de programmation dynamique](#dp-formulation)
4. [Mise en œuvre de l'Espace O(1) sur le Rolling-Array](#rolling-array)
5. [Complexité et compromis](#complexité)
6. [erreurs communes et comment les éviter](#erreurs)
7. [Variants de suivi](#suivi)
8. [Interview-Ready Tips](#interview-tips)
9. [Enveloppage](#Enveloppage)

---

3.1 Aperçu du problème
> **Maximum Energy Boost from Two Drinks** (LeetCode #1662) vous défie de maximiser la somme des valeurs de deux tableaux parallèles lorsque vous pouvez boire une par heure mais que vous devez vous reposer une heure après un changement de type. Pensez à deux boissons à bond d'énergie A et B, chacune avec une valeur horaire, et une règle : *la commutation coûte une heure de repos*.

**Pourquoi ça compte**
- Oui. Il teste votre compréhension de la programmation **dynamique** et de la gestion de l'état**.
- Oui. Le même modèle apparaît dans d'autres questions d'entrevue comme -House Robber ou -Somme de subséquence maximale avec Skips.
- Une solution d'espace O(1) propre est une réponse digne de brag sur votre CV.

---

3.2 Aperçu intuitif
Imaginez-vous debout à l'heure 'i'.
Vous avez deux options :

Qu'est-ce qui se passe ? Autres
- C'est quoi ?
Autres **Conservez la même boisson**= Buvez A/B et passez à `i+1`. Autres
**Switch drinks**= Buvez A/B, puis **rest** à `i+1` (pas de boisson), et peut boire l`autre type à `i+2`. Le reste signifie que vous ne pouvez pas ajouter d'énergie pour `i+1`; la prochaine contribution est `0`. Mais vous avez déjà pris une pause, donc le total des autres boissons est déjà valide. Autres

La prise: quand vous changez, vous *ne pouvez pas * utiliser le total qui ** juste bu l'autre type dans l'heure précédente** parce que vous aviez encore se reposer.
Par conséquent, après un interrupteur, le total de "fraîcheur" vient de la **autre boisson du mieux jusqu'à l'heure `i-1`**.

---

3.3 Formulation dynamique de la programmation
Laissez

«» "
dpA[i] – énergie maximale jusqu'à l'heure i, finissant par la boisson A
dpB[i] – même mais finition avec boisson B
«» "

Répétition :

«» "
dpA[i] = max(dpA[i-1] + A[i], dpB[i-1]) // garder ou interrupteur
dpB[i] = max(dpB[i-1] + B[i], dpA[i-1]) // garder ou interrupteur
«» "

Parce que chaque `dp*` ne regarde que les deux valeurs précédentes, nous pouvons **roll** le DP:

«» "
newA = max(a + A[i], b)
newB = max(b + B[i], a)
«» "

où `a` et `b` sont les `dpA` et `dpB` précédents.
Après avoir traité toutes les heures, répondez = `max(a, b)`.

---

3.4 Mise en œuvre de la mise en œuvre de l'appareil roulant (O(1) Espace)
*Afficher les extraits de code pour Java, Python et C++. *

"Java
long a = 0, b = 0;
pour (int i = 0; i < n; i++) {
long nouveauA = Math.max(a + A[i], b);
long nouveauB = Math.max(b + B[i], a);
a = nouveauA; b = nouveauB;
}
retour Math.max(a, b);
«» "

Le même motif apparaît dans Python (`int` est arbitraire-précision) et C++ (`long').

**Pourquoi O(1) espace? **
- `dpA` et `dpB` ne dépendent que des *derniers* totaux.
- Oui. Nous rejetons les anciens états, sauvons la mémoire et rendons l'algorithme élégant.

---

3.5 Complexité et compromis
Valeur métrique Pourquoi est-ce acceptable ? Autres
- C'est pas vrai.
Un scan linéaire, idéal pour les intervieweurs. Autres
**L'espace**=1=1=2 Seulement deux entiers 64 bits – parfaits pour les grandes entrées. Autres
**Alternatif**= Tableau 2-D complet: temps `O(n)`, `O(n)` espace: Fonctionne mais inutile; utilisez la version de roulement pour impressionner. Autres

---

3.6 Erreurs courantes et comment éviter Eux

1. **Omettre l'heure de repos** – conduit à des états incorrects.
*Fixe:* Considérez toujours le chemin de commutation (`max(a + A[i], b)` au lieu de `max(a + A[i], b + B[i])`).
2. **En utilisant un entier de 32 bits pour la somme** – risque de débordement.
*Fix:* Utilisez `long`/`long long`.
3. **Fournir toutes les combinaisons** – Temps exponentiel.
*Fix:* Reconnaître le problème comme un DP 1-D avec deux états.

---

3.7 Variantes de suivi

Variante Comment la solution change
-- -- -- -- -- -- -- -- -- -- -- -- -- --
**Plus de deux boissons**= DP avec des états `k`; utilisez un petit tableau de taille `k`.= `vecteur<long> dp(k, 0);` rouler. Autres
Autres **Coût pour le changement de poste**= Ajouter la pénalité `p` à `newA`/`newB`.= `newA = max(a + A[i], b - p)` etc. Autres
**Circulaire **La première heure suit la dernière heure. Réalisez le DP deux fois : une fois que nous supposons que nous commençons avec A, une fois avec B; choisissez le maximum tout en manipulant l'enroulement. Autres

---

3.8 Entretien— Conseils prêts

Conseil Explication
C'est pas vrai.
**Diagramme d'état d'abord**= Avant de coder, dessinez deux nœuds (A, B) et annotez les transitions. Autres
**Expliquez la règle de l'heure de ski** Autres
**Discuse le temps/l'espace**.Les recruteurs aiment vous voir discuter des deux. Autres
**Afficher l'astuce d'O(1)** Autres
Autres **Test sur les boîtiers de bord**. Autres
**Utilisez 64-bit**.Évitez tout débordement accidentel; mentionnez-le dans vos notes de solution. Autres

---

3.9 Enveloppe

Mastering **Maximum Energy Boost from Two Drinks** démontre que vous pouvez :

- Traduire une contrainte du monde réel (rest after a switch) en une récurrence PDD propre.
- Optimisez le temps et l'espace.
- Implémentez la même logique dans votre langue de choix.

Utilisez les extraits ci-dessus comme référence ou déposez-les dans votre dépôt GitHub sous `leetcode/1662`. Lorsque le prochain recruteur pose des questions sur LeetCode DP, vous aurez une réponse polie prête à briller.

Bon codage ! C'est ce qu'il a dit.

---

Ressources

- Problème de LeetCode 1662 – [lien](https://leetcode.com/problèmes/maximum-energy-boost-from-two-drinks/)
- Robber de maison – DP similaire avec règle de saut.
- * Programmation dynamique – playlist Hard & Medium* sur YouTube pour les apprenants visuels.

---

**Bonne entrevue!**

---

Besoin d'aide ?
Atteindre via Linked Dans ou sur Twitter, ou réservez une séance de préparation individuelle avec un mentor principal.

---

* Fin de l'article. *

---

4. Pensées finales

- Oui. La récurrence PD linéaire est au cœur de la solution; la version de roulement d'espace O(1) est à la fois élégante et conviviale.
- Oui. Les trois extraits de code vous fournissent un code prêt à copier et à produire dans les langues que les recruteurs aiment.
- Utilisez ces connaissances pour mettre en valeur **la pensée basée sur l'état**, **l'optimisation de l'espace** et **la modélisation du domaine** sur votre prochaine entrevue de codage ou dans votre curriculum vitae.

---

Bon codage ! C'est ce qu'il a dit