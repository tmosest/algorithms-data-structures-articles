---
Titre: LeetCode 1531. Compression des chaînes II -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1531 – Compression de chaîne II
**LeetCode Hard – DP, Encodage Run‐Length, Supprimer k Chars* *

---

C'est pas vrai. Le problème

On vous donne une chaîne inférieure `s` (`1 ≤=1 ≤=100`) et un entier `k` (`0 ≤ k ≤==").
Vous pouvez supprimer *au plus* les caractères `k` de `s`.
Après les suppressions vous exécutez **run-long encodage (RLE)**:

* Remplacer toute exécution du même caractère qui apparaît **2 fois ou plus** par
«char + compte».
* Les caractères simples restent tels qu'ils sont – pas de -1-- est ajouté.

Objectif : ** Minimiser la longueur de la chaîne encodée**.

> Exemple
> `s = "aaabccd", k = 2`
> Supprimer `b` et `d` → `aaaccc` → RLE → `"a3c3"` → longueur `4`.

Le problème est difficile car vous devez décider *qui* `k` caractères à supprimer et *où* à diviser la chaîne en exécut.

---

- Oui. Pourquoi DP est le bon outil

Si nous regardons la chaîne de gauche à droite, la décision à la position `i` dépend seulement de

* combien de suppressions nous avons encore,
* où le **suivant même caractère** après `i` est.

Par conséquent, l'État peut être représenté par
«(index i, restant k)» → *longueur encodée minimale pour le suffixe `s[i:]`*.

Il s'agit d'un problème classique de DP en 2 dimensions que nous pouvons résoudre par

* **Top-Down (mémoisation)** – récursion avec cache.
* **Bottom-Up (tabulation)** – PDD itérative.

Les deux solutions fonctionnent dans le temps `O(k · n2)` (le pire cas `n = 100`) et la mémoire `O(k · n)`, qui est assez rapide pour les contraintes.

---

- Oui. Aperçu des clés – Suivant Même personnage

Pendant le PDD nous devons savoir, pour chaque position `i`, le prochain index `j > i` où `s[j] == s[i]`.
Au lieu d'aller de l'avant chaque fois (qui ferait le DP `O(n3)`), nous construisons un tableau `next`:

«» "
next[i] = indice de la prochaine occurrence de s[i] après i (ou -1 si aucun)
«» "

Nous le construisons en **O(n)** en scannant la chaîne de droite à gauche et en conservant la dernière position pour chaque lettre.

Avec `next`, nous pouvons énumérer efficacement tous les 'Runs' possibles qui commencent par `i`.

---

- Oui. Comment fonctionne le PDD

«» "
dp[i][rem] = longueur minimale encodée de s[i:] en utilisant au plus des suppressions de rem
«» "

Transitions

1. **Supprimer `s[i]`**
`dp[i][rem] → dp[i+1][rem-1]` (si rem > 0)

2. **Garder une course à partir de 'i'**
Traversez toutes les occurrences ultérieures du même caractère (`cur = i, next[i], next[i], ...`).
Pour chaque paramètre d'exécution possible `cur`:

* `lenWindow = cur - i + 1` (caractères considérés)
* `occurrences = nombre de caractères conservés dans cette exécution "
(Les «occurrences» augmentent de 1 chaque fois que nous visitons un index de même lettre)
* `déplacements = lenWindow - occurrences` (caractères que nous supprimons dans la fenêtre)
* Si `suppressions > rem` → pause (plus de suppressions)
* `coût = 1` (pour la lettre elle-même)
plus `+1` chaque fois que `occurrences` atteint 2, 10, 100 (les chiffres grandissent)
* `dp[i][rem] = min(dp[i][rem], coût + dp[cur+1][remplacement] "

Le cas de base: `dp[n][*] = 0` (suffixe vide).
Si la longueur suffixe ≤ `rem`, nous pouvons supprimer tout → longueur `0`.

La réponse est «dp[0][k]».

---

Détails de la mise en oeuvre

Voici les solutions **ready‐to‐copy** dans **Java, Python et C++**.
Les trois utilisent le même algorithme et le même tableau `next` pré-computation.

> **Conseil:**
> - Pour Java et C++, utilisez un tableau de `int` initialisé à `-1` pour mémoriser.
> - Pour Python utiliser `functools.lru_cache` ou un dictionnaire explicite.

---

Java – Haut de la page Mémotisation descendante

"Java
Importer java.util. Les tableaux;

solution de classe publique {
// helper pour construire le tableau "prochain même caractère"
privé int[] buildSuivant(char[] s) {
int n = longueur s.
int[] suivante = nouvelle int[n];
int[] last = nouveau int[26];
les tableaux.fill(dernier, -1);
pour (int i = n - 1; i >= 0; i--) {
int idx = s[i] - 'a';
suivant[i] = dernier[idx];
last[idx] = i;
}
retour suivant;
}

Int public getLengthOfOptimalCompression(String s, int k) {
si (k >= s.longueur()) retourne 0;
int[] next = buildNext(s.toCharArray());
int n = s.longueur();
int[][] mémo = nouveau int[k + 1][n + 1];
pour (int[] ligne : mémo) Arrays.fill(row, -1);
retourner dfs(0, k, suivant, mémo);
}

int dfs(int i, int rem, int[] suivant, int[][] mémo) {
si (memo[rem][i] != -1) retourner le mémo[rem] [i];
int n = longueur suivante;
si (n - i <= rem) retourner mémo[rem] [i] = 0; // supprimer le reste

int best = entier.MAX_VALUE;

// Option 1: supprimer le char actuel
if (rem > 0) best = Math.min(best, dfs(i + 1, rem - 1, next, mémo));

// Option 2: maintenir une course à partir de i
icc = 0;
coût int = 1; // pour la lettre elle-même
pour (int cur = i; cur != -1; cur = next[cur]) {
occ++;
effacements int = (cur - i + 1) - oct; // à l'intérieur de la fenêtre
si (suppression > rem) pause; // ne peut pas se permettre plus de suppressions

// augmenter le coût lorsque les chiffres grandissent
si (occ) coût++;

best = Math.min(best, cost + dfs(cur + 1, rem - suppressions, next, mémo));
}

retourner mémo[rem] [i] = meilleur;
}
}
«» "

---

Python – DP récursif avec `lru_cache "

'`python
à partir de functools importer lru_cache
de taper l'importation Liste

Solution de classe:
def build_next(self, s: str) -> Liste[int]:
n = len(s)
nxt = [-1] * n
dernier = [-1] * 26
pour i dans la fourchette(n - 1, -1, -1):
idx = ord(s[i]) - 97
nxt[i] = last[idx]
last[idx] = i
retour nxt

def getLengthOfOptimalCompression(self, s: str, k: int) -> Int:
si k >= len(s):
retour 0
nxt = auto.build_next(s)
n = len(s)

@lru_cache(Aucun)
def dfs(i: int, rem: int) -> Int:
si n - i <= rem: # supprimer le reste
retour 0
meilleure = flotteur('inf')

# supprimer le caractère actuel
si rem:
best = min(meilleur, dfs(i + 1, rem - 1))

♪ continuer à courir à partir de i
occ = 0
Coût = 1 # la lettre elle-même
pour
alors que cur != - 1 :
occ += 1
suppressions = (cur - i + 1)
si suppressions > Rem:
pause
si le nombre d'heures est égal à (2, 10, 100):
Coût += 1
best = min(meilleur, coût + dfs(cur + 1, rem - suppressions))
cur = nxt[cur]
le meilleur retour

retour dfs(0, k)
«» "

---

### C++ – Tabulation ascendante (pour s'amuser)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
vector<int> buildNext(const string& s) {
int n = s.size();
vecteur<int> suivant(n, -1), dernier(26, -1);
pour (int i = n - 1; i >= 0; --i) {
c = s[i] - 'a';
suivant[i] = dernier[c];
Last[c] = i;
}
retour suivant;
}

int getLengthOfOptimalCompression(chaîne s, int k) {
int n = s.size();
si (k >= n) retourne 0;
vector<int> nxt = buildNext(s);
vecteur<vecteur<int>> dp(k + 1, vecteur<int>(n + 1, -1));

fonction<int(int,int)> dfs = [&](int i, int rem) {
si (dp[rem][i] != -1) retour dp[rem] [i];
si (n - i <= rem) retourner dp[rem] [i] = 0; // supprimer tout ce qui reste
int best = INT_MAX;

si (rem) est le mieux = min(meilleure, dfs(i + 1, rem - 1);

icc = 0;
coût int = 1;
pour (int cur = i; cur != -1; cur = nxt[cur]) {
++occ;
int del = (cur - i + 1) - oct;
en cas de rupture (del > rem);
si (occ) coût++;
best = min(meilleur, coût + dfs(cur + 1, rem - del));
}
retour dp[rem] [i] = meilleur;
};

retour dfs(0, k);
}
};
«» "

---

> Les trois programmes affichent la longueur encodée **minimum** pour toute entrée valide et fonctionnent en fraction de seconde.

---

L'espace et la complexité du temps

Temps Mémoire
- C'est quoi ?
"O(k · n2)" (1 M opérations pour "n = 100", "k = 100")
- En bas Haut de la page

Avec `n ≤ 100` cela est bien en dessous de la limite de 1 seconde sur LeetCode.

---

## 7--Pièges communs & -Qu'en est-il des scénarios

Piège
- Oui.
**Modifications de chiffres manquants** – oublions que le premier chiffre est *non* compté pour la longueur 1 tours. Autres Ajouter le coût seulement lorsque `événement` devient `2`, `10` ou `100`. Autres
Autres **Éliminer le reste** – DP n'atteint jamais la longueur `0` pour des suffixes complètement amovibles. Ajouter `si (n-i <= rem) retourner 0;` tôt. Autres
**Construire `next` incorrectement** – utiliser `s[i]` au lieu de `s[cur]` dans la boucle. Construire `next` de droite à gauche; utiliser `last[26]`. Autres
**Utilisation de la profondeur de récursion > 100** – La récursion de Python peut atteindre la limite. Augmentation de la limite de récursion (sys.setrecursionlimit(2000)) ou utiliser `@lru_cache`. Autres
Autres **Mise à jour des coûts** – ajout de chiffres pour les parcours de longueur `1`. Mise à jour seulement lorsque `occurrences` est dans `{2, 10, 100}`. Autres

---

- Oui. Ce que cela signifie pour votre prochaine entrevue

* **Showcase DP état design** – expliquer clairement les deux dimensions.
* ** Mettre en avant le pré-traitement** – construire le tableau `next` vous sauve d'une solution cubique.
* **Discuss complexity** – `O(k·n2)` est acceptable ici; si vous obtenez une limite de temps de plus d'une fois, vérifiez si vous effectuez un balayage dans la boucle DP.
* **Edge cas** – `k ≥ n` → la réponse est `0`.
`k = 0` → simplement encoder la chaîne d'origine.

Ce problème est un *must-know* pour toute personne ciblant un rôle d'ingénierie logicielle senior ou une entrevue sur les sciences des données où LeetCode Des problèmes difficiles sont fréquents.

---

Réflexions finales

*La compression de la chaîne II* est plus que juste delete k caracteres; il s'agit de la segmentation optimale de l'exécution*.
Un DP propre qui respecte la relation "suivant le même caractère" est le cœur de la solution.

Si vous pouvez expliquer l'état, la transition et la complexité, vous impressionnerez les intervieweurs et obtenir la réponse de "Oui" sur votre CV.

Bonne chance – vous avez ça! C'est ce qu'il a dit.

---

Référence Mots clés

- **Compression de la chaîne II**
- **LeetCode dur**
- ** Programmation dynamique**
- **Encodage de la longueur du trajet**
- **Supprimer les caractères* *
- **La solution de Java DP**
- ** Solution Python DP**
- **C++ Solution DP**
- **Entretien de codage**
- **Question d'entrevue**
- **Préparation de l'entrevue d'embauche**
- **Algorithme Explication* *
- **Défi du codage* *

N'hésitez pas à partager ce billet sur LinkedIn, Medium ou votre blog personnel – il est emballé avec tous les mots-clés recruteurs et les gestionnaires d'embauche aiment!