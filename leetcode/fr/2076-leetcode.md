---
titre: LeetCode 2076. Demandes d'amis restreints -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Aperçu de la solution – 2076. Demandes d'amis restreints

** Problème* *
Vous avez des gens `n` (0-indexés).
- "restrictions[i] = [x, y]" signifie *x* et *y* ne peuvent jamais devenir amis, directement ** ou** indirectement (par n'importe quelle chaîne d'amitiés).
- `requests[j] = [u, v]` est une demande ami qui doit être traitée dans l'ordre.
* Si la demande peut être acceptée, *u* et *v* deviennent des amis directs pour toutes les demandes futures. *

Retourner un tableau booléen `résultats[j]` indiquant si la *j*‐e demande a réussi.

> **Constraints**
> - "2 ≤ n ≤ 1000"
> - `0 ≤ restrictions.longueur ≤ 1000`
> - `1 ≤ demandes longueur ≤ 1000`

La solution naïve (vérifier chaque restriction pour chaque demande) serait **O(n ·m)**, ce qui est parfaitement bon pour les limites, mais nous pouvons résoudre le problème avec élégance avec **Disjoint Set Union (DSU)**, également connu sous le nom de **Union‐Find**.

---

- Oui. 2. Pourquoi l'union?

*Chaque personne appartient à un cercle ami (composant connecté).
Si deux personnes sont dans le même composant, elles sont déjà amies, sinon elles ne le sont pas. *

**Idée clé**

Quand une requête `[u, v]` arrive
1. Si `find(u) == find(v)` → déjà amis → *succès*.
2. Autrement, nous **hypothétiques** fusionnons les deux composants et vérifions ensuite toutes les restrictions.
*Si une restriction `[x, y]` se retrouverait dans le même composant, nous devons rejeter la demande. *

Comme le nombre de demandes et de restrictions est ≤ 1000, une analyse linéaire des restrictions pour chaque demande est assez rapide, tout en nous donnant un *O(α(n))* temps de recherche/d'union amorti.

---

- Oui. 3. Complexité

Étape
C'est quoi ?
"find" "O(α(n)" (inverse Ackermann)
"Union" "O(α(n)" Autres
Traitement d ' une demande
Total "O(q · r)" avec "q ≤ 1000" → ≤ 1 000 000 opérations

Mémoire: `O(n + r)`.

---

- Oui. 4. Exécution

Voici les implémentations **commentées** dans **Java**, **Python** et **C++**.

Autres Toutes les solutions supposent que les tableaux d'entrée sont indexés à zéro, selon l'énoncé du problème.

---

### 4.1 Java (Clean & Commented)

"Java
Importation de java.util.*;

solution de classe publique {
- Oui. Union‐Find (DSU) ---------- */
classe statique privée DSU {
Int[] parent, grade;
DSU(int n) {
parent = nouveau int[n];
rang = nouvelle int[n];
pour (int i = 0; i < n; i++) parent[i] = i;
}
int find(int x) {
si (parent[x] != x) parent[x] = find(parent[x]); // compression du chemin
retour du parent[x];
}
Union nulle(int a, int b) {
a = find(a); b = find(b);
si a) b) retour;
si (classe [a] < grade[b]) {
parent[a] = b;
} sinon si (rank[a] > rank[b]) {
parent[b] = a;
} autre {
parent[b] = a;
rang[a]++;
}
}
}

public booléen[] amiDemandes(int n, int[][] restrictions, int[][] demandes) {
int q = demandes. longueur;
booléen[] résultat = nouveau booléen[q];
DSU dsu = nouveau DSU(n);

pour (int i = 0; i < q; i++) {
int u = demandes[i][0];
int v = requêtes[i][1];

// déjà dans le même composant -> déjà amis
si (dsu.find(u) == dsu.find(v)) {
résultat[i] = vrai;
poursuivre;
}

// Union temporaire pour tester les restrictions
int pu = dsu.find(u);
int pv = dsu.find(v);
dsu.union(pu, pv);

booléen ok = vrai;
pour (int[] r : restrictions) {
int a = dsu.find(r[0]);
int b = dsu.find(r[1]);
si a) b) { // restriction serait violée
ok = faux;
pause;
}
}

