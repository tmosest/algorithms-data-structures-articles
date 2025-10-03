---
titre: LeetCode 3574. Maximiser le score de la sous-marque GCD -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
3574. Maximiser le score GCD de Subarray
**Douce**= 1500 ≤ n ≤ 1500= 1 ≤ nombre[i] ≤ 109= 1 ≤ k ≤ n

> Vous pouvez doubler n'importe quel élément au plus une fois, mais vous pouvez effectuer au plus **k** de telles opérations.
> Un score de sous-cours = (longueur du sous-cours) × (GCD du sous-cours).
> Retourner le score maximum possible après au plus **k** double.

---

- Oui. 1. Intuition

* Doubler un élément ne le multiplie que par 2.
* Le GCD d'une sous-tribu ne peut être augmenté que par des facteurs de 2 – tout le reste est déjà partagé par tous les éléments.
* On calcule chaque nombre comme

\[
nombres[i] = 2^{e_i}\; \cdot\; a_i, \qquad a_i\ \text{odd}
\]

`e_i` est l'exposant du bit le plus bas (`_buildingin_ctz` en C++, `Integer.numberOfTrailingZeros` en Java, `x & -x` trick en Python).
La partie étrange `a_i` ne peut pas être modifiée en doublant ; seul l'exposant `e_i` peut croître de 1 si nous double l'élément.

* Pour un sous-appel fixe `[l ... r]` le GCD des parties impaires est un seul nombre impair `g`.
Le GCD de toute la sous-tribu est alors

\[
GCD = g \; \cdot\; 2^{\min\{e_l,\dots,e_r\}}
\]

Le doublement d'un élément qui a déjà l'exposant *minimum* augmentera le GCD d'un autre facteur 2.
Le fait de doubler n'importe quel autre élément ne change pas le GCD car l'exposant minimum reste le même.

* Par conséquent, pour une sous-entente, nous ne nous soucions que de

1. **`g`** – gcd des parties impaires.
2. **`minE`** – plus petit exposant parmi les éléments.
3. **`cntMin`** – combien d'éléments de la sous-tribu ont exposé `minE`.

Si `cntMin ≤ k`, nous pouvons doubler tous ces éléments `cntMin` → GCD est doublé.

---

- Oui. 2. Algorithme

«» "
meilleur = 0
pour l = 0 ... n-1:
g = 0
minE = INF
cntMin = 0
pour r = l ... n-1:
g = gcd(g, a[r]) // a[r] = nombres[r] >> e[r]
e = exposant[r] // zéros de fuite des nombres[r]

si e < minE:
minE = e
cntMin = 1
Sinon si e == - Oui.
cntmin += 1

len = r - l + 1
base = len * g * (1LL << minE)
best = max (meilleur, base)

si cntMin <= k:
best = max(meilleur, base * 2) // nous pouvons doubler tous les éléments min-exposants
le meilleur retour
«» "

