---
titre: LeetCode 1439. Trouver la plus petite somme d'une matrice avec des rangées triées -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Le problème

> **LeetCode 1439 – Trouvez la somme la plus petite d'une matrice avec des lignes triées* *
> **Difficulté**: dur

On vous donne une matrice `m × n` `mat` dont les lignes sont triées dans un ordre non décroissant.
De chaque ligne, vous devez choisir **exactement un élément**, produisant un tableau de longueur `m`.
Parmi tous les tableaux possibles, vous avez besoin de la plus petite somme **kth** de ses éléments.

«» "
Entrée
mat = [[1,3,11],
[2,4,6]]
k = 5

Produit
7
«» "

Les cinq premières plus petites sommes sont
`[1,2] → 3`, `[1,4] → 5`, `[3,2] → 5`, `[3,4] → 7`, `[1,6] → 7`.
La cinquième somme est "7".

«1 ≤ m,n ≤ 40», «1 ≤ k ≤ min(200, m*n)», «1 ≤ mat[i][j] ≤ 5000».



-----------------------------------------------------------------------------------

- Oui. 2. L'Idée – Keep the Best k Sums

Le nombre de toutes les sommes possibles peut être astronomiquement important ('n^m').
Parce que **k est minuscule (= 200)** nous pouvons éviter de tout énumérer.

**Observation principale**
Lorsque vous avez traité les premières lignes `i`, vous n'avez besoin que des sommes partielles *k les plus petites*.
Toute somme qui n'est pas parmi ces k ne peut jamais faire partie d'une somme finale k-th plus petite –
elle serait déjà plus grande qu'au moins k autres sommes partielles.

Donc nous itérer rang par rang, en maintenant un *max-heap de taille au plus k* qui toujours
stocke les k plus petites sommes vues jusqu'à présent.
Quand une nouvelle ligne arrive, nous combinons chaque somme partielle actuelle avec chaque élément de
cette ligne et pousser les nouvelles sommes dans un nouveau tas, jetant les plus grandes
la taille ne dépasse jamais k.

L'algorithme est :

«» "
tas ← [0] // une somme avant que les lignes soient traitées
pour chaque rang r dans le tapis:
nouveaux Heap ← vide max-heap
pour chaque somme en tas:
pour chaque élément v dans les premiers éléments min(k, n) de r:
newHeap.push(s + v)
si newHeap.size > k:
newHeap.pop() // supprimer le plus grand
heap ← nouveauHeap

la plus petite somme k-th
«» "

Comme chaque ligne a au plus des colonnes pertinentes `k` (`k` ≤ 200), les boucles intérieures sont
très petite.
complexité du temps : **O(m · n · k · log k)**
complexité spatiale: **O(k)**

La même idée peut être implémentée avec un *min‐heap* si vous créez tout d'abord
le candidat résume et pop les plus petits k fois, mais le max-heap garde la mémoire
empreinte faible et donne la réponse en un seul passage.

-----------------------------------------------------------------------------------

- Oui. 3. Code – 3 langues

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
public int kthSmallest(int[][] mat, int k) {
Int C = Math.min(mat[0].longueur, k);

// max-heap: plus grand élément en haut
Priorité Queue<Integer> maxHeap = nouveau PriorityQueue<>(Collections.reverseOrder());
maxHeap.add(0); // somme initiale

pour (int[] rang : mat) {
Priorité Queue<Integer> next = new PriorityQueue<>(Collections.reverseOrder());

pour (int prev : maxHeap) {
pour (int c = 0; c < C; ++c) {
suivant.add(prev + ligne[c]);
si (next.size() > k) next.poll(); // ne conserver que k plus petit
}
}
maxHeap = suivant;
}
retour maxHeap.peek(); // k‐th plus petite somme
}
}
«» "

3.2 Python

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
def kthSmallest(self, mat: List[List[int]], k: int) -> Int:
C = min(len(mat[0]), k)

