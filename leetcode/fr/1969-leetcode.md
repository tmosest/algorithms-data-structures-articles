---
titre: LeetCode 1969. Produit minimum non zéro des éléments de la grille -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## ☆ 1969 – Produit minimum non zéro des éléments d'array
**LeetCode – Medium**

> **TL;DR** – Le produit optimal est
> "((2^p – 2)^(2^(p-1)-1) * (2^p – 1)) mod 1e9+7"
> (pour `p > 1`, sinon la réponse est `1`).
> Les trois solutions linguistiques ci-dessous fonctionnent dans l'espace **O(p)** et **O(1)**.

---

- Oui. 1. Récapitulation des problèmes

Description
C'est pas vrai.
**Input**
**Array `nums`**=1-indexé contenant chaque entier de `1` à `2^p-1` sous forme binaire=
**Exploitation**= Choisissez deux numéros `x` et `y` et échangez un bit *correspondant* (c'est-à-dire la même position de bit) entre eux, n'importe quel nombre de fois==
**Objectif**= Trouver le produit *minimum non-zéro* de tous les éléments du tableau après des swaps arbitraires, puis afficher ce produit modulo `1 000 000 007`. Autres

> **Important** – Le produit à minimiser est ** avant de prendre le modulo.
> Cela signifie que nous devons calculer le produit minimal exact (potentiellement gigantesque) et ensuite appliquer le module.

---

- Oui. 2. Pourquoi c'est une grande question d'entrevue

Aspect Pourquoi ça compte
-- -- -- -- -- --
**Le raisonnement au niveau du bit** Autres
**Propreté mathématique** Autres
**Arithmétique modulaire** Autres
Le produit naïf est astronomiquement énorme, de sorte qu'un algorithme doit travailler sur la *structure* des nombres, et non sur les nombres eux-mêmes. Autres

> **Astuce**: Dans une entrevue en direct, dessinez la preuve sur papier, puis concentrez-vous sur la mise en œuvre de la formule. La partie de la preuve peut être raccourcie à "Nous avons prouvé que la configuration optimale est ....

---

- Oui. 3. Intuition et configuration optimale

1. **Nombre total de bit en position* *
Dans le tableau initial `1 ... 2^p-1` chaque position bit est définie exactement `2^(p-1)` fois.
L'échange ne change pas ces totaux.

2. **Nombres de logements**
Paire `x` avec son complément bitwise `2^p-1-x`.
Dans chaque paire, l'union des bits est tous les uns, donc après les swaps nous pouvons faire un élément **plein de ceux** (valeur `2^p-2`) et l'autre **simple 1** (valeur `1`).

3. **L'élément le plus élevé**
Le nombre `2^p-1` a tous les bits.
Dans l'arrangement optimal, il reste intact – sinon nous créerions un zéro dans le produit.

4. **Résultats multiset**
«» "
(2^p-2) répétés (2^p-2)/2 fois,
1 répétition (2^p-2)/2 fois,
Une fois
«» "

5. **Produit minimal**
«» "
((2^p-2) ^ ((2^p-2)/2)) * (2^p-1)
«» "

> **Pourquoi est-ce minimal? **
> Tout élément avec plus d'un "1" bits peut être "pushed" dans la moitié supérieure pour réduire le produit (parce que la moitié inférieure se compose de plus petits nombres).
> La preuve dans l'éditorial original LeetCode montre rigoureusement que chaque configuration optimale doit ressembler à celle ci-dessus.

---

- Oui. 4. Algorithme

Étape Action Complexité
C'est quoi, ça ?
# 1= Poignée `p = 1= → retour "1".
Calculer `q = 2^p - 2`.
Calculer `exp = q / 2`.
O(log exp) → O(p) parce que `exp < 2^p`. Autres
Résultat = "pouvoir * (q + 1) mod MOD".

`MOD = 1_000_000_007`.

L'algorithme est linéaire dans le nombre de bits (`p`) – assez rapide pour `p ≤ 60`.

---

- Oui. 5. Preuve de l ' exactitude

1. **Invariant du nombre de bits** – L'échange conserve le nombre total de `1`s par bits.
2. **Construction** – Nous pouvons réaliser la configuration décrite dans la section 3 en déplaçant à plusieurs reprises chaque `1` sauf le moins significatif dans le même nombre.
3. **Optimalité** –
*Toute* nombre dans la moitié inférieure (`< 2^p-1`) qui a plus d'un `1` peut être diminué en déplaçant l'un de ses `1` à un nombre plus grand.
Répéter cet argument oblige tous les nombres de moitié inférieurs à devenir soit `1` ou `2^p-2`.
Le seul nombre qui peut rester plus grand que `2^p-2` est le `2^p-1` original.
4. ** Minimalité** – Parmi toutes ces configurations, le produit est fixe (même multiset), donc minimal. *

---

- Oui. 6. Mise en œuvre

Voici des solutions propres et idiomatiques dans **Java**, **Python** et **C++**.
Tous utilisent la même routine d'exposition modulaire rapide.

##### 6.1 Java

"Java
importation java.io.*;

solution de classe publique {
finale statique privée longue MOD = 1_000_000_007L;

/** Exponentiation rapide (x^e mod MOD) */
modPow statique privé (long x, long e) {
longue r = 1;
x %= MOD;
pendant que (e > 0) {
Si (e & 1) == 1) r = (r * x) % MOD;
x = (x * x) % MOD;
e >>= 1;
}
retour r;
}

Produit(int p) {
si (p == 1) retourner 1; // cas dégénéré
longue q = (1L << p) - 2; // 2^p - 2
longue durée = q >> 1; // (2^p - 2) / 2
long pow = modPow(q, exp);
long res = (pouvoir * (q + 1)) % MOD;
retour (int) rés;
}

/* ----- pour fonctionner localement ----- */
public statique vide main(String[] args) lance IOException {
BufferedReader br = nouveau BufferedReader(nouveau InputStreamReader(System.in));
int p = Integer.parseInt(br.readLine().trim());
System.out.println(nouvelle solution().minNonZeroProduct(p));
}
}
«» "

