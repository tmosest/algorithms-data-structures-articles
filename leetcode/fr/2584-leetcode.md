---
titre: LeetCode 2584. Split the Array pour fabriquer des produits Coprime -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Le problème (Code Leet 2584)

> **Split le tableau pour fabriquer des produits Coprime* *
> *Tarde*

On vous donne un tableau entier 0 indexé `nums` de longueur `n`.
Une division à l'indice «i» ( «0 ≤ i ≤ n‐2») est **valable** si

«» "
produit(nums[0 ... i]) et produit(nums[i+1 ... n-1])
«» "

sont coprimes ('gcd == 1').
Retourner le plus petit de ces `i`, ou `-1` si aucune scission n'existe.

«» "
nombres = [4, 7, 8, 15, 3, 5] → réponse = 2
«» "

«1 ≤ n ≤ 104», «1 ≤ nums[i] ≤ 106».

---

- Oui. 2. Le point de vue fondamental

Deux produits sont coprime **iff** aucun facteur principal n'apparaît dans *deux* parties.
Donc une scission est impossible quand une prime qui apparaît dans le préfixe
apparaît également plus tard dans le suffixe.

**Idée**

* Pour chaque facteur principal `p`, n'oubliez pas le **dernier indice** où `p` apparaît.
* En scannant de gauche à droite, gardez la trace du **farthest** dernier-index
parmi toutes les premières vues jusqu'ici.
Si l'indice actuel `i` est égal à cet indice le plus éloigné,
pas de prime vu dans le préfixe apparaît plus tard → split à `i` est valide.

Ceci donne un algorithme **O(n log M)** (`M = 106`) après un tamis linéaire.



---

- Oui. 3. Algorithme (Code de Pseudo)

«» "
construire SPF[1 ... 1_000_000] // Le plus petit facteur primaire

// 1ère passe : enregistrer le dernier index de chaque prime
dernierIndex[p] = -1
pour i = 0 ... n-1
pour chaque p primaire distinct des nombres[i] (en utilisant SPF)
dernierIndex[p] = i

// 2ème passe : balayage pour trouver la division
le plus éloigné = 0
pour i = 0 ... n-2
pour chaque p primaire distinct des nombres[i]
la plus éloignée = max(plus élevée, dernier indice[p])
i == la plus éloignée // toutes les premières dans le préfixe terminé ici
retour
retour -1
«» "

*Les premiers* sont obtenus en divisant à plusieurs reprises par le SPF
Le facteur courant disparaît.
Les boucles internes s'exécutent dans `O(number_of_distinct_primes)` –
au maximum ~7 pour tout nombre ≤ 106.

---

- Oui. 4. Exécution

On trouvera ci-dessous des solutions prêtes à l'emploi dans **Java**, **Python** et **C++**.

> **Astuce** – Pour une programmation ou une entrevue concurrentielles, précalculez
> tamiser une fois et la réutiliser dans les cas d'essai.

---

#### 4.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
int MAX = 1_000_000;
int[] spf = nouveau int[MAX + 1];

statique {
// tamis linéaire pour le plus petit facteur primaire
pour (int i = 2; i <= MAX; i++) spf[i] = i;
pour (int i = 2; i * i <= MAX; i++) {
i) {/ I est premier
pour (int j = i * i; j <= MAX; j += i) {
si (spf[j] == j) spf[j] = i;
}
}
}
}

/** retourner des facteurs principaux distincts de x en utilisant le tableau spf */
liste statique privée<entier> factorize(int x) {
Liste <Integer> res = nouvelle liste de distribution<>();
pendant que (x > 1) {
int p = spf[x];
rés.add(p);
pendant que (x % p == 0) x /= p;
}
retour rés;
}

