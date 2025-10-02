---
titre: LeetCode 1049. Dernière pierre Poids II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1049. Dernière pierre Poids II – Code + SEO-Optimized Blog Post

- Oui. 1. Récapitulation des problèmes (Code de bord 1049)

Vous êtes donné un tableau `pierres[]` d'entiers positifs.
Dans un mouvement vous choisissez deux pierres de poids `x ≤ y`, les briser:

Résultats
C'est quoi ?
Les deux pierres disparaissent
La pierre de poids `x` est détruite, la pierre de poids `y` devient `y - x`

Le processus se poursuit jusqu'à ce qu'il reste au plus une pierre.
Retourner le **le plus petit possible** poids de cette pierre (ou `0` si aucune).

Contraintes
- `1 ≤ pierres longueur ≤ 30`
- `1 ≤ pierres[i] ≤ 100`

Comme le tableau est minuscule, une solution de programmation dynamique basée sur l'idée **subset‐sum / 0‐1 knapsack** est parfaite.

---

- Oui. 2. Idées de base – Dépliez les pierres en deux piles

Le résultat de la destruction de toutes les pierres peut être considéré comme la partition de l'ensemble en deux groupes:

- Le groupe **A** (poids total "s1") est écrasé par rapport à **B** (poids total "s2").
- Après toutes les écrasements, le poids restant est `=1 – s2='.

Ainsi nous voulons **minimiser** `=s1 – s2=‘.
Si nous laissons `total = somme(pierres)`, alors `s2 = total – s1`.
L'objectif devient :

«» "
Mini total – 2 * s1
«» "

où «s1» doit être un poids réalisable par un sous-ensemble de «pierres».
C'est exactement le problème classique **subset-sum** (0-1 knapsack).

- Oui. Pourquoi ça marche ?

- Oui. Chaque coup équivaut à prendre une pierre d'un groupe et à la soustraire de l'autre.
- Après toutes les opérations, le reste du poids de pierre est la différence absolue des sommes des deux groupes.
- Oui. La différence minimale possible est obtenue en trouvant la somme du sous-ensemble la plus proche du « total / 2 ».

---

- Oui. 3. Mise en œuvre

Voici des solutions propres et idiomatiques dans **Java, Python et C++**.
Toutes les utilisations **bottom-up DP** avec une table booléenne 2-D `dp[i][j]` – pouvons-nous faire la somme `j` en utilisant les premières pierres `i`?
Heure: "O(n* total) "
Espace: `O(n * total)` (peut être réduit à "O(total)" avec un tableau 1-D, mais la version 2-D maintient la logique cristal‐clair).

#### 3.1 Java

"Java
***
* LeetCode 1049 – Dernière pierre Poids II
* Solution DP – temps O(n * total), espace O(n * total)
*/
solution de classe publique {
Int public lastStoneWeightII(int[] pierres) {
int n = longueur des pierres;
= 0;
pour (int w : pierres) total += w;

// dp[i][j] = vrai si nous pouvons obtenir la somme j avec les premières pierres i
booléen[][] dp = nouveau booléen[n + 1][total + 1];
pour (int i = 0; i <= n; i++) dp[i][0] = vrai; // somme 0 est toujours possible

pour (int i = 1; i <= n; i++) {
int w = pierres[i - 1];
pour (int j = 1; j <= total; j++) {
si (w <= j) {
dp[i][j] = dp[i - 1][j]
} autre {
dp[i][j] = dp[i - 1][j];
}
}
}

int best = entier.MAX_VALUE;
// chercher la somme du sous-ensemble la plus proche du total/2
pour (int s = 0; s <= total / 2; s++) {
si (dp[n][s]) {
int diff = Math.abs(total - 2 * s);
best = Math.min(best, diff);
}
}
le meilleur retour;
}
}
«» "

---

3.2 Python

'`python
Solution de classe:
def lastStoneWeightII(self, stones: List[int]) -> Int:
total = somme (pierres)
n = len(pierres)

