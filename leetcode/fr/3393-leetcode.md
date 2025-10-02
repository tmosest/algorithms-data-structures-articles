---
titre: LeetCode 3393. Compter les chemins avec la valeur XOR donnée -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. LeetCode 3393 – Compter les chemins avec la valeur XOR donnée
**Langues**: Java, Python, C++
**Complexité temporelle**: O(m · n · 16)
**Complexité spatiale**: O(m · n · 16) (ou O(m · 16) lorsque nous utilisons la version optimisée spatiale)

Ci-dessous vous trouverez trois solutions idiomatiques:

Style Espace Remarques
- C'est quoi ?
U(m · n · 16)
Python Python Python Python O(m · n · 16) Utilisations `defaultdict`/compréhension de la liste
U(m · 16)

> **Conseil pour les entrevues** – Montrez à l'intervieweur que vous comprenez pourquoi les valeurs XOR ne sont que de 0 à 15 (valeurs réseau < 16). C'est la clé pour garder le DP petit.

---

#### 1.1 Java – mémoisation en haut

"Java
Importation de java.util.*;

solution de classe publique {
int final statique privé MOD = 1_000_000_007;
Int m, n, k;
grille privée int[];
Int[][][][] note; // note[i][j][xor]

int public countPathsWithXorValue(int[]] grille, int k) {
Ça. grille = grille;
k = k;
ce.m = longueur de grille;
cette.n = grille[0].longueur;
mémo = nouvelle int[m][n][16];
pour (int[]] ligne : mémo) {
pour (int[] arr : rang) Arrays.fill(arr, -1);
}
retour dfs(0, 0, 0);
}

Int privé dfs(int i, int j, int curXor) {
si (i >= m) j >= n) retourne 0;
curXor ^= grille[i][j];
si (i == m - 1 && j == n - 1) retour curXor == k ? 1 : 0;
Int & = mémo[i][j][curXor];
si (& != -1) retour &;
int droite = dfs(i, j + 1, curXor) % MOD;
Int down = dfs(i + 1, j, curXor) % MOD;
retour [i][j][curXor] = (droit + bas) % MOD;
}
}
«» "

---

#### 1.2 Python – PDD ascendant (table complète)

'`python
Solution de classe:
MOD = 1 000 000 007

def countPathsWithXorValue(self, grid: List[List[int]], k: int) -> Int:
m, n = len(grid), len(grid[0])
# dp[i][j][xor] -> chemins de (i,j) à la fin avec xor actuel
dp = [[[0] * 16 pour _ dans la plage (n + 1)] pour _ dans la plage (m + 1)]
dp[m-1][n-1][grid[m-1][n-1] ^ k] = 1

pour i dans la plage (m-1, -1, -1):
pour j dans la plage (n-1, -1, -1):
pour x dans la plage(16):
nouvelle_x = x ^ grille[i][j]
si j + 1 < n:
dp[i][j][x] = (dp[i][j][x] + dp[i][j+1][new_x]) % soi-même. MOD
i + 1 < m:
dp[i][j][x] = (dp[i][j][x] + dp[i+1][j][new_x]) % self. MOD
retour dp[0][0][0]
«» "

---

### 1.3 C++ – PDD optimisé pour l'espace (deux lignes)

'`cpp
solution de classe {
public:
MOD = 1'000'000'007;

int countPathsWithXorValue(vecteur<vector<int>>& grille, int k) {
int m = quadrillage(), n = quadrillage[0].size();
vector<vector<int>> suivant(n + 1, vector<int>(16, 0));
suivant[n-1][k] = 1; // scénario de base

pour (int i = m-1; i >= 0; --i) {
vecteur<vector<int>> cur(n + 1, vecteur<int>(16, 0));
pour (int j = n-1; j >= 0; --j) {
pour (int x = 0; x < 16; ++x) {
int newX = x ^ grid[i][j];
(j+1 < n ? cur[j+1][newX] : 0) +
(i+1 < m ? suivant[j][newX] : 0) ) % MOD;
}
}
suivant.swap(cur);
}
retour suivant[0][0];
}
};
«» "

---

- Oui. 2. Article de blog – Le bon, le mauvais, et le mauvais de LeetCode 3393

