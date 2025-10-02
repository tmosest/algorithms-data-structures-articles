---
titre: LeetCode 3277. Score XOR maximum Subarray requêtes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes

**Score XOR maximum Subarray requêtes (Code Leet 3277)* *

On vous donne un tableau entier `nums` (longueur ≤ 2000) et jusqu'à 105 requêtes
«queries[i] = [li, ri]».
Pour chaque requête, vous devez déclarer le **maximum XOR‐score** qui peut être obtenu
en prenant **toute** sous-tribution de «nums[li...ri]».

> **Le score XOR d'un tableau** `a` est défini en faisant plusieurs fois
> `a[i] ← a[i] XOR a[i+1]` pour chaque `i` * simultanément* valide et ensuite
> suppression du dernier élément, jusqu'à ce qu'un seul élément reste.
> Ce seul élément restant est le score.

Des exemples sont fournis dans l'énoncé; l'observation clé est que
le score d'une sous-tribu est *pas* le XOR de tous ses éléments, mais il peut être
calculé efficacement avec une programmation dynamique.

---

- Oui. 2. Algorithme – PDD ascendant

Laissez

* `xor[i][j]` – XOR-score de la sous-tribu *exacte* `nums[i...j] "
(c.-à-d. le score si nous commençons par cette sous-entente et **ne pas considérer**
tout sous-réseau intérieur).
* «best[i][j]» – **maximum** XOR-score sur **all** sous-cours intérieur
"nums[i...j]".

- Oui. Récurrence

«» "
xor[i][i] = nombres[i]
best[i][i] = nombres[i]

pour len = 2 ... n:
pour i = 0 ... n-len:
j = i + len - 1
xor[i][j] = xor[i][j-1] ^ xor[i+1][j] // fusionner deux moitiés
best[i][j] = max( best[i][j-1], // étendre à gauche
best[i+1][j], // étendre à droite
xor[i][j] // prendre l'ensemble [i..j]
«» "

La première ligne de la boucle intérieure fusionne les deux moitiés * adjacentes* qui sont
déjà connu; la deuxième ligne choisit le meilleur parmi:

1. la meilleure sous-tribu qui se termine à «j-1» («meilleure [i][j-1]»;
2) la meilleure sous-procès qui commence à «i+1» («meilleure [i+1][j]»;
3. l'ensemble de la sous-entente «nums[i...j]» elle-même («xor[i][j]».

Une fois les tableaux remplis, répondez à chaque requête en **O(1)** par
«meilleure[l][r]».

- Oui. Pourquoi ça marche ?

La règle de transformation est associative dans le sens suivant:

«» "
score( [x, y, z] ) = (score([x, y]) XOR score([y, z]) (le dernier élément)
après la première réduction)
«» "

Par conséquent, `xor[i][j] = xor[i][j-1] ^ xor[i+1][j]` est valable pour tous
"i < j".
Le maximum à l'intérieur d'une plage ne peut provenir que d'une des deux sous-échelles
plus toute la gamme elle-même – d'où la récurrence `max()`.

---

- Oui. 3. Preuve d'exactitude

Nous prouvons que le DP renvoie en effet la réponse correcte pour chaque requête.

Lemma 1
Pour tout `i ≤ j`, `xor[i][j]` calculé par la récurrence égale le score XOR
obtenu si nous *démarrons* avec le sous-arraché `nums[i...j]` et ne prenons jamais
une sous-tribu plus courte à l'intérieur.

*Proof. *
Cas de base `len = 1`: triviallement le score d'un seul élément est que
élément.
Étape d'induction: supposons que le lemma tient pour toutes les longueurs `< len`.
Pour `nums[i...j]` la première réduction crée deux nombres

«» "
L = xor[i][j-1] (score des nombres[i...j-1])
R = xor[i+1][j] (score de nombres[i+1...j])
«» "

et le nouvel élément est "L XOR R".
Par hypothèse d ' induction " xor[i] " et " xor[i+1] " déjà tenir le
des scores corrects des deux moitiés, donc la récurrence
`xor[i][j] = xor[i][j-1] ^ xor[i+1][j]` donne le résultat correct. *



Lemma 2
Pour tout «i ≤ j», le «best[i][j]» est égal au score XOR maximal sur **all**
sous-tribus de «nums[i...j]».

*Proof. *
Cas de base `i=j`: il n'existe qu'une seule sous-tribu, de sorte que `best[i][i] = nums[i]`.
Étape d'induction : supposons que le lemma tient pour toutes les longueurs plus courtes.
Chaque sous-tribu de «nums[i...j]» est

1. à l'intérieur de «nums[i...j-1]», ou
2. à l'intérieur de "nums[i+1...j]", ou
3. l'ensemble des «nums[i...j]» lui-même.

Par l'hypothèse d'induction, les meilleurs scores de (1) et (2) sont
«best[i][j-1]» et «best[i+1][j]» respectivement, tandis que (3) est «xor[i][j]».
Le maximum des trois est donc le maximum sur **tous** sous-tribus,
d'où la récurrence pour «best[i][j]» est correcte. *



- Oui. Théorème
Après avoir rempli les tables, pour toute requête `[l, r]` la réponse «meilleur[l][r] "
est le maximum de XOR-score obtenu à partir d'un sous-ensemble de "nums[l...r]".

*Proof. *
Immédiatement à partir de Lemma 2: "meilleur[l][r]" est défini exactement comme le maximum
sur tous les sous-réseaux de cette gamme. *



---

- Oui. 4. Analyse de la complexité

* **Heure**
* Construire les deux tableaux : `-_{len=2}^{n} (n-len+1) = O(n2)`
* Réponse aux questions `q` en O(1) : `O(q)`
* **Total:** "
Avec `n ≤ 2000`, `n2 = 4 000 000`, assez rapide.

* **Espace**
Deux tables entières `n × n` → `2 * n2 * 4 octets 32 MB` en Java
(moins en C++/Python en raison de la mise en page de la mémoire).
Acceptable dans la limite de 512 Mo de LeetCode.

* **Notes pratiques**
* Utilisez **court-circuit** `pour` boucles pour garder le facteur constant bas.
* En Java, préférez `int[]` plutôt que `ArrayList` pour éviter la boxe.
* Dans Python, une liste de listes fonctionne bien; `sys.setrecursionlimit` est
*Pas besoin parce que nous utilisons un DP itératif.

---

- Oui. 5. Mise en oeuvre des références

> **Les trois versions utilisent le même DP ascendant.
> Vous pouvez copier l'extrait qui correspond à votre langue préférée. **

#### 5.1 Java 17

"Java
Importation de java.util.*;

solution de classe publique {
int[] max.SubarrayXor(int[] nums, int[][] requêtes) {
int n = longueur nums;
int[] xor = nouveau int[n][n];
int[][]meilleur = nouveau int[n][n];

// cas de base: longueur 1
pour (int i = 0; i < n; i++) {
xor[i]i] = nombres[i];
best[i][i] = nombres[i];
}

// remplir en augmentant la longueur
pour (int len = 2; len <= n; len++) {
pour (int i = 0; i + len <= n; i++) {
j = i + len - 1;
xor[i][j] = xor[i][j-1] ^ xor[i+1][j];
best[i][j] = Math.max[i][j-1],
Math.max(meilleur[i+1][j], xor[i][j]);
}
}

int[] ans = nouvelle int[queries.longueur];
pour (int k = 0; k < requêtes.longueur; k++) {
int l = requêtes[k][0];
int r = requêtes[k] [1];
ans[k] = meilleur[l][r];
}
le retour des an;
}
}
«» "

#### 5.2 Python 3

'`python
def maximumSubarrayXor(nombres, requêtes):
n = len(nums)
xor = [[0] * n pour _ dans la plage(n)]
best = [[0] * n pour _ dans la plage(n)]

