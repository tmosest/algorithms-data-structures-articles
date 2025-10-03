---
titre: LeetCode 3196. Maximiser le coût total des substituts -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3196. Maximiser le coût total des substituts
**Moyenne de la population de LeetCode**

---

TL;DR

- **Objectif:** Diviser le tableau en subarrays contigus de sorte que la somme de
`nums[l] – nombres[l+1] + ... + nombres[r]` pour chaque sous-tribunement est maximisé.
- **Résultat :**
Texte
dp[i] = max( s[i] + meilleur Odd , -s[i] + bestEven )
«» "
où `s[i]` est la somme du préfixe alternatif et
`bestOdd = max_{j impair} (dp[j] – s[j])`,
`bestEven = max_{j even} (dp[j] + s[j])`.
- **Complexité:** temps "O(n)", mémoire "O(1)".
- **Langues:** Java, Python, C++ (tous utilisent des entiers 64 bits).

---

Déclaration du problème (simplifiée)

Vous êtes donné un tableau entier `nums` de longueur `n`.

«» "
coût(l, r) = nombres[l] - nombres[l+1] + nombres[l+2] - ... + nombres[r] * (-1)^(r-l)
«» "

Diviser le tableau en une ou plusieurs subdivisions contiguës de façon à maximiser le coût total.
Retournez le coût total maximal.

---

## -Le point de vue clé

Le coût d'une sous-tribu ne dépend que de la parité de son indice de départ.
En précomputant la somme du préfixe ** alternant** `s[i] = ↓_{k=0..i} nums[k] * (-1)^k`, le coût de toute sous-utilisation peut être exprimé comme suit:

«» "
Coût(l, r) = (-1)^l * ( s[r] – s[l-1] )
«» "

Cela nous permet de formuler un DP 1-dimensionnel qui n'a besoin que de garder deux maximums d'exécution (`bestOdd`, `bestEven`) au lieu de scanner tous les points de division possibles.

---

## Description de la solution

1. **Préfixer l'alternance**
Texte
s[i] = s[i-1] + nombres[i] * (-1)^i
«» "
2. ** La transition vers la démocratie**
Pour chaque indice "i" (position de fin de la dernière sous-tribu):
Texte
dp[i] = max( s[i] + meilleur Odd , -s[i] + bestEven )
«» "
* `bestOdd` – valeur maximale de `dp[j] – s[j]` pour `j` impair (y compris `j = -1`).
* `bestEven` – valeur maximale de `dp[j] + s[j]` pour même `j`.
3. **Mise à jour des maxima d'exécution**
Après avoir calculé `dp[i]`, mettre à jour la parité correspondante:
Texte
Si je suis égal : mieux vaut Même = max(meilleur Même, dp[i] + s[i])
sinon: bestOdd = max(meilleur Odd, dp[i] - s[i])
«» "
4. **Réponse**
`dp[n-1]` est le coût total maximal.

---

Mise en œuvre du code

### Java

"Java
Importation de java.util.*;

solution de classe publique {
public long maximum TotalCost(int[] nombres) {
int n = longueur nums;
long[] s = nouveau long[n];
long bestOdd = 0; // dp[-1] - s[-1] = 0
longue meilleure Même = Long.MIN_VALUE; // pas encore j

pour (int i = 0; i < n; i++) {
long val = nombres[i];
long signe = (i & 1) == 0 ? 1 : -1;
s[i] = (i == 0 ? 0 : s[i-1]) + val * signe;

option longue1 = s[i] + bestOdd; // dernière sous-utilisation commence à l'indice impair
option longue2 = -s[i] + bestEven; // dernière sous-utilisation commence à indice pair
long dp = Math.max(option1, option2);

// Mettre à jour les meilleures valeurs pour les indices futurs
Si (i et 1)] 0) {/ même
bestEven = Math.max(bestEven, dp + s[i]);
} autre { // impair
le meilleur Odd = Math.max(meilleur Difficile, dp - s[i]);
}
}
retour s[n-1] + bestOdd; // dp[n-1] = max( s[n-1] + bestOdd , -s[n-1] + bestEven )
}
}
«» "

Python

'`python
Solution de classe:
def maximum TotalCoût(même, nombres: Liste[int]) -> Int:
n = len(nums)
s = [0] * n
best_odd = 0 # dp[-1] - s[-1] = 0
best_even = -10**18 # efficacement

pour i, v in énumérate(nums):
signe = 1 si i % 2 == 0 autre -1
s[i] = (s[i-1] si i autre 0) + v * signe

opt1 = s[i] + best_odd
opt2 = -s[i] + best_even
dp = max(opt1, opt2)

si i % 2] 0: # même indice
best_even = max(best_even, dp + s[i])
Autre : # indice impair
best_odd = max(best_odd, dp - s[i])

retourner s[-1] + best_odd # dp[n-1]
«» "

C++

