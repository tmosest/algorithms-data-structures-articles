---
titre: LeetCode 3310. Supprimer les méthodes du projet -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3310 – Supprimer les méthodes du projet
**Solution en Java, Python & C++ + SEO-Optimized Blog Post**

---

## TL;DR (Ce que vous apprendrez)

Langage (en anglais) Complexité temporelle Complexité spatiale (en anglais) Idée clé Autres
C'est-à-dire...
**DFS / BFS pour collecter des méthodes *suspicious*, puis un seul scan pour vérifier les appels externes
**Python** **O(n + m)** Autres
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

*`n` = nombre de méthodes, `m` = nombre d ' invocations. *

---

## Rétablissement du problème (facile à lire)

Vous avez des méthodes `n` (`0 ... n‐1`).
`invocations[i] = [a, b]` signifie *méthode `a` méthode des appels `b`*.

Une méthode `k` est **buggy**.
Toutes les méthodes qui sont appelées par `k`, directement ou indirectement, sont *suspicious*.

Vous ne pouvez supprimer le groupe suspect que si **aucune méthode non suspecte n'appelle une méthode à l'intérieur du groupe**.
Si cette règle est violée, vous * devez * garder tout le projet (retourner toutes les méthodes).

Retourner une liste des indices de méthode restants (tout ordre).
Si rien ne peut être supprimé, retourner `0 ... n‐1`.

---

## Intuition – Pourquoi un problème de graphique?

* La liste d'invocation est un graphique ** dirigé**.
* Chaîne d'appel → accessibilité dans le graphique.
* Appel externe → un bord entrant d'un noeud non suspect dans l'ensemble suspect.

Le travail se résume donc à :

1. **Trouver le jeu `S`** de tous les nœuds accessibles depuis `k`.
2. **Vérifier** si un nœud extérieur `S` a un bord dans `S`.
3. Si **non** tel edge → retourner `V \ S`.
Sinon → retourner tous les nœuds.

---

## Démarche détaillée (bon, mauvais et mauvais)

### Bonne – Propre et linéaire

* **DFS / BFS** pour découvrir `S`.
* Une seconde passe sur tous les bords pour voir s'il existe un bord externe.
* Deux boucles → au total **O(n + m)**.
* Aucun risque de débordement de pile récursive dans Java/Python/C++ parce que nous utilisons BFS itérative (`queue`/`deque`).

Mauvais – Mauvais contrôle de la direction de bord

* Certaines implémentations naïfs vérifient pour chaque bord, si `a` S et `b` S', puis *conservez tout le graphique* – c'est le contraire de ce dont nous avons besoin.
* Il s'agit d'un bug ** commun**; vous devez chercher les bords * entrants* **à** l'ensemble suspect, pas les bords sortants de lui.

### # Ugly – Travail redondant

* Exécuter le DFS à partir de *chaque nœud* au lieu de seulement de `k`.
* Construire une matrice d'adjacence (`n × n`) – impossible pour `n = 2·105`.
* La récursion dans les langues avec une petite pile (Python par défaut recursion limit ~1k) s'écrasera sur les chaînes d'appel profondes.

---

Algorithme (étape par étape)

1. **Liste d'adjacence construite** `g[a]` = tous les `b` qui `a` appelle.
2. **Collecter l'ensemble suspect** `S` par BFS à partir de `k`.
3. **Scan tous les bords**:
* si `a` -S` **et** `b` -S` → *bord externe* → avorter → retourner toutes les méthodes.
4. Si aucun bord extérieur → retourner tous `i` de telle sorte que `i S`.

---

Code

> Tous les codes sont **ment commentés** et prêts à être collés dans LeetCode / votre propre IDE.

- Oui. 1. Java

"Java
Importation de java.util.*;

***
* 3310. Supprimer les méthodes du projet
* Solution de style LeetCode (solution de classe publique { ... })
*/
solution de classe publique {
Liste publique<Intégrer> restantMéthods(int n, int k, int[][]invocations) {
// 1. Créer une liste d'adjacence
Liste<Liste<entier>> g = nouvelle liste de distribution<>();
pour (int i = 0; i < n; i++) g.add(new ArrayList<>());
pour (int[] e : invocations) g.get(e[0]).add(e[1]);

// 2. BFS de k pour trouver tous les nœuds suspects
booléen[] suspect = nouveau booléen[n];
Queue<integer> q = nouveau ArrayDeque<>();
q.add(k);
[k] = vrai;

alors que (!q.isEmpty()) {
int u = q.poll();
pour (int v: g.get(u)) {
si (!suspicious[v]) {
suspicion[v] = vrai;
q.add(v);
}
}
}

// 3. Un passage pour chercher des appelants externes
pour (int[] e : invocations) {
int a = e[0], b = e[1];
si (!suspicious[a] && suspicion[b]) {
// Appel externe trouvé → ne peut rien supprimer
Liste<entier> tous = nouvelle liste de répartition<>(n);
pour (int i = 0; i < n; i++) all.add(i);
tous les retours;
}
}

// 4. Retourner le complément de l'ensemble suspect
Liste <entier> restante = nouvelle liste d'array<>();
pour (int i = 0; i < n; i++) {
si (!suspicious[i]) restant.add(i);
}
le retour restant;
}
}
«» "