# dp[i][j] – Pouvons-nous obtenir la somme j avec les premières pierres i?
dp = [[Faux] * (total + 1) pour _ dans l ' intervalle (n + 1)]
pour i dans la plage (n + 1):
dp[i][0] = Vrai

pour i dans la plage(1, n + 1):
w = pierres[i - 1]
pour j dans la fourchette(1, total + 1):
si w <= j:
dp[i][j] = dp[i - 1][j] ou dp[i - 1][j - w]
Sinon:
dp[i][j] = dp[i - 1][j]

meilleure = flotteur("inf")
pour s dans l ' intervalle (total // 2 + 1):
si dp[n][s]:
best = min(meilleur, abs(total - 2 * s))

le meilleur retour
«» "

*(Les développeurs Python préfèrent souvent un DP 1-D pour les économies de mémoire: `dp[j] = dp[j] ou dp[j - w]`.) *

---

### 3.3 C++

'`cpp
***
* LeetCode 1049 – Dernière pierre Poids II
* Solution DP – temps O(n * total), espace O(n * total)
*/
solution de classe {
public:
int lastStoneWeightII(vecteur <int>& pierres) {
= 0;
pour (int w : pierres) total += w;
int n = pierres.size();

vector<vector<bool>> dp(n + 1, vector<bool>(total + 1, faux));
pour (int i = 0; i <= n; ++i) dp[i][0] = vrai;

pour (int i = 1; i <= n; ++i) {
int w = pierres[i - 1];
pour (int j = 1; j <= total; ++j) {
si (w <= j) {
dp[i][j] = dp[i - 1][j]
} autre {
dp[i][j] = dp[i - 1][j];
}
}
}

int best = INT_MAX;
pour (int s = 0; s <= total / 2; +) {
si (dp[n][s]) {
best = min(meilleur, abs(total - 2 * s));
}
}
le meilleur retour;
}
};
«» "

*(Les utilisateurs C++ avancés peuvent remplacer le DP 2-D par un seul bitset: `std::bitset<10001> dp; dp[0] = 1; pour (auto w : stones) dp= dp << w;` qui fonctionne dans ~O(n * total / 64) temps.) *

---

- Oui. 4. Analyse de la complexité

Heure de mise en œuvre
- Oui.
Java 2-D DP. Autres
Python 2-D DP=1 `O(n * total)`=1 `O(n * total)` Autres
C++ 2-D DP. Autres
Bitset / 1-D DP. Autres

Avec `n ≤ 30` et `total ≤ 3000` (30 * 100), ces runtimes sont assez rapides pour les limites de LeetCode.

---

- Oui. 5. Billet de blog – *Le Bon, le Mauvais, et l'Ugly du dernier poids de pierre II

Titre
**Dernier poids de pierre II – Le bon, le mauvais, et le mauvais de LeetCode #1049* *

Description de la méta
Apprenez à cracher LeetCode 1049 avec programmation dynamique, astuces knapsack et conseils d'entrevue de codage du monde réel. Solutions Java, Python et C++ + guide convivial SEO.

Mots clés
*LeetCode 1049, Dernière pierre Poids II, programmation dynamique, problème knapsack, interview de codage, Java DP, Python DP, C++ DP, interview d'algorithme, prép d'entretien d'emploi, interview technique, structures de données, conception d'algorithme*

---

Introduction

Si vous êtes à la recherche d'un défi de LeetCode qui mélange **la pensée combinée** avec la programmation classique **dynamique**, *Last Stone Weight II* (LeetCode #1049) est un ajustement parfait.

Dans cet article, nous disséquons le problème, nous traversons une solution PDD propre, nous discutons des écueils du bord, et nous évaluons enfin les aspects *bon*, *mauvais* et *beaucoup* des différentes approches. En chemin, nous fournissons des extraits de code Java, Python et C++ entièrement commentés que vous pouvez coller dans votre environnement IDE ou interview.

---

C'est vrai. Ce qui fait Ce problème

1. **Objectif clair** – minimiser le poids final de la pierre.
2. **Petites contraintes** – «n ≤ 30», «poids ≤ 100 ' → DP est trivial.
3. **Cadre classique** – c'est un knapsack / sous-ensemble déguisé.
4. **Langues multiples** – vous pouvez le résoudre en Java, Python, C++, etc.

---

- Oui. 1. Le bon – Pourquoi la solution de PDD se transforme

Aspect Pourquoi il est grand
-- -- -- -- -- --
**Optimalité**Le DP énumère **toutes** les sommes sous-ensemble, garantissant le minimum global. Autres
**Simplicité**Le code n'est que deux boucles imbriquées – pas de récursion ou de retour en arrière. Autres
**Readability**= Les tables booléennes (`dp[i][j]`) map directement à = peut-on obtenir la somme `j` avec les premières pierres `i`?=. Autres
**Réutilisabilité**La routine sous-ensemble-somme est un modèle de manuel pour de nombreux problèmes d'entrevue (changement de pièces, partition, etc.). Autres
Même si les contraintes deviennent `n = 200` et `poids ≤ 1000`, le DP reste confortablement adapté à la mémoire ('200 * 200k = 40M` booléens 40 MB). Autres

---

- Oui. 2. Les mauvais – compromis et Gotchas

Sujet Atténuation
- C'est quoi ?
Autres **Utilisation de l'espace** peut ballonner si vous n'êtes pas prudent. Utilisez un DP 1-D (`dp[j]`) pour couper la mémoire en deux. Autres
**Temps si `total` est énorme** Dans de tels cas, vous auriez besoin d'un coup de meet-in-the-middle ou bitset. Autres
**Bogues hors-par-un**= N'oubliez pas que `dp[i][j]` utilise les premières pierres `i` (1‐basé). Une erreur courante est le mélange d'indices basés sur 0. Autres
**Int vs. long**= Quand on résume jusqu'à 3000, `int` est bien, mais garde toujours contre le débordement si les contraintes changent. Autres

---

- Oui. 3. Les alternatives laborieuses – rapides et dirty

D'autre part quand il apparaît Pourquoi il s'agit d'Ugly
-- -- -- -- -- -- -- -- --
Des intervieweurs veulent que tu *penses* récursivement. «O(2^n)» – sans espoir pour «n = 30». Bon seulement pour l'apprentissage, pas la production. Autres
*Greedy *Pick la plus grande pierre** Si vous êtes rushing, vous pourriez juste continuer à casser les deux plus grandes pierres jusqu'à ce qu'il reste un. Cela donne une réponse sous-optimale dans de nombreux cas (par exemple «[2,74]». C'est un raccourci tentant mais dangereux. Autres
**Permutations de la branche de la force**= Générer toutes les permutations des pierres et simuler le processus. Autres Extrêmement lent ('O(n! * n)'). Il peut passer si les cas de test sont minuscules, mais obtiendra TLE sur les cas cachés. Autres
**Heuristiques randomisées** Peut passer un défi personnel, mais échouera presque toujours sur les tests cachés de LeetCode. Autres

> **Ligne de bottom:** *Ne pas utiliser les approches laids dans une vraie interview à moins que vous soyez dans une situation sous pression temporelle.* Le DP est propre, rapide et sûr.

---

- Oui. 4. Conseils linguistiques

- **Java**
- Utiliser `ArrayList` ou `int[]` – aucun générique nécessaire.
- Préférez `dp[i][0] = true` sur un `if` à l'intérieur de la boucle intérieure pour plus de clarté.

- **Python**
- La compréhension des listes crée rapidement la table DP.
- Le PDD 1-D peut être écrit comme suit :
'`python
dp = [Faux] * (total + 1)
dp[0] = Vrai
pour w en pierres:
pour j dans l'intervalle (total, l - 1, -1):
Dp[j]= dp[j - w]
«» "
- `abs(total - 2 * s)` est la différence minimale.

- **C++**
- `std::bitset` est le *speed-hero* pour les grands totaux:
'`cpp
md::bitset<10001> bits; // 3000 + 1 est sûr
bits[0] = 1;
pour (int w : pierres) bits= bits << w;
«» "
- Alors la réponse est `min_{s ≤ total/2} total - 2*s` où `bits[s]` est prêt.

---

- Oui. 4. Réflexions finales – Comment utiliser ceci dans votre entrevue

1. ** Expliquez la réduction** – C'est un problème de sous-ensemble-somme / knapsack. (en milliers de dollars)
2. **Settch la table DP** – sur un tableau blanc, écrire «dp[i][j]» et expliquer les cas de base.
3. **Coder** – écrire à la main les boucles imbriquées; ne pas copier-coller.
4. **Test ledge case** – `[1]`, `[1,2,3]`, `[100]*30` pour vous montrer les limites.
5. **Optimiser si demandé** – parler de 1-D DP ou bitset lorsque la pression d'espace/temps augmente.

En présentant les points de vue *bon*, *mauvais* et *puissant* vous démontrez **la maturité algorithmique** – la capacité d'évaluer les compromis – que les intervieweurs aiment.

---

Appel à l'action

> *Ton code est prêt ? Essayez sur LeetCode ! Soumettre, tester contre les cas cachés, et partager votre expérience dans les commentaires. *

Bon codage ! C'est ce qu'il a dit.

---

Conclusion

*Dernier Stone Weight II* est plus qu'un problème de LeetCode moyen ; c'est un terrain de jeu miniature pour la maîtrise de programmation dynamique.
Avec le modèle DP ci-dessus et la lentille analytique de cet article, vous êtes désormais équipé pour résoudre le problème en Java, Python ou C++ et pour impressionner vos intervieweurs avec un code propre, optimal et bien pensé.

---

**Bonne entrevue Préparez !**
*— Votre compagnon d'entrevue de codage*

---

* Fin du blog *

---

- Oui. 6. Notes finales

- **Copy-Paste Ready** – les trois extraits de code se compilent comme-est dans leurs environnements linguistiques respectifs.
- **Test du temps** – pour une limite de LeetCode de 1 seconde, le DP tourne en millisecondes sur les processeurs modernes.
- **Prép. d'entrevue d'embauche** – ce problème est un point de départ dans de nombreuses bibliothèques d'entrevues de haute technologie; sa maîtrise peut renforcer votre confiance sur des questions similaires de DP/knapsack.

Bonne chance, et que votre dernier poids de pierre soit toujours minimal!