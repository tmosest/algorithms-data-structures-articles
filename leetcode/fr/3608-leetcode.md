---
titre: LeetCode 3608. Temps minimum pour les composants connectés K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3608 – Temps minimum pour les composants connectés K
**Moyenne – LeetCode**

> **Lien de problème**: <https://leetcode.com/problems/minimum-time-for-k-connected-components/>

Ci-dessous vous trouverez:

1. **Trois solutions complètes** – Java, Python, C++ – qui passent les contraintes dures ( `n, bords ≤ 105' ).
2. **Un billet de blog complet et convivial pour le référencement** qui explique l'intuition, donne le bon, le mauvais, le mauvais, et est adapté pour vous aider à obtenir un emploi.

---

- Oui. 1. Les trois réalisations

> Les trois utilisent la même idée : **procéder inversement aux bords** dans l'ordre décroissant du temps d'enlèvement et conserver un DSU (Disjoint-Set Union) pour compter les composants connectés.

#### 1.1 Java

"Java
Importation de java.util.*;

solution de classe {
// DSU (Union‐Find) avec compression de chemin
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
Union booléenne(int a, int b) {
int ra = find(a), rb = find(b);
si (ra) rb) retourner faux;
si (rank[ra] < rank[rb]) parent[ra] = rb;
sinon si (rank[ra] > rank[rb]) parent[rb] = ra;
Autre { parent[rb] = ra; rang[ra]++; }
retour vrai;
}
}

Int public minTime(int n, int[]] bords, int k) {
// Trier les bords en descendant le temps
les tableaux.sort(edges, a, b) -> Integer.compare(b[2], a[2]);

DSU dsu = nouveau DSU(n);
int comps = n; // initialement tous les nœuds sont isolés

pour (int[] e : bords) {
si (dsu.union(e[0], e[1])) {
comps--; // fusion de deux composants
si (comps < k) // nous venons de tomber en dessous de k
e[2];
}
}
// si nous n'avons jamais chuté en dessous de k, la réponse est 0
retour 0;
}
}
«» "

#### 1.2 Python

'`python
de taper l'importation Liste

Classe DSU:
def __init_(self, n: int):
auto-parent = liste(range(n))
Self.rank = [0] * n

def find(self, x: int) -> Int:
si soi-même. parent[x] != x:
Self.parent[x] = self.find(self.parent[x])
Revenez vous-même. parent[x]

def union(self, a: int, b: int) -> C'est vrai.
ra, rb = self.find(a), self.find(b)
si rb:
Retour Faux
si self.rank[ra] < self.rank[rb]:
auto-parent[ra] = rb
elif self.rank[ra] > self.rank[rb]:
auto.parent[rb] = r
Sinon:
auto.parent[rb] = r
Self.rank[ra] += 1
retour Vrai

Solution de classe:
def minTime(self, n: int, bords: List[List[int]], k: int) -> Int:
# Tri par temps descendant
arêtes.sort(key=lambda e: -e[2])

dsu = DSU(n)
comps = n # tous les nœuds séparés

pour u, v, t dans les bords:
si dsu.union(u, v):
Comps -= 1
si comps < k:
retour t
retour 0
«» "

*## 1.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe DSU {
public:
vecteur <int> p, r;
DSU(int n = 0) { init(n); }
vide init(int n) {
p.resize(n);
l'attribution de r.(n, 0);
iota(p.begin(), p.end(), 0);
}
int find(int x) { retourner p[x] == x ? x : p[x] = find(p[x]); }
bool unit(int a, int b) {
a = find(a), b = find(b);
si a) b) retourner faux;
si (r[a] < r[b]) swap(a, b);
p[b] = a;
si (r[a] == r[b]) ++r[a];
retour vrai;
}
};

solution de classe {
public:
int minTime(int n, vector<vector<int>>& bords, int k) {
tri(edges.begin(), bords.end(),
[](const vector<int>& a, const vector<int>& b) {
a[2] > b[2];
});

DSU dsu(n);
d ' int comps = n;

pour (const auto &e : bords) {
si (dsu.unite(e[0], e[1])) {
si (--comps < k) retourne e[2];
}
}
retour 0;
}
};
«» "

---

- Oui. 2. Billet de blog – Le bon, le mauvais, et le mauvais temps minimum pour K composants connectés

> **Audience cible**: Ingénieurs de première ligne, passionnés de structures de données et tous ceux qui se préparent à une entrevue de type LeetCode.
> **Objectif** : Parcourez le problème, montrez comment le casser, soulignez les écueils et donnez des idées prêtes à l'entrevue.

