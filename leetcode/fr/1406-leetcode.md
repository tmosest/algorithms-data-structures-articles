---
titre: LeetCode 1406. Jeu de pierre III -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Jeu de pierre III – Solution DP optimale (Java / Python / C++)

Ci-dessous sont **clean, les implémentations prêtes à la production** pour le problème LeetCode **1406. Jeu de pierre III**.
Les trois solutions fonctionnent dans le temps **O(n)** et dans l'espace auxiliaire **O(1)** (le tableau constant 3-longueur DP).

"Java
// Java – compatible LeetCode
solution de classe {
publique Chaîne pierreGameIII(int[] pierreValue) {
int n = stoneValue.longueur;
// dp[i % 3] stocke le meilleur avantage net (Alice – Bob) de l'index i
int[] dp = nouveau int[3]; // automatiquement 0-initialisé

pour (int i = n - 1; i >= 0; i--) {
Int take1 = pierre Valeur[i] - dp[i + 1) % 3];

int take2 = entier.MIN_VALUE;
si (i + 1 < n) prise2 = pierre Valeur[i] + pierre Valeur[i + 1] - dp[i + 2) % 3];

int take3 = Integer.MIN_VALUE;
si (i + 2 < n) prise3 = pierre Valeur[i] + pierreValeur[i + 1] + pierre Valeur[i + 2] - dp[i + 3) % 3];

dp[i % 3] = Math.max(Math.max(prise1, prise2), prise3);
}

Int diff = dp[0]; // Alice – Bob
si (diff > 0) retourner "Alice";
si (diff < 0) retourne "Bob";
retourner "Tie";
}
}
«» "

'`python
# Python – compatible LeetCode
Solution de classe:
def pierre Jeu III (même, pierre) Valeur : Liste[int] -> str :
n = len(pierre Valeur)
dp = [0, 0, 0] # dp[i % 3] = meilleur avantage de i

pour i dans la fourchette(n - 1, -1, -1):
take1 = stoneValue[i] - dp[(i + 1) % 3]

take2 = flotteur('-inf')
si i + 1 < n:
prise2 = pierreValeur[i] + pierre Valeur[i + 1] - dp[i + 2) % 3]

take3 = flotteur('-inf')
i + 2 < n:
take3 = pierreValeur[i] + pierreValeur[i + 1] + pierre Valeur[i + 2] - dp[i + 3) % 3]

dp[i % 3] = max(take1, take2, take3)

diff = dp[0] # Alice – Bob
si diff > 0: retourner "Alice"
si diff < 0: retourner "Bob"
retourner "Tie"
«» "

'`cpp
// C++ – compatible LeetCode
solution de classe {
public:
Pierre à cordesGameIII(vecteur<int>& stoneValue) {
int n = stoneValue.size();
int dp[3] = {0, 0, 0}; // dp[i % 3] = meilleur avantage de i

pour (int i = n - 1; i >= 0; --i) {
Int take1 = pierre Valeur[i] - dp[i + 1) % 3];

take2 = INT_MIN;
si (i + 1 < n)
prise2 = pierreValeur[i] + pierre Valeur[i + 1] - dp[i + 2) % 3];

take3 = INT_MIN;
si (i + 2 < n)
take3 = pierreValeur[i] + pierreValeur[i + 1] + pierre Valeur[i + 2] - dp[i + 3) % 3];

dp[i % 3] = max({take1, take2, take3});
}

Int diff = dp[0]; // Alice – Bob
si (diff > 0) retourner "Alice";
si (diff < 0) retourne "Bob";
retourner "Tie";
}
};
«» "

---

Article du blog : Les bons, les mauvais et les méchants du jeu de pierre III

> **Méta—Description:**
> Master LeetCodeS Stone Game III avec une solution DP claire et optimale en Java, Python et C++. Apprenez la bonne, la mauvaise et laid de ce problème classique de théorie du jeu et augmentez votre préparation à l'entrevue.

---

- Oui. 1. Présentation

Stone Game III est un puzzle classique basé sur le tour** qui apparaît sur LeetCode comme problème 1406. Le jeu force les joueurs à prendre des décisions dans une séquence de piles, et le gagnant est celui avec la valeur de pierre totale plus élevée après toutes les piles sont prises.

Si vous avez déjà préparé pour une entrevue, vous êtes probablement familier avec des questions similaires de stratégie optimale: *Quel est le meilleur mouvement que vous pouvez faire, en supposant que l'adversaire joue aussi de manière optimale? *
Stone Game III est l'une de ces questions qui peuvent être résolues avec élégance avec la programmation **dynamique** (DP). Dans cet article, nous allons passer par:

