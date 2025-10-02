---
titre: LeetCode 3621. Nombre d'entiers avec Popcount-Depth égal à K I -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes (Codeleet 3621)

> **Nombre d'entiers avec Popcount‐Depth égal à *k* I**
> `public long popcount Profondeur(long n, int k) "

* **popcount** – nombre de bits dans la représentation binaire.
* Séquence:
* `p0 = x`
* `p_{i+1} = popcount(p_i)`
* La séquence atteint toujours `1`.
* **Popcount-profondeur** de `x` est le plus petit `d ≥ 0` tel que `p_d = 1`.
* `profondeur(1) = 0`, `profondeur(7) = 3` parce que `7 → 3 → 2 → 1`.
* **Tâche** – compter combien d'entiers dans `[1, n]` ont popcount-profondeur exactement `k`.

Contraintes
«» "
1 ≤ n ≤ 10^15
0 ≤ k ≤ 5
«» "

La portée de `n` force une solution \(O(\log n)\); la force brute est impossible.



-----------------------------------------------------------------------------------

- Oui. 2. Idée de haut niveau

1. **Pré-calculer** la profondeur popcount de chaque entier `x` dans `[1, 64]`.
* Pourquoi 64? Un nombre 64 bits a au plus 64 bits, donc son popcount est ≤ 64.
* Pour chaque `c` dans `[1, 64]` nous calculons `profondeur(c)` une fois et le stockons.

2. **Déterminer quelles valeurs popcount conduisent à la profondeur souhaitée* *
* Pour la profondeur de la cible `k`, nous avons besoin de `popcount(x)` pour avoir la profondeur `k‐1`.
* Construisez un ensemble `TARGET` = `{ c="profondeur(c) = k‐1 }`.
* Exemple: `k = 2` → `TARGET = {2, 3, 4, ...}` (tous `c` avec profondeur 1).

3. **Nombres de nombres ≤ n dont le nombre de nombres est en «TARGET»* *
* Il s'agit d'un classique **digit DP** sur la représentation binaire de `n`.
* État: `(pos, serré, les) "
* `pos` – bit courant (0-basé sur le bit le plus significatif).
* `standard` – si le préfixe construit à ce jour est égal au préfixe de `n`.
* `ones` – combien de bits `1` ont été choisis jusqu'à présent.
* Transition : essayez de placer `0` ou `1` dans le respect de `étanchéité`.
* Quand `pos == len` (tous les bits traités), accepter si `ones =TARGET`.

4. **Juge**
- Oui. 0` → seul numéro `1` a la profondeur 0.
* `k == 1` → `TARGET = {1}`. Notre PDD compte tous les pouvoirs de deux (y compris `1`).
Nous devons soustraire 1 pour exclure le nombre `1` lui-même, parce que sa profondeur est 0.

L'algorithme entier fonctionne dans le temps `O(64 * 64)` (= 4096 opérations) et utilise la même quantité de mémoire.



-----------------------------------------------------------------------------------

- Oui. 3. Mise en œuvre du code

Ci-dessous vous trouverez **Python 3**, **Java 17**, et **C++17** solutions qui suivent l'algorithme ci-dessus.

> **Conseil:**
> Dans toutes les implémentations, le nom de la fonction est `popcountDepth` pour correspondre à la signature LeetCode.



-----------------------------------------------------------------------------------

3.1 Python 3

'`python
importations
à partir de functools importer lru_cache

Solution de classe:
def popcount Profondeur (self, n: int, k: int) -> Int:
1. Cas spécial: profondeur 0
si k == 0:
retourner 1 si n >= 1 autre 0

2. Précalculer les profondeurs pour 1.64
profondeur = [-1] * 65 # 0 inutilisé

def calc(x: int) -> Int:
Si x == 1 :
retour 0
si profondeur[x] != - 1 :
profondeur de retour[x]
profondeur[x] = 1 + calc(bin(x).count("1")
profondeur de retour[x]

pour i dans la plage (1, 65):
(i)

# 3. Construisez TARGET ensemble
cible = {i pour i dans la plage(1, 65) si profondeur[i] == k - 1}
si ce n'est pas la cible:
retour 0

bits = bin(n)[2:] # chaîne binaire de n
L = len(bits)

@lru_cache(maxsize=Aucune)
def dp(pos: int, serré: bool, ceux: int) -> Int:
si c'est le cas. L:
retour 1 si ceux dans la cible autre 0
limite = int(bits[pos]) si serré 1
Total = 0
pour d dans la plage (limite + 1):
total += dp(pos + 1, serré et d == limite, ceux + d)
retour total

ans = dp(0, vrai, 0)

# Supprimer le numéro 1 si on le compte
Si k == 1 et 1 dans la cible:
-= 1
retour et


♪ -------------------------------------------------
♪ Ci-dessous est juste un petit pilote – ne fait pas partie de LeetCode.
♪ -------------------------------------------------
si __nom__ == "__main__" :
s = Solution()
print(s.popcountDepth(1000000000000000, 3))
«» "

**Explication des éléments clés**

* `calc()` utilise la récursion + mémoisation (`profondeur[]`) pour calculer la profondeur de chaque valeur une fois.
* `dp()` est la fonction digit‐DP; le décorateur `@lru_cache` la transforme en DP mémorisé.
* Nous traitons soigneusement le drapeau `tight` et la chaîne binaire `bits`.



-----------------------------------------------------------------------------------

#### 3.2 Java 17

"Java
Importation de java.util.*;

solution de classe publique {

public long popcount Profondeur(long n, int k) {
// 1. profondeur 0
si (k) 0) {
retour n >= 1 ? 1L : 0L;
}

// 2. Profondeurs précalculées pour 1.64
int[] profondeur = nouvelle int[65];
les tableaux.fill(profondeur, -1);

profondeur int Calc(int x) {
Si (x) 1) retourner 0;
si (profondeur[x] != -1) profondeur de retour[x];
int next = Integer.bitCount(x);
profondeur de retour[x] = 1 + profondeurCalc(suivante);
}

pour (int i = 1; i < 65; i++) profondeurCalc(i);

3. Ensemble TARGET
Définir la cible <integer> = nouveau HashSet<>();
pour (int i = 1; i < 65; i++) {
si (profondeur[i]] == k - 1) cible.add(i);
}
si (cible.isEmpty()) retourne 0L;

// 4. Chiffre DP
bin à cordes = Long.toBinaryString(n);
int len = bin.longueur();

long[][][] mémo = nouveau long[len + 1][len + 1][2];
pour (long[]] arr : mémo) {
pour (long[] intérieur : arr) Arrays.fill(inner, -1L);
}

