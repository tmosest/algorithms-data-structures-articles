---
titre: LeetCode 2428. Somme maximale d'un hourglass -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2428. Somme maximale d'un hourglass – 3-Way Solutions + SEO-Optimized Blog

> **Objectif** – Résoudre le problème de LeetCode *Somme maximale d'un hourglass* en **Java**, **Python** et **C++**.
> **Bonus** – Un billet de blog convivial pour le référencement qui explique le bon, le mauvais et le mauvais problème, vous aide à interviewer et améliore votre présence en ligne.

---

- Oui. 1. Le Code

> **Les trois implémentations se déroulent dans le temps O(m × n) et l'espace auxiliaire O(1)** – parfait pour les contraintes d'entrevue.

#### 1.1 Java

"Java
// 2428. Somme maximale d'un hourglass – Java (temps O(m*n), espace O(1))
solution de classe {
int public maxSum(int[[]] grille) {
int m = longueur de grille, n = longueur de grille[0];
int best = 0; // Toutes les valeurs sont non négatives
pour (int i = 1; i < m - 1; i++) { // Ligne moyenne de sablier
pour (int j = 1; j < n - 1; j++) { // Colonne médiane
int sum = grille[i-1][j-1] + grille[i-1][j] + grille[i-1][j+1]
+ grille[i][j]
+ grille[i+1][j-1] + grille[i+1][j] + grille[i+1][j+1];
best = Math.max (best, sum);
}
}
le meilleur retour;
}
}
«» "

> *Pourquoi ça marche*: Nous itérer sur chaque centre possible d'un sablier (c.-à-d. l'élément central). Le sablier est toujours 3×3, donc la somme est un motif fixe. Pas de structures de données supplémentaires nécessaires.

#### 1.2 Python

'`python
# 2428. Somme maximale d'un hourglass – Python (temps O(m*n), espace O(1))
Solution de classe:
def maxSum(self, grille: List[List[int]]) -> Int:
m, n = len(grid), len(grid[0])
meilleur = 0
pour i à portée (1, m - 1):
pour j dans la plage(1, n - 1):
s = (
quadrillage[i-1][j-1] + quadrillage[i-1][j] + quadrillage[i-1][j+1]
+ grille[i][j]
+ grille[i+1][j-1] + grille[i+1][j] + grille[i+1][j+1]
)
best = max (meilleur, s)
le meilleur retour
«» "

> *Astuce pyronique*: Utilisez `range(1, m-1)` pour sauter les lignes de bordure/cols qui ne peuvent accueillir un sablier.

*## 1.3 C++

'`cpp
// 2428. Somme maximale d'un sablier – C++ (temps O(m*n), espace O(1))
solution de classe {
public:
int maxSum(vecteur<vecteur<int>>& grille) {
int m = quadrillage(), n = quadrillage[0].size();
int best = 0; // tous les éléments >= 0
pour (int i = 1; i < m - 1; ++i) { // rang moyen
pour (int j = 1; j < n - 1; ++j) { //
somme int =
quadrillage[i-1][j-1] + quadrillage[i-1][j] + quadrillage[i-1][j+1] +
du réseau [i][j] +
quadrillage[i+1][j-1] + quadrillage[i+1][j] + quadrillage[i+1][j+1];
best = max (meilleure somme);
}
}
le meilleur retour;
}
};
«» "

> *Pourquoi c'est rapide*: Pas d'allocation de mémoire dynamique, juste simple entier arithmétique.

---

- Oui. 2. Article de blog optimisé SEO

> **Titre**: Le bon, le mauvais et le mauvais de résoudre le leetCode 2428 – *Somme maximale d'un hourglass*
> **Méta-Description**: Maîtrisez le problème de sablier LeetCode 2428 en Java, Python et C++. Apprenez les meilleures pratiques, les pièges communs et les stratégies d'entrevue pour établir votre prochain rôle d'ingénierie logicielle.
> **Mots-clés**: LeetCode 2428, Somme maximale d'un hourglass, codage d'entrevue, entretien d'emploi, algorithme, Java, Python, C++, codage d'entrevue, structure des données, complexité temporelle, complexité spatiale.

---

Aperçu du problème

LeetCode 2428 vous demande de calculer la somme maximale d'une matrice *m × n* :

«» "
a b c
d
e f g
«» "

* Un sablier ne peut pas être tourné.
* Elle doit s'intégrer entièrement à la matrice.
* Toutes les valeurs sont non négatives (0 ≤ grille[i][j] ≤ 106).

**Contrôles* *
3 ≤ m, n ≤ 150 → ≤ 22500 cellules → simples boucles imbriquées sont assez rapides.

