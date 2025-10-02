---
titre: LeetCode 2022. Convertir 1D Array en 2D Array -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# Convertissez 1D Array en 2D Array – LeetCode 1714
**Facile**

> **Problème** – LeetCode 1714
> *On vous donne un tableau entier 1-D indexé 0 `original` et deux entiers `m` et `n`.
> Construire un tableau `m × n` 2-D qui contient tous les éléments de `original` dans l'ordre des lignes.
> Si `original.longueur!= m * n`, retourner un tableau 2-D vide. *

---

Pourquoi ce problème fait-il un entretien d'embauche ?

* **Manipulation d'images** – compétences de base de la CS
* **Complexité du temps et de l'espace** – démontre la pensée analytique
* **La sensibilisation aux causes** – montre l'attention aux détails
* **Language-agnostic** – facile à mettre en œuvre dans n'importe quelle langue

Maîtriser celui-ci vous donne une solide confiance que les recruteurs aiment.

---

## Aperçu de la solution

1. ** Vérification de faisabilité* *
Texte
si original. longueur != m * n → retourner la matrice vide
«» "
2. **Cartographie linéaire**
Chaque élément `original[i]` maps to position `(row, col)` dans le résultat:
Texte
ligne = i / n (division entière)
= i % n
«» "
Équivalent à:
Texte
résultat[ligne][col] = original[i]
«» "
ou, en utilisant des boucles imbriquées:
Texte
résultat[i][j] = original[i*n + j]
«» "
3. **Retourner la matrice construite**.

---

Analyse de complexité

La complexité Raison
C'est pas vrai.
**Heure**="O(m * n)" – chaque élément est visité exactement une fois. Autres
**L'espace**=O(m * n)– matrice de sortie. Espace supplémentaire `O(1)` en dehors de la sortie. Autres

---

Code en trois langues

C'est pas vrai. Java – Simulation simple (98,3 % plus rapide)

"Java
solution de classe {
int[][]construire2Darray(int[] original, int m, int n) {
// 1. Essai de faisabilité rapide
si (original.longueur != m * n) retourner une nouvelle int[0][0];

// 2. Aligner la matrice de résultats
int[][] résultat = nouveau int[m][n];

// 3. Remplir ligne par ligne
pour (int i = 0; i < m; i++) {
pour (int j = 0; j < n; j++) {
résultat[i][j] = original[i * n + j];
}
}
le résultat du retour;
}
}
«» "

> **Bien** – O(1) espace supplémentaire, cartographie directe.
> **Bad** – Aucune.
> **Énormément** – Aucune.
> Juste une solution propre et prête à la production.

Python – Concise One-liner

'`python
Solution de classe:
def construct2DArray(self, original: List[int], m: int, n: int) -> Liste[Liste[int]]:
Contrôle rapide
si len(original) != m * n:
retour []

2. Remodeler en tranchant (Pythonique)
retour [original[i*n:(i+1)*n] pour i dans l'intervalle(m)]
«» "

> **Bien** – Utilisation de la tranche pythonique, lisible.
> **Bad** – Aucune.
> **Énormément** – Aucune.

#####C++ – Approche standard de la bibliothèque

'`cpp
solution de classe {
public:
vector<vector<int>> construct2DArray(vector<int>& original, int m, int n) {
// Vérification de faisabilité
si (original.size() != static_cast<size_t>(m * n))
retour {};

// Matrice de préallocate
résultats du vecteur<vector<int>>(m, vector<int>(n));

// Remplir la matrice
pour (int i = 0; i < m; ++i)
pour (int j = 0; j < n; ++j)
résultat[i][j] = original[i * n + j];

le résultat du retour;
}
};
«» "

> **Bonne** – Utilise efficacement le «vecteur».
> **Bad** – Aucune.
> **Énormément** – Aucune.

---

Cas de bord et pièges communs

Pourquoi ça compte ?
- Oui.
Durée initiale Les contraintes de problème l'interdisent, mais si vous les détendez, vous devez le gérer. Retourner `[]` ou une matrice vide en conséquence. Autres
`m * n` déborde 32 bits int Dans les langues avec int 32 bits (Java, C++), `m * n` peut déborder avant comparaison. Passez à `long` ou utilisez `size_t`. Autres
Pas permis par les contraintes, mais la programmation défensive est bonne. Valider et renvoyer vide. Autres
Il faut du temps linéaire, pas des boucles emboîtées qui calculent `i*n + j` à plusieurs reprises avec des frais de multiplication. Utiliser l'index `k` pour itérer une fois. Autres

---

Comment utiliser ceci dans une entrevue d'emploi

1. **Énoncer le plan** – Clarifier la faisabilité, la cartographie, la complexité.
2. **Write Clean Code** – Utilisez des noms de variables descriptives, commentez la vérification.
3. **Discuss Edge Cases** – Afficher la conscience du débordement, tableau vide.
4. **Talk Performance** – Souligner le temps O(m*n), l'espace auxiliaire O(1).
5. **Afficher les variantes** – Mention en python ou en mapping de flux en Java 8+.

Les intervieweurs aiment les candidats qui pensent à la fois à la justesse et à la robustesse.

---

## SEO Aperçu de blog optimisé

Titre
**"LeetCode 1714 – Convertir 1D Array en 2D Array: Java, Python, C++ Solutions + Conseils d'entrevue"* *

Description de la méta
"Master LeetCode 1714 avec des solutions étape par étape en Java, Python et C++. Apprenez le remaniement du tableau, l'analyse de la complexité, les cas de bordure et la discussion prête à l'entrevue.»

Rubriques

Contenu
- Oui.
LeetCode 1714 – Convertir 1D Array en 2D Array
**H2** , Déclaration de problème (facile)
Pourquoi ce problème compte dans les entrevues
**H3**
L'algorithme et la complexité
**H3**
Cartographie linéaire
Mise en œuvre complète du code
*H3 *Java
*H3 * Python *
C++
**H2**=Cas de bord et codage défensif
**H2**= Conseils d'entrevue et points de discussion=
**H2**

Mots clés et phrases
- LeetCode Convertir 1D Array en 2D Array
- remodelage du tableau Java
- Construction d'un tableau Python 2D
- Problème de matrice C++ 2D
- manipulation du tableau d'entretien
- Algorithme O(mn)
- la manipulation des cas bord

Utilisez ces mots clés naturellement dans les rubriques, le premier paragraphe, et la conclusion pour stimuler le référencement.

---

À emporter

- **Problème** : remodeler un tableau 1-D en `m × n` si possible.
- **Solution** : pass linéaire unique avec calcul direct de l'indice.
- **Complexité**: temps «O(mn)», espace «O(mn)».
- **Langues**: propres Java, Python, extraits C++.
- **Interview**: expliquer l'algorithme, discuter des cas de bord, afficher le code propre.

Avec cette connaissance, vous êtes prêt à répondre à la question d'interview de 1D Convert 1D Array en 2D Array et impressionner les recruteurs ! C'est ce qu'il a dit