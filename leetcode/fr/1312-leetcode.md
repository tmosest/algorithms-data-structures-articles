---
titre: LeetCode 1312. Étapes minimum d'insertion pour faire un Palindrome à cordes -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
Code maître de Leet 1312 – *Étapes d'insertion minimale pour faire un Palindrome à cordes*
*(Un guide complet, prêt à l'entrevue pour Java, Python & C++) *

---

### TL;DR
- **Problème**: Avec une chaîne `s`, retourner le nombre *minimum* d'insertions nécessaires pour en faire un palindrome.
- **Approche optimale**: Subséquence palindromique la plus longue (LPS) → `minInsertions ====S – LPS`.
- **Complexités**: temps «O(n2)», espace «O(n2)» (peut être réduit à «O(n)» Si vous êtes à l'aise).
- **Pourquoi c'est important**: C'est un problème DP classique qui montre que vous pouvez réduire un problème de manipulation de chaînes à LCS/LPS. Les recruteurs adorent ça.

---

Récapitulation des problèmes

Texte
Entrée: s = "mbadm"
Produit: 2

Explication :
"mbadm" → "mbdadbm" (insérer 'd' après 'b', 'a' avant 'd')
Deux insertions sont suffisantes, et vous pouvez le prouver.
«» "

− Longueur des " s " : " 1 ≤ " s " ≤ 500 "
- Seulement des lettres anglaises minuscules.

---

- Oui. Pourquoi LPS fonctionne

Une insertion seulement *adds* caractères; il ne supprime jamais ou ne modifie jamais ceux existants.
La plus longue séquence qui est déjà un palindrome peut rester intacte – nous n'avons qu'à insérer les caractères manquants.
Ainsi:

Texte
minInsertions ====s – longueur_de_longest_palindromic_subséquence(s)
«» "

La constatation de la LPS est identique à la constatation de la LCS entre les « s » et son inverse (« rev(s) »).
C'est pourquoi nous utilisons le classique **La plus longue séquence commune DP**.

---

- Oui. PDD Récurrence

Que `dp[i][j]` soit la longueur du LCS de `s[0...i-1]` et `rev[0...j-1]`.

«» "
si s[i-1] == rev[j-1] → dp[i][j] = 1 + dp[i-1][j-1]
autres → dp[i][j] = max(dp[i-1][j], dp[i][j-1])
«» "

Réponse: `n - dp[n][n]`, où `n = s.longueur()`.

---

La complexité

Complexe métrique
C'est pas vrai.
"O(n2)" ("n ≤ 500" → 250 k opérations, trivial pour toute langue)
Tableau DP de l ' espace < < O(n2) > >
Réduire l'espace à "O(n)" par des lignes de roulement (non indiquées ci-dessous pour plus de clarté). Autres

---

## 5--Cas de bord et pièges communs

Piège
- Oui.
Oubliez d'inverser la chaîne de caractères `StringBuilder(s).reverse()` (Java), `s[:-1]` (Python), `reverse()` (C++)
Utiliser `i <= n`, `j <= n` et accéder `s[i-1]` Autres
Autres Grande utilisation de la mémoire sur le tableau 2-D, `vector<vector<int>> dp(n+1, vector<int>(n+1, 0));` est bon pour n ≤ 500.

---

Mise en œuvre du code

Autres **Les trois versions utilisent la même logique DP – il suffit de modifier la syntaxe. **

#### 6.1 Java

"Java
solution de classe publique {
int public minInsertions(String s) {
int n = s.longueur();
String rev = nouveau StringBuilder(s).reverse().toString();

int[] dp = nouveau int[n + 1] [n + 1];

pour (int i = 1; i <= n; i++) {
pour (int j = 1; j <= n; j++) {
si (s.charAt(i - 1) == rev.charAt(j - 1)) {
dp[i][j] = dp[i - 1] [j - 1] + 1;
} autre {
dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1];
}
}
}
retour n - dp[n][n];
}
}
«» "

6.2 Python

'`python
Solution de classe:
def minInsertions(self, s: str) -> Int:
n = len(s)
Rev = s[:-1]
dp = [[0] * (n + 1) pour _ dans l ' intervalle (n + 1)]

pour i dans la plage(1, n + 1):
pour j dans la plage(1, n + 1):
Si s[i - 1] == rev[j - 1]:
dp[i][j] = dp[i - 1] [j - 1] + 1
Sinon:
dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])

