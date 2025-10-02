---
titre: LeetCode 2297. Jeu de saut VIII -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
* 2297. Jeu de saut VIII – La solution complète (Java-Python-C++)
### Un guide bon, mauvais et ingénieux + SEO-Optimized Blog Post

---

### TL;DR
La langue Idée clé Complexité
C'est pas vrai.
**O(n)** temps, **O(n)** espace
**Python**
**C++**=Caisse monotonique + DP=** **O(n)** temps, **O(n)** espace

Le problème se résume à : pour chaque indice `i`, vous pouvez sauter **une fois** (ou zéro fois) à l'élément *next* plus grand ou *next* plus petit qui satisfait la règle de l'écart qui augmente strictement.
Une fois que nous connaissons la seule cible possible pour chaque indice, le reste est un DP classique: `dp[i] = min(dp[j] + cost[i])` sur tous autorisés `j` qui peuvent atteindre `i`.

Ci-dessous sont des implémentations propres, prêtes à la production dans **Java, Python et C++** suivi d'un billet de blog SEO qui explique l'intuition, les pièges et les compromis.

---

- Oui. 1. Le problème (réaffirmé)

> **Don**
> - `nums[0...n‐1]` – la hauteur de chaque indice
> - `coûts[0...n‐1]` – coût d'atterrissage sur cet indice
>
> **Vous commencez à l'index 0** et pouvez sauter de `i` à `j` (`i < j`) si l'un des suivants tient:
> 1. `nums[i] ≤ nums[j]` **et** chaque élément entre eux est ** strictement plus petit** que "nums[i]".
> 2. `nums[i] > nums[j]` **et** chaque élément entre eux est **plus grand ou égal** à "nums[i]".
> **Objectif:** atteindre l'indice «n‐1» avec le coût total minimal (somme des «coûts» de chaque indice débarqué, sauf le début).

**Contraintes**: «1 ≤ n ≤ 105», «0 ≤ nums[i], coûts[i] ≤ 105».

---

- Oui. 2. Intuition et observation

1. **Au plus un saut sortant par indice** –
Si vous pouvez sauter de `i` à deux indices différents `j1` et `j2`, alors les deux conditions ne peuvent pas les deux tenir. Cela garantit que le graphique des sauts possibles est une collection ** de chaînes dirigées**.

2. **Seul l'élément de qualification suivant est important** –
Pour le cas croissant, vous n'avez besoin que de l'élément *next* qui est **≥ nums[i]**; tous les premiers seraient bloqués par un nombre plus petit.
De même, pour le cas décroissant, vous avez besoin de l'élément *next* qui est **< nums[i]**.

3. **Les piles monotoniques** nous donnent exactement les éléments suivants dans le temps linéaire.

4. ** Programmation dynamique** –
Une fois que nous connaissons le seul prédécesseur autorisé pour chaque indice, `dp[i]` est le coût minimum pour atteindre "i":
`dp[i] = min(dp[prev] + coûts[i])` sur tous les `prev` qui peuvent sauter à `i`.
Parce que chaque indice a un prédécesseur **=1** dans chaque direction, la transition est insignifiante.

---

- Oui. 3. Détails de la mise en œuvre

Histoire Autres
C'est pas vrai.
**Java**Utilisez `ArrayDeque<Integer>` comme pile. `long[] dp` pour éviter les débordements (`coûts` jusqu`à 105 et `n` jusqu`à 105 → 1010). Autres
**Python**= Liste en tant que pile (`append`, `pop`). `float('inf')` pour les valeurs dp initiales. Autres
**C++**"vector<long>`, `vector<int>` comme piles. `numeric_limits<long long>:max()` pour INF. Autres

3.1 Java – Monotonique Pioche + DP

"Java
Importation de java.util.*;

solution de classe publique {
Coût(s) total(s), coût(s) total(s)
int n = longueur nums;
INF long = Long.MAX_VALUE / 4; // éviter le débordement en compléments
long[] dp = nouveau long[n];
les tableaux.fill(dp, INF);
dp[0] = 0; // point de départ ne coûte rien

Deque<Integer> incStack = nouveau ArrayDeque<>(); // pile décroissante pour la suivante >=
Deque<Integer> decStack = nouveau ArrayDeque<>(); // augmenter la pile pour la suivante <

pour (int i = 0; i < n; i++) {
// Cas 1: nombres[i] >= nombres[stack.peek()] → sauter de pile.top() à i
alors que (!incStack.isEmpty() && nums[i] >= nums[incStack.peek()] {
int j = incStack.pop();
dp[i] = Math.min(dp[i], dp[j] + coûts[i]);
}
// Décision 2: nombres[i] < nombres[stack.peek()] → sauter de pile.top() à i
alors que (!decStack.isEmpty() && nums[i] < nums[decStack.peek()]) {
int j = decStack.pop();
dp[i] = Math.min(dp[i], dp[j] + coûts[i]);
}

le point i) est remplacé par le texte suivant:
dcStack.push(i);
}
retour dp[n - 1];
}
}
«» "

