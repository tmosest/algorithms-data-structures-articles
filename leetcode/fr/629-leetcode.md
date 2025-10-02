---
titre: LeetCode 629. K Paires inversées -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code de solution

Ci-dessous vous trouverez des implémentations propres, prêtes à copier dans **Java**, **Python** et **C++** qui résolvent LeetCode 629 – *K Inverse Pairs Array*.

> **Récapitulation des problèmes* *
> Étant donné `n` et `k`, compter les permutations de `[1...n]` qui contiennent exactement des paires inverses `k`.
> Retourner la réponse modulo `109+7`.

#### 1.1 Java – PDD roulant (O(n k) temps, O(k) espace)

"Java
// 629. K Paires inversées
// Java – PDD roulant, temps O(n*k), espace O(k)

solution de classe publique {
int final statique privé MOD = 1_000_000_007;

public int kInversePairs(int n, int k) {
int[] dp = nouvelle int[k + 1]; // dp[j] – #ways pour courant i avec j paires
dp[0] = 1; // base: 0 éléments → 1 sens (tableau vide)

pour (int i = 1; i <= n; i++) {
int[] suivante = nouvelle int[k + 1];
suivant[0] = 1; // seulement 1 permutation avec 0 paires pour n'importe quel i
pour (int j = 1; j <= k; j++) {
// dp[j] – dp[j-i] (si j-i >= 0)
int sub = (j - i) >= 0 ? dp[j - i] : 0;
int val = (dp[j] - sous + MOD) % MOD; // valeur temporaire pour ce j
next[j] = (next[j - 1] + val) % MOD; // préfixe sum trick
}
dp = suivant; // passer à la suivante i
}

// dp[k] détient la somme de dp[0..k], soustraire dp[k-1] pour obtenir exactement k
résultat int = (dp[k] - (k > 0 ? dp[k - 1] : 0) + MOD) % MOD;
le résultat du retour;
}
}
«» "

#### 1.2 Python – PD tournant (O(n k) temps, O(k) espace)

'`python
# 629. K Paires inversées
# Python 3 – PD roulant, temps O(n*k), espace O(k)

MOD = 1 000 000 007

def k_inverse_pairs(n: int, k: int) -> Int:
dp = [0] * (k + 1)
dp[0] = 1 # cas de base

pour i dans la plage(1, n + 1):
nxt = [0] * (k + 1)
nxt[0] = 1
pour j dans la plage (1, k + 1):
sous = dp[j - i] si j - i >= 0 autre 0
val = (dp[j] - sous) % MOD
nxt[j] = (nxt[j - 1] + valeur) % MOD
dp = nxt

# exactement des paires de k
retour (dp[k] - (dp[k - 1] si k > 0 autre 0)) % MOD
«» "

### 1.3 C++ – PDD roulant (O(n k) temps, O(k) espace)

'`cpp
// 629. K Paires inversées
// C++17 – PDD roulant, temps O(n*k), espace O(k)

#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int kPairs inversés(int n, int k) {
MOD = 1'000'000'007;
vecteur<int> dp(k + 1, 0), nxt(k + 1, 0);
dp[0] = 1; // scénario de base

pour (int i = 1; i <= n; ++i) {
nxt[0] = 1;
pour (int j = 1; j <= k; ++j) {
Int sub = (j - i >= 0) ? dp[j - i] : 0;
int val = (dp[j] - sous + MOD) % MOD; // valeur temporaire
nxt[j] = (nxt[j - 1] + val) % MOD; // préfixe sum trick
}
dp.swap(nxt); // passer à la suivante i
}

résultat int = (dp[k] - (k > 0 ? dp[k - 1] : 0) + MOD) % MOD;
le résultat du retour;
}
};
«» "

Les trois implémentations fonctionnent dans l'espace auxiliaire "O(n k)" et "O(k)", qui correspond facilement aux contraintes (`n, k ≤ 1000").

---

- Oui. 2. Article de blog – Le bon, le mauvais et le mauvais de K‐Inverse‐Pairs

