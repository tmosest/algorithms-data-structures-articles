---
Titre: LeetCode 1681. Incompatibilité minimale - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1681 – Incompatibilité minimale
**Langues** : C++
**Tags** : Leetcode, Dynamic Programming, Bitmask DP, Job Interview, Algorithm Interview, Software Engineer

---

- Oui. 1. Récapitulation des problèmes

> **Codage à gauche 1681 – Incompatibilité minimale**
> On vous donne un tableau entier `nums` de longueur `n` et un entier `k`.
> `n` est garanti être un multiple de `k`.
> Partition `nums` en groupes `k` de taille égale `n / k`.
> L'incompatibilité ** d'un groupe est la différence entre son élément maximal et son élément minimal.
> L ' objectif est de réduire au minimum les incompatibilités entre les groupes k.
> Retourner `-1` si une telle partition est impossible.

> **Constraints**
> - "2 ≤ n ≤ 16"
> - `1 ≤ k ≤ n`
> - `1 ≤ nombres[i] ≤ 16'
> - `n` est divisible par `k "

Parce que `n` est minuscule (16) nous pouvons énumérer en toute sécurité les sous-ensembles du tableau en utilisant des masques bit.
La solution classique est une programmation dynamique **bit-masque** qui précompute tous les groupes *valides* et construit ensuite la réponse en les combinant.

---

- Oui. 2. Idée de haut niveau

1. **Précalculer chaque sous-ensemble valide de taille `bucket = n / k`.**
*Un sous-ensemble est valide s'il ne contient pas de numéros dupliqués. *
Pour chaque sous-ensemble valide, nous stockons également son *incompatibilité* (`max - min`).

2. **Programmation dynamique sur masques bit* *
`dp[mask]` = incompatibilité totale minimale avec la partition des éléments dont les indices sont définis dans `mask`.
Il suffit de considérer des masques dont le nombre de bits est un multiple de "bucket".
Pour un masque `b`, nous itérer sur tous les sous-masques *valides* `s` de taille `bucket` et mettre à jour

«» "
dp[b] = min(dp[b], dp[b ^ s] + incompatibilité[s])
«» "

3. **Résultat**
La réponse est "dp[(1 << n) - 1]".
Si c'est toujours `INF`, la partition est impossible → retourner `-1`.

L'algorithme fonctionne dans le temps `O(n choose seau) * 2^n), ce qui est bien en dessous de la limite pour `n ≤ 16`.
L'utilisation de la mémoire est `O(2^n)`.

---

- Oui. 3. Exécution

Ci-dessous sont des solutions propres et entièrement commentées dans **Java**, **Python** et **C++**.
Tous utilisent le même noyau algorithmique mais sont adaptés aux idiomes de chaque langue.

---

#### 3.1 Solution Java

"Java
// Java 17
Importation de java.util.*;

solution de classe {
Incompatibilité(int[] nombres, int k) {
int n = longueur nums;
seau intérieur Taille = n / k; // taille de chaque groupe

/* Précalculer tous les sous-ensembles valides de seau de taille.
* stocker l'incompatibilité dans un tableau où
* -1 indique que le masque n'est PAS un groupe valide
*/
dans maxMask = 1 << n;
Int[] bonne MaskVal = nouvelle int[maxMask];
Arrays.fill(bienMaskVal, -1);

pour (int masque = 0; masque < maxMasque; masque++) {
si (Integer.bitCount(masque) != seauTaille) continue;

int vu = 0; // bitset de valeurs (1..16) déjà utilisé
int mn = 17, mx = 0; // parce que nombres[i] <= 16
booléen ok = vrai;

pour (int i = 0; i < n; i++) {
si ((masque & (1 << i))) == 0) poursuivre;
Int val = nombres[i];
si ((see & (1 << val)) != 0) { // duplicata dans le groupe
ok = faux;
pause;
}
vu= (1 << val);
mn = Math.min(mn, val);
mx = Math.max (mx, val);
}

si (ok) bonMaskVal[masque] = mx - mn;
}

/* DP sur masques */
int INF = entier.MAX_VALUE / 2; // éviter le débordement
int[] dp = nouveau int[maxMask];
les tableaux.fill(dp, INF);
dp[0] = 0;

pour (int masque = 0; masque < maxMasque; masque++) {
si (dp[masque] == INF) continuer;
// itérer sur des sous-masques de taille seau Taille
pour (int sub = masque; sub > 0; sub = (sub - 1) & masque) {
si (bienMaskVal[sub]] -1) poursuivre; // non valide
int newMask = masque ^ sub;
dp[mask] = Math.min(dp[mask], dp[newMask] + goodMaskVal[sub]);
}
}

réponse int = dp[maxMask - 1];
réponse au retour == INF ? -1 : réponse;
}
}
«» "

---

3.2 Solution Python

'`python
# Python 3.10+
de taper l'importation Liste

Solution de classe:
def minimumIncompatibilité(self, nombres: List[int], k: int) -> Int:
n = len(nums)
seau = n // k

_masque max = 1 << n
# groupe invalide & #160;: -1, autre valeur d'incompatibilité
good_val = [-1] * max_masque

# Précalculer tous les groupes valides de taille `bucket`
pour masque dans la plage(max_mask):
si bin(mask).count("1") != Seau:
poursuivre

