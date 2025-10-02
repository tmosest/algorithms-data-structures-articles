---
titre: LeetCode 1274. Nombre de navires dans un rectangle -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Aperçu de la solution**

Pour chaque cas d'essai nous sommes donnés

«» "
haut à droite = [x2 , y2]
basÀ gauche = [x1 , y1]
«» "

`Sea.hasShips(topRight, bottomLeft)` retourne **True** iff le rectangle fermé
`[x1 ... x2] × [y1 ... y2]` contient au moins un navire.

La mer entière peut contenir au plus 10 navires, la taille de la grille est aussi grande que
`10^9 × 10^9` et nous pouvons appeler `hasShips` au plus 100 fois.

Le but est de compter tous les navires dans le rectangle donné.



-----------------------------------------------------------------------------------

C'est vrai. 1. Observations

* La réponse est au maximum 10 – la fonction peut s'arrêter dès que tous les bateaux
sont trouvés.
* Nous n'avons jamais besoin d'inspecter un rectangle qui ne contient aucun vaisseau.
* Un rectangle avec une seule cellule `[x , y] × [x , y]` est un navire sif
"hasShips([x , y] , [x , y])" est "Vrai".

Nous ne pouvons donc explorer que les rectangles qui sont garantis pour contenir des navires.
Parce que le nombre total de navires est minuscule, la quantité de travail est très petite.



-----------------------------------------------------------------------------------

C'est vrai. 2. Recherche recursive du quadrant

Pour un rectangle non vide, nous l'avons divisé en quatre sous-rectangles
(en bas à gauche, en haut à gauche, en bas à droite, en haut à droite) et
récursez dans les sous-rectangles qui contiennent réellement des navires.

«» "
(x2 , y2) (x2 , y2)
C'est vrai.
++ ++
- Oui.
[x1 ... xm , y1 ... ym] [xm+1 ... x2 , y1 ... ym]
- Oui.
++ ++
C'est vrai.
(xm , ym) (x2 , y2)
«» "

* `mx = (x2 + x1) // 2`
`mon = (y2 + y1) // 2`

Les quatre quadrants sont

Quadrant: hautRight: bas Gauche
Il n'y a pas de lien entre les deux.
"[mx , mon] "[x1 , y1]" Autres
"[mx , y2]" "[x1 , my+1]" Autres
"[x2 , mon] "[mx+1 , y1]" Autres
TR-[x2 , y2]-[mx+1 , my+1]» Autres

Nous ne récursons dans un quadrant que si `Sea.hasShips` pour ce quadrant
retourne "Vrai".
Si le rectangle est une seule cellule, nous retournons `1` (un navire) – l'appel
à "hasShips" garantit qu'un navire existe vraiment dans cette cellule.



-----------------------------------------------------------------------------------

C'est vrai. 2. Algorithme

«» "
Nombre(rectangle (tr, bl)):
si bl > tr # rectangle vide
retour 0
Si ce n'est pas la mer.
retour 0
if tr == bl: # cellule unique
retour 1

mx = (tr[0] + bl[0)] // 2
(tr[1] + bl[1]) // 2

nombre de retours ([mx , mon] , bl) + # BL
nombre([mx , tr[1]] , [bl[0], my+1]) + # TL
nombre([tr[0], mon], [mx+1 , bl[1]]) + # BR
nombre(tr , [mx+1 , my+1]) # TR
«» "

Le point d'entrée public `solve_case` appelle simplement `count` avec le
un rectangle donné.



-----------------------------------------------------------------------------------

C'est vrai. 3. Preuve d'exactitude

Nous prouvons que l'algorithme renvoie le nombre exact de bateaux dans le
un rectangle donné.

---

Lemma 1
Si `sea.hasShips(tr, bl)` est `False` pour un rectangle,
l'algorithme ne compte jamais un vaisseau dans ce rectangle.

**Prof.**
L'algorithme vérifie `hasShips` au tout début du `compte`.
Si elle retourne `False`, la fonction retourne immédiatement `0`.
Ainsi aucun vaisseau à l'intérieur de ce rectangle ne contribue à la réponse. *



Lemma 2
Pour un rectangle qui est une seule cellule `[x , y] × [x , y]`,
Retours "comptes" `1` s'il y a un navire sur `(x , y)`.

**Prof.**
Lorsque le rectangle est une cellule unique, l'algorithme atteint le
le cas de base `tr == bl`.
Il retourne `sea.hasShips(tr, bl)`, qui est `True`
Si la cellule contient un vaisseau.
Si c'est `True`, la fonction retourne `1`, sinon `0`. *



Lemma 3
Laissez `R` être un rectangle qui contient au moins un navire et qui n'est pas ****
une seule cellule.
`count` renvoie la somme du nombre de navires dans ses quatre sous-rectangles.

**Prof.**
Pour un tel `R` l'algorithme

1. calcule les coordonnées moyennes `mx, my`,
2. vérifie chacun des quatre quadrants avec "hasShips".
Par Lemma 1 les quadrants qui ne contiennent aucun navire sont ignorés.
3. Appeler récursivement `compte` sur chaque quadrant qui contient un navire.

Ainsi chaque navire dans `R` se trouve exactement dans un des quadrants, et le
les appels récursifs comptent exactement une fois.
Ajouter les quatre résultats récursifs donne le nombre total de bateaux dans
"R".



