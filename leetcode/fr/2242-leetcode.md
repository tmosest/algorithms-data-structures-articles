---
titre: LeetCode 2242. Score maximal d'une séquence de nœuds -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes – LeetCode 2242
**Score maximal d'une séquence de nœuds**

> *On vous donne un graphique non dirigé avec des nœuds `n` (0-basé).
> Chaque noeud `i` a un score `scores[i]`.
> Une séquence *de nœud valide* de longueur 4 satisfait: *
> 1. chaque paire de nœuds consécutifs est connectée par un bord
> 2. aucun nœud n'apparaît deux fois
>
> Retourne la somme maximale possible des quatre scores.
> Si aucune séquence valide n'existe, retourner `‐1`. *

«4 ≤ n ≤ 5·104», «longueur des longeurs ≤ 5·104», «1 ≤ scores[i] ≤ 108».

---

- Oui. 2. Le Bien, le Mal et l'Ugly de la Force Brute

**Méthode**
C'est pas vrai.
Récapitulez chaque marche de 4 nœuds. Facile à mettre en œuvre.
DFS avec taille Réduit la branchement Toujours exponentielle dans le pire des cas
Programmation dynamique sur sous-ensembles

Les trois approches sont soit trop lentes, soit trop ennuyeuses. La clé d'une solution acceptée est d'éviter d'explorer tout l'espace de recherche**.

---

- Oui. 3. Insight – Ne conserver que les 3 principaux voisins

Considérez un bord `(u, v)`.
Si nous cherchons une séquence de 4 nœuds `a – u – v – b`, alors:

* `a` doit être un voisin de `u` (différent de `v`).
* `b` doit être un voisin de `v` (différent de `u`).

Pour maximiser le score total, nous n'avons jamais besoin de coupler `u` avec ses **trois voisins les plus importants**, et de même pour `v`.
Pourquoi *trois*?
Parce que les deux autres nœuds de la séquence sont `a` et `b`.
Si nous gardons les trois meilleurs voisins pour chaque nœud, nous garantissons qu'au moins l'un d'eux sera distinct de l'autre voisin et de `u` ou `v` lui-même.
(Si un nœud a moins de trois voisins, nous les gardons tous.)

Ainsi l'algorithme devient:

1. Construire des listes d'adjacence.
2. Pour chaque nœud, conservez les indices de ses 3 principaux voisins (par score).
3. Pour chaque bord `(u, v)` itérer sur les 3 premiers voisins de `u` et `v`.
* Passez des indices en double ou quand un voisin est égal à l'autre paramètre.
* Calculez la note `scores[u] + scores[v] + scores[a] + scores[b]`.
* Gardez le maximum.

Le travail est `O(n + m + 9m)` ↓ `O(n + m)` (la constante 9 vient de 3 × 3 contrôles par bord), facilement adapté aux contraintes.

---

- Oui. 4. Analyse de la complexité

**Métrique**
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
Temps "O(n + m)" Autres
Espace "O(n + m)" "O(n + m)" Autres

Tant le temps que l'espace sont linéaires dans la taille des entrées – la complexité asymptotique optimale pour ce problème.

---

- Oui. 5. Mise en œuvre du code

Ci-dessous, vous trouverez un code propre et prêt à la production en **Java, Python et C++** qui suit la stratégie de voisinage supérieure.

#### 5.1 Java (Java 17)

"Java
Importation de java.util.*;

