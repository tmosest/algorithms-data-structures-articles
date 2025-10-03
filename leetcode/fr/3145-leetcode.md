---
titre: LeetCode 3145. Trouver des produits d'éléments de grand tableau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Explication de la solution**

Pour une requête `l , r , m` nous devons sortir

«» "
big_nums[l] · big_nums[l+1] · ... · big_nums[r] (mod m)
«» "

`big_nums` est la liste de tous les nombres naturels écrits en ordre croissant

«» "
big_nums[0] = 1, big_nums[1] = 2, big_nums[2] = 3, ...
big_nums[i] = i + 1
«» "

le produit requis est le produit de tous les entiers de `l+1` à `r+1`
(inclus) pris modulo `m`.

-----------------------------------------------------------------------------------

C'est vrai. 1. Observations

* `m` est au plus `10^5`.
Dans toute séquence d ' entiers consécutifs `m` il y a un multiple de `m`
(principe du trou de pigeon).
Par conséquent, si la longueur d'intervalle `r – l + 1` est **≥ m**, le produit est
multiple de `m` et la réponse est `0`.

* Lorsque la longueur de l'intervalle est inférieure à `m`, le produit contient à
la plupart des facteurs «m‐1» (10^5)».
Nous pouvons calculer le produit directement, chaque facteur modulo `m`, parce que
la taille de la boucle est au plus `10^5`.

-----------------------------------------------------------------------------------

C'est vrai. 2. Algorithme
Pour chaque essai

«» "
len = r - l + 1
si len >= m → réponse = 0
Autre
prod = 1 (mod m)
pour i de 0 à len- 1
prod = prod * ((l + 1 + i) mod m) (mod m)
réponse = prod
réponse de sortie
«» "

-----------------------------------------------------------------------------------

C'est vrai. 3. Preuve d'exactitude

Nous prouvons que l'algorithme produit la valeur correcte pour chaque requête.

---

Lemma 1
Si `len = r – l + 1 ≥ m` alors
`big_nums[l] · ... · big_nums[r]` est divisible par `m`.

**Prof.**
`big_nums[i] = i + 1`.
Le jeu `{l+1, l+2, ..., r+1}` contient des entiers consécutifs `m`.
Parmi les entiers consécutifs `m` il y en a exactement un qui est multiple
de `m`.
Par conséquent, le produit contient ce multiple et est un multiple de `m`,
donc congruent à `0` modulo `m`.



Lemma 2
Si `len < m` la boucle de l`algorithme calcule

«» "
prod = ( (l+1) · (l+2) · ... (r+1) ) (mod m)
«» "

**Prof.**
La boucle itère au-dessus de `i = 0 ... len-1`.
Dans la 'i'-th itération, il multiplie le produit actuel par
`(l+1+i) mod m`.
Toutes les opérations sont effectuées modulo `m`, donc après la dernière itération
`prod` est égal au produit de tous les nombres de `l+1` à `r+1` pris modulo
"m".



C'est vrai. Théorème
Pour chaque requête `l , r , m` les sorties de l'algorithme

«» "
big_nums[l] · big_nums[l+1] · ... · big_nums[r] (mod m)
«» "

**Prof.**

*Si 'len ≥ m':
Par Lemma 1 le produit est un multiple de `m`; les sorties de l'algorithme
`0`, qui est égal à la valeur désirée modulo `m`.

*Si 'len < m ' :
Par Lemma 2 la boucle calcule exactement le produit de tous les facteurs
de `l+1` à `r+1` modulo `m`.
C'est la valeur requise. *



-----------------------------------------------------------------------------------

C'est vrai. 4. Analyse de la complexité

Pour une requête

* Si "len ≥ m" la réponse est calculée en "O(1)".
* Sinon, on effectue au maximum des multiplications < m-1 ≤ 10^5`,
chaque «O(1)».

D'où le temps par requête est `O(min(len, m) ≤ O(10^5)` et la mémoire
la consommation est «O(1)».

-----------------------------------------------------------------------------------

C'est vrai. 5. Mise en œuvre des références (Python 3)

'`python
importations

def resouver() -> Aucun:
données = list(map(int, sys.stdin.read().split())
t = données[0]
out = []
p = 1
pour _ dans l'intervalle(t):
l, r, m = données[p:p+3]
p += 3
Si m == 1: # tout est 0 modulo 1
out.append(0)
poursuivre

longueur = r - l + 1
si la longueur >= m: # un multiple de m se produit
out.append(0)
poursuivre

prod = 1 % m
début = l + 1
pour i dans la plage (longueur):
prod = (prod * ((démarrage + i) % m)) % m
out.append(prod)

sys.stdout.write("\n".join(map(str, out)))

si __nom__ == "__main__" :
résoudre()
«» "

Le programme suit exactement l'algorithme prouvé correct ci-dessus et
se conforme au format d'entrée/sortie requis.