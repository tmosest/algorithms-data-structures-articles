---
titre: LeetCode 3669. Décomposition équilibrée du facteur K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Décomposition équilibrée des facteurs K – Les bons, les mauvais et les mauvais
**Une interview de style LeetCode (Java-Python-C++)**

> *Si vous préparez une entrevue d'ingénierie logicielle, maîtriser ce problème peut augmenter vos chances d'obtenir un emploi. C'est un problème moyen sur LeetCode, mais les techniques que vous apprenez sont utiles pour un large éventail de questions d'entrevue. *

---

- Oui. 1. Récapitulation des problèmes

> **Décomposition du facteur K dans la balance**
> Compte tenu de deux entiers `n` et `k`, diviser `n` en entiers exactement `k` positifs dont le produit est égal à `n`.
> Return *any* fractionne qui ** minimise la différence entre le plus grand et le plus petit nombre** dans la fraction.

*Exemples*

Diffuseur min-max
- C'est quoi ?
[10, 10]
[2, 2, 11]

**Contrôles* *

* `4 ≤ n ≤ 105`
* `2 ≤ k ≤ 5`
* `k` < nombre total de diviseurs positifs de `n "

Parce que `k` est minuscule, une solution de recul est parfaitement viable.

---

- Oui. 2. Le bon – Pourquoi un simple retour fonctionne

Pourquoi ça compte dans une interview
Récapitulatif
La récursion reflète la définition : "Pick a factor, recurse on the reste product". Autres
**Minimal Boilerplate** Autres
**Résultat déterministe** En forçant un ordre de non-diminution (paramètre «départ»), nous évitons les factorisations dupliquées. Autres
**Ébauche**= Si le produit partiel actuel dépasse `n`, la branche meurt immédiatement. Autres
**Readability**= Clean, facile à expliquer à l'intervieweur. Autres

** Aperçu de l'algorithme**

1. **Fonction récursive** `dfs(remaining, k, start, current) "
* "rester" – ce qui doit encore être pris en compte
* `k` – combien de nombres doivent encore être choisis
* `démarrage` – plus petit diviseur autorisé (enforce l'ordre de non-diminution)
* `current` – liste des numéros choisis jusqu'à présent
2. **Cas de base** – `k == 0`. Si "remaining== 1", nous avons une factorisation complète. Calculez sa diff max‐min et gardez-la si elle s'améliore sur le meilleur jusqu'à présent.
3. **Loop** – itérer `i` de `start` à `remaining` inclusive.
* Si "remaining % i == 0`, ajouter `i` à `current` et revenir avec `remaining / i`, `k-1`, `i`.
* Retour après l'appel récursif.

Parce que `k ≤ 5`, la profondeur de récursion est minuscule, et le nombre d'appels récursifs est confortablement en dessous des limites même pour `n = 105`.

---

- Oui. 3. Les mauvaises – Pièges potentiels

À quoi il ressemble
C'est ce qu'on dit.
**Dupliquer les factorisations**
**High runtime for large `n`**=Enumeration de tous les nombres 1...n dans chaque récursion. Autres
**Overflow or wrong type**= Utiliser `int` pour le produit quand `n` est grand=_______________________________________________________________________________________________________________________________________________________________________________________________________________________________________
**Ne pas manipuler `k` > nombre de diviseurs**
**Ignorer l'objectif de la différence minimale**

---

- Oui. 4. Les pièges et les optimisations de l'Ugly – Edge-Case

#### a) Non-prime, très composite `n "

Lorsque `n` a de nombreux petits facteurs (par exemple `n = 28 = 256`), l'arbre de récursion peut ballonner.
**Optimisation:**
* Au lieu de boucler vers `remaining`, générer les *diviseurs* de `remaining` une fois, les stocker dans une liste, et itérer cette liste.
* Depuis `k ≤ 5`, les frais supplémentaires de la génération de diviseurs sont négligeables mais réduisent considérablement le facteur constant.

#### b) Grand `k` dans un sens théorique

Si les contraintes étaient assouplies (disons "k ≤ 10"), la mémorisation deviendrait essentielle.
**Idée de mémoisation**
«» "
clé = (en attente, k, début)
stocker la meilleure différence trouvée pour cet état
«» "
Toutefois, pour le problème actuel, cela n'est pas nécessaire.

#### c) Dépassement de la pile

La profondeur de récursion est au plus 5, donc c'est sûr en Java, Python et C++.
Si vous aviez un `k` plus grand, le DFS itératif ou le BFS serait plus sûr.

---

- Oui. 5. Solutions complètes

Voici des implémentations propres, prêtes à la production dans **Java, Python et C++**.
Tous les trois utilisent la même stratégie de rétrosuivi décrite ci-dessus.

---

##### 5.1 Java

"Java
Importation de java.util.*;

solution de classe publique {

liste privée<integer> meilleure = nouvelle liste d'array<>();
Int privé meilleur Diff = entier.MAX_VALUE;

vide privé dfs(int restant, int k, int début, liste <integer> curr) {
si (k) 0) {
si (rester) 1) { // factorisation complète
int mx = Collections.max(curr);
int mn = Collections.min(curr);
int diff = mx - mn;
si (diff < bestDiff) { // meilleure solution
le meilleur Diff = diff;
best = nouvelle liste de distribution<>(curr);
}
}
retour;
}

// seuls les diviseurs comptent; nous pouvons arrêter de rester
pour (int i = début; i <= restant; i++) {
i (pour mémoire % i) 0) {
curr.add(i);
dfs(demeure / i, k - 1, i, curr);
curr.remove(curr.size() - 1); // backtrack
}
}
}

