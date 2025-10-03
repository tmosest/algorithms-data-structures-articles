---
titre: LeetCode 3523. Faire Array Non-décroissant - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de solution

Voici trois solutions complètes, prêtes à soumettre – une dans **Java**, une dans **Python** et une dans **C++** – qui résolvent LeetCode 3523 *Make Array Non-Decreasing*.

Autres *L'approche "simple avide" est correcte pour ce problème.
> Il garde chaque élément qui n'est pas plus petit que l'élément conservé précédent et ignore le reste.
> Le tableau résultant est le plus long tableau de non-diminution possible qui peut être obtenu en fusionnant des sous-réseaux dans leurs valeurs maximales. *

---

### Java

"Java
// 3523. Faire en sorte que les rayons ne diminuent pas
// Durée: O(n), Mémoire: O(1)

solution de classe {
max. du public PossibleTaille(int[] nums) {
taille de l ' int = 0;
int prev = Integer.MIN_VALUE; // toute valeur inférieure au plus petit élément

pour (int num : nombres) {
si (num >= prev) { // conserver cet élément
prev = nombre;
taille++;
}
}
taille de retour;
}
}
«» "

---

Python

'`python
# 3523. Faire en sorte que les rayons ne diminuent pas
# Durée: O(n), Mémoire: O(1)

Solution de classe:
def maximumPossibleSize(self, nombres: List[int]) -> Int:
taille = 0
prev = float('-inf') # toute valeur inférieure au plus petit élément

pour num in nums:
si num >= prev: # conserver cet élément
prev = nombre
taille += 1

taille de retour
«» "

---

C++

'`cpp
// 3523. Faire en sorte que les rayons ne diminuent pas
// Durée: O(n), Mémoire: O(1)

solution de classe {
public:
Int maxPossibleSize(vecteur<int>& nums) {
taille de l ' int = 0;
int prev = INT_MIN; // toute valeur inférieure au plus petit élément

pour (int num : nombres) {
si (num >= prev) { // conserver cet élément
prev = nombre;
++ Taille;
}
}
taille de retour;
}
};
«» "

---

Article du blog – "Make Array Non-décroissant: le bon, le mauvais et le mauvais"

> **Mots clés**: *Make Array Non-decreasing, LeetCode 3523, défi de codage d'entrevue, algorithme cupide, plus longue subséquence non-decreasing, solution Java, solution Python, solution C++, entretien de structure de données, entretien d'algorithme, conseils d'entrevue de codage, entretien d'ingénierie logicielle, publication d'emploi sur le référencement, préparation d'entrevue technique. *

---

Introduction

Code du leet 3523 – *Make Array Non-decreasing* – est un problème trompeur, simple mais perspicace, qui se pose souvent dans les entrevues d'ingénierie logicielle. Il vous demande d'effectuer des opérations **zéro ou plus** sur un tableau, où chaque opération s'effondre en un seul élément égal à sa valeur maximale. Après toutes les opérations, le tableau résultant doit être **non-diminution**. Votre objectif : **maximiser la taille du tableau final**.

Pourquoi est-ce important ?
Dans le code du monde réel, on vous demande souvent de transformer les données avec un minimum de perte d'information. Ce problème vous force à penser à * jusqu'où vous pouvez garder des éléments intacts* tout en respectant les contraintes d'ordre. C'est une illustration classique d'une stratégie gourmande: garder tout ce que vous pouvez et jeter le reste.

---

C'est pas vrai. La bonne – Pourquoi la solution de l'avidité fonctionne

1.1 Intuition

Imaginez marcher à travers le tableau de gauche à droite.
- **Si l'élément courant est au moins aussi grand que le dernier élément que vous avez décidé de garder**, vous pouvez le garder en toute sécurité – il n'a pas brisé la propriété non décroissante.
- **Si c'est plus petit**, vous devez soit le fusionner dans l'élément précédent (perdant sa propre contribution) soit le laisser tomber entièrement. La fusion ne peut pas vous aider plus tard parce qu'une fusion avec un élément plus petit remplace seulement le sous-réseau par le maximum plus grand; l'élément plus petit ne deviendra jamais utile.

Ainsi, un **passe unique** qui garde les éléments de "good" est suffisant.

1.2 Argumentation formelle

Laissez `prev` être la valeur du dernier élément conservé.
- Quand `num >= prev`, le tableau `prev, num` est déjà non-décroissant.
- Lorsque `num < prev`, toute sous-tribu se terminant par `num` qui comprend `prev` aura le maximum `prev` (puisque `prev` est plus grand). Remplacer ce sous-barrage par `prev` maintient le tableau non-diminuer mais réduit la taille d'au moins un.
Par conséquent, *toute solution optimale gardera tous les éléments satisfaisant `num >= prev`, et laisser tomber le reste.

