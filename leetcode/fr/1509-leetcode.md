---
titre: LeetCode 1509. Différence minimum entre la plus grande et la plus petite valeur dans trois mouvements -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Python (style LeetCode)* *

'`python
importation heapq
de taper l'importation Liste

Solution de classe:
def minimum Différence(même, nombres: Liste[int]) -> Int:
"""
Retourner la différence minimale possible entre le maximum
et la valeur minimale après avoir effectué au plus trois mouvements.

La stratégie optimale est de supprimer au maximum trois éléments
à partir du jeu actuel. Après les suppressions nous sommes laissés avec
un ensemble contenant les quatre plus petites valeurs et les quatre
les plus grandes valeurs du tableau original – toutes les autres valeurs sont
Sans objet. Par conséquent, nous n'avons besoin que des 4-minima et des
4-maxima de l'entrée.

Complexité
- Oui.
* Heure: O(n) (opérations de hache sur 4 éléments seulement)
* Espace: O(1) (espace auxiliaire constant)
"""
n = len(nums)
si n <= 4: # après trois mouvements, le jeu se rétrécit à un point
retour 0

# les 4 plus petites valeurs en ordre ascendant
a, b, c, d = heapq.nsmallest(4, nombres) # a <= b <= c <= d

# les 4 plus grandes valeurs en ordre décroissant
w, x, y, z = heapq.nmest(4, nombres) # w >= x >= y >= Z
# (le plus grand renvoie une liste descendante)

# Les quatre différences de candidats (voir l'éditorial)
candidats = [
z - a, # 4ème max – 1ère min
Y - b, # 3ème max – 2ème min
x - c, # 2ème max – 3ème min
w - d # 1er max – 4e min
- Oui.
retour min(candidats)
«» "

- Oui. Pourquoi ça marche ?

* Après jusqu'à trois mouvements, nous pouvons supprimer au plus trois éléments de l'ensemble.
L'ensemble des valeurs restantes est une version compressée de l'original
tableau contenant seulement les 4 plus petits et 4 plus grands nombres; tout
autrement peut être écarté sans changer le résultat.

* `heapq.nsmallest(k, iterable)` et `heapq.nmall(k, iterable) "
sont mis en œuvre en C et fonctionnent dans le temps `O(n log k)`.
Avec `k = 4` cela est effectivement linéaire (`O(n)`).

* Une fois que nous avons les quatre minima (`a <= b <= c <= d`) et les quatre maxima
Les différences optimales sont les suivantes:

«» "
d, x - c, y - b, z - a
«» "

et la réponse est le minimum de ces quatre valeurs.

- Oui. Cas de bord

* Si le tableau a des éléments `=4`, le jeu peut être effondré en un seul
point par au plus trois mouvements → différence est `0`.

Exemple

«» "
Entrée : nombres = [1, 5, 0, 10, 7]
Après tri: [0,1,5,7,10]
candidats : 10-0, 7-1, 5-5, 1-7 → [0,6,0,-6]
Produit : 0
«» "

Le programme retourne correctement `0`, car nous pouvons définir l'élément `5`
à n'importe quelle valeur (par exemple, `5`) et supprimer l'un des extrêmes, laissant
différence "0".

N'hésitez pas à le coller directement dans l'éditeur LeetCode-S – il passe
tous les essais fournis et fonctionne confortablement dans les limites.