---
titre: LeetCode 1914. Rotation cyclique d'une grille -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes – LeetCode 1914

** Problème* *
> Avec une matrice de taille égale «grid» (m × n) et un entier «k»,
> faire pivoter chaque couche de la matrice dans le sens anti-horaire par des positions `k`.
> `k` peut être aussi grand que 109, de sorte que la rotation doit être effectuée en **O(1)** par élément.

A *shell* est l'ensemble de cellules qui partagent la même distance Manhattan de la frontière extérieure.
La coque extérieure contient toutes les cellules de bordure, la coque suivante est la
bordure de la sous-matrice qui reste après avoir pelé la couche externe, et ainsi de suite.

> **Retourner la grille après que toutes les coquilles ont été tournées. **

**Contrôles* *

Valeur des contraintes
C'est quoi ?
Longueur du réseau
Durée du réseau
Oui
`0 ≤ grille[i][j] ≤ 1000 ' , oui
Oui

Le but est une solution temporelle **O(m·n)** qui utilise seulement **O(m·n)** mémoire supplémentaire (ou encore moins).

---

- Oui. 2. Algorithme de haut niveau

1. **Peel chaque coque**
* Déplacer dans le sens des aiguilles d'une montre / dans le sens des aiguilles d'une montre le long des quatre bords (en haut → gauche → en bas → à droite) et recueillir les éléments dans un tableau 1-D `shell[]`.
2. **Roter le tableau 1-D**
* Parce que `k` peut être énorme, tourner seulement `k % shell.length` times.
* Une rotation de gauche par `r` peut être faite en place avec un astuce *reverse* (ou par slice).
3. **Écrire le shell tourné en arrière**
* Itérer sur les mêmes quatre bords dans le même ordre et écraser la matrice originale avec les valeurs tournantes.
4. **Raccord pour chaque coque**
* Commencez avec la coque extérieure (`top = 0`, `left = 0`, `bottom = m-1`, `right = n-1`) et rétrécissez les bordures jusqu'à `top >=bottom` ou `left >=right`.

---

- Oui. 2. Mise en œuvre du code

Ci-dessous vous trouverez trois solutions indépendantes, une dans chacune des trois langues d'entretien les plus courantes.

> **Astuce:** Dans chaque implémentation prête à l'entretien, nous utilisons `k %= shellLen` immédiatement après l'extraction du shell, de sorte que nous n'itérerons jamais plus que nécessaire.

---

### 2.1 Java (temps O(m·n), espace supplémentaire O(m·n)

"Java
Importation de java.util.*;

solution de classe {
(c) (c) (c)
int m = longueur de grille, n = longueur de grille[0];
int top = 0, gauche = 0, fond = m - 1, droite = n - 1;

pendant que (en haut < en bas && gauche < à droite) {
// 1. Extraire le shell actuel dans un tableau 1-D
int len = 2 * (en bas - en haut + à droite - à gauche);
int[] shell = nouvelle int[len];
Int idx = 0;

pour (int r = haut; r < bas; r++) // colonne gauche (haut→fond)
shell[idx++] = grille[r][gauche];
pour (int c = gauche; c < droite; c++) // ligne inférieure (gauche→droite)
shell[idx++] = grille[bottom][c];
pour (int r = bas; r > haut; r--) // colonne droite (bottom→top)
shell[idx++] = grille[r][droit];
pour (int c = droite; c > gauche; c--) // rang supérieur (droite→gauche)
shell[idx++] = quadrillage[top][c];

// 2. Rotation de la coque
déplacement int = k % len;
si (poste != 0) {
int[] tournée = nouvelle int[len];
pour (int i = 0; i < len; i++) {
rotationd[i] = shell[(i + shift) % len];
}
shell = rotation;
}

// 3. Rédigez le shell rotatif
idx = 0;
pour (int r = haut; r < bas; r++) // colonne de gauche
grid[r][left] = shell[idx++];
pour (int c = gauche; c < droite; c++) // ligne inférieure
grid[bottom][c] = shell[idx++];
pour (int r = bas; r > haut; r--) // colonne de droite
grid[r][right] = shell[idx++];
pour (int c = droite; c > gauche; c--) // rang supérieur
grid[top][c] = shell[idx++];

// Réduire le rectangle pour la coque suivante
haut++; bas--; gauche++; droite--;
}
la grille de retour;
}
}
«» "

**Complexité* *

- Oui.
-- -- -- -- -- --
**Temps**="O(m·n)" – chaque élément est lu et écrit une fois par shell="
Dans le pire des cas (la coque extérieure) – peut être réduit à "O(min(m,n)" en réutilisant un seul tableau

---

#### 2.2 Python 3 (temps O(m·n), espace supplémentaire O(m·n)

'`python
Solution de classe:
def rotationGrid(self, grille: List[List[int]], k: int) -> Liste[Liste[int]]:
m, n = len(grid), len(grid[0])
en haut, à gauche, en bas, à droite = 0, 0, m - 1, n - 1

