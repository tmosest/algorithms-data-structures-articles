---
titre: LeetCode 474. Ones et Zéroes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
LeetCode 474 – *Ones and Zeroes*
### Les bons, les mauvais et les méchants – Un entretien d'emploi Guide prêt

> **Mots clés**: LeetCode 474, Ones and Zeroes, programmation dynamique, knapsack, entretien d'emploi, ingénieur logiciel, algorithme, entretien de codage, défi de codage, data-structures, DP 2-dimensional, interview prep, CV, Java, Python, C++

---

#### 1-

Vous êtes donné un tableau de chaînes binaires `strs` et deux entiers `m` et `n`.
Trouvez la taille du sous-ensemble le plus important de " strs " de telle sorte que le sous-ensemble contient **au plus `m` zéros** et **au plus `n` ceux**.

«» "
Entrée :
strs = ["10", "0001", "111001", "1", "0"]
m = 5
n = 3

Produit :
4 // {"10", "0001", "1", "0"} est le sous-ensemble optimal
«» "

Contraintes
- C'est quoi ?
1 ≤ longueur des chaînes ≤ 600
1 ≤ strs[i].longueur ≤ 100
Les strs[i] se composent uniquement de '0' et '1'
1 ≤ m,n ≤ 100

---

C'est vrai. Pourquoi ce problème est-il à l'origine de votre portefeuille d'entrevues

Caractéristiques Pourquoi ça compte
C'est-à-dire
**Classique 0/1 Knapsack** de nombreuses entreprises demandent des variations du problème de knapsack. La preuve que vous pouvez l'adapter à une capacité bidimensionnelle montre une compréhension profonde du PDD. Autres
**La réduction de l'espace de l'État du PD**=De `O(L * m * n)` à `O(m * n)` par itération à l'envers. Ce compromis est un modèle favori dans le codage des entrevues. Autres
Autres **Manipulation d'un boîtier**= Nécessite le comptage de zéros/uns, la manipulation de grandes entrées et la garantie de ne pas déborder – tous bons tests de code propre. Autres
**Multi-Language Mastery**= Montrant le même algorithme en Java, Python et C++ démontre la pensée de l'algorithme langage-agnostique – un énorme plus dans les équipes multi-sacrées. Autres

> **SEO Conseil:** Termes de recherche comme la solution 474 de LeetCode, la programmation dynamique de Ones et Zeroes, et la question d'interview de Knapsack , sont des mots-clés chauds que les recruteurs utilisent lors de la numérisation des blogs candidats.

---

####3-

Considérez le problème comme un sac à dos bidimensionnel** :

- **Dimensions de poids :** nombre de zéros ('0') et nombre de zéros (`1').
- **Capacité :** `m` zéros et `n` ceux.
- **Valeur de l'article :** chaque chaîne contribue `1` à la taille totale du sous-ensemble.

Vous pouvez inclure ou exclure chaque chaîne exactement une fois – la logique classique 0/1 knapsack.

**Truse clé**: Itérer **backwards** lors de la mise à jour de la table DP pour éviter de réutiliser la même chaîne plusieurs fois.

---

Algorithme (Bottom-Up DP)

Texte
dp[z][o] = taille maximale du sous-ensemble en utilisant au plus z zéros et o ceux

pour chaque chaîne s en strs:
z0 = nombre de '0' dans s
o1 = nombre de '1' en s
pour z de m à z0:
o de n à o1:
dp[z][o] = max(dp[z][o], dp[z - z0][o - o1] +1)

retour dp[m][n]
«» "

**Complexité* *

- **Heure:** `O(L * m * n)` où `L = strs.longueur`.
- **Espace:** `O(m * n)` (2-D tableau).

Les boucles arrière assurent l'utilisation de chaque chaîne au plus une fois, faisant du DP 3-D un DP 2-D.

---

C'est vrai. Code (Java, Python, C++)

##### 5.1 Java

"Java
// LeetCode 474 – Ones et Zéroes (Java)
solution de classe publique {
public int findMaxForm(String[] strs, int m, int n) {
int[] dp = nouveau int[m + 1] n + 1;

pour (String s : strs) {
int[] cnt = countZerosOnes(s);
= cnt[0];
int = cnt[1];

// L'itération vers l'arrière assure un comportement 0/1
pour (int z = m; z >= zéros; z--) {
pour (int o = n; o >= un; o--) {
dp[z][o] = Math.max(dp[z][o], dp[z - zéros][o - ceux] + 1);
}
}
}
retour dp[m][n];
}

Int privé[] Nombre ZerosOnes(String s) {
int[] c = nouveau int[2];
pour (int i = 0; i < s.longueur(); i++) {
c[s.charAt(i) - '0']++; // '0' -> index 0, '1' -> index 1
}
retour c;
}
}
«» "

5.2 Python

'`python
# LeetCode 474 – Ones et Zeroes (Python 3)
Solution de classe:
def findMaxForm(self, strs: List[str], m: int, n: int) -> Int:
dp = [[0] * (n + 1) pour _ dans la plage (m + 1)]

pour s en strs:
zéros, un = s.count('0'), s.count('1')
pour z (m, zéros - 1, -1):
o dans l'intervalle(n, un - 1, -1):
dp[z][o] = max(dp[z][o], dp[z - zéros][o - uns] + 1)

retour dp[m][n]
«» "

C++

'`cpp
// LeetCode 474 – Ones et zéros (C++)
solution de classe {
public:
int findMaxForm(vector<string>& strs, int m, int n) {
vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));

pour (const : strs) {
= 0;
pour (charc : s) {
si (c == '0') zéros++; sinon ceux++;
}

pour (int z = m; z >= zéros; --z) {
pour (int o = n; o >= ceux; --o) {
dp[z][o] = max(dp[z][o], dp[z - zéros][o - ceux] + 1);
}
}
}
retour dp[m][n];
}
};
«» "

