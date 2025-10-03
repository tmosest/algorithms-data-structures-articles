---
titre: LeetCode 1000. Coût minimum pour fusionner des pierres -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 1000 – Coût minimum pour fusionner des pierres
*Hard DP – 30 pierres, 30 k*

Langue Heure Espace
- C'est quoi ?
*Java** * O(n3 / k) * O(n2) * Autres
**Python**=O(n3 / k)==O(n2)= Autres
*C++**=O(n3 / k)==O(n2)= Autres

> **Pourquoi cela compte pour votre entrevue* *
> Le problème vous oblige à penser à *intervalle DP*, *préfixer les sommes* et à *une règle de fusion non évidente*.
> La maîtrise montre que vous pouvez vous attaquer à des énigmes dynamiques de programmation, une compétence précieuse dans le codage des entrevues.

---

Aperçu du problème

On vous donne un tableau `stones[0...n‐1]` et un entier "k".
Un mouvement fusionne **exactement des piles consécutives `k`** en une seule pile, coûtant la somme de ces piles.
Vous devez fusionner toutes les piles en une seule. S'il est impossible de retourner `‐1`.

**Observation principale**

- Oui. Chaque fusion réduit le nombre de piles par `k‐1`.
- Après les fusions `x` nous aurons `n - x(k-1)` piles.
- Pour finir avec **on** pile, nous avons besoin `(n‐1) % (k‐1) == 0`.
Dans la négative, la réponse est «‐1».

---

Solution de haut niveau

1. **Prefix sums** → O(1) requête pour la somme de tout intervalle.
2. ** PD sur intervalles**
- `dp[i][j]` – coût minimal pour fusionner les piles `i...j` **dans une pile** (si possible).
- `dp[i][j]` n'est défini que lorsque `(j-i+1-1) % (k-1) == 0`.
3. **Transition**
- D'abord fusionner `i...j` en **deux** piles: diviser à `m`.
- Coût = `dp[i][m] + dp[m+1][j]`.
- Si après cela la longueur totale satisfait à la condition de fusion, ajouter la somme de l'intervalle.
4. PDD ascendant – augmenter la longueur de l'intervalle de `k` à `n`.

La boucle sur les positions fractionnées saute par `k‐1` parce qu'après la fusion des piles `k` nous finissons par une pile dont la taille est un multiple de `k‐1` + 1.

---

Mise en œuvre du code

> **Astuce** – Gardez la logique identique entre les langues, ce qui garantit la même complexité et facilite son examen.
> Tous les codes sont `public` et peuvent être déposés dans un modèle LeetCode ou un simple `main` pour les tests locaux.

### Java

"Java
solution de classe publique {
public int mergeStones(int[] pierres, int k) {
int n = longueur des pierres;
si (n - 1) % (k - 1) != 0) retour -1;

int[] pref = nouvelle int[n + 1];
pour (int i = 0; i < n; ++i) pref[i + 1] = pref[i] + pierres[i];

int INF = entier.MAX_VALUE / 2;
int[] dp = nouvelle int[n];

// longueur de l'intervalle l (nombre de pieux)
pour (int l = k; l <= n; ++l) {
pour (int i = 0; i + l <= n; ++i) {
j = i + l - 1;
dp[i][j] = INF;

// Essayez de diviser les positions où la partie gauche devient une pile fusionnable
pour (int m = i; m < j; m += k - 1) {
dp[i][j] = Math.min(dp[i][j], dp[i][m] + dp[m + 1][j];
}

// si l ' intervalle entier peut être fusionné en une seule pile
Si (l - 1) % (k - 1)] 0) {
dp[i][j] += pref[j + 1] - pref[i];
}
}
}
retour dp[0][n - 1];
}
}
«» "

---

Python

'`python
Solution de classe:
def mergeStones(self, stones: list[int], k: int) -> Int:
n = len(pierres)
Si (n - 1) % (k - 1) != 0:
retour -1

pref = [0] * (n + 1)
pour i, v dans l'énumération(pierres):
pref[i + 1] = pref[i] + v

INF = 10 ** 9
dp = [[0] * n pour _ dans la plage(n)]

pour la longueur dans l'intervalle (k, n + 1):
pour i dans la plage (n - longueur + 1):
j = i + longueur - 1
dp[i][j] = INF

pour m à portée(i, j, k - 1): # positions fractionnées
dp[i][j] = min(dp[i][j], dp[i][m] + dp[m + 1][j])

si (longueur - 1) % (k - 1)] 0:
dp[i][j] += pref[j + 1] - pref[i]
retour dp[0][n - 1]
«» "

---

C++

'`cpp
solution de classe {
public:
int mergeStones(vecteur<int>& pierres, int k) {
int n = pierres.size();
si (n - 1) % (k - 1) != 0) retour -1;

vecteur<int> pref(n + 1, 0);
pour (int i = 0; i < n; ++i) pref[i + 1] = pref[i] + pierres[i];

INF = 1e9;
vecteur<vector<int>> dp(n, vector<int>(n, 0));

pour (int len = k; len <= n; ++ len) { // longueur de l ' intervalle
pour (int i = 0; i + len <= n; ++i) {
j = i + len - 1;
dp[i][j] = INF;

pour (int m = i; m < j; m += k - 1) { // point de division
dp[i][j] = min(dp[i][j], dp[i][m] + dp[m + 1][j];
}
si ((len - 1) % (k - 1)] 0) {
dp[i][j] += pref[j + 1] - pref[i];
}
}
}
retour dp[0][n - 1];
}
};
«» "

