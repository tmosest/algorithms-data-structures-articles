---
titre: LeetCode 2269. Trouvez la beauté K d'un nombre -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solutions 3 langues pour **Code de cap 2269 – Trouvez la beauté K d'un numéro**

Langue Fichier Complexité Notes
- C'est quoi ?
Autres Java, "Solution.java" **O(n · k)** temps, **O(1)** extra Utilise le `String.substring` intégré + `Integer.parse Int'. Fonctionne confortablement parce que `n ≤ 10`. Autres
Python "solution.py" **O(n · k)** temps, **O(1)** extra" Utilise le slice et la conversion `int()`. Autres
**O(n · k)** time, **O(1)** extra. Autres

> **Conseil pour les entrevues** – si le nombre était beaucoup plus grand, vous voudriez une mise à jour entière *sliding-window* au lieu d'analyses répétées.
> Ici nous gardons le code propre parce que les contraintes sont minuscules.

---

### Java

"Java
// 2269. Trouvez la beauté K d'un nombre
// Problème de LeetCode #2269
// Auteur: ChatGPT (adapté de l'éditorial officiel)

solution de classe publique {
secteur public Sous-chaînes(int num, int k) {
// Convertir le nombre en une chaîne une fois
Chaîne s = entier.toString(num);
int len = longueur s.();
nombre int = 0;

pour (int i = 0; i <= len - k; i++) {
// Extraire la sous-chaîne de longueur k
sous-chaîne = s.subchaîne(i, i + k);
int val = Integer.parseInt(sub); // Les zéros sont bons

// 0 n'est jamais un diviseur
si (val != 0 && num % val] 0) {
count++;
}
}
le nombre de retours;
}
}
«» "

---

Python

'`python
# 2269. Trouvez la beauté K d'un nombre
# Problème de LeetCode #2269
♪ Auteur: ChatGPT (adapté de l'éditorial officiel)

Solution de classe:
def divisorSubstrings(self, num: int, k: int) -> Int:
s = str(num)
n = len(s)
nombre = 0

pour i dans la plage (n - k + 1):
Sous = s[i:i + k]
val = int(sub) # zéros de tête autorisés
Si val != 0 et num % valeur == 0:
nombre += 1
Nombre de retours
«» "

---

C++

'`cpp
// 2269. Trouvez la beauté K d'un nombre
// Problème de LeetCode #2269
// Auteur: ChatGPT (adapté de l'éditorial officiel)

#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
divisant int Sous-chaînes(int num, int k) {
chaîne s = to_string(num);
int n = s.size(), cnt = 0;

pour (int i = 0; i <= n - k; ++i) {
chaîne de caractères sub = s.substr(i, k);
int val = stoi(sub); // Amende des zéros
si (val != 0 && num % val] 0)
++cnt;
}
retour cnt;
}
};
«» "

---

- Oui. 2. SEO-Optimized Blog Post

> **Titre**: *Cracking LeetCode 2269: -Trouver la beauté K d'un numéro – Java, Python et C++ Solutions + Conseils d'entrevue*

> **Description détaillée**:
> Apprenez à résoudre le LeetCode #2269 en Java, Python et C++. Comprendre l'algorithme, la complexité, les pièges et la façon de répondre à la question lors d'une entrevue de codage. Boostez votre score d'entrevue de codage aujourd'hui!

---

Introduction

Le problème de la K‐Beauté d'un nombre** est un puzzle classique LeetCode qui teste la manipulation de votre chaîne, la logique du diviseur et la manipulation de cas de bord.
Dans cet article, nous allons:

1. ** Expliquez le problème** en anglais.
2. Parcourez l'algorithme **core** et fournissez des solutions dans **Java, Python et C++**.
3. Discutez des aspects bons, mauvais et laids** – du code propre aux pièges potentiels.
4. Donner des conseils prêts à l'entrevue** et comment présenter la solution aux gestionnaires d'embauche.

Laissez plonger !

---

Récapitulation du problème

> **Définition**: Le *k-beauty* d'un entier `num` est le nombre de sous-chaînes de `num` (lorsqu'elles sont lues comme une chaîne) qui satisfont:
> 1. La longueur est égale à "k".
> 2. La valeur entière de la sous-chaîne se divise de façon égale.
> 3. `0` est **jamais** un diviseur (même si la sous-chaîne est ..

**Input**
- `num`: entier positif (`1 ≤ num ≤ 10^9`).
- `k`: entier positif (`1 ≤ k ≤ longueur num`).

** Sortie**
- Nombre entier de sous-chaînes admissibles.

**Exemples**

Entrée Sortie Explication
C'est pas vrai.
`num = 240`, `k = 2` Autres
`num = 430043`, `k = 2`, `2`, ``43'' se produit deux fois; '30, '00, '04' sont invalides. Autres

---

Idée de base

1. **Stringify** l'entier afin que nous puissions prendre des tranches contiguës.
2. **Slide** une fenêtre de taille `k` sur la chaîne.
3. Convertissez chaque fenêtre en un entier (les zéros principaux ne comptent pas).
4. Vérifiez deux conditions: 'val != 0` et `num % de valeur == 0`.
5. Incrémenter le compteur en conséquence.

Comme la longueur maximale de `num` est de 10, l'algorithme `O(n · k)` naïf est plus que rapide.

---

### Détails et code de la solution

Ci-dessous est l'implémentation **canonique** que vous verrez dans l'éditeur de LeetCode pour les trois langues.

C'est vrai. Java

"Java
solution de classe publique {
secteur public Sous-chaînes(int num, int k) {
Chaîne s = entier.toString(num);
nombre int = 0;
pour (int i = 0; i <= s.length() - k; i++) {
Int val = Integer.parseInt(s.substring(i, i + k));
si (val != 0 && num % val] 0) {
count++;
}
}
le nombre de retours;
}
}
«» "

