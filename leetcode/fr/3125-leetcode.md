---
titre: LeetCode 3125. Nombre maximum qui rend le résultat de Bitwise et Zéro -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3125. **Nombre maximal qui rend le résultat de Bitwise et Zéro** – Une plongée profonde
*(Code leet, moyen)*

> **Objectif**
> Pour un «n donné (1 ≤ n ≤ 10^15)» trouver le plus grand entier `x` tel que `x ≤ n` et
> `x & (x+1) & ... & n == 0`.

---

## TL;DR – La ligne unique

«» "
x = 2 * log2(n) – 1
«» "

En Java/C++/Python ceci devient :

Code de la langue
C'est quoi, ça ?
**Java**= Retour (1L << Long.SIZE-Long.number OfLeadingZeros(n)) — 1;
**C++**= Retour (1ULL << (63 - __constructin_clzll(n)) — 1;
**Python** - 1) - 1'

Tous fonctionnent dans **O(1)** temps et **O(1)** mémoire.

---

- Oui. 1. Pourquoi ça marche?

C'est le 1.1. La règle la plus significative (MSB)

Prenez n'importe quel numéro `n`.
Let `p = 2^k` être la puissance la plus élevée de deux qui est **. n** – c'est la valeur du bit le plus significatif défini dans `n`.

- Pour tout `x ≥ p`, le bit MSB de `x` est **1**.
- Pour tout 'x < p`, ce morceau est **0**.

Si nous effectuons un ET bitwise sur une plage consécutive qui comprend **oth** un `x ≥ p` et un `x < p`, le MSB du résultat deviendra **0**.

Pour faire le *tout* ET zéro nous devons forcer **chaque** bit à être 0.
Une fois que le MSB est mis à zéro, tous les bits inférieurs sont également à zéro parce que le ET de *any* entiers consécutifs qui s'étendent sur une puissance de deux limites aura toujours tous les bits inférieurs mis à zéro.
C'est pourquoi nous ne nous soucions que de l'ESM.

Oui. Pourquoi `2^k – 1`?

`2^k – 1` est le plus grand nombre qui a **all** bits en dessous de la MSB réglée à 1 et la MSB elle-même 0.
Parce qu'il est < `p`, son ET avec un nombre plus grand `≥ p` zérora le MSB (et donc l'ensemble du résultat).
De plus, c'est le **maximum** tel nombre parce que toute plus grande valeur aurait le MSB réglé à 1 et n'atteindrait jamais zéro quand ETed avec des nombres qui gardent ce bit 1.

---

- Oui. 2. Les trois voies de mise en œuvre

- Oui. Boucle droite (O(log n))

"Java
public long maxNombre(long n) {
long msb = 1;
alors que (msb << 1) <= n) msb <<= 1; // trouver 2^k
retour msb - 1;
}
«» "

Points positifs: Effacer, aucun compilateur intrinsèque.
Points négatifs: Un peu plus lent, mais toujours `O(log n)` (~50 itérations pour 10^15).

---

#### 2.2. Bit‐trick / intégré (O(1))

C'est vrai. Java

"Java
public long maxNombre(long n) {
int k = 63 - Long.numberOfLeadingZeros(n); // log2(n)
retour (1L << k) - 1;
}
«» "

C++

'`cpp
non signé long maxNumber(non signé long n) {
int k = 63 - __constructin_clzll(n); // log2(n)
retour (1ULL << k) - 1;
}
«» "

Python

'`python
def maxNombre(n: int) -> Int:
retour (1 << (n.bit_length()) - 1)) - 1
«» "

Tous utilisent les helpers compilateur-fourni bit-count, ce qui les rend vraiment à temps constant.

---

- Oui. Brute- Force (jamais pour la production)

'`python
def maxNombre(n):
pour x dans la plage(n, 0, -1):
si (réduire(lambda a,b: a & b, range(x, n+1))) 0:
retour x
«» "

**Pourquoi l'éviter? **
"O(n)" temps, échoue les contraintes (n peut être 10^15). Inclus uniquement pour l'exhaustivité.

---

- Oui. 3. Bonne, mauvaise et laid

