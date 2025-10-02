---
titre: LeetCode 2191. Triez les numéros jumelles -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Ce que fait la solution – en mots clairs* *

1. **Amenez chaque numéro dans sa version -mapped. **
- Chaque chiffre du numéro original est remplacé par le chiffre que le tableau *mapping* nous demande d'utiliser.
- Exemple : si `mapping[3] = 8` et que le nombre est `123`, le `3` devient `8`.
- Une fois tous les chiffres remplacés, nous obtenons un nouveau nombre entier (par exemple `148`).

2. ** Gardez le numéro original et rappelez-vous sa position. **
- Pour chaque élément dans "nums", nous stockons un tuple:
`(<original number>, <mapper number>, <original index>)`.
- L'index original n'est utilisé que pour garder le genre **stable** (les éléments avec la même valeur cartographiée conservent leur ordre relatif).

3. **Trier par les numéros cartographiés. **
- La liste des tuples est triée d'abord sur le nombre *mapper* et, si deux nombres mappered sont égaux, sur l'index *original*.
- Oui. Cela garantit que deux nombres map à la même valeur apparaissent dans le même ordre que dans l'entrée.

4. **Construire le tableau final.**
- Après tri, nous lisons seulement les numéros d'origine des tuples triés et retournons ce tableau.

---

- Oui. Pourquoi ça marche ?

- **Mapping est une bijection sur les chiffres** – chaque chiffre 0‐9 est remplacé par un autre chiffre, de sorte que la cartographie est bien définie pour tout entier.
- **Stable** – En ajoutant l'index original comme clé de tri secondaire, nous conservons l'ordre des liens.
Dans la plupart des langues (`sort` en C++/Java, `sorted` en Python) l'algorithme de tri est stable, mais l'ajout de l'index le garantit même si l'implémentation du langage change.
- **Complexité** –
- La conversion d'un nombre de chiffres *d* coûte O(d).
- Nous le faisons pour tous les numéros *n*: O(n·d).
- Tri de la liste des coûts des tuples *n* O(n log n).
Le temps global est donc O(n log n + n·d), et l'espace est O(n) pour la liste des tuples.

---

pseudo-code rapide

Texte
pour chaque i en 0 .. nombres.longueur-1
s = représentation par chaîne de nombres[i]
mappedString = ""
pour chaque caractère c en s
mappedString += mapping[ int(c) ]
mappedVal = int(mappedString) // les zéros de tête sont rejetés
ajouter tuple (nums[i], mappedVal, i) à la liste

Liste de tri par (mappedVal, index original)

résultat = []
pour chaque tuple dans la liste triée
ajouter le numéro original au résultat

résultat du retour
«» "

Qu'est-ce que c'est – l'algorithme est juste la paire de "transform →" avec l'index → le tri stable → les originaux de sortie.