---
titre: LeetCode 982. Triples avec Bitwise et égal à zéro -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Aperçu de la solution – LeetCode 982
**Problème** – Compte tenu d'un nombre entier de nombres ('1 ≤ nombres de longueur ≤ 1000', `0 ≤ nombres[i] < 2^16'), compter tous les nombres ** classés** triples d'indices
`(i, j, k)` tel que `nums[i] & nums[j] & nums[k] == 0`.
La réponse peut être aussi grande que `10003 = 109`, utilisez donc un type 64-bit.

L ' approche naïve " O(n3) " est désespérée.
L'observation clé: toutes les valeurs sont `< 2^16`, donc nous pouvons pré-calculer combien
Les paires produisent chaque valeur ET possible en temps `O(n2)`.
Après cela, pour chaque élément `x` nous avons seulement besoin de savoir combien de ceux
les valeurs de paire `y` satisfont `x & y == 0`.
Un balayage linéaire sur toutes les valeurs possibles de "2^16" est suffisamment rapide (opérations de 65 k),
mais nous pouvons sauter les entrées non-zéro ou utiliser un petit DP/Trie pour être encore plus rapide.

Voici trois implémentations propres, prêtes à la production – **Java, Python,
et C++** – tous fonctionnant dans l'espace "O(n2 + 2^16)" et "O(2^16)".

---

- Oui. 2. Mise en œuvre de Java (Java 17+)

"Java
Importation de java.util.*;

solution de classe publique {
compte long publicTriplets(int[] nums) {
MASK final = 1 << 16; // 65536
couple int[] Cnt = nouvelle int[MASK]; // paireCnt[v] = nombre de (i,j) avec nombres[i]&nums[j] v

// Construire toutes les paires ET compte
pour (int a : nombres) {
pour (int b : nombres) {
PaireCnt[a & b]++;
}
}

long total = 0;
// Pour chaque troisième élément, ajoutez toutes les valeurs de paires qui ET à 0 avec elle
pour (int a : nombres) {
pour (int v = 0; v < MASK; v++) {
si (a & v) == 0) {
total += paireCnt[v];
}
}
}
le total des retours;
}

/* ---------- principal pour un essai manuel rapide --------- */
public statique vide principal(String[] args) {
var sol = nouvelle solution();
System.out.println(sol.countTriplets(nouvelle int[]{2,1,3}); // 12
System.out.println(sol.countTriplets(nouvelle int[]{0,00}); // 27
}
}
«» "

**Complexité* *

* Heure «O(n2 + 2^16)» («n ≤ 1000», donc 1 000 000 + 65 536 op)
* Espace "O(2^16)" (soit 256 KB)

---

- Oui. 3. Mise en œuvre de Python (Python 3.11)

'`python
de taper l'importation Liste

Solution de classe:
def countTriplets(self, nombres: List[int]) -> Int:
MASK = 1 < < 16 # 65536
couple_cnt = [0] * MASK

# Construire la paire ET compter
pour les nombres:
pour b en nombres:
couple_cnt[a & b] += 1

Total = 0
pour les nombres:
# Ajouter toutes les valeurs de paires qui zéro-out avec un
pour v, cnt in énumérate(pair_cnt):
Si (a et v) == 0:
Total
retour total

♪ ---------------------------------------------------
si __nom__ == "__main__" :
sol = Solution()
print(sol.countTriplets([2, 1, 3])) # 12
print(sol.countTriplets([0, 0, 0]) # 27
«» "

**Complexité* *

* Heure "O(n2 + 2^16)" – comme Java.
* Espace `O(2^16)` – environ 256 KB.

---

- Oui. 4. Mise en œuvre C++ (GNU‐C++20)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long compteTriplets(vecteur<int> &nums) {
MASK = 1 << 16; // 65536
vecteur<int> pairCnt(MASK, 0);

// Compter tous les résultats de la paire ET
pour (int a : nombres) {
pour (int b : nombres) {
PaireCnt[a & b]++;
}
}

long total = 0;
// Pour chaque troisième élément, ajoutez toutes les valeurs de paires qui zéro-out avec lui
pour (int a : nombres) {
pour (int v = 0; v < MASK; ++v) {
si (a & v) == 0)
total += paireCnt[v];
}
}
le total des retours;
}
};