---

2.1 Introduction

**LeetCode 3608 – Minimum Time for K Connected Components** est un problème classique *graph + DSU* qui teste votre compréhension du traitement Union-Find, tri et hors ligne. Il ne s'agit pas d'un problème trivial de composants de compte ; la torsion est que vous êtes demandé de trouver le *temps minimum* auquel le graphique aura *au moins* composants `k` après avoir enlevé les bords en dessous de ce temps.

> **SEO Mots-clés**: Temps minimum pour K Components connectés, LeetCode 3608 solution, Union‐Find graph problem, -DSU interview, -graph components interview question.

---

2.2 Réévaluation des problèmes

> Compte tenu des nœuds `n` (0-based) et `edges[i] = [u, v, time]` – un bord non dirigé qui disparaît à l'époque `time`.
> Pour un temps `t`, tous les bords avec `time <= t` sont enlevés.
> Trouvez le **minimum** `t` tel que le graphique restant possède **au moins `k` composants connectés**.
> Si le graphique contient déjà `k` ou plus de composants avant toute suppression, la réponse est `0`.

**Constances**: "1 ≤ n ≤ 105", "0 ≤ bords longueur ≤ 105", "temps ≤ 109".

---

2.3 Intuition – Le processus inverse

Pensez aux bords de *adding* au lieu de les enlever.

1. **Initialement**: Tous les bords sont enlevés → `n` noeuds isolés → `n` composants.
2. **Ajouter les bords dans l'ordre décroissant du "temps"** (c'est-à-dire les bords qui *survivraient* plus longtemps).
3. Chaque ajout fusionne potentiellement deux composants → `components--`.
4. Lorsque vous ajoutez un bord dont *time* est `t` et le nombre de composants tombe **ci-dessous** `k`, cela signifie
*Si nous avions enlevé tous les bords avec `temps <= t`, nous n'aurions pas **** fusionné ce bord → nous avons encore ≥ k composants. *
Par conséquent, `t` est le temps **minimum** qui garantit au moins `k` composants.

> **Pourquoi inverser?**
> * Enlever les bords → le temps augmente, les composants augmentent.
> * Ajouter les bords en arrière → le temps diminue, les composants diminuent.
> * Le premier moment où nous franchissons le seuil donne la réponse directement.

---

#### 2.4 Structure des données – Unité d'ensemble disjointe (Union-Find)

* **Trouver** avec compression de chemin.
* **Union** par grade (ou taille).
* Garanties d'une durée presque constante amortie: `α(n)` (inverse Ackermann).

> **L'heure de se souvenir**:
> *Dans les interviews, vous pouvez mentionner "DSU" , "Union‐Find" , "compression de chemin" , "rank‐by‐size" comme un signal que vous connaissez le trick classique pour la connectivité dynamique. *

---

2.5 Algorithme Étape par étape

Pourquoi ? Autres
- C'est quoi ?
Classer `edges` par `time` en descendant. Il fallait procéder en ordre inverse. Autres
Autres Initialisez le DSU avec les nœuds `n`; définissez `composants = n`. Autres
Autres Pour chaque bord `[u, v, t]` dans la liste triée: Autres
Autres Si `union(u, v)` réussit → `components--`. Autres
Autres Si après la fusion `composants < k` → **retour `t`**. Autres
Autres Après la boucle → retourner `0`. Le graphique n'a jamais eu besoin d'ajouter de bord pour atteindre ≥ k composants. Autres

---

### 2.5 Code complet – Choisissez votre langue

*Java* – classe `Solution` avec aide interne `DSU`.
*Python* – classe `DSU` + méthode `Solution`.
*C++* – classe `DSU` + `Solution::minTime`.

> **Note** : Les trois extraits de code ci-dessus se trouvent dans la section « Full » ; copiez-les directement dans votre IDE.

---

2.6 Analyse de la complexité

Opération Temps Espace
- C'est quoi ?
(avec `m = bords.longueur`) extra au-delà de l'entrée
Opérations du DSU **O((n + m) α(n))**
Total **O((n + m) log m)** (le tri domine)

Avec `n, m ≤ 105`, cela s'inscrit facilement dans les limites de 2 s / 512 MB de LeetCode.

---

#### 2.7 Les mauvais – Pièges communs

