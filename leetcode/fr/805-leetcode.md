---
titre: LeetCode 805. Répartition avec la même moyenne -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Aperçu du problème – Diviser le tableau avec la même moyenne
**Code de cap #805** – *Hard*

> Compte tenu d'un tableau «nums», il est divisé en deux sous-tables non vides **A** et **B** (ils peuvent être formés en réorganisant les éléments originaux).
> Si `moyen(A) ==moyen(B)` retourner `true`, sinon retourner `faux`.
>
> Contraintes:
> * `1 ≤ longueur nominale ≤ 30`
> * `0 ≤ nombres[i] ≤ 104`

Parce que la longueur du tableau est minuscule (- 30) nous pouvons nous permettre des solutions exponentielles à temps qui sont assez intelligentes pour tailler des branches impossibles.

---

- Oui. 2. Intuition et principales perspectives

Laissez

«» "
Total général Somme = somme(s)
n = longueur nominale
«» "

Si la moyenne d'un sous-ensemble choisi de taille `k` est égale à la moyenne du tableau entier, alors la somme du sous-ensemble doit être

«» "
cible Total Somme * k / n
«» "

Pour que cela soit un entier, nous avons besoin `(totalSum * k) % n == 0`.
Nous n'avons donc qu'à tester les tailles de sous-ensemble *possible* `k` (1 ... n/2) qui satisfont à la condition de divisibilité et vérifier s'il existe un sous-ensemble de cette taille dont la somme équivaut à `cible Somme.

Trouver un sous-ensemble avec une taille et une somme spécifiques est un problème classique *subset-sum*, mais avec une dimension supplémentaire (la taille).
Deux approches parfaitement adaptées :

1. **Recursive DP + Memoization** – explorez l'arbre de recherche tout en cachant des états déjà vus.
2. **Rencontre dans le milieu** – diviser le tableau en deux moitiés, énumérer toutes les sommes de sous-ensemble dans chaque moitié, puis les combiner.

Tous deux ont la même complexité théorique du pire cas "O(2^(n/2)")", mais le PDD récursif est souvent plus facile à lire et à mettre en œuvre dans les paramètres d'entrevue.

---

- Oui. 3. Pourquoi le DP récursif est-il bon?

* **Readability** – Une seule fonction récursive (`dfs`) capture l'idée, ou saute un élément.
* ** Taille précoce** – Si les éléments restants ne peuvent pas remplir la taille requise (`k + i > n`) ou si la cible devient négative, nous reculons immédiatement.
* **Mémoisation** – Nous ne recalculons jamais le même triple `(i, k, cible)`, de sorte que le nombre d'états distincts est limité par `n * (n/2) * cible` (toujours petite parce que `n ≤ 30`).
* **Déterministe** – Pas de randomisation ou de multipasse sur les données – l'algorithme se comporte de façon prévisible.

---

- Oui. 4. Pourquoi "Bad" ou "Ugly" (et comment l'éviter)

Mauvais/ Pourquoi Fixer
C'est pas vrai.
**Utiliser une clé de chaîne** comme "cible,k,i"` en Java. Autres
**Profondeur de récursion non limitée** dans des langues qui ne optimisent pas les appels de queue. Autres
**Vérifier tous `k` aveuglément** même quand `(total Somme * k) % n != Un travail trop gaspillé Passer ces valeurs `k` tôt. Autres
**Réallocation de mémoire** sur chaque appel DFS. Autres
**Ne pas manipuler les cas de bord** comme des tableaux d'éléments simples. Autres

---

- Oui. 5. Solution – PDD récursif (Mémoisation)

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**. Tous les trois résolvent le problème dans la mémoire *O(2^(n/2)*) et *O(n *)* et sont garantis de fonctionner rapidement pour la taille maximale d'entrée (`n = 30`).

> **Conseil pour les entrevues**: Lorsqu'on vous demande de résoudre ce problème, mentionnez d'abord la vérification de divisibilité, puis dites que vous allez utiliser la récursion + mémoisation. Cela montre que vous connaissez le cœur avant de plonger dans le code.

#### 5.1 Java

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
fractionnement public de booléenArraySameMoyenne(int[] nombres) {
int n = longueur nums;
si (n <= 1) retourner false; // ne peut pas se diviser en deux tableaux non vides

Total Somme = 0;
pour (int x : nombres) total Montant += x;

// Essayez toutes les tailles possibles de sous-ensemble k (1 ... n/2)
pour (int k = 1; k <= n / 2; k++) {
si (long) total Somme * k % n != 0) continuer; // la cible ne serait pas entière
Int cible = (int) ((long) total Somme * k / n);
si (dfs(nums, 0, k, cible, nouvelle HashMap<>()))
retour vrai;
}
retourner faux;
}

// touche mémo : (i, k, cible) -> Booléen
boolean privé dfs(int[] nums, int i, int k, int cible,
Carte<État, mémo Booléen> {
si (k) 0) objectif de retour == 0;
si (cible < 0) k + i > nums.longueur) retourner faux;
État clé = nouvel État(i, k, cible);
si (memo.contientKey(key)) retourne memo.get(key);

// choisir les nombres[i] ou sauter
Booléen res = dfs(nums, i + 1, k - 1, cible - nombres[i], mémo)
dfs(nums, i + 1, k, cible, mémo);
mémo.put(key, res);
retour rés;
}

