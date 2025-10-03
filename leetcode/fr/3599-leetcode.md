---
titre: LeetCode 3599. Tableau de partition pour minimiser les XOR -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1. Récapitulation du problème – LeetCode 3599 : *Partition disposée pour réduire au minimum les XOR*

> **Objectif** – Compte tenu d'un tableau entier «nums» (1 ≤ nums.longueur ≤ 250) et d'un entier «k» (1 ≤ k ≤ n), fractionner «nums» dans **k des sous-parcours contigus et non vides**.
> Pour chaque sous-réseau, calculez le **bitwise XOR** de tous ses éléments.
> Retourner la valeur **minimum possible de la XOR maximale** parmi les sous-tarifs `k`.

> **Exemple**
> `nums = [1,2,3]`, `k = 2` → réponse `1` (`[1]) [2,3]` → XORs 1 et 1).

---

2. Pourquoi la programmation dynamique + préfixe XOR?

* Les sous-cours doivent être contigus → classiques DP sur préfixes.
* XOR d'un sous-réseau `[l ... r]` se trouve dans **O(1)** en utilisant un tableau *préfix XOR*
«pref[i] = nombres[0] ^ ... ^ nombres[i‐1]».
Puis `xor(l,r) = pref[r+1] ^ pref[l]`.
* L'objectif est de minimiser le maximum de → une transition DP minimax.

Donc l'idée est :

«» "
dp[i][p] = minimum possible max‐ XOR lorsque les premiers numéros i sont divisés en parties p
«» "

Transition:

«» "
dp[i][p] = min sur tous les points s (p‐1 ≤ s < i)
de max( dp[s][p‐1] , xor(s, i-1) )
«» "

Le cas de base: `dp[i][1] = xor(0, i‐1)` – le XOR des premiers numéros `i`.

Avec «n ≤ 250» et «k ≤ n», le «O(n2·k)» DP est parfait.

---

3. Code – 3 langues

> Toutes les solutions partagent la même logique ; seule la syntaxe diffère.

---

### 3.1. Java 17

"Java
Importation de java.util.*;

solution de classe {
Int public minXor(int[] nums, int k) {
int n = longueur nums;

// ---------préfixe XOR ---------
int[] pref = nouvelle int[n + 1];
pour (int i = 1; i <= n; ++i) pref[i] = pref[i - 1] ^ nombres[i - 1];

// -------- PDD ---------
int INF = entier.MAX_VALUE;
int[] dp = nouvelle int[n + 1] k + 1;
pour (int i = 0; i <= n; ++i) Arrays.fill(dp[i], INF);

// boîtier de base: une partie
pour (int i = 0; i <= n; ++i) dp[i][1] = pref[i];

// transition
pour (int parties = 2; parties <= k; ++parties) {
pour (int end = parties; fin <= n; ++ end) { // besoin au moins d'éléments 'parties'
pour (int split = parties - 1; split < fin; + split) {
int segXor = pref[end] ^ pref[split];
le candidat int = Math.max(dp[split][parties - 1], segXor);
dp[end][parts] = Math.min(dp[end][parts], candidat);
}
}
}

retour dp[n][k];
}
}
«» "

---

3.2. Python 3

'`python
de taper l'importation Liste

Solution de classe:
def minXor(self, nombres: List[int], k: int) -> Int:
n = len(nums)

# préfixe XOR
pref = [0] * (n + 1)
pour i dans la plage(1, n + 1):
pref[i] = pref[i - 1] ^ nombres[i - 1]

INF = 10 ** 9
dp = [[INF] * (k + 1) pour _ dans la plage (n + 1)]

# case de base
pour i dans la plage (n + 1):
dp[i][1] = pref[i]

PDD transition
pour les pièces de la gamme(2, k + 1):
pour la fin dans la plage (parties, n + 1):
meilleure = INF
pour l'intervalle (parties - 1, fin):
seg_xor = pref[end] ^ pref[split]
candidat = max(dp[split][parties - 1], seg_xor)
si le candidat < le meilleur:
meilleur = candidat
dp[end][parties] = meilleur

retour dp[n][k]
«» "

