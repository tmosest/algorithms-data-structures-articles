---
titre: LeetCode 1611. Minimum un bit opérations pour faire zéro entier -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 1611 – Minimum un bit opérations pour faire zéro entiers
*(LeetCode – Hard, Bit‐Manipulation, Job‐Interview Favorite)*

> **Objectif:** Transformer un entier `n` en `0` en utilisant les opérations de bits autorisés *fewest*.

Opération Conditions
C'est quoi ?
Il est possible de retourner à tout moment. Autres
Autres Dépliez le morceau `i` (i ≥ 1)= Nécessite bit `i‐1` = `1` **et** tous les bits inférieurs (`i‐2 ... 0`) = `0`.

Retourner le nombre minimum d'opérations.

> **Exemple**
> `n = 3 (binaire 11)` → opérations `2`
> `3 → 1 (déplier le bit) 0) → 0 (dépôt 1)»

---

Pourquoi ce problème se pose-t-il pour les entrevues

* **Le raisonnement de niveau Bit** – montre la maîtrise de la manipulation de données de bas niveau.
* **PDD non évident / cupidité** – beaucoup de candidats essaient la force brute et se coincer.
* **Élégance mathématique** – le nombre optimal est égal au nombre de `1`s dans le code *inverse* gris de `n`.
* **Scales à 109** – nécessite une solution O(log n), pas une simulation naïve.

---

L'intuition derrière la formule optimale

Considérez la chaîne binaire de `n`.
Si nous **commençons à partir du plus important bit (MSB)** et **marchez vers la gauche**:

La Commission européenne a publié un rapport sur la mise en œuvre de la stratégie de Lisbonne. 0
C'est pas vrai.
0 0 0

*Lorsque le bit actuel est `1`, nous devons effectuer une opération de "carry-over" qui retourne un bit inférieur.
Si le bit à gauche est `0`, le chariot peut se propager jusqu'au bas, produisant le même nombre de flips que si nous avons commencé à partir de cette position. *

La récurrence clé:

«» "
f(n) = (2^k – 1) – f(n – 2^(k‐1))
«» "

où `k` est la position de la plus gauche `1` (0-basé).
Intuitivement, `2^k – 1` compte tous les flips qui se passeraient ** si nous avons commencé à partir d'un zéro propre** et devait définir ce MSB, tandis que le deuxième terme soustrait les flips -saved-- parce que nous avions déjà ce `1` là.

---

O(log n) Solutions

- Oui. 1. DP récursif (Python)

'`python
Solution de classe:
def minimum Opérations OneBit(self, n: int) -> Int:
@functools.lru_cache(Aucun)
def dp(x: int) -> Int:
si x <= 1:
retour x # 0 → 0, 1 → 1 (un flip)
# k: indice du bit le plus significatif
k = x.bit_longueur() - 1
retour (1 << k) - 1 - dp(x - (1 << (k - 1)))

retour dp(n)
«» "

*`bit_length()` est O(1) en CPython, rendant la complexité globale `O(log n)`. *

- Oui. 2. Trick itératif Bit (C++)

'`cpp
solution de classe {
public:
Int minimum Opérations d'unbit(int n) {
int res = 0;
pendant que (n) {
res = -res - (n ^ (n - 1)); // bit hack
n &= n - 1; // chute inférieure 1
}
abs(res) de retour;
}
};
«» "

*L'expression `n ^ (n-1)` isole le plus bas 1-bit, et le signe alternatif explique l'effet de portage. *

- Oui. 3. Le plus rapide des deux sens (Java)

"Java
solution de classe {
Int minimum public Opérations d'unbit(int n) {
Int ans = 0;
pendant que (n != 0) {
as = -ans - (n ^ (n - 1));
n &= n - 1;
}
retourner Math.abs(ans);
}
}
«» "

*La même logique que C++ – Les opérateurs bitwise de Java fonctionnent de la même manière. *

- Oui. 4. Code Greedy + Gray (Python – exemple)

'`python
def gris(n):
retour n ^ (n >> 1 )

Solution de classe:
def minimum Opérations OneBit(self, n: int) -> Int:
# nombre de 1 dans l'inverse Code gris de n
retourner bin(~gray(n)).count('1')
«» "

