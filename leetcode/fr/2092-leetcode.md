---
titre: LeetCode 2092. Trouver tous les gens avec secret -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2092 – Trouver toutes les personnes avec secret
### Solution dans **Java**, **Python** et **C++** (Union-Find + Time Battching)
---

### TL;DR
Le secret se répand seulement ** au moment exact d'une réunion**.
Si plusieurs réunions se déroulent en même temps, tous ceux qui ont déjà le secret peuvent instantanément le diffuser à **tous** participants de ce *time-batch*.
Le problème peut être résolu en **O(n + m log m)** temps et **O(n + m)** mémoire par:

1. **Désormais** séances par heure.
2. **Traitement** chaque fois qu'il s'agit d'un ensemble de temps à l'aide d'un ensemble mixte (DSU)** (Union-Find).
3. À la fin, tous les nœuds dont le représentant est `0` (personne 0) connaissent le secret.

Le DSU est réinitialisé après chaque lot de sorte que les personnes qui n'ont pas reçu le secret pendant cette période soient à nouveau isolées.

---

C'est pas vrai. Mise en œuvre Java

"Java
Importation de java.util.*;

solution de classe publique {
// - Oui. Union des ensembles disjoints
classe statique privée DSU {
Int[] parent, grade;
DSU(int n) {
parent = nouveau int[n];
rang = nouvelle int[n];
pour (int i = 0; i < n; i++) parent[i] = i;
}
int find(int x) {
si (parent[x] != x) parent[x] = find(parent[x]);
retour du parent[x];
}
Union nulle(int a, int b) {
int pa = find(a), pb = find(b);
si (pa == pb) retourne;
si (rank[pa] < rank[pb]) parent[pa] = pb;
sinon si (rank[pb] < rank[pa]) parent[pb] = pa;
Autre { parent[pb] = pa; rang[pa]++; }
}
}

liste publique<integer> trouverAllPeople(int n, int[][] réunions, int firstPerson) {
Tri par heure
Arrays.sort(réunions, comparator.comparingInt(a -> a[2]));

DSU dsu = nouveau DSU(n);
dsu.union(0, premierPersonne); // personne 0 donne le secret au moment 0

i = 0, m = longueur des réunions;
pendant que (i < m) {
Int curTime = réunions[i][2];
// garder tous les participants de ce lot de temps
Liste des participants <Integer> = nouvelle liste de distribution<>();

Union tous ceux qui se rencontrent en ce moment
pendant que (i < m && meetings[i][2] == curTime) {
int a = réunions[i][0];
int b = réunions[i][1];
dsu.union(a, b);
participants.add(a);
participants.add(b);
i++;
}

Réinitialisez le DSU pour les personnes qui n'ont PAS obtenu le secret
pour (int p : participants) {
si (dsu.find(p) != dsu.find(0))
dsu.parent[p] = p; // à nouveau isolé
}
}

// 4 Recueillir tous ceux qui sont connectés à 0
Liste <Integer> res = nouvelle liste de distribution<>();
pour (int i1 = 0; i1 < n; i1++)
si (dsu.find(i1) == dsu.find(0)) res.add(i1);

retour rés;
}
}
«» "

**Complexité* *
- "O(n + m) log m)" temps (le tri domine)
- Mémoire "O(n + m)" (DSU + tableau de réunions)

---

Mise en œuvre de Python

'`python
de collections importer par défautdict
importations
sys.setrecursionlimite(1 << 25)

Classe DSU:
def __init_(self, n):
self.par = list(range(n))
autornk = [0] * n

def find(self, x):
si self.par[x] != x:
self.par[x] = self.find(self.par[x])
retour self.par[x]

def union(self, a, b):
p, pb = self.find(a), self.find(b)
pb: retour
si self.rnk[pa] < self.rnk[pb]:
auto.par[pa] = pb
elif self.rnk[pb] < self.rnk[pa]:
self.par[pb] = pa
Sinon:
self.par[pb] = pa
égo.rnk[pa] += 1

def findAllPeople(n: int, meetings: list[list[int]], firstPerson: int) -> list[int]:
meetings.sort(key=lambda x: x[2]) # tri par temps
dsu = DSU(n)
dsu.union(0, firstPerson) # premier transfert secret

