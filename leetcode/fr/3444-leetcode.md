---
titre: LeetCode 3444. Augmentations minimales pour les multiples cibles dans un tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
3444 – Augmentations minimales pour les multiples cibles
> LeetCode DP + Bitmask**

---

TL;DR

Temps Mémoire
- C'est quoi ?
**Java**** 1 MB
**Python**
Mêmes asymptotiques, ~0,08 s

*`n` = `nums.length` (=5 000 000) – en fait 5 × 104 dans l'énoncé*
*`m` = `cible.longueur` (=4)*

La clé est de pré-calculer le **LCM de chaque sous-ensemble** de "cible".
Chaque `nums[i]` peut être incrémenté au multiple suivant de tout sous-ensemble de LCM, et
nous utilisons un DP classique sur bitmasks pour décider *quel* sous-ensemble chaque élément
sera satisfait.

---

- Oui. 1. Remise en état des problèmes

On vous donne deux tableaux entiers `nums` et `cible`.
Vous pouvez **incrémenter n'importe quel élément de "nums" par 1 n'importe quel nombre de fois**.
Après toutes les opérations, pour **chaque** élément `t` dans `cible`,
il doit y avoir au moins un élément `x` dans `nums` tel que `x % t == 0`.

Retournez le nombre total minimum d'augmentations* requis.

---

- Oui. 2. Pourquoi Bitmask DP?

`cible` est minuscule (- 4).
- Chaque élément de "nums" peut être transformé en un multiple de **tout sous-ensemble** de
les numéros cibles, pas seulement un à la fois.
- Le sous-ensemble qu'un "nums[i]" particulier couvre peut être représenté par un
bitmasque de longueur `m`.
Pour `m = 3`, masque `011` signifie que l'élément devient un multiple de
«cible[0]» et «cible[1]».

Avec `m ≤ 4` nous n'avons que `2^m ≤ 16` états – assez petits pour un DP exhaustif.

---

- Oui. 3. Aperçu de l ' algorithme

1. **Pré-calculer les ML**
Pour chaque masque non vide `s` (1 ... 2^m‐1) calculer
`lcm[s] = lcm(cible[i]= s_i == 1)`.

2. ** Programmation dynamique sur masques**
`dp[masque]` = coût minimal pour satisfaire *exactement* les objectifs dans `masque`
(en utilisant un certain nombre d'éléments du préfixe traité jusqu'à présent).

Initialiser: `dp[0] = 0`, autres = INF.

3. **Processus de chaque élément "nums"* *
Pour l'élément actuel `x "
* calculer le coût `coûts` pour faire `x` un multiple de `lcms` pour
tous les masques "
«coût[s] = (lcm[s] - x % lcm[s]) % lcm[s]».

* Mettre à jour le DP : pour chaque oldMask et chaque sous-ensemble s
Texte
newMask = ancien Masque
dp[newMask] = min(dp[newMask], dp[oldMask] + coût[s])
«» "

* Le cas de l'élément "skip" est implicite parce que `dp` est copié
dans `newdp` avant les mises à jour.

4. **Réponse**
Après traitement de tous les éléments, `dp[(1<<m)-1]` est le minimum
incréments nécessaires pour toutes les cibles.

La complexité est
"O(n · 2^m · 2^m)" → avec des opérations `m ≤ 4`, facilement rapides
Assez.

---

- Oui. 4. Cas de coin et correction

