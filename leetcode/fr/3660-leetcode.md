---
titre: LeetCode 3660. Jeu de saut IX -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
N° de jeu de saut IX – Résoudre le LeetCode 3660 en Java, Python & C++
> Le bien, le mal et l'Ugly – Comment maîtriser ce problème de mi-difficulté *

> *Mots clés:* Jump Game IX, LeetCode 3660, Prefix‐Suffix Array, DP, Greedy, Question d'entrevue, Java, Python, C++, entretien de codage, structures de données, conception d'algorithmes

---

- Oui. 1. Récapitulation des problèmes

> **On vous donne un tableau entier `nums`.**
> De n'importe quel index `i` vous pouvez sauter à un index `j` selon:

Direction État Explication
- C'est quoi ?
< nombres[i] > Aller de l'avant seulement vers un élément **plus petit**
"j " i " , " nums [j] > nums [i] " Aller en arrière seulement vers un élément **large**

> **Objectif:** Pour chaque index `i`, trouvez la valeur maximale que vous pouvez atteindre en suivant toute séquence de sauts valides commençant par `i`. Retourner un tableau `ans` où `ans[i]` est cette valeur maximale accessible.

> **Constraints**
> - 1 ≤ longueur nominale ≤ 105 "
> - `1 ≤ nombres[i] ≤ 109`

---

- Oui. 2. Approche naïve

Une force brute DFS/BFS de chaque indice explorerait un nombre exponentiel de chemins:
"O(n2)" dans le pire des cas (chaque indice pourrait atteindre de nombreux autres).
Avec `n = 105`, c'est absolument impossible.

---

- Oui. 3. L'Insight – Préfixe / suffixe

1. **Prefix Max (`pre[i]`)** – l'élément le plus important de la sous-puce `[0 ... i]`.
Lorsque vous sautez à gauche, vous *toujours* vous retrouvez à la valeur maximale vue jusqu'à présent.

2. **Suffix Min (`suff[i]`)** – l'élément le plus petit de la sous-tribu.
Lorsque vous sautez à droite, vous devez atterrir sur un élément plus petit.
Par conséquent, l'élément *premier* que vous pouvez atteindre à droite est la plus petite valeur à droite.

3. **Pourquoi la comparaison `pre[i] > suff[i+1]` administratives**
- Si le plus grand nombre à gauche (`pre[i]`) est **plus grand** que le plus petit nombre à droite (`suff[i+1]`), vous pouvez *premier* sauter à gauche vers `pre[i]` (gagnant une plus grande valeur) et *alors* sautent droit à une position qui finit par atteindre "pre[i+1]".
- Sinon, vous ne pouvez pas profiter de sauter juste après un saut à gauche, donc le mieux que vous pouvez faire est simplement rester sur le côté gauche, vous donnant `pré[i]`.

Avec cette observation, nous pouvons calculer la réponse en un seul balayage en arrière.

---

- Oui. 4. Algorithme final (O(n) Temps, O(n) Espace)

Texte
Pré[0] = nombres[0]
pour i = 1 ... n-1:
Pré[i] = max(pré[i-1], nombres[i])

suff[n-1] = nombres[n-1]
pour i = n-2 ... 0:
suff[i] = min(suff[i+1], nombres[i])

ans[n-1] = pré[n-1]
pour i = n-2 ... 0:
ans[i] = pre[i] // commencer par le meilleur à gauche
Si pre[i] > suffi[i+1]: // saut à gauche peut être suivi d'un saut à droite
ans[i] = ans[i+1] // hériter du meilleur du bon côté
retour et
«» "

---

- Oui. 5. Analyse de la complexité

Complexité
C'est pas vrai.
**Heure**="O(n)" – passe unique pour calculer `pre`, passe unique pour `suff`, passe unique pour répondre. Autres
**L'espace**="O(n)"– trois tableaux entiers de longueur `n`. Autres

---

- Oui. 6. Cas de bord traités

- Tableau à éléments uniques → la réponse est l'élément lui-même.
- Tous les éléments augmentent strictement → vous ne pouvez sauter droit à des nombres plus petits, donc la réponse est juste le préfixe max.
- Tous les éléments diminuant strictement → vous ne pouvez sauter à gauche à des nombres plus grands, donc la réponse est le préfixe max ainsi.
- Valeurs répétées → l'algorithme fonctionne encore parce que les conditions sont des inégalités strictes (`<` / `>`).

---

- Oui. 7. Mise en œuvre du code

#### 7.1 Java

"Java
Importation de java.util.*;

