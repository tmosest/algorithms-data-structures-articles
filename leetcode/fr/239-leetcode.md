---
titre: LeetCode 239. - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Exposé des problèmes* *
Avec un tableau entier `nums` et un entier `k`, retournez un tableau contenant la valeur maximale de chaque fenêtre coulissante de longueur `k` qui se déplace de gauche à droite sur le tableau.

---

- Oui. 1. Algorithme – Deque monotonique

Nous conservons une déco qui stocke **indices** d'éléments de tableau.
Les indices de la deque sont toujours dans l'ordre ** décroissant des valeurs correspondantes**:

«» "
nombres[q[0]] >= nombres[q[1]] >= ... >= nombres[q[-1]]
«» "

L'élément à l'avant (`q[0]`) est donc le maximum de la fenêtre actuelle.

Pour chaque nouvel élément `nums[i]`:

1. **Supprimer les petits éléments du dos** –
alors que le dernier élément de la deque est plus petit que `nums[i]` pop it.
Ces éléments ne peuvent jamais devenir un maximum pendant que l'élément courant est dans la fenêtre.

2. **Appendir l'index actuel** – « q.append(i) ».

3. **Supprimer l'élément avant s'il quitte la fenêtre** –
if `q[0] <= i - k` pop it from the front.

4. **Enregistrez le maximum** – une fois que nous avons traité au moins une fenêtre complète
(`i >= k-1`) ajouter `nums[q[0]]` au résultat.

---

- Oui. 2. Preuve d ' exactitude

Nous prouvons que l'algorithme produit le maximum pour chaque fenêtre.

**Lemme 1**
La deque contient toujours des indices d'éléments à l'intérieur de la fenêtre actuelle.

*Proof. *
Lorsque `i` augmente, la fenêtre est `[i-k+1 , i]`.
L'étape 3 supprime l'élément frontal si son index `<= i-k`.
Aucun autre indice ne peut sortir de la fenêtre car les indices augmentent de 1 par étape. *

**Lemme 2**
La deque est toujours dans l'ordre décroissant des valeurs:
«nums[q[0]] >= nums[q[1]] >= ...».

*Proof. *
Lorsqu'un nouvel index `i` est traité, nous sortons du dos alors que `nums[q[-1]] < nums[i]`.
Ainsi, après la boucle, tous les éléments restants de la deque sont **pas plus petits** que `nums[i]`.
Puisque `i` est joint au verso, l'ordre est maintenu. *

**Lemme 3**
L'élément à l'avant de la deque est la valeur maximale de la fenêtre actuelle.

*Proof. *
Par Lemma 2, tous les éléments de la deque sont en ordre décroissant.
Par Lemma 1, tous se trouvent dans la fenêtre actuelle.
Par conséquent, l'élément frontal est le plus grand parmi les éléments de fenêtre. *

* Théorème *
L'algorithme affiche le maximum correct pour chaque fenêtre coulissante.

*Proof. *
Pour chaque position `i ≥ k-1`, l'algorithme ajoute `nums[q[0]]`.
Par Lemma 3 cette valeur est égale au maximum de la fenêtre `[i-k+1 , i]`.
Ainsi, chaque entrée de sortie est correcte, et toutes les fenêtres sont traitées exactement une fois. *

---

- Oui. 3. Analyse de la complexité

*Heure* – Chaque index est inséré et supprimé au plus une fois : **O(n)**.
*Espace* – La deque détient au plus des indices `k`; le tableau de résultats détient des valeurs `n-k+1`: **O(k)** espace supplémentaire.

---

- Oui. 4. Mise en œuvre des références (Python)

'`python
à partir de collections import deque
de taper l'importation Liste

Solution de classe:
def maxSlidingWindow(self, nombres: List[int], k: int) -> Liste[int]:
si ce n'est pas des nombres ou des k == 0:
retour []

n = len(nums)
q = deque() # indices de stockage des maxima potentiels
res = []

pour i, num in énumérate(nums):
# Supprimer les indices dont les valeurs correspondantes sont inférieures à num
alors que q et nums[q[-1]] < num:
Quantité
q.appendice i)

# Si l'index avant est par la fenêtre, pop it
si q[0] <= i - k:
q.popleft()

# Enregistrer maximum une fois la première fenêtre complète traitée
Si i >= k - 1:
res.append(nums[q[0]])

retour res
«» "

Cette solution suit exactement l'algorithme prouvé correct ci-dessus et fonctionne en temps linéaire avec espace de sortie linéaire.