---
Titre: LeetCode 1276. Nombre de Burgers sans déchets d'ingrédients -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1276 – Nombre de Burgers sans déchets d'ingrédients
- Oui. Java • Python • C++ – Solution d'équation linéaire monoligne

> **TL;DR** –
> Le problème se résume à la résolution du système linéaire
> \[
> 4x + 2y = \texttt{tomatoSlices}\quad,\quad x + y = \texttt{cheeseSlices}
> \]
> avec les contraintes que \(x\) (hamburgers jumbo) et \(y\) (petits hamburgers) doivent être ** entiers non négatifs**.
> La solution optimale O(1) est:

Code (O(1))
C'est pas vrai.
**Java**"int public[] numOfBurgers(int TomateSlices, Int fromageSlices) { ... }"
**Python**
*C++** Exclusivité du vector<int> numOfBurgers(int TomateSlices, fromage intercalaireSlices) { ... }"

---

Récapitulation des problèmes (Code de débit 1276)

> **Don** deux entiers :
> - "tomates" (0 ≤ tomates)
> - "fromages" (0 ≤ fromages Tranches ≤ 107)
> **Trouver** le nombre de burgers *jumbo* et *petits* qui utilisent **exactement** tous les ingrédients:
> - Jumbo Burger: 4 tomates + 1 fromage
> - Petit Burger: 2 tomates + 1 fromage
> Retourner `[total_jumbo, total_small]` ou `[]` si c'est impossible.

---

La partie Maths – Bonne partie de la solution

1. **Définir les équations**

«» "
4x + 2y = tomateSlices // usage de la tomate
x + y = fromageSlices // utilisation du fromage
«» "

2. **Solve pour `x` (hamburgers jumbo)* *

«» "
De la seconde: y = fromageSlices - x
Branchez la première :
4x + 2chèces Tranches - x) = tomates Tranches
4x + 2cheeseSlices - 2x = tomateSlices
2x = tomates Tranches - 2 fromages Tranches
x = (tomates Tranches - 2 fromages Tranches) / 2
«» "

3. ** Contrôle des contraintes**

