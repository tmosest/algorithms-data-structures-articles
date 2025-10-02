---
titre: LeetCode 3610. Nombre minimum de primes à la cible -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Récapitulation du problème – Nombre minimum de Primes à Somme à Cible
**Code de cap #3610 – Moyen**

> On vous donne deux entiers `n` et `m`.
> Vous devez choisir un multiset des *premier `m` premiers nombres* (chaque premier peut être utilisé arbitrairement plusieurs fois) de sorte que leur somme égale exactement `n`.
> Retournez le nombre minimum de prime nécessaires, ou `-1` si c'est impossible.

**Contrôles* *

Variable
C'est quoi ?
1 ... 1 000
1 ... 1 000

---

Pourquoi ça ressemble à un changement de pièce

* Les premiers agissent comme **pièces** (approvisionnement non consolidé).
* Nous voulons que les pièces **fewest** atteignent une valeur cible.
* Solution classique de programmation dynamique (DP): "dp[i] = min(dp[i], dp[i‐coin] + 1)".

La seule torsion : nous devons limiter le jeu de pièces aux premiers "m" premiers.

---

Algorithme de haut niveau

1. ** Générer les premiers** jusqu'à `n` en utilisant le Sieve d'Eratosthenes.
*Seules les primes ≤ `n` peuvent contribuer à une somme de `n`. *
2. **Collectez les premiers "m" premiers** du tamis.
*Si `m` est plus grand que le nombre de premiers ≤ `n`, nous arrêtons tôt. *
3. **PDD sans limite (dp[0] = 0').
*Pour chaque prime `p`*
* pour `s = p ... n`
* `dp[s] = min(dp[s], dp[s-p] + 1)`
4. **Réponse**: `dp[n]` s'il est accessible, autrement `-1`.

- Oui. Pourquoi ça marche

* ** Substructure optimale** – le meilleur moyen d'atteindre les « s » utilise le meilleur moyen d'atteindre les « s-p » plus un autre « p ».
* **Sous-problèmes de recouvrement** – DP stocke déjà calculé des nombres minimaux.
* **Débordement** – la boucle interne itère **en augmentant** `s`, permettant le même premier à être utilisé plusieurs fois.

---

Analyse de complexité

Étape Temps Espace
C'est pas vrai.
Sieve (jusqu ' à `n`) Autres
Recueillir les premiers "m` prime" "O(n)" "O(min(m, π(n))" Autres
DP="O(n · min(m, π(n))" Autres

Avec `n ≤ 1000`, c'est trivial – facilement < 1 ms.

---

Code en trois langues

Ci-dessous vous trouverez des implémentations propres et commentées dans **Java**, **Python** et **C++**.
Tous suivent le même squelette algorithmique.

---

### Java

"Java
Importation de java.util.*;

solution de classe publique {
public int minNumberOfPrimes(int n, int m) {
// 1. Siéger jusqu ' à n
booléen[] isPrime = nouveau booléen[n + 1];
Arrays.fill(isPrime, true);
si (n >= 0) estPrime[0] = faux;
si (n >= 1) estPrime[1] = faux;
pour (int i = 2; i * i <= n; i++) {
si (isPrime[i]) {
pour (int j = i * i; j <= n; j += i) isPrime[j] = false;
}
}

// 2. Recueillir les premiers m prime (mais seulement ceux ≤ n)
Liste <Integer> prime = nouvelle liste d'array<>();
pour (int i = 2; i <= n && primes.size() < m; i++) {
si (isPrime[i]) prime.add(i);
}

// 3. PDD (changement de monnaie non consolidé)
int INF = entier.MAX_VALUE / 2; // éviter le débordement
int[] dp = nouvelle int[n + 1];
les tableaux.fill(dp, INF);
dp[0] = 0;

pour (int p : prime) {
pour (int s = p; s <= n; s++) {
dp[s] = Math.min(dp[s], dp[s - p] + 1);
}
}

retour dp[n] == INF ? -1 : dp[n];
}

public statique vide principal(String[] args) {
System.out.println(nouvelle solution().minNumberOfPrimes(10, 2)); // 4
System.out.println(nouvelle solution().minNumberOfPrimes(15, 5)); // 3
System.out.println(nouvelle solution().minNumberOfPrimes(7, 6)); // 1
}
}
«» "

---

Python

'`python
importer des maths
de taper l'importation Liste

Solution de classe:
def minNumberOfPrimes(self, n: int, m: int) -> Int:
Sieve
is_prime = [True] * (n + 1)
si n >= 0: is_prime[0] = Faux
si n >= 1: est_prime[1] = Faux
pour i dans la gamme(2, int(math.isqrt(n)) + 1):
si est_prime[i]:
étape = i
début = i * i
is_prime[start:n + 1:step] = [False] * ((n - start) //step + 1)

2. Premiers mois
prime = [i pour i dans la plage(2, n + 1) si is_prime[i][:m]

# 3. PDD
INF = 10 ** 9
dp = [INF] * (n + 1)
dp[0] = 0
pour p en prime:
pour s dans la plage (p, n + 1):
dp[s] = min(dp[s], dp[s - p] + 1)

retour -1 si dp[n] == INF autre dp[n]


si __nom__ == "__main__" :
sol = Solution()
print(sol.minNumber OfPrimes(10, 2)) # 4
print(sol.minNumberOfPrimes(15, 5)) # 3
print(sol.minNumberOfPrimes(7, 6)) # 1
«» "

---

### C++ (GNU C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minNumberOfPrimes(int n, int m) {
// 1. Siéger jusqu ' à n
vector<bool> isPrime(n + 1, true);
si (n >= 0) estPrime[0] = faux;
si (n >= 1) estPrime[1] = faux;
pour (int i = 2; i * i <= n; ++i)
si (isPrime[i])
pour (int j = i * i; j <= n; j += i)
isPrime[j] = faux;

// 2. Premiers mois
vecteur <int> premiers;
pour (int i = 2; i <= n && (int)primes.size() < m; ++i)
si (isPrime[i]) primes.push_back(i);

// 3. PDD
INF = 1e9;
vecteur<int> dp(n + 1, INF);
dp[0] = 0;
pour (int p : prime)
pour (int s = p; s <= n; +)
dp[s] = min(dp[s], dp[s - p] + 1);

retour dp[n] == INF ? -1 : dp[n];
}
};

Int main() {
Solution sol;
Cout << sol.minNumberOfPrimes(10, 2) << '\n'; // 4
nombre de primes(15, 5) << '\n'; // 3
<< sol.minNumberOfPrimes(7, 6) << '\n'; // 1
}
«» "

---

## -----------------

Catégorie Pourquoi il est bon Pourquoi il pourrait être mauvais
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Bon**• Le tamis O(n log n) est optimal pour les petits `n`. <br>• Le DP est *exact* et fonctionne dans < 1 ms. <br>• Le code est propre et entièrement sûr du type.
**Bad** Si vous ignorez la contrainte "m" première et utilisez simplement tous les premiers ≤ `n`, vous allez sur-compter. <br>• L'utilisation d'un PDD 2-D (« dp[prime][sum]») gaspille la mémoire supplémentaire O(m·n). **Utiliser `dp[i] = min(dp[i], dp[i‐p] + 1)» à l'intérieur de la même boucle primaire mais itérating `s` décroissant → qui donne *non bordé*?** – En fait, l'ordre décroissant interdit de réutiliser la même pièce dans la même itération, donnant *0-1* comportement. Autres
**Ugly**. • Remise en œuvre d'un test de primalité par divisions répétées au lieu d'un tamis → O(n √n). <br>• Liure supérieure codée en dur de 1000, ce qui rend la solution fragile pour les grands cas d'essai. <br>• Utiliser la récursion avec mémoisation mais oublier de passer `m`-limite peut faire sauter la pile. • Les performances se dégradent sur les plus grandes «n» (par exemple, 1 000 000). Éviter les variables d'état global ou statiques qui transportent des données statiques dans les cas d'essai. Autres

---

Ce que les intervieweurs recherchent

1. **Reconnaissant le modèle** (Modification des pièces).
2. **Traitement de la première restriction < < m > >**.
3. **Mettre en œuvre le tamis correctement** (éviter les erreurs hors-par-un).
4. **Efficacité du temps/de l'espace**: «O(n)» pour le PDD est une réponse claire.

Dans une entrevue, vous devriez :

* ** Expliquez l'algorithme en mots d'abord** – montrez que vous pouvez mapper le problème à un modèle connu.
* **Setch la récurrence DP** sur un tableau blanc.
* **Cas du bord de la mention** (plus grand que le nombre de prime ≤ `n`, sommes impossibles).
* **Discuse les optimisations potentielles** (p. ex., sortie anticipée si `dp[n]=1`, ou en utilisant le DP bit-set pour une vitesse supplémentaire).

Ces points sont *transférables* à de nombreux problèmes d'entrevues : *programmation dynamique*, *knapsack sans limite*, *génération de nombres primaires*, *LeetCode*.

---

Article de blog prêt au SEO

Titre (H1)
> LeetCode 3610: Nombre minimum de Primes à Sommer à Cible – Une solution de DP propre (Java, Python, C++)

---

Intro (H2)

> Êtes-vous en train de préparer un entretien d'ingénierie **logiciel**?
> Aujourd'hui, le projecteur est **LeetCode #3610 – Nombre minimum de Primes à Somme à Cible**.
> Le problème peut sembler un puzzle de maths obscur, mais c'est en fait un exercice **classique de programmation dynamique** que beaucoup d'intervieweurs aiment lancer aux candidats.
> Dans ce post, vous allez apprendre la solution complète dans **Java, Python et C++**, plus pourquoi l'algorithme est parfait pour les questions d'entrevue.

Mots-clés : LeetCode 3610, nombre minimum de premiers à la somme de cible, programmation dynamique, changement de pièce, entretien d'emploi, entretien d'ingénierie logicielle, Java Python C++.

---

### Énoncé du problème (H3)

> Compte tenu des nombres entiers `n` (somme cible) et `m` (nombre de premiers nombres disponibles), sélectionnez un ensemble multiple des premiers nombres primaires `m` (tout premier nombre peut être réutilisé) afin que la somme soit exactement `n`.
> Produit le nombre minimal de premiers utilisés, ou `-1` si impossible.

Contraintes: «1 ≤ n, m ≤ 1 000».

---

### Pourquoi c'est un problème de changement de pièce (H3)

- **Primes = pièces**: Chaque prime peut être utilisé des temps illimités.
- **Objectif**: Moins de pièces → moins de prime.
- **PDD connu**: "dp[i] = min(dp[i], dp[i‐coin] + 1)".
- **Special Twist**: N'utiliser que les premiers premiers "m"**.

---

La marche de l'algorithme (H3)

1. **Sieve d'Eratosthenes** – générer toutes les prime jusqu'à `n`.
2. **Prenez les premiers "m" premiers** du tamis (arrêtez tôt si moins de premiers existent).
3. **Knapsack DP** – remplir un tableau `dp[0...n]` où "dp[s]" est la prime minimale nécessaire pour la somme "s".
4. Return `dp[n]` ou `-1` s'il n'est pas accessible.

*(Voir les extraits de code ci-dessous.) *

---

Mise en œuvre Java (H3)

"Java
Importation de java.util.*;

solution de classe publique {
public int minNumberOfPrimes(int n, int m) {
// 1. Sieve
booléen[] isPrime = nouveau booléen[n + 1];
Arrays.fill(isPrime, true);
si (n >= 0) estPrime[0] = faux;
si (n >= 1) estPrime[1] = faux;
pour (int i = 2; i * i <= n; i++) {
si (isPrime[i]) {
pour (int j = i * i; j <= n; j += i) isPrime[j] = false;
}
}

// 2. Premiers mois
Liste <Integer> prime = nouvelle liste d'array<>();
pour (int i = 2; i <= n && primes.size() < m; i++) {
si (isPrime[i]) prime.add(i);
}

// 3. PDD
int INF = entier.MAX_VALUE / 2;
int[] dp = nouvelle int[n + 1];
les tableaux.fill(dp, INF);
dp[0] = 0;

pour (int p : prime) {
pour (int s = p; s <= n; s++) {
dp[s] = Math.min(dp[s], dp[s - p] + 1);
}
}

retour dp[n] == INF ? -1 : dp[n];
}
}
«» "

---

Mise en œuvre de Python (H3)

'`python
importer des maths
de taper l'importation Liste

Solution de classe:
def minNumberOfPrimes(self, n: int, m: int) -> Int:
♪ Sieve
is_prime = [True] * (n + 1)
si n >= 0: is_prime[0] = Faux
si n >= 1: est_prime[1] = Faux
pour i dans la gamme(2, int(math.isqrt(n)) + 1):
si est_prime[i]:
pour j dans la plage (i * i, n + 1, i):
is_prime[j] = Faux

Première année
prime = [i pour i dans la plage(2, n + 1) si is_prime[i][:m]

# PDD
INF = 10 ** 9
dp = [INF] * (n + 1)
dp[0] = 0
pour p en prime:
pour s dans la plage (p, n + 1):
dp[s] = min(dp[s], dp[s - p] + 1)

retour -1 si dp[n] == INF autre dp[n]
«» "

---

### C++ Mise en œuvre (GNU C++17) (H3)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minNumberOfPrimes(int n, int m) {
// Sieve
vector<bool> isPrime(n + 1, true);
si (n >= 0) estPrime[0] = faux;
si (n >= 1) estPrime[1] = faux;
pour (int i = 2; i * i <= n; ++i)
si (isPrime[i])
pour (int j = i * i; j <= n; j += i)
isPrime[j] = faux;

// Premiers mois
vecteur <int> premiers;
pour (int i = 2; i <= n && (int)primes.size() < m; ++i)
si (isPrime[i]) primes.push_back(i);

// PDD
INF = 1e9;
vecteur<int> dp(n + 1, INF);
dp[0] = 0;
pour (int p : prime)
pour (int s = p; s <= n; +)
dp[s] = min(dp[s], dp[s - p] + 1);

retour dp[n] == INF ? -1 : dp[n];
}
};
«» "

---

Analyse de complexité (H3)

- **Sieve**: temps `O(n log n)`, espace `O(n)`.
- **DP**: temps «O(n)», espace «O(n)».
- **Dans l'ensemble**: "O(n log n)" temps, "O(n)" mémoire – parfait pour "n ≤ 1 000".

---

### Prise- Conseils pour les entrevues (H3)

1. **Reconnaissance de la carte** – carte de la Knapsack non liée.
2. **Suivez la correction** – Attention aux erreurs.
3. **Récurrence des PV** – tableau blanc.
4. **Edge cas** – expliquer `m > #primes ≤ n` et les sommes inaccessibles.
5. **Optimisations** – arrêt anticipé si `dp[n] == 1`.

---

Conclusion (H2)

> Le problème **Minimum Nombre de Primes à Somme à Cible** est plus qu'un simple tour de LeetCode.
> Il démontre comment un problème basé sur **math** peut être résolu avec un modèle de **programmation dynamique** bien connu, une compétence que chaque candidat à l'ingénierie logicielle senior devrait maîtriser.
> Essayez de le coder dans votre langue préférée (Java, Python, C++) et exécutez les cas de test – vous serez prêt à impressionner les intervieweurs avec la théorie et la pratique.

---

### Appel à l'action (H2)

> Vous voulez d'autres solutions de style interview?
> Abonnez-vous à notre newsletter pour obtenir les dernières informations **LeetCode** et **Coding interview tips** en **Java, Python, C++**.

---

Enveloppe (H2)

Vous avez maintenant :

- ** Solution complète et efficace** en trois langues populaires.
- **Inspecter les modèles algorithmiques** qui résonnent dans les interviews.
- A **SEO-optimized blog post** qui est partagée et découverte pour toute personne étudiant LeetCode ou se préparant à une entrevue d'emploi.

Bon codage, et bonne chance pour votre prochaine interview!