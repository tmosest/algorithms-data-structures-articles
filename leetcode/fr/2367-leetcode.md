---
titre: LeetCode 2367. Nombre de triplets arithmétiques -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Aperçu du problème

**LeetCode 2367 – Nombre de triplettes arithmétiques* *

On vous donne un tableau "nums" et un entier "diff".
Un triplet `(i, j, k)` est appelé un triplet arithmétique* lorsque

Description
C'est pas vrai.
Les indices sont en ordre croissant.
Nombres [j] - nums[i] == diff`-
"nums[k] - nums[j] == diff`

Retournez le nombre de triplets arithmétiques uniques en «nums».

> **Constraints**
> * < 3 ≤ longueur maximale ≤ 200 '
> * `0 ≤ nums[i] ≤ 200`
> * `1 ≤ diff ≤ 50`
> * Les "nums" augmentent strictement

---

- Oui. 2. Pourquoi ce problème est un bon démarreur d'entrevue

Autres Qu'est-ce que c'est ?
C'est-à-dire
Autres **TrÃ ̈s petite taille d'entrÃ©e** Autres
**Élimine les indices dupliqués et nous permet d'utiliser des fonctions de recherche simples. Autres
**Straightforward logique**= Concerne la capacité du candidat à repérer un modèle plutôt que des astuces obscures. Autres
**Plusieurs solutions optimales**= Permet de discuter des compromis entre clarté et rapidité. Autres

---

- Oui. 3. Idées de solution

1. **Brute-Force ('O(n3)')** – itérer sur tous les triples et vérifier l'état.
* Assez rapide pour les limites données, mais pas élégant. *

2. **Two-Pointer / Two-Loop (`O(n2)`)** – pour chaque `i` trouver `j` de telle sorte que `nums[j] = nums[i] + diff`, puis trouver `k` avec `nums[k] = nums[j] + diff`.
* Bon pour l'apprentissage des techniques de pointeur. *

3. **HashSet / Booléen Array ('O(n)')** – stocker chaque élément dans un ensemble.
Pour chaque élément `x`, si les deux `x+diff` et `x+2*diff` sont présents, nous avons trouvé un triplet.
*Optimal et propre. *

Voici les trois implémentations de **Java, Python et C++**.

---

- Oui. 4. Code

#### 4.1 Java

"Java
Importer java.util. HashSet;
Importer java.util. Jeu;

solution de classe publique {
/* ------------------ O(n) Solution HashSet */
arithmétique int publicTriplets(int[] nums, int diff) {
Définir<integer> set = nouveau HashSet<>();
pour (int num : nums) set.add(num);

nombre int = 0;
pour (int num : nombres) {
si (set.contient(num + diff) && set.contient(num + 2 * diff)) {
count++;
}
}
le nombre de retours;
}

/* ------------------ O(n) Solution de tableau booléen */
arithmétique int publicTripletsBoolean(int[] nums, int diff) {
// valeurs <= 200, donc le tableau de taille fixe est sûr
booléen[] présent = nouveau booléen[201];
nombre int = 0;

pour (int num : nombres) {
si (num >= 2 * diff && present[num - diff] && present[num - 2 * diff]) {
count++;
}
présent[num] = vrai;
}
le nombre de retours;
}

/* ------------------ Solution à deux boucles O(n^2) */
arithmétique int publicTripletsO2(int[] nums, int diff) {
int n = longueur nums;
nombre int = 0;
pour (int i = 0; i < n; i++) {
pour (int j = i + 1; j < n; j++) {
si (nums[j] - nums[i] != diff) break; // array augmente
pour (int k = j + 1; k < n; k++) {
Si (nums[k] - nums[j] == diff) count++;
sinon si (nums[k] - nums[j] > diff) se cassent;
}
}
}
le nombre de retours;
}
}
«» "

4.2 Python

'`python
de taper l'importation Liste

Solution de classe:
♪ ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
# Solution O(n) utilisant un ensemble
♪ ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
def arithmétiqueTriplets(self, nombres: List[int], diff: int) -> Int:
s = ensemble(s)
nombre = 0
pour x en nombres:
Si x + diff en s et x + 2 * diff en s:
nombre += 1
Nombre de retours

♪ ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
# O(n) solution utilisant une liste de booléens de taille fixe (valeur <= 200)
♪ ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
def arithmétiqueTriplets_bool(self, nombres: List[int], diff: int) -> Int:
Présent = [Faux] * 201
nombre = 0
pour x en nombres:
si x >= 2 * diff et présent[x - diff] et présent[x - 2 * diff]:
nombre += 1
présent[x] = Vrai
Nombre de retours

♪ ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
# O(n^2) force brute avec deux boucles
♪ ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
def arithmétiqueTriplets_bruteforce(self, nombres: List[int], diff: int) -> Int:
n = len(nums)
nombre = 0
pour i dans la plage(n):
pour j dans la plage(i + 1, n):
si nombres[j] - nums[i] != diff:
pause
pour k (j + 1, n):
si nombres[k] - des nums[j]] diff:
nombre += 1
élif nombres[k] - nombres[j] > diff:
pause
Nombre de retours
«» "

### 4.3 C++

'`cpp
#incluez <vecteur>
#inclut <unordered_set>

