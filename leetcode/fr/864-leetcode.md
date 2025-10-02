---
titre: LeetCode 864. Voie la plus courte pour obtenir toutes les clés -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## La voie la plus courte pour obtenir toutes les clés – 864 (Code Leet)

Langue Nom du fichier Idée de clé Autres
- C'est quoi ?
**Java**= `Solution.java`= BFS + Bit-masking – état = `(ligne, col, clés)=" Autres
**Python**
*C++**= `solution.cpp`= `queue` + `unordered_set` pour les états visités==

On trouvera ci-dessous des solutions complètes prêtes à coller pour chaque langue, suivies d'un billet de blog **SEO-optimisé** qui explique le problème, l'algorithme et les conseils de style interview.

---

- Oui. 1. Java – `Solution.java "

"Java
Importation de java.util.*;

solution de classe publique {

État de la classe statique privée {
touches int; // bitmask des clés collectées
int r, c; // position actuelle

État(injecter les clés, int r, int c) {
Ça. clés = clés;
c.r = r;
c = c;
}
}

public PathAllKeys(String[] grille) {
m = quadrillage longueur, n = quadrillage[0] longueur();
Total Clés = 0;
int sr = -1, sc = -1;

// 1-
pour (int i = 0; i < m; i++) {
pour (int j = 0; j < n; j++) {
char ch = grille[i].charAt(j);
if (ch == '@') { sr = i; sc = j; }
si ('a' <= ch && ch <= 'f') totalKeys++;
}
}

int allKeysMask = (1 < < TotalKeys) - 1;
Queue<State> q = nouveau ArrayDeque<>();
Set<String> visité = nouveau HashSet<>();

q.offre(nouveau État(0, sr, sc));
visité.add(0 + " + sr + " + sc);

int[[]] dirs = {{1,0},{1,0},{0,1},{0,1}};
Étapes int = 0;

BFS
alors que (!q.isEmpty()) {
int sz = q.size();
pour (int s = 0; s < sz; s++) {
État cur = q.poll();

si (cur.keys) toutes les étapes de retourKeysMask;

pour (int[] d : dirs) {
int nr = cur.r + d[0];
int nc = cur.c + d[1];
si (nr < 0) nr >= m) continuer;

char ch = grille[nr].charAt(nc);
Si (ch == '#') continuer; // mur

int newKeys = cur.keys;
si ('a' <= ch && ch <= 'f')
newKeys= 1 << (ch - 'a'); //

Si ('A' <= ch && ch <= 'F' && (nouvelles clés >> (ch - 'A') & 1) == 0)
Continuer; // porte verrouillée

Clé de chaîne = newKeys + " + nr + " + nc;
si (visited.add(key)) { // nouvel état
q.offre(nouvel État(nouvelles clés, nr, nc));
}
}
}
étapes++;
}
retour -1; // impossible
}
}
«» "

Complexité

Heure Espace
- C'est quoi ?
**O(m · n · 2n)** où `n` ≤ 6 (clés)

---

