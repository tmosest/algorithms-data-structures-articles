---
titre: LeetCode 44. Correspondance Wildcard -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
## Correspondance Wildcard – LeetCode 44
**Tranquillité 2000 ≤=========================================================================================================================================================================================================================================================

> Les meilleures questions d'entrevue sont celles que vous pouvez répondre avec confiance et expliquer clairement. – *Chute d'emploi 101*

---

- Oui. 1. Aperçu du problème

Détails du champ
C'est quoi ?
**Nom** Autres
**LeetCode ID**
Difficulté
Deux chaînes `s` (texte) et `p` (modèle)
**Output**="true` si `p` correspond au *entre* `s`, `faux` sinon=
**Règles de la carte de faune**======================================================================================================================================================================================================================================================
**Constraints**"0 ≤ s.longueur, p.longueur ≤ 2000`<br>`s` seulement lettres anglaises minuscules<br>`p` seulement lettres anglaises minuscules, `?`, `*`

> Exemple
> `s = "aa"`, `p = "*" → true`
> `s = "cb"`, `p = "?a" → faux "

---

- Oui. 2. Intuition

Nous avons besoin de savoir ** si les deux chaînes peuvent "align"** lorsque nous remplaçons `?` et `*` par les caractères appropriés.

Le problème est une programmation dynamique classique sur les cordes :

«» "
dp[i][j] = est-ce que s[0..i) correspond à p[0..j)?
«» "

* `i` est la longueur du préfixe considéré de `s`
* `j` est la longueur du préfixe considéré de `p`

Avec cette récurrence, nous pouvons explorer toutes les possibilités **une fois** et obtenir un espace linéaire.

---

- Oui. 3. Quatre façons de résoudre

Approche Idée Complexité
- C'est quoi ?
**Récursifs**=Essayez chaque choix en rencontrant `*`.= O(2^n) temps== Très intuitif== Temps exponentiel, débordement de pile==
**Mémorisé** , même que récursif + cache , O(n m) temps , O(n m) espace , rapide , encore lisible , utilise toujours la pile de récursion
**Tabulation**= Tableau DP ascendant== O(n m) temps, O(n m) espace== Pas de récursion, plus facile à déboguer== Mémoire lourde pour 2000 × 2000 Autres
Autres **Space-Optimized DP** Exclure seulement la ligne précédente O(n m) time, **O(m)** space , 4 Mo en C++/Java, 2000 * 2000 , 4 Mo , légèrement plus logique pour la première colonne ,

> **Bonus** – une solution *greedy* linéaire à temps constant qui scanne de gauche à droite et rétrospective au besoin.
> Dans la pratique, la solution DP est ce que la plupart des intervieweurs s'attendent, mais l'astuce gourmande peut être une réponse soignée.

Voici les trois versions de code que vous voulez sur votre CV et dans votre portfolio GitHub.

---

- Oui. 4. Mise en œuvre des références

> **Astuce** – Conservez une copie du code PDD de votre GitHub, et mentionnez que vous *avez compris* la récurrence lorsqu'on vous a demandé.

---

##### 4.1 Java – PDD ascendant (2-D)

"Java
// 44. Correspondance Wildcard – LeetCode
solution de classe publique {
***
* Classic DP: dp[i][j] == true si s[0..i) correspond à p[0..j)
* Nous utilisons (n+1) x (m+1) table booléenne, où n = s.longueur(), m = p.longueur()
*/
boolean public isMatch(String s, String p) {
int n = longueur(), m = longueur();
boolean[][] dp = nouveau boolean[n + 1][m + 1];
dp[0][0] = true; // le motif vide correspond à une chaîne vide

/* Première ligne : s est vide – seulement en tête '*' en p peut correspondre */
pour (int j = 1; j <= m; j++) {
si (p.charAt(j - 1) == '*') dp[0][j] = dp[0][j - 1];
}

/* Remplir le tableau */
pour (int i = 1; i <= n; i++) {
pour (int j = 1; j <= m; j++) {
char pc = p.charAt(j - 1);
si (pc) {
dp[i] [j] = dp[i - 1] [j]]
} sinon si (pc == '?'"" pc == s.charAt(i - 1)) {
dp[i][j] = dp[i - 1][j - 1];
} autre {
dp[i][j] = faux;
}
}
}
retour dp[n][m];
}
}
«» "

* Heure*: **O(n m)**
*Espace*: **O(n m)** – pour 2000 × 2000, c'est ~4 Mo, amende pour LeetCode.

---

4.2 Python – PDD optimisé pour l'espace

'`python
44. Matching Wildcard – Python 3
def is_match(s): str, p: str) -> C'est vrai.
n, m = len(s), len(p)

