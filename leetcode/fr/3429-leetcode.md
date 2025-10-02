---
titre: LeetCode 3429. Maison de peinture IV -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3429. **Paint House IV** – Solution complète dans **Java, Python, C++** + SEO-Optimized Blog

---

### TL;DR
- Oui. Le problème est un PDD 2 dimensions sur des paires de maisons qui sont équidistantes des extrémités.
- État: `dp[i][prevL][prevR]` – coût minimal pour les premières paires `i`, où `prevL` est la couleur de la maison `i‐1` sur le côté gauche, et `prevR` est la couleur de la maison `n‐i` sur le côté droit.
- Récurrence : choisissez les couleurs `cL` et `cR` pour la paire actuelle qui respecte
* `cL != prevL` (pas de même adjacent à gauche)
* `cR != prevR` (pas de même adjacent à droite)
* 'cL != cR` (des maisons équivalentes doivent être différentes)
Réduire au minimum le coût[i][cL] + le coût[n‐1‐i][cR] + dp[i+1][cL][cR]».
- Complexité: **O(n · 144)** (= O(n)), mémoire **O(n · 16)** → convient facilement pour `n ≤ 1e5`.

Vous trouverez ci-dessous la mise en œuvre complète dans les trois langues demandées.

---

- Oui. 1. Solution Java

"Java
Importation de java.util.*;

solution de classe publique {
Inf = Long.MAX_VALUE / 4; // éviter le débordement

public long minCoût(int n, coût int[]) {
la moitié int = n / 2;
// dp[i][prevL][prevR] – indices de couleur prev: 0,12 ou 3 (aucune)
long[][] dp = nouveau long[moitié + 1][4];
pour (int i = 0; i <= moitié; i++) {
pour (int a = 0; a < 4; a++) {
les tableaux.fill(dp[i][a], INF);
}
}
dp[demi][3][3] = 0; // boîtier de base: plus de paires pour peindre

pour (int i = moitié - 1; i >= 0; i--) {
Int gauche Idx = i;
Int droite Idx = n - 1 - i;
pour (int prevL = 0; prevL < 4; prevL++) {
pour (int prevR = 0; prevR < 4; prevR++) {
longue meilleure = INF;
pour (int cL = 0; cL < 3; cL++) {
si (cL == prevL) continue; // adjacent à gauche
pour (int cR = 0; cR < 3; cR++) {
Si (cR == prevR) continue; // à droite adjacente
Si (cL == cR) continue; // équidistant
long cand = coût[leftIdx][cL] + coût[rightIdx][cR] + dp[i + 1][cL][cR];
si (cand < best) best = cand;
}
}
dp[i][prevL][prevR] = meilleur;
}
}
}
retour dp[0][3][3];
}

// Pour des tests rapides
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
[]] coût1 = {{35,7},{6,2,9},{4,8,1},{7,3,5}};
Système.out.println(sol.minCoût(4, coût1)); // 9

[[]] coût2 = {{2,4,6},{5,3,8},{7,1,9},{4,6,2},{3,5,7},{8,2,4}};
Système.out.println(sol.minCoût(6, coût2)); // 18
}
}
«» "

---

- Oui. 2. Solution Python

'`python
importations
de taper l'importation Liste

INF = 10**18

