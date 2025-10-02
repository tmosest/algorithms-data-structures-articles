---
titre: LeetCode 2484. Compte Palindromique Subséquences
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 2484 – Compte Palindromic Sous-séquences (longueur 5)

> **Problème**
> Étant donné qu'une chaîne `s` de chiffres (0-9) de longueur jusqu'à `104`, compter combien
> sous-séquences de *exactement* 5 caractères forment un palindrome.
> Retournez le compte modulo `109 + 7`.

---

- Oui. 1. Pourquoi ce problème est une grande question d'entrevue

* **Longueur fixe** – L'étiquette "Hard" est un peu erronée; le fait que
nous n'avons besoin que de subséquences de longueur 5 tours une explosion combinatoire
dans un problème traitable.
* ** Nécessite une bonne compréhension des tableaux préfixes / suffixes** – La plupart
les candidats ne pensent qu'à une force brute ou à une programmation dynamique
approche qui ignore la longueur fixe.
* **Élégant tour de mathématiques** – La solution utilise un préfixe-suffixe soigné qui
Beaucoup de personnes interrogées manquent.

> Si vous pouvez expliquer cette solution de manière claire, vous impressionnerez n'importe quel embauche
> gestionnaire qui se soucie des algorithmes, de la manipulation des chaînes et des mathématiques
> penser.

---

- Oui. 2. Intuition et dérivation

Un palindrome à 5 caractères a la forme

«» "
a b c d e
«» "

avec `a == e` et `b == d`.
Les indices doivent satisfaire à «a < b < c < d < e».
Ainsi, nous pouvons considérer la subséquence comme

1. Choisissez deux indices **outer** `a` et `e` qui détiennent le même chiffre.
2. Choisissez deux **inner** indices `b` et `d` qui détiennent le même chiffre.
3. Choisissez tout `c` qui se trouve entre `b` et `d`.

Le nombre de choix pour `c` est simplement `d - b - 1`.

Si nous itérer sur toutes les paires possibles `b < d` (la paire intérieure) nous seulement
besoin de savoir:

* Combien d'indices extérieurs avec le chiffre `x` existent à gauche de `b`? → `L[x]`.
* Combien d'indices extérieurs avec le chiffre `x` existent à droite de `d`? → `R[x]`.

Puis la contribution de cette paire `(b,d)` est

«» "
(d - b - 1) * φx L[x] * R[x]
«» "

Le défi est de calculer cette somme pour **chaque paire** `(b,d)`
sans double comptage.

- Oui. 3. Compte de préfixe / suffixe

Pour chaque chiffre `d` (0‐9), nous précalculons :

«» "
pref[d][i] – nombre de d=s dans s[0 ... i]
suff[d][i] – nombre de d=s dans s[i ... n-1]
«» "

Les deux tableaux peuvent être construits en temps O(10·n).

- Oui. 4. Agrégation par rapport aux paires intérieures

Que `y` soit le chiffre de la paire intérieure (`b` et `d` aient le chiffre `y`).
Recueillir toutes les positions où `s[pos] == y` dans un tableau `pos[0 ... k-1]`.

Pour un chiffre extérieur fixe `x` nous devons calculer

«» "
* suff[x] [pos[j]+1] * (pos[j] - pos[i] - 1)
«» "

Cela ressemble à une double boucle, mais nous pouvons l'effondrer à **O(k)** en utilisant
Montants courants:

«» "
sumA = <current} pref[x][pos[i]-1]
sumAPos = γ_{i<current} pref[x][pos[i]-1] * pos[i]
«» "

Pour le "j" actuel:

«» "
contrib = (pos[j] * sumA - sumAPos - sumA) * suff[x][pos[j]+1]
«» "

Ajouter `contrib` à la réponse globale, puis mettre à jour `sumA` et `sumAPos`
avec le courant `i = j`.