recherche publique ValidSplit(int[] nums) {
int n = longueur nums;
int[] lastIndex = nouvelle int[MAX + 1];
Arrays.fill (dernier indice, -1);

// premier passage – dernière occurrence de chaque prime
pour (int i = 0; i < n; i++) {
pour (int p : factorize(nums[i]) {
dernierIndex[p] = i;
}
}

// deuxième passe – balayage
Int le plus éloigné = 0;
pour (int i = 0; i < n - 1; i++) {
pour (int p : factorize(nums[i]) {
le plus éloigné = Math.max(le plus élevé, dernierIndex[p]);
}
Si (i) le plus éloigné, retourner i;
}
retour -1;
}
}
«» "

---

4.2 Python

'`python
importer des maths
de taper l'importation Liste

MAX = 1 000 000
spf = liste(range(MAX + 1))

# tamis linéaire
pour i dans la gamme(2, int(MAX**0.5) + 1):
si spf[i] == i:
pour j dans la gamme(i *, MAX + 1, i):
si spf[j] == j:
spf[j] = i

def factorize(x: int) -> Liste[int]:
"""retourner des facteurs principaux distincts de x en utilisant spf"""
res = []
pendant que x > 1 :
p = spf[x]
res.append(p)
alors que x % p == 0 & #160;:
x //= p
retour res

def findValidSplit(nums: List[int]) -> Int:
n = len(nums)
dernière = [-1] * (MAX + 1)

# 1ère passe
pour i, v in énumérate(nums):
pour p en factorize(v):
last[p] = i

# 2ème passe
le plus éloigné = 0
pour i dans la plage (n - 1):
pour p en factorize(nums[i]):
la plus éloignée = max (la plus avancée, la dernière [p])
i == le plus éloigné:
retour
retour -1
«» "

*Usage* (Signature de code leet)

'`python
Solution de classe:
def findValidSplit(self, nombres: List[int]) -> Int:
# le corps de la fonction est identique à celui ci-dessus
«» "

---

### 4.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

const int MAX = 1'000'000;
l'unité de mesure de la puissance de sortie,

vide build_sieve() {
pour (int i = 2; i <= MAX; ++i) spf[i] = i;
pour (int i = 2; i * i <= MAX; ++i)
si (spf[i]) i)
pour (int j = i * i; j <= MAX; j += i)
si (spf[j] == j) spf[j] = i;
}

vecteur<int> factorize(int x) {
vecteur<int> rés;
pendant que (x > 1) {
int p = spf[x];
res.push_back(p);
pendant que (x % p == 0) x /= p;
}
retour rés;
}

