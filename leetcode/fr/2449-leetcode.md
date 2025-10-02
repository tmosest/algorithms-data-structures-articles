---
titre: LeetCode 2449. Nombre minimum d'opérations pour rendre les tableaux similaires -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

- Oui. 1. Récapitulation des problèmes

**LeetCode 2449 – Nombre minimum d'opérations pour rendre les tableaux similaires**

«» "
Entrée
nombres : int[] (taille n)
cible : int[] (taille n)

Fonctionnement
Choisissez deux indices différents i, j
nombres[i] += 2
Nombres[j] -= 2

Deux tableaux sont *similaires* lorsque chaque valeur apparaît le même nombre de fois dans chaque tableau.

Objectif
Retourner le nombre minimum d'opérations nécessaires pour faire des "nums" semblables à "cible".

Garantie
Il est toujours possible de transformer des "nums" en un tableau similaire.
«» "

Les contraintes (`n ≤ 105`, valeurs ≤ 106) nous obligent à penser en **O(n log n)** ou mieux.

---

- Oui. 2. Aperçu clé – La parité est immuable

L'ajout ou la soustraction de `2` ne modifie jamais la **parité** (odd/even) d'un nombre.
Par conséquent:

Un élément peut se déplacer vers un élément ne peut se déplacer vers un élément
- C'est quoi ?
Un autre impair
Encore un autre

Donc :

*Le nombre d'éléments impairs dans `nums` doit correspondre au nombre d'éléments impairs dans `target`, et le même pour les paires. *
Le problème le garantit, de sorte que nous pouvons séparer en toute sécurité les deux groupes de parité.

---

- Oui. 3. Correspondance d'avidité après tri

Une fois que nous avons divisé les deux tableaux en seaux impairs et même, la tâche devient :

