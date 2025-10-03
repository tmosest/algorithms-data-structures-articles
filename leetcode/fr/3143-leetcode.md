---
titre: LeetCode 3143. Points maximums à l'intérieur de la place -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1. Aperçu du problème – Points maximaux à l'intérieur du carré

Mots-clés :
- C'est quoi ?
**3143**

**Objectif**
Vous recevez `points[i] = [x, y]` (coordonnées distinctes) et une chaîne `s` où `s[i]` est l'étiquette du point `i`.
Un carré **valable** est:

* centré sur l'origine `(0, 0)`
* bords parallèles aux axes
* ** pas de deux points à l'intérieur du carré partager la même balise * *

Retournez le nombre maximum de points qui peuvent être couverts par n'importe quel carré valide.

La longueur latérale du carré peut être nulle.

---

2. Pourquoi l'avidité ?

Observation Raison
C'est pas vrai.
Autres Le carré est défini par la coordination absolue *maximum* entre les points inclus (let `R = max(-x-y-y-)`). Autres
Autres Si une étiquette se produit deux fois avec des distances `d1 ≤ d2`, nous ne pouvons jamais inclure les deux points dans le même carré parce que le carré doit être assez grand pour le point plus éloigné (`d2`). Autres Par conséquent, la distance *seconde la plus petite* pour chaque balise détermine le premier conflit qui invaliderait un carré. Autres
Autres Pour toutes les étiquettes où la distance *la plus petite* est strictement inférieure à la distance *la deuxième plus petite*, nous pouvons inclure en toute sécurité le point avec la plus petite distance dans notre carré final. Le rayon carré peut être réglé à la plus grande distance minimale – tous les points choisis correspondent, et aucune balise n'est dupliquée. Autres

La réponse est donc le nombre d'étiquettes pour lesquelles
`minDistance[tag] < secondMinDistance[tag]`.

L'algorithme est **O(n)** time et **O(m)** space (`m` = nombre de balises distinctes).

---

Algorithme (Pseudo)

«» "
minDist = carte vide (étiquette → première plus petite distance)
deuxièmemin = +
nombre = 0

pour chaque point (x, y) avec l'étiquette t:
d = max. x, y) // distance de l ' origine au point
si t n'est pas dans minDist:
minDist[t] = d
sinon si d < minDist[t]:
2 min = min(secondemin, minDist[t])
minDist[t] = d
Sinon:
deuxièmemin = min(secondemin, d)

pour chaque étiquette dans minDist:
si minDist[tag] < secondMin:
nombre += 1

Nombre de retours
«» "

---

Code

Voici des solutions idiomatiques propres pour **Java**, **Python** et **C++**.

---

### 4.1 Java (Java 17)

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
int public maxPointsInsideSquare(int[][] points, Chaîne s) {
Carte<Caractère, entier> minDist = nouveau HashMap<>();
Int deuxième Min = entier. MAX_VALEUR;
nombre int = 0;

pour (int i = 0; i < points. longueur; i++) {
int d = Math.max(Math.abs[i][0]), Math.abs[i][1]);
marque de caractères = s.charAt(i);

si (!minDist.contientKey(tag)) {
minDist.put(tag, d);
} sinon si (d < minDist.get(tag)) {
deuxièmeMin = Math.min(secondeMin, minDist.get(tag));
minDist.put(tag, d);
} autre {
deuxièmemin = Math.min(secondemin, d);
}
}

pour (int d : minDist.values()) {
si (d < seconde minute) {
count++;
}
}
le nombre de retours;
}

public statique vide principal(String[] args) {
int[][] pts = {{2, 2}, {-1, -2}};
Balises à cordes = "ab";
System.out.println(nouvelle solution().maxPointsInsideSquare(pts, tags)); // 2
}
}
«» "

---

#### 4.2 Python (Python 3.10+)

'`python
de taper l'importation Liste, numéro

Solution de classe:
def maxPointsInsideSquare(self, points: List[List[int]], s: str) -> Int:
min_dist: Dict[str, int] = {}
second_min = flotteur('inf')

pour (x, y), étiquette dans zip(points, s):
d = max(abs(x), abs(y))
si l'étiquette n'est pas dans min_dist :
min_dist[tag] = d
elif d < min_dist[tag]:
second_min = min(second_min, min_dist[tag])
min_dist[tag] = d
Sinon:
seconde_min = min(seconde_min, d)

retour sum(1 pour d en min_dist.values() si d < second_min)
«» "

---

### 4.3 C++ (C++17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int maxPointsInsideSquare(vector<vector<int>>& points, chaîne s) {
non ordonné_map<char, int> minDist;
Int deuxième Min = INT_MAX;
nombre int = 0;

pour (size_t i = 0; i < points.size(); ++i) {
Int d = max(abs(points[i][0]), abs(points[i][1]);
marque de caractères = s[i];

si (!minDist.count(tag)) {
minDist[tag] = d;
} sinon si (d < minDist[tag]) {
la deuxièmemin = min(secondemin, minDist[tag]);
minDist[tag] = d;
} autre {
deuxièmemin = min(secondemin, d);
}
}

pour (auto &kv : minDist) {
si (kv.seconde < deuxièmemin) ++compte;
}
le nombre de retours;
}
};
«» "