Faire cela pour chaque chiffre extérieur `x` (0-9) et chaque chiffre intérieur `y "
(0-9) donne le nombre final en **O(10·10·n)** = "O(n)" temps.

Toutes les opérations sont effectuées modulo `MOD = 1_000_000_007`.

---

- Oui. 5. Preuve d'exactitude

Nous prouvons que l'algorithme renvoie le nombre exact de palindromiques
subséquences de la longueur 5.

---

Lemma 1
Pour tout indice `p` et le chiffre `d`, `pref[d][p-1]` (respectivement `suff[d][p+1]`)
égal au nombre d'indices extérieurs avec le chiffre `d` strictement à gauche
(respectivement au droit) de "p".

**Prof.**
«préf[d][p-1]» compte toutes les occurrences de `d` dans le préfixe se terminant juste
avant `p`, c'est-à-dire exactement le set `{ i=0 ≤ i < p, s[i] = d }`.
De même, "suff[d][p+1]" compte toutes les occurrences dans le suffixe commençant
juste après "p".



Lemma 2
Pour toute paire intérieure `b < d` (les deux chiffres étant égaux à `y`) et tout chiffre extérieur
"x", le terme

«» "
[x] [b-1] * suff[x] [d+1]
«» "

égale le nombre de façons de choisir une paire externe `(a,e)` avec le chiffre
`x` qui satisfait `a < b` et `d < e`.

**Prof.**
Par Lemma 1, "pref[x][b-1]` compte tous les "x" à gauche de "b"; chaque
un tel événement peut être utilisé comme "a".
`suff[x][d+1]` compte tous les `x`=" droit de `d`; chacun peut être utilisé comme `e`.
Les choix sont indépendants, donc le produit compte tous les
paires.



Lemma 3
Pour un chiffre intérieur fixe `y` et un chiffre extérieur `x`, l'algorithme calcule

«» "
* suff[x] [pos[j]+1] * (pos[j]-pos[i]-1)
«» "

Exactement.

**Prof.**
Considérez l'étape itérative pour l'index "j".

* `sumA` contient `-{i<j} pref[x][pos[i]-1]`.
* `sumAPos` détient `ш_{i<j} pref[x][pos[i]-1] * pos[i]`.

Ainsi

«» "
pos[j] * sumA = φ_{i<j} pref[x][pos[i]-1] * pos[j]
sumAPos = γ_{i<j} pref[x][pos[i]-1] * pos[i]
«» "

La soustraction donne

«» "
pos[j] * sumA - sumAPos = <j} pref[x] [pos[i]-1] * (pos[j] - pos[i])
«» "

Soustraire un rendement supplémentaire "sumA"

«» "
* (pos[j] - pos[i] - 1)
«» "

Multiplier par `suff[x][pos[j]+1]` donne exactement le terme que
la formule de contribution utilise. Par conséquent, chaque itération ajoute la bonne
montant pour toutes les paires `(i,j)` avec `i < j`. Résumé sur tous les x "
(0-9) et tous `y` (0-9), chaque palindrome admissible est compté une fois
Et seulement une fois.



- Oui. Théorème
`countPalindromicSubseq(s)` retourné par l'algorithme égale le nombre de
Sous-séquences palindromiques de 5 caractères de `s`, modulo `MOD`.

**Prof.**
De Lemma 3 nous savons que pour chaque choix de chiffre intérieur `y` et extérieur
le chiffre `x` la somme de l'algorithme sur toutes les positions extérieures admissibles
'i<j` le produit

«» "
[j+1] * (pos[j]-pos[i]-1)
«» "

Par la dérivation de la section 2, c'est précisément la contribution de tous
subséquences palindromiques dont les chiffres intérieurs sont égaux à « y » et les chiffres extérieurs
égale "x".
Le résumé de toutes les combinaisons 10×10 représente donc chaque
subséquence palindromique exactement une fois, prouvant le théorème. *



---

- Oui. 6. Analyse de la complexité

Étape Coût
- Oui.
"O(10·n)" Autres
Grande agrégation Autres
**Total******"O(n)" temps, "O(10·n)" mémoire**

Avec `n ≤ 104`, l'algorithme fonctionne confortablement sous 1 ms
langues officielles.

---

