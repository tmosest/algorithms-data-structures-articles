---
titre: LeetCode 481. Chaîne magique -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## 481. Chaîne magique – Code & Blog

---

- Oui. 1. Récapitulation des problèmes

Une chaîne **magique** `s` se compose uniquement des chiffres `1` et `2`.
Si vous regardez le *run-longueur* de chiffres identiques consécutifs dans `s`,
séquence de ces longueurs d'exécution est exactement "s" lui-même.

«» "
s = 1 22 11 2 1 22 1 22 11 2 11 22 ...
↑ ↑ ↑ ↑
longueurs = 1 2 2 1 1 2 1 2 1 2 ...
«» "

Compte tenu d'un entier `n (1 ≤ n ≤ 10^5)`, indiquez combien de `'1''s apparaissent dans la
les premiers caractères `n` de `s`.

---

- Oui. 2. Brute-Force contre Optimal

L'approche Temps L'espace Commentaires
C'est pas vrai.
Construire `s` caractère-par-caracter jusqu`à `n` , **O(n)** , **O(n)** , fonctionne pour les contraintes, mais `StringBuilder` en Java ou concaténation répétée en Python peut être coûteux. Autres
Pré-calculer les longueurs d'exécution dans un tableau et générer des `s` à la volée. Autres
Définition récursive avec mémoisation. **O(n)**. **O(n)**. Autres

> ** Bon** – temps O(n), mémoire O(n), simple à comprendre.
> **Bad** – Utiliser la concaténation `String` en Java/Python peut frapper le temps quadratique.
> **Ugly** – Certaines solutions en ligne utilisent `LinkedList` ou récursion, qui ajoutent des frais généraux inutiles et obscurcissent la logique.

---

- Oui. 3. Algorithme (temps linéaire, espace O(n))

1. **Pré-alloquer** un `int[] s` de la longueur `n` pour stocker la chaîne magique comme
numéros 1 ou 2.
2. `s[0] = 1`, `s[1] = 2`, `s[2] = 2`.
Ce sont les trois premiers chiffres qui satisfont à la définition.
3. Gardez deux pointeurs :
* `idx` – l'index dans `s` que nous lisons actuellement pour connaître la longueur d'exécution.
* `cur` – la position actuelle que nous écrivons dans `s`.
4. Alors que `cur < n`:
* `len = s[idx]` (longueur de la course: 1 ou 2).
* `val = 3 - s[cur-1]` – basculer entre 1 et 2.
* Ecrivez des copies de `val` dans `s` à partir de `cur`.
Arrêtez si nous atteignons `n`.
* Incrément "idx" et "cur" en conséquence.
5. Enfin, comptez le nombre de «1» dans les premières positions «n».

Parce que chaque caractère est écrit exactement une fois, l'algorithme est linéaire.

---

- Oui. 4. Exécution

C'est vrai. Java (style LeetCode)

"Java
solution de classe {
public int magique Chaîne(int n) {
si (n) 0) retour 0;

// Construisez la chaîne en tant que tableau int.
int[] s = nouvelle int[n];
s[0] = 1; // les trois premiers chiffres sont fixés
si (n > 1) s[1] = 2;
si (n > 2) s[2] = 2;

int idx = 2; // position en s indiquant la longueur d'exécution
int cur = 3; // prochaine position libre à écrire
int = 1; // nous avons déjà placé un '1' à s[0]

pendant que (cur < n) {
int len = s[idx]; // 1 ou 2
val int = 3 - s[cur - 1]; // basculer entre 1 et 2

// Ecrire des copies `len` de `val`
pour (int i = 0; i < len && cur < n; i++) {
s[cur++] = valeur;
si (val) 1) ceux++;
}
idx++;
}

les retours;
}
}
«» "

Python

'`python
Solution de classe:
def magiqueString(self, n: int) -> Int:
si n] 0:
retour 0

s = [0] * n
s[0] = 1
si n > 1: s[1] = 2
si n > 2: s[2] = 2

idx, cur, ones = 2, 3, 1 # idx: lire pos, cur: écrire pos, ones: compter

