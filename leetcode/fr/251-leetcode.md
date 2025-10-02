---
Titre: LeetCode 251. Vecteur 2D aplati -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

- Oui. 1. Récapitulation des problèmes
**Flatten 2-D Vecteur – LeetCode 251**

> Concevoir un itérateur qui aplatit un vecteur 2-D.
> L'itérateur doit soutenir les deux opérations
> `suivant()` – retourner l'élément suivant,
> `hasNext()` – retournez si d'autres éléments restent.

Le vecteur d'entrée peut être vide, peut contenir des sous-réseaux vides et a jusqu'à 200 × 500 éléments. Jusqu'à 105 appels à `next()` et `hasNext()` seront effectués.

---

- Oui. 2. Pourquoi il s'agit d'une question d'entrevue
* **Concepts de base** – conception d'itérateur, manipulation de pointeur, opérations amorties O(1).
* **Cas d'Edge** – lignes vides, longueurs de lignes variables, grands ensembles de données.
* **Suivi** – implémenter l'itérateur ** sans structure de données supplémentaires** (modèle de l'itérateur pur).

Répondre à cette question démontre clairement votre capacité à travailler avec les itérateurs, garder l'état correctement, et optimiser pour le temps et l'espace.

---

- Oui. 3. La solution "Deux-Pointeurs"

L'approche la plus simple et la plus efficace maintient **deux indices**:

Valeur de la variable
- C'est quoi ?
Indice de la ligne courante de la ligne `0 ≤ ligne < vec.size()` ou `row == vec.size()` si terminé
Indice de la «col» dans la ligne courante si terminé

L'algorithme :

1. **Constructeur** – initialiser `row = 0`, `col = 0`.
Passer sur les lignes vides de sorte que l'itérateur commence au premier élément réel.
2. **hasNext()** – retourne `true` iff `row < vec.size()`.
(Si nous avons dépassé la dernière ligne, nous avons fini.)
3. **suivant()** –
* Prenez "vec[row][col]".
* Augmentation "col".
* Si `col` atteint la fin de la ligne courante, passer à la prochaine ligne non vide (incrément `row`, réinitialiser `col` à `0`).

Toutes les opérations se déroulent en **O(1) temps amorti** et utilisent **O(1) espace supplémentaire**.

---

- Oui. 4. Mise en œuvre du code

#### 4.1 Java

"Java
Importer java.util. Liste;

***
* Iterator qui aplatit un vecteur entier 2-D.
* Utilise seulement deux indices – un modèle d'itérateur pur.
*/
classe publique Vector2D {
int[]] vec; // le tableau 2-D
ligne int privée = 0; // ligne courante
int privé col = 0; // colonne courante

public Vector2D(int[]] vec) {
ce.vec = véc;
avanceToNext(); // sauter toutes les lignes vides en tête
}

*** Retourne l'élément suivant. */
public int next() {
valeur int = vec[row][col];
col++; // passer à la colonne suivante
avanceToNext(); // sauter à l'élément valide suivant
valeur de retour;
}

*** Y a-t-il d'autres éléments? */
public booléen aSuivant() {
ligne de retour < longueur vec.;
}

/** Déplacer la ligne/col vers le prochain élément non vide. */
avancée privée du vide versNext() {
// Si nous avons terminé la ligne actuelle, passez à la prochaine ligne non vide.
pendant que (ligne < vec.longueur &&col >= vec[row].longueur) {
ligne++;
col = 0;
}
}
}
«» "

Utilisation

"Java
int[[]] données = {{1, 2}, {3}, {4}};
Vector2D vec = nouveau Vector2D(données);
pendant que (vec.hasNext()) {
Système.out.println(vec.next());
}
«» "

---

4.2 Python

'`python
classe Vector2D:
"""
Iterator qui aplatit une liste 2D.
Utilise deux indices : self.row, self.col.
"""
def __init_(self, vec):
Self.vec = Vec
Self.row = 0
Self.col = 0
Self._skip_vide_rows()

def next(self):
"""Retourner l'élément suivant."""
val = self.vec[self.row][self.col]
Self.col += 1
Self._skip_vide_rows()
retour val

def hasNext(self):
"""Retour Vrai si plus d'éléments restent."""
Retourner soi-même.row < len(self.vec)