solution de classe {
valeur(int[] nombres) {
int n = longueur nums;
int[] pre = nouvelle int[n];
int[] suff = nouvelle int[n];
int[] ans = nouvelle int[n];

pré[0] = nombres[0];
pour (int i = 1; i < n; i++) {
pre[i] = Math.max(pre[i - 1], nombres[i]);
}

suff[n - 1] = nombres[n - 1];
pour (int i = n - 2; i >= 0; i--) {
suff[i] = Math.min(suff[i + 1], nombres[i]);
}

ans[n - 1] = pre[n - 1];
pour (int i = n - 2; i >= 0; i--) {
ans[i] = pre[i];
si (pré[i] > suffi[i + 1]) {
as[i] = as[i + 1];
}
}
le retour des an;
}
}
«» "

7.2 Python

'`python
Solution de classe:
def maxValue(self, nombres: List[int]) -> Liste[int]:
n = len(nums)
Pré = [0] * n
suff = [0] * n
ans = [0] * n

Pré[0] = nombres[0]
pour i dans la plage (1, n):
Pré[i] = max(pré[i - 1], nombres[i])

suff[n - 1] = nombres[n - 1]
pour i dans la plage (n - 2, -1, -1):
suff[i] = min(suff[i + 1], nombres[i])

ans[n - 1] = pré[n - 1]
pour i dans la plage (n - 2, -1, -1):
ans[i] = pre[i]
si pre[i] > suff[i + 1]:
ans[i] = ans[i + 1]
retour et
«» "

### 7.3 C++

