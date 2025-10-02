---
titre: LeetCode 1828. Enquêtes sur le nombre de points dans un cercle -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 1828 – requêtes sur le nombre de points dans un cercle
> **Objectif:** Compter combien de points donnés se trouvent à l'intérieur (ou à la frontière de) chaque cercle de requête.
> **Platforms:** Java, Python, C++
> **SEO Mots-clés:** LeetCode 1828, Questions sur le nombre de points à l'intérieur d'un cercle, Solution Java, solution Python, solution C++, entretien par algorithme, temps O(n2), conseils d'entretien d'emploi

---

- Oui. 1. Déclaration de problème (simplifiée)

Vous recevez:

Sens de la variable
C'est pas vrai.
"points[i] = [xi, yi]"" Coordonnées du point *i*-ème (0 ≤ xi, yi ≤ 500) Autres
Centre `(xj, yj)` et rayon `rj` (1 ≤ rj ≤ 500)

Pour chaque requête, affichez le nombre de points qui satisfont

«» "
(xi – xj)2 + (yi – yj)2 ≤ rj2
«» "

(Les points à la frontière comptent comme à l'intérieur.)

Contraintes:
`1 ≤ points.longueur, requêtes.longueur ≤ 500`

---

Naïve Brute Approche de la force

1. **Loop sur chaque requête. **
2. **Couper sur chaque point. **
3. Calculer la distance au carré et comparer avec `r2`.

> **Complexité temporelle:** `O(Q · P)` → au plus `500 × 500 = 250 000` vérifications de distance.
> **Complexité spatiale:** (supprime le tableau de résultats).

Avec les limites données, cette solution passe confortablement, mais nous allons également explorer une méthode plus rapide.

---

- Oui. 3. C'est bon, mauvais, mauvais de la Forte-Force

Aspect du bien
- C'est quoi ?
**Mise en oeuvre**=Loops simples et unipasses== Nécessite `Math.pow` ou multiplication manuelle==La surutilisation des maths flottants (`Math.pow`) peut être lente et imprécise==
**Performance**) Acceptable pour 500×500) Quadratic → peut devenir lourd pour de plus grandes contraintes.
**Readability**= Effacer, peu de lignes== Code répétitif==___________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
* Maintenabilité * Facile à comprendre * Difficile à modifier pour de nouvelles fonctionnalités (p. ex., points pondérés)

---

4. Optimisation avec un préfixe 2D (Grid)

Parce que toutes les coordonnées se trouvent dans `[0, 500]`, nous pouvons pré-construire une grille 2-D `cnt[x][y]` qui enregistre le nombre de points assis à chaque cellule. Puis nous calculons une somme préfixe `pré[x][y]`. Pour tout cercle, nous pouvons:

1. **Itérer sur x** de `cx - r` à `cx + r`.
2. Pour chaque `x`, calculez la gamme `y` qui satisfait l'inégalité du cercle.
3. Utilisez la somme du préfixe pour demander combien de points se trouvent entre les deux bornes Y dans *O(1)*.

Cela réduit chaque requête de `O(P)` à `O(r)` (= 500). complexité générale: "O(P + Q·maxR)" → toujours bon pour les limites données.

---

- Oui. 5. Mise en œuvre

Voici des solutions propres et prêtes à la production pour **Java, Python et C++**.
Tous les trois utilisent la méthode de la force brute pour la clarté; la variante préfixe-sum est également affichée comme commentaire pour les lecteurs avancés.

---

##### 5.1 Java (Java 17)

"Java
// Fichier: Solution.java
Importation de java.util.*;