- Oui. 2. Python – `solution.py "

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
def le plus court PathAllKeys(self, grid: List[str]) -> Int:
m, n = len(grid), len(grid[0])
_clés totaux = 0
sr = sc = -1

N° 1 Trouver le départ, compter les clés
pour r dans la plage(m):
pour c dans la plage(n):
ch = grille[r][c]
Si ch == '@':
sr, sc = r, c
elif 'a' <= ch <= 'f':
_clés totaux += 1

all_keys_mask = (1 < < total_keys) - 1
q = deque([(0, sr, sc)]) # (clés, r, c)
visité = {(0, sr, sc)}
dirs = [(1,0),(-1,0),(0,1),(0,1)]
étapes = 0

N° 2
alors que q:
pour _ dans la plage(len(q)):
touches, r, c = q.popleft()
if keys == all_keys_mask :
étapes de retour

pour dr, dc en dirs:
nr, nc = r + dr, c + dc
si non (0 <= nr < m et 0 <= nc < n): continuer
ch = grille[nr][nc]
Si ch == '#': continuer

new_keys = clés
si 'a' <= ch <= 'f':
nouvelle_keys= 1 << (ord(ch) - ord('a'))
si 'A' <= ch <= 'F' et non (new_keys >> (ord(ch) - ord('A') & 1):
poursuivre

État = (nouvelles_clés, nr, nc)
si l'état n'est pas visité:
visité.add(état)
q.appendice(état)
étapes += 1
retour -1
«» "

Complexité

- **Heure**: `O(m · n · 2n)` – au plus `O(400 · 64)` pour la grille 20×20 avec 6 touches.
- **Espace**: "O(m · n · 2n)" – États visités.

---

- Oui. 3. C++ – `solution.cpp "

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
État de structure {
touches int; // bitmask
à r, c;
État(int k, int rr, int cc) : clés(k), r(rr), c(cc) {}
};
public:
int le plus courtPathAllKeys(vecteur<string>& grille) {
int m = quadrillage(), n = quadrillage[0].size();
Total Clés = 0, sr = -1, sc = -1;

Localiser les touches de départ et de comptage
pour (int i = 0; i < m; ++i)
pour (int j = 0; j < n; ++j) {
char ch = grille[i][j];
if (ch == '@') { sr = i; sc = j; }
si ('a' <= ch && ch <= 'f') ++total Clés;
}

int allMask = (1 < < TotalKeys) - 1;
file d'attente <État> q;
unordered_set<string> vis; // visited state hash

q.emplace(0, sr, sc);
vis.insert("0 " + to_string(sr) + " + to_string(sc));

const int dr[4] = {1,1,0,0};
const int dc[4] = {0,1,-1};
Étapes int = 0;

BFS
pendant que (!q.vide()) {
int sz = q.size();
pour (int i = 0; i < sz; ++i) {
État cur = q.front(); q.pop();

si (cur.keys) toutes les étapes de retour;

pour (int d = 0; d < 4; ++d) {
int nr = cur.r + dr[d];
int nc = cur.c + dc[d];
si (nr < 0) nr >= m) continuer;

char ch = grille[nr][nc];
Si (ch == '#') continuer; // mur

int newKeys = cur.keys;
si ('a' <= ch && ch <= 'f')
newKeys= 1 << (ch - 'a'); //

Si ('A' <= ch && ch <= 'F' && (nouvelles clés >> (ch - 'A') & 1) == 0)
Continuer; // porte verrouillée

string key = to_string(nouvelles clés) + " + to_string(nr) + " + to_string(nc);
si (vis.insert(key).second) { // nouvel état
q.emplacer(nouveau) Clés, nr, nc);
}
}
}
+ étapes;
}
retour -1; // inaccessible
}
};
«» "

---

- Oui. 4. Billet de blog – ♫Mastering LeetCode 864: chemin le plus court pour obtenir toutes les clés

> **Mots clés**: chemin le plus court pour obtenir toutes les clés, LeetCode 864, BFS, bitmask, solution Java, solution Python, solution C++, entretien de codage, entretien d'ingénierie logicielle, préparation d'entretien d'emploi

---

Introduction

**LeetCode 864 – *La voie la plus courte pour obtenir toutes les clés*** est un puzzle classique de recherche de grille qui teste deux compétences de base toutes les demandes d'entrevue de concepteur de logiciels:

1. **Breadth‐First Search (BFS)** – pour l'exploration des sentiers les plus courts.
2. **Bit-masque DP** – pour comprimer des ensembles de clés en un seul entier.

Avec jusqu'à **6 touches** (`a–f`) et une taille de grille modérée (`=20 × 20`), l'algorithme est à la fois rapide * et facile à comprendre – le problème d'entrevue parfait.

---

- Oui. Le problème (dans une phrase)

> *Avec une grille 2-D où `@` est votre départ, `#` bloque le mouvement, les lettres minuscules (`a–f`) sont des clés et les lettres majuscules (`A–F`) sont des portes verrouillées qui nécessitent la clé correspondante, trouver le nombre minimum de mouvements pour collecter chaque clé. *

Si vous ne pouvez pas obtenir toutes les clés, retourner `-1`.

---

### Pourquoi BFS + Bit-Masking fonctionne

Concept Explication
C'est pas vrai.
**État** (ligne, col, clés) – vous devez vous rappeler *où* vous êtes *et * quelles clés* vous avez. Autres
Chaque clé est un peu ('1 << index'). Pour ≤6 clés, nous avons besoin d'au plus 64 bits distincts («26»). Autres
* Transition * Déplacer vers une cellule adjacente si elle n'est pas un mur. Si elle contient une clé, définissez le bit; si elle est une porte, vérifiez le bit avant de bouger. Autres
**Visité**=Hash `(row, col, touches)` pour éviter de revoir les états. Sans la dimension des clés, on bouclerait pour toujours. Autres

Parce que BFS explore *niveau par niveau*, la première fois que nous voyons `allKeysMask` nous avons trouvé le chemin le plus court.

---