# case de base
pour i dans la plage(n):
xor[i][i] = nombres[i]
best[i][i] = nombres[i]

pour la longueur de portée(2, n + 1):
pour i dans la plage (n - longueur + 1):
j = i + longueur - 1
xor[i][j] = xor[i][j-1] ^ xor[i+1][j]
best[i][j] = max(best[i][j-1], best[i+1][j], xor[i][j])

retourner [meilleur[l][r] pour l, r dans les requêtes]
«» "

Numéro 5.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vectorielle<int> maximumSubarrayXor(vecteur<int> et nombres,
vector<vector<int>&questions) {
int n = nombres.size();
vecteur<vector<int>> xorTbl(n, vector<int>(n));
vecteur<vector<int>> meilleur(n, vecteur<int>(n));

// Cas de base
pour (int i = 0; i < n; ++i) {
xorTbl[i][i] = meilleur[i][i] = nombres[i];
}

// DP en augmentant la longueur
pour (int len = 2; len <= n; + len) {
pour (int i = 0; i + len <= n; ++i) {
j = i + len - 1;
xorTbl[i][j] = xorTbl[i][j-1] ^ xorTbl[i+1][j];
best[i][j] = max({best[i][j-1], best[i+1][j], xorTbl[i][j]};
}
}

vecteur <int> ans;
as.reserve(queries.size());
pour (auto &q : requêtes) {
[q[0]];
}
le retour des an;
}
};
«» "

