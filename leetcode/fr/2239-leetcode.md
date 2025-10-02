---
titre: LeetCode 2239. Trouver le numéro le plus proche à zéro -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 2239 – Trouver le numéro le plus proche de zéro
** Difficulté :** Facile **Tags:** Array **Complexité:** temps `O(n)`, `O(1)` espace

> **Problème**
> Avec un tableau entier `nums`, retournez l'élément qui est *clost* à `0`.
> S'il y a deux nombres avec la même distance absolue (par exemple, `-2` et `2`), retourner le **large**.

> **Exemples**
> 1. `nums = [-4,-2,1,4,8]` → `1`
> 2. `nums = [2,-1,1]` → `1`

> **Constraints**
> - `1 ≤ n ≤ 1000`
> - `-10^5 ≤ nums[i] ≤ 10^5`

---

Pourquoi ce problème se pose dans les entrevues

C'est bon C'est mauvais
C'est quoi ?
Autres **Énoncé simple et propre** – idéal pour une question d'échauffement. **Pas de cas de bord** si vous ne pensez qu'aux valeurs absolues. **Ambiguité**: certains candidats oublient de gérer la valeur plus grande sur la règle de l'égalité. Autres
**Simple pass** – temps `O(n)`, espace `O(1)`. Le tri mène à une mauvaise réponse si vous gardez la première réponse "closest" au lieu de la réponse plus grande. Autres
**Language agnostic** – fonctionne en Java, Python, C++, etc. Le signe `0` n'a pas d'importance, mais vous devez être prudent avec `Integer. MIN_VALUE` et `entier. MAX_VALUE`. Autres

---

## Solution optimale (4 lignes en C++, 5 en Java, 6 en Python)

L'idée clé : garder deux candidats

1. ** Le plus positif** (`pos`) – le plus petit nombre non négatif.
2. **Le plus négatif** (`nég`) – le plus grand nombre négatif (le plus proche à zéro du côté gauche).

Après avoir balayé le tableau, choisissez celui qui est le plus proche de zéro; sur une cravate, choisissez la plus grande valeur numérique.

### Java

"Java
solution de classe publique {
public int findFermerNumber(int[] nums) {
int pos = entier.MAX_VALUE; // non négatif le plus proche
int neg = entier.MIN_VALUE; // négatif le plus proche (le plus important)

pour (int x : nombres) {
si (x >= 0 && x < pos) pos = x;
si (x < 0 && x > ng) neg = x;
}

// Si un côté n'est jamais apparu, retournez l'autre.
Si (pos) Integer. MAX_VALUE) retour neg;
si (négatif) Integer.MIN_VALUE) retourne pos;

// Tie: pos == abs(neg) → choisir la plus grande (pos)
si (pos) Math.abs(neg)) retourne pos;

retour (pos < Math.abs(neg)) ? pos : neg;
}
}
«» "

Python

'`python
Solution de classe:
def trouver Numéro le plus proche(self, nombres: List[int]) -> Int:
pos = flotteur('inf') # non négatif le plus proche
ng = -float('inf') # négatif le plus proche (le plus important)

pour x en nombres:
si x >= 0 et x < pos:
pos = x
si x < 0 et x > nég:
ng = x

si pos == flotter('inf'): retourner neg
i ng == -float('inf'): retourner pos

# Tie: choisir le plus grand (pos)
si pos == abs(neg):
retour
retourner pos si pos < abs(neg) sinon neg
«» "

C++

'`cpp
solution de classe {
public:
int findFermerstNumber(vector<int>& nums) {
int pos = INT_MAX; //
int neg = INT_MIN; // le plus négatif

pour (int x : nombres) {
si (x >= 0 && x < pos) pos = x;
si (x < 0 && x > ng) neg = x;
}

si (pos) INT_MAX retourne neg;
si (négatif) INT_MIN retourne pos;

si (pos == abs(neg)) retourner pos; // lien → plus grand
retour (pos < abs(neg)) ? pos : neg; // proche de zéro
}
};
«» "