##### 6.2 Python

'`python
importations

MOD = 10 ** 9 + 7

def mod_pow(base: int, exp: int) -> Int:
"""retourne (base ** exp) % MOD en utilisant l'exposantiation binaire."""
résultat = 1
base %= MOD
pendant que exp:
si exp & 1:
résultat = (résultats * base) % MOD
base = (base * base) % MOD
Exp >>= 1
résultat du retour

Solution de classe:
def minNonZeroProduct(self, p: int) -> Int:
si p == 1:
retour 1
q = (1 << p) - 2 # 2^p - 2
Exp = q // 2
retour (mod_pow(q, exp) * (q + 1)) % MOD

Essai manuel rapide
si __nom__ == "__main__" :
print(Solution().minNonZeroProduct(int(sys.argv[1]))) # p.ex. solution python3. py 5
«» "

*### 6.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

longue MOD = 1'000'000'007LL;

// Expose rapide: base^exp % MOD
long long modPow(long long base, long exp) {
longue rés = 1;
base %= MOD;
pendant (exp) {
si (exp & 1) res = (res * base) % MOD;
base = (base * base) % MOD;
Exp >>= 1;
}
retour rés;
}

Int minNonZeroProduit(int p) {
si p == 1) retour 1; // cas particulier
long q = (1LL << p) - 2; // 2^p - 2
longue durée = q >> 1; // (2^p - 2) / 2
long long pow = modPow(q, exp);
retourner static_cast<int>(pow * (q + 1)) % MOD);
}

Int main() {
ios::sync_with_stdio(faux);
cin.tie (nullptr);

à l'intérieur p;
si (cin >> p) {
cout << minNonZeroProduct(p) << '\n';
}
retour 0;
}
«» "

> Les trois codes fonctionnent ** bien sous une milliseconde** pour `p = 60` (le pire cas).

---

- Oui. 7. Cas de bord et pièges communs

Piège
- Oui.
** `p = 1`** – `2^p-2` serait `0`, conduisant à `0^0` dans la formule. Retourne explicitement `1` quand `p == 1`. Autres
**Overflow in Java** – `1L << p` déborde si `p` > 63. Autres
**Modulo avant le produit minimum** – Beaucoup de participants prennent le module *inside* la boucle d'exposantiation incorrectement. Calculez le produit minimum *exactement* en utilisant la formule, puis appliquez `modPow` et la multiplication finale sous `MOD`. Autres
**L'utilisation de `int` pour les valeurs intermédiaires** – peut déborder. Toujours utiliser `long` (ou `BigInteger` en Java) pour les étapes intermédiaires. Autres

---

- Oui. 8. Essai des solutions

(avant mod)
- C'est pas vrai.
C'est vrai.
C'est vrai.
Dénomination des marchandises
1e9+7 = 184320
2 9+7 = 281936 Autres

(Pour les plus grands `p` les nombres explosent, mais nos formules les manipulent.)

Vous pouvez écrire un script rapide qui énumére le tableau pour le petit `p` (8) et vérifie le produit minimal contre la simulation de force brute.

---

- Oui. 9. Préparation de cette question

Compétence
C'est pas vrai.
**Comptabilité des bits**= Résoudre les problèmes comme==Coudre les bits dans une plage de bits== ou==Sum de bits sur tous les nombres==. Autres
**Proof by Construction**= Pratique prouvant qu'un arrangement avide est optimal (par exemple, faire tous les nombres soit 0 ou max=). Autres
**Expositions modulaires**= Rédigez `modPow` à partir de zéro, testez-le sur des cas de bord (`base = 0`, `exp = 0`). Autres
**LeetCode** Autres
**Interview Flow**= Croquer la preuve sur papier → calculer la formule → coder la formule → tester les cas de bord. Autres

---

10. OBJECTIFS DE RETRAITE

> **Mots clés**: *Produit Minimum Non-Zero des Eléments d'Array*, *LeetCode 1969*, *Bit manipulation interview*, *Java bitwise algorithme*, *Python fast pow*, *C++ exponentiation modulaire*, *coding interview preparation*, *software engineer interview questions*, *job interview algorithme*, *competitive programmation*.

Si vous lisez ceci parce que vous préparez une entrevue, rappelez-vous:

* LeetCode 1969 est un mélange parfait** de combinatoires, de preuves et d'implémentation.
* La clé est de **prouver la structure** de l'arrangement optimal une fois, puis mettre en œuvre la formule succincte.
* Les trois langues montrent que le même aperçu mathématique se traduit par un code propre et prêt à la production.

Bonne chance pour écraser votre prochain entretien de codage ! *

---

N° de feuille de référence du code

Langue Fonction Signature
- C'est quoi ?
Java `public int minNonZeroProduct(int p)`
Python Def minNonZeroProduct(self, p: int) -> int`
*C++=int minNonZeroProduct(int p)== fonction globale=

N'hésitez pas à copier les extraits dans votre éditeur local ou dans votre soumission LeetCode. Bon codage !