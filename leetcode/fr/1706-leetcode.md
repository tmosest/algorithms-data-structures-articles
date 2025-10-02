---
titre: LeetCode 1706. Où la balle tombera -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# LeetCode 1706 – Où tombera la balle ? (en milliers de dollars)
## Un guide complet, optimisé par le SEO (Java / Python / C++)
> **Vous voulez passer votre prochaine entrevue de codage? * *
> Lisez comment résoudre LeetCode 1706, comprendre les pièges et apprendre à en parler en format d'entrevue *STAR*.

---

- Oui. 1. Récapitulation des problèmes (mots clés du SEO : *LeetCode 1706*, * simulation de ballon*, *problème de grille*)

On vous donne un tableau `m x n` 2-D `grid`.
Chaque cellule contient soit `1` (en diagonale) ou `1` (en diagonale).

Une balle est tombée en haut de chaque colonne.
En se déplaçant vers le bas:

* Si une balle rencontre une paire en forme de V** (`1` à côté de `-1`), elle est coincée.
* Si une balle frappe un mur (bord gauche ou droit) en raison de la direction de la planche, elle est également coincée.

Retourner un tableau `réponse` de taille `n` où `réponse[i]` est la colonne où la balle tombe en bas, ou `-1` si elle est coincée.

---

- Oui. 2. Intuition et observation clé

> **Observation** – *Une boule ne peut se déplacer que de la colonne `c` vers la colonne `c+grid[row][c]` si la planche à la colonne suivante pointe dans la même direction. *

En anglais clair:
Si une cellule à `(row, c)` est `1`, la balle essaiera de se déplacer à droite vers la colonne `c+1`.
Mais la balle se déplace réellement **seulement si la cellule `(row, c+1)` est également "1"**.
La même règle s'applique pour `-1` (à gauche).

Cette règle simple nous permet de simuler le chemin de chaque boule en **O(m)** temps, où `m` est le nombre de lignes.

---

- Oui. 3. Simulation itérative de la DSV de Brute-Force

Démarche
C'est quoi ?
DFS (récursifs) : Récursion intuitive et naturelle : risque de débordement de la pile pour les grands réseaux (m ≤ 100 → fin, mais mauvais style) :
Simulation itérative : O(1) espace par boule, pas de récursion.

**Nous utiliserons la simulation itérative** car elle est plus rapide, plus sûre et plus facile à expliquer dans une entrevue.

---

- Oui. 4. La solution – étape par étape

1. **Tableau de résultats** – `int[] response = new int[n];`.
2. **Loop sur chaque colonne de départ** `startCol`.
3. **Simulez la balle**:
* `col = début Col.
* Pour chaque `ligne` de `0` à `m-1`:
* `col suivant = col + grille[ligne][col]` (la direction du tableau actuel)
* **Contrôle budgétaire**: si `nextCol` est à l'extérieur `[0, n-1]`, la balle est coincée → `réponse[startCol] = -1`.
* **V – vérification de la forme**: si `grid[row][nextCol] != grille[row][col]`, la balle est coincée → `réponse[startCol] = -1`.
* Sinon, définir `col = nextCol` et continuer à la ligne suivante.
4. Si la boucle se termine, la balle est sortie → `réponse[startCol] = col`.

---

- Oui. 5. Mise en œuvre du code

#### 5.1 Java

"Java
***
* LeetCode 1706 – Où tombera la balle
*
* Simulation itérative – temps O(m * n), espace supplémentaire O(1).
*/
solution de classe {
public int[] findBall(int[][]) {
int m = longueur de la grille; // nombre de lignes
int n = grille[0].longueur; // nombre de colonnes
résultat int[] = nouveau résultat int[n];

pour (int start = 0; start < n; start++) {
int col = début; // colonne courante de la boule

pour (int rang = 0; rang < m; rang++) {
int suivant Col = col + grille[ligne][col]; // colonne cible

// Si nous sortons des limites
if (col suivant < 0) nextCol >= n) {
col = -1;
pause;
}

// C'est coincé si on frappe un V
si (grid[row][nextCol] != grille[row][col] {
col = -1;
pause;
}

col = suivant Col; // déplacer la balle vers la colonne suivante
}

résultat[start] = col; // dernière colonne (ou -1 si bloqué)
}
le résultat du retour;
}
}
«» "

5.2 Python

'`python
Solution de classe:
"""
LeetCode 1706 – Où tombera la balle
Heure: O(m * n)
Espace: O(1) par boule (le tableau de résultats est O(n))
"""

