---
titre: LeetCode 2514. Compte Anagrammes - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
2514. Count Anagrams – Solution complète (Java, Python, C++)

Ci-dessous vous trouverez **trois implémentations prêtes à la production** qui résolvent le problème de LeetCode -Count Anagrams en **O(N + K)** temps (où *N* = longueur de chaîne et *K* = longueur maximale de mot).
Chaque mise en œuvre comprend :

* Facteurs précalculés et facteurs inverses modulo **1 000 000 007* *
* Exponentiation modulaire rapide (Fermats petit théorème)
* Commentaires clairs et entrée de style principal pour les tests rapides

---

C'est pas vrai. Java

"Java
importation java.io.*;
Importation de java.util.*;

solution de classe publique {

finale statique privée longue MOD = 1_000_000_007L;

- Oui. Pré-computation des facteurs ---------- */
fait statique privé long[];
statique privé long[] invFact;

précalcul du vide statique privé(int maxLen) {
fait = nouveau long[maxLen + 1];
invFact = nouveau long[maxLen + 1];
fait[0] = 1;
pour (int i = 1; i <= maxLen; i++) {
fact[i] = (fact[i - 1] * i) % MOD;
}
invFact[maxLen] = modInverse(fact[maxLen], MOD);
pour (int i = maxLen; i > 0; i--) {
invFact[i - 1] = (invFact[i] * i) % MOD;
}
}

- Oui. Inverse modulaire (Fermat) --------- */
privé statique long mod Inverse(long a, long mod) {
retourner modPow(a, mod - 2, mod);
}

modPow (long base, long exp, long mod) {
longue rés = 1;
base %= mod;
pendant la période (exp > 0) {
si ((exp & 1)] 1) res = (rés * base) % mod;
base = (base * base) % mod;
Exp >>= 1;
}
retour rés;
}

- Oui. Compter les anagrammes d'un seul mot
privé statique long mot Anagrammes(String w) {
int[] freq = nouveau int[26];
pour (char c : w.toCharArray()) freq[c - 'a']++;

numérateur long = fait[w.longueur()];
long nom = 1;
pour (int f : freq) si (f > 1) denom = (dénom * fait[f]) % MOD;

retour (numérateur * modInverse(denom, MOD)) % MOD;
}

- Oui. Solution principale
compte publicAnagrammes(String s) {
// Trouver le mot le plus long pour savoir combien de factorials nous avons besoin
Int maxLen = 0;
pour (String w : s.split("") maxLen = Math.max(maxLen, w.longueur());

le précalcul (maxLen);

long ans = 1;
pour [Pièce w : s.split("") {
as = (ans * wordAnagrams(w)) % MOD;
}
retour (int) ans;
}

- Oui. Pilote simple pour les essais locaux
public statique vide main(String[] args) lance IOException {
BufferedReader br = nouveau BufferedReader(nouveau InputStreamReader(System.in));
Ligne de chaîne = br.readLine(); // par exemple "trop chaud"
System.out.println(nouvelle solution().countAnagrams(line));
}
}
«» "

---

# # # # # #

'`python
#!/usr/bin/env python3
importations
Importations provenant des collections Compteur

MOD = 1 000 000 007

C'est... Facteurs précalculés ---------
def precompute(max_len: int):
fait = [1] * (max_len + 1)
pour i dans la plage (1, max_len + 1):
fait[i] = fait[i - 1] * i % MOD
inv_fact = [1] * (max_len + 1)
inv_fact[max_len] = pow(fact[max_len], MOD - 2, MOD) # Fermat
pour i dans l'intervalle (max_len, 0, -1):
inv_fact[i - 1] = inv_fact[i] * i % MOD
fait de retour, inv_fact

C'est... Compter les anagrammes d'un seul mot...
def word_anagrams(word: str, fact, inv_fact):
freq = Contre(mot)
num = fait[len(mot)]
denom = 1
pour f dans les valeurs freq.():
denom = denom * fait[f] % MOD
retour num * pow(denom, MOD - 2, MOD) % MOD

C'est... Solution principale
def count_anagrammes(s: str) -> Int:
mots = s.split()
max_len = max(len(w) pour w en mots) si autres mots 0
, inv_fact = précalcul(max_len)

ans = 1
pour w en mots:
ans = ans * word_anagrams(w, fact, inv_fact) % MOD
retour et

Le chauffeur du CLI...
si __nom__ == "__main__" :
s = sys.stdin.readline().strip()
print(count_anagrammes)
«» "

---

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Constexpr statique long MOD = 1'000'000'007LL;
vecteur <long> fait, invFact;

- Oui. Exponentiation modulaire --------- */
long long modPow(long long base, long exp) {
longue rés = 1;
base %= MOD;
pendant (exp) {
si (exp & 1) res = res * base % MOD;
base = base * base % MOD;
Exp >>= 1;
}
retour rés;
}

- Oui. Facteurs précalculés ---------- */
vide précalculé(int maxLen) {
fact.resize(maxLen + 1);
invFact.resize(maxLen + 1);
fait[0] = 1;
pour (int i = 1; i <= maxLen; ++i)
fait[i] = fait[i - 1] * i % MOD;
invFact[maxLen] = modPow(fact[maxLen], MOD - 2);
pour (int i = maxLen; i > 0; --i)
invFact[i - 1] = invFact[i] * i % MOD;
}

- Oui. Compter les anagrammes pour un mot ---------- */
long motAnagrams(chaîne de caractères &w) {
tableau <int, 26> freq = {0};
pour (char c : w) freq[c - 'a']++;

numérateur long = fait[w.size()];
long nom = 1;
pour (int f : freq) si (f > 1)
denom = denom * fait[f] % MOD;

numérateur de retour * modPow(denom, MOD - 2) % MOD;
}

- Oui. Solution principale
int countAnagrams(chaîne s) {
vecteur <string> les mots;
sss de chaîne de caractères;
chaîne w;
Int maxLen = 0;
pendant que (ss >> w) {
words.push_back(w);
maxLen = maxLen, (int)w.size();
}
le précalcul (maxLen);

long an = 1;
pour (auto & mot : mots)
ans = ans * wordAnagrams(word) % MOD;
retour (int)ans;
}
};