i = 0
alors que i < len (réunions):
cur_time = réunions[i [2]
participants = []

# Union toutes les réunions qui se déroulent en même temps
alors que i < len (réunions) et réunions[i][2]]. _temps
a, b, _ = réunions[i]
dsu.union(a, b)
participants.extend([a, b])
i += 1

# Réinitialisez les nœuds qui n'ont pas obtenu le secret pendant ce lot
pour les participants:
si dsu.find(p) != dsu.find(0):
dsu.par[p] = p

retour [i pour i dans range(n) si dsu.find(i) == dsu.find(0)]

♪ ----------------------------------------------------------------------------------
♪ Exemple d'utilisation (sans commentaire pour tester)
N = 6
Nombre de réunions = [[1,2,5],[2,3,8],[1,5,10]]
# print(findAllPeople(n, réunions, 1)) # -> [0, 1, 2, 3, 5]
«» "

**Complexité** – identique à la solution Java.

---

C++ Mise en œuvre

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe DSU {
public:
DSU(int n): parent(n), grade(n, 0) {
(parent.begin(), parent.end(), 0);
}
int find(int x) {
retour parent[x]==x ? x : parent[x]=find(parent[x]);
}
vide unit(int a, int b) {
int pa=find(a), pb=find(b);
if(pa==pb) retourne;
si(rank[pa]<rank[pb]) parent[pa]=pb;
sinon si(rank[pb]<rank[pa]) parent[pb]=pa;
autres { parent[pb]=pa; rang[pa]++; }
}
particulier:
vecteur <int> parent, grade;
};

solution de classe {
public:
vector<int> findAllPeople(int n, vector<vector<int>>& meetings, int firstPerson) {
tri(meetings.begin(), meetings.end(),
[](const auto &a, const auto &b){ retourner a[2] < b[2]; });

DSU dsu(n);
dsu.unite(0, premierPerson); // secret commence à la personne 0

i = 0;
pendant(i < (int)meetings.size()) {
int cur = réunions[i][2];
vector<int> part; // participants dans ce lot de temps

pendant(i < (int)meetings.size() && meetings[i][2] == cur) {
int a = réunions[i][0];
int b = réunions[i][1];
dsu.unite(a, b);
partie.push_back(a);
partie.push_back(b);
++i;
}

for(int p : part) // réinitialisez ceux qui n'ont pas obtenu de secret
if(dsu.find(p) != dsu.find(0))
dsu.unite(p, p); // définir le parent à lui-même
}

vecteur <int> ans;
pour(int j=0;j<n;++j)
if(dsu.find(j) == dsu.find(0))
c. «push_back» (j);
le retour des an;
}
};
«» "

Autres **Astuce**: En C++, vous pouvez sauter l'étape de "reset" en utilisant un *stack* de nœuds qui changent les parents pendant un lot, mais ce qui précède est plus facile à lire.

---

Article du blog – Le secret se répand : une plongée profonde en LeetCode 2092

Titre
**Le secret se répand: 2092 – De BFS à Union‐Find – Le bon, le mauvais, le mauvais* *

Description de la méta
Apprenez à fissurer LeetCode 2092 dans le temps O(n+m log m). Lisez la plongée profonde dans les stratégies de BFS, DSU et de mise à l'épreuve du temps. Parfait pour la préparation des entrevues, les entrevues de codage et les ingénieurs de recherche d'emploi.

---

Introduction

> **Récapitulation des problèmes* *
> On vous donne `n` des gens, une liste de réunions `(x, y, heure)`, et une `première personne`. Personne `0` a un secret à l'époque `0` et le transmet à `firstPerson`. Chaque fois qu'une réunion a lieu, quiconque connaît déjà le secret le partage instantanément avec l'autre participant.
> **Objectif** – rendre tous ceux qui connaissent le secret après toutes les réunions.

> **Pourquoi ça compte** –
> 1. **Concurrence** – plusieurs réunions en même temps.
> 2. **Production de couches** – un problème classique d'accessibilité, mais avec une torsion : la propagation se produit *seulement* à des heures précises.
> 3. **Interview challenge** – exige une réflexion attentive sur *quand* vous pouvez répandre le secret, pas seulement *qui* peut.

---

- Oui. La vue naïve : première recherche (BFS)

Un premier instinct est de traiter chaque rencontre comme un bord dans un graphique et d'exécuter un BFS à partir de la source `(0, firstPerson)`.

Texte
temps 0: 0 -> premier Personne
temps t: BFS de tous ceux qui connaissent le secret à ce moment
«» "

