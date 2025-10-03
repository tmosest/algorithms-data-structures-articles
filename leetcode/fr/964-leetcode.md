---
titre: LeetCode 964. Les opérateurs les moins importants pour exprimer le numéro -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code de Leet 964 – **Les opérateurs les plus bas pour exprimer le numéro**
Aperçu du problème

Étant donné un seul entier positif `x`, vous pouvez former une expression de la forme

«» "
x (op1) x (op2) x (op3) x ...
«» "

lorsque chaque `op` est de `+`, `-`, `*` ou `/`.
L'opérateur de division renvoie un nombre rationnel, les parenthèses sont **non** autorisées, et l'ordre habituel des opérations s'applique.

Votre objectif est de produire une expression qui évalue exactement à `cible` tout en utilisant **le moins d'opérateurs possibles**.
Retournez le nombre minimum d'opérateurs.

> **Constraints**
2 ≤ x ≤ 100
> * 1 ≤ objectif ≤ 2 × 108

---

## Aperçu de la solution

Le problème est un exemple classique de programmation *dynamique avec mémoisation* plus un peu de maths.
L'idée clé est :

1. **Éliminer la cible dans la plus grande puissance de "x" qui ne la dépasse pas**.
2. **Essayez deux stratégies* *
* ** Ajouter** la plus grande puissance et résoudre la partie restante.
* **Utilisez la prochaine plus grande puissance** et **soustraire** l'excédent.
3. **Memoir** résultats intermédiaires de sorte que chaque sous-problème ne soit résolu qu'une seule fois.

La profondeur de récursion est logarithmique dans la cible (`O(log_x cible)`), qui maintient l'utilisation de la pile minuscule.
La complexité de temps globale est `O(log_x cible × log_x cible)` parce que pour chaque niveau nous pouvons considérer les deux options, chacune menant à un autre appel récursif.
La complexité de l'espace est `O(log_x cible)` en raison de la carte de mémoisation et de la pile de récursion.

---

Détails de la mise en œuvre

- Oui. 1. Cas de base

* **`cible == 0`** → 0 opérateurs.
* ** 'cible < x '**
* **Ajouter** des copies `cible` des opérateurs `x/x` → `2 *cible` (`x/x` utilise deux opérateurs, plus chaque ajout).
* **Soustraire** de `x` → `2 * (x - cible) + 1` opérateurs (`x - (x-cible)*(x/x)`).
Choisissez le plus petit des deux.

- Oui. 2. Étape récursive

Laissez

«» "
pow = puissance la plus élevée de x telle que pow ≤ cible
cnt = nombre de multiplications pour obtenir pow (cnt = floor(log_x cible))
«» "

* **Option A (ajoutée)* *
«» "
opérateurs = cnt + resoudre(cible - pow)
«» "

* ** Option B (soustraction)** – seulement si `pow * x - cible < cible` (c'est-à-dire qu'il est moins cher de dépasser et de soustraire)
«» "
opérateurs = cnt + 1 + résolvez(pouvoir * x - cible)
«» "

Retournez le minimum des deux options.

---

Code des échantillons

Vous trouverez ci-dessous des solutions complètes et exploitables dans **Java, Python et C++**.
Chaque mise en œuvre utilise la mémorisation, gère de grands nombres avec `long`/`int64`, et est fortement commentée pour la clarté.

---

### Java (8 ms – la solution 2024 de Hassam)

"Java
Importer java.util. HashMap;
Importer java.util. Carte;

solution de classe publique {
// Carte de mémoisation : cible -> nombre minimal d'opérateurs
carte privée<Long, entier> mémo = nouveau HashMap<>();

au moins OpsExpressTarget(int x, int cible) {
// La routine récursive compte un opérateur *extra* au niveau supérieur
retour dfs(x, cible) - 1;
}

Int privé dfs(long x, longue cible) {
si (cible) 0) retour 0; // case de base
si (memo.contientKey(target)) retourne memo.get(target);

// -------- 1. cible < x ---------
si (cible < x) {
// a) ajouter des copies cibles de x/x
int add = (int) (2 * cible);
b) Soustraire de x
int sub = (int) (2 * (x - cible) + 1);
int ans = Math.min(ajouter, sous);
mémo.put(cible, ans);
le retour des an;
}

// -------- 2. cible >= x --------
// Trouver la plus grande puissance de x ne dépassant pas la cible
long pow = 1;
int cnt = 0; // nombre de multiplications pour atteindre pow
pendant que (pow * x <= cible) {
pow *= x;
cnt++;
}

// Option A: ajouter la plus grande puissance
int ans = cnt + dfs(x, cible - pow);

// Option B : utiliser la puissance suivante et soustraire
long suivant Pow = pow * x;
si (nextPow - cible < cible) { // moins cher à dépasser
int optB = cnt + 1 + dfs(x, suivant Pow - cible);
ans = Math.min(ans, optB);
}

mémo.put(cible, ans);
le retour des an;
}

// Conducteur simple pour tester la solution
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.leastOpsExpressTarget(3, 19)); // 5
Système.out.println(sol.leastOpsExpressTarget(5, 501)); // 8
Système.out.println(sol.leastOpsExpressTarget(100, 100_000_000)); // 3
}
}
«» "

> **Pourquoi ça marche* *
> *Mémoisation* nous permet de ne jamais recalculer la même cible.
> Le `-1` à la fin corrige le surcompte du premier opérateur, que la récursion inclut naturellement.

---

### Python (25 ms)

'`python
importations
à partir de functools importer lru_cache

Solution de classe:
moins OpsExpressTarget(self, x: int, cible: int) -> Int:
sys.setrecursionlimite(10 ** 7)

