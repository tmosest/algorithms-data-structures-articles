---
titre: LeetCode 2718. Somme de la matrice après les requêtes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 2718 – Somme de la matrice après les requêtes
**TL;DR** – L'astuce est de marcher à travers les requêtes *backwards*, garder un drapeau "seen" pour chaque ligne et colonne, et ajouter la contribution de chaque *unique* ligne/colonne une seule fois.
Complexité: **O(queries + n)** temps, **O(n)** espace.
Ci-dessous vous trouverez des solutions prêtes à la copie dans **Java, Python et C++** (tous annotés), suivi d'un court billet de blog SEO-friendly qui explique l'idée, pourquoi elle fonctionne, et comment vous pouvez l'utiliser pour impressionner les intervieweurs.

---

- Oui. 1. Le Code

#### 1.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
***
* Renvoie la somme de toutes les cellules dans une matrice n x n après application
* une liste des requêtes d'écrasement ligne/colonne.
*
* Taille de la matrice @param n (n x n)
* Liste des requêtes @param, chaque requête = [type, index, val]
* @retour total somme aussi longtemps
*/
publique longue matriceSumQueries(int n, int[][] requêtes) {
booléen[] rowSeen = nouveau booléen[n];
booléen[] colSeen = nouveau booléen[n];
la ligne intCount = 0, colCount = 0;
somme longue = 0;

// Procéder de la dernière requête à la première – les dernières victoires
pour (int i = requêtes.longueur - 1; i >= 0; i--) {
type int = requêtes[i][0];
int idx = requêtes[i][1];
int val = requêtes[i][2];

si (type) 0) { // écrasement de la ligne
si (!rowSeen[idx]) {
somme += (long) (n - colCount) * valeur; // seulement colonnes fraîches
rowSeen[idx] = true;
ligne Nombre++;
}
} autre { // colonne écrasement
si (!colSeen[idx]) {
somme += (long) (n - rangCount) * valeur; // seulement lignes fraîches
colSeen[idx] = vrai;
ccolCount++;
}
}
}
la somme de retour;
}
}
«» "

#### 1.2 Python

'`python
def matrixSumQueries(n: int, requêtes: list[list[int]]) -> Int:
"""
Retourne la somme d'une matrice n x n après avoir traité toutes les requêtes.
requêtes: [[type, index, val], ...]
"""
ligne_seen = [False] * n
col_seen = [Faux] * n
ligne_cnt = col_cnt = 0
Total = 0

pour typ, idx, val en marche arrière(requêtes):
si typ == 0 et non row_seen[idx]:
Total += (n - col_cnt) * valeur
row_seen[idx] = Vrai
ligne_cnt += 1
elif typ == 1 et non col_seen[idx]:
total += (n - ligne_cnt) * valeur
col_seen[idx] = Vrai
_cnt += 1

retour total
«» "

*## 1.3 C++

'`cpp
solution de classe {
public:
longue longue matriceSumQueries(int n, vector<vector<int>>& requêtes) {
vector<bool> rowSeen(n, false), colSeen(n, false);
dans la ligneCnt = 0, colCnt = 0;
somme longue = 0;

// Traverse de la fin – dernière opération
pour (int i = (int)queries.size() - 1; i >= 0; --i) {
type int = requêtes[i][0];
int idx = requêtes[i][1];
int val = requêtes[i][2];

si (type == 0 & & & !rowSeen[idx]) {
somme += 1LL * (n - colCnt) * valeur;
rowSeen[idx] = true;
+ ligne Cnt;
} sinon si (type == 1 & & & !colSeen[idx]) {
somme += 1LL * (n - ligneCnt) * valeur;
colSeen[idx] = vrai;
++colCnt;
}
}
la somme de retour;
}
};
«» "

> **Les trois implémentations fonctionnent en temps O(queries + n) et en mémoire O(n)** – assez rapidement pour les limites `n ≤ 104` et `queries ≤ 5·104`.