> Pour chaque seau, jumeler chaque élément de "nums" avec un élément de "cible" afin que le coût total
> (nombre d'opérations) est minimisé.

**Pourquoi trier les travaux* *

Si nous trions à la fois `nums_odd` et `target_odd`, l'appariement optimal est simplement `nums_odd[i] Cible_odd[i]».
Il s'agit d'une somme minimum classique des différences absolues où l'ordre trié donne le minimum.

La même logique s'applique au seau uniforme.

---

- Oui. 4. Calcul des coûts

Pour une paire `a, b)` (à la fois bizarre ou même) nous devons faire `a` égal à `b` en ajoutant à plusieurs reprises 2 à l'un et en soustrayant 2 de l'autre.

La différence `a - b=" est toujours égale (les deux nombres ont la même parité).
Chaque opération change la différence de `4` (augmentation de 2, baisse de l'autre de 2).
Ainsi le nombre d'opérations nécessaires pour cette paire est

«» "
A — B — 2
«» "

Parce que chaque opération touche **deux** indices, la somme sur toutes les paires doit être divisée par «2» à la fin.

---

- Oui. 5. Formule finale

«» "
total_moves = ( < < odd_i > > - cible < < Odd_i > > / 2
- cibleEven_i / 2 ) / 2
«» "

Tous les arithmétiques correspondent à 64 bits (long/long) parce que
`n * maxDiff / 2 ≤ 105 * 106 / 2 = 5·1010`, bien au-dessous de 263.

---

- Oui. 6. Mise en œuvre

Ci-dessous sont propres, implémentations idiomatiques dans **Java, Python, et C++**.
Les trois partagent la même structure : scindé par parité → trier → accumuler des différences absolues → scinder par 2.

> **Conseil pour les entrevues** – écrivez une fois la partie scission par parité, puis simplement la réutiliser pour les groupes bizarres et même.

---

#### 6.1 Java

"Java
Importation de java.util.*;

solution de classe {
public longue makeSimilar(int[] nums, int[] cible) {
Liste<entier> impairNums = nouvelle liste d'array<>();
Liste<entier> evenNums = nouvelle liste d'array<>();
Liste<Intégrer> impairTarget = nouvelle liste de distribution<>();
Liste <Integer> evenTarget = nouvelle liste d'array<>();

pour (int i = 0; i < nombres de longueur; i++) {
si ((nums[i] & 1) == 0) mêmeNums.add(nums[i]); sinon impairNums.add(nums[i]);
si ((cible[i] & 1)] 0) evenTarget.add(cible[i]); sinon impairTarget.add(cible[i]);
}

Collections.sort(oddNums);
Collections.sort(mêmeNums);
Collections.sort(oddTarget);
Collections.sort(evenTarget);

longs mouvements = 0;
pour (int i = 0; i < impairNums.size(); i++)
se déplace += Math.abs(oddNums.get(i) - impairTarget.get(i)) / 2;
pour (int i = 0; i < evenNums.size(); i++)
+= Math.abs(evenNums.get(i) - evenTarget.get(i)) / 2;

les mouvements de retour / 2;
}
}
«» "

---

6.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def makeSimilar(self, nombres: List[int], cible: List[int]) -> Int:
impair_nums, even_nums = [], []
impair_cible, even_cible = [], []

pour n, t en zip(nombres, cible):
si n & 1:
impair_nums.append(n)
Sinon:
even_nums.append(n)
si t & 1:
impair_cible.append(t)
Sinon:
even_target.append(t)

impair_nums.sort()
even_nums.sort()
impair_cible.sort()
even_target.sort()

mouvement = 0
mouvements += somme(abs(a - b) // 2 pour a, b dans zip(odd_nums, impair_target))
se déplace += somme(abs(a - b) // 2 pour a, b dans zip(even_nums, even_target))

mouvement de retour // 2
«» "

---

*### 6.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
longue makeSimilar(vecteur<int>& nums, vecteur<int>& cible) {
vecteur<int> impairNum, mêmeNum, impairTar, même Tar;
pour (size_t i = 0; i < nums.size(); ++i) {
si (nums[i] & 1) impairNum.push_back(nums[i]); sinon mêmeNum.push_back(nums[i]);
si (cible[i] & 1) impairTar.push_back(cible[i]); sinon mêmeTar.push_back(cible[i]);
}

tri(oddNum.degin(), impairNum.end());
tri(evenNum.begin(), evenNum.end());
tri(oddTar.begin(), impairTar.end());
tri(evenTar.begin(), evenTar.end());

longs déplacements longs = 0;
pour (size_t i = 0; i < impairNum.size(); ++i)
mouvements += llabs(oddNum[i] - impairTar[i]) / 2;
pour (size_t i = 0; i < evenNum.size(); ++i)
mouvements += llabs(evenNum[i] - même Tar[i]) / 2;

les mouvements de retour / 2;
}
};
«» "

---

- Oui. 7. Analyse de la complexité

Opération Temps Mémoire
C'est quoi ?
Partition par parité
Autres Tri de chaque liste **O(n log n)** (somme de quatre sortes, mais globale O(n log n))
Résumé
**O(n log n)**

Cela répond aux contraintes confortablement.

---

- Oui. 8. Les cas de bord et les Ugly

La situation Pourquoi c'est difficile
- C'est pas vrai.
Autres Vous devez retourner `0` – l'algorithme donne naturellement "0" Pas besoin de manipulation spéciale. Autres
Autres Le problème garantit la faisabilité, donc les comptes correspondent toujours. Autres Faites confiance à la garantie – sinon vous devrez retourner `-1` ou lancer. Autres
De grands nombres (près de 106) sont parfaits; Python utilise une précision arbitraire. Autres
Un seul élément, le nombre de fonctionnement doit être `0`. Autres

---

- Oui. 9. Autres approches (pourquoi nous les avons évitées)

1. **Greedy sans tri* *
- L'appariement dans un ordre arbitraire peut entraîner des coûts sous-optimaux.
- Le tri garantit une somme minimale de différences absolues.

2. **Deux points sur les listes triées**
- Similaire au tri + balayage linéaire ; notre solution le fait déjà implicitement.

3. **Multi-set / Carte de fréquence**
- Vous pouvez suivre le nombre de chaque numéro dont vous avez besoin, mais le coût d'une opération dépend de la différence numérique, pas seulement compte.
- Par conséquent, une carte de fréquence simple manque l'aspect de magnitude de déplacement.

---

## 10. Article de blog – Le bon, le mauvais, et le mauvais

> ** Mots-clés de référence**: `leetcode 2449`, `array transformation`, `parity cupidy`, `opérations minimales`, `algorithm interview`, `Java Python C++ solution`, `job interview coding "

---

#### 10.1 Introduction

Dans le contexte de l'embauche concurrentielle d'aujourd'hui, les questions de codage des entrevues sont souvent les premiers gardiens.
LeetCode 2449, *Nombre minimal d'opérations pour rendre les tableaux similaires*, est un problème apparemment simple qui révèle en fait beaucoup de votre pensée algorithmique.

Cet article passe par les aspects **good**, **bad** et **ugly** de la solution, explique pourquoi le tri par parité est la clé, et montre comment le mettre en œuvre dans **Java, Python et C++**.

À la fin, vous aurez non seulement une implémentation de référence propre, mais aussi un récit que vous pouvez discuter avec confiance dans une entrevue.

---

#### 10.2 Le bon – Un propre, O(n log n) Solution

* ** Invariance de rareté** – Une seule observation : l'ajout ou la soustraction de 2 conserve impair/even.
Cela écroule un problème à deux dimensions en deux dimensions.

* **Traitement des graisses** – Une fois divisé, l'appariement optimal est réalisé en alignant les tableaux triés.
C'est un truc algorithmique classique : *sort, paire par index, calcul du coût*.

* **Simplicité en code** – Trois fonctions presque identiques en trois langues faciles à lire, à tester et à expliquer.

---

### 10.3 Les mauvaises – Pièges potentiels

1. **La parité méconnaissable** – Beaucoup de candidats pensent à tort qu'un élément peut sauter à travers les parités.
En soulignant cela au cours de la conversation, vous comprenez les contraintes.

2. **Sur-ingénierie** – Essayer d'utiliser des structures de données complexes ( files d'attente prioritaires, cartes) masque le coût réel d'une opération : la différence numérique, et pas seulement les comptages.

