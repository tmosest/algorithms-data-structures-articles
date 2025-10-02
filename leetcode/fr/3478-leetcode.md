---
titre: LeetCode 3478. Choisir des éléments K Avec une somme maximale -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes

**LeetCode 3478 – Choisissez des éléments K Avec une somme maximale**

*Input*
`nums1`, `nums2` – deux tableaux entiers de longueur `n "
`k` – un entier positif (`1 ≤ k ≤ n`)

*Tâche*
Pour chaque indice «i» (0-basé):

1. Trouver tous les indices `j` de sorte que `nums1[j] < nums1[i]`.
2. Dans ces indices, choisir **au maximum** valeurs `k` de `nums2[j]` qui donnent la somme maximale possible.
3. Conservez cette somme dans `réponse[i]`.

Retourner le tableau `réponse`.

*Contrôles*
«1 ≤ n ≤ 105»
«1 ≤ nombres1[i], nombres2[i] ≤ 106»

La solution classique utilise un **sort + min-heap** ( file d'attente prioritaire) et fonctionne dans le temps `O(n log n)` et `O(k)` espace supplémentaire.

Ci-dessous vous trouverez des implémentations propres et bien commentées dans **Java, Python et C++**.

---

- Oui. 2. Idées fondamentales

1. **Trier par "nums1".**
Lorsque le tableau est trié de plus en plus, chaque élément que nous avons déjà traité a une valeur `nums1` *strictement plus petite* que le présent.
La seule nuance : les duplicatas ne doivent pas être considérés comme plus petits. Nous résolvons cela en regroupant des valeurs égales.

2. ** Maintenez une minute du meilleur `k` `nums2` vu jusqu'à présent. **
- Le tas stocke les valeurs "nums2" les plus importantes.
- `sum` conserve le total actuel du contenu du tas.
- Chaque fois qu'une nouvelle valeur `nums2` est insérée, nous la poussons; si le tas se développe au-delà de `k`, nous pop la plus petite valeur et la soustrayez de `sum`.
Ainsi, la somme est toujours la somme maximale d'éléments au plus `k` qui proviennent d'indices avec un `nums1' plus petit.

3. **Réponse pour un groupe égal de "nums1"**
Pour chaque indice du groupe, nous attribuons le «somme» actuel.
Ce n'est qu'après toutes les réponses pour le groupe que nous ajoutons les valeurs du groupe `nums2` au tas (ils ne sont donc pas comptés pour eux-mêmes).

---

- Oui. 3. Exécution

#### 3.1 Java

"Java
Importation de java.util.*;

***
* LeetCode 3478 – Choisir des éléments K Avec une somme maximale
*/
solution de classe {
public long[] findMaxSum(int[] nums1, int[] nums2, int k) {
int n = nombres1.longueur;
longue[] réponse = nouvelle longue[n];

// jumeler chaque élément avec son index original
int[][] paires = nouvelle int[n][2];
pour (int i = 0; i < n; i++) {
pair[i][0] = nombres1[i]; // valeur pour le tri
paires[i][1] = i; // indice original
}

// trier par nombres1 ascendant
les tableaux.sort(paires, comparator.comparingInt(a -> a[0]);

// min-pap pour les valeurs k les plus grandes nums2 observées jusqu'à présent
Priorité Queue<integer> tas = nouvelle prioritéQueue<>();
long courant Somme = 0;

i = 0;
pendant que (i < n) {
j = i;
// trouver la fin du groupe actuel (tous les nombres égaux1)
pendant que (j < n && pair[j][0] == paires[i][0]) j++;

// La réponse à chaque index du groupe utilise le courant Somme
pour (int t = i; t < j; t++) {
réponse[pairs[t][1]] = courantSum;
}

Ajouter maintenant les valeurs nums2 de ce groupe au tas
pour (int t = i; t < j; t++) {
int idx = paires[t][1];
Int val = nombres2[idx];
heap.offer(val);
actuel Montant += valeur;

// ne conserve que les plus grandes valeurs de k
si (pap.size() > k) {
actuel Somme -= heap.poll();
}
}

i = j; // passer au groupe suivant
}

réponse de retour;
}
}
«» "

3.2 Python

'`python
d'importation heappush, heappop
de taper l'importation Liste

Solution de classe:
def findMaxSum(self, nums1: List[int], nums2: List[int], k: int) -> Liste[int]:
n = len(nums1)
réponse = [0] * n

# valeur de paire avec indice d'origine
paires = triées([(val, idx) pour idx, val dans le dénombrement(nums1)], key=lambda x: x[0])

heap = [] # min-pap des meilleures valeurs k nums2
_somme actuelle = 0
i = 0
alors que i < n:
j = i
alors que j < n et paires[j][0]== paires[i][0]:
j += 1

# réponse pour ce groupe
pour t dans la plage(i, j):
réponse[pairs[t][1]] = current_sum

# ajouter les nombres2 du groupe au tas
pour t dans la plage(i, j):
idx = paires[t] Annexe
val = nombres2[idx]
heappush (pap, val)
current_sum += val
Si len(pap) > k:
current_sum -= heappop(heap)

i = j

réponse de retour
«» "

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<long> findMaxSum(vector<int>& nums1, vector<int>& nums2, int k) {
int n = nombres1.size();
vecteur <long> ans(n, 0);

// paire {nums1 valeur, index original}
le vecteur<pair<int,int>> paires(n);
pour (int i = 0; i < n; ++i) paires[i] = {nums1[i], i};

tri(pairs.begin(), pair.end(), [](const auto& a, const auto& b){
retour a. premier < b. premier;
});

priorité_queue<int, vecteur<int>, plus<int>> minCheap;
long curSum = 0;
i = 0;
pendant que (i < n) {
j = i;
pendant que (j < n && pair[j].first == paires[i].first) ++j; // groupe de nombres égaux1

// 1-- Donner la réponse pour l'ensemble du groupe
pour (int t = i; t < j; ++t)
ans[pairs[t].seconde] = curSum;

Ajouter les nombres2 du groupe dans le tas
pour (int t = i; t < j; ++t) {
int idx = paires[t].seconde;
Int val = nombres2[idx];
minHeap.push(val);
curSum += valeur;
Si ((int)minHeap.size() > k) {
curSum -= minHeap.top();
minHeap.pop();
}
}

i = j;
}
le retour des an;
}
};
«» "

