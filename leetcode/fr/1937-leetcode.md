---
titre: LeetCode 1937. Nombre maximal de points avec coût -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code 3-Way – Java / Python / C++

Vous trouverez ci-dessous des solutions propres et prêtes à la production pour LeetCode 1937.
Les trois codes fonctionnent dans **O(m × n)** temps et **O(n)** mémoire supplémentaire, ce qui est optimal pour les contraintes données.

---

### 1.1 Java (compatible avec le code leet)

"Java
// 1937. Nombre maximum de points avec coût
// Java 17 / LeetCode compatible

solution de classe publique {
public long maxPoints(int[][] points) {
int lignes = points. longueur;
int cols = points[0] longueur;

long[] dp = nouveau long[cols];
pour (int c = 0; c < cols; ++c) dp[c] = points[0][c];

pour (int r = 1; r < lignes; ++r) {
long[] gauche = nouveau long[cols];
long[] droite = nouveau long[cols];

// balayage de gauche à droite
gauche[0] = dp[0];
pour (int c = 1; c < cols; ++c) {
gauche[c] = Math.max(gauche[c - 1], dp[c] + c);
}

// balayage de droite à gauche
droit[cols - 1] = dp[cols - 1] - (cols - 1);
pour (int c = cols - 2; c >= 0; --c) {
droite[c] = Math.max(droit[c + 1], dp[c] - c);
}

long[] newDp = nouveau long[cols];
pour (int c = 0; c < cols; ++c) {
longue meilleure Précédent = Math.max(gauche[c] - c, droite[c] + c);
newDp[c] = bestPrev + points[r][c];
}
dp = nouveauDp;
}

long ans = long. _Valeur minimale;
pour (long v : dp) ans = Math.max(ans, v);
le retour des an;
}
}
«» "

---

#### 1.2 Python 3

'`python
# 1937. Nombre maximal de points avec coût
# Python 3

Solution de classe:
def maxPoints(self, points) -> Int:
lignes, cols = len(points), len(points[0])
dp = [points[0][c] pour c dans la plage(cols)]

pour r dans l'intervalle(1, lignes):
gauche = [0] * cols
droite = [0] * cols

gauche[0] = dp[0]
pour c dans la plage (1, cols):
gauche[c] = max(gauche[c-1], dp[c] + c)

droite[cols-1] = dp[cols-1] - (cols-1)
pour c dans l'intervalle (cols-2, -1, -1):
droite[c] = max(droit[c+1], dp[c] - c)

nouvelle_dp = [0] * cols
pour c dans la plage(cols):
best_prev = max(left[c] - c, right[c] + c)
new_dp[c] = best_prev + points[r][c]
dp = new_dp

retour max(dp)
«» "

---

### 1.3 C++ (g++17)

'`cpp
// 1937. Nombre maximum de points avec coût
// C++17

solution de classe {
public:
long maxPoints(vecteur<vecteur<int>&points) {
int R = points.size(), C = points[0].size();
vecteur <long> dp(C);
pour (int c = 0; c < C; ++c) dp[c] = points[0][c];

pour (int r = 1; r < R; ++r) {
vecteur <long> gauche(C), droite(C);

gauche[0] = dp[0];
pour (int c = 1; c < C; ++c)
gauche[c] = max(gauche[c-1], dp[c] + c);

droite[C-1] = dp[C-1] - (C-1);
pour (int c = C-2; c >= 0; --c)
droite[c] = max(droit[c+1], dp[c] - c);

vecteur <long> nouveauDp(C);
pour (int c = 0; c < C; ++c) {
long long bestPrev = max(left[c] - c, droit[c] + c);
newDp[c] = bestPrev + points[r][c];
}
dp.swap(nouveauDp);
}

retourner *max_element(dp.begin(), dp.end());
}
};
«» "

> **Pourquoi "long"?**
> Même si chaque «point[r][c] ≤ 105», nous pouvons additionner jusqu'à 105 cellules et soustraire jusqu'à 105 * 105 dans le pire des cas.
> La valeur intermédiaire maximale s'adapte confortablement en entier signé 64 bits («long long» / «long»), empêchant le débordement.

---

- Oui. 2. Article du blog – Le bon, le mauvais, et le mauvais de LeetCode 1937

### Titre (SEO-optimisé)

> * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

Description de la méta

> Apprenez la solution DP la plus propre de LeetCode 1937, évitez les erreurs courantes, et découvrez comment répondre à cette question dans votre prochaine interview technique. Comprend le code Java, Python et C++, ainsi que des idées de carrière.

