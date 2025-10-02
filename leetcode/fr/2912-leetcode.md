---
titre: LeetCode 2912. Nombre de façons d'atteindre la destination dans la grille -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2912 – *Nombre de moyens d'atteindre la destination dans la grille*
- Oui. Le bon, le mauvais, et le laid
*Programmation dynamique, Grille, Compte, Prép d'entrevue, Java / Python / C++*

---

- Oui. 1. Récapitulation des problèmes

Vous recevez une grille **1-indexée** de taille `n × m` ( `2 ≤ n,m ≤ 109` ), une cellule source `source = [x1, y1]` et une cellule de destination `dest = [x2, y2]`.
Dans un mouvement, vous pouvez sauter de la cellule `[x1, y1]` à `[x2, y2]` **iff** les deux cellules partagent la même **row** ou la même **colonne** (mais pas la même cellule).

**Objectif :** Compter le nombre de séquences distinctes de mouvements exactement « k » qui se terminent par « est ».
Retourner la réponse modulo `1 000 000 007`.
«1 ≤ k ≤ 105».

> **Pourquoi cela est important pour les entrevues* *
> 1. PDD classique sur une grille avec *restricted* moves.
> 2. Nécessite une compression d'état intelligente – un seul DP de taille 4 fonctionne.
> 3. Démontre la manipulation de grandes dimensions de grille (seulement les formules algébriques matière).

---

- Oui. 2. Les bonnes

Raison
- Oui.
**Temps linéaire** – «O(k)» – 100 000 itérations est trivial. Autres
**O(1) mémoire** – seulement 4 compteurs sont nécessaires. Autres
**Mathématiquement propre** – la matrice de transition est dérivée une fois. Autres
**Language-agnostic** – le même DP fonctionne en Java, Python, C++. Autres
Autres **Pas besoin d'exposer la matrice** – parce que `k` est au plus 105. Autres

---

- Oui. 3. Les mauvais