pendant le traitement < n:
longueur = s[idx] # 1 ou 2
val = 3 - s[cur - 1] # basculer entre 1 et 2

pour _ dans la plage (longueur):
si cur >= n:
pause
s[cur] = valeur
si val == 1 :
+= 1
pour 1
idx += 1

retour
«» "

C++

'`cpp
solution de classe {
public:
int magique Chaîne(int n) {
si (n) 0) retour 0;
vecteur<int> s(n, 0);
s[0] = 1;
si (n > 1) s[1] = 2;
si (n > 2) s[2] = 2;

int idx = 2; // lire l'index
Int cur = 3; // index d'écriture
int = 1; // nous avons déjà placé un 1

pendant que (cur < n) {
int len = s[idx]; // 1 ou 2
val int = 3 - s[cur - 1]; // bascule

pour (int i = 0; i < len && cur < n; ++i) {
s[cur++] = valeur;
si (val) 1) +ones;
}
++idx;
}
les retours;
}
};
«» "

---

- Oui. 5. Article de blog – LeetCode 481: Magical String – Une plongée profonde pour votre prochaine entrevue de codage

> **Description détaillée**
> Master LeetCode 481 Chaîne magique en Java, Python et C++ avec une solution O(n). Comprendre le problème, les pièges, et comment répondre à cette question d'entrevue moyenne.

---

Introduction

Si vous préparez des entretiens d'ingénierie logicielle, le problème LeetCode **481. Magical String** est un exercice parfait *medium*-difficile. Il teste votre capacité à:

- Traduisez une définition formelle en code.
- Générer une séquence à la volée sans stocker toute la chaîne en mémoire.
- Optimisez le temps et l'espace.

Dans ce post, nous allons marcher à travers l'énoncé de problème, illustrer une solution O(n) propre, examiner les pièges communs (=mauvais et=ugly=) et fournir des implémentations prêtes à la copie dans **Java**, **Python** et **C++**.

---

