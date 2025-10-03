---
titre: LeetCode 2087. Coût minimum Accueil d'un robot dans une grille -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. LeetCode 2087 – Coût minimum Accueil d'un robot dans une grille
### Solution avide d'un seul liner (espace O(1), temps O(========================)

"Java
// Java 17
solution de classe {
public int minCost(int[] startPos, int[] home Pos,
Int[] rangCoûts, int[] colCoûts) {
Int r = 0;
// Mouvements verticaux
si (startPos[0] < homePos[0]) {
pour (int i = startPos[0] + 1; i <= homePos[0]; ++i) r += rowCoûts[i];
} sinon si (startPos[0] > homePos[0]) {
pour (int i = startPos[0] - 1; i >= homePos[0]; --i) r += rangCoûts[i];
}

c = 0;
// Mouvements horizontaux
si (startPos[1] < homePos[1]) {
pour (int i = startPos[1] + 1; i <= homePos[1]; ++i) c += colCoûts[i];
} sinon si (startPos[1] > homePos[1]) {
pour (int i = startPos[1] - 1; i >= homePos[1]; --i) c += colCoûts[i];
}

retour r + c;
}
}
«» "

'`python
# Python 3.10
Solution de classe:
def minCoût(même, startPos, homePos, rowCoûts, colCoûts):
r = 0
# coût vertical
si startPos[0] < homePos[0]:
r += somme(ligneCoûts[startPos[0] + 1 : homePos[0] + 1])
elif startPos[0] > homePos[0]:
r += somme(rowCoûts[homePos[0] : startPos[0])

c = 0
# coût horizontal
si startPos[1] < homePos[1]:
c += somme(colCoûts[startPos[1] + 1 : homePos[1] + 1])
elif startPos[1] > homePos[1]:
c += somme(colCoûts[homePos[1] : startPos[1]])

retour r + c
«» "

'`cpp
// C++17
solution de classe {
public:
int minCoût(vecteur<int> et début Pos, vecteur<int>& chez soi Pos,
vectorielle<int>& rowCoûts, vectorielle<int>& colCoûts) {
coût long = 0;

// Mouvements verticaux
si (startPos[0] < homePos[0]) {
pour (int i = startPos[0] + 1; i <= homePos[0]; ++i) coût += rangCoûts[i];
} sinon si (startPos[0] > homePos[0]) {
pour (int i = startPos[0] - 1; i >= homePos[0]; --i) coût += rangCoût[i];
}

// Mouvements horizontaux
si (startPos[1] < homePos[1]) {
pour (int i = startPos[1] + 1; i <= homePos[1]; ++i) coût += colCoûts[i];
} sinon si (startPos[1] > homePos[1]) {
pour (int i = startPos[1] - 1; i >= homePos[1]; --i) coût += colCoûts[i];
}

retourner static_cast<int>(coût);
}
};
«» "

> **Pourquoi cela fonctionne** –
> Chaque chemin valide doit visiter *chaque ligne* entre `startRow` et `homeRow` et chaque colonne entre `startCol` et `home Colonel.
> Déplacer dans n'importe quel ordre ne peut jamais éviter de payer le coût de ces lignes/colonnes, de sorte que le coût total est indépendant de la forme de chemin spécifique. L'algorithme avide accumule simplement les coûts obligatoires en ligne et en colonne.

---

- Oui. 2. Article du blog
*(SEO-optimized, interview-friendly, "Good, Bad & Ugly" panne)*

Titre
> **LeetCode 2087 – Coût minimum d'accueil : Une solution simple d'avidité en Java, Python et C++ (Interview-Ready)* *

- Oui. Méta description
> Apprenez la solution d'espace O(1) pour LeetCode 2087. Comprendre pourquoi une somme gourmande de coûts de ligne/colonne est optimale, découvrir des cas de bord, et se préparer pour les questions de codage-entrevue.

Table des matières
1. [Présentation du problème](#problème-aperçu)
2. [Solution intuitive de l'axe des pays] (#solution intuitive)
3. [Proof & Complexité de Correctness] (#correctness)
4. [Pièges communs – Les mauvais] (# mauvais)
5. [Les cas d'escroquerie – Les Ugly] (#ugly)
6. [Approches alternatives (BFS / Dijkstra)](#alternatives)
7. [Sample Test Cases & Unit Tests] (#tests)
8. [Traitement pour la réussite de l'entrevue] (#Traitement)

---

### Aperçu du problème

> **LeetCode 2087 – Coût minimum d'un robot dans une grille* *
> Un robot commence à `startPos = [r1, c1]` dans une grille 2-D et doit atteindre `homePos = [r2, c2]`.
> Il peut seulement déplacer **up/down** (ligne de changement) ou **gauche/droite** (colonne de changement).
> **Chaque coût de déplacement** dépend uniquement de la ligne ou de la colonne *entrée*:
> - Déplacement dans une nouvelle ligne "i" coûts "rowCosts[i]".
> - Déplacement dans une nouvelle colonne `j` coûts `colCoûts[j]`.
> `rowCosts` a la longueur `m`, `colCosts` a la longueur `n`.
> Trouvez le coût total *minimum* du robot pour atteindre sa maison.

Contraintes:
- `1 ≤ m, n ≤ 105`
- Tous les coûts sont des entiers non négatifs.

---

Solution intuitive d'avidité

1. **Déplacements verticaux** – marcher de `r1` à `r2`.
*Si `r2 > r1`* → somme `rowCoûts[r1+1 ... r2]`.
*Si `r2 < r1`* → somme `rowCoûts[r1-1 ... r2]`.
2. **Déplacements horizontaux** – marcher de `c1` à `c2`.
*Si `c2 > c1`* → somme `colCoûts[c1+1 ... c2]`.
*Si `c2 < c1`* → somme `colCoûts[c1-1 ... c2]`.
3. Retourne la somme des deux sommes partielles.

**Pourquoi aucun chemin n'est requis* *
Parce que le robot ne peut se déplacer qu'orthogonalement, chaque chemin doit traverser chaque rangée intermédiaire ** et** chaque colonne intermédiaire au moins une fois. L'ordre dans lequel vous les croisez ne change pas l'ensemble total de lignes/colonnes visitées, et donc pas le coût total. Par conséquent, le coût minimal équivaut à la somme des lignes et colonnes obligatoires, ce qui est exactement ce que fait l'algorithme.

---

Preuve d'exactitude

Laisser `R = {min(r1, r2)+1 ... max(r1, r2)}` être l'ensemble des lignes qui doivent être entrées (chaque fois nous passons d'une ligne à l'autre).
De même, let `C = {min(c1, c2)+1 ... max(c1, c2)}` soit l'ensemble de colonnes à saisir.

*Lemme 1* – Tout chemin valide doit contenir chaque ligne dans `R` et chaque colonne dans `C`.

*Proof. *
Le robot commence à la ligne `r1`. La seule façon de changer son indice de ligne est de monter ou de descendre un pas à la fois. Pour atteindre la ligne `r2`, le chemin doit passer de `r1` à `r1±1`, puis à `r1±2`, ... jusqu'à `r2`. Ainsi, chaque rangée intermédiaire de `R` est visitée. Le même raisonnement s'applique horizontalement pour "C".

*Lemme 2* – Le coût encouru par un chemin est égal
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

*Proof. *
Chaque fois que le robot entre dans une nouvelle ligne `i` (en montant ou en descendant), il paie `rowCosts[i]` exactement une fois. Par Lemma 1 toutes les lignes dans `R` sont entrées, de sorte que le coût vertical total est la somme sur `R`. Analogue pour les colonnes. Aucun autre coût n'existe. *

*Theorem* – L'algorithme gourmand renvoie le coût minimum possible.

*Proof. *
Tout coût de chemin est exactement l'expression dans Lemma 2. Puisque l'algorithme calcule cette expression exacte, son résultat est le coût du chemin *any*, donc aussi le coût minimal. *

---

### # Pièges communs – Le mal

Que faire pour éviter Pourquoi il échoue
- C'est quoi ?
**En supposant que la distance soit la plus courte**
**Off‐by‐one dans les boucles**
**Utiliser le trop-plein de 64 bits**= Ajouter de gros coûts dans un `int`= Le coût peut atteindre `105 * 109` → utiliser `long`/`long` Autres
**Treating the robot as a graph problem**
Si un tableau de coûts contient des négatifs, cupidité fonctionne encore parce que tous les coûts sont résumés.

---

### Cas de bord – Le Ugly

Autres Décision Qu'est-ce qu'il faut vérifier ?
-- -- -- -- -- -- --
Autres Commencer équivaut à la maison. L'algorithme s'en occupe automatiquement (pas de boucles). Autres
Grande grille (105 lignes ou colonnes) Performance La longueur de boucle n'est que « Δrow » + Δcol », au plus « 2·105 » itérations – amende en < 1 ms.
Autres Gammes de coûts avec zéros. Autres
Les tableaux de coûts non continus (si le problème a permis des lacunes) Autres
Frais jusqu'à 109. Autres

---

Solutions alternatives (pourquoi elles ne sont pas nécessaires)

Algorithme Quand il est utile Pourquoi il est trop tuer ici
Il n'y a pas de lien entre les deux.
**Breadth‐First Search**= Poids de bord uniformes, petite grille= Chaque poids de bord est variable; BFS devrait garder une trace du coût par noeud → O(mn) time & memory. Autres
**Dijkstra**= Poids positifs variables== Fonctionne, mais la solution avide est plus simple et plus rapide. Autres
**Programmation dynamique**=Coûts dépendants de la trajectoire= Pas besoin parce que la structure des coûts n'est que ligne/colonne. Autres

---

- Oui. Essais d'unité d'échantillonnage

"Java
@Test
Essai de vide() {
var s = nouvelle solution();
affirmEquals(12, s.minCoût(
nouvelle int[]{1,1}, nouvelle int[]{4,3},
nouvelle int[]{1,3.5.2}, nouvelle int[]{2,4,6,1});
}
«» "

'`python
def test():
sol = Solution()
d'affirmer sol.minCost([1,1],[4,3],[1,3.5.2],[2,4,6,1]) == 12
«» "

'`cpp
Essai de vide() {
Solution sol;
assertion(sol.minCost({1,1},{4,3},{1,3.5.2},{2,4,61}) == 12);
}
«» "

---

### À emporter pour l'entrevue

1. **Identifiez les invariants** – Le robot doit traverser toutes les lignes/cols entre les deux points.
2. **Éviter la traversée inutile du graphique** – La fonction de coût du problème s'effondre à une somme simple.
3. ** Méfiez-vous des erreurs hors-par-un** – Rappelez-vous que le coût d'une ligne/col est payé * lorsque vous l'introduisez*, pas lorsque vous la quittez.
4. **Utilisez l'arithmétique 64 bits** – Le coût peut dépasser 231-1 sur les limites supérieures.
5. ** Expliquez la preuve gourmande** – Les intervieweurs aiment quand vous pouvez articuler *pourquoi* l'algorithme le plus simple est correct.

---

- Oui. 2. Billet de blog – LeetCode 2087: Le Robot Homecoming Puzzle (Java/Python/C++ Solutions)

> **Mots-clés** – *LeetCode 2087*, *Coefficient minimum pour le robot entrant*, *algorithme du réseau*, *solution de Java*, *solution de Python*, *solution de C++*, *codage d'entrevue*, *questions d'entrevue d'algorithme*, *algorithme d'entrevue d'emploi*.

---

La maîtrise du LeetCode 2087 – Le Puzzle Robot Homecoming

**Description détaillée**:
« Solution LeetCode 2087 étape par étape – calculez le coût minimum pour un robot de rentrer chez lui dans une grille. Java, Python, exemples de code C++, preuve d'exactitude, guide de cas de bord pour les interviews."

---

C'est vrai. Ce qui fait Ce puzzle intéressant ?

- Un robot** ne peut bouger qu'orthogonalement**.
- Chaque **row** et **colonne** a un coût *distinct*.
- Vous êtes demandé pour le coût **minimum**, pas le plus court chemin.

Cela ressemble à un problème classique de recherche de chemin, mais l'astuce réside dans le modèle de coût.

---

###### 2-- Le Trick Élégant de l'avidité

**Étape 1**: totaliser tous les coûts de ligne obligatoires* entre `r1` et `r2`.
**Étape 2**: Sommer tous les coûts obligatoires de la colonne entre `c1` et `c2`.
- **Résultat** : ajouter les deux montants partiels.

Pourquoi cela fonctionne : chaque marche traverse le même ensemble de lignes et de colonnes ; l'ordre n'a pas d'importance.
**Temps**:
**Espace**: O(1)

---

- Oui. Mauvais – L'approche par excès de moteur

- Les gens essaient BFS ou Dijkstra, en supposant que les poids de bord variables ont besoin d'une file d'attente prioritaire.
- Oui. Ces algorithmes utilisent la mémoire O(mn) et sont plus lents qu'une simple boucle.
- Les intersections et les off-by-one deviennent un cauchemar.

---

#######=" Ugly – Cas de bord qui piquent

- **Start est égal à la maison** → zéro coût.
- **Grandes grilles** → 105 lignes ou colonnes → s'assurer que les boucles ne dépassent pas cette limite.
- **Les coûts zéro ou négatif** → sont toujours correctement résumés.
- **Overflow** → Utilisez l'arithmétique 64-bit en Java (`long`), C++ (`long`), ou Python=s des ints arbitraires.

---

La preuve en anglais clair

1. *Invariant* : Pour passer de la ligne `r1` à la ligne `r2`, chaque ligne intermédiaire doit être visitée.
2. *Coût d'attribution*: Le robot paie les frais de fonctionnement une fois pour chaque ligne `i` il entre.
3. *Sommation*: Le coût total est égal à la somme sur toutes les lignes et colonnes visitées.
4. Puisque l'algorithme avide calcule exactement cette somme, elle est optimale.

Expliquez-le clairement dans les interviews – le "Why" est la moitié du travail.

---

Recettes de tests unitaires

Exemple de langue
C'est pas vrai.
**Java**="assertEquals(12, s.minCost(new int[]{1,1}, new int[]{4,3}, new int[]{1,3,52}, new int[]{2,4,61});"="
**Python**="assert sol.minCoût([1,1],[4,3],[1,3,52],[2,4,61]="
{1,1},{4,3},{1,3,52},{2,4,61}) == 12);

---

#### # 7-

- **Simplicité**: La solution n'est qu'une somme.
- **Proof**: Démontrer les invariants et pourquoi aucun autre algorithme n'est nécessaire.
- **Connaissance des cas**: Montrez que vous avez pris en compte les scénarios de "gugly".
- ** Compétence linguistique** : Fournir un code idiomatique propre pour Java, Python et C++.

---

La pensée finale

LeetCode 2087 est un bel exemple de la façon dont **les contraintes de problèmes peuvent transformer une question de chemin apparemment complexe en une somme cupide d'un liner**. Maître, expliquez la logique, et vous impressionnerez n'importe quel panel d'entretien. Bon codage !

---

**Profitez du code, asez l'entrevue, et continuez à résoudre! **

---


* Fin de l'article. *