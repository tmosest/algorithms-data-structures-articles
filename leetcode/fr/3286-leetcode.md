---
titre: LeetCode 3286. Trouvez une marche sûre à travers une grille -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3286 – Trouver une marche sécuritaire à travers une grille
*Java / Python / C++ Solutions + In-Depth Blog Post*

---

TL;DR
- **Objectif:** Commencer par `(0,0)`, terminer par `(m‐1, n‐1)` tout en maintenant la santé > 0 après avoir marché sur chaque cellule.
- ** Perte de santé :** `1` point pour chaque cellule dangereuse (`grid[i][j]==1`).
- **Retour:** `true` si un chemin sûr existe, sinon `faux`.

**Stratégie optimale:**
1. **BFS avec état (ligne, col, santé restante). **
2. **Gardez la meilleure santé que nous ayons vue à chaque cellule** – seulement de nouveau à l'arrivée avec *plus* santé.
3. **Temps:** "O(m × n × santé)" (-) 50 × 50 × 100 250 000).
4. **Espace:** `O(m × n)` pour la meilleure santé.

Nous montrons également une alternative *DP* (0-1 BFS) qui fonctionne dans `O(m × n)`.

---

- Oui. 1. Perspectives algorithmiques

C'est bien, c'est mal.
C'est pas vrai.
**BFS** nous garantit d'abord l'exploration de la voie *la plus courte* santé-perte. **Explosion d'État** si nous conservons naïvement chaque valeur de santé → la mémoire. Autres
**Visiter avec une santé maximale** évite de revoir une cellule avec une santé inférieure ou égale. La cellule de démarrage peut être dangereuse – nous devons soustraire cette perte avant BFS. Ne pas vérifier `santéReste > 0` après chaque mouvement conduit à de faux positifs. Autres
**0‐1 BFS DP** transforme le problème en un nombre minimum de cellules dangereuses le long de n'importe quel chemin. **DP ne fonctionne que lorsque vous connaissez le coût optimal** (ici 0/1 coûts). **La plus grande mémoire pour 3-D dp** (`m×n×health`) est inutile et lente. Autres

---

- Oui. 2. Solutions de référence

Ci-dessous vous trouverez des implémentations propres et idiomatiques dans **Java, Python et C++**.

> **Toutes les solutions supposent que la grille d'entrée est non vide et rectangulaire. **
> ** La santé est garantie 1'.**

---

### 2.1 Java – BFS avec la meilleure santé

"Java
Importation de java.util.*;

solution de classe publique {
// directions: en haut, en bas, à gauche, à droite
finale statique privée [] DIRS = {{-1,0},{1,0},{0,1},{0,1}};

public booléen trouverSafeWalk(Liste<Liste<entier>> grille, santé int) {
int m = quadrillage.size();
int n = grid.get(0).size();

// Santé initiale après le démarrage de la cellule
int startLoss = grid.get(0).get(0);
si (santé <= startLoss) retourner faux;
début int Santé = santé - début Perte;

// bestHealth[i][j] = santé maximale restante lorsque nous atteignons la première cellule (i,j)
int[] [] bestHealth = nouveau int[m][n];
pour (int[] rang : bestHealth) Arrays.fill(row, -1);

Queue<int[]> q = nouveau ArrayDeque<>();
q.offre(nouvelle int[]{0, 0, startHealth});
bestHealth[0]] = startHealth;

alors que (!q.isEmpty()) {
[] cur = q.poll();
int r = cur[0], c = cur[1], h = cur[2];

si (r == m - 1 && c == n - 1) retourner true; // atteint le but

pour (int[]d : DIRS) {
l'élément nr = r + d[0];
int nc = c + d[1];
si (nr < 0) nr >= m) continuer;

perte int = grid.get(nr).get(nc);
int nh = h - perte;
Si (nh <= 0) continue; // mourrait
si (nh <= bestHealth[nr][nc]) continue; // aucune amélioration

bestHealth[nr][nc] = nh;
q.offre(nouvelle int[]{nr, nc, nh});
}
}
retourner faux; // pas de chemin
}
}
«» "

