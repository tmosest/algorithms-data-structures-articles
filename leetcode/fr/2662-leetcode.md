---
titre: LeetCode 2662. Coût minimum d'un sentier avec des routes spéciales -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Idée de solution**

Pour deux points `p1` et `p2` nous pouvons toujours marcher par la grille et le coût est leur distance Manhattan

«» "
Dist(p1,p2) ==x1-x2=2 +=y1-y2=
«» "

Une *route spéciale* `(a,b,c,d,w)` nous donne un raccourci *dirigé* de `(a,b)` à `(c,d)` avec coût `w`.
Si `w` n'est pas moins cher que la distance normale de Manhattan nous n'utiliserons jamais cette route - nous pouvons simplement marcher directement.

Le problème est donc un problème le plus court sur un graphique:

* ** Vertices** – toutes les coordonnées distinctes qui apparaissent :
* point de départ
* point cible
* chaque `a,b` et `c,d` de toutes les routes spéciales

Que le nombre total de sommets soit `N` (`N ≤ 2 + 2·k`, `k ≤ 100`).

* **Edges**
* Pour chaque paire de vertices `u , v` ajouter un bord non dirigé avec le poids `dist(u,v)` (marche en réseau).
* Pour chaque route spéciale ajouter un bord dirigé de son début à sa fin avec le poids `w`.

Maintenant la réponse est simplement la longueur du chemin le plus court du vertex de départ au vertex cible.
Parce que le graphique est dense (Arêtes `N2`) nous pouvons exécuter **Dijkstra** directement sur elle – sa complexité
`O(N2 log N)` est plus que assez rapide pour `N ≤ 202`.

---

Algorithme
1. **Collecter tous les sommets**
Cartez chaque coordonnée unique sur un id entier.
2. **Précalculer toutes les distances de Manhattan**
`mdist[i][j] ===x_i-x_j=+=y_i-y_j=`.
3. **Listes d'adjacence construites**
* Pour chaque paire `i < j` ajouter le bord non dirigé `(i,j)` avec le poids `mdist[i][j]`.
* Pour chaque route spéciale `(a,b,c,d,w)` ajouter un bord dirigé de id(a,b) à id(c,d) avec le poids `w`.
4. **Run Dijkstra** depuis le sommet de départ.
5. Retourne la distance trouvée dans le vertex cible.

---

Preuve d'exactitude

Nous prouvons que l'algorithme renvoie le coût de voyage minimum possible.

**Lemme 1**
Pour les deux sommets `u` et `v` le graphique contient un bord de poids égal au minimum
le coût éventuel du déplacement de `u` à `v` en utilisant uniquement les déplacements normaux de la grille.

*Proof. *
Par construction nous avons ajouté un bord non dirigé entre chaque paire de sommets avec le poids
`=x_u-x_v== +=y_u-y_v==`. C'est exactement la distance de Manhattan, qui est le coût minimum
marcher entre `u` et `v` sans utiliser une route spéciale. *



**Lemme 2**
Pour toute route spéciale `(a,b)->(c,d,w)` le graphique contient un bord dirigé dont le poids
est égal au coût d'utilisation de cette route.

*Proof. *
Nous avons ajouté un bord dirigé de id(a,b) à id(c,d) avec le poids `w`.



**Lemme 3**
Pour toute promenade dans l'énoncé de problème original il existe un chemin dans le construit
graphique avec exactement le même coût total, et inversement.

*Proof. *
Une promenade consiste en des segments alternant de la grille de marche et (éventuellement) des routes spéciales.
* Un segment de marche entre deux sommets consécutifs 'u,v` de la marche
peut être remplacé par le bord `(u,v)` de Lemma 1 – la correspondance des coûts.
* Un segment de route spéciale est représenté par le bord dirigé correspondant de
Lemma 2 – les coûts correspondent.
Parce que nous avons inséré des bords pour *chaque* paire de sommets qui peuvent apparaître dans une promenade,
l'ensemble des cartes de marche à un chemin graphique de coût égal.
La direction inverse est triviale: n'importe quel chemin graphique se traduit de nouveau dans une promenade dans le
réglage original parce que chaque bord de graphique est réalisable soit en marchant ou par un spécial
route. *