Aspect du bien
- C'est quoi ?
**Complexité du temps**= Temps constant, pas de boucles== La boucle O(log n) est bonne pour 10^15== Brute-force O(n) serait time‐out===
Autres **Complexité spatiale**
**Code Clarté** , utilise bit_length , Légèrement verbeux mais lisible , La boucle naïve avec beaucoup de `if`s peut être confus ,
Autres **Causes d ' hypothèques** Aucun Autres
**Caractéristiques de la langue**
**Pièges potentiels**= Débordement entier en langues avec ints 32 bits (Java int)= Oublier `long`/`non signé long` Aucun

---

- Oui. 4. SEO-Optimized Blog Titre & Meta

**Titre:**
`LeetCode 3125 – Nombre maximal qui rend Bitwise ET Zero – Solutions Java, Python, C++ "

**Meta Description:**
> Master LeetCode 3125 en quelques secondes. Apprenez la solution d'un liner, comprenez la logique bit-wise et voyez le code Java, Python et C++. Idéal pour la préparation et le codage des entrevues.

**Mots clés de la cible:**
* Code Leet 3125
* Nombre maximal bitwise ET zéro
* Bitwise ET question d'entrevue
* Opérations bitwise Java
* manipulation de bits de Python

---

- Oui. 5. Billet de blog complet (SEO-Amis)

```markdown
Code Leet 3125 – Trouvez le plus grand X où ET de [X, N] est zéro

**Difficulté:** Moyenne
**Catégorie:** Manipulation bit, mathématiques
**Tags:** #LeetCode #Bitwise #Interview #CodingInterview

## Déclaration du problème

Compte tenu d'un entier `n` (1 ≤ n ≤ 1015), retourner le total maximal `x` de telle sorte que

«» "
x ≤ n
x & (x+1) & ... & n == 0
«» "

Intuition

Pensez à la représentation binaire.
La clé est le bit* le plus significatif (MSB) de `n`.
Que `p = 2^k` soit la puissance la plus élevée de deux ≤ `n`.
Tous les numéros de `p` jusqu`à `n` ont le bit MSB défini à `1`.
Si nous incluons un nombre `< p` dans la plage, l'ET effacera ce bit.
Le nombre le plus faible qui garantit que l'ESM est nettoyée tout en restant le plus grand possible est `p - 1`.

Ainsi:

«» "
réponse = 2^-log2(n) – 1
«» "

Analyse de complexité

*Heure:* **O(1)** (constante, sans boucles).
* Espace: * **O(1)**.

## Mise en œuvre

### Java

"Java
solution de classe publique {
public long maxNombre(long n) {
int k = 63 - Long.nombreOfLeadingZeros(n);
retour (1L << k) - 1;
}
}
«» "

C++

'`cpp
solution de classe {
public:
non signé long maxNumber(non signé long n) {
int k = 63 - _construitin_clzll(n);
retour (1ULL << k) - 1;
}
};
«» "

Python

'`python
Solution de classe:
def maxNumber(self, n: int) -> Int:
retour (1 << (n.bit_length()) - 1)) - 1
«» "

Bien, mal et mal

Aspect du bien
- C'est quoi ?
**Speed**
Un seul liner utilisant des lignes intégrées Aucun Les boucles trop compliquées peuvent masquer la logique
**Sécurité**=Poignées de 64 bits== L'oubli "long"/`long non signé long` peut déborder=================================================================================================================================================================================================================================

À emporter

La magie réside dans l'observation que l'ET des nombres consécutifs qui traversent une puissance de deux frontières effacera toujours tous les bits inférieurs.
En renvoyant simplement le nombre juste en dessous de la puissance la plus significative de deux, nous satisfions instantanément la condition.

Bonne chance pour vos entretiens !

«» "

---

- Oui. 6. Liste de contrôle finale

- Oui. [x] Solution monoligne en Java, C++, Python.
- [x] O(1) temps, O(1) espace.
- [x] Poignées jusqu'à 1015 (long/long non signé).
- [x] Article de blog avec des mots-clés SEO, structure, et bonne/mauvaise/meilleure analyse.
- [x] Commentaires de code pour plus de clarté.

Bon codage – et bonne chance à atterrir cette interview!