*Ceci montre la connexion plus profonde au code Gray mais est plus lent ('O(n)` bit ops). *

---

Analyse de complexité

L'approche Temps Espace
- C'est quoi ?
**O(log n)** (pile de récursion)
Un bit itératif Hack
Code gris

Tous répondent aux contraintes de LeetCode ('0 ≤ n ≤ 109').

---

Bien, mal, Méchant

Catégorie Ce qui s'est bien passé Pièges communs
- - Non. - Non.
**Bonne **• Solutions O(log n) élégantes<br>• Pas de table DP explicite nécessaire
**Bad**) • Simulation de la force brute (O(n)) → TLE<br>• Mauvaise interprétation de la seconde opération Conditions préalables • Oubliez les bits inférieurs doivent être la règle 0
**La mémorisation récursive peut frapper les limites de récursion dans Python < 3,7; • Cacher un grand espace d'état inutile (table PD plus grande que nécessaire) dans les langues où "n" pourrait atteindre 231-1 (Java int ok, C++ int ok, mais attention à déborder en étapes intermédiaires)

> ** Conseil professionnel :** Le signe alternatif ("res = -res - (n ^ (n-1)") est la solution la plus compacte* mais cache le raisonnement. Pour les intervieweurs, ** expliquer la récurrence** d'abord, puis montrer le bit hack.

---

Nombre de codes complets

### Python (3.10+)

'`python
importer des functools

Solution de classe:
def minimum Opérations OneBit(self, n: int) -> Int:
@functools.lru_cache(Aucun)
def dp(x: int) -> Int:
si x <= 1:
retour x
k = x.bit_longueur() - 1
retour (1 << k) - 1 - dp(x - (1 << (k - 1)))
retour dp(n)

Oui. démo ------------------
si __nom__ == "__main__" :
s = Solution()
print(s.minimumOneBitOperations(3)) # 2
imprimer(s.minimumOneBitOperations(6)) # 4
«» "

### C++ (GCC17)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Int minimum Opérations d'unbit(int n) {
int res = 0;
pendant que (n) {
res = -res - (n ^ (n - 1));
n &= n - 1; // chute bit le plus bas
}
abs(res) de retour;
}
};

// ------------------ démo ------------------
Int main() {
Solution s;
le nombre d'opérations << s.minimumOneBit(3) << '\n'; // 2
le nombre d'opérations << s.minimumOneBit(6) << '\n';
}
«» "

### Java (17)

"Java
solution de classe {
Int minimum public Opérations d'unbit(int n) {
Int ans = 0;
pendant que (n != 0) {
as = -ans - (n ^ (n - 1));
n &= n - 1;
}
retourner Math.abs(ans);
}
}

// ------------------ démo ------------------
classe publique {
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.minimumOneBitOperations(3)); // 2
Système.out.println(s.minimumOneBitOperations(6)); // 4
}
}
«» "

---

## Ohio SEO-Optimized Interview‐ Prêt Blog Post

> **Titre:**
> Comment faire pour éponger le LeetCode 1611 – Minimum un bit Operations (Python, C++, Java)

Introduction
> Commencez par un crochet : *=Vous avez fissuré le problème classique de "flip bits" mais pouvez-vous le faire dans O(log n)?==*

Récapitulation des problèmes
> Répétez le problème en anglais simple et donnez l'échantillon E/S.

Intuition et récurrence
> Divisez la règle de portage, illustrez avec un diagramme binaire, et écrivez la formule de récurrence.

Galerie de solutions
*Recursive DP → Itérative Bit Hack → Java Implementation → Gray Code Connection. *

C'est vrai. Tableau de complexité
Méthode Temps Espace
- Oui.

- Oui. Bon / mauvais / Méchant
Expliquez pourquoi la récursion est sécuritaire, pourquoi les TLE de force brute et pourquoi le bit-trick est caché.

Conseils d'entrevue
* Expliquez toujours la logique d'abord. (en milliers de dollars)
* Afficher la récurrence, puis le hack. (en milliers de dollars)
* Attention au débordement entier en étapes intermédiaires. (en milliers de dollars)

Conclusion et à emporter
> *La solution à 1611 est une gemme de manipulation de bits qui démontre le flair algorithmique. Maîtrisez-le, pratiquez-le sur LeetCode, et vous impressionnerez les recruteurs dans les entreprises de haute technologie. *

---

Comment ce blog aide votre recherche d'emploi

* **Mot-clé Rich** – LeetCode 1611, Minimum One Bit Operations, .....
* **Showcases Deep Knowledge** – Les recruteurs repèrent les candidats qui peuvent obtenir la récurrence optimale.
* ** Démo pratique** – Chaque démo linguistique imprime les réponses attendues, prêtes pour une entrevue de codage ou un portfolio GitHub.
* **Code propre et commenté** – Plus facile pour les recruteurs de copier et de comprendre.

> Astuce:** Poster cet article sur Medium, dev.to, ou votre blog personnel, et ajouter un lien dans votre curriculum vitae sous Projets d'Algorithme. Cela vous positionne comme un ingénieur *prêt à l'entrevue* capable de relever des défis difficiles.