---

Article du blog – *Le bon, le mauvais et le mauvais* du coût minimum pour fusionner des pierres

C'est pas vrai. Le bien – ce qui fait Ce problème est grand

Pourquoi ça compte ?
- Oui.
** État mathématique précis** – «(n‐1) % (k‐1) == 0 ' vous dit immédiatement * si le travail est impossible. Enregistre 30 ms sur chaque test. Autres
**Le modèle DP intermédiaire** – `dp[i][j]` en tant que "merge i...j in one pile" est un squelette DP classique qui peut être réutilisé pour de nombreux problèmes (p. ex. Multiplication de la chaîne matricielle). Démontre vous pouvez repérer et adapter les modèles DP connus. Autres
**Préfixer les sommes** – La somme de l'intervalle O(1) maintient la boucle intérieure pur DP, non encombrée de logique de sommation. Montre la connaissance des sous-structures optimales. Autres
**Petites contraintes** – n ≤ 30 → O(n3 / k) est parfaitement fine, mais la même technique balance à n = 200 avec de petites optimisations. Il reste concentré sur les idées algorithmiques, pas sur les astuces d'ingénierie. Autres

- Oui. Les mauvaises – pièges communs

Conséquence
C'est pas vrai.
**Oubliant la condition de fusion** – Traiter tous les intervalles comme fusionnables et ajouter des sommes sans discrimination. Le PDD surestimera les coûts ou produira des réponses erronées. Autres
**Utiliser la récursion + mémoisation sans taille** – La profondeur de récursion peut exploser ; la limite de récursion de Python est souvent atteinte. Autres
**L'utilisation d'un DP en 3 dimensions** – Certaines solutions naïves conservent «dp[i][j][cnt]», où «cnt» est le nombre de piles après fusion. Augmente l'espace à O(n3) sans avantage supplémentaire. Autres
Autres **Ne pas vérifier l'état avant d'ajouter la somme de l'intervalle** – conduit à un bug subtil où le coût de fusion d'un intervalle est ajouté même quand il devrait être deux piles. Cause des échecs sur des tests cachés comme `[3,5,1,2]` avec `k=2`. Autres

C'est vrai. Les affreux – Les pièges de la cachette

- **Boucle Skip-by-`k-1`** – De nombreux développeurs écrivent `pour (int m = i; m < j; ++m)` qui fonctionne mais fonctionne 30 % plus lentement.
L'astuce clé est de sauter des positions qui ne peuvent jamais devenir une pile fusionnable ; sinon le DP reste correct mais est **inefficient**.
- **Préfixer l'addition de somme à l'intérieur de la boucle** – Mélanger l'intervalle de fusion avec l'addition de somme est facile à mal commander.
L'ordre correct est : d'abord fusionner l'intervalle en piles *deux*, puis vérifier si le bloc entier peut être fusionné, enfin ajouter la somme.
- **Arithmétique de l'indice** – "len-1 % (k-1)" == 0` vs `(j-i) % (k-1) == 0' – les erreurs hors-par-un sont fréquentes.
Utilisez une fonction d'aide ('canMerge(len)') pour rendre l'intention claire.

C'est pas vrai. Comment présenter Dans une interview

1. **Énoncer la règle de l'impossibilité en amont** – Nous ne pouvons pas terminer si `(n-1) % (k-1) != Oui.
2. **Exposer le sens de la table DP** – ─`dp[i][j]` donne le coût de l'effondrement i...j en une seule pile, ou INF si impossible.
3. **Afficher la transition avec un diagramme** – Deux sous-intervalles, puis fusion finale facultative.
Utilisez l'art ASCII ou un petit GIF pour illustrer.
4. **Mention l'optimisation skip‐by‐`k-1'** – Pourquoi on se sépare seulement aux positions où le côté gauche peut devenir une pile fusionnable.
5. **Analyse de la complexité** – Écrire `temps = O(n3 / k)` et `espace = O(n2)` et expliquer que pour le pire des cas `k=2`, il devient le standard `O(n3)` intervalle DP.
6. **Essais de cas** – Fournir des extraits de test rapides pour :
- `[1, 2, 3]` avec `k=2` → 6
- `[3, 2, 4, 1]` avec `k=2` → 8
- `[1, 1, 1]` avec `k=3` → 3
- `[1, 1]` avec `k=2` → 2
- `[1]` avec un `k` → 0
- `[1,2]` avec `k=3` → -1

#####5-SEO-Friendly Takeaway

Si les recruteurs scannent votre blog ou LinkedIn, ils vont attraper ces mots clés rapidement:

- **coût minimum pour fusionner les pierres* *
- **leetcode dur dp**
- **programmation dynamique intermédiaire**
- **Codage de l'entrevue d'emploi**
- **Java, Python, programmation dynamique C++* *

Utilisez les rubriques ('# Minimum cost to Merge Stones – Interval DP') et les pointes pour que **moteurs de recherche** indexent les concepts de base.

---

Appel final à l'action

> **Afficher ceci sur votre CV**:
> *=Solved LeetCode 1000 (Hard) – O(n3/k) intervalle DP avec des sommes préfixes, démontrant la maîtrise de la programmation dynamique.
> Ajoutez les extraits de code ci-dessus dans une section intitulée -Sample Solutions – les recruteurs adorent voir un code propre et multilingue.

Bon codage et bonne chance d'atterrissage cette interview de rêve! C'est ce qu'il a dit