> ** Mots clés du référencement**:
> *Leetcode 3393*, *Count Paths With the Donated XOR Value*, *dynamique de programmation XOR*, *software engineer interview*, *grid path computing*, *XOR path problems*, *job interview algorithmes*, *DP tricks*, *space-optimized DP*, *job-search guide*

2.1 Capture de problème

> **Nom** – Compter les chemins avec la valeur XOR donnée
> **Difficulté** – Moyenne
> ** Contraintes principales**
> - Taille de grille jusqu'à 300 × 300
> - Chaque valeur de cellule < 16 (4 bits)
> - Cible XOR `k` < 16
> - Réponse de retour modulo `10^9 + 7`

Le problème se pose : *Combien de façons pouvez-vous marcher de la cellule supérieure gauche à la cellule inférieure droite, se déplaçant seulement à droite ou en bas, de sorte que le XOR de toutes les valeurs cellulaires visitées égale `k`? *

> **Pourquoi les valeurs XOR restent minuscules** – Parce que chaque cellule est 0-15, le XOR cumulatif est toujours 0-15. Cela nous permet de garder une dimension DP de taille 16 plutôt que `2^16` ou `1e9`.

---

2.2 Les bons

Autres Qu'est-ce qui est génial ? Pourquoi ça compte ? Autres
- Oui.
Autres **Espace petit état** – 4 bits XOR → 16 états DP par cellule. Rendre possible O(m · n · 16). Autres
**PDD classique sur une grille** – La même récurrence apparaît dans les Voies Uniques II (avec obstacles) ou Minimum Path Sum. Les candidats peuvent réutiliser des modèles familiers. Autres
**Intutions claires de base** – À la destination, nous vérifions si le dernier XOR correspond à `k`. Autres
**Potentiel d'optimisation de l'espace** – Seules deux lignes sont nécessaires, car le mouvement est monotonique. Réduit la mémoire de ~108 Mo à ~6 Mo en C++. Autres

> **Interview Insight** – Demandez à l'intervieweur : * Avons-nous vraiment besoin de 300 × 300 × 16 mémoires?* La réponse : « Non – nous pouvons la compresser à « m·16 » ». Cela met en évidence la pensée algorithmique.

---

2.3 Les mauvais

Un piège commun
-- -- -- -- --
**Utiliser un DP 2-D sans dimension XOR** – Ne pas se souvenir que XOR peut changer l'état. Ajouter une troisième dimension: "dp[i][j][xor]". Autres
**Ignorer le modulo à chaque étape** – Dépassement sur `int`. Autres
**Profondeur de récursion > 1000** – Cause le débordement de la pile sur 300 × 300 grilles. Soit augmenter la limite de récursion (Python) soit utiliser le DP itératif. Autres
**Treating XOR en tant qu'additif** – Perturbation de XOR pour ajout. Rappel: `newX = oldX ^ cellVal`. Autres

> **Pourquoi ce sont des Ils transforment un PDD propre en un désordre difficile à comprendre, et ils seront les premières choses que l'intervieweur attrapera.

---

2.4 La moche

