---
titre: LeetCode 1564. Mettre des boîtes dans l'entrepôt I -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## -Placer des boîtes dans l'entrepôt I – Le guide complet
*(Code à gauche) 1564 – Medium – Interview-Ready Solution en Java, Python & C++*

> **Meta‐Description** – Voulez-vous ace LeetCodes Ce post vous permet de parcourir l'intuition, une solution O(n log n) gourmande et un code entièrement testé en Java, Python et C++. Apprenez les approches *good*, *bad* et *ugly* et augmentez votre CV d'entrevue avec des mots-clés optimisés SEO: **LeetCode, gourmand, tri, entrepôt, boîtes, algorithme, interview**.

---

- Oui. 1. Aperçu du problème

On vous donne deux tableaux :

* "boîtes" – hauteurs des boîtes de largeur unitaire.
* `entrepôt` – hauteurs de pièces consécutives (de gauche à droite).

Règles

1. Les boîtes ne peuvent pas être empilées.
2. Vous pouvez réorganiser les boîtes arbitrairement.
3. Les boîtes sont insérées de gauche à droite.
4. Si une boîte est plus grande qu'une chambre, elle et toutes les boîtes *derrière* elle sont arrêtées avant cette chambre.

**Objectif** – retourner le nombre maximum de boîtes qui peuvent être placées dans l'entrepôt.

> **Exemples**
> 1. `boxes=[4,3,4,1]`, `warehouse=[5,3,3,4,1]` → `3`
> 2. `boxes=[1,2,2,3,4]`, `warehouse=[3,4,1,2]` → `3`
> 3. `boxes=[1,2,3]`, `warehouse=[1,2,3,4]` → `1`

---

- Oui. 2. Contraintes

* `1 ≤ boîtes.longueur, entrepôt.longueur ≤ 105 "
* `1 ≤ boîtes[i], entrepôt[i] ≤ 109 "

Donc un algorithme **O(n log n)** est nécessaire ; tout ce qui est pire sera TLE.

---

- Oui. 3. L'approche Naïve/Bad

Une idée de force brute : essayez chaque permutation de "boxes" et simulez l'insertion.
*Complexité temporelle:* `O(n! · n)` – absolument impossible pour `n = 105`.
* Pourquoi il échoue :* L'espace d'état explose ; il n'y a pas de façon déterministe de décider quelle boîte va où sans explorer tous les ordres.

---

- Oui. 4. Le point de vue sur l'avidité

Pensez à l'entrepôt de ** de droite à gauche**.
En se déplaçant vers la gauche, la hauteur **minimum** de la pièce vue jusqu'ici détermine la hauteur d'une boîte dans ce segment.

* Construire un tableau `minPref[i]` = minimum de «entrepôt[0...i]».
* Tri des "boîtes" ascendantes.
* Départ de la pièce la plus droite (`i = entrepôt.longueur‐1`) et de la plus petite boîte (`j = 0`).
* Si `minPref[i] ≥ box[j]`, la boîte correspond → la placer, incréments compteurs.
* Déplacez-vous dans la salle suivante (i‐1) et la boîte suivante (j+1).
* Arrêtez quand les boîtes sont épuisées ou plus de chambres.

Cela fonctionne parce que:
* Nous essayons toujours d'insérer la plus petite boîte possible dans la pièce restante la plus restrictive (la plus basse avec la hauteur admissible).
* Si la plus petite boîte ne s'adapte pas, aucune boîte plus grande ne s'adaptera non plus, alors nous sautons cette pièce.

---

- Oui. 5. Algorithme (Code de Pseudo)

«» "
trier les boîtes ascendantes
construire minPref[0...m-1] // m = entrepôt.longueur
minPref[0] = entrepôt[0]
pour i = 1 ... M- 1
minPref[i] = min(minPref[i-1], entrepôt[i])

cnt = 0 // nombre de boîtes placées
i = m-1 // pièce courante (à droite)
j = 0 // boîte courante (à partir de la gauche)

alors que i >= 0 et j < boîtes.longueur
si minPref[i] >= boîtes[j]
cnt++
j++ // boîte de place
i-- // passer à la chambre précédente

retour cnt
«» "

**Complexités* *

*Time* – `O(n log n)` pour le tri + `O(n)` pour le préfixe + `O(n)` scan à deux points.
*Espace* – `O(n)` pour le tableau de préfixes (peut être `O(1)` si vous calculez à la volée).

---

- Oui. 6. Liste de contrôle des cas de bord

Autres Décision Pourquoi ça compte ?
- Oui.
Aucun carton à placer. Retourner immédiatement.
Empty `warehouse`
Autres Toutes les boîtes sont plus grandes que la première chambre.
Autres Toutes les pièces inférieures à la plus petite boîte

---

- Oui. 7. Code complet – Java, Python, C++

##### 7.1 Java (Compatible avec Java 17)

"Java
Importation de java.util.*;

