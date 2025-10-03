---
titre: LeetCode 2664. La tournée du Chevalier -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## La tournée du chevalier sur LeetCode #2664
**Le bon, le mauvais et le mauvais – un guide de recherche d'emploi**

---

### TL;DR

Langue Complexité Remarques
C'est quoi, ça ?
**Java**= O(m·n) rétrotrachéage (mauvaise caisse, 120 000 chemins)= Utilisation de panneaux à base de 0, profondeur de récursion ≤ 25=
**Python** Utilise des tuples pour des positions, des "itertools" non nécessaires.
**C++** et d ' un tableau mondial

La carte est au plus 5 × 5, donc une recherche approfondie (DFS) est assez rapide.
La clé est de stocker l'ordre de visite dans `board[r][c]` et backtrack quand un point mort est touché.

---

- Oui. 1. Récapitulation des problèmes

On vous donne une carte de taille `m × n` (1 ≤ m, n ≤ 5) et une position de départ `(r, c)`.
Un chevalier se déplace comme dans les échecs: `(dr, dc)` est une paire où un composant est 2 et l'autre est 1.
Votre tâche est de retourner une matrice où chaque cellule contient le numéro d'étape où le chevalier a visité ce carré, à partir de `0` pour la cellule initiale.
Il est garanti qu'il existe une tournée complète pour les caisses d'essai fournies.

---

- Oui. 2. Pourquoi l'arrière-plan fonctionne ici

- **Espace Etat:** `m · n` cellules, chacune visitée exactement une → au plus 25! chemins possibles (minute pour m,n ≤ 5).
- ** Faisabilité :** Le problème garantit une solution, donc nous pouvons nous arrêter quand nous trouvons la première tournée.
- **Déterminisme :** La sortie est déterministe une fois que nous décidons de l'ordre dans lequel nous essayons de bouger.

Parce que le tableau est petit, nous pouvons ignorer l'heuristique plus avancée (règle de Warnsdorff) et toujours terminer bien sous 1 ms.
Cependant, l'ajout d'un simple ordre de déménagement (Warnsdorff) accélère la recherche et démontre de bonnes pratiques d'entrevue de codage.

---

- Oui. 3. Aperçu de l'algorithme

1. **Définition** le chevalier bouge.
2. **Créer** un tableau 2-D `board` initialisé avec `-1` pour marquer les cellules non visitées.
3. **FDS(position, étape):**
- Marquez la cellule actuelle avec "étape".
- Si `étape == m*n - 1`, nous avons fini → retour `true`.
- Générer les prochaines cellules.
- *Facultatif:* trier les candidats en fonction du nombre de mouvements en marche (Warnsdorff).
- Récursez chaque candidat.
- Si la récursion échoue, backtrack: set `board[next]` retour à `-1`.
4. **Appel** DFS à partir de `(r, c, 0)`.

---

- Oui. 4. Analyse de la complexité

- **Heure:**
Dans le pire des cas, nous visitons chaque noeud de l'arbre de récursion:
La Commission a décidé de ne pas modifier le règlement (CEE) n° 1408/71.
Pour m,n ≤ 5, il s'agit d'une recherche triviale (8'25') 3'10'22, mais les pruneaux de recherche sont très nombreux.
Pratiquement < 1 ms sur matériel moderne.

- **Espace:**
- "board": O(m·n).
- Pile de récursion : O(m·n).
- Pas de structures de données supplémentaires.

---

- Oui. 5. Cas de bord

Autres Décision Pourquoi ça compte ?
- Oui.
1 × 1 board
Autres Carrés inaccessibles (cartes ombrées)
Position de départ sur le coin

---

- Oui. 6. Mise en œuvre du code

Voici des solutions propres, prêtes à l'interview dans **Java, Python et C++**.
Tous les trois utilisent le même noyau de retour.

#### 6.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
int final statique privé[] DR = {2, 1, -1, -2, -2, -1, 1, 2};
int final statique privé[] DC = {1, 2, 2, 1, -1, -2, -2, -1};

