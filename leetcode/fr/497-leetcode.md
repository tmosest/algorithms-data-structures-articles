---
titre: LeetCode 497. Point aléatoire dans les rectangles non superposés -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code

Voici des implémentations propres et autonomes pour **Java**, **Python** et **C++** qui résolvent LeetCode 497 – *Random Point dans les rectangles non superposés*.
Les trois versions utilisent la même idée :

Étape Idée Autres
- Oui.
Autres 1= Précalculer le nombre ** de points entiers** dans chaque rectangle:
«zone = (x2 – x1 + 1) * (y2 – y1 + 1)» Autres
Autres 2=Construisez un tableau **préfixe-somme** (`pointsPrefix`) de sorte que `pointsPrefix[i]` soit le nombre total de points dans les rectangles `0 ... i`.
Autres Choisissez un entier aléatoire `t` dans `[0, totalPoints – 1]`. Autres
Autres Points de recherche binaire Préfixe` pour trouver le rectangle qui contient l'index `t`. Autres
Autres Convertir l'index local à l'intérieur de ce rectangle en coordonnées `x` et `y`. Autres

Le point résultant est **distribué uniformément** sur tous les points entiers de tous les rectangles.

---

- Oui. Java (Java 17)

"Java
Importation de java.util.*;

solution de classe {
les résultats finaux privés [];
préfixe interne final privé; // préfixe somme des nombres de points
Finale privée Rand aléatoire = nouveau Random();

solution publique(int[]] rects) {
ce.rects = rects;
int n = longueur rects;
préfixe = nouvelle int[n];
= 0;
pour (int i = 0; i < n; i++) {
int[] r = rects[i];
int pts = (r[2] - r[0] + 1) * (r[3] - r[1] + 1);
total += pts;
préfixe[i] = total;
}
}

public int[] select() {
cible int = rand.nextInt(préfix[préfix.longueur - 1]); // [0, total-1]
int rectIdx = binaireSearch(cible);
int[] r = rects[rectIdx];
largeur int = r[2] - r[0] + 1;
hauteur int = r[3] - r[1] + 1;
base int = rectIdx == 0 ? 0 : préfixe[rectIdx - 1];
int offset = cible - base; // 0-based offset inside this rectangle
int x = r[0] + (largeur en % offset);
int y = r[1] + (offset / largeur);
retourner une nouvelle int[]{x, y};
}

private int binaireSearch(int cible) {
int lo = 0, hi = préfix.longueur - 1;
pendant qu ' il y a (l < bonjour) {
Int milieu = (lo + hi) >>> 1;
si (cible < prefix[mid]) hi = milieu;
autrement lo = milieu + 1;
}
retour lo;
}
}
«» "

---

### Python (Python 3.10)

'`python
importation aléatoire
bisect d'importation
de taper l'importation Liste

Solution de classe:
def __init_(self, rects: List[List[int]]):
autorégulation = rects
autopréfixe = []
Total = 0
pour r en rects:
pts = (r[2] - r[0] + 1) * (r[3] - r[1] + 1)
Total += pts
(total)

def cueil(self) -> Liste[int]:
cible = aléatoire.randint(0, auto.préfixe[-1] - 1) # inclusive
rect_idx = bisect.bisect_left(self.prefix, cible)
r = autorégulation[rect_idx]
largeur = r[2] - r[0] + 1
hauteur = r[3] - r[1] + 1
base = 0 si rect_idx == 0 autre personne. préfixe[rect_idx - 1]
offset = objectif - base
x = r[0] + largeur % offset
y = r[1] + décalé // largeur
retour [x, y]
«» "

---

### C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur<vector<int>> rects;
vectorielle <long long> préfixe; // utiliser longtemps pour la sécurité
mt19937 rng{random_device{}()};

Solution(vecteur<vecteur<int>>& rects_) : rects(rects_) {
long total = 0;
pour (auto& r : rects) {
longs pts = 1LL * (r[2] - r[0] + 1) * (r[3] - r[1] + 1);
total += pts;
préfix.push_back(total);
}
}

