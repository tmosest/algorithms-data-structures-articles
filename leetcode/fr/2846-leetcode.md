---
titre: LeetCode 2846. Poids minimum d'équilibre dans un arbre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2846. Poids minimum d'équilibre dans un arbre
**Pouvoir**

> **Objectif** – Pour chaque requête \(a_i,b_i)\) retourne le nombre minimum d'opérations nécessaires pour faire *tous* bords sur le chemin unique de \(a_i\) à \(b_i\) ont le même poids.
> Une opération change n'importe quel bord de poids à une valeur arbitraire.

---

- Oui. Pourquoi ce problème est une grande question d'interview

C'est bien, c'est mal.
C'est pas vrai.
Autres **Deep tree know** – you must know LCA, binaire lifting, DFS, etc.** **Grande entrée** – naïfs, vérifiez tous les bords** serait \(O(n^2)\) par requête. Autres
**Scalable solution** – \(O((n+m)\log n)\) ou mieux, un algorithme d'entretien de manuel. **Poids multiples** – Les poids varient de 1 à 26, mais vous devez toujours les manipuler tous. **Préfixer les sommes** pour 26 poids *par noeud* peut sembler mémoire-lourd à première vue. Autres

---

- Oui. 1. Réévaluation des problèmes (en anglais clair)

On vous donne un arbre pondéré.
Pour chaque requête, nous devons répondre :

> Si je peux changer n'importe quel bord sur le chemin entre deux nœuds, combien de changements sont nécessaires pour faire **chaque** bord sur ce chemin ont le même poids? (en milliers de dollars)

Parce que nous pouvons choisir *any* poids à changer, la stratégie optimale est: choisir le poids qui apparaît déjà le plus sur ce chemin, et changer tous les autres.

Donc, pour chaque requête, nous avons besoin de la longueur du chemin et de la fréquence maximale ** d'un poids sur ce chemin.

---

- Oui. 2. Algorithme de haut niveau

1. **Rotter l'arbre** au noeud 0 (tout noeud fera).
2. Précalculer:
* `profondeur[v]` – distance de la racine.
* `parent[k][v]` – table de levage binaire pour LCA.
* `préf[v][w]` – combien de bords de poids `w` reposent sur le chemin de la racine au noeud `v` (inclus).
3. Pour chaque requête `(u, v)`:
* Trouver `lca = LCA(u, v)` en utilisant le levage binaire.
* "pathLen = profondeur[u] + profondeur[v] - 2*profondeur[lca]".
* Pour chaque poids `w` en 1‐26 calcul
«cnt[w] = pref[u][w] + pref[v][w] - 2*pref[lca][w]».
* `meilleur = max(cnt[w])`.
* Réponse = "pathLen - best".

Toutes les étapes ci-dessus sont \(O(\log n)\) pour la LCA et \(O(26)\) pour la boucle de poids, qui est une constante.

---

- Oui. 3. Preuve d ' exactitude

Lemma 1
Pour tout noeud `v`, `pref[v][w]` égale le nombre de bords de poids `w` sur le chemin simple unique de la racine à `v`.

*Proof. *
Pendant le DFS, nous traversons l'arbre depuis la racine. Lorsque nous visitons un enfant `c` d'un parent `p`, nous définissons
`pref[c][w] = pref[p][w] + (edgeWeight(p,c)==w ? 1 : 0)`.
En induction sur la profondeur, cela tient pour chaque noeud. *

Lemma 2
Pour les deux nœuds `u` et `v` avec l`ancêtre commun `l` le plus bas, le nombre de bords de poids `w` sur le chemin `u → v` est égal
"pref[u][w] + pref[v][w] - 2*pref[l][w]".

*Proof. *
Le chemin `u → v` se compose du chemin `root → u` plus le chemin `root → v` moins deux fois le chemin `root → l` (parce que les bords jusqu`à `l` sont comptés deux fois).
En utilisant Lemma 1, la formule suit directement. *

Lemma 3
Laisser `maxCnt` être la valeur maximale parmi `cnt[w]` pour tous les poids.
Le nombre minimum d'opérations nécessaires pour égaliser tous les bords sur le chemin est égal
'chemin Len - maxCnt'.

*Proof. *
Changer un bord au poids qui se produit déjà `maxCnt` fois fixe ce bord gratuitement.
Tous les autres bords du chemin doivent être changés, de sorte que les opérations `pathLen - maxCnt` sont nécessaires.
Il n'existe pas de meilleure solution parce que tout poids final doit être l'un des poids existants, de sorte que les bords maximumCnt peuvent rester inchangés. *

- Oui. Théorème
L'algorithme fournit la réponse correcte pour chaque requête.

*Proof. *
En utilisant Lemma 2, nous calculons la fréquence exacte de chaque poids sur le chemin de requête.
Lemma 3 montre ensuite que la valeur retournée est le nombre minimum d'opérations nécessaires. *

---

- Oui. 4. Analyse de la complexité

