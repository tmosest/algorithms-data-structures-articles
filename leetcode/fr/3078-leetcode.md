---
titre: LeetCode 3078. Correspondance alphabétique Modèle dans la matrice Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3078. Correspondance alphabétique Modèle dans la matrice I
**Moyenne******Java******Python******C++**

---

- Oui. 1. Récapitulation des problèmes

On vous donne

* `board`: une matrice de chiffres (de 0 à 9):
* `pattern`: une matrice de caractères `p × q` – chaque caractère est soit un chiffre (`'0'```'9'`) soit une lettre minuscule (`'a````'z``).

Une sous-matrice de «board» **matches** `pattern` s'il existe une cartographie de chaque lettre distincte dans `pattern` à un chiffre *unique* de telle sorte qu'après application de la cartographie chaque cellule de la sous-matrice égale la cellule correspondante dans `pattern`.
Les chiffres dans `pattern` doivent correspondre exactement au tableau.

Retourner les coordonnées `[row, col]` du coin **upper-gauche** de la première sous-matrice correspondante (ligne la plus basse, puis colonne la plus basse).
Si aucune correspondance n'existe, retourner `[-1, -1]`.

---

- Oui. 2. Pourquoi ce problème est une grande question d'entrevue

C'est bien, c'est mal.
C'est pas vrai.
**Profondeur conceptuelle** – testez votre compréhension de l'appariement des motifs, de la cartographie bijective et du passage 2-D. **Lassitude de la caisse** – de nombreuses erreurs hors-par-un, surtout lors de la cartographie des lettres aux chiffres. Autres

- **Bonne**: Le problème est assez petit pour vous laisser la force brute, mais il vous oblige à penser à *bijection* entre les lettres et les chiffres.
- **Bad**: Il est facile d'écrire un algorithme correct, mais obtenir des réponses erronées sur des cas d'angle tels que des lettres répétées, des conflits de lettres numériques, ou des motifs qui touchent la limite du tableau.
- **Ugly**: Si vous oubliez de réinitialiser votre mapping entre différentes positions de haut à gauche, vous obtiendrez de faux positifs.

Se préparer à ce problème vous mettra à l'aise avec:
* Passage en réseau bidimensionnel
* Cartographie des contraintes et détection des conflits
* Conditions de sortie anticipée (dès qu'une inadéquation est constatée)

Tous ces éléments sont des agrafes d'entretiens de codage de niveau supérieur à FAANG, Amazon, Google, etc.

---

- Oui. 3. Aperçu de la solution

1. **Il s'agit de toutes les positions de départ possibles* *
Pour chaque `r` dans `[0, m - p]` et `c` dans `[0, n - q]` nous considérons la sous-matrice dont le coin supérieur gauche est `(r, c)`.

2. **Maintenir deux cartes**
* `numérique → lettre` (pour mémoire de la taille 10, initialisée à "-1")
* "lettre → chiffre" (pour mémoire de la taille 128 ou d'un hashmap)

Ces deux cartes garantissent l'exigence de bijection.

3. **Valider le sous-matrice**
Pour chaque cellule `(i, j)` à l'intérieur du motif:
* Si le terme `pattern[i][j]` est un chiffre, il doit égaler la valeur du tableau à `(r+i, c+j)`.
* Si c'est une lettre:
* Si nous avons déjà cartographié ce chiffre, la lettre cartographiée doit être la même.
* Si nous avons déjà cartographié cette lettre, le chiffre doit être le même.
* S'il n'existe aucune cartographie, établir les deux.

4. **Retourner les premières coordonnées correspondantes* *
Parce que nous itérer les lignes en premier, les colonnes en second, le premier match réussi est automatiquement le lexicographiquement le plus petit.

5. **Si aucune correspondance ne correspond, retourner `[-1, -1]`. **

Complexité
*Temps*: "O(m-p+1)(n-q+1) * p * q)" – pire cas: "503 = 125 000".
*Espace*: "O(1)" – seulement des tableaux de taille fixe pour les deux cartes.

---

- Oui. 4. Mise en œuvre des références

Ci-dessous vous trouverez des solutions propres et idiomatiques dans **Java, Python et C++**.
Tous les trois suivent la même logique que celle décrite ci-dessus.

---

##### 4.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe {
public int[] findPattern[int[][] board, String[] pattern) {
int m = longueur de la planche, n = longueur de la planche[0]. longueur;
int p = pattern.longueur, q = pattern[0].longueur();

pour (int r = 0; r + p <= m; r++) {
pour (int c = 0; c + q <= n; c++) {
int[] digitToLettre = nouveau int[10]; // 0 signifie non mapée
lettreToDigit = nouvelle int[128]; // -1 signifie non mapée
Arrays.fill(digitToLetter, 0);
Arrays.fill(lettreToDigit, -1);

booléen ok = vrai;
pour (int i = 0; i < p && ok; i++) {
pour (int j = 0; j < q && ok; j++) {
carte intérieure Val = planche[r + i][c + j];
char pat = motif[i].charAt(j);

si (Caracter.isDigit(pat)) {
si (pat - '0' != boardVal) ok = faux;
} autre { // lettre
si (digitalToLetter[boardVal]) 0) {
// nouvelle cartographie
si (lettreToDigit[pat]) -1) {
digitToLetter[boardVal] = pat;
lettreToDigit[pat] = boardVal;
} autre {
// même lettre cartographiée à un chiffre différent
ok = faux;
}
} sinon si (digitToLetter[boardVal] != pat) {
// chiffre du tableau déjà cartographié à une autre lettre
ok = faux;
}
}
}
}

si (ok) retourne une nouvelle int[]{r, c};
}
}
retourner une nouvelle int[]{-1, -1};
}
}
«» "

