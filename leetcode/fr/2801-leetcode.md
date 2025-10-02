---
titre: LeetCode 2801. Compter les nombres de pas dans l'intervalle -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Ce qu'on vous demande de faire**

Avec deux chaînes décimales `low` et `high` (chaque chaîne peut contenir jusqu'à 100 000 chiffres)
compter tous les *numéros de pas* `x` de sorte que

«» "
faible ≤ x ≤ élevé
«» "

Un *numéro de pas* est un entier positif dont les chiffres décimaux satisfont

«» "
= 1 pour chaque paire de chiffres adjacente
«» "

(Exemples: 10, 121, 1234, 987, ...)

La réponse doit être retournée modulo `1 000 000 007`.

-----------------------------------------------------------------------------------

- Oui. 1. Idée de haut niveau

La gamme `[faible, élevée]` est astronomiquement grande – jusqu'à `10^100000`.
Nous ne pouvons pas itérer à travers tous les nombres.

Au lieu de cela, nous

1. **Count** tous les nombres de marche `=" haut` → `cnt Haut.
2. **Count** tous les nombres d ' échelon < < bas > > (c ' est-à-dire < < bas 1 > > ) → `cntLow`.
3. La réponse est `cntHigh - cntLow` et nous en ajoutons une de plus si *low est un pas
nombre (parce que la soustraction le supprime).

Le problème principal est donc :

> **Combien de nombres d'étapes sont `= N`? **

Il s'agit d'une programmation dynamique *numérique* classique (également appelée *numérique DP* ou *numérique).

-----------------------------------------------------------------------------------

- Oui. 2. Pourquoi le numérique-DP fonctionne

Nous traitons la représentation décimale de `N` du chiffre le plus significatif au moins.
Tandis que nous sommes toujours étanches (c'est-à-dire le préfixe que nous avons choisi est exactement égal à la
préfixe de `N`), le chiffre suivant que nous pouvons mettre est limité par le chiffre correspondant de `N`.
Dès que nous choisissons un chiffre plus petit, nous devenons libres et pouvons mettre les chiffres restants.

Pour faire respecter la propriété tremplin, nous conservons la valeur du chiffre précédent
(prévu).
Au tout premier chiffre non zéro nous n'avons pas de "prev", donc tout chiffre non zéro est
permis.
Après cela, le chiffre suivant doit différer de `prev` de exactement 1.

Nous devons également soutenir les nombres dont la longueur est **plus courte** que `N`.
Ceci est géré par un drapeau *leading-zero* – alors que nous ne mettons toujours que des zéros
n'ont pas encore commencé le nombre ; une fois que nous avons mis un chiffre non zéro le drapeau leader-zéro
est dégagé et à partir de là, chaque position est un vrai chiffre.

-----------------------------------------------------------------------------------

- Oui. 3. État DP

Paramètre Description Valeurs possibles
- C'est quoi ?
Indice "pos" dans la chaîne (0 ... possibilités "len")
Nous sommes toujours liés par le préfixe `N`?
"prev"" chiffre précédent (`-1` si nous n'avons pas encore vu un non-zéro) Autres
Est-ce que nous avons déjà placé un chiffre non zéro ? "0" ou "1"

Nombre total d'États:
`(len+1) × 2 × 11 × 2 ↓ 44 × len` – seulement quelques milliers pour `len = 100 000`.

Pour chaque état nous essayons au plus 10 chiffres (0‐9), donc la complexité globale est linéaire
dans le nombre de chiffres.

-----------------------------------------------------------------------------------

- Oui. 4. Récurrence

«» "
dfs(pos, serré, prev, commencé):
Si la réponse est la suivante:
// nous avons construit un nombre – mais nous ne devons pas compter le nombre all-zero
retour commencé ? 1 : 0

si mémorisé → le retourner

limite = serré ? N[pos] : 9
ans = 0

pour d de 0 à la limite:
next_tight = serré et (d == limite)

// nous pouvons placer d si:
// • nous sommes toujours dans la partie principale zéro, OU
// • nous n'avons pas encore choisi de chiffre (prev == -1), OU
// • d diffère de prev par exactement 1
si pas commencé et d == 0:
// toujours en tête des zéros
ans += dfs(pos+1, next_tight, prev, false)
Sinon, si commencés==false ou abs(prev - d) == 1 :
ans += dfs(pos+1, next_tight, d, true)
%= MOD
mémos
retour et
«» "

-----------------------------------------------------------------------------------

- Oui. 5. Manipulation de la liaison "bas"

Nous calculons :

«» "
Cnt Haut = dfs(0, vrai, -1, faux) // nombres ≤ haut
cntLow = dfs(0, true, -1, false) // nombres < faible (c'est-à-dire ≤ faible-1)
«» "

La différence `cntHigh - cntLow` compte tous les nombres de pas dans `[low+1 , high]`.

Si `bas` est lui-même un nombre de pas nous devons ajouter un autre, parce que la soustraction
Enlève ça.
Vérifier que c'est un simple balayage linéaire des chiffres de `low`.

-----------------------------------------------------------------------------------

- Oui. 6. Mise en œuvre complète de Java

"Java
Importer java.util. Les tableaux;

solution de classe {
int final statique privé MOD = 1_000_000_007;

/* --------------------------------------------- */
/* API publique */
/* --------------------------------------------- */
nombre d'entrées publiquesSteppingNumbers(String bas, String high) {
long cntHigh = compteJusqu'à (élevé);
longue cntLow = compteJusqu'à (faible);

long diff = (cntHigh - cntLow + MOD) % MOD; // nombres dans [low+1 , high]

si (isStepping(low)) { // ajouter bas si nécessaire
diff = (diff + 1) % MOD;
}
retour (int) diff;
}

/* --------------------------------------------- */
/* helper: nombre de marches ≤ N */
/* --------------------------------------------- */
Compteur privé long à (String N) {
int len = longueur N();
Long[][][][] mémo = nouveau Long[len][2][11][2];
// chiffre prev : -1 ... 9 → index prev+1 (0 ... 10)
// commencé? : 0 / 1 → index 0 / 1
// serré? : 0 / 1
retourner dfs(0, true, -1, false, N, mémo);
}

/* --------------------------------------------- */
/* PDD récursif */
/* --------------------------------------------- */
privé long dfs(int pos, booléen serré, int prev, booléen commencé,
Chaîne N, longue[][][] note] {

Si [pos] N.longueur() {
// Numéro construit? (à l'exclusion du nombre zéro)
retour commencé ? 1 : 0;
}

Int serré Idx = serré ? 0 : 1;
int prevIdx = prev + 1; // décalage de +1 car prev peut être -1
début int Idx = commencé ? 0 : 1;

si [memo[pos][tightIdx][prevIdx][startIdx] != null)
retour[pos][tightIdx][prevIdx][startIdx];

long res = 0;
int limite = serré ? N.charAt(pos) - '0' : 9;

pour (int d = 0; d <= limite; ++d) {
booléen suivant Tight = limite serrée && (d ==);
booléen nextStart = démarré (d != 0);

Si (!démarré && d == 0) { // toujours en tête des zéros
res += dfs(pos + 1, suivant Tight, prev, false, N, mémo);
} sinon si (!commencé) 1) {
res += dfs(pos + 1, suivant Tight, d, nextStart, N, mémo);
}
res %= MOD;
}

mémo[pos][tightIdx][prevIdx][startIdx] = res;
retour rés;
}

/* --------------------------------------------- */
/* vérifier si une chaîne décimale donnée est un nombre de pas */
/* --------------------------------------------- */
booléen privé estStepping(String s) {
pour (int i = 1; i < s.longueur(); ++i) {
i (Math.abs(s.charAt(i) - s.charAt(i - 1)) != 1) {
retourner faux;
}
}
retour vrai; // s est positif, pas besoin de vérifier pour zéro
}
}
«» "

- Oui. Pourquoi ce code est correct

Préoccupation Comment il est géré
Il n'y a pas de lien entre les deux.
**Le numéro de base retourne `0` si `started==false`. Autres
Chaque ajout est réduit modulo "MOD". Autres
**Nombres négatifs** La soustraction est enveloppée avec `+MOD` avant le `%`. Autres
Nous utilisons `long` pour les sommes intermédiaires et `long` objets pour la mémorisation;
chaque valeur est ≤ `len * 10` (=10^6 pour 100 k chiffres) de sorte que `long` est sûr. Autres
**Heure**
Dans le pire des cas – assez vite. Autres

-----------------------------------------------------------------------------------

- Oui. 7. Pièges communs et comment nous les évitons

Piège Explication
- C'est quoi ?
**Composition Un nombre de pas doit être *positif*. Dans le cas de base retour `démarré? 1 : 0`. Autres
**Les nombres plus courts doivent être représentés. Utilisez un drapeau `démarré`. Autres
**Modulo sur la soustraction**Le résultat peut devenir négatif. Autres
**Large chaîne**=La profondeur de récursion jusqu'à 100 000 peut déborder la pile d'appel. Java de la profondeur de récursion est ~1 000 000, donc il est très bien, mais si vous voulez un
approche plus sûre vous pouvez réécrire le PDD itérativement. Autres
** `prev` indexing**= `prev` peut être `-1`.= Déplacement de +1 lors de son utilisation comme index de tableau. Autres
**Performance**
Appel de récursion. Attribuer le tableau 4-D une fois par lien (`len × 2 × 11 × 2`). Autres

-----------------------------------------------------------------------------------

- Oui. 8. Vérification rapide de la santé mentale

"Java
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.countSteppingNumbers("1", "9")); // 8 (1,2,3,4,5,6,8,9)
Système.out.println(sol.countSteppingNumbers("10", "20")); // 2 (10,12)
Système.out.println(sol.countSteppingNumbers("100", "200")); // 5 (101 121 121? no, 121 < 200; 123 121? etc.)
}
«» "

Vous pouvez remplacer `String` par `StringBuilder` si vous préférez, mais l'algorithme reste
pareil.

-----------------------------------------------------------------------------------

- Oui. 9. A emporter

* Réduisez l'intervalle `[faible , élevé]` à deux problèmes liés par le biais du chiffre‐ PDD.
* Dans le DP, n'oubliez pas: `pos`, `standard`, `prev` (ou 'no prev'), et si le
Le numéro a commencé.
* Passez le numéro zéro dans le cas de base.
* N'oubliez pas d'ajouter `low' en arrière si c'est lui-même un nombre de pas.

Vous pouvez ainsi gérer en toute sécurité les gigantesques limites à 100 000 chiffres – la solution fonctionne
en quelques secondes sur le matériel moderne.