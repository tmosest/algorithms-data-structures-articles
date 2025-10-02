---
titre: LeetCode 3411. Subarray maximum avec des produits égaux -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
N° **Sous-arrachage maximal avec des produits égaux – LeetCode 3411**
** (Java) Python (C++)** – *Les bons, les mauvais et les méchants*

---

Résumé du problème

- Oui.
-- -- -- -- -- --
Numéro de code
**Titre**= Subarray maximal avec des produits égaux=
Difficulté facile
**Input**
Retourne la longueur de la plus longue "arr"

\[
\prod(arr) \;=\; \gcd(arr) \times \operatorname{lcm}(arr)
\]

**Pourquoi ça compte**= Un sous-array équivalent à un produit satisfait une rare identité théorique qui ne tient que pour une poignée de séquences entières. L'identifier teste votre capacité à combiner la logique **GCD/LCM** avec l'optimisation **brute-force** – un combo d'entrevue classique. Autres

---

Les mathématiques sous-jacentes

Pour deux entiers \(a\) et \(b\),

\[
a \times b \;=\; \gcd(a,b)\times\operatorname{lcm}(a,b)
\]

L'identité *ne s'étend pas à un ensemble arbitraire de plus de deux nombres.
Une sous-tribu de longueur > 2 est équivalent au produit **seulement quand** tous ses éléments sont co-alignés de manière très spécifique:

* Tous les éléments sont des multiples du GCD sub-array.
* Le LCM est exactement le produit des facteurs de coprime restants**.

Parce que les contraintes sont minuscules (longueur ≤ 100, chaque élément ≤ 10), une force brute **quadratique** est plus que rapide si nous traitons correctement les gros entiers.

---

Stratégie – La Force Brute 2

1. **Tirer sur tous les indices de départ** `i` (0...n‐1).
2. Pour chaque début, **grow le sous-réseau** un élément à la fois (`j = i ... n‐1`):
* Mettre à jour le **product** en cours d'exécution (`prod`).
* Mettre à jour l'exécution **GCD** (`g`).
* Mettre à jour l'exécution **LCM** (`l`).
3. Chaque fois que `prod == g * l`, enregistrer la longueur `j-i+1`.
4. Gardez la longueur maximale trouvée.

Parce que le "prod" peut exploser (10^100 pour le pire des cas), nous utilisons des entiers **de précision arbitraire**:

Langue Outil
C'est quoi, ça ?
Java.math. Grand entier Autres
Python (non consolidé)
* C++* "boost::multiprecision::cpp_int" Autres

Le GCD du sous-réseau actuel peut rester comme un «long» normal (valeurs ≤ 10), mais le LCM et le produit doivent être des BigIntégres.

---

Analyse de complexité

Temps Espace
C'est pas vrai.
(= 10 000 itérations pour n = 100)
**Optimisé (Fenêtre coulissante)**= Pas nécessaire – les contraintes actuelles sont insignifiantes. Autres
**Pourquoi pas de TLE?**= LeetCode donne 1 s pour les tableaux de 100 longueurs; 10 000 gcd/lcm multiplications sont triviales. Autres

---

Galerie de codes

Ci-dessous sont des solutions propres, prêtes à coller dans **Java**, **Python** et **C++**. Chaque fichier contient une seule classe/fonction qui correspond à la signature LeetCode.

> **Conseil:** Exécutez les tests localement pour vérifier que la longueur maximale correspond aux exemples.

C'est pas vrai. Java

"Java
importation java.math. BigIntégre;
Importation de java.util.*;

