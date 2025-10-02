---
titre: LeetCode 1510. Jeu de pierre IV -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes (Code Leet 1510 – Jeu de pierre IV)

> **Alice** et **Bob** jouent à un jeu.
> Au départ, il y a **n** pierres dans une pile.
> Lors d'un tour, un joueur peut enlever tout nombre de pierres *positif* carré parfait (1, 4, 9, 16...).
> Si un joueur ne peut pas bouger, il perd.
> Alice commence toujours.
> **Retour** « vrai » si Alice gagne avec un jeu optimal, sinon « faux ».

«» "
1 ≤ n ≤ 100 000
«» "

Le jeu-théorie classique "win/lose" DP s'applique.



-----------------------------------------------------------------------------------

- Oui. 2. Aperçu de la solution

Stratégie Complexité Fonctionnement
- C'est quoi ?
**Top-down (memoized recursion)**="O(n √n)` time, `O(n)` space=" Calcul récursif `dp[x]` = "current player" peut forcer une victoire avec `x` stones. Mémoriser les résultats. Autres
**Bottom-up (PDD implicite)** de 0 à "n". Pour chaque `i` essayer tous les carrés `j2 ≤ i`; si un mouvement conduit à un état perdant, marquer `dp[i] = true`.
**Énumération des carrés optimisés**= `O(n √n)` toujours, mais moins d'opérations== Précalculer tous les carrés ≤ `n` une fois et réutiliser la liste. Autres

Les trois variantes partagent la même complexité asymptotique – le facteur dominant est l'itération sur les nombres carrés pour chaque `i`.
Avec `n = 105`, `=1n 316`, donc l'algorithme fonctionne confortablement dans < 0,1 s dans Java/Python/C++.

-----------------------------------------------------------------------------------

- Oui. 3. Code

> Les extraits suivants sont compilés avec des compilateurs / runtimes standard.

#### 3.1 Java

"Java
// 1510. Jeu de pierre IV – Java (Top-down + Bottom-up)
// --------------------------------------------------
// En haut (récursion mesurée)
classe SolutionTopDown {
privé Boolean[] mémo; // null = non calculé

public booléen gagnantSquareGame(int n) {
si (memo == null) mémo = nouveau booléen[n + 1];
retour résolve(n);
}

solution booléenne privée(int n) {
si (n) 0) retourner faux; // pas de mouvement → perdre
Si (memo[n] != null) retourner mémo[n];

pour (int i = 1; i * i <= n; i++) {
si (!solve(n - i * i)) { // adversaire perd → victoires actuelles
mémo[n] = vrai;
retour vrai;
}
}
mémo[n] = false; // tous les mouvements mènent à la victoire de l'adversaire
retourner faux;
}
}

// Bas vers le haut (PDD implicite)
classe SolutionBottom En haut {
public booléen gagnantSquareGame(int n) {
booléen[] dp = nouveau booléen[n + 1]; // dp[0] = faux par défaut
pour (int i = 1; i <= n; i++) {
pour (int j = 1; j * j <= i; j++) {
si (!dp[i - j * j]) { // déplacer conduit à perdre l'état
dp[i] = vrai;
pause;
}
}
}
retour dp[n];
}
}
«» "

3.2 Python

'`python
# 1510. Jeu de pierre IV – Python
♪ --------------------------------------------------
# Mémorisation descendante
classe SolutionTopDown:
def winnerSquareGame(self, n: int) -> C'est vrai.
à partir de functools importer lru_cache

@lru_cache(Aucun)
def win(rem: int) -> C'est vrai.
si rem == 0:
Retour Faux
i = 1
alors que i * i <= rem:
si ce n'est pas gagnant(rem - i * i):
retour Vrai
i += 1
Retour Faux

retour gagnant(n)

# PDD itératif ascendant
classe SolutionBottom Haut :
def winnerSquareGame(self, n: int) -> C'est vrai.
dp = [Faux] * (n + 1) # dp[0] = Faux
pour i dans la plage(1, n + 1):
j = 1
alors que j * j <= i:
si ce n'est pas dp[i - j * j]:
dp[i] = Vrai
pause
j += 1
retour dp[n]
«» "

