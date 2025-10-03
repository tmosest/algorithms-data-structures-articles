---
Titre: LeetCode 1899. Fusionner Triplettes pour former Triplette cible -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
1899. Fusionner les triplets pour former la triplette cible – Solutions et entrevues‐ Prêt Blog Post

> **TL;DR**
> La solution gourmande est le temps O(n), l'espace O(1) – filtrez simplement les triplets et vérifiez que chaque composant de la cible peut être atteint.

Ci-dessous vous trouverez l'implémentation complète et spécifique à la langue (Java, Python, C++), suivie d'un article de blog complet, optimisé par le SEO, qui explique le problème, la logique, les pièges, et comment vous pouvez l'utiliser pour as votre prochaine interview.

---

Solutions de code

- Oui. 1. Java

"Java
Importer java.util. Les tableaux;

solution de classe {
fusion booléenne publiqueTriplets(int[][] triplets, int[] cible) {
int[] res = nouvelle int[3]; // courant max
pour (int[] t : triplets) {
// Sauter n'importe quel triplet qui est trop gros dans n'importe quelle dimension
si (t[0] <= cible[0] &&t[1] <= cible[1] &&t[2] <= cible[2]) {
res[0] = Math.max(res[0], t[0]);
res[1] = Math.max(res[1], t[1]);
res[2] = Math.max(res[2], t[2]);
}
}
retour Arrays.egals(res, cible);
}
}
«» "

> **Pourquoi cela fonctionne:**
> *Si un triplet dépasse la cible dans n'importe quelle dimension, il ne peut jamais vous aider à atteindre la cible. *
> Nous ne fusionnons que des triplets de type « good », prenant le maximum par composante. Si le maximum final est égal à la cible, la réponse est "vrai".

---

- Oui. 2. Python

