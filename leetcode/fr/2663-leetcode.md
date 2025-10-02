---
titre: LeetCode 2663. Lexicographiquement la plus petite belle corde -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2663 – Lexicographiquement La plus petite belle corde
## Un problème de LeetCode, résolu en Java, Python et C++
> **TL;DR**
> • Greedy – scanner de droite à gauche, frapper un personnage, puis reconstruire le suffixe avec les plus petites lettres légales.
> • Complexité: **O(n)** temps, **O(1)** espace supplémentaire (à l'exception de la chaîne de sortie).
> • Travaux pour *n* jusqu'à **100 000** et *k* de 4 à 26.

---

Récapitulation du problème

* On vous donne une chaîne **beau** `s` de longueur `n` (`1 ≤ n ≤ 10^5`).
* Une corde est *beau* si
1. Chaque caractère se trouve dans les premières lettres `k` de l'alphabet (`a ... a+k-1`).
2. Aucune sous-chaîne de longueur ≥ 2 n'est un palindrome.
* Trouvez la belle corde **lexicographiquement plus petite** qui est ** strictement plus grande** que `s`.
* Si aucune telle chaîne n'existe, retournez une chaîne vide.

---

## Intuition & Idée de la race

Considérez la chaîne comme un "lock" que nous voulons ouvrir au prochain état valide.

1. **Déplacer de droite à gauche**:
À partir de la dernière position, essayez d'augmenter ce caractère.
*Pourquoi droite à gauche? *
Parce que le suffixe qui vient après la position modifiée doit être reconstruit aux caractères les plus petits possibles ; nous ne pouvons pas nous permettre d'augmenter un caractère plus à gauche si un accroissement lexicographique plus petit existe à droite.

2. **Création juridique**
Incrément `s[i]` jusqu'à ce qu'il devienne une lettre ≤ `'a'+k-1`.
Après chaque incrément, nous devons vérifier que le nouveau caractère ne **pas** égal
* `s[i-1]` (pas de deux caractères égaux consécutifs) et
* `s[i-2]` (prévient un palindrome de 3 longueurs).

Si les deux contrôles passent nous avons trouvé la position la plus à gauche où nous pouvons frapper la corde.
Si `s[i]` atteint `'a'+k-1` et échoue toujours les vérifications, nous déplaçons une étape à gauche (`i--`) et répétons.

3. **Reconstruire le suffixe**
Une fois que nous avons un préfixe valide `s[0...i]`, le suffixe `s[i+1...n-1]` doit être la **lexicographiquement la plus petite** belle finition.
Pour chaque position `j` après `i` nous choisissons la plus petite lettre de l'ensemble `{a, b, ..., a+k-1}` qui est différent de `s[j-1]` et `s[j-2]`.
Parce que nous choisissons toujours la plus petite lettre possible, toute la chaîne sera la plus petite lexicographiquement parmi toutes les chaînes qui sont plus grandes que l'original.

4. **Aucune solution**
Si nous sortons de l'extrémité gauche (`i < 0`) cela signifie que nous ne pouvions trouver aucun accroissement légal, donc retourner `"".

---

La preuve de l'exactitude

Nous prouvons que l'algorithme renvoie la chaîne souhaitée ou les rapports correctement qu'aucune n'existe.

1. ** Existence d'un accroissement**
Si une plus grande belle corde existe, il doit y avoir une position "i" telle que
* `s[i] < 'a'+k-1` et
* Augmenter `s[i]` par au moins 1 garde la corde belle.
L'algorithme examine toutes les positions de droite à gauche et s'arrête à la première où un accroissement est possible. Ainsi, si une solution existe, l'algorithme trouvera un 'i' valide.

2. ** minimalité lexicographique du préfixe**
L'algorithme ne change jamais de caractère à gauche de `i`. Toute autre solution qui change un caractère gauche de `i` serait lexicographiquement plus grande parce que la position antérieure change à une lettre supérieure.

3. ** Minimum lexicographique du suffixe**
Une fois le préfixe fixé, chaque position `j > i` est réglée à la plus petite lettre qui maintient la beauté avec ses deux prédécesseurs.
Tout autre choix à la position `j` qui est plus grand rendrait l'ensemble de la chaîne lexicographiquement plus grand, et le choix d'une lettre plus petite briserait la contrainte beauté.
Ainsi le suffixe construit est le plus petit possible.

Combinant 1‐3, l'algorithme renvoie la plus petite belle chaîne qui est strictement plus grande que `s`. Si aucun tel `i` n'existe, aucune plus grande belle corde ne peut être formée, donc la réponse est `"".

---

## Cas de bord et pièges

Scénario Pourquoi ça compte Comment l'algorithme le gère
C'est ce qu'on dit.
**k = 4** (minimum autorisé)= Seules les lettres `a‐d` existent → les contraintes du palindrome sont plus serrées. La reconstruction suffixe utilise l'ensemble complet « {a,b,c,d} ». Autres
**s utilise déjà les plus grandes lettres**. La boucle va diminuer `i` après la fin gauche → retourner `""`. Autres
Autres **Longueur de la boucle = 1** L'algorithme fonctionne toujours; il n'existe aucun indice `i-1` ou `i-2`. Autres
Toutes les lettres alphabétiques autorisées. La logique reste identique; le suffixe peut utiliser l'une des 26 lettres. Autres
Autres **Ficelle très longue (10^5)** Besoin d'un temps linéaire. Autres

---

Code

Voici des implémentations propres et bien commentées dans **Java**, **Python** et **C++**.
Toutes les solutions suivent la même stratégie gourmande décrite ci-dessus.

- Oui. 1. Java

"Java
Importation de java.util.*;

solution de classe publique {
publique MagnifiqueString(String s, int k) {
char[] ch = s.toCharArray();
int n = longueur maximale;
i = n - 1;

// ----- trouver la position de la bosse -----
pendant que (i >= 0) {
ch[i]++; // essayer la lettre suivante
si (ch[i] - 'a' == k) { // a dépassé la plage autorisée
i--;
poursuivre;
}
Si [(i - 1 < 0) ch[i] != [i - 1]) &&
(i - 2 < 0) ch[i] != [i - 2]) {
casse; // bosse valable trouvée
}
}

si (i < 0) retourner "; // pas de plus grande chaîne belle

// ----- reconstruire le suffixe avec les plus petites lettres possibles -----
pour (int j = i + 1; j < n; j++) {
// choisir la plus petite lettre qui ne correspond pas
// le précédent ou le deux pas en arrière
pour (int x = 0; x < k; x++) {
Cand char = (char) ('a' + x);
si (j - 1 >= 0 && cand == ch[j - 1]) continuer;
si (j - 2 >= 0 && cand == ch[j - 2]) continuer;
ch[j] = cand;
pause;
}
}
retourner la nouvelle chaîne(ch);
}
}
«» "

- Oui. 2. Python

'`python
Solution de classe:
def plus petitBeautifulString(self, s: str, k: int) -> str:
chars = liste(s)
n = len(chars)
i = n - 1

# trouver la position la plus juste nous pouvons augmenter
alors que i >= 0:
Essayez la prochaine lettre
Chars[i] = chr(ord(chars[i]) + 1)
si chars[i] > chr(ord('a') + k - 1):
I -= 1
poursuivre

# Vérifiez la beauté
si (i - 1 < 0 ou chars[i] != Chars[i - 1]) et \
(i - 2 < 0 ou chars [i] != Chars[i - 2]:
pause
i < 0:
retour ""

# Rebâtir suffixe avec les plus petites lettres légales
pour j dans la plage(i + 1, n):
pour x dans la plage(k):
Cand = chr(ord('a') + x)
si j - 1 >= 0 et cand == chars[j - 1]:
poursuivre
si j - 2 >= 0 et cand == chars[j - 2]:
poursuivre
chars[j] = cand
pause

retourner "".join(chars)
«» "

- Oui. 3. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
string le plus petitBeautifulString(string s, int k) {
vecteur <char> ch(s.begin(), s.end());
int n = ch.size();
i = n - 1;

// trouver la position la plus droite qui peut être augmentée
pendant que (i >= 0) {
ch[i]++; // essayer la lettre suivante
si (ch[i] > char('a' + k - 1)) { // hors de portée
i--;
poursuivre;
}
Si [(i - 1 < 0) ch[i] != [i - 1]) &&
(i - 2 < 0) ch[i] != [i - 2]) {
casse; // bosse valide
}
}

si (i < 0) retourner "; // aucune solution

// Reconstruction du suffixe avec les lettres les plus petites possibles
pour (int j = i + 1; j < n; ++j) {
pour (int x = 0; x < k; ++x) {
char cand = char('a' + x);
si (j - 1 >= 0 && cand == ch[j - 1]) continuer;
si (j - 2 >= 0 && cand == ch[j - 2]) continuer;
ch[j] = cand;
pause;
}
}
retourner la chaîne(ch.begin(), ch.end());
}
};
«» "