1. **DSE de la force brute**
'`python
def dfs(i, j, cur_xor):
if i==m-1 et j==n-1: retourner cur_xor==k
# explorer les deux branches
«» "
*Temps:* O(2^(m+n) – impossible.

2. **Bitmasking 2 16 États**
'`python
dp[i][j][masque] # masque en 0,65535
«» "
* Espace:* 10 Go pour 300 × 300.
*Résultat:* Crash de mémoire.

3. **Mémotisation récursive sans élagage**
Sans l'observation 4 bits, on pourrait pré-alloquer «dp[m][n][65536]», qui à nouveau exploser.

> **Pourquoi c'est moche** – L'approche naïve montre un manque de perspicacité. Les entretiens pénalisent les candidats qui commencent par un immense espace d'État.

---

### 2.5 Mise en oeuvre

1. **Définition de l'État**
Texte
dp[i][j][xor] = nombre de voies à atteindre (m-1, n-1)
à partir de (i, j) alors que xor cumulé actuel = xor
«» "
2. **Transition**
- À droite: `dp[i][j][xor] +=dp[i][j+1][xor ^ grid[i][j]`
- Déplacer vers le bas: `dp[i][j][xor] += dp[i+1][j][xor ^ quadrillage[i][j]`
Toutes les opérations sont prises en modulo 'MOD '.

3. **Dossier de base**
À `(m-1, n-1)`:
Texte
dp[m-1][n-1][grid[m-1][n-1] ^ k] = 1
«» "
Parce que nous voulons que le xor final soit `k`, le xor *current* à la destination doit être `grid[m-1][n-1] ^ k`.

4. **Ordre de remplissage**
- En haut du coin inférieur droit au coin supérieur gauche.
- Parce que nous ne faisons référence qu'aux cellules de droite ou de dessous, le DP respecte la règle du chemin monotonique.

5. ** Optimisation de l'espace**
Seules les lignes actuelles et suivantes sont nécessaires :
Texte
nextRow[j][xor] <-- voies commençant par (i+1, j)
curRow[j][xor] <-- les voies commençant par (i, j)
«» "
La boucle intérieure sur les 16 xor reste.

---

Pourquoi le Trick XOR compte

Autres Que se passerait-il si les valeurs cellulaires étaient jusqu'à 109? Et si `k` était jusqu'à 109 ? Autres
Il n'y a pas de différence entre les deux.
Autres Le XOR pourrait devenir 32 bits → 232 états. Même – 232 états. Autres
La mémoire exploserait (soit 300 · 300 · 4 · 109 octets). Impossible. Autres
Autres Nous avions besoin de *bit‐DP* ou *meet‐in‐the‐middle*. Nous avons changé d'algorithme (par exemple BFS + bitset). Autres

En raison de la contrainte **4-bit**, le DP reste minuscule, et le problème est solvable avec un DP ordinaire.

---

2.7 Entretien— Conseils prêts

Situation Que dire
C'est pas vrai.
**Asked pour une solution O(m · n)**= Nous ne pouvons garder que deux rangées de tableaux de 16 éléments – ce qui est le DP standard optimisé pour l'espace. Autres
**Il s'agit d'une solution récursive. Récursion maintient le code propre, mais regardez la profondeur de la pile. Autres
**Vous voulez savoir pourquoi le modulo est utilisé.** Nous le conservons dans la gamme 64 bits, puis dans le mod 109 + 7 à chaque ajout. Autres
Autres **Le DP est de 16 × m × n pour les opérations de 1,44 × 106 pour la grille maximale, ce qui est confortablement sous la limite de 2 s de LeetCode. Autres
**Demande une optimisation**=Si la mémoire est une préoccupation, nous pouvons laisser tomber la troisième dimension d'une table 3-D complète à une table 2-D de `m` × 16 ou même `n` × 16.= Autres

---

#### 2.8 Liste de contrôle pour l'essai de votre solution

Scénario Résultats escomptés
-- -- -- -- -- -- -- --
1 × 1 grille "[k]" 1 (le seul chemin)
Autres Tous les zéros, `k` = 0. Autres
Griller tous les 1, `k` = 1=0 (longueur od → XOR = 1, mais la longueur du chemin est m+n‐1, vérifier la parité)=
Faire fonctionner une force brute pour n=5 pour vérifier. Autres

---

###2.9 Conclusion – Comment utiliser ceci dans votre chasse à l'emploi

* **Showcase DP + Bit-wise perspicacité** – Beaucoup d'intervieweurs cherchent la capacité de repérer des opportunités de compression d'état.
* ** Expliquer l'optimisation de l'espace** – Il démontre que vous pouvez lire les contraintes du problème et serrer la mémoire.
* **Discute de l'astuce XOR** – Il s'agit d'un thème d'entrevue commun; de nombreuses variations (problèmes de chemin ET/OU) apparaissent.
* **Pratique sur le LeetCode** – Ajoutez le problème à votre liste d'options et conservez le code dans votre GitHub pour une référence rapide.

> ** Pensée finale** – Mastering LeetCode 3393 vous enseigne comment transformer un état apparemment exponentiel en DP linéaire en tirant parti du problème de propriété cachée 4 bits. Cette compétence est un parfait exemple de l'élégance algorithmique que vous souhaitez afficher lors de votre prochain entretien d'ingénierie logicielle.

---

Joyeux codage – et heureux entretien! C'est ce qu'il a dit