'`cpp
solution de classe {
public:
long long maximum TotalCoût(vecteur<int>& nombres) {
int n = nombres.size();
vecteur <long> s(n);
longue longue meilleure Odd = 0; // dp[-1] - s[-1]
longue longue meilleure Même = LLONG_MIN / 2;

pour (int i = 0; i < n; ++i) {
long panneau long = (i % 2 == 0) ? 1 : -1;
s[i] = (i ? s[i-1] : 0) + 1LL * nums[i] * signe;

long opt1 = s[i] + bestOdd; // commencer à un indice impair
long long opt2 = -s[i] + meilleur Même; // commencer à l'index
long dp = max(opt1, opt2);

si (i % 2 == 0) // même j
bestEven = max (best Même, dp + s[i]);
Autre // impair j
bestOdd = max(meilleur Difficile, dp - s[i]);
}
retour s[n-1] + bestOdd; // dp[n-1]
}
};
«» "

---

Pourquoi ça marche ?

- **Formule de coût**
"coût(l, r) = (-1)^l * (s[r] – s[l-1])".
Le signe `(-1)^l` ne dépend que de la *parité* de `l`.

- **Réécriture du PD**
Que `i` soit la fin de la dernière subarraie.
`dp[i] = max_{j<i} dp[j] + cost(j+1, i)`.
La substitution de l'expression des coûts donne deux expressions linéaires distinctes dans `s[i]` selon la parité de "j".
D'où le maximum sur tous les `j` réduit au maximum deux valeurs d'exécution (`bestOdd`, `bestEven`).

- **Running maxima**
Les mises à jour `bestEven = max(bestEven, dp[i] + s[i])` (même `i`) et
`bestOdd = max(best Odd , dp[i] - s[i]» (odd `i`) garder le meilleur possible
contributions pour les futures transitions sans boucles.

---

Cas et pièges (bons / mauvais / mauvais)

Situation Que regarder Recommandation
- C'est quoi ?
**Les grandes sommes**="nums[i]` jusqu`à ±1 000 000 000, `n` jusqu`à 100 000 → total peuvent atteindre ~1014="Utiliser `long` en Java, `long` en C++, `int` est très bien en Python (sans limite). Autres
**Le meilleur Il y a *non* même index `j` avant le premier élément. Commencer par `-..` (par exemple, `Long.MIN_VALUE/2`). Autres
En Java & C++, `-1` est bizarre, donc `bestOdd` commence à 0, couvrant le cas où la première sous-tribu commence à indexer Réglez explicitement « bestOdd = 0 » et sautez « bestEven » au début. Autres
La valeur intermédiaire `dp[i] + s[i]` peut déborder de 32 bits. Autres
**Python** Utilisez `-10**18` ou `float('-inf')` si vous préférez. Autres
**Caisse de corner**. Le code le gère naturellement parce que nous calculons toujours `dp[0]`. Autres

---

Résumé de l'entrevue

1. **Comprendre la parité** – le signe bascule avec chaque élément, de sorte que l'index *démarrage* décide si nous ajoutons ou soustrayez la somme du préfixe alternatif.
2. **Dériver un O(n) DP** – garder deux maximums d'exécution; la transition devient un simple `max` de deux fonctions linéaires.
3. **Surveillez le type de données** – Les entiers 64 bits sont obligatoires pour Java/C++.
4. **Mise en œuvre proprement** – l'algorithme est seulement ~30 lignes par langue et n'utilise pas de tableaux supplémentaires au-delà de la somme du préfixe.

---

## #= Le point de vue du SEO

Si vous préparez pour un **coding interview** ou cherchez une solution élégante **LeetCode 3196**, cet article couvre tout ce dont vous avez besoin:

- **Mots-clés**: LeetCode 3196, Maximiser le coût total des sous-programmations alternantes, Programmation dynamique, Préparation d'entrevues, Java, Python, C++
- **Avantages**:
*One-pass, algorithme linéaire-time* qui peut être collé sur n'importe quelle plateforme d'entrevue.
La même idée s'applique à tout problème où le coût d'un segment ne dépend que de sa parité de départ.

---

Problèmes de pratique suggérés

Problème Difficulté Lien
- C'est quoi ?
**Somme maximale de la sous-couche avec signe alternant**=Medium==[Code 1180](https://leetcode.com/problèmes/somme maximale de la sous-couche avec signe alternant/) Autres
**Somme maximale de deux sous-procédures de non-overlapping** Autres
**Somme maximale de 3 sous-procédés de non-overlapping**=Moyenne (https://leetcode.com/problèmes/somme maximale de 3 sous-procédés de non-overlapping/) Autres

---

La pensée finale

La partie de ce problème est la gymnastique des signes: vous devez garder une poignée serrée sur lequel les indices sont même ou étrange et retourner le signe en conséquence. Une fois que vous maîtrisez ce tour, le reste est un passe DP propre avec deux constantes – ** une victoire d'interview classique**.

Bon codage ! C'est ce qu'il a dit