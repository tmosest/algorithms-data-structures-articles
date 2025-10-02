---
titre: LeetCode 2814. Temps minimum nécessaire pour atteindre la destination sans noyer -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Code Leet 2814 – Le temps minimum prend pour atteindre la destination sans noyer

> **Objectif:** Trouver le nombre minimum de secondes nécessaires pour marcher de **S** à **D** sur une grille `n × m` tout en évitant la pierre (`X`) et les cellules inondables (`*`).
>
> L'inondation s'étend chaque seconde aux cellules vides de 4 voisins. Vous ne pouvez pas marcher sur une cellule qui devient inondée à la même seconde vous marchez sur elle.
>
> **Retour** le temps de déplacement le plus court ou `-1` s'il est impossible.

---

TL;DR

* Calculer le temps que chaque cellule sera inondée par un BFS ** multi-source** qui part de chaque `*`.
* Exécuter un **seconde BFS** à partir de **S** où un déménagement vers un voisin n'est autorisé que si :
* le voisin n'est pas une pierre,
* le voisin n'est pas inondé * avant ou à l'arrivée
* le voisin est soit vide, soit la destination.
* La première fois que nous atteignons **D** est la réponse.

complexité temporelle: "O(n · m)"
complexité de la mémoire: `O(n ·m)`

---

- Oui. Pourquoi est-ce un grand problème d'entrevue?

