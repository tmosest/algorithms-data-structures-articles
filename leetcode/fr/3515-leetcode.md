---
titre: LeetCode 3515. Le chemin le plus court dans un arbre pondéré -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 3515 – Voie la plus courte dans un arbre pondéré
> C++ – Code complet + Interview Style Blog**

---

Récapitulation des problèmes

Vous êtes donné un arbre pondéré enraciné au nœud 1.
Deux types de questions arrivent en ligne :

Questionnement Signification
C'est quoi ?
**Mise à jour** du poids du bord `(u, v)` à `w`. La paire est garantie être un bord existant. Autres
Retourner la distance la plus courte** de la racine (node 1) au noeud `x`. Autres

«n, q ≤ 105», poids des bords
La tâche est de répondre efficacement à toutes les requêtes `[2, x]` tout en prenant en charge les mises à jour de bord.

---

C'est vrai. Solution naïve (Pourquoi il a gagné)

* Pour chaque changement `[1, ...]` reconstruire toutes les distances avec DFS/BFS – **O(n)** par mise à jour.
* Pour chaque `[2, ...]` lire la distance précalculée – **O(1)**.

Avec jusqu'à `105` mises à jour, cela devient `O(n·q)` .

---

C'est vrai. L'Élégante Idée – Euler Tour + Fenwick Tree

1. **FDS de la racine* *
* Calculer la distance initiale `dist[v]` du nœud 1 à chaque nœud "v".
* Enregistrer l'entrée (`tin[v]`) et la sortie (`tout[v]`) temps – le classique **Euler tour**.
* Pour un arbre enraciné, le sous-arbre entier de `v` occupe le segment continu `[tin[v], tout[v]`.

2. **Map chaque bord à l'enfant* *
* Pour un bord `(u, v)` le noeud avec plus grand `tin` est l'enfant.
* Conservez le poids actuel dans une carte «edgeWight[(parent, enfant)]».

3. **Fenwick (Binaire indexé) Arbre**
* Nous avons besoin de *range add* (mise à jour du sous-arbre entier) et de *point request* (distance à un noeud).
* Un arbre Fenwick qui prend en charge les mises à jour de gamme avec deux mises à jour de points fonctionne dans `O(log n)`.

4. ** Traitement d'une requête**

* **Mise à jour `[1, u, v, w]'**
* Identifier l'enfant (`c`).
* 'delta = w - oldWey '.
* Appliquer `delta` au segment `[tin[c], tout[c]]` par l'intermédiaire de "rangeAdd".
* Magasinez `newWeight` dans la carte.

* **Distance `[2, x]`**
* Réponse = `dist[x] + fenwick.pointQuery(tin[x])`.
* `dist[x]` est la distance de base, `fenwick` contient tous les deltas accumulés.

**Complexités* *

Opération Temps Espace
- C'est quoi ?
DFS (préprocessus) Autres
Chaque requête Autres

C'est assez rapide pour les nœuds `105` et les requêtes.

---

Code Passage

Voici des implémentations propres, prêtes à coller dans **Java**, **Python** et **C++** suivant le style Leetcode.

---

Solution Java

"Java
Importation de java.util.*;
importation java.io.*;

solution de classe publique {
*/
classe statique privée Fenwick {
bit final privé long[];
final privé n;
Fenwick(int n) { this.n = n; bit = new long[n + 2]; }
vide add(int idx, long val) {
pour (int i = idx; i <= n; i += i & -i) bit[i] += val;
}
longue somme(int idx) {
long res = 0;
pour (int i = idx; i > 0; i -= i & -i) res += bit[i];
retour rés;
}
/* ajouter: ajouter val à [l, r] */
plage de vides Ajouter (int l, int r, long val) {
ajouter(l, val);
ajouter(r + 1, -val);
}
}

- Oui. Aide clé de bord --------- */
clé longue statique privée(int a, int b) {
retour ((long) a << 32)= (b & 0xffffffffL);
}

- Oui. Solution principale
Liste publique<Intégrer> arbreQueries(int n, Liste<Intégrer>> les bords,
Liste des requêtes<Liste<entier>> {
/* liste des dépendances */
Liste <Liste<int[]>> g = nouvelle liste <>();
pour (int i = 0; i <= n; i++) g.add(new ArrayList<>());
pour (Liste <entier> e : bords) {
u = e.get(0), v = e.get(1), w = e.get(2);
g.get(u).add(nouvelle int[]{v, w});
g.get(v).add(nouvelle int[]{u, w});
}

/* tableaux */
long[] dist = nouveau long[n + 1];
int[] étain = nouveau int[n + 1];
int[] tout = nouvelle int[n + 1];
long[] minuteur = nouveau long[1]; // pour émuler un entier mutable
Carte <Long, entier> poidsMap = nouveau HashMap<>();

/* DFS pour calculer la dist, l'étain/tout et le poids des enfants */
dfs(1, 0, 0, g, dist, étain, tout, minuterie, masse map);

Fenwick = nouveau Fenwick(n);
Liste <Integer> ans = nouvelle liste de distribution<>();

pour (Liste<entier> q : requêtes) {
si (q.get(0)) 1) {/ MISE À JOUR
int u = q.get(1), v = q.get(2), w = q.get(3);
parent int, enfant;
si (tin[u] < tin[v]) { parent = u; enfant = v; }
Autre { parent = v; enfant = u; }

vieux = poidsMap.get(clé(parent, enfant));
delta long = (long) w - vieux;
fenwick.rangeAdd(tin[enfant], tout[enfant], delta);
poidsMap.put(clé(parent, enfant), w);
} autres { // DISTANCE
int x = q.get(1);
long cur = dist[x] + fenwick.sum(tin[x]);
as.add(int) cur); // s'insère dans les contraintes
}
}
le retour des an;
}

- Oui. Mise en œuvre du DAM
vide privé dfs(int u, int parent, int profondeur, List<List<int[]>> g,
long[] dist, int[] étain, int[] tout, long[] minuterie,
Carte <Long, entier> map) {
dist[u] = profondeur;
tin[u] = (int) timer[0] + 1; // 1-based index
minuterie[0]++;

pour [int[] nb : g.get(u) {
int v = nb[0], w = nb[1];
si (v) le parent continue;
poidsMap.put(key(u, v), w); // stocker parent→ poids de l'enfant
dfs(v, u, profondeur + w, g, dist, étain, tout, minuterie, map);
}
tout[u] = (int) minuterie[0];
}
}
«» "

**Points clés**

* `long` partout – évite le débordement si vous décidez de détendre les contraintes.
* La touche de bord emballe deux `int` dans un `long` pour un `HashMap` rapide.
* `Fenwick.range Add` est un classique *différence tableau*.

---

Solution Python

'`python
importations
de collections importer par défautdict
de taper l'importation Liste

