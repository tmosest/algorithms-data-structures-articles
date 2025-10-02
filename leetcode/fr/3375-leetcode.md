---
titre: LeetCode 3375. Opérations minimales pour rendre les valeurs de répartition égales à K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Opérations minimales pour rendre les valeurs de répartition égales à K
*(LeetCode 3375 – Facile)*

> **Récapitulation des problèmes**
> Vous recevez un tableau entier `nums` et une valeur cible `k`.
> Dans une opération, vous pouvez choisir un entier `h` de telle sorte que **tous** éléments plus grands que `h` soient *identiques*.
> Ensuite, vous définissez chaque élément `> h` à `h`.
> L'objectif est de transformer chaque élément en "k" en "nums" en utilisant le moins d'opérations possible.
> Retour `-1` si c'est impossible.

> **Principales contraintes *
> * `1 ≤ longueur nominale ≤ 100`
> * `1 ≤ nombres[i], k ≤ 100`

---

- Oui. 1. Pourquoi la réponse est le nombre de valeurs distinctes supérieures à k

1. **Vous ne pouvez jamais augmenter une valeur** – une opération réduit seulement les nombres.
2. **Vous ne pouvez toucher qu'un ensemble de nombres égaux** – tous les nombres plus grands que votre 'h' choisi doivent être les mêmes.
Par conséquent, si vous avez deux valeurs *différentes* plus grandes que `k`, vous ne pouvez pas les fusionner en une seule étape.
3. **La réduction d'une valeur supérieure à `k` nécessite exactement une opération** – choisissez `h = k`, puis tous les nombres `> k` deviennent `k`.
Mais vous ne pouvez le faire que si l'ensemble *current* de nombres plus grands que `k` est déjà identique.
Donc, vous devez d'abord "flatten" le tableau en tournant la plus grande valeur en la prochaine plus grande, et ainsi de suite.

Ainsi, le processus est équivalent à :
> Pour chaque valeur distincte `v` qui est **> k**, vous avez besoin d'une opération pour l'effondrer à la valeur distincte plus petite suivante (ou directement à `k`).
> Le nombre total d'opérations correspond au nombre de valeurs distinctes > k.

La seule fois qu'il est impossible est quand il y a un nombre **plus petit que k** – vous ne pouvez jamais l'élever à `k`.

---