solution de classe publique {
public int[] countPoints(int[][] points, int[][] requêtes) {
int qLen = requêtes. longueur;
résultat int[] = nouveau résultat int[qLen];

pour (int i = 0; i < qLen; ++i) {
int cx = requêtes[i][0];
int cy = requêtes[i][1];
int r = requêtes[i][2];
r2 = (long) r * r; // utiliser longtemps pour éviter les débordements

cnt = 0;
pour (int[] p : points) {
longue dx = p[0] - cx;
longue dy = p[1] - cy;
si (dx * dx + dy * dy <= r2) cnt++;
}
résultat[i] = cnt;
}
le résultat du retour;
}

- Oui. Version de grille optimisée en option - Oui.
// Précalculez une somme de préfixe 2D pour le temps de requête O(r).
// Décommentez si vous voulez l'utiliser au lieu de la boucle naïve.
public int[] countPointsGrid(int[][] points, int[][] requêtes) {
MAX = 500;
int[] cnt = nouveau int[MAX + 1][MAX + 1];
pour (int[] p : points) cnt[p[0]][p[1]]++;

// Construire des montants préfixés
int[][] pre = nouveau int[MAX + 2][MAX + 2];
pour (int x = 0; x <= MAX; ++x) {
pour (int y = 0; y <= MAX; ++y) {
Pré[x + 1][y + 1] = cnt[x][y] + pre[x][y + 1]
+ pre[x + 1][y] - pre[x][y];
}
}

int qLen = requêtes. longueur;
int[] res = nouveau int[qLen];
pour (int i = 0; i < qLen; ++i) {
int cx = requêtes[i][0];
int cy = requêtes[i][1];
int r = requêtes[i][2];
int minX = Math.max(0, cx - r);
int maxX = Math.min(MAX, cx + r);
= 0;

pour (int x = minX; x <= maxX; ++x) {
int dx = x - cx;
int maxDy = (int) Math.floor(Math.sqrt(r * r - dx * dx));
int minY = Math.max(0, cy - maxDy);
int maxY = Math.min(MAX, cy + maxDy);
total += requêtePréfixe(pre, minX, minY, maxX, maxY);
}
res[i] = total;
}
retour rés;
}

requête privée intPrefix(int[]] Pré, int minX, int minY, int maxX, int maxY) {
retour pré[maxX + 1][maxY + 1] - pré[minX][maxY + 1]
- pre[maxX + 1][minY] + pre[minX][minY];
}
----------------------------------- */
}
«» "

**Pourquoi c'est prêt* *

- Utilise `long` pour éviter le débordement entier.
- Évite `Math.pow` pour la vitesse.
- Effacer les noms de variables (`cx`, `cy`, `r2`).
- Autonome, pas de dépendance externe.

---

5.2 Python 3

'`python
# Fichier : solution. py
de taper l'importation Liste

Solution de classe:
def countPoints(self, points: List[List[int]],
questions : Liste[List[int]]) -> Liste[int]:
res = []
pour cx, cy, r dans les requêtes:
r2 = r * r
cnt = 0
pour x, y en points:
dx = x - cx
dy = y - cy
si dx * dx + dy * dy <= r2:
cnt += 1
res.append(cnt)
retour res

♪ ------------------------------------------------------------------------
# Optimisation optionnelle par grille (préfixer les sommes)
♪ ------------------------------------------------------------------------
# def countPointsGrid(points, requêtes) :
MAX = 500
# cnt = [[0]*(MAX+1) pour _ dans la plage(MAX+1)]
# pour x, y en points:
# cnt[x][y] += 1
# pre = [[0]*(MAX+2) pour _ dans la gamme(MAX+2)]
# pour x dans la plage(MAX+1):
# pour y dans la plage(MAX+1):
# pre[x+1][y+1] = cnt[x][y] + pre[x][y+1] + pre[x+1][y] - pre[x][y]
# requête def(minx, miny, maxx, maxy):
# retour pre[maxx+1][maxy+1] - pre[minx][maxy+1] - pre[maxx+1][miny] + pre[minx][miny]
# res = []
# pour cx, cy, r dans les requêtes:
Nombre total = 0
# pour x dans la plage(max(0, cx-r), min(MAX, cx+r)+1):
# dx = x - cx
# max_dy = int((r*r - dx*dx)**0,5)
# miny = max(0, cy-max_dy)
# maxy = min(MAX, cy+max_dy)
# total += requête(x, miny, x, maxy)
# res.append(total)
# retour rés
«» "

**Python : faits saillants**

- Le typage explicite maintient le type de code sûr pour les analyseurs statiques.
- Utilise l'arithmétique entier pour la vitesse.
- Oui. La version optionnelle de la grille est commentée mais prête pour copier-coller.

---

#### 5.3 C++17

'`cpp
// Fichier: solution.cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur<int> countPoints(vecteur<vecteur<int>>& points,
vector<vector<int>&questions) {
vecteur <int> ans;
pour (auto& q : requêtes) {
int cx = q[0], cy = q[1], r = q[2];
long r2 = 1LL * r * r; // 64-bit garde
cnt = 0;
pour (auto& p : points) {
long dx = p[0] - cx;
long dy = p[1] - cy;
si (dx * dx + dy * dy <= r2) ++cnt;
}
as.push_back(cnt);
}
le retour des an;
}

