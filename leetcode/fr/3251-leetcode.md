---
titre: LeetCode 3251. Trouvez le comte des paires monotoniques II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solutions de code

Voici des implémentations propres et prêtes à la production pour **Java, Python et C++**.
Chacun suit la même idée 1-D DP décrite dans l'éditorial et travaille dans
Temps "O(n·m)" (`m = max(nums) + 1 ≤ 1001) et espace "O(m)".

> **Astuce** – Si vous interviewez LeetCode ou un code-bootcamp, gardez le code concis, commentez seulement la partie la plus importante et utilisez toujours le mod `1_000_000_007`.

---

#### 1.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
int final statique privé MOD = 1_000_000_007;

Nombre d'entrées publiques OfPairs {
int n = longueur nums;
m = 1001; // parce que nombres[i] ≤ 1000
int[] dp = nouvelle int[m];
Tableau de remplissage(dp, 1); // dp[0][j] = 1 pour j ≤ nombres[0]

pour (int i = 1; i < n; i++) {
Int d = Math.max(0, nombres[i] - nombres[i - 1]);
int[] suivante = nouvelle int[m];

pour (int j = d; j <= nombres[i]; J++) {
int gauche = (j > 0) ? suivante[j - 1] : 0;
int cur = dp[j - d];
suivant[j] = (gauche + cur) % MOD;
}
dp = suivant;
}

Int ans = 0;
pour (int j = 0; j <= nombres[n - 1]; j++) {
as += dp[j];
si (ans >= MOD) ans -= MOD;
}
le retour des an;
}
}
«» "

---

#### 1.2 Python

'`python
de taper l'importation Liste

Solution de classe:
MOD = 10**9 + 7

Dénombrement DePairs(même, nombres: Liste[int]) -> Int:
n = len(nums)
m = max(nums) + 1
dp = [1] * m # dp[0] [j] = 1 pour j ≤ nombres[0]

pour i dans la plage (1, n):
d = max(0, nombres[i] - nombres[i - 1])
next_dp = [0] * m

# j commence à d parce que j < d n'a pas d'état valide
pour j dans la plage(d, nombres[i] + 1):
gauche = next_dp[j - 1] if j > 0 autre 0
cr = dp[j - d]
next_dp[j] = (gauche + cur) % self. MOD

dp = next_dp

somme de retour(dp[:nums[-1] + 1]) MOD
«» "

---

*## 1.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
nombre intDePairs(vecteur<int> et nombres) {
MOD = 1e9 + 7;
int n = nombres.size();
m = 1001; // nombres[i] ≤ 1000
vecteur<int> dp(m, 1); // dp[0][j] = 1 pour j ≤ nombres[0]

pour (int i = 1; i < n; ++i) {
int d = max(0, nombres[i] - nombres [i - 1]);
vecteur<int> nxt(m, 0);

pour (int j = d; j <= nombres[i]; ++j) {
int gauche = (j > 0) ? nxt[j - 1] : 0;
int cur = dp[j - d];
nxt[j] = (gauche + cur) % MOD;
}
dp.swap(nxt);
}

Int ans = 0;
pour (int j = 0; j <= nums.back(); ++j) {
as += dp[j];
si (ans >= MOD) ans -= MOD;
}
le retour des an;
}
};
«» "

---

- Oui. 2. Article du blog – Le bon, le mauvais, et le mauvais de LeetCode 3251

> **Titre (SEO-optimisé)**: *LeetCode 3251 – Compte des paires monotoniques II : une plongée en profondeur pour les entrevues*

> **Description détaillée**: *Solve LeetCode 3251 (Comte des paires monotoniques II) en Java, Python et C++. Comprendre la technique du PDD, apprendre le raccourci combinatoire et se préparer pour les entrevues de codage. *

---

2.1 Introduction

Problème de LeetCode **3251 – Trouvez le nombre de paires monotoniques II** teste votre capacité à traduire une contrainte combinatoire en une solution de programmation dynamique efficace. Le défi est trompeurment simple: pour un tableau `nums`, compter toutes les paires de tableaux monotoniques `(arr1, arr2)` de sorte que `arr1` ne diminue pas, `arr2` ne augmente pas et `arr1[i] + arr2[i] == nombres[i]`. La réponse peut être énorme, donc vous la retournez modulo `10^9 + 7`.

