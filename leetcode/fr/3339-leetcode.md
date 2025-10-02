---
titre: LeetCode 3339. Trouvez le nombre de photos K-Even -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Aperçu de la solution

Pour chaque paire d'éléments adjacents
"(arr[i], arr[i+1])" nous calculons

«» "
(arr[i] * arr[i+1]) – arr[i] – arr[i+1]
«» "

La valeur est **even** si les deux nombres ont la même parité ****
(même ou les deux bizarres).
Donc un tableau *k‐even* est un tableau de longueur `n` qui contient exactement `k` adjacent
des paires de la même parité.

Le problème se réduit à compter combien de façons nous pouvons construire un tableau de
longueur `n` où le nombre de paires d'égalités adjacentes est exactement `k`.

---

#### 1.1 État DP

«» "
dp[pos][cnt][prev] (0 ≤ pos ≤ n, 0 ≤ cnt ≤ k, prev {0,1})
«» "

* `pos` – combien d'éléments ont déjà été choisis (`0 ... n`)
* `cnt` – combien de paires de "good" nous avons construit jusqu'à présent
* `prev` – parité de l'élément placé à la position `pos‐1`
(«0 = impair», «1 = pair»)

Transition pour l'élément suivant:

* Si on place un numéro **even**
*newCnt = cnt + (prev == 1 ? 1 : 0)*
Il existe des numéros `m/2`.
* Si on place un numéro **odd**
*newCnt = cnt* (parce que la paire ne peut pas être "good" si un côté est bizarre)
Il existe des numéros impairs `(m+1)/2`.

La réponse est "dp[n][k][0] + dp[n][k][1] (mod MOD)".

Le DP fonctionne dans la mémoire **O(n · k)** et **O(n · k · 2)**,
bien dans les limites (`n ≤ 750`, `k ≤ n‐1`).

---

- Oui. 2. Mise en œuvre des références

#### 2.1 Java (mise en mémoire du haut vers le bas)

"Java
Importation de java.util.*;

solution de classe publique {
finale statique privée longue MOD = 1_000_000_007L;
privé long[][][] mémo;
Int m privé;

Nombre d'entrées publiques d'images (int n, int m, int k) {
ce.m = m;
mémo = nouveau long[n][k + 1][2];
pour (int i = 0; i < n; i++)
pour (int j = 0; j <= k; j++)
les tableaux.fill(memo[i][j], -1L);
retour (int) dfs(0, 0, 0, k);
}

Pf privés longs (int pos, int cnt, int prev, int k) {
Si (pos) 0) {/ aucun élément précédent
retour cnt == k ? 1 : 0; // ne devrait jamais se produire
}
si (pos) 0) retour 0; // sécurité
si (cnt > k) retourne 0; // taille
si (pos) 0) retour 0;/

si (memo[pos - 1][cnt][prev] != -1L)
retour [pos - 1][cnt][prev];

long res = 0;
// placer un nombre pair
Int nouveau Cnt = cnt + (prev == 1 ? 1 : 0);
res += ((m / 2L) * dfs(pos + 1, newCnt, 1, k)) % MOD;

// placer un nombre impair
res += (((m + 1L) / 2L) * dfs(pos + 1, cnt, 0, k)) % MOD;

mémo[pos - 1][cnt][prev] = res % MOD;
retour [pos - 1][cnt][prev];
}
}
«» "

> **Pourquoi mémorisation? **
> L'espace d'état est petit, mais les appels récursifs explosent sans mise en cache.
> Le stockage des résultats transforme la récursion exponentielle en DP linéaire.

---

#### 2.2 Python (PDD implicite)

'`python
MOD = 1 000 000 007

def countOfArrays(n: int, m: int, k: int) -> Int:
evens = m // 2
risque = (m + 1) // 2

# dp[pos][cnt][prev] prev: 0 impair, 1 pair
dp = [[[0, 0] pour _ dans la plage(k + 1)] pour _ dans la plage(n + 1)]
# premier élément – pas encore de paire
dp[1][0][0] = cotes
dp[1][0][1] = paires