C'est... Arbre Fenwick pour la gamme ajouter + requête point ---------
Catégorie Fenwick:
def __init_(self, n: int):
auto.n = n
Autobit = [0] * (n + 2)

def _add(self, i: int, delta: int) -> Aucun:
alors que i <= self.n:
Soi.bit[i] += delta
i += et -i

def range_add(self, l: int, r: int, delta: int) -> Aucun:
_Ajouter(l, delta)
_Ajouter(r + 1, -delta)

def point_query(self, i: int) -> Int:
s = 0
alors que 0:
s += self.bit[i]
I -= et -i
retour s


Solution de classe:
def treeQueries(self, n: int,
bords: Liste[Liste[int]],
questions : Liste[List[int]]) -> Liste[int]:
# liste d'adjacence
g = [[] pour _ dans la plage (n + 1)]
pour u, v, w dans les bords:
g[u].appendice(v, w))
g[v].appendice(u, w))

dist = [0] * (n + 1)
étain = [0] * (n + 1)
tout = [0] * (n + 1)
minuterie = 1

# carte: (parent, enfant) -> Poids
_w = {}

def dfs(u: int, p: int, d: int):
minuterie non locale
dist[u] = d
étain[u] = minuterie
minuterie += 1
pour v, w in g[u]:
si v == p: continuer
edge_w[(u, v)] = w # stock parent→ poids de l'enfant
dfs(v, u, d + w)
tout[u] = minuteur - 1

Dfs(1, 0, 0)

bit = Fenwick(n)
ans = []

pour q dans les requêtes :
si q[0] == 1: # mise à jour
_, u, v, new_w = q
enfant = v si tin[u] < tin[v] autre u
parent = u si enfant == v autre v
old = edge_w[(parent, enfant)]
delta = nouveau_w - ancien
bit.range_add(tin[enfant], tout[enfant], delta)
edge_w[(parent, enfant)] = new_w
Autre: # distance
_, x = q
cur = dist[x] + bit.point_query(tin[x])
ans.append(cur)

retour et
«» "

**Pourquoi c'est rapide**

* `timer` est 1-basé de sorte que les indices Fenwick correspondent aux temps d'entrée Euler.
* `edge_w` conserve la carte d'enfant *exact* – pas de DFS répété.

---

C++ Solution

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