# max-heap via des nombres négatifs
max_heap = [0] # commencer par la somme 0
pour la rangée du tapis:
nouveau_heap = []
pour s dans max_heap:
pour v dans la rangée[:C]:
heapq.heappush(nouveau__heap, -(s + v))
si len(new_heap) > k:
heapq.heappop(new_heap) # chute la plus importante
max_heap = nouveau_heap

# haut du talon max (négatif)
retour -max_heap[0]
«» "

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int kthSmallest(vecteur<vecteur<int>>& mat, int k) {
Int C = min(int)mat[0].size(), k);
// max-heap: priority_queue garde la plus grande taille en haut
priority_queue<int> maxHeap;
maxHeap.push(0); // somme initiale

pour (const auto & rang : mat) {
priorité_queue<int> suivante;
pendant que (!maxHeap.vide()) {
int s = maxHeap.top(); maxHeap.pop();
pour (int i = 0; i < C; ++i) {
suivant.push(s) + ligne[i];
si ((int)next.size() > k) next.pop(); // garder k le plus petit
}
}
maxHeap.swap(suivant);
}
retour maxHeap.top(); // k‐th plus petite somme
}
};
«» "

Les trois solutions fonctionnent dans **O(m · n · k · log k)** temps et utilisation **O(k)** mémoire –
parfait pour les contraintes (`m, n ≤ 40`, `k ≤ 200`).

-----------------------------------------------------------------------------------

- Oui. 4. Article de blog – Le bon, le mauvais, le mauvais de LeetCode Hards

> **Titre**: *Le bon, le mauvais, et le lamentable de LeetCode Problèmes difficiles – un guide de préparation à l'emploi*
> **Meta-description**: Master LeetCode 1439, le plus petit puzzle matriciel de la série "Kth", avec des solutions Java, Python et C++. Apprenez comment transformer les problèmes difficiles en victoires d'entrevue.
> **Mots clés**: LeetCode Hard, 1439, kth plus petite matrice de somme, préparation d'entrevue, entretien d'emploi, conception d'algorithme, max-heap, min-heap, conseils d'entrevue d'emploi

---

Introduction

Les intervieweurs aiment les problèmes de LeetCode. Ils sont la *signature* d'un bon ingénieur.
Mais sont-ils vraiment indiquer la compétence, ou sont-ils juste des puzzles qui vous font transpirer?
Laissez tomber avec l'une des questions les plus bavardes : **LeetCode 1439 – Trouvez la somme la plus petite d'une matrice avec des lignes triées**.

> **Pourquoi ça compte**
> * 1439 apparaît dans la plupart des listes de prép de l'entrevue.
> * Cela vous oblige à penser à des solutions **efficaces pour l'espace**, pas seulement à la force brute.
> * La maîtrise des signaux vous permet de gérer **programmation dynamique + tas** – une mine d'or pour les rôles seniors.

---

### # Le bon – Transformer un problème difficile en une entrevue Gold-Mine

1. ** Contraintes claires* *
* `k ≤ 200`* est un nombre minuscule; l'astuce est de l'utiliser.
Les intervieweurs l'adorent quand on repère que l'on peut *pousser* l'espace de recherche.

