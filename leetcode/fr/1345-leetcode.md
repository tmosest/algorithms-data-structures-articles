---
titre: LeetCode 1345. Jeu de saut IV -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Sauter le jeu IV – Problème et problème

- Oui.
-- -- -- -- -- --
Vous êtes debout au premier index d'un tableau entier `arr`. Dans un mouvement, vous pouvez sauter à `i+1`, `i-1`, ou tout indice `j` tel que `arr[i] == arr[j]`. Trouvez le nombre minimum de mouvements requis pour atteindre le dernier indice. Autres
**Constraints** Autres
Autres Le problème est un problème de trajectoire la plus courte sur un graphique implicite – chaque position de tableau est un nœud, et les bords existent entre les indices consécutifs et entre les indices à valeur égale. Une recherche étendue (BFS) garantit le nombre minimal d'étapes. Autres
**Bon** • BFS visite chaque nœud exactement une fois. <br>• O(n) time & O(n) extra espace – optimal pour les contraintes données. <br>• Simple à raisonner et facile à implémenter. Autres
**Bad**. • L'implémentation naïve qui continue de visiter les mêmes indices de valeur égale au-delà conduit à O(n2) ou pire. <br>• Certaines personnes oublient de marquer la liste des valeurs comme « traitées » après la première visite, causant une erreur de dépassement de délai. Autres
L'utilisation d'un `HashSet` de `int[]` comme clés, ou la conversion du tableau en une chaîne pour le hachage – les deux sont inutiles et lents. <br>• Le recours à la récursion ou au DFS peut causer un débordement de la pile pour de grandes entrées. Autres

---

- Oui. 2. Solutions

Ci-dessous sont des implémentations épurées et entièrement commentées dans **Java, Python et C++**.
Tous les trois partagent la même stratégie :

1. Construire une `Carte<valeur, Liste<indices>>`.
2. Utilisez une file d'attente pour BFS; stockez l'index actuel et le nombre de mouvements effectués.
3. Lors de la visite d'un nœud, demandez ses indices «i+1», «i‐1» et tous les indices de valeur égale.
4. Immédiatement **clair** la liste pour cette valeur – cela garantit que chaque liste est traitée au plus une fois.

### 2.1 Java – `Solution.java "

"Java
Importation de java.util.*;

***
* 1345. Jeu de saut IV
* BFS – temps O(n), espace O(n)
*/
solution de classe {
public int minJumps(int[] arr) {
int n = longueur de l'arrond;
si (n == 1) retourner 0; // déjà au dernier index

// 1. Construire la carte de la valeur à tous les indices ayant cette valeur
Carte<entier, liste<entier>> valeurIndices = nouvelle HashMap<>();
pour (int i = 0; i < n; i++) {
valueIndices.computeIfAbsent(arr[i], k -> new ArrayList<>()).add(i);
}

// 2. Structures du BFS
booléen[] visité = nouveau booléen[n];
visité[0] = vrai;
Queue<integer> q = nouveau ArrayDeque<>();
q.offre(0); // début de l'index 0

mouvement int = 0;
alors que (!q.isEmpty()) {
niveau intTaille = q.size(); // noeuds à la distance actuelle
pour (int s = 0; s < levelSize; s++) {
Int idx = q.poll();

// Vérifier les trois destinations possibles
// a) i+1
si (idx + 1 == n - 1) se déplace de retour + 1;
si (idx + 1 < n & & !visité[idx + 1]) {
visité[idx + 1] = vrai;
q.offre(idx + 1);
}

// b) i-1
si (idx - 1 == n - 1) se déplace de retour + 1;
Si (idx - 1 >= 0 && !visité[idx - 1]) {
visité[idx - 1] = vrai;
q.offre(idx - 1);
}

// c) Tous les indices j où arr[idx] == arr[j]
Liste <Intégrer> mêmeValIdx = valeurIndices.get(arr[idx]);
pour (int j : memeValIdx) {
si (j == n - 1) retourne les mouvements + 1;
si (!visité[j]) {
visité[j] = vrai;
q.offre(j);
}
}
// Important : effacer la liste pour éviter de revoir ces bords
mêmeValIdx.clear();
}
moves++; // niveau actuel de traitement fini
}

retour -1; // ne devrait jamais se produire pour une entrée valide
}
}
«» "

---

2.2 Python – `solution.py "

'`python
de collections import defaultdict, deque
de taper l'importation Liste

Solution de classe:
def minJumps(self, arr: List[int]) -> Int:
n = len(arr)
si n] 1 :
retour 0

# Construire la valeur → cartographie des indices
val_to_idx = defaultdict(list)
pour i, v in énumérate(arr):
val_to_idx[v].append(i)

visité = [Faux] * n
visité[0] = Vrai
q = deque([0]) # La file d'attente BFS détient des indices

mouvement = 0
alors que q:
pour _ dans la plage(len(q)):
idx = q.popleft()

