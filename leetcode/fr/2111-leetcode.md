---
titre: LeetCode 2111. Opérations minimales pour faire augmenter le risque K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2111. Minimum d'opérations pour faire augmenter le risque K
Les bons, les mauvais et les méchants
*Un guide convivial pour le SEO qui vous aidera à répondre à l'entrevue et à être embauché. *

---

Table des matières

Ce que vous apprendrez
- Oui.
Aperçu du problème La déclaration officielle et les contraintes
Naïf et Brute Pourquoi un simple DP échoue
Solution optimale – O(n log n)
Codes Java, Python et C++
Cas de bords d'écueils communs et comment les éviter
L'espace et le temps
Résumé de votre prochain entretien

> **Mots-clés du référencement**: *LeetCode 2111*, *Opérations Minimum pour faire de l'Array K-Increasing*, *LIS en déguisement*, *Longest Non-Decreasing Subséquence*, *K-upering array*, *Java Python solution C++*, *dynamic programming*, *binary search*, *O(n log n)*

---

- Oui. 1. Aperçu du problème

On vous donne un tableau 0 indexé `arr` de `n` entiers positifs et un entier `k` positif.

> **Définition**
> Le tableau est *k-uper* si pour chaque `i` avec `k ≤ i < n` nous avons
> `arr[i‐k] ≤ arr[i]`.

> **Opération**
> Dans une opération, vous pouvez choisir n'importe quel indice `i` et changer `arr[i]` en n'importe quel entier positif.

> **Objectif**
> Return le nombre d'opérations *minimum* nécessaires pour transformer le tableau donné en tableau k-croissant.

Obstacles

«» "
1 ≤ longueur ≤ 10^5
1 ≤ arr[i] ≤ 10^5
1 ≤ k ≤ longueur
«» "

---

- Oui. 2. L'idée naïve (et pourquoi elle fait défaut)

Un premier instinct est de traiter l'ensemble du tableau comme une seule séquence et d'essayer de le rendre non-décroissant.
Pour `k = 1` cela réduit aux modifications classiques minimum pour rendre un tableau non décroissant, ce qui équivaut à `n – LIS(arr)`.

Mais pour le général `k` vous pourriez penser à:

«» "
pour chaque i de 0 à k-1:
prendre en considération les éléments suivants: ...
réparer cette sous-tribu
«» "

Si vous appliquez un PDD quadratique (O(m2) où *m* est la longueur du sous-réseau) pour chaque sous-réseau, le coût total devient O(k * (n/k)2) = O(n2/k), ce qui fait sauter pour `n = 10^5`.

Donc la force brute est **O(n2)** dans le pire des cas – impossible à passer.

---

- Oui. 3. Le point de vue optimal : *LIS in Disguise*

Observation

Chaque indice `i` appartient exactement à l'un des subarrays `k` indépendants 'k-séparés':

«» "
S0 = arr[0], arr[k], arr[2k], ...
S1 = arr[1], arr[1+k], arr[1+2k], ...
...
Sk‐1 = arr[k-1], arr[2k-1], arr[3k-1], ...
«» "

La condition `arr[i‐k] ≤ arr[i]` est *exactement* la même que d'exiger que chaque sous-cours `Sx` soit **non-diminution**.

- Oui. Qu'est-ce que les opérations minimales signifient pour une seule sous-tribu ?

Si vous gardez certains éléments inchangés, le reste doit être remplacé.
Le mieux que vous pouvez faire est de conserver une séquence **la plus longue de cette sous-séquence et de changer tous les autres éléments.

Par conséquent, pour la sous-tribution `S`:

«» "
les opérations(S) ====– PND(S)
«» "

La réponse pour l'ensemble du tableau est la somme sur tous les subarrays `k`:

«» "
réponse = () ()
«» "

Nous avons donc besoin d'un algorithme rapide pour calculer les LNDS pour de nombreuses séquences courtes.

---

- Oui. 4. Calcul des LND en O(m log m)