Les trois implémentations fonctionnent dans **`O(n)`** temps et **`O(1)`** espace auxiliaire, et ils gèrent correctement la règle de cravate.

---

Étape par étape

1. **Initialiser** deux valeurs sentinelles :
- `pos = +.." (ou `entier. MAX_VALEUR') → stocker le nombre *le plus petit* non négatif.
- `neg = –--" (ou `Intéger.MIN_VALUE`) → pour stocker le nombre négatif *le plus important*.

2. **Scan une fois**: Pour chaque élément `x "
- Si `x >= 0` et `x < pos`, mettre à jour `pos`.
- Si `x < 0` et `x > neg`, mettre à jour `neg`.

3. **Poignée manquante**:
- Si `pos` n'a jamais été mis à jour → tous les numéros sont négatifs → retourner `neg`.
- Si `neg` n'a jamais été mis à jour → tous les numéros sont non-négatifs → retourner `pos`.

4. **Résoudre la cravate**:
- Si `pos', les deux sont également proches → retourner la plus grande (`pos`).
- Sinon, retournez celui avec une plus petite distance absolue à zéro.

5. **Retour** la valeur choisie.

---

## Description du blog optimisé SEO & Meta

**En-tête :**
> LeetCode 2239: Trouver le numéro le plus proche à zéro – Java, Python & C++ O(1) Solution spatiale

**Meta Description:**
> Master LeetCode 2239 avec une solution 4 lignes propre en Java, Python et C++. Apprenez l'algorithme, les cas de bord et les conseils d'entrevue. Parfait pour coder la préparation d'entrevue et la maîtrise de l'algorithme.

---

Article de blog – Le bon, le mauvais, et le mauvais

Introduction

Lors d'un entretien pour un rôle d'ingénierie logicielle, les intervieweurs aiment les problèmes qui sont *simple à déclarer mais difficile à résoudre correctement*. LeetCodeS **2239 – Trouver le numéro le plus proche à Zero** est l'un de ces joyaux cachés. L'énoncé est presque trop propre : Retournez l'élément le plus proche de zéro ; sur une cravate, choisissez le plus grand. Pourtant, beaucoup de candidats trébuchent parce qu'ils négligent la règle de l'égalité ou perdent du temps avec un tri inutile.

Dans cet article, nous allons disséquer le problème, expliquer pourquoi il est idéal pour les interviews, et marcher à travers une solution rock-solid, **O(n)** en Java, Python, et C++. Nous allons également discuter des pièges communs (les mauvais) et comment les éviter (les laids).

---

### La bonne : pourquoi ce problème est une question d'entrevue de premier ordre

1. **Clarté de la déclaration* *
Le problème peut être expliqué en une phrase. Pas de nuances cachées, juste un seul objectif.

2. ** Temps linéaire, espace constant**
Le défi idéal pour l'entrevue : *un passage*, *O(1) mémoire*. Vous pouvez démontrer l'efficacité algorithmique sans recourir à des structures de données supplémentaires.

3. **Language-agnostique**
Fonctionne dans n'importe quel langage courant – Java, Python, C++, Allez, JavaScript. Idéal pour les candidats qui connaissent plusieurs langues.

4. **Edge-Case Rich**
Bien que la plage d'entrée soit petite (`n ≤ 1000`), les valeurs peuvent être aussi basses que `-10^5`. Cela vous oblige à penser aux valeurs sentinelles et à éviter les débordements.

5. **Exigence de rupture* *
Ajoute une torsion subtile : S'il y a plusieurs réponses, retournez le nombre avec la plus grande valeur. Beaucoup de candidats ignorent cela, conduisant à de mauvaises réponses.

---

### Les mauvaises : idées fausses et pièges communs

C'est faux
- C'est quoi ?
Il suffit de trier et de choisir l'élément intermédiaire. Le tri est inutile et `O(n log n)`. Pire, après tri, vous devez toujours comparer les deux éléments intermédiaires pour décider de la plus grande valeur. Autres
Retour `Math.abs(nums[0])` d'abord rencontré. Autres
Utiliser `abs(entier. MIN_VALUE)` en Java. Autres
Ignorer la règle de l'égalité. Vous échouerez sur des cas comme `[2, -2]` ou `[0, -1]`. Autres
Utiliser un HashMap pour stocker des valeurs absolues. Une mémoire supplémentaire ('O(n)') et doit encore résoudre le lien. Autres

---

- Oui. L'Ugly: Pourquoi certaines solutions semblent Messy

Certains candidats écrivent une force brute de 20 lignes avec des boucles imbriquées, ou ils comptent sur des ruisseaux et des expressions lambda qui masquent la logique fondamentale. Une solution désordonnée non seulement risque des pénalités de performance, mais rend aussi difficile pour l'intervieweur de voir que vous comprenez les principes algorithmiques.

---

Nettoyez, Code lisible – Le réel

Ci-dessous nous présentons une logique de base concise de 4 lignes (à l'exclusion de la plaque de chaudière). Nous allons voir comment le traduire en trois langues populaires.

#### Java (5 lignes dans la méthode)

"Java
int pos = entier. MAX_VALUE, neg = entier.MIN_VALUE;
pour (int x : nombres) {
si (x >= 0 && x < pos) pos = x;
si (x < 0 && x > ng) neg = x;
}
Return pos == Integer.MAX_VALUE ? Négatif
: neg == Integer.MIN_VALUE ? os
Math.abs(neg) ? os
: pos < Math.abs(neg) ? pos : neg;
«» "

#### Python (7 lignes dans la méthode)

'`python
pos, neg = flotteur('inf'), -float('inf')
pour x en nombres:
si x >= 0 et x < pos: pos = x
Si x < 0 et x > ng: ng = x
return neg if pos == float('inf') other pos if neg == -float('inf') other pos if pos == abs(neg) other pos if pos < abs(neg) other neg
«» "