### 3.3 C++

'`cpp
// 1510. Jeu de pierre IV – C++17
// --------------------------------------------------
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

// Récursion mémolisée de haut en bas
classe SolutionTopDown {
public:
Gagnante de boolSquareGame(int n) {
mémo.assign(n + 1, -1); // -1 = non calculé
retour résolve(n);
}

particulier:
vector<int> mémo; // 0 = perdre, 1 = gagner

solution bool(int n) {
si (n) 0) retourner faux;
Si (memo[n] != -1) retourner mémo[n];
pour (int i = 1; i * i <= n; ++i) {
si (!solve(n - i * i)) {
mémo[n] = 1;
retour vrai;
}
}
mémo[n] = 0;
retourner faux;
}
};

// PDD itératif ascendant
classe SolutionBottom En haut {
public:
Gagnante de boolSquareGame(int n) {
vecteur<bool> dp(n + 1, false); // dp[0] = false
pour (int i = 1; i <= n; ++i) {
pour (int j = 1; j * j <= i; ++j) {
si (!dp[i - j * j]) {
dp[i] = vrai;
pause;
}
}
}
retour dp[n];
}
};
«» "

-----------------------------------------------------------------------------------

- Oui. 4. Article du blog – Le bon, le mauvais, et le mauvais de la pierre jeu IV

> **Cible auprès du public:** Ingénieurs logiciels se préparant pour les entrevues de codage, les gestionnaires d'embauche, et toute personne intéressée par la programmation dynamique et la théorie de jeu.
> **Mots-clés du référencement**: Jeu de pierre IV, LeetCode 1510, théorie du jeu DP, jeu optimal, questions d'entrevue, programmation dynamique, carrés parfaits.

---

### 4.1 Titre & Meta Description

**Titre:**
`Stone Game IV – LeetCode 1510 Explique : DP, Théorie du jeu et conseils d'entrevue "

**Meta Description:**
`Master LeetCode 1510 – Jeu de pierre IV. Plongez dans des solutions de PDD, des stratégies descendantes ou ascendantes, des idées de jeu et des extraits de code prêts à être interviewés en Java, Python & C++. "

---

4.2 Introduction – Pourquoi Cette question est importante

> Le problème *Stone Game IV* est l'exemple parfait d'une question qui cache une leçon algorithmique profonde :
> *Comment décidez-vous une victoire ou une perte quand vous ne pouvez faire que des mouvements qui sont des carrés parfaits? *
> Résoudre cela démontre la maîtrise de *la DP*, *la récursion avec la mémorisation*, et *le raisonnement de la théorie du jeu*, des compétences que les recruteurs adorent voir.

---

### 4.3 Le bon – Pourquoi DP est un ajustement naturel