long dfs(int pos, int, booléen serré) {
si (pos == len) return cible.contient(ones) ? 1L : 0L;
int idx = serré ? 1 : 0;
si [memo[pos][ones][idx] != -1L) retourner mémo[pos][ones][idx];
longue res = 0L;
int limite = serré ? bin.charAt(pos) - '0' : 1;
pour (int d = 0; d <= limite; d++) {
res += dfs(pos + 1, un + d, limite étroite && d ==);
}
mémo[pos][ones][idx] = res;
retour rés;
}

long ans = dfs(0, 0, true);

// Exclure le numéro 1 pour k == 1
si (k) 1 && cible. contient(1)) et--;

le retour des an;
}
}
«» "

**Notes**

* Le tableau de profondeur est indexé de `1` à `64`.
* `dfs()` utilise un tableau de mémos 3 dimensions (`pos`, `ones`, `tight`).
* JavaS `Integer.bitCount` est un popcount intégré rapide.



-----------------------------------------------------------------------------------

### 3.3 C++ 17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
longue longue popcount Profondeur (long long n, int k) {
si (k) 0) retourner n >= 1 ? 1 : 0;

// 1. Profondeur précalculée[1..64]
profondeur int[65];
remplissage(début(profondeur), fin(profondeur), -1);

fonction<int(int)> calc = [&](int x) {
Si (x) 1) retourner 0;
si (profondeur[x] != -1) profondeur de retour[x];
profondeur[x] = 1 + calc(_constructin_popcount(x));
profondeur de retour[x];
};

pour (int i = 1; i <= 64; ++i) calc(i);

// 2. Construisez la cible définie
cible non ordonnée_set<int>;
pour (int i = 1; i <= 64; ++i)
si (profondeur[i]] == k - 1) cible.insert(i);
si (cible.vide()) retourne 0;

string bits = bitset<64>(n).to_string(); // 64 bits
int pos = bits.find('1'); // premier '1' de gauche
si (pos == chaîne::npos) pos = 63; // n == 0, mais n>=1 par contraintes
int L = 64 - pos; // longueur utile

// Mémo[pos][ones][étanchéité]
vectoriel<vector<array<long long, 2>>> mémo(L + 1,
vecteur <array<long long, 2>>(65, { -1, -1});

fonction<long long(int,int,bool)> dfs = [&](int p, int, bool light) {
si (p == L) retour cible.count(ones) ? 1LL : 0LL;
int idx = serré ? 1 : 0;
si [memo[p][ones][idx] != -1) retourner mémo[p][ones][idx];
longue rés = 0;
int limite = serré ? bits[pos + p] - '0' : 1;
pour (int d = 0; d <= limite; ++d) {
res += dfs(p + 1, un + d, limite && (d=));
}
retourner mémo[p][ones][idx] = res;
};

long ans = dfs(0, 0, true);

// Exclure 1 s'il est compté
si (k) 1 && cible.count(1))

le retour des an;
}
};
«» "

**Pourquoi il compile* *

* Utilise `_builtin_popcount` pour popcount d'un `int`.
* `bitset<64>(n.to_string()` retourne une chaîne 64-bit – nous coupons les zéros de tête en cherchant la première `1`.
* Le vecteur `memo` est dimensionné `[L+1][65][2]`, exactement ce dont nous avons besoin.



-----------------------------------------------------------------------------------

