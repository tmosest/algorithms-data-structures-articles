---
titre: LeetCode 1444. Nombre de façons de couper une pizza -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Résoudre le LeetCode 1444 – Nombre de façons de couper une pizza
** Code source complet en Java, Python et C++ + un billet de blog favorable au référencement* *

---

- Oui. 1. Le Code

Ci-dessous vous trouverez trois solutions autonomes prêtes à fonctionner – une pour **Java 17**, **Python 3.10+** et **C++17**.
Tous les trois utilisent la même idée optimale :

* **Matrice préfixe** – nous indique rapidement combien de pommes se trouvent dans n'importe quel sous-rectangle.
* **3-D mémorisé DFS** (`dp[remainingCuts][row][col]`) – compte les façons de couper la pizza qui commence à la cellule `(row, col)` avec un nombre donné de coupures restant.

Texte
Temps : O(k · lignes · cols · (lignes + cols))
espace : O(k · lignes · cols)
«» "

---

- Oui. Java (Java 17)

"Java
Importation de java.util.*;

solution de classe publique {
int final statique privé MOD = 1_000_000_007;

moyen public int(String[] pizza, int k) {
int m = longueur de pizza;
n = pizza[0].longueur();

// Préfixer la somme des pommes: pre[r][c] = pommes dans la sous-matrice (r,c) .. (m-1,n-1)
int[][] pre = nouvelle int[m + 1][n + 1];
pour (int r = m - 1; r >= 0; --r) {
pour (int c = n - 1; c >= 0; --c) {
pre[r][c] = pre[r][c + 1] + pre[r + 1][c] - pre[r + 1][c + 1]
+ (pizza[r].charAt(c) == 'A' ? 1 : 0);
}
}

int[][][] memory = nouveau int[k][m][n];
pour (int[]]a : note)
pour (int[] b : a)
les tableaux.fill(b, -1);

retourner dfs(0, 0, k, pre, mémo);
}

Int dfs (int r, int c, int coupes Gauche,
Int[] [] pre, int[][][] note] {
int m = prélongueur - 1, n = pré[0].longueur - 1;

si [avant] [c]] 0) retourner 0; // pas de pomme dans cette tranche
Si (coupe) 1) retour 1; // dernière pièce doit contenir au moins une pomme

Int &memo Val = mémo[coupes Gauche − 1]r][c];
Si (memoVal != -1) retour mémoVal;

= 0;

// Coupes horizontales
pour (int nr = r + 1; nr < m; ++nr) {
si [avant][c] - avant][c] > 0) { // la partie supérieure a une pomme
ways = (ways + dfs(nr, c, cutsLeft, pre, memo)) % MOD;
}
}

// Coupes verticales
pour (int nc = c + 1; nc < n; + nc) {
si [pré[r]c] - pré[r][nc] > 0) { // la partie gauche a une pomme
ways = (ways + dfs(r, nc, cutsLeft, pre, memo)) % MOD;
}
}

mémoVal = voies;
les voies de retour;
}
}
«» "

---

### Python (Python 3.10+)

'`python
à partir de functools importer lru_cache
de taper l'importation Liste

MOD = 10**9 + 7

Solution de classe:
def ways(self, pizza: List[str], k: int) -> Int:
m, n = len(pizza), len(pizza[0])

# somme préfixe: pré[r][c] = pommes en sous-matrice (r,c) .. (m-1,n-1)
pre = [[0] * (n + 1) pour _ dans la plage (m + 1)]
pour r dans la plage (m - 1, -1, -1):
pour c dans la plage (n - 1, -1, -1):
pré[r][c] = (
Pré[r][c + 1] + pré[r + 1][c] - pré[r + 1][c + 1]
(pizza[r][c] == 'A')
)

@lru_cache(Aucun)
def dfs(r: int, c: int, cuts_left: int) -> Int:
si pré[r][c] == 0: # pas de pomme dans cette pièce
retour 0
if cuts_left == 1: # dernier morceau
retour 1

Res = 0
# coupes horizontales
pour nr dans la plage (r + 1, m):
si pre[r][c] - pre[nr][c] > 0:
res = (res + dfs(nr, c, coupes_gauche - 1)) % MOD

# coupes verticales
pour nc dans la plage(c + 1, n):
si pre[r][c] - pre[r][nc] > 0:
res = (res + dfs(r, nc, cuts_left - 1)) % MOD

retour res

retour dfs(0, 0, k)
«» "

---

### C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
l'état statique du constexpr MOD = 1'000'000'007;

Int ways(vecteur<string>& pizza, int k) {
int m = pizza.size(), n = pizza[0].size();
vecteur<vecteur<int>> pré(m + 1, vecteur<int>(n + 1, 0));

pour (int r = m - 1; r >= 0; --r) {
pour (int c = n - 1; c >= 0; --c) {
pre[r][c] = pre[r][c + 1] + pre[r + 1][c] - pre[r + 1][c + 1]
+ (pizza[r][c]] == 'A' ? 1 : 0);
}
}

