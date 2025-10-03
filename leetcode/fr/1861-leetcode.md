---
titre: LeetCode 1861. Rotation de la boîte -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Java, Python et C++ Solutions pour **LeetCode 1861 – Rotation de la boîte**

Ci-dessous vous trouverez des implémentations propres et prêtes à la production pour les trois langues d'entrevue les plus populaires.
Toutes les solutions suivent la même idée :

1. ** Appliquer la gravité** – pour chaque rangée, glisser chaque pierre (`#`) aussi loin qu'il peut aller tout en respectant les obstacles («*»).
2. **Rotat** – Transférer la matrice et la retourner horizontalement (ou utiliser l'algorithme classique de 90° dans le sens des aiguilles d'une montre).

La complexité temporelle est **O(m × n)** et la complexité spatiale est **O(1)** supplémentaire (la matrice de sortie est la valeur de retour requise).

---

### -Java (style LeetCode)

"Java
Importer java.util. Les tableaux;

solution de classe publique {

omble public[][] tournerTheBox(char[]] boîte) {
int m = box.longueur; // lignes originales
int n = boîte[0].longueur; // cols originaux

/* 1=1 Appliquer la gravité – chaque ligne indépendamment */
pour (int i = 0; i < m; i++) {
int empty = n - 1; // spot vide le plus à droite
pour (int j = n - 1; j >= 0; j--) {
si (case[i][j]] == '*') { // obstacle
vide = j - 1; // la place libre suivante en reste
} sinon si (box[i][j] == '#') { // pierre
si (j != vide) {
boîte[i][vide] = '#';
boîte[i][j] = '.';
}
vide--; // la pierre suivante doit atterrir à gauche
}
}
}

/* 2/
char[][] tourne = nouveau char[n][m];
pour (int i = 0; i < m; i++) {
pour (int j = 0; j < n; j++) {
rotation[j][m - 1 - i] = boîte[i][j];
}
}
retour rotatif;
}

/* harnais d'essai simple – supprimer pour la soumission de LeetCode */
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
char[][] entrée = {
C'est quoi ?
};
char[]] out = s.rotateTheBox(input);
pour (char[] ligne : out) Système.out.println(Arrays.toString(row));
}
}
«» "

---

Python (Python 3.9+)

'`python
Solution de classe:
def rotation TheBox(self, box: list[list[str]]) -> list[list[str]]:
m, n = len(box), len(box[0])

N° 1 Appliquer la gravité – chaque ligne indépendamment
pour i dans la plage (m):
vide = n - 1
pour j dans la plage(n - 1, -1, -1):
dans la case [i][j] == '*':
vide = j - 1
boîte elif[i][j]]
Si j != vide :
boîte[i][vide] = '# '
box[i][j] = '. '
vide -= 1

# 2-- Rotation 90° dans le sens des aiguilles d'une montre
retour [[box[i][j] pour i dans la plage(m)][:-1] pour j dans la plage(n)]

# Exemple
si __nom__ == "__main__" :
s = Solution()
la grille = [["#", ".", "#"]]
print(s.rotateTheBox(grid))
«» "

---

C++ (C++17)

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur<vector<char>> tournerTheBox(vector<vector<char>>& boîte) {
int m = boîte.size();
int n = boîte[0].taille();

/* 1=1 Appliquer la gravité – chaque ligne indépendamment */
pour (int i = 0; i < m; ++i) {
int vide = n - 1;
pour (int j = n - 1; j >= 0; --j) {
si [box[i][j]] == '*') {
vide = j - 1; // obstacle bloque le chemin
} sinon si (box[i][j]]
si (j != vide) {
boîte[i][vide] = '#';
boîte[i][j] = '.';
}
--vide; // la pierre suivante doit atterrir à gauche
}
}
}