---

- Oui. 2. Article du blog – Le bon, le mauvais, et le mauvais de la somme de la matrice après les requêtes

2.1 Introduction

LeetCode 2718 – *Sum of Matrix After Queries* – est un problème d'entrevue classique qui teste votre capacité à penser à "overwrites" dans un espace 2-D.
La tâche est simple à définir : vous commencez par une matrice all-zero `n × n`, puis une série d'affectations **row** ou **column** sont appliquées. Après toutes les requêtes, calculez la somme totale de la matrice.

Pourquoi est-ce important ?
* Dans les systèmes du monde réel, vous avez souvent *écraser* des lignes entières ou des colonnes (penser des mises à jour de tableurs, des shaders GPU ou des opérations de masse de bases de données).
* Les intervieweurs aiment les problèmes qui vous obligent à éviter une simulation évidente `O(n2)`, car ils révèlent votre conscience de l'optimisation algorithmique.

Au-dessous de l'I.I. va marcher à travers le **bon** (ce qui est juste), le **bad** (écueils communs), et le **ugly** (les solutions mesquines, mais possibles).

---

#### 2.2 Le bon – Un O propre (requêtes + n) Solution

**Insight clé:**
La requête *dernier* qui touche une ligne ou une colonne est la seule qui compte pour la matrice finale.

Par conséquent, nous pouvons traiter les requêtes **backwards**.
Tandis que l'itération de la fin:

1. Gardez deux tableaux de booléens – `rowSeen[n]` et `colSeen[n]`.
2. Tenir des comptes du nombre de lignes/colonnes distinctes déjà fixées.
3. Lorsque vous rencontrez une requête de ligne `[0, r, val]` qui n'a pas été vu:
* Chaque colonne qui ** n'a pas encore été écrasée contribue `val` à la somme.
* Cette contribution est "val* (n - colCnt)".
4. Faites la logique symétrique pour une requête en colonne.

