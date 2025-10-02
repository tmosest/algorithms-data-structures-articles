---
titre: LeetCode 1092. Surséquence commune la plus courte -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Superséquence commune la plus courte (Code de Leet 1092) – La bonne, la mauvaise, et la mauvaise
**Mots clés:** *Shortest Common Supersequence, LCS, Dynamic Programming, LeetCode 1092, interview de codage, Java, Python, C++*

---

- Oui. 1. Aperçu du problème

Point de détail
- C'est quoi ?
**Nom**
Numéro de code
Difficulté
**Input**= Deux cordes minuscules `str1` et `str2` (1 ≤ len ≤ 1000)=
La chaîne *shortest* qui contient à la fois `str1` et `str2` comme subséquences. Si plusieurs solutions existent, retourner n'importe quelle solution. Autres
**Exemple**. Autres

Un *subséquence* est obtenu en supprimant zéro ou plus de caractères d'une chaîne sans changer l'ordre des caractères restants.

---

- Oui. 2. Pourquoi ce problème est-il à l'origine de votre portefeuille d'entrevues

- **Showcases DP maîtrise** – Vous avez besoin de l'astuce classique *Longest Common Subsequence* (LCS), un point de départ dans de nombreuses interviews.
- ** Démontre une reconstruction intelligente** – Après avoir calculé LCS, vous devez construire la superséquence en temps linéaire.
- **Scales bien** – Poignées jusqu'à 1000 chaînes de caractères confortablement avec O(m × n) temps et O(m × n) espace.

---

- Oui. 3. Intuition et stratégie en deux étapes

1. **Comptabiliser les LCS**
Le LCS vous dit le plus long commun de la série. Les caractères du LCS doivent apparaître *une fois* dans la réponse finale.

2. **Merger en marchant en arrière* *
À partir des extrémités des deux cordes, marchez vers le début en utilisant la table DP pour décider si :
- Prendre un caractère commun (si égal).
- Prendre un caractère d'une seule chaîne (si différente et la valeur DP indique un meilleur choix).

Enfin, prépendez les caractères restants de chaque chaîne. La chaîne résultante est la plus courte séquence commune (SCS).

---

- Oui. 4. Tableau de programmation dynamique

Laissez

- `m = str1.longueur`, `n = str2.longueur`.
- `dp[i][j]` = longueur de LCS de `str1[0 ... i‐1]` et `str2[0 ... j‐1]`.

Transition:

«» "
Si str1[i-1] == str2[j-1]:
dp[i][j] = 1 + dp[i-1][j-1]
Sinon:
dp[i][j] = max(dp[i-1][j], dp[i][j-1])
«» "

Initialiser `dp[0][*] = dp[*][0] = 0`.

---

- Oui. 5. Reconstruire le SCS

Texte
i = m, j = n, résultat = []

alors que i > 0 et j > 0:
Si str1[i-1] == str2[j-1]:
résultat.append(str1[i-1])
J--
élif dp[i-1][j] > dp[i][j-1]:
résultat.append(str1[i-1])
Je...
Sinon:
result.append(str2[j-1])
J--

alors que 0:
résultat.append(str1[i-1]); i--
alors que j > 0:
résultat.append(str2[j-1]); j--

retour inverse(résultat)
«» "

L'étape inverse est nécessaire parce que nous avons construit la réponse de la fin en arrière.

---

- Oui. 6. Analyse de la complexité

Calcul métrique
C'est pas vrai.
**Temps**= O(m × n) – Tableau DP + suivi linéaire arrière==
**Space**= O(m × n) – Table DP (peut être réduite à O(n) si vous ne gardez que deux lignes, mais la reconstruction a besoin de la table complète)=

Avec `m, n ≤ 1000`, c'est confortablement rapide.

---

- Oui. 7. Liste de contrôle des cas de bord

Cas de bord Quoi regarder?
-- -- -- -- -- -- -- -- --
Le résultat est la chaîne elle-même (la plus courte possible). Autres
Autres Aucun caractère commun.Le résultat est `str1 + str2`. Autres
Autres Une chaîne vide est l'autre chaîne. Autres
Autres Tous les caractères identiques mais les chaînes diffèrent en longueur. Autres

