---
titre: LeetCode 1738. Trouver la plus grande valeur de coordonnées XOR -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1738. Trouver la plus grande valeur de coordonnées XOR de Kth
### Les bons, les mauvais et les méchants – Un profond Guide de plongée pour les entrevues
* (implémentations Java, Python & C++ + un article de blog convivial pour le référencement)*

---

### TL;DR
- **Problème**: Pour une matrice donnée `m × n`, calculez le XOR de tous les éléments du sous-matrix `(0,0)` → `(i,j)` pour chaque coordonnées `(i,j)`. Retourner le **k‐th le plus grand** de ces valeurs XOR.
- **Connaissance clé**: Le XOR d'un préfixe peut être calculé en O(1) à l'aide d'un tableau **préfixe-XOR** (similaire aux montants du préfixe 2-D).
- **Deux modèles de solutions populaires**
1. **Min-heap** – O(m n log k) temps, O(k) espace
2. **QuickSelect** – O(m n) temps prévu, O(m n) espace (tableau flatté)
- **Pourquoi c'est important**: LeetCode 1738 est un favori dans le codage des entrevues. La maîtrise montre que vous pouvez combiner DP, structures de données et algorithmes de sélection.

---

Rétablissement du problème

Texte
Entrée : matrice – int[m][n], 1 ≤ m, n ≤ 1000, 0 ≤ matrice[i][j] ≤ 1 000 000
k – 1-indexé, 1 ≤ k ≤ m·n

Sortie : int – la plus grande valeur coordonnée XOR
«» "

