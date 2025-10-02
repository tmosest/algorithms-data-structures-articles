---
titre: LeetCode 2320. Nombre de façons de placer des maisons -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code 2320 : *Nombre de moyens de placer des maisons*
Python C++** – PDD monoligne + option O(log n) fast-pow
*Guide optimisé pour la réussite des entrevues sur l'ingénierie logicielle*

---

Récapitulation des problèmes

> **LeetCode 2320 – Nombre de moyens de placer des maisons* *
> Il y a des parcelles "2·n" sur une rue (deux côtés).
> Les parcelles de chaque côté sont numérotées `1 ... n`.
> Une maison peut être construite sur n'importe quel terrain, mais ** deux maisons du même côté ne peuvent pas être adjacentes**.
> Les maisons des côtés opposés sont indépendantes – une maison sur le terrain `i` d'un côté ne l'interdit pas** sur le terrain `i` de l'autre côté.
>
> Retourner le nombre total de placements possibles modulés «1 000 000 007».

Exemple Produit Explication
- C'est quoi ?
, à gauche, à droite, les deux Autres
Voir le diagramme dans le problème LeetCode

---

Les contraintes

- `1 ≤ n ≤ 104`
- Modulo: «MOD = 1 000 000 007»

> **Pourquoi n = 104 importe? * *
> Un simple "O(n2)" explose. Nous avons besoin d'une solution "O(n)" ou meilleure.

---

C'est vrai. Observations et principales perspectives

- **Les bords sont indépendants** – le placement sur le côté gauche n'influence jamais le côté droit.
- Les moyens de comptage pour *un* côté est un problème classique de maison adjacente.
- Laisser `f[n]` = moyens de remplir `n` des parcelles sur un seul côté.
- `f[0] = 1` (pas de placettes, une façon – vide).
- `f[1] = 2` (vide ou maison).
Pour `n ≥ 2`: `f[n] = f[n-1] + f[n-2]` (placer la maison sur la dernière parcelle → la parcelle précédente doit être vide).
- Ainsi `f[n]` suit la séquence Fibonacci déplacée par 2 positions:
`f[n] = Fib(n+2)` où `Fib(0)=0, Fib(1)=1`.
- Les deux parties étant indépendantes :
**Réponse = f[n] × f[n] mod MOD**.

---

Deux solutions optimales

Démarche Temps Espace Remarques de mise en oeuvre
- C'est pas vrai.
**Itérative DP** Simple boucle, conserve les deux derniers numéros de Fibonacci. Autres
**Exposition de puissance rapide / matrice** Utiliser la forme fermée de Fibonacci par doublement rapide. Autres

> **Pourquoi les deux ? **
> - Pour les intervieweurs : la compréhension du PDD et du doublage rapide montre de la profondeur.
> - Pour la production: `O(n)` est parfaitement amende jusqu'à 104, mais `O(log n)` est résistant à l'avenir pour les entrées plus importantes.

---

Code – trois langues

> Toutes les solutions utilisent `MOD = 1_000_000_007`.
> La version *Iterative DP* est la solution de base; la version *Fast-Power* est optionnelle.

#### 5.1 Java

"Java
solution de classe {
finale statique privée longue MOD = 1_000_000_007L;

// ---- O(n) PDD -------------------------------------------------------------------
public int countMaisonPlacements(int n) {
long a = 1; // f[0]
long b = 2; // f[1]
pour (int i = 2; i <= n; i++) {
long c = (a + b) % MOD;
a = b;
b = c;
}
retour (int) (b * b) % MOD); // f[n] * f[n] % MOD
}

// ---- Facultatif: O(log n) Doublage rapide --------------------------------
fib(long k) privé { // retourne Fib(k) mod MOD
si (k) 0) retour 0;
long a = 0, b = 1; // (F(0), F(1))
pour (int i = 63 - Long.numberOfLeadingZeros(k); i >= 0; i--) {
long d = (a * ((b * 2 % MOD - a + MOD) % MOD)) % MOD; // F(2n)
long e = (a * a % MOD + b * b % MOD) % MOD; // F(2n+1)
a = d;
b = e;
si ((k >> i) et 1) == 1) { // aller à n+1
long f = (a + b) % MOD; // F(2n+1) + F(2n)
a = b;
b = f;
}
}
retour a;
}

Int public countMaisonPlacementsFast(int n) {
fibNPlus2 = fib(n + 2); // f[n] = Fib(n+2)
retour (int) ((fibNPlus2 * fibNPlus2) % MOD);
}
}
«» "

5.2 Python

'`python
MOD = 1 000 000 007

Solution de classe:
N° ---- O(n) PDD -------------------------------------------------------------------
def countMaisonPlacements(self, n: int) -> Int:
a, b = 1, 2 # f[0], f[1]
pour _ dans la plage(2, n + 1):
a, b = b, (a + b) % MOD
retour (b * b) % MOD