Piège
- Oui.
`n` et `m` peuvent être aussi grands que `109`, donc vous ** devez** utiliser l'arithmétique 64-bit avant de prendre le modulo. Autres
`k = 1` est un cas *spécial* – vous ne pouvez pas rester sur la même cellule. Autres
Les erreurs hors-par-un dans les comptes de transition (p. ex. `n‐1` vs `n‐2') sont faciles à faire. Autres
Dépassement en multiplication intermédiaire (`long * long` en Java / `int * int` en C++). Autres

---

- Oui. 4. L'Ugly

Erreur de correction
- Oui.
Autres **Restant sur la même cellule**= Autorisé par la règle de la même ligne/colonne uniquement si vous *déplacez* ailleurs. La transition d'"at dest" à "at dest" doit être `0`. Autres
**Le nombre de cellules qui partagent **ni la ligne**, ni la colonne avec `deest'. Autres
En Java/C++ `int * int` déborde avant que nous puissions appliquer `% MOD`. Autres
** Valeurs intermédiaires negatives** Les soustractions comme `m-2` peuvent devenir `-1` si `m=2`. Autres
Autres Le DP initialisé avec la source signalerait incorrectement `1` quand `source= det`. partager une ligne ou une colonne **et** ils ne sont pas la même cellule. Autres

---

- Oui. 5. L'Ugly-ish – Ce qu'il faut surveiller pendant le codage

Qu'est-ce qui peut mal tourner
Récapitulatif
**La transition erronée compte** – le double comptage ou l'absence d'un chemin mène à une mauvaise réponse. Autres
**Débordement entier avant modulo** – en particulier en Java ('int' est 32-bit). Autres
**Wrong état initial** – erreur de classification de la source comme «out» quand il est réellement sur la même ligne. Autres
**Performance frappe de boucles imbriquées** – 4×4×k est bien, mais l'utilisation d'une boucle imbriquée naïve pour chaque étape `k` peut être plus lente en Python si elle n'est pas écrite efficacement. Autres
**Fourni de gérer `k = 1`** – de nombreux concurrents produisent 1 pour `source == dest`.

---

- Oui. 3. Aperçu de base – 4 types de cellules

Au lieu de penser à *chaque cellule dans la grille, nous ne nous soucions que de sa relation* à la destination:

Type Condition Symbole
C'est quoi ?
**Out** – actions **ni la ligne** ni la colonne avec `dest` ** et** y y y y2 '
**Row** – même ligne que `deest`, colonne différente ** et** y y y y2 '
**Col** – même colonne que `est`, ligne différente=y=y2` ** et** < x x 2 > 2
**À** – exactement la destination ** et** `y = y2`

Seulement **quatre** compteurs sont requis: `cntOut, cntRow, cntCol, cntAt`.
Après chaque déplacement, tous les compteurs sont mis à jour simultanément en utilisant une matrice de transition fixe.

---

- Oui. 4. Matrice de transition

Let `MOD = 1 000 000 007`.
Laissez `i` être l'état actuel, `j` l'état suivant.

À partir de\To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To-To
C'est pas vrai.
*Out** *n+m-4 *1 *1 *1 *0 *
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
*Col. * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
**À**

**Pourquoi ces chiffres? **

* A partir d'une cellule *hors* de la ligne/col dest.
* sauter à n'importe quelle autre cellule extérieure – il ya `(m-1)+(n-1)-2 = n+m-4` de telles cellules,
* sauter à la seule cellule dans la même rangée que det – **1**,
* sauter à la seule cellule dans la même colonne que det – **1**.
* A partir d'une cellule *dans la même rangée* que celle de:
* sauter à n'importe quelle autre cellule dans cette rangée – `n-1`
* rester dans la même rangée, mais éviter les cellules `m-2`,
* sauter tout droit à destination – **1**.
* Les deux autres cas sont symétriques.
* De la destination, vous ne pouvez partir que – pas de transition de séjour.

Tous les nombres sont d'origine algébrique** de `n` et `m` et sont sûrs de calculer avec 64 bits entiers même pour `n,m = 109`.

---

- Oui. 5. Itération du PDD

«» "
dp[i] – nombre de façons d'être dans l'état i après le nombre actuel de mouvements
next[i] – même mais après un mouvement supplémentaire
«» "

«» "
pour l ' étape = 1 ... k-1
suivant[0...3] = 0
pour i en 0,3
pour j en 0,3
suivant[j] = (suivant[j] + dp[i] * T[i][j]) mod MOD
dp = suivant
réponse = dp[At] // nombre de voies qui se terminent après les déplacements de k
«» "

*Temps* : 'O(4·4·k) "
* Mémoire* : compteurs `O(4)` → `O(1)`

---

- Oui. 6. Manipulation spéciale pour `k = 1`

Quand `k == 1' nous ne pouvons pas rester dans la même cellule.
Les seuls chemins valides sont les sauts directs qui partagent une ligne ** ou** une colonne:

Texte
réponse = 1 si (source[0] == det[0] et source[1] != det[1]) // même ligne
ou (source[0] != dest[0] et source[1] == dest[1]) // même colonne
Autre 0
«» "

---

- Oui. 7. Mise en œuvre des références

Voici des solutions entièrement commentées pour **Java, Python et C++** qui suivent exactement la même logique DP.

---

#### 7.1 Java 17

"Java
solution de classe publique {
finale statique privée longue MOD = 1_000_000_007L;

// Indices d'état
int final statique privé OUT = 0, ROW = 1, COL = 2, AT = 3;

Nombre d'entrées publiques DeWays(int n, int m, int k, int[] source, int[] dest) {
- Oui. 1. Cas spécial k] 1 ----------------- */
si (k) 1) {
booléen memeRow = source[0] == dest[0] && source[1] != dest[1];
boolean sameCol = source[1] == dest[1] && source[0] != dest[0];
retour (mêmeRow) ? 1 : 0;
}

- Oui. 2. Matrice de transition ------------------- */
long[][] T = nouveau long[4][4];

// De l ' extérieur
[OUT] = n + m - 4;
T[OUT][ROY] = 1;
T[OUT][COL] = 1;
// T[OUT][AT] reste 0

// De la rue
[ROW] [OUT] = n - 1;
T[ROW][ROW] = m - 2;
T[ROW][AT] = 1;

// À partir de COL
T[COL][OUT] = m - 1;
T[COL][COL] = n - 2;
T[COL][AT] = 1;

// De AT (destination)
T[AT][ROW] = m - 1;
T[AT][COL] = n - 1;
// T[AT][AT] reste 0

- Oui. 3. Vecteur initial DP ------------------- */
long[] dp = nouveau long[4];
si (source[0] == det[0] && source[1] == det[1]) {
dp[AT] = 1;
} sinon si (source[0]]
dp[ROW] = 1;
} sinon si (source[1]) {
dp[COL] = 1;
} autre {
dp[OUT] = 1;
}

- Oui. 4. Itérations PDD ---------------------- */
pour (int step = 1; step < k; step++) {
long[] suivant = nouveau long[4];
pour (int i = 0; i < 4; i++) {
pour (int j = 0; j < 4; j++) {
si [T[i][j]] 0) continuer; // sauter les entrées zéro
next[j] = (next[j] + dp[i] * T[i][j]) % MOD;
}
}
dp = suivant;
}

- Oui. 5. Résultat */
retour (int) dp[AT];
}
}
«» "

---

7.2 Python 3.10