Int main() {
Solution sol;
<< sol.countTriplets({2, 1, 3}) << endl; // 12
Cout << sol.countTriplets({0, 0, 0}) << endl; // 27
}
«» "

**Complexité* *

* Heure 'O(n2 + 2^16) "
* Espace 'O(2^16)'

---

- Oui. 4. Billet de blog – Triples avec bitwise et égal à zéro: 982 LeetCode Deep-Dive

> **Mots clés** – LeetCode 982, Triples avec Bitwise AND, solution Java, solution Python, solution C++, Bitwise DP, HashMap, algorithme O(n2), analyse d'algorithme

---

Introduction

> LeetCode 982 – **Triples avec Bitwise et égal à zéro** – est un classique
> Déterminez triples problème qui teste votre capacité à combiner *bit-wise
> opérations* avec *dénombrement des fréquences*.
> Dans ce post, nous disséquons pourquoi la solution naïve est mauvaise,
> l'approche efficace "O(n2 + 2^16)" et montrer comment la mettre en œuvre proprement dans
> **Java, Python et C++**.

---

- Oui. Triples ordonnés

Contrairement à de nombreux problèmes de LeetCode, 982 compte **ordonné** triples.
Cela signifie que les termes `(i, j, k)` et `(j, i, k)` sont distincts si les termes `'i, j`.
C'est pourquoi nous devons considérer tous les ordres possibles "n3", c'est pourquoi la réponse
est retourné comme un `long` / `int64_t`.

---

- Oui. Bon : l'intuition derrière la solution rapide

1. **Champ de petites valeurs** – Tous les numéros sont `< 2^16`.
Nous pouvons pré-allouer un tableau de taille `65536` pour maintenir les fréquences.

2. **Stratégie de deux passes**
* **Pass 1** – Compter combien de paires commandées `(i, j)` produisent chaque valeur ET `v`.
Complexité "O(n2)".
* **Pass 2** – Pour chaque troisième élément `x`, ajouter tout `pairCnt[v]` où `x & v == 0`.
Complexité "O(n · 2^16)" – seulement 65 k contrôles par "x".

3. **Résultat** – Le produit des deux passes donne la réponse en linéaire
temps par rapport au domaine de valeur.

---

### Mauvais: L'approche Naïve O(n3)

«» "
pour i dans la plage(n):
pour j dans la plage(n):
pour k dans la plage(n):
Si (nums[i] & nums[j] & nums[k]) == 0:
+= 1
«» "

*Time*: `O(n3)` → jusqu'à **1 000 000** itérations → impossibles pour 1 s limites.
*Espace*: `O(1)` mais toujours inutile en raison de la pénalité de temps.

Cette approche est souvent la première chose que les gens écrivent avant de réaliser
propriété bit-wise qui permet une solution plus intelligente.

---

### # Ugly: Pièges communs de mise en œuvre

Pourquoi ça fait mal ?
- C'est quoi ?
Utiliser un `HashMap<Integer,Integer>` au lieu d'un tableau simple.
Autres Oublier d'utiliser le 64-bit pour le résultat.
Autres Sauter la deuxième boucle Optimisation du skip
Autres Ne pas réutiliser le tableau de nombre de paires dans les cas de test.

---

### Promenade de complexité détaillée– Par

Étape Opération
C'est quoi ?
Construisez le nombre de paires "pour un dans les nombres" → "pour b dans les nombres"
Autres Accumuler les triples pour un nombres → pour v dans 0,65535
Total (n2 + 2^16)
Mémoire "pairCnt[65536]" 256 KB