**Lemme 4**
L'algorithme de Dijkstras retourne la longueur du chemin le plus court du graphique dès le début
à la cible.

*Proof. *
Tous les poids de bord sont non-négatifs, donc l'argument de rectitude standard pour Dijkstra s'applique. *



* Théorème *
L'algorithme produit le coût de déplacement minimum possible depuis le point de départ jusqu'à la
point cible.

*Proof. *
Par Lemma 3 l'ensemble de promenades réalisables dans le problème initial est en un à un
correspondance avec l'ensemble des chemins du graphique construit, en préservant le coût total.
Par Lemma 4 Dijkstra trouve le chemin du coût minimum dans le graphique.
Par conséquent, le coût retourné par l'algorithme équivaut à l'optimum dans le problème initial. *



---

Analyse de complexité

Que `k` soit le nombre de routes spéciales (`k ≤ 100`).
Nombre de sommets "N = 2 + 2·k ≤ 202".

* Les distances de Manhattan pré-calculées: temps "O(N2)", mémoire "O(N2)".
* Listes d'adjacence : aussi bords `O(N2)`.
* Dijkstra: `O(E log V)` avec `E = γ(N2)` → `O(N2 log N)` temps.
* Consommation de mémoire: listes d'adjacence + tableau de distance → `O(N2)`.

Avec `N ≤ 202` cela est bien en dessous des limites pour un délai de 2 s.

---

### Mise en oeuvre de la référence (Python 3)

'`python
importations
importation heapq

def resouver() -> Aucun:
données = sys.stdin.read().strip().split()
si ce n'est pas des données:
retour
it = iter(données)
sx, sy, tx, ty = map(int, (next(it), next(it), next(it), next(it))
k = int(next(it))

# recueillir toutes les coordonnées distinctes
coord_to_id = {}
Coords = []

def get_id(x, y):
si (x, y) pas dans coord_to_id :
coord_to_id[(x, y)] = len(coords)
(x, y)
retourner coord_to_id[(x, y)]

start_id = get_id(sx, sy)
cible_id = get_id(tx, ty)

special_edges = [] # (u_id, v_id, poids)
pour _ dans la plage(k):
a, b, c, d, w = map(int, (next(it), next(it), next(it), next(it), next(it))
si w < abs(a - c) + abs(b - d): # route utile seulement
u = get_id(a, b)
v = get_id(c, d)
special_edges.append(u, v, w))

n = len(coords) Nombre de sommets

# distances précalculées de Manhattan
mdist = [[0] * n pour _ dans la plage(n)]
pour i dans la plage(n):
xi, yi = coords[i]
pour j dans la plage(i + 1, n):
xj, yj = coords[j]
d = abs(xi - xj) + abs(yi - yj)
mdist[i][j] = mdist[j][i] = d

# construire des listes d'adjacence
adj = [[] pour _ dans l'intervalle(n)]
# bords de la grille (non dirigés)
pour i dans la plage(n):
pour j dans la plage(i + 1, n):
w = mdist[i][j]
Annexe(j, w)
Annexe(i, w)
# bords de route spéciaux (dirigés)
pour u, v, w en _edges spéciaux:
(v, w))

Dijkstra
INF = 10**18
dist = [INF] * n
dist[start_id] = 0
pq = [(0, start_id)]

alors que pq:
d, u = heapq.heappop(pq)
Si d != dist[u]:
poursuivre
if u == cible_id:
pause
pour v, w in adj[u]:
nd = d + w
si nd < dist[v]:
dist[v] = nd
(pq, (nd, v))

print(dist[cible_id])

si __nom__ == "__main__" :
résoudre()
«» "

**Format d'entrée* *

«» "
Sx sy ty
k
a1 b1 c1 d1 w1
...
AK bk ck dk wk
«» "

** Sortie**

«» "
coût minimum
«» "

Le programme suit exactement l'algorithme prouvé correct ci-dessus et fonctionne confortablement
dans les limites.