---

- Oui. 8. Mise en œuvre – Java, Python, & C++

> **Conseil:** Gardez votre code propre et ajoutez des commentaires en ligne pour la lisibilité – les intervieweurs apprécient la logique claire.

---

##### 8.1 Java

"Java
***
* LeetCode 1092 – Superséquence commune la plus courte
*/
solution de classe {
public Chaîne plus courteCommonSuperséquence(String str1, String str2) {
int m = str1.longueur(), n = str2.longueur();
int[] dp = nouveau int[m + 1] n + 1;

// Construisez le tableau PDD de LCS
pour (int i = 1; i <= m; i++) {
pour (int j = 1; j <= n; j++) {
Si (str1.charAt(i - 1) == str2.charAt(j - 1))
dp[i][j] = 1 + dp[i-1][j-1];
Autre
dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1];
}
}

// Reconstruire le SCS
StringBuilder sb = nouveau StringBuilder();
i = m, j = n;
pendant que (i > 0 && j > 0) {
si (str1.charAt(i - 1) == str2.charAt(j - 1)) {
sb.append(str1.charAt(i - 1));
i--; j--;
} sinon si (dp[i - 1][j] > dp[i][j - 1]) {
sb.append(str1.charAt(i - 1));
i--;
} autre {
sb.append(str2.charAt(j - 1));
J--;
}
}

pendant (i > 0) { sb.append(str1.charAt(--i)); }
pendant que (j > 0) { sb.append(str2.charAt(--j)); }

retour sb.reverse().toString();
}
}
«» "

---

8.2 Python

'`python
# LeetCode 1092 – Superséquence commune la plus courte
Solution de classe:
def le plus courtCommonSuperséquence(self, str1: str, str2: str) -> str:
m, n = len(str1), len(str2)
Tableau DP
dp = [[0] * (n + 1) pour _ dans la plage (m + 1)]

pour i à portée (1, m + 1):
pour j dans la plage(1, n + 1):
Si str1[i-1] == str2[j-1]:
dp[i][j] = dp[i-1][j-1] + 1
Sinon:
dp[i][j] = max(dp[i-1][j], dp[i][j-1])

# Retour pour construire SCS
i, j = m, n
res = []
alors que i et j:
Si str1[i-1] == str2[j-1]:
res.append(str1[i-1])
i = 1; j = 1
élif dp[i-1][j] > dp[i][j-1]:
Annexe(str1[i-1]); i -= 1
Sinon:
Annexe(str2[j-1]); j -= 1

res.extend(reversed(str1[:i]))
res.extend(reversed(str2[:j]))
retour ''.join(reversed(res))
«» "

---

##### 8.3 C++

'`cpp
// LeetCode 1092 – Superséquence commune la plus courte
solution de classe {
public:
chaîne la plus courteCommonSuperséquence(chaîne str1, chaîne str2) {
int m = str1.size(), n = str2.size();
vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));

// Construire une table LCS
pour (int i = 1; i <= m; ++i)
pour (int j = 1; j <= n; ++j)
dp[i][j] = (str1[i-1] == str2[j-1]) ?
dp[i-1][j-1] + 1 :
dp[i-1], dp[i], j-1);

// Reconstruire le SCS
la chaîne rés;
i = m, j = n;
pendant que (i et j) {
Si (str1[i-1] == str2[j-1]) {
le nom et l'adresse de l'utilisateur;
--i; --j;
} sinon si (dp[i-1][j] > dp[i][j-1]) {
le nom et l'adresse de l'utilisateur;
--i;
} autre {
le nom et l'adresse de l'utilisateur;
--j;
}
}
pendant que (i) res.push_back(str1[--i]);
pendant que j) res.push_back(str2[--j]);

inverse(res.begin(), res.end());
retour rés;
}
};
«» "

---

- Oui. 9. Les bonnes