/* ---------------------------------------------------
// Mise en œuvre de la grille optimisée optionnelle (préfixe sum)
---------------------------------------------------
vecteur<int> countPointsGrid(vecteur<vecteur<int>>& points,
vector<vector<int>&questions) {
const int MAX = 500;
vecteur<vector<int>> cnt(MAX+1, vecteur<int>(MAX+1, 0));
pour (auto& p : points) cnt[p[0]][p[1]]++;

// Montants préfixés 2-D
vector<vector<int>> pre(MAX+2, vector<int>(MAX+2, 0));
pour (int x=0; x<=MAX; ++x)
pour (int y=0; y<=MAX; ++y)
pre[x+1][y+1] = cnt[x][y] + pre[x][y+1] + pre[x+1][y] - pre[x][y];

requête automatique = [&](int minx, int miny, int maxx, int maxy) {
retour pre[maxx+1][maxy+1] - pre[minx][maxy+1]
- pre[maxx+1][mineur] + pre[minx][mineur];
};

vecteur<int> rés;
pour (auto& q : requêtes) {
int cx = q[0], cy = q[1], r = q[2];
= 0;
pour (int x = max(0, cx-r); x <= min(MAX, cx+r); ++x) {
long dx = x - cx;
int maxdy = static_cast<int>(sqrt(r*r - dx*dx));
int miny = max(0, cy-maxdy);
int maxy = min(MAX, cy+maxdy);
total += requête(minx=min(0, cx-r), miny, maxx=max(0, cx+r), maxy);
}
res.push_back(total);
}
retour rés;
}
---------------------------------------------------- */
};
«» "

**Caractères clés prêts à l'emploi**

- Évite "pow()" en utilisant la multiplication entière.
- "long long" garantit la sécurité contre le débordement.
- Standard `<bits/stdc++.h>` header garde le fichier minimal.

---

- Oui. 6. Recapture de complexité

Mise en œuvre
- C'est quoi ?
"O(Q · P)" (= 2,5 × 105 ops)="O(1)" Autres
Préfixe de la grille (facultatif)

Les deux approches sont ** bien dans la limite de 1 seconde** sur LeetCode. La variante de grille brille lorsque les contraintes augmentent (par exemple, 10 000 points ou 10 000 requêtes).

---

- Oui. 7. Cas d ' essai d ' échantillon

Texte
points = [[1, 1], [2, 2], [3, 3], [4, 4]]
requêtes = [[2, 2, 2], [1, 1, 1], [0, 0, 10]]
«» "

Demande de renseignements Résultat
C'est quoi ?
(2, 2, 2) 3 (points à (1,1), (2,2), (3,3) sont à l'intérieur)
1 (uniquement (1,1)) Autres
0, 0, 10) 4 (tous les points dans un grand cercle)

Exécuter l'une des trois implémentations sur cette entrée retourne `[3, 1, 4]`.

---

### 8.

Qu'est-ce que regarder
C'est pas vrai.
**Le grand rayon** (`r = 500`) Autres
**Le résultat devrait être "[0, 0, ...]". Autres
**Points dupliqués**= Chaque duplicata contribue séparément – l'algorithme les compte tous. Autres
**Tous les points situés à la frontière doivent encore être comptés; l'inégalité est `==". Autres
**Dépassement**= Utiliser 64 bits (`long`/`long long`) pour le calcul de la distance. Autres

---

- Oui. 9. Les pensées finales

- **Pour les intervieweurs**: La solution simple O(Q·P) est une base solide. Il démontre la maîtrise des boucles de base, les formules de distance, et la manipulation de type soigneuse.
- **Pour les recruteurs**: Votre code devrait être **compact, correct et sûr** – l'exemple Java ci-dessus répond à ces critères.
- **Pour l'autoapprentissage**: Essayez d'échanger la boucle naïve avec la version préfixe du réseau. Il enseigne les sommes préfixes 2-D, qui apparaissent dans de nombreuses questions d'algorithme avancées (questions de portée, distance Manhattan, etc.).

---

- Oui. 10. À emporter pour la prochaine entrevue d'embauche

1. **Commencez simplement.** Montrez que vous pouvez résoudre le problème avec une logique claire avant de plonger dans des optimisations.
2. ** Expliquez vos compromis.** Les intervieweurs aiment quand vous parlez du bon, mauvais, laid de votre solution.
3. **Nettoyez le code :**
- Éviter les appels inutiles de fonction (`Math.pow`).
- Utilisez des entiers 64 bits où le dépassement est un risque.
- Nommez les variables de façon descriptive.
4. **Test rigoureux**: Inclure les cas d'angle dans vos tests unitaires.
5. **Parler de l'échelle**: Mentionnez comment la solution pourrait être améliorée si les contraintes se développaient (préfixation du réseau, indexation spatiale, etc.).

En suivant ces étapes vous allez non seulement ace LeetCode 1828 mais aussi démontrer l'état d'esprit d'ingénierie que les recruteurs recherchent.

Bon codage ! Les

---