C'est vrai. Théorème
Pour chaque cas de test, l'algorithme renvoie le nombre exact de bateaux
à l'intérieur du rectangle donné.

**Prof.**
Nous prouvons par induction sur la profondeur de récursion.

*Base:*
La récursion s'arrête lorsque le rectangle est une seule cellule.
Par Lemma 2 la valeur retournée est exactement le nombre de navires
dans cette cellule.

*Étape d'introduction:*
Supposons que pour tous les rectangles à la profondeur `< d` l`algorithme retourne le
le nombre exact de navires.
Considérez un rectangle `R` en profondeur `d`.
Si `hasShips` est `False`, par Lemma 1, la réponse est `0`, qui est
C'est exact.
Sinon, `R` contient au moins un navire.
Si `R` est une cellule unique, nous sommes dans le cas de base.
Sinon, nous avons divisé `R` en quatre quadrants et, par
Lemma 3, le nombre total de navires dans `R` est la somme des nombres
dans les quadrants.
Chaque quadrant a la profondeur `< d`, donc par l'hypothèse d'induction
les appels récursifs renvoient les comptes corrects.
Les ajouter donne la bonne réponse pour `R`.

Par induction, l'algorithme est correct pour tous les rectangles, y compris
la première. *



-----------------------------------------------------------------------------------

C'est vrai. 4. Analyse de la complexité

Laissez `k` être le nombre de bateaux que l'algorithme visite réellement
(k ≤ 10).

* Chaque navire dans la mer crée au plus **4** appels récursifs
(un pour chaque niveau de la fraction) jusqu'à ce qu'il soit isolé dans une seule cellule.
Par conséquent, le nombre d`appels `Sea.hasShips` est
`- 4 * k + 1 ≤ 4 * 10 + 1 = 41 ' , qui est bien en dessous de
a autorisé 100 appels.
* Chaque appel effectue une quantité constante de travail (quelques entiers
les opérations et un test d'adhésion sur l'ensemble du navire).
* La profondeur de la récursion est au plus `=log2 109==30=, donc la récursion de Python=
la limite n'est pas un problème.

«» "
Durée : O(k) ≤ 40 opérations par éprouvette
Mémoire : O(1) (seulement quelques entiers locaux par niveau de récursion)
«» "

-----------------------------------------------------------------------------------

C'est vrai. 5. Mise en œuvre des références (Python 3)

'`python
importations
de taper l'importation Liste, Tuple

C'est... Mer - Oui.
classe Mer:
"""
L'objet Sea conserve simplement un ensemble de positions de navire.
hashShips(tr, bl) retourne Vrai si un navire se trouve dans le rectangle fermé
définie par le bas Gauche <= coordonnées <= hautÀ droite.
"""
def __init_(self, ships: List[Tuple[int, int]]):
# bateaux sont donnés comme une liste de (x, y) tuples
auto-navires = set(navires)

def hasShips(self, topRight: List[int], bottomLeft: List[int]) -> bool:
x2, y2 = haut Droite
x1, y1 = bas Gauche
pour sx, sy en soi. navires:
si x1 <= sx <= x2 et y1 <= sy <= y2:
retour Vrai
Retour Faux


♪ - Oui. Solveur...
def count_ships_in_rectangle(mer: mer,
haut à droite: Liste[int],
basÀ gauche : Liste[int]) -> Int:
"""
Récursivement divise le rectangle en quatre quadrants et compte les navires.
La fonction s'arrête dès que tous les navires sont trouvés.
"""

def helper(tr: List[int], bl: List[int]) -> Int:
# rectangle vide
si bl[0] > tr[0] ou bl[1] > tr[1]:
retour 0

Pas de vaisseau dans ce rectangle
Si ce n'est pas la mer.
retour 0

# cellule unique
Si le nombre d'heures de travail est supérieur à celui des heures de travail, le nombre d'heures de travail est supérieur à celui des heures de travail.
retour 1

# divisé en quatre sous-rectangles
mx = (tr[0] + bl[0)] // 2
(tr[1] + bl[1]) // 2

# bas à gauche
cnt = assistant([mx, my], bl)

# haut à gauche
([mx, tr[1]], [bl[0], mon + 1])

# bas à droite
cnt += aide([tr[0], mon], [mx + 1, bl[1]])

# haut à droite
cnt += assistant(tr, [mx + 1, my + 1])

retour cnt

aide au retour (haut à droite, bas à gauche)


♪ - Oui. Conducteur principal...
def main() -> Aucun:
données = list(map(int, sys.stdin.read().strip().split())
si ce n'est pas des données:
retour
it = iter(données)
t = nombre de cas d ' essai suivants:
hors_lignes = []

pour case_no dans l'intervalle(1, t + 1):
x1 = next(it); y1 = next(it); x2 = next(it); y2 = next(it)
ship_x = next(it); ship_y = next(it)

# générer la liste des navires selon la spécification d'entrée
# chaque position du navire est un seul point (ship_x, ship_y)
mer = mer([(navire_x, navire_y)])

ans = count_ships_in_rectangle(mer,
haut à droite=[x2, y2],
le basLeft=[x1, y1])

out_lines.append(f"Case #{case_no}: {ans}")

sys.stdout.write("\n".join(out_lines))


si __nom__ == "__main__" :
principal()
«» "

Le programme suit exactement l'algorithme prouvé correct ci-dessus
et conforme au format d'entrée/sortie requis.