2. ** Modèle réutilisable**
La stratégie « Garder les meilleures sommes k » apparaît dans
* [LeetCode 373 – Trouvez des paires K avec les plus petites sommes](https://leetcode.com/problèmes/find-k-pairs-with-sums-smalls/)
* [LeetCode 373 – K Les plus petites paires](https://leetcode.com/problèmes/k-th-small-pair-distance/)
Pratiquer un problème difficile vous apprend un motif réutilisable: **max-heap de taille fixe**.

3. **Solution d'agnostique de la langue* *
Les trois langues ci-dessus résolvent le même problème de la même manière.
C'est le point de conversation parfait : *=Je peux écrire des codes Java, Python et C++ propres et efficaces.

---

Les mauvaises – pièges communs qui vous font perdre

Pourquoi ça fait mal ?
- C'est quoi ?
**Énumération de la force brute**= Espace exponentiellement grand → Time-outs
**Ignorer le nombre de n éléments → O(n2) par ligne
**Type de tas de gonflage**=La logique du tas de gonflage avec le tas de gonflage conduit à O(k2) pop/push==Utiliser le tas de taille k, pop le plus grand en cas de dépassement
**Cas de bord de ne pas sélectionner**=Matrice à ligne unique, lignes avec `n < k`=Poignée `m=1` et `C = min(n, k)` Autres

Lorsque vous tomberez dans l'un de ces pièges, l'intervieweur verra un *manque de perspicacité*.
Une solution propre et efficace en mémoire démontre la maturité algorithmique.

---

### - L'Ugly – Ce que les intervieweurs recherchent (et comment l'éviter)

Ce que les intervieweurs remarquent comment corriger
- C'est quoi ?
J'ai essayé toutes les combinaisons, il a chronométré.
J'ai utilisé la récursion et j'ai obtenu le débordement de la pile. Un DP surrécursif sans mémoisation
*J'ai retourné le mauvais élément (min-pap vs max-pap).** Une mauvaise compréhension du haut du tas

**À emporter**: Si vous pouvez *expliquer* pourquoi un max-pap de taille k fonctionne, vous êtes déjà en avance.

---

- Oui. 5. Conseils d'entrevue

1. **Démarrer avec les contraintes* *
Parce que k ≤ 200, nous ne pouvons garder que les meilleures sommes partielles k.
Les contraintes guident le chemin de la solution.

2. ** Expliquez le "why" avant le "how"* *
Les intervieweurs apprécient la perspicacité.
Nous gardons un lourd max parce que toute somme non parmi les k plus petites sommes partielles ne peut pas être dans la réponse finale. (en milliers de dollars)

3. **Voir les autres approches**
Mentionnez la méthode d'appariement min‐heap, la recherche binaire sur la réponse, etc.
C'est une deuxième façon d'utiliser un minimum de paires. (en milliers de dollars)

4. **Échanges temps/espace**
Discutez de l'approche O(m·n·k·log k) vs. O(m·n·k) et de la raison pour laquelle vous avez choisi le poids maximal.

5. **Écrire un code propre**
*Noms des variables descriptives*, *observations en ligne*, *annotations de type* (Python 3.9+).
Les intervieweurs vérifient la lisibilité autant que la justesse.

6. **Cas de bord des pratiques**
* Ligne unique, colonne unique, toutes valeurs égales, k = m*n. *
Soyez prêt à faire des tests rapides.

7. **Relativement à la vie réelle* *
Dans la production, vous avez souvent besoin des valeurs k les plus petites des flux triés – cet algorithme est le même. (en milliers de dollars)

---

- Oui. 6. Mots de clôture – Obtenez le travail

*Les problèmes difficiles comme LeetCode 1439 ne sont pas seulement des énigmes; ils sont un terrain **test** pour votre instinct de design. *
Lorsque vous pouvez marcher à travers:

* Le **contraintes** → Parce que k est petit... (en milliers de dollars)
* L'idée **core** → -Keep les meilleures sommes k
* L'implémentation **propre** → Java, Python, C++

Vous démontrerez les qualités mêmes que les gestionnaires d'embauche veulent : **la pensée algorithmique, l'attention aux détails et la capacité d'écrire du code prêt à la production**.

Alors la prochaine fois que vous verrez un problème difficile, rappelez-vous:
**Bien** – vous voyez un modèle.
**Bad** – vous perdez du temps à tout énumérer.
**Ugly** – vous appliquez mal les structures de données.

Évitez le mauvais et laid; pratiquez le bon, et vous serez prêt à ass que l'entrevue et atterrir le travail. Bon codage !