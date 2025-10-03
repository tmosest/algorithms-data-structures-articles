---
titre: LeetCode 2536. Sous-matrices d'accroissement par un -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 2536 – **Sous-matrices d'encre par Un**
Les bons, les mauvais et les méchants

> **Mots clés**: LeetCode 2536, Increment Submatrices by One, 2-D prefix sum, different array, range addition, coding interview, algorithme analysis, job interview

---

- Oui. 1. Récapitulation des problèmes

Vous recevez une matrice `n × n` zéro-initialisée `mat`.
Vous recevez un tableau de requêtes `queries[i] = [row1i, col1i, row2i, col2i]`.
Pour chaque requête, vous devez ajouter **1** à chaque élément du sous-matrice défini par les quatre indices.
Retourne la matrice finale après avoir appliqué toutes les requêtes.

> **Constraints**
> * `1 ≤ n ≤ 500`
> * `1 ≤ requêtes.longueur ≤ 104 "
> * `0 ≤ rang1i ≤ rang2i < n`
> * `0 ≤ col1i ≤ col2i < n`

---

- Oui. 2. Pourquoi le Brute-Force fait défaut (les mauvais)

Une implémentation simple itère sur chaque cellule touchée par une requête :

"Java
pour (int[] q : requêtes) {
pour (int r = q[0]; r <= q[2]; r++)
pour (int c = q[1]; c <= q[3]; c++)
[c]++;
}
«» "

* **Complexité temporelle** – O(`q * n2`) dans le pire des cas (chaque requête couvre toute la matrice).
Avec `q = 104` et `n = 500`, cela signifie 2,5 × 109 opérations → TLE.
* **Space** – O(1) supplémentaire, mais le temps d'exécution lourd domine.

Nous avons donc besoin d'un "ajout de gamme".

---

- Oui. 3. La différence à deux dimensions

L'astuce 1-D pour les mises à jour de la plage est de marquer le début et l'élément après la fin, puis prendre une somme de préfixe une fois à la fin.
En 2-D, nous faisons la même chose avec quatre mises à jour de "corner" :

Opération Effet
C'est quoi ?
Diff[r1] [c1] += 1 ' , début du rectangle
`diff[r1][c2+1] -= 1'= Limite de droite Autres
Diff[r2+1] [c1] -= Limite de l'extrémité du fond Autres
Diff[r2+1][c2+1] += contre-équilibre

Après le traitement de toutes les requêtes, nous effectuons une somme **préfixe sur les lignes** puis sur **colonnes** (ou vice-versa).
La matrice résultante est exactement la matrice après tous les incréments.

Complexité

* **Heure** – 'O(n2 + q) "
* Chaque requête est traitée en O(1).
* Deux boucles imbriquées sur la matrice pour les montants préfixes : opérations `n2`.
* **Espace** – `O(n2)` (le tableau de différence, peut réutiliser le tableau de résultat).

Avec `n ≤ 500`, `n2 = 250 000`, facilement sous les limites.

---

- Oui. 4. Edge Cases & Gotchas

Qu'est-ce qu'il faut surveiller ?
C'est ce que j'ai dit.
Autres Interrogez-vous sur le bord droit/dernier de l'appareil. Utilisez un tableau ou un garde `(n+1) × (n+1)` avec des vérifications `si`. Autres
Indices négatifs (aucun dans ce problème) Autres
Grand `n`, mais petit `q`. Toujours O(`n2`) pour les sommes de préfixe - inévitable parce que la sortie elle-même est `n2`. Autres
Limites de mémoire: 500 × 500 entiers: 1 Mo – sans danger sur la plupart des plateformes. Autres

---

- Oui. 5. Optimisations alternatives (les Ugly)

Quand ça aide
C'est pas vrai.
**Row-level diff** – stockez une liste de "updates" par ligne, accumulez un diff 1-D pour cette ligne. Autres
**Lazy prefix** – build prefix sums incrémentally while apply requests. Autres
**Représentation par satellite** – utiliser des cartes de hachage pour des mises à jour très rares. Autres

Ces variantes trade code complexité pour les gains de vitesse marginaux et sont rarement nécessaires pour les limites de LeetCode.

---

- Oui. 6. Mise en œuvre des références

Voici des solutions propres et prêtes à la production dans **Java, Python et C++**.
Tous utilisent le "(n+1) × (n+1)` difference array trick et deux passes de sommes préfixes.

---

#### Java (style LeetCode)

"Java
***
* LeetCode 2536: Sous-matrices d'augmentation par une
*/
solution de classe publique {
public int[][] rangeAddQueries(int n, int[][] requêtes) {
// diff a une ligne/col supplémentaire pour éviter les contrôles aux frontières
int[][] diff = nouvelle int[n + 1][n + 1];

pour (int[] q : requêtes) {
int r1 = q[0], c1 = q[1];
int r2 = q[2], c2 = q[3];
diff[r1][c1] += 1;
Diff[r1][c2 + 1] -= 1;
diff[r2 + 1][c1] -= 1;
diff[r2 + 1][c2 + 1] += 1;
}

// Préfixer la somme sur les lignes
pour (int r = 0; r < n; r++) {
pour (int c = 1; c < n; c++) {
diff[r][c] += diff[r][c - 1];
}
}

// Préfixer la somme sur les colonnes
pour (int r = 1; r < n; r++) {
pour (int c = 0; c < n; c++) {
diff[r][c] += diff[r - 1][c];
}
}

// Couper la ligne/col supplémentaire et retourner
int[][] res = nouvelle int[n][n];
pour (int r = 0; r < n; r++) {
Système.arraycopy(diff[r], 0, res[r], 0, n);
}
retour rés;
}
}
«» "

