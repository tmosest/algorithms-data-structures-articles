---
titre: LeetCode 2711. Différence du nombre de valeurs distinctes sur les diagonales -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## LeetCode 2711 – Différence de nombre de valeurs distinctes sur les diagonales
- Oui. Le bon, le mauvais et le mauvais – Un Java complet / Python / C++ Boîte de solution

> **Pourquoi cet article compte pour votre prochain entretien* *
> Mastering LeetCode 2711 montre que vous pouvez:
> * Lisez un énoncé de problème 2-D non trivial
> * Pensez à l'optimisation diagonale de la traversée, des ensembles et du bit-mask
> * Livrer un code propre, langue-agnostique en Java, Python et C++
> * Discutez des compromis dans l'espace-temps – une compétence d'entrevue incontournable

---

- Oui. 1. Énoncé de problème (de LeetCode)

> **Don** une grille 2-D «grid[m][n]» (1 ≤ m, n ≤ 50, 1 ≤ grille[i][j] ≤ 50)
> **Définir** pour chaque cellule (r, c):
> * `leftAbove[r][c]` – nombre de ** valeurs distinctes** sur la diagonale vers le haut gauche (à l'exclusion de la cellule elle-même).
> * `rightBelow[r][c]` – nombre de valeurs **distinctes** sur la diagonale à la droite (à l'exclusion de la cellule elle-même).
> **Retour** où
> `ans[r][c] ==" gaucheAu-dessus[r][c] – droiteAu-dessous[r][c]=".

Une diagonale est toute ligne qui commence à partir d'une cellule de la ligne supérieure ou de la colonne gauche et qui déplace une marche vers le bas jusqu'à ce que la grille se termine.

---

- Oui. 2. L'approche Good – Brute-Force (intuitive)

"Java
valeur(int[]]) {
int m = longueur de grille, n = longueur de grille[0];
int[]] ans = nouveau int[m][n];
pour (int i = 0; i < m; ++i) {
pour (int j = 0; j < n; ++j) {
Définir <integer> gauche = nouveau HashSet<>();
pour (int r = i-1, c = j-1; r >= 0 && c >= 0; --r, --c)
b) À gauche.add(grid[r][c]);

Définir <integer> droite = nouveau HashSet<>();
pour (int r = i+1, c = j+1; r < m && c < n; ++r, ++c)
l'alinéa a) est remplacé par le texte suivant:

ANS[i][j] = Math.abs(left.size() - right.size());
}
}
le retour des an;
}
«» "

* **Pros** – Facile à comprendre, utilise Javas `HashSet`.
* **Cons** – complexité temporelle "O(m*n*min(m,n)"", pire cas : 125 000 opérations par cellule (fin pour 50x50 mais lent dans les concours).
* ** Mémoire** – "O(min(m,n)" pour les deux ensembles temporaires.

---

- Oui. 3. Les mauvaises – Pourquoi la force brute fait-elle face à de véritables entrevues

* **Dépassement du délai**: Sur des entrées plus grandes ou dans des limites de compétition strictes, la solution "O(m*n*min(m,n)" peut atteindre 2 s timeout.
* ** Sets de recomptage** : Chaque cellule recalcule les mêmes diagonales à plusieurs reprises.
* ** Facteurs élevés constants** : l ' allocation de fonds par cellule est coûteuse.

> **Ligne de bottom** – vous impressionnerez votre recruteur si vous pouvez réduire l'algorithme à temps linéaire.

---

- Oui. 4. Les cas odieux – bord qui rompent le code naïf

Autres Décision Pourquoi ça casse
-- -- -- -- -- --
Cellule unique "[[1]]" Les diagonales sont vides; définit correctement la taille de retour 0. Autres
Grille rectangulaire La longueur diagonale diffère; doit garder les limites `r>=0 && c>=0` et `r<m && c<n`. Autres
Autres Les valeurs répétées le long d'une diagonale. Autres

Le code de force brute les gère tous, mais il est fragile si vous modifiez les boucles.

---

- Oui. 5. La solution optimisée – Temps linéaire avec Bit‐Masks

Comme chaque valeur de cellule est dans `[1, 50]`, nous pouvons stocker un masque 64 bits où le bit `k` (0-basé) indique que la valeur `k+1` est apparue.
Deux masques par cellule suffisent :

Symbole Signification Transition
- C'est quoi ?
"gaucheMask[i][j]"" Valeurs distinctes sur la diagonale supérieure gauche jusqu'à "(i,j)" ** À l'exclusion de** «gaucheMask[i][j] = gaucheMask[i-1][j-1]» Autres
"rightMask[i][j]"" Valeurs distinctes sur la diagonale inférieure droite commençant **après** "(i,j)" "rightMask[i][j] = rightMask[i+1][j+1]" (1L << (grid[i+1][j+1]-1)" Autres

La réponse pour une cellule est la différence absolue du pop-count des deux masques.

5.1 Mise en œuvre de Java

"Java
solution de classe {
valeur(int[]]) {
int m = longueur de grille, n = longueur de grille[0];
long[][]gaucheMask = nouveau long[m][n];
long[][] droiteMask = nouveau long[m][n];
int[]] ans = nouveau int[m][n];

// Construire gaucheMasque (en haut à gauche → en bas à droite)
pour (int i = 0; i < m; ++i) {
pour (int j = 0; j < n; ++j) {
Si (i > 0 & & j > 0) {
gaucheMask[i][j] = gaucheMask[i-1][j-1]
1L << (grid[i-1][j-1] - 1);
}
}
}

// Construire à droite Masque (en bas à droite → en haut à gauche)
pour (int i = m-1; i >= 0; --i) {
pour (int j = n-1; j >= 0; --j) {
si (i < m-1 && j < n-1) {
droiteMask[i][j] = droiteMask[i+1][j+1]
1L << (grid[i+1][j+1] - 1));
}
}
}

// Calculer la réponse
pour (int i = 0; i < m; ++i) {
pour (int j = 0; j < n; ++j) {
Int gauche Nombre = Long.bitCount(gaucheMask[i][j]);
Int droite Nombre = Long.bitCount(droiteMask[i][j]);
ans[i][j] = Math.abs(gaucheCount - droitCount);
}
}
le retour des an;
}
}
«» "

5.2 Mise en œuvre de Python

'`python
Solution de classe:
différence DeDistinctValues(même, grille: Liste[List[int]]) -> Liste[Liste[int]]:
m, n = len(grid), len(grid[0])
gauche_masque = [[0] * n pour _ dans l'intervalle(m)]
right_mask = [[0] * n pour _ dans l'intervalle(m)]

# gaucheMasque: en haut à gauche -> bas à droite
pour i dans la plage (m):
pour j dans la plage(n):
i > 0 et j > 0:
gauche_mask[i][j] = gauche_mask[i-1][j-1]

# droiteMasque: en bas à droite -> haut à gauche
pour i dans la plage (m-1, -1, -1):
pour j dans la plage (n-1, -1, -1):
i i < m-1 et j < n-1:
right_mask[i][j] = right_mask[i+1][j+1]=1 << (grid[i+1][j+1] -1)

ans = [[0] * n pour _ dans l ' intervalle(m)]
pour i dans la plage (m):
pour j dans la plage(n):
gauche_cnt = gauche_mask[i][j].bit_count()
right_cnt = right_mask[i][j].bit_count()
ans[i][j] = abs(left_cnt - right_cnt)
retour et
«» "

C++ Mise en œuvre

'`cpp
solution de classe {
public:
vector<vector<int>> differenceOfDistinctValues(vector<vector<int>>& grid) {
int m = quadrillage(), n = quadrillage[0].size();
vector<vector<unsigned long>> gaucheMasque(m, vector<unsigned long>(n, 0));
vector<vector<unsigned long>> droiteMasque(m, vector<unsigned long>(n, 0));
vector<vector<int>> ans(m, vector<int>(n, 0));

// gauche Masque: en haut à gauche en bas à droite
pour (int i = 0; i < m; ++i)
pour (int j = 0; j < n; ++j)
si (i et j)
gaucheMask[i][j] = gaucheMask[i-1][j-1]
(1ULL << (grid[i-1][j-1] - 1));

// droiteMasque: en bas à droite en haut à gauche
pour (int i = m-1; i >= 0; --i)
pour (int j = n-1; j >= 0; --j)
si (i < m-1 && j < n-1)
droiteMask[i][j] = droiteMask[i+1][j+1]
(1ULL << (grid[i+1][j+1] - 1));

// Réponse finale
pour (int i = 0; i < m; ++i)
pour (int j = 0; j < n; ++j) {
Int gauche Cnt = __constructin_popcountll(leftMask[i][j]);
Int droite Cnt = __constructin_popcountll(droiteMask[i][j]);
as[i][j] = abs(gaucheCnt - droiteCnt);
}
le retour des an;
}
};
«» "

---

- Oui. 6. Analyse de la complexité

L'approche du temps L'espace Pourquoi ça compte
-- -- -- -- -- -- -- -- -- -- -- -- --
Brute-Force (HashSet) **O(m × n × min(m,n))**
Optimisé (Bit-Mask) **O(m × n)**="O(m × n)" pour deux masques 64 bits="Linéaire, passe toutes les cases et concours de LeetCode="

* **Constant-Facteur Gain**
* Java: `Long.bitCount` est une seule instruction CPU.
* Python: `int.bit_count()` est également hautement optimisé en CPython 3.10+.
* C++: `_builtin_popcountll` est une seule instruction de machine.

Comme les valeurs de grille sont limitées à 50, un masque 64 bits est parfait.
Si la plage de valeurs était plus grande, vous revenez à `HashSet` ou utilisez une `HashMap<value, count>` pour chaque préfixe diagonal.

---

- Oui. 7. Conseils d'entrevue

1. ** Expliquez le problème dans vos propres mots** – Pour chaque cellule, nous regardons seulement la diagonale qui monte à gauche et celle qui descend à droite. (en milliers de dollars)
2. **Demander des questions claires** – par exemple, la longueur diagonale est-elle toujours la même? (en milliers de dollars)
3. **Afficher la force brute d'abord** – donne à l'intervieweur une base de référence.
4. **Introduire l'astuce du bit-mask** – Comme les valeurs sont ≤ 50, nous pouvons les traiter comme des bits. (en milliers de dollars)
5. **Discuss pop-count** – beaucoup d'intervieweurs vous aiment lorsque vous mentionnez `_builtin_popcountll` / `Long.bitCount`.
6. **Edge‐Case check** – soulignez comment votre code gère une grille monocellulaire ou des matrices non carrées.

---

- Oui. 8. Conclusion – Votre prochaine entrevue

LeetCode 2711 est plus qu'un simple problème diagonal – c'est une vitrine de:

* **Set theory** (éléments distincts en diagonale)
* ** Saveur de programmation dynamique** (masques préfixes)
* ** Optimisation du niveau du bit** (masques 64 bits)
* **Mise en œuvre de l'agnostique de la langue** (Java, Python, C++)

Baissez la version de la force brute pour impressionner, gardez la force brute dans vos notes pour le débogage rapide, et soyez toujours prêt à expliquer la solution de la force bit dans la salle d'entrevue. Bonne chance – vous êtes maintenant un pas vers l'atterrissage de ce rôle d'ingénierie de logiciel!