solution de classe {
public:
int findValidSplit(vector<int> &nums) {
int n = nombres.size();
vecteur statique<int> dernierIndex(MAX + 1, -1);

// 1er passage
pour (int i = 0; i < n; ++i)
pour (int p : factoricize(nums[i]) lastIndex[p] = i;

// 2e passe
Int le plus éloigné = 0;
pour (int i = 0; i < n - 1; ++i) {
pour (int p : factorize(nums[i])
la plus éloignée = max(autrement, dernier indice[p]);
Si (i) le plus éloigné, retourner i;
}
retour -1;
}
};
«» "

---

- Oui. 5. Le blog

> **Titre (friendly SEO)* *
> *Comment résoudre le LeetCode 2584 – Découper le tableau pour fabriquer des produits Coprime*

Voici un article complet de style balisage que vous pouvez coller dans un
plate-forme de blogging, Medium, ou votre propre site Web.
Il est écrit pour **débutants** et **interviewés** tout en contenant
la profondeur technique que les amateurs d'algorithmes désirent.

---

5.1 Introduction

> - Oui. Qu'est-ce que «Split the Array to Make Coprime Products»?
>
> LeetCode 2584 est un problème *Hard* qui teste votre capacité à travailler avec
> factorisation primaire, balayages préfixes et tamis linéaires.
> Dans cet article, nous traversons la solution **optimale O(n log M)**,
> pourquoi cela fonctionne, et comment le mettre en œuvre en Java, Python et C++.

*Mots clés:* LeetCode 2584, tableau divisé, produits coprime, factorisation primaire, tamis linéaire, analyse d'algorithme, prép d'entrevue, défi de codage.

---

5.2 Réévaluation des problèmes

> **Objectif:** Trouver le plus petit indice `i` pour que
> `product(nums[0 ... i])` et `product(nums[i+1 ... n-1])` sont coprimes.
> Si aucun tel `i` n'existe, retourner `-1`.

«» "
Entrée: nombres = [4, 7, 8, 15, 3, 5]
Produit: 2
«» "

---

5.3 Pourquoi il semble difficile au premier coup d'oeil

* Les produits peuvent être astronomiquement grands (`106`^104) – vous ne pouvez pas les multiplier.
* Le calcul systématique gcd pour chaque fraction possible serait O(n2).
* La factorisation répétée par division d'essai est trop lente pour la limite supérieure.

---

### 5.4 Le bon aperçu

1. **Les produits sont la coprime.
de l'arithmétique aux combinatoires.
2. ** Astuce du dernier indice** tourne un global. essai
dans un simple balayage linéaire.
3. **Le tamis linéaire** vous donne le plus petit facteur principal pour chaque nombre
à `106` en ‘O(M)` temps et `O(M)` mémoire – un coût unique.

> **Résultat:**
> *Temps:* `O(n log M)` (= O(n))
> *Memory:* `O(M)` pour le tamis + `O(M)` pour le tableau `lastIndex`
> * Pratique:* Fonctionne confortablement dans les limites de LeetCode pour 104 éléments.

---

5.5 Le côté "Bad"

Mauvais Pourquoi c'est important
-- -- -- -- --
** Empreinte mémoire** – Le tableau SPF ('1 000 001' ints) est ~4 Mo. Autres
**Factorisation – Même avec SPF, vous devez prendre chaque élément en compte deux fois. Toujours trivial pour 104 éléments, mais peut être un goulot d'étranglement si vous utilisez un tamis plus lent ou une division d'essai naïve. Autres
**Exigence de prime distinct** – Nous comptons sur les premiers *distinct*; les premiers duplicates sont ignorés, mais un bug dans la factorisation pourrait doubler. Une mise en œuvre attentive évite cela. Autres

---

5.6 Les alternatives naïves

1. ** Division de première instance par élément (O(n √M)** –
Fonctionne pour de petites entrées, mais facilement à temps sur `106`.
2. **Pre-computing all prime sets via une carte des premiers → liste des indices** –
Utilise plus de mémoire et plus de passes.
3. ** Calcul des produits réels** et appel `gcd` – débordement et `O(n2)` temps.

> *Ces solutions sont de grandes expériences d'apprentissage,
> rarement ce que les intervieweurs ou LeetCode attendent pour un problème *Hard*. *

---

#### 5.7 Étape par étape Passer par l'exemple

«» "
nombres = [4, 7, 8, 15, 3, 5]
Indices: 0 1 2 3 4 5
«» "

Les premiers dans les nombres[i]
Il n'y a pas de différence entre les deux.
D'après les résultats de l'enquête, l'écart entre les taux d'inflation et les taux d'inflation a été plus faible que prévu.
= 1
= 2
Last[3] = 4, Last[5] = 5

Pendant le balayage, après l'indice **2**, le dernier indice est **2**,
On peut se séparer ici.
(Les prénoms `2` et `7` n'apparaissent plus jamais après `i=2`.)

---

#### 5.8 Blocs de code complets (Prêt à coller)

Langue Nom du fichier Fonction clé Autres
- C'est quoi ?
Java "Solution.java" "public int findValidSplit(int[] nums)" Autres
Def findValidSplit(nums: List[int]) -> int:`
"C++" `solution.cpp`" `int findValidSplit(vecteur<int>& nums)`"

> Les trois versions partagent la même logique de balayage linéaire + deux passages.

---

- Oui. 6. Résumé et captures

Autres Qu'est-ce qui a bien fonctionné ?
[En anglais seulement]
**Le tamis linéaire** vous donne SPF en un seul passage. La refacturation de chaque nombre deux fois peut sembler lourde si vous n'utilisez pas SPF. Autres
**Last-index trick** transforme une contrainte globale en une contrainte locale. **Cas d'Edge** – vous devez vous arrêter à `n‐2` parce que la scission nécessite au moins un élément de chaque côté. La mise en œuvre incorrecte de l'extraction primaire distincte (par exemple, oublier de sauter des facteurs égaux) peut en silence briser la logique. Autres
**Complexité** – "O(n log M)" avec une petite constante. **Bogues de mise en œuvre** – erreurs hors-par-un, oubliant de réinitialiser « plus loin » après une scission, etc. L'algorithme peut ne pas être intuitif au début; un diagramme étape par étape aide. Autres

> **Ligne de bottom:**
> Si vous savez factoriser les nombres rapidement (SPF) et garder une trace de la
> *dernier* position de chaque prime, le problème fractionné s'effondre à une simple
> balayage linéaire.
> C'est le raisonnement exact derrière l'officiel le plus efficace.
> Solution LeetCode pour 2584.

---

- Oui. 7. Lecture et ressources supplémentaires

* [Sieve of Eratosthènes – Wikipedia] (https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes)
* [Linear Sieve (algorithme Elias–Zaks)] (https://cp-algorithms.com/algebra/prime-sieve-linear.html)
* [CMD de préfixe et suffixe – Codeforces 1542C]
*Un problème connexe qui utilise la même idée de l'index final. *

---

7.1 Dernier appel à l'action

> **Essayez-le vous-même!* *
> Écrivez la solution dans votre langue préférée, lancez-la contre
> Levet Cases de test de code, puis pousser votre propre torsion – par exemple, retourner le
> liste complète de tous les indices fractionnés valides.
> Partagez votre solution sur GitHub et discutez-en sur LinkedIn;
> la rétroaction de la communauté affinera votre raisonnement.

---

> *Codage heureux, et bonne chance écraser LeetCode 2584! *

---

** Fin de l'article. **

---

**(Soyez libres d'adapter les titres, le formatage ou le style de langue à vos attentes.) * *