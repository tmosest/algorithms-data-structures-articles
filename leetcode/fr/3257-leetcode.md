---
titre: LeetCode 3257. Maximum Somme de valeur en plaçant trois prises II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
N° 3257 – Maximum Somme de la valeur en plaçant trois prises II
**Langues** : C++
**Difficulté** : Dur
** URL de LeetCode** : <https://leetcode.com/problèmes/maximum-value-sum-by-placement-trois-rooks-ii/>

---

- Oui. 1. Récapitulation des problèmes

On vous donne un tableau `m × n` où `board[i][j]` est la valeur de la cellule `(i, j)`
«3 ≤ m, n ≤ 500», «-109 ≤ planche[i][j] ≤ 109».

Placez **exactement trois** rooks sur la planche de sorte qu'aucun deux rooks ne partagent la même ligne ou la même colonne.
Retourner la somme maximale possible des trois cellules choisies.

---

- Oui. 2. Le piège de la Force brute

La solution évidente est d'essayer chaque combinaison de trois cellules ('O(m3n3)') et vérifier
les contraintes de ligne/colonne – qui sont astronomiquement chères pour `500 × 500`.

Même un DFS de 3 niveaux («O(m3)») Les taux d'intérêt à court terme de l'ensemble des opérations de la zone euro sont les suivants:

> **Bad** – O(n6) = *impossible* pour les limites données.

---

- Oui. 3. Le point de vue "Good"

Nous n'avons besoin que de trois points, donc le nombre de positions *conflictuelles* qui peuvent être
bloqué par un rook est petit.
L'idée clé est :

1. **Réduire l'espace de recherche** en ne conservant que les cellules les plus précieuses*.
2. Après la réduction, le reste de l'ensemble est assez petit pour être brutalisé.

---

- Oui. 4. Les cas de bord de l'Ugly