---

4.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def findPattern(self, board: List[List[int]], pattern: List[str]) -> Liste[int]:
m, n = len(board), len(board[0])
p, q = len(pattern), len(pattern[0])

pour r dans la plage (m - p + 1):
pour c dans la plage (n - q + 1):
# chiffre -> lettre (0 signifie non marqué)
d2l = [0] * 10
# lettre -> chiffre (-1 signifie non maquillé)
l2d = [-1] * 128
ok = Vrai

pour i dans la plage (p):
si ce n'est pas bien:
pause
pour j dans la gamme q:
num = planche[r + i][c + j]
ch = modèle[i][j]

si ch.isdigit():
si int(ch) != Numéro:
ok = Faux
pause
Autre: # lettre
si d2l[num] 0:
si l2d[ord(ch)] == - 1 :
d2l[num] = ch
l2d[ord(ch)] = nombre
Sinon:
ok = Faux
pause
élif d2l[num] != Ch:
ok = Faux
pause

si oui:
retour [r, c]

retour [-1, -1]
«» "

---

*### 4.3 C++

'`cpp
#incluez <vecteur>
#incluez <string>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> findPattern(vector<vector<int>>& board, vector<string>& pattern) {
int m = board.size(), n = board[0].size();
int p = pattern.size(), q = pattern[0].size();

pour (int r = 0; r + p <= m; ++r) {
pour (int c = 0; c + q <= n; ++c) {
int d2l[10] = {0}; // chiffre -> lettre (0 signifie non maquillé)
int l2d[128];
remplir(début(l2d), fin(l2d), -1); // lettre -> Numéro

bool ok = true;
pour (int i = 0; i < p && ok; ++i) {
pour (int j = 0; j < q && ok; ++j) {
int num = planche[r + i][c + j];
char ch = motif[i][j];

Si (ch >= '0' && ch <= '9') {
si (ch - '0' != num) ok = faux;
} autre { // lettre
si (d2l[num]] 0) {
si [l2d[(int)ch]] -1) {
d2l[num] = ch;
l2d[(int)ch] = nombre;
} autre {
ok = faux;
}
} sinon si (d2l[num] != ch) {
ok = faux;
}
}
}
}

si (ok) retour {r, c};
}
}
retour {-1, -1};
}
};
«» "

---

- Oui. 5. Essais et cas de bord

Autres Essai
- C'est quoi ?
`board = [[0]]`, `pattern = ["a"]`"Cellule unique, cartographie des lettres. Autres
"board = [[5,5],[5,5]", "pattern = ["aa", "aa"]"" Tous les mêmes chiffres – la cartographie doit être cohérente. Autres
"board = [[1,2],[3,4]", "pattern = ["a1", "2b"]"" Mixte chiffre/lettre. Autres
"board" ou "pattern" à la frontière. Autres
"pattern" contenant des lettres répétées avec des chiffres différents. Autres

L'exécution des implémentations fournies par rapport aux cas ci-dessus (et les échantillons de LeetCode) donnent tous les résultats escomptés.

---

- Oui. 6. Conseils d'entrevue

1. **Clarifiez la bijection** – demandez à l'intervieweur si différentes lettres doivent correspondre à différents chiffres.
2. **Parlez à travers vos tableaux de cartographie** – expliquez pourquoi vous avez besoin de deux cartes et comment vous imposez l'unicité.
3. **Discuse la complexité** – soulignez que la force brute est bonne pour les contraintes mais peut être optimisée si la planche est grande.
4. **La pensée d'Edge** – mention d'erreurs hors-par-un et comment vos boucles assurent que nous restons à l'intérieur du tableau.
5. ** Ordre de retour** – soulignez que les lignes itératives garantissent d'abord les plus petites coordonnées.

---

- Oui. 7. Takeaway SEO-optimized

> Maître **LeetCode 2384** (Board Pattern Matching) – un défi classique d'appariement de motifs 2D qui enseigne la cartographie bijective, les stratégies de traversée bidimensionnelle et de sortie précoce. Plongez dans des solutions propres **Java, Python, et C++**, testez les cas de bord, et marchez interviewers à travers votre raisonnement pour atterrir ce rôle de haut niveau à Google, Amazon, ou toute société de haute technologie.

Bon codage, et bonne chance dans votre prochaine interview! C'est ce qu'il a dit.

---

*Préparé par [Votre nom], ingénieur logiciel senior & Codding Interview Coach. *