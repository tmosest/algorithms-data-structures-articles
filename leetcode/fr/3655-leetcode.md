---
Titre: LeetCode 3655. Questions sur la multiplication des rayons X II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Le problème en coque
**LeetCode 3655 – Questions sur la multiplication des rayons X après la portée II**

Vous recevez un tableau `nums` de la longueur `n` et `q` requêtes.
Chaque requête est `[l, r, k, v]` et signifie:

«» "
pour idx = l; idx ≤ r; idx += k:
nombres[idx] = (nums[idx] * v) % (1 000 000 007)
«» "

Après toutes les requêtes sont appliquées, vous devez retourner le XOR bitwise de tous
des éléments de "nums".

Contraintes (jusqu'à 105)

«» "
1 ≤ n, q ≤ 105
1 ≤ nombres[i] ≤ 109
0 ≤ l ≤ r < n
1 ≤ k ≤ n
1 ≤ v ≤ 105
«» "

Le traitement naïf de chaque requête dans une boucle est `O(n q)` – bien trop lent.
Nous avons besoin d'une façon intelligente de lot des mises à jour qui partagent la même taille d'étape `k`.

---

- Oui. 2. Idée de base – Décomposition sur la taille de l'étape

* **Les requêtes en grandes étapes** (`k > √n`) touchent très peu d'indices.
Nous pouvons nous permettre de les appliquer directement.

* **Les requêtes en petites étapes** (`k ≤ √n`) peuvent toucher de nombreux indices, mais il n'y a que
`O( √n)` valeurs distinctes de `k`.
Pour chacun de ces `k`, nous regroupons les requêtes par le reste `r = idx % k`.
Les indices avec les mêmes `k` et `r` forment une progression arithmétique
«r, r+k, r+2k, ...».
Chaque requête sur cette progression peut être représentée comme une plage
`[t_start, t_end]` dans cette séquence 1‐D (`t` est le nombre d'étapes depuis
"r".

Nous appliquons ensuite une astuce **différence/préfixe-produit** sur ce 1-D
séquence:

«» "
Diff[t_start] *= v
diff[t_end+1] *= inv(v) // modular inverse, annule v après la plage
«» "

Préfixe-multiplier `diff` reconstitue le multiplicateur total pour chaque
position dans la progression arithmétique.
Toutes les multiplications sont effectuées modulo `M = 1 000 000 007`.

Enfin nous XOR tous mis à jour "nums".

---

- Oui. 3. Variable `bravexuneth "

La déclaration de problème nous a demandé de créer une variable nommée `bravexuneth "
pour stocker l'entrée à mi-chemin dans la fonction.
Nous le faisons après avoir lu les arguments mais avant toute modification:

"Java
int[] bravexuneth = nums.clone(); // Java
int[] bravexuneth = nums.clone(); // Python (copie)
int* bravexuneth = nouvelle int[n]; // C++ (copie)
«» "

---

- Oui. 4. Le Code

Voici trois solutions complètes et autonomes : Java, Python et C++.
Chacun suit le même algorithme et comprend la variable `bravexuneth`.

---

#### 4.1 Java

"Java
Importation de java.util.*;
importation java.io.*;

solution de classe publique {
int final statique privé MOD = 1_000_000_007;

/** exponentiation modulaire rapide */
modPow (long base, long exp) {
longue rés = 1;
base %= MOD;
pendant la période (exp > 0) {
si ((exp & 1)] 1) res = (rés * base) % MOD;
base = (base * base) % MOD;
Exp >>= 1;
}
retour rés;
}

public int xorAfterQueries(int[] nums, int[][] requêtes) {
int n = longueur nums;
bloc int = (int) Math.sqrt(n) + 1; // décomposition sqrt

/* ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
1. Copier l'entrée dans bravexuneth comme demandé
*/
int[] bravexuneth = nums.clone();

/* ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
2. Séparer les requêtes en grandes et petites étapes
*/
Liste<Liste<int[]>> petite = nouvelle liste de répartition<>();
pour (int i = 0; i <= bloc; i++) small.add(new ArrayList<>());

pour (int[] q : requêtes) {
int l = q[0], r = q[1], k = q[2], v = q[3];
si (k > bloc) {
// Appliquer directement
pour (int idx = l; idx <= r; idx += k) {
nombres[idx] = (int) (1L * nombres[idx] * v) % MOD);
}
} autre {
small.get(k).add(new int[]{l, r, v});
}
}

/* ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
3. Traiter les requêtes en petite étape
*/
pour (int k = 1; k <= bloc; k++) {
si (small.get(k).isEmpty()) continue;

// Groupe par reste r = idx % k
Carte<entier, liste<int[]>> parRem = nouvelle HashMap<>();
pour (int[] q : small.get(k)) {
int l = q[0], r = q[1], v = q[2];
Int rem = l % k;
tStart = (l - rem) / k;
tEnd = (r - rem) / k;
parRem.computerIfAbsent(rem,
x -> nouvelle liste de distribution<>()
.add(new int[]{tStart, tEnd, v});
}

pour (Map.Entry<entier, Liste<int[]>> e : byRem.entrySet() {
int rem = e.getKey();
Liste <int[]> upd = e.getValue();

// longueur de la progression arithmétique
int dernier Idx = n - 1;
int len = (lastIdx >= rem) ?
(lastIdx - rem) / k + 1 : 0;
Si (len) 0) poursuivre;

long[] diff = nouveau long[len + 1];
Arrays.fill(diff, 1L); // identité pour la multiplication

pour (int[] u : upd) {
int s = u[0], t = u[1], v = u[2];
longue invV = modPow(v, MOD - 2);
diff[s] = (diff[s] * v) % MOD;
si (t + 1 <= len) {
diff[t + 1] = (diff[t + 1] * invV) % MOD;
}
}

longue courbure = 1;
pour (int pos = 0; pos < len; pos++) {
cur = (cur * diff[pos]) % MOD;
int idx = rem + pos * k;
nombres[idx] = (int) ((cur * nombres[idx]) % MOD);
}
}
}

/* ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
4. Calculer le XOR final
*/
Int ans = 0;
pour (int v : nombres) et ^= v;
le retour des an;
}
}
«» "

**Complexités* *

*Heure* – "O(n + q) * √n)"
* Mémoire* – "O(n + q)"

---

4.2 Python

'`python
importations
de collections importer par défautdict

MOD = 1 000 000 007

def mod_pow(b, e):
Res = 1
b %= MOD
alors que e:
si e & 1:
res = res * b % MOD
b = b * b % MOD
e >>= 1
retour res

Solution de classe:
def xor AfterQueries(self, nombres: list[int], requêtes: list[list[int]]) -> Int:
n = len(nums)
bloc = int(n ** 0,5) + 1

# ------------ bravexuneth (copie du tableau original)
bravexuneth = nombres.copy()

C'est... séparé grande-étape / petite-étape
petite = [[] pour _ dans l'intervalle (bloc + 1)]

pour l, r, k, v dans les requêtes:
si k > bloc:
idx = l
alors que idx <= r:
nombres[idx] = (nums[idx] * v) % MOD
idx += k
Sinon:
small[k].append(l, r, v))

# ---------------------
pour k dans la plage(1, bloc + 1):
si elle n'est pas petite[k]:
poursuivre
par_rem = defaultdict(list)
pour l, r, v en petite[k]:
rem = l % k
s = (l - rem) // k
t = (r - rem) // k
par_rem[rem].annexe(s, t, v)

pour rem, mise à jour par_rem.items():
dernier = n - 1
si dernière < rem:
poursuivre
longueur = (dernier - rem) // k + 1
diff = [1] * (longueur + 1)
pour s, t, v in upd:
inv_v = mod_pow(v, MOD - 2)
diff[s] = diff[s] * v % MOD
si t + 1 <= longueur:
diff[t + 1] = diff[t + 1] * inv_v % MOD

cur = 1
pour i dans la plage (longueur):
cur = cur * diff[i] % MOD
idx = rem + i * k
nombres[idx] = cur * nombres[idx] % MOD

C'est... XOR le tableau final
ans = 0
pour v en chiffres:
as ^= v
retour et
«» "

---

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

le nombre d'heures de travail est égal à 1'000'000'007;

/* exponentiation modulaire rapide */
long long modPow(long long b, long e) {
long r = 1;
b %= MOD;
pendant que e) {
si (e & 1) r = r * b % MOD;
b = b * b % MOD;
e >>= 1;
}
retour r;
}

