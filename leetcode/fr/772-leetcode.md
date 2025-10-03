---
titre: LeetCode 772. Calculatrice de base III –
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Aperçu de la solution**

Nous évaluons l'expression en un seul balayage linéaire.
Pendant le balayage, nous gardons

* `num` – le numéro en cours de lecture (peut contenir plusieurs chiffres)
* `pre` – la valeur *dernier* qui a déjà considéré la multiplication/la division
(il ne sera ajouté au résultat qu'après avoir vu un plus/moins ou la fin).
* `res` – la somme de tous les termes déjà finis.
* `sign` – l'opérateur qui sera appliqué au prochain `num`.

Lorsque nous rencontrons un `(` nous évaluons récursivement la sous-expression qui suit
jusqu'à ce qu'il corresponde `)'.
Lorsque nous voyons un opérateur (ou `)` ou la fin de la chaîne) nous nous engageons dans le courant
`num` à `res` / `pre` selon l'opérateur précédent.
Si le caractère qui a causé le commit est `)` nous retournons immédiatement
`res + pre` – cela termine le niveau actuel de récursion.

La profondeur récursive est limitée par le nombre de parenthèses nichées, de sorte que la
La taille de la pile auxiliaire est `O(#brackets)`.

-----------------------------------------------------------------------------------

Preuve d'exactitude

Nous prouvons que l'algorithme renvoie la valeur de l'expression `s`.

---

Lemma 1
A tout moment lors de l'évaluation d'un niveau (entre une paire de
entre parenthèses ou la chaîne entière) `res` égale la somme de toutes les finitions
la valeur de la durée en cours*
sera ajouté à «res» après le traitement du prochain opérateur).

**Prof.**
Initialement `res = 0` et `pre = 0`; le lemma tient.

Chaque fois que nous rencontrons un opérateur `op` (ou la fermeture `)` ou fin de la chaîne)
l'algorithme exécute:

«» "
interrupteur (signal) {
cas «+»: res += pre; pre = num; break;
cas «-»: res += pre; pre = -num; rupture;
cas '*': pré *= nombre; rupture;
cas '/': pré/= nombre; rupture;
}
«» "

`sign` est l'opérateur qui était en attente avant `num` a été lu.
- Pour `+` ou `-` le terme `pre` en attente est terminé et ajouté à `res`,
et `pre` est fixé au nouveau terme (`+num` ou `-num`).
- Pour `*` ou `/` le terme en suspens est * prolongé* par multiplication/division,
si `pre` est mis à jour mais pas encore ajouté à `res`.

Ainsi, après le commutateur, `res` contient tous les termes finis, et `pre` contient
le dernier terme inachevé (éventuellement déjà multiplié/divisé).
Si l'opérateur est `)`, la fonction retourne `res + pre`, qui par le lemma
égale la valeur de la sous-expression.
Par conséquent, l'invariant tient inductif pour chaque étape. *



Lemma 2
Lorsqu'une sous-expression entre parenthèses est évaluée de façon récursive, son retour
valeur égale la valeur mathématique de cette sous-expression.

**Prof.**
L'appel récursif est entré seulement quand un `(` est vu.
À l'intérieur de l'appel, le même invariant (Lemma 1) tient, parce que le
le même code est exécuté.
Lorsque la correspondance `)` est traitée, la fonction retourne `res + pre`,
qui par Lemma 1 égale la valeur de cette sous-expression. *



C'est vrai. Théorème
`calculer(s)` renvoie la valeur de l'expression arithmétique représentée par
« s ».

**Prof.**
L'appel de haut niveau traite toute la chaîne.
Chaque numéro est lu complètement (les nombres à plusieurs chiffres sont traités par la
`num = num*10 + chiffre` pas).
Lorsque la chaîne se termine, le `num` final est commis (parce que `idx == n`), donc tous
les termes sont ajoutés à «res».
Par Lemma 1 la valeur retournée est `res + pre`, qui est la valeur de la
expression complète.
Lemma 2 veille à ce que chaque sous-expression entre parenthèses soit évaluée
correctement.
Ainsi, la fonction retourne le résultat correct. *



-----------------------------------------------------------------------------------

Analyse de complexité

Laissez `n` être la longueur de la chaîne d'entrée.

* ** Temps** – Chaque caractère est examiné exactement une fois (`idx` seulement avance).
Par conséquent, le temps d'exécution est `-n`.

* **Espace** – La profondeur auxiliaire de la cheminée de récursion est égale à la nidation maximale
entre parenthèses, au plus `n/2`.
Ainsi l'espace auxiliaire est `O(#brackets)` ≤ "O(n)".

-----------------------------------------------------------------------------------

#### Mise en oeuvre des références (Java 17)

"Java
solution de classe {
// Index partagé – la position dans la chaîne qui est actuellement traitée
Int idx privé;

calcul de l'int public(en milliers) {
idx = 0; // début de chaque appel
eval(s) de retour;
}

***
* Évalue l'expression représentée par la chaîne `s`
* commençant à la valeur actuelle de `idx`. Il s'arrête quand la chaîne se termine
* ou lorsqu'un ')' correspondant est rencontré. La valeur de retour est la valeur
* de la partie traitée.
*/
valeur privée de l'inte
int res = 0; // somme cumulée des termes finis
int pre = 0; // durée en cours (après *, /)
int num = 0; // nombre courant en lecture
signe char = '+'; // opérateur qui sera appliqué au prochain numéro

int n = s.longueur();
pendant la période (idx < n) {
c = s.charAt(idx++);

si c == '(') { // début d'une sous-expression
num = eval(s); // l'évaluer récursivement
} sinon si (c >= '0' && c <= '9') { // nombre (éventuellement >1 chiffre)
num = num * 10 + (c - '0');
}

/* Commettre le nombre courant lorsqu'un opérateur, ')', ou la fin est vue */
if (c == '+'''''c == '-'''''c == '''''''c == '''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''' {
interrupteur (signal) {
cas «+»: res += pre; pre = num; break;
cas «-»: res += pre; pre = -num; rupture;
cas '*': pré *= nombre; rupture;
cas '/': pré/= nombre; rupture;
}

si c == ')') { // fini une sous-exposition entre parenthèses
retourner res + pre; // retourner sa valeur à l'appelant
}

num = 0; // réinitialiser pour le terme suivant
signe = c; // se souvenir de l'opérateur en attente
}
}
retour res + pre; // valeur finale de l'ensemble du niveau
}
}
«» "

Le programme suit exactement l'algorithme prouvé correct ci-dessus et satisfait
les contraintes de LeetCode 227.