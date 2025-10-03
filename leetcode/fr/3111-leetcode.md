---
titre: LeetCode 3111. Rectangles minimaux vers les points de couverture -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3111. Rectangles minimum vers les points de couverture – Solutions complètes + Blog

---

- Oui. 1. Récapitulation des problèmes
Vous êtes donné `points = [[x1,y1],[x2,y2], ...]` et une largeur `w`.
Un rectangle peut démarrer à n'importe quel `(x1,0)` et se terminer à `(x2, y2)` **seulement** si `x2 – x1 ≤ w`.
Tous les points doivent se trouver à l'intérieur ** ou sur** au moins un rectangle.
Retournez le nombre minimum de rectangles requis.

> **Insight clé** – Parce que les rectangles sont des bandes horizontales qui commencent à `y = 0`, seulement les questions **x‐coordonné** pour couvrir.
> Triez les points par `x` et placez avidement un rectangle chaque fois que nous atteignons un point en dehors du rectangle actuel.

---

- Oui. 2. Algorithme (Sorte + Greedy)

«» "
1. Trier les points par leur coordonnées x ascendantes.
2. LastCoveredX = --- (toute valeur < min(x))
3. résultat = 0
4. Pour chaque point (x, y) de la liste triée:
si x > dernier CouvertX:
// lancer un nouveau rectangle
résultat += 1
LastCoveredX = x + w // le plus lointain x ce rectangle peut couvrir
5. Résultat du retour
«» "

- Oui. Pourquoi ça marche ?
- Après tri, tout point qui apparaît après le rectangle actuel ne peut pas être couvert par lui.
- Oui. Le rectangle qui commence au point actuel et s'étend aussi loin à droite que permis (`x + w`) couvre **all** les points suivants dont `x` ≤ cette limite.
- Le placement de graisse est optimal car retarder un rectangle ne peut jamais réduire le nombre total.

---

- Oui. 3. Complexité