/* 2/
vecteur<vecteur<char>> tourné(n, vecteur<char>(m));
pour (int i = 0; i < m; ++i)
pour (int j = 0; j < n; ++j)
rotation[j][m - 1 - i] = boîte[i][j];

retour rotatif;
}
};
«» "

---

Article du blog – "Roting the Box: The Good, The Bad, and The Ugly"

> **Titre:** Rotation de la boîte (LeetCode 1861) – Une plongée profonde, une solution complète et des conseils d'entrevue
> **Méta—Description:** Master LeetCode 1861 -Rotation de la boîte avec pas à pas, code Java/Python/C++, analyse de complexité, gestion des cas de bord, et des explications conviviales pour l'entrevue. Augmentez votre score d'entrevue de codage!
> **Mots clés:** rotation de la boîte, leetcode 1861, rotation matricielle, simulation de gravité, interview prep, interview de codage, problème algorithmique, solution Java, solution Python, solution C++

---

Aperçu du problème

Sur LeetCode, vous obtenez une grille 2-D qui représente une vue latérale** d'une boîte rectangulaire.
Les cellules peuvent être :

Sens de caractère
C'est pas vrai.
* Pierre
Obstacle stationnaire
Espace vide

La boîte est tournée **90° dans le sens horaire**.
Les pierres tombent directement sous la gravité, s'arrêtant sur un obstacle, une autre pierre, ou le fond de la boîte.
Les obstacles ne bougent jamais, et les pierres gardent leur position horizontale pendant la rotation.

Votre tâche est de retourner la grille après la rotation.

> **Pourquoi est-ce important? * *
> Il teste votre capacité à manipuler des tableaux 2-D, à comprendre la simulation de gravité et à effectuer la rotation matricielle, tous les thèmes communs dans les entrevues de codage.

---

- Oui. Le bien: ce qui fonctionne

1. ** Gravité à deux points** – En scannant chaque rangée de droite à gauche et en maintenant la prochaine place libre (`vide`) nous pouvons glisser des pierres dans **O(n)** par rangée.
2. **Rotation déterministe** – Une seule boucle imbriquée tourne la matrice sans mémoire supplémentaire au-delà de la grille de résultats.
3. **Simplicité et lisibilité** – La solution n'utilise que des opérations primitives ; pas de bibliothèques fantaisistes ou de structures de données complexes.
4. **Complexité linéaire** – Avec `m × n ≤ 250 000`, l'algorithme s'inscrit confortablement dans les limites de temps de LeetCode.

---

C'est vrai. Les mauvais : les cas de bord & les gotchas

Numéro Explication
- C'est quoi ?
**Obstacles adjacents aux pierres**=Une pierre juste à côté d'un obstacle ne doit pas passer. La logique à deux points définit `vide = j - 1` lors de la rencontre `*`, assurant les terres de pierre qui en restent. Autres
Autres **Les touches sont déjà à la colonne la plus droite**= Ils doivent rester mis.= Si `j == vide`, le `si (j != vide)` garde saute des mouvements inutiles. Autres
Trop de boucles imbriquées pourraient atteindre la limite de récursion de Python? Nous évitons la récursion ; toutes les boucles sont itératives. Autres
**L'entrée non rectangulaire**LeetCode garantit un rectangle, mais une solution robuste doit protéger contre `box[i] == null`. Autres

---

C'est pas vrai. L'horrible : à quoi s'attendre

1. **Confuser les indices** – Rappelez-vous qu'après la rotation, la ligne originale devient une colonne. La formule `rotation[j][m - 1 - i] = boîte[i][j]` peut vous faire monter.
2. **Mutable Input** – L'algorithme mute la "box" originale. Si vous avez besoin de l'original pour le débogage, gardez une copie.
3. **Pièges linguistiques** –
* **Java**: Utilisez `char[]]` (et non `String[]`) pour éviter les chaînes immuables.
* **Python**: `list[list[str]]` est recommandé pour garder la mutabilité de ligne.
* **C++**: Éviter les départs avec le «vecteur<vecteur<char>>».

---

C'est vrai. Code Marche à suivre (Édition de Java)

"Java
// 1/ 1/ Appliquez la gravité sur chaque ligne
pour (int i = 0; i < m; i++) {
int vide = n - 1; // cellule libre la plus droite
pour (int j = n - 1; j >= 0; j--) { // scan de droite à gauche
si (boîte[i][j] == '*') { // obstacle – bloquer d'autres pierres
vide = j-1;
} sinon si (box[i][j] == '#') { // pierre
si (j != vide) { // déplacer seulement si déplacé
boîte[i][vide] = '#';
boîte[i][j] = '.';
}
vide--; // la pierre suivante doit atterrir à gauche
}
}
}
«» "

Pourquoi ça marche ? *
Parce que les pierres ne peuvent se déplacer qu'à gauche dans la grille ** de pré-rotation** (qui deviendra «down» après la rotation).
Le pointeur `vide` indique toujours le point vide le plus proche où une pierre pourrait s'installer.
Lorsque nous avons heurté un obstacle, nous réduisons la zone accessible en déplaçant `vide` une cellule gauche.

---

Analyse de complexité

Étape Temps Espace
C'est pas vrai.
Gravité par rangée
Autres Toutes les lignes
Rotation **O(m × n)**
**O(m × n)**

---

Test rapide (Python)

'`python
s = Solution()
quadrillage = [
["#", ".", "*", "."],
["#", "#", "*", "."]
- Oui.
print(s.rotateTheBox(grid))
♪ Attendu :
C'est pas vrai.
C'est pas vrai.
C'est pas vrai.
♪ ['.', '.']]
«» "

---

Conseils d'entrevue

- **Demander des éclaircissements** : par exemple, les pierres maintiennent-elles des positions horizontales après la rotation ? (en milliers de dollars)
- ** Expliquez votre approche à haute voix** : passez à travers la simulation de gravité et la rotation séparément.
- **Highlight ledge cases**: obstacles à côté de pierres, pierres à la limite, grilles vides.
- **La complexité du temps est importante**: rassurez l'intervieweur que vous n'utilisez pas des boucles imbriquées qui itèrent plus de deux fois sur toute la matrice.

---

#### 9.

- **Mots clés**: *Rotation de la boîte, LeetCode 1861, rotation matricielle, simulation de gravité, prep interview, problème algorithmique, solution Java, solution Python, solution C++*
- **Description détaillée**: *Maître LeetCode 1861, avec pas à pas, solution complète en Java, Python et C++, analyse de complexité et explications prêtes à l'entrevue. *
- **Blog Post Hook**: Vous souhaitez répondre à la question de matrix-manipulation lors de votre prochaine entrevue de codage? Lisez comment résoudre Rotation de la boîte en 30 secondes. (en milliers de dollars)

En publiant cet article sur une plate-forme qui se classe pour la solution de leetCode 1861, vous attirerez les gestionnaires d'embauche qui sont activement à la recherche de candidats qui peuvent résoudre les problèmes d'entrevue rapidement et proprement. Utilisez un ton engageant, des extraits de code, et une section prête à l'interview pour présenter votre état d'esprit de résolution de problèmes – exactement ce que les recruteurs veulent.

---

Enveloppe

Rotation de la boîte peut sembler intimidant au début, mais une fois que vous divisez le problème en **gravité** et **rotation**, la solution est simple et élégante.
Avec le code fourni dans votre langue préférée et l'explication amicale de l'entrevue ci-dessus, vous serez prêt à impressionner tout recruteur qui s'attaque à ce défi classique d'entrevue de codage. Bonne chance !

---

Codage heureux !
---

> *Nota de l'auteur: N'hésitez pas à adapter l'article à votre propre voix ou à ajouter vos propres exemples de monde réel. Plus vous donnez de contexte, plus les recruteurs de chance vous verront comme un atout précieux. *