pour pos dans la plage(2, n + 1):
pour cnt dans la plage (k + 1):
# précédent impair
si dp[pos - 1][cnt][0]:
dp[pos][cnt][0] = (dp[pos][cnt][0] +
% MOD
si cnt + 1 <= k:
dp[pos][cnt + 1][1] = (dp[pos][cnt + 1][1] +
% MOD
# précédent même
si dp[pos - 1][cnt][1]:
dp[pos][cnt][0] = (dp[pos][cnt][0] +
dp[pos - 1][cnt][1] * cotes) % MOD
si cnt + 1 <= k:
dp[pos][cnt + 1][1] = (dp[pos][cnt + 1][1] +
% MOD

retour (dp[n][k][0] + dp[n][k][1]) % MOD
«» "

> **Conseil:**
> Initialiser le premier élément séparément évite le cas particulier "prev = -1".

---

### 2.3 C++ (DP ascendant)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
nombre d'int d'images (int n, int m, int k) {
longue MOD = 1'000'000'007LL;
longues paires longues = m / 2;
longue probabilité = (m + 1) / 2;

// dp[pos][cnt][prev] prev: 0 impair, 1 pair
vecteur<vector<array<long long,2>>> dp(n + 1,
vecteur<array<long long,2>>(k + 1, {0,0});

// premier élément
dp[1][0][0] = cotes;
dp[1][0][1] = paires;

pour (int pos = 2; pos <= n; ++pos) {
pour (int cnt = 0; cnt <= k; ++cnt) {
// avant impair
si [dp[pos-1][cnt]]] {
dp[pos][cnt][0] = (dp[pos][cnt][0] +
dp[pos-1][cnt][0] * cotes) % MOD;
si (cnt+1 <= k)
dp[pos][cnt+1][1] = (dp[pos][cnt+1][1] +
dp[pos-1][cnt][0] * evens) % MOD;
}
// avant même
si (dp[pos-1][cnt][1]) {
dp[pos][cnt][0] = (dp[pos][cnt][0] +
dp[pos-1][cnt][1] * cotes) % MOD;
si (cnt+1 <= k)
dp[pos][cnt+1][1] = (dp[pos][cnt+1][1] +
dp[pos-1][cnt][1] * evens) % MOD;
}
}
}
retour (dp[n][k][0] + dp[n][k][1]) % MOD;
}
};
«» "

---

- Oui. 3. Billet de blog – Le bon, le mauvais, et le lamentable de résoudre le leetCode #3339

### 3.1 Titre et mots clés
**Titre:**
*Le bon, le mauvais, et le lamentable de résoudre le leetCode .

**Mots-clés principaux:**
- Code Leet 3339
- tableaux k-even
- entretien de programmation dynamique
- codage des entretiens d'emploi
- conception d'algorithmes
- Optimisation du PDD

Pourquoi le référencement ? *
Ces mots clés apparaissent dans les requêtes de recherche populaires des candidats à l'ingénierie logicielle
à la recherche d'un entretien. Le classement supérieur aide les recruteurs à repérer votre blog.

---

3.2 Introduction

> On vous donne trois entiers *n*, *m*, *k*.
> Comptez combien de tableaux de taille *n* avec des éléments dans [1, *m*] ont exactement *k* paires adjacentes dont le produit moins la somme est pair. (en milliers de dollars)

Il semble intimidant, mais une fois que vous reconnaissez le tour de parité, la solution est
un problème de DP de manuel.
Dans cet article, je vais passer par:

1. **Le bon** – espace propre, raisonnement de parité intuitive.
2. **Les mauvais** – pièges comme le débordement entier, mauvais cas de base.
3. **La moche** – code récursif messy qui est difficile à déboguer et à tester.

En chemin, je vous donnerai un code prêt à copier en **Java, Python et C++**,
plus des conseils d'entrevue pour impressionner les gestionnaires d'embauche.

---

3.3 Les bonnes – Pourquoi Ce problème est un PDD

Pourquoi c'est bon Explication
-- -- -- -- -- --
**Éclairer l'état du problème**.Un seul paramètre entier change ; la condition de parité est facile à calculer. Autres
Autres **L'espace de l'État est petit. Autres
**Transitions monotoniques** Chaque étape ne dépend que de la parité de l'élément précédent. Autres
**Arithmétique modulaire**La réponse est toujours prise modulo 1 000 000 007, une constante familière. Autres
**Application directe de DP**. Autres

Ces traits en font une question d'entrevue idéale pour un candidat de niveau intermédiaire
connaît les modèles de base du PDD.

---

3.4 Les mauvaises – erreurs courantes

Une erreur dans la façon dont ça arrive
C'est le cas.
La bonne condition est *même parité* (même ou les deux impairs). Autres
**Off‐by‐one dans les indices «dp»**= Mélanger 0-based vs 1-based array length=» Utilisez «dp[pos][cnt][prev]» où «pos» est le nombre d'éléments placés. Autres
**Ignorer le débordement**= Utiliser `int` pour la multiplication intermédiaire (`evens * ways`)== Utiliser `long` (Java) ou `int64_t` (C++), mod après chaque multiplication. Autres
**Profondeur de récursion non nécessaire**=La récursion directe peut atteindre les limites de la pile pour `n=750`=Utilisez un DP ascendant ou une mémoisation itérative. Autres
**Caisse de base manquante** Initialiser le premier élément séparément: `dp[1][0][0] = cotes`, `dp[1][0][1] = evens`.

Une liste de contrôle mentale rapide avant le codage :

1. La condition de parité est-elle correcte?
2. Les tailles des tableaux sont-elles suffisantes?
3. Est-ce que je lance à 64 bits avant la multiplication?
4. Est-ce que j'applique le modulo à chaque étape ?

---

#### 3.5 L'horrible – Code de mess qui fait des entrevues

Considérez le modèle récursif suivant (Java):

"Java
solution longue(int pos, int cnt, int prev) {
si (pos) n) retour cnt == k ? 1 : 0;
longue ret = 0;
ret += (m/2) * resolu(pos+1, cnt + (prev=1?1:0), 1);
(m+1)/2) * résoudre(pos+1, cnt, 0);
retourner ret % MOD;
}
«» "

