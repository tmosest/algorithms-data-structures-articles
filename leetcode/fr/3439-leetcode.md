---
titre: LeetCode 3439. Reprogrammer les réunions pour un temps libre maximum Je...
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Explication de la solution**

Pour chaque cas de test nous sommes donnés

* `n` – nombre de réunions
* `k` – le gestionnaire doit supprimer les réunions `k`
* `m` - le jour a la longueur `m` (le temps est `0 ... m`)
* "n" intervalles "[l i , r i ]" – "0 ≤ l i < r i ≤ m" –
une réunion occupe le segment semi-ouvert "[l i , r i ]".

Toute la journée est gratuite sauf pour les intervalles qui restent.
Le gestionnaire peut supprimer toute réunion "k".
Après la suppression, les séances restantes peuvent être reportées (leur ordre peut être
être changés) tant qu'ils ne se chevauchent toujours pas et qu'ils restent à l'intérieur
«[0 , m]».
Nous devons trouver la longueur maximale possible d'un
l'intervalle dans le calendrier résultant.



-----------------------------------------------------------------------------------

C'est vrai. 1. Observations

«» "
Si toutes les réunions restantes sont regroupées en un seul bloc continu,
le temps libre est la longueur de la partie vide qui est à l'extérieur de ce bloc.
«» "

Parce que les réunions peuvent être réorganisées,
le calendrier optimal pour les réunions restantes est toujours à mettre
les uns ensemble dans un bloc (l'arrangement d'étanchéité).
Tous les autres arrangements ne peuvent qu'augmenter la partie occupée
ne jamais augmenter l'intervalle libre.

Pour un ensemble fixe de réunions
(let `S` contient des réunions `t` après triage par heure de début)

«» "
bloc = [ min l dans S , max r dans S ]
longueur = max r – min l (partie occupée)

la partie libre en dehors de ce bloc est
( m – longueur ) – ( longueur de l'écart entre les
bloc et la réunion la plus proche à l'extérieur
ce bloc )
«» "

Lorsque nous supprimons les réunions `k`, toutes les réunions restantes forment une réunion contiguë
segment dans la liste triée – sinon nous pourrions supprimer une réunion
à l'intérieur de ce segment et agrandir la partie libre.
Par conséquent, les réunions restantes sont exactement une fenêtre coulissante de taille
`n‐k` sur la liste triée.



-----------------------------------------------------------------------------------

C'est vrai. 2. Précomputation

«» "
intervalles – gamme de paires (l, r) triées par l
gaucheGap[i] – l[i] – r[i‐1] (écart entre i‐1 et i)
droitGap[i] – l[i+1] – r[i] (écart entre i et i+1)
«» "

`leftGap` et `rightGap` sont `0` lorsque l'index correspondant ne
existe.
Nous construisons deux tableaux d'aide.

«» "
prefMax[i] – maximum de gaucheGap[0 ... i] (meilleure partie libre à gauche)
suffMax[i] – maximum de droiteGap[i ... n-1] (meilleure partie libre sur la droite)
«» "

Tous sont construits en temps "O(n).



-----------------------------------------------------------------------------------

C'est vrai. 3. Fenêtre coulissante

Pour une fenêtre commençant à la position `p` et contenant des réunions `n‐k`
('p ... p + n‐k – 1') nous savons

«» "
longueur du bloc = r[p + n-k – 1] – l[p] (partie occupée)
leftFree = prefMax[p‐1] (gauche à gauche de la fenêtre)
rightFree = suffMax[p + n-k] (gap à droite de la fenêtre)
«» "

Le maximum de temps libre possible avec cette fenêtre est

«» "
meilleur = max( gauche Gratuit , droit Gratuit )
«» "

Nous faisons glisser la fenêtre à travers toutes les positions `n‐k+1` et gardons le maximum
valeur – c'est la réponse pour le cas d'essai.



-----------------------------------------------------------------------------------

C'est vrai. 4. Preuve d ' exactitude

Nous prouvons que l'algorithme imprime le temps libre maximum requis.

---

Lemma 1
Après avoir supprimé les " k " réunions, les autres réunions sont contiguës
de toutes les réunions.

**Prof.**

Supposons le contraire – il existe une réunion "A" en dehors du reste
segment qui se situe strictement entre deux réunions restantes `B` et `C`
dans l'ordre trié.
Supprimer `B` au lieu de `A`.
L ' intervalle de `B` est inférieur ou égal à l ' intervalle de `A` dans
durée du début,
d ' où l ' écart entre < < B > > et < < C > > n ' est pas inférieur à l ' écart entre
`A` et `C`.
Par conséquent, le temps libre obtenu par ce nouvel ensemble de
les réunions sont au moins aussi grandes que l'original – contradiction. *



Lemma 2
Pour un ensemble fixe de réunions restantes, le calendrier optimal est de
fusionner tous en un seul bloc continu.

**Prof.**

