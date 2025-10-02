---
titre: LeetCode 3409. La plus longue séquence avec la diminution de la différence adjacente -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Problème : Subséquence la plus longue avec diminution de la différence adjacente (Code Leet 3409)

> **Donné d'un nombre entier (2 ≤ n ≤ 104, 1 ≤ nums[i] ≤ 300)**
> Trouvez la longueur de la plus longue séquence « seq » de telle sorte que
> ""seq[i+1] - suite[i]" est non-augmentation.
> Retournez la longueur maximale possible.

Exemples
Entrée Sortie Explication
C'est pas vrai.
"[16,6,3]"" "3" "[16,6,3]" → diffs "[10,3]" Autres
[6,5,3,4,2,1] → diffs `[2,2,1]` Autres
Mots-clés: Autres

La contrainte `nums[i] ≤ 300` est un indice clé : l'espace d'état peut être limité par le domaine de valeur au lieu de la longueur du tableau.

---

Aperçu de la solution

1. ** Programmation dynamique sur la valeur et la dernière différence**
`dp[v][d]` = plus longue séquence que **démarre** avec la valeur `v` et dont **première différence adjacente** est `d`.
En scannant le tableau de droite à gauche, nous mettons à jour ces états.

2. **Transition**
Pour l'élément actuel `x = nombres[i] "
* Pour chaque valeur *prochaine* `y` (1 ... 300)
* ' diff ==x - y="
* `dp[x][diff] = max(dp[x][diff], dp[y][diff] + 1)`
– nous pouvons ajouter `x` avant un subséquence qui commence par `y` et utilise le même `diff`.
* Après avoir considéré tous `y`, nous devons également laisser la séquence ** raccourcir la différence** (puisque la séquence ne peut devenir *plus* non-augmentation).
* Pour "diff" de 1 à 299
`dp[x][diff] = max(dp[x][diff], dp[x][diff-1)] "
* Suivre la réponse globale `ans = max(ans, dp[x][diff]'.

3. **Complexité**
* **Heure**: `O(n * V2)` où `V = 300`.
`n ≤ 104`, `V2 = 90 000` → environ **9 × 106** opérations – bien en dessous de la limite.
* **Espace**: `O(V2)` → une matrice entière `301 × 301` (~0,36 Mo).

4. **Pourquoi cela fonctionne**
* L'analyse de la bonne garantie que lorsque nous traitons `x`, toutes les continuations possibles sont déjà calculées.
* La propriété "non-augmentation" est imposée par la deuxième passe (`dp[x][diff] = max(dp[x][diff], dp[x][diff-1])" qui dit essentiellement: *=Si nous pouvons obtenir la longueur `k` avec la différence `diff-1`, nous pouvons également obtenir la longueur `k` avec la différence `diff` (puisque la séquence peut rester la même ou réduire la différence).

---

Mise en œuvre du code

Voici des solutions propres et autonomes pour **Java**, **Python** et **C++**. Chaque fichier contient la classe `Solution` (style LeetCode) et une méthode `main` qui démontre l'utilisation.

---

### Java

"Java
Importation de java.util.*;

solution de classe publique {
public int le plus longSujet(int[] nombres) {
Int MAX_VAL = 300;
// dp[value][diff] = longueur la plus longue commençant par 'value' et premier diff 'diff '
int[] dp = nouveau int[MAX_VAL + 1][MAX_VAL + 1];
Int ans = 0;

pour (int i = longueur nominale - 1; i >= 0; i--) {
int x = nombres[i];

// Considérons toutes les valeurs suivantes possibles
pour (int y = 1; y <= MAX_VAL; y++) {
Int diff = Math.abs(x - y);
dp[x][diff] = Math.max(dp[x][diff], dp[y][diff] + 1);
}

// Autoriser la diminution de la diff (contrainte non croissante)
pour (int diff = 1; diff <= MAX_VAL; diff++) {
dp[x][diff] = Math.max(dp[x][diff], dp[x][diff - 1];
ans = Math.max(ans, dp[x][diff]);
}
}
le retour des an;
}

// - Oui. Démo - Oui.
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.longestSubséquence(nouvelle int[]{16, 6, 3})); // 3
Système.out.println(sol.longestSubséquence(nouvelle int[]{6, 5, 3, 4, 2, 1}); // 4
System.out.println(sol.longestSubséquence(nouvelle int[]{10,20,10,19,10,20}); // 5
}
}
«» "

---

Python

'`python
Solution de classe:
plus longtemps Subséquence(self, nombres: list[int]) -> Int:
MAX_VAL = 300
* dp[v][d] -> longueur commençant par la valeur v et le premier diff d
dp = [[0] * (MAX_VAL + 1) pour _ dans la plage (MAX_VAL + 1)]
ans = 0

pour x en sens inverse(nombres):
# Transition vers toutes les valeurs suivantes possibles
pour y dans la plage(1, MAX_VAL + 1):
diff = abs(x - y)
dp[x][diff] = max(dp[x][diff], dp[y][diff] + 1)

# Autoriser la diminution de la diff (propriété non croissante)
pour diff dans la plage(1, MAX_VAL + 1):
dp[x][diff] = max(dp[x][diff], dp[x][diff - 1])
ans = max(ans, dp[x][diff])

retour et

♪ - Oui. Démonstration...
si __nom__ == "__main__" :
sol = Solution()
print(sol.longestSubséquence([16, 6, 3])) # 3
print(sol.longestSubséquence([6, 5, 3, 4, 2, 1]) # 4
print(sol.longestSubséquence([10,20,10,19,10,20]) # 5
«» "

---

C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
la plus longue subséquence(vecteur<int>& nombres) {
const int MAXV = 300;
vecteur<vecteur<int>> dp(MAXV + 1, vecteur<int>(MAXV + 1, 0)
Int ans = 0;

pour (int i = (int)nums.size() - 1; i >= 0; --i) {
int x = nombres[i];

// transition vers toutes les valeurs suivantes possibles
pour (int y = 1; y <= MAXV; ++y) {
int diff = abs(x - y);
dp[x][diff] = max(dp[x][diff], dp[y][diff] + 1);
}

// permettre la diminution de la diff (contrainte non croissante)
pour (int diff = 1; diff <= MAXV; ++diff) {
dp[x][diff] = max(dp[x][diff], dp[x][diff-1];
ans = max(ans, dp[x][diff];
}
}
le retour des an;
}
};

// - Oui. Démonstration...
Int main() {
Solution sol;
Cout << sol.longestSubséquence({16, 6, 3}) << endl; // 3
Cout << sol.longestSubséquence({6, 5, 3, 4, 2, 1}) << endl; // 4
Cout << sol.longestSubséquence({10,20,10,19,10,20}) << endl; // 5
retour 0;
}
«» "

---

Article de blog (optimisé par le référencement)

---

# Subséquence la plus longue avec diminution de la différence adjacente – une plongée profonde dans le LeetCode 3409

**Mots clés**: LeetCode 3409, Subséquence la plus longue avec diminution de la différence adjacente, programmation dynamique, Java, Python, C++, interview, FAANG, interview de codage, algorithme, solution DP

---

C'est pas vrai. Quel est le problème ?

On vous donne une liste des entiers (`1 ≤ nombres[i] ≤ 300`).
Vous devez choisir une sous-séquence où la différence absolue entre les choix consécutifs ne croît jamais :
«= a2 – a1= ≥= a3 – a2= ≥ ...»
Votre objectif : **Durée maximale**.

Pourquoi est-ce difficile ?
- La subséquence peut sauter des éléments arbitraires.
- Oui. La contrainte non croissante couples chaque paire adjacente.
- Les solutions exponentielles Brute-force sont impossibles pour `n = 104`.

---

C'est vrai. L'initiative «Bien» – Tirer parti de la petite gamme de valeurs

La pointe la plus puissante: **`nums[i] ≤ 300`**.
Au lieu de traiter chaque indice comme un état séparé (ce qui nous donnerait un "O(n2)" DP), nous traitons **la valeur** elle-même comme faisant partie de l'état.
Cela réduit l'espace d'état des indices `104` à seulement `300` valeurs distinctes.

---

C'est vrai. Les Fails de la PDD naïve

Une première tentative pourrait penser :
`dp[i]` = la plus longue séquence commençant à l'index `i`.
Mais lorsque vous essayez d'ajouter la contrainte non croissante, vous finissez par devoir vous souvenir de la *dernière différence* utilisée, conduisant à un état comme `dp[i][lastDiff]`.
Même alors, `lastDiff` peut être jusqu'à 300, donc vous êtes toujours coincé à `O(n2)` pour la boucle intérieure.

Cette approche est *mauvaise* parce qu'elle explose rapidement à quelques centaines de millions d'opérations, bien au-delà des limites d'entrevue typiques.

---

C'est pas vrai. La tentative "Ugly" – Même pire

Certaines personnes tentent une approche gourmande ou à deux points, en supposant que toujours choisir la plus petite différence suivante fonctionne.
Cela échoue dans les cas d'essai comme `[10,20,10,19,10,20]`, où l'avidité manquerait l'optimum `[10,20,10,19,10]`.
L'écueil de l'Escaut n'est pas responsable des éléments **supports** et de la propriété *pleine* non-augmentation.

---

C'est vrai. Le meilleur – PDD basé sur la valeur avec rétrécissement de différence

5.1 Définition de l'État

`dp[value][diff]` – subséquence la plus longue **en commençant par `value`** où la première différence est `diff`.
Nous remplissons cette table tout en itérant le tableau d'entrée de **de droite à gauche**.

5.2 Transition

Pour le courant `x = nombres[i]`:

Valeur suivante `y` Actualiser l'explication
- C'est quoi ?
Tous `y` (1...300)""dp[x][diff] = max(dp[x][diff], dp[y][diff] + 1)""nous pouvons prépendre `x` avant une sous-séquence qui commence déjà par `y` et utilise la même première différence. Autres

Après tout `y`, nous devons permettre à la séquence d'effacer la différence (puisque la séquence peut utiliser une première différence *large* mais ne pas augmenter):

Raison de la mise à jour
C'est quoi, ça ?
"diff` 1...300 "dp[x][diff] = max(dp[x][diff], dp[x][diff-1]" Si nous pouvons obtenir la longueur `k` avec une différence plus petite, nous pouvons également obtenir la longueur `k` avec une différence plus grande (ou égale) parce que la subséquence peut rester la même ou réduire l'écart. Autres

Au cours de cette deuxième passe, nous mettons à jour le maximum global `ans`.

Pourquoi le droit à Travaux à gauche

Le traitement à partir de la fin garantit que tous les futurs subséquences sont déjà connus, donc la transition est valide. Il s'agit d'une astuce classique *offline DP* utilisée dans de nombreux problèmes de LeetCode (p. ex., la plus longue séquence croissante avec un DP basé sur la valeur).

---

#### 6-

Point à emporter
C'est pas vrai.
**Utiliser les contraintes** Autres
**Compression de l'état**= Valeur + dernière diff → `O(V2)` au lieu de `O(n2)`. Autres
**Mise à jour en deux phases** Autres
**Complexité du temps** Autres
**Complexité spatiale** → petite mémoire. Autres
**Les cas d'Edge**=Tous les nombres sont égaux → répondent `n`. Autres
1. Expliquez l'intuition tôt. 2. Afficher le concept de table DP. 3. Discuter de la complexité. 4. Mentionnez le tour de la valeur-domaine. Autres

> **Conseil pro**: Lorsque vous discutez de ce problème dans une entrevue, soulignez le PDD *basé sur la valeur* comme une façon classique d'exploiter de petites gammes entières. Mentionnez que vous irez de l'arrière pour vous assurer que les futurs États sont prêts.

---

#### 7-SEO-Optimized Summary

- **Titre**: LeetCode 3409 – Subséquence la plus longue avec diminution de la différence adjacente.
- **Description détaillée**: Découvrez une solution de programmation dynamique propre pour LeetCode 3409. Apprenez le code Java, Python et C++, la complexité du temps et de l'espace et les conseils d'entrevue pour FAANG. (en milliers de dollars)
- **Phrases clés**: LeetCode 3409, Subséquence la plus longue avec diminution de la différence adjacente, solution DP, Java, Python, C++, problème d'entrevue, interview de codage, FAANG, analyse d'algorithme.

---

Bonus : Exécution du code

Les trois extraits ci-dessus contiennent une section `main` / `demo` qui imprime les résultats attendus pour les entrées de l'échantillon. Copiez le code dans un fichier (`Solution.java`, `solution.py`, `solution.cpp`) et exécutez-le avec votre compilateur/interprète préféré pour voir la magie en action.

---

Bon codage, et que votre subséquence reste toujours non-augmentation! Les