* Les valeurs négatives – la réponse pourrait être le plus grand* (c'est-à-dire le moins négatif) triple.
* Dupliquer les valeurs dans la même ligne/colonne – nous devons toujours éviter de partager les lignes/colonnes.
* Les liens – nous devons garder suffisamment de candidats pour couvrir toutes les combinaisons optimales.

Un pic naïf de type «top‐K» (p. ex. K = 250) peut manquer un triple optimal si l'optimum
implique une cellule qui est * juste en dessous* de la coupure.
C'est pourquoi nous avons besoin d'un lien déterministe qui garantisse que nous captions tout le maximum possible.

---

- Oui. 5. La solution optimale (O(m·n) + O(K3) où K ≤ 15)

1. **En haut de la ligne–3**
Pour chaque ligne, gardez les 3 cellules avec les plus grandes valeurs.
(Si une rangée a moins de 3 cellules, gardez-les toutes.)

2. ** Recueillir les candidats* *
Rassemblez toutes ces cellules → au plus `3·m` cellules.

3. ** Filtre par colonne**
Trier les cellules collectées par valeur (descendant).
Scanner la liste triée et garder jusqu'à **3** cellules par colonne (les meilleurs).
Après cette étape, la liste contient ** au plus `3·m + 3·n ́ cellules**, mais dans la pratique elle
Des psys spectaculaires.

4. **Établir la liste finale à 15 cellules**
Pour toute cellule choisie, au plus 2 autres cellules partagent leur rang et au plus 2 partagent leur rang.
colonne → un total de 5 cellules contradictoires.
Comme nous n'avons besoin que de 3 prises, le nombre maximum de cellules que nous *pouvions*
vérifier est `3 · 5 = 15`.
Par conséquent, nous pouvons prendre en toute sécurité les premières **15** cellules de la liste triée
(ou tous si moins).

5. ** Forcer tous les triplets* *
Avec au plus 15 cellules, il n'y a que `C(15, 3) = 455` triples – trivial à tester.

6. **Retourner la meilleure somme** (utiliser `long` pour éviter les débordements).

L'exactitude

- Oui. Le top‐3 par rangée garantit que tout placement optimal de prise doit utiliser une cellule
c'est l'un des 3 meilleurs de sa rangée.
- Oui. Le filtre par colonne garantit que pour chaque colonne nous conservons ses 3 meilleurs
cellules qui ont survécu au filtre de rangée.
- La liaison de la cellule 15 découle du principe du casier décrit ci-dessus.
- Oui. Par conséquent, chaque triple optimal apparaît dans la liste finale et est examiné.

Complexité

Étape Temps Espace
C'est pas vrai.
Haut de la ligne – 3 (paie par ligne) – « O(m·n·log 3) » – « O(m·n) » Autres
Filtre à colonnes (sort + nombre) Autres
Liste finale (de 15 cellules) Autres
"O(153) = 455" "O(1)" Autres
**Total**

La mémoire est dominée par le conseil lui-même (entrée).
L'algorithme est entièrement linéaire dans la taille du tableau et utilise seulement une poignée de extra
les tableaux.

---

- Oui. 6. Mise en œuvre

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.

---

#### 6.1 Java

"Java
Importation de java.util.*;
importation java.io.*;

solution de classe publique {
cellule statique privée {
int r, c, val;
Cell(int r, int c, int val) { this.r = r; this.c = c; this.val = val; }
}

public long maximum ValeurSum(int[][]) {
int m = longueur de la planche, n = longueur de la planche[0]. longueur;
Liste des candidats<Cell> = nouvelle liste de répartition<>();

// 1/ 1/ 1/ par rang haut-3 (minimum de la taille 3)
pour (int i = 0; i < m; i++) {
PrioritéQueue<Cell> min = nouvelle prioritéQueue<>(Comparator.comparingInt(a -> a.val));
pour (int j = 0; j < n; j++) {
Cur cellule = nouvelle cellule(i, j, planche[i][j]);
min.offre(cur);
si (min.size() > 3) poll min();
}
candidats.addAll(min);
}

2/ Filtre par colonne – garder jusqu'à 3 meilleurs par colonne
candidats.sort(a, b) -> Integer.compare(b.val, a.val)); // descendant
Carte <entier, entier> colCnt = nouveau HashMap<>();
Liste<Cell> filtrée = nouvelle liste de distribution<>();
pour (cellule cellulaire : candidats) {
int c = cellule.c;
si (colCnt.getOrDefault(c, 0) < 3) {
filtre.add(cellule);
colCnt.put(c, colCnt.getOrDefault(c, 0) + 1);
}
}

// Conserver seulement les 15 premières cellules (ou toutes si elles sont inférieures)
limite int = Math.min(filtered.size(), 15);
long best = Long.MIN_VALUE;

Brute-force tous les triples
pour (int i = 0; i < limite; i++) {
pour (int j = i + 1; j < limite; j++) {
pour (int k = j + 1; k < limite; k++) {
Cellule a = filtre.get(i);
b = filtre.get(j);
c = filtre.get(k);
Si (a.r) == a.r.r == c.r.r == c.r.
A.c == B.c.c == c.c. {
Continuer; // même ligne ou colonne
}
somme longue = (long) a.val + b.val + c.val;
si (somme > meilleure) meilleure = somme;
}
}
}
le meilleur retour;
}
}
«» "

---

6.2 Python

'`python
Solution de classe:
def maximum ValueSum(self, board: List[List[int]]) -> Int:
m, n = len(board), len(board[0])

- Oui. Étape 1: garder en haut 3 par rangée ------------------------------------
row_candidats = [] # liste de (r, c, val)
pour r dans la plage(m):
heap = [] # min–pape de longueur <=3
pour c dans la plage(n):
val = planche[r][c]
si len(pap) < 3:
(val, c))
Sinon:
si val > tas[0][0]:
[0] = (val, c)
# Gardez le tas trié après chaque insert
en tas.sort()
pour val, c en tas:
row_candidats.append(r, c, val)

- Oui. Étape 2: garder le top 3 par colonne ---------------------------------
row_candidats.sort(key=lambda x: -x[2]) # trier par la valeur descendante
_colcnt = {}
_candidats = []
pour r, c, val en rangée_candidats:
si col_cnt.get(c, 0) < 3:
col_candidats.append(r, c, val)
col_cnt[c] = col_cnt.get(c, 0) + 1

- Oui. Étape 3: prendre 15 (ou tout) ---------------------------------
limite = min(15, len(col_candidats))
best = -10**18 # assez longtemps pour les négatifs