Solution de classe:
def minCost(self, n: int, coût: List[List[int]]) -> Int:
moitié = n // 2
# dp[i][prevL][prevR]
dp = [[[INF] * 4 pour _ dans l'intervalle(4)] pour _ dans l'intervalle(demi + 1)]
dp[demi][3][3] = 0 # cas de base

pour i dans l'intervalle(demi - 1, -1, -1):
gauche, droite = i, n - 1 - i
pour prevL dans la plage(4):
pour prevR dans la plage(4):
meilleure = INF
pour cL dans l'intervalle(3):
si cL == prevL: # même que le voisin gauche
poursuivre
pour cR dans la plage(3):
si cR == prevR: # même que le voisin droit
poursuivre
si cL == cR: # les maisons équidistantes doivent différer
poursuivre
cand = coût[gauche][cL] + coût[droit][cR] + dp[i + 1][cL][cR]
si cand < meilleur:
meilleur = cand
dp[i][prevL][prevR] = meilleur
retour dp[0][3][3]


si __nom__ == "__main__" :
sol = Solution()
print(sol.minCost(4, [[3,5,7],[6,2,9],[4,8,1],[7,3]]) # 9
print(sol.minCost(6, [[2,4,6],[5,3,8],[7,1,9],[4,6],[3,5,7],[8,2,4]) # 18
«» "

---

- Oui. 3. Solution C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long minCoût(int n, vecteur<vecteur<int>>&coût) {
Const longue longue INF = 4e18; /
la moitié int = n / 2;
// dp[i][prevL][prevR] – indices de couleur prev: 0,12 ou 3 (aucune)
vecteur<vecteur<vecteur<vecteur<long>>> dp(demi + 1,
vecteur<vecteur<long>>(4, vecteur<long>(4, INF));
dp[demi][3][3] = 0; // scénario de base

pour (int i = moitié - 1; i >= 0; --i) {
Int gauche = i;
Int droite = n - 1 - i;
pour (int prevL = 0; prevL < 4; ++prevL) {
pour (int prevR = 0; prevR < 4; ++prevR) {
longue longue meilleure = INF;
pour (int cL = 0; cL < 3; ++cL) {
si (cL == prevL) continue; // même que le voisin gauche
pour (int cR = 0; cR < 3; ++cR) {
si (cR == prevR) continue; // même que le voisin droit
si (cL == cR) continuer; // les maisons équidistantes doivent différer
long cand = coût[gauche][cL] + coût[droit][cR] + dp[i + 1][cL][cR];
best = min(meilleur, cand);
}
}
dp[i][prevL][prevR] = meilleur;
}
}
}
retour dp[0][3][3];
}
};
«» "

---

- Oui. 4. Article de blog – Maison de la peinture IV: Le bon, le mauvais, et l'hugly

> **Titre:** Maison de peinture IV – Un guide complet de la solution de DP optimale
> **Meta Description:** Master LeetCodeS Paint House IV problème. Apprenez le bon, le mauvais et le mauvais des solutions DP, avec le code en Java, Python et C++.

---

Introduction

Si vous avez déjà lutté avec **LeetCodeS_________________, vous n'êtes pas seul. Le défi est d'une simplicité trompeuse – des maisons peintes de trois couleurs – mais les contraintes (pas de même maisons adjacentes *et* pas de même couleur pour les paires équidistantes) jettent une torsion que beaucoup de solutions de mémorisation descendantes manquent.

Dans cet article, nous disséquerons le problème sous trois angles:

1. **Le Bon** – Que faire dès le début.
2. **Le mauvais** – Pièges communs qui conduisent à des délais ou des réponses incorrectes.
3. **L'Ugly** – Manipulation avancée des boîtiers qui voyage parfois jusqu'à des codeurs assaisonnés.

Nous avons terminé avec des implémentations polies dans **Java, Python et C++** que vous pouvez déposer directement dans votre prép d'interview.

---

### Le problème (Récapitulation rapide)

Compte tenu d'un nombre pair de `n` de maisons et d'une matrice de coûts de 3 couleurs `[n][3]`, peindre chaque maison de telle sorte que:

1. **Aucune maison adjacente ne partage la même couleur. **
2. **Aucune maison qui soit équidistante des extrémités ne partage la même couleur. **

Retourner le coût total de la peinture **.

---

## Le bon : un PDD de 2 dimensions sur les paires

C'est vrai. Pourquoi des paires ?

Parce que la troisième contrainte couples maisons qui siègent *symétrie* autour du tableau. Au lieu de traiter chaque maison de façon indépendante, nous traitons **paires**: maison `i` et maison `n‐1‐i`. La peinture d'une paire à la fois garantit que la contrainte équidistante est appliquée **once**.

Conception de l'État

"dp[i][prevL][prevR] "

- `i` – nombre de paires déjà traitées (à partir de l'intérieur externe).
- `prevL` – la couleur utilisée pour le voisin gauche de la maison actuelle gauche (`i‐1`).
- `prevR` – la couleur utilisée pour le voisin droit de la maison droite actuelle (`n‐i`).
- Oui. Nous ajoutons un indice factice `3` pour représenter la couleur précédente (utilisée au tout premier appel).

Avec 3 couleurs réelles + 1 mannequin, nous avons seulement **4 × 4 = 16** possibles "prevL, prevR` combinaisons par paire. Ça garde la table DP minuscule.

Transition

Pour chaque paire `(i, n‐1‐i)` choisir les couleurs `cL` et `cR` de telle sorte que

«» "
cL != prevL // voisin gauche
cR != prevR // voisin droit
cL != cR // maisons équidistantes différentes
«» "

Le coût ajouté est «coût[i][cL] + coût[n‐1‐i][cR]».
Ajouter le coût de la solution optimale pour la paire *next*: `dp[i+1][cL][cR]`.

Texte
dp[i][prevL][prevR] = min {
Coût[i][cL] + coût[n‐1‐i][cR] + dp[i+1][cL][cR]
pour tous les cL, cR valides
}
«» "

Complexité

- Les boucles internes itèrent plus de 3 × 3 choix de couleurs pour chaque état.
- Avec 16 états par paire → **144 opérations par paire**.
- Pour `n = 100 000` c'est < 15 millions d'opérations primitives → bien en dessous de la limite de 1 seconde.

---

Pourquoi le DP naïf fait faillite

- Oui. 1. Ignorer la contrainte équivalente

Beaucoup de solutions pour la première fois ne vérifient que les maisons adjacentes.
Ils peindreont joyeusement `i` et `n‐1‐i` de la même couleur, causant une liaison inférieure ** incorrecte**.

- Oui. 2. Utiliser seulement un PDD de 1 dimension

Traiter le problème comme une maison de peinture classique dans une ligne ignore la *symétrie*.
Le PDD qui en résulterait serait **O(n3)** et impossible pour les contraintes données.

- Oui. 3. Récursion avec mémorisation 1-D

Un mémo en haut vers le bas qui ne stocke que la maison actuelle et la dernière couleur de ce côté oublie la dernière couleur du côté *droit*, conduisant à des états illégaux répétés.

---

- Oui. L'horrible: les cas de bord qui vous voyagent vers le haut

Qu'est-ce qui peut mal tourner
- C'est quoi ?
**Indice du poids** (`3`)= Oublier d'initialiser `dp[moitié][3]=0`.= Ajouter le cas de base explicitement. Autres
**Dépassement**= Le cumul de deux coûts `int` et `INF` peut déborder `int`.= Utiliser `long` / `long` partout et un `INF` sûr. Autres
**Limites de l'image**= Utiliser `n-1-i` quand `i` atteint le centre pour `n` impair (mais le problème garantit même). Assurer `n % 2 == 0' avant de procéder, ou simplement faire confiance à l'entrée. Autres
**Temps limite** Exclusivité 3×3 boucles dans 4×4 états → 144 ops par paire. Pour 100 000 maisons, c'est 14,4 millions d'ops. Certaines langues de haut niveau peuvent atteindre la limite de 2 secondes. Utilisez le PDD itératif ascendant, évitez les frais généraux et précalculez les indices de coûts. Autres

---

Les pensées finales

La beauté de Paint House IV se trouve dans la paire DP**: une fois que vous réalisez que la troisième contrainte est une condition de miroir, le problème s'effondre dans un petit espace d'état.

Pour les intervieweurs, la clé à retenir est le raisonnement **État-transition**:

1. Quelles informations antérieures ai-je besoin ? → couleurs des deux voisins adjacents.
2. Quelles sont les contraintes supplémentaires qui existent?
3. Combien d'états?

Si vous pouvez expliquer ce raisonnement, vous allez clouer le problème dans n'importe quelle entrevue.

---

Prêt à coder ?

Copiez la solution de votre langue préférée à partir de la section "Solution" ci-dessus, lancez-la contre les exemples de cas, et sentez-vous confiant que vous avez cloué Paint House IV!

Bon codage ! C'est ce qu'il a dit.

---

**Tags:** `LeetCode`, `DP`, `Dynamic Programming`, `Java`, `Python`, `C++`, `Algorithme`, `Préparation d'entretien "
**Auteur:** *Votre nom – Algorithme Enthousiaste et ingénieur logiciel*
**Date:** *2024‐04‐27*

---

*Pour des explications plus détaillées, n'hésitez pas à me faire du ping sur Twitter @YourHandle ou laisser un commentaire sur l'article. *