Si (!ok) {
// retour: annuler l'union en recréant le DSU
// (depuis n ≤ 1000, nous pouvons le reconstruire à moindre coût)
dsu = nouveau DSU(n);
pour (int k = 0; k < i; k++) dsu.union(demandes[k][0], requêtes[k][1];
résultat[i] = faux;
} autre {
résultat[i] = vrai;
}
}
le résultat du retour;
}
}
«» "

> **Note** – Dans le code Java ci-dessus nous reconstruisons le DSU sur le rejet parce qu'un vrai retour en arrière est difficile.
> Pour le problème de petites limites c'est parfaitement bien; pour des limites plus grandes, vous garderiez une pile d'historique et retourneriez l'union.

---

#### 4.2 Python (effacement et idiomatique)

'`python
de taper l'importation Liste

Classe DSU:
def __init_(self, n: int):
auto-parent = liste(range(n))
Self.rank = [0] * n

def find(self, x: int) -> Int:
si soi-même. parent[x] != x:
Self.parent[x] = self.find(self.parent[x]) # compression du chemin
Revenez vous-même. parent[x]

def union(self, a: int, b: int) -> Aucun:
a, b = self.find(a), self.find(b)
si a == b: retour
si self.rank[a] < self.rank[b]:
[a] = b
elif self.rank[a] > self.rank[b]:
[b] = a
Sinon:
[b] = a
Self.rank[a] += 1

Solution de classe:
def amiDemandes(
soi-même,
n: int,
restrictions: Liste[Liste[int]],
demandes : Liste[Liste[int]]
-> Liste [bool]:
res = [Faux] * len(demandes)
dsu = DSU(n)

pour i, (u, v) en énumération (demandes):
Déjà amis
si dsu.find(u) == dsu.find(v):
res[i] = Vrai
poursuivre

# Essayez de fusionner et valider les restrictions
dsu.union(u, v)
ok = Vrai
pour a, b dans les restrictions:
si dsu.find(a) == dsu.find(b):
ok = Faux
pause

si ce n'est pas ok: # retour en arrière en reconstruisant DSU
dsu = DSU(n)
pour j dans la plage i:
dsu.union(*demandes[j])
res[i] = Faux
Sinon:
res[i] = Vrai

retour res
«» "

---

### 4.3 C++ (Fast & Modern)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

struct DSU {
vecteur <int> parent, rnk;
DSU(int n = 0) { init(n); }
vide init(int n) {
parent.resize(n);
l'attribution de rnk.(n, 0);
(parent.begin(), parent.end(), 0);
}
int find(int x) {
retour parent[x] == x ? x : parent[x] = find(parent[x]); // compression du chemin
}
vide unit(int a, int b) {
a = find(a); b = find(b);
si a) b) retour;
si (rnk[a] < rnk[b]) parent[a] = b;
sinon si (rnk[a] > rnk[b]) parent[b] = a;
autres { parent[b] = a; ++rnk[a]; }
}
};