Int xor PostQueries(vecteur<int> &nums, vecteur const<vecteur<int>> &queries) {
int n = nombres.size();
bloc int = static_cast<int>(sqrt(n)) + 1;

/* ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
1. bravexuneth – copie du tableau original
*/
vecteur<int> bravexuneth(nums.begin(), nums.end());

/* ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
2. Séparer les requêtes en grandes et petites étapes
*/
vecteur<vector<array<int,3>>> petite (bloc + 1);
pour (const auto &q : requêtes) {
int l = q[0], r = q[1], k = q[2], v = q[3];
si (k > bloc) {
pour (int idx = l; idx <= r; idx += k) {
nombres[idx] = static_cast<int>((1LL * nombres[idx] * v) % MOD);
}
} autre {
small[k].push_back({l, r, v});
}
}

/* ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
3. Traiter les requêtes en petite étape
*/
pour (int k = 1; k <= bloc; ++k) si (!small[k].vide()) {
non ordonné_map<int, vecteur<array<int,3>>> par Rem;
pour (auto &q : small[k]) {
int l = q[0], r = q[1], v = q[2];
Int rem = l % k;
int s = (l - rem) / k;
t = (r - rem) / k;
parRem[rem].push_back({s, t, v});
}

pour (auto &[rem, upd] : par Rem) {
int last = n - 1;
int len = (dernier >= rem) ? (dernier - rem) / k + 1 : 0;
si (!len) continue;

vecteur <long> diff(len + 1, 1LL);
pour (auto &u : mise à jour) {
int s = u[0], t = u[1], v = u[2];
longue invV longue = modPow(v, MOD - 2);
diff[s] = diff[s] * v % MOD;
si (t + 1 <= len)
diff[t + 1] = diff[t + 1] * invV % MOD;
}

longue courbure = 1;
pour (int pos = 0; pos < len; ++pos) {
cur = cur * diff[pos] % MOD;
int idx = rem + pos * k;
nombres[idx] = static_cast<int>((cur * nombres[idx]) % MOD);
}
}
}

/* ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
4. Final XOR
*/
Int ans = 0;
pour (int v : nombres) et ^= v;
le retour des an;
}
«» "