Récapitulation du problème (Ce que veut l'intervieweur)

> Une chaîne *magique* `s` se compose uniquement des chiffres `1` et `2`.
> Si vous regroupez des chiffres identiques consécutifs dans `s`, la longueur *run* de chaque groupe est égale au chiffre correspondant dans `s` lui-même.

> **Objectif:**
> Retourner le nombre de `'1`s dans les premiers caractères `n` de `s` (`1 ≤ n ≤ 10^5`).

> **Exemples**
> `` "
> n = 6 → s = 122112 → 3 un
> n = 1 → s = 1 → 1 un
> `` "

---

Pourquoi ce problème est-il intéressant ?

- **Séquence autoréférentiel** – La chaîne se définit elle-même, un motif classique vu dans les problèmes de type Fibonacci.
- **Run‐Length Encoding** – Vous allez construire une chaîne à partir de sa représentation de longueur d'exécution, un tour d'interview commun.
- **Grande taille d'entrée** – Vous devez éviter les approches O(n^2) telles que la concaténation de cordes répétées.

---

Les approches naïves

1. **Concaténation répétée** –
"Java
Chaîne s = ";
pendant que (longueur() < n) {
s += (s.longueur() == 0 ? "1" : (s.longueur() % 2 == 0 ? "22" : "1");
}
«» "
*Pourquoi c'est mauvais :* Chaque `+=` sur un `String` crée un nouvel objet → O(n2) time.

2. **Liste de caractères liée** –
"Java
List LinkedList<Integer> list = nouvelle List LinkedList<>();
liste.add(1); liste.add(2); liste.add(2);
«» "
*Pourquoi c'est mauvais:* lié Les frais généraux de la liste sont élevés, et vous toujours itérer sur la liste plusieurs fois.

Ces modèles sont faciles à écrire mais font échouer la solution pour `n = 10^5`.

---

Stratégie optimale (les bonnes)

1. **Pré-allouer un tableau** de taille `n` (ou un `int[]` en Java, `vector<int>` en C++, `list[int]` en Python).
2. **Utilisez deux indicateurs** :
- `idx` – lit la longueur d'exécution du tableau.
- `cur` – écrit le groupe suivant dans le tableau.
3. **Toggle entre 1 et 2** par `val = 3 - prev`, en évitant les déclarations conditionnelles.
4. **Count `1`s à la volée** – pas besoin d'un deuxième passage.

**Complexité temporelle:** `O(n)` – chaque élément est écrit exactement une fois.
**Complexité spatiale:** `O(n)` – nous conservons la gamme de longueur `n` (le stockage minimal nécessaire).

---

(Illustration)

«» "
Début: s[0] = 1, s[1] = 2, s[2] = 2
idx = 2 (pointage au troisième élément indiquant la longueur d'exécution 2)
cur = 3 (position libre suivante)

Boucle :
len = s[idx] = 2 // Nous avons besoin d'un groupe de 2 chiffres
val = 3 - s[cur-1] = 3-2 = 1 // basculer à 1
Écrire 2 exemplaires de 1 aux postes 3 et 4
+= 2
idx++ → 3
cur++ → 5
«» "

Continuer jusqu'à "cur". Le tableau contient maintenant les premiers chiffres `n` de la chaîne magique, et nous savons déjà combien nous en avons compté.

---

C'est vrai. Le code

> **Java**
> ``java
> solution de classe {
> public int magique Chaîne(int n) { ... }
> }
> `` "

> **Python**
> ``python
> solution de classe:
> def magiqueString(self, n: int) -> int: ...
> `` "

> **C++**
> ``cpp
> solution de classe {
> public:
> Int magiqueString(int n) { ... }
> };
> `` "

*(Voir les blocs de code ci-dessus pour les implémentations complètes.) *

---

#### Cas de bord et essais

Source : Produit prévu Raison
- C'est quoi ?
Uniquement le premier chiffre `1`. Autres
"12" – toujours un "1". Autres
§ 3° 1° `122` – seul le premier chiffre est `1`. Autres
- deux "1".
100000 $ *some number*= S'assurer que l'algorithme fonctionne dans le temps. Autres

Testez toujours les limites inférieures, la valeur exacte `n = 10^5` et les valeurs moyennes aléatoires.

---

Traces d'entrevue courantes

Qu'est-ce que regarder?
-- -- -- -- -- -- --
Erreurs hors-par-un. Autres
Autres Débordement entier de `n ≤ 10^5`, donc `int` est sûr. Autres
Utiliser `val = 3 - prev` au lieu de `prev == 1 ? 2 : 1`. Autres
Les boucles inutiles Éviter les boucles imbriquées qui itèrent sur les parties déjà générées. Autres

---

#### Réflexions finales (les voyous)

Quelques solutions sur Internet :

- ** Génération récursive** avec mémoisation – fonctionne mais cache la nature linéaire et augmente le risque de profondeur de cheminée.
- **LinkedList ou Queue** pour la séquence longueur d'exécution – ajoute des facteurs constants qui importent pour des limites de temps serrées.
- **StringBuilder avec de nombreux appels `append`** – toujours O(n) mais le facteur constant est plus élevé que la manipulation de tableau.

Tenez-vous à l'approche linéaire basée sur le réseau pour une solution propre et rapide.

---

Référence Résumé

- **Mots-clés**: *LeetCode 481, *Magical String*, *Java solution*, *Python solution*, *C++ solution*, *codage interview*, *algorithme*, *entretien d'emploi*, *ingénierie logicielle*, *programmation interview questions*.
- **Meta**: -Solve LeetCode 481 – Chaîne magique en Java, Python & C++ avec un algorithme O(n). Apprenez comment répondre à cette question d'entrevue. (en milliers de dollars)

---

- Oui. 6. Liste de contrôle de l'approche à suivre

- [ ] Comprendre la définition d'une chaîne magique.
- [ ] Utilisez un tableau pour stocker la séquence – aucune concaténation de chaîne.
- [ ] Maintenir deux pointeurs (`idx`, `cur`) et basculer les valeurs avec `3 - prev`.
- [ ] Comptez ceux que vous générez.
- [ ] Vérifier avec les cas de bord (1, 2, 3, 4, 10^5).
- [ ] Gardez le temps de solution O(n) et la mémoire O(n).

Bonne chance, et le codage heureux!