*Pourquoi c'est laid*

- Oui. Pas de mémoisation → temps exponentiel.
- Pas de taille pour "cnt > k".
- Mélanger la multiplication et le module peut déborder.
- Le premier appel avec `prev` non défini (`-1`) conduit à des bugs subtils.

**À emporter :** Dans une entrevue, vous voulez un code propre, commenté que *juste fonctionne*,
pas un hack intelligent qui peut échouer sur les cas de test cachés.

---

### 3.6 Entretien– Conseils prêts

Pourquoi ça aide ?
-- -- -- -- -- --
**Expliquer la réduction de parité tôt** Autres
**Énoncer clairement la transition du PDD** Autres
Autres **Afficher la case de base pour le premier élément**. Autres
**Mention modulo handling**.Les recruteurs s'attendent à ce que vous soyez prudent avec de grands entiers. Autres
**Complexité de l'action** Autres
Autres **Demander des éclaircissements**= Par exemple, `k` est toujours < `n`?= – révèle la rigueur. Autres

Aussi, donnez-leur un bref contrôle de la santé mentale de la carie, comme:

- La réponse `n = 1, k = 0` → doit être `m`.
- `k = 0` → aucune paire adjacente ne satisfait à l'état.
- `k = n-1` → toutes les paires adjacentes doivent correspondre à la parité.

Ces petites vérifications peuvent transformer une solution décente en une solution parfaite.

---

### 3.7 Extraits de code pour référence rapide

On trouvera ci-dessous des extraits de notes de travail dans les trois langues principales.
Copiez, collez, lancez, et vous êtes prêt à soumettre.

Langue Nom du fichier Ligne clé
C'est le cas.
Java "Solution.java" "dp[pos][cnt][prev]` bas vers le haut PDD. Autres
"Python" `3339_k_even_arrays.py`" Bas-up `dp` avec deux boucles imbriquées. Autres
"C++" "3339_k_even_arrays.cpp" "vecteur<vecteur<array<long long,2>>" PDD. Autres

N'hésitez pas à les adapter à votre style de codage – gardez la logique DP intacte.

---

### 3.7 Conclusion – Transformer le problème en pièce de portefeuille

LeetCode 3339 est un problème *classique* d'interview DP.
La solution est simple une fois que vous remarquez le tour de parité, mais un **clean
mise en œuvre** est essentielle pour briller dans les entrevues.

Utilisez le code ci-dessus comme kit *Starter* pour votre portfolio.
Ajoutez ce problème à votre GitHub, marquez le dépôt avec les mots-clés,
et le lier dans votre Linked Dans la section Projets.
Les recruteurs aiment voir des solutions prêtes à l'entrevue qui sont *rapides, correctes et
Bien documenté. *

Bon codage et bonne chance pour votre prochaine interview!

---

### 3.8 Clôture

*Si vous avez trouvé cet article utile, partagez-le sur LinkedIn, Twitter et
Des communautés discordantes comme les «questions de carrière».
Des questions ? Laissez un commentaire ci-dessous ou envoyez-moi un courriel à `dev@exemple.com`. *

---

####3.9 FAQ (Section facultative)

Question Réponse
-- -- -- -- -- --
* Pouvons-nous le résoudre avec des combinatoires? Vous pouvez, mais le DP est plus simple et garantit la justesse. Autres
*Et si `m` est 109?*= Encore très bien – nous ne nous divisons que par 2 et utilisons des ints 64 bits. Autres
*Le PDD change-t-il pour `k` ≥ `n`? C'est impossible; `k` doit être < `n`. L'énoncé du problème le garantit. Autres

---

- Oui. 4. Notes de clôture

Le problème LeetCode #3339 peut sembler obscur, mais avec le trick **parity** il
se réduit à un DP classique.
En présentant **clean Java, Python et C++, vous montrez des recruteurs
que vous pouvez:

- Traduisez les maths en code.
- Cas de bord de poignée et modulo arithmétique.
- Vérifiez la complexité du temps et de la mémoire.

Donc la prochaine fois que l'intervieweur dit "Let"s voir comment vous attaquez les tableaux k-even,
vous serez prêt à expliquer l'état, la transition et la complexité en secondes
et de fournir un code de qualité de production sans bug.

Bonne interview – et que les chances (et les mêmes) soient toujours en votre faveur!

---