/* - Oui. Pilote simple pour un test rapide
Int main() {
ios::sync_with_stdio(faux);
cin.tie (nullptr);
ligne de chaîne;
getline(cin, ligne); // par exemple "trop chaud"
Solution sol;
Cout << sol.countAnagrams(line) << '\n';
retour 0;
}
«» "

---

Article du blog sur le LeetCode : le bon, le mauvais, le mauvais

> **Titre:** *=Count Anagrammes – 2514 LeetCode – La solution mathématique, modulaire et arithmétique qui fera sourire vos intervieweurs*
> **Description détaillée:** *Découvrez comment résoudre le problème dur de LeetCode ‘Count Anagrams' en utilisant les combinaisons, les inverses modulaires et les factoriaux précalculés. Code en Java, Python et C++. Maître les parties bonnes, mauvaises et laides.

Introduction

Le problème d'Anagrammes de Count (LeetCode 2514) vous demande de calculer le nombre d'anagrammes distincts **sentence-level** d'une chaîne donnée de mots minuscules séparés par des espaces uniques. À première vue, il se sent comme un cauchemar combinatoire – mais avec le bon calcul vous pouvez le résoudre en temps linéaire.

> **Pourquoi c'est important:**
> Les intervieweurs aiment les problèmes qui combinent la programmation dynamique*-style pensée avec l'arithmétique modulaire*. La maîtrise de ce problème démontre que vous pouvez :
> * Reconnaître les sous-problèmes indépendants (chaque mot)
> * Appliquer des coefficients multinomiaux
> * Manipulation de grands nombres modulo 1 000 000 007
> * Écrire un code propre et efficace en plusieurs langues

Rétablissement du problème

> **Input**: `s` – une phrase contenant un ou plusieurs mots, tous minuscules, espaces uniques entre les mots.
> **Output**: `count` – le nombre d'anagrammes distincts de la phrase entière modulo 1 000 000 007.

C'est vrai. Le Bon – Un Tout droit Mathématiques

Étape Qu'est-ce que ça veut dire ?
- C'est quoi ?
**1. Les mots sont indépendants. Répartir la phrase et multiplier les résultats par mot. Autres
Pour un mot de longueur `L` avec les fréquences de caractères `f1, f2, ..., f26`, le nombre de permutations uniques est:

\[
\frac{L!}{f_1!\,f_2!\,\dots F_{26} !
Calcul des facteurs `L!` et diviser par chaque `f_i!`. Autres
**3. Modulo arithmétique** Utiliser `MOD = 1 000 000 007`. Autres
Vous ne pouvez pas diviser directement. Autres

Aperçu de l'algorithme

1. **Précalculer les facteurs** jusqu'à la longueur du mot le plus long.
2. Pour chaque mot :
* Compter les fréquences des lettres (`cnt[a] ... cnt[z]`).
* `num = fait[word_len] "
* `den = Π fait[cnt[c]]` pour tous `c` avec `cnt[c] > 1'
* `word_ans = num * den−1 mod MOD`
3. **Multiply** toutes les valeurs `word_ans` modulo MOD pour obtenir la réponse finale.

La complexité du temps est **O(N + K)** – linéaire dans la longueur d'entrée plus un petit facteur `O(K)` pour le tableau factoriel le plus long. L'utilisation de la mémoire est aussi linéaire dans la longueur maximale du mot.

C'est pas vrai. Le bon – ce qui rend cette solution belle

Aspect Pourquoi c'est bon
C'est quoi, ça ?
La formule multinomiale est l'expression la plus *propre* possible pour la réponse. Pas de table DP ou de récursion nécessaire. Autres
**La pré-computation linéaire est générée une fois par cas d'essai. Leur réutilisation garantit une recherche O(1) pour toute longueur de mot. Autres
**Language-agnostic**Le même algorithme peut être écrit en Java, Python ou C++ avec des changements minimes. Autres
**Sécurité modulaire**= Toutes les opérations sont effectuées modulo `1 000 000 007`, garantissant qu'il n'y a pas de débordement dans les entiers 64 bits. Autres
Chaque fonction a une seule responsabilité (`precompute`, `wordAnagrams`, `modPow`). Cette lisibilité est une victoire dans les entrevues. Autres

C'est vrai. Le mauvais – où les pièges se produisent

Numéro Explication
- Oui.
**Grande matrice factorielle**** Si un mot est très long (par exemple, 105), l'attribution de `fait` et `invFact` de cette taille peut frapper les limites de mémoire de certains juges. Calculez seulement jusqu'à la longueur maximale *réelle* du mot. Autres
**Splited splits**=L'utilisation de `s.split(""")` deux fois peut être O(N2) dans les langues les plus mauvaises qui copient les chaînes. Répartir une fois, stocker les mots dans un vecteur/array. Autres
**Calls de pow répétés**. Appeler `pow` dans la boucle pour chaque mot peut sembler coûteux. Le calcul pré-invFact est une simple multiplication (invFact[denom]). Autres
**La division par zéro**= Si vous oubliez de gérer une fréquence de 0 ou 1, vous pouvez essayer par inadvertance de calculer `0!−1`.= seulement multiplier par `fact[f]` lorsque `f > 1`. Autres

- Oui. Les horribles cas de bord qui peuvent casser Toi

Autres Ugly situation: Pourquoi il casse: Que regarder?
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
Autres **Très long mot unique** , les facteurs croissent rapidement; le pré-comptage jusqu'à 106 peut dépasser les limites par défaut de la pile ou de la mémoire. Utilisez `long' (64-bit) et un vecteur *statique*; évitez les récursions. Autres
**Modulaire inverse de 0** Dans ce problème, le dénominateur est toujours un produit de factorials de nombres non-zéro, de sorte qu'il ne peut jamais être 0 mod MOD (parce que tous les factorials jusqu'à MOD-1 sont non-zéro). Autres
**Un espace blanc inattendu**Le problème garantit des espaces uniques, mais un intervieweur pourrait tester `"trop chaud"` pour voir si vous êtes défensif. Autres Trimez la chaîne et divisez-la sur les caractères regex `\s+` ou analysez manuellement. Autres
**Signature vide**= Certaines solutions supposent au moins un mot; une chaîne vide doit renvoyer 0 ou 1?= Définir le contrat : retourner `0` si la phrase n'a pas de mots. Autres

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Séparer la phrase **O(N)**
**O(K)** (deux tableaux)
Autres Comptabiliser les anagrammes par mot **O(K)** chaque → total **O(N)**
Total****************

Parce que *K* est au maximum la longueur du mot le plus long (= 105 dans les tests LeetCode), l'utilisation de la mémoire reste bien inférieure à 20 Mo dans les trois langues.

Résumé – Ce que vous allez prendre à la maison

Autres Ce que j'ai appris Ce que je vais montrer à l'interview
RÉSULTATS
**Coefficients multinomiaux**= Chaque mot anagramme n'est qu'une formule combinatoire. Autres
**Modules inverses**Le petit théorème de Fermat donne une façon rapide et fiable de diviser sous modulo. Autres
**Tricks de pré-computation**= Un passe pour construire des factoriels, un passe pour construire des factoriels inverses. Autres
**Diagnostics spécifiques à la langue** Autres

> ** Conseil professionnel :**
> Testez toujours votre code sur les cas bord suivants avant l'entrevue :
> * `"a"` – caractère unique
> * `"abcdefghijklmnopqrstuvwxyz"` – mot le plus long possible (26 lettres)
> * `"aaaaaa"` – lettres répétées
> * `" "` (entrée vide) – garde contre les fentes

---

À emporter

Le problème des « Count Anagrams » est une vitrine *combinatoire‐plus‐modulaire‐arithmétique*. Avec les trois solutions prêtes à l'emploi ci-dessus, vous êtes désormais équipé pour :

* **Solve** le problème en temps O(N + K)
* ** Expliquer** les maths derrière chaque étape d'une entrevue
* **Switch** entre Java, Python et C++ avec confiance

Bonne chance – et rappelez-vous: *code clair + maths propres = succès d'entrevue! *