vector<vector<vector<int>>> memo(k, vector<vector<int>>(m, vector<int>(n, -1));
retourner dfs(0, 0, k, pre, mémo);
}

particulier:
int dfs(int r, int c, coupes d'int, vecteur const<vector<int>>& avant,
vector<vector<vector<int>>>& memory) {
si [avant] [c]] 0) retourner 0; // pas de pomme
si (coupes) 1) retour 1; // dernière tranche

int& res = mémo[cuts - 1][r][c];
Si (res != -1) retour rés;

res = 0;
int m = pre.size() - 1, n = pre[0].size() - 1;

// coupes horizontales
pour (int nr = r + 1; nr < m; ++nr) {
si [avant][c] - avant][c] > 0) {
res = (res + dfs(nr, c, coupes - 1, pré, mémo)) % MOD;
}
}

// coupes verticales
pour (int nc = c + 1; nc < n; + nc) {
si [pré[r]c] - pré[r][nc] > 0) {
res = (res + dfs(r, nc, coupes - 1, pré, mémo)) % MOD;
}
}

retour rés;
}
};
«» "

---

- Oui. 2. Le blog – Le bon, le mauvais, le mauvais de LeetCode 1444

> **Déverrouillez la solution prête à l'entrevue pour LeetCode 1444 – Nombre de façons de couper une pizza* *
> Maîtriser la programmation dynamique, préfixer les montants et la mémorisation récursive en **Java, Python et C++**.
> Idéal pour la préparation de l'entrevue front-end, back-end et full-stack.

---

Introduction

Si vous préparez des interviews de codage, vous avez probablement rencontré le problème *Pizza Cutting* – LeetCode **1444**.
Le but est simple : couper une pizza rectangulaire en **k** morceaux de sorte que chaque morceau contient au moins une pomme ('A'').
Les coupes peuvent être horizontales ou verticales, et nous comptons toutes les manières distinctes modulo 1 000 000 007.

Pourquoi ce problème est-il une mine d'or pour les intervieweurs?

* Il mélange la programmation dynamique **grid** avec la compression de l'état**.
* Il teste votre capacité à gérer **memoization** et **prefix-sum** des optimisations.
* Il vous force à penser à **conditions limites** (par exemple, quand une pomme est absente).

Laissons tomber **le bon**, **le mauvais**, et **le laid** de résoudre ce problème.

---

## Le bon: propre, lisible et optimisé

Pourquoi ça compte ?
- Oui.
**Prefix-Sum Matrix**= O(1) requête pour les pommes dans tout sous-rectangle. Autres
**3-D Mémoire DP** ('dp[coupes][ligne][col]') Réutilise les résultats, empêchant les explosions exponentielles. Autres
**Coupes de coupe itératives**= Boucles horizontales et verticales droites; pas de frais généraux supplémentaires. Autres
**Modulo Arithmétique À l'intérieur de la boucle**. Autres
**Language-Indépendant Logic** La même approche fonctionne pour Java, Python, C++. Autres
Autres **Complexité du temps \(O(k·rows·cols·(rows+cols))\)**) Répond aux contraintes officielles 30 × 30 × 30. Autres
Autres **Complexité spatiale \(O(k·rows·cols)\)**= Acceptable pour les environnements d'entretien modernes. Autres

À emporter

- **Le prétraitement rapide** (la somme du préfixe) coupe l'espace de recherche de façon spectaculaire.
- **Mémoisation** transforme une récursion naïve de 'O(2^k)' en polynôme.
- **La conception modulaire** (aide DFS séparée) rend le code testable et durable.

---

## Les mauvaises: Naïve Brute-Force, Récursion redondante

Conséquence
C'est pas vrai.
Autres Vérifier chaque coupe *sans* préfixe des sommes.Chaque appel scanne une sous-matrice → **O(rows·cols)** par appel. Autres
Le temps expanentiel, impossible même pour `k=3`. Autres
Autres Oublier le cas de base d'Apple produit des réponses incorrectes pour les cas d'angle. Autres
En utilisant des variables globales en récursion (Python) Autres

**Ligne de bottom** – un *pur DFS* qui scanne la grille sur chaque récursion est un *slow-down* que les intervieweurs vont signaler.

---

- Oui. L'horrible : des cauchemars sur les bords et un jargon trop optimisé

1. **Missing Apples dans la pizza entière**
* La pizza peut contenir **0 pommes** dans certaines rangées/colonnes.
* Vous devez *ignorer* les coupes qui laisseraient un morceau sans pomme; sinon la réponse sera `0`.

2. ** Erreurs hors pair dans l'indexation des préfixes**
* Préfixer les sommes utilise souvent une astuce extra ligne/colonne (`pre[m][c] = 0`).
* Un seul indice mal typé (`pre[r+1][c]` vs `pre[nr][c]`) retourne la logique.

3. **Grand k > 30**
* Si vous allouez naïvement `dp[k][rows][cols]`, vous frapperez **limites de mémoire** pour les entrées plus importantes.
* L'astuce est d'indexer `dp` par **cuts gauche** (`k-1`) – il reste minuscule.