'`cpp
solution de classe {
public:
vector<int> maxValue(vector<int>& nums) {
int n = nombres.size();
vecteur <int> pre(n), suff(n), ans(n);

pré[0] = nombres[0];
pour (int i = 1; i < n; ++i)
b) Pré[i] = max(pré[i-1], nombres[i];

suff[n-1] = nombres[n-1];
pour (int i = n-2; i >= 0; --i)
suff[i] = min(suff[i+1], nombres[i];

ans[n-1] = pre[n-1];
pour (int i = n-2; i >= 0; --i) {
ans[i] = pre[i];
si (pré[i] > suffi[i+1])
ans[i] = ans[i+1];
}
le retour des an;
}
};
«» "

Les trois implémentations fonctionnent dans **O(n)** temps et **O(n)** espace auxiliaire, correspondant à la solution optimale.

---

- Oui. 8. Article de blog: -Le bon, le mauvais, et le bâillon de Jump Game IX

> **Cible Public:** Ingénieurs en logiciels de niveau intermédiaire, candidats à la préparation d'entrevues et tous ceux qui veulent maîtriser les problèmes de LeetCode pour les entrevues d'emploi.

8.1 Introduction

> Et si vous pouviez sauter sur les nombres dans un tableau aussi longtemps que vous suivez une règle simple? (en milliers de dollars)
> Code du leet 3660 – *Jump Game IX* – prend cette question et la transforme en un puzzle qui mélange le raisonnement avide, les astuces de préfixe et une touche d'intuition. Dans ce post, nous allons disséquer le problème, marcher à travers la solution élégante, et apprendre pourquoi maîtriser ce défi vous donne un avantage concurrentiel dans les entretiens techniques.

#### 8.2 Déclaration de problème (en anglais)

- Vous êtes à un indice dans une gamme d'entiers.
- Oui. Si vous voulez sauter **droit**, la cible doit être **plus petite** que votre valeur actuelle.
- Oui. Si vous voulez sauter **gauche**, la cible doit être **large**.
- Oui. Vous pouvez sauter en chaîne arbitrairement longtemps.
- Pour chaque indice de départ, quel est le nombre **maximum** sur lequel vous pouvez vous retrouver ?

### 8.3 L'approche Naïve «I‐Will‐DFS» (Pourquoi c'est mauvais*)

- **Complexité temporelle:** `O(n2)` (chaque index explore beaucoup d'autres).
- **Complexité spatiale:** "O(n)" pile de récursion ou file d'attente.
- Avec `n = 105`, le DFS/BFS exploserait vite.
- Les intervieweurs aiment vous voir penser au temps et à l'espace.

### 8.4 Le point de vue sur le bien: préfixe Max & suffixe Min.

1. **Prefix Max (`pre`)** – le meilleur que vous pouvez obtenir en sautant seulement vers la gauche.
Parce que chaque saut gauche a besoin d'un plus grand nombre, vous finirez inévitablement sur la plus grande valeur à gauche vue jusqu'à présent.

2. **Suffix Min (`suff`)** – le plus petit que vous pourriez rencontrer si vous sautez à droite.
Un saut droit nécessite un nombre plus petit ; le *premier* tel nombre que vous pouvez frapper est le minimum sur le côté droit.

3. ** Les combiner**
Si le plus grand nombre à gauche (`pre[i]`) est plus grand que le plus petit nombre à droite (`suff[i+1]`), vous pouvez *premier* prendre un saut à gauche vers `pre[i]` et puis un saut droit qui vous conduira à au moins `pré[i+1]`.
Sinon, vous êtes coincé à gauche, et `pre[i]` est la réponse.

### 8.5 L'Edge Ugly: Inégalités strictes et valeurs répétées

- Les conditions sont **strict** (`<` / `>`), pas `=" ou `≥`.
- Les numéros dupliqués ne vous aident pas à sauter; l'algorithme respecte toujours les règles strictes parce que nous utilisons seulement les comparaisons `max` et `min`, qui rejettent naturellement les duplicatas.

#### 8.6 Algorithme complet en un seul balayage

- Calculer `pre` dans une passe avant.
- Calculez "suff" dans une passe arrière.
- Résoudre la réponse par un scan en utilisant le tour de comparaison ci-dessus.

> **Heure:** `O(n) "
> **Espace:** `O(n)` (trois tableaux auxiliaires).
> C'est exactement ce que les intervieweurs attendent.

### 8.7 Afficher en plusieurs langues

- Les extraits de Java, Python et C++ démontrent que la même logique est le langage-agnostique.
- Mettre en évidence l ' utilisation de `Math.max` / `std::max`* et *`Math.min` / `std::min`* comme micro-optimisations.

8.8 Ce que les intervieweurs recherchent

- **Compréhension des problèmes** – reformuler clairement les règles.
- **Conception algorithmique** – expliquer pourquoi vous avez besoin de `O(n)` et non de `O(n2)`.
- **Clarté du code** – code lisible et bien commenté.
- **Conscience des cas** – démontrer que l'algorithme permet d'augmenter, de diminuer et de reproduire des séquences.
- **Les compromis entre l'espace temporel** – parler des tableaux auxiliaires et des mises à jour en place si vous êtes conscient de la mémoire.

### 8.9 Prise- Conseils pour votre prochaine entrevue

1. **Démarrer avec -Qu'est-ce que vous pouvez garantir sur la gauche ?** → `pre[i]`.
2. **Demander Quel est le premier obstacle à droite?
3. **Comparer et décider** – la comparaison est la ligne unique qui déverrouille le chemin optimal.
4. **Pratiquer un modèle similaire** – de nombreux problèmes LeetCode (p. ex., *Maximum Subarray*, *Sliding Window Maximum*) dépendent également de la précomputation préfixe/suffixe.

8.10 Mot final

Sauter le jeu IX n'est pas un simple puzzle ; c'est un **micro-cours dans l'élégance algorithmique**.
En transformant une recherche potentiellement exponentielle en un passage linéaire à travers des tableaux préfixes et suffixes, vous prouvez votre capacité à repérer les modèles et à écrire un code efficace – exactement ce que veulent les recruteurs et les gestionnaires d'embauche.

> ** Continuer à pratiquer**
> Essayez d'adapter le même modèle de préfixe/suffixe aux variations comme *=Jump Game VI=* ou *=Maximum Subarray avec One Deletion=*.
> Plus vous internalisez les modèles, plus vous vous sentirez confiant quand la prochaine question d'entrevue atterrira sur votre bureau.

---

- Oui. 9. Réflexions finales

- **Jump Game IX** présente la puissance de *simple structures de données* (préfixe/suffixe) pour résoudre des problèmes de recherche de chemin apparemment complexes.
- Oui. L'algorithme de linéarité n'est pas seulement une gentillesse théorique; c'est une nécessité pratique pour passer des interviews critiques dans le temps.
- La maîtrise de ce problème et la compréhension de son principe sous-jacent démontrent que vous pouvez traduire les contraintes de problème en code efficace – exactement ce que les entreprises de haute technologie valorisent.

Bonne chance avec vos entretiens ! C'est ce qu'il a dit.

---

> **Suivez-moi** pour des plongées plus approfondies dans les puzzles LeetCode, les stratégies d'entrevue et les défis de codage du monde réel.
Autres *Laissez un commentaire ci-dessous avec votre propre à emporter de Jump Game IX! *

---

Cette démarche complète non seulement résout le problème de manière efficace, mais le cadre également d'une manière qui soit prête à l'entrevue et favorable au référencement. Bonne chance, et que votre voyage de codage soit plein de * sauts intelligents*!