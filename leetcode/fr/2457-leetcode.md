---
titre: LeetCode 2457. Ajout minimum pour rendre l'entier beau -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2457. Ajout minimum pour rendre Integer belle
**Difficulté:** Moyenne

> Un entier est beau si la somme de ses chiffres est ≤ "cible".
> Trouvez le plus petit entier non négatif `x` tel que `n + x` est beau.

Vous trouverez ci-dessous une solution complète et prête à la production dans **Java**, **Python** et **C++**.
Après le code, vous lisez un court article de blog SEO optimisé qui explique
algorithme, discute le bon, le mauvais et le laid, et montre pourquoi il est un grand
sujet pour la préparation de l'entrevue.

---

- Oui. 1. Code

#### 1.1 Java

"Java
***
* 2457. Minimum d'ajout pour rendre l'entier beau
* Problème de LeetCode – Moyen
*/
solution de classe {

*** Aide qui retourne la somme des chiffres décimaux de n */
digitaux int privésSum(long n) {
= 0;
pendant la période (n > 0) {
somme += (int) (n % 10);
n/= 10;
}
la somme de retour;
}

public long makeIntegerBeautiful(long n, int cible) {
long original = n;
longue puissance = 1; // 10^k – le bloc courant que nous incrémenterons

pendant que (digitSum(n) > cible) {
// 1. Passer au prochain multiple de pouvoir
n = n / 10 + 1; // division entière – laisser tomber le dernier chiffre, ajouter 1
// 2. Restaurer les zéros de fuite
n *= puissance;
// 3. Augmenter le bloc pour la prochaine itération
puissance *= 10;
}

retour n - original; // le plus petit x qui rend le nombre beau
}
}
«» "

---

#### 1.2 Python

'`python
# 2457. Ajout minimum pour rendre Integer belle
# Code Leet – Moyen
Solution de classe:
def makeIntegerBeautiful(self, n: int, cible: int) -> Int:
original = n
puissance = 1

def digit_sum(x: int) -> Int:
somme de retour(int(d) pour d en str(x))

pendant que chiffre_sum(n) > cible:
n = n // 10 + 1 # sauter au bloc suivant
n *= puissance
puissance *= 10

retour n - original
«» "

---

*## 1.3 C++

'`cpp
// 2457. Ajout minimum pour rendre l'entier magnifique
// LeetCode – Moyenne
solution de classe {
public:
// helper: somme des chiffres décimaux
chiffre d'entrée statique Somme (longe x) {
= 0;
pendant que (x > 0) {
sum += static_cast<int>(x % 10);
x/= 10;
}
la somme de retour;
}

longue longue makeIntegerBeautiful(long long n, int cible) {
long original = n;
longue puissance = 1; // 10^k

pendant que (digitSum(n) > cible) {
n = n / 10 + 1; // aller au bloc suivant
n *= puissance; // remplir les chiffres inférieurs de 0
puissance *= 10; // augmenter la taille du bloc
}
n - original;
}
};
«» "

Les trois solutions fonctionnent dans **O(d log d)** time, où *d* est le nombre de chiffres de *n*
(maximum 13 pour `n ≤ 1012`), et utiliser **O(1)** espace supplémentaire.

---

- Oui. 2. Article de blog – Le bon, le mauvais, et l'indulgence de l'addition minimale pour rendre entier beau.

2.1 Introduction

Lors de la préparation d'une entrevue d'ingénierie logicielle, vous rencontrerez **LeetCode** des problèmes qui testent votre capacité à penser avec cupidité, utiliser des astuces arithmétiques et raisonner sur les opérations numériques.
Problème **2457 – Ajout minimum pour rendre Integer Beautiful** est un exemple classique.
Dans cet article, nous disséquons l'algorithme, en soulignons les avantages et les inconvénients, et nous vous montrons comment l'expliquer dans une interview.

**Mots clés**: *LeetCode 2457, ajout minimum pour rendre l'entier beau, algorithme d'entrevue, cupidité, somme des chiffres, Java, Python, C++ *

---

#### 2.2 Le bon – Pourquoi ce problème est un grand sujet d'entrevue

1. **Énoncé de problème clair* *
*Don* `n` et `cible`, *return* le minimum `x` de telle sorte que la somme des chiffres `n +` ≤ `cible`.
Il y a une seule réponse bien définie.

2. **Encourage la pensée gourmande* *
La solution optimale est de *arrondir* `n` au multiple suivant de `10`, puis `100`, puis `1000`, etc.
Cela démontre que vous pouvez faire un choix local optimal (en incrément le plus petit chiffre possible) qui mène à un résultat mondial optimal.

