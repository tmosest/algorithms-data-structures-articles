---
Titre: LeetCode 3555. La plus petite sous-tribu à trier dans chaque fenêtre coulissante -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Python – Solution de tri et de comparaison rectiligne* *
*Complexité temporelle:* `O(n−k+1) · k log k) "
*Complexité spatiale:* `O(k)`

L'idée est simple :

1. Pour chaque fenêtre coulissante de longueur `k`, prendre le sous-barrage `sub`.
2. Triez une copie de cette sous-entente (`sorted_sub`).
3. Scanner les deux tableaux simultanément.
*Si un élément de `sub` est différent de l'élément du même index dans
`sorted_sub`, cette position est hors de la place. *
Le plus petit bloc contigu qui contient toutes les positions hors site
est exactement le bloc qui doit être trié pour faire la fenêtre entière triée.

La longueur de ce bloc est "droite – gauche + 1".
Si la fenêtre est déjà triée, `left` ne se déplace jamais à partir de `ш` et nous retournons `0`.

'`python
de taper l'importation Liste

Solution de classe:
def minSubarray Tri(self, nombres: List[int], k: int) -> Liste[int]:
n = len(nums)
ans = []

# glisser sur toutes les fenêtres de longueur k
pour i dans la plage (n - k + 1):
sub = nombres[i:i + k] # fenêtre actuelle
trié_sub = trié(sub) # sa version triée

gauche, droite = k, -1 # stockera les indices min et max mal appariés

# trouver les positions les plus à gauche et les plus à droite
pour j dans la plage(k):
si sous-[j] != _sous[j] trié :
gauche = min (gauche, j)
droite = max (droite, j)

# si aucune erreur n'a été trouvée, la fenêtre est déjà triée
Si c'est bien. -1: # pas d'erreur d'appariement
ans.append(0)
Sinon:
ans.append(droite - gauche + 1)

retour et
«» "

- Oui. Comment ça marche
* Pour chaque fenêtre, nous avons l'ordre "current" (`sub`) et l'ordre "désiré"
(`sorted_sub`).
* Chaque indice où ils diffèrent est un endroit qui n'est pas dans le bon
position relative dans la fenêtre.
* La plus petite sous-tribu qui contient tous ces indices est précisément la
segment qui doit être trié.
Sa longueur est "droite – gauche + 1".
Si la fenêtre est déjà triée, aucun indice ne diffère et nous retournons `0`.

La solution est facile à comprendre, implémente l'idée centrale directement,
et est assez rapide pour les contraintes LeetCode typiques.