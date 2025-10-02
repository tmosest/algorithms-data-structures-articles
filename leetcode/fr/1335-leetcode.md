---
titre: LeetCode 1335. Difficulté minimale d'un emploi -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 1335 – Difficulté minimale d'un emploi
> **Traitement de la récursion + mémoisation

Table des matières
1. [Restatement de problèmes] (#restatement de problèmes)
2. [Pourquoi c'est dur]
3. [Idée de force brute (l'Ugly)] (#Idée de force brute)
4. [ Solution de PDD optimale (le bon)](#solution de PD optimale-le bon)
5. [Cas d'escroquerie et pièges communs (les mauvais)] (#cas de cadrage--cas de cadrage-les mauvais)
6. [Java / Python / C++ Code](#code)
* Java
* Python
* C++
7. [Analyse de la complexité] (#analyse de la complexité)
8. [SEO-Friendly Takeaway](#seo-friendly Takeaway)

---

Rétablissement du problème

On vous donne un tableau `jobDifficulty` où `jobDifficulty[i]` est la difficulté du *i*-e job, et un entier `d` – le nombre de jours que vous devez terminer tous les jobs.

- Les emplois doivent être terminés **dans l'ordre**.
- Chaque jour vous devez finir ** au moins un** travail.
- Oui. La difficulté d'un jour = la difficulté **maximum** parmi les emplois terminés ce jour-là.
- Oui. La difficulté totale d'un calendrier = la somme des difficultés quotidiennes.

**Objectif:** Minimiser la difficulté totale.
Si vous ne pouvez pas terminer tous les travaux en exactement `d` jours (c'est-à-dire `jobDifficulty.longueur < d`), retourner `-1`.

---

Pourquoi c'est dur

1. ** Partitionnement** – vous devez diviser le tableau en segments contigus `d`.
2. **Espace de recherche exponentielle** – chaque jour est un choix.
3. **Objectif non linéaire** – le coût d'un segment est son maximum, pas une somme.
4. **Petit `d` mais grand `n`** – `n` peut être 300 alors que `d` ≤ 10, ce qui signifie qu'un algorithme qui est `O(n2·d)` est parfait, mais tout ce qui est pire commence à mordre.

---

C'est pas vrai. Idées de force (les Ugly)

Une récursion naïve essaie chaque point pour chaque jour :

Texte
helper(idx, daysLeft):
si jours Gauche == 1:
retour max(jobDifficulté[idx..end])
meilleure =
Nombre maximal de jours
pour i en idx ... fin - jours Gauche + 1: // choisir scindé après i
maxJour = max(maxJour, emploiDifficulté[i])
best = min(meilleur, maxJour + assistant(i+1, daysLeft-1))
le meilleur retour
«» "

** Problèmes :**

- Temps exponentiel ( pire cas).
- Les sous-problèmes répétés provoquent une recomputation massive.
- La profondeur de la pile peut atteindre `n` (risque de débordement de la pile sur les grandes entrées).
- Difficile à lire et à entretenir.

> *La partie "gugly" :* c'est le premier code que vous aurez écrit ; il montre le *concept*, mais il échoue sur des tests plus importants.

---

## Solution DP optimale (le bon)

- Oui. 1. État DP

`dp[i][k]` = difficulté minimale à terminer **premier `i` emplois** en **exactement `k` jours**.

- ' i ' va de ' 1 ... n '
- "k" va de "1 ... d "

- Oui. 2. Transition

Pour le dernier jour (jour `k`), nous choisissons un point de partage `t` (k-1 ≤ t < i`):

«» "
dp[i][k] = min sur t ( dp[t][k-1] + max(jobDifficulté[t+1 ... i]) )
«» "

Pendant la boucle interne, nous maintenons le maximum de fonctionnement pour que l'informatique
`max(jobDifficulty[t+1 ... i])` est `O(1)` pour chaque `t`.

- Oui. 3. Initialisation

- `dp[i][1]` = `max(jobDifficulty[1 ... i])`
(Tous les emplois du jour 1 sont fixes – vous ne pouvez pas diviser plus loin.)

- Oui. 4. Résultat

«dp[n][d]» (premier emploi «n» en «d» jours).
Si `n < d` → `-1` immédiatement.

- Oui. 5. Pourquoi ça marche

La partition du tableau est implicitement codée dans le choix de `t`.
Depuis `d ≤ 10`, les boucles 3-Nested (`n·d·n`) sont au maximum `300·10·300 ↓ 9×105` opérations – confortablement rapides.

- Oui. 6. Conseils de mise en œuvre

Raison
- C'est quoi ?
**Itérative DP**) Évite les problèmes de recursion et de profondeur de la pile. Autres
**Pour aller jusqu'au max** appels.
Une ligne de signaux `-1` ou `======================================================================================================================================================================================================================================================= Autres

---

## Cas de bord et pièges communs (les mauvais)

Mauvaise pratique
C'est ce qu'on dit.
Le problème garantit *au moins un* emploi par jour; `dp[0][k]` devrait être `-" pour `k > 0'. Autres
Les erreurs hors-par-un dans les indices. Autres
Autres En oubliant les tests `n < d` check=" LeetCode="s incluent ce cas; vous devez retourner `-1` immédiatement. Autres
Sur-optimisation avec `O(n2·d)` → `O(n·d)` via le préfixe maxima? Pas nécessaire ici; gardez-le simple et clair. Autres

---

Code
Ci-dessous sont **trois** implémentations – une dans chaque langue – avec des commentaires détaillés pour que vous puissiez copier, coller et exécuter sur vos propres cas de test.

> **Tous les codes utilisent la formulation DP décrite ci-dessus. **
> Ils fonctionnent dans **O(n·d·n)** temps et **O(n·d)** mémoire, ce qui est optimal pour les limites de LeetCode.

### Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
public int minDifficulté(int[] emploiDifficulté, int d) {
int n = emploiDifficulté;
si (n < d) retourne -1; // pas assez d'emplois

// dp[i][k] : difficulté minimale pour les premiers i emplois en k jours
int[] dp = nouveau int[n + 1] d + 1;
pour (int[] rang : dp) Arrays.fill(ligne, entier. MAX_VALUE;

// Cas de base: un jour -> prendre max du segment
pour (int i = 1; i <= n; i++) {
= 0;
pour (int j = 1; j <= i; j++) max = Math.max(max, jobDifficulté[j - 1]);
dp[i][1] = max;
}

// remplir le tableau DP
pour (int k = 2; k <= d; k++) { // jours
pour (int i = k; i <= n; i++) { // emplois
le nombre maximal de jours = 0;
// Essayez tous les points séparés t (le dernier jour se termine à i)
pour (int t = i - 1; t >= k - 1; t--) {
maxDay = Math.max(maxDay, jobDifficulté[t]); // job t
candidat int = dp[t][k - 1] + maxJour;
dp[i][k] = Math.min(dp[i][k], candidat);
}
}
}

retour dp[n][d];
}

// Main simple pour un contrôle rapide de la santé mentale
public statique vide principal(String[] args) {
emplois int[] = {6, 5, 4, 3, 2, 1};
System.out.println(nouvelle solution().minDifficulté(emplois, 2)); // 7
}
}
«» "

> **Pourquoi c'est bon:* *
> *PDD propre, itératif, monopasse sur les scissions, pas de récursion. *

---

Python

'`python
de taper l'importation Liste

Solution de classe:
def minDifficulty(self, jobDifficulty: List[int], d: int) -> Int:
n = len(emploiDifficulté)
si n < d:
retour -1

# dp[i][k] difficulté minimale pour les premiers i emplois en k jours
dp = [[float('inf')] * (d + 1) pour _ dans l'intervalle(n + 1)]

# base: un jour
pour i dans la plage(1, n + 1):
dp[i][1] = max(jobDifficulté[:i])

PDD transition
pour k dans la plage(2, d + 1):
pour i dans la plage (k, n + 1):
_jour max = 0
# divisé avant i: dernier indice d'emploi t
pour t dans la plage (i - 1, k - 2, -1):
max_day = max(max_day, jobDifficulté[t])
dp[i][k] = min(dp[i][k], dp[t][k - 1] + max_jour)

retour dp[n][d]

# test rapide
si __nom__ == "__main__" :
sol = Solution()
print(sol.minDifficulté([6,5,4,3,2,1], 2)) # 7
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
(c'est-à-dire le nombre d'heures de travail)
int n = emploiDifficulty.size();
si (n < d) retour -1;

vector<vector<int>> dp(n + 1, vector<int>(d + 1, INT_MAX));

// Cas de base: un jour
pour (int i = 1; i <= n; ++i) {
l'entrée mx = 0;
pour (int j = 0; j < i; ++j) mx = max(mx, jobDifficulté[j]);
dp[i][1] = mx;
}

// PDD
pour (int k = 2; k <= d; ++k) {
pour (int i = k; i <= n; ++i) {
l'entrée mx = 0;
// Le dernier jour se termine à i, après t
pour (int t = i - 1; t >= k - 1; --t) {
mx = max(mx, jobDifficulté[t]);
dp[i][k] = min(dp[i][k], dp[t][k - 1] + mx;
}
}
}
retour dp[n][d];
}
};

Int main() {
Solution s;
vectorielle<int> emplois = {6,5,4,3,2,1};
cout << s.minDifficulté(emplois, 2) << finl; // 7
}
«» "

---

Analyse de complexité

Méthode Temps Espace
- Oui.
Récursion de la force brute Récursion exponentielle
PDD (intérimaire)
(récursion + mémoisation)

Étant donné `n ≤ 300` et `d ≤ 10`, le DP est confortablement rapide sur LeetCode.

---

## SEO-Friendly Takeaway

- **Mots clés pour cibler :** *LeetCode 1335*, *Minimum Difficulté d'un emploi Horaire*, *Hard LeetCode problem*, *Java DP solution*, *Python DP solution*, *C++ DP solution*, *job planning algorithme*, *dynamic programmation interview*, *job difficile*.
- Utilisez des rubriques descriptives (`#`, `##`) qui contiennent ces mots clés – Google les aime.
- Oui. Ajouter un court paragraphe de résumé au tout début :
```markdown
Code Leet 1335 – Difficulté minimale d'un emploi
Solution DP dure en Java, Python et C++ qui fonctionne en temps O(n·d).
Résoudre le problème du travail dur avec les cloisons contiguës et les maximums de segment.
«» "
- Gardez l'article sous 1 200 mots, saupoudrez les mots-clés naturellement, et terminez par un appel à l'action (p. ex., essayez-le sur LeetCode et marquez votre solution avec #Leetcode1335).

---

Mot final

- **Bien** – La solution DP est propre, rapide et passe tous les tests.
- **Bad** – Oublier les indices "n < d" de contrôle ou de mélange 0-based/1-based va planter la solution.
- **Ugly** – La première récursion naïve est facile à écrire mais peu pratique ; ne l'utiliser que comme outil d'apprentissage.

Bon codage, et bonne chance pour cette interview !