C'est bien, c'est mal.
C'est pas vrai.
**BFS** multi-source – enseigne au candidat comment gérer la propagation simultanée (comme le feu, l'infection). **Contrôles budgétaires** peuvent devenir désordonnés. **Étapez dans une cellule qui est inondée à la même seconde** – un cas de coin subtil qui voyage souvent les candidats. Autres
**L'approche en deux phases** – séparation claire de ce qui va se passer. **La plus grande grille (100×100)** → doit éviter les algorithmes quadratiques ou exponentiels. Autres ** Erreurs hors-par-un** dans le calcul du temps lorsque l'inondation et le mouvement se produisent au même instant. Autres
Autres La solution est ** évolutive** à des contraintes plus grandes (par exemple `10^3 × 10^3'). Il faut penser à **visité** état; naïf `booléen[][]` peut ne pas suffire si vous autorisez la révision à un moment ultérieur. **Les multiples structures de données** (queues, matrices) peuvent encombrer le code pour une courte entrevue. Autres

---

Solutions complètes

Vous trouverez ci-dessous un code propre, prêt à la production pour **Java**, **Python** et **C++**.
Chaque implémentation suit la même logique : calculer les temps d'inondation, puis BFS le joueur.

---

- Oui. 1. Java

"Java
Importation de java.util.*;

solution de classe publique {
finale statique privée [] DIRS = {{-1,0},{1,0},{0,1},{0,1}};
Inf = entier.MAX_VALUE;

Int minimum public Seconds(Liste<Liste<String>> terrain) {
int n = terrain.size();
int m = land.get(0).size();

Temps d'inondation: BFS multi-sources de tous '* '
int[]] inondation = nouvelle int[n][m];
pour (int i = 0; i < n; i++) Arrays.fill(flood[i], INF);

Queue<int[]> q = nouveau ArrayDeque<>();
int startR = 0, startC = 0, detR = 0, detC = 0;

pour (int r = 0; r < n; r++) {
pour (int c = 0; c < m; c++) {
Cellule chaîne = land.get(r).get(c);
si ("*".egals(cell)) {
inondation[r][c] = 0;
q.add(nouvelle int[]{r, c});
} sinon si ("S".equals(cellule)) {
startR = r; startC = c;
} sinon si ("D" egals(cell) {
detR = r; detC = c;
}
}
}

alors que (!q.isEmpty()) {
[] cur = q.poll();
int r = cur[0], c = cur[1], t = inondation[r][c];
pour (int[]d : DIRS) {
int nr = r + d[0], nc = c + d[1];
Si (0 <= nr && nr < n && 0 <= nc && nc < m &&
(land.get(nr).get(nc).equals(."")
INF) {
inondation[nr][nc] = t + 1;
q.add(nouvelle int[]{nr, nc});
}
}
}

Le joueur BFS
booléen[]] vis = nouveau booléen[n][m];
Queue<int[]> pq = nouveau ArrayDeque<>();
pq.add(new int[]{startR, startC, 0}); // r, c, time
vis[startR][startC] = true;

pendant que (!pq.isEmpty()) {
int[] cur = pq.poll();
int r = cur[0], c = cur[1], t = cur[2];
si (r) destR &&c == destC) retourne t;

pour (int[]d : DIRS) {
int nr = r + d[0], nc = c + d[1];
t + 1;
Si (0 <= nr && nr < n && 0 <= nc && nc < m &&
[nr][nc] &&
!land.get(nr).get(nc).equals("X") &&
(land.get(nr).get(nc).equals(."")
inondation[nr][nc] > nt) { // jamais inondé avant l'arrivée
vis[nr][nc] = vrai;
pq.add(nouvelle int[]{nr, nc, nt});
}
}
}

retour -1; // inaccessible
}
}
«» "

---

- Oui. 2. Python

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
DIRS = [(-1, 0), (1, 0), (0, -1), (0, 1)]
INF = 10 ** 9

def minimum Seconds(self, land: List[List[str]]) -> Int:
n, m = len(land), len(land[0])

N° 1 Temps d'inondation
inondation = [[self.INF] * m pour _ dans la plage(n)]
q = deque()
sr = sc = dr = dc = 0

pour i dans la plage(n):
pour j dans la plage(m):
si land[i][j]== '*':
inondation[i][j] = 0
q. appendice(i, j))
land [i][j] == 'S':
sr, sc = i, j
élif land[i][j]== 'D':
dr, dc = i, j

alors que q:
r, c = q.popleft()
t = crue[r][c]
pour Drc, Dcc en soi. - Oui.
nr, nc = r + drc, c + dcc
si 0 <= nr < n et 0 <= nc < m et \
et de l'inondation. soi-même. INF:
inondation[nr][nc] = t + 1
q.annexe(nr, nc))

N° 2 Joueur BFS
vis = [[Faux] * m pour _ dans la plage(n)]
q = deque([(sr, sc, 0)]) # r, c, time
vis[sr][sc] = Vrai

alors que q:
r, c, t = q.popleft()
i r == dr et c == dc:
retour t
pour Drc, Dcc en soi. - Oui.
nr, nc = r + drc, c + dcc
nt = t + 1
si 0 <= nr < n et 0 <= nc < m et \
non vis[nr][nc] et \
[nr][nc] != 'X' et \
(land[nr][nc] in {'.', 'D'}) et \
inondation[nr][nc] > nt: # sûr d'entrer
vis[nr][nc] = Vrai
(nr, nc, nt)

retour -1
«» "

---

- Oui. 3. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
INF = 1e9;
vecteur<pair<int,int>> dirs = {{-1,0},{1,0},{0,1},{0,1}};

Int minimum Seconds(vecteur<vecteur<char>>&terre) {
int n = land.size(), m = land[0].size();

// -------- Temps d'inondation - Oui.
vecteur<vector<int>> inondation(n, vecteur<int>(m, INF)
file d'attente <pair<int,int>> q;
int sr=0, sc=0, dr=0, dc=0;

pour (int r=0; r<n; ++r) {
pour (int c=0; c<m; ++c) {
si (land[r][c]=='*') {
inondation[r][c]=0;
q.emplacer(r,c);
} sinon si (land[r][c]=='S') {
sr=r; sc=c;
} sinon si (land[r][c]=='D') {
dr=r; dc=c;
}
}
}

pendant que (!q.vide()) {
auto [r,c] = q.front(); q.pop();
t = inondation[r][c];
pour (auto [drc, dcc]: dirs) {
l'information nr=r+drc, nc=c+dcc;
si (nr>=0 && nr<n && nc>=0 && nc<m &&
(land[nr][nc]====================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================
inondation[nr][nc]==INF] {
inondation[nr][nc]=t+1;
q.emplace(nr,nc);
}
}
}

// -------- Le joueur BFS --------
vecteur<vector<bool>> vis(n, vector<bool>(m,false));
file d'attente<tuple<int,int,int>> pq; // r,c,time
pq.emplace(sr,sc,0);
vis[sr][sc]=true;

pendant que (!pq.vide()) {
auto [r,c,t] = pq.front(); pq.pop();
si (r==dr && c==dc) retourne t;
pour (auto [drc, dcc]: dirs) {
l'information nr=r+drc, nc=c+dcc;
int nt=t+1;
si (nr>=0 && nr<n && nc>=0 && nc<m &&
[nr][nc] &&
[nr][nc]!='X' &&
(land[nr][nc]============== Terre[nr][nc]===== D] &&
inondation[nr][nc]>nt) {
vis[nr][nc]=true;
pq.emplace(nr,nc,nt);
}
}
}
retour -1;
}
};
«» "

---

## Pièges communs et comment les éviter

Pourquoi ça arrive ?
- Oui.
**Off‐by‐one lorsque l'on compare le temps d'inondation** Autres
Autres Le joueur peut attendre sur une cellule qui inondera la seconde suivante. Autres
**Tirer la destination**=Certains candidats oublient que l'entrée dans **D** est toujours permise, même si le temps d'inondation est `0'='. Autres
**Grande valeur INF** Utilisez une valeur sentinelle (`INF = 1e9` ou `INT_MAX / 2`) qui peut être incrémentée en toute sécurité. Autres
**Restaurer une cellule plus tard peut être optimal (mais jamais nécessaire ici) Autres

---

Analyse de complexité

Étape Opérations Complexité
- C'est quoi ?
Chaque cellule est découlée une fois, 4 voisins vérifiés → "4·n·m` checks" Autres
Le même raisonnement que l'inondation de BFS. Autres
Mémoire de deux matrices `int` (`inondation` et `vis`) Autres

Pour les contraintes maximales ('100 × 100'), l'algorithme se termine en quelques millisecondes et utilise < 1 Mo de mémoire – parfaitement acceptable pour une entrevue.

---

Prêt à... Utiliser le modèle pour les entrevues

Au cours d'un entretien chronométré, vous ne voulez pas passer du temps à construire un UI, à écrire des analyseurs d'entrée, etc.
Vous trouverez ci-dessous un modèle **minimum** que vous pouvez coller dans l'éditeur LeetCode (Java, Python ou C++).

Modèle de langue
C'est pas vrai.
* * * * * * } * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
**Python**=_________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
* * * * * * } }