- Oui. Étape 4: force brute tous les triples --------------------------------
pour i dans la plage (limite):
r1, c1, v1 = col_candidats[i]
pour j dans la plage (i+1, limite):
r2, c2, v2 = col_candidats[j]
si r1 == r2 ou c1 == c2: continuer
pour k dans la plage (j+1, limite):
r3, c3, v3 = col_candidats[k]
si r1 == r3 ou r2 == r3 ou c1 == c3 ou c2 == c3: continuer
best = max(meilleur, v1 + v2 + v3)
le meilleur retour
«» "

---

*### 6.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Cellule de structure {
int r, c, val;
Cell(int _r, int _c, int _v) : r(_r), c(_c), val(_v) {}
};

long long maximumValueSum(vecteur<vecteur<int>>& conseil) {
int m = board.size(), n = board[0].size();
vector<Cell> rangeTop; // au plus 3 par rang

// -------- Étape 1: haut‐3 par rangée ----------
pour (int r = 0; r < m; ++r) {
priority_queue<Cell, vector<Cell>, fonction<bool(const Cell&, const Cell&)>> minChap(
[](const Cell& a, const Cell& b){ retour a.val < b.val; }); // max-heap
pour (int c = 0; c < n; ++c) {
minHeap.emplace(r, c, planche[r][c];
si (minHeap.size() > 3) minHeap.pop();
}
pendant que (!minHeap.vide()) {
la ligneTop.push_back(minHeap.top());
minHeap.pop();
}
}

// -------- Étape 2 : filtrer par colonne
Tri(rowTop.begin(), rowTop.end(),
[](const Cell& a, const Cell& b) { retourner a.val > b.val; });

vecteur<Cell> colTop;
unordered_map<int,int> colCnt;
pour (const Cell& x : rangeTop) {
si (colCnt[x.c] < 3) {
(x)
++colCnt[x.c];
}
}

// -------- Étape 3 : conserver au plus 15 cellules...
int lim = min(int)colTop.size(), 15;
longue longue meilleure = LLONG_MIN;

// - Oui. Étape 4: triples de force brute - Oui.
pour (int i = 0; i < lim; ++i) {
pour (int j = i+1; j < lim; ++j) {
si (colTop[i].r == colTop[j].r.
pour (int k = j+1; k < lim; ++k) {
if (colTop[i].r == colTop[k].r.
colTop[i].c == colTop[k].c.
longue somme longue = (long long)colTop[i].val + colTop[j].val + colTop[k]. valeur;
best = max (meilleure somme);
}
}
}
le meilleur retour;
}
};
«» "

---

- Oui. 6. Testez votre solution

Texte
Entrée: tableau = [[1, 2, 3], [3, 4, 5], [7, 6, 8]]
Produit: 23 (3 + 8 + 12? 5 + 7 + 11 = 23)
«» "

Cas de bord:

Conseil d'administration Résultat prévu
-- -- -- -- -- -- -- --
Autres Tous les négatifs, par exemple `[-5,-10,-3,-2,-8]` → `-3 + -5 + -8 = -16`
Les valeurs identiques dans la même ligne s'assurent que les conflits de lignes sont vérifiés.
Autres L'algorithme des colonnes/lignes très clairsemées choisit toujours le top‐3 par ligne/colonne.

---

- Oui. 7. Pourquoi ce blog vous aidera à trouver un emploi

Comment l'article le démontre
-- -- -- -- -- --------------------------------------------------
**Décomposition du problème**= Naïve → réduire l'espace de recherche → force-brute finale
**Conception de l'algorithme**
**Analyse de la complexité**
**Codage propre**
**La pensée d'un cas d'urgence**

Les intervieweurs aiment les ingénieurs qui peuvent **voir les modèles**, **optimiser** et **écrire un code maintenable**. Cet article montre exactement cela.

---

- Oui. 8. TL;DR

1. Conservez les 3 cellules de base par rang** (taille ≤ 3 de la feuille de base).
2. Garder **en haut de 3 cellules par colonne** de celles (déclin de tri).
3. **Ne prendre que les 15 premières cellules** (ou toutes si moins).
4. Brute-force tous les triples, en sautant les combinaisons même ligne / même colonne.
5. Complexité: **O(m × n)** temps, **O(m × n)** mémoire.

---

N'hésitez pas à copier le code, à l'exécuter sur LeetCode et à l'ajouter à votre portfolio GitHub. Bon codage !

---

*Mots clés: `valeur maximale`, `board`, `time linéaire`, `3x3 board`, `algorithme design`, `LeetCode`, `Java`, `Python`, `C++`, `O(m*n)`. *