- Oui. 6. Mise en œuvre des références

Voici les implémentations propres et idiomatiques dans **Java 17**, **Python 3.11**,
et **C++17**.
Tous les trois utilisent la même logique, de sorte que vous pouvez déposer un dans un harnais de test ou
Portez-le dans une autre langue sans effort.

> **Conseil** – Lors de la soumission à un juge en ligne, assurez-vous que vous définissez
> `MOD = 1_000_000_007L` (Java) ou `MOD = 1000000007` (Python, C++).

---

#### 5.1 Java 17

"Java
importation java.io.*;
Importation de java.util.*;

classe publique {
finale statique privée longue MOD = 1_000_000_007L;

compte public statique longPalindromicSubseq(String s) {
int n = s.longueur();
int[][] pref = nouvelle int[10][n];
int[]] suff = nouvelle int[10]n];

// Préfixe
pour (int d = 0; d < 10; d++) {
cnt = 0;
pour (int i = 0; i < n; i++) {
si (s.charAt(i) - '0' == d) cnt++;
pref[d][i] = cnt;
}
}

// suffixe
pour (int d = 0; d < 10; d++) {
cnt = 0;
pour (int i = n - 1; i >= 0; i--) {
si (s.charAt(i) - '0' == d) cnt++;
suff[d][i] = cnt;
}
}

long ans = 0;

// Pour chaque chiffre intérieur y
pour (int y = 0; y < 10; y++) {
// Recueillir toutes les positions du chiffre y
Liste <Integer> posList = nouvelle liste de distribution<>();
pour (int i = 0; i < n; i++) {
si (s.charAt(i) - '0' == y) posList.add(i);
}
int k = posList.size();
si (k <= 1) continuer; // besoin d ' au moins deux indices intérieurs

// Pour chaque chiffre extérieur x
pour (int x = 0; x < 10; x++) {
longue sommeA = 0;
long sumAPos = 0;
pour (int idx = 0; idx < k; idx++) {
int pos = posList.get(idx);
long A = pos == 0 ? 0 : pref[x][pos - 1];
long B = pos == n - 1 ? 0 : suff[x][pos + 1];

long terme = (pos * suma % MOD - sumapos - suma) % MOD + MOD) % MOD;
long contrib = terme * B % MOD;
ans = (ans + contrib) % MOD;

sumA = (sumA + A) % MOD;
sumAPos = (sumAPos + A * pos) % MOD;
}
}
}
le retour des an;
}

// -------- Conducteur pour le test...
public statique vide main(String[] args) lance IOException {
BufferedReader br = nouveau BufferedReader(nouveau InputStreamReader(System.in));
Chaîne s = br.readLine().trim();
Système.out.println(countPalindromicSubseq(s));
}
}
«» "

---

#### 5.2 Python 3.11

'`python
importations

MOD = 1 000 000 007

def count_palindromic_subseq(s: str) -> Int:
n = len(s)

