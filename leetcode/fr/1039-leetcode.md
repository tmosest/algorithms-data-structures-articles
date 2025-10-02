---
titre: LeetCode 1039. Triangulation minimale du polygone -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 1039 – Triangulation minimale des points du polygone
*Moyen *** * Programmation dynamique ** *Matrix-Chain Multiplication Variante*

---

### TL;DR
- **Objectif** – Diviser un polygone convexe en triangles `n‐2` de telle sorte que la somme des
`value[i] * value[j] * value[k]` pour chaque triangle est minimal.
- **Solution** – Classique **intervalle DP** (variante de Multiplication Matrix-Chain).
- **Complexités** – temps "O(n3)", espace "O(n2)".

---

Récapitulation des problèmes

On vous donne un tableau `valeurs` (`3 ≤ n ≤ 50`) où `valeurs[i]` est le poids du vertex `i` d'un polygone convexe `n` côté.
Une triangulation est un ensemble de triangles `n‐2` dont les sommets sont des sommets du polygone.
Le score d'une triangulation = somme du produit des valeurs des trois sommets de chaque triangle.

Retournez la note *minimum* possible.

> **Exemple**
> `valeurs = [3,7,4,5]` → score minimal = **144** (triangulation: `(3,4,5)` + `(3,4,7)`).

---

Intuition – Multiplication Matrix-Chain

Si vous regardez un sous-polygon défini par vertices `i ... j`, vous pouvez choisir un vertex `k` (`i < k < j`) comme troisième vertex d'un triangle qui utilise le bord `i‐j`.

«» "
Les - - - - - - - - Non.
C'est vrai.
C'est vrai.
«» "

Le score de ce triangle est "valeurs[i] * valeurs[j] * valeurs[k]".
Le polygone restant est divisé en deux sous-polygones indépendants: `i ... k` et `k ... j`.
Ainsi, la note minimale pour "i ... j" peut être exprimée de manière récursive:

«» "
dp[i][j] = min sur k ( dp[i][k] + dp[k][j] + valeurs[i]*valeurs[j]*valeurs[k])
«» "

Lorsque le sous-polygon n'a que deux sommets (`j == i+1`), aucun triangle ne peut être formé → score `0`.

C'est exactement la récurrence utilisée dans la Multiplication Matrix‐Chain, seul le terme "Cost" est un produit de trois nombres au lieu d'un coût de multiplication matrix.

---

Conception de l'algorithme

