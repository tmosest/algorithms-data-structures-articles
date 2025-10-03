---
Titre: LeetCode 115. Subséquences distinctes - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code Leet 115 – Subséquences distinctes
** Programmation dynamique difficile* *

Code de la langue
C'est quoi, ça ?
**Java**
**Python**
*C++******solution.cpp**

> Les trois solutions fonctionnent dans **O(n · m)** temps et utilisation **O(min(n, m))** mémoire (la table 2-D est optionnelle – un tableau de roulement 1-D est affiché dans l'implémentation Java).
> La réponse est garantie dans un entier signé 32 bits.

---

- Oui. 1. Java – 1-D DP (O(1) espace supplémentaire)

"Java
// Solution.java
solution de classe publique {
***
* Compter les sous-séquences distinctes de s qui sont égales à t.
* Chaîne source @param s
* @param t chaîne cible
* @retour du nombre de sous-séquences distinctes
*/
public int numDistinct(String s, String t) {
int n = longueur(), m = longueur();

// Si t est plus long que s, impossible de former t
si (m > n) retourner 0;

// dp[j] tiendra le nombre de façons de former t[0..j-1]
// du préfixe de s
int[] dp = nouvelle int[m + 1];
dp[0] = 1; // vide t

pour (int i = 1; i <= n; i++) { // itérer sur s
char sc = s.charAt(i - 1);
// itérer en arrière de sorte que dp[j-1] se réfère à la ligne précédente
pour (int j = m; j >= 1; j--) {
i (sc == t.charAt(j - 1)) {
dp[j] += dp[j - 1];
}
}
}
retour dp[m];
}

public statique vide principal(String[] args) {
Solution sol = nouvelle solution();
Système.out.println(sol.numDistinct("rabbit", "rabbit"); // 3
Système.out.println(sol.numDistinct("babgbag", "bag"); // 5
}
}
«» "

**Pourquoi 1‐D fonctionne? **
La transition `dp[j] = dp[j] + dp[j‐1]` utilise la valeur de la ligne précédente (`dp[j]` avant la mise à jour) et la valeur de la colonne précédente («dp[j‐1]».
En louant `j` de `m` vers le bas à `1`, la valeur de la ligne précédente est toujours intacte quand elle est nécessaire, donc un seul tableau suffit.

---

- Oui. 2. Python – PDD 1-D (compact et lisible)

'`python
# solution. py
Solution de classe:
def numDistinct(s: str, t: str) -> Int:
n, m = len(s), len(t)
si m > n: # Sortie anticipée
retour 0

dp = [0] * (m + 1)
dp[0] = 1

pour sc en s:
pour j dans la plage (m, 0, -1):
Si sc == t[j - 1]:
dp[j] += dp[j - 1]
retour dp[m]

si __nom__ == "__main__" :
sol = Solution()
print(sol.numDistinct("rabbit", "rabbit") # 3
print(sol.numDistinct("babgbag", "bag") # 5
«» "

Python's `range(m, 0, -1)` donne un itérateur inverse, gardant la logique identique à Java.

---

- Oui. 3. C++ – 1-D DP (rapide et sans danger de type)

'`cpp
// solution.cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
int numDistinct(chaîne s, chaîne t) {
int n = s.size(), m = t.size();
si (m > n) retourner 0;

vecteur<int> dp(m + 1, 0);
dp[0] = 1; // vide t

pour (charbon : s) {
pour (int j = m; j >= 1; --j) {
si (sc == t[j - 1]) {
dp[j] += dp[j - 1];
}
}
}
retour dp[m];
}
};

Int main() {
ios::sync_with_stdio(faux);
cin.tie (nullptr);

Solution sol;
Cout << sol.numDistinct("rabbit", "rabbit") << '\n'; // 3
Cout << sol.numDistinct("babgbag", "bag") << '\n'; // 5
retour 0;
}
«» "

> `vector<int>` garantit des boucles arithmétiques signées 32 bits et de style `range` garder le code minimal.

---

Article du blog – LeetCode 115 : Subséquences distinctes – Le Bon, le Mauvais et l'Ugly

> **Cible Public:**
> * Candidats à l'entrevue en génie logiciel*
> * Recruters à la recherche de connaissances solides en PDD*
> * Les étudiants polissent leur boîte à outils d'entrevue*

> **Références géographiques:**
> `Distinct Subsequences`, `Leetcode 115`, `programme dynamique`, `coding interview`, `job interview`, `Java solution`, `Python solution`, `C++ solution`, `algorithmic problem resolution`, `job search coding`, `software engineer interview`, `codding challenge`, `competitive programmation`.

---

# Cracking LeetCode 115: Subséquences distinctes – Le Bon, le Mauvais, et l'Ugly

> *Programmation dynamique (DP) × Manipulation de chaînes*
> *Pourquoi ça compte pour votre prochaine entrevue de codage*

---

Qu'est-ce que les subséquences distinctes?

Dans ce problème classique de LeetCode vous êtes donné deux chaînes:
* **`s`** – la chaîne source,
* **`t`** – la chaîne cible.

Votre tâche est de compter **combien de façons distinctes** vous pouvez supprimer des caractères de **`s`** de sorte que le reste de la chaîne égale **`t`**.
Chaque position dans `s` peut être soit **utilisée** (si elle correspond au caractère actuel dans `t`) ou **supportée**. L'ordre des caractères dans `t` doit être préservé, mais ils n'ont pas besoin d'être contigus dans `s`.

---

La récurrence classique du DP

Laissez

`dp[i][j]` = nombre de façons de former les premiers caractères **`j`** de `t` en utilisant les premiers caractères **`i`** de `s`.

Transition:

* Si «s[i‐1]]»;
«dp[i][j] = dp[i‐1][j‐1]» (cocher ce char)
«+ dp[i‐1][j]» (il l'a pris)
* Sinon:
«dp[i][j] = dp[i‐1][j]» (ne peut pas choisir)

Cas de base:

= 1 ' (vide `t` peut toujours être formé en ne prenant rien)
"i" = 0" (non vide "t" ne peut pas être formé à partir d'un "s" vide) Autres

Réponse : **`dp[n][m]`** où `n ======`` et `m ========.

---

Complexité

Démarche Temps Espace supplémentaire
- C'est quoi ?
2-D DP (tableau complet) **O(n · m)**
Tableau de roulement 1-D **O(n · m)** Autres

> Dans tous les cas, l'algorithme est linéaire dans le produit des longueurs de chaîne et n'utilise que des entiers 32 bits parce que le problème garantit la réponse dans un "int" signé.

---

Pourquoi ce problème est-il une question d'entrevue?

1. **Maîtrise du DP – Les intervieweurs demandent souvent des variations : Nombre de façons de former une chaîne d'une autre ? (en milliers de dollars)
2. ** Optimisation de l'espace** – La solution 1-D démontre une astuce DP classique (itération inverse) qui maintient la mémoire basse.
3. **Connaissance de cas** – Sortie anticipée si `=t=" >="s=" montre une vérification minutieuse des frontières, les intervieweurs de caractères cherchent.
4. **agnosticisme linguistique** – Vous pouvez livrer la solution en **Java, Python ou C++** – les trois langues sont fréquemment utilisées dans les entretiens techniques.

---

## Comment utiliser ces solutions dans votre entrevue

Étape Quoi montrer
C'est pas vrai.
**Exposer le tableau de la PDD**. Autres
**Afficher l'optimisation 1-D**= Expliquer pourquoi l' itération à l'envers préserve les valeurs de la ligne précédente. Autres
**Analyse du temps et de l'espace** Faites la notation et discutez pourquoi 32 bits s'adapte. Autres
**Boîtes de bord de Mention** Autres
**Découvrez les tests**. Autres
**Optionnel**= Partager un test de petite unité ou une routine `main` pour chaque langue. Autres

---

Le bon, le mauvais et le mauvais de l'approche du PDD

Aspect du bien
- C'est quoi ?
La transition `dp[j] += dp[j-1]` est intuitive une fois que vous pensez à l'optimisation 1-D. En oubliant d'itérer `j` à l'envers conduit à **wrong** réponses – ce bug subtil est souvent le coupable de l'échec du test. Autres
**Performance**= O(n · m) est optimal; aucun survol quadratique caché. Aucun – l'algorithme est prouvé optimal pour ce problème. Dans les langues où l'accès aux chaînes est lent (p. ex. l'ancien C), vous devrez peut-être mettre en cache les caractères `s` et `t` pour éviter l'indexation répétée. Autres
**Mémorie**=1-D utilise la mémoire **O(min(n, m)** – idéale pour les contraintes d'entrevue. 2-D est plus facile à lire mais double l'utilisation de la mémoire. En utilisant des entiers 64 bits lorsque ce n'est pas nécessaire, vous pouvez gaspiller de l'espace; mais en toute sécurité si la réponse peut dépasser 32 bits. Autres
**Edge-cases**=" Vide `t` donne toujours 1, vide `s` donne 0 pour non-vide `t`.=" Sortie anticipée pour `m > n` accélère les cas triviaux. Oublier de définir `dp[0] = 1` conduit à zéro nombre. Autres
Les noms variables `dp`, `sc` sont clairs; les commentaires expliquent la direction de la boucle. Python's `range(m, 0, -1)' cache la boucle inverse. C++ `vector<int>` garantit la sécurité du type mais nécessite `#include <bits/stdc++.h>` pour la brièveté. Autres

---

OBJET D'AVENIR

> *Si vous êtes en préparation pour une entrevue d'ingénierie logicielle, les sous-séquences distinctes sont un problème que vous allez presque certainement rencontrer. La maîtrise démontre votre compréhension de la programmation dynamique, de la manipulation des chaînes et de l'optimisation de l'espace. Utilisez les extraits Java, Python et C++ ci-dessus comme référence dans votre repo pratique, et n'oubliez pas de mettre en évidence la perspicacité algorithmique lorsque vous l'expliquez aux intervieweurs. *

---

Lire plus

- [LeetCode 115 – Subséquences distinctes] (https://leetcode.com/problèmes/subséquences distinctes/)
- [Programmation dynamique: de la théorie à la pratique] (https://www.geeksforgeeks.org/dynamic-programming/)
- [Questions d'entrevue que vous devez maîtriser pour 2024](https://exemple.com/interview-prep-2024)

> ** Bonne chance pour votre voyage de codage!**

---