**Pourquoi ça marche* *

* La file d'attente nous garantit d'explorer les cellules dans l'ordre croissant du *nombre de mesures prises*, pas la santé.
* Les pruneaux de table `bestHealth` sont revisités à moins que nous n'arrivions avec *plus* de santé qu'auparavant.
* Parce que chaque cellule est enquêtée au plus "santé" temps, l'algorithme fonctionne assez rapidement pour les contraintes.

---

#### 2.2 Python – BFS + meilleure santé

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
def trouver SafeWalk(self, grille: List[List[int]], santé: int) -> C'est vrai.
m, n = len(grid), len(grid[0])
start_loss = grille[0][0]
si santé <= start_loss:
Retour Faux
start_health = santé - start_loss

best = [[-1] * n pour _ dans la plage(m)]
best[0][0] = start_health
q = deque([(0, 0, start_health)])

dirs = [(-1, 0), (1, 0), (0, -1), (0, 1)]

alors que q:
r, c, h = q.popleft()
si r == m - 1 et c == n - 1:
retour Vrai
pour dr, dc en dirs:
nr, nc = r + dr, c + dc
si 0 <= nr < m et 0 <= nc < n:
perte = grille[nr][nc]
nh = h - perte
si nh <= 0:
poursuivre
si nh <= best[nr][nc]:
poursuivre
best[nr][nc] = nh
(nr, nc, nh)
Retour Faux
«» "

---

### 2.3 C++ – BFS avec priorité sur la santé restante

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Bool findSafeWalk(vecteur<vecteur<int>>& grille, santé int) {
int m = quadrillage(), n = quadrillage[0].size();
début int Perte = grille[0][0];
si (santé <= startLoss) retourner faux;
début int Santé = santé - début Perte;

vecteur<vector<int>> meilleur(m, vecteur<int>(n, -1));
file d'attente<tuple<int,int,int>> q;
q.emplace(0,0,startHealth);
best[0][0] = startHealth;

const int dr[4] = {-1,1,0,0};
const int dc[4] = {0,0,-1,1};

pendant que (!q.vide()) {
auto [r,c,h] = q.front(); q.pop();
si (r==m-1 && c==n-1) retourne true;
pour (int k=0;k<4;++k) {
l'alinéa suivant est ajouté:
si (nr <0="nr>=m="nc<0="nc>=n) poursuivre;
perte int = grille[nr][nc];
int nh = h - perte;
si (nh<=0) continue;
si (nh <= best[nr][nc]) continue;
best[nr][nc] = nh;
q.emplace(nr,nc,nh);
}
}
retourner faux;
}
};
«» "

---

3. Une solution de rechange pour les PDD (0-1 BFS)

Le BFS ci-dessus est déjà optimal, mais beaucoup d'intervieweurs aiment voir un *programmation dynamique* à emporter :
Trouver le nombre minimum de cellules dangereuses (`grid[i][j]==1`) sur n'importe quel chemin. (en milliers de dollars)

Si ce minimum est « k », nous n'avons besoin que de « santé > k » (parce que chaque cellule dangereuse déduit un point de santé).

#### 3.1 Pourquoi 0‐1 BFS?
* Chaque déplacement coûte soit `0` (cellule de sécurité) ou `1` (cellule de sécurité).
* La norme Dijkstra serait surqualifiée; BFS 0‐1 utilise une file d'attente double pour traiter les bords coût‐0 avant les bords coût‐1, donnant du temps linéaire.

Mise en œuvre de Java

"Java
Importation de java.util.*;