4. **Manipulation du module en C++**
* Oublier d'appliquer `% MOD` à l'intérieur de la boucle peut déborder `int`.
* Javas `int` est 32-bit; Python=s `int` est débordé, mais vous avez encore besoin de `% MOD` pour les performances.

---

### Aperçu de l'entrevue dans le monde réel

> **Les intervieweurs demandent souvent**: Pouvez-vous prouver pourquoi ce DP est correct?
> Expliquez que chaque état `(cuts, r, c)` représente un **unique sous-pizza** (celui qui commence à la cellule `(r, c)` et s'étend vers le bas à droite).
> Toute coupe valide de cet état divise la sous-pizza en deux sous-rectangles; la partie supérieure/gauche doit contenir au moins une pomme, garantissant que la partie inférieure/droite peut être manipulée de façon récursive.

---

## Solution étape par étape

1. **Construire le préfixe-sum**
* Pour chaque cellule `(r, c)`, calculer les pommes dans le sous-réseau **sud-est**.
* Formule:
«« pre[r]c] = pre[r][c+1] + pre[r+1]c] - pre[r+1][c+1] + (pizza[r]c] == «A»»;» "

2. **Récursifs DFS + mémorisation**
* Cas de base 1: "pré[r][c] == 0` → retourner 0 (pas de pomme).
* Cas de base 2 : < < coupes > > Gauche == 1` → retour 1 (la tranche restante contient déjà une pomme).
* Recherche Memo ('dp[cutsLeft-1][r][c]').
* Essayez chaque coupe horizontale possible (`nr > r`) où la tranche supérieure a une pomme**.
* Essayez chaque coupe verticale possible (`nc > c`) où la tranche ** gauche a une pomme**.
* Calculer les résultats modulo `1_000_000_007`.

3. **Retour** le résultat de l'appel racine (`dfs(0, 0, k)`).

Les extraits de code ci-dessus implémentent exactement cet algorithme.
Les versions **Java** et **C++** utilisent des tableaux 3-D explicites pour mémoriser, tandis que **Python** s'appuie sur `functools.lru_cache` pour une mémorisation transparente.

---

## Comment utiliser ces solutions dans les entrevues

1. ** Expliquer l'idée d'abord** – parler de préfixe des sommes et de mémoisation.
2. **Afficher l'état** – montrer «dp[remainingCuts][row][col]».
3. **Pseudocode** – écrire les boucles pour les coupes horizontales et verticales.
4. **Edge Cases** – demandez à l'intervieweur comment vous traitez la situation de la pomme.
5. **Mise en oeuvre** – codez la solution dans la langue avec laquelle vous êtes le plus à l'aise (Java, Python ou C++).

---

Questions d'entrevue courantes tirées de 1444

Question: Compétences de base testées
-- -- -- -- -- -- -- -- --
Autres Que faire si `k` est plus grand que le nombre de pommes? Le raisonnement de la frontière et la preuve de la justesse. Autres
Autres Comment modifier l'algorithme pour les coupures de 4 directions ? Généralisation et exploration d'État. Autres
Autres Pouvez-vous traiter la grille différemment? D'autres structures de données (BIT, Segment Trees). Autres
Autres Pourquoi le préfixe est-il orienté vers le coin inférieur droit? Optimisation pour toutes requêtes de sous-rectangle. Autres

---

- Oui. L'Ugly: Déboguer les erreurs et les performances Pièges

1. **Off‐by‐One dans les indices préfixes** – mène à un nombre incorrect de pommes.
2. **Missing le cas de base de la pomme de l'Ombre** – compte les tranches invalides.
3. **Utiliser un `int` en Python pour la profondeur de récursion** – mène à `RecursionError`.
4. **Facile de mod après chaque ajout** – déborde en Java/C++ et mauvais résultats.
5. ** Mémoire excessive** – l'attribution de `dp[k][rows][cols]` sans le décalage `-1` peut causer `StackOverflowError` en Java.

---

- Oui. 3. Pourquoi ce blog est votre avantage dans l'entrevue

* **L'en-tête favorable au référencement** – Code Leet 1444 – Nombre de façons de couper une pizza apparaît dans les requêtes de recherche de milliers de demandeurs d'emploi.
* **Multi-langue Showcase** – Les managers d'embauche adorent voir les candidats à l'aise avec **Java**, **Python** et **C++**.
* **Narratif de résolution des problèmes** – La structure « Good/Bad/Ugly » démontre votre *meta-pensing* – un trait d'entrevue clé.

---

Mot final

Mastering LeetCode 1444 est plus qu'un simple code d'écriture ; il s'agit de construire une solution robuste, efficace et claire que vous pouvez discuter avec les intervieweurs en toute confiance.
Utilisez les extraits ci-dessus comme votre *ready-reference* et le blog pour répéter votre *storytelling* lors d'entretiens pratiques.

Bon codage, et bonne chance avec votre prochaine interview!