vecteur<int> pic() {
la distribution uniforme_int_<long long> dist(0, prefix.back() - 1);
longue cible longue = dist(rng); // [0, total-1]
int rectIdx = lower_bound(prefix.begin(), prefix.end(), cible) - prefix.begin();

const auto& r = rects[rectIdx];
largeur longue = r[2] - r[0] + 1;
hauteur longue = r[3] - r[1] + 1;
longue base longue = rectIdx == 0 ? 0 : préfixe[rectIdx - 1];
long décalage long = cible - base; //

int x = r[0] + int (largeur en % offset);
int y = r[1] + int(offset / largeur);
retourner {x, y};
}
};
«» "

Les trois solutions fonctionnent dans **O(log n)** temps par `pick()` (recherche binaire sur au plus 100 rectangles) et **O(n)** temps pour l'initialisation.

---

- Oui. 2. Article du blog

> **Titre**
> LeetCode 497 – Point aléatoire dans la non-overlaping Rectangles : solutions Java, Python et C++ (les bonnes, les mauvaises et les mauvaises)

---

Introduction

Si vous préparez une entrevue de codage, vous trouverez rapidement que **randomisation** peut être un sujet étonnamment difficile. LeetCodeS *Random Point in Non-overlaping Rectangles* (Problème 497) est un exemple classique qui teste non seulement vos connaissances en structures de données, mais aussi votre capacité à raisonner sur la probabilité et l'efficacité.

Dans cet article, nous allons:

1. Récapitulez l'énoncé du problème.
2. Discutez des pièges qui peuvent transformer une bonne idée en une mise en œuvre *bug-prone*.
3. Présentez une solution de requête propre **O(n)** pré-traitement + **O(log n)**.
4. Afficher le code dans **Java, Python et C++**.
5. Explorez le bon, le mauvais et les aspects laids du problème et de ses solutions.
6. Offrez des renseignements prêts à l'entrevue et des questions de suivi possibles.

Laisse plonger.

---

- Oui. 1. Remise en état des problèmes

On vous donne un tableau de "rects" de rectangles non superposés, alignés sur l'axe.
Chaque rectangle est `[x1, y1, x2, y2]` où `(x1, y1)` est le coin inférieur gauche et `(x2, y2)` le coin supérieur droit (tous deux compris).

> **Tâche** – Concevoir une classe qui :
> * Initialise avec les "rects".
> * Renvoie un point entier aléatoire `[x, y]` qui se trouve à l'intérieur de *toute* des rectangles, chaque point entier étant également probable.

Contraintes:
* `1 ≤ longueur des rects ≤ 100`
* `10^9 ≤ x1 < x2, y1 < y2 ≤ 10^9`
* `x2 – x1 ≤ 2000`, `y2 – y1 ≤ 2000`
* Tous les rectangles sont disjoints.
* Jusqu'à `10^5` appels à `pick()' dans un cas d'essai.

---

- Oui. 2. Les pièges – *Pourquoi la randomisation est difficile*

Pourquoi ça compte ?
-- -- -- -- -- -- -- --------------------------------------------------
**Inclusifs par rapport aux limites exclusives** Si vous les traitez comme exclusifs, vous aurez des points de sous-compte.
**Les dépassements peuvent être jusqu'en 2001. Carré donne ~4 M. 100 rectangles → ~400 M points. Il convient toujours à `int`, mais l'utilisation d'un entier signé 32 bits peut être dangereuse dans certaines langues (par exemple, Java="int` est 32 bits, mais `long` est plus sûr). En utilisant `int` partout dans Java peut conduire à des bogues subtils si les données de test repoussent la limite supérieure. Autres
**Random range off‐by‐one** Oublier l'extrémité inclusive mène à une distribution ** biaisée**. Le mélange de `nxtInt(n)` avec `nxtInt(n) + 1` ou `randrange(n+1)` est incorrect. Autres
Avec jusqu'à 100 rectangles, une recherche linéaire est bonne, mais elle est toujours *O(n)* par `pick()`. Dans une interview, vous voulez montrer une étape logarithmique (recherche binaire) si vous le pouvez. Ne pas utiliser `bisect`/`lower_bound`, ni scanner chaque rectangle pour chaque choix. Autres
**La mutation d'état**La classe doit maintenir les sommes du préfixe; si vous les recalculez chaque appel, vous perdrez l'avantage O(1). Reconstruire les montants du préfixe à l'intérieur de `pick()' → TLE sur les cas d'essai lourds. Autres

