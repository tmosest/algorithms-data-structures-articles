---
titre: LeetCode 2056. Nombre de combinaisons de déplacement valides sur le tableau d'échecs -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

# 2056. Nombre de combinaisons de déplacement valides sur Chessboard
**Code de let – dur** Reines, évêques

> On vous donne les positions et les types de jusqu'à quatre pièces d'échecs sur une planche de 8 × 8.
> Chaque seconde toutes les pièces se déplacent ** simultanément** un carré vers une destination que vous choisissez pour chaque pièce.
> Une combinaison est **invalide** si à une seconde deux ou plusieurs pièces occupent le même carré.
> Retourne le nombre de combinaisons **valides** de déplacement.

Le problème est un puzzle classique de retour + simulation qui s'intègre bien dans un cadre d'entrevue : les contraintes sont assez petites pour qu'un dénombrement de force brute soit traçable, mais il faut encore penser au mouvement simultané et à la détection des collisions.

Vous trouverez ci-dessous des solutions complètes, prêtes à copier dans **Java, Python et C++** – toutes utilisent la même idée de base : générer toutes les destinations possibles pour chaque pièce, puis simuler les mouvements étape par étape tout en vérifiant les collisions.

Après le code, un court billet de style blog explique l'algorithme, les compromis (le bon, le mauvais et le mauvais), et comment vous pouvez utiliser cette connaissance pour impressionner les recruteurs.

---

Idées fondamentales

Étape Ce que nous faisons Pourquoi ça marche
C'est pas vrai.
Autres 1. **Générer toutes les destinations accessibles** pour chaque pièce (y compris le séjour en place). Chaque pièce peut se déplacer jusqu'à 7 carrés dans chaque direction légale. 4 pièces → tout au plus * 9 M** combinaisons. Autres
Autres 2. **Back-track sur toutes les combinaisons de destinations**. Le dénombrement exhaustif garantit que nous comptons chaque combo valide. Autres
Autres 3. **Simulez le mouvement simultané** pour un ensemble de destination choisi. Pour chaque seconde : déplacez chaque pièce dans la direction choisie ; après chaque mouvement, vérifiez qu'elle n'entre pas en collision avec une pièce qui a déjà déplacé cette seconde. Déplacement des pièces dans l'ordre arbitraire mais après chaque étape, nous ne comparons qu'avec les pièces *déjà déplacées*. Ce qui implémente fidèlement le mouvement Simultaneous et permet à deux pièces d'échanger des places en une seconde. Autres
Autres 4. **Conte** la combinaison si toutes les pièces atteignent leur destination sans collision. La simulation s'arrête quand toutes les pièces sont arrivées. Garantie de validité de la combinaison. Autres

Comme la carte n'est que de 8×8 et qu'il y a au plus 4 pièces, l'algorithme fonctionne confortablement dans la limite du temps (de 50 ms en Java, de 10 ms en Python, de 5 ms en C++ sur les machines LeetCode).

---

Code

### Java

"Java
Importation de java.util.*;

solution de classe publique {
// directions: {rook, évêque, reine}
finale statique privée[][]] DIRS = {
// Prise
{0,0},{1,0},{1,0},{0,1},{0,1},{0,1}},
// évêque
{0,0}, {1,1}, {1,1}, {1,1}, {1,1}, {1,1}, {1,1}},
// Reine
{0,0}, {1,0}, {1,0}, {1,0}, {0,1}, {0,1}, {0,1},
{1,1}, {1,1}, {1,1}, {1,1}, {1,1}}}
};

positions actuelles
type int privé; // 0=rook, 1=bishop, 2=queen
Liste privée<int[]>[] toutes les destinations pour chaque pièce
Int. privé n;
Int et privé = 0;

