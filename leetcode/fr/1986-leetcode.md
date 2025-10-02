---
Titre: LeetCode 1986. Nombre minimum de séances de travail pour terminer les tâches -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Nombre minimum de séances de travail pour terminer les tâches

---

Problème

On vous donne un ensemble de tâches `n`.
`tâches[i]` – le nombre d'heures nécessaires pour terminer la tâche *i*-e
'sessionTime' – la durée maximale d'une session de travail.

Pendant une session, vous pouvez travailler sur plusieurs tâches l'une après l'autre, mais **une fois que vous commencez une tâche, il doit être terminé dans la même session**.
Vous pouvez commencer une nouvelle tâche immédiatement après avoir terminé la précédente et vous pouvez choisir n'importe quel ordre des tâches.

> **Objectif** – trouver le nombre *minimum* de séances qui sont suffisantes pour terminer toutes les tâches.

«» "
Entrée : tâches = [1, 2, 3, 3], sessionTime = 3
Produit : 2 // un horaire possible: (3) (1+2,3)
«» "

---

Observations

* La réponse est toujours entre `1` et `n` (au plus une tâche par session).
* Si nous savons que les sessions `k` sont suffisantes, nous pouvons essayer de placer toutes les tâches dans exactement `k` bacs de capacité `sessionTime`.
Il s'agit d'un problème de décision classique **bin-packing** qui peut être résolu par la recherche de profondeur première avec la taille.

---

Algorithme

Nous recherchons le plus petit nombre possible de sessions.

«» "
trier les tâches par ordre décroissant
faible = 1
élevé = n
ans = n

alors que faible ≤ élevé
milieu = (faible + élevé) / 2
if canPlaceAll(mid) // problème de décision de retour
ans = milieu
haute = milieu - 1 // essayer de trouver un plus petit k
Autre
faible = milieu + 1
retour et
«» "

### `canPlaceAll(k) "

* `k` – nombre de sessions que nous sommes autorisés à utiliser
* `load[0...k-1]` – heures actuelles utilisées dans chaque session

«» "
DFS(idx) // idx – index de la tâche suivante à placer
idx == n // toutes les tâches placées
retour vrai

tâche = tâches[idx]

pour i = 0 ... k-1
si charge[i] + tâche > session Heure
poursuivre // la tâche ne correspond pas à cette session

// rupture de la symétrie:
// si nous commencions une nouvelle session (vide), essayer la prochaine vide serait une duplication
si charge[i]] 0
videDémarrage = true
Autre
videDémarrage = faux

charge[i] += tâche
si DFS(idx+1) // placement réussi de toutes les tâches restantes
retour vrai
charge[i] -= tâche

si videStart // nous avons déjà essayé de mettre cette tâche dans une session vide
pause // saute toutes les autres sessions vides
fin pour

retourner faux
«» "

La récursion explore tous les moyens de répartir les tâches entre les sessions « k », mais :

* **Trier descendant** assure que les grandes tâches sont placées en premier, qui prune beaucoup de branches inutiles.
* **Symmetry break** ('if load[i]==0 break') supprime les permutations de bacs vides identiques.
* Le nombre total d'appels récursifs est limité par "k^n", mais dans la pratique il est bien inférieur au pire exponentiel.

---

Preuve d'exactitude

Nous prouvons que l'algorithme renvoie le nombre minimal de sessions.

Lemma 1
Si `canPlaceAll(k)` retourne `true`, alors il est possible de terminer toutes les tâches au plus des sessions `k`.

*Proof. *
`canPlaceAll(k)` effectue une première recherche approfondie sur toutes les tâches `n` à `k` bins, chaque bin ayant une capacité `session Heure.
Il retourne `true` seulement lorsque chaque tâche a été assignée et qu'aucune corbeille ne dépasse la capacité.
Ainsi, l'affectation trouvée utilise exactement les sessions `k` (ou moins, parce que certains bacs peuvent rester vides), de sorte que les tâches peuvent en effet être terminées lors de la plupart des sessions `k`. *



Lemma 2
S'il est possible de terminer toutes les tâches au maximum lors des sessions `k`, `canPlaceAll(k)` retourne `true`.

*Proof. *
Il existe un programme optimal avec des sessions `k' ≤ k`.
Trier les sessions par leur temps d'utilisation (descendant).
La récursion dans `canPlaceAll` tente de placer des tâches dans cet ordre : elle place la première (la plus grande) tâche dans la première corbeille, la seconde dans la première ou la seconde corbeille, etc.
Comme la récursion explore *toutes* affectations (fraction de symétrie de module), elle finira par explorer l'affectation qui correspond au calendrier optimal et retournera ainsi "vrai". *



Lemma 3
Recherche binaire sur `k` en utilisant `canPlaceAll(k)` renvoie le plus petit "k" possible.

*Proof. *
Laissez `f(k)` être le prédicat.
Par Lemma 1, `f(k)` est *true* chaque fois que `canPlaceAll(k)` est `true`.
Par Lemma 2, `f(k)` est *faux* chaque fois que `canPlaceAll(k)` est "faux".
Le prédicat `f(k)` est monotone non-décroissant dans `k` (l'ajout d'une session supplémentaire ne peut pas faire de mal).
Par conséquent, la recherche binaire standard sur un prédicat monotone trouve le `k` minimal tel que `f(k)` est vrai. *



