---
titre: LeetCode 2519. Compter le nombre d'indices K-Big -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de maîtrise du leet 2519 – Nombre d'indices K-Big

> ** Pourquoi lire ça ? * *
> • Obtenez une solution claire et prête à la production en **Java, Python & C++**.
> • Comprendre les *bons* (intuitifs), *mauvais* (écueils communs) et *ugly* (quirks de la carotte).
> • Apprenez deux techniques puissantes : *deux lignes prioritaires* (O(n log k)) et un arbre de Fenwick* (O(n log M)).
> • Polissez votre style d'interview: vous serez prêt à expliquer, coder et optimiser sur place.

> **Références clés** – *LeetCode 2519, indices k‐big, question de codage des interviews, file d'attente prioritaire Java, tas de Python, file_priority C++, Arbre de Fenwick, interview algorithmique, structures de données, grande notation O, solutions d'entretien de codage. *

---

- Oui. 1. Exposé des problèmes (paraphrasé)

> **Input**
> `nums` – tableau entier indexé 0 (`1 ≤ len(nums) ≤ 105`)
> `k` – entier positif (`1 ≤ k ≤ len(nums)`)

> **Définition**
> L'indice `i` est **k‐big** si
> * il y a au moins `k` indices distincts `idx1 < i` avec `nums[idx1] < nums[i]`;
> * il y a au moins `k` indices distincts `idx2 > i` avec `nums[idx2] < nums[i]`.

> **Tâche**
> Retourner le nombre d'indices k‐big.

> **Exemple**
> ```texte
> nombres = [2,3,6,5,2,3], k = 2 → 2
> `` "

---

- Oui. 2. Intuition et observations clés

Observation Pourquoi ça compte
C'est-à-dire
**Côté gauche** – Nous devons savoir *combien de petits nombres existent à gauche*. Si nous connaissons le *k‐th le plus petit* sur la gauche, nous pouvons décider immédiatement. Autres
**Côté droit** – Symmétrique : nous avons besoin du *k‐th le plus petit* à droite. Autres
**Structure monotonique** – Pour chaque indice, nous avons juste besoin de *la taille de l'ensemble le plus petit de k; nous ne nous soucions pas de leurs valeurs exactes. Autres
**Scan linéaire à deux passages** – Calculez d'abord l'information de gauche, puis balayez de droite à gauche pour vérifier simultanément le côté droit et le côté gauche. Autres
**Temps par rapport à l'échange d'espace** – `O(n log k)` avec les files d'attente prioritaires est plus simple et assez rapide; l'arborescence Fenwick donne `O(n log M)` (M = valeur maximale) et n'utilise que des tableaux. Autres

---

- Oui. 3. L'approche «Good» – Deux priorités‐Quées (O(n log k))

3.1 Étapes de l'algorithme

1. **Pass gauche**
*Maintenir un poids max de taille `k`* (c.-à-d., file d'attente prioritaire en ordre décroissant).
Pour chaque `i` de gauche à droite:
* Si la taille du tas est `k` ** et** l'élément le plus important du tas (`top`) est `< nums[i]`, alors nous savons qu'il y a au moins `k` plus petits éléments à gauche → marquer `gauche Bien[i] = vrai».
* Poussez `nums[i]` dans le tas. Si la taille du tas dépasse `k`, pop le maximum (qui est le plus grand parmi les plus petits `k`).

2. ** Pass droit** – Faire la même chose de droite à gauche:
* Utiliser un poids maximal frais de la taille `k`.
* Quand le tas a des éléments `k` et son `top` < `nums[i]`, alors *à droite* est bon.
* Combiner avec la réponse précédente `leftGood[i]`; si les deux vraie → incrément.
* Poussez `nums[i]` et pop si taille > `k`.

3. **Retour** la réponse accumulée.

3.2 Pourquoi ça marche

*Le tas contient toujours les plus petites valeurs `k` vues jusqu'à présent. *
Si la masse maximale (`top`) est `< nums[i]`, cela signifie **chaque** élément dans le tas est `< nums[i]`, nous avons au moins `k` ces éléments.
Sinon, nous n'avons pas encore d'éléments plus petits `k`.