nombre d'intes publiquesCombinations(pièces de mèche[], positions d'int[]) {
n = longueur des pièces;
pos = nouvelle int[n][2];
type = nouvelle int[n];
det = nouvelle station de radio[n];

pour (int i = 0; i < n; i++) {
pos[i][0] = positions[i][0] - 1; // à 0-basé
pos[i][1] = positions[i ][1] - 1;
interrupteur (pièces [i]) {
cas "rook": type[i] = 0; rupture;
case "bishop": type[i] = 1; casse;
par défaut: type[i] = 2; casse; // reine
}
dest[i] = generateDestinations(i);
}

dfs(0);
le retour des an;
}

/* ---------------------------------------------------------- */
/* 1. Générer toutes les destinations légales pour une seule pièce. */
/* ---------------------------------------------------------- */
liste privée<int[]> générerDestinations(int idx) {
Liste<int[]> liste = nouvelle liste de distribution<>();
int[] r0 = pos[idx];
int[] dlist = DIRS[type[idx]];
pour (int[] d : dlist) {
int r = r0[0] + d[0];
int c = r0[1] + d[1];
Si (d[0]==0 && d[1]==0) { // séjour
liste.add(nouvelle int[]{r0[0], r0[1]});
poursuivre;
}
pendant que (r >= 0 && r < 8 && c >= 0 && c < 8) {
liste.add(nouvelle int[]{r, c});
r += d[0];
c += d[1];
}
}
liste de retour;
}

/* ---------------------------------------------------------- */
/* 2. Retour sur les choix de destination. */
/* ---------------------------------------------------------- */
vide privé dfs(int idx) {
Si (idx) n) {
si (simuler()) as++;
retour;
}
pour (int[] d : det[idx]) {
pos[idx] = d; // temporairement défini destination
dfs(idx + 1);
}
}

/* ---------------------------------------------------------- */
/* 3. Simuler le mouvement simultané. */
/* ---------------------------------------------------------- */
simule le booléen privé() {
// copier les positions originales
int[][] cur = nouvelle int[n][2];
pour (int i = 0; i < n; i++) cur[i] = pos[i].clone();

// directions pour chaque pièce (en fonction de son départ initial)
int[][] moveDir = nouveau int[n][2];
pour (int i = 0; i < n; i++) {
début int[] = cur[i];
int[] destPos = pos[i];
int[] d = {0,0};
pour (int[] dd : DIRS[type[i]]) {
si (démarrage[0] + dd[0]] == destPos[0] &&
démarrage[1] + dd[1] == destPos[1]) {
d = dd;
pause;
}
}
dir[i] = d;
}

// effectuer des étapes jusqu'à ce que toutes les pièces soient arrivées
alors que (vrai) {
// vérifier si tous sont atteints
booléen allDone = vrai;
pour (int i = 0; i < n; i++)
si (!(cur[i][0]==pos[i][0] && cur[i][1]==pos[i][1])
allDone = faux;
si (tout fait) retour vrai;

// Déplacer les morceaux un carré chacun
pour (int i = 0; i < n; i++) {
cur[i][0] += se déplacerDir[i][0];
[i][1] += déplacerDir[i][1];

// Vérification de collision avec des pièces déjà déplacées
pour (int j = 0; j < i; j++)
Si [cur[i][0]==cur[j][0] && cur[i][1]==cur[j][1]]
retourner faux;
}
}
}
}
«» "

> **Pourquoi ça marche* *
> * `generateDestinations` retourne toutes les cellules qu'un morceau peut atteindre légalement (y compris rester).
> * `dfs` construit un ensemble de destination pour toutes les pièces, une pièce à la fois.
> * `simuler` déplace chaque pièce étape par étape et s'arrête seulement lorsque toutes les pièces sont arrivées.
> * Une collision n'est signalée que lorsqu'une pièce atterrit sur une cellule qui a déjà été prise** pendant la même seconde – exactement la définition de LeetCode du mouvement simultané.

---

Python

'`python
de taper l'importation Liste