---

#### 6--Cas de bord et pièges communs

Ce qui ne va pas
C'est ce que j'ai dit.
En utilisant `z >= zéros` mais en accédant `dp[z - zéros]` peut aller négativement en boucle de `m` vers le bas à `zeros`, inclusivement
**Les plus grandes chaînes d'entrée**= Comptage des zéros/ones via `s.count('0')` dans Python est O(longueur)===Temps total limité par des contraintes==
**Déploiement entier**= Pas de problème en Java/Python; C++ utilise `int` (fits 32-bit)=Assurer les capacités `m, n <= 100` → safe
**Chiffre d'empty**= `count('0')` et `count('1')` sont 0 → toujours valides== Le code le gère naturellement==
**Délai**= Les boucles imbriquées `L*m*n` peuvent toucher 6 opérations e7 au pire== Acceptable pour 1 limite dans la plupart des juges; envisager la taille si `m` ou `n` small==

---

### 7--Des conseils d'entrevue

1. **Exposer l'analogie 2-D DP**: C'est un sac qui peut contenir X zéros et Y. (en milliers de dollars)
2. **Montrer l'itération vers l'arrière**: Ceci garantit que chaque chaîne est utilisée une fois. (en milliers de dollars)
3. **Discuse la complexité**: temps O(Lmn), espace O(mn); avec `m,n=100` il est très bien. (en milliers de dollars)
4. ** Optimisations de la concentration**: Si nous précalculons les zéros/ones compte, nous évitons de re-scanner chaque chaîne. (en milliers de dollars)
5. **Lisibilité des feux**: Les noms de variables (`zeros`, `ones`) et les méthodes d'aide aident à maintenir les données. (en milliers de dollars)

---

#### 8=" Bonus – Mémoisation du haut de la piste (facultative)

"Java
// Version mémolisée Java
public int findMaxFormMemo(String[] strs, int m, int n) {
int[][] mémo = nouveau int[m+1][n+1];
pour (int[] ligne : mémo) Arrays.fill(row, -1);
retourner dfs(strs, 0, m, n, mémo);
}

int dfs(String[] strs, int idx, int zéros, int, int [] mémo) {
si (idx == strs.longueur) retourne 0;
si [memo[zeros][ones] != -1) retourner le mémo[zéros][ones];

int z = strs[idx].chars().filter(c -> c == '0').count();
int o = strs[idx].chars().filter(c -> c == '1').count();

int exclu = dfs(strs, idx+1, zéros, un, mémo);
= 0;
si (zéros >= z && uns >= o)
inclure = 1 + dfs(strs, idx+1, zéros - z, ceux - o, mémo);

retourner mémo[zeros][ones] = Math.max(exclusion, inclure);
}
«» "

---

#### 9- Loin

- **Problème**: 2-D 0/1 knapsack (zeros & uns) → classique DP.
- **Solution**: PDD ascendant avec boucles arrière → temps `O(L*m*n)`, espace `O(m*n)`.
- **Pourquoi ça compte**: Démontre la programmation dynamique, les compromis espace/temps et le codage propre en Java/Python/C++.
- **Influence de l'embauche**: Parlez de l'intuition du knapsack, de la complexité, des cas de pointe et de la pensée linguistique pour impressionner les gestionnaires d'embauche.

> **SEO CTA:** *Si vous voulez maîtriser LeetCode 474 et atterrir votre rôle d'ingénierie logicielle de rêve, plonger dans ce post, pratiquer les extraits de code, et partager vos propres variations sur GitHub. Suivez pour en savoir plus sur les PDD, la préparation d'entrevues et les conseils de croissance de carrière! *

Bon codage et bonne chance dans votre prochaine interview! C'est ce qu'il a dit