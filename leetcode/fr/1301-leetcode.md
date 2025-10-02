---
titre: LeetCode 1301. Nombre de chemins avec score max -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

Code Leet 1301 – **Nombre de chemins avec une note maximale**
** Difficulté :** C'est dur **Tags:** DP, BFS, Grille, Modulo, Top-Down

---

Résumé du problème

Vous recevez une carte `n × n` (`2 ≤ n ≤ 100`).
Chaque cellule contient l'un des caractères suivants :

Sens de caractère
C'est pas vrai.
Démarrage (coin inférieur droit)
Fin (coin supérieur gauche)
Valeur numérique pouvant être collectée
"X" Obstacle – ne peut pas être entré

Vous pouvez déplacer **up**, **left** ou **up-left** (diagonalement) seulement si la cellule cible n'est pas un obstacle.
Votre objectif est de :

1. ** Maximiser** la somme des chiffres recueillis le long d'un chemin allant de `S` à `E`.
2. Comptez combien de chemins distincts atteignent ce score maximum.
Le compte doit être retourné modulo `1 000 000 007`.

Si aucun chemin n'existe, retourner `[0, 0]`.

---

- Oui. Idée de solution de haut niveau

Parce que chaque mouvement autorisé diminue l'indice de ligne et/ou de colonne, le graphique est **acyclique** – vous ne retournez jamais à une cellule que vous avez déjà visitée.
Cette propriété nous permet d'utiliser une approche simple **dynamique-programmation** qui traite le tableau ** depuis le début (en bas à droite)** vers le but (en haut à gauche).

Pour chaque cellule `(i, j)` nous stockons deux valeurs:

"maxScore[i][j]"" La plus grande somme qui puisse être obtenue lorsque nous *arrivons* à `(i, j)". Autres
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
"ways[i][j]"" Nombre de moyens d'obtenir ce "maxScore[i][j]".

Nous initialisons la cellule de départ avec le score `0` et `1`, puis itérer toutes les cellules dans l'ordre inverse ligne par ligne.
Pour chaque cellule, nous propagons son score aux trois cellules possibles de la suite (en haut, à gauche, en haut à gauche).
En nous propageant

* **Remplacez** le score de la cellule de destination si le nouveau score est plus grand.
* **Ajouter** à la cellule de destination s'il s'agit d'un nouveau score égal au maximum actuel.

Parce que chaque transition est monotone (seulement "upwards"), nous n'avons jamais besoin de revoir une cellule après qu'elle ait été traitée.

---

Algorithme (Code Pseudo)

«» "
MOD = 1 000 000 007
n = longueur de la planche
maxScore[n][n] =
Voies[n][n] = 0

// Commencez en bas à droite
maxScore[n-1][n-1] = 0
moyens[n-1][n-1] = 1

pour i de n-1 à 0:
pour j de n-1 à 0:
Si maxScore[i][j] == --
pour chaque (di, dj) dans {( -1, 0), (0, -1), (-1, -1)}:
ni = i + di; nj = j + dj
si ni < 0 ou nj < 0: continuer
si la planche[ni][nj]] «X»: continuer
ajouter = 0
si la table[ni][nj] est un chiffre:
ajouter = int(board[ni][nj])
Nouveau score = maxScore[i][j] + ajouter
Si NewScore > maxScore[ni][nj]:
maxScore[ni][nj] = nouveauScore
ways[ni][nj] = ways[i][j]
Sinon, si newScore == maxScore[ni][nj]:
ways[ni][nj] = (ways[ni][nj] + ways[i][j]) % MOD

réponse = [maxScore[0][0], voies[0][0]]]
si la réponse[0] est donnée
réponse de retour
«» "

**Complexité* *

Étape Temps Espace
C'est pas vrai.
"O(n2)" Autres

Avec `n ≤ 100` cela satisfait facilement les limites.

---

C'est pas vrai. Mise en œuvre des références

Voici des solutions propres et idiomatiques pour **Java, Python et C++**.

---

##### 4.1 Java 17