Parce que chaque ligne ou colonne est comptée **once** (la première fois que vous la voyez dans l'ordre inverse), l'algorithme est linéaire.

**Pourquoi c'est bien:* *
* Temps linéaire, espace linéaire – bien dans les limites de LeetCode.
* Intuitif une fois que vous comprendrez la dernière victoire.
* Fonctionne pour les contraintes maximales (`n = 104`, `demandes = 5·104`).

---

2.3 Les mauvaises – approches naïves qui meurent

L'approche du temps L'espace Pourquoi il échoue
- C'est quoi ?
**Simulation complète de la matrice**= O(n2 · q)= O(n2)= `n2` peut être 108 cellules – impossible. Autres
Autres **Track per-cell dernier écrivain**= O(n2)= O(n2)= Même numéro – trop de cellules. Autres
**Scannage vers l'avant avec set**= O(q · n)== O(n)= Toujours quadratique dans le pire des cas parce que vous recalculez chaque ligne/colonne plusieurs fois. Autres
**Ignorer les requêtes dupliquées**=O(q · n)=O(n)=Toujours trop lent; vous faites 5×104 × 104=5×108 ops – limite ou plus. Autres

Les intervieweurs donnent souvent la solution de la matrice complète comme un exemple de ce que *pas* faire.
Même une implémentation Python qui écrit naïvement à la cellule matricielle par cellule TLE sur les plus grands tests.

---

2.4 Les variations messy qui fonctionnent mais sont difficiles à expliquer

1. **Utilisation de `unordered_map` pour enregistrer la dernière fois d'écriture** –
*Store pour chaque ligne/colonne le *time stamp* de sa dernière affectation et ensuite reconstruire la matrice. *
* Il faut toujours `O(n2)` pour la somme finale à moins que vous ne fassiez un astucieux tour de maths.

2. **Compression de bits + BFS** –
*Utilisez un bitset pour marquer les lignes/colonnes visibles et BFS pour propager les valeurs. *
* Fonctionne, mais le code devient un labyrinthe de manipulations de bits difficiles à déboguer.

Ces solutions sont techniquement correctes mais apportent **verbosity** et **bogues cachées** (par exemple, erreurs off-by-one dans le multiplicateur `(n - colCnt)`).

> **Ligne de bottom:** Si vous pouvez terminer la solution d'itération inversée en moins de 2 minutes, vous avez surperformé les solutions d'itération inversées par une large marge.

---

2.4 Pourquoi le Trick inverse fonctionne (Proof par induction)

Laissez-nous prouver que le scan inverse fonctionne :

- **Cas de base:** La dernière requête de la liste touche une ligne `r`. Dans la simulation avant, après cette affectation toutes les cellules `(r, c)` pour tous `c` deviennent `val`. Comme aucune requête ultérieure n'écrase `r`, la valeur finale de la ligne `r` est exactement `val`.

- **Étape inductive :** Supposons que pour chaque ligne/colonne traitée jusqu'à présent (à partir de la fin), la somme fournie par *unique* lignes/colonnes est correcte.
Lorsque l'on touche ensuite une nouvelle ligne `r`, chaque colonne `c` *pas encore traitée* (c.-à-d. non vue en sens inverse) est toujours à sa valeur originale de "précédent".
Ainsi, ajouter "val* (n - colCnt)" capture exactement les cellules fraîches que la ligne `r` possédera dans la matrice finale.

Par induction, chaque ligne/colonne unique contribue correctement, et les duplicatas sont ignorés.

---

2.5 Variations que vous pourriez entendre dans une entrevue

Variante Stratégie
C'est pas vrai.
**Queries qui ajoutent à une ligne/colonne au lieu d'écraser**. Autres
**Matrix parse (n est énorme, mais peu de lignes/colonnes actives)** Autres
**Taille de la matrice dynamique**=Utilisez *hash map* pour les drapeaux vus; toujours O(q) time, O(#lignes/cols distinctes). Autres

Si vous pouvez expliquer comment l'idée de l'itération inverse s'adapte à l'un de ces éléments, vous serez un candidat étoile.

---

2.6 Comment utiliser cette solution dans une entrevue

1. **Expliquez la propriété "La dernière requête gagne"** – elle démontre que vous n'écrivez pas seulement du code, vous raisonnez sur le problème.
2. **Afficher la complexité O(n + q)** – demander à l'intervieweur si cela est acceptable pour les contraintes.
3. **Parcourez l'entrée de l'échantillon** – étape par étape (p. ex. `[0,15]`, `[1,32]`, ...) – pour montrer comment fonctionne le multiplicateur.
4. **Cas de bord de Mention** – p.ex. requêtes dupliquées, toutes les lignes puis toutes les colonnes, matrice monocellulaire.
5. **Bonus:** Offrez un extrait de Python ou Java sur place.

> Souvent, les intervieweurs cherchent *explainability* plus que *speed*, alors gardez l'explication concise mais complète.

---

2.7 Conclusion – Une solution pour votre prochain emploi

LeetCode 2718 est un grand problème d'algorithme-plus-histoire.
- **Good** – La solution d'itération inverse est un algorithme O(queries + n) de manuel.
- **Bad** – Ne tombez pas dans le piège de simulation de matrice naïf.
- **Ugly** – Il y a beaucoup de moyens désordonnés pour pirater le problème, mais ils sont rarement nécessaires.

Lorsque vous atterrissez sur ce problème, visez la solution propre, arriérée, mentionnez ses garanties linéaires, et vous obtiendrez non seulement la réponse correcte, mais impressionnerez également le gestionnaire d'embauche avec votre état d'esprit d'efficacité.

> ** Mots clés du référencement* *
> Sum of Matrix After Queries=LeetCode 2718=2 Solution Java=2 Solution Python=2 Solution C++=2

Codage heureux, et que vos futures interviews soient *remplies de solutions propres et efficaces!*