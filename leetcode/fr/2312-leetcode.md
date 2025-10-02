---
Titre: LeetCode 2312. Vente de pièces de bois -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2312 – Vente de pièces de bois
**LeetCode dur – Programmation dynamique* *

Langue Heure Espace Remarques
C'est pas vrai.
*Java** * O(m · n · (m + n) * O(m · n) * 64-bit `long' *
*Python *Utilisez `list` de `list`
"O(m · n · (m + n)" "O(m · n)" 64-bit "long" Autres

> Le même DP bottom-up fonctionne pour chaque langue – assurez-vous simplement d'utiliser un type 64-bit parce que la réponse peut atteindre `10^6 · 200 · 200 ↓ 4×10^10`.

---

Récapitulation des problèmes (version courte)

Vous avez une planche rectangulaire de taille `m × n`.
Un ensemble de **offres de prix** est donné, chaque offre `[h, w, prix]` signifie que vous pouvez vendre un morceau de taille `h × w` pour `prix` dollars.
Vous pouvez couper la planche n'importe quel nombre de fois **horizontalement ou verticalement sur toute la largeur/hauteur**.
Vous pouvez vendre n'importe quel nombre de pièces (y compris zéro) des formes que vous possédez.

> **Objectif:** maximiser le montant total gagné par le conseil d'administration `m × n`.

> **Aucune rotation autorisée** – un `1×4` ne peut pas devenir `4×1`.

---

Intuition

La seule chose qui compte, c'est comment le conseil est divisé.
Si nous connaissons la valeur optimale pour un rectangle **plus petit**, nous pouvons combiner deux sous-rectangles pour former un rectangle plus grand.

C'est le problème classique de la coupe de valeur maximale → ** Programmation dynamique (DP)**.

- Oui. Récurrence

Que `dp[h][w]` soit l'argent maximal d'un morceau de taille `h × w`.
Les valeurs de base proviennent des offres données; d'autres cellules commencent à `0`.

«» "
dp[h][w] = max( dp[h][w], // aucune coupure
dp[i][w] + dp[h-i][w] pour i = 1 .. h/2 ) // coupes horizontales
dp[h][j] + dp[h][w-j] pour j = 1 .. w/2 ) // coupes verticales
«» "

Pourquoi seulement `h/2` et `w/2`?
Parce qu'une coupe à `i` et à `h-i` produisent la même paire de sous-rectangles - nous considérons juste une direction.

- Oui. Pourquoi ?

Nous calculons toutes les valeurs «dp» dans l'ordre croissant de «h» et «w».
Lorsque nous traitons `dp[h][w]`, tous les petits rectangles sont déjà optimaux, de sorte que nous pouvons les combiner en toute sécurité.

---

Code

Ci-dessous vous trouverez exactement le même algorithme implémenté dans **Java**, **Python** et **C++**.
N'hésitez pas à copier-coller dans votre éditeur et à courir contre le harnais de test LeetCode.

---

### Java

"Java
Importation de java.util.*;

solution de classe publique {
vente longue durée publique Bois(int m, int n, int[][] prix) {
// dp[h][w] – argent maximum pour un h x w pièce
long[] dp = nouveau long[m + 1][n + 1];

// cas de base: prix fixés
pour (int[] p : prix) {
Int h = p[0], w = p[1];
dp[h][w] = p[2];
}

// bas vers le haut PDD
pour (int h = 1; h <= m; ++h) {
pour (int w = 1; w <= n; ++w) {
// coupes horizontales
pour (int i = 1; i <= h / 2; ++i) {
dp[h][w] = Math.max(dp[h][w],
dp[i][w] + dp[h - i][w];
}
// coupes verticales
pour (int j = 1; j <= w / 2; ++j) {
dp[h][w] = Math.max(dp[h][w],
dp[h] [j] + dp[h] [w - j]);
}
}
}
retour dp[m][n];
}
}
«» "

---

Python

'`python
Solution de classe:
vente Bois(self, m: int, n: int, prix: Liste[Liste[int]]) -> Int:
# dp[h][w] – argent maximum pour un h x w pièce
dp = [[0] * (n + 1) pour _ dans la plage (m + 1)]

pour h, w, p en prix:
dp[h][w] = p

pour h dans la plage (1, m + 1):
pour w dans la plage(1, n + 1):
# coupes horizontales
pour i dans la plage (1, h // 2 + 1):
dp[h][w] = max(dp[h][w], dp[i][w] + dp[h - i][w])
# coupes verticales
pour j dans la plage (1, w // 2 + 1):
dp[h][w] = max(dp[h][w], dp[h][j] + dp[h][w - j])

retour dp[m][n]
«» "

---

C++

'`cpp
solution de classe {
public:
longue vente Bois(int m, int n, vecteur<vector<int>>& prix) {
// dp[h][w] – argent maximum pour un h x w pièce
vecteur<vecteur<long long>> dp(m + 1, vecteur<long long>(n + 1, 0));

// Cas de base
pour (auto & p : prix) {
Int h = p[0], w = p[1];
dp[h][w] = p[2];
}

// bas vers le haut PDD
pour (int h = 1; h <= m; ++h) {
pour (int w = 1; w <= n; ++w) {
// coupes horizontales
pour (int i = 1; i <= h / 2; ++i)
dp[h][w] = max(dp[h][w], dp[i][w] + dp[h - i][w];

// coupes verticales
pour (int j = 1; j <= w / 2; ++j)
dp[h][w] = max(dp[h][w], dp[h][j] + dp[h][w - j]);
}
}
retour dp[m][n];
}
};
«» "

---

Complexité

Opération Complexité
C'est quoi ?
Remplissage de la caisse de base Autres
Boucles PDD principales
Mémoire

**Pourquoi est-ce "O(m · n · (m + n)"?**
Pour chacune des cellules `m · n` nous essayons jusqu`à `h/2 + w/2 ≤ (m + n)/2` coupes.

---

Cas de bord et pièges communs

Piège
- Oui.
En utilisant `int` pour `dp`. Utilisez `long`/`long`. Autres
Autres Oublier de définir des cas de base.Les cellules non initiales restent `0`, qui peuvent être sous-optimales si toutes les offres sont négatives. Autres
Découpe au-delà de la moitié. Seul l'itération «h/2» et «w/2». Autres
Indices hors-par-un LeetCode est basé sur 1 dans la récurrence; attribuer `m+1` et `n+1`. Autres
Utiliser la division entière ('h // 2` dans Python, `h / 2` dans Java/C++). Autres

---

Stratégies alternatives

Stratégie
C'est quoi ?
**Top-down + Memousing**
**Branch & Bound / DFS**
**Greedy** Ne fonctionne que pour des ensembles de prix spéciaux (par exemple, seulement 1×1). Autres
**Bitmask DP**= Fonctionne lorsque `m, n ≤ 10'== Exponentiel, ne convient pas pour 200=

Pour les entrevues, le DP **bottom-up** est la réponse la plus sûre car il garantit des sous-solutions optimales sans risque de débordement de cheminée.

---

Billet de blog : La vente de morceaux de bois – Le bon, le mauvais et le mauvais

> **Balises du référencement:**
> * vente de morceaux de leet code bois
> * leetcode 2312 solution
> * programmation dynamique de coupe de bois
> * programme dynamique d'entrevue
> * Python Java C++ Solution LeetCode

---

# Vente de morceaux de bois : une plongée profonde dans la programmation dynamique
(Le bon, le mauvais et le mauvais – SEO optimisé)

---

Coup d'oeil sur le problème

> **LeetCode 2312 – Vente de pièces de bois**
> Couper une planche `m × n` en petits morceaux pour maximiser les gains, en respectant un ensemble d'offres de prix et de réductions non rotationnelles.

> **Pourquoi ça compte**
> Ce problème se pose dans chaque entretien *algorithme* qui teste votre compréhension du DP 2-D, de la récursion et de l'optimisation.

---

- Oui. Bon – Pourquoi C'est un grand problème d'entrevue

Explication
C'est pas vrai.
**État de la DP claire** Le conseil est divisé en sous-rectangles indépendants. Autres
**Bottom-Up Simplicité**= Une boucle triple-nested; aucune pile de récursion à gérer. Autres
**Language-agnostique** ► La même logique fonctionne en Java, Python, C++ – parfait pour les interviews de codage en plusieurs langues. Autres
**Scales Well** Exclusive les contraintes maximales (`m, n ≤ 200`) confortablement en 2 s sur LeetCode. Autres
**L'analogie du monde réel**L'analogie du monde réel est un miroir des problèmes de stocks de coupe du monde réel (fibre, métal, etc.). Autres

> *Astuce:* Utilisez des entiers 64 bits (`long`/`long`) pour éviter le débordement.

---

- Oui. Mauvais – Les choses Ça peut mal tourner

Qu'est-ce qui peut briser votre solution ? Autres
- Oui.
**Dépassement**= Prix * 40 000 000 > 231–1 → utiliser 64-bit. Autres
Les indices DP commencent à `1`; oubliant le `+1` dans la taille du tableau tue l'algorithme. Autres
**Découpes à pleine portée**=Essai `i = 1 .. h-1` double travail; utiliser `h/2` et `w/2`. Autres
**Prix de base manquants**= Toute forme sans offre de prix est implicitement `0`. Si toutes les offres sont négatives, vous devez toujours considérer zéro coupure. Autres
La récursion pure peut atteindre la limite de récursion de Python (1000). Autres
**Délais** Les opérations de 16 M sont parfaites en Java/Python; en C++, c'est plus rapide, mais il reste à regarder pour 2002×400, 16 000 000 boucles. Autres

---

## 4.

Pourquoi c'est moche
- Oui.
Autres **Half-Cut Optimisation**= N'oubliez pas d' itérer jusqu'à `h/2` et `w/2`. Passer ce double fonctionne et peut vous ralentir. Autres
**Carte des prix vs. DP**. Certaines personnes stockent une carte des prix et la regardent pendant DP. C'est inutile ; il suffit d'écrire le prix directement dans "dp". Autres
Autres **Choosing Cut Direction**= Les coupes horizontales à `i` et `h-i` produisent la même paire; vous devez éviter de les compter deux fois. Autres
Autres **L'échange de l'espace**= Un PDD 2-D de `200 × 200' n'est que 40 000 cellules – amende. Mais si vous avez essayé un DP 3-D (hauteur, largeur, restes), il explose. Autres
**Test sur LeetCode** La réponse peut être jusqu'à `4×1010`, vous devez donc retourner `long`/`long`. Beaucoup de solutions retournent par erreur `int` et obtiennent une mauvaise réponse. Autres

---

Une solution complète (Java + Python + C++)

*(Les extraits de code sont déjà affichés ci-dessus – vous pouvez les copier directement.) *

---

Analyse de complexité

Mesure Java Python C++
C'est quoi, ça ?
(m+n) Autres
* Espace * * O(m·n) Autres
Autres **Meilleure affaire ops**

> **Pourquoi il est assez rapide** – Les opérations entières de 16 M fonctionnent < 0,2 s en Java/C++ et < 0,5 s en Python sur les serveurs LeetCode.

---

Autres approches

Quand l'utiliser
- C'est quoi ?
**Mémotisation du haut vers le bas (DFS)**= Petit nombre d'offres; vous voulez le code brivety=__________________________________________________________________________________________________________________________________________________________________________________________________________________________________ Autres
**Bitmask DP**= Taille de la carte ≤ 10= Fonctionne pour tous les modèles de coupe. Autres
**Greedy / DP sur 1×1 seulement**= Si toutes les offres sont 1×1=1 O(1)=1 Mauvais en général – manque des offres de plus grande valeur. Autres
**Divide & Conquer + Memo**= Pour la récursion de l'enseignement. Autres

> *Bottom-up DP est la réponse d'entrevue canonique – il montre que vous comprenez la commande sous-problème et peut gérer les grandes contraintes. *

---

- Oui. Comment tourner Ceci dans une entrevue de réussite

1. **Afficher l'intuition du DP** – parler de `dp[h][w]` et pourquoi les coupes horizontales/verticales n'ont besoin que de la moitié de la gamme.
2. **Exposer la complexité** – les intervieweurs vous aiment quand vous êtes explicite sur "O(m·n·(m+n)")".
3. **Parler de cas de bord** – par exemple, un 2×2 peut être moins cher que quatre 1×1s; toujours vérifier les offres de base.
4. **Sécurité 64 bits** – J'utilise "long`/`long` parce que la réponse peut dépasser 32 bits.
5. **Optionnel** – discutez de la mémorisation par rapport au bas vers le haut et pourquoi le bas vers le haut est habituellement le plus sûr dans les entrevues de production.
6. **Afficher le code en plusieurs langues** – démontre la polyvalence.
7. **Enveloppez** – Je peux résoudre ce problème en Java, Python ou C++ avec le même algorithme optimal. (en milliers de dollars)

> *Résultat:* Vous atterrissez une entrevue de codage où ils vous demandent d'expliquer ou d'étendre cette solution.

---

Les pensées finales

* **Bien:** PDD propre et déterministe; O(16 M) opérations passent facilement; aucun piège de récursion.
* **Bad:** Doit se rappeler l'optimisation à moitié coupée et les entiers 64 bits.
* **Défaut :** Erreurs hors-par-un, doubles comptages et subtiles différences linguistiques.

Si vous pouvez transmettre tout cela de façon concise dans une entrevue, vous montrez que vous n'êtes pas seulement un *codeur* mais un *algorithmiste* qui peut penser à travers des états, du temps/espace et des contraintes du monde réel.

Bon codage ! C'est ce qu'il a dit.

---

* Fin du blog *

---

Bonne entrevue ! Si vous souhaitez plonger plus profondément dans DP ou avoir des questions sur la mise en œuvre de la solution dans un autre langage, n'hésitez pas à laisser un commentaire.