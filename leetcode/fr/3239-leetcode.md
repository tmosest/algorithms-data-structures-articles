---
titre: LeetCode 3239. Nombre minimum de flips pour rendre la grille binaire palindromique Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solution 3 langues pour LeetCode 3239
**Nombre minimal de flips pour rendre la grille binaire palindromique**

Langue Fichier / Classe Complexe
C'est quoi ?
**Java** espace
**Python** espace
**C++**="solution.cpp"="O(m·n)" time, `O(1)` espace

> *m = nombre de lignes, n = nombre de colonnes, 1 ≤ m·n ≤ 2·105*

---

#### 1.1 Java

"Java
// 3239. Nombre minimum de flips pour rendre la grille binaire palindromique – Java
solution de classe {
Int public minFlips(int[][] grille) {
int m = longueur de la grille;
int n = grille[0].longueur;

// flips nécessaires si on force chaque rangée à être un palindrome
ligne intFlips = 0;
pour (int i = 0; i < m; i++) {
pour (int j = 0; j < n / 2; j++) {
si (grid[i][j] != [i][n - 1 - j]) {
rowFlips++; // retourner une des deux cellules
}
}
}

// flips nécessaires si on force chaque colonne à être un palindrome
colFlips int = 0;
pour (int j = 0; j < n; j++) {
pour (int i = 0; i < m / 2; i++) {
si (grid[i][j] != (j) {
colFlips++; // retourner une des deux cellules
}
}
}

retour Math.min(rowFlips, colFlips);
}
}
«» "

---

#### 1.2 Python

'`python
# 3239. Nombre minimum de flips pour rendre la grille binaire palindromique – Python
def minFlips(grid):
m, n = len(grid), len(grid[0])

# flips pour que toutes les lignes soient palindromiques
ligne_flips = somme(
1 pour i dans la plage(m) pour j dans la plage(n // 2)
si grille[i][j] != de la grille [i] [n - 1 - j]
)

# flips pour que toutes les colonnes soient palindromiques
col_flips = somme(
1 pour j (n) pour i (m // 2)
si grille[i][j] != (j)
)

retour min(row_flips, col_flips)
«» "

---

*## 1.3 C++

'`cpp
// 3239. Nombre minimum de flips pour rendre la grille binaire palindromique – C++
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int minFlips(vecteur<vecteur<int>>& grille) {
int m = quadrillage.size();
int n = grille[0].taille();

ligne intFlips = 0;
pour (int i = 0; i < m; ++i) {
pour (int j = 0; j < n / 2; ++j) {
si (grid[i][j] != [i][n - 1 - j]) {
++Flips de rangée;
}
}
}

colFlips int = 0;
pour (int j = 0; j < n; ++j) {
pour (int i = 0; i < m / 2; ++i) {
si (grid[i][j] != (j) {
++colFlips;
}
}
}

retour min(rowFlips, colFlips);
}
};
«» "

---

- Oui. 2. Article de blog – Le bon, le mauvais, et le mauvais de LeetCode 3239

> **Mots clés**: Leetcode, palindrome de grille binaire, flips minimum, interview, algorithme, interview de codage, Java, Python, C++, interview d'emploi, défi de codage, pensée algorithmique, résolution de problèmes

---

2.1 Introduction

Lorsque vous vous préparez à des entrevues d'ingénierie logicielle, vous rencontrez souvent des problèmes de type «grid» qui testent votre capacité à penser en deux dimensions. LeetCode 3239, *Nombre minimum de flips pour faire du Binary Grid Palindromic*, est un parfait exemple : vous avez une matrice binaire et vous avez demandé de retourner le moins de cellules pour que **toutes les lignes ou toutes les colonnes deviennent palindromes**.

La déclaration semble simple, mais quelques points subtils en font un bon teaser d'interview-cerveau:

* Vous pouvez retourner ** n'importe quelle** cellule, pas seulement un côté d'une inadéquation.
* Vous devez décider **globalement**: soit des lignes cibles ou des colonnes cibles; vous ne pouvez pas mélanger les deux stratégies.
* La grille peut être aussi grande que 200 000 cellules, de sorte qu'un algorithme "O(m·n)" est la seule solution viable.

Laissez-les marcher à travers les parties "good", "bad" et "ugly" pour résoudre ce problème, et voyez comment les trois implémentations linguistiques ci-dessus incarnent une solution propre et prête à la production.

---

2.2 Le bon – La simplicité gagne

Ce que nous avons fait Pourquoi il est grand
C'est-à-dire
Chaque ligne (ou colonne) peut être vérifiée en comparant les paires symétriques `grid[i][j]` et `grid[i][n-1-j]`. S'ils diffèrent, retourner une cellule corrige cette paire. Autres
**Dénombrement indépendant**= Chaque paire d'anomalies est indépendante; le fait de retourner une cellule ne résout jamais deux anomalies différentes dans la même ligne ou colonne. Autres
**Single pass par direction**= Deux boucles imbriquées donnent "O(m·n)" temps. Pas de mémoire au-delà de quelques compteurs. Autres
**Le code lisible**Les versions Java, Python et C++ expriment toutes la même logique en boucles unilignes, ce qui facilite l'audit. Autres

Cette approche traduit directement le problème en un minimum d'opérations : pour chaque paire qui n'est pas déjà un palindrome, retourner une des cellules. Le nombre total de flips n'est que la somme des erreurs.

---

2.3 Les mauvaises – Pièges communs

Erreur d'explication
- C'est quoi ?
**Couvant les deux côtés d'une incompréhension** Flip seulement un; la paire devient égale. Autres
**Mixer les lignes et les colonnes**=Essai de retourner les cellules pour satisfaire simultanément les palindromes des lignes et des colonnes mène à une explosion combinatoire. Décidez **une fois**: soit toutes les lignes, soit toutes les colonnes. Autres
**Ignorer l'élément du milieu dans les rangées/colonnes de longueurs impaires**= L'élément du milieu n'a pas de partenaire; il n'a jamais besoin de basculer. Loop seulement jusqu'à `n/2` ou `m/2`. Autres
**Over-optimizing with bit-wise tricks**.L'utilisation de XOR ou de bits est inutile et peut occulter l'idée centrale. Collez à une simple comparaison entière. Autres
**Utiliser de l'espace supplémentaire pour les transposes**= Transposer la grille pour gérer les colonnes utilise la mémoire `O(m·n)`, qui est gaspillée. Il faut passer directement sur les colonnes. Autres

Éviter ces pièges maintient la solution maigre et compréhensible – exactement ce que les intervieweurs recherchent.

---

2.4 L'horrible – Arguments et interprétations erronées

Pourquoi c'est bizarre Comment nous l'avons géré
- C'est quoi ?
**Ligne unique ou colonne unique**La grille devient trivialement palindromique; vous pourriez essayer par erreur de compter les erreurs où il n'y en a pas. Nos boucles sautent naturellement les erreurs parce que `n/2` ou `m/2` est égal "0". Autres
**La plus grande grille (200 000 cellules)**= Une solution quadratique serait épuisée.= `O(m·n)` est linéaire dans le nombre de cellules, parfaitement acceptable. Autres
La réponse est `0`, mais une implémentation de buggy peut toujours retourner des valeurs positives. Nous résumons les erreurs, et avec des valeurs uniformes, la somme est zéro. Autres
**Parité de ligne/colonne mixte**= Si `m` est égal mais `n` est impair (ou vice-versa), vous pouvez faire un double comptage incorrect. Les boucles séparées pour les lignes et les colonnes gèrent la parité indépendamment. Autres
Autres **Lisant la déclaration de manière incorrecte**= Certains candidats pensent que vous pouvez retourner pour satisfaire simultanément les lignes et les colonnes, ce qui n'est pas ce que le problème demande. Énoncé clair : *retourner les flips minimums pour faire soit toutes les lignes palindromiques ** ou** toutes les colonnes palindromiques*. Autres

En prêtant une attention particulière à ces scénarios, les trois versions linguistiques restent robustes dans chaque cas de test que la plateforme LeetCode peut vous lancer.

---

#### 2.5 A emporter dans les langues croisées

Concept Java Python C++
C'est quoi, ça ?
**Structure de boucle**"pour (int j = 0; j < n / 2; j++)" – division entière explicite.
**Comptoir des Flips**="int rowFlips = 0;`– variable unique. "row_flips = 0` – simple entier. Autres
**Colonne Traversale**= Boucle extérieure sur colonnes, boucle intérieure sur lignes. Expressions de générateurs imbriqués. Des boucles doubles avec `i < m/2`. Autres
**Valeur de retour**"Math.min(rowFlips, colFlips)" – clean. Autres

Chaque implémentation est prête à être collée dans l'éditeur LeetCode et fonctionnera dans une fraction de seconde, même sur la plus mauvaise taille de grille. De plus, le code est facilement adaptable aux bases de code de production – si vous devez traiter un tableau booléen 2-D dans une application réelle, vous apprécierez l'empreinte minimale.

---

#### 2.6 À emporter pour le candidat en attente d'entrevue

1. **Traduisez le problème à un problème de comptage minimum** – Dépliez une cellule par paire d'anomalies.
2. **Décider la direction de la cible tôt** – vous ne pouvez pas mélanger les lignes et les colonnes; la réponse est le minimum des deux comptages indépendants.
3. **Continuer la mémoire** – itérer directement sur les colonnes; éviter de construire une transposition ou des tableaux supplémentaires.
4. ** Parité de la poignée automatiquement** – boucle uniquement à `n/2` ou `m/2`; les éléments intermédiaires de longueur impair sont naturellement ignorés.
5. ** Validation des boîtiers de bord** – ligne/colonne unique, grilles uniformes, grandes tailles d'entrée.

Lorsque vous articulez ces points dans une entrevue, vous démontrerez à la fois la perspicacité algorithmique et la discipline de codage pratique – qualités que les recruteurs aiment.

---

2.7 Conclusion

LeetCode 3239 est trompeurment simple une fois que vous retirez le fluff. La stratégie de comparaison **pair-wise** vous donne un algorithme propre 'O(m·n)` qui fonctionne dans les trois langues d'entretien les plus populaires.

Qu'il s'agisse d'un ingénieur Java, d'un Pythonista ou d'un développeur C++, le motif est le même : *compter les erreurs, choisir la direction avec le plus petit nombre, et la renvoyer*.

Ainsi, la prochaine fois que vous verrez un problème de grille de "flip to palindrome", rappelez-vous les trois prises de vue ci-dessus et vous sentirez confiant que vous pouvez l'aborder, peu importe comment le panel d'entrevue cadre la question. Bon codage, et bonne chance pour votre prochain entretien technique!