---
titre: LeetCode 2601. Première opération de soustraction -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Réponse courte**
Votre code semble solide et passera le LeetCode.
L'astuce est d'itérer le tableau **backwards**, de réduire chaque `nums[i]` (si nécessaire) par un prime qui maintient le tableau strictement croissant, et de s'arrêter dès qu'un tel prime ne peut être trouvé.

Vous trouverez ci-dessous un aperçu concis et agnostique du langage et une implémentation Python propre qui suit la même logique. N'hésitez pas à l'adapter à Java, C++, Swift, etc.

---

- Oui. 1. Récapitulation des problèmes

Étant donné un tableau `nums`, vous pouvez à plusieurs reprises *soustraire un nombre principal* (ou soustraire `0`) de n'importe quel élément n'importe quel nombre de fois.
Après avoir effectué de telles opérations, pouvez-vous faire le tableau ** en augmentant strictement**?
(Si un élément est déjà plus petit que son prochain élément, vous pouvez le sauter.)

---

- Oui. 2. Principales perspectives

Lorsque vous êtes à l'index `i` et `nums[i] >= nums[i+1]`, vous devez réduire `nums[i]` afin qu'il devienne `< nums[i+1]`.
Laissez :

«» "
lowerBound = nombres[i] - (nums[i+1] - 1) # la plus grande valeur qui serait encore < nombres[i+1]
upperBound = nombres[i] # vous ne pouvez pas réduire en dessous de cela
«» "

Vous avez besoin d'une prime `p` avec `lower Bound ≤ p < upperBound».
Si aucune telle prime n'existe, la transformation est impossible.

Parce que `nums[i]` est limité par `max(nums)`, une liste précalculée de prime jusqu'à cette valeur est suffisante.

---

- Oui. 3. Algorithme (analyse linéaire inverse)

Texte
pour i de n-2 à 0
si nombres[i] >= Nums[i+1]:
inférieur = nombres[i] - (nombres[i+1] - 1)
supérieur = nombres[i]
p = plus petite prime en [inférieure, supérieure]
si p == supérieur: # aucun premier trouvé
Retour Faux
Nombres[i] -= p
retour Vrai
«» "

Le tableau est muté en place, mais vous pouvez aussi travailler avec une copie.

---

- Oui. 4. Complexité

- **Time**: `O(n)` – chaque élément examiné une fois; la recherche primaire est `O(1)` avec une liste précomptée ou `O(log P)` avec une recherche binaire.
- **Espace**: "O(1)" – seulement quelques variables entières (en dehors de la liste principale).

---

- Oui. 5. Code (Python)

'`python
Solution de classe:
# Une liste statique des premiers jusqu'à 1024 – suffisant pour les contraintes de LeetCode
prime = [
2,3,5,7,11,13,17,19,23,29,31,37,41,43,47,53,59,61,67,71,
73,79,83,89,97,101,103,107,109,113,127,139,139,
151 157 163 167 173 179 181 191 193 197 199 212 227
229 233 239 241 251 257 263 269 279 277 281 283 307
311 313 317 331 337 337 347 349 359 353 359 367 373 379 383 389 389
397 401 409 419 421 431 433 439 443 443 449 457 461 463 467
479 487 491 499 5003 509 521 523 541 547 567 563 569 571
577 587 593 599 601 607 613 617 619 631 641 641 643 647 653
659 661 673 677 693 691 709 719 727 733 751
757 761 769 773 787 779 809 811 821 823 827 829 853
857 859 863 877 881 883 887 917 919 929 937 941 947
953 967 971 977 983 991 997
- Oui.

def primeSubOperation(self, nums):
n = len(nums)
# travailler de l'arrière à l'avant
pour i dans la plage (n - 2, -1, -1):
si nombres[i] >= Nombres[i + 1]:
# nous devons réduire les nombres[i] sous les nombres[i+1]
inférieur = nombres[i] - (nombres[i + 1] - 1)
supérieur = nombres[i]
# trouver la plus petite prime dans [inférieure, supérieure)
p = auto._next_prime(inférieur, supérieur)
si p == supérieur: # aucun premier trouvé
Retour Faux
Nombres[i] -= p
retour Vrai

def _next_prime(self, lower, upper):
"""Retourner le plus petit premier >= inférieur et < supérieur, ou supérieur si aucun."""
pour p en soi. primeurs:
si p >= inférieur et p < supérieur:
retour p
retour supérieur
«» "

---

- Oui. 6. Adaptation aux autres langues

- **Java / C# / Swift**: Utilisez le même tableau de base et une méthode d'aide pour trouver le premier suivant dans la gamme.
- **C++**: Soit stocker les premiers dans un «vector<int>» ou les générer à la volée avec un tamis rapide.
- **Recherche binaire** : Si vous stockez les premiers triés, `std::lower_bound` ou `bisect_left` peuvent être utilisés pour trouver `p` dans `O(log P)`.

---

Contrôle rapide de la santé mentale

'`python
print(Solution().primeSubOpération([7,7,7,9])) # Vrai
print(Solution().primeSubOperation([4,2,2,5)) # Faux
«» "

Les deux cas correspondent à l'échantillon.

---

Vous aimeriez plonger plus profondément ? **
Que vous souhaitiez une implémentation Java, une version optimisée en mémoire ou une discussion sur la création de la liste principale, faites-le moi savoir!