---
titre: LeetCode 1016. Chaîne binaire avec sous-chaînes représentant 1 à N -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Problème 1016 – Chaîne binaire avec sous-chaînes représentant 1 à N
> **LeetCode**

**Lien:** <https://leetcode.com/problems/binary-string-with-substrings-representing-1-to-n>

---

Déclaration du problème
Vous recevez une chaîne binaire `s` (seulement `0` et `1`) et un entier positif `n`.
Retour **`true`** iff *every* entier de **1 à `n`** (inclus) a son binaire
la représentation comme sous-chaîne de « s ». Sinon retourner **`false`**.

> **Exemples**
> 1. `s = "0110"`, `n = 3` → `true` (sous-chaînes `"1"`, `"10"`, `"11"`)
> 2. `s = "0110"`, `n = 4` → `faux` (sans `"100"`)

---

Pourquoi ce problème est une grande question d'entrevue
* ** Manipulation d'attache + bit-math** – teste la capacité de penser en dehors du DP pur.
* **Large `n` (1 000 000 000)** – force un algorithme efficace qui ne
Il y a des chiffres.
* **La longueur de `s` est minuscule (= 1000)** – nous pouvons utiliser une approche de fenêtre coulissante.

Il est parfait pour montrer le design algorithmique, les compromis temporels et le code propre en plusieurs langues.

---

L'idée fondamentale

**Aspect**
C'est pas vrai.
**Brute Force**= Fonctionne pour de petites entrées.== `O(n ·="s)= → impossible quand `n` est 109.= `indexOf` pour chaque nombre → quadratique. Autres
**Optimisé**=Scan `s` une fois, stocker toutes les sous-chaînes binaires jusqu`à la longueur `log2(n)+1`.=Il faut toujours vérifier chaque nombre jusqu`à `n`.=Si `n` est énorme, scanner 1...n est gaspillé, mais nous allons tôt sortir quand `n > setSize`.=
**Structure de données**== `HashSet<Integer>=` pour les recherches O(1).==Les collisions Hash sont rarement un problème. L'utilisation d'un tableau `int` de taille `n` est impossible (1 GB+). Autres
**Les sous-chaînes commençant par « 0 » sont invalides. Nombres avec des zéros de tête ignorés. Nécessité de convertir la sous-chaîne binaire en entier efficacement. Autres

L'élégante solution maintient la complexité limitée par "O(......log2(n)" qui, pour les contraintes données, est au maximum "30 × 1 000...30 000" opérations – trivialement rapides.

---

Mise en œuvre

Voici des implémentations propres, prêtes à coller dans **Java**, **Python** et **C++**.

> **Aide commune** – Calculer la valeur entière d'une sous-chaîne binaire pendant
> le scanner pour éviter les répétitions `Integer.parseInt`.

---

Java (O(S) 30 000)

"Java
Importation de java.util.*;

solution de classe publique {
/** Convertir la sous-chaîne binaire en int pendant la numérisation. */
binaire int privé ToInt(String s, int start, int len) {
Int val = 0;
pour (int i = démarrage; i < démarrage + len; i++) {
val = (val << 1)) (s.charAt(i) - '0');
}
valeur de retour;
}

requête publique booléenneString(String s, int n) {
// Longueur maximale de la représentation binaire de n
int maxLen = entier.toBinaryString(n).longueur();

// Conservez tous les numéros valides qui apparaissent comme sous-chaînes
Définir<integer> vu = nouveau HashSet<>();

pour (int i = 0; i < s.longueur(); i++) {
si (s.charAt(i) == '0') continue; // conduisant à zéro -> sauter
Int val = 0;
pour (int l = 1; l <= maxLen && i + l <= s.longueur(); l++) {
val = (val << 1)) (s.charAt(i + l - 1) - '0');
si (val > n) rupture; // pas besoin de conserver des valeurs plus grandes
voir.add(val);
}
}

// Un échec rapide si on ne peut pas couvrir tous les chiffres
si (n > vu.size()) retourne faux;

// Vérifier chaque numéro 1..n est présent
pour (int num = 1; num <= n; num++) {
si (!see.contient) retourner faux;
}
retour vrai;
}
}
«» "

---

Python (O(S) 30 000)

'`python
Solution de classe:
def requêteString(self, s: str, n: int) -> C'est vrai.
max_len = n.bit_longueur() # longueur de la représentation binaire
vu = set()

pour i, ch dans le(s) énuméré(s):
si ch == '0': continuer # sauter en tête des zéros
Valeur = 0
pour l dans la gamme(1, max_len + 1):
i + l > l(s): rupture
val = (val < < 1)) (ord(s[i + l - 1]) et 1)
si valeur > n: pause
voir.add(val)

si n > len(see): retourner Faux
retourner all(num dans vu pour num dans la plage(1, n + 1))
«» "

---

