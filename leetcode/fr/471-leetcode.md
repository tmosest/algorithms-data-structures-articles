---
titre: LeetCode 471. Chaîne de code avec longueur la plus courte -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
---

# 471. **Encoder la chaîne avec la longueur la plus courte**
> **Hard** – LeetCode

> **Problème**:
> On vous donne une chaîne `s` composée seulement de lettres minuscules.
> Encodez-le en utilisant la règle `k[encoded_string]` où le `encoded_string` est répété exactement `k` fois.
> La chaîne codée doit être **plus courte** que l'original; sinon, conservez l'original.
> Retournez *any* encodage le plus court possible.

> **Exemples**

Entrée Sortie Explication
C'est pas vrai.
""aaa" ""aaa" """"""" Pas d'encodage le rend plus court
""aaaaa""""5[a]""""5[a]" est plus court"
""aaaaaaaaaaaaaaaaaaaaa" ""10[a]" ""10[a]" ", "9[a]a" ", "a9[a]" " ont tous la même longueur minimale"

> **Constraints**
> `1 ≤ longueur ≤ 150`
> `s` ne contient que des lettres anglaises minuscules.

---

Pourquoi ça compte

- Oui. Le problème est une question **classique d'entrevue** qui teste la programmation dynamique, la manipulation de chaînes et la créativité dans la manipulation des cas de bord.
- Oui. Il s'agit d'une excellente vitrine pour votre capacité à concevoir des solutions optimales** pour les problèmes de cordes *non-trivial* – une compétence essentielle pour les ingénieurs de front-end/back-end, les data savants et les rôles algorithmiques.
- Une mise en œuvre correcte et bien commentée de ce problème démontre la compétence dans *Java*, *Python* et *C++*, les trois langages de programmation les plus recherchés par l'embauche de gestionnaires.

---

## Aperçu de la solution

