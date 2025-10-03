---
titre: LeetCode 2126. Détruire les astéroïdes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

# Détruire les astéroïdes – 2126. LeetCode – Un problème d'entrevue de préparation à l'emploi

**Mots clés:** LeetCode 2126, Détruire les astéroïdes, Algorithme de Greedy, Tri, Tableau de fréquences, Java, Python, C++, Préparation de l'entrevue, Entretien de génie logiciel, Structures de données, Conception de l'algorithme

---

- Oui. 1. Aperçu du problème

On vous donne une "masse" entière – la masse initiale d'une planète – et un tableau "astéroïdes" où "astéroïdes[i]" est la masse de l'astéroïde *i*.
La planète peut entrer en collision avec les astéroïdes dans **n'importe quel ordre**.
* Si la masse actuelle de la planète est **≥** la masse de l'astéroïde, l'astéroïde est détruit et sa masse est ajoutée à la planète.
* Si la masse de la planète est **<** la masse de l'astéroïde, la planète est détruite.

**Retour** `true` s'il est possible de détruire *tous* astéroïdes, sinon `faux`.

**Contrôles* *

Variable
C'est quoi ?
"masse" 1 ... 10 <sup>5 </sup>
1 ... 10<sup>5</sup>
1 ... 10 <sup>5 </sup>

---

- Oui. 2. Intuition

Pour grandir aussi vite que possible, vous devez toujours absorber l'astéroïde *le plus petit* que la planète peut actuellement vaincre.
Si vous absorbez d'abord un astéroïde plus gros, vous risquez de manquer la chance de grandir suffisamment pour en prendre un peu plus tard.

Ainsi, la stratégie optimale est:

1. **Trier** les masses d'astéroïdes dans l'ordre ascendant.
2. Itérer à travers la liste triée, en ajoutant chaque masse d'astéroïde à la masse de la planète.
3. Si à tout moment la planète ne peut pas absorber l'astéroïde actuel, vous ne pouvez jamais l'absorber plus tard (parce que tous les astéroïdes restants sont égaux ou plus grands).

Cette stratégie gourmande garantit que si une solution existe, vous la trouverez.

---

- Oui. 3. Algorithme (gredi + tri)

«» "
Tri(astéroïdes) // ascendant
pour chacun des astéroïdes:
si masse >= a:
masse += a
Sinon:
retourner faux
retour vrai
«» "

**Pourquoi ça marche* *

- Oui. La masse de la planète augmente seulement quand elle absorbe avec succès un astéroïde.
- Oui. Le plus petit astéroïde restant est le plus facile à absorber ; si vous ne pouvez pas l'absorber, vous ne pouvez pas absorber n'importe quel plus grand.
- Absorber la plus petite première ne peut qu'augmenter la masse de la planète, jamais la diminuer, donc le choix avide est sûr.

---

- Oui. 4. Analyse de la complexité

Métrique Temps Espace
- Oui.
(où *n* = `astéroïdes.longueur`) Autres
Itération
Total des dépenses

> **Note :**
> Si les masses d'astéroïdes sont limitées par une petite constante (=10<sup>5</sup>), un tri *counting* (`O(n + maxMass)`) peut réduire le temps à linéaire, mais le tri classique est plus simple et assez rapide pour les limites données.

---

- Oui. 5. Cas de bord

Motif
C'est quoi ?
**Mass déjà ≥ tous les astéroïdes**La boucle absorbera tous; retourner `true`. Autres
**Un seul astéroïde plus lourd que la masse** Autres
Une fois que vous échouez sur un, vous échouerez sur tous ceux identiques. Autres
**Mass ou taille d'astéroïde jusqu'à 10<sup>5</sup>**=Utilisez `long` (Java) ou `long` (C++) pour éviter les débordements en remuant de nombreux astéroïdes. Autres

---

- Oui. 6. Mise en œuvre du code

Voici des implémentations propres, prêtes à l'interview dans **Java**, **Python** et **C++**. Chacun suit la stratégie de tri cupide + et comprend des commentaires pour plus de clarté.

