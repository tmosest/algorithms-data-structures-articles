---
titre: LeetCode 3116. Kth plus petite quantité avec une seule combinaison de dénomination -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de la solution

Ci-dessous, vous trouverez trois implémentations prêtes à la production pour **LeetCode 3116 – Kth Plus petite quantité avec une seule combinaison de dénomination**.
Tous les trois utilisent la même idée :

1. **Inclusion–Exclusion** pour compter le nombre de montants valides ≤ X.
2. **Recherche binaire** sur l'espace de réponse.
3. arithmétique 64 bits (Java `long`, Python `int`, C++ `long`) pour rester dans les limites.

> **Pourquoi ça marche* *
> Chaque dénomination peut être utilisée infiniment plusieurs fois, mais les pièces de *différentes* dénominations ne peuvent être mélangées.
> Pour un ensemble fixe `S` de dénominations, chaque quantité accessible est un multiple de
> `lcm(S)` (le moins commun est multiple).
> Inclusion–Exclusion permet de compter le nombre de multiples de *any* lcm tout en évitant les doubles intersections de comptage.

---

## 1.1 Java (Java 17)

"Java
Importation de java.util.*;

solution de classe publique {

/** Point d'entrée principal pour LeetCode. */
public long findKthSmallest(int[] coins, int k) {
n = durée des pièces;
// Tous les sous-ensembles non vides – 2^n - 1 possibilités
Liste <Long> lcmList = nouvelle liste de répartition<>(1 < n);

// Précalculer lcm pour chaque sous-ensemble et retenir son signe
pour (int masque = 1; masque < (1 < < n); ++masque) {
long lcm = 1;
pour (int i = 0; i < n; ++i) {
si ((masque & (1 << i)) != 0) {
lcm = lcm(lcm, pièces [i]);
}
}
// Inclusion–Signal d'exclusion: + pour taille impair, – pour taille uniforme
Int bits = Integer.bitCount(masque);
lcmList.add(bits % 2 == 1 ? lcm : -lcm);
}

long bas = 1, haut = Long.MAX_VALUE; // haut peut être très grand
pendant que (faible < haut) {
long milieu = faible + (élevé - faible) / 2;
si (compte (milieu, lcmListe) < k) {
faible = milieu + 1; // la réponse est plus grande
} autre {
haute = moyenne; // la réponse peut être moyenne ou plus petite
}
}
retour faible;
}

*** Compter le nombre de montants ≤ cible pouvant être représentés. */
compte long privé(cible longue, liste <Long>lcmList) {
longue cnt = 0;
pour (long lcm : lcmList) {
cnt += cible / lcm; // négatif lcm soustrait automatiquement
}
retour cnt;
}

/** Aides classiques gcd / lcm qui ne débordent jamais. */
privé long gcd(long a, long b) {
pendant que (b != 0) {
long tmp = a % b;
a = b;
b = tmp;
}
retour a;
}

privé long lcm(long a, long b) {
retourner a / gcd(a, b) * b; // (a/gcd)*b ne déborde jamais de 64 bits
}
}
«» "

*Pourquoi le code est sûr*
`a / gcd(a, b)` est exécuté en premier, donc nous ne multiplions jamais deux grands nombres qui pourraient déborder.
L'espace de recherche est limité par `Long.MAX_VALUE`; la recherche binaire s'arrête lorsque `low == high`, qui est garanti être la réponse parce que la fonction `count(x)` est monotonique.

---

## 1.2 Python 3

'`python
d'importation de mathématiques gcd
de taper l'importation Liste

Solution de classe:
def trouver KthSmallest(self, coins: List[int], k: int) -> Int:
n = len(coins)
lcm_list = []

# Précalculer lcm pour chaque sous-ensemble non vide
pour masque de portée(1, 1 << n):
l = 1
pour i dans la plage(n):
si masque & (1 << i):
1 = l * pièces[i] // gcd(l, pièces[i])
bits = bin(masque).count('1')
lcm_list.append(l si bits % 2 == 1 autre -l)