---

Le bon – Une approche propre et prête à l'entrevue

1. **Indices de boucle intuitifs**
* Itérer au-dessus du *centre* `(i, j)` de chaque sablier: `i [1, m-2]`, `j [1, n-2]`.
* Cela exclut automatiquement les cellules frontalières qui ne peuvent accueillir un sablier complet.

2. ** Calcul de la somme directe* *
* Calculer les 7 cellules explicitement; pas de structures de données supplémentaires.
* `sum = haut Ligne + milieu + bas Ligne.

3. **Espace auxiliaire continu**
* Seulement quelques variables entières (`best`, `sum`).
* Parfait pour les intervieweurs à la recherche d'un code d'efficacité spatiale.

4. **Sécurité des caisses**
* Parce que toutes les valeurs sont non négatives, initialiser `meilleur = 0' fonctionne.
* Si des négatifs étaient autorisés, définissez `meilleur = INT_MIN` / `-inf`.

5. **Complexité temporelle**
* `O(m × n)` – chaque cellule est considérée comme un nombre constant de fois.
* Avec *m, n* ≤ 150, le pire des cas est 22 500 itérations – trivial.

---

Les mauvaises – Pièges communs

Pourquoi il échoue
- C'est quoi ?
**Incluant les cellules frontalières**=Essai d'accès à `grid[i-1][j-1]` lorsque `i=0` ou `j=0` → `ArrayIndexOutOfBounds`.=Loop `i` de `1` à `m-2`; `j` de `1` à `n-2`. Autres
**L'hypothèse de valeurs négatives**L'initialisation `meilleur = 0` donne une réponse erronée si tous les nombres sont négatifs. Initialiser `-inf` ou `INT_MIN`. Autres
**Utiliser l'espace O(n2)**= Pré-calculer les montants ou une table DP sans intérêt; gâcher la mémoire. Stick à l'espace constant. Autres
**Ne pas manipuler de gros ints** Utilisez `long` si vous prévoyez des sommes > 231-1 (pas nécessaire ici). Autres

---

### Les pièges d'optimisation

1. ** Préfixer la surcapacité de somme**
* Certaines solutions pré-calculent une somme de préfixe 2D puis glissent une fenêtre.
* Bien que cela fonctionne, il ajoute *O(m × n)* espace et une boucle de 2 niveaux pour chaque sablier – inutile.

2. **Brute-Force récursive**
* Récurer régulièrement sur la grille pour choisir 7 cellules est à la fois lent et empilé.
* Les intervieweurs s'attendent à ce qu'il y ait une boucle **.

3. **Loop intérieur micro-optimisant**
* Utilisation de tableaux temporaires pour maintenir les tranches de rangée.
* Complète le code sans gain de vitesse mesurable dans cette taille.

**Ligne de bottom:** La simplicité gagne. Les intervieweurs apprécient le code propre et lisible qui résout le problème dans les limites des contraintes.

---

#### ♫ Takeaways pour l'entrevue de travail

Pourquoi ça compte ?
- Oui.
**Exposer les limites de la boucle** Autres
**La complexité du temps et de l'espace de Mention** Démontre la pensée algorithmique. Autres
**Afficher la conscience des cas de bord** Autres
**Discuse pourquoi tu as choisi cette solution** Autres
**Découvrez les tests**. Autres

**Conseil:** Après avoir écrit la solution, passez par un exemple rapide avec une petite matrice. Les intervieweurs aiment voir le code en action.

---

Ressources supplémentaires

- [Problème de code leet 2428 – Somme maximale d'un hourglass] (https://leetcode.com/problèmes/somme maximale d'un hourglass/)
- [Discussion Threads (Java/Python/C++)] (https://leetcode.com/problèmes/maximum-sum-of-an-heureglass/solutions/)
- [Interview Warm-Up: 2-D Array Problems] (https://www.educative.io/courses/leetcode-interview-préparation/4)

---

Mot final

Résoudre *La somme maximale d'un hourglass* est une victoire rapide pour votre boîte à outils d'entrevue.
- **Java**: Montrez la maîtrise des tableaux et des boucles.
- **Python**: Mettre en évidence la syntaxe concise et la lisibilité.
- **C++**: Démontrer la sensibilisation aux performances et l'utilisation de STL.

Utilisez cette solution, parlez à travers le bon, mauvais, laid, et vous impressionnerez n'importe quel interviewer, que vous postuliez à une startup ou à une entreprise Fortune 500.

Bon codage et bonne chance pour votre prochaine chasse au travail! C'est ce qu'il a dit