Ce qui fait gagner cette solution

- **Efficacité du temps**: "O(m·n·2^k)" où `k` ≤ 6, parfaitement adapté aux limites du LeetCode.
- **Efficacité de l'espace**: «O(m·n·2^k)» des états visités – moins de 400 × 64 .
- **Straightforward**: Une boucle BFS claire, une opération bitmask par mouvement.
- **Language-agnostique**: La même logique fonctionne en Java, Python, C++ et même Go ou Rust.

---

### # # #Bad=" – Les choses à surveiller

Ce qui arrive
- C'est quoi ?
**Masque de clé Wong**= Utiliser `1 << (ch - 'a')' avec le mauvais caractère de base conduit à de mauvais bits pour `d`–`f`. Autres
**Les États survisagés**=Le fait de stocker simplement `(row, col)` ignore les différences clés, provoquant des cycles. Inclure les « clés » dans la clé visitée. Autres
**Grande grille et de nombreuses clés**Le pire cas peut exploser; si les clés > 10 la solution ralentit considérablement. Le problème garantit ≤6 clés, donc il est sûr. Autres

---

La complexité subtile

- **Voyage en Hash**: Construire des chaînes `"mask r c"` ou des tuples peut être *mémory faim* si la grille est grande.
- *Solution*: En C++ vous pouvez utiliser un vecteur 3-D `vecteur<vecteur<vecteur<bool>> visite;` ou une `structure` personnalisée C'est ça.
- **Portes à main avant les clés**: Si vous choisissez une touche *after* passant une porte, vous devez reculer – le BFS gère automatiquement cela, mais le débogage peut être déroutant.
- **Plusieurs points de départ**: LeetCode garantit un démarrage, mais un résolveur générique devrait faire la queue sur toutes les cellules `@`.

---

### Conseils pour l'entrevue

Situation Que dire
C'est pas vrai.
**Quand on a demandé d'expliquer BFS** , alors pour chaque niveau I , on va étendre tous les voisins. Parce que la grille n'est pas pondérée, la première fois que j'atteigne le but est garantie d'être le plus court. Autres
Autres **Lorsqu'un intervieweur met la mémoire en évidence** . . Comme nous avons au plus 6 touches, nous pouvons coder des ensembles de touches dans un entier 6 bits, réduisant considérablement l'espace d'état. Autres
Autres **Si l'intervieweur veut une solution en C++** .I.ll utilise un hachage personnalisé pour la structure `(r, c, masque)` et une `queue`. Cela évite de construire des cordes. Autres
Autres **S'ils s'interrogent sur les boîtiers de bord**=I=ll traitera une porte comme un mur si je n'ai pas la clé, sinon je passerai. Le masque assure que je ne revois jamais un état avec le même ensemble de clés. Autres
Autres **Quand la complexité du temps est interrogée**=C'est O(m·n·2^k) où k ≤ 6, donc au plus 400 × 64 opérations, ce qui est trivial pour les grilles 20×20.= Autres

---

Dernier verdict

**LeetCode 864** est *le puzzle de grille qui met en valeur la maîtrise de BFS + bitmask. Votre capacité à l'implémenter dans l'une des langues que vous avez pratiquées (Java, Python, C++) prouve que vous comprenez *recherche*, *compression d'état* et *échanges espace-temps*.

Lorsque vous présentez la solution dans une entrevue:

1. **Afficher le pseudocode** (état, transition, visité).
2. ** Expliquez pourquoi BFS donne le chemin le plus court**.
3. ** Mettre en avant le truc du mass** – Chaque clé est un peu, donc nous n'avons besoin que de 6 bits. (en milliers de dollars)
4. ** Contraintes à la peine de mort** – Au plus 6 clés, donc l'espace d'état reste minuscule. (en milliers de dollars)

Vous allez non seulement résoudre le problème, mais aussi convaincre l'intervieweur que vous êtes prêt pour les défis du graphe traversant du monde réel.

---

### Envelopper

Mastering LeetCode 864 signifie que vous avez pratiqué un motif algorithmique *core* qui apparaîtra sur de nombreuses interviews de codage : **Recherche + compression d'état**.

Essayez les implémentations **Java**, **Python** et **C++** ci-dessus, testez les cas de bord, et vous aurez confiance en vous promenant dans n'importe quelle salle d'entrevue.

Bonne chance ! C'est ce qu'il a dit.

---


> * Se sentir libre d'adapter le texte du blog à votre propre voix ou d'ajouter des extraits de code pour votre langue préférée. Bon codage ! *