* **Complexité temporelle** – Deux boucles imbriquées → **O(n2)** (2 · 106 itérations pour n = 1500).
* **Complexité spatiale** – O(1) supplémentaire (seulement quelques entiers / longs).
* Tous les arithmétiques correspondent à 64 bits signés (`long` in Java / C++ / Python="s int).

---

- Oui. 3. Preuve d'exactitude

Nous prouvons que l'algorithme renvoie le score maximum réalisable GCD.

Lemma 1
Pour toute sous-tribu `S`, que `g` soit le GCD de ses parties impaires, `minE` l'exposant minimum, et `cntMin` le nombre d'éléments atteignant `minE`.
Le GCD de `S` sans aucun doublement est `g · 2^{minE}`.

*Proof. *
Chaque élément peut être écrit sous la forme `2^{e_i} · a_i` avec un étrange `a_i`.
Le GCD des parties impaires est `g`.
Le GCD des pouvoirs de deux est le plus petit exposant, "minE".
Ainsi le GCD est leur produit. *



Lemma 2
Si nous doubleons tous les éléments `cntMin` qui ont exposant `minE`, le GCD de `S` devient
`g · 2^{minE+1}`; le doublement de tout autre élément ne peut pas augmenter le GCD.

*Proof. *
Le fait de doubler un élément avec l'exposant `e_i` l'élève à `2^{e_i+1}·a_i`.
Si `e_i > minE`, l'exposant minimum parmi les éléments reste `minE`, de sorte que le GCD reste `g·2^{minE}`.
Si `e_i = minE`, le nouveau minimum devient `minE+1`, donc le GCD augmente exactement d'un facteur 2.



Lemma 3
Pour toute sous-requête `S`, le maximum de DCG qui peut être obtenu après au plus des doubles `k` est

«» "
score(S) = len(S) * g * 2^{minE} si cntMin > k
score(S) = len(S) * g * 2^{minE+1} si cntMin ≤ k
«» "

*Proof. *
Si `cntMin > k`, nous ne pouvons pas doubler tous les éléments d'exposition minimal, donc le mieux que nous pouvons faire est de garder le GCD comme dans Lemma 1.
Si `cntMin ≤ k`, nous pouvons doubler tous ces éléments (en utilisant au plus `cntMin ≤ k` opérations), atteindre le plus grand GCD par Lemma 2.
Aucune autre combinaison de doublements ne peut augmenter le GCD davantage parce que tous les autres éléments ont un exposant ≥ `minE`.



C'est vrai. Théorème
L'algorithme produit le score maximal de GCD possible après au plus des «k» doubles.

*Proof. *
Au cours de la double boucle, chaque sous-réseau possible `[l...r]` est examiné exactement une fois.
Pour ce sous-réseau, l'algorithme calcule `base = len · g · 2^{minE}` (Lemma 1).
Si `cntMin ≤ k`, il évalue également `base·2` (Lemma 2).
Par Lemma 3, ce sont précisément les meilleurs scores possibles pour cette sous-tribu.
La variable `meilleur' conserve le maximum de tous ces scores, de sorte qu'après tous les sous-cours sont traités `meilleur' égale l'optimum global. *



---

- Oui. 4. Exécution

Voici des solutions complètes et compilables dans **Java**, **Python** et **C++**.

---

##### 4.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
// GCD pour int – fonctionne pour toutes les valeurs <= 1e9
interne statique privé gcd(int a, int b) {
pendant que (b != 0) {
t = a % b;
a = b;
b = t;
}
retour a;
}

public long maxGCDScore(int[] nums, int k) {
int n = longueur nums;
// Exponents précalculés et pièces impaires
int[] exp = nouvelle int[n];
int[] impair = nouveau int[n];
pour (int i = 0; i < n; i++) {
int e = entier.numberOfTrailingZeros(nums[i]); // exposant de bit le plus bas
exp[i] = e;
impair[i] = nombres[i] >> e; // décalage droit par bits
}

longue meilleure = 0;

pour (int l = 0; l < n; l++) {
g = 0;
int minE = entier.MAX_VALUE;
Int cntMin = 0;

pour (int r = l; r < n; r++) {
g = gcd(g, impair[r]);

e = exp[r];
si (e < minE) {
minE = e;
cntMin = 1;
} sinon si (e == minE) {
cntMin++;
}

longue len = r - l + 1;
base longue = len * g * (1L << minE);
best = Math.max (best, base);

si (cntMin <= k) {
best = Math.max (best, base * 2); // double tous les éléments minimaux
}
}
}

le meilleur retour;
}
}
«» "

