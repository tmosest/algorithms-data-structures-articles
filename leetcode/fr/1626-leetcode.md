---
titre: LeetCode 1626. Meilleure équipe sans conflit -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1626 – **Meilleure équipe sans conflit**
*Programmation dynamique en Java
*SEO-Optimized Blog for Job‐Hunters: The Good, the Bad, & the Ugly*

---

Récapitulation des problèmes

> **Meilleure équipe sans conflit**
> Vous êtes le manager d'une équipe de basket.
> Chaque joueur a un **score** et un **age**.
>
> **Règlement :**
> *Vous ne pouvez pas avoir un joueur plus jeune avec un score strictement plus élevé qu'un joueur plus âgé. *
> (Les joueurs du même âge sont autorisés à commander n'importe quel score.)
>
> **Objectif:** Choisissez un sous-ensemble de joueurs qui respecte la règle et maximise la somme de leurs scores.

**Input**

Paramètre Type Contraintes
C'est quoi ?
"scores" "int[]" "1 ≤ scores.longueur ≤ 1000"
"âges" "int[]" "1 ≤ âges.longueur ≤ 1000"
(les deux tableaux sont de même longueur)

** Sortie**
`int` – score total maximum réalisable.

---

Intuition

La restriction est essentiellement une relation *non-diminution* entre **age** et **score**.
Si nous commandons les joueurs par âge (et pour des âges égaux par score ascendant), une équipe valide est une subséquence **non-diminution des scores**.

Ainsi, le problème est un classique **Longe Augmenting Subsequence (LIS)**–style DP, mais au lieu de compter la longueur, nous résumons les scores.

---

Approche optimale (O(n2) DP)

1. **Pair & Tri**
Construire un tableau de paires `(age, score)` et trier par âge, puis par score.
Après tri, toute équipe valide est une sous-séquence où chaque score subséquent est ≥ le précédent.

2. **DP**
`dp[i]` = score total maximal d'une équipe valide qui se termine avec le joueur `i`.
Transition:
Texte
dp[i] = scores[i] + max{ dp[j]
«» "
La réponse est `max(dp)`.

3. **Complexités**
*Temps*: `O(n2)` (n ≤ 1000 → amende pour LeetCode).
*Espace*: `O(n)` pour le tableau DP.

---

Mise en œuvre du code

Autres Toutes les solutions retournent le même résultat ; choisissez la langue avec laquelle vous êtes à l'aise.

---

Java

"Java
Importation de java.util.*;

solution de classe publique {
public int bestTeamScore(int[] scores, int[] âges) {
int n = scores.longueur;
// Paire (âge, score)
int[][]joueurs = nouveau int[n][2];
pour (int i = 0; i < n; i++) {
joueurs[i][0] = âges[i];
joueurs[i][1] = scores[i];
}

// Tri par âge, puis par score
Tableaux.sort(joueurs, a, b) -> {
si (a[0] != b[0]) retourne a[0] - b[0];
retour a[1] - b[1];
});

int[] dp = nouvelle int[n];
int best = 0;
pour (int i = 0; i < n; i++) {
dp[i] = joueurs[i][1]; // commencer une nouvelle équipe
pour (int j = 0; j < i; j++) {
si (joueurs[i][1] >= joueurs[j][1]) {
dp[i] = Math.max(dp[i], dp[j] + joueurs[i][1]);
}
}
best = Math.max(best, dp[i]);
}
le meilleur retour;
}
}
«» "

---

Python

'`python
Solution de classe:
def best TeamScore(self, scores: Liste[int], âges: Liste[int]) -> Int:
joueurs = triés(zip(ages, scores)) # trier par âge, puis marquer
n = len(joueurs)
dp = [0] * n
meilleur = 0

pour i dans la plage(n):
dp[i] = joueurs[i][1] # lancer une nouvelle équipe
pour j dans la plage i:
si les joueurs[i][1] >= joueurs[j][1]:
dp[i] = max(dp[i], dp[j] + joueurs[i][1])
best = max(best, dp[i])

le meilleur retour
«» "

---

C++

'`cpp
solution de classe {
public:
Int bestTeamScore(vecteur<int>& scores, vecteur<int>& âges) {
int n = scores.size();
vecteur<pair<int,int>> joueurs(n); // (âge, score)
pour (int i = 0; i < n; ++i)
joueurs[i] = {ages[i], scores[i]};

tri(players.begin(), players.end()); // âge asc, score asc

vecteur<int> dp(n);
int best = 0;
pour (int i = 0; i < n; ++i) {
dp[i] = joueurs[i].seconde; // nouvelle équipe
pour (int j = 0; j < i; ++j)
i (joueurs[i].seconde >=joueurs[j].seconde)
dp[i] = max(dp[i], dp[j] + players[i].seconde);
best = max(best, dp[i]);
}
le meilleur retour;
}
};
«» "

---

C'est vrai. Les bons, les mauvais et les méchants

**Quoi faire**
C'est ce qu'on dit.
**Bon**• Compréhension claire et facile à comprendre DP<br>• Fonctionne pour jusqu'à 1000 joueurs (limite de LeetCode)<br>• Manipulation des liens de même âge avec tri-par-score
**Bad**) • O(n2) peut atteindre des limites de temps sur des ensembles de données plus importants dans d'autres contextes (n > 105)<br>• Tri par âge ignore seulement la possibilité d'utiliser un Fenwick/BIT pour obtenir O(n log n) si nécessaire
**Désormais** Si vous oubliez de trier par score pour des âges égaux, vous pouvez manquer une séquence ultérieure valide.<br>• Une comparaison erronée (`>` vs `>=`) rompt la règle.<br>• La mémoisation récursive peut faire sauter la pile si pas prudent.