> **Mots clés:**
> `K Inverse Pairs Array`, `LeetCode 629`, `programme dynamique`, `optimisation du PD`, `codage interview`, `Java`, `Python`, `C++`, `entretien d'emploi`, `entretien d'algorithme`, `LeetCode dur "

2.1 Introduction

Si vous vous préparez à un entretien technique ou à un bootcamp de data-structures-and-algorithmes (DSA), vous rencontrerez assez souvent **LeetCode 629 – K Inverse Pairs Array**. C'est un problème *Hard* qui vous force à penser au-delà de la récursion naïve et de la force brute. Dans ce post, nous allons disséquer le problème, marcher à travers une solution **dynamique-programmation**, explorer les pièges communs (le *mauvais*), et révéler un **optimisé linéaire-espace** (le *bon*). Enfin, nous allons parler de la façon dont maîtriser ce problème peut vous séparer dans un pipeline de location.

> **Lire le tutoriel complet sur le site officiel de LeetCode :** https://leetcode.com/problèmes/k-inverse-pairs-array/

---

2.2 Récapitulation du problème

> **Avec** un entier `n` et un entier `k`, retournez le nombre de permutations de `[1 ... n]` qui contiennent **exactement des paires inverses `k`**.
> Une paire **inverse** est une paire `(i, j)` où `i < j` et `nums[i] > nums[j]`.
> La réponse doit être retournée modulo `1 000 000 007`.

> **Exemples**
> 1. `n = 3, k = 0` → `1` (seulement `[1,2,3]`)
> 2. `n = 3, k = 1` → `2` (`[1,32]`, `[2,1,3]`)

---

2.3 L'approche de la Force brute

Une première pensée est de générer toutes les permutations `n!`, compter les paires inverses, et filtrer. Pour `n = 10` c'est déjà astronomique (permutations '3.6M`). Même avec la mémorisation, le comptage des paires inverses pour chaque permutation serait `O(n2)` par permutation – clairement impossible pour les contraintes (`n, k ≤ 1000`).

> **Pourquoi il échoue :**
> - Temps exponentiel ("O(n!)").
> - Explosion de l'espace en raison du stockage des permutations.
> - Faible évolutivité : l'algorithme se décroît bien avant les essais officiels.

Il nous faut donc un algorithme polynôme. C'est là où **la programmation dynamique** intervient.

---

#### 2.4 Le DP – La récurrence classique 2-D

Laissez `dp[i][j]` = nombre de permutations des premiers `i` nombres (`1...i`) qui ont exactement `j` paires inverses.

**Transition* *

Lorsque nous insérons le nombre `i` dans une permutation de `1...i-1`, le nouvel élément peut atterrir dans n'importe quelle position `p` (1-basé). Il créera de nouvelles paires inverses `p-1` parce qu'il sera plus grand que tous les éléments à sa gauche. Ainsi:

«» "
dp[i][j] = γ_{p=1}^{i} dp[i-1][j-(p-1)]
«» "

Simplifier en modifiant l'indice: `q = p-1`, `q ↓ [0, i-1]`:

«» "
dp[i][j] = ш_{q=0}^{min(i-1, j)} dp[i-1][j-q]
«» "

**Affaires de base**

«» "
dp[0]] = 1 // permutation vide
dp[0][j>0] = 0
«» "

**Complexité* *

- Temps: `O(n * k * n)` → `O(n2 k)` (parce que la somme intérieure peut atteindre `i`).
- Espace: `O(n * k)` pour une table 2-D complète.

Alors que cela résout le problème, il est encore trop lent pour `n = k = 1000`. Nous avons besoin d'une récurrence plus intelligente.

---

#### 2.5 Le bon – Optimisation de la somme des préfixes (O(n k))

Notez que la transition est une **convolution** de la ligne précédente avec une fenêtre coulissante de largeur `i`. Nous pouvons éviter la somme intérieure en utilisant un **préfixe sum** astuce:

Laissez écrire la récurrence comme:

«» "
dp[i][j] = dp[i][j-1] + dp[i-1][j] - dp[i-1][j-i]
«» "

Explication :