---

Table des matières

1. [Présentation du problème](#problème-aperçu)
2. [Force-Brute – Les mauvaises] (#force-brute)
3. [Programme dynamique – le bon] (#dp-good)
4. [Two-Pass Optimization – The Ugly & The Clever] (#two-pass)
5. [Dossiers et essais] (#cases de référence)
6. [Complexité temporelle et spatiale](#complexité)
7. [Interview Take-aways](#interview)
8. [Conclusion et conseils professionnels](#conclusion)

---

C'est vrai. 1. Aperçu du problème <un nom="problème-overview"></a>

> **Nombre maximum de points avec coût (Code Leet 1937)* *
> Avec une matrice `m × n` `points`, choisissez exactement une cellule par ligne.
> Score = somme des cellules choisies – somme des différences de colonnes absolues entre les lignes consécutives.
> Retournez le score maximum réalisable.

> **Constraints**
> 1 ≤ m, n ≤ 105 '
> • `m × n ≤ 105`
> • <0 ≤ points[i][j] ≤ 105 "

Le problème est un DP classique sur une grille 2-D avec un coût qui dépend de la distance de colonne.

---

C'est vrai. 2. Brute-Force – La mauvaise <un nom="brute-force"></a>

Une approche naïve tenterait tous les chemins possibles.
Même pour `m = 10` et `n = 10`, cela représente des possibilités `105` – encore trop grandes.
Plus généralement, un PDD simple qui itère sur toutes les paires de colonnes de chaque transition coûterait **O(m × n2)**, ce qui est impossible quand `n` est `105`.

**À emporter :** Évitez les boucles de colonnes imbriquées ; vous avez besoin d'une stratégie linéaire par ligne.

---

C'est vrai. 3. Programmation dynamique – Le bon <un nom="dp-good"></a>

**Observation* *

Pour la ligne `r`, si nous connaissons déjà les meilleurs scores jusqu'à la ligne `r‐1` pour chaque colonne `c`, nous pouvons calculer le meilleur score pour chaque colonne `c'` dans la ligne `r`:

«» "
dp_r[c'] = points[r][c'] + max sur tous les c ( dp_{r-1}[c]
«» "

Le seul problème est que le maximum intérieur semble quadratique.

**Réformulation**

Parce que "c" - c" = c" - c` si "c ≤ c"` et "c - c"` Sinon, nous pouvons diviser le maximum en deux parties:

«» "
max( max_{c ≤ c'} (dp_{r-1}[c] + c) - c',
max_{c ≥ c'} (dp_{r-1}[c] - c) + c' )
«» "

Notez que l'expression à l'intérieur de chaque max dépend uniquement d'un *préfixe* ou *suffixe* de `c`.
Ainsi, en précomputant les meilleures valeurs de préfixe ("c` croissant) et les meilleures valeurs de suffixe (`c` décroissant), nous pouvons répondre à chaque "c" en O(1) temps.

---

C'est vrai. 4. Optimisation des deux passes – La folie et la délicatesse <un nom="deux passes"></a>

** Préfixe balayage (gauche → droite)* *

«» "
gauche[c] = max( gauche[c-1], dp_{r-1}[c] + c )
«» "

Après le balayage, `left[c]` égale `max_{k ≤ c} (dp_{r-1}[k] + k)`.

**Suffix balayage (à droite → à gauche)* *

«» "
droite[c] = max( droite[c+1], dp_{r-1}[c] - c )
«» "

Après le balayage, `à droite[c]` égale `max_{k ≥ c} (dp_{r-1}[k] - k)`.

**Combinaison* *

«» "
bestPrev = max( gauche[c'] - c', droite[c'] + c' )
dp_r[c'] = points[r][c'] + meilleur Précédent
«» "

Comme chaque balayage est linéaire, toute la transition par rangée est **O(n)**.

**Pourquoi est-ce la partie laid? * *
À première vue, les deux balayages ressemblent à un tour, mais ils sont en fait une façon *clever* de transformer un DP quadratique en temps linéaire.
Si vous êtes à l'aise d'expliquer pourquoi les balayages fonctionnent, vous impressionnerez interviewers.

---

C'est vrai. 4. Cas de bord et essais <un nom="cas de bord"></a>

Autres Test de la matrice Score attendu Pourquoi ça compte
-- -- -- -- -- -- -- -- -- --
[[]]» Une ligne, aucun coût
[[1, 2, 3]]» Une seule ligne, vérifiez si l'algorithme choisit la cellule max.
[5, 0], [0, 5]» 2 rangs, max quand vous restez dans la même colonne
Le coût est nul lorsque vous alternez les colonnes (`=1-0=1`, `=1=1`) – vous apprendrez à gérer les grandes colonnes `=1=1=1` Autres
"[[10^5]*10^5]""" `10^5 × 10^5"" Les valeurs maximales possibles, les tests débordent si vous utilisez des ints 32 bits"
La transition est triviale – l'algorithme devrait encore se terminer dans < 1 s

**Stratégie d'essai* *

1. **Petites matrices manuelles** – santé – vérifier chaque ligne de DP.
2. **Random grandes matrices** – générer `m × n ≤ 105` et vérifier contre un résolveur de force brute pour `m ≤ 5`.
3. ** Limites d'âge** – `m = 1` et `n = 105`, et inversement.

Si votre implémentation passe tout cela, vous êtes prêt pour une interview.

---

C'est vrai. 5. Complexité temporelle et spatiale <un nom=complexité></a>

Algorithme Temps Espace supplémentaire
C'est quoi ?
*(m × n2)
PDD (quadratique)
**Two-Pass DP (les nôtres)**

Avec `m × n ≤ 105`, cela signifie que la solution fonctionne en millisecondes sur LeetCode et satisfait à toutes les contraintes.

---

C'est vrai. 6. Take-aways de l'entrevue <a name="interview"></a>

Conseil Pourquoi c'est important
-- -- -- -- --
**Expliquez la fonction de coût analytiquement** – cassez `=c'‐c=` en `c'‐c` / `c‐c'`. Autres
Autres **Afficher le balayage à deux passages** – de nombreux candidats sautent cette étape. Démontre la créativité algorithmique et les économies de temps. Autres
** Mettre en évidence l'utilisation longue et longue** – éviter les débordements. Les recruteurs accordent une grande importance aux détails et aux pratiques de codage sécuritaires. Autres
**Mention (m × n2) est un piège** – parlez de pourquoi il échoue. Dire que vous comprenez les contraintes et les budgets de performance. Autres
**Run à travers un exemple sur le tableau blanc** – marcher à travers une matrice 3×4. Autres Les intervieweurs aiment voir le raisonnement, pas seulement le code. Autres

> **Bonus:** Beaucoup de gestionnaires d'embauche demandent : Que feriez-vous si `n` étaient 106?= Réponse : =Vous ne pouvez pas exécuter `n2` boucles; vous avez besoin de l'astuce bipass ou d'une structure de données alternative (arbre de segment) mais cela coûte toujours O(n log n). (en milliers de dollars)

---

C'est vrai. 7. Conclusion et conseils de carrière <un nom></a>

> **Je viens de résoudre LeetCode 1937 avec un temps optimal, une mémoire optimale et un risque zéro de débordement entier. **
> En maîtrisant cette question, vous allez :

1. **Showcase DP mastery** – un incontournable pour les entrevues sur les structures de données et les algorithmes.
2. **Éviter les pièges les plus courants** – balayages quadratiques, mauvaise manipulation de la valeur absolue, débordement entier.
3. **Construisez un portfolio de langages** – les implémentations Java, Python et C++ prêtes vous aident à répondre à cette question.
4. **Renforcez votre confiance en code** – pratiquez ce problème exact avant votre prochaine entrevue.

> **Entrevue d'emploi Conseil :**
> Quand on vous demande de résoudre un problème de LeetCode, commencez toujours par une idée de haut niveau (DP ici) avant de plonger dans le code. Promenez votre intervieweur à travers les étapes "bad", "good" et "ugly" – il démontre *problème-solution de pensée*, qui recruteurs valorisent bien plus qu'un seul extrait correct.

---

La pensée finale

LeetCode 1937 est plus qu'un puzzle de codage ; c'est un micro-écosystème de contraintes, de choix algorithmiques et de rhétorique d'entrevue.
En présentant une solution DP propre dans **Java**, **Python** et **C++**, vous montrez que vous pouvez :

* Code de la production écrite
* Optimiser pour le temps et l'espace
* Communiquer clairement les idées complexes

Tout ce qui sont exactement ce que **recruteurs de haute technologie** cherchent. Continuez la pratique, continuez le polissage, et vous atterrissez cette offre d'emploi en un rien de temps!