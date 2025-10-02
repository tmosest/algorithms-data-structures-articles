---
titre: LeetCode 2992. Nombre de permutations autodivisibles -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2992 – *Nombre de permutations autodivisibles*
**Langues**: Java, Python, C++
**Difficulté**: Moyenne
**Max n**: 12

> **Balises de référence**:
> `LeetCode 2992`, `auto-permutations divisibles`, `programmation dynamique bitmask`, `Java solution`, `Python solution`, `C++ solution`, `job interview coding`, `algorithmes interview`, `bitmask DP`

---

Déclaration du problème (courte)

Compter le nombre de permutations du tableau 1 indexé `nums = [1, 2, ..., n]` satisfaire
`gcd(nums[i], i) == 1' pour chaque «1 ≤ i ≤ n».
La longueur du tableau est au maximum **12**.

---

Intuition

L'exigence est locale: lorsque nous décidons de l'élément qui va en position `i`, nous devons seulement vérifier s'il est coprime avec `i`.
Ceci suggère une programmation dynamique *state‐by‐state* où l'état enregistre les nombres déjà placés.

Parce que `n ≤ 12`, un masque 12-bit (ou 64-bit entier en C++) peut encoder efficacement l'ensemble des nombres utilisés.
Laissez `masque` être tel que le bit `j‐1` est `1` si le nombre `j` a déjà été placé.
Si `mask` a des bits `k`, alors la position libre suivante est `k + 1`.

De l'état `masque`, nous essayons chaque nombre `x` inutilisé (`1 ... n`).
Si `x` est coprime avec la nouvelle position `k+1`, nous pouvons la placer et la transition vers `masque=1 << (x-1)`.
La valeur DP `dp[masque]` est le nombre de moyens valables pour remplir exactement les postes décrits par le «masque».

---

Algorithme (Bitmask DP)

1. `S = 1 << n` – nombre total de masques.
2. `dp[0] = 1` – l'arrangement vide est un moyen.
3. Pour chaque `masque` de `0` à `S-1`:
* `k = popcount(mask)` – nombres déjà placés.
* `pos = k + 1` – indice de la position suivante à remplir.
* Pour chaque nombre `x` (`1 ... n`):
* si le bit `x-1` est **unset** dans `mask` **et** `gcd(x, pos) == 1'
puis «dp[mask]» (1 << (x-1))] += dp[mask]».
4. La réponse est `dp[S-1]` – tous les nombres utilisés.

> **Complexité temporelle**: 'O(2^n * n) "
> **Complexité spatiale**: 'O(2^n) "
> Avec `n ≤ 12', c'est parfaitement bien (opérations `2^12 * 12 ' 49k').

---

Mise en œuvre du code

Ci-dessous vous trouverez des solutions propres et prêtes à coller dans **Java**, **Python** et **C++**.
Tous les trois partagent la même logique et sont fortement commentés par souci de clarté.

---

#### Java 17

"Java
Importation de java.util.*;

solution de classe {
public int autodivisiblePermutationCount(int n) {
Total Masque = 1 << n; // 2^n
int[] dp = nouveau int[total Mask];
dp[0] = 1; // permutation vide

pour (int masque = 0; masque < total Masque; masque++) {
si (dp[masque]) 0) continuer; // aucune façon d'atteindre cet état

int placé = Integer.bitCount(masque); // nombres déjà utilisés
int suivant Pos = placé + 1; // index suivant à remplir

pour (int x = 1; x <= n; x++) {
// sauter si x déjà utilisé
si ((masque et (1 << (x - 1))) != 0) poursuivre;

// contrôle de coprime
si (gcd(x, nextPos) == 1) {
int newMask = masque () (1 << (x - 1));
dp[newMask] += dp[mask];
}
}
}
retour dp[total Masque - 1];
}

/** Algorithme d'Euclid */
Int privé gcd(int a, int b) {
pendant que (b != 0) {
t = a % b;
a = b;
b = t;
}
retour a;
}
}
«» "

