---
titre: LeetCode 3250. Trouvez le comte des paires monotoniques I -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
*(Java + Python + C++)*

---

Récapitulation du problème

On vous donne un tableau entier positif `nums` de longueur `n` (`1 ≤ n ≤ 2000`, `1 ≤ nombres[i] ≤ 50`).
Une paire **monotonique** est une paire de tableaux

«» "
(arr1 , arr2) // longueur des deux n
«» "

* `arr1` est **non-diminution** : `arr1[0] ≤ arr1[1] ≤ ... ≤ arr1[n-1] "
* `arr2` est **non-augmentation** : `arr2[0] ≥ arr2[1] ≥ ... ≥ arr2[n-1] "
* Pour chaque indice `i`, `arr1[i] + arr2[i] = nombres[i] "

Retourner le nombre de ces paires, modulo `10^9 + 7`.

---

Intuition et observation clé

Si nous regardons la position `i‐th`, les deux valeurs `a = arr1[i]` et `b = arr2[i]` doit satisfaire

«» "
a + b = nombres[i] (1)
«» "

et ils doivent respecter les contraintes de monotonicité par rapport à la position précédente:

«» "
≤ a (2)
arr2[i-1] ≥ b (3)
«» "

De (1) et (3) nous obtenons

«» "
arr1[i-1] + nombres[i] - arr1[i-1] ≤ a
C'est ce que j'ai dit.
arr1[i-1] + (nums[i] - nombres[i-1]) ≤ a
«» "

Définir

«» "
d = max(0, nombres[i] - nombres[i-1])
«» "

Ensuite, tout `a` valide doit satisfaire `a ≥ arr1[i-1] + d`.
La partie importante est que **la limite inférieure de `a` n'est qu'un décalage constant (`d`) de la précédente `a`** – il ne dépend pas** de la valeur exacte de `arr1[i-1]`.

Cela conduit à un PDD simple:

*Let* `dp[j]` *be le nombre de façons de remplir les premiers postes `i` de telle sorte que* `arr1[i-1] = j`.

Lorsque nous passons de la position `i-1` à `i`:

«» "
newDP[j] = sum_{k ≤ j-d} dp[k]
«» "

Parce que `k` est le `arr1[i-1]` précédent, et `j` est le `arr1[i]` actuel.
La somme peut être calculée en O(1) par `j` si nous conservons une somme de préfixe en cours d'exécution.

Ainsi nous pouvons implémenter le DP en **O(n * max(nums))** temps et **O(max(nums))** espace.

---

Aperçu de l'algorithme

«» "
1. m = 1001 // valeur maximale possible de arr1[i] (nums[i] ≤ 50, mais nous allouons un peu plus pour la sécurité)
2. dp[0...m-1] ← 1 // pour i = 0, n'importe quel a dans [0, nombres[0]] est possible
3. Pour i = 1 ... n-1
d = max(0, nombres[i] - nombres[i-1])
nouveauDP[0...m-1] ← 0
pref ← 0
Pour j = d ... nombres[i] // j est le courant a
pref ← (pref + dp[j-d]) mod MOD
nouveauDP[j] ← pref
dp ← nouveauDP
4. réponse = sum_{j=0}^{nums[n-1]} dp[j] // nombre de façons de terminer à la dernière position
5. retour de réponse mod MOD
«» "

La boucle intérieure ne visite que la gamme `0 ... nums[i]` (parce que des valeurs plus élevées ne peuvent pas apparaître – `a` ne peut pas dépasser `nums[i]`).
Tout arithmétique est fait modulo `10^9 + 7`.

---

Code – 1 D DP (Java / Python / C++)

Code de la langue
C'est quoi, ça ?
[Code de Java](/path/to/java.png)
[Code Python](/path/to/python.png)
[Code C++](/path/to/cpp.png)

> **NOTE** – Dans les extraits suivants, la taille du tableau `m` est `1001`.
> Puisque `nums[i] ≤ 50`, vous pouvez attribuer `m = 51` ou `m = 52` – l'algorithme fonctionne pour n'importe quel `m ≥ max(nums)`.

---

Mise en œuvre Java

"Java
// - Oui. Solution Java 1D DP pour LeetCode 3250 ----------
Importation de java.util.*;

solution de classe publique {
int final statique privé MOD = 1_000_000_007;
// Valeur maximale que tout arr1[i] peut prendre: nombres[i] ≤ 50, mais attribuer un peu plus.
finale statique privée MAXV = 1001;

Nombre d'entrées publiques OfPairs {
int n = longueur nums;
int[] dp = nouvelle int[MAXV];
int[] newDP = new int[MAXV];

// Cas de base: i = 0
pour (int j = 0; j <= nombres[0]; j++) dp[j] = 1;

// DP sur les postes restants
pour (int i = 1; i < n; i++) {
Int d = Math.max(0, nombres[i] - nombres[i - 1]);

Tableau.fill(nouveauDP, 0);
Int pref = 0;
// Il suffit de calculer jusqu'à nums[i] – rien de plus élevé est impossible.
pour (int j = 0; j <= nombres[i]; J++) {
// pref tient sum_{k <= j-d} dp[k]
si (j - d >= 0) {
pref = (pref + dp[j - d]) % MOD;
}
newDP[j] = pref;
}
// Échanger des références pour la prochaine itération
int[] tmp = dp;
dp = nouveauDP;
nouveauDP = tmp;
}

// Résumez toutes les façons qui se terminent par arr1[n-1] dans [0, nombres[n-1]]
Int ans = 0;
pour (int j = 0; j <= nombres[n - 1]; j++) {
as += dp[j];
si (ans >= MOD) ans -= MOD;
}
le retour des an;
}
}
«» "

> **Pourquoi `Arrays.fill(newDP, 0)`?**
> Java réutilise le tableau de référence chaque itération, nous devons donc le réinitialiser avant de le remplir.

---

Mise en œuvre de Python (style monoligne)

'`python
♪ - Oui. Solution Python 1D DP pour LeetCode 3250 ----------
MOD = 10 ** 9 + 7
MAXV = 1001

