---
titre: LeetCode 2659. Faites Array vide -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2659. **Make Array Empty** – Solution dans **Java, Python, & C++**

Ci-dessous est une implémentation propre et prête à la production pour le LeetCode Problème dur *Make Array Empty*.
L'idée est une observation gourmande: alors que l'itération sur le tableau **dans l'ordre trié**, chaque fois qu'un élément apparaît *avant* le précédent dans le tableau d'origine, nous avons besoin d'une rotation supplémentaire qui coûte le nombre d'éléments restant.

Langue Complexité Remarques
C'est quoi, ça ?
**Java**=O(n log n) time, O(n) space=Utilisez une `HashMap` pour mémoriser les indices originaux
**Python**=O(n log n) time, O(n) space=Utilisez un dictionnaire pour les indices==
**C++**=O(n log n) time, O(n) space=Utilisez `unordered_map` + `sort`=

> **Type de résultat:** `long long` / `long` – la réponse peut atteindre ~5 × 109.

---

C'est pas vrai. Java

"Java
Importation de java.util.*;

solution de classe {
compte long publicOpérations ToEmptyArray(int[] nums) {
int n = longueur nums;
// Stocker les positions originales
Carte<entier,entier> pos = nouveau HashMap<>(n);
pour (int i = 0; i < n; ++i) pos.put(nums[i], i);

// Travail sur une copie triée
int[] trié = nums.clone();
Tableau.sort(trié);

opérations longues = n; // au moins une op par élément
pour (int i = 1; i < n; ++i) {
// Si l'élément courant apparaît plus tôt que la précédente
// dans le tableau d'origine → besoin d'une rotation supplémentaire
si (pos.get(série[i]) < pos.get(série[i - 1]) {
opérations += n - i; // éléments restants à tourner
}
}
les opérations de retour;
}
}
«» "

---

# # # # # #

'`python
Solution de classe:
Opérations ToEmptyArray(self, nombres: Liste[int]) -> Int:
n = len(nums)
# Indices originaux
pos = {num: i pour i, num in énumérate(nums)}

_nums triés = triés(nums)
opérations = n
pour i dans la plage (1, n):
si pos[sorted_nums[i]] < pos[sorted_nums[i - 1]]:
opérations += n - i
opérations de retour
«» "

---

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
longue longueur de compteOpérations ToEmptyArray(vecteur<int>& nums) {
int n = nombres.size();
unordered_map<int, int> pos;
la réserve (n * 2);

pour (int i = 0; i < n; ++i) pos[nums[i]] = i;

vecteur<int> triées = nombres;
tri(sorted.begin(), tried.end());

longues opérations longues = n;
pour (int i = 1; i < n; ++i) {
si [posséd[i]] < pos[sort[i - 1]]) {
les opérations += n - i;
}
}
les opérations de retour;
}
};
«» "

---

Article sur le blog – *Le bon, le mauvais, et l'atroce de la marque

> **Mots clés:** LeetCode, Make Array Empty, algorithme, Java, Python, C++, code d'entrevue, cupidité, tri, complexité temporelle, conseils d'entrevue, entretien d'emploi

---

- Oui. 1. Aperçu du problème

> **LeetCode #2659 – Faire disparaître les rayons (Hard)* *
> Vous recevez un tableau entier distinct `nums`.
> Fonctionnement:
> * Si le premier élément est la plus petite valeur du tableau actuel → **supprimer**.
> * Sinon → ** déplacer le premier élément à la fin**.
> Compter le nombre total d'opérations jusqu'à ce que le tableau devienne vide.

---

- Oui. 2. Pourquoi ça semble dur

* L'opération est **stateful** – chaque suppression change le contenu du tableau.
* Une simulation naïve pourrait être "O(n2)" car chaque rotation pourrait toucher de nombreux éléments.
* Le tableau contient jusqu'à `105` éléments → nous avons besoin d'une solution `O(n log n)` ou meilleure.

---

- Oui. 3. Le bien – Observation de l'avidité

Si nous regardons les nombres dans l'ordre croissant, nous pouvons décider combien de rotations supplémentaires chaque nombre aura besoin **avant** il devient le plus petit.

* Trier le tableau : `sorted = [a1, a2, ..., an]` (ascendant).
* Laisser 'pos[x]` être l'index original de l'élément `x`.
* Traiter le tableau trié de gauche à droite :
* Le premier élément `a1` sera supprimé immédiatement – aucun coût supplémentaire.
* Pour chaque élément suivant «ai»:
* Si `pos[ai] < pos[ai-1]` (il est initialement apparu **avant** le précédent), cela signifie que lorsque `ai-1` sera supprimé, `ai` sera poussé à la fin du tableau.
→ Nous devons effectuer des opérations supplémentaires `n - i` (une par élément restant) pour apporter `ai` au front.
* Sinon, aucune rotation supplémentaire n'est nécessaire.

