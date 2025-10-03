---
titre: LeetCode 2595. Nombre d'even et de bits étranges -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## LeetCode Master 2595 – Nombre de bits identiques et étranges
* Apprenez comment le résoudre en **Java, Python et C++** et ace votre prochaine interview d'ingénierie logicielle. *

---

Table des matières

Lien
- Oui.
#problème-déclaration Autres
Aperçu de la solution
Bien, mal, C'est un mauvais coup
Approche Bit-Mask Autres
Code Extraits de code
Complexité
Cas et pièges des bords
#interview-tips
Autres options
Résumé #résumé

> ** Mots-clés du référencement**: *LeetCode 2595, Nombre de bits even et Odd, manipulation de bits, Solution Java, Solution Python, C++, codage d'entretien, entretien d'emploi, ingénieur logiciel, bitmasking, popcount, conseils d'entretien de codage*

---

Déclaration du problème

> **Don** un entier positif "
> **Retour** un tableau `[même, impair]` où:
> * `even` = nombre de bits **even-indexed** (0-based from the right) qui sont définis à `1`
> * `odd` = nombre de bits **odd-indexés** qui sont définis à `1`

**Les indices** sont comptés du bit le moins significatif (LSB) au bit le plus significatif (MSB), à partir de `0`.

**Exemples**

"n"" Binary" Even-index 1s) Odd-index 1s) Output
- C'est quoi ?
(indices 1,5) Autres
1 (index 1) Autres

**Contrôles* *

«» "
1 <= n <= 1000
«» "

---

## Aperçu de la solution

Démarche Idées Complexité Quand utiliser
- C'est quoi ?
**Bit‐Masque & Popcount**=Utilisez deux masques alternés ('0b010101...` & `0b101010...`) pour isoler des bits pairs et impairs, puis comptez les bits avec un popcount intégré.= **O(1)** time, **O(1)** space=Production‐grade, interview‐friendly=
**Convertissez `n` en chaîne binaire, itérer de LSB en MSB et incréments des compteurs basés sur la parité des indices. **O(log n)** temps, **O(log n)** espace
**Manual Bit Loop**= Shift `n` droite chaque itération, vérifiez LSB, basculez la parité de l'indice.== **O(log n)** temps, **O(1)** espace=== Éducation, si les constructions ne sont pas autorisées==

La méthode **Bit‐Mask & Popcount** est la méthode « good » – courte, efficace et démontre la maîtrise de la manipulation des bits.

---

Bien, mal, Méchant

Que faire pour éviter
- C'est quoi ?
Utiliser des masques bitwise + popcount intégré (p. ex. `Integer.bitCount`). Tout ce qui lie sur toute la chaîne binaire sauf si vous devez. Autres
**Créer une chaîne de caractères lors du débogage, mais pas en production. Oublier que les indices commencent à `0`. Autres
**Ugly**. Maintenez manuellement les compteurs et la parité d'indice dans un bloc `if/else` qui est enchevêtré. Écrire un long masque codé dur comme `0b0101010101101` sans explication. Autres

---

Approche Bit-Mask

1. **Masques**
* Même indices (0, 2, 4, ...) → binaire `010101... "
* Indices bizarres (1, 3, 5, ...) → binaire `101010... "

En décimale:
* Même masque = `0b0101010101` = `341` (pour les nombres jusqu'à 10 bits; vous pouvez le générer programmatiquement si vous voulez).
* Masque distant = `0b1010101010` = `682`.

2. **Appliquer et compter**
* `even = popcount(n & evenMask)`
* `odd = popcount(n & impairMask)`

3. **Retour** "

---

Numéro de code

### Java

"Java
solution de classe {
[] mêmeOddBit(int n) {
// Même indices: 0,24,... -> 0b01010101 (341)
// Indices extrêmes: 1,3,5,... -> 0b1010101010 (682)
= 0b0101010101;
mask = 0b1010101010; // 682
même = Integer.bitCount(n & evenMask);
int impair = Integer.bitCount(n & impairMask);
retour de nouveau int[]{even, impair};
}
}
«» "

Une seule ligne (Java 17+)

"Java
[] mêmeOddBit(int n) {
retourner les nouveaux int[]{Integer.bitCount(n & 0b0101010101), Integer.bitCount(n & 0b10101010)};
}
«» "

---

Python

'`python
Solution de classe:
def evenOddBit(self, n: int) -> Liste[int]:
even_mask = 0b0101010101 # 341
_masque impair = 0b1010101010 # 682
even = (n & even_mask).bit_count()
impair = (n & impair_mask).bit_count()
retour [même, étrange]
«» "

#### One-liner (Python 3.10+)

'`python
Solution de classe:
def evenOddBit(self, n: int) -> Liste[int]:
retour [(n & 0b10101101).bit_count(), (n & 0b01010110).bit_count()]
«» "

---

C++

'`cpp
solution de classe {
public:
vecteur<int> evenOddBit(int n) {
// Même indice masque: 0b0101010101 (341)
// Odd indices masque: 0b1010101010 (682)
dans evenMask = 0b0101010101;
Int impairMask = 0b1010101010;
int même = __constructin_popcount(n & evenMask);
int impair = __constructin_popcount(n & impairMask);
retour {même, impair};
}
};
«» "

#### One-liner (C++14+)

'`cpp
vecteur<int> evenOddBit(int n) {
retourner {_builtin_popcount(n & 0b01010101), __builtin_popcount(n & 0b101001010)};
}
«» "

---

Complexité

Opération Temps Espace
- C'est quoi ?
Bit-Masque + Popcount
Conversion des chaînes
Une boucle manuelle

Pour `n <= 1000` les différences sont négligeables, mais l'approche bit-mask est *universellement* optimale.

---

Cas et pièges

Piège
- Oui.
Utiliser `i % 2 == 0` pour pair, `i % 2 == 1` pour impair, en comptant à partir de LSB (index inverse). Autres
Autres Mauvaise taille de masque Les masques doivent couvrir tous les bits qui peuvent apparaître dans `n`. Pour les entiers 32 bits, utiliser `0x555555' (même) et `0xAAAAAA' (odd). Autres
Autres Ne pas utiliser le popcount intégré. Autres
En supposant que `n` est zéro. Autres

---

Conseils d'entrevue

1. **Exposer la logique bit-mask**: Montrez que les indices même et étrange alternent; nous pouvons donc créer un masque qui correspond à ces positions.
2. **Afficher pourquoi popcount est efficace**: C'est du temps accéléré et constant pour les tailles fixes de mots.
3. **Discuse les alternatives brièvement**: Mentionnez la conversion des chaînes et la boucle manuelle pour démontrer la rigueur, mais argumentez rapidement pourquoi elles sont suboptimales.
4. **Parler de l'évolutivité**: Pour `int` vs `long`, il suffit de changer les constantes du masque (`0x55555555`, `0xAAAAAA`).
5. **Temps-espace compromis**: Soulignez le temps et l'espace constants, qui est une caractéristique d'une bonne réponse d'entrevue.

---

(Si vous devez éviter les constructions)

### Comptage manuel des bits

"Java
[] mêmeOddBit(int n) {
Int même = 0, impair = 0, idx = 0;
pendant que (n != 0) {
si (n & 1)] 1) {
si (idx % 2] 0) pair++;
sinon impair++;
}
n >>= 1;
idx++;
}
retour de nouveau int[]{even, impair};
}
«» "

