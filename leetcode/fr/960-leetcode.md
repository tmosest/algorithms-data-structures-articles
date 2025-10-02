---
titre: LeetCode 960. Supprimer les colonnes pour faire trier III -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Problème – LeetCode 960: *Supprimer les colonnes pour faire trier III*

**Objectif**
Étant donné un tableau de chaînes `n` de longueur égale `m`, supprimer le nombre minimum de colonnes de sorte que **chaque chaîne** restante soit dans un ordre lexicographique non décroissant (c'est-à-dire que ses caractères sont triés de gauche à droite).

Échantillon Entrée Sortie Raisonnement
- C'est quoi ?
"["babca", "bbazb"]" Supprimer les colonnes `0,1,4` → `["bc","az"]`. Autres
Toute colonne restante briserait l'ordre. Autres
Toutes les lignes déjà triées. Autres

Contraintes
«» "
1 ≤ n ≤ 100
1 ≤ m ≤ 100
strs[i] se compose de lettres anglaises minuscules
«» "

---

- Oui. 2. Intuition – Subséquence de colonne la plus longue valide

Si nous conservons un sous-ensemble de colonnes, elles doivent respecter la règle de commande ** pour toutes les lignes**.
Pensez à chaque colonne comme un caractère et nous voulons la plus longue subséquence de colonnes qui est **compatible**:

«» "
Colonne j peut précéder la colonne i
Pour chaque ligne r: strs[r][j] ≤ strs[r][i]
«» "

Si nous trouvons la plus longue subséquence (appelez-la L), alors les suppressions minimales sont `m – L`.

Le problème est essentiellement le **Longe Augmenting Subsequence (LIS)** sur l'ensemble de colonnes avec une comparaison personnalisée.
Parce que `m ≤ 100`, une simple solution de programmation dynamique `O(m2 · n)` est assez rapide.

---

- Oui. 3. Algorithme (Programmation dynamique)

«» "
dp[i] = longueur de la plus longue séquence valide se terminant à la colonne i
réponse = 0

pour i = 0 ... m-1
dp[i] = 1 // subséquence de longueur 1 (seulement colonne i)
pour j = 0 ... i-1
si la colonne j peut précéder la colonne i // vérifier toutes les lignes
dp[i] = max(dp[i], dp[j] + 1)
réponse = max(réponse, dp[i])

retour m - réponse
«» "

*Le contrôle de la colonne j peut précéder la colonne i.*
Bouclez toutes les lignes `r`.
Si un `strs[r][j] > strs[r][i]`, la paire est invalide → pause.
Si toutes les lignes passent, la paire est valide.

complexité temporelle: "O(m2 · n) "
complexité spatiale: `O(m)`

---

- Oui. 4. Mise en œuvre des références

#### 4.1 Java

"Java
Importation de java.util.*;

solution de classe publique {
public int minDeletionSize(String[] strs) {
int n = longueur strs; // nombre de lignes
int m = strs[0].longueur(); // nombre de colonnes

int[] dp = nouvelle int[m];
int best = 0;

pour (int i = 0; i < m; i++) {
dp[i] = 1; // au moins cette colonne seule
pour (int j = 0; j < i; j++) {
si (peutprécéder(strs, j, i)) {
dp[i] = Math.max(dp[i], dp[j] + 1);
}
}
best = Math.max(best, dp[i]);
}
retour m - meilleur; // colonnes à supprimer
}

*** Retourne true si la colonne j peut précéder la colonne i pour toutes les lignes */
boîte de booléen privéePrecede(String[] strs, int j, int i) {
pour (String s : strs) {
si (s.charAt(j) > s.charAt(i)) {
retourner faux;
}
}
retour vrai;
}
}
«» "

---

4.2 Python

'`python
Solution de classe:
def minDélétion Taille(self, strs: List[str]) -> Int:
n, m = len(strs), len(strs[0)]
dp = [1] * m
meilleur = 0

pour i dans la plage (m):
pour j dans la plage i:
si tous(s[j] <= s[i] pour s dans strs):
dp[i] = max(dp[i], dp[j] + 1)
best = max(best, dp[i])

retour m - meilleur
«» "

---

### 4.3 C++

'`cpp
solution de classe {
public:
int minDeletionSize(vecteur<string>& strs) {
int n = strs.size();
int m = strs[0].size();
vecteur<int> dp(m, 1);
int best = 0;

pour (int i = 0; i < m; ++i) {
pour (int j = 0; j < i; ++j) {
bool ok = true;
pour (int r = 0; r < n; ++r) {
si (strs[r][j] > strs[r][i]) { ok = faux; casser; }
}
si (ok) dp[i] = max(dp[i], dp[j] + 1;
}
best = max(best, dp[i]);
}
retour m - meilleur;
}
};
«» "

---

- Oui. 5. Les bons, les mauvais, les méchants

Aspect du bien
- C'est quoi ?
**Problème Compréhension**= Effacer: trouver les suppressions minimales → la plus longue colonne valide subséquence== Mauvaise lecture ==____________________________________________________________________________________________________________________________________________________________________________________________________________________________ Autres
**Le choix de l'algorithme**Le DP simple ('O(m2·n)') est rapide et facile à raisonner.
**Cas d'esquive**=Poignées `m = 1`, toutes les lignes déjà triées== Oublier de soustraire `m` → mauvaise réponse== Ne pas vérifier toutes les lignes pour chaque paire → bugs silencieux===
Autres **Codage Style**=Clean helper `canPrecede` améliore la lisibilité==Les boucles en ligne deviennent difficiles à déboguer== Mélanger les indices 0 et 1= = erreurs hors-par-un==
**Tests**= Tests unitaires pour échantillons, cas aléatoires== Pas de tests → confiance faible== Tests de stress sur des données aléatoires 100x100==
**Complexité**

** À emporter :** Gardez la solution simple, testez soigneusement et rappelez-vous que les contraintes du problème permettent une solution DP propre.

---

- Oui. 6. Article de blog optimisé par le SEO

> **Titre:**
> *Supprimer les colonnes pour faire trier III – LeetCode 960 – Java, Python, C++ Solution DP et conseils d'entrevue*

> **Désignation de la Méta (155 caractères):**
> Master LeetCode 960 -Supprimer les colonnes pour faire trier III-- avec une solution PD claire en Java, Python et C++. Apprenez les bonnes, les mauvaises et les mauvaises parties des entrevues de codage.

---

- Oui. 1. Présentation

Si vous préparez pour des entretiens d'ingénierie logicielle, **LeetCode 960 – Supprimer les colonnes pour faire Trier III** est un agrafe. Le défi teste votre capacité à penser aux subséquences, à la programmation dynamique et au traitement minutieux des données multidimensionnelles. Ci-dessous, nous traversons une solution DP propre, fournissons des implémentations dans **Java**, **Python** et **C++**, et discutons des pièges communs qui peuvent vous coûter une interview.

- Oui. 2. Récapitulation des problèmes

Étant donné un tableau de chaînes de longueur égale, nous pouvons supprimer tout ensemble d'indices de colonnes. Après les suppressions, **chaque ligne** doit être triée en ordre non décroissant. Retournez le nombre minimal de suppressions nécessaires.

> Exemple
> `["babca","bbazb"]` → Supprimer les colonnes `{0,1,4}` → Résultat `["bc","az"]` → **3 suppressions**.

- Oui. 3. Pourquoi une subséquence de plus en plus longue (LIS) sur les colonnes?

Si nous conservons un sous-ensemble de colonnes, elles doivent respecter la règle de commande ** pour toutes les lignes**.
Ainsi, nous pouvons traiter chaque colonne comme une lettre et rechercher la plus longue séquence de colonnes qui soit compatible: pour toute colonne antérieure `j` et la colonne ultérieure `i`, toutes les lignes satisfont `strs[r][j] ≤ strs[r][i]`.

La longueur maximale `L` d'une telle séquence nous indique le nombre de colonnes que nous pouvons garder. La réponse est simplement "m – L".

Comme les contraintes (`m, n ≤ 100`) sont minuscules, une approche de programmation dynamique simple suffit.

- Oui. 4. Formule PDD

«» "
dp[i] = 1
pour j dans [0, i):
si la colonne j peut précéder i (cochez toutes les lignes):
dp[i] = max(dp[i], dp[j] + 1)
«» "

L'état de l'aide -colonne j peut précéder i-
Texte
R : strs[r][j] ≤ strs[r][i]
«» "
Si une ligne viole cela, la paire est invalide.

La réponse est `m - max(dp)`.

- Oui. 5. Code en 3 langues

C'est vrai. Java
"Java
solution de classe publique {
public int minDeletionSize(String[] strs) {
int n = longueur des chaînes, m = longueur des chaînes[0].
int[] dp = nouvelle int[m];
int best = 0;

pour (int i = 0; i < m; i++) {
dp[i] = 1;
pour (int j = 0; j < i; j++) {
si (peutprécéder(strs, j, i)) {
dp[i] = Math.max(dp[i], dp[j] + 1);
}
}
best = Math.max(best, dp[i]);
}
retour m - meilleur;
}

boîte de booléen privéePrecede(String[] strs, int j, int i) {
pour (String s : strs) {
si (s.charAt(j) > s.charAt(i)) retourne faux;
}
retour vrai;
}
}
«» "

Python
'`python
Solution de classe:
def minDélétion Taille(self, strs: List[str]) -> Int:
n, m = len(strs), len(strs[0)]
dp = [1] * m
meilleur = 0

pour i dans la plage (m):
pour j dans la plage i:
si tous(s[j] <= s[i] pour s dans strs):
dp[i] = max(dp[i], dp[j] + 1)
best = max(best, dp[i])

retour m - meilleur
«» "

C++
'`cpp
solution de classe {
public:
int minDeletionSize(vecteur<string>& strs) {
int n = strs.size(), m = strs[0].size();
vecteur<int> dp(m, 1);
int best = 0;

pour (int i = 0; i < m; ++i) {
pour (int j = 0; j < i; ++j) {
bool ok = true;
pour (int r = 0; r < n; ++r)
si (strs[r][j] > strs[r][i]) { ok = faux; casser; }
si (ok) dp[i] = max(dp[i], dp[j] + 1;
}
best = max(best, dp[i]);
}
retour m - meilleur;
}
};
«» "

- Oui. 6. Analyse de la complexité

- **Heure:** `O(m2 · n)` – au maximum `100 * 100 * 100 = 1 000 000 ' opérations, négligeables.
- **Espace:** `O(m)` – un tableau DP.

- Oui. 7. Erreurs courantes d'entrevue

Pourquoi il échoue
- C'est quoi ?
**En supposant que seules les rangées adjacentes ont une matière**. Coupez toutes les lignes en vérifiant une paire. Autres
**En utilisant `m2` mais en ignorant `n`**.Les comparaisons de rangées négligées rendent le DP invalide. Autres
**Les erreurs hors-par-un sont fréquentes avec les chaînes 0. Stick à 0 indices tout au long. Autres
**Retour `m - max(dp)` Si vous oubliez de soustraire de `m`, la réponse sera `max(dp)` à la place. Autres

- Oui. 8. Pourquoi cela compte pour votre carrière

- ** Programmation dynamique :** La maîtrise du PDD sur un tableau 2-D démontre une forte pensée algorithmique, essentielle aux rôles de backend, d'ingénierie de données ou de pile complète.
- **Compétences linguistiques multiples:** Savoir mettre en œuvre la même logique dans **Java**, **Python** et **C++** met en valeur la polyvalence; les recruteurs apprécient les candidats qui peuvent changer de contexte.
- **Décomposition du problème :** Reconnaître l'analogie LIS montre votre capacité à résumer une exigence complexe en un sous-problème plus simple – une compétence d'entrevue appréciée.

- Oui. 9. Prochaines étapes

1. Exécutez les solutions fournies contre les cas de tests aléatoires (Les tests cachés de LeetCode sont souvent importants).
2. Ajoutez vos propres tests unitaires pour les scénarios de bord (`m=1`, déjà triés, complètement non triés).
3. Pratique expliquant à haute voix la formule du PDD – les intervieweurs veulent que vous réfléchissiez sur place.

- Oui. 9. Conclusion

Levet Le code 960 est une introduction douce mais puissante à la programmation dynamique sur matrices. En traitant le problème comme un LIS sur les colonnes et en utilisant un "O(m2·n) propre" DP, vous pouvez le résoudre efficacement dans n'importe quelle langue. Gardez le code simple, manipulez toutes les lignes et évitez les pièges communs. Bonne chance pour résoudre ce problème – et votre prochaine interview d'ingénierie logicielle!

---

#### 9.1. Liste de contrôle rapide pour les intervieweurs

- **Lisez attentivement l'invite** – colonnes vs lignes.
- ** Expliquez votre approche** avant le codage.
- **Ecrire les fonctions d'aide** pour la lisibilité.
- **Testez votre solution mentalement** sur tous les échantillons.
- **Complexité des mentions** pour faire preuve de sensibilisation.

---

** Bon codage !**

---

> *Vous voulez plus d'entrevue ? Abonnez-vous à notre bulletin hebdomadaire pour des analyses approfondies des problèmes de LeetCode, des modèles d'algorithmes et des histoires d'interview réelles. *

---

Mots clés

- Supprimer les colonnes à faire trier III
- LeetCode 960
- Solution DP
- Programmation dynamique
- Subséquence la plus longue
- Mise en œuvre Java
- Solution Python
- Algorithme C++
- Entretien en génie logiciel
- Codage des modèles d'entrevue

---

** Fin de l'article. **