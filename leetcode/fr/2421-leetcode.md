---
titre: LeetCode 2421. Nombre de bonnes voies -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Python – Union – Trouver une solution pour le nombre de bonnes voies *

Le but est de compter le nombre de chemins *bons* dans un graphique non dirigé.

* Un bon chemin est un chemin simple (pas de vertex répété) dont les paramètres ont la même valeur, et la valeur maximale sur l'ensemble du chemin est égale à cette valeur.
* Chaque vertex est un bon chemin trivial – qui contribue à la réponse.

La solution classique fonctionne dans
"O( (n + m) · α(n) )" temps (`α` = fonction Ackermann inverse) et
Mémoire `O(n + m)`, où `n` est le nombre de nœuds et `m` le nombre de bords.

---

- Oui. 1. Idées

1. **Liste de proximité** – stocker le graphique comme une liste de voisins pour chaque noeud.
2. **Value → map des nœuds** – pour chaque valeur de nœuds distincts, conservez une liste de nœuds ayant cette valeur.
3. ** Valeurs du processus en ordre ascendant** –
Pour une valeur courante `v`, il suffit de fusionner des nœuds qui peuvent être connectés par un chemin qui ne contient **pas** une valeur supérieure à `v`.
Cela signifie que nous pouvons en toute sécurité un nœud avec un voisin *iff* la valeur du voisin ≤ "v".
4. **Component component** – après que tous les unions pour la valeur actuelle sont fait, regardez seulement les nœuds qui ont réellement la valeur `v`.
Compter combien d'entre eux appartiennent à chaque composant connecté (racine).
Si un composant contient de tels nœuds `k`, toutes les paires non ordonnées d'entre eux donnent des bons chemins `k·(k‐1)/2` supplémentaires.
Ajoutez-les à la réponse.
5. **Réponse initiale** – chaque nœud seul contribue à une bonne voie.
Nous commençons donc par `ans = n` et ajoutons la paire au fur et à mesure.

---

- Oui. 2. Code

'`python
de collections importer par défautdict
de taper l'importation Liste

C'est... Union‐Find (Union de l'ensemble disjoint) --------
Classe DSU:
"""
Classic DSU avec compression de chemin et union par taille.
parent[x] == x → x est une racine
taille[root] → nombre de nœuds dans le composant
"""
def __init_(self, n: int):
auto-parent = liste(range(n))
taille de soi = [1] * n

def find(self, x: int) -> Int:
"""Retourne la racine de x avec compression de chemin."""
alors que moi. parent[x] != x:
auto.parent[x] = auto.parent[self.parent[x]]
x = parent propre[x]
retour x

def union(self, a: int, b: int) -> Aucun:
"""Modifier les composants contenant a et b."""
ra, rb = self.find(a), self.find(b)
si rb:
retour
# union par taille – attacher le plus petit arbre au plus grand
si self.size[ra] < self.size[rb]:
Le nombre d'heures de travail est égal à celui des heures de travail.
auto.parent[rb] = r
self.size[ra] += self.size[rb]

C'est... Solution principale
def number_of_good_paths(vals: List[int], bords: List[List[int]]) -> Int:
"""
Comptez tous les bons chemins dans un graphique non dirigé.

Paramètres
- Oui.
Vals : Liste[int]
Valeurs du nœud. Node i a valeur vals[i].
bords : Liste[Liste[int]]
Bords non orientés, chaque bord est [u, v] (0 indices basés).

Retourne
- Oui.
Int
Le nombre total de bons chemins.
"""
n = len(vals)
1. Construire une liste d'adjacence
adj = defaultdict(list)
pour u, v dans les bords:
adj[u].appendice(v)
Annexe(u)

# 2. Valeur de la carte → liste des nœuds ayant cette valeur
val_to_nodes = defaultdict(list)
pour le noeud, la vale dans l'énumération(s):
val_to_nodes[val].append(node)

3. Préparez le DSU
dsu = DSU(n)

4. Réponse initiale : chaque nœud est un bon chemin
ans = n

5. Valeurs de processus en ordre ascendant
pour la valeur triée(val_to_nodes):
noeuds = val_to_nodes[val]

# a) Fusionner des nœuds avec des voisins de valeur <= valeur actuelle
pour noeud en noeuds:
pour nb en adj[node]:
si vals[nb] <= vals:
dsu.union(node, nb)

# b) Compter les nœuds de cette valeur à l'intérieur de chaque composant
comp_cnt = defaultdict(int)
pour noeud en noeuds:
racine = dsu.find(node)
Comp_cnt[root] += 1

# c) Chaque paire non ordonnée de tels nœuds forme un bon chemin
pour cnt en valeurs comp_cnt.():
si cnt > 1:
ans += cnt * (cnt - 1) // 2

retour et
«» "

---

- Oui. 3. Comment ça marche – une visite rapide

* **Trier les valeurs** garantit que lorsque nous traitons une valeur `v`, chaque noeud qui peut se trouver sur un bon chemin vers un autre noeud de valeur `v` a déjà été fusionné avec toutes les valeurs strictement plus petites.
* **L'union seulement avec les voisins de valeur ≤ v** conserve la condition que le maximum sur le chemin est `v`.
Tout voisin ayant une valeur `> v` violerait la règle du bon chemin et ne doit donc pas être fusionné pour cette étape.
* **Pairs de calcul par composant** – une fois les unions terminées, tous les nœuds de valeur `v` qui partagent la même racine appartiennent à un seul composant connecté qui ne contient que des nœuds ≤ `v`.
Chaque paire peut être connectée par un bon chemin, d'où le coefficient binomial.

---

- Oui. 4. Analyse de la complexité

*Liste d'attente pour la construction* – «O(n + m)»
*Valeurs uniques* – `O(k log k)`, où `k` ≤ `n "
* Traitement de chaque nœud une fois pour chacun de ses voisins* – syndicats « O(m) », chaque « α(n) » amorti
*Component de comptage* – `O(n)` sur toutes les valeurs

Temps total: **'O((n + m) · α(n)"** (essentiellement linéaire).
Consommation de mémoire: **«O(n + m)»**.

---

- Oui. 5. Exemple

'`python
si __nom__ == "__main__" :
valeurs = [1, 3, 2, 1, 3]
bords = [[0,1], [1,2], [2,3], [2,4]
print(number_of_good_paths(vals, bords)) # Sortie: 6
«» "

Les 6 bons chemins sont:

1. `[0]` (valeur 1)
2. `[1]` (valeur 3)
3. `[2]` (valeur 2)
4. `[3]` (valeur 1)
5. `[4]` (valeur 3)
6. `[1, 2, 4]` – les deux paramètres 3, le nœud intermédiaire 2 a une valeur 2 ≤ 3.

---

N'hésitez pas à déposer la fonction dans votre propre base de codes ou à l'utiliser comme référence pour la mise en œuvre du problème *Nombre de bonnes voies* dans n'importe quel environnement Python.