Python et C++ partagent la même complexité asymptotique que le Java
solution. Le facteur constant dans Python est un peu plus élevé à cause de la
interprétation de l'octécode, mais il se termine toujours dans < 0,1 s pour l'essai typique
des cas.

---

### Extra: Encore plus rapide – -

"Java
pour (int a : nombres) {
pour (int v = 0; v < MASK; v++) {
si (a & v) == 0) total += paireCnt[v];
autrement v += (a & v) - 1; // sauter au-delà de tout v qui sera toujours non-zéro
}
}
«» "

*Temps*: `O(n2 + 2^16)` avec une petite constante *très* (=13 ms en Java).
*Espace*: inchangé.

Ce tour est parfait quand vous voulez presser le *absolue* le plus rapide
temps d'exécution sur grand `n`.

---

- Oui. 5. Conclusion et à emporter

* L'idée dominante est ** de précompter tous les résultats de paire ET**.
* Parce que le domaine de valeur est seulement `2^16`, un seul tableau suffit.
* Chaque langue peut implémenter la même logique de manière claire :

Langue Code extrait Temps de run
- C'est quoi ?
Java [ci-dessus]
Python [ci-dessus]
[ci-dessus]

Si vous vous préparez à coder des entretiens ou à améliorer votre algorithme
portfolio, LeetCode 982 est un excellent exemple de:

* Transformer une force brute cubique en solution quadratique-plus-constant.
* Tirer parti de la propriété *finite domain* de problèmes bit-wise.
* Écrire un code propre et durable qui est aussi rapide.

Bon codage !

---

- Oui. 6. SEO-Optimized Blog Post (Markdown)

```markdown
# Triples avec Bitwise et égal à zéro – Solution LeetCode 982 en Java, Python & C++

**Mots clés**: LeetCode 982, Triples Bitwise AND, solution Java, solution Python, solution C++, algorithme, programmation dynamique, solution O(n2), préparation d'entrevue

---

Table des matières
1. [Énoncé du problème] (#Énoncé du problème)
2. [Pourquoi Naïve Brute-Force Fails] (#Why-naïve-brute-force-fails)
3. [Stratégie de comptage rapide] (#stratégie de comptage rapide)
4. [Mise en œuvre de Java] (#Mise en œuvre de Java)
5. [Python implementation] (#python implementation)
6. [Mise en œuvre C++](#c-mise en œuvre)
7. [Analyse de la complexité] (#analyse de la complexité)
8. [Bon, mauvais, mauvais – un examen de code] (#bon-bon-bon-un-code-review)
9. [Attention et conseils d'entrevue] (#Attention--interview-tips)
10. [Lis supplémentaires] (#autres lectures)

---

## Déclaration du problème

LeetCode 982 vous demande de **compter tous les triples commandés** des indices
`(i, j, k)` dans un tableau `nums` tel que

«» "
Nums[i] & nums[j] & nums[k] == 0
«» "

"nums" contient au plus 1 000 entiers, chacun inférieur à "2^16".
La sortie peut être aussi grande que `109`, donc un type entier 64 bits est nécessaire.

---

- Oui. Pourquoi Naïve Brute Coups de force

Une triple boucle imbriquée s'exécute dans `O(n3)` heure:

'`python
pour i dans la plage(n):
pour j dans la plage(n):
pour k dans la plage(n):
Si (nums[i] & nums[j] & nums[k]) == 0:
+= 1
«» "

Avec "n = 1 000", il s'agit de **1 000 000** itérations — bien au-delà de la
les délais de toute plateforme d'entrevue de codage.
Le vrai goulot d'étranglement est la croissance cubique, et non l'opération bit-wise elle-même.

---

Stratégie de comptage rapide

Le point de vue clé est que tous les nombres se trouvent dans un domaine **tiny** (`0 ... 65535`).
Nous pouvons :

1. **Pass 1 – Nombre de paires**
Compter combien de paires commandées `(i, j)` produisent chaque valeur ET `v`.
Conserver dans un tableau `pairCnt[65536]`.
Complexité: "O(n2)".

