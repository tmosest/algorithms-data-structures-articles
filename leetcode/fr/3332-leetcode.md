---
titre: LeetCode 3332. Points maximums Tourist peut gagner - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 3332 – Points maximaux Les touristes peuvent gagner
C++ – Tout le code dont vous avez besoin
Billet de blog – Les bons, les mauvais et les méchants (friendly SEO)

---

Récapitulation des problèmes

> **Vous êtes donné**
> * `n` – nombre de villes (graphique entièrement connecté)
> * `k` – nombre de jours (0-indexé)
> * `stayScore[i][c]` – points gagnés si vous **stay** en ville `c` le jour ` Les "
> * "travelScore[c][d]" – points gagnés si vous **voyagez** de la ville `c` à la ville `d` en tout jour
>
> **Objectif**: commencer dans n'importe quelle ville, effectuer une action par jour (séjour ou déménagement), et **maximiser le total des points** après "k" jours.

> **Constraints**
> * `1 ≤ n ≤ 200`
> * `1 ≤ k ≤ 200`
> * `0 ≤ voyageScore[c][d] ≤ 100`, `1 ≤ séjourScore[i][c] ≤ 100`

---

Intuition

Le problème est un PDD classique *dépendant du temps*:

* L'avenir touristique dépend seulement de **où** il est *et* ** quel jour** il est.
* Nous pouvons travailler **backwards** – après le dernier jour le touriste ne gagne rien, de sorte que le DP pour le prochain jour est `0` pour toutes les villes.
* Pour chaque jour, nous choisissons **stay** ou **mouver** et choisissons le meilleur résultat.

La transition clé pour la ville `c` le jour `d` est

«» "
séjour = séjourScore[d][c] + dp[d+1][c]
mouvement = max sur tous les d' ( travelScore[c][d'] + dp[d+1][d'] )
dp[d][c] = max (réglage, déplacement)
«» "

Parce que nous n'avons besoin que du DP pour le *prochain* jour, nous conservons **deux tableaux 1-D** (`prev`, `curr`) au lieu d'une table 2-D complète → **O(n)** espace.

---

C'est vrai. Complexité

* **Heure**: `O(k · n2)` – pour chaque jour nous évaluons une transition `n`‐by‐n`.
* **Espace**: `O(n)` – deux tableaux 1-D.

Avec les limites (`n, k ≤ 200`), c'est bien dans les limites de LeetCode (8 millions d'itérations internes).

---

C'est pas vrai. Code

Java

"Java
Importation de java.util.*;

solution de classe {
Int public maxScore(int n, int k, int[] [] stayScore, int[][] travelScore) {
int[] prev = nouveau int[n]; // dp pour le lendemain (initialement 0)
int[] curr = nouvelle int[n];

pour (int day = k - 1; day >= 0; jour--) {
pour (int ville = 0; ville < n; ville++) {
// Séjour dans la même ville
séjour int = séjourScore[jour][ville] + prev[ville];

// Déménagement dans toute autre ville (y compris le séjour : voyageScore[ville][ville] == 0)
mouvement int = entier.MIN_VALUE;
pour (int dest = 0; dest < n; dest++) {
Int val = voyage Score[ville][dest] + prev[dest];
si (val > se déplacer) se déplacer = val;
}
curr[city] = Math.max(station, déplacement);
}
// Swap prev & curr
int[] tmp = prév;
prev = curr;
curr = tmp;
}

// Commencer la ville peut être n'importe, alors prenez le meilleur
réponse int = 0;
pour (int val : prev) {
si (val > réponse) réponse = val;
}
réponse de retour;
}
}
«» "

---

Python 3

'`python
Solution de classe:
def maxScore(self, n: int, k: int, stayScore: List[List[int]],
Voyages Note: Liste[Liste[int]]) -> Int:
prev = [0] * n # dp pour le jour suivant
Carrière = [0] * n

pour la journée dans l'intervalle(k - 1, -1, -1):
pour la ville à portée(n):
séjour = séjourScore[jour][ville] + prev[ville]
Max sur toutes les destinations
mouvement = max (voyage) Score[city][dest] + prev[dest] pour le destination dans l'intervalle(n)
curr[city] = max(stay, moving)
prev, curr = curr, prev # tableaux de réutilisation

retour max(prev)
«» "

---

C++

'`cpp
solution de classe {
public:
int maxScore(int n, int k, vecteur<vector<int>>& Restez Score,
vector<vector<int>&travelScore) {
vecteur <int> prev(n, 0), curr(n, 0);

pour (int day = k - 1; day >= 0; --jour) {
pour (int ville = 0; ville < n; + ville) {
séjour int = séjourScore[jour][ville] + prev[ville];
int move = INT_MIN;
pour (int dest = 0; dest < n; ++ dest) {
Int val = voyage Score[ville][dest] + prev[dest];
mouvement = max (déplacer, val);
}
curr[city] = max(stay, moving);
}
swap(prev, curr); // réutiliser les deux tableaux
}
retourner *max_element(prev.begin(), prev.end());
}
};
«» "

---

C'est vrai. Article du blog – Le bon, le mauvais et le mauvais

---

Titre
> **Points maximaux Les touristes peuvent gagner – LeetCode 3332**
> **Java / Python / C++ Solution DP