"Java
Importation de java.util.*;

solution de classe publique {
int final statique privé MOD = 1_000_000_007;

voies publiques int[]AvecMaxScore(Liste<String>) {
int n = board.size();
char[][] grille = nouveau char[n][n];
pour (int i = 0; i < n; i++)
grille[i] = board.get(i).toCharArray();

int[] maxScore = nouveau int[n][n];
int[][] ways = nouvelle int[n][n];
pour (int[] ligne : maxScore) Arrays.fill(ligne, entier.MIN_VALUE);

// cellule de démarrage (en bas à droite)
maxScore[n - 1] = 0;
Moyens [n - 1] - 1] = 1;

int[] dx = {-1, 0, -1};
int[] dy = {0, -1, -1};

pour (int i = n - 1; i >= 0; i--) {
pour (int j = n - 1; j >= 0; j--) {
si [maxScore[i][j]] Integer.MIN_VALUE) continuer; // inaccessible
pour (int dir = 0; dir < 3; dir++) {
Int ni = i + dx[dir];
int nj = j + dy[dir];
si (ni < 0) nj < 0) continuer;
char ch = grille[ni][nj];
si (ch) «X» continue;

int add = (ch >= '1' && ch <= '9') ? ch - '0' : 0;
int newScore = maxScore[i][j] + ajouter;

si (nouvelle note > maxScore[ni][nj]) {
maxScore[ni][nj] = nouveauScore;
ways[ni][nj] = ways[i][j];
} sinon si (nouvelle note == maxScore[ni][nj]) {
ways[ni][nj] = (ways[ni][nj] + ways[i][j]) % MOD;
}
}
}
}

Int final Score = maxScore[0][0];
Int final Voies = voies[0][0];
si (finalScore == Integer.MIN_VALUE) retourne le nouveau int[]{0, 0};
retour nouveau int[]{final Note finale Voies};
}
}
«» "

---

4.2 Python 3.10+

'`python
de taper l'importation Liste

MOD = 1 000 000 007

Solution de classe:
def chemins AvecMaxScore(self, board: List[str]) -> Liste[int]:
n = len(board)
grille = [liste(ligne) pour la ligne de tableau]

max_score = [[-10**9] * n pour _ dans l'intervalle(n)]
ways = [[0] * n pour _ dans l'intervalle(n)]

= 0
moyens[n-1][n-1] = 1

dirs = [(-1, 0), (0, -1), (-1, -1)]

pour i dans la plage(n-1, -1, -1):
pour j dans la plage (n-1, -1, -1):
Si max_score[i][j] == -10**9 :
poursuivre
pour di, dj in dirs:
ni, nj = i + di, j + dj
si ni < 0 ou nj < 0:
poursuivre
ch = grille[ni][nj]
Si ch == 'X':
poursuivre
ajouter = int(ch) si ch.isdigit() sinon 0
nouveau = max_score[i][j] + ajouter

Si nouveau > max_score[ni][nj]:
max_score[ni][nj] = nouveau
ways[ni][nj] = ways[i][j]
elif new == max_score[ni][nj]:
ways[ni][nj] = (ways[ni][nj] + ways[i][j]) % MOD

si max_score[0][0]] -10**9 :
retour [0, 0]
retour [max_score[0][0], voies[0][0]]]
«» "

---

*### 4.3 C++ 17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
MOD = 1'000'000'007;

vector<int> pathsAvecMaxScore(vector<string>& board) {
int n = board.size();
le vecteur<vector<int>> score(n, vector<int>(n, INT_MIN));
vecteur<vector<int>> voies(n, vecteur<int>(n, 0));

// cellule inférieure droite
score[n-1][n-1] = 0;
[n-1][n-1] = 1;

const int dx[3] = {-1, 0, -1};
const int dy[3] = { 0,1,-1};

pour (int i = n-1; i >= 0; --i) {
pour (int j = n-1; j >= 0; --j) {
Si (score[i][j]] == INT_MIN) continuer; // inaccessible
pour (int dir = 0; dir < 3; ++ dir) {
int ni = i + dx[dir], nj = j + dy[dir];
si (ni < 0) nj < 0) continuer;
char ch = planche[ni][nj];
si (ch) «X» continue;

int add = (ch >= '1' && ch <= '9') ? ch - '0' : 0;
int newScore = score[i][j] + ajouter;

si (nouvelle note > score[ni][nj]) {
score[ni][nj] = nouveau score;
ways[ni][nj] = ways[i][j];
} sinon si (NewScore == score[ni][nj]) {
ways[ni][nj] = (ways[ni][nj] + ways[i][j]) % MOD;
}
}
}
}