def findBall(self, grid: List[List[int]]) -> Liste[int]:
m, n = len(grid), len(grid[0])
res = []

pour commencer dans la plage(n):
col = début
pour la ligne de range(m):
next_col = col + grid[row][col]
# Hors limites
si next_col < 0 ou next_col >= n:
col = -1
pause
# Détection de la forme V
if grid[row][next_col] != grid[row][col]:
col = -1
pause
col = suivant_col
res.append(col)
retour res
«» "

C++

'`cpp
***
* LeetCode 1706 – Où tombera la balle
*
* Heure: O(m * n)
* Espace: O(1) espace supplémentaire
*/
solution de classe {
public:
vecteur<int> findBall(vecteur<vecteur<int>>& grille) {
int m = quadrillage.size();
int n = grille[0].taille();
vecteur<int> réponse(n);

pour (int start = 0; start < n; ++start) {
int col = début; // colonne courante de la boule

pour (int rang = 0; rang < m; ++row) {
int suivant Col = col + grille[ligne][col];

// La balle est coincée au mur
if (col suivant < 0) nextCol >= n) {
col = -1;
pause;
}

// La balle est coincée en forme de V
si (grid[row][nextCol] != grille[row][col] {
col = -1;
pause;
}

col = suivant Col; // avance vers la colonne suivante
}

réponse[démarrage] = col; // dernière colonne ou -1
}

réponse de retour;
}
};
«» "

---

- Oui. 6. Analyse de la complexité

**Exploitation**
- C'est quoi ?
Autres Simulation d'une boule Autres
Toutes les boules `n` pour le tableau de sortie

Compte tenu des contraintes ('1 ≤ m, n ≤ 100'), cette solution fonctionne en millisecondes et est bien dans les limites.

---

- Oui. 7. Cas de bord à discuter dans les entrevues

1. **Une seule ligne / une seule colonne** – s'assure que la balle sort toujours ou se coince immédiatement.
2. **Toutes les grilles `1` ou `1`** – la balle se déplace tout droit à droite ou à gauche jusqu'au mur.
3. ** Modèle alternatif `1,-1,1,-1...'** – chaque balle est coincée à cause des formes V.
4. **Grands segments consécutifs `1` ou `-1`** – la balle peut déplacer de nombreuses colonnes d'une rangée; le contrôle de la cellule suivante garantit la justesse.

Montrez le cas de test dans l'article pour renforcer que le code les gère tous.

---

- Oui. 8. Bien / mal / Ugly – Entretien – Discussion amicale

Catégorie
C'est ce qu'on dit.
**Bien** La simulation est un liner unique dans chaque langue. <br>• **Aucune récursion** – Évite le débordement de la pile. <br>• ** Mémoire prévisible** – O(1) par balle, facile à expliquer. Autres
**Certains essaient de simuler chaque cellule pour chaque balle, ce qui conduit à "O(m*n^2)" (probablement avec `m,n=100`, mais toujours un mauvais modèle). Autres
**Ugly**) • ** DFS récursion** – Fonctionne mais se sent . <br>• **Over‐optimization** – Essayer d'utiliser des astuces bit‐mask ou des mathématiques fantaisistes peut rendre la solution illisible. Autres

> **Conseil d'entrevue** – Si un candidat propose une solution DFS, demandez-leur d'expliquer l'utilisation de la pile et pourquoi une approche itérative est préférable.

---

- Oui. 8. Parlons du problème dans une entrevue (format STAR)

**Situation******Tâche******
- C'est quoi ?
Autres Nous avions une grille de diagonales `m x n`. J'ai simulé la balle pour chaque colonne, en vérifiant les liaisons extérieures et les formes V – un algorithme `O(m*n)'. Autres