Aller à idx+1
Si idx + 1 == n - 1:
mouvement de retour + 1
si idx + 1 < n et non visité[idx + 1]:
visité[idx + 1] = Vrai
q.annexe(idx + 1)

Aller à idx-1
Si idx - 1 == n - 1:
mouvement de retour + 1
si idx - 1 >= 0 et non visité[idx - 1]:
visité[idx - 1] = Vrai
q. appendice(idx - 1)

# Aller à tous les indices de valeur égale
pour j dans val_to_idx[arr[idx]]:
Si j == n - 1:
mouvement de retour + 1
si elle n'est pas visitée[j]:
visité[j] = Vrai
q.annexe j)

# Important : ne revisite plus jamais cette valeur
val_to_idx[arr[idx]].clear()

mouvements += 1

retour -1
«» "

---

### 2.3 C++ – `Solution.cpp "

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

/*
* 1345. Jeu de saut IV
* BFS – temps O(n), espace O(n)
*/
solution de classe {
public:
La Commission a adopté une proposition de directive relative à la protection des données à caractère personnel.
int n = arr.size();
si (n) 1) retourner 0;

// 1. Carte de la valeur à la liste des indices
non ordonné_map<int, vector<int>> mp;
pour (int i = 0; i < n; ++i)
[arr[i]].push_back(i);

vecteur<bool> visité(n, false);
file d'attente <int> q;
q.push(0);
visité[0] = vrai;

mouvement int = 0;
pendant que (!q.vide()) {
int sz = q.size();
pour (int _ = 0; _ < sz; ++_) {
ixx = q.front(); q.pop();

// idx+1
si (idx + 1 == n - 1) se déplace de retour + 1;
si (idx + 1 < n & & !visité[idx + 1]) {
visité[idx + 1] = vrai;
q.push(idx + 1);
}

// idx-1
si (idx - 1 == n - 1) se déplace de retour + 1;
Si (idx - 1 >= 0 && !visité[idx - 1]) {
visité[idx - 1] = vrai;
q.push(idx - 1);
}

// Tous les indices de valeur égale
auto &vec = mp[arr[idx]];
pour (int j: vec) {
si (j == n - 1) retourne les mouvements + 1;
si (!visité[j]) {
visité[j] = vrai;
q.push(j);
}
}
vec.clear(); // traité une fois
}
+ mouvements;
}
retour -1; // inaccessible – jamais déclenché pour une entrée valide
}
};
«» "

---

- Oui. 3. Article de blog – Jeu de jeu IV: Mastering BFS pour LeetCode Interviews

> **Titre**:
> **Jump Jeu IV – Leetcode 1345**: Solution BFS pour Java / Python / C++

> **Description détaillée**:
> Découvrez la solution BFS la plus rapide pour LeetCodes *Jump Game IV*. Apprenez les implémentations Java, Python et C++, les astuces d'optimisation et les idées prêtes à l'entretien.

---

3.1 Introduction

Si vous vous préparez à une interview technique ou à s'attaquer au LeetCodes (Jump Game IV) (problème #1345), vous vous rendrez rapidement compte que l'approche naïve à chaque valeur égale souffle dans le temps. Le secret est de traiter le tableau comme un graphique et d'utiliser **Breadth‐First Search (BFS)** pour trouver le chemin le plus court. Dans cet article, nous traversons l'algorithme, illustrons pourquoi il fonctionne, et fournissons un code propre dans **Java, Python et C++**.

> **Mots clés**: `Jump Game IV`, `Leetcode 1345`, `BFS`, `minimum sumps`, `array sumps`, `Java solution`, `Python solution`, `C++ solution`, `concurrential programming`, `interview coding`.

---

### 3.2 Énoncé du problème (réécrit pour Clarity)

On vous donne un tableau unidimensionnel des entiers `arr`.
Vous commencez à l'index `0` et souhaitez atteindre le dernier indice (`arr.leng-1`).
Dans **une étape** vous pouvez:

1. Aller à `i + 1` (s'il existe).
2. Passer à "i - 1" (s ' il existe).
3. Sauter à n'importe quel index `j` tel que `arr[i] == arr[j]`.

Retournez le nombre minimum d'étapes** requis pour atteindre le dernier indice.
Si la longueur du tableau est `1`, la réponse est `0` (vous êtes déjà là).

---

### 3.3 Exemple

Indices égaux Notes
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
[100, -23, -23, 404, 100, 23, 23] – – – – 1 – 4 – Sautez de 0 → 4 en une seule étape (même valeur). Autres
À partir de 4, vous pouvez aller à 5 ou n'importe quel indice avec la valeur 100.

Le chemin optimal pour ce tableau est : `0 → 4 → 5 → 6 → 7` → **4 étapes**.

---

3.4 Conception de l'algorithme

1. **Modèle de diagramme* *
- Nœuds: indices de tableau "0 ... n-1".
- Bords :
* `i ш i+1` (si les limites intérieures).
Chaque fois qu ' il s ' agit d ' arr[i] == arr[j]».

Ce graphique est **non pondéré**, donc BFS donne la longueur de chemin la plus courte.

2. **Prétraitement**
Construire une carte de hachage: `value → liste de tous les indices ayant cette valeur`.
Complexité: "O(n)".

3. ** Exécution du BFS**
* Gardez une `queue<int>` (ou `deque` dans Python/C++).
* Gardez un tableau `visited[n]` pour éviter de revisiter les nœuds.
* Pour chaque indice popped `i`, demandez :
* `i-1` (si valide et non visité).
* `i+1` (si valide et non visité).
* Chaque indice `j` dans `valueIndices[arr[i]]` (sauf `i`).
* **Clear** `valueIndices[arr[i]]` après la première visite – cela garantit que chaque liste de bord de valeur égale est traitée une fois.

4. **Compte de niveau**
Suivre le nombre de niveaux que nous avons élargis (`mouvements`).
Lorsque nous enquêtons sur une destination qui est le dernier indice, retourner `moves+1`.

4. **Termination**
Puisque tous les bords sont traités, l'algorithme se termine toujours par une réponse.

---

#### 3.5 Pourquoi la clarté après la première visite est critique

Sans effacer la liste des indices égaux, chaque nœud tenterait de sauter à **all** nœuds égaux à chaque visite, conduisant à un "O(n^2)".
En éliminant après la première fois que nous traversons une valeur particulière, nous réduisons le nombre de bords que nous explorons à ** au plus `n`**.
C'est l'optimisation principale qui transforme une solution de force brute en un algorithme rapide « O(n) ».

---

3.6 Analyse de la complexité

Étape
C'est quoi ?
Carte du hash du bâtiment Autres
Chaque noeud visité une fois, chaque bord examiné au plus une fois → `O(n)` Autres
Total **'O(n)' temps** et **'O(n)' espace**

Cela répond aux exigences relatives aux contraintes liées aux entrevues.

---

3.7 Faits saillants de la mise en oeuvre

C'est vrai. Java
- Utilise `ArrayDeque` (plus rapide que `LinkedList` pour la file d'attente).
- `ArrayList` pour la cartographie; `clear()` est appelé pour éviter le re-traitement.

Python
- `defaultdict(list)` stocke des indices.
- "deque" pour les opérations pop/append.
- Nettoyage de la liste par `clear()`.

C++
- `unordered_map<int, vector<int>>` donne une recherche moyenne de cas O(1).
- "vecteur " pour les drapeaux visités.
- `queue<int>` (ou `std::deque` si vous préférez) pour BFS.

---

3.8 Pièges et correctifs communs

Piège
- Oui.
Après avoir visité l'index `i`, appelez `mp[arr[i]].clear()` ou `val_to_idx[arr[i]].clear()`. Autres
**Vérifications de limites manquantes** 0` et `i+1 < n` avant de pousser. Autres
**Ne pas utiliser le tableau visité**= Utiliser un tableau booléen pour sauter les nœuds déjà traités; sinon vous obtiendrez des boucles infinies. Autres
**Returning before level incréments**.Dans BFS, retournez `moves+1` *after* en traitant le niveau, pas immédiatement après avoir sauté, sauf si vous avez trouvé la cible. Autres

---

3.9 A emporter pour les entrevues

* Traitez les tableaux comme des graphiques.
* Problèmes de chemin le plus court non pondéré → BFS.
* Préprocéder à l'effondrement de multiples bords (clair après la première visite).
* Maintenir les drapeaux visités pour éviter une nouvelle exploration.
* Gardez le compteur de niveau pour calculer la distance.

La maîtrise de ce modèle vous aidera à résoudre d'autres problèmes de LeetCode comme le jeu de jump (problèmes 55, 1302) et les puzzles basés sur des graphiques.

---

3.10 Réflexions finales

La solution BFS de *Jump Game IV* est élégante et fonctionne dans un temps linéaire, ce qui la rend à la fois efficace et facile à expliquer lors d'un entretien technique. Que vous soyez en codage en Java, Python ou C++, l'idée clé reste : **processus des bords à valeur égale seulement une fois**.
N'hésitez pas à copier les extraits de code ci-dessus dans votre éditeur local, à exécuter des tests et à modifier au besoin. Bonne chance pour couper vos scores LeetCode !

---

3.11 Lecture supplémentaire

- [LeetCode 1345 – Jeu de saut IV sur Discuter] (https://leetcode.com/problèmes/jump-game-iv/)
- [Comprendre le BFS en profondeur – Série YouTube par le train de codage]
- [théorie de la programmation – Livre de Mark Allen Weiss]

---

3.12 Fin de l'article

---

> **Fin du blog**
> (Vous pouvez partager vos propres solutions, ajouter des commentaires ou poser des questions. Bon codage !)

---

**C'est là que vous l'avez**: un parcours complet, prêt à l'entrevue et code pour LeetCodes *Jump Game IV*. La stratégie BFS non seulement assure une performance optimale, mais elle démontre également un modèle puissant applicable à de nombreux autres défis de voie plus courte. Bon codage !