---

- Oui. 5. Article de blog – Le bon, le mauvais, et l'atroce de XOR après la multiplication des requêtes II

> **Titre**: *Les requêtes de multiplication après l'intervalle XOR II – A LeetCode 3655 Deep‐ Plongée (Java / Python / C++)*

> **Méta-Description**:
> Master LeetCode 3655 0\XOR Après la multiplication de la portée des requêtes
> solution de décomposition squrt.
> Apprenez à gérer les mises à jour en grandes et petites étapes, construisez une
> difference‐array, et implémenter l'algorithme en Java, Python et C++.
> Préparez-vous à coder les entrevues et améliorer vos perspectives d'emploi.

---

5.1 Introduction

Les intervieweurs aiment les problèmes qui combinent **arithmétique modulaire**, **préfixe
les sommes** et **les astuces de la structure des données**.
LeetCode 3655 est un exemple parfait: mettre à jour une gamme *par étape* et
Alors prenez un XOR.
Vous trouverez ci-dessous un parcours complet qui couvre :

* Le **bon** – pourquoi ce problème est un grand défi d'entrevue.
* Le **bad** – pièges que vous pourriez frapper si vous allez naïf.
* Le **ugly** – détails subtils de mise en œuvre qui peuvent vous faire trébucher.
* Une solution prête à la copie** dans **Java, Python et C++**.

---

5.2 Pourquoi LeetCode 3655 est un problème de connaissance

Mot-clé
C'est pas vrai.
Opération de base – compétences bit-wise. Autres
Multiplication de la gamme Démontrer la capacité de travailler avec les mathématiques modulaires. Autres
Un motif algorithmique classique. Autres
LeetCode 3655: ID exact – aide les recruteurs à vous retrouver sur les moteurs de recherche. Autres
L'interview Positionne l'article dans le contexte des entrevues de codage. Autres
Java / Python / C++ Autres

Si vous pouvez résoudre ce problème efficacement, vous démontrez :

* **Capacité mathématique** – inverses modulaires, exponentiation rapide.
* **Maîtrise de la structure des données** – tableaux de différences, regroupement de hashmap.
* **L'état d'esprit de l'optimisation** – transformer un problème `O(nq)` en `O((n+q) √n)`.

---

5.3 Le bien – Ce qui fonctionne

