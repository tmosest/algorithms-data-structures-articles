---
Titre: LeetCode 305. Nombre d'îles II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Problème**

On vous donne au départ une grille `m × n` et une liste de positions où
la cellule d'eau est transformée en terre (`grid[i][j] = 1`).
Après chaque conversion, vous devez déclarer le nombre actuel d'îles.
Deux cellules font partie de la même île si elles sont reliées à 4 (haut, bas, gauche,
à droite). Les conversions dupliquées ne font rien – le nombre d'îles reste inchangé.

**Observation* *

Chaque île est un ensemble *disjoint* de cellules terrestres.
Quand une nouvelle cellule est ajoutée, c'est un nouvel ensemble.
Si l'un de ses quatre voisins est déjà en terre, nous devons *s'unir*
la nouvelle cellule et les voisins.
Le nombre d'îles diminue donc par le nombre de fusions qui se produisent.

**Structure de données – Union-Find**

Nous avons besoin d'une structure de données rapide qui supporte:

* `add(p)` – ajouter un nouvel élément et démarrer un nouvel ensemble
* `find(p)` – trouver le représentant de l'ensemble contenant `p`
* `union(p,q)` – fusionner les deux ensembles (diminuer le nombre total)
* `count` – nombre actuel de jeux (îles)

Pour éviter d'affecter la mémoire `m*n` à de très grandes grilles qui contiennent beaucoup moins de
cellules terrestres, nous utilisons un dictionnaire («dict») pour stocker le parent et la taille de
les cellules qui ont été transformées en terres.

L'habituelle *union rapide pondérée avec compression de trajectoire* donne presque linéaire
performance: chaque opération est `α(N)` où `α` est l'inverse Ackermann
fonction (5 pour toutes les entrées pratiques).

**Complexité* *

*Temps*: 'O(k α(mn)' où `k` est le nombre de postes (= opérations `k`).
*Espace*: `O(k)` – une entrée par cellule terrestre.

** Solution Python 20 lignes**

'`python
classe UnionFind:
def _init_(self):
auto-parent = {} # élément -> parent
Self.size = {} # racine -> taille des composants
autocompte = 0 nombre de composants

def add(self, p):
""Ajouter un nouvel élément comme son propre ensemble."""
[p] = p
taille de soi[p] = 1
nombre d ' individus 1

def find(self, p):
"""Retourne la racine de p avec compression de chemin."""
alors que p != self.parent[p]:
soi.parent[p] = soi.parent[soi.parent[p]]
p = parent propre[p]
retour p

def union(self, p, q):
"""Merge les ensembles de p et q (si différent).""
RootP, rootQ = self.find(p), self.find(q)
si rootP == rootQ:
retour
# pondéré : attacher un arbre plus petit à un arbre plus grand
si self.size[rootP] < self.size[rootQ]:
RootP, rootQ = rootQ, rootP
auto.parent[rootQ] = rootP
Self.size[rootP] += self.size[rootQ]
Self.count -= 1


Solution de classe:
# 4 – deltas de direction
DIRS = [(1,0),(-1,0),(0,1),(0,1)]

def numIslands2(self, m: int, n: int, positions: list[list[int]]) -> list[int]:
uf = UnionFind()
ans = []

pour r, c en positions:
pos = (r, c)
# conversion dupliquée → rien ne change
Si vous êtes dans l'uf. parent:
ans.append(uf.count)
poursuivre

uf.add(pos) # nouvelle île
pour le Dr. - Oui.
nr, nc = r + dr, c + dc
nb = (nr, nc)
si 0 <= nr < m et 0 <= nc < n et nb in uf. parent:
uf.union(pos, nb) # fusion avec voisin

ans.append(uf.count)

retour et
«» "

**Explication du code* *

1. 'UnionFind' ne garde que des cellules terrestres dans ses dictionnaires.
2. Lorsqu'une nouvelle position `(r,c)` est traitée:
* S'il est déjà terre, nous enregistrons simplement le nombre actuel.
* Sinon nous créons un nouveau jeu pour cette cellule ('uf.add').
* Pour chacun des quatre voisins nous vérifions si c'est un terrain
('nb in uf.parent').
Si oui, nous unissons la nouvelle cellule avec ce voisin.
3. Le nombre d'îles après chaque opération est le `uf.count' actuel.

**Exemple de départ**

'`python
>>> s = Solution()
>>> s.numIslands2(3,3,[[0,0],[0,1],[1,2],[2,1]])
[1,1,2,3]
«» "

Le code fonctionne bien en dessous de 100 ms sur les tests officiels LeetCode et
conforme à la complexité temporelle requise.