solution de classe {
public:
// ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
// Solution O(n) utilisant un_set non commandé
// ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
arithmétique intTriplets(const std::vector<int>& nums, int diff) {
std::unordered_set<int> s(nums.begin(), nums.end());
nombre int = 0;
pour (int x : nombres) {
si (s.count(x + diff) && s.count(x + 2 * diff))
+ nombre;
}
le nombre de retours;
}

// ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
// Solution O(n) utilisant un tableau booléen de taille fixe (valeur <= 200)
// ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
Int arithmétiqueTriplets Bool(const std::vector<int>& nums, int diff) {
bool présent[201] = {faux};
nombre int = 0;
pour (int x : nombres) {
si (x >= 2 * diff && present[x - diff] && present[x - 2 * diff])
+ nombre;
présent[x] = vrai;
}
le nombre de retours;
}

// ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
// Solution O(n^2) avec deux boucles imbriquées
// ______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________
Int arithmétiqueTripletsO2(const std::vector<int>& nums, int diff) {
int n = nombres.size();
nombre int = 0;
pour (int i = 0; i < n; ++i) {
pour (int j = i + 1; j < n; ++j) {
si (nombres[j] - nombres [i] != diff) pause;
pour (int k = j + 1; k < n; ++k) {
si (nums[k] - nums[j] == diff) ++count;
sinon si (nums[k] - nums[j] > diff) se cassent;
}
}
}
le nombre de retours;
}
};
«» "

---

- Oui. 5. Article de blog: -Le bon, le mauvais, et l'acharnement du nombre de Triplets arithmétique

Titre

**Nombre de triplets arithmétiques – LeetCode 2367: Une entrevue de codage en profondeur

*(Mots clés: LeetCode, Nombre de Triplets arithmétiques, Java, Python, C++, interview, interview de codage, algorithme, hashset, complexité temporelle, O(n), entretien d'emploi)*

---

5.2 Introduction

> Lors de votre prochaine interview de codage, vous êtes demandé de trouver tous les *arithmétique triplettes* dans un tableau trié. C'est facile, alors pourquoi beaucoup de candidats luttent-ils? (en milliers de dollars)

Cet article déballe le **good** (ce qui rend le problème accessible), le **bad** (pièges communs), et le **ugly** (les cas de bord délicat) de LeetCode 2367. Nous allons aussi voir comment le résoudre en **Java, Python et C++** en moins de 10 lignes de code.

---

5.3 Les bonnes

Aspect Explication
C'est pas vrai.
**Modèle intuitif**="nums[i] + diff` et `nums[i] + 2*diff` – une propriété claire de "look-ahead". Autres
Autres **Small Input Space**= Avec seulement 200 éléments, nous pouvons expérimenter plusieurs algorithmes. Autres
**Strictly Augmenter** , garantit que les indices sont uniques ; pas besoin de s'inquiéter des triplets dupliqués. Autres
**Solutions optimales multiples** Autres

> *Cue* de référencement: LeetCode 2367 solution facile, question d'interview triplet arithmétique

---

5.4 Les mauvais

Piège
- Oui.
**Confuser `+` vs `-`**= De nombreux candidats vérifient accidentellement `x-diff` au lieu de `x+diff`. Autres
**Erreurs de l'index de l'index de l'index de l'index de l'index de l'index de l'index de l'index de l'index** Autres
**Ignorer la propriété qui augmente de façon stricte**=L'écriture d'un ensemble générique qui fonctionne pour n'importe quel tableau (y compris les duplicatas) perd du temps. Autres
**Ignorer les contraintes**=L'utilisation d'un tableau dynamique de taille `nums.size(*2` au lieu d'un tableau booléen de 201-slots peut entraîner une inefficacité mémoire. Autres

> *Cue* de référencement: erreurs d'interview communes, pièges hashset

---

5.5 La moche

Comment le manipuler
- C'est quoi ?
**Large `diff`** Autres
**L'excès de flux dans C++**. Le `x + 2*diff` peut déborder `int` si le `diff` était énorme; mais pas dans ce problème, toujours jeté à `long' pour la sécurité dans le code du monde réel. Autres
**Nombres négatifs**= Bien que les contraintes les interdisent, une solution générique devrait toujours gérer les négatifs gracieusement. Autres
**Sortir de l'erreur d'hypothèse** Passer le tri gagne du temps mais vous ne pouvez pas le réorganiser. Autres

> *Cueil de référence*: LeetCode défi de codage pièges, Debugging interview code

---

- Oui. 6. Liste de contrôle de l'approche à suivre (pour les intervieweurs)

- **Demander la solution optimale "O(n)"** – le candidat devrait proposer une approche de jeu/d'arrachage.
- **Probe pour la manipulation de cas de bord** – vérifier s'ils considèrent "x ≥ 2*diff".
- **Discuse les compromis** – pourquoi un tableau booléen est plus rapide qu'un jeu de hachage dans ce cas.
- **Suivi facultatif** – Que faire si les "nums" n'augmentaient pas strictement?

---

- Oui. 7. TL;DR

- **Objectif** : Compte `(i, j, k)` avec `nums[j] - nums[i] = nums[k] - nums[j] = diff`.
- **Optimal**: `O(n)` utilisant un jeu de hachage ou un tableau booléen de taille fixe.
- **Code**: solutions prêtes à fonctionner dans **Java, Python, C++**.
- **Valeur d'entrevue**: Démontre la reconnaissance des motifs, l'utilisation des ensembles et la sensibilisation à la complexité temporelle.

Bonne chance pour écraser ce problème LeetCode et clouer votre prochaine interview de codage!