Pourquoi ça arrive ?
- Oui.
**Trier dans l'ordre ascendant**= Ajoute des bords qui disparaissent *plus tôt* → nombre de composants *augmentations* → algorithme ne voit jamais une goutte d'eau au-dessous de `k`.= Tri **descendant** (`b[2] - a[2]`). Autres
**La compression de la trajectoire de déplacement de l'Union se dégrade en O(n) par opération pour les arbres biaisés → TLE. Utiliser la compression de chemin (`find(x) = parent[x]==x?x:parent[x]=find(parent[x])`). Autres
**L'utilisation incorrecte de la taille**= Toujours attacher un arbre plus grand à un arbre plus petit entraîne un déséquilibre de rang si vous ignorez la taille. Union‐par‐classe ou union‐par‐taille; mettre à jour le rang/taille en conséquence. Autres
**Returning `t` **after** component count *remains* ≥ `k` au lieu de `< k`. Autres
En fait, la réponse est toujours `0` si le graphique commence par des composants `n`; la boucle la couvre. Pas de cas particulier. Autres

---

Pourquoi certaines personnes l'écrivent mal

1. **Recherche binaire + en ligne**
*De nombreux candidats essaient de faire des recherches binaires sur `t` et de reconstruire le DSU chaque itération. *
*Résultat*: `O(m log T)` avec `T = 109` → ~30 reconstruit → 3 × 106 opérations syndicales → **TLE**.
**Leçon**: Évitez la reconstruction de DSU par itération; utilisez le traitement inversé *offline*.

2. **Liste d'adjonctions + DFS par retrait**
*Enlever les bords un par un et recompiler les composants avec DFS donne `O(m n)` – désespéré. *
**Leçon** : Le graphique est *dynamique*, utilise une structure de données qui supporte *la connectivité dynamique* dans un temps quasi linéaire.

3. **Utilisation d'une carte du temps → bords* *
*Le stockage des bords dans une carte clé par le temps et l' itération au fil du temps peut conduire à une boucle O(T). *
**Leçon**: Ne jamais itérer sur toutes les fois possibles; ne traiter que les bords existants.

---

2.9 Entretien— Conseils prêts

Conseil Explication
C'est pas vrai.
**Dites votre plan à haute voix** Autres
**Mention Union-Trouver par nom** Autres
**Expliquez la logique inverse** Autres
**La compression du chemin de mention** Autres
**Conversation de complexité** Le DSU est linéaire. Autres
**Les cas d'Edge**=Si `k` est égal `n`, la réponse est toujours `0`. Autres
**Pourquoi déconnecter?****** Nous n'avons pas besoin de simuler chaque unité de temps; nous sautons directement aux seuls bords pertinents. Autres

---

#### 2.10 Rapide- Liste de contrôle des codes

Mise en œuvre du DSU
- C'est quoi ?
*Java************************************************************************************************************************************************************************************************************************************************************** Autres
**Python**= classe DSU="edges.sort(key=lambda e: -e[2])=" Autres
**C++**="vector<int> p, r`="sort(edges.begin(), bords.end(), cmp)` où `cmp` commande par `time` descendant

---

2.11 Conclusion

> Le problème du temps minimum pour K Composants connectés est une belle illustration de la façon dont le traitement hors ligne + Union‐Find peut transformer une question de suppression apparemment dynamique en un simple balayage linéaire.

> La maîtrise de ce modèle vous fera confiance dans n'importe quel entretien graphique + DSU. De plus, vous avez maintenant **trois solutions prêtes à coller** en Java, Python et C++ – exactement ce que les recruteurs recherchent.

Autres **À emporter**: *Réverser le problème* → *DSU garde les composants* → *le premier point de passage est la réponse*.
> Et c'est la sauce secrète que vous pouvez expliquer avec confiance dans une entrevue de codage.

---

2.12 Pensée finale

Si vous préparez votre prochaine entrevue, pratiquez ce modèle sur d'autres problèmes graphiques LeetCode, tels que **Nombre d'îles (DFS/BFS)**, **Composants connectés dans le graphique non dirigé** (`207. Programme de cours`), et la famille ** Connectivité dynamique**. Plus vous pouvez *visualiser l'ajout* ou *enlever* bords, plus il devient facile de repérer le tour du processus inverse.

Bonne chance, et que votre DSU trouve toujours le bon parent! C'est ce qu'il a dit.

---

2.13 Références et lectures supplémentaires

* <https://cp-algorithms.com/data_structures/disjoint_set_union.html> – DSU tutoriel
* <https://leetcode.com/problemset/all/?topicSlugs=graph> – Plus de problèmes graphiques DSU
* <https://github.com/mission-peace/interview> – Questions pratiques du Mémorandum d'accord

---

*Bon code ! *