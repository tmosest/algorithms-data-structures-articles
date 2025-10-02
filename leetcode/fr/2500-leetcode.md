---
titre: LeetCode 2500. Supprimer la plus grande valeur de chaque ligne -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Supprimer la plus grande valeur de chaque ligne – LeetCode 2500
C++ – Fast, Clean & Interview‐ Solutions prêtes**

---

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Greedy Insight & Algorithm] (#greedy-insight-&-algorithm)
3. [Complexité temporelle et spatiale] (#complexité temporelle et spatiale)
4. [Points saillants de la mise en œuvre](#mise en œuvre-faits saillants)
* Java
* Python
* C++
5. [Bien, mal et mal à l'aise – Ce que les recruteurs se soucient de] (#bon, mal à l'aise)
6. [Conseils d'entrevue et questions fréquemment posées](#interview-tips)
7. [Résumé optimisé du SEO](#seo-summary)
8. [Références et lectures supplémentaires](#références)

---

## Aperçu du problème <a name="problem-overview"></a>
On vous donne une grille **m × n** d'entiers positifs. Effectuez à plusieurs reprises l'opération suivante jusqu'à ce que la grille soit vide:

1. **Supprimer** la plus grande valeur de chaque ligne (s'il y a une cravate).
2. **Ajouter** le maximum de toutes les valeurs supprimées à un total courant.

Rends le total final.

> **Exemple**
> grille = `[[1,2,4],[3,3,1]]` → Réponse = **8**
> (Supprimer `4` & `3` → ajouter `4`; Supprimer `2` & `3` → ajouter `3`; Supprimer `1` & `1` → ajouter `1`).

**Contrôles* *
- `1 ≤ m, n ≤ 50`
- `1 ≤ grille[i][j] ≤ 100`

---

## Greedy Insight & Algorithme <un nom></a>
Lorsque les lignes sont ** triées en ordre ascendant**, la suppression *k*‐th supprime toujours l'élément dans la colonne *k*‐th de la ligne triée.
Ainsi, la valeur maximale supprimée dans le *k*‐th round correspond au maximum dans la colonne *k*‐th de la grille **triée**.

**Algorithme**
1. **Trier chaque rangée** en ordre ascendant.
2. Pour chaque index de colonne `j` (0 ... n‐1):
* Trouver `max(grid[i][j]` pour toutes les lignes `i`.
* Ajouter ce maximum à la réponse.
3. Retourne la réponse.

Il s'agit d'une simulation cupide classique; il n'est pas nécessaire d'effectuer une rétro-traque ou un PDD.

---

## Complexité temporelle et spatiale <un nom</a>
Formule métrique Raison
C'est quoi, ça ?
**Temps**=1 `O(m · n · log n)=1 Le tri de chacune des lignes `m` coûte `O(n log n)`; la numérisation de toutes les colonnes coûte `O(m · n)`. Autres
**Espace** Le tri est effectué en place; seules quelques variables auxiliaires sont utilisées. Autres

Avec `m, n ≤ 50`, cela satisfait facilement les limites.

---

## Faits saillants de la mise en oeuvre <un nom</a>
Voici les solutions **ready‐to-copy** en Java, Python et C++.
Chaque mise en œuvre suit la même approche O(m · n · log n).

### Java

"Java
Importer java.util. Les tableaux;

solution de classe {
public int supprimerGreatestValue(int[][] grille) {
int m = longueur de la grille;
int n = grille[0].longueur;
= 0;

// Trie chaque rang ascendant
pour (int[] ligne : grille) {
Tableaux.sort(ligne);
}

// Pour chaque colonne, choisissez la plus grande valeur parmi toutes les lignes
pour (int col = 0; col < n; col++) {
nt colMax = 0;
pour (int rang = 0; rang < m; rang++) {
colMax = Math.max(colMax, grille[ligne][col]);
}
Total += colMax;
}

le total des retours;
}
}
«» "

Python

'`python
de taper l'importation Liste

Solution de classe:
Supprimer GreatestValue(self, grille: List[List[int]]) -> Int:
# Trier chaque rangée (en place)
pour la ligne de la grille:
ligne.sort()

Total = 0
n = len(grid[0])
pour le col dans la plage(n):
col_max = max(row[col] pour la ligne de la grille)
Total += col_max

retour total
«» "

C++

'`cpp
solution de classe {
public:
int supprimer Grande valeur(vecteur<vecteur<int>>& grille) {
int m = quadrillage.size();
int n = grille[0].taille();
= 0;

// Trier chaque ligne
pour (auto &row : grille)
tri(row.begin(), rang.end());

// Numériser les colonnes
pour (int col = 0; col < n; ++col) {
nt colMax = 0;
pour (int rang = 0; rang < m; ++ rang)
colMax = max(colMax, grille[ligne][col]);
Total += colMax;
}

le total des retours;
}
};
«» "

> **Pourquoi le tri est-il suffisant? * *
> Après le tri, chaque élément de ligne s'efface à la ronde *k* est simplement l'élément à l'index *k*.
> L'algorithme transforme ensuite le processus en un simple balayage maximal en colonne.

---

## Good, Bad & Ugly – Ce que les recruteurs se soucient de <a name</a>
Catégorie Ce que les recruteurs recherchent
-- -- -- -- -- -- -- -- -- -- -- --
**Bien** - Code clair auto-documenté<br>- Pas de suringénierie (p. ex., pas de tas à moins que nécessaire)<br>- Poignées cas de bord (`m==1`, `n==1`) naturellement - L'utilisation du tri intégré maintient la complexité minimale
**Bad** - Hypothèses codées en dur (p. ex., grille toujours rectangulaire) - Supposons que toutes les rangées ont la même longueur; gardez-vous contre l'entrée mal formée.
**Ugly**- Simulation manuelle avec des files d'attente ou des tas, ajoutant des frais généraux inutiles de log-factor<br>- Utilisation de variables globales ou d'entrées mutantes de manière surprenante.

**Ligne de bottom:** La solution *sort‐and‐scan* est concise, rapide et conforme aux attentes des interviews pour un problème de simulation gourmand.

---

## Conseils d'entrevue et questions fréquemment posées <un nom></a>
1. ** Expliquer le choix avide**: Les lignes de commande garantissent que la suppression k-th est toujours l'élément de la colonne k-th. (en milliers de dollars)
2. **Discuss alternatives**: Mention des files d'attente prioritaires (max-heaps) par rangée comme une approche valide mais plus lente.
3. ** Contrôle de complexité**: Montrez que `O(m·n·log n)` satisfait aux contraintes (`- 50 × 50`).
4. **Champs d'application**: épreuve `[[1]]`, `[[5,5],[5,5]`, `[[1,100],[100,1]]`.
5. **Demander des éclaircissements**: Si l'énoncé du problème est ambigu (p. ex., tout élément supprimé si tie), confirmez avec l'intervieweur.

---

## SEO-Optimized Summary <a name="seo-summary"></a>
> **Supprimer la plus grande valeur de chaque ligne – LeetCode 2500**
> Maîtrisez ce problème avide facile à résoudre avec des solutions concises Java, Python et C++.
> Apprenez l'algorithme optimal `O(m·n·log n)`, comprenez pourquoi le tri des lignes fonctionne, et voyez comment éviter les pièges communs.
> Parfait pour la pratique *coding interview*, *Java solution*, *Python solution*, *C++ solution*, *LeetCode interview prep* et *greedy algorithme* sujets.

Utilisez cet article pour booster votre blog technique, as votre interview LeetCode, et présenter une implémentation propre et prête à l'entretien.

---

## Références & Lecture supplémentaire <un nom="références"></a>
- [LeetCode 2500 – Supprimer la plus grande valeur de chaque ligne](https://leetcode.com/problems/delete-greatest-value-in-each-row/)
- [Greedy Algorithms – YouTube Playlist](https://www.youtube.com/playlist?list=PLcR2n8XkK1kR0Wm4w2Y1k9R6Yy2Y)
- [Traitement vs priorité] Demandes d'arbitrage](https://stackoverflow.com/questions/1577611/who-to-use-heap-vs-sort)

---

N'hésitez pas à adapter les extraits de code, à les exécuter sur votre environnement local et à pratiquer les points de discussion. Bonne chance dans votre prochain entretien de codage!