// Clé immuable pour mémoisation
État de la classe finale statique privée {
int final idx, taille, cible;
État(int idx, taille int, cible int) {
ce.idx = idx; ce.size = taille; ceci. cible = cible;
}
@Override public booléen égal(Object o) {
si (celui-ci) est vrai;
si (!o cas de l'État) retourner faux;
État autre = (État) o;
retourner idx == autre.idx && taille == autre.size && cible == autre.cible;
}
@Override public int hashCode() {
h = 17;
h = 31 * h + idx;
h = 31 * h + taille;
h = 31 * h + cible;
retour h;
}
}
}
«» "

**Pourquoi c'est bon**
* `State` est immuable et utilise une bonne paire `hashCode() / egals()`, de sorte que le `HashMap` se comporte de façon prévisible.
* La fonction récursive est concise et utilise les trois paramètres exacts dont nous avons besoin pour la mémorisation.

5.2 Python

'`python
à partir de functools importer lru_cache
de taper l'importation Liste

Solution de classe:
def splitArraySameMoyenne(self, nombres: List[int]) -> bool:
n = len(nums)
si n <= 1:
Retour Faux

total_somme = somme(s)

# vérifier toutes les tailles de sous-ensemble valides
pour k dans la plage(1, n // 2 + 1):
si (total_somme * k) % n != 0:
poursuivre
cible = (total_somme * k) // n

@lru_cache(maxsize=Aucune)
def dfs(i: int, reste_k: int, restant_cible: int) -> C'est vrai.
s'il reste_k] 0:
retourner la_cible restante == 0
si reste_cible < 0 ou restant_k + i > n:
Retour Faux
# choisir ou sauter l'élément courant
retour (dfs(i + 1, reste_k - 1, restant_cible - nombres[i]) ou
dfs(i + 1, restant_k, restant_cible))

si dfs(0, k, cible):
retour Vrai
Retour Faux
«» "

**Pourquoi c'est bon**
* Le décorateur `@lru_cache` gère automatiquement la mémorisation.
* La profondeur de récursion est sûre (`n ≤ 30`).
* Le code n'est que quelques lignes, ce qui le rend idéal pour les séances d'entrevue rapide.

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
Fendeur de boolArraySameMoyenne(vecteur<int>&nums) {
int n = nombres.size();
si (n <= 1) retourner faux;

Total Somme = 0;
pour (int x : nombres) total Montant += x;

// clé de mémorisation : (idx, k, cible)
Carte_non ordonnée<longe> mémo;

clé automatique = [](int idx, int k, int cible) -> long {
retour (static_cast<long long>(idx) << 40)
(statical_cast <long long>(k) << 20)
static_cast<long long>(cible);
};

fonction<bool(int,int,int)> dfs = [&](int idx, int k, int cible) -> Bool {
si (k) 0) objectif de retour == 0;
si (cible < 0) k + idx > n) retourner false;
longue id longue = clé(idx, k, cible);
auto it = mémo.find(id);
si (it != memo.end()) retourne->seconde;

bool res = dfs(idx + 1, k - 1, cible - nums[idx])
dfs(idx + 1, k, cible);
mémo[id] = res;
retour rés;
};

pour (int k = 1; k <= n / 2; ++k) {
si ((1LL * totalSum * k) % n != 0) poursuivre;
cible int = (int)((1LL * totalSum * k) / n);
si (dfs(0, k, cible)) retourne true;
}
retourner faux;
}
};
«» "

**Pourquoi c'est bon**
* La fonction `key` regroupe les trois entiers en un seul entier 64 bits, donnant une recherche O(1) dans la carte non ordonnée.
* La lambda récursive maintient la logique compacte.

---

- Oui. 6. Analyse de la complexité

L'approche Temps Espace
- C'est quoi ?
(Mémoisation) (le pire cas) (entrées de mémoire)
Rencontrer dans le milieu pour stocker toutes les sommes de sous-ensemble

Avec `n = 30`, `2^(n/2) = 2^15 ↓ 32.768`, qui s'insère confortablement dans la mémoire et fonctionne en quelques millisecondes sur les processeurs modernes.

---

- Oui. 7. À emporter pour les intervieweurs

1. **Mentionnez d'abord la règle de divisibilité**.
2. ** Expliquez le problème de recherche**: sous-ensemble de la taille `k` avec la somme `cible`.
3. **Choisissez récursion + mémoisation** – montrez que vous pouvez écrire propre, mémorisé DFS.
4. **Optionnel**: Si vous demandez une solution à facteur constant encore plus rapide, suggérez Meet‐in‐the‐Middle.

Ce problème démontre la maîtrise de la programmation dynamique*, de la sous-somme* et des astuces de la masquinerie*, ce qui en fait un élément de base des trousses d'entrevues techniques.

---

- Oui. 7. Pensée finale

Recursive DP + Memoization n'est pas juste un hack rapide ; c'est une stratégie éprouvée et conviviale qui équilibre **élégance conceptuelle** et **performance pratique**.
N'hésitez pas à l'écrire dans n'importe quelle langue, et soyez prêt à expliquer les premiers choix de taille et de mémorisation – vous venez de transformer un problème apparemment complexe en une solution concise et efficace!