C++ (O(S) 30 000)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
requête boolString(string s, int n) {
maxLen = 32 - __constructin_clz(n); // longueur du bit de n
non ordonné_set<int> vu;

pour (int i = 0; i < (int)s.zize(); ++i) {
si (s[i] == '0') continuer; // aucun zéro de début
Int val = 0;
pour (int l = 1; l <= maxLen && i + l <= (int)s.size(); ++l) {
val = (val << 1)) (s[i + l - 1] - '0');
en cas de rupture (val > n);
voir.insérer(val);
}
}

si (n > (int)seen.size()) retourne false; // sortie anticipée

pour (int num = 1; num <= n; ++num)
si (!see.count(num)) retourne faux;
retour vrai;
}
};
«» "

---

Analyse de complexité

**Métrique**
- C'est quoi ?
**Java**="O(="s · log2(n)" ≤ 30 000 opérations="O(="s · log2(n)" pour le jeu de hachage (=" 30 000 entiers)="
Même
Même

Pourquoi c'est rapide :*
La boucle externe scanne la chaîne une fois.
La boucle intérieure tourne au maximum `maxLen = -log2 n--= 1 ≤ 30 ' fois par position.
Ainsi, le travail total est limité par "30 "s", négligeable pour "s" ≤ 1000.

---

Cas de bord et pièges communs

*Cas** **Explication**
- C'est quoi ?
Seulement la sous-chaîne `"1"' nécessaire. Autres
La chaîne commence avec de nombreux zéros.Les zéros de tête sont ignorés; seules les sous-chaînes commençant par `1` sont considérées. Sauter les indices où `s[i] == '0''. Autres
"n` plus grand que possible sous-chaînes uniques" Retour `false` tôt (`n > vu.size()`). Aide à éviter les boucles inutiles sur grand `n`. Autres
Utiliser le déplacement de bits sur `int`; valeur maximale ≤ 231-1. Autres
Empty string "s" longueur ≥ 1 par contrainte, mais garde quand même. Retour `faux`. Autres

---

Autres approches

1. **Trie / Préfixe Tree** – Insérez toutes les sous-chaînes de `s` dans un trie, puis marchez
de `1` à `n` en binaire pour voir si le chemin existe.
*Pros:* Structure claire, fonctionne pour très grande `n` si la trie est clairsemée.
*Cons:* Mémoire et complexité supplémentaires, overkill pour "s ≤ 1000".

2. **KMP / Rabin‐Karp** – Construire un jumeleur pour chaque chaîne binaire.
*Pros:* Bon pour les grands motifs.
*Cons:* La recomposition pour chaque `i` est coûteuse; pas nécessaire ici.

3. ** Programmation dynamique** – Pas vraiment applicable parce que nous avons juste besoin de présence, pas de nombre minimal.

L'approche de hachage est le bon endroit : simple, rapide et facile à raisonner.

---

Stratégie d'essai

**Test**
C'est pas vrai.
' s = " 111111 " , n = 1 ' , ' true ' Autres
"s = "0000", n = 1 ""false" (pas de ""1""). Autres
`s = "101010 ", n = 6 ' , `true` (binaire de 1 à 6 tous apparaissent). Autres
"s" = "111000111", n = 7`" vrai". Autres
« s » = « 0110 », n = 4 « faux ». Autres
« s » = « 1001001 », n = 9 « true ». Autres
Autres Très grande `n` (`n = 109`) mais courte chaîne de caractères. Autres

Ajoutez ces cas à vos tests unitaires – ils couvrent le minimum, le type et le bord
les situations.

---

## --Enveloppe & Takeaway

* Le problème vous oblige à penser **logarithmique** en `n` au lieu de linéaire.
* Un seul passage sur `s`, couplé à un `HashSet` de sous-chaînes, donne une solution linéaire avec seulement quelques milliers d'entiers stockés.
* Le code propre en Java, Python ou C++ démontre la maîtrise des opérations bit et des structures de données, deux compétences d'interview très appréciées.

---

## Description rapide de la feuille de thé pour les intervieweurs

- **Pourquoi `log2(n)`? **
Tout nombre > `n` ne peut pas être nécessaire, donc nous ignorons les sous-chaînes plus longues.

- Pourquoi sauter en tête des zéros ? * *
Les numéros binaires ne commencent jamais par `0` (sauf si le nombre lui-même est zéro).

- **Pourquoi sortir tôt avec `n > vu.size()`? * *
Garanties que même si chaque nombre était présent, vous ne pourriez toujours pas les couvrir tous.

- **Comment convertissez-vous une sous-chaîne à une entrée efficacement? * *
Utiliser le déplacement de bits (`val = (val << 1)) bit`) au lieu de `Integer.parse Int'.

---

Résumé du SEO

> **Mots-clés**: *Chaîne binaire, recherche sous-chaîne, manipulation de bits, jeu de hachage, LeetCode 1016, algorithme de chaîne, question d'entretien, solution Java, solution Python, solution C++, analyse de complexité temporelle, cas de bord, conception algorithmique, entretien de codage*

Cet article couvre tout ce dont vous avez besoin pour débarquer la chaîne Binary avec des sous-chaînes Représenter avec confiance 1 à N. Le problème d'entrevue est multiple, le code propre et une plongée profonde dans la logique qui compte pour l'embauche des gestionnaires. Bon codage 