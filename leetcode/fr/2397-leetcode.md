---
titre: LeetCode 2397. Lignes maximales couvertes par des colonnes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2397. Lignes maximales couvertes par les colonnes – Code 3-Way, blog et référence de l'emploi

> **TL;DR**
> *Problème:* Choisissez exactement les colonnes `numSelect` d'une matrice binaire `m × n` pour couvrir le nombre maximum de lignes (une ligne est *couverte* si chaque ligne `1` dans cette ligne se trouve dans une colonne choisie).
> *Connaissance clé:* Les contraintes sont minuscules (`n ≤ 12`), donc une solution **bitmask + backtracking** est à la fois simple et rapide.
> *Complexité:* `O( (n choisissez numSelect) · m · n )` temps, `O(1)` espace supplémentaire.

Ci-dessous vous trouverez:

1. A **SEO-optimized blog** expliquant le problème, les pièges, et l'algorithme en anglais clair.
2. Trois implémentations de travail – **Java**, **Python** et **C++** – que vous pouvez copier-coller dans LeetCode.
3. Un rapide de quoi parler dans une section d'interview.

---

## Le problème (Code 2397)

Texte
Entrée: matrice: List[List[int]], numSelect: int
Sortie: int // nombre max de lignes qui peuvent être couvertes
«» "

- `matrix` est `m × n`, `0 ≤ m,n ≤ 12`, les entrées sont `0` ou `1`.
- Vous devez choisir **exactement** `numSelect` colonnes distinctes.
- Une ligne est *couverte* si **chaque** `1` dans cette ligne se trouve dans une colonne choisie (ou la ligne n'a pas `1`s).

> Exemple
> matrice = [[0,00],[1,0,1],[0,1],[0,0,1]], numSelect = 2 → **3**

---

- Oui. Pourquoi Brute Force fonctionne (mais est toujours une mauvaise idée)

Avec `n ≤ 12`, le nombre total de sous-ensembles de colonnes est `2^n ≤ 4096`.
Vous pouvez énumérer tous les sous-ensembles et choisir ceux de la taille `numSelect`.
C'est très bien **temps-wise**, mais le code devient bruyant, et il est difficile à expliquer dans une entrevue.

Toutefois, l'approche **backtrawing** reflète naturellement l'arbre de décision :
*Cochez la colonne courante?* – *ou sautez-la?* – et prunez quand vous avez déjà choisi les colonnes `numSelect`.
Cela donne un code propre et récursif qui est facile à lire, à tester et à étendre.

---

- Oui. Idée de base – Bitmask + Backtracking

1. **Représenter un ensemble de colonnes sélectionnées sous la forme d'un bitmask** (un `int` où bit `j` = 1 φ colonne `j` sélectionnée).
2. **DSE récursif**:
* `idx` – indice de la colonne actuelle (0 ... n-1).
* `cnt` – nombre de colonnes déjà choisies.
* `masque` – masque de colonnes choisies.
3. **Cas de base**: quand `cnt= numSelect` → compter les lignes couvertes.
4. **Direction générale** :
* * *Pick* colonne `idx` → définir son bit, revenir avec `cnt+1`.
* *Skip* colonne `idx` → laisser bit 0, revenir avec le même `cnt`.
5. **Ébauche** : si les colonnes restantes sont inférieures aux colonnes encore nécessaires, arrêtez-vous tôt.

Compter des lignes couvertes pour un `masque` donné est `O(m · n)` – assez petit pour nos contraintes.

---

Complexité

Opération Temps Espace
- C'est quoi ?
Autres Enumeration de tous les sous-ensembles de la taille `k`. Autres
Autres Nombre de lignes pour un masque Autres
Profondeur de récursion (hors pile d'appel)

Parce que `(12 choisissez 6) = 924` au pire, l'algorithme fonctionne en bien moins d'un milliseconde sur LeetCode.

---

- Oui. 1. Java (LeetCode Style)

"Java
solution de classe {
Int m, n, cible;
tapis privé;

public int maxRows(int[][] matrice, int numSelect) {
ce.mat = matrice;
ce.m = matrice.longueur;
cette.n = matrice[0].longueur;
Ça. cible = nombre Sélectionner;
retour dfs(0, 0, 0);
}

Int dfs (int idx, int cnt, masque int) {
si (cnt == cible) // nous avons choisi suffisamment de colonnes
retour countCovered(masque);

si (idx == n) // plus de colonnes à considérer
retour 0;

int restant = n - idx;
si (rester + cnt < cible) // impossible d'atteindre la cible
retour 0;

// Option 1: choisissez cette colonne
cueillir int = dfs(idx + 1, cnt + 1, masque) (1 < < idx));

// Option 2: sauter cette colonne
int skip = dfs(idx + 1, cnt, masque);

retourner Math.max(pick, skip);
}

Nombre d'entrées privées Couvert(masque) {
Int couvert = 0;
pour (int i = 0; i < m; i++) {
booléen ok = vrai;
pour (int j = 0; j < n; j++) {
Si (mat[i][j] == 1 && (masque & (1 << j)) == 0) {
ok = faux;
pause;
}
}
si (ok) couvert++;
}
le retour couvert;
}
}
«» "