retour n - dp[n][n]
«» "

*### 6.3 C++

'`cpp
solution de classe {
public:
int minInsertions(chaîne s) {
int n = s.size();
chaîne de caractères rev(s.rbegin(), s.rend());
vector<vector<int>> dp(n + 1, vector<int>(n + 1, 0));

pour (int i = 1; i <= n; ++i) {
pour (int j = 1; j <= n; ++j) {
Si (s[i - 1] == rev[j - 1])
dp[i][j] = dp[i - 1] [j - 1] + 1;
Autre
dp[i][j] = max(dp[i - 1][j], dp[i][j - 1];
}
}
retour n - dp[n][n];
}
};
«» "

---

## 7-

Autres Test d'entrée prévu
- C'est quoi ?
""zazz" ""0"
""mbadm" """" "2"
""code de sécurité" """
"a" "0"
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

Exécutez les tests d'unité fournis dans votre éditeur IDE ou LeetCode en ligne pour vérifier l'exactitude.

---

- Oui. Pertinence réelle-mondiale

- **Éditeurs de texte et IDE**: Les moteurs automatiques et de vérification orthographique doivent comparer les chaînes avec des modifications minimales.
- **Séquençage de l'ADN**: La recherche de subséquences palindromiques est essentielle pour l'analyse du génome.
- **Compilateurs**: Les motifs palindromiques aident à mettre en évidence et à vérifier la syntaxe.

---

## 9- Accueil Leçons

C'est bien, c'est mal.
C'est pas vrai.
Clear **problèmes reduction**: LPS → LCS → DP=1 Certaines solutions utilisent des approches *brute-force* ou *récursive* qui explosent exponentiellement.
**Code modulaire**: Séparer la méthode `minInsertions`, réutilisable dans les interviews.
** Variante optimisée de l'espace** : DP unidimensionnel (s'il est demandé)

---

Bonus : optimisation de l'espace (O(n)) Python Implementation

'`python
def minInsertions(s): str) -> Int:
Rev = s[:-1]
n = len(s)
Prév = [0] * (n + 1)
pour i dans la plage(1, n + 1):
[0] * (n + 1)
pour j dans la plage(1, n + 1):
cur[j] = prev[j - 1] + 1 si s[i-1] == r[j-1] sinon max(prev[j], cur[j-1])
prev = cur
retour n - prev[n]
«» "

---

Pourquoi ce blog vous aide à trouver un emploi

- **Contenu riche en mots-clés**: LeetCode 1312.
- **Structure claire**: Intro → Intuition → DP → Code → Tests → Takeaways.
- **Code actionnable**: Extraits prêts à copier pour Java, Python, C++.
- **Ton professionnel**: Démontre une compréhension profonde des concepts algorithmiques.

Autres **Vous voulez plus de guides prêts à l'entrevue?** Abonnez-vous à notre newsletter ou consultez la série complète sur *Programmation dynamique, graphiques et structures de données*.

---

Code final Cheat- Feuille

"Java
// Java
solution de classe {
int public minInsertions(String s) { /* DP comme ci-dessus */ }
}
«» "

'`python
# Python
Solution de classe:
def minInsertions(self, s: str) -> int: # DP comme ci-dessus
«» "

'`cpp
// C++
solution de classe {
public:
int minInsertions(chaîne s) { /* DP comme ci-dessus */ }
};
«» "

Copier, coller, courir, et vous êtes prêt pour votre prochaine question d'entrevue. Bon codage 