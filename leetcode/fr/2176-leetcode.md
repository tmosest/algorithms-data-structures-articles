---
titre: LeetCode 2176. Compter des paires égales et divisibles dans un tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**LeetCode 2176 – Nombre de paires égales et divisibles dans un tableau* *

> **Tâche**
> Pour chaque paire d'indices `(i , j)` (`i < j`) en `nums` compter la paire lorsque
> 1. `nums[i] == nums[j] "
> 2. `i * j` est divisible par `k`.

Les seules paires que nous devons jamais regarder sont celles dont les valeurs sont les mêmes.
Si deux indices indiquent des nombres différents, la paire ne peut jamais être comptée, donc nous pouvons sauter ces comparaisons.

---

- Oui. Idée de haut niveau

1. **Indices de groupe par valeur** –
Scannez le tableau une fois, en stockant pour chaque valeur les indices auxquels il apparaît jusqu'à présent.
2. **Vérifier seulement les paires dans chaque groupe** –
Lorsque nous rencontrons l'index `i`, nous regardons la liste des indices antérieurs qui contiennent la même valeur.
Pour chaque index antérieur `j` dans cette liste, nous testons la condition de divisibilité `i * j % k == 0`.
S'il tient nous incrémentons la réponse.
3. **Ajouter l'indice actuel** –
Après vérification, nous poussons `i` sur la liste pour sa valeur afin que les indices futurs puissent s'associer avec elle.

C'est essentiellement l'astuce "Hash-map-with-position-lists" qui transforme la force brute "O(n2)" naïve en une construction monopass qui vérifie toujours chaque paire valide, mais qui ne touche jamais des paires de valeurs différentes.

---

- Oui. Preuve d'exactitude

Nous prouvons que l'algorithme renvoie exactement le nombre de paires valides.

*Let* `pos[v]` être la liste des indices que nous avons vu jusqu'à présent dont l'élément est «v».

Lorsque la boucle extérieure est à l'index «i»:

* Pour chaque `j` dans `pos[nums[i]]` nous vérifions la paire `(j, i)`.
Parce que `j < i` (nous insérons des indices seulement après les avoir traités),
cette paire satisfait à la condition 2.
L'algorithme le compte sif `nums[j] == nums[i]` (par construction) et
`i * j % k == 0`, c'est-à-dire si elle satisfait aux trois conditions.

* Toutes les autres paires qui pourraient être valides sont du formulaire `(j, i)` où `j < i "
et "nums[j] == nums[i]".
Ce sont exactement les paires énumérées dans la boucle sur `pos[nums[i]]`.
Aucune paire avec `j < i` et `nums[j] != nums[i]` n'est jamais considérée,
parce qu'il ne serait jamais inséré dans «pos[nums[i]]».

Ainsi, chaque paire comptée satisfait l'instruction et chaque paire qui satisfait l'instruction est comptée exactement une fois (la première fois que son indice plus grand est traité).

*

---

Analyse de complexité

Technique Temps Espace Remarques
Il n'y a pas de problème.
Brute-force boucles imbriquées Autres
Dans la pratique, beaucoup plus vite parce que seuls les indices de même valeur sont inspectés. Autres

`n ≤ 2·105` sur LeetCode, donc l'approche basée sur la carte passe confortablement.

---

## Mise en œuvre de la référence (Python 3)

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
def countPairs(self, nombres: List[int], k: int) -> Int:
# carte de la valeur à la liste des indices vus jusqu'à présent
pos = defaultdict(list)
ans = 0
pour i, val dans l'énumération(nombres):
# voir les indices précédents avec la même valeur
pour j in pos[val]:
si (i * j) % k == 0:
+= 1
# enregistrer l'indice actuel pour les paires futures
Pos[val].append(i)
retour et
«» "

Le code suit exactement l'algorithme décrit ci-dessus et fonctionne dans les limites requises.