def countOfPairs(nums: list[int]) -> Int:
n = len(nums)
dp = [1] * MAXV
pour i dans la plage (1, n):
d = max(0, nombres[i] - nombres[i - 1])
nouvelle_dp = [0] * MAXV
pref = 0
pour j dans la plage(0, nombres[i] + 1):
si j - d >= 0:
pref = (pref + dp[j - d]) % MOD
new_dp[j] = pref
dp = new_dp

# somme de tous les dp[j] pour j en [0, nombres[-1]]
somme de retour(dp[:nums[-1] + 1]) % MOD
«» "

*Notes pyroniques*
* `MAXV` est suraffecté pour la sécurité; vous pouvez utiliser `51` directement (`MAXV = 51`).
* La boucle intérieure ne fonctionne que jusqu'à `nums[i]` – toutes les valeurs au-delà de cela sont impossibles.

---

Mise en œuvre C++ (rapide, sans STL)

'`cpp
// - Oui. C++ Solution DP 1D pour LeetCode 3250
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
nombre intDePairs(vecteur<int> et nombres) {
MOD = 1'000'000'007;
const int MAXV = 1001; //
vecteur<int> dp(MAXV, 1); // i == 0

pour (size_t i = 1; i < nums.size(); ++i) {
int d = max(0, nombres[i] - nombres [i - 1]);
vector<int> new_dp(MAXV, 0);
Int pref = 0;
pour (int j = 0; j <= nombres[i]; ++j) {
si (j - d >= 0) {
pref += dp[j - d];
si (pref >= MOD) pref -= MOD;
}
new_dp[j] = pref;
}
dp.swap(new_dp); // réutiliser la mémoire
}

long an = 0;
pour (int j = 0; j <= nums.back(); ++j) {
as += dp[j];
si (ans >= MOD) ans -= MOD;
}
retour de l'intra(ans);
}
};
«» "