Les trois solutions fonctionnent dans le temps `O(n log n)` et utilisent `O(k)` espace supplémentaire, qui correspond confortablement aux contraintes (`n ≤ 105`).

---

- Oui. 4. Billet de blog – Choisir des éléments K avec la somme maximale: le bon, le mauvais et le mauvais

> ** Mots-clés du référencement**: LeetCode 3478, Choose K Elements Avec maximum Somme, tas de tri, file d'attente prioritaire, conception d'algorithmes, complexité de l'espace temporel, solutions Java, Python, C++

---

4.1 Introduction

Si vous vous adressez à des questions d'entrevue basées sur des réseaux, vous avez probablement vu les meilleurs problèmes de k.
LeetCode 3478 vous demande de faire juste cela – mais avec une torsion ajoutée: les indices que vous pouvez choisir sont **restrictés par une comparaison sur un deuxième tableau**.
Dans ce post, nous traversons la solution **bonne**, signalons les pièges **mauvais** qui font souvent monter les gens, et exposons les cas **meilleures** qui rendent ce problème subtil.

---

### 4.2 Le bien – Pourquoi Cette approche est élégante

1. **Trier donne un ordre linéaire pour le petit* *
Une fois le tableau trié par `nums1`, tous les éléments antérieurs satisfont `nums1[j] < nums1[i]` automatiquement – pas de scans coûteux nécessaires.

2. **Min-heap ne garde que les meilleurs numéros k**
Parce que le tas est un tas *min*, nous pouvons garder exactement les nombres `k` dans `O(log k)` par insertion.
Le « sum » en cours d'exécution vous donne la réponse instantanément – pas de re-scanning ou de recomputation.

3. ** Logique du groupe par valeur égale**
Les duplicata donneraient autrement une mauvaise relation plus petite. Les regrouper assure la rigueur et maintient l'algorithme linéaire après le tri initial.

---

### 4.3 Les erreurs communes

Pourquoi ça se casse
C'est pas vrai.
**En utilisant une comparaison `<=`** pour les duplicata. Groupe égal valeurs et réponse **avant** insérer le groupe. Autres
Autres **Mettre chaque élément individuellement avant d'attribuer des réponses**. D'abord attribuer des réponses à l'ensemble du groupe, puis pousser le groupe dans le tas. Autres
**L'utilisation d'un tableau au lieu d'un tas**=Vous devriez trier chaque fois que vous avez besoin du top-k, transformer l'algorithme en `O(nk)` ou pire.=Utilisez un `PriorityQueue`/`heapq`/`min-heap`. Autres
Autres **En supposant que k est égal à n**, le tas conserverait toutes les valeurs, mais l'algorithme fonctionne toujours; cependant, utiliser un tas dans ce cas est surkill. Autres Si vous voulez un boîtier super-rapide, vous pouvez simplement trier "nums2` et prendre la somme top-k, mais la solution générique reste propre. Autres

---

### 4.4 Les cas de bord et les extensions

1. **Très grand `k`**
Lorsque `k` est proche de `n`, le tas va grandir à cette taille; encore très bien, mais vous pouvez sauter l'entretien du tas entièrement en prenant la somme des premières valeurs `k` triées `nums2`.
*Complexité*: `O(n log n)` toujours.

2. ** Nombres négatifs en nombres2**
L'énoncé de problème garantit des nombres entiers positifs, mais si vous vous détendez cela, la règle de K= est essentielle : vous pouvez choisir moins d'éléments `k` si l'ajout d'une valeur négative réduit le total.

3. **Mettre à jour `k` à la volée**
Si l'intervieweur veut une version dynamique où `k` change par requête, vous auriez besoin d'une BST équilibrée ou d'un tour à deux fois – une discussion toute différente.

4. ** Variante d'économie d'espace* *
Au lieu d'un tas, vous pouvez garder un multiset trié des meilleures valeurs `k` (`std::multiset` dans C++ ou `SortedList` dans Python).
La complexité temporelle reste `O(n log k)`, mais les constantes sont un peu plus grandes.

---

4.5 Récapitulation de la complexité

Langue
- C'est quoi ?
Java (n log n) (n log n) Autres
Python "O(n log n)" "O(k)" Autres
"O(n log n)" "O(k)" Autres

Avec `n ≤ 100 000`, chaque solution fonctionne bien sous une seconde sur le matériel typique.

---

4.6 Réflexions finales

LeetCode 3478 est une excellente illustration de la façon dont ** trier + une file d'attente prioritaire** transforme un problème de k=" apparemment coûteux en une solution propre et linéaire.
En manipulant soigneusement les duplicatas, nous évitons l'écueil le plus commun et conservons la relation stricte de -<-.

N'hésitez pas à copier les extraits de code dans votre IDE local, à lancer les cas de test et à pratiquer l'ajustement de l'algorithme pour les variations (p. ex., pick the best k *gross*. Bon codage !