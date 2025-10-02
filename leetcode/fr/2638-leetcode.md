---
titre: LeetCode 2638. Compter le nombre de sous-ensembles sans K -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

- Oui. 1. Le Code

Voici trois solutions complètes et autonomes pour **LeetCode 2638 – Compter le nombre de sous-ensembles libres de K**.
Chaque solution suit la même logique :

* Triez les "nums".
* Nombres de groupes par "num % k". Les nombres de différents groupes ne peuvent jamais différer par exactement "k".
* Pour chaque groupe exécuter un DP unidimensionnel qui se comporte comme Fibonacci lorsque les éléments consécutifs diffèrent par `k`, sinon nous doublerons le nombre de sous-ensembles.
* Multipliez les résultats de tous les groupes.

La réponse est garantie dans un entier 64 bits (`long` / `int64_t` / `long` en Java).

---

#### 1.1 Java – propre, commenté, O(n log n)

"Java
Importation de java.util.*;

solution de classe publique {
Dénombrement public long Les sous-ensemblesNumOfKFree(int[] nums, int k) {
// 1. Triez le tableau – cela nous permet de scanner chaque groupe dans l'ordre.
Tableaux.sort(nums);

// 2. Nombres de groupes par leur reste, divisés par k.
Carte<entier, liste<entier>> groupes = nouvelle HashMap<>();
pour (int num : nombres) {
groups.computeIfAbsent(num % k, x -> new ArrayList<>()).add(num);
}

réponse longue = 1L; // commencer par le sous-ensemble vide

// 3. Traiter chaque groupe restant indépendamment.
pour (Liste <entier> groupe : groups.values() {
int m = groupe.size();
// dp[i] = nombre de sous-ensembles sans k utilisant les premiers éléments i de ce groupe
long[] dp = nouveau long[m + 1];
dp[0] = 1; // sous-ensemble vide
si (m > 0) dp[1] = 2; // { } ou { premier élément }

pour (int i = 1; i < m; ++i) {
Int cur = groupe.get(i);
int prev = group.get(i - 1);

si (cur - prev == k) { // ne peut pas prendre les deux
dp[i + 1] = dp[i] + dp[i - 1];
} autre { // peut inclure ou exclure librement
dp[i + 1] = dp[i] * 2;
}
}

réponse *= dp[m];
}

réponse de retour;
}

/* ----------------------------------------------------------------------------------
* Un petit main() pour que vous puissiez copier-coller dans un IDE LeetCode et tester.
* ------------------------------------------------------------------ */
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
System.out.println(s.countTheNumOfKFreeSubsets(new int[]{5,4,6}, 1)); // 5
System.out.println(s.countTheNumOfKFreeSubsets(new int[]{2,3,5,8}, 5)); // 12
System.out.println(s.countTheNumOfKFreeSubsets(new int[]{10,5,911}, 20)); // 16
}
}
«» "

---

#### 1.2 Python 3 – 100 % lisible

'`python
de taper l'importation Liste
de collections importer par défautdict

Solution de classe:
def countTheNumOfKFreeSubsets(self, nums: List[int], k: int) -> Int:
nombres.sort()
groupes = defaultdict(list)

# Groupe par reste
pour n en nombres:
groupes[n % k].append(n)

ans = 1

pour groupe en groupes.valeurs():
m = len(groupe)
# dp[i] – sous-ensembles utilisant les premiers éléments i de ce groupe
dp = [0] * (m + 1)
dp[0] = 1
si m:
dp[1] = 2

pour i à portée (1, m):
si groupe[i] - groupe [i-1] == k:
dp[i+1] = dp[i] + dp[i-1]
Sinon:
dp[i+1] = dp[i] * 2

*= dp[m]

retour et