3. ** Implémentation rapide et propre* *
La solution est d'environ 10 lignes de code dans chaque langue.
Vous pouvez le terminer avant l'entrevue et vous concentrer sur l'explication du raisonnement.

4. **Manipulation des caisses**
Les contraintes garantissent l'existence d'une solution, mais vous devez toujours gérer les cas où la somme des chiffres est déjà ≤ "cible".
Démontrer comment détecter et raccourcir ce cas montre une pensée attentive.

5. **Language-agnostique**
L'algorithme n'utilise que des boucles complètes et simples – parfaites pour les interviews Java, Python ou C++.

---

2.3 Les mauvaises – Pièges communs

Comment éviter
C'est pas vrai.
**L'utilisation du module 10** sur l'ensemble du nombre à plusieurs reprises.
**En supposant que vous pouvez ajouter 1 à l'ensemble du nombre**
**Oubliant de mettre à jour `power`** , boucle infinie ou mauvaise réponse , après chaque itération multiplier `power` par 10 ,
**Utiliser la récursion sans mémorisation**

---

2.4 Le mauvais – Pourquoi certaines solutions vont mal

Parfois, les personnes interviewées tentent une force brute d'essayer chaque approche "x" ou d'utiliser une table **dynamique** de taille "cible".
Bien que théoriquement correctes, ces approches sont exagérées :

- **Brute-force** fonctionne en O(1012) dans le pire des cas, impossible dans les délais.
- **DP** sur la somme des chiffres n'est pas nécessaire; la propriété cupide "round-up" est beaucoup plus simple.
- Utiliser **strings** pour manipuler des chiffres (Python `str(n)`) peut conduire à des bugs subtils lors de la conversion en entier.

Un algorithme avide bien structuré, tel que présenté ci-dessus, évite tous ces pièges et maintient le code lisible et durable.

---

#### 2.5 Étape par étape

Laissez passer l'algorithme avec l'exemple `n = 467`, `cible = 6`.

"n" avant "digitSum(n)" Action "n" après
- C'est quoi ?
# 0= 467 # 17= >6 → arrondir à 10= 10+ multiple # 470 #
Un peu plus d'une centaine de fois
# 500 # 5 # ≤6 → stop #

La réponse est `500 - 467 = 33`, exactement comme le problème indique.

**Pourquoi ça marche ? **
Lorsque la somme des chiffres est trop élevée, la seule façon de la réduire est d'augmenter le chiffre le plus significatif qui peut affecter la somme tout en réinitialisant les chiffres moins significatifs à zéro.
Incrémenter le dernier chiffre ne réduirait pas assez la somme, donc nous avons à la prochaine valeur plus élevée.

---

2.6 Analyse de la complexité

Langue Heure Espace
- C'est quoi ?
Autres Java, Python, C++. **O(d log d)** (d = nombre de chiffres ≤ 13)

Puisque `d` est minuscule, l'algorithme fonctionne en microsecondes – parfait pour un réglage d'entrevue.

---

2.7 Comment expliquer Dans une interview

1. **Énoncer l'observation* *
*Si la somme des chiffres est trop grande, nous pouvons incrémenter en toute sécurité la valeur de la place suivante et zéror les chiffres inférieurs sans jamais augmenter la somme des chiffres au-delà de la nécessité. *

2. **Décrivez l'étape gourmande**
* À chaque étape, remplacer `n` par `(n // 10 + 1) * puissance`, où `puissance` commence à 1 et multiplie par 10 chaque itération. *

3. **Afficher la condition d'arrêt* *
*Quand `digitSum(n) ≤ cible`, nous sommes fait. *

4. ** Présenter la réponse finale**
*Retour `n - original_n`. *

4. **Cas de bord des peines**
*Si la somme des chiffres de l'original `n` est déjà bien, retourner immédiatement 0. *

5. **Facultatif – Marche en code**
*Voyez les lignes de code, en particulier la division, le report et la mise à jour de puissance. *

---

### 2.8 Conclusion

Problème 2457 vous enseigne un truc cupide soigné qui est à la fois élégant et rapide.
Il s'agit d'un **must-know** pour tout candidat visant à ace data-structure et questions d'algorithme sur *LeetCode* ou dans *interviews techniques*.

En maîtrisant ce problème, vous allez :

- Ayez confiance dans le raisonnement avide,
- Apprenez à garder le code concis à travers Java, Python et C++,
- Démontrer une communication claire avec les intervieweurs.

Bon codage et bonne chance avec votre préparation d'entrevue!