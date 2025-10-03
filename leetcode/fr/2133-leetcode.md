---
titre: LeetCode 2133. Vérifiez si chaque ligne et colonne contient tous les nombres -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

# Code de Leet 2133 – Vérifiez si chaque ligne et colonne contient tous les nombres
### Les bons, les mauvais et les méchants – Un développeur plein de piles
> *Des échantillons de code prêts à l'emploi (Java, Python, C++), une analyse de plongée profonde et un billet de blog qui vous fera remarquer par les recruteurs. *

---

Aperçu du problème

> ** Vérifier si chaque ligne et colonne contient tous les nombres* *
> **Difficulté:** Facile (Code Leet 2133)

> **Objectif**:
> Avec une matrice entière `n x n` ` matrix`, retourner `true` iff chaque ligne et chaque colonne contient **all** les entiers de `1` à `n` ** Exactement une fois**.

> **Constraints**
> * `1 ≤ n ≤ 100`
> * `1 ≤ matrice[i][j] ≤ n`

---

Solutions de code

> Voici des solutions propres et prêtes à la production dans **Java**, **Python 3** et **C++17**.
> Chaque extrait utilise la technique la plus courante et la plus efficace (HashSet/Bitset) et contient des commentaires pour plus de clarté.

---

### Java – HashSet (temps O(n2), espace O(n)

"Java
Importation de java.util.*;

solution de classe publique {
***
* Vérifie si chaque ligne et colonne de la matrice contient tous les nombres de 1 à n.
*
* Matrice @param La matrice n x n entier.
* @retour vrai si valide, faux sinon.
*/
contrôle public du booléenValide(int[][] matrice) {
int n = matrice. longueur;

pour (int r = 0; r < n; ++r) {
Définir <integer> ligne = nouveau HashSet<>();
Définir <integer> col = nouveau HashSet<>();

pour (int c = 0; c < n; ++c) {
si (!row.add[r][c])
// Dupliquer trouvé dans la ligne ou la colonne actuelle
retourner faux;
}
}
}
retour vrai;
}
}
«» "

> **Pourquoi HashSet? * *
> *Fast O(1) temps moyen d'insertion/de vérification. *
> *Pas besoin d'effacer l'ensemble après chaque ligne/colonne – un nouvel ensemble est créé par itération externe. *

---

### Python 3 – Régler / Bitset (temps O(n2), espace O(n))

'`python
de taper l'importation Liste

Solution de classe:
def checkValid(self, matrix: List[List[int]]) -> bool:
n = len(matrix)

# Mise en œuvre simple basée sur des ensembles
pour rangée, col en zip(matrice, zip(*matrice)):
si len(set(row)) != n ou len(set(col)) != n:
Retour Faux
retour Vrai
«» "

> **Alternative (octetarray/Bitset)** – encore plus rapide en pratique lorsque `n` ≤ 100.

'`python
Solution de classe:
def checkValid(self, matrix: List[List[int]]) -> bool:
n = len(matrix)
pour r dans la plage(n):
row_used = bytearray(n + 1) # indices 1..n
col_used = bytearray(n + 1)
pour c dans la plage(n):
val_r, val_c = matrice[r][c], matrice[c][r]
si row_used[val_r] ou col_used[val_c]:
Retour Faux
ligne_utilisée[val_r] = 1
= 1
retour Vrai
«» "

---

### C++17 – `std::unordered_set` (temps O(n2), espace O(n))

'`cpp
#incluez <vecteur>
#inclut <unordered_set>

solution de classe {
public:
Vérification du boolValide(std::vector<std::vector<int>& matrice) {
int n = matrice.size();

pour (int r = 0; r < n; ++r) {
std::unordered_set<int> ligne, col;
pour (int c = 0; c < n; ++c) {
si (!row.insert(matrix[r][c]).second="!col.insert(matrix[c][r]).second=") {
retourner false; // duplicata en ligne ou en colonne
}
}
}
retour vrai;
}
};
«» "

> **Pourquoi `unordered_set`?**
> *Moyenne O(1) insérer/vérifier; frais généraux négligeables pour "n ≤ 100". *

---