#### 6.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
***
* Déterminer si la planète peut détruire tous les astéroïdes.
*
* Masse de @param masse de la planète initiale
* @param astéroïdes tableau de masses d'astéroïdes
* @retour vrai si tous les astéroïdes peuvent être détruits, faux sinon
*/
astéroïdes booléens publics Détruit(masse d'int, astéroïdes int[]) {
// Tri en ordre croissant
Arrays.sort(astéroïdes);

long courant Masse = masse; // Utilisez longtemps pour éviter le débordement

pour (int a : astéroïdes) {
si (courantMass >= a) {
actuel Masse += a;
} autre {
retourner faux; // Ne peut pas absorber cet astéroïde
}
}
retour vrai; // Tous les astéroïdes détruits
}
}
«» "

6.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def astéroïdes Détruyed(self, masse: int, astéroïdes: List[int]) -> bool:
"""
Solution d'avidité : absorber le plus petit astéroïde que vous pouvez.
"""
astéroïdes.sort() # En croissant
courant = masse

pour les astéroïdes:
si courant >= a:
courant += a
Sinon:
Retour Faux
retour Vrai
«» "

*### 6.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
les astéroïdes bool Détruit(masse d'int, vecteur<int> et astéroïdes) {
tri(astéroïdes.degin(), astéroïdes.end()); // Accent
long cur = masse; // 64-bit pour éviter le débordement

pour (int a : astéroïdes) {
si (cur >= a) cur += a;
sinon retourner faux;
}
retour vrai;
}
};
«» "

> **Conseil pour les entrevues:**
> Expliquez que vous utilisez des nombres entiers `long` (C++), `long` (Java) ou Python=s pour gérer la masse cumulative en toute sécurité.

---

- Oui. 7. Les bons, les mauvais et les méchants

Aspect du bien
- C'est quoi ?
**Sobriété algorithmique**=Le sort Greedy + est intuitif et facile à expliquer. Il faut trier, qui est *O(n log n)*. Autres
Autres **Complexité du temps**= Assez rapide pour 10<sup>5</sup> éléments. Le tri peut être considéré comme trop qualifié si vous savez que les données sont déjà triées. L'utilisation d'une structure de données inefficace (p. ex. file d'attente prioritaire avec suppressions répétées) peut ajouter des frais généraux inutiles. Autres
Autres **Utilisation de l'espace**= Tri en place → O(1) supplémentaire.=Le tri modifie le tableau d'entrée – peut être indésirable si le tableau doit rester inchangé.== Ne pas utiliser un genre de comptage quand `maxMass` est petit; vous perdez du temps à trier un énorme tableau. Autres
**Manipulation de l'Edge** Aucun.
**Clarté du code** Nécessite une brève explication de pourquoi l'avidité fonctionne. Le surmenage peut encombrer la solution. Autres

**À emporter :** La solution de triage et d'avidité est la façon de "bien". Si vous interviewez dans une entreprise technologique qui valorise *vitesse* et *simplicité*, expliquez l'intuition, montrez le code, et vous gagnerez l'entrevue.

---

- Oui. 8. Fermeture optimisée par le SEO

*Si vous êtes à la recherche d'un emploi dans le génie logiciel, maîtriser des problèmes d'entrevue comme **Détruire des astéroïdes** démontre votre capacité à appliquer des algorithmes gourmands et la raison sur des stratégies optimales. Pratiquer de tels problèmes LeetCode renforce vos compétences de résolution de problèmes, fait votre CV se démarquer, et montre aux gestionnaires d'embauche que vous pouvez écrire un code propre et efficace dans **Java**, **Python** ou **C++**.*

> **Prêt à conquérir la prochaine entrevue de codage? * *
> - Pratiquer les problèmes gourmands: Région arrondie, région maximum, région de fond
> - Construisez un projet personnel qui utilise la logique de tri et d'avidité (par exemple, un jeu simple AI).
> - Gardez une repo GitHub avec des solutions annotées – recruteurs aiment voir le vrai code.

Bon codage, et bonne chance pour votre prochaine interview!

---