def count(x: int) -> Int:
somme de retour(x // l pour l en lcm_list)

lo, hi = 1, 2 ** 63 - 1 # Python int n'a pas de limite mais nous le plafonnons
alors que:
milieu = (lo + hi) // 2
si nombre(milieu) < k:
lo = milieu + 1
Sinon:
hé = milieu
retour lo
«» "

*Notes de python*
* `int` est arbitraire-précision, donc nous ne nous inquiétons pas de débordement.
* `2**63-1` est utilisé pour refléter la longue limite Java; l'algorithme convergerait encore si nous utilisions une limite encore plus grande.

---

## 1,3 C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
longue découverte KthSmallest(vecteur<int>& coins, int k) {
int n = coins.size();
vecteur <long> lcm_liste;
lcm_list.reserve(1 << n);

// Précalculer lcm pour chaque sous-ensemble non vide
pour (int masque = 1; masque < (1 < < n); ++masque) {
long l = 1;
pour (int i = 0; i < n; ++i) {
si (masque et (1 << i)) {
l = lcm(l, long)coins[i];
}
}
bits int = __constructin_popcount(masque);
lcm_list.push_back(bits & 1 ? l : -l);
}

nombre automatique = [&](long long x) {
longue rés = 0;
pour (long l : lcm_list)
res += x / l; // négatif l soustrait automatiquement
retour rés;
};

longue longue lo = 1, hi = LLONG_MAX;
pendant qu ' il y a (l < bonjour) {
long long milieu = lo + (hi - lo) / 2;
si (count(mid) < k) lo = milieu + 1;
Autre salut = milieu;
}
retour lo;
}

particulier:
// gcd / Icm aides qui évitent le débordement
long long gcd(long long a, long b) {
b) { long t = a % b; a = b; b = t; }
retour a;
}

long long lcm (long long a, long long b) {
retourner a / gcd(a, b) * b; // (a/gcd)*b en sécurité en 64 bits
}
};
«» "

---

♪ 2. Article de blog – LeetCode de maîtrise 3116: Le bon, le mauvais, et le mauvais

> **Mots clés**: LeetCode 3116, Kth plus petite quantité, Inclusion–Exclusion, Recherche binaire, Algorithme Interview, Problème de pièce, Entrevue de codage, Défis de programmation, Conseils d'entrevue

---

2.1 Aperçu du problème

LeetCode 3116 – *Kth plus petit montant avec une seule combinaison de dénomination* – vous donne un ensemble de **dénominations de pièces distinctes** et demande:

> *Vous avez un approvisionnement infini de chaque pièce, mais vous ne pouvez pas mélanger différentes dénominations. Quelle est la quantité **k‐th la plus petite** qui peut être faite? *

Les contraintes en font un problème classique de nombre par valeur :

* `coins.longueur ≤ 15` – assez petite pour permettre le dénombrement bit-masque.
* `coins[i] ≤ 25` – valeurs des pièces de petite taille.
* `k ≤ 2·109` – la réponse peut être énorme, jusqu'à `Long. MAX_VALUE'.

Vous devez produire une réponse **exacte** entière.

---

## 2.2 Pourquoi la force brute fait défaut

Un algorithme naïf :

1. Générer tous les multiples de chaque pièce jusqu'à un énorme lien.
2. Fusionne-les et trie.
3. Choisissez le k-th.

Même avec un lien comme `109`, vous généreriez des dizaines de millions de nombres – beaucoup trop lents et intensifs en mémoire. En outre, la réponse pourrait être bien au-delà de toute simple limite.

Nous avons donc besoin d'une approche plus intelligente.

---

## 2.3 Le point de vue : inclusion – exclusion + recherche binaire

2.3.1 Inclusion–Exclusion

Pour tout sous-ensemble `S` de dénominations, chaque quantité accessible est un multiple de `lcm(S)` (le moins commun multiple).
Si nous comptons combien de multiples de `lcm(S)` sont ≤ X, nous obtenons `=X / lcm(S)=".

Mais nous ne pouvons pas simplement résumer tous les sous-ensembles parce qu'un nombre qui est un multiple de *deux* `lcm(A)` et `lcm(B)` serait double-comptabilisé.
**Inclusion–Exclusion** corrige ceci:

«» "
count(X) = (-1)^(-)(-)
sur tous les sous-ensembles non vides S
«» "

Le signe est **positif** lorsque la taille du sous-ensemble est étrange, **négatif** lorsque même.

Avec `n ≤ 15`, il y a au plus `2n−1 = 32 767` sous-ensembles – triviaux à précalculer.

### 2.3.2 Recherche binaire

`count(X)` est une fonction non décroissante.
Nous pouvons rechercher le plus petit `X` tel que `count(X) ≥ k`.
Parce que `k` peut être jusqu'à `2·109`, l'espace de recherche est grand, mais le log2(29) 32 itérations – rapide.

La clé est d'utiliser **64-bit** arithmétique (`long long` / `long`) pour éviter le débordement.
Le lcm jusqu'à 15 numéros, chacun ≤ 25, convient confortablement en 64 bits:
`257 φ 6.1·109`, et le produit de l'ensemble des 15 est au plus `2515 φ 9.3·1019` – toujours < `9.22·1018` (`Long.MAX_VALUE`).

---

2.4 Pièges de mise en œuvre

Ce qui arrive
- C'est quoi ?
**Les dépassements en lcm**. Calculer d'abord `a / gcd(a, b): `lcm = (a / gcd) * b`.
**High lied too low**= Si vous cap `high` à `k * max_coin`, vous pouvez manquer la réponse si elle se trouve au-dessus. Autres Utilisez `Long.MAX_VALUE` ou `LLONG_MAX`. L'algorithme converge encore parce que nous n'avons besoin que de la monotonicité, pas d'une limite supérieure exacte. Autres
**Négatif signe de lcm** Conservez chaque lcm avec son signe (±). `count(X)` puis utilise `X / lcm` directement; un lcm négatif soustrait automatiquement. Autres
**Time-outs in Python**= Le somme de plus de 32k lcm dans chaque itération est très bien, mais l'utilisation de `2**63-1` comme limite supérieure conduit à de grands entiers qui sont lents. Tenir le lien petit (par exemple, `2**63-1`) et laisser Python's int gérer tout débordement. Autres