# prev[j] est dp[i-1][j] de la ligne précédente
prev = [Faux] * (m + 1)
prev[0] = Vrai

# Initialiser la première ligne (vide s)
pour j dans la plage (1, m + 1):
si p[j - 1] == '*':
prev[j] = prev[j - 1]

pour i dans la plage(1, n + 1):
Carrière = [Faux] * (m + 1)
curr[0] = Faux # non-vide s ne peut correspondre au motif vide
pour j dans la plage (1, m + 1):
si p[j - 1] == '*':
curr[j] = prev[j] ou curr[j - 1]
Elif p[j - 1] == '?' ou p[j - 1] == [i - 1]:
curr[j] = prev[j - 1]
Sinon:
[j] = Faux
prev = curr

retour prev[m]
«» "

*Space*: **O(m)**
*Temps*: **O(n m)** (4 millions d'opérations – trivial pour CPython).

---

#### 4.3 C++ – PDD ascendant avec grilles 1-D

'`cpp
// 44. Correspondance Wildcard – C++17
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
bool isMatch(chaîne s, chaîne p) {
int n = s.size(), m = p.size();
vecteur<bool> prev(m + 1, false), curr(m + 1, false);
prev[0] = true; // un motif vide correspond à une chaîne vide

// Texte vide, seul '*' peut correspondre
pour (int j = 1; j <= m; ++j)
si (p[j - 1] == '*') prev[j] = prev[j - 1];

pour (int i = 1; i <= n; ++i) {
curr[0] = false; // texte non vide ne peut correspondre au motif vide
pour (int j = 1; j <= m; ++j) {
Si (p[j - 1] == '*')
curr[j] = prev[j]
Sinon, si (p[j - 1] == '?'"" p[j - 1] == [i - 1])
curr[j] = prev[j - 1];
Autre
curr[j] = faux;
}
prev.swap(curr);
}
retour prev[m];
}
};
«» "

*Espace*: **O(m)**
* Temps*: **O(n m)** – encore ~4 millions d'ops, assez rapide même dans une interview serrée.

---

### 4.4 Greedy Linear-Time, solution d'espace constant

> ** Pourquoi parler d'avidité ? * *
> Dans de nombreux panels d'entrevue, une solution *simple-pass* est un facteur de "wow". L'algorithme gourmand est aussi la réponse *canonique* à ce problème.

Texte
Marche à travers s et p une fois.
Gardez deux pointeurs :
i – indice actuel en s
j – indice actuel en p
Suivre :
starIndex – le plus récent '*' en p (ou -1 si aucun)
iAfterStar – index en s quand le dernier '*' a été apparié

Si les caractères correspondent ou p[j] == '?', avancez les deux.
Si p[j] == '*', rappelez-vous les positions et sautez '*'.
En cas d'inadéquation et nous avons un précédent '*', retour:
j = étoileIndex + 1 (réutiliser le '*')
i = iAfterStar + 1 (consommer un autre omble de s)
iAprèsStar = i
En cas d'inadéquation et non '*', retourner faux.
«» "

*Heure*: **O(n + m)**
*Espace*: **O(1)**
* Bon pour les entrevues* : vous pouvez expliquer le raisonnement en 3-5 minutes.

> **Caveat** – Greedy ne fonctionne que pour cette grammaire exacte (`?` et `*`). Pour les autres wildcards il peut échouer.