3. **Ignorer les débordements** – Comprenant jusqu'à 5×1010 opérations avec des débordements entiers 32 bits en Java/C++.
Utilisez des types 64 bits et expliquez le raisonnement.

---

#### 10.4 Les horribles subtilités cachées

* **Pourquoi trier fonctionne** – L'appariement arbitraire d'éléments peut conduire à un nombre d'opérations exponentiellement plus grand.
Par exemple, la correspondance d'un très grand nombre impair avec un petit nombre impair tout en ignorant un partenaire plus proche entraîne des déplacements inutiles.

* **Divisant par deux** – Chaque opération touche *deux* indices, de sorte que la somme naïve sur les paires est *deux fois* la vraie réponse.
L'oubli de la division finale conduit à un bug commun hors-par-deux.

* **Cas d ' urgence** – Bien que le problème garantisse la faisabilité, la manipulation `n = 1` ou des tableaux déjà similaires gracieusement est toujours essentielle.
Une boucle bien structurée renvoie automatiquement 0, mais vous devriez la mentionner dans votre explication.

---

#### 10.5 L'horrible – Quand ça tourne mal

Imaginez que vous essayez de résoudre le problème en construisant une carte de fréquence de `nums` et `cible`.
Vous remarquerez correctement que la parité compte, mais vous serez toujours coincé :

> Je dois augmenter de 7 à 11, mais je ne sais pas combien d'opérations ça prend vraiment. (en milliers de dollars)

Le coût dépend de la distance *numérique*, pas seulement de la présence d'une valeur.
Le fait de manquer cette nuance peut conduire à une simulation de la force brute de 100 lignes qui s'arrête sur l'ensemble d'essai.

---

10.6 Parler À propos de la solution dans une entrevue

1. **Énoncer l'écart de parité** – Cela montre que vous pouvez repérer des invariants.
2. **Expliquez la stratégie à deux coups** – Odd ne peut passer qu'à étrange, voire à pair. (en milliers de dollars)
3. **Justifier le tri** – -Le tri aligne les plus petites différences, ce qui donne la somme minimale des différences absolues. (en milliers de dollars)
4. **Afficher les maths** – Pour une paire `(a,b)` chaque opération touche deux indices, donc nous divisons le total par 2. (en milliers de dollars)
5. **Complexité de la concentration** – temps O(n log n), espace O(n), confortablement dans les contraintes. (en milliers de dollars)
6. **Illustrez les conseils spécifiques au langage** – Javas `ArrayList`, Python=s list comprehensions, C++=s `labs`.

Si vous pouvez articuler ces étapes en 5-7 minutes, vous impressionnerez n'importe quel intervieweur.

---

### 10.7 Conclusion

LeetCode 2449 est une vitrine parfaite de la façon dont un **simple invariant** (parité) transforme un tableau complexe en un algorithme avide rangé.
Le **good** est une implémentation propre et prête à l'essai.
Le **mauvais** est la tentation d'être trop compliqué.
Le **ugly** est l'écueil subtil des opérations de comptabilisation erronée en raison du mélange de parité.

Apportez les trois codes de référence à votre prochaine entrevue, expliquez l'idée de base dans vos propres mots, et vous vous démarquerez comme un candidat qui peut ** transformer la perspicacité en élégance**.