Analyse de complexité

L'approche Temps Espace
- C'est quoi ?
Brute-force (boucles nestées, en vérifiant chaque fois toute la ligne/col)
HashSet/Bitset (recommandé)
2-D matrice booléenne (explicite «row[i][num]», «col[j][num]»)

> **Pourquoi la solution HashSet gagne**
> *Runs dans le même temps asymptotique que la meilleure solution possible*
> *Utilise seulement la mémoire supplémentaire linéaire (= 200 `int`s pour `n = 100`) *
> * Facile à lire, à maintenir et à traduire entre les langues. *

---

Le bon, le mauvais et le mauvais

Aspect du bien
- C'est quoi ?
**Simplicité L'approche fondée sur les ensembles est concise et autodocumentée. La suringénierie (p. ex., matrice booléenne `O(n2)`) ajoute du bruit. Les boucles imbriquées avec index manuel jonglant et des vérifications manuelles en double sont sujettes à erreur. Autres
La force brute de `O(n3)` devient impossible pour `n = 100`. Autres
**L'espace**=Les jeux `O(n)`, nettoyés automatiquement chaque ligne/colonne.==Les tableaux `O(n2)` pour la duplication `row`/`col`. Potentiel de fuite de mémoire si les ensembles ne sont pas nettoyés ou réutilisés correctement. Autres
**Readability** Hypothèses implicites (par exemple, que l'entrée est toujours valide). Le mélange de trucs bitwise (`BitSet`, `byterarray`) avec une logique complexe peut confondre les évaluateurs. Autres

> **À emporter**:
> Dans un cadre d'entrevue, choisissez la solution **HashSet / Bitset** – elle est rapide, claire et démontre une solide connaissance de la structure des données.

---

Pourquoi ce blog vous aide à trouver un emploi

1. **En-têtes optimisés par référence au référencement** – LeetCode 2133.
2. **Mot-clé-Rich Content** – Termes tels que *=unicité de la ligne* *= unicité de la colonne* *=Hashset* *=bitset* *= complexité du temps* *= complexité de l'espace* *=interview d'emploi* sont aspergés naturellement.
3. **Exemples de codes clairs** – Les recruteurs peuvent instantanément copier et exécuter les extraits pour vérifier votre compréhension.
4. **Problem‐Solving Mindset** – La section « Good, Bad, Ugly » vous montre non seulement comment résoudre, mais comment critiquer des solutions – une compétence d'entrevue très appréciée.

---

## Comment utiliser ces solutions dans votre portefeuille

1. **Répertoire GitHub** – Communiquez chaque fichier de solution (`SolutionJava.java`, `solution.py`, `solution.cpp`) avec un README qui fait référence à ce blog.
2. **Blog Post** – Publier sur Medium/Dev.to, y compris une démo en ligne (p. ex. en utilisant **repl.it** ou **Gist**).
3. **LienD'article** – Poster le blog avec une brève description: LeetCode 2133 en Java, Python, C++ – Analyse du temps et de l'espace – Prêt à l'entrevue! #LeetCode #CodingInterview Java Python Cpp.
4. **Resumer Bullet** – Mise en œuvre d'un validateur O(n2) pour les matrices n×n (LeetCode 2133) en utilisant des structures de données langage-agnostiques, réduisant l'empreinte mémoire à O(n). (en milliers de dollars)

---

Liste de contrôle avant votre prochaine entrevue de codage

- Lire les contraintes du problème *avant* écrire le code.
- Choisir le modèle **HashSet / Bitset**.
- Écrire propre, le code commenté.
- Expliquez la complexité temps/espace à la volée.
- Critique une solution de rechange (force-brute) – pratiquez l'analyse de bonne, mauvaise, ugly.

---

La pensée finale

LeetCode 2133 peut être étiqueté "Easy", mais la maîtrise de son modèle d'unicité **row/colonne** démontre une compréhension fondamentale des recherches basées sur le hash et de l'optimisation algorithmique.

> **Show it off, blog it, share it** – votre prochain recruteur vous remerciera pour la clarté et la profondeur.

Bonne chance, et le codage heureux! C'est ce qu'il a dit.

---