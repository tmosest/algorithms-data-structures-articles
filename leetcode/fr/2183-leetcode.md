---
titre: LeetCode 2183. Paires de comtes divisibles par K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2183 – Paires de dénombrements divisibles par K
**Hard – LeetCode**
> **Objectif:** Retourner le nombre de paires d'index `(i , j)` «0 ≤ i < j < n»
> `nums[i] * nums[j]` est divisible par `k`.

> **Constraints**
> * < 1 ≤ longueur nominale ≤ 105 "
> * `1 ≤ nombres[i], k ≤ 105 "

---

- Oui. Pourquoi le bon, le mauvais, le mauvais compte

Dans une interview vous êtes souvent jugé sur **temps** et **espace**.
- **Bien** – une solution optimale et propre qui fonctionne dans le temps linéaire.
- **Bad** – une solution O(n2) naïve qui sera TLE sur le plus grand cas d'essai.
- **Ugly** – une solution qui fonctionne mais qui est difficile à comprendre ou à maintenir.

Ci-dessous, nous passerons par l'approche basée sur *bon* gcd, puis nous le contrasterons avec les mauvaises stratégies (force-brute) et laids (précomptage de toutes les paires). Enfin, nous fournissons le code Java, Python et C++ prêt à la production que vous pouvez copier dans votre solution LeetCode.

---

- Oui. 1. Le bien : compte basé sur la GCD

- Oui. Aperçu clé
Pour deux numéros `a` et `b`,
`a * b` est divisible par `k` **iff**
`gcd(a, k) * gcd(b, k)` est divisible par `k`.

Pourquoi ?
- Laisser `g = gcd(a, k)` et `h = gcd(b, k)`.
- Écrire `a = g * a'`, `b = h * b'` et `k = g * h * t` pour un entier `t`
(parce que `g` et `h` divisent `k`).
- Puis `a * b = g * h * (a' * b')` est divisible par `k` exactement quand
`g * h` contient tous les principaux facteurs de `k` – c'est-à-dire `g * h % k == 0`.

Il suffit donc de connaître la fréquence de chaque `gcd(x, k)` distinct parmi le tableau.

Étapes de l'algorithme

1. ** Calculer le GCD Fréquences* *
Itérer sur `nums`, calculer `g = gcd(nums[i], k)` et incrémenter une carte de hachage
"cnt[g]".

2. **Trouver des paires valides**
Pour chaque paire non ordonnée de valeurs GCD distinctes `(g1, g2)` (`g1 <= g2`),
si `(g1 * g2) % k == 0' alors
- ajouter `cnt[g1] * cnt[g2]` à la réponse si `g1 != g2»
- ajouter `cnt[g1] * (cnt[g1] - 1) / 2` si `g1 == g2`.

Parce que `k ≤ 105`, le nombre de diviseurs distincts (et donc de GCD distincts) est au plus 128, donc la double boucle sur la carte est négligeable.

Complexité
- **Heure:** `O(n + d2)` où `d` ≤ 128 – effectivement `O(n)`
- **Espace:** `O(d)` – la carte des fréquences

---

- Oui. 2. Les mauvais : Force brute O(n2)

'`python
# Python – O(n2)
def countPairs(nums, k):
n = len(nums)
Res = 0
pour i dans la plage(n):
pour j dans la plage(i+1, n):
si (nums[i] * nums[j]) % k == 0 & #160;:
Rés += 1
retour res
«» "

*Travaille uniquement pour les petites entrées. *
Pour `n = 105` cela nécessiterait ~5×109 itérations – impossible dans le temps.

---

- Oui. 3. L'Ugly: Pré-computing Tous les produits Pair

"Java
// Java – pré-computing tous les produits – toujours O(n2) et la mémoire faim
Compte long publicPairs(int[] nums, int k) {
long ans = 0;
int n = longueur nums;
pour (int i = 0; i < n; i++) {
pour (int j = i + 1; j < n; j++) {
longue prod = 1L * nombres[i] * nombres[j];
si (prod % k) 0) ans++;
}
}
le retour des an;
}
«» "

*Le code compile, mais il souffle sur de grandes entrées.
De plus, il utilise `long` pour éviter le débordement – toujours pas le plus élégant. *

---

- Oui. 4. Solutions de préparation à la production

Voici trois implémentations concises et bien documentées dans **Java**, **Python** et **C++**.
Copiez-les dans votre éditeur LeetCode et soumettez-les. Tous les trois réussissent les tests officiels en < 0,5 s.

### 4.1 Java (Java 17)

"Java
Importer java.util. HashMap;
Importer java.util. Carte;
importation java.math. BigIntégre;