en haut < en bas et à gauche < à droite:
1. Extraire la coque actuelle
coque = []

pour r dans la plage (haut, bas): # colonne de gauche
shell.append(grid[r][gauche])

pour c dans la plage (gauche, droite): # rang inférieur
shell.append(grid[bottom][c])

pour r dans la plage (en bas, en haut, -1): # colonne de droite
shell.append(grid[r][droit])

pour c dans l'intervalle (droite, gauche, -1): # rang supérieur
shell.append(grid[top][c])

# 2. Rotation laissée par k % len(shell)
déplacement = k % len(shell)
en cas de déplacement:
shell = shell[shift:] + shell[:shift]

3. Réécrivez
idx = 0
pour r dans la plage (haut, bas): # colonne de gauche
grille[r][gauche] = shell[idx]; idx += 1

pour c dans la plage (gauche, droite): # rang inférieur
quadrillage[fond][c] = coque[idx]; idx += 1

pour r dans la plage (en bas, en haut, -1): # colonne de droite
grille[r][droite] = shell[idx]; idx += 1

pour c dans l'intervalle (droite, gauche, -1): # rang supérieur
quadrillage[top][c] = shell[idx]; idx += 1

haut, bas, gauche, droite = haut + 1, bas - 1, gauche + 1, droite - 1

grille de retour
«» "

**Complexité* *

- Oui.
-- -- -- -- -- --
**Heure** Autres
**L'espace**=O(min(m, n)=" – le tableau de shell temporaire="

---

#### 2.3 C++ (temps O(m·n), espace supplémentaire O(m·n)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur<vector<int>> rotationGrid(vector<vector<int>>& grille, int k) {
int m = quadrillage(), n = quadrillage[0].size();
int top = 0, bas = m - 1, gauche = 0, droite = n - 1;

pendant que (en haut < en bas && gauche < à droite) {
// 1. Coque d ' extrait
vecteur<int> coque;
pour (int r = haut; r < bas; ++r) // colonne de gauche
shell.push_back(grid[r][gauche]);

pour (int c = gauche; c < droite; ++c) // ligne inférieure
shell.push_back(grid[bottom][c]);

pour (int r = bas; r > haut; --r) // colonne de droite
shell.push_back(grid[r][droite]);

pour (int c = droite; c > gauche; --c) // rang supérieur
shell.push_back(grid[top][c]);

// 2. Rotation gauche par k % shell.size()
déplacement int = k % shell.size();
si (classement) {
rotation (shell.begin(), shell.begin() + déplacement, shell.end());
}

// 3. Réécrivez
Int idx = 0;
pour (int r = haut; r < bas; ++r)
grid[r][left] = shell[idx++];

pour (int c = gauche; c < droite; ++c)
grid[bottom][c] = shell[idx++];

pour (int r = fond; r > haut; --r)
grid[r][right] = shell[idx++];

pour (int c = droite; c > gauche; --c)
grid[top][c] = shell[idx++];

++top; --bottom; ++left; --right;
}
la grille de retour;
}
};
«» "

**Complexité* *

- Oui.
-- -- -- -- -- --
**Heure** Autres
**L'espace**="O(min(m,n)"– le tableau de shell="

> **Pourquoi nous faisons `k % shell.size()`? **
> Rotation d'un shell de longueur `L` par des positions `L` ou `2·L` est l'identité.
> L'utilisation du modulo élimine le travail inutile lorsque `k` est énorme.

---

- Oui. 3. Code: Ce que les intervieweurs cherchent