---

- Oui. 3. La solution élégante

**Idée de base** – Pensez à tous les points entiers comme un tableau linéaire unique* de longueur « TotalPoints ».
Si nous pouvions cartographier un index aléatoire dans ce tableau sur un point concret `(x, y)`, nous aurions une distribution uniforme automatiquement.

1. ** Nombre de points par rectangle* *
Chaque rectangle contient
Texte
pts = (x2 - x1 + 1) * (y2 - y1 + 1)
«» "
(le `+1` rend les coins inclus).

2. **Prefix Sum Array** – `pointsPrefix[i]` = nombre total de points dans les rectangles `0 ... i`.
*Construit une fois en O(n). *

3. **Random Target** – choisir un entier `t` dans `[0, totalPoints-1]`.
Chaque valeur de `t` correspond à un point unique du tableau linéaire global.

4. **Recherche binaire** – trouver le plus petit `i` de telle sorte que `points Préfixe.
Ce rectangle contient le point avec le décalage local `t - previousPrefix`.

5. **Traduisez offset → Coordonnées**
Dans le rectangle choisi, `largeur = x2 - x1 + 1`.
Texte
localX = x1 + (pourcentage de la largeur)
localY = y1 + (offset / largeur)
«» "

Comme chaque point entier a une représentation *identique* dans le tableau linéaire, le point résultant est uniformément aléatoire.

> **Pourquoi la recherche binaire? * *
> `pointsPrefix` est trié (en augmentation monétaire). Un standard `lower_bound`/`bisect_left` nous donne le rectangle en **O(log n)** temps – bien dans les limites du problème (100 rectangles) et les attentes d'entrevue.

---

- Oui. 4. Passage du code (Java)

"Java
solution de classe publique {
les résultats finaux privés [];
préfixe int[] final privé;
Finale privée Rand aléatoire = nouveau Random();

solution publique(int[]] rects) {
ce.rects = rects;
int n = longueur rects;
préfixe = nouvelle int[n];
= 0;
pour (int i = 0; i < n; i++) {
int[] r = rects[i];
int pts = (r[2] - r[0] + 1) * (r[3] - r[1] + 1);
total += pts;
préfixe[i] = total;
}
}

public int[] select() {
int cible = rand.nextInt(préfix[préfix.longueur - 1]); // [0,total-1]
int idx = binaireSearch(cible);
int[] r = rects[idx];
largeur int = r[2] - r[0] + 1;
hauteur int = r[3] - r[1] + 1;
base int = idx == 0 ? 0 : préfixe[idx - 1];
int offset = cible - base;
int x = r[0] + (largeur en % offset);
int y = r[1] + (offset / largeur);
retourner une nouvelle int[]{x, y};
}

private int binaireSearch(int cible) {
int lo = 0, hi = préfix.longueur - 1;
pendant qu ' il y a (l < bonjour) {
Int milieu = (lo + hi) >>> 1;
si (cible < prefix[mid]) hi = milieu;
autrement lo = milieu + 1;
}
retour lo;
}
}
«» "

**À emporter** – la classe est apatride après la construction; `pick()` est pur et rapide.

---

- Oui. 5. Les bons, les mauvais et les méchants

Le bon Le mauvais Le mauvais
- C'est quoi ?
**L'élégance algorithmique**L'utilisation d'un préfixe sum + la recherche binaire est un modèle de manuel de traduction. Le fait de ne pas traiter les limites de façon inclusive conduit à des résultats biaisés. Essayer d'utiliser un point aléatoire naïf dans la boîte de délimitation et rejeter l'approche entraîne un temps exponentiel lorsque les rectangles sont minuscules ou clairsemés. Autres
**Randomness correctness**= `nextInt(total)` + offset conversion garantit l'uniformité sans post-traitement.== Un mauvais calcul de l'offset (par exemple, oubliant le `+1` sur la largeur) fausse la distribution. Le retour d'un point basé sur `Math.random()` (float) puis l'arrondi peuvent introduire un biais caché parce que la résolution du flotteur n'est pas uniforme sur la plage entière. Autres
**Performance**Le prétraitement est linéaire dans `n` (= 100). La requête est logarithmique. L'utilisation d'une recherche linéaire par `pick()` est toujours acceptable ici, mais une interview peut s'attendre à `O(log n)` si `n` peut croître. La production de nombres aléatoires dans l'espace 64 bits sans module approprié peut déborder ou être inférieure à l'échantillon. Autres
**Quirks de la langue** Le python `random.randint(a, b)` est inclus aux deux extrémités; ajuster en conséquence. C++S `uniform_int_distribution` prend **liures inclusives** – utiliser `dist(rng)` correctement. Autres
**Pièges d'entrevue potentiels** – vous auriez besoin d'une approche différente (par exemple, des intervalles aléatoires pondérés). Et si les coordonnées étaient flottantes ? – la même idée fonctionne, mais vous auriez besoin de choisir à partir d'une gamme continue. Et si nous devions soutenir l'insertion/la suppression dynamique des rectangles ? – vous auriez besoin d'un arbre segmentaire ou Fenwick. Autres

---

- Oui. 6. Analyse de la complexité

Opération Temps Espace
- C'est quoi ?
**Construction**= `O(n)` – passe unique pour construire des montants de préfixe.= `O(n)` – stocker les rectangles et le tableau de préfixe. Autres
"O(log n)" – recherche binaire sur le tableau de préfixes (`n ≤ 100`). Autres

Parce que `n` est limité par 100, c'est essentiellement *constante* temps par requête dans la pratique, mais les garanties asymptotiques rendent la solution robuste pour les entrées plus grandes.

---

- Oui. 7. Interview-Ready Insights

* **Pourquoi avons-nous ajouté `+1` à la largeur et à la hauteur? * *
Les coordonnées du rectangle sont inclusives. Le comptage des points le long d'un axe doit comprendre les deux paramètres.

* **Et si les rectangles étaient autorisés à se chevaucher? * *
La technique de la somme préfixe fonctionne toujours, mais vous devez vous assurer que vous ne doublez pas les régions qui se chevauchent. Une astuce courante est de **scanline** l'avion pour construire un ensemble de sous-rectangles disjoints d'abord.

* **Et si nous avions besoin de points aléatoires continus? * *
Remplacer le calcul du décalage entier par un point flottant généré uniformément en `[0, largeur)` et `[0, hauteur)`. La logique de recherche binaire reste la même.

* ** Pouvons-nous faire mieux? **
Pour un très grand `n`, vous pouvez utiliser un arbre **segment** ou **Fenwick tree** pour réaliser le prétraitement `O(log n)` et les requêtes `O(log n)`. Mais avec `n ≤ 100` le tableau simple est préférable pour sa clarté.

---

- Oui. 8. Questions de suivi pour l'intervieweur

1. ** Contraintes de mémoire** – *Et si nous avions 10^5 rectangles? *
Discutez de la façon dont le tableau préfixe s'échelle et si vous avez besoin d'une structure de données plus sophistiquée (arbre de fenêtre/segment).

2. ** Mises à jour dynamiques** – *Les rectangles peuvent-ils être insérés ou enlevés après la construction? *
Parlez de la mise à jour de l'équilibre par rapport à la performance de la requête.

3. **Manipulation d'erreurs** – *Et si le générateur aléatoire est faible ou biaisé? *
Insistez sur l'utilisation de fonctions de bibliothèque éprouvées et évitez les PRNGs personnalisés à moins de spécifier.

4. **Cas d'Edge** – *Que se passe-t-il lorsqu'un rectangle a une zone zéro? *
Le nombre de points devient 0 ; l'algorithme doit gérer cela gracieusement (skiper de tels rectangles).

5. **Précision** – *Les coordonnées sont des nombres réels avec jusqu'à 6 décimales. *
Montrez comment adapter le calcul offset aux points flottants tout en préservant l'uniformité.

---

- Oui. 9. Résumé

- Oui. Le problème est une question classique *mapping aléatoire index → point*.
- Une somme préfixe de nombres de points + recherche binaire donne une solution ** exactement uniforme**.
- Oui. Soyez prudent avec l'inclusivité, le débordement et les limites aléatoires.
- Oui. Le code Java présenté, ainsi que ses homologues Python/C++, présente une implémentation propre, efficace et langagière.

Bonne chance avec votre entretien – vous avez maintenant à la fois la perspicacité algorithmique et le code pour l'appuyer!