---

2.5 Pourquoi l'approche est optimale

* **Pré-computation**: valeurs de 32k lcm → O(2n) 104 opérations.
* **Count**: divisions «O(2n)» par «compte(X)».
* **Binary Search**: 64 itérations × 32k divisions 2 millions de divisions entières – sous-seconde dans n'importe quelle langue.

La consommation de mémoire est négligeable : nous ne stockons que la liste de lcm (~64 kB).
La solution est donc *optimale* compte tenu des contraintes.

---

2.6 Erreurs courantes d'entrevue

Erreurs Symptômes Comment éviter
- C'est quoi ?
En supposant que k-th valeur égale `k * min_coin`. Utilisez la recherche binaire avec le comptage exact. Autres
Mélanger `int` et `long` en Java. "Conservez tout dans "long". Calculer `(a / gcd(a, b)) * b`.
Autres Oublier le signe dans inclusion – exclusion. Mauvaise réponse pour de nombreux cas de test. Enregistrer explicitement `±lcm` pour chaque sous-ensemble. Autres
Utiliser `int` pour la recherche liée dans C++. Autres

---

2.7 Takeaway: Construire une fonction de comptage, puis rechercher

Face à des contraintes qui rendent impossible le dénombrement, le schéma commun est :

1. **Count** – Construire une fonction monotonique rapide `f(x)` qui vous indique combien de valeurs ≤ x satisfont à la propriété.
2. **Recherche binaire** – Trouvez le seuil où `f(x) ≥ k`.

Cette stratégie apparaît dans des problèmes comme:

* K-th numéro divisible (Code Leet 1794).
* K-th laid number (LeetCode 264).
* K-th plus grande valeur dans une matrice.

LeetCode 3116 est simplement une variante qui vous force à combiner des sous-ensembles *différents* de pièces. Maîtriser le modèle d'inclusion-exclusion vous aidera à conquérir de nombreux autres puzzles de compte-par-subset.

---

2.8 Liste de contrôle de l'entrevue – Amies

Liste de contrôle
-- -- -- -- -- --
Utiliser **bit‐masque** pour énumérer tous les sous-ensembles (= 32k). Autres
Calculez `lcm` en toute sécurité: `a / gcd(a, b) * b`.
Entreposez chaque signe de sous-ensemble (`+` pour la taille impair, `-` pour la même). Autres
Écrire un `compte(x)` qui iternise sur la liste précalculée. Autres
Recherche binaire sur `[1, Long.MAX_VALUE]` (ou `LLONG_MAX`). Autres
Utilisez `long`/`long long` partout dans Java / C++. Autres
Tester les cases de bord: `k = 1`, `k` à la limite supérieure, pièce unique, toutes les pièces. Autres

---

2.9 Réflexions finales

LeetCode 3116 est un formidable micro-challenge qui vous force à :

1. **Reconnaissez** que le comptage par valeur est préférable à la production de valeurs.
2. **Appliquer** Inclusion–Exclusion correctement.
3. **Combinez le comptage avec une recherche monotone.

La solution qui en résulte est propre, mathématiquement élégante et fonctionne en microsecondes sur n'importe quel processeur moderne. Maîtriser ce modèle vous donnera un outil puissant pour votre prochaine entrevue de codage.

Bon codage ! C'est ce qu'il a dit.

---



♪ 3 Remarques finales

*Les implémentations Java, Python et C++ ci-dessus sont prêtes à être soumises sur LeetCode. *
*L'article de blog est structuré pour guider les lecteurs de l'intuition à la mise en œuvre, en soulignant les pièges communs et comment les éviter. *

N'hésitez pas à copier, coller et lancer les extraits dans votre IDE ou dans l'éditeur LeetCode. Bonne chance pour votre entretien !