solution de classe publique {
int public maxBoxesInWarehouse(int[] boîtes, entrepôt int[]) {
if (boîtes) == entrepôt null="null="boîtes.longueur== 0="warehouse.longueur== 0) {
retour 0;
}

Classer les boîtes ascendantes
les tableaux.sort(boîtes);

Construisez un préfixe min des hauteurs d'entrepôt
m = longueur de l ' entrepôt;
int[] minPref = nouvelle int[m];
minPref[0] = entrepôt[0];
pour (int i = 1; i < m; i++) {
minPref[i] = Math.min(minPref[i - 1], entrepôt[i]);
}

2-pointer scan avide
i = m - 1; // index de la pièce (de droite à gauche)
int j = 0; // index de la boîte (le plus petit au plus grand)
nombre int = 0;

pendant que (i >= 0 && j < cases.longueur) {
si (minPref[i] >= boîtes[j]) {
count++; // placer la boîte
j++; // la plus petite boîte suivante
}
i--; // passer à la chambre précédente
}
le nombre de retours;
}
}
«» "

7.2 Python 3

'`python
de taper l'importation Liste

Solution de classe:
def maxBoxesInWarehouse(self, boîtes: List[int], entrepôt: List[int]) -> Int:
si ce n'est pas une boîte ou un entrepôt:
retour 0

Boîtes de tri (croissantes)
box.sort()

# Construire le préfixe min de l'entrepôt
min_pref = [0] * len(entrepôt)
min_pref[0] = entrepôt[0]
pour i dans la gamme(1, len(warehouse)):
min_pref[i] = min(min_pref[i - 1], entrepôt[i])

i, j, nombre = len(entrepôt) - 1, 0, 0
alors que i >= 0 et j < len(boîtes):
si min_pref[i] >= les cases [j]:
nombre += 1
j += 1
I -= 1

Nombre de retours
«» "

#### 7.3 C++ (C++17)

'`cpp
#incluez <vecteur>
#incluez <algorithme>

solution de classe {
public:
int maxBoxesInWarehouse(std::vector<int>& boîtes, std::vector<int>& entrepôt) {
si (boîtes.vide()) warehouse.vide() retourne 0;

std::sort(boxes.begin(), boxes.end()); // ascendant

int m = entrepôt.taille();
à:vecteur<int> minPréf(m);
minPref[0] = entrepôt[0];
pour (int i = 1; i < m; ++i)
minPref[i] = md:min(minPref[i - 1], entrepôt[i];

i = m - 1, j = 0, nombre = 0;
pendant que (i >= 0 && j < cases.size()) {
si (minPref[i] >= boîtes[j]) {
+ nombre;
++j;
}
--i;
}
le nombre de retours;
}
};
«» "

---

- Oui. 8. Essais de mise en œuvre

'`python
♪ Exemple exécuté dans Python
sol = Solution()
print(sol.maxBoxesInWarehouse([4,3,4,1], [5,3,3,4,1]) # → 3
print(sol.maxBoxesInWarehouse([1,2,2,3,4], [3,4,1,2]) # → 3
print(sol.maxBoxesInWarehouse([1,2,3], [1,2,3,4)) # → 1
«» "

Les tests unitaires en Java/C++ suivent le même schéma – instantiate `Solution`, appelle la méthode, et affirme la sortie attendue.

---

- Oui. 9. Conseils d'entrevue

Sujet Ce que les intervieweurs recherchent Comment cette solution aide
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Greedy Raisonnement**
**Analyse de la complexité**= Expliquer `O(n log n)` tri et `O(n)` scanning (en anglais seulement) Afficher la connaissance des limites de temps/espace
**Cas d'escroquerie**
**Codage Style**
**Langage Adaptabilité**= Implémenter en Java/Python/C++=Remarquable polyvalence pour plusieurs piles de technologie==

---

- Oui. 10. Conclusion – Pourquoi ce code rocks

* **Simplicité** – La logique gourmande est facile à expliquer, vous pouvez donc l'articuler sur un tableau blanc.
* **Performance** – LeetCode répond à des limites strictes (éléments `105`) tout en restant très lisible.
* **Cross‐Language** – Fonctionne en Java, Python et C++ – parfait pour adapter votre CV à une pile technologique que vous ciblez.

**À emporter :** Maîtriser les boîtes de Put dans l'entrepôt L'entrepôt I est une vitrine de votre capacité à penser avide, à trier efficacement les données et à écrire un code propre et prêt à la production.

Bon codage ! C'est ce qu'il a dit.

---

Autres lectures
* LeetCode Discuter – [Simple solution Java](https://leetcode.com/problems/put-boxes-in-the-warehouse-i/solutions/5789805/simple-java-solution-by-sakshikishore-cwrh/)
* Algorithmes et structures de données – chapitre *Two-Pointer
* Préparation de l'entrevue – *Greedy Algorithm*

---

**Mots-clés** – LeetCode, boîtes à sous Dans l'entrepôt, algorithme gourmand, tri, deux pointeurs, Java, Python, C++, prép d'interview, interview d'algorithme, complexité temporelle, complexité spatiale.