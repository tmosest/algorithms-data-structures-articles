---
titre: LeetCode 2741. Permutations spéciales - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Idée de solution**

Pour une permutation valide, il suffit de garantir que
pour chaque paire consécutive `a , b` dans la permutation

«» "
A % b == 0 OU b % a == 0
«» "

La façon la plus facile de générer *toutes* permutations et de ne compter que les
Ceux qui sont valides doivent effectuer une première recherche en profondeur (DFS).
Tout en explorant nous avons besoin d'un moyen rapide de se rappeler quels nombres ont
déjà utilisé – c'est un masque **bit**.

Nous conservons deux éléments d'information pendant le DFS :

Sens de la variable
C'est pas vrai.
Indice "prev" du nombre placé immédiatement avant le courant
"masque" de tous les indices déjà utilisés

Si `prev == -1` nous sommes au tout début, donc n'importe quel nombre peut être le
premier élément.

L'état de la recherche est complètement décrit par `(prev, masque)`,
donc nous mémorisons la réponse dans un tableau 2 dimensions
`dp[prev+1][masque]` (`prev+1` parce que `prev` peut être `-1`).

«» "
dp[prev+1][masque] // -1 -> pas encore calculé
«» "

-----------------------------------------------------------------------------------

- Oui. Récurrence

«» "
dfs(prev, masque) = φ dfs(next, masque) (1<<next))
sur tous les suivants qui ne sont pas dans le masque
et (prév)
nombres[prev] % nombres[next] == 0 OU
nombres[next] % nombres[prev] == 0)
«» "

Quand `mask` contient déjà tous les bits `n`, nous avons construit un
permutation → retourner `1`.

Tous les calculs sont effectués modulo `M = 1 000 000 007`.

-----------------------------------------------------------------------------------

Preuve d'exactitude

Nous prouvons que l'algorithme renvoie le nombre de *spécial*
des permutations.

---

Lemma 1
`dfs(prev, masque)` retourne le nombre de permutations valides qui peuvent être
terminé lorsque le dernier élément placé a index `prev` et l'ensemble
Les indices déjà utilisés sont les «masques».

*Proof. *

*Base:*
Si `mask` contient tous les indices `n`, la permutation est complète.
Exactement une permutation satisfait cet état – celui qui a juste
a été construit – donc la fonction retourne `1`.

*Étape d'introduction:*
Supposons que le lemma tient pour tous les plus grands masques (c.-à-d. avec plus de bits).
L'algorithme itère sur chaque indice `next` qui n'est pas encore utilisé
(`mask` ne contient pas son bit).
Il ajoute `dfs(next, masque=1<<next)' au résultat seulement lorsque

«» "
prev == -1 (aucun élément avant) OU
nombres[prev] % nombres[next] == 0 OU
nombres[next] % nombres[prev] == 0
«» "

Exactement les conditions qui maintiennent la permutation *spécial* pour le
prochain élément.
Par l'hypothèse d'induction chaque appel récursif compte exactement le
permutations qui peuvent être construites après avoir choisi `next`.
Résumant tous les «suivants» admissibles, ils comptent **tous** et **seulement* *
des continuations valides de la permutation partielle actuelle. *



Lemma 2
`dfs(prev, masque)` ne compte jamais une permutation deux fois.

*Proof. *

Le masque garantit que chaque index est utilisé au plus une fois dans un
chemin récursif.
Différents chemins de récursion correspondent à différents ordres de choisir le
même ensemble d'indices, c'est-à-dire à des permutations différentes.
Par conséquent, chaque permutation est produite par exactement un chemin de récursion,
donc compté exactement une fois. *



C'est vrai. Théorème
L'algorithme produit le nombre de **permutations spéciales** du
tableau d'entrée «nums».

*Proof. *

L'appel initial est `dfs(-1, 0)`: aucun élément n'a encore été placé,
"masque = 0".
Par Lemma 1 cet appel retourne le nombre de permutations qui peuvent être
complété à partir du préfixe vide, c'est-à-dire le nombre de *spécial*
permutations de toute la gamme.
La valeur est retournée modulo `M`.



-----------------------------------------------------------------------------------

Analyse de complexité

«» "
n ≤ 14
«» "

Le nombre d'états distincts est

«» "
les possibilités de n+1
les possibilités
«» "

Par conséquent, au plus `(n+1) * 2^n ≤ 15 * 16384 = 245 760` états.

Pour chaque État, nous supprimons tous les indices "n" pour qu'ils soient admissibles.
les éléments suivants,

«» "
Temps : O(n * 2^n * n) = O(n^2 * 2^n)
Mémoire : O(n * 2^n) = O(14 * 16384)
«» "

Les deux s'inscrivent confortablement dans les limites.

-----------------------------------------------------------------------------------

### Mise en oeuvre des références (Java 17)

"Java
Importer java.util. Les tableaux;

solution de classe publique {
int final statique privé MOD = 1_000_000_007;

Services généraux
int n = longueur nums;
// dp[prev+1][masque] (prev == -1 est stocké à l'index 0)
int[] dp = nouvelle int[n + 1][1 << n];
pour (int[] rang : dp) Arrays.fill(row, -1);

retour dfs(nums, -1, 0, dp);
}

/** recherche profondeur-première avec mémoisation */
Int privé dfs(int[] nums, int prev, int masque, int[][] dp) {
// tous les numéros utilisés ?
i (masque) - 1) retour 1;

mémo int = dp[prev + 1][masque];
Si (memo != -1) le mémo de retour;

longueur = 0;
pour (int next = 0; next < nums.longueur; next++) {
si ((masque & (1 << suivant)) != 0) continuer; // déjà utilisé

// admissible à placer `next` après `prev`
si (prév)
nums[prev] % nums[next] ==
nombres[next] % nombres[prev] == 0) {

ways += dfs(nums, next, mask=1 (1 << next), dp);
Voies %= MOD;
}
}

dp[prev + 1][masque] = (int) voies;
les moyens de retour;
}
}
«» "

**Explication du code* *

1. `dp[prev+1][masque]` – tableau de mémorisation.
`prev == -1` est stocké à l'index `0` (`prev+1`).

2. `dfs(nums, prev, masque) "
* `prev` – index de l'élément placé juste avant la position actuelle.
* `masque` – bitmasque d'indices déjà placés.

3. Cas de base: si `mask` contient tous les bits (`mask=1<n)-1`) nous avons
formé une permutation complète → retour `1`.

4. Si l'état a déjà été calculé (`dp[prev+1][masque] != -1') nous
Il suffit de retourner la valeur mise en cache.

5. Dans le cas contraire, nous supprimons tous les indices "next" encore inutilisés,
vérifier la condition de divisibilité et compter récursivement
les permutations qui commencent par "next".
Le résultat est stocké dans `dp` avant de revenir.

-----------------------------------------------------------------------------------

**Test**

"Java
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.s.specialPerm(nouvelle int[]{2,3}); // 3
}
«» "

Le programme imprime `3`, qui correspond au nombre prévu de
les permutations pour «[2,36]».