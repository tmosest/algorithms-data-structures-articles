---
titre: LeetCode 3563. Lexicographiquement la plus petite chaîne après les suppressions adjacentes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 3563 – Lexicographiquement Plus petite chaîne après enlèvements adjacents
> * 250 lettres *

Le problème:
Étant donné qu'une chaîne de caractères `s` (`1 ≤="s ≤ 250`) est constituée de lettres minuscules, nous pouvons supprimer à plusieurs reprises *toute paire adjacente de lettres consécutives dans l'alphabet (y compris la paire circulaire `a‐z`). Après toutes les suppressions possibles, nous voulons la chaîne *lexicographiquement la plus petite* issue.

> Exemple
> `s = "abc"` → supprimer `"bc"` → `"a"` (meilleur que nous pouvons faire)
> `s = "bcda"` → supprimer `"cd"` → `"ba"` → supprimer `"ba"` → `""
> `s = "zdce"` → supprimer `"dc"` → `"ze"` mais `"zdce"` est lexicographiquement plus petit, donc nous conservons l'original.

La clé est que *suppression* une paire peut exposer une nouvelle paire qui devient amovible, mais la suppression d'une paire peut également rendre une suppression ultérieure impossible. Par conséquent, nous devons considérer *toutes* séquences de suppression possibles.

---

- Oui. 1. L'idée – Programmation dynamique sur les intervalles

Laissez

«» "
dp[l][r] = la plus petite chaîne lexicographique pouvant être obtenue
de la sous-chaîne s[l ... r] (inclus).
«» "

La réponse est «dp[0][n‐1]».

- Oui. Cas de base

* `l > r` – sous-chaîne vide → chaîne vide.
* `l == r` – caractère unique – ne peut pas être supprimé → le caractère lui-même.

Transition

Pour une sous-chaîne `s[l ... r]` nous avons deux options:

1. ** Garder le premier personnage**
`s[l]` + `dp[l+1][r]`.

2. **Supprimer `s[l]` avec certains `s[k]` (`l < k ≤ r`)**
Ceci n'est possible que lorsque:

* `s[l]` et `s[k]` sont consécutifs (circulairement) → `isConsec(s[l], s[k])`.
* Le segment *entier* entre eux `s[l+1 ... k-1]` peut être effacé.
C'est exactement quand `dp[l+1][k-1] == """.

Si les deux conditions se maintiennent, après avoir supprimé cette paire, le reste de la
la sous-chaîne est «dp[k+1][r]».
Nous choisissons la plus petite chaîne parmi tous ces candidats.

Parce qu ' il s ' agit d ' un " O(n3) " direct DP (ou récursion mémolisée) fonctionne bien sous une seconde.

---

- Oui. 2. Comment vérifier

Pour deux lettres `c1` et `c2`

«» "
diff = (c1 - 'a' - (c2 - 'a') + 26) % 26
«» "

`diff` est égal `1` ou `25` les lettres sont consécutives
«a‐b», «b‐c», ... ou la circulaire «z‐a», «a‐z».

---

- Oui. 2. Mise en œuvre des références

Voici trois solutions **complètes, prêtes à la production** – Java, Python et C++ – qui suivent la stratégie DP décrite ci-dessus.
Tous les codes sont compilés avec les compilateurs standard:

* **Java** – `Javac Solution.java Solution & & java "
* **Python** – `python3 solution. py "
* **C++** – `g++ -std=c++17 -O2 solution.cpp && ./solution "

---

#### 2.1 Java 17

"Java
Importation de java.util.*;

solution de classe publique {
Chaîne privée s;
Int. privé n;
chaîne privée[]] mémo;

public Chaîne lexicographique Plus petite boucle(s) {
s = s;
c.n = longueur();
mémo = nouvelle chaîne[n][n];
retour dp(0, n - 1);
}

chaîne privée dp(int l, int r) {
si (l > r) retourner ";
si (l) r) retourne String.valueOf(s.charAt(l));

// Si nous gardons le premier caractère
Chaîne best = s.charAt(l) + dp(l + 1, r);

// Essayez de supprimer s[l] avec un certain s[k]
pour (int k = l + 1; k <= r; k++) {
si (s.charAt(l), s.charAt(k)) &&
dp(l + 1, k - 1). estEmpty() {

Candidat à la chaîne = dp(k + 1, r);
si (candidate.comparerÀ(meilleure) < 0) le meilleur = candidat;
}
}
mémo[l][r] = meilleur;
le meilleur retour;
}

booléen privé estconsécutif(char a, char b) {
(a - 'a' - (b - 'a') + 26) % 26;
retour diff == 25;
}

// ----------------------------------------------------------------------------------
// Harnais d'essai – peut être retiré dans la production
// ----------------------------------------------------------------------------------
public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.lexicographiquementSmallestString("abc")); // a
Système.out.println(sol.lexicographiquementSmallestString("bcda")); // (vide)
System.out.println(sol.lexicographiquementSmallestString("zdce")); // zdce
Système.out.println(sol.lexicographiquementSmallestString("ab")); // a
Système.out.println(sol.lexicographiquementSmallestString("za")); // (vide)
}
}
«» "

---

2.2 Python 3

'`python
importer des functools

Solution de classe:
def lexicographieallySmallestString(self, s: str) -> str:
n = len(s)

@functools.lru_cache(maxsize=Aucune)
def dp(l: int, r: int) -> str:
si l > r:
retour ""
si l == r:
retour s[l]

1. Gardez le premier caractère
best = s[l] + dp(l + 1, r)

2. Essayez de supprimer s[l] avec un s[k]
pour k dans la plage(l + 1, r + 1):
si self._consecutive(s[l], s[k]) et dp(l + 1, k - 1) == "":
cand = dp(k + 1, r)
si cand < meilleur:
meilleur = cand
le meilleur retour

retour dp(0, n - 1)

@staticmethod
Def _consecutive(a: str, b: str) -> C'est vrai.
diff = (ord(a) - ord(b)) % 26
retour diff == 1 ou diff == 25

♪ (En milliers de dollars des États-Unis)
♪ Exemple d'utilisation
♪ (En milliers de dollars des États-Unis)
si __nom__ == "__main__" :
sol = Solution()
print(sol.lexicographiquementSmallestString("abc")) #a
impression(sol.lexicographiquementSmallestString("bcda")) # ''
print(sol.lexicographiquementSmallestString("zdce")) # zdce
print(sol.lexicographiquementSmallestString("ab")) # une
«» "

---

#### 2.3 C++17

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne lexicographiquement Plus petite(chaîne s) {
int n = s.size();
vector<vector<string>> memo(n, vector<string>(n));
pour (int i = 0; i < n; ++i) mémo[i]i] = chaîne(1, s[i]);

pour (int len = 2; len <= n; + len) {
pour (int l = 0; l + len - 1 < n; ++l) {
int r = l + len - 1;
string best = s[l] + mémo[l + 1][r];

pour (int k = l + 1; k <= r; ++k) {
si (consec(s[l], s[k]) && memo[l + 1][k - 1].vide() {
string cand = (k == r) ? "" : mémo[k + 1][r];
si (cand < best) best = cand;
}
}
mémo[l][r] = meilleur;
}
}
retour du mémo[0][n - 1];
}

particulier:
Bool consec(char a, char b) const {
(a - 'a' - (b - 'a') + 26) % 26;
retour diff == 25;
}
};

// (En milliers de dollars des États-Unis)
// Démo en main – supprimer dans la production
// (En milliers de dollars des États-Unis)
Int main() {
Solution sol;
Cout << sol.lexicographiquementSmallestString("abc") << '\n'; // a
Cout << sol.lexicographiquementSmallestString("bcda") << '\n'; // (vide)
cout << sol.lexicographiquementSmallestString("zdce") << '\n'; // zdce
retour 0;
}
«» "

Les trois implémentations s'exécutent en temps `O(n3)` et en mémoire `O(n2)`.
Avec `n ≤ 250` le nombre d'opérations le plus défavorable est inférieur à 16 millions – assez rapide pour la limite de 2 secondes.

---

- Oui. 2. Ce qui fonctionne bien – Le bien

Aspect
- Oui.
**Correctness** – le DP explore chaque chemin de suppression, garantissant le véritable minimum. Autres
**Simplicité** – le code est une petite fonction récursive plus un petit assistant, pas de structures de données exotiques. Autres
**Scalabilité** – « O(n3) » avec « n = 250 » est banal pour les processeurs modernes. Autres
**Extensibilité** – le même modèle DP peut être adapté à de nombreux problèmes d'éloignement intervalle. Autres

---

- Oui. 3. Où il peut faire demi-tour – le "Bad"

Numéro
- Oui.
**Le temps** – un retour naïf ferait exploser (factoriel) – le DP coupe cela. Autres
**Space** – une table de chaînes mémolisées peut utiliser beaucoup de mémoire ; nous conservons des chaînes `O(n2)`, mais chaque chaîne peut être jusqu'à des caractères `n` longs – toujours < 250 × 250 kB. Autres
**Readability** – Interval DP est un modèle classique qui peut ne pas être évident pour les nouveaux venus. Autres

---

- Oui. 4. Ce que nous n'avons pas fait – l'Ugly

* L'algorithme cupide d'élimination des piles (pop quand le courant supérieur est consécutif) ne donne pas toujours la plus petite chaîne lexicographiquement.
Il fonctionne pour les paires consécutives adjacentes *classical* 0\delete jusqu'à ce qu'aucune paire ne reste problème, mais l'exigence ici est de *minimiser* la chaîne finale, de ne pas minimiser le nombre de suppressions.

* Une énumération brute de tous les ordres de suppression est **exponentielle** – complètement impraticable, même pour «S» = 20».

Ainsi, l'intervalle DP est la solution la plus propre et la plus fiable.

---

- Oui. 5. Essai du Code

Source : Produit prévu Raison
- C'est quoi ?
Supprimer "bc"
"bcda""""""cd` → `ba` → `ba` → `a` → `z` → rien
Aucune suppression ne donne une chaîne plus petite.
`aab`= `a`= conserver la première `a`, supprimer `ab` Autres
Supprimer la paire `za` Autres
La paire `az`

Exécutez les harnais de test dans chaque fichier ou utilisez le coureur LeetCode en ligne.

---

- Oui. 6. A emporter pour les entrevues

1. **Identifiez l'intervalle** – si l'opération dépend d'un segment contigu, DP sur les longueurs est un go‐to.
2. **Le code peut être supprimé?** en tant que fonction booléenne (`isConsecutive`).
3. **Memoise** – éviter la recomputation; en Java ou en Python utiliser un tableau 2-D ou `lru_cache`.
4. **Comparer les chaînes lexicographiquement** – `<` fonctionne dans toutes les langues.

---

- Oui. 6. SEO et notes d'apprentissage

Cet article est écrit pour:

* **Programmeurs concurrents** à la recherche d'une solution DP propre.
* ** Ingénieurs logiciels** se préparant pour les entrevues de codage (LeetCode, HackerRank).
* **Étudiants** apprenant l'intervalle DP et la mémorisation récursive.

N'hésitez pas à adapter le code de référence à vos propres projets ou matériels pédagogiques.

Bon codage ! C'est ce qu'il a dit.

---

**Mots clés:** Java DP, suppression de l'intervalle Python, récursion C++, chaîne laxicographiquement plus petite, lettres consécutives, interview d'algorithme, problème LeetCode, solution O(n3), tutoriel d'intervalle DP.