#### C++ (4 lignes dans la méthode)

'`cpp
int pos = INT_MAX, neg = INT_MIN;
pour (int x : nombres) {
si (x >= 0 && x < pos) pos = x;
si (x < 0 && x > ng) neg = x;
}
INT_MAX ? Négatif
INT_MIN ? os
: pos == abs(neg) ? os
: pos < abs(neg) ? pos : neg;
«» "

Pourquoi ça marche ? *
- **Les valeursentinelles** garantissent que nous avons toujours une comparaison valide plus tard.
- Oui. La chaîne ternaire gère les 4 scénarios en une seule déclaration de retour.
- Oui. Pas de structures de données auxiliaires, pas de tri – juste un balayage linéaire.

---

Liste de contrôle de la préparation de l'entrevue

Objet
- Oui.
Autres Lire attentivement l'énoncé du problème (surtout la règle de l'égalité). Autres
Autres 2. Comprendre les contraintes (`n ≤ 1000`, valeurs allant jusqu'à `±10^5`). Autres
Il faut penser à une solution `O(n)` – un seul passage avec deux variables. Autres
Autres Test sur les cas de bord : tous négatifs, tous positifs, mélangés, liés. Autres
Autres Coder dans votre langue préférée, puis traduire à d'autres. Autres
Autres 6. Discuter clairement de la complexité du temps et de l'espace. Autres

---

Les pensées finales

LeetCode 2239 est une question d'entrevue classique *-clean-yet-subtle. Une solution bien structurée démontre :

- **La pensée algorithmique** (passe linéaire, espace constant).
- **Attention au détail** (manipulation des attaches, éviter le débordement).
- **La clarté du code** (pas de tri inutile ni de structures de données).

Maîtrisez ce problème, ajoutez-le à votre arsenal d'entretien, et vous impressionnerez les recruteurs avec vitesse et précision.

---

Code de référence rapide

"Java
// Java
public int findFermerNumber(int[] nums) { /* ... */ }

// Python
Solution de classe:
def trouver Numéro le plus proche(self, nums: List[int]) -> int: /* ... */

// C++
solution de classe {
public:
int findFermerstNumber(vector<int>& nums) { /* ... */ }
};
«» "

Bon codage et bonne chance pour votre prochaine interview!