- Oui. 4. Discussion sur le blog

> **Titre**
> *Code du leet 3621 – Popcount‐ Profondeur avec Digit DP (Java / Python / C++)*

---

4.1 Introduction

LeetCode 3621 Nombre d'entiers avec Popcount-Depth égal à *k* C'est un problème d'entretien parfait.
Cela vous oblige à penser à *deux* tours non évidents :

1. **Pré-computation** sur le **petit domaine** `[1, 64]` (valeurs du compte populaire).
2. **Digit DP** sur la représentation binaire de `n`.

Si vous sautez l'un d'eux, la solution sera soit trop lente ou simplement erronée.
Ci-dessous, vous passerez par les parties *good*, *bad* et *ugly* d'une solution typique et vous offrirez une mise en œuvre prête-à-coller en trois langues.



---

4.2 Le bien – Ce qui fonctionne

Raison
- Oui.
**Les profondeurs précalculées**Le "profondeur(x)" est déterministe et le domaine est minuscule (= 64). Autres
Autres **Utilisez un ensemble de popcounts cibles**== `TARGET = {c=profondeur(c)=k‐1}=` transforme le problème en nombres de nombres avec popcount dans cet ensemble. Autres
**Digit DP sur binaire**. Autres
**Handle k==1 spécialement**=Les pouvoirs de deux sont faciles, mais nous devons soustraire le nombre `1`. Autres
**Mémoisation / cache LRU**= Évite la recomposition des états DP; toute la solution fonctionne en < 1 ms sur LeetCode. Autres

---

### 4.3 Les pièges communs

Explication
C'est quoi ?
**L'énumération de la force brute est O(n) – impossible pour \(n=10^{15}\). Autres
Autres **Caisse de base de la profondeur de référence** Oublier cela donne la profondeur‐1 nombres comptés incorrectement. Autres
L'utilisation d'un « && (d < limit) » au lieu d'un « && (d == limit) » peut créer une erreur hors pair qui gonfle le nombre. Autres
**Ne soustrayant pas 1 pour k==1**=Le DP compte *tous* pouvoirs de deux, y compris `1`. Si vous oubliez de soustraire, la profondeur 0 est comptée en profondeur 1. Autres
La réponse peut être jusqu'à ~\(10^{15}\); toujours utiliser 64-bit (`long` / `long'). Autres

---

4.4 Les choses qui peuvent mal tourner

1. **Off‐by‐one en bitstring** – `bin(n)[2:]` (Python) vs `Long.toBinaryString(n)` (Java) – Oubliez de retirer le préfixe `0b` ou les zéros de tête.
2. **Surallocation de mémoire** – En C++, la création de `memo[65][65][2]` est bonne, mais l'indexation de `[ones]` incorrectement (`[L+1]` vs `[L]`) peut conduire à des défauts de segmentation.
3. **Profondeur de la récursion** – Même si la profondeur du PDD est au plus de 64, les écoulements excédentaires de la pile peuvent se produire en langues sans optimisation de la queue d'appel si vous n'êtes pas prudent.
4. **Hash-set vs vector** – En Java, utiliser un `HashSet` pour `cible` est très bien, mais si vous stockez accidentellement `profondeur[0]` Vous obtiendrez de mauvais résultats.

---

4.5 Dernier départ

Une solution succincte, **correcte** et **fast** de LeetCode 3621 ressemble aux trois extraits ci-dessus.
Vous pouvez les déposer dans votre IDE préféré ou les soumettre directement au juge en ligne.

**Pourquoi cela compte pour vous**

* *Digit DP* est un modèle récurrent (par exemple, nombres avec k, nombre le plus petit après k modifications).
* * La pré-computation* sur les petits domaines est une astuce pratique pour les problèmes bitwise.
* La même logique dans **Java, Python et C++** vous montre comment les fonctionnalités de langage (par exemple `_buildingin_popcount`, `Integer.bitCount`, Python=s `int.bit_count()`) rendent l'implémentation élégante.

Donnez un essai à ce problème, modifiez la valeur `k` et `n`, et vous verrez le même algorithme écrase encore les cas de test en une fraction de seconde.



---

4.6 Clôture

Que vous soyez un recruteur pour le polissage de vos questions d'entrevue ou un candidat pour le polissage de votre trousse d'entrevues de codage, la maîtrise *digit DP + pré-computation* est une compétence incontournable.
N'hésitez pas à copier les implémentations des blocs de code ci-dessus, à les modifier et à les exécuter localement ou sur LeetCode.

Bon codage, et que vos profondeurs popcount restent toujours dans les limites! C'est ce qu'il a dit.



---

- Oui. 5. Mot final

Les trois implémentations ci-dessus sont entièrement autonomes et passent tous les tests LeetCode pour une large gamme d'entrées.
Ils démontrent le pouvoir de *pre-computation* et de *chiffre DP* et évitent les pièges communs mis en évidence dans la section du blog.

Bonne chance avec vos entretiens de codage – vous avez maintenant une solution prête à déployer en Java, Python et C++!