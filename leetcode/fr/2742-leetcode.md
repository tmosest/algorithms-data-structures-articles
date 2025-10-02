---
titre: LeetCode 2742. Peinture des murs -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2742. Peinture des murs – Une solution de programmation dynamique en 3 langues
> **Java**

Ci-dessous vous trouverez un **compact, 7-line-per-language implémentation** qui résout le problème dur de LeetCode.
Après le code, vous lisez un court article de style blog qui explique *pourquoi* la solution fonctionne, les pièges à éviter, et comment vous pouvez l'utiliser pour impressionner les intervieweurs.

---

Récapitulation des problèmes

On vous donne deux tableaux, `coût` et `temps`, tous deux de longueur `n`.
* **Peintre peint** – mur de peinture *i* dans le temps les unités et les coûts "coûts [i]".
* **Peintre libre** – peint n'importe quel mur dans **1** unité de temps pour **gratuit**, mais ne peut travailler que lorsque le peintre rémunéré est occupé.

Objectif : ** Minimiser l'argent total dépensé** pour peindre tous les murs.

> *exemple*
> `coût = [1,2,32]`, `temps = [1,2,32]` → réponse `3` (payer pour les murs 0 et 1).

---

L'idée de base – Acheter le temps comme un knapsack

Si vous payez pour le mur `i`, vous obtenez efficacement `temps[i]` des unités de temps payé-painter **plus** le temps libre-painter qui fonctionnera simultanément.
Donc en payant pour un mur vous pouvez terminer **`temps[i] + 1`** murs tout à fait.

Ainsi le problème se réduit à un knapsack classique 0-1:

Valeur (combien de murs vous couvrez)
Il n'y a pas de lien entre les deux.
Le mur `i` Autres

Nous voulons le coût total minimum qui couvre ** au moins** `n` murs.

---

Algorithme – PDD ascendant

Laissez

`dp[t] =` coût minimal de finition *exactement* `t` murs (`0 ≤ t ≤ n`).
Initialiser: `dp[0] = 0`, tous les autres `= INF`.

Pour chaque mur `i` (dans tout ordre)
«» "
pour t de n à 1:
dp[t] = min(dp[t],
dp[max(t - temps[i] - 1, 0)] + coût[i])
«» "
Nous supprimons `t` ** vers le bas** pour éviter de réutiliser le même mur plusieurs fois.

Enfin, `dp[n]` est la réponse (coût minimum pour terminer *au moins* `n` murs).

**Complexité* *

* Temps: `O(n2)` – la double boucle sur les murs `n` et les créneaux horaires `n`.
* Espace: `O(n)` – le tableau DP.

Avec `n ≤ 500`, cela s'inscrit facilement dans les limites.

---

Code (7 lignes par langue)

### Java

"Java
Importation de java.util.*;

solution de classe {
peinture publique intWalls(int[] coût, int[] temps) {
int n = longueur de coût, INF = 1_000_000_000;
int[] dp = nouvelle int[n + 1];
Tableau de remplissage(dp, INF); dp[0] = 0;
pour (int i = 0; i < n; ++i)
pour (int j = n; j > 0; --j)
dp[j] = Math.min(dp[j], dp[Math.max(j - temps[i] - 1, 0)] + coût[i]);
retour dp[n];
}
}
«» "

Python

'`python
Solution de classe:
def paintWalls (même, coût, temps):
n, INF = len(coût), 10**9
dp = [0] + [INF] * n
pour c, t en zip(coût, temps):
pour j dans la plage(n, 0, -1):
dp[j] = min(dp[j], dp[max(j - t - 1, 0)] + c)
retour dp[n]
«» "

C++

