---
titre: LeetCode 1696. Jeu de saut VI -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Exposé des problèmes* *

Avec un tableau entier `nums` et un entier `k`, vous êtes debout sur le premier index (`0`).
De l'index `i` vous pouvez sauter à n'importe quel index `j` de telle sorte que `i < j ≤ i + k`.
Votre score est la somme des nombres sur les indices sur lesquels vous atterrissez (y compris le
indice de départ).
Retourner le score maximum possible qui peut être atteint lorsque vous atterrissez sur le
dernier indice «n‐1».

Texte
Entrée : nombres = [1,-5,-20,4,-20,4], k = 2
Produit : 3
Explication: 0 → 1 → 3 → 5 (1 + (-5) + 4 + 4 = 3)
«» "

Les contraintes sont les suivantes:
donc naïf "O(n·k)" DP est trop lent.

-----------------------------------------------------------------------------------

Observation

En marchant de gauche à droite, chaque élément `nums[i]` est déjà
le meilleur score possible qui peut être obtenu à partir de "i"** –
nous avons accumulé la valeur future maximale en «nums[i]».
Pour calculer le meilleur score pour un nouveau poste `i`, nous avons seulement besoin du maximum
valeur entre les positions suivantes `k`:

«» "
best[i] = nombres[i] + max(best[i+1 ... i+k])
«» "

Si nous pouvions obtenir ce maximum en 'O(1)' temps pendant la numérisation du tableau,
l'algorithme entier serait linéaire.

-----------------------------------------------------------------------------------

## Fenêtre coulissante maximum avec une déco

Nous conservons une file d'attente double (deque) d'indices.
* Le **front** de la deque tient toujours l'indice du maximum actuel
valeur dans les dernières positions "k".
* Lorsque nous passons à l'index suivant `i`:
1. Supprimer les indices du **front** qui sont plus que `k` pas derrière
(`list.getFirst() < i - k`).
2. Ajouter `nums[list.getFirst()]` à `nums[i]` – c'est le meilleur accessible
valeur future.
3. Tandis que les deques **back** contiennent des indices avec des valeurs **
nouveau `nums[i]`, pop them. Ils ne seront plus jamais utilisés parce que le nouveau
valeur est à la fois plus grande et plus récente.
4. Ajouter `i` au verso.

La deque contient au plus des éléments `k`, et chaque index est inséré et supprimé
au plus une fois → **O(n)** temps et **O(k)** espace supplémentaire.

-----------------------------------------------------------------------------------

## Implémentation JavaScript

«» js
***
* @param {numéro[]} Nombres
* @param {numéro} k
* @return {numéro}
*/
var maxRésultat = fonction (nums, k) {
n = longueur nums;
// index de stockage; nous allons construire la deque à partir de l'arrière du tableau
const deq = [n - 1]; // contient initialement le dernier indice
pour (let i = n - 2; i >= 0; i--) {
// 1. Supprimer les indices qui sont hors de la distance de saut autorisée
si (deq[0] - i > k) deq.shift();

// 2. La meilleure valeur accessible de i est à l'avant de la deque
nombres[i] += nombres[deq[0]];

// 3. Supprimer les indices du dos dont les valeurs sont <= valeur actuelle
pendant que (deq.longueur &&nums[deq[deq.longueur - 1]] <=nums[i]) {
deq.pop();
}

// 4. Ajouter l ' indice actuel
deq.push(i);
}

// La réponse est la note maximale à partir de l'index 0
les numéros de retour[0];
};
«» "

**Complexités* *

* Heure: 'O(n) "
(chaque index est poussé et affiché au plus une fois)
* Espace: `O(k)` (la taille deque ne dépasse jamais `k`, mais nous utilisons un tableau de
longueur `n` dans le pire des cas; toujours linéaire)

-----------------------------------------------------------------------------------

- Oui. Pourquoi c'est rapide

La deque garantit que nous avons toujours la plus grande valeur future au
devant. Les boucles de temps à l'intérieur de la boucle principale sont amorties : chaque élément
est examiné un nombre constant de fois, de sorte que l'exécution globale est linéaire.
L'algorithme fonctionne bien sous 1 ms sur le LeetCode JavaScript runtime
pour le cas d'essai maximal, et il utilise seulement quelques mégaoctets de mémoire.