---

> **Auteur**: *[Votre nom]* – Ingénieur à fond et coach d'entrevue
> **Suivez** sur Linked In ou GitHub pour plus d'algorithmes.

---

11. Pensée de clôture

La parité est souvent le gardien caché dans les problèmes de tableau.
Une fois que vous l'avez remarqué, beaucoup de questions apparemment difficiles se réduisent en sous-problèmes gérables.

N'hésitez pas à adapter les implémentations ci-dessus à votre propre style de codage et à les amener avec confiance lors de votre prochaine entrevue. Bon codage ! C'est ce qu'il a dit.

---


# 2449. Nombre minimum d'opérations pour rendre les tableaux similaires
## Déclaration du problème
Compte tenu de deux tableaux entiers, "nums" et "cible", tous deux de taille "n", trouver le nombre minimum d'opérations nécessaires pour rendre "nums" égal à "cible". Dans chaque opération, vous pouvez :

1. Choisissez une position `i` dans `nums` et ajoutez 2 à la valeur **original** à cette position.
2. Choisissez une position `i` dans `cible` 1.
Le problème indique qu'il y a une opération **réversible** que nous venons d'avoir un **invariant** à **compte** **n**-1/??? Ce problème date de 2449.
Nous devons trouver le nombre minimum de **s**.. **?**


On nous demande de résoudre le problème de Leetcode 2449 - Nombre minimum d'opérations pour rendre les tableaux similaires. Nous devons fournir une solution. La conversation: l'utilisateur a posté une déclaration de problème mais avec quelques erreurs, mais nous devons donner une réponse complète. La conversation a aussi eu une explication de solution : invariance de parité, fractionné impair/even, trier, calculer le coût. Nous devons produire une réponse finale qui couvre cela.

Nous devons produire une description de la solution et peut-être un code. Nous pouvons produire la réponse finale comme une explication complète avec le code en Java, Python, C++.

Compte tenu de l'« analyse » ci-dessus, nous pouvons produire une réponse finale résumant le problème, les principaux points de vue, l'algorithme, la complexité et fournir des implémentations.

Ainsi répondez: Problème: Compte tenu de deux séries d'entiers, chaque opération augmente un élément par 2 et diminue un autre par 2, trouver des opérations minimales pour transformer les nombres en cible.

Perspective clé: invariant de parité. Séparer impair/même. Classez chaque groupe. Paire par indices triés, calcul de la différence totale abs, diviser par 2 chaque paire, somme et diviser par 2. Complexité O(n log n).

Nous pouvons fournir du code. Notez également que c'est LeetCode 2449.

Nous pouvons produire une réponse finale en conséquence. Produisons une réponse finale résumant la solution, avec des étapes d'algorithme et des extraits de code en Java, Python, C++.

Nous mentionnerons aussi l'explication.

Répondons.

Nous allons produire une réponse finale:

**Solution**:

- Séparer les nombres impairs/même des nombres et de la cible.
- Triez chaque liste.
- Pour chaque groupe, additionnez la différence abs / 2.
- Diviser la somme totale par 2.

Complexités: Temps O(n log n), espace O(n).

Fournir des implémentations Java, Python, C++.

Nous allons leur donner.

Très bien. Allons-y. **LeetCode 2449 – Nombre minimum d'opérations pour rendre les tableaux similaires**

---

Problème (court)

Pour deux tableaux entiers `nums` et `cible` de la même longueur `n` ( ≤ 105 ), une opération est