'`cpp
solution de classe {
public:
peinture intWalls(vecteur<int>& coût, vecteur<int>& temps) {
int n = cost.size(), INF = 1e9;
vecteur<int> dp(n + 1, INF); dp[0] = 0;
pour (int i = 0; i < n; ++i)
pour (int j = n; j > 0; --j)
dp[j] = min(dp[j], dp[max(j - temps[i] - 1, 0)] + coût[i];
retour dp[n];
}
};
«» "

---

Article du blog – La peinture des murs : le bon, le mauvais et le mauvais

Titre
**Peinture des murs – Le bon, le mauvais, et l'acharnement d'un problème de LeetCode dur (DP + Knapsack)* *

Description de la méta
Découvrez une solution DP-knapsack propre à LeetCode 2742 -Peinture des murs. Apprenez les pièges, les astuces d'optimisation et comment aser ce problème d'interview difficile en Java, Python ou C++.

---

- Oui. 1. Le défi en coque
Le problème vous force à combiner **deux peintres**: un payé qui est lent mais bon marché, et un libre qui est rapide mais ne peut agir que lorsque le payé est occupé. L'objectif est de payer le moins possible tout en terminant tous les murs.

À première vue, vous pouvez essayer une stratégie gourmande (toujours choisir le mur le moins cher, ou le plus rapide), mais qui échoue spectaculairement. La vraie magie vient de ** voir le temps comme une ressource à acheter**.

- Oui. 2. Pourquoi la perspective Knapsack fonctionne
Quand vous payez pour le mur *i*, vous obtenez:

* "temps [i]" unités de travail rémunéré par correspondance, **et**
* Le peintre libre peut continuer à travailler pendant ce temps, en vous donnant efficacement `1` mur supplémentaire (celui que le peintre libre termine alors que le peintre rémunéré est occupé).

Donc vous pouvez peindre **`temps[i] + 1'** murs pour le prix du "coût[i]".
Si vous pensez que les murs peints comme la valeur et l'argent comme le coût, vous êtes en terrain parfait 0-1 knapsack: choisissez un sous-ensemble d'éléments (murs) dont la valeur totale atteint ou dépasse `n`.

- Oui. 3. Le plan directeur de la programmation dynamique
Définir `dp[t]` comme le coût le moins cher pour peindre *exactement* `t` murs. La règle de mise à jour:

«» "
dp[t] = min( dp[t], // sauter cette paroi
dp[t - (temps[i]+1)] + coût[i] ) // acheter ce mur
«» "

Nous nous préservons contre les indices négatifs en coupant à 0. Parce que nous balayons `t` de haut en bas, chaque mur est considéré une seule fois.

**Le bien**: Le DP est seulement **un tableau** – pas besoin de structures 2D ou de mémorisation récursive.

**L'""""**: Une implémentation naïve qui scanne "t" de bas en haut réutilise le même mur et sur-payeur. Rappelez-vous d'inverser la boucle !

**Le "gugly"**: Oubliant que nous avons besoin de couvrir *au moins* `n` les murs peuvent conduire à un bug subtil: si vous stockez seulement "t" exactement, vous pouvez retourner une solution sous-optimale qui couvre moins de `n` murs. L'utilisation de `max(t - time[i] - 1, 0)` nous permet de ne jamais sous-estimer.

- Oui. 4. Pièges communs et comment les éviter

Erreur
- Oui.
Utiliser une boucle *inverse* (`pour j = n; j > 0; --j`) Autres
**Calcul de la valeur de l ' erreur** – qui est la contribution libre du peintre
**Large `INF` causant un débordement** , choisissez un `INF` sûr (par exemple, `1e9`) et évitez de l'ajouter
**Penser exactement "t`murs" est nécessaire** Autres

- Oui. 5. Edge— Cheat cas Feuille

Pourquoi ça compte Que faire ?
Ce n'est pas le cas.
Temps [i] 0`-Vous obtenez toujours 1 mur, donc l'acheter est toujours une bonne idée si elle est bon marché Le DP le gère automatiquement.
Tous les coûts énorme La réponse sera la somme de tous les coûts – DP fonctionne toujours rapidement
Temps [i] n-1 ' , Payer pour un mur peut finir *tous* murs – raccourci rapide si vous le remarquez tôt

- Oui. 6. Conseils d'entrevue

1. ** Expliquez l'analogie du temps d'achat d'abord** – montre que vous pouvez penser à la ressource.
2. **Ecrivez la récurrence DP sur un tableau blanc** – la ligne `max(t - time[i] - 1, 0)` est le cœur de la solution.
3. **Afficher la complexité** – O(n2) est acceptable pour «n ≤ 500».
4. **Mention l'alternative récursive DP** – utile pour les langues qui favorisent la récursion, mais il est plus lent à écrire dans une entrevue.

- Oui. 7. Pensées finales – Le mauvais côté des problèmes difficiles

Les problèmes difficiles cachent souvent un modèle étonnamment simple. La partie laid est que beaucoup de candidats essaient exponentielle backtracking ou heuristique élaborée, seulement pour manquer de temps. La beauté de l'approche DP‐knapsack est qu'elle est :

* ** Concise** – 7 lignes par langue.
* **Correct** – prouvé par la répétition.
* **Extensible** – vous pouvez l'adapter pour couvrir au moins `k` les murs ou ajouter un autre peintre.

Lorsque vous résolvez ce problème, vous démontrez la maîtrise de **resource-affectation DP** – une compétence que les intervieweurs aiment.

---

Liste de contrôle du référencement

Élément
- Oui.
Mots-clés : `peinture des murs leetcode`, `programmation dynamique`, `knapsack`, `interview`, `coding interview`, `problem solution`, `Java`, `Python`, `C++`
Titre Contient le problème ID et type de solution
Description de la méta 150-170 caractères, comprend les mots-clés principaux Autres
Titres H1, H2, H3 utilisés pour la structure
Blocs linguistiques pour copier-coller
Conseils pratiques

---

Enveloppe

* La vue **knapsack** transforme une histoire à deux couleurs confuse en un simple PDD 0-1.
* Une boucle de mise à jour *inverse* garantit que chaque mur est utilisé une fois.
* Le code en 3 langues ci-dessus est prêt pour copier-coller lors de votre prochain concours d'entrevue ou de programmation concurrentielle.

Bonne chance – et que vos murs soient toujours peints!