- `dp[i][j-1]` contient déjà toutes les permutations où le dernier élément inséré créé ≤ `j-1` nouvelles paires.
- Ajouter `dp[i-1][j]` ajoute un cas où le dernier élément crée exactement des paires `0` nouvelles.
- Soustraire `dp[i-1][j-i]` supprime le surcompte où le nouvel élément créerait plus de paires `i-1` (c'est-à-dire `p > i`).

Toutes les opérations sont prises en modulo `M`.

**Tarifs itinérants**

Puisque `dp[i][*]` ne dépend que de `dp[i-1][*]`, nous pouvons conserver deux tableaux 1-D:

Texte
[j] – dp[i-1][j]
[j] – dp[i][j]
«» "

Et après chaque boucle extérieure nous les échangeons. Cela réduit l'espace à `O(k)`.

**Étape finale**

Après avoir construit jusqu'à `i = n`, `dp[n][k]` détient en fait le nombre **cumulatif** de permutations avec des paires inverses ≤ `k` en raison de l'astuce préfixe-sum. Pour obtenir exactement `k`, soustrayez la valeur précédente :

«» "
réponse = dp[n][k] - dp[n][k-1] (mod M)
«» "

---

2.6 Les pièges communs

Pourquoi ça arrive ?
- Oui.
**Modulo négatif**="dp[i-1][j] - dp[i-1][j-i]` peut être négatif=" Ajouter `MOD` avant d'appliquer `%` Autres
**Index Out‐of‐Bounds** 0)»
**Débordement entier en C++** peut dépasser `int`.
Autres **Limite de temps en raison des boucles 3-D naïfs**
**Caisse de base manquante** Définissez le tableau entier à `0` puis `dp[0] = 1`
Après chaque `i`, `prev` et `curr` sont mélangés avec `prev.swap(curr)` (C++), `dp = nxt` (Java/Python)

---

2.7 A emporter: Pourquoi le règlement de 629 compte

1. **Shows DP Mastery** – De nombreux problèmes de LeetCode sont liés au DP. Démontrer une récurrence correcte et une optimisation intelligente indique une compréhension profonde des transitions d'état.
2. **Mathematical Insight** – Reconnaître la propriété de la fenêtre coulissante et utiliser des sommes préfixes souligne l'intuition mathématique – un trait précieux pour les entrevues de conception système.
3. ** Ingénierie du rendement** – Les implémentations qui évitent `O(n2 k)` sont pratiques. Les recruteurs aiment les candidats qui savent **réduire le temps et l'espace**.
4. **Langue Agnostique** – Que vous codez en Java, Python ou C++, l'idée algorithmique est la même. Cela montre de la flexibilité – un autre atout dans un environnement technologique en évolution rapide.

---

### 2.8 Conclusion

LeetCode 629 est un problème classique qui vous apprend à:

1. Formuler une table DP («dp[i][j]».
2. Trouvez une convolution et transformez-la en une récurrence préfixe.
3. Déployez un tableau de roulement pour l'espace linéaire.
4. Gérez correctement l'arithmétique modulaire.

La maîtrise de ce problème vous permettra non seulement de gagner un score élevé sur LeetCode, mais aussi de vous équiper d'un ensemble de compétences transférables : *definition d'état, simplification de récurrence et optimisation de l'espace. *

> ** Conseil professionnel :** Après que vous soyez à l'aise avec ce tour de DP, essayez de résoudre la plus petite fraction primaire de KK* ou de produit maximum Subarray* – ils sont structurellement similaires et suivent les mêmes principes d'optimisation.

Bon codage, et que vos intervieweurs voient le *Bon* et le *Ugly* dans votre propre voyage algorithmique! C'est ce qu'il a dit.

---

> **Pour plus ample lecture:**
> - *Programmation dynamique* (MIT OCW) – https://ocw.mit.edu/course/6-006-introduction-to-algorithms-fall-2011/lecture-notes/
> - *L'art du PDD dans les entrevues* – https://www.interviewbit.com/dynamic-programming-interview-questions/
> - *LeetCode Discuter – 629* – https://leetcode.com/problèmes/k-inverse-pairs-array/discuss/
---

**Bonne entrevue!**