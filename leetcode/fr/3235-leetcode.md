---
titre: LeetCode 3235. Vérifiez si le coin rectangle est accessible -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
### Union-Find (Union mixte-Set, MSU)

Union‐Find est une structure de données très rapide qui permet de suivre une partition d'un ensemble dans **sous-ensembles disjoints (non-overlaping)**.
Vous pouvez

1. **Trouver** à quel sous-ensemble un élément appartient.
2. **Union** (fusion) deux sous-ensembles en un seul.

C'est l'épine dorsale de nombreux algorithmes : Kruskal, détection de cycle dans les graphiques, connectivité réseau, traitement d'image, etc.

---

- Oui. 1. Ce que la structure stocke

Définition
C'est quoi ?
Pour chaque élément `i`, le parent `i` dans une forêt. Si `i` est la racine d'un arbre, `parent[i] == C'est vrai.
"Rank[i]` (ou "size[i]`)" Environ la hauteur (ou la taille) de l'arbre dont la racine est "i". Utilisé pour garder les arbres peu profonds. Autres

Au départ, chaque élément est son propre ensemble :

Texte
parent[i] = i
rang[i] = 0 (ou taille[i] = 1)
«» "

Tous les ensembles sont représentés comme une forêt d'arbres.

---

- Oui. 2. Opérations

### `find(x)` – localiser l'ensemble contenant `x "

```pseudo
fonction find(x) :
si parent[x] != x:
parent[x] = trouver(parent[x]) // Compression de la trajectoire
retour du parent[x]
«» "

* Marchez régulièrement jusqu'à la racine. *
Pendant la promenade, nous **compressons le chemin**: chaque nœud visité pointe directement vers la racine.
Après une «fin», la profondeur de l'arbre devient au plus 1 pour les nœuds visités.

### `union(x, y)` – fusionner les ensembles contenant `x` et `y "

```pseudo
union de fonction(x, y):
rootX = find(x)
racineY = find(y)
if rootX == rootY: retourne // déjà dans le même ensemble

// Union par grade (ou par taille)
si rang[rootX] < rang[rootY]:
parent[rootX] = rootY
Sinon, si rang[rootX] > rang[rootY]:
parent[rootY] = rootX
Sinon:
parent[rootY] = rootX
rang[rootX] += 1
«» "

Si les rangs sont égaux, nous choisissons arbitrairement une nouvelle racine et incrémentons son rang.

---

- Oui. 3. Pourquoi c'est rapide

- Chaque `fin` fait la compression du chemin → l'arbre devient un seul niveau lors des prochaines visites.
- Chaque `union` attache le plus petit arbre sous le plus grand (par rang) → la profondeur de l'arbre reste basse.

Le temps amorti par opération est **inverse Ackermann**:
`α(n) 4` pour tous les `n` pratiques. Bref, c'est essentiellement *O(1)* pour toutes les entrées réalistes.

---

- Oui. 4. Exemple rapide

Supposons que nous ayons des éléments 0...5. Les syndicats:

«» "
union(0,1) // sets: {0,1} {2} {3} {4} {5}
union(2,3) // sets: {0,1} {2,3} {4} {5}
union(1,2) // fusionner les deux ensembles
«» "

Après ces opérations:

«» "
find(0) → racine r
trouver(5) → racine 5 (différent)
«» "

La structure après compression peut ressembler à:

«» "
parent = [r, r, r, r, 4, 5]
rang = [1, 0, 0, 0, 0]
«» "

Tous les nœuds de l'ensemble fusionné pointent maintenant directement vers `r`.

---

- Oui. 5. Cas d'utilisation courante: Kruskal.

```pseudo
Trier les bords en poids
pour chaque bord (u,v) dans l'ordre:
si find(u) != find(v):
ajouter le bord au MST
Union(u,v)
«» "

Parce que `find` indique rapidement si ajouter un bord créerait un cycle, nous pouvons construire un MST dans le temps `O(E log V)`.

---

- Oui. 6. Extraits de C++/Python

### C++ (compacte)

'`cpp
struct DSU {
vecteur <int> parent, grade;
DSU(int n=0) { init(n); }

vide init(int n){
parent.resize(n);
l'attribution de grade.(n,0);
(parent.begin(), parent.end(), 0);
}

int find(int x){
retour parent[x]==x ? x : parent[x]=find(parent[x]); // compression du chemin
}

vide unit(int a, int b){
a=find(a); b=find(b);
ia==b) retour;
swap(a,b);
parent[b]=a;
if(rank[a]==rank[b]) rang[a]++;
}
};
«» "

### Python (clair)

'`python
Classe DSU:
def __init_(self, n):
auto-parent = liste(range(n))
Self.rank = [0]*n

def find(self, x):
si soi-même. parent[x] != x:
Self.parent[x] = self.find(self.parent[x]) # compression du chemin
Revenez vous-même. parent[x]

def union(self, a, b):
a, b = self.find(a), self.find(b)
si a == b: retour
si self.rank[a] < self.rank[b]:
a, b = b, a
[b] = a
si soi-même. rang[a]== Self.ranking[b]:
Self.rank[a] += 1
«» "

---

- Oui. 7. A emporter

* Union‐Find* est une structure à temps presque constant pour maintenir une partition d'éléments dans le cadre des opérations syndicales.
Avec la compression **path** et **union par rang/taille** elle garantit l'amortissement `O(α(n)` par opération, qui est pratiquement *O(1)*.
Sa simplicité et sa vitesse le rendent indispensable dans les algorithmes graphiques et de nombreuses autres applications.