- Oui. Facultatif: O(log n) Doublage rapide --------------------------------
def fib(self, k: int) -> Int: # Fib(k) % MOD
si k == 0:
retour 0
a, b = 0, 1
pour les bits en marche arrière(bin(k)[2:]):
d = (a * (b * 2 - a) % MOD)) % MOD
e = (a * a + b * b) % MOD
a, b = d, e
si bit == «1»:
a, b = b, (a + b) % MOD
retour a

def countMaisonPlacementsFast(self, n: int) -> Int:
fib_n_plus_2 = self.fib(n + 2)
retour (fib_n_plus_2 * fib_n_plus_2) % MOD
«» "

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
longue MOD = 1'000'000'007LL;

public:
// ---- O(n) PDD -------------------------------------------------------------------
Int countMaisonPlacements(int n) {
long a = 1, b = 2; // f[0], f[1]
pour (int i = 2; i <= n; ++i) {
long c = (a + b) % MOD;
a = b;
b = c;
}
retourner static_cast<int>(b * b) % MOD);
}

// ---- Facultatif: O(log n) Doublage rapide --------------------------------
long long fib(long long k) { // retour Fib(k) % MOD
si (k) 0) retour 0;
long a = 0, b = 1; // (F(0), F(1))
pour (int i = 63 - __constructin_clzll(k); *= 0; --i) {
longue durée d = (a * (b * 2 % MOD - a + MOD) % MOD; // F(2n)
long e = (a * a % MOD + b * b % MOD) % MOD; // F(2n+1)
a = d;
b = e;
si ((k >> i) & 1LL) { // passer à n+1
long f = (a + b) % MOD;
a = b;
b = f;
}
}
retour a;
}

Int countMaisonPlacementsFast(int n) {
long fibNPlus2 = fib(n + 2); // f[n] = Fib(n+2)
retourner static_cast<int>((fibNPlus2 * fibNPlus2) % MOD);
}
};
«» "

> **Astuce** – Les trois langues conservent **`long/long`** pour la multiplication intermédiaire afin d'éviter les débordements avant le `% MOD`.

---

# # # 6 Pourquoi ce blog vous fera sortir

Comment le blog le démontre
- C'est quoi ?
**La pensée algorithmique ** Nous avons brisé le problème en *indépendant* et utilisé Fibonacci. Autres
**La programmation dynamique** La boucle DP est une solution propre et conviviale. Autres
**Élégance mathématique** montre que vous pouvez repérer des formulaires fermés. Autres
**Technologies avancées** Autres
**Multilinguisme de mise en œuvre**** La fourniture de solutions Java, Python et C++ met en valeur la polyvalence. Autres
**Clean code & mod arithmétique**= Pas de nombres magiques, d'espace à temps constant et de manipulations modulaires robustes. Autres

---

Liste de contrôle pour le démarrage rapide de l'entrevue

1. ** Expliquez l'indépendance des deux côtés** – donne à l'intervieweur un aperçu de vos compétences en matière de décomposition des problèmes.
2. **Dériver la récurrence de Fibonacci d'un côté** – assurez-vous de pouvoir expliquer pourquoi `f[n] = f[n-1] + f[n-2]`.
3. **Afficher la formule finale** – réponse = `f[n]^2 mod MOD`.
4. **Écrire le DP** itératif – 5-10 lignes de code, O(n), mémoire O(1).
5. **Optionnel**: mention/mise en œuvre de la Fibonacci à double effet pour "O(log n)" pour impressionner sur la profondeur.
6. **Cas de bord d'essai** – `n = 1`, `n = 2`, `n = 104` et un test de santé pour `n = 0` (si le harnais d'essai le permet).
7. **Parler à travers la complexité** – confirmer qu'il satisfait les contraintes.

---

- Oui. Pensée finale : du code à la carrière

> **LeetCode 2320** est un exemple d'un manuel de réflexion en termes de sous-problèmes indépendants.
> Le même motif apparaît dans **Hotel Booking, House Robber et Matrix Chain Multiplication**.
> En maîtrisant ce problème dans **Java, Python et C++**, vous êtes équipé pour :
> - Passez le cycle de conception d'algorithme typique dans toute entrevue avec une entreprise technologique.
> - Expliquez comment mettre à l'échelle un PDD `O(n)` à `O(log n)` avec un doublement rapide – un point de discussion pour les rôles supérieurs.
> - Montrez que vous pouvez écrire un code propre, prêt à la production, qui gère sans faille l'arithmétique grand mode.

Gardez cette solution dans votre *algorithme triche-sheet* et vous serez prêt à clouer la prochaine entrevue de codage. Bon codage ! Les

---

**Mots clés**: *entretien d'ingénierie de logiciels, conception d'algorithmes, programmation dynamique, Fibonacci, LeetCode 2320, entretien de codage Java, entretien Python, interview C++, doublement rapide, algorithmes O(log n), maisons sans lien, préparation d'entrevue*.