Bordure Que se passe-t-il ? Autres
- C'est quoi ?
"cible" déjà couverte par "nums" séjours Pour chaque élément, nous pouvons définir `cost[s] = 0` si c'est déjà un multiple. Autres
Quelques cibles > tous les nombres Nous serons toujours en mesure d'augmenter un élément pour l'atteindre.Le DP explore toutes les possibilités, y compris en utilisant de nombreux incréments. Autres
Le dépassement du LCM est toujours en 32 bits, mais nous utilisons le « long » pour la sécurité. Autres
Empty `nums` Le problème garantit `nums.longueur ≥ 1'' Pas nécessaire. Autres
Plusieurs solutions optimales de DP maintient un coût minimal. Autres

---

- Oui. 5. Code – Java

"Java
Importation de java.util.*;

solution de classe {
Infraction(int[] nombres, int[] cible) {
int m = cible. longueur;
int allMask = (1 << m) - 1;
longue[] lcm = nouveau long[1 << m];
// 1. pré-calculer lcm pour chaque sous-ensemble
pour (int mask = 1; masque <= allMask; mask++) {
longue courbure = 1;
pour (int i = 0; i < m; i++) {
si ((masque & (1 << i)) != 0) {
cur = lcm(cur, cible[i]);
}
}
lcm[masque] = cur;
}

INF longue finale = Long.MAX_VALUE / 4;
long[] dp = nouveau long[1 << m];
les tableaux.fill(dp, INF);
dp[0] = 0;

// 2. traiter chaque élément nums
pour (int x : nombres) {
long[] suivant = dp.clone(); // cas de saut
// coût de pré-calcul pour ce x
long[] coût = nouveau long[1 << m];
pour (int mask = 1; masque <= allMask; mask++) {
long r = x % lcm[masque];
coût[masque] = (r == 0) ? 0 : lcm[masque] - r;
}
// PDD transition
pour (int old = 0; old <= allMask; old++) {
si (dp[old] == INF) continuer;
pour (int sub = 1; sub <= allMask; sub++) {
int newMask = ancien sous-groupe;
long cand = dp[old] + coût[sub];
si (cand < next[newMask]) next[newMask] = cand;
}
}
dp = suivant;
}
retour (int) dp[allMask];
}

// --------- aide ---------
privé long gcd(long a, long b) {
retour b == 0 ? a : gcd(b, a % b);
}

privé long lcm(long a, long b) {
retourner a / gcd(a, b) * b; // aucun dépassement parce que les valeurs ≤ 104
}
}
«» "

---

- Oui. 6. Code – Python

'`python
d'importation de mathématiques gcd
de taper l'importation Liste

Solution de classe:
def minimumIncrement(self, nombres: List[int], cible: List[int]) -> Int:
m = len(cible)
pleine = (1 << m) - 1
lcm = [0] * (1 << m)

# 1. pré-calculer lcm de chaque sous-ensemble
pour masque de portée(1, 1 << m):
cur = 1
pour i dans la plage (m):
si masque & (1 << i):
cur = cur // gcd(cur, cible[i]) * cible[i]
lcm[masque] = cur

INF = 10 ** 18
dp = [INF] * (1 << m)
dp[0] = 0

2. itérer à travers les nums
pour x en nombres:
new_dp = dp[:] # case skip
# coûts pour chaque sous-ensemble
Coût = [0] * (1 << m)
pour masque de portée(1, 1 << m):
r = x % lcm[masque]
coût[masque] = 0 si r == 0 autre lcm[masque] - r
PDD transition
pour les vieux de portée(1 << m):
si dp[old] == INF:
poursuivre
pour les sous-groupes de la gamme(1, 1 << m):
nouveau_masque = ancien(e) sous
val = dp[old] + coût[sub]
si val < new_dp[new_mask]:
new_dp[new_mask] = val
dp = new_dp

retour int(dp[full])
«» "

---