Soyez prêt à répondre aux questions suivantes :

* *Pourquoi cochez-vous `grid[row][nextCol] != grid[row][col]`?* – Parce qu'une balle ne bouge que si la prochaine planche pointe dans la même direction; autrement, on frappe une forme V.
* *Et si nous avions 105 lignes?* – Discutez en utilisant la simulation O(m)** amortie par balle et comment vous avez précalculé des colonnes accessibles avec DP ou mémorisation.
* * Pouvons-nous faire mieux que O(m*n)?* – Non, chaque bille doit examiner chaque ligne au moins une fois ; vous ne pouvez enregistrer que le tableau de sortie `O(n)`.

---

- Oui. 9. Liste de contrôle de la préparation de l'entrevue

1. **Lisez attentivement le problème** – faites attention aux conditions de l'arrêt.
2. **Exposer l'observation principale** – la direction du tableau doit correspondre à la cellule suivante.
3. **Afficher la simulation itérative** – écrire un pseudo-code sur le tableau blanc.
4. **Ecrire le code dans une langue** (Java, Python, ou C++) – le rendre propre, commenté et testé.
5. **Analyser la complexité** – temps « O(m*n) », espace « O(n) ».
6. **Talk à travers les boîtiers de bord** – murs, formes en V, grilles monolignes.
7. **Suivi des réponses** – sécurité de la cheminée, approches alternatives.

---

- Oui. 10. Comment ce problème vous aide à trouver un emploi

* **Compétences de la structure des données** – Vous démontrez la manipulation du tableau et l'indexation bidimensionnelle.
* ** Pensée algorithmique** – Vous présentez l'observation → simulation → implémentation.
* **Codage Style** – Propre, le code itératif est la marque d'un ingénieur senior.
* **Entrevue Conversation** – Vous pouvez utiliser ce problème comme un point de discussion pour *System Design* (visualisation de la grille) et *Data Structures* (gestion de tableaux 2-D).

> ** Conseil professionnel :** Quand votre intervieweur dit *=Pouvez-vous résoudre ce problème récursivement?==*, commencez par DFS, puis pivotez gracieusement vers la méthode itérative, expliquant pourquoi celle-ci est supérieure.

---

## 11. Conclusion – Les derniers départs

* **LeetCode 1706** est un problème classique de simulation *grid-ball* qui teste votre capacité à raisonner sur la direction, les limites et les conditions d'échec.
* La simulation interactive** est la solution la plus robuste, la plus efficace et la plus conviviale pour les interviews.
* En comprenant les aspects *good* (simplicité), *bad* (troubles de récursion) et *ugly* (suringénierie), vous serez en mesure d'expliquer le problème avec confiance lors de votre prochaine entrevue de codage.

---

- Oui. Bonus : Cheat de référence rapide Feuille

Langue Heure Espace Code Extrait
- C'est quoi ?
"O(m*n)" "O(n)" "Details" Afficher le code</résumé>Block de code de Java ci-dessus</details> Autres
Python "O(m*n)" "O(n)" "Détails" Afficher le code</résumé> Bloc de code Python ci-dessus</details> Autres
* C++ * O(m*n) * O(n) * <details> <sommary> Afficher le code</résumé>C++ bloc de code ci-dessus</détails> Autres

---

Mot final

Maîtrise **LeetCode 1706 Où Will the Ball Fall** vous montre :

* Traduire une description physique réelle en code propre et efficace.
* Choisissez la bonne stratégie algorithmique (simulation sur DFS).
* Communiquer la complexité et les cas de pointe aux intervieweurs.

Allez vous entraîner ! Ajoutez ce problème à votre liste de vérification de préparation de l'entrevue, et vous irez dans votre prochaine entrevue technique avec confiance.

Bon codage ! C'est ce qu'il a dit