classe publique SolutionDP {
finale statique privée [] DIRS = {{-1,0},{1,0},{0,1},{0,1}};

public booléen trouverSafeWalk(Liste<Liste<entier>> grille, santé int) {
int m = grille.size(), n = grille.get(0).size();
int[]] dist = nouvelle int[m][n];
pour (int[] rang : dist) Arrays.fill(ligne, entier. MAX_VALUE;

Deque<int[]> dq = nouveau ArrayDeque<>();
int startLoss = grid.get(0).get(0);
si (santé <= startLoss) retourner false; // ne peut même pas passer au début

dist[0][0] = startLoss; // le coût comprend la cellule de démarrage
dq.offreFirst(new int[]{0,0});

alors que (!dq.isEmpty()) {
[] cur = dq.pollFirst();
int r = cur[0], c = cur[1];

pour (int[]d : DIRS) {
int nr = r + d[0], nc = c + d[1];
si (nr < 0) nr >= m) continuer;
Int add = grid.get(nr).get(nc);
int nd = dist[r][c] + ajouter;
si (nd < dist[nr][nc]) {
dist[nr][nc] = nd;
si (add == 0) dq.offreFirst(new int[]{nr,nc});
dq.offreDernière(nouvelle int[]{nr,nc});
}
}
}
// dist[m-1][n-1] = nombre minimal de cellules dangereuses sur n'importe quel chemin
retour santé > dist[m-1][n-1];
}
}
«» "

Version Python

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
def trouver SafeWalk(self, grille: List[List[int]], santé: int) -> C'est vrai.
m, n = len(grid), len(grid[0])
INF = 10**9
dist = [[INF]*n pour _ dans la plage(m)]
dist[0][0] = grille[0][0]
dq = masse([(0,0)])

dirs = [(-1,0),(1,0),(0,1),(0,1)]

alors que dq:
r,c = dq.popleft()
pour dr, dc en dirs:
nr, nc = r+dr, c+dc
si 0 <= nr < m et 0 <= nc < n:
Coût = grille[nr][nc]
nd = dist[r][c] + coût
si nd < dist[nr][nc]:
dist[nr][nc] = nd
si coût == 0:
(nr,nc)
Sinon:
Annexe(nr,nc)

retour santé > dist[m-1][n-1]
«» "

**Complexité* *

* **Temps:** `O(m × n)` – chaque cellule traitée au plus deux fois (une fois pour un bord `0`, une fois pour un bord `1`).
* **Espace:** `O(m × n)` – un simple tableau 2-D de nombre minimal de cellules dangereuses.

---

- Oui. 4. Liste de contrôle des cas de bord

Autres Décision Comment faire face au problème Pourquoi ça compte
- Oui.
**Démarrer la cellule dangereuse**=Soustraire sa perte *avant* BFS.=Le fait de ne pas le faire reviendra `vrai` même si vous mourez immédiatement. Autres
**La santé est exactement égale à la perte** Le problème dit explicitement que la santé doit rester **> 0**.
**Cellule de l'objectif dangereuse** Si on ignore la perte à la cellule finale, on peut penser qu'un chemin existe quand il est fatal. Autres
**Aucune manipulation spéciale – la table de taille s'en occupe. Seules les cellules qui améliorent la santé reçoivent une nouvelle demande, de sorte que la mémoire reste `O(m × n)`. Autres

---

- Oui. 5. Conseils d'entrevue

Conseil Code Extrait de code Pourquoi il est utile
-- -- -- -- -- -- -- -- -- -- -- -- --
**Expliquer l'état** – `(r, c, reste de la santé)' – **avant** plongée dans le code. Autres
Autres **Afficher l'idée de taille** – Nous garderons la meilleure santé pour chaque cellule. Autres
**Poignez la cellule de départ explicitement**. Autres
**Mention 0-1 BFS** comme alternative. Autres

---

- Oui. 6. Pensées finales

* L'approche BFS est **simple, rapide et garantie correcte** sous les contraintes.
* La solution de rechange DP/0‐1 BFS est idéale pour démontrer une vision de la réduction des coûts.
* Évitez le PDD 3-D ou la récursion naïve du SSD – ils sont inutiles et peuvent induire en erreur les intervieweurs.

Bonne chance ! C'est ce qu'il a dit.

---

- Oui. 7. Moteur de recherche Mots clés prêts

- LeetCode 3286
- Trouver une marche sûre à travers une grille
- Taille de la santé BFS
- Programmation dynamique BFS 0-1
- Solution Java BFS LeetCode
- Python BFS chemin de grille
- C++ BFS avec santé restante

---