---

- Oui. 6. Autre solution (mémorisation-efficacité) Approche

Si vous êtes serré sur la mémoire (par exemple n = 2000 est toujours bien, mais vous pouvez vouloir
pour déposer une table de 32 Mo), vous pouvez traiter les requêtes *par longueur*:

1. Indices de requêtes de groupe par `len = r-l`.
2. Garder un seul tableau `cur` qui stocke les scores maximums actuels pendant
nous effectuons les réductions XOR en place sur `nums`.
3. Chaque fois que l'étape de réduction actuelle correspond à la longueur d'une requête,
répondre à toutes ces questions avec `cur[l]`.

Ceci donne une solution spatiale **O(n2)** et **O(n)**
(voir l'éditorial de LeetCode).

---

- Oui. 7. Pourquoi cela importe pour les entretiens d'emploi

* **Le choix de la structure des données** – le DP bidimensionnel est un classique
modèle de programmation dynamique; les recruteurs apprécient un cache propre
mise en œuvre.
* ** Pensée algorithmique** – vous devriez être en mesure d'expliquer la transformation
règle et pourquoi le maximum à l'intérieur d'une plage doit venir des deux
les sous-catégories plus toute la gamme.
* **Le raisonnement de complexité** – les intervieweurs aiment quand vous dites
"O(n2 + q)" complexité et expliquer pourquoi elle satisfait aux contraintes.
* **Cas d'Edge** – n'oubliez pas de tester les gammes d'éléments uniques
longueur la plus longue possible.

---

- Oui. 7. Liste de contrôle finale avant la soumission

- [ ] Vérifier l'environnement: Java 17, Python 3.8+, C++17.
- [ ] Tester avec les exemples de cas donnés dans le problème.
- [ ] Exécuter un test de contrainte: aléatoire `n` (
vous restez dans la limite du temps (- 0,2 s sur LeetCode).
- [ ] Vérifie le débordement d'entier ?
Le score XOR ne dépasse jamais `232-1` parce que chaque élément est un `int`.

---

- Oui. 8. Pourquoi cette solution est une bonne entrevue

* **Concept algorithmique solide** – programmation dynamique sur intervalles.
* **Le raisonnement basé sur leproof** – vous pouvez passer par les étapes d'induction
dans un entretien.
* **Scalabilité** – la complexité temporelle est indépendante du nombre de
questions; seuls les coûts de pré-traitement sont importants.
* **Codage manuel** – l'implémentation de référence est courte et
C'est propre, donc vous pouvez le coder dans une minute si demandé.

Bonne chance pour votre entretien ! C'est ce qu'il a dit.

---

- Oui. 9. Bonus – Sommaire de style blog

> *Si vous voulez une lecture rapide, faites défiler vers le bas jusqu'à l'adresse suivante : *

#### Résumé du blog

Une seule page, sans fioritures, explication du PDD qui résout le
> «Maximum XOR Sub‐array» problème sur LeetCode, y compris la justesse
> des extraits de preuve, de complexité et de code en Java, Python et C++.

---

## 10. Glossaire

Symbole Signification
C'est quoi ?
Longueur du nombre
"xor[i][j]"" XOR-score de "nums[i...j]" quand vous commencez avec cette gamme
"Best[i][j]""" XOR-score maximum parmi tous les sous-groupes de "nums[i...j]""
Longueur du sous-réseau actuel (utilisée pour le DP)
Liste des paires de paires de paires de paires de paires de «[l, r]» (0 indices basés) Autres

---

> **Profitez du codage!** Si vous vous retrouvez dans le temps, vérifiez que vous
> compilé avec `-O2` (C++), utilisé `sys.setrecursionlimit` seulement si vous
> passé à une version récursive, et évité copie inutile.