@lru_cache(Aucun)
def dfs(t: int) -> Int:
Si t == 0:
retour 0
si t < x:
# ajouter t copies de x/x -> 2*t ops
ajouter = 2 * t
# soustraire de x -> 2*(x-t)+1 ops
sous = 2 * (x - t) + 1
retour min(ajouter, sub)

# puissance maximale de x n'excédant pas t
pow_ = 1
cnt = 0
alors que pow_ * x <= t:
pow_ *= x
cnt += 1

# Option A: ajouter la plus grande puissance
res = cnt + dfs(t - pow_)

# Option B : utiliser la puissance suivante et soustraire
_pow suivante = pow * x
si next_pow - t < t:
res = min(res, cnt + 1 + dfs(next_pow - t))

retour res

retour dfs(cible) - 1 # ajuster pour l'opérateur supplémentaire compté

Chauffeur
si __nom__ == "__main__" :
sol = Solution()
print(sol.leastOpsExpressTarget(3, 19)) # 5
print(sol.leastOpsExpressTarget(5, 501)) # 8
print(sol.leastOpsExpressTarget(100, 100_000_000))# 3
«» "

---

### C++ (12 ms)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
unordered_map<long long, int> mémo;

Int minimum OpsExpressTarget(int x, int cible) {
retour dfs(x, cible) - 1; // supprimer l'opérateur supplémentaire compté à la racine
}

particulier:
int dfs(long long x, longue cible) {
si (cible) 0) retour 0;
si (memo.count(target)) retourne mémo[target];

// --------- cible < x --------
si (cible < x) {
int add = static_cast<int>(2 * cible); // ajouter des copies t de x/x
int sub = static_cast<int>(2 * (x - cible) + 1); // soustraire de x
mémo[target] = min(add, sub);
retourner mémo[cible];
}

Objectif >= x --------
long pow = 1;
int cnt = 0; // multiplications pour atteindre pow
pendant que (pow * x <= cible) {
pow *= x;
++cnt;
}

// Option A: ajouter la plus grande puissance
int ans = cnt + dfs(x, cible - pow);

// Option B : utiliser la puissance suivante et soustraire
long et long suivant Pow = pow * x;
si (nextPow - cible < cible) { // moins cher à dépasser
as = min(ans, cnt + 1 + dfs(nextPow - cible));
}

mémo[cible] = ans;
le retour des an;
}
};

// - Oui. harnais d'essai simple...
Int main() {
Solution s;
Cout << s.leastOpsExpressTarget(3, 19) << endl; // 5
Cout << s.leastOpsExpressTarget(5, 501) << endl; // 8
Cout << s.leastOpsExpressTarget(100, 100000000) << endl; // 3
retour 0;
}
«» "

> **Pourquoi le code C++ est rapide**
> *Unordered_map* donne une recherche à temps constant en moyenne.
> Utilisation de "long long" garde la multiplication en sécurité même lorsque `x == 100` et `cible` est proche de `2×108`.

---

## -- Interviews à emporter

Aspect **Bien**
- C'est quoi ?
**Readability** Aucun.Le cas de base de l'option Add/sub est non intuitif – vous devez penser à `x/x` comme une paire d'opérateur *simple*. Autres
**Performance** La profondeur de récursion pourrait atteindre la limite de Python sur certains interprètes ; augmenter la limite de récursion. Autres
**Manipulation d'un boîtier d'Edge** Aucun. Autres
**Pièges spécifiques à la langue** Nécessité de butter la limite de récursion et regarder pour TLE sur les grandes entrées. Faites attention avec les collisions par hachage par défaut de `unordered_map`. Autres

---

Pourquoi ce problème est un *Gold-Mine* pour les entrevues

1. **Mathematical Insight** – Les intervieweurs aiment les problèmes qui peuvent être résolus en pensant à l'extérieur de la boîte (ici: utiliser la prochaine puissance de `x`).
2. **Maîtrise de programmation dynamique** – La solution est une démonstration claire de PDD *top-down avec mémoisation*.
3. **Échanges de complexité** – Vous pouvez parler de la profondeur de la récursion, de la sécurité de la pile et du plan de hachage.
4. **Manipulation de la valise** – Explique comment traiter avec élégance `cible < x`.

> **Astuce Pro** – Pour expliquer la solution, commencez par *=Et si nous choisissons la plus grande puissance?==* Ceci indique immédiatement à l'intervieweur que vous êtes sur la bonne voie.

---

Titre et mots clés

> **Titre**:
> **LeetCode 964 – Moins d'opérateurs pour Express Number – Java, Python, C++ Solutions + Interview Deep‐Dive**

> ** Mots-clés principaux* *
> * LeetCode 964
> * Moins d'opérateurs pour exprimer le numéro
> * Mise à jour DP
> * cible de log de profondeur de récursion
> * Solution Java
> * Solution Python
> * Solution C++

> ** Mots-clés secondaires* *
Ordre des opérations
> * la division retourne rationnelle
> * entretien de programmation dynamique

---

Les pensées finales

LeetCode 964 est un problème plus intelligent que prévu**.
Si vous maîtrisez l'astuce puissance-de-x' et mémorisez les sous-problèmes, vous obtiendrez une solution rapide et concise** dans n'importe quelle langue.
Pratiquez l'écriture de routine récursive dans votre langue préférée; c'est une vitrine parfaite de la façon dont les mathématiques et DP peuvent se combiner pour résoudre des énigmes de construction d'expression apparemment complexes.

Bonne chance pour votre prochaine interview : laissez tomber cette solution dans votre repo, collez le code dans votre éditeur et affichez la vitesse Java de 8 ms ! C'est ce qu'il a dit