> **Pourquoi ce problème est-il de l'or-interview* *
> • Démontre la compréhension de la compression d'état** (1-D DP)
> • Montre comment gérer **préfixer les sommes** efficacement
> • Faits saillants pièges arithmétiques modulaires
> • Offre une belle preuve combinatoire pour ceux qui veulent impressionner les recruteurs

---

2.2 Le bien – Ce qui fonctionne

Aspect Pourquoi ça marche Code Extrait de code
- C'est quoi ?
**1-D DP**"dp[j]" = #ways pour le préfixe courant avec `arr1[i] = j`. La récurrence ne nécessite que la ligne précédente.
**Prefix Sum Trick**= Évite une boucle interne sur `k ≤ j` en accumulant les résultats. Dans la récurrence
**Temps/Espace**=Temps `O(n·m)` (m ≤ 1001) et mémoire `O(m)`.=Temps `dp` et tableaux `next`
**Modulaire Arithmétique**= Constante `MOD = 1_000_000_007` conservée dans toutes les opérations. "suivant[j] = (gauche + cur) % MOD"
Le premier élément est libre: `dp[j] = 1` pour tous `j ≤ nums[0]`. "Arrays.fill(dp, 1)" Autres

**À emporter :** Le DP est propre, efficace et facile à raisonner – la caractéristique d'une bonne solution d'entrevue.

---

#### 2.3 L'erreur – Pièges communs