#### Description de la méta (SEO)
> Apprenez l'approche de programmation dynamique optimale pour le LeetCode 3332. Solutions complètes en Java, Python et C++. Perfect interview prep pour les emplois en génie logiciel.

---

Présentation

Lorsque le recruteur demande : « Pouvez-vous résoudre un problème de DP impliquant des villes, des scores de voyage et des scores de séjour ? » Le premier instinct est de penser à une recherche de force brute.
Mais **LeetCode 3332** est un défi classique de programmation dynamique *dépendant du temps* qui teste à la fois votre perspicacité mathématique et votre style de codage.

Dans ce post, nous lisons:

1. Briser le problème.
2. Marchez dans le **bon** tour DP.
3. Montrez où se trouvent les pièges **mauvais**.
4. Confrontez-vous aux cas de bord **ugly**.
5. Partagez le code propre, prêt à la production en Java, Python et C++.

---

C'est pas vrai. Le bon – O(k · n2) DP avec deux tableaux

* **Backward DP**: En commençant par le dernier jour et en revenant à l'envers, nous n'avons besoin que des valeurs du prochain jour.
* **Deux tableaux 1-D** (`prev`, `curr`): réduit la mémoire de `O(k·n)` à `O(n)`.
C'est l'astuce "clean-up" qui maintient le code lisible et rapide.
* **Transitions de séjour/déplacement explicites**:
Texte
séjour = séjourScore[jour][ville] + prev[ville]
mouvement = max. Score[ville][dest] + prev[dest] )
curr[city] = max(stay, moving)
«» "
Formules simples, pas de boucles cachées.

Parce que `n, k ≤ 200`, la boucle intérieure `n2` fonctionne au plus 40 000 fois par jour – parfaitement bien pour LeetCode.

---

- Oui. Les mauvaises – quand les choses tournent mal

Mauvaise pratique Pourquoi il est mauvais Correction
C'est pas vrai.
Autres **Le stockage de l'ensemble `dp[k][n]` tableau**=Utilise la mémoire `O(k·n)` – inutile et peut atteindre des limites pour de plus grandes contraintes. Autres Conserver seulement deux rangées (`prev`, `curr`). Autres
**Re-computing `mouver` de scratch à chaque fois**= Toujours `O(n2)` par jour, mais vous pouvez pré-calculer le max intérieur si vous avez beaucoup de requêtes (pas besoin ici). Calculer `mouver` à l'intérieur de la boucle intérieure comme indiqué; simple et rapide. Autres
**Utiliser la récursion + mémorisation**. Le PDD itératif (bas-up) est plus sûr. Autres

---

- Oui. Les cas de bord et les bogues subtils

La manipulation de l'impact
- C'est quoi ?
"travelScore[ville] [ville] == Il est tentant de sauter la ville, mais sauter peut cacher une transition valide si rester est le meilleur mouvement. Autres Gardez la boucle de destination telle quelle; le poids `0` est inoffensif. Autres
** Grandes valeurs près des limites de `int`** Les points totaux maximums peuvent atteindre `100 * 200 + 100 * 200 = 40 000 '. Toujours en sécurité pour `int`. Si les contraintes changent, utilisez `long`. Autres
**Toutes les villes sont liées**= La réponse est le maximum au cours du premier jour; oublier de prendre `max(prev)` conduit à une erreur hors-par-un.= Après l'échange final, utilisez `max_element(prev)` (C++), `max(prev)` (Python), ou une simple boucle (Java). Autres

---

Les solutions complètes – Code propre dans chaque langue

Nous avons déjà posté les implémentations **Java**, **Python** et **C++** plus tôt.
Chaque version suit la même structure, utilise des noms de variables clairs (`prev`, `curr`), et comprend des commentaires expliquant la transition.

---

C'est pas vrai. A emporter pour l'interview

* ** Expliquer le DP** : Parlez de l'itération en arrière, de l'optimisation à deux rangs, et de la formule de séjour/déplacement.
> J'ai calculé `dp[d][c]` en regardant le lendemain, donc je n'ai besoin que de deux tableaux. (en milliers de dollars)
* **Mention temps/espace**: Montrez que vous pouvez manipuler `n, k = 200` confortablement.
* **Voir le code**: Offrez un extrait propre et compilable dans la langue de votre choix.
– Les recruteurs aiment le code concis qui fonctionne en millisecondes.

> **Résultat**: Vous démontrerez la maîtrise du PDD dépendant du temps, l'optimisation de la mémoire et le codage propre, tous caractères dorés pour une entrevue d'ingénierie logicielle.

---

Lire plus

* [Programme dynamique – Entretien avec la bibliothèque Algorithm] (https://www.interviewbit.com/dynamic-programming/)
* [Space-Optimized DP – LeetCode Tips](https://leetcode.com/articles/dynamic-programming-tutorial/)
* [C++ `swap()` vs `memcpy()` pour les tableaux DP](https://stackoverflow.com/questions/1137481/why-swap-is-faster-than-copys)

---

La pensée finale

LeetCode 3332 n'est pas seulement un puzzle DP ; c'est un *codage style test*.
Si vous pouvez:

1. ** Expliquez la transition** rapidement.
2. **Écrire le code itératif ascendant** avec deux lignes.
3. **Connais les pièges** (grandes tables, pile de récursion, etc.).

Vous brillerez dans n'importe quelle entrevue de codage et vous vous démarquerez des gestionnaires d'embauche.

Bon codage ! Les

---