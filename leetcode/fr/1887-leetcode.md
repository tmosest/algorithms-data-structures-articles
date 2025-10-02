---
Titre: LeetCode 1887. Opérations de réduction pour rendre les éléments de répartition égaux -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code du leet 1887 – Opérations de réduction pour rendre les éléments de représentation égaux

La complexité temporelle La complexité spatiale Autres
Il s'agit d'un projet pilote.
**O(n log n)**
**O(n log n)**
* * * * * * * * * * * * * * * * * * * * * *

---

TL;DR (Solution en une seule ligne)

"Java
Tableaux.sort(nums);
int ans = 0, prev = nombres[0];
pour (int i = 1; i < nombres de longueur; i++) {
si (nums[i] != prev) { ans += i; prev = nombres[i]; }
}
le retour des an;
«» "

---

- Oui. 1. Récapitulation des problèmes

On vous donne un nombre entier.
Un **opération** est:

1. Trouvez la valeur *la plus grande* (si plusieurs, choisissez la valeur la plus à gauche).
2. Réduisez cet élément à la valeur *plus petite* suivante.
3. Répéter jusqu'à ce que chaque élément soit égal.

Retourner le nombre total d'opérations nécessaires.

---

- Oui. 2. Intuition et observation clé

Pensez au tableau trié **de plus en plus**:

«» "
[1, 3, 5] → triés : [1, 3, 5]
«» "

* Chaque fois que la valeur change, tous les éléments *à gauche* sont strictement plus petits.
L'élément qui a provoqué le changement sera réduit *exactement une fois* pour devenir égal à la valeur de gauche.

Ainsi, pour chaque indice `i` où `nums[i]!= nums[i‐1]`, nous ajoutons `i` opérations.
L'ajout de tous ces nombres Jump donne la réponse.

---

- Oui. 3. Pièges de l'affaire Edge

Autres Décision Qu'est-ce qui peut mal tourner ? Comment l'éviter
-- -- -- -- -- -- -- -- -- --
Autres Tous les éléments égaux peuvent compter incorrectement les transitions. Autres
La boucle commence à "i = 1"
Dupliquer les valeurs dispersées Dupliquer l'ordre des poignées; les duplicatas deviennent contigus

---

- Oui. 4. Analyse de la complexité

Étape Coût
- Oui.
Classer le tableau **O(n log n)**
* * * * * * * * * Autres
L'espace supplémentaire La copie d'array (tri en place) → **O(1)** (Java's `Arrays.sort' est en place)

Généralités: **Heure** `O(n log n)` **Espace** `O(1)` (ou `O(n)` si vous copiez).

---

- Oui. 5. Mise en œuvre dans trois langues

#### 5.1 Java

"Java
Importer java.util. Les tableaux;

solution de classe publique {
réduction de l'activité publique
Tableaux.sort(nums); // O(n log n)
Int ops = 0;
int prev = nombres[0];
pour (int i = 1; i < nombres de longueur; i++) {
si (nums[i] != prev) {
ops += i; // tous les éléments avant i sont plus petits
prev = nombres[i];
}
}
les opérations de retour;
}
}
«» "

5.2 Python

'`python
Solution de classe:
def reductionOperations(self, nombres: list[int]) -> Int:
nombres.sort() # O(n log n)
ops = 0
prev = nombres[0]
pour i dans la plage(1, len(nums)):
si nombres != Prév:
Opérations += i # tous les éléments avant que je ne sois plus petit
prev = nombres[i]
retour ops
«» "

C++

'`cpp
#incluez <algorithme>
#incluez <vecteur>

solution de classe {
public:
la réduction de l'int.
à:sort(nums.begin(), nums.end(); // O(n log n)
Int ops = 0;
int prev = nombres[0];
pour (size_t i = 1; i < nums.size(); ++i) {
si (nums[i] != prev) {
ops += static_cast<int>(i); // tous les éléments avant i sont plus petits
prev = nombres[i];
}
}
les opérations de retour;
}
};
«» "

---

- Oui. 6. Vue alternative: Utilisation de la carte de fréquence

Si vous préférez ne pas trier le tableau entier, vous pouvez :

1. Construire une carte de fréquence (`TreeMap` en Java, `SortedDict` en Python, ou `std::map` en C++).
2. Traverser les touches dans l'ordre **descendant**, maintenir une somme suffisante de comptes, l'ajouter à la réponse pour chaque touche sauf la plus petite.

Cela donne le même temps `O(n log n)` mais peut être plus clair lorsque vous travaillez déjà avec un multiset.

---

- Oui. 7. Pourquoi cela est un grand problème d'entrevue

1. **Shows Compréhension du tri et préfixe Somme** – Beaucoup d'intervieweurs recherchent la capacité du candidat à transformer un problème en une vue préfixe triée.
2. **Edge‐Case Sensibility** – Manipulation de tableaux avec tous les éléments égaux ou singletons teste l'attention au détail.
3. ** Solutions multiples** – Vous pouvez discuter à la fois de l'approche de saut de tableau trié et de l'approche de suffixe de carte de fréquence, en soulignant les compromis.

---

- Oui. 8. SEO–Résumé amical

- **Mots-clés**: *Code d'accès 1887*, *Opérations de réduction*, *Faire des éléments de tableau égaux*, *solution de Java*, *solution de Python*, *solution de C++*, *entrevue d'algorithme*, *codage interview prep*, *O(n log n*), *tableau trié*.
- **Méta-Description**: Apprendre à résoudre le LeetCode 1887 – Opérations de réduction pour rendre les éléments de répartition égaux. Afficher les implémentations Java, Python et C++ ainsi qu'un blog en profondeur expliquant l'algorithme, les cas de bord et les conseils d'entrevue. (en milliers de dollars)

---

La pensée finale

La clé de *LeetCode 1887* est de reconnaître que chaque jump du tableau trié nous indique exactement combien de réductions sont nécessaires. Un simple laissez-passer après tri donne une solution élégante et optimale qui impressionnera les intervieweurs et vous rapprochera de votre travail de rêve. Bon codage !