'`python
Solution de classe:
MOD = 10**9 + 7
OUT, ROW, COL, AT = 0, 1, 2, 3

Numéro DeWays(self, n: int, m: int, k: int,
Source: List[int], det: List[int] -> Int:
C'est pas vrai. 1 manipulation spéciale - Oui.
Si k == 1:
meme_row = source[0] == det[0] et source[1] != det[1]
même_col = source[1] == det[1] et source[0] != det[0]
retourner int(même_row ou même_col)

C'est... Matrice de transition - Oui.
T = [[0] * 4 pour _ dans la plage(4)]

# De dehors
[SANS] [SANS] = n + m - 4
[Self.OUT][Self.row] = 1
[Self.OUT][Self.COL] = 1

De la rue
[Self.row][Self. OUT] = n - 1
T[self.row][self.row] = m - 2
T[self.row][self.AT] = 1

# De COL
T[self.COL][self. OUT] = m - 1
[Self.COL][Self.COL] = n - 2
T[self.COL][self.AT] = 1

# De l'AT
T[self.AT][self.row] = m - 1
T[self.AT][self.COL] = n - 1

C'est... Vecteur initial
dp = [0] * 4
Si la source[0] == det[0] et la source[1] == det[1]:
moi-même. AT] = 1
Dénomination des marchandises
moi-même. ROW] = 1
dest[1]:
moi-même. COL] = 1
Sinon:
moi-même. OUT] = 1

C'est... Les itérations du PDD...
pour _ dans la gamme(1, k): # nous avons déjà géré l'étape 1
nxt = [0] * 4
pour i dans la plage(4):
si dp[i] == 0:
poursuivre
pour j dans la plage(4):
si T[i][j] == 0:
poursuivre
nxt[j] = (nxt[j] + dp[i] * T[i][j]) % soi-même. MOD
dp = nxt

retour int(dp[self.AT])
«» "

---

### 7.3 C++20

'`cpp
solution de classe {
public:
Constexpr statique long MOD = 1'000'000'007LL;
// Indices d'état
OUT = 0, ROW = 1, COL = 2, AT = 3;

Numéro int DeWays(int n, int m, int k, vecteur<int>& source, vecteur<int>&dest) {
- Oui. 1 cas particulier
si (k) 1) {
bool sameRow = source[0] == dest[0] && source[1] != dest[1];
bool sameCol = source[1] == dest[1] && source[0] != dest[0];
retour (mêmeRow) ? 1 : 0;
}

- Oui. matrice de transition
longue longue T[4][4] = {}; //
T[OUT][OUT] = (long)n + m - 4;
T[OUT][ROY] = 1;
T[OUT][COL] = 1;

[ROW] [OUT] = n - 1;
T[ROW][ROW] = (long)m - 2;
T[ROW][AT] = 1;

T[COL][OUT] = m - 1;
T[COL][COL] = n - 2;
T[COL][AT] = 1;

T[AT][ROW] = (long)m - 1;
T[AT][COL] = (long)n - 1;

/* ------------- Vecteur DP initial --------- */
long dp[4] = {0,00,0};
si (source[0] == det[0] && source[1] == det[1]) dp[AT] = 1;
sinon si (source[0] == det[0]) dp[ROW] = 1;
sinon si (source[1] ==dest[1]) dp[COL] = 1;
sinon dp[OUT] = 1;

- Oui. PDD itérations --------- */
pour (int pas = 1; pas < k; + + pas) {
long nxt[4] = {0,00,0};
pour (int i = 0; i < 4; ++i) {
si (dp[i]] 0) poursuivre;
pour (int j = 0; j < 4; ++j) {
si [T[i][j]] 0) poursuivre;
nxt[j] = (nxt[j] + dp[i] * T[i][j]) % MOD;
}
}
la taille du(dp);
}
retour (int)dp[AT];
}
};
«» "

---

- Oui. 8. Pensées finales

* La solution se résume à **quatre compteurs** et une matrice de transition **fixée**.
* Tous les nombres de chemins sont exprimés en fonctions algébriques simples de `n` et `m`.
* La manipulation attentive de `k = 1` et la promotion aux types 64-bits garantissent la justesse.

Avec cette compréhension, vous pouvez implémenter la solution dans n'importe quelle langue sans tomber dans les pièges typiques. Bon codage !

---

- Oui. 9. Lecture supplémentaire (facultative)

* ** Programmation dynamique sur les graphiques** – pourquoi la réduction d'état fonctionne.
* **Comptabilité algébrique des chemins** – voir interprétations combinatoires des comptes de transition.
* **Arithmétique modulaire en 64 bits** – pièges dans des langues comme Java/C++/Python.

---

*Bonne résolution de problème! *