[] minDifférence(int n, int k) {
dfs(n, k, 1, nouveau tableau <>());
int[] res = nouveau int[best.size()];
pour (int i = 0; i < best.size(); i++) res[i] = best.get(i);
retour rés;
}

// Exemple d'utilisation
public statique vide principal(String[] args) {
System.out.println(Arrays.toString(nouvelle solution(.minDifférence(100, 2));
System.out.println(Arrays.toString(nouvelle solution().minDifférence(44, 3));
}
}
«» "

**Complexité temporelle** –
Dans le pire des cas, la récursion explore toutes les factorisations de `n` en parties `k`.
Avec `k ≤ 5`, cela est très inférieur à `O(n)` pour les limites données.
**Complexité spatiale** – O(k) pour la pile de récursion + O(k) pour le "meilleur".

---

5.2 Python

'`python
de taper l'importation Liste

Solution de classe:
def _init_(self):
auto.meilleur = []
self.best_diff = flotteur('inf')

def dfs(self, reste: int, k: int, début: int, curr: List[int]) -> Aucun:
si k == 0:
s'il reste == 1 :
diff = max(curr) - min(curr)
if diff < self.best_diff:
self.best_diff = diff
auto.meilleur = curr.copy()
retour

pour i à portée (démarrage, restant + 1):
si le reste % i == 0 & #160;:
Annexe(i)
Self.dfs(remaining // i, k - 1, i, curr)
Chr.pop() # derrière

def minDifférence(self, n: int, k: int) -> Liste[int]:
(n, k, 1, [])
Revenez vous-même. le meilleur


♪ Exemple d'utilisation
si __nom__ == "__main__" :
sol = Solution()
print(sol.minDifférence(100, 2)) # [10, 10]
print(sol.minDifférence(44, 3)) # [2, 2, 11]
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vecteur<int> le meilleur;
int mieux Diff = INT_MAX;

vide dfs(int restant, int k, int début, vecteur<int>& curr) {
si (k) 0) {
si (rester) 1) {
int mx = *max_element(curr.begin(), curr.end());
int mn = *min_element(curr.begin(), curr.end());
int diff = mx - mn;
si (diff < bestDiff) {
le meilleur Diff = diff;
le meilleur est le curr;
}
}
retour;
}

pour (int i = début; i <= restant; ++i) {
i (pour mémoire % i) 0) {
curr.push_back(i);
dfs(demeure / i, k - 1, i, curr);
curr.pop_back(); // backtrack
}
}
}

vecteur<int> minDifférence(int n, int k) {
vecteur <int> curr;
dfs(n, k, 1, curr);
le meilleur retour;
}
};

Int main() {
Solution s;
auto r1 = s.minDifférence(100, 2);
auto r2 = s.minDifférence(44, 3);
pour (int x : r1) cout << x << '; cout << '\n';
pour (int x : r2) cout << x << '; cout << '\n';
}
«» "

---

- Oui. 6. Comment expliquer Dans une interview

> **Démarrer**: "Let" pense à `n` comme un produit de nombres `k`. Si nous choisissons un facteur `f`, nous sommes laissés avec `n/f`, toujours à prendre en compte dans les nombres `k-1`. (en milliers de dollars)
> **Procédé**: Nous utiliserons une première recherche en profondeur. Pour éviter les doubles, nous ne choisissons que les diviseurs dans un ordre non décroissant. (en milliers de dollars)
> **Afficher**: Quand nous atteignons `k = 0`, nous calculons le diff max‐min. Nous gardons la meilleure division. (en milliers de dollars)

Concentrez-vous sur **pourquoi la récursion fonctionne** (dirigée par la définition), **comment nous préparons** (seulement les diviseurs valides), et **comment nous atteignons l'objectif** (suivant le «bestDiff»).

---

- Oui. 7. Takeaways et applications plus larges

* **Backtracking** est un agrafe pour les problèmes d'entrevue de partition/sous-ensemble.
* Enforcer un ordre trié (`start`) est un truc générique pour éliminer les duplicatas dans DFS combinatoire.
* Lorsqu'un problème ajoute un critère d'optimisation (minimiser/maximiser quelque chose), il suffit d'enregistrer le meilleur jusqu'à présent pendant le DFS.
* Pour les entrées plus importantes, le même squelette peut être amélioré avec **diviseur pré-computation** ou **mémisation**.

---

Liste de contrôle rapide avant de soumettre

- [ ] Avez-vous imposé une ordonnance de non-diminution pour éviter les doubles?
- [ ] Avez-vous calculé et mis à jour la meilleure différence max‐min?
- [ ] Avez-vous utilisé le backtracking (poush/pop) pour garder la mémoire basse?
- [ ] Avez-vous testé votre solution sur les exemples et les cases?

---

Mot final

> Une solution de rétrosuivi de minuscules paramètres est un puissant outil d'entrevue.
> Il vous enseigne la récursion, la taille et l'optimisation, tout en résolvant un vrai problème de LeetCode.

** Bonne chance** — et rappelez-vous: * expliquez votre approche, surveillez les duplicatas et gardez-la simple. *

---

Références

* Problème de LeetCode : **Décomposition du facteur K dans la balance**
* Mots-clés : `Returnracking`, `Recursion`, `Divide et Conquer`

---

*Si vous avez trouvé cet article utile, partagez-le avec vos pairs et continuez d'explorer le problème de la décomposition de K‐Factor Balanced. Ta préparation d'interview vient d'être un peu plus robuste ! *