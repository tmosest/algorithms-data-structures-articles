---
titre: LeetCode 3274. Vérifiez si deux carrés de tableau d'échec ont la même couleur -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 3274. Vérifiez si deux carrés de tableau d'échec ont la même couleur
*(LeetCode – Facile)*

> **Objectif** – Compte tenu de deux coordonnées du tableau d'échecs (par exemple, `"a1"` et `"c3"`), retourner `true` si les deux carrés ont la même couleur (noir ou blanc) et `faux` autrement.

Langue Heure Espace
- C'est quoi ?
J.O.I.(1)
Python O(1)
(En milliers de dollars des États-Unis)

---

C'est pas vrai. L'idée – Un trick mathématique à une ligne

Sur une carte standard 8 × 8, le motif de couleur alterne comme un tableau de bord.
Si nous convertissons une coordonnée en un seul entier:

«» "
valeur = (lettre de colonne) + (numéro de ligne)
«» "

* la lettre de colonne peut être transformée en sa valeur ASCII ( `'a'` → 97, `'b'` → 98, ...),
* le numéro de ligne est déjà un chiffre 1‐8.

Toutes les valeurs **even** correspondent à une couleur (disons noir) et toutes les valeurs **odd** à l'autre couleur.
Par conséquent, deux carrés ont la même couleur **iff** la parité de leurs valeurs correspond.

Texte
valeur1 % 2 == valeur2 % 2 → même couleur
«» "

C'est ça – 3 lignes de code.

---

Mise en œuvre

Java

"Java
solution de classe {
contrôle public du booléen TwoChessboards(Coordonnée de la chaîne1, Coordonnée de la chaîne2) {
int v1 = coordinator1.charAt(0) + Character.getNumericValue(coordorator1.charAt(1));
int v2 = coordinate2.charAt(0) + Character.getNumericValue(coordinate2.charAt(1));
retour (v1 & 1) == (v2 & 1); // même parité → même couleur
}
}
«» "

> **Pourquoi `& 1`?**
> C'est une micro-optimisation minuscule: bitwise ET est plus rapide que "% 2".

---

Python 3

'`python
Solution de classe:
Contrôle TwoChessboards(self, coordinator1: str, coordinator2: str) -> C'est vrai.
v1 = ord(coordonné1[0]) + int(coordonné1[1])
v2 = ord(coordonné2[0]) + int(coordonné2[1])
retour v1 % 2 == v2 % 2
«» "

---

C++

'`cpp
solution de classe {
public:
Contrôle des bools TwoChessboards(coordonnée de chaîne1,coordonnée de chaîne2) {
int v1 = coordonnée1[0] + (coordonné1[1] - '0');
int v2 = coordonnée2[0] + (coordonné2[1] - '0');
retour (v1 & 1) == (v2 & 1);
}
};
«» "

---

- Oui. Billet de blog – *Les bons, les mauvais et les méchants*

> **Référencement:**
> *LeetCode 3274 – ♫Vérifiez si deux carrés d'échec ont la même couleur – Java, Python, C++ Solutions & Interview‐ Guide prêt*

> **Meta Description:**
> Résolvez le LeetCode 3274 en moins de 5 minutes. Lisez le code Java, Python et C++ propre et efficace, ainsi que l'intuition derrière le tour des maths. Apprenez à coder les entrevues!

3.1 Les bons – Pourquoi Ce problème est une réussite *Starter*

1. **O(1) Temps, O(1) Espace** – Idéal pour les intervieweurs à la recherche de solutions à temps constant.
2. **Mathématical Insight** – souligne la capacité du candidat à voir des modèles (ASCII + parité numérique).
3. **Language-agnostique** – La même logique fonctionne en Java, Python, C++, Allez, etc.
4. **Clean Code** – Un 3-liner démontre sa lisibilité et sa précision.

J'ai résolu 3274 en 3 minutes lors de mon dernier entretien. L'intervieweur a été impressionné par le tour des maths.

3.2 Les mauvaises – Les pièges communs à éviter

Pourquoi ça compte ?
- Oui.
**Utilisation incorrecte des conversions `int` et `char`** est un «char»; l'ajouter à un «int» sans convertir le deuxième chiffre en un nombre produira ASCII + ASCII (par exemple, «97 + 49» pour «a1»); Convertir le chiffre correctement (`int(coordonné[1]) - '0'' en C++/Java ou `int(coordonné[1])' en Python). Autres
**Off‐by‐one errors**. Oublier que les lignes commencent à `'1'` → doivent soustraire `'0'` ou utiliser `int()` Utiliser `Caracter.getNumericValue()` ou `int()` dans Python. Autres
La même couleur signifie même *lettre* ou même *numéro*. Autres
**Performance désaccordée**=En utilisant `% 2` au lieu de bitwise `& 1` (pas critique mais agréable)= Remplacer par `(v & 1)` pour la vitesse. Autres

3.3 La mauvaise direction et l'excès d'ingéniosité

1. **Simuler le tableau d'échecs** – Bâtir une matrice 8×8 et la remplir de couleurs, c'est trop.
2. **Approche récursive ou PDD** – Pas de récursion nécessaire; un contrôle à temps constant est tout ce qui est requis.
3. **Parsing parsing Overkill** – L'utilisation de régex ou de sous-chaîne ajoute des frais généraux inutiles.
4. **Utiliser des structures complexes de données** – Cartes, ensembles ou Enums pour stocker des couleurs ajouter du bruit.

J'ai passé 20 minutes à écrire un Chessboard avec "getColor(row, col)" avant de réaliser le tour de parité. – *Jordanie, développeur de niveau intermédiaire*

3.4 Comment le faire dans une vraie interview

1. **Exposer le premier aperçu**
- Je remarque que chaque couleur carré peut être déduite de la parité de la somme de sa colonne ASCII code et numéro de ligne. (en milliers de dollars)
2. **Afficher les mathématiques**
- Fournir l'équation simple: `color = (col + ligne) % 2`.
3. **Écrire le code**
- Gardez-le concis, commentez le moins possible, mais mentionnez la conversion pour plus de clarté.
4. **Courir les cas d'essai rapide* *
- `"a1", "c3"` → vrai
- `"a1", "h3"` → faux
- `"d4", "f6"` → vrai
5. **Parler de la complexité* *
- O(1) temps, O(1) espace.

---

Pourquoi devriez-vous maîtriser ce problème ?

- **Shows Pattern Recognition** – L'intervieweur aime les candidats qui peuvent repérer le tour algébrique caché.
- **Démontre la propreté du code** – Un 3-liner est élégant et durable.
- **Construire la confiance** – Une petite victoire renforce votre moral pour le prochain problème, plus difficile.

Dépôt de code final

Lien
C'est quoi, ça ?
Java (en anglais seulement) https://github.com/yourrepo/leetcode3274-java Autres
https://github.com/yourrepo/leetcode3274-python Autres
https://github.com/yourrepo/leetcode3274-cpp Autres

> *Push votre code, commit souvent, et utiliser des messages de commit clairs – cette pratique impressionne les gestionnaires d'embauche. *

---

### Appel à l'action

> **Prêt pour le prochain défi? **
> Pratiquez ce trick de reconnaissance sur d'autres problèmes de couleur ou de parité comme *=Nombre d'étapes pour réduire un nombre* ou *=Kth Distance de paire la plus petite*.
> Ajoutez la solution à votre portfolio et marquez-la avec **#leetcode**.

Bon codage, et bonne chance avec votre prochaine interview!