- Oui. 7. Code – C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minimumIncrement(vecteur<int>& nums, vecteur<int>& cible) {
int m = cible.size();
Int pleine = (1 << m) - 1;
vecteur <long> lcm(1 << m, 1);

// ---- pré-calculer la ML pour chaque sous-ensemble ----
pour (int masque = 1; masque <= plein; ++masque) {
longue courbure = 1;
pour (int i = 0; i < m; ++i)
si (masque et (1 << i))
cur = lcm(cur, cible[i]);
lcm[masque] = cur;
}

longue INF = (1LL < < 60);
vecteur <long> dp(1 << m, INF);
dp[0] = 0;

// ---- traiter chaque élément des nombres ----
pour (int x : nombres) {
vector<long long> newdp = dp; // cas de saut
coût vectoriel <long>(1 << m, 0);
pour (int masque = 1; masque <= plein; ++masque) {
long r = x % lcm[masque];
coût[masque] = (r == 0) ? 0 : lcm[masque] - r;
}

pour (int old = 0; old <= full; ++old) {
si (dp[old] == INF) continuer;
pour (int sub = 1; sub <= full; ++sub) {
int newMask = ancien sous-groupe;
long val = dp[old] + coût[sub];
si (val < newdp[newMask]) newdp[newMask] = val;
}
}
dp.swap(newdp);
}
retourner static_cast<int>(dp[full]); // s'adapte à int
}

particulier:
long gcd(long long a, long b) { retour b == 0 ? a : gcd(b, a % b); }
long long lcm(long long a, long b) { retour a / gcd(a, b) * b; }
};
«» "

---

- Oui. 6. Les bons, les mauvais et les méchants

**Qu'est-ce qu'il s'agit de**
C'est-à-dire...
**Bon**• Longueur de la cible ≤ 4 → 16 états DP<br>• La pré-computation du sous-ensemble LCM est O(2^m) → trivial<br>• Code est court, facile à comprendre<br>• Fonctionne pour les trois langages (Java 8+, Python 3, C++17) Les intervieweurs aiment une solution DP propre qui * correspond aux contraintes*. Autres
• Si "m" était plus grand, "O" (n2^m·2^m)" serait exploser <br>• Certaines personnes utilisent une cupidité naïve qui transforme seulement un élément en une cible *simple* multiple → sous-optimale Soyez prêt à expliquer pourquoi le PDD est nécessaire si l'intervieweur repousse. Autres
**Le LCM peut déborder si les cibles sont grandes (pas dans ce problème)<br>• En oubliant l'affaire "Skip" de cet élément, on obtient de mauvaises réponses.Utilisez `long` partout et testez avec de grandes entrées pour éviter le débordement. Autres

---

- Oui. 7. Résumé de la préparation au référencement

- **LeetCode 3444** – *Incréments minimaux pour les multiples cibles dans un tableau*
- **Java/Python/C++** – *bitmask DP solution*
- ** Programmation dynamique** + **LCM** + **bitmask**
- *Temps-optimal* pour "cible.longueur ≤ 4"
- Excellent exemple d'entrevue pour **ingénieur logiciel** postes

> *Si vous préparez un entretien technique ou polissez votre LeetCode
> portfolio, cette solution est incontournable. Lâche-toi si ça t'aide à
> entretien!*

---

- Oui. 8. Pensées finales

* ** Pourquoi vous allez l'adorer** –
Le DP est mathématiquement sain, fonctionne en millisecondes, et démontre une
Bien joué : * transformer un élément de tableau en un multiple de tout sous-ensemble de cible
nombres à la fois*.

* **Quoi faire attention** –
Toujours pré-calculer les LCM une fois; les recalculer dans la boucle intérieure
tuer la performance.
Utiliser des entiers 64 bits pour la sécurité, même si les contraintes conservent des valeurs
petit.

* ** angle d'entrevue** –
Mettez en évidence que vous avez identifié le petit tableau `cible` et tourné le
problème dans un DP de 16 états. Expliquez la logique LCM, montrez un cas d'essai
('nums = [1,2,3], cible = [2,3]' → répondre `1`).
Cela montre que vous pouvez *transférer une contrainte réelle dans un DP propre*
exactement ce que les gestionnaires d'embauche recherchent.

Bonne chance pour LeetCode et pour la prochaine interview ! C'est ce qu'il a dit