> **Pourquoi `swap(new_dp)` au lieu de réaffecter? * *
> L'échange est O(1) et garde l'empreinte de la mémoire minimale.

---

- Oui. Solution alternative pour les combinaisons

Le PDD ci-dessus compte essentiellement le nombre de séquences ** non décroissantes** `arr1` qui respectent un déplacement lié inférieur `d`.
Il s'avère que le nombre final est égal à un simple coefficient binomial:

«» "
v = nombres[n-1] - ↓ max(0, nombres[i] - nombres[i-1]) //
réponse = C(n + v - 1, v) (mod. 1e9+7) // étoiles et barres
«» "

Pourquoi ça marche ? *
Après avoir appliqué les augmentations minimales (`d`s) à chaque étape, nous sommes laissés avec un problème de placer `n` indistinguible =stars (la partie variable de `arr1`) dans les seaux `v+1` (la valeur maximale finale).
Le résultat des étoiles et des barres standard donne la formule ci-dessus.

**Pros** – temps O(n + v), espace O(1).
**Cons** – Nécessite des combinaisons modulaires (`C` modulo a prime), qui peuvent être lourdes pour les grandes `v`.
Pour les contraintes de LeetCode ('nums[i] ≤ 50'), le DP 1-D est plus simple et assez rapide.

---

## 4--Cas de bord et pièges communs

Pourquoi il échoue
- C'est quoi ?
Autres Oubliant le `max(0, ...)` lors du calcul `d`-" négatif `d` casse la liaison `a ≥ arr1[i-1] + d`-" toujours pince `d` à zéro
Utiliser `nums[i]` au lieu de `m` pour la longueur du tableau.
Autres Oublier le modulo après chaque ajout.
La boucle de sommation de `0` à `j-d` au lieu du préfixe=O(n * m2) time=Utilisez la somme du préfixe en cours d'exécution (`pref`) pour la faire O(n * m)=
Ne pas réinitialiser "newDP" chaque itération

---

Analyse de complexité

Langue Heure Espace
- C'est quoi ?
Java 1-D DP.
Python 1-D DP.
C++ 1-D DP.
Ensemble (étoiles et barres)

Les contraintes sont minuscules ('nums[i] ≤ 50'), de sorte que le DP 1-D est ** bien dans les délais** pour toutes les langues.

---

Réflexions finales pour les intervieweurs

* **Afficher votre processus de pensée** – expliquer comment vous avez dérivé `d = max(0, nums[i] – nums[i-1]'.
* **Parler de la monotonicité** – pourquoi un tableau non décroissant force une limite inférieure sur chaque élément.
* **Pourquoi préfixer les sommes?** – pour éviter le temps quadratique.
* **Arithmétique modulaire** – mettre en évidence l'importance de « MOD » après chaque opération.
* **Mention le raccourci étoiles-et-bars** – il démontre que vous pensez à des points de vue alternatifs.

---



# Guide de style Blog – Pourquoi 1-D DP fonctionne

Dans cette section, nous traversons l'intuition derrière le PDD 1-D, comme si vous l'expliquiez à un candidat.
(Sentez-vous libre de copier/coller le balisage dans votre blog ou votre message LinkedIn!)

---



---

# *Blog: *Solving LeetCode 3250 – Un DP 1-D avec un Twist**
(Vous pouvez coller le balisage entier dans un éditeur de blog – il contient du code, des tables et des explications.)

---



* Fin**

> Bon codage, et bonne chance pour votre prochain entretien de codage!

---

*Cet article a été écrit pour aider les développeurs à implémenter la solution à LeetCode 3250 – Numéro de compte d'expositions originales possibles.
N'hésitez pas à fourcher, à vous améliorer et à partager. *