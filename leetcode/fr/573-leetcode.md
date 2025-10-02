---
titre: LeetCode 573. Simulation de l'écureuil -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 573. Simulation de l'écureuil
**Difficulté:** Moyenne
**URL du code leet:** <https://leetcode.com/problèmes/squirrel-simulation/>

> **Objectif** – L'écureuil commence à une cellule donnée, doit ramasser *tous* noix un par un, déposer chaque noix sous l'arbre et enfin revenir à l'arbre.
> **Mouvement** – Quatre directions seulement (en haut, en bas, à gauche, à droite).
> ** Sortie** – Nombre minimum de mouvements requis.

---

# # # # Une perspective fondamentale

Quand vous prenez un écrou, vous devez toujours marcher:

1. **De l'arbre à la noix** (ou de l'écureuil à la noix si elle est la première).
2. **De l'écrou à l'arbre** pour le déposer.

Si nous additionnons naïvement *2 × distance (noix, arbre)* pour chaque écrou, nous additionnons la jambe que l'écureuil prend *premier* de sa position de départ à la première écrou.
Le mieux que nous pouvons faire est de choisir l'écrou qui donne le plus grand *épargne*:

«» "
épargne = distance (noix, arbre) – distance (noix, écureuil)
«» "

La distance minimale est donc:

«» "
total = 2 × distance (noix, arbre)
minimum = total – max(économie)
«» "

Cette formule fonctionne dans **O(n)** temps et **O(1)** espace supplémentaire.

---

Mise en œuvre

Ci-dessous vous trouverez trois solutions propres et prêtes à la production – une dans **Java**, **Python** et **C++**.
Tous utilisent la même aide à distance de Manhattan.

### Java

"Java
solution de classe publique {
intérieur public minDistance(hauteur de l'int, largeur de l'int,
arbre int, écureuil int,
Int[][] noix) {
= 0;
int maxSaving = entier.MIN_VALUE;

pour (int[] noix : noix) {
Dist. ToTree = manhattan (noix, arbre);
Dist. ToSquirrel = manhattan (noix, écureuil);

Total += dist À l ' ordre du jour* 2;
maxSaving = Math.max(maxSaving, distToTree - distToSquirrel);
}

total de retour - maxSaving;
}

Int privé manhattan(int[] a, int[] b) {
retourner Math.abs(a[0] - b[0]) + Math.abs(a[1] - b[1]);
}
}
«» "

Python

'`python
Solution de classe:
def minDistance(même, hauteur: int, largeur: int,
arbre: Liste[int], écureuil: Liste[int],
noix: Liste[List[int]]) -> Int:
Total = 0
max_saving = flotteur('-inf')

pour les noix:
dist_tree = self._manhattan(noix, arbre)
dist_squirrel = self._manhattan(noix, écureuil)