*Compiler & exécuter:*
"""
Javac Solution.java
java Solution // appeler maxGCDScore(...) à partir d'un harnais d'essai
«» "

---

4.2 Python 3

'`python
importations
d'importation de mathématiques gcd
de taper l'importation Liste

Solution de classe:
def maxGCDScore(self, nombres: List[int], k: int) -> Int:
n = len(nums)

# Exponent précalculé du bit le plus bas et de la partie étrange
Exp = [0] * n
impair = [0] * n
pour i, val dans l'énumération(nombres):
e = (val & -val).bit_longueur() - 1 # zéros de piste via x & -x
exp[i] = e
impair[i] = valeur >> e

meilleur = 0

pour l dans la plage(n):
g = 0
minE = n + 1 # sentinelle
cntMin = 0

pour r dans la plage(l, n):
g = gcd(g, impair[r])

e = exp[r]
si e < minE:
minE = e
cntMin = 1
- Oui. - Oui.
cntmin += 1

longueur = r - l + 1
base = longueur * g * (1 < < minE)
best = max (meilleur, base)

si cntMin <= k:
best = max (meilleur, base * 2)

le meilleur retour
«» "

---

*### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

Int main() {
ios::sync_with_stdio(faux);
cin.tie (nullptr);

l'élément n, k;
si (!(cin >> n >> k)) retourne 0;
vecteur <long> nums(n);
pour (int i = 0; i < n; ++i) cin >> nombres[i];

// Exponents précalculés et pièces impaires
vecteur <int> exp(n);
vecteur<int> impair(n);
pour (int i = 0; i < n; ++i) {
int e = __constructin_ctzll(nums[i]); // exposant du bit le plus bas
exp[i] = e;
d'une part, et
}

longue longue meilleure = 0;

pour (int l = 0; l < n; ++l) {
g = 0;
int minE = INT_MAX;
Int cntMin = 0;

pour (int r = l; r < n; ++r) {
g = md:gcd(g, impair[r]);

e = exp[r];
si (e < minE) {
minE = e;
cntMin = 1;
} sinon si (e == minE) {
++cntmin;
}

longue len longue = r - l + 1;
longue base longue = len * g * (1LL << minE);
best = max (meilleur, base);

si (cntMin <= k) {
best = max (meilleur, base * 2); // double tous les éléments d'exposition min
}
}
}

cout << best << '\n';
retour 0;
}
«» "

Les trois programmes ont **O(n2)** runtime et **O(1)** mémoire auxiliaire, satisfaisant les limites.

---

- Oui. 5. Discussion sur le blog

5.1 Récapitulation des problèmes

> *Vous pouvez doubler au maximum **k** éléments (une fois par élément) et vous voulez le plus haut `(longueur × GCD)` de n'importe quel sous-array. *

La principale est que seules les puissances de deux peuvent être affectées par un doublement; tous les autres facteurs communs sont déjà présents dans le GCD.

5.2 Pourquoi deux boucles sont assez bonnes

Avec `n ≤ 1500` le nombre total de sous-cours est

\[
\frac{n(n+1)}{2} \le 1\,125\,750
\]

Même avec le calcul interne GCD (temps constant) c'est bien en dessous d'une seconde dans les processeurs modernes.
Une recherche de force brute qui recalcule le GCD à partir de zéro pour chaque sous-arrachage serait *O(n3)* et serait TLE – notre GCD incrémental intelligent le garde *O(n2)*.

5.3 Pièges communs

Piège
- Oui.
Utiliser des entiers 32 bits pour le produit final (`len * g * 2^minE`) peut déborder.
Autres Oubliant de déplacer correctement la partie *odd* (Java/C++) ou `odd[i] = nombres[i] // (1 << e[i])» (Python)
En utilisant `_builtin_ctz` sur zéro. Autres
Réinitialiser `cntMin=1` quand `e < minE`.

5.4 Résumé de la complexité

Étape Temps Espace
C'est pas vrai.
Objets de prétraitement et pièces détachées
Autres Deux boucles imbriquées
Ensemble

Dans le pire des cas `n = 1500`, ce n'est qu'environ 2 × 106 itérations internes – assez vite.

Pourquoi la solution est-elle élégante ?

* Nous ne touchons jamais le tableau original; nous travaillons sur sa représentation factorisée.
* Tout le problème se réduit à garder la trace de l'exposant **minimum** dans une fenêtre coulissante.
* Le doublage est traité comme une multiplication *conditionnelle* par 2 – pas besoin d'un DP compliqué.

#### 5.6 Référencement et étiquettes

- **LeetCode 3574**
- ** Maximiser le score du GCD**
- **Opérations de doublement**
- **Array GCD**
- **O(n2) solution**
- **Astuce GCD à deux points* *
- **C++ O(n2) GCD**
- **Java 64 bits entier**

---

**Codage heureux!**