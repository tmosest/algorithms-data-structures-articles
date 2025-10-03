---
titre: LeetCode 2031. Compter Subarrays avec plus que zéros -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Idée**

Pour une sous-tribution `A[l ... r]` laisser

«» "
S(i) = (#ones – #zeros) dans A[0 ... i]
«» "

`S(i)` est une somme préfixe qui peut être **+1** (pour un `1`) ou **–1** (pour un `0`).

La sous-tribution «A[l ... r]» contient plus de `1`s que `0`s iff

«» "
S(r) – S(l‐1) ≥ 1
«» "

donc

«» "
S(l‐1) ≤ S(r) – 1
«» "

Pour un `r` fixe, nous n'avons besoin que de savoir combien de sommes préfixées
sont les suivants:
Au lieu d'effectuer une requête de gamme, nous pouvons garder un compteur de
combien de sous-cours qui se terminent à `r` satisfont à la condition.
Lorsque nous passons de `r-1` à `r`, le compteur peut être mis à jour en **O(1)**.

-----------------------------------------------------------------------------------

#### Algorithme monopass O(n)

«» "
somme – somme préfixe actuelle (one – zéros)
cnt – nombre de sous-groupes admissibles qui se terminent à l'indice actuel
ans – nombre total de sous-cours admissibles
freq – hash map: prefix sum → combien de fois il est apparu
«» "

«» "
freq[0] = 1 // préfixe vide
somme = 0
cnt = 0
ans = 0

pour chaque élément x en nombres
Si x == 1
cnt += freq[sum] // les sous-tribus qui se terminent ici
Montant 1
Sinon // x == 0
Montant 1
cnt -= freq[sum] // les sous-tribus qui se terminent ici
ans = (ans + cnt) mod MOD
freq[sum] += 1
«» "

*Pourquoi ça marche ? *

* Quand `x == 1` nous ajoutons une `+1` à la somme préfixe.
Chaque préfixe précédent sum `p` qui est **égal** au courant
`sum` crée une sous-tribution `A[l ... r]` avec
`S(r) – S(l‐1) = 1`, c'est-à-dire plus `1`s que `0`s.
Le nombre de ces préfixes est `freq[sum]`.
Après la mise à jour de `sum` nous incluons également la nouvelle sous-tribution qui
commence à l'index `0`.

* Quand `x == 0` nous ajoutons un `–1`.
Chaque somme préfixe précédente qui est **exactement** égale au *nouveau*
`sum` ferait la différence `0` (nombre égal de `1`s et `0`s),
qui ** ne satisfait pas à cette exigence.
Par conséquent, nous soustraitons `freq[sum]` de `cnt`.

La variable courante `cnt` contient toujours le nombre de qualificatifs
les sous-réseaux qui se terminent à la position actuelle, donc l'ajouter à «ans "
indique le nombre total.

-----------------------------------------------------------------------------------

Preuve d'exactitude

Nous prouvons que l'algorithme renvoie le nombre exact de sous-réseaux
contenant plus de `1`s que `0`s.

---

Lemma 1
Après traitement des premiers éléments «i» («0 ≤ i < n»),
"freq[p]" est égal au nombre d'indices `j` (`-1 ≤ j < i`) de telle sorte que
«S(j) = p».

**Prof.**

*Initialisation ('i = 0'). *
Avant le début de la boucle, nous définissons `freq[0] = 1`.
Seul le préfixe vide `S(-1)=0` existe, de sorte que l'instruction se tient.

*Étape d'initiation. *
Supposons que le lemma tient après l'élément `i-1`.
Pendant le traitement de l'élément `i` nous incréments
`freq[sum]` par un, où `sum = S(i)`.
Tous les indices antérieurs sont intacts, donc après la mise à jour
"freq[p]" compte exactement les occurrences du préfixe sum `p`
entre indices `-1 ... i`.



Lemma 2
Pendant l'itération pour l'indice "i" (`0 ≤ i < n`) la variable `cnt`
est égal au nombre de sous-tarifs éligibles qui se terminent à l'indice «i».

**Prof.**

Laissez `s_avant` être la valeur de `sum` avant la mise à jour du courant
élément et `s_after` sa valeur par la suite.

*Case 1 – `x == 1`.*

`S(i) = s_after`.
Chaque sous-tribu qui se termine à `i` et commence à `l` «0 ≤ l ≤ i»
a une différence

«» "
S(i) – S(l‐1) = s_après – S(l‐1)
«» "

Il est ≥ 1 **iff** `S(l‐1) = s_avant "
(parce que `s_avant = s_après – 1`).
`freq[s_avant]` compte exactement tous ces indices «l‐1».
Par conséquent, `cnt` devient le nombre correct.

*Case 2 – `x == 0`. *

`S(i) = s_after`.
Un sous-appel se terminant à « i » aurait la différence « 0 » si et seulement si
`S(l‐1) = s_after`.
Tous ces sous-tarifs doivent **pas** être comptés.
`freq[s_après]` On les compte, donc on soustrait cette quantité de
"cnt".
Après la soustraction, `cnt` est exactement le nombre de sous-tarifs
se terminant à "i" qui satisfont à la prescription.

Ainsi, dans les deux cas `cnt` est mis à jour à la valeur correcte. *



Lemma 2
À chaque étape, l'algorithme ajoute à `ans` exactement le nombre de
les sous-groupes admissibles qui se terminent à l'indice actuel.

**Prof.**

Directement à partir de Lemma 2, `cnt` est ce nombre,
et l'algorithme effectue
`ans ← ans + cnt (mod MOD)`. *



C'est vrai. Théorème
`ans` retournés par l'algorithme est égal au nombre de sous-groupes
`nums` qui contiennent strictement plus `1`s que `0`s (modulo `MOD`).

**Prof.**

Par Lemma 2, pendant toute la traversée chaque qualification
la sous-tribu est ajoutée à «ans» exactement une fois – à savoir quand son droit
le paramètre est traité.
Aucune autre sous-entente n'est ajoutée, car `cnt` ne compte que ceux qui
satisfaire à l'état (par la construction des mises à jour).

Ainsi, après la dernière itération `ans` contient le nombre total de
Sous-cours de qualification.



-----------------------------------------------------------------------------------

Analyse de complexité

Étape Temps Mémoire
C'est pas vrai.
"O(n)" "O(n)" (carte hash de la plupart des "n+1" différentes sommes préfixées)
Toutes les autres opérations Autres

Donc la complexité temporelle globale est **O(n)** et l'espace auxiliaire
est **O(n)** (carte hash).

-----------------------------------------------------------------------------------

Référence mise en œuvre (Java)

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
finale statique privée longue MOD = 1_000_000_007L;

public long numSubarrayOùPlusOnesThanZeros(int[] nums) {
long ans = 0; // réponse finale
longue cnt = 0; // sous-ensembles admissibles se terminant à i
somme int = 0; // somme préfixe (#ones – #zeros)

Carte <entier, long> freq = nouveau HashMap<>();
freq.put(0, 1L); // préfixe vide

pour (int x : nombres) {
Si (x) 1) {
// sous-cours qui se terminent ici et satisfont à la condition
cnt = (cnt + freq.getOrDefault(sum, 0L)) % MOD;
Montant 1;
} autres { // x == 0
somme = 1;
// soustraire les sous-tarifs qui rendraient les comptes égaux
cnt = (cnt - freq.getOrDéfaut(sum, 0L) + MOD) % MOD;
}
as = (ans + cnt) % MOD;
freq.put(sum, freq.getOrDefault(sum, 0L) + 1);
}
le retour des an;
}

// ---- Pour les essais rapides ----
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.numSubarrayOùPlusOnesThanZeros(
nouvelle int[]{0,1,1,0}); // 5
Système.out.println(s.numSubarrayOùPlusOnesThanZeros(
nouvelle int[]{0,1,0,0,0,1,0,1}); // 18
}
}
«» "

-----------------------------------------------------------------------------------

#### Mise en oeuvre de la référence (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
longue MOD statique = 1'000'000'007LL;
long long numSubarrayOùPlusOnesThanZeros(vecteur<int>& nums) {
unordered_map<int, long> freq;
freq[0] = 1; // préfixe vide
somme longue = 0; // somme préfixe (#ones – #zeros)
long long cnt = 0; // sous-arrays se terminant à idx courant
long an = 0;
pour (int x : nombres) {
Si (x) 1) {
cnt = (cnt + freq[sum]) % MOD; // sous-réseaux qui se terminent ici
+ somme;
} autres { // x == 0
--somme;
cnt = (cnt - freq[sum] + MOD) % MOD; // soustraire les mauvais
}
as = (ans + cnt) % MOD;
++freq[sum];
}
le retour des an;
}
};
«» "

-----------------------------------------------------------------------------------

La même logique peut être écrite dans n'importe quelle autre langue (Python, Go, Rust,
etc.) – la clé est la technique du préfixe monopass + plan de hachage.