- `tomatoSlices` doit être **même** (autrement `x` n'est pas un entier).
- "x" doit être ≥ 0.
- `y = fromageSlices - x` doit être ≥ 0.

Si toutes les conditions sont réunies, la solution est «[x, y]». Sinon, retourner `[]`.

---

Mise en œuvre

####=1=Java (heure O(1), espace O(1))

"Java
Importation de java.util.*;

solution de classe {
Int[] numOfBurgers(int tomateSlices, fromages d'inte) {
// tomates Les tranches doivent être uniformes.
si (tomates Tranches % 2 != 0) retourner la nouvelle int[0];

int jumbo = tomate Tranches / 2 - fromage Tranches; // x
si (jumbo < 0) retourne une nouvelle int[0];

int small = fromage Tranches - jumbo; // y
si (petite < 0) retourne une nouvelle int[0];

retour de nouveau int[]{jumbo, petit};
}
}
«» "

> **Pourquoi c'est bon** –
> Pas de boucle, juste arithmétique. Gérez instantanément toute la gamme 0–107.

Python (Pythonique O(1))

'`python
Solution de classe:
def numOfBurgers(self, tomateSlices: int, fromageSlices: int) -> Liste[int]:
en cas de tomate Tranches % 2:
retour []
jumbo = tomate Tranches // 2 - fromage Tranches
si jumbo < 0:
retour []
petit = fromage Tranches - jumbo
si petite < 0:
retour []
retour [jumbo, petit]
«» "

C++ (Fast, O(1))

'`cpp
#incluez <vecteur>
utilisant l'espace de noms std;

solution de classe {
public:
vectorielle<int> numOfBurgers(int tomateSlices, fromages intercalairesSlices) {
si (tomatoSlices % 2) retourne {};
int jumbo = tomate Tranches / 2 - fromage Tranches;
si (jumbo < 0) retourne {};
int small = fromage Tranches - jumbo;
si (petite < 0) retour {};
retour {jumbo, petit};
}
};
«» "

---

C'est pas vrai. Liste de contrôle des cas

Autres Tests attendus Raisons
C'est quoi ?
Pas de burgers, pas de déchets
"TomatoSlices = 1, fromageSlices = 0"" "[]" Impossible (tomates od)
"TomatoSlices = 16, fromageSlices = 7"" "[1,6]"
Choux de tomates = 17, fromage Choux = 4'
"TomatoSlices = 4, fromageSlices = 17"

---

Analyse de complexité

Java / Python / C++
-- -- -- -- -- -- -- -- --
Temps **O(1)** – arithmétique constant
Espace **O(1)** – aucune structure de données auxiliaire

---

## Les voies de l'apprentissage

Pourquoi c'est mauvais / Ugly
- C'est quoi ?
**Brute Force** – essayez tous `x` de 0 à `cheeseSlices` et calculez `y`. Autres
**Récursif DFS** – retour sur l'utilisation des ingrédients. Temps exponentiel, risque de débordement. Autres
**Floating Point Math** – résolution des équations avec "double". Erreurs de précision, complexité inutile. Autres

> **À emporter** – Utilisez le raccourci algébrique; pas de boucles, pas de récursion.

---

## -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Catégorie Exemple Leçon
- C'est quoi ?
Solution d'équation linéaire O(1) Pour résoudre le problème de base, il faut réduire mathématiquement la complexité du code et améliorer les performances. Autres
**Contrôler toutes les combinaisons ("pour" boucle) ─ Même si cela fonctionne, il montre un manque de perspicacité et de ressources ; les intervieweurs s'attendent à des maths intelligents. Autres
Quand le problème est une équation simple, quelques lignes de code sont plus propres et plus lisibles. Autres

---

## # SEO-Optimized Blog Post Outline

1. **Titre** – LeetCode 1276 – Nombre de Burgers sans déchets d'ingrédients (Java, Python, C++)
2. **Meta Description** – ♫Solve LeetCode 1276 en moins de 5 minutes avec une solution pure-math O(1). Exemples de code en Java, Python, C++ – parfait pour votre prochaine interview de codage !
3. **Mots clés** – `LeetCode 1276`, `Nombre de Burgers sans déchets d'ingrédients`, `Java solution`, `Python solution`, `C++ solution`, `interview d'équations linéaires`, `codage interview prep`.
4. ** Structure en tête**
- `# LeetCode 1276: Solution mathématique rapide "
- Oui. Énoncé du problème "
- Oui. O(1) Algorithme "
- Oui. Mise en œuvre Java "
- Mise en œuvre de Python "
- Oui. C++ Mise en œuvre "
- Oui. Cas de bord et essais "
- Oui. Bon, le mauvais et le mauvais
- FAQ `##'
- `## Conclusion – Boostez votre jeu d'entrevue "
5. **Rich Snippet** – Ajouter un **Code Block** avec les trois implémentations.
6. ** Liens internes** – Lien vers d'autres solutions LeetCode (p. ex., 1275, 1277) et votre portefeuille.
7. **Call‐to‐Action** – Invitez les lecteurs à télécharger un PDF de la feuille de Cheat Code.

> **Résultat :** Un article bien structuré et riche en mots clés que les moteurs de recherche aiment et que les intervieweurs admirent.

---

À emporter

- **Le calcul est simple** – une équation linéaire, une étape algébrique.
- **La mise en œuvre est banale** – seulement quelques lignes par langue.
- **Le rendement est imbattable** – O(1) temps et espace, pas de boucles.
- **Pour les entrevues** – présenter l'équation, puis donner le code.
J'ai résolu le système analytiquement. (en milliers de dollars)

Bon codage, et peut-être que votre prochaine entrevue n'a aucun déchet d'ingrédients! (en milliers de dollars)