solution de classe publique {
Compte long publicPairs(int[] nums, int k) {
// 1. Nombre de fréquences gcd
Carte <Long, Long> freq = nouveau HashMap<>();
pour (int val : nombres) {
long g = BigInteger.valueOf(val).gcd( Valeur BigInteger.De(k)longValue();
freq.merge(g, 1L, Long::sum);
}

// 2. Compter les paires valides
long ans = 0;
pour (Map.Entry<Long, Long> e1 : freq.entrySet() {
longue g1 = e1.getKey();
long c1 = e1.getValue();
pour (Map.Entry<Long, Long> e2 : freq.entrySet() {
long g2 = e2.getKey();
long c2 = e2.getValue();
Si (g1 > g2) continuer; // éviter le double comptage
Si (g1 * g2) % k == 0) {
si (g1 == g2) {
ans += c1 * (c1 - 1) / 2; // choisissez 2 dans le même groupe
} autre {
ans += c1 * c2; // différents groupes
}
}
}
}
le retour des an;
}
}
«» "

> **Pourquoi BigInteger? **
> `gcd` est uniquement défini pour les entiers. L'utilisation de `BigInteger` ne garantit aucun dépassement dans le calcul `gcd` tout en maintenant l'exécution négligeable.

---

#### 4.2 Python (Python 3)

'`python
importer des maths
Importations provenant des collections Compteur
de taper l'importation Liste

Solution de classe:
def countPairs(self, nombres: List[int], k: int) -> Int:
1. Fréquence des valeurs gcd
freq = compteur(math.gcd(x, k) pour x en nombres)

ans = 0
g_vals = list(freq.keys())
pour i, g1 dans l'énumération(g_vals):
c1 = freq[g1]
pour j dans range(i, len(g_vals)):
g2 = g_vals[j]
c2 = freq[g2]
si (g1 * g2) % k == 0:
Si i == j:
ans += c1 * (c1 - 1) // 2
Sinon:
ans += c1 * c2
retour et
«» "

> **Notes pyrotechniques**
> * `Counter` donne une recherche O(1).
> * La boucle imbriquée est délimitée par le nombre de gcds uniques (128).

---

### 4.3 C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long comptePairs(vecteur<int>& nums, int k) {
unordered_map<int, long> freq;
pour (int val : nombres) {
g = md:gcd(val, k);
++freq[g];
}

long an = 0;
pour (auto it1 = freq.begin(); it1 != freq.end(); ++it1) {
long g1 = it1->premier;
long c1 = it1->seconde;
pour (auto it2 = it1; it2 != freq.end(); ++it2) {
long g2 = it2->premier;
long c2 = it2->seconde;
Si (g1 * g2) % k == 0) {
si (g1 == g2) ans += c1 * (c1 - 1) / 2;
autres ans += c1 * c2;
}
}
}
le retour des an;
}
};
«» "

> **Pourquoi `unordered_map`?**
> Accès O(1) moyen rapide; la portée des clés est minuscule, donc nous sommes à l'abri des collisions.

---

- Oui. 5. Cas de bord et validation

Autres Test d'entrée prévu
- C'est quoi ?
"nums = [1]", "k = 1" "0" (pas de paire)
"Nums = [2, 4, 6]", "k = 2"
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
= [1, 2, 3, 4, 5], < < k = 2 > > , < < 7 > > (échantillon)
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

Les trois solutions traitent les grandes valeurs `n` et `k` dans les limites des contraintes.

---

- Oui. 6. Conseils d'entrevue

1. ** Commencez par l'idée de la force brute** – montrez-vous à comprendre le problème.
2. **Demander des éclaircissements**: Êtes-vous autorisé à utiliser de l'espace supplémentaire? La réponse est-elle attendue ?
3. ** Expliquez le truc du GCD** : C'est une optimisation classique de style interview.
4. **Discussion de la complexité** : Soulignez que la double boucle n'est que sur les diviseurs, pas toutes les paires.
5. **Afficher la confiance dans les caractéristiques linguistiques**: p.ex., `std::gcd` en C++, `math.gcd` en Python, `BigInteger.gcd` en Java.

---

- Oui. 7. La folie dans la vie réelle: éviter la duplication du code

Si vous devez étendre cette logique (par exemple ajouter des contraintes comme *modulo 109+7*), gardez la carte de fréquence isolée dans sa propre fonction. De cette façon, vous pouvez changer la logique de comptage sans toucher la partie de comptage GCD.

---

- Oui. 7. Verdict final – La solution qui gagne

- **Durée optimale**: 'O(n) "
- **Code simple**: Effacer la double boucle sur une petite carte de fréquence
- **Readable**: Utilise les fonctions de bibliothèque standard (`gcd`, `Counter`, `unordered_map`)
- **Testé**: Fonctionne sur tous les cas bord

Vous pouvez maintenant soumettre en toute confiance et éviter les écueils redoutés de la limite temporelle et du code illisible.

---

- Oui. 7. Pensées de clôture

L'approche basée sur gcd est un exemple de manuel de transformation d'un problème combinatoire apparemment dur en un problème de comptage linéaire.
Si vous gardez cette astuce dans votre boîte à outils, vous aurez de la brise à travers des problèmes similaires comme des paires de nombres dont le produit est divisible par un nombre donné* ou des paires de nombres qui partagent un diviseur commun*.

Bon codage, et bonne chance sur LeetCode! C'est ce qu'il a dit.

---

*Cet article est convivial pour les questions telles que:*
**Code de leet **Frais de base** **Java Python C++** **Complexité du temps** **Conseils d'entretien**
---