Il suffit de remplacer le commentaire `/* ... */` par le code complet ci-dessus.

---

## Liste de contrôle des entrevues amicales

1. **Énoncez l'idée en deux phases** (première inondation, puis bougez).
2. **Afficher BFS** – vous pouvez marcher à travers comment initialiser la file d'attente et visiter les voisins.
3. ** Expliquez la condition temporelle**: `foodTime[voix] > heure actuelle + 1 %.
4. **Parler des cas d'angle**:
* Si la cellule de départ est entourée de cellules d'inondation → impossible.
* Si **D** est sur la même ligne/col qu'un `*` → vous devez arriver *avant* il inonde.
5. **Complexité**: `O(n · m)` est le meilleur que vous pouvez faire – la grille est le facteur limitant.
6. **Demander des questions claires** (p. ex., pouvons-nous marcher en diagonale?

---

## SEO-Friendly Takeaway

Si vous êtes à la recherche de *land que prochain emploi de technologie* ou *écraser votre entrevue de codage*, mettre en évidence LeetCode 2814 dans votre CV:

- **Mots clés:** `LeetCode 2814`, `temps minimum pour arriver à destination sans noyade`, `BFS multisources`, `Java BFS inondation spread`, `Python BFS solution`, `C++ inondation BFS`, `coding interview problem`, `coding challenge interview`.

- **Pourquoi c'est important :** Démontrer *décomposition de problèmes*, *pensée algorithmique* et *compétences de mise en oeuvre propres* – tous les intervieweurs ont une grande valeur.

---

La dernière pensée

LeetCode 2814 est plus qu'un puzzle d'évasion d'inondation; il s'agit d'une étude **mini-case** de la façon de combiner **simulation** (l'inondation) et **recherche** (votre chemin) dans une solution unique et efficace.

**Montrer aux intervieweurs** que vous pouvez :

1. Briser un problème en **phases claires**.
2. Utilisez **BFS** – le cheval de bataille de nombreux problèmes d'entrevue.
3. Gérer les contraintes subtiles **temps-synchronisation**.

Bonne chance, et rappelez-vous – l'inondation n'est qu'une métaphore des contraintes du monde réel; restez calme et codez! C'est vrai