**Problème** – BFS suppose un graphique *statique*. Dans notre problème, les bords ne deviennent pertinents **une fois** à l'heure de la réunion, et ils peuvent être éteints - si le secret n'a jamais atteint ce bord. L'exécution d'un tampon BFS une fois par fois conduirait à un algorithme **O(n ·m)** – beaucoup trop lent pour les contraintes (`m` jusqu'à `2·105`).

---

### Les bons – Union‐Find + Time‐Batching

Tri et lot

Trier toutes les réunions par `temps`. Toutes les réunions qui partagent le même temps forment un *batch*.

##### # 2-

Pendant un lot, si ** n'importe quel** participant connaît le secret, le secret se propage à **chaque** composant connecté de ce lot instantanément.
Union‐Find nous permet de fusionner* tous les participants d'un lot dans un temps presque constant amorti.

- Oui. Réinitialiser après le lot

Après avoir traité le lot, nous ** devons isoler** ceux qui n'ont pas **** obtenir le secret.
En code, ceci ressemble à :

```pseudo
pour chaque participant p de ce lot:
si find(p) != find(0):
parent[p] = p // se réinitialiser
«» "

Cette astuce garantit que la prochaine fois commence à zéro pour tous ceux qui n'ont pas reçu le secret.

---

- Oui. Le mauvais – Pourquoi BFS est une impasse

L'approche de la complexité Pourquoi il fait défaut
- C'est quoi ?
"O(n · m)" "Trop lent quand `m` est énorme. Autres
BFS + Trier () `O(m log m + n)`" Toujours `O(n·m)` parce que nous avons besoin de recalculer l'accessibilité à partir de zéro pour chaque time-stamp. Autres

En bref, BFS ignore la dimension *time* et ne peut donc pas gérer efficacement les réunions simultanées.

---

### Les cas de bord qui brisent le code simple

Problème
C'est pas vrai.
**Rencontres avec la même paire à des moments différents**=Le DSU peut se souvenir incorrectement des unions passées.==Réinitialiser les parents *après* chaque lot. Autres
**Grande taille d'entrée**. Utilisez la compression de chemin et les boucles itératives ou augmentez les limites de récursion. Autres
**Plusieurs visites à la même personne en un seul lot**.L'ajout du même participant deux fois peut gonfler inutilement la liste des participants. Autres

---

Répartition de la complexité

Étape Opération Temps
C'est pas vrai.
Autres Trier les réunions Autres
Opérations du DSU Autres
Réinitialiser les boucles au plus `2 · m` par lot
Analyse finale Autres

> **Résultat** – temps `O(n+m) log m), espace `O(n+m)`.

---

### Conseils à emporter pour les entrevues

1. ** Expliquez d'abord l'idée du décalage horaire.** Les intervieweurs aiment vous voir compris pourquoi les réunions simultanées sont spéciales.
2. **Afficher l'astuce de réinitialisation du DSU** – c'est l'œuf de Pâques* qui transforme une solution Naïve du DSU en solution optimale.
3. **Mentions alternatives** (BFS avec une file d'événements estampés dans le temps, ou un graphique par horodatage). Cela montre que vous êtes conscient du paysage.
4. **Optimisation de l'espace** – par exemple, réutiliser le vecteur de réunions, ou utiliser un vecteur de nœuds modifiés au lieu de réinitialiser tout le tableau parent.
5. **Pratique sur des problèmes similaires** – p.ex., *BFS avec contraintes*, *Union‐Find avec fenêtres de temps*.

---

Conclusion

LeetCode 2092 vous apprend à mélanger deux concepts classiques:

**BFS** (accessibilité)
- **Union-Find** (composants connectés)

...et de les combiner avec une astuce **time-batching** qui respecte les règles de concurrence du problème.
La maîtrise de ce modèle vous donnera confiance pour les questions sur *les réseaux temporaires*, *la propagation animée par l'événement* et *la connectivité dynamique* dans les entrevues techniques.

---

### Références & Lecture supplémentaire

- [Union-Find (DSU) – Wikipedia] (https://en.wikipedia.org/wiki/Disjoint-set_data_structure)
- [BFS sur les graphiques – LeetCode](https://leetcode.com/problèmes/breadth-first-search/)
- [Problèmes de graphiques assortis de temps – Codeforces EDU](https://codeforces.com/blog/entry/11978)

Bon codage ! C'est ce qu'il a dit