Les trois codes fonctionnent en **temps linéaire** ('O(n)') et n'utilisent que quelques variables auxiliaires.

---

Testez votre solution

Texte
Entrée : s = "abcd", k = 4 → "abdc"
Entrée : s = "abdc", k = 4 → "abcd" (pas de chaîne plus grande)
Entrée : s = "a", k = 4 → "b"
Entrée: s = "zzz", k = 26 → ""
«» "

N'hésitez pas à coller les extraits dans l'éditeur en ligne de LeetCode et à exécuter les tests unitaires.

---

- Oui. Et si ça tourne ? – Bugs communs

Correction du bug
C'est pas vrai.
Utiliser `pour (char c : s)` en Java sans copier → modifie la chaîne d'origine. Autres
Peut tenter d'augmenter au-delà de `'a'+k-1''. Au lieu de "=="
Autres Reconstruire le suffixe avec seulement `{a,b,c}` quand `k>3`= Mauvaise réponse pour `k=26`= Iterate `x < k` (alphabet complet)=
Ignorer `i-2` lorsque `j < 2`= Mauvaise vérification du palindrome pour un suffixe court , Garde avec `si (j - 2 >= 0 && ...)` Autres

---

## Complexité temporelle et spatiale

Temps de mise en œuvre
C'est pas vrai.
Java **O(n)**
Python **O(n)**
* * * * * * * * *

