---
titre: LeetCode 2585. Nombre de façons de gagner des points -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2585 – Nombre de façons de gagner des points
> **Hard** – LeetCode

---

- Oui. 1. Récapitulation des problèmes

Vous êtes donné

* `cible` – le total des points que vous voulez marquer (`1 ≤ cible ≤ 1000`).
* `types[i] = [counti, marki]` –
* il y a des questions de type `counti` indistinguables Les "
* chaque question vaut "marki" points
* `1 ≤ comte, marki ≤ 50`, `1 ≤ n = types de longueur ≤ 50`

Combien de façons différentes pouvez-vous atteindre ** exactement** points `cible`?
Retourner la réponse modulo `1 000 000 007`.

> **Exemple**
> `cible = 6, types = [[6,1],[3,2],[2,3]` → **7** voies.

---

- Oui. 2. Idée de haut niveau – Bounded Knapsack DP

Le problème est un knapsack* (ou des pièces limitées) classique.
Nous devons compter, pour chaque valeur de point possible `p` de `0` à `cible`, combien de façons nous pouvons obtenir exactement `p` en utilisant les types de questions disponibles, en respectant la limite par type (`counti`).

Laissez

«» "
dp[p] = nombre de façons d'atteindre exactement les points p
«» "

Initialiser `dp[0] = 1` (il y a un moyen d'atteindre 0 points – ne pas poser de questions).

Pour chaque type de question `(cnt, val)` nous mettons à jour le DP **in inverse**:

Texte
pour i de la cible jusqu'à 0:
pour k de 1 à cnt:
i >= k * valeur:
Dp[i] += Dp[i - k * val]
«» "

Reverser la boucle externe garantit que lorsque nous lisons `dp[i - k * val]` nous utilisons toujours les valeurs du type *précédent*, pas celles que nous écrivons actuellement.
Toutes les opérations sont effectuées modulo "MOD = 1 000 000 007".

La complexité du temps est
«O(cible * n * max(counti)) ≤ 1000 * 50 * 50 = 2,5 × 106»,
Bien dans les limites.
La complexité de l'espace est "O(cible)".

---

- Oui. 3. Code

Voici des implémentations propres et prêtes à la production dans **Java**, **Python** et **C++**.

> *Les trois solutions utilisent la même logique DP – seule la syntaxe diffère. *

---

#### 3.1 Java

"Java
Importation de java.util.*;

solution de classe {
int final statique privé MOD = 1_000_000_007;

moyens publics intToReachTarget(int cible, int[][] types) {
int[] dp = nouvelle int[cible + 1];
dp[0] = 1;

pour (int[] t : types) {
nombre int = t[0];
marque int = t[1];

// ordre inverse : de la cible à 0
pour (int i = cible; i >= 0; i--) {
// essayez de répondre à des questions k de ce type
pour (int k = 1; k <= nombre; k++) {
coût int = k * mark;
si (i < coût) pause; // ne peut pas répondre aux questions k
dp[i] = (dp[i] + dp[i - coût]) % MOD;
}
}
}
retour dp[cible];
}
}
«» "

---

3.2 Python

'`python
Solution de classe:
MOD = 1 000 000 007

Def ways ToReachTarget(self, cible: int, types: List[List[int]]) -> Int:
dp = [0] * (objectif + 1)
dp[0] = 1

pour cnt, valeur en types:
# ordre inverse
pour i dans l'intervalle (cible, -1, -1):
pour k dans la plage(1, cnt + 1):
Coût = k * valeur
i < coût:
pause
dp[i] = (dp[i] + dp[i - coût]) MOD

retour dp[cible]
«» "

---

### 3.3 C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
l'état statique du constexpr MOD = 1'000'000'007;

public:
int waysToReachTarget(int cible, vector<vector<int>>& types) {
vecteur<int> dp(cible + 1, 0);
dp[0] = 1;

pour (const auto &t : types) {
nombre int = t[0];
marque int = t[1];

pour (int i = cible; i >= 0; --i) { // ordre inverse
pour (int k = 1; k <= nombre; ++k) {
coût int = k * mark;
Si i < coût) pause;
dp[i] = (dp[i] + dp[i - coût]) % MOD;
}
}
}
retour dp[cible];
}
};
«» "

---

- Oui. 4. Article de blog – Knapsack, DP & Pourquoi cela compte pour votre prochain travail

> **Longueur:** ~1 200 mots
> **Audience:** Ingénieurs logiciels se préparant pour des entretiens LeetCode ou de conception de système
> **Don:** Amiable, perspicace, parsemé d'entretiens

