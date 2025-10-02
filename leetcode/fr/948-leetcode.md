---
titre: LeetCode 948. Sac de jetons -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Sac de jetons – Solution de graisse optimale

** Problème* *
Vous commencez par `power = P` et `score = 0`.
Vous avez une liste `tokens` où `tokens[i]` est le coût de puissance de jeton *i*.
Vous pouvez jouer n'importe quel jeton au plus une fois, dans n'importe quel ordre, de l'une des deux façons

Mesure requise Effet
- C'est quoi ?
"pouvoir ≥ jetons[i]" "pouvoir -= jetons[i]", `score += C'est vrai.
Face vers le bas

Retournez le score maximum que vous pouvez atteindre.

-----------------------------------------------------------------------------------

- Oui. Pourquoi une stratégie avide à deux points fonctionne

* ** Dépenser le jeton le moins cher pour gagner un point* *
Lorsque vous avez assez de puissance pour jouer un face-up jeton, il est toujours préférable d'utiliser le jeton *le plus petit* disponible. Tout jeton plus grand gaspillerait plus de puissance pour le même point +1.

* **Utilisez un point pour gagner le plus de puissance**
Lorsque vous ne pouvez pas jouer de face vers le haut, vous pouvez convertir un point en puissance. Il est optimal d'utiliser le plus grand jeton restant pour cela, car il donne la puissance maximale possible pour un seul -1 point.

Si nous appliquons ces deux règles à plusieurs reprises, nous

1. augmenter le score aussi longtemps que la puissance le permet (en utilisant les jetons les moins chers);
2. si nous manquons de puissance mais avons encore des points, nous récupérons la puissance avec le jeton le plus cher (perdant un point);
3. arrêter quand aucun mouvement n'est possible.

Pendant le processus, nous gardons la trace du score maximum vu – c'est la réponse.

-----------------------------------------------------------------------------------

Algorithme (deux-pointeurs avides)

«» "
Tri(jetons) # O(n log n)
l = 0 # jeton le plus à gauche inutilisé
r = len(tokens)-1 # jeton le plus à droite inutilisé
score = 0
maxScore = 0

alors que l <= r:
si jetons[l] <= puissance: # peut jouer face vers le haut
puissance -= jetons[l]
l += 1
score += 1
maxScore = max(maxScore, score)
score elif > 0: # besoin de jouer face vers le bas
puissance += jetons[r]
r -= 1
score -= 1
Sinon : # ne peut plus jouer
pause

retour maxScore
«» "

-----------------------------------------------------------------------------------

Preuve d'exactitude

Nous prouvons que l'algorithme renvoie le score maximum réalisable.

---

Lemma 1
Si un jeton peut être joué face-up, utiliser le jeton restant *le plus petit* n'est jamais pire que d'utiliser un autre jeton.

**Prof.**
Jouer n'importe quel jeton face-up consomme sa valeur de puissance et donne +1 point.
Laisser `x ≤ y` être deux jetons restants.
Après avoir joué `x` nous avons au moins autant de puissance qu`après avoir joué `y` (`P - x ≥ P - y`).
Les deux actions donnent le même point +1, donc l'utilisation de `x` ne peut nous laisser qu'avec plus de puissance, ce qui ne peut qu'aider dans les mouvements futurs. *



Lemma 2
Si nous devons jouer un face-down en jeton (c'est-à-dire que nous n'avons aucun pouvoir pour un jeu face-up, mais au moins un point), utiliser le jeton restant *le plus grand* n'est jamais pire.