> **Conseil d'entrevue** – Demandez à l'intervieweur si vous pouvez améliorer l'exécution. Une belle segue pour discuter Fenwick/BIT ou la compression de coordonnées pour une solution O(n log n).

---

- Oui. Avancé : O(n log n) avec arbre Fenwick

> Seulement si l'entrevue d'embauche prévoit des solutions à haut rendement.

1. Compresser les scores dans les rangs (`1..M`).
2. Trier les joueurs par âge, puis par score.
3. Utilisez un arbre Fenwick pour interroger le score total maximal pour tous les scores ≤ score courant.
4. Mettre à jour l'arborescence avec `currentScore + bestFromTree`.

**Heure**: `O(n log M)` – idéal pour `n = 105`.
**Espace**: `O(M)` – `M` scores distincts.

*Nous conservons la version O(n2) simple pour plus de clarté, mais vous pouvez tomber dans le code Fenwick si vous voulez impressionner. *

---

Essais et cas de bord

Autres Test d'entrée prévu
- C'est quoi ?
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
[2,1,2,1]
[1,2,3,5] `<br>` `[8,9,10,1]`
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
[1,1]

> **Conseil:** Inclure toujours le même scénario d'âge dans votre harnais d'essai; c'est un piège commun.

---

### # 8.

- **Problem‐Solving** – Transformez une règle en un modèle tri+DP; le même truc apparaît dans les problèmes de Subséquence Maximum et d'équipe Constructive.
- **Code Clarity** – Gardez les noms de variables expressifs (`joueurs`, `dp`, `meilleur`).
- **Time vs Space** – O(n2) est bon pour LeetCode; mention possible O(n log n) si l'intervieweur demande.
- **Test** – Couvrir les conditions limites, les liens et les cas à élément unique.
- **Soft Skill** – Communiquer les compromis. Un bon ingénieur demande toujours des éclaircissements sur les contraintes et discute des alternatives de performance.

Autres *Lorsque vous pouvez résoudre un problème de LeetCode en quelques lignes puis discuter d'une amélioration, vous démontrez à la fois maîtrise et ambition – exactement ce que les recruteurs recherchent. *

Bonne chance avec vos interviews de codage ! Si vous souhaitez plonger plus profondément dans les arbres du Fenwick, ou pratiquer des énigmes plus dynamiques, n'hésitez pas à me piquer. C'est ce qu'il a dit.

---

> **Mots clés en évidence:**
> *LeetCode 1626, Best Team With No Conflicts, Dynamic Programming, Java solution, Python solution, C++ solution, Software Engineer interview, Algorithm interview, Recherche d'emploi, Optimisation des performances, Fenwick tree, LIS, LIS‐DP, problème de codage d'entrevue, conseils d'entrevue, entretien d'ingénierie logicielle. *

Bon codage – et que votre prochaine interview parte *viral*!