---
titre: LeetCode 2835. Minimum des opérations pour former un subséquence avec une somme cible -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2835 – Opérations minimales pour former la séquence subséquente avec la somme cible
LeetCode**

> **Job-Hunting Edge:**
> *C'est le genre de défi LeetCode que les intervieweurs aiment : il mélange raisonnement avide, astuces bit-wise, et une analyse de complexité claire. Maîtriser cela fera de vous un candidat fort pour les rôles qui exigent la pensée algorithmique et la fluidité de la structure des données. *

---

Récapitulation du problème

On vous donne un tableau "nums" qui ne contient que deux pouvoirs (par exemple "1, 2, 4, 8, ...").
Vous pouvez effectuer une opération n'importe quel nombre de fois:

1. Choisissez un élément `x` dans le tableau tel que `x > 1`.
2. Supprimer `x`.
3. Ajouter deux copies de `x / 2` à la fin du tableau.

La somme totale du tableau ne change jamais.
Après toute séquence d'opérations, vous avez besoin d'un **subséquence** (pas nécessairement contigu) qui correspond exactement à une "cible".
Retourner le nombre minimum d'opérations nécessaires, ou `-1` s'il est impossible.



Valeur des principales contraintes
- Oui.
1 ≤ longueur nominale ≤ 1000
1 ≤ nums[i] Toutes les valeurs sont des puissances de deux.
Objectif < 231
Délai



---

- Oui. L'idée – Grande à petite graisse

1. **Cocher la somme totale** – Si la somme de tous les nombres est plus petite que `cible`, il est impossible → `-1`.
Si la somme équivaut à `cible`, nous sommes déjà fait → `0`.

2. **Cueillir le plus gros élément** –
* Pourquoi plus grand?
* Si le nombre le plus élevé peut être *ignoré* (car les nombres restants représentent encore au moins `cible`), cela ne nous aidera jamais à atteindre la cible. Il réduit la somme et maintient le reste intact.
* S'il est **obligatoire**, nous l'utilisons (si elle ne dépasse pas la "cible" restante) ou la fractionnons (si elle dépasse). Le fractionnement maintient la somme totale inchangée tout en produisant des blocs de construction plus petits.

3. **Splitting** –
Lorsque le nombre actuel `x` est plus grand que le nombre restant `cible` mais `x > 1`, le diviser en deux `x/2`. Cela consomme une opération, mais la somme reste la même.

4. **Répéter** jusqu'à ce que la "cible" devienne zéro.
Parce que chaque scission réduit l'élément *maximum*, nous allons finalement atteindre un état où l'élément le plus important est `1` et nous pouvons terminer le processus.

5. **Proof d'optimalité** –
Le choix avide de la skipe si possible est optimal parce que:
* Sauter un grand élément ne peut jamais augmenter le nombre d'opérations nécessaires; il supprime seulement un candidat qui n'est pas nécessaire.
* Si un grand élément est nécessaire, soit nous l'utilisons (en forme exacte) soit nous le divisons; aucune autre opération ne peut aider plus efficacement.

---

## Mise en œuvre du code

Voici des solutions propres et autonomes dans **Java**, **Python** et **C++**.
Tous utilisent un max-heap (`PriorityQueue`/`heapq`/`priority_queue`) pour récupérer l'élément le plus important actuel dans `O(log n)`.

- Oui. 1. Java

"Java
Importation de java.util.*;

solution de classe {
Activités publiques (liste <entier> nombres, cible int) {
// Montant total
somme longue = 0;
pour (int v : nombres) somme += v;

si (somme < cible) retour -1;
si (somme == cible) retourne 0;

// Max-heap
Priorité Queue<integer> pq = nouvelle prioritéQueue<>(Collections.reverseOrder());
pq.addAll(nums);

Int ops = 0;
pendant la période (cible > 0) {
int x = pq.poll(); // élément le plus important

si (somme - x >= cible) { // nous pouvons le sauter
somme -= x;
poursuivre;
}

si (x <= cible) { // nous avons besoin de cette valeur
cible -= x;
somme -= x;
} autres { // x > cible et x > 1 -> fractionné
si (x == 1) { // ne peut pas diviser 1, mais cela ne devrait jamais arriver
// Si nous sommes ici, l'algorithme est faux.
retour -1;
}
(x / 2);
(x / 2);
ops++;
}
}
les opérations de retour;
}
}
«» "