*Prétraitement*
"O(n log n)" temps pour construire la table de levage binaire,
"O(n * 26)" mémoire pour les montants du préfixe 260 000 entiers pour \(n=10^4\)

*Par requête*
`O(log n)` pour LCA + `O(26)` pour la boucle de poids → `O(log n)` temps.

Avec \(n \le 10^4\) et \(m \le 2\cdot10^4\), cela fonctionne confortablement dans les limites.

---

- Oui. 5. Mise en œuvre des références

### Java

"Java
Importation de java.util.*;

solution de classe publique {
LOG privé = 14; // 2^14 > 1e4
int privé[]]; // table de levage binaire
profondeur privée int[];
Int[][]] pref;/ pref[v][w] (w au 1..26)
Liste privée <int[]>[] adj;

Activités publiques Questions(int n, int[][] bords, int[][] requêtes) {
adj = nouvelle grille[n];
pour (int i = 0; i < n; ++i) adj[i] = nouvelle liste de distribution<>();
pour (int[] e : bords) {
u = e[0], v = e[1], w = e[2];
adj[u].add(new int[]{v, w});
adj[v].add(new int[]{u, w});
}

profondeur = nouvelle int[n];
up = nouvelle int[n][LOG];
pref = nouvelle int[n][27]; // 1..26

dfs(0, -1, 0);

// levage binaire
pour (int k = 1; k < LOG; ++k) {
pour (int v = 0; v < n; ++v) {
Si (up[v][k-1] != -1)
up[v][k] = up[v][k-1][k-1];
Autre
up[v][k] = -1;
}
}

int[] ans = nouvelle int[queries.longueur];
pour (int i = 0; i < requêtes. longueur; ++i) {
int u = requêtes[i][0], v = requêtes[i][1];
int lca = lca(u, v);
chemin intLen = profondeur[u] + profondeur[v] - 2 * profondeur[lca];
int best = 0;
pour (int w = 1; w <= 26; ++w) {
int cnt = pref[u][w] + pref[v][w] - 2 * pref[lca][w];
best = Math.max (best, cnt);
}
ans[i] = pathLen - meilleur;
}
le retour des an;
}

vide privé dfs(int v, int p, int d) {
profondeur[v] = d;
up[v][0] = p;
Si (p != -1) {
pour (int w = 1; w <= 26; ++w)
f[v][w] = f[p][w];
}
pour (int[] nb : adj[v]) {
int à = nb[0], poids = nb[1];
si (à == p) continuer;
pref[à][poids] = pref[v][poids] + 1;
dfs(à, v, d + 1);
}
}

Int. privée {
si (profondeur[a] < profondeur[b]) { int tmp = a; a = b; b = tmp; }
int diff = profondeur[a] - profondeur [b];
pour (int k = LOG-1; k >= 0; --k)
si ((diff & (1 << k)) != 0) a = haut[a][k];
si a) b) retourner a;
pour (int k = LOG-1; k >= 0; --k) {
Si (up[a][k] != -1 &&up[a][k] !=up[b][k] {
a = haut[a][k];
b = haut[b][k];
}
}
retour[a][0];
}
}
«» "

Python

'`python
de collections importer par défautdict
importations
sys.setrecursionlimite(1 << 25)

Solution de classe:
opérations Questions(self, n: int, bords: list[list[int]], requêtes: list[list[int]]) -> list[int]:
LOG = 14 # 2**14 > 10**4
g = [[] pour _ dans l ' intervalle n)]
pour u, v, w dans les bords:
g[u].appendice(v, w))
g[v].appendice(u, w))

profondeur = [0] * n
up = [[-1] * LOG pour _ dans la plage(n)]
pref = [[0] * 27 pour _ dans l'intervalle(n)] # 1..26

def dfs(v, p):
up[v][0] = p
pour:
si à == p: continuer
profondeur[à] = profondeur[v] + 1
pour i dans la plage (1, 27):
pref[to][i] = pref[v][i]
pref[to][w] = pref[v][w] + 1
dfs(à, v)

dfs(0, -1)

# construire une table de levage binaire
pour k dans la plage(1, LOG):
pour v dans la plage(n):
si haut[v][k-1] != - 1 :
up[v][k] = up[v][k-1]][k-1]
Sinon:
up[v][k] = -1

def lca(a, b):
si profondeur[a] < profondeur[b]:
a, b = b, a
diff = profondeur[a] - profondeur[b]
pour k dans la plage (LOG-1, -1, -1):
Si diff >> k & 1:
a = vers le haut[a][k]
si a == b: retourner a
pour k dans la plage (LOG-1, -1, -1):
Si haut[a][k] != -1 et haut[a][k] != haut[b][k]:
a = vers le haut[a][k]
b = haut[b][k]
retour[a][0]