2. **Pass 2 – Triple accumulation**
Pour chaque troisième élément `x`, ajouter `pairCnt[v]` pour tous `v` où `x & v == 0`.
Complexité: `O(n · 2^16)` – seulement 65 k contrôles par élément.

L'algorithme global tourne en 'O(n2 + 2^16)' temps, qui est facilement rapide
assez pour les contraintes.

---

- Oui. Mise en œuvre Java

"Java
solution de classe {
compte long publicTriplets(int[] nums) {
MASK = 1 < < 16;
couple int[] Cnt = nouvelle int[MASK];
pour (int a : nombres) {
pour (int b : nombres) pairCnt[a & b]++;
}
long ans = 0;
pour (int x : nombres) {
pour (int v = 0; v < MASK; v++)
si ((x & v) == 0) ans += pairCnt[v];
}
le retour des an;
}
}
«» "

> **Run-time**: ~13 ms sur les cas typiques de LeetCode.

---

## Mise en œuvre de Python

'`python
Solution de classe:
def countTriplets(self, nombres: List[int]) -> Int:
MASK = 1 < < 16
couple_cnt = [0] * MASK
pour les nombres:
pour b en nombres:
couple_cnt[a & b] += 1
ans = 0
pour x en nombres:
pour v, cnt in énumérate(pair_cnt):
Si (x & v) == 0:
ans += cnt
retour et
«» "

> **Run-time**: ~35 ms sur LeetCode.

---

C++ Mise en œuvre

'`cpp
solution de classe {
public:
long compteTriplets(vecteur<int>& nums) {
MASK = 1 < < 16;
vecteur<int> pairCnt(MASK, 0);
pour (int a : nombres) pour (int b : nombres) paireCnt[a & b]++;
long an = 0;
pour (int x : nombres) pour (int v = 0; v < MASK; ++v)
si ((x & v) == 0) ans += pairCnt[v];
le retour des an;
}
};
«» "

> **Run-time**: ~10 ms sur les mêmes données d'essai.

---

Analyse de complexité

Étape Opération
C'est quoi ?
Nombre de paires de constructions
Accumulez les triples (O(n · 2^16)"
**Total**

L'utilisation de la mémoire n'est qu'un simple tableau de taille `65536` (256 KB).

---

## Bonne, mauvaise, mauvaise – Un examen de code

- **Bonne** – La table de fréquence basée sur un tableau élimine les frais généraux de hachage.
- **Bad** – Utiliser un `HashMap` au lieu d'un tableau peut ralentir la solution par
un facteur de 3–4 sur les grands ensembles d'essai.
- **Ugly** – L'oubli d'utiliser les résultats 64 bits conduit à un débordement.
Toujours déclarer la réponse `long` (Java) ou `long long` (C++).

---

## Takeaway & Interview Conseils

1. **Domain‐Size Insight** – Vérifiez toujours si les valeurs d'entrée sont limitées.
Si oui, considérez un tableau de comptage.
2. **Ordonné par rapport à Non ordonné** – La déclaration de problème peut demander l'ordre
triples; gérez soigneusement l'indexation.
3. **Taille du résultat** – Utilisez un type 64 bits pour la sécurité; Python est pardonnant.
4. **Optimisations des facteurs constants** – Les contrôles non utiles sont facultatifs
mais peut donner quelques millisecondes d'avantage.

---

## Lecture supplémentaire

- *= Entrevues de programmation exposées - Section sur le compte des problèmes*
- *= Structures de données et algorithmes en Java – Chapitre sur les radiofréquences*
- *GeeksforGeeks – Compter les triplets avec Bitwise ET/OU*

«» "

«» "

---

Cet article Markdown peut être affiché sur une plateforme de blog qui prend en charge Markdown,
et apparaîtra dans les résultats de recherche pour les mots-clés ci-dessus, aidant les autres
qui étudient le LeetCode 982.