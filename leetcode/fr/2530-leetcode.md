---
titre: LeetCode 2530. Score maximal après application des opérations K - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. LeetCode 2530 – Note maximale après application des opérations K

> **Problème**
> On vous donne un tableau `nums` d'entiers positifs et un entier `k`.
> Au départ, votre score est `0`. Dans une opération, vous choisissez un index `i`,
> ajouter `nums[i]` à votre score, et remplacer `nums[i]` par `ceil(nums[i] / 3)`.
> Effectuez **exactement** opérations `k` et retournez le score maximum que vous pouvez atteindre.

> **Constraints**
> * `1 ≤ longueur nominale, k ≤ 105`
> * `1 ≤ nombres[i] ≤ 109`

URL officielle LeetCode: <https://leetcode.com/problèmes/maximal-score-après-application-k-operations/>

---

- Oui. 2. Aperçu de la solution

L'opération vous donne toujours la valeur *current* d'un élément, et après cela
l'élément est réduit à environ un tiers de sa taille antérieure.
Pour maximiser le score total, vous devez toujours choisir le **plus grand** restant
Numéro.

### Greedy + Max-Heap

1. **Construire une file d'attente prioritaire (max-heap**) contenant tous les éléments de «nums».
2. Répéter "k" fois:
* Extraire le plus grand élément `x` (O(log n)).
* Ajouter `x` au score (`long` pour éviter le débordement).
* Calculez `ceil(x / 3)` et repoussez-le dans le tas.

Parce que chaque opération est indépendante, en choisissant le plus grand élément à chaque
étape est optimale – aucune opération future ne peut bénéficier d'une valeur actuelle plus petite.

Complexité

Opération Temps Espace
- C'est quoi ?
"O(n)" Autres
Chaque opération
Total pour "k` ops" Autres

Avec `n, k ≤ 105` cela correspond facilement dans les limites.

---

- Oui. 3. Mise en œuvre complète du code

On trouvera ci-dessous des solutions propres, prêtes à être copiées dans **Java**, **Python** et **C++**.
Tous utilisent un gain max et un accumulateur 64 bits pour la partition.

---

#### 3.1 Java

"Java
Importer java.util. Priorité Demande;

solution de classe publique {
public long maxKelements(int[] nums, int k) {
// Max-heap: élément le plus important à la tête
PrioritéQuue<entier> maxHeap = nouveau PrioritéQuue<>(a, b) -> b - a);
pour (int num : nombres) {
maxHeap.offre(num);
}

long score = 0;
pour (int i = 0; i < k; i++) {
int x = maxHeap.poll(); // valeur la plus élevée
score += x;
int réduit = (int) Math.ceil(x / 3.0);
maxHeap.offrer(réduit);
}
le score de retour;
}
}
«» "

---

3.2 Python

'`python
importation heapq
de maths import ceil
de taper l'importation Liste

Solution de classe:
def maxKelements(self, nombres: List[int], k: int) -> Int:
# Python a un min-heap, donc stocker des négatifs pour simuler un max-heap
max_heap = [-x pour x en nombres]
heapq.heapify(max_heap)

score = 0
pour _ dans la plage(k):
x = -heapq.heappop(max_heap) # élément le plus important
score += x
réduit = ceil(x / 3)
heapq.heappush(max_heap, -réduit)
retour
«» "

---

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long maxKelements(vecteur<int>& nums, int k) {
// Max-heap utilisant priority_queue
priorité_queue <long long> pq;
pour (int num : nums) pq.push(num);

long score = 0;
pour (int i = 0; i < k; ++i) {
long x = pq.top(); pq.pop();
score += x;
longue réduction longue = (x + 2) / 3; // ceil(x/3) pour les entiers positifs
pq.push(réduit);
}
le score de retour;
}
};
«» "

---

- Oui. 4. Plongée profonde de style Blog

> **Titre**: *Mastering LeetCode 2530 – score maximal après application des opérations K avec une approche de la graisse basée sur le talon*
> **Description détaillée**: Apprenez la solution avide + max-heap pour LeetCode 2530. Implantations Java, Python et C++ étape par étape. Augmentez votre score d'entrevue !

4.1 Introduction

Lors de la préparation des interviews de codage, les problèmes qui combinent des choix avides avec une structure de données comme un tas continuent de surgir.
LeetCode **2530 – Score Maximal Après l'application des opérations K** est un parfait exemple.
Il vous demande de choisir à plusieurs reprises l'élément le plus important d'un tableau, de l'ajouter à un total courant, puis de le réduire.