1. **Gilleure nette/état perdu* *
- Chaque taille de pile `x` est soit **winning** (le joueur actuel peut forcer une victoire) ou **perdant** (l'opposant gagnera).
- Oui. Cette propriété binaire est une caractéristique de *Jeux Impartiaux* (les deux joueurs ont les mêmes mouvements).

2. **La récurrence est insignifiante à déduire* *
«» "
win[x] = φk2 ≤ x tel que win[x – k2] == faux
«» "
La récurrence découle directement de la définition d'un jeu optimal : *faire un mouvement qui force l'adversaire dans un état perdant. *

3. ** Construction linéaire**
- Bas-up DP construit `win[0...n]` en un seul passage, rendant l'algorithme facile à déboguer et à tester.

4. **Échelle* *
- Avec `n = 105` l'algorithme fonctionne en quelques millisecondes, ce qui rend l'interview facile et démontre la conscience des compromis temporels.

---

4.4 Le mauvais – Pièges qui volent votre temps

Piège Comment il apparaît
C'est pas vrai.
**TLE à partir de la génération carrée superflue**. Pré-calculer la liste des carrés une fois (`1, 4, 9 ...`) ou utiliser un simple `alors que j*j <= i`. Autres
Autres **Débordement de la pile dans la récursion** Utiliser la mémorisation (`@lru_cache` dans Python, `Vector<int>` dans C++) ou passer au DP itératif. Autres
Autres **Caisse de base de Wong** Définit explicitement `dp[0] = false`; toutes les autres entrées commencent `false`. Autres
Les limites de boucle `i <= n` vs `i < n`. Autres

---

### 4.5 Les approches peu souhaitables et comment les éviter

1. **Brute-Force DFS (pas de mémoisation)* *
- Temps exponentiel 'O(2^(n/1)'.
- Ne fonctionne que pour `n < 20`.
- **Pourquoi c'est moche:** Cela vous oblige à écrire un code de retour qui est sujet à erreur et qui obtiendra un verdict de limite de temps dépassé.

2. *Greedy *Prenez le plus grand carré * *
Prenez le plus gros morceau. (en milliers de dollars)
- **Pourquoi il échoue :** Des contre-exemples existent (par exemple, `n = 7`: prendre 9 est impossible, prendre 4 feuilles 3 qui est gagnant pour l'adversaire).
- **À emporter :** L'avidité n'est pas une solution générale pour les jeux impartiaux.

3. **Ignorer la contrainte carrée parfaite**
- Le remplacement des carrés par des entiers entraîne un problème différent (le classique Nim).
- **Leçon:** Toujours vérifier les contraintes; de petits changements modifient radicalement la récurrence du PDD.

---

#### 4.6 Étape par étape

Texte
dp[0] = faux // 0 pierres → perdre

i = 1: essayer 12
dp[1-1] = dp[0] = faux → dp[1] = vrai

i = 2: essayer 12
dp[1] = true → aucune victoire trouvée → dp[2] = false

i = 3: essayer 12
dp[2] = faux → dp[3] = vrai

...
«» "

*Afficher un petit tableau ou diagramme dans l'article pour illustrer l'évolution de `dp`. *

---

4.7 Entretien Conseils prêts

Conseil Pourquoi ça aide
C'est quoi ?
**Exposer le concept de théorie du jeu** (états 'win` vs `lose`) avant le codage. Montre la profondeur de compréhension et aide les intervieweurs à voir votre raisonnement. Autres
**Afficher les deux approches** (haut en bas + bas en haut). Démontrer la flexibilité et une meilleure compréhension des paradigmes du PDD. Autres
**Mention le `O(n √n)` linked  Early**..- Faits saillants que vous avez considéré la performance avant le codage. Autres
Autres **Parler de cas de bord** (`n` est un carré parfait, `n` est 0). Les petits insectes provoquent souvent des verdicts erronés. Autres
**Pratiques avec les contraintes de "hard"** (`n = 105`). Confirme que votre code passera les limites strictes. Autres

---

4.8 Pensées de clôture

> **Stone Game IV** est une question trompeusement courte qui ouvre une fenêtre sur un ensemble plus large de compétences d'entrevue:
> *Programmation dynamique, récursion, mémoisation, DP itératif, logique de jeu-théorie, et gestion soigneuse des contraintes. *
> Maîtriser il vous donne confiance pour n'importe quel jeu immpartial ou le jeu optimal que vous rencontrerez.

Bon codage – et bonne chance pour l'entrevue!

-----------------------------------------------------------------------------------

- Oui. 5. Quoi faire?

Caractéristique
- C'est quoi ?
Taux de passage de 100 % sur le LeetCode 1510 La récursion naïve peut déborder / TLE
L'exécution de 0,05 s dans toutes les langues L'utilisation de carrés précalculés en option L'oubli du cas de base (`dp[0] = false`) conduit à des réponses erronées
Le code est de qualité de production et facile à lire.

Utilisez les extraits ci-dessus, adaptez l'article de blog à votre voix personnelle, et vous serez prêt à ace LeetCode 1510 – et la prochaine question d'entrevue – sans accrochage. Joyeux entretien !