classe Fenwick {
vecteur <long> bit;
l'élément n;
public:
Fenwick(int n=0){ init(n); }
vide init(int n_) { n = n_; bit.assign(n+2, 0); }
vide add(int idx, long long val){
pour(int i=idx;i<=n;i+=i&-i) bit[i] += val;
}
longue somme(int idx){
longue rés=0;
pour(int i=idx;i>0;i-=i&-i) res+=bit[i];
retour rés;
}
// plage ajouter [l,r] += valeur
plage de vides Ajouter (int l,int r, long val) {
ajouter(l,val); ajouter(r+1,-val);
}
};

clé longue statique en ligne(int a,int b){
retour (static_cast<long long>(a)<<32)) (b & 0xffffffffLL);
}

solution de classe {
public:
vector<int> treeQueries(int n, vector<vector<int>>& bords,
vector<vector<int>&questions) {
/* dépendance */
vecteur<vector<pair<int,int>>> g(n+1);
pour(auto &e: bords) {
int u=e[0],v=e[1],w=e[2];
g[u].push_back({v,w});
g[v].push_back({u,w});
}

vecteur <long> dist(n+1,0);
vecteur<int> étain(n+1), tout(n+1);
la minuterie int=0;

non ordonné_map<long long,int> bordW; // parent->poids de l'enfant

fonction<vit(int,int,long long)> dfs = [&](int u,int p,long long d) {
dist[u]=d;
tin[u]=++timer;
pour(auto [v,w]: g[u]) {
iv==p) continuer;
edgeW[key(u,v)] = w;
dfs(v,u,d+w);
}
tout[u]=timer;
};
dfs(1,0,0);

Fenwick fw(n);
vecteur <int> ans;
pour(auto &q: requêtes) {
if(q[0]==1){ // mise à jour
int _,u,v,newW; tie(_,u,v,newW)=make_tuple(q[0],q[1],q[2],q[3]);
enfant int = (tin[u] < tin[v])? v : u;
parent int = (enfant==v)? u : v;
long long vieuxW = bordW[clé(parent,enfant)];
delta long = nouveauW - vieuxW;
fw.rangeAdd(tin[enfant], tout[enfant], delta);
edgeW[key(parent,child)] = nouveauW;
}else{ // distance
int _,x; tie(_,x)=make_tuple(q[0],q[1]);
longue courbure = dist[x] + fw.sum(tin[x]);
as.push_back((int)cur);
}
}
le retour des an;
}
};
«» "

> **Note :**
> * La solution utilise "long" pour les sommes internes afin d'éviter les débordements lorsque l'environnement d'entrevue change les contraintes.
> * `key()` emballe une paire de 32 bits dans une clé de 64 bits – parfait pour une `unordered_map`.

---

Comment présenter cette solution dans une entrevue

1. **Afficher que l'arbre est *statique* dans la structure** – vous pouvez préprocéder une fois.
2. **Expliquer la tournée d'Euler** – tous les sous-arbres deviennent des segments contigus.
3. **Expliquez le tour de Fenwick** – range add via deux mises à jour point; requête n'est qu'une somme préfixe.
4. **Étendez le `O(log n)` par requête** – répond aux contraintes.
5. **Pièges de Mention** – par exemple, oublier de mettre à jour la carte ou utiliser des indices basés sur 0 avec un arbre Fenwick basé sur 1.

---

Pièges communs & Quirks

Problème
C'est-à-dire
**Dégissez la direction**=Traitez `(u, v)` et `(v, u)` comme le même enfant → parent. Autres Toujours déterminer l'enfant en comparant `tin[u]` et `tin[v]`. Autres
**Indicateurs de Fenwick** Utiliser `++timer` pour le temps d'entrée; `fw.sum(tin[x])`. Autres
**Overflow**= Utiliser `int` pour les sommes → résultats négatifs sur des graphiques énormes. Utilisez `longe` ou `long` partout. Autres
**Collision des clés de carte**= Utiliser `unordered_map<int, int>` sur la paire → collision de hachage. Pack paire dans "long long" ou utiliser `map<pair<int,int>,int>`. Autres
**Profondeur de la récursion**=Débordement de la cheminée pour les arbres profonds. Autres

---

À emporter

* **Prétraitement + tableau de différence + Euler tour = élégant et efficace. **
* La méthode est **langue-agnostique** – vous pouvez l'adapter à Java, Go, Rust, etc.
* Dans un entretien d'emploi, toujours *justifier* chaque choix de conception et **prévoir les questions de l'intervieweur** sur la complexité, la mémoire et les cas de bord.

Bonne chance ! *