---

#### 3.3. C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int minXor(vecteur<int>& nums, int k) {
int n = nombres.size();

// préfixe XOR
vecteur<int> pref(n + 1, 0);
pour (int i = 1; i <= n; ++i) pref[i] = pref[i - 1] ^ nombres[i - 1];

const int INF = INT_MAX;
vecteur<vector<int>> dp(n + 1, vecteur<int>(k + 1, INF)

// Cas de base
pour (int i = 0; i <= n; ++i) dp[i][1] = pref[i];

// PDD transition
pour (int parties = 2; parties <= k; ++parties) {
pour (int fin = parties; fin <= n; ++ fin) {
int best = INF;
pour (int split = parties - 1; split < fin; + split) {
int segXor = pref[end] ^ pref[split];
int cand = max(dp[split][parties - 1], segXor);
best = min(meilleur, cand);
}
dp[end][parties] = meilleur;
}
}

retour dp[n][k];
}
};
«» "

---

4. Analyse de la complexité

Opération Temps Espace
- C'est quoi ?
Préfixe XOR
PDD Transition (en milliers de dollars)

Avec `n ≤ 250`, le pire des cas est d'environ `250·250 - 1.6 × 107' opérations - assez rapide dans les trois langues.

---

5. Essais et cas de bord

'`python
def test():
sol = Solution()
d'affirmer sol.minXor([1, 2, 3], 2) == 1
affirme sol.minXor([2, 3, 3, 2], 3) == 2
d'affirmer sol.minXor([1, 1, 2, 3, 1], 2) == 0
# Tous les éléments le même
affirme sol.minXor([5] * 5, 3) == 5
# minimum k = 1
d'affirmer sol.minXor([4, 2, 7], 1)
# k = n → chaque élément son propre sous-réseau → réponse = max(nums)
d'affirmer sol.minXor([4, 2, 7], 3) == max(4, 2, 7)
print("Tous les tests sont passés!")

essai()
«» "

* ** tableau à éléments simples** (`n == k == 1`) – la réponse est simplement `nums[0]`.
* **k = n** – la réponse est l'élément maximum (chaque élément forme sa propre sous-tribu).
* ** Grandes valeurs** ('nums[i] == 109') – s'inscrit toujours dans un entier signé 32 bits; pas de débordement.

---

6. Pièges communs (Pièces Bad et Ugly)

Piège
- Oui.
**L'utilisation de `int` pour XOR > 231** – peut déborder dans certaines langues. i vous prévoyez > 231; les ints de Python sont débordés. Autres
**Ignorer la contrainte de contiguïté** – essayer une combinaison "k-subset" donnera une réponse incorrecte. Construire le DP sur les indices préfixes seulement. Autres
Autres **Les erreurs hors-par-un dans l'indexation de «pref»** – «pref[i]» représentent XOR des premiers éléments de «i». Conservez l'aide `xor(l, r) = pref[r+1] ^ pref[l]`. Autres
Utiliser `INF = INT_MAX` / `10**9` et `min(...)` pour mettre à jour. Autres
**Délai sur le très grand harnais d'essai** – les boucles imbriquées sont nécessaires mais peuvent être optimisées par des pauses précoces. Avec n=250 pas besoin; mais pour la pratique, pré-calculer tous les XOR de segment dans un tableau 2-D pour éviter de recompiler `pref[end] ^ pref[split]`. Autres

---

6. Autres approches (Nice, mais moins efficace)

L'approche de l'idée de complexité quand elle aide
- C'est quoi ?
Autres **Binary Search + DP**. Pour un `mid` donné, pouvons-nous diviser en parties ≤ k où chaque partie XOR ≤ `mid`? Bon quand vous voulez un facteur *logarithmique* ou quand `n` est énorme. Autres
La transition satisfait l'inégalité quadrangle → peut se réduire à "O(n·k)" après la pré-computation. Une amélioration théorique, mais pas nécessaire pour «n ≤ 250». Bon pour les interviews qui mettent l'accent sur le fait plus que naïf. Autres

---

6. Pourquoi cette solution se trouve-t-elle dans votre entretien