solution de classe publique {
Int maximum Score(int[] scores, int[][] bords) {
int n = scores.longueur;
// Créer des listes d'adjacence et garder les 3 premiers voisins par noeud
Liste<int[]>[] top = nouvelle liste de distribution[n];
pour (int i = 0; i < n; i++) top[i] = new ArrayList<>();

// min‐heaps temporaires pour garder les 3 meilleurs scores
Liste<PriorityQueue<int[]>> pq = nouvelle liste d'array<>(n);
pour (int i = 0; i < n; i++) {
pq.add(new PriorityQueue<>(Comparator.comparingInt(a -> a[1])); // min-heap sur la note
}

// Entaches
pour (int[] e : bords) {
u = e[0], v = e[1];
pq.get(u).offre(nouvelle int[]{v, scores[v]});
pq.get(v).offre(nouvelle int[]{u, scores[u]});
si (pq.get(u).size() > 3) pq.get(u).poll();
si (pq.get(v).size() > 3) pq.get(v).poll();
}

// extraire les 3 principaux voisins
pour (int i = 0; i < n; i++) {
pendant que [!pq.get(i).isEmpty()] {
haut[i].add(pq.get(i).poll());
}
// inverser pour avoir le score le plus élevé en premier (facultatif)
Collections.reverse(top[i]);
}

int best = -1;
pour (int[] e : bords) {
u = e[0], v = e[1];
pour (int[] a : top[u]) {
aIdx = a[0];
si (aIdx == v) continuer;
pour (int[] b : haut[v]) {
int bIdx = b[0];
si (bIdx) continue;
score int = scores[u] + scores[v] + scores[aIdx] + scores[bIdx];
best = Math.max(best, score);
}
}
}
le meilleur retour;
}
}
«» "

#### 5.2 Python (Python 3.10)

'`python
importation heapq
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def maximum Score(self, scores: List[int], bords: List[List[int]]) -> Int:
n = len(scores)

# Min-heaps pour chaque nœud pour garder les 3 meilleurs scores
geap = [] pour _ dans l'intervalle(n) ]

pour u, v dans les bords:
heapq.heappush(heap[u], (scores[v], v))
heapq.heappush(heap[v], (scores[u], u))
si len[u] > 3: heapq.heappop(heap[u])
si len(heap[v]) > 3: heapq.heappop(heap[v])

# Convertir en listes triées par score décroissant
haut = [trié(h, inverse=True) pour h dans le tas]

meilleure = -1
pour u, v dans les bords:
pour s_a, a en haut[u]:
si a == v: continuer
pour s_b, b en haut[v]:
si b == u ou b == a: continuer
best = max(meilleur, scores[u] + scores[v] + scores[a] + scores[b])

le meilleur retour
«» "

### 5.3 C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int maximum Score(vecteur<int>& scores, vecteur<vecteur<int>>& bords) {
int n = scores.size();
vecteur<array<int, 3>> haut(n); // indices des 3 principaux voisins
vector<vector<int>> topSize(n, {}); // taille réelle par noeud

// Min‐heaps (core, voisin)
vectorielle<priority_queue<pair<int,int>, vectorielle<pair<int,int>>, plus grande<>>> minHeap(n);
pour (auto& e : bords) {
u = e[0], v = e[1];
minHeap[u].push({scores[v], v});
minHeap[v].push({scores[u], u});
si (minHeap[u].size() > 3) minHeap[u].pop();
si (minHeap[v].size() > 3) minHeap[v].pop();
}

// Extraire les 3 principaux voisins pour chaque noeud
pour (int i = 0; i < n; ++i) {
vecteur<pair<int,int>> tmp;
pendant que (!minHeap[i].vide()) {
le nom de l'autorité compétente,
l'annexe II est modifiée comme suit:
}
// tmp a maintenant des voisins dans l'ordre des scores
inverse(tmp.begin(), tmp.end()); // descendant
pour (auto& p : tmp) {
topSize[i].push_back(p.seconde);
}
}

int best = -1;
pour (auto& e : bords) {
u = e[0], v = e[1];
pour (int a : topSize[u]) {
si a) v) se poursuit;
pour (int b : topSize[v]) {
si (b) (u) (a) continuer;
best = max(meilleur, scores[u] + scores[v] + scores[a] + scores[b]);
}
}
}
le meilleur retour;
}
};
«» "

> **Pourquoi le code C++ est-il sûr pour les grandes entrées? **
> `vecteur<array<int,3>>` garde exactement trois voisins par nœud – pas d'allocation dynamique pendant la boucle principale.
> `priority_queue` est un tas d'opérations `O(log 3)`, c'est-à-dire un temps constant.

---

- Oui. 6. Article de blog – Code de Leet 2242 : 3-Algorithme graphique voisin

#### 6.1 Titre (SEO‐first)

> **LeetCode 2242 – Score maximum Node Sequence – Java, Python & C++ Solution graphique pour réussir l'entrevue**

### 6.2 Méta-Description