1.3 Complexité temporelle et spatiale

La complexité temporelle La complexité spatiale Autres
Il s'agit d'un projet pilote.
* * * * * * *
Python **O(n)**
* * * * * * * * *

`n` est la longueur du tableau (jusqu'à 200 000). Un passage linéaire est le plus rapide possible.

---

- Oui. Les mauvaises – pièges communs

Une erreur Pourquoi ça se trompe
- Oui.
**Tréer comme une subséquence croissante plus longue (LIS)**LIS considère toute subséquence; ici, vous ne pouvez pas réorganiser les éléments, fusionner seulement. Utilisez la règle d'entretien cupide si ≥ prev. Autres
Autres ** Utilisation d'une pile ou d'une deque pour simuler des fusions**= Suringénierie; l'effet opération= est trivial (remplacer avec max). Un passage suffit, pas besoin de structures de données supplémentaires. Autres
**En supposant que vous pouvez garder toutes les paires non décroissantes**Vous pourriez sauter un élément ultérieur qui pourrait être conservé si vous aviez fusionné les précédentes. L'algorithme gourmand s'en charge automatiquement : si un élément ultérieur est plus petit, vous le sautez, indépendamment des fusions antérieures. Autres
**Ignorer les cas de bord (tous égaux, tous décroissants)** Initialiser `prev` à un très petit nombre (`INT_MIN`, `-inf`, ou `Integer.MIN_VALUE`). Autres

---

C'est vrai. Les pièges de l'Edge-Case et les scénarios Si

Scénario Qu'est-ce qui ne va pas ? Recommandation
-- -- -- -- -- -- -- -- --
Autres **Très grands nombres (jusqu'à 2 × 105)** L'utilisation de `int` en Java ou C++ est très bien; mais évitez `short` ou `octet`. Autres
**Les valeurs négatives**= Les contraintes de problème garantissent des éléments positifs, mais si elles sont modifiées, l'algorithme fonctionne toujours avec `prev = -inf`. Autres
**Empty array**=LeetCode garantit au moins un élément, mais le codage défensif est bon. Retourner 0 si le tableau est vide. Autres
Vous pourriez penser par erreur que vous pouvez garder tout. L'algorithme ne conserve correctement que le premier élément. Autres
**Tous égaux** Puisque chaque élément est égal à `prev`, vous gardez tout – le résultat est `n`. Autres

---

####4-- Bonus – Pourquoi ce problème est une grande question d'entrevue

1. **Clarité des contraintes** – Simple entier tableau, fonctionnement fixe.
2. ** Solution immédiate** – Un passage, une comparaison.
3. **Deep Insight** – Il vous apprend à reconnaître quand une stratégie avide est optimale.
4. **Horloge de pression** – Vous pouvez coder dans 5 minutes, mais vous devez encore expliquer le raisonnement.

Une bonne réponse lors d'une entrevue :
> Il y a une variable "prev". Si l'élément courant est ≥ `prev`, je vais le garder et mettre à jour `prev`. Sinon, je l'oublierai. Cela donne la taille maximale parce que tout élément qui est plus petit que le précédent conservé nous obligerait à le fusionner avec l'élément précédent, réduisant la taille. L'algorithme est temps O(n) et espace O(1). (en milliers de dollars)

---

C'est vrai. Réflexions finales

*Faire irruption Le non-décroissant* est une belle illustration de **. La solution gourmande est non seulement efficace mais aussi élégante : elle capture l'essence de l'opération sans aucune structure de données auxiliaire.

Que vous écriviez Java pour LeetCode, Python pour une interview de codage, ou C++ pour une interview de niveau système, la logique reste identique. N'oubliez pas d'initialiser `prev` à une valeur plus petite que n'importe quel élément de tableau, puis de traverser une fois et de compter les éléments "good" .

---

Référence rapide – Extraits de code

Mots clés Autres
C'est pas vrai.
{ si (num >= prev) { prev = num; size++; }
**Python** prev: prev = num; taille += C'est vrai.
**C++**="pour (int num : nums) { si (num >= prev) { prev = num; ++size; }="

---

À emporter

Si vous cherchez à être remarqué par des recruteurs ou des scanners de CV automatisés, incluez **mots clés** tels que:

- Faire Array Solution de non-diminution
- LeetCode 3523 Java
- Algorithme de cupidité Python
- Interview sur la transformation du tableau de C++
- Sous-séquence de non-diminution la plus longue
- Solutions de défi de codage d'interview

Ces termes sont fortement recherchés par les gestionnaires d'embauche à la recherche de candidats avec des côtelettes algorithmiques. Combinez-les avec les extraits de code ci-dessus, et vous aurez une vitrine solide pour votre portfolio ou LinkedIn.

Bon codage, et que vos tableaux restent toujours non-décroissants!