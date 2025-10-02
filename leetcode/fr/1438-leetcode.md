---
titre: LeetCode 1438. Subarray continu le plus long avec diff absolu inférieur ou égal à limite -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1438. Subarray continu le plus long avec écart absolu ≤ limite
Code Leet – Moyen

** Exposé des problèmes* *

> Compte tenu d'un tableau entier «nums» et d'une «limite» entière, retourner la taille de la sous-aire la plus longue *non-vide* de sorte que la différence absolue entre deux éléments de cette sous-aire soit au plus «limite».

«» "
Entrée : nombres = [8,2,4,7] , limite = 4
Produit : 2
«» "

**Pourquoi est-ce intéressant? **
La solution naïve (vérifier chaque sous-aire possible) est \(O(n^2)\) et sera temps-out sur la taille d'entrée maximale \(n = 10^5\).
Une solution de fenêtre coulissante linéaire utilisant deux deques (ou une file d'attente BST/priorité équilibrée) fonctionne en \(O(n)\) et est le modèle canonique -greedy + data structuration-) que les intervieweurs aiment.

---

- Oui. 1. Algorithme – Fenêtre coulissante à deux étages

1. Gardez deux deques :
* `maxDeque` – stocke des indices d'éléments dans l'ordre **decreasing** (le front est le maximum actuel).
* `minDeque` – stocke des indices d'éléments dans l'ordre **croissant** (le front est le minimum actuel).
2. Étendre la fin droite de la fenêtre une étape à la fois.
* Alors que le nouvel élément est plus petit que le dos de `maxDeque`, pop le dos - nous ne conservons que des candidats utiles pour le maximum.
* Alors que le nouvel élément est plus grand que le dos de `minDeque`, pop le dos - nous ne gardons que des candidats utiles pour le minimum.
* Poussez le nouvel index sur les deux deques.
3. Après avoir ajouté l'élément, vérifiez si la fenêtre est **valide**:
\[
nombres[maxDeque.front] - nombres[minDeque.front] \le limite
\]
Si c'est **invalid**, rétrécissez la fenêtre de la gauche (`gauche`) jusqu'à ce qu'elle redevienne valide, en supprimant les indices qui quittent la fenêtre de l'avant de chaque deque.
4. Mettre à jour la réponse avec la taille actuelle de la fenêtre (` droite - gauche + 1`).

**Pourquoi ça marche ? **
Comme les deques tiennent toujours la fenêtre actuelle maximum et minimum, la différence peut être obtenue en \(O(1)\).
Lorsque la fenêtre devient invalide, nous savons que l'élément qui a causé la violation doit être sur le côté gauche - le déplacement `gauche` vers l'avant le supprime. Cela garantit que chaque index est inséré et supprimé au plus une fois → temps linéaire.

---

- Oui. 2. Complexité

Opération Temps Espace
- C'est quoi ?
Loop principal \(O(n)\)=" \(O(n)\) (deques, mais chaque index enregistré une seule fois)="
Réponse finale Autres

---

- Oui. 3. Mise en œuvre des références

### Java

"Java
Importer java.util. - ArrayDeque;

solution de classe publique {
public int le plus longSubarray(int[] nums, int limit) {
ArrayDeque<Integer> maxQ = nouveau ArrayDeque<>(); // décroissant
ArrayDeque<Integer> minQ = nouveau ArrayDeque<>(); // augmentant
int gauche = 0, ans = 0;

pour (int droite = 0; droite < nums.longueur; droite++) {
// maintenir la quantité maximale
alors que (!maxQ.isEmpty() && nums[maxQ.peekLast()] < nums[right]) {
maxQ.pollLast();
}
maxQ.offreDernière(à droite);

// maintenir min deque
pendant que (!minQ.isEmpty() && nums[minQ.peekLast()] > nums[right]) {
minQ.pollLast();
}
minQ.offreDernière(à droite);

// Réduire la fenêtre si nécessaire
alors que (nums[maxQ.peekFirst()] - nombres[minQ.peekFirst()] > limite) {
si (maxQ.peekFirst() == gauche) maxQ.pollFirst();
si (minQ.peekFirst() == gauche) minQ.pollFirst();
gauche++;
}

ans = Math.max(ans, droite - gauche + 1);
}
le retour des an;
}
}
«» "

Python

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
plus longtemps Subarray(self, nombres: Liste[int], limite: int) -> Int:
max_q = deque() # décroissant
min_q = deque() # augmentant
gauche = 0
ans = 0

pour droite, num in énumérate(nums):
pendant que max_q et nums[max_q[-1]] < num:
_q.pop() max
max_q.append(droite)

alors que min_q et nums[min_q[-1]] > num:
min_q.pop()
min_q.append(droite)

pendant les nombres[max_q[0]] - nombres[min_q[0]] > limite:
Si max_q[0] == gauche:
max_q.popleft()
si min_q[0] == gauche:
min_q.popleft()
gauche += 1

ans = max(ans, droite - gauche + 1)
retour et
«» "

C++

'`cpp
#incluez <vecteur>
#incluez <deque>
#incluez <algorithme>

solution de classe {
public:
int le plus long Subarray(std:vector<int>& nums, limite int) {
std::deque<int> maxQ; // décroissant
md::deque<int> minQ; // augmentation
int gauche = 0, ans = 0;

pour (int right = 0; right < (int)nums.size(); ++right) {
pendant que (!maxQ.vide() && nums[maxQ.back()] < nums[right])
maxQ.pop_back();
maxQ.push_back(droite);

pendant que (!minQ.vide() && nums[minQ.back()] > nums[right])
minQ.pop_back();
minQ.push_back(à droite);

pendant que (nums[maxQ.front()] - nombres[minQ.front()] > limite) {
si (maxQ.front() == gauche) maxQ.pop_front();
si (minQ.front() == gauche) minQ.pop_front();
+ + gauche;
}
ans = md::max(ans, droite - gauche + 1);
}
le retour des an;
}
};
«» "

---

- Oui. 4. Article de blog – *Le bon, le mauvais, et le mauvais des solutions de fenêtre coulissante*

Introduction

Lorsque vous voyez un problème de LeetCode intitulé "Longest Continuous Subarray ...", votre esprit court immédiatement à *sliding window*. Les fenêtres coulissantes sont le pain-and-butter de la préparation d'entrevue : elles sont rapides, intuitives et souvent la seule solution acceptable pour les grandes contraintes d'entrée.

Dans ce post, nous allons marcher à travers les aspects **good**, **bad** et **ugly** des solutions de fenêtre coulissante pour LeetCode 1438, *Longest continue Subarray with Absolute Diff ≤ Limit*. Je vais décomposer l'algorithme, montrer le code Java/Python/C++ propre, et donner des conseils qui vous aideront à briller dans une interview technique ou un blog de recherche d'emploi.

> **Fonctionnement du référencement**: "Master LeetCode 1438: Sliding-Window Deques to Pass in O(n) – Java, Python & C++"

---

Les bons

Pourquoi ça compte ?
C'est-à-dire
**Temps linéaire**
**O(1) amortised window updates** Autres
**Readability**=Two deques + pointers== Facile à expliquer dans une interview. Autres
**Mémory friendly**= Chaque index stocké une fois== \(O(n)\) dans le pire des cas, mais les deques sont minuscules. Autres

Le *good* est évident : l'algorithme est optimal pour les contraintes du problème et utilise un modèle de structure de données propre que les intervieweurs aiment.

---

- Oui. Les mauvais

Sujet Atténuation
C'est quoi, ça ?
**Complexité du cas d'Edge**= Manipulation des taches vides lors du rétrécissement== Vérifier soigneusement `front()` avant de sauter. Autres
**Language quirks**=Java's `ArrayDeque` vs `LinkedList`=Utilisez `ArrayDeque` pour O(1) ops. Autres
**Les plus grandes valeurs entières**= `int` vs `long`= En Java, utilisez `int` parce que les limites du problème s'adaptent, mais attention si vous prolongez la logique. Autres
**Pièges de lisibilité**=Décommentation excessive par rapport à l'abstraction excessive=Tenir un équilibre: ne commenter que les parties non évidentes. Autres

Ce sont des ennuis mineurs qui apparaissent si vous collez un modèle sans comprendre la nuance de chaque langue.

---

- Oui. L'Ugly

Pièges
C'est pas vrai.
**Bogues hors-par-un**=La boucle de rupture peut laisser la fenêtre invalide==Vérifier après la boucle avec un test d'affirmation ou d'unité. Autres
**O(n2) dans les cas les plus graves**. Autres
Autres **Débordement de la pile sur la récursion**. Aucun dans ce problème. Autres
Autres **La limite de temps dépasse sur la grande entrée**= Extra `Math.max` boucle intérieure== Déplacez-la si vous le pouvez, mais ici elle est bon marché. Autres

La partie *ugly* nous rappelle que la fenêtre coulissante est puissante **seulement** si elle est correctement implémentée. Une seule typo dans la logique de la tâche peut transformer une solution optimale \(O(n)\) en solution lente.

---

- Oui. 5. Comment montrer ceci sur votre blog ou un résumé

1. **Titre** – Faire en sorte qu'il soit riche en mots-clés : « Subarray continu le plus long » (LeetCode 1438) – Déques de fenêtres coulissantes en Java, Python, C++.
2. **Intro** – Présentez brièvement le problème et le défi de la grande contribution.
3. **Section d'algorithme** – Utilisez un pseudo-code et diagrammez vos deques.
4. **Analyse de complexité** – Notation Big-O avec explications.
5. **Les extraits de code** – Inclure les trois implémentations linguistiques. Mentionnez que les deques sont les pinces.
6. **Discussion** – Bon, mauvais, laid – vous montre que vous ne vous contentez pas de copier; vous comprenez les compromis.
7. **Lien** – Fournir l'URL LeetCode et un lien vers une repo GitHub avec la solution complète.
8. **Balises de référence** – LeetCode 1438, La fenêtre coulissante, Java Deque, Python Deque, C++ Deque, O(n) solution, Interview technique.

L'ajout d'une petite section de test unitaire ou d'un point de repère de performance (p. ex. « timeit » en Python) donne au lecteur une confiance supplémentaire.

---

- Oui. 6. Liste de contrôle à emporter

- Utilisation **deux deques**: une pour max, une pour min.
- Maintenez les deques dans l'ordre **monotonique**.
- Réduire la fenêtre jusqu'à la différence ≤ limite.
- Mise à jour de la réponse après chaque extension.
- Éviter les erreurs hors-par-un en testant les cas de bord.

---

### TL;DR

- Problème: Subarray le plus long avec la limite ≤max‐min.
- Solution : Fenêtre coulissante + deux deques (fiscales monotoniques).
- Complexité: \(O(n)\) temps, \(O(n)\) espace.
- Code prêt pour Java, Python, C++.

> **Conseil pro**: Lorsque vous expliquez cela à un intervieweur, commencez par -Je garde le maximum et le minimum de la fenêtre actuelle en deques afin que je puisse connaître la différence en O(1). Puis je glisse la fenêtre jusqu'à ce que la différence soit ≤ limite. C'est un pas de 10 secondes qui montre instantanément le motif.

Bon codage – et bonne chance pour ce travail!