Mots-clés Pourquoi ça compte
C'est-à-dire
**LeetCode 3599** Autres
**Partition Array pour réduire au minimum les XOR** Autres
Autres **La solution DP de Java** / **La solution DP de Python** / **C++** Autres
**Codage de l'algorithme de l'entretien** Autres
**Algorithme de l'entrevue d'emploi**= Indique que vous pouvez répondre à de vraies questions d'entrevue. Autres

---

- Oui. Wrap-Up de style Blog

> **Titre** – LeetCode 3599 (Partition Array to Minimize XOR) – Une solution d'amitié DP en Java, Python & C++ – Boost Your Interview Score

> **Méta-description** – Apprendre l'approche de programmation dynamique étape par étape pour résoudre le LeetCode 3599. Obtenez le code Java, Python et C++, l'analyse de la complexité et des idées prêtes à l'entrevue. Parfait pour votre prochain entretien de codage. (en milliers de dollars)

> **Tags** – `LeetCode 3599`, `Partition Array to Minimize XOR`, `DP`, `prefix XOR`, `coding interview`, `job interview algorithme`, `Java solution`, `Python solution`, `C++ solution`.

- Oui. Le poste

```markdown
# Tableau de partition pour réduire au minimum la radioactivité (Code de débit 3599)

Lors d'un entretien de codage, on vous demande de diviser un tableau en « k » pièces de sorte que le *maximum XOR* des pièces soit minimisé. Les contraintes (n ≤ 250) donnent à penser qu'un *quadratic DP* fonctionnera dans le temps, mais le défi est de calculer efficacement les XOR sub-array. La clé est un tableau **préfix XOR**.

## 1-
> ... (comme ci-dessus) ...

- Oui. Naïve O(k · n!) Force brute
Le dénombrement de toutes les partitions `k` est combinatoire et impossible pour n=250. Nous avons besoin d'une approche structurée.

- Oui. DP + Préfixe XOR – La voie -
* Construire `pref` dans O(n).
* `dp[i][p]` = meilleur max-XOR pour les premiers nombres `i` divisés en parties `p`.
* Transition :
«dp[i][p] = min_{split} max(dp[split][p‐1], pref[i] ^ pref[split]»

*Proof d'exactitude*: ... (argument minimal).

Mise en œuvre (Java / Python / C++)
> Blocs de code ci-dessus.

C'est pas vrai. Complexité
> Temps O(n2·k), espace O(n·k).

## 6.
> ... (affirmations) ...

C'est pas vrai. Et si n était plus grand?
> * Recherche binaire + DP gourmand.
> * Optimisation de type knuth.

À emporter
* Comprendre la structure *minimum* de la réduction maximale.
N'oubliez pas que XOR est associatif et réversible – le truc du préfixe est un sauveteur.
* L'écriture d'un code clair et commenté en 3 langues montre une adaptabilité – un must-have pour les panels d'entrevue.

---

Autres Prêt à faire ton prochain entretien ? Laissez un commentaire, partagez vos propres solutions et laissez ace LeetCode 3599 ensemble ! C'est ce qu'il a dit.
«» "

---

8. Pensée finale

> **Bonne** – formulation PDD claire, O(n2·k) est optimale pour les contraintes, code propre.
> **Bad** – Certains candidats oublient l'exigence « contigüe » et essaient une approche de sous-ensemble combinatoire – ce qui leur donnera de mauvaises réponses.
> **Ugly** – Codage dur de la récurrence XOR sans tableau de préfixe conduit à un O(n3) DP et est une recette pour TLE.

Choisissez la solution DP ci-dessus, testez-la sur les cas échantillons, et vous aurez une réponse **prête à coller** pour LeetCode 3599.

** Astuce pour les interviews d'emploi** – Apportez l'idée de "minimax DP" , parlez de l'astuce XOR préfixe, et mentionnez comment vous avez adapté le code à **O(n·k)** espace si demandé pour l'optimisation supplémentaire. Cela démontre la profondeur de la pensée au-delà juste un code de travail. (en milliers de dollars)

Bon codage ! C'est ce qu'il a dit