- Oui. 2. Solution optimale (temps O(n), espace O(n)

Texte
1. Si un élément < k → retourne -1.
2. Compter combien de valeurs distinctes > k apparaissent dans les nombres.
3. Rends ce compte.
«» "

Parce que les contraintes sont minuscules, même une solution O(n log n) basée sur le tri fonctionne, mais l'approche de hachage est propre et rapide.

---

- Oui. 3. Mise en œuvre du code

Voici des solutions prêtes à être collées dans **Java, Python et C++**.

#### 3.1 Java

"Java
Importer java.util. HashSet;
Importer java.util. Jeu;

solution de classe publique {
Activités(int[] nums, int k) {
int min = entier. MAX_VALEUR;
Définir <Intégrer> plusSet = nouveau HashSet<>();

pour (int num : nombres) {
si (num < k) retour -1; // impossible
si (num > k) plusSet.add(num);
min = Math.min (min, num);
}

retourner plus grandSet.size();
}
}
«» "

3.2 Python

'`python
Solution de classe:
def minOperations(self, nombres: List[int], k: int) -> Int:
# Sortie anticipée si un nombre est inférieur à k
le cas échéant(x < k pour x en nombres):
retour -1

# Compter des nombres distincts supérieurs à k
retourner len({x pour x en nombres si x > k})
«» "

### 3.3 C++

'`cpp
solution de classe {
public:
int minOpérations(vecteur <int>& nums, int k) {
unordered_set<int> plus grand; // valeurs distinctes > k
pour (int x : nombres) {
si (x < k) retour -1; // impossible
si (x > k) plus.insérer(x);
}
retour plus grand.size();
}
};
«» "

Les trois solutions fonctionnent en **O(n)** temps et utilisation au maximum **O(n)** espace supplémentaire pour le hachage.

---

- Oui. 4. Les bons, les mauvais et les laids – Ce que veulent vraiment les intervieweurs

Aspect du bien
- C'est quoi ?
Autres **La complexité du temps est optimale. O(n log n) (sort) est acceptable mais moins élégant. La simulation de la force brute O(n2) est un drapeau rouge. Autres
Autres **Utilisation de l'espace**= Constante ou O(n) pour un ensemble de hachage. O(n) est fine, avec des limites minuscules. Attribution inutile de grands tableaux ou ensembles de bits > 100 k.
**Manipulation d'un cas d'urgence** En oubliant la règle "plus petite que k" → mauvaise réponse sur les tests cachés. Ne pas gérer les tableaux vides ou les cas à élément unique gracieusement. Autres
**Readability**= Logique claire d'un liner.=Les boucles ou le tri des aiguilles sont trop compliqués. Le mélange de fonctions de langage (par exemple, Python `set` dans une boucle) dans une seule solution. Autres
**Explainabilité**= Expliquez pourquoi les valeurs distinctes > k comptent; liez-les à la règle d'opération. Il suffit de compter distinctement > k. Sans raisonnement. Réclamation Nous pouvons toujours descendre à k directement – manque l'exigence de valeur identique. Autres

- Oui. Comment parler dans une interview

1. **Énoncez votre intuition d'abord** – Je ne peux que diminuer les valeurs, donc une valeur inférieure ne peut pas devenir k ; donc toute valeur < k est impossible. (en milliers de dollars)
2. **Sketch le processus** – Je dois d'abord aplatir la plus grande valeur, puis la suivante ... chaque valeur distincte > k coûte une opération. (en milliers de dollars)
3. **Cliquer sur la structure des données** – A HashSet me donne le temps O(n) ; je vais juste insérer tous les nombres > k et ensuite retourner sa taille. (en milliers de dollars)
4. **Déplier les cas de bordure** – Si le tableau contient déjà seulement `k`, nous renvoyons 0; s'il contient une valeur < k, nous renvoyons -1; sinon la taille définie est la réponse. (en milliers de dollars)

---

- Oui. 5. Tester votre solution

Autres Cas d'essai prévu Explication
- C'est quoi ?
`nums = [9,10,5,10,8]`, `k=5`" `3`" Les valeurs distinctes > 5 sont {9,10,8}. Autres
«nombres = [5,5,5]», `k=5`-" `0`-" Déjà tous k. Autres
"nums = [4,5,6]", "k=5" "1" 4 < 5, impossible. Autres
`nums = [7,7]`, `k=5`=1`= Une seule opération distincte > 5 → une. Autres

Exécutez ces tests dans votre IDE ou juge en ligne pour vérifier l'exactitude.

---

- Oui. 5. Pourquoi ce problème est un grand exercice d'entretien

* Il force les candidats à traduire un **processus** (flattant par des valeurs identiques) en une propriété **statique** (valeurs distinctes > k).
* Il teste la compréhension des compromis entre les ensembles de trésorerie* et le triage*.
* Il vérifie si le candidat constate l'impossibilité* (valeurs < k).

La plupart des intervieweurs aiment une solution qui est:

1. **Simple** – logique d'un liner plus un petit jeu d'aide.
2. **Correct** – passe tous les cas d'angle.
3. **Bien commenté** – vous pouvez indiquer les trois règles qui justifient l'algorithme.

---

- Oui. 6. méta-données de blogs favorables au référencement

html
<meta name="description" content="Apprendre à résoudre LeetCode 3375 – Opérations minimales pour faire des valeurs de répartition égales à K en Java, Python et C++. Découvrez la solution O(n) optimale et les conseils d'entrevue.">
<meta name="keywords" content="LeetCode 3375, Minimum Operations to Make Array Values Equal to K, Java solution, Python solution, C++ solution, problème d'entretien, interview de codage, algorithme, hashset, O(n) time">
<title>LeetCode 3375: Opérations minimales pour faire des valeurs de représentation égales à K – Solutions Java/Python/C++ et conseils d'entrevue</title>
«» "

---

- Oui. 7. Liste de contrôle à emporter pour la préparation de l'entrevue

1. **Lire attentivement l'énoncé** – identifier les opérations interdites (vous ne pouvez pas augmenter les valeurs).
2. **Règles en contraintes** – ici, vous ne pouvez toucher que des nombres égaux.
3. **Chercher le nombre minimal de points** – souvent la réponse est simplement le nombre de valeurs distinctes au-dessus d'un seuil.
4. **Mise en œuvre avec un hachage** – garantit le temps O(n) et l'espace O(n).
5. ** Expliquez votre raisonnement** – soulignez pourquoi la solution est optimale et pourquoi les cas de bord comptent.

---

La pensée finale

Le problème des opérations minimales est un exemple de manuel de la façon dont **une transformation apparemment compliquée se résume à un simple problème de comptage**.
Maîtrisez-le, et vous aurez une solution propre et efficace qui impressionne les intervieweurs et les scores élevés sur LeetCode!