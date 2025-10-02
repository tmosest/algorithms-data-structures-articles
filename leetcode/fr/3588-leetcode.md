---
titre: LeetCode 3588. Trouver le maximum Zone d'un triangle -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

3588 – Trouver le maximum Zone d'un triangle
### 3 Solutions complètes + SEO-Optimized Blog Post

> *Leetcode 3588* est un problème moyen qui apparaît souvent dans les entretiens par algorithme.
> Il teste votre capacité à combiner **hash-maps**, **greedy thought**, et une compréhension claire de **géométrie**.

Ci-dessous vous trouverez:

Langue Fichier Complexité Faits saillants Autres
C'est pas vrai.
Autres Java=1 `Solution.java=1 **O(n log n)**=1 Utilise `HashMap` + `TreeSet` pour la récupération rapide min/max=1
Python "solution.py" **O(n log n)**
* (n log n) * Rapide, utilise `unordered_map` + `set`

Après le code vous obtiendrez un article de blog complet qui couvre *le bon, le mauvais, et le laid* de ce problème – tous SEO-friendly pour que les recruteurs puissent le trouver!

---

Récapitulatif du problème (code de bord 3588)

On vous donne un tableau de coordonnées 2-D distinctes `coords[n][2]`.
Trouvez la zone **maximum** d'un triangle dont les sommets sont à trois points des "coords", *avec la restriction supplémentaire qu'au moins un côté est parallèle à l'axe X ou à l'axe Y*.

Retour **deux fois la zone** ('2 * A').
Si un tel triangle n'existe pas, retourner `-1`.
Un triangle avec zone zéro n'est pas autorisé.

Contraintes

Un point unique
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --

---

# # # Une perspective fondamentale

> Un triangle qui a un côté parallèle à un axe doit contenir **deux points qui partagent la même coordonnées X ou Y**.

Donc la tâche se résume à:

1. **Points de groupe par X** – ce sont des côtés verticaux potentiels.
Pour chaque groupe X, la longueur de base *vertical* est `maxY - minY`.
Pour maximiser la superficie, choisissez le troisième point qui est le plus éloigné horizontalement de ce X (c.-à-d. le minimum global ou le maximum X).

2. **Points de groupe par Y** – logique symétrique pour les côtés horizontaux.

Seulement quand un groupe a ** au moins deux points** (si base > 0) *et* il y a un troisième point distinct (distance horizontale/verticale) 0) peut-on former un triangle valide.

---

C'est pas vrai. Java – `Solution.java "

"Java
Importation de java.util.*;

solution de classe publique {
public long maxArea(int[][] coords) {
// Cartes: X -> (min., max., Y -> (min., max.)
Carte<entier, int[]> xMap = nouveau HashMap<>();
Carte<entier, int[]> yMap = nouveau HashMap<>();

mondial MinX = entier.MAX_VALUE, globalMaxX = entier.MIN_VALUE;
mondial MinY = entier.MAX_VALUE, globalMaxY = entier.MIN_VALUE;

pour (int[] p : coords) {
int x = p[0], y = p[1];

// Mettre à jour la carte X
xMap.computeIfAbsent(x, k -> new int[]{entier. MAX_VALUE, entier.MIN_VALUE});
[] yRange = xMap.get(x);
yRange[0] = Math.min(yRange[0], y);
yRange[1] = Math.max(yRange[1], y);

// Mettre à jour la carte Y
yMap.computer IfAbsent(y, k -> new int[]{Integer. MAX_VALUE, entier.MIN_VALUE});
[] xRange = yMap.get(y);
xRange[0] = Math.min(xRange[0], x);
xRange[1] = Math.max(xRange[1], x);

// Les extrêmes mondiaux
mondial MinX = Math.min(globalMinX, x);
mondial MaxX = Math.max (globalMaxX, x);
mondial MinY = Math.min(global) ii) MinY, y);
mondial MaxY = Math.max(global) - MaxY, y);
}

longue meilleure = -1;

// Côtés verticaux (même X)
pour (entrée var : xMap.entrySet()) {
int x = entrée.getKey();
int[] yRange = entry.getValue();
Si (yRange[0]] == yRange[1]) continuer; // hauteur zéro
base longue = (long) (yRange[1] - yRange[0]);

// Le troisième point doit être horizontal
longue horiz1 = Math.abs(long) x - globalMinX;
longue horiz2 = Math.abs(long) x - globalMaxX;
Si (horizon 1 ) 0 && horiz 2 ) 0) continuer; // partage de tous les points X

longueur = Math.max(horizon1, horiz2);
best = Math.max(best, base * height);
}

// Côtés horizontaux (même Y)
pour (entrée var : yMap.entrySet()) {
int y = entry.getKey();
int[] xRange = entry.getValue();
si (xRange[0] == xRange[1]) continuer; // largeur zéro
base longue = (long) (xRange[1] - xRange[0]);

long vert1 = Math.abs(long) y - global ii) Miny);
long vert2 = Math.abs(long) y - globalMaxY);
Si (vert1 == 0 &&vert2 == 0) continuer; // partage de tous les points Y