---

3.2 Python – Stack monotonique + DP

'`python
de taper l'importation Liste
importations

Solution de classe:
def minCoût(même, nombres: Liste[int], coûts: Liste[int]) -> Int:
n = len(nums)
INF = 10 ** 18
dp = [INF] * n
dp[0] = 0

inc_stack = [] # pile pour la suivante >= (monotonique décroissante)
dec_stack = [] # pile pour la suivante < (augmentation de la monotonie)

pour i dans la plage(n):
alors qu'inc_stack et nums[i] >= nums[inc_stack[-1]]:
j = inc_stack.pop()
dp[i] = min(dp[i], dp[j] + coûts[i])

alors que déc_stack et nums[i] < nums[dec_stack[-1]]:
j = dec_stack.pop()
dp[i] = min(dp[i], dp[j] + coûts[i])

inc_stack.append(i)
dec_stack.append(i)

retour dp[-1]
«» "

---

### 3.3 C++ – Pile monotonique + DP

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
longue minCoût(vecteur<int> et nombres, vecteur<int> et coûts) {
int n = nombres.size();
INF = LLONG_MAX / 4;
vecteur <long> dp(n, INF);
dp[0] = 0;

vector<int> incStack; // pile décroissante pour la suivante >=
vector<int> decStack; // augmenter la pile pour la suivante <

pour (int i = 0; i < n; ++i) {
pendant que (!incStack.vide() && nums[i] >= nums[incStack.back()]) {
int j = incStack.back();
incStack.pop_back();
dp[i] = min(dp[i], dp[j] + coûts[i];
}
pendant que (!decStack.vide() && nums[i] < nums[decStack.back()]) {
int j = decStack.back();
decStack.pop_back();
dp[i] = min(dp[i], dp[j] + coûts[i];
}
incStack.push_back(i);
dcStack.push_back(i);
}
retour dp.back();
}
};
«» "

---

- Oui. 4. Billet de blog – Le bon, le mauvais, et le lamentable du jeu de saut VIII

> **Titre:** *Jump Game VIII: Des piles monotoniques à O(n) DP – Un guide complet*
> **Mots clés:** LeetCode 2297, Jeu de saut VIII, Programmation dynamique, Monotonic Stack, Java, Python, C++, Prép d'entrevue, Algorithme Analyse

---

Introduction

LeetCodeS *Jump Game VIII* (Problème 2297) se trouve au niveau de difficulté de moyenne, mais sa torsion sur le narratif classique du jeu de saut peut faire monter des codeurs même assaisonnés. La clé est de reconnaître que chaque indice a ** au plus un** saut sortant dans chaque direction, grâce aux règles strictes de "gap". Cette observation transforme un problème apparemment lourd de graphs en un PDD rangé qui peut être résolu en **O(n)** temps en utilisant des piles **monotoniques**.

Laissez-nous disséquer ce qui rend ce problème **bon**, quels pièges (le **bad**) se cachent sous, et où la solution peut devenir **ugly** si nous ne sommes pas prudents.

---

C'est vrai. Les bonnes

1. **Linear Time & Space**
L'approche de la pile monotonique garantit le temps d'exécution `O(n)` et l'espace auxiliaire `O(n)`. Ceci est critique pour les contraintes données (`n ≤ 105`).

2. **Single Pass, deux piles**
En traitant les indices de gauche à droite et en maintenant deux piles (une en baisse, une en hausse), nous pouvons gérer simultanément les transitions *suivant plus grand* et *suivant plus petit* sans rétrotraçage.

3. **Clean DP Transition* *
Comme chaque indice a au plus un prédécesseur dans chaque direction, la récurrence du PDD se réduit à une seule opération «min». Pas besoin de boucles imbriquées ou de suivi d'état complexe.

4. **Language-agnostique**
La même logique se traduit parfaitement par Java, Python, et C++, ce qui en fait une excellente solution d'entretien portable.

---

C'est vrai. Les mauvais

1. ** Risque de dépassement**
`costs[i]` peut être jusqu'à `105` et vous pouvez chaîner jusqu'à `105` sauts. Utiliser `int` pour `dp` débordera. Toutes les implémentations utilisent `long`/`long` et une valeur INF sûre.

2. **Incompréhension de la croissance *
C'est facile à confondre plus ou égaliser avec plus strictement. La première condition du problème permet l'égalité ('nums[i] ≤ nums[j]'). La logique de la pile doit préserver l'inégalité correcte lors de l'apparition.

3. **Délibérations**
- Quand `n = 1`, la réponse est trivialement `0`.
- Lorsque le premier élément ne peut atteindre aucun autre indice (par exemple, un tableau qui diminue strictement), le DP reste à INF pour les indices inaccessibles – le code doit gérer cela avec grâce.

4. ** Empreinte mémoire* *
L'utilisation d'un `Deque<Integer>` ou `vector<int>` pour les piles peut coûter plus de mémoire si vous poussez tous les indices. Cependant, les piles ne grandissent jamais au-delà de `n`, de sorte que la mémoire totale reste `O(n)`.

---

C'est vrai. L'Ugly

1. **Difficile de lire sans commentaires**
La logique à deux piles semble cryptique à première vue. L'ajout de commentaires en ligne ou d'un diagramme dans le code de production améliore grandement la maintenance.

2. **Défauts de commande de piles* *
Si vous poussez des indices sur la mauvaise pile ou oubliez de mettre à jour `dp[i]` avant de pousser, la solution devient silencieusement incorrecte, ce qui est plus difficile à déboguer parce que toutes les transitions se produisent en un seul passage.

3. **Non-monotonique Exécution* *
Une approche naïve qui scanne le tableau pour l'élément de qualificatif « suivante » pour chaque indice (O(n2)) est techniquement correcte, mais elle sera temporelle. Évitez de telles solutions quadratiques à moins que vous soyez dans un cadre d'entrevue très limité.

4. **Copier-Pâtisserie* *
Dans les entrevues, les gens copient souvent la plaque de chaudière sans ajuster les tailles d'INF ou de piles, ce qui entraîne des bugs subtils.

---

### Exemple d'étape par étape

> **Array**: «nombres = [2, 1, 4, 3]»
> **Coûts**: "coûts = [0, 5, 2, 1]"

Indice Empoigné de `incStack`? Empoigné de `decStack`?
Il n'y a pas de lien entre les deux.
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
0 + 5 = 5'
Pop (1) → `dp[2] = 5 + 2 = 7'
2 – Pop (2) → `dp[3] = 7 + 1 = 8'

Résultat: `dp[3] = 8` – le coût minimum pour atteindre le dernier indice.

Un diagramme rapide peut aider les lecteurs à visualiser les deux chaînes dirigées.

---

Les pensées finales

Jump Game VIII met en valeur la beauté des réductions algorithmiques: un problème qui se sent comme un graphe traversant est, avec la bonne observation, un DP classique résolu avec deux piles monotoniques. Gardez un oeil sur le nombre entier, les inégalités et les cas de bord pour éviter le *mauvais* et ajoutez des commentaires clairs pour apprivoiser le *mauvais*.

Bon codage, et que vos sauts soient toujours minimes!

---

### Références & Lecture supplémentaire

- LeetCode 2297 – [Déclaration de problème](https://leetcode.com/problèmes/jump-game-iv/)
* Introduction aux piles monotoniques* – [GeeksforGeeks] (https://www.geeksforgeeks.org/stack-data-structure/)
- * Programmation dynamique 101* – *Cracking the Coding Interview*, 7e édition.

---

**Auteur:** [Votre nom] – Coach d'entrevue, Algorithm Enthusiast, contributeur Open Source.
**Contact:** `youremail@exemple.com "

---

- Oui. 5. Liste de contrôle finale

- [ ] Utilisez `long`/`long long` pour éviter les débordements.
- [ ] Assurez-vous que l'état pop de la pile respecte `=" vs `<`.
- [ ] Poignée `n] 1' immédiatement.
- [ ] Ajouter des commentaires ou des diagrammes pour clarifier le code d'entrevue ou de production réel.
- [ ] Tester contre les cas aléatoires, en particulier les tableaux de bord (en augmentation ou en diminution).

Avec cela, vous êtes entièrement équipé pour affronter *Jump Game VIII* dans n'importe quel paramètre d'entrevue et tout langage de programmation que vous préférez. Bon codage !

---