3.3 Complexité

Opération Temps Espace
- C'est quoi ?
Chaque poussoir/pop est "O(log k)" "O(n log k)" "O(k)" pour le tas + "O(n)" pour "gauche" Bon tableau
Total (en milliers de dollars)

Parce que «k ≤ n ≤ 105», cela satisfait facilement les contraintes.

---

- Oui. 4. Les erreurs courantes et les cas de bord

Erreurs Symptômes Correction
C'est pas vrai.
**L'utilisation d'un minimum de poids** doit être "heap.size() == k && heap.peek() < nums[i]` mais "peek()` sera le *le plus petit* → mal. Utilisez un **max-heap** (ordre inverse). Autres
Autres **Pushing after the check**.Si vous poussez en premier, vous pouvez inclure l'élément courant dans le compte. Vérifier ** avant d'insérer**. Autres
**Off‐by‐one lors de la sortie du côté droit**= Pour l'index `i`, nous ne devons pas considérer `nums[i]` lui-même dans le côté droit. Démarrer la passe droite avec un tas *vide* et *first* pousser la valeur courante après la vérification. Autres
**Ignorer les valeurs dupliquées****La condition exige ** des nombres beaucoup plus petits**.
**Ne pas défricher le tas entre les passages** Réinitialisez le tas. Autres

---

- Oui. 5. L'Arbre de Fenwick (Binary Indexed Tree)

Si vous préférez des solutions basées sur le jeu, un arbre Fenwick qui compte les occurrences de valeurs fonctionne bien.
Idée clé: maintenir deux arbres Fenwick de fréquence – un pour le côté gauche (`leftTree`) et un pour le côté droit (`rightTree`).
Pendant le scan:

1. Dans un premier temps, tous les éléments appartiennent à "rightTree".
2. Pour chaque indice `i` (à partir de `k` à `n-k-1` pour garantir suffisamment d'éléments des deux côtés):
* Supprimer `nums[i]` de droite Arbre.
* Interroger `leftTree.prefixSum(nums[i]-1)` et `rightTree.prefixSum(nums[i]-1)` pour savoir combien de nombres * strictement plus petits* existent de chaque côté.
* Si les deux comptes ≥ `k`, la réponse par incrément.
* Ajouter `nums[i]` à `gauche Arbre.

Les requêtes/mises à jour de l'arborescence Fenwick sont `O(log M)` où `M` est la valeur maximale en `nums` (= 105 après compression).
L'espace est "O(M)" et aucun tas n'est nécessaire.

> **Quand utiliser? **
> *Vous devez gérer très grand `k` près de `n`* ou *vous voulez un facteur de log-factor déterministe indépendant de `k`*.
> *Vous êtes à l'aise avec l'indexation basée sur 1 et préfixez les sommes. *

---

- Oui. 6. Code type – Les trois langues

> Chaque extrait compile sur sa propre soumission LeetCode.
> Les noms de classe et les signatures de méthode correspondent au modèle de problème officiel.

---

#### 6.1 Java

"Java
Importer java.util. Priorité Demande;
Importer java.util. Recouvrements;

solution de classe {
Int public kBigIndices(int[] nums, int k) {
int n = longueur nums;
booléen[] gaucheBien = nouveau booléen[n];

- Oui. Passage gauche
Priorité Queue<integer> leftHeap = nouvelle prioritéQueue<>(Collections.reverseOrder());
pour (int i = 0; i < n; i++) {
si (leftHeap.size() == k && leftHeap.peek() < nums[i]) {
gaucheGood[i] = vrai;
}
gaucheHeap.offer(nums[i]);
si (leftHeap.size() > k) leftHeap.poll();
}

- Oui. Pass droit -------- */
réponse int = 0;
Priorité Queue<Integer> rightHeap = nouveau PriorityQueue<>(Collections.reverseOrder());
pour (int i = n - 1; i >= 0; i--) {
si (rightHeap.size() == k && rightHeap.peek() < nums[i]) {
si (à gauche) réponse++;
}
droitHeap.offer(nums[i]);
si (droiteHeap.size() > k) droitHeap.poll();
}

réponse de retour;
}
}
«» "