Opération Temps Espace
- C'est quoi ?
"O(n log n)" "O(1)" (en place)
Numérisation de la graisse Autres
Total **«O(n log n)»****«O(1)»** (hors tableau d'entrée)

---

- Oui. 4. Mise en œuvre des références

#### 4.1 Java

"Java
Importer java.util. Les tableaux;
Importer java.util. Comparateur;

solution de classe publique {
public int minRectanglesToCoverPoints[][] points, int w) {
// Tri par coordonnées x
les tableaux.sort(points, Comparator.comparingInt(a -> a[0]);

nombre int = 0;
longue dernière CouvertX = -1; // sans danger pour les grandes valeurs

pour (int[] p : points) {
int x = p[0];
si ((long) x > lastCoveredX) { // nouveau rectangle nécessaire
count++;
LastCoveredX = (long) x + w; // plus loin x ce rectangle peut atteindre
}
}
le nombre de retours;
}
}
«» "

4.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def minRectanglesToCoverPoints(self, points: List[List[int]], w: int) -> Int:
points.sort(key=lambda p: p[0]) # trier par x

nombre = 0
Last_covered = -1 # toute valeur < min(x)

pour x, _ en points:
si x > last_covered: # commencer un nouveau rectangle
nombre += 1
last_covered = x + w
Nombre de retours
«» "

### 4.3 C++

'`cpp
#incluez <vecteur>
#incluez <algorithme>

solution de classe {
public:
int minRectanglesToCoverPoints(std::vector<std::vector<int>&points, int w) {
// trier par x
à:sort(points.begin(), points.end(),
[](const std::vector<int>& a, const std::vector<int>& b) {
retourner a[0] < b[0];
});

nombre int = 0;
longue longue dernière Couvert = -1; // sans danger pour les grandes valeurs

pour (const auto & p : points) {
si ((long)p[0] > dernierCouvert) {
+ nombre;
dernier Couvert = (long)p[0] + w;
}
}
le nombre de retours;
}
};
«» "

Les trois solutions partagent la même logique de base et fonctionnent dans le temps `O(n log n)` avec `O(1)` espace supplémentaire.

---

- Oui. 5. Article de blog – LeetCode de Master 3111: Rectangles minimum pour couvrir les points

> **Mots clés**: LeetCode 3111, Rectangles minimums vers les points de couverture, algorithme tri-greedy, solution Java, solution Python, solution C++, entretien de codage, entretien d'algorithme, structures de données, entretien d'emploi, ingénieur logiciel, entretien technique

---

Introduction

Si vous vous préparez à des entrevues en génie logiciel, vous rencontrerez rapidement des problèmes qui nécessitent une stratégie propre *sort-and-greedy*. LeetCode 3111, **Les rectangles mineurs vers les points de couverture**, est un exemple classique. Dans cet article, je vais parcourir le problème, montrer la solution avide optimale, discuter des cas de bord, présenter le code prêt-à-copier en Java, Python et C++, et expliquer pourquoi ce problème est un excellent point de discussion d'interview.

---

### Déclaration de problème

Étant donné:
- `points = [[x1, y1], [x2, y2], ...]` – tous les points sont uniques.
- Une largeur w.

Chaque rectangle doit avoir:
- Coin inférieur de l'axe des x: `(x1, 0)`.
- Coin supérieur n'importe où au-dessus: `(x2, y2)` avec `x2 - x1 ≤ w`.

Objectif : **Couvrir chaque point avec les moindres rectangles possibles**.

---

Pourquoi ce problème est intéressant

1. **Réduction de la dimension** – Bien que chaque point ait une valeur `x` et `y`, la valeur `y` n'est pas pertinente pour la couverture car tous les rectangles s'étendent de `y = 0` vers le haut.
2. **Greedy Optimality** – Un choix avide bien choisi (commençant un rectangle au point le plus découvert à gauche) garantit l'optimalité.
3. **Grande entrée** – `n` peut être jusqu'à 100 000, donc une solution `O(n log n)` est nécessaire.
4. **Real‐World Insight** – Cette tendance est courante dans les problèmes de calendrier, de couverture des intervalles et d'allocation des ressources.

---

### La perspective de l'avidité

Trier les points par leur coordonnées x. Puis scanner de gauche à droite :

- Oui. Si le point actuel est au-delà de la portée du rectangle actuel (`x > lastCoveredX`), **démarrez un nouveau rectangle** à ce point.
- Le rectangle s'étend de `x` à `x + w', ainsi défini `lastCoveredX = x + w`.

Cela garantit que chaque rectangle couvre autant de points que possible à sa droite.

---

### Mise en oeuvre

C'est vrai. Java

"Java
Importer java.util. Les tableaux;
Importer java.util. Comparateur;

solution de classe publique {
public int minRectanglesToCoverPoints[][] points, int w) {
// 1. Tri par x
les tableaux.sort(points, Comparator.comparingInt(a -> a[0]);

int res = 0;
longue dernière = -1; // toute valeur < min(x)

pour (int[] p : points) {
int x = p[0];
// 2. Si ce point n'est pas couvert, lancez un nouveau rectangle
si ((long) x > dernier) {
res++;
dernier = (long) x + w; // portée du nouveau rectangle
}
}
retour rés;
}
}
«» "

**Quoi mettre en évidence dans une entrevue* *

- Utilisez `long` pour `lastCoveredX` pour éviter le débordement (`x + w` peut être jusqu'à 2 × 109).
- Expliquer que le tri avec `Arrays.sort` est *stable* assez parce que seulement `x` compte.

Python

'`python
Solution de classe:
def minRectanglesToCoverPoints(self, points: List[List[int]], w: int) -> Int:
points.sort(key=lambda p: p[0]) # trier par x

Res = 0
Dernier = -1

pour x, _ en points:
si x > dernier:
Rés += 1
dernier = x + w
retour res
«» "

**Interview Tip** – Montrer que les Python's intégrés `sort` sont `Timsort` (optimal `O(n log n)`).

C++

'`cpp
solution de classe {
public:
int minRectanglesToCoverPoints(vecteur<vecteur<int>>&points, int w) {
// Trier par x
tri(points.begin(), points.end(),
[](const auto& a, const auto& b) { retourner a[0] < b[0]; });

nombre int = 0;
longue longue dernière = -1; // utiliser longtemps pour la sécurité

pour (const auto & p : points) {
si ((long)p[0] > dernier) {
+ nombre;
dernière = (long)p[0] + w;
}
}
le nombre de retours;
}
};
«» "

---

Cas de bord et pièges communs

Qu'est-ce qu'il faut regarder
-- -- -- -- -- -- -- -- --
= 0 ' Chaque rectangle ne couvre qu'un seul point. L'algorithme fonctionne toujours. Autres
Très grande < x + w > (= 2 × 109) Utilisez des entiers 64 bits (`long` / `long`) pour éviter les débordements. Autres
Points avec des valeurs `x` identiques Le problème garantit l'unicité, mais sinon, le tri fonctionne encore ; les duplicatas partagent simplement le même rectangle. Autres
Retour `0` – notre boucle la gère naturellement. Autres
Coordonnées négatives Tri des négatifs des poignées juste très bien; `lastCoveredX` commence par `-1`. Autres

---

### Stratégie d'essai

Autres Test de précision Points attendus Raison
C'est pas vrai.
Un rectangle `[1,4]` couvre tout. Autres
Deux rectangles : `[1,3]` et `[6,8]`. Autres
[[10,0],[20,0],[30,0]» La largeur est trop petite pour couvrir plus d'un point. Autres
Large tableau aléatoire (105 points) Autres

---

### Prise- Pour les entrevues

- **Énoncer l'Intuition** : Le y-coordonné n'a jamais d'importance car tous les rectangles commencent à y = 0.
- **Expliquer l'optimisation**: Montrer que le démarrage d'un rectangle au point le plus à gauche découvert ne peut être amélioré par aucun autre placement.
- **Time & Space**: Mention que le tri domine le temps, et nous n'utilisons que la mémoire supplémentaire constante.
- **Language-agnostique**: Vous pouvez présenter l'algorithme dans n'importe quelle langue. C'est une grande démonstration d'un algorithme d'avidité propre O(n log n).
- **Talk About Edge Cases**: Débordement de mention et coordonnées négatives. Il montre que vous pensez à la robustesse de la production.

---

Les pensées finales

LeetCode 3111 est un problème trompeur simple qui regroupe plusieurs concepts interviewables:
- Tri
- Prise de décision sur l'avidité
- Revêtement d'intervalle
- Manipulation des caisses

La maîtrise vous offre non seulement une solution prête à l'emploi pour la plateforme LeetCode, mais démontre également votre capacité à *réduire la dimensionnalité* et *appliquer une stratégie avide* éprouvée – compétences que les gestionnaires embauchent adorent voir. Bonne chance pour votre prochain entretien technique!

---

Références

- Problème de LeetCode 3111 – *Rectangles mineurs aux points de couverture*
- Discussions officielles sur les solutions (Java / Python / C++)
- Interview‐prep blogs sur les algorithmes gourmands et la couverture de l'intervalle

---

Bon codage, et que vos rectangles soient toujours optimaux!