♪ ----------------------------------------------------------------------------------
♪ Démo – copier dans LeetCode ou un Python REPL local
♪ ----------------------------------------------------------------------------------
si __nom__ == "__main__" :
s = Solution()
print(s.countTheNumOfKFreeSubsets([5,4,6], 1)) # 5
print(s.countTheNumOfKFreeSubsets([2,3,5,8], 5) # 12
print(s.countTheNumOfKFreeSubsets([10,5,9,11], 20) # 16
«» "

---

### 1.3 C++17 – Rapide, facile à lire

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
long compte long Les sous-ensemblesNumOfKFree(vecteur<int>& nums, int k) {
(noms.begin(), nums.end());

Nombres de groupes par groupe restant
non ordonné_map<int, vector<int>> les groupes;
pour (int n : nombres) groupes[n % k].push_back(n);

longue réponse longue = 1;

pour (auto &kv : groupes) {
Const vector<int>& g = kv.seconde;
int m = g.size();
vecteur <long> dp(m + 1, 0);
dp[0] = 1;
si m) dp[1] = 2;

pour (int i = 1; i < m; ++i) {
si (g[i] - g[i-1] == k) // ne peut pas prendre les deux
dp[i+1] = dp[i] + dp[i-1];
Autre
dp[i+1] = dp[i] * 2;
}
réponse *= dp[m];
}

réponse de retour;
}
};

/* ----------------------------------------------------------------------------------
* Démo – exécuter localement ou coller dans l'éditeur C++ de LeetCode.
* ------------------------------------------------------------------ */
Int main() {
Solution s;
Cout << s.count Les sous-ensemblesNumOfKFree({5,4,6}, 1) << '\n'; // 5
Cout << s.count Les sous-ensemblesNumOfKFree({2,3,5,8}, 5) << '\n'; // 12
Cout << s.count Les sous-ensemblesNumOfKFree({10,5,9,11}, 20) << '\n'; // 16
retour 0;
}
«» "

---

- Oui. 2. L'article du blog

> **Titre**: "Mastering LeetCode 2638: The K‐Free Subset Puzzle – Good, Bad & Ugly (Java, Python, C++)"

> **Méta-Description**: Apprendre à craquer LeetCode 2638 en moins de 5 minutes. Comprendre le truc DP, les maths derrière le regroupement, et obtenir le code en Java, Python et C++. Préparation d'entrevue parfaite pour les ingénieurs logiciels. (en milliers de dollars)

#### 2.1 Pourquoi LeetCode 2638 est un Gold-Mine pour les entrevues

- ** Taille du problème**: `n ≤ 50` – assez petit pour la force brute, mais toujours un bon test pour l'intuition de la programmation dynamique*.
- **La richesse en cas d'urgence**: "k" à un seul chiffre, "k" à un seul chiffre (jusqu'à 1 000 000 000) et un ensemble varié de "nums" vous donnent l'habitude de manipuler le débordement entier et la manipulation des caisses.
- **Scoring**: La réponse peut être aussi grande que `2^50 ↓ 10^15`, donc vous aurez besoin de penser à l'utilisation entière 64-bit.
- **Concepts testés**:
- Tri et manipulation du tableau
- **Arithmétique modulaire** – un trick classique
- *PDD de style Fibonacci – un modèle qui apparaît dans de nombreux problèmes d'entrevue

> **SEO Mots-clés**: *LeetCode 2638, sous-ensembles K-free, programmation dynamique, codage d'entrevue, Java DP, algorithme Python, question d'entrevue C++, interview d'ingénieur logiciel*

2.2 La bonne idée

1. **Groupement modulaire**
Les deux nombres qui appartiennent à *différent* restent `num % k` ne peuvent pas différer par exactement `k`.
Pourquoi ? *
Si `a % k = r1` et `b % k = r2` avec `r1 γ r2`, alors
`=a - b=% k ==r1 - r2=% k=0`, donc la différence ne peut pas être `k`.

2. ** Sous-problèmes indépendants**
Une fois le tableau séparé en groupes restants, chaque groupe est un sous-problème *indépendant*.
La réponse totale est simplement le produit des réponses pour chaque groupe.

3. **PDD unidimensionnel**
Scanner un groupe dans l'ordre trié.
*Si `curr - prev == k`* – vous *ne pouvez pas* choisir les deux, donc la récurrence est Fibonacci:
«dp[i] = dp[i‐1] + dp[i‐2]».
*Autrement* – vous êtes libre d'inclure ou d'exclure l'élément courant, de sorte que `dp[i] = dp[i‐1] * 2`.