Dans cet article, nous allons parcourir l'intuition, les pièges et les implémentations des meilleures pratiques.

4.2 Réaffirmation du problème

> *Avec un tableau `nums` de taille `n` et un entier `k`, effectuer exactement `k` opérations.
> Dans chaque opération:
> 1. Choisissez l'indice `i' (n'importe quel).
> 2. Ajouter `nums[i]` à votre score.
> 3. Remplacer «nums[i]» par «ceil(nums[i]/3)».
> Retournez le score maximum réalisable. *

### 4.3 Intuition – Pourquoi l'avidité fonctionne

L'opération est **deterministic**: une fois que vous choisissez une valeur, elle contribue immédiatement au score, puis se rétrécit.
Supposons à une étape que vous choisissez un élément sous-optimal `y < x` alors qu'un élément plus grand `x` est disponible.
Parce que les réductions futures dépendent uniquement de la valeur *current*, le choix `y` ne peut plus jamais vous donner un total plus grand que le choix `x`.
Ainsi, la règle cupide, toujours choisir le plus grand élément, est optimale.

4.4 Choix de la structure des données

L'approche naïve de la numérisation du tableau pour le maximum dans chacune des étapes `k` serait `O(k·n)`.
Au lieu de cela, nous maintenons un **max-heap** ( file d'attente prioritaire) qui donne `O(log n)` extraction et insertion.

- **Java**: `PriorityQueue<integer>` avec un comparateur personnalisé `(a, b) -> b - a`.
- **Python**: `heapq` est un min-heap; stocker des négatifs pour inverser la commande.
- **C++**: `priority_queue<long long>` est un max-heap par défaut.

#### 4.5 Pseudocode étape par étape

«» "
construire max-heap à partir de nombres
score = 0
répéter k fois:
x = pop-max()
score += x
y = ceil(x / 3)
Poussez y dans le tas
retour
«» "

4.6 Cas de bord et dépassement

- Utilisez `long`/`long` pour le score de course (`nums[i]` peut être jusqu'à `10^9` et `k` jusqu'à `10^5` → score jusqu'à `10^14`).
- La division Ceil pour les entiers positifs peut être faite comme `(x + 2) / 3` (arithmétique entier).

Bien, mal, Méchant

Catégorie Qu'est-ce que le bien Qu'est-ce que le mal Quoi ?
- C'est quoi ?
**Bon**) • Simple règle d'avidité<br>• Garanties de gain « O(log n) » ops<br>• Poignées de grandes entrées
**Bad** Le calcul Ceil peut prêter à confusion pour les nouveaux arrivants.
**Désormais** Si vous oubliez d'utiliser un max-heap you=ll obtenir de mauvaises réponses<br>• Off‐by‐one en formule ceil peut conduire à des bugs subtils

4.8 Approches alternatives (lorsque le lourd suffit)

- ** Multiset / TreeMap** (C++ / Java): similaire à un tas mais permet une commande personnalisée.
- **Bucket Tri pour petite portée**: Si les valeurs `nums` sont limitées, maintenez les nombres par valeur et traversez de haut en bas.
- ** Programmation dynamique** : Ne s'applique pas ici en raison d'un énorme espace d'état.

Cependant, l'approche du tas reste la plus simple et la plus efficace.

4.9 Pensées finales

*LeetCode 2530* est un exercice classique qui teste votre capacité à traduire une stratégie gourmande en une mise en œuvre efficace en utilisant des tas.
La clé à retenir :

> **Choisissez toujours la plus grande valeur disponible, mettez-la à jour et répétez. **

Avec les extraits Java, Python et C++ ci-dessus, vous pouvez résoudre ce problème avec confiance dans n'importe quel paramètre d'entretien.

---

- Oui. 5. Clôture

N'hésitez pas à copier les extraits de code dans votre éditeur local, à les lancer contre les cas de test LeetCode, et à les modifier au besoin.
Si vous vous préparez à des entretiens techniques, essayez d'étendre ce problème:

- Oui. Que faire si le facteur de réduction change (p. ex. diviser par 4)?
- Oui. Et si vous pouviez sauter les opérations ?

Comprendre le modèle d'avidité basé sur le tas vous servira à bien d'autres problèmes.

---