'`python
Solution de classe:
def mergeTriplets(self, triplets: List[List[int]], cible: List[int]) -> bool:
res = [0, 0, 0] # courant max
pour t dans les triplets:
si tous(t[i] <= cible[i] pour i dans l'intervalle(3)):
pour i dans la plage(3):
res[i] = max(res[i], t[i])
return res == cible
«» "

---

- Oui. 3. C++

'`cpp
solution de classe {
public:
Bool mergeTriplets(vecteur<vecteur<int>>& triplets, vecteur<int>& cible) {
vecteur <int> res(3, 0);
pour (auto & t : triplets) {
si (t[0] <= cible[0] &&t[1] <= cible[1] &&t[2] <= cible[2]) {
res[0] = max(res[0], t[0]);
res[1] = max(res[1], t[1]);
res[2] = max(res[2], t[2]);
}
}
return res == cible;
}
};
«» "

---

> Les trois solutions fonctionnent dans **O(n)** temps et **O(1)** espace supplémentaire, où *n* = `triplets.length`.
> Ils sont faciles à comprendre, faciles à déboguer et parfaits pour coder les entrevues.

---

Article du blog – Fusionnez les Triplettes pour former la triplette cible : le bon, le mauvais et le mauvais.

### Titre (friendly SEO)
> ** Fusionner les triplets pour former la triplette de la cible – Un code de leet #1899 Guide (Java, Python, C++)* *

Description de la méta
> Résolvez LeetCode 1899 avec un algorithme gourmand. Apprenez les solutions Java, Python et C++, l'analyse du temps et de l'espace, les pièges et les conseils d'entrevue.

Aperçu

Section du contenu
C'est pas vrai.
Autres 1. Introduction Récapitulation du problème et pourquoi il importe pour les entrevues
Autres 2. Déclaration de problème
Autres 3. Le Greedy Insight (Bon)
Autres 4. Code Walk‐through (Good) - Explication détaillée de la solution O(n) -
Autres 5. Erreurs courantes et cas de bord (Bad)
Autres 6. Solutions de rechange avancées (Ugly)
Autres 7. Analyse de la complexité
Autres 8. Stratégie de l'entrevue
Autres 9. Takeaway: Résumé et prochaines étapes

---

- Oui. 1. Présentation

LeetCode="Merge Triplets to Form Target Triplet=" (problème #1899) est un défi **moyen‐difficulté** qui apparaît sur de nombreuses piles d'entrevues.
Il teste :

- **Le raisonnement grêle** – sélectionne seulement les triplets utiles.
- **Manipulation d'images** – maximum par composante.
- **Connaissance au cas par cas** – contraintes de compréhension (triplettes ≤ cible).

Savoir comment résoudre ce problème en **Java, Python et C++** vous donne une victoire rapide sur les tests de codage et un point de conversation solide pour les entretiens techniques.

---

- Oui. 2. Exposé des problèmes

> **Input:**
> `triplets`: `int[]`, taille *n* (1 ≤ *n* ≤ 105)
> `cible`: `int[]`, longueur 3
> **Output:** `boolean` – si la cible peut apparaître après une série d'opérations de fusion.

**Merge operation**: choisir deux indices `i` et `j` (`i --j`) et remplacer `triplets[j]` avec
«[max(ai, aj), max(bi, bj), max(ci, cj)]».

**Objectif:** Retour `true` si un triplet peut devenir exactement `cible`.

---

- Oui. 3. Le point de vue sur l'avidité (bon)

> **Observation 1** – Un triplet qui dépasse la cible dans toute dimension ne peut jamais aider.
> **Reason:** L'opération `max` ne diminue jamais une valeur. Si un composant est déjà plus grand que les cibles, la fusion ne peut qu'aggraver le résultat.

> **Observation 2** – Si nous continuons à fusionner tous les triplets de bonne qualité (=), le maximum de composants résultant est le *meilleur que nous pouvons atteindre*.

Ainsi, un simple scan qui :

1. **Filtres** sur les triplets.
2. **Garde un max** courant pour chaque coordonnée.

est suffisant.

---

- Oui. 4. Passage du code (bon)

C'est vrai. Java
"Java
int[] res = nouvelle int[3]; // courant max
pour (int[] t : triplets) {
si (t[0] <= cible[0] &&t[1] <= cible[1] &&t[2] <= cible[2]) {
res[0] = Math.max(res[0], t[0]);
res[1] = Math.max(res[1], t[1]);
res[2] = Math.max(res[2], t[2]);
}
retour Arrays.egals(res, cible);
«» "

* Points clés: *

- `t[0] <= cible[0] && ...` – vérification de dimension explicite.
- `Math.max` – mise à jour par composante.
- "Arrays.equals" – comparaison finale.

Python
'`python
res = [0, 0, 0] # courant max
pour t dans les triplets:
si tous(t[i] <= cible[i] pour i dans l'intervalle(3)):
pour i dans la plage(3):
res[i] = max(res[i], t[i])
return res == cible
«» "

C++
'`cpp
vecteur <int> res(3, 0);
pour (auto & t : triplets) {
si (t[0] <= cible[0] &&t[1] <= cible[1] &&t[2] <= cible[2]) {
res[0] = max(res[0], t[0]);
res[1] = max(res[1], t[1]);
res[2] = max(res[2], t[2]);
}
}
return res == cible;
«» "

> **Pourquoi c'est élégant:**
> *Un seul passe, aucune structure de données supplémentaire, aucune boucle compliquée. *

---

- Oui. 5. Erreurs courantes et cas de bord (mal)

Pourquoi ça arrive ?
- Oui.
Autres **Incluant les triplets de "bad"
**Utiliser `==` au lieu de `>=`**
**Over-optimiser avec les drapeaux**=Le suivi des drapeaux pour chaque coordonnée peut être trompeur si un seul triplet couvre deux coordonnées== La méthode max en cours est plus sûre===
En supposant que *n* est minuscule → en utilisant des doubles boucles O(n2)

---

- Oui. 6. Solutions de remplacement avancées

> Certains candidats tentent de sur-ingénieur :
> - **Programme dynamique** sur l'espace d'état de 3 coordonnées → mémoire exponentielle.
> - **La première recherche** sur toutes les fusions possibles → O(n2) dans le pire des cas.
> - **Recursive backtracking** pour essayer chaque ordre de fusion → 105! des possibilités.

Ces approches sont ** inutiles**; elles font exploser le plus grand cas d'essai et ne sont pas favorables aux entrevues.

---

- Oui. 7. Analyse de la complexité

Java / Python / C++
-- -- -- -- -- -- -- -- --
**Temps** **O(n)** – un balayage linéaire. Autres
**Espace******O(1)** – seulement 3 variables entières. Autres

> **Pourquoi O(n) est-il optimal? **
> Chaque triplet doit être examiné au moins une fois pour confirmer qu'il est bien ou non. Il n'y a pas d'algorithme plus rapide car l'entrée elle-même est linéaire dans la taille.

---

- Oui. 8. Stratégie d'entrevue

1. ** Expliquez l'observation gourmande** d'abord – cela montre que vous comprenez la logique fondamentale.
2. **Va à travers le code** tout en mettant en évidence le filtre et le max en cours d'exécution.
3. **Les cas de bord de discussion** – par exemple, tous les triplets dépassent la cible → répondre `false`.
4. **Réponse aux questions de suivi** (peut-on modifier l'algorithme si la cible est longue) 3? → encore la même idée).
5. **Écrire un code propre et idiomatique** – choisissez l'un des extraits fournis.

Si le temps est serré, commencez par la solution Python à trois lignes; si vous êtes dans une interview Java, la version basée sur un tableau est souvent préférée.

---

- Oui. 9. A emporter

- **LeetCode 1899** est un problème avide de manuels.
- Un seul passe qui **filters out triplets** et **tracks un maximum** en cours d'exécution le résout en temps linéaire.
- Éviter la suringénierie; s'en tenir à la solution gourmande à moins que l'intervieweur ne demande explicitement une approche différente.
- Oui. Utilisez les extraits de code comme feuille de triche pour votre prochaine entrevue ou test de codage en ligne.

Autres **Étape suivante:** Exécutez les solutions sur LeetCode, ajoutez la classe `Solution` à votre projet local, et pratiquez l'explication de la logique à haute voix. Vous vous sentirez confiants en s'attaquant à des problèmes similaires à ceux d'une personne sur n'importe quel entretien technique.

---

Liste de contrôle du référencement

Qu'est-ce qu'inclure
-- -- -- -- -- --
Mots-clés Fusionner Triplelets pour former Triplet cible, Leetcode 1899, Solution de Java, Solution de Python, Solution de C++, Algorithme de gré à gré
Autres Mots-clés de la méta Titre, description, URL canonique
Titres H1: Titre du problème, H2: Bonne/Bad/Ugly sections
Lien vers d'autres articles de LeetCode sur votre blog
Référence à la page du problème officiel de LeetCode
Ajouter un petit diagramme de fusion (facultatif)
Données structurées JSON‐LD pour le schéma `TechArticle` Autres

---

Bon codage et interview-winning! Les