Prendre tout programme des réunions restantes qui n'est pas un bloc.
Déplacer les réunions vers la gauche jusqu'à ce qu'une réunion touche sa gauche
voisin. La partie occupée ne grandit pas, d'où la partie libre
Pas de psy.
Répéter cette étape pour toutes les réunions produit exactement un bloc,
un calendrier avec au moins un intervalle libre. *



Lemma 3
Laissez les réunions restantes former une fenêtre «W» de longueur «t = n‐k».
Que `lmin` et `rmax` soient respectivement le plus petit départ et le
l'achèvement le plus important de toutes les réunions dans `W`.
Que `gapL` soit le plus grand écart à gauche de `W`
('prefMax[p‐1]` dans l'algorithme) et `gapR` le plus grand écart par rapport au
à droite de `W` (`suffMax[p+t]`).
Puis l'intervalle libre maximal obtenu avec cette fenêtre est égal
"max(gapL, gapR)".

**Prof.**

Le bloc qui contient toutes les réunions dans `W` occupe le segment
`[lmin , rmax)` de longueur `len = rmax – lmin`.
Le bloc peut être déplacé à l'intérieur des deux espaces voisins.
*Si le bloc commence à la limite gauche de l'écart gauche*,
la partie libre sur son côté gauche est "gapL".
*Si elle se termine à la limite droite de l'écart de droite*,
la partie libre sur son côté droit est "gapR".
Aucun autre placement ne peut augmenter de chaque côté, car le bloc
ne peut pas traverser une réunion voisine.
Par conséquent, le meilleur temps libre possible pour cette fenêtre est
"max(gapL, gapR)". *



Lemma 4
Pendant l'étape de la fenêtre coulissante, l'algorithme calcule
`max(gapL , gapR)` correctement pour chaque fenêtre.

**Prof.**

Pour une fenêtre qui commence à la position `p`

«» "
prefMax[p‐1] = gapL (par définition de prefMax)
suffMax[p+t] = gapR (par définition de suffMax)
«» "

L'algorithme évalue `max(prefMax[p‐1], suffMax[p+t])',
Par conséquent, il obtient exactement `max(gapL , gapR)` pour cette fenêtre. *



C'est vrai. Théorème
Pour chaque cas d'essai, l'algorithme produit la longueur maximale possible
d'un intervalle libre continu après suppression des réunions "k".

**Prof.**

Par Lemma 1 les autres réunions sont une fenêtre contiguë de
longueur `n‐k` dans la liste triée.
Par Lemma 2 nous pouvons les fusionner en un seul bloc.
Lemma 3 donne le meilleur intervalle libre pour cette fenêtre particulière
et Lemma 4 montre que l'algorithme évalue cette valeur.
Prendre le maximum sur toutes les fenêtres possibles, l'algorithme
rend exactement l'optimum. *



-----------------------------------------------------------------------------------

C'est vrai. 5. Analyse de la complexité

«» "
Intervalles de tri : O(n log n)
Préfixe de construction / tableaux suffixes : O(n)
Fenêtre coulissante sur toutes les fenêtres : O(n)
«» "

D'où la durée totale de fonctionnement d'un cas d'essai est "O(n log n)"
et la consommation de mémoire est "O(n)".



-----------------------------------------------------------------------------------

C'est vrai. 6. Mise en œuvre des références (Python 3)

'`python
importations
bisect d'importation

♪ ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

def resolve_one(n, k, m, intervalles):
# 1. Tri par heure de départ
intervalles.sort() # par l, r automatiquement
l = [iv[0] pour iv en intervalles]
r = [iv[1] pour iv à intervalles]

2. préfixer les écarts – plus grand écart qui se termine à i
pref = [0] * n
pour i dans la plage (1, n):
écart = l[i] - r[i-1]
pref[i] = max(pref[i-1], écart)

3. suffixe des écarts – plus grand écart qui commence à i
suff = [0] * n
pour i dans la plage(n-2, -1, -1):
écart = l[i+1] - r[i]
suff[i] = max(suff[i+1], écart)

3. Fenêtre coulissante (autres réunions)
t = n - k Nombre de réunions qui restent
meilleur = 0
pour p dans la plage(0, t + 1):
gauche_g = pref[p-1] si p > 0 autre 0
right_g = suff[p + t] si p + t < n autre 0
best = max(meilleur, gauche_g, droite_g)
le meilleur retour

♪ ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
def resouver() -> Aucun:
il = iter(sys.stdin.read().strip().split())
hors_lignes = []
alors que Vrai:
n = int(next(it))
k = int(next(it))
m = int(next(it))
si n == 0 et k == 0 et m == 0:
pause
intervalles = [(int(next(it)), int(next(it))) pour _ dans l'intervalle(n)]
out_lines.append(str(solve_one(n, k, m, intervalles))
sys.stdout.write("\n".join(out_lines))

♪ ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
si __nom__ == "__main__" :
résoudre()
«» "

Le programme suit exactement l'algorithme prouvé correct ci-dessus et
se conforme au format d'entrée/sortie requis.