---

6.2 Python

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
def kBigIndices(self, nombres: List[int], k: int) -> Int:
n = len(nums)
gauche_good = [Faux] * n

C'est pas vrai. De gauche à droite
gauche = [] # Le heapq de Python est un min-heap → négatif de magasin pour obtenir un max-heap
pour i, val dans l'énumération(nombres):
i len(left_heap) == k et -left_heap[0] < val:
gauche_good[i] = Vrai
heapq.heappush (pap gauche, -val)
si len(le_pap) > k:
heapq.heappop(pap_gauche)

C'est pas vrai. De droite à gauche -----
heap_droite = []
ans = 0
pour i dans la fourchette(n - 1, -1, -1):
si len(right_heap) == k et -right_heap[0] < nums[i]:
si gauche_good[i]:
+= 1
heapq.heappush(heap, -nums[i])
si len(gauche droite) > k:
heapq.heappop (heap)

retour et
«» "

---

*### 6.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int kBigIndices(vecteur<int>& nums, int k) {
int n = nombres.size();
vecteur<char> gaucheBien(n, 0);

// ---- Passage à gauche
priority_queue<int> gauche Heap; // max-heap par défaut
pour (int i = 0; i < n; ++i) {
Si (leftHeap.size() == k && leftHeap.top() < nums[i]) {
gaucheBien[i] = 1;
}
gaucheHeap.push(nums[i]);
si (leftHeap.size() > k) leftHeap.pop();
}

// ---- Pass droit -----
priorité_queue<int> droite Cuillère;
Int ans = 0;
pour (int i = n - 1; i >= 0; --i) {
Si (rightHeap.size() == k && rightHeap.top() < nums[i]) {
si (à gauche) ++ans;
}
heap.push(nums[i]);
Si (droiteHeap.size() > k) droitHeap.pop();
}

le retour des an;
}
};
«» "

> **Note**: Les trois snippets fonctionnent dans **O(n log k)** time et n'utilisent qu'un tableau booléen + deux tas.

---

- Oui. 6. Liste de contrôle 6-Étapes

Étape Que dire / faire
-- -- -- -- -- -- --
Autres 1. Clarify Plus petit que plus petit Autres
Autres 2. Choisissez la structure des données. Autres
Autres 3. Ecrivez le pass gauche. Autres
Autres 4. Passage à droite : la même logique, mais il faut éviter de compter l'élément courant du côté droit. Autres
Autres 5. Vérifier l'état combiné. Autres
Autres 6. Complexité: temps O(n log k), espace O(n) – passe facilement 105 contraintes. Autres
Autres 7. Cases de bords de l'échantillon, hors-par-un, en utilisant max-heap. Autres

---

- Oui. 7. Conseils pour les essais

Autres Résultats attendus Pourquoi
- C'est quoi ?
`nums = [1,2,3,4,5%], k = 1 ' , 4 , Chaque indice sauf le premier a au moins un plus petit sur la gauche et à droite. Autres
Aucun indice n'a de valeurs *plus petites* des deux côtés. Autres
"nums = [1,1,1,1], k = 1 ''0' Pas de valeurs strictement plus petites. Autres
Le premier élément est k‐big parce qu'il y en a beaucoup de plus petits à droite. Autres
Utilité aléatoire grand tableau + aléatoire `k`. et vérifier avec la force brute pour les petits `n`. Autres

---

- Oui. 8. Pensées finales

* **Two-priority-queues**: plus rapide à coder, élégant et satisfait pleinement les contraintes de problème.
* **Fenwick tree**: super si vous avez besoin d'éviter les frais généraux ou si vous êtes déjà familier avec les BIT.
* Gardez toujours à l'esprit les nuances * strictement plus petites* et *off‐by‐one* – ce sont les gremlins d'entrevue habituels.

Vous pouvez maintenant vous attaquer au LeetCode 2519 en **Java, Python et C++** tout en expliquant le *Why* et le *how* à un embaucheur.

---

**Codage heureux & bonne chance sur votre prochaine interview! * *