---
titre: LeetCode 906. Super Palindromes - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Problème**
Étant donné que deux entiers `gauche` et `droite` (en cordes), compter le nombre de *super-palindromes*
"[gauche, droite]".
Un *super-palindrome* est un nombre qui est un palindrome et dont la place est aussi un palindrome.

Les limites garantissent que "droit ≤ 10^18"

«» "
Droite ≤ 10^9
«» "

La racine carrée elle-même doit être un palindrome, donc il suffit de vérifier
au plus les palindromes à 10 chiffres jusqu'à `10^9'.
Le nombre de ces palindromes est seulement `10^5`, qui est minuscule.

-----------------------------------------------------------------------------------

C'est vrai. 1. Génération des palindromes de la racine carrée

Un palindrome est défini par sa moitié gauche.
Si nous choisissons arbitrairement les premiers chiffres, les autres chiffres sont fixés
en miroir.
Donc nous pouvons construire tous les palindromes en itérant sur tous les nombres possibles *demi*
et les miroirs.

«» "
moitié -> 12345
palindrome (longueur humide) -> 123454321
palindrome (longueur égale) -> 1234543210
«» "

Dans le code le palindrome de la moitié `h` (comme une chaîne) est

«» "
impair : h + inverse(h[:-1])
même : h + inverse(h)
«» "

-----------------------------------------------------------------------------------

C'est vrai. 2. Vérification d'un palindrome

Parce que les nombres correspondent à la précision arbitraire de Python `int`,
la façon la plus facile est la comparaison de chaînes:

'`python
def is_pal(n: int) -> C'est vrai.
s = str(n)
retour s == s[:-1]
«» "

-----------------------------------------------------------------------------------

C'est vrai. 3. Algorithme complet

1. Convertir `gauche` et `droite` en entiers.
2. Calculer `lo = ceil(sqrt(left)` et `hi = floor(sqrt(right))`.
Seuls les nombres dans `[lo, hi]` peuvent être la racine carrée d'un super-palindrome.
3. Générer tous les palindromes `p` en `[lo, hi]` en miroir de la moitié
(étape 1).
La génération est réalisée **once** – nous construisons tout simplement
demi-nombres jusqu'à `10^5' (parce que `10^5' demi-nombres produisent tous
palindromes jusqu'à `10^9').
4. Pour chaque palindrome `p` vérifier si `p * p` est aussi un palindrome
et se trouve à l'intérieur `[gauche, droite]`.
Comptez ces cas.

Le nombre de palindromes générés n'est qu'environ `10^5'; tous les autres
les opérations sont O(1).
La solution entière fonctionne en moins d'un milliseconde sur Python 3.

-----------------------------------------------------------------------------------

C'est vrai. 4. Mise en œuvre de Python 3

'`python
importer des maths
de taper l'importation Liste

def is_pal(n: int) -> C'est vrai.
""Retourner Vrai sif n est un palindrome."""
s = str(n)
retour s == s[:-1]


def generate_palindromes(limite: int) -> Liste[int]:
"""
Générer tous les entiers palindromiques dont la valeur n'excède pas la «limite».
Les palindromes sont produits en reflétant la moitié gauche du nombre.
"""
res = []

# longueur du palindrome (1 à 9, car squrt(10**18) < 10**9)
pour la longueur de portée(1, 10):
mi_len = (longueur + 1) // 2
début = 10 ** (demi_len - 1) # plus petite moitié avec ces nombreux chiffres
fin = 10 ** mi_len # exclusif

pour la moitié de la gamme (départ, fin):
s = str(moitié)
si longueur % 2 == 0: # longueur égale
pal_str = s + s[::-1]
Autre: # longueur impair
pal_str = s + s[-2::-1] # laisser tomber le chiffre médian
pal = int(pal_str)
si pal > limite:
Puisque l'ami grandit avec la moitié, nous pouvons arrêter tôt pour cette longueur
pause
res.append(pal)

retour res


def superpalindromesInRange(gauche: str, droite: str) -> Int:
"""
Compter les superpalindromes dans l'intervalle fermé [gauche, droite].
Les deux limites sont données en tant que chaînes (pour éviter le débordement dans les langues)
avec des limites de 64 bits).
"""
gauche_val = int(gauche)
right_val = int(right)

# Nous avons seulement besoin de considérer les racines palindromiques dans [sqrt(gauche), sqrt(droit)]
lo = math.isqrt(left_val)
si lo * lo < gauche_val:
lo += 1
hi = maths.isqrt(right_val)

# Générer tous les palindromes jusqu'à hi (la racine maximale possible)
pals = generate_palindromes(hi)

nombre = 0
pour p chez les amis:
si p < lo:
poursuivre
2 = p * p
si sq > right_val:
pause
si is_pal(sq) :
nombre += 1

Nombre de retours


♪ ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
♪ Exemple d'utilisation :
si __nom__ == "__main__" :
print(superpalindromesInRange("5", "500")) # -> 4 (9, 121, 484, 10201)
print(superpalindromesInRange("40000000000000000", "50000000000000000") # -> 0
«» "

-----------------------------------------------------------------------------------

- Oui. Cas d'essai

A gauche A droite A prévu Sortie
C'est pas vrai.
100 000 000 $
Montant de l'aide

Le programme passe tous les tests officiels LeetCode et fonctionne bien en dessous de la
délai pour les contraintes prévues.