public int[][] tourOfKnight(int m, int n, int r, int c) {
int[][] plan = nouveau int[m][n];
pour (int[] ligne : planche) Arrays.fill(row, -1);
dfs(bord, r, c, 0);
la pension de retour;
}

boolean privé dfs(int[[]], int r, int c, int step) {
board[r][c] = étape;
si (étape == board.longueur * board[0].longueur - 1) retourner vrai;

Liste des déplacements <int[]> = nouvelle liste de distribution<>();
pour (int k = 0; k < 8; k++) {
int nr = r + DR[k], nc = c + DC[k];
si (nr >= 0 && nr < board.longueur &&
nc >= 0 & & nc < board[0]. longueur &&
Conseil[nr][nc] == -1) {
moves.add(nouvelle int[]{nr, nc});
}
}

// Commande facultative de Warnsdorff
moves.sort(Comparator.comparingInt(a -> onwardCount(board, a[0], a[1]));

pour (int[] mv : déplacements) {
si (dfs(board, mv[0], mv[1], pas + 1) le retour est vrai;
}

plan[r][c] = -1; //
retourner faux;
}

Count(int[]], int r, int c) {
cnt = 0;
pour (int k = 0; k < 8; k++) {
int nr = r + DR[k], nc = c + DC[k];
si (nr >= 0 && nr < board.longueur &&
nc >= 0 & & nc < board[0]. longueur &&
Conseil[nr][nc] == -1) cnt++;
}
retour cnt;
}
}
«» "

6.2 Python

'`python
Solution de classe:
mouvements = [(2, 1), (1, 2), (-1, 2), (-2, 1),
(-2, -1), (-1, -2), (1, -2), (2, -1)]

def tourOfKnight(self, m: int, n: int, r: int, c: int) -> list[list[int]]:
tableau = [[-1] * n pour _ dans la plage(m)]
auto.dfs(planche, r, c, 0)
tableau de retour

def dfs(self, board, r, c, step):
board[r][c] = étape
Si l'étape == len(board) * len(board[0]) - 1:
retour Vrai

candidats = []
pour le Dr. mouvements:
nr, nc = r + dr, c + dc
si 0 <= nr < len(board) et 0 <= nc < len(board[0]) et la planche[nr]]. - 1 :
candidats.annexe(nr, nc))

# Warnsdorff: trier par le nombre de mouvements en avant
candidats.sort(key=lambda pos: auto.onward(board, *pos))

pour nr, nc dans les candidats:
s'il s'agit d'un véhicule automoteur (bord, nr, nc, pas + 1):
retour Vrai

board[r][c] = -1 # retour
Retour Faux

def onward(self, board, r, c):
nombre = 0
pour le Dr. mouvements:
nr, nc = r + dr, c + dc
si 0 <= nr < len(board) et 0 <= nc < len(board[0]) et la planche[nr]]. - 1 :
nombre += 1
Nombre de retours
«» "

*### 6.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
const int dr[8] = {2,1,-1,-2,-2,-1,1,2};
const int dc[8] = {1,2,2,1,-1,-2,-2,-1};

vector<vector<int>> tourOfKnight(int m, int n, int r, int c) {
vector<vector<int>> board(m, vector<int>(n, -1));
dfs(bord, r, c, 0);
la pension de retour;
}

particulier:
bool dfs(vector<vector<int>>& board, int r, int c, int step) {
board[r][c] = étape;
si (étape == board.size() * board[0].size() - 1) retourner true;

le vecteur<pair<int,int>> se déplace;
pour (int k=0;k<8;k++){
l'alinéa suivant est ajouté:
si (nr>=0 && nr<(int)board.size() &&
nc>=0 && nc<(int)board[0].size() &&
Planche[nr][nc]==1)
moves.push_back({nr,nc});
}

// Warnsdorff heuristique
Tri(moves.begin(), moves.end(),
[&](paire de const<int,int>&a, paire de const<int,int>&b) {
retour vers l'intérieur (à bord,a.first,a.second) <
vers l'avant (board, b.first, b.second);
});

pour (auto [nr,nc]: se déplace) {
si (dfs(board,nr,nc,step+1)) retourne true;
}
plan[r][c] = -1; //
retourner faux;
}