Étape
- C'est quoi ?
Autres Initialiser un tableau 2-D `dp[n][n]` avec `-1` (ou `=" pour le bas vers le haut). Autres
Autres 2) Calculer récursivement «dp[i][j]» en utilisant la mémorisation (en haut vers le bas) ou en itérer sur des longueurs subpolygonales croissantes (en bas vers le haut). Autres
Pour chaque «i < k < j» évaluer «score = dp[i][k] + dp[k][j] + valeurs[i]*valeurs[j]*valeurs[k]». Autres
Autres 4. Entreposez le minimum dans `dp[i][j]`. Autres
Le résultat est "dp[0][n-1]". Autres

---

Code en trois langues

> **Note:** Toutes les implémentations suivent la même logique – mémoisation descendante.
> Le bas-up peut être ajouté dans les commentaires si vous préférez une version itérative.

C'est pas vrai. Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
int public minScoreTriangulation(valeurs int[]) {
int n = valeurs.longueur;
int[] dp = nouvelle int[n];
pour (int[] rang : dp) Arrays.fill(row, -1);
retourner dfs(valeurs, 0, n - 1, dp);
}

valeurs privées dfs(int[], int i, int j, int[] dp) {
si (i >= j - 1) retourner 0; // moins de 3 sommets
si (dp[i][j] != -1) retour dp[i][j];

int best = entier.MAX_VALUE;
pour (int k = i + 1; k < j; k++) {
coût int = valeurs[i] * valeurs[j] * valeurs[k]
+ dfs(valeurs, i, k, dp)
+ dfs(valeurs, k, j, dp);
si (coût < le meilleur) le meilleur = coût;
}
dp[i][j] = meilleur;
le meilleur retour;
}
}
«» "

# # # # # #

'`python
Solution de classe:
def minScoreTriangulation(self, valeurs: list[int]) -> Int:
n = len(valeurs)
mémo = [[Aucun] * n pour _ dans l'intervalle(n)]

def dfs(i: int, j: int) -> Int:
i >= j - 1: # < 3 sommets
retour 0
si mémo[i][j] n'est pas Néant:
retour de mémo[i][j]

meilleure = flotteur("inf")
pour k dans la plage(i + 1, j):
Coût = (
valeurs[i] * valeurs[j] * valeurs[k]
+ dfs(i, k)
+ dfs(k, j)
)
best = min (best, coût)

mémo[i][j] = meilleur
le meilleur retour

retour dfs(0, n - 1)
«» "

C'est vrai. C++

'`cpp
#incluez <vecteur>
#incluez <algorithme>
#incluez <limites>

solution de classe {
public:
Int minScoreTriangulation(std::vector<int>& valeurs) {
int n = valeurs.size();
à:vecteur<std::vecteur<int>> dp(n, à:vecteur<int>(n, -1));
retourner dfs(valeurs, 0, n - 1, dp);
}

particulier:
int dfs(const std::vector<int>& v, int i, int j, std::vector<std::vector<int>&dp) {
si (i >= j - 1) retourner 0; // moins de 3 sommets
si (dp[i][j] != -1) retour dp[i][j];

int best = INT_MAX;
pour (int k = i + 1; k < j; ++k) {
coût int = v[i] * v[j] * v[k]
+ dfs(v, i, k, dp)
+ dfs(v, k, j, dp);
best = md::min(best, cost);
}
dp[i][j] = meilleur;
le meilleur retour;
}
};
«» "

---

Analyse de complexité

Technique Temps Espace
- C'est quoi ?
La mémorisation du haut vers le bas (tous les 3 codes) **O(n3)** – Sous-problèmes `O(n2)`, chaque scan `O(n)` fractionne. Autres
Même chose

Avec `n ≤ 50`, l'algorithme s'inscrit facilement dans les limites (=125 000 itérations).

---

Les bons, les mauvais et les méchants

Catégorie
C'est pas vrai.
**Bonne**) • Récurrence intuitive – facile à comprendre. <br>• Ne nécessite que la mémoire `O(n2)`. <br>• Fonctionne pour tous les polygones convexes (pas de cas cachés). Autres
**Le temps est cubique; pour la très grande `n` il deviendrait lourd (bien que `n=50` est très bien). <br>• Le produit `valeurs[i] *valeurs[j] *valeurs[k]` pourrait déborder l'int 32 bits dans les cas extrêmes (si les valeurs étaient plus grandes). Dans les limites du problème officiel ( ''100') il est sûr. Autres
La récurrence du PDD est *pas* évidente pour les novices; ils peuvent penser à la multiplication de la matrice et se confondre. <br>• La mémorisation nécessite une manipulation soigneuse de la base de données (`i >= j-1`). Une faute de frappe entraîne un débordement de la pile ou de mauvaises réponses. <br>• Dans les langues avec de petites plages d'entrée (p. ex. JavaScript), vous devez utiliser BigInt. Autres

**À emporter :** Concentrez-vous sur un cas de base clair, utilisez de longs entiers au besoin et testez les cas de bord (`n=3`, toutes valeurs égales, tableaux ascendants/descendants).

---

## Description du blog optimisé SEO & Meta

**Titre:**
> Triangulation de score minimal de polygone – LeetCode 1039 Python, Solutions C++

**Meta Description:**
> Découvrez comment résoudre le LeetCode 1039 (Triangulation de score minimal de polygone) avec mémoisation top-down. Code Full Java, Python et C++, analyse de complexité et plongée profonde dans les bonnes, mauvaises et laids des solutions DP. (en milliers de dollars)

---

Les pensées finales

- Pourquoi ? Parce que la triangulation optimale d'un sous-polygon dépend uniquement de ses paramètres, un ajustement parfait pour l'intervalle DP.
- **Pourquoi mémorisation?** La récursion maintient le code propre, et la taille du problème (`n ≤ 50`) ne garantit aucun problème de pile.
- **Quand passer au bas vers le haut?** Si vous avez besoin d'éviter la récursion pour des limites de récursion très profondes ou si vous voulez pré-allouer la table DP explicitement.

Avec les extraits de code et l'explication ci-dessus, vous pouvez aborder avec confiance **LeetCode 1039** dans des interviews, des billets de blog ou des concours de codage. Bon codage 