L'algorithme n'a jamais besoin d'une file d'attente ou d'un tri prioritaire – nous essayons simplement la lettre suivante et effectuons des contrôles à temps constant.

---

- Oui. Pourquoi ce problème est-il un problème?

1. ** Contraintes claires** – La limite `n ≤ 100 000` vous oblige à penser aux solutions linéaires.
2. **Propreté grêle** – Les intervieweurs aiment des preuves concises qui justifient une approche avide.
3. ** Manipulation d'échelle + logique palindrome** – Un joli mélange de structures de données et de perspicacité algorithmique.
4. **Variants** – Le même modèle apparaît dans les problèmes concernant la permutation lexicographique suivante ou le mot de passe valide suivant, donc maîtriser il vous donne un outil réutilisable pour les questions futures.

Afficher cette solution dans un portfolio (Java, Python, C++) démontre :

* Compétence en plusieurs langues.
* Capacité d'écrire un code propre et prêt à la production.
* Forte compréhension des algorithmes avides et des preuves correctes.

---

## SEO–Résumé amical

- **Lexicographically Smallest Beautiful String** – Le mot clé pour lequel vous voulez vous classer.
- **LeetCode 2663** – Marque directement le numéro de problème pour les moteurs de recherche.
- ** Solution Java/Python/C++** – Donne aux intervieweurs une référence linguistique immédiate.
- **Codage d'entrevues d'emploi** – Indique la valeur réelle de ce tour algorithmique.
- ** Chaîne libre de Palindrome** – Ajoute de la profondeur pour les requêtes d'algorithmes avancées.

Utilisez les extraits de code et les explications ci-dessus dans votre prép d'entrevue, les billets de blog ou le portfolio pour faire une forte impression sur l'embauche des gestionnaires. Bon codage !