- **Fondation claire du PDD** – LCS est une question d'entrevue classique; la réutiliser ici démontre une compréhension profonde.
- **Reconstruction propre** – La marche en arrière maintient le code concis et linéaire.
- **Évoluable** – O(106) opérations pour le pire cas, bien en dessous des délais typiques.

---

10 ans. Le "Ugly" – Qu'est-ce qui pourrait vous faire monter

Piège
- Oui.
Autres Oublier d'inverser à la fin La réponse est construite à partir de la queue; inverser est essentiel. Autres
Toujours tester sur les petites chaînes (`"a"`, `"b"`), `i-1` vs `i` est une source fréquente de bogues. Autres
Si `dp[i-1][j] == dp[i][j-1]`, choisir l'une ou l'autre des chaînes fonctionne; votre code gère cela en sélectionnant `str2[j-1]`. Autres
L'utilisation d'une table DP complète est très bien, mais vous pouvez la réduire à O(n) si vous faites attention à la reconstruction. Autres

---

11 ans. Les mauvaises (erreurs communes)

1. **En utilisant seulement une ligne DP**
- Fonctionne pour la longueur LCS, mais vous perdez la table complète nécessaire pour le back-tracking → conduit à une mauvaise SCS ou une complexité supplémentaire.

2. **Appendication avant inversion**
- Beaucoup de solutions par erreur ajouter les caractères dans l'ordre inverse sans inverser à la fin → la réponse sera reflétée.

3. **Ignorer la branche "common"* *
- Certaines fusions naïves oublient de *supprimer* les duplicatas du LCS, produisant une superséquence plus longue.

---

#### 11.1 Quoi éviter dans les entrevues

- **Code Verbose** – Garder les fonctions courtes; éviter les boucles imbriquées à l'intérieur des boucles, sauf si nécessaire.
- **Nombres magiques non mentionnés** – Toujours expliquer la signification de «dp[i][j] > dp[i][j-1]».
- **Assumer l'égalité** – Les cas de bord où une chaîne est vide doivent être traités explicitement pour être complets.

---

11 ans. L'Ugly

- **O(m × n) espace** – Bien que acceptables, certains candidats visent l'espace O(n) en jetant la table tôt. C'est une optimisation *bonne* pour montrer mais complique la reconstruction.
- **Pièges de suivi** – La mauvaise direction donne une réponse *sous-optimale*; revérifiez les transitions DP par rapport aux cas d'essai.

---

11 ans. L'horrible – Quand Ça pose problème.

- ** Grande entrée** – Si le juge impose des limites de mémoire strictes, une table de 1000×1000 (4 Mo en Java) peut encore être d'accord, mais pour 104 il exploserait.
- **Multiples passes** – Re-computer DP ou reconstruire deux fois défait le tag « hard ».

---

11 ans. Correction rapide pour les environnements spatialisés

Si vous devez entrer dans 1 Mo, gardez deux rangées de `dp` pendant la construction, mais *store* la table entière *seulement* si vous avez besoin de reconstruction. Sinon, vous pouvez reconstruire à la volée avec une approche avide à deux pointeurs qui pourrait produire une réponse plus longue mais toujours valable pour les contraintes difficiles.

---

10 ans. Réflexions finales

Vous venez de traverser un problème *hard* qui reconditionne magnifiquement un astuce *easy* DP (LCS). L'exécution de l'une des trois implémentations ci-dessus dans une entrevue impressionnera les gestionnaires d'embauche et vous prouvera que vous êtes prêt à répondre à vos questions.

> **Pro‐Tip:** Combinez cette solution avec une explication succincte de la logique de PDD sous-jacente – c'est-à-dire la combinaison qui transforme un bon candidat en un bon.

Joyeux codage – et heureux entretien! C'est ce qu'il a dit.

---

> *Sentez-vous libre de copier les extraits de code dans votre IDE préféré, de les utiliser en fonction des exemples fournis, et de les partager sur votre portfolio ou LinkedIn pour présenter vos morceaux de résolution de problèmes. *