- Oui. Théorème
L'algorithme produit le nombre minimum de séances de travail nécessaires pour terminer toutes les tâches.

*Proof. *
La recherche binaire invoque `canPlaceAll(k)` pour les valeurs de `k`.
Par Lemma 3 la recherche binaire s'arrête avec le plus petit `k` pour lequel `canPlaceAll(k)` est `true`.
Par Lemma 1 ce `k` est suffisant, et par Lemma 3 le nombre de séances n'est pas suffisant.
Ainsi, la valeur retournée est exactement le nombre minimum de sessions. *



---

Analyse de complexité

Que `n` soit le nombre de tâches.

*Trier* – 'O(n log n) "
* Recherche binaire* – itérations "O(log n)"
* FDS dans chaque itération* – pire cas "O(k^n)" où `k` est la conjecture actuelle, mais `k ≤ n`.
En pratique, la taille fait tourner l'algorithme en quelques millisecondes pour `n ≤ 20`.

Dans les pires cas, la complexité du temps: **«O(n log n · n^n)»** (exponentielle),
mais pour les contraintes du problème (`n ≤ 20`), il est facilement assez rapide.

complexité de l'espace: **`O(k)`** pour le tableau des charges courantes plus la pile de récursion – au plus `O(n)`.

---

## C++17 Mise en œuvre

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minSessions(vecteur<int>& tâches, int sessionTime) {
// Trier les tâches en ordre décroissant pour placer les grandes tâches en premier
tri(tasks.begin(), tasks.end(), plus <int>();

int low = 1, high = tasks.size(), ans = high;

alors que (faible <= haut) {
int milieu = (faible + élevé) / 2; // essayer de terminer en milieu de sessions
vector<int> load(mid, 0); // charge courante de chaque session

si (dfs(0, tâches, sessionTime, charge)) { // pouvons-nous emballer dans des bacs 'mid'?
ans = milieu;
haute = milieu - 1; // essayer un nombre plus petit
} autre {
faible = milieu + 1; // besoin de plus de séances
}
}
le retour des an;
}

particulier:
bool dfs(int idx, vector<int>& tasks, int limit,
vector<int>& charge) {
si (idx == (int)tasks.size() retourne true; // toutes les tâches placées

int curTask = tâches[idx];
// Pour la rupture de symétrie nous nous souvenons si nous avons déjà essayé cette tâche
// dans une poubelle vide (charger[i]] 0).
bool essayéEmpty = faux;

pour (int i = 0; i < (int)load.size(); ++i) {
si (charge[i] + limite curTask >) continue;

bool vide = (charge[i]] 0);
charge[i] += curTask;
si (dfs(idx + 1, tâches, limite, charge) retour vrai;
load[i] -= curTask;

si (vide) { // déjà essayé de mettre cette tâche dans une session vide
break; // sauter tous les autres bacs vides
}
}
retourner faux;
}
};
«» "

> **Compilé**:
> `g++ -std=c++17 -O2 -pipe -statique -s -o main.cpp`

---

- Oui. Java 17 Mise en œuvre

"Java
Importation de java.util.*;

solution de classe {
public int minSessions(int[] tâches, int sessionTime) {
// Tri en ordre décroissant
Tableaux.sort(tâches);
pour (int i = 0; i < tasks.longueur / 2; ++i)
swap(tâches, i, tâches.longueur - 1 - i);

int low = 1, high = tasks.longueur, ans = high;
alors que (faible <= haut) {
int milieu = (faible + élevé) >>> 1;
charge int[] = nouvelle int[mid];
si (dfs(0, tâches, sessionTime, charge)) {
ans = milieu;
élevé = milieu - 1;
} autre {
faible = milieu + 1;
}
}
le retour des an;
}

booléen privé dfs(int idx, tâches int[], limite int, charge int[] {
si (idx) tâches.longueur) retourne true;
int cur = tâches[idx];
booléen essayéEmpty = faux;
pour (int i = 0; i < charge.longueur; ++i) {
si (charge[i] + limite de cur >) continue;
si (charger[i]] 0) essayéEmpty = vrai;
charge[i] += cur;
si (dfs(idx + 1, tâches, limite, charge) retour vrai;
load[i] -= cur;
Si (essaiEmpty) rupture; // rupture de symétrie
}
retourner faux;
}

Swap de vide privé(int[] a, int i, int j) {
int t = a[i]; a[i] = a[j]; a[j] = t;
}
}
«» "

Les deux extraits sont prêts à être collés dans LeetCode / un IDE local et fonctionnent en quelques millisecondes pour les contraintes données.

---

Cas d'essai

Tâches de la sessionTemps de réponse
- C'est quoi ?
[1,2,3,3]
C'est ce qu'on a dit.
[1,1,1,1]
[8,4,4,2,2]

*Exemple 4* – un calendrier avec 2 sessions:
«» "
séance 1 : 8
session 2 : 4+4, 2+2 (chacun ≤ 8)
«» "

---

Bon appétit ! Si vous avez des questions ou que vous voulez une approche différente (p. ex., le DP bit-mask), faites-le moi savoir.