- Oui. 2. Python 3

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
restant Méthodes(
auto, n: int, k: int, invocations: Liste[Liste[int]]
-> Liste[int]:
1. Construire une liste d'adjacence
g = [[] pour _ dans l ' intervalle n)]
pour a, b en invocations:
Annexe b)

2. BFS pour collecter tous les nœuds accessibles à partir de k
suspect = [Faux] * n
q = deque([k])
[k] = Vrai
alors que q:
u = q.popleft()
pour v en g[u]:
si ce n'est pas suspect[v]:
[v] = Vrai
q.appendice v)

# 3. Scanner tous les bords pour les appelants externes
pour a, b en invocations:
si elle n'est pas suspecte[a] et suspecte[b]:
liste de retour(range(n)) # ne peut pas supprimer

4. Retour des méthodes restantes
retour [i pour i à distance(n) si non suspect[i]]
«» "

- Oui. 3. C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur<int> restantMéthods(int n, int k, vecteur<vector<int>>&invocations) {
// 1. Créer une liste d'adjacence
vecteur<vector<int>> g(n);
pour (auto &e : invocations) g[e[0]].push_back(e[1]);

// 2. BFS de k
vecteur<bool> suspect(n, faux);
file d'attente <int> q;
q.push(k);
[k] = vrai;

pendant que (!q.vide()) {
i) u = q.front();
pour (int v: g[u]) si (!suspicious[v]) {
suspicion[v] = vrai;
q.push(v);
}
}

// 3. Cherchez un appelant externe
pour (auto & e : invocations) {
int a = e[0], b = e[1];
si (!suspicious[a] && suspicion[b]) {
// ne peut pas supprimer
vecteur<int> tous(n);
(all.begin(), all.end(), 0);
tous les retours;
}
}

// 4. Méthodes restantes de retour
vecteur <int> restant;
pour (int i = 0; i < n; ++i)
si (!suspicious[i]) reste.push_back(i);
le retour restant;
}
};
«» "

---

## Pourquoi cette solution est "Job-Ready"

Pourquoi les recruteurs l'aiment
C'est ce qu'on dit.
**Scan linéaire**= Affiche que vous pouvez gérer de grandes données (`n`, `m` jusqu'à 2 × 105). Autres
De nombreux intervieweurs s'interrogent sur l'accessibilité, l'ordre topologique, la détection du cycle. Autres
**Découverte de la mise en jeu suspecte par rapport au contrôle de validité – test facile à effectuer. Autres
Autres **Pas d'astuces de nombres magiques**. Autres
**Efficacité de l'espace** mémoire supplémentaire – bon pour les équipes intégrées / contraintes de ressources. Autres

> Si vous pouvez expliquer *pourquoi* vous choisissez BFS plutôt que DFS pour l'étape d'accessibilité, les recruteurs sauront que vous êtes au courant des compromis entre pile et file d'attente.

---

## SEO-Friendly Meta- Données

- **Titre**: 3310 – Supprimer les méthodes du projet: Solution graphique en Java, Python & C++
- **Mots clés**: LeetCode 3310, Supprimer les méthodes du projet, algorithmes graphiques, DFS, BFS, préparation d'entrevues, solutions d'entrevues de codage, entrevue d'ingénieur logiciel, questions de codage d'entrevues d'emploi.
- **Description**: Découvrez comment résoudre le problème LeetCode 3310 – Supprimer les méthodes du projet – en Java, Python et C++. Lisez notre solution propre, linéaire, avec du code, des explications et des idées prêtes à l'entrevue. (en milliers de dollars)

---

- Oui. Harnais d'essai de l'échantillon (vérification rapide de la santé mentale)

"Java
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
System.out.println(sol.remainingMéthods(4, 1, nouvelle int[][]{{0,1},{1,2},{2,3}}); // [0]
System.out.println(sol.remainingMéthods(3, 1, new int[][]{{0,1},{1,2}}); // [0,1]
}
«» "

'`python
sol = Solution()
print(sol.remainingMéthods(4,1,[[0,1],[1,2],[2,3]) # [0]
print(sol.remainingMéthods(3,1,[[0,1],[1,2]]) # [0,1]
«» "

'`cpp
Solution sol;
auto r = sol.remainingMéthods(4,1,{{0,1},{1,2},{2,3}});
pour (int x: r) cout<<x<<"; // 0
«» "

---

## Pièges communs à éviter

Erreur
- Oui.
En utilisant **DFS à partir de chaque nœud** au lieu de juste à partir de `k`.Construisez l'ensemble accessible une fois – il est O(n + m) pas O(n × m). Autres
Vérifier les bords *en cours* des noeuds suspects au lieu de *en cours* des bords. Autres
Erreurs de profondeur de récursion dans Python / Java. Autres
Retour `S` au lieu du complément.Le problème demande des méthodes *remaining*. Autres

---

## Pensées de clôture

- **Les algorithmes de graphiques** sont le pain-and-butter de la plupart des entrevues de codage.
- Une solution à deux passages propre (accessibilité + validation du bord) démontre **décomposition du problème** et **efficacité algorithmique**.
- Oui. En mettant en œuvre la même logique dans **Java, Python & C++**, vous montrez que vous pouvez traduire des idées de haut niveau à travers les écosystèmes – une compétence très appréciée dans une pile multi-langue.

Bon codage, et bonne chance d'obtenir cette entrevue d'ingénierie logicielle! C'est ce qu'il a dit