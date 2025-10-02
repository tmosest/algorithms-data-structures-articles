---
titre: LeetCode 1900. Les premiers et les derniers tours où les joueurs se disputent -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Explication de la solution**

Pour chaque cas de test nous sommes donnés

* `N` – nombre de participants au cycle actuel
* `P1 , P2` – positions des deux joueurs dans la ronde actuelle
(les positions sont `1 ... N`, le joueur le plus à gauche a la position `1`)

Dans un tour se produit le suivant

«» "
joueur 1 vs joueur N
joueur 2 vs joueur N-1
joueur 3 vs joueur N-2
...
«» "

Le gagnant de chaque paire (ou le seul joueur moyen quand `N` est bizarre)
continue jusqu'au prochain round.
Les gagnants sont placés dans une ligne ** triés par leurs postes** (à gauche)
à droite) – l'ordre est complètement déterministe, il ne dépend pas
qui gagne dans une paire.

La tâche est de déterminer après combien de tours les deux joueurs se rencontrent
(première fois).
La réponse est la même pour le meilleur possible et pour le pire possible
situation – elle est définie uniquement par les données initiales.



-----------------------------------------------------------------------------------

Observation 1
Dans un tour les deux joueurs se rencontrent **iff**

«» "
P1 + P2 = N + 1
«» "

parce que le joueur en position `i` rencontre le joueur en position `N-i+1`.

-----------------------------------------------------------------------------------

Observation 2
Après un tour les positions des deux joueurs dans le tour suivant peuvent
être calculé ** sans savoir qui a gagné**.

Laissez `M = (N + 1) / 2` – nombre de gagnants (division entière).

Pour tout joueur à la position `x` dans le tour actuel la nouvelle position dans
le prochain tour est

«» "
newPos = ceil(x / 2)
«» "

"ceil" peut être exprimé avec l'arithmétique entier comme

«» "
newPos = (x + 1) / 2 // division entière
«» "

Esquisse de preuve :

* Pour la partie gauche du champ (`x ≤ N/2`) le gagnant est le
`x`‐th gagnant, d'où son nouvel indice est `ceil(x/2)`.
* Pour la partie droite du champ (`x > N/2`) le gagnant est le
"N-x+1" - premier gagnant, mais après avoir trié les gagnants l'ordre relatif
des deux gagnants provenant de la même paire sont conservés,
Par conséquent, le nouvel indice est également «ceil(x/2)».
* Pour le joueur du milieu quand `N` est impair (`x = (N+1)/2`) la même
formule donne le nouvel indice correct – il se termine au milieu de
le prochain round.

Ainsi, les nouvelles positions sont entièrement déterminées par l'actuel
le nombre actuel de participants.

-----------------------------------------------------------------------------------

Algorithme
Pour chaque essai

«» "
ronde = 1
alors que vrai
Si P1 + P2 == N + 1 // les deux joueurs se rencontrent
réponse = ronde
pause
// sinon ils survivent tous les deux au tour suivant
P1 = (P1 + 1) / 2
P2 = (P2 + 1) / 2
N = (N + 1) / 2
round++
réponse de sortie
«» "

La boucle tourne au plus `log2(N)` temps, donc la complexité est
`O(log N)` par cas d ' essai.

-----------------------------------------------------------------------------------

Preuve d'exactitude

Nous prouvons que l'algorithme produit le tour dans lequel les deux joueurs
première rencontre.

---

Lemma 1
Lors de chaque itération de la boucle, les variables `P1` et `P2`
sont les vraies positions des deux joueurs dans la ronde actuelle.

**Prof.**

* Au départ, ce sont les positions données – vrai.
* Supposons qu'ils soient corrects avant une itération.
S'ils ne se rencontrent pas, les deux survivent au tour suivant.
Nous les mettons à jour pour
`P1 = (P1 + 1) / 2` et `P2 = (P2 + 1) / 2`
Par l'observation ce sont exactement leurs positions dans la suivante
ronde.
Par conséquent, l'invariant tient pour la prochaine itération. *



Lemma 2
Lorsque la boucle se termine, la valeur `réponse` correspond au premier tour
que les deux joueurs rencontrent.

**Prof.**

La boucle ne s'arrête que lorsque la condition `P1 + P2 == N + 1` tient.
Par Observation 1 cette condition est équivalente aux deux joueurs
se réunir dans cette ronde.
Parce que la boucle tourne dans l'ordre croissant de "round",
la première fois que la condition devient vraie est la première réunion.
Ainsi, la réponse est la valeur souhaitée. *



C'est vrai. Théorème
Pour chaque cas d'essai, l'algorithme produit le nombre de tours après
que les deux joueurs donnés se rencontrent pour la première fois.

**Prof.**

Par Lemma 1 la boucle s'arrête exactement quand les deux joueurs se rencontrent.
Par Lemma 2 le nombre de tours enregistré correspond à la première réunion
ronde.
Par conséquent, le numéro imprimé est correct. *



-----------------------------------------------------------------------------------

Analyse de complexité
Que `N` soit le nombre initial de participants.

* Chaque itération réduit `N` au moins par un facteur de deux
(`N ← (N+1)/2`), de sorte que la boucle tourne `=log2 N=" fois.
* Toutes les opérations à l'intérieur de la boucle sont `O(1)`.

Ainsi

«» "
Temps : O(log N) par cas d ' essai
Mémoire : O(1)
«» "

-----------------------------------------------------------------------------------

#### Mise en oeuvre des références (Go 1.17)

''Allez
paquet principal

importations (
"bufio"
"fmt"
"os"
)

func main() {
dans := bufio.NewReader(os.Stdin)
var T int
if _, err := fmt.Fscan(in, &T); err != zéro {
retour
}
auteur := bufio.NewWriter(os.Stdout)
pour ; T > 0; T-- {
var N, P1, P2 int64
si _, err := fmt.Fscan(dans, &N, &P1, &P2); err != zéro {
retour
}
round := int64(1)
pour {
Si P1+P2 == N+1 {
fmt.Fprintln(auteur, rond)
pause
}
// avance vers la prochaine ronde
P1 = (P1 + 1) / 2
P2 = (P2 + 1) / 2
N = (N + 1) / 2
round++
}
}
écrivain. Fuite()
}
«» "

Le programme suit exactement l'algorithme prouvé correct ci-dessus et
conforme à Go 1.17.