Python

'`python
Solution de classe:
def divisorSubstrings(self, num: int, k: int) -> Int:
s = str(num)
nombre = 0
pour i dans la plage(lent(s) - k + 1):
val = int(s[i:i + k])
Si val != 0 et num % valeur == 0:
nombre += 1
Nombre de retours
«» "

C++

'`cpp
solution de classe {
public:
divisant int Sous-chaînes(int num, int k) {
chaîne s = to_string(num);
nombre int = 0;
pour (int i = 0; i <= s.size() - k; ++i) {
valeur int = stoi(s.substr(i, k);
si (val != 0 && num % val] 0)
+ nombre;
}
le nombre de retours;
}
};
«» "

**Complexité* *

- *Time*: `O(n · k)` (le pire cas ~ 100 opérations, trivial pour les processeurs modernes).
*Espace*: "O(1)" (signifier la chaîne d'entrée, qui fait partie du problème).

---

Bon, mauvais et affreux

Aspect du bien
- C'est quoi ?
**Readability**= Effacer les noms de variables (`s`, `val`, `count`). Aucune. Autres
**Cas d'escroquerie** > 4). Doit protéger contre la "val". 0' pour éviter la division par zéro. Oublier le garde fait le code s'écraser ou donner de mauvaises réponses. Autres
Avec `n ≤ 10` la solution naïve est bonne. Utiliser `Integer.parse Int` à l`intérieur d`une boucle peut se sentir lourd mais est négligeable. Autres Pour les entrées plus grandes, vous voulez une mise à jour entière *rolling* pour éviter une analyse répétée. Autres
Pour `num` > 2^31‐1 vous auriez besoin `long` ou `BigInteger`. Autres
**Idiomes de langue**= Java utilise `substring`; Python slicing; C++ `substr`.== Aucune.=Le mélange d'indices 0 et 1 conduit à des erreurs hors-par-un. Autres

---

### Conseils d'entrevue

1. **Exposer les contraintes en premier**
- `num` ≤ 10^9 → au plus 10 chiffres.
- `k` ≤ nombre de chiffres → la taille de la fenêtre ne dépasse jamais la longueur de la chaîne.

2. **Parler à travers les cas de bord* *
- Les zéros de tête → `int("00") = 0`.
- Règle zéro diviseur.
- Les sous-chaînes dupliquées (par exemple, "43" apparaissent deux fois dans "430043".

3. **Afficher un O(n · k) propre Exécution**
- Mentionnez qu'une mise à jour intégrale de la fenêtre coulissante pourrait réduire les facteurs constants, mais est inutile ici.

4. **Analyse du temps et de l'espace**
- Temps O(n·k), espace O(1).
- Pourquoi il répond aux contraintes du problème.

5. **Si vous avez demandé une version plus efficace* *
- Afficher l'approche de la fenêtre roulante :
«» "
val = valeur % pow10(k-1) * 10 + nouveau chiffre
«» "
Mais expliquez pourquoi il est trop compétent pour ce problème.

---

Pensées de clôture

Le défi « Trouver la beauté K d'un numéro » est trompeurment simple, mais il met en évidence l'importance de la manipulation des cas de bord** (leading zéros, division by zéro) et de la structure de code **claire**. Résoudre en Java, Python ou C++ démontre la pensée algorithmique du langage – une compétence clé d'interview.

N'hésitez pas à copier les extraits ci-dessus dans votre éditeur IDE ou LeetCode local. Bon codage, et que ce problème renforce votre confiance en l'entrevue! C'est ce qu'il a dit.

---

### Ressources & Lecture supplémentaire

- [LeetCode Problem 2269](https://leetcode.com/problèmes/find-the-k-beauty-of-a-number/)
- [Technique de fenêtre coulissante](https://leetcode.com/discuss/general-discussion/1172340/sliding-window-solution)
- [Éviter la division par zéro] (https://stackoverflow.com/q/1157228/)

---

**Référencement Mots clés:**
LeetCode 2269, Trouvez la beauté K-Beauty d'un Numéro, solution Java, solution Python, solution C++, interview de codage, algorithme, manipulation de chaînes, diviseur, conseils d'entrevue, préparation d'entrevue.