> **Définition** –
> `value(i, j) = matrice[0][0] ^ matrice[0][1] ^ ... ^ matrice[i][j]`
> (XOR de tous les éléments du rectangle depuis le coin supérieur gauche jusqu'à `(i, j)`).

---

Plan directeur

Étape Action Pourquoi
C'est quoi ?
**Construire une table préfixe 2-D XOR** `pref` de taille `(m+1) × (n+1)`"" pref[i][j]` détient XOR de sous-matrix `(0,0)` → `(i-1,j-1)`. Répétition :
«pref[i][j] = matrice[i-1][j-1] ^ pref[i-1][j] ^ pref[i][j-1] ^ pref[i-1][j-1]» Autres
Autres 2. **Flatten** toutes les valeurs de préfixe non zéro dans un tableau 1-D `arr`. Autres
**Sélectionnez le k-th le plus grand** soit par:
3a) **Min-heap** (taille k) – garder les valeurs k supérieures. espace supplémentaire
Autres 3b) **QuickSelect** – partition autour d'un pivot jusqu'à ce que le k-th les plus grandes terres. Autres

Les deux approches sont linéaires dans la taille de la matrice après l'étape de préfixe.

---

2. Mise en œuvre du code

Voici des implémentations propres, prêtes à la production dans **Java, Python et C++**.

2.1 Java – Deux approches

"Java
Importer java.util. Priorité Demande;
Importer java.util. Aléatoire;

solution de classe publique {

- Oui. Préfixe XOR + Min-Chap --------- */
LargestValueHeap(int[[]] matrice, int k) {
int m = matrice.longueur, n = matrice[0].longueur;
int[][] pref = nouvelle int[m + 1][n + 1];
Priorité Queue<integer> minHeap = nouvelle prioritéQuue<>(k);

pour (int i = 1; i <= m; i++) {
pour (int j = 1; j <= n; j++) {
pref[i][j] = matrice[i - 1][j - 1]
^ pref[i - 1] [j]
^ pref[i][j - 1]
^ pref[i - 1] [j - 1];
minHeap.offrer(pref[i][j]);
si (minHeap.size() > k) minHeap.poll();
}
}
retour minHeap.peek();
}

- Oui. 2------ */
valeur(int[][] matrice, int k) {
int m = matrice.longueur, n = matrice[0].longueur;
int[][] pref = nouvelle int[m + 1][n + 1];
int[] arr = nouvelle int[m * n];
Int idx = 0;

pour (int i = 1; i <= m; i++) {
pour (int j = 1; j <= n; j++) {
pref[i][j] = matrice[i - 1][j - 1]
^ pref[i - 1] [j]
^ pref[i][j - 1]
^ pref[i - 1] [j - 1];
arr[idx++] = pref[i][j];
}
}

int cible = arr.longueur - k; // kth plus grande = (lent-k)th plus petite
select rapide(arr, 0, arr.longueur - 1, cible);
retour arr[cible];
}

vide privé rapideSelect(int[] a, int gauche, int droite, int k) {
si (gauche >= droite) retour;
int pivot = médianeDeTrois (a, gauche, droite);
int i = gauche, j = droite;
pendant que (i <= j) {
pendant que (a[i] < pivot) i++;
pendant (a[j] > pivot) j--;
si (i <= j) swap(a, i++, j--);
}
si (k <= j) QuickSelect(a, gauche, j, k);
autre rapideSelect(a, i, droite, k);
}

Int médiane privéeDeTrois(int[] a, int l, int r) {
Int m = (l + r) >>> 1;
int aL = a[l], aM = a[m], aR = a[r];
si (aL > aM) { int tmp = aL; aL = aM; aM = tmp; }
si (aM > aR) { int tmp = aM; aM = aR; aR = tmp; }
si (aL > aM) { int tmp = aL; aL = aM; aM = tmp; }
retourner aM;
}

Swap de vide privé(int[] a, int i, int j) {
int tmp = a[i]; a[i] = a[j]; a[j] = tmp;
}
}
«» "

> **Pourquoi deux méthodes? * *
> - `kthLargestValueHeap` est simple, déterministe, et utilise seulement `O(k)` mémoire supplémentaire.
> - `kthLargestValue` est plus rapide en pratique pour le grand `k` parce que QuickSelect a le temps prévu linéaire.

#### 2.2 Python – Min‐Heap + QuickSelect

'`python
importation heapq
importation aléatoire
de taper l'importation Liste

Solution de classe:
C'est... Préfixe XOR + taille minimale - Oui.
def kthLargestValueHeap(self, matrix: List[List[int]], k: int) -> Int:
m, n = len(matrice), len(matrice[0])
pref = [[0]*(n+1) pour _ dans l'intervalle(m+1)]
min_heap = []

pour i dans la plage (1, m+1):
pour j dans la plage(1, n+1):
pref[i][j] = (matrix[i-1][j-1] ^ pref[i-1][j] ^
^ pref[i][j-1] ^ pref[i-1]
heapq.heappush(min_heap, pref[i][j])
si len(min_heap) > k:
heapq.heappop(min_heap)
retour min_heap[0]

C'est... Préfixe XOR + sélection rapide - Oui.
def kthPlus grande Valeur(self, matrix: List[List[int]], k: int) -> Int:
m, n = len(matrice), len(matrice[0])
pref = [[0]*(n+1) pour _ dans l'intervalle(m+1)]
arr = []

pour i dans la plage (1, m+1):
pour j dans la plage(1, n+1):
pref[i][j] = (matrix[i-1][j-1] ^ pref[i-1][j] ^
^ pref[i][j-1] ^ pref[i-1]
Annexe(pref[i][j])

cible = len(arr) - k # kth le plus grand -> (en k)ème plus petit
Self.quick_select(arr, 0, len(arr)-1, cible)
retour arr[cible]

def quick_select(self, a: List[int], gauche: int, droite: int, k: int):
si gauche >= à droite :
retour
pivot = auto.médiane_de_trois(a, gauche, droite)
i, j = gauche, droite
alors que i <= j:
pendant que a[i] < pivot:
i += 1
pendant que a[j] > pivot:
J = 1
i <= j:
a[i], a[j] = a[j], a[i]
i += 1
J = 1
si k <= j:
self.quick_select(a, gauche, j, k)
Sinon:
Self.quick_select(a, i, droite, k)

def médiane_de_trois(self, a, l, r):
m = (l + r) >> 1
trio = trié([a[l], a[m], a[r]])
retour trio[1]
«» "

> **Note** – Les Python's intégrés dans le «heapq» est un **min‐heap**. QuickSelect est implémenté manuellement car Python n'a pas de `nth_element` natif.

#### 2.3 C++ – Min‐Heap & QuickSelect

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
// -------- Préfixe XOR + taille minimale - Oui.
LargestValueHeap(vector<vector<int>>& matrix, int k) {
int m = matrice.size(), n = matrice[0].size();
vecteur<vector<int>> pref(m+1, vector<int>(n+1, 0)
priorité_queue<int, vecteur<int>, plus<int>> minCheap;

pour (int i = 1; i <= m; ++i) {
pour (int j = 1; j <= n; ++j) {
pref[i][j] = matrice[i-1][j-1]
^ pref[i-1][j]
^ pref[i][j-1]
^ pref[i-1][j-1];
minHeap.push(pref[i][j]);
si ((int)minHeap.size() > k) minHeap.pop();
}
}
retour minHeap.top();
}

// -------- Préfixe XOR + sélection rapide - Oui.
LargestValue(vecteur<vecteur<int>>& matrice, int k) {
int m = matrice.size(), n = matrice[0].size();
vecteur<vector<int>> pref(m+1, vector<int>(n+1, 0)
vecteur <int> arr; arr.reserve(m*n);
pour (int i = 1; i <= m; ++i) {
pour (int j = 1; j <= n; ++j) {
pref[i][j] = matrice[i-1][j-1]
^ pref[i-1][j]
^ pref[i][j-1]
^ pref[i-1][j-1];
arr.push_back(pref[i][j]);
}
}
int cible = arr.size() - k; // kth plus grande -> (taille-k)ème plus petite
nth_element(arr.begin(), arr.begin()+cible, arr.end(),
[](int a, int b) { retourner a > b; });
retour arr[cible];
}
};
«» "

> **C++ `nth_element`**
> Les outils "nth_element" de la STL QuickSelect interne et fonctionne dans le temps prévu linéaire.
> Nous lui donnons une comparaison *descendant* (`a > b`) de sorte que le `k‐th` le plus grand finit à l'index `size-k`.

---

## Résumé des performances

L'approche du temps L'espace supplémentaire Notes pratiques
- C'est pas vrai.
Préfixe + Min-heap **O(m n log k)**O(k)=Déterministe, grand pour `k << m·n`.
Préfixe + choix rapide **O(m n)** attendu Plus rapide pour grand `k`; utilise `nth_element` / partition personnalisée. Autres
Préfixe + Tri () **O(m n log (m n))**=O(m n)=En direct mais plus lent; rarement utilisé dans les entrevues. Autres

> ** Consommation spatiale* *
> La table préfixe 2-D consomme des entiers `(m+1) × (n+1)` (~4 Mo pour une matrice 1000×1000).
> L'aplatissement ajoute un autre entier "m" (~4 Mo).
> Dans l'ensemble, < 10 Mo – parfaitement sûr pour la limite de LeetCodes 256 Mo.

---

3. Les bons, les mauvais, les méchants

Catégorie : Quoi ?
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**L'élégance algorithmique**= combine DP + XOR + heap/QuickSelect en un seul passage. Aucun.
Autres **Complexité du temps**= Heap: `O(mn log k)` → bon pour le petit k. Sélection rapide : attendu `O(mn)` → excellent pour grand k. Non, la méthode naïve "O(mn)^2)" est morte. Pour le plus mauvais cas QuickSelect (toujours cueillir le plus mauvais pivot) → `O(mn)^2)`. Migré par pivot aléatoire ou médiane de trois. Autres
Autres **L'utilisation de l'espace**= Min-heap: `O(k)` → très convivial pour la mémoire.== QuickSelect: nécessite un tableau aplati de `mn` ints → mémoire supplémentaire `O(mn)`.== Quand `k` est presque `m·n`, le tas garde toujours toutes les valeurs (k=mn) → le coût de l'espace augmente à `O(mn)`. Autres
**Complexité du codage** C++ `nth_element` est trivial, mais personnaliser le comparateur peut confondre les novices. Autres
**Sécurité de l'appareillage** Le choix rapide doit se garder des sous-cours vides (toujours `pref[i][j]`) Aucune.
**Readability** "heapq" est concis ; QuickSelect peut être un peu verbeux. C++ avec STL `nth_element` est court mais peut masquer la logique de sélection. Autres
**Valeur de l'interview**= Démonstration du PDD (préfixe des sommes) + des structures de données (pail). Affiche que vous pouvez appliquer QuickSelect, un algorithme de sélection classique. Points saillants Utilisation de STL. Autres

---

4. Pourquoi LeetCode 1738 est-il Interview-Gold

1. **Il teste la pensée multidisciplinaire* *
- Programmation dynamique (préfixe XOR)
- Choix de la structure des données (pap vs. tableau)
- Sélection algorithmique (QuickSelect)

2. **Il a une réponse claire – pas de hasard, juste la valeur déterministe k‐th la plus grande.

3. **Il vous oblige à raisonner sur l'espace/temps compromis** – quelque chose que les intervieweurs aiment entendre.

4. **C'est une gemme cachée dans la famille "préfix sum"** – de nombreux candidats oublient la variante XOR.

---

Article de blog amical

> **Titre**: *Trouver la plus grande valeur de coordonnées XOR – LeetCode 1738 (Java, Python, C++)*
> **Méta-Description**: Résoudre le LeetCode 1738 Trouver la plus grande valeur XOR de Kth avec le code Java, Python et C++. Apprenez l'astuce préfixe-XOR, min-heap vs. QuickSelect, et des conseils d'entrevue.

---

Introduction

Dans les interviews de codage, LeetCode 1738 apparaît souvent comme un problème de niveau moyen qui peut être résolu en **O(m n)** temps. Il mélange une table préfixe **dynamique-programmation** avec un algorithme classique **sélection**. La maîtrise de ce problème montre que vous pouvez jongler avec des opérations bitwise, des tableaux bidimensionnels et des structures de données efficaces.

---

Résumé du problème

> Pour une matrice, calculez le XOR bitwise de chaque sous-matrice préfixe et retournez ensuite le **k‐th le plus grand** de ces valeurs XOR.

---

C'est vrai. Insight clé: Préfixe-XOR Tableau

Étape Formule Pourquoi ça marche
C'est pas vrai.
"pref[i][j] = matrice[i‐1][j‐1] ^ pref[i‐1][j] ^ pref[i][j‐1] ^ pref[i‐1][j‐1]" Utilise l'inclusion-exclusion avec XOR (note: XOR est associatif et commutatif). Après avoir rempli la table, `pref[i][j]` tient le XOR du rectangle `(1,1)` → `(i,j)`. Aucune recomputation nécessaire. Autres

Le tableau prend un passage; chaque entrée est calculée en O(1). Donc nous obtenons tous les préfixes XOR dans un seul `O(m n)` scan.

---

Deux solutions rapides

#### A) Préfixe

1. Construire une table de préfixe.
2. Poussez chaque valeur sur un **min-heap** (`PriorityQueue` en Java, `heapq` en Python).
3. Gardez la taille du tas ≤ k; pop quand il dépasse.
4. C'est la réponse.

**Pros**: Déterministe, très efficace dans l'espace («O(k)»).
**Cons**: Un peu plus lent pour le grand `k` en raison du facteur log.

#### B) Préfixe + Sélection rapide / `nth_element "

1. Construire une table préfixe et pousser toutes les valeurs dans un tableau.
2. Calculer "cible = taille - k".
3. Utilisez `nth_element` (C++) ou un QuickSelect personnalisé (Java/Python) pour partitionner le tableau de sorte que le `k‐th` le plus grand se termine à index `target`.
4. Retourne cet élément.

**Pour**: Temps prévu linéaire, parfait pour les grands "k".
**Cons**: Nécessite une partition personnalisée; certains candidats trouvent qu'elle est sujette à erreur.

---

C'est pas vrai. Extraits de code linguistique

- **Java** – "PriorityQueue" + boucles; QuickSelect avec médiane de trois.
- **Python** – `heapq` + boucles; QuickSelect manuel.
- **C++** – STL `nth_element` avec un comparateur descendant.

(Insérer les blocs de code des sections ci-dessus.)

---

C'est vrai. Conseils d'entrevue

- ** Expliquez votre choix**: Si `k` est petit, justifier le tas; si `k` est grand, mentionnez QuickSelect.
- **Parler des propriétés XOR**: Associative, commutative et qui `x ^ x = 0`.
- **Boîtes de bord de mention**: `k=1` et `k=m·n`.
- **Afficher les compromis**: Mémoire contre vitesse.

---

Tableau de complexité

(Inclure le tableau de rendement de plus tôt.)

---

- Oui. Réflexions finales

LeetCode 1738 n'est pas juste un autre problème moyen. C'est un exemple de manuel de la façon de transformer un défi apparemment difficile de la catégorie «k‐th» en une solution **O(m n)**. Que ce soit en Java, Python ou C++, la clé réside dans ce préfixe simple. Formule XOR et choix intelligent de la structure des données.

Bon codage ! C'est ce qu'il a dit.

---

5. Prochaines étapes

- Exécutez les extraits fournis sur LeetCode.
- Cas de bord d'exercice: monoligne, monocolonne, k=1, k=m·n.
- Essayez de *modifier* la solution pour retourner le **k‐th le plus petit** (comparaison inverse).
- Discutez des compromis avec un ami ou un mentor.

---

> **Bonne entrevue‐ Préparation!**
> Rappelez-vous : une explication claire est souvent plus précieuse qu'une solution fantaisiste.

---

* Fin de l'article. *