solution de classe {
public:
vector<bool> amiDemandes(int n,
le vecteur const<vector<int>> et les restrictions,
Const vector<vector<int>& requests) {
vector<bool> ans(requests.size(), false);
DSU dsu(n);

pour (int i = 0; i < (int)requests.size(); ++i) {
int u = demandes[i][0];
int v = requêtes[i][1];

si (dsu.find(u) == dsu.find(v)) { // déjà amis
ans[i] = vrai;
poursuivre;
}

dsu.unite(u, v); // fusion provisoire
bool ok = true;
pour (auto &p : restrictions) {
si (dsu.find(p[0]) == dsu.find(p[1])) { // restriction violée
ok = faux;
pause;
}
}

si (!ok) { // retour en arrière en reconstruisant DSU
dsu.init(n);
pour (int j = 0; j < i; ++j)
dsu.unite(demandes[j][0], demandes[j][1]);
ans[i] = faux;
Autre
ans[i] = vrai;
}
le retour des an;
}
};
«» "

Autres **Pourquoi reconstruire en retour? * *
> Pour les contraintes données reconstruction est bon marché (`O(n)`), mais si vous voulez un vrai retour, vous gardez une pile de paires qui ont été fusionnées et inverser l'opération.

---

- Oui. 5. Bon – Mauvais – Ugly de l'approche du DSU

Qu'est-ce qu'il y a ?
-- -- -- -- -- -- -- --------------------------------------------------------------------------------------------------
**Simplicité**=Cartographie claire des cercles d'amis aux composants du DSU=Il faut encore scanner les restrictions pour chaque demande==Reconstruire le DSU sur le rejet se sent ==hacky=– vous perdez la vraie sémantique==
**Scalabilité**= Fonctionne pour `n, q, r ≤ 106` si vous remplacez le scan de restriction linéaire par un jeu de hachages de paires interdites== Le scan de restriction linéaire devient un goulot d'étranglement à 106== La compression à elle seule n'empêche pas la violation de la restriction - vous avez toujours besoin du scan===
**Edge-cases** Si une paire de restrictions est déjà violée avant toute requête (entrée contradictoire) – l'algorithme rejette simplement toutes les requêtes pertinentes.

---

- Oui. 6. Liste de vérification de l'entrevue

Pourquoi ça compte dans une interview technique
-- -- -- -- -- -- ----------------------------------
**Utilisez DSU** – montre que vous connaissez une structure de données classique et que vous pouvez l'appliquer à un problème de connectivité. Autres
**Expliquez l'astuce de la fusion hypothétique** – beaucoup de candidats sont coincés sur la façon de tester les restrictions. Autres
**Discuss runback** – démontrer que le syndicat-find ne soutient pas naturellement l'annulation, et expliquer la stratégie de reconstruction-comme retour (ou l'annulation basée sur la pile pour des données plus grandes). Autres
**Analyze complexité** – montrer que vous pouvez raisonner sur l'amortissement `α(n)` et pourquoi la solution est assez rapide. Autres
**Optimisations du potentiel de concentration** – par exemple, cartographier chaque restriction à un ensemble de voisins, ou stocker les paires de valeurs interdites dans un hachage pour O(1) après une fusion. Autres

---

- Oui. 7. Réflexions finales et prochaines étapes

- **Good** – Le DSU donne une solution claire et quasi linéaire qui s'écaille bien.
- **Bad** – La technique de reconstruction sur renvoi est une solution de rechange; un système réel aurait besoin d'une pile correcte.
- **Ugly** – Scanner toutes les restrictions pour chaque demande est simple, mais peut devenir un point chaud si les contraintes augmentent à 105.
→ *Astuce d'optimisation :* conserver pour chaque composant l'ensemble de partenaires restreints ; lors de la fusion, vérifier rapidement si l'intersection n'est pas vide.

---

- Oui. 8. SEO-Optimized Blog Post

Ci-dessous est un article poli que vous pouvez déposer sur votre GitHub README, blog, ou LinkedIn pour présenter vos côtelettes algorithmiques.

---

# Demandes d'amis restreints – Leetcode 2076
*Une solution de recherche syndicale qui est parfaite pour votre prochaine entrevue technique. *

---