---

- Oui. 4. Échanges – bons, mauvais, Méchant

Aspect du bien
- C'est quoi ?
**Readability**
La graisse est linéaire.
**Edge-cases**= Tous les `*` dans le pattern → correspondent à une chaîne vide==Il faut gérer séparément les chaînes vides=Les bogues hors-par-un sont courants dans le manuel DP=
**La perception de l'interview**=Le DP montre la compréhension de la chaîne DP==La graisse démontre la créativité algorithmique==La récursive peut être vue comme =lazy== et non comme optimale==

> **Key Takeaway** – *Démarrez toujours avec la solution de travail la plus simple (récursive), puis mettez-la à niveau à un DP prêt à la production. Dans les entrevues, l'étape de mise à niveau (ajout de mémorisation ou de tabulation) démontre des compétences en résolution de problèmes. *

---

- Oui. 5. Liste de contrôle de préparation à l'entrevue

1. ** Clarifier le match entier** – le motif doit couvrir *tout* de `s`.
2. **Déclarez la sémantique de la carte sauvage** – écrivez-les explicitement.
3. **Demander des contraintes de temps et d'espace** – confirmer 2000×2000 correspond à la mémoire.
4. **Afficher la récurrence du PDD** – dessiner la grille `dp[i][j]`.
5. **Écrire le code dans la langue d'entrevue** – utiliser Java/Python/C++ comme demandé.
6. ** Mentionnez l'astuce gourmande** – parfois les intervieweurs veulent que vous pensiez en dehors du DP.
7. **Parler d'un exemple non trivial** – p.ex. « s»abbcd », p"*b?d"« pour démontrer les transitions d'état.
8. **Demander des questions claires** – par exemple, « Qu'en est-il des motifs avec plusieurs suites «*» ? – pour montrer une compréhension profonde.
9. **Cas de bord de discussion** – chaînes vides, toutes `*`, ou modèle commence par `*`.
10. **La complexité de l'espace-temps** – toujours les énoncer et les comparer.

---

- Oui. 6. Pensées finales

Wildcard Matching est l'un de ces problèmes "Hard" qui ** passe de la force brute à l'élégant DP**. La maîtrise vous donne :

- Une bonne compréhension de **string DP** qui s'applique à de nombreux problèmes de LeetCode (p. ex., "Regular Expression Matching", "Decode Ways").
- Un modèle DP** optimisé pour l'espace, prêt à l'emploi, que vous pouvez déposer dans n'importe quelle entrevue.
- Oui. La capacité de lancer une solution **greedy** lorsque vous devez impressionner.

Ajoutez les implémentations de référence à votre portfolio, écrivez un billet de blog rapide ou une courte vidéo expliquant l'algorithme, et vous serez bien placé pour marquer haut sur les écrans techniques et les tests de codage.

Bonne chance avec votre parcours de codage et la prochaine interview!

---

- Oui. 7. Bibliographie et lecture supplémentaire

- **Problème de code 44** – [Mise en correspondance des cartes marines](https://leetcode.com/problèmes/wildcard-matching/)
- **Cracking the Coding Interview – String DP** – Chapitres sur la programmation dynamique et les expressions régulières.
- **GeeksforGeeks – Wildcard Matching** – fournit le passage gourmand.

---

**Note moyenne** – Si vous préparez un message vidéo ou blog, intégrez les extraits de code avec la mise en valeur syntaxique. Les recruteurs aiment voir une solution propre et bien commentée.

Bon codage ! C'est ce qu'il a dit.

---

**Référencement Mots-clés**: LeetCode 44 Wildcard Matching, Java DP solution, Python wildcard regex, C++ 1D array DP, algorithme gourmand pour wildcard, conseils d'entrevue, programmation dynamique de chaîne, complexité du temps, optimisation de l'espace.

---

*(Fin de guide de référence – n'hésitez pas à vous adapter ou à vous étendre avec les tests unitaires ou Junit en Java.) *