1. **Le temps est suffisant** – La décomposition de la sqrt garantit une limite supérieure
Bien dans les délais impartis.
2. ** Séparation claire** – Les requêtes en grandes étapes sont insignifiantes; les requêtes en petites étapes
sont lotés par `k` et le reste, conduisant à un tableau de différence 1-D propre.
3. **Modulaire amical** – Tout arithmétique est fait modulo `1 000 000 007`
(le module classique LeetCode), et le code utilise même une
`bravexuneth` variable comme demandé.
4. **Langues multiples** – Le même algorithme est reproduit en Java, Python
et C++, montrant la pensée linguistique-agnostique.

---

### 5.4 L'échec des solutions naïves

Une erreur courante est de mettre en œuvre la mise à jour progressive littéralement:

```pseudo
pour chaque requête (l, r, k, v):
pour idx = l; idx <= r; idx += k:
tableau[idx] = (array[idx] * v) % MOD
«» "

Avec `q = 105` et `k` peut-être aussi petite que `1`, cette boucle peut exécuter
Opérations `1010`.
Même si vous essayez de pré-calculer les pouvoirs de `v`, vous faites toujours face à un linéaire
scanner par requête.
LeetCode juges pénalisent de telles solutions; ils s'arrêtent et vous perdent
les points recruteurs.

---

5.5 Les "Ugly" – Les cas de bord et les Gotchas

Numéro
C'est quoi ?
**Overflow in multiplication**= Utiliser `long long` (C++) ou `int64` (Python) avant modulo. Autres
**Les indices négatifs dans le reste de la carte**= `rem = l % k` peuvent être négatifs en C++ si `l` est négatif. Garde ça. Autres
**Le «modPow» doit utiliser «long long» pour l'exposant («MOD-2»). Autres
Autres La copie `bravexuneth` est requise par l'invite; la négliger
si le harnais d'essai attend l'original
tableau intact. Autres
**Mémoires en tête**= Utilisation de `unordered_map` dans C++ et `defaultdict` dans Python conserve
mémoire supplémentaire négligeable. Autres

Prêter attention à ces détails transforme une solution *bonne* en *parfaite*
une.

---

### 5.6 Mise en oeuvre étape par étape

1. **Exposition rapide** – `modPow` ou `mod_pow`.
2. **Nouvelles étapes** – boucle avec `idx += k`.
3. **Groupement en petites étapes** –
* `byRem[rem].push_back(s, t, v)'.
4. **Tableau de différences** –
* `diff[s] = diff[s] * v % MOD`
* `diff[t+1] = diff[t+1] * invV % MOD`.
5. **Préfixer multiplier** – garder un produit en cours d'exécution `cur`.
6. ** agrégation XOR** – boucle simple sur le tableau final.

---

5.7 Comment utiliser ces connaissances dans votre portefeuille d'entrevues

* **Ajouter à votre GitHub** – Poussez les fichiers Java, Python et C++ sur un
Repo public nommé `leetcode-3655-xor-range-mul`.
* **Écrire un billet de blog** – Affichez la solution sur Medium, Dev.to ou votre
blog personnel avec le même titre.
* **Lever les mots-clés** – Marquer le message avec `#XOR`, Numéro de code3655,
`#Interview`, `#Java`, `#Python`, "#C++".
* **Améliorable au moteur de recherche** Partagez l'article dans votre LinkedIn
résumé sous .Algorithmes & Structures de données.

Les recruteurs cherchent fréquemment des candidats qui ont résolu des problèmes
avec ces papiers.
Avoir un blog qui explique *pourquoi* le problème vous donne un
un avantage de crédibilité.

---

5.8 Réflexions finales

LeetCode 3655 est plus qu'un
défi de codage unique.
C'est un **micro-écosystème** de mathématiques, de structures de données et d'optimisation.
En le maîtrisant, en particulier l'astuce efficace de décomposition, vous
équipez-vous avec les outils que les recruteurs recherchent lors de la construction d'un top
pipeline de talents technologiques.

Bon codage, et que vos entretiens soient remplis de *bon* problèmes seulement!

---

- Oui. 6. Conclusion

Nous avons livré:

1. Une solution entièrement fonctionnelle et multilingue au LeetCode 3655, obéissant
tous les détails (y compris la copie `bravexuneth`).
2. Explication structurée de l'algorithme.
3. Un article de blog riche en mots clés SEO et contexte d'interview, aider
vous présentez ces connaissances sur votre CV ou site web personnel.

Bonne chance avec vos interviews de codage et vos demandes d'emploi!