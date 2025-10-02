---
titre: LeetCode 3472. Palindromique le plus long Subséquences après au plus K opérations - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# LeetCode 3472 – Subséquence palindromique la plus longue après les opérations à la majorité K
> **Interview-Ready Solution (Java / Python / C++) + In-Depth Blog Post**

---

Table des matières
1. [Récapitulation des problèmes] (#récapitulation des problèmes)
2. [Pourquoi ce problème compte] (#pourquoi-ce-problème-matières)
3. [Intuition & Idée de haut niveau] (#Intuition)
4. [solution de programmation dynamique] (#dp-solution)
4.1 État et transition
4.2. Mise en œuvre du bas vers le haut (O(n2·k))
5. [Analyse de la complexité] (#complexité)
6. [Le bon, le mauvais, le mauvais]
7. [Code complet (Java / Python / C++)](#code)
8. [SEO checklist & Comment cela aide votre recherche d'emploi](#seo)
9. [Conclusion et lecture supplémentaire](#conclusion)

---

- Oui. 1. Récapitulation du problème <un nom="problème-recap"></a>

**LeetCode #3472 – Subséquence palindromique la plus longue après la plupart des opérations K**

On vous donne une chaîne `s` de lettres anglaises minuscules (`1 ≤ s.longueur ≤ 200`) et un entier `k` (`1 ≤ k ≤ 200`).
Dans **une** opération vous pouvez remplacer n'importe quel caractère par sa prochaine ** ou** lettre précédente dans l'alphabet (envelopper autour: après `z` vient `a`, avant `a` vient `z`).
Exemple: `'a' → 'b'` ou `'a' → 'z'`.

**Tâche**
Retourner la longueur maximale possible d'une séquence palindromique de `s` après avoir effectué ** au maximum** des opérations `k`.

> **Exemples**
> *Input*: `s = "abced"`, «k = 2»
> * Sortie*: `3` (modifier `"accec"` → subséquence `"ccc"`)

> *Input*: `s = "aaazzz"`, `k = 4`
> * Sortie*: `6` (modifier `"zaaaaz"` → chaîne entière est palindrome)

---

- Oui. 2. Pourquoi ce problème est-il important?

- **String & DP Mastery** – Combine classique *Longest Palindromic Subsequence (LPS)* avec une dimension extra *resource-bounded transformation*.
- **Interview Signal** – Montre que vous pouvez:
- Convertissez une transformation de chaîne en un PDD *optimal-matching*.
- Gérer une dimension *coût* supplémentaire (les opérations `k`) sans faire exploser l'espace d'état.
- Optimiser la pré-computation («coût(a, b)»).
- **Analogie du monde réel** – Considérez-le comme un montage d'une séquence d'ADN dans un budget de mutation limité pour maximiser la symétrie – un modèle qui apparaît dans la bioinformatique et le traitement de texte.

---

- Oui. 3. Intuition et idées de haut niveau <un nom></a>

1. **Problème de base** – Pour un `k = 0` fixe, la réponse est le LPS classique: `dp[i][j]` = longueur du palindrome le plus long dans `s[i...j]`.
2. **Extra Dimension** – Autoriser les opérations `k`. Nous devons savoir *combien d'opérations restent* tout en explorant les sous-chaînes.
3. **Transition**
- Si `s[i] == s[j]` → nous pouvons garder les deux extrémités → `dp[i][j][k] = 2 + dp[i+1][j-1][k]`.
- Sinon, nous pouvons soit **skip** un bout ou **change** les deux bouts pour se correspondre.
Modification des coûts "coût(s) [i], [j]".
Si `k >= coût`, nous pouvons prendre `2 + dp[i+1][j-1][k - coût]`.
4. **Bottom-Up** – Durées d'itération de 1 à `n`, remplir les tableaux DP. La complexité reste gérable parce que «n ≤ 200», «k ≤ 200».

---

- Oui. 4. Solution de programmation dynamique <un nom="dp-solution"></a>

### 4.1. État et transition

- `dp[i][j][t]` – *longueur maximale* d'un palindrome qui peut être formé à partir de la sous-chaîne `s[i...j]` en utilisant tout au plus `t` opérations.
- **Base**
- `dp[i][i][t] = 1` (un seul caractère est un palindrome de longueur 1).
- `dp[i][j][t] = 0` pour `i > j` (sous-chaîne vide).
- **Transition**
«» "
si s[i] == [j]:
dp[i][j][t] = 2 + dp[i+1][j-1][t]
Sinon:
dp[i][j][t] = max(
dp[i+1][j][t], // skip gauche
dp[i][j-1][t], // sauter à droite
(t >= coût(s[i],s[j]) ? 2 + dp[i+1][j-1][t - coût] : 0
)
«» "

- **Fonction de coût**
«» "
Coût(a,b) = min (a-b, 26 -a-b)
«» "
parce qu'avancer ou reculer autour de l'alphabet donne le même nombre minimal d'opérations.

4.2. Mise en œuvre du bas vers le haut (O(n2·k))

Nous précalculons la matrice de coûts pour toutes les paires de lettres 26×26 afin d'éviter la recomputation.

Code Pseudo:

«» "
pour len = 1 .. n:
pour i = 0 .. n-len:
j = i + len - 1
pour t = 0 .. k:
Si i == j:
dp[i][j][t] = 1
Sinon si s[i] == [j]:
dp[i][j][t] = 2 + dp[i+1][j-1][t]
Sinon:
as = max(dp[i+1][j][t], dp[i][j-1][t])
c = coût[s[i]][s[j]]
si t >= c:
ans = max(ans, 2 + dp[i+1][j-1][t - c])
dp[i][j][t] = ans
«» "

Réponse: `dp[0][n-1][k]`.

---

- Oui. 5. Analyse de complexité <un nom="complexité"></a>

Formule métrique Résultat
C'est quoi, ça ?
**Temps**="O(n2 · k)"=" ≤ `2002 · 200`=" 8 millions d'opérations – s'adapte facilement à 1 s.="
**L'espace**=O(n2 · k)==8 millions d'entiers=32 Mo (Java int) – acceptable. Autres
**Optimisation**= Utilisez deux couches 2-D (`prev`, `curr`) pour réduire la mémoire à `O(n·k)` si désiré. Autres

---

- Oui. 6. Le Bon, le Mauvais, le Méchant <un nom></a>

Aspect du bien
- C'est quoi ?
**Idée PD**= Séparation nette des sous-chaînes et du budget de fonctionnement. Fonctionne pour n'importe quel `k`. Autres
**La matrice de coûts accélère les boucles internes. Si on l'oublie, le coût à l'intérieur de 3 boucles imbriquées devient un goulot d'étranglement. Autres
**L'empreinte de la mémoire**L'empreinte de 32 Mo est bonne pour les limites de LeetCode. Le tableau 3-D est lourd; les intervieweurs peuvent vous demander de *streamline* il. Autres
**Récursif (Top-Down)**= Code élégant; moins de boucles. La profondeur de la pile peut souffler (`n` jusqu`à 200) → problèmes de limite de récursion. Autres
Réutiliser les résultats. Autres
**Pratique**= Indices de sous-chaîne + budget → naturel pour les intervieweurs. Certains candidats sur-optimisent tôt et perdent de la clarté. Autres
Une solution naïve qui tente chaque ensemble d'opérations (sous-ensembles « k » ) est exponentielle – *ne PAS* essayer. Autres

** À emporter* *
- Oui. Utilisez le PDD *bottom-up comme solution d'accès.
- Oui. Si vous êtes pressé pour l'espace, ne gardez que deux couches.
- Évitez la mémoisation récursive à moins que vous soyez sûr que votre langage gère bien la récursion profonde.

---

- Oui. 7. Code complet (Java / Python / C++) <un nom (code)></a>

- Oui. Java (Bas-Up optimisé)

"Java
importation java.io.*;

solution de classe publique {
// Coût avant calcul entre les 26 lettres
int final statique privé[] COST = nouveau int[26][26];

statique {
pour (int a = 0; a < 26; a++) {
pour (int b = 0; b < 26; b++) {
int diff = Math.abs(a - b);
COST[a][b] = Math.min(diff, 26 - diff);
}
}
}

public int le plus longSujet(String s, int k) {
int n = s.longueur();
char[] ch = s.toCharArray();

// dp[i][j][t] (i <= j)
int[][] dp = nouvelle int[n][n][k + 1];

pour (int len = 1; len <= n; len++) {
pour (int i = 0; i + len - 1 < n; i++) {
j = i + len - 1;
pour (int t = 0; t <= k; t++) {
si i) j) {
dp[i][j][t] = 1;
} sinon si {
dp[i][j][t] = 2 + dp[i + 1][j - 1][t];
} autre {
int best = Math.max(dp[i + 1][j][t], dp[i][j - 1][t];
coût int = COST[ch[i] - 'a'][ch[j] - 'a'];
si (t >= coût) {
best = Math.max(meilleur, 2 + dp[i + 1][j - 1][t - coût]);
}
dp[i][j][t] = meilleur;
}
}
}
}
retour dp[0][n - 1][k];
}

- Oui. Pour LeetCode --------- */
public statique vide main(String[] args) lance Exception {
Solution sol = nouvelle solution();
Système.out.println(sol.longestSubséquence("abced", 2)); // 3
Système.out.println(sol.longestSubséquence("aaazzz", 4)); // 6
}
}
«» "

> **Astuce** – Remplacer `int[][]] dp` par `int[][] prev = nouvelle int[n][k+1]` et `int[][]] curr` pour réduire de moitié l'utilisation de la mémoire.

---

7.2. Python (Bottom-Up)

'`python
Solution de classe:
def leastSubséquence(s: str, k: int) -> Int:
n = len(s)
# matrice de coûts 26x26
coût = [[0]*26 pour _ dans l'intervalle(26)]
pour une gamme(26):
pour b dans la fourchette(26):
diff = abs(a - b)
coût[a][b] = min(diff, 26 - diff)

# dp[i][j][t] – Liste 3-D
dp = [[[0]*(k+1) pour _ dans la plage(n)] pour _ dans la plage(n)]

pour la longueur de portée(1, n+1):
pour i dans la plage (n-longueur+1):
j = i + longueur - 1
pour t dans la plage(k+1):
Si i == j:
dp[i][j][t] = 1
C'est vrai. [j]:
dp[i][j][t] = 2 + dp[i+1][j-1][t]
Sinon:
best = max(dp[i+1][j][t], dp[i][j-1][t])
c = coût[ord(s[i]) - 97][ord(s[j]) - 97]
si t >= c:
best = max(meilleur, 2 + dp[i+1][j-1][t-c])
dp[i][j][t] = meilleur
retour dp[0][n-1][k]
«» "

** Version Python la plus rapide** – Remplacer le tableau 3-D par deux calques 2-D (dépliant DP) et pré-calculer `cost` en tant que liste 26×26 pour la mémoire O(n·k).

---

7.3. C++ (Bottom-Up)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int le plus longSujet(chaîne s, int k) {
int n = s.size();
// Matrice de coûts précalculée
coût int[26][26];
pour (int a = 0; a < 26; ++a)
pour (int b = 0; b < 26; ++b) {
int diff = abs(a - b);
coût[a][b] = min(diff, 26 - diff);
}

// dp[i][j][t] – vecteur 3-D
vecteur<vecteur<vecteur<int>>> dp(n,
vecteur<vector<int>>(n, vector<int>(k+1, 0));

pour (int len = 1; len <= n; ++ len) {
pour (int i = 0; i + len - 1 < n; ++i) {
j = i + len - 1;
pour (int t = 0; t <= k; ++t) {
si i) j) {
dp[i][j][t] = 1;
} sinon si (s[i] == s[j]) {
dp[i][j][t] = 2 + dp[i+1][j-1][t];
} autre {
int best = max(dp[i+1][j][t], dp[i][j-1][t];
int c = coût[s[i]-'a'][s[j]-'a'];
si (t >= c)
best = max(meilleur, 2 + dp[i+1][j-1][t-c];
dp[i][j][t] = meilleur;
}
}
}
}
retour dp[0][n-1][k];
}
};
«» "

---

## 7.4. (facultatif) Mémoire optimisée C++ (deux calques)

'`cpp
// Ne conserver que la longueur du courant et les tranches antérieures
le nom et l'adresse de l'autorité compétente;
// Remplir cur en utilisant prev (dp[i+1][j-1] devient prev[j-1] après le déplacement)
// Swap cur/prev à chaque itération de longueur
«» "

---

- Oui. 7. Le bon, le mauvais, l'horrible <un nom></a>

**Catégorie ********************
- C'est quoi ?
**Readability**= Effacer le DP 3-D avec les commentaires== Le nom de tableau 3-D `dp` est verbeux mais auto-documentant=== Memorisation profonde et récursive sans cas de base → confusion===
**Performance**.O(n2·k) – 8 M ops.
**Maintenabilité**=Matrice de coûts précalculée== Nécessite une indexation soigneuse (`'a' → 0`)== Formules codées dur à l'intérieur des boucles, risque de hors-par-un==
**L'espace est clair. Autres

---

- Oui. 7. Code complet (Java / Python / C++) <un nom (code)></a>

- Oui. Java (LeetCode-Ready)

"Java
solution de classe publique {
int final statique privé[] COST = nouveau int[26][26];

statique {
pour (int a = 0; a < 26; a++)
pour (int b = 0; b < 26; b++) {
int diff = Math.abs(a - b);
COST[a][b] = Math.min(diff, 26 - diff);
}
}

public int le plus longSujet(String s, int k) {
int n = s.longueur();
char[] ch = s.toCharArray();

int[][] dp = nouvelle int[n][n][k + 1];

pour (int len = 1; len <= n; len++) {
pour (int i = 0; i + len - 1 < n; i++) {
j = i + len - 1;
pour (int t = 0; t <= k; t++) {
si i) j) {
dp[i][j][t] = 1;
} sinon si {
dp[i][j][t] = 2 + dp[i + 1][j - 1][t];
} autre {
int best = Math.max(dp[i + 1][j][t], dp[i][j - 1][t];
coût int = COST[ch[i] - 'a'][ch[j] - 'a'];
si (t >= coût)
best = Math.max(meilleur, 2 + dp[i + 1][j - 1][t - coût]);
dp[i][j][t] = meilleur;
}
}
}
}
retour dp[0][n - 1][k];
}
}
«» "

---

7.2. Python (LeetCode-Ready)

'`python
Solution de classe:
def leastSubséquence(s: str, k: int) -> Int:
n = len(s)
# Matrice de coûts précalculée 26x26
coût = [[0]*26 pour _ dans l'intervalle(26)]
pour une gamme(26):
pour b dans la fourchette(26):
diff = abs(a-b)
coût[a][b] = min(diff, 26-diff)

dp = [[[0]*(k+1) pour _ dans la plage(n)] pour _ dans la plage(n)]
pour la longueur de portée(1, n+1):
pour i dans la plage (n-longueur+1):
j = i + longueur - 1
pour t dans la plage(k+1):
Si i == j:
dp[i][j][t] = 1
C'est vrai. [j]:
dp[i][j][t] = 2 + dp[i+1][j-1][t]
Sinon:
best = max(dp[i+1][j][t], dp[i][j-1][t])
c = coût[ord(s[i])-97][ord(s[j])-97]
si t >= c:
best = max(meilleur, 2 + dp[i+1][j-1][t-c])
dp[i][j][t] = meilleur
retour dp[0][n-1][k]
«» "

---

### 7.3. C++ (LeetCode-Ready)

'`cpp
solution de classe {
public:
int le plus longSujet(chaîne s, int k) {
int n = s.size();
coût int[26][26];
pour (int a=0; a<26; ++a)
pour (int b=0; b<26; ++b) {
int diff = abs(a-b);
coût[a][b] = min(diff, 26-diff);
}

vector<vector<vector<int>>> dp(n, vector<vector<int>>(n, vector<int>(k+1,0));

pour (int len=1; len<=n; ++len) {
pour (int i=0; i+len-1<n; ++i) {
int j=i+len-1;
pour (int t=0; t<=k; ++t) {
si i==j) dp[i][j][t]=1;
si (s[i]==s[j]) dp[i][j][t]=2+dp[i+1][j-1][t];
autres {
int best=max(dp[i+1][j][t], dp[i][j-1][t];
c=coût[s[i]-'a'][s[j]-'a'];
si (t>=c) best=max(best, 2+dp[i+1][j-1][t-c];
dp[i][j][t]=meilleur;
}
}
}
}
retour dp[0][n-1][k];
}
};
«» "

---

- Oui. 8. Conclusion

- La solution *bottom-up 3-D DP* est l'approche **optimale** du problème LeetCode #2414.
- Précalculer la matrice des coûts de l'alphabet; garder les boucles serrées.
- Oui. Si l'espace est une préoccupation, rouler le DP en deux couches.
- Évitez les solutions récursives qui ignorent la mémoisation – elles sont **ugly** et exponentielles.

** Bon codage !**

---


---

**Méta-information pour LeetCodes page HTML (facultatif)* *

html
- Oui. DOCTYPE html>
<html>
<tête>
<meta charset="UTF-8">
<title>LeetCode 2414 – Subséquence la plus longue</title>
<meta name="description" content="Implémenter la plus longue sous-séquence palindrome-comme avec des changements d'alphabet limités.">
</tête>
<corps>
<h1>2414. Subséquence la plus longue</h1>
<p>Java, Python, solutions C++ basées sur le DP 3-D avec coût de changement d'alphabet précalculé.</p>
</corps>
</html>
«» "

---


**Profitez de la résolution, et bonne chance dans votre interview! * *