# Préfixe et suffixe
pref = [[0] * n pour _ dans l'intervalle(10)]
suff = [[0] * n pour _ dans l'intervalle(10)]

Construire préf
pour d dans la plage(10):
cnt = 0
pour i, ch dans le(s) énuméré(s):
Si ord(ch) - 48 == d:
cnt += 1
pref[d][i] = cnt

# Construire des suffisances
pour d dans la plage(10):
cnt = 0
pour i dans la fourchette(n - 1, -1, -1):
si ord(s[i]) - 48 == d:
cnt += 1
[d]i] = cnt

ans = 0

# Principale agrégation
pour y dans la plage(10):
positions = [i pour i, ch dans le ou les énuméré(s) si ord(ch) - 48 == y]
k = len(positions)
si k <= 1:
poursuivre

pour x dans la plage(10):
sumA = 0
sumAPos = 0
pour les positions:
A = pref[x][pos - 1] si pos > 0 autre 0
B = suff[x][pos + 1] si pos + 1 < n autre 0

# (pos * sumA - sumAPos - sumA) mod MOD
terme = (pos * sumA - sumAPos - sumA) % MOD
contrib = terme * B % MOD
ans = (ans + contrib) % MOD

sumA = (sumA + A) % MOD
sumAPos = (sumAPos + A * pos) % MOD

retour et

si __nom__ == "__main__" :
s = sys.stdin.readline().strip()
print(count_palindromic_subseq(s))
«» "

---

Numéro 5.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;
longue MOD = 1'000'000'007LL;

long comptePalindromicSubseq(chaîne de caractères Const& s) {
int n = s.size();
vecteur<array<int, 10001>> pref(10), suffixe(10); // 10 x n

// Préfixe
pour (int d = 0; d < 10; ++d) {
cnt = 0;
pour (int i = 0; i < n; ++i) {
si (s[i] - '0' == d) ++cnt;
pref[d][i] = cnt;
}
}

// suffixe
pour (int d = 0; d < 10; ++d) {
cnt = 0;
pour (int i = n - 1; i >= 0; --i) {
si (s[i] - '0' == d) ++cnt;
suff[d][i] = cnt;
}
}

long an = 0;
vecteur <int> pos;

pour (int y = 0; y < 10; ++y) {
Pos.clear();
pour (int i = 0; i < n; ++i)
si (s[i] - '0' == y) pos.push_back(i);
int k = pos.size();
si (k <= 1) continuer;

pour (int x = 0; x < 10; ++x) {
long sumA = 0, sumAPos = 0;
pour (int p : pos) {
long A = (p == 0) ? 0 : pref[x][p - 1];
long B = (p + 1 == n) ? 0 : suff[x][p + 1];

long terme = (p * suma % MOD - sumapos - suma) % MOD + MOD) % MOD;
longue longue contrib = terme * B % MOD;
ans = (ans + contrib) % MOD;

sumA = (sumA + A) % MOD;
sumAPos = (sumAPos + A * p) % MOD;
}
}
}
le retour des an;
}

Int main() {
ios::sync_with_stdio(faux);
cin.tie (nullptr);
string s; getline(cin, s);
Cout << cutPalindromicSubseq(s) << '\n';
}
«» "

---

- Oui. 7. Foire aux questions

Question Réponse
C'est pas vrai.
Autres Pour `n=104`, la force brute est `O(n^5)` → impossible. Autres
Autres **Que faire si la chaîne est vide? Autres
Autres **L'algorithme peut-il gérer une mémoire énorme?**=Il utilise seulement `O(10·n)` ints → < 400 KB. Autres
Autres **Pourquoi ignorons-nous `k ≤ 1`?**= Une paire intérieure nécessite au moins deux indices. Autres

---

- Oui. 8. Qu'est-ce qui rend ce problème difficile?

1. **Structure à quatre niveaux** – Vous devez gérer simultanément deux
dimensions (indices intérieurs et indices extérieurs) tout en respectant les contraintes d'ordre.
2. **Dénombrement dynamique** – Le dénombrement naïf serait exponentiel.
3. **Modulo arithmétique** – Prévenir le débordement tout en préservant la justesse.
4. **Cas d'Edge** – Chaînes vides, tous les chiffres identiques, très courtes
Des cordes.

Un algorithme bien structuré qui tire parti des sommes préfixées est le seul moyen
pour le résoudre efficacement.

---

- Oui. 9. Conclusion

Nous avons construit une solution optimale pour compter les 5 caractères palindromiques
subséquences:

* Une réduction combinatoire soigneuse qui conduit à un algorithme linéaire.
* Une preuve rigoureuse que la méthode est correcte.
* Trois implémentations de référence que vous pouvez copier, tester et adapter.

> **Note finale** – Le même motif (préfixe–suffix compte + agrégation)
> peut être appliqué à de nombreux autres problèmes de comptage de sous-chaînes (p. ex.
> occurrences de patrons de subséquence spécifiques, ou palindromes à 3 caractères
> avec différentes contraintes). La maîtrise de cette technique sera payante
> dans les concours futurs. Bon codage ! C'est ce qu'il a dit.
---



**Codage heureux!**