* choisir un index ` Les "
* ajouter 2 à la valeur `nums[i]` **ou** à la cible [i] "
* soustrayez 2 de l'autre valeur

Les deux tableaux doivent devenir égaux.
La tâche consiste à produire le nombre d'opérations *minimum*.
(Les valeurs sont ≤ 106, l'ensemble d'essai garantit l'existence d'une solution.)

---

- Oui. Observation clé – la parité ne change jamais

L'ajout ou la soustraction de 2 ne change jamais un nombre d'impair/même nature.
Alors

«» "
les nombres impairs ne peuvent que devenir impairs,
même les nombres ne peuvent que devenir égaux.
«» "

Par conséquent, le nombre de nombres impairs dans `nums` est égal au nombre de nombres impairs dans `target`, et le même pour les paires (la déclaration le garantit).

---

### De la parité à deux problèmes indépendants

Diviser chaque tableau en

* `numsOdd`, `cible Curieuse "
* `numsEven`, `cible Même "

Maintenant le problème est : pour chaque seau, jumeler chaque élément de "nums" avec un élément de "cible" de sorte que le nombre total d'opérations soit minimal.

---

- Oui. Pourquoi le tri donne l'appariement optimal

Pour les deux listes `A` et `B` de même taille, le minimum de

«» "
* A_i - B_{π(i)}
«» "

toutes les permutations π sont réalisées lorsque les deux listes sont triées et appariées par index ('A[i][i][i]').
C'est une somme classique minimum de différences absolues.

Ainsi nous trions les quatre seaux et les paires par index.

---

- Oui. Coût d'une paire

Pour une paire `(a, b)` avec la même parité, `=a – b=` est pair.
Chaque opération change la différence de 4 ( +2 d'un côté, –2 de l'autre), donc le nombre d'opérations nécessaires pour cette paire est

«» "
A — B — 2
«» "

Parce qu'une opération touche deux indices, après avoir additionné toutes les paires, nous divisons le total par 2.

---

Formule finale

«» "
total = ( < < odd_i > > – cible < < od_i > > / 2
2 ) / 2
«» "

Tous les arithmétiques correspondent à 64 bits.

---

Complexité

Étape Temps Espace
(En dollars des États-Unis)
Partition par parité
Trier chaque liste
Montant des différences
**O(n log n)**

Satisfait les limites facilement.

---

## Mise en œuvre des références

### Java

"Java
solution de classe {
public long minimumOpérations(int[] nombres, int[] cible) {
List d'array<entier> impairA = nouvelle List d'array<>();
Tableau <entier> impairB = nouveau tableau<>();
List d'array<entier> evenA = nouvelle List d'array<>();
ArrayList<integer> evenB = nouvelle ArrayList<>();

pour (int i = 0; i < nombres de longueur; i++) {
si ((nums[i] & 1) == 0) {
mêmeA.add(nums[i]);
le nom de l'autorité compétente,
} autre {
les numéros d'ordre suivants:
b) impairB.add(cible[i]);
}
}

Collections.sort(oddA);
Collections.sort(oddB);
Collections.sort(evenA);
Collections.sort(evenB);

longue distance = 0;
pour (int i = 0; i < impairA.size(); i++) {
diff += Math.abs(oddA.get(i) - impairB.get(i));
}
pour (int i = 0; i < evenA.size(); i++) {
diff += Math.abs(evenA.get(i) - evenB.get(i));
}
// chaque paire coûte a-b-
retour diff / 4;
}
}
«» "

Python

'`python
Solution de classe:
def minimumOperations(self, nombres: List[int], cible: List[int]) -> Int:
[]

pour a, b en zip(nombres, cible):
si a & 1:
impair_a.append(a); impair_b.append(b)
Sinon:
even_a.append(a); even_b.append(b)

impair_a.sort(); impair_b.sort()
even_a.sort(); even_b.sort()

diff = somme(abs(a - b) pour a, b dans zip(odd_a, impair_b))
diff += sum(abs(a - b) pour a, b dans zip(even_a, even_b))

retour diff // 4 # deux moitiés de la division
«» "

C++

'`cpp
solution de classe {
public:
longue durée minimumOpérations(vecteur<int> et nombres, vecteur<int> et cible) {
vecteur<int> impairA, impairB, evenA, evenB;
pour (int i = 0; i < nums.size(); ++i) {
i (nums[i] & 1) { impairA.push_back(nums[i]); impairB.push_back(target[i]); }
Autre { evenA.push_back(nums[i]); evenB.push_back(target[i]); }
}

tri(oddA.begin(), impairA.end());
tri(oddB.begin(), impairB.end());
tri(evenA.degin(), evenA.end());
tri(evenB.degin(), evenB.end());

longue distance = 0;
pour (int i = 0; i < impairA.size(); ++i) diff += llabs(oddA[i] - impairB[i]);
pour (int i = 0; i < evenA.size(); ++i) diff += llabs(evenA[i] - même B[i]);

retour diff / 4; // /2 pour coût de paire + /2 pour toucher deux indices
}
};
«» "

---

** À emporter* *
Le nombre minimum d'opérations se trouve en exploitant l'invariant que la parité ne change jamais, se scindant en groupes impairs/même, triant chaque groupe, appariant par index, additionnant les différences absolues (divisées par deux) et finalement divisant le total par deux.
Cela donne une solution `O(n log n)` qui passe facilement les contraintes.