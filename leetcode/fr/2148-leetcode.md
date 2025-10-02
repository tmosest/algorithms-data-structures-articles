---
titre: LeetCode 2148. Éléments de comptage avec des éléments strictement plus petits et plus grands -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

## LeetCode 2148: Éléments de compte avec des éléments strictement plus petits et plus grands
*Le bon, le mauvais et l'hugly – Java

**Méta—Description**
Découvrez comment résoudre le LeetCode 2148 en temps O(N) avec une solution d'espace O(1) propre. Obtenez le code Java, Python et C++, une explication en profondeur, une discussion de cas de bord, et un billet de blog convivial SEO qui vous aidera à ace vos interviews de codage et atterrir votre travail de rêve.

---

Déclaration du problème (Code de bord 2148)

> **Count des éléments avec des éléments strictement plus petits et plus grands**
> **Difficulté:** Facile
> **Constraints**
1 ≤ longueur nominale ≤ 100
> -105 ≤ nums[i] ≤ 105

> **Grâce** à un tableau entier `nums`, retournez le nombre d'éléments qui ont *deux* un strictement plus petit **et** un élément strictement plus grand présent quelque part dans le tableau.

> **Exemple**
> `` "
> Entrée: nombres = [11, 7, 2, 15]
> Produit: 2
> Explication: 7 et 11 satisfont à la condition.
> `` "

---

- Oui. Pourquoi ce problème est-il une grande interview

- **Low-Complexity & Conceptual Profondeur** L'astuce consiste à reconnaître que *seulement la matière minimale et maximale globale*.
- **Edge‐Case Handling** – Des doublons, des tableaux tout-égal ou des tableaux à éléments uniques testent votre compréhension de « strictement » par rapport à « non-strict ».
- **Approche linguistique-agnostique** – La même logique se traduit par Java, Python, C++ ou même JavaScript.

---

## Description de la solution (bon)

1. **Trouver le minimum global (`minVal`) et le maximum (`maxVal`)** en un seul passage.
2. **Couvercle des éléments qui se situent strictement entre** `minVal` et `maxVal`.
- Un élément `x` est admissible si `minVal < x < maxVal`.
3. Rendez le compte.

> **Pourquoi c'est "Good"* *
> *Temps linéaire*, *espace supplémentaire constant* et *pas de tri* – l'approche la plus efficace.

---

Pièges communs

Pièges à quoi ça ressemble
C'est ce qu'on dit.
**Désorceler le tableau**= Utiliser `Arrays.sort()` puis itérer – ajoute le temps O(N log N) inutilement. Passer le tri; juste suivre min & max. Autres
**Utiliser `<=` au lieu de `<`**" Compte les éléments égaux à `minVal` ou `maxVal` par erreur. Comparer strictement avec `<` et `>`. Autres
**Ignorer les duplicata** Traitement indépendant de chaque événement. Autres

---

Cas de bords (en général)

- **Tous les éléments sont égaux** → `count = 0`.
- **Un seul élément** → `count = 0`.
- **Tableau de deux éléments** → `count = 0` (aucun élément ne peut avoir les deux côtés).
- ** Nombres négatifs** – la logique min et max tient toujours.
- **Grand nombre** (±105) – aucun risque de débordement avec `int` en Java/C++ ou `int` en Python.

---

Mise en œuvre du code

C'est pas vrai. Java (optionnel + facile)

"Java
solution de classe publique {
Le nombre d'entrées dans le secteur public comprend les éléments suivants: {
int minVal = entier.MAX_VALUE;
Int max Val = entier.MIN_VALUE;

// Premier passage: trouver min & max
pour (int num : nombres) {
si (num < minVal) minVal = num;
si (num > maxVal) maxVal = num;
}

// Deuxième passe: compter strictement entre
nombre int = 0;
pour (int num : nombres) {
si (num > minVal && num < maxVal) count++;
}
le nombre de retours;
}
}
«» "

> **Complexité** – temps « O(n) », espace auxiliaire « O(1) ».

---

# # # # # #

'`python
Solution de classe:
def countElements(self, nombres: List[int]) -> Int:
min_val = min(nums)
max_val = max(nums)

retour de somme(1 pour x en nombres si min_val < x < max_val)
«» "

> **Complexité** – temps `O(n)`, espace `O(1)` (à part la liste des entrées).

---

C'est vrai. C++

'`cpp
solution de classe {
public:
nombre d'éléments(vecteur<int> et nombres) {
int minVal = INT_MAX;
Int max Val = INT_MIN;

pour (int x : nombres) {
minVal = min(minVal, x);
maxVal = max(maxVal, x);
}

cnt = 0;
pour (int x : nombres) {
si (x > minVal && x < maxVal) cnt++;
}
retour cnt;
}
};
«» "

> **Complexité** – temps « O(n) », espace auxiliaire « O(1) ».

---

Comment expliquer Ceci dans une entrevue d'emploi

1. **Énoncer clairement le problème** – Mentionnez le besoin d'éléments * strictement plus petits* et * strictement plus grands*.
2. **Exposer l'observation** – Seulement la matière globale min et max; tout élément en dehors de cette plage ne peut pas satisfaire la condition.
3. **Afficher l'algorithme à deux passes** – Parlez des compromis temps/espace.
4. **Cas d'Address Edge** – Mettre en évidence des duplicatas, des tableaux à éléments uniques, etc.
5. **Optionnel** – Mention qu'une seule passe est possible avec une stratégie `minSeen` et `maxSeen` mais deux passes sont plus simples et parfaitement acceptables pour `n ≤ 100`.

---

Résumé optimisé du SEO

Mot-clé
C'est quoi ?
Titre, rubriques, introduction
Description du problème
Autres Solution Java LeetCode 2148.
Solution Python LeetCode 2148
Solution C++ LeetCode 2148
LeetCode question d'entretien
La complexité de l'algorithme
Codage des conseils d'entrevue Conclusion
Structures de données

> **Étiquette de référence pour le référencement final**
> **Master LeetCode 2148 avec des solutions Java, Python et C++ – rapides, propres et prêtes à l'entretien.*

---

Enveloppe

- **Bien**: Temps linéaire, espace constant, pas de tri.
- **Bad**: Suringénierie avec tri ou utilisation abusive des opérateurs de comparaison.
- **Ugly**: Oublier les duplicatas ou la manipulation des caisses de bord.

Implémentez l'approche simple à deux passes et vous obtiendrez la solution parfaite à chaque fois – prêt pour votre prochaine entrevue de codage ou pour impressionner votre gestionnaire d'embauche.

Bon codage ! C'est ce qu'il a dit