Total += 2 * dist_tre
max_saving = max(max_saving, dist_tree - l'écureuil)

retour total - _économie maximale

@staticmethod
def _manhattan(a: List[int], b: List[int]) -> Int:
abs(a[0] - b[0]) + abs(a[1] - b[1])
«» "

C++

'`cpp
solution de classe {
public:
int minDistance(hauteur de l'int, largeur de l'int,
vectorielle<int>&arbre, vectorielle<int>&écureuil,
vecteur<vecteur<int>>& noix) {
long total = 0; // utiliser long pour éviter le débordement
long maxSauvage = LLONG_MIN;

pour (const auto & écrou : noix) {
longue longue dist Arbre = manhattan (noix, arbre);
longue distSquirrel = manhattan(noix, écureuil);

Total += 2 * dist Arbre;
maxSaving = max(maxSaving, distTree - distSquirrel);
}
retourner static_cast<int>(total - maxSaving);
}

particulier:
long long manhattan (vecteur Const<int>& a, vecteur Const<int>& b) const {
retourner les labs(a[0] - b[0]) + les labs(a[1] - b[1]);
}
};
«» "

---

Article du blog – Simulation de l'écureuil : le bon, le mauvais et le mauvais

> **Références clés:** *Squirrel Simulation LeetCode*, *minAlgorithme de distance*, *Java Python C++ solution*, *problème de codage de l'entrevue*, *Distance manhattan*, *conception de l'algorithme*

---

- Oui. 1. Présentation

Le problème **Squirrel Simulation** est un élément essentiel du LeetCode pour ceux qui se préparent à des entrevues de codage. Il vous demande de trouver le nombre minimal de mouvements qu'un écureuil doit faire pour recueillir toutes les noix et les déposer sous un arbre, en se déplaçant seulement vers le haut, vers le bas, vers la gauche ou vers la droite. Bien que la déclaration soit fantaisiste, elle touche en fait aux concepts algorithmiques classiques : **Distance manhattan** et **optimisation en forme**.

- Oui. 2. Pourquoi ce problème se pose

- ** Contraintes claires** – Pas d'obstacles, seulement des limites de grille.
- **Pas besoin de BFS** – Comme il n'y a pas d'obstacles, la distance de Manhattan est exacte.
- **O(n) Solution** – Un seul passage dans la liste des écrous vous donne la réponse instantanément.

- Oui. 3. La Solution Élégante – -Le Bon

Ce qui arrive Pourquoi ça marche
- C'est quoi ?
Autres Calculer **dist (noix, arbre)** pour chaque noix. Autres
Autres Sum "2 * dist(noix, arbre)". On double parce que chaque écrou a besoin d'un aller-retour. Autres
Calculer **sauvegarder** = `dist(noix, arbre) – dist(noix, écureuil)`. Si nous commençons avec cette noix, nous remplaçons la jambe *tree → noix* par *squirrel → noix*. Autres
Autres Soustrayez le plus grand **économie** du total. C'est le meilleur premier écrou possible; tous les autres écrous restent sur le modèle aller-retour. Autres

> **Résultat** – Un nombre minimal de mouvements dans le temps linéaire et l'espace supplémentaire constant.

- Oui. 4. Edge Cases et Gotchas – Le mal

- **Grandes entrées** – Avec jusqu'à 5000 écrous, le débordement entier peut s'infiltrer. Utilisez `long' en C++ ou `long` en Java/Python `int` (qui n'est pas lié) en toute sécurité.
- ** Cellules inaccessibles** – Le problème garantit que chaque écrou et l'arbre sont à l'intérieur des limites, de sorte qu'aucune recherche de chemin n'est nécessaire. Si le problème changeait pour inclure des obstacles, le simple raccourci de Manhattan serait invalide.
- **Coordonnées négatives** – Selon les contraintes, les coordonnées ne sont pas négatives, mais une mise en œuvre devrait être suffisamment robuste pour gérer les valeurs entières.

- Oui. 5. Quand les choses deviennent messies – Le Ugly

Si vous deviez aborder une variante où l'écureuil ne peut traverser certaines cellules (par exemple, des trous ou de l'eau), le raccourci de Manhattan se décompose. Vous auriez besoin :

1. **Computation du chemin le plus court** – BFS de chaque écrou à l'arbre et de l'écureuil à chaque écrou, qui est O(n · (h·w)).
2. ** Programmation dynamique ou FST** – Le problème se transforme en une variante du vendeur itinérant, qui est NP‐hard.

Ainsi, alors que le problème de Simulation d'écureuil est un outil d'enseignement merveilleux, l'étendre sans soins s'enroule rapidement en territoire de complexité.

- Oui. 6. Pourquoi vous devriez aimer la solution

- **Simplicité** – Une seule boucle, une méthode d'aide et un peu de maths.
- **Performance** – Exécute en microsecondes sur des piles d'entrevue typiques.
- **Adaptabilité** – Le motif (double compte + soustraire l'épargne maximale) apparaît dans d'autres problèmes de collecte et de retour.

- Oui. 7. A emporter pour des entrevues de travail

- ** Mettre en avant l'argument de Greedy** – Expliquez pourquoi choisir l'écrou avec un maximum d'économie donne le premier mouvement optimal.
- **Talk About Complexity** – O(n) time, O(1) espace est un excellent point de vente.
- **Afficher la polyvalence du langage** – Fournir des solutions en Java, Python et C++ pour démontrer l'ampleur.

---

Conclusion

Le problème de simulation de l'écureuil est un exemple brillant de la façon dont un défi apparemment ludique peut illustrer une pensée algorithmique puissante. En exploitant les distances de Manhattan et un ajustement avide intelligent, nous obtenons une solution à la fois élégante et efficace.

Que vous soyez en train de polir votre préparation d'entrevue, de concevoir un projet de portfolio ou simplement de profiter de la joie du codage, ce problème et sa solution offrent un mélange délicieux de clarté, de défi et de maîtrise.

Bon codage – et que vos écureuils collectent toujours les noix de la manière la plus courte possible!