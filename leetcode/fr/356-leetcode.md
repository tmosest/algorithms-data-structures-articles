---
titre: LeetCode 356. Réflexion en ligne - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solutions de code

Voici des implémentations propres, prêtes à la production dans **Java**, **Python** et **C++** qui résolvent LeetCode 356 – *Réflexion en ligne* en **O(n)** temps et **O(n)** espace supplémentaire.

---

### 1.1 Java – `Solution.java "

"Java
Importer java.util. HashSet;
Importer java.util. Jeu;

solution de classe publique {
***
* Vérifie si tous les points peuvent être reflétés sur une ligne verticale.
*
* @param points Tableau entier 2-D de points. 0 ≤ points[i].longueur] 2
* @retour vrai si une ligne verticale de réflexion existe, faux sinon
*/
le booléen public est réflecté(int[][] points) {
if (points) == null="points.longueur == 0) retour vrai;

// Trouvez les coordonnées x extrêmes.
int minX = entier.MAX_VALUE;
int maxX = entier.MIN_VALUE;
pour (int[] p : points) {
minX = Math.min(minX, p[0]);
maxX = Math.max(maxX, p[0]);
}

// Somme des coordonnées x extrêmes = 2 * centre de symétrie
somme int = minX + maxX;

// Conservez chaque point d'un ensemble de hachage pour les recherches O(1).
Set<Long> set = nouveau HashSet<>();
pour (int[] p : points) {
la valeur de référence de l'élément d'identification de l'élément d'identification de l'élément d'identification;
}

// Pour chaque point, son miroir doit aussi exister.
pour (int[] p : points) {
int miroirx = somme - p[0];
clé longue = encode(mirroredX, p[1]);
si (!set.contient(clé)) {
retourner faux; // partenaire manquant – pas symétrique
}
}
retour vrai;
}

***
* Encode une paire (x, y) dans une seule longue.
* Hypothèses : ≤ 10^8 → convient confortablement en 32 bits chacun.
*/
code long privé(int x, int y) {
retour (((long) x) << 32) ^ (y & 0xffffffffL);
}
}
«» "

---

### 1.2 Python – `solution.py "

'`python
de taper l'importation Liste

Solution de classe:
def isReflected(self, points: List[List[int]]) -> bool:
"""Retour Vrai si l'ensemble de points est symétrique sur une ligne verticale."""
si ce n'est pas les points suivants:
retour Vrai

# Trouvez les extrêmes de l'axe des x.
min_x = min(p[0] pour p en points)
max_x = max(p[0] pour p en points)
sum_x = min_x + max_x # 2 * centre de symétrie

# Conservez tous les points comme des tuples dans un ensemble pour les recherches O(1).
point_set = {tuple(p) pour p en points}

Chaque point doit avoir son miroir.
pour x, y en points:
miroir = (somme_x - x, y)
si miroir non dans point_set:
Retour Faux
retour Vrai
«» "

---

### 1.3 C++ – `Solution.cpp "

'`cpp
#incluez <vecteur>
#inclut <unordered_set>
#incluez <cstdint>