- Oui.
-- -- -- -- -- --
**Bien**.
Utiliser `k % shellLen` juste après extraction. Autres
Réduit les limites en une seule ligne (`++top; --bottom; ...`). Autres
Les commentaires expliquent *pourquoi *pas *comment* (p. ex., rotation dans le sens antihoraire par quart de gauche). Autres
**Recalcule la longueur du shell plusieurs fois; n'utilise pas modulo; réécrit sans utiliser directement le tableau rotatif. Autres
Boucles imbriquées avec contrôles redondants. Autres
Aucun commentaire ni explication concernant la rotation inverse. Autres

---

- Oui. 4. Code Bad – Un mini-guide

Caractéristiques Bonne mauvaise
C'est pas vrai.
**Clarté**="extractShell()`, `rotateArray()`, `writeBack()` helpers=" Tout est enchevêtré en une seule boucle="
**Connaissance de la complexité**
**Rétrécissement de l'extrémité de la ligne ('++top; --bottom; ...') Plusieurs variables ont changé dans des lignes séparées, rendant les bogues faciles.
Commentaires expliquant chaque étape Aucun commentaire, juste un code
**Tests**=Poignées vides / matrices à 1 cellule (cas de bord)= uniquement pour le cas type=

---

- Oui. 5. Pourquoi cela compte pour les entrevues

1. **La complexité du temps est le premier signal** – les recruteurs demandent la meilleure complexité possible.
"O(m·n)" est le temps minimum; tout lent sera immédiatement rejeté.
2. **L'espace-complexité montre la conscience** – en utilisant "O(min(m,n)" au lieu de "O(m·n)" révèle que vous savez que la longueur de la coquille est limitée par la dimension plus petite.
3. **Le tour de moto pour l'énorme `k`** – démontre que `k` peut déborder et que les rotations sont cycliques.
4. **Code lisible et autonome** – code de valeur des intervieweurs qu'ils peuvent lire, tester et expliquer en moins d'une minute.

---

- Oui. 6. Code Bad – Liste de contrôle finale

- [ ] ** Extraction de shell** faite une fois par coquille.
- [ ] **Rotation** utilise `k % shellLen` immédiatement.
- [ ] **L'écriture-retour** suit le même ordre que l'extraction.
Les variables** pour les limites des rectangles sont mises à jour atomiquement.
- [ ] **Commentaires** expliquer *pourquoi* nous faisons chaque étape.
- [ ] **Pas de limites codées en dur** – les échelles de solution avec taille d'entrée.

---

- Oui. 7. TL;DR pour les intervieweurs

> *Vous épluchez une coquille, faites pivoter sa représentation 1-D par `k % de longueur`, et écrivez-la. Répétez jusqu'à ce que toutes les coquilles soient terminées. Mettre cela en œuvre dans l'espace O(m·n) et O(min(m,n). *

---

- Oui. 8. A emporter

> Les solutions présentées sont **parfaites pour les entrevues techniques**:
> * Ils résolvent le problème dans les limites des contraintes.
> * Ils mettent en valeur la perspicacité algorithmique (coquilles de peeling, tour de rotation inverse).
> * Ils sont écrits en **Java, Python et C++**, couvrant la majorité des piles d'interviews.

Bonne chance avec votre préparation d'entrevue, et rappelez-vous: une solution propre et bien commentée est beaucoup plus impressionnante qu'une solution rapide et illisible. Bon codage !

---

Questions fréquentes

* ** Pouvons-nous résoudre cela avec O(1) espace supplémentaire? **
Oui – vous pouvez faire pivoter le shell en place avec un échange à quatre sens. Il est un peu plus impliqué, mais toujours temps O(m·n).
* **Pourquoi la rotation gauche par `r` fonctionne pour le mouvement anti-horaire? * *
Parce que nous avons recueilli la coquille dans l'ordre *horaire*, une rotation de gauche par `r` place l'élément qui était `r` en avant sur la position actuelle, ce qui équivaut à une rotation antihoraire dans la matrice 2-D.
* ** Devons-nous gérer des dimensions bizarres? **
Le problème garantit des dimensions égales, donc le rectangle intérieur se rétrécit toujours uniformément.

---

Bonne interview-préparation! Si vous avez des questions ou que vous voulez plonger plus profondément dans le tour de la rotation inverse, faites-le moi savoir.