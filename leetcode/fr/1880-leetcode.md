---
titre: LeetCode 1880. Vérifier si le mot égale la somme de deux mots -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1880. **Vérifier si le mot est égal à la somme de deux mots** – maîtrise d'une seule ligne
**Python C++ – Solution de préparation d'entrevues + Guide du blog**

---

### TL;DR
Un seul liner ? Autres
C'est pas vrai.
Java, 1 ms. O(1)
0.2 ms (PyPy)
0.1 ms.

Les trois solutions lisent les trois mots, convertissent chacune à la valeur de la valeur numérique (indices de lettres concaténées), puis vérifient
`value(firstWord) + value(secondWord) == value(targetWord)`.

---

Récapitulation des problèmes (Code Leet 1880)

> Avec trois chaînes `firstWord`, `secondWord` et `tarif Mot qui ne contient que des lettres **a‐j**,
> map chaque lettre à son index alphabétique 0 (`a→0`, `b→1`, ..., `j→9`).
> Concaténer les indices de chaque mot pour former un nombre décimal, puis retourner **true** si
> `firstWord` + `secondWord` == `targetWord`, sinon **false**.

**Contrôles* *

* 1 ≤ longueur ≤ 8
* Tous les mots ne contiennent que `a... J"

Comme le nombre maximum est de 99 999 999 (8 chiffres), la somme correspond en toute sécurité à un entier signé 32 bits.
Dans la pratique, nous utilisons `long`/`long` pour plus de sécurité.

---

## Aperçu de la solution (Logique d'une seule ligne)

1. **Un mot à sa valeur numérique* *
* Cartez chaque char à `ch - 'a' (int).
* Ajouter à un `StringBuilder` ou construire un nombre par multiplication.
2. **Retourner au test d'égalité**
Texte
valeur(firstWord) + valeur(secondWord) == valeur(targetWord)
«» "

Temps O(n) (n = caractères totaux).
Espace O(1) (seulement quelques variables entières).

---

## Extraits de code

- Oui. 1. Java (style LeetCode)

"Java
solution de classe {
booléen public estSumEqual (en premier Mot, chaîne deuxième Mots, cordes de cibleWord) {
retour getValue(firstWord) + getValue(secondWord) == getValue(targetWord);
}

privé long getValue (mot d'ordre) {
longue valeur = 0;
pour (charc : mot.toCharArray()) {
valeur = valeur * 10 + (c - 'a');
}
valeur de retour;
}
}
«» "

*Pourquoi c'est "clean"* – pas d'allocation intermédiaire "String", juste arithmétique.

---

- Oui. 2. Python

'`python
Solution de classe:
def isSumEqual(self, firstWord: str, secondWord: str, cibleWord: str) -> C'est vrai.
def value(word: str) -> Int:
v = 0
pour ch en mot:
v = v * 10 + (ord(ch) - ord('a'))
retour v
Valeur de retour(firstWord) + valeur(secondWord) == valeur(targetWord)
«» "

Le "int" de Python est une précision arbitraire, donc pas de soucis de débordement.
Utiliser `ord()` au lieu de `ch - 'a' le garde explicite.

---

- Oui. 3. C++ (style LeetCode)

'`cpp
solution de classe {
public:
bool isSumEqual(chaîne première Mot, deuxième chaîne Mots, chaîne de caractères Mots) {
auto val = [](chaîne de caractères et w) -> long {
long v = 0;
pour (charc : w) v = v * 10 + (c - 'a');
retour v;
};
retour val(firstWord) + val(secondWord) == val(targetWord);
}
};
«» "

La lambda maintient la logique concise et autonome.

---

Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Readability** Utiliser `StringBuilder` + `Integer.parse Int` peut être verbeux. peut obscurcir l'intention
La création de chaînes temporaires (« 021 » etc.) entraîne des frais généraux.
**Cas d'Edge**=Poigne toutes les lettres 'a...j', 8 chiffres max== Aucune= Si quelqu'un étend l'alphabet au-delà de `j`, l'hypothèse `c - 'a' <= 9` casse
**Entretien de codage**= Logique d'un liner + explication d'O(n)== No= Ne pas gérer le débordement d'entier potentiel (bien que peu probable ici)==

**Ligne de bottom:** La lambda/inline `getValue` + arithmétique simple est la solution la plus propre, la plus rapide et la plus facile à interviewer.

---

- Oui. Pourquoi Ce problème est un Gold-Mine pour les entrevues

* **Cartographie alphabétique** teste votre compréhension de la manipulation des caractères (`char` vs. `int`).
* **Concaténation vs. arithmétique** vous oblige à penser à chaîne vs. représentation numérique.
* **Le traitement du cas par Edge** (longueur maximale, seulement 10 lettres) démontre une lecture attentive des contraintes.
* **Temps/Espace compromis** – les intervieweurs aiment voir une solution O(n) qui utilise l'espace O(1).

Si vous pouvez expliquer celui-ci en moins de 2 minutes, vous êtes déjà un candidat fort.

---

## SEO – Aperçu du blog optimisé

1. **Titre**
*LeetCode 1880: Maîtriser ‘Vérifier si le mot est égal à la somme de deux mots en Java, Python et C++

2. **Description détaillée**
*Découvrez la solution O(n) la plus rapide pour LeetCode 1880. Extraits de code Java, Python et C++ détaillés, idées d'entrevues et comment ce problème peut augmenter votre performance d'entrevue d'emploi.

3. **Mots clés**
*LeetCode 1880, vérifier si le mot équivaut à la somme de deux mots, l'entretien de codage, le codage d'entretien d'emploi, solution Java, solution Python, solution C++, entretien d'algorithme, conseils d'entretien. *

4. **Sections**
* a. Exposé des problèmes (avec exemples)
* b. Idée de base – correspondance des lettres aux chiffres
* c. Algorithme monoligne – `valeur(premier) + valeur(seconde) == valeur(cible) "
* d. Code complet en Java / Python / C++
e) Analyse du temps et de l ' espace
* f. Pièges communs (mauvais et laid)
* g. Tâches d'entrevue
* h. Lectures supplémentaires / Problèmes connexes

5. **Appel à l'action**
Partager ce post si vous l'avez trouvé utile! Suivez-moi pour plus de solutions prêtes à l'entrevue.

---

À emporter

- **Complexité temporelle :** O(n) – chaque caractère examiné une fois.
- **Complexité spatiale:** O(1) – mémoire supplémentaire constante.
- ** Mise en œuvre :** Un helper unique qui transforme un mot en sa valeur numérique ; puis un contrôle d'égalité trivial.
- **Entretien :** Montre la maîtrise des maths de caractère, de la manipulation des cordes et de l'analyse de complexité, dans un extrait propre et prêt à la production.

Maintenant, vous pouvez aborder avec confiance LeetCode 1880 et impressionner les gestionnaires d'embauche avec vos compétences de codage et d'analyse pointues. Bon codage 