> Apprenez comment résoudre LeetCode 2242 dans le temps O(n+m).
> Obtenez le code Java, Python et C++ propre, ainsi qu'une plongée profonde dans le top‐3 voisin.
> Parfait pour toute personne se préparant à des entrevues d'ingénierie logicielle ou à une affectation graphique.

Article

«» "
# LeetCode 2242: Score maximum d'une séquence de nœuds – Un graphique prêt à l'emploi

Lorsque vous regardez un problème de LeetCode qui ressemble à *graph-heavy*, il est tentant de penser que la force brute est la seule façon.
Mais pour **Score maximum d'une séquence de nœud** (problème 2242) l'astuce optimale est *petite* – **garder les 3 meilleurs voisins**.

Pourquoi avons-nous besoin du top 3 ?
Parce que tout chemin de 4 nœuds `a‐u‐v‐b` ne concerne que deux voisins: `a` (pour `u`) et `b` (pour `v`).
Si nous gardons les trois meilleurs voisins pour chaque nœud, nous sommes garantis de capturer le meilleur possible `a` et `b` sans jamais regarder le graphique entier.

Voici la stratégie 3 lignes :

1. Construire des listes d'adjacence.
2. Pour chaque noeud, conservez des indices de ses trois voisins les plus importants**.
3. Pour chaque bord `(u,v)` vérifier les 3×3 paires de ces voisins, sauter duplicata, calculer le score et se rappeler le maximum.

L'algorithme est `O(n+m)` – temps linéaire et mémoire, ce qui est parfait pour les limites (nœuds `5·104`, bords `5·104`).

- Oui. 1. Code – Java

"Java
// Solution Java 17 (voir le code complet dans la section réponses)
Int maximum Score(int[] scores, int[][] bords) { ... }
«» "

- Oui. 2. Code – Python

'`python
# Solution Python 3.10 (voir le code complet dans la section réponses)
Solution de classe:
def maximum Score(self, scores: List[int], bords: List[List[int]]) -> int: ...
«» "

- Oui. 3. Code – C++

'`cpp
// C++17 solution (voir le code complet dans la section réponse)
solution de classe { public: int maxScore(vector<int>& scores, vector<vector<int>>& bords) { ... } };
«» "

- Oui. 4. Pourquoi cela gagne des entrevues

* **Simplicité** – L'algorithme se résume à deux boucles : une à des voisins préprocédés, une à des bords de contrôle.
* **Scalabilité** – La complexité linéaire garantit que même les plus grands cas d'essai se terminent en millisecondes.
* **Portabilité** – La même logique fonctionne en Java, Python et C++ – idéal pour un portefeuille d'entrevues de codage.

Ajouter les extraits de code ci-dessus à votre repo GitHub, les marquer avec `leetcode-2242`, `graph-algorithm`, `top-3-voix`, et vous aurez une solution prête à passer pour la prochaine interview.

---

- Oui. 7. Pensées finales – La partie "Ugly"

Alors que le top‐3 est élégant, vous devez toujours être prudent sur:

* Les nœuds avec **moins que trois voisins** – tout simplement les garder tous.
* **Indice du double** – `a` peut être égal `b`, ou un voisin pourrait être l'autre paramètre du bord.
* Débordement entier en Java ou en C++ (utiliser `long`/`long` pour résumer quatre 108 scores).

Si vous sautez ces détails, vous obtiendrez de mauvaises réponses sur les tests cachés.

---

### TL;DR

*Le problème 2242 est résolu en temps linéaire en ne conservant que les trois premiers voisins de chaque noeud.
La solution est disponible en Java, Python et C++ – copier-coller dans votre profil LeetCode ou votre carnet d'entretien. *

---

Liens rapides

Code de la langue
C'est quoi, ça ?
JAJO <details><sommaire> Cliquez pour agrandir</résumé>... (code Java)</details> Autres
Python : <détails><résumé> Cliquez pour agrandir</résumé>... (code Python)</details> Autres
C++=Détails><résumé> Cliquez pour agrandir</résumé>... (code C++)</details> Autres

*(Remplacez la source complète ci-dessus.) *

Bon codage, et que ce top‐3 voisin vous lance ce prochain rôle d'ingénierie logicielle!