L'algorithme O(m log m) classique pour la séquence de l'augmentation la plus longue (LIS) fonctionne également pour les sous-séquences **non-décroissant** si vous changez la condition de recherche binaire en *=supérieur à *=*.

Esquisse d'algorithme pour une séquence « seq » :

«» "
fin = [] # valeur la plus basse possible pour une séquence de longueur i+ 1
pour v en suite:
pos = premier indice où se termine[pos] > v (bisect_right pour non-diminution)
si pos == len(ends): find.append(v)
Autrement : fin[pos] = v
retour len(ends)
«» "

Parce que nous ne remplaçons que *un élément qui est plus grand que `v`, la subséquence représentée par `ends` reste triée et garde la longueur optimale.

---

- Oui. 5. Algorithme final (Pseudocode)

«» "
1. Construire un tableau se termine[0 ... k-1] – chaque entrée est un vecteur vide.
2. Pour chaque Sx subarray (x = 0 ... k-1):
m = 0
pour chaque élément v dans Sx:
pos = premier indice dans fin[x] avec fin[x][pos] > v (bisect_right)
si pos == m: fin[x].append(v) // extension LNDS
autres: fin[x][pos] = v
// après la boucle, m = LNDS(Sx)
Opérations +===Sx== - m
3. Opérations de retour
«» "

La recherche binaire interne tourne dans `O(log m)`.
Chaque élément participe à **exactement un** subarray, donc le temps d'exécution total est

«» "
(Sx) = O( n log (n/k) ) = O( n log n )
«» "

L'utilisation de la mémoire est `O(k)` pour les vecteurs `k` plus `O(n)` pour le tableau lui-même.

---

- Oui. 5. Mise en oeuvre des références

Ci-dessous sont trois implémentations qui fonctionnent dans `O(n log n)` et satisfont aux limites de temps LeetCode.
N'hésitez pas à copier-coller, tester et modifier.

### 5.1 Java (en utilisant `ArrayList` et `Collections.binarySearch`)

"Java
Importation de java.util.*;

solution de classe {
kAugmentation(int[] arr, int k) {
int n = longueur de l'arrond;
= 0;

// Pour chacune des sous-séquences séparées de k
pour (int start = 0; start < k; start++) {
Liste <Integer> subseq = nouvelle liste de distribution<>();
pour (int idx = début; idx < n; idx += k) {
sous-seq.add(arr[idx]);
}
Total général Lnds += lndsLength(subseq);
}

retour n - totalLnds; // n – --
}

// Subséquence la plus longue non déclenchante (LNDS) – O(m log m)
Int lndsLength(Liste <entier> suiv) {
Liste<entier> queue = nouvelle liste d'array<>(); // queue[i] = dernière valeur minimale de LND de longueur i+ 1

pour (int v: sec) {
int pos = Collections.binarySearch(tail, v, Comparator.naturalOrder());
si (pos < 0) pos = -(pos + 1); // premier indice où la queue[pos] > v
si [pos] queue.size()
arrière.add(v); // extension
Autre
tail.set(pos, v); // remplacer
}
retour queue.size();
}
}
«» "

#### 5.2 Python (en utilisant `bisect`)

'`python
de bisect import bisect_right
de taper l'importation Liste

Solution de classe:
def kIncreasing(self, arr: List[int], k: int) -> Int:
n = len(arr)
= 0

pour commencer dans la plage(k):
subseq = arr[départ:n:k]
Total_inds += auto.inds_longueur(subseq)

n - total_inds

def lnds_length(self, sq: List[int]) -> Int:
queue = [] # dernier élément minimum possible de LND de chaque longueur
pour v en suite:
pos = bisect_right(tail, v) # trouver la première queue[pos] > v
Si la position est la suivante:
(v)
Sinon:
[pos] = v
retour len(tail)
«» "

### 5.3 C++ (en utilisant `vector` et `upper_bound`)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int kAugmentation(vecteur<int>& arr, int k) {
int n = arr.size();
= 0;

