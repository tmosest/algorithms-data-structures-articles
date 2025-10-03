---
titre: LeetCode 1779. Trouver le point le plus proche qui a la même coordonnées X ou Y -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1779 – Trouvez le point le plus proche qui a la même coordonnées X ou Y
**LeetCode 1779: Facile**
Langue Code Complexité
- C'est quoi ?
**Java** ValidPoint(int x, int y, int[][] points)""O(n)` time, `O(1)` espace
**Python**="def le plus procheValidPoint(x: int, y: int, points: List[List[int]])=> int`="O(n)` time, `O(1)` espace
**C++**= <int la plus procheValidPoint(int x, int y, vector<vector<int>>& points)===<O(n)======================================================================================================================================================================================================================== espace

---

Solutions de code

### Java

"Java
solution de classe {
Int public le plus proche ValidPoint(int x, int y, int[][] points) {
int minDistance = entier.MAX_VALUE; // garde la trace de la plus petite distance de Manhattan
int bestIndex = -1; // -1 indique "aucun point valide trouvé"

pour (int i = 0; i < points. longueur; i++) {
int px = points[i][0];
int py = points[i][1];

// Un point n'est valide que s'il partage la même coordonnées x ou y.
si (px) [x]
distance int = Math.abs(px - x) + Math.abs(py - y);

// Mettre à jour lorsque nous trouvons une distance strictement plus petite
si (distance < minDistance) {
minDistance = distance;
bestIndex = i;
}
}
}

retour bestIndex; // sera -1 si aucun point valide n'existe
}
}
«» "

Python

'`python
de taper l'importation Liste

Solution de classe:
def le plus proche ValidPoint(self, x: int, y: int, points: List[List[int]]) -> Int:
min_dist = flotteur('inf')
best_idx = -1

pour i, (px, py) dans l'énumération (points):
si px == x ou py == y:
dist = abs(px - x) + abs(py - y)
si dist < min_dist:
min_dist = dist
best_idx = i

return best_idx
«» "

C++

'`cpp
solution de classe {
public:
int la plus procheValidPoint(int x, int y, vector<vector<int>& points) {
int minDist = INT_MAX;
int mieux Idx = -1;

pour (int i = 0; i < points.size(); ++i) {
int px = points[i][0];
int py = points[i][1];

si (px) [x]
int dist = abs(px - x) + abs(py - y);
si (dist < minDist) {
minDist = dist;
bestIdx = i;
}
}
}
le meilleur retour Idx;
}
};
«» "

---

Récapitulation des problèmes et contraintes

**Input**: point actuel `(x, y)` et liste `points` des points `N`, chacun `[ai, bi]`.
- **Point Valide** : partage soit le même "x" soit le même "y".
- **Objectif** : retourner l'index du point le plus proche* valide par la distance Manhattan.
- **Tie‐break**: si deux points sont également proches, choisissez celui avec l'indice *le plus petit*.
- **Pas de point valide**: retour `-1`.
- **Constraints**
- `1 ≤ N ≤ 10^4`
- `1 ≤ x, y, ai, bi ≤ 10^4`

---

Les bons, les mauvais et les méchants

Aspect Ce que cela signifie Comment il affecte les entrevues
- C'est quoi ?
**Le bon**** - **O(N) temps** – balayage linéaire, aucune structure de tri ou de données supplémentaires. <br>- **O(1) espace** – nous ne stockons que quelques entiers. <br>- Poigne les cas de bord (p. ex., le point lui-même, aucun point valide). Affiche que vous pouvez raisonner sur les contraintes, choisir l'algorithme le plus simple, et garder l'utilisation de la mémoire minimale – une attente d'entrevue commune. Autres
**Le mauvais** - **Le calcul de distance manhattan** peut être une source d'erreurs hors-par-un si vous oubliez la valeur absolue. <br>- Erreurs dans le fait de prendre le même `x` ** ou** pour le même `y`=" pour les deux? est un piège classique. Autres Des erreurs mineures de codage peuvent causer une mauvaise réponse, donc il est essentiel de tester la logique en profondeur. Autres
**La manipulation de l'index**: initialiser `bestIdx` à `0` briserait le cas de point valide de l'index; vous avez besoin de `-1`. <br>- **Tie-break**: ignorer le plus petit indice lorsque les distances sont égales résultats dans un WA sur des cas de test comme `[[1, 2], [1, 2]`. Toujours écrire des tests unitaires pour couvrir les cas de bord. Autres

---

Comment expliquer le problème dans une entrevue

1. ** Clarifier l'énoncé du problème* *
- Le point actuel est-il inclus? Oui, ça peut être un point valable.
- Que faire si deux points sont à la même distance? → Retourner l'index inférieur.

2. ** Pensez aux contraintes**
- `N` jusqu`à `10^4` → Une solution `O(N^2)` TLE.
- Les coordonnées sont de petits ints positifs → Pas de structure de données spéciale nécessaire.

3. **Ébauche d'une approche de force brute**
- Boucler sur chaque point, calculer la distance si elle est valide.
- Gardez une trace de la distance et de l'index min.

4. **Proof d'optimalité* *
- Chaque point est examiné une fois → Le temps linéaire est optimal car chaque point pourrait être la réponse.

5. **Optimisation de l'espace**
- Pas besoin de contenants auxiliaires, il suffit de garder quelques inter.

6. **Passer dans un échantillon* *
- Montrez comment vous traitez la rupture d'attache et pas de point valide.

---

Cas de bord à tester

Autres Test d'entrée prévu
- C'est quoi ?
= [3, 4]» `0` (même emplacement)
[[2,3]]» `-1` (sans objet)
"x = 3, y = 4, points = [[3,1],[2,4],[4,4]" "2" (coupe de distance, indice inférieur)
= 5, y = 5, points = [[5,5],[5,5],[5,5]» "0" (premier événement)
= [[2,3],[4,5]]

---

## C'est le SEO et les conseils de recherche d'emploi

- **Titre riche en mots-clés**: LeetCode 1779: Trouvez le point le plus proche avec les mêmes solutions X ou Y – Java, Python & C++
- **Description détaillée**: Apprendre à résoudre le LeetCode 1779 – Trouvez le point le plus proche qui partage la coordination X ou Y. Solutions Java, Python et C++ détaillées, analyse de complexité et conseils d'entretien. (en milliers de dollars)
- **En-têtes**: Utilisez les balises H2 pour *Récapitulation des problèmes*, *Solutions de code*, *Analyse de la complexité*, *Les bons, les mauvais et les mauvais*, *Stratégie d'entrevue*.
- **Liens internes**: Lien vers d'autres problèmes liés au LeetCode que vous avez résolus (p. ex., série de points proches).
- **Liens externes**: Cite l'URL officielle du problème LeetCode, et les références de la solution que vous avez mentionnées.
- **Données structurées**: Ajouter JSON‐LD pour l'article référencement (facultatif pour un blog).

---

À emporter

- **Simple Scan linéaire** est tout ce dont vous avez besoin:
Texte
pour chaque point:
si même x ou même y:
Calcul de la distance Manhattan
Mettre à jour le mieux si distance < courant min
«» "
- **Initialiser l'indice à -1** pour différencier -no valide point de l'index 0.
- **Déclenchement**: garder le premier événement; pas besoin de comparaisons supplémentaires.

Cette solution fonctionne dans **O(N)** temps, **O(1)** espace, et passe tous les cas de bord. La maîtrise de ces problèmes fera briller votre portefeuille d'entretiens techniques et vous donnera la confiance nécessaire pour relever le prochain défi.

Bon codage, et bonne chance pour votre prochaine interview! C'est ce qu'il a dit