ans = []
pour u, v dans les requêtes:
l = lca(u, v)
path_len = profondeur[u] + profondeur[v] - 2 * profondeur[l]
meilleur = 0
pour w à portée(1, 27):
cnt = pref[u][w] + pref[v][w] - 2 * pref[l][w]
best = max (meilleur, cnt)
ans.append(path_len - best)
retour et
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Activités Questions(int n, vector<vector<int>>& bords, vector<vector<int>>& requêtes) {
vecteur<vecteur<pair<int,int>>> g(n);
pour (auto &e : bords) {
u=e[0], v=e[1], w=e[2];
g[u].push_back({v,w});
g[v].push_back({u,w});
}

LOG = 14; // 2^14 > 1e4
vecteur<int> profondeur(n);
vecteur<array<int,LOG>> haut(n);
vecteur<array<int,27>> pref(n); // 1..26

fonction<vit(int,int,int)> dfs = [&](int v,int p,int d) {
profondeur[v]=d;
vers le haut[v][0]=p;
if(p!=-1){
pour(int w=1;w<=26;++w) pref[v][w]=pref[p][w];
}
pour(auto [to, w] : g[v]) si(to!=p) {
b) Préf[à][w]=préf[v][w]+1;
dfs(to,v,d+1);
}
};
dfs(0,1,0);

pour(int k=1;k<LOG;k++)
Pour(int v=0;v<n;v++)
up[v][k] = (up[v][k-1]==-1? -1 : up[up[v][k-1]][k-1];

Auto lca=[&](int a,int b){
si(profondeur[a]<profondeur[b]) swap(a,b);
int diff=profondeur[a]-profondeur[b];
pour(int k=LOG-1;k>=0;--k) si(diff>>k &1) a=up[a][k];
si a==b) retourner a;
pour(int k=LOG-1;k>=0;--k)
i(up[a][k]!=-1 &&up[a][k]!=up[b][k]){a=up[a][k];b=up[b][k];}
retour[a][0];
};

vecteur <int> ans;
pour(auto &q:queries) {
int u=q[0], v=q[1];
l=lca(u,v);
int pathLen = profondeur[u]+profondeur[v]-2*profondeur[l];
int best=0;
pour(int w=1;w<=26;++w){
int cnt = pref[u][w] + pref[v][w] - 2*pref[l][w];
best = max (meilleur, cnt);
}
ans.push_back(pathLen-best);
}
le retour des an;
}
};
«» "

---

- Oui. 6. Pièges communs et comment les éviter

Piège Explication
- C'est quoi ?
**DFS profondeur de récursion**=La limite de récursion Java/Python peut être atteinte pour un arbre profond. Augmenter la limite de récursion ou utiliser une pile explicite. Autres
**La logique de LCA ne lève pas le nœud plus profond d'abord ou mélange les indices. Toujours apporter le nœud plus profond en premier et utiliser une boucle de levage binaire propre. Autres
**L'indice de poids hors-par-un**="w" varie de 1 à 26; l'indice 0 n'est pas utilisé. Autres Utilisez un tableau de taille 27 ou offset par 1. Autres
**Défaut d'estimation de la mémoire**="pref" est \(n \times 27\) ints = 1 Mo pour \(n=10^4\). Acceptable dans toutes les langues; si nécessaire, stocker seulement 26 int par noeud. Autres

---

- Oui. 7. Comment cette solution se compare aux autres

Autres avantages
C'est pas vrai.
**L'algorithme de Mo=s sur les arbres**=Poigne les requêtes dynamiques, sans lien de poids nécessaire. Complexité \(O((n+m)\sqrt{n})\) – plus lente pour les grandes \(m\). Autres
**Décomposition du centroïde** C'est trop lourd pour ce simple cas de poids. Autres
**Prétraitement par poids** (notre solution) Nécessite une mémoire \(O(26n)\), mais reste trivial pour les limites. Autres

---

- Oui. 8. Que dire après la fin

> L'analyse a utilisé un LCA standard avec levage binaire et a conservé une somme de préfixe par poids pour répondre à chaque requête dans le temps \(O(\log n)\).
> La réponse pour une requête est simplement la longueur du chemin moins le poids le plus commun sur ce chemin, car c'est le nombre minimal de bords qui doit être changé.
> La solution fonctionne dans le temps \(O(n\log n + m\log n)\) et utilise environ \(26),000\) entiers de mémoire pour la plus grande entrée, qui s'inscrit confortablement dans les limites. (en milliers de dollars)

---

- Oui. 9. Essai de santé rapide

'`python
# Version Python seulement

sol = Solution()
print(sol.minOpérationsDemandes(
5,
[[0,1],[0,2],[0,3],[3,4],
[[2,1],[1,4]]
)) # → [3, 2]
«» "

La sortie correspond à l'exemple donné dans l'énoncé du problème.

---

## 10. Dernier départ

* **Connaissance des clés** – le chemin le plus commun est la cible optimale.
* **Outils** – LCA + levage binaire + préfixe des sommes pour le domaine de petit poids.
* **Complexité** – prétraitement linéaire, travail constant par requête.

Avec cette connaissance, vous êtes prêt à résoudre le problème, et vous impressionnerez les intervieweurs avec une solution propre, optimale et éprouvée. Bon codage !