---

- Oui. 2. Python (3.8+)

'`python
Solution de classe:
def maximum Lignes(self, natte: List[List[int]], numSelect: int) -> Int:
automat = mat
self.m = len(mat)
auto.n = len(mat[0])
soi-même. cible = nombre Sélectionner
retourner self._dfs(0, 0, 0)

def _dfs(self, idx: int, cnt: int, masque: int) -> Int:
Si cnt est lui-même. cible:
retourner self._count(masque)

Si idx == auto.n:
retour 0

reste = auto.n - idx
si restant + cnt < soi-même. cible:
retour 0

Choisir
sélection = auto._dfs(idx + 1, cnt + 1, masque)
♪ Sauter
skip = self._dfs(idx + 1, cnt, masque)
retour max(pick, skip)

def _count(self, masque: int) -> Int:
couvert = 0
pour la rangée en soi. Tapis:
ok = Vrai
pour j, val en énumération(ligne):
si valeur et non (masque et (1 < < j)):
ok = Faux
pause
si oui:
couvert += 1
retour couvert
«» "

---

- Oui. 3. C++ (GNU C++17)

'`cpp
solution de classe {
public:
Int maximum Lignes(vecteur<vecteur<int>>& matrice, int numSelect) {
m = matrice.size();
n = matrice[0].size();
mat = matrice;
cible = nombre Sélectionner;
retour dfs(0, 0, 0);
}

particulier:
vecteur<vecteur<int>> natte;
int m, n, cible;

int dfs(int idx, int cnt, masque int) {
si (cnt == cible) // déjà sélectionné suffisamment de colonnes
retour countCovered(masque);
si (idx == n) retourner 0; // épuisé des colonnes

int restant = n - idx;
si (le maintien + cnt < cible) // ne peut pas atteindre la cible
retour 0;

// Choisir la colonne actuelle
cueillir int = dfs(idx + 1, cnt + 1, masque) (1 < < idx));

// Sauter la colonne actuelle
int skip = dfs(idx + 1, cnt, masque);

retour max(pick, skip);
}

nombre d'int Couvert(masque) {
Int couvert = 0;
pour (int i = 0; i < m; ++i) {
bool ok = true;
pour (int j = 0; j < n; ++j) {
si (mat[i][j]] 1 && !(masque & (1 << j)) {
ok = faux;
pause;
}
}
si (ok) couvert++;
}
le retour couvert;
}
};
«» "

---

- Oui. Comment parler dans une interview

1. **Énoncer les contraintes** (`n ≤ 12`) → permet des algorithmes exponentiels.
2. **Expliquez la représentation bitmask** – cela montre instantanément que vous pouvez coder des ensembles de colonnes dans l'espace `O(1)`.
3. **Afficher l'arborescence de récursion DFS** – Pick ou skip – et pourquoi la taille est sûre.
4. **Complexité** – soulignez que l'algorithme est *optimal pour les contraintes données*.
5. **Mention alternatives** – une simple boucle sur les combinaisons ou une solution `next_permutation` – juste pour vous montrer les compromis.
6. **Pourquoi c'est un bon problème d'interview** – teste la récursion, la manipulation des bits et le comptage soigneux.

---

## SEO Mots clés (pour les pages de recherche d'emploi)

- LeetCode 2397
- Lignes maximales Couvert par des colonnes
- Algorithme de retour
- Solution Bitmask
- Solution Java 17 LeetCode
- Solution Python 3 LeetCode
- C++ Solution LeetCode
- Questions d'entrevue de l'ingénieur logiciel
- Préparation de l'entretien avec l'algorithme
- Entretien sur la structure des données

Inclure ces balises sur votre lien Dans post ou blog personnel pour attirer les recruteurs à la recherche de candidats qui peuvent résoudre les problèmes LeetCode efficacement.

---

Mot final

- L'approche **backtracking + bitmask** vous donne un code propre et durable qui est facile à expliquer.
- Oui. La complexité du temps est bien dans les limites du problème – vous finirez en millisecondes.
- Mettez en avant l'algorithme dans votre prochaine interview : Nous traitons les colonnes comme des bits, marchons l'arbre de décision, et ne comptons les rangées couvertes qu'une fois par feuille. (en milliers de dollars)

Bonne chance avec l'entrevue, et le codage heureux!