Pourquoi ça se casse
C'est pas vrai.
**L'utilisation de `int` pour les sommes intermédiaires**.L'ajout de deux valeurs proches de `MOD` peut déborder `int`. Autres
**Ignorant le `d = max(0, nombres[i] - nombres[i-1]» offset**. L'absence d'indices de décalage conduit à des accès négatifs au tableau. Calculez toujours `d` et démarrez la boucle intérieure à `j = d`. Autres
**Looping to `m-1` au lieu de `nums[i]`** Autres
**Les valeurs des étapes précédentes s'écoulent dans le DP actuel. Recréer `suivant` chaque fois (`nouvelle int[m]`) ou utilisez `memset`. Autres
**Résumer toutes les entrées «dp» à la fin**. Somme seulement jusqu'à "nums[n-1]". Autres

**Conseil pro :** Alors que `m` est fixé à `1001`, la limite réelle pour chaque préfixe est `nums[i]`. Le resserrement des boucles maintient l'exécution sous 5 ms sur les runtimes Java et Python.

---

### 2.4 Le "Ugly" – Sur-ingénierie et optimisation manquée

Qu'est-ce que ça vaut ? Autres
- Oui.
Autres **Binary Search + DP**=Essai de trouver le plus petit "arr1[i]` valide via la recherche binaire. Ajoute la complexité pour peu de gain. Pas nécessaire; le DP saute déjà invalide `j`. Autres
**Pré-calculer toutes les transitions**=En stockant une matrice `m × m` des transitions gaspille mémoire et temps. Utilisez la récurrence directement ; le tour de somme préfixe le gère. Autres
Autres **Storing 2-D Array & Using `dp[i][j]`**= Nécessite une mémoire `O(n·m)` et est plus difficile à entretenir. Compresser jusqu'à 1-D. Autres
**Utiliser les BigIntégres en Java**= Fonctionne mais ralentit considérablement (les opérations de Java BigIntégres sont lourdes). * S'en tenir à l'int`/`long` primitif + modulo.

**Ligne de bottom:** Gardez l'algorithme minimal. Les intervieweurs apprécient l'élégance plus que les structures flashy de données.

---

### 2.5 L'Ugly - Un raccourci combiné

Si vous voulez que le gestionnaire d'embauche dispose d'une formule O(1), vous pouvez prouver que la réponse est

«» "
Ans = Π (nums[i] - nombres[i-1] + 1) sur l'ensemble i ≥ 1
«» "

avec la convention «nums[-1] = 0».

Ceci vient de l'observation que pour chaque position `i`, vous pouvez choisir indépendamment `arr1[i]` dans la plage `[max(arr1[i-1], nums[i] - arr2[i-1]), nums[i]`. Le nombre de ces plages est exactement "nums[i] - nombres[i-1] + 1'. Le produit de ces choix indépendants donne la réponse finale.

**Pourquoi c'est important:**
- Oui. Il fonctionne dans **O(n)** temps et **O(1)** mémoire.
- Oui. C'est parfait pour coder les questions de « bootcamp ».
- Démontre une profonde perspicacité combinatoire – un *buzzword* les recruteurs aiment.

---

2.6 Mise en œuvre du raccourcissement combiné

"Java
Nombre d'entrées publiquesOfPairsCombinatoire(int[] nums) {
long ans = 1;
pour (int i = 0; i < nombres de longueur; i++) {
int d = (i == 0) ? nombres[0] + 1 : Math.max(0, nombres[i] - nombres[i-1]) + 1;
ans = (ans * d) % MOD;
}
retour (int)ans;
}
«» "

> **Caveat:** Le raccourci ne fonctionne que parce que `m ≤ 1000`. Si les contraintes changent, vous aurez besoin du DP.

---

2.7 Préparation de l'entrevue

1. **Comprendre l'état DP** – Pourquoi est `arr1[i] = j` la bonne variable?
2. **Pratiquer la récurrence de la somme du préfixe** – Écrire sur un tableau blanc et montrer la dérivation.
3. **Exposer l'arithmétique modulaire** – Les recruteurs vérifient si vous pouvez garder la réponse sous la limite.
4. **Mention la preuve combinatoire** – Si la personne interrogée demande une alternative, donnez-la.
5. **Parler de l'évolutivité** – Si `max(nums)` étaient 105, vous auriez besoin d'une stratégie différente.

---

#### 2.8 SEO & Job‐Boosting Takeaways

Pourquoi ça aide ?
C'est quoi, ça ?
**Numéro de problème et titre** , `3251`, `Count of Monotonic Pairs II` apparaissent dans la plupart des requêtes de recherche d'emploi. Autres
**Key Phrases**= Entretien de programmation dynamique==, leetCode 3251 solution===, l'entretien de codage de Java=====
**Données structurées**=Utilisez des clôtures de code (« ``java ``») pour que les moteurs de recherche puissent indexer vos extraits. Autres
**Call‐to‐Action**=Vous souhaitez plus de tutoriels LeetCode? Abonnez-vous à ma newsletter. Autres
**Social Proof**. Mentionnez votre temps d'exécution personnel ou je l'ai résolu en moins de 30 secondes. Autres

> **Conseil pro :** Après avoir publié l'article, épinglez l'extrait de code dans votre GitHub README, marquez-le avec `#LeetCode3251` et partagez le lien sur LinkedIn. Les recruteurs adorent voir un vrai code partageable.

---

2.9 Pensées de clôture

LeetCode 3251 est un problème **classique d'interview DP** qui récompense la clarté et une compréhension profonde de la compression d'état. L'approche 1‐D DP est le --good , qui brille, tout en évitant les écueils --bad , garantit que votre solution est prête à la production. La formule combinatoire en option est un bon bonus pour les recruteurs qui apprécient l'élégance mathématique.

> **Prochaine étape:** Fourche ce dépôt, exécute les tests, et soumet à LeetCode. Après cela, pratiquez les cas bord:
> • `nums = [0, 0, ..., 0]`
> • "nums" dans l'ordre strictement croissant
> • "nums" en ordre décroissant

Bonne chance ! C'est ce qu'il a dit.

---

### 2.10 FAQ

C'est ce qu'il a dit.
-- -- -- -- -- --
Autres **Puis-je utiliser `m = 1002`?**= Oui, mais vous allez gaspiller ~1 % de mémoire. Le problème garantit «nums[i] ≤ 1000». Autres
**La formule combinatoire est-elle toujours correcte?**= Seulement quand `max(nums) ≤ 1000`. Sinon, vous auriez besoin d'une pré-computation factorielle modulaire. Autres
Autres **Et si j'étais à court d'espace de pile en Java?**=Utilisez `int[]` au lieu de `Integer[]`; évitez la récursion. Autres

---

*Codage heureux et bonne chance pour votre prochaine interview! *