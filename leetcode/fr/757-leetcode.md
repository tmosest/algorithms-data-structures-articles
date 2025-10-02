---
titre: LeetCode 757. Set Taille d'intersection au moins deux -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Problème redressé* *

Compte tenu d'une série d'intervalles entiers "intervalles[i] = [li , ri] "
trouver la taille minimale d'un ensemble `S` d'entiers de telle sorte que chaque intervalle
contient au moins **deux** numéros de `S`.

-----------------------------------------------------------------------------------

- Oui. Pourquoi une stratégie gourmande fonctionne

1. Si nous traitons un intervalle qui se termine le plus tôt possible, nous sommes libres de
choisir des points situés près de la fin de cet intervalle.
2. Les points choisis près d'un intervalle sont les plus susceptibles d'être
à l'intérieur de tous **plus tard** intervalles qui commencent après le courant.
3. Par conséquent, lorsque nous allons de gauche à droite (après triage à la fin),
nous ne pouvons garder que les deux **points les plus importants** qui ont déjà été
choisi; tout intervalle qui commence avant le deuxième point le plus important
est déjà couvert par au moins deux de ces points.

-----------------------------------------------------------------------------------

Algorithme

«» "
1. Si le tableau d'entrée est vide → retourner 0.

2. Trier les intervalles par
• extrémité croissante (intervalle[i][1])
• si les extrémités sont égales, début décroissant (ainsi l'intervalle plus long
vient d'abord). Cela garantit que nous traitons le plus court
les intervalles de fin possibles d'abord.

3. Initialiser un tableau `ans` (ou seulement deux variables) qui conservera
les points ajoutés à l'ensemble de réponses.
Ajouter les deux plus grands nombres du premier intervalle :
ans = [intervalle[0][1] - 1 , intervalle[0][1]]

4. Pour chaque intervalle restant [l, r] dans l'ordre trié
let last = ans[-1] // le plus grand point ajouté
let secondLast= ans[-2] // deuxième point le plus important ajouté

• Si l <= secondeLast: // les deux points sont dans l'intervalle
rien à faire

• Sinon si l <= last: // exactement un point à l'intérieur
ajouter r à ans

• Sinon: // aucun point à l'intérieur
ajouter r-1 et r aux ans
(Le cas spécial l == dernier est géré par la deuxième branche
parce que le premier point satisfait déjà l'intervalle.)

5. Retourne la longueur de `ans`.
«» "

-----------------------------------------------------------------------------------

## Esquisse d'exactitude

Nous prouvons par induction qu'après traitement le premier *k* trié
le nombre minimum possible de
des points.

*Base* – Après le premier intervalle, nous devons choisir deux points.
Le choix `{r-1, r}` est optimal: tout ensemble couvrant le premier intervalle
doit contenir deux entiers à l'intérieur; placer un à la fin et
l'autre immédiatement avant la fin maximise la chance
Les intervalles suivants comporteront également au moins un de ces points.

*Étape d'induction* – Supposons que la réclamation est valable pour les premiers intervalles *k-1*
et les deux points les plus importants sont "dernier" et "deuxième dernier".
Pour l'intervalle *k*-th `[l, r]` nous avons quatre cas:

1. ** 'l > dernier '** – Aucun point de `ans` ne se trouve dans l'intervalle, donc nous devons
insérer deux nouveaux points.
Choisir `{r-1, r}` est optimal pour la même raison que dans la base
C'est une affaire.

2. **'l == dernier'** – Exactement un point ('dernier') est dans l'intervalle,
un point de plus est nécessaire. Ajouter `r` donne deux points à l'intérieur
«[l, r]».

3. **'l > deuxième Dernier** – L'intervalle commence après la deuxième plus grande
avant ou au point le plus important.
Seul le dernier se trouve à l'intérieur, donc un seul point supplémentaire
«r» suffit.

4. **`l <= deuxièmeLast`** – Les deux `dernier` et `deuxièmeLast` se trouvent à l'intérieur de la
l'intervalle, donc il est déjà satisfait et aucun nouveau
nécessaire.

Dans chaque cas, nous ajoutons le nombre **minimum** de nouveaux points
s'assure que l'intervalle actuel comporte au moins deux éléments de «ans».
Ainsi, après avoir traité l'intervalle *k*-th, l'ensemble reste minimal.

Par induction, l'ensemble final `ans` est de taille minimale possible.

-----------------------------------------------------------------------------------

Complexité

Opération Temps Espace
- C'est quoi ?
(ou "O(log n)" pour le tri en place)
Un seul scan `O(n)`"" `O(1)` supplémentaire (ou `O(n)` si vous conservez la liste des points)

Total: **«O(n log n)» temps, «O(n)» espace auxiliaire** (la liste des
les points sélectionnés peuvent être omis, ne laissant que quelques variables entières).

-----------------------------------------------------------------------------------

Référence mise en œuvre (Java)

"Java
solution de classe {
intersection publique de l'inte TailleDeux[[][] intervalles] {
int n = intervalles de longueur;
// 1. trier par fin ascendante, puis commencer à descendre
Tableaux.sort(intervalles, a, b) -> {
si (a[1] == b[1]) retourner b[0] - a[0];
retour a[1] - b[1];
});

// 2. garder seulement les deux derniers points choisis
int last = intervalles[0][1]; //
int secondDernière = intervalles[0][1] - 1; // deuxième plus grand
nombre int = 2;

pour (int i = 1; i < n; i++) {
int l = intervalles [i][0];
int r = intervalles[i][1];

si (l <= deuxièmedernier) { // déjà couvert par 2 points
poursuivre;
} sinon si (l <= dernier) { // couvert par un point
count++; // ajouter une autre
secondDernier = dernier;
dernier = r;
} autres { // Aucun point à l'intérieur
nombre += 2; // ajouter deux nouveaux points
deuxièmeDernière = r - 1;
dernier = r;
}
}
le nombre de retours;
}
}
«» "

La même logique fonctionne dans n'importe quelle langue; les idées clés sont:

* trier en augmentant l'extrémité droite,
* commencer par les deux plus grands nombres du premier intervalle,
* pour chaque intervalle suivant, comparer sa limite gauche avec les deux plus grandes
nombres déjà choisis et ajouter 0, 1, ou 2 nouveaux points en conséquence.

Cela donne la taille minimale d'un ensemble qui a au moins deux éléments
en commun avec chaque intervalle.