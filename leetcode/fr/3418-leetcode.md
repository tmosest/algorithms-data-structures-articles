---
titre: LeetCode 3418. Montant maximum d'argent Robot peut gagner - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Récapitulation des problèmes – LeetCode 3418: *La quantité maximale de l'argent Robot peut gagner*

**Objectif**
Un robot commence à `(0,0)` et se déplace seulement **à droite** ou **à bas** pour atteindre `(m‐1, n‐1)` dans une grille `m × n` `coins`.
* `coins[i][j] ≥ 0` → le robot **gains** que beaucoup de pièces.
* `coins[i][j] < 0` → un voleur vole `=coins[i][j]=".
Le robot peut neutraliser les voleurs en ** au plus deux cellules** sur son chemin, empêchant ces vols.

Retourne le total **maximum** des pièces que le robot peut collecter (le total peut être négatif).

> **Constraints**
> «1 ≤ m, n ≤ 500»
> `-1000 ≤ pièces[i][j] ≤ 1000`

---

Pourquoi ce problème est-il un savoir-faire pour les entrevues d'emploi

* ** PD sur la grille 2-D** – un modèle d'entrevue classique.
* **Ressource limitée (2 neutralisations)** – montre comment ajouter une dimension supplémentaire à DP.
* ** Grande entrée** (`500×500`) – teste votre capacité à gérer le temps et la mémoire.

Si vous pouvez expliquer clairement cette solution dans une interview, vous montrerez la maîtrise de la programmation dynamique et la résolution de problèmes – un énorme plus pour tout rôle d'ingénierie logiciel.

---

Aperçu de la solution

1. **État**
`dp[i][j][k]` – pièces maximales qui peuvent être collectées lorsque le robot se trouve à la cellule `(i,j)` ayant utilisé exactement `k` neutralisations (`k = 0, 1, 2`).

2. **Transition**
À partir de `(i-1,j)` ou `(i,j-1)` nous pouvons
* ** Déplacer sans utiliser** un neutraliseur:
«dp[i][j][k] = max(dp[i][j][k], dp[prev][k] + pièces[i][j]»
* ** Déplacer et utiliser** un neutraliseur sur la cellule actuelle (si `k > 0`):
`dp[i][j][k] = max(dp[i][j][k], dp[prev][k-1] + (coins[i][j] >= 0 ? pièces[i][j] : 0)»
(Lorsque nous neutralisons, une valeur négative est traitée comme « 0 ».

3. **Initialisation**
«dp[0][0][0] = pièces[0][0]»
Si `coins[0][0] < 0`, nous définissons également `dp[0][0][1] = 0` (neutralisant le premier braqueur).

4. **Réponse**
"max(dp[m-1][n-1][0], dp[m-1][n-1][1], dp[m-1][n-1][2]) "

5. **Complexités**
*Temps* – "O(m × n × 3)" – "O(mn)" – rapide pour 500×500.
*Espace* – «O(m × n × 3)» - «O(mn)» (~ 4 Mo).
Nous pouvons également réduire à 2 lignes (`O(2 × n × 3)`), mais le tableau 3-D complet garde le code simple.

---

Mise en œuvre du code

Voici des implémentations claires et bien commentées dans **Java, Python et C++**.
N'hésitez pas à les copier dans votre IDE et à effectuer vos propres tests.

####==# Java (style LeetCode)

"Java
solution de classe {
Int maximum Montant(int[][] pièces) {
m = pièces de monnaie, n = pièces de monnaie[0];
Int final NEG = entier.MIN_VALUE / 4; // sentinelle négative sûre

// dp[i][j][k] : max pièces à (i,j) après utilisation de neutralisations k
int[][] dp = nouveau int[m][n][3];
pour (int i = 0; i < m; i++)
pour (int j = 0; j < n; j++)
pour (int k = 0; k < 3; k++)
dp[i][j][k] = NEG;

// Démarrer la cellule
dp[0][0][0] = pièces[0][0];
si (coins[0][0] < 0) dp[0][0][1] = 0; // neutraliser le premier braquage

pour (int i = 0; i < m; i++) {
pour (int j = 0; j < n; j++) {
Si (i) 0 && j) 0) continuer; // déjà initialisé

pour (int k = 0; k < 3; k++) {
// depuis le haut
si (i > 0) {
// 1. déplacer sans neutralisation
dp[i][j][k] = Math.max(dp[i][j][k],
dp[i-1][j][k] + pièces[i][j];

// 2. déplacer et neutraliser cette cellule
si (k > 0) {
Int val = dp[i-1][j][k-1];
val += (coins[i][j] >= 0) ? pièces[i][j] : 0;
dp[i][j][k] = Math.max(dp[i][j][k], val);
}
}

// de gauche
si (j > 0) {
dp[i][j][k] = Math.max(dp[i][j][k],
dp[i][j-1][k] + pièces[i][j];

si (k > 0) {
Int val = dp[i][j-1][k-1];
val += (coins[i][j] >= 0) ? pièces[i][j] : 0;
dp[i][j][k] = Math.max(dp[i][j][k], val);
}
}
}
}
}

retour Math.max(dp[m-1][n-1][0],
b) Math.max(dp[m-1][n-1][1], dp[m-1][n-1][2]);
}
}
«» "

---

Python 3

'`python
Solution de classe:
def maximum Montant(même, pièces: Liste[Liste[int]]) -> Int:
m, n = len(coins), len(coins[0])
NEG = -10**15

dp = [[[NEG] * 3 pour _ dans l'intervalle(n)] pour _ dans l'intervalle(m)]

Première cellule
dp[0][0][0] = pièces[0][0]
si les pièces[0][0] < 0:
dp[0][0][1] = 0 # neutraliser le premier braqueur

pour i dans la plage (m):
pour j dans la plage(n):
Si i == 0 et j == 0:
poursuivre

pour k dans la plage(3):
# du haut
i > 0:
dp[i][j][k] = max(dp[i][j][k],
dp[i-1][j][k] + pièces[i][j])
si k > 0:
val = dp[i-1][j][k-1] + \
(pièces [i][j] si pièces [i][j] >= 0 autre 0)
dp[i][j][k] = max(dp[i][j][k], val)

# de gauche
si j > 0:
dp[i][j][k] = max(dp[i][j][k],
dp[i][j-1][k] + pièces[i][j])
si k > 0:
val = dp[i][j-1][k-1] + \
(pièces [i][j] si pièces [i][j] >= 0 autre 0)
dp[i][j][k] = max(dp[i][j][k], val)

retour max(dp[m-1][n-1])
«» "

---

C++ (style LeetCode)

'`cpp
solution de classe {
public:
Int maximum Montant(vecteur<vecteur<int>> et pièces) {
int m = pièces.size(), n = pièces[0].size();
const int NEG = -1e9; // sentinelle négative sûre

// dp[i][j][k] – pièces max à (i,j) après utilisation de neutralisations k
vector<vector<array<int,3>>> dp(m, vector<array<int,3>>(n, {NEG,NEG,NEG});

dp[0][0][0] = pièces[0][0];
si (coins[0][0] < 0) dp[0][0][1] = 0; // neutraliser le démarrage

pour (int i = 0; i < m; ++i) {
pour (int j = 0; j < n; ++j) {
Si (i) 0 && j) 0) continuer; // déjà init

pour (int k = 0; k < 3; ++k) {
// depuis le haut
si (i > 0) {
dp[i][j][k] = max(dp[i][j][k],
dp[i-1][j][k] + pièces[i][j];

si (k > 0) {
Int val = dp[i-1][j][k-1];
val += (coins[i][j] >= 0 ? pièces[i][j] : 0);
dp[i][j][k] = max(dp[i][j][k], val);
}
}

// de gauche
si (j > 0) {
dp[i][j][k] = max(dp[i][j][k],
dp[i][j-1][k] + pièces[i][j];

si (k > 0) {
Int val = dp[i][j-1][k-1];
val += (coins[i][j] >= 0 ? pièces[i][j] : 0);
dp[i][j][k] = max(dp[i][j][k], val);
}
}
}
}
}

retour max({dp[m-1][n-1][0], dp[m-1][n-1][1], dp[m-1][n-1][2]};
}
};
«» "

> **Astuce** – Si vous voulez raser la mémoire, remplacez `dp` par deux lignes (`dp[2][n][3]`) et roulez les indices.

---

Ce qui fait cette solution

Catégorie
C'est quoi ?
**Correctivité Le DP couvre toutes les utilisations possibles des neutraliseurs. Autres
**Efficacité du temps**= ~ 750 k opérations pour 500×500 – facilement en dessous de 0,1 s sur LeetCode.=== Les solutions Brute-force `O(3^mn)` ou `O(mn2)` ont touché le TL. Autres
**Memory-Footprint**= 4 Mo (complète tableau 3-D) – bien en dessous de la limite de LeetCode=256 Mo.===_______________________________________________________________________________________________________________________________________________________________________________________________________________________ Autres
**Échelle** Le DP peut être réduit à **deux lignes** (`O(2×n×3)`) pour des environnements extrêmement perturbés par la mémoire. Autres

---

Les pièces d'Ugly – Pièges communs à éviter

1. ** Récursion profonde sans mémoisation** – obtient un *RuntimeError* ou un *Time Limit dépassé* dans Python/LeetCode.
2. **Le stockage de quatre entiers par cellule** (`k=0,1,2`) dans un gigantesque vecteur 3-D et sans élagage conduit à ~ 1 Go de mémoire (en langues avec des frais élevés).
3. **Éviter de neutraliser une cellule négative** – vous manquerez le budget de 2-neutralisation et retournerez une réponse sous-optimale.

**Ligne de bottom:** S'en tenir au PDD 3-D décrit ci-dessus ; il est simple, rapide et démontre une logique claire à un intervieweur.

---

Bonus : un harnais d'essai (Python)

'`python
si __nom__ == "__main__" :
s = Solution()
print(s.maximumMontant([[0, 1], [-2, -3]]) # → 1
print(s.maximumMontant([[[1, -5], [0, 2]])) # → 3
# Ajoutez vos propres grilles ici !
«» "

---

Prêt pour l'entretien ?

* Passez par la définition de l'état **** ('dp[i][j][k]').
* Expliquez la logique **de transition** – surtout l'affaire "use a neutraliser".
* Mettez en avant l'astuce **initialisation** pour la première cellule.
* Mentionnez l'échange **temps/espace** et l'optimisation possible de 2 lignes.
* Montrez l'un des extraits de code propre et soyez prêt à **debug** sur place.

Si vous pouvez le faire, vous avez prouvé que vous comprenez la programmation dynamique, les contraintes en matière de ressources et la gestion à grande échelle des entrées – toutes les compétences que les recruteurs recherchent chez un ingénieur logiciel senior. C'est ce qu'il a dit.

Bon codage ! Les