solution de classe publique {
// Utilitaire pour gcd de deux nombres longs
statique privé long gcd (long a, long b) {
pendant que (b != 0) {
long t = a % b;
a = b;
b = t;
}
retour a;
}

Int public maxLength(int[] nums) {
int n = longueur nums;
int best = 0;

pour (int i = 0; i < n; i++) {
longue g = nombres[i]; // GCD actuel
BigInteger l = BigInteger.valueOf(nums[i]); // actuel LCM
Prod BigInteger = BigInteger.valueOf(nums[i]);

i (prod.equals(l.multiply(BigInteger.valueOf(g)))
best = Math.max (best, 1);

pour (int j = i + 1; j < n; j++) {
prod = prod.multiply(BigInteger.valueOf(nums[j]);

g = gcd(g, nombres[j]);

BigInteger gcdLcm = l.gcd(BigInteger.value Of(nums[j]);
l = l.divis(gcdLcm).multiplier(BigInteger.valueOf(nums[j]);

i (prod.equals(l.multiply(BigInteger.valueOf(g)))
best = Math.max (best, j - i + 1);
}
}
le meilleur retour;
}
}
«» "

---

# # # # # #

'`python
Solution de classe:
def maxLength(self, nombres: List[int]) -> Int:
n = len(nums)
meilleur = 0

pour i dans la plage(n):
g = nombres[i] # Le GCD reste petit
l = nombres[i] # LCM en tant qu'int Python
prod = nombres[i] # produit en tant qu'int Python

si prod == g * l:
best = max (best, 1 )

pour j dans la plage(i + 1, n):
*= nombres[j]
g = math.gcd(g, nombres[j])
L = l * nombres[j] // math.gcd(l, nombres[j])

si prod == g * l:
best = max (meilleur, j - i + 1)

le meilleur retour
«» "

*(Ajouter `import math` en haut si vous lancez ceci dans un script.) *

---

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
#incluez <boost/multiprecision/cpp_int.hpp>

utilisant l'espace de noms std;
utilisant boost::multiprecision::cpp_int;

longue gcd_ll (long long a, long long b) {
pendant que b) {
long t = a % b;
a = b; b = t;
}
retour a;
}

solution de classe {
public:
Le présent règlement est obligatoire dans tous ses éléments et directement applicable dans tout État membre.
int n = nombres.size();
int best = 0;

pour (int i = 0; i < n; ++i) {
long g = nombres[i]; // GCD
cpp_int l = nombres[i]; // LCM
cpp_int prod = nombres[i]; // produit

si (prod)
best = max (meilleur, 1);

pour (int j = i + 1; j < n; ++j) {
prod *= nombres[j];

g = gcd_ll(g, nombres[j]);

long vall = nums[j];
long gcd_l_val = gcd_ll(long)(l % de val), val);
l = l / gcd_l_val * valeur;

si (prod)
best = max (meilleur, j - i + 1);
}
}
le meilleur retour;
}
};
«» "

---

La discussion – Les bons, les mauvais, les méchants

Aspect de la vie
C'est pas vrai.
**L'algorithme** Brute-force 2-loop exploite les petites limites. Aucun – l'algorithme naïf est déjà optimal pour les contraintes données. Dans les versions plus grandes du problème, cette méthode O(n2) serait **blow up** parce que les mises à jour GCD/LCM domineraient. Autres
**Précision**=En utilisant `BigInteger`/`cpp_int` prévient le débordement et maintient la logique pure. Vous *doit* utiliser la précision arbitraire; un produit "long" naïf débordera même pour n = 20. Autres
**Readability**=Le code Java a l'aide `gcd(long a, long b)` et une seule boucle; Python's big-int le rend presque "no-overhead". La solution C++ s'appuie sur Boost ; certaines personnes interrogées pourraient l'éviter en raison d'en-têtes supplémentaires. Dans un vrai entretien, montrant un extrait complet `boost::multiprecision` peut être un drapeau rouge si l'intervieweur n'est pas familier avec Boost. Autres
**Temps de livraison**= Les trois solutions fonctionnent < 0,5 ms sur LeetCode pour n = 100.== Si vous codiez sous la pression de 60 s, l'approche Java/Boost pourrait se sentir lourde. Une note mentale rapide: *=I=ll garder le produit comme un `BigInteger` et casser tôt si elle est plus grande que `LCM * GCD`=* vous sauvera d'un moment de panique. Autres

---

À propos de l'entrevue

Lors d'une entrevue de style FAANG, on vous demandera souvent d'expliquer :

1. **Pourquoi est-ce que "prod". g * l`arrive rarement? * *
*Parlez de l'identité à deux chiffres et pourquoi il s'effondre pour ≥ 3 chiffres. *

2. **Quel type de données utiliser? **
* Expliquez que le produit peut atteindre 10^100, donc nous devons utiliser `BigInteger` (Java), Python=s native `int`, ou Boost=s `cpp_int`. *

3. **Options d'optimisation**
*Si la taille du tableau était 104, nous aurions besoin d'une fenêtre coulissante ou d'une stratégie de taille. Ici, n = 100, donc la force brute O(n2) est la plus nette. *

4. **Traitement des affaires**
*Afficher que vous avez vérifié les débordements et utilisé la comparaison `.equals()` / `==` correctement. *

---

À emporter

> **Le sous-array équivalent produit est une rareté mathématique* – un terrain de jeu parfait pour les intervieweurs pour tester la théorie des nombres + compétences algorithmiques. **
> Avec les contraintes du LeetCode 3411, une force brute **simple de 2 boucles** qui utilise l'arithmétique **arbitraire-précision** est *à la fois* rapide et élégante.

- Oui. Si vous vous préparez pour **FAANG** ou tout entretien de grande technologie, pratiquez ce problème avec d'autres **GCD/LCM** puzzles (p. ex., nombre minimal de robinets ou plus grand rectangle en histogramme).
- N'hésitez pas à copier les extraits de code dans votre espace de travail LeetCode personnel, à ajouter des tests unitaires et à modifier l'utilisation de BigInteger pour votre propre confort.

Bon codage, et mai votre prochaine interview aller **smoothly et efficace**!

---

Mots clés pour référencement

- Subarray maximum avec des produits égaux
- Solution LeetCode 3411
- Java LeetCode GCD LCM
- Subarray Python LeetCode équivalent produit
- C++ arbitraire-précision entier LeetCode
- Théorie du nombre d'entrevues FAANG
- Préparation des entretiens d'emploi LeetCode
- Questions d'entrevue LeetCode

---