si (score[0]] == INT_MIN) retourne {0, 0};
retour {score[0][0], voies[0][0]};
}
};
«» "

---

C'est vrai. « Bonnes et mauvaises nouvelles – La bonne santé** par rapport à la mauvaise santé**

Bonne voie Autres
C'est le cas.
**Complexité**
**Effort de mise en œuvre**
**Empreinte de la mémoire** Autres
Très élevé Très élevé
Le graphique est un DAG – pas de cycles → DP linéaire

> **Bottom-Ligne:** Une seule passe DP est la bonne voie qui gagne sur le temps et la mémoire.

---

- Oui. La bonne et la mauvaise (erreurs communes)

Erreurs Pourquoi ça arrive Comment réparer
- C'est quoi ?
Ajouter la valeur de la cellule de départ. Traitement `S` comme score `0` seulement. Autres
*2 Oubliant de sauter les obstacles**.Path may ..step.. sur une cellule `X` et planter le programme. Explicite `si (ch == 'X') continue;'
Utiliser `int` pour les scores sur un plateau de 32 bits** – correspond toujours à `int`, mais quand vous utilisez `Integer. MIN_VALUE` en tant qu'"inatteignable" vous devez faire attention à ne pas déborder. Autres Utilisez une sentinelle (`-INF` ou `-109`) qui est bien en dessous de tout score réel. Autres
**4=Modulo sur chaque ajout**= Seulement les "ways" ont besoin de modulo. Les partitions ne le font pas. Conserver les notes comme `int`/`long`; appliquer `% MOD` uniquement sur `ways`. Autres
Revenir `[maxScore[0][0], ways[0][0]]» quand le but est inaccessible donne un score d'ordure. Après la boucle DP, si `maxScore[0][0]` est toujours `-INF`, retourner `[0, 0]`. Autres

---

Testez votre propre planche

'`python
# Python – test de santé rapide
si __nom__ == "__main__" :
sol = Solution()
tableau = [
"S123",
"X1X1",
"2X2E",
"121X"
- Oui.
print(sol.pathsWithMaxScore(board)) # [max_score, ways]
«» "

N'hésitez pas à modifier le tableau et à regarder comment l'algorithme se comporte.

---

Pourquoi cela compte pour votre préparation d'entrevue

Prestation
- Oui.
**Poignées Cycles Avec grâce**Le tableau est un DAG, donc un seul balayage DP suffit. Autres
**Définition claire de l'État**= `maxScore` + `ways` est une paire DP de manuel. Autres
**Le comptage modulaire**Le truc modulo est un agrafe dans les problèmes de la grille-DP. Autres
** Facile à traduire** Le même motif fonctionne en *any* langue (Java, Python, C++). Autres

---

## Résumé des recherches

* Code Leet 1301 – Nombre de chemins avec score maximal
* Grille acyclique DP – temps «O(n2)», «O(n2)» espace
* État bidimensionnel: `maxScore` et `ways` (mod `1e9+7`)
* Code de référence: **Java, Python, C++**

---

Lire plus

Sujet Lien
- Oui.
Profils de la grille du PDD https://leetcode.com/explore/learn/card/programmation dynamique avancée/ Autres
L'arithmétique modulaire dans DP. Autres
Haut vers le bas versus bas vers le haut. Autres

Bon codage, et que vos scores soient toujours *maximum*! C'est ce qu'il a dit