---

Python 3

'`python
Solution de classe:
def autoDivisiblePermutationCount(self, n: int) -> Int:
_masque total = 1 << n # 2^n
dp = [0] * total_masque
dp[0] = 1

pour masque dans l'intervalle(total_masque):
si dp[mask] == 0:
poursuivre

placé = bin(mask).count("1") nombres déjà utilisés
pos = placé + 1 # prochain indice

pour x dans la plage(1, n + 1):
Si masque & (1 << (x - 1)):
continuer # déjà utilisé

si self._gcd(x, pos) == 1 :
nouveau_masque = masque
dp[new_mask] += [masque]

retour dp[total_mask - 1]

@staticmethod
def _gcd(a: int, b: int) -> Int:
tandis que b:
a, b = b, a % b
retour a
«» "

---

C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int autoDivisiblePermutationCount(int n) {
Total Masque = 1 << n; // 2^n
vecteur<int> dp(total le masque 0);
dp[0] = 1; // disposition vide

pour (int masque = 0; masque < total Masque; + masque) {
si (!dp[mask]) continue;

int placé = __constructin_popcount(masque);
int pos = placé + 1; // index suivant

pour (int x = 1; x <= n; ++x) {
si (masque & (1 << (x - 1))) continuer; // déjà utilisé

si [gcd(x, pos)] 1) {
int newMask = masque () (1 << (x - 1));
dp[newMask] += dp[mask];
}
}
}
retour dp[total Masque - 1];
}

particulier:
int gcd(int a, int b) {
pendant que b) {
t = a % b;
a = b;
b = t;
}
retour a;
}
};
«» "

---

Bonne, mauvaise et moche

Aspect du bien
- C'est quoi ?
**Algorithme**= Bitmask DP utilise tous les 2n états une fois → optimum pour n ≤ 12= La complexité temporelle `O(2n·n)` croît de façon exponentielle, mais n est minuscule== Aucun – algorithme est propre==
**Mise en œuvre**=Loop simple sur les masques + les opérations de bits. L'oubli de la vérification `gcd` peut produire une mauvaise réponse.
**Alternative de rétro-suivi** – beaucoup plus lent pour n=12.
**Readability**= Self-documenting with comments== Peut sembler dense aux nouveaux arrivants== S/O
**Space**=O(2n) int array=__________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

---

Pourquoi c'est un bon point d'entrevue

1. **Compression d'état** – Utiliser un bitmask pour coder les nombres utilisés montre la maîtrise du DP combinatoire.
2. **Insight spécifique au problème** – Reconnaître que la position suivante dépend seulement du nombre de numéros déjà placés.
3. **Efficient GCD Check** – L'algorithme Euclide est standard; vous pouvez mentionner le potentiel de cache des résultats si nécessaire.
4. ** Discussion sur l'évolutivité** – Vous pouvez expliquer pourquoi cette approche fonctionne jusqu'à `n = 12`, mais elle se briserait pour `n` plus grande, et quelles alternatives (par exemple, inclusion-exclusion) vous pourriez envisager.

---

Liste de contrôle à emporter

- Utiliser un DP bitmask pour les contraintes combinatoires avec `n ≤ 20`.
- Nombre utilisé avec `popcount` (`_builtin_popcount`, `Integer.bitCount` ou `bin(mask.count`).
- La transition vers la position *next* (`k+1`) uniquement.
- Vérifier la conformité avec le « gcd ».
- Retour `dp[(1<<n)-1]`.

---

Prêt à impressionner les recruteurs ?

Utilisez les extraits de code Java / Python / C++ ci-dessus comme votre code « show‐off ».
Expliquez l'intuition et parlez à travers la table de bon/mauvais/mauvais dans une interview de niveau suivant – vous allez clouer que LeetCode 2992 question et démontrer le genre de pensée algorithmique recruteurs aiment!