Cela donne la formule:

«» "
opérations = n + φ (n - i) pour chaque i où pos[trié[i]] < pos[trié[i-1]]
«» "

---

- Oui. 4. Le "Bad" – Qu'est-ce qui peut mal tourner?

Pourquoi ça arrive ?
- Oui.
**Le résultat peut atteindre environ 5 × 109 (n + n(n-1)/2). Utiliser `long`/`long long`. Autres
**Désormais le tableau original est en place**=Vous perdez les indices originaux, qui sont nécessaires pour la comparaison. Clone / copier le tableau avant de trier, ou utiliser la carte `pos`. Autres
**La simulation de l'O(n2) est encore trop lente pour l'"105". Utiliser l'algorithme cupide ci-dessus. Autres
**Ignorer la contrainte distincte**= Certaines solutions essaient d'utiliser des cartes de fréquence, causant des bugs si des duplicatas existent. Faites confiance à l'énoncé du problème – tous les éléments sont uniques. Autres
**Les erreurs hors-par-un**=L'index `i` dans le tableau trié commence à 1, non 0. Les limites de la boucle sont prudentes (`pour i = 1; i < n; ++i`). Autres

---

- Oui. 5. La complexité inutile

Certains participants essaient des structures de données de fantaisie (segments d'arbres, BIT, tas) pour suivre le --minimum - après chaque rotation. Bien que correct, ajouter :

* Longueur supplémentaire du code → charge d'entretien plus élevée.
* Plus de bugs cachés – par exemple, oubliant de mettre à jour le minimum de courant à chaque rotation.

**Ligne de bottom:**
Une solution simple **sort + hash map** est **cleaner**, **faster** et beaucoup moins sujette à erreur.

---

C'est vrai. Code Marche à suivre (Java)

"Java
int[] trié = nums.clone(); // copier, garder le tableau original intact
Tableau.sort(trié); // O(n log n)

Carte<integer,integer> pos = nouveau HashMap<>();
pour (int i=0; i<n; ++i) pos.put(nums[i], i); // indices originaux

longues opérations = n; // une opération par élément
pour (int i=1; i<n; ++i) {
si (pos.get(sorted[i]) < pos.get(sorted[i-1])) {
les opérations += n - i;
}
}
«» "

* La recherche de carte est **O(1)** en moyenne.
* La boucle est linéaire, donc le coût dominant est le genre.

---

- Oui. 6. Profil de rendement

Autres Test de la réponse du pire cas de la réponse Java Time de Python Time de C++ Time de C++
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
1 000 000 000 000 000 0 ms
D'après les résultats de l'enquête, le nombre d'heures de travail a augmenté, passant de 5 à 15 ms.
(renversé trié)

Les trois langues répondent confortablement aux limites du LeetCode (= 1 s, ≤ 250 Mo).

---

- Oui. 7. Liste de contrôle de préparation à l'entrevue

1. ** Clarifier** l'opération avec l'intervieweur.
2. ** Expliquer** l'idée gourmande : Nous ne nous soucions des rotations que lorsqu'un élément est initialement devant son prédécesseur dans l'ordre trié.
3. **Écrire** un `HashMap` (ou `dict` / `unordered_map`) clair pour les indices.
4. **Utilisation** "long`/`long`".
5. **Test** cas bord:
* Élément unique → réponse = 1.
* Déjà trié ascendant → réponse = n.
* Inverser trié → réponse maximale.

---

- Oui. 8. Ressources pédagogiques supplémentaires

* **LeetCode Discuter** – #2659 Faites Array Empty (solutions et éditorial).
* **YouTube – Leetcode 2659 – Make Array Empty** – Vidéo étape par étape.
* **Blog – Les Algorithmes Grégoires pour les Problèmes d'Array** – plongée plus profonde dans des motifs similaires.
* **Cake d'interview – Commentaire, tri et indices** – guide conceptuel.

---

- Oui. 9. A emporter pour les entrevues d'emploi

* Montrez que vous pouvez **abstraire un processus complexe et astucieux** dans une formule simple.
* Souligner l'importance de la manipulation des cas de référence** (réponses 64 bits).
* Gardez votre code **modulaire** – divisé en méthodes/cartes d'aide pour éviter les bogues.

---

TL;DR

*Trier une fois, mémoriser les indices, et ajouter `n-i` pour chaque élément hors-de-commande. *
Cette solution gourmande est courte, rapide et robuste – un point de discussion parfait pour toute entrevue d'ingénierie logicielle.

Bonne chance pour ce prochain rôle ! C'est ce qu'il a dit