---

Python 3

'`python
"""
LeetCode 2536: Sous-matrices d'augmentation par une
"""
Solution de classe:
gamme AddQueries(self, n: int, requêtes: List[List[int]]) -> Liste[Liste[int]]:
# +1 pour effectuer des mises à jour de coin en toute sécurité
diff = [[0] * (n + 1) pour _ dans la plage (n + 1)]

pour r1, c1, r2, c2 dans les requêtes:
diff[r1][c1] += 1
diff[r1][c2 + 1] -= 1
diff[r2 + 1][c1] -= 1
Diff[r2 + 1][c2 + 1] += 1

Préfixe sur les lignes
pour r dans la plage(n):
pour c dans la plage(1, n):
diff[r][c] += diff[r][c - 1]

Préfixe sur les colonnes
pour r dans la plage (1, n):
pour c dans la plage(n):
diff[r][c] += diff[r - 1][c]

Retourne la matrice parée
retourner [row[:n] pour ligne dans diff[:n]]
«» "

---

#### C++ (GNU C++17)

'`cpp
***
* LeetCode 2536: Sous-matrices d'augmentation par une
*/
solution de classe {
public:
vecteur<vecteur<int>> rangeAddQueries(int n, vector<vector<int>>& requêtes) {
// diff a une ligne/col supplémentaire pour la sécurité
vector<vector<int>> diff(n + 1, vector<int>(n + 1, 0));

pour (const auto& q : requêtes) {
int r1 = q[0], c1 = q[1];
int r2 = q[2], c2 = q[3];
diff[r1][c1] += 1;
Diff[r1][c2 + 1] -= 1;
diff[r2 + 1][c1] -= 1;
diff[r2 + 1][c2 + 1] += 1;
}

// Préfixer la somme sur les lignes
pour (int r = 0; r < n; ++r)
pour (int c = 1; c < n; ++c)
diff[r][c] += diff[r][c - 1];

// Préfixer la somme sur les colonnes
pour (int r = 1; r < n; ++r)
pour (int c = 0; c < n; ++c)
diff[r][c] += diff[r - 1][c];

// Couper la matrice en n x n
vector<vector<int>> res(n, vector<int>(n));
pour (int r = 0; r < n; ++r)
pour (int c = 0; c < n; ++c)
res[r][c] = diff[r][c];

retour rés;
}
};
«» "

---

- Oui. 7. Essais et validation

Autres Essai prévu
C'est pas vrai.
"n = 1", une requête "[0,00,0]" Autres
"n = 3", requêtes couvrant les sous-matrices disjointes
`n = 500`, chaque requête couvre la matrice entière.
Des questions touchant la frontière.

Exécutez les implémentations fournies contre ces cas – ils passent tous instantanément sur le harnais de test LeetCode.

---

- Oui. 8. Ce que les intervieweurs recherchent

1. **Comprendre les sommes préfixes 2-D** – montre que vous pouvez généraliser l'astuce de mise à jour 1-D.
2. **Manipulation d'Edge** – traiter correctement les limites `+1` est une source commune de bogues.
3. **L'analyse de complexité** – être capable d'expliquer "O(n2 + q)" est crucial.
4. **Clean code** – des commentaires lisibles et des noms de variables appropriés aident l'évaluateur à lire rapidement votre solution.

Si vous visez une interview d'ingénierie logicielle, expliquez le concept de tableau de différences* et peut-être même dessinez l'algorithme sur un tableau blanc. Cela démontre une pensée claire et de solides fondamentaux algorithmiques.

---

- Oui. 9. FAQ

Question Réponse
C'est pas vrai.
Autres **Puis-je utiliser un tableau de diff 1-D seulement? Non – un seul tableau 1-D ne peut capter deux dimensions indépendantes d'un rectangle. Autres
Autres **Et si la valeur à ajouter n'est pas 1?**=2 Même idée, il suffit d'ajouter la valeur au lieu de `1`. Autres
**Peut-on utiliser `int64` pour éviter les débordements? Pour les problèmes généralisés, vous pouvez passer à "long". Autres
Autres **Y a-t-il un meilleur algorithme que l'algorithme d'O(n2)? Si vous pouviez sauter la sortie de la matrice, une ligne de balayage ou une diff clairsemée pourrait aider. Autres

---

10 ans. Prise finale Loin

> *Increment Submatrices by One* est un exemple de la façon dont un simple tableau de différence 2-D transforme un runtime autrement impossible en une solution élégante `O(n2 + q)`.
> Maîtrisez ce modèle, et vous serez prêt à répondre à de nombreuses questions d'entrevues de type « Range-update » qui apparaissent dans les cycles de conception de systèmes et de structure de données.

Bonne chance, et que vos intervieweurs aiment votre propre code Java/Python/C++!