La solution optimale est un DP **3-dimensionnel** qui fonctionne dans le temps `O(n3)` (avec `n ≤ 150`, c'est parfaitement bien).

1. ** Tableau PD**
`dp[i][j]` = *chaîne encodée la plus courte* pour la sous-chaîne `s[i ... j]`.

2. **Initialisation**
Pour chaque caractère unique `dp[i][i] = s[i]`.

3. **Répétition**
Pour chaque longueur `len` de `2` à `n "
- **Split** la sous-chaîne en deux parties `s[i ... k]` et `s[k+1 ... j]`.
«dp[i][j] = min(dp[i][k] + dp[k+1][j]»
- **Vérifier la répétition**:
Laissez la longueur de sous-chaîne être "len".
Pour chaque diviseur `k` de `len` (à l ' exclusion de `len` lui-même):
*Si la sous-chaîne est faite de répétitions `len / k` de ses premiers caractères `k`, nous pouvons l'encoder comme
"cnt[k] + "[" + dp[i][i+k-1] + "]"".
Gardez le résultat le plus court.

4. **Retour** `dp[0][n-1]`.

**Aide clé** – 'findPatternLength(sub)'
Vérifie la période minimale d'une chaîne dans `O(len)` en utilisant la fonction de préfixe KMP. Il est utilisé pour identifier efficacement les motifs répétés.

---

Code

Ci-dessous sont trois solutions propres et entièrement commentées : une dans **Java**, une dans **Python** et une dans **C++**.

> **Note**: Tous les trois utilisent la même logique et peuvent être copiés dans votre IDE ou boîte de soumission.

---

C'est pas vrai. Java

"Java
Importation de java.util.*;

solution de classe publique {
chaîne publique encode(chaîne s) {
int n = s.longueur();
Chaîne[][] dp = nouvelle chaîne[n][n];

// 1. lettres uniques
pour (int i = 0; i < n; i++) dp[i][i] = String.valueDe(s.charAt(i));

// 2. PDD pour toutes les longueurs
pour (int len = 2; len <= n; len++) {
pour (int i = 0; i + len - 1 < n; i++) {
j = i + len - 1;
dp[i][j] = s.substring(i, j + 1); // initial: la sous-chaîne brute

// 2.1 Séparer
pour (int k = i; k < j; k++) {
Candidat à la chaîne = dp[i][k] + dp[k + 1][j];
si [candidate.longueur() < dp[i][j].longueur()
dp[i][j] = candidat;
}

2.2 Répétition
int patternLen = findPatternLen(s.substring(i, j + 1));
si (patternLen < len) { // seulement si nous avons trouvé une répétition
temps int = len / motif Len;
Chaîne encodée = heures + "[" + dp[i][i + patternLen - 1] + "];
si (encodé.longueur() < dp[i][j].longueur()
dp[i][j] = encodé;
}
}
}
retour dp[0][n - 1];
}

// Fonction de préfixe KMP pour trouver une période minimale
Recherche privéePatternLen(String sub) {
int n = longueur inférieure();
int[] lps = nouvelle int[n];
pour (int i = 1, len = 0; i < n; ) {
si (sub.charAt(i) == sub.charAt(len) {
lps[i++] = ++len;
} sinon si (len != 0) {
len = lps[len - 1];
} autre {
lps[i++] = 0;
}
}
période int = n - lps[n - 1];
retour (n % période) 0) ? période : n;
}
}
«» "

---

# # # # # #

'`python
Solution de classe:
def encode(self, s: str) -> str:
n = len(s)
dp = [[""] * n pour _ dans l'intervalle(n)]

Lettres uniques
pour i dans la plage(n):
dp[i][i] = s[i]

# DP pour toutes les longueurs
pour la longueur de portée(2, n + 1):
pour i dans la plage (n - longueur + 1):
j = i + longueur - 1
Sous = s[i:j + 1]
dp[i][j] = sous- # sous-chaîne brute

# Séparer
pour k dans la plage(i, j):
Cand = dp[i][k] + dp[k + 1][j]
si len(cand) < len(dp[i][j]:
dp[i][j] = cand

# Répétition
période = auto_période(sub)
si période < longueur: # répétition existe
durée = longueur // période
Cand = f"{times}[{dp[i][i + période - 1]}]"
si len(cand) < len(dp[i][j]:
dp[i][j] = cand

retour dp[0][n - 1]

def _period(self, s: str) -> Int:
"""Retourne la période minimale de la chaîne s (en utilisant KMP)."""
n = len(s)
lps = [0] * n
pour i dans la plage (1, n):
j = lps[i - 1]
alors que j > 0 et s[i] != [j]:
j = lps[j - 1]
si s[i] == [j]:
j += 1
lps[i] = j
période = n - lps[-1]
période de retour si n % période 0 autre n
«» "

---

C'est vrai. C++

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

solution de classe {
public:
chaîne encode(chaîne s) {
int n = s.size();
vector<vector<string>> dp(n, vector<string>(n));

// lettres uniques
pour (int i = 0; i < n; ++i) dp[i]i] = chaîne(1, s[i]);

pour (int len = 2; len <= n; + len) {
pour (int i = 0; i + len - 1 < n; ++i) {
j = i + len - 1;
chaîne sub = s.substr(i, len);
dp[i][j] = sous-chaîne // brute

// Séparer
pour (int k = i; k < j; ++k) {
Cand chaîne = dp[i][k] + dp[k + 1][j];
si (cand.size() < dp[i][j].size()
dp[i][j] = cand;
}

// Répétition
période int = findPeriod(sub);
si (période < len) { // nous avons trouvé une répétition
temps int = len / période;
chaîne cand = to_string(times) + "[" + dp[i][i + période - 1] + "]";
si (cand.size() < dp[i][j].size()
dp[i][j] = cand;
}
}
}
retour dp[0][n - 1];
}

particulier:
int findPeriod(chaîne de &s Const) {
int n = s.size();
vecteur<int> lps(n, 0);
pour (int i = 1, len = 0; i < n; ) {
si (s[i] == s[len]) lps[i++] = ++len;
si (len) len = lps[len - 1];
autres lps[i++] = 0;
}
période int = n - lps[n - 1];
retour (n % période) 0) ? période : n;
}
};
«» "

---

## Blog Post – Encoder String avec la longueur la plus courte: Le Bon, le Mauvais, et le Ugly

- Oui. 1. Présentation

Lors d'un entretien pour un rôle **logiciel**, vous tomberez inévitablement sur des problèmes de codage de cordes. L'un des plus populaires est **LeetCode 471 – Encode String with Shortest Length**. Il vous demande de compresser une chaîne dans sa représentation la plus courte possible en utilisant une simple syntaxe `k[encoded_string]`.

Pourquoi ce problème est-il un *must-know*?

- Oui. Il mélange **programmation dynamique** avec **transformation de chaînes**.
- Oui. Il révèle comment vous traitez les cas de base** et **optimisation**.
- Oui. Il démontre votre capacité à produire **un code propre et durable** dans plusieurs langues – exactement ce que les recruteurs recherchent sur LinkedIn et GitHub.

Cet article passe par les problèmes **bon** (ce qui fonctionne bien), les **mauvais** (pièges communs) et les **ugly** (cas de pointe qui voyagent même les programmeurs chevronnés). À la fin, vous aurez une solution éprouvée pour toute entrevue de codage.

---

- Oui. 2. Le bien: ce qui fait Ce problème est résolu

Pourquoi ça aide ?
C'est quoi ?
**Extrait déterministe**= Vous avez toujours besoin de la chaîne encodée la plus courte*. Pas de hasard. Autres
Autres **Petite taille d'entrée** (`- 150`) Solution DP sans soucis de délai. Autres
**Fixed Syntax** (`k[... ]`)= Aucune ambiguïté; vous pouvez diviser ou coder de façon fiable. Autres
Autres **Solf-Containment**.La chaîne n'est que des lettres minuscules – pas de caractères spéciaux pour s'échapper. Autres

Ces contraintes rendent naturel un PDD ascendant :

1. **Sous-problème** – coder une sous-chaîne `s[i..j]`.
2. **Transition** – fractionner la sous-chaîne ou la compresser si elle est une répétition.
3. **Base** – les caractères simples sont déjà encodés.

Parce que vous pouvez calculer chaque plus petite sous-chaîne d'abord, la table DP remplit de petites à grandes sous-chaînes. L'algorithme résultant est à la fois intuitif et efficace.

---

- Oui. 3. Le mauvais: les pièges communs et pourquoi il est tombé à l'écart

"Piège" "Ce qui ne va pas"
C'est-à-dire
**Utiliser `int` pour count**= Si vous codez =aaaaa...(1000 fois)=, convertir le compte en une chaîne incorrectement (dépassement)== Toujours convertir le *int* en une chaîne (`String.valueOf(count)` ou `to_string(count)`). Autres
Autres **Vérification de la répétition naïve** Utiliser la fonction *prefix (KMP)* pour trouver la période minimale dans `O(n)`. Autres
**Ignorer déjà les sous-chaînes optimales**= Si une scission donne la même longueur que la sous-chaîne brute, vous pourriez l'écraser inutilement== Garder la sous-chaîne *originale* comme un repli et ne remplacer que lorsque le nouveau codage est strictement plus court. Autres
**Index off‐by‐one**= Les tables DP utilisent souvent `dp[i][j]` ce qui signifie `i` inclusive, `j` exclusive; l'erreur d'appariement conduit à des bugs==Choisir une convention (inclusive-inclusive ou inclusive-exclusive) et s'y tenir tout au long. Autres
Autres **Récursifs avec mémoisation mais manquants la règle de l'encodage**.Vous pouvez retourner une chaîne compressée qui *n'est pas plus courte*, violant l'instruction du problème. Autres

---

- Oui. 4. Les horribles cas de bord qui peuvent vous faire monter

1. **Ficelles très courtes* *
`s = "a"` – devrait retourner `"a"`.
**Pourquoi?** Une solution DP peut essayer de se diviser en pièces vides. Garder contre "i".

2. **Plusieurs solutions optimales* *
Les termes "aaaaaaaaaaaaa" peuvent être encodés comme suit: ""10a"`, "9aa"`, "a9a"".
**Pourquoi?** Le DP n'a besoin que de * n'importe quel * le plus court, mais votre implémentation pourrait involontairement renvoyer une chaîne plus longue encodée si la comparaison n'est pas stricte (`<=` au lieu de `<`).

3. ** Nombre de répétitions importantes**
`"abababab..."` répété 50 fois – le nombre devient 50.
**Pourquoi?** La conversion de l'entier en une chaîne peut prendre plusieurs chiffres, rendant la chaîne codée plus longue que la chaîne brute. Toujours comparer les longueurs complètes.

4. **Encodage nesté**
`"aaaaaa"` → `=6[a]=" est optimal, mais `=3[2[a]=" est aussi de 6 caractères.
**Pourquoi?** Le DP doit tenir compte des patrons imbriqués correctement. La détection minimale des périodes s'en charge automatiquement.

5. **Longues non divisibles**
`"abcab"` – pas une répétition complète.
**Pourquoi?** La détection de la période doit renvoyer la longueur d'origine; sinon, vous pourriez mal l'encoder comme étant `1[abcabcab]`.

---

- Oui. 5. La marche du PDD

Texte
dp[i][j] – codage le plus court pour s[i...j]
«» "

1. **Initialisation**
`dp[i][i] = s[i] "

2. **Longueur** ( 'len ' de 2 à n)

Pour chaque `i`, définir `j = i + len - 1'

- **Démarrer avec la sous-chaîne brute* *
`dp[i][j] = s[i...j] "
- **Essayez chaque fraction** `k` (`i ≤ k < j`)
`cand = dp[i][k] + dp[k+1][j] "
Si `cand` plus court → `dp[i][j] = cand "
- **Vérifier la répétition**
«période = minimumPériode(s[i...j]) "
Si `période < len` → répétition existe
`cand = nombre + '[' + dp[i][i+période-1] + ']'
Remplacer si strictement plus court.

3. **Résultat** – `dp[0][n-1]`

Le *période* est trouvé en utilisant KMP dans `O(len)`. Ainsi, la complexité globale est `O(n3)` (longueur × scissions) avec un contrôle supplémentaire de répétition `O(n)` à l'intérieur de chaque itération.

---

- Oui. 6. Multi-langue Maîtrise

Les recruteurs demandent souvent : Quelle est votre langue préférée pour une entrevue de codage?
Un candidat fort démontre sa compétence dans au moins:

- **Java** (ou Kotlin) – pile d'entreprise
- **Python** – prototypage rapide, science des données
- **C++** – programmation de systèmes, concours d'algorithmes

Les solutions que nous avons présentées plus tôt sont presque identiques entre les langues, en soulignant :

- **Réutilisabilité** – même logique, juste changements de syntaxe de langage.
- **Readability** – noms de variables clairs, indices DP cohérents.
- **Modularité** – fonctions d'aide pour la détection des périodes KMP et la conversion des chaînes.

Lorsque vous présentez ces solutions sur GitHub ou lors d'une entrevue, vous montrerez que vous pouvez *adapter* plutôt que *copier-coller*.

---

- Oui. 6. Liste de contrôle à emporter

- [ ] **Cas de base**: `dp[i][i] = s[i] "
- [ ] **Toujours garder la sous-chaîne brute** si rien de plus court est trouvé.
- [ ] **Utilisez KMP** (fonction de préfixe) pour trouver une période minimale.
- [ ] **Comparer les longueurs** après avoir généré un candidat encodé.
- [ ] **Éviter le débordement entier** – convertir le nombre en chaîne avant de comparer.
- [ ] **Cas de bord de test**: char simple, motifs imbriqués, nombres à chiffres élevés.

Exécutez votre implémentation contre les cas de test *code dur* et quelques cas de bord *client* pour être sûr.

---

- Oui. 7. Mot final

LeetCode 471 est plus qu'un puzzle amusant ; c'est un test litmus pour votre pensée algorithmique. Maîtrisez-le, et vous :

- Gagner **Les badges Top Interviewer** sur les plateformes comme LeetCode.
- Oui. Ayez une solution prête à coller** pour votre prochain cycle de codage.
- Impress recruteurs à la recherche de programmation dynamique + manipulation de chaînes de caractères sur LinkedIn.

Bon codage, et que votre prochaine interview soit aussi *court* et *optimal* que votre encodage!

---

- Oui. 8. Ressources connexes

- [Principaux de programmation dynamique](https://leetcode.com/discuss/interview-question/12620/DP-en-10 minutes)
(https://www.geeksforgeeks.org/knuth-morris-pratt-algorithm/)
- [LeetCode 472 – Mots concaténés] (https://leetcode.com/problèmes/mots concaténés/)
- [LeetCode 451 – Tri des caractères Par fréquence](https://leetcode.com/problèmes/sort-caracters-by-fréquence/)

---

- Oui. 9. Appel à l ' action

Vous avez votre propre mise en œuvre ? **Partager** sur GitHub, l'étiqueter avec `#leetcode471`, et faire savoir à la communauté. Vous voulez pratiquer plus de problèmes de cordes ? **Rejoignez notre défi d'entrevue de 30 jours** et commencez par celui-ci aujourd'hui!

---

10 ans. Références

- Problème de LeetCode 471
- Algorithme KMP sur GeeksforGeeks
- Programmation dynamique – *Introduction aux algorithmes* (CLRS)

---

> *Souvenez-vous: dans le codage des interviews, **clarity** bat *cleverness*. L'approche du PDD ci-dessus en témoigne. Bonne chance ! *

---

- Oui. 6. Conclusion

Vous avez maintenant :

- Une solution testée ** en Java, Python et C++.
- Une feuille de route** pour éviter les pièges habituels.
- A **blog post** qui met en valeur votre compréhension profonde – parfait pour Linked Dans ou dans votre portefeuille.

Lorsque les recruteurs recherchent l'encodage de chaîne de programmation dynamique, ils trouveront votre code, votre polyvalence linguistique et votre explication de problème poli. C'est exactement ce qui fait qu'un candidat *se démarque*.

Joyeux entretien !

---

*Sentez-vous libre de commenter, partager ou fourcher le code. Laissez-les continuer la conversation ! *