*Utiliser* `Solution s = nouvelle solution(); s.minOpérations(nombres, cible);*


- Oui. 2. Python

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
def minOpérations(auto, nombres: Liste[int], cible: int) -> Int:
total = somme(s)
si total < cible:
retour -1
si total == cible:
retour 0

# max-heap via des nombres négatifs
pq = [-x pour x en nombres]
heapq.heapify(pq)

ops = 0
pendant la cible:
x = -heapq.heappop(pq) # élément le plus important
si total - x >= cible : # peut ignorer
Total -= x
elif x <= cible: # nous en avons besoin
Total -= x
cible -= x
Sinon : # x > cible, la diviser
(pq, -x // 2)
(pq, -x // 2)
Opérations += 1

retour ops
«» "

- Oui. 3. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minOpérations(vecteur<int>& nums, cible int) {
somme longue = 0;
pour (int v : nombres) somme += v;

si (somme < cible) retour -1;
si (somme == cible) retourne 0;

priority_queue<int> pq(nums.begin(), nums.end()); // max‐heap
Int ops = 0;

pendant que (cible) {
int x = pq.top(); pq.pop();

si (somme - x >= cible) { // skip
somme -= x;
} sinon si (x <= cible) { // utiliser
cible -= x;
somme -= x;
} autre { // split
si (x > 1) {
pq.push(x/2);
pq.push(x/2);
ops++;
}
}
}
les opérations de retour;
}
};
«» "

Les trois solutions fonctionnent dans le temps `O(n log n)` et la mémoire `O(n)` – bien dans les limites du problème.



---

## Bonne, mauvaise et moche – Pièges communs

Question de ce qu'il ressemble Correction / Meilleure pratique Autres
Il y a un problème.
**Skipping when sum‐x < cible**=________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________ Toujours soustraire l'élément de `sum` *avant la vérification*. Autres
**Splitter La tentative de diviser `x = 1` lance une exception ou donne lieu à une boucle sans fin. Autres Séparer seulement si `x > 1`. Autres
**Dépassement de la somme**= Utiliser `int` pour la somme totale supérieure à 231 peut déborder. Conservez la somme dans un type 64-bit (`long` / `long long`). Autres
Autres **L'utilisation d'un heap min sans négation ni comparaison personnalisée conduit à choisir l'élément *le plus petit*, ce qui brise la logique gourmande. Utilisez un max-heap ou poussez des valeurs négatives. Autres
**Missing Base Cases**= Oublier `sum=cible=============================================================================================================================================================================================================================================== Autres

---

Analyse de complexité

Étape Coût
- Oui.
Autres Calcul de la somme Autres
Construction de puits (Java: `addAll`; C++: constructeur; Python: `heapify`) Autres
Chaque itération effectue une opération de tas ("O(log n)").
Dans le pire des cas, nous avons divisé chaque élément jusqu'à ce que tous deviennent `1`.
Total des scissions ≤ nombre de fois que nous double la longueur du tableau, qui est limité par "sum(nums)".
Par conséquent, la complexité globale est « O(n log n) ». Autres
Mémoire "O(n)" pour le tas. Autres

---

- Oui. Que faire si les nombres n'étaient pas des puissances de deux? (en milliers de dollars)

La même stratégie cupide **ne** travaille pour les entiers arbitraires positifs, parce que l'opération fractionnée produit toujours deux nombres plus petits qui ajoutent au même total.
Seule la restriction "powers-of-two" nous donne la garantie pratique *exact de décomposition binaire* qu'une solution existe toujours quand "sum ≥ cible".
Si vous supprimez cette garantie, vous auriez besoin d'un algorithme DP ou sous-ensemble plus sophistiqué.



---

## À emporter pour l'intervieweur

1. ** Expliquez le bilan de santé total** – montre que vous comprenez les invariants.
2. **Montrer le tas** – les intervieweurs adorent voir une structure de données en action.
3. **Discuse le raisonnement cupide "skip" ou "split"** – démontre la conception algorithmique.
4. **Parcourez un court exemple** sur le tableau.
5. **Mention le `O(n log n)` lié** – l'intervieweur sera impressionné par votre conscience de la complexité.

---

## SEO-Friendly Conclusion

> **Vous souhaitez améliorer votre performance d'entrevue de codage? * *
> Le problème 2835 est une vitrine parfaite pour les algorithmes *greedy*, *priority queues* et *bit manipulation*. La maîtrise de ce défi vous permet non seulement de décrocher un badge LeetCode de qualité supérieure, mais aussi de vous équiper d'un démarreur de conversation pour des entretiens techniques, en particulier dans les domaines de l'ingénierie logicielle aux startups Google, Amazon, Microsoft et fintech.
> Pratiquez avec les trois implémentations propres ci-dessus, modifiez-les pour votre langue préférée, et vous serez prêt à affronter même les puzzles d'interview les plus difficiles.

**Mots clés:** LeetCode 2835, Opérations minimales pour former subséquence, Problèmes de LeetCode dur, Préparation d'entrevue, Conception d'algorithme, Approche de la graisse, PriorityQueue, Heapq, C++ priority_queue, Java PriorityQuie, Python LeetCode Solutions, Tech Interview Tips.