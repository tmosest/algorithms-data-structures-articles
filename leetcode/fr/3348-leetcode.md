---
titre: LeetCode 3348. Plus petit Digit Divisible Produit II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
** Explication de la solution**

Pour un nombre

«» "
x = d1 d2 ... dm ( di – chiffres décimaux )
«» "

*produit* est le produit de tous ses chiffres décimaux

«» "
produit(x) = d1 · d2 · ... · dm .
«» "

Pour un cas d'essai nous sommes donnés

* un produit requis `t` ( `t ≥ 2` )
* une longueur maximale `n` ( `1 ≤ n` )
* un lien inférieur `k` ( `k ≥ 1` )

Nous devons trouver un numéro

«» "
x ( 1 ≤ longueur(x) ≤ n , produit(x) = t )
«» "

avec la plus petite valeur décimale possible.
Si un tel numéro n'existe pas, la réponse est **NO SOLUTION**.



-----------------------------------------------------------------------------------

C'est vrai. 1. Observations

* Le produit d'un nombre dépend uniquement de ses chiffres.
* La factorisation primaire d'un chiffre décimal ne contient que les premiers
«2 , 3 , 5 , 7».
Tous les autres facteurs principaux n'apparaissent dans aucun chiffre décimal, par conséquent
ils ne peuvent jamais faire partie d'un produit à chiffres décimaux.
Par conséquent,

«» "
si t contient un facteur primaire autre que 2,35,7
→ aucun numéro avec le produit t existe du tout
«» "

* Pour les premiers `2 , 3 , 5 , 7` le tableau suivant montre le
* Chiffre le plus efficace* - c'est-à-dire le chiffre qui utilise le moins de
chiffres pour une quantité donnée de facteurs principaux

Nombre de chiffres utilisés
C'est-à-dire qu'il n'y a pas de lien entre les deux.
- Oui.
22,0 4,0 1,0
2 · 3
32,0 9,0 1,0
Dénomination des marchandises
C'est vrai.
D'après les résultats de l'enquête
Dénomination des marchandises

En utilisant les chiffres de ce tableau, le nombre de chiffres
sont nécessaires pour réaliser un ensemble donné de facteurs principaux est
minimisé.
Après cela, pour une valeur numérique minimale, les chiffres doivent être triés
dans l'ordre croissant.

-----------------------------------------------------------------------------------

C'est vrai. 2. Algorithme

Pour chaque essai

«» "
1. Lisez k, n, t.
2. factorise t dans les exposants de 2,3,5,7.
si t contient un autre facteur principal → NON SOLUTION
3. Produire le multiset de chiffres décimaux qui réalise le facteur
exposants avec le plus petit nombre possible de chiffres.
(Gredy, en utilisant le tableau de la section 1)
4. Si la quantité de chiffres produits > n
→ PAS DE SOLUTION
5. Construire le nombre en triant de plus en plus les chiffres produits.
Qu'il soit candi.
6. Si cand < k
→ PAS DE SOLUTION
7. Sinon, sortie cand
«» "

-----------------------------------------------------------------------------------

C'est vrai. 3. Preuve d'exactitude

Nous prouvons que l'algorithme fournit une réponse correcte pour chaque test
C'est une affaire.

---

Lemma 1
Si `t` contient un facteur primaire autre que `2,35,7`, alors aucune décimale
numéro a produit `t`.

**Prof.**
Chaque chiffre décimal n'a de facteurs principaux que parmi les "2,35,7".
Le produit de n'importe quel nombre de chiffres décimaux est donc un produit
ces premiers seulement, il ne contient jamais un autre facteur premier. *



Lemma 2
Le multiset de chiffres produit en step 3 réalise la factorisation
et utilise le plus petit nombre possible de chiffres.

**Prof.**
Considérez une quantité fixe de facteurs principaux de chaque type.
Le tableau de la section 1 présente, pour chaque facteur principal, un chiffre qui :
a besoin du plus petit nombre de décimales pour réaliser ce facteur.
Par conséquent, en utilisant les chiffres du tableau
supprime les principaux facteurs de la factorisation de «t»
exactement aussi vite que possible.
Par conséquent, après l'étape de remplacement avide le nombre de produits
nombres est minimal parmi tous les nombres multisets qui réalisent le facteur
exposants de "t".



Lemma 2
Parmi tous les nombres décimaux dont le chiffre multiset est celui obtenu en
step 3 la plus petite valeur numérique est celle obtenue par tri
les chiffres de plus en plus.

**Prof.**
Laissez `S` être le multiset de chiffres qui réalise `t`.
Tout nombre décimal qui utilise exactement le multiset `S` se compose du
chiffres de `S` dans un certain ordre.
Tri de `S` en ordre ascendant donne un nombre qui est lexicographique
pas plus grand que toute autre commande du même multiset, par conséquent
il est numériquement minimal. *



Lemma 3
Si l'algorithme produit un nombre `cand` dans step 7, alors
`cand` satisfait à toutes les contraintes du problème.

**Prof.**

* Par la construction des chiffres (step 3) le produit du
les chiffres sont égaux à `t`, donc `product(cand)=t`.
* Le nombre de chiffres produits ne dépasse jamais `n` (step 4),
par conséquent "longueur(cand) ≤ n".
* Dans step 6, nous avons vérifié `cand ≥ k`.
Ainsi `cand` est un certain nombre de longueur au plus `n` et le produit `t`
qui n'est pas inférieur à la limite inférieure requise "k".



Lemma 4
Si l'algorithme sort **NO SOLUTION** alors aucun nombre valide n'existe.

**Prof.**
L'algorithme peut sortir **NO SOLUTION** en quatre différents
situations:

1. Un facteur principal autre que `2,35,7` a été trouvé.
Par Lemma 1 aucun numéro avec le produit `t` n'existe.
2. La quantité de chiffres produits dépasse `n`.
Tout numéro avec le produit `t` doit contenir au moins les chiffres de
multiset produit dans step 3, donc il contient au moins
que beaucoup de chiffres, donc plus long que `n`.
3. Le "cand" construit est plus petit que le "k".
Tous les nombres qui réalisent le même ensemble de nombres sont
permutations de "cand"; la plus petite permutation est "cand" "
elle-même (Lemma 2).
Par conséquent, chaque numéro avec le produit `t` et au plus `n` chiffres
est inférieur à "k".
4. Le multiset contient un facteur primaire autre que "2,35,7".
Comme dans 1. le produit ne peut pas être atteint.

Dans chaque cas, aucun nombre ne peut satisfaire aux contraintes. *



Lemma 5
Si l'algorithme produit un nombre `cand` dans step 7, alors
`cand` est le plus petit nombre décimal avec le produit `t` et la longueur
au plus `n` qui n'est pas plus petit que `k`.

**Prof.**
Tous les nombres décimaux avec le produit `t` et au plus `n` doivent utiliser
un ensemble de chiffres qui réalise la factorisation de «t».
Par Lemma 2 le nombre minimal de chiffres que tout multiset peut
contient celui produit dans step 3.
Par conséquent, chaque autre numéro admissible a au moins autant de chiffres
comme "cand".
Si il a plus de chiffres, il est plus grand que n'importe quel nombre avec le même
nombre de chiffres parce que son chiffre de tête est au moins `1`
Des chiffres supplémentaires ajoutent de la valeur.
Si elle a le même nombre de chiffres, alors elle doit être différente
permutation du même multiset.
Parmi toutes les permutations d'un multiset fixe le plus petit numériquement
est obtenu en triant les chiffres de plus en plus (Lemma 2).
Ainsi, le "cand" n'est pas plus grand que tout autre nombre admissible.

Enfin, dans step 6, nous avons rejeté tous les nombres inférieurs à `k`.
Par conséquent, le nombre restant `cand` est le plus petit nombre admissible
qui est au moins `k`.



C'est vrai. Théorème
Pour chaque cas d'essai, l'algorithme imprime le numéro requis s'il est
existe, sinon il imprime **NO SOLUTION**.

**Prof.**
Si l'algorithme imprime un nombre, Lemma 5 garantit que
nombre satisfait toutes les contraintes et est le plus petit possible.
Si elle imprime **NO SOLUTION**, Lemma 4 indique qu'aucune
nombre existe. Par conséquent, l'algorithme est correct. *



-----------------------------------------------------------------------------------

C'est vrai. 4. Analyse de la complexité

Laisser `P = sqrt(t)`.

*Factorisation* – tout au plus divisions "O(P)".
Toutes les autres opérations sont linéaires dans la quantité de chiffres qui sont
produit, c'est-à-dire au plus `O(n)'.

«» "
Temps : O( √t + n ) par cas d'essai
Mémoire : O( n )
«» "

-----------------------------------------------------------------------------------

C'est vrai. 4. Mise en œuvre des références (Python 3)

'`python
importations
importer des maths

♪ ----------------------------------------------
# helper: factorise t en exposants de 2,35,7
♪ ----------------------------------------------
déf factorize(t):
cnt = {2:0, 3:0, 5:0, 7:0}
pour p in (2,3,5,7):
alors que t % p == 0 & #160;:
cnt[p] += 1
t //= p
# si quelque chose reste → un facteur principal en dehors de 2,35,7
retour cnt, t

♪ ----------------------------------------------
# produire le multiset avec le plus petit nombre de chiffres
♪ ----------------------------------------------
def produce_digits(cnt):
res = []
# utiliser les chiffres efficaces d'abord
# 2^3
alors que cnt[2] >= 3 :
res.append('8')
cnt[2] -= 3
# 3^2
alors que cnt[3] >= 2 :
res.append('9')
cnt[3] -= 2
# 2 * 3
alors que cnt[2] >= 1 et cnt[3] >= 1 :
res.append('6')
cnt[2] -= 1
cnt[3] -= 1
N° 2
alors que cnt[2] >= 2 :
res.append('4')
cnt[2] -= 2
# 2 et 3 restants
alors que cnt[2] >= 1 :
res.append('2')
cnt[2] -= 1
alors que cnt[3] >= 1 :
res.append('3')
cnt[3] -= 1
# 5 et 7
alors que cnt[5] >= 1 :
res.append('5')
cnt[5] -= 1
pendant que cnt[7] >= 1 :
res.append('7')
cnt[7] -= 1
retour res

♪ ----------------------------------------------
# Résolveur principal
♪ ----------------------------------------------
résoudre():
il = iter(sys.stdin.read().strip().split())
hors_lignes = []
Essayez :
alors que Vrai:
k = int(next(it))
n = int(next(it))
t = int(next(it))

# factorise t
cnt, repos = factorize(t)
Si vous vous reposez != 1 :
out_lines.append("NO SOLUTION")
poursuivre

nombres = nombres de produits(cnt)
si len(chiffres) > n:
out_lines.append("NO SOLUTION")
poursuivre

cand = ''.join(trié(chiffres))
si int(cand) < k:
out_lines.append("NO SOLUTION")
Sinon:
out_lines.append(cand)
Sauf StopItération:
passer

sys.stdout.write("\n".join(out_lines))

si __nom__ == "__main__" :
résoudre()
«» "

Le programme suit exactement l'algorithme prouvé correct ci-dessus.