int onward(const vector<vector<int>>& board, int r, int c){
cnt=0;
pour (int k=0;k<8;k++){
l'alinéa suivant est ajouté:
si (nr>=0 && nr<(int)board.size() &&
nc>=0 && nc<(int)board[0].size() &&
board[nr][nc]==1) cnt++;
}
retour cnt;
}
};
«» "

---

- Oui. 7. Exposition Blog-Style: La tournée du Chevalier – Bon, mauvais, et lugubre

#### 7.1 Bon – Pourquoi Ce problème est un Gold‐Mine pour les intervieweurs

1. **Shows Mastery of DFS & Backtracking**
La tournée Knight est un problème classique de DFS qui vérifie si le candidat peut gérer la profondeur de récursion, la taille et la restauration de l'état.
2. ** Encourage la pensée algorithmique* *
Les candidats doivent raisonner au sujet d'un espace de recherche combinatoire, décider de déplacer l'ordre et gérer les états visités.
3. ** Contraintes du temps et de l'espace Fit LeetCodes Catégorie* *
Avec `m, n ≤ 5`, la force brute est acceptable, mais c'est toujours un puzzle subtil – bon pour distinguer les penseurs rapides.

#### 7.2 Mauvais – Pièges communs des candidats

Pourquoi ça va mal Comment réparer
- C'est quoi ?
Autres **Storing visité dans un tableau 1‐D**=Difficile de cartographier les coordonnées → erreurs off‐by‐one==Utilisez une matrice 2‐D ou un bitmask avec `(r * n + c)` Autres
Autres **Pas de rétro-suivi**
**Caisse de base manquante**. Récursion jamais fini → débordement de la pile.
**Utiliser l'état mutable global sans réinitialiser** , les appels suivants réutiliser le même tableau , réinitialiser le tableau dans chaque méthode publique

7.3 Ugly – Pourquoi il peut s'envoler hors de contrôle

1. ** Génération de mouvement non ordonnée**
Sans Warnsdorff ou n'importe quelle taille, la recherche explore de nombreuses impasses, surtout sur 5 × 5 planches.
2. **Profondeur excessive de récursion dans d'autres langues* *
Dans des langues comme le Python, la profondeur de récursion par défaut est de 1000, mais pour une planche de 25 cellules, elle est très bien; quand même, fixez toujours une garde si vous prévoyez de l'étendre.
3. **Ignorer la garantie d'une solution**
Certains candidats écrivent des résolveurs hamiltoniens-path génériques qui s'occupent de n'importe quelle taille du conseil d'administration—surcompétence pour ce problème.

### 7.4 Conseils pour réduire votre solution

* Initialisez toujours le tableau à `-1`** (sans visite).
- **Utilisez les 8 mouvements prévus** – aucun nombre magique.
- **Appliquez Warnsdorff** (facultatif) – triez les mouvements par le nombre de déplacements pour réduire les ramifications.
- **Test cas de bord**: 1 × 1, commençant au milieu, commençant par un coin.

---

- Oui. 8. Mot final pour le recruteur

Si vous embauchez un ingénieur logiciel, présenter la tournée de Knights dans une séance d'entrevue est un signal fort d'un candidat.
Les solutions ci-dessus démontrent l'approche propre et de qualité de production que la plupart des recruteurs apprécient.
Et pour les demandeurs d'emploi : une mise en œuvre solide ici vous rapporte un coup de pouce et un coup de confiance rapide pour votre prochain cycle de codage.

---

- Oui. 9. Références et lectures supplémentaires

- [Code Leet 1231. Visite des chevaliers (hard)](https://leetcode.com/problèmes/knights-tour/)
- [Règle de Warnsdorff – Wikipedia] (https://en.wikipedia.org/wiki/Warndorff%27s_rule)
(https://www.crackingthecodinginterview.com/)

---

*Ce post combine la rigueur algorithmique et les idées stratégiques de l'entrevue – parfait pour les deux candidats affûtant leurs compétences et les recruteurs affinant leurs critères d'évaluation. *