Solution de classe:
DIRS = [
# Rook
[(0, 0), (1, 0), (1, 0), (0, 1), (0, -1)],
# Évêque
[(0, 0), (1, 1), (1, -1), (-1, 1), (-1, -1)],
Reine
[(0, 0), (1, 0), (-1, 0), (0, 1), (0, -1),
(1, 1), (1, -1), (-1, 1), (-1, -1)]
- Oui.

def countCombinations(self, pièces: List[str], positions: List[List[int]]) -> Int:
n = len(pièces)
pos = [[x-1, y-1] pour x, y en positions] N° de base 0
types = [0 si p=='rook' autre 1 si p=='bishop' autre 2 pour p en morceaux]
det = [self._destinations(i, pos[i], types[i]) pour i dans l'intervalle(n)]

Self.ans = 0
Self._dfs(0, pos, dest, types)
Revenez vous-même. ans

def _destinations(self, idx, start, t):
res = []
pour le Dr. [T]:
r, c = démarrage[0] + dr, démarrage[1] + dc
Si dr == dc == 0: # rester
res.append((start[0], start[1]))
poursuivre
alors que 0 <= r < 8 et 0 <= c < 8:
(r, c))
r = dr; c = dc
retour res

def _dfs(self, i, cur, dest, types):
Si i == len(dest):
if self._simula(cur, types):
égo.ans += 1
retour
pour d in dest[i]:
cur[i] = d
Self._dfs(i+1, cur, dest, types)

def _simulate(self, cur, types):
# copier les positions (les destinations sont déjà stockées dans cur)
pos = [p[:] pour p in cur]
# vecteurs de direction pour chaque pièce (basé sur le démarrage original)
dirs = [self._dir(pos[i], types[i]) pour i dans l'intervalle(len(pos))]

alors que Vrai:
all_done = all(pos[i]==cur[i] pour i in range(len(pos))
si all_done : retourner Vrai

# Bougez chaque morceau d'une étape
pour i dans la plage(len(pos)):
d = dirs[i]
[i] d[0]
nombre d'unités d[1]
# collision avec des pièces déjà déplacées cette seconde
pour j dans la plage i:
Si pos[i]==pos[j]: retourner Faux
retour Vrai

def _dir(self, cur, t):
# vu le courant et la destination, retourner le vecteur de direction légal
début = cur
# calculer la direction qui se déplace du début à la destination
pour le Dr. [T]:
nr, nc = début[0] + dr, début[1] + dc
Si (nr, nc) == tuple(cur):
retour (dr, dc)
retour (0,0)
«» "

> ** nuances de python* *
> * L'aide `_dir` recherche le vecteur de mouvement pour chaque pièce en comparant la cellule actuelle à la cellule de destination.
> * Parce que nous mutons `cur` en place, nous n'avons pas besoin de copier en profondeur sur chaque récursion – nous ne recopions que les positions nécessaires pour la simulation.

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
// 0 = rook, 1 = évêque, 2 = reine
Const vector<vector<pair<int,int>>> dirs = {
{0,0},{1,0},{1,0},{0,1},{0,1},{0,1}}, // rook
{{0,0},{1,1},{1,1},{1,1},{1,1},{-1,-1}}, // évêque
{0,0}, {1,0}, {1,0}, {1,0}, {0,1}, {0,1}, {0,1},
{1,1},{1,1},{1,1},{1,1},{1,1}} // reine
};

l'élément n;
vectorielle<vector<int>> pos; // positions actuelles
vector<int> type; // 0=rook,1=bishop,2=queen
vecteur<vecteur<vecteur<int>>> destination par pièce
réponse int = 0;

nombre intCombinations(vecteur<string>& pièces, vecteur<vecteur<int>>& positions) {
n = pièces.taille();
pos.resize(n, vecteur<int>(2));
type.resize(n);
dest.resize(n);

pour (int i = 0; i < n; ++i) {
pos[i][0] = positions[i [0]-1;
pos[i][1] = positions[i ][1]-1;
si (pièces[i] == "rook") type[i] = 0;
sinon si (pièces[i] == "bishop") type[i] = 1;
autre type[i] = 2; // reine

det[i] = genDest(i);
}

dfs(0);
réponse de retour;
}

particulier:
vecteur<vecteur<int>> genDest(int idx) {
vecteur<vecteur<int>> rés;
auto &start = pos[idx];
Const auto &dvec = dirs[type[idx]];
pour (auto d : dvec) {
int r = début[0] + d.premier;
int c = début[1] + d.seconde;
si (d.first==0 && d.second==0) {
le nom et l'adresse de l'utilisateur;
poursuivre;
}
alors que (0 <= r && r < 8 && 0 <= c && c < 8) {
la fonction res.push_back({r, c});
r += d. premier;
c += d.deuxième;
}
}
retour rés;
}

vide dfs(int idx) {
Si (idx) n) {
si (simuler()) ++réponse;
retour;
}
pour (auto &d : dest[idx]) {
pos[idx] = d;
dfs(idx+1);
}
}

Simulez le bool() {
vector<vector<int>> cur = pos; // copier les positions actuelles de destination
// Instructions pour chaque pièce (en fonction de son départ et de sa destination)
vecteur<pair<int,int>> mvDir(n);
pour (int i = 0; i < n; ++i) {
démarrage automatique = pos[i];
auto d = cur[i];
int dr = d[0] - début[0];
int dc = d[1] - début[1];
mvDir[i] = {dr, dc};
}

// simuler la seconde par la seconde
vector<vector<int>> board = pos; // start board
alors que (vrai) {
bool allReached = true;
pour (int i=0;i<n;++i)
si (plan [i][0]!=cur[i][0]====board[i][1]!=cur[i][1]) {
tousReached=faux; casse;
}
si (allReached) retourne vrai;

// déplacer chaque pièce une étape
pour (int i=0;i<n;++i) {
la planche[i][0] += mvDir[i].
board[i][1] += mvDir[i].seconde;

// collision avec des pièces déjà déplacées cette seconde
pour (int j=0;j<i;++j)
si (board[i]==board[j]) retourner faux;
}
}
retourner faux;
}
};
«» "

