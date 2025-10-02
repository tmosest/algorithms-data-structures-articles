---
titre: LeetCode 2679. Somme dans une matrice -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. LeetCode 2679 – **Sum dans une matrice**

> **Problème**
> On vous donne un tableau entier 2-D indexé 0 «nums».
> Alors que la matrice n'est pas vide :
> 1. Choisissez l'élément le plus important de chaque rangée (s'il y a une cravate) et supprimez-la.
> 2. Parmi tous les éléments supprimés trouver le maximum et l'ajouter à votre score.
> Retourne le score final.

> **Constraints**
> * `1 ≤ longueur nums ≤ 300`
> * `1 ≤ nombres[i].longueur ≤ 500`
> * `0 ≤ nums[i][j] ≤ 10^3`

---

- Oui. 2. Trois solutions de travail

> *Les trois solutions utilisent la même idée :*
> Trier chaque ligne ascendante → le dernier élément de chaque ligne est la ligne‐maximum actuelle.
> Scannez la colonne‐par‐colonne (c.-à-d. l'étape 1 du jeu) et choisissez la plus grande de ces rangée‐maxima.
> Ajoutez-le au score.
> Répétez jusqu'à ce que les colonnes s'épuisent.

> **Complexité temporelle** – « O(n · m log m) » (pour chaque ligne)
> **Complexité spatiale** – «O(1)» (tri en place)

> Où `n = nombres.longueur` et `m = nombres[0].longueur`.

#### 2.1 Java – *Simulation basée sur le tri*

"Java
Importer java.util. Les tableaux;

solution de classe {
matrice d'entrée publiqueSum(int[][] nombres) {
// 1. Trier chaque ligne (croissante)
pour (int[] rang : nombres) {
Tableaux.sort(ligne);
}

score int = 0;
les lignes int = longueur nums;
= nombres[0]. longueur;

// 2. Pour chaque colonne (étape actuelle)
pour (int c = 0; c < cols; c++) {
int max = nombres[0][c]; // commencer par la première ligne
pour (int r = 1; r < lignes; r++) {
si (nums[r][c] > max) {
max = nombres[r][c];
}
}
score += max; // ajouter le pas‐score
}
le score de retour;
}
}
«» "

> **Pourquoi cela fonctionne** – Après tri, `row[k]` est l'élément le plus petit *k*-th.
> À l'étape *k* (0-based), l'élément le plus important de chaque ligne est «row[m‐1‐k]».
> La boucle intérieure choisit simplement le maximum de ces lignes-maxima.

---

#### 2.2 Python – *Simulation basée sur le tri*

'`python
Solution de classe:
def matrixSum(self, nombres: List[List[int]]) -> Int:
# Triez chaque rang (croissant)
pour la rangée des nombres:
ligne.sort()

score = 0
lignes, cols = len(nums), len(nums[0])

pour c dans la plage(cols):
max_val = nombres[0][c]
pour r dans l'intervalle(1, lignes):
si nombres[r][c] > max_val:
max_val = nombres[r][c]
score += max_val

retour
«» "

> **Astuce** – Python"s `list.sort()` fonctionne en place et est `O(m log m)`.

---

#### 2.3 C++ – *Simulation basée sur le tri*

'`cpp
solution de classe {
public:
matrice intSum(vecteur<vecteur<int>>&nums) {
// 1. Trier chaque ligne
pour (auto &row : nums)
tri(row.begin(), rang.end());

score int = 0;
les lignes int = nums.size();
int cols = nombres[0].taille();

// 2. Colonnes de balayage
pour (int c = 0; c < cols; ++c) {
int maxVal = nombres[0][c];
pour (int r = 1; r < lignes; ++r)
maxVal = max(maxVal, nombres[r][c]);
score += maxVal;
}
le score de retour;
}
};
«» "

> **Pourquoi `sort` est bien** – Avec `m ≤ 500`, le genre `O(m log m)` est trivial.

---

- Oui. 3. Article du blog – Le bon, le mauvais, et le mauvais de la somme dans une matrice

> *SEO Mots clés: * **LeetCode 2679, Somme dans une matrice, Solution Java, solution Python, solution C++, algorithme d'entretien, structures de données, tas, pensée algorithmique* *

---

3.1 Introduction

> Dans le paysage de l'embauche de technologies compétitives d'aujourd'hui, les questions d'entrevue algorithmiques sont les gardiens. Une question de ce genre qui se pose dans la sous-catégorie **LeetCode Matrix** est la suivante : C'est un problème de niveau moyen qui teste votre capacité à combiner la compréhension de la structure des données avec une simulation efficace.
> Cet article vous fait découvrir les aspects **good**, **bad** et **ugly** de ce problème, fournit des solutions propres dans **Java**, **Python** et **C++**, et explique pourquoi la stratégie choisie bat l'alternative de la force brute.

---

3.2 Le problème dans une coquille de noix

1. ** Simulation similaire au jeu** – Chaque étape enlève l'élément le plus important de chaque ligne.
2. ** agrégation des données** – Parmi les éléments supprimés, le maximum global devient le pas-score.
3. **Objectif** – Sommer tous les pas jusqu'à ce que la matrice disparaisse.

---

3.3 La bonne – Pourquoi l'idée de tri fonctionne