---

♪ 5. Le bon, le mauvais et l'acharnement

> *Ce que chaque recruteur recherche dans un code de candidat : clarté, efficacité et une touche d'intelligence. *

---

#### 5.1 Le bon – Pourquoi le Knapsack Bounded gagne

**Ce que les recruteurs aiment**
Il n'y a pas de lien entre les deux.
**Temps-Complexité**="O(target · n · maxCount)="2,5 M operations" montre que vous pouvez résoudre *Hard* LeetCode dans < 0,1 s"
**Space‐Efficiency**= Mémoire `O(target)' (=4 KB en Java/C++/Python)= Démonstration d'un état d'esprit à faible empreinte de pied==
**Scalabilité**= Fonctionne pour 1000 points, 50 types, 50 questions chacune=Poigne les contraintes les plus graves Autres
**Le déterminisme**Le DP garantit le comptage correct

---

5.2 Les mauvaises – Pièges communs

1. **Mettre à jour DP dans le mauvais ordre* *
*Si vous bouclez `i` de `0` à `cible`, vous aurez le double compte* (chaque type peut être réutilisé des temps illimités).
**Fix:** inverser la boucle.

2. **Utilisation «int» sans module**
Le nombre brut peut croître astronomiquement (`C(50, 0) * ...`).
**Fix:** toujours `dp[i] %= MOD.

3. **Ignorer les limites par type**
Une pièce de monnaie DP naïve, sans limite, surestimerait.
**Fix:** boucle imbriquée sur `k = 1 ... cnt`.

4. **Récursion + frais généraux de mémorisation**
La profondeur de récursion peut atteindre 51 (safe), mais la limite de récursion de Python est de 1000 – encore très bien, mais DP est plus facile à cache et plus rapide.

---

5.3 L'Ugly – Un Brute-Force moins efficace

> *Un DFS simple qui essaie chaque combinaison est O(`cnti^n`*.
> Il n ' est pas possible d ' appliquer la formule < < cible = 1000, n = 50 > > .

'`python
def bad_solution(cible, types):
à partir de functools importer lru_cache

@lru_cache(Aucun)
def dfs(idx, restant):
s'il reste == 0:
retour 1
si idx == len(types) ou restant < 0:
retour 0
cnt, val = types[idx]
somme de retour(dfs(idx + 1, restant - k * val) pour k dans l'intervalle(cnt + 1)) % MOD

retour dfs(0, cible)
«» "

Alors que *agréable à lire*, cette approche serait chronométrée sur de grandes entrées – un compromis classique.

---

- Oui. 6. Pourquoi ce problème (et la solution) est un grand écran d'entrevue

1. ** Démontre la maîtrise de DP**
C'est un agrafe. Résoudre correctement montre que vous pouvez gérer *état* et *transition* design.

2. **S'intéresse aux contraintes**
L'utilisation du PDD inverse pour respecter les limites plutôt qu'une approche naïve parle d'optimisation réfléchie.

3. **Fait ressortir des pratiques de codage propres* *
Les arithmétiques modulaires à temps constant et les boucles claires rendent votre code lisible pour les évaluateurs.

4. ** Polyvalence des langues *
Être capable de traduire la même logique en Java, Python ou C++ prouve l'agnosticisme de la langue – évaluable en équipes polyglottes.

---

- Oui. 7. SEO-Friendly Wrap-Up (Mots-clés cibles: Knapsack, Code du jeu 2585, Interview du PD, Points d'acquisition DP, Changement de pièce lié)

> **Titre**: *Master LeetCode 2585 – Bounded Knapsack DP pour le nombre de façons de gagner des points*
> **Description de la Méta**: *Solve LeetCode 2585 (Nombre de façons d'obtenir des points) en Java, Python et C++ en utilisant un Knapsack DP limité efficace. Apprenez l'algorithme, la complexité et le code d'entrevue. *
> **Tags**: #Dynamique Programmation #Knapsack #LeetCode #Interview #CodingInterview #Algorithme

---

- Oui. 8. TL;DR (résumé d'une ligne)

Utiliser un DP à ordre inversé limité à la poignée :

Texte
dp[0] = 1
pour chaque type (cnt, val):
pour i = cible ... 0:
pour k = 1 ... cnt:
i >= k*val:
dp[i] = (dp[i] + dp[i-k*val]) % MOD
«» "

Cela fonctionne dans ~2,5 M ops et utilise la mémoire `O(target)` – parfait pour LeetCode 2585.

---

Bon codage ! C'est ce qu'il a dit