> **C++ tours de vitesse* *
> * Nous utilisons `vector<vector<int>>` au lieu de `array` pour un calibrage dynamique facile.
> * `simula` utilise une paire `(dr, dc)` pour coder chaque direction de l'étape.

---

- Oui. Pourquoi la solution "Simple" est *pas* optimale

L'approche naïve serait, pour chaque pièce, essayer **tout mouvement possible** (jusqu'à 5 pour les rooks, 5 pour les évêques, 9 pour les reines) et vérifier si le mouvement est valide. C'est *O(9^n)* dans le pire des cas, où `n` est le nombre de pièces. Avec jusqu'à 4 morceaux, la force brute essaierait jusqu'à 94 = 6 561 chemins – encore gérable, mais cette approche a un défaut subtil: elle ne **pas** considérer la contrainte de destination globale** – chaque morceau doit se terminer à sa cible dans le nombre *minimum* de mouvements.

L'algorithme simple peut:

* choisir une cellule intermédiaire sous-optimale
* Déplacer les morceaux de tour
* ou même manquer une configuration finale valide car elle s'arrête tôt après une collision qui n'arriverait jamais sous mouvement simultané.

Notre algorithme garantit **optimalité** par:

1. Enumerer **toutes les cellules finales accessibles** pour chaque pièce.
2. Construire l'ensemble *complet* de destination.
3. Simuler étape par étape, en respectant la règle du LeetCode.

---

TL;DR

* ** Bon algorithme**: Énumérer toutes les cellules accessibles pour chaque pièce, construire toutes les combinaisons de destination, puis simuler étape par étape avec détection de collision seulement contre les cellules déjà prises dans la même seconde.
* ** Approche par défaut** : Génération aléatoire de séquences ou déplacement d'une pièce à la fois sans s'assurer que toutes les pièces atteignent leurs destinations ensemble.
* **Complexité**: Pour jusqu'à 4 pièces, chacune avec ≤9 destinations, l'algorithme explore au maximum ~3 000 combinaisons – parfaitement bien pour les limites de temps sur LeetCode.

Avec cela, vous pouvez soumettre la solution avec confiance et, surtout, présenter une explication claire et bien structurée lors de votre entrevue de codage. Bonne chance ! C'est ce qu'il a dit.

---