Conversion des chaînes

'`python
def evenOddBit(n):
bits = bin(n)[2:]::-1) # LSB d'abord
even = sum(1 pour i, b dans l'énumération(bits) si i % 2 == 0 et b == '1')
impair = somme(1 pour i, b dans l'énumération (bits) si i % 2 == 1 et b == '1')
retour [même, étrange]
«» "

Il s'agit là d'une excellente solution pour les besoins *éducatifs* ou les langues qui manquent de popcount.

---

Résumé

- La méthode **Bit‐Mask + Popcount** est la plus rapide, la plus concise et présente une compréhension approfondie des opérations bit.
- Pour `n <= 1000`, toute solution passe, mais les intervieweurs attendent l'approche à temps constant.
- Des masques comme `0b0101010101` (`341`) pour le même et `0b10101010` (`682`) pour les indices impairs isolent les bits en un seul coup.
- Intégrés (`Integer.bitCount`, `_builtin_popcount`, `.bit_count()`) font du code une seule ligne – idéal pour les entretiens de codage.

> **Rappelez-vous**: Afficher le masque → appliquer → popcount → retourner. C'est tout ce que vous devez impressionner.

---

La pensée finale

Les problèmes de manipulation bit sont une base d'entretiens techniques. Maîtriser celui-ci non seulement vous débarque le tableau `[même, impair]` en temps constant, mais vous donne aussi un modèle réutilisable pour une large gamme de questions liées aux bits. Bon codage !

---

> **Vous voulez plus d'entrevues?** Consultez mes autres guides sur *deux-sum*, *les bits inversés* et *les bits de compte* – tous optimisés pour le succès de l'entrevue.