vu = 0
mn, mx = 17, -1 # nombres[i] <= 16
ok = Vrai
pour i dans la plage(n):
Si non (masque >> i) & 1:
poursuivre
val = nombres[i]
si (voir >> valeur) & 1:
ok = Faux
pause
vu= 1 << valeur
mn = min(mn, val)
mx = max(mx, val)

si oui:
good_val[masque] = mx - mn

INF = 10 ** 9
dp = [INF] * max_masque
dp[0] = 0

pour masque dans la plage(max_mask):
si dp[mask] == INF:
poursuivre
# itérer sur tous les sous-masques de `masque`
sous = masque
tandis que sous:
si bon_val[sub] != -1 et dp[masque ^ sub] != INF:
dp[mask] = min(dp[mask], dp[mask ^ sub] + good_val[sub])
sous = (sous - 1) & masque

retour -1 si dp[max_mask - 1] == INF sinon dp[max_mask - 1]
«» "

---

#### 3.3 C++ Solution

'`cpp
// C++17
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Incompatibilité minimale(vecteur<int>& nums, int k) {
int n = nombres.size();
seau int = n / k;
dans maxMask = 1 << n;
INF = 1e9;

/* Pré-calculer les groupes valides de taille `bucket`.
* `incomp[masque]` = incompatibilité si le masque est valide, sinon -1
*/
vecteur<int> incomp(maxMask, -1);
pour le masque (int = 0; masque < maxMasque; ++Masque) {
si (_builtin_popcount(mask) != seau) continue;

Int vu = 0;
Int mn = 17, mx = -1;
bool ok = true;
pour (int i = 0; i < n; ++i) {
si (!(masque >> i) & 1) continuer;
Int val = nombres[i];
si (voir & (1 << val)) { // duplicata dans le groupe
ok = faux;
pause;
}
vu= 1 << valeur;
mn = min(mn, valeur);
mx = max(mx, val);
}
si (ok) incomp[masque] = mx - mn;
}

/* DP sur masques */
vecteur<int> dp(maxMask, INF);
dp[0] = 0;
pour le masque (int = 0; masque < maxMasque; ++Masque) {
si (dp[masque] == INF) continuer;
// itérer sur des sous-masques de taille `bucket "
pour (int sub = masque; sub > 0; sub = (sub - 1) & masque) {
si (incomp[sub]]] -1) poursuivre; // non valide
int newMask = masque ^ sub;
dp[mask] = min(dp[mask], dp[newMask] + incomp[sub]);
}
}

Int ans = dp[maxMask - 1];
INF ? -1 : ans;
}
};
«» "

---

- Oui. 4. Mises en œuvre

Ce que vous devez **faire**
Il n'y a pas de lien entre les deux.
**Bon*** *Pré-calculer* tous les groupes valides → temps `O(2^n)` au lieu d'explorer chaque partition de façon récursive.
**Bon**Utiliser *sous-masque de dénombrement* (`sub = (sub-1) & masque`) → linéaire dans le nombre de sous-masques.
**Bonne**) Conservez l'incompatibilité dans un tableau, et non une `carte`, pour éviter les frais généraux.
Un retour naïf qui vérifie toutes les permutations "k!".
Oubliez que les duplications à l'intérieur d'un groupe rendent le groupe invalide.
Utiliser un DP exponentiel (`dp[mask] = min(dp[mask], dp[mask^sub] + ...)"), mais oublier de limiter aux masques dont le nombre de bits est un multiple de `bucket`.
Retenez `INF` comme `INT_MAX`; en ajoutant deux valeurs de ce type, vous débordez.

---

- Oui. 5. Pourquoi cela compte pour une entrevue d'emploi

* **Complexité temporelle**:
Votre recruteur voudra voir que vous pouvez raisonner sur le pire des cas et choisir un algorithme qui correspond aux contraintes.
Une solution qui énumére naïvement toutes les partitions `k` est \(O(k! \cdot n^k)\) – évidemment **impossible** pour `n = 16`.

* **Efficacité spatiale**:
L'utilisation d'un masque 32 bits (`1 << n`) vous permet de stocker l'état de manière compacte et d'effectuer des opérations bitwise en temps constant.

* ** Astuces linguistiques** :
- Dans **Java** utiliser `Integer.bitCount` et `Arrays.fill`.
- Dans **Python**, utilisez `bin(mask.count('1')` ou `_builtin_popcount` (via `int.bit_count` en 3.8+).
- Dans **C++** utiliser `_builtin_popcount` et les macros de manipulation de bits.

* ** Expliquer clairement la logique** :
Dans une entrevue, passez par la pré-computation, la transition du PDD et la réponse finale.
Mentionnez pourquoi la duplication importe et pourquoi l'incompatibilité est simplement "max - min".

* ** Démontrer la confiance** :
Parlez de la protection `INF` contre le débordement, et de la taille précoce (`si dp[masque] == INF continue`).
Ces petits détails font souvent la différence entre une réponse propre et un TLE.

---

- Oui. 6. Dernier départ

- **Pré-calcul** groupes valides → supprime une énorme quantité de travail.
- **Bit-mask DP** + **sub-mask énumération** → garantit la performance "O(2^n)".
- **Éviter la récursion naïve ou le tri répété des boucles intérieures.

Avec les modèles ci-dessus, vous serez prêt à frapper l'interview.En Java, Python ou C++, vous pourrez transformer un cauchemar de force en une solution soignée et optimale. Bon codage !