Table des matières
1. [Ce que vous apprendrez]
2. [Le problème en un coup d'oeil] (#le problème en un coup d'œil)
3. [Pourquoi Union-Find Rocks](#Why-union-find-rocks)
4. [De Pseudocode au code de préparation à la production] (#from-pseudocode-to-production-ready-code)
5. [Complexité et performance](#complexité-performance)
6. [Manipulation d'une cornière] (#manipulation d'une cornière)
7. [Optimisations pour les entrées plus importantes] (#optimisations pour les entrées plus grandes)
8. [Puggets d'entrevue](#Puggets d'entrevue)
9. [Remplissage](#Remplissage)

---

- Oui. 1. Ce que vous apprendrez

- **Union‐Find (Disjoint Set Union)** – la structure de données pour les problèmes de connectivité.
- Comment gérer ** contraintes de paires restreintes** tout en fusionnant des composants.
- Code en **Java, Python et C++** – prêt pour une soumission de Leetcode ou une interview technique.
- Une explication prête à l'emploi qui met en lumière votre pensée algorithmique** et votre qualité de code**.

---

- Oui. 2. Le problème en bref

«» "
n = 5
restrictions = [[0, 1], [2, 3]]
demandes = [[0, 2], [1, 3], [0, 4]]
«» "

*Procéder à chaque demande dans l'ordre, mais ne jamais permettre à une paire restreinte de partager un composant. *

Produit: `[vrai, faux, vrai]`.

---

- Oui. 3. Pourquoi Union-Find Rocks

- **Demandes de composants rapides** : `find(x)` vous dit si deux personnes sont déjà connectées.
- **Temps O(α(n)** amorti pour «union» et «find».
- **Reversement propre**: Au rejet, vous pouvez reconstruire le DSU à partir de zéro (les limites sont petites).

> **Connaissance clé** – *Une restriction est violée si ses deux paramètres finissent dans le même DSU après une fusion. *

---

- Oui. 4. Du Pseudocode au code de préparation à la production

#### 4.1 Java

"Java
solution de classe publique {
// -------- Le Mémorandum d'accord...
classe statique privée DSU {
[] p, r;
DSU(int n){ p=new int[n]; r=new int[n]; pour(int i=0;i<n;i++) p[i]=i;}
int find(int x){ retourner p[x]==x?x:p[x]=find(p[x]);}
Union nulle(int a,int b){
a=find(a); b=find(b);
ia==b) retour;
si(r[a]<r[b]) p[a]=b;
autres si(r[a]>r[b]) p[b]=a;
autres{ p[b]=a; r[a]++; }
}
}

public booléen[] amiDemandes(int n, int[][] restrictions, int[][] demandes){
int q=demandes. longueur;
booléen[] ans=nouveau booléen[q];
DSU dsu=nouveau DSU(n);

pour(int i=0;i<q;i++){
u=demandes[i][0], v=demandes[i ][1];

if(dsu.find(u)==dsu.find(v)){ ans[i]=true; continuer; }

// Fusion provisoire
dsu.union(u,v);
booléen ok=true;
pour(int[] r: restrictions) {
if(dsu.find(r[0])==dsu.find(r[1]){ ok=false; break; }
}

if(!ok){ // retour: reconstruire le DSU
dsu=nouveau DSU(n);
pour(int j=0;j<i;j++) dsu.union(demandes[j][0],demandes[j][1];
[i]=faux;
} sinon ans[i]=true;
}
le retour des an;
}
}
«» "

4.2 Python

'`python
Classe DSU:
def __init_(self,n): self.p=list(range(n)); self.r=[0]*n
def find(self,x): retourner x si self.p[x]==x autre self._set(x,self.find(self.p[x])
def _set(self,x,val): self.p[x]=val; return val
def union(self,a,b):
a,b=self.find(a),self.find(b)
si a==b: retour
si self.r[a]<self.r[b]: self.p[a]= b
elif self.r[a]>self.r[b]: self.p[b]=a
Autre: self.p[b]=a; self.r[a]+=1

Solution de classe:
def amiDemandes(auto,n,restrictions,demandes):
ans=[Faux]*len(demandes)
dsu=DSU(n)
pour i,(u,v) en énumération(demandes):
Si dsu.find(u)== dsu.find(v):
[i]=Vrai; continuer
dsu.union(u,v)
ok=Vrai
pour a,b dans les restrictions:
si dsu.find(a)== dsu.find(b): ok=False; casser
si ce n'est pas bien:
dsu=DSU(n)
pour j dans la plage(i): dsu.union(*demandes[j])
ans[i]=Faux
sinon: ans[i]=Vrai
retour et
«» "

### 4.3 C++

'`cpp
classe DSU{
vecteur <int> p,r;
public:
DSU(int n){ p.resize(n); r.assign(n,0); iota(p.begin(),p.end(),0);}
int find(int x){ retourner p[x]==x?x:p[x]=find(p[x]);}
vide unit(int a,int b){
a=find(a); b=find(b);
si a==b)retour;
si(r[a]<r[b]) p[a]=b;
autres si(r[a]>r[b]) p[b]=a;
autres{ p[b]=a; r[a]++; }
}
};

Solution de classe{
public:
vector<bool> amiDemandes(int n,
le vecteur const<vector<int>> et les restrictions,
Const vector<vector<int>>& requests){
vecteur<bool> ans(requests.size());
DSU dsu(n);
pour(int i=0;i<(int)requests.size();++i) {
int u=demandes[i][0],v=demandes[i][1];
if(dsu.find(u)==dsu.find(v)){ ans[i]=true; continuer; }
dsu.unite(u,v);
bool ok=true;
pour(auto &p:restrictions)
if(dsu.find(p[0])==dsu.find(p[1]){ ok=false; break; }
if(!ok){ dsu=DSU(n);
pour(int j=0;j<i;j++) dsu.unite(demandes[j][0],demandes[j][1];
[i]=faux; }
autrement ans[i]=true;
}
le retour des an;
}
};
«» "

---

- Oui. 5. Complexité et performance

Opération Temps Espace
- C'est quoi ?
O(α(n))
O(α(n))
Restriction par fusion O(r)
Algorithme complet O(q + r) · α(n))

Avec **α(n) ≤ 4** même pour `n = 106`, l'algorithme tourne en quelques millisecondes sur le matériel moderne.

---

- Oui. 6. Traitement des cas en coin

Introduction Comportement attendu
-- -- -- -- -- -- -- -- --
Autres Paire restreinte déjà connectée (`restrictions = [0,1]`, `demandes = [0,1]`) Rejet – sortie « faux ». Autres
Requêtes dupliquées Chaque vérification gérée de manière indépendante, déjà connectée, ne garantit aucun travail supplémentaire. Autres
Autres Toutes les demandes réussissent – le DSU se réduit au classique ami‐graphe. Autres

---

- Oui. 7. Optimisations pour les entrées plus grandes

1. ** Ensemble de partenaires interdits** par composant.
2. Lors de la fusion, calculer `intersection=partnersA partenaires B`; si non-vide → rejeter.
3. Utiliser **Union by Rank** + **Compression des feuilles** pour garder la profondeur des arbres peu profonde.

---

- Oui. 8. Les pépites d'entrevue

- ** Expliquez le "Why" avant le "how"**: Commencez par décrire le graphique de connectivité, puis apportez le DSU.
- **Rollback**: Reconnaître que le syndicat-fin n'est pas non-friendly; discuter soit des options de reconstruction-ou-stack-undo.
- **Recours dans l'espace temporel**: Montrez que vous pouvez passer d'un scan de restriction linéaire à un jeu de hachage si les contraintes augmentent.
- **Tests**: Fournir des tests unitaires pour les scénarios déjà connectés et de violation de restriction.

---

- Oui. 9. Enveloppage

Vous avez maintenant :

- Une solution de DSU ** concise et lisible** en trois langues principales**.
- Une explication claire de la façon de ** respecter les restrictions** tout en fusionnant des composants.
- Des points de discussion prêts à l'entrevue qui démontrent **la maîtrise de la structure des données** et **l'analyse de complexité**.

Déposez cet article dans votre portfolio, utilisez-le pour impressionner les gestionnaires d'embauche, ou simplement pour s'amuser – vos amis vous remercieront pour avoir démystifié un problème délicat de Leetcode!

---

Autres **Codage heureux et bonne chance lors de votre prochain entretien technique!**

---

*Sentez libre de commenter ci-dessous ou ouvrez un PR si vous remarquez des améliorations. Laissez passer la conversation algorithmique ! *

---

*Tags: #Leetcode #2076 #UnionFind #DisjointSetUnion #AlgorithmDesign #Java #Python #C++ #TechnicalInterview*

---

Et c'est ça ! Vous êtes tous prêts à démontrer que vous pouvez ** résoudre** et ** expliquer** le problème *Process Restricted Friend Requests* comme un pro. Joyeux entretien 