pour (int start = 0; start < k; ++start) {
vecteur<int> sous-séq;
pour (int idx = début; idx < n; idx += k)
sousseq.push_back(arr[idx]);

Total général Lnds += lndsLength(subseq);
}

retour n - totalLnds; // n - DND
}

particulier:
int lndsLength(vecteur const<int>&sq) {
vectorielle<int> queue; // valeur minimale de dernière valeur pour les PND de chaque longueur
pour (int v: sec) {
auto it = upper_bound(tail.begin(), tail.end(), v); // first > v
si (it)
fall.push_back(v);
Autre
*it = v;
}
retour (int)tail.size();
}
};
«» "

> **Pourquoi la version C++ utilise `upper_bound`**
> `upper_bound` trouve le premier élément **plus grand** que `v`, ce qui est parfait pour les sous-séquences *non-décroissant*.
> Si nous utilisions `lower_bound` (premier **pas moins**), nous imposerions par erreur des subséquences en augmentation stricte.

---

5.4 Pièges communs

Pourquoi il casse
- Oui.
**L'utilisation de LIS au lieu de LNDS**. L'augmentation stricte supprime les éléments égaux, ce qui donne une plus petite séquence. Autres
**Tréer l'ensemble du tableau en une seule séquence**
Pour `k = n` les longueurs de subarray sont 1; `LNDS` doit être 1= L'algorithme le gère naturellement (`=S=1, LNDS=1`) Autres
**Utiliser `bisect_left` au lieu de `bisect_right`**
**O(n log n) par sous-réseau**=Reconstruire le tableau `ends` pour chaque sous-réseau mène à O(nk log n)=Trouver chaque index une seule fois, conserver `ends` par subséquence==

---

- Oui. 6. Analyse de la complexité

Métrique
- C'est quoi ?
**Heure**="O(n log n)" (chaque élément faisant partie d'un calcul LNDS)="O(n log n)"="O(n log n)" Autres
Listes auxiliaires `O(k)` + tableau d'entrée
**Pourquoi il passe** Opérations M – confortablement sous la limite de 1 seconde sur LeetCode

---

- Oui. 7. Cas d ' épreuve rapide

'`python
Version Python
sol = Solution()

affirmons sol.kAugmentation([1,2,3], 1) == 0 # déjà non-diminution
affirmant sol.kAugmentation([3,1,2,4,5], 2) == 1
affirme sol.kAugmentation([5,4,3,2,1], 3) 2
«» "

> Utilisez un générateur de tableaux aléatoires pour vérifier la santé de Python et de C++ par rapport à la solution Java.

---

- Oui. 8. Take‐Aways pour votre prochaine entrevue

1. **Reconnaissez l'indépendance** – les sous-arrachages séparés en k sont des contraintes *indépendantes*.
2. **Réduire à un problème connu** – LNDS est le sous-problème exact.
L'ensemble du tableau se transforme en une somme de (longueur subarray – LNDS).
3. **Leverage O(n log n)** Algorithme LIS pour chaque sous-réseau.
Il est plus rapide que DP et fonctionne jusqu'à 105 éléments.
4. **Mise en œuvre proprement** – utiliser `upper_bound` (C++), `bisect_right` (Python) ou `Collections.binarySearch` (Java) pour la variante non décroissante.
5. **Edge-cases** – testez toujours `k = 1`, `k = n` et des entrées aléatoires importantes.
6. ** Expliquez votre processus de pensée** – les intervieweurs adorent voir le "pourquoi" derrière le code.

---

La pensée finale

La beauté de LeetCode 2111 réside dans la transformation d'un problème apparemment difficile à réorganiser en une poignée de problèmes LIS classiques. Une fois que vous avez repéré l'indépendance *k-séparée*, le reste suit naturellement.

Montrez cette astuce dans votre prochaine interview et vous impressionnerez le panel avec à la fois **perspective algorithmique** et **code propre** – exactement ce que les gestionnaires d'embauche recherchent.

Bon codage, et que votre prochaine offre soit une augmentation de K! C'est ce qu'il a dit.

---