---
titre: LeetCode 1697. Vérification de l'existence des chemins limités de longueur des bords -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 1697 – Vérification de l'existence de voies limitées Edge-Length
### Les bons, les mauvais, et les affreux Un profond- Dive Blog pour les demandeurs d'emploi

> **Mot-clé cible**: *LeetCode 1697 solution* – *union‐find* – *edge‐longueur limitée* – *problème dur* – *codage interview*

Si vous êtes à la chasse pour ce problème de LeetCode qui fera des recruteurs s'asseoir et vous remarquer, vous voulez maîtriser **1697. Vérification de l'existence des chemins limités de longueur des bords**.
Ci-dessous vous trouverez:

- Oui. Ce que vous allez apprendre
-- -- -- -- -- -- -- -- -- -- --
Autres La stratégie optimale **union‐find** (disjoint‐set) O((E+Q) log(E+Q) est assez rapide pour 105 bords et requêtes.
Tri des astuces pour garder les réponses dans l'ordre original
Manipulation de multi-edges et de grandes limites entières
Clean, language-agnostic implementation

---

- Oui. 1. Récapitulation des problèmes

> **Don**
> * Nœuds `n` (0-basés).
> * `edgeList[i] = [ui, vi, disi]` – bord non dirigé avec distance `disi`.
> * `queries[j] = [pj, qj, limitj]` – demander si un chemin existe de `pj` à `qj` **avec tous les bords < limitj**.

> **Retour** `boolean[] response` – une valeur par requête.

**Constraints** (plus mauvais cas)

* «2 ≤ n ≤ 105»
* `1 ≤ edgeListe.longueur, requêtes.longueur ≤ 105 "
* `1 ≤ disi, limitej ≤ 109 "
* Plusieurs bords peuvent exister entre la même paire de nœuds.

---

- Oui. 2. Pourquoi un syndicat-Find (un syndicat disjoint-Set) fonctionne

Considérez chaque bord comme un pont qui devient disponible lorsque sa distance est ** strictement plus petite** que la requête actuelle.
Si nous traitons tous les bords dans **de l'ordre croissant de la distance**, nous pouvons incrémenter le graphe:

1. **Trier** tous bords par distance.
2. **Trier** toutes les requêtes par "limite".
(Souvenez-vous de l'index original pour remettre la réponse plus tard.)
3. Maintenir une structure de DSU sur les nœuds `n`.
4. Tandis que le prochain edge=s distance `< current request=s limit`, unissez ses deux paramètres.
5. Après la fusion de toutes les arêtes applicables, les deux nœuds de la requête sont connectés s'ils appartiennent au même ensemble DSU.

Parce que nous traitons les requêtes dans la "limite" ascendante, chaque bord est considéré **une fois** – donnant une complexité globale de
**O((E + Q) log (E + Q)** pour le tri plus **O(E α(n))** pour les opérations DSU (`α` = inverse Ackermann, pratiquement constante).

---

- Oui. 3. Les bons, les mauvais, les méchants

Aspect du bien
- C'est quoi ?
**Algorithme **= O(E+Q) log (E+Q) → rapide pour 105== Aucune –=
**Mise en œuvre de l'USD**=La compression du chemin + union‐par‐rank → quasi-constante amortie== Nécessite une gestion soigneuse de l'index (0‐basée)=Le fait d'oublier la mise à jour de `parent» dans `find' conduit à des boucles infinies==
**Désormais des questions**=Conserve les réponses dans l'ordre original==Requiert une mémoire supplémentaire pour l'index==Si vous triez par `limité` mais oubliez de stocker l'index original, vous retournerez les mauvaises réponses===
**Multiple Edges**=Poigné automatiquement – nous les traitons tout simplement= Pas de manipulation spéciale nécessaire=Si vous dédoublez les bords par erreur, vous perdez des informations==
**Edge & Limit Size**= 32 bits nombre suffisant, mais utiliser `long` si vous êtes paranoïaque.

---

- Oui. 4. Code complet – Java, Python, C++

> Les trois implémentations utilisent la même logique.
> Chaque fichier est autonome, comprend les importations nécessaires et est prêt à être collé dans votre environnement IDE ou LeetCode.

#### 4.1 Java

"Java
Importation de java.util.*;

// -----------------
classe DSU {
parent final privé;
rang final privé; // syndicat par rang

DSU(int n) {
parent = nouveau int[n];
rang = nouvelle int[n];
pour (int i = 0; i < n; ++i) parent[i] = i;
}

int find(int x) {
// Compression de la trajectoire
si (parent[x] != x) parent[x] = find(parent[x]);
retour du parent[x];
}

union vide(int x, int y) {
int rx = find(x);
int ry = find(y);
i (rx) retour;

// Union par grade
si [rx] < rang[ry]) parent[rx] = ry;
sinon si (rank[rx] > rank[ry]) parent[ry] = rx;
autres {
parent[ry] = rx;
rang[rx]++;
}
}
}

// - Oui. Solution principale - Oui.
solution de classe publique {
public booléen[] distanceLimité Voies existantes(int n,
[][] bord Liste,
int[][] questions) {
// Joindre les indices originaux aux requêtes
int m = requêtes. longueur;
[] qWithIdx = nouvelle int[m][4];
pour (int i = 0; i < m; ++i) {
qWithIdx[i][0] = requêtes[i][0];
qWithIdx[i][1] = requêtes[i][1];
qWithIdx[i][2] = requêtes[i][2];
qWithIdx[i][3] = i; // position originale
}

// Trier les bords par distance
les tableaux.sort(edgeList, Comparator.comparingInt(a -> a[2]);

// Trier les requêtes par limite
Tableau.sort(qWithIdx, Comparator.comparingInt(a -> a[2]));

DSU dsu = nouveau DSU(n);
booléen[] ans = nouveau booléen[m];
int eIdx = 0; // pointeur sur les bords triés

pour (int[] q : qWithIdx) {
limite int = q[2];
// Ajouter tous les bords avec la distance < limite
pendant que (eIdx < ledgeList.longueur && ledgeList[eIdx][2] < limite) {
dsu.union(edgeList[eIdx][0], edgeList[eIdx][1]);
eIdx++;
}
// Si les deux nœuds sont connectés, la réponse est vraie
[q[3]] = dsu.find(q[0)] == dsu.find(q[1]);
}
le retour des an;
}
}
«» "

> **Comment courir**
> *Passez la classe `Solution` dans LeetCode, puis appelez `distanceLimitedPathsExist(...)`. *

---

#### 4.2 Python (Python 3)

'`python
de taper l'importation Liste

C'est... Le Mémorandum d'accord...
Classe DSU:
def __init_(self, n: int):
auto-parent = liste(range(n))
Self.rank = [0] * n

def find(self, x: int) -> Int:
si soi-même. parent[x] != x:
Self.parent[x] = self.find(self.parent[x]) La compression du chemin
Revenez vous-même. parent[x]

def union(self, x: int, y: int) -> Aucun:
xr, yr = self.find(x), self.find(y)
si xr == yr: retour
si self.rank[xr] < self.rank[an]:
auto.parent[xr] = année
elif self.rank[xr] > self.rank[an]:
auto-parent[an] = xr
Sinon:
auto-parent[an] = xr
Self.rank[xr] += 1

♪ - Oui. Principale --------
Solution de classe:
distance Paths limités Existe(
self, n: int, edgeListe: List[List[int]], requêtes: List[List[int]]
-> Liste [bool]:
# Joindre l'index original à chaque requête
q_with_idx = [q + [i] pour i, q dans les requêtes]

# Trier les bords et les requêtes
edgeList.sort(key=lambda x: x[2])
q_with_idx.sort(key=lambda x: x[2])

dsu = DSU(n)
ans = [Faux] * len(creuses)
e_idx = 0

pour q dans q_with_idx :
limite = q[2]
alors que e_idx < len(edgeList) et edgeList[e_idx][2] < limite:
dsu.union(edgeList[e_idx][0], edgeList[e_idx][1])
e_idx += 1
[q[3]] = dsu.find(q[0]) == dsu.find(q[1])

retour et
«» "

> **Run**
> *Téléchargez la classe `Solution` vers LeetCode et lancez. *

---

### 4.3 C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

// -------- Le Mémorandum d'accord...
classe DSU {
public:
vecteur <int> parent, rnk;
DSU(int n) : parent(n), rnk(n, 0) {
(parent.begin(), parent.end(), 0);
}
int find(int x) {
retour parent[x] == x ? x : parent[x] = find(parent[x]); // compression du chemin
}
vide unit(int x, int y) {
int xr = find(x), yr = find(y);
si (xr == yr) retour;
si (rnk[xr] < rnk[an]) parent[xr] = an;
sinon si (rnk[xr] > rnk[an]) parent[an] = xr;
autres {
parent[an] = xr;
++rnk[xr];
}
}
};

// - Oui. Principale --------
solution de classe {
public:
vecteur<bool> distanceLimité Voies existantes(int n,
vecteur<vecteur<int>>& bord Liste,
vector<vector<int>&questions) {
int m = requêtes.size();
// stocker les requêtes comme [u, v, limite, original_idx]
vecteur<array<int,4>> qs;
qs.réserve(m);
pour (int i = 0; i < m; ++i)
qs.push_back({queries[i][0], requêtes[i][1], requêtes[i][2], i});

tri(edgeList.begin(), edgeList.end(),
[](const auto &a, const auto &b){ retourner a[2] < b[2]; });

tri(qs.begin(), qs.end(),
[](const auto &a, const auto &b){ retourner a[2] < b[2]; });

DSU dsu(n);
vecteur <bool> ans(m);
taille_t eIdx = 0;

pour (auto &q : qs) {
limite int = q[2];
pendant que (eIdx < ledgeList.size() && ledgeList[eIdx][2] < limit) {
dsu.unite(edgeList[eIdx][0], edgeList[eIdx][1]);
++eIdx;
}
[q[3]] = (dsu.find(q[0]) == dsu.find(q[1]));
}
le retour des an;
}
};
«» "

> **Compilé**
> *`g++ -std=c++17 -O2 solution.cpp && ./a.out'*

---

- Oui. 5. Comment les recruteurs jugeront votre argumentation

1. **Qualité du code** – Les trois langues utilisent un nom clair, des commentaires en ligne et aucune constante magique.
2. **Manipulation des caisses** – Les solutions gèrent correctement ** multi-edges** et **grandes limites** (pas de débordement entier).
3. **Complexité temporelle** – L'entrevue remarquera que vous ne faites pas de BFS/DFS naïf pour chaque requête.
4. ** Polyvalence linguistique** – Vous pouvez présenter les trois solutions dans un entretien ou un test technique.

---

- Oui. 6. Prochaines étapes: polonais vos compétences d'entrevue

Lire comme suit :
C'est la première fois que l'on s'en occupe.
*Algorithmes de graphiques *= *Union-Find* dans *Cracking the Coding Interview*=
*LeetCode discut*
*C++ STL* Autres
*Python *= `functools.lru_cache` pour mémoriser `find` si vous préférez la récursion
*Java*="Arrays.sort" + `Comparator.comparing Int' Autres

---

La pensée finale

Avec cette solution **union‐find**, vous pouvez résoudre LeetCode 1697 en moins d'une seconde sur l'entrée la plus difficile.
Afficher les recruteurs vous pouvez traduire un algorithme slick en code propre à travers **Java, Python, C++**, et vous serez un peu plus près de cette interview de rêve.

Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---

**Sentez-vous libre de copier/coller l'une des trois implémentations ci-dessus, de les exécuter localement et de vous vanter le jour de votre interview!**