longueur = Math.max(vert1, vert2);
best = Math.max(best, base * height);
}

le meilleur retour;
}
}
«» "

**Points clés**

- Les magasins `int[]` `[min, max]` pour chaque clé.
- `computerIfAbsent` garde le code propre.
- La multiplication longue (`base * hauteur`) ne garantit aucun débordement.
- Complexité: temps `O(n)`, espace `O(n)` (tableaux deash).

---

Python – `solution.py "

'`python
importations
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def maxArea(self, coords: List[List[int]]) -> Int:
x_map = defaultdict(lambda: [sys.maxsize, -sys.maxsize])
y_map = defaultdict(lambda: [sys.maxsize, -sys.maxsize])

min_x = min_y = sys.maxsize
max_x = max_y = -sys.maxsize

pour x, y dans les coordonnées:
Groupes X
r = x_map[x]
r[0] = min(r[0], y)
r[1] = max(r[1], y)
Groupes Y
r = y_map[y]
[0] = min(r[0], x)
r[1] = max(r[1], x)

# extrêmes mondiaux
min_x = min(min_x, x)
max_x = max(max_x, x)
min_y = min(min_y, y)
max_y = max(max_y, y)

meilleure = -1

# Côtés verticaux
pour x, (ymin, ymax) dans x_map.items():
Si ymin == ymax: # hauteur zéro
poursuivre
base = ymax - ymin
horiz = max(abs(x - min_x), abs(x - max_x)
si horiz == 0: # aucun autre x
poursuivre
best = max (meilleur, base * horiz)

# Côtés horizontaux
pour y, (xmin, xmax) dans y_map.items():
Si xmin == xmax: # largeur zéro
poursuivre
base = xmax - xmin
vert = max(abs(y - min_y), abs(y - max_y))
en cas de vertige 0: # aucune autre y
poursuivre
best = max(meilleur, base * vert)

le meilleur retour
«» "

**Pourquoi ça marche**

- Oui. Utilise une seule passe pour remplir deux hash‐maps (`x_map`, `y_map`).
- `defaultdict` conserve `[min, max]` automatiquement.
- Oui. Pas besoin de tri explicite; `max(abs(x-min_x), abs(x-max_x)` est le choix gourmand.
- Même temps "O(n)", "O(n)".

---

## C++ 3=2 – `Solution.cpp "

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
longue longueur maxZone(vecteur<vecteur<int>>&coords) {
sans ordre_map<int, paire<int,int>> xMap, yMap;
Int minX = INT_MAX, maxX = INT_MIN;
Int minY = INT_MAX, maxY = INT_MIN;

// Popular cartes et extrêmes mondiaux
pour (auto &p : coords) {
int x = p[0], y = p[1];

Auto &yr = xMap[x];
if (an.first==0 && an.seconde==0) { // première fois
ANS = {INT_MAX, INT_MIN};
}
yr.first = min(an.first, y);
yr.seconde = max (an.seconde, y);

auto &xr = yMap[y];
Si (xr.first==0 && xr.second==0) {
xr = {INT_MAX, INT_MIN};
}
xr.first = min(xr.first, x);
xr.seconde = max(xr.seconde, x);

minX = min(minX, x); maxX = max(maxX, x);
minY = min(minY, y); maxY = max(maxY, y);
}

longueur longue meilleure = -1;

// Côtés verticaux (même X)
pour (auto &kv : xMap) {
int x = kv.first;
int ymin = kv.second.first, ymax = kv.second.second;
si (ymin) ymax continue; // pas de hauteur
longue base longue = (long long) (ymax - ymin);

horiz long = max( llabs(long)x - MinX),
llabs(long)x - maxX));
Si (horizon) 0) continuer; // tous les points partagent ce X

best = max (meilleur, base * horiz);
}

// Côtés horizontaux (même Y)
pour (auto &kv : yMap) {
int y = kv.first;
int xmin = kv.second.first, xmax = kv.second.second;
Si (xmin) xmax continue; // aucune largeur
longue base longue = (long long) (xmax - xmin);

long vert = max( llabs(long)y - minY),
les labs(long)y - maxY);
si (vert) 0) continuer; // tous les points partagent ce Y

best = max (meilleur, base * vert);
}

le meilleur retour;
}
};
«» "

** Faits saillants* *

- `unordered_map<int, pair<int,int>>` Garde la mémoire basse.
- Les « labs » garantissent une valeur absolue « longue ».
- Oui. L'algorithme est **linéaire dans la pratique** parce que les recherches de hash-map sont moyennes O(1).

---

Article de blog optimisé du SEO

> **Mots clés**: Leetcode 3588, maximum area triangle, entretien d'emploi, algorithme, Java, Python, C++, hash map, géométrie, complexité du temps, recruteur, structure des données, interview prep

---

Le problème qui vous fait penser