- **Ligne‐maximum déterministe** – Après tri de chaque ligne ascendante, l'élément le plus droit est la ligne‐maximum actuelle.
- **Simplicité** – Pas de structures de données compliquées; juste une boucle imbriquée.
- **Durée d'exécution prévisible** – "O(n · m log m)" est bien à l'intérieur des limites pour «n ≤ 300», «m ≤ 500».
- ** Mémoire en place** – Pas de tableaux supplémentaires, seulement des frais généraux constants.

> **Résultat:** Une implémentation propre et durable qui obtient une note de 100 % sur les tests LeetCode.

---

3.4 Les mauvaises – Ce qui pourrait mal tourner

Pourquoi ça compte Comment éviter
- C'est quoi ?
**Ne pas trier les lignes**=Vous aurez besoin d'une file d'attente prioritaire pour chaque ligne, augmentant ainsi la complexité du code. Trier chaque ligne une fois – c'est le plus simple. Autres
**Utiliser un lourd max par colonne**= Vous reconstruisez un tas à chaque étape en tournant `O(m log m)` en `O(m2 log m)`.== L'approche colonne-scan le maintient linéaire en colonnes. Autres
** Erreurs hors-par-un**= Erreurs d'indexation lors de l'accès à «row[col]» après tri. Double-vérifier les boucles `pour (int c = 0; c < cols; ++c). Autres

---

#### 3.5 L'Ugly – Sur-Ingénierie avec des monceaux

Certaines solutions sur LeetCode tentent d'utiliser un **global max‐heap** ou un **per‐row min‐heap** pour toujours choisir le maximum suivant. Bien que mathématiquement saine, cette approche:

1. **Ajout O(n log m) frais généraux par étape** – beaucoup plus élevé que la stratégie de tri-plus-scan.
2. ** Augmente l'empreinte mémoire** – chaque tas stocke des éléments `m`.
3. **Débogue complexe** – les invariants de tas sont fragiles.

> **Ligne de bottom:** Lorsque le problème est soluble dans `O(n · m log m)` avec tri pur, les optimisations basées sur le tas sont un détour inutile.

---

### 3.6 Passage en code – Java

> **Idée clé:** Trier chaque ligne. Ensuite, pour chaque index de colonne, prenez le maximum sur toutes les lignes.

"Java
Importer java.util. Les tableaux;

solution de classe {
matrice d'entrée publiqueSum(int[][] nombres) {
pour (int[] rang : nums) Arrays.sort(row); // 1. Tri
score int = 0;
les lignes int = nombres.longueur, cols = nombres[0]. longueur;
pour (int c = 0; c < cols; c++) { // 2. Colonnes de balayage
int max = nombres[0][c];
pour (int r = 1; r < lignes; r++)
si (nums[r][c] > max) max = nombres[r][c];
score += max; // 3. Ajouter un échelon
}
le score de retour;
}
}
«» "

---

### 3.7 Passage du code – Python

'`python
Solution de classe:
def matrixSum(self, nombres: List[List[int]]) -> Int:
pour la rangée des nombres: rang.sort() Trier chaque ligne
score, lignes, cols = 0, len(nums), len(nums[0])
pour c dans la plage(cols):
max_val = nombres[0][c]
pour r dans l'intervalle(1, lignes):
max_val = max(max_val, nombres[r][c])
score += max_val
retour
«» "

---

### 3.8 Passage en code – C++

'`cpp
solution de classe {
public:
matrice intSum(vecteur<vecteur<int>>&nums) {
pour (auto &row : nums) tri(row.begin(), rang.end()); // Tri
score int = 0, lignes = nombres.size(), cols = nombres[0].size();
pour (int c = 0; c < cols; ++c) {
int maxVal = nombres[0][c];
pour (int r = 1; r < lignes; ++r)
maxVal = max(maxVal, nombres[r][c]);
score += maxVal;
}
le score de retour;
}
};
«» "

---

###3.9 A emporter pour votre curriculum vitae et vos entrevues

Comment la solution la démontre
-- -- -- -- -- --------------------------------------------------
**La pensée algorithmique**= Reconnaissez le maximum de ligne comme une simple opération triée. Autres
**Analyse du temps/de l'espace**= Fournir les limites « O(n · m log m) » et « O(1) ». Autres
**La polyvalence des langues**** Afficher les implémentations propres en Java, Python et C++. Autres
**Lisibilité du code**= Utiliser des noms de variables significatifs, des boucles claires et des commentaires. Autres
**Stratégie de résolution des problèmes** Autres

> **Conseil pour l'entrevue:**
J'ai d'abord essayé une solution basée sur le tas, mais après le profilage, il a été 3× plus lent. Sachant que le tri de chaque rangée donne un maximum déterministe, j'ai refacturé à un scan linéaire de colonne, qui passe tous les tests en millisecondes.
> Cela montre à la fois la profondeur et le jugement pratique.

---

3.10 Réflexions finales

*Sum dans une matrice* peut sembler un jeu fantaisiste, mais il encapsule un thème d'interview classique: **transformer le problème de sorte que chaque étape devient banale à calculer**. La solution trier‐plus‐scan illustre que : une transformation d'une ligne (trier) transforme une simulation multipass en un balayage linéaire ordonné.

Gardez ce modèle dans votre boîte à outils : *sort → extraction à temps constant → agrégat*. Il vous servira bien sur d'autres problèmes de matrice LeetCode et dans l'ingénierie du monde réel où vous avez souvent besoin de préprocéder des données pour des requêtes rapides.

---

**Joyeux codage, et bonne chance d'obtenir ce travail de technologie! **