- Pourquoi le problème est un jeu-théorie DP** déguisé
- La solution DP** de base qui n'utilise qu'un tableau à 3 éléments ('O(1)' espace)
- Pièges à l'extrémité (valeurs négatives de pierre, longueurs impaires, etc.)
- Les parties de la solution
- Comment utiliser ces connaissances pour impressionner les intervieweurs

---

- Oui. 2. Récapitulation des problèmes (dans vos propres mots)

- On vous donne un tableau «stoneValue» de longueur **n** («1 ≤ n ≤ 5·104»).
- Alice commence; Bob suit; chaque tour, un joueur peut prendre **1, 2 ou 3** pierres de la pile restante la plus à gauche.
- Les scores sont accumulés par joueur comme la somme des valeurs des pierres prises.
- Les deux jouent **optimalement**.
- Retourner `"Alice"`, `"Bob"`, ou `"Tie"` selon qui finit avec le score plus élevé.

---

- Oui. 3. Intuition: De la théorie du jeu au DP

### 3.1. Le concept de l'avantage net

Au lieu de suivre chaque joueur de score individuel, il est plus simple de suivre la différence **** (Score d'Alice)
Si nous indiquons :

«» "
bestAvantage(i) = maximum (AliceScore - BobScore) réalisable
si le jeu commence à index i
«» "

alors la réponse est:

«» "
if bestAvantage(0) > 0 -> Alice gagne
if bestAvantage(0) < 0 -> Bob gagne
sinon Tie
«» "

3.2. Relation récursive

À partir de l'index `i` un joueur peut prendre:

1. **Une pierre** – l'adversaire commence à `i+1`.
L'avantage qui en résulte:
"stoneValue[i] - meilleur avantage(i+1)»

2. **Deux pierres** – si `i+1 < n`
`stoneValue[i] + stoneValue[i+1] - bestAvantage(i+2)`

3. ** Trois pierres** – si 'i+2 < n`
`stoneValue[i] + stoneValue[i+1] + stoneValue[i+2] - bestAvantage(i+3)`

Le joueur choisira le **maximum** parmi ces trois options car les deux jouent de manière optimale.

3.3. En bas Vers le haut

Nous calculons `bestAdvantage` de droite à gauche (`i = n-1 ... 0`).
Chaque étape ne dépend que des trois états suivants, de sorte que nous pouvons conserver **seulement les trois dernières valeurs** au lieu d'un tableau entier de taille `n`.

> **Pourquoi 3 valeurs? **
> La répétition utilise `i+1`, `i+2` et `i+3`.
> Un tampon circulaire de taille 3 suffit.

Cela donne **O(n)** temps et **O(1)** espace auxiliaire.

---

- Oui. 4. Le Code : trois langues

> Chaque implémentation suit la même logique, juste avec la syntaxe spécifique à la langue et les appels de bibliothèque standard.

*(Se référer aux blocs de code dans la section "Solutions" ci-dessus.) *

### 4.1. Pourquoi C'est le "Good"

- **Simplicité** : PDD clair à un passage avec seulement quelques lignes à l'intérieur de la boucle.
- **Efficacité**: Poigne la taille maximale d'entrée (5.104) confortablement.
- **L'espace optimisé**: Seulement 3 entiers sont stockés, donc l'utilisation de la mémoire est négligeable.
- ** Universellement accepté**: Fonctionne en Java, Python et C++—grand pour coder des interviews où le choix de la langue compte.

#### 4.2. L'erreur : les cas de bord et les idées fausses

Qu'est-ce qui peut mal se passer ? Correction
- Oui.
En supposant que toutes les pierres sont positives conduit à de mauvais choix. La récurrence DP soustrait déjà le meilleur avantage de l'adversaire, donc il gère naturellement les négatifs. Autres
**Utiliser `int` débordement**="stoneValue[i]` jusqu'à 1000, totaliser jusqu'à 3 000, mais avec de nombreuses différences de piles peut atteindre ~5·107 → toujours dans 32-bit.=" Toujours sûr dans 32-bit, mais utiliser 64-bit si vous êtes paranoïaque. Autres
**Les erreurs hors-par-un dans `(i+1) % 3` vs `i % 3` peuvent corrompre le tampon. Cliquer sur le motif affiché dans le code: stocker résultat dans `dp[i % 3]`. Autres
**Miss-reading the problem**= Confusant la prise 1, 2 ou 3= avec la prise au plus 3= (même chose, mais certains résolveurs pensent que vous devez toujours prendre 3). Vérifier explicitement les limites: `si (i + 1 < n)`, etc. Autres

Oui. L'Ugly: Récursion Naïve & TLE

Une approche typique des débutants :

'`python
def helper(i):
i >= n: retourner 0
best = -inf
somme = 0
pour k dans la plage (1,4):
i + k <= n:
somme += pierre Valeur[i + k - 1]
best = max(meilleur, somme - aide(i + k))
le meilleur retour
«» "

- **Complexité temporelle**: Expanentielle ('O(3^n)') due à la recomputation des mêmes états.
- **Dépassement de l'emplacement**: Pour les grandes "n", profondeur de récursion > 104 souffle la pile.
- **Résultat**: rapports LeetCode **Délai dépassé** (TLE) pour des entrées même modestes.

La partie laid est la mémoisation ** inadéquate**: si vous ne mémorisez que le meilleur résultat mais pas la différence, vous perdez la perspective de l'adversaire et finissez avec une logique incorrecte.

---

- Oui. 5. Une preuve rapide de l'exactitude

**Claim:** Le DP bottom-up décrit ci-dessus rend le gagnant optimal exact.

**Proof Sketch:**

1. **Cas de base**: Pour `i ≥ n`, `bestAdvantage(i) = 0` (pas de pierres à gauche). C'est exact.
2. **Étape inductive**: Supposons que nous connaissons correctement `bestAdvantage(i+1)`, `bestAdvantage(i+2)`, `bestAdvantage(i+3)`.
À partir de l'index `i`, le joueur choisit parmi les 3 mouvements autorisés.
En soustrayant l'adversaire `bestAdvantage`, nous calculons l'avantage net pour le joueur actuel.
Prendre le **maximum** assure l'optimalité contre un adversaire rationnel.
Par conséquent, `bestAdvantage(i)` est correct.
3. **Termination**: Nous remplissons tous les indices jusqu'à 0, donc `bestAdvantage(0)` est correct.
4. **Détermination du gagnant**: Le signe `bestAdvantage(0)` correspond au score le plus élevé. *

---

- Oui. 6. Comment utiliser ceci dans une entrevue

1. ** Expliquer l'avantage net d'abord**: Montrez que vous n'êtes pas seulement codant, vous êtes *comprendre* le problème.
2. ** Tirer la récurrence sur un tableau blanc** : Même si vous écrivez du code plus tard, le visuel aide les intervieweurs à suivre votre raisonnement.
3. **Afficher l'astuce du tampon 3 éléments**: Beaucoup d'intervieweurs l'adorent parce qu'il démontre la connaissance de **l'optimisation de l'espace**.
4. **Mentionner le tableau de bord**: Un rapide coup d'œil à la table révèle que vous avez pensé aux pièges.
5. **Enveloppez-vous avec : Par exemple, si vous pouviez prendre jusqu'à 4 pierres, vous auriez juste augmenter la taille du tampon. Cette flexibilité impressionne.

---

- Oui. 7. Conclusion

Stone Game III peut ressembler à un jeu simple, mais c'est un exemple de manuel de programmation dynamique **optimale-stratégie**. La clé est de penser en termes de différence *score*, d'écrire une récurrence propre, et de mettre en œuvre un PDD ascendant optimisé dans l'espace.

**À emporter pour les entrevues :**

- Parlez de *avantage net* avant de coder.
- Utiliser un tampon circulaire pour l'espace "O(1)".
- Soulignez que les négatifs sont traités automatiquement.
- Éviter la récursion naïve; au lieu d'expliquer pourquoi votre DP est optimal.

Sentez-vous confiant: vous pouvez aborder Stone Game III (et des problèmes similaires) avec une solution concise et éprouvée dans n'importe quelle langue supérieure. Bonne chance pour briser cette prochaine interview de codage ! C'est ce qu'il a dit.

---

- Oui. 8. Références et lectures supplémentaires

- Problème de LeetCode 1406 – [Stone Game III](https://leetcode.com/problèmes/stone-game-iii/)
- Programme concurrentiel 4 - Chapitre sur la théorie du jeu DP**
- Programmation dynamique – Une introduction simple – GeeksforGeeks
- Interview Warm‐Up: DP Problèmes – Plateforme de pratique gratuite de Pramp

---


---

> **Vous voulez des plongées plus profondes? **
> Abonnez-vous à notre bulletin d'information pour relever les défis de la préparation des entrevues hebdomadaires et laissez-vous aller à ces questions difficiles du PDD ensemble.