Leetcode 3588 est un problème de géométrie de niveau moyen* qui apparaît dans de nombreuses interviews techniques.
Les recruteurs adorent parce qu'il vérifie :

- **Manipulation de la carte deash** (groupage rapide).
- **Choix de mariage** (cochez le point le plus éloigné).
- ** Géométrie euclidienne de base** (zone = base × hauteur / 2).

La solution de l'idée en une seule phrase

> **Points de groupe par X et Y, conserver min/max pour chaque groupe, et multiplier la longueur de base par la distance la plus éloignée possible jusqu'à un troisième point. **

Il s'agit d'une astuce *classique, cupide-plus-hash-map* : on n'a jamais besoin d'inspecter chaque triple ; on a juste besoin des extrêmes.

C'est vrai. Le bien

Raison
- Oui.
**Intuitive** – un côté parallèle à un axe signifie que deux points partagent une coordonnée. Autres
**Fast** – un seul passage pour construire des hash-maps, puis quelques scans linéaires. Autres
**Tables de hachage `O(n)`, pas de tableaux 2-D de taille `106 × 106`. Autres
**Cadre réutilisable** – peut être appliqué à d'autres problèmes de triangle parallèle. Autres

C'est pas vrai. Le mal

Problème
- Oui.
** Grande entrée** – 105 points ont besoin d'un algorithme linéaire ; toute tentative O(n2) TLE. Autres
**Cas d'Edge** – tous les points partagent le même X ou Y → aucun triangle valide. Autres
**Off‐by‐one** – oublier d'utiliser `long`/`long long` en multipliant peut déborder même avec 106 limites. Autres
**Miss-liser la zone deux fois** – de nombreux auteurs oublient de doubler le produit. Autres

C'est vrai. L'Ugly

Raison
- Oui.
**Troisième point confusion** – beaucoup commencent par choisir un troisième point et ensuite essayer de le fixer plus tard, provoquant des bugs subtils. Autres
**TreeSet vs. simple min/max** – certaines solutions utilisent "TreeSet" inutilement, ce qui rend le code plus long. Autres
**Global extremes mix-up** – l'utilisation de `globalMinX` par rapport à `globalMinY` conduit à une mauvaise zone. Autres
**Drapeau booléen vs. sentinelle** – l'initialisation `best` à 0 est tentante, mais vous avez besoin d'un drapeau pour distinguer le triangle de la zone 0. Autres

#### 6=" Code Marche à travers (Toutes les langues)

*Les trois extraits ci-dessous sont identiques en logique – juste les changements de syntaxe. *

Texte
1. Construire 2 cartes : X → (minY, maxY) et Y → (minX, maxX)
2. Conserver au niveau mondial min/max X et Y.
3. Pour chaque groupe X:
- base = maxY - minY (doit être > 0)
- hauteur = max. (= x - globalMinX,= x - globalMaxX) (doit être > 0)
- zone candidate = base * hauteur
4. Pour chaque groupe Y : même, échange d'axes.
5. Retourner la zone candidate maximale, ou -1 si aucune n'existe.
«» "

#### 7-

Langue Heure Espace
- C'est quoi ?
Java **O(n)** (les recherches hash-map sont amorties O(1))
Python **O(n)**
* * * * * * * *

> Le seul facteur logarithmique provient du `TreeSet` ou `set` utilisé pour récupérer les extrêmes mondiaux – mais c'est toujours linéaire dans l'ensemble car chaque extrême est mis à jour en O(1).

Réflexions finales pour votre entrevue

- ** Expliquez d'abord le point de vue principal** – Deux points doivent partager X ou Y.
- **Show the cupidy cueil** – le troisième point le plus loin, pas un point arbitraire.
- **Boîtes de bord de Mention** – tous les points sur une seule ligne verticale, ou tous sur une seule ligne horizontale.
- **Clarifier les types de données** – utiliser des entiers 64 bits pour éviter le débordement.

---

Pourquoi les recruteurs devraient s'en soucier

- **Profondeur algorithmique**: démontre la maîtrise du hash-map.
- ** Style de codage** : concis mais lisible – signe de code propre.
- **Performance**: temps linéaire sur jusqu'à 100k points – montre que vous vous souciez de l'efficacité.

Utilisez les extraits de code comme projets de portefeuille ou exemples d'entrevue, et le billet de blog comme une vitrine écrite de votre voyage de résolution de problèmes.

---

TL;DR

*Leetcode 3588 est solvable en une seule passe linéaire plus quelques vérifications gourmandes.
Vos solutions devraient : *

1. **Groupe par X et Y** (cartes hash).
2. **Garder le niveau global min/max** pour les deux axes.
3. **Zone de calcul** en utilisant le troisième point le plus éloigné possible.
4. **Retour -1** si aucun triangle valide n'existe.

Les trois langues ci-dessus répondent parfaitement aux exigences.

Bon codage et bonne chance à l'arrivée de la prochaine entrevue de travail! C'est ce qu'il a dit