solution de classe {
public:
bool isReflected(std::vector<std::vector<int>&points) {
si (points.vide()) retourne true;

// Trouvez des valeurs x extrêmes.
Int minX = INT_MAX, maxX = INT_MIN;
pour (const auto & p : points) {
minX = md:min(minX, p[0]);
maxX = md:max(maxX, p[0]);
}
int sumX = minX + maxX; // 2 * centre de symétrie

// Encodez un point dans un entier de 64 bits.
encode automatique = [](int x, int y) -> int64_t {
retour (static_cast<int64_t>(x) << 32) ^ static_cast<int64_t>(y) & 0xffffffffLL;
};

std::unordered_set<int64_t> S;
pour (const auto & p : points)
S.insérer(encode(p[0], p[1]);

pour (const auto & p : points) {
int miroirX = sommeX - p[0];
si (!S.count(encode(mirroredX, p[1])))
retourner faux;
}
retour vrai;
}
};
«» "

> **Pourquoi ça marche ? * *
> La ligne de symétrie doit être à mi-chemin entre les valeurs "x" les plus petites et les plus grandes.
> Si un point `(x, y)` existe, le point réfléchi doit être `(minX + maxX - x, y)`.
> L'utilisation d'un jeu de hachage donne des contrôles de partenaires à temps constant, de sorte que l'algorithme entier est linéaire.

---

- Oui. 2. Article du blog – Réflexion sur la ligne : le bon, le mauvais et le mauvais

> **Méta‐Description (friendly SEO): **
> Maître LeetCode 356 – Réflexion en ligne. Obtenez une plongée profonde dans l'algorithme, les extraits de code en Java, Python & C++, ainsi que des informations sur les cas de bord, les performances et les conseils d'entrevue. Boostez votre préparation d'entrevue de codage!

2.1 Introduction

Lorsque vous vous asseyez pour résoudre LeetCode 356, *Line Reflection*, la première pensée est probablement un tri astuce ou deux pointeurs. En réalité, il y a une solution O(n) beaucoup plus propre qui passe même 104 points avec des couleurs volantes. Dans cet article, nous allons disséquer le problème, marcher à travers la meilleure approche, toucher les pièges (la laid), et terminer avec le code prêt à la copie pour **Java**, **Python** et **C++**.

### 2.2 Énoncé du problème (reformulé)

> ** Don**: `n` points sur un plan 2-D, `points[i] = [x_i, y_i]`.
> **Tâche**: Déterminer s'il existe une ligne verticale `x = k` telle que le reflet de tous les points sur cette ligne donne exactement le même ensemble de points.

> Des points répétés sont autorisés.

2.3 Intuition: La ligne miroir est à mi-chemin entre les extrêmes

Pensez à la ligne comme un miroir. Pour tout point `(x, y)`, sa réflexion est `(k*2 - x, y)`. Remarquez que la coordination y reste la même – seulement x flips. Par conséquent, si vous connaissez les lignes **center**, vous pouvez calculer instantanément un partenaire.

Le centre `k` est simplement la moyenne des plus petites et des plus grandes coordonnées x:

«» "
k = (minX + maxX) / 2
«» "

Pourquoi ? Parce que les points le plus à gauche et le plus à droite doivent être symétriques sur le miroir; sinon, aucune ligne ne peut satisfaire tous les points. Cela nous donne un candidat O(1) pour `k`.

2.4 La solution O(n) élégante (Hash Set)

1. **Trouver des extrêmes** – traverser une fois pour obtenir `minX` et `maxX`.
2. **Somme de calcul** – `sumX = minX + maxX`.
*Note*: "sumX` est égal à "2 * k". Travailler avec `sumX` nous maintient en entiers et évite les erreurs de point flottant.
3. **Store tous les points** – hachage chaque paire `(x, y)`. En Java/C++, nous encoderons en un seul entier 64 bits; en Python, un tuple est parfait.
4. **Vérifier les partenaires** – pour chaque point `(x, y)` vérifier si `(sumX - x, y)` existe dans l'ensemble.

Si un point manque son partenaire, la réponse est "faux". Sinon, nous avons une symétrie parfaite.

> **Pourquoi O(n)**:
> - Un passage pour trouver des extrêmes → O(n).
> - Un passe pour construire le set → O(n).
> - Un passe pour vérifier les partenaires → O(n).
> Le jeu de hachage donne une recherche à temps constant, donc le total est linéaire.

#### 2.5 Cas de bord (les plus moches)

Pourquoi ça compte Comment l'algorithme le gère
Il n'y a pas de lien entre les deux.
Des points dupliqués Ils doivent tous avoir des partenaires (même avec eux-mêmes). Hash set stocke chaque instance, donc `compte` fonctionne. Autres
Autres Tous les points sur la même ligne verticale. Autres
Autres Très grandes coordonnées (±108) : Prévenir le débordement. Autres
Un seul point est trivialement symétrique. La boucle trouve son propre partenaire. Autres

2.6 Approches alternatives (les bonnes)

- **Two Pointers** – trier par x, puis pour chaque point le plus à gauche le couple avec le plus à droite. Fonctionne en O(n log n).
*Pro*: Pas de jeu de hachage nécessaire.
*Con*: Facteur log supplémentaire; code plus verbeux.

- **Carte de y → Ensemble de x** – groupe par y pour gérer grand n plus rapidement en pratique.
*Pro* : gère bien les énormes ensembles de données.
*Con*: Plus complexe.

2.7 Pourquoi cela compte pour les entrevues

- **Fait connaître les structures de hachage** – une compétence d'entrevue de structure de données de base.
- **Fait ressortir la compréhension de la géométrie** – pas seulement le codage.
- ** Démontre un code propre et testable** – essentiel pour les entretiens de production.

2.8 Le dernier mot (les mauvais)

- ** Méfiez-vous du débordement entier** lors du summing `minX + maxX` si vous utilisez des ints 32 bits dans des langues comme C++/Java.
- **Rappelez-vous d'encoder les paires**; utiliser une chaîne `"x#y"` est facile mais plus lent.
- **Les cas d'Edge** comme des points répétés ou une seule ligne de points peuvent trébucher des solutions naïves.

####2.9 Extraits de code

> **Java**
> ``java
> solution de classe publique {
> le booléen public est réflecté(int[][] points) {
-// ... (code de la section 1.1)
> }
> }
> `` "

> **Python**
> ``python
> solution de classe:
> def isReflected(self, points: List[List[int]]) -> Bool:
> # ... (code de la section 1.2)
> `` "

> **C++**
> ``cpp
> solution de classe {
> public:
> bool isReflected(vector<vector<int>>& points) {
-// ... (code de la section 1.3)
> }
> };
> `` "

### 2.10 Enveloppe

LeetCode 356 est trompeurment simple mais une grande vitrine de pensée algorithmique et de code propre. Le tour de hachage vous donne un **O(n)**, **O(n)** solution spatiale qui passe tous les cas de bord et est prête à l'entrevue. Utilisez les extraits ci-dessus pour polir votre portfolio, as l'entrevue, et peut-être harceler cette prochaine offre d'emploi. Bon codage !

---

**Mots clés:** Réflexion en ligne, LeetCode 356, symétrie en ligne verticale, Algorithme O(n), solution de jeu de hachage, Java, Python, C++, prép interview, interview de codage, résolution de problèmes algorithmique.