**Prof.**
Jouer un visage vers le bas donne `+tokens[i]` puissance au prix de `-1` point.
Laisser `x ≤ y` être deux jetons restants.
Après avoir joué `y` nous avons au moins autant de puissance qu`après avoir joué `x` (`P + y ≥ P + x`).
Les deux actions perdent exactement un point, donc l'utilisation de "y" ne peut nous laisser qu'avec plus de puissance, ce qui ne peut qu'aider plus tard. *



Lemma 3
Lors de l'exécution de l'algorithme, à chaque étape, l'ensemble de jetons qui n'ont pas été utilisés **** est un suffixe du tableau trié.

**Prof.**
Au départ, aucun jeton n'est utilisé.
L'algorithme ne supprime les jetons que de deux façons :

* 'Jetons[l] ' est enlevé en déplaçant `l` vers l'avant.
* "Jetons[r]" est enlevé en déplaçant `r` vers l'arrière.

Ainsi, les jetons enlevés sont toujours contigus du début ou de la fin, laissant un suffixe intact `tokens[l ... r]`.



Lemma 4
L'algorithme ne manque jamais une séquence optimale de mouvements.

**Prof.**
Supposons une séquence optimale `S` qui donne le score maximum.
Considérez la première étape où `S` diffère de l'algorithme avide.

*Si `S` joue un jeton face à face alors que l'avidité ne le fait pas*:
Greedy a assez de pouvoir (pour qu'il joue aussi) ou pas.
Si l'avidité ne peut jouer aucun jeton face-à-face, alors le jeton dans `S` doit être *plus cher* que `jetons[l]` (par Lemma 1).
Remplacer ce jeton dans `S` par le moins cher `tokens[l]` ne peut pas réduire le score et augmente seulement la puissance restante, en contradiction avec l'optimalité.

*Si `S` joue un jeton face-à-face alors que l'avidité ne le fait pas*:
Greedy ne joue pas face vers le bas que lorsque `score == 0`.
Tout mouvement face à face réduit le score à négatif, ce qui n'est jamais utile pour atteindre un score final plus élevé, de sorte qu'une solution optimale ne jouerait jamais un jeton face à face dans cette situation.

Ainsi, à chaque étape, le choix avide est au moins aussi bon que n'importe quel autre, et aucune solution optimale ne peut obtenir un score plus élevé que l'algorithme avide. *



C'est vrai. Théorème
`maxScore` retourné par l'algorithme est égal au score maximum possible.

**Prof.**
Par Lemma 4 l'algorithme gourmand peut être transformé en une séquence optimale qui donne le même score ou plus.
L'algorithme enregistre le score le plus important vu pendant la transformation, de sorte que `maxScore` est au moins le score optimal.
Inversement, l'algorithme ne dépasse jamais le véritable optimum car chaque étape est conforme aux règles du problème.
Par conséquent, la sortie de l'algorithme est égale à l'optimum. *



-----------------------------------------------------------------------------------

Analyse de complexité

*Trier* – temps `O(n log n)`, espace `O(n)` (le tri Python's utilise Timsort).
*Loop* - chaque jeton est traité au plus une fois, temps `O(n)`, espace supplémentaire `O(1)`.

Total : **Heure `O(n log n)`, espace `O(1)`** (enregistrant les entrées).

-----------------------------------------------------------------------------------

### Mise en oeuvre de la référence (Python 3)

'`python
de taper l'importation Liste

Solution de classe:
def bagOfTokens Score(self, jetons: List[int], power: int) -> Int:
jetons.sort() # ordre croissant
l, r = 0, len(tokens) - 1 # deux pointeurs
score, meilleur = 0, 0

alors que l <= r:
si jetons[l] <= puissance: # jouer face vers le haut
puissance -= jetons[l]
l += 1
score += 1
meilleur = max (meilleur, score)
score elif > 0: # jouer face vers le bas
puissance += jetons[r]
r -= 1
score -= 1
Sinon : # pas de mouvements à gauche
pause

le meilleur retour
«» "

La même logique peut être écrite en C++/Java avec une structure à deux pointeurs identique; le code ci-dessus suit l'algorithme de façon textuelle et contient des commentaires explicatifs.

-----------------------------------------------------------------------------------

**Résultat:**
La solution est optimale, simple à mettre en œuvre, et fonctionne dans le minimum de temps possible étant donné la nécessité de trier l'entrée.