def _skip_vide_rows(self):
""Avant le prochain élément non vide."""
pendant que self.row < len(self.vec) et self.col >= len(self.vec[self.row]):
Self.row += 1
Self.col = 0
«» "

Utilisation

'`python
données = [[1, 2], [3], [4]]
vec = Vector2D(données)
alors que vec.hasNext():
print(vec.next())
«» "

---

### 4.3 C++

'`cpp
#incluez <vecteur>

classe Vector2D {
particulier:
Les résultats de l'enquête ont été publiés dans le Bulletin de l'Union européenne. Vec;
taille_t ligne = 0, col = 0;

// Déplacer vers l'élément valide suivant
avance nulle() {
pendant que (ligne < vec.size() && col >= vec[row].size()) {
+ ligne;
col = 0;
}
}

public:
Vector2D(const std::vector<std::vector<int>&& v) : vec(v) {
avancée(); // sauter en tête des lignes vides
}

Int next() {
int val = vec[row][col++];
avance();
valeur de retour;
}

bool hasNext() const {
ligne de retour < vec.size();
}
};
«» "

Utilisation

'`cpp
std::vector<std::vector<int>> données = {{1,2}, {3}, {4}};
Vector2D v(données);
alors que (v.hasNext()) {
std::tout << v.next() << ";
}
«» "

---

- Oui. 5. Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Simplicité**= Deux indices, pas de copie de conteneur – facile à raisonner. Requiert une manipulation soigneuse des lignes vides. Oublier de sauter les lignes vides → s'écrase sur `next()` ou une mauvaise sortie. Autres
**Complexité du temps** Le constructeur est O(1) – aucun coût de prétraitement. Certains intervieweurs pourraient s'attendre à une approche *lazy* qui fonctionne également dans `O(1)` sans scanner des lignes à chaque fois. Autres
Autres **Complexité spatiale** Doit stocker la référence originale; ne peut pas copier le vecteur entier. L'utilisation d'une file d'attente ou `deque` peut gaspiller la mémoire pour de très grandes données. Autres
**Suivant (Iterator-Only)**= Ne fonctionne qu'avec des indices bruts – pas d'aide. Java/C++ ont intégré des itérateurs; Python utilise aussi des indices. Sur-ingénierie : l'utilisation de plusieurs itérateurs, ou la manipulation de `NoSuchElementException` peut masquer la logique de base. Autres

**À emporter :** L'approche à deux pointeurs est la solution la plus conviviale pour les interviews. Il équilibre la clarté, la vitesse et l'utilisation de la mémoire.

---

- Oui. 6. Pointeurs de blog optimisés SEO

Pour décrocher ce poste d'interview de structure de données, saupoudrez l'article de ces mots clés :

* Question de l'interview de l'auteur de l'article "
* `entretien de tableau 2D flatté "
* `LeetCode 251 solution "
* "deux techniques de pointeur "
* `Python conception itérateur "
* `C++ vecteur itérateur "
* "O 1) itérateur de temps "

Utilisez des rubriques H1‐H3 claires (celles de cet article) et insérez la méta-description riche en mots clés :

> Découvrez la meilleure solution pour le LeetCode 251 – Flatten 2-D Vector. Obtenez des exemples de code Java, Python et C++, ainsi qu'un guide étape par étape pour implémenter un itérateur pur qui fonctionne dans l'espace O(1) time et O(1). (en milliers de dollars)

Ajoutez également une section **tags** en bas pour une référence rapide :

Texte
Mots clés: Java, Python, C++, Iterator, LeetCode 251, Flatten 2D Vector, Interview
«» "

---

- Oui. 6. Conclusion

Aplatir un vecteur 2-D avec un itérateur est un problème d'entrevue classique qui teste votre compréhension de l'itération majestueuse, de la manipulation des cas de bord et de l'optimisation algorithmique.

La solution la plus concise, la plus efficace dans le temps et la plus respectueuse de l'espace est le modèle à deux pointeurs, l'itérateur pur. Il est simple d'implémenter dans **Java, Python et C++** – il suffit d'adapter la logique de l'index aux idiomes du langage.

En maîtrisant cette question, vous impressionnerez les intervieweurs qui apprécient le code propre et efficace et qui veulent vous voir résoudre les cas de bord dur avec des frais généraux minimes. Bonne chance pour votre prochain entretien !