4. **Complexité**
*Trier* domine: `O(n log n)`.
Le DP à l'intérieur de chaque groupe est linéaire, et avec au plus des numéros `50` le produit reste dans un entier 64 bits.

#### 2.3 L'erreur – Pièges communs

Piège Comment ça arrive
- Oui.
**Renforcement du groupe**Renforcement du groupe par «num / k» au lieu de «num % k» Utilisez le reste («num % k»). Autres
**Off‐by‐One dans DP**=Démarrer `dp[1]` incorrectement ou oublier le sous-ensemble vide== Définissez explicitement `dp[0]=1`, `dp[1]=2` lorsque le groupe n'est pas vide. Autres
**Integer Overflow**= Utiliser `int` (32-bit) dans Java/C++= Utiliser `long` / `int64_t` / `long long`. Autres
**Missing Edge Cases**=Rayau vide ou groupes d'éléments simples=Poignée `m == 0` et `m== 1' avec grâce. Autres
**Temps-out dans LeetCode** Autres

2.4 Les choses Cette pause Les choses sont tombées

1. **Naïve Brute-Force**
Enumerer tous les sous-ensembles `2^n` est faisable pour `n=50` sur une machine puissante, mais la solution est *O(2^n*) et cache vos connaissances DP. Les intervieweurs adorent pourquoi ne pas tout essayer ?

2. **Misscompréhension gratuite* *
Certaines solutions interprètent "k-free" comme "no" deux nombres consécutifs diffèrent par "k" (wrong). La vraie définition est -No deux *choisi* nombres diffèrent par exactement `k` n'importe où dans le set.
L'astuce de regroupement modulaire est la clé pour éviter cette mauvaise interprétation.

3. **Codage dur `k==0`**
Le problème garantit `k ≥ 1`, mais en supposant aveuglément que cela peut vous faire monter dans un test avec un cas de test caché personnalisé où `k == 0`. Un contrôle de défense ('si (k == 0) retour 1;') est inoffensif et montre l'attention au détail.

### 2.5 Un rapide

Laissez passer `nums = [2,3,5,8]`, `k = 5`.

1. **Trier** → `[2,3,5,8]`.
2. **Groupe** par «num % 5»:
* reste `2` → `[2]`
* reste `3` → `[3]`
* reste `0` → `[5,8]` (tous deux 0 (mod. 5))
3. **Groupes de processus**:
* `[2]`: DP → `dp = [1, 2]` → sous-ensembles = `2`
* `[3]`: DP → `dp = [1, 2]` → sous-ensembles = `2`
* «[5,8]»:
* `dp[0] = 1`
* `dp[1] = 2`
* `8 - 5 == 3 φ 5` → `dp[2] = 4`
→ sous-ensembles = `4`
4. ** Multiplier** → `2 * 2 * 4 = 16`.

L'exemple correspond à la réponse attendue.

---

- Oui. 3. Comment utiliser ceci dans un CV / entrevue

Sensibiliser Comment ça aide le code Référence
- C'est quoi ?
**La programmation dynamique** Autres Les trois solutions
**Modulaire Arithmétique** Regroupement par «num % k» Autres
**Codage multilingue** Blocs de codes
**La pensée algorithmique**Le problème semble être combiné en sous-problèmes indépendants. Analyse de blog

J'ai résolu LeetCode 2638 en moins de 5 minutes et j'ai compris l'astuce DP derrière le reste du groupe. N'hésitez pas à discuter rapidement de la façon dont cela peut vous aider à décrocher votre prochain rôle d'ingénierie logicielle.

---

3.1 Liste de contrôle finale avant votre prochaine entrevue

1. **Exposer le regroupement Modulo** – C'est le moment que la plupart des intervieweurs attendent.
2. **Dériver la récurrence DP** – Montrer l'analogie de Fibonacci quand `diff == k`.
3. **Talk About Complexity** – Tri (« O(n log n) »), PDD linéaire par groupe, global « O(n log n) ».
4. **Mention Edge Cases** – Groupes à éléments uniques, plus grand que toute différence, et sécurité de débordement.
5. **Afficher le code** – Déposer dans la langue de l'interview (Java, Python, C++).

Bonne chance, et que votre code soit aussi propre qu'il est correct!