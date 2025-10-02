---
titre: LeetCode 2644. Trouvez le score maximal de divisibilité -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2644. Trouvez le score maximal de divisibilité
**LeetCode 2644 – Facile**

> **Objectif** – Pour chaque diviseur `d` dans `diviseurs`, compter le nombre de nombres dans `nums` qui sont divisibles par `d`.
> Rends le diviseur avec le nombre **maximum**; si plusieurs diviseurs sont liés, retourne le nombre **le plus petit**.

> **Constraints**
> * 1 ≤ "longueur en chiffres", "longueur en diviseurs" ≤ 1000
> * 1 ≤ `nums[i]`, `diviseurs[i]` ≤ 109

Parce que les limites sont minuscules, une double boucle simple court en moins d'un milliseconde. Vous trouverez ci-dessous des implémentations propres et prêtes à la production dans **Java, Python et C++**.

---

- Oui. 1. Solution Java

"Java
// 2644. Trouvez le score maximal de divisibilité – Java
solution de classe {
Int public maxDivScore(int[] nombres, int[] diviseurs) {
// le résultat tient le diviseur avec le meilleur score jusqu'à présent
// maxCount détient sa partition
résultat int = 0;
int maxCount = -1; // garantit que le premier diviseur gagne des liens

pour (int diviseur : diviseur) {
nombre int = 0;
pour (int num : nombres) {
Si (num % de diviseur) 0) nombre++;
}
// Mettre à jour si nous avons trouvé un score plus élevé, ou un score égal mais un diviseur plus petit
si (comptez > maxCount=" (compte == maxCount && diviseur < résultat)) {
maxCount = nombre;
résultat = diviseur;
}
}
le résultat du retour;
}
}
«» "

**Pourquoi ça marche* *

* "O(n · m)" temps – deux boucles imbriquées, chacune à au plus 1000 itérations.
* "O(1)" espace supplémentaire – seulement quelques variables entières.

---

- Oui. 2. Solution Python

'`python
# 2644. Trouvez le score maximal de divisibilité – Python
def maxDivScore(nums: List[int], diviseurs: List[int]) -> Int:
résultat, max_count = 0, -1 # même idée que Java
pour les diviseurs:
nombre = somme (1 pour nombre en nombres si nombre % diviseur == 0)
if count > max_count ou (count == max_count et diviseur < result):
_compte max = compte
résultat = diviseur
résultat du retour
«» "

*Utilise une expression de générateur pour la brièveté tout en conservant le même temps d'exécution `O(n·m). *

---

- Oui. 3. Solution C++

'`cpp
// 2644. Trouvez le score maximal de divisibilité – C++
solution de classe {
public:
Int maxDivScore(vecteur<int>& nums, vecteur<int>& diviseurs) {
résultat int = 0;
d'une puissance n'excédant pas 1 kW
pour (int d : diviseurs) {
cnt = 0;
pour (int num : nombres)
si (num % d) 0) + cnt;
si (cnt > maxCount) {
maxCount = cnt;
résultat = d;
}
}
le résultat du retour;
}
};
«» "

*Simple, lisible et entièrement conforme au juge LeetCode. *

---

- Oui. 4. Promenade du blog À travers: Le Bon, le Mauvais, et l'Ugly

### 4.1 Récapitulation du problème

> **Input** – Deux tableaux "nums" et "diviseurs".
> **Output** – Diviseur de "diviseurs" qui divise le plus de nombres en "nums".
> **Tie‐breaker** – Retourne le plus petit diviseur lorsque l'attache est multiple.

#### 4.2 Le bon – Pourquoi l'approche de la force brute gagne

1. **Simplicité** – Deux boucles imbriquées, pas de structures de données supplémentaires.
2. **Correctness by construction** – Chaque paire `(diviseur, num)` est examinée exactement une fois.
3. ** Performance prévisible** – `n,m ≤ 1000` garanties < 1 million d'itérations, bien en dessous des délais.
4. ** Facile à tester** – Vous pouvez énumérer toutes les possibilités manuellement.

### 4.3 Les mauvaises – Où les Brutes La force pourrait échouer

1. **Évoluabilité** – Si les contraintes s'élevaient à 105, « O(n·m) » serait irréalisable.
2. **Cache-miss lourd** – La boucle intérieure est liée à la mémoire pour de très grands tableaux.
3. ** Travail rémunéré** – La même opération de module est recalculée pour chaque diviseur.

> *Conseils du monde réel:* Pour le code de qualité de production, il faut tenir compte du nombre de diviseurs avant le calcul ou utiliser une carte de hachage clé par le reste. Mais pour ce problème, la solution simple est optimale.

4.4 Les cas les plus odieux et les pièges communs

Pourquoi ça arrive
- Oui.
Autres **Mettre à jour le résultat en utilisant `<=` au lieu de `<`. Utiliser `si (compte > maxCount=" (compte == maxCount && divisor < result))`. Autres
**Valeur de résultat initiale**=Le paramètre `result` à `diviseurs[0]` et `maxCount` à `0` peut sauter un diviseur avec 0 score si tous ont 0. Initialise `maxCount = -1` pour que le premier diviseur gagne toujours des liens. Autres
**Excédent** , `num % divisor` correspond à `int` pour les valeurs ≤ 109, mais si les valeurs étaient plus grandes, vous auriez besoin de `long`. , Utilisez `long` pour la sécurité lorsque les valeurs approchent 231−1. Autres
**Les tableaux d'empty**= Non permis par les contraintes, mais le codage défensif est bon. Ajouter un garde: si `divisors.isEmpty()` retour `-1`. Autres

4.5 Analyse de la complexité

Heure de mise en œuvre
- Oui.
Java / Python / C++
*Explication* : deux boucles imbriquées, variables auxiliaires constantes. Autres

Avec `n, m ≤ 1000`, le pire des cas est d'environ 1 000 000 opérations – facilement gérées par n'importe quel processeur moderne.

### 4.6 Entretien– Conseils prêts

1. **Exposer la force brute d'abord** – Il démontre la compréhension de l'énoncé du problème.
2. **Mentions les contraintes** – Montrez-vous où la solution est efficace.
3. **Discuse les optimisations possibles** – Parlez des ensembles de diviseurs précomputants ou utilisez une table de fréquence si les contraintes changent.
4. **Écrire un code propre, commenté** – Les recruteurs aiment le code durable.
5. **Cas de bord de test** – Tous les zéros, tous les mêmes nombres, tableaux d'éléments uniques.

4.7 À emporter

> Pour LeetCode 2644, une solution à double boucle est **parfaitement adéquate**.
> La clé de l'entrevue n'est pas seulement l'algorithme, mais aussi votre **clarité de pensée**, **sensibilité aux cas de référence** et **code propre**.

> Continuez à pratiquer des problèmes similaires de comptage :
> * 1815. Compter les éléments correspondant à une règle (LeetCode)
> * 1515. Coût minimum pour embaucher des travailleurs K (Code Leet)
> Ils renforcent les boucles, l'arithmétique modulaire et la logique de rupture des liens.

---

- Oui. 5. SEO-Optimized Meta‐Description (pour votre CV ou blog)

> Apprendre à résoudre le LeetCode 2644 – Trouvez le score maximal de divisibilité – avec le code Java, Python et C++ propre. Comprenez la complexité du temps et de l'espace, la logique de rupture des liens et les conseils prêts pour l'entrevue pour décrocher votre prochain emploi en génie logiciel. (en milliers de dollars)

N'hésitez pas à copier les extraits de code, à publier le billet de blog ou à intégrer la discussion à votre prochaine entrevue de codage. Bon codage !