Les trois solutions fonctionnent dans **temps linéaire** et utilisent une seule carte de hachage pour les balises.

---

5. Surmonter Liste de contrôle des cas

Cas d'Edge
-- -- -- -- -- -- -- -- --
Autres Pas de points ('points.longueur == Retour `0`. Autres
Autres Tous les tags uniques. Autres
Autres Tous les points ont la balise *même*. Autres
Points avec distance Ils sont parfaitement à l'intérieur d'un carré de taille zéro; manipulés de la même façon. Autres

---

C'est vrai. 6. Pièges communs (=Le mauvais et le mauvais)

1. **Diversité de la longueur du côté**
*De nombreux candidats considèrent la longueur latérale comme la longueur *pleine* plutôt que la moitié ('R'). *
**Fix:** Travaillez avec `R = max(==x,==y)`; le côté carré réel est `2R`.

2. **Remplissage au premier duplicata**
*Un simple - trié par R et cassé sur duplicata donne de mauvaises réponses quand un duplicata précoce bloque deux étiquettes uniques plus tard. *
**Fix:** Utilisez l'astuce min/seconde-min décrite ci-dessus.

3. **Dépassement de la distance**
*Si les coordonnées peuvent être `±10^9`, `max(abs(x),abs(y)` correspond à `int`. Évitez `long` à moins que vous ne sachiez que la portée dépasse `2^31‐1`. *
**Fix:** Utiliser `int` si les contraintes sont `=x=,=y ≤ 10^9`. Sinon passer à "long".

4. **Tag comme chaîne au lieu de char* *
C'est ça. est un caractère unique, pas une sous-chaîne. *
**Fix:** Utiliser `s.charAt(i)` (Java) / `s[i]` (Python) / `s[i]` (C++).

---

7. Vérification par essai

Texte
Entrée :
points = [[2,2], [-1,-2]]
s = "ab"
Produit: 2
«» "

Texte
Entrée :
points = [[-1,-2],[3,0],[0,3]]
s = "aaB"
Sortie: 1 // seule la 'a' la plus proche peut être prise
«» "

Texte
Entrée :
points = [[0,0],[1,1],[2,2]]
s = "abc"
Sortie: 3 // toutes les étiquettes uniques, côté carré 4 correspond à tous
«» "

Exécutez le code dans n'importe quelle langue et vérifiez les sorties.

---

8. Les bonnes, les mauvaises, et le laid des solutions d'entrevue

Aspect du bien
- C'est quoi ?
**Complexité**= O(n) cupide, facile à prouver== O(n log n) tri ou recherche binaire – plus lourd sur l'explication== O(n2) brute-force, accepté uniquement sur les données de jouets==
**Readability**
**Robustness**=Poigne les carrés de taille zéro, les coordonnées négatives==Fails quand les étiquettes dupliquées apparaissent tôt mais les points ultérieurs peuvent être choisis==_______________________________________________________________________________________________________________________________________________________________________________________________________________________

**À emporter :**
Pour une entrevue *logiciel-ingénierie*, vous voulez la solution *la plus propre, la plus rapide et la plus facile à expliquer* – la cupidité **min-vs-seconde-min** est exactement cela.

---

9. Conseils de préparation à l'entrevue

1. ** Expliquez d'abord la distance métrique ('R'). **
Étant donné que le carré est aligné sur l'axe et centré à l'origine, tout point à l'intérieur doit satisfaire aux conditions suivantes: `=x==R` et `=y==R`. Le carré est donc complètement déterminé par le maximum de ces deux valeurs absolues. (en milliers de dollars)

2. **Afficher la logique de conflit avec un petit exemple** (contre-exemple `a(1), a(2), b(3)`).
Cela démontre que vous comprenez vraiment pourquoi une étiquette ne peut pas apparaître deux fois.

3. **Mention la nature à deux passages** (min → secondeMin → compter) et donner la complexité à l'avant.

4. ** Prime facultative:**
Si l'intervieweur demande une longueur *réelle* côté carré, il suffit de sortir `2 * maxMinDist` où `maxMinDist` est le plus grand `minDist` qui satisfait la condition.

---

10 ans. Résumé

* Le problème se réduit à choisir un point par étiquette de sorte que la distance **maximum** entre les points choisis soit minimisée.
* L'astuce cupide "Small vs second-smallest" donne l'optimum dans le temps linéaire.
* Des implémentations propres existent en Java, Python et C++ – toutes identiques en logique.
* Soyez prêt à expliquer l'intuition et la manipulation des cas de bord – c'est ce que les *intervieweurs* cherchent.

Bonne chance pour votre prochain entretien de codage – vous avez l'algorithme *golden*! - Oui.

---

**Mots-clés**: Leetcode, interview de codage, points maximum dans le carré, entretien Java, entretien Python, entretien C++, algorithme gourmand, complexité du temps, complexité de l'espace, travail d'ingénierie logicielle, préparation d'entrevue.